# Moorsyl Java SDK

Official Java client for the [Moorsyl API](https://docs.moorsyl.com) — send SMS, verify phone numbers, and react to events in Mauritania.

- Documentation — [docs.moorsyl.com](https://docs.moorsyl.com)
- Source — [github.com/SoftwareSavants/moorsyl-java](https://github.com/SoftwareSavants/moorsyl-java)
- Maven Central — [`com.moorsyl:moorsyl-java`](https://central.sonatype.com/artifact/com.moorsyl/moorsyl-java)

## Installation

### Maven

```xml
<dependency>
  <groupId>com.moorsyl</groupId>
  <artifactId>moorsyl-java</artifactId>
  <version>1.0.3</version>
</dependency>
```

### Gradle

```groovy
implementation 'com.moorsyl:moorsyl-java:1.0.3'
```

## Initialization

```java
import com.moorsyl.ApiClient;
import com.moorsyl.api.SmsApi;
import com.moorsyl.api.VerifyApi;

ApiClient client = new ApiClient();
client.setApiKey("sk_live_...");

SmsApi sms = new SmsApi(client);
VerifyApi verify = new VerifyApi(client);
```

The SDK defaults to `https://api.moorsyl.com/api`. Override with `client.setBasePath(...)` if needed.

## Send an SMS

Requires a secret key (`sk_…`). See [API Keys](https://docs.moorsyl.com/api-keys).

```java
import com.moorsyl.ApiClient;
import com.moorsyl.api.SmsApi;
import com.moorsyl.model.SmsSendRequest;
import com.moorsyl.model.SmsSend200Response;

ApiClient client = new ApiClient();
client.setApiKey("sk_live_...");

SmsApi sms = new SmsApi(client);

SmsSendRequest request = new SmsSendRequest()
    .to("+22236551999")
    .from("MyBrand")
    .body("Your order #1042 has been shipped.");

SmsSend200Response response = sms.smsSend(request);

System.out.println("Accepted: " + response.getAccepted());
System.out.println("Idempotency key: " + response.getIdempotencyKey());
```

Supply `idempotencyKey` to prevent duplicate sends on retries:

```java
SmsSendRequest request = new SmsSendRequest()
    .to("+22236551999")
    .from("MyBrand")
    .body("Your code is 847291")
    .idempotencyKey("otp-user42-20240101T120000");

sms.smsSend(request);
```

## Phone Verification

Use a publishable key (`pk_…`) so this code can run safely in client-facing contexts. See [API Keys](https://docs.moorsyl.com/api-keys).

```java
import com.moorsyl.ApiClient;
import com.moorsyl.api.VerifyApi;

ApiClient client = new ApiClient();
client.setApiKey("pk_live_...");

VerifyApi verify = new VerifyApi(client);
```

### Send a verification code

```java
import com.moorsyl.model.VerifySendRequest;
import com.moorsyl.model.VerifySend200Response;

VerifySend200Response sendResponse = verify.verifySend(
    new VerifySendRequest().to("+22236551999")
);

String verificationId = sendResponse.getVerificationId();
```

### Check the code

```java
import com.moorsyl.model.VerifyCheckRequest;
import com.moorsyl.model.VerifyCheck200Response;

VerifyCheck200Response checkResponse = verify.verifyCheck(
    new VerifyCheckRequest()
        .verificationId(verificationId)
        .code(userEnteredCode)
);

if (checkResponse.getStatus() == VerifyCheck200Response.StatusEnum.APPROVED) {
    // phone is verified — proceed
}
```

### Full flow

```java
import com.moorsyl.ApiClient;
import com.moorsyl.api.VerifyApi;
import com.moorsyl.model.*;

public class PhoneVerification {
    public static boolean verifyPhoneNumber(String phoneNumber, String userCode) throws Exception {
        ApiClient client = new ApiClient();
        client.setApiKey("pk_live_...");
        VerifyApi verify = new VerifyApi(client);

        // Step 1 — send the code
        VerifySend200Response sendResponse = verify.verifySend(
            new VerifySendRequest().to(phoneNumber)
        );

        // Step 2 — check the code the user entered
        VerifyCheck200Response checkResponse = verify.verifyCheck(
            new VerifyCheckRequest()
                .verificationId(sendResponse.getVerificationId())
                .code(userCode)
        );

        return checkResponse.getStatus() == VerifyCheck200Response.StatusEnum.APPROVED;
    }
}
```

## Error Handling

API methods throw `ApiException` on non-2xx responses:

```java
import com.moorsyl.ApiException;

try {
    sms.smsSend(new SmsSendRequest()
        .to("+22236551999")
        .from("MyBrand")
        .body("Hello!"));
} catch (ApiException e) {
    System.out.println("Status: " + e.getCode());
    System.out.println("Body: " + e.getResponseBody());
}
```

Common status codes are documented on the [SMS](https://docs.moorsyl.com/sms) and [Verify](https://docs.moorsyl.com/verify) pages.

## Webhook Signature Verification

Verify incoming webhook signatures to ensure requests are genuine. See [Webhooks](https://docs.moorsyl.com/webhooks).

```java
import javax.crypto.Mac;
import javax.crypto.spec.SecretKeySpec;
import java.security.MessageDigest;
import java.util.Base64;

public class WebhookVerifier {
    public static boolean verify(String rawBody, String header, String secret) {
        try {
            String[] pairs = header.split(",");
            String timestamp = null, signature = null;

            for (String pair : pairs) {
                String[] kv = pair.split("=", 2);
                if ("t".equals(kv[0])) timestamp = kv[1];
                if ("v1".equals(kv[0])) signature = kv[1];
            }

            if (timestamp == null || signature == null) return false;

            long age = System.currentTimeMillis() / 1000 - Long.parseLong(timestamp);
            if (age > 300) return false;

            byte[] keyBytes = Base64.getDecoder().decode(secret.replace("whsec_", ""));
            Mac mac = Mac.getInstance("HmacSHA256");
            mac.init(new SecretKeySpec(keyBytes, "HmacSHA256"));

            byte[] hash = mac.doFinal((timestamp + "." + rawBody).getBytes());
            String expected = bytesToHex(hash);

            return MessageDigest.isEqual(expected.getBytes(), signature.getBytes());
        } catch (Exception e) {
            return false;
        }
    }

    private static String bytesToHex(byte[] bytes) {
        StringBuilder sb = new StringBuilder();
        for (byte b : bytes) sb.append(String.format("%02x", b));
        return sb.toString();
    }
}
```

## Requirements

- Java 8+
- Maven 2.2+ or Gradle

## Other SDKs

- [TypeScript / JavaScript](https://www.npmjs.com/package/@moorsyl/sdk)
- [Dart / Flutter](https://docs.moorsyl.com/dart)

## License

MIT

# VerifyApi

All URIs are relative to *https://api.moorsyl.com/api*

| Method | HTTP request | Description |
|------------- | ------------- | -------------|
| [**verifyCheck**](VerifyApi.md#verifyCheck) | **POST** /verify/check | Check a verification code |
| [**verifyGet**](VerifyApi.md#verifyGet) | **POST** /verify/get | Get verification status |
| [**verifySend**](VerifyApi.md#verifySend) | **POST** /verify/send | Send a verification code |


<a id="verifyCheck"></a>
# **verifyCheck**
> VerifyCheck200Response verifyCheck(verifyCheckRequest)

Check a verification code

Validate the one-time code entered by the user and return approved for a correct match, or denied when the code is incorrect, expired, or already used.

### Example
```java
// Import classes:
import com.moorsyl.ApiClient;
import com.moorsyl.ApiException;
import com.moorsyl.Configuration;
import com.moorsyl.auth.*;
import com.moorsyl.models.*;
import com.moorsyl.api.VerifyApi;

public class Example {
  public static void main(String[] args) {
    ApiClient defaultClient = Configuration.getDefaultApiClient();
    defaultClient.setBasePath("https://api.moorsyl.com/api");
    
    // Configure API key authorization: ApiKey
    ApiKeyAuth ApiKey = (ApiKeyAuth) defaultClient.getAuthentication("ApiKey");
    ApiKey.setApiKey("YOUR API KEY");
    // Uncomment the following line to set a prefix for the API key, e.g. "Token" (defaults to null)
    //ApiKey.setApiKeyPrefix("Token");

    VerifyApi apiInstance = new VerifyApi(defaultClient);
    VerifyCheckRequest verifyCheckRequest = new VerifyCheckRequest(); // VerifyCheckRequest | 
    try {
      VerifyCheck200Response result = apiInstance.verifyCheck(verifyCheckRequest);
      System.out.println(result);
    } catch (ApiException e) {
      System.err.println("Exception when calling VerifyApi#verifyCheck");
      System.err.println("Status code: " + e.getCode());
      System.err.println("Reason: " + e.getResponseBody());
      System.err.println("Response headers: " + e.getResponseHeaders());
      e.printStackTrace();
    }
  }
}
```

### Parameters

| Name | Type | Description  | Notes |
|------------- | ------------- | ------------- | -------------|
| **verifyCheckRequest** | [**VerifyCheckRequest**](VerifyCheckRequest.md)|  | |

### Return type

[**VerifyCheck200Response**](VerifyCheck200Response.md)

### Authorization

[ApiKey](../README.md#ApiKey)

### HTTP request headers

 - **Content-Type**: application/json
 - **Accept**: application/json

### HTTP response details
| Status code | Description | Response headers |
|-------------|-------------|------------------|
| **200** | OK |  -  |

<a id="verifyGet"></a>
# **verifyGet**
> VerifyGet200Response verifyGet(verifySend200Response)

Get verification status

Retrieve the current status and details of a phone verification by its ID.

### Example
```java
// Import classes:
import com.moorsyl.ApiClient;
import com.moorsyl.ApiException;
import com.moorsyl.Configuration;
import com.moorsyl.auth.*;
import com.moorsyl.models.*;
import com.moorsyl.api.VerifyApi;

public class Example {
  public static void main(String[] args) {
    ApiClient defaultClient = Configuration.getDefaultApiClient();
    defaultClient.setBasePath("https://api.moorsyl.com/api");
    
    // Configure API key authorization: ApiKey
    ApiKeyAuth ApiKey = (ApiKeyAuth) defaultClient.getAuthentication("ApiKey");
    ApiKey.setApiKey("YOUR API KEY");
    // Uncomment the following line to set a prefix for the API key, e.g. "Token" (defaults to null)
    //ApiKey.setApiKeyPrefix("Token");

    VerifyApi apiInstance = new VerifyApi(defaultClient);
    VerifySend200Response verifySend200Response = new VerifySend200Response(); // VerifySend200Response | 
    try {
      VerifyGet200Response result = apiInstance.verifyGet(verifySend200Response);
      System.out.println(result);
    } catch (ApiException e) {
      System.err.println("Exception when calling VerifyApi#verifyGet");
      System.err.println("Status code: " + e.getCode());
      System.err.println("Reason: " + e.getResponseBody());
      System.err.println("Response headers: " + e.getResponseHeaders());
      e.printStackTrace();
    }
  }
}
```

### Parameters

| Name | Type | Description  | Notes |
|------------- | ------------- | ------------- | -------------|
| **verifySend200Response** | [**VerifySend200Response**](VerifySend200Response.md)|  | |

### Return type

[**VerifyGet200Response**](VerifyGet200Response.md)

### Authorization

[ApiKey](../README.md#ApiKey)

### HTTP request headers

 - **Content-Type**: application/json
 - **Accept**: application/json

### HTTP response details
| Status code | Description | Response headers |
|-------------|-------------|------------------|
| **200** | OK |  -  |

<a id="verifySend"></a>
# **verifySend**
> VerifySend200Response verifySend(verifySendRequest)

Send a verification code

Send a one-time passcode via SMS to the specified Mauritanian phone number. Returns a verificationId to use with the check endpoint.

### Example
```java
// Import classes:
import com.moorsyl.ApiClient;
import com.moorsyl.ApiException;
import com.moorsyl.Configuration;
import com.moorsyl.auth.*;
import com.moorsyl.models.*;
import com.moorsyl.api.VerifyApi;

public class Example {
  public static void main(String[] args) {
    ApiClient defaultClient = Configuration.getDefaultApiClient();
    defaultClient.setBasePath("https://api.moorsyl.com/api");
    
    // Configure API key authorization: ApiKey
    ApiKeyAuth ApiKey = (ApiKeyAuth) defaultClient.getAuthentication("ApiKey");
    ApiKey.setApiKey("YOUR API KEY");
    // Uncomment the following line to set a prefix for the API key, e.g. "Token" (defaults to null)
    //ApiKey.setApiKeyPrefix("Token");

    VerifyApi apiInstance = new VerifyApi(defaultClient);
    VerifySendRequest verifySendRequest = new VerifySendRequest(); // VerifySendRequest | 
    try {
      VerifySend200Response result = apiInstance.verifySend(verifySendRequest);
      System.out.println(result);
    } catch (ApiException e) {
      System.err.println("Exception when calling VerifyApi#verifySend");
      System.err.println("Status code: " + e.getCode());
      System.err.println("Reason: " + e.getResponseBody());
      System.err.println("Response headers: " + e.getResponseHeaders());
      e.printStackTrace();
    }
  }
}
```

### Parameters

| Name | Type | Description  | Notes |
|------------- | ------------- | ------------- | -------------|
| **verifySendRequest** | [**VerifySendRequest**](VerifySendRequest.md)|  | |

### Return type

[**VerifySend200Response**](VerifySend200Response.md)

### Authorization

[ApiKey](../README.md#ApiKey)

### HTTP request headers

 - **Content-Type**: application/json
 - **Accept**: application/json

### HTTP response details
| Status code | Description | Response headers |
|-------------|-------------|------------------|
| **200** | OK |  -  |


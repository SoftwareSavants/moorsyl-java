# SmsApi

All URIs are relative to *https://api.moorsyl.com/api*

| Method | HTTP request | Description |
|------------- | ------------- | -------------|
| [**smsGet**](SmsApi.md#smsGet) | **POST** /sms/get | Get SMS status |
| [**smsSend**](SmsApi.md#smsSend) | **POST** /sms | Send an SMS |


<a id="smsGet"></a>
# **smsGet**
> SmsGet200Response smsGet(smsGetRequest)

Get SMS status

Retrieve the current status and details of a previously sent SMS message by its ID.

### Example
```java
// Import classes:
import com.moorsyl.ApiClient;
import com.moorsyl.ApiException;
import com.moorsyl.Configuration;
import com.moorsyl.auth.*;
import com.moorsyl.models.*;
import com.moorsyl.api.SmsApi;

public class Example {
  public static void main(String[] args) {
    ApiClient defaultClient = Configuration.getDefaultApiClient();
    defaultClient.setBasePath("https://api.moorsyl.com/api");
    
    // Configure API key authorization: ApiKey
    ApiKeyAuth ApiKey = (ApiKeyAuth) defaultClient.getAuthentication("ApiKey");
    ApiKey.setApiKey("YOUR API KEY");
    // Uncomment the following line to set a prefix for the API key, e.g. "Token" (defaults to null)
    //ApiKey.setApiKeyPrefix("Token");

    SmsApi apiInstance = new SmsApi(defaultClient);
    SmsGetRequest smsGetRequest = new SmsGetRequest(); // SmsGetRequest | 
    try {
      SmsGet200Response result = apiInstance.smsGet(smsGetRequest);
      System.out.println(result);
    } catch (ApiException e) {
      System.err.println("Exception when calling SmsApi#smsGet");
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
| **smsGetRequest** | [**SmsGetRequest**](SmsGetRequest.md)|  | |

### Return type

[**SmsGet200Response**](SmsGet200Response.md)

### Authorization

[ApiKey](../README.md#ApiKey)

### HTTP request headers

 - **Content-Type**: application/json
 - **Accept**: application/json

### HTTP response details
| Status code | Description | Response headers |
|-------------|-------------|------------------|
| **200** | OK |  -  |

<a id="smsSend"></a>
# **smsSend**
> SmsSend200Response smsSend(smsSendRequest)

Send an SMS

Send a text message to a Mauritanian phone number. The message is queued immediately and delivered through Mauritania-optimized carrier routing.

### Example
```java
// Import classes:
import com.moorsyl.ApiClient;
import com.moorsyl.ApiException;
import com.moorsyl.Configuration;
import com.moorsyl.auth.*;
import com.moorsyl.models.*;
import com.moorsyl.api.SmsApi;

public class Example {
  public static void main(String[] args) {
    ApiClient defaultClient = Configuration.getDefaultApiClient();
    defaultClient.setBasePath("https://api.moorsyl.com/api");
    
    // Configure API key authorization: ApiKey
    ApiKeyAuth ApiKey = (ApiKeyAuth) defaultClient.getAuthentication("ApiKey");
    ApiKey.setApiKey("YOUR API KEY");
    // Uncomment the following line to set a prefix for the API key, e.g. "Token" (defaults to null)
    //ApiKey.setApiKeyPrefix("Token");

    SmsApi apiInstance = new SmsApi(defaultClient);
    SmsSendRequest smsSendRequest = new SmsSendRequest(); // SmsSendRequest | 
    try {
      SmsSend200Response result = apiInstance.smsSend(smsSendRequest);
      System.out.println(result);
    } catch (ApiException e) {
      System.err.println("Exception when calling SmsApi#smsSend");
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
| **smsSendRequest** | [**SmsSendRequest**](SmsSendRequest.md)|  | |

### Return type

[**SmsSend200Response**](SmsSend200Response.md)

### Authorization

[ApiKey](../README.md#ApiKey)

### HTTP request headers

 - **Content-Type**: application/json
 - **Accept**: application/json

### HTTP response details
| Status code | Description | Response headers |
|-------------|-------------|------------------|
| **200** | OK |  -  |


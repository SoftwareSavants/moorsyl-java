

# SmsGet200Response


## Properties

| Name | Type | Description | Notes |
|------------ | ------------- | ------------- | -------------|
|**id** | **String** |  |  |
|**to** | **String** |  |  |
|**from** | **String** |  |  |
|**body** | **String** |  |  |
|**status** | [**StatusEnum**](#StatusEnum) |  |  |
|**createdAt** | **OffsetDateTime** |  |  |
|**updatedAt** | **OffsetDateTime** |  |  |



## Enum: StatusEnum

| Name | Value |
|---- | -----|
| PENDING | &quot;pending&quot; |
| PROCESSING | &quot;processing&quot; |
| SENT | &quot;sent&quot; |
| FAILED | &quot;failed&quot; |




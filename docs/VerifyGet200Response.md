

# VerifyGet200Response


## Properties

| Name | Type | Description | Notes |
|------------ | ------------- | ------------- | -------------|
|**id** | **String** |  |  |
|**to** | **String** |  |  |
|**status** | [**StatusEnum**](#StatusEnum) |  |  |
|**attempts** | **BigDecimal** |  |  |
|**expiresAt** | **OffsetDateTime** |  |  |
|**createdAt** | **OffsetDateTime** |  |  |
|**updatedAt** | **OffsetDateTime** |  |  |



## Enum: StatusEnum

| Name | Value |
|---- | -----|
| PENDING | &quot;pending&quot; |
| APPROVED | &quot;approved&quot; |
| EXPIRED | &quot;expired&quot; |
| CANCELED | &quot;canceled&quot; |




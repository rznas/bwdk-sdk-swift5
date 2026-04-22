# ShippingMethod

## Properties
Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**id** | **Int** |  | [readonly] 
**name** | **String** | نام روش ارسال | 
**description** | **String** | توضیحات روش ارسال و جزئیات تحویل آن | [optional] 
**shippingType** | [**ShippingTypeEnum**](ShippingTypeEnum.md) | نوع روش ارسال: عادی یا دیجی اکسپرس  * &#x60;1&#x60; - سایر * &#x60;2&#x60; - دیجی اکسپرس | [optional] 
**getShippingTypeDisplay** | **String** |  | [readonly] 
**shippingTypeDisplay** | **String** |  | [readonly] 
**cost** | **Int** | هزینه ارسال برای منطقه اولیه (مثلاً تهران) به تومان | [optional] 
**secondaryCost** | **Int** | هزینه ارسال برای مناطق دیگر به تومان | [optional] 
**minimumTimeSending** | **Int** | حداقل تعداد روزها از تاریخ سفارش تا تحویل | [optional] 
**maximumTimeSending** | **Int** | حداکثر تعداد روزها از تاریخ سفارش تا تحویل | [optional] 
**deliveryTimeDisplay** | **String** |  | [readonly] 
**deliveryTimeRangeDisplay** | [**DeliveryTimeRangeDisplay**](DeliveryTimeRangeDisplay.md) |  | [readonly] 
**inventoryAddress** | [**BusinessAddress**](BusinessAddress.md) |  | [readonly] 
**isPayAtDestination** | **Bool** | Whether the shipping method is pay at destination | [optional] 

[[Back to Model list]](../README.md#documentation-for-models) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to README]](../README.md)



# ShippingMethod

## Properties
Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**id** | **Int** |  | [readonly] 
**name** | **String** | نام روش/گزینه بسته‌بندی | 
**description** | **String** | شناسه روش ارسال برای استفاده در سفارش | [optional] 
**shippingType** | [**ShippingTypeEnum**](ShippingTypeEnum.md) | شناسه وضعیت ارسال از دیجی اکسپرس  * &#x60;1&#x60; - سایر * &#x60;2&#x60; - دیجی اکسپرس | [optional] 
**getShippingTypeDisplay** | **String** |  | [readonly] 
**shippingTypeDisplay** | **String** |  | [readonly] 
**cost** | **Int** | هزینه ارسال برای منطقه اصلی (مثلاً تهران) به تومان | [optional] 
**secondaryCost** | **Int** | هزینه ارسال برای مناطق دیگر به تومان | [optional] 
**minimumTimeSending** | **Int** | حداقل تعداد روز از تاریخ سفارش تا تحویل | [optional] 
**maximumTimeSending** | **Int** | Maximum number of days from order date to delivery | [optional] 
**deliveryTimeDisplay** | **String** |  | [readonly] 
**deliveryTimeRangeDisplay** | [**DeliveryTimeRangeDisplay**](DeliveryTimeRangeDisplay.md) |  | [readonly] 
**inventoryAddress** | [**BusinessAddress**](BusinessAddress.md) |  | [readonly] 
**isPayAtDestination** | **Bool** | آیا روش ارسال پرداخت در مقصد است | [optional] 

[[Back to Model list]](../README.md#documentation-for-models) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to README]](../README.md)



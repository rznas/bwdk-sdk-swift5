# OrderItemCreate

## Properties
Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**name** | **String** | نام کامل محصول شامل تمام مشخصات | 
**primaryAmount** | **Int** | قیمت اولیه برای هر واحد بدون تخفیف (به تومان) | [optional] 
**amount** | **Int** | قیمت نهایی برای تمام واحدها بعد از تخفیف (به تومان) | [optional] 
**count** | **Int** | تعداد واحدهای این کالا در سفارش | 
**discountAmount** | **Int** | مبلغ کل تخفیف برای این کالا (به تومان) | [optional] 
**taxAmount** | **Int** | مبلغ کل مالیات برای این کالا (به تومان) | [optional] 
**imageLink** | **String** | آدرس تصویر محصول | [optional] 
**options** | [Option] |  | 
**preparationTime** | **Int** | زمان آمادهسازی کالا (به روز) | [optional] [default to 2]
**weight** | **Double** | وزن کالا (بر حسب گرم) | [optional] 

[[Back to Model list]](../README.md#documentation-for-models) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to README]](../README.md)



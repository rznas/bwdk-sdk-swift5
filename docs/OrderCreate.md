# OrderCreate

## Properties
Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**merchantOrderId** | **String** | شناسه منحصر به فرد این سفارش در سیستم فروشنده | 
**merchantUniqueId** | **String** | شناسه منحصر به فرد برای تأیید اصالت سفارش | 
**mainAmount** | **Int** | مجموع قیمت‌های اولیه تمام کالاها بدون تخفیف (به تومان) | [optional] 
**finalAmount** | **Int** | مبلغ نهایی: مبلغ_اصلی - مبلغ_تخفیف + مبلغ_مالیات (به تومان) | [optional] 
**totalPaidAmount** | **Int** | مبلغ کل پرداخت شده توسط کاربر: مبلغ_نهایی + هزینه_ارسال (به تومان) | [optional] 
**discountAmount** | **Int** | مبلغ کل تخفیف برای تمام سفارش (به تومان) | [optional] 
**taxAmount** | **Int** | مبلغ کل مالیات برای تمام سفارش (به تومان) | [optional] 
**shippingAmount** | **Int** | هزینه ارسال برای سفارش (به تومان) | [optional] 
**loyaltyAmount** | **Int** | مبلغ تخفیف باشگاه مشتریان/پاداش (به تومان) | [optional] 
**callbackUrl** | **String** | آدرس وب‌هوک برای دریافت اطلاع رسانی وضعیت پرداخت | 
**destinationAddress** | **AnyCodable** |  | [readonly] 
**items** | [OrderItemCreate] |  | 
**merchant** | **Int** | مقدار توسط سیستم جایگذاری می شود | [optional] 
**sourceAddress** | **AnyCodable** | مقدار توسط سیستم جایگذاری می شود | [optional] 
**user** | **Int** |  | [readonly] 
**reservationExpiredAt** | **Int** | مهلت پرداخت (به عنوان Unix timestamp) قبل از اتمام سفارش | [optional] 
**referenceCode** | **String** | کد مرجع منحصر به فرد برای پیگیری سفارش مشتری (فرمت: BD-XXXXXXXX) | [readonly] 
**preparationTime** | **Int** | زمان آمادهسازی سفارش (به روز) | [optional] [default to 2]
**weight** | **Double** | وزن کل سفارش (بر حسب گرم) | [optional] 

[[Back to Model list]](../README.md#documentation-for-models) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to README]](../README.md)



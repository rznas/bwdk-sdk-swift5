# OrderDetail

## Properties
Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**id** | **Int** |  | [readonly] 
**createdAt** | **Date** |  | [readonly] 
**orderUuid** | **UUID** |  | [readonly] 
**reservationExpiredAt** | **Int** | Unix timestamp تا زمانی که سفارش برای پرداخت رزرو شده است | [readonly] 
**merchantOrderId** | **String** | شناسه منحصر به فرد سفارش در سیستم فروشنده | [readonly] 
**status** | [**OrderStatusEnum**](OrderStatusEnum.md) |  | [readonly] 
**statusDisplay** | **String** |  | [readonly] 
**mainAmount** | **Int** | مجموع قیمت‌های اولیه تمام کالاها بدون تخفیف (به تومان) | [readonly] 
**finalAmount** | **Int** | قیمت نهایی قابل پرداخت توسط مشتری: مبلغ_اصلی - مبلغ_تخفیف + مبلغ_مالیات (به تومان) | [readonly] 
**totalPaidAmount** | **Int** | مبلغ کل پرداخت شده توسط کاربر: مبلغ_نهایی + هزینه_ارسال (به تومان) | [readonly] 
**discountAmount** | **Int** | کل تخفیف اعمال شده بر سفارش (به تومان) | [readonly] 
**taxAmount** | **Int** | مبلغ کل مالیات برای سفارش (به تومان) | [readonly] 
**shippingAmount** | **Int** | هزینه ارسال برای سفارش (به تومان) | [readonly] 
**loyaltyAmount** | **Int** | مقدار تخفیف از برنامه باشگاه مشتریان/پاداش (به تومان) | [readonly] 
**callbackUrl** | **String** | آدرسی برای دریافت اطلاع رسانی وضعیت پرداخت پس از تکمیل سفارش | [readonly] 
**merchant** | [**Merchant**](Merchant.md) |  | 
**items** | [OrderItemCreate] |  | 
**sourceAddress** | **AnyCodable** |  | [readonly] 
**destinationAddress** | **AnyCodable** |  | [readonly] 
**selectedShippingMethod** | [**ShippingMethod**](ShippingMethod.md) |  | [readonly] 
**shippingSelectedAt** | **Date** |  | [readonly] 
**addressSelectedAt** | **Date** |  | [readonly] 
**packingAmount** | **Int** | هزینه روش بسته‌بندی انتخاب‌شده (به تومان) | [readonly] 
**packingSelectedAt** | **Date** |  | [readonly] 
**selectedPacking** | [**Packing**](Packing.md) |  | [readonly] 
**canSelectPacking** | **Bool** |  | [readonly] 
**canSelectShipping** | **Bool** |  | [readonly] 
**canSelectAddress** | **Bool** |  | [readonly] 
**canProceedToPayment** | **Bool** |  | [readonly] 
**isPaid** | **Bool** |  | [readonly] 
**user** | [**OrderUser**](OrderUser.md) |  | [readonly] 
**payment** | [**PaymentOrder**](PaymentOrder.md) |  | [readonly] 
**preparationTime** | **Int** | زمان آمادهسازی سفارش (به روز) | [readonly] 
**weight** | **Double** | وزن کل سفارش (بر حسب گرم) | [readonly] 
**selectedShippingData** | **[String: AnyCodable]** |  | [readonly] 
**referenceCode** | **String** | کد مرجع منحصر به فرد برای پیگیری سفارش مشتری (فرمت: BD-XXXXXXXX) | [readonly] 
**promotionDiscountAmount** | **Double** |  | [readonly] 
**promotionData** | **[String: AnyCodable]** |  | [readonly] 
**digipayMarkupAmount** | **Int** | مبلغ نشانه‌گذاری برای سفارش (به تومان) | [readonly] 
**markupCommissionPercentage** | **Int** | درصد کمیسیون نشانه‌گذاری برای سفارش (به درصد) | [readonly] 
**previousStatus** | [**OrderStatusEnum**](OrderStatusEnum.md) |  | [readonly] 
**previousStatusDisplay** | **String** |  | [readonly] 

[[Back to Model list]](../README.md#documentation-for-models) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to README]](../README.md)



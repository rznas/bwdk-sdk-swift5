# OrderShippingAPI

All URIs are relative to *https://bwdk-backend.digify.shop*

Method | HTTP request | Description
------------- | ------------- | -------------
[**orderApiV1ManagerCancelShipmentCreate**](OrderShippingAPI.md#orderapiv1managercancelshipmentcreate) | **POST** /order/api/v1/manager/{order_uuid}/cancel-shipment/ | Cancel Shipment
[**orderApiV1ManagerChangeShippingMethodUpdate**](OrderShippingAPI.md#orderapiv1managerchangeshippingmethodupdate) | **PUT** /order/api/v1/manager/{order_uuid}/change-shipping-method/ | Change Shipping Method
[**orderApiV1ManagerReviveShipmentCreate**](OrderShippingAPI.md#orderapiv1managerreviveshipmentcreate) | **POST** /order/api/v1/manager/{order_uuid}/revive-shipment/ | Revive Shipment


# **orderApiV1ManagerCancelShipmentCreate**
```swift
    open class func orderApiV1ManagerCancelShipmentCreate(orderUuid: UUID, completion: @escaping (_ data: MerchantOrderCancelShipmentResponse?, _ error: Error?) -> Void)
```

Cancel Shipment

<div dir=\"rtl\" style=\"text-align: right;\">  لغو مرسوله دیجی‌اکسپرس  ## توضیحات  این endpoint برای لغو یک مرسوله ثبت‌شده در سرویس دیجی‌اکسپرس استفاده می‌شود. پس از لغو موفق، مرسوله از صف ارسال خارج می‌شود.  نیاز به **API_KEY** فروشنده دارد.  ## شرایط لغو  * سفارش باید دارای روش ارسال **DigiExpress** باشد * مرسوله باید در وضعیت **در انتظار تحویل به پیک** (Request for Pickup) باشد  </div>  ```mermaid sequenceDiagram     participant M as فروشنده     participant API as BWDK API     participant DX as دیجی‌اکسپرس      M->>API: POST /order/api/v1/manager/{order_uuid}/cancel-shipment/     Note over M,API: Header: X-API-KEY (بدون بدنه)      alt روش ارسال DigiExpress نیست         API-->>M: 400 خطا         Note over API,M: {error: \"Selected shipping method is not DigiExpress\"}     else مرسوله قابل لغو نیست         API-->>M: 400 خطا         Note over API,M: {error: \"...\"}     else لغو موفق         API->>DX: لغو مرسوله         DX-->>API: تأیید لغو         API-->>M: 200 موفق         Note over API,M: {message, order_uuid, status, status_display}     end ``` 

### Example
```swift
// The following code samples are still beta. For any issue, please report via http://github.com/OpenAPITools/openapi-generator/issues/new
import OpenAPIClient

let orderUuid = 987 // UUID | 

// Cancel Shipment
OrderShippingAPI.orderApiV1ManagerCancelShipmentCreate(orderUuid: orderUuid) { (response, error) in
    guard error == nil else {
        print(error)
        return
    }

    if (response) {
        dump(response)
    }
}
```

### Parameters

Name | Type | Description  | Notes
------------- | ------------- | ------------- | -------------
 **orderUuid** | **UUID** |  | 

### Return type

[**MerchantOrderCancelShipmentResponse**](MerchantOrderCancelShipmentResponse.md)

### Authorization

[MerchantAPIKeyAuth](../README.md#MerchantAPIKeyAuth)

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json

[[Back to top]](#) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to Model list]](../README.md#documentation-for-models) [[Back to README]](../README.md)

# **orderApiV1ManagerChangeShippingMethodUpdate**
```swift
    open class func orderApiV1ManagerChangeShippingMethodUpdate(orderUuid: UUID, orderDetail: OrderDetail, completion: @escaping (_ data: OrderDetail?, _ error: Error?) -> Void)
```

Change Shipping Method

<div dir=\"rtl\" style=\"text-align: right;\">  تغییر روش ارسال سفارش  ## توضیحات  این endpoint به فروشنده اجازه می‌دهد روش ارسال یک سفارش را تغییر دهد. این عملیات معمولاً زمانی استفاده می‌شود که فروشنده بخواهد از DigiExpress به روش ارسال پیش‌فرض (یا بالعکس) تغییر دهد.  نیاز به **API_KEY** فروشنده دارد.  ## پارامترهای ورودی  * **updated_shipping**: شناسه روش ارسال جدید * **preparation_time** (اختیاری): زمان آماده‌سازی (روز) برای DigiExpress  </div> 

### Example
```swift
// The following code samples are still beta. For any issue, please report via http://github.com/OpenAPITools/openapi-generator/issues/new
import OpenAPIClient

let orderUuid = 987 // UUID | 
let orderDetail = OrderDetail(id: 123, createdAt: Date(), orderUuid: 123, reservationExpiredAt: 123, merchantOrderId: "merchantOrderId_example", status: OrderStatusEnum(), statusDisplay: "statusDisplay_example", mainAmount: 123, finalAmount: 123, totalPaidAmount: 123, discountAmount: 123, taxAmount: 123, shippingAmount: 123, loyaltyAmount: 123, callbackUrl: "callbackUrl_example", merchant: Merchant(name: "name_example", domain: "domain_example", logo: "logo_example"), items: [OrderItemCreate(name: "name_example", primaryAmount: 123, amount: 123, count: 123, discountAmount: 123, taxAmount: 123, imageLink: "imageLink_example", options: [Option(typeName: TypeNameEnum(), name: "name_example", value: "value_example", isColor: false)], preparationTime: 123, weight: 123)], sourceAddress: 123, destinationAddress: 123, selectedShippingMethod: ShippingMethod(id: 123, name: "name_example", description: "description_example", shippingType: ShippingTypeEnum(), getShippingTypeDisplay: "getShippingTypeDisplay_example", shippingTypeDisplay: "shippingTypeDisplay_example", cost: 123, secondaryCost: 123, minimumTimeSending: 123, maximumTimeSending: 123, deliveryTimeDisplay: "deliveryTimeDisplay_example", deliveryTimeRangeDisplay: DeliveryTimeRangeDisplay(minDate: "minDate_example", maxDate: "maxDate_example"), inventoryAddress: BusinessAddress(id: 123, address: "address_example", postalCode: "postalCode_example", cityName: "cityName_example", stateName: "stateName_example", districtId: 123, districtName: "districtName_example", longitude: 123, latitude: 123, buildingNumber: "buildingNumber_example", unit: "unit_example", receiverName: "receiverName_example", receiverPhone: "receiverPhone_example", isAccurate: false, isActive: false, createdAt: Date(), modifiedAt: Date()), isPayAtDestination: false), shippingSelectedAt: Date(), addressSelectedAt: Date(), packingAmount: 123, packingSelectedAt: Date(), selectedPacking: Packing(id: 123, name: "name_example", price: 123), canSelectPacking: false, canSelectShipping: false, canSelectAddress: false, canProceedToPayment: false, isPaid: false, user: OrderUser(firstName: "firstName_example", lastName: "lastName_example", phoneNumber: "phoneNumber_example", nationalIdentityNumber: "nationalIdentityNumber_example", birthDate: Date()), payment: PaymentOrder(finalAmount: 123, gatewayType: GatewayTypeEnum(), gatewayTypeDisplay: "gatewayTypeDisplay_example", paidAt: "paidAt_example", gatewayName: "gatewayName_example", invoiceId: "invoiceId_example", settlementDate: "settlementDate_example", settlementStatus: 123, settlementStatusDisplay: "settlementStatusDisplay_example"), preparationTime: 123, weight: 123, selectedShippingData: "TODO", referenceCode: "referenceCode_example", promotionDiscountAmount: 123, promotionData: "TODO", digipayMarkupAmount: 123, markupCommissionPercentage: 123, previousStatus: nil, previousStatusDisplay: "previousStatusDisplay_example") // OrderDetail | 

// Change Shipping Method
OrderShippingAPI.orderApiV1ManagerChangeShippingMethodUpdate(orderUuid: orderUuid, orderDetail: orderDetail) { (response, error) in
    guard error == nil else {
        print(error)
        return
    }

    if (response) {
        dump(response)
    }
}
```

### Parameters

Name | Type | Description  | Notes
------------- | ------------- | ------------- | -------------
 **orderUuid** | **UUID** |  | 
 **orderDetail** | [**OrderDetail**](OrderDetail.md) |  | 

### Return type

[**OrderDetail**](OrderDetail.md)

### Authorization

[MerchantAPIKeyAuth](../README.md#MerchantAPIKeyAuth)

### HTTP request headers

 - **Content-Type**: application/json, application/x-www-form-urlencoded, multipart/form-data
 - **Accept**: application/json

[[Back to top]](#) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to Model list]](../README.md#documentation-for-models) [[Back to README]](../README.md)

# **orderApiV1ManagerReviveShipmentCreate**
```swift
    open class func orderApiV1ManagerReviveShipmentCreate(orderUuid: UUID, reviveShipment: ReviveShipment? = nil, completion: @escaping (_ data: MerchantOrderReviveShipmentResponse?, _ error: Error?) -> Void)
```

Revive Shipment

<div dir=\"rtl\" style=\"text-align: right;\">  احیای مرسوله دیجی‌اکسپرس  ## توضیحات  این endpoint برای احیای (reactivate) یک مرسوله دیجی‌اکسپرس که قبلاً لغو شده یا در وضعیت غیرفعال است استفاده می‌شود. با ارسال `preparation_time` (زمان آماده‌سازی بر حسب روز)، زمان جدید آماده بودن بار تنظیم می‌شود.  نیاز به **API_KEY** فروشنده دارد.  ## پارامترهای ورودی  * **preparation_time** (اختیاری، پیش‌فرض: ۲): تعداد روز تا آماده‌شدن بار برای تحویل به پیک  ## شرایط  * سفارش باید دارای روش ارسال **DigiExpress** باشد * مرسوله باید در وضعیت قابل احیا باشد  </div>  ```mermaid sequenceDiagram     participant M as فروشنده     participant API as BWDK API     participant DX as دیجی‌اکسپرس      M->>API: POST /order/api/v1/manager/{order_uuid}/revive-shipment/     Note over M,API: Header: X-API-KEY<br/>{preparation_time: 2}      alt روش ارسال DigiExpress نیست         API-->>M: 400 خطا         Note over API,M: {error: \"Selected shipping method is not DigiExpress\"}     else احیا موفق         API->>DX: احیای مرسوله با زمان جدید         DX-->>API: تأیید احیا         API-->>M: 200 موفق         Note over API,M: {message, order_uuid, status, status_display}     end ``` 

### Example
```swift
// The following code samples are still beta. For any issue, please report via http://github.com/OpenAPITools/openapi-generator/issues/new
import OpenAPIClient

let orderUuid = 987 // UUID | 
let reviveShipment = ReviveShipment(preparationTime: 123) // ReviveShipment |  (optional)

// Revive Shipment
OrderShippingAPI.orderApiV1ManagerReviveShipmentCreate(orderUuid: orderUuid, reviveShipment: reviveShipment) { (response, error) in
    guard error == nil else {
        print(error)
        return
    }

    if (response) {
        dump(response)
    }
}
```

### Parameters

Name | Type | Description  | Notes
------------- | ------------- | ------------- | -------------
 **orderUuid** | **UUID** |  | 
 **reviveShipment** | [**ReviveShipment**](ReviveShipment.md) |  | [optional] 

### Return type

[**MerchantOrderReviveShipmentResponse**](MerchantOrderReviveShipmentResponse.md)

### Authorization

[MerchantAPIKeyAuth](../README.md#MerchantAPIKeyAuth)

### HTTP request headers

 - **Content-Type**: application/json, application/x-www-form-urlencoded, multipart/form-data
 - **Accept**: application/json

[[Back to top]](#) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to Model list]](../README.md#documentation-for-models) [[Back to README]](../README.md)


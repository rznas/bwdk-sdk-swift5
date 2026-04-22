# DefaultAPI

All URIs are relative to *https://bwdk-backend.digify.shop*

Method | HTTP request | Description
------------- | ------------- | -------------
[**merchantApiV1AuthStatusRetrieve**](DefaultAPI.md#merchantapiv1authstatusretrieve) | **GET** /merchant/api/v1/auth/status/ | وضعیت لاگین بودن
[**orderApiV1CreateOrderCreate**](DefaultAPI.md#orderapiv1createordercreate) | **POST** /order/api/v1/create-order/ | ساخت سفارش
[**orderApiV1ManagerCancelShipmentCreate**](DefaultAPI.md#orderapiv1managercancelshipmentcreate) | **POST** /order/api/v1/manager/{order_uuid}/cancel-shipment/ | لغو ارسال سفارش
[**orderApiV1ManagerChangeShippingMethodUpdate**](DefaultAPI.md#orderapiv1managerchangeshippingmethodupdate) | **PUT** /order/api/v1/manager/{order_uuid}/change-shipping-method/ | تغییر روش ارسال
[**orderApiV1ManagerList**](DefaultAPI.md#orderapiv1managerlist) | **GET** /order/api/v1/manager/ | لیست سفارشات
[**orderApiV1ManagerPaidList**](DefaultAPI.md#orderapiv1managerpaidlist) | **GET** /order/api/v1/manager/paid/ | سفارش پرداخت‌شده و تایید‌نشده
[**orderApiV1ManagerRefundCreate**](DefaultAPI.md#orderapiv1managerrefundcreate) | **POST** /order/api/v1/manager/{order_uuid}/refund/ | بازگشت سفارش
[**orderApiV1ManagerRetrieve**](DefaultAPI.md#orderapiv1managerretrieve) | **GET** /order/api/v1/manager/{order_uuid}/ | دریافت سفارش
[**orderApiV1ManagerReviveShipmentCreate**](DefaultAPI.md#orderapiv1managerreviveshipmentcreate) | **POST** /order/api/v1/manager/{order_uuid}/revive-shipment/ | احیای ارسال سفارش
[**orderApiV1ManagerUpdateStatusUpdate**](DefaultAPI.md#orderapiv1managerupdatestatusupdate) | **PUT** /order/api/v1/manager/{order_uuid}/update-status/ | به‌روزرسانی وضعیت سفارش
[**orderApiV1ManagerVerifyCreate**](DefaultAPI.md#orderapiv1managerverifycreate) | **POST** /order/api/v1/manager/{order_uuid}/verify/ | تایید سفارش
[**walletsApiV1WalletBalanceRetrieve**](DefaultAPI.md#walletsapiv1walletbalanceretrieve) | **GET** /wallets/api/v1/wallet-balance/ | دریافت موجودی کیف پول


# **merchantApiV1AuthStatusRetrieve**
```swift
    open class func merchantApiV1AuthStatusRetrieve(completion: @escaping (_ data: AuthStatusResponse?, _ error: Error?) -> Void)
```

وضعیت لاگین بودن

<div dir=\"rtl\" style=\"text-align: right;\">  بررسی وضعیت احراز هویت فروشنده  ## توضیحات  این endpoint برای بررسی اعتبار **API_KEY** فروشنده استفاده می‌شود. اگر کلید معتبر باشد، پاسخ `is_authenticated: true` برمی‌گردد. از این endpoint برای تأیید صحت کلید API قبل از شروع عملیات استفاده کنید.  نیاز به **API_KEY** فروشنده دارد (فقط Header لازم است، بدنه درخواست ندارد).  </div> 

### Example
```swift
// The following code samples are still beta. For any issue, please report via http://github.com/OpenAPITools/openapi-generator/issues/new
import OpenAPIClient


// وضعیت لاگین بودن
DefaultAPI.merchantApiV1AuthStatusRetrieve() { (response, error) in
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
This endpoint does not need any parameter.

### Return type

[**AuthStatusResponse**](AuthStatusResponse.md)

### Authorization

[MerchantAPIKeyAuth](../README.md#MerchantAPIKeyAuth)

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json

[[Back to top]](#) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to Model list]](../README.md#documentation-for-models) [[Back to README]](../README.md)

# **orderApiV1CreateOrderCreate**
```swift
    open class func orderApiV1CreateOrderCreate(orderCreate: OrderCreate, completion: @escaping (_ data: OrderCreateResponse?, _ error: Error?) -> Void)
```

ساخت سفارش

<div dir=\"rtl\" style=\"text-align: right;\">  ساخت سفارش جدید در سیستم BWDK  ## توضیحات  این endpoint برای ایجاد یک سفارش جدید در سیستم خرید با دیجی‌کالا استفاده می‌شود. در این درخواست باید اطلاعات سفارش، اقلام سبد خرید، و آدرس callback شامل شود.  برای شروع ارتباط با سرویس‌های **خرید با دیجی‌کالا** شما باید دارای **API_KEY** باشید که این مورد از سمت تیم دیجی‌فای در اختیار شما قرار خواهد گرفت.  ### روند کاری  **مرحله ۱: درخواست ساخت سفارش**  کاربر پس از انتخاب کالاهای خود در سبد خرید، بر روی دکمه **خرید با دیجی‌کالا** کلیک می‌کند و بک‌اند مرچنت درخواستی برای ساخت سفارش BWDK دریافت می‌کند. در این مرحله اولین درخواست خود را به بک‌اند BWDK ارسال می‌نمایید:  BWDK یک سفارش جدید برای مرچنت با وضعیت **INITIAL** ایجاد می‌کند و **order_uuid** را جنریت می‌کند. آدرس **order_start_url** نقطه شروع مسیر تکمیل سفارش است (انتخاب آدرس، شیپینگ، پکینگ، پرداخت و غیره). <br> </div>  ```mermaid sequenceDiagram     participant M as فروشنده     participant API as BWDK API     participant C as مشتری     participant PG as درگاه پرداخت      M->>API: POST /api/v1/orders/create     Note over M,API: شناسه سفارش, کالاها, مبلغ, callback_url     API-->>M: {لینک شروع سفارش, شناسه سفارش}      M->>C: تغییر مسیر به لینک شروع      C->>API: تکمیل درخواست خرید توسط مشتری     API->>PG: شروع فرآیند پرداخت     PG-->>C: نتیجه پرداخت     PG->>API: تأیید پرداخت     API-->>C: تغییر مسیر به callback_url      M->>API: POST /api/v1/orders/manager/{uuid}/verify     Note over M,API: {شناسه منحصربفرد فروشنده}     API-->>M: سفارش تأیید شد و آماده ارسال است ```  </div> 

### Example
```swift
// The following code samples are still beta. For any issue, please report via http://github.com/OpenAPITools/openapi-generator/issues/new
import OpenAPIClient

let orderCreate = OrderCreate(merchantOrderId: "merchantOrderId_example", merchantUniqueId: "merchantUniqueId_example", mainAmount: 123, finalAmount: 123, totalPaidAmount: 123, discountAmount: 123, taxAmount: 123, shippingAmount: 123, loyaltyAmount: 123, callbackUrl: "callbackUrl_example", destinationAddress: 123, items: [OrderItemCreate(name: "name_example", primaryAmount: 123, amount: 123, count: 123, discountAmount: 123, taxAmount: 123, imageLink: "imageLink_example", options: [Option(typeName: TypeNameEnum(), name: "name_example", value: "value_example", isColor: false)], preparationTime: 123, weight: 123)], merchant: 123, sourceAddress: 123, user: 123, reservationExpiredAt: 123, referenceCode: "referenceCode_example", preparationTime: 123, weight: 123) // OrderCreate | 

// ساخت سفارش
DefaultAPI.orderApiV1CreateOrderCreate(orderCreate: orderCreate) { (response, error) in
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
 **orderCreate** | [**OrderCreate**](OrderCreate.md) |  | 

### Return type

[**OrderCreateResponse**](OrderCreateResponse.md)

### Authorization

[MerchantAPIKeyAuth](../README.md#MerchantAPIKeyAuth)

### HTTP request headers

 - **Content-Type**: application/json, application/x-www-form-urlencoded, multipart/form-data
 - **Accept**: application/json

[[Back to top]](#) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to Model list]](../README.md#documentation-for-models) [[Back to README]](../README.md)

# **orderApiV1ManagerCancelShipmentCreate**
```swift
    open class func orderApiV1ManagerCancelShipmentCreate(orderUuid: UUID, completion: @escaping (_ data: MerchantOrderCancelShipmentResponse?, _ error: Error?) -> Void)
```

لغو ارسال سفارش

<div dir=\"rtl\" style=\"text-align: right;\">  لغو مرسوله دیجی‌اکسپرس  ## توضیحات  این endpoint برای لغو یک مرسوله ثبت‌شده در سرویس دیجی‌اکسپرس استفاده می‌شود. پس از لغو موفق، مرسوله از صف ارسال خارج می‌شود.  نیاز به **API_KEY** فروشنده دارد.  ## شرایط لغو  * سفارش باید دارای روش ارسال **DigiExpress** باشد * مرسوله باید در وضعیت **در انتظار تحویل به پیک** (Request for Pickup) باشد  </div>  ```mermaid sequenceDiagram     participant M as فروشنده     participant API as BWDK API     participant DX as دیجی‌اکسپرس      M->>API: POST /order/api/v1/manager/{order_uuid}/cancel-shipment/     Note over M,API: Header: X-API-KEY (بدون بدنه)      alt روش ارسال DigiExpress نیست         API-->>M: 400 خطا         Note over API,M: {error: \"Selected shipping method is not DigiExpress\"}     else مرسوله قابل لغو نیست         API-->>M: 400 خطا         Note over API,M: {error: \"...\"}     else لغو موفق         API->>DX: لغو مرسوله         DX-->>API: تأیید لغو         API-->>M: 200 موفق         Note over API,M: {message, order_uuid, status, status_display}     end ``` 

### Example
```swift
// The following code samples are still beta. For any issue, please report via http://github.com/OpenAPITools/openapi-generator/issues/new
import OpenAPIClient

let orderUuid = 987 // UUID | 

// لغو ارسال سفارش
DefaultAPI.orderApiV1ManagerCancelShipmentCreate(orderUuid: orderUuid) { (response, error) in
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

تغییر روش ارسال

<div dir=\"rtl\" style=\"text-align: right;\">  تغییر روش ارسال سفارش  ## توضیحات  این endpoint به فروشنده اجازه می‌دهد روش ارسال یک سفارش را تغییر دهد. این عملیات معمولاً زمانی استفاده می‌شود که فروشنده بخواهد از DigiExpress به روش ارسال پیش‌فرض (یا بالعکس) تغییر دهد.  نیاز به **API_KEY** فروشنده دارد.  ## پارامترهای ورودی  * **updated_shipping**: شناسه روش ارسال جدید * **preparation_time** (اختیاری): زمان آماده‌سازی (روز) برای DigiExpress  </div> 

### Example
```swift
// The following code samples are still beta. For any issue, please report via http://github.com/OpenAPITools/openapi-generator/issues/new
import OpenAPIClient

let orderUuid = 987 // UUID | 
let orderDetail = OrderDetail(id: 123, createdAt: Date(), orderUuid: 123, reservationExpiredAt: 123, merchantOrderId: "merchantOrderId_example", status: OrderStatusEnum(), statusDisplay: "statusDisplay_example", mainAmount: 123, finalAmount: 123, totalPaidAmount: 123, discountAmount: 123, taxAmount: 123, shippingAmount: 123, loyaltyAmount: 123, callbackUrl: "callbackUrl_example", merchant: Merchant(name: "name_example", domain: "domain_example", logo: "logo_example"), items: [OrderItemCreate(name: "name_example", primaryAmount: 123, amount: 123, count: 123, discountAmount: 123, taxAmount: 123, imageLink: "imageLink_example", options: [Option(typeName: TypeNameEnum(), name: "name_example", value: "value_example", isColor: false)], preparationTime: 123, weight: 123)], sourceAddress: 123, destinationAddress: 123, selectedShippingMethod: ShippingMethod(id: 123, name: "name_example", description: "description_example", shippingType: ShippingTypeEnum(), getShippingTypeDisplay: "getShippingTypeDisplay_example", shippingTypeDisplay: "shippingTypeDisplay_example", cost: 123, secondaryCost: 123, minimumTimeSending: 123, maximumTimeSending: 123, deliveryTimeDisplay: "deliveryTimeDisplay_example", deliveryTimeRangeDisplay: DeliveryTimeRangeDisplay(minDate: "minDate_example", maxDate: "maxDate_example"), inventoryAddress: BusinessAddress(id: 123, address: "address_example", postalCode: "postalCode_example", cityName: "cityName_example", stateName: "stateName_example", districtId: 123, districtName: "districtName_example", longitude: 123, latitude: 123, buildingNumber: "buildingNumber_example", unit: "unit_example", receiverName: "receiverName_example", receiverPhone: "receiverPhone_example", isAccurate: false, isActive: false, createdAt: Date(), modifiedAt: Date()), isPayAtDestination: false), shippingSelectedAt: Date(), addressSelectedAt: Date(), packingAmount: 123, packingSelectedAt: Date(), selectedPacking: Packing(id: 123, name: "name_example", price: 123), canSelectPacking: false, canSelectShipping: false, canSelectAddress: false, canProceedToPayment: false, isPaid: false, user: OrderUser(firstName: "firstName_example", lastName: "lastName_example", phoneNumber: "phoneNumber_example", nationalIdentityNumber: "nationalIdentityNumber_example", birthDate: Date()), payment: PaymentOrder(finalAmount: 123, gatewayType: GatewayTypeEnum(), gatewayTypeDisplay: "gatewayTypeDisplay_example", paidAt: "paidAt_example", gatewayName: "gatewayName_example", invoiceId: "invoiceId_example", settlementDate: "settlementDate_example", settlementStatus: 123, settlementStatusDisplay: "settlementStatusDisplay_example"), preparationTime: 123, weight: 123, selectedShippingData: "TODO", referenceCode: "referenceCode_example", promotionDiscountAmount: 123, promotionData: "TODO", digipayMarkupAmount: 123, markupCommissionPercentage: 123, previousStatus: nil, previousStatusDisplay: "previousStatusDisplay_example") // OrderDetail | 

// تغییر روش ارسال
DefaultAPI.orderApiV1ManagerChangeShippingMethodUpdate(orderUuid: orderUuid, orderDetail: orderDetail) { (response, error) in
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

# **orderApiV1ManagerList**
```swift
    open class func orderApiV1ManagerList(cities: String? = nil, createdAt: Date? = nil, cursor: String? = nil, orderIds: String? = nil, ordering: String? = nil, paymentTypes: String? = nil, provinces: String? = nil, referenceCode: String? = nil, search: String? = nil, shippingTypes: String? = nil, status: Status_orderApiV1ManagerList? = nil, statuses: String? = nil, todayPickup: Bool? = nil, completion: @escaping (_ data: PaginatedOrderDetailList?, _ error: Error?) -> Void)
```

لیست سفارشات

<div dir=\"rtl\" style=\"text-align: right;\">  لیست سفارشات فروشنده  ## توضیحات  این endpoint لیست تمام سفارشات مرتبط با فروشنده را با امکان فیلتر، جستجو و مرتب‌سازی برمی‌گرداند. نتایج به صورت صفحه‌بندی‌شده (Cursor Pagination) ارسال می‌شوند و به ترتیب جدیدترین سفارش اول مرتب می‌شوند.  نیاز به **API_KEY** فروشنده دارد.  ## پارامترهای فیلتر  * **status**: وضعیت سفارش (INITIAL, PENDING, PAID_BY_USER, VERIFIED_BY_MERCHANT, ...) * **created_at__gte / created_at__lte**: فیلتر بر اساس تاریخ ایجاد * **search**: جستجو در شماره تلفن مشتری، نام، کد مرجع، شناسه سفارش مرچنت * **ordering**: مرتب‌سازی بر اساس created_at, final_amount, status, merchant_order_id  </div> 

### Example
```swift
// The following code samples are still beta. For any issue, please report via http://github.com/OpenAPITools/openapi-generator/issues/new
import OpenAPIClient

let cities = "cities_example" // String |  (optional)
let createdAt = Date() // Date |  (optional)
let cursor = "cursor_example" // String | مقدار نشانگر صفحه‌بندی. (optional)
let orderIds = "orderIds_example" // String |  (optional)
let ordering = "ordering_example" // String | کدام فیلد باید هنگام مرتب‌سازی نتایج استفاده شود. (optional)
let paymentTypes = "paymentTypes_example" // String |  (optional)
let provinces = "provinces_example" // String |  (optional)
let referenceCode = "referenceCode_example" // String |  (optional)
let search = "search_example" // String | یک عبارت جستجو. (optional)
let shippingTypes = "shippingTypes_example" // String |  (optional)
let status = 987 // Int | * `1` - اولیه * `2` - شروع در * `3` - در انتظار * `4` - در انتظار درگاه * `5` - منقضی شده * `6` - لغو شده * `7` - ممنوع شده توسط ما * `8` - ناموفق در پرداخت * `9` - تأیید شده توسط فروشنده * `10` - ناموفق در تأیید توسط فروشنده * `11` - فروشگاه * `12` - لغو شده توسط فروشنده * `13` - درخواست بازگرداندن وجه به مشتری به دلیل درخواست مشتری * `14` - درخواست بازگرداندن وجه به فروشنده پس از ناموفقی در تأیید توسط فروشنده * `15` - درخواست بازگرداندن وجه به مشتری پس از ناموفقی توسط فروشنده * `16` - بازگردانده شده به فروشنده پس از لغو توسط فروشنده * `17` - بازگرداندن وجه تکمیل شد * `18` - زمان مجاز برای منقضی کردن گذشته است * `19` - تحویل نشده * `20` - مرسوله (optional)
let statuses = "statuses_example" // String |  (optional)
let todayPickup = true // Bool |  (optional)

// لیست سفارشات
DefaultAPI.orderApiV1ManagerList(cities: cities, createdAt: createdAt, cursor: cursor, orderIds: orderIds, ordering: ordering, paymentTypes: paymentTypes, provinces: provinces, referenceCode: referenceCode, search: search, shippingTypes: shippingTypes, status: status, statuses: statuses, todayPickup: todayPickup) { (response, error) in
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
 **cities** | **String** |  | [optional] 
 **createdAt** | **Date** |  | [optional] 
 **cursor** | **String** | مقدار نشانگر صفحه‌بندی. | [optional] 
 **orderIds** | **String** |  | [optional] 
 **ordering** | **String** | کدام فیلد باید هنگام مرتب‌سازی نتایج استفاده شود. | [optional] 
 **paymentTypes** | **String** |  | [optional] 
 **provinces** | **String** |  | [optional] 
 **referenceCode** | **String** |  | [optional] 
 **search** | **String** | یک عبارت جستجو. | [optional] 
 **shippingTypes** | **String** |  | [optional] 
 **status** | **Int** | * &#x60;1&#x60; - اولیه * &#x60;2&#x60; - شروع در * &#x60;3&#x60; - در انتظار * &#x60;4&#x60; - در انتظار درگاه * &#x60;5&#x60; - منقضی شده * &#x60;6&#x60; - لغو شده * &#x60;7&#x60; - ممنوع شده توسط ما * &#x60;8&#x60; - ناموفق در پرداخت * &#x60;9&#x60; - تأیید شده توسط فروشنده * &#x60;10&#x60; - ناموفق در تأیید توسط فروشنده * &#x60;11&#x60; - فروشگاه * &#x60;12&#x60; - لغو شده توسط فروشنده * &#x60;13&#x60; - درخواست بازگرداندن وجه به مشتری به دلیل درخواست مشتری * &#x60;14&#x60; - درخواست بازگرداندن وجه به فروشنده پس از ناموفقی در تأیید توسط فروشنده * &#x60;15&#x60; - درخواست بازگرداندن وجه به مشتری پس از ناموفقی توسط فروشنده * &#x60;16&#x60; - بازگردانده شده به فروشنده پس از لغو توسط فروشنده * &#x60;17&#x60; - بازگرداندن وجه تکمیل شد * &#x60;18&#x60; - زمان مجاز برای منقضی کردن گذشته است * &#x60;19&#x60; - تحویل نشده * &#x60;20&#x60; - مرسوله | [optional] 
 **statuses** | **String** |  | [optional] 
 **todayPickup** | **Bool** |  | [optional] 

### Return type

[**PaginatedOrderDetailList**](PaginatedOrderDetailList.md)

### Authorization

[MerchantAPIKeyAuth](../README.md#MerchantAPIKeyAuth)

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json

[[Back to top]](#) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to Model list]](../README.md#documentation-for-models) [[Back to README]](../README.md)

# **orderApiV1ManagerPaidList**
```swift
    open class func orderApiV1ManagerPaidList(cities: String? = nil, createdAt: Date? = nil, cursor: String? = nil, orderIds: String? = nil, ordering: String? = nil, paymentTypes: String? = nil, provinces: String? = nil, referenceCode: String? = nil, search: String? = nil, shippingTypes: String? = nil, status: Status_orderApiV1ManagerPaidList? = nil, statuses: String? = nil, todayPickup: Bool? = nil, completion: @escaping (_ data: PaginatedMerchantPaidOrderListList?, _ error: Error?) -> Void)
```

سفارش پرداخت‌شده و تایید‌نشده

لیست تمامی سفارشاتی که توسط کاربر پرداخت شده اند ولی توسط فروشنده تایید نشده اند. 

### Example
```swift
// The following code samples are still beta. For any issue, please report via http://github.com/OpenAPITools/openapi-generator/issues/new
import OpenAPIClient

let cities = "cities_example" // String |  (optional)
let createdAt = Date() // Date |  (optional)
let cursor = "cursor_example" // String | مقدار نشانگر صفحه‌بندی. (optional)
let orderIds = "orderIds_example" // String |  (optional)
let ordering = "ordering_example" // String | کدام فیلد باید هنگام مرتب‌سازی نتایج استفاده شود. (optional)
let paymentTypes = "paymentTypes_example" // String |  (optional)
let provinces = "provinces_example" // String |  (optional)
let referenceCode = "referenceCode_example" // String |  (optional)
let search = "search_example" // String | یک عبارت جستجو. (optional)
let shippingTypes = "shippingTypes_example" // String |  (optional)
let status = 987 // Int | * `1` - اولیه * `2` - شروع در * `3` - در انتظار * `4` - در انتظار درگاه * `5` - منقضی شده * `6` - لغو شده * `7` - ممنوع شده توسط ما * `8` - ناموفق در پرداخت * `9` - تأیید شده توسط فروشنده * `10` - ناموفق در تأیید توسط فروشنده * `11` - فروشگاه * `12` - لغو شده توسط فروشنده * `13` - درخواست بازگرداندن وجه به مشتری به دلیل درخواست مشتری * `14` - درخواست بازگرداندن وجه به فروشنده پس از ناموفقی در تأیید توسط فروشنده * `15` - درخواست بازگرداندن وجه به مشتری پس از ناموفقی توسط فروشنده * `16` - بازگردانده شده به فروشنده پس از لغو توسط فروشنده * `17` - بازگرداندن وجه تکمیل شد * `18` - زمان مجاز برای منقضی کردن گذشته است * `19` - تحویل نشده * `20` - مرسوله (optional)
let statuses = "statuses_example" // String |  (optional)
let todayPickup = true // Bool |  (optional)

// سفارش پرداخت‌شده و تایید‌نشده
DefaultAPI.orderApiV1ManagerPaidList(cities: cities, createdAt: createdAt, cursor: cursor, orderIds: orderIds, ordering: ordering, paymentTypes: paymentTypes, provinces: provinces, referenceCode: referenceCode, search: search, shippingTypes: shippingTypes, status: status, statuses: statuses, todayPickup: todayPickup) { (response, error) in
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
 **cities** | **String** |  | [optional] 
 **createdAt** | **Date** |  | [optional] 
 **cursor** | **String** | مقدار نشانگر صفحه‌بندی. | [optional] 
 **orderIds** | **String** |  | [optional] 
 **ordering** | **String** | کدام فیلد باید هنگام مرتب‌سازی نتایج استفاده شود. | [optional] 
 **paymentTypes** | **String** |  | [optional] 
 **provinces** | **String** |  | [optional] 
 **referenceCode** | **String** |  | [optional] 
 **search** | **String** | یک عبارت جستجو. | [optional] 
 **shippingTypes** | **String** |  | [optional] 
 **status** | **Int** | * &#x60;1&#x60; - اولیه * &#x60;2&#x60; - شروع در * &#x60;3&#x60; - در انتظار * &#x60;4&#x60; - در انتظار درگاه * &#x60;5&#x60; - منقضی شده * &#x60;6&#x60; - لغو شده * &#x60;7&#x60; - ممنوع شده توسط ما * &#x60;8&#x60; - ناموفق در پرداخت * &#x60;9&#x60; - تأیید شده توسط فروشنده * &#x60;10&#x60; - ناموفق در تأیید توسط فروشنده * &#x60;11&#x60; - فروشگاه * &#x60;12&#x60; - لغو شده توسط فروشنده * &#x60;13&#x60; - درخواست بازگرداندن وجه به مشتری به دلیل درخواست مشتری * &#x60;14&#x60; - درخواست بازگرداندن وجه به فروشنده پس از ناموفقی در تأیید توسط فروشنده * &#x60;15&#x60; - درخواست بازگرداندن وجه به مشتری پس از ناموفقی توسط فروشنده * &#x60;16&#x60; - بازگردانده شده به فروشنده پس از لغو توسط فروشنده * &#x60;17&#x60; - بازگرداندن وجه تکمیل شد * &#x60;18&#x60; - زمان مجاز برای منقضی کردن گذشته است * &#x60;19&#x60; - تحویل نشده * &#x60;20&#x60; - مرسوله | [optional] 
 **statuses** | **String** |  | [optional] 
 **todayPickup** | **Bool** |  | [optional] 

### Return type

[**PaginatedMerchantPaidOrderListList**](PaginatedMerchantPaidOrderListList.md)

### Authorization

[MerchantAPIKeyAuth](../README.md#MerchantAPIKeyAuth)

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json

[[Back to top]](#) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to Model list]](../README.md#documentation-for-models) [[Back to README]](../README.md)

# **orderApiV1ManagerRefundCreate**
```swift
    open class func orderApiV1ManagerRefundCreate(orderUuid: UUID, refundOrder: RefundOrder? = nil, completion: @escaping (_ data: MerchantOrderRefundResponse?, _ error: Error?) -> Void)
```

بازگشت سفارش

<div dir=\"rtl\" style=\"text-align: right;\"> بازگشت و لغو سفارش  ## توضیحات  این endpoint برای بازگشت یا لغو سفارشی استفاده می‌شود که قبلاً پرداخت شده یا تایید شده است. در این مرحله مبلغ سفارش به کاربر بازگشت داده می‌شود و وضعیت سفارش به **REFUNDED** تغییر می‌یابد.   ## شرایط بازگشت  سفارش باید در یکی از وضعیت‌های زیر باشد تا بازگشت امکان‌پذیر باشد: * **PAID_BY_USER**: سفارش پرداخت شده است اما هنوز تایید نشده * **VERIFIED_BY_MERCHANT**: سفارش تایید شده است  سفارش نباید قبلاً بازگشت داده شده باشد.  **پاسخ خطا** - اگر سفارش در وضعیت مناسب نباشد یا قبلاً بازگشت داده شده باشد </div>  ```mermaid sequenceDiagram     participant M as فروشنده     participant API as BWDK API      M->>API: POST /api/v1/orders/manager/{uuid}/refund     Note over M,API: {reason: \"درخواست مشتری\"}      alt سفارش قابل بازگشت نیست         API-->>M: 500 خطا         Note over API,M: {error: \"شروع بازگشت ناموفق بود.<br/>لطفاً دوباره تلاش کنید.\"}     else سفارش معتبر است         API-->>M: 200 موفق         Note over API,M: {message: \"درخواست بازگشت با<br/>موفقیت شروع شد\",<br/>order_uuid, status: 13,<br/>status_display,<br/>refund_reason}          M->>API: GET /api/v1/orders/manager/{uuid}         Note over M,API: بررسی وضعیت سفارش<br/>(endpoint جداگانه /refund/status وجود ندارد)          alt status: 17 (بازگشت تکمیل شد)             API-->>M: 200 موفق             Note over API,M: {order_uuid, status: 17,<br/>status_display: \"بازگشت تکمیل شد\",<br/>metadata.refund_tracking_code,<br/>metadata.refund_completed_at}          else status: 13 (در حال پردازش)             API-->>M: 200 موفق             Note over API,M: {order_uuid, status: 13,<br/>status_display: \"درخواست بازگشت به مشتری<br/>به دلیل درخواست<br/>مشتری\",<br/>metadata.refund_reason}          else status: قبلی (بازگشت ناموفق)             API-->>M: 200 موفق             Note over API,M: {order_uuid, status: (قبلی),<br/>metadata.refund_error,<br/>metadata.refund_failed_at}         end     end ``` 

### Example
```swift
// The following code samples are still beta. For any issue, please report via http://github.com/OpenAPITools/openapi-generator/issues/new
import OpenAPIClient

let orderUuid = 987 // UUID | 
let refundOrder = RefundOrder(reason: "reason_example") // RefundOrder |  (optional)

// بازگشت سفارش
DefaultAPI.orderApiV1ManagerRefundCreate(orderUuid: orderUuid, refundOrder: refundOrder) { (response, error) in
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
 **refundOrder** | [**RefundOrder**](RefundOrder.md) |  | [optional] 

### Return type

[**MerchantOrderRefundResponse**](MerchantOrderRefundResponse.md)

### Authorization

[MerchantAPIKeyAuth](../README.md#MerchantAPIKeyAuth)

### HTTP request headers

 - **Content-Type**: application/json, application/x-www-form-urlencoded, multipart/form-data
 - **Accept**: application/json

[[Back to top]](#) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to Model list]](../README.md#documentation-for-models) [[Back to README]](../README.md)

# **orderApiV1ManagerRetrieve**
```swift
    open class func orderApiV1ManagerRetrieve(orderUuid: UUID, completion: @escaping (_ data: OrderDetail?, _ error: Error?) -> Void)
```

دریافت سفارش

<div dir=\"rtl\" style=\"text-align: right;\">  # مدیریت سفارشات  ## توضیحات  این endpoint برای مدیریت و مشاهده سفارشات فروشنده استفاده می‌شود.  </div> 

### Example
```swift
// The following code samples are still beta. For any issue, please report via http://github.com/OpenAPITools/openapi-generator/issues/new
import OpenAPIClient

let orderUuid = 987 // UUID | 

// دریافت سفارش
DefaultAPI.orderApiV1ManagerRetrieve(orderUuid: orderUuid) { (response, error) in
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

[**OrderDetail**](OrderDetail.md)

### Authorization

[MerchantAPIKeyAuth](../README.md#MerchantAPIKeyAuth)

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json

[[Back to top]](#) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to Model list]](../README.md#documentation-for-models) [[Back to README]](../README.md)

# **orderApiV1ManagerReviveShipmentCreate**
```swift
    open class func orderApiV1ManagerReviveShipmentCreate(orderUuid: UUID, reviveShipment: ReviveShipment? = nil, completion: @escaping (_ data: MerchantOrderReviveShipmentResponse?, _ error: Error?) -> Void)
```

احیای ارسال سفارش

<div dir=\"rtl\" style=\"text-align: right;\">  احیای مرسوله دیجی‌اکسپرس  ## توضیحات  این endpoint برای احیای (reactivate) یک مرسوله دیجی‌اکسپرس که قبلاً لغو شده یا در وضعیت غیرفعال است استفاده می‌شود. با ارسال `preparation_time` (زمان آماده‌سازی بر حسب روز)، زمان جدید آماده بودن بار تنظیم می‌شود.  نیاز به **API_KEY** فروشنده دارد.  ## پارامترهای ورودی  * **preparation_time** (اختیاری، پیش‌فرض: ۲): تعداد روز تا آماده‌شدن بار برای تحویل به پیک  ## شرایط  * سفارش باید دارای روش ارسال **DigiExpress** باشد * مرسوله باید در وضعیت قابل احیا باشد  </div>  ```mermaid sequenceDiagram     participant M as فروشنده     participant API as BWDK API     participant DX as دیجی‌اکسپرس      M->>API: POST /order/api/v1/manager/{order_uuid}/revive-shipment/     Note over M,API: Header: X-API-KEY<br/>{preparation_time: 2}      alt روش ارسال DigiExpress نیست         API-->>M: 400 خطا         Note over API,M: {error: \"Selected shipping method is not DigiExpress\"}     else احیا موفق         API->>DX: احیای مرسوله با زمان جدید         DX-->>API: تأیید احیا         API-->>M: 200 موفق         Note over API,M: {message, order_uuid, status, status_display}     end ``` 

### Example
```swift
// The following code samples are still beta. For any issue, please report via http://github.com/OpenAPITools/openapi-generator/issues/new
import OpenAPIClient

let orderUuid = 987 // UUID | 
let reviveShipment = ReviveShipment(preparationTime: 123) // ReviveShipment |  (optional)

// احیای ارسال سفارش
DefaultAPI.orderApiV1ManagerReviveShipmentCreate(orderUuid: orderUuid, reviveShipment: reviveShipment) { (response, error) in
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

# **orderApiV1ManagerUpdateStatusUpdate**
```swift
    open class func orderApiV1ManagerUpdateStatusUpdate(orderUuid: UUID, updateOrderStatus: UpdateOrderStatus, completion: @escaping (_ data: OrderDetail?, _ error: Error?) -> Void)
```

به‌روزرسانی وضعیت سفارش

<div dir=\"rtl\" style=\"text-align: right;\">  بروزرسانی وضعیت سفارش  ## توضیحات  این endpoint به فروشنده امکان می‌دهد وضعیت یک سفارش را به‌صورت مستقیم تغییر دهد. این endpoint برای مواردی مانند علامت‌گذاری سفارش به‌عنوان «ارسال شده» یا «تحویل داده شده» توسط فروشنده استفاده می‌شود.  نیاز به **API_KEY** فروشنده دارد.  ## وضعیت‌های مجاز  * **DELIVERED**: تحویل شد * **DISPATCHED**: ارسال شد * سایر وضعیت‌های تعریف‌شده در سیستم  </div>  ```mermaid sequenceDiagram     participant M as فروشنده     participant API as BWDK API      M->>API: PUT /order/api/v1/manager/{order_uuid}/update-status/     Note over M,API: Header: X-API-KEY<br/>{status: \"DELIVERED\"}      alt وضعیت معتبر است         API-->>M: 200 موفق         Note over API,M: اطلاعات کامل سفارش با وضعیت جدید     else وضعیت نامعتبر است         API-->>M: 400 خطا         Note over API,M: {error: \"invalid status\"}     end ``` 

### Example
```swift
// The following code samples are still beta. For any issue, please report via http://github.com/OpenAPITools/openapi-generator/issues/new
import OpenAPIClient

let orderUuid = 987 // UUID | 
let updateOrderStatus = UpdateOrderStatus(status: OrderStatusEnum()) // UpdateOrderStatus | 

// به‌روزرسانی وضعیت سفارش
DefaultAPI.orderApiV1ManagerUpdateStatusUpdate(orderUuid: orderUuid, updateOrderStatus: updateOrderStatus) { (response, error) in
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
 **updateOrderStatus** | [**UpdateOrderStatus**](UpdateOrderStatus.md) |  | 

### Return type

[**OrderDetail**](OrderDetail.md)

### Authorization

[MerchantAPIKeyAuth](../README.md#MerchantAPIKeyAuth)

### HTTP request headers

 - **Content-Type**: application/json, application/x-www-form-urlencoded, multipart/form-data
 - **Accept**: application/json

[[Back to top]](#) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to Model list]](../README.md#documentation-for-models) [[Back to README]](../README.md)

# **orderApiV1ManagerVerifyCreate**
```swift
    open class func orderApiV1ManagerVerifyCreate(orderUuid: UUID, verifyOrder: VerifyOrder, completion: @escaping (_ data: OrderDetail?, _ error: Error?) -> Void)
```

تایید سفارش

<div dir=\"rtl\" style=\"text-align: right;\">  تایید سفارش پس از پرداخت  ## توضیحات  پس از اتمام فرایند پرداخت توسط کاربر، مرچنت باید سفارش را تایید کند. این endpoint برای تایید و نهایی کردن سفارش پس از پرداخت موفق توسط مشتری استفاده می‌شود. در این مرحله مرچنت سفارش را تایید می‌کند و وضعیت سفارش به **VERIFIED_BY_MERCHANT** تغییر می‌یابد.  ## روند کاری  **مرحله ۲: بازگشت کاربر و دریافت نتیجه**  پس از تکمیل فرایند پرداخت (موفق یا ناموفق)، کاربر به آدرس callback_url که هنگام ساخت سفارش ارسال کرده بودید بازگردانده می‌شود. در این درخواست وضعیت سفارش به صورت query parameters ارسال می‌شود:   **Query Parameters:** * **success**: متغیر منطقی نشان‌دهنده موفق یا ناموفق بودن سفارش * **status**: وضعیت سفارش (PAID، FAILED، وغیره) * **phone_number**: شماره تلفن مشتری * **order_uuid**: شناسه یکتای سفارش * **merchant_order_id**: شناسه سفارش در سیستم مرچنت  **مرحله ۳: تایید سفارش در بک‌اند**  سپس شما باید این endpoint را فراخوانی کنید تا سفارش را تایید کنید و اطمینان حاصل کنید که سفارش موفقیت‌آمیز ثبت شده است: </div> 

### Example
```swift
// The following code samples are still beta. For any issue, please report via http://github.com/OpenAPITools/openapi-generator/issues/new
import OpenAPIClient

let orderUuid = 987 // UUID | 
let verifyOrder = VerifyOrder(merchantUniqueId: "merchantUniqueId_example") // VerifyOrder | 

// تایید سفارش
DefaultAPI.orderApiV1ManagerVerifyCreate(orderUuid: orderUuid, verifyOrder: verifyOrder) { (response, error) in
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
 **verifyOrder** | [**VerifyOrder**](VerifyOrder.md) |  | 

### Return type

[**OrderDetail**](OrderDetail.md)

### Authorization

[MerchantAPIKeyAuth](../README.md#MerchantAPIKeyAuth)

### HTTP request headers

 - **Content-Type**: application/json, application/x-www-form-urlencoded, multipart/form-data
 - **Accept**: application/json

[[Back to top]](#) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to Model list]](../README.md#documentation-for-models) [[Back to README]](../README.md)

# **walletsApiV1WalletBalanceRetrieve**
```swift
    open class func walletsApiV1WalletBalanceRetrieve(completion: @escaping (_ data: WalletBalance?, _ error: Error?) -> Void)
```

دریافت موجودی کیف پول

<div dir=\"rtl\" style=\"text-align: right;\">  موجودی کیف پول فروشنده  ## توضیحات  این endpoint موجودی کیف پول فروشنده را برمی‌گرداند. کیف پول برای پرداخت هزینه ارسال دیجی‌اکسپرس استفاده می‌شود. هنگام ثبت مرسوله دیجی‌اکسپرس، هزینه ارسال به‌صورت خودکار از کیف پول کسر می‌شود.  نیاز به **API_KEY** فروشنده دارد.  </div> 

### Example
```swift
// The following code samples are still beta. For any issue, please report via http://github.com/OpenAPITools/openapi-generator/issues/new
import OpenAPIClient


// دریافت موجودی کیف پول
DefaultAPI.walletsApiV1WalletBalanceRetrieve() { (response, error) in
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
This endpoint does not need any parameter.

### Return type

[**WalletBalance**](WalletBalance.md)

### Authorization

[MerchantAPIKeyAuth](../README.md#MerchantAPIKeyAuth)

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json

[[Back to top]](#) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to Model list]](../README.md#documentation-for-models) [[Back to README]](../README.md)


# SellerProfileManagementAPI

All URIs are relative to *https://bwdk-backend.digify.shop*

Method | HTTP request | Description
------------- | ------------- | -------------
[**merchantApiV1AuthStatusRetrieve**](SellerProfileManagementAPI.md#merchantapiv1authstatusretrieve) | **GET** /merchant/api/v1/auth/status/ | وضعیت لاگین بودن


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
SellerProfileManagementAPI.merchantApiV1AuthStatusRetrieve() { (response, error) in
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


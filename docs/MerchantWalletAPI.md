# MerchantWalletAPI

All URIs are relative to *https://bwdk-backend.digify.shop*

Method | HTTP request | Description
------------- | ------------- | -------------
[**walletsApiV1WalletBalanceRetrieve**](MerchantWalletAPI.md#walletsapiv1walletbalanceretrieve) | **GET** /wallets/api/v1/wallet-balance/ | Get Wallet Balance


# **walletsApiV1WalletBalanceRetrieve**
```swift
    open class func walletsApiV1WalletBalanceRetrieve(completion: @escaping (_ data: WalletBalance?, _ error: Error?) -> Void)
```

Get Wallet Balance

<div dir=\"rtl\" style=\"text-align: right;\">  موجودی کیف پول فروشنده  ## توضیحات  این endpoint موجودی کیف پول فروشنده را برمی‌گرداند. کیف پول برای پرداخت هزینه ارسال دیجی‌اکسپرس استفاده می‌شود. هنگام ثبت مرسوله دیجی‌اکسپرس، هزینه ارسال به‌صورت خودکار از کیف پول کسر می‌شود.  نیاز به **API_KEY** فروشنده دارد.  </div> 

### Example
```swift
// The following code samples are still beta. For any issue, please report via http://github.com/OpenAPITools/openapi-generator/issues/new
import OpenAPIClient


// Get Wallet Balance
MerchantWalletAPI.walletsApiV1WalletBalanceRetrieve() { (response, error) in
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


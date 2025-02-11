**Get Started With Installing The Package**

```
composer require shurjomukhi/shurjopay-plugin-php
```

**Then Read The .Env File And Make A Surjopay Instance Using That Env Data**

```
$env = new ShurjopayEnvReader(base_path('.env'));
$sp_instance = new Shurjopay($env->getConfig());
```

Tip. Create A 'transaction_track' Table And Track Every Step Of The Payment Process, From Start To End.

**In The .env File Add Those Environmental Variable**
```
# shurjopay merchant username
SP_USERNAME=''
# shurjopay merchant password
SP_PASSWORD=''
# Merchant prefix used to generate order id
SP_PREFIX=''
# shurjopay payment gateway API endpoint
SHURJOPAY_API='https://engine.shurjopayment.com'
# URL to redirect after completion of a payment. Sample: https://sandbox.shurjopayment.com/response
SP_CALLBACK='http://192.168.10.96:8000/payment-success'
# Log location of shurjopay php plugin
SP_LOG_LOCATION='/var/log/shurjopay'
# CURLOPT_SSL_VERIFYPEER=0 only for local and non-SSL environment
CURLOPT_SSL_VERIFYPEER=0
```

**Then Create A PaymentRequest Object, Add Necessary Data, And Call makePayment function With The Request Object**
```
$request = new PaymentRequest();
$request->currency = 'BDT';
$request->amount = $order_summery->total;
$request->discountAmount = 0;
$request->discPercent = 0;
$request->customerName = $user_data['full_name'];
$request->customerPhone = $user_data['phone'];
$request->customerEmail = $user_data['email'];
$request->customerAddress = $user_data['street_address'];
$request->customerCity = $user_data['city']->name;
$request->customerState = $user_data['state']->name;
$request->customerPostcode = $user_data['zip_code'];
$request->customerCountry = 'Bangladesh';
$request->shippingAddress = $user_data['street_address'];
$request->shippingCity = $user_data['city']->name;
$request->shippingCountry = 'Bangladesh';
$request->receivedPersonName = $user_data['full_name'];
$request->shippingPhoneNumber = $user_data['phone'];
$request->value1 = $onhold_order_details->id;

$sp_instance->makePayment($request);
```

Tip. You Can Pass Any String Data In The value1, value2, value3 And value4. You Will get Your Data Back From The Response Of verifyPayment() function

**PaymentRequest() And ShurjopayEnvReader() Should Come From SurjoPay Plugin Package**

```
use ShurjopayPlugin\PaymentRequest;
use ShurjopayPlugin\ShurjopayEnvReader;
```

**If Payment Is Successful Surjopay Will Redirect You To Your Payment Success URL, You Will Get Your Order Id As A Get Request Parameter, Then Use The Order Id To Verify Your Payment**
```
$order_id = $request->get('order_id');

$env = new ShurjopayEnvReader(base_path('.env'));
$sp_instance = new Shurjopay($env->getConfig());

$payment_response_array = $sp_instance->verifyPayment($order_id);
$onhold_order_details_id = $payment_response_array[0]->value1;
```

make sure to update your transaction_track table in every step of the process

**In The JsonResponse From verifyPayment() Function. Grab The 0th Element, If The Payment Was Success sp_code will be 1000 and sp_message will be Success **

```
$payment_response_array[0]->sp_code == "1000" &&  $payment_response_array[0]->sp_message == "Success"
```

1. Get Started By Downloading The Template Files From Official [SSLCommerz Laravel](https://github.com/sslcommerz/SSLCommerz-Laravel) Github Repositories
2. Copy Every File To Your Project Accoding To Their Exect Path In The Templete Project.
3. In The Middleware Folder There Should Be A File VerifyCsrfToken.php Which Will Be Already Present In Your Project. Just Repleace Your $except Array With Below Array
   ```
   protected $except = [
       '/pay-via-ajax', '/success','/cancel','/fail','/ipn'
   ];
   ```
4. Make A Table To Track The Transaction State. You Can Create You Custom Table Or You Can Use The Default Table Provided By SSLCommerz
5. Lets Use The Default table. In the phpmyadmin Import The Sql File Provided By The Template Project.
6. In The .env File Add Some Env Variable
   ```
   SSLCZ_STORE_ID=""
   SSLCZ_STORE_PASSWORD=""
   SSLCZ_TESTMODE="True"
   SSLCZ_SUCCESS_URL="/success"
   SSLCZ_FAILED_URL="/fail"
   SSLCZ_CANCEL_URL="/cancel"
   SSLCZ_IPN_URL="/ipn"
   ```
7. You can Initiate A Payment Sequence By Calling The index Function Of SslCommerzPaymentController.php Controller. Make A Route Of Post Method And Connect The Function To The Route
8. Then Customize The Index Function To Add Real Info About The Transaction
9. In The config/sslcommerz.php File Grab The success, failed, cancel and ipn url From .Env File Instead of HardCode Url
10. Now In The SslCommerzPaymentController.php File Change And Add Your Bussness Logic To The success fail cancel and ipn function
11. In Case Of Production make SSLCZ_TESTMODE="false" And Put Live Details In The SslCommerz Credentials Variable in the .env File

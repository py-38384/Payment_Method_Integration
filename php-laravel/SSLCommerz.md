1. Get Started By Downloading The Template Files From Official [SSLCommerz Laravel](https://github.com/sslcommerz/SSLCommerz-Laravel) Github Repositories
2. Copy Every File To Your Project Accoding To Their Exect Path In The Templete Project.
3. In The Middleware Folder There Should Be A File VerifyCsrfToken.php Which Will Be Already Present In Your Project. Just Repleace Your $except Array With Below Array
   ```
   protected $except = [
       '/pay-via-ajax', '/success','/cancel','/fail','/ipn'
   ];
   ```
4. Make A Table To Track The Transaction State. You Can Create You Custom Table Or You Can Use The Default Table Provided By SSLCommerz
5. In Th

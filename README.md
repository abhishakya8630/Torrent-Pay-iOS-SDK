# Introduction
TorrentPay Browser (codename: Godel) aims to reduce friction in Second Factor Authentication for Cards and Netbanking.
The library provides various convenience and security features for users to be able to complete the transaction quickly. The library also provides much deeper insight into the events occurring in the payment flow. With Godel, you will be able to provide a pleasing payment experience to your Android users.

# SDK Integration Steps
  ### Step 1: Configuration:
   #### First merchants need to call the ConnectionWrapper from checkout activity and need to pass the configuration parameters in a Dictionary.
             Bundle configuration= new Bundle();
             configuration.putInt("environment",2);
             configuration.putInt("theme_id",1); 
             configuration.putStringArrayList("return_urls",String[]); 
             configuration.putString("post_data","https://www.pinelabs.com/make-payment"); 
             configuration.putInt("should_start_pine_pg_loader", true/false);
             BrowserCheckout .openConnection(context, configuration);

              
### Step 2: Service calling
#### Two parameters, object of implentation of ICallbackResponses and payment parameters in json object will be required to start the browser.
           BrowserCheckout.makeServiceCall(objCallBack,paymentParameters) will be used to start the browser 
           objCallBack:Object of IPinePGResponseCallback interface implementation 
           paymentParameters:Payment parameters to be specified in Bundle object
                  
### 2.1: ICallbackResponses Callback:
  #### Merchant need to implement the ICallbackResponses for the callback to get the transaction response
              public IPinePGResponseCallback objCallBack=new IPinePGResponseCallback(){
                  @Override
                  public void onPageStarted(WebView view, String url) 
                  { //will be called when webview starts loading
                  }
                  @Override
                  public void onErrorOccured (int code,String message) 
                  {
                  //will be called if any error occurs
                  //error code and error message will be passed
                  }
                  @Override
                  public void onTransactionResponse(Bundle response) 
                  {
                  }
                  //will be called when end url is reached
                  //Txn response will be passed in bundle object
                  @Override
                  public void onWebViewReady(WebView webView) 
                  { //will be called when page finished loading
                  }
                  @Override
                  public void onCancelTxn () 
                  {
                  //will be called when user cancels the transaction
                  }
                  @Override
                  public void onPressedBackButton () {
                  //will be called when user back pressed the button
                  } };

                        
 ### 2.2: Payment parameters
#### Merchant need to pass the payment parameter in a bundle object to start the payment
              Bundle paymentParameters = new Bundle(); 
              paymentParameters.putString("merchant_id",String); //Compulsory 
              paymentParameters.putString("order_id",String); 
              paymentParameters.putString("transaction_id",String); //Compulsory 
              paymentParameters.putString("amount_in_paise",String); 
              paymentParameters.putString("customer_id",String); 
              paymentParameters.putString("customer_email",String); 
              paymentParameters.putString("customer_phone_no",String);
              
### Start the service:
              BrowserCheckout.makeServiceCall(MerchantCallback(),paymentParameters)
### Stop the service:
              BrowserCheckout.requestServiceStop()
              
#### This method can be called any time to stop the browser and callback will be triggered.
              responseBundle.getBoolean(“is_error_occurred”);
              responseBundle.getInt(“error_code”);
              responseBundle.getString(“error_message”);
              responseBundle.getBoolean(“have_sms_permission”);
              responseBundle.getBoolean(“is_otp_detected”);
              responseBundle.getBoolean(“is_back_pressed”);
              responseBundle.getBoolean(“is_otp_approved”);
              responseBundle.getString(“start_url”);
              responseBundle.getString(“payment_finish_time”);
              responseBundle.getString(“payment_start_time”)

## 2 .Manifest configuration:
### Minimum permission required
              <manifest ...>
               <uses-permission android:name="android.permission.INTERNET" />
               <uses-permission android:name="android.permission.READ_SMS" />
               <uses-permission android:name="android.permission.RECEIVE_SMS" />
               <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
              </manifest>
              
# ScreenShots

<img width="360" alt="Screenshot 2020-10-22 at 12 02 33 AM" src="https://user-images.githubusercontent.com/23396167/96767340-07e2fc00-13fa-11eb-8716-5a4e5be11da8.png"> <img width="375" alt="Screenshot 2020-10-22 at 12 00 38 AM" src="https://user-images.githubusercontent.com/23396167/96767534-48db1080-13fa-11eb-8d68-324aa2f322e6.png"> <img width="349" alt="Screenshot 2020-10-22 at 12 02 13 AM" src="https://user-images.githubusercontent.com/23396167/96767591-5a241d00-13fa-11eb-9051-8b9f692f0c6b.png">

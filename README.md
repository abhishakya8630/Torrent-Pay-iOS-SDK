#Introduction
TorrentPay Browser (codename: Godel) aims to reduce friction in Second Factor Authentication for Cards and Netbanking.
The library provides various convenience and security features for users to be able to complete the transaction quickly. The library also provides much deeper insight into the events occurring in the payment flow. With Godel, you will be able to provide a pleasing payment experience to your iOS users.

# SDK Integration Steps
  ## Step 1: Configuration:
   ### First merchants need to call the ConnectionWrapper from checkout activity and need to pass the configuration parameters in a Dictionary.
              var configuration= Dictionary<String,Any>();
              configuration ["environment"] = 2;
              configuration ["theme_id"] = 1 ;
              configuration ["return_urls"] = String[];
              configuration ["post_data"] ="https://www.pinelabs.com/make-payment";
              configuration ["should_start_pine_pg_loader”] = true/false;
              configuration ["navigation_bar”] = true/false;
              
              
## Step 2: Service calling
### Two parameters, object of implentation of ICallbackResponses and payment parameters in json object will be required to start the browser.
                  ConnectionWrapper.makeServiceCall(MerchantCallback(),paymentParameters) will be used to start
                  the browser
                  MerchantCallback(),: Inherited class object of ICallbackResponses interface implementation
                  paymentParameters: Payment parameters to be specified in Dictionary object
                  
## 2.1: ICallbackResponses Callback:
  ### Merchant need to implement the ICallbackResponses for the callback to get the transaction response
                        public class MerchantCallback: ICallbackResponses{
                        public func onErrorOccured (code:Int ,message:String)
                        {
                        //will be called if any error occurs
                        //error code and error message will be passed
                        }
                        public func onTransactionResponse(response:Dictionary<String,Any>)
                        {
                        //will be called when end url is reached
                        //Txn response will be passed in bundle object
                        }
                        public func onCancelTxn (code:Int,message:String)
                        {
                        //will be called when user cancels the transaction
                        }
                        public func onPressedBackButton(code:Int,message:String)
                        {
                        //will be called when user back pressed the button
                        }
                        public func ValidationFailure(code:Int,message:String)
                        {
                        //will be called when user back pressed the button
                        }
                        public func internetNotAvailable(code:Int,message:String)
                        {
                        //will be called when user back pressed the button
                        }
                        
 ## 2.2: Payment parameters
## Merchant need to pass the payment parameter in a bundle object to start the payment
                        var paymentParameters= Dictionary<String,String>();
                        paymentParameters["merchant_id"]=String;
                        paymentParameters["order_id"]=String;
                        paymentParameters["transaction_id"]=String;
                        paymentParameters["amount_in_paise"]=String;
                        paymentParameters["customer_id"]=String;
                        paymentParameters["customer_email"]=String;
                        paymentParameters["customer_phone_no"]=String;
### Start the service:
               ConnectionWrapper .makeServiceCall(MerchantCallback(),paymentParameters)
## Stop the service:
### This method can be called any time to stop the browser and callback will be triggered.
                          BrowserCheckout .requestServiceStop()
                          Browser Response: Merchant can access the response of ConnectionWrapper by using response
                          Dictionary object passed at the time of onTransactionResponse callback.
                          responseBundle[“is_error_occurred”];
                          responseBundle[“error_code”];
                          responseBundle[“error_message”];
                          responseBundle[“have_sms_permission”];
                          responseBundle[“is_otp_detected”];
                          responseBundle[“is_back_pressed”];
                          responseBundle[“is_otp_approved”];
                          responseBundle[“start_url”];
                          responseBundle[“payment_finish_time”];
                          responseBundle[“payment_start_time”]

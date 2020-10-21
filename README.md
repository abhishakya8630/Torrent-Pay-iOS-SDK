# Introduction
TorrentPay for Mobile SDK facilitates enhanced mobile payments experience for end user in mobile app eco-system. It helps to build best in market mobile-based payment systems using this SDK.

TorrentPay enhances the payment experience and boosts the success rate with the following array of the features.

1.  **Auto-OTP processing**
###### In TorrentPay enabled transaction journey, Auto-OTP processing involves following functions.

- It reads the OTP from the customer's registered mobile number.
- It shows the OTP to the customer and asks for the approval to process the same.
- Once approved, it inputs the OTP in the required filed and processes it further.

2. **Showing correct keypad for required input**
###### On any mobile application, on the tap on any input field the keypad pops up. The keypad of Android and iOS show alphabetic keypad as a default for every input field. The feature of "Showing correct keypad for required input" involves the following.

- The numeric keypad to be opened if the input to be entered is numeric. For example, the customer ID of HDFC bank is numeric. When a customer clicks on input filed of customer ID the numeric keypad will be opened.
- Fields where input can be alpha numeric, the default keypad will be opened.

3. **Auto-zoom and Auto-scroll**
###### In a normal transaction journey, the bank page opens in the following two fashions.

- Page fits in the mobile screen - In such cases, due to small size of mobile screens, the content of the page is very difficult to read. So, the customer must zoom-in into the page to see the content and tap on the input box. In Pine Labs' Plural Checkout enabled payment page, the bank page is zoomed in automatically and customer can easily enter the input to proceed with the transaction.
- The input field is not visible - Input box is not visible on the screen. In such cases, the customer must scroll left, scroll right, scroll up, and scroll down to reach the input box. With Pine Labs' Plural Checkout payment pages, input is focused, and a user does not have to scroll.

4. **Remember Net banking User ID**
###### It pertains to the Net Banking transactions in which the customer has given the permission to remember the Net Banking user ID. When the customer visits the application subsequently for any transaction, Net Banking user ID is shown pre-filled. Customer can the change Net Banking user ID in case he intends to transact from another user ID of the same bank.

5. **Auto-manual reload when page load fails**
###### When the payment page fails to load customers tends to cancel the transaction. It impacts the success rate of transaction. With TorrentPay the page reloads automatically on page load failures or the customer can reload the page.

## SDK Integration Steps
### Step 1: Configuration:
#### First merchants need to call the ConnectionWrapper from checkout activity and need to pass the configuration parameters in a Dictionary.
          var configuration= Dictionary<String,Any>();
          configuration ["environment"] = 2;
          configuration ["theme_id"] = 1 ;
          configuration ["return_urls"] = String[];
          configuration ["post_data"] ="https://www.pinelabs.com/make-payment";
          configuration ["should_start_pine_pg_loader”] = true/false;
          configuration ["navigation_bar”] = true/false;
### Step 2: Service calling
#### Two parameters, object of implentation of ICallbackResponses and payment parameters in json object will be required to start the browser.
              ConnectionWrapper.makeServiceCall(MerchantCallback(),paymentParameters) will be used to start
              the browser
              MerchantCallback(),: Inherited class object of ICallbackResponses interface implementation
              paymentParameters: Payment parameters to be specified in Dictionary object
### 2.1: ICallbackResponses Callback:
#### Merchant need to implement the ICallbackResponses for the callback to get the transaction response
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
### 2.2: Payment parameters
#### Merchant need to pass the payment parameter in a bundle object to start the payment
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

#### This method can be called any time to stop the browser and callback will be triggered.
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
              
# ScreenShots

<img width="360" alt="Screenshot 2020-10-22 at 12 02 33 AM" src="https://user-images.githubusercontent.com/23396167/96767340-07e2fc00-13fa-11eb-8716-5a4e5be11da8.png"> <img width="375" alt="Screenshot 2020-10-22 at 12 00 38 AM" src="https://user-images.githubusercontent.com/23396167/96767534-48db1080-13fa-11eb-8d68-324aa2f322e6.png"> <img width="349" alt="Screenshot 2020-10-22 at 12 02 13 AM" src="https://user-images.githubusercontent.com/23396167/96767591-5a241d00-13fa-11eb-9051-8b9f692f0c6b.png">

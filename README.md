


SendOTP Android Sdk!
===================


The  **SendOtp** Verification SDK makes verifying phone numbers easy. SDK supports the verification of phone numbers via **SMS & Calls**.

----------

Getting started
===============

Gradle
------

Just add the

    dependencies {
    ...
     implementation 'com.msg91.sendotpandroid.library:library:1.0'
     implementation 'com.googlecode.libphonenumber:libphonenumber:7.0.4'//required
    ...
    }
Maven
------
grab via Maven:

<dependency>
  <groupId>com.msg91.sendotpandroid.library</groupId>
  <artifactId>library</artifactId>
  <version>1.0</version>
  <type>pom</type>
</dependency>

> -Login or create account at [MSG91]([https://control.msg91.com/signup/sendotp](https://control.msg91.com/signup/sendotp)) to use sendOTP services.

#### <i class="icon-file"></i> Get your authKey

After login at [MSG91](https://control.msg91.com/) </i> follow below steps to get your **authkey**




> - Select **API** option available on panel.
> - If you are first time user then generate new authkey.
> - copy authKey & keep it enable, Paste in manifest under application tag.
> `  <meta-data
            android:name="sendotp.key"
            android:value="@string/sendotp_key" />`

#### <i class="icon-book"></i> Usage

>  implement '**VerificationListener**' in your class & override below result callbacks.

     @Override
     public void onInitiated(String response) {
       Log.d(TAG, "Initialized!" + response);
       //OTP successfully resent/sent.
     }

	   @Override
	   public void onInitiationFailed(Exception exception) {
	     Log.e(TAG, "Verification initialization failed: " + exception.getMessage());
	      //sending otp failed.
	   }

	 @Override
	   public void onVerified(String response) {
	     Log.d(TAG, "Verified!\n" + response);
	        //OTP verified successfully.
	   }

	   @Override
	   public void onVerificationFailed(Exception exception) {
	     Log.e(TAG, "Verification failed: " + exception.getMessage());
	     //OTP  verification failed.
	   }


create instance of **Verification** as a class variable and `initialise` it by passing country code and mobile number.
Optional Parameters are gose in blow method.

	 mVerification = SendOtpVerification.createSmsVerification
 	                   (SendOtpVerification
                            .config(countryCode + phoneNumber)

                            .context(this)
			    .unicode(false) // set true if you want to use unicode in sms
                            .autoVerification(false)
                            .httpsConnection(false)//connection to be use in network calls
                            .expiry("5")//value in minutes
                            .senderId("XXXXXX") //where XXXX is any string
                            .otplength("4") //length of your otp max length up to 9 digits
                            //--------case 1-------------------
                            .message("##OTP## is Your verification digits.")//##OTP## use for default generated OTP
                          //--------case 2-------------------
                            .otp("1234")// Custom Otp code, if want to add yours
                            .message("1234 is Your verification digits.")//Here 1234 same as above Custom otp.
                            //-------------------------------------
                            //use single case at a time either 1 or 2
                            .build(), this);
    	        mVerification.initiate();



Note : Add SMS read permission for autoVerification.

sending OTP

    mVerification.initiate();

manually verifying OTP

    mVerification.verify(otp_code);
resend OTP use 'voice' or 'text' as a param.

    mVerification.resend("voice");


**Androidx Developers:**
Add below code in application tag in AndroidManifest.xml file.

    tools:replace="android:allowBackup"

Optional Parameters
------
> - **message**("##OTP## with your Custom OTP message.") [for custom OTP message]
>- **httpsConnection**(true) [secure connection]
>- **expiry**(5) [value in minutes]
>- **senderId**("OTPSMS")
>- **otp**("1234") [use your OTP code]
>- **otplength**("4") [custom OTP length]
>- **unicode**(false) [use unicode (or other languages)]
>**Auto Verification** direct verification while connect with mobile network without enters otp
>three parameter required in that case :
>autoVerification(false)
>setIp(getIp(withoutOtp))
>verifyWithoutOtp(withoutOtp) obtain details are mention in sample code

<img src="https://cloud.githubusercontent.com/assets/8371249/13195073/bcf22e40-d7cd-11e5-9891-f1f656d9ff45.png" width="270">    <img src="https://cloud.githubusercontent.com/assets/8371249/13195075/bcf7b6b2-d7cd-11e5-8e58-0a0c8e8849de.png" width="270">  <img src="https://cloud.githubusercontent.com/assets/8371249/13195074/bcf257f8-d7cd-11e5-970e-78ee034df112.png" width="270">

License
=======

    Copyright 2019 MSG91

    Licensed under the Apache License, Version 2.0 (the "License");
    you may not use this file except in compliance with the License.
    You may obtain a copy of the License at

       http://www.apache.org/licenses/LICENSE-2.0

    Unless required by applicable law or agreed to in writing, software
    distributed under the License is distributed on an "AS IS" BASIS,
    WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    See the License for the specific language governing permissions and
    limitations under the License.

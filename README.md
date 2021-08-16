# Setting up an android environment for dynamic analysis


## Step 0 - Requirements
- [x] Download and install [Genymotion](https://www.genymotion.com/download/) 
- [x] Download and install [Burpsuite](https://portswigger.net/burp/releases/community/latest)
- [x] Install [Frida](https://frida.re/docs/installation/) 

## Step 1 - Installing BurpSuite cacert into Android

Export BurpSuite CA certificate

![burp1](../includes/burp1.png)

Converting cacert file

 `openssl x509 -inform DER -in cacert.der -out cacert.pem`
 
`openssl x509 -inform PEM -subject_hash_old -in cacert.pem |head -1`

`mv cacert.pem <hash>.0`

![burp2](../includes/burp2.png)

In a previously installed genymotion create a new android virtual device `avd`

![burp3](../includes/burp3.png)

Now its needed to transfer your burp certificate in an android-readable format to your `avd`

`/opt/genymobile/genymotion/tools/adb shell mount -o rw,remount /system`

`/opt/genymobile/genymotion/tools/adb push 9a5ba575.0 /system/etc/security/cacerts/9a5ba575.0`

![burp4](../includes/burp4.png)

`/opt/genymobile/genymotion/tools/adb shell chmod 644 /system/etc/security/cacerts/9a5ba575.0`

![burp5](../includes/burp5.png)

Now your certificate must be installed on your device, you can check it on the System Trusted credentials

![burp6](../includes/burp6.png)

## Step 2 - Setup BurpSuite proxy on Android

![burp7](../includes/burp8.png)

![burp8](../includes/burp8.png)

Now you can proxy your android device traffic.



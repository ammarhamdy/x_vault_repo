
To export Burp Suite’s **CA certificate** so that you can install it on your Android device (for HTTPS interception), follow these steps:

* * *

### ✅ Step-by-Step: Export Burp Suite CA Certificate for Android

#### 🔧 Requirements:

* **Burp Suite** (Community or Pro)
    
* Android device connected to the **same Wi-Fi network**
    
* Burp Suite running as a **proxy** (default: `127.0.0.1:8080`)
    
* Burp listening on your computer's **LAN IP** (not just localhost)
    

* * *

### 🧰 Step 1: Configure Burp to Listen on External Interface

1. Go to **Proxy > Options > Proxy Listeners**
    
2. Click **Edit** the default listener (usually 127.0.0.1:8080)
    
3. Change it to listen on **All interfaces** or your **computer’s LAN IP**
    
4. Click **OK** and ensure it's running
    

* * *

### 🌐 Step 2: Set Proxy on Android Device

On your Android device:

1. Go to **Settings > Wi-Fi**
    
2. Long press your connected network > **Modify network**
    
3. Under **Advanced options**, set:
    
    * **Proxy** = Manual
        
    * **Hostname** = your computer's IP (e.g., `192.168.1.10`)
        
    * **Port** = `8080` (or whatever Burp is using)
        

* * *

### 📥 Step 3: Download Burp's CA Certificate on Android

1. Open the browser on your Android device
    
2. Go to: `http://burp` (yes, just `http://burp`)
    
3. Download the certificate file:
    
    * **`cacert.der`**
        

* * *

### 🛠️ Step 4: Convert and Install Certificate

#### 📌 Android 7+ (Nougat and later):

Android only trusts **user certificates** for **non-system apps**. 
For system apps or apps with **certificate pinning**, you’ll need rooting or Frida.

##### 🧾 Rename:

Change `cacert.der` to `burp.cer`

##### 🛜 Install Certificate:

1. Go to **Settings > Security > Install from storage**
    
2. Choose **CA certificate** and locate `burp.cer`
    
3. Confirm installation (you’ll see a warning about network monitoring)
    

* * *

### 🚫 Note on Certificate Pinning

Some apps use **certificate pinning** to prevent Burp from intercepting HTTPS, even with the certificate installed.

➡️ To bypass this, you’ll need tools like:

* **Frida** (to hook and disable pinning dynamically)
    
* **Objection**
    
* Or **patch the APK** (if you're reverse engineering)
    

* * *
Connecting to CSU Off Campus
=============================

When you're off-campus, you'll need to use the university’s Virtual Private Network (VPN) to access our network securely. Think of a VPN like a safe, private tunnel that protects the information on your computer from prying eyes. This secure connection is very important because it keeps your work and research data safe even when you’re not on the CSU campus.

In this guide, we will also show you how to set up DUO on your phone. DUO is a free app that adds an extra step to confirm your identity (a process called two-factor authentication) before you can log in. This extra check makes it much harder for someone else to access your account. After setting up DUO, the guide will walk you through installing and using the Global Protect VPN client so you can easily connect to our secure system.

Installing DUO on Mobile
--------------------------

1. **Download the Duo Mobile App**

   - Open the **App Store** (iOS) or **Google Play Store** (Android).
   - Search for **Duo Mobile** and install the app.

2. **Register Your Smartphone or Tablet**
   
   - Log in to the `NetID Two-Factor Authentication (Duo) <https://netid.colostate.edu/twofactor.aspx>`_ page using your NetID and password.
   - Click **Register Device** on the right side of the page.
   - Enter a unique **Device Name** (e.g., *Cam's iPhone 14*).
   - Select **Duo Mobile App** from the **Type** dropdown.
   - Choose your device platform (e.g., *Apple iOS*, *Google Android*) from the **Platform** dropdown.
   - Click **Save** to store your device information.
   - After saving, the page will refresh to the **Two-Factor Device Activation** screen, displaying a **barcode**. Leave this page open.

3. **Activate Duo Mobile**
   
   - Open the **Duo Mobile** app on your device.
   - Tap **+ Add** next to the **Accounts** section.
   - Use the app’s barcode scanner to **scan the barcode** displayed on the Two-Factor Device Activation page.
   - Once activated, Duo Mobile will show **Colorado State University** as an account.
   - Click **Return** to view your registered devices.


Installing Global Protect
--------------------------

.. tabs:: 

   .. tab:: Windows

      1. **Download the Installer**
         
         Use your web browser to connect to the `GlobalProtect web portal downloads page <https://gateway.colostate.edu/global-protect/getsoftwarepage.esp>`_ and select the appropriate version for your Windows device:
         
         - **64-bit Windows** (Most common): Click "Download Windows 64-bit GlobalProtect agent".
         - **32-bit Windows** (Older devices): Click "Download Windows 32-bit GlobalProtect agent".
         - **ARM Windows** (Surface and tablets): `Submit a help request <https://csusystem.freshservice.com/support/tickets/new>`_ for the GlobalProtect ARM installer.

         **Tip:** To check your processor type, open *About Your PC* and look at *System Type*.

      2. **Install the Software**
         
         After downloading the installer, open it and proceed through the installation steps. Once installation is complete, open GlobalProtect from the Start menu.

      3. **Configure and Connect**
         
         - Enter `gateway.colostate.edu` or `pueblogateway.colostate.edu` as the Gateway Address.
         - Click **Connect**.

      4. **Authenticate with Duo**
         
         Before the connection can be established, you'll need to authenticate using Duo for security.

      5. **Verify Connection**
         
         Once GlobalProtect displays **"Connected"**, your VPN is active and you may now securely access CSU resources.


   .. tab:: MacOS
      
      1. **Download the Installer**
   
         Use your web browser to connect to the `GlobalProtect web portal downloads page <https://gateway.colostate.edu/global-protect/getsoftwarepage.esp>`_ and select:
         
         - Click **"Download Mac 32/64-bit GlobalProtect agent"**.
         - **Important:** Do **not** install GlobalProtect from the Apple App Store unless you're using an iPhone or iPad.

      2. **Install the Software**
         
         After downloading the installer, open it and proceed through the installation steps.  
         - On the *Installation Type* step, **check the box for "GlobalProtect System extensions"**—GlobalProtect will not work if this system extension is missing.

      3. **Security Settings on macOS**
         
         When you open GlobalProtect for the first time, macOS may prompt you to modify your security settings.  
         - Follow the instructions carefully—GlobalProtect will **not** work unless these settings are adjusted.

      4. **Configure and Connect**
         
         - Open GlobalProtect from **Spotlight**.
         - Enter `gateway.colostate.edu` or `pueblogateway.colostate.edu` in the **Portal** field.
         - Click **Connect**.

      5. **Authenticate with Duo**
         
         Before GlobalProtect can finish connecting, you'll need to authenticate using Duo for security.

      6. **Verify Connection**
         
         Once GlobalProtect displays **"Connected"**, your VPN is active and ready for use.

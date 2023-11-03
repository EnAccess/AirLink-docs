# AirLink App

The AirLink Mobile app is a communication app skeleton enabling gateway functionality i.e. end to end communication between AirLink Bluetooth® devices and an AirLink server. The app is intended to act as a base that takes care of device interactions, on which different customer experiences can be built by the businesses adopting AirLink.

![AirLink Data Flow.png](AirLink%20App/AirLink_Data_Flow.png)

Once the *App Instance is authenticated to the tenant or customer by the application server transferring the provisioning codes, it can provision the phone as an AirLink gateway using the phone’s IMEI*. This allows flexibility in lost phones by tying functionality and device ownership to an authenticated user rather than a particular phone. The app provides a UI for entering these codes until the application server is enabled.

The app demonstrates three different roles that can be used to build different business processes:

1. Manufacturer Role: Registering AirLink devices to the server securely - this needs to be the first step
2. End-User Role:
      1. Scanning and connecting to AirLink devices automatically
      2. Updating Pay-as-you-go status of the device securely
      3. Posting data from the device to the server with authentication
      4. Finding AirLink devices even when the app is not running, and posting their locations to the server
3. Device Admin Role: Generating PAYGO tokens for AirLink or Angaza devices - this needs to be done before a User Role could sync the token to the device via the App

## App Chronology

While AirLink Devices are the end use-case for any AirLink business case, and the AirLink server the main infrastructure needed, The AirLink App (or an equivalent hardware gateway) is the *primary enabler*. As such, much of the user activity around the lifecycle of AirLink Devices happens with the Gateway. Here, we take a look at this device lifecycle, which starts with first linking the AirLink App instance to the server.

### Configuring to connect to server (Manufacturer role)

First Step: Enter the information from AirLink Server and Provision the phone as a gateway on the server. In a production app, this information might be hardcoded or saved as credentials within the app, invisible to the user.

!!! info "Security check"
    The server credentials, especially the manufacturer role, is a very powerful role that can impact all devices and data, so it should be shared only as needed and securely encoded into the app!

![home - credentials page - airlink.jpg](AirLink%20App/home%20-%20credentials%20page%20-%20airlink.jpg)

If you enter the data correctly including the tenant administrator, the app instance will be provisioned as a Gateway device on the AirLink Server, allowing data transfer operations and linking to AirLink Devices.

<style>
.youtube-embed-container {
position: relative;
padding-bottom: 56.25%;
height: 0;
overflow:
hidden; max-width: 100%;
}
.youtube-embed-container iframe,
.youtube-embed-container object,
.youtube-embed-container embed { position: absolute; top: 0; left: 0; width: 100%; height: 100%; }
</style>
<div class="youtube-embed-container">
<iframe
src="https://youtube.com/embed/L4Tj_V7B4CE?enablejsapi=1"
frameborder="0"
allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share"
allowfullscreen>
</iframe>
</div>

### Discovering AirLink devices

Second Step: Your phone is ready to sync devices. Discover AirLink devices in the vicinity! (The AirLink App looks for CBOR-encoded advertisements as an identifying signature to filter out AirLink devices from other BLE devices that might be present).

![Devices view](AirLink%20App/home%20-%20device%20list%20page.jpg)

Once you find a device, tapping on it simply brings up a list of Nexus resources available on the device

![Resources view](AirLink%20App/home%20-%20device%20list%20page%20-%20device%20details%20page.jpg)

!!! info "Device Emulator App"

    To enable quick end to end testing of AirLink, we have designed a single-page Android-native app that imitates an AirLink device with temperature, battery and device configuration resources. The source code of this app as well as an Android-9 executable APK is saved in the [AirLink Devices Github repository](https://github.com/EnAccess/AirLink-Devices) under the Device Simulator folder.

    ![Device Simulator app running on an Android-9 phone](AirLink%20App/AirLink_BLE_Simulator.jpg)

    Device Simulator app running on an Android-9 phone

    This app allows you to:

    1. Pair with the main AirLink (gateway) app on another phone
    2. Go through the provisioning flow and initialize the token generation flow
    3. Send data to the server via the AirLink gateway app
    4. Accept tokens from the server - although there is no nexus token decoder running in the app, so it will accept any token

    The source code is meant as a reference when designing embedded firmware that can match AirLink’s provisioning and data exchange flows. With the emulator app, anyone can test AirLink without requiring hardware, simply by downloading it onto an Android phone, installing the AirLink gateway app on another phone, and logging on to the demo/custom tenant on the AirLink server.

    The [source code](https://github.com/EnAccess/AirLink-Devices) is not meant to actually process tokens, but could act as a starting point if Android Airlink devices are being developed.

### Authorizing the gateway to the device with the Access Token

Always, when connecting to a device, we recommend that the device lock it’s properties until the (default or server) access token is supplied. Authorizing the device supplies it with the default access token. To authorize the device, simply tap the “Authorize” button. The default access token is already saved on both the App and the device. The device will then compare its access token with this default one. Once they match, the device will be successfully authorized.

![AUTHORIZE](AirLink%20App/home%20-%20device%20list%20page%20-%20device%20details%20page%20authorize.jpg)

Once authorized, you can now read data from the device. The App receives CBOR encoded data from the device, and decodes it into a JSON that is more amenable to posting to the server, and displays this for each property when tapped.

![READ RESOURCE - Data is displayed.jpg](AirLink%20App/property%20readout.jpg)

### Serializing and provisioning a new device and preparing it for accepting tokens

If a device has just been manufactured, it may not yet be serialized, and be locked with a default access token. Enter this token, then press “Provision” to provision the device. The app will prompt for serial number entry.

![PROVISION - Choice for serialization.jpg](AirLink%20App/home%20-%20device%20list%20page%20-%20device%20details%20page%20-%20provisioning%20input.jpg)

Scan or enter by hand this serial number. This is a one-time activity after which the device will forever remember it’s serial number. However if the serial number exists on the server, the provisioning will fail. As long as a unique serial number is supplied, the server accepts the device and returns a device-specific access token, which the app saves automatically to secure storage as well as displays in the access token field

!!! info "Provisioning Solaris or Angaza devices"
    For Solaris devices, uploading a CSV to the AirLink server (and correspondingly adding them to the Solaris Distributor account) is the only option.
    Angaza devices can be provisioned via the AirLink app. All you need are your Angaza API credentials for the manufacturer role. Enter these in the server (see rule-chains section):
    <style>
    .youtube-embed-container {
    position: relative;
    padding-bottom: 56.25%;
    height: 0;
    overflow:
    hidden; max-width: 100%;
    }
    .youtube-embed-container iframe,
    .youtube-embed-container object,
    .youtube-embed-container embed { position: absolute; top: 0; left: 0; width: 100%; height: 100%; }
    </style>
    <div class="youtube-embed-container">
    <iframe
    src="https://youtube.com/embed/6GAqmAPOLjI?enablejsapi=1"
    frameborder="0"
    allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share"
    allowfullscreen>
    </iframe>
    </div>

    ![Solaris device provisioning in AirLink](AirLink%20App/home%20-%20device%20list%20page%20-%20device%20details%20page%20-%20provisioning%20input%20with%20type%20expanded.jpg)

### Synchronizing data with the server over the lifetime of the device

All AirLink properties can be kept in sync between the server and the individual device simply by tapping the Sync button, or using the underlying function in an automated flow in your custom version of the app. The ability of the gateway to post device data to the server (”Client Scope”) as well as pull server data into the device (”Shared Scope”) generates a success message. All failure messages can be effectively debugged using the USB-connected debug mode of Visual Studio or IntelliJ.

![Syncing data](AirLink%20App/home%20-%20device%20list%20page%20-%20device%20details%20page%20sync.jpg)

The previous few steps about connecting to devices and synchronizing data are also described in this video:
     <style>
     .youtube-embed-container {
     position: relative;
     padding-bottom: 56.25%;
     height: 0;
     overflow:
     hidden; max-width: 100%;
     }
     .youtube-embed-container iframe,
     .youtube-embed-container object,
     .youtube-embed-container embed { position: absolute; top: 0; left: 0; width: 100%; height: 100%; }
     </style>
     <div class="youtube-embed-container">
     <iframe
     src="https://youtube.com/embed/2zY5vETH4zk?enablejsapi=1"
     frameborder="0"
     allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share"
     allowfullscreen>
     </iframe>
     </div>

### Entering Tokens

Some properties are writeable, especially true for the PAYG token property, found in the “PC” resource. Tapping this will open a prompt to enter a token. During the Provisioning stage, the token generator on the server is initialized and matched to each device’s secret. Hence, the token can be obtained from the server automatically by syncing the phone, or by manually copying the PC_tkn property value and inputting by hand while the phone is offline.

![ENTER PAYG TOKEN](AirLink%20App/home%20-%20device%20list%20page%20-%20device%20details%20page%20-%20transfer%20payg%20token.jpg)

PAYG tokens are single-use and must match the individual device. If these criteria are met, the device accepts the token.

### Generating Tokens

The AirLink App also demonstrates the ability to generate PAYG Tokens for AirLink and Angaza devices.

![Token Generation](AirLink%20App/home%20-%20payg%20token%20page%20-%20token%20generated.jpg)

Also see this video!
     <style>
     .youtube-embed-container {
     position: relative;
     padding-bottom: 56.25%;
     height: 0;
     overflow:
     hidden; max-width: 100%;
     }
     .youtube-embed-container iframe,
     .youtube-embed-container object,
     .youtube-embed-container embed { position: absolute; top: 0; left: 0; width: 100%; height: 100%; }
     </style>
     <div class="youtube-embed-container">
     <iframe
     src="https://youtube.com/embed/OAEcQaUBIao?enablejsapi=1"
     frameborder="0"
     allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share"
     allowfullscreen>
     </iframe>
     </div>

## Architecture

### App Development Framework: Flutter

**Flutter is Google’s multi-platform mobile app development framework.**

   <style>
    .youtube-embed-container {
    position: relative;
    padding-bottom: 56.25%;
    height: 0;
    overflow:
    hidden; max-width: 100%;
    }
    .youtube-embed-container iframe,
    .youtube-embed-container object,
    .youtube-embed-container embed { position: absolute; top: 0; left: 0; width: 100%; height: 100%; }
    </style>
    <div class="youtube-embed-container">
    <iframe
    src="https://www.youtube.com/embed/VPvVD8t02U8?enablejsapi=1"
    frameborder="0"
    allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share"
    allowfullscreen>
    </iframe>
    </div>

**Flutter uses a layered Architecture:** [Flutter architectural overview](https://docs.flutter.dev/resources/architectural-overview)

**UI Design:** Flutter uses design widgets to make it easy to move between software that supports prototyping (e.g. Figma) and app development. This app uses the in-built Flutter widgets to display the app’s functionalities. However, they can be customized to fit the specific needs of the app, allowing you to create unique and engaging user experiences.

!!! info "Flutter packages"
    To realize the BLE requirements and other core functionality of AirLink, the AirLink app (gateway) uses the following packages:

    - cbor: ^6.1.1
    - convert: ^3.0.1
    - hex: ^0.2.0
    - flutter_secure_storage: ^6.0.0
    - http: ^1.1.0
    - device_info_plus: ^3.2.2
    - flutter_barcode_scanner: ^2.0.0
    - location: ^5.0.3
    - provider: ^6.0.2
    - app_settings: ^5.1.1
    - workmanager: ^0.5.1
    - permission_handler: ^11.0.0
    - path_provider: ^2.0.14
    - equatable: ^2.0.5
    - dartz: ^0.10.1
    - get_it: ^7.6.0
    - internet_connection_checker: ^1.0.0+1
    - hive: ^2.2.3
    - hive_flutter: ^1.1.0
    - flutter_dotenv: ^5.1.0
    - flutter_blue_plus: ^1.16.2

## Gateway as a Sync relay - mapping property names

The primary role of an AirLink gateway is to keep AirLink devices (BLE, or GSM devices that can also work without the gateway) and the AirLink server (availabke on GSM/Wifi) in sync with respect to the state and operation of the device. There are three types of **data sync**:

1. Server updates Device: Pay as you go credits after payment are the primary server update, along with client and configuration data

  ![AirLink Gateways or this App maps Server and Device properties](AirLink%20App/IoT_Communications_and_Components_spec_-_App_Architecture-2%201.png)

  AirLink Gateways or this App maps Server and Device properties
2. Device posts time-series telemetry via primary gateway: Device posts various IoT data described in Nexus Resource Models relating to energy generation, consumption, battery use as well as productive output. In this case, the app actually masquerades as the device and posts data directly into the device's telemetry endpoint. This is enabled for the app via user input of device access token or in a production app, from the server pairing the gateway with devices via sharing of the access token automatically upon sale. Location is added by the gateway.
3. Neighborhood watch gateway posts device advertisement: If the app finds an AirLink device that is not registered as managed by that app instance (e.g. that customer doesn't have permissions for that device but another customer might), it will post the device's advertisement data to the server as a 'piggy-back' onto it's own telemetry, which the server then snips out and decides to post to the original device or forward on to the lost devices database.

  ![**AirLink Lost/Stolen Devices Flow**](AirLink_Unknown_Device_Flow.png)

To convert between server-friendly JSON and Bluetooth-service friendly CBOR/.NET objects, the [Json.NET](http://Json.NET) and [PeterO.CBOR](https://github.com/peteroupc/CBOR) libraries are used. Since the list of properties can vary, we use collections and read the property types = device resource models such as “/batt” and “/temp” from the Bluetooth Descriptors.

[Serializing Collections](https://www.newtonsoft.com/json/help/html/SerializingCollections.htm)

---

![Simusolar Inc](Simusolar_logo.png)

Copyright 2023 Simusolar Inc

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

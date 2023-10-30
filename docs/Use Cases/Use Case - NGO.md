# An NGO wanting to define a adaptable hardware/software standard for data collection in your projects or grantees

## Why adopt AirLink as an NGO

Several common needs for IoT data transfer at low cost and poor-network areas using a semi-skilled workforce of agents are covered natively by AirLink, and customization to a particular device type or project can be done with software modifications. Further, hardware devices get a clear spec to design to from this AirLink documentation, making it easier to engage contractors.

## Out of the box

AirLink, after you complete the *first three steps* in [the video playlist](https://www.youtube.com/playlist?list=PLzs9gB3KSMw_u0zuKGCKE0x2EER0s6ONP), also detailed in the [Quick-Start](Quick-start%20guide.md), can synchronize data from AirLink-compatible devices to the server without any other setup. Server data and device configuration updates can be pulled from the server when in network range, and device updates and data collection from the device can be done fully offline over Bluetooth®. This can be tested using the AirLink Gateway App and AirLink Devices app as shown in the guide.

To customize this behavior for your own data collection project, you will need to customize your Bluetooth® device firmware as well as the open-source AirLink App as below:

## Making Devices compatible with AirLink

If the devices that will serve the data you need to collect have Bluetooth® enabled, then compatibility takes four simple steps focused on Advertisement and Data format, and optionally on authentication. Please discuss these with the device manufacturer, and ensure that they get the devices declared with the Bluetooth® SIG:

1. Customize the Advertisement packet to match AirLink spec, as mentioned in the [AirLink Devices](AirLink%20Devices.md) page. The easiest way to do this is to fork the open source [Nordic nRF firmware codebase](https://www.nordicsemi.com/Products/Bluetooth-Low-Energy).
2. Group similar properties e.g. tempC, maxTemp. Create a [CBOR array](https://cbor.me) with these properties. These will be transferred once the app connects to the device
3. Name the Bluetooth® *descriptor* with the property name e.g. 'temp'. Then, AirLink will understand your properties as temp_tempC, temp_maxTemp etc and on successful sync you will find these properties in the timeseries data for that device on the server. Device configurations are also saved similarly in dcfg_* properties.
4. Optional: Build an access control flow in your devices which relies on a Server Access Token "password" unique to the device, starting with a pre-programmed value which is entered into to the firmware. Then, your device will only allow data transfer from/to a particular app which knows the default access token - and once provisioned on the server, will receive an access token *unique* to it. All device data access control will then be locked to phones that can access this unique device token from the server, based on the Role-Based Access Control functions available on the server.

## Building information ownership

Want to assign devices to certain agents? Want to ensure that they automatically pull data when in range / on a button press? Need to store access tokens for certain devices on certain agent phones? No problem! All of these can be achieved using the API access between the AirLink App and the server, and the Role Based Access Control available in thingsboard. The full documentation for the server API is live at the server's [Swagger URL](https://airlink.enaccess.org/swagger-ui.html).

Here are some starting ideas to get your work setup. These can be either done in the Flutter app itself, or on a server running your own application stack "Your Stack".

1. Relating Agents and Devices - AirLink Server UI OR Flutter App OR Your Stack - The first step is to create a relation from the Agent or Customer, registered as a user or customer in the AirLink server, to your device. You can do this via the AirLink server UI, or API access using the "Tenant Administrator" role available in the Flutter app for demonstration, as shown below:
    UI: ![Relating Devices to Other Entities via UI](AirLink%20Server/RelatingDevicesToEntities.gif)

    API: [Adding Relations via API](https://airlink.enaccess.org/swagger-ui/#/entity-relation-controller/saveRelationUsingPOST)

2. Pulling relevant Server Access Tokens from the server for devices related to a particular app - Flutter App - The first step here is to relate each app instance to the user/customer created in Step #1. At Simusolar for example, we built a SMS based authentication flow for customers and an email based flow for our Staff, all using Thingsboard.io Rule Chains on the AirLink server connecting to our software stack via API. Once you have users/customers related to the app instance, the relations built in Step #1 will indirectly relate the devices to the app instance. You can then download a list of all the devices that have the relevant relationship, using a query based lookup supported by the AirLink server. For this, you will need to use the "Tenant Administrator" role in the Flutter App and access this API:
    [Entity Query Controller](https://airlink.enaccess.org/swagger-ui/#/entity-query-controller)
    and then then get the Access Tokens for each of the related devices:
    [Device credentials by ID](https://airlink.enaccess.org/swagger-ui/#/device-controller/getDeviceCredentialsByDeviceIdUsingGET)

## Using the devices and app to collect data at scale

1. Device initialization and Use - Flutter App -
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
2. Synchronizing data via app - Flutter App -
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
3. Optional: Create an Automation in your Flutter app that scans for devices, connects to them one by one and pulls data from them to make the process seamless for an Agent or user. The open-source app has the mechanism for the individual steps but leaves the process automation to you depending on your use case.

---

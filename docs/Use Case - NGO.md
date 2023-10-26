# An NGO wanting to define a adaptable hardware/software standard for data collection in your projects or grantees

## Why adopt AirLink as an NGO

Several common needs for IoT data transfer at low cost and poor-network areas using a semi-skilled workforce of agents are covered natively by AirLink, and customization to a particular device type or project can be done with software modifications. Further, hardware devices get a clear spec to design to from this AirLink documentation, making it easier to engage contractors.

## Out of the box

AirLink, after following the [Quick-Start](Quick-start%20guide.md), can synchronize data from AirLink-compatible devices to the server without any other setup. Server data and device configuration updates can be pulled from the server when in network range, and device updates and data collection from the device can be done fully offline over Bluetooth®. This can be tested using the AirLink Gateway App and AirLink Devices app as shown in the guide.

To customize this behavior for your own data collection project, you will need to customize your Bluetooth® device firmware as well as the open-source AirLink App as below:

## Making Devices compatible with AirLink

If the devices that will serve the data you need to collect have Bluetooth® enabled, then compatibility takes four simple steps focused on Advertisement and Data format, and optionally on authentication. Please discuss these with the device manufacturer, and ensure that they get the devices declared with the Bluetooth® SIG:

1. Customize the Advertisement packet to match AirLink spec, as mentioned in the [AirLink Devices](AirLink%20Devices.md) page.
2. Group similar properties e.g. tempC, maxTemp. Create a [CBOR array](https://cbor.me) with these properties. These will be transferred once the app connects to the device
3. Name the Bluetooth® *descriptor* with the property name e.g. 'temp'. Then, AirLink will understand your properties as temp_tempC, temp_maxTemp etc and on successful sync you will find these properties in the timeseries data for that device on the server. Device configurations are also saved similarly in dcfg_* properties.
4. Optional: Build an [access control flow](#airlink-main-flows) in your devices which relies on a Server Access Token "password" unique to the device, starting with a pre-programmed value which is entered into to the firmware. Then, your device will only allow data transfer from/to a particular app which knows the default access token - and once provisioned on the server, will receive an access token *unique* to it. All device data access control will then be locked to phones that can access this unique device token from the server, based on the Role-Based Access Control functions available on the server.

## Building information ownership

Want to assign devices to certain agents? Want to ensure that they automatically pull data when in range / on a button press? Need to store access tokens for certain devices on certain agent phones? No problem! All of these can be achieved using the API access between the AirLink App and the server, and the Role Based Access Control available in thingsboard. The full documentation for the server API is live at the server's [Swagger URL](https://airlink.enaccess.org/swagger-ui.html).

Here are some starting ideas to get your work setup. These can be either done in the Flutter app itself, or on a server running your own application stack "Your Stack".

1. Relating Agents and Devices - AirLink Server UI OR Flutter App OR Your Stack - The first step is to create a relation from the Agent or Customer, registered as a user or customer in the AirLink server, to your device. You can do this via the AirLink server UI, or API access using the "Tenant Administrator" role available in the Flutter app for demonstration, as shown below:
   UI:
   ![]()

   API:
   []()

   ![]()
2. Pulling relevant Server Access Tokens from the server for devices related to a particular app - Flutter App - The first step here is to relate each app instance to the user/customer created in Step #1. At Simusolar, we built a SMS based authentication flow for customers and an email based flow for our Staff, all using Thingsboard.io Rule Chains on the AirLink server connecting to our software stack via API. Once you have users/customers related to the app instance, the relations built in Step#1 will indirectly relate the devices to the app instance. You can then download a list of all 'Server Access Tokens' from the server for the devices that have the relevant relationship, using a query based lookup supported by the AirLink server. For this, you will need to use the "Tenant Administrator" role in the Flutter App andn access this API:
   []()

   For example, to download access tokens related to a particular customer's "Owned" devices, here is the code:

   ```JSON
   abcd
   ```

## Using the devices and app to collect data at scale

1. Admin and Agent roles for Device initialization and Use - Flutter App -
2. Auto-synchronizing - Flutter App -
3. Optional: Create an Automation in your Flutter app that scans for devices, connects to them one by one and pulls data from them to make the process seamless for an Agent or user. The open-source app has the mechanism for the individual steps but leaves the process automation to you depending on your use case.

---

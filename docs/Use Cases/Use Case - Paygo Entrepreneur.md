# A Fintech/PAYGO entrepreneur focused on innovative software, needing a standard hardware spec to share with a device manufacturer

## Why AirLink as a Fintech/PAYGO entrepreneur

Does your idea require network-connected or PAYGO devices at low cost? Are you planning on a smartphone app as the primary UI for the customer / end user? Do you want to get started with your idea quickly? Then AirLink might be for you!

## Trying AirLink out

You can decide if AirLink is for you by simply downloading two apps and getting access to the demo server from EnAccess. The [Quick-start](../Quick-start%20guide.md#Trying-out-AirLink-is-easy) outlines this process.

## Saving MVP costs

AirLink can help you get to MVP quickly and cost effectively by reducing infrastructure costs, development time and hardware uncertainty. The EnAccess team are committed to open source innovation, and run the [AirLink server](../AirLink%20Server.md) for the same reason. By requesting your own tenancy on the server, you can start prototyping your custom app immediately! With in-built PAYGO functionality, AirLink takes the most complex and non-differentiating pieces out of the equation and lets you focus on your differentiating development. If your idea requires PAYGO devices *without data connectivity*, do also check out the [OpenPAYGO Token](https://enaccess.org/materials/openpaygotoken/).

## Idea -> differentiating development, quickly

AirLink allows you to focus on what is unique to your business idea by abstracting away the complexity of setting up an IoT device-gateway-server connection. If the smartphone-centric use case is what you need, you can dive into your differentiating development while awaiting prototype devices from a manufacturer of your choice. After trying out the initial demo, follow this playlist to get your AirLink tenancy setup:

### [4 steps to full AirLink functionality](https://www.youtube.com/playlist?list=PLzs9gB3KSMw_u0zuKGCKE0x2EER0s6ONP)

In short, you will first setup your own server tenant (you don't have to run the server, EnAccess does this for you), then connect the open source AirLink App to the server tenant using your credentials, then provision a device using the Gateway App, perform data sychronization, and finally generate a Pay as you go token for the AirLink device.

Then, focus on your *differentiating* development:

1. Fork the Flutter code from the [AirLink Gateway app](https://github.com/EnAccess/Airlink-App/tree/main/airlink_flutter) and start developing.
2. Download the [AirLink Device demo app](https://github.com/EnAccess/AirLink-Devices) APK, so that you can use a phone as a representative device. If it helps, modify the simple Android-native Java source-code to add more 'device' functionality to the device demo app.
3. Provide the [AirLink Devices](../AirLink%20Devices.md) spec and the [Nordic nRF firmware codebase](https://www.nordicsemi.com/Products/Bluetooth-Low-Energy) as a reference to any hardware manufacturer capable of making a Bluetooth® device to your specifications.
4. Use the [Swagger documentation](https://airlink.enaccess.org/swagger-ui.html) for API access to the AirLink server and read the [Thingsboard PE documentation](https://thingsboard.io/docs/pe/) as you develop complex customer-device functionality using Thingsboard.io's full Pro version!

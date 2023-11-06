# A Device Manufacturer developing devices to be used in remote-region IoT data collection or PAYGO-financed use

## Why

AirLink saves manufacturers from the hassle of building out a custom IoT software backend for their hardware devices, and the open source format makes it likely that several adopters with different software stacks for business management can adopt AirLink devices. *This clear separation of the hardware and software stacks using the most commonly adopted ad-hoc wireless communication standard, Bluetooth®, is a key benefit of AirLink.* If your idea requires PAYGO devices *without* data connectivity, do also check out the [OpenPAYGO Token](https://enaccess.org/materials/openpaygotoken/).

## Out of the box

AirLink gives you open source code for:

1. Smartphone App to manage devices and connect them to the Data or PAYGO service
2. Tenancy on a data server with 3 types of PAYGO available, run by EnAccess
3. Device firmware for Nordic Devices

With these three components, AirLink gives you a jump-start on your IoT or PAYGO project: it can synchronize data from AirLink-compatible devices to the IoT server hosted by EnAccess without any more development. To try AirLink, simply download two APK files and use one phone as a mock device with another acting as a gateway to transfer data to the Demo server. See the steps to do a quick trial [here](../Quick-start%20guide.md#Trying-out-AirLink-is-easy)

Adoption is also simplified, with open source code for the gateway app as well as Bluetooth firmware. For server infrastructure, all you need is tenancy on EnAccess's server, requested by an email. Once you have tenancy, configuring your tenant to support AirLink takes a few easy steps detailed in this video:
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

After configuring the server, you can focus on device development.

## Making your Devices compatible with AirLink

Compatibility takes four simple steps focused on Advertisement and Data format, and optionally on authentication.

1. Customize the Advertisement packet to match AirLink spec, as mentioned in the [AirLink Devices](../AirLink%20Devices.md) page. The easiest way to do this is to fork the open source [Nordic nRF firmware codebase](https://www.nordicsemi.com/Products/Bluetooth-Low-Energy).
2. Group similar properties e.g. tempC, maxTemp. Create a [CBOR array](https://cbor.me) with these properties. These will be transferred once the app connects to the device. Collapsing several individual properties into one CBOR Array has the added benefit of making the data transfer memory efficient and fast.
3. Name the Bluetooth® *descriptor* with the property name e.g. 'temp'. Then, AirLink will understand your properties as temp_tempC, temp_maxTemp etc and on successful sync you will find these properties in the timeseries data for that device on the server. Device configurations are also saved similarly in dcfg_* properties.
4. Optional: Build an access control flow in your devices which relies on a Server Access Token "password" unique to the device, starting with a pre-programmed value which is entered into to the firmware. Then, your device will only allow data transfer from/to a particular app which knows the default access token - and once provisioned on the server, will receive an access token *unique* to it. All device data access control will then be locked to phones that can access this unique device token from the server, based on the Role-Based Access Control functions available on the server.

## Supplying AirLink Devices to your customers

There are three main options to having distributors or end users adopt your AirLink devices.

1. Get tenancy on the [AirLink Server](../AirLink%20Server.md) and manage devices yourself, using API capabilities to interface with the software stack of the adopter. Upload devices using [CSV upload](Quick-start%20guide.md#How-to-get-started-with-your-own-AirLink-deployment) to get them ready for the adopter's AirLink App. Alternatively, you can use the App out of the box to provision your devices yourself:
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
2. Get tenancy on the [AirLink Server](../AirLink%20Server.md) and use the built-in Angaza or Solaris integration to make your devices connect with one of those software stack, using credentials supplied by Angaza or Solaris. This means any adopter using those software stacks can use your devices, only requirement being obtaining manufacturer and/or distributor API credentials from Angaza or Solaris.
3. Send your devices to the distributor or end user with only the default access token programmed, and the distributor can then associate them with their own version of the AirLink App and their own server tenancy

For each of the cases, the only input required to the devices after [Compatibility](#making-your-devices-compatible-with-airlink) is programming the default access token. Similarly, the only step required to move devices between distributors e.g. reselling stock is to change the default access token to the one supported by the other adopter. The devices themselves are separate from any custom functionality developed in the AirLink app for each distributor/user/adopter so the AirLink Bluetooth® protocol effectively acts to insulate the devices from software stack changes.

!!! info "Bluetooth® SIG registration"
    If your customer will be selling the devices without changing the product name or incorporating into another product, you might need to register with the Bluetooth® SIG at your cost (or negotiate with a distributor). You only have to do this once for all your products that depend on a single Bluetooth® IC e.g. nRF81822, or the Laird BL653 etc. More details are on the [AirLink Devices](../AirLink%20Devices.md) page.

# A Device Manufacturer developing devices to be used in remote-region IoT data collection or PAYGO-financed use

## Why

AirLink saves manufacturers from the hassle of building out a custom IoT software backend for their hardware devices, and the open source format makes it likely that several adopters with different software stacks for business management can adopt AirLink devices. *This clear separation of the hardware and software stacks using the most commonly adopted ad-hoc wireless communication standard, Bluetooth®, is a key benefit of AirLink.* If your idea requires PAYGO devices *without* data connectivity, do also check out the [OpenPAYGO Token](https://enaccess.org/materials/openpaygotoken/).

## Making your Devices compatible with AirLink

Compatibility takes four simple steps focused on Advertisement and Data format, and optionally on authentication.

1. Customize the Advertisement packet to match AirLink spec, as mentioned in the [AirLink Devices](AirLink%20Devices.md) page. The easiest way to do this is to fork the open source [Nordic nRF firmware codebase](https://www.nordicsemi.com/Products/Bluetooth-Low-Energy).
2. Group similar properties e.g. tempC, maxTemp. Create a [CBOR array](https://cbor.me) with these properties. These will be transferred once the app connects to the device. Collapsing several individual properties into one CBOR Array has the added benefit of making the data transfer memory efficient and fast.
3. Name the Bluetooth® *descriptor* with the property name e.g. 'temp'. Then, AirLink will understand your properties as temp_tempC, temp_maxTemp etc and on successful sync you will find these properties in the timeseries data for that device on the server. Device configurations are also saved similarly in dcfg_* properties.
4. Optional: Build an [access control flow](https://youtu.be/2zY5vETH4zk) in your devices which relies on a Server Access Token "password" unique to the device, starting with a pre-programmed value which is entered into to the firmware. Then, your device will only allow data transfer from/to a particular app which knows the default access token - and once provisioned on the server, will receive an access token *unique* to it. All device data access control will then be locked to phones that can access this unique device token from the server, based on the Role-Based Access Control functions available on the server.

## Supplying AirLink Devices

There are three main options to having distributors or end users adopt your AirLink devices.

1. Get tenancy on the [AirLink Server](AirLink%20Server.md) and manage devices yourself, using API capabilities to interface with the software stack of the adopter. Upload devices using [CSV upload](Quick-start%20guide.md) to get them ready for the adopter's AirLink App.
2. Get tenancy on the [AirLink Server](AirLink%20Server.md) and use the built-in Angaza or Solaris integration to make your devices connect with one of those software stack, using credentials supplied by Angaza or Solaris. This means any adopter using those software stacks can use your devices, only requirement being obtaining manufacturer and/or distributor API credentials from Angaza or Solaris.
3. Send your devices to the distributor or end user with only the default access token programmed, and the distributor can then associate them with their own version of the AirLink App and their own server tenancy

For each of the cases, the only input required to the devices after [Compatibility](#making-your-devices-compatible-with-airlink) is programming the default access token. Similarly, the only step required to move devices between distributors e.g. reselling stock is to change the default access token to the one supported by the other adopter. The devices themselves are separate from any custom functionality developed in the AirLink app for each distributor/user/adopter so the AirLink Bluetooth® protocol effectively acts to insulate the devices from software stack changes.

!!! info "Bluetooth® SIG registration"
    If your customer will be selling the devices without changing the product name or incorporating into another product, you might need to register with the Bluetooth® SIG at your cost (or negotiate with a distributor). You only have to do this once for all your products that depend on a single Bluetooth® IC e.g. nRF81822, or the Laird BL653 etc. More details are on the [AirLink Devices](AirLink%20Devices.md) page.

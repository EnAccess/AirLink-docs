<!-- markdownlint-disable-next-line first-line-h1 -->
<p align="center">
  <a href="https://github.com/EnAccess/AirLink-Server">
    <img
      src="https://enaccess.org/wp-content/uploads/2023/04/Airlink-Graphics-GitHub-2240-%C3%97-800-.svg"
      alt="AirLink-Server"
      width="640"
    >
  </a>
</p>
<p align="center">
  <em>AirLink uses financed phones as relay-extensions of the internet in remote areas, to extend productive asset data coverage in even the most rural communities. By introducing open-standards communications, AirLink allows customers’ phones and PAYGo assets to communicate with each other by using widely available, standard low-energy Bluetooth connectivity.</em>
</p>
<p align="center">
  <img
      alt="Project Status"
      src="https://img.shields.io/badge/Project%20Status-stable-green"
  >
  <a href="https://github.com/EnAccess/AirLink-Server/blob/main/LICENSE" target="_blank">
    <img
      alt="License"
      src="https://img.shields.io/github/license/EnAccess/AirLink-Server"
    >
  </a>
</p>

---

This is **technical documentation** for AirLink. If you are looking for an overview of the AirLink project, see this:

- [:octicons-arrow-right-24: AirLink project page @EnAccess](https://enaccess.org/airlink/)

---

## Use cases

*For all potential use cases, EnAccess hosts the IoT server for free so that you can try your idea quickly and cost effectively!* [🏁 Quick-start guide](Quick-start guide.md)

How to use AirLink in some common uses:

### [:material-factory: A Device Manufacturer developing devices to be used in remote-region IoT data collection or PAYGO-financed use](Use%20Case%20-%20Device%20Manufacturer.md)

### [:clipboard: An NGO wanting to define a adaptable hardware/software standard for data collection in your projects or grantees](Use%20Case%20-%20Paygo%20Entrepreneur.md)

### [:material-lightbulb-on: A Fintech/PAYGO entrepreneur focused on innovative software, needing a standard hardware spec to share with a device manufacturer](Use%20Case%20-%20Device%20Manufacturer.md)

---

## AirLink components

![AirLink Components](AirLink_Components.png)

### :material-radio: **AirLink devices** ([Nordic nRF](https://www.nordicsemi.com/Products/Bluetooth-Low-Energy) firmware)

  [:octicons-arrow-right-24: AirLink devices documentation](AirLink Devices.md)

  [:octicons-mark-github-16: AirLink devices on Github](https://github.com/EnAccess/AirLink-Devices)

### :octicons-device-mobile-16: **AirLink App** ([Flutter](https://flutter.dev/) app)

  [:octicons-arrow-right-24: AirLink App documentation](AirLink App.md)

  [:octicons-mark-github-16: AirLink App on Github](https://github.com/EnAccess/AirLink-App)

### :material-server: **AirLink Server** ([Thingsboard](https://thingsboard.io/) server configuration)

  [:octicons-arrow-right-24: AirLink Server documentation](AirLink Server.md)

  [:octicons-mark-github-16: AirLink Server on Github](https://github.com/EnAccess/AirLink-Server)

---

## Key ideas built into AirLink

### BLE-GSM Data transfer

![AirLink Data transfer flow](Simusolar_Architecture_Diagram_-_IoT_Data_Flow.png)

### IoT Device Lifecycle

![Device Lifecycle](IoT_Communications_and_Components_spec_-_App_Architecture.png)

### App-driven, Crowdsourced locatability

![AirLink unknown device flow](AirLink_Unknown_Device_Flow.png)

### PAYGO control

[3-types of AirLink PAYGO](Connecting%20to%20Solaris%20or%20Angaza.md)

---

## Related resources

- [CBOR](http://cbor.io/): Memory-efficient JSON-like data format
- [OCF](https://openconnectivity.org/developer/specifications/): Data structure standard to represent IoT devices

- [Nexus Channel](https://angaza.github.io/nexus-channel-models/resource_type_spec.html): Angaza's Inter-operability initiative
- [OpenPAYGO Link](https://github.com/EnAccess/OpenPAYGO-Link/tree/main/Documentation): Wired inter-operability from Solaris/EnAccess
- [OpenPAYGO Metrics](https://github.com/openpaygo/metrics): GSM inter-operability from Solaris
- [OpenPAYGO Token](https://github.com/EnAccess/OpenPAYGO-Token): Open Source PAYGO token reference design from Solaris/EnAccess

---

![Simusolar Inc](Simusolar_logo.png)

AirLink was developed by [Simusolar Inc](https://www.simusolar.com/) with support from [EnAccess](https://enaccess.org).

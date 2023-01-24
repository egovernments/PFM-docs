# Bluetooth Thermal Printer Integration

Portable Bluetooth thermal printers are used to generate the mini receipts.

### Dependencies  <a href="#dependencies" id="dependencies"></a>

`bluetooth_thermal_printer`

`js`

![](../../../../.gitbook/assets/image-20220210-083823.png)

### Printing Receipts via Bluetooth Thermal Printer  <a href="#printing-receipts-via-bluetooth-thermal-printer" id="printing-receipts-via-bluetooth-thermal-printer"></a>

* Enable the Bluetooth in the respective mobile device.
* Switch the thermal printer.
* Tap on the Print button from the respective screen if the printer device is connected already it will print the receipt directly or else it will show a dialogue with a list of Bluetooth devices, from their user need to a selected respective thermal printer, once the device is paired successfully it will generate a receipt in the printer.

### Helper Methods <a href="#helper-methods" id="helper-methods"></a>

*   `printTicket` → Used to write the bytes to the thermal printer if the device is connected otherwise it will show paired Bluetooth devices in a dialogue.

    Required Arguments → bytes, context
* `getTicket` → Used to generate the bytes from Image and also sets the paper size.\
  Required Arguments → Image
* `showMyDialog` → Used to show the Paired Bluetooth devices\
  Required Arguments → bytes, context
* `setConnect` → If the device is already connected it will generate the receipt or else it will show the paired devices to connect.

### **Files Path**

[<img src="https://github.com/fluidicon.png" alt="" data-size="line">punjab-mgramseva/common\_printer.dart at master · misdwss/punjab-mgramseva](https://github.com/misdwss/punjab-mgramseva/blob/master/frontend/mgramseva/lib/utils/common\_printer.dart)

[<img src="https://github.com/fluidicon.png" alt="" data-size="line">punjab-mgramseva/index.html at master · misdwss/punjab-mgramseva](https://github.com/misdwss/punjab-mgramseva/blob/master/frontend/mgramseva/web/index.html)



> [![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)_​_](http://creativecommons.org/licenses/by/4.0/)_All content on this page by_ [_eGov Foundation_](https://egov.org.in/) _is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._

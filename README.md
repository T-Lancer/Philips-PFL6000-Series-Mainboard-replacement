# Philips-PFL6000-Series-Mainboard-replacement
This repository shall document my process of reusing old TV LCD Panels with generic universal LVDS controllers. In this instance the testbed is a 47PFL6057K/12 3D TV
# Background
I own multiple Philips Ambilight PFL6000 series TVs (37 to 55" for, office, basement, guest and bedroom). Mostly obtained for free due to defective mainboards or cheap for parts due to broken Panels and then salvaged for working mainboards.  In some cases, the mainboard could be fixed by careful reflow of the CPU.

see this blog by Alpengeist for information about the process or repairing the Fusion CPUs: https://alpengeist-tvrepair.blogspot.com/2020/06/all-i-know-about-philips-qfu-mainboard.html

After also improving the cooling of the CPUs by cutting a whole in the back of the TV and attaching a large passive aluminium heatsink, as well as de-lidding the CPUs IHS, the TVs have worked for a number of years without issue. Unfortunately, years of pre-stressing due to the poor thermal design has led to some of these TV are failing again with the known 2-Blink error. This indicates a problem with the Fusion CPU unable to boot.  As the panels are perfectly intact, it seems such a waste to dispose of these TVs.

In the past I have reused laptop panels with generic LVDS controllers with great success, sometimes even normal 24" LCD Monitors.  Though TVs seemed to always be excluded from this possibility as I could never find much information about others reusing the panels despite the panels being documented online with datasheets.  The main limiting factor may have been that the generic LVDS controllers often only supported up to 2 channel 8bit LVDS interfaces.  The panel used in the Philips PFL6000 Series (in my case the LC470EUF FE P1) uses 4 channel LVDS with 8 or 10bit resolution. Though this may only be due to the fact this is a 3D panel, so it needs to display two images, hence double the bandwidth.  Either way, I was determined to keep these TVs, as I have 4 of them and they will probably all fail eventually.  Despite the TVs being over 10 years old, they are still nice TVs with Ambilight Aswell.

#Proof of concept

Another reason I am determined to reuse these TVs is the fact that full schematics and service manuals are available online. Making reverse engineering extremely easy.  Every component is documented in every variant of the TV. from 32 to 55 inches including other intermediate configurations that included Zigbee RF receivers for use with a special Philips keyboard as well as webcams (for smart TV features, not that I have these variants, but it is nice to see how it worked). PSU, Mainboard, IR board, Ambilight strip schematics are all available to inspect. this making finding interfaces and pinouts much easier.

My first task was to find an LVDS controller that supports 4 channel LVDS.  Since the introduction of 2K and 4K LCDs, this problem seems to have been solved.  4 channel controllers are now as cheap as older 2 channel controllers.  these are often marketed as DIY e-sports controllers with low latency.  No Idea if this really does any better than OEM controllers, but there you go.  After getting in touch with some sellers, they agreed to configure the driver for the LCD panel in question.  While these LVDS controller also include an LED backlight driver, I would not actually need to use it.  All the sellers really need to know is the resolution, channel width and bit depth as well as panel voltage and refresh rate.  The LC470EUF FE P1 has the following specifications that are important:

* 1920x1080
* 4 Channel LVDS
* 8 or 10 bit (selectable on TCON board)
* 12V supply
* 120Hz (in 3D mode this would be 2x 60Hz signals presumably)

After receiving the driver board, I proceeded with my first test of gutting the TV and testing the driver board.  The TCON board uses the standard 92pin connector scheme (41 and 51 pin connectors). An additional wire needed to be pinned to the connector to select 8bit mode, as the drivers only support 8bit mode. Getting the TV to turn on is also trivial, as the service manual specifies the signals from the PSU.  After bridging standby and BL-ON to ground and 12V, the TV turned on and powers the backlight.  Next step was then to plug in the controller and power it from the PSU's own 12V supply which also turns on automatically once the standby pin is grounded.
To my delight, the panel immediately displayed the controllers No-Signal test image consisting of a full screen RGB loop.  Attaching my laptop proved this project will work as I could display my laptops screen without a problem on the TV with no obvious signs of artifacts with the screen; signal, or colour.  Further images tests are still needed, but experience with these controllers tell me that they will work perfectly fine. Obvisuly I will not have 3D features, nor Smart TV features. but these are features I have never used on these TVs, nor intend to use ever on a TV.  I have HTPCs and Chromecasts for smart features.  All I need is a screen to display content.

The driver board I have used in this test can be found on Ali Express

https://de.aliexpress.com/item/1005004570698943.html

For another project involving a 2K 27" Lenovo LCD I ordered this driver

https://de.aliexpress.com/item/1005008067664306.html

In both cases one specifies the panel to the seller and they will check if it is compatible and program the firmware with the needed configuration.

Despite the images showing different PCBs the one I received for the Philips TV is identical to the one I previously received for the Lenovo screen.  So just keep that in mind if you order a driver board yourself.

Service manual:
https://elektrotanya.com/philips_chassis_qfu2.1e_la.pdf/download.html

this also includes advanced error code list. Bridge the SDM Testpoint to ground and turn on the power to enable this mode.  If there is an error it will provide the advanced error code via the front LED.

LCD Panel datasheet:
https://datasheet4u.com/datasheets/LG/LC470EUF-FEP1/906135

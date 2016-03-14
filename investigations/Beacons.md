**Introduction**

As part of Connected Devices IOT research I have been learning about Beacons and I'd like to share some of what I've learned. I'm just learning myself so this is by no means a detailed or expert source of information, however it will provide a high-level overview and perhaps it will peak your interest in the subject.

**What is a Beacon?**

The Beacons I am referencing here are BLE (Bluetooth Low Energy) Beacons which are small devices that broadcast tiny bits of information into the surrounding world.

**How Beacons are Used**

Beacons are all about expanding the internet to the objects around us, making it easier to learn information and interact with our surroundings based on our current physical location. For example, you see a movie poster and want to quickly find and watch the trailer. Or you're walking by a shop and want to easily see if there are any sales that interest you. Maybe you find a lost puppy and want to be able to learn where it lives and contact it's residence fast. Maybe you're at a restaurant and want to check out the menu before you go inside. With smart devices and the 'internet of things' expanding all around us, there are potentially endless use cases.

**Some Projects that use Beacons**

Currently there are a couple of major players working on initiatives that use BLE Beacons: Apple's 'iBeacon', and Google's open-source project called 'The Physical Web'. For my purposes I researched more about the open-source Physical Web project.

**Beacons and The Physical Web**

The general idea of the Physical Web is to extend the internet so that one can interact with physical objects around them. Beacons broadcast URLs that are location-sensitive in that the URL will point to a web site that is relevant to the beacon's physical location or purpose. Clients run on mobile phones and scan the area around their current location and discover messages advertised on nearby beacons.

Beacons are very limited in the size of data which they can broadcast, so for the Physical Web they're restricted to a URL. Upon discovery of a beacon and corresponding URL, the mobile client can connect to the Physical Web server and retrieve more metadata or attachments related to the URL which was broadcast. This also makes it easy to update the content associated with a beacon by just updating the corresponding beacon attachment in the server, and not having to update the physical beacon itself (unless changing the actual URL).

If a beacon is embedded inside a smart device, once discovered by a mobile client, the client could even ultimately connect to and interact with the smart device itself via the server, if the device itself is internet enabled. One example that Google notes is discovering a beacon that is inside a parking meter; then using your mobile phone to pay for parking, and the parking meter is updated accordingly.

Google offers open-source Physical Web client apps for both ios and android (links below). You can develop your own mobile client using the Bluetooth BLE, Google Developers Nearby, and Eddystone Protocol APIs.

**How Beacons Work**

BLE beacons use bluetooth (obviously hah) to broadcast a tiny bit of information around them. They just use the bluetooth 'advertising' packet so that mobile devices don't have to actually pair with the beacon itself. A beacon broadcasts the advertising message in a special format according to the beacon protocol being used. 

For iBeacons, they have their own iBeacon protocol. For The Physical Web, Google has developed an open-source beacon protocol called Eddystone.

Beacons that support the Eddystone protocol broadcast a URL using the 'Eddystone-URL' frame type. The URL itself is encoded so that it can be extremely short (since there is a limited number of bytes that can be broadcast) and the URL is decoded on the mobile client. For example, 'http://www.' may be encoded down to one special single character.

**Beacon Health**

Eddystone beacons also broadcast a special frame type called 'Eddystone-TLM' that contains beacon telemetry data. This data includes battery info, beacon device temperature, broadcast duration etc. which can be used to analyze and report the general health of the beacons. Dashboards can be built that monitor the beacons and warn when they are not working correctly or run out of battery power, etc.

**Configuring Beacons**

How beacons are configured depends on the manufacturer. Most of them that I have seen provide cloud tools or apps that allow you to connect to the beacon and configure it. Generally you can configure the following options on a beacon:

- Broadcast protocol (i.e. Eddystone, iBeacon)

- A beacon name

- Location description or other location-based metadata

- The URL/message being advertised
 
 - Transmission power (i.e. broadcast range); obviously a further range will use more beacon power. Beacon range depends on the type of beacon (USB or stand-alone), the manufacturer, and the physical environment where the beacon is placed; but I've seen some advertised online as having a range of up to 75 metres

 - Broadcast speed (i.e. the faster the broadcast rate the faster a beacon client can read the packets and discover it; however a faster broadcast rate also requires more beacon power

 - How many telemetry frames are broadcast vs actual message frames

 For example, [BlueCats Beacons](http://bluecats.com/) have cloud tools that can be accessed via a web browser or mobile app. Their web portal doesn't connect directly to the beacon itself; however their mobile phone app does via the device's bluetooth; therefore any configuration settings made via the web are not applied to the beacon until the beacon is connected to the mobile phone app. Or beacons can be configured directly from the mobile app itself. BlueCats also offers their own SDK.

 The BlueCats ios and android apps include a sniffer that allows your mobile phone to discover the beacons around you, and then connect and configure the ones that you own or have permissions for. The BlueCats beacon configuration tools are very impressive and extensive, and allow you to configure and categorize your BlueCat beacons in a variety of different ways.

 I have seen some online beacon manufacturers and cloud services that offer full beacon configuration and setup online at the time of purchase, so that on arrival your beacons are ready to go right out of the box. I could see this being a great option, for example, for a small business that wants to use beacons to advertise but doesn't necessarily have the expertise or time to configure the beacons themselves.

 **Beacon Manufacturers and Cost**

 There are a variety of manufacturers of BLE Beacons around the world. There are USB beacons which are super tiny, and connect to a USB port in order to power them (they can be connected to an AC power USB port instead of a computer). There are stand-alone beacons which are larger and have their own power source ranging from watch-like batteries to several AA batteries. Depending on the manufacturer and model, beacons can have a battery life ranging from a few months to several years. For a list of popular beacon manufacturers see the resources section below.

 To work with the Physical Web, be sure to purchase beacons that support the Eddystone protocol and have the supporting configuration tools. Several of the beacons that I saw online support broadcasting both the iBeacon and Eddystone protocols, but some only support one or the other.

 Cost-wise this greatly varies depending on manufacturer. Beacons manufactured in Asia tend to be cheaper. Also USB beacons tend to cost a bit less than stand-alone beacons but are not as convenient to be placed since they require USB power, and generally have a smaller transmission range. 

 I've seen some manufacturers require a 3-unit minimum when ordering their beacons, and also some provide discounts when beacons are ordered in large quantities. Some manufacturers offer beacon 'starter packs' which include a few beacons as well as access to their online cloud software. For pricing it's best to go online and have a look as it is a very wide range. The beacons that I tried out ([BlueCat AA Beacon](http://store.bluecats.com/collections/featured-products/products/aa-beacon-3)) cost $29 USD each with a 3-beacon minimum, at least at the time of writing this. 

 **Further Resources**

 I hope that was interesting and helpful. Here are some useful links that can provide you with much more detailed information about beacons and The Physical Web!

 - [iBeacon](https://en.wikipedia.org/wiki/IBeacon) on Wikipedia

 - Apple's [iBeacon Developer](https://developer.apple.com/ibeacon/) resources page

 - The [Physical Web](https://google.github.io/physical-web/) home page

 - [Google Developers: Beacons](https://developers.google.com/beacons/) home page

 - Google Developers: [Getting Started with Beacons](https://developers.google.com/beacons/get-started)

 -  Google Developers: Beacons [Platform Overview](https://developers.google.com/beacons/overview)

 - The Physical Web [github repository](https://github.com/google/physical-web)

 - The Physical Web [technical overview](https://github.com/google/physical-web/blob/master/documentation/technical_overview.md)

 - The Eddystone protocol [github repository](https://github.com/google/eddystone)

 - Google Developers: [Nearby API](https://developers.google.com/nearby/)

 - Google Developers: [Proximity Beacon API](https://developers.google.com/beacons/proximity/guides)

 - The [Physical Web Cookbook](http://google.github.io/physical-web/cookbook/)

 - YouTube: [Introduction to the Physical Web](https://youtu.be/w0XazPrh7r0) (Ubiquity Dev Summit 2016)

 - Although perhaps a bit outdated now, a [List of the 9 biggest Beacon Manufacturers](http://www.nodesagency.com/list-9-biggest-beacon-manufacturers/)

 - The Physical Web open-source [android app source](https://github.com/google/physical-web/tree/master/android) and the [ios app source](https://github.com/google/physical-web/tree/master/ios)

 - The Physical Web [demo app](https://play.google.com/store/apps/details?id=physical_web.org.physicalweb) on the Google Play Store

 - Node.js Eddystone [Beacon Scanner](https://github.com/sandeepmistry/node-eddystone-beacon-scanner)

 - [BlueCats](http://bluecats.com/) home page

 - BlueCats [Beacons](http://bluecats.com/beacons.html) and [Developer Resources](http://bluecats.com/developers.html)

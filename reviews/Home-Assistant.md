**Home Assistant**

As part of our IOT research I tried out [Home Assistant](https://home-assistant.io/). Home Assistant is an open-source home automation platform that allows you to control and monitor all of your home IOT devices in one central location. Home Assistant supports a wide range of IOT devices from different manufactures. The open-source community adds support for the various IOT devices.

The actual setup and configuration of the IOT devices themselves is kept independent of Home Assistant, in that once the devices are setup then they can be plugged into the platform. The platform supports a bunch of different protocols so that it can talk to the various devices. Some devices can be auto-detected 'out of the box'. Automation rules can also be created to control the IOT devices, for example turn on a light at sunset.

The platform is built on Python 3. The source code can be found [here on Github](https://github.com/balloob/home-assistant). Check out the [Home Assistant Demo page](https://home-assistant.io/demo/) for a cool example of what the dashboard can look like.

**Setup**

It only took me about 45 minutes total, to: Have a local instance of Home Assistant up and running, with my Arduino uno board attached; with raw light and temperature sensor data appearing on the dashboard; and a light control switch for my Arduino LED working on the Home Assistant dashboard.

After that I tried hooking up a WeMo wifi power outlet, that was supposed to be auto-detected; it failed to be found when I started up Home Assistant. However it turns out this was because my Ubuntu VM was using ""NAT"" for the network adaptor setup; once I switched my VM network to use ""bridged"", then it found the WeMo right away. Then I was able to turn a lamp at my desk on/off remotely via a switch on the Home Assistant dashboard. If I wasn't using a VM or had the correct VM network setup, it would have literally taken just minutes to add the WeMo power switch to the dashboard and use it.

Steps to setup on my Ubuntu 14.04 VM:

- If you don't have it, install Python 3 (I used a virtual env)

- Install the platform (simple ubuntu shell commands)

- Edit the config file to add your IOT devices and a password

- Ensure your IOT devices are online

- Start the server (in an ubuntu shell: hass --open-ui)

- Browse to http://localhost:8123, login, and it's ready to use

**Usage**

Once it was all setup it was easy to use. Just browse to the dashboard on your browser (localhost) and on the dashboard you can see the status of your IOT devices and control them. I could see my Arduino board sensor data displayed, and I could also use the mouse to turn the WeMo power switch (and attached desk lamp) on and off.

I just setup Home Assistant to run on my local WiFi network. However it can be figured to be accessible from anywhere on the internet (i.e. open a port on your router) but I didn't try that out.

**Issues**

Generally the dashboard worked great with my WeMo power switch. Only once I did notice that it got confused with the power switch state; it thought the switch/light was on when in reality it was off; and then when I clicked the switch it turned on the light but indicated that it was off. I had to restart the server to fix the issue.

**Summary**

Very easy to setup and a really cool dashboard. I really liked it and if I was setting up a bunch of IOT devices in my home I would seriously consider using this platform.

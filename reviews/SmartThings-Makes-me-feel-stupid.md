This is the second installment of setting up my SmartThings to [do the scenarios described here](https://github.com/mozilla/connected-devices-experiments/issues/1).

Feel free to comment - especially if you've also purchased anything in the SmartThings family!

++++++++++++++++++++

### Hub setup 
<img src="https://cloud.githubusercontent.com/assets/234670/13186852/eff1455a-d6fc-11e5-8429-4459cc3b1960.png" height="300" >

Start by setting up the hub. It needs to plug into my router. Fine, but the cord is super short -- it's maybe 3 feet. Spend 15 minutes reorganizing my desk area where the router lives so that I can position the hub in a place that works and isn't in the way of other desk things that are already there.

The instructions ask you to download the SmartThings app, which then walks you through setting up an account and setting up the hub. **The hub setup screens are the best part of the SmartThings app; they did a nice job here.**

++++++++++++++++++++

### Motion Sensor setup
Next I open and pair one motion sensor - 5 minutes. I can see in the SmartThings app that motion is being detected - cool! Discovered that the motion sensor registers temperature -- didn't know that. 

++++++++++++++++++++

### Smart Outlet setup
Then start setting up the outlet for the kitchen lights. I want to be able to wave my hand over the motion sensor in my bedroom to trigger the kitchen lights to go on.

Pairing the outlet for the kitchen was easy and took just a few minutes. I did take me a while to figure out the logic of how this worked with my kitchen lights. The manual light switch needs to be in the "on" position in order for the outlet to control it, so that when I set the outlet to "on" with the SmartThings app, the kitchen lights go on. 

I'm in my kitchen all the time using this light, and I don't want to have to use the SmartThings app all the time to do that. So it's good that I can still use the manual light switch to turn on/off. 

But...I can see that it would be easy for me to forget to set this correctly before going to bed. That is, before going to bed, I need to make sure the manual light switch is in the "on" position and that the SmartThings outlet is set to "off." I can probably automate the SmartThings outlet to turn off a certain time in the evening, but I'll need to remember to leave the manual switch in the "on" position. 

> Sidebar: This kind of setup is prone to "user error," e.g., a family member accidentally turns the manual switch "off" in the evening, and everybody's pissed in the morning when the lights don't come on as expected.

++++++++++++++++++++

### Mashing it up
Now to connect the motion sensor to the outlet. SmartThings has some built-in "routines" like _Good Morning_ and _Good Night_. The _Good Morning_ routine seems a good place to start. 

<img src="https://cloud.githubusercontent.com/assets/234670/13186918/2fb91d48-d6fd-11e5-917b-76b28b16220f.PNG" height="300">

The hit area for the settings gear is far too small. I keep missing it and pressing the larger hit area that triggers the routine to start. Super irritating. Finally get into the routine settings.

> Incredibly annoying: Every selection in the SmartThings app triggers the spinner while the app “thinks about” something. My sense is that I’m "wasting a lot of time" in this app. They should fix this, as most of the actions are navigation and should not require the system to do any thinking.

<img src="https://cloud.githubusercontent.com/assets/234670/13186996/96a754fc-d6fd-11e5-8d3b-fa581152adc2.PNG" height="300">

Select _Kitchen Outlet 1_ under _Turn on these lights or switches_. 

<img src="https://cloud.githubusercontent.com/assets/234670/13187078/f9cbdca6-d6fd-11e5-9892-17137bae4e92.PNG" height="300">

Now what? Further down the screen is a section called _Automatically perform "Good Morning."_ This phrase does not include the words _when_ or _if_, so I don’t immediately make the connection that this section is how I trigger this routine. Tap it anyway. 

<img src="https://cloud.githubusercontent.com/assets/234670/13187086/0dbac150-d6fe-11e5-8e23-928c2b455841.PNG" height="300">

Go through a few screens to select the _Bedroom Motion 1 sensor_.  Ugh the whole point of me using the motion sensor is so I don't have to set a schedule -- I keep odd hours and don't always wake up at the same time, so I just want this routine to start whenever I wave my hand over the motion sensor, even if that time is 11pm. But SmartThings has decided that a timeframe is required in order to save this routine. Lame. Select 4am to noon. Save.

<img src="https://cloud.githubusercontent.com/assets/234670/13187278/21c4b614-d6ff-11e5-915a-904e7a5f34e6.PNG" height="300">

> Sidebar: After revisiting this screen 5 times, I realized that the _Automatically perform “Good Morning”_ phrase now includes the word _when_. This is just silly. The phrase should not change in this barely noticeable (but very important) way. It should always say _Automatically perform “Good Morning” when_  so that it helps people understand what they’re doing.

<img src="https://cloud.githubusercontent.com/assets/234670/13187722/b3823692-d701-11e5-8de1-cdd6c9ab9c7e.PNG" height="300">

Go into bedroom and wave hand over motion sensor. Nothing happens to the lights, though the app tells me that motion is being detected. Double-check the routine, which requires going deep into screens, each time watching the annoying spinner. Everything looks ok. Try it again. Doesn't work.

Argh, time to start over. Unplug the outlet and re-pair it. Delete the routine. Create a new routine, call it “Good Morning” and do all the steps over. Test it out. Now it works! 

At first this feels anti-climatic (see below for why). But then I test it a couple more times. Each time I feel a kind of glee when I see that lights "magically" turn on when I wave my hand over the sensor. That's cool, though likely a short-lived sense as I get used to this tech in my home.

> Sidebar: This is the kind of experience that makes people feel like they made a mistake in purchasing this system. Rather than making me feel empowered -- I’ve conquered my home! -- instead I don't know what happened, and I assume that I made a mistake somewhere setting up this incredibly simple routine. Yet I don't actually know what I did wrong, so I won't be able to avoid this "mistake" in the future. Doesn't inspire confidence in the system or in my ability to master it. 
**_Smart home systems should make me feel smart. Not stupid._**

In the next installment, I'll attempt to connect my coffee maker and my favorite jazz station to this routine so they turn on at the same time as the lights.

> Annoying: I hate the SmartThings app so much that I want to throw my phone across the room. Get rid of the spinner! It just draws attention to how much time I'm wasting in this app. Do something different and maybe even clever like tell me that "SmartThings is making shit happen for you!" Anything but the spinner. I say the spinner is lazy product design. [@uxDonaldTrump](https://twitter.com/uxDonaldTrump) would say it's "WEAK product design."


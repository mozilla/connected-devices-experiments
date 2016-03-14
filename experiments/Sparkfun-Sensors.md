**Introduction**

With the 'Internet of Things' taking off there are some cloud services out there that allow you to publish data from your various IOT devices. One such service is hosted by [SparkFun](https://data.sparkfun.com/), and I wanted to give it a try to see what the world of publishing sensor data is like.

**The SparkFun Cloud**

[SparkFun](https://data.sparkfun.com/) is a free sensor data publishing service that lets you create a data 'stream', name your stream, and define what type of data you will be publishing. It's cool as you don't have to create an account to use their publishing cloud; instead of requiring a sign-in you are provided with a stream public key and private key. You don't have to provide any personal information (you can even publish completely anonymously if you like).

Your data stream is allocated 50 MB maximum, and once you reach that limit it acts as a queue where the oldest sensor data records will be deleted as new ones are received. Any data that you do publish will be public, and it may be used by 'data scientists' around the world. However it appears that you do have full control over your own data, in that you can choose to clear out your data stream or delete it completely at any given time. There is a limit to how fast you can post data to your stream: a maximum of 100 data pushes in any given 15 minute window (approximately one post to your data stream every 9 seconds).

SparkFun also has an [online storefront](https://www.sparkfun.com/) where you can purchase IOT hacking equipment such as Arduino boards, Raspberry Pi's, sensor kits, their own branded hacking boards, and lots of other fun stuff. Note that the [data.sparkfun.com](https://data.sparkfun.com/) publishing cloud supports data posted from any platform not just from hardware purchased from the SparkFun store.

**My Data Experiment**

To try out sparkfun.data.com I decided to create a live data stream and post light sensor and temperature data from my office environment, using my Arduino Uno board and sensor shield. I am running an Ubuntu 14.04 VM on my MacBook.

**Step 1: Setup my Arduino Board**

As mentioned earlier I'm using an [Arduino Uno](https://www.arduino.cc/en/Main/ArduinoBoardUno) board with an attached Tinkerkit sensor shield, that I purchased as part of a [sensor starter kit](http://www.canadarobotix.com/microcontroller-kits/1701-carobot-tinkerkit-basic-starter-bundle).

![sparkfun1](https://cloud.githubusercontent.com/assets/2198968/13439630/64d9e364-dfbc-11e5-9633-31f8ebc5a6b4.jpg)
_Arduino Uno with Tinkerkit Sensor Shield_

I previously flashed my Arduino board with the Arduino 'Standard Firmata' firmware (to allow my board to run code and to talk to my VM, etc.) using the [Arduino IDE](https://www.arduino.cc/en/Main/Software). I won't go into [the details](https://www.arduino.cc/en/Guide/HomePage) as that is basically the standard way to setup an Arduino board before you start hacking with it.

After attaching the sensor shield to the Arduino board, I attached a photoresistor to the sensor shield input I0, a temperature sensor to the shield's input I1, and also a green LED to the shield's output O0.

![sparkfun2](https://cloud.githubusercontent.com/assets/2198968/13439649/788c14ae-dfbc-11e5-8fff-971dbd8b8d64.jpg)
_Arduino Tinkerkit sensor shield ports_

I just used a box to standup the sensors so that I could interact with the sensors easily. The green LED will be used just to indicate that sensor data is being received.

![sparkfun3](https://cloud.githubusercontent.com/assets/2198968/13439655/80827b3a-dfbc-11e5-99eb-975a70717f92.jpg)
_Tinkerkit LED, photoresistor, and temperature sensor_

**Step 2: Create a SparkFun Stream**

It was really easy to create a new SparkFun data stream and as I mentioned earlier the best part is no account creation/sign-in is required. To create the data stream I just browsed to [data.sparkfun.com](https://data.sparkfun.com/) and then clicked the 'Create' button to 'create a free data stream immediately'.

![sparkfuncreate](https://cloud.githubusercontent.com/assets/2198968/13439838/44b84ce6-dfbd-11e5-801d-018d58befc08.png)
_Create stream page on data.sparkfun.com_

Once on the create stream page, I just had to:

- Provide a name for my stream, this name is displayed publicly on your stream page as well as by default on the list of public streams. I named my stream 'Office environment'.

- Provide a stream description (this also appears publicly on your stream page). I used 'Light and temperature sensor data from the office in Toronto, ON' for my stream description.

- Your stream data is always public and can be viewed via your stream URL. By default streams will appear in SparkFun's [public stream list](https://data.sparkfun.com/streams/) which shows active streams ordered by those that have published new data most recently. If you select 'Hidden' for the 'Show in Public Stream List' option, then your data will still be public via the URL, however the stream URL won't be advertised on the public streams list.

- Specified the names of the fields for the data that will be published. These appear as column headings on the data stream page. I used 'light, temp_c' for my field names.

- Optionally specified a stream alias. This is really cool and allows you to have a custom URL for your data stream instead of just the cryptic stream ID. The resulting alias will be in the form of 'http://data.sparkfun.com/your_stream_alias'.

- Optionally specified tag(s) for your data stream, this just helps other people find your sensor data. I used 'light, temperature' for my stream tags.

- Specified a location, but don't put an exact address in case this value is used publicly. I just used 'Toronto, ON' for my stream location.

Then I clicked the 'Save' button and was good to go! The new stream was created and a new stream page displayed, that showed my new stream public key (which is a part of the stream URL), alias, private key and a delete key. These keys are required to publish to, clear, or delete your data stream (and there is an option to provide your email address so the keys are sent to you).

**Step 3: Write the Code**

With the Arduino board and sensors ready, and my SparkFun data stream created, next I had to write the code to grab the sensor data from the board and post it to the data stream.

I wanted to write the code in node.js, so I used a super cool framework called [Johnny-five](http://johnny-five.io/). Johnny-five is an open-source framework that lets you talk to your arduino board using node.js and the Arduino's 'StandardFirmata' firmware. The JS code runs on your local machine but connects to and interacts with the Arduino board via the board's firmware. With the [J5 API](http://johnny-five.io/api/) you can create objects to control your Arduino board and interact with the board inputs and outputs. J5 also adds support for the REPL (Read-Eval-Print-Loop) command line, so when you are running your node.js code you can type in commands in the terminal and interact with your Arduino board live (using the objects that you created in your code). This is great for debugging and for just learning how to use the API in general.

J5 makes it super easy. As an example, using J5 and node.js to control an LED that is attached to the sensor shield output O0, you would do something like:

```javascript
var five = require('johnny-five');
var board = new five.Board();

// when board is booted and connected, turn on the LED
board.on('ready', function() {
  var myLed = new five.Led('O0');
  myLed.on();
});
```

When creating a new J5 sensor object, you can specify the frequency at which you want to take sensor data readings (ms). A callback is specified that will be invoked each time new data is received from the sensor. For example, to use J5 to read light sensor data from the Arduino board every 10 seconds:

```javascript
var five = require('johnny-five');
var board = new five.Board();

// when board is booted and connected, get light sensor data every 10 seconds
board.on('ready', function() {
  var myLightSensor = new five.Sensor({pin:'A0', freq: 10000});
  myLightSensor.on('data', () => {
      lightValue = myLightSensor.value;
      console.log(`Light sensor reading: ${lightValue}`);
  });
});
```

To post sensor data to the SparkFun data stream, SparkFun provides the [Phant-Client](https://www.npmjs.com/package/phant-client) NPM package which uses the [Phant API](http://phant.io/docs/input/http/). First you have to connect to your existing SparkFun data stream, like this:

```javascript
var Phant = require('phant-client').Phant;

var phant = new Phant();
var iri = 'https://data.sparkfun.com/streams/' + '<your_data_stream_public_key_here>';

// connect to the data stream
phant.connect(iri, function(error, streamd) {
    if (error) {
      // handle error
    } else {
      // successfully connected to the data stream, so continue
    }
});
```

After connecting to the stream you need to add the stream's private key to the stream object, so that you can post data:

```javascript
myStream = streamd;
myStream.privateKey = sparkey; // sparkey contains the private key
```

Then the sensor data (lightValue, and tempValue in this example) can be posted using phant.add. A callback is provided which is invoked once the data has been successfully posted to your stream. Important: the value names you provide must match the field names that you specified at the time of your stream creation:

```javascript
// post to my data.sparkfun.com stream
phant.add(myStream, {light: lightValue, temp_c: tempValue}, () => {
  console.log(`Successfully posted to ${iri}`);
});
```

My full node.js code that I developed for this experiment can be found [here in my Github repo](https://github.com/rwood-moz/iot-hacking/blob/master/arduino/sparkfun.js).

**Step 4: Start it Up!**

With my Arduino board connected to USB and powered up, I started my node.js program in an Ubuntu terminal (providing my SparkFun stream private key as an environment variable on the command line). 

My program successfully connected to my Sparkfun data stream online. Once the Arduino board entered the 'ready' state my program began grabbing light and temperature sensor data every minute, posting each data-set to my live stream. I let it run for awhile to generate some data (and at one point I turned on a lamp and touched the temperature sensor, to cause noticeable changes in the sensor values).

![arduinoconsole](https://cloud.githubusercontent.com/assets/2198968/13439854/54c90a4e-dfbd-11e5-8639-88f69bfded74.png)
_Console output for my node.js program. I turned a desk lamp on and touched the temperature sensor just before sensor reading 8_

**Step 5: View the Data Online**

Now that data was successfully being posted to my live stream, I could go and check it out! I just browsed to [my sensor stream alias](https://data.sparkfun.com/robs_office) or directly to my [sensor stream URL](https://data.sparkfun.com/streams/JxEyArKAN9T1g08J1rNR), and there it is. Success!

![mystream](https://cloud.githubusercontent.com/assets/2198968/13406771/569a100e-def3-11e5-93ea-22813432096b.png)
_My resulting live sensor data stream on data.sparkfun.com_

Besides viewing your own data, you can explore the other [SparkFun Public Streams](https://data.sparkfun.com/streams/) and see what other people are posting too.

**Exporting Sensor Data**

Another really cool feature of [data.sparkfun.com](https://data.sparkfun.com/) is that you can export all of your sensor data from the cloud to your local drive. All you have to do is browse to your data stream, then in the top left there is the option to export to JSON, CSV, etc. I tested this out and exported all of my sensor data at that particular time to JSON, and you can see the [resulting JSON file here](https://github.com/rwood-moz/iot-hacking/blob/master/arduino/sparkfun-export.json) in my Github repo.

**In Summary**

Using my [Arduino](https://www.arduino.cc/) board, the [Johnny-five](http://johnny-five.io/) node.js framework, and the [Phant-Client](https://github.com/dpjanes/iotdb-phant-client), it was relatively easy to publish my sensor data on [data.sparkfun.com](https://data.sparkfun.com/). Cloud publishing services like this will encourage and enable hackers to get involved in the internet-of-things and learn new skills in general. Very cool!

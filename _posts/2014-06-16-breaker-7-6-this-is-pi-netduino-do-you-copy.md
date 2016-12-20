---
ID: 1843
post_title: >
  Breaker 7-6, This is Pi, Netduino Do You
  Copy?
author: Marc LaFleur
post_date: 2014-06-16 22:12:31
post_excerpt: >
  I recently wrote about getting the a
  Raspberry Pi connected with Azure
  storage. This works well for when you
  have a full network stack to work with
  but what those scenarios where you
  don’t have this luxury? Here we’ll
  walk through one potential solution
  using a couple of cheap nRF24L01+ radio
  modules, a Netduino 2 and a Raspberry
  Pi.
layout: post
permalink: >
  http://massivescale.com/breaker-7-6-this-is-pi-netduino-do-you-copy/
published: true
dsq_thread_id:
  - "3539258146"
---
I recently wrote about getting the a <a href="http://massivescale.azurewebsites.net/hello-azure-my-name-is-pi/" target="_blank">Raspberry Pi connected with Azure</a> storage. This works well for when you have a full network stack to work with but what those scenarios where you don’t have this luxury? Here we’ll walk through one potential solution using the some super inexpensive radios, a <a href="http://www.amazon.com/gp/product/B009QOWOFU/ref=as_li_tl?ie=UTF8&amp;camp=1789&amp;creative=390957&amp;creativeASIN=B009QOWOFU&amp;linkCode=as2&amp;tag=soapb30-20" target="_blank">Netduino 2</a> and the <a href="https://www.amazon.com/RASPBERRY-MODEL-756-8308-Raspberry-Pi/dp/B009SQQF9C/ref=as_sl_pc_ss_til?tag=soapb30-20&amp;linkCode=w01&amp;linkId=&amp;creativeASIN=B009SQQF9C" target="_blank">Raspberry Pi</a>.

The architecture of this solution is pretty simple. We’re going to turn the Raspberry Pi into a hub for one or more stand-alone microcontrollers. In this example I’m using a Netduino 2 but this model works with just about any microcontroller (Arduino, BeagleBoard, etc.).  The radios are <a href="https://www.amazon.com/nRF24L01-Wireless-Transceiver-Arduino-Compatible/dp/B00E594ZX0/ref=as_sl_pc_ss_til?tag=soapb30-20&amp;linkCode=w01&amp;linkId=&amp;creativeASIN=B00E594ZX0" target="_blank">nRF24L01+ 2.5Ghz</a> transceivers.

<a href="http://massivescale.blob.core.windows.net/blogmedia/2014/06/rpi_nd_nrf.png"><img style="margin: 0px auto; border: 0px currentcolor; float: none; display: block; background-image: none;" title="rpi_nd_nrf" src="http://massivescale.blob.core.windows.net/blogmedia/2014/06/rpi_nd_nrf_thumb.png" alt="rpi_nd_nrf" width="435" height="242" border="0" /></a>

<h4>Prepping the Pi</h4>

Before we can use the nRF module with the Pi we need to first install a couple of packages. The nRF radio uses a standard SPI (serial to parallel interface) connection plus a couple of additional pins to handle enabling transmission and handling notification of new messages coming in. In order to work support the module we’ll need to enable GPIO (and SPI).

There are a number of ways of getting GPIO and SPI set up on the Pi. My personal preference is a project called <a href="http://wiringpi.com/download-and-install/" target="_blank">WiringPi</a> due to the drop-dead simplicity of the process. There are complete instructions (and lots of other interesting tid-bits) available as the <a href="http://wiringpi.com/download-and-install/" target="_blank">WiringPi site</a> but the bare-bone-basic installation requires just a couple of lines:

<div id="scid:C89E2BDB-ADD3-4f7a-9810-1B7EACF446C1:b25c7ac3-38c1-4508-a131-36ff85d23d65" class="wlWriterEditableSmartContent" style="margin: 0px; padding: 0px; float: none; display: inline;">

[sourcecode language="bash"]
sudo apt-get update
sudo apt-get upgrade
sudo apt-get install git-core
git clone git://git.drogon.net/wiringPi
cd wiringPi
./build
gpio -v
[/sourcecode]

</div>

Once completed you should see the version number (currently 2.14) displayed on the screen. The only remaining task is to enable SPI. Please note that WiringPi is designed for prototyping which means it doesn’t permanently enable SPI. This means that you’ll have to execute this command again after a restart. It isn’t a big deal but I’ve caught myself running a script and wondering why it failed only to remember I needed to re-enable SPI.

<div id="scid:C89E2BDB-ADD3-4f7a-9810-1B7EACF446C1:ce19ffa9-17eb-4f7c-92a4-8ff50019e6ab" class="wlWriterEditableSmartContent" style="margin: 0px; padding: 0px; float: none; display: inline;">

[sourcecode language="bash"]
gpio load spi
[/sourcecode]

</div>

Finally we need to install the Node-NRF package for Node.js. This will provide the interface between Node and our radio (if you get a chance, show your appreciation
by giving the author a star over at GitHub <a href="https://github.com/natevw/node-nrf">https://github.com/natevw/node-nrf</a>. They did an awesome job).

<div id="scid:C89E2BDB-ADD3-4f7a-9810-1B7EACF446C1:277086d7-da87-462e-bbba-9b4705545915" class="wlWriterEditableSmartContent" style="margin: 0px; padding: 0px; float: none; display: inline;">

[sourcecode language="bash"]
npm install nrf
[/sourcecode]

</div>

Now we can move on to actually wiring the radio. GPIO on the Pi can be a little difficult thanks to the male pin header. I’ve taken to using a little device from <a href="https://www.adafruit.com/" target="_blank">Adafruit</a> called the <a href="http://www.amazon.com/gp/product/B00JE1T1WY/ref=as_li_tl?ie=UTF8&amp;camp=1789&amp;creative=390957&amp;creativeASIN=B00JE1T1WY&amp;linkCode=as2&amp;tag=soapb30-20&quot;" target="_blank">Pi T-Cobbler</a> that makes life a lot easier. It allows you to use a simple breadboard instead of messing around with female to female jumper cables.  The pin configuration is as follows:

<a href="http://massivescale.blob.core.windows.net/blogmedia/2014/06/pi-nrf.png"><img style="margin: 0px auto; border: 0px currentcolor; float: none; display: block; background-image: none;" title="pi-nrf" src="http://massivescale.blob.core.windows.net/blogmedia/2014/06/pi-nrf_thumb.png" alt="pi-nrf" width="576" height="336" border="0" /></a>

<h4>Prepping the Netduino</h4>

For the Netduino I started with <a href="http://nrf24l01.codeplex.com/" target="_blank">Jakub Bartkowiak’s nRF24L01p driver on Codeplex</a>. This worked extremely well when both sides were Netduino’ s but when one side was an Arduino or Pi it fell down. Thankfully <a href="http://forums.netduino.com/index.php?/topic/8266-433mhz-24ghz-communications-with-netduinonetduino-plus/?p=57957" target="_blank">ShVerni over in the Netduino forums</a> pointed out that the driver wasn’t in compliance with the nRF24L01+ spec. According to the spec all data must be sent Least Significant Byte First (i.e. inverted). With a few changes to the driver (and condensing it into a single .cs file) I had a working driver. I’ve put up my altered version at <a title="https://gist.github.com/mlafleur/44a54c0f9b15b0b5f285" href="https://gist.github.com/mlafleur/44a54c0f9b15b0b5f285">https://gist.github.com/mlafleur/44a54c0f9b15b0b5f285</a>.

The wiring for the Netduino is very straightforward:

<a href="http://massivescale.blob.core.windows.net/blogmedia/2014/06/image.png"><img style="margin: 0px auto; border: 0px currentcolor; float: none; display: block; background-image: none;" title="Netduino to nRF " src="http://massivescale.blob.core.windows.net/blogmedia/2014/06/image_thumb.png" alt="Netduino to nRF Mappings" width="586" height="343" border="0" /></a>

<h4></h4>

<h4>Turing It On</h4>

Since this is a proof of concept the code is extremely simple.  The nRF module can transmit to 1 address and receive on 6. For our example we’re telling the Raspberry Pi to listen for messages at 0xF0F0F0F0E1 and transmit messages to 0xF5F0F0F0F2 (the Netduino is logically the opposite). The goal is to have the Netduino send a message to the Pi and for the Pi to then bounce that message back. This will illustrate how the modules work without any application specific clutter.

The code for the Netduino can be found at <a title="https://github.com/mlafleur/Netduino-nRF24L01p" href="https://github.com/mlafleur/Netduino-nRF24L01p">https://github.com/mlafleur/Netduino-nRF24L01p</a>. Alternatively you can download <a title="Netduino-nRF24L01p as a zip file" href="https://github.com/mlafleur/Netduino-nRF24L01p/archive/master.zip">Netduino-nRF24L01p as a zip file</a>. Once you have the project loaded in Visual Studio you can simply deploy to your Netduino by pressing F5. The debugger will begin outputting some status information.

The core component of this code can be found in the Start() method of Program.cs. In here we initialize and enable the radio (the rest is fairly common C#).

<div id="scid:C89E2BDB-ADD3-4f7a-9810-1B7EACF446C1:4b2d43ca-49e6-4708-a2c0-1725daa8e63e" class="wlWriterEditableSmartContent" style="margin: 0px; padding: 0px; float: none; display: inline;">

[sourcecode language="csharp"]
// Initialize the radio on our pins
_radio.Initialize(SPI_Devices.SPI1, Pins.GPIO_PIN_D10, Pins.GPIO_PIN_D9, Pins.GPIO_PIN_D8);
_radio.Configure(new byte[] { 0xF5, 0xF0, 0xF0, 0xF0, 0xF2 }, 76, NRFDataRate.DR1Mbps);
_radio.OnDataReceived += _radio_OnDataReceived;
_radio.Enable();
[/sourcecode]

</div>

The first line initializes the correct pins while the second configures the radio to listen at F5F0F0F0F2 on channel 76 with a data rate of 1 Mbps. We then wire up the event for data received and enable the radio.

The code for the Raspberry Pi can be found at <a title="https://gist.github.com/mlafleur/4fc521b23c2fd0cfab13" href="https://gist.github.com/mlafleur/4fc521b23c2fd0cfab13">https://gist.github.com/mlafleur/4fc521b23c2fd0cfab13</a>. Once run you should begin seeing communication on both the console of the Pi and the debugger of the Netduino.

<h4>Coming Soon…</h4>

In another post I will start digging in to this model a little deeper. We will be wiring up some sensors to the Netduino and routing the results to Azure through the Pi Hub. We’ll also investigate using an Arduino along side the Netduino.
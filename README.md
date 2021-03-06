# homebridge-hubitat-tonesto7

This is based off of @pdlove homebridge-smartthings

[![npm version](https://badge.fury.io/js/homebridge-hubitat-tonesto7.svg)](https://badge.fury.io/js/homebridge-hubitat-tonesto7)

**```Current App version: 1.1.6```**

<br>

# Change Log:

#### Hubitat App:

***v1.0.0*** - Ported app over from my SmartThings version.

***v1.0.1*** - Hubitat Safety Monitor Support is set to Off by Default.

***v1.1.3*** - App Cleanups.  Added Windows Shades support for Native HomeKit control.

***v1.1.5*** - Code Cleanups

***v1.1.5*** - Shade Fixes

#### Homebridge Plugin:

***v1.0.0*** - Reworked alot of the code to allow for better direct communication with Hubitat

***v1.1.2*** - Added Native support for Window Shades

***v1.1.3*** - Readme Update test

***v1.1.7*** - Fixed Shades Support

***v1.1.8*** - Shade Fixes

<br>

# Explanation:

### Direct Updates
This method is nearly instant.
This option allows the hub to send updates directly to your homebridge-hubitat-tonesto7 installation.
The hub must be able to send an http packet to your device so make sure to allow incoming traffic on the applicable port.
The port used for this can be configured by the "direct_port" setting and defaults to 8000.
The program will attempt to determine your IP address automatically, but that can be overridden by "direct_ip" which is useful if you have multiple addresses.

When properly setup, you should see something like this in your Homebridge startup immediately after the PIN:
```
[1/29/2017, 8:28:45 AM] Homebridge is running on port 51826.
[1/29/2017, 8:28:45 AM] [Hubitat] Direct Connect Is Listening On 10.0.0.70:8000
[1/29/2017, 8:28:45 AM] [Hubitat] Hubitat Hub Communication Established
```

<br>

# Installation:

Installation comes in two parts:

## 1. Hubitat App Installation

* Open your Hubitat web interface
* Goto <u><b>```Apps Code```</b></u>
* Copy/Paste the code from [Hubitat App Code](https://raw.githubusercontent.com/tonesto7/homebridge-hubitat-tonesto7/master/smartapps/tonesto7/homebridge-hubitat.src/homebridge-hubitat.groovy) 
* Press <u><b>```Save```</b></u>
* Press <u><b>```Oauth```</b></u> and press <u><b>```Enable```</b></u>
* Press <u><b>```Save```</b></u>
* Your <u><b>```Done```</b></u> with the Hubitat code install.

## 2. Hubitat App Configuration

* Under the Hubitat Web Interface, Click on <u><b>```Apps```</b></u> in the left side menu. 
* Click on the button <u><b>```+Load New App```</b></u>
* Select <u><b>```Homebridge (Hubitat)```</b></u> from the list of User Apps
* There are 4 inputs at the top that can be used to force a device to be discovered as a specific type in HomeKit.
* For any devices not added by type Tap on the input next to an appropriate device group and then select each device you would like to use (The same devices can be in any of the Sensor, Switch, Other inputs)
  * There are several categories because of the way Hubitat assigns capabilities. So you might not see your device in one, but might in another.
  * Almost all devices contain the Refresh capability and are under the "Other Devices" group
  * Some sensors don't have a refresh and are under the "Sensor Devices" group.
  * Some devices, mainly Virtual Switches, only have the Switch Capability and are in the "Switch Devices".
 
 * If you select the same device in multiple categories it will only be shown once in HomeKit, so you can safely check them all in all groups.
 * If a device isn't listed, let me know by submitting an issue on GitHub.
 * Tap <u><b>```Done```</b></u> and you are finished with the App configuration.


## 3. Homebridge Plugin Installation:

 1. Install homebridge using: ```npm i -g homebridge``` (For Homebridge Install: [Homebridge Instructions](https://github.com/nfarina/homebridge/blob/master/README.md))
 2. Install Hubitat plugin using: ```npm i -g homebridge-hubitat-tonesto7```
 3. Update your configuration file. See sample config.json snippet below.

  <h3 style="padding: 0em .6em;">Config.json Settings Example</h3>

  <h4 style="padding: 0em .6em; margin-bottom: 5px;"><u>Example of all settings. Not all settings are required. Read the breakdown below</u></h4>
   
   <div style=" overflow:auto;width:auto;border-width:.1em .1em .1em .8em;padding:.2em .6em;"><pre style="margin: 0; line-height: 125%"><span style="color: #f8f8f2">{</span>
   <span style="color: #f92672">&quot;platform&quot;</span><span style="color: #f8f8f2">:</span> <span style="color: #e6db74">&quot;Hubitat&quot;</span><span style="color: #f8f8f2">,</span> 
   <span style="color: #f92672">&quot;name&quot;</span><span style="color: #f8f8f2">:</span> <span style="color: #e6db74">&quot;Hubitat&quot;</span><span style="color: #f8f8f2">,</span>
   <span style="color: #f92672">&quot;app_url&quot;</span><span style="color: #f8f8f2">:</span> <span style="color: #e6db74">&quot;10.0.0.40/api/app/YOUR_APPS_ID/&quot;</span><span style="color: #f8f8f2">,</span>
   <span style="color: #f92672">&quot;access_token&quot;</span><span style="color: #f8f8f2">:</span> <span style="color: #e6db74">&quot;THIS-SHOULD-BE-YOUR-TOKEN&quot;</span><span style="color: #f8f8f2">,</span>
   <span style="color: #f92672">&quot;direct_ip&quot;</span><span style="color: #f8f8f2">:</span> <span style="color: #e6db74">&quot;10.0.0.70&quot;</span><span style="color: #f8f8f2">,</span>
   <span style="color: #f92672">&quot;direct_port&quot;</span><span style="color: #f8f8f2">:</span> <span style="color: #ae81ff">8000</span><span style="color: #f8f8f2">,</span>
<span style="color: #f8f8f2">}</span>
</pre></div>


 * <p><u>platform</u> & <u>name</u>  <small style="color: orange; font-weight: 600;"><i>Required</i></small><br>
    This information is used by homebridge to identify the plugin and should be the settings above.</p>

 * <p><u>app_url</u> & <u>access_token</u>  <small style="color: orange; font-weight: 600;"><i>Required</i></small><br>
    To get this information, open Hubitat web interface in your browser, goto "Apps" "Homebridge (Hubitat)" and tap on "View Configuration Data for Homebridge"<br><small style="color: yellow;"><b>Notice:</b> The app_url in the example above may be different for you.</small></p>

 * <p><u>direct_ip</u>  <small style="color: #f92672; font-weight: 600;"><i>Optional</i></small><br>
    Defaults to first available IP on your computer<br><small style="color: gray;">Most installations won't need this, but if for any reason it can't identify your ip address correctly, use this setting to force the IP presented to Hubitat for the hub to send to.</small></p>

 * <p><u>direct_port</u>  <small style="color: #f92672; font-weight: 600;"><i>Optional</i></small><br>
   Defaults to 8000<br><small style="color: gray;">This is the port that homebridge-hubitat plugin will listen on for traffic from your hub. Make sure your firewall allows incoming traffic on this port from your hub's IP address.</small></p>



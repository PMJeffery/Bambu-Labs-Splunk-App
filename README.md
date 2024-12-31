
Foreword: This app has zero official affiliation with Bambu Labs, Home Assistant or Splunk.  This is a completely voluntary and free Splunk App for anyone to use. 

# Dashboards for 3D Printers
## Why?
There is really no good way of tracking your print progress or status of your Bambu Lab printer(s) outside of the desktop or mobile app.  

Tested on Splunk Enterprise 9.3.x, Home Assistant 2024.12.x, Bambu Labs P1S w/ AMS (latest firmware as of 12/2024)

Current Data Flow: Bambu Labs P1S > Home Assistant > Splunk

## How?
### Prerequisites 
- Bambu Lab Printer (P1S - tested, but other existing and future ones should/may work)
    - Optional: Bambu Labs AMS Unit (Tested in this app to work)
- Home Assistant (HA)
    - HACS installed
    - Bambu Labs integration added
    - Your printer added to HA
- Splunk Enterprise 9.x (Tested) // Splunk Cloud (should work)
    - Create Index for HA, index=hassio
    - Create and configure a HEC token for your HA index
	    - Choose a different index by selecting it in the **Available Indexes** pane of the **Select Allowed Indexes** control.  Select 'hassio'
    - Install this app (see Release section)
    - Note: All HA events will go to Splunk, not just the Bambu Labs printer events!

## What?
### Integration Instructions
#### Splunk Enterprise
1. Download and install Splunk Enterprise (Requires Splunk.com Account)
    - https://www.splunk.com/en_us/download/splunk-enterprise.html
    - https://docs.splunk.com/Documentation/Splunk/9.4.0/Installation/Chooseyourplatform 
 2. Create index
     - https://docs.splunk.com/Documentation/Splunk/9.4.0/Indexer/Setupmultipleindexes#Create_events_indexes_2

3. Create HEC Token
    - https://docs.splunk.com/Documentation/Splunk/9.4.0/Data/UsetheHTTPEventCollector#Configure_HTTP_Event_Collector_on_Splunk_Enterprise
4. Install Bambu Labs Splunk App
	- Extract the zip file and copy the "3d printer" folder to $SPLUNK/etc/apps/
	- Restart Splunk via web UI or via command line
		- Settings > Server Controls > Restart Splunk
		- $SPLUNK/bin/ ./splunk restart

#### Home Assistant
1. Setup HA w/ HACS
    - https://hacs.xyz/docs/use/download/download/
2. Setup Bambu Labs integration with HACS
    - https://github.com/greghesp/ha-bambulab
3. Add Splunk HA integration
    - https://www.home-assistant.io/integrations/splunk/
    - Example configuration.yaml 
``` yaml 
#Splunk HEC
splunk:
  token: <paste your HEC token here>
  host: <FQDN or IP of your Splunk Server>
  port: 8088
  ssl: false
  verify_ssl: false
  name: homeassistant
```

### Splunk App Configuration
1. The default index used is 'hassio' 
	- If you are using a different index, you can do a find-and-replace accordingly 
	- Dashboard code is located in $SPLUNK/etc/apps/3d_printer/local/data/ui/views

### Acknowledgements
- SVG Icons from svgrepo.com

## To-Do List
- [ ] Add AMS visualization
- [ ] Add tabs for print farm, basic stats, historical stats
- [ ] Add Bambu Lab printer image logic for AMS Hex Color codes
- [ ] Add Instructions dashboard w/ MarkDown text
- [ ] Fix dashboard reports to auto refresh
- [ ] Fix reports that don't show latest data
- [ ] Create saerch macross for different printer serial numbers, indexes, etc.
- [x] ~~Upload current build~~
- [x] ~~Add SVG Icons~~


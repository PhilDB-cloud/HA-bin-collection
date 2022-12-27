# HA-bin-collection
Home assistant: Mid and East Antrim bin refuse collection integration

## Important note: troubleshooting
If the yaml is incorrect the check that it doesn't identify an area that you have changed.

If no values are returned then manually check that the site url for your street (see below) is correct and available through a browser.  Sometimes the response is slow for the site.

# HA Mid and East Antrim refuse collection custom component

This integration is intended for residents of Northern Ireland in the Mid and East Antrim council.  We currently have a Brown and a Black (officially a Grey) wheelie bin which need to be presented for collection on alternate weeks.  The council website (https://www.midandeastantrim.gov.uk/resident/waste-recycling/collection-dates/) provides an interface for residents to find out which bin to present for collection and on which day.  

This component uses the Multiscrape component to pull the relevant data from the council website and create relevant sensors in Home Assistant so that you can be reminded which bin to put out this week and when.  There are sensors for how many days until collection so that automations can be created for reminders the day before and also sensors to alert to public holidays in case the collection date has been moved to another day (which isn't reflected on the published schedule of collections).

The sensors update every 8 hours.  There should be no need to run it more frequently than that although you may decide to run it less frequently, in which case update the scan_interval to the appropriate number of seconds.  


## Installation

[![hacs][hacsbadge]][hacs]

Currently not available.

### Manually

Install Hacs, Multiscrape and holiday helper.
Holiday helper https://github.com/bruxy70/Holidays
Multiscrape https://github.com/danieldotnl/hass-multiscrape

Add the following line to your configuration.yaml file and then copy the multiscrape.yaml file into the same directory as your configuration.yaml.

```yaml
multiscrape: !include multiscrape.yaml
```

You will need to find the url for your street to add into the first line of multiscrape.yaml.  Go to https://www.midandeastantrim.gov.uk/resident/waste-recycling/collection-dates/ and select your town and street.  You will then be directed to a page with your street's bin collection details.  Copy that url from the address bar and paste it into the first line of the multicrape.yaml after '- resourse: ', replacing the placeholder that is already in the file

Save your changes and go to the developer section to check the yaml is valid and then restart Home Assistant.

## Sensors

Based on latest (pre) release.


| name                            | description                                                        | 
| ------------------------------- | ------------------------------------------------------------------ | 
| sensor.next_bin_collection      | Next Bin Collection - colour of bin to present                     |
| sensor.next_bin_collection_black| Next Black Bin Collection date                                     |
| sensor.next_bin_collection_brown| Next Brown Bin Collection date                                     |
| sensor.next_bin_collection_date | Collection Date for the next collection                            |
| sensor.next_bin_days_away       | Days to Next Collection                                            |
| sensor.next_bin_days_away_black | Days to Next Black Bin Collection                                  |
| sensor.next_bin_days_away_brown | Days to Next Brown Bin Collection                                  |
| sensor.next_bin_holiday_name    | Collection Day Holiday Name (None if not a holiday)                |
| sensor.next_bin_is_a_holiday    | Next Collection Day is a Holiday (true or false)                   |
| ------------------------------- | ------------------------------------------------------------------ | 


## Debug logging

Debug logging can be enabled as follows:

```yaml
logger:
  default: info
  logs:
    custom_components.multiscrape: debug
```

Depending on your issue, also consider enabling `log_response`.

### Contributions are welcome!

I'm not totally sure what I am doing in relation to all of this so please feel free to suggest any improvements (preferably not just code refactoring)

### Credits


---

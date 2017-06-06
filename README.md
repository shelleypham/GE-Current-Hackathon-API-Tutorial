# GE-Current-Hackathon-API-Tutorial
This documentation provides more details on how to set up the hackathon environment on Postman, retrieve Intelligent Cities (IC) and Intelligent Enterprises (IE) access tokens, and how to use those access token to retrieve resources.

### Contents
- [Set up Postman Environments](#set-up-postman-environment)
- [Retrieve Access Tokens](#retrieve-access-token)
- [Intelligent Cities - Retrieve Parking Zone Details](#intelligent-cities---retrieve-parking-zone-details)
- Intelligent Enterprises (In progress)

## Set up Postman environment
1. Download `Predix Transform Hackathon` environment provided by GE.
2. Go to `Settings` (the cog icon on the upper right), then click `Manage Environments`.
3. Click `Import` and find your environment file.

## Retrieve Access Token
1. Make sure the request is set to `GET`. If you're using IC, copy and paste this line:
```
{{ic_uaa_url}}/oauth/token?grant_type=client_credentials
```
For IE, copy and paste this line:
```
{{ie_uaa_url}}/oauth/token?grant_type=client_credentials
```

2. Under `Headers`:
Type `Authorization` under `Keys`, and its value is
```
Basic aGFja2F0aG9uOkBoYWNrYXRob24=
```

3. Press `Send`. You should see body text in json format.

4. Copy the contents in between the quotes of the `access_token`. You will need this access token to retrieve contents from your IC or IE APIs, depending on what you choose.


## Intelligent Cities - Retrieve Parking Zone Details
*There are many resources that could be retrieved. For the sake of time, I'll explain how to retrieve parking data based on a particular zone.*
1. In the address bar, copy and paste this:
```
{{ic_metadataurl}}/locations/{{locationId}}
```

2. Under `Headers`
Type `Authorization` under `Keys`, and its value is
```
Bearer YOUR_ACCESS_TOKEN
```
where YOUR_ACCESS_TOKEN is what you copied from the earlier steps.

Other `Keys` and `Values` you need:
```
Content-Type
application/x-www-form-urlencoded
```
```
Predix-Zone-Id
{{parking_zone_id}}
```

3. Press `Send` to retrieve parking data.

4. Your body output should look something like this
```
{
  "locationUid": "LOCATION-213",
  "locationType": "PARKING_ZONE",
  "parentLocationUid": null,
  "coordinatesType": "GEO",
  "coordinates": "32.713584194572846:-117.15861705406382,32.713554100678394:-117.15861805406382,32.713551201356786:-117.1589225508907,32.71358309389445:-117.15892441316802",
  "name": null,
  "city": "San Diego",
  "state": "CA",
  "country": "USA",
  "zipcode": "92101",
  "timezone": "PST",
  "properties": {
    "PARK_DIRECTION": "270"
  },
  "address": "1029-P4@601-699 F St",
  "analyticCategory": {
    "PKOCC": "PARKING",
    "PKOVLP": "PARKING"
  }
}
```

## Intelligent Enterprises
In progress.

# Dahua SDK
A module for Dahua IP Cameras to retrieve the people counting statistics through the RPC2 interface.

## Info

API's are extracted by reverse engineering the JavaScript in Web UI. 

## Example Snippet

Login to camera
```py
from dahua_rpc import DahuaRpc

# Initialize the object
dahua = DahuaRpc(host="192.168.1.10", username="admin", password="password")

# Login to create session
dahua.login()
```

Some basic functions
```py
# Get the current time on the device
print(dahua.current_time())

# Get serial number
print("SN : " + (dahua.request(method="magicBox.getSerialNo"))['params']['sn'])
```

Get ANPR details
```py
# Get the people counting statistics for defined area and specific period of time by using the following
# Get the statistics object id
object_id = dahua.get_people_counting_info() 

# Request the total count of the statistics stored for the defined period of time
print("\nTotal number of statistics stored data : ", 
	dahua.start_find_statistics_data(object_id, 
	"2024-05-13 00:00:00", 
	"2024-05-15 23:59:59", 
	1) ) 

# Get statistics list
r = dahua.do_find_statistics_data(object_id)
print(*r, sep = "\n")

# Release token
dahua.stop_find_statistics_data(object_id)

dahua.logout() 
```


## Credits

Forked from [this gist](https://github.com/naveenrobo/dahua-ip-cam-sdk.git) and added filtering and retrieving statistics for the count of people who have passed through the defined zone.

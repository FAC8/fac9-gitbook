# Morning Challenge

## Goal
**Master callbacks**
<p></p>
![callback-hell](https://s3-ap-southeast-1.amazonaws.com/kipalog.com/B4UaJfMCQAE67QB.png_mnu9u7omer)

##Steps
1. **Pair up** and **choose 1-2 API**(s) you have **already used**. If you feel brave, by all means try new ones, but do *mind the timeline*.
2. Perform a series of combined(chained) asynchronous operations with the APIs.

####If you don't have an idea, try this:
1. Start from a physical address(street name and street number) and retrieve location info with **[Google Maps geocoding](https://developers.google.com/maps/documentation/geocoding/intro#geocoding)** 
2. Retrieve the weather forecast for the next 5 days for that location with **[MetaWeather API](https://www.metaweather.com/api)**. You will probably need 2 separate calls for that (one for location id, one for weather result).
3. Store the each day's forecast in a separate json file. If you haven't tried node's **fs** module yet, the docs are **[here](https://nodejs.org/api/fs.html#fs_fs_writefile_file_data_options_callback)**.

####Bonus
You can try this at home if you don't have time during the challenge.
4. Try to use the **[exec](https://nodejs.org/api/child_process.html#child_process_child_process_exec_command_options_callback)** function from node's ```child-process``` module to perform bash commands. Read the contents of the files in the directory where you saved the json files.
5. Write a test to check whether those files have the correct content. If you use fs, do not use the synchronous functions.
6. Delete the files where the forecast predicts bad weather.

####Banned:
* using synchronous functions or ```setTimeout```
* functions which are longer than 4 lines.
* promises... :( :( pity, they're actually fun.
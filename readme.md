# Monitor the health of your online data collections via scraping and APIs

## Purpose
Monitor the availability / recency of one's data scraping architecture.

## How
Python script (scheduled via Windows Task Scheduler or cron on Linux/Mac), that verifies the health of data collections, and pushes a daily status message to a mobile phone using the [Pushover Notification API](https://pushover.net).

## Running instructions

### i. Configure Environment Variables
Please store your Pushover login credentials in your system's/user's environment variables:

```
pushover_userkey = XXXXXXX (your user key to authenticate with Pushover)
pushover_apptoken = XXXXXXX (your app token)
```

For more information on setting environment variables, see https://github.com/RoyKlaasseBos/Hiding-Instagram-Likes/.

### ii. Installation and configuration
1. Install <a href="https://www.anaconda.com/products/individual">Anaconda</a> (Python distribution - including Jupyter Notebook).
2. Register with [Pushover](https://pushover.net), and obtain your user key and app key.
3. Configure your environment variables
4. Configure functions that define the health of your data collections (see examples)
5. Schedule to run `monitor.py` at desired intervals

### iii. Examples

- The current implementation connects to Amazon S3, scans the directory of the `uvt-netflix` bucket (directory: `raw/csv`),
and returns TRUE if at least one of the available files is stamped with today's date, and larger than 10000 bytes. In other words,
the function checks whether the scraper has pushed data to S3 today, and that the data is not empty.

## Screenshots

### Pushover

![Screenshot from Pushover.net](/doc/pushover.png)
 
### Windows Task Scheduler

__Configuring triggers__

Here: task configured to occur daily at 11.55am.

![Screenshot to configure triggers](/doc/taskscheduler-triggers.png)
 
 __Configuring actions__

Here: run.bat is called, which opens Anaconda prompt and runs the script `monitor.py`. Remember to set working directory to the same path as the monitoring scripts.

![Screenshot to configure actions](/doc/taskscheduler-actions.png)

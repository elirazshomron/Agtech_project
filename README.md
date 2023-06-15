# Agtech_project
#penman
#install pakcage
!pip install pyet




#import

import urllib
import matplotlib.pyplot as plt
import numpy as np
import pandas as pd
import matplotlib.dates as mdates
from datetime import datetime, timedelta

import matplotlib.pyplot as plt
import seaborn as sns
import matplotlib
import numpy as np
import pandas as pd
from pandas.plotting import register_matplotlib_converters
register_matplotlib_converters()  # datetime converter for a matplotlib
sns.set(style="ticks", font_scale=1.5)
import pyet


# define what to download
channels = "2187009"
fields = "1,2,3,4,5,6,7,8"

# Calculate start and end times (6 PM yesterday to 6 PM today)
now = datetime.now()
start_time = datetime(now.year, now.month, now.day, 18, 0) - timedelta(days=1)
end_time = datetime(now.year, now.month, now.day, 18, 0)

start_time_str = start_time.strftime("%Y-%m-%d%%20%H:%M:%S")
end_time_str = end_time.strftime("%Y-%m-%d%%20%H:%M:%S")

# URL to fetch data from the last 24 hours
url = f"https://api.thingspeak.com/channels/{channels}/fields/{fields}.csv?start={start_time_str}&end={end_time_str}"

# Open the URL and get the response
data = urllib.request.urlopen(url)
# Read the response data
d = data.read()

# Save data to CSV
filename1 = '/content/drive/MyDrive/faculty/year_3/agro-tech_lab/data_2023-06-13_18-00-00_to_2023-06-14_18-00-00.csv'
file = open(filename1, "w")
file.write(d.decode('UTF-8'))
file.close()

# Load data
df = pd.read_csv(filename1)

# Rename columns
df = df.rename(columns={"created_at": "timestamp",
                        "field1": "Temperature (°C)",
                        "field2": "Altitude (m)",
                        "field3": "Radiation Intensity  (W/m²)",
                        "field4": "Latitude (rad)",
                        "field5": "Wind Speed (m/sec)",
                        "field6": "Pressure (kPa)",
                        "field7": "Humidity (%)",
                        "field8": "Elevation (m)",
                        })

# Set timestamp as index
df['timestamp'] = pd.to_datetime(df['timestamp'])
df = df.set_index('timestamp')
#convert the rad to the fit units

df['Radiation Intensity  (W/m²)'] = np.where(df['Radiation Intensity  (W/m²)'] < 0, 0, df['Radiation Intensity  (W/m²)'])
rad_sum=df['Radiation Intensity  (W/m²)'].sum()
rad_sum=(rad_sum*0.0864)/1000 #convert from W to MJ

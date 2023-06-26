Management of the water system in the plant

One of the critical questions in agriculture is the management of the water system. How do we know when to water? How much water did the plant lose and what does the root feel in its immediate environment?

There are many methods for managing the water system in the plant and in the field. Some are purely computational and some rely on direct measurement of the plant and its immediate environment. This project offers a solution for automatic irrigation based on a combination of the two methods together.
A computational PENMAN formula that returns the potential daily evapotranspiration, i.e. the atmospheric demand for evaporation. The formula is based on significant climatic data such as radiation, relative humidity, temperature, etc. With the help of this formula, we will know how much water the plant or the field has lost in a given time and how much must be returned to it.
This method does not necessarily reflect what is happening in the field in real-time.
To this end, we also resorted to a direct measurement of soil moisture, which reflects in real-time the availability of water to the root system.

The steps:

Part A- Irrigation based on calculation:
1. Collecting temperature, radiation, and relative humidity data (on ESP)
2. Sending the data to Thingspeaks.
3. Downloading the data and calculating the daily evaporation (Python)
4. Sending an 'Activate' message using the MQTT platform
5. Receiving the message in the ESP and opening the solenoid for the calculated time

Part B - Irrigation based on real-time water availability:
6. Using a soil moisture meter for the local opening of the solenoid upon crossing a lower threshold and closing upon reaching an upper threshold (on ESP).

In the end we created a simple and cheap kit for controlled and efficient automatic watering of the garden or the plant on the balcony

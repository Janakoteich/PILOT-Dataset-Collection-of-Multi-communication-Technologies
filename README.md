# Wireless-networks-scanning-Dataset-WBL-


In this repository you can find a dataset for the collected traces from scanning, by using FiPy microcontroller from Pycom. In each text file there is the output of the collected data. For each wireless technology the following features are collected:

Wifi: {time-stamp, ssid, bssid; sec, channel, rssi}

Bluetooth : {time-stamp, name, rssi, adv_tx_pwr, tx_range, def_tx_pwr, mac, scan_tx_pwr, conn_tx_pwr}

LoRa: {time-stamp, spreading_factor, data, frequency, bandwidth, rx_timestamp, rssi, snr, sfrx, sftx, tx_trials, tx_power, tx_time_on_air, tx_counter, tx_frequency}

Others:
{time-stamp, Acceleration, Roll, battery_voltage, battery_percentage, Pitch}


Dataset Guide: The dataset is composed of two main scenarios: Static and Mobile.

Static:
Office, Home, Restaurent, University

Mobile:
Pedestrian, Bus, Car, Train, Metro

More details regarding each scanned file can be found in the 'Dataset guide' file.

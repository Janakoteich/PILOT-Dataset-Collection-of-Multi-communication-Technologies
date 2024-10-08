# PILOT Dataset


In this repository you can find a dataset for the collected traces from scanning, by using FiPy microcontroller from Pycom. In each text file there is the output of the collected data. For each wireless technology the following features are collected:

Wifi: {time-stamp, ssid, bssid; sec, channel, rssi}

Bluetooth : {time-stamp, name, rssi, adv_tx_pwr, tx_range, def_tx_pwr, mac, scan_tx_pwr, conn_tx_pwr}

LoRa: {time-stamp, spreading_factor, data, frequency, bandwidth, rx_timestamp, rssi, snr, sfrx, sftx, tx_trials, tx_power, tx_time_on_air, tx_counter, tx_frequency}

Others:
{time-stamp, Acceleration, Roll, battery_voltage, battery_percentage, Pitch}

The dataset is scanned using FiPy microcontrollers from pycom.

Dataset Guide: The dataset is composed of two main scenarios: Static and Mobile.

Static:
Office, Home, Restaurent, University

Mobile:
Pedestrian, Bus, Car, Train, Metro

More details about the dataset are presented in the following article: https://inria.hal.science/hal-04524617/file/2024111813%20%284%29.pdf


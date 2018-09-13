# check_dht [![CodeFactor](https://www.codefactor.io/repository/github/wernerfred/check_dht/badge)](https://www.codefactor.io/repository/github/wernerfred/check_dht)

This plugin will read the temperature and humidity values from your sensor (dht11, dht22, 3202).

This check plugin needs the adafruit dht library available on: https://github.com/adafruit/Adafruit_Python_DHT.git

Usage:
```
> python check_dht.py -h
usage: check_dht.py [-h] [-wt WT] [-ct CT] [-wh WH] [-ch CH] {11,22,3202} gpio
```
Example check:
```
> python check_dht.py 22 4 -wt 40 -ch 99
OK - Temperature: 24.6 C  Humidity: 47.7 % | temperature=24.6c humidity=47%
```

Example ```CheckCommand``` for use with ```icinga2```:
```
object CheckCommand "check_dht" {
  command = ["/usr/bin/sudo", "/usr/bin/python", PluginDir + "/check_dht.py" ]
  arguments = {
    "--model" = {
       skip_key = true
       order = 0
       value = "$dht_model$"
    }
    "--gpio" = {
       skip_key = true
       order = 1
       value = "$dht_gpio$"
    }
    "--wt" = "$dht_warning_temperature$"
    "--wh" = "$dht_warning_humidity$"
    "--ct" = "$dht_critical_temperatur$"
    "--ch" = "$dht_critical_humidity$"
  }
}
```

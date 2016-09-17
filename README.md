python-OBD
==========

A python module for handling realtime sensor data from OBD-II vehicle
ports. Works with ELM327 OBD-II adapters, and is fit for the Raspberry
Pi.

Installation
------------

```Shell
$ pip install obd
```

Basic Usage
-----------
Single Command Query
```Python
import obd

connection = obd.OBD() # auto-connects to USB or RF port

cmd = obd.commands.SPEED # select an OBD command (sensor)

response = connection.query(cmd) # send the command, and parse the response

print(response.value) # returns unit-bearing values thanks to Pint
print(response.value.to("mph")) # user-friendly unit conversions
```

Multiple Command Query (CAN ECUs ONLY; 6 Commands MAX)
```Python
import obd

connection = obd.OBD() # auto-connects to USB or RF port

# query_multi(command1, ..., command6, force=False/True)
# function uses an arbitrary argument (*args) for the commands, and keyword arg (**kwargs) for command forcing.

# commands can be input directly into the query_multi call
speed, rpm = connection.query_multi(obd.commands.SPEED, obd.commands.RPM) # send the command, and parse the response

# or, commands can be placed into a list, and then into the query_multi call. list variable must be unpacked with '*'
cmds = [obd.commands.SPEED, obd.commands.RPM]
speed, rpm = connection.query_multi(*cmds) # send the command, and parse the response

# responses will be assigned as OBDCommand objects into the variable order you called them
print(speed.value)
print(rpm.value)
```

Documentation
-------------

Available at [python-obd.readthedocs.org](http://python-obd.readthedocs.org/en/latest/)

Commands
--------

Here are a handful of the supported commands (sensors). For a full list, see [the docs](http://python-obd.readthedocs.io/en/latest/Command%20Tables/)

*note: support for these commands will vary from car to car*

-   Calculated Engine Load
-   Engine Coolant Temperature
-   Fuel Pressure
-   Intake Manifold Pressure
-   Engine RPM
-   Vehicle Speed
-   Timing Advance
-   Intake Air Temp
-   Air Flow Rate (MAF)
-   Throttle Position
-   Engine Run Time
-   Fuel Level Input
-   Number of warm-ups since codes cleared
-   Barometric Pressure
-   Ambient air temperature
-   Commanded throttle actuator
-   Time run with MIL on
-   Time since trouble codes cleared
-   Hybrid battery pack remaining life
-   Engine fuel rate

License
-------

GNU GPL v2

This library is forked from:

-   <https://github.com/peterh/pyobd>
-   <https://github.com/Pbartek/pyobd-pi>

Enjoy and drive safe!

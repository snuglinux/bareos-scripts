bareos-incoming-connect - Python script to replace the standard RunOnIncomingConnectInterval mechanism for performing backups for laptops, etc. (the devices is not constantly working). Currently not working correctly.

Additional dependencies: python2-bareos

The config file is located /etc/bareos/bareos-dir.d/bareos-scripts.conf
configuration file structure:
[NAME]      - section named director
address     - domain name or IP address of the director
port        - director port (default 9101)
enable      - will script be executed for this director or not (True or False)
name        - login to connect to the director console
password    - password to connect to the director console
hours_cycle - after how many hours to create a job, analogue of RunOnIncomingConnectInterval

The idea was taken from here: https://trac.dass-it.de/pub/browser/people/joerg.steffens/technical/bareos/triggerjob/triggerjob.py
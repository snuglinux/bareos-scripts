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

The script is started with the command:
  systemctl restart bareos-incoming-connect@bareos-dir.timer

bareos-dir - the name of the director to run

By default, the script will be executed every minute, you can change the script startup period for yourself in the configuration file /etc/systemd/system/bareos-incoming-connect@.timer.d/bareos-incoming-connect.conf

To view the list of running timers in the system, you can run:
  systemctl list-timers

The script uses only clients whose configuration uses the Connection From Client To Director = yes directive, and so that the Job does not run according to the schedule, Job must be set to Enabled = no.

Configuration example:

Client {
  Name = client1
  Address = 10.10.10.90
  Password = "123456"
  Connection From Client To Director = true
  Connection From Director To Client = no
}

Job {
  Name = "backup-client"
  Client = "client1"
  Enabled = no
  JobDefs = "backup-client-jobdefs"
}

The idea was taken from here: https://trac.dass-it.de/pub/browser/people/joerg.steffens/technical/bareos/triggerjob/triggerjob.py
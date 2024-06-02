# Setting up SSH connections to GFDL

## Establishing ssh keys

## Note your personal port numbers

```
ssh First.Last@analysis-rsa.princeton.rdhpcs.noaa.gov
```

At the end of the login message, you will see a list of local and remore port forwarding numbers. Make note of these numbers as you will need them in the next step:

```
You will now be connected to the lightest-loaded analysis host.
To select a specific host, hit ^C within 5 seconds.
Local port xxxxx forwarded to remote host.
Remote port yyyyy forwarded to local host.
```

Repeat this process for gaea:

```
ssh First.Last@gaea-rsa.princeton.rdhpcs.noaa.gov

...

You will now be connected to OneNOAA RDHPCS: Gaea (CMRS/NCRC) system.
To select a specific host, hit ^C within 5 seconds.
Local port ppppp forwarded to remote host.
Remote port qqqqq forwarded to local host.
```

## Obtain your VNC port forwarding number

You can access this by starting a VNC session on GFDL's public workstation

```
ssh First.Last@ssh.gfdl.noaa.gov
```

At the promopt, ssh to a public workstation (either `public3` or `public4`) and login with your GFDL password

```
ssh public3
```

## Start a VNC session (note: select the default value (1) for KDE without effects)

```
VNC 4b

```

This will print out a message that includes a port number (`vvvvv`) for VNC. Make note of this port for the next step:

```
* Establish port forwarding (tunnels) if coming from outside GFDL.
  Source port 5908 to public3:vvvv
  Linux / macOS OpenSSH command would be:
     ssh -l <First.Last> -L 5908:public3:vvvv ssh.gfdl.noaa.gov
  (replace <First.Last> with your username)
```


## Establish Personal Port Numbers for Jupter/Dask on Analysis

Every user should have their unique port number to run Jupyter and Dask on the analysis machine.  By default, Jupyter uses port 8888 and Dask uses port 8787. It creates a conflict if multiple users attempt to use the same port.

An easy reccomendation is to take your current zip code and make that your Jupyter port number (`aaaaa`). You can also create a port for Dask (`bbbbb`) by increment the last digit by 1.


## Setup `.ssh/config` file

Copy the contents of this template to file called `~/.ssh/config`

```
# -------------------- GFDL MACHINES
Host gfdl
  HostName                ssh.gfdl.noaa.gov
  User                    First.Last
  LocalForward            6022 public3.gfdl.noaa.gov:22
  LocalForward            5905 public3.gfdl.noaa.gov:vvvvv
  LocalForward            3128 mayflower.gfdl.noaa.gov:3128

Host wks
  HostName                localhost
  User                    First.Last
  Port                    6022
  LocalForward            8888 localhost:8888
  LocalForward            8787 localhost:8787
  LocalForward            aaaaa localhost:aaaaa
  LocalForward            bbbbb localhost:bbbbb


# -------------------- ANALYSIS MACHINES
Host analysis
  HostName                analysis-rsa.princeton.rdhpcs.noaa.gov
  User                    First.Last
  ControlMaster           auto
  LocalForward            xxxxx localhost:xxxxx
  RemoteForward           yyyyy localhost:22
  NoHostAuthenticationForLocalhost yes
  ForwardX11              yes
  StrictHostKeyChecking   no

Host analysis-boulder
  HostName                analysis-rsa.boulder.rdhpcs.noaa.gov
  User                    First.Last
  ControlMaster           auto
  LocalForward            xxxxx localhost:xxxxx
  RemoteForward           yyyyy localhost:22
  NoHostAuthenticationForLocalhost yes
  ForwardX11              yes
  StrictHostKeyChecking   no

Host an
  HostName                localhost
  User                    First.Last
  Port                    xxxxx
  LocalForward            aaaaa localhost:aaaaa
  LocalForward            bbbbb localhost:bbbbb
  StrictHostKeyChecking   no

Host an-remote
  HostName                localhost
  Port                    yyyyy
  User                    First.Last


# -------------------- GAEA MACHINES
Host gaea
  HostName                gaea-rsa.princeton.rdhpcs.noaa.gov
  User                    First.Last
  ControlMaster           auto
  LocalForward            ppppp localhost:ppppp
  RemoteForward           qqqqq localhost:22
  NoHostAuthenticationForLocalhost yes
  ForwardX11              yes

Host gaea-boulder
  HostName                gaea-rsa.boulder.rdhpcs.noaa.gov
  User                    First.Last
  ControlMaster           auto
  LocalForward            ppppp localhost:ppppp
  RemoteForward           qqqqq localhost:22
  NoHostAuthenticationForLocalhost yes
  ForwardX11              yes


Host *
  NoHostAuthenticationForLocalhost yes
  UseKeychain yes
  AddKeysToAgent yes
  IdentityFile ~/.ssh/id_rsa
  User                    First.Last
  CheckHostIP             yes
  ForwardAgent            yes
  ForwardX11              yes
  ControlPath             ~/.ssh/%r@%h:%p
  ControlMaster           no
  AddressFamily           inet
  ServerAliveInterval     60
```

Generate an SSH key on your machine
$ ssh-keygen -t rsa
save in .ssh/id_rsa_gfdl (set passphrase), also creates a .pub key
copy contents of .pub key to analysis .ssh/authorized_keys
(will be prompted to enter passphrase whenever connecting to the local host ex. an)

To screen jupyter 
$ nohup jupyter lab --port=____ --no-browser &
will return a job id (creates a new file nohup.out - here you can find localhost path to notebook that is still running)
$ ps -u (shows you current running PID)
$ kill id_number (consider deleting nohub.out)
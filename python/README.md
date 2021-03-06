# Hashtopolis Python Agent

[![CodeFactor](https://www.codefactor.io/repository/github/s3inlc/hashtopolis-agent/badge)](https://www.codefactor.io/repository/github/s3inlc/hashtopolis-agent)
[![LoC](https://tokei.rs/b1/github/s3inlc/Hashtopolis-Agent?category=code)](https://github.com/s3inlc/Hashtopolis-Agent)

This Hashtopolis agent is only compatible with Hashtopolis versions 0.5.0 and higher.

## Prerequisites

You need python3 installed on your agent system. 
Following python packages are required:

* requests

## Manual

You can either download the agent from the Hashtopolis new agent page or you can use the url shown there to download the agent with 
wget/curl.

### Run

To run the agent you simply need to call `python3 hashtopolis.zip`. There are no command line options accepted, all 
settings/configurations are done via the config file, described in the following section.

Please note that the client does not correctly recognize the OS when you are running in Cygwin or similar on Windows. You need to run it in Windows command line.

### Config

When you run the client for the first time it will ask automatically for all the requirement settings and then saves it automatically to a config file called `config.json`. This could for example look like this:

```
{
  "url": "https://coray.org/htp-test/src/api/server.php", 
  "token": "7RNDqtnPxm", 
  "uuid": "49dcd31c-3637-4f2a-8df1-b545202df5b3"
}
```

### Overview

| field                 | type    | default | description                                                                |
|-----------------------|---------|---------|----------------------------------------------------------------------------|
| voucher               | string  |         | Used for agent registration (will be prompted on first start)              |
| url                   | string  |         | The hashtopolis API endpoint (will be prompted on first start)             |
| token                 | string  |         | The access token for the API (sent by server on registration)              |
| uuid                  | string  |         | Unique identifier of the agent (generated on registration)                 |
| debug                 | boolean | false   | Enables debug output                                                       |
| allow-piping          | boolean | false   | Allows hashcat to read password candidates from stdin                      |
| piping-threshold      | integer | 95      | Restarts chunk in piping mode when GPU UTIL is below this value            |
| rsync                 | boolean | false   | Enables download of wordlists and rules via rsync                          |
| rsync-path            | string  |         | Remote path to hashtopolis files directory                                 |
| multicast-device      | string  | eth0    | Device which is used to retrieve UDP multicast file distribution           |
| file-deletion-disable | boolean | false   | Disable requesting the server for files to delete                          |
| file-deletion-interval| integer | 600     | Interval time in seconds in which the agent should check for deleted files |

### Debug example

```
{
  "url": "https://coray.org/htp-test/src/api/server.php", 
  "token": "7RNDqtnPxm",
  "uuid": "49dcd31c-3637-4f2a-8df1-b545202df5b3",
  "debug": true
}
```

### rsync

You need a user on the server which can automatically login (e.g. SSH keys) and has read access to the files directory of hashtopolis. On the client side you need rsync installed and set the following lines in your agent config.

```
  "rsync": true,
  "rsync-path": "user@yourserver:/path/to/hashtopolis/files"
```

### Multicast

In order to use the multicast distribution for files, please make sure that the agents and server are prepared according to this:https://github.com/s3inlc/hashtopolis-runner

## Hashcat Compatibility

The list contains all Hashcat versions with which the client was tested and is able to work with (other versions might work):

* 4.2.1
* 4.2.0
* 4.1.0
* 4.0.1
* 4.0.0

## Generic Crackers

This client is able to run generic Hashtopolis cracker binaries which fulfill the minimal functionality requirements, described [here](https://github.com/s3inlc/hashtopolis/tree/master/doc/README.md). An example implementation can be found [here](https://github.com/s3inlc/hashtopolis-generic-cracker)

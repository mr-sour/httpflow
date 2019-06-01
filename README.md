# httpflow

[![Build Status](https://travis-ci.org/six-ddc/httpflow.svg?branch=master)](https://travis-ci.org/six-ddc/httpflow)

![](https://github.com/six-ddc/httpflow/blob/master/demo.gif?raw=true)

## Installation

### MacOs

```bash
brew update
brew install httpflow
```

### Linux

* Install [zlib](http://www.zlib.net/), [pcap](http://www.tcpdump.org/), [pcre](http://pcre.org/)

```bash
## On CentOS
yum update
yum install libpcap-devel zlib-devel pcre-devel

## On Ubuntu / Debian
apt-get update
apt-get install libpcap-dev zlib1g-dev libpcre3 libpcre3-dev

## On Clear linux
#total over kill but it works
sudo swupd bundle-add os-clr-on-clr-dev
```

* Building httpflow

```bash
> git clone https://github.com/six-ddc/httpflow
> cd httpflow &&  make && make install
```

or directly download [Release](https://github.com/six-ddc/httpflow/releases) binary file.

## Usage

```
libpcap version libpcap version 1.8.1 -- Apple version 67.60.1
httpflow version 0.0.5

Usage: httpflow [-i interface | -r pcap-file] [-f packet-filter] [-u url-filter] [-w output-path]

  -i interface      Listen on interface
  -r pcap-file      Read packets from file (which was created by tcpdump with the -w option)
                    Standard input is used if file is '-'
  -f packet-filter  Selects which packets will be dumped
                    If filter expression is given, only packets for which expression is 'true' will be dumped
                    For the expression syntax, see pcap-filter(7)
  -u url-filter     Matches which urls will be dumped
  -w output-path    Write the http request and response to a specific directory

  For more information, see https://github.com/six-ddc/httpflow

```

* Capture default interface

```bash
> httpflow
```

* Capture all interfaces

```bash
> httpflow -i any
```

* Use the expression to filter the capture results

```bash
# If no expression is given, all packets on the net will be dumped.
# For the expression syntax, see pcap-filter(7).
> httpflow -f 'tcp port 80 and host baidu.com'
```

* Use the regexp to filter request urls

```bash
> httpflow -u '(google.com|httpbin.org)/.*/get'
```

* Read packets from file

```bash
# tcpdump -w a.cap
> httpflow -r a.cap
```

* Read packets from input

```bash
> tcpdump -w - | httpflow -r -
```

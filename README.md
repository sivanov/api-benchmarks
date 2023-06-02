# api-benchmarks
Rest API benchamraks and researches


## List with HTTP benchmarking tools

### Complite list with tools
https://github.com/denji/awesome-http-benchmark

### Autocannon
Notice: autocannon uses a single thread at 80% CPU load. For multi 
Github: https://github.com/mcollina/autocannon
An HTTP/1.1 benchmarking tool written in node, greatly inspired by wrk and wrk2, with support for HTTP pipelining 
and HTTPS. On my box, autocannon can produce more load than wrk and wrk2, see limitations for more details.

Instal via NPM like grlobal node modules:
```
npm i autocannon -g
```
exmple usage:
```sh
autocannon -c10 -d1 http://localhost:5000/api
```
result
```sh
Running 1s test @ http://localhost:5000/api
10 connections

┌─────────┬──────┬──────┬───────┬───────┬─────────┬─────────┬───────┐
│ Stat    │ 2.5% │ 50%  │ 97.5% │ 99%   │ Avg     │ Stdev   │ Max   │
├─────────┼──────┼──────┼───────┼───────┼─────────┼─────────┼───────┤
│ Latency │ 1 ms │ 3 ms │ 14 ms │ 17 ms │ 3.74 ms │ 3.57 ms │ 46 ms │
└─────────┴──────┴──────┴───────┴───────┴─────────┴─────────┴───────┘
┌───────────┬────────┬────────┬────────┬────────┬────────┬───────┬────────┐
│ Stat      │ 1%     │ 2.5%   │ 50%    │ 97.5%  │ Avg    │ Stdev │ Min    │
├───────────┼────────┼────────┼────────┼────────┼────────┼───────┼────────┤
│ Req/Sec   │ 2341   │ 2341   │ 2341   │ 2341   │ 2341   │ 0     │ 2341   │
├───────────┼────────┼────────┼────────┼────────┼────────┼───────┼────────┤
│ Bytes/Sec │ 461 kB │ 461 kB │ 461 kB │ 461 kB │ 461 kB │ 0 B   │ 461 kB │
└───────────┴────────┴────────┴────────┴────────┴────────┴───────┴────────┘

Req/Bytes counts sampled once per second.
# of samples: 1

2k requests in 1.03s, 461 kB read
```


### WRK
Under linux we can install with 
```sh
sudo apt-get install wrk
```
If by some reason you get error like this(fro example under Linux Mint 20.1):
```
Reading package lists... Done
Building dependency tree       
Reading state information... Done
E: Unable to locate package wrk
```
Next alternative variatn is to download source from Github and build program with short list of commands
Notice: required space during build:``` 6 010 items, totalling 516,3 MB```
Final program size will be around 4.4MB.
```sh
sudo apt-get install build-essential libssl-dev git -y 
git clone https://github.com/wg/wrk.git wrk 
cd wrk 
sudo make 
# move the executable, will be usable for all users
sudo cp wrk /usr/local/bin 
```
The /usr/local hierarchy is for use by the system administrator when installing software locally.

To check if program work run in terminal:
```
wrk --version
```

#### Example usage
In this example I am running a bench mark for 1 second, 
using 4 threads, and keeping 10 HTTP connections open.

```sh
wrk -t4 -c10 -d1 http://localhost:5000/api

Running 1s test @ http://localhost:5000/api
  4 threads and 10 connections
  Thread Stats   Avg      Stdev     Max   +/- Stdev
    Latency     3.39ms    5.04ms  43.40ms   91.97%
    Req/Sec     0.85k   258.48     1.37k    72.50%
  3395 requests in 1.00s, 653.14KB read
Requests/sec:   3380.06
Transfer/sec:    650.26KB
```

### WRK 2 - Experimental
Notice: WRK 2 is currently in experimental/development mode, and may well be merged into wrk in the future if others see fit to adopt it's changes.
https://github.com/giltene/wrk2


### AB-Apache Benchmakr

#### Installation
```sh
sudo apt-get update
# Install apache2 utils package to get access to Apache Bench.
apt-get install apache2-utils
# check installed version 
ab -V
```

Example usage.:
-c is the concurrency and denotes the number of multiple requests to perform at a time. Default is one request at a time.
-t is time duration of test in this example 1 second 
```sh
ab -c 10 -t 1 http://localhost:5000/api
```

Result
```sh
This is ApacheBench, Version 2.3 <$Revision: 1843412 $>
Copyright 1996 Adam Twiss, Zeus Technology Ltd, http://www.zeustech.net/
Licensed to The Apache Software Foundation, http://www.apache.org/

Benchmarking localhost (be patient)
Finished 1686 requests


Server Software:        
Server Hostname:        localhost
Server Port:            5000

Document Path:          /api
Document Length:        23 bytes

Concurrency Level:      10
Time taken for tests:   1.000 seconds
Complete requests:      1686
Failed requests:        0
Total transferred:      219700 bytes
HTML transferred:       38870 bytes
Requests per second:    1686.00 [#/sec] (mean)
Time per request:       5.931 [ms] (mean)
Time per request:       0.593 [ms] (mean, across all concurrent requests)
Transfer rate:          214.55 [Kbytes/sec] received

Connection Times (ms)
              min  mean[+/-sd] median   max
Connect:        0    0   0.3      0      10
Processing:     1    6   2.9      5      26
Waiting:        0    3   2.4      3      26
Total:          1    6   2.9      5      26

Percentage of the requests served within a certain time (ms)
  50%      5
  66%      6
  75%      7
  80%      7
  90%     10
  95%     12
  98%     15
  99%     16
 100%     26 (longest request)
```

### Loadtest

[NPM page](https://www.npmjs.com/package/loadtest)

[Github page](https://github.com/alexfernandez/loadtest)

Install globally as root:
> npm install -g loadtest
# How To

This command will run until you press 'ctl-c' ...

```bash
$ ab -r -t 20 http://192.168.122.83:30030/
This is ApacheBench, Version 2.3 <$Revision: 1903618 $>
Copyright 1996 Adam Twiss, Zeus Technology Ltd, http://www.zeustech.net/
Licensed to The Apache Software Foundation, http://www.apache.org/

Benchmarking 192.168.122.83 (be patient)
Completed 5000 requests
Completed 10000 requests
Completed 15000 requests
Completed 20000 requests
Completed 25000 requests
^C

Server Software:        nginx/1.29.3
Server Hostname:        192.168.122.83
Server Port:            30030

Document Path:          /
Document Length:        615 bytes

Concurrency Level:      1
Time taken for tests:   11.300 seconds
Complete requests:      26012
Failed requests:        0
Total transferred:      22058409 bytes
HTML transferred:       15997380 bytes
Requests per second:    2302.01 [#/sec] (mean)
Time per request:       0.434 [ms] (mean)
Time per request:       0.434 [ms] (mean, across all concurrent requests)
Transfer rate:          1906.38 [Kbytes/sec] received

Connection Times (ms)
              min  mean[+/-sd] median   max
Connect:        0    0   0.1      0      18
Processing:     0    0   0.3      0      26
Waiting:        0    0   0.3      0      26
Total:          0    0   0.3      0      27

Percentage of the requests served within a certain time (ms)
  50%      0
  66%      0
  75%      0
  80%      1
  90%      1
  95%      1
  98%      1
  99%      1
 100%     27 (longest request)
```

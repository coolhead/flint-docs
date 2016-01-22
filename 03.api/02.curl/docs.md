---
title: Using cURL
taxonomy:
    category: docs
---

## Using the cURL tool
To know about cURL command line tool, please refer [http://curl.haxx.se/docs/httpscripting.html](http://curl.haxx.se/docs/httpscripting.html)

### Run Flintbit Async

``` bash
curl -X POST -H "Content-Type: application/json" -H "x-flint-username: admin" -H "x-flint-password: admin123" -d '{"name":"adam"}' 'http://localhost:3501/v1/bit/run/example:hello.rb'
```

``` bash
curl -X POST -H "Content-Type: application/json" -H "flint-key: <your flint key>" -d '{"name":"tom"}' 'http://localhost:3501/v1/bit/run/example:hello.rb'
```


### Run Flintbit Sync

``` bash
curl -X POST -H "Content-Type: application/json" -H "x-flint-username: admin" -H "x-flint-password: admin123" -d '{"name":"adam"}' 'http://localhost:3501/v1/bit/run/example:hello.rb/sync'
```
``` bash
curl -X POST -H "Content-Type: application/json" -H "flint-key: <your flint key>" -d '{"name":"tom"}' 'http://localhost:3501/v1/bit/run/example:hello.rb/sync'
```

### Run Flintbit Sync with timeout

``` bash
curl -X POST -H "Content-Type: application/json" -H "x-flint-username: admin" -H "x-flint-password: admin123" -d '{"name":"adam"}' 'http://localhost:3501/v1/bit/run/example:hello.rb/sync/60000'
```
``` bash
curl -X POST -H "Content-Type: application/json" -H "flint-key: <your flint key>" -d '{"name":"tom"}' 'http://localhost:3501/v1/bit/run/example:hello.rb/sync/60000'
```


### Get Flintbit job result
``` bash
curl -X GET -H "Content-Type: application/json" -H "x-flint-username: admin" -H "x-flint-password: admin123" 'http://localhost:3501/v1/bit/result/job-e381654d-065f-48f3-bbd4-f3420da18495'
```

``` bash
curl -X GET -H "Content-Type: application/json" -H "flint-key: <your flint key>" 'http://localhost:3501/v1/bit/result/job-e381654d-065f-48f3-bbd4-f3420da18495'
```

---
title: REST APIs
taxonomy:
    category: docs
---

REST API's are gateways to Flint which provide an interface to run flintbits from external systems.
This is the reference document for the REST API and resources provided by Flint.


## Structure of REST URL

To use REST API, external systems will make an HTTP request and parse the HTTP response.

Flint's REST API's use JSON or XML as a communication medium for standard HTTP Methods - Get, Post, Put and Delete.

Structure of REST URI's is as follows:

``` http
http://hostname:port/v1/bit/run/flintbox_name:flintbit_name

# Example
http://localhost:3501/v1/bit/run/mybox:hello.rb

```
| Parameter | Description | required |
| ------ | ----------- |
| hostname | Hostname of the server on which Flint is installed ( default is localhost ) | true |
| port | REST API Port Number ( default is 3501 ) | true |
| flintbox-name | Name of the Flintbox ( Git repository ) recently created to store all the Flintbits and configured it ( mybox ) | true |
| flintbit-name | Name of the Flintbit created and added to the Flintbox ( hello.rb ) | true |

<br>
## Flint REST API Authentication

### Set username and password in HTTP header

You can set **x-flint-username** and **x-flint-password** HTTP headers in request with valid username and password.

``` http
x-flint-username:admin
x-flint-passowrd:admin123
```
### Set Flint Key in header

You can obtain valid flint key for your account from the UI console or ask Flint Admin to give it to you.
You can set **flint-key** header with valid key.

``` http
flint-key:v0zAJsljulCDY2%2BMZ3XmFRJZNCIt3r7Kb4jYbSaQWQsLqU6nC1ol6YOuJEQ8VLf0
```

### Set Flint key in URL as parameter
If your REST call does not support adding headers (like github hook). You can also set flint-key as URL parameter for all the URL.

``` http
http://localhost:3501/v1/bit/run/mybox:hello.rb?flint-key=FLINT_KEY
```

<br>
## Content-Type HTTP Header

Apart from the authentication headers flint also requires **Content-Type** header with valid input document type. The valid values are application/json and application/xml.

``` http
Content-Type:application/json
### OR ###
Content-Type:application/xml
```
>>>> If flint do not find **Content-Type header** it will construct JSON using request body and pass it to flintbit.

<br>
## Actions

### Run Flintbit Asynchronously [Recommended]

Runs a flintbit in asynchronous way. Post body will have a valid JSON or XML document. Default timeout of 6000 ms will be used.

``` http
POST http://localhost:3501/v1/bit/run/mybox:hello.rb
```
See [REST API response](#rest-api-response) section for output parameters.

### Run Flintbit Synchronously

Runs a flintbit in synchronous way. Post body will have a valid JSON or XML document. Default timeout of 6000 ms will be used.

``` http
POST http://localhost:3501/v1/bit/run/mybox:hello.rb/sync
```
See [REST API response](#rest-api-response) section for output parameters.

### Run Flintbit Synchronously with Timeout

Runs a flintbit in synchronous way with user specified timeout. Post body will have a valid JSON or XML document.

Flint does **not guarantee** that the flintbit job will be complete in specified timeout. If the timeout value is reached it will return back the status of the job. You can always use Result API (discussed later in this document) to retrieve result at a latter point of time.

``` http
POST http://localhost:3501/v1/bit/run/mybox:hello.rb/sync/60000
```
See [REST API response](#rest-api-response) section for output parameters.

### Get Flintbit run Result

You can get run result of the job triggered asyncronusly or timed out before the run is complete.

``` http
GET http://localhost:3501/v1/bit/result/job-e381654d-065f-48f3-bbd4-f3420da18495
```
where, job-e381654d-065f-48f3-bbd4-f3420da18495 is the job id from the flintbit run request.

See [REST API response](#rest-api-response) section for output parameters.

<br>
## REST API Response

In case of **synchronous requests** an **output** object is set which is the actual output of flintbit. A meta object is always returned back along with the output of the flintbit. The meta object gives you additional information about the flintbit job you are running.

In case of **asynchronous** request only meta object is returned. You can query for the status of job using [result api](#get-flintbit-run-result) which is described above in this document.

### Response parameters

| Parameter | Description |
| ------ | ----------- |
| job-id | Job id is unique identifier of the request being submitted |
| exit-code |	Exit status code of the job run request. Zero value indicates success , non zero value indicates error|
| context	Fully | qualified name of the flintbit that was run. Example - mybox:hello.rb |
| message |	Human readable job execution status messages. This can be a status or error message |
| status |	Status of the job run request. Possible status values are **submitted**, **running**, **complete**, **aborted**, **error**
| timeout |	Time out of the job run request
| timestamp |	Time at which the job was executed
| content-type |	Content type of the request being submitted. This can be application/xml or application/json|

#### Example JSON
``` json
{
  "meta": {
    "job-id": "job-209bc504-887a-4614-b16d-480284364caa",
    "exit-code": 0,
    "context": "mybox:hello.rb",
    "message": "success",
    "timeout": 60000,
    "timestamp": 1435923867907,
    "status": "complete",
    "content-type": "application/json"
  },
  "output": {
    "message": "Welcome to Flint !!"
  }
}
```
#### Example XML
``` xml
<?xml version="1.0" encoding="UTF-8" standalone="no"?>
<flint>
    <meta>
        <job-id>job-aab20c62-9460-439f-951d-7bcbe48a61fd</job-id>
        <exit-code>0</exit-code>
        <context>mybox:hello.rb</context>
        <content-type>application/xml</content-type>
        <message>success</message>
        <timeout>60000</timeout>
        <timestamp>1435927066310</timestamp>
        <status>complete</status>
    </meta>
    <output>
        <message>Welcome to Flint !!</message>
    </output>
</flint>
```

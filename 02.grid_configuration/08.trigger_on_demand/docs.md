---
title: Trigger on Demand [TOD]
taxonomy:
    category: docs
process:
	twig: true
---


You can trigger Flintbits using Flint's TOD. Depending on your application workflow, necessary inputs can be provided to Flintbits which help interact with connectors or listeners. Thus, running a Flintbit from TOD will not only trigger the workflow but also help us observe the response for the same with appropriate logs.

Trigger On Demand is all about - Running a Flintbit, displaying output of a Flintbit in its well structured raw form and monitoring logs.


### To Run a Flintbit


#### Run Mode

Similar to connectors/listeners, Flintbits also, can be executed in a synchronous and asynchronous manner.

* Synchronous : Execute Flintbits in a synchronous way. Default timeout is of 60,000 ms.
* Asynchronous : Execute Flintbits in an asynchronous way straight away returning the meta object, without waiting for the job to complete.

##### Name

This field is the Flintbit name along with the Flintbox name in whcih it resides. All the Flintboxes by default reside in the Flintbox directory. Naming convention is as followed :

```
flintbox-name:flintbit-name
```

where, a **colon ( : )** represents the path change.

##### Example

Generally ( a non-nested directory structure ),

``` http
example:hello.rb  
```
where, a colon ( : ) represents the path change.

In case of a nested directory structure,

``` http
http:my-requests:http_get.rb
```

A nested directory structure representing the following,each separated by a colon ( : ) :

```
-flintbox
  -http
    -my-requests
      -http_get.rb  
```
##### Input Type

Used to specify the type of input documents for a Flintbit. Valid input document types are :

* JSON ( application/json )
* XML ( application/xml )

##### Timeout

Used to specify the timeout for a Flintbit's execution in a synchronous mode. Default timeout is 60,000 ms.

##### Input( XML/JSON )

Used to specify a JSON Object in case of JSON type input document or a XML document in case of XML type input document. The data in these documents are actual inputs to your Flintbits.

![tod-run-flintbit](tod-run-flintbit.png)

<br>
### Output

Here, you can view a well structured response of your Flintbit. All the parameters of the response stand out with their corresponding values. Parameters are separated out perfectly so you can study values which are significant to your debugging.

![tod-output](tod-output.png)

<br>
### Raw

The raw view is just a big text area with the Flintbit response body. A minified version of the JSON Object or XML document will be displayed depending on the type of input supplied.

![tod-raw](tod-raw.png)

<br>
### Logs

Logs will help you walk-through your Flintbit processing in detail. With various logging levels and all possible errors captured, Flint's logging will make it easy to debug, identify and resolve errors/failures. It is a good practice to start logs before running any Flintbit.

![tod-logs](tod-logs.png)

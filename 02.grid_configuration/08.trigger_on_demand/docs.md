---
title: Trigger on Demand [TOD]
taxonomy:
    category: docs
process:
	twig: true
---


Flint's TOD (Trigger on Demand) is an user interface that provides the capability to trigger and debug Flintbit executions. Depending on the workflow, necessary inputs are provided to Flintbits which then interact with connectors/listeners. 

Thus, running a Flintbit from TOD will not only trigger the workflow but also help us observe the response for the same with appropriate logs.

Trigger On Demand is all about - running a Flintbit, displaying output of a Flintbit in its well structured raw form and monitoring logs.


### To Run a Flintbit


#### Run Mode

Similar to connectors/listeners, Flintbits also, can be executed in a synchronous and asynchronous manner.

* Synchronous : Execute Flintbits in a synchronous way. Default timeout is of 60,000 ms.
* Asynchronous : Execute Flintbits in an asynchronous way straight away returning the meta object, without waiting for the job to complete.

##### Name

This field is the Flintbit name along with the Flintbox name in which it resides. By default, all the Flintbits reside in the Flintbox directory. Naming convention is as followed :

```
flintbox-name:flintbit-name
```

where, a **colon ( : )** represents the path change.

For example, a non-nested directory structure looks like:

``` http
example:hello.rb  
```
Whereas, a nested directory structure looks like:

``` http
http:my-requests:http_get.rb
```

A nested directory structure representing the following, each separated by a colon ( : ) :

```
-flintbox
  -http
    -my-requests
      -http_get.rb  
```
##### Input Type

This is used to specify the type of input documents for a Flintbit. Valid input document types are :

* JSON ( application/json )
* XML ( application/xml )

##### Timeout

This is used to specify the timeout for a Flintbit's execution in a synchronous mode. Default timeout is 60,000 ms.

##### Input( XML/JSON )

This is used to specify:

- a JSON Object in case of JSON type input document
- a XML document in case of XML type input document

The data in these documents are actual inputs to your Flintbits.

![tod-run-flintbit](tod-run-flintbit.png)

<br>
### Output

Here, you can view a well structured response of your Flintbit execution. All the parameters of the response stand out with their corresponding values. Parameters are separated out perfectly so you can study values which are significant to your debugging.

![tod-output](tod-output.png)

<br>
### Raw

The raw view is just a big text area with the Flintbit response body. A minified version of the JSON Object or XML document will be displayed depending on the type of input provided.

![tod-raw](tod-raw.png)

<br>
### Logs

Logs will help you walk-through your Flintbit processing in detail. With various logging levels and all possible errors captured, Flint's logging makes it easy to debug, identify and resolve errors/failures. It is a good practice to start logs before running any Flintbit.

![tod-logs](tod-logs.png)

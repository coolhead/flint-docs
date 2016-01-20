---
title: Flintbit Functions
taxonomy:
    category: docs
---

## Flintbit Objects and Functions

Flintbits are nothing, but scripts written in Ruby / Groovy.

Imagine a flintbit script as a normal script you would write to automate any task. You would give an input to the script, typically using a command line and then the script will do some processing and produce an output.

Flintbit behaves in a similar way. The difference here is we have some simple functions that help us get input, which can be JSON or XML, we have functions to help you perform some useful tasks and then finally to produce an output.

> Flint automatically injects these objects to your flintbits. You don't have to declare or include anything to use them.

## Input
Input object is used when you want to read JOSN/XML input which are supplied to the flintbit at runtime.

#### Get a parameter

``` ruby
# for ruby
@input.get("name")
```
``` java
// for groovy
input.get("name")
```
It will return you values of parameters/elements depending on the JSON/XML document you have supplied as input: String, Integer, Float, List or another JSON or XML object.

#### Get a parameter using path
Many times the JSON/XML document you have supplied as input to flintbit is complex. So to retrieve values from it, we can also use JSON path or XPATH. This depends upon the content-type of the input. If the input document is of the type JSON it uses JSON path and if its a XML document it uses XPATH.

``` ruby
# for ruby
@input.path("$.name")
```
``` java
// for groovy
input.path("$.name")
```
It will return you values of parameters/elements depending on the JSON/XML document you have supplied as input: String, Integer, Float, List or another JSON or XML object.

#### Get raw input
To get raw JSON/XML input data.
``` ruby
# ruby
@input.raw()
@input.to_s
```
``` java
// groovy
input.raw()
input.toString()
```
It returns a string representation of your JSON/XML input document.

#### Get Job Meta information
Input object also tells us more about the job being run

| Function | Description |
| ------ | ----------- |
|input.jobid()|	Job id of the request being submitted|
|input.username()|	Username of the account which triggred the job|
|input.email()|	Email address of the account which triggred the job|


<br>
## Log

You can add log statements within your flintbit using the “log” object. It allows you to report and persist trace, debug, info, warning,fatal and error information ( e.g. runtime statistics ) so that the information can later be viewed and analyzed.
``` ruby
# ruby
@log.info("this is an info log")
@log.error("this is an error log")
@log.warn("this is an warning log")
@log.debug("this is an debug log")
```

``` java
// groovy
log.info("this is an info log")
log.error("this is an error log")
log.warn("this is an warning log")
log.debug("this is an debug log")
```
<br>
## Output
Once you are done with your task or logic, you want to set an output to the script. This is done using the “output” object.

#### Set a parameter

You can use the “set” method to set parameter. It excepts key and value.

``` ruby
# ruby
@output.set("name","Tom")
```
``` java
// groovy
output.set("name","Tom")
```

#### Set raw XML element /JSON document
You can use the “setraw” method to set an raw xml/json depending on the content-type you are dealing with. It excepts key and raw XML/JSON string as value.
``` ruby
# ruby
@output.setraw('name','{"name":"tom"}')
```
``` java
// Groovy
output.setraw("name","<name>tom</name>")
```
#### Remove a parameter

You can use the “remove” method to remove an already set parameter. It excepts key to remove.

``` ruby
# ruby
@output.remove("name")
```
``` java
// groovy
output.remove("name")
```

<br>
## Call


#### Call Connector
Connector calls are to perform operations on another system.

Connectors are called using the `call.connector()` function. You must supply a valid connector name that you have configured on Flint Platform (see grid configuration). You can pass parameters using the “set” method. The `sync()` and `async()` method executes the connector call synchronously or asynchronously. You will get a response object in return. You must check the corresponding connector.

| Code | Description |
| ------ | ----------- |
|`response = @call.connector("connector_name").set("key","value").sync`|	Call connector syncronously|
|`@call.connector("connector_name").set("key","value").async`|	Call connector asyncronously. Fire and forget|


#### Call Flintbit

Flintbits are called using the “call.bit()” function. You must supply a valid fully qualified flintbit name. Make sure you have enables the corresponding flintbox on flint platform. You can pass parameters using the “set” method. The `sync()` and `async()` method executes the flintbit call synchronously or asynchronously. You will get a response object in return.

| Code | Description |
| ------ | ----------- |
|`response = @call.bit("example:hello.rb").set("key","value").sync`|	Call flintbit syncronously|
|`@call.bit("example:hello.rb").set("key","value").async`|	Call flintbit asyncronously. Fire and forget|

#### Response object

A Response object is always returned back while executing a connector or for a flintbit call. The response object gives you additional information about the flintbit job or connector call you are running. Following are the attributes of a response object.

| Code | Description |
| ------ | ----------- |
| `response.jobid()` | Job id is unique identifier of the request being submitted
| `response.exitcode()` |	Exit status code of the job run request. Zero value indicates success , non zero value indicates error
| `response.context()` |	Fully qualified name of the flintbit that was run. Example - mybox:hello.rb
| `response.message()` |	Status of the job run request. Possible status that may appear submitted, running, complete, aborted, error
| `response.status()`	| status of the job run request. This can be submitted, running, complete, aborted, error
| `response.timeout()` | Time out of the job run request

<br>
## Config

Global and local configuration can be accessed via the `@config` object. you can add remove values from it using the console (see grid configuration).

A local configuration belongs to the “local.conf” file which you can create in your flintbox repository. This file must be present in the root of flintbox repository.

You can add remove values from it by editing the file. It follows simple and flexible HOCON format


| Code | Description |
| ------ | ----------- |
| `@config.global("aws.username")` | Get Global configuration |
| `@config.local("aws.username")` |	Get local configuration |


<br>
## Util
Utility object gives you some useful functions to save your time.

| Code | Description |
| ------ | ----------- |
| `name = @util.json('{"name":"tom"}').get("name")` | Parse raw JSON string |
| `name = @util.xml("<info><name>tom</name></info>").path("/info/name/text()")` |	Parse raw XML string |

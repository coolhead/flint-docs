---
title: Terminology
taxonomy:
    category: docs
---
![how_it_works](how_it_works.png)

## Flintbox

> Flintbox is a collection of similar Flintbits stored in the git repository

Flintbox is a git repository which contains or packages the Flintbits (workflows written in Ruby or Groovy). The collection of similar Flintbits packaged within the git repository or Flintbox. 

Flintbox can be deployed independently and are versioned within the git repository.


## Flintbit

> ruby or groovy scripts developed and packaged inside Flintbox

Flintbit is a ruby or groovy script, which contain the business logic. It uses 'flintbit functions' to get input, call connectors or to call or trigger other Flintbits.

Flintbits accepts JSON as input and returns JSON in output. All Flintbits are accessible via RESTful APIs, hence expose them as micro-services.


## Flintbit objects and functions

> objects and functions that are used to interact with Flint from your scripts

Flintbit functions those are readily available in all the Flintbits.

They are used to:
* Read JSON or XML input. e.g. `@input.get("name")`
* Log messages to log file and to console. e.g `@log.info("some message")`
* Call connectors and pass arguments to it. e.g. `@call.connector("connector_name")`
* Call/Run other flintbits and pass input to them. e.g. `@call.bit("example:hello.rb")`
* Set output of the flintbit. e.g `@output.set("message","hello")`

For list of objects and functions that flint provides see [Flintbit functions](../flintbit_functions) section.

## Flint Job

> Each Flintbit execution is a job with a unique job-id


## Flint WorkNode

> Instance of Flint running on physical or virtual server


## Flint Grid

> A collection of one or more Flint worknodes collaboratively forms a high-available and scalable grid


## Connectors

> Flint components which are designed to integrate with external systems for desired actions/tasks.

Connectors are used to communicate with the external world. For the communication to take place, connectors are configured on Grid nodes and Flintbits are used to call a connector, thus accomplishing the purpose of a connector and fulfilling your needs.

Connectors are configured on Flint work nodes using flint console.

## Listeners

> Flint components that listen or monitors external systems for incomings events/messages.

Listeners listen to events from external system. For example emails arriving at a mail box or message arriving at MQTT topic. Listeners trigger configured Flintbit with received event as an input to that Flintbit.

Listeners are configured on Flint worknodes using Flint console.

## Schedules

> Enables Flint to design and perform scheduled execution of Flintbits


## Global Config

> Configuration which is available to all the Flintbox and Flintbits deployed on the grid

Parameters declared in Global Configuration, are visible to all the Flintbox thereby being accessible to all the Flintbits. Global Config help you to avoid hard-coded variables in your Flintbits.

You can Add/update Global config form Flint Console.

Global Config can be used for:
* Additional credentials that might be associated with your applications
* Remote Server configurations
* Directoy/File locations
* **Parameters which needs to be quickly changed over time**

## Local Configuration

> Configuration which is available only to the specific Flintbox and Flintbits in which it is defined.

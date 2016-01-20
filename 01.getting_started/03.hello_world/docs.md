---
title: Hello World
taxonomy:
    category: docs
---

## Kick-start with 'Hello World'

To get started with Flint, we have defined a usual "hello world" example.

This guide assumes that you have already installed flint locally on your workstation.


## Create your first Flintbox

#### What is a Flintbox?

Flintbox is a git repository location which contains or hold all the flintbits (workflows written in Ruby or Groovy).

> flintbox = git repository

In production or remote flint deployment, flintbox are always cloned from git repository into the 'flintbox' directory. In development setup and when running flint locally, you can directly open and edit them in your favorite text editor.

#### Create Flintbox

We will create a flintbox named 'mybox' under the 'flintbox' directory.

To create a Flintbox-
* Navigate to flint-x.x.x.x ( flint installation directory )
* Navigate to flintbox directory
* Create a directory named 'mybox' to store flintbits.
* This can be performed by executing the below commands on a new terminal.

``` bash
$ cd flint-x.x.x.x
$ cd flintbox
$ mkdir mybox
```

>>>>> Newly created Flintbox will also appear on Flint Console afetr the Git repository for mybox is configured. For this, refer sections Git repository for Flintbox and Configure Flintbox with Flint in this document.

## Create your first Flintbit

#### What is a Flintbit?

Flintbit is a ruby or groovy script, which contain your business logic. It uses 'flitbit functions' to get input, call connectors and other flintbits and finally to set output.

All flintbits are accessible via RESTful APIs making them micro-services.

> flintbit = ruby or groovy scripts stored inside flintbox

#### Create Flntbit

To create a flintbit, Navigate to mybox directory using your favorite code editor.

Create a ruby or groovy flintbit under 'mybox' directory. You can copy paste the following code :

``` ruby
# for hello.rb
@log.info("Welcome to flint!")
@output.set("message","Hello World!")
```
``` java
// For hello.groovy
log.info("Welcome to flint!")
output.set("message","Hello World!")
```

#### Flintbit reference path or flintbit name
When you want to refer your flintbit in flint, you have to use flint's path convention. This is very simple, Just remember folders and flintbits are separated by **colon (:)** operator.

Following example shows the folder structure and path to refer the flintbits
```
flintbox
├── mybox             # our new flintbox
    ├── hello.groovy  # mybox:hello.rb
    └── hello.rb      # mybox:hello.groovy
```

## Run the Flintbit

#### Open TOD Console
Open the flint console in your browser and navigate to Trigger on Demand [TOD] screen

![tod_link](tod_link.png)

#### Enable Logs
Before ruuning our flintbit we will enable logs so that we can see live logs from the running script. This is very useful when developing and debugging flintbits.

![start_logs](start_logs.png)

#### Run flintbit hello.rb or hello.groovy
Now that the logs are enabled lets run our flintbit
![run_flintbit](run_flintbit.png)

Upon execution of Flintbit logs as below will be displayed
![see_logs](hello_logs.png)

For more information on using trigger on demand console see [Trigger on Demand](../../grid_configuration/trigger_on_demand)

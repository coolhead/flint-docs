---
title: Release Notes
taxonomy:
    category: docs
---
## Flint Platform Release Notes

### Version : Flint v0.28.0.0-beta
Release Date: 5 October 2015

* Ability to configure grid from Flint console UI
* UI and Usability Improvements
* Base platform improvements
* Change in Grid configuration structure
* Ability to take snapshot of Grid configuration
* Performance and Stability improvements

### Version : Flint v0.27.0.2-beta
Release Date: 4 September 2015

* Bug Fixes
* Performance and Stability improvements
* Listener HA - failure detection and redeployment

### Version : Flint v0.27.0.1-beta
Release Date: 27 August 2015

> This is the first public beta release for Flint IT Automation platform.

#### Features

* Run Ruby and Groovy jobs
* REST API to trigger jobs
* Administration console
* Git version control integration
* Deploy/undeploy connectors and listeners
* Deploy/undeploy of Flintbox (Git repos containing workflow scripts)
* Cron expression based scheduling of jobs
* Call connectors from flintbits (ruby and groovy scripts)
* Directly pull flintboxes and grid configuration from remote git repos
** List of connectors**
* SSH Connector - v0.1.0.1
* File Connector - v0.1.0.0
* DB Connector - v0.1.0.1
* SMTP Connector - v0.1.0.0
* Windows Connector - v0.1.0.0
* HTTP Connector - v0.1.0.0
* AWS-EC2 Connector - v0.1.0.0
** List of Listeners**
* IMAP Listener- v0.1.0.0

#### Dependencies
Oracle Java Development Kit - 1.8.0_51

#### System Requirements

**Minimum:**
* Dual Core CPU
* 4 GB RAM
* 10 GB Hard Disk Space
* Recomended:
* Quad Core CPU
* 8 GB RAM
* 20 GB Hard Disk Space

#### Known Issues

* IMAP listener: Number of listeners listening for incoming emails depend upon the number of instances of connector. We must only start one instance of this connector.
* For windows: Inconsistency in disabling flintbox in case one of the flintbit from it is in use or running.
* IMAP listener do not support Yahoo.com and Outlook.com mail server yet.
* SMTP connector does not support Outlook mail server.
* DB connector does not support generation of dynamic jdbc-url for the databases other than Mysql, so in case of other databases need to give jdbc-url in connector configuration or request parameter. Connection pooling is coming soon.
* `output.remove()` do not work in case of XML
* `output.set()` can not handle null values in case of XML


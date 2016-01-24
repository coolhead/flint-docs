---
title: Principles of Flint
taxonomy:
    category: docs
---
### Automation as Code
> Identify, Track, Audit & debug changes in your automation.

In Flint, all the automation you do is represented as code. This code could be Ruby and Groovy scripts; we call them Flintbits.
Working with automation as code gives you numerous advantages such as-

* Identifying the changes as it happens in the automation environment.
* Track the changes via review before deployment.
* Audit the changes.
* Debug or rollback them by precisely pointing to the version.
* The Flintbits developed and packaged within the git repository, we call it Flintbox.

Flint pulls or fetches Flintbox (aka GIT repositories) with all its configurations from GIT servers (public or private) and deploy it on flint-grid.

### Micro-services Architecture
> Get full advantage for micro-services pattern

Each Flintbox can be
* Quickly deployed
* Can be deployed
* Is a small collection of related services
* Versioned separately

Each Flintbit is
* Available as REST service
* Monitored: health, distributed logging, statistics
* Uses async communication
* Prevents cascading failure and be fault tolerant
* Uses JSON and messaging for communication

### Generic Technologies
> Concentrate on your workflows and not on technologies.

Flint is designed so that automation can be developed leveraging skills of simple scripting. Flint has been kept simple, and does not demand to learn new DSLs/development tools. Provided with very simple, minimum, easy to remember functions to interact with Flint platform from or within the Flintbits.

### Resilient Platform
> Run your automation workflows with confidence.

Flintbits are run and managed centrally on the grid. These are not scattered across your infrastructure which quite a problem to manage. Once you deploy Flintbits and Flintbox on the grid, the automation becomes scalable, highly available, fault tolerant and RESTful.

It's like your generic automation scripts wearing a jetpack!

### API-Centric
> Automate and integrate with other systems with ease

In Flint, everything has a REST API. So it is easier for other applications to interact with Flint platform and vice-a-versa. The Flintbits you design and deploy on Flint grid, automatically becomes available and exposed via REST APIs.

### Modular & Shareable
> Easily reuse your automation code.

In Flint, modularity is king. Develop and package the Flintbits uniquely developed for a logical operation or a function. And, then these Flintbits can be called or triggered from another Flintbits providing reusability of Flinbits and pre-built functions.

For example, an “aws-ec2” Flintbox can have Flintbit like ‘create_server.rb’. This is for a particular operation of creating a new EC2 server instance. 

Another Flintbit such as “app-deploy.rb” can use this “aws-ec2:create_server.rb” Flintbit to reuse functionality of creating a new AWS instance for deployment.

Isn’t that awesome?! You can compose new Flintbits with the use of existing Flintbits and keep on developing new automation on top of existing automation!

The best part is, you can share these Flintbox with your colleagues, friends or with the community on github/bitbucket. We are soon bringing in an open central registry where you can register your Flintbox and share them across.

### Immutable via Version
> Easily transition between versions. Rollback if anything goes wrong.

Immutability is a wonderful concept in the software domain. Immutability means “unable to be changed”.

We envision immutability as version control systems, once a commit is made it cannot be changed. All the grid configuration, Flintbox are stored or placed in-actual GIT repositories.

This provides a benefit of fluently changing versions of grid configuration and Flintbox, so these can be tracked precisely for the changes and modifications. We can as well rollback the version if any new deployment version goes sour.

---
title: Principles of Flint
taxonomy:
    category: docs
---
### Automation as Code
> Identify, Track, Audit & debug changes in your automation.

In flint all the automation you do is represented as code. This code could be Ruby and Groovy scripts, we call them flintbits. Writing Automation as code give you numerous advantages.

* Identifying the changes happening to automation infrastructure.
* Track the changes via review before deployment.
* Audit the changes.
* Debug or rollback them by exactly pointing to the version.
* The flintbits you design are packaged within GIT repository, we call it flintbox.

Flint pulls or fetch flintbox (aka GIT repositories) with all its configurations from GIT servers (public or private) and deploy it on flint-grid.

### Generic Technologies
> Concentrate on your workflows and not on technologies.

We have designed flint in such a way that you can use your existing knowledge of scripting which you have acquired over the years.

Flint has been kept simple, and you need not to learn new DSLs/development tools just to use flint or for your automation. Provided with very simple, minimum, easy to remember functions to interact with flint platform from within your flintbits.

### Resilient Platform
> Run your automation workflows with confidence.

Flintbits are run and managed centrally on the grid. They are not scattered across your infrastructure which quite a problem to manage. Once you deploy flintbits and flintboxes on the platform flint makes them Scalable, Highly available, Fault tolerant and RESTful.

Its like your generic automation scripts wearing a jetpack!

### API Centric
> Automate and integrate with other systems with ease

In flint everything has an REST API. So it is easier for other applications to interact with flint platform and vice-a-versa.

You can automate each and every aspect of flint platform using APIs. The flintbits you design and deploy on flint-grid, automatically becomes available via the REST APIs.

### Modular & Shareable
> Easily reuse your automation code.

In flint modularity is king! Develop and package your flintbits specific to a function. Then you can compose the other flintbits which can re-use those flintbits for specific function/s.

For example, an “aws-ec2” flintbox can have flintbit like ‘create_server.rb’. This is to create a new EC2 server instance. The flintbit such as “app-deploy.rb” can use this “aws-ec2:create_server.rb” flintbit to create a new AWS server for deployment.

Isn’t that awesome?! You can compose new flintbits using your existing flintbits and keep on developing new automation on top of existing automation!

The best part is, you can share these flintboxes with your colleagues, friends or with the community on github/bitbucket. We are soon bringing in an open central registry where you can register your flintboxes and share them with the world.

### Immutable via Version
> Easily transition between versions. Rollback if anything goes wrong.

Immutability is a wonderful concept in software domain. Immutability means “unable to be changed”.

We envision immutability as Version control systems, once a commit is made it cannot be changed. In flint all the grid configuration, flintboxes are in-actual GIT repositories.

The benefit of this is that you can fluently change versions of grid configuration and flintboxes, can track exactly what has changed and who did the modifications. You can rollback the version if any new deployment version goes sour.

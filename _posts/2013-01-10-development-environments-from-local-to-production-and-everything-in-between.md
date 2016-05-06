---

title: Development Environments
description: "From local to production and everything in-between"
tags: [tutorial, dev, prod, fut, sit, ci, staging, environments]
comments: true
image:
  feature: texture-feature-01.jpg
---

Within every enterprise development company, whether it be a SMB or a large multinational company, the makeup of its development environment is crucial to the quality and success of a project.<br><br>
Here I will detail the development environments any company should implement to improve their life cycle process:<br><br>
**Sandbox**  
Local setup of a development environment on your own local machine, the project is sandboxed within the confines for your hard drive, any code changes can be deployed locally to test before checking in.<br><br>
**Build Server**  
The CI (continuous integration) server is the deployment target for your project. Generally polling your code base for changed and kicking off a build when a change is detected, this allows for near immediate feedback if bad code is introduced into the code base.<br><br>
**Dev**  
This is the first remote server that the combined project code base will be deployed to, this allows developers to test their code in an environment that should mimic production, however it is often unstable due to constant changes in API, versions and buggy code check-ins.<br><br>
**FUT**  
The functional unit testing environment is controlled by your QA team, and can be used for manual or automated testing.<br><br>
**SIT**  
This is the first real proving ground of the configured application, as they are configured and packaged together mimicking the production environment. This is where projects are tested to ensure they can coexist within the full product ecosystem.<br><br>
**Performance**  
This environment needs to closely match your target production model in order to validate that your application will perform. Owned and managed by the performance management team, tests are load based to see how much stress it can handle.<br><br>
**Staging (Pre-Production)**
This environment is the final step before deploying code to production, and also is used to diagnose production bugs after go-live.<br><br>
And there you have it…any bad code that makes it through all these obstacles deserves to see the light of day :P if a defect does make it through, its back to staging and time to schedule a patch release.
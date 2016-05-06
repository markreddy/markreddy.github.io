---

title: Restarting Jenkins
description: "How to gracefully and forcefully restart Jenkins"
tags: [tutorial, jenkins]
comments: true
image:
  feature: texture-feature-01.jpg
---

Jenkins is a wonderful CI tool the I rely on heavily for any project that I indeed to bring to fruition. However sometimes is can act a little funny, for example if you rename a project it will not display the build history from before the name change and may randomly drop the build history after the name change. This can be rectified by simply restarting Jenkins and allowing it to pick up those changes in a more stable way.  
The best way I know of to restart Jenkins is as follows:<br><br>
In your browser go to:<br><br>

````jenkins_url/safeRestart````<br><br>
This is a smart restart that will allow existing jobs to finish and restart when they are complete. As for queued job, they will remain in the queue to run after the restart is complete. Great!<br><br>
If you require a forcefully restart of Jenkins this can achieved by hitting:<br><br>

````jenkins_url/restart````<br><br>
This will force a restart without waiting for builds to complete.
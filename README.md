# Configuring Travis CI to Run a Deno Project 

I am a big fan of Deno. I am also a big fan of Travis CI. What’s not to like? Deno is a powerful new programming framework that picks up where Node.js left off. Travis CI is a CI/CD platform that integrates easily with the projects stored in my GitHub repo. They’re both very cool.

But there’s a problem: Travis CI does not support Deno out of the box.

[Deno](https://deno.land) is still in its infancy, so it makes sense that it is not quite yet on the Travis CI radar. Still, no biggie. Travis CI is flexible enough to allow me to build support for Deno right into the CI/CD workflow that kicks off when my Deno project runs on Travis CI. In fact, getting Deno to run on Travis CI was pretty easy, and the results are very useful, so allow me to share.

First I’m going to cover the overall process for deploying to Travis CI and running a workflow defined in a `.travis.yml` file. Then I’ll show you the custom `.travis.yml` file I wrote that has Travis CI install Deno and run the unit tests for my Deno project.

## Travis CI 101
Travis CI runs a CI/CD process right out of the box as part of its signup process. The first time you come to travic-ci.org, you’ll be asked to log in to Travis CI using your GitHub or BitBucket credentials. (The Bitbucket signup is in beta.)

The signup process asks you to declare repositories on the source code management (SCM) service, into which a webhook will be installed. Once a webhook is installed on the given repository, Travis CI will receive notifications about events that happen in that repository. For example, when a developer commits code into a repository that has a webhook installed, Travis CI will be notified about the commit.

Travis CI will clone the contents of that repo into a virtual machine instance running in the Travis CI domain. Once the runner VM has the contents of the cloned repository, it will look for a special file named travis.yml that contains instructions for provisioning the VM and about tasks to perform once the runner VM is provisioned. Figure 1 below describes the process.

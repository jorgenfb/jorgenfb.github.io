---
layout:     post
title:      sbt clean on Heroku
date:       2014-10-21 15:31:19
summary:    How to run sbt clean before building your application on Heroku.
categories: sbt heroku
---

Yesterday I updated a [Play Framework](https://playframework.com) running on [Heroku](https://www.heroku.com/) from version 2.2.x to 2.3.x. The process was mostly pain free. I updated some dependecies and did a couple of migration steps, no problems. Finally I ran ```sbt clean build``` to test my application. Testing when fine so I decided to deploy the new version.

I got the first error during the build process on heroku. The message was:

```
java.util.NoSuchElementException: key not found XXX
```

The missing element actually changed during subsequent builds on heroku. At first I thought it migth be a problem running on Java 6, so I updated to Java 7. The problem still existed. When I finally sat down to read all the output from Heroku, I discovered that Heroku does not run the sbt clean command before building the project. A quick google search told my how to run sbt clean on Heroku. All you have to do is set the environment variable SBT_CLEAN=true for your application. If you have the heroku toolbelt installed you can do this by running:

```
heroku config:set SBT_CLEAN=true
```

That's it! Heroku will now run sbt clean before building your projects.
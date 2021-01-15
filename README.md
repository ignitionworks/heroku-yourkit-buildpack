# Heroku YourKit Buildpack

This buildpack will add the shared library to be used as the YourKit agent to be loaded by the JVM. This allows
YourKit to be used to profile the Java application running on Heroku.

## Usage

Add buildpack:

```
$ heroku buildpacks:add https://github.com/ignitionworks/heroku-yourkit-buildpack --app YOUR_APP
```

Modify your JAVA_OPTS to include:

```
-agentpath:yourkit/bin/linux-x86-64/libyjpagent.so=port=10001,disablestacktelemetry,exceptions=off
```

_(`disablestacktelemetry`, and `exceptions=off` significantly reduced bootup time for me, and can be enabled once connected)_

See [YourKit docs](https://www.yourkit.com/docs/java/help/) for help and the [startup options](https://www.yourkit.com/docs/java/help/startup_options.jsp).

Forward the port:

```
$ heroku ps:forward 10001 --app YOUR_APP
```

Then connect YourKit

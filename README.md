#Config Override Example

Example of best-practice for providing overrides to config values in an Akka/Play/Lagom application when moving from local development into some other environment.

##Usage

in `conf/application.conf` we have the following configuration

```
demo.welcome-message = "Welcome to Play!"
demo.welcome-message = ${?WELCOME_MESSAGE}
```

If you start the Play! application running with 

```bash
sbt run
```

You'll see the welcome message

```bash
Welcome to Play!
```

However, you can override this default by setting an environment variable with the key `WELCOME_MESSAGE`, for instance:

```bash
export WELCOME_MESSAGE="Hola, bienvenido a Play"
sbt run
```

Will result in the welcome message

```bash
Hola, bienvenido a Play
```

## What's Happening?

The `?` in the config substitution value tells the config system to ignore the value if it doesn't exist and fallback to whatever it was set to previously.

In this case we set it to something we want in development (our local Kafka or Cassandra endpoints, for instance) and then, when we want to run in a staging environment we can override in our Kubernetes config by setting an environment variable for the container running our application.
# Islandora Demo Web Service

This is a small demo project to show you how to expose RESTful web services in an OSGi runtime like Karaf using JAXRS annotations.

## Requirements

- Java
- Maven
- An OSGi runtime, like Karaf

## Installation

From the project root, `mvn install` will compile the bundle and put it in your local maven repository.  From there, you can deploy into your OSGi runtime as usual.  For Karaf, the easiest way is to copy the islandora-web-service-1.0-SNAPSHOT.jar from the `target` directory to the `deploy` folder of your Karaf installation.

You'll also need to make sure to install the cxf feature in Karaf, like so: `feature:install cxf`.

## Usage

This demo service yells back at you.  Whatever message you send it gets converted to uppercase and is returned as `text/plain` response.  By default, all web services are exposed off of a ‘root’ endpoint of `/cxf`, so your service should be available at `localhost:8181/cxf/shout`.

For example:
```bash
$ curl “localhost:8181/cxf/shout/hey”

HEY
```

## Making Your Own Services

You can always use this as a reference, but an even easier approach is just to use maven to generate a stub project for you.

```bash
$ mvn archetype:generate -DarchetypeGroupId=org.apache.karaf.archetypes -DarchetypeArtifactId=karaf-blueprint-archetype
```

Then you just add the following dependency to your POM and start annotating some beans:
```xml
<dependency>
      <groupId>org.apache.cxf</groupId>
      <artifactId>cxf-rt-frontend-jaxrs</artifactId>
      <version>3.1.4</version>
</dependency>
```

See [the JAXRS documentation](https://jersey.java.net/documentation/latest/jaxrs-resources.html) for all the things you can do.

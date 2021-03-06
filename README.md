# anchore-engine-with-proxy
## about this project

This is a really simple little project that I created to deal with some issues I was having running the **anchore engine** in a Docker image behind our corporate firewall. The **feeds service** uses the Python **requests** library which unfortunately appears to send **SSL** packets when doing the initial SSL/TLS handshake. It doesn't appear to do this when running outside our environment, so there is some logic down in **OpenSSL** that is switching it to SSL. Due to the POODLE vulnerability in SSL, we need the requests to use **TLSv1.2**.

## dependencies

This project depends on the image **anchore/anchore-engine**.

## building

To build the images for this project, run the following commands:

```
docker pull docker.io/anchore/anchore-engine
docker build -t anchore-engine-with-proxy:latest .
docker build -t anchore-proxy:latest anchore-proxy
```

## usage

The included **docker-compose.yaml** file provides a sample of how to run the **anchore engine**. It is based off the sample compose file that anchore provides; the only difference is that it uses my **anchore-engine-with-proxy** image instead of theirs and adds a service based on the **anchore-proxy** image.

Once you have all the required images built/pulled, you can run the engine like this in the directory where the **docker-compose.yaml** file is:

```
docker-compose up
```

If you want to run the images in the background, run it like this:

```
docker-compose up -d
```

To stop the images, run:

```
docker-compose down
```

# questions/comments?

You can email me at openshiftninja@gmail.com

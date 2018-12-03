## Supported tags and respective `Dockerfile` links

## What is Varnish Cache?

Varnish is an HTTP accelerator designed for content-heavy dynamic web sites as well as APIs.

For more details, check the following links:  
https://varnish-cache.org/  
https://en.wikipedia.org/wiki/Varnish_(software)  
https://github.com/varnishcache/varnish-cache

## Environment Variables

* `LISTEN_ADDRESS`  
  Client requests listen address.  
  Used in `varnishd -a`.  
  Value is left empty by default.

* `LISTEN_PORT`  
  Client requests listen address port.  
  Used in `varnishd -a`.  
  Default value: `8080`.

* `MANAGEMENT_INTERFACE_ADDRESS`  
  Management interface address.  
  Used in `varnishd -T <address[:port]>`.  
  Value is left empty by default.

* `MANAGEMENT_INTERFACE_PORT`  
  Management interface address port.  
  Used in `varnishd -T <address[:port]>`.  
  Default value: `6082`.

* `BACKEND_DEFAULT_HOST`  
  Can be used in file `default.vcl.template` only.  
  Default value: `127.0.0.1`.

* `BACKEND_DEFAULT_PORT`  
  Can be used in file `default.vcl.template` only.  
  Default value: `8080`.

* `VSL_RECLEN`  
  Used in `varnishd -p <vsl_reclen=value>`.  
  Default value: `255`.

  For more details, check the following link:  
  https://varnish-cache.org/docs/trunk/reference/varnishd.html#vsl-reclen

* `MALLOC`  
  Used in `varnishd -s <malloc[,size]>`.  
  Default value: `256m`.

  For more details, check the following link:  
  https://varnish-cache.org/docs/trunk/users-guide/storage-backends.html

## Starting a Docker container

Run in `detached` mode:
```
docker run -d aka1/docker-varnish:<DOCKER_TAG_NAME>
```

For more details, check the following link:  
https://docs.docker.com/engine/reference/commandline/run/

## Starting a Docker container with Docker Compose

Run in `detached` mode:
```
docker-compose up -d
```

For more details, check the following link:  
https://docs.docker.com/compose/reference/up/

For a quick start, check the file [docker-compose.yml.dist](https://github.com/akai-z/docker-varnish/blob/master/docker-compose.yml.dist).

## Building a Docker image

```
docker build -t <IMAGE_NAME> <Path/URL to Dockerfile>
```

For more details, check the following link:  
https://docs.docker.com/engine/reference/commandline/build/

## Using custom VCL file

In most cases,  
A custom VCL file should be used with this Docker image.  
(Instead of using the default one provided by the image)

That could be done by using  
the `-v` or the `--volume` flag in `docker run` command.  
(The same applies to Docker Compose)

For more details, check the following link:  
https://docs.docker.com/storage/volumes/

The file name in the second field of flag `-v`  
(where the file is mounted in the container),  
must be named `default.vcl.template`.  
And its full path is: `/etc/varnish/default.vcl.template`.

That would allow environment variables (if used)  
to be substituted with real values.

Example:
```
docker run \
  -v <PATH_TO_VCL_FILE>:/etc/varnish/default.vcl.template \
  -d aka1/docker-varnish:<DOCKER_TAG_NAME>
```

## Passing arguments to `varnishd`

It is possible to pass arguments to `varnishd`,  
by setting them in `docker run` command.

For example:
```
docker run -d aka1/docker-varnish:<DOCKER_TAG_NAME> \
  -b 127.0.0.1:8080
```

However, by using this approach,  
all the preset/default parameters that are already set in the image  
will not be included.

And all `varnishd` required parameters must be set, as a result.

For more details, check the following link:  
https://varnish-cache.org/docs/trunk/reference/varnishd.html

## Authors

* Ammar K.

## License

[GNU General Public License version 2](https://github.com/akai-z/docker-varnish/blob/master/LICENSE)

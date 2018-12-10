## Supported tags and respective `Dockerfile` links

* [`6.1.1-alpine, 6.1-alpine-edge, 6.1-alpine, 6-alpine, latest-alpine, alpine` (*alpine/6.1/Dockerfile*)](https://github.com/akai-z/docker-alpine-varnish/blob/ecad10e7aa778c42fcc59a373706597e9c15e0c1/6.1/Dockerfile)
* [`6.1.1-debian, 6.1-debian-stretch, 6-debian, latest-debian, debian` (*debian/6.1/Dockerfile*)](https://github.com/akai-z/docker-debian-varnish/blob/323592d1ee9ceb1f7c9482010258ffed45c55d1e/6.1/Dockerfile)
* [`6.0.0-alpine, 6.0-alpine3.8, 6.0-alpine` (*alpine/6.0/Dockerfile*)](https://github.com/akai-z/docker-alpine-varnish/blob/ecad10e7aa778c42fcc59a373706597e9c15e0c1/6.0/Dockerfile)
* [`6.0.2-debian, 6.0-debian-stretch, 6.0lts-debian, 6.0-debian` (*debian/6.0/Dockerfile*)](https://github.com/akai-z/docker-debian-varnish/blob/323592d1ee9ceb1f7c9482010258ffed45c55d1e/6.0/Dockerfile)
* [`5.2.1-alpine, 5.2-alpine3.7, 5.2-alpine, 5-alpine` (*alpine/5.2/Dockerfile*)](https://github.com/akai-z/docker-alpine-varnish/blob/ecad10e7aa778c42fcc59a373706597e9c15e0c1/5.2/Dockerfile)
* [`5.2.1-debian, 5.2-debian-stretch, 5.2-debian, 5-debian` (*debian/5.2/Dockerfile*)](https://github.com/akai-z/docker-debian-varnish/blob/323592d1ee9ceb1f7c9482010258ffed45c55d1e/5.2/Dockerfile)
* [`4.1.9-alpine, 4.1-alpine3.6, 4.1-alpine, 4-alpine` (*alpine/4.1/Dockerfile*)](https://github.com/akai-z/docker-alpine-varnish/blob/ecad10e7aa778c42fcc59a373706597e9c15e0c1/4.1/Dockerfile)

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
docker run -d aka1/varnish:<docker_tag_name>
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

For a quick start, check the file [`docker-compose.yml.dist`](https://github.com/akai-z/docker-varnish/blob/master/docker-compose.yml.dist).

## Building a Docker image

```
docker build -t <image_name> <dockerfile_path_or_url>
```

For more details, check the following link:  
https://docs.docker.com/engine/reference/commandline/build/

## Using custom VCL file

In most cases,  
A custom VCL file should be used with this Docker image.  
(Instead of using the default one provided by the image.)

That could be done by using  
the `-v` or the `--volume` flag in `docker run` command.  
(The same applies to Docker Compose.)

For more details about volumes in Docker, check the following link:  
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
  -v <custom_vcl_file_path>:/etc/varnish/default.vcl.template \
  -d aka1/varnish:<docker_tag_name>
```

## Passing arguments to `varnishd`

It is possible to pass arguments to `varnishd`,  
by setting them in `docker run` command.

For example:
```
docker run -d aka1/varnish:<docker_tag_name> \
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

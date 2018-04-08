# Building

The easiest way to build this module is using NGINX's `build_module.sh` script.

```bash
$ wget http://hg.nginx.org/pkg-oss/raw-file/default/build_module.sh
$ chmod +x build_module.sh
$ ./build_module.sh -y https://github.com/gomlgs/nginx-request-start-time.git
```

This produces a deb package that works with the `mainline` version of NGINX.
See flags for `build_module.sh` for other options, including building for other
NGINX versions. I'd recommend building this inside a container.

## Docs

* [From NGINX](https://www.nginx.com/blog/creating-installable-packages-dynamic-modules/) - Building dynamic modules.
* [build_module.sh](https://hg.nginx.org/pkg-oss/file/tip/build_module.sh)

# Usage

Load the module early in the NGINX config.

```
load_module /etc/nginx/modules/ngx_request_start_time_module.so;
```

This provides a new variable `$request_start_usec` that can be used in other configuration.
An example:

```
  location / {
    proxy_set_header X-Request-Start $request_start_usec;
    
    proxy_pass http://some_server;
  }
```

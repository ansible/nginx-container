#nginx-container 

[![Build Status](https://travis-ci.org/chouseknecht/nginx-container-1.svg?branch=master)](https://travis-ci.org/chouseknecht/nginx-container-1)

Adds an nginx service to your [Ansible Container](https://github.com/ansible/ansible-container) project. Run the following commands
to install the service:

```
# Set the working directory to your Ansible Container project root
$ cd myproject

# Install the service
$ ansible-container install j00bar.nginx-container
```

This role is consumed by the [Ansible Container demo project](https://github.com/j00bar/django-gulp-nginx).

## Requirements

- [Ansible Container](https://github.com/ansible/ansible-container)
- An existing Ansible Container project. To create a project, simply run the following:
    ```
    # Create an empty project directory
    $ mkdir myproject

    # Set the working directory to the new directory
    $ cd myproject

    # Initialize the project
    $ ansible-contiainer init
    ```

## Role Variables

STATIC_ROOT: /static
> Path to static content to be served by nginx.

PIDFILE_DIR: /run/nginx
> Path where nginx will store the current PID value. 

ASSET_PATHS: []
> List of paths from which static content will be copied. Content will be copied to {{ STATIC_ROOT }}. 

> *NOTE* paths must be valid within the Ansible build container. If you're copying source files, mount the source
  directory to the build container using --with-volumes.

PROXY_DJANGO: no
> When using this role as part of the demo app, nginx needs to proxy the django service, in which case set this to 'yes'. 

PROXY_DJANGO_PASS: http://django:8080/
> The URL where proxied request will be sent.

## Dependencies

None.

## Development

For convenience, as you're working on changes to this role, you can test by using the following workflow:

```
# Commit your changes
$ git commit -m

# Push your changes 
$ git push 

# Set the working directory to tests
$ cd tests 

# Run a build that installs the role at the most recent commit 
$ ./build.sh
```

A couple of notes:

- You have to push your changes in order for the build to pick them up.
- Modify build.sh to point to your fork of this role.
- If all goes well and the build succeeds, the container built from your latest commit will be running in the background.
- The running container will publish port 8000:8000, so if you point a browser to localhost:8000, you should see the dfault nginx page .

## License

Apache v2

## Author Information

[@j00bar](https://github.com/j00bar)


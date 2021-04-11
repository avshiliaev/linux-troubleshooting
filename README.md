https://www.redhat.com/sysadmin
https://geekflare.com/cheat-sheet-system-admin/
https://linuxconfig.org/gnu-linux-general-troubleshooting-guide-for-beginners

# Intro
## Start in Docker

To run a disposable new container, you can simply attach a tty and standard input:

`docker run --rm -it --entrypoint bash <image-name-or-id>`

To prevent the above container from being disposed, run it without `--rm`.

Or to enter a running container, use `exec` instead:

`docker exec -it <container-name-or-id> bash`

For Ubuntu, you need to run:

`apt-get update`

before installing packages, and if your command is in a Dockerfile, you'll then need:

`apt-get -y install curl`

To suppress the standard output from a command use -qq. E.g.

`apt-get -qq -y install curl`

## Useful services

### Command not found

Refer to the [Command-not-found](https://command-not-found.com/) to see how to install a package depending on your
distribution.

### Explain shell

Refer to [Explain Shell](https://explainshell.com/) to get a detailed description of a command sequence.

# Troubleshooting scenarios 

#### Site is down
Sometimes we may run in to troubles when one of our web-server or site is down,We should be able to identify this 
problem which are likely causing the issues and fix the problem.

[Site is down](./SITE_IS_DOWN.md)


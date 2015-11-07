# Image Contents

This image is based on [shanesveller/elixir-lang](https://registry.hub.docker.com/u/shanesveller/elixir-lang/) and includes the features of that image.

At the time of writing, this Dockerfile results in an image that also contains:

* NodeJS 5.0.x (installed via [NodeSource](https://github.com/nodesource/distributions)'s APT repository)
* npm 3.3.6

It also includes the following `ONBUILD` steps for convenience of use as a base image itself:

* Creates a working directory for your app at `/usr/src/app`
* Adds files like `package.json` and `brunch-config.js` and installs `npm` dependencies
* Sets `MIX_ENV` to `prod`
* Copies files needed to determine Mix config and dependencies, then downloads and compiles those dependencies

All of the above occur before any custom instructions in a child Dockerfile that uses `FROM` to inherit from this one.

## Checking Versions

Want to check the current versions included in the latest image in light of future rebuilds?

* `docker run -it --rm shanesveller/elixir-lang apt-cache policy nodejs`

# Caveats

* `MIX_ENV` is set to `prod` globally for all commands run in the Docker container, unless overridden on a per-command basis or a later `ENV` Dockerfile instruction
* When building your own apps based on a third party's Docker image, you should make note of any `ONBUILD` instructions in the base image's `Dockerfile`, as these are executed dynamically while building your app, prior to **ANY** of the instructions in your own `Dockerfile`.

# Alternative images

Not happy with the Dockerfile steps? Having compatibility problems? Try one of these alternatives:

* [nifty/elixir](https://registry.hub.docker.com/u/nifty/elixir/)
* [josephyi/phoenixframework](https://registry.hub.docker.com/u/josephyi/phoenixframework/)
* [marcelocg/phoenix](https://registry.hub.docker.com/u/marcelocg/phoenix/)
* [mikaak/node-elixir-phoenix](https://registry.hub.docker.com/u/mikaak/node-elixir-phoenix/)

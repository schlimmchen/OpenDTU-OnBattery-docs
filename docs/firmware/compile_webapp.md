# Working with the WebApp

## General information

The WebApp works completly independent from the C/C++ firmware. When compiling
the firmware, the pre-compiled WebApp will be embedded into the firmware `.bin`
file. The WebApp is served to the browser by the embedded web server and then
runs on the client side. The communication between the frontend and the ESP32
running OpenDTU-OnBattery is done using the Web API.

The WebApp has to be (re-)compiled before building the firmware, as the WebApp
compilation result is not versioned in Git. A PlatformIO pre-script makes sure
that an up-to-date WebApp is available in your working directory right before
attempting to build the firmware.

There is a development server which hosts the frontend at your local computer
and allows easy development. It will forward the requests to the backend
automatically to your ESP32 (configurable IP address). That means you can
develop the webinterface without flashing the ESP32 (if the WebAPI stays the
same).

## Install prerequisits

* Install Node.js v20 to be able to work with the WebApp.
* The `yarn` package manager is required to install Node.js packages and to
  execute commands related to the WebApp. To make `yarn` available, you should
  enable `corepack`, which is shipped together with Node.js. `corepack`
  installs a shim to act as `yarn`, with the benefit of installing the one
  version of `yarn` configured for this project.

=== "Windows :material-microsoft-windows:"

    * Install Node.js v20 using the [prebuilt installer][1]{target=_blank} (use
      the default settings during installation).
    * Execute `corepack enable` in an elevated command prompt (run command
      prompt as administrator).

=== "Debian/Ubuntu Linux :material-linux:"

    * Install Node.js v20 from [nodesource][2]{target=_blank}.
    * Execute `sudo corepack enable`.

[1]: https://nodejs.org/en/download/prebuilt-installer
[2]: https://github.com/nodesource/distributions

## Building the WebApp

The WebApp is build using `yarn`. First of all you have to install or update
all the dependencies. Afterwards the app will be build. Start a Terminal of
your choice and enter the following commands:

```bash
cd webapp
yarn install
yarn build
```

The generated WebApp will be placed in the `webapp_dist` directory from where
it gets included by PlatformIO.

## Starting the Development Server

Create a file called `vite.user.ts` in the `webappp` directory with the
following content:

```ts
export const proxy_target = '192.168.20.110'
```

Replace the IP with the IP of your ESP32 running OpenDTU-OnBattery.

To start the development server execute the following command:

```bash
yarn dev
```

## Lint with [ESLint](https://eslint.org/)

```bash
yarn lint
```

## Format Source Code

Automatically format the source code files to use a common format before
committing changes.

```bash
yarn format
```

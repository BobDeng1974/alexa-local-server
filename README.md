
# alexa-local-server

[![GoDoc](https://godoc.org/github.com/AndreasAbdi/alexa-local-server?status.png)](http://godoc.org/github.com/AndreasAbdi/alexa-local-server)
[![Go Report Card](https://goreportcard.com/badge/github.com/AndreasAbdi/alexa-local-server)](https://goreportcard.com/report/github.com/AndreasAbdi/alexa-local-server)
[![Build Status](https://travis-ci.org/AndreasAbdi/alexa-local-server.svg?branch=master)](https://travis-ci.org/AndreasAbdi/alexa-local-server)

# Description

This is a server for local control of different components in my house. Controls chromecast, commanding it to play youtube videos/and other chromecast media controls as well as infrared microcontrollers to turn on tvs,air conditioners, sound bars, etc.

## Instructions

### Build

Running `make build` will generate a binary in the folder `${project_directory}/bin/`. This can be deployed via running `./bin_name`.

Deploying via docker is possible. Running `make docker_build` will build an image with the name `aa/alexa-local-server`.
That image can then be used via running `docker run -d -p 8000:8000 aa/alexa-local-server`

### Deployment

1. [Install the Alexa CLI.](https://developer.amazon.com/docs/smapi/quick-start-alexa-skills-kit-command-line-interface.html)

2. modify the .serverconf.json.template with appropriate config values.

    - AlexaAppID is autogenerated by the deploy.sh script. Don't need to mess with it.
    - ServerAddress is the port where the server should listen on.
    - The IRFunctionality is based on an [ir blaster arduino endpoint.](https://github.com/mdhiggins/ESP8266-HTTP-IR-Blaster/). Not really mandatory to input.
    - Google Key is the google API key with the values to access youtube api. (Youtube Data API V3)

3. Run `./scripts/deploy.sh`

4. Tell alexa to do things like

    - `alexa, tell local server to play summertime sadness`
    - `alexa, tell local server to pause`
    - `alexa, tell local server i'm home`

5. Terminate by running the `./scripts/kill.sh` script.

## Notes

config file named `.serverconf.json` is read in the following order from

- the current directory of the application,
- a directory called `.als` in the current
- a directory called `.als` in the user's home directory

## Images

![Image of tv/sound bar turning on and a youtube stream loading](https://raw.githubusercontent.com/AndreasAbdi/alexa-local-server/master/configs/startup.gif)

## References

References [alexaskilserver](https://github.com/mikeflynn/go-alexa/blob/master/skillserver/skillserver.go) for middleware, encoding, and validation.

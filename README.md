## Cloud Foundry buildpack: Erlang

This is a Cloud Foundry buildpack for Erlang apps. It uses [Rebar](https://github.com/basho/rebar).

It was adapted from a [Heroku Buildpack](https://github.com/archaelus/heroku-buildpack-erlang) with just a couple things changed to be CF compatible.

### Select an Erlang version

The Erlang/OTP release version that will be used to build and run your application is now sourced from a dotfile called `.preferred_otp_version`. It needs to be the branch or tag name from the http://github.com/erlang/otp repository, and further, needs to be one of the versions that precompiled binaries are available for.

Currently supported OTP versions:

* master (R17B pre)
* master-pu (R16B pre)
* OTP_R15B
* OTP_R15B01
* OTP_R15B02
* OTP_R16B
* OTP_R16B01
* OTP_R16B02
* OTP_R16B03

To select the version for your app:

    $ echo OTP_R15B01 > .preferred_otp_version
    $ git commit -m "Select R15B01 as preferred OTP version" .preferred_otp_version

### Create a Procfile for CF to run

Rebar projects must be run with the appliaation name, so it must be defined in a Procfile

    $ echo "web: erl -pa ebin deps/*/ebin -noshell -s <app name>" > Procfile
    $ git commit -m "Added Procfile" Procfile

### Build your CF App

    $ cf push <app name> -b https://github.com/spiegela/cf-buildpack-erlang

You may need to write a new commit and push if your code was already up to date.

## Heroku buildpack: Zotonic

This is a Heroku buildpack for a Zotonic site.
Use it for easy deployment of a single Zotonic site.
The buildpack will automatically provision a dev database and configure your Zotonic site to use it.

NOTICE: The git repo to push should only contain a Zotonic site, not the whole Zotonic source.

### Configure your site

    $ heroku config:add BUILDPACK_URL="https://github.com/cstar/heroku-buildpack-zotonic.git" -a YOUR_APP

or
    
    $ heroku create --buildpack "https://github.com/cstar/heroku-buildpack-zotonic.git"

### Configure your Zotonic site

Set the following environment variables :

* ADMIN_PASSWORD (That's the admin password, obviously)
* OTP_VERSION (Erlang version to be used, defaults to ```OTP_R16B03-1```)
* ZOTONIC_VERSION (Defaults to ```master```)

### Select an Erlang version

The Erlang/OTP release version that will be used to build and run your application is now sourced from the environment variable ```OTP_VERSION```. It needs to be the branch or tag name from the http://github.com/erlang/otp repository, and further, needs to be one of the versions that precompiled binaries are available for.

Currently supported OTP versions:

* OTP_R15B
* OTP_R15B01
* OTP_R15B02
* OTP_R16B01
* OTP_R16B02
* OTP_R16B03-1

To select the version for your app set environment variable ```OTP_VERSION``` to define Erlang version.

    $ heroku config:set OTP_VERSION=OTP_R16B03-1

### Select Zotonic version

The Zotonic version can be selected via an environment variable similar to the Erlang version. By default the ```master``` branch of Zotonic source is used. To define a release version set the ```ZOTONIC_VERSION``` environment variable.

    $ heroku config:set ZOTONIC_VERSION=release-0.10.1

Here are a few example of possible values for ```ZOTONIC_VERSION```:

* release-0.9.5
* release-0.10.0
* release-0.10.0p1
* release-0.10.1

### Deploy your site

    $ git push heroku master

You may need to write a new commit and push if your code was already up to date.

### TODO

~~Select the Zotonic version to deploy. Currently fetches master.~~

Fetches deps and rebuilds all Zotonic on each deploys, should use the build cache to only recompile the necessary bits.

IMPORTANT: All file uploads go to the transient file system, meaning that everything is destroyed on each deploys. These assets should go to S3 or similar.

Pull requests are very welcome.

### THANKS

Geoff Cant for writing the base heroku-buildpack-erlang, the starting point of this buildpack. And the Zotonic and Heroku guys.

### ABOUT ZOTONIC

Zotonic is a blazingly fast CMS. Read more about it here: http://www.zotonic.com

### AUTHOR

Eric Cestari

http://twitter.com/cstar

http://eric.cestari.info/

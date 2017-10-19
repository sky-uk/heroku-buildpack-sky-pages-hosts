# Heroku Buildpack Sky Pages Hosts


## Introduction

A Heroku buildpack for setting additional hosts allowing heroku to run functional tests on apps that use domain based routing.


## Installation

Add the buildpack to your Heroku app either using the CLI or the Heroku dashboard.

    $ heroku buildpacks:add https://github.com/sky-uk/heroku-buildpack-sky-pages-hosts.git

## Usage

Add a CSV of domains to add to the build to the ENV variable DOMAIN_ROUTING_HOSTNAMES

# Heroku Buildpack Sky Pages Hosts


## Introduction

A Heroku buildpack for setting additional hosts allowing heroku to run functional tests on apps that use domain based routing.


## Installation

Add the buildpack to your Heroku app either using the CLI or the Heroku dashboard.

    $ heroku buildpacks:set --index 1 https://github.com/sky-uk/heroku-buildpack-sky-pages-hosts.git

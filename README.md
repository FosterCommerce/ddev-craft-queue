# fostercommerce/ddev-craft-queue <!-- omit in toc -->

[![tests](https://github.com/fostercommerce/ddev-craft-queue/actions/workflows/tests.yml/badge.svg)](https://github.com/fostercommerce/ddev-craft-queue/actions/workflows/tests.yml) ![project is maintained](https://img.shields.io/maintenance/yes/2024.svg)

- [Introduction](#introduction)
- [Installation Started](#installation)
- [Configuration](#configuration)

## Introduction

This add-on allows you to start a Craft queue worker in a Craft's DDEV web container.

## Installation

```shell
ddev get fostercommerce/ddev-craft-queue
ddev restart
```

## Configuration

This plugin adds the `web-build/craft-worker.conf` file. To configure your queue workers, remove the `#ddev-generated` line, and update the file.

For example, to run multiple queue workers, update the file to

```
[program:craft-queue]
process_name=%(program_name)s_%(process_num)s
command=/usr/bin/php /var/www/html/craft queue/listen
autostart=true
autorestart=true
numprocs=4
stdout_logfile=/var/tmp/logpipe
stdout_logfile_maxbytes=0
redirect_stderr=true
stopwaitsecs=3600
```
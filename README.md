# Rosie, the robot

[![Build Status](https://travis-ci.org/datasciencebr/rosie.svg?branch=master)](https://travis-ci.org/datasciencebr/rosie)
[![Code Climate](https://codeclimate.com/github/datasciencebr/rosie/badges/gpa.svg)](https://codeclimate.com/github/datasciencebr/rosie)
[![Coverage Status](https://coveralls.io/repos/github/datasciencebr/rosie/badge.svg?branch=master)](https://coveralls.io/github/datasciencebr/rosie?branch=master)

A Python application reading receipts from the [Quota for Exercising Parliamentary Activity](https://github.com/datasciencebr/serenata-de-amor/blob/master/CONTRIBUTING.md#more-about-the-quota-for-exercising-parliamentary-activity-ceap) (aka CEAP) from the Brazilian Chamber of Deputies and outputs, for each of the receipts, a _probability of corruption_ and a list of reasons why it was considered this way.

## Running

### With Docker

```console
$ docker build -t rosie .
$ docker run --rm -v /tmp/serenata-data:/tmp/serenata-data rosie

```

Then check your `/tmp/serenata-data/` directory in you host machine for `irregularities.xz`.

### Without Docker

#### Setup

```console
$ conda update conda
$ conda create --name serenata_rosie python=3
$ source activate serenata_rosie
$ ./setup
```

#### Running

```console
$ python rosie.py run
```

The toolbox expects to find Amazon credentials in a `config.ini` file. If You get an error of missing `config.ini` you can just copy the `config.ini.example` to a `config.ini` and everything will run smoothly (don't bother about `AccessKey` and `SecretKey` unless you're planning to upload files to S3).

A `/tmp/serenata-data/irregularities.xz` file will be created. It's a compacted CSV with all the irregularities Rosie is able to find.

Also a target directory (where files are saved) can de passed — for example:

```console
$ python rosie.py run /my/serenata/directory/
```

#### Test suite

```console
$ python rosie.py test
```
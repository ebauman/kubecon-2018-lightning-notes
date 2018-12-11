# Kubegres: Accessing K8s From Postgres

Liz Frost, Heptio @stillinbeta

I'm in her selfie!

_You got database in my cloud!_

## Postgres Foreign Data Wrappers

They are a way for postgres to query data not stored in the database itself. 

e.g.
- ODBC
- Hue Bulbs

Postgres wrappers are mostly written in C, but someone wrote a Go wrapper (missed github link)

## Install the Library

`CREATE EXTENSION IF NOT EXISTS k8s_fdc;`

Pass in a kubeconfig, and create a table (see graphic).

## More complex things

Use JSONPATH to pull out information from advanced json replies from k8s api

This is really cool. See if we can get ahold of the slides for this one. 
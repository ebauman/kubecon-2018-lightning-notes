# CI/CD, Kubernetes, and Databases: Better Together

| Person | Handle | Company |
| ------ | ------ | ------- |
| Niraj Tolia | @nirajtolia | Kasten |
| Tom Manville | @tdmanv | Kasten |

--- 

## Our goal: move fast and test with real data

## What is not covered

- Stateful app debate
- Data protection strategies

## Why is there fear and risk with cloud-native and databases?
- Snowflakes
    
    Databases have traditionally been pets vs cattle

- Automation gap

    Not built into CICD pipelines. Test datasets have manual imports and get stale quickly

- DBAs and Ops

    Still see database groups isolated from both dev and infra ops groups. Not part of app dev. 

## What should the future look like?

> Keep calm and automate all the things

### Source Control

Include all schema changes, upgrade changes, tools, etc. in the *application* repository.

### Database Infrastructure

Deliver database infrastructure and configuration as *code*

### CI/CD Pipeline

Automate testing all database changes and modifications


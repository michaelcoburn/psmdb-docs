# System requirements

## x86_64    

Percona Server for MongoDB has the exact [system requirements](https://www.mongodb.com/docs/v6.0/administration/production-notes/#x86_64) as the MongoDB Community Edition.     

Starting in MongoDB 5.0, `mongod,` `mangos`, and the legacy `Mongo` shell are supported on x86_64 platforms that must meet these minimum micro-architecture requirements:     

* Only Oracle Linux running the Red Hat Compatible Kernel (RHCK) is supported. MongoDB does not support the Unbreakable Enterprise Kernel (UEK).     

* MongoDB 5.0 and above require the AVX instruction set, which is available on [select Intel and AMD processors](https://en.wikipedia.org/wiki/Advanced_Vector_Extensions#CPUs_with_AVX). 

## ARM64

Percona Server for MongoDB requires the ARMv8.2-A or later micro-architecture. Support for ARM64 (AARch64) includes [AWS Graviton processors](https://aws.amazon.com/ec2/graviton/).﻿

Currently, only [Docker images](https://hub.docker.com/r/percona/percona-server-mongodb/) are available.

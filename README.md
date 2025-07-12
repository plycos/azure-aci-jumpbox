# azure-aci-jumpbox

A lightweight Docker image designed for use as a jumpbox in [Azure Container Instances (ACI)](https://learn.microsoft.com/en-us/azure/container-instances/). Provides essential networking and SQL Server tools for troubleshooting and administrative tasks.

## Features

- Based on `ubuntu:22.04`
- Includes:
    - `curl`, `dnsutils` for network diagnostics
    - Microsoft SQL Server command-line tools (`mssql-tools18`)
    - `unixodbc-dev` for ODBC support
- Keeps the container running with `sleep infinity` for interactive sessions

## Build
```bash
  docker build -t azure-aci-jumpbox .
```
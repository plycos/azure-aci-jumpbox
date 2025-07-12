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

## Deploy to Azure via CLI

1. **Deploy to Azure Container Instances**
#### Public Setup
```bash
az container create \
  --resource-group <your-resource-group> \
  --name aci-jumpbox \
  --image ghcr.io/plycos/azure-aci-jumpbox:latest \
  --cpu 1 --memory 1 \
  --os-type Linux \
  --restart-policy Never \
  --ip-address Public
```
#### Subnet Setup
```bash
az container create \
  --resource-group <your-resource-group> \
  --name aci-jumpbox \
  --image ghcr.io/plycos/azure-aci-jumpbox:latest \
  --os-type Linux \
  --cpu 1 --memory 1 \
  --restart-policy Never \
  --vnet <your-vnet> \
  --subnet <your-subnet>
```
2. **Access the Jumpbox**
```bash
az container exec \
  --resource-group <your-resource-group> \
  --name aci-jumpbox \
  --exec-command "/bin/bash" 
```
3. **Delete when Done**
```bash
az container delete \
  --resource-group <your-resource-group> \
  --name aci-jumpbox \
  --yes
```
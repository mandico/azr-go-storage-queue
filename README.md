# Azure Golang Storage Queue

Sample program for sending/receiving message in Azure Storage Queue Trigger. 

# How to run the sample

## Prerequisite
* Install Go lang
* Docker

## Create Azure Storage Account Queue

## Set Environment Variables for the container

| Key | Description |
| ---- | ------ |
| ConnectionString | The Connection String for the Azure Storage Account |
| queueName | The name of the queue |

## Run queue receiver/sender

### receiver

Receive queue messages.

```bash
$ export ConnectionString="YOUR_CONNECTION_STRING_HERE"
$ export queueName=hello
$ go run receive.go
```

### sender

Send 100 messages to the Azure Storage Queue.

```bash
$ cd cmd/send
$ export ConnectionString="YOUR_CONNECTION_STRING_HERE"
$ export queueName=hello
$ go run send.go 100
```

```bash
LOCATION="eastus"
RESOURCE_GROUP="azr-rg-stg-queue"
STORAGE_ACCOUNT="azrstgqueue"
QUEUE="demo"

az group create -l $LOCATION -n $RESOURCE_GROUP
az storage account create -n $STORAGE_ACCOUNT -g $RESOURCE_GROUP -l $LOCATION --sku Standard_LRS
az storage queue create -n $QUEUE --account-name $STORAGE_ACCOUNT


Get Connection String
```
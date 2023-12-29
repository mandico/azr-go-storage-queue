# Azure Golang Storage Queue

Sample program for sending/receiving message in Azure Storage Queue Trigger. 

# How to run the sample

## Prerequisite
* Install Golang
* Docker

## Create Azure Storage Account Queue

```bash
LOCATION="eastus"
RESOURCE_GROUP="azr-rg-stg-queue"
STORAGE_ACCOUNT="azrstgqueue"
QUEUE="demo"

az group create -l $LOCATION -n $RESOURCE_GROUP
az storage account create -n $STORAGE_ACCOUNT -g $RESOURCE_GROUP -l $LOCATION --sku Standard_LRS
az storage queue create -n $QUEUE --account-name $STORAGE_ACCOUNT

export ConnectionString=$(az storage account show-connection-string -g $RESOURCE_GROUP -n $STORAGE_ACCOUNT -o tsv)
export queueName=$QUEUE
```

## Set Environment Variables for the container

| Key | Description |
| ---- | ------ |
| ConnectionString | The Connection String for the Azure Storage Account |
| queueName | The name of the queue |

```bash
export ConnectionString=$(az storage account show-connection-string -g $RESOURCE_GROUP -n $STORAGE_ACCOUNT -o tsv)
export queueName=$QUEUE
```


## Run queue receiver/sender

### receiver

Receive queue messages.

```bash
$ go run cmd/receive/receive.go
```

### sender

Send 100 messages to the Azure Storage Queue.

```bash
$ go run cmd/send/send.go 100
```
---
# How to Build Application and Image

Docker Build and Docker Release
```bash
make docker-build

make docker-release
```
---
# How to Deploy in Kubernetes

Deploy with CronJob
```bash
kubectl apply -f k8s/job.yaml
```

---
# Delete Resources
```bash
LOCATION="eastus"
RESOURCE_GROUP="azr-rg-stg-queue"
STORAGE_ACCOUNT="azrstgqueue"
QUEUE="demo"

az group delete -n $RESOURCE_GROUP -y
```
---
title: Azure Containerexemplaren - meerdere containergroep | Azure Docs
description: Azure Containerexemplaren - groep met meerdere container
services: container-instances
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: 
keywords: 
ms.assetid: 
ms.service: container-instances
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/26/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 140f58582645ea32f77e901eb13364ed145bbecf
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="deploy-a-container-group"></a><span data-ttu-id="f229c-103">Een containergroep implementeren</span><span class="sxs-lookup"><span data-stu-id="f229c-103">Deploy a container group</span></span>

<span data-ttu-id="f229c-104">Azure Containerexemplaren ondersteuning van de implementatie van meerdere containers naar één host met behulp van een *containergroep*.</span><span class="sxs-lookup"><span data-stu-id="f229c-104">Azure Container Instances support the deployment of multiple containers onto a single host using a *container group*.</span></span> <span data-ttu-id="f229c-105">Dit is handig bij het bouwen van een toepassing ter voor logboekregistratie, bewaken of een andere configuratie waarbij een tweede gekoppelde proces in een service nodig heeft.</span><span class="sxs-lookup"><span data-stu-id="f229c-105">This is useful when building an application sidecar for logging, monitoring, or any other configuration where a service needs a second attached process.</span></span> 

<span data-ttu-id="f229c-106">Dit document helpt bij het uitvoeren van een eenvoudige meerdere container ter-configuratie met een Azure Resource Manager-sjabloon.</span><span class="sxs-lookup"><span data-stu-id="f229c-106">This document walks through running a simple multi-container sidecar configuration using an Azure Resource Manager template.</span></span>

## <a name="configure-the-template"></a><span data-ttu-id="f229c-107">De sjabloon configureren</span><span class="sxs-lookup"><span data-stu-id="f229c-107">Configure the template</span></span>

<span data-ttu-id="f229c-108">Maak een bestand met de naam `azuredeploy.json` en kopieer de volgende json naar deze.</span><span class="sxs-lookup"><span data-stu-id="f229c-108">Create a file named `azuredeploy.json` and copy the following json into it.</span></span> 

<span data-ttu-id="f229c-109">In dit voorbeeld wordt is een containergroep met twee containers en een openbare IP-adres gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="f229c-109">In this sample, a container group with two containers and a public IP address is defined.</span></span> <span data-ttu-id="f229c-110">De eerste container van de groep wordt een internettoepassing gerichte uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="f229c-110">The first container of the group runs an internet facing application.</span></span> <span data-ttu-id="f229c-111">De tweede container, de ter maakt een HTTP-aanvraag naar de belangrijkste webtoepassing via een van de groep lokale netwerk.</span><span class="sxs-lookup"><span data-stu-id="f229c-111">The second container, the sidecar, makes an HTTP request to the main web application via the group's local network.</span></span> 

<span data-ttu-id="f229c-112">In dit voorbeeld ter kan worden uitgebreid activeren van een waarschuwing als er een HTTP-antwoordcode dan 200 OK ontvangen.</span><span class="sxs-lookup"><span data-stu-id="f229c-112">This sidecar example could be expanded to trigger an alert if it received an HTTP response code other than 200 OK.</span></span> 

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
  },
  "variables": {
    "container1name": "aci-tutorial-app",
    "container1image": "microsoft/aci-helloworld:latest",
    "container2name": "aci-tutorial-sidecar",    
    "container2image": "microsoft/aci-tutorial-sidecar"
  },
    "resources": [
      {
        "name": "myContainerGroup",
        "type": "Microsoft.ContainerInstance/containerGroups",
        "apiVersion": "2017-08-01-preview",
        "location": "[resourceGroup().location]",
        "properties": {
          "containers": [
            {
              "name": "[variables('container1name')]",
              "properties": {
                "image": "[variables('container1image')]",
                "resources": {
                  "requests": {
                    "cpu": 1,
                    "memoryInGb": 1.5
                    }
                },
                "ports": [
                  {
                    "port": 80
                  }
                ]
              }
            },
            {
              "name": "[variables('container2name')]",
              "properties": {
                "image": "[variables('container2image')]",
                "resources": {
                  "requests": {
                    "cpu": 1,
                    "memoryInGb": 1.5
                    }
                }
              }
            }
          ],
          "osType": "Linux",
          "ipAddress": {
            "type": "Public",
            "ports": [
              {
                "protocol": "tcp",
                "port": "80"
              }
            ]
          }
        }
      }
    ],
    "outputs": {
      "containerIPv4Address": {
        "type": "string",
        "value": "[reference(resourceId('Microsoft.ContainerInstance/containerGroups/', 'myContainerGroup')).ipAddress.ip]"
      }
    }
  }
```

<span data-ttu-id="f229c-113">Voor het gebruik van een installatiekopie van privé-container register, moet u een object toevoegen aan het json-document met de volgende indeling.</span><span class="sxs-lookup"><span data-stu-id="f229c-113">To use a private container image registry, add an object to the json document with the following format.</span></span>

```json
"imageRegistryCredentials": [
    {
    "server": "[parameters('imageRegistryLoginServer')]",
    "username": "[parameters('imageRegistryUsername')]",
    "password": "[parameters('imageRegistryPassword')]"
    }
]
```

## <a name="deploy-the-template"></a><span data-ttu-id="f229c-114">De sjabloon implementeren</span><span class="sxs-lookup"><span data-stu-id="f229c-114">Deploy the template</span></span>

<span data-ttu-id="f229c-115">Een resourcegroep maken met de opdracht [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="f229c-115">Create a resource group with the [az group create](/cli/azure/group#create) command.</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location westus
```

<span data-ttu-id="f229c-116">Implementeren van de sjabloon met de [az implementatie maken](/cli/azure/group/deployment#create) opdracht.</span><span class="sxs-lookup"><span data-stu-id="f229c-116">Deploy the template with the [az group deployment create](/cli/azure/group/deployment#create) command.</span></span>

```azurecli-interactive
az group deployment create --name myContainerGroup --resource-group myResourceGroup --template-file azuredeploy.json
```

<span data-ttu-id="f229c-117">Binnen enkele seconden ontvangt u een eerste reactie van Azure.</span><span class="sxs-lookup"><span data-stu-id="f229c-117">Within a few seconds, you will receive an initial response from Azure.</span></span> 

## <a name="view-deployment-state"></a><span data-ttu-id="f229c-118">Implementatiestatus weergeven</span><span class="sxs-lookup"><span data-stu-id="f229c-118">View deployment state</span></span>

<span data-ttu-id="f229c-119">U kunt de status van de implementatie weergeven, met de `az container show` opdracht.</span><span class="sxs-lookup"><span data-stu-id="f229c-119">To view the state of the deployment, use the `az container show` command.</span></span> <span data-ttu-id="f229c-120">Hiermee wordt de ingerichte openbaar IP-adres gedurende welke de toepassing toegankelijk zijn.</span><span class="sxs-lookup"><span data-stu-id="f229c-120">This returns the provisioned public IP address over which the application can be accessed.</span></span>

```azurecli-interactive
az container show --name myContainerGroup --resource-group myResourceGroup -o table
```

<span data-ttu-id="f229c-121">Uitvoer:</span><span class="sxs-lookup"><span data-stu-id="f229c-121">Output:</span></span>

```azurecli
Name              ResourceGroup    ProvisioningState    Image                                                             IP:ports           CPU/Memory    OsType    Location
----------------  ---------------  -------------------  ----------------------------------------------------------------  -----------------  ------------  --------  ----------
myContainerGroup  myResourceGrou2  Succeeded            microsoft/aci-tutorial-sidecar,microsoft/aci-tutorial-app:v1      40.118.253.154:80  1.0 core/1.5 gb   Linux     westus
```

## <a name="view-logs"></a><span data-ttu-id="f229c-122">Logboeken bekijken</span><span class="sxs-lookup"><span data-stu-id="f229c-122">View logs</span></span>   

<span data-ttu-id="f229c-123">Weergave van de logboekuitvoer van een container met de `az container logs` opdracht.</span><span class="sxs-lookup"><span data-stu-id="f229c-123">View the log output of a container using the `az container logs` command.</span></span> <span data-ttu-id="f229c-124">De `--container-name` argument Hiermee geeft u de container waarin voor het ophalen van Logboeken.</span><span class="sxs-lookup"><span data-stu-id="f229c-124">The `--container-name` argument specifies the container from which to pull logs.</span></span> <span data-ttu-id="f229c-125">In dit voorbeeld wordt is de eerste container opgegeven.</span><span class="sxs-lookup"><span data-stu-id="f229c-125">In this example, the first container is specified.</span></span> 

```azurecli-interactive
az container logs --name myContainerGroup --container-name aci-tutorial-app --resource-group myResourceGroup
```

<span data-ttu-id="f229c-126">Uitvoer:</span><span class="sxs-lookup"><span data-stu-id="f229c-126">Output:</span></span>

```bash
istening on port 80
::1 - - [27/Jul/2017:17:35:29 +0000] "HEAD / HTTP/1.1" 200 1663 "-" "curl/7.54.0"
::1 - - [27/Jul/2017:17:35:32 +0000] "HEAD / HTTP/1.1" 200 1663 "-" "curl/7.54.0"
::1 - - [27/Jul/2017:17:35:35 +0000] "HEAD / HTTP/1.1" 200 1663 "-" "curl/7.54.0"
::1 - - [27/Jul/2017:17:35:38 +0000] "HEAD / HTTP/1.1" 200 1663 "-" "curl/7.54.0"
```

<span data-ttu-id="f229c-127">Overzicht van de logboeken voor de container side auto dezelfde opdracht geven de tweede containernaam worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="f229c-127">To see the logs for the side-car container, run the same command specifying the second container name.</span></span>

```azurecli-interactive
az container logs --name myContainerGroup --container-name aci-tutorial-sidecar --resource-group myResourceGroup
```

<span data-ttu-id="f229c-128">Uitvoer:</span><span class="sxs-lookup"><span data-stu-id="f229c-128">Output:</span></span>

```bash
Every 3.0s: curl -I http://localhost                                                                                                                       Mon Jul 17 11:27:36 2017

  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
  0     0    0     0    0     0      0      0 --:--:-- --:--:-- --:--:--     0  0  1663    0     0    0     0      0      0 --:--:-- --:--:-- --:--:--     0
HTTP/1.1 200 OK
Accept-Ranges: bytes
Content-Length: 1663
Content-Type: text/html; charset=utf-8
Last-Modified: Sun, 16 Jul 2017 02:08:22 GMT
Date: Mon, 17 Jul 2017 18:27:36 GMT
```

<span data-ttu-id="f229c-129">Zoals u ziet, is de ter periodiek een HTTP-aanvraag die naar de belangrijkste webtoepassing via een van de groep lokale netwerk om ervoor te zorgen dat deze wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="f229c-129">As you can see, the sidecar is periodically making an HTTP request to the main web application via the group's local network to ensure that it is running.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f229c-130">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="f229c-130">Next steps</span></span>

<span data-ttu-id="f229c-131">Dit document besproken de stappen die nodig zijn voor het implementeren van een exemplaar van de container voor meerdere Azure-container.</span><span class="sxs-lookup"><span data-stu-id="f229c-131">This document covered the steps needed for deploying a multi-container Azure container instance.</span></span> <span data-ttu-id="f229c-132">Zie de zelfstudie exemplaren van Azure-Container voor een complete Containerexemplaren Azure-ervaring.</span><span class="sxs-lookup"><span data-stu-id="f229c-132">For an end to end Azure Container Instances experience, see the Azure Container Instances tutorial.</span></span>

> [!div class="nextstepaction"]
> <span data-ttu-id="f229c-133">[Azure Containerexemplaren zelfstudie]:./container-instances-tutorial-prepare-app.md</span><span class="sxs-lookup"><span data-stu-id="f229c-133">[Azure Container Instances tutorial]: ./container-instances-tutorial-prepare-app.md</span></span>

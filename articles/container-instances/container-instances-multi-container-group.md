---
title: aaaAzure Containerexemplaren - meerdere containergroep | Azure Docs
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
ms.openlocfilehash: 976f578cd2a9bf7f05ab97f24662139bb72062ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-container-group"></a><span data-ttu-id="3cb8f-103">Een containergroep implementeren</span><span class="sxs-lookup"><span data-stu-id="3cb8f-103">Deploy a container group</span></span>

<span data-ttu-id="3cb8f-104">Azure Containerexemplaren ondersteuning Hallo-implementatie van meerdere containers naar één host met behulp van een *containergroep*.</span><span class="sxs-lookup"><span data-stu-id="3cb8f-104">Azure Container Instances support hello deployment of multiple containers onto a single host using a *container group*.</span></span> <span data-ttu-id="3cb8f-105">Dit is handig bij het bouwen van een toepassing ter voor logboekregistratie, bewaken of een andere configuratie waarbij een tweede gekoppelde proces in een service nodig heeft.</span><span class="sxs-lookup"><span data-stu-id="3cb8f-105">This is useful when building an application sidecar for logging, monitoring, or any other configuration where a service needs a second attached process.</span></span> 

<span data-ttu-id="3cb8f-106">Dit document helpt bij het uitvoeren van een eenvoudige meerdere container ter-configuratie met een Azure Resource Manager-sjabloon.</span><span class="sxs-lookup"><span data-stu-id="3cb8f-106">This document walks through running a simple multi-container sidecar configuration using an Azure Resource Manager template.</span></span>

## <a name="configure-hello-template"></a><span data-ttu-id="3cb8f-107">Hallo-sjabloon configureren</span><span class="sxs-lookup"><span data-stu-id="3cb8f-107">Configure hello template</span></span>

<span data-ttu-id="3cb8f-108">Maak een bestand met de naam `azuredeploy.json` en kopiëren Hallo json in het volgende.</span><span class="sxs-lookup"><span data-stu-id="3cb8f-108">Create a file named `azuredeploy.json` and copy hello following json into it.</span></span> 

<span data-ttu-id="3cb8f-109">In dit voorbeeld wordt is een containergroep met twee containers en een openbare IP-adres gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="3cb8f-109">In this sample, a container group with two containers and a public IP address is defined.</span></span> <span data-ttu-id="3cb8f-110">Hallo eerste container van Hallo groep wordt een internettoepassing gerichte uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="3cb8f-110">hello first container of hello group runs an internet facing application.</span></span> <span data-ttu-id="3cb8f-111">Hallo tweede container Hallo ter, kunt u een HTTP-aanvraag toohello hoofdweb toepassing via Hallo van de groep lokale netwerk.</span><span class="sxs-lookup"><span data-stu-id="3cb8f-111">hello second container, hello sidecar, makes an HTTP request toohello main web application via hello group's local network.</span></span> 

<span data-ttu-id="3cb8f-112">In dit voorbeeld ter mogelijk uitgebreide tootrigger een waarschuwing als er een HTTP-antwoordcode dan 200 OK ontvangen.</span><span class="sxs-lookup"><span data-stu-id="3cb8f-112">This sidecar example could be expanded tootrigger an alert if it received an HTTP response code other than 200 OK.</span></span> 

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

<span data-ttu-id="3cb8f-113">een object toohello json-document toouse een register van de installatiekopie van privé-container toevoegen met de volgende indeling Hallo.</span><span class="sxs-lookup"><span data-stu-id="3cb8f-113">toouse a private container image registry, add an object toohello json document with hello following format.</span></span>

```json
"imageRegistryCredentials": [
    {
    "server": "[parameters('imageRegistryLoginServer')]",
    "username": "[parameters('imageRegistryUsername')]",
    "password": "[parameters('imageRegistryPassword')]"
    }
]
```

## <a name="deploy-hello-template"></a><span data-ttu-id="3cb8f-114">Hallo-sjabloon implementeren</span><span class="sxs-lookup"><span data-stu-id="3cb8f-114">Deploy hello template</span></span>

<span data-ttu-id="3cb8f-115">Een resourcegroep maken met de Hallo [az groep maken](/cli/azure/group#create) opdracht.</span><span class="sxs-lookup"><span data-stu-id="3cb8f-115">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location westus
```

<span data-ttu-id="3cb8f-116">Hallo sjabloon Hello implementeren [az implementatie maken](/cli/azure/group/deployment#create) opdracht.</span><span class="sxs-lookup"><span data-stu-id="3cb8f-116">Deploy hello template with hello [az group deployment create](/cli/azure/group/deployment#create) command.</span></span>

```azurecli-interactive
az group deployment create --name myContainerGroup --resource-group myResourceGroup --template-file azuredeploy.json
```

<span data-ttu-id="3cb8f-117">Binnen enkele seconden ontvangt u een eerste reactie van Azure.</span><span class="sxs-lookup"><span data-stu-id="3cb8f-117">Within a few seconds, you will receive an initial response from Azure.</span></span> 

## <a name="view-deployment-state"></a><span data-ttu-id="3cb8f-118">Implementatiestatus weergeven</span><span class="sxs-lookup"><span data-stu-id="3cb8f-118">View deployment state</span></span>

<span data-ttu-id="3cb8f-119">status van de tooview Hallo van Hallo-implementatie, gebruik Hallo `az container show` opdracht.</span><span class="sxs-lookup"><span data-stu-id="3cb8f-119">tooview hello state of hello deployment, use hello `az container show` command.</span></span> <span data-ttu-id="3cb8f-120">Hiermee wordt ingericht Hallo openbaar IP-adres via welke Hallo toepassing toegankelijk zijn.</span><span class="sxs-lookup"><span data-stu-id="3cb8f-120">This returns hello provisioned public IP address over which hello application can be accessed.</span></span>

```azurecli-interactive
az container show --name myContainerGroup --resource-group myResourceGroup -o table
```

<span data-ttu-id="3cb8f-121">Uitvoer:</span><span class="sxs-lookup"><span data-stu-id="3cb8f-121">Output:</span></span>

```azurecli
Name              ResourceGroup    ProvisioningState    Image                                                             IP:ports           CPU/Memory    OsType    Location
----------------  ---------------  -------------------  ----------------------------------------------------------------  -----------------  ------------  --------  ----------
myContainerGroup  myResourceGrou2  Succeeded            microsoft/aci-tutorial-sidecar,microsoft/aci-tutorial-app:v1      40.118.253.154:80  1.0 core/1.5 gb   Linux     westus
```

## <a name="view-logs"></a><span data-ttu-id="3cb8f-122">Logboeken bekijken</span><span class="sxs-lookup"><span data-stu-id="3cb8f-122">View logs</span></span>   

<span data-ttu-id="3cb8f-123">Hallo logboekuitvoer van een container met Hallo weergeven `az container logs` opdracht.</span><span class="sxs-lookup"><span data-stu-id="3cb8f-123">View hello log output of a container using hello `az container logs` command.</span></span> <span data-ttu-id="3cb8f-124">Hallo `--container-name` geeft Hallo-container uit welke logboeken toopull argument.</span><span class="sxs-lookup"><span data-stu-id="3cb8f-124">hello `--container-name` argument specifies hello container from which toopull logs.</span></span> <span data-ttu-id="3cb8f-125">In dit voorbeeld wordt is de eerste container Hallo opgegeven.</span><span class="sxs-lookup"><span data-stu-id="3cb8f-125">In this example, hello first container is specified.</span></span> 

```azurecli-interactive
az container logs --name myContainerGroup --container-name aci-tutorial-app --resource-group myResourceGroup
```

<span data-ttu-id="3cb8f-126">Uitvoer:</span><span class="sxs-lookup"><span data-stu-id="3cb8f-126">Output:</span></span>

```bash
istening on port 80
::1 - - [27/Jul/2017:17:35:29 +0000] "HEAD / HTTP/1.1" 200 1663 "-" "curl/7.54.0"
::1 - - [27/Jul/2017:17:35:32 +0000] "HEAD / HTTP/1.1" 200 1663 "-" "curl/7.54.0"
::1 - - [27/Jul/2017:17:35:35 +0000] "HEAD / HTTP/1.1" 200 1663 "-" "curl/7.54.0"
::1 - - [27/Jul/2017:17:35:38 +0000] "HEAD / HTTP/1.1" 200 1663 "-" "curl/7.54.0"
```

<span data-ttu-id="3cb8f-127">Hallo toosee logboeken voor Hallo side auto-container, Hallo uitgevoerd dezelfde opdracht geven Hallo tweede containernaam.</span><span class="sxs-lookup"><span data-stu-id="3cb8f-127">toosee hello logs for hello side-car container, run hello same command specifying hello second container name.</span></span>

```azurecli-interactive
az container logs --name myContainerGroup --container-name aci-tutorial-sidecar --resource-group myResourceGroup
```

<span data-ttu-id="3cb8f-128">Uitvoer:</span><span class="sxs-lookup"><span data-stu-id="3cb8f-128">Output:</span></span>

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

<span data-ttu-id="3cb8f-129">Zoals u ziet, brengen Hallo ter periodiek een HTTP-aanvraag toohello hoofdweb toepassing via Hallo van de groep lokale netwerk tooensure dat deze wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="3cb8f-129">As you can see, hello sidecar is periodically making an HTTP request toohello main web application via hello group's local network tooensure that it is running.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3cb8f-130">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="3cb8f-130">Next steps</span></span>

<span data-ttu-id="3cb8f-131">Dit document besproken Hallo-stappen die nodig zijn voor het implementeren van een meerdere container exemplaar van Azure-container.</span><span class="sxs-lookup"><span data-stu-id="3cb8f-131">This document covered hello steps needed for deploying a multi-container Azure container instance.</span></span> <span data-ttu-id="3cb8f-132">Zie voor een end-tooend die containerexemplaren Azure-ervaring, hello Azure Containerexemplaren zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="3cb8f-132">For an end tooend Azure Container Instances experience, see hello Azure Container Instances tutorial.</span></span>

> [!div class="nextstepaction"]
> <span data-ttu-id="3cb8f-133">[Azure Containerexemplaren zelfstudie]:./container-instances-tutorial-prepare-app.md</span><span class="sxs-lookup"><span data-stu-id="3cb8f-133">[Azure Container Instances tutorial]: ./container-instances-tutorial-prepare-app.md</span></span>

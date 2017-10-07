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
# <a name="deploy-a-container-group"></a>Een containergroep implementeren

Azure Containerexemplaren ondersteuning Hallo-implementatie van meerdere containers naar één host met behulp van een *containergroep*. Dit is handig bij het bouwen van een toepassing ter voor logboekregistratie, bewaken of een andere configuratie waarbij een tweede gekoppelde proces in een service nodig heeft. 

Dit document helpt bij het uitvoeren van een eenvoudige meerdere container ter-configuratie met een Azure Resource Manager-sjabloon.

## <a name="configure-hello-template"></a>Hallo-sjabloon configureren

Maak een bestand met de naam `azuredeploy.json` en kopiëren Hallo json in het volgende. 

In dit voorbeeld wordt is een containergroep met twee containers en een openbare IP-adres gedefinieerd. Hallo eerste container van Hallo groep wordt een internettoepassing gerichte uitgevoerd. Hallo tweede container Hallo ter, kunt u een HTTP-aanvraag toohello hoofdweb toepassing via Hallo van de groep lokale netwerk. 

In dit voorbeeld ter mogelijk uitgebreide tootrigger een waarschuwing als er een HTTP-antwoordcode dan 200 OK ontvangen. 

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

een object toohello json-document toouse een register van de installatiekopie van privé-container toevoegen met de volgende indeling Hallo.

```json
"imageRegistryCredentials": [
    {
    "server": "[parameters('imageRegistryLoginServer')]",
    "username": "[parameters('imageRegistryUsername')]",
    "password": "[parameters('imageRegistryPassword')]"
    }
]
```

## <a name="deploy-hello-template"></a>Hallo-sjabloon implementeren

Een resourcegroep maken met de Hallo [az groep maken](/cli/azure/group#create) opdracht.

```azurecli-interactive
az group create --name myResourceGroup --location westus
```

Hallo sjabloon Hello implementeren [az implementatie maken](/cli/azure/group/deployment#create) opdracht.

```azurecli-interactive
az group deployment create --name myContainerGroup --resource-group myResourceGroup --template-file azuredeploy.json
```

Binnen enkele seconden ontvangt u een eerste reactie van Azure. 

## <a name="view-deployment-state"></a>Implementatiestatus weergeven

status van de tooview Hallo van Hallo-implementatie, gebruik Hallo `az container show` opdracht. Hiermee wordt ingericht Hallo openbaar IP-adres via welke Hallo toepassing toegankelijk zijn.

```azurecli-interactive
az container show --name myContainerGroup --resource-group myResourceGroup -o table
```

Uitvoer:

```azurecli
Name              ResourceGroup    ProvisioningState    Image                                                             IP:ports           CPU/Memory    OsType    Location
----------------  ---------------  -------------------  ----------------------------------------------------------------  -----------------  ------------  --------  ----------
myContainerGroup  myResourceGrou2  Succeeded            microsoft/aci-tutorial-sidecar,microsoft/aci-tutorial-app:v1      40.118.253.154:80  1.0 core/1.5 gb   Linux     westus
```

## <a name="view-logs"></a>Logboeken bekijken   

Hallo logboekuitvoer van een container met Hallo weergeven `az container logs` opdracht. Hallo `--container-name` geeft Hallo-container uit welke logboeken toopull argument. In dit voorbeeld wordt is de eerste container Hallo opgegeven. 

```azurecli-interactive
az container logs --name myContainerGroup --container-name aci-tutorial-app --resource-group myResourceGroup
```

Uitvoer:

```bash
istening on port 80
::1 - - [27/Jul/2017:17:35:29 +0000] "HEAD / HTTP/1.1" 200 1663 "-" "curl/7.54.0"
::1 - - [27/Jul/2017:17:35:32 +0000] "HEAD / HTTP/1.1" 200 1663 "-" "curl/7.54.0"
::1 - - [27/Jul/2017:17:35:35 +0000] "HEAD / HTTP/1.1" 200 1663 "-" "curl/7.54.0"
::1 - - [27/Jul/2017:17:35:38 +0000] "HEAD / HTTP/1.1" 200 1663 "-" "curl/7.54.0"
```

Hallo toosee logboeken voor Hallo side auto-container, Hallo uitgevoerd dezelfde opdracht geven Hallo tweede containernaam.

```azurecli-interactive
az container logs --name myContainerGroup --container-name aci-tutorial-sidecar --resource-group myResourceGroup
```

Uitvoer:

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

Zoals u ziet, brengen Hallo ter periodiek een HTTP-aanvraag toohello hoofdweb toepassing via Hallo van de groep lokale netwerk tooensure dat deze wordt uitgevoerd.

## <a name="next-steps"></a>Volgende stappen

Dit document besproken Hallo-stappen die nodig zijn voor het implementeren van een meerdere container exemplaar van Azure-container. Zie voor een end-tooend die containerexemplaren Azure-ervaring, hello Azure Containerexemplaren zelfstudie.

> [!div class="nextstepaction"]
> [Azure Containerexemplaren zelfstudie]:./container-instances-tutorial-prepare-app.md

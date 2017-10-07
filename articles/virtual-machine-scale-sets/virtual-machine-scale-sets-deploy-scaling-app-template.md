---
title: een app op een virtuele machine van Azure-schaalset aaaDeploy | Microsoft Docs
description: Meer informatie over toodeploy een toepassing eenvoudig automatisch schalen op een virtuele-machineschaalset ingesteld met een Azure Resource Manager-sjabloon.
services: virtual-machine-scale-sets
documentationcenter: 
author: rwike77
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/24/2017
ms.author: ryanwi
ms.openlocfilehash: 6fccc310312cabfcdddfcbcd2d154fc5cc440417
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-autoscaling-app-using-a-template"></a>Een automatisch schalende app implementeren met een sjabloon

[Azure Resource Manager-sjablonen](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#template-deployment) zijn een goede manier toodeploy groepen verwante resources. Deze zelfstudie bouwt voort op [implementeren van een eenvoudige schaalset](virtual-machine-scale-sets-mvss-start.md) en beschrijft hoe toodeploy een toepassing eenvoudig automatisch schalen op een schaal instelt met een Azure Resource Manager-sjabloon.  U kunt ook met behulp van PowerShell, CLI of Hallo portal automatisch schalen instellen. Zie het [overzicht van automatisch schalen](virtual-machine-scale-sets-autoscale-overview.md) voor meer informatie.

## <a name="two-quickstart-templates"></a>Twee snelstartsjablonen
Wanneer u een schaalset implementeert, kunt u nieuwe software installeren op een platforminstallatiekopie met een [VM-extensie](../virtual-machines/virtual-machines-windows-extensions-features.md). Een VM-extensie is een kleine toepassing waarmee configuratie- en automatiseringstaken na de implementatie worden uitgevoerd op virtuele Azure-machines, zoals het implementeren van een app. Twee verschillende voorbeeldsjablonen vindt u in [Azure/azure-Quick Start-sjablonen](https://github.com/Azure/azure-quickstart-templates) die laten zien hoe een toepassing automatisch schalen op een schaal toodeploy instelt met behulp van de VM-extensies.

### <a name="python-http-server-on-linux"></a>Python HTTP-server op Linux
Hallo [Python HTTP-server op Linux](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-bottle-autoscale) voorbeeldsjabloon implementeert een eenvoudige automatisch schalen toepassing die wordt uitgevoerd op een Linux-schaalset.  [Bottle](http://bottlepy.org/docs/dev/), een Python-web framework en een eenvoudige HTTP-server zijn geïmplementeerd op elke virtuele machine in Hallo scale ingesteld met een aangepast script VM-extensie. Hallo schaal instellen schalen wanneer gemiddelde CPU-gebruik over alle VM's groter dan 60 is % en ingeschaald omlaag wanneer de gemiddelde CPU-gebruik Hallo minder dan 30 is %.

Bovendien toohello schaalset resource hello *azuredeploy.json* voorbeeldsjabloon declareert ook virtueel netwerk, openbare IP-adres, load balancer en resources voor automatisch schalen-instellingen.  Zie [Linux-schaalset met automatisch schalen](virtual-machine-scale-sets-linux-autoscale.md) voor meer informatie over het maken van deze resources in een sjabloon.

In Hallo *azuredeploy.json* sjabloon, Hallo `extensionProfile` eigenschap Hallo `Microsoft.Compute/virtualMachineScaleSets` resource Hiermee geeft u een extensie voor aangepaste scripts. `fileUris`Hiermee geeft u Hallo script (s)-locatie. In dit geval twee bestanden: *workserver.py*, definieert een eenvoudige HTTP-server en *installserver.sh*, die Bottle wordt geïnstalleerd en gestart Hallo HTTP-server. `commandToExecute`Hiermee geeft u Hallo opdracht toorun na de implementatie van Hallo schaalset.

```json
          "extensionProfile": {
            "extensions": [
              {
                "name": "lapextension",
                "properties": {
                  "publisher": "Microsoft.Azure.Extensions",
                  "type": "CustomScript",
                  "typeHandlerVersion": "2.0",
                  "autoUpgradeMinorVersion": true,
                  "settings": {
                    "fileUris": [
                      "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vmss-bottle-autoscale/installserver.sh",
                      "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vmss-bottle-autoscale/workserver.py"
                    ],
                    "commandToExecute": "bash installserver.sh"
                  }
                }
              }
            ]
          }
```

### <a name="aspnet-mvc-application-on-windows"></a>ASP.NET MVC-toepassing in Windows
Hallo [ASP.NET MVC-toepassing op Windows](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-windows-webapp-dsc-autoscale) voorbeeldsjabloon implementeert een eenvoudige ASP.NET MVC-app in IIS wordt uitgevoerd op Windows-schaalset.  IIS en Hallo MVC-app zijn geïmplementeerd met Hallo [PowerShell desired state configuration (DSC)](virtual-machine-scale-sets-dsc.md) VM-extensie.  Hallo schaal instellen schalen (op het exemplaar van de virtuele machine tegelijk) wanneer het CPU-gebruik is groter dan 50% gedurende vijf minuten. 

Bovendien toohello schaalset resource hello *azuredeploy.json* voorbeeldsjabloon declareert ook virtueel netwerk, openbare IP-adres, load balancer en resources voor automatisch schalen-instellingen. In deze sjabloon kunt u ook een toepassingsupgrade bekijken.  Zie [Windows-schaalset met automatisch schalen](virtual-machine-scale-sets-windows-autoscale.md) voor meer informatie over het maken van deze resources in een sjabloon.

In Hallo *azuredeploy.json* sjabloon, Hallo `extensionProfile` eigenschap Hallo `Microsoft.Compute/virtualMachineScaleSets` resource geeft een [desired state configuration (DSC)](virtual-machine-scale-sets-dsc.md) -extensie die wordt geïnstalleerd, IIS en een standaardbericht Web-app uit een web Deploy-pakket.  Hallo *IISInstall.ps1* script IIS op Hallo virtuele machine installeert en is gevonden in Hallo *DSC* map.  Hallo MVC-web-app is gevonden in Hallo *WebDeploy* map.  Hallo paden toohello installatiescript en Hallo web-app zijn gedefinieerd in Hallo `powershelldscZip` en `webDeployPackage` parameters in Hallo *azuredeploy.parameters.json* bestand. 

```json
          "extensionProfile": {
            "extensions": [
              {
                "name": "Microsoft.Powershell.DSC",
                "properties": {
                  "publisher": "Microsoft.Powershell",
                  "type": "DSC",
                  "typeHandlerVersion": "2.9",
                  "autoUpgradeMinorVersion": true,
                  "forceUpdateTag": "[parameters('powershelldscUpdateTagVersion')]",
                  "settings": {
                    "configuration": {
                      "url": "[variables('powershelldscZipFullPath')]",
                      "script": "IISInstall.ps1",
                      "function": "InstallIIS"
                    },
                    "configurationArguments": {
                      "nodeName": "localhost",
                      "WebDeployPackagePath": "[variables('webDeployPackageFullPath')]"
                    }
                  }
                }
              }
            ]
          }
```

## <a name="deploy-hello-template"></a>Hallo-sjabloon implementeren
Hallo eenvoudigste manier toodeploy hello [Python HTTP-server op Linux](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-bottle-autoscale) of [ASP.NET MVC-toepassing op Windows](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-windows-webapp-dsc-autoscale) sjabloon is toouse hello **tooAzure implementeren** knop gevonden in Hallo in de Leesmij-bestanden Hallo in GitHub.  U kunt ook toodeploy Hallo voorbeeldsjablonen PowerShell of Azure CLI gebruiken.

### <a name="powershell"></a>PowerShell
Kopiëren Hallo [Python HTTP-server op Linux](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-bottle-autoscale) of [ASP.NET MVC-toepassing op Windows](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-windows-webapp-dsc-autoscale) bestanden uit Hallo GitHub-repo-tooa map op uw lokale computer.  Open Hallo *azuredeploy.parameters.json* bestands- en update Hallo standaardwaarden Hallo `vmssName`, `adminUsername`, en `adminPassword` parameters. Hallo volgende PowerShell-script op te slaan*deploy.ps1* in Hallo dezelfde map als Hallo *azuredeploy.json* sjabloon. toodeploy hello voorbeeld sjabloon uitvoeren Hallo *deploy.ps1* script vanaf een PowerShell-opdrachtvenster.

```powershell
param(
 [Parameter(Mandatory=$True)]
 [string]
 $subscriptionId,

 [Parameter(Mandatory=$True)]
 [string]
 $resourceGroupName,

 [string]
 $resourceGroupLocation,

 [Parameter(Mandatory=$True)]
 [string]
 $deploymentName,

 [string]
 $templateFilePath = "template.json",

 [string]
 $parametersFilePath = "parameters.json"
)

<#
.SYNOPSIS
    Registers RPs
#>
Function RegisterRP {
    Param(
        [string]$ResourceProviderNamespace
    )

    Write-Host "Registering resource provider '$ResourceProviderNamespace'";
    Register-AzureRmResourceProvider -ProviderNamespace $ResourceProviderNamespace;
}

#******************************************************************************
# Script body
# Execution begins here
#******************************************************************************
$ErrorActionPreference = "Stop"

# sign in
Write-Host "Logging in...";
Login-AzureRmAccount;

# select subscription
Write-Host "Selecting subscription '$subscriptionId'";
Select-AzureRmSubscription -SubscriptionID $subscriptionId;

# Register RPs
$resourceProviders = @("microsoft.compute","microsoft.insights","microsoft.network");
if($resourceProviders.length) {
    Write-Host "Registering resource providers"
    foreach($resourceProvider in $resourceProviders) {
        RegisterRP($resourceProvider);
    }
}

#Create or check for existing resource group
$resourceGroup = Get-AzureRmResourceGroup -Name $resourceGroupName -ErrorAction SilentlyContinue
if(!$resourceGroup)
{
    Write-Host "Resource group '$resourceGroupName' does not exist. toocreate a new resource group, please enter a location.";
    if(!$resourceGroupLocation) {
        $resourceGroupLocation = Read-Host "resourceGroupLocation";
    }
    Write-Host "Creating resource group '$resourceGroupName' in location '$resourceGroupLocation'";
    New-AzureRmResourceGroup -Name $resourceGroupName -Location $resourceGroupLocation
}
else{
    Write-Host "Using existing resource group '$resourceGroupName'";
}

# Start hello deployment
Write-Host "Starting deployment...";
if(Test-Path $parametersFilePath) {
    New-AzureRmResourceGroupDeployment -ResourceGroupName $resourceGroupName -TemplateFile $templateFilePath -TemplateParameterFile $parametersFilePath;
} else {
    New-AzureRmResourceGroupDeployment -ResourceGroupName $resourceGroupName -TemplateFile $templateFilePath;
}
```

### <a name="azure-cli"></a>Azure CLI
```azurecli
#!/bin/bash
set -euo pipefail
IFS=$'\n\t'

# -e: immediately exit if any command has a non-zero exit status
# -o: prevents errors in a pipeline from being masked
# IFS new value is less likely toocause confusing bugs when looping arrays or arguments (e.g. $@)

usage() { echo "Usage: $0 -i <subscriptionId> -g <resourceGroupName> -n <deploymentName> -l <resourceGroupLocation>" 1>&2; exit 1; }

declare subscriptionId=""
declare resourceGroupName=""
declare deploymentName=""
declare resourceGroupLocation=""

# Initialize parameters specified from command line
while getopts ":i:g:n:l:" arg; do
    case "${arg}" in
        i)
            subscriptionId=${OPTARG}
            ;;
        g)
            resourceGroupName=${OPTARG}
            ;;
        n)
            deploymentName=${OPTARG}
            ;;
        l)
            resourceGroupLocation=${OPTARG}
            ;;
        esac
done
shift $((OPTIND-1))

#Prompt for parameters is some required parameters are missing
if [[ -z "$subscriptionId" ]]; then
    echo "Subscription Id:"
    read subscriptionId
    [[ "${subscriptionId:?}" ]]
fi

if [[ -z "$resourceGroupName" ]]; then
    echo "ResourceGroupName:"
    read resourceGroupName
    [[ "${resourceGroupName:?}" ]]
fi

if [[ -z "$deploymentName" ]]; then
    echo "DeploymentName:"
    read deploymentName
fi

if [[ -z "$resourceGroupLocation" ]]; then
    echo "Enter a location below toocreate a new resource group else skip this"
    echo "ResourceGroupLocation:"
    read resourceGroupLocation
fi

#templateFile Path - template file toobe used
templateFilePath="template.json"

if [ ! -f "$templateFilePath" ]; then
    echo "$templateFilePath not found"
    exit 1
fi

#parameter file path
parametersFilePath="parameters.json"

if [ ! -f "$parametersFilePath" ]; then
    echo "$parametersFilePath not found"
    exit 1
fi

if [ -z "$subscriptionId" ] || [ -z "$resourceGroupName" ] || [ -z "$deploymentName" ]; then
    echo "Either one of subscriptionId, resourceGroupName, deploymentName is empty"
    usage
fi

#login tooazure using your credentials
az account show 1> /dev/null

if [ $? != 0 ];
then
    az login
fi

#set hello default subscription id
az account set --name $subscriptionId

set +e

#Check for existing RG
az group show $resourceGroupName 1> /dev/null

if [ $? != 0 ]; then
    echo "Resource group with name" $resourceGroupName "could not be found. Creating new resource group.."
    set -e
    (
        set -x
        az group create --name $resourceGroupName --location $resourceGroupLocation 1> /dev/null
    )
    else
    echo "Using existing resource group..."
fi

#Start deployment
echo "Starting deployment..."
(
    set -x
    az group deployment create --name $deploymentName --resource-group $resourceGroupName --template-file $templateFilePath --parameters $parametersFilePath
)

if [ $?  == 0 ];
 then
    echo "Template has been successfully deployed"
fi
```

## <a name="next-steps"></a>Volgende stappen

[!INCLUDE [mvss-next-steps-include](../../includes/mvss-next-steps.md)]

---
title: Een app implementeren op een virtuele-machineschaalset in Azure | Microsoft Docs
description: Informatie over het implementeren van een eenvoudige, automatisch schalende toepassing op een virtuele-machineschaalset met een Azure Resource Manager-sjabloon.
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
ms.openlocfilehash: 07883a33382cc660b043c99872312a9e77228253
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="deploy-an-autoscaling-app-using-a-template"></a><span data-ttu-id="08338-103">Een automatisch schalende app implementeren met een sjabloon</span><span class="sxs-lookup"><span data-stu-id="08338-103">Deploy an autoscaling app using a template</span></span>

<span data-ttu-id="08338-104">[Azure Resource Manager-sjablonen](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#template-deployment) zijn bijzonder handig om groepen gerelateerde resources te implementeren.</span><span class="sxs-lookup"><span data-stu-id="08338-104">[Azure Resource Manager templates](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#template-deployment) are a great way to deploy groups of related resources.</span></span> <span data-ttu-id="08338-105">In deze zelfstudie wordt verder ingegaan op [Een eenvoudige schaalset implementeren](virtual-machine-scale-sets-mvss-start.md) en wordt beschreven hoe u een eenvoudige, automatisch schalende toepassing kunt implementeren op een schaalset met een Azure Resource Manager-sjabloon.</span><span class="sxs-lookup"><span data-stu-id="08338-105">This tutorial builds on [Deploy a simple scale set](virtual-machine-scale-sets-mvss-start.md) and describes how to deploy a simple autoscaling application on a scale set using an Azure Resource Manager template.</span></span>  <span data-ttu-id="08338-106">U kunt automatisch schalen ook instellen met PowerShell, CLI of de portal.</span><span class="sxs-lookup"><span data-stu-id="08338-106">You can also set up autoscaling using PowerShell, CLI, or the portal.</span></span> <span data-ttu-id="08338-107">Zie het [overzicht van automatisch schalen](virtual-machine-scale-sets-autoscale-overview.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="08338-107">For more information, see [Autoscale overview](virtual-machine-scale-sets-autoscale-overview.md).</span></span>

## <a name="two-quickstart-templates"></a><span data-ttu-id="08338-108">Twee snelstartsjablonen</span><span class="sxs-lookup"><span data-stu-id="08338-108">Two quickstart templates</span></span>
<span data-ttu-id="08338-109">Wanneer u een schaalset implementeert, kunt u nieuwe software installeren op een platforminstallatiekopie met een [VM-extensie](../virtual-machines/virtual-machines-windows-extensions-features.md).</span><span class="sxs-lookup"><span data-stu-id="08338-109">When you deploy a scale set you can install new software on a platform image using a [VM Extension](../virtual-machines/virtual-machines-windows-extensions-features.md).</span></span> <span data-ttu-id="08338-110">Een VM-extensie is een kleine toepassing waarmee configuratie- en automatiseringstaken na de implementatie worden uitgevoerd op virtuele Azure-machines, zoals het implementeren van een app.</span><span class="sxs-lookup"><span data-stu-id="08338-110">A VM extension is a small application that provides post-deployment configuration and automation tasks on Azure virtual machines, such as deploying an app.</span></span> <span data-ttu-id="08338-111">In [Azure/azure-quickstart-templates](https://github.com/Azure/azure-quickstart-templates) vindt u twee voorbeeldsjablonen waarin u kunt zien hoe u een automatisch schalende toepassing implementeert op een schaalset met VM-extensies.</span><span class="sxs-lookup"><span data-stu-id="08338-111">Two different sample templates are provided in [Azure/azure-quickstart-templates](https://github.com/Azure/azure-quickstart-templates) which show how to deploy an autoscaling application onto a scale set using VM extensions.</span></span>

### <a name="python-http-server-on-linux"></a><span data-ttu-id="08338-112">Python HTTP-server op Linux</span><span class="sxs-lookup"><span data-stu-id="08338-112">Python HTTP server on Linux</span></span>
<span data-ttu-id="08338-113">Met de voorbeeldsjabloon [Python HTTP-server op Linux](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-bottle-autoscale) wordt een eenvoudige, automatisch schalende toepassing geïmplementeerd die wordt uitgevoerd op een Linux-schaalset.</span><span class="sxs-lookup"><span data-stu-id="08338-113">The [Python HTTP server on Linux](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-bottle-autoscale) sample template deploys a simple autoscaling application running on a Linux scale set.</span></span>  <span data-ttu-id="08338-114">Op elke VM in de schaalset worden [Bottle](http://bottlepy.org/docs/dev/), een Python-webframework, en een eenvoudige HTTP-server geïmplementeerd met behulp van een VM-extensie met een aangepast script.</span><span class="sxs-lookup"><span data-stu-id="08338-114">[Bottle](http://bottlepy.org/docs/dev/), a Python web framework, and a simple HTTP server are deployed on each VM in the scale set using a custom script VM extension.</span></span> <span data-ttu-id="08338-115">De schaalset schaalt omhoog wanneer gemiddeld CPU-gebruik over alle VM's hoger is dan 60% en schaalt omlaag wanneer het gemiddelde CPU-gebruik lager is dan 30%.</span><span class="sxs-lookup"><span data-stu-id="08338-115">The scale set scales up when average CPU utilization across all VMs is greater than 60% and scales down when the average CPU utilization is less than 30%.</span></span>

<span data-ttu-id="08338-116">Naast de schaalsetresource worden met de voorbeeldsjabloon *azuredeploy.json* ook de resources voor het virtuele netwerk, het openbare IP-adres, de load balancer en instellingen voor automatisch schalen gedeclareerd.</span><span class="sxs-lookup"><span data-stu-id="08338-116">In addition to the scale set resource, the *azuredeploy.json* sample template also declares virtual network, public IP address, load balancer, and autoscale settings resources.</span></span>  <span data-ttu-id="08338-117">Zie [Linux-schaalset met automatisch schalen](virtual-machine-scale-sets-linux-autoscale.md) voor meer informatie over het maken van deze resources in een sjabloon.</span><span class="sxs-lookup"><span data-stu-id="08338-117">For more information on creating these resources in a template, see [Linux scale set with autoscale](virtual-machine-scale-sets-linux-autoscale.md).</span></span>

<span data-ttu-id="08338-118">In de sjabloon *azuredeploy.json* wordt met de eigenschap `extensionProfile` van de resource `Microsoft.Compute/virtualMachineScaleSets` een aangepaste scriptextensie opgegeven.</span><span class="sxs-lookup"><span data-stu-id="08338-118">In the *azuredeploy.json* template, the `extensionProfile` property of the `Microsoft.Compute/virtualMachineScaleSets` resource specifies a custom script extension.</span></span> <span data-ttu-id="08338-119">`fileUris` geeft de locatie van het script/de scripts aan.</span><span class="sxs-lookup"><span data-stu-id="08338-119">`fileUris` specifies the script(s) location.</span></span> <span data-ttu-id="08338-120">Dat zijn in dit geval twee bestanden: *workserver.py*, waarmee een eenvoudige HTTP-server wordt gedefinieerd, en *installserver.sh*, waarmee Bottle wordt geïnstalleerd en de HTTP-server wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="08338-120">In this case, two files: *workserver.py*, which defines a simple HTTP server, and *installserver.sh*, which installs Bottle and starts the HTTP server.</span></span> <span data-ttu-id="08338-121">`commandToExecute` geeft de opdracht aan die moet worden uitgevoerd nadat de schaalset is geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="08338-121">`commandToExecute` specifies the command to run after the scale set has been deployed.</span></span>

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

### <a name="aspnet-mvc-application-on-windows"></a><span data-ttu-id="08338-122">ASP.NET MVC-toepassing in Windows</span><span class="sxs-lookup"><span data-stu-id="08338-122">ASP.NET MVC application on Windows</span></span>
<span data-ttu-id="08338-123">Met de voorbeeldsjabloon [ASP.NET MVC-toepassing in Windows](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-windows-webapp-dsc-autoscale) wordt een eenvoudige ASP.NET MVC-app geïmplementeerd die wordt uitgevoerd in IIS op een Windows-schaalset.</span><span class="sxs-lookup"><span data-stu-id="08338-123">The [ASP.NET MVC application on Windows](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-windows-webapp-dsc-autoscale) sample template deploys a simple ASP.NET MVC app running in IIS on Windows scale set.</span></span>  <span data-ttu-id="08338-124">IIS en de MVC-app worden geïmplementeerd met de VM-extensie [PowerShell Desired State Configuration (DSC)](virtual-machine-scale-sets-dsc.md).</span><span class="sxs-lookup"><span data-stu-id="08338-124">IIS and the MVC app are deployed using the [PowerShell desired state configuration (DSC)](virtual-machine-scale-sets-dsc.md) VM extension.</span></span>  <span data-ttu-id="08338-125">De schaalset schaalt omhoog (één VM-exemplaar tegelijk) wanneer het CPU-gebruik gedurende vijf minuten hoger is dan 50%.</span><span class="sxs-lookup"><span data-stu-id="08338-125">The scale set scales up (on VM instance at a time) when CPU utilization is greater than 50% for 5 minutes.</span></span> 

<span data-ttu-id="08338-126">Naast de schaalsetresource worden met de voorbeeldsjabloon *azuredeploy.json* ook de resources voor het virtuele netwerk, het openbare IP-adres, de load balancer en instellingen voor automatisch schalen gedeclareerd.</span><span class="sxs-lookup"><span data-stu-id="08338-126">In addition to the scale set resource, the *azuredeploy.json* sample template also declares virtual network, public IP address, load balancer, and autoscale settings resources.</span></span> <span data-ttu-id="08338-127">In deze sjabloon kunt u ook een toepassingsupgrade bekijken.</span><span class="sxs-lookup"><span data-stu-id="08338-127">This template also demonstrates application upgrade.</span></span>  <span data-ttu-id="08338-128">Zie [Windows-schaalset met automatisch schalen](virtual-machine-scale-sets-windows-autoscale.md) voor meer informatie over het maken van deze resources in een sjabloon.</span><span class="sxs-lookup"><span data-stu-id="08338-128">For more information on creating these resources in a template, see [Windows scale set with autoscale](virtual-machine-scale-sets-windows-autoscale.md).</span></span>

<span data-ttu-id="08338-129">In de sjabloon *azuredeploy.json* wordt met de eigenschap `extensionProfile` van de resource `Microsoft.Compute/virtualMachineScaleSets` een [Desired State Configuration](virtual-machine-scale-sets-dsc.md)-extensie (DSC) opgegeven waarmee IIS en een standaardweb-app worden geïnstalleerd vanuit een WebDeploy-pakket.</span><span class="sxs-lookup"><span data-stu-id="08338-129">In the *azuredeploy.json* template, the `extensionProfile` property of the `Microsoft.Compute/virtualMachineScaleSets` resource specifies a [desired state configuration (DSC)](virtual-machine-scale-sets-dsc.md) extension which installs IIS and a default web app from a WebDeploy package.</span></span>  <span data-ttu-id="08338-130">Met het script *IISInstall.ps1* wordt IIS geïnstalleerd op de virtuele machine. Dit script kunt u vinden in de map *DSC*.</span><span class="sxs-lookup"><span data-stu-id="08338-130">The *IISInstall.ps1* script installs IIS on the virtual machine and is found in the *DSC* folder.</span></span>  <span data-ttu-id="08338-131">De MVC-web-app bevindt zich in de map *WebDeploy*.</span><span class="sxs-lookup"><span data-stu-id="08338-131">The MVC web app is found in the *WebDeploy* folder.</span></span>  <span data-ttu-id="08338-132">De paden naar het installatiescript en de web-app zijn gedefinieerd in de parameters `powershelldscZip` en `webDeployPackage` in het bestand *azuredeploy.parameters.json*.</span><span class="sxs-lookup"><span data-stu-id="08338-132">The paths to the install script and the web app are defined in the `powershelldscZip` and `webDeployPackage` parameters in the *azuredeploy.parameters.json* file.</span></span> 

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

## <a name="deploy-the-template"></a><span data-ttu-id="08338-133">De sjabloon implementeren</span><span class="sxs-lookup"><span data-stu-id="08338-133">Deploy the template</span></span>
<span data-ttu-id="08338-134">U kunt de sjabloon [Python HTTP-server op Linux](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-bottle-autoscale) of [ASP.NET MVC-toepassing in Windows](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-windows-webapp-dsc-autoscale) het eenvoudigst implementeren met de knop **Implementeren in Azure** in de Leesmij-bestanden in GitHub.</span><span class="sxs-lookup"><span data-stu-id="08338-134">The simplest way to deploy the [Python HTTP server on Linux](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-bottle-autoscale) or [ASP.NET MVC application on Windows](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-windows-webapp-dsc-autoscale) template is to use the **Deploy to Azure** button found in the in the readme files in GitHub.</span></span>  <span data-ttu-id="08338-135">U kunt ook PowerShell of Azure CLI gebruiken om de voorbeeldsjablonen te implementeren.</span><span class="sxs-lookup"><span data-stu-id="08338-135">You can also use PowerShell or Azure CLI to deploy the sample templates.</span></span>

### <a name="powershell"></a><span data-ttu-id="08338-136">PowerShell</span><span class="sxs-lookup"><span data-stu-id="08338-136">PowerShell</span></span>
<span data-ttu-id="08338-137">Kopieer de bestanden voor [Python HTTP-server op Linux](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-bottle-autoscale) of [ASP.NET MVC-toepassing in Windows](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-windows-webapp-dsc-autoscale) van de GitHub-opslagplaats naar een map op uw lokale computer.</span><span class="sxs-lookup"><span data-stu-id="08338-137">Copy the [Python HTTP server on Linux](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-bottle-autoscale) or [ASP.NET MVC application on Windows](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-windows-webapp-dsc-autoscale) files from the GitHub repo to a folder on your local computer.</span></span>  <span data-ttu-id="08338-138">Open het bestand *azuredeploy.parameters.json* en werk de standaardwaarden van de parameters `vmssName`, `adminUsername` en `adminPassword` bij.</span><span class="sxs-lookup"><span data-stu-id="08338-138">Open the *azuredeploy.parameters.json* file and update the default values of the `vmssName`, `adminUsername`, and `adminPassword` parameters.</span></span> <span data-ttu-id="08338-139">Sla het volgende PowerShell-script op als *deploy.ps1*, in dezelfde map als de sjabloon *azuredeploy.json*.</span><span class="sxs-lookup"><span data-stu-id="08338-139">Save the following PowerShell script to *deploy.ps1* in the same folder as the *azuredeploy.json* template.</span></span> <span data-ttu-id="08338-140">Als u de voorbeeldsjabloon wilt implementeren, voert u het script *deploy.ps1* uit vanuit een PowerShell-opdrachtvenster.</span><span class="sxs-lookup"><span data-stu-id="08338-140">To deploy the sample template run the *deploy.ps1* script from a PowerShell command window.</span></span>

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
    Write-Host "Resource group '$resourceGroupName' does not exist. To create a new resource group, please enter a location.";
    if(!$resourceGroupLocation) {
        $resourceGroupLocation = Read-Host "resourceGroupLocation";
    }
    Write-Host "Creating resource group '$resourceGroupName' in location '$resourceGroupLocation'";
    New-AzureRmResourceGroup -Name $resourceGroupName -Location $resourceGroupLocation
}
else{
    Write-Host "Using existing resource group '$resourceGroupName'";
}

# Start the deployment
Write-Host "Starting deployment...";
if(Test-Path $parametersFilePath) {
    New-AzureRmResourceGroupDeployment -ResourceGroupName $resourceGroupName -TemplateFile $templateFilePath -TemplateParameterFile $parametersFilePath;
} else {
    New-AzureRmResourceGroupDeployment -ResourceGroupName $resourceGroupName -TemplateFile $templateFilePath;
}
```

### <a name="azure-cli"></a><span data-ttu-id="08338-141">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="08338-141">Azure CLI</span></span>
```azurecli
#!/bin/bash
set -euo pipefail
IFS=$'\n\t'

# -e: immediately exit if any command has a non-zero exit status
# -o: prevents errors in a pipeline from being masked
# IFS new value is less likely to cause confusing bugs when looping arrays or arguments (e.g. $@)

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
    echo "Enter a location below to create a new resource group else skip this"
    echo "ResourceGroupLocation:"
    read resourceGroupLocation
fi

#templateFile Path - template file to be used
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

#login to azure using your credentials
az account show 1> /dev/null

if [ $? != 0 ];
then
    az login
fi

#set the default subscription id
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

## <a name="next-steps"></a><span data-ttu-id="08338-142">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="08338-142">Next steps</span></span>

[!INCLUDE [mvss-next-steps-include](../../includes/mvss-next-steps.md)]

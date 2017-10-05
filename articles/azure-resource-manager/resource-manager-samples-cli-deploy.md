---
title: Azure CLI-Script steekproef - sjabloon implementeren | Microsoft Docs
description: Voorbeeld van een script voor het implementeren van een Azure Resource Manager-sjabloon.
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: azure-resource-manager
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/19/2017
ms.author: tomfitz
ms.openlocfilehash: 974230f349aec46fde58e69658e05a13bff4296f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-resource-manager-template-deployment---azure-cli-script"></a><span data-ttu-id="1c17a-103">Azure Resource Manager sjabloonimplementatie - script voor Azure CLI</span><span class="sxs-lookup"><span data-stu-id="1c17a-103">Azure Resource Manager template deployment - Azure CLI script</span></span>

<span data-ttu-id="1c17a-104">Dit script implementeert u een Resource Manager-sjabloon naar een resourcegroep in uw abonnement.</span><span class="sxs-lookup"><span data-stu-id="1c17a-104">This script deploys a Resource Manager template to a resource group in your subscription.</span></span>

[!INCLUDE [sample-cli-install](../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="1c17a-105">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="1c17a-105">Sample script</span></span>

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
az account set --subscription $subscriptionId

#Check for existing RG
if [ $(az group exists --name $resourceGroupName) == 'false' ]; then
    echo "Resource group with name" $resourceGroupName "could not be found. Creating new resource group.."
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

## <a name="clean-up-deployment"></a><span data-ttu-id="1c17a-106">Opschonen van implementatie</span><span class="sxs-lookup"><span data-stu-id="1c17a-106">Clean up deployment</span></span> 

<span data-ttu-id="1c17a-107">Voer de volgende opdracht om te verwijderen van de resourcegroep en alle bijbehorende resources.</span><span class="sxs-lookup"><span data-stu-id="1c17a-107">Run the following command to remove the resource group and all its resources.</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="1c17a-108">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="1c17a-108">Script explanation</span></span>

<span data-ttu-id="1c17a-109">Dit script maakt gebruik van de volgende opdrachten om de implementatie te maken.</span><span class="sxs-lookup"><span data-stu-id="1c17a-109">This script uses the following commands to create the deployment.</span></span> <span data-ttu-id="1c17a-110">Elk item in de tabel is gekoppeld aan de specifieke documentatie opdracht.</span><span class="sxs-lookup"><span data-stu-id="1c17a-110">Each item in the table links to command specific documentation.</span></span>

| <span data-ttu-id="1c17a-111">Opdracht</span><span class="sxs-lookup"><span data-stu-id="1c17a-111">Command</span></span> | <span data-ttu-id="1c17a-112">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="1c17a-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="1c17a-113">AZ groep bestaat</span><span class="sxs-lookup"><span data-stu-id="1c17a-113">az group exists</span></span>](/cli/azure/group#exists) | <span data-ttu-id="1c17a-114">Controleert of de brongroep bestaat.</span><span class="sxs-lookup"><span data-stu-id="1c17a-114">Checks whether resource group exists.</span></span> |
| [<span data-ttu-id="1c17a-115">AZ groep maken</span><span class="sxs-lookup"><span data-stu-id="1c17a-115">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="1c17a-116">Maakt een resourcegroep waarin alle resources worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="1c17a-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="1c17a-117">implementatie van AZ groep maken</span><span class="sxs-lookup"><span data-stu-id="1c17a-117">az group deployment create</span></span>](/cli/azure/group/deployment#create) | <span data-ttu-id="1c17a-118">Start een implementatie.</span><span class="sxs-lookup"><span data-stu-id="1c17a-118">Start a deployment.</span></span>  |
| [<span data-ttu-id="1c17a-119">AZ groep verwijderen</span><span class="sxs-lookup"><span data-stu-id="1c17a-119">az group delete</span></span>](/cli/azure/group#delete) | <span data-ttu-id="1c17a-120">Hiermee verwijdert u een resourcegroep met inbegrip van de bijhorende resources.</span><span class="sxs-lookup"><span data-stu-id="1c17a-120">Deletes a resource group including all its resources.</span></span> |



## <a name="next-steps"></a><span data-ttu-id="1c17a-121">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="1c17a-121">Next steps</span></span>
* <span data-ttu-id="1c17a-122">Zie voor een inleiding tot het implementeren van sjablonen [implementeren van resources met Resource Manager-sjablonen en Azure PowerShell](resource-group-template-deploy-cli.md).</span><span class="sxs-lookup"><span data-stu-id="1c17a-122">For an introduction to deploying templates, see [Deploy resources with Resource Manager templates and Azure PowerShell](resource-group-template-deploy-cli.md).</span></span>
* <span data-ttu-id="1c17a-123">Zie voor meer informatie over het implementeren van een sjabloon waarvoor een SAS-token [persoonlijke sjabloon implementeren met SAS-token](resource-manager-cli-sas-token.md).</span><span class="sxs-lookup"><span data-stu-id="1c17a-123">For information about deploying a template that requires a SAS token, see [Deploy private template with SAS token](resource-manager-cli-sas-token.md).</span></span>
* <span data-ttu-id="1c17a-124">Om parameters te definiëren in de sjabloon, Zie [sjablonen](resource-group-authoring-templates.md#parameters).</span><span class="sxs-lookup"><span data-stu-id="1c17a-124">To define parameters in template, see [Authoring templates](resource-group-authoring-templates.md#parameters).</span></span>
* <span data-ttu-id="1c17a-125">Voor begeleiding bij de manier waarop ondernemingen Resource Manager effectief kunnen gebruiken voor het beheer van abonnementen, gaat u naar [Azure enterprise-platform - Prescriptieve abonnementsgovernance](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="1c17a-125">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>


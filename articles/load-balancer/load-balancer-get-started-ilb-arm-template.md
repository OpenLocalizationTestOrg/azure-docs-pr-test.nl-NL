---
title: aaaCreate een interne load balancer - Azure-sjabloon | Microsoft Docs
description: Meer informatie over hoe toocreate een interne load balancer met een sjabloon in Resource Manager
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-resource-manager
ms.assetid: 64150862-6ced-42de-85dc-89d323257d7c
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 3ffa8178b863367cd79e2bc2b7ce4e45b23267e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-internal-load-balancer-using-a-template"></a><span data-ttu-id="84a92-103">Een interne load balancer maken met behulp van een sjabloon</span><span class="sxs-lookup"><span data-stu-id="84a92-103">Create an internal load balancer using a template</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="84a92-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="84a92-104">Azure Portal</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-portal.md)
> * [<span data-ttu-id="84a92-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="84a92-105">PowerShell</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-ps.md)
> * [<span data-ttu-id="84a92-106">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="84a92-106">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-cli.md)
> * [<span data-ttu-id="84a92-107">Sjabloon</span><span class="sxs-lookup"><span data-stu-id="84a92-107">Template</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-template.md)

[!INCLUDE [load-balancer-get-started-ilb-intro-include.md](../../includes/load-balancer-get-started-ilb-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="84a92-108">Azure heeft twee verschillende implementatiemodellen voor het maken van en werken met resources: [Resource Manager en het klassieke model](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="84a92-108">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="84a92-109">In dit artikel wordt beschreven hoe u Hallo Resource Manager-implementatiemodel, die Microsoft voor de meeste nieuwe implementaties in plaats van Hallo aanbeveelt [klassieke implementatiemodel](load-balancer-get-started-ilb-classic-ps.md).</span><span class="sxs-lookup"><span data-stu-id="84a92-109">This article covers using hello Resource Manager deployment model, which Microsoft recommends for most new deployments instead of hello [classic deployment model](load-balancer-get-started-ilb-classic-ps.md).</span></span>

[!INCLUDE [load-balancer-get-started-ilb-scenario-include.md](../../includes/load-balancer-get-started-ilb-scenario-include.md)]

## <a name="deploy-hello-template-by-using-click-toodeploy"></a><span data-ttu-id="84a92-110">Hallo-sjabloon implementeren met Klik toodeploy</span><span class="sxs-lookup"><span data-stu-id="84a92-110">Deploy hello template by using click toodeploy</span></span>

<span data-ttu-id="84a92-111">Hallo voorbeeldsjabloon beschikbaar in de openbare opslagplaats Hallo maakt gebruik van een parameterbestand met Hallo standaard waarden gebruikt toogenerate Hallo scenario die hierboven worden beschreven.</span><span class="sxs-lookup"><span data-stu-id="84a92-111">hello sample template available in hello public repository uses a parameter file containing hello default values used toogenerate hello scenario described above.</span></span> <span data-ttu-id="84a92-112">toodeploy toodeploy, het gebruik van deze sjabloon Klik Volg [deze koppeling](https://github.com/Azure/azure-quickstart-templates/tree/master/201-2-vms-internal-load-balancer), klikt u op **tooAzure implementeren**, vervang Hallo standaardparameterwaarden indien nodig en volg de instructies Hallo in Hallo-portal.</span><span class="sxs-lookup"><span data-stu-id="84a92-112">toodeploy this template using click toodeploy, follow [this link](https://github.com/Azure/azure-quickstart-templates/tree/master/201-2-vms-internal-load-balancer), click **Deploy tooAzure**, replace hello default parameter values if necessary, and follow hello instructions in hello portal.</span></span>

## <a name="deploy-hello-template-by-using-powershell"></a><span data-ttu-id="84a92-113">Hallo-sjabloon implementeren met behulp van PowerShell</span><span class="sxs-lookup"><span data-stu-id="84a92-113">Deploy hello template by using PowerShell</span></span>

<span data-ttu-id="84a92-114">toodeploy hello sjabloon die u hebt gedownload met behulp van PowerShell, Hallo volgende stappen.</span><span class="sxs-lookup"><span data-stu-id="84a92-114">toodeploy hello template you downloaded by using PowerShell, follow hello steps below.</span></span>

1. <span data-ttu-id="84a92-115">Als u Azure PowerShell nog nooit hebt gebruikt, raadpleegt u [hoe tooInstall en configureer Azure PowerShell](/powershell/azure/overview) en volg de instructies Hallo alle Hallo manier toohello toosign beëindigen in Azure en uw abonnement te selecteren.</span><span class="sxs-lookup"><span data-stu-id="84a92-115">If you have never used Azure PowerShell, see [How tooInstall and Configure Azure PowerShell](/powershell/azure/overview) and follow hello instructions all hello way toohello end toosign into Azure and select your subscription.</span></span>
2. <span data-ttu-id="84a92-116">Download Hallo parameters tooyour lokale schijf.</span><span class="sxs-lookup"><span data-stu-id="84a92-116">Download hello parameters file tooyour local disk.</span></span>
3. <span data-ttu-id="84a92-117">Hallo-bestand bewerken en opslaan.</span><span class="sxs-lookup"><span data-stu-id="84a92-117">Edit hello file and save it.</span></span>
4. <span data-ttu-id="84a92-118">Voer Hallo **New-AzureRmResourceGroupDeployment** cmdlet toocreate een resource-groep met Hallo sjabloon.</span><span class="sxs-lookup"><span data-stu-id="84a92-118">Run hello **New-AzureRmResourceGroupDeployment** cmdlet toocreate a resource group using hello template.</span></span>

    ```azurecli
    New-AzureRmResourceGroupDeployment -Name TestRG -Location westus `
        -TemplateFile 'https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-2-vms-internal-load-balancer/azuredeploy.json' `
        -TemplateParameterFile 'C:\temp\azuredeploy.parameters.json'
    ```

## <a name="deploy-hello-template-by-using-hello-azure-cli"></a><span data-ttu-id="84a92-119">Hallo-sjabloon implementeren met hello Azure CLI</span><span class="sxs-lookup"><span data-stu-id="84a92-119">Deploy hello template by using hello Azure CLI</span></span>

<span data-ttu-id="84a92-120">toodeploy hello sjabloon via Azure CLI Hallo Hallo volgende stappen.</span><span class="sxs-lookup"><span data-stu-id="84a92-120">toodeploy hello template by using hello Azure CLI, follow hello steps below.</span></span>

1. <span data-ttu-id="84a92-121">Als u Azure CLI nog nooit hebt gebruikt, raadpleegt u [installeren en configureren van Azure CLI Hallo](../cli-install-nodejs.md) en volg de instructies Hallo toohello punt waar u uw Azure-account en abonnement selecteren.</span><span class="sxs-lookup"><span data-stu-id="84a92-121">If you have never used Azure CLI, see [Install and Configure hello Azure CLI](../cli-install-nodejs.md) and follow hello instructions up toohello point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="84a92-122">Voer Hallo **azure config mode** opdracht tooswitch tooResource modus Manager, zoals hieronder wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="84a92-122">Run hello **azure config mode** command tooswitch tooResource Manager mode, as shown below.</span></span>

    ```azurecli
    azure config mode arm
    ```

    <span data-ttu-id="84a92-123">Dit is verwacht Hallo uitvoer voor Hallo bovenstaande opdracht:</span><span class="sxs-lookup"><span data-stu-id="84a92-123">Here is hello expected output for hello command above:</span></span>

        info:    New mode is arm

3. <span data-ttu-id="84a92-124">Hallo parameterbestand openen, selecteer de inhoud en tooa bestand opslaan op uw computer.</span><span class="sxs-lookup"><span data-stu-id="84a92-124">Open hello parameter file, select its contents, and save it tooa file in your computer.</span></span> <span data-ttu-id="84a92-125">In dit voorbeeld is opgeslagen Hallo parameterbestand te*parameters.json*.</span><span class="sxs-lookup"><span data-stu-id="84a92-125">For this example, we saved hello parameters file too*parameters.json*.</span></span>
4. <span data-ttu-id="84a92-126">Voer Hallo **implementatie van de azure-groep maken** opdracht toodeploy Hallo nieuwe interne taakverdeling met behulp van Hallo sjabloon en de parameterbestanden die u hebt gedownload en hierboven zijn gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="84a92-126">Run hello **azure group deployment create** command toodeploy hello new internal load balancer by using hello template and parameter files you downloaded and modified above.</span></span> <span data-ttu-id="84a92-127">Hallo-lijst die wordt weergegeven na Hallo uitvoer wordt uitgelegd Hallo parameters die worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="84a92-127">hello list shown after hello output explains hello parameters used.</span></span>

    ```azurecli
    azure group create --name TestRG --location westus --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-2-vms-internal-load-balancer/azuredeploy.json --parameters-file parameters.json
    ```

## <a name="next-steps"></a><span data-ttu-id="84a92-128">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="84a92-128">Next steps</span></span>

[<span data-ttu-id="84a92-129">Een distributiemodus voor de load balancer configureren met bron-IP-affiniteit</span><span class="sxs-lookup"><span data-stu-id="84a92-129">Configure a load balancer distribution mode using source IP affinity</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="84a92-130">TCP-time-outinstellingen voor inactiviteit voor de load balancer configureren</span><span class="sxs-lookup"><span data-stu-id="84a92-130">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)


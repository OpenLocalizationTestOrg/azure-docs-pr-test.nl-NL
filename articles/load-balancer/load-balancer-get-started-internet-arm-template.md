---
title: aaaCreate een internetgerichte load balancer - Azure-sjabloon | Microsoft Docs
description: Meer informatie over hoe de toocreate een Internet gerichte load balancer in Resource Manager, met een sjabloon
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-resource-manager
ms.assetid: b24f4729-4559-4458-8527-71009d242647
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 2bce8cb87303838f3bc732d51228ab46d8015552
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="creating-an-internet-facing-load-balancer-using-a-template"></a><span data-ttu-id="53ba4-103">Aan de slag met het maken van een internetgerichte load balancer met een sjabloon</span><span class="sxs-lookup"><span data-stu-id="53ba4-103">Creating an Internet facing load balancer using a template</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="53ba4-104">Portal</span><span class="sxs-lookup"><span data-stu-id="53ba4-104">Portal</span></span>](../load-balancer/load-balancer-get-started-internet-portal.md)
> * [<span data-ttu-id="53ba4-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="53ba4-105">PowerShell</span></span>](../load-balancer/load-balancer-get-started-internet-arm-ps.md)
> * [<span data-ttu-id="53ba4-106">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="53ba4-106">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-internet-arm-cli.md)
> * [<span data-ttu-id="53ba4-107">Sjabloon</span><span class="sxs-lookup"><span data-stu-id="53ba4-107">Template</span></span>](../load-balancer/load-balancer-get-started-internet-arm-template.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="53ba4-108">In dit artikel bevat informatie over Hallo Resource Manager-implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="53ba4-108">This article covers hello Resource Manager deployment model.</span></span> <span data-ttu-id="53ba4-109">U kunt ook [meer informatie over hoe een internetverbinding toocreate netwerktaakverdeler met klassieke implementatiemodel](load-balancer-get-started-internet-classic-portal.md)</span><span class="sxs-lookup"><span data-stu-id="53ba4-109">You can also [Learn how toocreate an Internet facing load balancer using classic deployment model](load-balancer-get-started-internet-classic-portal.md)</span></span>

[!INCLUDE [load-balancer-get-started-internet-scenario-include.md](../../includes/load-balancer-get-started-internet-scenario-include.md)]

## <a name="deploy-hello-template-by-using-click-toodeploy"></a><span data-ttu-id="53ba4-110">Hallo-sjabloon implementeren met Klik toodeploy</span><span class="sxs-lookup"><span data-stu-id="53ba4-110">Deploy hello template by using click toodeploy</span></span>

<span data-ttu-id="53ba4-111">Hallo voorbeeldsjabloon beschikbaar in de openbare opslagplaats Hallo maakt gebruik van een parameterbestand met Hallo standaard waarden gebruikt toogenerate Hallo scenario die hierboven worden beschreven.</span><span class="sxs-lookup"><span data-stu-id="53ba4-111">hello sample template available in hello public repository uses a parameter file containing hello default values used toogenerate hello scenario described above.</span></span> <span data-ttu-id="53ba4-112">toodeploy toodeploy, het gebruik van deze sjabloon Klik Volg [deze koppeling](http://go.microsoft.com/fwlink/?LinkId=544801), klikt u op **tooAzure implementeren**, vervang Hallo standaardparameterwaarden indien nodig en volg de instructies Hallo in Hallo-portal.</span><span class="sxs-lookup"><span data-stu-id="53ba4-112">toodeploy this template using click toodeploy, follow [this link](http://go.microsoft.com/fwlink/?LinkId=544801), click **Deploy tooAzure**, replace hello default parameter values if necessary, and follow hello instructions in hello portal.</span></span>

## <a name="deploy-hello-template-by-using-powershell"></a><span data-ttu-id="53ba4-113">Hallo-sjabloon implementeren met behulp van PowerShell</span><span class="sxs-lookup"><span data-stu-id="53ba4-113">Deploy hello template by using PowerShell</span></span>

<span data-ttu-id="53ba4-114">toodeploy hello sjabloon die u hebt gedownload met behulp van PowerShell, Hallo volgende stappen.</span><span class="sxs-lookup"><span data-stu-id="53ba4-114">toodeploy hello template you downloaded by using PowerShell, follow hello steps below.</span></span>

1. <span data-ttu-id="53ba4-115">Als u Azure PowerShell nog nooit hebt gebruikt, raadpleegt u [hoe tooInstall en configureer Azure PowerShell](/powershell/azure/overview) en volg de instructies Hallo alle Hallo manier toohello toosign beëindigen in Azure en uw abonnement te selecteren.</span><span class="sxs-lookup"><span data-stu-id="53ba4-115">If you have never used Azure PowerShell, see [How tooInstall and Configure Azure PowerShell](/powershell/azure/overview) and follow hello instructions all hello way toohello end toosign into Azure and select your subscription.</span></span>
2. <span data-ttu-id="53ba4-116">Voer Hallo **New-AzureRmResourceGroupDeployment** cmdlet toocreate een resource-groep met Hallo sjabloon.</span><span class="sxs-lookup"><span data-stu-id="53ba4-116">Run hello **New-AzureRmResourceGroupDeployment** cmdlet toocreate a resource group using hello template.</span></span>

    ```powershell
    New-AzureRmResourceGroupDeployment -Name TestRG -Location uswest `
        -TemplateFile 'https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-2-vms-loadbalancer-lbrules/azuredeploy.json' `
        -TemplateParameterFile 'https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-2-vms-loadbalancer-lbrules/azuredeploy.parameters.json'
    ```

## <a name="deploy-hello-template-by-using-hello-azure-cli"></a><span data-ttu-id="53ba4-117">Hallo-sjabloon implementeren met hello Azure CLI</span><span class="sxs-lookup"><span data-stu-id="53ba4-117">Deploy hello template by using hello Azure CLI</span></span>

<span data-ttu-id="53ba4-118">toodeploy hello sjabloon via Azure CLI Hallo Hallo volgende stappen.</span><span class="sxs-lookup"><span data-stu-id="53ba4-118">toodeploy hello template by using hello Azure CLI, follow hello steps below.</span></span>

1. <span data-ttu-id="53ba4-119">Als u Azure CLI nog nooit hebt gebruikt, raadpleegt u [installeren en configureren van Azure CLI Hallo](../cli-install-nodejs.md) en volg de instructies Hallo toohello punt waar u uw Azure-account en abonnement selecteren.</span><span class="sxs-lookup"><span data-stu-id="53ba4-119">If you have never used Azure CLI, see [Install and Configure hello Azure CLI](../cli-install-nodejs.md) and follow hello instructions up toohello point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="53ba4-120">Voer Hallo **azure config mode** opdracht tooswitch tooResource modus Manager, zoals hieronder wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="53ba4-120">Run hello **azure config mode** command tooswitch tooResource Manager mode, as shown below.</span></span>

    ```azurecli
    azure config mode arm
    ```

    <span data-ttu-id="53ba4-121">Dit is verwacht Hallo uitvoer voor Hallo bovenstaande opdracht:</span><span class="sxs-lookup"><span data-stu-id="53ba4-121">Here is hello expected output for hello command above:</span></span>

        info:    New mode is arm

3. <span data-ttu-id="53ba4-122">Vanuit de browser te navigeren[Snelstartsjabloon met de Hallo](https://github.com/Azure/azure-quickstart-templates/tree/master/201-2-vms-loadbalancer-lbrules), Hallo inhoud van Hallo json-bestand kopiëren en plakken in een nieuw bestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="53ba4-122">From your browser, navigate too[hello Quickstart Template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-2-vms-loadbalancer-lbrules), copy hello contents of hello json file and paste into a new file in your computer.</span></span> <span data-ttu-id="53ba4-123">In dit scenario voor u het Hallo-waarden onder tooa-bestand met de naam zou kopiëren **c:\lb\azuredeploy.parameters.json**.</span><span class="sxs-lookup"><span data-stu-id="53ba4-123">For this scenario, you would be copying hello values below tooa file named **c:\lb\azuredeploy.parameters.json**.</span></span>
4. <span data-ttu-id="53ba4-124">Voer Hallo **implementatie van de azure-groep maken** cmdlet toodeploy Hallo nieuwe load balancer met behulp van Hallo sjabloon en de parameterbestanden die u hebt gedownload en hierboven zijn gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="53ba4-124">Run hello **azure group deployment create** cmdlet toodeploy hello new load balancer by using hello template and parameter files you downloaded and modified above.</span></span> <span data-ttu-id="53ba4-125">Hallo-lijst die wordt weergegeven na Hallo uitvoer wordt uitgelegd Hallo parameters die worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="53ba4-125">hello list shown after hello output explains hello parameters used.</span></span>

    ```azurecli
    azure group create --name TestRG --location westus --template-file 'https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-2-vms-loadbalancer-lbrules/azuredeploy.json' --parameters-file 'c:\lb\azuredeploy.parameters.json'
    ```

## <a name="next-steps"></a><span data-ttu-id="53ba4-126">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="53ba4-126">Next steps</span></span>

[<span data-ttu-id="53ba4-127">Aan de slag met het configureren van een interne load balancer</span><span class="sxs-lookup"><span data-stu-id="53ba4-127">Get started configuring an internal load balancer</span></span>](load-balancer-get-started-ilb-arm-ps.md)

[<span data-ttu-id="53ba4-128">Een distributiemodus voor de load balancer configureren</span><span class="sxs-lookup"><span data-stu-id="53ba4-128">Configure a load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="53ba4-129">TCP-time-outinstellingen voor inactiviteit voor de load balancer configureren</span><span class="sxs-lookup"><span data-stu-id="53ba4-129">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)

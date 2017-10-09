---
title: aaaMigrate VMs tooResource Manager met Azure CLI | Microsoft Docs
description: Dit artikel begeleidt u bij Hallo platform ondersteund migratie van resources van klassieke tooAzure Resource Manager met Azure CLI
services: virtual-machines-linux
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: d6f5a877-05b6-4127-a545-3f5bede4e479
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 03/30/2017
ms.author: kasing
ms.openlocfilehash: 0b11f4bb1b4658b3e88bf7629147ed953b678556
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-iaas-resources-from-classic-tooazure-resource-manager-by-using-azure-cli"></a><span data-ttu-id="91902-103">Migreren van IaaS-resources van klassieke tooAzure Resource Manager met behulp van Azure CLI</span><span class="sxs-lookup"><span data-stu-id="91902-103">Migrate IaaS resources from classic tooAzure Resource Manager by using Azure CLI</span></span>
<span data-ttu-id="91902-104">Deze stappen ziet u hoe Azure-opdrachtregelinterface (CLI) toouse toomigrate infrastructuur opdrachten als een dienst (IaaS) resources vanuit Hallo classic deployment model toohello Azure Resource Manager-implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="91902-104">These steps show you how toouse Azure command-line interface (CLI) commands toomigrate infrastructure as a service (IaaS) resources from hello classic deployment model toohello Azure Resource Manager deployment model.</span></span> <span data-ttu-id="91902-105">Hallo artikel vereist Hallo [Azure CLI](../../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="91902-105">hello article requires hello [Azure CLI](../../cli-install-nodejs.md).</span></span>

> [!NOTE]
> <span data-ttu-id="91902-106">Alle Hallo bewerkingen hier beschreven zijn idempotent.</span><span class="sxs-lookup"><span data-stu-id="91902-106">All hello operations described here are idempotent.</span></span> <span data-ttu-id="91902-107">Als er een probleem dan een niet-ondersteunde functie of een configuratiefout, raden wij aan dat u opnieuw Hallo proberen voorbereiden, afgebroken of doorgevoerd, bewerking.</span><span class="sxs-lookup"><span data-stu-id="91902-107">If you have a problem other than an unsupported feature or a configuration error, we recommend that you retry hello prepare, abort, or commit operation.</span></span> <span data-ttu-id="91902-108">Hallo actie opnieuw wordt en probeer het Hallo-platform.</span><span class="sxs-lookup"><span data-stu-id="91902-108">hello platform will then try hello action again.</span></span>
> 
> 

<br>
<span data-ttu-id="91902-109">Hier volgt een stroomdiagram tooidentify Hallo volgorde waarin stappen toobe uitgevoerd tijdens een migratie moeten</span><span class="sxs-lookup"><span data-stu-id="91902-109">Here is a flowchart tooidentify hello order in which steps need toobe executed during a migration process</span></span>

![Schermafbeelding van de migratiestappen Hallo](../windows/media/migration-classic-resource-manager/migration-flow.png)

## <a name="step-1-prepare-for-migration"></a><span data-ttu-id="91902-111">Stap 1: Voorbereiden voor migratie</span><span class="sxs-lookup"><span data-stu-id="91902-111">Step 1: Prepare for migration</span></span>
<span data-ttu-id="91902-112">Hier volgen enkele aanbevolen procedures die wij adviseren kijkt u bij het evalueren van IaaS-Resourcemigratie van klassieke tooResource Manager:</span><span class="sxs-lookup"><span data-stu-id="91902-112">Here are a few best practices that we recommend as you evaluate migrating IaaS resources from classic tooResource Manager:</span></span>

* <span data-ttu-id="91902-113">Lees Hallo [lijst met niet-ondersteunde configuraties of functies](../windows/migration-classic-resource-manager-overview.md).</span><span class="sxs-lookup"><span data-stu-id="91902-113">Read through hello [list of unsupported configurations or features](../windows/migration-classic-resource-manager-overview.md).</span></span> <span data-ttu-id="91902-114">Als u virtuele machines die gebruikmaken van niet-ondersteunde configuraties of functies hebt, raden wij wachten op Hallo functie of configuratieserver ondersteuning toobe aangekondigd.</span><span class="sxs-lookup"><span data-stu-id="91902-114">If you have virtual machines that use unsupported configurations or features, we recommend that you wait for hello feature/configuration support toobe announced.</span></span> <span data-ttu-id="91902-115">U kunt ook kunt u deze functie verwijderen of verplaatsen buiten de migratie van die configuratie tooenable als deze bij uw behoeften past.</span><span class="sxs-lookup"><span data-stu-id="91902-115">Alternatively, you can remove that feature or move out of that configuration tooenable migration if it suits your needs.</span></span>
* <span data-ttu-id="91902-116">Als u scripts die uw infrastructuur en toepassingen vandaag implementeert geautomatiseerde, kunt u toocreate instellingen voor een vergelijkbaar met behulp van deze scripts voor de migratie.</span><span class="sxs-lookup"><span data-stu-id="91902-116">If you have automated scripts that deploy your infrastructure and applications today, try toocreate a similar test setup by using those scripts for migration.</span></span> <span data-ttu-id="91902-117">U kunt ook voorbeeld omgevingen instellen met behulp van hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="91902-117">Alternatively, you can set up sample environments by using hello Azure portal.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="91902-118">Toepassingsgateways worden momenteel niet ondersteund voor migratie van klassiek tooResource Manager.</span><span class="sxs-lookup"><span data-stu-id="91902-118">Application Gateways are not currently supported for migration from classic tooResource Manager.</span></span> <span data-ttu-id="91902-119">Hallo gateway toomigrate een klassiek virtueel netwerk met een toepassingsgateway verwijderen voordat u een netwerk voorbereiden bewerking toomove Hallo uitvoert.</span><span class="sxs-lookup"><span data-stu-id="91902-119">toomigrate a classic virtual network with an Application gateway, remove hello gateway before running a Prepare operation toomove hello network.</span></span> <span data-ttu-id="91902-120">Nadat u Hallo migratie hebt voltooid, sluit u Hallo gateway in Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="91902-120">After you complete hello migration, reconnect hello gateway in Azure Resource Manager.</span></span> 
>
><span data-ttu-id="91902-121">ExpressRoute-gateways die verbinding maken met tooExpressRoute circuits in een ander abonnement kunnen niet automatisch worden gemigreerd.</span><span class="sxs-lookup"><span data-stu-id="91902-121">ExpressRoute gateways connecting tooExpressRoute circuits in another subscription cannot be migrated automatically.</span></span> <span data-ttu-id="91902-122">In dergelijke gevallen Hallo ExpressRoute-gateway verwijderen, Migreer het virtuele netwerk Hallo en maak Hallo-gateway.</span><span class="sxs-lookup"><span data-stu-id="91902-122">In such cases, remove hello ExpressRoute gateway, migrate hello virtual network and recreate hello gateway.</span></span> <span data-ttu-id="91902-123">Zie [migreren ExpressRoute-circuits en bijbehorende virtuele netwerken vanuit Hallo klassieke toohello Resource Manager-implementatiemodel](../../expressroute/expressroute-migration-classic-resource-manager.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="91902-123">Please see [Migrate ExpressRoute circuits and associated virtual networks from hello classic toohello Resource Manager deployment model](../../expressroute/expressroute-migration-classic-resource-manager.md) for more information.</span></span>
> 
> 

## <a name="step-2-set-your-subscription-and-register-hello-provider"></a><span data-ttu-id="91902-124">Stap 2: Stel uw abonnement en Hallo provider registreren</span><span class="sxs-lookup"><span data-stu-id="91902-124">Step 2: Set your subscription and register hello provider</span></span>
<span data-ttu-id="91902-125">Voor migratiescenario's, moet u tooset van uw omgeving voor zowel klassieke en het Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="91902-125">For migration scenarios, you need tooset up your environment for both classic and Resource Manager.</span></span> <span data-ttu-id="91902-126">[Azure CLI installeren](../../cli-install-nodejs.md) en [Selecteer uw abonnement](../../xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="91902-126">[Install Azure CLI](../../cli-install-nodejs.md) and [select your subscription](../../xplat-cli-connect.md).</span></span>

<span data-ttu-id="91902-127">Aanmelden tooyour-account.</span><span class="sxs-lookup"><span data-stu-id="91902-127">Sign-in tooyour account.</span></span>

    azure login

<span data-ttu-id="91902-128">Selecteer hello Azure-abonnement met behulp van de volgende opdracht Hallo.</span><span class="sxs-lookup"><span data-stu-id="91902-128">Select hello Azure subscription by using hello following command.</span></span>

    azure account set "<azure-subscription-name>"

> [!NOTE]
> <span data-ttu-id="91902-129">Registratie is een eenmalige stap maar behoeften toobe eenmaal voordat u de migratie wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="91902-129">Registration is a one time step but it needs toobe done once before attempting migration.</span></span> <span data-ttu-id="91902-130">Zonder te registreren ziet u Hallo volgende foutbericht wordt weergegeven</span><span class="sxs-lookup"><span data-stu-id="91902-130">Without registering you'll see hello following error message</span></span> 
> 
> <span data-ttu-id="91902-131">*BadRequest: Abonnement is niet geregistreerd voor migratie.*</span><span class="sxs-lookup"><span data-stu-id="91902-131">*BadRequest : Subscription is not registered for migration.*</span></span> 
> 
> 

<span data-ttu-id="91902-132">Registreren bij de Hallo migratie resourceprovider met behulp van de volgende opdracht Hallo.</span><span class="sxs-lookup"><span data-stu-id="91902-132">Register with hello migration resource provider by using hello following command.</span></span> <span data-ttu-id="91902-133">Houd er rekening mee dat in sommige gevallen kan deze opdracht time-out. Hallo-registratie is gelukt.</span><span class="sxs-lookup"><span data-stu-id="91902-133">Note that in some cases, this command times out. However, hello registration will be successful.</span></span>

    azure provider register Microsoft.ClassicInfrastructureMigrate

<span data-ttu-id="91902-134">Wacht vijf minuten voor Hallo registratie toofinish.</span><span class="sxs-lookup"><span data-stu-id="91902-134">Please wait five minutes for hello registration toofinish.</span></span> <span data-ttu-id="91902-135">U kunt de status van de Hallo van Hallo goedkeuring controleren met behulp van de volgende opdracht Hallo.</span><span class="sxs-lookup"><span data-stu-id="91902-135">You can check hello status of hello approval by using hello following command.</span></span> <span data-ttu-id="91902-136">Zorg ervoor dat RegistrationState `Registered` voordat u doorgaat.</span><span class="sxs-lookup"><span data-stu-id="91902-136">Make sure that RegistrationState is `Registered` before you proceed.</span></span>

    azure provider show Microsoft.ClassicInfrastructureMigrate

<span data-ttu-id="91902-137">Schakel nu over CLI toohello `asm` modus.</span><span class="sxs-lookup"><span data-stu-id="91902-137">Now switch CLI toohello `asm` mode.</span></span>

    azure config mode asm

## <a name="step-3-make-sure-you-have-enough-azure-resource-manager-virtual-machine-cores-in-hello-azure-region-of-your-current-deployment-or-vnet"></a><span data-ttu-id="91902-138">Stap 3: Controleer of er voldoende virtuele Machine van Azure Resource Manager kernen in hello Azure-regio van uw huidige implementatie of VNET</span><span class="sxs-lookup"><span data-stu-id="91902-138">Step 3: Make sure you have enough Azure Resource Manager Virtual Machine cores in hello Azure region of your current deployment or VNET</span></span>
<span data-ttu-id="91902-139">Voor deze stap moet u tooswitch te`arm` modus.</span><span class="sxs-lookup"><span data-stu-id="91902-139">For this step you'll need tooswitch too`arm` mode.</span></span> <span data-ttu-id="91902-140">Dit doen met de volgende opdracht Hallo.</span><span class="sxs-lookup"><span data-stu-id="91902-140">Do this with hello following command.</span></span>

```
azure config mode arm
```

<span data-ttu-id="91902-141">U kunt Hallo na CLI opdracht toocheck Hallo huidige hoeveelheid kernen hebt u in Azure Resource Manager gebruiken.</span><span class="sxs-lookup"><span data-stu-id="91902-141">You can use hello following CLI command toocheck hello current amount of cores you have in Azure Resource Manager.</span></span> <span data-ttu-id="91902-142">toolearn meer informatie over quota core, Zie [limieten en hello Azure Resource Manager](../../azure-subscription-service-limits.md#limits-and-the-azure-resource-manager)</span><span class="sxs-lookup"><span data-stu-id="91902-142">toolearn more about core quotas, see [Limits and hello Azure Resource Manager](../../azure-subscription-service-limits.md#limits-and-the-azure-resource-manager)</span></span>

```
azure vm list-usage -l "<Your VNET or Deployment's Azure region"
```

<span data-ttu-id="91902-143">Als u klaar bent voor het verifiëren van deze stap kunt u schakelen terug te`asm` modus.</span><span class="sxs-lookup"><span data-stu-id="91902-143">Once you're done verifying this step, you can switch back too`asm` mode.</span></span>

    azure config mode asm


## <a name="step-4-option-1---migrate-virtual-machines-in-a-cloud-service"></a><span data-ttu-id="91902-144">Stap 4: Optie 1 - migreren van virtuele machines in een cloudservice</span><span class="sxs-lookup"><span data-stu-id="91902-144">Step 4: Option 1 - Migrate virtual machines in a cloud service</span></span>
<span data-ttu-id="91902-145">Haal de lijst Hallo van cloud-services met behulp van de volgende opdracht Hallo en kies Hallo cloudservice die u wilt toomigrate.</span><span class="sxs-lookup"><span data-stu-id="91902-145">Get hello list of cloud services by using hello following command, and then pick hello cloud service that you want toomigrate.</span></span> <span data-ttu-id="91902-146">Houd er rekening mee dat als Hallo virtuele machines in de cloudservice Hallo in een virtueel netwerk zijn of als ze web/worker rollen hebben, u een foutbericht weergegeven ontvangt.</span><span class="sxs-lookup"><span data-stu-id="91902-146">Note that if hello VMs in hello cloud service are in a virtual network or if they have web/worker roles, you will get an error message.</span></span>

    azure service list

<span data-ttu-id="91902-147">Hallo volgende tooget Hallo implementatie opdrachtnaam voor cloudservice Hallo uit Hallo uitgebreide uitvoer worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="91902-147">Run hello following command tooget hello deployment name for hello cloud service from hello verbose output.</span></span> <span data-ttu-id="91902-148">In de meeste gevallen is implementatienaam Hallo Hallo dezelfde is als Hallo cloud service-naam.</span><span class="sxs-lookup"><span data-stu-id="91902-148">In most cases, hello deployment name is hello same as hello cloud service name.</span></span>

    azure service show <serviceName> -vv

<span data-ttu-id="91902-149">Eerst valideren als u met behulp van de volgende opdrachten Hallo Hallo-cloudservice kunt migreren:</span><span class="sxs-lookup"><span data-stu-id="91902-149">First, validate if you can migrate hello cloud service using hello following commands:</span></span>

```shell
azure service deployment validate-migration <serviceName> <deploymentName> new "" "" ""
```

<span data-ttu-id="91902-150">Bereid Hallo virtuele machines in de cloudservice Hallo voor migratie.</span><span class="sxs-lookup"><span data-stu-id="91902-150">Prepare hello virtual machines in hello cloud service for migration.</span></span> <span data-ttu-id="91902-151">U hebt twee opties toochoose uit.</span><span class="sxs-lookup"><span data-stu-id="91902-151">You have two options toochoose from.</span></span>

<span data-ttu-id="91902-152">Als u toomigrate Hallo VMs tooa platform gemaakt virtueel netwerk wilt, gebruikt u Hallo opdracht te volgen.</span><span class="sxs-lookup"><span data-stu-id="91902-152">If you want toomigrate hello VMs tooa platform-created virtual network, use hello following command.</span></span>

    azure service deployment prepare-migration <serviceName> <deploymentName> new "" "" ""

<span data-ttu-id="91902-153">Als u toomigrate tooan bestaande virtuele netwerk in Hallo Resource Manager-implementatiemodel wilt, gebruikt u Hallo opdracht te volgen.</span><span class="sxs-lookup"><span data-stu-id="91902-153">If you want toomigrate tooan existing virtual network in hello Resource Manager deployment model, use hello following command.</span></span>

    azure service deployment prepare-migration <serviceName> <deploymentName> existing <destinationVNETResourceGroupName> <subnetName> <vnetName>

<span data-ttu-id="91902-154">Nadat het Hallo voorbereiden bewerking is voltooid, kunt u bekijkt hello uitgebreide uitvoer tooget Hallo migratiestatus Hallo VM's en ervoor te zorgen dat ze Hallo `Prepared` status.</span><span class="sxs-lookup"><span data-stu-id="91902-154">After hello prepare operation is successful, you can look through hello verbose output tooget hello migration state of hello VMs and ensure that they are in hello `Prepared` state.</span></span>

    azure vm show <vmName> -vv

<span data-ttu-id="91902-155">Controleer de configuratie van Hallo voor Hallo voorbereid resources met behulp van de CLI of hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="91902-155">Check hello configuration for hello prepared resources by using either CLI or hello Azure portal.</span></span> <span data-ttu-id="91902-156">Als u niet klaar voor de migratie bent en u toogo back toohello oude status wilt, gebruik Hallo opdracht te volgen.</span><span class="sxs-lookup"><span data-stu-id="91902-156">If you are not ready for migration and you want toogo back toohello old state, use hello following command.</span></span>

    azure service deployment abort-migration <serviceName> <deploymentName>

<span data-ttu-id="91902-157">Als Hallo voorbereide configuratie er goed uitziet, kunt u verder gaan en Hallo resources met behulp van de volgende opdracht Hallo doorvoeren.</span><span class="sxs-lookup"><span data-stu-id="91902-157">If hello prepared configuration looks good, you can move forward and commit hello resources by using hello following command.</span></span>

    azure service deployment commit-migration <serviceName> <deploymentName>



## <a name="step-4-option-2----migrate-virtual-machines-in-a-virtual-network"></a><span data-ttu-id="91902-158">Stap 4: Optie 2: migreren van virtuele machines in een virtueel netwerk</span><span class="sxs-lookup"><span data-stu-id="91902-158">Step 4: Option 2 -  Migrate virtual machines in a virtual network</span></span>
<span data-ttu-id="91902-159">Pick Hallo virtueel netwerk dat u wilt dat toomigrate.</span><span class="sxs-lookup"><span data-stu-id="91902-159">Pick hello virtual network that you want toomigrate.</span></span> <span data-ttu-id="91902-160">Houd er rekening mee dat als Hallo virtueel netwerk web/werkrollen of VM's met niet-ondersteunde configuraties bevat, u een validatiefoutbericht krijgt.</span><span class="sxs-lookup"><span data-stu-id="91902-160">Note that if hello virtual network contains web/worker roles or VMs with unsupported configurations, you will get a validation error message.</span></span>

<span data-ttu-id="91902-161">Alle Hallo virtuele netwerken in Hallo abonnement ophalen met behulp van de volgende opdracht Hallo.</span><span class="sxs-lookup"><span data-stu-id="91902-161">Get all hello virtual networks in hello subscription by using hello following command.</span></span>

    azure network vnet list

<span data-ttu-id="91902-162">Hallo-uitvoer ziet er ongeveer als volgt:</span><span class="sxs-lookup"><span data-stu-id="91902-162">hello output will look something like this:</span></span>

![Schermopname van het Hallo-opdrachtregel met de naam van de hele virtuele netwerk Hallo gemarkeerd.](../media/virtual-machines-linux-cli-migration-classic-resource-manager/vnet.png)

<span data-ttu-id="91902-164">Hallo in Hallo hierboven voorbeeld **virtualNetworkName** is de volledige naam Hallo **'Groep classicubuntu16 classicubuntu16'**.</span><span class="sxs-lookup"><span data-stu-id="91902-164">In hello above example, hello **virtualNetworkName** is hello entire name **"Group classicubuntu16 classicubuntu16"**.</span></span>

<span data-ttu-id="91902-165">Eerst valideren als u Hallo virtueel netwerk met behulp van de volgende opdracht Hallo kunt migreren:</span><span class="sxs-lookup"><span data-stu-id="91902-165">First, validate if you can migrate hello virtual network using hello following command:</span></span>

```shell
azure network vnet validate-migration <virtualNetworkName>
```

<span data-ttu-id="91902-166">Hallo virtueel netwerk van uw keuze voorbereiden voor migratie met behulp van de volgende opdracht Hallo.</span><span class="sxs-lookup"><span data-stu-id="91902-166">Prepare hello virtual network of your choice for migration by using hello following command.</span></span>

    azure network vnet prepare-migration <virtualNetworkName>

<span data-ttu-id="91902-167">Controleer de configuratie van Hallo voor Hallo voorbereid virtuele machines met behulp van de CLI of hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="91902-167">Check hello configuration for hello prepared virtual machines by using either CLI or hello Azure portal.</span></span> <span data-ttu-id="91902-168">Als u niet klaar voor de migratie bent en u toogo back toohello oude status wilt, gebruik Hallo opdracht te volgen.</span><span class="sxs-lookup"><span data-stu-id="91902-168">If you are not ready for migration and you want toogo back toohello old state, use hello following command.</span></span>

    azure network vnet abort-migration <virtualNetworkName>

<span data-ttu-id="91902-169">Als Hallo voorbereide configuratie er goed uitziet, kunt u verder gaan en Hallo resources met behulp van de volgende opdracht Hallo doorvoeren.</span><span class="sxs-lookup"><span data-stu-id="91902-169">If hello prepared configuration looks good, you can move forward and commit hello resources by using hello following command.</span></span>

    azure network vnet commit-migration <virtualNetworkName>

## <a name="step-5-migrate-a-storage-account"></a><span data-ttu-id="91902-170">Stap 5: Een opslagaccount migreren</span><span class="sxs-lookup"><span data-stu-id="91902-170">Step 5: Migrate a storage account</span></span>
<span data-ttu-id="91902-171">Zodra u klaar bent met het migreren van Hallo virtuele machines, wordt u aangeraden dat u migreert Hallo storage-account.</span><span class="sxs-lookup"><span data-stu-id="91902-171">Once you're done migrating hello virtual machines, we recommend you migrate hello storage account.</span></span>

<span data-ttu-id="91902-172">Hallo opslagaccount voorbereiden voor migratie met behulp van de volgende opdracht Hallo</span><span class="sxs-lookup"><span data-stu-id="91902-172">Prepare hello storage account for migration by using hello following command</span></span>

    azure storage account prepare-migration <storageAccountName>

<span data-ttu-id="91902-173">Controleer de configuratie van Hallo voor Hallo met CLI of Azure-portal Hallo voorbereid storage-account.</span><span class="sxs-lookup"><span data-stu-id="91902-173">Check hello configuration for hello prepared storage account by using either CLI or hello Azure portal.</span></span> <span data-ttu-id="91902-174">Als u niet klaar voor de migratie bent en u toogo back toohello oude status wilt, gebruik Hallo opdracht te volgen.</span><span class="sxs-lookup"><span data-stu-id="91902-174">If you are not ready for migration and you want toogo back toohello old state, use hello following command.</span></span>

    azure storage account abort-migration <storageAccountName>

<span data-ttu-id="91902-175">Als Hallo voorbereide configuratie er goed uitziet, kunt u verder gaan en Hallo resources met behulp van de volgende opdracht Hallo doorvoeren.</span><span class="sxs-lookup"><span data-stu-id="91902-175">If hello prepared configuration looks good, you can move forward and commit hello resources by using hello following command.</span></span>

    azure storage account commit-migration <storageAccountName>

## <a name="next-steps"></a><span data-ttu-id="91902-176">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="91902-176">Next steps</span></span>

* [<span data-ttu-id="91902-177">Overzicht van de migratie van IaaS-resources van klassieke tooAzure Resource Manager-platform ondersteund</span><span class="sxs-lookup"><span data-stu-id="91902-177">Overview of platform-supported migration of IaaS resources from classic tooAzure Resource Manager</span></span>](migration-classic-resource-manager-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="91902-178">Technische deep dive op platform ondersteund migratie van klassiek tooAzure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="91902-178">Technical deep dive on platform-supported migration from classic tooAzure Resource Manager</span></span>](migration-classic-resource-manager-deep-dive.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="91902-179">Migratie van IaaS-resources van klassieke tooAzure Resource Manager plannen</span><span class="sxs-lookup"><span data-stu-id="91902-179">Planning for migration of IaaS resources from classic tooAzure Resource Manager</span></span>](migration-classic-resource-manager-plan.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="91902-180">PowerShell toomigrate IaaS resources van klassieke tooAzure Resource Manager gebruiken</span><span class="sxs-lookup"><span data-stu-id="91902-180">Use PowerShell toomigrate IaaS resources from classic tooAzure Resource Manager</span></span>](../windows/migration-classic-resource-manager-ps.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="91902-181">Community-hulpprogramma's voor hulp bij de migratie van IaaS-resources van klassieke tooAzure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="91902-181">Community tools for assisting with migration of IaaS resources from classic tooAzure Resource Manager</span></span>](../windows/migration-classic-resource-manager-community-tools.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="91902-182">Bekijk de meest voorkomende migratiefouten</span><span class="sxs-lookup"><span data-stu-id="91902-182">Review most common migration errors</span></span>](migration-classic-resource-manager-errors.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="91902-183">Bekijk Hallo veelgestelde meest vragen over migreren IaaS resources van klassieke tooAzure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="91902-183">Review hello most frequently asked questions about migrating IaaS resources from classic tooAzure Resource Manager</span></span>](migration-classic-resource-manager-faq.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

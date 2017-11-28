---
title: een Site Recovery-kluis aaaUpgrade tooan Azure Recovery Services-kluis
description: Meer informatie over hoe een Azure Site Recovery-kluis tooupgrade tooa Recovery Services-kluis
documentationcenter: 
author: rajani-janaki-ram
manager: rochakm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/31/2017
ms.author: rajani-janaki-ram
ms.openlocfilehash: a18a923ee3bad91873e654c9b9b5bf8b83acc123
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-a-site-recovery-vault-tooan-azure-resource-manager-based-recovery-services-vault"></a><span data-ttu-id="a0dfe-103">Upgrade van een Site Recovery-kluis tooan Azure Resource Manager gebaseerde Recovery Services-kluis</span><span class="sxs-lookup"><span data-stu-id="a0dfe-103">Upgrade a Site Recovery vault tooan Azure Resource Manager-based Recovery Services vault</span></span>

<span data-ttu-id="a0dfe-104">Dit artikel wordt beschreven hoe tooupgrade Azure Site Recovery-Service voor herstel op basis van een Resource Manager-kluizen tooAzure zonder invloed op de lopende replicatie kluizen.</span><span class="sxs-lookup"><span data-stu-id="a0dfe-104">This article describes how tooupgrade Azure Site Recovery vaults tooAzure Resource Manager-based Recovery Service vaults without any impact on ongoing replication.</span></span> <span data-ttu-id="a0dfe-105">Zie voor meer informatie over Azure Resource Manager-functies en voordelen [overzicht van Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a0dfe-105">For more information about Azure Resource Manager features and benefits, see [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>

## <a name="introduction"></a><span data-ttu-id="a0dfe-106">Inleiding</span><span class="sxs-lookup"><span data-stu-id="a0dfe-106">Introduction</span></span>
<span data-ttu-id="a0dfe-107">Een Recovery Services-kluis is een Azure Resource Manager-bron voor het beheren van back-up en herstel na noodgevallen in Hallo cloud ingebouwd.</span><span class="sxs-lookup"><span data-stu-id="a0dfe-107">A Recovery Services vault is an Azure Resource Manager resource for managing backup and disaster recovery natively in hello cloud.</span></span> <span data-ttu-id="a0dfe-108">Is een uniform kluis die u kunt gebruiken in Hallo nieuwe Azure-portal en vervangt deze Hallo klassieke back-up en kluizen van Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="a0dfe-108">It is a unified vault that you can use in hello new Azure portal, and it replaces hello classic backup and Site Recovery vaults.</span></span>

<span data-ttu-id="a0dfe-109">Recovery Services-kluizen bieden een matrix van functies, waaronder:</span><span class="sxs-lookup"><span data-stu-id="a0dfe-109">Recovery Services vaults offer an array of features, including:</span></span>

* <span data-ttu-id="a0dfe-110">Ondersteuning van Azure Resource Manager: U kunt beveiligen en uw virtuele machines en fysieke machines failover in een Azure Resource Manager-stack.</span><span class="sxs-lookup"><span data-stu-id="a0dfe-110">Azure Resource Manager support: You can protect and fail over your virtual machines and physical machines into an Azure Resource Manager stack.</span></span>

* <span data-ttu-id="a0dfe-111">Schijf uitsluiten: als u tijdelijke bestanden of hoge verloop gegevens die u niet wilt toouse uw bandbreedte voor hebt, kunt u de volumes uitsluiten van replicatie.</span><span class="sxs-lookup"><span data-stu-id="a0dfe-111">Exclude disk: If you have temp files or high churn data that you don’t want toouse all your bandwidth for, you can exclude volumes from replication.</span></span> <span data-ttu-id="a0dfe-112">Deze mogelijkheid is ingeschakeld op dit moment in *VMware tooAzure* en *Hyper-V tooAzure* en ook tooother-scenario's wordt uitgebreid.</span><span class="sxs-lookup"><span data-stu-id="a0dfe-112">This capability has been enabled currently in *VMware tooAzure* and *Hyper-V tooAzure* and is extended tooother scenarios as well.</span></span>

* <span data-ttu-id="a0dfe-113">Ondersteuning voor premium en lokaal redundante opslag: U kunt nu servers beveiligen in premium-opslag accounts waarmee klanten tooprotect toepassingen met hogere i/o-bewerkingen per seconde (IOPS).</span><span class="sxs-lookup"><span data-stu-id="a0dfe-113">Support for premium and locally redundant storage: You can now protect servers in premium storage accounts that allow customers tooprotect applications with higher input/output operations per second (IOPS).</span></span> <span data-ttu-id="a0dfe-114">Deze mogelijkheid is momenteel ingeschakeld in *VMware tooAzure*.</span><span class="sxs-lookup"><span data-stu-id="a0dfe-114">This capability is currently enabled in *VMware tooAzure*.</span></span>

* <span data-ttu-id="a0dfe-115">Gestroomlijnde ervaring aan de slag: Hallo verbeterde aan de slag ervaring is ontworpen toomake herstel na noodgevallen setup eenvoudig.</span><span class="sxs-lookup"><span data-stu-id="a0dfe-115">Streamlined getting-started experience: hello enhanced getting-started experience has been designed toomake disaster-recovery setup easy.</span></span>

* <span data-ttu-id="a0dfe-116">Back-up en het beheer van de Site Recovery uit dezelfde kluis Hallo: U kunt nu servers voor herstel na noodgevallen beveiligen of back-up van Hallo dezelfde kluis, waardoor uw beheer overhead aanzienlijk kan verminderen.</span><span class="sxs-lookup"><span data-stu-id="a0dfe-116">Backup and Site Recovery management from hello same vault: You can now protect servers for disaster recovery or perform backup from hello same vault, which can reduce your management overhead significantly.</span></span>

<span data-ttu-id="a0dfe-117">Zie voor meer informatie over functies en gebruikerservaring Hallo bijgewerkt Hallo [opslag, back-up en herstel blog](https://azure.microsoft.com/blog/azure-site-recovery-now-available-in-a-new-experience-with-support-for-arm-and-csp/).</span><span class="sxs-lookup"><span data-stu-id="a0dfe-117">For more information about hello upgraded experience and features, see hello [Storage, Backup, and Recovery blog](https://azure.microsoft.com/blog/azure-site-recovery-now-available-in-a-new-experience-with-support-for-arm-and-csp/).</span></span>

## <a name="salient-features"></a><span data-ttu-id="a0dfe-118">Opvallende kenmerken</span><span class="sxs-lookup"><span data-stu-id="a0dfe-118">Salient features</span></span>

* <span data-ttu-id="a0dfe-119">Er zijn geen gevolgen voor de lopende replicatie: lopende replicaties doorgaan zonder een onderbreking tijdens en na de upgrade.</span><span class="sxs-lookup"><span data-stu-id="a0dfe-119">No impact on ongoing replication: Ongoing replications continue without any interruption during and post upgrade.</span></span>

* <span data-ttu-id="a0dfe-120">Kan zonder extra kosten: ophalen van een volledige set van bijgewerkte mogelijkheden zonder extra kosten.</span><span class="sxs-lookup"><span data-stu-id="a0dfe-120">No additional cost: Get an entire set of updated capabilities at no additional cost.</span></span>

* <span data-ttu-id="a0dfe-121">Er is geen gegevensverlies: omdat dit proces een upgrade en niet een migratie is, bestaande herstelpunten voor replicatie en -instellingen blijven behouden tijdens en na de upgrade Hallo.</span><span class="sxs-lookup"><span data-stu-id="a0dfe-121">No data loss: Because this process is an upgrade and not a migration, existing replication recovery points and settings remain intact during and after hello upgrade.</span></span>


## <a name="what-happens-during-hello-vault-upgrade"></a><span data-ttu-id="a0dfe-122">Wat gebeurt er tijdens de upgrade van Hallo kluis?</span><span class="sxs-lookup"><span data-stu-id="a0dfe-122">What happens during hello vault upgrade?</span></span>

<span data-ttu-id="a0dfe-123">Tijdens de upgrade hello, kunt u bewerkingen zoals het registreren van een nieuwe server of het inschakelen van replicatie voor een virtuele machine (VM) niet uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="a0dfe-123">During hello upgrade, you cannot perform operations such as registering a new server or enabling replication for a virtual machine (VM).</span></span> <span data-ttu-id="a0dfe-124">Bewerkingen met betrekking tot het lezen van gegevens uit of schrijven van gegevens toohello kluis, zoals de lopende replicatie van beveiligde items toohello kluis, niet wordt onderbroken.</span><span class="sxs-lookup"><span data-stu-id="a0dfe-124">Operations that involve reading data from or writing data toohello vault, such as ongoing replication of protected items toohello vault, continue uninterrupted.</span></span>

### <a name="changes-tooautomation-and-tooling-after-hello-upgrade"></a><span data-ttu-id="a0dfe-125">Tooautomation en tooling na Hallo upgrade wijzigen</span><span class="sxs-lookup"><span data-stu-id="a0dfe-125">Changes tooautomation and tooling after hello upgrade</span></span>
<span data-ttu-id="a0dfe-126">Als u een upgrade uitvoert van Hallo kluis type vanuit Hallo classic deployment model toohello Resource Manager-implementatiemodel, bestaande automatisering Hallo of tooling tooensure dat het toowork na de upgrade Hallo blijft bijwerken.</span><span class="sxs-lookup"><span data-stu-id="a0dfe-126">As you upgrade hello vault type from hello classic deployment model toohello Resource Manager deployment model, update hello existing automation or tooling tooensure that it continues toowork after hello upgrade.</span></span>

### <a name="prepare-your-environment-for-hello-upgrade"></a><span data-ttu-id="a0dfe-127">Uw omgeving voorbereiden voor upgrade Hallo</span><span class="sxs-lookup"><span data-stu-id="a0dfe-127">Prepare your environment for hello upgrade</span></span>

* [<span data-ttu-id="a0dfe-128">PowerShell installeren of upgraden tooversion 5 of hoger</span><span class="sxs-lookup"><span data-stu-id="a0dfe-128">Install PowerShell or upgrade it tooversion 5 or later</span></span>](https://www.microsoft.com/download/details.aspx?id=50395)
* [<span data-ttu-id="a0dfe-129">Hallo meest recente versie van MSI van Azure PowerShell installeren</span><span class="sxs-lookup"><span data-stu-id="a0dfe-129">Install hello latest version of Azure PowerShell MSI</span></span>](https://github.com/Azure/azure-powershell/releases)
* [<span data-ttu-id="a0dfe-130">Recovery Services-kluis upgradescript Hallo downloaden</span><span class="sxs-lookup"><span data-stu-id="a0dfe-130">Download hello Recovery Services vault upgrade script</span></span>](https://aka.ms/vaultupgradescript)

### <a name="prerequisites"></a><span data-ttu-id="a0dfe-131">Vereisten</span><span class="sxs-lookup"><span data-stu-id="a0dfe-131">Prerequisites</span></span>
<span data-ttu-id="a0dfe-132">tooupgrade van Site Recovery-Service voor herstel op basis van een Resource Manager-kluizen tooAzure kluizen, moet u Hallo volgens de vereisten voldoen:</span><span class="sxs-lookup"><span data-stu-id="a0dfe-132">tooupgrade from Site Recovery vaults tooAzure Resource Manager-based Recovery Service vaults, you must meet hello following requirements:</span></span>

* <span data-ttu-id="a0dfe-133">Minimale agent-versie: Hallo-versie van Azure Site Recovery Provider is geïnstalleerd op de server moet 5.1.1700.0 of hoger.</span><span class="sxs-lookup"><span data-stu-id="a0dfe-133">Minimum agent version: hello version of Azure Site Recovery Provider installed on your server must be 5.1.1700.0 or later.</span></span>

* <span data-ttu-id="a0dfe-134">Ondersteunde configuratie: U kunt uw kluis niet configureren met storage area network (SAN) of SQL Server AlwaysOn-beschikbaarheidsgroepen.</span><span class="sxs-lookup"><span data-stu-id="a0dfe-134">Supported configuration: You cannot configure your vault with storage area network (SAN) or SQL Server AlwaysOn Availability Groups.</span></span> <span data-ttu-id="a0dfe-135">Alle andere configuraties worden ondersteund.</span><span class="sxs-lookup"><span data-stu-id="a0dfe-135">All other configurations are supported.</span></span>

    >[!NOTE]
    ><span data-ttu-id="a0dfe-136">Na de upgrade hello, kunt u de toewijzing van opslag via de PowerShell beheren.</span><span class="sxs-lookup"><span data-stu-id="a0dfe-136">After hello upgrade, you can manage storage mapping only via PowerShell.</span></span>

* <span data-ttu-id="a0dfe-137">Ondersteunde implementatiescenario: uw kluis Hallo mag niet *VMware tooAzure* verouderde implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="a0dfe-137">Supported deployment scenario: Your vault shouldn’t be hello *VMware tooAzure* legacy deployment model.</span></span> <span data-ttu-id="a0dfe-138">Voordat u doorgaat, moet u eerst de verbeterde implementatiemodel toohello verplaatsen.</span><span class="sxs-lookup"><span data-stu-id="a0dfe-138">Before you proceed, first move toohello enhanced deployment model.</span></span>

* <span data-ttu-id="a0dfe-139">Geen actieve gebruiker gestart taken die betrekking hebben op management vlak operations: omdat tijdens de upgrade toegang toohello management vlak beperkt is, Voer uw acties voor de vlak management voordat u de upgrade Hallo activeren.</span><span class="sxs-lookup"><span data-stu-id="a0dfe-139">No active user-initiated jobs that involve management plane operations: Because access toohello management plane is restricted during upgrade, complete all your management plane actions before you trigger hello upgrade.</span></span> <span data-ttu-id="a0dfe-140">Dit proces omvat niet lopende replicatie.</span><span class="sxs-lookup"><span data-stu-id="a0dfe-140">This process doesn’t include ongoing replication.</span></span>

## <a name="frequently-asked-questions"></a><span data-ttu-id="a0dfe-141">Veelgestelde vragen</span><span class="sxs-lookup"><span data-stu-id="a0dfe-141">Frequently asked questions</span></span>

<span data-ttu-id="a0dfe-142">**Deze upgrade invloed heeft op Mijn lopende replicatie?**</span><span class="sxs-lookup"><span data-stu-id="a0dfe-142">**Does this upgrade affect my ongoing replication?**</span></span>

<span data-ttu-id="a0dfe-143">Nee.</span><span class="sxs-lookup"><span data-stu-id="a0dfe-143">No.</span></span> <span data-ttu-id="a0dfe-144">De lopende replicatie blijft onderbroken tijdens en na de upgrade Hallo.</span><span class="sxs-lookup"><span data-stu-id="a0dfe-144">Your ongoing replication continues uninterrupted during and after hello upgrade.</span></span>

<span data-ttu-id="a0dfe-145">**Wat gebeurt er toonetwork instellingen zoals site-naar-site VPN- en IP-instellingen?**</span><span class="sxs-lookup"><span data-stu-id="a0dfe-145">**What happens toonetwork settings such as site-to-site VPN and IP settings?**</span></span>

<span data-ttu-id="a0dfe-146">Hallo upgrade heeft geen invloed op Hallo netwerkinstellingen.</span><span class="sxs-lookup"><span data-stu-id="a0dfe-146">hello upgrade doesn't affect hello network settings.</span></span> <span data-ttu-id="a0dfe-147">Alle Azure-naar-on-premises verbindingen blijven behouden.</span><span class="sxs-lookup"><span data-stu-id="a0dfe-147">All Azure-to-on-premises connections remain intact.</span></span>

<span data-ttu-id="a0dfe-148">**Wat gebeurt er toomy kluizen als ik niet van plan tooupgrade in Hallo nabije toekomst bent?**</span><span class="sxs-lookup"><span data-stu-id="a0dfe-148">**What happens toomy vaults if I don’t plan tooupgrade in hello near future?**</span></span>

<span data-ttu-id="a0dfe-149">Ondersteuning voor de Site Recovery-kluis in Hallo oude Azure-portal zullen worden afgeschaft vanaf September 2017.</span><span class="sxs-lookup"><span data-stu-id="a0dfe-149">Support for Site Recovery vault in hello old Azure portal will be deprecated starting September 2017.</span></span> <span data-ttu-id="a0dfe-150">Het is raadzaam Hallo upgradefunctie toomove toohello nieuwe portal te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="a0dfe-150">We strongly recommend that you use hello upgrade feature toomove toohello new portal.</span></span>

<span data-ttu-id="a0dfe-151">**Wat betekent dit migratieplan voor mijn bestaande tooling?**</span><span class="sxs-lookup"><span data-stu-id="a0dfe-151">**What does this migration plan mean for my existing tooling?**</span></span>  

<span data-ttu-id="a0dfe-152">Bijwerken van uw tooling toohello Resource Manager-implementatiemodel is een van de belangrijkste Hallo-wijzigingen die u in uw upgrade plan moet rekening houden met.</span><span class="sxs-lookup"><span data-stu-id="a0dfe-152">Updating your tooling toohello Resource Manager deployment model is one of hello most important changes that you must account for in your upgrade plans.</span></span> <span data-ttu-id="a0dfe-153">Hallo Recovery Services-kluizen zijn gebaseerd op Hallo Resource Manager-implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="a0dfe-153">hello Recovery Services vaults are based on hello Resource Manager deployment model.</span></span> 

<span data-ttu-id="a0dfe-154">**Hoe lang Hallo management vlak uitvaltijd laatste zijn?**</span><span class="sxs-lookup"><span data-stu-id="a0dfe-154">**How long does hello management-plane downtime last?**</span></span>

<span data-ttu-id="a0dfe-155">Hallo upgrade duurt normaal gesproken ongeveer 15 minuten voor too30 en het kan duren voordat tooa maximaal één uur.</span><span class="sxs-lookup"><span data-stu-id="a0dfe-155">hello upgrade ordinarily takes about 15 too30 minutes, and it could take up tooa maximum of one hour.</span></span>

<span data-ttu-id="a0dfe-156">**Kan ik terugdraaien na de upgrade?**</span><span class="sxs-lookup"><span data-stu-id="a0dfe-156">**Can I roll back after upgrading?**</span></span>

<span data-ttu-id="a0dfe-157">Nee.</span><span class="sxs-lookup"><span data-stu-id="a0dfe-157">No.</span></span> <span data-ttu-id="a0dfe-158">Terugdraaien wordt niet ondersteund nadat Hallo resources hebt geüpgraded.</span><span class="sxs-lookup"><span data-stu-id="a0dfe-158">Rollback is not supported after hello resources have been successfully upgraded.</span></span>

<span data-ttu-id="a0dfe-159">**Kan ik mijn abonnement of valideren resources toosee of ze kunnen worden bijgewerkt?**</span><span class="sxs-lookup"><span data-stu-id="a0dfe-159">**Can I validate my subscription or resources toosee whether they can be upgraded?**</span></span>

<span data-ttu-id="a0dfe-160">Ja.</span><span class="sxs-lookup"><span data-stu-id="a0dfe-160">Yes.</span></span> <span data-ttu-id="a0dfe-161">Hallo eerste stap bij het Hallo-upgrade is in Hallo platform ondersteund upgrade-optie, toovalidate dat Hallo-resources geschikt voor een upgrade zijn.</span><span class="sxs-lookup"><span data-stu-id="a0dfe-161">In hello platform-supported upgrade option, hello first step in hello upgrade is toovalidate that hello resources are capable of an upgrade.</span></span> <span data-ttu-id="a0dfe-162">Als Hallo validatie mislukt, ontvangt u passende foutberichten of waarschuwingen.</span><span class="sxs-lookup"><span data-stu-id="a0dfe-162">If hello validation fails, you will receive appropriate error messages or warnings.</span></span>

<span data-ttu-id="a0dfe-163">**Hoe kan ik een probleem met de Hallo upgrade melden?**</span><span class="sxs-lookup"><span data-stu-id="a0dfe-163">**How do I report an issue with hello upgrade?**</span></span>

<span data-ttu-id="a0dfe-164">Als er fouten tijdens de upgrade hello optreden, houd er rekening mee Hallo bewerkings-ID die opgenomen in het Hallo-fout.</span><span class="sxs-lookup"><span data-stu-id="a0dfe-164">If you experience any failures during hello upgrade, note hello operation ID that's listed in hello error.</span></span> <span data-ttu-id="a0dfe-165">Microsoft Support proactief te laten werken op het oplossen van Hallo probleem.</span><span class="sxs-lookup"><span data-stu-id="a0dfe-165">Microsoft Support will proactively work on resolving hello issue.</span></span> <span data-ttu-id="a0dfe-166">U kunt ook contact opnemen met het ondersteuningsteam Hallo met uw abonnements-ID, de kluisnaam en de bewerking-ID.</span><span class="sxs-lookup"><span data-stu-id="a0dfe-166">You can also contact hello Support team with your subscription ID, vault name, and operation ID.</span></span> <span data-ttu-id="a0dfe-167">Ondersteuning werkt tooresolve Hallo probleem zo snel mogelijk.</span><span class="sxs-lookup"><span data-stu-id="a0dfe-167">Support will work tooresolve hello issue as quickly as possible.</span></span> <span data-ttu-id="a0dfe-168">Probeer de bewerking Hallo niet opnieuw tenzij u expliciet gebruiksaanwijzing toodo zo is door Microsoft.</span><span class="sxs-lookup"><span data-stu-id="a0dfe-168">Do not retry hello operation unless you are explicitly instructed toodo so by Microsoft.</span></span>

## <a name="run-hello-script"></a><span data-ttu-id="a0dfe-169">Hallo-script uitvoeren</span><span class="sxs-lookup"><span data-stu-id="a0dfe-169">Run hello script</span></span>

<span data-ttu-id="a0dfe-170">Voer in PowerShell Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="a0dfe-170">In PowerShell, run hello following command:</span></span>

    PS > .\RecoveryServicesVaultUpgrade-1.0.0.ps1 -SubscriptionID <subscriptionID>  -VaultName <vaultname> -Location <location> -ResourceType HyperVRecoveryManagerVault -TargetResourceGroupName <rgname>

* <span data-ttu-id="a0dfe-171">Abonnements-id: Hallo abonnements-ID die is gekoppeld aan het Hallo-kluis die u een upgrade uitvoert.</span><span class="sxs-lookup"><span data-stu-id="a0dfe-171">SubscriptionID: hello subscription ID that's associated with hello vault that you're upgrading.</span></span>

* <span data-ttu-id="a0dfe-172">VaultName: naam van Hallo van Hallo kluis die u een upgrade uitvoert.</span><span class="sxs-lookup"><span data-stu-id="a0dfe-172">VaultName: hello name of hello vault that you're upgrading.</span></span>

* <span data-ttu-id="a0dfe-173">Locatie: locatie van Hallo van Hallo kluis die u een upgrade uitvoert.</span><span class="sxs-lookup"><span data-stu-id="a0dfe-173">Location: hello location of hello vault that you're upgrading.</span></span>

* <span data-ttu-id="a0dfe-174">ResourceType: HyperVRecoveryManagerVault voor Site Recovery-kluizen.</span><span class="sxs-lookup"><span data-stu-id="a0dfe-174">ResourceType: HyperVRecoveryManagerVault for Site Recovery vaults.</span></span>

* <span data-ttu-id="a0dfe-175">TargetResourceGroupName: Hallo resourcegroep waarin u wilt dat Hallo bijgewerkt kluis toobe geplaatst.</span><span class="sxs-lookup"><span data-stu-id="a0dfe-175">TargetResourceGroupName: hello resource group into which you want hello upgraded vault toobe placed.</span></span> <span data-ttu-id="a0dfe-176">TargetResourceGroupName kan een bestaande resourcegroep in Azure Resource Manager of een nieuwe zijn.</span><span class="sxs-lookup"><span data-stu-id="a0dfe-176">TargetResourceGroupName can be an existing resource group in Azure Resource Manager or a new one.</span></span> <span data-ttu-id="a0dfe-177">Als Hallo TargetResourceGroupName dat wordt meegeleverd niet bestaat, wordt deze gemaakt als onderdeel van de upgrade Hallo in Hallo dezelfde locatie als Hallo-kluis.</span><span class="sxs-lookup"><span data-stu-id="a0dfe-177">If hello TargetResourceGroupName that's supplied does not exist, it is created as part of hello upgrade in hello same location as hello vault.</span></span> <span data-ttu-id="a0dfe-178">Zie voor meer informatie Hallo 'Resourcegroepen' sectie [overzicht van Azure Resource Manager](../azure-resource-manager/resource-group-overview.md#resource-groups).</span><span class="sxs-lookup"><span data-stu-id="a0dfe-178">For more information, see hello "Resource groups" section of [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md#resource-groups).</span></span>

    >[!NOTE]
    ><span data-ttu-id="a0dfe-179">Naamgeving van de resource-groep is onderwerp toocertain beperkingen.</span><span class="sxs-lookup"><span data-stu-id="a0dfe-179">Resource group naming is subject toocertain constraints.</span></span> <span data-ttu-id="a0dfe-180">tooprevent kluis upgrade mislukt, ervoor tooobserve Hallo naamgevingsconventie zorgvuldig worden.</span><span class="sxs-lookup"><span data-stu-id="a0dfe-180">tooprevent vault upgrade failure, be sure tooobserve hello naming convention carefully.</span></span>
    >
    ><span data-ttu-id="a0dfe-181">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="a0dfe-181">For example:</span></span>
    >
    ><span data-ttu-id="a0dfe-182">.\RecoveryServicesVaultUpgrade-1.0.0.ps1 - SubscriptionId 1234-54123-354354-56416-8645 - VaultName gen2dr-locatie 'Noord-Europa' - ResourceType hypervrecoverymanagervault - TargetResourceGroupName abc</span><span class="sxs-lookup"><span data-stu-id="a0dfe-182">.\RecoveryServicesVaultUpgrade-1.0.0.ps1 -SubscriptionId 1234-54123-354354-56416-8645 -VaultName gen2dr -Location "north europe" -ResourceType hypervrecoverymanagervault -TargetResourceGroupName abc</span></span>

<span data-ttu-id="a0dfe-183">U kunt ook Hallo na script uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="a0dfe-183">Alternatively, you can run hello following script.</span></span> <span data-ttu-id="a0dfe-184">Hallo-waarden opgeven voor Hallo vereiste parameters.</span><span class="sxs-lookup"><span data-stu-id="a0dfe-184">Enter hello values for hello required parameters.</span></span>

    PS > .\RecoveryServicesVaultUpgrade-1.0.0.ps1
    cmdlet RecoveryServicesVaultUpgrade-1.0.0.ps1 at command pipeline position 1

    Supply values for hello following parameters:
    SubscriptionId:
    VaultName:
    Location:
    ResourceType:
    TargetResourceGroupName:

1. <span data-ttu-id="a0dfe-185">Hallo PowerShell-script wordt tooenter u gevraagd uw referenties.</span><span class="sxs-lookup"><span data-stu-id="a0dfe-185">hello PowerShell script prompts you tooenter your credentials.</span></span> <span data-ttu-id="a0dfe-186">Voer deze twee keer eenmaal voor Hallo classic deployment model account en eenmaal voor hello Azure Resource Manager-account.</span><span class="sxs-lookup"><span data-stu-id="a0dfe-186">Enter them twice, once for hello classic deployment model account and once for hello Azure Resource Manager account.</span></span>

2. <span data-ttu-id="a0dfe-187">Nadat u uw referenties hebt ingevoerd, wordt in het Hallo-script een selectievakje toodetermine wordt uitgevoerd of uw Hallo infrastructuur setup voldoet aan vereisten voor het eerder opgemerkt.</span><span class="sxs-lookup"><span data-stu-id="a0dfe-187">After you've entered your credentials, hello script runs a check toodetermine whether your infrastructure setup meets hello previously mentioned requirements.</span></span>

3. <span data-ttu-id="a0dfe-188">Nadat het Hallo-vereisten zijn gecontroleerd en bevestigd, bent u na vragen aan gebruiker tooproceed Hallo kluis voortzet.</span><span class="sxs-lookup"><span data-stu-id="a0dfe-188">After hello prerequisites have been checked and confirmed, you are prompted tooproceed with hello vault upgrade.</span></span> <span data-ttu-id="a0dfe-189">Hallo-upgradeproces start een upgrade van uw kluis.</span><span class="sxs-lookup"><span data-stu-id="a0dfe-189">hello upgrade process starts upgrading your vault.</span></span> <span data-ttu-id="a0dfe-190">Hallo volledige upgrade kunt toocomplete van 15 too30 minuten duren.</span><span class="sxs-lookup"><span data-stu-id="a0dfe-190">hello entire upgrade can take 15 too30 minutes toocomplete.</span></span>

4. <span data-ttu-id="a0dfe-191">Nadat het Hallo-upgrade is voltooid, kunt u de bijgewerkte kluis in de nieuwe Azure portal Hallo Hallo openen.</span><span class="sxs-lookup"><span data-stu-id="a0dfe-191">After hello upgrade has been completed successfully, you can access hello upgraded vault in hello new Azure portal.</span></span>

## <a name="post-upgrade-vault-management"></a><span data-ttu-id="a0dfe-192">Na de upgrade kluis management</span><span class="sxs-lookup"><span data-stu-id="a0dfe-192">Post-upgrade vault management</span></span>

### <a name="replicate-by-using-azure-site-recovery-in-hello-recovery-services-vault"></a><span data-ttu-id="a0dfe-193">Repliceren met behulp van Azure Site Recovery in Hallo die Recovery Services-kluis</span><span class="sxs-lookup"><span data-stu-id="a0dfe-193">Replicate by using Azure Site Recovery in hello Recovery Services vault</span></span>

* <span data-ttu-id="a0dfe-194">U kunt nu uw Azure VM's beveiligen tegen tooanother één regio.</span><span class="sxs-lookup"><span data-stu-id="a0dfe-194">You can now protect your Azure VMs from one region tooanother.</span></span> <span data-ttu-id="a0dfe-195">Zie voor meer informatie [Azure-machines repliceren tussen regio's met Azure Site Recovery](site-recovery-azure-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="a0dfe-195">For more information, see [Replicate Azure VMs between regions with Azure Site Recovery](site-recovery-azure-to-azure.md).</span></span>

* <span data-ttu-id="a0dfe-196">Zie voor meer informatie over het repliceren van virtuele VMware-machines tooAzure [tooAzure VMware-machines repliceren met Site Recovery](vmware-walkthrough-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a0dfe-196">For more information about replicating VMware VMs tooAzure, see [Replicate VMware VMs tooAzure with Site Recovery](vmware-walkthrough-overview.md).</span></span>

* <span data-ttu-id="a0dfe-197">Zie voor meer informatie over het repliceren van Hyper-V-machines (zonder VMM) tooAzure [repliceren Hyper-V virtuele machines (zonder VMM) tooAzure](hyper-v-site-walkthrough-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a0dfe-197">For more information about replicating Hyper-V VMs (without VMM) tooAzure, see [Replicate Hyper-V virtual machines (without VMM) tooAzure](hyper-v-site-walkthrough-overview.md).</span></span>

* <span data-ttu-id="a0dfe-198">Zie voor meer informatie over het repliceren van Hyper-V-machines (met VMM) tooAzure [repliceren Hyper-V virtuele machines in VMM-clouds tooAzure met Site Recovery in de Azure-portal Hallo](vmm-to-azure-walkthrough-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a0dfe-198">For more information about replicating Hyper-V VMs (with VMM) tooAzure, see [Replicate Hyper-V virtual machines in VMM clouds tooAzure using Site Recovery in hello Azure portal](vmm-to-azure-walkthrough-overview.md).</span></span>

* <span data-ttu-id="a0dfe-199">Zie voor meer informatie over Hyper-VM's (met VMM) tooa secundaire site repliceren [repliceren Hyper-V virtuele machines in VMM clouds tooa secundaire VMM site met behulp van Azure-portal Hallo](site-recovery-vmm-to-vmm.md).</span><span class="sxs-lookup"><span data-stu-id="a0dfe-199">For more information about replicating Hyper-VMs (with VMM) tooa secondary site, see [Replicate Hyper-V virtual machines in VMM clouds tooa secondary VMM site using hello Azure portal](site-recovery-vmm-to-vmm.md).</span></span>

* <span data-ttu-id="a0dfe-200">Zie voor meer informatie over het repliceren van virtuele VMware-machines tooa secundaire site [repliceren lokale virtuele VMware-machines of fysieke servers tooa secundaire site in de klassieke Azure portal Hallo](site-recovery-vmware-to-vmware.md).</span><span class="sxs-lookup"><span data-stu-id="a0dfe-200">For more information about replicating VMware VMs tooa secondary site, see [Replicate on-premises VMware virtual machines or physical servers tooa secondary site in hello classic Azure portal](site-recovery-vmware-to-vmware.md).</span></span>

### <a name="view-your-replicated-items"></a><span data-ttu-id="a0dfe-201">De gerepliceerde items weergeven</span><span class="sxs-lookup"><span data-stu-id="a0dfe-201">View your replicated items</span></span>

<span data-ttu-id="a0dfe-202">Hallo toont volgende afbeelding Hallo Recovery Services-kluis dashboardpagina die belangrijke entiteiten voor Hallo kluis wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="a0dfe-202">hello following image shows hello Recovery Services vault dashboard page that displays key entities for hello vault.</span></span> <span data-ttu-id="a0dfe-203">selecteert u een lijst met beveiligde entiteiten in de kluis hello, tooview **siteherstel** > **gerepliceerde items**.</span><span class="sxs-lookup"><span data-stu-id="a0dfe-203">tooview a list of protected entities in hello vault, select **Site Recovery** > **Replicated items**.</span></span>


![Gerepliceerde items](./media/upgrade-site-recovery-vaults/replicateditems.png)

<span data-ttu-id="a0dfe-205">Hallo volgende afbeelding toont Hallo-werkstroom voor het weergeven van uw gerepliceerde items en Hallo **Failover** opdracht voor het initiëren van een failover.</span><span class="sxs-lookup"><span data-stu-id="a0dfe-205">hello following image shows hello workflow for viewing your replicated items and hello **Failover** command for initiating a failover.</span></span>

![Gerepliceerde items](./media/upgrade-site-recovery-vaults/failover.png)

### <a name="view-your-replication-settings"></a><span data-ttu-id="a0dfe-207">Replicatie-instellingen weergeven</span><span class="sxs-lookup"><span data-stu-id="a0dfe-207">View your replication settings</span></span>

<span data-ttu-id="a0dfe-208">In de Site Recovery-kluis hello, is elke beveiligingsgroep worden geconfigureerd met kopieerfrequentie, herstelpunt bewaartermijn, frequentie van toepassingsconsistente momentopnamen en andere replicatie-instellingen.</span><span class="sxs-lookup"><span data-stu-id="a0dfe-208">In hello Site Recovery vault, each protection group is configured with copy frequency, recovery point retention, frequency of application consistent snapshots, and other replication settings.</span></span> <span data-ttu-id="a0dfe-209">In de Recovery Services-kluis hello, worden deze instellingen geconfigureerd als een beleids-replicatie.</span><span class="sxs-lookup"><span data-stu-id="a0dfe-209">In hello Recovery Services vault, these settings are configured as a replication policy.</span></span> <span data-ttu-id="a0dfe-210">Hallo Hallo beleid is Hallo-naam van het Hallo-beveiligingsgroep of Hallo *primarycloud_Policy*.</span><span class="sxs-lookup"><span data-stu-id="a0dfe-210">hello name of hello policy is hello name of hello protection group or hello *primarycloud_Policy*.</span></span>

<span data-ttu-id="a0dfe-211">Zie voor meer informatie over beleid voor wachtwoordreplicatie [beheren replicatiebeleid voor VMware tooAzure](site-recovery-setup-replication-settings-vmware.md).</span><span class="sxs-lookup"><span data-stu-id="a0dfe-211">For more information about replication policy, see [Manage replication policy for VMware tooAzure](site-recovery-setup-replication-settings-vmware.md).</span></span>

---
title: Upgrade van een Azure Service Fabric-cluster | Microsoft Docs
description: Upgrade van de Service Fabric-code en/of de configuratie die wordt uitgevoerd van een Service Fabric-cluster, inclusief het instellen van de cluster-updatemodus, certificaten, toe te voegen toepassing poorten, OS patches doen upgraden enzovoort. Wat kunt u verwachten wanneer de upgrades worden uitgevoerd?
services: service-fabric
documentationcenter: .net
author: ChackDan
manager: timlt
editor: 
ms.assetid: 15190ace-31ed-491f-a54b-b5ff61e718db
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 8/10/2017
ms.author: chackdan
ms.openlocfilehash: 7ea71ab891583c51b3c07a4d0a9f0b4f54e56669
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="upgrade-an-azure-service-fabric-cluster"></a><span data-ttu-id="f6d46-104">Upgrade van een Azure Service Fabric-cluster</span><span class="sxs-lookup"><span data-stu-id="f6d46-104">Upgrade an Azure Service Fabric cluster</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f6d46-105">Azure-Cluster</span><span class="sxs-lookup"><span data-stu-id="f6d46-105">Azure Cluster</span></span>](service-fabric-cluster-upgrade.md)
> * [<span data-ttu-id="f6d46-106">Zelfstandige Cluster</span><span class="sxs-lookup"><span data-stu-id="f6d46-106">Standalone Cluster</span></span>](service-fabric-cluster-upgrade-windows-server.md)
> 
> 

<span data-ttu-id="f6d46-107">Ontwerpen voor kunnen is essentieel bij het bereiken van succes op lange termijn van uw product voor elk moderne systeem.</span><span class="sxs-lookup"><span data-stu-id="f6d46-107">For any modern system, designing for upgradability is key to achieving long-term success of your product.</span></span> <span data-ttu-id="f6d46-108">Een Azure Service Fabric-cluster is een resource die u bezit, maar gedeeltelijk wordt beheerd door Microsoft.</span><span class="sxs-lookup"><span data-stu-id="f6d46-108">An Azure Service Fabric cluster is a resource that you own, but is partly managed by Microsoft.</span></span> <span data-ttu-id="f6d46-109">Dit artikel wordt beschreven wat automatisch wordt beheerd en wat u kunt zelf configureren.</span><span class="sxs-lookup"><span data-stu-id="f6d46-109">This article describes what is managed automatically and what you can configure yourself.</span></span>

## <a name="controlling-the-fabric-version-that-runs-on-your-cluster"></a><span data-ttu-id="f6d46-110">De fabric-versie die wordt uitgevoerd op uw Cluster beheren</span><span class="sxs-lookup"><span data-stu-id="f6d46-110">Controlling the fabric version that runs on your Cluster</span></span>
<span data-ttu-id="f6d46-111">U kunt instellen dat uw cluster automatische fabric-upgrades ontvangen als ze door Microsoft worden uitgegeven of kunt u een ondersteunde fabric-versie die u wilt dat uw cluster op.</span><span class="sxs-lookup"><span data-stu-id="f6d46-111">You can set your cluster to receive automatic fabric upgrades as they are released by Microsoft or you can select a supported fabric version you want your cluster to be on.</span></span>

<span data-ttu-id="f6d46-112">Dit doet u door het instellen van de clusterconfiguratie 'upgradeMode' op de portal of met behulp van Resource Manager op het moment van worden gemaakt of later op een live cluster</span><span class="sxs-lookup"><span data-stu-id="f6d46-112">You do this by setting the "upgradeMode" cluster configuration on the portal or using Resource Manager at the time of creation or later on a live cluster</span></span> 

> [!NOTE]
> <span data-ttu-id="f6d46-113">Zorg ervoor dat het cluster een ondersteunde fabric-versie altijd uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="f6d46-113">Make sure to keep your cluster running a supported fabric version always.</span></span> <span data-ttu-id="f6d46-114">Als en dat we de release van een nieuwe versie van het service fabric aankondigen, wordt de vorige versie gemarkeerd voor einde van ondersteuning na een minimum van 60 dagen na die datum.</span><span class="sxs-lookup"><span data-stu-id="f6d46-114">As and when we announce the release of a new version of service fabric, the previous version is marked for end of support after a minimum of 60 days from that date.</span></span> <span data-ttu-id="f6d46-115">de nieuwe releases worden aangekondigd [op het service fabric-teamblog](https://blogs.msdn.microsoft.com/azureservicefabric/).</span><span class="sxs-lookup"><span data-stu-id="f6d46-115">the  The new releases are announced [on the service fabric team blog](https://blogs.msdn.microsoft.com/azureservicefabric/).</span></span> <span data-ttu-id="f6d46-116">De nieuwe versie is beschikbaar om te kiezen klikt.</span><span class="sxs-lookup"><span data-stu-id="f6d46-116">The new release is available to choose then.</span></span> 
> 
> 

<span data-ttu-id="f6d46-117">14 dagen vóór het verstrijken van de release van die het cluster wordt uitgevoerd, een statusgebeurtenis gegenereerd die het cluster in een waarschuwingsstatus wordt geplaatst.</span><span class="sxs-lookup"><span data-stu-id="f6d46-117">14 days prior to the expiry of the release your cluster is running, a health event is generated that puts your cluster into a warning health state.</span></span> <span data-ttu-id="f6d46-118">Het cluster blijft in een waarschuwingsstatus totdat u een naar een ondersteunde fabric-versie upgrade.</span><span class="sxs-lookup"><span data-stu-id="f6d46-118">The cluster remains in a warning state until you upgrade to a supported fabric version.</span></span>

### <a name="setting-the-upgrade-mode-via-portal"></a><span data-ttu-id="f6d46-119">De upgrademodus via de portal instellen</span><span class="sxs-lookup"><span data-stu-id="f6d46-119">Setting the upgrade mode via portal</span></span>
<span data-ttu-id="f6d46-120">Wanneer u het cluster maakt, kunt u het cluster instellen op automatisch of handmatig.</span><span class="sxs-lookup"><span data-stu-id="f6d46-120">You can set the cluster to automatic or manual when you are creating the cluster.</span></span>

![Create_Manualmode][Create_Manualmode]

<span data-ttu-id="f6d46-122">U kunt het cluster instellen op automatisch of handmatig moet worden gebruikt vanaf een live cluster met behulp van de ervaring beheren.</span><span class="sxs-lookup"><span data-stu-id="f6d46-122">You can set the cluster to automatic or manual when on a live cluster, using the manage experience.</span></span> 

#### <a name="upgrading-to-a-new-version-on-a-cluster-that-is-set-to-manual-mode-via-portal"></a><span data-ttu-id="f6d46-123">Upgraden naar een nieuwe versie op een cluster dat is ingesteld op de handmatige modus via de portal.</span><span class="sxs-lookup"><span data-stu-id="f6d46-123">Upgrading to a new version on a cluster that is set to Manual mode via portal.</span></span>
<span data-ttu-id="f6d46-124">Als u wilt upgraden naar een nieuwe versie, is hoeft u de beschikbare versie uit de vervolgkeuzelijst selecteert en slaat u.</span><span class="sxs-lookup"><span data-stu-id="f6d46-124">To upgrade to a new version, all you need to do is select the available version from the dropdown and save.</span></span> <span data-ttu-id="f6d46-125">De Fabric-upgrade wordt automatisch gestart.</span><span class="sxs-lookup"><span data-stu-id="f6d46-125">The Fabric upgrade gets kicked off automatically.</span></span> <span data-ttu-id="f6d46-126">De cluster-statusbeleid (een combinatie van het knooppunt status en de status alle toepassingen die worden uitgevoerd in het cluster) om te worden gehouden tijdens de upgrade.</span><span class="sxs-lookup"><span data-stu-id="f6d46-126">The cluster health policies (a combination of node health and the health all the applications running in the cluster) are adhered to during the upgrade.</span></span>

<span data-ttu-id="f6d46-127">Als het statusbeleid cluster niet wordt voldaan, is de upgrade teruggedraaid.</span><span class="sxs-lookup"><span data-stu-id="f6d46-127">If the cluster health policies are not met, the upgrade is rolled back.</span></span> <span data-ttu-id="f6d46-128">Schuif omlaag in dit document voor meer informatie over het instellen van deze aangepaste statusbeleid.</span><span class="sxs-lookup"><span data-stu-id="f6d46-128">Scroll down this document to read more on how to set those custom health policies.</span></span> 

<span data-ttu-id="f6d46-129">Als u de problemen dat heeft geresulteerd in de terugdraaiactie hebt opgelost, moet u de upgrade opnieuw door de dezelfde stappen als voordat initiëren.</span><span class="sxs-lookup"><span data-stu-id="f6d46-129">Once you have fixed the issues that resulted in the rollback, you need to initiate the upgrade again, by following the same steps as before.</span></span>

![Manage_Automaticmode][Manage_Automaticmode]

### <a name="setting-the-upgrade-mode-via-a-resource-manager-template"></a><span data-ttu-id="f6d46-131">De upgrademodus via Resource Manager-sjabloon instellen</span><span class="sxs-lookup"><span data-stu-id="f6d46-131">Setting the upgrade mode via a Resource Manager template</span></span>
<span data-ttu-id="f6d46-132">De configuratie 'upgradeMode' toevoegen aan de resourcedefinitie Microsoft.ServiceFabric/clusters en de 'clusterCodeVersion' ingesteld op een van de ondersteunde fabric-versies zoals hieronder wordt weergegeven en vervolgens de sjabloon te implementeren.</span><span class="sxs-lookup"><span data-stu-id="f6d46-132">Add the "upgradeMode" configuration to the Microsoft.ServiceFabric/clusters resource definition and set the "clusterCodeVersion" to one of the supported fabric versions as shown below and then deploy the template.</span></span> <span data-ttu-id="f6d46-133">De geldige waarden voor 'upgradeMode' zijn 'Handmatig' of 'Automatisch'</span><span class="sxs-lookup"><span data-stu-id="f6d46-133">The valid values for "upgradeMode" are "Manual" or "Automatic"</span></span>

![ARMUpgradeMode][ARMUpgradeMode]

#### <a name="upgrading-to-a-new-version-on-a-cluster-that-is-set-to-manual-mode-via-a-resource-manager-template"></a><span data-ttu-id="f6d46-135">Upgraden naar een nieuwe versie op een cluster dat is ingesteld op de handmatige modus via Resource Manager-sjabloon.</span><span class="sxs-lookup"><span data-stu-id="f6d46-135">Upgrading to a new version on a cluster that is set to Manual mode via a Resource Manager template.</span></span>
<span data-ttu-id="f6d46-136">Wanneer het cluster in de handmatige modus is, om te upgraden naar een nieuwe versie, de 'clusterCodeVersion' wijzigen naar een ondersteunde versie en deze implementeren.</span><span class="sxs-lookup"><span data-stu-id="f6d46-136">When the cluster is in Manual mode, to upgrade to a new version, change the "clusterCodeVersion" to a supported version and deploy it.</span></span> <span data-ttu-id="f6d46-137">De implementatie van de sjabloon, gang van de Fabric-upgrade opgehaald gestarte automatisch.</span><span class="sxs-lookup"><span data-stu-id="f6d46-137">The deployment of the template, kicks of the Fabric upgrade gets kicked off automatically.</span></span> <span data-ttu-id="f6d46-138">De cluster-statusbeleid (een combinatie van het knooppunt status en de status alle toepassingen die worden uitgevoerd in het cluster) om te worden gehouden tijdens de upgrade.</span><span class="sxs-lookup"><span data-stu-id="f6d46-138">The cluster health policies (a combination of node health and the health all the applications running in the cluster) are adhered to during the upgrade.</span></span>

<span data-ttu-id="f6d46-139">Als het statusbeleid cluster niet wordt voldaan, is de upgrade teruggedraaid.</span><span class="sxs-lookup"><span data-stu-id="f6d46-139">If the cluster health policies are not met, the upgrade is rolled back.</span></span> <span data-ttu-id="f6d46-140">Schuif omlaag in dit document voor meer informatie over het instellen van deze aangepaste statusbeleid.</span><span class="sxs-lookup"><span data-stu-id="f6d46-140">Scroll down this document to read more on how to set those custom health policies.</span></span> 

<span data-ttu-id="f6d46-141">Als u de problemen dat heeft geresulteerd in de terugdraaiactie hebt opgelost, moet u de upgrade opnieuw door de dezelfde stappen als voordat initiëren.</span><span class="sxs-lookup"><span data-stu-id="f6d46-141">Once you have fixed the issues that resulted in the rollback, you need to initiate the upgrade again, by following the same steps as before.</span></span>

### <a name="get-list-of-all-available-version-for-all-environments-for-a-given-subscription"></a><span data-ttu-id="f6d46-142">Lijst met alle beschikbare versie ophalen voor alle omgevingen voor een bepaald abonnement</span><span class="sxs-lookup"><span data-stu-id="f6d46-142">Get list of all available version for all environments for a given subscription</span></span>
<span data-ttu-id="f6d46-143">Voer de volgende opdracht en krijgt u uitvoer ongeveer als volgt.</span><span class="sxs-lookup"><span data-stu-id="f6d46-143">Run the following command, and you should get an output similar to this.</span></span>

<span data-ttu-id="f6d46-144">'supportExpiryUtc' vertelt uw wanneer een bepaalde versie is verlopen of is verlopen.</span><span class="sxs-lookup"><span data-stu-id="f6d46-144">"supportExpiryUtc" tells your when a given release is expiring or has expired.</span></span> <span data-ttu-id="f6d46-145">De meest recente versie is geen geldige datum - deze heeft de waarde ' 9999-12-31T23:59:59.9999999 ', wat betekent dat de vervaldatum is nog niet ingesteld.</span><span class="sxs-lookup"><span data-stu-id="f6d46-145">The latest release does not have a valid date - it has a value of "9999-12-31T23:59:59.9999999", which just means that the expiry date is not yet set.</span></span>

```REST
GET https://<endpoint>/subscriptions/{{subscriptionId}}/providers/Microsoft.ServiceFabric/locations/{{location}}/clusterVersions?api-version=2016-09-01

Example: https://management.azure.com/subscriptions/1857f442-3bce-4b96-ad95-627f76437a67/providers/Microsoft.ServiceFabric/locations/eastus/clusterVersions?api-version=2016-09-01

Output:
{
                  "value": [
                    {
                      "id": "subscriptions/35349203-a0b3-405e-8a23-9f1450984307/providers/Microsoft.ServiceFabric/environments/Windows/clusterVersions/5.0.1427.9490",
                      "name": "5.0.1427.9490",
                      "type": "Microsoft.ServiceFabric/environments/clusterVersions",
                      "properties": {
                        "codeVersion": "5.0.1427.9490",
                        "supportExpiryUtc": "2016-11-26T23:59:59.9999999",
                        "environment": "Windows"
                      }
                    },
                    {
                      "id": "subscriptions/35349203-a0b3-405e-8a23-9f1450984307/providers/Microsoft.ServiceFabric/environments/Windows/clusterVersions/4.0.1427.9490",
                      "name": "5.1.1427.9490",
                      "type": " Microsoft.ServiceFabric/environments/clusterVersions",
                      "properties": {
                        "codeVersion": "5.1.1427.9490",
                        "supportExpiryUtc": "9999-12-31T23:59:59.9999999",
                        "environment": "Windows"
                      }
                    },
                    {
                      "id": "subscriptions/35349203-a0b3-405e-8a23-9f1450984307/providers/Microsoft.ServiceFabric/environments/Windows/clusterVersions/4.4.1427.9490",
                      "name": "4.4.1427.9490",
                      "type": " Microsoft.ServiceFabric/environments/clusterVersions",
                      "properties": {
                        "codeVersion": "4.4.1427.9490",
                        "supportExpiryUtc": "9999-12-31T23:59:59.9999999",
                        "environment": "Linux"
                      }
                    }
                  ]
                }


```

## <a name="fabric-upgrade-behavior-when-the-cluster-upgrade-mode-is-automatic"></a><span data-ttu-id="f6d46-146">Fabric upgrade gedrag wanneer het cluster de modus bijwerken automatisch is</span><span class="sxs-lookup"><span data-stu-id="f6d46-146">Fabric upgrade behavior when the cluster Upgrade Mode is Automatic</span></span>
<span data-ttu-id="f6d46-147">Microsoft onderhoudt op de fabric-code en de configuratie die in een Azure-cluster wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="f6d46-147">Microsoft maintains the fabric code and configuration that runs in an Azure cluster.</span></span> <span data-ttu-id="f6d46-148">We uitvoeren automatische gecontroleerde upgrades naar de software op een als dat nodig is.</span><span class="sxs-lookup"><span data-stu-id="f6d46-148">We perform automatic monitored upgrades to the software on an as-needed basis.</span></span> <span data-ttu-id="f6d46-149">Deze upgrades mogelijk code en/of de configuratie.</span><span class="sxs-lookup"><span data-stu-id="f6d46-149">These upgrades could be code, configuration, or both.</span></span> <span data-ttu-id="f6d46-150">Om ervoor te zorgen dat uw toepassing te lijden heeft onder geen gevolgen of minimale gevolgen als gevolg van deze upgrades, voeren we de upgrades in de volgende fasen:</span><span class="sxs-lookup"><span data-stu-id="f6d46-150">To make sure that your application suffers no impact or minimal impact due to these upgrades, we perform the upgrades in the following phases:</span></span>

### <a name="phase-1-an-upgrade-is-performed-by-using-all-cluster-health-policies"></a><span data-ttu-id="f6d46-151">Fase 1: Een upgrade wordt uitgevoerd met behulp van alle cluster statusbeleid</span><span class="sxs-lookup"><span data-stu-id="f6d46-151">Phase 1: An upgrade is performed by using all cluster health policies</span></span>
<span data-ttu-id="f6d46-152">Tijdens deze fase wordt de upgrades één upgradedomein tegelijk gaan en de toepassingen die worden uitgevoerd in het cluster worden uitgevoerd zonder uitvaltijd.</span><span class="sxs-lookup"><span data-stu-id="f6d46-152">During this phase, the upgrades proceed one upgrade domain at a time, and the applications that were running in the cluster continue to run without any downtime.</span></span> <span data-ttu-id="f6d46-153">De cluster-statusbeleid (een combinatie van het knooppunt status en de status alle toepassingen die worden uitgevoerd in het cluster) om te worden gehouden tijdens de upgrade.</span><span class="sxs-lookup"><span data-stu-id="f6d46-153">The cluster health policies (a combination of node health and the health all the applications running in the cluster) are adhered to during the upgrade.</span></span>

<span data-ttu-id="f6d46-154">Als het statusbeleid cluster niet wordt voldaan, is de upgrade teruggedraaid.</span><span class="sxs-lookup"><span data-stu-id="f6d46-154">If the cluster health policies are not met, the upgrade is rolled back.</span></span> <span data-ttu-id="f6d46-155">Vervolgens wordt een e-mailbericht verzonden naar de eigenaar van het abonnement.</span><span class="sxs-lookup"><span data-stu-id="f6d46-155">Then an email is sent to the owner of the subscription.</span></span> <span data-ttu-id="f6d46-156">Het e-mailbericht bevat de volgende informatie:</span><span class="sxs-lookup"><span data-stu-id="f6d46-156">The email contains the following information:</span></span>

* <span data-ttu-id="f6d46-157">Melding dat we hadden terugdraaien van de upgrade van een cluster.</span><span class="sxs-lookup"><span data-stu-id="f6d46-157">Notification that we had to roll back a cluster upgrade.</span></span>
* <span data-ttu-id="f6d46-158">Voorgestelde corrigerende acties, indien van toepassing.</span><span class="sxs-lookup"><span data-stu-id="f6d46-158">Suggested remedial actions, if any.</span></span>
* <span data-ttu-id="f6d46-159">Het aantal dagen (n) totdat we fase 2 uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="f6d46-159">The number of days (n) until we execute Phase 2.</span></span>

<span data-ttu-id="f6d46-160">We proberen uit te voeren dezelfde upgrade een paar keer geval eventuele upgrades is mislukt door redenen infrastructuur.</span><span class="sxs-lookup"><span data-stu-id="f6d46-160">We try to execute the same upgrade a few more times in case any upgrades failed for infrastructure reasons.</span></span> <span data-ttu-id="f6d46-161">Na de n dagen vanaf de datum waarop die het e-mailbericht is verzonden, gaan we voor fase 2.</span><span class="sxs-lookup"><span data-stu-id="f6d46-161">After the n days from the date the email was sent, we proceed to Phase 2.</span></span>

<span data-ttu-id="f6d46-162">Als de cluster-statusbeleid wordt voldaan, wordt de upgrade beschouwd als geslaagd en als voltooid gemarkeerd.</span><span class="sxs-lookup"><span data-stu-id="f6d46-162">If the cluster health policies are met, the upgrade is considered successful and marked complete.</span></span> <span data-ttu-id="f6d46-163">Dit kan gebeuren tijdens de upgrade of een van de upgrade herhalingen in deze fase.</span><span class="sxs-lookup"><span data-stu-id="f6d46-163">This can happen during the initial upgrade or any of the upgrade reruns in this phase.</span></span> <span data-ttu-id="f6d46-164">Er is geen e-mailbevestiging van een geslaagde uitvoering.</span><span class="sxs-lookup"><span data-stu-id="f6d46-164">There is no email confirmation of a successful run.</span></span> <span data-ttu-id="f6d46-165">Dit is om te voorkomen dat u te veel e-mails--ontvangt een e-mailbericht moet worden gezien als een uitzondering in normale tekst verzonden.</span><span class="sxs-lookup"><span data-stu-id="f6d46-165">This is to avoid sending you too many emails--receiving an email should be seen as an exception to normal.</span></span> <span data-ttu-id="f6d46-166">We verwachten dat de meeste van de cluster-upgrades kan slagen zonder die invloed hebben op de beschikbaarheid van uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="f6d46-166">We expect most of the cluster upgrades to succeed without impacting your application availability.</span></span>

### <a name="phase-2-an-upgrade-is-performed-by-using-default-health-policies-only"></a><span data-ttu-id="f6d46-167">Fase 2: Een upgrade wordt uitgevoerd met behulp van standaard statusbeleid alleen</span><span class="sxs-lookup"><span data-stu-id="f6d46-167">Phase 2: An upgrade is performed by using default health policies only</span></span>
<span data-ttu-id="f6d46-168">Het statusbeleid in deze fase worden ingesteld in zodanig dat het aantal toepassingen die aan het begin van de upgrade in orde zijn hetzelfde voor de duur van het upgradeproces blijft.</span><span class="sxs-lookup"><span data-stu-id="f6d46-168">The health policies in this phase are set in such a way that the number of applications that were healthy at the beginning of the upgrade remains the same for the duration of the upgrade process.</span></span> <span data-ttu-id="f6d46-169">Als fase 1 in de fase 2-upgrades één upgradedomein tegelijk gaan en de toepassingen die worden uitgevoerd in het cluster worden uitgevoerd zonder uitvaltijd.</span><span class="sxs-lookup"><span data-stu-id="f6d46-169">As in Phase 1, the Phase 2 upgrades proceed one upgrade domain at a time, and the applications that were running in the cluster continue to run without any downtime.</span></span> <span data-ttu-id="f6d46-170">De cluster-statusbeleid (een combinatie van het knooppunt status en de status alle toepassingen die worden uitgevoerd in het cluster) aan voor de duur van de upgrade worden gehouden.</span><span class="sxs-lookup"><span data-stu-id="f6d46-170">The cluster health policies (a combination of node health and the health all the applications running in the cluster) are adhered to for the duration of the upgrade.</span></span>

<span data-ttu-id="f6d46-171">Als de cluster-statusbeleid wordt van kracht niet voldaan, is de upgrade teruggedraaid.</span><span class="sxs-lookup"><span data-stu-id="f6d46-171">If the cluster health policies in effect are not met, the upgrade is rolled back.</span></span> <span data-ttu-id="f6d46-172">Vervolgens wordt een e-mailbericht verzonden naar de eigenaar van het abonnement.</span><span class="sxs-lookup"><span data-stu-id="f6d46-172">Then an email is sent to the owner of the subscription.</span></span> <span data-ttu-id="f6d46-173">Het e-mailbericht bevat de volgende informatie:</span><span class="sxs-lookup"><span data-stu-id="f6d46-173">The email contains the following information:</span></span>

* <span data-ttu-id="f6d46-174">Melding dat we hadden terugdraaien van de upgrade van een cluster.</span><span class="sxs-lookup"><span data-stu-id="f6d46-174">Notification that we had to roll back a cluster upgrade.</span></span>
* <span data-ttu-id="f6d46-175">Voorgestelde corrigerende acties, indien van toepassing.</span><span class="sxs-lookup"><span data-stu-id="f6d46-175">Suggested remedial actions, if any.</span></span>
* <span data-ttu-id="f6d46-176">Het aantal dagen (n) totdat we fase 3 uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="f6d46-176">The number of days (n) until we execute Phase 3.</span></span>

<span data-ttu-id="f6d46-177">We proberen uit te voeren dezelfde upgrade een paar keer geval eventuele upgrades is mislukt door redenen infrastructuur.</span><span class="sxs-lookup"><span data-stu-id="f6d46-177">We try to execute the same upgrade a few more times in case any upgrades failed for infrastructure reasons.</span></span> <span data-ttu-id="f6d46-178">Een herinnering is verzonden een paar dagen voordat n dagen actief zijn.</span><span class="sxs-lookup"><span data-stu-id="f6d46-178">A reminder email is sent a couple of days before n days are up.</span></span> <span data-ttu-id="f6d46-179">Na de n dagen vanaf de datum waarop die het e-mailbericht is verzonden, verder we met stap 3.</span><span class="sxs-lookup"><span data-stu-id="f6d46-179">After the n days from the date the email was sent, we proceed to Phase 3.</span></span> <span data-ttu-id="f6d46-180">De e-mailberichten we u in de fase 2 sturen ernstig moeten worden gehaald en corrigerende acties moeten worden genomen.</span><span class="sxs-lookup"><span data-stu-id="f6d46-180">The emails we send you in Phase 2 must be taken seriously and remedial actions must be taken.</span></span>

<span data-ttu-id="f6d46-181">Als de cluster-statusbeleid wordt voldaan, wordt de upgrade beschouwd als geslaagd en als voltooid gemarkeerd.</span><span class="sxs-lookup"><span data-stu-id="f6d46-181">If the cluster health policies are met, the upgrade is considered successful and marked complete.</span></span> <span data-ttu-id="f6d46-182">Dit kan gebeuren tijdens de upgrade of een van de upgrade herhalingen in deze fase.</span><span class="sxs-lookup"><span data-stu-id="f6d46-182">This can happen during the initial upgrade or any of the upgrade reruns in this phase.</span></span> <span data-ttu-id="f6d46-183">Er is geen e-mailbevestiging van een geslaagde uitvoering.</span><span class="sxs-lookup"><span data-stu-id="f6d46-183">There is no email confirmation of a successful run.</span></span>

### <a name="phase-3-an-upgrade-is-performed-by-using-aggressive-health-policies"></a><span data-ttu-id="f6d46-184">Fase 3: Een upgrade wordt uitgevoerd met behulp van agressieve statusbeleid</span><span class="sxs-lookup"><span data-stu-id="f6d46-184">Phase 3: An upgrade is performed by using aggressive health policies</span></span>
<span data-ttu-id="f6d46-185">Deze statusbeleid in deze fase zijn gericht op de voltooiing van de upgrade in plaats van de status van de toepassingen.</span><span class="sxs-lookup"><span data-stu-id="f6d46-185">These health policies in this phase are geared towards completion of the upgrade rather than the health of the applications.</span></span> <span data-ttu-id="f6d46-186">In deze fase eindigen heel weinig cluster-upgrades.</span><span class="sxs-lookup"><span data-stu-id="f6d46-186">Very few cluster upgrades end up in this phase.</span></span> <span data-ttu-id="f6d46-187">Als uw cluster in deze fase wordt, is er een goede kans dat uw toepassing slecht functioneert en/of beschikbaarheid verliezen.</span><span class="sxs-lookup"><span data-stu-id="f6d46-187">If your cluster gets to this phase, there is a good chance that your application becomes unhealthy and/or lose availability.</span></span>

<span data-ttu-id="f6d46-188">Net als bij de andere twee fasen, upgrades voor fase 3 voortgezet één upgradedomein tegelijk.</span><span class="sxs-lookup"><span data-stu-id="f6d46-188">Similar to the other two phases, Phase 3 upgrades proceed one upgrade domain at a time.</span></span>

<span data-ttu-id="f6d46-189">Als het statusbeleid cluster niet wordt voldaan, is de upgrade teruggedraaid.</span><span class="sxs-lookup"><span data-stu-id="f6d46-189">If the cluster health policies are not met, the upgrade is rolled back.</span></span> <span data-ttu-id="f6d46-190">We proberen uit te voeren dezelfde upgrade een paar keer geval eventuele upgrades is mislukt door redenen infrastructuur.</span><span class="sxs-lookup"><span data-stu-id="f6d46-190">We try to execute the same upgrade a few more times in case any upgrades failed for infrastructure reasons.</span></span> <span data-ttu-id="f6d46-191">Het cluster is hierna is vastgemaakt, zodat deze niet langer ondersteuning en/of upgrades ontvangt.</span><span class="sxs-lookup"><span data-stu-id="f6d46-191">After that, the cluster is pinned, so that it will no longer receive support and/or upgrades.</span></span>

<span data-ttu-id="f6d46-192">Een e-mailbericht met deze informatie wordt verzonden naar de eigenaar van het abonnement, samen met de corrigerende acties.</span><span class="sxs-lookup"><span data-stu-id="f6d46-192">An email with this information is sent to the subscription owner, along with the remedial actions.</span></span> <span data-ttu-id="f6d46-193">We verwachten niet alle clusters om op te halen in een status waarbij de fase 3 is mislukt.</span><span class="sxs-lookup"><span data-stu-id="f6d46-193">We do not expect any clusters to get into a state where Phase 3 has failed.</span></span>

<span data-ttu-id="f6d46-194">Als de cluster-statusbeleid wordt voldaan, wordt de upgrade beschouwd als geslaagd en als voltooid gemarkeerd.</span><span class="sxs-lookup"><span data-stu-id="f6d46-194">If the cluster health policies are met, the upgrade is considered successful and marked complete.</span></span> <span data-ttu-id="f6d46-195">Dit kan gebeuren tijdens de upgrade of een van de upgrade herhalingen in deze fase.</span><span class="sxs-lookup"><span data-stu-id="f6d46-195">This can happen during the initial upgrade or any of the upgrade reruns in this phase.</span></span> <span data-ttu-id="f6d46-196">Er is geen e-mailbevestiging van een geslaagde uitvoering.</span><span class="sxs-lookup"><span data-stu-id="f6d46-196">There is no email confirmation of a successful run.</span></span>

## <a name="cluster-configurations-that-you-control"></a><span data-ttu-id="f6d46-197">Clusterconfiguraties die u beheert</span><span class="sxs-lookup"><span data-stu-id="f6d46-197">Cluster configurations that you control</span></span>
<span data-ttu-id="f6d46-198">Naast de mogelijkheid om het cluster upgrademodus, hier zijn de configuraties die u in een live cluster wijzigen kunt.</span><span class="sxs-lookup"><span data-stu-id="f6d46-198">In addition to the ability to set the cluster upgrade mode, Here are the configurations that you can change on a live cluster.</span></span>

### <a name="certificates"></a><span data-ttu-id="f6d46-199">Certificaten</span><span class="sxs-lookup"><span data-stu-id="f6d46-199">Certificates</span></span>
<span data-ttu-id="f6d46-200">U kunt nieuwe toevoegen of verwijderen van certificaten voor het cluster en de client via de portal eenvoudig.</span><span class="sxs-lookup"><span data-stu-id="f6d46-200">You can add new or delete certificates for the cluster and client via the portal easily.</span></span> <span data-ttu-id="f6d46-201">Raadpleeg [dit document voor gedetailleerde instructies](service-fabric-cluster-security-update-certs-azure.md)</span><span class="sxs-lookup"><span data-stu-id="f6d46-201">Refer to [this document for detailed instructions](service-fabric-cluster-security-update-certs-azure.md)</span></span>

![Schermafbeelding van certificaatvingerafdrukken in de Azure portal.][CertificateUpgrade]

### <a name="application-ports"></a><span data-ttu-id="f6d46-203">Poorten van de toepassing</span><span class="sxs-lookup"><span data-stu-id="f6d46-203">Application ports</span></span>
<span data-ttu-id="f6d46-204">U kunt poorten van de toepassing wijzigen door de Load Balancer resource-eigenschappen die gekoppeld aan het knooppunttype zijn te wijzigen.</span><span class="sxs-lookup"><span data-stu-id="f6d46-204">You can change application ports by changing the Load Balancer resource properties that are associated with the node type.</span></span> <span data-ttu-id="f6d46-205">U kunt de portal gebruiken of kunt u rechtstreeks Resource Manager PowerShell gebruiken.</span><span class="sxs-lookup"><span data-stu-id="f6d46-205">You can use the portal, or you can use Resource Manager PowerShell directly.</span></span>

<span data-ttu-id="f6d46-206">U opent een nieuwe poort op alle virtuele machines in een knooppunttype door het volgende doen:</span><span class="sxs-lookup"><span data-stu-id="f6d46-206">To open a new port on all VMs in a node type, do the following:</span></span>

1. <span data-ttu-id="f6d46-207">Een nieuwe test toevoegen aan de geschikte load balancer.</span><span class="sxs-lookup"><span data-stu-id="f6d46-207">Add a new probe to the appropriate load balancer.</span></span>
   
    <span data-ttu-id="f6d46-208">Als u uw cluster hebt geïmplementeerd met behulp van de portal, de load balancers zijn met de naam 'LB-naam van de Resource-group-NodeTypename', één voor elk knooppunttype.</span><span class="sxs-lookup"><span data-stu-id="f6d46-208">If you deployed your cluster by using the portal, the load balancers are named "LB-name of the Resource group-NodeTypename", one for each node type.</span></span> <span data-ttu-id="f6d46-209">Omdat de load balancer-namen uniek alleen binnen een resourcegroep zijn, wordt het aanbevolen als u naar deze onder een bepaalde resourcegroep zoekt.</span><span class="sxs-lookup"><span data-stu-id="f6d46-209">Since the load balancer names are unique only within a resource group, it is best if you search for them under a specific resource group.</span></span>
   
    ![Schermafbeelding van een test toe te voegen aan een load balancer in de portal.][AddingProbes]
2. <span data-ttu-id="f6d46-211">Een nieuwe regel toevoegen aan de load balancer.</span><span class="sxs-lookup"><span data-stu-id="f6d46-211">Add a new rule to the load balancer.</span></span>
   
    <span data-ttu-id="f6d46-212">Een nieuwe regel toevoegen aan dezelfde load balancer met behulp van de test op die u in de vorige stap hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="f6d46-212">Add a new rule to the same load balancer by using the probe that you created in the previous step.</span></span>
   
    ![Een nieuwe regel toe te voegen aan een load balancer in de portal.][AddingLBRules]

### <a name="placement-properties"></a><span data-ttu-id="f6d46-214">Plaatsingseigenschappen</span><span class="sxs-lookup"><span data-stu-id="f6d46-214">Placement properties</span></span>
<span data-ttu-id="f6d46-215">U kunt aangepaste plaatsingseigenschappen die u wilt gebruiken in uw toepassingen toevoegen voor elk van de knooppunttypen.</span><span class="sxs-lookup"><span data-stu-id="f6d46-215">For each of the node types, you can add custom placement properties that you want to use in your applications.</span></span> <span data-ttu-id="f6d46-216">NodeType is een standaardeigenschap die u gebruiken kunt zonder deze expliciet toe te voegen.</span><span class="sxs-lookup"><span data-stu-id="f6d46-216">NodeType is a default property that you can use without adding it explicitly.</span></span>

> [!NOTE]
> <span data-ttu-id="f6d46-217">Raadpleeg voor meer informatie over het gebruik van plaatsingsbeperkingen, knooppunteigenschappen en hoe ze kunnen worden gedefinieerd aan de sectie 'Plaatsing beperkingen en eigenschappen van knooppunt' in het Service Fabric-Cluster Resource Manager-Document op [met een beschrijving van uw Cluster](service-fabric-cluster-resource-manager-cluster-description.md).</span><span class="sxs-lookup"><span data-stu-id="f6d46-217">For details on the use of placement constraints, node properties, and how to define them, refer to the section "Placement Constraints and Node Properties" in the Service Fabric Cluster Resource Manager Document on [Describing Your Cluster](service-fabric-cluster-resource-manager-cluster-description.md).</span></span>
> 
> 

### <a name="capacity-metrics"></a><span data-ttu-id="f6d46-218">Capaciteit metrische gegevens</span><span class="sxs-lookup"><span data-stu-id="f6d46-218">Capacity metrics</span></span>
<span data-ttu-id="f6d46-219">U kunt voor elk van de knooppunttypen aangepaste capaciteit metrische gegevens die u wilt gebruiken in uw toepassingen en rapporteren over de belasting toevoegen.</span><span class="sxs-lookup"><span data-stu-id="f6d46-219">For each of the node types, you can add custom capacity metrics that you want to use in your applications to report load.</span></span> <span data-ttu-id="f6d46-220">Raadpleeg voor meer informatie over het gebruik van metrische gegevens voor capaciteit om te rapporteren over de belasting op de Service Fabric-Cluster Resource Manager-documenten op [met een beschrijving van uw Cluster](service-fabric-cluster-resource-manager-cluster-description.md) en [metrische gegevens en de belasting](service-fabric-cluster-resource-manager-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="f6d46-220">For details on the use of capacity metrics to report load, refer to the Service Fabric Cluster Resource Manager Documents on [Describing Your Cluster](service-fabric-cluster-resource-manager-cluster-description.md) and [Metrics and Load](service-fabric-cluster-resource-manager-metrics.md).</span></span>

### <a name="fabric-upgrade-settings---health-polices"></a><span data-ttu-id="f6d46-221">Instellingen voor fabric-upgrade - Health-beleid</span><span class="sxs-lookup"><span data-stu-id="f6d46-221">Fabric upgrade settings - Health polices</span></span>
<span data-ttu-id="f6d46-222">U kunt opgeven om de gezondheid van aangepaste beleidsregels voor fabric-upgrade.</span><span class="sxs-lookup"><span data-stu-id="f6d46-222">You can specify custom health polices for fabric upgrade.</span></span> <span data-ttu-id="f6d46-223">Als u uw cluster automatische fabric-upgrades hebt ingesteld, krijgen deze beleidsregels toegepast op de fase-1 van de automatische fabric-upgrades.</span><span class="sxs-lookup"><span data-stu-id="f6d46-223">If you have set your cluster to Automatic fabric upgrades, then these policies get applied to the Phase-1 of the automatic fabric upgrades.</span></span>
<span data-ttu-id="f6d46-224">Als u hebt uw cluster voor handmatige fabric upgrades ingesteld, krijgen deze beleidsregels telkens wanneer die u een nieuwe versie activatie van het systeem ere van de fabric-upgrade in uw cluster selecteert toegepast.</span><span class="sxs-lookup"><span data-stu-id="f6d46-224">If you have set your cluster for Manual fabric upgrades, then these policies get applied each time you select a new version triggering the system to kick off the fabric upgrade in your cluster.</span></span> <span data-ttu-id="f6d46-225">Als u het beleid niet overschrijven, worden de standaardwaarden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="f6d46-225">If you do not override the policies, the defaults are used.</span></span>

<span data-ttu-id="f6d46-226">U kunt de aangepaste statusbeleid opgeven of de huidige instellingen onder de blade 'fabric-upgrade' bekijken door het selecteren van de geavanceerde instellingen voor de upgrade.</span><span class="sxs-lookup"><span data-stu-id="f6d46-226">You can specify the custom health policies or review the current settings under the "fabric upgrade" blade, by selecting the advanced upgrade settings.</span></span> <span data-ttu-id="f6d46-227">Bekijk de volgende afbeelding voor het.</span><span class="sxs-lookup"><span data-stu-id="f6d46-227">Review the following picture on how to.</span></span> 

![Aangepaste statusbeleid beheren][HealthPolices]

### <a name="customize-fabric-settings-for-your-cluster"></a><span data-ttu-id="f6d46-229">Fabric-instellingen voor uw cluster aanpassen</span><span class="sxs-lookup"><span data-stu-id="f6d46-229">Customize Fabric settings for your cluster</span></span>
<span data-ttu-id="f6d46-230">Raadpleeg [service fabric-clusterinstellingen fabric](service-fabric-cluster-fabric-settings.md) op wat en hoe u ze kunt aanpassen.</span><span class="sxs-lookup"><span data-stu-id="f6d46-230">Refer to [service fabric cluster fabric settings](service-fabric-cluster-fabric-settings.md) on what and how you can customize them.</span></span>

### <a name="os-patches-on-the-vms-that-make-up-the-cluster"></a><span data-ttu-id="f6d46-231">OS patches op de virtuele machines die gezamenlijk van het cluster</span><span class="sxs-lookup"><span data-stu-id="f6d46-231">OS patches on the VMs that make up the cluster</span></span>
<span data-ttu-id="f6d46-232">Raadpleeg [Patch Orchestration toepassing](service-fabric-patch-orchestration-application.md) waarop kan worden geïmplementeerd op het cluster om patches te installeren via Windows Update op een geregiseerde manier, de tijd om de beschikbare services te houden.</span><span class="sxs-lookup"><span data-stu-id="f6d46-232">Refer to [Patch Orchestration Application](service-fabric-patch-orchestration-application.md) which can be deployed on your cluster to install patches from Windows Update in an orchestrated manner, keeping the services available all the time.</span></span> 

### <a name="os-upgrades-on-the-vms-that-make-up-the-cluster"></a><span data-ttu-id="f6d46-233">Upgrades voor het besturingssysteem op de virtuele machines die gezamenlijk van het cluster</span><span class="sxs-lookup"><span data-stu-id="f6d46-233">OS upgrades on the VMs that make up the cluster</span></span>
<span data-ttu-id="f6d46-234">Als u de installatiekopie van het besturingssysteem op de virtuele machines van het cluster upgraden moet, moet u dit één VM doen op een tijdstip.</span><span class="sxs-lookup"><span data-stu-id="f6d46-234">If you must upgrade the OS image on the virtual machines of the cluster, you must do it one VM at a time.</span></span> <span data-ttu-id="f6d46-235">U bent zelf verantwoordelijk voor deze upgrade--er is momenteel geen automation voor deze.</span><span class="sxs-lookup"><span data-stu-id="f6d46-235">You are responsible for this upgrade--there is currently no automation for this.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f6d46-236">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="f6d46-236">Next steps</span></span>
* <span data-ttu-id="f6d46-237">Informatie over het aanpassen van enkele van de [service fabric-clusterinstellingen fabric](service-fabric-cluster-fabric-settings.md)</span><span class="sxs-lookup"><span data-stu-id="f6d46-237">Learn how to customize some of the [service fabric cluster fabric settings](service-fabric-cluster-fabric-settings.md)</span></span>
* <span data-ttu-id="f6d46-238">Meer informatie over hoe u [in en uit het cluster schalen](service-fabric-cluster-scale-up-down.md)</span><span class="sxs-lookup"><span data-stu-id="f6d46-238">Learn how to [scale your cluster in and out](service-fabric-cluster-scale-up-down.md)</span></span>
* <span data-ttu-id="f6d46-239">Meer informatie over [toepassingsupgrades](service-fabric-application-upgrade.md)</span><span class="sxs-lookup"><span data-stu-id="f6d46-239">Learn about [application upgrades](service-fabric-application-upgrade.md)</span></span>

<!--Image references-->
[CertificateUpgrade]: ./media/service-fabric-cluster-upgrade/CertificateUpgrade2.png
[AddingProbes]: ./media/service-fabric-cluster-upgrade/addingProbes2.PNG
[AddingLBRules]: ./media/service-fabric-cluster-upgrade/addingLBRules.png
[HealthPolices]: ./media/service-fabric-cluster-upgrade/Manage_AutomodeWadvSettings.PNG
[ARMUpgradeMode]: ./media/service-fabric-cluster-upgrade/ARMUpgradeMode.PNG
[Create_Manualmode]: ./media/service-fabric-cluster-upgrade/Create_Manualmode.PNG
[Manage_Automaticmode]: ./media/service-fabric-cluster-upgrade/Manage_Automaticmode.PNG

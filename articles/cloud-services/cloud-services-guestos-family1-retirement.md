---
title: u ziet aaaGuest OS-familie 1 buiten gebruik stellen | Microsoft Docs
description: Bevat informatie over hoe en wanneer hello Azure Gast OS-familie 1 buiten gebruik stellen, is er gebeurd toodetermine als u last
services: cloud-services
documentationcenter: na
author: raiye
manager: timlt
editor: 
ms.assetid: 37b422e9-0713-4a81-a942-f553ef478064
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 5/21/2017
ms.author: raiye
ms.openlocfilehash: fa8b904c6560dbbe4982c301f818c7a5cbc4eacb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="guest-os-family-1-retirement-notice"></a><span data-ttu-id="3b93f-103">U ziet het buiten gebruik stellen van Gast OS-familie 1</span><span class="sxs-lookup"><span data-stu-id="3b93f-103">Guest OS Family 1 retirement notice</span></span>
<span data-ttu-id="3b93f-104">Hallo buiten gebruik stellen van OS-familie 1 werd eerst aangekondigd op 1 juni 2013.</span><span class="sxs-lookup"><span data-stu-id="3b93f-104">hello retirement of OS Family 1 was first announced on June 1, 2013.</span></span>

<span data-ttu-id="3b93f-105">**2 september 2014** hello Azure gastbesturingssysteem (Gast OS) familie 1.x, die is gebaseerd op Hallo van Windows Server 2008-besturingssysteem, is officieel buiten gebruik gesteld.</span><span class="sxs-lookup"><span data-stu-id="3b93f-105">**Sept 2, 2014** hello Azure Guest operating system (Guest OS) Family 1.x, which is based on hello Windows Server 2008 operating system, was officially retired.</span></span> <span data-ttu-id="3b93f-106">Alle pogingen toodeploy nieuwe services of upgrade bestaande services met behulp van familie 1 mislukt met een foutbericht weergegeven waarin wordt gemeld dat Hallo dat Gast OS-familie 1 is buiten gebruik gesteld.</span><span class="sxs-lookup"><span data-stu-id="3b93f-106">All attempts toodeploy new services or upgrade existing services using Family 1 will fail with an error message informing you that hello Guest OS Family 1 has been retired.</span></span>

<span data-ttu-id="3b93f-107">**3 november 2014** uitgebreide ondersteuning voor gast OS-familie 1 beëindigd en het is volledig buiten gebruik gesteld.</span><span class="sxs-lookup"><span data-stu-id="3b93f-107">**November 3, 2014** Extended support for Guest OS Family 1 ended and it is fully retired.</span></span> <span data-ttu-id="3b93f-108">Alle services nog steeds op familie 1 zullen worden beïnvloed.</span><span class="sxs-lookup"><span data-stu-id="3b93f-108">All services still on Family 1 will be impacted.</span></span> <span data-ttu-id="3b93f-109">We kunnen deze services op elk gewenst moment stoppen.</span><span class="sxs-lookup"><span data-stu-id="3b93f-109">We may stop those services at any time.</span></span> <span data-ttu-id="3b93f-110">Er is geen garantie dat uw services blijven toorun tenzij u handmatig ze zelf bijwerken.</span><span class="sxs-lookup"><span data-stu-id="3b93f-110">There is no guarantee your services will continue toorun unless you manually upgrade them yourself.</span></span>

<span data-ttu-id="3b93f-111">Als u aanvullende vragen hebt, gaat u naar Hallo [Cloud Services-Forums](http://social.msdn.microsoft.com/Forums/home?forum=windowsazuredevelopment&filter=alltypes&sort=lastpostdesc) of [Neem contact op met de ondersteuning van Azure](https://azure.microsoft.com/support/options/).</span><span class="sxs-lookup"><span data-stu-id="3b93f-111">If you have additional questions, visit hello [Cloud Services Forums](http://social.msdn.microsoft.com/Forums/home?forum=windowsazuredevelopment&filter=alltypes&sort=lastpostdesc) or [contact Azure support](https://azure.microsoft.com/support/options/).</span></span>

## <a name="are-you-affected"></a><span data-ttu-id="3b93f-112">Worden beïnvloed?</span><span class="sxs-lookup"><span data-stu-id="3b93f-112">Are you affected?</span></span>
<span data-ttu-id="3b93f-113">Uw Cloud-Services worden beïnvloed als een van de volgende Hallo van toepassing is:</span><span class="sxs-lookup"><span data-stu-id="3b93f-113">Your Cloud Services are affected if any one of hello following applies:</span></span>

1. <span data-ttu-id="3b93f-114">U hebt een waarde van ' osFamily = "1" expliciet worden opgegeven in Hallo ServiceConfiguration.cscfg-bestand voor de Cloudservice.</span><span class="sxs-lookup"><span data-stu-id="3b93f-114">You have a value of "osFamily = "1" explicitly specified in hello ServiceConfiguration.cscfg file for your Cloud Service.</span></span>
2. <span data-ttu-id="3b93f-115">U beschikt niet over een waarde voor osFamily expliciet worden opgegeven in Hallo ServiceConfiguration.cscfg-bestand voor de Cloudservice.</span><span class="sxs-lookup"><span data-stu-id="3b93f-115">You do not have a value for osFamily explicitly specified in hello ServiceConfiguration.cscfg file for your Cloud Service.</span></span> <span data-ttu-id="3b93f-116">Op dit moment Hallo system gebruikt Hallo standaardwaarde '1' in dit geval.</span><span class="sxs-lookup"><span data-stu-id="3b93f-116">Currently, hello system uses hello default value of "1" in this case.</span></span>
3. <span data-ttu-id="3b93f-117">de waarde van de familie gastbesturingssysteem bevat Hello Azure-portal als 'WindowsServer 2008'.</span><span class="sxs-lookup"><span data-stu-id="3b93f-117">hello Azure portal lists your Guest Operating System family value as "Windows Server 2008".</span></span>

<span data-ttu-id="3b93f-118">toofind welke van uw cloudservices welke OS-familie worden uitgevoerd, kunt u Hallo volgende script in Azure PowerShell uitvoeren als u moet [instellen van Azure PowerShell](/powershell/azureps-cmdlets-docs) eerste.</span><span class="sxs-lookup"><span data-stu-id="3b93f-118">toofind which of your cloud services are running which OS Family, you can run hello following script in Azure PowerShell, though you must [set up Azure PowerShell](/powershell/azureps-cmdlets-docs) first.</span></span> <span data-ttu-id="3b93f-119">Zie voor meer informatie over Hallo script [Azure Gast OS-familie 1 einde van de levenscyclus: juni 2014](http://blogs.msdn.com/b/ryberry/archive/2014/04/02/azure-guest-os-family-1-end-of-life-june-2014.aspx).</span><span class="sxs-lookup"><span data-stu-id="3b93f-119">For more information on hello script, see [Azure Guest OS Family 1 End of Life: June 2014](http://blogs.msdn.com/b/ryberry/archive/2014/04/02/azure-guest-os-family-1-end-of-life-june-2014.aspx).</span></span>

```Powershell
foreach($subscription in Get-AzureSubscription) {
    Select-AzureSubscription -SubscriptionName $subscription.SubscriptionName

    $deployments=get-azureService | get-azureDeployment -ErrorAction Ignore | where {$_.SdkVersion -NE ""}

    $deployments | ft @{Name="SubscriptionName";Expression={$subscription.SubscriptionName}}, ServiceName, SdkVersion, Slot, @{Name="osFamily";Expression={(select-xml -content $_.configuration -xpath "/ns:ServiceConfiguration/@osFamily" -namespace $namespace).node.value }}, osVersion, Status, URL
}
```

<span data-ttu-id="3b93f-120">Uw cloudservices zullen worden beïnvloed door de OS-familie 1 buiten gebruik stellen als Hallo besturingssysteemtype kolom in de scriptuitvoer Hallo leeg is of bevat een '1'.</span><span class="sxs-lookup"><span data-stu-id="3b93f-120">Your cloud services will be impacted by OS Family 1 retirement if hello osFamily column in hello script output is empty or contains a "1".</span></span>

## <a name="recommendations-if-you-are-affected"></a><span data-ttu-id="3b93f-121">Aanbevelingen als u last</span><span class="sxs-lookup"><span data-stu-id="3b93f-121">Recommendations if you are affected</span></span>
<span data-ttu-id="3b93f-122">U wordt aangeraden dat u uw Cloudservice rollen tooone van Hallo ondersteund Gast OS-familie migreren:</span><span class="sxs-lookup"><span data-stu-id="3b93f-122">We recommend you migrate your Cloud Service roles tooone of hello supported Guest OS Families:</span></span>

<span data-ttu-id="3b93f-123">**Gast OS-familie 4.x** -Windows Server 2012 R2 *(aanbevolen)*</span><span class="sxs-lookup"><span data-stu-id="3b93f-123">**Guest OS family 4.x** - Windows Server 2012 R2 *(recommended)*</span></span>

1. <span data-ttu-id="3b93f-124">Zorg ervoor dat uw toepassing van SDK 2.1 of hoger met .NET framework 4.0, 4.5 en 4.5.1 gebruikmaakt.</span><span class="sxs-lookup"><span data-stu-id="3b93f-124">Ensure that your application is using SDK 2.1 or later with .NET framework 4.0, 4.5 or 4.5.1.</span></span>
2. <span data-ttu-id="3b93f-125">Hallo osFamily-kenmerk te "4" in hello ServiceConfiguration.cscfg bestand ingesteld en implementeer uw cloudservice opnieuw.</span><span class="sxs-lookup"><span data-stu-id="3b93f-125">Set hello osFamily attribute too“4” in hello ServiceConfiguration.cscfg file, and redeploy your cloud service.</span></span>

<span data-ttu-id="3b93f-126">**Gast OS-familie 3.x** -Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="3b93f-126">**Guest OS family 3.x** - Windows Server 2012</span></span>

1. <span data-ttu-id="3b93f-127">Zorg ervoor dat uw toepassing van SDK 1.8 of hoger met .NET framework 4.0 of 4.5 gebruikmaakt.</span><span class="sxs-lookup"><span data-stu-id="3b93f-127">Ensure that your application is using SDK 1.8 or later with .NET framework 4.0 or 4.5.</span></span>
2. <span data-ttu-id="3b93f-128">Hallo osFamily-kenmerk te "3" in hello ServiceConfiguration.cscfg bestand ingesteld en implementeer uw cloudservice opnieuw.</span><span class="sxs-lookup"><span data-stu-id="3b93f-128">Set hello osFamily attribute too“3” in hello ServiceConfiguration.cscfg file, and redeploy your cloud service.</span></span>

<span data-ttu-id="3b93f-129">**Gast OS-familie 2.x** -Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="3b93f-129">**Guest OS family 2.x** - Windows Server 2008 R2</span></span>

1. <span data-ttu-id="3b93f-130">Zorg ervoor dat uw toepassing van SDK 1.3 gebruikmaakt en hoger met .NET framework 3.5 of 4.0.</span><span class="sxs-lookup"><span data-stu-id="3b93f-130">Ensure that your application is using SDK 1.3 and above with .NET framework 3.5 or 4.0.</span></span>
2. <span data-ttu-id="3b93f-131">Hallo osFamily-kenmerk te '2' in hello ServiceConfiguration.cscfg bestand ingesteld en implementeer uw cloudservice opnieuw.</span><span class="sxs-lookup"><span data-stu-id="3b93f-131">Set hello osFamily attribute too"2" in hello ServiceConfiguration.cscfg file, and redeploy your cloud service.</span></span>

## <a name="extended-support-for-guest-os-family-1-ended-nov-3-2014"></a><span data-ttu-id="3b93f-132">Uitgebreide ondersteuning voor de Gast OS-familie 1 afgelopen 3 november 2014</span><span class="sxs-lookup"><span data-stu-id="3b93f-132">Extended Support for Guest OS Family 1 ended Nov 3, 2014</span></span>
<span data-ttu-id="3b93f-133">Cloudservices op de Gast OS-familie 1 worden niet langer ondersteund.</span><span class="sxs-lookup"><span data-stu-id="3b93f-133">Cloud services on Guest OS family 1 are no longer supported.</span></span> <span data-ttu-id="3b93f-134">Migratie uitgeschakeld familie 1 zo snel mogelijk tooavoid service wordt onderbroken.</span><span class="sxs-lookup"><span data-stu-id="3b93f-134">Migrate off family 1 as soon as possible tooavoid service disruption.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="3b93f-135">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="3b93f-135">Next steps</span></span>
<span data-ttu-id="3b93f-136">Laatste controle Hallo [Gast OS releases](cloud-services-guestos-update-matrix.md).</span><span class="sxs-lookup"><span data-stu-id="3b93f-136">Review hello latest [Guest OS releases](cloud-services-guestos-update-matrix.md).</span></span>

---
title: aaaAzure SDK voor .NET 2.9 Release-opmerkingen
description: Azure SDK voor .NET 2.9 Release-opmerkingen
services: app-service\web
documentationcenter: .net
author: chrissfanos
editor: 
ms.assetid: c83d815b-fc19-4260-821e-7d2a7206dffc
ms.service: app-service
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 02/24/2017
ms.author: juliako
ms.openlocfilehash: 96df2b80224190cc2093e6bf350eaec224ac2e98
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sdk-for-net-29-release-notes"></a><span data-ttu-id="a9f2f-103">Azure SDK voor .NET 2.9 release-opmerkingen</span><span class="sxs-lookup"><span data-stu-id="a9f2f-103">Azure SDK for .NET 2.9 release notes</span></span>

<span data-ttu-id="a9f2f-104">Dit onderwerp bevat opmerkingen bij de release voor versies 2.9 en 2.9.6 van Azure SDK voor .NET.</span><span class="sxs-lookup"><span data-stu-id="a9f2f-104">This topic includes release notes for versions 2.9 and 2.9.6 of Azure SDK for .NET.</span></span>

##<a name="azure-sdk-for-net-296-release-summary"></a><span data-ttu-id="a9f2f-105">Azure SDK voor .NET 2.9.6 release samenvatting</span><span class="sxs-lookup"><span data-stu-id="a9f2f-105">Azure SDK for .NET 2.9.6 release summary</span></span>

<span data-ttu-id="a9f2f-106">Releasedatum: 16-11-2016</span><span class="sxs-lookup"><span data-stu-id="a9f2f-106">Release date: 11/16/2016</span></span>
 
<span data-ttu-id="a9f2f-107">Er zijn geen recente wijzigingen toohello Azure SDK 2.9 zijn geïntroduceerd in deze release.</span><span class="sxs-lookup"><span data-stu-id="a9f2f-107">No breaking changes toohello Azure SDK 2.9 have been introduced in this release.</span></span> <span data-ttu-id="a9f2f-108">Er is ook geen tooleverage upgradeproces nodig deze SDK met bestaande Cloud Service-projecten.</span><span class="sxs-lookup"><span data-stu-id="a9f2f-108">There is also no upgrade process needed tooleverage this SDK with existing Cloud Service projects.</span></span>

### <a name="visual-studio-2017-release-candidate"></a><span data-ttu-id="a9f2f-109">Visual Studio 2017 Release Candidate</span><span class="sxs-lookup"><span data-stu-id="a9f2f-109">Visual Studio 2017 Release Candidate</span></span>

- <span data-ttu-id="a9f2f-110">In Visual Studio 2017 RC, wordt deze versie van hello Azure SDK voor .NET ingebouwd in hello Azure werkbelasting.</span><span class="sxs-lookup"><span data-stu-id="a9f2f-110">In Visual Studio 2017 RC, this release of hello Azure SDK for .NET is built in in hello Azure Workload.</span></span> <span data-ttu-id="a9f2f-111">Alle Hallo-hulpprogramma's, moet u toodo ontwikkelen van Azure zal onderdeel zijn van Visual Studio 2017 RC voortaan.</span><span class="sxs-lookup"><span data-stu-id="a9f2f-111">All hello tools you need toodo Azure development will be part of Visual Studio 2017 RC going forward.</span></span> <span data-ttu-id="a9f2f-112">Voor Visual Studio 2015 en Visual Studio 2013 steeds Hallo SDK nog beschikbaar is via WebPI.</span><span class="sxs-lookup"><span data-stu-id="a9f2f-112">For Visual Studio 2015 and Visual Studio 2013, hello SDK will still be available through WebPI.</span></span> <span data-ttu-id="a9f2f-113">We zullen worden beëindigde Azure SDK voor .NET-versies voor Visual Studio 2013 wanneer Visual Studio 2017 als laatste product loslaat.</span><span class="sxs-lookup"><span data-stu-id="a9f2f-113">We will be discontinuing Azure SDK for .NET releases for Visual Studio 2013, when Visual Studio 2017 releases as a final product.</span></span> <span data-ttu-id="a9f2f-114">Volg deze link toodownload Visual Studio 2017 RC: https://www.visualstudio.com/vs/visual-studio-2017-rc/</span><span class="sxs-lookup"><span data-stu-id="a9f2f-114">Follow this link toodownload Visual Studio 2017 RC: https://www.visualstudio.com/vs/visual-studio-2017-rc/</span></span>

### <a name="azure-diagnostics"></a><span data-ttu-id="a9f2f-115">Azure Diagnostics</span><span class="sxs-lookup"><span data-stu-id="a9f2f-115">Azure Diagnostics</span></span>

- <span data-ttu-id="a9f2f-116">Een gedeeltelijke verbindingsreeks gewijzigde Hallo gedrag tooonly opslaan met Hallo sleutel vervangen door een token voor de verbindingsreeks voor opslag van Cloud Services-diagnostische gegevens.</span><span class="sxs-lookup"><span data-stu-id="a9f2f-116">Changed hello behavior tooonly store a partial connection string with hello key replaced by a token for Cloud Services diagnostics storage connection string.</span></span> <span data-ttu-id="a9f2f-117">de werkelijke opslagsleutel Hallo worden nu opgeslagen in de map gebruikersprofiel Hallo zodat de toegang kan worden beheerd.</span><span class="sxs-lookup"><span data-stu-id="a9f2f-117">hello actual storage key is now stored in hello user profile folder so its access can be controlled.</span></span> <span data-ttu-id="a9f2f-118">Visual Studio wordt Hallo-opslagsleutel lezen uit de map voor lokale foutopsporing en publicatieproces gebruikersprofiel.</span><span class="sxs-lookup"><span data-stu-id="a9f2f-118">Visual Studio will read hello storage key from user profile folder for local debugging and publishing process.</span></span> 
- <span data-ttu-id="a9f2f-119">In het antwoord toohello wijziging die hierboven worden beschreven, team Visual Studio Online verbeterde hello Azure Cloud Services-implementatiesjabloon taak zodat gebruikers Hallo-opslagsleutel voor het instellen van de extensie voor diagnostische gegevens bij het publiceren van tooAzure in continue integratie kunnen opgeven en implementatie.</span><span class="sxs-lookup"><span data-stu-id="a9f2f-119">In response toohello change described above, Visual Studio Online team enhanced hello Azure Cloud Services deployment task template so users could specify hello storage key for setting diagnostics extension when publishing tooAzure in Continuous Integration and Deployment.</span></span>
- <span data-ttu-id="a9f2f-120">We hebben het mogelijke toostore beveiligde verbindingsreeks en tokeniseren voor Azure Diagnostics (af), het oplossen van problemen met configuratie over environements toohelp aangebracht.</span><span class="sxs-lookup"><span data-stu-id="a9f2f-120">We’ve made it possible toostore secure connection string and tokenization for Azure Diagnostics (WAD), toohelp you solve problems with configuration across environements.</span></span>
 
### <a name="windows-server-2016-virtual-machines"></a><span data-ttu-id="a9f2f-121">Windows Server 2016 virtuele machines</span><span class="sxs-lookup"><span data-stu-id="a9f2f-121">Windows Server 2016 virtual machines</span></span>

- <span data-ttu-id="a9f2f-122">Visual Studio ondersteunt nu implementeren Cloudservices tooOS familie 5 (Windows Server 2016) virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="a9f2f-122">Visual Studio now supports deploying Cloud Services tooOS Family 5 (Windows Server 2016) virtual machines.</span></span> <span data-ttu-id="a9f2f-123">Voor bestaande cloudservices, kunt u uw instellingen tootarget Hallo van nieuwe OS-familie.</span><span class="sxs-lookup"><span data-stu-id="a9f2f-123">For existing cloud services, you can change your settings tootarget hello new OS Family.</span></span> <span data-ttu-id="a9f2f-124">Bij het maken van nieuwe cloudservices als u ervoor kiest toocreate Hallo service met .net 4.6 of hoger, wordt standaard Hallo service toouse OS-familie 5.</span><span class="sxs-lookup"><span data-stu-id="a9f2f-124">When creating new cloud services, if you choose toocreate hello service using .net 4.6 or higher, it will default hello service toouse OS Family 5.</span></span>  <span data-ttu-id="a9f2f-125">Voor meer informatie kunt u bekijken Hallo [Gastbesturingssysteemgroep ondersteunen tabel](https://azure.microsoft.com/en-us/documentation/articles/cloud-services-guestos-update-matrix/).</span><span class="sxs-lookup"><span data-stu-id="a9f2f-125">For more information, you can review hello [Guest OS Family support table](https://azure.microsoft.com/en-us/documentation/articles/cloud-services-guestos-update-matrix/).</span></span>

#### <a name="known-issues"></a><span data-ttu-id="a9f2f-126">Bekende problemen</span><span class="sxs-lookup"><span data-stu-id="a9f2f-126">Known issues</span></span>

- <span data-ttu-id="a9f2f-127">Azure .NET SDK 2.9.6 geïntroduceerd een beperking die blokkeert de implementatie van niet-ondersteunde .NET frameworks (zoals .NET 4.6) tooany OS-familie met projecten < 5.</span><span class="sxs-lookup"><span data-stu-id="a9f2f-127">Azure .NET SDK 2.9.6 introduced a restriction that blocks deployment of projects using unsupported .NET frameworks (such as .NET 4.6) tooany OS Family < 5.</span></span> <span data-ttu-id="a9f2f-128">Een tijdelijke oplossing wordt aangeboden [hier](https://github.com/MicrosoftDocs/azure-cloud-services-files/tree/master/Azure%20Targets%20SDK%202.9).</span><span class="sxs-lookup"><span data-stu-id="a9f2f-128">A workaround is provided [here](https://github.com/MicrosoftDocs/azure-cloud-services-files/tree/master/Azure%20Targets%20SDK%202.9).</span></span>

 
### <a name="azure-in-role-cache"></a><span data-ttu-id="a9f2f-129">Azure In-Role Cache</span><span class="sxs-lookup"><span data-stu-id="a9f2f-129">Azure In-Role Cache</span></span> 

- <span data-ttu-id="a9f2f-130">Ondersteuning voor Azure In-Role Cache eindigt op 30 November 2016.</span><span class="sxs-lookup"><span data-stu-id="a9f2f-130">Support for Azure In-Role Cache ends on November 30, 2016.</span></span> <span data-ttu-id="a9f2f-131">Klik voor meer informatie [hier](https://azure.microsoft.com/en-us/blog/azure-managed-cache-and-in-role-cache-services-to-be-retired-on-11-30-2016/).</span><span class="sxs-lookup"><span data-stu-id="a9f2f-131">For more details, click [here](https://azure.microsoft.com/en-us/blog/azure-managed-cache-and-in-role-cache-services-to-be-retired-on-11-30-2016/).</span></span>

### <a name="azure-resource-manager-templates-for-azure-stack"></a><span data-ttu-id="a9f2f-132">Azure Resource Manager-sjablonen voor Azure Stack</span><span class="sxs-lookup"><span data-stu-id="a9f2f-132">Azure Resource Manager Templates for Azure Stack</span></span>

- <span data-ttu-id="a9f2f-133">Hebben wij de Stack Azure als het implementatiedoel van een voor uw Azure Resource Manager-sjablonen.</span><span class="sxs-lookup"><span data-stu-id="a9f2f-133">We’ve introduced Azure Stack as a deployment target for your Azure Resource Manager Templates.</span></span>


## <a name="azure-sdk-for-net-29-summary"></a><span data-ttu-id="a9f2f-134">Azure SDK voor .NET 2.9 samenvatting</span><span class="sxs-lookup"><span data-stu-id="a9f2f-134">Azure SDK for .NET 2.9 summary</span></span>

## <a name="overview"></a><span data-ttu-id="a9f2f-135">Overzicht</span><span class="sxs-lookup"><span data-stu-id="a9f2f-135">Overview</span></span>
<span data-ttu-id="a9f2f-136">Dit document bevat Hallo release-opmerkingen voor hello Azure SDK voor .NET 2.9 release.</span><span class="sxs-lookup"><span data-stu-id="a9f2f-136">This document contains hello release notes for hello Azure SDK for .NET 2.9 release.</span></span> 

<span data-ttu-id="a9f2f-137">Zie voor gedetailleerde informatie over de updates in deze release Hallo [Azure SDK 2.9 aankondiging post](https://azure.microsoft.com/blog/announcing-visual-studio-azure-tools-and-sdk-2-9/).</span><span class="sxs-lookup"><span data-stu-id="a9f2f-137">For detailed information about updates in this release, see hello [Azure SDK 2.9 announcement post](https://azure.microsoft.com/blog/announcing-visual-studio-azure-tools-and-sdk-2-9/).</span></span>

## <a name="azure-sdk-29-for-visual-studio-2015-update-2-and-visual-studio-15-preview"></a><span data-ttu-id="a9f2f-138">Azure SDK 2.9 voor Visual Studio 2015 Update 2 en Visual Studio "15" Preview</span><span class="sxs-lookup"><span data-stu-id="a9f2f-138">Azure SDK 2.9 for Visual Studio 2015 Update 2 and Visual Studio "15" Preview</span></span>
<span data-ttu-id="a9f2f-139">Deze update omvat Hallo oplossingen voor problemen te volgen:</span><span class="sxs-lookup"><span data-stu-id="a9f2f-139">This update includes hello following bug fixes:</span></span>

* <span data-ttu-id="a9f2f-140">Verwante tooREST API Client generatie uitgeven in in welke tekenreeks Hallo 'Onbekend Type' wordt weergegeven als Hallo-naam van Hallo code gen map en/of Hallo-naam van het Hallo-naamruimte neergezet in Hallo gegenereerde code.</span><span class="sxs-lookup"><span data-stu-id="a9f2f-140">Issue related tooREST API Client Generation in in which hello string "Unknown Type” would appear as hello name of hello code-gen folder and/or hello name of hello namespace dropped into hello generated code.</span></span>
* <span data-ttu-id="a9f2f-141">Verwante tooScheduled WebJobs in welke Hallo verificatiegegevens toobe toohello Scheduler-inrichtingsproces doorgegeven vertoonde uitgeven.</span><span class="sxs-lookup"><span data-stu-id="a9f2f-141">Issue related tooScheduled WebJobs in which hello authentication information was failing toobe passed toohello Scheduler provisioning process.</span></span>

<span data-ttu-id="a9f2f-142">Deze update bevat de volgende nieuwe functie Hallo:</span><span class="sxs-lookup"><span data-stu-id="a9f2f-142">This update includes hello following new feature:</span></span>

* <span data-ttu-id="a9f2f-143">Ondersteuning voor secundaire App Services Hallo 'Services' tabblad Hallo inrichting dialoogvenster App Service.</span><span class="sxs-lookup"><span data-stu-id="a9f2f-143">Support for secondary App Services in hello "Services" tab of hello App Service provisioning dialog.</span></span> 

## <a name="azure-data-lake-tools-for-visual-studio-2015-update-2"></a><span data-ttu-id="a9f2f-144">Azure Data Lake Tools voor Visual Studio 2015 Update 2</span><span class="sxs-lookup"><span data-stu-id="a9f2f-144">Azure Data Lake Tools for Visual Studio 2015 Update 2</span></span>
<span data-ttu-id="a9f2f-145">Deze update omvat Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="a9f2f-145">This updates includes hello following:</span></span>

* <span data-ttu-id="a9f2f-146">**Azure Data Lake Tools** voor Visual Studio nu samengevoegd met hello Azure SDK voor .NET versie.</span><span class="sxs-lookup"><span data-stu-id="a9f2f-146">**Azure Data Lake Tools** for Visual Studio is now merged into hello Azure SDK for .NET release.</span></span> <span data-ttu-id="a9f2f-147">Hallo-hulpprogramma wordt automatisch geïnstalleerd wanneer u Azure SDK installeert.</span><span class="sxs-lookup"><span data-stu-id="a9f2f-147">hello tool is automatically installed when you install Azure SDK.</span></span> 
  
    <span data-ttu-id="a9f2f-148">Hallo hulpprogramma vaak wordt bijgewerkt, gaat u [hier](http://aka.ms/datalaketool) tooget Hallo updates.</span><span class="sxs-lookup"><span data-stu-id="a9f2f-148">hello tool is updated frequently, go [here](http://aka.ms/datalaketool) tooget hello updates.</span></span>
* <span data-ttu-id="a9f2f-149">**Server Explorer** nu kunt u alle tooview en sommige U-SQL-metagegevens-entiteiten maken.</span><span class="sxs-lookup"><span data-stu-id="a9f2f-149">**Server Explorer** now enables you tooview all and create some U-SQL metadata entities.</span></span> <span data-ttu-id="a9f2f-150">Zie voor meer informatie [dit](https://azure.microsoft.com/documentation/services/data-lake-analytics/) blog.</span><span class="sxs-lookup"><span data-stu-id="a9f2f-150">For more information, see [this](https://azure.microsoft.com/documentation/services/data-lake-analytics/) blog.</span></span>

## <a name="hdinsight-tools"></a><span data-ttu-id="a9f2f-151">HDInsight-hulpprogramma 's</span><span class="sxs-lookup"><span data-stu-id="a9f2f-151">HDInsight Tools</span></span>
<span data-ttu-id="a9f2f-152">**HDInsight Tools** voor Visual Studio nu ondersteunt HDInsight versie 3.3, inclusief met Tez-grafieken en andere taal worden opgelost.</span><span class="sxs-lookup"><span data-stu-id="a9f2f-152">**HDInsight Tools** for Visual Studio now supports HDInsight version 3.3, including showing Tez graphs and other language fixes.</span></span>

## <a name="azure-resource-manager"></a><span data-ttu-id="a9f2f-153">Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="a9f2f-153">Azure Resource Manager</span></span>
<span data-ttu-id="a9f2f-154">Deze release voegt [KeyVault](../azure-resource-manager/resource-manager-keyvault-parameter.md) ondersteuning voor Resource Manager-sjablonen.</span><span class="sxs-lookup"><span data-stu-id="a9f2f-154">This release adds [KeyVault](../azure-resource-manager/resource-manager-keyvault-parameter.md) support for Resource Manager templates.</span></span>

## <a name="see-also"></a><span data-ttu-id="a9f2f-155">Zie ook</span><span class="sxs-lookup"><span data-stu-id="a9f2f-155">See also</span></span>
[<span data-ttu-id="a9f2f-156">Azure SDK 2.9 aankondiging post</span><span class="sxs-lookup"><span data-stu-id="a9f2f-156">Azure SDK 2.9 announcement post</span></span>](https://azure.microsoft.com/blog/announcing-visual-studio-azure-tools-and-sdk-2-9/)


---
title: Azure SDK voor .NET 2.9 Release-opmerkingen
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
ms.openlocfilehash: 199f0906f73d693d7cd4b73c928f23ae83b99596
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="azure-sdk-for-net-29-release-notes"></a><span data-ttu-id="7c8ba-103">Azure SDK voor .NET 2.9 release-opmerkingen</span><span class="sxs-lookup"><span data-stu-id="7c8ba-103">Azure SDK for .NET 2.9 release notes</span></span>

<span data-ttu-id="7c8ba-104">Dit onderwerp bevat opmerkingen bij de release voor versies 2.9 en 2.9.6 van Azure SDK voor .NET.</span><span class="sxs-lookup"><span data-stu-id="7c8ba-104">This topic includes release notes for versions 2.9 and 2.9.6 of Azure SDK for .NET.</span></span>

##<a name="azure-sdk-for-net-296-release-summary"></a><span data-ttu-id="7c8ba-105">Azure SDK voor .NET 2.9.6 release samenvatting</span><span class="sxs-lookup"><span data-stu-id="7c8ba-105">Azure SDK for .NET 2.9.6 release summary</span></span>

<span data-ttu-id="7c8ba-106">Releasedatum: 16-11-2016</span><span class="sxs-lookup"><span data-stu-id="7c8ba-106">Release date: 11/16/2016</span></span>
 
<span data-ttu-id="7c8ba-107">Geen recente wijzigingen in de Azure SDK 2.9 zijn geïntroduceerd in deze release.</span><span class="sxs-lookup"><span data-stu-id="7c8ba-107">No breaking changes to the Azure SDK 2.9 have been introduced in this release.</span></span> <span data-ttu-id="7c8ba-108">Er is geen upgradeproces nodig gebruikmaken van deze SDK met bestaande Cloud Service-projecten.</span><span class="sxs-lookup"><span data-stu-id="7c8ba-108">There is also no upgrade process needed to leverage this SDK with existing Cloud Service projects.</span></span>

### <a name="visual-studio-2017-release-candidate"></a><span data-ttu-id="7c8ba-109">Visual Studio 2017 Release Candidate</span><span class="sxs-lookup"><span data-stu-id="7c8ba-109">Visual Studio 2017 Release Candidate</span></span>

- <span data-ttu-id="7c8ba-110">Deze versie van de Azure SDK voor .NET is Visual Studio 2017 RC ingebouwd in in de Azure-werkbelasting.</span><span class="sxs-lookup"><span data-stu-id="7c8ba-110">In Visual Studio 2017 RC, this release of the Azure SDK for .NET is built in in the Azure Workload.</span></span> <span data-ttu-id="7c8ba-111">Alle hulpprogramma's die u wilt ontwikkelen van Azure zal onderdeel zijn van Visual Studio 2017 RC voortaan.</span><span class="sxs-lookup"><span data-stu-id="7c8ba-111">All the tools you need to do Azure development will be part of Visual Studio 2017 RC going forward.</span></span> <span data-ttu-id="7c8ba-112">Voor Visual Studio 2015 en Visual Studio 2013 steeds de SDK nog beschikbaar is via WebPI.</span><span class="sxs-lookup"><span data-stu-id="7c8ba-112">For Visual Studio 2015 and Visual Studio 2013, the SDK will still be available through WebPI.</span></span> <span data-ttu-id="7c8ba-113">We zullen worden beëindigde Azure SDK voor .NET-versies voor Visual Studio 2013 wanneer Visual Studio 2017 als laatste product loslaat.</span><span class="sxs-lookup"><span data-stu-id="7c8ba-113">We will be discontinuing Azure SDK for .NET releases for Visual Studio 2013, when Visual Studio 2017 releases as a final product.</span></span> <span data-ttu-id="7c8ba-114">Volg deze link om te downloaden van Visual Studio 2017 RC: https://www.visualstudio.com/vs/visual-studio-2017-rc/</span><span class="sxs-lookup"><span data-stu-id="7c8ba-114">Follow this link to download Visual Studio 2017 RC: https://www.visualstudio.com/vs/visual-studio-2017-rc/</span></span>

### <a name="azure-diagnostics"></a><span data-ttu-id="7c8ba-115">Azure Diagnostics</span><span class="sxs-lookup"><span data-stu-id="7c8ba-115">Azure Diagnostics</span></span>

- <span data-ttu-id="7c8ba-116">Het gedrag voor het opslaan van slechts een gedeeltelijke verbindingsreeks met de sleutel vervangen door een token voor de verbindingsreeks voor opslag van Cloud Services-diagnostische gegevens wordt gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="7c8ba-116">Changed the behavior to only store a partial connection string with the key replaced by a token for Cloud Services diagnostics storage connection string.</span></span> <span data-ttu-id="7c8ba-117">De werkelijke opslagsleutel worden nu opgeslagen in de map van het gebruikersprofiel en kan dus de toegang kan worden beheerd.</span><span class="sxs-lookup"><span data-stu-id="7c8ba-117">The actual storage key is now stored in the user profile folder so its access can be controlled.</span></span> <span data-ttu-id="7c8ba-118">Visual Studio, leest van de opslagsleutel van gebruikersprofielmap voor lokale foutopsporing en publicatieproces.</span><span class="sxs-lookup"><span data-stu-id="7c8ba-118">Visual Studio will read the storage key from user profile folder for local debugging and publishing process.</span></span> 
- <span data-ttu-id="7c8ba-119">Visual Studio Online-team verbeterd in reactie op de wijziging die hierboven worden beschreven, de Azure Cloud Services-implementatiesjabloon taak zodat gebruikers de opslagsleutel voor het instellen van de extensie voor diagnostische gegevens bij het publiceren naar Azure in continue integratie en implementatie kunnen opgeven.</span><span class="sxs-lookup"><span data-stu-id="7c8ba-119">In response to the change described above, Visual Studio Online team enhanced the Azure Cloud Services deployment task template so users could specify the storage key for setting diagnostics extension when publishing to Azure in Continuous Integration and Deployment.</span></span>
- <span data-ttu-id="7c8ba-120">We hebben aangebracht voor het opslaan van beveiligde verbindingsreeks en tokeniseren voor Azure Diagnostics (af), om u te helpen bij het oplossen van problemen met configuratie over environements mogelijk.</span><span class="sxs-lookup"><span data-stu-id="7c8ba-120">We’ve made it possible to store secure connection string and tokenization for Azure Diagnostics (WAD), to help you solve problems with configuration across environements.</span></span>
 
### <a name="windows-server-2016-virtual-machines"></a><span data-ttu-id="7c8ba-121">Windows Server 2016 virtuele machines</span><span class="sxs-lookup"><span data-stu-id="7c8ba-121">Windows Server 2016 virtual machines</span></span>

- <span data-ttu-id="7c8ba-122">Visual Studio biedt nu ondersteuning voor het implementeren van Cloud-Services op OS-familie 5 (Windows Server 2016) virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="7c8ba-122">Visual Studio now supports deploying Cloud Services to OS Family 5 (Windows Server 2016) virtual machines.</span></span> <span data-ttu-id="7c8ba-123">Voor bestaande cloudservices, kunt u uw instellingen voor het doel van de nieuwe OS-familie.</span><span class="sxs-lookup"><span data-stu-id="7c8ba-123">For existing cloud services, you can change your settings to target the new OS Family.</span></span> <span data-ttu-id="7c8ba-124">Bij het maken van nieuwe cloudservices als u wilt maken van de service met .net 4.6 of hoger, wordt standaard de service voor het gebruik van de OS-familie 5.</span><span class="sxs-lookup"><span data-stu-id="7c8ba-124">When creating new cloud services, if you choose to create the service using .net 4.6 or higher, it will default the service to use OS Family 5.</span></span>  <span data-ttu-id="7c8ba-125">Raadpleeg voor meer informatie de [Gastbesturingssysteemgroep ondersteunen tabel](https://azure.microsoft.com/en-us/documentation/articles/cloud-services-guestos-update-matrix/).</span><span class="sxs-lookup"><span data-stu-id="7c8ba-125">For more information, you can review the [Guest OS Family support table](https://azure.microsoft.com/en-us/documentation/articles/cloud-services-guestos-update-matrix/).</span></span>

#### <a name="known-issues"></a><span data-ttu-id="7c8ba-126">Bekende problemen</span><span class="sxs-lookup"><span data-stu-id="7c8ba-126">Known issues</span></span>

- <span data-ttu-id="7c8ba-127">Azure .NET SDK 2.9.6 geïntroduceerd een beperking die implementatie van de projecten met behulp van niet-ondersteunde .NET frameworks (zoals .NET 4.6) naar een OS-familie blokkeert < 5.</span><span class="sxs-lookup"><span data-stu-id="7c8ba-127">Azure .NET SDK 2.9.6 introduced a restriction that blocks deployment of projects using unsupported .NET frameworks (such as .NET 4.6) to any OS Family < 5.</span></span> <span data-ttu-id="7c8ba-128">Een tijdelijke oplossing wordt aangeboden [hier](https://github.com/MicrosoftDocs/azure-cloud-services-files/tree/master/Azure%20Targets%20SDK%202.9).</span><span class="sxs-lookup"><span data-stu-id="7c8ba-128">A workaround is provided [here](https://github.com/MicrosoftDocs/azure-cloud-services-files/tree/master/Azure%20Targets%20SDK%202.9).</span></span>

 
### <a name="azure-in-role-cache"></a><span data-ttu-id="7c8ba-129">Azure In-Role Cache</span><span class="sxs-lookup"><span data-stu-id="7c8ba-129">Azure In-Role Cache</span></span> 

- <span data-ttu-id="7c8ba-130">Ondersteuning voor Azure In-Role Cache eindigt op 30 November 2016.</span><span class="sxs-lookup"><span data-stu-id="7c8ba-130">Support for Azure In-Role Cache ends on November 30, 2016.</span></span> <span data-ttu-id="7c8ba-131">Klik voor meer informatie [hier](https://azure.microsoft.com/en-us/blog/azure-managed-cache-and-in-role-cache-services-to-be-retired-on-11-30-2016/).</span><span class="sxs-lookup"><span data-stu-id="7c8ba-131">For more details, click [here](https://azure.microsoft.com/en-us/blog/azure-managed-cache-and-in-role-cache-services-to-be-retired-on-11-30-2016/).</span></span>

### <a name="azure-resource-manager-templates-for-azure-stack"></a><span data-ttu-id="7c8ba-132">Azure Resource Manager-sjablonen voor Azure Stack</span><span class="sxs-lookup"><span data-stu-id="7c8ba-132">Azure Resource Manager Templates for Azure Stack</span></span>

- <span data-ttu-id="7c8ba-133">Hebben wij de Stack Azure als het implementatiedoel van een voor uw Azure Resource Manager-sjablonen.</span><span class="sxs-lookup"><span data-stu-id="7c8ba-133">We’ve introduced Azure Stack as a deployment target for your Azure Resource Manager Templates.</span></span>


## <a name="azure-sdk-for-net-29-summary"></a><span data-ttu-id="7c8ba-134">Azure SDK voor .NET 2.9 samenvatting</span><span class="sxs-lookup"><span data-stu-id="7c8ba-134">Azure SDK for .NET 2.9 summary</span></span>

## <a name="overview"></a><span data-ttu-id="7c8ba-135">Overzicht</span><span class="sxs-lookup"><span data-stu-id="7c8ba-135">Overview</span></span>
<span data-ttu-id="7c8ba-136">Dit document bevat de releaseopmerkingen voor de Azure SDK voor .NET 2.9 release.</span><span class="sxs-lookup"><span data-stu-id="7c8ba-136">This document contains the release notes for the Azure SDK for .NET 2.9 release.</span></span> 

<span data-ttu-id="7c8ba-137">Zie voor gedetailleerde informatie over de updates in deze release de [Azure SDK 2.9 aankondiging post](https://azure.microsoft.com/blog/announcing-visual-studio-azure-tools-and-sdk-2-9/).</span><span class="sxs-lookup"><span data-stu-id="7c8ba-137">For detailed information about updates in this release, see the [Azure SDK 2.9 announcement post](https://azure.microsoft.com/blog/announcing-visual-studio-azure-tools-and-sdk-2-9/).</span></span>

## <a name="azure-sdk-29-for-visual-studio-2015-update-2-and-visual-studio-15-preview"></a><span data-ttu-id="7c8ba-138">Azure SDK 2.9 voor Visual Studio 2015 Update 2 en Visual Studio "15" Preview</span><span class="sxs-lookup"><span data-stu-id="7c8ba-138">Azure SDK 2.9 for Visual Studio 2015 Update 2 and Visual Studio "15" Preview</span></span>
<span data-ttu-id="7c8ba-139">Deze update bevat de volgende oplossingen voor problemen:</span><span class="sxs-lookup"><span data-stu-id="7c8ba-139">This update includes the following bug fixes:</span></span>

* <span data-ttu-id="7c8ba-140">Probleem dat is gerelateerd aan de REST-API-Client generatie in waarin de tekenreeks 'Onbekend Type' wordt weergegeven als de naam van de map code gen en/of de naam van de naamruimte neergezet in de gegenereerde code.</span><span class="sxs-lookup"><span data-stu-id="7c8ba-140">Issue related to REST API Client Generation in in which the string "Unknown Type” would appear as the name of the code-gen folder and/or the name of the namespace dropped into the generated code.</span></span>
* <span data-ttu-id="7c8ba-141">Het probleem is gerelateerd aan geplande webtaken waarin de verificatiegegevens konden niet worden doorgegeven aan de planner inrichtingsproces.</span><span class="sxs-lookup"><span data-stu-id="7c8ba-141">Issue related to Scheduled WebJobs in which the authentication information was failing to be passed to the Scheduler provisioning process.</span></span>

<span data-ttu-id="7c8ba-142">Deze update bevat de volgende nieuwe functie:</span><span class="sxs-lookup"><span data-stu-id="7c8ba-142">This update includes the following new feature:</span></span>

* <span data-ttu-id="7c8ba-143">Ondersteuning voor secundaire App-Services op het tabblad 'Services' van het dialoogvenster voor het inrichten van App Service.</span><span class="sxs-lookup"><span data-stu-id="7c8ba-143">Support for secondary App Services in the "Services" tab of the App Service provisioning dialog.</span></span> 

## <a name="azure-data-lake-tools-for-visual-studio-2015-update-2"></a><span data-ttu-id="7c8ba-144">Azure Data Lake Tools voor Visual Studio 2015 Update 2</span><span class="sxs-lookup"><span data-stu-id="7c8ba-144">Azure Data Lake Tools for Visual Studio 2015 Update 2</span></span>
<span data-ttu-id="7c8ba-145">Deze update omvat het volgende:</span><span class="sxs-lookup"><span data-stu-id="7c8ba-145">This updates includes the following:</span></span>

* <span data-ttu-id="7c8ba-146">**Azure Data Lake Tools** voor Visual Studio nu samengevoegd met de Azure SDK voor .NET versie.</span><span class="sxs-lookup"><span data-stu-id="7c8ba-146">**Azure Data Lake Tools** for Visual Studio is now merged into the Azure SDK for .NET release.</span></span> <span data-ttu-id="7c8ba-147">Het hulpprogramma wordt automatisch geïnstalleerd wanneer u Azure SDK installeert.</span><span class="sxs-lookup"><span data-stu-id="7c8ba-147">The tool is automatically installed when you install Azure SDK.</span></span> 
  
    <span data-ttu-id="7c8ba-148">Het hulpprogramma vaak wordt bijgewerkt, gaat u [hier](http://aka.ms/datalaketool) om de updates te downloaden.</span><span class="sxs-lookup"><span data-stu-id="7c8ba-148">The tool is updated frequently, go [here](http://aka.ms/datalaketool) to get the updates.</span></span>
* <span data-ttu-id="7c8ba-149">**Server Explorer** nu kunt u alle weergeven en sommige U-SQL-metagegevens-entiteiten maken.</span><span class="sxs-lookup"><span data-stu-id="7c8ba-149">**Server Explorer** now enables you to view all and create some U-SQL metadata entities.</span></span> <span data-ttu-id="7c8ba-150">Zie voor meer informatie [dit](https://azure.microsoft.com/documentation/services/data-lake-analytics/) blog.</span><span class="sxs-lookup"><span data-stu-id="7c8ba-150">For more information, see [this](https://azure.microsoft.com/documentation/services/data-lake-analytics/) blog.</span></span>

## <a name="hdinsight-tools"></a><span data-ttu-id="7c8ba-151">HDInsight-hulpprogramma 's</span><span class="sxs-lookup"><span data-stu-id="7c8ba-151">HDInsight Tools</span></span>
<span data-ttu-id="7c8ba-152">**HDInsight Tools** voor Visual Studio nu ondersteunt HDInsight versie 3.3, inclusief met Tez-grafieken en andere taal worden opgelost.</span><span class="sxs-lookup"><span data-stu-id="7c8ba-152">**HDInsight Tools** for Visual Studio now supports HDInsight version 3.3, including showing Tez graphs and other language fixes.</span></span>

## <a name="azure-resource-manager"></a><span data-ttu-id="7c8ba-153">Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="7c8ba-153">Azure Resource Manager</span></span>
<span data-ttu-id="7c8ba-154">Deze release voegt [KeyVault](../azure-resource-manager/resource-manager-keyvault-parameter.md) ondersteuning voor Resource Manager-sjablonen.</span><span class="sxs-lookup"><span data-stu-id="7c8ba-154">This release adds [KeyVault](../azure-resource-manager/resource-manager-keyvault-parameter.md) support for Resource Manager templates.</span></span>

## <a name="see-also"></a><span data-ttu-id="7c8ba-155">Zie ook</span><span class="sxs-lookup"><span data-stu-id="7c8ba-155">See also</span></span>
[<span data-ttu-id="7c8ba-156">Azure SDK 2.9 aankondiging post</span><span class="sxs-lookup"><span data-stu-id="7c8ba-156">Azure SDK 2.9 announcement post</span></span>](https://azure.microsoft.com/blog/announcing-visual-studio-azure-tools-and-sdk-2-9/)


---
title: Azure SDK voor .NET 3.0 Release-opmerkingen | Microsoft Docs
description: Azure SDK voor .NET 3.0 Release-opmerkingen
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
ms.date: 03/07/2017
ms.author: juliako
ms.openlocfilehash: eea4e569ac2d0192ed7872d2fcb9bed03614832b
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="azure-sdk-for-net-30-release-notes"></a><span data-ttu-id="926cb-103">Azure SDK voor .NET 3.0 release-opmerkingen</span><span class="sxs-lookup"><span data-stu-id="926cb-103">Azure SDK for .NET 3.0 release notes</span></span>

<span data-ttu-id="926cb-104">Dit onderwerp bevat de releaseopmerkingen voor versie 3.0 van de Azure SDK voor .NET.</span><span class="sxs-lookup"><span data-stu-id="926cb-104">This topic includes release notes for version 3.0 of the Azure SDK for .NET.</span></span>

##<a name="azure-sdk-for-net-30-release-summary"></a><span data-ttu-id="926cb-105">Azure SDK voor .NET 3.0 release samenvatting</span><span class="sxs-lookup"><span data-stu-id="926cb-105">Azure SDK for .NET 3.0 release summary</span></span>

<span data-ttu-id="926cb-106">Releasedatum: 07-03/2017</span><span class="sxs-lookup"><span data-stu-id="926cb-106">Release date: 03/07/2017</span></span>
 
<span data-ttu-id="926cb-107">Geen recente wijzigingen in de Azure SDK 3.0 zijn geïntroduceerd in deze release.</span><span class="sxs-lookup"><span data-stu-id="926cb-107">No breaking changes to the Azure SDK 3.0 have been introduced in this release.</span></span> <span data-ttu-id="926cb-108">Er is geen upgradeproces nodig gebruikmaken van deze SDK met bestaande Cloud Service-projecten.</span><span class="sxs-lookup"><span data-stu-id="926cb-108">There is also no upgrade process needed to leverage this SDK with existing Cloud Service projects.</span></span> <span data-ttu-id="926cb-109">Als u gebruik van de Azure SDK 3.0 zonder een upgradeproces, installeert Azure SDK 3.0 in dezelfde directory als de Azure SDK 2.9.</span><span class="sxs-lookup"><span data-stu-id="926cb-109">To allow use of the Azure SDK 3.0 without requiring an upgrade process, Azure SDK 3.0 installs to the same directories as Azure SDK 2.9.</span></span> <span data-ttu-id="926cb-110">Meest voor de onderdelen is niet veranderd met de primaire versie van 2.9 maar in plaats daarvan het build-nummer zojuist hebt bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="926cb-110">Most the components did not change the major version from 2.9 but instead just updated the build number.</span></span>

## <a name="visual-studio-2017-rtw"></a><span data-ttu-id="926cb-111">Visual Studio 2017 RTW</span><span class="sxs-lookup"><span data-stu-id="926cb-111">Visual Studio 2017 RTW</span></span>

- <span data-ttu-id="926cb-112">In Visual Studio-2017 is deze versie van de Azure SDK voor .NET ingebouwd in de Azure-werkbelasting.</span><span class="sxs-lookup"><span data-stu-id="926cb-112">In Visual Studio 2017, this release of the Azure SDK for .NET is built in to the Azure Workload.</span></span> <span data-ttu-id="926cb-113">Alle hulpprogramma's die u wilt ontwikkelen van Azure zal onderdeel zijn van Visual Studio 2017 voortaan.</span><span class="sxs-lookup"><span data-stu-id="926cb-113">All the tools you need to do Azure development will be part of Visual Studio 2017 going forward.</span></span> <span data-ttu-id="926cb-114">Voor Visual Studio 2015 steeds de SDK nog beschikbaar is via WebPI.</span><span class="sxs-lookup"><span data-stu-id="926cb-114">For Visual Studio 2015 the SDK will still be available through WebPI.</span></span> <span data-ttu-id="926cb-115">We hebben Azure SDK voor .NET-versies voor Visual Studio 2013 stopgezet nu dat Visual Studio 2017 is vrijgegeven.</span><span class="sxs-lookup"><span data-stu-id="926cb-115">We have discontinued Azure SDK for .NET releases for Visual Studio 2013 now that Visual Studio 2017 has been released.</span></span>

### <a name="azure-diagnostics"></a><span data-ttu-id="926cb-116">Azure Diagnostics</span><span class="sxs-lookup"><span data-stu-id="926cb-116">Azure Diagnostics</span></span>

- <span data-ttu-id="926cb-117">Het gedrag voor het opslaan van slechts een gedeeltelijke verbindingsreeks met de sleutel vervangen door een token voor de verbindingsreeks voor opslag van Cloud Services-diagnostische gegevens wordt gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="926cb-117">Changed the behavior to only store a partial connection string with the key replaced by a token for Cloud Services diagnostics storage connection string.</span></span> <span data-ttu-id="926cb-118">De werkelijke opslagsleutel worden nu opgeslagen in de map van het gebruikersprofiel en kan dus de toegang kan worden beheerd.</span><span class="sxs-lookup"><span data-stu-id="926cb-118">The actual storage key is now stored in the user profile folder so its access can be controlled.</span></span> <span data-ttu-id="926cb-119">Visual Studio, leest van de opslagsleutel van gebruikersprofielmap voor lokale foutopsporing en publicatieproces.</span><span class="sxs-lookup"><span data-stu-id="926cb-119">Visual Studio will read the storage key from user profile folder for local debugging and publishing process.</span></span> 
- <span data-ttu-id="926cb-120">Visual Studio Online-team verbeterd in reactie op de wijziging die hierboven worden beschreven, de Azure Cloud Services-implementatiesjabloon taak zodat gebruikers de opslagsleutel voor het instellen van de extensie voor diagnostische gegevens bij het publiceren naar Azure in continue integratie en implementatie kunnen opgeven.</span><span class="sxs-lookup"><span data-stu-id="926cb-120">In response to the change described above, Visual Studio Online team enhanced the Azure Cloud Services deployment task template so users could specify the storage key for setting diagnostics extension when publishing to Azure in Continuous Integration and Deployment.</span></span>
- <span data-ttu-id="926cb-121">We hebben aangebracht voor het opslaan van beveiligde verbindingsreeks en tokeniseren voor Azure Diagnostics (af), om u te helpen bij het oplossen van problemen met configuratie over environements mogelijk.</span><span class="sxs-lookup"><span data-stu-id="926cb-121">We’ve made it possible to store secure connection string and tokenization for Azure Diagnostics (WAD), to help you solve problems with configuration across environements.</span></span>
 
### <a name="windows-server-2016-virtual-machines"></a><span data-ttu-id="926cb-122">Windows Server 2016 virtuele machines</span><span class="sxs-lookup"><span data-stu-id="926cb-122">Windows Server 2016 virtual machines</span></span>

- <span data-ttu-id="926cb-123">Visual Studio biedt nu ondersteuning voor het implementeren van Cloud-Services op OS-familie 5 (Windows Server 2016) virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="926cb-123">Visual Studio now supports deploying Cloud Services to OS Family 5 (Windows Server 2016) virtual machines.</span></span> <span data-ttu-id="926cb-124">Voor bestaande cloudservices, kunt u uw instellingen voor het doel van de nieuwe OS-familie.</span><span class="sxs-lookup"><span data-stu-id="926cb-124">For existing cloud services, you can change your settings to target the new OS Family.</span></span> <span data-ttu-id="926cb-125">Bij het maken van nieuwe cloudservices als u wilt maken van de service met .net 4.6 of hoger, wordt standaard de service voor het gebruik van de OS-familie 5.</span><span class="sxs-lookup"><span data-stu-id="926cb-125">When creating new cloud services, if you choose to create the service using .net 4.6 or higher, it will default the service to use OS Family 5.</span></span>  <span data-ttu-id="926cb-126">Raadpleeg voor meer informatie de [Gastbesturingssysteemgroep ondersteunen tabel](../cloud-services/cloud-services-guestos-update-matrix.md).</span><span class="sxs-lookup"><span data-stu-id="926cb-126">For more information, you can review the [Guest OS Family support table](../cloud-services/cloud-services-guestos-update-matrix.md).</span></span>

### <a name="known-issues"></a><span data-ttu-id="926cb-127">Bekende problemen</span><span class="sxs-lookup"><span data-stu-id="926cb-127">Known issues</span></span>

- <span data-ttu-id="926cb-128">Azure .NET SDK 3.0 geïntroduceerd om een probleem bij het verwijderen van Visual Studio 2017 in de configuratie van een gelijktijdige met Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="926cb-128">Azure .NET SDK 3.0 introduced an issue when removing Visual Studio 2017 in a side by side configuration with Visual Studio 2015.</span></span>  <span data-ttu-id="926cb-129">Als u de Azure SDK voor Visual Studio 2015 geïnstalleerd hebt, worden de Microsoft Azure-Opslagemulator en Microsoft Azure Compute-Emulator verwijderd als u Visual Studio 2017 verwijdert.</span><span class="sxs-lookup"><span data-stu-id="926cb-129">If you have the Azure SDK installed for Visual Studio 2015, the Microsoft Azure Storage Emulator and Microsoft Azure Compute Emulator will be removed if you uninstall Visual Studio 2017.</span></span>  <span data-ttu-id="926cb-130">Het resultaat is een fout bij het maken en foutopsporing van nieuwe Cloud services-projecten in Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="926cb-130">This will produce an error when creating and debugging new Cloud services projects in Visual Studio 2015.</span></span> <span data-ttu-id="926cb-131">Om dit probleem oplossen, installeer de Azure-SDK van de Web Platform Installer.</span><span class="sxs-lookup"><span data-stu-id="926cb-131">In order to fix this issue,  reinstall the Azure SDK from the Web Platform Installer.</span></span>  <span data-ttu-id="926cb-132">Het probleem worden opgelost in een toekomstige update voor Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="926cb-132">The issue will be resolved in a future Visual Studio 2017 update.</span></span>  <span data-ttu-id="926cb-133">.</span><span class="sxs-lookup"><span data-stu-id="926cb-133">.</span></span>

 
### <a name="azure-in-role-cache"></a><span data-ttu-id="926cb-134">Azure In-Role Cache</span><span class="sxs-lookup"><span data-stu-id="926cb-134">Azure In-Role Cache</span></span> 

- <span data-ttu-id="926cb-135">Ondersteuning voor Azure In-Role Cache is gestopt op 30 November 2016.</span><span class="sxs-lookup"><span data-stu-id="926cb-135">Support for Azure In-Role Cache ended on November 30, 2016.</span></span> <span data-ttu-id="926cb-136">Klik voor meer informatie [hier](https://azure.microsoft.com/blog/azure-managed-cache-and-in-role-cache-services-to-be-retired-on-11-30-2016/).</span><span class="sxs-lookup"><span data-stu-id="926cb-136">For more details, click [here](https://azure.microsoft.com/blog/azure-managed-cache-and-in-role-cache-services-to-be-retired-on-11-30-2016/).</span></span>





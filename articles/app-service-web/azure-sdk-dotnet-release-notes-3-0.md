---
title: aaaAzure SDK voor .NET 3.0 Release-opmerkingen | Microsoft Docs
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
ms.openlocfilehash: 8970b4c9b64de40dc29a33d69006a00ae5e38a50
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sdk-for-net-30-release-notes"></a><span data-ttu-id="cb29e-103">Azure SDK voor .NET 3.0 release-opmerkingen</span><span class="sxs-lookup"><span data-stu-id="cb29e-103">Azure SDK for .NET 3.0 release notes</span></span>

<span data-ttu-id="cb29e-104">Dit onderwerp bevat de releaseopmerkingen voor versie 3.0 van hello Azure SDK voor .NET.</span><span class="sxs-lookup"><span data-stu-id="cb29e-104">This topic includes release notes for version 3.0 of hello Azure SDK for .NET.</span></span>

##<a name="azure-sdk-for-net-30-release-summary"></a><span data-ttu-id="cb29e-105">Azure SDK voor .NET 3.0 release samenvatting</span><span class="sxs-lookup"><span data-stu-id="cb29e-105">Azure SDK for .NET 3.0 release summary</span></span>

<span data-ttu-id="cb29e-106">Releasedatum: 07-03/2017</span><span class="sxs-lookup"><span data-stu-id="cb29e-106">Release date: 03/07/2017</span></span>
 
<span data-ttu-id="cb29e-107">Er zijn geen recente wijzigingen toohello Azure SDK 3.0 zijn geïntroduceerd in deze release.</span><span class="sxs-lookup"><span data-stu-id="cb29e-107">No breaking changes toohello Azure SDK 3.0 have been introduced in this release.</span></span> <span data-ttu-id="cb29e-108">Er is ook geen tooleverage upgradeproces nodig deze SDK met bestaande Cloud Service-projecten.</span><span class="sxs-lookup"><span data-stu-id="cb29e-108">There is also no upgrade process needed tooleverage this SDK with existing Cloud Service projects.</span></span> <span data-ttu-id="cb29e-109">tooallow gebruik van Azure SDK 3.0 Hallo zonder een upgradeproces Azure SDK 3.0 installeert toohello dezelfde directory als de Azure SDK 2.9.</span><span class="sxs-lookup"><span data-stu-id="cb29e-109">tooallow use of hello Azure SDK 3.0 without requiring an upgrade process, Azure SDK 3.0 installs toohello same directories as Azure SDK 2.9.</span></span> <span data-ttu-id="cb29e-110">De meeste Hallo-onderdelen is niet veranderd met Hallo hoofdversie van 2.9 maar Hallo build-nummer in plaats daarvan zojuist hebt bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="cb29e-110">Most hello components did not change hello major version from 2.9 but instead just updated hello build number.</span></span>

## <a name="visual-studio-2017-rtw"></a><span data-ttu-id="cb29e-111">Visual Studio 2017 RTW</span><span class="sxs-lookup"><span data-stu-id="cb29e-111">Visual Studio 2017 RTW</span></span>

- <span data-ttu-id="cb29e-112">In Visual Studio-2017 is deze release van hello Azure SDK voor .NET ingebouwd in toohello Azure werkbelasting.</span><span class="sxs-lookup"><span data-stu-id="cb29e-112">In Visual Studio 2017, this release of hello Azure SDK for .NET is built in toohello Azure Workload.</span></span> <span data-ttu-id="cb29e-113">Alle Hallo-hulpprogramma's, moet u toodo ontwikkelen van Azure zal onderdeel zijn van Visual Studio 2017 voortaan.</span><span class="sxs-lookup"><span data-stu-id="cb29e-113">All hello tools you need toodo Azure development will be part of Visual Studio 2017 going forward.</span></span> <span data-ttu-id="cb29e-114">Voor Visual Studio 2015 steeds Hallo SDK nog beschikbaar is via WebPI.</span><span class="sxs-lookup"><span data-stu-id="cb29e-114">For Visual Studio 2015 hello SDK will still be available through WebPI.</span></span> <span data-ttu-id="cb29e-115">We hebben Azure SDK voor .NET-versies voor Visual Studio 2013 stopgezet nu dat Visual Studio 2017 is vrijgegeven.</span><span class="sxs-lookup"><span data-stu-id="cb29e-115">We have discontinued Azure SDK for .NET releases for Visual Studio 2013 now that Visual Studio 2017 has been released.</span></span>

### <a name="azure-diagnostics"></a><span data-ttu-id="cb29e-116">Azure Diagnostics</span><span class="sxs-lookup"><span data-stu-id="cb29e-116">Azure Diagnostics</span></span>

- <span data-ttu-id="cb29e-117">Een gedeeltelijke verbindingsreeks gewijzigde Hallo gedrag tooonly opslaan met Hallo sleutel vervangen door een token voor de verbindingsreeks voor opslag van Cloud Services-diagnostische gegevens.</span><span class="sxs-lookup"><span data-stu-id="cb29e-117">Changed hello behavior tooonly store a partial connection string with hello key replaced by a token for Cloud Services diagnostics storage connection string.</span></span> <span data-ttu-id="cb29e-118">de werkelijke opslagsleutel Hallo worden nu opgeslagen in de map gebruikersprofiel Hallo zodat de toegang kan worden beheerd.</span><span class="sxs-lookup"><span data-stu-id="cb29e-118">hello actual storage key is now stored in hello user profile folder so its access can be controlled.</span></span> <span data-ttu-id="cb29e-119">Visual Studio wordt Hallo-opslagsleutel lezen uit de map voor lokale foutopsporing en publicatieproces gebruikersprofiel.</span><span class="sxs-lookup"><span data-stu-id="cb29e-119">Visual Studio will read hello storage key from user profile folder for local debugging and publishing process.</span></span> 
- <span data-ttu-id="cb29e-120">In het antwoord toohello wijziging die hierboven worden beschreven, team Visual Studio Online verbeterde hello Azure Cloud Services-implementatiesjabloon taak zodat gebruikers Hallo-opslagsleutel voor het instellen van de extensie voor diagnostische gegevens bij het publiceren van tooAzure in continue integratie kunnen opgeven en implementatie.</span><span class="sxs-lookup"><span data-stu-id="cb29e-120">In response toohello change described above, Visual Studio Online team enhanced hello Azure Cloud Services deployment task template so users could specify hello storage key for setting diagnostics extension when publishing tooAzure in Continuous Integration and Deployment.</span></span>
- <span data-ttu-id="cb29e-121">We hebben het mogelijke toostore beveiligde verbindingsreeks en tokeniseren voor Azure Diagnostics (af), het oplossen van problemen met configuratie over environements toohelp aangebracht.</span><span class="sxs-lookup"><span data-stu-id="cb29e-121">We’ve made it possible toostore secure connection string and tokenization for Azure Diagnostics (WAD), toohelp you solve problems with configuration across environements.</span></span>
 
### <a name="windows-server-2016-virtual-machines"></a><span data-ttu-id="cb29e-122">Windows Server 2016 virtuele machines</span><span class="sxs-lookup"><span data-stu-id="cb29e-122">Windows Server 2016 virtual machines</span></span>

- <span data-ttu-id="cb29e-123">Visual Studio ondersteunt nu implementeren Cloudservices tooOS familie 5 (Windows Server 2016) virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="cb29e-123">Visual Studio now supports deploying Cloud Services tooOS Family 5 (Windows Server 2016) virtual machines.</span></span> <span data-ttu-id="cb29e-124">Voor bestaande cloudservices, kunt u uw instellingen tootarget Hallo van nieuwe OS-familie.</span><span class="sxs-lookup"><span data-stu-id="cb29e-124">For existing cloud services, you can change your settings tootarget hello new OS Family.</span></span> <span data-ttu-id="cb29e-125">Bij het maken van nieuwe cloudservices als u ervoor kiest toocreate Hallo service met .net 4.6 of hoger, wordt standaard Hallo service toouse OS-familie 5.</span><span class="sxs-lookup"><span data-stu-id="cb29e-125">When creating new cloud services, if you choose toocreate hello service using .net 4.6 or higher, it will default hello service toouse OS Family 5.</span></span>  <span data-ttu-id="cb29e-126">Voor meer informatie kunt u bekijken Hallo [Gastbesturingssysteemgroep ondersteunen tabel](../cloud-services/cloud-services-guestos-update-matrix.md).</span><span class="sxs-lookup"><span data-stu-id="cb29e-126">For more information, you can review hello [Guest OS Family support table](../cloud-services/cloud-services-guestos-update-matrix.md).</span></span>

### <a name="known-issues"></a><span data-ttu-id="cb29e-127">Bekende problemen</span><span class="sxs-lookup"><span data-stu-id="cb29e-127">Known issues</span></span>

- <span data-ttu-id="cb29e-128">Azure .NET SDK 3.0 geïntroduceerd om een probleem bij het verwijderen van Visual Studio 2017 in de configuratie van een gelijktijdige met Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="cb29e-128">Azure .NET SDK 3.0 introduced an issue when removing Visual Studio 2017 in a side by side configuration with Visual Studio 2015.</span></span>  <span data-ttu-id="cb29e-129">Als u hello Azure SDK voor Visual Studio 2015 geïnstalleerd hebt, wordt Hallo Microsoft Azure-Opslagemulator en Microsoft Azure Compute-Emulator verwijderd als u Visual Studio 2017 verwijdert.</span><span class="sxs-lookup"><span data-stu-id="cb29e-129">If you have hello Azure SDK installed for Visual Studio 2015, hello Microsoft Azure Storage Emulator and Microsoft Azure Compute Emulator will be removed if you uninstall Visual Studio 2017.</span></span>  <span data-ttu-id="cb29e-130">Het resultaat is een fout bij het maken en foutopsporing van nieuwe Cloud services-projecten in Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="cb29e-130">This will produce an error when creating and debugging new Cloud services projects in Visual Studio 2015.</span></span> <span data-ttu-id="cb29e-131">In de order toofix dit probleem, hello Azure SDK uit Hallo Web Platform Installer te installeren.</span><span class="sxs-lookup"><span data-stu-id="cb29e-131">In order toofix this issue,  reinstall hello Azure SDK from hello Web Platform Installer.</span></span>  <span data-ttu-id="cb29e-132">Hallo probleem worden opgelost in een toekomstige update voor Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="cb29e-132">hello issue will be resolved in a future Visual Studio 2017 update.</span></span>  <span data-ttu-id="cb29e-133">.</span><span class="sxs-lookup"><span data-stu-id="cb29e-133">.</span></span>

 
### <a name="azure-in-role-cache"></a><span data-ttu-id="cb29e-134">Azure In-Role Cache</span><span class="sxs-lookup"><span data-stu-id="cb29e-134">Azure In-Role Cache</span></span> 

- <span data-ttu-id="cb29e-135">Ondersteuning voor Azure In-Role Cache is gestopt op 30 November 2016.</span><span class="sxs-lookup"><span data-stu-id="cb29e-135">Support for Azure In-Role Cache ended on November 30, 2016.</span></span> <span data-ttu-id="cb29e-136">Klik voor meer informatie [hier](https://azure.microsoft.com/blog/azure-managed-cache-and-in-role-cache-services-to-be-retired-on-11-30-2016/).</span><span class="sxs-lookup"><span data-stu-id="cb29e-136">For more details, click [here](https://azure.microsoft.com/blog/azure-managed-cache-and-in-role-cache-services-to-be-retired-on-11-30-2016/).</span></span>





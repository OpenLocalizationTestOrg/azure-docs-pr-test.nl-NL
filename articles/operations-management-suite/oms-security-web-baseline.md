---
title: aaaOperations Management Suite beveiligings- en Audit oplossing Web basislijn | Microsoft Docs
description: Dit document wordt uitgelegd hoe toouse OMS beveiligings- en Audit oplossing tooperform een beoordeling van de basislijn web van alle bewaakte webservers voor naleving en beveiliging doel.
services: operations-management-suite
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ROBOTS: NOINDEX
redirect_url: https://www.microsoft.com/cloud-platform/security-and-compliance
ms.assetid: 17837c8b-3e79-47c0-9b83-a51c6ca44ca6
ms.service: operations-management-suite
ms.custom: oms-security
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/27/2017
ms.author: yurid
ms.openlocfilehash: 8aa87fa404ff97ab549dda3f9bebb75766055963
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="web-baseline-assessment-in-operations-management-suite-security-and-audit-solution"></a><span data-ttu-id="f4558-103">Evaluatie van de webbasislijn in de oplossing voor beveiliging en controle voor Operations Management Suite</span><span class="sxs-lookup"><span data-stu-id="f4558-103">Web Baseline Assessment in Operations Management Suite Security and Audit Solution</span></span>
<span data-ttu-id="f4558-104">Dit document helpt u toouse [Operations Management Suite (OMS) beveiligings- en Audit oplossing](operations-management-suite-overview.md) web-basislijn assessment mogelijkheden tooaccess Hallo beveiligingsstatus van uw bewaakte resources.</span><span class="sxs-lookup"><span data-stu-id="f4558-104">This document helps you toouse [Operations Management Suite (OMS) Security and Audit Solution](operations-management-suite-overview.md) web baseline assessment capabilities tooaccess hello secure state of your monitored resources.</span></span>

## <a name="what-is-web-baseline-assessment"></a><span data-ttu-id="f4558-105">Wat is evaluatie van de webbasislijn?</span><span class="sxs-lookup"><span data-stu-id="f4558-105">What is Web Baseline Assessment?</span></span>
<span data-ttu-id="f4558-106">Beveiliging voor OMS biedt momenteel evaluatie van de beveiligingsbasislijn voor besturingssystemen.</span><span class="sxs-lookup"><span data-stu-id="f4558-106">Currently OMS Security provides security baseline assessment for operating systems.</span></span> <span data-ttu-id="f4558-107">Wordt gescand Hallo besturingssysteeminstellingen van uw servers om de 24 uur en biedt een weergave in het potentieel kwetsbaar instellingen.</span><span class="sxs-lookup"><span data-stu-id="f4558-107">It scans hello operating system settings of your servers every 24 hours and provides a view into potentially vulnerable settings.</span></span> <span data-ttu-id="f4558-108">Lees [Basislijnevaluatie in de oplossing voor beveiliging en controle voor Operations Management Suite](oms-security-baseline.md) voor meer informatie hierover.</span><span class="sxs-lookup"><span data-stu-id="f4558-108">Read [Baseline Assessment in Operations Management Suite Security and Audit Solution](oms-security-baseline.md) for more information on this.</span></span>

<span data-ttu-id="f4558-109">Hallo-doel van Hallo web basislijn assessment is toofind kwetsbaar web server-instellingen.</span><span class="sxs-lookup"><span data-stu-id="f4558-109">hello goal of hello web baseline assessment is toofind potentially vulnerable web server settings.</span></span> <span data-ttu-id="f4558-110">Hallo drie primaire bronnen voor Hallo web basislijnconfiguraties zijn: .NET, ASP.NET en IIS-configuratie.</span><span class="sxs-lookup"><span data-stu-id="f4558-110">hello three primary sources for hello web baseline configurations are: .NET, ASP.NET, and IIS configuration.</span></span>  <span data-ttu-id="f4558-111">Net zoals het operationele systeem basislijn assessment hello, OMS beveiliging gaat tooscan uw webservers elke 24hrs en bieden een overzicht van de beveiligingsstatus van deze.</span><span class="sxs-lookup"><span data-stu-id="f4558-111">Just like hello operating system baseline assessment, OMS Security is going tooscan your web servers every 24hrs and provide a view into security state of them.</span></span>  <span data-ttu-id="f4558-112">Internet Information Service (IIS)-configuraties zijn zeer aanpasbare waarmee verschillende site en toepassing niveaus toobe-genegeerd.</span><span class="sxs-lookup"><span data-stu-id="f4558-112">In Internet Information Service (IIS), configurations are highly customizable, which allows various site and application levels toobe overridden.</span></span> <span data-ttu-id="f4558-113">Hallo scanner controleert Hallo-instellingen op elke toepassing siteniveau in toevoeging toohello standaard hoofdniveau.</span><span class="sxs-lookup"><span data-stu-id="f4558-113">hello scanner checks hello settings at each application/site level in addition toohello default root level.</span></span> <span data-ttu-id="f4558-114">Dit helpt u bij tooidentify mogelijke beveiligingsproblemen instellingen locaties en snel herstellen.</span><span class="sxs-lookup"><span data-stu-id="f4558-114">This helps you tooidentify potential vulnerability settings locations and quickly remediate.</span></span>


## <a name="web-security-baseline-assessment"></a><span data-ttu-id="f4558-115">Basislijnevaluatie van de webbeveiliging</span><span class="sxs-lookup"><span data-stu-id="f4558-115">Web Security Baseline Assessment</span></span>
<span data-ttu-id="f4558-116">Deze functie gaat toobe toegankelijk via Hallo OMS zoekoptie voor deze preview.</span><span class="sxs-lookup"><span data-stu-id="f4558-116">For this preview this feature is going toobe accessed using hello OMS Search option.</span></span> <span data-ttu-id="f4558-117">Hallo stappen hieronder tooperform Hallo bestemd voor toevoeging query:</span><span class="sxs-lookup"><span data-stu-id="f4558-117">Follow hello steps below tooperform hello appropriated query:</span></span>

1. <span data-ttu-id="f4558-118">In Hallo **Microsoft Operations Management Suite** hoofddashboard Klik **beveiligings- en Audit** tegel.</span><span class="sxs-lookup"><span data-stu-id="f4558-118">In hello **Microsoft Operations Management Suite** main dashboard click **Security and Audit** tile.</span></span>
2. <span data-ttu-id="f4558-119">In Hallo **beveiligings- en Audit** dashboard, klikt u op **logboek zoeken** knop.</span><span class="sxs-lookup"><span data-stu-id="f4558-119">In hello **Security and Audit** dashboard, click **Log Search** button.</span></span>
3. <span data-ttu-id="f4558-120">Hallo eerste query die u kunt gebruiken is Hallo **Web basislijn Assessment samenvatting**.</span><span class="sxs-lookup"><span data-stu-id="f4558-120">hello first query that you can use is hello **Web Baseline Assessment Summary**.</span></span> <span data-ttu-id="f4558-121">In Hallo **Begin zoeken hier** veld, typt u deze query: Type*SecurityBaselineSummary BaselineType = web =*.</span><span class="sxs-lookup"><span data-stu-id="f4558-121">In hello **Begin search here** field, type this query: Type*=SecurityBaselineSummary BaselineType=web*.</span></span> <span data-ttu-id="f4558-122">Hallo scherm volgen is een voorbeeld van uitvoer:</span><span class="sxs-lookup"><span data-stu-id="f4558-122">hello following screen has an output sample:</span></span>

![Overzicht van evaluatie van de webbasislijn](./media/oms-security-web-baseline/oms-security-web-baseline-fig1-new.png)

> [!NOTE]
> <span data-ttu-id="f4558-124">In deze query geeft elke record het evaluatieoverzicht op één server weer.</span><span class="sxs-lookup"><span data-stu-id="f4558-124">In this query, each record indicates assessment summary on a single server.</span></span>

<span data-ttu-id="f4558-125">Wanneer u naar Hallo **logboek zoeken**, kunt u verschillende query's tooobtain meer informatie over Hallo web basislijn assessment typen.</span><span class="sxs-lookup"><span data-stu-id="f4558-125">Once you are in hello **Log Search**, you can type different queries tooobtain more information about hello web baseline assessment.</span></span> <span data-ttu-id="f4558-126">Bovendien toohello vorige query, u kunt ook gebruiken Hallo uitzonderingen in dit voorbeeld te volgen.</span><span class="sxs-lookup"><span data-stu-id="f4558-126">In addition toohello previous query, you can also use hello following ones in this preview.</span></span>

<span data-ttu-id="f4558-127">**Web Baseline Rule Assessment** (Evaluatie van webbasislijnregels): elke record vertegenwoordigt een evaluatie van één webbasislijnregel op één server.</span><span class="sxs-lookup"><span data-stu-id="f4558-127">**Web Baseline Rule Assessment**: Each record represents a single web baseline rule evaluation on a single server.</span></span> <span data-ttu-id="f4558-128">Dit omvat alle gegevens voor de regel hello, locatie, Hallo verwacht resultaat en Hallo werkelijke resultaat.</span><span class="sxs-lookup"><span data-stu-id="f4558-128">It includes all data for hello rule, location, hello expected result, and hello actual result.</span></span>

<span data-ttu-id="f4558-129">**Query**: Type*=SecurityBaseline BaselineType=web*</span><span class="sxs-lookup"><span data-stu-id="f4558-129">**Query**: Type*=SecurityBaseline BaselineType=web*</span></span>

![Evaluatie van webbasislijnregels](./media/oms-security-web-baseline/oms-security-web-baseline-fig2.png)

<span data-ttu-id="f4558-131">**Weergeven van alle resultaten voor een specifieke server**: deze query geeft aan hoe toosee resultaten van een specifieke server.</span><span class="sxs-lookup"><span data-stu-id="f4558-131">**Show all results for a specific server**: This query shows how toosee results of a specific server.</span></span>

<span data-ttu-id="f4558-132">**Query**: *Type=SecurityBaseline BaselineType=web Computer=BaselineTestVM1*</span><span class="sxs-lookup"><span data-stu-id="f4558-132">**Query**: *Type=SecurityBaseline BaselineType=web Computer=BaselineTestVM1*</span></span>

![Alle resultaten](./media/oms-security-web-baseline/oms-security-web-baseline-fig3.png)

<span data-ttu-id="f4558-134">U kunt deze toocreate records/query's ook uw eigen dashboards, rapporten of meldingen.</span><span class="sxs-lookup"><span data-stu-id="f4558-134">You can also use these records/queries toocreate your own dashboards, reports, or alerts.</span></span> <span data-ttu-id="f4558-135">welkomstscherm onderstaande is een voorbeeld-UI-besturingselement dat u tooyour dashboard kunt toevoegen.</span><span class="sxs-lookup"><span data-stu-id="f4558-135">hello screen below has a sample UI control that you can add tooyour dashboard.</span></span> <span data-ttu-id="f4558-136">U leert hoe toovisualize uw gegevens dankzij OMS-ontwerper [hier](https://blogs.technet.microsoft.com/msoms/2016/06/30/oms-view-designer-visualize-your-data-your-way/).</span><span class="sxs-lookup"><span data-stu-id="f4558-136">You can learn how toovisualize your data using OMS View Designer [here](https://blogs.technet.microsoft.com/msoms/2016/06/30/oms-view-designer-visualize-your-data-your-way/).</span></span> <span data-ttu-id="f4558-137">welkomstscherm onderstaande is een voorbeeld van hoe Hallo tegel eruitziet nadat u deze aanpassing.</span><span class="sxs-lookup"><span data-stu-id="f4558-137">hello screen below is an example of how hello tile will look like once you make this customization.</span></span>

![Voorbeeld-UI](./media/oms-security-web-baseline/oms-security-web-baseline-fig4.png)

> [!NOTE]
> <span data-ttu-id="f4558-139">Als u tooknow Hallo instellingen die zijn geselecteerd voor de beoordeling van Hallo basislijn wilt, kunt u downloaden [deze Excel-spreadsheet](https://gallery.technet.microsoft.com/OMS-Web-Baseline-1e811690) die deze instellingen bevat.</span><span class="sxs-lookup"><span data-stu-id="f4558-139">If you would like tooknow hello settings that are checked for hello baseline assessment, you can download [this Excel spreadsheet](https://gallery.technet.microsoft.com/OMS-Web-Baseline-1e811690) that contains these settings.</span></span>

## <a name="see-also"></a><span data-ttu-id="f4558-140">Zie ook</span><span class="sxs-lookup"><span data-stu-id="f4558-140">See also</span></span>
<span data-ttu-id="f4558-141">In dit document hebt u meer kunnen lezen over het evalueren van de webbasislijn met behulp van de oplossing voor beveiliging en controle voor OMS.</span><span class="sxs-lookup"><span data-stu-id="f4558-141">In this document, you learned about OMS Security and Audit web baseline assessment.</span></span> <span data-ttu-id="f4558-142">toolearn meer informatie over OMS-beveiliging, Zie Hallo artikelen te volgen:</span><span class="sxs-lookup"><span data-stu-id="f4558-142">toolearn more about OMS Security, see hello following articles:</span></span>

* [<span data-ttu-id="f4558-143">Overzicht van Operations Management Suite (OMS)</span><span class="sxs-lookup"><span data-stu-id="f4558-143">Operations Management Suite (OMS) overview</span></span>](operations-management-suite-overview.md)
* [<span data-ttu-id="f4558-144">Bewaking en reageren tooSecurity waarschuwingen in de beveiliging van Operations Management Suite en Audit-oplossing</span><span class="sxs-lookup"><span data-stu-id="f4558-144">Monitoring and Responding tooSecurity Alerts in Operations Management Suite Security and Audit Solution</span></span>](oms-security-responding-alerts.md)
* [<span data-ttu-id="f4558-145">Resources bewaken in de oplossing Beveiliging en controle van Operations Management Suite </span><span class="sxs-lookup"><span data-stu-id="f4558-145">Monitoring Resources in Operations Management Suite Security and Audit Solution</span></span>](oms-security-monitoring-resources.md)


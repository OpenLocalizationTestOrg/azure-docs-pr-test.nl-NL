---
title: Webbasislijn van de oplossing voor beveiliging en controle voor Operations Management Suite | Microsoft Docs
description: In dit document wordt uitgelegd hoe u de oplossing voor beveiliging en controle voor OMS kunt gebruiken voor het uitvoeren van een evaluatie van de webbasislijn van alle bewaakte webservers, voor nalevings- en beveiligingsdoeleinden.
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
ms.openlocfilehash: 0d4707dc0c0ffbf40d0d10a6d12b9709a9655258
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="web-baseline-assessment-in-operations-management-suite-security-and-audit-solution"></a><span data-ttu-id="9bf23-103">Evaluatie van de webbasislijn in de oplossing voor beveiliging en controle voor Operations Management Suite</span><span class="sxs-lookup"><span data-stu-id="9bf23-103">Web Baseline Assessment in Operations Management Suite Security and Audit Solution</span></span>
<span data-ttu-id="9bf23-104">Dit document helpt u om de mogelijkheden van de [oplossing voor beveiliging en controle voor Operations Management Suite](operations-management-suite-overview.md) te gebruiken om evaluaties van de webbasislijn uit te voeren, en zo de beveiligde status van uw bewaakte resources te evalueren.</span><span class="sxs-lookup"><span data-stu-id="9bf23-104">This document helps you to use [Operations Management Suite (OMS) Security and Audit Solution](operations-management-suite-overview.md) web baseline assessment capabilities to access the secure state of your monitored resources.</span></span>

## <a name="what-is-web-baseline-assessment"></a><span data-ttu-id="9bf23-105">Wat is evaluatie van de webbasislijn?</span><span class="sxs-lookup"><span data-stu-id="9bf23-105">What is Web Baseline Assessment?</span></span>
<span data-ttu-id="9bf23-106">Beveiliging voor OMS biedt momenteel evaluatie van de beveiligingsbasislijn voor besturingssystemen.</span><span class="sxs-lookup"><span data-stu-id="9bf23-106">Currently OMS Security provides security baseline assessment for operating systems.</span></span> <span data-ttu-id="9bf23-107">Het scant de besturingssysteeminstellingen van uw servers elke 24 uur en biedt inzicht in mogelijk kwetsbare instellingen.</span><span class="sxs-lookup"><span data-stu-id="9bf23-107">It scans the operating system settings of your servers every 24 hours and provides a view into potentially vulnerable settings.</span></span> <span data-ttu-id="9bf23-108">Lees [Basislijnevaluatie in de oplossing voor beveiliging en controle voor Operations Management Suite](oms-security-baseline.md) voor meer informatie hierover.</span><span class="sxs-lookup"><span data-stu-id="9bf23-108">Read [Baseline Assessment in Operations Management Suite Security and Audit Solution](oms-security-baseline.md) for more information on this.</span></span>

<span data-ttu-id="9bf23-109">Het doel van de evaluatie van de webbasislijn is om mogelijk kwetsbare webserverinstellingen te vinden.</span><span class="sxs-lookup"><span data-stu-id="9bf23-109">The goal of the web baseline assessment is to find potentially vulnerable web server settings.</span></span> <span data-ttu-id="9bf23-110">De drie primaire bronnen voor de configuraties van de webbasislijn zijn: .NET, ASP.NET en IIS-configuratie.</span><span class="sxs-lookup"><span data-stu-id="9bf23-110">The three primary sources for the web baseline configurations are: .NET, ASP.NET, and IIS configuration.</span></span>  <span data-ttu-id="9bf23-111">Net als bij de evaluatie van de besturingssysteembasislijn, scant de beveiliging voor OMS uw webservers elke 24 uur en geeft u inzicht in hun beveiligingsstatus.</span><span class="sxs-lookup"><span data-stu-id="9bf23-111">Just like the operating system baseline assessment, OMS Security is going to scan your web servers every 24hrs and provide a view into security state of them.</span></span>  <span data-ttu-id="9bf23-112">In IIS (Internet Information Service) zijn configuraties in hoge mate aanpasbaar, waardoor verschillende niveaus voor sites en toepassingen kunnen worden overschreven.</span><span class="sxs-lookup"><span data-stu-id="9bf23-112">In Internet Information Service (IIS), configurations are highly customizable, which allows various site and application levels to be overridden.</span></span> <span data-ttu-id="9bf23-113">De scanner controleert de instellingen op elk niveau van de toepassing/site en op het standaardhoofdniveau.</span><span class="sxs-lookup"><span data-stu-id="9bf23-113">The scanner checks the settings at each application/site level in addition to the default root level.</span></span> <span data-ttu-id="9bf23-114">Zo kunt u de locatie van mogelijk kwetsbare instellingen identificeren en ze snel herstellen.</span><span class="sxs-lookup"><span data-stu-id="9bf23-114">This helps you to identify potential vulnerability settings locations and quickly remediate.</span></span>


## <a name="web-security-baseline-assessment"></a><span data-ttu-id="9bf23-115">Basislijnevaluatie van de webbeveiliging</span><span class="sxs-lookup"><span data-stu-id="9bf23-115">Web Security Baseline Assessment</span></span>
<span data-ttu-id="9bf23-116">In deze preview wordt de functie geopend met de zoekfuntie van OMS.</span><span class="sxs-lookup"><span data-stu-id="9bf23-116">For this preview this feature is going to be accessed using the OMS Search option.</span></span> <span data-ttu-id="9bf23-117">Volg de onderstaande stappen om de toegewezen query uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="9bf23-117">Follow the steps below to perform the appropriated query:</span></span>

1. <span data-ttu-id="9bf23-118">Klik in het hoofddashboard van **Microsoft Operations Management Suite** op de tegel **Beveiliging en controle**.</span><span class="sxs-lookup"><span data-stu-id="9bf23-118">In the **Microsoft Operations Management Suite** main dashboard click **Security and Audit** tile.</span></span>
2. <span data-ttu-id="9bf23-119">Klik in het dashboard **Beveiliging en controle** op de knop **Zoeken in logboeken**.</span><span class="sxs-lookup"><span data-stu-id="9bf23-119">In the **Security and Audit** dashboard, click **Log Search** button.</span></span>
3. <span data-ttu-id="9bf23-120">De eerste query die u kunt gebruiken is de **Web Baseline Assessment Summary** (Overzicht van de webbasislijnevaluatie).</span><span class="sxs-lookup"><span data-stu-id="9bf23-120">The first query that you can use is the **Web Baseline Assessment Summary**.</span></span> <span data-ttu-id="9bf23-121">Typ in het veld **Beginnen met zoeken** de volgende query: Type*=SecurityBaselineSummary BaselineType=web*.</span><span class="sxs-lookup"><span data-stu-id="9bf23-121">In the **Begin search here** field, type this query: Type*=SecurityBaselineSummary BaselineType=web*.</span></span> <span data-ttu-id="9bf23-122">Het volgende scherm heeft een voorbeelduitvoer:</span><span class="sxs-lookup"><span data-stu-id="9bf23-122">The following screen has an output sample:</span></span>

![Overzicht van evaluatie van de webbasislijn](./media/oms-security-web-baseline/oms-security-web-baseline-fig1-new.png)

> [!NOTE]
> <span data-ttu-id="9bf23-124">In deze query geeft elke record het evaluatieoverzicht op één server weer.</span><span class="sxs-lookup"><span data-stu-id="9bf23-124">In this query, each record indicates assessment summary on a single server.</span></span>

<span data-ttu-id="9bf23-125">Zodra u **Zoeken in logboeken** hebt geopend, kunt u verschillende query's invoeren om meer informatie over de evaluatie van de webbasislijn te verkrijgen.</span><span class="sxs-lookup"><span data-stu-id="9bf23-125">Once you are in the **Log Search**, you can type different queries to obtain more information about the web baseline assessment.</span></span> <span data-ttu-id="9bf23-126">U kunt naast de voorgaande query ook de volgende query's gebruiken in deze preview.</span><span class="sxs-lookup"><span data-stu-id="9bf23-126">In addition to the previous query, you can also use the following ones in this preview.</span></span>

<span data-ttu-id="9bf23-127">**Web Baseline Rule Assessment** (Evaluatie van webbasislijnregels): elke record vertegenwoordigt een evaluatie van één webbasislijnregel op één server.</span><span class="sxs-lookup"><span data-stu-id="9bf23-127">**Web Baseline Rule Assessment**: Each record represents a single web baseline rule evaluation on a single server.</span></span> <span data-ttu-id="9bf23-128">Deze bevat alle gegevens voor de regel, locatie, het verwachte resultaat en het werkelijke resultaat.</span><span class="sxs-lookup"><span data-stu-id="9bf23-128">It includes all data for the rule, location, the expected result, and the actual result.</span></span>

<span data-ttu-id="9bf23-129">**Query**: Type*=SecurityBaseline BaselineType=web*</span><span class="sxs-lookup"><span data-stu-id="9bf23-129">**Query**: Type*=SecurityBaseline BaselineType=web*</span></span>

![Evaluatie van webbasislijnregels](./media/oms-security-web-baseline/oms-security-web-baseline-fig2.png)

<span data-ttu-id="9bf23-131">**Show all results for a specific server** (Alle resultaten voor een specifieke server weergeven): deze query laat zien hoe u de resultaten van een bepaalde server kunt bekijken.</span><span class="sxs-lookup"><span data-stu-id="9bf23-131">**Show all results for a specific server**: This query shows how to see results of a specific server.</span></span>

<span data-ttu-id="9bf23-132">**Query**: *Type=SecurityBaseline BaselineType=web Computer=BaselineTestVM1*</span><span class="sxs-lookup"><span data-stu-id="9bf23-132">**Query**: *Type=SecurityBaseline BaselineType=web Computer=BaselineTestVM1*</span></span>

![Alle resultaten](./media/oms-security-web-baseline/oms-security-web-baseline-fig3.png)

<span data-ttu-id="9bf23-134">U kunt deze records/query's ook gebruiken om uw eigen dashboards, rapporten en waarschuwingen te maken.</span><span class="sxs-lookup"><span data-stu-id="9bf23-134">You can also use these records/queries to create your own dashboards, reports, or alerts.</span></span> <span data-ttu-id="9bf23-135">Het onderstaande scherm bevat een voorbeeld van een UI-besturingselement die u aan uw dashboard kunt toevoegen.</span><span class="sxs-lookup"><span data-stu-id="9bf23-135">The screen below has a sample UI control that you can add to your dashboard.</span></span> <span data-ttu-id="9bf23-136">U kunt [hier](https://blogs.technet.microsoft.com/msoms/2016/06/30/oms-view-designer-visualize-your-data-your-way/) leren hoe u uw gegevens visualiseert met behulp van de weergaveontwerper van OMS.</span><span class="sxs-lookup"><span data-stu-id="9bf23-136">You can learn how to visualize your data using OMS View Designer [here](https://blogs.technet.microsoft.com/msoms/2016/06/30/oms-view-designer-visualize-your-data-your-way/).</span></span> <span data-ttu-id="9bf23-137">Het scherm hieronder bevat een voorbeeld van hoe de tegel eruitziet nadat u deze aanpassing hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="9bf23-137">The screen below is an example of how the tile will look like once you make this customization.</span></span>

![Voorbeeld-UI](./media/oms-security-web-baseline/oms-security-web-baseline-fig4.png)

> [!NOTE]
> <span data-ttu-id="9bf23-139">Als u wilt weten welke instellingen worden geselecteerd voor de basislijnevaluatie, kunt u [dit Excel-werkblad](https://gallery.technet.microsoft.com/OMS-Web-Baseline-1e811690) met de instellingen downloaden.</span><span class="sxs-lookup"><span data-stu-id="9bf23-139">If you would like to know the settings that are checked for the baseline assessment, you can download [this Excel spreadsheet](https://gallery.technet.microsoft.com/OMS-Web-Baseline-1e811690) that contains these settings.</span></span>

## <a name="see-also"></a><span data-ttu-id="9bf23-140">Zie ook</span><span class="sxs-lookup"><span data-stu-id="9bf23-140">See also</span></span>
<span data-ttu-id="9bf23-141">In dit document hebt u meer kunnen lezen over het evalueren van de webbasislijn met behulp van de oplossing voor beveiliging en controle voor OMS.</span><span class="sxs-lookup"><span data-stu-id="9bf23-141">In this document, you learned about OMS Security and Audit web baseline assessment.</span></span> <span data-ttu-id="9bf23-142">Raadpleeg de volgende artikelen voor meer informatie over OMS Beveiliging:</span><span class="sxs-lookup"><span data-stu-id="9bf23-142">To learn more about OMS Security, see the following articles:</span></span>

* [<span data-ttu-id="9bf23-143">Overzicht van Operations Management Suite (OMS)</span><span class="sxs-lookup"><span data-stu-id="9bf23-143">Operations Management Suite (OMS) overview</span></span>](operations-management-suite-overview.md)
* [<span data-ttu-id="9bf23-144">Beveiligingswaarschuwingen in de oplossing Beveiliging en controle van Operations Management Suite bewaken en erop reageren</span><span class="sxs-lookup"><span data-stu-id="9bf23-144">Monitoring and Responding to Security Alerts in Operations Management Suite Security and Audit Solution</span></span>](oms-security-responding-alerts.md)
* [<span data-ttu-id="9bf23-145">Resources bewaken in de oplossing Beveiliging en controle van Operations Management Suite </span><span class="sxs-lookup"><span data-stu-id="9bf23-145">Monitoring Resources in Operations Management Suite Security and Audit Solution</span></span>](oms-security-monitoring-resources.md)


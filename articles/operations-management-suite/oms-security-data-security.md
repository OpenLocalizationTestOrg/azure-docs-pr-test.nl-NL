---
title: aaaOperations Management Suite beveiligings- en gegevensbeveiliging Audit-oplossing | Microsoft Docs
description: In dit document wordt uitgelegd hoe gegevens worden beheerd en bewaakt in de oplossing Beveiliging en controle in Operations Management Suite.
services: operations-management-suite
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: 
ms.assetid: 9cdf7deb-2a30-4672-b89f-71179ee8326a
ms.service: operations-management-suite
ms.custom: oms-security
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/30/2017
ms.author: yurid
ms.openlocfilehash: 9c4181b3b491e4f7f0c57d7252eca78a819722d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="operations-management-suite-security-and-audit-solution-data-security"></a><span data-ttu-id="ded57-103">Gegevensbeveiliging in de oplossing Beveiliging en controle in Operations Management Suite</span><span class="sxs-lookup"><span data-stu-id="ded57-103">Operations Management Suite Security and Audit solution data security</span></span>
<span data-ttu-id="ded57-104">toohelp klanten detecteren, voorkomen van en reageren toothreats, [Operations Management Suite (OMS) beveiligings- en Audit oplossing](operations-management-suite-overview.md) verzamelt en verwerkt gegevens over uw resources, waaronder:</span><span class="sxs-lookup"><span data-stu-id="ded57-104">toohelp customers prevent, detect, and respond toothreats, [Operations Management Suite  (OMS) Security and Audit Solution](operations-management-suite-overview.md) collects and processes data about your resources, which includes:</span></span>

* <span data-ttu-id="ded57-105">Beveiligingslogboek</span><span class="sxs-lookup"><span data-stu-id="ded57-105">Security event log</span></span>
* <span data-ttu-id="ded57-106">ETW-gebeurtenissen (Event Tracing for Windows)</span><span class="sxs-lookup"><span data-stu-id="ded57-106">Event Tracing for Windows (ETW) events</span></span>
* <span data-ttu-id="ded57-107">Controlegebeurtenissen AppLocker</span><span class="sxs-lookup"><span data-stu-id="ded57-107">AppLocker auditing events</span></span>
* <span data-ttu-id="ded57-108">Windows Firewall-logboek</span><span class="sxs-lookup"><span data-stu-id="ded57-108">Windows Firewall log</span></span>
* <span data-ttu-id="ded57-109">Advanced Threat Analytics-gebeurtenissen</span><span class="sxs-lookup"><span data-stu-id="ded57-109">Advanced Threat Analytics events</span></span>
* <span data-ttu-id="ded57-110">Resultaten van de evaluatie van de basislijn</span><span class="sxs-lookup"><span data-stu-id="ded57-110">Results of baseline assessment</span></span>
* <span data-ttu-id="ded57-111">Resultaten van de antimalware-evaluatie</span><span class="sxs-lookup"><span data-stu-id="ded57-111">Results of antimalware assessment</span></span>
* <span data-ttu-id="ded57-112">Resultaten van de evaluatie van updates/patching</span><span class="sxs-lookup"><span data-stu-id="ded57-112">Results of update/patch assessment</span></span>
* <span data-ttu-id="ded57-113">Syslogs stromen die expliciet zijn ingeschakeld op het Hallo-agent</span><span class="sxs-lookup"><span data-stu-id="ded57-113">Syslogs streams that are explicitly enabled on hello agent</span></span>

<span data-ttu-id="ded57-114">Wij maken sterk verbintenissen tooprotect Hallo privacy en beveiliging van deze gegevens.</span><span class="sxs-lookup"><span data-stu-id="ded57-114">We make strong commitments tooprotect hello privacy and security of this data.</span></span> <span data-ttu-id="ded57-115">Microsoft toostrict naleving en beveiliging richtlijnen voldoet, van een service toooperating coderen.</span><span class="sxs-lookup"><span data-stu-id="ded57-115">Microsoft adheres toostrict compliance and security guidelines—from coding toooperating a service.</span></span>
<span data-ttu-id="ded57-116">In dit artikel wordt uitgelegd hoe gegevens worden beheerd en beveiligd in Beveiliging en controle in OMS.</span><span class="sxs-lookup"><span data-stu-id="ded57-116">This article explains how data is managed and safeguarded in OMS Security and Audit Solution.</span></span>

## <a name="data-sources"></a><span data-ttu-id="ded57-117">Gegevensbronnen</span><span class="sxs-lookup"><span data-stu-id="ded57-117">Data sources</span></span>
<span data-ttu-id="ded57-118">OMS beveiligings- en Audit oplossing analyseren van gegevens op uw virtuele Machines en fysieke computers waarop Hallo OMS-Agent is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="ded57-118">OMS Security and Audit Solution analyze data from your Virtual Machines and physical computers where hello OMS Agent is installed.</span></span> <span data-ttu-id="ded57-119">Met de oplossing Beveiliging en controle in OMS worden configuratiegegevens over beveiligingsgebeurtenissen verzameld, zoals Windows-gebeurtenissen, controlelogboeken, IIS-logboeken en syslog-berichten.</span><span class="sxs-lookup"><span data-stu-id="ded57-119">OMS Security and Audit Solution can collect configuration information about security events, such as Windows event, audit logs, IIS logs and syslog messages.</span></span> <span data-ttu-id="ded57-120">Voorbeelden van dergelijke gegevens zijn: besturingssysteemtype en -versie, actieve processen, computernaam, IP-adressen, aangemelde gebruiker en tenant-id.</span><span class="sxs-lookup"><span data-stu-id="ded57-120">Examples of such data are: operating system type and version, running processes, machine name, IP addresses, logged in user, and tenant ID.</span></span>  

## <a name="data-protection"></a><span data-ttu-id="ded57-121">Gegevensbeveiliging</span><span class="sxs-lookup"><span data-stu-id="ded57-121">Data protection</span></span>
<span data-ttu-id="ded57-122">**Gegevensscheiding**: gegevens worden voor elk onderdeel in de gehele Hallo service logisch gescheiden gehouden.</span><span class="sxs-lookup"><span data-stu-id="ded57-122">**Data segregation**: Data is kept logically separate on each component throughout hello service.</span></span> <span data-ttu-id="ded57-123">Alle gegevens worden gemarkeerd per organisatie.</span><span class="sxs-lookup"><span data-stu-id="ded57-123">All data is tagged per organization.</span></span> <span data-ttu-id="ded57-124">Deze labels zich blijft voordoen gedurende de levenscyclus van Hallo gegevens en het wordt afgedwongen op elke laag van Hallo-service.</span><span class="sxs-lookup"><span data-stu-id="ded57-124">This tagging persists throughout hello data lifecycle, and it is enforced at each layer of hello service.</span></span> 

<span data-ttu-id="ded57-125">**Toegang tot gegevens**: tooprovide beveiligingsaanbevelingen en onderzoeken van mogelijke bedreigingen, medewerkers van Microsoft mogelijk toegang tot gegevens verzameld of geanalyseerd door services.</span><span class="sxs-lookup"><span data-stu-id="ded57-125">**Data access**: tooprovide security recommendations and investigate potential security threats, Microsoft personnel may access information collected or analyzed by services.</span></span> <span data-ttu-id="ded57-126">We ons houden toohello [Microsoft Online servicevoorwaarden](http://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=31) en [privacyverklaring](https://www.microsoft.com/privacystatement/en-us/OnlineServices/Default.aspx), die dat Microsoft wordt niet klantgegevens gebruiken of gegevens worden opgehaald van het voor adverteren of vergelijkbare status commerciële doeleinden.</span><span class="sxs-lookup"><span data-stu-id="ded57-126">We adhere toohello [Microsoft Online Services Terms](http://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=31) and [Privacy Statement](https://www.microsoft.com/privacystatement/en-us/OnlineServices/Default.aspx), which state that Microsoft will not use Customer Data or derive information from it for any advertising or similar commercial purposes.</span></span> <span data-ttu-id="ded57-127">beveiligingsaanbevelingen voor de tooprovide en onderzoeken van mogelijke bedreigingen, medewerkers van Microsoft mogelijk toegang tot gegevens verzameld of geanalyseerd door services.</span><span class="sxs-lookup"><span data-stu-id="ded57-127">tooprovide security recommendations and investigate potential security threats, Microsoft personnel may access information collected or analyzed by services.</span></span> <span data-ttu-id="ded57-128">We gebruiken klantgegevens alleen als de benodigde tooprovide u met Azure-services, met inbegrip van de toepassing compatibel is met deze services bieden.</span><span class="sxs-lookup"><span data-stu-id="ded57-128">We only use Customer Data as needed tooprovide you with Azure services, including purposes compatible with providing those services.</span></span> <span data-ttu-id="ded57-129">U behoudt alle rechten tooyour eigen gegevens.</span><span class="sxs-lookup"><span data-stu-id="ded57-129">You retain all rights tooyour own data.</span></span>

<span data-ttu-id="ded57-130">**Gebruik**: Microsoft patronen gebruikt en dreigingen gezien over meerdere tenants tooenhance onze mogelijkheden voor preventie en detectie; zo doen dat in overeenstemming met Hallo privacy verbintenissen beschreven in onze [Privacy Instructie](https://www.microsoft.com/privacystatement/en-us/OnlineServices/Default.aspx).</span><span class="sxs-lookup"><span data-stu-id="ded57-130">**Data use**: Microsoft uses patterns and threat intelligence seen across multiple tenants tooenhance our prevention and detection capabilities; we do so in accordance with hello privacy commitments described in our [Privacy Statement](https://www.microsoft.com/privacystatement/en-us/OnlineServices/Default.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="ded57-131">Locatie van gegevens is geconfigureerd op het niveau Hallo OMS werkruimte, tijdens het Hallo werkruimte maken, die deel uitmaakt van Hallo initiële OMS beveiligings- en Audit configuratieproces.</span><span class="sxs-lookup"><span data-stu-id="ded57-131">Data location is configured at hello OMS workspace level, during hello workspace creation, which is part of hello initial OMS Security and Audit configuration process.</span></span>
> 
> 

## <a name="see-also"></a><span data-ttu-id="ded57-132">Zie ook</span><span class="sxs-lookup"><span data-stu-id="ded57-132">See also</span></span>
<span data-ttu-id="ded57-133">In dit document hebt u geleerd hoe gegevens worden beheerd en bewaakt in OMS.</span><span class="sxs-lookup"><span data-stu-id="ded57-133">In this document, you learned how data is managed and safeguarded in OMS.</span></span> <span data-ttu-id="ded57-134">toolearn meer informatie over OMS beveiligings- en Audit-oplossing, Zie:</span><span class="sxs-lookup"><span data-stu-id="ded57-134">toolearn more about OMS Security and Audit solution, see:</span></span>

* [<span data-ttu-id="ded57-135">Overzicht van Operations Management Suite (OMS)</span><span class="sxs-lookup"><span data-stu-id="ded57-135">Operations Management Suite (OMS) overview</span></span>](operations-management-suite-overview.md)
* [<span data-ttu-id="ded57-136">Bewaking en reageren tooSecurity waarschuwingen in de beveiliging van Operations Management Suite en Audit-oplossing</span><span class="sxs-lookup"><span data-stu-id="ded57-136">Monitoring and Responding tooSecurity Alerts in Operations Management Suite Security and Audit Solution</span></span>](oms-security-responding-alerts.md)
* [<span data-ttu-id="ded57-137">Resources bewaken in de oplossing Beveiliging en controle van Operations Management Suite </span><span class="sxs-lookup"><span data-stu-id="ded57-137">Monitoring Resources in Operations Management Suite Security and Audit Solution</span></span>](oms-security-monitoring-resources.md)


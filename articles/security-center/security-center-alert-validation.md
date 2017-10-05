---
title: Validatie van waarschuwingen in Azure Security Center | Microsoft Docs
description: In dit document leest u hoe u de beveiligingswaarschuwingen in Azure Security Center valideert.
services: security-center
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: f8f17a55-e672-4d86-8ba9-6c3ce2e71a57
ms.service: security-center
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/11/2017
ms.author: yurid
ms.openlocfilehash: 121b5d8f023a9b663d0e7af26dce8f81db27672c
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="alerts-validation-in-azure-security-center"></a><span data-ttu-id="adad0-103">Validatie van waarschuwingen in Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="adad0-103">Alerts Validation in Azure Security Center</span></span>
<span data-ttu-id="adad0-104">In dit document leest u hoe u kunt controleren of uw systeem op de juiste manier is geconfigureerd voor waarschuwingen van Azure Security Center.</span><span class="sxs-lookup"><span data-stu-id="adad0-104">This document helps you learn how to verify if your system is properly configured for Azure Security Center alerts.</span></span>

## <a name="what-are-security-alerts"></a><span data-ttu-id="adad0-105">Wat zijn beveiligingswaarschuwingen?</span><span class="sxs-lookup"><span data-stu-id="adad0-105">What are security alerts?</span></span>
<span data-ttu-id="adad0-106">In Security Center worden automatisch logboekgegevens verzameld, geanalyseerd en geïntegreerd van uw Azure-resources, het netwerk en verbonden partneroplossingen, zoals firewalls en oplossingen voor eindpuntbeveiliging, om bedreigingen te detecteren en u hiervoor te waarschuwen.</span><span class="sxs-lookup"><span data-stu-id="adad0-106">Security Center automatically collects, analyzes, and integrates log data from your Azure resources, the network, and connected partner solutions, like firewall and endpoint protection solutions, to detect and alert you to threats.</span></span> <span data-ttu-id="adad0-107">Lees [Beveiligingswaarschuwingen beheren en erop reageren in Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-managing-and-responding-alerts) voor meer informatie over beveiligingswaarschuwingen. Lees [Beveiligingswaarschuwingen in Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-alerts-type) voor meer informatie over de verschillende typen waarschuwingen.</span><span class="sxs-lookup"><span data-stu-id="adad0-107">Read [Managing and responding to security alerts in Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-managing-and-responding-alerts) for more information about security alerts, and read [Understanding security alerts in Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-alerts-type) to learn more about the different types of alerts.</span></span>

## <a name="alert-validation"></a><span data-ttu-id="adad0-108">Waarschuwingen valideren</span><span class="sxs-lookup"><span data-stu-id="adad0-108">Alert validation</span></span>
<span data-ttu-id="adad0-109">Als de Security Center-agent is geïnstalleerd op uw computer, volgt u de onderstaande stappen op de computer waarvoor u een waarschuwing wilt ontvangen bij een aanval:</span><span class="sxs-lookup"><span data-stu-id="adad0-109">After Security Center agent is installed on your computer, follow the steps below from the computer where you want to be the attacked resource of the alert:</span></span>

1. <span data-ttu-id="adad0-110">Kopieer een uitvoerbaar bestand (bijvoorbeeld calc.exe) naar het bureaublad van de computer of een andere map die eenvoudig toegankelijk is.</span><span class="sxs-lookup"><span data-stu-id="adad0-110">Copy an executable (for example calc.exe) to the computer’s desktop, or other directory of your convenience.</span></span>
2. <span data-ttu-id="adad0-111">Wijzig de naam van dit bestand in **ASC_AlertTest_662jfi039N.exe**.</span><span class="sxs-lookup"><span data-stu-id="adad0-111">Rename this file to **ASC_AlertTest_662jfi039N.exe**.</span></span>
3. <span data-ttu-id="adad0-112">Open de opdrachtprompt en voer dit bestand uit met een zelf bedacht argument zoals *ASC_AlertTest_662jfi039N.exe - foo*</span><span class="sxs-lookup"><span data-stu-id="adad0-112">Open the command prompt and execute this file with an argument (just a fake argument name), such as: *ASC_AlertTest_662jfi039N.exe -foo*</span></span>
4. <span data-ttu-id="adad0-113">Wacht 5 tot 10 minuten en open Security Center.</span><span class="sxs-lookup"><span data-stu-id="adad0-113">Wait 5 to 10 minutes and open Security Center Alerts.</span></span> <span data-ttu-id="adad0-114">Hier moet u nu een waarschuwing zien zoals deze:</span><span class="sxs-lookup"><span data-stu-id="adad0-114">There you should find an alert similar to following one:</span></span>

    ![Waarschuwingen valideren](./media/security-center-alert-validation/security-center-alert-validation-fig1.png)

<span data-ttu-id="adad0-116">Als u deze waarschuwing bekijkt, moet in het veld Controle van argumenten ingeschakeld 'waar' worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="adad0-116">When reviewing this alert, make sure the field Arguments Auditing Enabled appears as true.</span></span> <span data-ttu-id="adad0-117">Als u de waarde 'onwaar' ziet, moet u de controle van opdrachtregelargumenten inschakelen.</span><span class="sxs-lookup"><span data-stu-id="adad0-117">If it shows false, you need to enable command-line arguments auditing.</span></span> <span data-ttu-id="adad0-118">Dit kan met de volgende opdrachtregel:</span><span class="sxs-lookup"><span data-stu-id="adad0-118">You can enable this option using the following command line:</span></span>

<span data-ttu-id="adad0-119">*reg add "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\policies\system\Audit" /f /v "ProcessCreationIncludeCmdLine_Enabled"*</span><span class="sxs-lookup"><span data-stu-id="adad0-119">*reg add "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\policies\system\Audit" /f /v "ProcessCreationIncludeCmdLine_Enabled"*</span></span>


## <a name="see-also"></a><span data-ttu-id="adad0-120">Zie ook</span><span class="sxs-lookup"><span data-stu-id="adad0-120">See also</span></span>
<span data-ttu-id="adad0-121">In dit artikel hebben we aandacht besteed aan het valideren van waarschuwingen.</span><span class="sxs-lookup"><span data-stu-id="adad0-121">This article introduced you to the alerts validation process.</span></span> <span data-ttu-id="adad0-122">Raadpleeg de volgende artikelen als u meer over dit onderwerp wilt weten:</span><span class="sxs-lookup"><span data-stu-id="adad0-122">Now that you're familiar with this validation, try the following articles:</span></span>

* <span data-ttu-id="adad0-123">[Beveiligingswaarschuwingen beheren en erop reageren in Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-managing-and-responding-alerts).</span><span class="sxs-lookup"><span data-stu-id="adad0-123">[Managing and responding to security alerts in Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-managing-and-responding-alerts).</span></span> <span data-ttu-id="adad0-124">Informatie over het beheren van waarschuwingen en het reageren op beveiligingsincidenten in Security Center.</span><span class="sxs-lookup"><span data-stu-id="adad0-124">Learn how to manage alerts, and respond to security incidents in Security Center.</span></span>
* <span data-ttu-id="adad0-125">[Beveiligingsstatus bewaken in Azure Security Center](security-center-monitoring.md).</span><span class="sxs-lookup"><span data-stu-id="adad0-125">[Security health monitoring in Azure Security Center](security-center-monitoring.md).</span></span> <span data-ttu-id="adad0-126">Meer informatie over het controleren van de status van uw Azure-resources.</span><span class="sxs-lookup"><span data-stu-id="adad0-126">Learn how to monitor the health of your Azure resources.</span></span>
* <span data-ttu-id="adad0-127">[Beveiligingswaarschuwingen in Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-alerts-type).</span><span class="sxs-lookup"><span data-stu-id="adad0-127">[Understanding security alerts in Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-alerts-type).</span></span> <span data-ttu-id="adad0-128">Meer informatie over de verschillende typen beveiligingswaarschuwingen.</span><span class="sxs-lookup"><span data-stu-id="adad0-128">Learn about the different types of security alerts.</span></span>
* <span data-ttu-id="adad0-129">[Handleiding voor het oplossen van problemen met Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-troubleshooting-guide).</span><span class="sxs-lookup"><span data-stu-id="adad0-129">[Azure Security Center Troubleshooting Guide](https://docs.microsoft.com/azure/security-center/security-center-troubleshooting-guide).</span></span> <span data-ttu-id="adad0-130">Informatie over het oplossen van veelvoorkomende problemen met Security Center.</span><span class="sxs-lookup"><span data-stu-id="adad0-130">Learn how to troubleshoot common issues in Security Center.</span></span> 
* <span data-ttu-id="adad0-131">[Veelgestelde vragen over Azure Security Center](security-center-faq.md).</span><span class="sxs-lookup"><span data-stu-id="adad0-131">[Azure Security Center FAQ](security-center-faq.md).</span></span> <span data-ttu-id="adad0-132">Raadpleeg de veelgestelde vragen over het gebruik van de service.</span><span class="sxs-lookup"><span data-stu-id="adad0-132">Find frequently asked questions about using the service.</span></span>
* <span data-ttu-id="adad0-133">[Azure-beveiligingsblog](http://blogs.msdn.com/b/azuresecurity/).</span><span class="sxs-lookup"><span data-stu-id="adad0-133">[Azure Security Blog](http://blogs.msdn.com/b/azuresecurity/).</span></span> <span data-ttu-id="adad0-134">Raadpleeg de blogberichten over beveiliging en naleving in Azure.</span><span class="sxs-lookup"><span data-stu-id="adad0-134">Find blog posts about Azure security and compliance.</span></span>


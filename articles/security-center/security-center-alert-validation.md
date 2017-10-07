---
title: aaaAlerts validatie in Azure Security Center | Microsoft Docs
description: Dit document helpt u toovalidate Hallo beveiligingswaarschuwingen in Azure Security Center.
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
ms.openlocfilehash: 030e9e74303758192eedaf517f1cb0d2e4a7852e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="alerts-validation-in-azure-security-center"></a><span data-ttu-id="36c91-103">Validatie van waarschuwingen in Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="36c91-103">Alerts Validation in Azure Security Center</span></span>
<span data-ttu-id="36c91-104">Dit document helpt u meer informatie over hoe tooverify als uw systeem juist is geconfigureerd voor Azure Security Center-waarschuwingen.</span><span class="sxs-lookup"><span data-stu-id="36c91-104">This document helps you learn how tooverify if your system is properly configured for Azure Security Center alerts.</span></span>

## <a name="what-are-security-alerts"></a><span data-ttu-id="36c91-105">Wat zijn beveiligingswaarschuwingen?</span><span class="sxs-lookup"><span data-stu-id="36c91-105">What are security alerts?</span></span>
<span data-ttu-id="36c91-106">Security Center automatisch verzamelt, analyseert en integreert logboekgegevens van uw Azure-resources, het Hallo-netwerk en de verbonden partneroplossingen, zoals een firewall en endpoint protection-oplossingen, toodetect en waarschuwing toothreats u.</span><span class="sxs-lookup"><span data-stu-id="36c91-106">Security Center automatically collects, analyzes, and integrates log data from your Azure resources, hello network, and connected partner solutions, like firewall and endpoint protection solutions, toodetect and alert you toothreats.</span></span> <span data-ttu-id="36c91-107">Lees [beheren en reageert toosecurity waarschuwingen in Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-managing-and-responding-alerts) voor meer informatie over beveiligingswaarschuwingen en lezen [beveiligingswaarschuwingen in Azure Security Center begrijpen](https://docs.microsoft.com/azure/security-center/security-center-alerts-type) toolearn meer over de verschillende typen Hallo van waarschuwingen.</span><span class="sxs-lookup"><span data-stu-id="36c91-107">Read [Managing and responding toosecurity alerts in Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-managing-and-responding-alerts) for more information about security alerts, and read [Understanding security alerts in Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-alerts-type) toolearn more about hello different types of alerts.</span></span>

## <a name="alert-validation"></a><span data-ttu-id="36c91-108">Waarschuwingen valideren</span><span class="sxs-lookup"><span data-stu-id="36c91-108">Alert validation</span></span>
<span data-ttu-id="36c91-109">Security Center-agent is geïnstalleerd op uw computer, Volg na Hallo stappen hieronder van Hallo computer waar u toobe Hallo aangevallen bron van het Hallo-waarschuwing:</span><span class="sxs-lookup"><span data-stu-id="36c91-109">After Security Center agent is installed on your computer, follow hello steps below from hello computer where you want toobe hello attacked resource of hello alert:</span></span>

1. <span data-ttu-id="36c91-110">Het bureaublad van de computer van een uitvoerbaar bestand (voor voorbeeld calc.exe) toohello of andere directory van uw gemak kopiëren.</span><span class="sxs-lookup"><span data-stu-id="36c91-110">Copy an executable (for example calc.exe) toohello computer’s desktop, or other directory of your convenience.</span></span>
2. <span data-ttu-id="36c91-111">Wijzig de naam van dit bestand te**ASC_AlertTest_662jfi039N.exe**.</span><span class="sxs-lookup"><span data-stu-id="36c91-111">Rename this file too**ASC_AlertTest_662jfi039N.exe**.</span></span>
3. <span data-ttu-id="36c91-112">Hallo-opdrachtprompt openen en het uitvoeren van dit bestand met een argument (alleen een valse argumentnaam), zoals: *ASC_AlertTest_662jfi039N.exe - foo*</span><span class="sxs-lookup"><span data-stu-id="36c91-112">Open hello command prompt and execute this file with an argument (just a fake argument name), such as: *ASC_AlertTest_662jfi039N.exe -foo*</span></span>
4. <span data-ttu-id="36c91-113">Wacht 5 minuten voor too10 en open Security Center Alerts.</span><span class="sxs-lookup"><span data-stu-id="36c91-113">Wait 5 too10 minutes and open Security Center Alerts.</span></span> <span data-ttu-id="36c91-114">Hier vindt u een waarschuwing vergelijkbare toofollowing een:</span><span class="sxs-lookup"><span data-stu-id="36c91-114">There you should find an alert similar toofollowing one:</span></span>

    ![Waarschuwingen valideren](./media/security-center-alert-validation/security-center-alert-validation-fig1.png)

<span data-ttu-id="36c91-116">Als deze waarschuwing wordt bekeken, controleert u Hallo veld argumenten controle ingeschakeld wordt weergegeven als waar.</span><span class="sxs-lookup"><span data-stu-id="36c91-116">When reviewing this alert, make sure hello field Arguments Auditing Enabled appears as true.</span></span> <span data-ttu-id="36c91-117">Als u deze waarde false ziet, moet u opdrachtregelargumenten tooenable controle.</span><span class="sxs-lookup"><span data-stu-id="36c91-117">If it shows false, you need tooenable command-line arguments auditing.</span></span> <span data-ttu-id="36c91-118">U kunt deze optie met behulp van de opdrachtregel na Hallo inschakelen:</span><span class="sxs-lookup"><span data-stu-id="36c91-118">You can enable this option using hello following command line:</span></span>

<span data-ttu-id="36c91-119">*reg add "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\policies\system\Audit" /f /v "ProcessCreationIncludeCmdLine_Enabled"*</span><span class="sxs-lookup"><span data-stu-id="36c91-119">*reg add "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\policies\system\Audit" /f /v "ProcessCreationIncludeCmdLine_Enabled"*</span></span>


## <a name="see-also"></a><span data-ttu-id="36c91-120">Zie ook</span><span class="sxs-lookup"><span data-stu-id="36c91-120">See also</span></span>
<span data-ttu-id="36c91-121">In dit artikel geïntroduceerd toohello waarschuwingen validatieproces.</span><span class="sxs-lookup"><span data-stu-id="36c91-121">This article introduced you toohello alerts validation process.</span></span> <span data-ttu-id="36c91-122">Nu u bekend bent met deze validatie, proberen Hallo artikelen te volgen:</span><span class="sxs-lookup"><span data-stu-id="36c91-122">Now that you're familiar with this validation, try hello following articles:</span></span>

* <span data-ttu-id="36c91-123">[Het beheer van is en reageert toosecurity waarschuwingen in Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-managing-and-responding-alerts).</span><span class="sxs-lookup"><span data-stu-id="36c91-123">[Managing and responding toosecurity alerts in Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-managing-and-responding-alerts).</span></span> <span data-ttu-id="36c91-124">Meer informatie over hoe toomanage waarschuwingen en reageren toosecurity incidenten in Security Center.</span><span class="sxs-lookup"><span data-stu-id="36c91-124">Learn how toomanage alerts, and respond toosecurity incidents in Security Center.</span></span>
* <span data-ttu-id="36c91-125">[Beveiligingsstatus bewaken in Azure Security Center](security-center-monitoring.md).</span><span class="sxs-lookup"><span data-stu-id="36c91-125">[Security health monitoring in Azure Security Center](security-center-monitoring.md).</span></span> <span data-ttu-id="36c91-126">Meer informatie over hoe toomonitor Hallo status van uw Azure-resources.</span><span class="sxs-lookup"><span data-stu-id="36c91-126">Learn how toomonitor hello health of your Azure resources.</span></span>
* <span data-ttu-id="36c91-127">[Beveiligingswaarschuwingen in Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-alerts-type).</span><span class="sxs-lookup"><span data-stu-id="36c91-127">[Understanding security alerts in Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-alerts-type).</span></span> <span data-ttu-id="36c91-128">Meer informatie over de verschillende soorten beveiligingswaarschuwingen Hallo.</span><span class="sxs-lookup"><span data-stu-id="36c91-128">Learn about hello different types of security alerts.</span></span>
* <span data-ttu-id="36c91-129">[Handleiding voor het oplossen van problemen met Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-troubleshooting-guide).</span><span class="sxs-lookup"><span data-stu-id="36c91-129">[Azure Security Center Troubleshooting Guide](https://docs.microsoft.com/azure/security-center/security-center-troubleshooting-guide).</span></span> <span data-ttu-id="36c91-130">Meer informatie over hoe tootroubleshoot algemene problemen in Security Center.</span><span class="sxs-lookup"><span data-stu-id="36c91-130">Learn how tootroubleshoot common issues in Security Center.</span></span> 
* <span data-ttu-id="36c91-131">[Veelgestelde vragen over Azure Security Center](security-center-faq.md).</span><span class="sxs-lookup"><span data-stu-id="36c91-131">[Azure Security Center FAQ](security-center-faq.md).</span></span> <span data-ttu-id="36c91-132">Veelgestelde vragen over het gebruik van Hallo service vinden.</span><span class="sxs-lookup"><span data-stu-id="36c91-132">Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="36c91-133">[Azure-beveiligingsblog](http://blogs.msdn.com/b/azuresecurity/).</span><span class="sxs-lookup"><span data-stu-id="36c91-133">[Azure Security Blog](http://blogs.msdn.com/b/azuresecurity/).</span></span> <span data-ttu-id="36c91-134">Raadpleeg de blogberichten over beveiliging en naleving in Azure.</span><span class="sxs-lookup"><span data-stu-id="36c91-134">Find blog posts about Azure security and compliance.</span></span>


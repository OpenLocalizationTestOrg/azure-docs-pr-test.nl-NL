---
title: Inschakelen van controle en detectie van bedreigingen op SQL-databases in Azure Security Center | Microsoft Docs
description: Dit document ziet u hoe de aanbeveling Azure Security Center implementeren ** inschakelen van controle en detectie van bedreigingen op SQL-databases **.
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 224b6755-2b36-4ecd-9af8-139a198e0df1
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/30/2017
ms.author: terrylan
ms.openlocfilehash: 8f4febdaa4497fee0dc690b59cd6eaa415c5e5cf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="enable-auditing-and-threat-detection-on-sql-databases-in-azure-security-center"></a><span data-ttu-id="1987e-103">Inschakelen van controle en detectie van bedreigingen op SQL-databases in Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="1987e-103">Enable auditing and threat detection on SQL databases in Azure Security Center</span></span>
<span data-ttu-id="1987e-104">Azure Security Center beveelt aan dat u controle en detectie van bedreigingen voor alle SQL-databases inschakelen als de controle en detectie van dreigingen nog niet is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="1987e-104">Azure Security Center will recommend that you turn on auditing and threat detection for all SQL databases if auditing and threat detection is not already enabled.</span></span> <span data-ttu-id="1987e-105">Controle en threat detectie kunt u de naleving van regelgeving onderhouden, de activiteit in een database begrijpen en meer van inzicht krijgen in discrepanties en afwijkingen die kunnen wijzen op problemen voor het bedrijf of vermoedelijke beveiligingsschendingen.</span><span class="sxs-lookup"><span data-stu-id="1987e-105">Auditing and threat detection can help you maintain regulatory compliance, understand database activity, and gain insight into discrepancies and anomalies that could indicate business concerns or suspected security violations.</span></span>

<span data-ttu-id="1987e-106">Wanneer u eenmaal hebt ingeschakeld controle kunt u instellingen voor de detectie van dreigingen en e-mailberichten voor het ontvangen van beveiligingsberichten kunt configureren.</span><span class="sxs-lookup"><span data-stu-id="1987e-106">Once you’ve turned on auditing you can configure Threat Detection settings and emails to receive security alerts.</span></span> <span data-ttu-id="1987e-107">Detectie van dreigingen detecteert afwijkende databaseactiviteiten die wijzen op beveiligingsdreigingen voor de database.</span><span class="sxs-lookup"><span data-stu-id="1987e-107">Threat Detection detects anomalous database activities indicating potential security threats to the database.</span></span> <span data-ttu-id="1987e-108">Hiermee kunt u om te detecteren en op mogelijke bedreigingen reageert wanneer deze zich voordoen.</span><span class="sxs-lookup"><span data-stu-id="1987e-108">This enables you to detect and respond to potential threats as they occur.</span></span>

<span data-ttu-id="1987e-109">Deze aanbeveling is van toepassing op de Azure SQL-service. SQL uitgevoerd op uw virtuele machines zijn niet opgenomen.</span><span class="sxs-lookup"><span data-stu-id="1987e-109">This recommendation applies to the Azure SQL service only; it doesn't include SQL running on your virtual machines.</span></span>

> [!NOTE]
> <span data-ttu-id="1987e-110">In dit document wordt de service geïntroduceerd aan de hand van een voorbeeldimplementatie.</span><span class="sxs-lookup"><span data-stu-id="1987e-110">This document introduces the service by using an example deployment.</span></span>  <span data-ttu-id="1987e-111">Dit is geen stapsgewijze handleiding.</span><span class="sxs-lookup"><span data-stu-id="1987e-111">This is not a step-by-step guide.</span></span>
>
>

## <a name="implement-the-recommendation"></a><span data-ttu-id="1987e-112">De aanbeveling implementeren</span><span class="sxs-lookup"><span data-stu-id="1987e-112">Implement the recommendation</span></span>
1. <span data-ttu-id="1987e-113">In de **aanbevelingen** blade Selecteer **controle inschakelen en detectie van bedreigingen op SQL-databases**.</span><span class="sxs-lookup"><span data-stu-id="1987e-113">In the **Recommendations** blade, select **Enable Auditing & Threat detection on SQL databases**.</span></span>  <span data-ttu-id="1987e-114">Hiermee opent u de **controle inschakelen en detectie van bedreigingen op SQL-databases** blade.</span><span class="sxs-lookup"><span data-stu-id="1987e-114">This opens the **Enable Auditing & Threat detection on SQL databases** blade.</span></span>

   ![Controleren voor SQL-databases inschakelen][1]
2. <span data-ttu-id="1987e-116">Selecteer een SQL-database inschakelen van controle op.</span><span class="sxs-lookup"><span data-stu-id="1987e-116">Select a SQL database to enable auditing on.</span></span> <span data-ttu-id="1987e-117">Hiermee opent u de **controle en detectie van dreigingen** blade.</span><span class="sxs-lookup"><span data-stu-id="1987e-117">This opens the **Auditing & Threat Detection** blade.</span></span>

3. <span data-ttu-id="1987e-118">Op de **controle en detectie van dreigingen** blade Selecteer **ON** onder **controle**.</span><span class="sxs-lookup"><span data-stu-id="1987e-118">On the **Auditing & Threat Detection** blade, select **ON** under **Auditing**.</span></span>

   ![Inschakelen van controle en detectie van bedreigingen][2]
4. <span data-ttu-id="1987e-120">Volg de stappen in [SQL Database met detectie van dreigingen in de Azure portal](../sql-database/sql-database-threat-detection-portal.md) inschakelen en configureren van detectie van dreigingen en de lijst met e-mailberichten die u waarschuwingen op vreemde activiteiten ontvangt configureert.</span><span class="sxs-lookup"><span data-stu-id="1987e-120">Follow the steps in [SQL Database Threat Detection in the Azure portal](../sql-database/sql-database-threat-detection-portal.md) to turn on and configure Threat Detection and to configure the list of emails that will receive security alerts upon detection of anomalous activities.</span></span>

## <a name="see-also"></a><span data-ttu-id="1987e-121">Zie ook</span><span class="sxs-lookup"><span data-stu-id="1987e-121">See also</span></span>
<span data-ttu-id="1987e-122">In dit artikel hebt u geleerd hoe u implementeert de aanbeveling Security Center ' Enable controle en detectie van bedreigingen op SQL-databases.'</span><span class="sxs-lookup"><span data-stu-id="1987e-122">This article showed you how to implement the Security Center recommendation "Enable Auditing & Threat detection on SQL databases."</span></span> <span data-ttu-id="1987e-123">Zie de volgende onderwerpen voor meer informatie over het beveiligen van uw SQL-database:</span><span class="sxs-lookup"><span data-stu-id="1987e-123">To learn more about securing your SQL database, see the following:</span></span>

* [<span data-ttu-id="1987e-124">Uw SQL-database beveiligen</span><span class="sxs-lookup"><span data-stu-id="1987e-124">Securing your SQL Database</span></span>](../sql-database/sql-database-security-overview.md)

<span data-ttu-id="1987e-125">Zie de volgende onderwerpen voor meer informatie over het Beveiligingscentrum:</span><span class="sxs-lookup"><span data-stu-id="1987e-125">To learn more about Security Center, see the following:</span></span>

* <span data-ttu-id="1987e-126">[Setting security policies in Azure Security Center](security-center-policies.md) (Beveiligingsbeleid instellen in Azure Security Center): leer hoe u beveiligingsbeleid voor uw Azure-abonnementen en -resourcegroepen configureert.</span><span class="sxs-lookup"><span data-stu-id="1987e-126">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how to configure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="1987e-127">[Aanbevelingen voor beveiliging in Azure Security Center beheren](security-center-recommendations.md) --Leer hoe aanbevelingen u uw Azure-resources te beveiligen.</span><span class="sxs-lookup"><span data-stu-id="1987e-127">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="1987e-128">[Beveiligingsstatus bewaken in Azure Security Center](security-center-monitoring.md) --informatie over het bewaken van de status van uw Azure-resources.</span><span class="sxs-lookup"><span data-stu-id="1987e-128">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how to monitor the health of your Azure resources.</span></span>
* <span data-ttu-id="1987e-129">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) (Beveiligingswaarschuwingen beheren en erop reageren in Azure Security Center): ontdek hoe u beveiligingswaarschuwingen kunt beheren en erop kunt reageren.</span><span class="sxs-lookup"><span data-stu-id="1987e-129">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how to manage and respond to security alerts.</span></span>
* <span data-ttu-id="1987e-130">[Partneroplossingen bewaken met Azure Security Center](security-center-partner-solutions.md): leer hoe u de integriteitsstatus van uw partneroplossingen kunt bewaken.</span><span class="sxs-lookup"><span data-stu-id="1987e-130">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how to monitor the health status of your partner solutions.</span></span>
* <span data-ttu-id="1987e-131">[Azure Security Center FAQ](security-center-faq.md) (Veelgestelde vragen over Azure Security Center): raadpleeg veelgestelde vragen over het gebruik van de service.</span><span class="sxs-lookup"><span data-stu-id="1987e-131">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using the service.</span></span>
* <span data-ttu-id="1987e-132">[Azure-Beveiligingsblog](http://blogs.msdn.com/b/azuresecurity/) --Lees het laatste nieuws van de Azure-beveiliging en de informatie.</span><span class="sxs-lookup"><span data-stu-id="1987e-132">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Get the latest Azure security news and information.</span></span>

<!--Image references-->
[1]: ./media/security-center-enable-auditing-on-sql-databases/enable-auditing-on-sql-databases.png
[2]: ./media/security-center-enable-auditing-on-sql-databases/auditing-threat-detection-blade.png

---
title: Inschakelen van controle en detectie van bedreigingen op SQL-servers in Azure Security Center | Microsoft Docs
description: Dit document ziet u hoe de aanbeveling Azure Security Center implementeren ** controle inschakelen en detectie van bedreigingen op SQL-servers **.
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 042fca4d-7dab-4172-8614-e8c21ccb4960
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/30/2017
ms.author: terrylan
ms.openlocfilehash: 660b537aef8d175a478ff93d60b8391d55fc92ad
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="enable-auditing-and-threat-detection-on-sql-servers-in-azure-security-center"></a><span data-ttu-id="646a5-103">Inschakelen van controle en detectie van bedreigingen op SQL-servers in Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="646a5-103">Enable auditing and threat detection on SQL servers in Azure Security Center</span></span>
<span data-ttu-id="646a5-104">Azure Security Center beveelt aan dat u controle inschakelt en detectie van dreigingen voor alle databases op uw Azure SQL-servers als controle is niet ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="646a5-104">Azure Security Center will recommend that you turn on auditing and threat detection for all databases on your Azure SQL servers if auditing is not already enabled.</span></span> <span data-ttu-id="646a5-105">Controle en threat detectie kunt u de naleving van regelgeving onderhouden, de activiteit in een database begrijpen en meer van inzicht krijgen in discrepanties en afwijkingen die kunnen wijzen op problemen voor het bedrijf of vermoedelijke beveiligingsschendingen.</span><span class="sxs-lookup"><span data-stu-id="646a5-105">Auditing and threat detection can help you maintain regulatory compliance, understand database activity, and gain insight into discrepancies and anomalies that could indicate business concerns or suspected security violations.</span></span>

<span data-ttu-id="646a5-106">Wanneer u eenmaal hebt ingeschakeld controle kunt u instellingen voor de detectie van dreigingen en e-mailberichten voor het ontvangen van beveiligingsberichten kunt configureren.</span><span class="sxs-lookup"><span data-stu-id="646a5-106">Once you’ve turned on auditing you can configure Threat Detection settings and emails to receive security alerts.</span></span> <span data-ttu-id="646a5-107">Detectie van dreigingen detecteert afwijkende databaseactiviteiten die wijzen op beveiligingsdreigingen voor de database.</span><span class="sxs-lookup"><span data-stu-id="646a5-107">Threat Detection detects anomalous database activities indicating potential security threats to the database.</span></span> <span data-ttu-id="646a5-108">Hiermee kunt u om te detecteren en op mogelijke bedreigingen reageert wanneer deze zich voordoen.</span><span class="sxs-lookup"><span data-stu-id="646a5-108">This enables you to detect and respond to potential threats as they occur.</span></span>

<span data-ttu-id="646a5-109">Deze aanbeveling is van toepassing op de Azure SQL-service. SQL Server wordt uitgevoerd op uw virtuele machines in Azure-infrastructuurservices (Azure IaaS) zijn niet opgenomen.</span><span class="sxs-lookup"><span data-stu-id="646a5-109">This recommendation applies to the Azure SQL service only; it doesn’t include SQL Server running on your virtual machines in Azure Infrastructure Services (Azure IaaS).</span></span>

> [!NOTE]
> <span data-ttu-id="646a5-110">In dit document wordt de service geïntroduceerd aan de hand van een voorbeeldimplementatie.</span><span class="sxs-lookup"><span data-stu-id="646a5-110">This document introduces the service by using an example deployment.</span></span>  <span data-ttu-id="646a5-111">Dit is geen stapsgewijze handleiding.</span><span class="sxs-lookup"><span data-stu-id="646a5-111">This is not a step-by-step guide.</span></span>
>
>

## <a name="implement-the-recommendation"></a><span data-ttu-id="646a5-112">De aanbeveling implementeren</span><span class="sxs-lookup"><span data-stu-id="646a5-112">Implement the recommendation</span></span>
1. <span data-ttu-id="646a5-113">In de **aanbevelingen** blade Selecteer **controle inschakelen en detectie van bedreigingen op SQL-servers**.</span><span class="sxs-lookup"><span data-stu-id="646a5-113">In the **Recommendations** blade, select **Enable Auditing & Threat detection on SQL servers**.</span></span>  <span data-ttu-id="646a5-114">Hiermee opent u de **controle inschakelen en detectie van bedreigingen op SQL-servers** blade.</span><span class="sxs-lookup"><span data-stu-id="646a5-114">This opens the **Enable Auditing & Threat detection on SQL servers** blade.</span></span>

   ![Controleren voor SQL-servers inschakelen][1]
2. <span data-ttu-id="646a5-116">Selecteer een SQL-server inschakelen van controle en detectie van bedreigingen op.</span><span class="sxs-lookup"><span data-stu-id="646a5-116">Select a SQL server to enable auditing and threat detection on.</span></span> <span data-ttu-id="646a5-117">Hiermee opent u de **controle en detectie van dreigingen** blade.</span><span class="sxs-lookup"><span data-stu-id="646a5-117">This opens the **Auditing & Threat Detection** blade.</span></span>

3. <span data-ttu-id="646a5-118">Op de **controle en detectie van dreigingen** blade Selecteer **ON** onder **controle**.</span><span class="sxs-lookup"><span data-stu-id="646a5-118">On the **Auditing & Threat Detection** blade, select **ON** under **Auditing**.</span></span>

   ![Controle-instellingen inschakelen][2]
4. <span data-ttu-id="646a5-120">Volg de stappen in [SQL database auditing in de Azure portal](../sql-database/sql-database-auditing-portal.md) configureren van opslag waar de controlelogboeken worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="646a5-120">Follow the steps in [SQL database auditing in the Azure portal](../sql-database/sql-database-auditing-portal.md) to configure storage where your audit logs will be stored.</span></span> <span data-ttu-id="646a5-121">Storage-account voor het verzamelen van gegevens van het abonnement is het standaardopslagaccount.</span><span class="sxs-lookup"><span data-stu-id="646a5-121">The subscription's storage account for data collection is the default storage account.</span></span>
5. <span data-ttu-id="646a5-122">Volg de stappen in [aan de slag met SQL Database met detectie van dreigingen](../sql-database/sql-database-threat-detection.md) inschakelen en configureren van detectie van dreigingen en de lijst met e-mailberichten die u waarschuwingen op vreemde activiteiten ontvangt configureert.</span><span class="sxs-lookup"><span data-stu-id="646a5-122">Follow the steps in [Get started with SQL Database Threat Detection](../sql-database/sql-database-threat-detection.md) to turn on and configure Threat Detection and to configure the list of emails that will receive security alerts upon detection of anomalous activities.</span></span>

## <a name="see-also"></a><span data-ttu-id="646a5-123">Zie ook</span><span class="sxs-lookup"><span data-stu-id="646a5-123">See also</span></span>
<span data-ttu-id="646a5-124">In dit artikel hebt u geleerd hoe u implementeert de Security Center aanbeveling ' Enable controle en detectie van bedreigingen op SQL-servers."</span><span class="sxs-lookup"><span data-stu-id="646a5-124">This article showed you how to implement the Security Center recommendation "Enable auditing and threat detection on SQL servers."</span></span> <span data-ttu-id="646a5-125">Zie de volgende onderwerpen voor meer informatie over het beveiligen van uw SQL-database:</span><span class="sxs-lookup"><span data-stu-id="646a5-125">To learn more about securing your SQL database, see the following:</span></span>

* [<span data-ttu-id="646a5-126">Uw SQL-database beveiligen</span><span class="sxs-lookup"><span data-stu-id="646a5-126">Securing your SQL Database</span></span>](../sql-database/sql-database-security-overview.md)

<span data-ttu-id="646a5-127">Zie de volgende onderwerpen voor meer informatie over het Beveiligingscentrum:</span><span class="sxs-lookup"><span data-stu-id="646a5-127">To learn more about Security Center, see the following:</span></span>

* <span data-ttu-id="646a5-128">[Setting security policies in Azure Security Center](security-center-policies.md) (Beveiligingsbeleid instellen in Azure Security Center): leer hoe u beveiligingsbeleid voor uw Azure-abonnementen en -resourcegroepen configureert.</span><span class="sxs-lookup"><span data-stu-id="646a5-128">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how to configure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="646a5-129">[Aanbevelingen voor beveiliging in Azure Security Center beheren](security-center-recommendations.md) --Leer hoe aanbevelingen u uw Azure-resources te beveiligen.</span><span class="sxs-lookup"><span data-stu-id="646a5-129">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="646a5-130">[Beveiligingsstatus bewaken in Azure Security Center](security-center-monitoring.md) --informatie over het bewaken van de status van uw Azure-resources.</span><span class="sxs-lookup"><span data-stu-id="646a5-130">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how to monitor the health of your Azure resources.</span></span>
* <span data-ttu-id="646a5-131">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) (Beveiligingswaarschuwingen beheren en erop reageren in Azure Security Center): ontdek hoe u beveiligingswaarschuwingen kunt beheren en erop kunt reageren.</span><span class="sxs-lookup"><span data-stu-id="646a5-131">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how to manage and respond to security alerts.</span></span>
* <span data-ttu-id="646a5-132">[Partneroplossingen bewaken met Azure Security Center](security-center-partner-solutions.md): leer hoe u de integriteitsstatus van uw partneroplossingen kunt bewaken.</span><span class="sxs-lookup"><span data-stu-id="646a5-132">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how to monitor the health status of your partner solutions.</span></span>
* <span data-ttu-id="646a5-133">[Azure Security Center FAQ](security-center-faq.md) (Veelgestelde vragen over Azure Security Center): raadpleeg veelgestelde vragen over het gebruik van de service.</span><span class="sxs-lookup"><span data-stu-id="646a5-133">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using the service.</span></span>
* <span data-ttu-id="646a5-134">[Azure-Beveiligingsblog](http://blogs.msdn.com/b/azuresecurity/) --Lees het laatste nieuws van de Azure-beveiliging en de informatie.</span><span class="sxs-lookup"><span data-stu-id="646a5-134">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Get the latest Azure security news and information.</span></span>

<!--Image references-->
[1]: ./media/security-center-enable-auditing-on-sql-server/enable-auditing-on-sql-servers.png
[2]: ./media/security-center-enable-auditing-on-sql-server/auditing-settings-blade.png

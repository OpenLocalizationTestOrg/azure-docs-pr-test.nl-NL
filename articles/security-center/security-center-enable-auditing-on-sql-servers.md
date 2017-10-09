---
title: aaaEnable controle en detectie van bedreigingen op SQL-servers in Azure Security Center | Microsoft Docs
description: Dit document leest u hoe tooimplement hello Azure Security Center aanbeveling ** controle inschakelen en detectie van bedreigingen op SQL-servers **.
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
ms.openlocfilehash: b082c48cdbc386f14e677f4e13a7f306f37fd0e8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="enable-auditing-and-threat-detection-on-sql-servers-in-azure-security-center"></a><span data-ttu-id="884a8-103">Inschakelen van controle en detectie van bedreigingen op SQL-servers in Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="884a8-103">Enable auditing and threat detection on SQL servers in Azure Security Center</span></span>
<span data-ttu-id="884a8-104">Azure Security Center beveelt aan dat u controle inschakelt en detectie van dreigingen voor alle databases op uw Azure SQL-servers als controle is niet ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="884a8-104">Azure Security Center will recommend that you turn on auditing and threat detection for all databases on your Azure SQL servers if auditing is not already enabled.</span></span> <span data-ttu-id="884a8-105">Controle en threat detectie kunt u de naleving van regelgeving onderhouden, de activiteit in een database begrijpen en meer van inzicht krijgen in discrepanties en afwijkingen die kunnen wijzen op problemen voor het bedrijf of vermoedelijke beveiligingsschendingen.</span><span class="sxs-lookup"><span data-stu-id="884a8-105">Auditing and threat detection can help you maintain regulatory compliance, understand database activity, and gain insight into discrepancies and anomalies that could indicate business concerns or suspected security violations.</span></span>

<span data-ttu-id="884a8-106">Wanneer u eenmaal hebt ingeschakeld controle kunt u de detectie van dreigingen instellingen en e-mailberichten tooreceive beveiligingswaarschuwingen configureren.</span><span class="sxs-lookup"><span data-stu-id="884a8-106">Once you’ve turned on auditing you can configure Threat Detection settings and emails tooreceive security alerts.</span></span> <span data-ttu-id="884a8-107">Detectie van dreigingen detecteert afwijkende databaseactiviteiten die wijzen op mogelijke bedreigingen toohello database met.</span><span class="sxs-lookup"><span data-stu-id="884a8-107">Threat Detection detects anomalous database activities indicating potential security threats toohello database.</span></span> <span data-ttu-id="884a8-108">Hiermee kunt u toodetect en toopotential bedreigingen reageert wanneer deze zich voordoen.</span><span class="sxs-lookup"><span data-stu-id="884a8-108">This enables you toodetect and respond toopotential threats as they occur.</span></span>

<span data-ttu-id="884a8-109">Deze aanbeveling is van toepassing toohello Azure SQL-service. SQL Server wordt uitgevoerd op uw virtuele machines in Azure-infrastructuurservices (Azure IaaS) zijn niet opgenomen.</span><span class="sxs-lookup"><span data-stu-id="884a8-109">This recommendation applies toohello Azure SQL service only; it doesn’t include SQL Server running on your virtual machines in Azure Infrastructure Services (Azure IaaS).</span></span>

> [!NOTE]
> <span data-ttu-id="884a8-110">Dit document bevat Hallo service met behulp van een voorbeeldimplementatie.</span><span class="sxs-lookup"><span data-stu-id="884a8-110">This document introduces hello service by using an example deployment.</span></span>  <span data-ttu-id="884a8-111">Dit is geen stapsgewijze handleiding.</span><span class="sxs-lookup"><span data-stu-id="884a8-111">This is not a step-by-step guide.</span></span>
>
>

## <a name="implement-hello-recommendation"></a><span data-ttu-id="884a8-112">Hallo aanbeveling implementeren</span><span class="sxs-lookup"><span data-stu-id="884a8-112">Implement hello recommendation</span></span>
1. <span data-ttu-id="884a8-113">In Hallo **aanbevelingen** blade Selecteer **controle inschakelen en detectie van bedreigingen op SQL-servers**.</span><span class="sxs-lookup"><span data-stu-id="884a8-113">In hello **Recommendations** blade, select **Enable Auditing & Threat detection on SQL servers**.</span></span>  <span data-ttu-id="884a8-114">Hiermee opent u Hallo **controle inschakelen en detectie van bedreigingen op SQL-servers** blade.</span><span class="sxs-lookup"><span data-stu-id="884a8-114">This opens hello **Enable Auditing & Threat detection on SQL servers** blade.</span></span>

   ![Controleren voor SQL-servers inschakelen][1]
2. <span data-ttu-id="884a8-116">Selecteer een SQL server tooenable controle en detectie van bedreigingen op.</span><span class="sxs-lookup"><span data-stu-id="884a8-116">Select a SQL server tooenable auditing and threat detection on.</span></span> <span data-ttu-id="884a8-117">Hiermee opent u Hallo **controle en detectie van dreigingen** blade.</span><span class="sxs-lookup"><span data-stu-id="884a8-117">This opens hello **Auditing & Threat Detection** blade.</span></span>

3. <span data-ttu-id="884a8-118">Op Hallo **controle en detectie van dreigingen** blade Selecteer **ON** onder **controle**.</span><span class="sxs-lookup"><span data-stu-id="884a8-118">On hello **Auditing & Threat Detection** blade, select **ON** under **Auditing**.</span></span>

   ![Controle-instellingen inschakelen][2]
4. <span data-ttu-id="884a8-120">Volg de stappen Hallo in [SQL database auditing in Azure-portal Hallo](../sql-database/sql-database-auditing-portal.md) tooconfigure opslag waar de controlelogboeken worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="884a8-120">Follow hello steps in [SQL database auditing in hello Azure portal](../sql-database/sql-database-auditing-portal.md) tooconfigure storage where your audit logs will be stored.</span></span> <span data-ttu-id="884a8-121">Hallo is van abonnement storage-account voor gegevensverzameling Hallo storage-standaardaccount.</span><span class="sxs-lookup"><span data-stu-id="884a8-121">hello subscription's storage account for data collection is hello default storage account.</span></span>
5. <span data-ttu-id="884a8-122">Hallo stappen in [aan de slag met SQL Database-Bedreigingsdetectie](../sql-database/sql-database-threat-detection.md) tooturn op en configureren van detectie van dreigingen en tooconfigure Hallo lijst met e-mailberichten die beveiligingswaarschuwingen bij vreemde activiteiten worden ontvangen.</span><span class="sxs-lookup"><span data-stu-id="884a8-122">Follow hello steps in [Get started with SQL Database Threat Detection](../sql-database/sql-database-threat-detection.md) tooturn on and configure Threat Detection and tooconfigure hello list of emails that will receive security alerts upon detection of anomalous activities.</span></span>

## <a name="see-also"></a><span data-ttu-id="884a8-123">Zie ook</span><span class="sxs-lookup"><span data-stu-id="884a8-123">See also</span></span>
<span data-ttu-id="884a8-124">In dit artikel hebt u geleerd hoe tooimplement Security Center aanbeveling Hallo 'Bedreigingendetectie op SQL-servers en controle in te schakelen.'</span><span class="sxs-lookup"><span data-stu-id="884a8-124">This article showed you how tooimplement hello Security Center recommendation "Enable auditing and threat detection on SQL servers."</span></span> <span data-ttu-id="884a8-125">toolearn meer informatie over het beveiligen van uw SQL-database Hallo ziet:</span><span class="sxs-lookup"><span data-stu-id="884a8-125">toolearn more about securing your SQL database, see hello following:</span></span>

* [<span data-ttu-id="884a8-126">Uw SQL-database beveiligen</span><span class="sxs-lookup"><span data-stu-id="884a8-126">Securing your SQL Database</span></span>](../sql-database/sql-database-security-overview.md)

<span data-ttu-id="884a8-127">toolearn meer informatie over Security Center Hallo ziet:</span><span class="sxs-lookup"><span data-stu-id="884a8-127">toolearn more about Security Center, see hello following:</span></span>

* <span data-ttu-id="884a8-128">[Beveiligingsbeleid instellen in Azure Security Center](security-center-policies.md) --meer informatie over hoe tooconfigure beveiligingsbeleid voor uw Azure-abonnementen en resourcegroepen.</span><span class="sxs-lookup"><span data-stu-id="884a8-128">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how tooconfigure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="884a8-129">[Aanbevelingen voor beveiliging in Azure Security Center beheren](security-center-recommendations.md) --Leer hoe aanbevelingen u uw Azure-resources te beveiligen.</span><span class="sxs-lookup"><span data-stu-id="884a8-129">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="884a8-130">[Beveiligingsstatus bewaken in Azure Security Center](security-center-monitoring.md) --meer informatie over hoe toomonitor Hallo status van uw Azure-resources.</span><span class="sxs-lookup"><span data-stu-id="884a8-130">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how toomonitor hello health of your Azure resources.</span></span>
* <span data-ttu-id="884a8-131">[Het beheer van is en reageert toosecurity waarschuwingen in Azure Security Center](security-center-managing-and-responding-alerts.md) --meer informatie over hoe toomanage en gereageerd had toosecurity waarschuwingen.</span><span class="sxs-lookup"><span data-stu-id="884a8-131">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how toomanage and respond toosecurity alerts.</span></span>
* <span data-ttu-id="884a8-132">[Partneroplossingen bewaken met Azure Security Center](security-center-partner-solutions.md) --meer informatie over hoe toomonitor gezondheidsstatus van uw partneroplossingen Hallo.</span><span class="sxs-lookup"><span data-stu-id="884a8-132">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how toomonitor hello health status of your partner solutions.</span></span>
* <span data-ttu-id="884a8-133">[Veelgestelde vragen over Azure Security Center](security-center-faq.md) --Raadpleeg Veelgestelde vragen over het gebruik van Hallo-service.</span><span class="sxs-lookup"><span data-stu-id="884a8-133">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="884a8-134">[Azure-Beveiligingsblog](http://blogs.msdn.com/b/azuresecurity/) --Hallo nieuwste Azure-beveiliging nieuws en informatie.</span><span class="sxs-lookup"><span data-stu-id="884a8-134">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Get hello latest Azure security news and information.</span></span>

<!--Image references-->
[1]: ./media/security-center-enable-auditing-on-sql-server/enable-auditing-on-sql-servers.png
[2]: ./media/security-center-enable-auditing-on-sql-server/auditing-settings-blade.png

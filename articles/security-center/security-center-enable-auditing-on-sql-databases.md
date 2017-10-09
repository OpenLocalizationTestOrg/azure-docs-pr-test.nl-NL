---
title: aaaEnable controle en detectie van bedreigingen op de SQL-databases in Azure Security Center | Microsoft Docs
description: Dit document leest u hoe tooimplement hello Azure Security Center aanbeveling ** inschakelen van controle en detectie van bedreigingen op SQL-databases **.
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
ms.openlocfilehash: c94140acf37cabaca3e681ba5db79d6827e7b9db
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="enable-auditing-and-threat-detection-on-sql-databases-in-azure-security-center"></a><span data-ttu-id="7019f-103">Inschakelen van controle en detectie van bedreigingen op SQL-databases in Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="7019f-103">Enable auditing and threat detection on SQL databases in Azure Security Center</span></span>
<span data-ttu-id="7019f-104">Azure Security Center beveelt aan dat u controle en detectie van bedreigingen voor alle SQL-databases inschakelen als de controle en detectie van dreigingen nog niet is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="7019f-104">Azure Security Center will recommend that you turn on auditing and threat detection for all SQL databases if auditing and threat detection is not already enabled.</span></span> <span data-ttu-id="7019f-105">Controle en threat detectie kunt u de naleving van regelgeving onderhouden, de activiteit in een database begrijpen en meer van inzicht krijgen in discrepanties en afwijkingen die kunnen wijzen op problemen voor het bedrijf of vermoedelijke beveiligingsschendingen.</span><span class="sxs-lookup"><span data-stu-id="7019f-105">Auditing and threat detection can help you maintain regulatory compliance, understand database activity, and gain insight into discrepancies and anomalies that could indicate business concerns or suspected security violations.</span></span>

<span data-ttu-id="7019f-106">Wanneer u eenmaal hebt ingeschakeld controle kunt u de detectie van dreigingen instellingen en e-mailberichten tooreceive beveiligingswaarschuwingen configureren.</span><span class="sxs-lookup"><span data-stu-id="7019f-106">Once you’ve turned on auditing you can configure Threat Detection settings and emails tooreceive security alerts.</span></span> <span data-ttu-id="7019f-107">Detectie van dreigingen detecteert afwijkende databaseactiviteiten die wijzen op mogelijke bedreigingen toohello database met.</span><span class="sxs-lookup"><span data-stu-id="7019f-107">Threat Detection detects anomalous database activities indicating potential security threats toohello database.</span></span> <span data-ttu-id="7019f-108">Hiermee kunt u toodetect en toopotential bedreigingen reageert wanneer deze zich voordoen.</span><span class="sxs-lookup"><span data-stu-id="7019f-108">This enables you toodetect and respond toopotential threats as they occur.</span></span>

<span data-ttu-id="7019f-109">Deze aanbeveling is van toepassing toohello Azure SQL-service. SQL uitgevoerd op uw virtuele machines zijn niet opgenomen.</span><span class="sxs-lookup"><span data-stu-id="7019f-109">This recommendation applies toohello Azure SQL service only; it doesn't include SQL running on your virtual machines.</span></span>

> [!NOTE]
> <span data-ttu-id="7019f-110">Dit document bevat Hallo service met behulp van een voorbeeldimplementatie.</span><span class="sxs-lookup"><span data-stu-id="7019f-110">This document introduces hello service by using an example deployment.</span></span>  <span data-ttu-id="7019f-111">Dit is geen stapsgewijze handleiding.</span><span class="sxs-lookup"><span data-stu-id="7019f-111">This is not a step-by-step guide.</span></span>
>
>

## <a name="implement-hello-recommendation"></a><span data-ttu-id="7019f-112">Hallo aanbeveling implementeren</span><span class="sxs-lookup"><span data-stu-id="7019f-112">Implement hello recommendation</span></span>
1. <span data-ttu-id="7019f-113">In Hallo **aanbevelingen** blade Selecteer **controle inschakelen en detectie van bedreigingen op SQL-databases**.</span><span class="sxs-lookup"><span data-stu-id="7019f-113">In hello **Recommendations** blade, select **Enable Auditing & Threat detection on SQL databases**.</span></span>  <span data-ttu-id="7019f-114">Hiermee opent u Hallo **controle inschakelen en detectie van bedreigingen op SQL-databases** blade.</span><span class="sxs-lookup"><span data-stu-id="7019f-114">This opens hello **Enable Auditing & Threat detection on SQL databases** blade.</span></span>

   ![Controleren voor SQL-databases inschakelen][1]
2. <span data-ttu-id="7019f-116">Selecteer een SQL database tooenable controle op.</span><span class="sxs-lookup"><span data-stu-id="7019f-116">Select a SQL database tooenable auditing on.</span></span> <span data-ttu-id="7019f-117">Hiermee opent u Hallo **controle en detectie van dreigingen** blade.</span><span class="sxs-lookup"><span data-stu-id="7019f-117">This opens hello **Auditing & Threat Detection** blade.</span></span>

3. <span data-ttu-id="7019f-118">Op Hallo **controle en detectie van dreigingen** blade Selecteer **ON** onder **controle**.</span><span class="sxs-lookup"><span data-stu-id="7019f-118">On hello **Auditing & Threat Detection** blade, select **ON** under **Auditing**.</span></span>

   ![Inschakelen van controle en detectie van bedreigingen][2]
4. <span data-ttu-id="7019f-120">Volg de stappen Hallo in [SQL Database met detectie van dreigingen in hello Azure-portal](../sql-database/sql-database-threat-detection-portal.md) tooturn op en configureren van detectie van dreigingen en tooconfigure Hallo lijst met e-mailberichten die u waarschuwingen op vreemde activiteiten ontvangt.</span><span class="sxs-lookup"><span data-stu-id="7019f-120">Follow hello steps in [SQL Database Threat Detection in hello Azure portal](../sql-database/sql-database-threat-detection-portal.md) tooturn on and configure Threat Detection and tooconfigure hello list of emails that will receive security alerts upon detection of anomalous activities.</span></span>

## <a name="see-also"></a><span data-ttu-id="7019f-121">Zie ook</span><span class="sxs-lookup"><span data-stu-id="7019f-121">See also</span></span>
<span data-ttu-id="7019f-122">In dit artikel hebt u geleerd hoe tooimplement Hallo Security Center aanbeveling ' Enable controle en detectie van bedreigingen op SQL-databases.'</span><span class="sxs-lookup"><span data-stu-id="7019f-122">This article showed you how tooimplement hello Security Center recommendation "Enable Auditing & Threat detection on SQL databases."</span></span> <span data-ttu-id="7019f-123">toolearn meer informatie over het beveiligen van uw SQL-database Hallo ziet:</span><span class="sxs-lookup"><span data-stu-id="7019f-123">toolearn more about securing your SQL database, see hello following:</span></span>

* [<span data-ttu-id="7019f-124">Uw SQL-database beveiligen</span><span class="sxs-lookup"><span data-stu-id="7019f-124">Securing your SQL Database</span></span>](../sql-database/sql-database-security-overview.md)

<span data-ttu-id="7019f-125">toolearn meer informatie over Security Center Hallo ziet:</span><span class="sxs-lookup"><span data-stu-id="7019f-125">toolearn more about Security Center, see hello following:</span></span>

* <span data-ttu-id="7019f-126">[Beveiligingsbeleid instellen in Azure Security Center](security-center-policies.md) --meer informatie over hoe tooconfigure beveiligingsbeleid voor uw Azure-abonnementen en resourcegroepen.</span><span class="sxs-lookup"><span data-stu-id="7019f-126">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how tooconfigure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="7019f-127">[Aanbevelingen voor beveiliging in Azure Security Center beheren](security-center-recommendations.md) --Leer hoe aanbevelingen u uw Azure-resources te beveiligen.</span><span class="sxs-lookup"><span data-stu-id="7019f-127">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="7019f-128">[Beveiligingsstatus bewaken in Azure Security Center](security-center-monitoring.md) --meer informatie over hoe toomonitor Hallo status van uw Azure-resources.</span><span class="sxs-lookup"><span data-stu-id="7019f-128">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how toomonitor hello health of your Azure resources.</span></span>
* <span data-ttu-id="7019f-129">[Het beheer van is en reageert toosecurity waarschuwingen in Azure Security Center](security-center-managing-and-responding-alerts.md) --meer informatie over hoe toomanage en gereageerd had toosecurity waarschuwingen.</span><span class="sxs-lookup"><span data-stu-id="7019f-129">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how toomanage and respond toosecurity alerts.</span></span>
* <span data-ttu-id="7019f-130">[Partneroplossingen bewaken met Azure Security Center](security-center-partner-solutions.md) --meer informatie over hoe toomonitor gezondheidsstatus van uw partneroplossingen Hallo.</span><span class="sxs-lookup"><span data-stu-id="7019f-130">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how toomonitor hello health status of your partner solutions.</span></span>
* <span data-ttu-id="7019f-131">[Veelgestelde vragen over Azure Security Center](security-center-faq.md) --Raadpleeg Veelgestelde vragen over het gebruik van Hallo-service.</span><span class="sxs-lookup"><span data-stu-id="7019f-131">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="7019f-132">[Azure-Beveiligingsblog](http://blogs.msdn.com/b/azuresecurity/) --Hallo nieuwste Azure-beveiliging nieuws en informatie.</span><span class="sxs-lookup"><span data-stu-id="7019f-132">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Get hello latest Azure security news and information.</span></span>

<!--Image references-->
[1]: ./media/security-center-enable-auditing-on-sql-databases/enable-auditing-on-sql-databases.png
[2]: ./media/security-center-enable-auditing-on-sql-databases/auditing-threat-detection-blade.png

---
title: aaaEnable Transparent Data Encryption in Azure Security Center | Microsoft Docs
description: Dit document leest u hoe tooimplement hello Azure Security Center aanbeveling ** inschakelen Transparent Data Encryption **.
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: e4be8a0e-2118-4ee9-a266-69e52d9f7f8e
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/02/2017
ms.author: terrylan
ms.openlocfilehash: 94c6e9a1feddaa48faac6c835d416c4d131cd5c5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="enable-transparent-data-encryption-in-azure-security-center"></a><span data-ttu-id="6eaa0-103">Transparante gegevensversleuteling in Azure Security Center inschakelen</span><span class="sxs-lookup"><span data-stu-id="6eaa0-103">Enable Transparent Data Encryption in Azure Security Center</span></span>
<span data-ttu-id="6eaa0-104">Azure Security Center beveelt aan dat u Transparent Data Encryption (TDE) voor SQL-databases inschakelen als TDE nog niet is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="6eaa0-104">Azure Security Center will recommend that you enable Transparent Data Encryption (TDE) on SQL databases if TDE is not already enabled.</span></span> <span data-ttu-id="6eaa0-105">TDE beschermt u uw gegevens en kunt u voldoen aan nalevingsvereisten door uw database, gekoppelde back-ups en transactielogboekbestanden in rust, zonder dat wijzigingen tooyour toepassing te versleutelen.</span><span class="sxs-lookup"><span data-stu-id="6eaa0-105">TDE protects your data and helps you meet compliance requirements by encrypting your database, associated backups, and transaction log files at rest, without requiring changes tooyour application.</span></span> <span data-ttu-id="6eaa0-106">toolearn Zie meer [Transparent Data Encryption met Azure SQL Database](https://msdn.microsoft.com/library/dn948096).</span><span class="sxs-lookup"><span data-stu-id="6eaa0-106">toolearn more see [Transparent Data Encryption with Azure SQL Database](https://msdn.microsoft.com/library/dn948096).</span></span>

<span data-ttu-id="6eaa0-107">Deze aanbeveling is van toepassing toohello Azure SQL-service. bevat geen SQL uitgevoerd op uw virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="6eaa0-107">This recommendation applies toohello Azure SQL service only; doesn't include SQL running on your virtual machines.</span></span>

> [!NOTE]
> <span data-ttu-id="6eaa0-108">Dit document bevat Hallo service met behulp van een voorbeeldimplementatie.</span><span class="sxs-lookup"><span data-stu-id="6eaa0-108">This document introduces hello service by using an example deployment.</span></span>  <span data-ttu-id="6eaa0-109">Dit is geen stapsgewijze handleiding.</span><span class="sxs-lookup"><span data-stu-id="6eaa0-109">This is not a step-by-step guide.</span></span>
>
>

## <a name="implement-hello-recommendation"></a><span data-ttu-id="6eaa0-110">Hallo aanbeveling implementeren</span><span class="sxs-lookup"><span data-stu-id="6eaa0-110">Implement hello recommendation</span></span>
1. <span data-ttu-id="6eaa0-111">In Hallo **aanbevelingen** blade Selecteer **Transparent Data Encryption inschakelen**.</span><span class="sxs-lookup"><span data-stu-id="6eaa0-111">In hello **Recommendations** blade, select **Enable Transparent Data Encryption**.</span></span>
   <span data-ttu-id="6eaa0-112">![Transparante gegevensversleuteling inschakelen][1]</span><span class="sxs-lookup"><span data-stu-id="6eaa0-112">![Enable Transparent Data Encryption][1]</span></span>
2. <span data-ttu-id="6eaa0-113">Hiermee opent u Hallo **Transparent Data Encryption voor SQL-databases inschakelen** blade.</span><span class="sxs-lookup"><span data-stu-id="6eaa0-113">This opens hello **Enable Transparent Data Encryption on SQL databases** blade.</span></span> <span data-ttu-id="6eaa0-114">Selecteer een SQL-database tooenable TDE op.</span><span class="sxs-lookup"><span data-stu-id="6eaa0-114">Select a SQL database tooenable TDE on.</span></span>
   <span data-ttu-id="6eaa0-115">![Selecteer SQL DB tooenable TDE op][2]</span><span class="sxs-lookup"><span data-stu-id="6eaa0-115">![Select SQL DB tooenable TDE on][2]</span></span>
3. <span data-ttu-id="6eaa0-116">Op Hallo **transparante gegevensversleuteling** blade Selecteer **ON** onder gegevensversleuteling en selecteer **opslaan** in de bovenste lint Hallo van Hallo-blade.</span><span class="sxs-lookup"><span data-stu-id="6eaa0-116">On hello **Transparent data encryption** blade, select **ON** under Data encryption and select **Save** in hello top ribbon of hello blade.</span></span>
   <span data-ttu-id="6eaa0-117">![TDE inschakelen][3]</span><span class="sxs-lookup"><span data-stu-id="6eaa0-117">![Turn on TDE][3]</span></span>

   <span data-ttu-id="6eaa0-118">Zodra TDE is ingeschakeld voor Hallo geselecteerd SQL-database, hello **coderingsstatus** wordt ook wijzigen**versleutelde**.</span><span class="sxs-lookup"><span data-stu-id="6eaa0-118">Once TDE is enabled on hello selected SQL database, hello **Encryption status** will change too**Encrypted**.</span></span>    

   ![Coderingsstatus][4]

## <a name="see-also"></a><span data-ttu-id="6eaa0-120">Zie ook</span><span class="sxs-lookup"><span data-stu-id="6eaa0-120">See also</span></span>
<span data-ttu-id="6eaa0-121">In dit artikel hebt u geleerd hoe tooimplement Hallo Security Center aanbeveling 'Enable Transparent Data Encryption'.</span><span class="sxs-lookup"><span data-stu-id="6eaa0-121">This article showed you how tooimplement hello Security Center recommendation "Enable Transparent Data Encryption."</span></span> <span data-ttu-id="6eaa0-122">toolearn meer informatie over SQL TDE Hallo ziet:</span><span class="sxs-lookup"><span data-stu-id="6eaa0-122">toolearn more about SQL TDE, see hello following:</span></span>

* [<span data-ttu-id="6eaa0-123">Transparante gegevensversleuteling met Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="6eaa0-123">Transparent Data Encryption with Azure SQL Database</span></span>](https://msdn.microsoft.com/library/dn948096)
* [<span data-ttu-id="6eaa0-124">Aan de slag met Transparent Data Encryption (TDE)</span><span class="sxs-lookup"><span data-stu-id="6eaa0-124">Get started with Transparent Data Encryption (TDE)</span></span>](../sql-data-warehouse/sql-data-warehouse-encryption-tde.md)

<span data-ttu-id="6eaa0-125">toolearn meer informatie over Security Center Hallo ziet:</span><span class="sxs-lookup"><span data-stu-id="6eaa0-125">toolearn more about Security Center, see hello following:</span></span>

* <span data-ttu-id="6eaa0-126">[Beveiligingsbeleid instellen in Azure Security Center](security-center-policies.md) --meer informatie over hoe tooconfigure beveiligingsbeleid voor uw Azure-abonnementen en resourcegroepen.</span><span class="sxs-lookup"><span data-stu-id="6eaa0-126">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how tooconfigure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="6eaa0-127">[Aanbevelingen voor beveiliging in Azure Security Center beheren](security-center-recommendations.md) --Leer hoe aanbevelingen u uw Azure-resources te beveiligen.</span><span class="sxs-lookup"><span data-stu-id="6eaa0-127">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="6eaa0-128">[Beveiligingsstatus bewaken in Azure Security Center](security-center-monitoring.md) --meer informatie over hoe toomonitor Hallo status van uw Azure-resources.</span><span class="sxs-lookup"><span data-stu-id="6eaa0-128">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how toomonitor hello health of your Azure resources.</span></span>
* <span data-ttu-id="6eaa0-129">[Het beheer van is en reageert toosecurity waarschuwingen in Azure Security Center](security-center-managing-and-responding-alerts.md) --meer informatie over hoe toomanage en gereageerd had toosecurity waarschuwingen.</span><span class="sxs-lookup"><span data-stu-id="6eaa0-129">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how toomanage and respond toosecurity alerts.</span></span>
* <span data-ttu-id="6eaa0-130">[Partneroplossingen bewaken met Azure Security Center](security-center-partner-solutions.md) --meer informatie over hoe toomonitor gezondheidsstatus van uw partneroplossingen Hallo.</span><span class="sxs-lookup"><span data-stu-id="6eaa0-130">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how toomonitor hello health status of your partner solutions.</span></span>
* <span data-ttu-id="6eaa0-131">[Veelgestelde vragen over Azure Security Center](security-center-faq.md) --Raadpleeg Veelgestelde vragen over het gebruik van Hallo-service.</span><span class="sxs-lookup"><span data-stu-id="6eaa0-131">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="6eaa0-132">[Azure-Beveiligingsblog](http://blogs.msdn.com/b/azuresecurity/) --Hallo nieuwste Azure-beveiliging nieuws en informatie.</span><span class="sxs-lookup"><span data-stu-id="6eaa0-132">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Get hello latest Azure security news and information.</span></span>

<!--Image references-->
[1]: ./media/security-center-enable-tde-on-sql-databases/enable-tde.png
[2]:./media/security-center-enable-tde-on-sql-databases/transparent-data-encryption-blade.png
[3]: ./media/security-center-enable-tde-on-sql-databases/turn-on-tde.png
[4]: ./media/security-center-enable-tde-on-sql-databases/encrypted.png

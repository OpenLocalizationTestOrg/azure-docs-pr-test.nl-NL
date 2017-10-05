---
title: Transparante gegevensversleuteling in Azure Security Center inschakelen | Microsoft Docs
description: Dit document ziet u hoe de aanbeveling Azure Security Center implementeren ** inschakelen Transparent Data Encryption **.
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
ms.openlocfilehash: 2a2963affdbff3710ad08f86c6ed4e6304335559
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="enable-transparent-data-encryption-in-azure-security-center"></a><span data-ttu-id="12dc1-103">Transparante gegevensversleuteling in Azure Security Center inschakelen</span><span class="sxs-lookup"><span data-stu-id="12dc1-103">Enable Transparent Data Encryption in Azure Security Center</span></span>
<span data-ttu-id="12dc1-104">Azure Security Center beveelt aan dat u Transparent Data Encryption (TDE) voor SQL-databases inschakelen als TDE nog niet is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="12dc1-104">Azure Security Center will recommend that you enable Transparent Data Encryption (TDE) on SQL databases if TDE is not already enabled.</span></span> <span data-ttu-id="12dc1-105">TDE beschermt u uw gegevens en kunt u voldoen aan nalevingsvereisten door uw database, gekoppelde back-ups en transactielogboekbestanden in rust, zonder dat wijzigingen in uw toepassing te versleutelen.</span><span class="sxs-lookup"><span data-stu-id="12dc1-105">TDE protects your data and helps you meet compliance requirements by encrypting your database, associated backups, and transaction log files at rest, without requiring changes to your application.</span></span> <span data-ttu-id="12dc1-106">Voor meer informatie over [Transparent Data Encryption met Azure SQL Database](https://msdn.microsoft.com/library/dn948096).</span><span class="sxs-lookup"><span data-stu-id="12dc1-106">To learn more see [Transparent Data Encryption with Azure SQL Database](https://msdn.microsoft.com/library/dn948096).</span></span>

<span data-ttu-id="12dc1-107">Deze aanbeveling is van toepassing op de Azure SQL-service. bevat geen SQL uitgevoerd op uw virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="12dc1-107">This recommendation applies to the Azure SQL service only; doesn't include SQL running on your virtual machines.</span></span>

> [!NOTE]
> <span data-ttu-id="12dc1-108">In dit document wordt de service geïntroduceerd aan de hand van een voorbeeldimplementatie.</span><span class="sxs-lookup"><span data-stu-id="12dc1-108">This document introduces the service by using an example deployment.</span></span>  <span data-ttu-id="12dc1-109">Dit is geen stapsgewijze handleiding.</span><span class="sxs-lookup"><span data-stu-id="12dc1-109">This is not a step-by-step guide.</span></span>
>
>

## <a name="implement-the-recommendation"></a><span data-ttu-id="12dc1-110">De aanbeveling implementeren</span><span class="sxs-lookup"><span data-stu-id="12dc1-110">Implement the recommendation</span></span>
1. <span data-ttu-id="12dc1-111">In de **aanbevelingen** blade Selecteer **Transparent Data Encryption inschakelen**.</span><span class="sxs-lookup"><span data-stu-id="12dc1-111">In the **Recommendations** blade, select **Enable Transparent Data Encryption**.</span></span>
   <span data-ttu-id="12dc1-112">![Transparante gegevensversleuteling inschakelen][1]</span><span class="sxs-lookup"><span data-stu-id="12dc1-112">![Enable Transparent Data Encryption][1]</span></span>
2. <span data-ttu-id="12dc1-113">Hiermee opent u de **Transparent Data Encryption voor SQL-databases inschakelen** blade.</span><span class="sxs-lookup"><span data-stu-id="12dc1-113">This opens the **Enable Transparent Data Encryption on SQL databases** blade.</span></span> <span data-ttu-id="12dc1-114">Selecteer een SQL-database in te schakelen TDE voor.</span><span class="sxs-lookup"><span data-stu-id="12dc1-114">Select a SQL database to enable TDE on.</span></span>
   <span data-ttu-id="12dc1-115">![Selecteer SQL DB TDE inschakelen op][2]</span><span class="sxs-lookup"><span data-stu-id="12dc1-115">![Select SQL DB to enable TDE on][2]</span></span>
3. <span data-ttu-id="12dc1-116">Op de **transparante gegevensversleuteling** blade Selecteer **ON** onder gegevensversleuteling en selecteer **opslaan** in het bovenste lint van de blade.</span><span class="sxs-lookup"><span data-stu-id="12dc1-116">On the **Transparent data encryption** blade, select **ON** under Data encryption and select **Save** in the top ribbon of the blade.</span></span>
   <span data-ttu-id="12dc1-117">![TDE inschakelen][3]</span><span class="sxs-lookup"><span data-stu-id="12dc1-117">![Turn on TDE][3]</span></span>

   <span data-ttu-id="12dc1-118">Zodra TDE is ingeschakeld voor de geselecteerde SQL-database, de **coderingsstatus** wordt gewijzigd in **versleutelde**.</span><span class="sxs-lookup"><span data-stu-id="12dc1-118">Once TDE is enabled on the selected SQL database, the **Encryption status** will change to **Encrypted**.</span></span>    

   ![Coderingsstatus][4]

## <a name="see-also"></a><span data-ttu-id="12dc1-120">Zie ook</span><span class="sxs-lookup"><span data-stu-id="12dc1-120">See also</span></span>
<span data-ttu-id="12dc1-121">In dit artikel hebt u geleerd hoe u de aanbeveling Security Center implementeert 'Transparent Data Encryption inschakelen'.</span><span class="sxs-lookup"><span data-stu-id="12dc1-121">This article showed you how to implement the Security Center recommendation "Enable Transparent Data Encryption."</span></span> <span data-ttu-id="12dc1-122">Voor meer informatie over SQL TDE, Zie de volgende:</span><span class="sxs-lookup"><span data-stu-id="12dc1-122">To learn more about SQL TDE, see the following:</span></span>

* [<span data-ttu-id="12dc1-123">Transparante gegevensversleuteling met Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="12dc1-123">Transparent Data Encryption with Azure SQL Database</span></span>](https://msdn.microsoft.com/library/dn948096)
* [<span data-ttu-id="12dc1-124">Aan de slag met Transparent Data Encryption (TDE)</span><span class="sxs-lookup"><span data-stu-id="12dc1-124">Get started with Transparent Data Encryption (TDE)</span></span>](../sql-data-warehouse/sql-data-warehouse-encryption-tde.md)

<span data-ttu-id="12dc1-125">Zie de volgende onderwerpen voor meer informatie over het Beveiligingscentrum:</span><span class="sxs-lookup"><span data-stu-id="12dc1-125">To learn more about Security Center, see the following:</span></span>

* <span data-ttu-id="12dc1-126">[Setting security policies in Azure Security Center](security-center-policies.md) (Beveiligingsbeleid instellen in Azure Security Center): leer hoe u beveiligingsbeleid voor uw Azure-abonnementen en -resourcegroepen configureert.</span><span class="sxs-lookup"><span data-stu-id="12dc1-126">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how to configure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="12dc1-127">[Aanbevelingen voor beveiliging in Azure Security Center beheren](security-center-recommendations.md) --Leer hoe aanbevelingen u uw Azure-resources te beveiligen.</span><span class="sxs-lookup"><span data-stu-id="12dc1-127">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="12dc1-128">[Beveiligingsstatus bewaken in Azure Security Center](security-center-monitoring.md) --informatie over het bewaken van de status van uw Azure-resources.</span><span class="sxs-lookup"><span data-stu-id="12dc1-128">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how to monitor the health of your Azure resources.</span></span>
* <span data-ttu-id="12dc1-129">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) (Beveiligingswaarschuwingen beheren en erop reageren in Azure Security Center): ontdek hoe u beveiligingswaarschuwingen kunt beheren en erop kunt reageren.</span><span class="sxs-lookup"><span data-stu-id="12dc1-129">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how to manage and respond to security alerts.</span></span>
* <span data-ttu-id="12dc1-130">[Partneroplossingen bewaken met Azure Security Center](security-center-partner-solutions.md): leer hoe u de integriteitsstatus van uw partneroplossingen kunt bewaken.</span><span class="sxs-lookup"><span data-stu-id="12dc1-130">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how to monitor the health status of your partner solutions.</span></span>
* <span data-ttu-id="12dc1-131">[Azure Security Center FAQ](security-center-faq.md) (Veelgestelde vragen over Azure Security Center): raadpleeg veelgestelde vragen over het gebruik van de service.</span><span class="sxs-lookup"><span data-stu-id="12dc1-131">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using the service.</span></span>
* <span data-ttu-id="12dc1-132">[Azure-Beveiligingsblog](http://blogs.msdn.com/b/azuresecurity/) --Lees het laatste nieuws van de Azure-beveiliging en de informatie.</span><span class="sxs-lookup"><span data-stu-id="12dc1-132">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Get the latest Azure security news and information.</span></span>

<!--Image references-->
[1]: ./media/security-center-enable-tde-on-sql-databases/enable-tde.png
[2]:./media/security-center-enable-tde-on-sql-databases/transparent-data-encryption-blade.png
[3]: ./media/security-center-enable-tde-on-sql-databases/turn-on-tde.png
[4]: ./media/security-center-enable-tde-on-sql-databases/encrypted.png

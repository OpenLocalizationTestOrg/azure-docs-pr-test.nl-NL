---
title: aaaHow toocreate een ondersteuningsticket voor SQL Data Warehouse | Microsoft Docs
description: Hoe ticket toocreate een ondersteuningsaanvraag in Azure SQL Data Warehouse.
services: sql-data-warehouse
documentationcenter: NA
author: kevinvngo
manager: jhubbard
editor: 
ms.assetid: a91d1f53-03cb-464b-9d5b-4a9c1a194ed3
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: manage
ms.date: 10/31/2016
ms.author: kevin;barbkess
ms.openlocfilehash: 72f7eac82112fb7f1bfb05abca4ce40aeb3c828c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-support-ticket-for-sql-data-warehouse"></a><span data-ttu-id="6ade6-103">Hoe toocreate een ondersteuning voor SQL Data Warehouse-ticket</span><span class="sxs-lookup"><span data-stu-id="6ade6-103">How toocreate a support ticket for SQL Data Warehouse</span></span>
<span data-ttu-id="6ade6-104">Als u problemen ondervindt met SQL Data Warehouse, kunt u een ondersteuningsticket maken zodat ons technisch team u kan helpen.</span><span class="sxs-lookup"><span data-stu-id="6ade6-104">If you are having any issues with your SQL Data Warehouse, please create a support ticket so that our engineering team can assist you.</span></span>

> [!NOTE] 
> <span data-ttu-id="6ade6-105">Vanaf 20-12-2016 is Hallo resource statuscontrole in hello Azure-portal niet nauwkeurig.</span><span class="sxs-lookup"><span data-stu-id="6ade6-105">As of 12/20/2016, hello resource health check in hello Azure portal is not accurate.</span></span> <span data-ttu-id="6ade6-106">Er wordt gewerkt toofix dit probleem.</span><span class="sxs-lookup"><span data-stu-id="6ade6-106">We are actively working toofix this issue.</span></span> 


## <a name="create-a-support-ticket"></a><span data-ttu-id="6ade6-107">Een ondersteuningsticket maken</span><span class="sxs-lookup"><span data-stu-id="6ade6-107">Create a support ticket</span></span>
1. <span data-ttu-id="6ade6-108">Open Hallo [Azure-portal][Azure portal].</span><span class="sxs-lookup"><span data-stu-id="6ade6-108">Open hello [Azure portal][Azure portal].</span></span>
2. <span data-ttu-id="6ade6-109">Klik op Hallo beginscherm op Hallo **Help + ondersteuning** tegel.</span><span class="sxs-lookup"><span data-stu-id="6ade6-109">On hello Home screen, click hello **Help + support** tile.</span></span>
   
    ![Help en ondersteuning](./media/sql-data-warehouse-get-started-create-support-ticket/help-support.png)
3. <span data-ttu-id="6ade6-111">Klik op Hallo Help + ondersteuning blade **ondersteuningsverzoek maken**.</span><span class="sxs-lookup"><span data-stu-id="6ade6-111">On hello Help + Support blade, click **Create support request**.</span></span>
   
    ![Nieuw ondersteuningsverzoek](./media/sql-data-warehouse-get-started-create-support-ticket/create-support-request.png)
   
    <a name="request-quota-change"></a> 
4. <span data-ttu-id="6ade6-113">Selecteer Hallo **aanvraagtype**.</span><span class="sxs-lookup"><span data-stu-id="6ade6-113">Select hello **Request Type**.</span></span>
   
    ![Soort aanvraag](./media/sql-data-warehouse-get-started-create-support-ticket/request-type.png)
   
   > [!NOTE]
   > <span data-ttu-id="6ade6-115">Elke SQL-server (bijvoorbeeld myserver.database.windows.net) heeft standaard een **DTU-quotum** van 45.000.</span><span class="sxs-lookup"><span data-stu-id="6ade6-115">By default, each SQL server (e.g. myserver.database.windows.net) has a **DTU Quota** of 45,000.</span></span> <span data-ttu-id="6ade6-116">Dit quotum is gewoon een veiligheidsbeperking.</span><span class="sxs-lookup"><span data-stu-id="6ade6-116">This quota is simply a safety limit.</span></span> <span data-ttu-id="6ade6-117">U kunt uw quotum verhogen door een ondersteuningsticket maken en te selecteren *quotum* als Hallo aanvraagtype.</span><span class="sxs-lookup"><span data-stu-id="6ade6-117">You can increase your quota by creating a support ticket and selecting *Quota* as hello request type.</span></span> <span data-ttu-id="6ade6-118">uw DTU moet, Vermenigvuldig toocalculate Hallo 7.5 door Hallo totale [DWU] [ DWU] nodig.</span><span class="sxs-lookup"><span data-stu-id="6ade6-118">toocalculate your DTU needs, multiply hello 7.5 by hello total [DWU][DWU] needed.</span></span> <span data-ttu-id="6ade6-119">Bijvoorbeeld, u wilt toohost twee DW6000s op één SQL server, dan hebt u moet een DTU-quotum van 90,000 aanvragen.</span><span class="sxs-lookup"><span data-stu-id="6ade6-119">For example, you would like toohost two DW6000s on one SQL server, then you should request a DTU quota of 90,000.</span></span>  <span data-ttu-id="6ade6-120">U kunt uw huidige DTU-verbruik van SQL server-blade Hallo weergeven in Hallo-portal.</span><span class="sxs-lookup"><span data-stu-id="6ade6-120">You can view your current DTU consumption from hello SQL server blade in hello portal.</span></span> <span data-ttu-id="6ade6-121">Onderbroken en voortgezet databases meetellen voor Hallo DTU-quotum.</span><span class="sxs-lookup"><span data-stu-id="6ade6-121">Both paused and un-paused databases count toward hello DTU quota.</span></span> 
   > 
   > 
5. <span data-ttu-id="6ade6-122">Selecteer Hallo **abonnement** dat hosts Hallo database met Hallo probleem.</span><span class="sxs-lookup"><span data-stu-id="6ade6-122">Select hello **Subscription** that hosts hello database with hello problem you are reporting.</span></span>
   
    ![Abonnement](./media/sql-data-warehouse-get-started-create-support-ticket/subscription.png)
6. <span data-ttu-id="6ade6-124">Selecteer **SQL Data Warehouse** zoals Hallo Resource.</span><span class="sxs-lookup"><span data-stu-id="6ade6-124">Select **SQL Data Warehouse** as hello Resource.</span></span>
   
    ![Resource](./media/sql-data-warehouse-get-started-create-support-ticket/resource.png)
7. <span data-ttu-id="6ade6-126">Selecteer uw [Azure-ondersteuningsplan][Azure support plan].</span><span class="sxs-lookup"><span data-stu-id="6ade6-126">Select your [Azure support plan][Azure support plan].</span></span>
   
   * <span data-ttu-id="6ade6-127">Ondersteuning voor het **beheren van facturering, quota en abonnementen** is op alle ondersteuningsniveaus beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="6ade6-127">**Billing, quota and subscription management** support is available at all support levels.</span></span>
   * <span data-ttu-id="6ade6-128">**Probleemoplossing** wordt ondersteund op de ondersteuningsniveaus [Developer][Developer], [Standard][Standard], [Professional Direct][Professional Direct] en [Premier][Premier].</span><span class="sxs-lookup"><span data-stu-id="6ade6-128">**Break-fix** support is provided through [Developer][Developer], [Standard][Standard], [Professional Direct][Professional Direct] or [Premier][Premier] support.</span></span> <span data-ttu-id="6ade6-129">Schadevergoedings problemen zijn problemen die door klanten tijdens het gebruik van Azure waarbij er een redelijke verwachting is dat Microsoft veroorzaakt Hallo probleem.</span><span class="sxs-lookup"><span data-stu-id="6ade6-129">Break-fix issues are problems experienced by customers while using Azure where there is a reasonable expectation that Microsoft caused hello problem.</span></span>
   * <span data-ttu-id="6ade6-130">**Begeleiding van ontwikkelaars** en **adviesdiensten** zijn beschikbaar op Hallo [Professional Direct] [ Professional Direct] en [Premier] [ Premier] ondersteuningsniveau.</span><span class="sxs-lookup"><span data-stu-id="6ade6-130">**Developer mentoring** and **advisory services** are available at hello [Professional Direct][Professional Direct] and [Premier][Premier] support levels.</span></span> 
     
     <span data-ttu-id="6ade6-131">Als u een Premier-ondersteuningsplan hebt, kunt u ook SQL Data Warehouse rapporteren problemen op Hallo [Microsoft Premier online-portal][Microsoft Premier online portal].</span><span class="sxs-lookup"><span data-stu-id="6ade6-131">If you have a Premier support plan, you can also report SQL Data Warehouse related issues on hello [Microsoft Premier online portal][Microsoft Premier online portal].</span></span>  <span data-ttu-id="6ade6-132">Zie [Azure-ondersteuningsplannen] [ Azure support plan] toolearn meer over Hallo verschillende plannen ondersteunen, waaronder bereik, reactietijden, prijzen enzovoort.  Zie [Veelgestelde vragen over ondersteuning van Azure][Azure support FAQs] voor veelgestelde vragen over de ondersteuning van Azure.</span><span class="sxs-lookup"><span data-stu-id="6ade6-132">See [Azure support plans][Azure support plan] toolearn more about hello various support plans, including scope, response times, pricing, etc.  For frequently asked questions about Azure support, see [Azure support FAQs][Azure support FAQs].</span></span>  
     
     ![Ondersteuningsplan](./media/sql-data-warehouse-get-started-create-support-ticket/support-plan.png)
8. <span data-ttu-id="6ade6-134">Selecteer Hallo **probleemtype** en **categorie**.</span><span class="sxs-lookup"><span data-stu-id="6ade6-134">Select hello **Problem Type** and **Category**.</span></span> <span data-ttu-id="6ade6-135">In dit voorbeeld hebben we gekozen 'Tools' als Hallo probleemtype en 'Clienthulpprogramma's ' als Hallo categorie.</span><span class="sxs-lookup"><span data-stu-id="6ade6-135">In this example, we have chosen "Tools" as hello Problem type and "Client tools" as hello category.</span></span> 
   
    ![Probleemtype categorie](./media/sql-data-warehouse-get-started-create-support-ticket/problem-type-category.png)
9. <span data-ttu-id="6ade6-137">Het probleem Hallo Beschrijf en kies Hallo niveau van de impact.</span><span class="sxs-lookup"><span data-stu-id="6ade6-137">Describe hello problem and choose hello level of business impact.</span></span>
   
    ![Beschrijving van het probleem](./media/sql-data-warehouse-get-started-create-support-ticket/problem-description.png)
10. <span data-ttu-id="6ade6-139">Uw **contactgegevens** voor dit ondersteuningsticket worden vooraf ingevuld.</span><span class="sxs-lookup"><span data-stu-id="6ade6-139">Your **contact information** for this support ticket will be pre-filled.</span></span> <span data-ttu-id="6ade6-140">U kunt deze indien nodig bijwerken.</span><span class="sxs-lookup"><span data-stu-id="6ade6-140">Update this if necessary.</span></span>
    
    ![Contactgegevens](./media/sql-data-warehouse-get-started-create-support-ticket/contact-info.png)
11. <span data-ttu-id="6ade6-142">Klik op **maken** toosubmit Hallo ondersteuning aan te vragen.</span><span class="sxs-lookup"><span data-stu-id="6ade6-142">Click **Create** toosubmit hello support request.</span></span>

## <a name="monitor-a-support-ticket"></a><span data-ttu-id="6ade6-143">Een ondersteuningsticket bewaken</span><span class="sxs-lookup"><span data-stu-id="6ade6-143">Monitor a support ticket</span></span>
<span data-ttu-id="6ade6-144">Nadat u Hallo ondersteuningsaanvraag hebt ingediend, ondersteuningsteam van Azure Hallo contact met u op.</span><span class="sxs-lookup"><span data-stu-id="6ade6-144">After you have submitted hello support request, hello Azure support team will contact you.</span></span> <span data-ttu-id="6ade6-145">toocheck de aanvraagstatus en meer informatie klikt u op **ondersteuningsaanvragen beheren** op Hallo-dashboard.</span><span class="sxs-lookup"><span data-stu-id="6ade6-145">toocheck your request status and details, click **Manage support requests** on hello dashboard.</span></span>

![Status controleren](./media/sql-data-warehouse-get-started-create-support-ticket/check-status.png)

## <a name="other-resources"></a><span data-ttu-id="6ade6-147">Meer informatie</span><span class="sxs-lookup"><span data-stu-id="6ade6-147">Other Resources</span></span>
<span data-ttu-id="6ade6-148">Bovendien kunt u verbinding maken met de Hallo SQL Data Warehouse-community op [Stack Overflow] [ Stack Overflow] of op Hallo [Azure SQL Data Warehouse MSDN-forum] [ Azure SQL Data Warehouse MSDN forum].</span><span class="sxs-lookup"><span data-stu-id="6ade6-148">Additionally, you can connect with hello SQL Data Warehouse community on [Stack Overflow][Stack Overflow] or on hello [Azure SQL Data Warehouse MSDN forum][Azure SQL Data Warehouse MSDN forum].</span></span>

<!--Image references--> 

<!--Article references--> 
[DWU]: ./sql-data-warehouse-overview-what-is.md

<!--MSDN references--> 

<!--Other web references--> 
[Azure portal]: https://portal.azure.com/
[Azure support plan]: https://azure.microsoft.com/support/plans/?WT.mc_id=Support_Plan_510979/  
[Developer]: https://azure.microsoft.com/support/plans/developer/  
[Standard]: https://azure.microsoft.com/support/plans/standard/  
[Professional Direct]: https://azure.microsoft.com/support/plans/prodirect/  
[Premier]: https://azure.microsoft.com/support/plans/premier/  
[Azure support FAQs]: https://azure.microsoft.com/support/faq/
[Microsoft Premier online portal]: https://premier.microsoft.com/
[Stack Overflow]: https://stackoverflow.com/questions/tagged/azure-sqldw/
[Azure SQL Data Warehouse MSDN forum]: https://social.msdn.microsoft.com/Forums/home?forum=AzureSQLDataWarehouse/


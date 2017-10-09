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
# <a name="how-toocreate-a-support-ticket-for-sql-data-warehouse"></a>Hoe toocreate een ondersteuning voor SQL Data Warehouse-ticket
Als u problemen ondervindt met SQL Data Warehouse, kunt u een ondersteuningsticket maken zodat ons technisch team u kan helpen.

> [!NOTE] 
> Vanaf 20-12-2016 is Hallo resource statuscontrole in hello Azure-portal niet nauwkeurig. Er wordt gewerkt toofix dit probleem. 


## <a name="create-a-support-ticket"></a>Een ondersteuningsticket maken
1. Open Hallo [Azure-portal][Azure portal].
2. Klik op Hallo beginscherm op Hallo **Help + ondersteuning** tegel.
   
    ![Help en ondersteuning](./media/sql-data-warehouse-get-started-create-support-ticket/help-support.png)
3. Klik op Hallo Help + ondersteuning blade **ondersteuningsverzoek maken**.
   
    ![Nieuw ondersteuningsverzoek](./media/sql-data-warehouse-get-started-create-support-ticket/create-support-request.png)
   
    <a name="request-quota-change"></a> 
4. Selecteer Hallo **aanvraagtype**.
   
    ![Soort aanvraag](./media/sql-data-warehouse-get-started-create-support-ticket/request-type.png)
   
   > [!NOTE]
   > Elke SQL-server (bijvoorbeeld myserver.database.windows.net) heeft standaard een **DTU-quotum** van 45.000. Dit quotum is gewoon een veiligheidsbeperking. U kunt uw quotum verhogen door een ondersteuningsticket maken en te selecteren *quotum* als Hallo aanvraagtype. uw DTU moet, Vermenigvuldig toocalculate Hallo 7.5 door Hallo totale [DWU] [ DWU] nodig. Bijvoorbeeld, u wilt toohost twee DW6000s op één SQL server, dan hebt u moet een DTU-quotum van 90,000 aanvragen.  U kunt uw huidige DTU-verbruik van SQL server-blade Hallo weergeven in Hallo-portal. Onderbroken en voortgezet databases meetellen voor Hallo DTU-quotum. 
   > 
   > 
5. Selecteer Hallo **abonnement** dat hosts Hallo database met Hallo probleem.
   
    ![Abonnement](./media/sql-data-warehouse-get-started-create-support-ticket/subscription.png)
6. Selecteer **SQL Data Warehouse** zoals Hallo Resource.
   
    ![Resource](./media/sql-data-warehouse-get-started-create-support-ticket/resource.png)
7. Selecteer uw [Azure-ondersteuningsplan][Azure support plan].
   
   * Ondersteuning voor het **beheren van facturering, quota en abonnementen** is op alle ondersteuningsniveaus beschikbaar.
   * **Probleemoplossing** wordt ondersteund op de ondersteuningsniveaus [Developer][Developer], [Standard][Standard], [Professional Direct][Professional Direct] en [Premier][Premier]. Schadevergoedings problemen zijn problemen die door klanten tijdens het gebruik van Azure waarbij er een redelijke verwachting is dat Microsoft veroorzaakt Hallo probleem.
   * **Begeleiding van ontwikkelaars** en **adviesdiensten** zijn beschikbaar op Hallo [Professional Direct] [ Professional Direct] en [Premier] [ Premier] ondersteuningsniveau. 
     
     Als u een Premier-ondersteuningsplan hebt, kunt u ook SQL Data Warehouse rapporteren problemen op Hallo [Microsoft Premier online-portal][Microsoft Premier online portal].  Zie [Azure-ondersteuningsplannen] [ Azure support plan] toolearn meer over Hallo verschillende plannen ondersteunen, waaronder bereik, reactietijden, prijzen enzovoort.  Zie [Veelgestelde vragen over ondersteuning van Azure][Azure support FAQs] voor veelgestelde vragen over de ondersteuning van Azure.  
     
     ![Ondersteuningsplan](./media/sql-data-warehouse-get-started-create-support-ticket/support-plan.png)
8. Selecteer Hallo **probleemtype** en **categorie**. In dit voorbeeld hebben we gekozen 'Tools' als Hallo probleemtype en 'Clienthulpprogramma's ' als Hallo categorie. 
   
    ![Probleemtype categorie](./media/sql-data-warehouse-get-started-create-support-ticket/problem-type-category.png)
9. Het probleem Hallo Beschrijf en kies Hallo niveau van de impact.
   
    ![Beschrijving van het probleem](./media/sql-data-warehouse-get-started-create-support-ticket/problem-description.png)
10. Uw **contactgegevens** voor dit ondersteuningsticket worden vooraf ingevuld. U kunt deze indien nodig bijwerken.
    
    ![Contactgegevens](./media/sql-data-warehouse-get-started-create-support-ticket/contact-info.png)
11. Klik op **maken** toosubmit Hallo ondersteuning aan te vragen.

## <a name="monitor-a-support-ticket"></a>Een ondersteuningsticket bewaken
Nadat u Hallo ondersteuningsaanvraag hebt ingediend, ondersteuningsteam van Azure Hallo contact met u op. toocheck de aanvraagstatus en meer informatie klikt u op **ondersteuningsaanvragen beheren** op Hallo-dashboard.

![Status controleren](./media/sql-data-warehouse-get-started-create-support-ticket/check-status.png)

## <a name="other-resources"></a>Meer informatie
Bovendien kunt u verbinding maken met de Hallo SQL Data Warehouse-community op [Stack Overflow] [ Stack Overflow] of op Hallo [Azure SQL Data Warehouse MSDN-forum] [ Azure SQL Data Warehouse MSDN forum].

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


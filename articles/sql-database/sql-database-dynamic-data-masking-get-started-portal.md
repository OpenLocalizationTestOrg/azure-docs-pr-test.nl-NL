---
title: 'Azure-portal: SQL-Database dynamische-gegevensmaskering | Microsoft Docs'
description: Hoe tooget gestart met de SQL-Database dynamische-gegevensmaskering in hello Azure Portal
services: sql-database
documentationcenter: 
author: ronitr
manager: jhubbard
editor: 
ms.assetid: "2"
ms.service: sql-database
ms.custom: security
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.date: 11/22/2016
ms.author: ronitr; ronmat
ms.openlocfilehash: 5c5f74682a15d42eceb78c3ca0705401e1ac0ae7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-sql-database-dynamic-data-masking-with-hello-azure-portal"></a>Aan de slag met SQL-Database dynamische-gegevensmaskering Hello Azure Portal

Dit onderwerp leest u hoe tooimplement [dynamische gegevensmaskering](sql-database-dynamic-data-masking-get-started.md) Hello Azure-portal. U kunt ook implementeren dat maskering met behulp van dynamische gegevens [cmdlets van Azure SQL Database](https://msdn.microsoft.com/library/azure/mt574084.aspx) of Hallo [REST-API](https://msdn.microsoft.com/library/dn505719.aspx).


## <a name="set-up-dynamic-data-masking-for-your-database-using-hello-azure-portal"></a>Dynamische gegevens maskeren voor de database met de Hallo Azure Portal instellen
1. Start de Azure-Portal op Hallo [https://portal.azure.com](https://portal.azure.com).
2. Blade voor toohello-instellingen van Hallo-database waarin Hallo gevoelige gegevens die u wilt dat toomask navigeren.
3. Klik op Hallo **dynamische-Gegevensmaskering** tegel die Hallo Start **dynamische-Gegevensmaskering** configuratie blade.
   
   * U kunt ook kunt u omlaag schuiven toohello **Operations** sectie en klik op **dynamische-Gegevensmaskering**.
     
     ![Navigatiedeelvenster](./media/sql-database-dynamic-data-masking-get-started/4_ddm_settings_tile.png)<br/><br/>
4. In Hallo **dynamische-Gegevensmaskering** configuratie blade ziet u mogelijk enkele databasekolommen die Hallo aanbevelingen-engine is gemarkeerd voor maskering. In volgorde tooaccept Hallo aanbevelingen, klikt u op **masker toevoegen** voor een of meer kolommen en een masker wordt gemaakt op basis van het standaardtype Hallo voor deze kolom. Hallo gegevensmaskeringsfunctie door te klikken op Hallo maskeringsregel en bewerken van Hallo dat maskering veld indeling tooa andere indeling van uw keuze, kunt u wijzigen. Ervoor tooclick worden **opslaan** toosave uw instellingen.
   
    ![Navigatiedeelvenster](./media/sql-database-dynamic-data-masking-get-started/5_ddm_recommendations.png)<br/><br/>
5. tooadd een masker voor elke kolom in de database, boven Hallo Hallo **dynamische-Gegevensmaskering** configuratie blade Klik **masker toevoegen** tooopen hello **maskeren regel toevoegen** configuratie-blade
   
    ![Navigatiedeelvenster](./media/sql-database-dynamic-data-masking-get-started/6_ddm_add_mask.png)<br/><br/>
6. Selecteer Hallo **Schema**, **tabel** en **kolom** toodefine Hallo aangewezen veld dat wordt gemaskeerd.
7. Kies een **maskeren veldindeling** uit de lijst Hallo met gevoelige gegevens maskeren categorieën.
   
    ![Navigatiedeelvenster](./media/sql-database-dynamic-data-masking-get-started/7_ddm_mask_field_format.png)<br/><br/>        
8. Klik op **opslaan** in het maskeren van blade tooupdate Hallo regelset van de regels in Hallo dynamische-gegevensmaskering beleid maskeren Hallo van gegevens.
9. Type Hallo SQL-gebruikers of AAD-identiteiten die moeten worden uitgesloten van maskering en hebben toegang tot toohello ontmaskerd gevoelige gegevens. Dit moet een door puntkomma's gescheiden lijst met gebruikers. Houd er rekening mee dat gebruikers met beheerdersrechten altijd toegang tot toohello oorspronkelijke toegankelijk gegevens hebben.
   
    ![Navigatiedeelvenster](./media/sql-database-dynamic-data-masking-get-started/8_ddm_excluded_users.png)
   
   > [!TIP]
   > toomake deze dus toepassingslaag Hallo kunnen gevoelige gegevens voor beschermde toepassingsgebruikers weergeven, Hallo SQL-gebruiker toevoegen of AAD-identiteit Hallo toepassing tooquery Hallo database gebruikt. Het is raadzaam dat deze lijst een minimum aantal bevoegde gebruikers toominimize blootstelling van Hallo gevoelige gegevens bevatten.
   > 
   > 
10. Klik op **opslaan** in Hallo gegevens maskeren blade toosave Hallo nieuwe of bijgewerkte maskering configuratiebeleid.


## <a name="next-steps"></a>Volgende stappen

* Zie voor een overzicht van dynamische gegevensmaskering [dynamische gegevensmaskering](sql-database-dynamic-data-masking-get-started.md).
* U kunt ook implementeren dat maskering met behulp van dynamische gegevens [cmdlets van Azure SQL Database](https://msdn.microsoft.com/library/azure/mt574084.aspx) of Hallo [REST-API](https://msdn.microsoft.com/library/dn505719.aspx).

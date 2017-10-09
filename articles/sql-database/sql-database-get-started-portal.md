---
title: 'Azure Portal: een SQL-database maken | Microsoft Docs'
description: Meer informatie over hoe Hallo toocreate een logische SQL Database-server, firewallregel op serverniveau en databases die in Azure-portal. U leert ook tooquery een Azure SQL database met behulp van hello Azure-portal.
keywords: zelfstudie over sql-database, een sql-database maken
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: aeb8c4c3-6ae2-45f7-b2c3-fa13e3752eed
ms.service: sql-database
ms.custom: mvc,DBs & servers
ms.workload: data-management
ms.tgt_pltfrm: portal
ms.devlang: na
ms.topic: hero-article
ms.date: 05/30/2017
ms.author: carlrab
ms.openlocfilehash: d30352d834f2007e0b6b3eabfc3c108c61479b22
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-sql-database-in-hello-azure-portal"></a>Maken van een Azure SQL database in hello Azure-portal

Deze zelfstudie wordt uitgelegd hoe toocreate een SQL-database in Azure. Azure SQL-Database is een 'Database-as-a-Service' waarmee u toorun en schaal maximaal beschikbare SQL Server-databases in Hallo cloud aanbieden. Deze snel starten ziet u hoe tooget gestart door het maken van een SQL-database met behulp van hello Azure-portal.

Als u nog geen Azure-abonnement hebt, maakt u een [gratis account](https://azure.microsoft.com/free/) voordat u begint.

## <a name="log-in-toohello-azure-portal"></a>Meld u bij toohello Azure-portal

Meld u bij toohello [Azure-portal](https://portal.azure.com/).

## <a name="create-a-sql-database"></a>Een SQL-database maken

Een Azure SQL-database wordt gemaakt met een gedefinieerde set [reken- en opslagresources](sql-database-service-tiers.md). Hallo-database wordt gemaakt binnen een [Azure-resourcegroep](../azure-resource-manager/resource-group-overview.md) en in een [logische Azure SQL Database-server](sql-database-features.md). 

Volg deze stappen toocreate een SQL-database met voorbeeldgegevens van Hallo LT van Adventure Works. 

1. Klik op Hallo **nieuw** knop gevonden op Hallo linkerbovenhoek Hallo Azure-portal.

2. Selecteer **Databases** van Hallo **nieuw** pagina en selecteer **SQL-Database** van Hallo **Databases** pagina.

   ![database-1 maken](./media/sql-database-get-started-portal/create-database-1.png)

3. Hallo SQL-Database formulier invullen Hello volgende informatie, zoals wordt weergegeven op Hallo voorafgaand aan de installatiekopie:   

   | Instelling       | Voorgestelde waarde | Beschrijving | 
   | ------------ | ------------------ | ------------------------------------------------- | 
   | **Databasenaam** | mySampleDatabase | Zie [Database-id's](https://docs.microsoft.com/en-us/sql/relational-databases/databases/database-identifiers) voor geldige databasenamen. | 
   | **Abonnement** | Uw abonnement  | Zie [Abonnementen](https://account.windowsazure.com/Subscriptions) voor meer informatie over uw abonnementen. |
   | **Resourcegroep**  | myResourceGroup | Zie [Naming conventions](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions) (Naamgevingsconventies) voor geldige resourcegroepnamen. |
   | **Bron selecteren** | Sample (AdventureWorksLT) | Hallo AdventureWorksLT schema en de gegevens laadt in de nieuwe database |

   > [!IMPORTANT]
   > U moet de voorbeelddatabase Hallo op dit formulier selecteren omdat deze wordt gebruikt in Hallo rest van deze snel starten.
   > 

4. Onder **Server**, klikt u op **vereiste instellingen configureren** en vul Hallo formulier voor SQL server (logische server) met Hallo informatie, zoals wordt weergegeven op Hallo installatiekopie te volgen:   

   | Instelling       | Voorgestelde waarde | Beschrijving | 
   | ------------ | ------------------ | ------------------------------------------------- | 
   | **Servernaam** | Een wereldwijd unieke naam | Zie [Naming conventions](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions) (Naamgevingsconventies) voor geldige servernamen. | 
   | **Aanmeldgegevens van serverbeheerder** | Een geldige naam | Zie [Database-id's](https://docs.microsoft.com/en-us/sql/relational-databases/databases/database-identifiers) voor geldige aanmeldingsnamen. |
   | **Wachtwoord** | Een geldig wachtwoord | Uw wachtwoord moet ten minste 8 tekens bestaan en moet tekens bevatten uit drie van de volgende categorieën Hallo: hoofdletters, kleine letters, cijfers en en niet-alfanumerieke tekens bevatten. |
   | **Abonnement** | Uw abonnement | Zie [Abonnementen](https://account.windowsazure.com/Subscriptions) voor meer informatie over uw abonnementen. |
   | **Resourcegroep** | myResourceGroup | Zie [Naming conventions](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions) (Naamgevingsconventies) voor geldige resourcegroepnamen. |
   | **Locatie** | Een geldige locatie | Zie [Azure-regio's](https://azure.microsoft.com/regions/) voor informatie over regio's. |

   > [!IMPORTANT]
   > aanmeldgegevens van serverbeheerder Hallo en het wachtwoord dat u hier opgeeft, zijn vereiste toolog in toohello server en de databases verderop in dit snel starten. Onthoud of noteer deze informatie voor later gebruik. 
   >  

   ![database-server maken](./media/sql-database-get-started-portal/create-database-server.png)

5. Wanneer u Hallo formulier hebt ingevuld, klikt u op **Selecteer**.

6. Klik op **prijscategorie** toospecify Hallo prijscategorie en prestatieniveau serviceniveau voor de nieuwe database. Gebruik Hallo schuifregelaar tooselect **20 dtu's** en **250** GB aan opslagruimte. Zie [Wat is een DTU?](sql-database-what-is-a-dtu.md) voor meer informatie over DTU's.

   ![database-s1 maken](./media/sql-database-get-started-portal/create-database-s1.png)

7. Klik na het geselecteerde Hallo hoeveelheid dtu's op **toepassen**.  

8. Nu u Hallo SQL-Database formulier hebt ingevuld, klikt u op **maken** tooprovision Hallo-database. De inrichting duurt een paar minuten. 

9. Op de werkbalk Hallo **meldingen** toomonitor Hallo-implementatieproces.

   ![melding](./media/sql-database-get-started-portal/notification.png)

## <a name="create-a-server-level-firewall-rule"></a>Een serverfirewallregel maken

Hallo SQL Database-service maakt een firewall op Hallo-serverniveau waarmee wordt voorkomen dat externe toepassingen en hulpprogramma's verbinden toohello server of een database op de server Hallo tenzij een firewallregel tooopen Hallo firewall voor specifieke IP-adressen is gemaakt. Volg deze stappen toocreate een [SQL-Database firewallregel op serverniveau](sql-database-firewall-configure.md) voor uw client-IP-adressen en inschakelen van externe connectiviteit via Hallo SQL Database-firewall voor uw IP-adres. 

> [!NOTE]
> SQL Database communiceert via poort 1433. Als u tooconnect van binnen een bedrijfsnetwerk probeert, kan uitgaand verkeer via poort 1433 niet worden toegestaan door de firewall van uw netwerk. Als dit het geval is, kunt u tooyour Azure SQL Database-server kan geen verbinding tenzij uw IT-afdeling poort 1433 wordt geopend.
>

1. Nadat het Hallo-implementatie is voltooid, klikt u op **SQL-databases** van Hallo links menu en klik vervolgens op **mySampleDatabase** op Hallo **SQL-databases** pagina. Hallo overzichtspagina voor uw database wordt geopend, waarin u Hallo volledig gekwalificeerde servernaam (zoals **mynewserver20170313.database.windows.net**) en biedt opties voor verdere configuratie. Kopieer deze volledig gekwalificeerde servernaam voor later gebruik.

   > [!IMPORTANT]
   > U moet deze server volledig gekwalificeerde naam tooconnect tooyour server en de databases in de volgende snel aan de slag.
   > 

   ![servernaam](./media/sql-database-connect-query-dotnet/server-name.png) 

2. Klik op **serverfirewall ingesteld** op Hallo werkbalk zoals weergegeven in de vorige afbeelding Hallo. Hallo **Firewall-instellingen** pagina voor Hallo SQL Database-server wordt geopend. 

   ![serverfirewallregel](./media/sql-database-get-started-portal/server-firewall-rule.png) 

3. Klik op **client-IP toevoegen** op Hallo werkbalk tooadd nieuwe firewallregel tooa van uw huidige IP-adressen. Een firewallregel kan poort 1433 openen voor een afzonderlijk IP-adres of voor een aantal IP-adressen.

4. Klik op **Opslaan**. Een firewallregel op serverniveau is gemaakt voor uw huidige IP-adres poort 1433 op Hallo logische server te openen.

   ![serverfirewallregel instellen](./media/sql-database-get-started-portal/server-firewall-rule-set.png) 

4. Klik op **OK** en sluit vervolgens Hallo **Firewall-instellingen** pagina.

U kunt nu verbinding toohello SQL Database-server en de databases met SQL Server Management Studio of een ander hulpprogramma naar keuze van deze IP-adres met Hallo beheerder serveraccount eerder hebt gemaakt.

> [!IMPORTANT]
> Toegang via Hallo SQL Database-firewall is standaard ingeschakeld voor alle Azure-services. Klik op **OFF** op deze pagina toodisable voor alle Azure-services.
>

## <a name="query-hello-sql-database"></a>Query Hallo SQL-database

Nu dat u een voorbeelddatabase in Azure gemaakt hebt, gaan we Hallo ingebouwde query hulpprogramma binnen hello Azure portal tooconfirm dat u verbinding toohello database en query Hallo gegevens maken kunt te gebruiken. 

1. Hallo pagina van de SQL-Database voor uw database, klik op **extra** op Hallo-werkbalk. Hallo **extra** pagina wordt geopend.

   ![menu extra](./media/sql-database-get-started-portal/tools-menu.png) 

2. Klik op **Query-editor (preview)**, klikt u op Hallo **Preview-voorwaarden** selectievakje, en klik vervolgens op **OK**. pagina Hallo Query-editor wordt geopend.

3. Klik op **aanmelding** en selecteer vervolgens desgevraagd **SQL server-verificatie** en geef aanmeldgegevens van serverbeheerder Hallo en het wachtwoord die u eerder hebt gemaakt.

   ![aanmelding](./media/sql-database-get-started-portal/login.png) 

4. Klik op **OK** toolog in.

5. Nadat u bent geverifieerd, typt u de volgende query in de editor Querydeelvenster Hallo Hallo.

   ```sql
   SELECT TOP 20 pc.Name as CategoryName, p.name as ProductName
   FROM SalesLT.ProductCategory pc
   JOIN SalesLT.Product p
   ON pc.productcategoryid = p.productcategoryid;
   ```

6. Klik op **uitvoeren** en bekijk vervolgens de queryresultaten Hallo in Hallo **resultaten** deelvenster.

   ![resultaten queryeditor](./media/sql-database-get-started-portal/query-editor-results.png)

7. Sluit Hallo **Query-editor** pagina en Hallo **extra** pagina.

## <a name="clean-up-resources"></a>Resources opschonen

Als u deze resources niet nodig voor een andere Quick Start/zelfstudie (Zie [Vervolgstappen](#next-steps)), kunt u ze verwijderen door Hallo volgende te doen:


1. Hallo links menu in hello Azure-portal en klik op **resourcegroepen** en klik vervolgens op **myResourceGroup**. 
2. Klik op de pagina van de groep resource **verwijderen**, type **myResourceGroup** in Hallo in het tekstvak en klik vervolgens op **verwijderen**.

## <a name="next-steps"></a>Volgende stappen

Nu u een database hebt, kunt u verbinding maken met een hulpprogramma naar keuze en hiermee query's uitvoeren. Klik op de onderstaande hulpprogramma's voor meer informatie:

- [SQL Server Management Studio](sql-database-connect-query-ssms.md)
- [Visual Studio Code](sql-database-connect-query-vscode.md)
- [.NET](sql-database-connect-query-dotnet.md)
- [PHP](sql-database-connect-query-php.md)
- [Node.js](sql-database-connect-query-nodejs.md)
- [Java](sql-database-connect-query-java.md)
- [Python](sql-database-connect-query-python.md)
- [Ruby](sql-database-connect-query-ruby.md)

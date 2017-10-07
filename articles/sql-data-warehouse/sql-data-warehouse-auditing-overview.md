---
title: aaaAuditing in Azure SQL Data Warehouse | Microsoft Docs
description: Aan de slag met Azure SQL Data Warehouse controle
services: sql-data-warehouse
documentationcenter: 
author: ronortloff
manager: jhubbard
editor: 
ms.assetid: 0e6af148-b218-4b43-bb5f-907917d20330
ms.service: sql-data-warehouse
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: security
ms.date: 08/21/2017
ms.author: rortloff;barbkess
ms.openlocfilehash: 948de74fa052ef206cf1aa65c0d81f084b18cb00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="auditing-in-azure-sql-data-warehouse"></a>Controle van Azure SQL datawarehouse
> [!div class="op_single_selector"]
> * [Controle](sql-data-warehouse-auditing-overview.md)
> * [Detectie van bedreigingen](sql-data-warehouse-security-threat-detection.md)
> 
> 

SQL Data Warehouse controle kunt u toorecord gebeurtenissen in uw database tooan controlelogboek in uw Azure Storage-account. Controle, kunt u de naleving van regelgeving onderhouden, de activiteit in een database begrijpen en meer inzicht krijgen in discrepanties en afwijkingen die kunnen wijzen op problemen voor het bedrijf of vermoedelijke beveiligingsschendingen. Controle van SQL Data Warehouse ook worden geïntegreerd met Microsoft Power BI voor inzoomen rapportage en analyse.

Controleprogramma's inschakelen en vergemakkelijken van naleving toocompliance standaarden, maar niet garanderen dat. Zie voor meer informatie over Azure programma's die nalevingsscan standaarden, Hallo <a href="http://azure.microsoft.com/support/trust-center/compliance/" target="_blank">Azure Vertrouwenscentrum</a>.

* [Basisbeginselen van de database-controle]
* [Controle voor uw database instellen]
* [Controlelogboeken en -rapporten analyseren]

## <a id="subheading-1"></a>Basisbeginselen van Azure SQL Data Warehouse-Database controleren
Controle van SQL Data Warehouse-database, kunt u:

* **Behouden** een audittrail van de geselecteerde gebeurtenissen. Categorieën van database acties toobe gecontroleerd, kunt u definiëren.
* **Rapport** op database-activiteit. U kunt vooraf geconfigureerde rapporten en een dashboard tooget snel de slag met de activiteit en rapportage gebruiken.
* **Analyseren** rapporten. U kunt verdachte gebeurtenissen, ongebruikelijke activiteiten en trends vinden.

U kunt configureren om controle-instellingen voor de volgende gebeurteniscategorieën Hallo:

**Gewone SQL** en **geparametriseerde SQL** voor welke Hallo verzamelde controlelogboeken zijn geclassificeerd als  

* **Toegang toodata**
* **Wijzigingen in het schema (DDL)**
* **Gegevenswijzigingen (DML)**
* **Accounts, rollen en machtigingen (DCL)**
* **Opgeslagen Procedure**, **aanmelding** en, **transactiebeheer**.

Voor elke gebeurteniscategorie controle van **geslaagd** en **fout** bewerkingen afzonderlijk geconfigureerd.

Zie voor meer informatie over het Hallo-activiteiten en gebeurtenissen die worden gecontroleerd, Hallo <a href="http://go.microsoft.com/fwlink/?LinkId=506733" target="_blank">indeling verwijzing naar controlelogboek (doc-bestand downloaden)</a>.

Auditlogboeken worden opgeslagen in uw Azure storage-account. U kunt een bewaarperiode van audit log definiëren.

Een controlebeleid kan worden gedefinieerd voor een specifieke database of als een standaardbeleid voor de server. Een controle standaardbeleid voor server geldt tooall databases op een server die niet over een specifieke database controle beleid gedefinieerd.

Voordat u kunt instellen audit controle selectievakje in als u een ['Downlevel Client'.](sql-data-warehouse-auditing-downlevel-clients.md)

## <a id="subheading-2"></a>Controle voor uw database instellen
1. Hallo starten <a href="https://portal.azure.com" target="_blank">Azure-portal</a>.
2. Ga toohello **instellingen** blade Hallo SQL Data Warehouse gewenste tooaudit. In Hallo **instellingen** blade Selecteer **controle en detectie van bedreigingen**.
   
    ![][1]
3. Schakel vervolgens de controle door te klikken op Hallo **ON** knop.
   
    ![][3]
4. Selecteer in de Hallo configuratie blade controle, **OPSLAGGROEP** tooopen Hallo Audit logboeken opslag blade. Selecteer hello Azure storage-account waarin de logboeken worden opgeslagen en Hallo bewaarperiode. 
>[!TIP]
>Gebruik Hallo hetzelfde opslagaccount voor alle gecontroleerde databases tooget Hallo optimaal gebruik van Hallo vooraf geconfigureerde rapporten sjablonen.
   
    ![][4]
5. Klik op Hallo **OK** knop toosave Hallo opslagconfiguratie voor meer informatie.
6. Onder **LOGBOEKREGISTRATIE door GEBEURTENIS**, klikt u op **geslaagd** en **fout** toolog alle gebeurtenissen of kies een afzonderlijke gebeurteniscategorieën.
7. Als u controle voor een database configureren wilt, moet u mogelijk het Hallo-verbindingsreeks tooalter van uw client-tooensure controle van de gegevens correct wordt vastgelegd. Controleer Hallo [Server FDQN wijzigen in de verbindingsreeks Hallo](sql-data-warehouse-auditing-downlevel-clients.md) onderwerp voor downlevel-clientverbindingen.
8. Klik op **OK**.

## <a id="subheading-3"></a>Controlelogboeken en -rapporten analyseren
Controlelogboeken worden geaggregeerd in een verzameling van Store tabellen met een **SQLDBAuditLogs** voorvoegsel in hello Azure storage-account die u hebt gekozen tijdens de installatie. U kunt met een hulpprogramma zoals logboekbestanden weergeven <a href="http://azurestorageexplorer.codeplex.com/" target="_blank">Azure Opslagverkenner</a>.

Een vooraf geconfigureerde dashboard rapportsjabloon is beschikbaar als een <a href="http://go.microsoft.com/fwlink/?LinkId=403540" target="_blank">downloadbare Excel-spreadsheet</a> toohelp u logboekgegevens sneller kunt analyseren. op uw controlelogboeken toouse Hallo-sjabloon, moet u Excel 2013 of later en Power Query die u kunt downloaden <a href="http://www.microsoft.com/download/details.aspx?id=39379">hier</a>.

Hallo sjabloon fictieve voorbeeldgegevens in deze, en u kunt instellen Power Query tooimport uw controlelogboek rechtstreeks vanuit uw Azure storage-account.

## <a id="subheading-4"></a>Opslag van sessiesleutels
In productie bent u waarschijnlijk toorefresh uw opslag periodiek-codes. Bij het vernieuwen van uw sleutels, moet u toosave Hallo beleid. Hallo-proces is als volgt:

1. In Hallo controle configuratie blade (hierboven beschreven in het Hallo-installatieprogramma sectie controle) overschakelen Hallo **toegangssleutel voor opslag** van *primaire* te*secundaire* en  **Sla**.

   ![][4]
2. Ga toohello opslag configuratie blade en **genereren** hello *primaire toegangssleutel*.
3. Gaat u terug toohello controle configuratie blade switch Hallo **toegangssleutel voor opslag** van *secundaire* te*primaire* en druk op **opslaan**.
4. Ga terug toohello opslag gebruikersinterface en **genereren** hello *secundaire toegangssleutel* (als voorbereiding op Hallo volgende sleutels vernieuwen cyclus.

## <a id="subheading-5"></a>Automation (PowerShell/REST API)
U kunt ook configureren om controle in Azure SQL Data Warehouse met behulp van Hallo automatiseringsprogramma's te volgen:

* **PowerShell-cmdlets**:

   * [Get-AzureRMSqlDatabaseAuditingPolicy][101]
   * [Get-AzureRMSqlServerAuditingPolicy][102]
   * [Verwijder AzureRMSqlDatabaseAuditing][103]
   * [Verwijder AzureRMSqlServerAuditing][104]
   * [Set-AzureRMSqlDatabaseAuditingPolicy][105]
   * [Set-AzureRMSqlServerAuditingPolicy][106]
   * [Gebruik AzureRMSqlServerAuditingPolicy][107]

<!--Anchors-->
[Basisbeginselen van de database-controle]: #subheading-1
[Controle voor uw database instellen]: #subheading-2
[Controlelogboeken en -rapporten analyseren]: #subheading-3


<!--Image references-->
[1]: ./media/sql-data-warehouse-auditing-overview/sql-data-warehouse-auditing.png
[2]: ./media/sql-data-warehouse-auditing-overview/sql-data-warehouse-auditing-inherit.png
[3]: ./media/sql-data-warehouse-auditing-overview/sql-data-warehouse-auditing-enable.png
[4]: ./media/sql-data-warehouse-auditing-overview/sql-data-warehouse-auditing-storage-account.png
[5]: ./media/sql-data-warehouse-auditing-overview/sql-data-warehouse-auditing-dashboard.png


<!--Link references-->
[101]: /powershell/module/azurerm.sql/get-azurermsqldatabaseauditingpolicy
[102]: /powershell/module/azurerm.sql/Get-AzureRMSqlServerAuditingPolicy
[103]: /powershell/module/azurerm.sql/Remove-AzureRMSqlDatabaseAuditing
[104]: /powershell/module/azurerm.sql/Remove-AzureRMSqlServerAuditing
[105]: /powershell/module/azurerm.sql/Set-AzureRMSqlDatabaseAuditingPolicy
[106]: /powershell/module/azurerm.sql/Set-AzureRMSqlServerAuditingPolicy
[107]: /powershell/module/azurerm.sql/Use-AzureRMSqlServerAuditingPolicy
---
title: aaaGet de slag met Azure SQL database auditing | Microsoft Docs
description: Aan de slag met Azure SQL database auditing
services: sql-database
documentationcenter: 
author: giladm
manager: jhubbard
editor: giladm
ms.assetid: 89c2a155-c2fb-4b67-bc19-9b4e03c6d3bc
ms.service: sql-database
ms.custom: security
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/07/2017
ms.author: giladm
ms.openlocfilehash: 5494c602d702ac41992520f900c393a98cc7c989
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-sql-database-auditing"></a>Aan de slag met SQL Database Auditing
Azure SQL database auditing houdt databasegebeurtenissen bij en schrijft deze tooan controlelogboek in uw Azure storage-account. Ook controleren:

* Helpt u naleving van regelgeving onderhouden, de activiteit in een database begrijpen en meer inzicht krijgen in discrepanties en afwijkingen die kunnen wijzen op problemen voor het bedrijf of vermoedelijke beveiligingsschendingen.

* Hiermee wordt en vereenvoudigt naleving toocompliance standaarden, hoewel het geen garantie naleving. Zie voor meer informatie over Azure programma's die nalevingsscan standaarden, Hallo [Azure Vertrouwenscentrum](https://azure.microsoft.com/support/trust-center/compliance/).


## <a id="subheading-1"></a>Azure SQL-database controle-overzicht
U kunt gebruiken om SQL-database in op:


* **Behouden** een audittrail van de geselecteerde gebeurtenissen. Categorieën van database acties toobe gecontroleerd, kunt u definiëren.
* **Rapport** op database-activiteit. U kunt vooraf geconfigureerde rapporten en een dashboard tooget snel de slag met de activiteit en rapportage gebruiken.
* **Analyseren** rapporten. U kunt verdachte gebeurtenissen, ongebruikelijke activiteiten en trends vinden.

Kunt u controle voor verschillende soorten gebeurteniscategorieën, zoals uitgelegd in Hallo [controle instelt voor uw database](#subheading-2) sectie.

Auditlogboeken worden tooAzure Blob-opslag geschreven op uw Azure-abonnement.


## <a id="subheading-8"></a>Serverniveau versus databaseniveau controlebeleid definiëren

Een controlebeleid kan worden gedefinieerd voor een specifieke database of als een standaardbeleid voor server:

* Een serverbeleid geldt tooall bestaande en nieuwe databases op Hallo-server.

* Als *server blob-controle is ingeschakeld*, het *, geldt altijd toohello database* (dat wil zeggen, Hallo-database worden gecontroleerd), ongeacht Hallo database controle-instellingen.

* Inschakelen van controle op Hallo-database in toevoeging tooenabling deze op Hallo van server, blob wordt *niet* overschrijven of wijzigen van Hallo-instellingen van het Hallo server auditingfunctie voor blobs. Beide audits, naast elkaar bestaan. Met andere woorden, worden Hallo-database gecontroleerd tweemaal parallel (eenmaal door Hallo serverbeleid en eens Hallo database beleid).

   > [!NOTE]
   > Vermijd het inschakelen van de server blob controle en het blob Databasecontrole samen tenzij:
    > * U wilt dat een andere toouse *opslagaccount* of *bewaarperiode* voor een specifieke database.
    > * U wilt tooaudit gebeurtenistypen of categorieën voor een specifieke database die afwijken van de typen gebeurtenissen of categorieën worden voor de rest Hallo van Hallo-databases op Hallo-server wordt gecontroleerd. Bijvoorbeeld wellicht tabel invoegen die toobe gecontroleerd alleen voor een specifieke database moeten.
   > 
   > Anders is het raadzaam dat u alleen serverniveau auditingfunctie voor blobs en laat de eigenschap Hallo databaseniveau controle uitgeschakeld voor alle databases inschakelen.


## <a id="subheading-2"></a>Controle voor uw database instellen
Hallo volgende sectie wordt beschreven Hallo-configuratie van de controlefunctie met hello Azure-portal.

1. Ga toohello [Azure-portal](https://portal.azure.com).
2. Ga toohello **instellingen** blade Hallo SQL database/SQL server waarmee u tooaudit. In Hallo **instellingen** blade Selecteer **controle en detectie van bedreigingen**.

    <a id="auditing-screenshot"></a>![Navigatiedeelvenster][1]
3. Als u liever tooset van een server controlebeleid (die van toepassing tooall bestaande en nieuwe databases op deze server), kunt u Hallo **serverinstellingen weergeven** koppeling in de blade controle Hallo-database. U kunt vervolgens weergeven of wijzigen Hallo server controle-instellingen.

    ![Navigatiedeelvenster][2]
4. Als u liever tooenable auditingfunctie voor blobs op databaseniveau hello (in aanvulling tooor in plaats van het niveau van de server controleren), voor **controle**, selecteer **ON**, en voor **type controle** , selecteer **Blob**.

    Als server auditingfunctie voor blobs is ingeschakeld, wordt naast Hallo server blob audit Hallo database geconfigureerd audit bestaan.  

    ![Navigatiedeelvenster][3]
5. Hallo tooopen **Audit logboeken opslag** blade Selecteer **opslaggroep**. Selecteer hello Azure storage-account waarin logboeken worden opgeslagen en selecteer vervolgens de bewaarperiode hello, als u welke Hallo oude logboeken worden verwijderd. Klik vervolgens op **OK**. 
   >[!TIP] 
   >Hallo tooget optimaal gebruik van Hallo controle rapporten sjablonen, gebruik Hallo hetzelfde opslagaccount voor alle gecontroleerde databases. 

    <a id="storage-screenshot"></a>![Navigatiedeelvenster][4]
6. Als u wilt dat toocustomize Hallo gecontroleerd gebeurtenissen, kunt u dit doen via PowerShell of Hallo REST-API. Zie voor meer informatie, Hallo [Automation (PowerShell/REST-API)](#subheading-7) sectie.
7. Nadat u de controle-instellingen hebt geconfigureerd, kunt u Hallo nieuwe threat detectiefunctie inschakelen en e-mailberichten tooreceive beveiligingswaarschuwingen configureren. Wanneer u detectie van dreigingen gebruikt, ontvangt u proactieve waarschuwingen voor afwijkende databaseactiviteiten die kunnen duiden op beveiligingsdreigingen. Zie voor meer informatie [aan de slag met detectie van dreigingen](sql-database-threat-detection-get-started.md).
8. Klik op **Opslaan**.





## <a id="subheading-3"></a>Controlelogboeken en -rapporten analyseren
Controlelogboeken zijn geaggregeerd in hello Azure storage-account die u hebt gekozen tijdens de installatie. U kunt de controlelogboeken verkennen met een hulpprogramma zoals [Azure Opslagverkenner](http://storageexplorer.com/).

BLOB controle logboeken worden opgeslagen als een verzameling van blob-bestanden in een container met de naam **sqldbauditlogs**.

Zie voor meer informatie over hiërarchie van Hallo blob audit logboeken-opslagmap, blob naamconventies en logboekindeling Hallo Hallo [Audit Log indeling Blobverwijzing (.docx-bestand downloaden)](https://go.microsoft.com/fwlink/?linkid=829599).

Er zijn verschillende methoden kunt u tooview blob controlelogboeken:

* Gebruik Hallo [Azure-portal](https://portal.azure.com).  Open Hallo relevant de database. AT Hallo bovenaan Hallo-database **controle en detectie van bedreigingen** blade, klikt u op **weergave controlelogboeken**.

    ![Navigatiedeelvenster][7]

    Een **controleren records** blade wordt geopend, waarin u kunnen tooview Hallo logboeken zult.

    - U kunt specifieke datums weergeven door te klikken op **Filter** bovenaan Hallo Hallo **controleren records** blade.
    - U kunt schakelen tussen controlerecords die zijn gemaakt met een server beleid of database beleid audit.

       ![Navigatiedeelvenster][8]

* Gebruik de systeemfunctie Hallo **sys.fn_get_audit_file** (T-SQL) tooreturn Hallo audit-logboekgegevens in tabelvorm. Zie voor meer informatie over het gebruik van deze functie Hallo [sys.fn_get_audit_file documentatie](https://docs.microsoft.com/sql/relational-databases/system-functions/sys-fn-get-audit-file-transact-sql).


* Gebruik **controlebestanden samenvoegen** in SQL Server Management Studio (SSMS 17 vanaf):  
    1. Hallo SSMS menu en selecteer **bestand** > **Open** > **controlebestanden samenvoegen**.

        ![Navigatiedeelvenster][9]
    2. Hallo **controlebestanden toevoegen** dialoogvenster wordt geopend. Selecteer een van de Hallo **toevoegen** opties te kiezen of toomerge audit van een lokale bestanden schijf of ze importeren uit Azure Storage (u vereiste tooprovide worden uw Azure Storage-informatie en de accountsleutel).

    3. Nadat alle bestanden toomerge zijn toegevoegd, klikt u op **OK** toocomplete Hallo samenvoegbewerking.

    4. Hallo samengevoegde bestand geopend in SSMS, waar u kunt weergeven en analyseren, alsmede export deze tooan xel-bestand of de CSV-bestand of tooa tabel.

* Gebruik Hallo [toepassing synchroniseren](https://github.com/Microsoft/Azure-SQL-DB-auditing-OMS-integration) die we hebben gemaakt. Het wordt uitgevoerd in Azure en maakt gebruik van Operations Management Suite (OMS) Log Analytics openbare API's toopush SQL controlelogboeken in OMS. Hallo sync toepassing duwt SQL controlelogboeken in OMS Log Analytics voor consumptie via Hallo OMS Log Analytics-dashboard. 

* Power BI gebruiken. U kunt weergeven en analyseren van gegevens van de audit log in Power BI. Meer informatie over [Power BI en toegang tot een sjabloon downloaden](https://blogs.msdn.microsoft.com/azuresqldbsupport/2017/05/26/sql-azure-blob-auditing-basic-power-bi-dashboard/).

* Downloaden van de logboekbestanden van uw Azure Storage blob-container via Hallo portal of met een hulpprogramma zoals [Azure Opslagverkenner](http://storageexplorer.com/).
    * Nadat u lokaal een logboekbestand hebt gedownload, dubbelklikt u op Hallo bestand tooopen, weergeven en analyseren van Hallo Logboeken in SSMS.
    * U kunt ook meerdere bestanden tegelijkertijd via Azure Opslagverkenner downloaden. Met de rechtermuisknop op een specifieke submap (bijvoorbeeld: een submap met alle logboekbestanden voor een specifieke datum) en selecteer **opslaan als** toosave in een lokale map.

* Extra methoden:
   * Na het downloaden van verschillende bestanden (of een submap met logboekbestanden voor een volledige dag, zoals beschreven in het vorige item in deze lijst Hallo), kunt u deze samenvoegen lokaal zoals beschreven in Hallo controlebestanden van SSMS Merge-instructies eerder beschreven.

   * Weergave auditingfunctie voor blobs registreert programmatisch:

     * Gebruik Hallo [uitgebreide gebeurtenissen lezer](https://blogs.msdn.microsoft.com/extended_events/2011/07/20/introducing-the-extended-events-reader/) C#-bibliotheek.
     * [Uitgebreide gebeurtenissen bestanden query](https://sqlscope.wordpress.com/2014/11/15/reading-extended-event-files-using-client-side-tools-only/) met behulp van PowerShell.




## <a id="subheading-5"></a>Procedures voor productie
<!--hello description in this section refers toopreceding screen captures.-->

### <a id="subheading-6">Geogerepliceerde databases controle</a>
Wanneer u databases geo-replicatie gebruikt, is het mogelijk tooset van de controle op de primaire database hello, Hallo secundaire database of beide, afhankelijk van Hallo audit-type.

Volg deze instructies (Vergeet niet dat auditingfunctie voor blobs kan worden ingeschakeld in of uit alleen vanaf de primaire database Hallo controle-instellingen):

* **Primaire database**. Schakel auditingfunctie voor blobs, op Hallo-server of op Hallo-database zelf, zoals beschreven in Hallo [controle instelt voor uw database](#subheading-2) sectie.
* **Secundaire database**. Blob controlebeleid inschakelen op de primaire database hello, zoals beschreven in Hallo [controle instelt voor uw database](#subheading-2) sectie. 
   * Controle van de BLOB moet worden ingeschakeld op Hallo *primaire database zelf*, niet op Hallo-server.
   * Nadat de blob-controle is ingeschakeld op de primaire database hello, wordt deze ook ingeschakeld op de secundaire database Hallo.

     >[!IMPORTANT]
     >Standaard wordt instellingen voor de opslag voor de secundaire database Hallo Hallo zijn identiek toothose van de primaire database hello, waardoor cross-regionale verkeer. U kunt dit vermijden door in te schakelen blob controle op de secundaire server Hallo en lokale opslag configureren in de instellingen voor de opslag van Hallo secundaire server. Hallo-opslaglocatie voor de secundaire database Hallo en resultaat in elke database opslaan van de audit logboeken toolocal opslag worden hiermee overschreven.  
<br>

### <a id="subheading-6">Opslag van sessiesleutels</a>
In productie bent u waarschijnlijk toorefresh uw opslag periodiek-codes. Bij het vernieuwen van uw sleutels, moet u tooresave Hallo controlebeleid. Hallo-proces is als volgt:

1. Open Hallo **opslaggroep** blade. In Hallo **toegangssleutel voor opslag** de optie **secundaire**, en klik op **OK**. Klik vervolgens op **opslaan** bovenaan Hallo Hallo configuratie blade controle.

    ![Navigatiedeelvenster][5]
2. Ga toohello opslag configuratie blade en opnieuw genereren van de primaire toegangssleutel Hallo.

    ![Navigatiedeelvenster][6]
3. Controle van configuratie-blade toohello terug, Hallo toegangssleutel voor opslag van secundaire tooprimary overschakelen en klik op **OK**. Klik vervolgens op **opslaan** bovenaan Hallo Hallo configuratie blade controle.
4. Ga terug toohello opslag configuratie blade en de secundaire toegangssleutel opnieuw genereren hello (in voorbereiding op Hallo volgende sleutel vernieuwingscyclus).

## <a id="subheading-7"></a>Automation (PowerShell/REST API)
U kunt ook configureren om controle in Azure SQL Database met behulp van Hallo automatiseringsprogramma's te volgen:

* **PowerShell-cmdlets**:

   * [Get-AzureRMSqlDatabaseAuditingPolicy][101]
   * [Get-AzureRMSqlServerAuditingPolicy][102]
   * [Verwijder AzureRMSqlDatabaseAuditing][103]
   * [Verwijder AzureRMSqlServerAuditing][104]
   * [Set-AzureRMSqlDatabaseAuditingPolicy][105]
   * [Set-AzureRMSqlServerAuditingPolicy][106]
   * [Gebruik AzureRMSqlServerAuditingPolicy][107]

   Zie voor een scriptvoorbeeld van een, [configureren van controle en detectie van bedreigingen met behulp van PowerShell](scripts/sql-database-auditing-and-threat-detection-powershell.md).

* **REST-API - Auditingfunctie voor blobs**:

   * [Maken of bijwerken van de Database Blob controlebeleid](https://msdn.microsoft.com/library/azure/mt695939.aspx)
   * [Maken of bijwerken van de Server Blob controlebeleid](https://msdn.microsoft.com/library/azure/mt771861.aspx)
   * [Database-Blob controlebeleid ophalen](https://msdn.microsoft.com/library/azure/mt695938.aspx)
   * [Ophalen van Server Blob controlebeleid](https://msdn.microsoft.com/library/azure/mt771860.aspx)
   * [Ophalen van Server Blob die het resultaat van controle](https://msdn.microsoft.com/library/azure/mt771862.aspx)


<!--Anchors-->
[Azure SQL Database Auditing overview]: #subheading-1
[Set up auditing for your database]: #subheading-2
[Analyze audit logs and reports]: #subheading-3
[Practices for usage in production]: #subheading-5
[Storage Key Regeneration]: #subheading-6
[Automation (PowerShell / REST API)]: #subheading-7
[Blob/Table differences in Server auditing policy inheritance]: (#subheading-8)  

<!--Image references-->
[1]: ./media/sql-database-auditing-get-started/1_auditing_get_started_settings.png
[2]: ./media/sql-database-auditing-get-started/2_auditing_get_started_server_inherit.png
[3]: ./media/sql-database-auditing-get-started/3_auditing_get_started_turn_on.png
[4]: ./media/sql-database-auditing-get-started/4_auditing_get_started_storage_details.png
[5]: ./media/sql-database-auditing-get-started/5_auditing_get_started_storage_key_regeneration.png
[6]: ./media/sql-database-auditing-get-started/6_auditing_get_started_regenerate_key.png
[7]: ./media/sql-database-auditing-get-started/7_auditing_get_started_blob_view_audit_logs.png
[8]: ./media/sql-database-auditing-get-started/8_auditing_get_started_blob_audit_records.png
[9]: ./media/sql-database-auditing-get-started/9_auditing_get_started_ssms_1.png
[10]: ./media/sql-database-auditing-get-started/10_auditing_get_started_ssms_2.png

[101]: /powershell/module/azurerm.sql/get-azurermsqldatabaseauditingpolicy
[102]: /powershell/module/azurerm.sql/Get-AzureRMSqlServerAuditingPolicy
[103]: /powershell/module/azurerm.sql/Remove-AzureRMSqlDatabaseAuditing
[104]: /powershell/module/azurerm.sql/Remove-AzureRMSqlServerAuditing
[105]: /powershell/module/azurerm.sql/Set-AzureRMSqlDatabaseAuditingPolicy
[106]: /powershell/module/azurerm.sql/Set-AzureRMSqlServerAuditingPolicy
[107]: /powershell/module/azurerm.sql/Use-AzureRMSqlServerAuditingPolicy

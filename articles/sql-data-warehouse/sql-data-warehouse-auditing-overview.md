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
# <a name="auditing-in-azure-sql-data-warehouse"></a><span data-ttu-id="a59f5-103">Controle van Azure SQL datawarehouse</span><span class="sxs-lookup"><span data-stu-id="a59f5-103">Auditing in Azure SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a59f5-104">Controle</span><span class="sxs-lookup"><span data-stu-id="a59f5-104">Auditing</span></span>](sql-data-warehouse-auditing-overview.md)
> * [<span data-ttu-id="a59f5-105">Detectie van bedreigingen</span><span class="sxs-lookup"><span data-stu-id="a59f5-105">Threat detection</span></span>](sql-data-warehouse-security-threat-detection.md)
> 
> 

<span data-ttu-id="a59f5-106">SQL Data Warehouse controle kunt u toorecord gebeurtenissen in uw database tooan controlelogboek in uw Azure Storage-account.</span><span class="sxs-lookup"><span data-stu-id="a59f5-106">SQL Data Warehouse auditing allows you toorecord events in your database tooan audit log in your Azure Storage account.</span></span> <span data-ttu-id="a59f5-107">Controle, kunt u de naleving van regelgeving onderhouden, de activiteit in een database begrijpen en meer inzicht krijgen in discrepanties en afwijkingen die kunnen wijzen op problemen voor het bedrijf of vermoedelijke beveiligingsschendingen.</span><span class="sxs-lookup"><span data-stu-id="a59f5-107">Auditing can help you maintain regulatory compliance, understand  database activity, and gain insight into discrepancies and anomalies that could indicate business concerns or suspected security violations.</span></span> <span data-ttu-id="a59f5-108">Controle van SQL Data Warehouse ook worden geïntegreerd met Microsoft Power BI voor inzoomen rapportage en analyse.</span><span class="sxs-lookup"><span data-stu-id="a59f5-108">SQL Data Warehouse auditing also integrates with Microsoft Power BI for drill-down reporting and analysis.</span></span>

<span data-ttu-id="a59f5-109">Controleprogramma's inschakelen en vergemakkelijken van naleving toocompliance standaarden, maar niet garanderen dat.</span><span class="sxs-lookup"><span data-stu-id="a59f5-109">Auditing tools enable and facilitate adherence toocompliance standards but don't guarantee compliance.</span></span> <span data-ttu-id="a59f5-110">Zie voor meer informatie over Azure programma's die nalevingsscan standaarden, Hallo <a href="http://azure.microsoft.com/support/trust-center/compliance/" target="_blank">Azure Vertrouwenscentrum</a>.</span><span class="sxs-lookup"><span data-stu-id="a59f5-110">For more information about Azure programs that support standards compliance, see hello <a href="http://azure.microsoft.com/support/trust-center/compliance/" target="_blank">Azure Trust Center</a>.</span></span>

* <span data-ttu-id="a59f5-111">[Basisbeginselen van de database-controle]</span><span class="sxs-lookup"><span data-stu-id="a59f5-111">[Database Auditing basics]</span></span>
* <span data-ttu-id="a59f5-112">[Controle voor uw database instellen]</span><span class="sxs-lookup"><span data-stu-id="a59f5-112">[Set up auditing for your database]</span></span>
* <span data-ttu-id="a59f5-113">[Controlelogboeken en -rapporten analyseren]</span><span class="sxs-lookup"><span data-stu-id="a59f5-113">[Analyze audit logs and reports]</span></span>

## <span data-ttu-id="a59f5-114"><a id="subheading-1"></a>Basisbeginselen van Azure SQL Data Warehouse-Database controleren</span><span class="sxs-lookup"><span data-stu-id="a59f5-114"><a id="subheading-1"></a>Azure SQL Data Warehouse Database Auditing basics</span></span>
<span data-ttu-id="a59f5-115">Controle van SQL Data Warehouse-database, kunt u:</span><span class="sxs-lookup"><span data-stu-id="a59f5-115">SQL Data Warehouse database auditing allows you to:</span></span>

* <span data-ttu-id="a59f5-116">**Behouden** een audittrail van de geselecteerde gebeurtenissen.</span><span class="sxs-lookup"><span data-stu-id="a59f5-116">**Retain** an audit trail of selected events.</span></span> <span data-ttu-id="a59f5-117">Categorieën van database acties toobe gecontroleerd, kunt u definiëren.</span><span class="sxs-lookup"><span data-stu-id="a59f5-117">You can define categories of database actions  toobe audited.</span></span>
* <span data-ttu-id="a59f5-118">**Rapport** op database-activiteit.</span><span class="sxs-lookup"><span data-stu-id="a59f5-118">**Report** on database activity.</span></span> <span data-ttu-id="a59f5-119">U kunt vooraf geconfigureerde rapporten en een dashboard tooget snel de slag met de activiteit en rapportage gebruiken.</span><span class="sxs-lookup"><span data-stu-id="a59f5-119">You can use preconfigured reports and a dashboard tooget started quickly with activity and event reporting.</span></span>
* <span data-ttu-id="a59f5-120">**Analyseren** rapporten.</span><span class="sxs-lookup"><span data-stu-id="a59f5-120">**Analyze** reports.</span></span> <span data-ttu-id="a59f5-121">U kunt verdachte gebeurtenissen, ongebruikelijke activiteiten en trends vinden.</span><span class="sxs-lookup"><span data-stu-id="a59f5-121">You can find suspicious events, unusual activity, and trends.</span></span>

<span data-ttu-id="a59f5-122">U kunt configureren om controle-instellingen voor de volgende gebeurteniscategorieën Hallo:</span><span class="sxs-lookup"><span data-stu-id="a59f5-122">You can configure auditing for hello following event categories:</span></span>

<span data-ttu-id="a59f5-123">**Gewone SQL** en **geparametriseerde SQL** voor welke Hallo verzamelde controlelogboeken zijn geclassificeerd als</span><span class="sxs-lookup"><span data-stu-id="a59f5-123">**Plain SQL** and **Parameterized SQL** for which hello collected audit logs are classified as</span></span>  

* <span data-ttu-id="a59f5-124">**Toegang toodata**</span><span class="sxs-lookup"><span data-stu-id="a59f5-124">**Access toodata**</span></span>
* <span data-ttu-id="a59f5-125">**Wijzigingen in het schema (DDL)**</span><span class="sxs-lookup"><span data-stu-id="a59f5-125">**Schema changes (DDL)**</span></span>
* <span data-ttu-id="a59f5-126">**Gegevenswijzigingen (DML)**</span><span class="sxs-lookup"><span data-stu-id="a59f5-126">**Data changes (DML)**</span></span>
* <span data-ttu-id="a59f5-127">**Accounts, rollen en machtigingen (DCL)**</span><span class="sxs-lookup"><span data-stu-id="a59f5-127">**Accounts, roles, and permissions (DCL)**</span></span>
* <span data-ttu-id="a59f5-128">**Opgeslagen Procedure**, **aanmelding** en, **transactiebeheer**.</span><span class="sxs-lookup"><span data-stu-id="a59f5-128">**Stored Procedure**, **Login** and, **Transaction Management**.</span></span>

<span data-ttu-id="a59f5-129">Voor elke gebeurteniscategorie controle van **geslaagd** en **fout** bewerkingen afzonderlijk geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="a59f5-129">For each Event Category, Auditing of **Success** and **Failure** operations are configured separately.</span></span>

<span data-ttu-id="a59f5-130">Zie voor meer informatie over het Hallo-activiteiten en gebeurtenissen die worden gecontroleerd, Hallo <a href="http://go.microsoft.com/fwlink/?LinkId=506733" target="_blank">indeling verwijzing naar controlelogboek (doc-bestand downloaden)</a>.</span><span class="sxs-lookup"><span data-stu-id="a59f5-130">For more information about hello activities and events audited, see hello <a href="http://go.microsoft.com/fwlink/?LinkId=506733" target="_blank">Audit Log Format Reference (doc file download)</a>.</span></span>

<span data-ttu-id="a59f5-131">Auditlogboeken worden opgeslagen in uw Azure storage-account.</span><span class="sxs-lookup"><span data-stu-id="a59f5-131">Audit logs are stored in your Azure storage account.</span></span> <span data-ttu-id="a59f5-132">U kunt een bewaarperiode van audit log definiëren.</span><span class="sxs-lookup"><span data-stu-id="a59f5-132">You can define an audit log retention period.</span></span>

<span data-ttu-id="a59f5-133">Een controlebeleid kan worden gedefinieerd voor een specifieke database of als een standaardbeleid voor de server.</span><span class="sxs-lookup"><span data-stu-id="a59f5-133">An auditing policy can be defined for a specific database or as a default server policy.</span></span> <span data-ttu-id="a59f5-134">Een controle standaardbeleid voor server geldt tooall databases op een server die niet over een specifieke database controle beleid gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="a59f5-134">A default server auditing policy applies tooall databases on a server, which do not have a specific overriding database auditing policy defined.</span></span>

<span data-ttu-id="a59f5-135">Voordat u kunt instellen audit controle selectievakje in als u een ['Downlevel Client'.](sql-data-warehouse-auditing-downlevel-clients.md)</span><span class="sxs-lookup"><span data-stu-id="a59f5-135">Before setting up audit auditing check if you are using a ["Downlevel Client."](sql-data-warehouse-auditing-downlevel-clients.md)</span></span>

## <span data-ttu-id="a59f5-136"><a id="subheading-2"></a>Controle voor uw database instellen</span><span class="sxs-lookup"><span data-stu-id="a59f5-136"><a id="subheading-2"></a>Set up auditing for your database</span></span>
1. <span data-ttu-id="a59f5-137">Hallo starten <a href="https://portal.azure.com" target="_blank">Azure-portal</a>.</span><span class="sxs-lookup"><span data-stu-id="a59f5-137">Launch hello <a href="https://portal.azure.com" target="_blank">Azure portal</a>.</span></span>
2. <span data-ttu-id="a59f5-138">Ga toohello **instellingen** blade Hallo SQL Data Warehouse gewenste tooaudit.</span><span class="sxs-lookup"><span data-stu-id="a59f5-138">Go toohello **Settings** blade of hello SQL Data Warehouse you want tooaudit.</span></span> <span data-ttu-id="a59f5-139">In Hallo **instellingen** blade Selecteer **controle en detectie van bedreigingen**.</span><span class="sxs-lookup"><span data-stu-id="a59f5-139">In hello **Settings** blade, select **Auditing & Threat detection**.</span></span>
   
    ![][1]
3. <span data-ttu-id="a59f5-140">Schakel vervolgens de controle door te klikken op Hallo **ON** knop.</span><span class="sxs-lookup"><span data-stu-id="a59f5-140">Next, enable auditing by clicking hello **ON** button.</span></span>
   
    ![][3]
4. <span data-ttu-id="a59f5-141">Selecteer in de Hallo configuratie blade controle, **OPSLAGGROEP** tooopen Hallo Audit logboeken opslag blade.</span><span class="sxs-lookup"><span data-stu-id="a59f5-141">In hello auditing configuration blade, select **STORAGE DETAILS** tooopen hello Audit Logs Storage blade.</span></span> <span data-ttu-id="a59f5-142">Selecteer hello Azure storage-account waarin de logboeken worden opgeslagen en Hallo bewaarperiode.</span><span class="sxs-lookup"><span data-stu-id="a59f5-142">Select hello Azure storage account where logs will be saved and, hello retention period.</span></span> 
>[!TIP]
><span data-ttu-id="a59f5-143">Gebruik Hallo hetzelfde opslagaccount voor alle gecontroleerde databases tooget Hallo optimaal gebruik van Hallo vooraf geconfigureerde rapporten sjablonen.</span><span class="sxs-lookup"><span data-stu-id="a59f5-143">Use hello same storage account for all audited databases tooget hello most out of hello pre-configured reports templates.</span></span>
   
    ![][4]
5. <span data-ttu-id="a59f5-144">Klik op Hallo **OK** knop toosave Hallo opslagconfiguratie voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="a59f5-144">Click hello **OK** button toosave hello storage details configuration.</span></span>
6. <span data-ttu-id="a59f5-145">Onder **LOGBOEKREGISTRATIE door GEBEURTENIS**, klikt u op **geslaagd** en **fout** toolog alle gebeurtenissen of kies een afzonderlijke gebeurteniscategorieën.</span><span class="sxs-lookup"><span data-stu-id="a59f5-145">Under **LOGGING BY EVENT**, click **SUCCESS** and **FAILURE** toolog all events, or choose individual event categories.</span></span>
7. <span data-ttu-id="a59f5-146">Als u controle voor een database configureren wilt, moet u mogelijk het Hallo-verbindingsreeks tooalter van uw client-tooensure controle van de gegevens correct wordt vastgelegd.</span><span class="sxs-lookup"><span data-stu-id="a59f5-146">If you are configuring Auditing for a database, you may need tooalter hello connection string of your client tooensure data auditing is correctly captured.</span></span> <span data-ttu-id="a59f5-147">Controleer Hallo [Server FDQN wijzigen in de verbindingsreeks Hallo](sql-data-warehouse-auditing-downlevel-clients.md) onderwerp voor downlevel-clientverbindingen.</span><span class="sxs-lookup"><span data-stu-id="a59f5-147">Check hello [Modify Server FDQN in hello connection string](sql-data-warehouse-auditing-downlevel-clients.md) topic for downlevel client connections.</span></span>
8. <span data-ttu-id="a59f5-148">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="a59f5-148">Click **OK**.</span></span>

## <span data-ttu-id="a59f5-149"><a id="subheading-3"></a>Controlelogboeken en -rapporten analyseren</span><span class="sxs-lookup"><span data-stu-id="a59f5-149"><a id="subheading-3"></a>Analyze audit logs and reports</span></span>
<span data-ttu-id="a59f5-150">Controlelogboeken worden geaggregeerd in een verzameling van Store tabellen met een **SQLDBAuditLogs** voorvoegsel in hello Azure storage-account die u hebt gekozen tijdens de installatie.</span><span class="sxs-lookup"><span data-stu-id="a59f5-150">Audit logs are aggregated in a collection of Store Tables with a **SQLDBAuditLogs** prefix in hello Azure storage account you chose during setup.</span></span> <span data-ttu-id="a59f5-151">U kunt met een hulpprogramma zoals logboekbestanden weergeven <a href="http://azurestorageexplorer.codeplex.com/" target="_blank">Azure Opslagverkenner</a>.</span><span class="sxs-lookup"><span data-stu-id="a59f5-151">You can view log files using a tool such as <a href="http://azurestorageexplorer.codeplex.com/" target="_blank">Azure Storage Explorer</a>.</span></span>

<span data-ttu-id="a59f5-152">Een vooraf geconfigureerde dashboard rapportsjabloon is beschikbaar als een <a href="http://go.microsoft.com/fwlink/?LinkId=403540" target="_blank">downloadbare Excel-spreadsheet</a> toohelp u logboekgegevens sneller kunt analyseren.</span><span class="sxs-lookup"><span data-stu-id="a59f5-152">A preconfigured dashboard report template is available as a <a href="http://go.microsoft.com/fwlink/?LinkId=403540" target="_blank">downloadable Excel spreadsheet</a> toohelp you quickly analyze log data.</span></span> <span data-ttu-id="a59f5-153">op uw controlelogboeken toouse Hallo-sjabloon, moet u Excel 2013 of later en Power Query die u kunt downloaden <a href="http://www.microsoft.com/download/details.aspx?id=39379">hier</a>.</span><span class="sxs-lookup"><span data-stu-id="a59f5-153">toouse hello template on your audit logs, you need Excel 2013 or later and Power Query, which you can download <a href="http://www.microsoft.com/download/details.aspx?id=39379">here</a>.</span></span>

<span data-ttu-id="a59f5-154">Hallo sjabloon fictieve voorbeeldgegevens in deze, en u kunt instellen Power Query tooimport uw controlelogboek rechtstreeks vanuit uw Azure storage-account.</span><span class="sxs-lookup"><span data-stu-id="a59f5-154">hello template has fictional sample data in it, and you can set up Power Query tooimport your audit log directly from your Azure storage account.</span></span>

## <span data-ttu-id="a59f5-155"><a id="subheading-4"></a>Opslag van sessiesleutels</span><span class="sxs-lookup"><span data-stu-id="a59f5-155"><a id="subheading-4"></a>Storage key regeneration</span></span>
<span data-ttu-id="a59f5-156">In productie bent u waarschijnlijk toorefresh uw opslag periodiek-codes.</span><span class="sxs-lookup"><span data-stu-id="a59f5-156">In production, you are likely toorefresh your storage keys periodically.</span></span> <span data-ttu-id="a59f5-157">Bij het vernieuwen van uw sleutels, moet u toosave Hallo beleid.</span><span class="sxs-lookup"><span data-stu-id="a59f5-157">When refreshing your keys, you need toosave hello policy.</span></span> <span data-ttu-id="a59f5-158">Hallo-proces is als volgt:</span><span class="sxs-lookup"><span data-stu-id="a59f5-158">hello process is as follows:</span></span>

1. <span data-ttu-id="a59f5-159">In Hallo controle configuratie blade (hierboven beschreven in het Hallo-installatieprogramma sectie controle) overschakelen Hallo **toegangssleutel voor opslag** van *primaire* te*secundaire* en  **Sla**.</span><span class="sxs-lookup"><span data-stu-id="a59f5-159">In hello auditing configuration blade (described above in hello setup auditing section) switch hello **Storage Access Key** from *Primary* too*Secondary* and **SAVE**.</span></span>

   ![][4]
2. <span data-ttu-id="a59f5-160">Ga toohello opslag configuratie blade en **genereren** hello *primaire toegangssleutel*.</span><span class="sxs-lookup"><span data-stu-id="a59f5-160">Go toohello storage configuration blade and **regenerate** hello *Primary Access Key*.</span></span>
3. <span data-ttu-id="a59f5-161">Gaat u terug toohello controle configuratie blade switch Hallo **toegangssleutel voor opslag** van *secundaire* te*primaire* en druk op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="a59f5-161">Go back toohello auditing configuration blade, switch hello **Storage Access Key** from *Secondary* too*Primary* and press **SAVE**.</span></span>
4. <span data-ttu-id="a59f5-162">Ga terug toohello opslag gebruikersinterface en **genereren** hello *secundaire toegangssleutel* (als voorbereiding op Hallo volgende sleutels vernieuwen cyclus.</span><span class="sxs-lookup"><span data-stu-id="a59f5-162">Go back toohello storage UI and **regenerate** hello *Secondary Access Key* (as preparation for hello next keys refresh cycle.</span></span>

## <span data-ttu-id="a59f5-163"><a id="subheading-5"></a>Automation (PowerShell/REST API)</span><span class="sxs-lookup"><span data-stu-id="a59f5-163"><a id="subheading-5"></a>Automation (PowerShell/REST API)</span></span>
<span data-ttu-id="a59f5-164">U kunt ook configureren om controle in Azure SQL Data Warehouse met behulp van Hallo automatiseringsprogramma's te volgen:</span><span class="sxs-lookup"><span data-stu-id="a59f5-164">You can also configure auditing in Azure SQL Data Warehouse by using hello following automation tools:</span></span>

* <span data-ttu-id="a59f5-165">**PowerShell-cmdlets**:</span><span class="sxs-lookup"><span data-stu-id="a59f5-165">**PowerShell cmdlets**:</span></span>

   * <span data-ttu-id="a59f5-166">[Get-AzureRMSqlDatabaseAuditingPolicy][101]</span><span class="sxs-lookup"><span data-stu-id="a59f5-166">[Get-AzureRMSqlDatabaseAuditingPolicy][101]</span></span>
   * <span data-ttu-id="a59f5-167">[Get-AzureRMSqlServerAuditingPolicy][102]</span><span class="sxs-lookup"><span data-stu-id="a59f5-167">[Get-AzureRMSqlServerAuditingPolicy][102]</span></span>
   * <span data-ttu-id="a59f5-168">[Verwijder AzureRMSqlDatabaseAuditing][103]</span><span class="sxs-lookup"><span data-stu-id="a59f5-168">[Remove-AzureRMSqlDatabaseAuditing][103]</span></span>
   * <span data-ttu-id="a59f5-169">[Verwijder AzureRMSqlServerAuditing][104]</span><span class="sxs-lookup"><span data-stu-id="a59f5-169">[Remove-AzureRMSqlServerAuditing][104]</span></span>
   * <span data-ttu-id="a59f5-170">[Set-AzureRMSqlDatabaseAuditingPolicy][105]</span><span class="sxs-lookup"><span data-stu-id="a59f5-170">[Set-AzureRMSqlDatabaseAuditingPolicy][105]</span></span>
   * <span data-ttu-id="a59f5-171">[Set-AzureRMSqlServerAuditingPolicy][106]</span><span class="sxs-lookup"><span data-stu-id="a59f5-171">[Set-AzureRMSqlServerAuditingPolicy][106]</span></span>
   * <span data-ttu-id="a59f5-172">[Gebruik AzureRMSqlServerAuditingPolicy][107]</span><span class="sxs-lookup"><span data-stu-id="a59f5-172">[Use-AzureRMSqlServerAuditingPolicy][107]</span></span>

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
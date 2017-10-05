---
title: Controle van Azure SQL datawarehouse | Microsoft Docs
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
ms.openlocfilehash: f851c82ebeaa647f663d499a4d327c3479e36121
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="auditing-in-azure-sql-data-warehouse"></a><span data-ttu-id="ac83f-103">Controle van Azure SQL datawarehouse</span><span class="sxs-lookup"><span data-stu-id="ac83f-103">Auditing in Azure SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ac83f-104">Controle</span><span class="sxs-lookup"><span data-stu-id="ac83f-104">Auditing</span></span>](sql-data-warehouse-auditing-overview.md)
> * [<span data-ttu-id="ac83f-105">Detectie van bedreigingen</span><span class="sxs-lookup"><span data-stu-id="ac83f-105">Threat detection</span></span>](sql-data-warehouse-security-threat-detection.md)
> 
> 

<span data-ttu-id="ac83f-106">Controle van SQL Data Warehouse kunt u record gebeurtenissen in de database naar een auditlogboek in uw Azure Storage-account worden geregistreerd.</span><span class="sxs-lookup"><span data-stu-id="ac83f-106">SQL Data Warehouse auditing allows you to record events in your database to an audit log in your Azure Storage account.</span></span> <span data-ttu-id="ac83f-107">Controle, kunt u de naleving van regelgeving onderhouden, de activiteit in een database begrijpen en meer inzicht krijgen in discrepanties en afwijkingen die kunnen wijzen op problemen voor het bedrijf of vermoedelijke beveiligingsschendingen.</span><span class="sxs-lookup"><span data-stu-id="ac83f-107">Auditing can help you maintain regulatory compliance, understand  database activity, and gain insight into discrepancies and anomalies that could indicate business concerns or suspected security violations.</span></span> <span data-ttu-id="ac83f-108">Controle van SQL Data Warehouse ook worden geïntegreerd met Microsoft Power BI voor inzoomen rapportage en analyse.</span><span class="sxs-lookup"><span data-stu-id="ac83f-108">SQL Data Warehouse auditing also integrates with Microsoft Power BI for drill-down reporting and analysis.</span></span>

<span data-ttu-id="ac83f-109">Controleprogramma's inschakelen en voldoen aan de nalevingsstandaards vergemakkelijken, maar niet garanderen dat.</span><span class="sxs-lookup"><span data-stu-id="ac83f-109">Auditing tools enable and facilitate adherence to compliance standards but don't guarantee compliance.</span></span> <span data-ttu-id="ac83f-110">Zie voor meer informatie over Azure programma's die nalevingsscan standaarden, de <a href="http://azure.microsoft.com/support/trust-center/compliance/" target="_blank">Azure Vertrouwenscentrum</a>.</span><span class="sxs-lookup"><span data-stu-id="ac83f-110">For more information about Azure programs that support standards compliance, see the <a href="http://azure.microsoft.com/support/trust-center/compliance/" target="_blank">Azure Trust Center</a>.</span></span>

* <span data-ttu-id="ac83f-111">[Basisbeginselen van de database-controle]</span><span class="sxs-lookup"><span data-stu-id="ac83f-111">[Database Auditing basics]</span></span>
* <span data-ttu-id="ac83f-112">[Controle voor uw database instellen]</span><span class="sxs-lookup"><span data-stu-id="ac83f-112">[Set up auditing for your database]</span></span>
* <span data-ttu-id="ac83f-113">[Controlelogboeken en -rapporten analyseren]</span><span class="sxs-lookup"><span data-stu-id="ac83f-113">[Analyze audit logs and reports]</span></span>

## <span data-ttu-id="ac83f-114"><a id="subheading-1"></a>Basisbeginselen van Azure SQL Data Warehouse-Database controleren</span><span class="sxs-lookup"><span data-stu-id="ac83f-114"><a id="subheading-1"></a>Azure SQL Data Warehouse Database Auditing basics</span></span>
<span data-ttu-id="ac83f-115">Controle van SQL Data Warehouse-database, kunt u:</span><span class="sxs-lookup"><span data-stu-id="ac83f-115">SQL Data Warehouse database auditing allows you to:</span></span>

* <span data-ttu-id="ac83f-116">**Behouden** een audittrail van de geselecteerde gebeurtenissen.</span><span class="sxs-lookup"><span data-stu-id="ac83f-116">**Retain** an audit trail of selected events.</span></span> <span data-ttu-id="ac83f-117">Categorieën van databaseacties moeten worden gecontroleerd, kunt u definiëren.</span><span class="sxs-lookup"><span data-stu-id="ac83f-117">You can define categories of database actions  to be audited.</span></span>
* <span data-ttu-id="ac83f-118">**Rapport** op database-activiteit.</span><span class="sxs-lookup"><span data-stu-id="ac83f-118">**Report** on database activity.</span></span> <span data-ttu-id="ac83f-119">U kunt vooraf geconfigureerde rapporten en een dashboard snel aan de slag met de activiteit en rapportage.</span><span class="sxs-lookup"><span data-stu-id="ac83f-119">You can use preconfigured reports and a dashboard to get started quickly with activity and event reporting.</span></span>
* <span data-ttu-id="ac83f-120">**Analyseren** rapporten.</span><span class="sxs-lookup"><span data-stu-id="ac83f-120">**Analyze** reports.</span></span> <span data-ttu-id="ac83f-121">U kunt verdachte gebeurtenissen, ongebruikelijke activiteiten en trends vinden.</span><span class="sxs-lookup"><span data-stu-id="ac83f-121">You can find suspicious events, unusual activity, and trends.</span></span>

<span data-ttu-id="ac83f-122">U kunt configureren om controle-instellingen voor de volgende gebeurteniscategorieën:</span><span class="sxs-lookup"><span data-stu-id="ac83f-122">You can configure auditing for the following event categories:</span></span>

<span data-ttu-id="ac83f-123">**Gewone SQL** en **geparametriseerde SQL** waarvoor de controlelogboeken van de verzamelde zijn geclassificeerd als</span><span class="sxs-lookup"><span data-stu-id="ac83f-123">**Plain SQL** and **Parameterized SQL** for which the collected audit logs are classified as</span></span>  

* <span data-ttu-id="ac83f-124">**Toegang tot gegevens**</span><span class="sxs-lookup"><span data-stu-id="ac83f-124">**Access to data**</span></span>
* <span data-ttu-id="ac83f-125">**Wijzigingen in het schema (DDL)**</span><span class="sxs-lookup"><span data-stu-id="ac83f-125">**Schema changes (DDL)**</span></span>
* <span data-ttu-id="ac83f-126">**Gegevenswijzigingen (DML)**</span><span class="sxs-lookup"><span data-stu-id="ac83f-126">**Data changes (DML)**</span></span>
* <span data-ttu-id="ac83f-127">**Accounts, rollen en machtigingen (DCL)**</span><span class="sxs-lookup"><span data-stu-id="ac83f-127">**Accounts, roles, and permissions (DCL)**</span></span>
* <span data-ttu-id="ac83f-128">**Opgeslagen Procedure**, **aanmelding** en, **transactiebeheer**.</span><span class="sxs-lookup"><span data-stu-id="ac83f-128">**Stored Procedure**, **Login** and, **Transaction Management**.</span></span>

<span data-ttu-id="ac83f-129">Voor elke gebeurteniscategorie controle van **geslaagd** en **fout** bewerkingen afzonderlijk geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="ac83f-129">For each Event Category, Auditing of **Success** and **Failure** operations are configured separately.</span></span>

<span data-ttu-id="ac83f-130">Zie voor meer informatie over de activiteiten en gebeurtenissen die worden gecontroleerd, de <a href="http://go.microsoft.com/fwlink/?LinkId=506733" target="_blank">indeling verwijzing naar controlelogboek (doc-bestand downloaden)</a>.</span><span class="sxs-lookup"><span data-stu-id="ac83f-130">For more information about the activities and events audited, see the <a href="http://go.microsoft.com/fwlink/?LinkId=506733" target="_blank">Audit Log Format Reference (doc file download)</a>.</span></span>

<span data-ttu-id="ac83f-131">Auditlogboeken worden opgeslagen in uw Azure storage-account.</span><span class="sxs-lookup"><span data-stu-id="ac83f-131">Audit logs are stored in your Azure storage account.</span></span> <span data-ttu-id="ac83f-132">U kunt een bewaarperiode van audit log definiëren.</span><span class="sxs-lookup"><span data-stu-id="ac83f-132">You can define an audit log retention period.</span></span>

<span data-ttu-id="ac83f-133">Een controlebeleid kan worden gedefinieerd voor een specifieke database of als een standaardbeleid voor de server.</span><span class="sxs-lookup"><span data-stu-id="ac83f-133">An auditing policy can be defined for a specific database or as a default server policy.</span></span> <span data-ttu-id="ac83f-134">Een controle standaardbeleid voor server geldt voor alle databases op een server die niet over een specifieke database controle beleid gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="ac83f-134">A default server auditing policy applies to all databases on a server, which do not have a specific overriding database auditing policy defined.</span></span>

<span data-ttu-id="ac83f-135">Voordat u kunt instellen audit controle selectievakje in als u een ['Downlevel Client'.](sql-data-warehouse-auditing-downlevel-clients.md)</span><span class="sxs-lookup"><span data-stu-id="ac83f-135">Before setting up audit auditing check if you are using a ["Downlevel Client."](sql-data-warehouse-auditing-downlevel-clients.md)</span></span>

## <span data-ttu-id="ac83f-136"><a id="subheading-2"></a>Controle voor uw database instellen</span><span class="sxs-lookup"><span data-stu-id="ac83f-136"><a id="subheading-2"></a>Set up auditing for your database</span></span>
1. <span data-ttu-id="ac83f-137">Start de <a href="https://portal.azure.com" target="_blank">Azure-portal</a>.</span><span class="sxs-lookup"><span data-stu-id="ac83f-137">Launch the <a href="https://portal.azure.com" target="_blank">Azure portal</a>.</span></span>
2. <span data-ttu-id="ac83f-138">Ga naar de **instellingen** blade van de SQL Data Warehouse die u wilt controleren.</span><span class="sxs-lookup"><span data-stu-id="ac83f-138">Go to the **Settings** blade of the SQL Data Warehouse you want to audit.</span></span> <span data-ttu-id="ac83f-139">In de **instellingen** blade Selecteer **controle en detectie van bedreigingen**.</span><span class="sxs-lookup"><span data-stu-id="ac83f-139">In the **Settings** blade, select **Auditing & Threat detection**.</span></span>
   
    ![][1]
3. <span data-ttu-id="ac83f-140">Schakel vervolgens de controle door te klikken op de **ON** knop.</span><span class="sxs-lookup"><span data-stu-id="ac83f-140">Next, enable auditing by clicking the **ON** button.</span></span>
   
    ![][3]
4. <span data-ttu-id="ac83f-141">Selecteer in de blade controle configuratie **OPSLAGGROEP** om de blade Audit logboeken opslag te openen.</span><span class="sxs-lookup"><span data-stu-id="ac83f-141">In the auditing configuration blade, select **STORAGE DETAILS** to open the Audit Logs Storage blade.</span></span> <span data-ttu-id="ac83f-142">Selecteer de Azure-opslagaccount waarin de logboeken worden opgeslagen en de bewaarperiode.</span><span class="sxs-lookup"><span data-stu-id="ac83f-142">Select the Azure storage account where logs will be saved and, the retention period.</span></span> 
>[!TIP]
><span data-ttu-id="ac83f-143">Gebruik hetzelfde opslagaccount voor alle gecontroleerde databases optimaal buiten de vooraf geconfigureerde rapporten sjablonen.</span><span class="sxs-lookup"><span data-stu-id="ac83f-143">Use the same storage account for all audited databases to get the most out of the pre-configured reports templates.</span></span>
   
    ![][4]
5. <span data-ttu-id="ac83f-144">Klik op de **OK** om op te slaan de opslagconfiguratie voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="ac83f-144">Click the **OK** button to save the storage details configuration.</span></span>
6. <span data-ttu-id="ac83f-145">Onder **LOGBOEKREGISTRATIE door GEBEURTENIS**, klikt u op **geslaagd** en **fout** met alle gebeurtenissen of kies een afzonderlijke gebeurteniscategorieën.</span><span class="sxs-lookup"><span data-stu-id="ac83f-145">Under **LOGGING BY EVENT**, click **SUCCESS** and **FAILURE** to log all events, or choose individual event categories.</span></span>
7. <span data-ttu-id="ac83f-146">Als u controle voor een database configureren wilt, moet u mogelijk voor het wijzigen van de verbindingsreeks van de client om controle van de gegevens correct wordt vastgelegd.</span><span class="sxs-lookup"><span data-stu-id="ac83f-146">If you are configuring Auditing for a database, you may need to alter the connection string of your client to ensure data auditing is correctly captured.</span></span> <span data-ttu-id="ac83f-147">Controleer de [Server FDQN wijzigen in de verbindingsreeks](sql-data-warehouse-auditing-downlevel-clients.md) onderwerp voor downlevel-clientverbindingen.</span><span class="sxs-lookup"><span data-stu-id="ac83f-147">Check the [Modify Server FDQN in the connection string](sql-data-warehouse-auditing-downlevel-clients.md) topic for downlevel client connections.</span></span>
8. <span data-ttu-id="ac83f-148">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="ac83f-148">Click **OK**.</span></span>

## <span data-ttu-id="ac83f-149"><a id="subheading-3"></a>Controlelogboeken en -rapporten analyseren</span><span class="sxs-lookup"><span data-stu-id="ac83f-149"><a id="subheading-3"></a>Analyze audit logs and reports</span></span>
<span data-ttu-id="ac83f-150">Controlelogboeken worden geaggregeerd in een verzameling van Store tabellen met een **SQLDBAuditLogs** -voorvoegsel op in de Azure storage-account dat u hebt gekozen tijdens de installatie.</span><span class="sxs-lookup"><span data-stu-id="ac83f-150">Audit logs are aggregated in a collection of Store Tables with a **SQLDBAuditLogs** prefix in the Azure storage account you chose during setup.</span></span> <span data-ttu-id="ac83f-151">U kunt met een hulpprogramma zoals logboekbestanden weergeven <a href="http://azurestorageexplorer.codeplex.com/" target="_blank">Azure Opslagverkenner</a>.</span><span class="sxs-lookup"><span data-stu-id="ac83f-151">You can view log files using a tool such as <a href="http://azurestorageexplorer.codeplex.com/" target="_blank">Azure Storage Explorer</a>.</span></span>

<span data-ttu-id="ac83f-152">Een vooraf geconfigureerde dashboard rapportsjabloon is beschikbaar als een <a href="http://go.microsoft.com/fwlink/?LinkId=403540" target="_blank">downloadbare Excel-spreadsheet</a> waarmee u kunt snel analyseren logboekgegevens.</span><span class="sxs-lookup"><span data-stu-id="ac83f-152">A preconfigured dashboard report template is available as a <a href="http://go.microsoft.com/fwlink/?LinkId=403540" target="_blank">downloadable Excel spreadsheet</a> to help you quickly analyze log data.</span></span> <span data-ttu-id="ac83f-153">De sjabloon wilt gebruiken op uw controlelogboeken, moet u Excel 2013 of later en Power Query die u kunt downloaden <a href="http://www.microsoft.com/download/details.aspx?id=39379">hier</a>.</span><span class="sxs-lookup"><span data-stu-id="ac83f-153">To use the template on your audit logs, you need Excel 2013 or later and Power Query, which you can download <a href="http://www.microsoft.com/download/details.aspx?id=39379">here</a>.</span></span>

<span data-ttu-id="ac83f-154">De sjabloon met fictieve voorbeeldgegevens erin en kunt u Power Query voor het importeren van het controlelogboek rechtstreeks vanuit uw Azure storage-account instellen.</span><span class="sxs-lookup"><span data-stu-id="ac83f-154">The template has fictional sample data in it, and you can set up Power Query to import your audit log directly from your Azure storage account.</span></span>

## <span data-ttu-id="ac83f-155"><a id="subheading-4"></a>Opslag van sessiesleutels</span><span class="sxs-lookup"><span data-stu-id="ac83f-155"><a id="subheading-4"></a>Storage key regeneration</span></span>
<span data-ttu-id="ac83f-156">In productie bent u waarschijnlijk uw opslagsleutels periodiek te vernieuwen.</span><span class="sxs-lookup"><span data-stu-id="ac83f-156">In production, you are likely to refresh your storage keys periodically.</span></span> <span data-ttu-id="ac83f-157">Wanneer uw sleutels vernieuwen, moet u het beleid op te slaan.</span><span class="sxs-lookup"><span data-stu-id="ac83f-157">When refreshing your keys, you need to save the policy.</span></span> <span data-ttu-id="ac83f-158">Het proces is als volgt:</span><span class="sxs-lookup"><span data-stu-id="ac83f-158">The process is as follows:</span></span>

1. <span data-ttu-id="ac83f-159">Overschakelen op de controle configuratie blade (hierboven beschreven in de sectie controle-instellingen) de **toegangssleutel voor opslag** van *primaire* naar *secundaire* en **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="ac83f-159">In the auditing configuration blade (described above in the setup auditing section) switch the **Storage Access Key** from *Primary* to *Secondary* and **SAVE**.</span></span>

   ![][4]
2. <span data-ttu-id="ac83f-160">Ga naar de blade van de configuratie van opslag en **genereren** de *primaire toegangssleutel*.</span><span class="sxs-lookup"><span data-stu-id="ac83f-160">Go to the storage configuration blade and **regenerate** the *Primary Access Key*.</span></span>
3. <span data-ttu-id="ac83f-161">Ga terug naar de blade met controle configuratie, schakelt u de **toegangssleutel voor opslag** van *secundaire* naar *primaire* en druk op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="ac83f-161">Go back to the auditing configuration blade, switch the **Storage Access Key** from *Secondary* to *Primary* and press **SAVE**.</span></span>
4. <span data-ttu-id="ac83f-162">Ga terug naar de opslag gebruikersinterface en **genereren** de *secundaire toegangssleutel* (als voorbereiding op de volgende sleutels vernieuwen cyclus.</span><span class="sxs-lookup"><span data-stu-id="ac83f-162">Go back to the storage UI and **regenerate** the *Secondary Access Key* (as preparation for the next keys refresh cycle.</span></span>

## <span data-ttu-id="ac83f-163"><a id="subheading-5"></a>Automation (PowerShell/REST API)</span><span class="sxs-lookup"><span data-stu-id="ac83f-163"><a id="subheading-5"></a>Automation (PowerShell/REST API)</span></span>
<span data-ttu-id="ac83f-164">U kunt ook configureren om controle in Azure SQL Data Warehouse met behulp van de volgende automation-hulpprogramma's:</span><span class="sxs-lookup"><span data-stu-id="ac83f-164">You can also configure auditing in Azure SQL Data Warehouse by using the following automation tools:</span></span>

* <span data-ttu-id="ac83f-165">**PowerShell-cmdlets**:</span><span class="sxs-lookup"><span data-stu-id="ac83f-165">**PowerShell cmdlets**:</span></span>

   * <span data-ttu-id="ac83f-166">[Get-AzureRMSqlDatabaseAuditingPolicy][101]</span><span class="sxs-lookup"><span data-stu-id="ac83f-166">[Get-AzureRMSqlDatabaseAuditingPolicy][101]</span></span>
   * <span data-ttu-id="ac83f-167">[Get-AzureRMSqlServerAuditingPolicy][102]</span><span class="sxs-lookup"><span data-stu-id="ac83f-167">[Get-AzureRMSqlServerAuditingPolicy][102]</span></span>
   * <span data-ttu-id="ac83f-168">[Verwijder AzureRMSqlDatabaseAuditing][103]</span><span class="sxs-lookup"><span data-stu-id="ac83f-168">[Remove-AzureRMSqlDatabaseAuditing][103]</span></span>
   * <span data-ttu-id="ac83f-169">[Verwijder AzureRMSqlServerAuditing][104]</span><span class="sxs-lookup"><span data-stu-id="ac83f-169">[Remove-AzureRMSqlServerAuditing][104]</span></span>
   * <span data-ttu-id="ac83f-170">[Set-AzureRMSqlDatabaseAuditingPolicy][105]</span><span class="sxs-lookup"><span data-stu-id="ac83f-170">[Set-AzureRMSqlDatabaseAuditingPolicy][105]</span></span>
   * <span data-ttu-id="ac83f-171">[Set-AzureRMSqlServerAuditingPolicy][106]</span><span class="sxs-lookup"><span data-stu-id="ac83f-171">[Set-AzureRMSqlServerAuditingPolicy][106]</span></span>
   * <span data-ttu-id="ac83f-172">[Gebruik AzureRMSqlServerAuditingPolicy][107]</span><span class="sxs-lookup"><span data-stu-id="ac83f-172">[Use-AzureRMSqlServerAuditingPolicy][107]</span></span>

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
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
# <a name="get-started-with-sql-database-auditing"></a><span data-ttu-id="8bb7d-103">Aan de slag met SQL Database Auditing</span><span class="sxs-lookup"><span data-stu-id="8bb7d-103">Get started with SQL database auditing</span></span>
<span data-ttu-id="8bb7d-104">Azure SQL database auditing houdt databasegebeurtenissen bij en schrijft deze tooan controlelogboek in uw Azure storage-account.</span><span class="sxs-lookup"><span data-stu-id="8bb7d-104">Azure SQL database auditing tracks database events and writes them tooan audit log in your Azure storage account.</span></span> <span data-ttu-id="8bb7d-105">Ook controleren:</span><span class="sxs-lookup"><span data-stu-id="8bb7d-105">Auditing also:</span></span>

* <span data-ttu-id="8bb7d-106">Helpt u naleving van regelgeving onderhouden, de activiteit in een database begrijpen en meer inzicht krijgen in discrepanties en afwijkingen die kunnen wijzen op problemen voor het bedrijf of vermoedelijke beveiligingsschendingen.</span><span class="sxs-lookup"><span data-stu-id="8bb7d-106">Helps you maintain regulatory compliance, understand database activity, and gain insight into discrepancies and anomalies that could indicate business concerns or suspected security violations.</span></span>

* <span data-ttu-id="8bb7d-107">Hiermee wordt en vereenvoudigt naleving toocompliance standaarden, hoewel het geen garantie naleving.</span><span class="sxs-lookup"><span data-stu-id="8bb7d-107">Enables and facilitates adherence toocompliance standards, although it doesn't guarantee compliance.</span></span> <span data-ttu-id="8bb7d-108">Zie voor meer informatie over Azure programma's die nalevingsscan standaarden, Hallo [Azure Vertrouwenscentrum](https://azure.microsoft.com/support/trust-center/compliance/).</span><span class="sxs-lookup"><span data-stu-id="8bb7d-108">For more information about Azure programs that support standards compliance, see hello [Azure Trust Center](https://azure.microsoft.com/support/trust-center/compliance/).</span></span>


## <span data-ttu-id="8bb7d-109"><a id="subheading-1"></a>Azure SQL-database controle-overzicht</span><span class="sxs-lookup"><span data-stu-id="8bb7d-109"><a id="subheading-1"></a>Azure SQL database auditing overview</span></span>
<span data-ttu-id="8bb7d-110">U kunt gebruiken om SQL-database in op:</span><span class="sxs-lookup"><span data-stu-id="8bb7d-110">You can use SQL database auditing to:</span></span>


* <span data-ttu-id="8bb7d-111">**Behouden** een audittrail van de geselecteerde gebeurtenissen.</span><span class="sxs-lookup"><span data-stu-id="8bb7d-111">**Retain** an audit trail of selected events.</span></span> <span data-ttu-id="8bb7d-112">Categorieën van database acties toobe gecontroleerd, kunt u definiëren.</span><span class="sxs-lookup"><span data-stu-id="8bb7d-112">You can define categories of database actions toobe audited.</span></span>
* <span data-ttu-id="8bb7d-113">**Rapport** op database-activiteit.</span><span class="sxs-lookup"><span data-stu-id="8bb7d-113">**Report** on database activity.</span></span> <span data-ttu-id="8bb7d-114">U kunt vooraf geconfigureerde rapporten en een dashboard tooget snel de slag met de activiteit en rapportage gebruiken.</span><span class="sxs-lookup"><span data-stu-id="8bb7d-114">You can use preconfigured reports and a dashboard tooget started quickly with activity and event reporting.</span></span>
* <span data-ttu-id="8bb7d-115">**Analyseren** rapporten.</span><span class="sxs-lookup"><span data-stu-id="8bb7d-115">**Analyze** reports.</span></span> <span data-ttu-id="8bb7d-116">U kunt verdachte gebeurtenissen, ongebruikelijke activiteiten en trends vinden.</span><span class="sxs-lookup"><span data-stu-id="8bb7d-116">You can find suspicious events, unusual activity, and trends.</span></span>

<span data-ttu-id="8bb7d-117">Kunt u controle voor verschillende soorten gebeurteniscategorieën, zoals uitgelegd in Hallo [controle instelt voor uw database](#subheading-2) sectie.</span><span class="sxs-lookup"><span data-stu-id="8bb7d-117">You can configure auditing for different types of event categories, as explained in hello [Set up auditing for your database](#subheading-2) section.</span></span>

<span data-ttu-id="8bb7d-118">Auditlogboeken worden tooAzure Blob-opslag geschreven op uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="8bb7d-118">Audit logs are written tooAzure Blob storage on your Azure subscription.</span></span>


## <span data-ttu-id="8bb7d-119"><a id="subheading-8"></a>Serverniveau versus databaseniveau controlebeleid definiëren</span><span class="sxs-lookup"><span data-stu-id="8bb7d-119"><a id="subheading-8"></a>Define server-level vs. database-level auditing policy</span></span>

<span data-ttu-id="8bb7d-120">Een controlebeleid kan worden gedefinieerd voor een specifieke database of als een standaardbeleid voor server:</span><span class="sxs-lookup"><span data-stu-id="8bb7d-120">An auditing policy can be defined for a specific database or as a default server policy:</span></span>

* <span data-ttu-id="8bb7d-121">Een serverbeleid geldt tooall bestaande en nieuwe databases op Hallo-server.</span><span class="sxs-lookup"><span data-stu-id="8bb7d-121">A server policy applies tooall existing and newly created databases on hello server.</span></span>

* <span data-ttu-id="8bb7d-122">Als *server blob-controle is ingeschakeld*, het *, geldt altijd toohello database* (dat wil zeggen, Hallo-database worden gecontroleerd), ongeacht Hallo database controle-instellingen.</span><span class="sxs-lookup"><span data-stu-id="8bb7d-122">If *server blob auditing is enabled*, it *always applies toohello database* (that is, hello database will be audited), regardless of hello database auditing settings.</span></span>

* <span data-ttu-id="8bb7d-123">Inschakelen van controle op Hallo-database in toevoeging tooenabling deze op Hallo van server, blob wordt *niet* overschrijven of wijzigen van Hallo-instellingen van het Hallo server auditingfunctie voor blobs.</span><span class="sxs-lookup"><span data-stu-id="8bb7d-123">Enabling blob auditing on hello database, in addition tooenabling it on hello server, will *not* override or change any of hello settings of hello server blob auditing.</span></span> <span data-ttu-id="8bb7d-124">Beide audits, naast elkaar bestaan.</span><span class="sxs-lookup"><span data-stu-id="8bb7d-124">Both audits will exist side by side.</span></span> <span data-ttu-id="8bb7d-125">Met andere woorden, worden Hallo-database gecontroleerd tweemaal parallel (eenmaal door Hallo serverbeleid en eens Hallo database beleid).</span><span class="sxs-lookup"><span data-stu-id="8bb7d-125">In other words, hello database will be audited twice in parallel (once by hello server policy and once by hello database policy).</span></span>

   > [!NOTE]
   > <span data-ttu-id="8bb7d-126">Vermijd het inschakelen van de server blob controle en het blob Databasecontrole samen tenzij:</span><span class="sxs-lookup"><span data-stu-id="8bb7d-126">You should avoid enabling both server blob auditing and database blob auditing together, unless:</span></span>
    > * <span data-ttu-id="8bb7d-127">U wilt dat een andere toouse *opslagaccount* of *bewaarperiode* voor een specifieke database.</span><span class="sxs-lookup"><span data-stu-id="8bb7d-127">You want toouse a different *storage account* or *retention period* for a specific database.</span></span>
    > * <span data-ttu-id="8bb7d-128">U wilt tooaudit gebeurtenistypen of categorieën voor een specifieke database die afwijken van de typen gebeurtenissen of categorieën worden voor de rest Hallo van Hallo-databases op Hallo-server wordt gecontroleerd.</span><span class="sxs-lookup"><span data-stu-id="8bb7d-128">You want tooaudit event types or categories for a specific database that differ from event types or categories that are being audited for hello rest of hello databases on hello server.</span></span> <span data-ttu-id="8bb7d-129">Bijvoorbeeld wellicht tabel invoegen die toobe gecontroleerd alleen voor een specifieke database moeten.</span><span class="sxs-lookup"><span data-stu-id="8bb7d-129">For example, you might have table inserts that need toobe audited only for a specific database.</span></span>
   > 
   > <span data-ttu-id="8bb7d-130">Anders is het raadzaam dat u alleen serverniveau auditingfunctie voor blobs en laat de eigenschap Hallo databaseniveau controle uitgeschakeld voor alle databases inschakelen.</span><span class="sxs-lookup"><span data-stu-id="8bb7d-130">Otherwise, we recommended that you enable only server-level blob auditing and leave hello database-level auditing disabled for all databases.</span></span>


## <span data-ttu-id="8bb7d-131"><a id="subheading-2"></a>Controle voor uw database instellen</span><span class="sxs-lookup"><span data-stu-id="8bb7d-131"><a id="subheading-2"></a>Set up auditing for your database</span></span>
<span data-ttu-id="8bb7d-132">Hallo volgende sectie wordt beschreven Hallo-configuratie van de controlefunctie met hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="8bb7d-132">hello following section describes hello configuration of auditing using hello Azure portal.</span></span>

1. <span data-ttu-id="8bb7d-133">Ga toohello [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="8bb7d-133">Go toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="8bb7d-134">Ga toohello **instellingen** blade Hallo SQL database/SQL server waarmee u tooaudit.</span><span class="sxs-lookup"><span data-stu-id="8bb7d-134">Go toohello **Settings** blade of hello SQL database/SQL server you want tooaudit.</span></span> <span data-ttu-id="8bb7d-135">In Hallo **instellingen** blade Selecteer **controle en detectie van bedreigingen**.</span><span class="sxs-lookup"><span data-stu-id="8bb7d-135">In hello **Settings** blade, select **Auditing & Threat detection**.</span></span>

    <span data-ttu-id="8bb7d-136"><a id="auditing-screenshot"></a>![Navigatiedeelvenster][1]</span><span class="sxs-lookup"><span data-stu-id="8bb7d-136"><a id="auditing-screenshot"></a> ![Navigation pane][1]</span></span>
3. <span data-ttu-id="8bb7d-137">Als u liever tooset van een server controlebeleid (die van toepassing tooall bestaande en nieuwe databases op deze server), kunt u Hallo **serverinstellingen weergeven** koppeling in de blade controle Hallo-database.</span><span class="sxs-lookup"><span data-stu-id="8bb7d-137">If you prefer tooset up a server auditing policy (which will apply tooall existing and newly created databases on this server), you can select hello **View server settings** link in hello database auditing blade.</span></span> <span data-ttu-id="8bb7d-138">U kunt vervolgens weergeven of wijzigen Hallo server controle-instellingen.</span><span class="sxs-lookup"><span data-stu-id="8bb7d-138">You can then view or modify hello server auditing settings.</span></span>

    ![Navigatiedeelvenster][2]
4. <span data-ttu-id="8bb7d-140">Als u liever tooenable auditingfunctie voor blobs op databaseniveau hello (in aanvulling tooor in plaats van het niveau van de server controleren), voor **controle**, selecteer **ON**, en voor **type controle** , selecteer **Blob**.</span><span class="sxs-lookup"><span data-stu-id="8bb7d-140">If you prefer tooenable blob auditing on hello database level (in addition tooor instead of server-level auditing), for **Auditing**, select **ON**, and for **Auditing type**, select  **Blob**.</span></span>

    <span data-ttu-id="8bb7d-141">Als server auditingfunctie voor blobs is ingeschakeld, wordt naast Hallo server blob audit Hallo database geconfigureerd audit bestaan.</span><span class="sxs-lookup"><span data-stu-id="8bb7d-141">If server blob auditing is enabled, hello database-configured audit will exist side by side with hello server blob audit.</span></span>  

    ![Navigatiedeelvenster][3]
5. <span data-ttu-id="8bb7d-143">Hallo tooopen **Audit logboeken opslag** blade Selecteer **opslaggroep**.</span><span class="sxs-lookup"><span data-stu-id="8bb7d-143">tooopen hello **Audit Logs Storage** blade, select **Storage Details**.</span></span> <span data-ttu-id="8bb7d-144">Selecteer hello Azure storage-account waarin logboeken worden opgeslagen en selecteer vervolgens de bewaarperiode hello, als u welke Hallo oude logboeken worden verwijderd.</span><span class="sxs-lookup"><span data-stu-id="8bb7d-144">Select hello Azure storage account where logs will be saved, and then select hello retention period, after which hello old logs will be deleted.</span></span> <span data-ttu-id="8bb7d-145">Klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="8bb7d-145">Then click **OK**.</span></span> 
   >[!TIP] 
   ><span data-ttu-id="8bb7d-146">Hallo tooget optimaal gebruik van Hallo controle rapporten sjablonen, gebruik Hallo hetzelfde opslagaccount voor alle gecontroleerde databases.</span><span class="sxs-lookup"><span data-stu-id="8bb7d-146">tooget hello most out of hello auditing reports templates, use hello same storage account for all audited databases.</span></span> 

    <span data-ttu-id="8bb7d-147"><a id="storage-screenshot"></a>![Navigatiedeelvenster][4]</span><span class="sxs-lookup"><span data-stu-id="8bb7d-147"><a id="storage-screenshot"></a> ![Navigation pane][4]</span></span>
6. <span data-ttu-id="8bb7d-148">Als u wilt dat toocustomize Hallo gecontroleerd gebeurtenissen, kunt u dit doen via PowerShell of Hallo REST-API.</span><span class="sxs-lookup"><span data-stu-id="8bb7d-148">If you want toocustomize hello audited events, you can do this via PowerShell or hello REST API.</span></span> <span data-ttu-id="8bb7d-149">Zie voor meer informatie, Hallo [Automation (PowerShell/REST-API)](#subheading-7) sectie.</span><span class="sxs-lookup"><span data-stu-id="8bb7d-149">For more details, see hello [Automation (PowerShell/REST API)](#subheading-7) section.</span></span>
7. <span data-ttu-id="8bb7d-150">Nadat u de controle-instellingen hebt geconfigureerd, kunt u Hallo nieuwe threat detectiefunctie inschakelen en e-mailberichten tooreceive beveiligingswaarschuwingen configureren.</span><span class="sxs-lookup"><span data-stu-id="8bb7d-150">After you've configured your auditing settings, you can turn on hello new threat detection feature and configure emails tooreceive security alerts.</span></span> <span data-ttu-id="8bb7d-151">Wanneer u detectie van dreigingen gebruikt, ontvangt u proactieve waarschuwingen voor afwijkende databaseactiviteiten die kunnen duiden op beveiligingsdreigingen.</span><span class="sxs-lookup"><span data-stu-id="8bb7d-151">When you use threat detection, you receive proactive alerts on anomalous database activities that can indicate potential security threats.</span></span> <span data-ttu-id="8bb7d-152">Zie voor meer informatie [aan de slag met detectie van dreigingen](sql-database-threat-detection-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="8bb7d-152">For more details, see [Getting started with threat detection](sql-database-threat-detection-get-started.md).</span></span>
8. <span data-ttu-id="8bb7d-153">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="8bb7d-153">Click **Save**.</span></span>





## <span data-ttu-id="8bb7d-154"><a id="subheading-3"></a>Controlelogboeken en -rapporten analyseren</span><span class="sxs-lookup"><span data-stu-id="8bb7d-154"><a id="subheading-3"></a>Analyze audit logs and reports</span></span>
<span data-ttu-id="8bb7d-155">Controlelogboeken zijn geaggregeerd in hello Azure storage-account die u hebt gekozen tijdens de installatie.</span><span class="sxs-lookup"><span data-stu-id="8bb7d-155">Audit logs are aggregated in hello Azure storage account you chose during setup.</span></span> <span data-ttu-id="8bb7d-156">U kunt de controlelogboeken verkennen met een hulpprogramma zoals [Azure Opslagverkenner](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="8bb7d-156">You can explore audit logs by using a tool such as [Azure Storage Explorer](http://storageexplorer.com/).</span></span>

<span data-ttu-id="8bb7d-157">BLOB controle logboeken worden opgeslagen als een verzameling van blob-bestanden in een container met de naam **sqldbauditlogs**.</span><span class="sxs-lookup"><span data-stu-id="8bb7d-157">Blob auditing logs are saved as a collection of blob files within a container named **sqldbauditlogs**.</span></span>

<span data-ttu-id="8bb7d-158">Zie voor meer informatie over hiërarchie van Hallo blob audit logboeken-opslagmap, blob naamconventies en logboekindeling Hallo Hallo [Audit Log indeling Blobverwijzing (.docx-bestand downloaden)](https://go.microsoft.com/fwlink/?linkid=829599).</span><span class="sxs-lookup"><span data-stu-id="8bb7d-158">For further details about hello hierarchy of hello blob audit logs storage folder, blob naming conventions, and log format, see hello [Blob Audit Log Format Reference (.docx file download)](https://go.microsoft.com/fwlink/?linkid=829599).</span></span>

<span data-ttu-id="8bb7d-159">Er zijn verschillende methoden kunt u tooview blob controlelogboeken:</span><span class="sxs-lookup"><span data-stu-id="8bb7d-159">There are several methods you can use tooview blob auditing logs:</span></span>

* <span data-ttu-id="8bb7d-160">Gebruik Hallo [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="8bb7d-160">Use hello [Azure portal](https://portal.azure.com).</span></span>  <span data-ttu-id="8bb7d-161">Open Hallo relevant de database.</span><span class="sxs-lookup"><span data-stu-id="8bb7d-161">Open hello relevant database.</span></span> <span data-ttu-id="8bb7d-162">AT Hallo bovenaan Hallo-database **controle en detectie van bedreigingen** blade, klikt u op **weergave controlelogboeken**.</span><span class="sxs-lookup"><span data-stu-id="8bb7d-162">At hello top of hello database's **Auditing & Threat detection** blade, click **View audit logs**.</span></span>

    ![Navigatiedeelvenster][7]

    <span data-ttu-id="8bb7d-164">Een **controleren records** blade wordt geopend, waarin u kunnen tooview Hallo logboeken zult.</span><span class="sxs-lookup"><span data-stu-id="8bb7d-164">An **Audit records** blade opens, from which you'll be able tooview hello logs.</span></span>

    - <span data-ttu-id="8bb7d-165">U kunt specifieke datums weergeven door te klikken op **Filter** bovenaan Hallo Hallo **controleren records** blade.</span><span class="sxs-lookup"><span data-stu-id="8bb7d-165">You can view specific dates by clicking **Filter** at hello top of hello **Audit records** blade.</span></span>
    - <span data-ttu-id="8bb7d-166">U kunt schakelen tussen controlerecords die zijn gemaakt met een server beleid of database beleid audit.</span><span class="sxs-lookup"><span data-stu-id="8bb7d-166">You can switch between audit records that were created by a server policy or database policy audit.</span></span>

       ![Navigatiedeelvenster][8]

* <span data-ttu-id="8bb7d-168">Gebruik de systeemfunctie Hallo **sys.fn_get_audit_file** (T-SQL) tooreturn Hallo audit-logboekgegevens in tabelvorm.</span><span class="sxs-lookup"><span data-stu-id="8bb7d-168">Use hello system function **sys.fn_get_audit_file** (T-SQL) tooreturn hello audit log data in tabular format.</span></span> <span data-ttu-id="8bb7d-169">Zie voor meer informatie over het gebruik van deze functie Hallo [sys.fn_get_audit_file documentatie](https://docs.microsoft.com/sql/relational-databases/system-functions/sys-fn-get-audit-file-transact-sql).</span><span class="sxs-lookup"><span data-stu-id="8bb7d-169">For more information on using this function, see hello [sys.fn_get_audit_file documentation](https://docs.microsoft.com/sql/relational-databases/system-functions/sys-fn-get-audit-file-transact-sql).</span></span>


* <span data-ttu-id="8bb7d-170">Gebruik **controlebestanden samenvoegen** in SQL Server Management Studio (SSMS 17 vanaf):</span><span class="sxs-lookup"><span data-stu-id="8bb7d-170">Use **Merge Audit Files** in SQL Server Management Studio (starting with SSMS 17):</span></span>  
    1. <span data-ttu-id="8bb7d-171">Hallo SSMS menu en selecteer **bestand** > **Open** > **controlebestanden samenvoegen**.</span><span class="sxs-lookup"><span data-stu-id="8bb7d-171">From hello SSMS menu, select **File** > **Open** > **Merge Audit Files**.</span></span>

        ![Navigatiedeelvenster][9]
    2. <span data-ttu-id="8bb7d-173">Hallo **controlebestanden toevoegen** dialoogvenster wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="8bb7d-173">hello **Add Audit Files** dialog box opens.</span></span> <span data-ttu-id="8bb7d-174">Selecteer een van de Hallo **toevoegen** opties te kiezen of toomerge audit van een lokale bestanden schijf of ze importeren uit Azure Storage (u vereiste tooprovide worden uw Azure Storage-informatie en de accountsleutel).</span><span class="sxs-lookup"><span data-stu-id="8bb7d-174">Select one of hello **Add** options to choose whether toomerge audit files from a local disk or import them from Azure Storage (you will be required tooprovide your Azure Storage details and account key).</span></span>

    3. <span data-ttu-id="8bb7d-175">Nadat alle bestanden toomerge zijn toegevoegd, klikt u op **OK** toocomplete Hallo samenvoegbewerking.</span><span class="sxs-lookup"><span data-stu-id="8bb7d-175">After all files toomerge have been added, click **OK** toocomplete hello merge operation.</span></span>

    4. <span data-ttu-id="8bb7d-176">Hallo samengevoegde bestand geopend in SSMS, waar u kunt weergeven en analyseren, alsmede export deze tooan xel-bestand of de CSV-bestand of tooa tabel.</span><span class="sxs-lookup"><span data-stu-id="8bb7d-176">hello merged file opens in SSMS, where you can view and analyze it, as well as export it tooan XEL or CSV file or tooa table.</span></span>

* <span data-ttu-id="8bb7d-177">Gebruik Hallo [toepassing synchroniseren](https://github.com/Microsoft/Azure-SQL-DB-auditing-OMS-integration) die we hebben gemaakt.</span><span class="sxs-lookup"><span data-stu-id="8bb7d-177">Use hello [sync application](https://github.com/Microsoft/Azure-SQL-DB-auditing-OMS-integration) that we have created.</span></span> <span data-ttu-id="8bb7d-178">Het wordt uitgevoerd in Azure en maakt gebruik van Operations Management Suite (OMS) Log Analytics openbare API's toopush SQL controlelogboeken in OMS.</span><span class="sxs-lookup"><span data-stu-id="8bb7d-178">It runs in Azure and utilizes Operations Management Suite (OMS) Log Analytics public APIs toopush SQL audit logs into OMS.</span></span> <span data-ttu-id="8bb7d-179">Hallo sync toepassing duwt SQL controlelogboeken in OMS Log Analytics voor consumptie via Hallo OMS Log Analytics-dashboard.</span><span class="sxs-lookup"><span data-stu-id="8bb7d-179">hello sync application pushes SQL audit logs into OMS Log Analytics for consumption via hello OMS Log Analytics dashboard.</span></span> 

* <span data-ttu-id="8bb7d-180">Power BI gebruiken.</span><span class="sxs-lookup"><span data-stu-id="8bb7d-180">Use Power BI.</span></span> <span data-ttu-id="8bb7d-181">U kunt weergeven en analyseren van gegevens van de audit log in Power BI.</span><span class="sxs-lookup"><span data-stu-id="8bb7d-181">You can view and analyze audit log data in Power BI.</span></span> <span data-ttu-id="8bb7d-182">Meer informatie over [Power BI en toegang tot een sjabloon downloaden](https://blogs.msdn.microsoft.com/azuresqldbsupport/2017/05/26/sql-azure-blob-auditing-basic-power-bi-dashboard/).</span><span class="sxs-lookup"><span data-stu-id="8bb7d-182">Learn more about [Power BI, and access a downloadable template](https://blogs.msdn.microsoft.com/azuresqldbsupport/2017/05/26/sql-azure-blob-auditing-basic-power-bi-dashboard/).</span></span>

* <span data-ttu-id="8bb7d-183">Downloaden van de logboekbestanden van uw Azure Storage blob-container via Hallo portal of met een hulpprogramma zoals [Azure Opslagverkenner](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="8bb7d-183">Download log files from your Azure Storage blob container via hello portal or by using a tool such as [Azure Storage Explorer](http://storageexplorer.com/).</span></span>
    * <span data-ttu-id="8bb7d-184">Nadat u lokaal een logboekbestand hebt gedownload, dubbelklikt u op Hallo bestand tooopen, weergeven en analyseren van Hallo Logboeken in SSMS.</span><span class="sxs-lookup"><span data-stu-id="8bb7d-184">After you have downloaded a log file locally, you can double-click hello file tooopen, view, and analyze hello logs in SSMS.</span></span>
    * <span data-ttu-id="8bb7d-185">U kunt ook meerdere bestanden tegelijkertijd via Azure Opslagverkenner downloaden.</span><span class="sxs-lookup"><span data-stu-id="8bb7d-185">You can also download multiple files simultaneously via Azure Storage Explorer.</span></span> <span data-ttu-id="8bb7d-186">Met de rechtermuisknop op een specifieke submap (bijvoorbeeld: een submap met alle logboekbestanden voor een specifieke datum) en selecteer **opslaan als** toosave in een lokale map.</span><span class="sxs-lookup"><span data-stu-id="8bb7d-186">Right-click a specific subfolder (for example, a subfolder that includes all log files for a specific date) and select **Save as** toosave in a local folder.</span></span>

* <span data-ttu-id="8bb7d-187">Extra methoden:</span><span class="sxs-lookup"><span data-stu-id="8bb7d-187">Additional methods:</span></span>
   * <span data-ttu-id="8bb7d-188">Na het downloaden van verschillende bestanden (of een submap met logboekbestanden voor een volledige dag, zoals beschreven in het vorige item in deze lijst Hallo), kunt u deze samenvoegen lokaal zoals beschreven in Hallo controlebestanden van SSMS Merge-instructies eerder beschreven.</span><span class="sxs-lookup"><span data-stu-id="8bb7d-188">After downloading several files (or a subfolder that includes log files for an entire day, as described in hello previous item in this list), you can merge them locally as described in hello SSMS Merge Audit Files instructions described earlier.</span></span>

   * <span data-ttu-id="8bb7d-189">Weergave auditingfunctie voor blobs registreert programmatisch:</span><span class="sxs-lookup"><span data-stu-id="8bb7d-189">View blob auditing logs programmatically:</span></span>

     * <span data-ttu-id="8bb7d-190">Gebruik Hallo [uitgebreide gebeurtenissen lezer](https://blogs.msdn.microsoft.com/extended_events/2011/07/20/introducing-the-extended-events-reader/) C#-bibliotheek.</span><span class="sxs-lookup"><span data-stu-id="8bb7d-190">Use hello [Extended Events Reader](https://blogs.msdn.microsoft.com/extended_events/2011/07/20/introducing-the-extended-events-reader/) C# library.</span></span>
     * <span data-ttu-id="8bb7d-191">[Uitgebreide gebeurtenissen bestanden query](https://sqlscope.wordpress.com/2014/11/15/reading-extended-event-files-using-client-side-tools-only/) met behulp van PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8bb7d-191">[Query Extended Events Files](https://sqlscope.wordpress.com/2014/11/15/reading-extended-event-files-using-client-side-tools-only/) by using PowerShell.</span></span>




## <span data-ttu-id="8bb7d-192"><a id="subheading-5"></a>Procedures voor productie</span><span class="sxs-lookup"><span data-stu-id="8bb7d-192"><a id="subheading-5"></a>Production practices</span></span>
<!--hello description in this section refers toopreceding screen captures.-->

### <span data-ttu-id="8bb7d-193"><a id="subheading-6">Geogerepliceerde databases controle</a></span><span class="sxs-lookup"><span data-stu-id="8bb7d-193"><a id="subheading-6">Auditing geo-replicated databases</a></span></span>
<span data-ttu-id="8bb7d-194">Wanneer u databases geo-replicatie gebruikt, is het mogelijk tooset van de controle op de primaire database hello, Hallo secundaire database of beide, afhankelijk van Hallo audit-type.</span><span class="sxs-lookup"><span data-stu-id="8bb7d-194">When you use geo-replicated databases, it is possible tooset up auditing on either hello primary database, hello secondary database, or both, depending on hello audit type.</span></span>

<span data-ttu-id="8bb7d-195">Volg deze instructies (Vergeet niet dat auditingfunctie voor blobs kan worden ingeschakeld in of uit alleen vanaf de primaire database Hallo controle-instellingen):</span><span class="sxs-lookup"><span data-stu-id="8bb7d-195">Follow these instructions (remember that blob auditing can be turned on or off only from hello primary database auditing settings):</span></span>

* <span data-ttu-id="8bb7d-196">**Primaire database**.</span><span class="sxs-lookup"><span data-stu-id="8bb7d-196">**Primary database**.</span></span> <span data-ttu-id="8bb7d-197">Schakel auditingfunctie voor blobs, op Hallo-server of op Hallo-database zelf, zoals beschreven in Hallo [controle instelt voor uw database](#subheading-2) sectie.</span><span class="sxs-lookup"><span data-stu-id="8bb7d-197">Turn on blob auditing, either on hello server or on hello database itself, as described in hello [Set up auditing for your database](#subheading-2) section.</span></span>
* <span data-ttu-id="8bb7d-198">**Secundaire database**.</span><span class="sxs-lookup"><span data-stu-id="8bb7d-198">**Secondary database**.</span></span> <span data-ttu-id="8bb7d-199">Blob controlebeleid inschakelen op de primaire database hello, zoals beschreven in Hallo [controle instelt voor uw database](#subheading-2) sectie.</span><span class="sxs-lookup"><span data-stu-id="8bb7d-199">Turn on blob auditing on hello primary database, as described in hello [Set up auditing for your database](#subheading-2) section.</span></span> 
   * <span data-ttu-id="8bb7d-200">Controle van de BLOB moet worden ingeschakeld op Hallo *primaire database zelf*, niet op Hallo-server.</span><span class="sxs-lookup"><span data-stu-id="8bb7d-200">Blob auditing must be enabled on hello *primary database itself*, not hello server.</span></span>
   * <span data-ttu-id="8bb7d-201">Nadat de blob-controle is ingeschakeld op de primaire database hello, wordt deze ook ingeschakeld op de secundaire database Hallo.</span><span class="sxs-lookup"><span data-stu-id="8bb7d-201">After blob auditing is enabled on hello primary database, it will also become enabled on hello secondary database.</span></span>

     >[!IMPORTANT]
     ><span data-ttu-id="8bb7d-202">Standaard wordt instellingen voor de opslag voor de secundaire database Hallo Hallo zijn identiek toothose van de primaire database hello, waardoor cross-regionale verkeer.</span><span class="sxs-lookup"><span data-stu-id="8bb7d-202">By default, hello storage settings for hello secondary database will be identical toothose of hello primary database, causing cross-regional traffic.</span></span> <span data-ttu-id="8bb7d-203">U kunt dit vermijden door in te schakelen blob controle op de secundaire server Hallo en lokale opslag configureren in de instellingen voor de opslag van Hallo secundaire server.</span><span class="sxs-lookup"><span data-stu-id="8bb7d-203">You can avoid this by enabling blob auditing on hello secondary server and configuring local storage in hello secondary server storage settings.</span></span> <span data-ttu-id="8bb7d-204">Hallo-opslaglocatie voor de secundaire database Hallo en resultaat in elke database opslaan van de audit logboeken toolocal opslag worden hiermee overschreven.</span><span class="sxs-lookup"><span data-stu-id="8bb7d-204">This will override hello storage location for hello secondary database and result in each database saving its audit logs toolocal storage.</span></span>  
<br>

### <span data-ttu-id="8bb7d-205"><a id="subheading-6">Opslag van sessiesleutels</a></span><span class="sxs-lookup"><span data-stu-id="8bb7d-205"><a id="subheading-6">Storage key regeneration</a></span></span>
<span data-ttu-id="8bb7d-206">In productie bent u waarschijnlijk toorefresh uw opslag periodiek-codes.</span><span class="sxs-lookup"><span data-stu-id="8bb7d-206">In production, you are likely toorefresh your storage keys periodically.</span></span> <span data-ttu-id="8bb7d-207">Bij het vernieuwen van uw sleutels, moet u tooresave Hallo controlebeleid.</span><span class="sxs-lookup"><span data-stu-id="8bb7d-207">When refreshing your keys, you need tooresave hello auditing policy.</span></span> <span data-ttu-id="8bb7d-208">Hallo-proces is als volgt:</span><span class="sxs-lookup"><span data-stu-id="8bb7d-208">hello process is as follows:</span></span>

1. <span data-ttu-id="8bb7d-209">Open Hallo **opslaggroep** blade.</span><span class="sxs-lookup"><span data-stu-id="8bb7d-209">Open hello **Storage Details** blade.</span></span> <span data-ttu-id="8bb7d-210">In Hallo **toegangssleutel voor opslag** de optie **secundaire**, en klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="8bb7d-210">In hello **Storage Access Key** box, select **Secondary**, and click **OK**.</span></span> <span data-ttu-id="8bb7d-211">Klik vervolgens op **opslaan** bovenaan Hallo Hallo configuratie blade controle.</span><span class="sxs-lookup"><span data-stu-id="8bb7d-211">Then click **Save** at hello top of hello auditing configuration blade.</span></span>

    ![Navigatiedeelvenster][5]
2. <span data-ttu-id="8bb7d-213">Ga toohello opslag configuratie blade en opnieuw genereren van de primaire toegangssleutel Hallo.</span><span class="sxs-lookup"><span data-stu-id="8bb7d-213">Go toohello storage configuration blade and regenerate hello primary access key.</span></span>

    ![Navigatiedeelvenster][6]
3. <span data-ttu-id="8bb7d-215">Controle van configuratie-blade toohello terug, Hallo toegangssleutel voor opslag van secundaire tooprimary overschakelen en klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="8bb7d-215">Go back toohello auditing configuration blade, switch hello storage access key from secondary tooprimary, and then click **OK**.</span></span> <span data-ttu-id="8bb7d-216">Klik vervolgens op **opslaan** bovenaan Hallo Hallo configuratie blade controle.</span><span class="sxs-lookup"><span data-stu-id="8bb7d-216">Then click **Save** at hello top of hello auditing configuration blade.</span></span>
4. <span data-ttu-id="8bb7d-217">Ga terug toohello opslag configuratie blade en de secundaire toegangssleutel opnieuw genereren hello (in voorbereiding op Hallo volgende sleutel vernieuwingscyclus).</span><span class="sxs-lookup"><span data-stu-id="8bb7d-217">Go back toohello storage configuration blade and regenerate hello secondary access key (in preparation for hello next key's refresh cycle).</span></span>

## <span data-ttu-id="8bb7d-218"><a id="subheading-7"></a>Automation (PowerShell/REST API)</span><span class="sxs-lookup"><span data-stu-id="8bb7d-218"><a id="subheading-7"></a>Automation (PowerShell/REST API)</span></span>
<span data-ttu-id="8bb7d-219">U kunt ook configureren om controle in Azure SQL Database met behulp van Hallo automatiseringsprogramma's te volgen:</span><span class="sxs-lookup"><span data-stu-id="8bb7d-219">You can also configure auditing in Azure SQL Database by using hello following automation tools:</span></span>

* <span data-ttu-id="8bb7d-220">**PowerShell-cmdlets**:</span><span class="sxs-lookup"><span data-stu-id="8bb7d-220">**PowerShell cmdlets**:</span></span>

   * <span data-ttu-id="8bb7d-221">[Get-AzureRMSqlDatabaseAuditingPolicy][101]</span><span class="sxs-lookup"><span data-stu-id="8bb7d-221">[Get-AzureRMSqlDatabaseAuditingPolicy][101]</span></span>
   * <span data-ttu-id="8bb7d-222">[Get-AzureRMSqlServerAuditingPolicy][102]</span><span class="sxs-lookup"><span data-stu-id="8bb7d-222">[Get-AzureRMSqlServerAuditingPolicy][102]</span></span>
   * <span data-ttu-id="8bb7d-223">[Verwijder AzureRMSqlDatabaseAuditing][103]</span><span class="sxs-lookup"><span data-stu-id="8bb7d-223">[Remove-AzureRMSqlDatabaseAuditing][103]</span></span>
   * <span data-ttu-id="8bb7d-224">[Verwijder AzureRMSqlServerAuditing][104]</span><span class="sxs-lookup"><span data-stu-id="8bb7d-224">[Remove-AzureRMSqlServerAuditing][104]</span></span>
   * <span data-ttu-id="8bb7d-225">[Set-AzureRMSqlDatabaseAuditingPolicy][105]</span><span class="sxs-lookup"><span data-stu-id="8bb7d-225">[Set-AzureRMSqlDatabaseAuditingPolicy][105]</span></span>
   * <span data-ttu-id="8bb7d-226">[Set-AzureRMSqlServerAuditingPolicy][106]</span><span class="sxs-lookup"><span data-stu-id="8bb7d-226">[Set-AzureRMSqlServerAuditingPolicy][106]</span></span>
   * <span data-ttu-id="8bb7d-227">[Gebruik AzureRMSqlServerAuditingPolicy][107]</span><span class="sxs-lookup"><span data-stu-id="8bb7d-227">[Use-AzureRMSqlServerAuditingPolicy][107]</span></span>

   <span data-ttu-id="8bb7d-228">Zie voor een scriptvoorbeeld van een, [configureren van controle en detectie van bedreigingen met behulp van PowerShell](scripts/sql-database-auditing-and-threat-detection-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="8bb7d-228">For a script example, see [Configure auditing and threat detection using PowerShell](scripts/sql-database-auditing-and-threat-detection-powershell.md).</span></span>

* <span data-ttu-id="8bb7d-229">**REST-API - Auditingfunctie voor blobs**:</span><span class="sxs-lookup"><span data-stu-id="8bb7d-229">**REST API - Blob auditing**:</span></span>

   * [<span data-ttu-id="8bb7d-230">Maken of bijwerken van de Database Blob controlebeleid</span><span class="sxs-lookup"><span data-stu-id="8bb7d-230">Create or Update Database Blob Auditing Policy</span></span>](https://msdn.microsoft.com/library/azure/mt695939.aspx)
   * [<span data-ttu-id="8bb7d-231">Maken of bijwerken van de Server Blob controlebeleid</span><span class="sxs-lookup"><span data-stu-id="8bb7d-231">Create or Update Server Blob Auditing Policy</span></span>](https://msdn.microsoft.com/library/azure/mt771861.aspx)
   * [<span data-ttu-id="8bb7d-232">Database-Blob controlebeleid ophalen</span><span class="sxs-lookup"><span data-stu-id="8bb7d-232">Get Database Blob Auditing Policy</span></span>](https://msdn.microsoft.com/library/azure/mt695938.aspx)
   * [<span data-ttu-id="8bb7d-233">Ophalen van Server Blob controlebeleid</span><span class="sxs-lookup"><span data-stu-id="8bb7d-233">Get Server Blob Auditing Policy</span></span>](https://msdn.microsoft.com/library/azure/mt771860.aspx)
   * [<span data-ttu-id="8bb7d-234">Ophalen van Server Blob die het resultaat van controle</span><span class="sxs-lookup"><span data-stu-id="8bb7d-234">Get Server Blob Auditing Operation Result</span></span>](https://msdn.microsoft.com/library/azure/mt771862.aspx)


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

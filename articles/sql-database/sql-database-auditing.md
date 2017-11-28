---
title: Aan de slag met Azure SQL database auditing | Microsoft Docs
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
ms.openlocfilehash: f4324a59b5fa4c2e1ab5b1d7fc7e5fe986ea80f8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-sql-database-auditing"></a><span data-ttu-id="7ff4b-103">Aan de slag met SQL Database Auditing</span><span class="sxs-lookup"><span data-stu-id="7ff4b-103">Get started with SQL database auditing</span></span>
<span data-ttu-id="7ff4b-104">Azure SQL database auditing houdt databasegebeurtenissen en schrijft die deze naar een auditlogboek Meld u bij uw Azure storage-account.</span><span class="sxs-lookup"><span data-stu-id="7ff4b-104">Azure SQL database auditing tracks database events and writes them to an audit log in your Azure storage account.</span></span> <span data-ttu-id="7ff4b-105">Ook controleren:</span><span class="sxs-lookup"><span data-stu-id="7ff4b-105">Auditing also:</span></span>

* <span data-ttu-id="7ff4b-106">Helpt u naleving van regelgeving onderhouden, de activiteit in een database begrijpen en meer inzicht krijgen in discrepanties en afwijkingen die kunnen wijzen op problemen voor het bedrijf of vermoedelijke beveiligingsschendingen.</span><span class="sxs-lookup"><span data-stu-id="7ff4b-106">Helps you maintain regulatory compliance, understand database activity, and gain insight into discrepancies and anomalies that could indicate business concerns or suspected security violations.</span></span>

* <span data-ttu-id="7ff4b-107">Hiermee wordt en vereenvoudigt voldoen aan de nalevingsstandaards, hoewel het geen garantie naleving.</span><span class="sxs-lookup"><span data-stu-id="7ff4b-107">Enables and facilitates adherence to compliance standards, although it doesn't guarantee compliance.</span></span> <span data-ttu-id="7ff4b-108">Zie voor meer informatie over Azure programma's die nalevingsscan standaarden, de [Azure Vertrouwenscentrum](https://azure.microsoft.com/support/trust-center/compliance/).</span><span class="sxs-lookup"><span data-stu-id="7ff4b-108">For more information about Azure programs that support standards compliance, see the [Azure Trust Center](https://azure.microsoft.com/support/trust-center/compliance/).</span></span>


## <span data-ttu-id="7ff4b-109"><a id="subheading-1"></a>Azure SQL-database controle-overzicht</span><span class="sxs-lookup"><span data-stu-id="7ff4b-109"><a id="subheading-1"></a>Azure SQL database auditing overview</span></span>
<span data-ttu-id="7ff4b-110">U kunt gebruiken om SQL-database in op:</span><span class="sxs-lookup"><span data-stu-id="7ff4b-110">You can use SQL database auditing to:</span></span>


* <span data-ttu-id="7ff4b-111">**Behouden** een audittrail van de geselecteerde gebeurtenissen.</span><span class="sxs-lookup"><span data-stu-id="7ff4b-111">**Retain** an audit trail of selected events.</span></span> <span data-ttu-id="7ff4b-112">Categorieën van databaseacties moeten worden gecontroleerd, kunt u definiëren.</span><span class="sxs-lookup"><span data-stu-id="7ff4b-112">You can define categories of database actions to be audited.</span></span>
* <span data-ttu-id="7ff4b-113">**Rapport** op database-activiteit.</span><span class="sxs-lookup"><span data-stu-id="7ff4b-113">**Report** on database activity.</span></span> <span data-ttu-id="7ff4b-114">U kunt vooraf geconfigureerde rapporten en een dashboard snel aan de slag met de activiteit en rapportage.</span><span class="sxs-lookup"><span data-stu-id="7ff4b-114">You can use preconfigured reports and a dashboard to get started quickly with activity and event reporting.</span></span>
* <span data-ttu-id="7ff4b-115">**Analyseren** rapporten.</span><span class="sxs-lookup"><span data-stu-id="7ff4b-115">**Analyze** reports.</span></span> <span data-ttu-id="7ff4b-116">U kunt verdachte gebeurtenissen, ongebruikelijke activiteiten en trends vinden.</span><span class="sxs-lookup"><span data-stu-id="7ff4b-116">You can find suspicious events, unusual activity, and trends.</span></span>

<span data-ttu-id="7ff4b-117">Configureer controle voor verschillende soorten gebeurteniscategorieën, zoals wordt beschreven in de [controle instelt voor uw database](#subheading-2) sectie.</span><span class="sxs-lookup"><span data-stu-id="7ff4b-117">You can configure auditing for different types of event categories, as explained in the [Set up auditing for your database](#subheading-2) section.</span></span>

<span data-ttu-id="7ff4b-118">Controlelogboeken worden geschreven naar Azure Blob-opslag op uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="7ff4b-118">Audit logs are written to Azure Blob storage on your Azure subscription.</span></span>


## <span data-ttu-id="7ff4b-119"><a id="subheading-8"></a>Serverniveau versus databaseniveau controlebeleid definiëren</span><span class="sxs-lookup"><span data-stu-id="7ff4b-119"><a id="subheading-8"></a>Define server-level vs. database-level auditing policy</span></span>

<span data-ttu-id="7ff4b-120">Een controlebeleid kan worden gedefinieerd voor een specifieke database of als een standaardbeleid voor server:</span><span class="sxs-lookup"><span data-stu-id="7ff4b-120">An auditing policy can be defined for a specific database or as a default server policy:</span></span>

* <span data-ttu-id="7ff4b-121">Een serverbeleid geldt voor alle bestaande en nieuwe databases op de server.</span><span class="sxs-lookup"><span data-stu-id="7ff4b-121">A server policy applies to all existing and newly created databases on the server.</span></span>

* <span data-ttu-id="7ff4b-122">Als *server blob-controle is ingeschakeld*, het *altijd van toepassing is op de database* (dat wil zeggen, de database worden gecontroleerd), ongeacht de database controle-instellingen.</span><span class="sxs-lookup"><span data-stu-id="7ff4b-122">If *server blob auditing is enabled*, it *always applies to the database* (that is, the database will be audited), regardless of the database auditing settings.</span></span>

* <span data-ttu-id="7ff4b-123">Blob controle op de database is ingeschakeld, naast het inschakelen van deze op de server wordt *niet* overschrijven of wijzigen van de instellingen van de server auditingfunctie voor blobs.</span><span class="sxs-lookup"><span data-stu-id="7ff4b-123">Enabling blob auditing on the database, in addition to enabling it on the server, will *not* override or change any of the settings of the server blob auditing.</span></span> <span data-ttu-id="7ff4b-124">Beide audits, naast elkaar bestaan.</span><span class="sxs-lookup"><span data-stu-id="7ff4b-124">Both audits will exist side by side.</span></span> <span data-ttu-id="7ff4b-125">Met andere woorden, worden de database gecontroleerd tweemaal parallel (eenmaal door het serverbeleid en eens door het beleid van de database).</span><span class="sxs-lookup"><span data-stu-id="7ff4b-125">In other words, the database will be audited twice in parallel (once by the server policy and once by the database policy).</span></span>

   > [!NOTE]
   > <span data-ttu-id="7ff4b-126">Vermijd het inschakelen van de server blob controle en het blob Databasecontrole samen tenzij:</span><span class="sxs-lookup"><span data-stu-id="7ff4b-126">You should avoid enabling both server blob auditing and database blob auditing together, unless:</span></span>
    > * <span data-ttu-id="7ff4b-127">U wilt gebruiken een andere *opslagaccount* of *bewaarperiode* voor een specifieke database.</span><span class="sxs-lookup"><span data-stu-id="7ff4b-127">You want to use a different *storage account* or *retention period* for a specific database.</span></span>
    > * <span data-ttu-id="7ff4b-128">U wilt controleren gebeurtenistypen of voor een specifieke database die afwijken van de typen gebeurtenissen categorieën worden voor de rest van de databases op de server wordt gecontroleerd.</span><span class="sxs-lookup"><span data-stu-id="7ff4b-128">You want to audit event types or categories for a specific database that differ from event types or categories that are being audited for the rest of the databases on the server.</span></span> <span data-ttu-id="7ff4b-129">Bijvoorbeeld wellicht tabel invoegen die moeten worden gecontroleerd alleen voor een specifieke database.</span><span class="sxs-lookup"><span data-stu-id="7ff4b-129">For example, you might have table inserts that need to be audited only for a specific database.</span></span>
   > 
   > <span data-ttu-id="7ff4b-130">Anders, raden wij u alleen serverniveau blob controle in te schakelen en laat de databaseniveau controle uitgeschakeld voor alle databases.</span><span class="sxs-lookup"><span data-stu-id="7ff4b-130">Otherwise, we recommended that you enable only server-level blob auditing and leave the database-level auditing disabled for all databases.</span></span>


## <span data-ttu-id="7ff4b-131"><a id="subheading-2"></a>Controle voor uw database instellen</span><span class="sxs-lookup"><span data-stu-id="7ff4b-131"><a id="subheading-2"></a>Set up auditing for your database</span></span>
<span data-ttu-id="7ff4b-132">De volgende sectie beschrijft de configuratie van controlebeleid met de Azure portal.</span><span class="sxs-lookup"><span data-stu-id="7ff4b-132">The following section describes the configuration of auditing using the Azure portal.</span></span>

1. <span data-ttu-id="7ff4b-133">Ga naar de [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="7ff4b-133">Go to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="7ff4b-134">Ga naar de **instellingen** blade van de SQL database/SQL-server die u wilt controleren.</span><span class="sxs-lookup"><span data-stu-id="7ff4b-134">Go to the **Settings** blade of the SQL database/SQL server you want to audit.</span></span> <span data-ttu-id="7ff4b-135">In de **instellingen** blade Selecteer **controle en detectie van bedreigingen**.</span><span class="sxs-lookup"><span data-stu-id="7ff4b-135">In the **Settings** blade, select **Auditing & Threat detection**.</span></span>

    <span data-ttu-id="7ff4b-136"><a id="auditing-screenshot"></a>![Navigatiedeelvenster][1]</span><span class="sxs-lookup"><span data-stu-id="7ff4b-136"><a id="auditing-screenshot"></a> ![Navigation pane][1]</span></span>
3. <span data-ttu-id="7ff4b-137">Als u liever voor het instellen van een server controlebeleid (die van toepassing op alle bestaande en nieuwe databases op deze server), kunt u de **serverinstellingen weergeven** koppeling in de databaseblade voor controle.</span><span class="sxs-lookup"><span data-stu-id="7ff4b-137">If you prefer to set up a server auditing policy (which will apply to all existing and newly created databases on this server), you can select the **View server settings** link in the database auditing blade.</span></span> <span data-ttu-id="7ff4b-138">U kunt vervolgens weergeven of wijzigen van de server controle-instellingen.</span><span class="sxs-lookup"><span data-stu-id="7ff4b-138">You can then view or modify the server auditing settings.</span></span>

    ![Navigatiedeelvenster][2]
4. <span data-ttu-id="7ff4b-140">Als u liever blob controle op databaseniveau (naast of in plaats van het niveau van de server controleren), in te schakelen voor **controle**, selecteer **ON**, en voor **type controle**, selecteer **Blob**.</span><span class="sxs-lookup"><span data-stu-id="7ff4b-140">If you prefer to enable blob auditing on the database level (in addition to or instead of server-level auditing), for **Auditing**, select **ON**, and for **Auditing type**, select  **Blob**.</span></span>

    <span data-ttu-id="7ff4b-141">Als server auditingfunctie voor blobs is ingeschakeld, wordt de controle van de database geconfigureerd bestaan naast de blob-controle-server.</span><span class="sxs-lookup"><span data-stu-id="7ff4b-141">If server blob auditing is enabled, the database-configured audit will exist side by side with the server blob audit.</span></span>  

    ![Navigatiedeelvenster][3]
5. <span data-ttu-id="7ff4b-143">Openen van de **Audit logboeken opslag** blade, selecteer **opslaggroep**.</span><span class="sxs-lookup"><span data-stu-id="7ff4b-143">To open the **Audit Logs Storage** blade, select **Storage Details**.</span></span> <span data-ttu-id="7ff4b-144">Selecteer de Azure-opslagaccount waarin de logboeken worden opgeslagen en selecteer vervolgens de bewaartermijn, waarna de oude logboeken worden verwijderd.</span><span class="sxs-lookup"><span data-stu-id="7ff4b-144">Select the Azure storage account where logs will be saved, and then select the retention period, after which the old logs will be deleted.</span></span> <span data-ttu-id="7ff4b-145">Klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="7ff4b-145">Then click **OK**.</span></span> 
   >[!TIP] 
   ><span data-ttu-id="7ff4b-146">Als u de meest buiten de controle rapporten sjablonen, gebruikt u hetzelfde opslagaccount voor alle gecontroleerde databases.</span><span class="sxs-lookup"><span data-stu-id="7ff4b-146">To get the most out of the auditing reports templates, use the same storage account for all audited databases.</span></span> 

    <span data-ttu-id="7ff4b-147"><a id="storage-screenshot"></a>![Navigatiedeelvenster][4]</span><span class="sxs-lookup"><span data-stu-id="7ff4b-147"><a id="storage-screenshot"></a> ![Navigation pane][4]</span></span>
6. <span data-ttu-id="7ff4b-148">Als u aanpassen van de gecontroleerde gebeurtenissen wilt, kunt u dit doen via PowerShell of de REST-API.</span><span class="sxs-lookup"><span data-stu-id="7ff4b-148">If you want to customize the audited events, you can do this via PowerShell or the REST API.</span></span> <span data-ttu-id="7ff4b-149">Zie voor meer informatie de [Automation (PowerShell/REST-API)](#subheading-7) sectie.</span><span class="sxs-lookup"><span data-stu-id="7ff4b-149">For more details, see the [Automation (PowerShell/REST API)](#subheading-7) section.</span></span>
7. <span data-ttu-id="7ff4b-150">Nadat u de controle-instellingen hebt geconfigureerd, kunt u de mogelijkheid voor het detecteren van nieuwe threat inschakelen en configureren van e-mailberichten voor het ontvangen van beveiligingsberichten.</span><span class="sxs-lookup"><span data-stu-id="7ff4b-150">After you've configured your auditing settings, you can turn on the new threat detection feature and configure emails to receive security alerts.</span></span> <span data-ttu-id="7ff4b-151">Wanneer u detectie van dreigingen gebruikt, ontvangt u proactieve waarschuwingen voor afwijkende databaseactiviteiten die kunnen duiden op beveiligingsdreigingen.</span><span class="sxs-lookup"><span data-stu-id="7ff4b-151">When you use threat detection, you receive proactive alerts on anomalous database activities that can indicate potential security threats.</span></span> <span data-ttu-id="7ff4b-152">Zie voor meer informatie [aan de slag met detectie van dreigingen](sql-database-threat-detection-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="7ff4b-152">For more details, see [Getting started with threat detection](sql-database-threat-detection-get-started.md).</span></span>
8. <span data-ttu-id="7ff4b-153">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="7ff4b-153">Click **Save**.</span></span>





## <span data-ttu-id="7ff4b-154"><a id="subheading-3"></a>Controlelogboeken en -rapporten analyseren</span><span class="sxs-lookup"><span data-stu-id="7ff4b-154"><a id="subheading-3"></a>Analyze audit logs and reports</span></span>
<span data-ttu-id="7ff4b-155">Controlelogboeken worden samengevoegd in de Azure storage-account dat u hebt gekozen tijdens de installatie.</span><span class="sxs-lookup"><span data-stu-id="7ff4b-155">Audit logs are aggregated in the Azure storage account you chose during setup.</span></span> <span data-ttu-id="7ff4b-156">U kunt de controlelogboeken verkennen met een hulpprogramma zoals [Azure Opslagverkenner](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="7ff4b-156">You can explore audit logs by using a tool such as [Azure Storage Explorer](http://storageexplorer.com/).</span></span>

<span data-ttu-id="7ff4b-157">BLOB controle logboeken worden opgeslagen als een verzameling van blob-bestanden in een container met de naam **sqldbauditlogs**.</span><span class="sxs-lookup"><span data-stu-id="7ff4b-157">Blob auditing logs are saved as a collection of blob files within a container named **sqldbauditlogs**.</span></span>

<span data-ttu-id="7ff4b-158">Zie voor meer informatie over de hiërarchie van de blob audit logboeken opslagmap, blob naamconventies en logboekindeling de [Audit Log indeling Blobverwijzing (.docx-bestand downloaden)](https://go.microsoft.com/fwlink/?linkid=829599).</span><span class="sxs-lookup"><span data-stu-id="7ff4b-158">For further details about the hierarchy of the blob audit logs storage folder, blob naming conventions, and log format, see the [Blob Audit Log Format Reference (.docx file download)](https://go.microsoft.com/fwlink/?linkid=829599).</span></span>

<span data-ttu-id="7ff4b-159">Er zijn verschillende methoden die u gebruiken kunt om blob controlelogboeken weer te geven:</span><span class="sxs-lookup"><span data-stu-id="7ff4b-159">There are several methods you can use to view blob auditing logs:</span></span>

* <span data-ttu-id="7ff4b-160">Gebruik de [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="7ff4b-160">Use the [Azure portal](https://portal.azure.com).</span></span>  <span data-ttu-id="7ff4b-161">Open de betreffende database.</span><span class="sxs-lookup"><span data-stu-id="7ff4b-161">Open the relevant database.</span></span> <span data-ttu-id="7ff4b-162">Aan de bovenkant van de database **controle en detectie van bedreigingen** blade, klikt u op **weergave controlelogboeken**.</span><span class="sxs-lookup"><span data-stu-id="7ff4b-162">At the top of the database's **Auditing & Threat detection** blade, click **View audit logs**.</span></span>

    ![Navigatiedeelvenster][7]

    <span data-ttu-id="7ff4b-164">Een **controleren records** blade wordt geopend, waarin u zult kunnen de logboeken weergeven.</span><span class="sxs-lookup"><span data-stu-id="7ff4b-164">An **Audit records** blade opens, from which you'll be able to view the logs.</span></span>

    - <span data-ttu-id="7ff4b-165">U kunt specifieke datums weergeven door te klikken op **Filter** boven aan de **controleren records** blade.</span><span class="sxs-lookup"><span data-stu-id="7ff4b-165">You can view specific dates by clicking **Filter** at the top of the **Audit records** blade.</span></span>
    - <span data-ttu-id="7ff4b-166">U kunt schakelen tussen controlerecords die zijn gemaakt met een server beleid of database beleid audit.</span><span class="sxs-lookup"><span data-stu-id="7ff4b-166">You can switch between audit records that were created by a server policy or database policy audit.</span></span>

       ![Navigatiedeelvenster][8]

* <span data-ttu-id="7ff4b-168">Gebruik de systeemfunctie **sys.fn_get_audit_file** (T-SQL) te retourneren van de logboekgegevens audit in tabelvorm.</span><span class="sxs-lookup"><span data-stu-id="7ff4b-168">Use the system function **sys.fn_get_audit_file** (T-SQL) to return the audit log data in tabular format.</span></span> <span data-ttu-id="7ff4b-169">Zie voor meer informatie over het gebruik van deze functie de [sys.fn_get_audit_file documentatie](https://docs.microsoft.com/sql/relational-databases/system-functions/sys-fn-get-audit-file-transact-sql).</span><span class="sxs-lookup"><span data-stu-id="7ff4b-169">For more information on using this function, see the [sys.fn_get_audit_file documentation](https://docs.microsoft.com/sql/relational-databases/system-functions/sys-fn-get-audit-file-transact-sql).</span></span>


* <span data-ttu-id="7ff4b-170">Gebruik **controlebestanden samenvoegen** in SQL Server Management Studio (SSMS 17 vanaf):</span><span class="sxs-lookup"><span data-stu-id="7ff4b-170">Use **Merge Audit Files** in SQL Server Management Studio (starting with SSMS 17):</span></span>  
    1. <span data-ttu-id="7ff4b-171">Selecteer in het menu SSMS **bestand** > **Open** > **controlebestanden samenvoegen**.</span><span class="sxs-lookup"><span data-stu-id="7ff4b-171">From the SSMS menu, select **File** > **Open** > **Merge Audit Files**.</span></span>

        ![Navigatiedeelvenster][9]
    2. <span data-ttu-id="7ff4b-173">De **controlebestanden toevoegen** dialoogvenster wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="7ff4b-173">The **Add Audit Files** dialog box opens.</span></span> <span data-ttu-id="7ff4b-174">Selecteer een van de **toevoegen** opties te kiezen of auditbestanden van een lokale schijf samen, of ze importeren uit Azure Storage (u moet uw Azure Storage details en de accountsleutel opgeven).</span><span class="sxs-lookup"><span data-stu-id="7ff4b-174">Select one of the **Add** options to choose whether to merge audit files from a local disk or import them from Azure Storage (you will be required to provide your Azure Storage details and account key).</span></span>

    3. <span data-ttu-id="7ff4b-175">Nadat alle bestanden samenvoegen zijn toegevoegd, klikt u op **OK** de samenvoegen uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="7ff4b-175">After all files to merge have been added, click **OK** to complete the merge operation.</span></span>

    4. <span data-ttu-id="7ff4b-176">Het samengevoegde bestand wordt geopend in SSMS, waar u kunt weergeven en analyseren, evenals exporteren naar een xel-bestand of de CSV-bestand of een tabel.</span><span class="sxs-lookup"><span data-stu-id="7ff4b-176">The merged file opens in SSMS, where you can view and analyze it, as well as export it to an XEL or CSV file or to a table.</span></span>

* <span data-ttu-id="7ff4b-177">Gebruik de [toepassing synchroniseren](https://github.com/Microsoft/Azure-SQL-DB-auditing-OMS-integration) die we hebben gemaakt.</span><span class="sxs-lookup"><span data-stu-id="7ff4b-177">Use the [sync application](https://github.com/Microsoft/Azure-SQL-DB-auditing-OMS-integration) that we have created.</span></span> <span data-ttu-id="7ff4b-178">Het wordt uitgevoerd in Azure en maakt gebruik van Operations Management Suite (OMS) logboekanalyse openbare API's voor de push-SQL-controlelogboeken in OMS.</span><span class="sxs-lookup"><span data-stu-id="7ff4b-178">It runs in Azure and utilizes Operations Management Suite (OMS) Log Analytics public APIs to push SQL audit logs into OMS.</span></span> <span data-ttu-id="7ff4b-179">De synchronisatie-toepassing duwt SQL controlelogboeken in OMS Log Analytics voor consumptie via het dashboard OMS-logboekanalyse.</span><span class="sxs-lookup"><span data-stu-id="7ff4b-179">The sync application pushes SQL audit logs into OMS Log Analytics for consumption via the OMS Log Analytics dashboard.</span></span> 

* <span data-ttu-id="7ff4b-180">Power BI gebruiken.</span><span class="sxs-lookup"><span data-stu-id="7ff4b-180">Use Power BI.</span></span> <span data-ttu-id="7ff4b-181">U kunt weergeven en analyseren van gegevens van de audit log in Power BI.</span><span class="sxs-lookup"><span data-stu-id="7ff4b-181">You can view and analyze audit log data in Power BI.</span></span> <span data-ttu-id="7ff4b-182">Meer informatie over [Power BI en toegang tot een sjabloon downloaden](https://blogs.msdn.microsoft.com/azuresqldbsupport/2017/05/26/sql-azure-blob-auditing-basic-power-bi-dashboard/).</span><span class="sxs-lookup"><span data-stu-id="7ff4b-182">Learn more about [Power BI, and access a downloadable template](https://blogs.msdn.microsoft.com/azuresqldbsupport/2017/05/26/sql-azure-blob-auditing-basic-power-bi-dashboard/).</span></span>

* <span data-ttu-id="7ff4b-183">Downloaden van de logboekbestanden van uw Azure Storage blob-container via de portal of met een hulpprogramma zoals [Azure Opslagverkenner](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="7ff4b-183">Download log files from your Azure Storage blob container via the portal or by using a tool such as [Azure Storage Explorer](http://storageexplorer.com/).</span></span>
    * <span data-ttu-id="7ff4b-184">Nadat u lokaal een logboekbestand hebt gedownload, kunt u het bestand te openen, weergeven en analyseren van de logboeken in SSMS dubbelklikken.</span><span class="sxs-lookup"><span data-stu-id="7ff4b-184">After you have downloaded a log file locally, you can double-click the file to open, view, and analyze the logs in SSMS.</span></span>
    * <span data-ttu-id="7ff4b-185">U kunt ook meerdere bestanden tegelijkertijd via Azure Opslagverkenner downloaden.</span><span class="sxs-lookup"><span data-stu-id="7ff4b-185">You can also download multiple files simultaneously via Azure Storage Explorer.</span></span> <span data-ttu-id="7ff4b-186">Met de rechtermuisknop op een specifieke submap (bijvoorbeeld: een submap met alle logboekbestanden voor een specifieke datum) en selecteer **opslaan als** om op te slaan in een lokale map.</span><span class="sxs-lookup"><span data-stu-id="7ff4b-186">Right-click a specific subfolder (for example, a subfolder that includes all log files for a specific date) and select **Save as** to save in a local folder.</span></span>

* <span data-ttu-id="7ff4b-187">Extra methoden:</span><span class="sxs-lookup"><span data-stu-id="7ff4b-187">Additional methods:</span></span>
   * <span data-ttu-id="7ff4b-188">Na het downloaden van verschillende bestanden (of een submap met logboekbestanden voor een volledige dag, zoals beschreven in het vorige item in deze lijst), kunt u deze samenvoegen lokaal zoals beschreven in de controlebestanden van SSMS Merge-instructies eerder beschreven.</span><span class="sxs-lookup"><span data-stu-id="7ff4b-188">After downloading several files (or a subfolder that includes log files for an entire day, as described in the previous item in this list), you can merge them locally as described in the SSMS Merge Audit Files instructions described earlier.</span></span>

   * <span data-ttu-id="7ff4b-189">Weergave auditingfunctie voor blobs registreert programmatisch:</span><span class="sxs-lookup"><span data-stu-id="7ff4b-189">View blob auditing logs programmatically:</span></span>

     * <span data-ttu-id="7ff4b-190">Gebruik de [uitgebreide gebeurtenissen lezer](https://blogs.msdn.microsoft.com/extended_events/2011/07/20/introducing-the-extended-events-reader/) C#-bibliotheek.</span><span class="sxs-lookup"><span data-stu-id="7ff4b-190">Use the [Extended Events Reader](https://blogs.msdn.microsoft.com/extended_events/2011/07/20/introducing-the-extended-events-reader/) C# library.</span></span>
     * <span data-ttu-id="7ff4b-191">[Uitgebreide gebeurtenissen bestanden query](https://sqlscope.wordpress.com/2014/11/15/reading-extended-event-files-using-client-side-tools-only/) met behulp van PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7ff4b-191">[Query Extended Events Files](https://sqlscope.wordpress.com/2014/11/15/reading-extended-event-files-using-client-side-tools-only/) by using PowerShell.</span></span>




## <span data-ttu-id="7ff4b-192"><a id="subheading-5"></a>Procedures voor productie</span><span class="sxs-lookup"><span data-stu-id="7ff4b-192"><a id="subheading-5"></a>Production practices</span></span>
<!--The description in this section refers to preceding screen captures.-->

### <span data-ttu-id="7ff4b-193"><a id="subheading-6">Geogerepliceerde databases controle</a></span><span class="sxs-lookup"><span data-stu-id="7ff4b-193"><a id="subheading-6">Auditing geo-replicated databases</a></span></span>
<span data-ttu-id="7ff4b-194">Wanneer u databases geo-replicatie gebruikt, is controle instellen voor de primaire database, de secundaire database, of beide, afhankelijk van het type audit.</span><span class="sxs-lookup"><span data-stu-id="7ff4b-194">When you use geo-replicated databases, it is possible to set up auditing on either the primary database, the secondary database, or both, depending on the audit type.</span></span>

<span data-ttu-id="7ff4b-195">Volg deze instructies (Vergeet niet dat auditingfunctie voor blobs kan worden ingeschakeld in of uit alleen vanaf de primaire database controle-instellingen):</span><span class="sxs-lookup"><span data-stu-id="7ff4b-195">Follow these instructions (remember that blob auditing can be turned on or off only from the primary database auditing settings):</span></span>

* <span data-ttu-id="7ff4b-196">**Primaire database**.</span><span class="sxs-lookup"><span data-stu-id="7ff4b-196">**Primary database**.</span></span> <span data-ttu-id="7ff4b-197">Schakel auditingfunctie voor blobs, op de server of op de database zelf, zoals beschreven in de [controle instelt voor uw database](#subheading-2) sectie.</span><span class="sxs-lookup"><span data-stu-id="7ff4b-197">Turn on blob auditing, either on the server or on the database itself, as described in the [Set up auditing for your database](#subheading-2) section.</span></span>
* <span data-ttu-id="7ff4b-198">**Secundaire database**.</span><span class="sxs-lookup"><span data-stu-id="7ff4b-198">**Secondary database**.</span></span> <span data-ttu-id="7ff4b-199">Blob controlebeleid inschakelen op de primaire database, zoals beschreven in de [controle instelt voor uw database](#subheading-2) sectie.</span><span class="sxs-lookup"><span data-stu-id="7ff4b-199">Turn on blob auditing on the primary database, as described in the [Set up auditing for your database](#subheading-2) section.</span></span> 
   * <span data-ttu-id="7ff4b-200">Controle van de BLOB moet worden ingeschakeld op de *primaire database zelf*, niet op de server.</span><span class="sxs-lookup"><span data-stu-id="7ff4b-200">Blob auditing must be enabled on the *primary database itself*, not the server.</span></span>
   * <span data-ttu-id="7ff4b-201">Nadat de blob-controle is ingeschakeld op de primaire database, wordt deze ook ingeschakeld op de secundaire database.</span><span class="sxs-lookup"><span data-stu-id="7ff4b-201">After blob auditing is enabled on the primary database, it will also become enabled on the secondary database.</span></span>

     >[!IMPORTANT]
     ><span data-ttu-id="7ff4b-202">Standaard zal de instellingen voor de opslag voor de secundaire database zijn identiek aan die van de primaire database waardoor cross-regionale verkeer.</span><span class="sxs-lookup"><span data-stu-id="7ff4b-202">By default, the storage settings for the secondary database will be identical to those of the primary database, causing cross-regional traffic.</span></span> <span data-ttu-id="7ff4b-203">U kunt dit vermijden door in te schakelen blob controle op de secundaire server en lokale opslag configureren in de opslaginstellingen voor de secundaire server.</span><span class="sxs-lookup"><span data-stu-id="7ff4b-203">You can avoid this by enabling blob auditing on the secondary server and configuring local storage in the secondary server storage settings.</span></span> <span data-ttu-id="7ff4b-204">Hierdoor wordt de opslaglocatie voor de secundaire database en het resultaat in elke database de controlelogboeken voor lokale opslag opslaan overschreven.</span><span class="sxs-lookup"><span data-stu-id="7ff4b-204">This will override the storage location for the secondary database and result in each database saving its audit logs to local storage.</span></span>  
<br>

### <span data-ttu-id="7ff4b-205"><a id="subheading-6">Opslag van sessiesleutels</a></span><span class="sxs-lookup"><span data-stu-id="7ff4b-205"><a id="subheading-6">Storage key regeneration</a></span></span>
<span data-ttu-id="7ff4b-206">In productie bent u waarschijnlijk uw opslagsleutels periodiek te vernieuwen.</span><span class="sxs-lookup"><span data-stu-id="7ff4b-206">In production, you are likely to refresh your storage keys periodically.</span></span> <span data-ttu-id="7ff4b-207">Bij het vernieuwen van uw sleutels, moet u het beveiligingsbeleid opnieuw op te slaan.</span><span class="sxs-lookup"><span data-stu-id="7ff4b-207">When refreshing your keys, you need to resave the auditing policy.</span></span> <span data-ttu-id="7ff4b-208">Het proces is als volgt:</span><span class="sxs-lookup"><span data-stu-id="7ff4b-208">The process is as follows:</span></span>

1. <span data-ttu-id="7ff4b-209">Open de **opslaggroep** blade.</span><span class="sxs-lookup"><span data-stu-id="7ff4b-209">Open the **Storage Details** blade.</span></span> <span data-ttu-id="7ff4b-210">In de **toegangssleutel voor opslag** de optie **secundaire**, en klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="7ff4b-210">In the **Storage Access Key** box, select **Secondary**, and click **OK**.</span></span> <span data-ttu-id="7ff4b-211">Klik vervolgens op **opslaan** aan de bovenkant van de controlemogelijkheden configuratie-blade.</span><span class="sxs-lookup"><span data-stu-id="7ff4b-211">Then click **Save** at the top of the auditing configuration blade.</span></span>

    ![Navigatiedeelvenster][5]
2. <span data-ttu-id="7ff4b-213">Ga naar de blade van de configuratie van opslag en opnieuw genereren van de primaire toegangssleutel.</span><span class="sxs-lookup"><span data-stu-id="7ff4b-213">Go to the storage configuration blade and regenerate the primary access key.</span></span>

    ![Navigatiedeelvenster][6]
3. <span data-ttu-id="7ff4b-215">Ga terug naar de blade controle configuratie schakelt de toegangssleutel voor opslag van secundaire op primaire en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="7ff4b-215">Go back to the auditing configuration blade, switch the storage access key from secondary to primary, and then click **OK**.</span></span> <span data-ttu-id="7ff4b-216">Klik vervolgens op **opslaan** aan de bovenkant van de controlemogelijkheden configuratie-blade.</span><span class="sxs-lookup"><span data-stu-id="7ff4b-216">Then click **Save** at the top of the auditing configuration blade.</span></span>
4. <span data-ttu-id="7ff4b-217">Ga terug naar de blade van de configuratie van opslag en opnieuw genereren van de secundaire toegangssleutel (in voorbereiding op de volgende sleutel vernieuwingscyclus).</span><span class="sxs-lookup"><span data-stu-id="7ff4b-217">Go back to the storage configuration blade and regenerate the secondary access key (in preparation for the next key's refresh cycle).</span></span>

## <span data-ttu-id="7ff4b-218"><a id="subheading-7"></a>Automation (PowerShell/REST API)</span><span class="sxs-lookup"><span data-stu-id="7ff4b-218"><a id="subheading-7"></a>Automation (PowerShell/REST API)</span></span>
<span data-ttu-id="7ff4b-219">U kunt ook configureren om controle in Azure SQL Database met behulp van de volgende automation-hulpprogramma's:</span><span class="sxs-lookup"><span data-stu-id="7ff4b-219">You can also configure auditing in Azure SQL Database by using the following automation tools:</span></span>

* <span data-ttu-id="7ff4b-220">**PowerShell-cmdlets**:</span><span class="sxs-lookup"><span data-stu-id="7ff4b-220">**PowerShell cmdlets**:</span></span>

   * <span data-ttu-id="7ff4b-221">[Get-AzureRMSqlDatabaseAuditingPolicy][101]</span><span class="sxs-lookup"><span data-stu-id="7ff4b-221">[Get-AzureRMSqlDatabaseAuditingPolicy][101]</span></span>
   * <span data-ttu-id="7ff4b-222">[Get-AzureRMSqlServerAuditingPolicy][102]</span><span class="sxs-lookup"><span data-stu-id="7ff4b-222">[Get-AzureRMSqlServerAuditingPolicy][102]</span></span>
   * <span data-ttu-id="7ff4b-223">[Verwijder AzureRMSqlDatabaseAuditing][103]</span><span class="sxs-lookup"><span data-stu-id="7ff4b-223">[Remove-AzureRMSqlDatabaseAuditing][103]</span></span>
   * <span data-ttu-id="7ff4b-224">[Verwijder AzureRMSqlServerAuditing][104]</span><span class="sxs-lookup"><span data-stu-id="7ff4b-224">[Remove-AzureRMSqlServerAuditing][104]</span></span>
   * <span data-ttu-id="7ff4b-225">[Set-AzureRMSqlDatabaseAuditingPolicy][105]</span><span class="sxs-lookup"><span data-stu-id="7ff4b-225">[Set-AzureRMSqlDatabaseAuditingPolicy][105]</span></span>
   * <span data-ttu-id="7ff4b-226">[Set-AzureRMSqlServerAuditingPolicy][106]</span><span class="sxs-lookup"><span data-stu-id="7ff4b-226">[Set-AzureRMSqlServerAuditingPolicy][106]</span></span>
   * <span data-ttu-id="7ff4b-227">[Gebruik AzureRMSqlServerAuditingPolicy][107]</span><span class="sxs-lookup"><span data-stu-id="7ff4b-227">[Use-AzureRMSqlServerAuditingPolicy][107]</span></span>

   <span data-ttu-id="7ff4b-228">Zie voor een scriptvoorbeeld van een, [configureren van controle en detectie van bedreigingen met behulp van PowerShell](scripts/sql-database-auditing-and-threat-detection-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="7ff4b-228">For a script example, see [Configure auditing and threat detection using PowerShell](scripts/sql-database-auditing-and-threat-detection-powershell.md).</span></span>

* <span data-ttu-id="7ff4b-229">**REST-API - Auditingfunctie voor blobs**:</span><span class="sxs-lookup"><span data-stu-id="7ff4b-229">**REST API - Blob auditing**:</span></span>

   * [<span data-ttu-id="7ff4b-230">Maken of bijwerken van de Database Blob controlebeleid</span><span class="sxs-lookup"><span data-stu-id="7ff4b-230">Create or Update Database Blob Auditing Policy</span></span>](https://msdn.microsoft.com/library/azure/mt695939.aspx)
   * [<span data-ttu-id="7ff4b-231">Maken of bijwerken van de Server Blob controlebeleid</span><span class="sxs-lookup"><span data-stu-id="7ff4b-231">Create or Update Server Blob Auditing Policy</span></span>](https://msdn.microsoft.com/library/azure/mt771861.aspx)
   * [<span data-ttu-id="7ff4b-232">Database-Blob controlebeleid ophalen</span><span class="sxs-lookup"><span data-stu-id="7ff4b-232">Get Database Blob Auditing Policy</span></span>](https://msdn.microsoft.com/library/azure/mt695938.aspx)
   * [<span data-ttu-id="7ff4b-233">Ophalen van Server Blob controlebeleid</span><span class="sxs-lookup"><span data-stu-id="7ff4b-233">Get Server Blob Auditing Policy</span></span>](https://msdn.microsoft.com/library/azure/mt771860.aspx)
   * [<span data-ttu-id="7ff4b-234">Ophalen van Server Blob die het resultaat van controle</span><span class="sxs-lookup"><span data-stu-id="7ff4b-234">Get Server Blob Auditing Operation Result</span></span>](https://msdn.microsoft.com/library/azure/mt771862.aspx)


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

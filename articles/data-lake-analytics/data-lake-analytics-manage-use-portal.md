---
title: aaaManage Azure Data Lake Analytics met behulp van Azure-portal Hallo | Microsoft Docs
description: Meer informatie over hoe Data Lake Analytics acounts, gegevens toomanage, gebruikers bronnen, en taken.
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: jhubbard
editor: cgronlun
ms.assetid: a0e045f1-73d6-427f-868d-7b55c10f811b
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 12/05/2016
ms.author: edmaca
ms.openlocfilehash: f63ccdfae79772c92e92462194e8cdc636a73dc6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-data-lake-analytics-by-using-hello-azure-portal"></a><span data-ttu-id="6f061-103">Azure Data Lake Analytics beheren met behulp van hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="6f061-103">Manage Azure Data Lake Analytics by using hello Azure portal</span></span>
[!INCLUDE [manage-selector](../../includes/data-lake-analytics-selector-manage.md)]

<span data-ttu-id="6f061-104">Meer informatie over hoe Hallo toomanage Azure Data Lake Analytics-accounts, gegevensbronnen account, gebruikers en taken met behulp van Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="6f061-104">Learn how toomanage Azure Data Lake Analytics accounts, account data sources, users, and jobs by using hello Azure portal.</span></span> <span data-ttu-id="6f061-105">toosee management onderwerpen over het gebruik van andere hulpprogramma's, klikt u op een tabblad bovenaan Hallo Hallo pagina.</span><span class="sxs-lookup"><span data-stu-id="6f061-105">toosee management topics about using other tools, click a tab at hello top of hello page.</span></span>

<!-- ################################ -->
<!-- ################################ -->

## <a name="manage-data-lake-analytics-accounts"></a><span data-ttu-id="6f061-106">Data Lake Analytics-accounts beheren</span><span class="sxs-lookup"><span data-stu-id="6f061-106">Manage Data Lake Analytics accounts</span></span>

### <a name="create-an-account"></a><span data-ttu-id="6f061-107">Een account maken</span><span class="sxs-lookup"><span data-stu-id="6f061-107">Create an account</span></span>

1. <span data-ttu-id="6f061-108">Meld u aan toohello [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="6f061-108">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="6f061-109">Klik op **Nieuw** > **Intelligence + analyse** > **Data Lake Analytics**.</span><span class="sxs-lookup"><span data-stu-id="6f061-109">Click **New** > **Intelligence + analytics** > **Data Lake Analytics**.</span></span>
3. <span data-ttu-id="6f061-110">Waarden selecteren voor Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="6f061-110">Select values for hello following items:</span></span> 
   1. <span data-ttu-id="6f061-111">**Naam**: naam Hallo Hallo Data Lake Analytics-account.</span><span class="sxs-lookup"><span data-stu-id="6f061-111">**Name**: hello name of hello Data Lake Analytics account.</span></span>
   2. <span data-ttu-id="6f061-112">**Abonnement**: hello Azure-abonnement gebruikt voor het Hallo-account.</span><span class="sxs-lookup"><span data-stu-id="6f061-112">**Subscription**: hello Azure subscription used for hello account.</span></span>
   3. <span data-ttu-id="6f061-113">**Resourcegroep**: hello Azure resourcegroep in welk toocreate Hallo-account.</span><span class="sxs-lookup"><span data-stu-id="6f061-113">**Resource Group**: hello Azure resource group in which toocreate hello account.</span></span> 
   4. <span data-ttu-id="6f061-114">**Locatie**: hello Azure-datacenter voor Hallo Data Lake Analytics-account.</span><span class="sxs-lookup"><span data-stu-id="6f061-114">**Location**: hello Azure datacenter for hello Data Lake Analytics account.</span></span> 
   5. <span data-ttu-id="6f061-115">**Data Lake Store**: Hallo standaard store toobe gebruikt voor Hallo Data Lake Analytics-account.</span><span class="sxs-lookup"><span data-stu-id="6f061-115">**Data Lake Store**: hello default store toobe used for hello Data Lake Analytics account.</span></span> <span data-ttu-id="6f061-116">Hello Azure Data Lake Store-account en Hallo Data Lake Analytics-account moet zich in Hallo dezelfde locatie.</span><span class="sxs-lookup"><span data-stu-id="6f061-116">hello Azure Data Lake Store account and hello Data Lake Analytics account must be in hello same location.</span></span>
4. <span data-ttu-id="6f061-117">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="6f061-117">Click **Create**.</span></span> 

### <a name="delete-a-data-lake-analytics-account"></a><span data-ttu-id="6f061-118">Een Data Lake Analytics-account verwijderen</span><span class="sxs-lookup"><span data-stu-id="6f061-118">Delete a Data Lake Analytics account</span></span>

<span data-ttu-id="6f061-119">Voordat u een Data Lake Analytics-account verwijdert, verwijdert u de Data Lake Store-standaardaccount.</span><span class="sxs-lookup"><span data-stu-id="6f061-119">Before you delete a Data Lake Analytics account, delete its default Data Lake Store account.</span></span>

1. <span data-ttu-id="6f061-120">Ga in de Azure-portal hello, tooyour Data Lake Analytics-account.</span><span class="sxs-lookup"><span data-stu-id="6f061-120">In hello Azure portal, go tooyour Data Lake Analytics account.</span></span>
2. <span data-ttu-id="6f061-121">Klik op **Verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="6f061-121">Click **Delete**.</span></span>
3. <span data-ttu-id="6f061-122">Typenaam Hallo-account.</span><span class="sxs-lookup"><span data-stu-id="6f061-122">Type hello account name.</span></span>
4. <span data-ttu-id="6f061-123">Klik op **Verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="6f061-123">Click **Delete**.</span></span>

<!-- ################################ -->
<!-- ################################ -->

## <a name="manage-data-sources"></a><span data-ttu-id="6f061-124">Gegevensbronnen beheren</span><span class="sxs-lookup"><span data-stu-id="6f061-124">Manage data sources</span></span>

<span data-ttu-id="6f061-125">Data Lake Analytics ondersteunt Hallo gegevensbronnen te volgen:</span><span class="sxs-lookup"><span data-stu-id="6f061-125">Data Lake Analytics supports hello following data sources:</span></span>

* <span data-ttu-id="6f061-126">Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="6f061-126">Data Lake Store</span></span>
* <span data-ttu-id="6f061-127">Azure Storage</span><span class="sxs-lookup"><span data-stu-id="6f061-127">Azure Storage</span></span>

<span data-ttu-id="6f061-128">U kunt Data Explorer toobrowse gegevensbronnen gebruiken en basic bestand beheerbewerkingen uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="6f061-128">You can use Data Explorer toobrowse data sources and perform basic file management operations.</span></span> 

### <a name="add-a-data-source"></a><span data-ttu-id="6f061-129">Een gegevensbron toevoegen</span><span class="sxs-lookup"><span data-stu-id="6f061-129">Add a data source</span></span>

1. <span data-ttu-id="6f061-130">Ga in de Azure-portal hello, tooyour Data Lake Analytics-account.</span><span class="sxs-lookup"><span data-stu-id="6f061-130">In hello Azure portal, go tooyour Data Lake Analytics account.</span></span>
2. <span data-ttu-id="6f061-131">Klik op **gegevensbronnen**.</span><span class="sxs-lookup"><span data-stu-id="6f061-131">Click **Data Sources**.</span></span>
3. <span data-ttu-id="6f061-132">Klik op **gegevensbron toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="6f061-132">Click **Add Data Source**.</span></span>
    
   * <span data-ttu-id="6f061-133">tooadd een Data Lake Store-account, moet u Hallo-account en toohello account toobe kunnen tooquery deze.</span><span class="sxs-lookup"><span data-stu-id="6f061-133">tooadd a Data Lake Store account, you need hello account name and access toohello account toobe able tooquery it.</span></span>
   * <span data-ttu-id="6f061-134">tooadd Azure Blob-opslag, moet u Hallo storage-account en accountsleutel Hallo.</span><span class="sxs-lookup"><span data-stu-id="6f061-134">tooadd Azure Blob storage, you need hello storage account and hello account key.</span></span> <span data-ttu-id="6f061-135">toofind ze, gaat u toohello storage-account in Hallo-portal.</span><span class="sxs-lookup"><span data-stu-id="6f061-135">toofind them, go toohello storage account in hello portal.</span></span>

## <a name="set-up-firewall-rules"></a><span data-ttu-id="6f061-136">Firewallregels instellen</span><span class="sxs-lookup"><span data-stu-id="6f061-136">Set up firewall rules</span></span>

<span data-ttu-id="6f061-137">U kunt Data Lake Analytics toofurther vergrendelen toegang tooyour Data Lake Analytics-account op netwerkniveau hello gebruiken.</span><span class="sxs-lookup"><span data-stu-id="6f061-137">You can use Data Lake Analytics toofurther lock down access tooyour Data Lake Analytics account at hello network level.</span></span> <span data-ttu-id="6f061-138">U kunt een firewall inschakelen, Geef een IP-adres of een IP-adresbereik voor de vertrouwde clients te definiëren.</span><span class="sxs-lookup"><span data-stu-id="6f061-138">You can enable a firewall, specify an IP address, or define an IP address range for your trusted clients.</span></span> <span data-ttu-id="6f061-139">Nadat u deze maatregelen hebt ingeschakeld, kunnen alleen clients waarvoor Hallo IP-adressen binnen het bereik van Hallo gedefinieerd verbinding toohello store maken.</span><span class="sxs-lookup"><span data-stu-id="6f061-139">After you enable these measures, only clients that have hello IP addresses within hello defined range can connect toohello store.</span></span>

<span data-ttu-id="6f061-140">Als andere Azure-services, zoals Azure Data Factory- of virtuele machines, verbinding toohello Data Lake Analytics-account maakt, controleert u of **Azure-Services toestaan** is ingeschakeld **op**.</span><span class="sxs-lookup"><span data-stu-id="6f061-140">If other Azure services, like Azure Data Factory or VMs, connect toohello Data Lake Analytics account, make sure that **Allow Azure Services** is turned **On**.</span></span> 

### <a name="set-up-a-firewall-rule"></a><span data-ttu-id="6f061-141">Een firewallregel instellen</span><span class="sxs-lookup"><span data-stu-id="6f061-141">Set up a firewall rule</span></span>

1. <span data-ttu-id="6f061-142">Ga in de Azure-portal hello, tooyour Data Lake Analytics-account.</span><span class="sxs-lookup"><span data-stu-id="6f061-142">In hello Azure portal, go tooyour Data Lake Analytics account.</span></span>
2. <span data-ttu-id="6f061-143">Klik op het menu aan de linkerkant Hallo Hallo **Firewall**.</span><span class="sxs-lookup"><span data-stu-id="6f061-143">On hello menu on hello left, click **Firewall**.</span></span>

## <a name="add-a-new-user"></a><span data-ttu-id="6f061-144">Een nieuwe gebruiker toevoegen</span><span class="sxs-lookup"><span data-stu-id="6f061-144">Add a new user</span></span>

<span data-ttu-id="6f061-145">U kunt Hallo **Wizard gebruiker toevoegen** tooeasily nieuwe Data Lake gebruikers hebt ingericht.</span><span class="sxs-lookup"><span data-stu-id="6f061-145">You can use hello **Add User Wizard** tooeasily provision new Data Lake users.</span></span>

1. <span data-ttu-id="6f061-146">Ga in de Azure-portal hello, tooyour Data Lake Analytics-account.</span><span class="sxs-lookup"><span data-stu-id="6f061-146">In hello Azure portal, go tooyour Data Lake Analytics account.</span></span>
2. <span data-ttu-id="6f061-147">Op Hallo links, klikt u onder **aan de slag**, klikt u op **Wizard gebruiker toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="6f061-147">On hello left, under **Getting Started**, click **Add User Wizard**.</span></span>
3. <span data-ttu-id="6f061-148">Selecteer een gebruiker en klik vervolgens op **Selecteer**.</span><span class="sxs-lookup"><span data-stu-id="6f061-148">Select a user, and then click **Select**.</span></span>
4. <span data-ttu-id="6f061-149">Selecteer een rol en klik vervolgens op **Selecteer**.</span><span class="sxs-lookup"><span data-stu-id="6f061-149">Select a role, and then click **Select**.</span></span> <span data-ttu-id="6f061-150">tooset van een nieuwe developer toouse Azure Data Lake, selecteer Hallo **Data Lake Analytics Developer** rol.</span><span class="sxs-lookup"><span data-stu-id="6f061-150">tooset up a new developer toouse Azure Data Lake, select hello **Data Lake Analytics Developer** role.</span></span>
5. <span data-ttu-id="6f061-151">Selecteer Hallo toegangsbeheerlijsten (ACL's) voor Hallo U-SQL-databases.</span><span class="sxs-lookup"><span data-stu-id="6f061-151">Select hello access control lists (ACLs) for hello U-SQL databases.</span></span> <span data-ttu-id="6f061-152">Wanneer u tevreden met uw keuzes bent, klikt u op **Selecteer**.</span><span class="sxs-lookup"><span data-stu-id="6f061-152">When you're satisfied with your choices, click **Select**.</span></span>
6. <span data-ttu-id="6f061-153">Selecteer Hallo ACL's voor bestanden.</span><span class="sxs-lookup"><span data-stu-id="6f061-153">Select hello ACLs for files.</span></span> <span data-ttu-id="6f061-154">Voor het standaardarchief hello, niet te wijzigen Hallo ACL's voor de hoofdmap Hallo '/' en voor Hallo/System-map.</span><span class="sxs-lookup"><span data-stu-id="6f061-154">For hello default store, don't change hello ACLs for hello root folder "/" and for hello /system folder.</span></span> <span data-ttu-id="6f061-155">Klik op **Selecteren**.</span><span class="sxs-lookup"><span data-stu-id="6f061-155">Click **Select**.</span></span>
7. <span data-ttu-id="6f061-156">Controleer de geselecteerde wijzigingen en klik vervolgens op **uitvoeren**.</span><span class="sxs-lookup"><span data-stu-id="6f061-156">Review all your selected changes, and then click **Run**.</span></span>
8. <span data-ttu-id="6f061-157">Wanneer het Hallo-wizard is voltooid, klikt u op **gedaan**.</span><span class="sxs-lookup"><span data-stu-id="6f061-157">When hello wizard is finished, click **Done**.</span></span>

## <a name="manage-role-based-access-control"></a><span data-ttu-id="6f061-158">Toegangsbeheer op basis van rollen beheren</span><span class="sxs-lookup"><span data-stu-id="6f061-158">Manage Role-Based Access Control</span></span>

<span data-ttu-id="6f061-159">Net als andere Azure-services, kunt u rollen gebaseerd toegangsbeheer (RBAC) toocontrol hoe gebruikers interacteren met Hallo-service.</span><span class="sxs-lookup"><span data-stu-id="6f061-159">Like other Azure services, you can use Role-Based Access Control (RBAC) toocontrol how users interact with hello service.</span></span>

<span data-ttu-id="6f061-160">Hallo standaard RBAC-rollen hebben Hallo volgende mogelijkheden:</span><span class="sxs-lookup"><span data-stu-id="6f061-160">hello standard RBAC roles have hello following capabilities:</span></span>
* <span data-ttu-id="6f061-161">**Eigenaar**: kunt verzenden van taken, taken controleren, annuleren taken van elke gebruiker en Hallo-account configureren.</span><span class="sxs-lookup"><span data-stu-id="6f061-161">**Owner**: Can submit jobs, monitor jobs, cancel jobs from any user, and configure hello account.</span></span>
* <span data-ttu-id="6f061-162">**Inzender**: kunt verzenden van taken, taken controleren, annuleren taken van elke gebruiker en Hallo-account configureren.</span><span class="sxs-lookup"><span data-stu-id="6f061-162">**Contributor**: Can submit jobs, monitor jobs, cancel jobs from any user, and configure hello account.</span></span>
* <span data-ttu-id="6f061-163">**Lezer**: taken kunt bewaken.</span><span class="sxs-lookup"><span data-stu-id="6f061-163">**Reader**: Can monitor jobs.</span></span>

<span data-ttu-id="6f061-164">Hallo Data Lake Analytics Developer rol tooenable U-SQL-ontwikkelaars toouse Hallo Data Lake Analytics service gebruiken.</span><span class="sxs-lookup"><span data-stu-id="6f061-164">Use hello Data Lake Analytics Developer role tooenable U-SQL developers toouse hello Data Lake Analytics service.</span></span> <span data-ttu-id="6f061-165">U kunt Hallo Data Lake Analytics Developer-rol:</span><span class="sxs-lookup"><span data-stu-id="6f061-165">You can use hello Data Lake Analytics Developer role to:</span></span>
* <span data-ttu-id="6f061-166">Verzenden van taken.</span><span class="sxs-lookup"><span data-stu-id="6f061-166">Submit jobs.</span></span>
* <span data-ttu-id="6f061-167">De voortgang taak status en Hallo van taken die worden verzonden door een gebruiker.</span><span class="sxs-lookup"><span data-stu-id="6f061-167">Monitor job status and hello progress of jobs submitted by any user.</span></span>
* <span data-ttu-id="6f061-168">Zie Hallo U-SQL-scripts uit taken die worden aangeboden door een gebruiker.</span><span class="sxs-lookup"><span data-stu-id="6f061-168">See hello U-SQL scripts from jobs submitted by any user.</span></span>
* <span data-ttu-id="6f061-169">Alleen uw eigen taken annuleren.</span><span class="sxs-lookup"><span data-stu-id="6f061-169">Cancel only your own jobs.</span></span>

### <a name="add-users-or-security-groups-tooa-data-lake-analytics-account"></a><span data-ttu-id="6f061-170">Gebruikers- of beveiliging groepen tooa Data Lake Analytics-account toevoegen</span><span class="sxs-lookup"><span data-stu-id="6f061-170">Add users or security groups tooa Data Lake Analytics account</span></span>

1. <span data-ttu-id="6f061-171">Ga in de Azure-portal hello, tooyour Data Lake Analytics-account.</span><span class="sxs-lookup"><span data-stu-id="6f061-171">In hello Azure portal, go tooyour Data Lake Analytics account.</span></span>
2. <span data-ttu-id="6f061-172">Klik op **toegangsbeheer (IAM)** > **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="6f061-172">Click **Access control (IAM)** > **Add**.</span></span>
3. <span data-ttu-id="6f061-173">Selecteer een rol.</span><span class="sxs-lookup"><span data-stu-id="6f061-173">Select a role.</span></span>
4. <span data-ttu-id="6f061-174">Een gebruiker toevoegen.</span><span class="sxs-lookup"><span data-stu-id="6f061-174">Add a user.</span></span>
5. <span data-ttu-id="6f061-175">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="6f061-175">Click **OK**.</span></span>

>[!NOTE]
><span data-ttu-id="6f061-176">Als een gebruiker of een beveiligingsgroep toosubmit taken moet, nodig ze ook machtiging op Hallo store-account.</span><span class="sxs-lookup"><span data-stu-id="6f061-176">If a user or a security group needs toosubmit jobs, they also need permission on hello store account.</span></span> <span data-ttu-id="6f061-177">Zie voor meer informatie [beveiliging van gegevens die zijn opgeslagen in Data Lake Store](../data-lake-store/data-lake-store-secure-data.md).</span><span class="sxs-lookup"><span data-stu-id="6f061-177">For more information, see [Secure data stored in Data Lake Store](../data-lake-store/data-lake-store-secure-data.md).</span></span>
>

<!-- ################################ -->
<!-- ################################ -->

## <a name="manage-jobs"></a><span data-ttu-id="6f061-178">Taken beheren</span><span class="sxs-lookup"><span data-stu-id="6f061-178">Manage jobs</span></span>

### <a name="submit-a-job"></a><span data-ttu-id="6f061-179">Verzenden van een taak</span><span class="sxs-lookup"><span data-stu-id="6f061-179">Submit a job</span></span>

1. <span data-ttu-id="6f061-180">Ga in de Azure-portal hello, tooyour Data Lake Analytics-account.</span><span class="sxs-lookup"><span data-stu-id="6f061-180">In hello Azure portal, go tooyour Data Lake Analytics account.</span></span>

2. <span data-ttu-id="6f061-181">Klik op **nieuwe taak**.</span><span class="sxs-lookup"><span data-stu-id="6f061-181">Click **New Job**.</span></span> <span data-ttu-id="6f061-182">Voor elke taak configureren:</span><span class="sxs-lookup"><span data-stu-id="6f061-182">For each job,  configure:</span></span>

    1. <span data-ttu-id="6f061-183">**Taaknaam**: Hallo-naam van Hallo-taak.</span><span class="sxs-lookup"><span data-stu-id="6f061-183">**Job Name**: hello name of hello job.</span></span>
    2. <span data-ttu-id="6f061-184">**Prioriteit**: lagere getallen hebben een hogere prioriteit.</span><span class="sxs-lookup"><span data-stu-id="6f061-184">**Priority**: Lower numbers have higher priority.</span></span> <span data-ttu-id="6f061-185">Als u twee taken in de wachtrij staan, Hallo met lagere prioriteitswaarde eerste wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="6f061-185">If two jobs are queued, hello one with lower priority value runs first.</span></span>
    3. <span data-ttu-id="6f061-186">**Parallelle uitvoering**: Hallo kunt u het maximum aantal compute tooreserve voor deze taak worden verwerkt.</span><span class="sxs-lookup"><span data-stu-id="6f061-186">**Parallelism**: hello maximum number of compute processes tooreserve for this job.</span></span>

3. <span data-ttu-id="6f061-187">Klik op **Taak verzenden**.</span><span class="sxs-lookup"><span data-stu-id="6f061-187">Click **Submit Job**.</span></span>

### <a name="monitor-jobs"></a><span data-ttu-id="6f061-188">Taken controleren</span><span class="sxs-lookup"><span data-stu-id="6f061-188">Monitor jobs</span></span>

1. <span data-ttu-id="6f061-189">Ga in de Azure-portal hello, tooyour Data Lake Analytics-account.</span><span class="sxs-lookup"><span data-stu-id="6f061-189">In hello Azure portal, go tooyour Data Lake Analytics account.</span></span>
2. <span data-ttu-id="6f061-190">Klik op **alle taken weergeven**.</span><span class="sxs-lookup"><span data-stu-id="6f061-190">Click **View All Jobs**.</span></span> <span data-ttu-id="6f061-191">Een lijst met alle Hallo actief en recent voltooide taken in Hallo-account wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="6f061-191">A list of all hello active and recently finished jobs in hello account is shown.</span></span>
3. <span data-ttu-id="6f061-192">Klik desgewenst op **Filter** toohelp vindt u de taken op Hallo **tijdsbereik**, **taaknaam**, en **auteur** waarden.</span><span class="sxs-lookup"><span data-stu-id="6f061-192">Optionally, click **Filter** toohelp you find hello jobs by **Time Range**, **Job Name**, and **Author** values.</span></span> 

### <a name="monitoring-pipeline-jobs"></a><span data-ttu-id="6f061-193">Taken van de pijplijn bewaken</span><span class="sxs-lookup"><span data-stu-id="6f061-193">Monitoring pipeline jobs</span></span>
<span data-ttu-id="6f061-194">Taken die deel van een pijplijn uitmaken werken samen, meestal opeenvolgend tooaccomplish een specifiek scenario.</span><span class="sxs-lookup"><span data-stu-id="6f061-194">Jobs that are part of a pipeline work together, usually sequentially, tooaccomplish a specific scenario.</span></span> <span data-ttu-id="6f061-195">U kunt bijvoorbeeld een pijplijn die schoongemaakt, pakt, transformaties, gebruik voor de klant insights aggregeert hebben.</span><span class="sxs-lookup"><span data-stu-id="6f061-195">For example, you can have a pipeline that cleans, extracts, transforms, aggregates usage for customer insights.</span></span> <span data-ttu-id="6f061-196">Pipeline-taken worden aangeduid met Hallo "Pipeline" eigenschap bij het Hallo-taak is verzonden.</span><span class="sxs-lookup"><span data-stu-id="6f061-196">Pipeline jobs are identified using hello "Pipeline" property when hello job was submitted.</span></span> <span data-ttu-id="6f061-197">Taken gepland met ADF V2 hebben automatisch deze eigenschap is ingevuld.</span><span class="sxs-lookup"><span data-stu-id="6f061-197">Jobs scheduled using ADF V2 will automatically have this property populated.</span></span> 

<span data-ttu-id="6f061-198">een lijst met U-SQL-taken die deel van pijplijnen uitmaken tooview:</span><span class="sxs-lookup"><span data-stu-id="6f061-198">tooview a list of U-SQL jobs that are part of pipelines:</span></span> 

1. <span data-ttu-id="6f061-199">Ga in de Azure-portal hello, tooyour Data Lake Analytics-accounts.</span><span class="sxs-lookup"><span data-stu-id="6f061-199">In hello Azure portal, go tooyour Data Lake Analytics accounts.</span></span>
2. <span data-ttu-id="6f061-200">Klik op **taak Insights**.</span><span class="sxs-lookup"><span data-stu-id="6f061-200">Click **Job Insights**.</span></span> <span data-ttu-id="6f061-201">Hallo die tabblad 'Alle taken' wordt standaard ingesteld, bevat een overzicht van die wordt uitgevoerd, in de wachtrij en taken beëindigd.</span><span class="sxs-lookup"><span data-stu-id="6f061-201">hello "All Jobs" tab will be defaulted, showing a list of running, queued, and ended jobs.</span></span>
3. <span data-ttu-id="6f061-202">Klik op Hallo **pijplijn taken** tabblad. Een lijst met taken van de pijplijn wordt weergegeven samen met de samengevoegde statistieken voor elke pijplijn.</span><span class="sxs-lookup"><span data-stu-id="6f061-202">Click hello **Pipeline Jobs** tab. A list of pipeline jobs will be shown along with aggregated statistics for each pipeline.</span></span>

### <a name="monitoring-recurring-jobs"></a><span data-ttu-id="6f061-203">Terugkerende taken bewaken</span><span class="sxs-lookup"><span data-stu-id="6f061-203">Monitoring recurring jobs</span></span>
<span data-ttu-id="6f061-204">Een terugkerende taak is een die Hallo heeft dezelfde bedrijfslogica hierbij wordt gebruikgemaakt van verschillende invoergegevens telkens wanneer deze wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="6f061-204">A recurring job is one that has hello same business logic but uses different input data every time it runs.</span></span> <span data-ttu-id="6f061-205">In het ideale geval moeten terugkerende taken altijd slagen en hebben relatief stabiel uitvoeringstijd; Deze problemen bewaking helpt ervoor te zorgen Hallo-taak is in orde.</span><span class="sxs-lookup"><span data-stu-id="6f061-205">Ideally, recurring jobs should always succeed, and have relatively stable execution time; monitoring these behaviors will help ensure hello job is healthy.</span></span> <span data-ttu-id="6f061-206">Terugkerende taken worden aangeduid met Hallo "Recurrence" eigenschap.</span><span class="sxs-lookup"><span data-stu-id="6f061-206">Recurring jobs are identified using hello "Recurrence" property.</span></span> <span data-ttu-id="6f061-207">Taken gepland met ADF V2 hebben automatisch deze eigenschap is ingevuld.</span><span class="sxs-lookup"><span data-stu-id="6f061-207">Jobs scheduled using ADF V2 will automatically have this property populated.</span></span>

<span data-ttu-id="6f061-208">een lijst met U-SQL-taken die zijn terugkerende tooview:</span><span class="sxs-lookup"><span data-stu-id="6f061-208">tooview a list of U-SQL jobs that are recurring:</span></span> 

1. <span data-ttu-id="6f061-209">Ga in de Azure-portal hello, tooyour Data Lake Analytics-accounts.</span><span class="sxs-lookup"><span data-stu-id="6f061-209">In hello Azure portal, go tooyour Data Lake Analytics accounts.</span></span>
2. <span data-ttu-id="6f061-210">Klik op **taak Insights**.</span><span class="sxs-lookup"><span data-stu-id="6f061-210">Click **Job Insights**.</span></span> <span data-ttu-id="6f061-211">Hallo die tabblad 'Alle taken' wordt standaard ingesteld, bevat een overzicht van die wordt uitgevoerd, in de wachtrij en taken beëindigd.</span><span class="sxs-lookup"><span data-stu-id="6f061-211">hello "All Jobs" tab will be defaulted, showing a list of running, queued, and ended jobs.</span></span>
3. <span data-ttu-id="6f061-212">Klik op Hallo **terugkerende taken** tabblad. Een lijst met terugkerende taken wordt samen met de samengevoegde statistieken voor elke terugkerende taak weergegeven.</span><span class="sxs-lookup"><span data-stu-id="6f061-212">Click hello **Recurring Jobs** tab. A list of recurring jobs will be shown along with aggregated statistics for each recurring job.</span></span>

## <a name="manage-policies"></a><span data-ttu-id="6f061-213">Beleid beheren</span><span class="sxs-lookup"><span data-stu-id="6f061-213">Manage policies</span></span>

### <a name="account-level-policies"></a><span data-ttu-id="6f061-214">Beleid account-niveau</span><span class="sxs-lookup"><span data-stu-id="6f061-214">Account-level policies</span></span>

<span data-ttu-id="6f061-215">Deze beleidsregels van toepassing tooall taken in een Data Lake Analytics-account.</span><span class="sxs-lookup"><span data-stu-id="6f061-215">These policies apply tooall jobs in a Data Lake Analytics account.</span></span>

#### <a name="maximum-number-of-aus-in-a-data-lake-analytics-account"></a><span data-ttu-id="6f061-216">Maximum aantal AUs in een Data Lake Analytics-account</span><span class="sxs-lookup"><span data-stu-id="6f061-216">Maximum number of AUs in a Data Lake Analytics account</span></span>
<span data-ttu-id="6f061-217">Een beleid regelt Hallo kunt u het totale aantal Analytics-eenheden (AUs) uw Data Lake Analytics-account kunt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="6f061-217">A policy controls hello total number of Analytics Units (AUs) your Data Lake Analytics account can use.</span></span> <span data-ttu-id="6f061-218">Hallo-waarde is standaard too250.</span><span class="sxs-lookup"><span data-stu-id="6f061-218">By default, hello value is set too250.</span></span> <span data-ttu-id="6f061-219">Als deze waarde is ingesteld too250 AUs, u kunt bijvoorbeeld één taak uitgevoerd met 250 AUs toegewezen tooit of 10 taken uitgevoerd met 25 AUs elke.</span><span class="sxs-lookup"><span data-stu-id="6f061-219">For example, if this value is set too250 AUs, you can have one job running with 250 AUs assigned tooit, or 10 jobs running with 25 AUs each.</span></span> <span data-ttu-id="6f061-220">Aanvullende taken die zijn ingediend in de wachtrij staan totdat Hallo actieve taken zijn voltooid.</span><span class="sxs-lookup"><span data-stu-id="6f061-220">Additional jobs that are submitted are queued until hello running jobs are finished.</span></span> <span data-ttu-id="6f061-221">Wanneer taken zijn voltooid, AUs worden vrijgemaakt voor de Hallo toorun taken in de wachtrij.</span><span class="sxs-lookup"><span data-stu-id="6f061-221">When running jobs are finished, AUs are freed up for hello queued jobs toorun.</span></span>

<span data-ttu-id="6f061-222">toochange hello aantal AUs voor uw Data Lake Analytics-account:</span><span class="sxs-lookup"><span data-stu-id="6f061-222">toochange hello number of AUs for your Data Lake Analytics account:</span></span>

1. <span data-ttu-id="6f061-223">Ga in de Azure-portal hello, tooyour Data Lake Analytics-account.</span><span class="sxs-lookup"><span data-stu-id="6f061-223">In hello Azure portal, go tooyour Data Lake Analytics account.</span></span>
2. <span data-ttu-id="6f061-224">Klik op **Eigenschappen**.</span><span class="sxs-lookup"><span data-stu-id="6f061-224">Click **Properties**.</span></span>
3. <span data-ttu-id="6f061-225">Onder **maximale AUs**, verplaatsen Hallo schuifregelaar tooselect een waarde of Hallo waarde invoeren in het tekstvak Hallo.</span><span class="sxs-lookup"><span data-stu-id="6f061-225">Under **Maximum AUs**, move hello slider tooselect a value, or enter hello value in hello text box.</span></span> 
4. <span data-ttu-id="6f061-226">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="6f061-226">Click **Save**.</span></span>

> [!NOTE]
> <span data-ttu-id="6f061-227">Als u moet meer dan standaard (250) Hallo AUs, klik in Hallo portal op **Help + ondersteuning** toosubmit ondersteuning aan te vragen.</span><span class="sxs-lookup"><span data-stu-id="6f061-227">If you need more than hello default (250) AUs, in hello portal, click **Help+Support** toosubmit a support request.</span></span> <span data-ttu-id="6f061-228">Hallo aantal AUs beschikbaar in uw Data Lake Analytics-account kan worden verhoogd.</span><span class="sxs-lookup"><span data-stu-id="6f061-228">hello number of AUs available in your Data Lake Analytics account can be increased.</span></span>
>

#### <a name="maximum-number-of-jobs-that-can-run-simultaneously"></a><span data-ttu-id="6f061-229">Maximum aantal taken dat tegelijkertijd kan worden uitgevoerd</span><span class="sxs-lookup"><span data-stu-id="6f061-229">Maximum number of jobs that can run simultaneously</span></span>
<span data-ttu-id="6f061-230">Een beleid bepaalt hoeveel taken kunnen uitvoeren op Hallo hetzelfde moment.</span><span class="sxs-lookup"><span data-stu-id="6f061-230">A policy controls how many jobs can run at hello same time.</span></span> <span data-ttu-id="6f061-231">Standaard is deze waarde too20 ingesteld.</span><span class="sxs-lookup"><span data-stu-id="6f061-231">By default, this value is set too20.</span></span> <span data-ttu-id="6f061-232">Als uw Data Lake Analytics AUs beschikbaar heeft, worden nieuwe taken geplande toorun onmiddellijk totdat Hallo totaal aantal actieve taken Hallo-waarde van dit beleid heeft bereikt.</span><span class="sxs-lookup"><span data-stu-id="6f061-232">If your Data Lake Analytics has AUs available, new jobs are scheduled toorun immediately until hello total number of running jobs reaches hello value of this policy.</span></span> <span data-ttu-id="6f061-233">Wanneer u Hallo kunt u het maximum aantal taken dat tegelijkertijd kan worden uitgevoerd bereikt, latere taken in de wachtrij staan in volgorde van prioriteit als een of meer actieve taken hebt voltooid (afhankelijk van de beschikbaarheid van Australië).</span><span class="sxs-lookup"><span data-stu-id="6f061-233">When you reach hello maximum number of jobs that can run simultaneously, subsequent jobs are queued in priority order until one or more running jobs complete (depending on AU availability).</span></span>

<span data-ttu-id="6f061-234">toochange hello aantal taken dat tegelijk kunt uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="6f061-234">toochange hello number of jobs that can run simultaneously:</span></span>

1. <span data-ttu-id="6f061-235">Ga in de Azure-portal hello, tooyour Data Lake Analytics-account.</span><span class="sxs-lookup"><span data-stu-id="6f061-235">In hello Azure portal, go tooyour Data Lake Analytics account.</span></span>
2. <span data-ttu-id="6f061-236">Klik op **Eigenschappen**.</span><span class="sxs-lookup"><span data-stu-id="6f061-236">Click **Properties**.</span></span>
3. <span data-ttu-id="6f061-237">Onder **Maximum aantal van een actief taken**, verplaatsen Hallo schuifregelaar tooselect een waarde of Hallo waarde invoeren in het tekstvak Hallo.</span><span class="sxs-lookup"><span data-stu-id="6f061-237">Under **Maximum Number of Running Jobs**, move hello slider tooselect a value, or enter hello value in hello text box.</span></span> 
4. <span data-ttu-id="6f061-238">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="6f061-238">Click **Save**.</span></span>

> [!NOTE]
> <span data-ttu-id="6f061-239">Als u meer dan Hallo standaard (20) aantal taken in Hallo-portal klikt u op toorun moet **Help + ondersteuning** toosubmit ondersteuning aan te vragen.</span><span class="sxs-lookup"><span data-stu-id="6f061-239">If you need toorun more than hello default (20) number of jobs, in hello portal, click **Help+Support** toosubmit a support request.</span></span> <span data-ttu-id="6f061-240">Hallo aantal taken dat tegelijk in uw Data Lake Analytics-account uitvoeren kunt kan worden verhoogd.</span><span class="sxs-lookup"><span data-stu-id="6f061-240">hello number of jobs that can run simultaneously in your Data Lake Analytics account can be increased.</span></span>
>

#### <a name="how-long-tookeep-job-metadata-and-resources"></a><span data-ttu-id="6f061-241">Hoe lang tookeep taak metagegevens en resources</span><span class="sxs-lookup"><span data-stu-id="6f061-241">How long tookeep job metadata and resources</span></span> 
<span data-ttu-id="6f061-242">Wanneer uw gebruikers U-SQL-taken uitvoeren, behoudt Hallo Data Lake Analytics-service alle bijbehorende bestanden.</span><span class="sxs-lookup"><span data-stu-id="6f061-242">When your users run U-SQL jobs, hello Data Lake Analytics service retains all related files.</span></span> <span data-ttu-id="6f061-243">Verwante bestanden bevatten Hallo U-SQL-script waarnaar wordt verwezen in Hallo U-SQL-script, gecompileerde bronnen en statistieken van Hallo dll-bestanden.</span><span class="sxs-lookup"><span data-stu-id="6f061-243">Related files include hello U-SQL script, hello DLL files referenced in hello U-SQL script, compiled resources, and statistics.</span></span> <span data-ttu-id="6f061-244">Hallo-bestanden zijn in Hallo /system/ map van Hallo standaard Azure Data Lake Storage-account.</span><span class="sxs-lookup"><span data-stu-id="6f061-244">hello files are in hello /system/ folder of hello default Azure Data Lake Storage account.</span></span> <span data-ttu-id="6f061-245">Dit beleid bepaalt hoe lang deze resources worden opgeslagen voordat ze automatisch worden verwijderd (Hallo standaardwaarde is 30 dagen).</span><span class="sxs-lookup"><span data-stu-id="6f061-245">This policy controls how long these resources are stored before they are automatically deleted (hello default is 30 days).</span></span> <span data-ttu-id="6f061-246">U kunt deze bestanden gebruiken voor foutopsporing en voor prestaties afstemmen van taken die u opnieuw in toekomstige Hallo gaat uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="6f061-246">You can use these files for debugging, and for performance-tuning of jobs that you'll rerun in hello future.</span></span>

<span data-ttu-id="6f061-247">toochange hoe lang tookeep taak metagegevens en bronnen:</span><span class="sxs-lookup"><span data-stu-id="6f061-247">toochange how long tookeep job metadata and resources:</span></span>

1. <span data-ttu-id="6f061-248">Ga in de Azure-portal hello, tooyour Data Lake Analytics-account.</span><span class="sxs-lookup"><span data-stu-id="6f061-248">In hello Azure portal, go tooyour Data Lake Analytics account.</span></span>
2. <span data-ttu-id="6f061-249">Klik op **Eigenschappen**.</span><span class="sxs-lookup"><span data-stu-id="6f061-249">Click **Properties**.</span></span>
3. <span data-ttu-id="6f061-250">Onder **dagen tooRetain taak voert een query**, verplaatsen Hallo schuifregelaar tooselect een waarde of Hallo waarde invoeren in het tekstvak Hallo.</span><span class="sxs-lookup"><span data-stu-id="6f061-250">Under **Days tooRetain Job Queries**, move hello slider tooselect a value, or enter hello value in hello text box.</span></span>  
4. <span data-ttu-id="6f061-251">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="6f061-251">Click **Save**.</span></span>

### <a name="job-level-policies"></a><span data-ttu-id="6f061-252">Beleid Job-niveau</span><span class="sxs-lookup"><span data-stu-id="6f061-252">Job-level policies</span></span>
<span data-ttu-id="6f061-253">U kunt beheren met beleid voor niveau van de taak Hallo maximale AUs en Hallo maximumprioriteit individuele gebruikers (of leden van bepaalde beveiligingsgroepen) kunnen worden ingesteld voor taken die ze verzenden.</span><span class="sxs-lookup"><span data-stu-id="6f061-253">With job-level policies, you can control hello maximum AUs and hello maximum priority that individual users (or members of specific security groups) can set on jobs that they submit.</span></span> <span data-ttu-id="6f061-254">Dit kunt u Hallo kosten van gebruikers beheren.</span><span class="sxs-lookup"><span data-stu-id="6f061-254">This lets you control hello costs incurred by users.</span></span> <span data-ttu-id="6f061-255">U kunt ook besturingselement Hallo effect dat taken worden geplande mogelijk hebt u een hoge prioriteit productietaken die worden uitgevoerd in Hallo dezelfde Data Lake Analytics-account.</span><span class="sxs-lookup"><span data-stu-id="6f061-255">It also lets you control hello effect that scheduled jobs might have on high-priority production jobs that are running in hello same Data Lake Analytics account.</span></span>

<span data-ttu-id="6f061-256">Data Lake Analytics heeft twee beleidsregels die u op Hallo taakniveau instellen kunt:</span><span class="sxs-lookup"><span data-stu-id="6f061-256">Data Lake Analytics has two policies that you can set at hello job level:</span></span>

* <span data-ttu-id="6f061-257">**Australië limiet is per taak**: gebruikers kunnen alleen taken die u een aantal AUs toothis hebt indienen.</span><span class="sxs-lookup"><span data-stu-id="6f061-257">**AU limit per job**: Users can only submit jobs that have up toothis number of AUs.</span></span> <span data-ttu-id="6f061-258">Standaard is deze limiet Hallo hetzelfde als Hallo Australië maximumlimiet voor Hallo-account.</span><span class="sxs-lookup"><span data-stu-id="6f061-258">By default, this limit is hello same as hello maximum AU limit for hello account.</span></span>
* <span data-ttu-id="6f061-259">**Prioriteit**: gebruikers kunnen alleen indienen voor taken met een prioriteitswaarde toothis lager is dan of gelijk zijn.</span><span class="sxs-lookup"><span data-stu-id="6f061-259">**Priority**: Users can only submit jobs that have a priority lower than or equal toothis value.</span></span> <span data-ttu-id="6f061-260">Houd er rekening mee dat een hoger getal een lagere prioriteit geeft.</span><span class="sxs-lookup"><span data-stu-id="6f061-260">Note that a higher number means a lower priority.</span></span> <span data-ttu-id="6f061-261">Dit is standaard too1, namelijk Hallo hoogst mogelijke prioriteit.</span><span class="sxs-lookup"><span data-stu-id="6f061-261">By default, this is set too1, which is hello highest possible priority.</span></span>

<span data-ttu-id="6f061-262">Er is een standaardbeleid instellen voor elke account.</span><span class="sxs-lookup"><span data-stu-id="6f061-262">There is a default policy set on every account.</span></span> <span data-ttu-id="6f061-263">Hallo-standaardbeleid is van toepassing tooall gebruikers van Hallo-account.</span><span class="sxs-lookup"><span data-stu-id="6f061-263">hello default policy applies tooall users of hello account.</span></span> <span data-ttu-id="6f061-264">U kunt extra beleidsregels instellen voor specifieke gebruikers en groepen.</span><span class="sxs-lookup"><span data-stu-id="6f061-264">You can set additional policies for specific users and groups.</span></span> 

> [!NOTE]
> <span data-ttu-id="6f061-265">Beleidsregels voor account-niveau en op jobniveau toepassing tegelijk.</span><span class="sxs-lookup"><span data-stu-id="6f061-265">Account-level policies and job-level policies apply simultaneously.</span></span>
>

#### <a name="add-a-policy-for-a-specific-user-or-group"></a><span data-ttu-id="6f061-266">Een beleid voor een specifieke gebruiker of groep toevoegen</span><span class="sxs-lookup"><span data-stu-id="6f061-266">Add a policy for a specific user or group</span></span>

1. <span data-ttu-id="6f061-267">Ga in de Azure-portal hello, tooyour Data Lake Analytics-account.</span><span class="sxs-lookup"><span data-stu-id="6f061-267">In hello Azure portal, go tooyour Data Lake Analytics account.</span></span>
2. <span data-ttu-id="6f061-268">Klik op **Eigenschappen**.</span><span class="sxs-lookup"><span data-stu-id="6f061-268">Click **Properties**.</span></span>
3. <span data-ttu-id="6f061-269">Onder **taak verzending limieten**, klikt u op Hallo **beleid toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="6f061-269">Under **Job Submission Limits**, click hello **Add Policy** button.</span></span> <span data-ttu-id="6f061-270">Vervolgens, selecteer of typ Hallo volgende instellingen:</span><span class="sxs-lookup"><span data-stu-id="6f061-270">Then, select or enter hello following settings:</span></span>
    1. <span data-ttu-id="6f061-271">**Beleidsnaam COMPUTE**: Voer een naam voor beleid tooremind u Hallo doel van Hallo-beleid.</span><span class="sxs-lookup"><span data-stu-id="6f061-271">**Compute Policy Name**: Enter a policy name, tooremind you of hello purpose of hello policy.</span></span>
    2. <span data-ttu-id="6f061-272">**Gebruiker of groep selecteren**: Selecteer Hallo-gebruiker of groep die dit beleid is van toepassing op.</span><span class="sxs-lookup"><span data-stu-id="6f061-272">**Select User or Group**: Select hello user or group this policy applies to.</span></span>
    3. <span data-ttu-id="6f061-273">**Hallo Australië taaklimiet ingesteld**: Hallo Australië limiet die van toepassing toohello is geselecteerde gebruiker of groep.</span><span class="sxs-lookup"><span data-stu-id="6f061-273">**Set hello Job AU Limit**: Set hello AU limit that applies toohello selected user or group.</span></span>
    4. <span data-ttu-id="6f061-274">**Hallo prioriteit limiet ingesteld**: Hallo prioriteit limiet die van toepassing toohello is geselecteerde gebruiker of groep.</span><span class="sxs-lookup"><span data-stu-id="6f061-274">**Set hello Priority Limit**: Set hello priority limit that applies toohello selected user or group.</span></span>

4. <span data-ttu-id="6f061-275">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="6f061-275">Click **Ok**.</span></span>

5. <span data-ttu-id="6f061-276">Hallo nieuwe beleid wordt weergegeven in Hallo **standaard** beleid tabel onder **taak verzending limieten**.</span><span class="sxs-lookup"><span data-stu-id="6f061-276">hello new policy is listed in hello **Default** policy table, under **Job Submission Limits**.</span></span> 

#### <a name="delete-or-edit-an-existing-policy"></a><span data-ttu-id="6f061-277">Verwijder of een bestaand beleid bewerken</span><span class="sxs-lookup"><span data-stu-id="6f061-277">Delete or edit an existing policy</span></span>

1. <span data-ttu-id="6f061-278">Ga in de Azure-portal hello, tooyour Data Lake Analytics-account.</span><span class="sxs-lookup"><span data-stu-id="6f061-278">In hello Azure portal, go tooyour Data Lake Analytics account.</span></span>
2. <span data-ttu-id="6f061-279">Klik op **Eigenschappen**.</span><span class="sxs-lookup"><span data-stu-id="6f061-279">Click **Properties**.</span></span>
3. <span data-ttu-id="6f061-280">Onder **taak verzending limieten**, zoeken Hallo beleid gewenste tooedit.</span><span class="sxs-lookup"><span data-stu-id="6f061-280">Under **Job Submission Limits**, find hello policy you want tooedit.</span></span>
4.  <span data-ttu-id="6f061-281">Hallo toosee **verwijderen** en **bewerken** opties in de meest rechtse kolom Hallo van Hallo tabel, klikt u op **...** .</span><span class="sxs-lookup"><span data-stu-id="6f061-281">toosee hello **Delete** and **Edit** options, in hello rightmost column of hello table, click **...**.</span></span>

### <a name="additional-resources-for-job-policies"></a><span data-ttu-id="6f061-282">Aanvullende bronnen voor taak-beleid</span><span class="sxs-lookup"><span data-stu-id="6f061-282">Additional resources for job policies</span></span>
* [<span data-ttu-id="6f061-283">Blogbericht beleid-overzicht</span><span class="sxs-lookup"><span data-stu-id="6f061-283">Policy overview blog post</span></span>](https://blogs.msdn.microsoft.com/azuredatalake/2017/06/08/managing-your-azure-data-lake-analytics-compute-resources-overview/)
* [<span data-ttu-id="6f061-284">Blogbericht beleid account-niveau</span><span class="sxs-lookup"><span data-stu-id="6f061-284">Account-level policies blog post</span></span>](https://blogs.msdn.microsoft.com/azuredatalake/2017/06/08/managing-your-azure-data-lake-analytics-compute-resources-account-level-policy/)
* [<span data-ttu-id="6f061-285">Blogbericht beleid Job-niveau</span><span class="sxs-lookup"><span data-stu-id="6f061-285">Job-level policies blog post</span></span>](https://blogs.msdn.microsoft.com/azuredatalake/2017/06/08/managing-your-azure-data-lake-analytics-compute-resources-job-level-policy/)

## <a name="next-steps"></a><span data-ttu-id="6f061-286">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="6f061-286">Next steps</span></span>

* [<span data-ttu-id="6f061-287">Overzicht van Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="6f061-287">Overview of Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
* [<span data-ttu-id="6f061-288">Aan de slag met Data Lake Analytics met behulp van hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="6f061-288">Get started with Data Lake Analytics by using hello Azure portal</span></span>](data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="6f061-289">Azure Data Lake Analytics beheren met behulp van Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="6f061-289">Manage Azure Data Lake Analytics by using Azure PowerShell</span></span>](data-lake-analytics-manage-use-powershell.md)


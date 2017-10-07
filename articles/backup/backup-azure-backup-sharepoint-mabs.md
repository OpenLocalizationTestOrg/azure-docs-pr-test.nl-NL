---
title: aaaUse Azure Backup-server tooback van een SharePoint-farm tooAzure | Microsoft Docs
description: Azure Backup-Server tooback gebruikt en uw SharePoint-gegevens herstellen. In dit artikel biedt Hallo informatie tooconfigure uw SharePoint-farm zodat de gewenste gegevens kunnen worden opgeslagen in Azure. U kunt beveiligde SharePoint-gegevens terugzetten vanaf schijf of Azure.
services: backup
documentationcenter: 
author: pvrk
manager: shivamg
editor: 
ms.assetid: 34ba87a4-91f1-4054-a4a1-272af1e15496
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: pullabhk
ms.openlocfilehash: 350c1ac0f3518f400062f3b586bbe9710a79915a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-a-sharepoint-farm-tooazure"></a><span data-ttu-id="65114-105">Back-up van een SharePoint-farm tooAzure</span><span class="sxs-lookup"><span data-stu-id="65114-105">Back up a SharePoint farm tooAzure</span></span>
<span data-ttu-id="65114-106">U back-up van een SharePoint-farm tooMicrosoft Azure met behulp van Microsoft Azure Backup-Server (MABS) in veel Hallo dezelfde manier als u back-up van andere gegevensbronnen.</span><span class="sxs-lookup"><span data-stu-id="65114-106">You back up a SharePoint farm tooMicrosoft Azure by using Microsoft Azure Backup Server (MABS) in much hello same way that you back up other data sources.</span></span> <span data-ttu-id="65114-107">Azure Backup biedt flexibiliteit in Hallo back-upschema toocreate dagelijkse, wekelijkse, maandelijkse of jaarlijkse back-uppunten en geeft u de bewaarperiode beleidsopties voor verschillende back-uppunten.</span><span class="sxs-lookup"><span data-stu-id="65114-107">Azure Backup provides flexibility in hello backup schedule toocreate daily, weekly, monthly, or yearly backup points and gives you retention policy options for various backup points.</span></span> <span data-ttu-id="65114-108">Het bevat ook Hallo mogelijkheid toostore lokale schijf kopieën voor snelle doelstellingen voor hersteltijd (RTO) en toostore kopieert tooAzure voor het bewaren van voordelige, op lange termijn.</span><span class="sxs-lookup"><span data-stu-id="65114-108">It also provides hello capability toostore local disk copies for quick recovery-time objectives (RTO) and toostore copies tooAzure for economical, long-term retention.</span></span>

## <a name="sharepoint-supported-versions-and-related-protection-scenarios"></a><span data-ttu-id="65114-109">SharePoint ondersteunde versies en gerelateerde beveiligingsscenario 's</span><span class="sxs-lookup"><span data-stu-id="65114-109">SharePoint supported versions and related protection scenarios</span></span>
<span data-ttu-id="65114-110">Azure Backup voor DPM ondersteunt Hallo volgen scenario's:</span><span class="sxs-lookup"><span data-stu-id="65114-110">Azure Backup for DPM supports hello following scenarios:</span></span>

| <span data-ttu-id="65114-111">Workload</span><span class="sxs-lookup"><span data-stu-id="65114-111">Workload</span></span> | <span data-ttu-id="65114-112">Versie</span><span class="sxs-lookup"><span data-stu-id="65114-112">Version</span></span> | <span data-ttu-id="65114-113">SharePoint-implementatie</span><span class="sxs-lookup"><span data-stu-id="65114-113">SharePoint deployment</span></span> | <span data-ttu-id="65114-114">Beveiliging en herstel</span><span class="sxs-lookup"><span data-stu-id="65114-114">Protection and recovery</span></span> |
| --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="65114-115">SharePoint</span><span class="sxs-lookup"><span data-stu-id="65114-115">SharePoint</span></span> |<span data-ttu-id="65114-116">SharePoint 2013, SharePoint 2010, SharePoint 2007 SharePoint 3.0</span><span class="sxs-lookup"><span data-stu-id="65114-116">SharePoint 2013, SharePoint 2010, SharePoint 2007, SharePoint 3.0</span></span> |<span data-ttu-id="65114-117">SharePoint geïmplementeerd als een fysieke server of Hyper-V/VMware virtuele machine</span><span class="sxs-lookup"><span data-stu-id="65114-117">SharePoint deployed as a physical server or Hyper-V/VMware virtual machine</span></span> <br> -------------- <br> <span data-ttu-id="65114-118">De Sqlalwayson</span><span class="sxs-lookup"><span data-stu-id="65114-118">SQL AlwaysOn</span></span> | <span data-ttu-id="65114-119">Opties voor herstel van SharePoint-Farm beveiligen: herstelfarm, database en bestand of lijstitem vanaf schijfherstelpunten.</span><span class="sxs-lookup"><span data-stu-id="65114-119">Protect SharePoint Farm recovery options: Recovery farm, database, and file or list item from disk recovery points.</span></span>  <span data-ttu-id="65114-120">Herstel van Azure herstelpunten farm en de database.</span><span class="sxs-lookup"><span data-stu-id="65114-120">Farm and database recovery from Azure recovery points.</span></span> |

## <a name="before-you-start"></a><span data-ttu-id="65114-121">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="65114-121">Before you start</span></span>
<span data-ttu-id="65114-122">Er zijn een aantal dingen die u moet tooconfirm voordat u back-up van een tooAzure van SharePoint-farm.</span><span class="sxs-lookup"><span data-stu-id="65114-122">There are a few things you need tooconfirm before you back up a SharePoint farm tooAzure.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="65114-123">Vereisten</span><span class="sxs-lookup"><span data-stu-id="65114-123">Prerequisites</span></span>
<span data-ttu-id="65114-124">Voordat u doorgaat, zorg ervoor dat u hebt [geïnstalleerd en voorbereid hello Azure Backup-Server](backup-azure-microsoft-azure-backup.md) tooprotect werkbelastingen.</span><span class="sxs-lookup"><span data-stu-id="65114-124">Before you proceed, make sure that you have [installed and prepared hello Azure Backup Server](backup-azure-microsoft-azure-backup.md) tooprotect workloads.</span></span>

### <a name="protection-agent"></a><span data-ttu-id="65114-125">Beveiligingsagent</span><span class="sxs-lookup"><span data-stu-id="65114-125">Protection agent</span></span>
<span data-ttu-id="65114-126">Hallo-beveiligingsagent moet worden geïnstalleerd op Hallo van server met SharePoint, Hallo-servers waarop SQL Server en alle andere servers die deel van de SharePoint-farm Hallo uitmaken.</span><span class="sxs-lookup"><span data-stu-id="65114-126">hello Protection agent must be installed on hello server that's running SharePoint, hello servers that are running SQL Server, and all other servers that are part of hello SharePoint farm.</span></span> <span data-ttu-id="65114-127">Voor meer informatie over het tooset up Hallo beveiligingsagent, Zie [Setup beveiligingsagent](https://technet.microsoft.com/library/hh758034\(v=sc.12\).aspx).</span><span class="sxs-lookup"><span data-stu-id="65114-127">For more information about how tooset up hello protection agent, see [Setup Protection Agent](https://technet.microsoft.com/library/hh758034\(v=sc.12\).aspx).</span></span>  <span data-ttu-id="65114-128">Hallo een uitzondering is dat u Hallo-agent op een enkel web-front-end (WFE)-server installeren.</span><span class="sxs-lookup"><span data-stu-id="65114-128">hello one exception is that you install hello agent only on a single web front end (WFE) server.</span></span> <span data-ttu-id="65114-129">DPM moet Hallo-agent op één WFE-server alleen tooserve als toegangspunt Hallo voor beveiliging.</span><span class="sxs-lookup"><span data-stu-id="65114-129">DPM needs hello agent on one WFE server only tooserve as hello entry point for protection.</span></span>

### <a name="sharepoint-farm"></a><span data-ttu-id="65114-130">SharePoint-farm</span><span class="sxs-lookup"><span data-stu-id="65114-130">SharePoint farm</span></span>
<span data-ttu-id="65114-131">Voor elke 10 miljoen items in Hallo-farm, moet er ten minste 2 GB ruimte op volume Hallo waar Hallo MABS map zich bevindt.</span><span class="sxs-lookup"><span data-stu-id="65114-131">For every 10 million items in hello farm, there must be at least 2 GB of space on hello volume where hello MABS folder is located.</span></span> <span data-ttu-id="65114-132">Deze ruimte is vereist voor het genereren van de catalogus.</span><span class="sxs-lookup"><span data-stu-id="65114-132">This space is required for catalog generation.</span></span> <span data-ttu-id="65114-133">Genereren van de catalogus maakt voor MABS toorecover specifieke items (siteverzamelingen, sites, lijsten, documentbibliotheken, mappen, individuele documenten en lijstitems), een lijst van Hallo-URL's die zijn opgenomen in elke inhoudsdatabase.</span><span class="sxs-lookup"><span data-stu-id="65114-133">For MABS toorecover specific items (site collections, sites, lists, document libraries, folders, individual documents, and list items), catalog generation creates a list of hello URLs that are contained within each content database.</span></span> <span data-ttu-id="65114-134">U kunt Hallo lijst met URL's weergeven in Hallo herstelbaar item deelvenster in Hallo **herstel** taakgebied van MABS Administrator-Console.</span><span class="sxs-lookup"><span data-stu-id="65114-134">You can view hello list of URLs in hello recoverable item pane in hello **Recovery** task area of MABS Administrator Console.</span></span>

### <a name="sql-server"></a><span data-ttu-id="65114-135">SQL Server</span><span class="sxs-lookup"><span data-stu-id="65114-135">SQL Server</span></span>
<span data-ttu-id="65114-136">MABS wordt uitgevoerd als lokale systeemaccount.</span><span class="sxs-lookup"><span data-stu-id="65114-136">MABS runs as a LocalSystem account.</span></span> <span data-ttu-id="65114-137">tooback van SQL Server-databases MABS moet een sysadmin-machtigingen op dat account voor Hallo-server die SQL Server wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="65114-137">tooback up SQL Server databases, MABS needs sysadmin privileges on that account for hello server that's running SQL Server.</span></span> <span data-ttu-id="65114-138">NT AUTHORITY\SYSTEM te ingesteld*sysadmin* op Hallo-server die SQL Server wordt uitgevoerd voordat u een back-up.</span><span class="sxs-lookup"><span data-stu-id="65114-138">Set NT AUTHORITY\SYSTEM too*sysadmin* on hello server that's running SQL Server before you back it up.</span></span>

<span data-ttu-id="65114-139">Als de SharePoint-farm Hallo SQL Server-databases die zijn geconfigureerd met SQL Server-aliassen, installeert u Hallo SQL Server-clientonderdelen op Hallo front-endwebserver die MABS beveiligt.</span><span class="sxs-lookup"><span data-stu-id="65114-139">If hello SharePoint farm has SQL Server databases that are configured with SQL Server aliases, install hello SQL Server client components on hello front-end Web server that MABS will protect.</span></span>

### <a name="sharepoint-server"></a><span data-ttu-id="65114-140">SharePoint Server</span><span class="sxs-lookup"><span data-stu-id="65114-140">SharePoint Server</span></span>
<span data-ttu-id="65114-141">Terwijl de prestaties zijn afhankelijk van veel factoren zoals de grootte van de SharePoint-farm, algemene richtlijnen kunt één MABS beveiligen een SharePoint-farm 25 TB.</span><span class="sxs-lookup"><span data-stu-id="65114-141">While performance depends on many factors such as size of SharePoint farm, as general guidance one MABS can protect a 25 TB SharePoint farm.</span></span>

### <a name="whats-not-supported"></a><span data-ttu-id="65114-142">Wat wordt er niet ondersteund</span><span class="sxs-lookup"><span data-stu-id="65114-142">What's not supported</span></span>
* <span data-ttu-id="65114-143">MABS die een SharePoint-farm beveiligt biedt geen bescherming zoekindexen of toepassing-servicedatabases.</span><span class="sxs-lookup"><span data-stu-id="65114-143">MABS that protects a SharePoint farm does not protect search indexes or application service databases.</span></span> <span data-ttu-id="65114-144">U moet tooconfigure Hallo beveiliging van deze databases afzonderlijk.</span><span class="sxs-lookup"><span data-stu-id="65114-144">You will need tooconfigure hello protection of these databases separately.</span></span>
* <span data-ttu-id="65114-145">MABS biedt geen back-up van de SharePoint SQL Server-databases die worden gehost op Servershares van scale-out bestandsserver (SOFS).</span><span class="sxs-lookup"><span data-stu-id="65114-145">MABS does not provide backup of SharePoint SQL Server databases that are hosted on scale-out file server (SOFS) shares.</span></span>

## <a name="configure-sharepoint-protection"></a><span data-ttu-id="65114-146">SharePoint-beveiliging configureren</span><span class="sxs-lookup"><span data-stu-id="65114-146">Configure SharePoint protection</span></span>
<span data-ttu-id="65114-147">Voordat u MABS tooprotect SharePoint gebruiken kunt, moet u Hallo SharePoint VSS Writer-service (WSS Writer-service) configureren met behulp van **ConfigureSharePoint.exe**.</span><span class="sxs-lookup"><span data-stu-id="65114-147">Before you can use MABS tooprotect SharePoint, you must configure hello SharePoint VSS Writer service (WSS Writer service) by using **ConfigureSharePoint.exe**.</span></span>

<span data-ttu-id="65114-148">U vindt **ConfigureSharePoint.exe** in Hallo [MABS Installation Path] \bin map op de front-endwebserver Hallo.</span><span class="sxs-lookup"><span data-stu-id="65114-148">You can find **ConfigureSharePoint.exe** in hello [MABS Installation Path]\bin folder on hello front-end web server.</span></span> <span data-ttu-id="65114-149">Dit hulpprogramma biedt Hallo beveiligingsagent met Hallo referenties voor Hallo SharePoint-farm.</span><span class="sxs-lookup"><span data-stu-id="65114-149">This tool provides hello protection agent with hello credentials for hello SharePoint farm.</span></span> <span data-ttu-id="65114-150">U uitvoeren deze op één WFE-server.</span><span class="sxs-lookup"><span data-stu-id="65114-150">You run it on a single WFE server.</span></span> <span data-ttu-id="65114-151">Als u meerdere WFE-servers hebt, selecteert u slechts één wanneer u een beveiligingsgroep configureert.</span><span class="sxs-lookup"><span data-stu-id="65114-151">If you have multiple WFE servers, select just one when you configure a protection group.</span></span>

### <a name="tooconfigure-hello-sharepoint-vss-writer-service"></a><span data-ttu-id="65114-152">tooconfigure hello SharePoint VSS Writer-service</span><span class="sxs-lookup"><span data-stu-id="65114-152">tooconfigure hello SharePoint VSS Writer service</span></span>
1. <span data-ttu-id="65114-153">Ga te op Hallo WFE-server bij een opdrachtprompt \bin\ [installatielocatie MABS]</span><span class="sxs-lookup"><span data-stu-id="65114-153">On hello WFE server, at a command prompt, go too[MABS installation location]\bin\\</span></span>
2. <span data-ttu-id="65114-154">Voer ConfigureSharePoint - EnableSharePointProtection.</span><span class="sxs-lookup"><span data-stu-id="65114-154">Enter ConfigureSharePoint -EnableSharePointProtection.</span></span>
3. <span data-ttu-id="65114-155">Geef beheerdersreferenties Hallo-farm.</span><span class="sxs-lookup"><span data-stu-id="65114-155">Enter hello farm administrator credentials.</span></span> <span data-ttu-id="65114-156">Deze account moet lid zijn van Hallo lokale groep Administrators op Hallo WFE-server.</span><span class="sxs-lookup"><span data-stu-id="65114-156">This account should be a member of hello local Administrator group on hello WFE server.</span></span> <span data-ttu-id="65114-157">Als de farmbeheerder Hallo niet een lokale beheerder grant Hallo volgende machtigingen op Hallo WFE-server:</span><span class="sxs-lookup"><span data-stu-id="65114-157">If hello farm administrator isn’t a local admin grant hello following permissions on hello WFE server:</span></span>
   * <span data-ttu-id="65114-158">Verleen Hallo WSS_Admin_WPG-groep volledige controle toohello DPM map (% Program Files%\Microsoft Azure Backup\DPM).</span><span class="sxs-lookup"><span data-stu-id="65114-158">Grant hello WSS_Admin_WPG group full control toohello DPM folder (%Program Files%\Microsoft Azure Backup\DPM).</span></span>
   * <span data-ttu-id="65114-159">Verleen Hallo WSS_Admin_WPG-groep leestoegang toohello DPM registersleutel (HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Data Protection Manager).</span><span class="sxs-lookup"><span data-stu-id="65114-159">Grant hello WSS_Admin_WPG group read access toohello DPM Registry key (HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Data Protection Manager).</span></span>

> [!NOTE]
> <span data-ttu-id="65114-160">U moet toorerun ConfigureSharePoint.exe wanneer er een wijziging in de beheerdersreferenties van Hallo SharePoint-farm.</span><span class="sxs-lookup"><span data-stu-id="65114-160">You’ll need toorerun ConfigureSharePoint.exe whenever there’s a change in hello SharePoint farm administrator credentials.</span></span>
>
>

## <a name="back-up-a-sharepoint-farm-by-using-mabs"></a><span data-ttu-id="65114-161">Back-up van een SharePoint-farm met behulp van MABS</span><span class="sxs-lookup"><span data-stu-id="65114-161">Back up a SharePoint farm by using MABS</span></span>
<span data-ttu-id="65114-162">Nadat u hebt MABS en Hallo SharePoint-farm zoals hierboven is geconfigureerd, kan SharePoint worden beveiligd door MABS.</span><span class="sxs-lookup"><span data-stu-id="65114-162">After you have configured MABS and hello SharePoint farm as explained previously, SharePoint can be protected by MABS.</span></span>

### <a name="tooprotect-a-sharepoint-farm"></a><span data-ttu-id="65114-163">tooprotect een SharePoint-farm</span><span class="sxs-lookup"><span data-stu-id="65114-163">tooprotect a SharePoint farm</span></span>
1. <span data-ttu-id="65114-164">Van Hallo **beveiliging** tabblad Hallo MABS Administrator-Console klikt u op **nieuw**.</span><span class="sxs-lookup"><span data-stu-id="65114-164">From hello **Protection** tab of hello MABS Administrator Console, click **New**.</span></span>
    <span data-ttu-id="65114-165">![Tabblad voor nieuwe beveiliging](./media/backup-azure-backup-sharepoint/dpm-new-protection-tab.png)</span><span class="sxs-lookup"><span data-stu-id="65114-165">![New Protection Tab](./media/backup-azure-backup-sharepoint/dpm-new-protection-tab.png)</span></span>
2. <span data-ttu-id="65114-166">Op Hallo **Type beveiligingsgroep selecteren** pagina Hallo **nieuwe beveiligingsgroep maken** wizard, selecteer **Servers**, en klik vervolgens op **volgende** .</span><span class="sxs-lookup"><span data-stu-id="65114-166">On hello **Select Protection Group Type** page of hello **Create New Protection Group** wizard, select **Servers**, and then click **Next**.</span></span>

    ![Type beveiligingsgroep selecteren](./media/backup-azure-backup-sharepoint/select-protection-group-type.png)
3. <span data-ttu-id="65114-168">Op Hallo **groepsleden selecteren** scherm, het selectievakje selecteert Hallo voor Hallo SharePoint server tooprotect en klik op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="65114-168">On hello **Select Group Members** screen, select hello check box for hello SharePoint server you want tooprotect and click **Next**.</span></span>

    ![Groepsleden selecteren](./media/backup-azure-backup-sharepoint/select-group-members2.png)

   > [!NOTE]
   > <span data-ttu-id="65114-170">Met de Hallo-beveiligingsagent is geïnstalleerd, kunt u Hallo-server in de wizard Hallo zien.</span><span class="sxs-lookup"><span data-stu-id="65114-170">With hello protection agent installed, you can see hello server in hello wizard.</span></span> <span data-ttu-id="65114-171">MABS toont ook de structuur.</span><span class="sxs-lookup"><span data-stu-id="65114-171">MABS also shows its structure.</span></span> <span data-ttu-id="65114-172">Omdat u ConfigureSharePoint.exe hebt uitgevoerd, MABS communiceert met Hallo SharePoint VSS Writer-service en de bijbehorende SQL Server-databases en herkent Hallo SharePoint-farmstructuur, Hallo inhoudsdatabases, en alle bijbehorende items die zijn gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="65114-172">Because you ran ConfigureSharePoint.exe, MABS communicates with hello SharePoint VSS Writer service and its corresponding SQL Server databases and recognizes hello SharePoint farm structure, hello associated content databases, and any corresponding items.</span></span>
   >
   >
4. <span data-ttu-id="65114-173">Op Hallo **methode voor gegevensbeveiliging selecteren** pagina, voer de naam Hallo Hallo **beveiligingsgroep**, en selecteer de gewenste *beveiligingsmethode*.</span><span class="sxs-lookup"><span data-stu-id="65114-173">On hello **Select Data Protection Method** page, enter hello name of hello **Protection Group**, and select your preferred *protection methods*.</span></span> <span data-ttu-id="65114-174">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="65114-174">Click **Next**.</span></span>

    ![Methode voor gegevensbeveiliging selecteren](./media/backup-azure-backup-sharepoint/select-data-protection-method1.png)

   > [!NOTE]
   > <span data-ttu-id="65114-176">Hallo schijf beveiligingsmethode helpt toomeet korte hersteltijd doelstellingen.</span><span class="sxs-lookup"><span data-stu-id="65114-176">hello disk protection method helps toomeet short recovery-time objectives.</span></span>
   >
   >
5. <span data-ttu-id="65114-177">Op Hallo **Kortetermijndoelen opgeven** pagina, selecteer de gewenste **bewaartermijn** en als u wilt dat back-ups toooccur te identificeren.</span><span class="sxs-lookup"><span data-stu-id="65114-177">On hello **Specify Short-Term Goals** page, select your preferred **Retention range** and identify when you want backups toooccur.</span></span>

    ![Korte-termijndoelstellingen opgeven](./media/backup-azure-backup-sharepoint/specify-short-term-goals2.png)

   > [!NOTE]
   > <span data-ttu-id="65114-179">Omdat het herstel meestal nodig is voor gegevens die minder dan vijf dagen oud, we een bewaartermijn van vijf dagen op schijf geselecteerd en gewaarborgd dat Hallo back-up wordt uitgevoerd tijdens de niet-productieve uren, in dit voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="65114-179">Because recovery is most often required for data that's less than five days old, we selected a retention range of five days on disk and ensured that hello backup happens during non-production hours, for this example.</span></span>
   >
   >
6. <span data-ttu-id="65114-180">Hallo opslaggroepschijfruimte die voor het Hallo-beveiligingsgroep is toegewezen bekijken en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="65114-180">Review hello storage pool disk space allocated for hello protection group, and click then **Next**.</span></span>
7. <span data-ttu-id="65114-181">Voor elke beveiligingsgroep MABS schijfruimte toostore toewijst en replica's te beheren.</span><span class="sxs-lookup"><span data-stu-id="65114-181">For every protection group, MABS allocates disk space toostore and manage replicas.</span></span> <span data-ttu-id="65114-182">MABS moet op dit punt wordt een kopie van Hallo geselecteerd gegevens maken.</span><span class="sxs-lookup"><span data-stu-id="65114-182">At this point, MABS must create a copy of hello selected data.</span></span> <span data-ttu-id="65114-183">Selecteer hoe en wanneer u wilt dat Hallo replica is gemaakt en klik op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="65114-183">Select how and when you want hello replica created, and then click **Next**.</span></span>

    ![Methode voor het maken van replica selecteren](./media/backup-azure-backup-sharepoint/choose-replica-creation-method.png)

   > [!NOTE]
   > <span data-ttu-id="65114-185">toomake ervoor dat verkeer niet plaatsvindt, selecteer een tijdstip buiten productie-uren.</span><span class="sxs-lookup"><span data-stu-id="65114-185">toomake sure that network traffic is not effected, select a time outside production hours.</span></span>
   >
   >
8. <span data-ttu-id="65114-186">MABS wordt de gegevensintegriteit gewaarborgd door het uitvoeren van consistentiecontroles uit op Hallo replica.</span><span class="sxs-lookup"><span data-stu-id="65114-186">MABS ensures data integrity by performing consistency checks on hello replica.</span></span> <span data-ttu-id="65114-187">Er zijn twee opties beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="65114-187">There are two available options.</span></span> <span data-ttu-id="65114-188">U kunt definiëren een planning toorun consistentie te controleren of DPM consistentiecontroles uit op Hallo replica automatisch kan worden uitgevoerd wanneer het inconsistent wordt.</span><span class="sxs-lookup"><span data-stu-id="65114-188">You can define a schedule toorun consistency checks, or DPM can run consistency checks automatically on hello replica whenever it becomes inconsistent.</span></span> <span data-ttu-id="65114-189">Selecteer de gewenste optie en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="65114-189">Select your preferred option, and then click **Next**.</span></span>

    ![Consistentiecontrole](./media/backup-azure-backup-sharepoint/consistency-check.png)
9. <span data-ttu-id="65114-191">Op Hallo **gegevens voor Online beveiliging opgeven** pagina, selecteert u Hallo SharePoint-farm wilt tooprotect en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="65114-191">On hello **Specify Online Protection Data** page, select hello SharePoint farm that you want tooprotect, and then click **Next**.</span></span>

    ![DPM SharePoint Protection1](./media/backup-azure-backup-sharepoint/select-online-protection1.png)
10. <span data-ttu-id="65114-193">Op Hallo **Online back-upschema opgeven** pagina, selecteer uw voorkeursplanning en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="65114-193">On hello **Specify Online Backup Schedule** page, select your preferred schedule, and then click **Next**.</span></span>

    ![Online_backup_schedule](./media/backup-azure-backup-sharepoint/specify-online-backup-schedule.png)

    > [!NOTE]
    > <span data-ttu-id="65114-195">MABS biedt een maximum van twee tooAzure voor dagelijkse back-ups van Hallo vervolgens beschikbaar laatste schijf back-up herstelpunt.</span><span class="sxs-lookup"><span data-stu-id="65114-195">MABS provides a maximum of two daily backups tooAzure from hello then available latest disk backup point.</span></span> <span data-ttu-id="65114-196">Azure Backup kunt ook bepalen Hallo hoeveelheid WAN-bandbreedte die kan worden gebruikt voor back-ups in piek- en daluren met behulp van [Azure back-up netwerkbeperking](https://azure.microsoft.com/documentation/articles/backup-configure-vault/#enable-network-throttling).</span><span class="sxs-lookup"><span data-stu-id="65114-196">Azure Backup can also control hello amount of WAN bandwidth that can be used for backups in peak and off-peak hours by using [Azure Backup Network Throttling](https://azure.microsoft.com/documentation/articles/backup-configure-vault/#enable-network-throttling).</span></span>
    >
    >
11. <span data-ttu-id="65114-197">Afhankelijk van de back-upschema Hallo die u hebt geselecteerd, op Hallo **Online bewaarbeleid opgeven** pagina, selecteer Hallo bewaarbeleid voor dagelijkse, wekelijkse, maandelijkse en jaarlijkse back-uppunten.</span><span class="sxs-lookup"><span data-stu-id="65114-197">Depending on hello backup schedule that you selected, on hello **Specify Online Retention Policy** page, select hello retention policy for daily, weekly, monthly, and yearly backup points.</span></span>

    ![Online_retention_policy](./media/backup-azure-backup-sharepoint/specify-online-retention.png)

    > [!NOTE]
    > <span data-ttu-id="65114-199">Een opa-vader-zoon bewaarschema waarin een andere bewaarbeleid kan worden gekozen MABS gebruikt voor andere back-uppunten.</span><span class="sxs-lookup"><span data-stu-id="65114-199">MABS uses a grandfather-father-son retention scheme in which a different retention policy can be chosen for different backup points.</span></span>
    >
    >
12. <span data-ttu-id="65114-200">Vergelijkbare toodisk een eerste verwijzing punt replica moet toobe gemaakt in Azure.</span><span class="sxs-lookup"><span data-stu-id="65114-200">Similar toodisk, an initial reference point replica needs toobe created in Azure.</span></span> <span data-ttu-id="65114-201">Selecteer uw voorkeursoptie toocreate een tooAzure eerste back-up en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="65114-201">Select your preferred option toocreate an initial backup copy tooAzure, and then click **Next**.</span></span>

    ![Online_replica](./media/backup-azure-backup-sharepoint/online-replication.png)
13. <span data-ttu-id="65114-203">Controleer de geselecteerde instellingen op Hallo **samenvatting** pagina en klik vervolgens op **groep maken**.</span><span class="sxs-lookup"><span data-stu-id="65114-203">Review your selected settings on hello **Summary** page, and then click **Create Group**.</span></span> <span data-ttu-id="65114-204">U ziet een bericht nadat Hallo-beveiligingsgroep is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="65114-204">You will see a success message after hello protection group has been created.</span></span>

    ![Samenvatting](./media/backup-azure-backup-sharepoint/summary.png)

## <a name="restore-a-sharepoint-item-from-disk-by-using-mabs"></a><span data-ttu-id="65114-206">Een SharePoint-item terugzetten vanaf schijf met MABS</span><span class="sxs-lookup"><span data-stu-id="65114-206">Restore a SharePoint item from disk by using MABS</span></span>
<span data-ttu-id="65114-207">Hallo in Hallo voorbeeld te volgen, *herstellen van SharePoint-item* per ongeluk is verwijderd en moet toobe hersteld.</span><span class="sxs-lookup"><span data-stu-id="65114-207">In hello following example, hello *Recovering SharePoint item* has been accidentally deleted and needs toobe recovered.</span></span>
<span data-ttu-id="65114-208">![MABS SharePoint Protection4](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection5.png)</span><span class="sxs-lookup"><span data-stu-id="65114-208">![MABS SharePoint Protection4](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection5.png)</span></span>

1. <span data-ttu-id="65114-209">Open Hallo **DPM Administrator-Console**.</span><span class="sxs-lookup"><span data-stu-id="65114-209">Open hello **DPM Administrator Console**.</span></span> <span data-ttu-id="65114-210">Alle SharePoint-farms die zijn beveiligd door DPM worden weergegeven in Hallo **beveiliging** tabblad.</span><span class="sxs-lookup"><span data-stu-id="65114-210">All SharePoint farms that are protected by DPM are shown in hello **Protection** tab.</span></span>

    ![MABS SharePoint Protection3](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection4.png)
2. <span data-ttu-id="65114-212">Selecteer Hallo-toobegin toorecover Hallo item **herstel** tabblad.</span><span class="sxs-lookup"><span data-stu-id="65114-212">toobegin toorecover hello item, select hello **Recovery** tab.</span></span>

    ![MABS SharePoint Protection5](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection6.png)
3. <span data-ttu-id="65114-214">U kunt zoeken in SharePoint voor *herstellen van SharePoint-item* verwijzen met behulp van een zoekopdracht op basis van een jokerteken binnen een herstelbewerking bereik.</span><span class="sxs-lookup"><span data-stu-id="65114-214">You can search SharePoint for *Recovering SharePoint item* by using a wildcard-based search within a recovery point range.</span></span>

    ![MABS SharePoint Protection6](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection7.png)
4. <span data-ttu-id="65114-216">Selecteer de juiste herstelpunt Hallo in zoekresultaten Hallo, met de rechtermuisknop op het Hallo-item en selecteer **herstellen**.</span><span class="sxs-lookup"><span data-stu-id="65114-216">Select hello appropriate recovery point from hello search results, right-click hello item, and then select **Recover**.</span></span>
5. <span data-ttu-id="65114-217">U kunt ook door verschillende herstelpunten bladeren en selecteren van een database of item toorecover.</span><span class="sxs-lookup"><span data-stu-id="65114-217">You can also browse through various recovery points and select a database or item toorecover.</span></span> <span data-ttu-id="65114-218">Selecteer **datum > hersteltijd**, en selecteer vervolgens de juiste Hallo **Database > SharePoint-farm > herstelpunt > Item**.</span><span class="sxs-lookup"><span data-stu-id="65114-218">Select **Date > Recovery time**, and then select hello correct **Database > SharePoint farm > Recovery point > Item**.</span></span>

    ![MABS SharePoint Protection7](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection8.png)
6. <span data-ttu-id="65114-220">Hallo-item met de rechtermuisknop en selecteer vervolgens **herstellen** tooopen hello **Herstelwizard**.</span><span class="sxs-lookup"><span data-stu-id="65114-220">Right-click hello item, and then select **Recover** tooopen hello **Recovery Wizard**.</span></span> <span data-ttu-id="65114-221">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="65114-221">Click **Next**.</span></span>

    ![Selectie voor herstel controleren](./media/backup-azure-backup-sharepoint/review-recovery-selection.png)
7. <span data-ttu-id="65114-223">Selecteer Hallo type herstel dat u tooperform wilt en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="65114-223">Select hello type of recovery that you want tooperform, and then click **Next**.</span></span>

    ![Hersteltype](./media/backup-azure-backup-sharepoint/select-recovery-type.png)

   > [!NOTE]
   > <span data-ttu-id="65114-225">selectie van Hallo **toooriginal herstellen** in Hallo voorbeeld Hallo item toohello oorspronkelijke SharePoint-site herstelt.</span><span class="sxs-lookup"><span data-stu-id="65114-225">hello selection of **Recover toooriginal** in hello example recovers hello item toohello original SharePoint site.</span></span>
   >
   >
8. <span data-ttu-id="65114-226">Selecteer Hallo **herstelproces** dat u wilt dat toouse.</span><span class="sxs-lookup"><span data-stu-id="65114-226">Select hello **Recovery Process** that you want toouse.</span></span>

   * <span data-ttu-id="65114-227">Selecteer **herstellen zonder herstelfarm** als Hallo SharePoint-farm is niet gewijzigd en Hallo dezelfde zijn als Hallo herstel die wijst wordt hersteld.</span><span class="sxs-lookup"><span data-stu-id="65114-227">Select **Recover without using a recovery farm** if hello SharePoint farm has not changed and is hello same as hello recovery point that is being restored.</span></span>
   * <span data-ttu-id="65114-228">Selecteer **herstellen met behulp van een herstelfarm** als Hallo SharePoint-farm is gewijzigd sinds Hallo herstelpunt is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="65114-228">Select **Recover using a recovery farm** if hello SharePoint farm has changed since hello recovery point was created.</span></span>

     ![Herstelproces](./media/backup-azure-backup-sharepoint/recovery-process.png)
9. <span data-ttu-id="65114-230">Een SQL Server-exemplaar locatie toorecover Hallo faseringsdatabase tijdelijk, en bieden een tijdelijke bestandsshare op MABS en Hallo-server waarop SharePoint toorecover Hallo-item wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="65114-230">Provide a staging SQL Server instance location toorecover hello database temporarily, and provide a staging file share on MABS and hello server that's running SharePoint toorecover hello item.</span></span>

    ![Fasering Location1](./media/backup-azure-backup-sharepoint/staging-location1.png)

    <span data-ttu-id="65114-232">MABS koppelt Hallo inhoudsdatabase die als host voor Hallo SharePoint-item toohello tijdelijke SQL Server-exemplaar fungeert.</span><span class="sxs-lookup"><span data-stu-id="65114-232">MABS attaches hello content database that is hosting hello SharePoint item toohello temporary SQL Server instance.</span></span> <span data-ttu-id="65114-233">Van de inhoudsdatabase hello, het Hallo-item wordt hersteld en plaatst deze op Hallo tijdelijke bestandslocatie op MABS.</span><span class="sxs-lookup"><span data-stu-id="65114-233">From hello content database, it recovers hello item and puts it on hello staging file location on MABS.</span></span> <span data-ttu-id="65114-234">Hallo hersteld artikel op Hallo faseringslocatie nu behoeften toobe geëxporteerd toohello tijdelijke locatie op Hallo SharePoint-farm.</span><span class="sxs-lookup"><span data-stu-id="65114-234">hello recovered item that's on hello staging location now needs toobe exported toohello staging location on hello SharePoint farm.</span></span>

    ![Fasering Location2](./media/backup-azure-backup-sharepoint/staging-location2.png)
10. <span data-ttu-id="65114-236">Selecteer **herstelopties opgeven**, en toepassen van beveiliging instellingen toohello SharePoint-farm of toepassen van beveiligingsinstellingen Hallo Hallo herstelpunt werd gemaakt.</span><span class="sxs-lookup"><span data-stu-id="65114-236">Select **Specify recovery options**, and apply security settings toohello SharePoint farm or apply hello security settings of hello recovery point.</span></span> <span data-ttu-id="65114-237">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="65114-237">Click **Next**.</span></span>

    ![Opties voor herstel](./media/backup-azure-backup-sharepoint/recovery-options.png)

    > [!NOTE]
    > <span data-ttu-id="65114-239">U kunt toothrottle Hallo netwerkbandbreedte gebruikt.</span><span class="sxs-lookup"><span data-stu-id="65114-239">You can choose toothrottle hello network bandwidth usage.</span></span> <span data-ttu-id="65114-240">Hierdoor minimaliseert impact toohello productieserver tijdens de productie-uren.</span><span class="sxs-lookup"><span data-stu-id="65114-240">This minimizes impact toohello production server during production hours.</span></span>
    >
    >
11. <span data-ttu-id="65114-241">Hallo samenvattingsinformatie controleren en klik vervolgens op **herstellen** toobegin herstellen van Hallo-bestand.</span><span class="sxs-lookup"><span data-stu-id="65114-241">Review hello summary information, and then click **Recover** toobegin recovery of hello file.</span></span>

    ![Samenvatting van herstel](./media/backup-azure-backup-sharepoint/recovery-summary.png)
12. <span data-ttu-id="65114-243">Nu selecteren Hallo **bewaking** tabblad in Hallo **MABS Administrator-Console** tooview hello **Status** Hallo herstel.</span><span class="sxs-lookup"><span data-stu-id="65114-243">Now select hello **Monitoring** tab in hello **MABS Administrator Console** tooview hello **Status** of hello recovery.</span></span>

    ![Herstelstatus](./media/backup-azure-backup-sharepoint/recovery-monitoring.png)

    > [!NOTE]
    > <span data-ttu-id="65114-245">Hallo-bestand is nu hersteld.</span><span class="sxs-lookup"><span data-stu-id="65114-245">hello file is now restored.</span></span> <span data-ttu-id="65114-246">U kunt Hallo SharePoint-site toocheck Hallo hersteld bestand vernieuwen.</span><span class="sxs-lookup"><span data-stu-id="65114-246">You can refresh hello SharePoint site toocheck hello restored file.</span></span>
    >
    >

## <a name="restore-a-sharepoint-database-from-azure-by-using-dpm"></a><span data-ttu-id="65114-247">Een SharePoint-database herstellen van Azure met DPM</span><span class="sxs-lookup"><span data-stu-id="65114-247">Restore a SharePoint database from Azure by using DPM</span></span>
1. <span data-ttu-id="65114-248">een SharePoint-inhoudsdatabase toorecover bladeren door verschillende herstelpunten (zoals eerder is weergegeven) en selecteer Hallo herstelpunt dat u wilt dat toorestore.</span><span class="sxs-lookup"><span data-stu-id="65114-248">toorecover a SharePoint content database, browse through various recovery points (as shown previously), and select hello recovery point that you want toorestore.</span></span>

    ![MABS SharePoint Protection8](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection9.png)
2. <span data-ttu-id="65114-250">Dubbelklik op Hallo SharePoint punt tooshow Hallo beschikbaar SharePoint-catalogus herstelgegevens.</span><span class="sxs-lookup"><span data-stu-id="65114-250">Double-click hello SharePoint recovery point tooshow hello available SharePoint catalog information.</span></span>

   > [!NOTE]
   > <span data-ttu-id="65114-251">Omdat de SharePoint-farm Hallo voor lange bewaartermijn in Azure wordt beveiligd, is er is geen catalogusinformatie (metagegevens) beschikbaar op MABS.</span><span class="sxs-lookup"><span data-stu-id="65114-251">Because hello SharePoint farm is protected for long-term retention in Azure, no catalog information (metadata) is available on MABS.</span></span> <span data-ttu-id="65114-252">Als gevolg hiervan als een SharePoint-inhoudsdatabase punt in tijd toobe hersteld moet, moet u toocatalog Hallo SharePoint-farm opnieuw.</span><span class="sxs-lookup"><span data-stu-id="65114-252">As a result, whenever a point-in-time SharePoint content database needs toobe recovered, you need toocatalog hello SharePoint farm again.</span></span>
   >
   >
3. <span data-ttu-id="65114-253">Klik op **opnieuw catalogiseren**.</span><span class="sxs-lookup"><span data-stu-id="65114-253">Click **Re-catalog**.</span></span>

    ![MABS SharePoint Protection10](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection12.png)

    <span data-ttu-id="65114-255">Hallo **Cloud opnieuw catalogiseren** statusvenster wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="65114-255">hello **Cloud Recatalog** status window opens.</span></span>

    ![MABS SharePoint Protection11](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection13.png)

    <span data-ttu-id="65114-257">Nadat catalogiseren is voltooid, Hallo status verandert te*geslaagd*.</span><span class="sxs-lookup"><span data-stu-id="65114-257">After cataloging is finished, hello status changes too*Success*.</span></span> <span data-ttu-id="65114-258">Klik op **Sluiten**.</span><span class="sxs-lookup"><span data-stu-id="65114-258">Click **Close**.</span></span>

    ![MABS SharePoint Protection12](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection14.png)
4. <span data-ttu-id="65114-260">Klik op Hallo SharePoint-object wordt weergegeven in Hallo MABS **herstel** tabblad tooget Hallo inhoudsdatabase structuur.</span><span class="sxs-lookup"><span data-stu-id="65114-260">Click hello SharePoint object shown in hello MABS **Recovery** tab tooget hello content database structure.</span></span> <span data-ttu-id="65114-261">Met de rechtermuisknop op het Hallo-item en klik vervolgens op **herstellen**.</span><span class="sxs-lookup"><span data-stu-id="65114-261">Right-click hello item, and then click **Recover**.</span></span>

    ![MABS SharePoint Protection13](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection15.png)
5. <span data-ttu-id="65114-263">Op dit moment volgen Hallo [herstel stappen eerder in dit artikel](#restore-a-sharepoint-item-from-disk-using-dpm) toorecover een SharePoint-inhoudsdatabase van de schijf.</span><span class="sxs-lookup"><span data-stu-id="65114-263">At this point, follow hello [recovery steps earlier in this article](#restore-a-sharepoint-item-from-disk-using-dpm) toorecover a SharePoint content database from disk.</span></span>

## <a name="faqs"></a><span data-ttu-id="65114-264">Veelgestelde vragen</span><span class="sxs-lookup"><span data-stu-id="65114-264">FAQs</span></span>
<span data-ttu-id="65114-265">V: kan ik een SharePoint-item toohello oorspronkelijke locatie herstellen als SharePoint is geconfigureerd met behulp van SQL AlwaysOn (met beveiliging op schijf)?</span><span class="sxs-lookup"><span data-stu-id="65114-265">Q: Can I recover a SharePoint item toohello original location if SharePoint is configured by using SQL AlwaysOn (with protection on disk)?</span></span><br>
<span data-ttu-id="65114-266">A: Hallo-item kan Ja, de herstelde toohello oorspronkelijke SharePoint-site zijn.</span><span class="sxs-lookup"><span data-stu-id="65114-266">A: Yes, hello item can be recovered toohello original SharePoint site.</span></span>

<span data-ttu-id="65114-267">V: kan ik een SharePoint-database toohello oorspronkelijke locatie herstellen als SharePoint met behulp van SQL AlwaysOn is geconfigureerd?</span><span class="sxs-lookup"><span data-stu-id="65114-267">Q: Can I recover a SharePoint database toohello original location if SharePoint is configured by using SQL AlwaysOn?</span></span><br>
<span data-ttu-id="65114-268">A: omdat SharePoint-databases zijn geconfigureerd in de SQL AlwaysOn, kan deze niet worden gewijzigd als Hallo beschikbaarheidsgroep wordt verwijderd.</span><span class="sxs-lookup"><span data-stu-id="65114-268">A: Because SharePoint databases are configured in SQL AlwaysOn, they cannot be modified unless hello availability group is removed.</span></span> <span data-ttu-id="65114-269">Als gevolg hiervan kan MABS niet een database toohello oorspronkelijke locatie herstellen.</span><span class="sxs-lookup"><span data-stu-id="65114-269">As a result, MABS cannot restore a database toohello original location.</span></span> <span data-ttu-id="65114-270">U kunt een SQL Server-exemplaar van SQL Server-database tooanother herstellen.</span><span class="sxs-lookup"><span data-stu-id="65114-270">You can recover a SQL Server database tooanother SQL Server instance.</span></span>

## <a name="next-steps"></a><span data-ttu-id="65114-271">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="65114-271">Next steps</span></span>
* <span data-ttu-id="65114-272">Meer informatie over MABS beveiliging van SharePoint - Zie [Video Series - DPM-beveiliging van SharePoint](http://channel9.msdn.com/Series/Azure-Backup/Microsoft-SCDPM-Protection-of-SharePoint-1-of-2-How-to-create-a-SharePoint-Protection-Group)</span><span class="sxs-lookup"><span data-stu-id="65114-272">Learn more about MABS Protection of SharePoint - see [Video Series - DPM Protection of SharePoint](http://channel9.msdn.com/Series/Azure-Backup/Microsoft-SCDPM-Protection-of-SharePoint-1-of-2-How-to-create-a-SharePoint-Protection-Group)</span></span>

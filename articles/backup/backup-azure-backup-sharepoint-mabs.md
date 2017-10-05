---
title: Gebruik Azure Backup-server naar de back-up van een SharePoint-farm naar Azure | Microsoft Docs
description: Azure Backup-Server gebruiken om back-up en herstellen van uw SharePoint-gegevens. In dit artikel bevat de informatie voor het configureren van uw SharePoint-farm zodat de gewenste gegevens kunnen worden opgeslagen in Azure. U kunt beveiligde SharePoint-gegevens terugzetten vanaf schijf of Azure.
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
ms.openlocfilehash: 3ed000affd326eb1bd7c99773ec021ad6e03cc3b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="back-up-a-sharepoint-farm-to-azure"></a><span data-ttu-id="0f1d5-105">Een back-up maken in Azure van een SharePoint-farm</span><span class="sxs-lookup"><span data-stu-id="0f1d5-105">Back up a SharePoint farm to Azure</span></span>
<span data-ttu-id="0f1d5-106">U back-up van een SharePoint-farm naar Microsoft Azure met behulp van Microsoft Azure Backup-Server (MABS) in ongeveer dezelfde manier als dat u back-up van andere gegevensbronnen.</span><span class="sxs-lookup"><span data-stu-id="0f1d5-106">You back up a SharePoint farm to Microsoft Azure by using Microsoft Azure Backup Server (MABS) in much the same way that you back up other data sources.</span></span> <span data-ttu-id="0f1d5-107">Azure Backup biedt flexibiliteit in het back-upschema maken het dagelijkse, wekelijkse, maandelijkse of jaarlijkse back-up verwijst en biedt u de bewaarperiode beleidsopties voor verschillende back-uppunten.</span><span class="sxs-lookup"><span data-stu-id="0f1d5-107">Azure Backup provides flexibility in the backup schedule to create daily, weekly, monthly, or yearly backup points and gives you retention policy options for various backup points.</span></span> <span data-ttu-id="0f1d5-108">Het biedt ook de mogelijkheid voor het opslaan van kopieën van de lokale schijf voor snelle doelstellingen voor hersteltijd (RTO) en voor het opslaan van kopieën naar Azure voor het bewaren van voordelige, op lange termijn.</span><span class="sxs-lookup"><span data-stu-id="0f1d5-108">It also provides the capability to store local disk copies for quick recovery-time objectives (RTO) and to store copies to Azure for economical, long-term retention.</span></span>

## <a name="sharepoint-supported-versions-and-related-protection-scenarios"></a><span data-ttu-id="0f1d5-109">SharePoint ondersteunde versies en gerelateerde beveiligingsscenario 's</span><span class="sxs-lookup"><span data-stu-id="0f1d5-109">SharePoint supported versions and related protection scenarios</span></span>
<span data-ttu-id="0f1d5-110">Azure Backup voor DPM ondersteunt de volgende scenario's:</span><span class="sxs-lookup"><span data-stu-id="0f1d5-110">Azure Backup for DPM supports the following scenarios:</span></span>

| <span data-ttu-id="0f1d5-111">Workload</span><span class="sxs-lookup"><span data-stu-id="0f1d5-111">Workload</span></span> | <span data-ttu-id="0f1d5-112">Versie</span><span class="sxs-lookup"><span data-stu-id="0f1d5-112">Version</span></span> | <span data-ttu-id="0f1d5-113">SharePoint-implementatie</span><span class="sxs-lookup"><span data-stu-id="0f1d5-113">SharePoint deployment</span></span> | <span data-ttu-id="0f1d5-114">Beveiliging en herstel</span><span class="sxs-lookup"><span data-stu-id="0f1d5-114">Protection and recovery</span></span> |
| --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="0f1d5-115">SharePoint</span><span class="sxs-lookup"><span data-stu-id="0f1d5-115">SharePoint</span></span> |<span data-ttu-id="0f1d5-116">SharePoint 2013, SharePoint 2010, SharePoint 2007 SharePoint 3.0</span><span class="sxs-lookup"><span data-stu-id="0f1d5-116">SharePoint 2013, SharePoint 2010, SharePoint 2007, SharePoint 3.0</span></span> |<span data-ttu-id="0f1d5-117">SharePoint geïmplementeerd als een fysieke server of Hyper-V/VMware virtuele machine</span><span class="sxs-lookup"><span data-stu-id="0f1d5-117">SharePoint deployed as a physical server or Hyper-V/VMware virtual machine</span></span> <br> -------------- <br> <span data-ttu-id="0f1d5-118">De Sqlalwayson</span><span class="sxs-lookup"><span data-stu-id="0f1d5-118">SQL AlwaysOn</span></span> | <span data-ttu-id="0f1d5-119">Opties voor herstel van SharePoint-Farm beveiligen: herstelfarm, database en bestand of lijstitem vanaf schijfherstelpunten.</span><span class="sxs-lookup"><span data-stu-id="0f1d5-119">Protect SharePoint Farm recovery options: Recovery farm, database, and file or list item from disk recovery points.</span></span>  <span data-ttu-id="0f1d5-120">Herstel van Azure herstelpunten farm en de database.</span><span class="sxs-lookup"><span data-stu-id="0f1d5-120">Farm and database recovery from Azure recovery points.</span></span> |

## <a name="before-you-start"></a><span data-ttu-id="0f1d5-121">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="0f1d5-121">Before you start</span></span>
<span data-ttu-id="0f1d5-122">Er zijn enkele dingen die u nodig om te bevestigen voordat u een SharePoint-farm naar Azure back-up.</span><span class="sxs-lookup"><span data-stu-id="0f1d5-122">There are a few things you need to confirm before you back up a SharePoint farm to Azure.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="0f1d5-123">Vereisten</span><span class="sxs-lookup"><span data-stu-id="0f1d5-123">Prerequisites</span></span>
<span data-ttu-id="0f1d5-124">Voordat u doorgaat, zorg ervoor dat u hebt [geïnstalleerd en de Azure Backup-Server voorbereid](backup-azure-microsoft-azure-backup.md) om workloads te beschermen.</span><span class="sxs-lookup"><span data-stu-id="0f1d5-124">Before you proceed, make sure that you have [installed and prepared the Azure Backup Server](backup-azure-microsoft-azure-backup.md) to protect workloads.</span></span>

### <a name="protection-agent"></a><span data-ttu-id="0f1d5-125">Beveiligingsagent</span><span class="sxs-lookup"><span data-stu-id="0f1d5-125">Protection agent</span></span>
<span data-ttu-id="0f1d5-126">De beveiligingsagent moet worden geïnstalleerd op de server waarop SharePoint, de servers waarop SQL Server en alle andere servers die deel van de SharePoint-farm uitmaken.</span><span class="sxs-lookup"><span data-stu-id="0f1d5-126">The Protection agent must be installed on the server that's running SharePoint, the servers that are running SQL Server, and all other servers that are part of the SharePoint farm.</span></span> <span data-ttu-id="0f1d5-127">Zie voor meer informatie over het instellen van de beveiligingsagent [Setup beveiligingsagent](https://technet.microsoft.com/library/hh758034\(v=sc.12\).aspx).</span><span class="sxs-lookup"><span data-stu-id="0f1d5-127">For more information about how to set up the protection agent, see [Setup Protection Agent](https://technet.microsoft.com/library/hh758034\(v=sc.12\).aspx).</span></span>  <span data-ttu-id="0f1d5-128">De enige uitzondering hierop is dat u de agent op een enkel web-front-end (WFE)-server installeren.</span><span class="sxs-lookup"><span data-stu-id="0f1d5-128">The one exception is that you install the agent only on a single web front end (WFE) server.</span></span> <span data-ttu-id="0f1d5-129">DPM moet de agent op één WFE-server alleen om te fungeren als het toegangspunt voor beveiliging.</span><span class="sxs-lookup"><span data-stu-id="0f1d5-129">DPM needs the agent on one WFE server only to serve as the entry point for protection.</span></span>

### <a name="sharepoint-farm"></a><span data-ttu-id="0f1d5-130">SharePoint-farm</span><span class="sxs-lookup"><span data-stu-id="0f1d5-130">SharePoint farm</span></span>
<span data-ttu-id="0f1d5-131">Voor elke 10 miljoen items in de farm, moet er minstens 2 GB aan ruimte op het volume waar de map MABS zich bevindt.</span><span class="sxs-lookup"><span data-stu-id="0f1d5-131">For every 10 million items in the farm, there must be at least 2 GB of space on the volume where the MABS folder is located.</span></span> <span data-ttu-id="0f1d5-132">Deze ruimte is vereist voor het genereren van de catalogus.</span><span class="sxs-lookup"><span data-stu-id="0f1d5-132">This space is required for catalog generation.</span></span> <span data-ttu-id="0f1d5-133">Genereren van de catalogus maakt voor MABS om specifieke items (siteverzamelingen, sites, lijsten, documentbibliotheken, mappen, individuele documenten en lijstitems) te herstellen, een lijst van de URL's die zijn opgenomen in elke inhoudsdatabase.</span><span class="sxs-lookup"><span data-stu-id="0f1d5-133">For MABS to recover specific items (site collections, sites, lists, document libraries, folders, individual documents, and list items), catalog generation creates a list of the URLs that are contained within each content database.</span></span> <span data-ttu-id="0f1d5-134">U kunt de lijst met URL's bekijken in het deelvenster herstelbaar item in de **herstel** taakgebied van MABS Administrator-Console.</span><span class="sxs-lookup"><span data-stu-id="0f1d5-134">You can view the list of URLs in the recoverable item pane in the **Recovery** task area of MABS Administrator Console.</span></span>

### <a name="sql-server"></a><span data-ttu-id="0f1d5-135">SQL Server</span><span class="sxs-lookup"><span data-stu-id="0f1d5-135">SQL Server</span></span>
<span data-ttu-id="0f1d5-136">MABS wordt uitgevoerd als lokale systeemaccount.</span><span class="sxs-lookup"><span data-stu-id="0f1d5-136">MABS runs as a LocalSystem account.</span></span> <span data-ttu-id="0f1d5-137">Als u wilt back-up van SQL Server-databases, moet MABS sysadmin-machtigingen op dat account voor de server die SQL Server wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="0f1d5-137">To back up SQL Server databases, MABS needs sysadmin privileges on that account for the server that's running SQL Server.</span></span> <span data-ttu-id="0f1d5-138">NT AUTHORITY\SYSTEM ingesteld op *sysadmin* op de server waarop SQL Server wordt uitgevoerd voordat u een back-up.</span><span class="sxs-lookup"><span data-stu-id="0f1d5-138">Set NT AUTHORITY\SYSTEM to *sysadmin* on the server that's running SQL Server before you back it up.</span></span>

<span data-ttu-id="0f1d5-139">Als de SharePoint-farm SQL Server-databases die zijn geconfigureerd met SQL Server-aliassen, installeert u de SQL Server-clientonderdelen op de front-endwebserver die MABS beveiligt.</span><span class="sxs-lookup"><span data-stu-id="0f1d5-139">If the SharePoint farm has SQL Server databases that are configured with SQL Server aliases, install the SQL Server client components on the front-end Web server that MABS will protect.</span></span>

### <a name="sharepoint-server"></a><span data-ttu-id="0f1d5-140">SharePoint Server</span><span class="sxs-lookup"><span data-stu-id="0f1d5-140">SharePoint Server</span></span>
<span data-ttu-id="0f1d5-141">Terwijl de prestaties zijn afhankelijk van veel factoren zoals de grootte van de SharePoint-farm, algemene richtlijnen kunt één MABS beveiligen een SharePoint-farm 25 TB.</span><span class="sxs-lookup"><span data-stu-id="0f1d5-141">While performance depends on many factors such as size of SharePoint farm, as general guidance one MABS can protect a 25 TB SharePoint farm.</span></span>

### <a name="whats-not-supported"></a><span data-ttu-id="0f1d5-142">Wat wordt er niet ondersteund</span><span class="sxs-lookup"><span data-stu-id="0f1d5-142">What's not supported</span></span>
* <span data-ttu-id="0f1d5-143">MABS die een SharePoint-farm beveiligt biedt geen bescherming zoekindexen of toepassing-servicedatabases.</span><span class="sxs-lookup"><span data-stu-id="0f1d5-143">MABS that protects a SharePoint farm does not protect search indexes or application service databases.</span></span> <span data-ttu-id="0f1d5-144">U moet de beveiliging van deze databases afzonderlijk te configureren.</span><span class="sxs-lookup"><span data-stu-id="0f1d5-144">You will need to configure the protection of these databases separately.</span></span>
* <span data-ttu-id="0f1d5-145">MABS biedt geen back-up van de SharePoint SQL Server-databases die worden gehost op Servershares van scale-out bestandsserver (SOFS).</span><span class="sxs-lookup"><span data-stu-id="0f1d5-145">MABS does not provide backup of SharePoint SQL Server databases that are hosted on scale-out file server (SOFS) shares.</span></span>

## <a name="configure-sharepoint-protection"></a><span data-ttu-id="0f1d5-146">SharePoint-beveiliging configureren</span><span class="sxs-lookup"><span data-stu-id="0f1d5-146">Configure SharePoint protection</span></span>
<span data-ttu-id="0f1d5-147">Voordat u MABS gebruiken kunt om SharePoint te beveiligen, moet u de SharePoint VSS Writer-service (WSS Writer-service) configureren met behulp van **ConfigureSharePoint.exe**.</span><span class="sxs-lookup"><span data-stu-id="0f1d5-147">Before you can use MABS to protect SharePoint, you must configure the SharePoint VSS Writer service (WSS Writer service) by using **ConfigureSharePoint.exe**.</span></span>

<span data-ttu-id="0f1d5-148">U vindt **ConfigureSharePoint.exe** in de map [MABS Installation Path] \bin op de front-endwebserver.</span><span class="sxs-lookup"><span data-stu-id="0f1d5-148">You can find **ConfigureSharePoint.exe** in the [MABS Installation Path]\bin folder on the front-end web server.</span></span> <span data-ttu-id="0f1d5-149">Dit hulpprogramma bevat de beveiligingsagent met de referenties voor de SharePoint-farm.</span><span class="sxs-lookup"><span data-stu-id="0f1d5-149">This tool provides the protection agent with the credentials for the SharePoint farm.</span></span> <span data-ttu-id="0f1d5-150">U uitvoeren deze op één WFE-server.</span><span class="sxs-lookup"><span data-stu-id="0f1d5-150">You run it on a single WFE server.</span></span> <span data-ttu-id="0f1d5-151">Als u meerdere WFE-servers hebt, selecteert u slechts één wanneer u een beveiligingsgroep configureert.</span><span class="sxs-lookup"><span data-stu-id="0f1d5-151">If you have multiple WFE servers, select just one when you configure a protection group.</span></span>

### <a name="to-configure-the-sharepoint-vss-writer-service"></a><span data-ttu-id="0f1d5-152">De SharePoint VSS Writer-service configureren</span><span class="sxs-lookup"><span data-stu-id="0f1d5-152">To configure the SharePoint VSS Writer service</span></span>
1. <span data-ttu-id="0f1d5-153">Op de WFE-server bij een opdrachtprompt, gaat u naar \bin\ [installatielocatie MABS]</span><span class="sxs-lookup"><span data-stu-id="0f1d5-153">On the WFE server, at a command prompt, go to [MABS installation location]\bin\\</span></span>
2. <span data-ttu-id="0f1d5-154">Voer ConfigureSharePoint - EnableSharePointProtection.</span><span class="sxs-lookup"><span data-stu-id="0f1d5-154">Enter ConfigureSharePoint -EnableSharePointProtection.</span></span>
3. <span data-ttu-id="0f1d5-155">Voer de referenties van de farmbeheerder.</span><span class="sxs-lookup"><span data-stu-id="0f1d5-155">Enter the farm administrator credentials.</span></span> <span data-ttu-id="0f1d5-156">Deze account moet lid zijn van de lokale groep Administrators op de WFE-server.</span><span class="sxs-lookup"><span data-stu-id="0f1d5-156">This account should be a member of the local Administrator group on the WFE server.</span></span> <span data-ttu-id="0f1d5-157">Als de farmbeheerder geen lokale beheerder de volgende machtigingen op de WFE-server toewijzen:</span><span class="sxs-lookup"><span data-stu-id="0f1d5-157">If the farm administrator isn’t a local admin grant the following permissions on the WFE server:</span></span>
   * <span data-ttu-id="0f1d5-158">Verleen de WSS_Admin_WPG-groep volledige controle naar de DPM-map (% Program Files%\Microsoft Azure Backup\DPM).</span><span class="sxs-lookup"><span data-stu-id="0f1d5-158">Grant the WSS_Admin_WPG group full control to the DPM folder (%Program Files%\Microsoft Azure Backup\DPM).</span></span>
   * <span data-ttu-id="0f1d5-159">De WSS_Admin_WPG-groep lezen toegang verlenen tot de DPM-registersleutel (HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Data Protection Manager).</span><span class="sxs-lookup"><span data-stu-id="0f1d5-159">Grant the WSS_Admin_WPG group read access to the DPM Registry key (HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Data Protection Manager).</span></span>

> [!NOTE]
> <span data-ttu-id="0f1d5-160">U moet ConfigureSharePoint.exe opnieuw uitgevoerd wanneer er een wijziging in de beheerdersreferenties van de SharePoint-farm.</span><span class="sxs-lookup"><span data-stu-id="0f1d5-160">You’ll need to rerun ConfigureSharePoint.exe whenever there’s a change in the SharePoint farm administrator credentials.</span></span>
>
>

## <a name="back-up-a-sharepoint-farm-by-using-mabs"></a><span data-ttu-id="0f1d5-161">Back-up van een SharePoint-farm met behulp van MABS</span><span class="sxs-lookup"><span data-stu-id="0f1d5-161">Back up a SharePoint farm by using MABS</span></span>
<span data-ttu-id="0f1d5-162">Nadat u hebt MABS en de SharePoint-farm zoals hierboven is geconfigureerd, kan SharePoint worden beveiligd door MABS.</span><span class="sxs-lookup"><span data-stu-id="0f1d5-162">After you have configured MABS and the SharePoint farm as explained previously, SharePoint can be protected by MABS.</span></span>

### <a name="to-protect-a-sharepoint-farm"></a><span data-ttu-id="0f1d5-163">Een SharePoint-farm beveiligen</span><span class="sxs-lookup"><span data-stu-id="0f1d5-163">To protect a SharePoint farm</span></span>
1. <span data-ttu-id="0f1d5-164">Van de **beveiliging** tabblad van de MABS Administrator-Console klikt u op **nieuw**.</span><span class="sxs-lookup"><span data-stu-id="0f1d5-164">From the **Protection** tab of the MABS Administrator Console, click **New**.</span></span>
    <span data-ttu-id="0f1d5-165">![Tabblad voor nieuwe beveiliging](./media/backup-azure-backup-sharepoint/dpm-new-protection-tab.png)</span><span class="sxs-lookup"><span data-stu-id="0f1d5-165">![New Protection Tab](./media/backup-azure-backup-sharepoint/dpm-new-protection-tab.png)</span></span>
2. <span data-ttu-id="0f1d5-166">Op de **Type beveiligingsgroep selecteren** pagina van de **nieuwe beveiligingsgroep maken** wizard, selecteer **Servers**, en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="0f1d5-166">On the **Select Protection Group Type** page of the **Create New Protection Group** wizard, select **Servers**, and then click **Next**.</span></span>

    ![Type beveiligingsgroep selecteren](./media/backup-azure-backup-sharepoint/select-protection-group-type.png)
3. <span data-ttu-id="0f1d5-168">Op de **groepsleden selecteren** scherm, selecteert u het selectievakje in voor de SharePoint-server die u wilt beveiligen en klikt u op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="0f1d5-168">On the **Select Group Members** screen, select the check box for the SharePoint server you want to protect and click **Next**.</span></span>

    ![Groepsleden selecteren](./media/backup-azure-backup-sharepoint/select-group-members2.png)

   > [!NOTE]
   > <span data-ttu-id="0f1d5-170">Met de beveiligingsagent is geïnstalleerd, ziet u de server in de wizard.</span><span class="sxs-lookup"><span data-stu-id="0f1d5-170">With the protection agent installed, you can see the server in the wizard.</span></span> <span data-ttu-id="0f1d5-171">MABS toont ook de structuur.</span><span class="sxs-lookup"><span data-stu-id="0f1d5-171">MABS also shows its structure.</span></span> <span data-ttu-id="0f1d5-172">Omdat u ConfigureSharePoint.exe hebt uitgevoerd, wordt MABS communiceert met de SharePoint VSS Writer-service en de bijbehorende SQL Server-databases en de structuur van SharePoint-farm, de bijbehorende inhoudsdatabases, en alle bijbehorende items herkent.</span><span class="sxs-lookup"><span data-stu-id="0f1d5-172">Because you ran ConfigureSharePoint.exe, MABS communicates with the SharePoint VSS Writer service and its corresponding SQL Server databases and recognizes the SharePoint farm structure, the associated content databases, and any corresponding items.</span></span>
   >
   >
4. <span data-ttu-id="0f1d5-173">Op de **methode voor gegevensbeveiliging selecteren** pagina, voer de naam van de **beveiligingsgroep**, en selecteer de gewenste *beveiligingsmethode*.</span><span class="sxs-lookup"><span data-stu-id="0f1d5-173">On the **Select Data Protection Method** page, enter the name of the **Protection Group**, and select your preferred *protection methods*.</span></span> <span data-ttu-id="0f1d5-174">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="0f1d5-174">Click **Next**.</span></span>

    ![Methode voor gegevensbeveiliging selecteren](./media/backup-azure-backup-sharepoint/select-data-protection-method1.png)

   > [!NOTE]
   > <span data-ttu-id="0f1d5-176">De schijf-methode voor gegevensbeveiliging helpt te voldoen aan korte doelstellingen voor hersteltijd.</span><span class="sxs-lookup"><span data-stu-id="0f1d5-176">The disk protection method helps to meet short recovery-time objectives.</span></span>
   >
   >
5. <span data-ttu-id="0f1d5-177">Op de **Kortetermijndoelen opgeven** pagina, selecteer de gewenste **bewaartermijn** en als u wilt dat back-ups te identificeren.</span><span class="sxs-lookup"><span data-stu-id="0f1d5-177">On the **Specify Short-Term Goals** page, select your preferred **Retention range** and identify when you want backups to occur.</span></span>

    ![Korte-termijndoelstellingen opgeven](./media/backup-azure-backup-sharepoint/specify-short-term-goals2.png)

   > [!NOTE]
   > <span data-ttu-id="0f1d5-179">Omdat het herstel meestal nodig is voor gegevens die minder dan vijf dagen oud, we een bewaartermijn van vijf dagen op schijf geselecteerd en ervoor gezorgd dat de back-up moet worden uitgevoerd tijdens de niet-productieve uren, in dit voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="0f1d5-179">Because recovery is most often required for data that's less than five days old, we selected a retention range of five days on disk and ensured that the backup happens during non-production hours, for this example.</span></span>
   >
   >
6. <span data-ttu-id="0f1d5-180">De opslaggroep schijfruimte die voor de beveiligingsgroep is toegewezen en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="0f1d5-180">Review the storage pool disk space allocated for the protection group, and click then **Next**.</span></span>
7. <span data-ttu-id="0f1d5-181">Voor elke beveiligingsgroep wordt MABS toegewezen schijfruimte voor het opslaan en beheren van replica's.</span><span class="sxs-lookup"><span data-stu-id="0f1d5-181">For every protection group, MABS allocates disk space to store and manage replicas.</span></span> <span data-ttu-id="0f1d5-182">MABS moet op dit punt wordt een kopie van de geselecteerde gegevens maken.</span><span class="sxs-lookup"><span data-stu-id="0f1d5-182">At this point, MABS must create a copy of the selected data.</span></span> <span data-ttu-id="0f1d5-183">Selecteer hoe en wanneer u wilt dat de replica is gemaakt en klik op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="0f1d5-183">Select how and when you want the replica created, and then click **Next**.</span></span>

    ![Methode voor het maken van replica selecteren](./media/backup-azure-backup-sharepoint/choose-replica-creation-method.png)

   > [!NOTE]
   > <span data-ttu-id="0f1d5-185">Om ervoor te zorgen dat verkeer niet wordt gedaan, selecteer een tijdstip buiten productie-uren.</span><span class="sxs-lookup"><span data-stu-id="0f1d5-185">To make sure that network traffic is not effected, select a time outside production hours.</span></span>
   >
   >
8. <span data-ttu-id="0f1d5-186">MABS wordt de gegevensintegriteit gewaarborgd door het uitvoeren van consistentiecontroles uit op de replica.</span><span class="sxs-lookup"><span data-stu-id="0f1d5-186">MABS ensures data integrity by performing consistency checks on the replica.</span></span> <span data-ttu-id="0f1d5-187">Er zijn twee opties beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="0f1d5-187">There are two available options.</span></span> <span data-ttu-id="0f1d5-188">Kunt u een planning wordt uitgevoerd, consistentiecontroles of DPM consistentiecontroles automatisch op de replica wordt uitgevoerd wanneer het inconsistent wordt.</span><span class="sxs-lookup"><span data-stu-id="0f1d5-188">You can define a schedule to run consistency checks, or DPM can run consistency checks automatically on the replica whenever it becomes inconsistent.</span></span> <span data-ttu-id="0f1d5-189">Selecteer de gewenste optie en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="0f1d5-189">Select your preferred option, and then click **Next**.</span></span>

    ![Consistentiecontrole](./media/backup-azure-backup-sharepoint/consistency-check.png)
9. <span data-ttu-id="0f1d5-191">Op de **gegevens voor Online beveiliging opgeven** pagina, selecteert u de SharePoint-farm die u wilt beveiligen en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="0f1d5-191">On the **Specify Online Protection Data** page, select the SharePoint farm that you want to protect, and then click **Next**.</span></span>

    ![DPM SharePoint Protection1](./media/backup-azure-backup-sharepoint/select-online-protection1.png)
10. <span data-ttu-id="0f1d5-193">Op de **Online back-upschema opgeven** pagina, selecteer uw voorkeursplanning en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="0f1d5-193">On the **Specify Online Backup Schedule** page, select your preferred schedule, and then click **Next**.</span></span>

    ![Online_backup_schedule](./media/backup-azure-backup-sharepoint/specify-online-backup-schedule.png)

    > [!NOTE]
    > <span data-ttu-id="0f1d5-195">MABS biedt een maximum van twee dagelijkse back-ups naar Azure vanaf het vervolgens beschikbaar nieuwste schijf back-punt.</span><span class="sxs-lookup"><span data-stu-id="0f1d5-195">MABS provides a maximum of two daily backups to Azure from the then available latest disk backup point.</span></span> <span data-ttu-id="0f1d5-196">Azure Backup kan ook bepalen welke WAN-bandbreedte die kan worden gebruikt voor back-ups in piek- en daluren met behulp van [Azure back-up netwerkbeperking](https://azure.microsoft.com/documentation/articles/backup-configure-vault/#enable-network-throttling).</span><span class="sxs-lookup"><span data-stu-id="0f1d5-196">Azure Backup can also control the amount of WAN bandwidth that can be used for backups in peak and off-peak hours by using [Azure Backup Network Throttling](https://azure.microsoft.com/documentation/articles/backup-configure-vault/#enable-network-throttling).</span></span>
    >
    >
11. <span data-ttu-id="0f1d5-197">Afhankelijk van het back-upschema die u hebt geselecteerd op de **Online bewaarbeleid opgeven** pagina, selecteert u het bewaarbeleid voor dagelijkse, wekelijkse, maandelijkse en jaarlijkse back-uppunten.</span><span class="sxs-lookup"><span data-stu-id="0f1d5-197">Depending on the backup schedule that you selected, on the **Specify Online Retention Policy** page, select the retention policy for daily, weekly, monthly, and yearly backup points.</span></span>

    ![Online_retention_policy](./media/backup-azure-backup-sharepoint/specify-online-retention.png)

    > [!NOTE]
    > <span data-ttu-id="0f1d5-199">Een opa-vader-zoon bewaarschema waarin een andere bewaarbeleid kan worden gekozen MABS gebruikt voor andere back-uppunten.</span><span class="sxs-lookup"><span data-stu-id="0f1d5-199">MABS uses a grandfather-father-son retention scheme in which a different retention policy can be chosen for different backup points.</span></span>
    >
    >
12. <span data-ttu-id="0f1d5-200">Vergelijkbaar met schijf, een eerste verwijzing punt replica moet worden gemaakt in Azure.</span><span class="sxs-lookup"><span data-stu-id="0f1d5-200">Similar to disk, an initial reference point replica needs to be created in Azure.</span></span> <span data-ttu-id="0f1d5-201">Selecteer uw voorkeursoptie een eerste back-up naar Azure maken en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="0f1d5-201">Select your preferred option to create an initial backup copy to Azure, and then click **Next**.</span></span>

    ![Online_replica](./media/backup-azure-backup-sharepoint/online-replication.png)
13. <span data-ttu-id="0f1d5-203">Controleer de geselecteerde instellingen op de **samenvatting** pagina en klik vervolgens op **groep maken**.</span><span class="sxs-lookup"><span data-stu-id="0f1d5-203">Review your selected settings on the **Summary** page, and then click **Create Group**.</span></span> <span data-ttu-id="0f1d5-204">U ziet een bericht nadat de beveiligingsgroep is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="0f1d5-204">You will see a success message after the protection group has been created.</span></span>

    ![Samenvatting](./media/backup-azure-backup-sharepoint/summary.png)

## <a name="restore-a-sharepoint-item-from-disk-by-using-mabs"></a><span data-ttu-id="0f1d5-206">Een SharePoint-item terugzetten vanaf schijf met MABS</span><span class="sxs-lookup"><span data-stu-id="0f1d5-206">Restore a SharePoint item from disk by using MABS</span></span>
<span data-ttu-id="0f1d5-207">In het volgende voorbeeld wordt de *herstellen van SharePoint-item* per ongeluk is verwijderd en moet worden hersteld.</span><span class="sxs-lookup"><span data-stu-id="0f1d5-207">In the following example, the *Recovering SharePoint item* has been accidentally deleted and needs to be recovered.</span></span>
<span data-ttu-id="0f1d5-208">![MABS SharePoint Protection4](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection5.png)</span><span class="sxs-lookup"><span data-stu-id="0f1d5-208">![MABS SharePoint Protection4](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection5.png)</span></span>

1. <span data-ttu-id="0f1d5-209">Open de **DPM Administrator-Console**.</span><span class="sxs-lookup"><span data-stu-id="0f1d5-209">Open the **DPM Administrator Console**.</span></span> <span data-ttu-id="0f1d5-210">Alle SharePoint-farms die zijn beveiligd door DPM worden weergegeven in de **beveiliging** tabblad.</span><span class="sxs-lookup"><span data-stu-id="0f1d5-210">All SharePoint farms that are protected by DPM are shown in the **Protection** tab.</span></span>

    ![MABS SharePoint Protection3](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection4.png)
2. <span data-ttu-id="0f1d5-212">Om te beginnen met het item herstellen, selecteert u de **herstel** tabblad.</span><span class="sxs-lookup"><span data-stu-id="0f1d5-212">To begin to recover the item, select the **Recovery** tab.</span></span>

    ![MABS SharePoint Protection5](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection6.png)
3. <span data-ttu-id="0f1d5-214">U kunt zoeken in SharePoint voor *herstellen van SharePoint-item* verwijzen met behulp van een zoekopdracht op basis van een jokerteken binnen een herstelbewerking bereik.</span><span class="sxs-lookup"><span data-stu-id="0f1d5-214">You can search SharePoint for *Recovering SharePoint item* by using a wildcard-based search within a recovery point range.</span></span>

    ![MABS SharePoint Protection6](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection7.png)
4. <span data-ttu-id="0f1d5-216">Selecteer het juiste herstelpunt in de zoekresultaten, met de rechtermuisknop op het item en selecteer vervolgens **herstellen**.</span><span class="sxs-lookup"><span data-stu-id="0f1d5-216">Select the appropriate recovery point from the search results, right-click the item, and then select **Recover**.</span></span>
5. <span data-ttu-id="0f1d5-217">U kunt ook bladeren door verschillende herstelpunten en selecteer een database of het item dat u wilt herstellen.</span><span class="sxs-lookup"><span data-stu-id="0f1d5-217">You can also browse through various recovery points and select a database or item to recover.</span></span> <span data-ttu-id="0f1d5-218">Selecteer **datum > hersteltijd**, en selecteer vervolgens de juiste **Database > SharePoint-farm > herstelpunt > Item**.</span><span class="sxs-lookup"><span data-stu-id="0f1d5-218">Select **Date > Recovery time**, and then select the correct **Database > SharePoint farm > Recovery point > Item**.</span></span>

    ![MABS SharePoint Protection7](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection8.png)
6. <span data-ttu-id="0f1d5-220">Met de rechtermuisknop op het item en selecteer vervolgens **herstellen** openen de **Herstelwizard**.</span><span class="sxs-lookup"><span data-stu-id="0f1d5-220">Right-click the item, and then select **Recover** to open the **Recovery Wizard**.</span></span> <span data-ttu-id="0f1d5-221">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="0f1d5-221">Click **Next**.</span></span>

    ![Selectie voor herstel controleren](./media/backup-azure-backup-sharepoint/review-recovery-selection.png)
7. <span data-ttu-id="0f1d5-223">Selecteer het type herstel dat u wilt uitvoeren en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="0f1d5-223">Select the type of recovery that you want to perform, and then click **Next**.</span></span>

    ![Hersteltype](./media/backup-azure-backup-sharepoint/select-recovery-type.png)

   > [!NOTE]
   > <span data-ttu-id="0f1d5-225">De selectie van **herstellen naar oorspronkelijke** Hiermee herstelt u het item naar de oorspronkelijke SharePoint-site in het voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="0f1d5-225">The selection of **Recover to original** in the example recovers the item to the original SharePoint site.</span></span>
   >
   >
8. <span data-ttu-id="0f1d5-226">Selecteer de **herstelproces** die u wilt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="0f1d5-226">Select the **Recovery Process** that you want to use.</span></span>

   * <span data-ttu-id="0f1d5-227">Selecteer **herstellen zonder herstelfarm** als de SharePoint-farm is niet gewijzigd en is hetzelfde als het herstelpunt dat wordt hersteld.</span><span class="sxs-lookup"><span data-stu-id="0f1d5-227">Select **Recover without using a recovery farm** if the SharePoint farm has not changed and is the same as the recovery point that is being restored.</span></span>
   * <span data-ttu-id="0f1d5-228">Selecteer **herstellen met behulp van een herstelfarm** als de SharePoint-farm is gewijzigd sinds het herstelpunt is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="0f1d5-228">Select **Recover using a recovery farm** if the SharePoint farm has changed since the recovery point was created.</span></span>

     ![Herstelproces](./media/backup-azure-backup-sharepoint/recovery-process.png)
9. <span data-ttu-id="0f1d5-230">Een gefaseerde installatie locatie voor het exemplaar van SQL Server tijdelijk voor de database, en bieden een gefaseerde installatie bestandsshare op MABS en de server waarop SharePoint voor het herstellen van het item wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="0f1d5-230">Provide a staging SQL Server instance location to recover the database temporarily, and provide a staging file share on MABS and the server that's running SharePoint to recover the item.</span></span>

    ![Fasering Location1](./media/backup-azure-backup-sharepoint/staging-location1.png)

    <span data-ttu-id="0f1d5-232">MABS koppelt de inhoudsdatabase die als host voor de SharePoint-item naar de tijdelijke SQL Server-exemplaar fungeert.</span><span class="sxs-lookup"><span data-stu-id="0f1d5-232">MABS attaches the content database that is hosting the SharePoint item to the temporary SQL Server instance.</span></span> <span data-ttu-id="0f1d5-233">Van de inhoud van de database, het Hiermee herstelt u het item en plaatst deze op de tijdelijke bestandslocatie op MABS.</span><span class="sxs-lookup"><span data-stu-id="0f1d5-233">From the content database, it recovers the item and puts it on the staging file location on MABS.</span></span> <span data-ttu-id="0f1d5-234">Het herstelde item dat is nu op de faseringslocatie moet worden geëxporteerd naar de faseringslocatie op de SharePoint-farm.</span><span class="sxs-lookup"><span data-stu-id="0f1d5-234">The recovered item that's on the staging location now needs to be exported to the staging location on the SharePoint farm.</span></span>

    ![Fasering Location2](./media/backup-azure-backup-sharepoint/staging-location2.png)
10. <span data-ttu-id="0f1d5-236">Selecteer **herstelopties opgeven**, en beveiligingsinstellingen toepassen op de SharePoint-farm of toepassen van de beveiligingsinstellingen van het herstelpunt.</span><span class="sxs-lookup"><span data-stu-id="0f1d5-236">Select **Specify recovery options**, and apply security settings to the SharePoint farm or apply the security settings of the recovery point.</span></span> <span data-ttu-id="0f1d5-237">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="0f1d5-237">Click **Next**.</span></span>

    ![Opties voor herstel](./media/backup-azure-backup-sharepoint/recovery-options.png)

    > [!NOTE]
    > <span data-ttu-id="0f1d5-239">U kunt het gebruik van netwerkbandbreedte te beperken.</span><span class="sxs-lookup"><span data-stu-id="0f1d5-239">You can choose to throttle the network bandwidth usage.</span></span> <span data-ttu-id="0f1d5-240">Dit minimaliseert van invloed op de productieserver tijdens de productie-uren.</span><span class="sxs-lookup"><span data-stu-id="0f1d5-240">This minimizes impact to the production server during production hours.</span></span>
    >
    >
11. <span data-ttu-id="0f1d5-241">Controleer de overzichtsgegevens en klik vervolgens op **herstellen** om te beginnen met herstel van het bestand.</span><span class="sxs-lookup"><span data-stu-id="0f1d5-241">Review the summary information, and then click **Recover** to begin recovery of the file.</span></span>

    ![Samenvatting van herstel](./media/backup-azure-backup-sharepoint/recovery-summary.png)
12. <span data-ttu-id="0f1d5-243">Nu selecteren de **bewaking** tabblad de **MABS Administrator-Console** om weer te geven de **Status** van het herstel.</span><span class="sxs-lookup"><span data-stu-id="0f1d5-243">Now select the **Monitoring** tab in the **MABS Administrator Console** to view the **Status** of the recovery.</span></span>

    ![Herstelstatus](./media/backup-azure-backup-sharepoint/recovery-monitoring.png)

    > [!NOTE]
    > <span data-ttu-id="0f1d5-245">Het bestand is nu hersteld.</span><span class="sxs-lookup"><span data-stu-id="0f1d5-245">The file is now restored.</span></span> <span data-ttu-id="0f1d5-246">U kunt de SharePoint-site om te controleren van het bestand moet worden teruggezet vernieuwen.</span><span class="sxs-lookup"><span data-stu-id="0f1d5-246">You can refresh the SharePoint site to check the restored file.</span></span>
    >
    >

## <a name="restore-a-sharepoint-database-from-azure-by-using-dpm"></a><span data-ttu-id="0f1d5-247">Een SharePoint-database herstellen van Azure met DPM</span><span class="sxs-lookup"><span data-stu-id="0f1d5-247">Restore a SharePoint database from Azure by using DPM</span></span>
1. <span data-ttu-id="0f1d5-248">Als u wilt herstellen op een SharePoint-inhoudsdatabase, bladeren door verschillende herstelpunten (zoals eerder is weergegeven) en selecteer het herstelpunt dat u wilt herstellen.</span><span class="sxs-lookup"><span data-stu-id="0f1d5-248">To recover a SharePoint content database, browse through various recovery points (as shown previously), and select the recovery point that you want to restore.</span></span>

    ![MABS SharePoint Protection8](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection9.png)
2. <span data-ttu-id="0f1d5-250">Dubbelklik op de SharePoint-herstelpunt om weer te geven van de beschikbare informatie van de SharePoint-catalogus.</span><span class="sxs-lookup"><span data-stu-id="0f1d5-250">Double-click the SharePoint recovery point to show the available SharePoint catalog information.</span></span>

   > [!NOTE]
   > <span data-ttu-id="0f1d5-251">Omdat de SharePoint-farm is beveiligd voor lange bewaartermijn in Azure, is er is geen catalogusinformatie (metagegevens) beschikbaar op MABS.</span><span class="sxs-lookup"><span data-stu-id="0f1d5-251">Because the SharePoint farm is protected for long-term retention in Azure, no catalog information (metadata) is available on MABS.</span></span> <span data-ttu-id="0f1d5-252">Als een SharePoint-inhoudsdatabase punt in tijd worden hersteld moet, moet u als gevolg hiervan de SharePoint-farm opnieuw catalogiseren.</span><span class="sxs-lookup"><span data-stu-id="0f1d5-252">As a result, whenever a point-in-time SharePoint content database needs to be recovered, you need to catalog the SharePoint farm again.</span></span>
   >
   >
3. <span data-ttu-id="0f1d5-253">Klik op **opnieuw catalogiseren**.</span><span class="sxs-lookup"><span data-stu-id="0f1d5-253">Click **Re-catalog**.</span></span>

    ![MABS SharePoint Protection10](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection12.png)

    <span data-ttu-id="0f1d5-255">De **Cloud opnieuw catalogiseren** statusvenster wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="0f1d5-255">The **Cloud Recatalog** status window opens.</span></span>

    ![MABS SharePoint Protection11](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection13.png)

    <span data-ttu-id="0f1d5-257">Nadat catalogiseren is voltooid, wordt de status gewijzigd in *geslaagd*.</span><span class="sxs-lookup"><span data-stu-id="0f1d5-257">After cataloging is finished, the status changes to *Success*.</span></span> <span data-ttu-id="0f1d5-258">Klik op **Sluiten**.</span><span class="sxs-lookup"><span data-stu-id="0f1d5-258">Click **Close**.</span></span>

    ![MABS SharePoint Protection12](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection14.png)
4. <span data-ttu-id="0f1d5-260">Klik op de SharePoint-object dat wordt weergegeven in de MABS **herstel** tabblad om op te halen van de inhoud van de database-structuur.</span><span class="sxs-lookup"><span data-stu-id="0f1d5-260">Click the SharePoint object shown in the MABS **Recovery** tab to get the content database structure.</span></span> <span data-ttu-id="0f1d5-261">Met de rechtermuisknop op het item en klik vervolgens op **herstellen**.</span><span class="sxs-lookup"><span data-stu-id="0f1d5-261">Right-click the item, and then click **Recover**.</span></span>

    ![MABS SharePoint Protection13](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection15.png)
5. <span data-ttu-id="0f1d5-263">Op dit moment, volgt u de [herstel stappen eerder in dit artikel](#restore-a-sharepoint-item-from-disk-using-dpm) voor het herstellen van een SharePoint-inhoudsdatabase van de schijf.</span><span class="sxs-lookup"><span data-stu-id="0f1d5-263">At this point, follow the [recovery steps earlier in this article](#restore-a-sharepoint-item-from-disk-using-dpm) to recover a SharePoint content database from disk.</span></span>

## <a name="faqs"></a><span data-ttu-id="0f1d5-264">Veelgestelde vragen</span><span class="sxs-lookup"><span data-stu-id="0f1d5-264">FAQs</span></span>
<span data-ttu-id="0f1d5-265">V: kan ik een SharePoint-item naar de oorspronkelijke locatie herstellen als SharePoint is geconfigureerd met behulp van SQL AlwaysOn (met beveiliging op schijf)?</span><span class="sxs-lookup"><span data-stu-id="0f1d5-265">Q: Can I recover a SharePoint item to the original location if SharePoint is configured by using SQL AlwaysOn (with protection on disk)?</span></span><br>
<span data-ttu-id="0f1d5-266">A: Ja, de items kan worden hersteld naar de oorspronkelijke SharePoint-site.</span><span class="sxs-lookup"><span data-stu-id="0f1d5-266">A: Yes, the item can be recovered to the original SharePoint site.</span></span>

<span data-ttu-id="0f1d5-267">V: kan ik een SharePoint-database naar de oorspronkelijke locatie herstellen als SharePoint met behulp van SQL AlwaysOn is geconfigureerd?</span><span class="sxs-lookup"><span data-stu-id="0f1d5-267">Q: Can I recover a SharePoint database to the original location if SharePoint is configured by using SQL AlwaysOn?</span></span><br>
<span data-ttu-id="0f1d5-268">A: omdat SharePoint-databases zijn geconfigureerd in de SQL AlwaysOn, kan deze niet worden gewijzigd als de beschikbaarheidsgroep wordt verwijderd.</span><span class="sxs-lookup"><span data-stu-id="0f1d5-268">A: Because SharePoint databases are configured in SQL AlwaysOn, they cannot be modified unless the availability group is removed.</span></span> <span data-ttu-id="0f1d5-269">Als gevolg hiervan terugzetten MABS een database niet naar de oorspronkelijke locatie.</span><span class="sxs-lookup"><span data-stu-id="0f1d5-269">As a result, MABS cannot restore a database to the original location.</span></span> <span data-ttu-id="0f1d5-270">U kunt een SQL Server-database naar een ander exemplaar van SQL Server herstellen.</span><span class="sxs-lookup"><span data-stu-id="0f1d5-270">You can recover a SQL Server database to another SQL Server instance.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0f1d5-271">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="0f1d5-271">Next steps</span></span>
* <span data-ttu-id="0f1d5-272">Meer informatie over MABS beveiliging van SharePoint - Zie [Video Series - DPM-beveiliging van SharePoint](http://channel9.msdn.com/Series/Azure-Backup/Microsoft-SCDPM-Protection-of-SharePoint-1-of-2-How-to-create-a-SharePoint-Protection-Group)</span><span class="sxs-lookup"><span data-stu-id="0f1d5-272">Learn more about MABS Protection of SharePoint - see [Video Series - DPM Protection of SharePoint](http://channel9.msdn.com/Series/Azure-Backup/Microsoft-SCDPM-Protection-of-SharePoint-1-of-2-How-to-create-a-SharePoint-Protection-Group)</span></span>

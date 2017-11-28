---
title: aaaManage databases in Azure SQL Data Warehouse | Microsoft Docs
description: Overzicht van het beheren van databases in SQL Data Warehouse. Beheerhulpprogramma's voor dwu's en scale-out-prestaties queryprestaties tot stand brengen van goede beveiligingsbeleid en het herstellen van een database van beschadigde gegevens of van een regionale uitval probleemoplossing bevat.
services: sql-data-warehouse
documentationcenter: NA
author: kevinvngo
manager: jhubbard
editor: 
ms.assetid: 8576fdb3-71fe-4b3b-a4e0-5e8a7f148acf
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: manage
ms.date: 10/31/2016
ms.author: kevin;barbkess
ms.openlocfilehash: caec6572c4ab395107c3b095adc69a53eae8bd88
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-databases-in-azure-sql-data-warehouse"></a><span data-ttu-id="304b9-104">Databases in Azure SQL Data Warehouse beheren</span><span class="sxs-lookup"><span data-stu-id="304b9-104">Manage databases in Azure SQL Data Warehouse</span></span>
<span data-ttu-id="304b9-105">SQL Data Warehouse automatiseert veel aspecten van het beheer van uw databases.</span><span class="sxs-lookup"><span data-stu-id="304b9-105">SQL Data Warehouse automates many aspects of managing your databases.</span></span> <span data-ttu-id="304b9-106">Bijvoorbeeld tooscale prestaties hoeft alleen tooadjust en betaalt voor Hallo rechts niveau van rekenresources en laat SQL Data Warehouse werk alle Hallo van uitbreiden en schalen weer.</span><span class="sxs-lookup"><span data-stu-id="304b9-106">For example, tooscale performance you only need tooadjust and pay for hello right level of compute resources, and then let SQL Data Warehouse do all hello work of scaling out and scaling back.</span></span>

<span data-ttu-id="304b9-107">U wilt toomonitor ongetwijfeld van uw werkbelasting tooidentify prestaties van uw behoeften, evenals oplossen langlopende query's.</span><span class="sxs-lookup"><span data-stu-id="304b9-107">You will undoubtedly want toomonitor your workload tooidentify your performance needs as well as troubleshoot long-running queries.</span></span> <span data-ttu-id="304b9-108">U moet ook tooperform enkele taken toomanage beveiligingsmachtigingen voor gebruikers en aanmeldingen.</span><span class="sxs-lookup"><span data-stu-id="304b9-108">You will also need tooperform a few security tasks toomanage permissions for users and logins.</span></span>

<span data-ttu-id="304b9-109">Dit overzicht bevat informatie over deze aspecten van het beheer van SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="304b9-109">This overview covers these aspects of managing SQL Data Warehouse.</span></span>

* <span data-ttu-id="304b9-110">Beheerhulpprogramma's</span><span class="sxs-lookup"><span data-stu-id="304b9-110">Management tools</span></span>
* <span data-ttu-id="304b9-111">Scale Compute</span><span class="sxs-lookup"><span data-stu-id="304b9-111">Scale Compute</span></span>
* <span data-ttu-id="304b9-112">Onderbreken en hervatten</span><span class="sxs-lookup"><span data-stu-id="304b9-112">Pause and Resume</span></span>
* <span data-ttu-id="304b9-113">Aanbevolen procedures voor prestaties</span><span class="sxs-lookup"><span data-stu-id="304b9-113">Performance Best Practices</span></span>
* <span data-ttu-id="304b9-114">Bewaking van de query</span><span class="sxs-lookup"><span data-stu-id="304b9-114">Query Monitoring</span></span>
* <span data-ttu-id="304b9-115">Beveiliging</span><span class="sxs-lookup"><span data-stu-id="304b9-115">Security</span></span>
* <span data-ttu-id="304b9-116">Back-ups en herstellen</span><span class="sxs-lookup"><span data-stu-id="304b9-116">Backup and restore</span></span>

## <a name="management-tools"></a><span data-ttu-id="304b9-117">Beheerhulpprogramma's</span><span class="sxs-lookup"><span data-stu-id="304b9-117">Management tools</span></span>
<span data-ttu-id="304b9-118">U kunt een aantal extra toomanage databases in SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="304b9-118">You can use a variety of tools toomanage databases in SQL Data Warehouse.</span></span> <span data-ttu-id="304b9-119">Als u databases beheren, kunt u hulpprogramma voorkeuren ontwikkelen voor elke taak moet u tooperform.</span><span class="sxs-lookup"><span data-stu-id="304b9-119">As you manage databases, you will develop tool preferences for each type of task you need tooperform.</span></span>

### <a name="azure-portal"></a><span data-ttu-id="304b9-120">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="304b9-120">Azure portal</span></span>
<span data-ttu-id="304b9-121">Hallo [Azure-portal] [ Azure portal] is een web-portal kunt u maken, bijwerken, en verwijdert u de databases en databaseresources bewaken.</span><span class="sxs-lookup"><span data-stu-id="304b9-121">hello [Azure portal][Azure portal] is a web-based portal where you can create, update, and delete databases and monitor database resources.</span></span> <span data-ttu-id="304b9-122">Dit hulpprogramma is een goede is als u alleen aan de slag met Azure, het beheren van een klein aantal datawarehouse-databases, of moet tooquickly iets doen.</span><span class="sxs-lookup"><span data-stu-id="304b9-122">This tool is great is if you're just getting started with Azure, managing a small number of data warehouse databases, or need tooquickly do something.</span></span>

<span data-ttu-id="304b9-123">de slag met Azure-portal Hallo tooget Zie [maken van een SQL Data Warehouse (Azure-portal)][Create a SQL Data Warehouse (Azure portal)].</span><span class="sxs-lookup"><span data-stu-id="304b9-123">tooget started with hello Azure portal, see [Create a SQL Data Warehouse (Azure portal)][Create a SQL Data Warehouse (Azure portal)].</span></span>

### <a name="sql-server-data-tools-in-visual-studio"></a><span data-ttu-id="304b9-124">SQL Server Data Tools in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="304b9-124">SQL Server Data Tools in Visual Studio</span></span>
<span data-ttu-id="304b9-125">[SQL Server Data Tools] [ SQL Server Data Tools] (SSDT) in Visual Studio kunt u tooconnect te beheren en ontwikkelen van uw databases.</span><span class="sxs-lookup"><span data-stu-id="304b9-125">[SQL Server Data Tools][SQL Server Data Tools] (SSDT) in Visual Studio allows you tooconnect to, manage, and develop your databases.</span></span> <span data-ttu-id="304b9-126">Als u bent een toepassingsontwikkelaar bekend bent met Visual Studio of andere geïntegreerde ontwikkelomgevingen (IDE), probeert u SSDT in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="304b9-126">If you're an application developer familiar with Visual Studio or other integrated development environments (IDEs), try using SSDT in Visual Studio.</span></span>

<span data-ttu-id="304b9-127">SSDT Hallo SQL Server Object Explorer waarmee u toovisualize bevat, verbinding maken en uitvoeren van scripts in SQL Data Warehouse-databases.</span><span class="sxs-lookup"><span data-stu-id="304b9-127">SSDT includes hello SQL Server Object Explorer which enables you toovisualize, connect, and execute scripts against SQL Data Warehouse databases.</span></span> <span data-ttu-id="304b9-128">tooquickly verbinding tooSQL Data Warehouse, kunt u eenvoudig hello op **openen in Visual Studio** knop in de opdrachtbalk Hallo wanneer u bekijkt hello databasedetails in Hallo klassieke Azure-Portal.</span><span class="sxs-lookup"><span data-stu-id="304b9-128">tooquickly connect tooSQL Data Warehouse, you can simply click hello **Open in Visual Studio** button in hello command bar when viewing hello database details in hello Azure Classic Portal.</span></span>  

<span data-ttu-id="304b9-129">tooget gestart met SSDT in Visual Studio, Zie [Query Azure SQL Data Warehouse met Visual Studio][Query Azure SQL Data Warehouse with Visual Studio].</span><span class="sxs-lookup"><span data-stu-id="304b9-129">tooget started with SSDT in Visual Studio, see [Query Azure SQL Data Warehouse with Visual Studio][Query Azure SQL Data Warehouse with Visual Studio].</span></span>

### <a name="command-line-tools"></a><span data-ttu-id="304b9-130">Opdrachtregelprogramma's</span><span class="sxs-lookup"><span data-stu-id="304b9-130">Command-line tools</span></span>
<span data-ttu-id="304b9-131">Opdrachtregelprogramma's zijn ideaal voor het automatiseren van uw werkbelastingen.</span><span class="sxs-lookup"><span data-stu-id="304b9-131">Command line tools are ideal for automating your workloads.</span></span>  <span data-ttu-id="304b9-132">PowerShell en sqlcmd zijn twee manieren geweldige tooautomate uw processen.</span><span class="sxs-lookup"><span data-stu-id="304b9-132">PowerShell and sqlcmd are two great ways tooautomate your processes.</span></span>  <span data-ttu-id="304b9-133">U wordt aangeraden deze hulpprogramma's voor het beheren van een groot aantal logische servers en de wijzigingen van de resources in een productieomgeving implementeert, zoals Hallo taken kunnen worden vastgelegd in een script en vervolgens automatisch.</span><span class="sxs-lookup"><span data-stu-id="304b9-133">We recommend these tools for managing a large number of logical servers and deploying resource changes in a production environment as hello tasks necessary can be scripted and then automated.</span></span>

### <a name="dynamic-management-views"></a><span data-ttu-id="304b9-134">Dynamische beheerweergaven</span><span class="sxs-lookup"><span data-stu-id="304b9-134">Dynamic management views</span></span>
<span data-ttu-id="304b9-135">DMV's zijn Hallo brood en boter van het beheer van SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="304b9-135">DMVs are hello bread and butter of managing SQL Data Warehouse.</span></span> <span data-ttu-id="304b9-136">Bijna alle informatie waarmee Hallo portal afhankelijk van de DMV's.</span><span class="sxs-lookup"><span data-stu-id="304b9-136">Almost all information that surfaces in hello portal relies on DMVs.</span></span> <span data-ttu-id="304b9-137">Zie voor een lijst met SQL Data Warehouse DMV's, toosee [SQL Data Warehouse systeemweergaven][SQL Data Warehouse system views].</span><span class="sxs-lookup"><span data-stu-id="304b9-137">toosee a list of SQL Data Warehouse DMVs, see [SQL Data Warehouse system views][SQL Data Warehouse system views].</span></span>

<span data-ttu-id="304b9-138">tooget gestart, Zie [Connect en query met sqlcmd][Connect and query with sqlcmd], en [maken van een database (PowerShell)][Create a database (PowerShell)].</span><span class="sxs-lookup"><span data-stu-id="304b9-138">tooget started, see [Connect and query with sqlcmd][Connect and query with sqlcmd], and [Create a database (PowerShell)][Create a database (PowerShell)].</span></span>

## <a name="scale-compute"></a><span data-ttu-id="304b9-139">Scale compute</span><span class="sxs-lookup"><span data-stu-id="304b9-139">Scale compute</span></span>
<span data-ttu-id="304b9-140">In SQL Data Warehouse, kunt u snel de prestaties af of terug te vergroten of verkleinen van rekenresources van CPU, geheugen en i/o-bandbreedte te schalen.</span><span class="sxs-lookup"><span data-stu-id="304b9-140">In SQL Data Warehouse, you can quickly scale performance out or back by increasing or decreasing compute resources of CPU, memory, and I/O bandwidth.</span></span> <span data-ttu-id="304b9-141">tooscale prestaties toodo hoeft u pas Hallo aantal datawarehouse Units (dwu's) dat de SQL Data Warehouse-database tooyour toewijst.</span><span class="sxs-lookup"><span data-stu-id="304b9-141">tooscale performance, all you need toodo is adjust hello number of data warehouse units (DWUs) that SQL Data Warehouse allocates tooyour database.</span></span> <span data-ttu-id="304b9-142">SQL Data Warehouse Hallo wijzigen kunt u snel en verwerkt alle Hallo onderliggende wijzigingen toohardware of software.</span><span class="sxs-lookup"><span data-stu-id="304b9-142">SQL Data Warehouse quickly makes hello change and handles all hello underlying changes toohardware or software.</span></span>

<span data-ttu-id="304b9-143">toolearn meer informatie over het schalen van dwu's, Zie [prestaties schalen].</span><span class="sxs-lookup"><span data-stu-id="304b9-143">toolearn more about scaling DWUs, see [Scale performance].</span></span>

## <a name="pause-and-resume"></a><span data-ttu-id="304b9-144">Onderbreken en hervatten</span><span class="sxs-lookup"><span data-stu-id="304b9-144">Pause and resume</span></span>
<span data-ttu-id="304b9-145">toosave kosten, u kunt onderbreken en hervatten compute-bronnen op aanvraag.</span><span class="sxs-lookup"><span data-stu-id="304b9-145">toosave costs, you can pause and resume compute resources on-demand.</span></span> <span data-ttu-id="304b9-146">Bijvoorbeeld als u niet Hallo database tijdens nacht hello en in het weekend gebruikt, kunt u tijdens de tijdstippen onderbreken en hervatten tijdens Hallo dag.</span><span class="sxs-lookup"><span data-stu-id="304b9-146">For example, if you won't be using hello database during hello night and on weekends, you can pause it during those times, and resume it during hello day.</span></span> <span data-ttu-id="304b9-147">U geen afgeschreven voor dwu's tijdens het Hallo-database is onderbroken.</span><span class="sxs-lookup"><span data-stu-id="304b9-147">You won't be charged for DWUs while hello database is paused.</span></span>

<span data-ttu-id="304b9-148">Zie voor meer informatie [rekencapaciteit onderbreken][Pause compute], en [compute hervatten][Resume compute].</span><span class="sxs-lookup"><span data-stu-id="304b9-148">For more information, see [Pause compute][Pause compute], and [Resume compute][Resume compute].</span></span>

## <a name="performance-best-practices"></a><span data-ttu-id="304b9-149">Aanbevolen procedures voor prestaties</span><span class="sxs-lookup"><span data-stu-id="304b9-149">Performance Best Practices</span></span>
<span data-ttu-id="304b9-150">Wanneer aan de slag met een nieuwe technologie, bespaart detecteren Hallo tips en trucs die best rechts vanaf het begin van de Hallo werken u veel tijd.</span><span class="sxs-lookup"><span data-stu-id="304b9-150">When getting started with a new technology, discovering hello tips and tricks that work best right from hello start can save you lots of time.</span></span>  <span data-ttu-id="304b9-151">Vindt u aanbevolen procedures in de gehele veel van de onderwerpen over onze.</span><span class="sxs-lookup"><span data-stu-id="304b9-151">You will find best practices throughout many of our topics.</span></span>

<span data-ttu-id="304b9-152">Zie toosee veel een samenvatting van Hallo meest belangrijke overwegingen bij het ontwikkelen van uw werkbelasting [aanbevolen procedures van SQL Data Warehouse][SQL Data Warehouse Best Practices].</span><span class="sxs-lookup"><span data-stu-id="304b9-152">toosee many a summary of hello most important considerations when developing your workload, see [SQL Data Warehouse Best Practices][SQL Data Warehouse Best Practices].</span></span>

## <a name="query-monitoring"></a><span data-ttu-id="304b9-153">Bewaking van de query</span><span class="sxs-lookup"><span data-stu-id="304b9-153">Query Monitoring</span></span>
<span data-ttu-id="304b9-154">Soms een query te lang wordt uitgevoerd, maar u niet weet welke Hallo stackpad is.</span><span class="sxs-lookup"><span data-stu-id="304b9-154">Sometimes a query is running too long, but you aren't sure of which one is hello culprit.</span></span> <span data-ttu-id="304b9-155">SQL Data Warehouse heeft dynamische beheerweergaven (DMV's) waarmee u toofigure kunt uit welke query is te lang duurt.</span><span class="sxs-lookup"><span data-stu-id="304b9-155">SQL Data Warehouse has dynamic management views (DMVs) that you can use toofigure out which query is taking too long.</span></span>

<span data-ttu-id="304b9-156">toofind langlopende query's, Zie [bewaken van uw werkbelasting via DMV's][Monitor your workload using DMVs].</span><span class="sxs-lookup"><span data-stu-id="304b9-156">toofind long-running queries, see [Monitor your workload using DMVs][Monitor your workload using DMVs].</span></span>

## <a name="security"></a><span data-ttu-id="304b9-157">Beveiliging</span><span class="sxs-lookup"><span data-stu-id="304b9-157">Security</span></span>
<span data-ttu-id="304b9-158">een beveiligd systeem toomaintain, moet u zich op Hallo waarschuwing en bescherming tegen onbevoegde toegang tot elk type.</span><span class="sxs-lookup"><span data-stu-id="304b9-158">toomaintain a secure system, you must be on hello alert and guard against any type of unauthorized access.</span></span> <span data-ttu-id="304b9-159">Een beveiligingssysteem moet toomake ervoor firewallregels wordt beveiligd zodat alleen-geautoriseerd IP-adressen verbinding kunnen maken.</span><span class="sxs-lookup"><span data-stu-id="304b9-159">A security system needs toomake sure firewall rules are in place so only authorized IP addresses can connect.</span></span> <span data-ttu-id="304b9-160">Het moet de juiste verificatiegegevens van de gebruikersreferenties.</span><span class="sxs-lookup"><span data-stu-id="304b9-160">It needs proper authentication of user credentials.</span></span> <span data-ttu-id="304b9-161">Nadat een gebruiker toohello database verbonden heeft, mag Hallo gebruiker alleen hebben machtigingen tooperform een minimum aantal acties.</span><span class="sxs-lookup"><span data-stu-id="304b9-161">After a user has connected toohello database, hello user should only have permissions tooperform a minimal number of actions.</span></span> <span data-ttu-id="304b9-162">toosecure gegevens, u kunt versleuteling gebruiken.</span><span class="sxs-lookup"><span data-stu-id="304b9-162">toosecure data, you can use encryption.</span></span> <span data-ttu-id="304b9-163">Het is ook belangrijk toohave controleren en bij te houden, zodat u gebeurtenissen keren kunt als er verdachte activiteiten.</span><span class="sxs-lookup"><span data-stu-id="304b9-163">It's also important toohave auditing and tracking so you can retrace events if there is any suspicious activity.</span></span>

<span data-ttu-id="304b9-164">toolearn over het beheren van beveiliging, head via toohello [beveiligingsoverzicht][Security overview].</span><span class="sxs-lookup"><span data-stu-id="304b9-164">toolearn about managing security, head over toohello [Security overview][Security overview].</span></span>

## <a name="backup-and-restore"></a><span data-ttu-id="304b9-165">Back-ups en herstellen</span><span class="sxs-lookup"><span data-stu-id="304b9-165">Backup and restore</span></span>
<span data-ttu-id="304b9-166">Met betrouwbare backps van uw gegevens is een essentieel onderdeel van een productiedatabase.</span><span class="sxs-lookup"><span data-stu-id="304b9-166">Having reliable backps of your data is an essential part of any production database.</span></span> <span data-ttu-id="304b9-167">SQL Data Warehouse houdt uw gegevens veilig door automatisch back-ups van uw actieve databases met regelmatige tussenpozen.</span><span class="sxs-lookup"><span data-stu-id="304b9-167">SQL Data Warehouse keeps your data safe by automatically backing up your active databases at regular intervals.</span></span> <span data-ttu-id="304b9-168">Deze back-ups kunnen u toorecover van scenario's waar hebt u uw gegevens beschadigd of per ongeluk verwijderd van uw gegevens of de database.</span><span class="sxs-lookup"><span data-stu-id="304b9-168">These backups allow you toorecover from scenarios where you've corrupted your data or accidentally dropped your data or database.</span></span>  <span data-ttu-id="304b9-169">Voor Hallo gegevens back-upschema bewaarbeleid en hoe toorestore een database, Zie [herstellen vanuit een momentopname][Restore from snapshot].</span><span class="sxs-lookup"><span data-stu-id="304b9-169">For hello data backup schedule, retention policy and how toorestore a database, see [Restore from snapshot][Restore from snapshot].</span></span>

## <a name="next-steps"></a><span data-ttu-id="304b9-170">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="304b9-170">Next steps</span></span>
<span data-ttu-id="304b9-171">Met behulp van de principes van de database goed ontwerp maakt het eenvoudiger toomanage uw databases in SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="304b9-171">Using good database design principles will make it easier toomanage your databases in SQL Data Warehouse.</span></span> <span data-ttu-id="304b9-172">toolearn meer, head via toohello [overzicht voor ontwikkelaars][Development overview].</span><span class="sxs-lookup"><span data-stu-id="304b9-172">toolearn more, head over toohello [Development overview][Development overview].</span></span>

<!--Image references-->

<!--Article references-->
[Create a SQL Data Warehouse (Azure Portal)]: sql-data-warehouse-get-started-provision.md
[Create a database (PowerShell)]: sql-data-warehouse-get-started-provision-powershell.md
[connection]: sql-data-warehouse-develop-connections.md
[Query Azure SQL Data Warehouse with Visual Studio]: sql-data-warehouse-query-visual-studio.md
[Connect and query with sqlcmd]: sql-data-warehouse-get-started-connect-sqlcmd.md
[Development overview]: sql-data-warehouse-overview-develop.md
[Monitor your workload using DMVs]: sql-data-warehouse-manage-monitor.md
[Pause compute]: sql-data-warehouse-manage-compute-overview.md#pause-compute-bk
[Restore from snapshot]: sql-data-warehouse-restore-database-overview.md
[Resume compute]: sql-data-warehouse-manage-compute-overview.md#resume-compute-bk
[prestaties schalen]: sql-data-warehouse-manage-compute-overview.md#scale-compute
[Security overview]: sql-data-warehouse-overview-manage-security.md
[SQL Data Warehouse Best Practices]: sql-data-warehouse-best-practices.md
[SQL Data Warehouse system views]: sql-data-warehouse-reference-tsql-system-views.md

<!--MSDN references-->
[SQL Server Data Tools]: https://msdn.microsoft.com/library/mt204009.aspx

<!--Other web references-->
[Azure portal]: http://portal.azure.com/

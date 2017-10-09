---
title: aaaFix is een verbindingsfout SQL tijdelijke fout | Microsoft Docs
description: 'Ontdek hoe tootroubleshoot, onderzoeken en te voorkomen dat een SQL-fout of een tijdelijke fout in Azure SQL Database. '
keywords: SQL-verbinding, verbindingsreeks, problemen met de netwerkverbinding, tijdelijke fout, is een verbindingsfout
services: sql-database
documentationcenter: 
author: dalechen
manager: cshepard
editor: 
ms.assetid: efb35451-3fed-4264-bf86-72b350f67d50
ms.service: sql-database
ms.custom: develop apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: daleche
ms.openlocfilehash: d225e610b9e88170ab53ca16d615bd07220603cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-diagnose-and-prevent-sql-connection-errors-and-transient-errors-for-sql-database"></a><span data-ttu-id="9d641-104">Oplossen, opsporen en voorkomen van SQL-verbindingsfouten en tijdelijke fouten voor SQL-database</span><span class="sxs-lookup"><span data-stu-id="9d641-104">Troubleshoot, diagnose, and prevent SQL connection errors and transient errors for SQL Database</span></span>
<span data-ttu-id="9d641-105">Dit artikel wordt beschreven hoe tooprevent, oplossen, analyseren en beperken van verbindingsfouten en tijdelijke fouten die uw clienttoepassing tegenkomt wanneer deze met Azure SQL Database samenwerkt.</span><span class="sxs-lookup"><span data-stu-id="9d641-105">This article describes how tooprevent, troubleshoot, diagnose, and mitigate connection errors and transient errors that your client application encounters when it interacts with Azure SQL Database.</span></span> <span data-ttu-id="9d641-106">Informatie over hoe tooconfigure Pogingslogica, Hallo-verbindingsreeks en andere instellingen aanpassen.</span><span class="sxs-lookup"><span data-stu-id="9d641-106">Learn how tooconfigure retry logic, build hello connection string, and adjust other connection settings.</span></span>

<a id="i-transient-faults" name="i-transient-faults"></a>

## <a name="transient-errors-transient-faults"></a><span data-ttu-id="9d641-107">Tijdelijke fouten (tijdelijke fouten)</span><span class="sxs-lookup"><span data-stu-id="9d641-107">Transient errors (transient faults)</span></span>
<span data-ttu-id="9d641-108">Een tijdelijke fout - ook tijdelijke fout - heeft een oorzaak die wordt binnenkort automatisch opgelost.</span><span class="sxs-lookup"><span data-stu-id="9d641-108">A transient error - also, transient fault - has an underlying cause that will soon resolve itself.</span></span> <span data-ttu-id="9d641-109">Een incidentele oorzaak van tijdelijke fouten is wanneer hello Azure systeem snel hardware resources toobetter verdelen verschillende workloads verschuift.</span><span class="sxs-lookup"><span data-stu-id="9d641-109">An occasional cause of transient errors is when hello Azure system quickly shifts hardware resources toobetter load-balance various workloads.</span></span> <span data-ttu-id="9d641-110">De meeste van deze gebeurtenissen herconfiguratie vaak voltooid in minder dan 60 seconden.</span><span class="sxs-lookup"><span data-stu-id="9d641-110">Most of these reconfiguration events often complete in less than 60 seconds.</span></span> <span data-ttu-id="9d641-111">Tijdens deze tijdsspanne herconfiguratie wellicht hebt u connectiviteit problemen tooAzure SQL-Database.</span><span class="sxs-lookup"><span data-stu-id="9d641-111">During this reconfiguration time span, you may have connectivity issues tooAzure SQL Database.</span></span> <span data-ttu-id="9d641-112">Toepassingen verbinding tooAzure SQL-Database moet worden opgebouwd tooexpect deze tijdelijke fouten ingang ze door het implementeren van Pogingslogica in de code in plaats van ze toousers als toepassingsfouten halen.</span><span class="sxs-lookup"><span data-stu-id="9d641-112">Applications connecting tooAzure SQL Database should be built tooexpect these transient errors, handle them by implementing retry logic in their code instead of surfacing them toousers as application errors.</span></span>

<span data-ttu-id="9d641-113">Als uw clientprogramma ADO.NET, het programma is adviseert over tijdelijke fout Hallo Hallo throw van een **SqlException**.</span><span class="sxs-lookup"><span data-stu-id="9d641-113">If your client program is using ADO.NET, your program is told about hello transient error by hello throw of an **SqlException**.</span></span> <span data-ttu-id="9d641-114">Hallo **getal** eigenschap kan worden vergeleken op basis van de lijst Hallo van tijdelijke fouten aan de bovenkant Hallo van Hallo onderwerp: [SQL-foutcodes voor SQL-Database-clienttoepassingen](sql-database-develop-error-messages.md).</span><span class="sxs-lookup"><span data-stu-id="9d641-114">hello **Number** property can be compared against hello list of transient errors near hello top of hello topic: [SQL error codes for SQL Database client applications](sql-database-develop-error-messages.md).</span></span>

<a id="connection-versus-command" name="connection-versus-command"></a>

### <a name="connection-versus-command"></a><span data-ttu-id="9d641-115">De verbinding ten opzichte van de opdracht</span><span class="sxs-lookup"><span data-stu-id="9d641-115">Connection versus command</span></span>
<span data-ttu-id="9d641-116">U kunt opnieuw proberen Hallo SQL-verbinding of opnieuw instellen, afhankelijk van de volgende Hallo:</span><span class="sxs-lookup"><span data-stu-id="9d641-116">You'll retry hello SQL connection or establish it again, depending on hello following:</span></span>

* <span data-ttu-id="9d641-117">**Een tijdelijke fout optreedt tijdens een verbindingspoging**: Hallo verbinding moet opnieuw worden geprobeerd na enkele seconden vertraagd.</span><span class="sxs-lookup"><span data-stu-id="9d641-117">**A transient error occurs during a connection try**: hello connection should be retried after delaying for several seconds.</span></span>
* <span data-ttu-id="9d641-118">**Een tijdelijke fout optreedt tijdens de opdracht van een SQL-query**: Hallo-opdracht moet niet onmiddellijk opnieuw uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="9d641-118">**A transient error occurs during a SQL query command**: hello command should not be immediately retried.</span></span> <span data-ttu-id="9d641-119">In plaats daarvan na een vertraging Hallo verbinding moet worden opnieuw worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="9d641-119">Instead, after a delay, hello connection should be freshly established.</span></span> <span data-ttu-id="9d641-120">Vervolgens Hallo-opdracht kan opnieuw worden geprobeerd.</span><span class="sxs-lookup"><span data-stu-id="9d641-120">Then hello command can be retried.</span></span>

<a id="j-retry-logic-transient-faults" name="j-retry-logic-transient-faults"></a>

### <a name="retry-logic-for-transient-errors"></a><span data-ttu-id="9d641-121">Pogingslogica voor tijdelijke problemen</span><span class="sxs-lookup"><span data-stu-id="9d641-121">Retry logic for transient errors</span></span>
<span data-ttu-id="9d641-122">Client-programma's die soms treedt er een tijdelijke fout zijn krachtiger wanneer ze Pogingslogica bevatten.</span><span class="sxs-lookup"><span data-stu-id="9d641-122">Client programs that occasionally encounter a transient error are more robust when they contain retry logic.</span></span>

<span data-ttu-id="9d641-123">Wanneer uw programma met Azure SQL Database via een 3e partij middleware communiceert, informeren met Hallo leverancier of Hallo middleware Pogingslogica voor tijdelijke fouten bevat.</span><span class="sxs-lookup"><span data-stu-id="9d641-123">When your program communicates with Azure SQL Database through a 3rd party middleware, inquire with hello vendor whether hello middleware contains retry logic for transient errors.</span></span>

<a id="principles-for-retry" name="principles-for-retry"></a>

#### <a name="principles-for-retry"></a><span data-ttu-id="9d641-124">Principes voor een nieuwe poging</span><span class="sxs-lookup"><span data-stu-id="9d641-124">Principles for retry</span></span>
* <span data-ttu-id="9d641-125">Een poging tooopen een verbinding moet opnieuw worden geprobeerd, als tijdelijke Hallo-fout.</span><span class="sxs-lookup"><span data-stu-id="9d641-125">An attempt tooopen a connection should be retried if hello error is transient.</span></span>
* <span data-ttu-id="9d641-126">Een SQL SELECT-instructie is mislukt met een tijdelijke fout moet niet opnieuw worden geprobeerd rechtstreeks.</span><span class="sxs-lookup"><span data-stu-id="9d641-126">A SQL SELECT statement that fails with a transient error should not be retried directly.</span></span>
  
  * <span data-ttu-id="9d641-127">In plaats daarvan een nieuwe verbinding tot stand brengen en probeer vervolgens Hallo selecteren.</span><span class="sxs-lookup"><span data-stu-id="9d641-127">Instead, establish a fresh connection, and then retry hello SELECT.</span></span>
* <span data-ttu-id="9d641-128">Wanneer een UPDATE van SQL-instructie is mislukt met een tijdelijke fout, moet een nieuwe verbinding worden gemaakt voordat Hallo die update wordt herhaald.</span><span class="sxs-lookup"><span data-stu-id="9d641-128">When a SQL UPDATE statement fails with a transient error, a fresh connection should be established before hello UPDATE is retried.</span></span>
  
  * <span data-ttu-id="9d641-129">Hallo Pogingslogica moet ervoor zorgen dat Hallo gehele databasetransactie is voltooid of dat Hallo hele transactie wordt teruggedraaid.</span><span class="sxs-lookup"><span data-stu-id="9d641-129">hello retry logic must ensure that either hello entire database transaction completed, or that hello entire transaction is rolled back.</span></span>

#### <a name="other-considerations-for-retry"></a><span data-ttu-id="9d641-130">Andere overwegingen voor een nieuwe poging</span><span class="sxs-lookup"><span data-stu-id="9d641-130">Other considerations for retry</span></span>
* <span data-ttu-id="9d641-131">Een batch-programma die automatisch wordt gestart nadat de werkuren en die wordt voltooid voordat de ochtend betaalbare toovery geduld met lange tijdsintervallen tussen de nieuwe pogingen.</span><span class="sxs-lookup"><span data-stu-id="9d641-131">A batch program that is automatically started after work hours, and which will complete before morning, can afford toovery patient with long time intervals between its retry attempts.</span></span>
* <span data-ttu-id="9d641-132">Een gebruikersinterfaceprogramma moet rekening houden met Hallo menselijke neiging toogive up na een wachttijd te lang.</span><span class="sxs-lookup"><span data-stu-id="9d641-132">A user interface program should account for hello human tendency toogive up after too long a wait.</span></span>
  
  * <span data-ttu-id="9d641-133">Echter mag Hallo oplossing geen tooretry paar seconden, omdat dit beleid Hallo-systeem met aanvragen overspoelen kunt.</span><span class="sxs-lookup"><span data-stu-id="9d641-133">However, hello solution must not be tooretry every few seconds, because that policy can flood hello system with requests.</span></span>

#### <a name="interval-increase-between-retries"></a><span data-ttu-id="9d641-134">Verhoging van het interval tussen nieuwe pogingen</span><span class="sxs-lookup"><span data-stu-id="9d641-134">Interval increase between retries</span></span>
<span data-ttu-id="9d641-135">Het is raadzaam om u te stellen voor 5 seconden voordat de eerste poging.</span><span class="sxs-lookup"><span data-stu-id="9d641-135">We recommend that you delay for 5 seconds before your first retry.</span></span> <span data-ttu-id="9d641-136">Probeert het opnieuw nadat een korter is dan 5 seconden vertraging risico's overweldigend Hallo-cloudservice.</span><span class="sxs-lookup"><span data-stu-id="9d641-136">Retrying after a delay shorter than 5 seconds risks overwhelming hello cloud service.</span></span> <span data-ttu-id="9d641-137">Voor elke opeenvolgende pogingen Hallo vertraging moet worden uitgebreid exponentieel, up tooa maximaal 60 seconden.</span><span class="sxs-lookup"><span data-stu-id="9d641-137">For each subsequent retry hello delay should grow exponentially, up tooa maximum of 60 seconds.</span></span>

<span data-ttu-id="9d641-138">Een beschrijving van de Hallo *blokkerende periode* voor clients die gebruikmaken van ADO.NET is beschikbaar in [SQL Server-verbinding groeperen (ADO.NET)](http://msdn.microsoft.com/library/8xx3tyca.aspx).</span><span class="sxs-lookup"><span data-stu-id="9d641-138">A discussion of hello *blocking period* for clients that use ADO.NET is available in [SQL Server Connection Pooling (ADO.NET)](http://msdn.microsoft.com/library/8xx3tyca.aspx).</span></span>

<span data-ttu-id="9d641-139">U kunt ook het maximale aantal nieuwe pogingen tooset voordat Hallo programma zelf wordt beëindigd.</span><span class="sxs-lookup"><span data-stu-id="9d641-139">You might also want tooset a maximum number of retries before hello program self-terminates.</span></span>

#### <a name="code-samples-with-retry-logic"></a><span data-ttu-id="9d641-140">Codevoorbeelden met Pogingslogica</span><span class="sxs-lookup"><span data-stu-id="9d641-140">Code samples with retry logic</span></span>
<span data-ttu-id="9d641-141">Codevoorbeelden met Pogingslogica in diverse programmeertalen, zijn beschikbaar op:</span><span class="sxs-lookup"><span data-stu-id="9d641-141">Code samples with retry logic, in a variety of programming languages, are available at:</span></span>

* [<span data-ttu-id="9d641-142">Verbindingsbibliotheken voor SQL-Database en SQL Server</span><span class="sxs-lookup"><span data-stu-id="9d641-142">Connection libraries for SQL Database and SQL Server</span></span>](sql-database-libraries.md)

<a id="k-test-retry-logic" name="k-test-retry-logic"></a>

#### <a name="test-your-retry-logic"></a><span data-ttu-id="9d641-143">Uw Pogingslogica testen</span><span class="sxs-lookup"><span data-stu-id="9d641-143">Test your retry logic</span></span>
<span data-ttu-id="9d641-144">tootest uw Pogingslogica heeft, moet u simuleren of een fout veroorzaken, dan kan worden gecorrigeerd terwijl uw programma nog steeds actief is.</span><span class="sxs-lookup"><span data-stu-id="9d641-144">tootest your retry logic, you must simulate or cause an error than can be corrected while your program is still running.</span></span>

##### <a name="test-by-disconnecting-from-hello-network"></a><span data-ttu-id="9d641-145">Testen door Hallo netwerk verbreekt</span><span class="sxs-lookup"><span data-stu-id="9d641-145">Test by disconnecting from hello network</span></span>
<span data-ttu-id="9d641-146">Een manier die u kunt uw Pogingslogica testen is toodisconnect uw clientcomputer vanuit Hallo netwerk terwijl Hallo programma wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="9d641-146">One way you can test your retry logic is toodisconnect your client computer from hello network while hello program is running.</span></span> <span data-ttu-id="9d641-147">Hallo-fout is:</span><span class="sxs-lookup"><span data-stu-id="9d641-147">hello error will be:</span></span>

* <span data-ttu-id="9d641-148">**SqlException.Number** 11001 =</span><span class="sxs-lookup"><span data-stu-id="9d641-148">**SqlException.Number** = 11001</span></span>
* <span data-ttu-id="9d641-149">Bericht: "Er is geen host is onbekend'</span><span class="sxs-lookup"><span data-stu-id="9d641-149">Message: "No such host is known"</span></span>

<span data-ttu-id="9d641-150">Als onderdeel van Hallo proberen eerst poging, kan uw programma Hallo onjuist gespeld corrigeren en vervolgens probeert tooconnect.</span><span class="sxs-lookup"><span data-stu-id="9d641-150">As part of hello first retry attempt, your program can correct hello misspelling, and then attempt tooconnect.</span></span>

<span data-ttu-id="9d641-151">Dit praktische toomake, u de computer vanaf het netwerk Hallo loskoppelen voordat u uw programma.</span><span class="sxs-lookup"><span data-stu-id="9d641-151">toomake this practical, you unplug your computer from hello network before you start your program.</span></span> <span data-ttu-id="9d641-152">Het programma herkent vervolgens een runtime-parameter die ervoor zorgt Hallo dat:</span><span class="sxs-lookup"><span data-stu-id="9d641-152">Then your program recognizes a run time parameter that causes hello program to:</span></span>

1. <span data-ttu-id="9d641-153">11001 tooits lijst met fouten tooconsider tijdelijk toevoegen als tijdelijk.</span><span class="sxs-lookup"><span data-stu-id="9d641-153">Temporarily add 11001 tooits list of errors tooconsider as transient.</span></span>
2. <span data-ttu-id="9d641-154">De eerste verbinding gewoon proberen.</span><span class="sxs-lookup"><span data-stu-id="9d641-154">Attempt its first connection as usual.</span></span>
3. <span data-ttu-id="9d641-155">Nadat het Hallo-fout is opgetreden, verwijdert u 11001 uit Hallo-lijst.</span><span class="sxs-lookup"><span data-stu-id="9d641-155">After hello error is caught, remove 11001 from hello list.</span></span>
4. <span data-ttu-id="9d641-156">Een bericht Hallo gebruiker tooplug Hallo computer aan op Hallo netwerk weergeven.</span><span class="sxs-lookup"><span data-stu-id="9d641-156">Display a message telling hello user tooplug hello computer into hello network.</span></span>
   * <span data-ttu-id="9d641-157">Verder kan worden uitgevoerd met behulp van beide Hallo onderbreken **Console.ReadLine** methode of een dialoogvenster met de knop OK.</span><span class="sxs-lookup"><span data-stu-id="9d641-157">Pause further execution by using either hello **Console.ReadLine** method or a dialog with an OK button.</span></span> <span data-ttu-id="9d641-158">Hallo-gebruiker op Hallo Enter-toets drukt nadat Hallo computer op Hallo-netwerk aangesloten.</span><span class="sxs-lookup"><span data-stu-id="9d641-158">hello user presses hello Enter key after hello computer plugged into hello network.</span></span>
5. <span data-ttu-id="9d641-159">Probeer opnieuw tooconnect, succes verwacht.</span><span class="sxs-lookup"><span data-stu-id="9d641-159">Attempt again tooconnect, expecting success.</span></span>

##### <a name="test-by-misspelling-hello-database-name-when-connecting"></a><span data-ttu-id="9d641-160">Testen door onjuist gespeld Hallo databasenaam op om verbinding te maken</span><span class="sxs-lookup"><span data-stu-id="9d641-160">Test by misspelling hello database name when connecting</span></span>
<span data-ttu-id="9d641-161">Het programma kan Hallo gebruikersnaam voordat de eerste verbindingspoging Hallo opzettelijk Maak een typefout.</span><span class="sxs-lookup"><span data-stu-id="9d641-161">Your program can purposely misspell hello user name before hello first connection attempt.</span></span> <span data-ttu-id="9d641-162">Hallo-fout is:</span><span class="sxs-lookup"><span data-stu-id="9d641-162">hello error will be:</span></span>

* <span data-ttu-id="9d641-163">**SqlException.Number** 18456 =</span><span class="sxs-lookup"><span data-stu-id="9d641-163">**SqlException.Number** = 18456</span></span>
* <span data-ttu-id="9d641-164">Bericht: 'aanmelding is mislukt voor gebruiker 'WRONG_MyUserName'.'</span><span class="sxs-lookup"><span data-stu-id="9d641-164">Message: "Login failed for user 'WRONG_MyUserName'."</span></span>

<span data-ttu-id="9d641-165">Als onderdeel van Hallo proberen eerst poging, kan uw programma Hallo onjuist gespeld corrigeren en vervolgens probeert tooconnect.</span><span class="sxs-lookup"><span data-stu-id="9d641-165">As part of hello first retry attempt, your program can correct hello misspelling, and then attempt tooconnect.</span></span>

<span data-ttu-id="9d641-166">Dit praktische toomake, het programma kan een runtime-parameter die ervoor zorgt Hallo dat herkend:</span><span class="sxs-lookup"><span data-stu-id="9d641-166">toomake this practical, your program could recognize a run time parameter that causes hello program to:</span></span>

1. <span data-ttu-id="9d641-167">Tijdelijk 18456 tooits lijst met fouten tooconsider toevoegen als tijdelijk.</span><span class="sxs-lookup"><span data-stu-id="9d641-167">Temporarily add 18456 tooits list of errors tooconsider as transient.</span></span>
2. <span data-ttu-id="9d641-168">De naam van de gebruiker toohello 'WRONG_' opzettelijk toevoegen.</span><span class="sxs-lookup"><span data-stu-id="9d641-168">Purposely add 'WRONG_' toohello user name.</span></span>
3. <span data-ttu-id="9d641-169">Nadat het Hallo-fout is opgetreden, verwijdert u 18456 uit Hallo-lijst.</span><span class="sxs-lookup"><span data-stu-id="9d641-169">After hello error is caught, remove 18456 from hello list.</span></span>
4. <span data-ttu-id="9d641-170">'WRONG_' uit de gebruikersnaam Hallo verwijderen.</span><span class="sxs-lookup"><span data-stu-id="9d641-170">Remove 'WRONG_' from hello user name.</span></span>
5. <span data-ttu-id="9d641-171">Probeer opnieuw tooconnect, succes verwacht.</span><span class="sxs-lookup"><span data-stu-id="9d641-171">Attempt again tooconnect, expecting success.</span></span>

<a id="net-sqlconnection-parameters-for-connection-retry" name="net-sqlconnection-parameters-for-connection-retry"></a>

### <a name="net-sqlconnection-parameters-for-connection-retry"></a><span data-ttu-id="9d641-172">.NET-SqlConnection parameters voor een nieuwe poging verbinding</span><span class="sxs-lookup"><span data-stu-id="9d641-172">.NET SqlConnection parameters for connection retry</span></span>
<span data-ttu-id="9d641-173">Als uw clientprogramma tootooAzure SQL-Database verbindt met behulp van .NET Framework-klasse Hallo **System.Data.SqlClient.SqlConnection**, moet u .NET 4.6.1 of hoger (of .NET Core) zodat u van de functie van de verbinding opnieuw gebruikmaken kunt.</span><span class="sxs-lookup"><span data-stu-id="9d641-173">If your client program connects tootooAzure SQL Database by using hello .NET Framework class **System.Data.SqlClient.SqlConnection**, you should use .NET 4.6.1 or later (or .NET Core) so you can leverage its connection retry feature.</span></span> <span data-ttu-id="9d641-174">Details van de functie Hallo zijn [hier](http://go.microsoft.com/fwlink/?linkid=393996).</span><span class="sxs-lookup"><span data-stu-id="9d641-174">Details of hello feature are [here](http://go.microsoft.com/fwlink/?linkid=393996).</span></span>

<!--
2015-11-30, FwLink 393996 points toodn632678.aspx, which links tooa downloadable .docx related tooSqlClient and SQL Server 2014.
-->


<span data-ttu-id="9d641-175">Wanneer u Hallo bouwen [verbindingsreeks](http://msdn.microsoft.com/library/System.Data.SqlClient.SqlConnection.connectionstring.aspx) voor uw **SqlConnection** object, moet u waarden tussen de volgende parameters Hallo Hallo coördineren:</span><span class="sxs-lookup"><span data-stu-id="9d641-175">When you build hello [connection string](http://msdn.microsoft.com/library/System.Data.SqlClient.SqlConnection.connectionstring.aspx) for your **SqlConnection** object, you should coordinate hello values among hello following parameters:</span></span>

* <span data-ttu-id="9d641-176">ConnectRetryCount &nbsp; &nbsp; *(de standaardwaarde is 1. Bereik is 0 tot en met 255.)*</span><span class="sxs-lookup"><span data-stu-id="9d641-176">ConnectRetryCount &nbsp;&nbsp;*(Default is 1. Range is 0 through 255.)*</span></span>
* <span data-ttu-id="9d641-177">ConnectRetryInterval &nbsp; &nbsp; *(de standaardwaarde is 1 seconde. Bereik is 1 tot en met 60).*</span><span class="sxs-lookup"><span data-stu-id="9d641-177">ConnectRetryInterval &nbsp;&nbsp;*(Default is 1 second. Range is 1 through 60.)*</span></span>
* <span data-ttu-id="9d641-178">Verbindingstime-out &nbsp; &nbsp; *(de standaardwaarde is 15 seconden. Bereik is 0 tot 2147483647)*</span><span class="sxs-lookup"><span data-stu-id="9d641-178">Connection Timeout &nbsp;&nbsp;*(Default is 15 seconds. Range is 0 through 2147483647)*</span></span>

<span data-ttu-id="9d641-179">Uw gekozen waarden moet in het bijzonder Hallo gelijkheid waar te volgen:</span><span class="sxs-lookup"><span data-stu-id="9d641-179">Specifically, your chosen values should make hello following equality true:</span></span>

* <span data-ttu-id="9d641-180">Verbindingstime-out ConnectRetryCount = * ConnectionRetryInterval</span><span class="sxs-lookup"><span data-stu-id="9d641-180">Connection Timeout = ConnectRetryCount * ConnectionRetryInterval</span></span>

<span data-ttu-id="9d641-181">Bijvoorbeeld, als hello tellen = 3, en interval = 10 seconden, een time-out van alleen 29 seconden niet erg Hallo systeem voldoende tijd voor de 3e en final opnieuw op verbinding te maken krijgt: 29 < 3 * 10.</span><span class="sxs-lookup"><span data-stu-id="9d641-181">For example, if hello count = 3, and interval = 10 seconds, a timeout of only 29 seconds would not quite give hello system enough time for its 3rd and final retry at connecting: 29 < 3 * 10.</span></span>

<a id="connection-versus-command" name="connection-versus-command"></a>

### <a name="connection-versus-command"></a><span data-ttu-id="9d641-182">De verbinding ten opzichte van de opdracht</span><span class="sxs-lookup"><span data-stu-id="9d641-182">Connection versus command</span></span>
<span data-ttu-id="9d641-183">Hallo **ConnectRetryCount** en **ConnectRetryInterval** parameters, kunnen uw **SqlConnection** object opnieuw Hallo verbindingsbewerking zonder ontvangt of proberen alles uit uw programma, zoals tooyour besturingsprogramma retourneren.</span><span class="sxs-lookup"><span data-stu-id="9d641-183">hello **ConnectRetryCount** and **ConnectRetryInterval** parameters let your **SqlConnection** object retry hello connect operation without telling or bothering your program, such as returning control tooyour program.</span></span> <span data-ttu-id="9d641-184">Hallo pogingen kunnen in Hallo volgende situaties optreden:</span><span class="sxs-lookup"><span data-stu-id="9d641-184">hello retries can occur in hello following situations:</span></span>

* <span data-ttu-id="9d641-185">de methodeaanroep mySqlConnection.Open</span><span class="sxs-lookup"><span data-stu-id="9d641-185">mySqlConnection.Open method call</span></span>
* <span data-ttu-id="9d641-186">de methodeaanroep mySqlConnection.Execute</span><span class="sxs-lookup"><span data-stu-id="9d641-186">mySqlConnection.Execute method call</span></span>

<span data-ttu-id="9d641-187">Er is een geldt de volgende werkwijze.</span><span class="sxs-lookup"><span data-stu-id="9d641-187">There is a subtlety.</span></span> <span data-ttu-id="9d641-188">Als een tijdelijke fout optreedt terwijl uw *query* wordt uitgevoerd, uw **SqlConnection** -object heeft geen nieuwe poging Hallo verbindingsbewerking deze gewoon probeert niet opnieuw uw query.</span><span class="sxs-lookup"><span data-stu-id="9d641-188">If a transient error occurs while your *query* is being executed, your **SqlConnection** object does not retry hello connect operation, and it certainly does not retry your query.</span></span> <span data-ttu-id="9d641-189">Echter, **SqlConnection** zeer snel controles Hallo verbinding voordat de query voor uitvoering worden verzonden.</span><span class="sxs-lookup"><span data-stu-id="9d641-189">However, **SqlConnection** very quickly checks hello connection before sending your query for execution.</span></span> <span data-ttu-id="9d641-190">Als Hallo snelle controle een verbindingsprobleem detecteert **SqlConnection** verbindingsbewerking Hallo voor nieuwe pogingen.</span><span class="sxs-lookup"><span data-stu-id="9d641-190">If hello quick check detects a connection problem, **SqlConnection** retries hello connect operation.</span></span> <span data-ttu-id="9d641-191">Als Hallo nieuwe poging is gelukt, wordt u query verzonden voor uitvoering.</span><span class="sxs-lookup"><span data-stu-id="9d641-191">If hello retry succeeds, you query is sent for execution.</span></span>

#### <a name="should-connectretrycount-be-combined-with-application-retry-logic"></a><span data-ttu-id="9d641-192">Moet ConnectRetryCount worden gecombineerd met toepassingslogica opnieuw proberen?</span><span class="sxs-lookup"><span data-stu-id="9d641-192">Should ConnectRetryCount be combined with application retry logic?</span></span>
<span data-ttu-id="9d641-193">Stel dat uw toepassing robuuste aangepaste Pogingslogica.</span><span class="sxs-lookup"><span data-stu-id="9d641-193">Suppose your application has robust custom retry logic.</span></span> <span data-ttu-id="9d641-194">Dit mogelijk opnieuw Hallo verbindingsbewerking 4 keer.</span><span class="sxs-lookup"><span data-stu-id="9d641-194">It might retry hello connect operation 4 times.</span></span> <span data-ttu-id="9d641-195">Als u **ConnectRetryInterval** en **ConnectRetryCount** = 3 tooyour verbindingsreeks, verhoogt u Hallo opnieuw aantal too4 * 3 = 12 opnieuw probeert.</span><span class="sxs-lookup"><span data-stu-id="9d641-195">If you add **ConnectRetryInterval** and **ConnectRetryCount** =3 tooyour connection string, you will increase hello retry count too4 * 3 = 12 retries.</span></span> <span data-ttu-id="9d641-196">U kunt niet van plan bent een groot aantal pogingen.</span><span class="sxs-lookup"><span data-stu-id="9d641-196">You might not intend such a high number of retries.</span></span>

<a id="a-connection-connection-string" name="a-connection-connection-string"></a>

## <a name="connections-tooazure-sql-database"></a><span data-ttu-id="9d641-197">Verbindingen tooAzure SQL-Database</span><span class="sxs-lookup"><span data-stu-id="9d641-197">Connections tooAzure SQL Database</span></span>
<a id="c-connection-string" name="c-connection-string"></a>

### <a name="connection-connection-string"></a><span data-ttu-id="9d641-198">Verbinding: De verbindingsreeks</span><span class="sxs-lookup"><span data-stu-id="9d641-198">Connection: Connection string</span></span>
<span data-ttu-id="9d641-199">Hallo-verbindingsreeks nodig voor het verbinden van tooAzure SQL-Database is enigszins afwijken van het Hallo-tekenreeks voor het verbinden van tooMicrosoft SQL Server.</span><span class="sxs-lookup"><span data-stu-id="9d641-199">hello connection string necessary for connecting tooAzure SQL Database is slightly different from hello string for connecting tooMicrosoft SQL Server.</span></span> <span data-ttu-id="9d641-200">U kunt Hallo-verbindingsreeks voor uw database kopiëren van Hallo [Azure-portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="9d641-200">You can copy hello connection string for your database from hello [Azure portal](https://portal.azure.com/).</span></span>

[!INCLUDE [sql-database-include-connection-string-20-portalshots](../../includes/sql-database-include-connection-string-20-portalshots.md)]

<a id="b-connection-ip-address" name="b-connection-ip-address"></a>

### <a name="connection-ip-address"></a><span data-ttu-id="9d641-201">Verbinding: IP-adres</span><span class="sxs-lookup"><span data-stu-id="9d641-201">Connection: IP address</span></span>
<span data-ttu-id="9d641-202">U moet Hallo SQL-Database tooaccept servercommunicatie van Hallo IP-adres van Hallo-computer die als host fungeert voor uw clientprogramma configureren.</span><span class="sxs-lookup"><span data-stu-id="9d641-202">You must configure hello SQL Database server tooaccept communication from hello IP address of hello computer that hosts your client program.</span></span> <span data-ttu-id="9d641-203">U dit doen door de firewall-instellingen via Hallo Hallo bewerken [Azure-portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="9d641-203">You do this by editing hello firewall settings through hello [Azure portal](https://portal.azure.com/).</span></span>

<span data-ttu-id="9d641-204">Als u tooconfigure Hallo IP-adres vergeet, mislukt het programma met een handige foutbericht dat Hallo vereiste IP-adres aangeeft.</span><span class="sxs-lookup"><span data-stu-id="9d641-204">If you forget tooconfigure hello IP address, your program will fail with a handy error message that states hello necessary IP address.</span></span>

[!INCLUDE [sql-database-include-ip-address-22-portal](../../includes/sql-database-include-ip-address-22-v12portal.md)]

<span data-ttu-id="9d641-205">Zie voor meer informatie: [procedure: firewall-instellingen configureren op de SQL-Database](sql-database-configure-firewall-settings.md)</span><span class="sxs-lookup"><span data-stu-id="9d641-205">For more information, see: [How to: Configure firewall settings on SQL Database](sql-database-configure-firewall-settings.md)</span></span>

<a id="c-connection-ports" name="c-connection-ports"></a>

### <a name="connection-ports"></a><span data-ttu-id="9d641-206">Verbinding: poorten</span><span class="sxs-lookup"><span data-stu-id="9d641-206">Connection: Ports</span></span>
<span data-ttu-id="9d641-207">Normaal gesproken hoeft u alleen tooensure dat poort 1433 is geopend voor uitgaande communicatie, op Hallo-computer waarop u clientprogramma wordt gehost.</span><span class="sxs-lookup"><span data-stu-id="9d641-207">Typically you only need tooensure that port 1433 is open for outbound communication, on hello computer that hosts you client program.</span></span>

<span data-ttu-id="9d641-208">Bijvoorbeeld, wanneer uw clientprogramma wordt gehost op een Windows-computer, kunt Hallo Windows Firewall op Hallo host u tooopen poort 1433:</span><span class="sxs-lookup"><span data-stu-id="9d641-208">For example, when your client program is hosted on a Windows computer, hello Windows Firewall on hello host enables you tooopen port 1433:</span></span>

1. <span data-ttu-id="9d641-209">Hallo Configuratiescherm openen</span><span class="sxs-lookup"><span data-stu-id="9d641-209">Open hello Control Panel</span></span>
2. <span data-ttu-id="9d641-210">&gt;Alle Configuratiescherm-onderdelen</span><span class="sxs-lookup"><span data-stu-id="9d641-210">&gt; All Control Panel Items</span></span>
3. <span data-ttu-id="9d641-211">&gt;Windows Firewall</span><span class="sxs-lookup"><span data-stu-id="9d641-211">&gt; Windows Firewall</span></span>
4. <span data-ttu-id="9d641-212">&gt;Geavanceerde instellingen</span><span class="sxs-lookup"><span data-stu-id="9d641-212">&gt; Advanced Settings</span></span>
5. <span data-ttu-id="9d641-213">&gt;Regels voor uitgaande verbindingen</span><span class="sxs-lookup"><span data-stu-id="9d641-213">&gt; Outbound Rules</span></span>
6. <span data-ttu-id="9d641-214">&gt;Acties</span><span class="sxs-lookup"><span data-stu-id="9d641-214">&gt; Actions</span></span>
7. <span data-ttu-id="9d641-215">&gt;Nieuwe regel</span><span class="sxs-lookup"><span data-stu-id="9d641-215">&gt; New Rule</span></span>

<span data-ttu-id="9d641-216">Als wordt uw clientprogramma wordt gehost in Azure een virtuele machine (VM), dient u te lezen:</span><span class="sxs-lookup"><span data-stu-id="9d641-216">If your client program is hosted on an Azure virtual machine (VM), you should read:</span></span><br/><span data-ttu-id="9d641-217">[Poorten buiten 1433 voor ADO.NET 4.5 en SQL Database](sql-database-develop-direct-route-ports-adonet-v12.md).</span><span class="sxs-lookup"><span data-stu-id="9d641-217">[Ports beyond 1433 for ADO.NET 4.5 and SQL Database](sql-database-develop-direct-route-ports-adonet-v12.md).</span></span>

<span data-ttu-id="9d641-218">Zie voor achtergrondinformatie over cofiguration van poorten en IP-adres: [Azure SQL Database-firewall](sql-database-firewall-configure.md)</span><span class="sxs-lookup"><span data-stu-id="9d641-218">For background information about cofiguration of ports and IP address, see: [Azure SQL Database firewall](sql-database-firewall-configure.md)</span></span>

<a id="d-connection-ado-net-4-5" name="d-connection-ado-net-4-5"></a>

### <a name="connection-adonet-461"></a><span data-ttu-id="9d641-219">Verbinding: ADO.NET 4.6.1</span><span class="sxs-lookup"><span data-stu-id="9d641-219">Connection: ADO.NET 4.6.1</span></span>
<span data-ttu-id="9d641-220">Als het programma wordt gebruikt voor klassen als ADO.NET **System.Data.SqlClient.SqlConnection** tooconnect tooAzure SQL-Database, het is raadzaam dat u .NET Framework versie 4.6.1 of hoger.</span><span class="sxs-lookup"><span data-stu-id="9d641-220">If your program uses ADO.NET classes like **System.Data.SqlClient.SqlConnection** tooconnect tooAzure SQL Database, we recommend that you use .NET Framework version 4.6.1 or higher.</span></span>

<span data-ttu-id="9d641-221">ADO.NET 4.6.1:</span><span class="sxs-lookup"><span data-stu-id="9d641-221">ADO.NET 4.6.1:</span></span>

* <span data-ttu-id="9d641-222">Voor Azure SQL Database zich verbeterde betrouwbaarheid wanneer u een verbinding openen met behulp van Hallo **SqlConnection.Open** methode.</span><span class="sxs-lookup"><span data-stu-id="9d641-222">For Azure SQL Database, there is improved reliability when you open a connection by using hello **SqlConnection.Open** method.</span></span> <span data-ttu-id="9d641-223">Hallo **Open** methode bevat nu best effort opnieuw mechanismen antwoord tootransient fouten, voor bepaalde fouten binnen Hallo verbinding time-outperiode.</span><span class="sxs-lookup"><span data-stu-id="9d641-223">hello **Open** method now incorporates best effort retry mechanisms in response tootransient faults, for certain errors within hello Connection Timeout period.</span></span>
* <span data-ttu-id="9d641-224">Ondersteunt Groepsgewijze verbinding nodig.</span><span class="sxs-lookup"><span data-stu-id="9d641-224">Supports connection pooling.</span></span> <span data-ttu-id="9d641-225">Dit omvat een doeltreffende controle verbinding Hallo object geeft uw programma werkt.</span><span class="sxs-lookup"><span data-stu-id="9d641-225">This includes an efficient verification that hello connection object it gives your program is functioning.</span></span>

<span data-ttu-id="9d641-226">Wanneer u een verbindingsobject van een verbindingsgroep gebruikt, wordt u aangeraden dat uw programma Hallo verbinding tijdelijk sluiten wanneer deze niet direct gebruikt.</span><span class="sxs-lookup"><span data-stu-id="9d641-226">When you use a connection object from a connection pool, we recommend that your program temporarily close hello connection when not immediately using it.</span></span> <span data-ttu-id="9d641-227">Opnieuw een verbinding te openen, is geen dure Hallo manier voor het maken van een nieuwe verbinding is.</span><span class="sxs-lookup"><span data-stu-id="9d641-227">Re-opening a connection is not expensive hello way creating a new connection is.</span></span>

<span data-ttu-id="9d641-228">Als u van ADO.NET 4.0 gebruikmaakt of eerder wordt aangeraden dat u een upgrade toohello uitvoert nieuwste ADO.NET.</span><span class="sxs-lookup"><span data-stu-id="9d641-228">If you are using ADO.NET 4.0 or earlier, we recommend that you upgrade toohello latest ADO.NET.</span></span>

* <span data-ttu-id="9d641-229">U kunt vanaf November 2015 [downloaden ADO.NET 4.6.1](http://blogs.msdn.com/b/dotnet/archive/2015/11/30/net-framework-4-6-1-is-now-available.aspx).</span><span class="sxs-lookup"><span data-stu-id="9d641-229">As of November 2015, you can [download ADO.NET 4.6.1](http://blogs.msdn.com/b/dotnet/archive/2015/11/30/net-framework-4-6-1-is-now-available.aspx).</span></span>

<a id="e-diagnostics-test-utilities-connect" name="e-diagnostics-test-utilities-connect"></a>

## <a name="diagnostics"></a><span data-ttu-id="9d641-230">Diagnostiek</span><span class="sxs-lookup"><span data-stu-id="9d641-230">Diagnostics</span></span>
<a id="d-test-whether-utilities-can-connect" name="d-test-whether-utilities-can-connect"></a>

### <a name="diagnostics-test-whether-utilities-can-connect"></a><span data-ttu-id="9d641-231">Diagnostische gegevens: Testen of hulpprogramma's verbinding kunnen maken</span><span class="sxs-lookup"><span data-stu-id="9d641-231">Diagnostics: Test whether utilities can connect</span></span>
<span data-ttu-id="9d641-232">Als het programma niet tooconnect tooAzure SQL-Database, is een optie om diagnostische tootry tooconnect met een hulpprogramma's.</span><span class="sxs-lookup"><span data-stu-id="9d641-232">If your program is failing tooconnect tooAzure SQL Database, one diagnostic option is tootry tooconnect with a utility program.</span></span> <span data-ttu-id="9d641-233">In het ideale geval Hallo hulpprogramma verbinding te maken met behulp van Hallo dezelfde bibliotheek dat het programma gebruikt.</span><span class="sxs-lookup"><span data-stu-id="9d641-233">Ideally hello utility would connect by using hello same library that your program uses.</span></span>

<span data-ttu-id="9d641-234">Op elke Windows-computer probeert u deze hulpprogramma's:</span><span class="sxs-lookup"><span data-stu-id="9d641-234">On any Windows computer, you can try these utilities:</span></span>

* <span data-ttu-id="9d641-235">SQL Server Management Studio (ssms.exe) die is verbonden met ADO.NET.</span><span class="sxs-lookup"><span data-stu-id="9d641-235">SQL Server Management Studio (ssms.exe), which connects by using ADO.NET.</span></span>
* <span data-ttu-id="9d641-236">Sqlcmd.exe die verbinding met behulp van maakt [ODBC](http://msdn.microsoft.com/library/jj730308.aspx).</span><span class="sxs-lookup"><span data-stu-id="9d641-236">sqlcmd.exe, which connects by using [ODBC](http://msdn.microsoft.com/library/jj730308.aspx).</span></span>

<span data-ttu-id="9d641-237">Eenmaal zijn verbonden, test u of een korte SQL SELECT-query werkt.</span><span class="sxs-lookup"><span data-stu-id="9d641-237">Once connected, test whether a short SQL SELECT query works.</span></span>

<a id="f-diagnostics-check-open-ports" name="f-diagnostics-check-open-ports"></a>

### <a name="diagnostics-check-hello-open-ports"></a><span data-ttu-id="9d641-238">Diagnostische gegevens: Open poorten Hallo controleren</span><span class="sxs-lookup"><span data-stu-id="9d641-238">Diagnostics: Check hello open ports</span></span>
<span data-ttu-id="9d641-239">Stel dat u vermoedt dat verbindingspogingen vanwege tooport problemen mislukken.</span><span class="sxs-lookup"><span data-stu-id="9d641-239">Suppose you suspect that connection attempts are failing due tooport issues.</span></span> <span data-ttu-id="9d641-240">U kunt een hulpprogramma waarmee u over Hallo poortconfiguraties rapporten uitvoeren op uw computer.</span><span class="sxs-lookup"><span data-stu-id="9d641-240">On your computer you can run a utility that reports on hello port configurations.</span></span>

<span data-ttu-id="9d641-241">Op Linux Hallo volgende hulpprogramma's mogelijk nuttig zijn:</span><span class="sxs-lookup"><span data-stu-id="9d641-241">On Linux hello following utilities might be helpful:</span></span>

* `netstat -nap`
* `nmap -sS -O 127.0.0.1`
  * <span data-ttu-id="9d641-242">(Hallo voorbeeld waarde toobe uw IP-adres wijzigen.)</span><span class="sxs-lookup"><span data-stu-id="9d641-242">(Change hello example value toobe your IP address.)</span></span>

<span data-ttu-id="9d641-243">Op Windows hello [PortQry.exe](http://www.microsoft.com/download/details.aspx?id=17148) hulpprogramma kan handig zijn.</span><span class="sxs-lookup"><span data-stu-id="9d641-243">On Windows hello [PortQry.exe](http://www.microsoft.com/download/details.aspx?id=17148) utility might be helpful.</span></span> <span data-ttu-id="9d641-244">Hier volgt een voorbeeld van de uitvoering die Hallo poort situatie op een Azure SQL Database-server een query uitgevoerd en die is uitgevoerd op een laptopcomputer:</span><span class="sxs-lookup"><span data-stu-id="9d641-244">Here is an example execution that queried hello port situation on an Azure SQL Database server, and which was run on a laptop computer:</span></span>

```
[C:\Users\johndoe\]
>> portqry.exe -n johndoesvr9.database.windows.net -p tcp -e 1433

Querying target system called:
 johndoesvr9.database.windows.net

Attempting tooresolve name tooIP address...
Name resolved too23.100.117.95

querying...
TCP port 1433 (ms-sql-s service): LISTENING

[C:\Users\johndoe\]
>>
```


<a id="g-diagnostics-log-your-errors" name="g-diagnostics-log-your-errors"></a>

### <a name="diagnostics-log-your-errors"></a><span data-ttu-id="9d641-245">Diagnostische gegevens: Uw fouten in logboek registreren</span><span class="sxs-lookup"><span data-stu-id="9d641-245">Diagnostics: Log your errors</span></span>
<span data-ttu-id="9d641-246">Er is een onregelmatig probleem wordt soms beste gediagnosticeerd door detectie van een algemene patroon gedurende dagen of weken.</span><span class="sxs-lookup"><span data-stu-id="9d641-246">An intermittent problem is sometimes best diagnosed by detection of a general pattern over days or weeks.</span></span>

<span data-ttu-id="9d641-247">De client kan helpen bij het een diagnose door logboekregistratie van alle fouten die worden aangetroffen.</span><span class="sxs-lookup"><span data-stu-id="9d641-247">Your client can assist in a diagnosis by logging all errors it encounters.</span></span> <span data-ttu-id="9d641-248">U kunt toocorrelate Hallo logboekvermeldingen met foutgegevens met Azure SQL Database intern zichzelf registreert mogelijk.</span><span class="sxs-lookup"><span data-stu-id="9d641-248">You might be able toocorrelate hello log entries with error data that Azure SQL Database logs itself internally.</span></span>

<span data-ttu-id="9d641-249">Enterprise-bibliotheek 6 (EntLib60) biedt beheerde klassen tooassist met logboekregistratie:</span><span class="sxs-lookup"><span data-stu-id="9d641-249">Enterprise Library 6 (EntLib60) offers .NET managed classes tooassist with logging:</span></span>

* [<span data-ttu-id="9d641-250">5 - als gemakkelijk als vallen buiten een logboek: met behulp van Hallo Logging Application Block</span><span class="sxs-lookup"><span data-stu-id="9d641-250">5 - As Easy As Falling Off a Log: Using hello Logging Application Block</span></span>](http://msdn.microsoft.com/library/dn440731.aspx)

<a id="h-diagnostics-examine-logs-errors" name="h-diagnostics-examine-logs-errors"></a>

### <a name="diagnostics-examine-system-logs-for-errors"></a><span data-ttu-id="9d641-251">Diagnostische gegevens: Raadpleeg het systeemlogboek in Logboeken op fouten</span><span class="sxs-lookup"><span data-stu-id="9d641-251">Diagnostics: Examine system logs for errors</span></span>
<span data-ttu-id="9d641-252">Hier volgen enkele Transact-SQL SELECT-instructies die querylogboeken van de fout en andere informatie.</span><span class="sxs-lookup"><span data-stu-id="9d641-252">Here are some Transact-SQL SELECT statements that query logs of error and other information.</span></span>

| <span data-ttu-id="9d641-253">Query van het logboek</span><span class="sxs-lookup"><span data-stu-id="9d641-253">Query of log</span></span> | <span data-ttu-id="9d641-254">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="9d641-254">Description</span></span> |
|:--- |:--- |
| `SELECT e.*`<br/>`FROM sys.event_log AS e`<br/>`WHERE e.database_name = 'myDbName'`<br/>`AND e.event_category = 'connectivity'`<br/>`AND 2 >= DateDiff`<br/>&nbsp;&nbsp;`(hour, e.end_time, GetUtcDate())`<br/>`ORDER BY e.event_category,`<br/>&nbsp;&nbsp;`e.event_type, e.end_time;` |<span data-ttu-id="9d641-255">Hallo [sys.event_log](http://msdn.microsoft.com/library/dn270018.aspx) weergave biedt informatie over afzonderlijke gebeurtenissen, inclusief een aantal die leiden tijdelijke fouten of verbindingsproblemen tot kunnen.</span><span class="sxs-lookup"><span data-stu-id="9d641-255">hello [sys.event_log](http://msdn.microsoft.com/library/dn270018.aspx) view offers information about individual events, including some that can cause transient errors or connectivity failures.</span></span><br/><br/><span data-ttu-id="9d641-256">In het ideale geval correleren van Hallo **start_time** of **end_time** waarden met informatie over wanneer uw clientprogramma problemen ondervonden.</span><span class="sxs-lookup"><span data-stu-id="9d641-256">Ideally you can correlate hello **start_time** or **end_time** values with information about when your client program experienced problems.</span></span><br/><br/><span data-ttu-id="9d641-257">**TIP:** moet u verbinding maken met toohello **master** toorun deze database.</span><span class="sxs-lookup"><span data-stu-id="9d641-257">**TIP:** You must connect toohello **master** database toorun this.</span></span> |
| `SELECT c.*`<br/>`FROM sys.database_connection_stats AS c`<br/>`WHERE c.database_name = 'myDbName'`<br/>`AND 24 >= DateDiff`<br/>&nbsp;&nbsp;`(hour, c.end_time, GetUtcDate())`<br/>`ORDER BY c.end_time;` |<span data-ttu-id="9d641-258">Hallo [sys.database_connection_stats](http://msdn.microsoft.com/library/dn269986.aspx) weergave biedt cumulatief aantal gebeurtenistypen, voor aanvullende diagnostische gegevens.</span><span class="sxs-lookup"><span data-stu-id="9d641-258">hello [sys.database_connection_stats](http://msdn.microsoft.com/library/dn269986.aspx) view offers aggregated counts of event types, for additional diagnostics.</span></span><br/><br/><span data-ttu-id="9d641-259">**TIP:** moet u verbinding maken met toohello **master** toorun deze database.</span><span class="sxs-lookup"><span data-stu-id="9d641-259">**TIP:** You must connect toohello **master** database toorun this.</span></span> |

<a id="d-search-for-problem-events-in-the-sql-database-log" name="d-search-for-problem-events-in-the-sql-database-log"></a>

### <a name="diagnostics-search-for-problem-events-in-hello-sql-database-log"></a><span data-ttu-id="9d641-260">Diagnostische gegevens: Zoek naar gebeurtenissen in het SQL-databaselogboek Hallo probleem</span><span class="sxs-lookup"><span data-stu-id="9d641-260">Diagnostics: Search for problem events in hello SQL Database log</span></span>
<span data-ttu-id="9d641-261">U kunt zoeken naar vermeldingen over probleem gebeurtenissen in Hallo van Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="9d641-261">You can search for entries about problem events in hello log of Azure SQL Database.</span></span> <span data-ttu-id="9d641-262">Probeer het volgende Transact-SQL SELECT-instructie in Hallo Hallo **master** database:</span><span class="sxs-lookup"><span data-stu-id="9d641-262">Try hello following Transact-SQL SELECT statement in hello **master** database:</span></span>

```
SELECT
   object_name
  ,CAST(f.event_data as XML).value
      ('(/event/@timestamp)[1]', 'datetime2')                      AS [timestamp]
  ,CAST(f.event_data as XML).value
      ('(/event/data[@name="error"]/value)[1]', 'int')             AS [error]
  ,CAST(f.event_data as XML).value
      ('(/event/data[@name="state"]/value)[1]', 'int')             AS [state]
  ,CAST(f.event_data as XML).value
      ('(/event/data[@name="is_success"]/value)[1]', 'bit')        AS [is_success]
  ,CAST(f.event_data as XML).value
      ('(/event/data[@name="database_name"]/value)[1]', 'sysname') AS [database_name]
FROM
  sys.fn_xe_telemetry_blob_target_read_file('el', null, null, null) AS f
WHERE
  object_name != 'login_event'  -- Login events are numerous.
  and
  '2015-06-21' < CAST(f.event_data as XML).value
        ('(/event/@timestamp)[1]', 'datetime2')
ORDER BY
  [timestamp] DESC
;
```


#### <a name="a-few-returned-rows-from-sysfnxetelemetryblobtargetreadfile"></a><span data-ttu-id="9d641-263">Enkele geretourneerde rijen uit sys.fn_xe_telemetry_blob_target_read_file</span><span class="sxs-lookup"><span data-stu-id="9d641-263">A few returned rows from sys.fn_xe_telemetry_blob_target_read_file</span></span>
<span data-ttu-id="9d641-264">Hierna volgt wat een geretourneerde rij als volgt uitzien.</span><span class="sxs-lookup"><span data-stu-id="9d641-264">Next is what a returned row might look like.</span></span> <span data-ttu-id="9d641-265">Hallo null-waarden weergegeven zijn vaak niet null zijn in andere rijen.</span><span class="sxs-lookup"><span data-stu-id="9d641-265">hello null values shown are often not null in other rows.</span></span>

```
object_name                   timestamp                    error  state  is_success  database_name

database_xml_deadlock_report  2015-10-16 20:28:01.0090000  NULL   NULL   NULL        AdventureWorks
```


<a id="l-enterprise-library-6" name="l-enterprise-library-6"></a>

## <a name="enterprise-library-6"></a><span data-ttu-id="9d641-266">Enterprise-bibliotheek 6</span><span class="sxs-lookup"><span data-stu-id="9d641-266">Enterprise Library 6</span></span>
<span data-ttu-id="9d641-267">Enterprise-bibliotheek 6 (EntLib60) is een raamwerk van .NET-klassen waarmee u robuuste clients van cloud-services te implementeren waarbij een van de hello Azure SQL Database-service is.</span><span class="sxs-lookup"><span data-stu-id="9d641-267">Enterprise Library 6 (EntLib60) is a framework of .NET classes that helps you implement robust clients of cloud services, one of which is hello Azure SQL Database service.</span></span> <span data-ttu-id="9d641-268">U kunt speciale tooeach gebied van onderwerpen waarin EntLib60 in eerste via helpen kan zoeken:</span><span class="sxs-lookup"><span data-stu-id="9d641-268">You can locate topics dedicated tooeach area in which EntLib60 can assist by first visiting:</span></span>

* [<span data-ttu-id="9d641-269">Enterprise-bibliotheek 6 April 2013</span><span class="sxs-lookup"><span data-stu-id="9d641-269">Enterprise Library 6 - April 2013</span></span>](http://msdn.microsoft.com/library/dn169621%28v=pandp.60%29.aspx)

<span data-ttu-id="9d641-270">Pogingslogica voor tijdelijke foutafhandeling is een gebied waarin EntLib60 kan helpen:</span><span class="sxs-lookup"><span data-stu-id="9d641-270">Retry logic for handling transient errors is one area in which EntLib60 can assist:</span></span>

* [<span data-ttu-id="9d641-271">4 - perseverance, geheim van alle successen: met behulp van Hallo tijdelijke fout afhandeling van Application Block</span><span class="sxs-lookup"><span data-stu-id="9d641-271">4 - Perseverance, Secret of All Triumphs: Using hello Transient Fault Handling Application Block</span></span>](http://msdn.microsoft.com/library/dn440719%28v=pandp.60%29.aspx)

> [!NOTE]
> <span data-ttu-id="9d641-272">Hallo broncode voor EntLib60 is beschikbaar voor openbare [downloaden](http://go.microsoft.com/fwlink/p/?LinkID=290898).</span><span class="sxs-lookup"><span data-stu-id="9d641-272">hello source code for EntLib60 is available for public [download](http://go.microsoft.com/fwlink/p/?LinkID=290898).</span></span> <span data-ttu-id="9d641-273">Microsoft heeft geen plannen toomake verdere functie-updates of onderhoud tooEntLib bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="9d641-273">Microsoft has no plans toomake further feature updates or maintenance updates tooEntLib.</span></span>
> 
> 

<a id="entlib60-classes-for-transient-errors-and-retry" name="entlib60-classes-for-transient-errors-and-retry"></a>

### <a name="entlib60-classes-for-transient-errors-and-retry"></a><span data-ttu-id="9d641-274">EntLib60 klassen voor tijdelijke fouten en probeer het opnieuw</span><span class="sxs-lookup"><span data-stu-id="9d641-274">EntLib60 classes for transient errors and retry</span></span>
<span data-ttu-id="9d641-275">Hallo na EntLib60 klassen zijn bijzonder nuttig voor Pogingslogica.</span><span class="sxs-lookup"><span data-stu-id="9d641-275">hello following EntLib60 classes are particularly useful for retry logic.</span></span> <span data-ttu-id="9d641-276">Alle deze in, of zijn onder meer naamruimte Hallo **Microsoft.Practices.EnterpriseLibrary.TransientFaultHandling**:</span><span class="sxs-lookup"><span data-stu-id="9d641-276">All these  are in, or are further under, hello namespace **Microsoft.Practices.EnterpriseLibrary.TransientFaultHandling**:</span></span>

<span data-ttu-id="9d641-277">*In de naamruimte Hallo **Microsoft.Practices.EnterpriseLibrary.TransientFaultHandling**:*</span><span class="sxs-lookup"><span data-stu-id="9d641-277">*In hello namespace **Microsoft.Practices.EnterpriseLibrary.TransientFaultHandling**:*</span></span>

* <span data-ttu-id="9d641-278">**Het RetryPolicy** klasse</span><span class="sxs-lookup"><span data-stu-id="9d641-278">**RetryPolicy** class</span></span>
  
  * <span data-ttu-id="9d641-279">**ExecuteAction** methode</span><span class="sxs-lookup"><span data-stu-id="9d641-279">**ExecuteAction** method</span></span>
* <span data-ttu-id="9d641-280">**ExponentialBackoff** klasse</span><span class="sxs-lookup"><span data-stu-id="9d641-280">**ExponentialBackoff** class</span></span>
* <span data-ttu-id="9d641-281">**SqlDatabaseTransientErrorDetectionStrategy** klasse</span><span class="sxs-lookup"><span data-stu-id="9d641-281">**SqlDatabaseTransientErrorDetectionStrategy** class</span></span>
* <span data-ttu-id="9d641-282">**ReliableSqlConnection** klasse</span><span class="sxs-lookup"><span data-stu-id="9d641-282">**ReliableSqlConnection** class</span></span>
  
  * <span data-ttu-id="9d641-283">**ExecuteCommand** methode</span><span class="sxs-lookup"><span data-stu-id="9d641-283">**ExecuteCommand** method</span></span>

<span data-ttu-id="9d641-284">In de naamruimte Hallo **Microsoft.Practices.EnterpriseLibrary.TransientFaultHandling.TestSupport**:</span><span class="sxs-lookup"><span data-stu-id="9d641-284">In hello namespace **Microsoft.Practices.EnterpriseLibrary.TransientFaultHandling.TestSupport**:</span></span>

* <span data-ttu-id="9d641-285">**AlwaysTransientErrorDetectionStrategy** klasse</span><span class="sxs-lookup"><span data-stu-id="9d641-285">**AlwaysTransientErrorDetectionStrategy** class</span></span>
* <span data-ttu-id="9d641-286">**NeverTransientErrorDetectionStrategy** klasse</span><span class="sxs-lookup"><span data-stu-id="9d641-286">**NeverTransientErrorDetectionStrategy** class</span></span>

<span data-ttu-id="9d641-287">Hier vindt u koppelingen tooinformation over EntLib60:</span><span class="sxs-lookup"><span data-stu-id="9d641-287">Here are links tooinformation about EntLib60:</span></span>

* <span data-ttu-id="9d641-288">Gratis [adresboek downloaden: Developer's Guide tooMicrosoft Enterprise-bibliotheek, 2e Edition](http://www.microsoft.com/download/details.aspx?id=41145)</span><span class="sxs-lookup"><span data-stu-id="9d641-288">Free [Book Download: Developer's Guide tooMicrosoft Enterprise Library, 2nd Edition](http://www.microsoft.com/download/details.aspx?id=41145)</span></span>
* <span data-ttu-id="9d641-289">Aanbevolen procedures: [Probeer algemene richtlijnen](../best-practices-retry-general.md) is een uitstekende gedetailleerdere beschrijving van Pogingslogica.</span><span class="sxs-lookup"><span data-stu-id="9d641-289">Best practices: [Retry general guidance](../best-practices-retry-general.md) has an excellent in-depth discussion of retry logic.</span></span>
* <span data-ttu-id="9d641-290">Downloaden van NuGet [Enterprise Library - toepassing blok 6.0 afhandeling van tijdelijke fout](http://www.nuget.org/packages/EnterpriseLibrary.TransientFaultHandling/)</span><span class="sxs-lookup"><span data-stu-id="9d641-290">NuGet download of [Enterprise Library - Transient Fault Handling application block 6.0](http://www.nuget.org/packages/EnterpriseLibrary.TransientFaultHandling/)</span></span>

<a id="entlib60-the-logging-block" name="entlib60-the-logging-block"></a>

### <a name="entlib60-hello-logging-block"></a><span data-ttu-id="9d641-291">EntLib60: Hallo logboekregistratie blokkeren</span><span class="sxs-lookup"><span data-stu-id="9d641-291">EntLib60: hello logging block</span></span>
* <span data-ttu-id="9d641-292">Hallo logboekregistratie blok is een zeer flexibele en configureerbare oplossing waarmee u kunt:</span><span class="sxs-lookup"><span data-stu-id="9d641-292">hello Logging block is a highly flexible and configurable solution that allows you to:</span></span>
  
  * <span data-ttu-id="9d641-293">Maak en logboekberichten opslaan in een groot aantal verschillende locaties.</span><span class="sxs-lookup"><span data-stu-id="9d641-293">Create and store log messages in a wide variety of locations.</span></span>
  * <span data-ttu-id="9d641-294">Categoriseren en berichten filteren.</span><span class="sxs-lookup"><span data-stu-id="9d641-294">Categorize and filter messages.</span></span>
  * <span data-ttu-id="9d641-295">Contextuele informatie verzameld die handig voor foutopsporing en tracering, evenals voor controle en algemene logboekregistratie vereisten.</span><span class="sxs-lookup"><span data-stu-id="9d641-295">Collect contextual information that is useful for debugging and tracing, as well as for auditing and general logging requirements.</span></span>
* <span data-ttu-id="9d641-296">Hallo logboekregistratie blok isoleert Hallo functionaliteit logboekregistratie van Hallo logboekbestemming zodat Hallo toepassingscode consistent, ongeacht het Hallo-locatie en het type van Hallo doel logboekregistratie store.</span><span class="sxs-lookup"><span data-stu-id="9d641-296">hello Logging block abstracts hello logging functionality from hello log destination so that hello application code is consistent, irrespective of hello location and type of hello target logging store.</span></span>

<span data-ttu-id="9d641-297">Zie voor meer informatie: [5 - als gemakkelijk als vallen buiten een logboek: met behulp van Hallo Logging Application Block](https://msdn.microsoft.com/library/dn440731%28v=pandp.60%29.aspx)</span><span class="sxs-lookup"><span data-stu-id="9d641-297">For details see: [5 - As Easy As Falling Off a Log: Using hello Logging Application Block](https://msdn.microsoft.com/library/dn440731%28v=pandp.60%29.aspx)</span></span>

<a id="entlib60-istransient-method-source-code" name="entlib60-istransient-method-source-code"></a>

### <a name="entlib60-istransient-method-source-code"></a><span data-ttu-id="9d641-298">EntLib60 IsTransient methode broncode</span><span class="sxs-lookup"><span data-stu-id="9d641-298">EntLib60 IsTransient method source code</span></span>
<span data-ttu-id="9d641-299">Vervolgens Hallo **SqlDatabaseTransientErrorDetectionStrategy** klasse, Hallo C#-broncode voor Hallo **IsTransient** methode.</span><span class="sxs-lookup"><span data-stu-id="9d641-299">Next, from hello **SqlDatabaseTransientErrorDetectionStrategy** class, is hello C# source code for hello **IsTransient** method.</span></span> <span data-ttu-id="9d641-300">Hallo-broncode wordt uitleg gegeven over welke fouten zijn beschouwd als tijdelijke toobe en leveringsopties opnieuw vanaf April 2013.</span><span class="sxs-lookup"><span data-stu-id="9d641-300">hello source code clarifies which errors were considered toobe transient and worthy of retry, as of April 2013.</span></span>

<span data-ttu-id="9d641-301">Talrijke **//comment** regels zijn verwijderd uit deze kopie tooemphasize leesbaarheid.</span><span class="sxs-lookup"><span data-stu-id="9d641-301">Numerous **//comment** lines have been removed from this copy tooemphasize readability.</span></span>

```
public bool IsTransient(Exception ex)
{
  if (ex != null)
  {
    SqlException sqlException;
    if ((sqlException = ex as SqlException) != null)
    {
      // Enumerate through all errors found in hello exception.
      foreach (SqlError err in sqlException.Errors)
      {
        switch (err.Number)
        {
            // SQL Error Code: 40501
            // hello service is currently busy. Retry hello request after 10 seconds.
            // Code: (reason code toobe decoded).
          case ThrottlingCondition.ThrottlingErrorNumber:
            // Decode hello reason code from hello error message to
            // determine hello grounds for throttling.
            var condition = ThrottlingCondition.FromError(err);

            // Attach hello decoded values as additional attributes to
            // hello original SQL exception.
            sqlException.Data[condition.ThrottlingMode.GetType().Name] =
              condition.ThrottlingMode.ToString();
            sqlException.Data[condition.GetType().Name] = condition;

            return true;

          case 10928:
          case 10929:
          case 10053:
          case 10054:
          case 10060:
          case 40197:
          case 40540:
          case 40613:
          case 40143:
          case 233:
          case 64:
            // DBNETLIB Error Code: 20
            // hello instance of SQL Server you attempted tooconnect to
            // does not support encryption.
          case (int)ProcessNetLibErrorCode.EncryptionNotSupported:
            return true;
        }
      }
    }
    else if (ex is TimeoutException)
    {
      return true;
    }
    else
    {
      EntityException entityException;
      if ((entityException = ex as EntityException) != null)
      {
        return this.IsTransient(entityException.InnerException);
      }
    }
  }

  return false;
}
```


## <a name="next-steps"></a><span data-ttu-id="9d641-302">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="9d641-302">Next steps</span></span>
* <span data-ttu-id="9d641-303">Voor het oplossen van andere veelvoorkomende verbindingsproblemen van Azure SQL Database, gaat u naar [oplossen verbinding problemen tooAzure SQL-Database](sql-database-troubleshoot-common-connection-issues.md).</span><span class="sxs-lookup"><span data-stu-id="9d641-303">For troubleshooting other common Azure SQL Database connection issues, visit [Troubleshoot connection issues tooAzure SQL Database](sql-database-troubleshoot-common-connection-issues.md).</span></span>
* [<span data-ttu-id="9d641-304">SQL Server-verbinding (ADO.NET) groeperen</span><span class="sxs-lookup"><span data-stu-id="9d641-304">SQL Server Connection Pooling (ADO.NET)</span></span>](http://msdn.microsoft.com/library/8xx3tyca.aspx)
* [<span data-ttu-id="9d641-305">*Opnieuw proberen* is een Apache 2.0 in licentie gegeven algemene bibliotheek, geschreven in opnieuw **Python**, toosimplify Hallo taak opnieuw gedrag toojust over iets toe te voegen.</span><span class="sxs-lookup"><span data-stu-id="9d641-305">*Retrying* is an Apache 2.0 licensed general-purpose retrying library, written in **Python**, toosimplify hello task of adding retry behavior toojust about anything.</span></span>](https://pypi.python.org/pypi/retrying)


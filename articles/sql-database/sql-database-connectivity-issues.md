---
title: Een SQL-verbindingsfout, een tijdelijke fout oplossen | Microsoft Docs
description: 'Informatie over het oplossen van, diagnoses stellen en voorkomen dat een SQL-fout of een tijdelijke fout in Azure SQL Database. '
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
ms.openlocfilehash: ae081fc0432e36bf9f4d4f06f289386ddce37990
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-diagnose-and-prevent-sql-connection-errors-and-transient-errors-for-sql-database"></a><span data-ttu-id="f2d97-104">Oplossen, opsporen en voorkomen van SQL-verbindingsfouten en tijdelijke fouten voor SQL-database</span><span class="sxs-lookup"><span data-stu-id="f2d97-104">Troubleshoot, diagnose, and prevent SQL connection errors and transient errors for SQL Database</span></span>
<span data-ttu-id="f2d97-105">In dit artikel wordt beschreven hoe voorkomen, oplossen, analyseren en beperken verbindingsfouten en tijdelijke fouten die uw clienttoepassing tegenkomt wanneer deze met Azure SQL Database samenwerkt.</span><span class="sxs-lookup"><span data-stu-id="f2d97-105">This article describes how to prevent, troubleshoot, diagnose, and mitigate connection errors and transient errors that your client application encounters when it interacts with Azure SQL Database.</span></span> <span data-ttu-id="f2d97-106">Informatie over het configureren van Pogingslogica, de verbindingsreeks en andere verbindingsinstellingen aanpassen.</span><span class="sxs-lookup"><span data-stu-id="f2d97-106">Learn how to configure retry logic, build the connection string, and adjust other connection settings.</span></span>

<a id="i-transient-faults" name="i-transient-faults"></a>

## <a name="transient-errors-transient-faults"></a><span data-ttu-id="f2d97-107">Tijdelijke fouten (tijdelijke fouten)</span><span class="sxs-lookup"><span data-stu-id="f2d97-107">Transient errors (transient faults)</span></span>
<span data-ttu-id="f2d97-108">Een tijdelijke fout - ook tijdelijke fout - heeft een oorzaak die wordt binnenkort automatisch opgelost.</span><span class="sxs-lookup"><span data-stu-id="f2d97-108">A transient error - also, transient fault - has an underlying cause that will soon resolve itself.</span></span> <span data-ttu-id="f2d97-109">Een incidentele oorzaak van tijdelijke fouten is wanneer het Azure systeem snel hardwarebronnen betere taakverdeling verschillende workloads verschuift.</span><span class="sxs-lookup"><span data-stu-id="f2d97-109">An occasional cause of transient errors is when the Azure system quickly shifts hardware resources to better load-balance various workloads.</span></span> <span data-ttu-id="f2d97-110">De meeste van deze gebeurtenissen herconfiguratie vaak voltooid in minder dan 60 seconden.</span><span class="sxs-lookup"><span data-stu-id="f2d97-110">Most of these reconfiguration events often complete in less than 60 seconds.</span></span> <span data-ttu-id="f2d97-111">Tijdens deze tijdsspanne herconfiguratie mogelijk hebt u verbindingsproblemen met Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="f2d97-111">During this reconfiguration time span, you may have connectivity issues to Azure SQL Database.</span></span> <span data-ttu-id="f2d97-112">Verbinding maken met Azure SQL Database toepassingen moeten worden samengesteld om verwacht dat deze tijdelijke fouten, wordt deze door het implementeren van Pogingslogica in de code in plaats van ze naar gebruikers als toepassingsfouten bepaalde te verwerken.</span><span class="sxs-lookup"><span data-stu-id="f2d97-112">Applications connecting to Azure SQL Database should be built to expect these transient errors, handle them by implementing retry logic in their code instead of surfacing them to users as application errors.</span></span>

<span data-ttu-id="f2d97-113">Als uw clientprogramma ADO.NET, het programma is adviseert over de tijdelijke fout door de throw van een **SqlException**.</span><span class="sxs-lookup"><span data-stu-id="f2d97-113">If your client program is using ADO.NET, your program is told about the transient error by the throw of an **SqlException**.</span></span> <span data-ttu-id="f2d97-114">De **getal** eigenschap kan worden vergeleken in de lijst met tijdelijke fouten aan de bovenkant van het onderwerp: [SQL-foutcodes voor SQL-Database-clienttoepassingen](sql-database-develop-error-messages.md).</span><span class="sxs-lookup"><span data-stu-id="f2d97-114">The **Number** property can be compared against the list of transient errors near the top of the topic: [SQL error codes for SQL Database client applications](sql-database-develop-error-messages.md).</span></span>

<a id="connection-versus-command" name="connection-versus-command"></a>

### <a name="connection-versus-command"></a><span data-ttu-id="f2d97-115">De verbinding ten opzichte van de opdracht</span><span class="sxs-lookup"><span data-stu-id="f2d97-115">Connection versus command</span></span>
<span data-ttu-id="f2d97-116">U probeert de SQL-verbinding of opnieuw instellen, afhankelijk van het volgende:</span><span class="sxs-lookup"><span data-stu-id="f2d97-116">You'll retry the SQL connection or establish it again, depending on the following:</span></span>

* <span data-ttu-id="f2d97-117">**Een tijdelijke fout optreedt tijdens een verbindingspoging**: de verbinding moet opnieuw worden geprobeerd na enkele seconden vertraagd.</span><span class="sxs-lookup"><span data-stu-id="f2d97-117">**A transient error occurs during a connection try**: The connection should be retried after delaying for several seconds.</span></span>
* <span data-ttu-id="f2d97-118">**Een tijdelijke fout optreedt tijdens de opdracht van een SQL-query**: de opdracht mag niet onmiddellijk opnieuw uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="f2d97-118">**A transient error occurs during a SQL query command**: The command should not be immediately retried.</span></span> <span data-ttu-id="f2d97-119">In plaats daarvan na een vertraging de verbinding moet worden opnieuw worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="f2d97-119">Instead, after a delay, the connection should be freshly established.</span></span> <span data-ttu-id="f2d97-120">Vervolgens de opdracht kan opnieuw worden geprobeerd.</span><span class="sxs-lookup"><span data-stu-id="f2d97-120">Then the command can be retried.</span></span>

<a id="j-retry-logic-transient-faults" name="j-retry-logic-transient-faults"></a>

### <a name="retry-logic-for-transient-errors"></a><span data-ttu-id="f2d97-121">Pogingslogica voor tijdelijke problemen</span><span class="sxs-lookup"><span data-stu-id="f2d97-121">Retry logic for transient errors</span></span>
<span data-ttu-id="f2d97-122">Client-programma's die soms treedt er een tijdelijke fout zijn krachtiger wanneer ze Pogingslogica bevatten.</span><span class="sxs-lookup"><span data-stu-id="f2d97-122">Client programs that occasionally encounter a transient error are more robust when they contain retry logic.</span></span>

<span data-ttu-id="f2d97-123">Wanneer uw programma met Azure SQL Database via een 3e partij middleware communiceert, informeren met de leverancier of de middleware Pogingslogica voor tijdelijke fouten bevat.</span><span class="sxs-lookup"><span data-stu-id="f2d97-123">When your program communicates with Azure SQL Database through a 3rd party middleware, inquire with the vendor whether the middleware contains retry logic for transient errors.</span></span>

<a id="principles-for-retry" name="principles-for-retry"></a>

#### <a name="principles-for-retry"></a><span data-ttu-id="f2d97-124">Principes voor een nieuwe poging</span><span class="sxs-lookup"><span data-stu-id="f2d97-124">Principles for retry</span></span>
* <span data-ttu-id="f2d97-125">Een poging om een verbinding te openen, moet opnieuw worden uitgevoerd als de fout tijdelijk is.</span><span class="sxs-lookup"><span data-stu-id="f2d97-125">An attempt to open a connection should be retried if the error is transient.</span></span>
* <span data-ttu-id="f2d97-126">Een SQL SELECT-instructie is mislukt met een tijdelijke fout moet niet opnieuw worden geprobeerd rechtstreeks.</span><span class="sxs-lookup"><span data-stu-id="f2d97-126">A SQL SELECT statement that fails with a transient error should not be retried directly.</span></span>
  
  * <span data-ttu-id="f2d97-127">In plaats daarvan een nieuwe verbinding tot stand brengen en probeer vervolgens de is geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="f2d97-127">Instead, establish a fresh connection, and then retry the SELECT.</span></span>
* <span data-ttu-id="f2d97-128">Wanneer een UPDATE van SQL-instructie is mislukt met een tijdelijke fout, moet een nieuwe verbinding worden ingesteld voordat de UPDATE wordt herhaald.</span><span class="sxs-lookup"><span data-stu-id="f2d97-128">When a SQL UPDATE statement fails with a transient error, a fresh connection should be established before the UPDATE is retried.</span></span>
  
  * <span data-ttu-id="f2d97-129">De Pogingslogica moet ervoor zorgen dat de gehele databasetransactie is voltooid of dat de hele transactie wordt teruggedraaid.</span><span class="sxs-lookup"><span data-stu-id="f2d97-129">The retry logic must ensure that either the entire database transaction completed, or that the entire transaction is rolled back.</span></span>

#### <a name="other-considerations-for-retry"></a><span data-ttu-id="f2d97-130">Andere overwegingen voor een nieuwe poging</span><span class="sxs-lookup"><span data-stu-id="f2d97-130">Other considerations for retry</span></span>
* <span data-ttu-id="f2d97-131">Een batch-programma die automatisch wordt gestart nadat de werkuren en die wordt voltooid voordat de ochtend toestaan van zeer geduld met lange tijdsintervallen tussen de nieuwe pogingen.</span><span class="sxs-lookup"><span data-stu-id="f2d97-131">A batch program that is automatically started after work hours, and which will complete before morning, can afford to very patient with long time intervals between its retry attempts.</span></span>
* <span data-ttu-id="f2d97-132">Een gebruikersinterfaceprogramma moet rekening houden met de menselijke neiging te geven, na een wachttijd te lang.</span><span class="sxs-lookup"><span data-stu-id="f2d97-132">A user interface program should account for the human tendency to give up after too long a wait.</span></span>
  
  * <span data-ttu-id="f2d97-133">De oplossing moet echter niet opnieuw proberen om de paar seconden worden omdat dit beleid kan het systeem met aanvragen overspoelen.</span><span class="sxs-lookup"><span data-stu-id="f2d97-133">However, the solution must not be to retry every few seconds, because that policy can flood the system with requests.</span></span>

#### <a name="interval-increase-between-retries"></a><span data-ttu-id="f2d97-134">Verhoging van het interval tussen nieuwe pogingen</span><span class="sxs-lookup"><span data-stu-id="f2d97-134">Interval increase between retries</span></span>
<span data-ttu-id="f2d97-135">Het is raadzaam om u te stellen voor 5 seconden voordat de eerste poging.</span><span class="sxs-lookup"><span data-stu-id="f2d97-135">We recommend that you delay for 5 seconds before your first retry.</span></span> <span data-ttu-id="f2d97-136">Opnieuw proberen na een vertraging die korter is dan 5 seconden risico's die zijn afgeleid van de cloudservice.</span><span class="sxs-lookup"><span data-stu-id="f2d97-136">Retrying after a delay shorter than 5 seconds risks overwhelming the cloud service.</span></span> <span data-ttu-id="f2d97-137">Voor elke opeenvolgende pogingen de vertraging exponentieel, moet groeien maximaal 60 seconden.</span><span class="sxs-lookup"><span data-stu-id="f2d97-137">For each subsequent retry the delay should grow exponentially, up to a maximum of 60 seconds.</span></span>

<span data-ttu-id="f2d97-138">Een bespreking van de *blokkerende periode* voor clients die gebruikmaken van ADO.NET is beschikbaar in [SQL Server-verbinding groeperen (ADO.NET)](http://msdn.microsoft.com/library/8xx3tyca.aspx).</span><span class="sxs-lookup"><span data-stu-id="f2d97-138">A discussion of the *blocking period* for clients that use ADO.NET is available in [SQL Server Connection Pooling (ADO.NET)](http://msdn.microsoft.com/library/8xx3tyca.aspx).</span></span>

<span data-ttu-id="f2d97-139">U kunt ook het maximale aantal nieuwe pogingen ingesteld voordat het programma zelf wordt beëindigd.</span><span class="sxs-lookup"><span data-stu-id="f2d97-139">You might also want to set a maximum number of retries before the program self-terminates.</span></span>

#### <a name="code-samples-with-retry-logic"></a><span data-ttu-id="f2d97-140">Codevoorbeelden met Pogingslogica</span><span class="sxs-lookup"><span data-stu-id="f2d97-140">Code samples with retry logic</span></span>
<span data-ttu-id="f2d97-141">Codevoorbeelden met Pogingslogica in diverse programmeertalen, zijn beschikbaar op:</span><span class="sxs-lookup"><span data-stu-id="f2d97-141">Code samples with retry logic, in a variety of programming languages, are available at:</span></span>

* [<span data-ttu-id="f2d97-142">Verbindingsbibliotheken voor SQL-Database en SQL Server</span><span class="sxs-lookup"><span data-stu-id="f2d97-142">Connection libraries for SQL Database and SQL Server</span></span>](sql-database-libraries.md)

<a id="k-test-retry-logic" name="k-test-retry-logic"></a>

#### <a name="test-your-retry-logic"></a><span data-ttu-id="f2d97-143">Uw Pogingslogica testen</span><span class="sxs-lookup"><span data-stu-id="f2d97-143">Test your retry logic</span></span>
<span data-ttu-id="f2d97-144">Als u wilt testen uw Pogingslogica, moet u simuleren of een fout veroorzaken, dan kan worden gecorrigeerd terwijl uw programma nog steeds actief is.</span><span class="sxs-lookup"><span data-stu-id="f2d97-144">To test your retry logic, you must simulate or cause an error than can be corrected while your program is still running.</span></span>

##### <a name="test-by-disconnecting-from-the-network"></a><span data-ttu-id="f2d97-145">Testen door het netwerk verbreekt</span><span class="sxs-lookup"><span data-stu-id="f2d97-145">Test by disconnecting from the network</span></span>
<span data-ttu-id="f2d97-146">Een manier kunt u uw Pogingslogica testen is op uw computer loskoppelen van het netwerk terwijl het programma wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="f2d97-146">One way you can test your retry logic is to disconnect your client computer from the network while the program is running.</span></span> <span data-ttu-id="f2d97-147">De fout is:</span><span class="sxs-lookup"><span data-stu-id="f2d97-147">The error will be:</span></span>

* <span data-ttu-id="f2d97-148">**SqlException.Number** 11001 =</span><span class="sxs-lookup"><span data-stu-id="f2d97-148">**SqlException.Number** = 11001</span></span>
* <span data-ttu-id="f2d97-149">Bericht: "Er is geen host is onbekend'</span><span class="sxs-lookup"><span data-stu-id="f2d97-149">Message: "No such host is known"</span></span>

<span data-ttu-id="f2d97-150">Als onderdeel van de eerste nieuwe poging, uw programma Corrigeer de onjuist gespeld, en vervolgens probeert te verbinden.</span><span class="sxs-lookup"><span data-stu-id="f2d97-150">As part of the first retry attempt, your program can correct the misspelling, and then attempt to connect.</span></span>

<span data-ttu-id="f2d97-151">Om dit praktisch, loskoppelen u uw computer via het netwerk voordat u uw programma.</span><span class="sxs-lookup"><span data-stu-id="f2d97-151">To make this practical, you unplug your computer from the network before you start your program.</span></span> <span data-ttu-id="f2d97-152">Het programma herkent vervolgens een runtime-parameter zorgt ervoor dat het programma:</span><span class="sxs-lookup"><span data-stu-id="f2d97-152">Then your program recognizes a run time parameter that causes the program to:</span></span>

1. <span data-ttu-id="f2d97-153">11001 tijdelijk toevoegen aan de lijst met fouten in overweging moet nemen als tijdelijk.</span><span class="sxs-lookup"><span data-stu-id="f2d97-153">Temporarily add 11001 to its list of errors to consider as transient.</span></span>
2. <span data-ttu-id="f2d97-154">De eerste verbinding gewoon proberen.</span><span class="sxs-lookup"><span data-stu-id="f2d97-154">Attempt its first connection as usual.</span></span>
3. <span data-ttu-id="f2d97-155">Nadat de fout is opgetreden, 11001 uit de lijst verwijderen.</span><span class="sxs-lookup"><span data-stu-id="f2d97-155">After the error is caught, remove 11001 from the list.</span></span>
4. <span data-ttu-id="f2d97-156">Een bericht aan van de gebruiker op de computer op het netwerk aansluiten weergeven.</span><span class="sxs-lookup"><span data-stu-id="f2d97-156">Display a message telling the user to plug the computer into the network.</span></span>
   * <span data-ttu-id="f2d97-157">Onderbreken verder worden uitgevoerd met behulp van de **Console.ReadLine** methode of een dialoogvenster met de knop OK.</span><span class="sxs-lookup"><span data-stu-id="f2d97-157">Pause further execution by using either the **Console.ReadLine** method or a dialog with an OK button.</span></span> <span data-ttu-id="f2d97-158">De gebruiker op de Enter-toets drukt nadat de computer is aangesloten op het netwerk.</span><span class="sxs-lookup"><span data-stu-id="f2d97-158">The user presses the Enter key after the computer plugged into the network.</span></span>
5. <span data-ttu-id="f2d97-159">Opnieuw verbinding probeert te, succes verwacht.</span><span class="sxs-lookup"><span data-stu-id="f2d97-159">Attempt again to connect, expecting success.</span></span>

##### <a name="test-by-misspelling-the-database-name-when-connecting"></a><span data-ttu-id="f2d97-160">Testen door de databasenaam bevat een typefout wanneer verbinding wordt gemaakt</span><span class="sxs-lookup"><span data-stu-id="f2d97-160">Test by misspelling the database name when connecting</span></span>
<span data-ttu-id="f2d97-161">Het programma kan de naam van de gebruiker voordat de eerste verbindingspoging opzettelijk Maak een typefout.</span><span class="sxs-lookup"><span data-stu-id="f2d97-161">Your program can purposely misspell the user name before the first connection attempt.</span></span> <span data-ttu-id="f2d97-162">De fout is:</span><span class="sxs-lookup"><span data-stu-id="f2d97-162">The error will be:</span></span>

* <span data-ttu-id="f2d97-163">**SqlException.Number** 18456 =</span><span class="sxs-lookup"><span data-stu-id="f2d97-163">**SqlException.Number** = 18456</span></span>
* <span data-ttu-id="f2d97-164">Bericht: 'aanmelding is mislukt voor gebruiker 'WRONG_MyUserName'.'</span><span class="sxs-lookup"><span data-stu-id="f2d97-164">Message: "Login failed for user 'WRONG_MyUserName'."</span></span>

<span data-ttu-id="f2d97-165">Als onderdeel van de eerste nieuwe poging, uw programma Corrigeer de onjuist gespeld, en vervolgens probeert te verbinden.</span><span class="sxs-lookup"><span data-stu-id="f2d97-165">As part of the first retry attempt, your program can correct the misspelling, and then attempt to connect.</span></span>

<span data-ttu-id="f2d97-166">Om dit praktisch, kan uw programma herkend door een runtime-parameter zorgt ervoor dat het programma:</span><span class="sxs-lookup"><span data-stu-id="f2d97-166">To make this practical, your program could recognize a run time parameter that causes the program to:</span></span>

1. <span data-ttu-id="f2d97-167">Tijdelijk 18456 toevoegen aan de lijst met fouten in overweging moet nemen als tijdelijk.</span><span class="sxs-lookup"><span data-stu-id="f2d97-167">Temporarily add 18456 to its list of errors to consider as transient.</span></span>
2. <span data-ttu-id="f2d97-168">Opzettelijk 'WRONG_' toevoegen aan de gebruikersnaam.</span><span class="sxs-lookup"><span data-stu-id="f2d97-168">Purposely add 'WRONG_' to the user name.</span></span>
3. <span data-ttu-id="f2d97-169">Nadat de fout is opgetreden, 18456 uit de lijst verwijderen.</span><span class="sxs-lookup"><span data-stu-id="f2d97-169">After the error is caught, remove 18456 from the list.</span></span>
4. <span data-ttu-id="f2d97-170">'WRONG_' verwijderen uit de gebruikersnaam.</span><span class="sxs-lookup"><span data-stu-id="f2d97-170">Remove 'WRONG_' from the user name.</span></span>
5. <span data-ttu-id="f2d97-171">Opnieuw verbinding probeert te, succes verwacht.</span><span class="sxs-lookup"><span data-stu-id="f2d97-171">Attempt again to connect, expecting success.</span></span>

<a id="net-sqlconnection-parameters-for-connection-retry" name="net-sqlconnection-parameters-for-connection-retry"></a>

### <a name="net-sqlconnection-parameters-for-connection-retry"></a><span data-ttu-id="f2d97-172">.NET-SqlConnection parameters voor een nieuwe poging verbinding</span><span class="sxs-lookup"><span data-stu-id="f2d97-172">.NET SqlConnection parameters for connection retry</span></span>
<span data-ttu-id="f2d97-173">Als uw clientprogramma verbindt met naar Azure SQL Database met behulp van de .NET Framework-klasse **System.Data.SqlClient.SqlConnection**, moet u .NET 4.6.1 of hoger (of .NET Core) zodat u van de functie van de verbinding opnieuw gebruikmaken kunt.</span><span class="sxs-lookup"><span data-stu-id="f2d97-173">If your client program connects to to Azure SQL Database by using the .NET Framework class **System.Data.SqlClient.SqlConnection**, you should use .NET 4.6.1 or later (or .NET Core) so you can leverage its connection retry feature.</span></span> <span data-ttu-id="f2d97-174">Details van de functie zijn [hier](http://go.microsoft.com/fwlink/?linkid=393996).</span><span class="sxs-lookup"><span data-stu-id="f2d97-174">Details of the feature are [here](http://go.microsoft.com/fwlink/?linkid=393996).</span></span>

<!--
2015-11-30, FwLink 393996 points to dn632678.aspx, which links to a downloadable .docx related to SqlClient and SQL Server 2014.
-->


<span data-ttu-id="f2d97-175">Wanneer u bouwt het [verbindingsreeks](http://msdn.microsoft.com/library/System.Data.SqlClient.SqlConnection.connectionstring.aspx) voor uw **SqlConnection** object, moet u de waarden onder de volgende parameters coördineren:</span><span class="sxs-lookup"><span data-stu-id="f2d97-175">When you build the [connection string](http://msdn.microsoft.com/library/System.Data.SqlClient.SqlConnection.connectionstring.aspx) for your **SqlConnection** object, you should coordinate the values among the following parameters:</span></span>

* <span data-ttu-id="f2d97-176">ConnectRetryCount &nbsp; &nbsp; *(de standaardwaarde is 1. Bereik is 0 tot en met 255.)*</span><span class="sxs-lookup"><span data-stu-id="f2d97-176">ConnectRetryCount &nbsp;&nbsp;*(Default is 1. Range is 0 through 255.)*</span></span>
* <span data-ttu-id="f2d97-177">ConnectRetryInterval &nbsp; &nbsp; *(de standaardwaarde is 1 seconde. Bereik is 1 tot en met 60).*</span><span class="sxs-lookup"><span data-stu-id="f2d97-177">ConnectRetryInterval &nbsp;&nbsp;*(Default is 1 second. Range is 1 through 60.)*</span></span>
* <span data-ttu-id="f2d97-178">Verbindingstime-out &nbsp; &nbsp; *(de standaardwaarde is 15 seconden. Bereik is 0 tot 2147483647)*</span><span class="sxs-lookup"><span data-stu-id="f2d97-178">Connection Timeout &nbsp;&nbsp;*(Default is 15 seconds. Range is 0 through 2147483647)*</span></span>

<span data-ttu-id="f2d97-179">In het bijzonder moet uw gekozen waarden de volgende gelijkheid true:</span><span class="sxs-lookup"><span data-stu-id="f2d97-179">Specifically, your chosen values should make the following equality true:</span></span>

* <span data-ttu-id="f2d97-180">Verbindingstime-out ConnectRetryCount = * ConnectionRetryInterval</span><span class="sxs-lookup"><span data-stu-id="f2d97-180">Connection Timeout = ConnectRetryCount * ConnectionRetryInterval</span></span>

<span data-ttu-id="f2d97-181">Bijvoorbeeld, als het aantal = 3, en interval = 10 seconden, een time-out van alleen 29 seconden niet erg, het systeem genoeg tijd voor de 3e en final opnieuw op verbinding te maken krijgt: 29 < 3 * 10.</span><span class="sxs-lookup"><span data-stu-id="f2d97-181">For example, if the count = 3, and interval = 10 seconds, a timeout of only 29 seconds would not quite give the system enough time for its 3rd and final retry at connecting: 29 < 3 * 10.</span></span>

<a id="connection-versus-command" name="connection-versus-command"></a>

### <a name="connection-versus-command"></a><span data-ttu-id="f2d97-182">De verbinding ten opzichte van de opdracht</span><span class="sxs-lookup"><span data-stu-id="f2d97-182">Connection versus command</span></span>
<span data-ttu-id="f2d97-183">De **ConnectRetryCount** en **ConnectRetryInterval** parameters, kunnen uw **SqlConnection** object probeer het opnieuw verbinden zonder ontvangt of proberen alles uit uw programma, zoals het besturingselement wordt teruggezonden naar uw programma.</span><span class="sxs-lookup"><span data-stu-id="f2d97-183">The **ConnectRetryCount** and **ConnectRetryInterval** parameters let your **SqlConnection** object retry the connect operation without telling or bothering your program, such as returning control to your program.</span></span> <span data-ttu-id="f2d97-184">De nieuwe pogingen kunnen optreden in de volgende situaties:</span><span class="sxs-lookup"><span data-stu-id="f2d97-184">The retries can occur in the following situations:</span></span>

* <span data-ttu-id="f2d97-185">de methodeaanroep mySqlConnection.Open</span><span class="sxs-lookup"><span data-stu-id="f2d97-185">mySqlConnection.Open method call</span></span>
* <span data-ttu-id="f2d97-186">de methodeaanroep mySqlConnection.Execute</span><span class="sxs-lookup"><span data-stu-id="f2d97-186">mySqlConnection.Execute method call</span></span>

<span data-ttu-id="f2d97-187">Er is een geldt de volgende werkwijze.</span><span class="sxs-lookup"><span data-stu-id="f2d97-187">There is a subtlety.</span></span> <span data-ttu-id="f2d97-188">Als een tijdelijke fout optreedt terwijl uw *query* wordt uitgevoerd, uw **SqlConnection** object komt niet opnieuw verbinding maken en deze gewoon probeert niet opnieuw uw query.</span><span class="sxs-lookup"><span data-stu-id="f2d97-188">If a transient error occurs while your *query* is being executed, your **SqlConnection** object does not retry the connect operation, and it certainly does not retry your query.</span></span> <span data-ttu-id="f2d97-189">Echter, **SqlConnection** zeer snel controleert de verbinding voordat de query voor uitvoering worden verzonden.</span><span class="sxs-lookup"><span data-stu-id="f2d97-189">However, **SqlConnection** very quickly checks the connection before sending your query for execution.</span></span> <span data-ttu-id="f2d97-190">Als de snelle controle een verbindingsprobleem detecteert **SqlConnection** opnieuw probeert de bewerking verbinding maken.</span><span class="sxs-lookup"><span data-stu-id="f2d97-190">If the quick check detects a connection problem, **SqlConnection** retries the connect operation.</span></span> <span data-ttu-id="f2d97-191">Als de nieuwe poging is gelukt, wordt u query verzonden voor uitvoering.</span><span class="sxs-lookup"><span data-stu-id="f2d97-191">If the retry succeeds, you query is sent for execution.</span></span>

#### <a name="should-connectretrycount-be-combined-with-application-retry-logic"></a><span data-ttu-id="f2d97-192">Moet ConnectRetryCount worden gecombineerd met toepassingslogica opnieuw proberen?</span><span class="sxs-lookup"><span data-stu-id="f2d97-192">Should ConnectRetryCount be combined with application retry logic?</span></span>
<span data-ttu-id="f2d97-193">Stel dat uw toepassing robuuste aangepaste Pogingslogica.</span><span class="sxs-lookup"><span data-stu-id="f2d97-193">Suppose your application has robust custom retry logic.</span></span> <span data-ttu-id="f2d97-194">Deze mogelijk opnieuw verbinding maken met 4 keer.</span><span class="sxs-lookup"><span data-stu-id="f2d97-194">It might retry the connect operation 4 times.</span></span> <span data-ttu-id="f2d97-195">Als u **ConnectRetryInterval** en **ConnectRetryCount** = 3 op uw verbindingsreeks verhoogt u het maximale aantal pogingen tot en met 4 * 3 = 12 nieuwe pogingen.</span><span class="sxs-lookup"><span data-stu-id="f2d97-195">If you add **ConnectRetryInterval** and **ConnectRetryCount** =3 to your connection string, you will increase the retry count to 4 * 3 = 12 retries.</span></span> <span data-ttu-id="f2d97-196">U kunt niet van plan bent een groot aantal pogingen.</span><span class="sxs-lookup"><span data-stu-id="f2d97-196">You might not intend such a high number of retries.</span></span>

<a id="a-connection-connection-string" name="a-connection-connection-string"></a>

## <a name="connections-to-azure-sql-database"></a><span data-ttu-id="f2d97-197">Verbindingen met Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="f2d97-197">Connections to Azure SQL Database</span></span>
<a id="c-connection-string" name="c-connection-string"></a>

### <a name="connection-connection-string"></a><span data-ttu-id="f2d97-198">Verbinding: De verbindingsreeks</span><span class="sxs-lookup"><span data-stu-id="f2d97-198">Connection: Connection string</span></span>
<span data-ttu-id="f2d97-199">De verbindingsreeks nodig voor het verbinden met Azure SQL Database is enigszins afwijken van de tekenreeks voor het verbinden met Microsoft SQL Server.</span><span class="sxs-lookup"><span data-stu-id="f2d97-199">The connection string necessary for connecting to Azure SQL Database is slightly different from the string for connecting to Microsoft SQL Server.</span></span> <span data-ttu-id="f2d97-200">U kunt de verbindingsreeks kopiëren voor uw database van de [Azure-portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="f2d97-200">You can copy the connection string for your database from the [Azure portal](https://portal.azure.com/).</span></span>

[!INCLUDE [sql-database-include-connection-string-20-portalshots](../../includes/sql-database-include-connection-string-20-portalshots.md)]

<a id="b-connection-ip-address" name="b-connection-ip-address"></a>

### <a name="connection-ip-address"></a><span data-ttu-id="f2d97-201">Verbinding: IP-adres</span><span class="sxs-lookup"><span data-stu-id="f2d97-201">Connection: IP address</span></span>
<span data-ttu-id="f2d97-202">U moet de SQL-databaseserver voor het accepteren van communicatie van het IP-adres van de computer die als host fungeert voor uw clientprogramma configureren.</span><span class="sxs-lookup"><span data-stu-id="f2d97-202">You must configure the SQL Database server to accept communication from the IP address of the computer that hosts your client program.</span></span> <span data-ttu-id="f2d97-203">U dit doen door het bewerken van de firewallinstellingen via de [Azure-portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="f2d97-203">You do this by editing the firewall settings through the [Azure portal](https://portal.azure.com/).</span></span>

<span data-ttu-id="f2d97-204">Als u vergeet voor het configureren van het IP-adres, mislukt het programma met een handige foutbericht dat aangeeft van de vereiste IP-adres.</span><span class="sxs-lookup"><span data-stu-id="f2d97-204">If you forget to configure the IP address, your program will fail with a handy error message that states the necessary IP address.</span></span>

[!INCLUDE [sql-database-include-ip-address-22-portal](../../includes/sql-database-include-ip-address-22-v12portal.md)]

<span data-ttu-id="f2d97-205">Zie voor meer informatie: [procedure: firewall-instellingen configureren op de SQL-Database](sql-database-configure-firewall-settings.md)</span><span class="sxs-lookup"><span data-stu-id="f2d97-205">For more information, see: [How to: Configure firewall settings on SQL Database](sql-database-configure-firewall-settings.md)</span></span>

<a id="c-connection-ports" name="c-connection-ports"></a>

### <a name="connection-ports"></a><span data-ttu-id="f2d97-206">Verbinding: poorten</span><span class="sxs-lookup"><span data-stu-id="f2d97-206">Connection: Ports</span></span>
<span data-ttu-id="f2d97-207">Normaal gesproken alleen moet u ervoor zorgen dat poort 1433 is geopend voor uitgaande communicatie, op de computer waarop u clientprogramma wordt gehost.</span><span class="sxs-lookup"><span data-stu-id="f2d97-207">Typically you only need to ensure that port 1433 is open for outbound communication, on the computer that hosts you client program.</span></span>

<span data-ttu-id="f2d97-208">Bijvoorbeeld, wanneer uw clientprogramma wordt gehost op een Windows-computer, kunt de Windows Firewall op de host u poort 1433 openen:</span><span class="sxs-lookup"><span data-stu-id="f2d97-208">For example, when your client program is hosted on a Windows computer, the Windows Firewall on the host enables you to open port 1433:</span></span>

1. <span data-ttu-id="f2d97-209">Open het Configuratiescherm</span><span class="sxs-lookup"><span data-stu-id="f2d97-209">Open the Control Panel</span></span>
2. <span data-ttu-id="f2d97-210">&gt;Alle Configuratiescherm-onderdelen</span><span class="sxs-lookup"><span data-stu-id="f2d97-210">&gt; All Control Panel Items</span></span>
3. <span data-ttu-id="f2d97-211">&gt;Windows Firewall</span><span class="sxs-lookup"><span data-stu-id="f2d97-211">&gt; Windows Firewall</span></span>
4. <span data-ttu-id="f2d97-212">&gt;Geavanceerde instellingen</span><span class="sxs-lookup"><span data-stu-id="f2d97-212">&gt; Advanced Settings</span></span>
5. <span data-ttu-id="f2d97-213">&gt;Regels voor uitgaande verbindingen</span><span class="sxs-lookup"><span data-stu-id="f2d97-213">&gt; Outbound Rules</span></span>
6. <span data-ttu-id="f2d97-214">&gt;Acties</span><span class="sxs-lookup"><span data-stu-id="f2d97-214">&gt; Actions</span></span>
7. <span data-ttu-id="f2d97-215">&gt;Nieuwe regel</span><span class="sxs-lookup"><span data-stu-id="f2d97-215">&gt; New Rule</span></span>

<span data-ttu-id="f2d97-216">Als wordt uw clientprogramma wordt gehost in Azure een virtuele machine (VM), dient u te lezen:</span><span class="sxs-lookup"><span data-stu-id="f2d97-216">If your client program is hosted on an Azure virtual machine (VM), you should read:</span></span><br/><span data-ttu-id="f2d97-217">[Poorten buiten 1433 voor ADO.NET 4.5 en SQL Database](sql-database-develop-direct-route-ports-adonet-v12.md).</span><span class="sxs-lookup"><span data-stu-id="f2d97-217">[Ports beyond 1433 for ADO.NET 4.5 and SQL Database](sql-database-develop-direct-route-ports-adonet-v12.md).</span></span>

<span data-ttu-id="f2d97-218">Zie voor achtergrondinformatie over cofiguration van poorten en IP-adres: [Azure SQL Database-firewall](sql-database-firewall-configure.md)</span><span class="sxs-lookup"><span data-stu-id="f2d97-218">For background information about cofiguration of ports and IP address, see: [Azure SQL Database firewall](sql-database-firewall-configure.md)</span></span>

<a id="d-connection-ado-net-4-5" name="d-connection-ado-net-4-5"></a>

### <a name="connection-adonet-461"></a><span data-ttu-id="f2d97-219">Verbinding: ADO.NET 4.6.1</span><span class="sxs-lookup"><span data-stu-id="f2d97-219">Connection: ADO.NET 4.6.1</span></span>
<span data-ttu-id="f2d97-220">Als het programma wordt gebruikt voor klassen als ADO.NET **System.Data.SqlClient.SqlConnection** voor verbinding met Azure SQL Database, het is raadzaam dat u .NET Framework versie 4.6.1 of hoger.</span><span class="sxs-lookup"><span data-stu-id="f2d97-220">If your program uses ADO.NET classes like **System.Data.SqlClient.SqlConnection** to connect to Azure SQL Database, we recommend that you use .NET Framework version 4.6.1 or higher.</span></span>

<span data-ttu-id="f2d97-221">ADO.NET 4.6.1:</span><span class="sxs-lookup"><span data-stu-id="f2d97-221">ADO.NET 4.6.1:</span></span>

* <span data-ttu-id="f2d97-222">Voor Azure SQL Database bestaat verbeterde betrouwbaarheid bij het openen van een verbinding via de **SqlConnection.Open** methode.</span><span class="sxs-lookup"><span data-stu-id="f2d97-222">For Azure SQL Database, there is improved reliability when you open a connection by using the **SqlConnection.Open** method.</span></span> <span data-ttu-id="f2d97-223">De **Open** methode bevat nu best effort opnieuw mechanismen in reactie op tijdelijke fouten voor bepaalde fouten binnen de time-out voor verbinding.</span><span class="sxs-lookup"><span data-stu-id="f2d97-223">The **Open** method now incorporates best effort retry mechanisms in response to transient faults, for certain errors within the Connection Timeout period.</span></span>
* <span data-ttu-id="f2d97-224">Ondersteunt Groepsgewijze verbinding nodig.</span><span class="sxs-lookup"><span data-stu-id="f2d97-224">Supports connection pooling.</span></span> <span data-ttu-id="f2d97-225">Dit omvat een doeltreffende controle het verbindingsobject die dit biedt uw programma werkt.</span><span class="sxs-lookup"><span data-stu-id="f2d97-225">This includes an efficient verification that the connection object it gives your program is functioning.</span></span>

<span data-ttu-id="f2d97-226">Wanneer u een verbindingsobject van een verbindingsgroep gebruikt, wordt u aangeraden dat uw programma tijdelijk de verbinding niet sluiten wanneer deze niet direct gebruikt.</span><span class="sxs-lookup"><span data-stu-id="f2d97-226">When you use a connection object from a connection pool, we recommend that your program temporarily close the connection when not immediately using it.</span></span> <span data-ttu-id="f2d97-227">Opnieuw een verbinding te openen is niet duur is van de manier waarop een nieuwe verbinding maken.</span><span class="sxs-lookup"><span data-stu-id="f2d97-227">Re-opening a connection is not expensive the way creating a new connection is.</span></span>

<span data-ttu-id="f2d97-228">Als u van ADO.NET 4.0 gebruikmaakt of eerder, we raden u een upgrade uitvoert naar de meest recente ADO.NET.</span><span class="sxs-lookup"><span data-stu-id="f2d97-228">If you are using ADO.NET 4.0 or earlier, we recommend that you upgrade to the latest ADO.NET.</span></span>

* <span data-ttu-id="f2d97-229">U kunt vanaf November 2015 [downloaden ADO.NET 4.6.1](http://blogs.msdn.com/b/dotnet/archive/2015/11/30/net-framework-4-6-1-is-now-available.aspx).</span><span class="sxs-lookup"><span data-stu-id="f2d97-229">As of November 2015, you can [download ADO.NET 4.6.1](http://blogs.msdn.com/b/dotnet/archive/2015/11/30/net-framework-4-6-1-is-now-available.aspx).</span></span>

<a id="e-diagnostics-test-utilities-connect" name="e-diagnostics-test-utilities-connect"></a>

## <a name="diagnostics"></a><span data-ttu-id="f2d97-230">Diagnostiek</span><span class="sxs-lookup"><span data-stu-id="f2d97-230">Diagnostics</span></span>
<a id="d-test-whether-utilities-can-connect" name="d-test-whether-utilities-can-connect"></a>

### <a name="diagnostics-test-whether-utilities-can-connect"></a><span data-ttu-id="f2d97-231">Diagnostische gegevens: Testen of hulpprogramma's verbinding kunnen maken</span><span class="sxs-lookup"><span data-stu-id="f2d97-231">Diagnostics: Test whether utilities can connect</span></span>
<span data-ttu-id="f2d97-232">Als het programma kan niet verbinden met Azure SQL Database, wordt een diagnostische mogelijkheid is om te proberen om te verbinden met een hulpprogramma's.</span><span class="sxs-lookup"><span data-stu-id="f2d97-232">If your program is failing to connect to Azure SQL Database, one diagnostic option is to try to connect with a utility program.</span></span> <span data-ttu-id="f2d97-233">In het ideale geval zou het hulpprogramma verbinding maken met behulp van dezelfde bibliotheek dat het programma gebruikt.</span><span class="sxs-lookup"><span data-stu-id="f2d97-233">Ideally the utility would connect by using the same library that your program uses.</span></span>

<span data-ttu-id="f2d97-234">Op elke Windows-computer probeert u deze hulpprogramma's:</span><span class="sxs-lookup"><span data-stu-id="f2d97-234">On any Windows computer, you can try these utilities:</span></span>

* <span data-ttu-id="f2d97-235">SQL Server Management Studio (ssms.exe) die is verbonden met ADO.NET.</span><span class="sxs-lookup"><span data-stu-id="f2d97-235">SQL Server Management Studio (ssms.exe), which connects by using ADO.NET.</span></span>
* <span data-ttu-id="f2d97-236">Sqlcmd.exe die verbinding met behulp van maakt [ODBC](http://msdn.microsoft.com/library/jj730308.aspx).</span><span class="sxs-lookup"><span data-stu-id="f2d97-236">sqlcmd.exe, which connects by using [ODBC](http://msdn.microsoft.com/library/jj730308.aspx).</span></span>

<span data-ttu-id="f2d97-237">Eenmaal zijn verbonden, test u of een korte SQL SELECT-query werkt.</span><span class="sxs-lookup"><span data-stu-id="f2d97-237">Once connected, test whether a short SQL SELECT query works.</span></span>

<a id="f-diagnostics-check-open-ports" name="f-diagnostics-check-open-ports"></a>

### <a name="diagnostics-check-the-open-ports"></a><span data-ttu-id="f2d97-238">Diagnostische gegevens: Controleer de geopende poorten</span><span class="sxs-lookup"><span data-stu-id="f2d97-238">Diagnostics: Check the open ports</span></span>
<span data-ttu-id="f2d97-239">Stel dat u vermoedt dat verbindingspogingen vanwege problemen met de poort mislukken.</span><span class="sxs-lookup"><span data-stu-id="f2d97-239">Suppose you suspect that connection attempts are failing due to port issues.</span></span> <span data-ttu-id="f2d97-240">U kunt een hulpprogramma waarmee u over de poortconfiguraties rapporten uitvoeren op uw computer.</span><span class="sxs-lookup"><span data-stu-id="f2d97-240">On your computer you can run a utility that reports on the port configurations.</span></span>

<span data-ttu-id="f2d97-241">Op Linux kunnen het handig zijn de volgende hulpprogramma's:</span><span class="sxs-lookup"><span data-stu-id="f2d97-241">On Linux the following utilities might be helpful:</span></span>

* `netstat -nap`
* `nmap -sS -O 127.0.0.1`
  * <span data-ttu-id="f2d97-242">(De Voorbeeldwaarde om uw IP-adres wijzigen).</span><span class="sxs-lookup"><span data-stu-id="f2d97-242">(Change the example value to be your IP address.)</span></span>

<span data-ttu-id="f2d97-243">In Windows de [PortQry.exe](http://www.microsoft.com/download/details.aspx?id=17148) hulpprogramma kan handig zijn.</span><span class="sxs-lookup"><span data-stu-id="f2d97-243">On Windows the [PortQry.exe](http://www.microsoft.com/download/details.aspx?id=17148) utility might be helpful.</span></span> <span data-ttu-id="f2d97-244">Hier volgt een voorbeeld van de uitvoering die de situatie poort op een Azure SQL Database-server een query uitgevoerd en die is uitgevoerd op een laptopcomputer:</span><span class="sxs-lookup"><span data-stu-id="f2d97-244">Here is an example execution that queried the port situation on an Azure SQL Database server, and which was run on a laptop computer:</span></span>

```
[C:\Users\johndoe\]
>> portqry.exe -n johndoesvr9.database.windows.net -p tcp -e 1433

Querying target system called:
 johndoesvr9.database.windows.net

Attempting to resolve name to IP address...
Name resolved to 23.100.117.95

querying...
TCP port 1433 (ms-sql-s service): LISTENING

[C:\Users\johndoe\]
>>
```


<a id="g-diagnostics-log-your-errors" name="g-diagnostics-log-your-errors"></a>

### <a name="diagnostics-log-your-errors"></a><span data-ttu-id="f2d97-245">Diagnostische gegevens: Uw fouten in logboek registreren</span><span class="sxs-lookup"><span data-stu-id="f2d97-245">Diagnostics: Log your errors</span></span>
<span data-ttu-id="f2d97-246">Er is een onregelmatig probleem wordt soms beste gediagnosticeerd door detectie van een algemene patroon gedurende dagen of weken.</span><span class="sxs-lookup"><span data-stu-id="f2d97-246">An intermittent problem is sometimes best diagnosed by detection of a general pattern over days or weeks.</span></span>

<span data-ttu-id="f2d97-247">De client kan helpen bij het een diagnose door logboekregistratie van alle fouten die worden aangetroffen.</span><span class="sxs-lookup"><span data-stu-id="f2d97-247">Your client can assist in a diagnosis by logging all errors it encounters.</span></span> <span data-ttu-id="f2d97-248">U kunt mogelijk de logboekvermeldingen correleren met foutgegevens met Azure SQL Database intern zichzelf registreert.</span><span class="sxs-lookup"><span data-stu-id="f2d97-248">You might be able to correlate the log entries with error data that Azure SQL Database logs itself internally.</span></span>

<span data-ttu-id="f2d97-249">Enterprise-bibliotheek 6 (EntLib60) biedt beheerde klassen om te helpen bij logboekregistratie:</span><span class="sxs-lookup"><span data-stu-id="f2d97-249">Enterprise Library 6 (EntLib60) offers .NET managed classes to assist with logging:</span></span>

* [<span data-ttu-id="f2d97-250">5 - zo eenvoudig als het een logboek vallen: met behulp van de logboekregistratie Application Block</span><span class="sxs-lookup"><span data-stu-id="f2d97-250">5 - As Easy As Falling Off a Log: Using the Logging Application Block</span></span>](http://msdn.microsoft.com/library/dn440731.aspx)

<a id="h-diagnostics-examine-logs-errors" name="h-diagnostics-examine-logs-errors"></a>

### <a name="diagnostics-examine-system-logs-for-errors"></a><span data-ttu-id="f2d97-251">Diagnostische gegevens: Raadpleeg het systeemlogboek in Logboeken op fouten</span><span class="sxs-lookup"><span data-stu-id="f2d97-251">Diagnostics: Examine system logs for errors</span></span>
<span data-ttu-id="f2d97-252">Hier volgen enkele Transact-SQL SELECT-instructies die querylogboeken van de fout en andere informatie.</span><span class="sxs-lookup"><span data-stu-id="f2d97-252">Here are some Transact-SQL SELECT statements that query logs of error and other information.</span></span>

| <span data-ttu-id="f2d97-253">Query van het logboek</span><span class="sxs-lookup"><span data-stu-id="f2d97-253">Query of log</span></span> | <span data-ttu-id="f2d97-254">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="f2d97-254">Description</span></span> |
|:--- |:--- |
| `SELECT e.*`<br/>`FROM sys.event_log AS e`<br/>`WHERE e.database_name = 'myDbName'`<br/>`AND e.event_category = 'connectivity'`<br/>`AND 2 >= DateDiff`<br/>&nbsp;&nbsp;`(hour, e.end_time, GetUtcDate())`<br/>`ORDER BY e.event_category,`<br/>&nbsp;&nbsp;`e.event_type, e.end_time;` |<span data-ttu-id="f2d97-255">De [sys.event_log](http://msdn.microsoft.com/library/dn270018.aspx) weergave biedt informatie over afzonderlijke gebeurtenissen, inclusief een aantal die leiden tijdelijke fouten of verbindingsproblemen tot kunnen.</span><span class="sxs-lookup"><span data-stu-id="f2d97-255">The [sys.event_log](http://msdn.microsoft.com/library/dn270018.aspx) view offers information about individual events, including some that can cause transient errors or connectivity failures.</span></span><br/><br/><span data-ttu-id="f2d97-256">U kunt in het ideale geval correleren de **start_time** of **end_time** waarden met informatie over wanneer uw clientprogramma problemen ondervonden.</span><span class="sxs-lookup"><span data-stu-id="f2d97-256">Ideally you can correlate the **start_time** or **end_time** values with information about when your client program experienced problems.</span></span><br/><br/><span data-ttu-id="f2d97-257">**TIP:** u moet verbinding maken met de **master** database uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="f2d97-257">**TIP:** You must connect to the **master** database to run this.</span></span> |
| `SELECT c.*`<br/>`FROM sys.database_connection_stats AS c`<br/>`WHERE c.database_name = 'myDbName'`<br/>`AND 24 >= DateDiff`<br/>&nbsp;&nbsp;`(hour, c.end_time, GetUtcDate())`<br/>`ORDER BY c.end_time;` |<span data-ttu-id="f2d97-258">De [sys.database_connection_stats](http://msdn.microsoft.com/library/dn269986.aspx) weergave biedt cumulatief aantal gebeurtenistypen, voor aanvullende diagnostische gegevens.</span><span class="sxs-lookup"><span data-stu-id="f2d97-258">The [sys.database_connection_stats](http://msdn.microsoft.com/library/dn269986.aspx) view offers aggregated counts of event types, for additional diagnostics.</span></span><br/><br/><span data-ttu-id="f2d97-259">**TIP:** u moet verbinding maken met de **master** database uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="f2d97-259">**TIP:** You must connect to the **master** database to run this.</span></span> |

<a id="d-search-for-problem-events-in-the-sql-database-log" name="d-search-for-problem-events-in-the-sql-database-log"></a>

### <a name="diagnostics-search-for-problem-events-in-the-sql-database-log"></a><span data-ttu-id="f2d97-260">Diagnostische gegevens: Zoek naar gebeurtenissen probleem in de SQL-Database</span><span class="sxs-lookup"><span data-stu-id="f2d97-260">Diagnostics: Search for problem events in the SQL Database log</span></span>
<span data-ttu-id="f2d97-261">U kunt zoeken naar vermeldingen over probleem gebeurtenissen in het logboek van Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="f2d97-261">You can search for entries about problem events in the log of Azure SQL Database.</span></span> <span data-ttu-id="f2d97-262">Probeer de volgende Transact-SQL SELECT-instructie in de **master** database:</span><span class="sxs-lookup"><span data-stu-id="f2d97-262">Try the following Transact-SQL SELECT statement in the **master** database:</span></span>

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


#### <a name="a-few-returned-rows-from-sysfnxetelemetryblobtargetreadfile"></a><span data-ttu-id="f2d97-263">Enkele geretourneerde rijen uit sys.fn_xe_telemetry_blob_target_read_file</span><span class="sxs-lookup"><span data-stu-id="f2d97-263">A few returned rows from sys.fn_xe_telemetry_blob_target_read_file</span></span>
<span data-ttu-id="f2d97-264">Hierna volgt wat een geretourneerde rij als volgt uitzien.</span><span class="sxs-lookup"><span data-stu-id="f2d97-264">Next is what a returned row might look like.</span></span> <span data-ttu-id="f2d97-265">De null-waarden weergegeven zijn vaak niet null zijn in andere rijen.</span><span class="sxs-lookup"><span data-stu-id="f2d97-265">The null values shown are often not null in other rows.</span></span>

```
object_name                   timestamp                    error  state  is_success  database_name

database_xml_deadlock_report  2015-10-16 20:28:01.0090000  NULL   NULL   NULL        AdventureWorks
```


<a id="l-enterprise-library-6" name="l-enterprise-library-6"></a>

## <a name="enterprise-library-6"></a><span data-ttu-id="f2d97-266">Enterprise-bibliotheek 6</span><span class="sxs-lookup"><span data-stu-id="f2d97-266">Enterprise Library 6</span></span>
<span data-ttu-id="f2d97-267">Enterprise-bibliotheek 6 (EntLib60) is een raamwerk van .NET-klassen waarmee u het implementeren van krachtige clients van cloud-services, waarbij een van de Azure SQL Database-service is.</span><span class="sxs-lookup"><span data-stu-id="f2d97-267">Enterprise Library 6 (EntLib60) is a framework of .NET classes that helps you implement robust clients of cloud services, one of which is the Azure SQL Database service.</span></span> <span data-ttu-id="f2d97-268">U kunt de onderwerpen die zijn toegewezen aan elk gebied waarin EntLib60 kan helpen in eerste via vinden:</span><span class="sxs-lookup"><span data-stu-id="f2d97-268">You can locate topics dedicated to each area in which EntLib60 can assist by first visiting:</span></span>

* [<span data-ttu-id="f2d97-269">Enterprise-bibliotheek 6 April 2013</span><span class="sxs-lookup"><span data-stu-id="f2d97-269">Enterprise Library 6 - April 2013</span></span>](http://msdn.microsoft.com/library/dn169621%28v=pandp.60%29.aspx)

<span data-ttu-id="f2d97-270">Pogingslogica voor tijdelijke foutafhandeling is een gebied waarin EntLib60 kan helpen:</span><span class="sxs-lookup"><span data-stu-id="f2d97-270">Retry logic for handling transient errors is one area in which EntLib60 can assist:</span></span>

* [<span data-ttu-id="f2d97-271">4 - perseverance, geheim van alle successen: met behulp van de blokkering van de toepassing afhandeling van tijdelijke fout</span><span class="sxs-lookup"><span data-stu-id="f2d97-271">4 - Perseverance, Secret of All Triumphs: Using the Transient Fault Handling Application Block</span></span>](http://msdn.microsoft.com/library/dn440719%28v=pandp.60%29.aspx)

> [!NOTE]
> <span data-ttu-id="f2d97-272">De broncode voor EntLib60 is beschikbaar voor openbare [downloaden](http://go.microsoft.com/fwlink/p/?LinkID=290898).</span><span class="sxs-lookup"><span data-stu-id="f2d97-272">The source code for EntLib60 is available for public [download](http://go.microsoft.com/fwlink/p/?LinkID=290898).</span></span> <span data-ttu-id="f2d97-273">Microsoft heeft geen plannen verdere functie-updates en onderhoud om aan te brengen EntLib.</span><span class="sxs-lookup"><span data-stu-id="f2d97-273">Microsoft has no plans to make further feature updates or maintenance updates to EntLib.</span></span>
> 
> 

<a id="entlib60-classes-for-transient-errors-and-retry" name="entlib60-classes-for-transient-errors-and-retry"></a>

### <a name="entlib60-classes-for-transient-errors-and-retry"></a><span data-ttu-id="f2d97-274">EntLib60 klassen voor tijdelijke fouten en probeer het opnieuw</span><span class="sxs-lookup"><span data-stu-id="f2d97-274">EntLib60 classes for transient errors and retry</span></span>
<span data-ttu-id="f2d97-275">De volgende EntLib60 klassen zijn bijzonder nuttig voor Pogingslogica.</span><span class="sxs-lookup"><span data-stu-id="f2d97-275">The following EntLib60 classes are particularly useful for retry logic.</span></span> <span data-ttu-id="f2d97-276">Al deze, of worden verdere onder de naamruimte **Microsoft.Practices.EnterpriseLibrary.TransientFaultHandling**:</span><span class="sxs-lookup"><span data-stu-id="f2d97-276">All these  are in, or are further under, the namespace **Microsoft.Practices.EnterpriseLibrary.TransientFaultHandling**:</span></span>

<span data-ttu-id="f2d97-277">*In de naamruimte **Microsoft.Practices.EnterpriseLibrary.TransientFaultHandling**:*</span><span class="sxs-lookup"><span data-stu-id="f2d97-277">*In the namespace **Microsoft.Practices.EnterpriseLibrary.TransientFaultHandling**:*</span></span>

* <span data-ttu-id="f2d97-278">**Het RetryPolicy** klasse</span><span class="sxs-lookup"><span data-stu-id="f2d97-278">**RetryPolicy** class</span></span>
  
  * <span data-ttu-id="f2d97-279">**ExecuteAction** methode</span><span class="sxs-lookup"><span data-stu-id="f2d97-279">**ExecuteAction** method</span></span>
* <span data-ttu-id="f2d97-280">**ExponentialBackoff** klasse</span><span class="sxs-lookup"><span data-stu-id="f2d97-280">**ExponentialBackoff** class</span></span>
* <span data-ttu-id="f2d97-281">**SqlDatabaseTransientErrorDetectionStrategy** klasse</span><span class="sxs-lookup"><span data-stu-id="f2d97-281">**SqlDatabaseTransientErrorDetectionStrategy** class</span></span>
* <span data-ttu-id="f2d97-282">**ReliableSqlConnection** klasse</span><span class="sxs-lookup"><span data-stu-id="f2d97-282">**ReliableSqlConnection** class</span></span>
  
  * <span data-ttu-id="f2d97-283">**ExecuteCommand** methode</span><span class="sxs-lookup"><span data-stu-id="f2d97-283">**ExecuteCommand** method</span></span>

<span data-ttu-id="f2d97-284">In de naamruimte **Microsoft.Practices.EnterpriseLibrary.TransientFaultHandling.TestSupport**:</span><span class="sxs-lookup"><span data-stu-id="f2d97-284">In the namespace **Microsoft.Practices.EnterpriseLibrary.TransientFaultHandling.TestSupport**:</span></span>

* <span data-ttu-id="f2d97-285">**AlwaysTransientErrorDetectionStrategy** klasse</span><span class="sxs-lookup"><span data-stu-id="f2d97-285">**AlwaysTransientErrorDetectionStrategy** class</span></span>
* <span data-ttu-id="f2d97-286">**NeverTransientErrorDetectionStrategy** klasse</span><span class="sxs-lookup"><span data-stu-id="f2d97-286">**NeverTransientErrorDetectionStrategy** class</span></span>

<span data-ttu-id="f2d97-287">Hier vindt u koppelingen naar informatie over EntLib60:</span><span class="sxs-lookup"><span data-stu-id="f2d97-287">Here are links to information about EntLib60:</span></span>

* <span data-ttu-id="f2d97-288">Gratis [downloaden van het adresboek: Ontwikkelaarshandleiding voor Microsoft Enterprise-bibliotheek, 2e Edition](http://www.microsoft.com/download/details.aspx?id=41145)</span><span class="sxs-lookup"><span data-stu-id="f2d97-288">Free [Book Download: Developer's Guide to Microsoft Enterprise Library, 2nd Edition](http://www.microsoft.com/download/details.aspx?id=41145)</span></span>
* <span data-ttu-id="f2d97-289">Aanbevolen procedures: [Probeer algemene richtlijnen](../best-practices-retry-general.md) is een uitstekende gedetailleerdere beschrijving van Pogingslogica.</span><span class="sxs-lookup"><span data-stu-id="f2d97-289">Best practices: [Retry general guidance](../best-practices-retry-general.md) has an excellent in-depth discussion of retry logic.</span></span>
* <span data-ttu-id="f2d97-290">Downloaden van NuGet [Enterprise Library - toepassing blok 6.0 afhandeling van tijdelijke fout](http://www.nuget.org/packages/EnterpriseLibrary.TransientFaultHandling/)</span><span class="sxs-lookup"><span data-stu-id="f2d97-290">NuGet download of [Enterprise Library - Transient Fault Handling application block 6.0](http://www.nuget.org/packages/EnterpriseLibrary.TransientFaultHandling/)</span></span>

<a id="entlib60-the-logging-block" name="entlib60-the-logging-block"></a>

### <a name="entlib60-the-logging-block"></a><span data-ttu-id="f2d97-291">EntLib60: De logboekregistratie blokkeren</span><span class="sxs-lookup"><span data-stu-id="f2d97-291">EntLib60: The logging block</span></span>
* <span data-ttu-id="f2d97-292">De logboekregistratie voor scriptblokkering is een zeer flexibele en configureerbare oplossing waarmee u kunt:</span><span class="sxs-lookup"><span data-stu-id="f2d97-292">The Logging block is a highly flexible and configurable solution that allows you to:</span></span>
  
  * <span data-ttu-id="f2d97-293">Maak en logboekberichten opslaan in een groot aantal verschillende locaties.</span><span class="sxs-lookup"><span data-stu-id="f2d97-293">Create and store log messages in a wide variety of locations.</span></span>
  * <span data-ttu-id="f2d97-294">Categoriseren en berichten filteren.</span><span class="sxs-lookup"><span data-stu-id="f2d97-294">Categorize and filter messages.</span></span>
  * <span data-ttu-id="f2d97-295">Contextuele informatie verzameld die handig voor foutopsporing en tracering, evenals voor controle en algemene logboekregistratie vereisten.</span><span class="sxs-lookup"><span data-stu-id="f2d97-295">Collect contextual information that is useful for debugging and tracing, as well as for auditing and general logging requirements.</span></span>
* <span data-ttu-id="f2d97-296">Het blok logboekregistratie isoleert de logboekregistratie van de doel-logboek zodat de toepassingscode consistent, ongeacht de locatie en het type van het archief van de doel-logboekregistratie is.</span><span class="sxs-lookup"><span data-stu-id="f2d97-296">The Logging block abstracts the logging functionality from the log destination so that the application code is consistent, irrespective of the location and type of the target logging store.</span></span>

<span data-ttu-id="f2d97-297">Zie voor meer informatie: [5 - als gemakkelijk als vallen buiten een logboek: met behulp van de Logging Application Block](https://msdn.microsoft.com/library/dn440731%28v=pandp.60%29.aspx)</span><span class="sxs-lookup"><span data-stu-id="f2d97-297">For details see: [5 - As Easy As Falling Off a Log: Using the Logging Application Block](https://msdn.microsoft.com/library/dn440731%28v=pandp.60%29.aspx)</span></span>

<a id="entlib60-istransient-method-source-code" name="entlib60-istransient-method-source-code"></a>

### <a name="entlib60-istransient-method-source-code"></a><span data-ttu-id="f2d97-298">EntLib60 IsTransient methode broncode</span><span class="sxs-lookup"><span data-stu-id="f2d97-298">EntLib60 IsTransient method source code</span></span>
<span data-ttu-id="f2d97-299">Vervolgens uit de **SqlDatabaseTransientErrorDetectionStrategy** klasse, is de C#-broncode voor de **IsTransient** methode.</span><span class="sxs-lookup"><span data-stu-id="f2d97-299">Next, from the **SqlDatabaseTransientErrorDetectionStrategy** class, is the C# source code for the **IsTransient** method.</span></span> <span data-ttu-id="f2d97-300">De broncode wordt uitleg gegeven over welke fouten zijn aangemerkt als een tijdelijke en leveringsopties opnieuw vanaf April 2013.</span><span class="sxs-lookup"><span data-stu-id="f2d97-300">The source code clarifies which errors were considered to be transient and worthy of retry, as of April 2013.</span></span>

<span data-ttu-id="f2d97-301">Talrijke **//comment** regels zijn verwijderd uit deze kopie benadrukken leesbaarheid.</span><span class="sxs-lookup"><span data-stu-id="f2d97-301">Numerous **//comment** lines have been removed from this copy to emphasize readability.</span></span>

```
public bool IsTransient(Exception ex)
{
  if (ex != null)
  {
    SqlException sqlException;
    if ((sqlException = ex as SqlException) != null)
    {
      // Enumerate through all errors found in the exception.
      foreach (SqlError err in sqlException.Errors)
      {
        switch (err.Number)
        {
            // SQL Error Code: 40501
            // The service is currently busy. Retry the request after 10 seconds.
            // Code: (reason code to be decoded).
          case ThrottlingCondition.ThrottlingErrorNumber:
            // Decode the reason code from the error message to
            // determine the grounds for throttling.
            var condition = ThrottlingCondition.FromError(err);

            // Attach the decoded values as additional attributes to
            // the original SQL exception.
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
            // The instance of SQL Server you attempted to connect to
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


## <a name="next-steps"></a><span data-ttu-id="f2d97-302">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="f2d97-302">Next steps</span></span>
* <span data-ttu-id="f2d97-303">Voor het oplossen van andere veelvoorkomende verbindingsproblemen van Azure SQL Database, gaat u naar [verbindingsproblemen met Azure SQL Database oplossen](sql-database-troubleshoot-common-connection-issues.md).</span><span class="sxs-lookup"><span data-stu-id="f2d97-303">For troubleshooting other common Azure SQL Database connection issues, visit [Troubleshoot connection issues to Azure SQL Database](sql-database-troubleshoot-common-connection-issues.md).</span></span>
* [<span data-ttu-id="f2d97-304">SQL Server-verbinding (ADO.NET) groeperen</span><span class="sxs-lookup"><span data-stu-id="f2d97-304">SQL Server Connection Pooling (ADO.NET)</span></span>](http://msdn.microsoft.com/library/8xx3tyca.aspx)
* [<span data-ttu-id="f2d97-305">*Opnieuw proberen* is een Apache 2.0 in licentie gegeven algemene bibliotheek, geschreven in opnieuw **Python**, voor het vereenvoudigen van de taak van het gedrag voor het opnieuw op vrijwel elk element toevoegen.</span><span class="sxs-lookup"><span data-stu-id="f2d97-305">*Retrying* is an Apache 2.0 licensed general-purpose retrying library, written in **Python**, to simplify the task of adding retry behavior to just about anything.</span></span>](https://pypi.python.org/pypi/retrying)


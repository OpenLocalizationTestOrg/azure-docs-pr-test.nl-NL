---
title: 'Stream Analytics: Aanmelden referenties voor de invoer en uitvoer draaien | Microsoft Docs'
description: Informatie over het bijwerken van de referenties voor Stream Analytics-invoer en uitvoer.
keywords: aanmeldingsreferenties
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 42ae83e1-cd33-49bb-a455-a39a7c151ea4
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 2cb995a3969a8cb025f371ed0ab160cd04b0454d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="rotate-login-credentials-for-inputs-and-outputs-in-stream-analytics-jobs"></a><span data-ttu-id="71011-104">Draaien aanmeldingsreferenties voor in- en uitgangen in Stream Analytics-taken</span><span class="sxs-lookup"><span data-stu-id="71011-104">Rotate login credentials for inputs and outputs in Stream Analytics Jobs</span></span>
## <a name="abstract"></a><span data-ttu-id="71011-105">Abstracte</span><span class="sxs-lookup"><span data-stu-id="71011-105">Abstract</span></span>
<span data-ttu-id="71011-106">Azure Stream Analytics toegestaan vandaag nog niet in de referenties op een i/o vervangen terwijl de taak wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="71011-106">Azure Stream Analytics today doesn’t allow replacing the credentials on an input/output while the job is running.</span></span>

<span data-ttu-id="71011-107">Terwijl Azure Stream Analytics biedt ondersteuning voor het hervatten van een taak van laatste uitvoer, die we wilden delen van het gehele proces voor het minimaliseren van de vertraging tussen het stoppen en starten van de taak en roteren van de aanmeldingsreferenties.</span><span class="sxs-lookup"><span data-stu-id="71011-107">While Azure Stream Analytics does support resuming a job from last output, we wanted to share the entire process for minimizing the lag between the stopping and starting of the job and rotating the login credentials.</span></span>

## <a name="part-1---prepare-the-new-set-of-credentials"></a><span data-ttu-id="71011-108">Deel 1: voorbereiden van de nieuwe set referenties:</span><span class="sxs-lookup"><span data-stu-id="71011-108">Part 1 - Prepare the new set of credentials:</span></span>
<span data-ttu-id="71011-109">Dit onderdeel is van toepassing op de volgende invoer/uitvoer:</span><span class="sxs-lookup"><span data-stu-id="71011-109">This part is applicable to the following inputs/outputs:</span></span>

* <span data-ttu-id="71011-110">Blob Storage</span><span class="sxs-lookup"><span data-stu-id="71011-110">Blob Storage</span></span>
* <span data-ttu-id="71011-111">Event Hubs</span><span class="sxs-lookup"><span data-stu-id="71011-111">Event Hubs</span></span>
* <span data-ttu-id="71011-112">SQL Database</span><span class="sxs-lookup"><span data-stu-id="71011-112">SQL Database</span></span>
* <span data-ttu-id="71011-113">Table Storage</span><span class="sxs-lookup"><span data-stu-id="71011-113">Table Storage</span></span>

<span data-ttu-id="71011-114">Voor andere invoer/uitvoer, gaat u verder met deel 2.</span><span class="sxs-lookup"><span data-stu-id="71011-114">For other inputs/outputs, proceed with Part 2.</span></span>

### <a name="blob-storagetable-storage"></a><span data-ttu-id="71011-115">BLOB storage-/ tabelnaam-opslag</span><span class="sxs-lookup"><span data-stu-id="71011-115">Blob storage/Table storage</span></span>
1. <span data-ttu-id="71011-116">Ga naar de extensie van de opslag op de Azure Management portal:</span><span class="sxs-lookup"><span data-stu-id="71011-116">Go to the Storage extention on the Azure Management portal:</span></span>  
   ![graphic1][graphic1]
2. <span data-ttu-id="71011-118">Zoek naar de opslag die wordt gebruikt door de taak en gaat u in de App:</span><span class="sxs-lookup"><span data-stu-id="71011-118">Locate the storage used by your job and go into it:</span></span>  
   ![graphic2][graphic2]
3. <span data-ttu-id="71011-120">Klik op de opdracht toegangssleutels beheren:</span><span class="sxs-lookup"><span data-stu-id="71011-120">Click the Manage Access Keys command:</span></span>  
   ![graphic3][graphic3]
4. <span data-ttu-id="71011-122">Tussen de primaire toegangssleutel en de secundaire toegangssleutel **kiest u het niet wordt gebruikt door uw taak**.</span><span class="sxs-lookup"><span data-stu-id="71011-122">Between the Primary Access Key and the Secondary Access Key, **pick the one not used by your job**.</span></span>
5. <span data-ttu-id="71011-123">Klik op opnieuw genereren:</span><span class="sxs-lookup"><span data-stu-id="71011-123">Hit regenerate:</span></span>  
   ![graphic4][graphic4]
6. <span data-ttu-id="71011-125">Kopieer het zojuist gegenereerde sleutel:</span><span class="sxs-lookup"><span data-stu-id="71011-125">Copy the newly generated key:</span></span>  
   ![graphic5][graphic5]
7. <span data-ttu-id="71011-127">Deel 2 blijven.</span><span class="sxs-lookup"><span data-stu-id="71011-127">Continue to Part 2.</span></span>

### <a name="event-hubs"></a><span data-ttu-id="71011-128">Event hubs</span><span class="sxs-lookup"><span data-stu-id="71011-128">Event hubs</span></span>
1. <span data-ttu-id="71011-129">Ga naar de Service Bus-uitbreiding op de Azure Management portal:</span><span class="sxs-lookup"><span data-stu-id="71011-129">Go to the Service Bus extension on the Azure Management portal:</span></span>  
   ![graphic6][graphic6]
2. <span data-ttu-id="71011-131">Zoek naar de Service Bus-Namespace gebruikt door de taak en gaat u in de App:</span><span class="sxs-lookup"><span data-stu-id="71011-131">Locate the Service Bus Namespace used by your job and go into it:</span></span>  
   ![graphic7][graphic7]
3. <span data-ttu-id="71011-133">Als uw taak gebruikmaakt van een gedeeld toegangsbeleid op de Service Bus-Namespace, Ga naar stap 6</span><span class="sxs-lookup"><span data-stu-id="71011-133">If your job uses a shared access policy on the Service Bus Namespace, jump to step 6</span></span>  
4. <span data-ttu-id="71011-134">Ga naar het tabblad Event Hubs:</span><span class="sxs-lookup"><span data-stu-id="71011-134">Go to the Event Hubs tab:</span></span>  
   ![graphic8][graphic8]
5. <span data-ttu-id="71011-136">Zoek naar de Event Hub gebruikt door de taak en gaat u in de App:</span><span class="sxs-lookup"><span data-stu-id="71011-136">Locate the Event Hub used by your job and go into it:</span></span>  
   ![graphic9][graphic9]
6. <span data-ttu-id="71011-138">Ga naar het tabblad configureren:</span><span class="sxs-lookup"><span data-stu-id="71011-138">Go to the Configure Tab:</span></span>  
   ![graphic10][graphic10]
7. <span data-ttu-id="71011-140">Zoek het beleid voor gedeelde toegang gebruikt door de taak op de vervolgkeuzelijst de naam van beleid:</span><span class="sxs-lookup"><span data-stu-id="71011-140">On the Policy Name drop-down, locate the shared access policy used by your job:</span></span>  
   ![graphic11][graphic11]
8. <span data-ttu-id="71011-142">Tussen de primaire sleutel en de secundaire sleutel **kiest u het niet wordt gebruikt door uw taak**.</span><span class="sxs-lookup"><span data-stu-id="71011-142">Between the Primary Key and the Secondary Key, **pick the one not used by your job**.</span></span>  
9. <span data-ttu-id="71011-143">Klik op opnieuw genereren:</span><span class="sxs-lookup"><span data-stu-id="71011-143">Hit regenerate:</span></span>  
   ![graphic12][graphic12]
10. <span data-ttu-id="71011-145">Kopieer het zojuist gegenereerde sleutel:</span><span class="sxs-lookup"><span data-stu-id="71011-145">Copy the newly generated key:</span></span>  
   ![graphic13][graphic13]
11. <span data-ttu-id="71011-147">Deel 2 blijven.</span><span class="sxs-lookup"><span data-stu-id="71011-147">Continue to Part 2.</span></span>  

### <a name="sql-database"></a><span data-ttu-id="71011-148">SQL Database</span><span class="sxs-lookup"><span data-stu-id="71011-148">SQL Database</span></span>
> [!NOTE]
> <span data-ttu-id="71011-149">Opmerking: u moet verbinding maken met de SQL Database-Service.</span><span class="sxs-lookup"><span data-stu-id="71011-149">Note: you will need to connect to the SQL Database Service.</span></span> <span data-ttu-id="71011-150">We gaan laten zien hoe u dit doen met behulp van de beheerervaring op de Azure Management portal, maar u kunt sommige clientzijde hulpprogramma ook zoals SQL Server Management Studio te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="71011-150">We are going to show how to do this using the management experience on the Azure Management portal but you may choose to use some client-side tool such as SQL Server Management Studio as well.</span></span>
>
> 

1. <span data-ttu-id="71011-151">Ga naar de extensie van de SQL-Databases op de Azure Management portal:</span><span class="sxs-lookup"><span data-stu-id="71011-151">Go to the SQL Databases extension on the Azure Management portal:</span></span>  
   ![graphic14][graphic14]
2. <span data-ttu-id="71011-153">Zoek de SQL-Database die wordt gebruikt door uw werk en **Klik op de server** koppeling op dezelfde regel:</span><span class="sxs-lookup"><span data-stu-id="71011-153">Locate the SQL Database used by your job and **click on the server** link on the same line:</span></span>  
   <span data-ttu-id="71011-154">![graphic15][graphic15]</span><span class="sxs-lookup"><span data-stu-id="71011-154">![graphic15][graphic15]</span></span>
3. <span data-ttu-id="71011-155">Klik op de opdracht beheren:</span><span class="sxs-lookup"><span data-stu-id="71011-155">Click the Manage command:</span></span>  
   ![graphic16][graphic16]
4. <span data-ttu-id="71011-157">Type Database Master:</span><span class="sxs-lookup"><span data-stu-id="71011-157">Type Database Master:</span></span>  
   ![graphic17][graphic17]
5. <span data-ttu-id="71011-159">Typ uw gebruikersnaam, wachtwoord, en klik op logboek op:</span><span class="sxs-lookup"><span data-stu-id="71011-159">Type in your User Name, Password, and click Log on:</span></span>  
   ![graphic18][graphic18]
6. <span data-ttu-id="71011-161">Klik op nieuwe Query:</span><span class="sxs-lookup"><span data-stu-id="71011-161">Click New Query:</span></span>  
   ![graphic19][graphic19]
7. <span data-ttu-id="71011-163">Type in de volgende query waarbij < login_name > vervangt door uw gebruikersnaam en vervangen <enterStrongPasswordHere> met uw nieuwe wachtwoord:</span><span class="sxs-lookup"><span data-stu-id="71011-163">Type in the following query replacing <login_name> with your User Name and replacing <enterStrongPasswordHere> with your new password:</span></span>  
   `CREATE LOGIN <login_name> WITH PASSWORD = '<enterStrongPasswordHere>'`
8. <span data-ttu-id="71011-164">Klik op uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="71011-164">Click Run:</span></span>  
   ![graphic20][graphic20]
9. <span data-ttu-id="71011-166">Ga terug naar stap 2 en deze keer klikt u op de database:</span><span class="sxs-lookup"><span data-stu-id="71011-166">Go back to step 2 and this time click the database:</span></span>  
   ![graphic21][graphic21]
10. <span data-ttu-id="71011-168">Klik op de opdracht beheren:</span><span class="sxs-lookup"><span data-stu-id="71011-168">Click the Manage command:</span></span>  
   ![graphic22][graphic22]
11. <span data-ttu-id="71011-170">Typ uw gebruikersnaam, wachtwoord, en klik op aanmelden:</span><span class="sxs-lookup"><span data-stu-id="71011-170">type in your User Name, Password, and click Logon:</span></span>  
   ![graphic23][graphic23]
12. <span data-ttu-id="71011-172">Klik op nieuwe Query:</span><span class="sxs-lookup"><span data-stu-id="71011-172">Click New Query:</span></span>  
   ![graphic24][graphic24]
13. <span data-ttu-id="71011-174">Typ in de volgende query waarbij < gebruikersnaam > vervangt door een naam waarmee u deze aanmelding in de context van deze database wilt (u kunt u < login_name > bijvoorbeeld heeft dezelfde waarde opgeven) te identificeren en vervangen < login_name > met uw nieuwe gebruikersnaam:</span><span class="sxs-lookup"><span data-stu-id="71011-174">Type in the following query replacing <user_name> with a name by which you want to identify this login in the context of this database (you can provide the same value you gave for <login_name>, for example) and replacing <login_name> with your new user name:</span></span>  
   `CREATE USER <user_name> FROM LOGIN <login_name>`
14. <span data-ttu-id="71011-175">Klik op uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="71011-175">Click Run:</span></span>  
   ![graphic25][graphic25]
15. <span data-ttu-id="71011-177">Bieden nu de nieuwe gebruiker met dezelfde functies en de oorspronkelijke gebruiker heeft bevoegdheden.</span><span class="sxs-lookup"><span data-stu-id="71011-177">You should now provide your new user with the same roles and privileges your original user had.</span></span>
16. <span data-ttu-id="71011-178">Deel 2 blijven.</span><span class="sxs-lookup"><span data-stu-id="71011-178">Continue to Part 2.</span></span>

## <a name="part-2-stopping-the-stream-analytics-job"></a><span data-ttu-id="71011-179">Deel 2: De Stream Analytics-taak stoppen</span><span class="sxs-lookup"><span data-stu-id="71011-179">Part 2: Stopping the Stream Analytics Job</span></span>
1. <span data-ttu-id="71011-180">Ga naar de Stream Analytics-uitbreiding op de Azure Management portal:</span><span class="sxs-lookup"><span data-stu-id="71011-180">Go to the Stream Analytics extension on the Azure Management portal:</span></span>  
   ![graphic26][graphic26]
2. <span data-ttu-id="71011-182">Zoek uw taak en gaat u in de App:</span><span class="sxs-lookup"><span data-stu-id="71011-182">Locate your job and go into it:</span></span>  
   ![graphic27][graphic27]
3. <span data-ttu-id="71011-184">Ga naar het tabblad invoer of de uitvoer op basis van of het roteren van de referenties op invoer of uitvoer.</span><span class="sxs-lookup"><span data-stu-id="71011-184">Go to the Inputs tab or the Outputs tab based on whether you are rotating the credentials on an Input or on an Output.</span></span>  
   ![graphic28][graphic28]
4. <span data-ttu-id="71011-186">Klik op de opdracht Stop en Bevestig dat de taak is gestopt:</span><span class="sxs-lookup"><span data-stu-id="71011-186">Click the Stop command and confirm the job has stopped:</span></span>  
   <span data-ttu-id="71011-187">![graphic29][graphic29] wacht u totdat de taak te stoppen.</span><span class="sxs-lookup"><span data-stu-id="71011-187">![graphic29][graphic29] Wait for the job to stop.</span></span>
5. <span data-ttu-id="71011-188">Zoek de invoer/uitvoer die u wilt draaien referenties op en gaat u in de App:</span><span class="sxs-lookup"><span data-stu-id="71011-188">Locate the input/output you want to rotate credentials on and go into it:</span></span>  
   ![graphic30][graphic30]
6. <span data-ttu-id="71011-190">Ga naar deel 3.</span><span class="sxs-lookup"><span data-stu-id="71011-190">Proceed to Part 3.</span></span>

## <a name="part-3-editing-the-credentials-on-the-stream-analytics-job"></a><span data-ttu-id="71011-191">Deel 3: De referenties op de Stream Analytics-taak bewerken</span><span class="sxs-lookup"><span data-stu-id="71011-191">Part 3: Editing the credentials on the Stream Analytics Job</span></span>
### <a name="blob-storagetable-storage"></a><span data-ttu-id="71011-192">BLOB storage-/ tabelnaam-opslag</span><span class="sxs-lookup"><span data-stu-id="71011-192">Blob storage/Table storage</span></span>
1. <span data-ttu-id="71011-193">Zoek het sleutelveld van Storage-Account en uw zojuist gegenereerde sleutel plakken:</span><span class="sxs-lookup"><span data-stu-id="71011-193">Find the Storage Account Key field and paste your newly generated key into it:</span></span>  
   ![graphic31][graphic31]
2. <span data-ttu-id="71011-195">Klik op de opdracht opslaan en Bevestig de wijzigingen worden opgeslagen:</span><span class="sxs-lookup"><span data-stu-id="71011-195">Click the Save command and confirm saving your changes:</span></span>  
   ![graphic32][graphic32]
3. <span data-ttu-id="71011-197">Een verbindingstest wordt automatisch gestart wanneer u de wijzigingen opslaan, zorg ervoor dat geslaagd is.</span><span class="sxs-lookup"><span data-stu-id="71011-197">A connection test will automatically start when you save your changes, make sure that is has successfully passed.</span></span>
4. <span data-ttu-id="71011-198">Ga naar deel 4.</span><span class="sxs-lookup"><span data-stu-id="71011-198">Proceed to Part 4.</span></span>

### <a name="event-hubs"></a><span data-ttu-id="71011-199">Event hubs</span><span class="sxs-lookup"><span data-stu-id="71011-199">Event hubs</span></span>
1. <span data-ttu-id="71011-200">Zoek het sleutelveld Event Hub-beleid en uw zojuist gegenereerde sleutel plakken:</span><span class="sxs-lookup"><span data-stu-id="71011-200">Find the Event Hub Policy Key field and paste your newly generated key into it:</span></span>  
   ![graphic33][graphic33]
2. <span data-ttu-id="71011-202">Klik op de opdracht opslaan en Bevestig de wijzigingen worden opgeslagen:</span><span class="sxs-lookup"><span data-stu-id="71011-202">Click the Save command and confirm saving your changes:</span></span>  
   ![graphic34][graphic34]
3. <span data-ttu-id="71011-204">Een verbindingstest wordt automatisch gestart wanneer u de wijzigingen opslaan, zorg ervoor dat met succes is verstreken.</span><span class="sxs-lookup"><span data-stu-id="71011-204">A connection test will automatically start when you save your changes, make sure that it has successfully passed.</span></span>
4. <span data-ttu-id="71011-205">Ga naar deel 4.</span><span class="sxs-lookup"><span data-stu-id="71011-205">Proceed to Part 4.</span></span>

### <a name="power-bi"></a><span data-ttu-id="71011-206">Power BI</span><span class="sxs-lookup"><span data-stu-id="71011-206">Power BI</span></span>
1. <span data-ttu-id="71011-207">Klik op de autorisatie vernieuwen:</span><span class="sxs-lookup"><span data-stu-id="71011-207">Click the Renew authorization:</span></span>  

   ![graphic35][graphic35]
2. <span data-ttu-id="71011-209">U krijgt de bevestiging van het volgende:</span><span class="sxs-lookup"><span data-stu-id="71011-209">You will get the following confirmation:</span></span>  

   ![graphic36][graphic36]
3. <span data-ttu-id="71011-211">Klik op de opdracht opslaan en Bevestig de wijzigingen worden opgeslagen:</span><span class="sxs-lookup"><span data-stu-id="71011-211">Click the Save command and confirm saving your changes:</span></span>  
   ![graphic37][graphic37]
4. <span data-ttu-id="71011-213">Een verbindingstest wordt automatisch gestart wanneer u uw wijzigingen hebt opgeslagen, zorg ervoor dat het heeft doorstaan.</span><span class="sxs-lookup"><span data-stu-id="71011-213">A connection test will automatically start when you save your changes, make sure it has successfully passed.</span></span>
5. <span data-ttu-id="71011-214">Ga naar deel 4.</span><span class="sxs-lookup"><span data-stu-id="71011-214">Proceed to Part 4.</span></span>

### <a name="sql-database"></a><span data-ttu-id="71011-215">SQL Database</span><span class="sxs-lookup"><span data-stu-id="71011-215">SQL Database</span></span>
1. <span data-ttu-id="71011-216">De velden gebruikersnaam en wachtwoord te vinden en plak de zojuist gemaakte set referenties in deze:</span><span class="sxs-lookup"><span data-stu-id="71011-216">Find the User Name and Password fields and paste your newly created set of credentials into them:</span></span>  
   ![graphic38][graphic38]
2. <span data-ttu-id="71011-218">Klik op de opdracht opslaan en Bevestig de wijzigingen worden opgeslagen:</span><span class="sxs-lookup"><span data-stu-id="71011-218">Click the Save command and confirm saving your changes:</span></span>  
   ![graphic39][graphic39]
3. <span data-ttu-id="71011-220">Een verbindingstest wordt automatisch gestart wanneer u de wijzigingen opslaan, zorg ervoor dat met succes is verstreken.</span><span class="sxs-lookup"><span data-stu-id="71011-220">A connection test will automatically start when you save your changes, make sure that it has successfully passed.</span></span>  
4. <span data-ttu-id="71011-221">Ga naar deel 4.</span><span class="sxs-lookup"><span data-stu-id="71011-221">Proceed to Part 4.</span></span>

## <a name="part-4-starting-your-job-from-last-stopped-time"></a><span data-ttu-id="71011-222">Deel 4: De taak starten vanuit de tijd van laatste gestopt</span><span class="sxs-lookup"><span data-stu-id="71011-222">Part 4: Starting your job from last stopped time</span></span>
1. <span data-ttu-id="71011-223">De invoer/uitvoer verlaat:</span><span class="sxs-lookup"><span data-stu-id="71011-223">Navigate away from the Input/Output:</span></span>  
   ![graphic40][graphic40]
2. <span data-ttu-id="71011-225">Klik op de opdracht Start:</span><span class="sxs-lookup"><span data-stu-id="71011-225">Click the Start command:</span></span>  
   ![graphic41][graphic41]
3. <span data-ttu-id="71011-227">Kies het laatst is gestopt, en klik op OK:</span><span class="sxs-lookup"><span data-stu-id="71011-227">Pick the Last Stopped Time and click OK:</span></span>  
   ![graphic42][graphic42]
4. <span data-ttu-id="71011-229">Ga naar deel 5.</span><span class="sxs-lookup"><span data-stu-id="71011-229">Proceed to Part 5.</span></span>  

## <a name="part-5-removing-the-old-set-of-credentials"></a><span data-ttu-id="71011-230">Deel 5: De oude set referenties verwijderen</span><span class="sxs-lookup"><span data-stu-id="71011-230">Part 5: Removing the old set of credentials</span></span>
<span data-ttu-id="71011-231">Dit onderdeel is van toepassing op de volgende invoer/uitvoer:</span><span class="sxs-lookup"><span data-stu-id="71011-231">This part is applicable to the following inputs/outputs:</span></span>

* <span data-ttu-id="71011-232">Blob Storage</span><span class="sxs-lookup"><span data-stu-id="71011-232">Blob Storage</span></span>
* <span data-ttu-id="71011-233">Event Hubs</span><span class="sxs-lookup"><span data-stu-id="71011-233">Event Hubs</span></span>
* <span data-ttu-id="71011-234">SQL Database</span><span class="sxs-lookup"><span data-stu-id="71011-234">SQL Database</span></span>
* <span data-ttu-id="71011-235">Table Storage</span><span class="sxs-lookup"><span data-stu-id="71011-235">Table Storage</span></span>

### <a name="blob-storagetable-storage"></a><span data-ttu-id="71011-236">BLOB storage-/ tabelnaam-opslag</span><span class="sxs-lookup"><span data-stu-id="71011-236">Blob storage/Table storage</span></span>
<span data-ttu-id="71011-237">Herhaal Part 1 voor de toegangssleutel die eerder werd gebruikt door de taak voor het vernieuwen van de toegangssleutel nu niet worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="71011-237">Repeat Part 1 for the Access Key that was previously used by your job to renew the now unused Access Key.</span></span>

### <a name="event-hubs"></a><span data-ttu-id="71011-238">Event hubs</span><span class="sxs-lookup"><span data-stu-id="71011-238">Event hubs</span></span>
<span data-ttu-id="71011-239">Herhaal Part 1 voor de sleutel die eerder werd gebruikt door de taak voor het vernieuwen van de sleutel nu niet worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="71011-239">Repeat Part 1 for the Key that was previously used by your job to renew the now unused Key.</span></span>

### <a name="sql-database"></a><span data-ttu-id="71011-240">SQL Database</span><span class="sxs-lookup"><span data-stu-id="71011-240">SQL Database</span></span>
1. <span data-ttu-id="71011-241">Ga terug naar het queryvenster van deel 1 stap 7 en typt u de volgende query waarbij < previous_login_name > vervangt door de gebruikersnaam die eerder werd gebruikt door de taak:</span><span class="sxs-lookup"><span data-stu-id="71011-241">Go back to the query window from Part 1 Step 7 and type in the following query, replacing <previous_login_name> with the User Name that was previously used by your job:</span></span>  
   `DROP LOGIN <previous_login_name>`  
2. <span data-ttu-id="71011-242">Klik op uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="71011-242">Click Run:</span></span>  
   ![graphic43][graphic43]  

<span data-ttu-id="71011-244">U moet de volgende bevestiging krijgen:</span><span class="sxs-lookup"><span data-stu-id="71011-244">You should get the following confirmation:</span></span> 

    Command(s) completed successfully.

## <a name="get-help"></a><span data-ttu-id="71011-245">Help opvragen</span><span class="sxs-lookup"><span data-stu-id="71011-245">Get help</span></span>
<span data-ttu-id="71011-246">Voor verdere hulp kunt u mogelijk terecht op het [Azure Stream Analytics-forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="71011-246">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="71011-247">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="71011-247">Next steps</span></span>
* [<span data-ttu-id="71011-248">Inleiding tot Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="71011-248">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="71011-249">Aan de slag met Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="71011-249">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="71011-250">Azure Stream Analytics-taken schalen</span><span class="sxs-lookup"><span data-stu-id="71011-250">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="71011-251">Naslaggids voor Azure Stream Analytics Query</span><span class="sxs-lookup"><span data-stu-id="71011-251">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="71011-252">REST API-naslaggids voor Azure Stream Analytics Management</span><span class="sxs-lookup"><span data-stu-id="71011-252">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

[graphic1]: ./media/stream-analytics-login-credentials-inputs-outputs/1-stream-analytics-login-credentials-inputs-outputs.png
[graphic2]: ./media/stream-analytics-login-credentials-inputs-outputs/2-stream-analytics-login-credentials-inputs-outputs.png
[graphic3]: ./media/stream-analytics-login-credentials-inputs-outputs/3-stream-analytics-login-credentials-inputs-outputs.png
[graphic4]: ./media/stream-analytics-login-credentials-inputs-outputs/4-stream-analytics-login-credentials-inputs-outputs.png
[graphic5]: ./media/stream-analytics-login-credentials-inputs-outputs/5-stream-analytics-login-credentials-inputs-outputs.png
[graphic6]: ./media/stream-analytics-login-credentials-inputs-outputs/6-stream-analytics-login-credentials-inputs-outputs.png
[graphic7]: ./media/stream-analytics-login-credentials-inputs-outputs/7-stream-analytics-login-credentials-inputs-outputs.png
[graphic8]: ./media/stream-analytics-login-credentials-inputs-outputs/8-stream-analytics-login-credentials-inputs-outputs.png
[graphic9]: ./media/stream-analytics-login-credentials-inputs-outputs/9-stream-analytics-login-credentials-inputs-outputs.png
[graphic10]: ./media/stream-analytics-login-credentials-inputs-outputs/10-stream-analytics-login-credentials-inputs-outputs.png
[graphic11]: ./media/stream-analytics-login-credentials-inputs-outputs/11-stream-analytics-login-credentials-inputs-outputs.png
[graphic12]: ./media/stream-analytics-login-credentials-inputs-outputs/12-stream-analytics-login-credentials-inputs-outputs.png
[graphic13]: ./media/stream-analytics-login-credentials-inputs-outputs/13-stream-analytics-login-credentials-inputs-outputs.png
[graphic14]: ./media/stream-analytics-login-credentials-inputs-outputs/14-stream-analytics-login-credentials-inputs-outputs.png
[graphic15]: ./media/stream-analytics-login-credentials-inputs-outputs/15-stream-analytics-login-credentials-inputs-outputs.png
[graphic16]: ./media/stream-analytics-login-credentials-inputs-outputs/16-stream-analytics-login-credentials-inputs-outputs.png
[graphic17]: ./media/stream-analytics-login-credentials-inputs-outputs/17-stream-analytics-login-credentials-inputs-outputs.png
[graphic18]: ./media/stream-analytics-login-credentials-inputs-outputs/18-stream-analytics-login-credentials-inputs-outputs.png
[graphic19]: ./media/stream-analytics-login-credentials-inputs-outputs/19-stream-analytics-login-credentials-inputs-outputs.png
[graphic20]: ./media/stream-analytics-login-credentials-inputs-outputs/20-stream-analytics-login-credentials-inputs-outputs.png
[graphic21]: ./media/stream-analytics-login-credentials-inputs-outputs/21-stream-analytics-login-credentials-inputs-outputs.png
[graphic22]: ./media/stream-analytics-login-credentials-inputs-outputs/22-stream-analytics-login-credentials-inputs-outputs.png
[graphic23]: ./media/stream-analytics-login-credentials-inputs-outputs/23-stream-analytics-login-credentials-inputs-outputs.png
[graphic24]: ./media/stream-analytics-login-credentials-inputs-outputs/24-stream-analytics-login-credentials-inputs-outputs.png
[graphic25]: ./media/stream-analytics-login-credentials-inputs-outputs/25-stream-analytics-login-credentials-inputs-outputs.png
[graphic26]: ./media/stream-analytics-login-credentials-inputs-outputs/26-stream-analytics-login-credentials-inputs-outputs.png
[graphic27]: ./media/stream-analytics-login-credentials-inputs-outputs/27-stream-analytics-login-credentials-inputs-outputs.png
[graphic28]: ./media/stream-analytics-login-credentials-inputs-outputs/28-stream-analytics-login-credentials-inputs-outputs.png
[graphic29]: ./media/stream-analytics-login-credentials-inputs-outputs/29-stream-analytics-login-credentials-inputs-outputs.png
[graphic30]: ./media/stream-analytics-login-credentials-inputs-outputs/30-stream-analytics-login-credentials-inputs-outputs.png
[graphic31]: ./media/stream-analytics-login-credentials-inputs-outputs/31-stream-analytics-login-credentials-inputs-outputs.png
[graphic32]: ./media/stream-analytics-login-credentials-inputs-outputs/32-stream-analytics-login-credentials-inputs-outputs.png
[graphic33]: ./media/stream-analytics-login-credentials-inputs-outputs/33-stream-analytics-login-credentials-inputs-outputs.png
[graphic34]: ./media/stream-analytics-login-credentials-inputs-outputs/34-stream-analytics-login-credentials-inputs-outputs.png
[graphic35]: ./media/stream-analytics-login-credentials-inputs-outputs/35-stream-analytics-login-credentials-inputs-outputs.png
[graphic36]: ./media/stream-analytics-login-credentials-inputs-outputs/36-stream-analytics-login-credentials-inputs-outputs.png
[graphic37]: ./media/stream-analytics-login-credentials-inputs-outputs/37-stream-analytics-login-credentials-inputs-outputs.png
[graphic38]: ./media/stream-analytics-login-credentials-inputs-outputs/38-stream-analytics-login-credentials-inputs-outputs.png
[graphic39]: ./media/stream-analytics-login-credentials-inputs-outputs/39-stream-analytics-login-credentials-inputs-outputs.png
[graphic40]: ./media/stream-analytics-login-credentials-inputs-outputs/40-stream-analytics-login-credentials-inputs-outputs.png
[graphic41]: ./media/stream-analytics-login-credentials-inputs-outputs/41-stream-analytics-login-credentials-inputs-outputs.png
[graphic42]: ./media/stream-analytics-login-credentials-inputs-outputs/42-stream-analytics-login-credentials-inputs-outputs.png
[graphic43]: ./media/stream-analytics-login-credentials-inputs-outputs/43-stream-analytics-login-credentials-inputs-outputs.png


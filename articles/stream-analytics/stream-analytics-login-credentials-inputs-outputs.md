---
title: 'Stream Analytics: Aanmelden referenties voor de invoer en uitvoer draaien | Microsoft Docs'
description: Meer informatie over hoe tooupdate Hallo-referenties voor Stream Analytics-invoer en uitvoer.
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
ms.openlocfilehash: ac2374c539012b66ab390656c5750024e02f6bdc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="rotate-login-credentials-for-inputs-and-outputs-in-stream-analytics-jobs"></a><span data-ttu-id="919a4-104">Draaien aanmeldingsreferenties voor in- en uitgangen in Stream Analytics-taken</span><span class="sxs-lookup"><span data-stu-id="919a4-104">Rotate login credentials for inputs and outputs in Stream Analytics Jobs</span></span>
## <a name="abstract"></a><span data-ttu-id="919a4-105">Abstracte</span><span class="sxs-lookup"><span data-stu-id="919a4-105">Abstract</span></span>
<span data-ttu-id="919a4-106">Azure Stream Analytics vandaag nog niet is toegestaan Hallo-referenties op een i/o vervangen terwijl Hallo-taak wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="919a4-106">Azure Stream Analytics today doesn’t allow replacing hello credentials on an input/output while hello job is running.</span></span>

<span data-ttu-id="919a4-107">Terwijl Azure Stream Analytics biedt ondersteuning voor het hervatten van een taak van laatste uitvoer, wilden we tooshare Hallo gehele proces voor het minimaliseren Hallo vertraging tussen Hallo stoppen en starten van de taak Hallo en Hallo aanmeldingsreferenties draaien.</span><span class="sxs-lookup"><span data-stu-id="919a4-107">While Azure Stream Analytics does support resuming a job from last output, we wanted tooshare hello entire process for minimizing hello lag between hello stopping and starting of hello job and rotating hello login credentials.</span></span>

## <a name="part-1---prepare-hello-new-set-of-credentials"></a><span data-ttu-id="919a4-108">Deel 1: voorbereiden Hallo nieuwe set referenties:</span><span class="sxs-lookup"><span data-stu-id="919a4-108">Part 1 - Prepare hello new set of credentials:</span></span>
<span data-ttu-id="919a4-109">Dit onderdeel is van toepassing toohello invoer/uitvoer te volgen:</span><span class="sxs-lookup"><span data-stu-id="919a4-109">This part is applicable toohello following inputs/outputs:</span></span>

* <span data-ttu-id="919a4-110">Blob Storage</span><span class="sxs-lookup"><span data-stu-id="919a4-110">Blob Storage</span></span>
* <span data-ttu-id="919a4-111">Event Hubs</span><span class="sxs-lookup"><span data-stu-id="919a4-111">Event Hubs</span></span>
* <span data-ttu-id="919a4-112">SQL Database</span><span class="sxs-lookup"><span data-stu-id="919a4-112">SQL Database</span></span>
* <span data-ttu-id="919a4-113">Table Storage</span><span class="sxs-lookup"><span data-stu-id="919a4-113">Table Storage</span></span>

<span data-ttu-id="919a4-114">Voor andere invoer/uitvoer, gaat u verder met deel 2.</span><span class="sxs-lookup"><span data-stu-id="919a4-114">For other inputs/outputs, proceed with Part 2.</span></span>

### <a name="blob-storagetable-storage"></a><span data-ttu-id="919a4-115">BLOB storage-/ tabelnaam-opslag</span><span class="sxs-lookup"><span data-stu-id="919a4-115">Blob storage/Table storage</span></span>
1. <span data-ttu-id="919a4-116">Ga toohello opslag extensie op Hallo Azure Management portal:</span><span class="sxs-lookup"><span data-stu-id="919a4-116">Go toohello Storage extention on hello Azure Management portal:</span></span>  
   ![graphic1][graphic1]
2. <span data-ttu-id="919a4-118">Zoek naar Hallo opslag van uw werk en gaat u in de App:</span><span class="sxs-lookup"><span data-stu-id="919a4-118">Locate hello storage used by your job and go into it:</span></span>  
   ![graphic2][graphic2]
3. <span data-ttu-id="919a4-120">Klik op Hallo toegangssleutels beheren-opdracht:</span><span class="sxs-lookup"><span data-stu-id="919a4-120">Click hello Manage Access Keys command:</span></span>  
   ![graphic3][graphic3]
4. <span data-ttu-id="919a4-122">Tussen Hallo primaire toegangssleutel en Hallo secundaire toegangssleutel, **Hallo niet gebruikt door uw werk kiezen**.</span><span class="sxs-lookup"><span data-stu-id="919a4-122">Between hello Primary Access Key and hello Secondary Access Key, **pick hello one not used by your job**.</span></span>
5. <span data-ttu-id="919a4-123">Klik op opnieuw genereren:</span><span class="sxs-lookup"><span data-stu-id="919a4-123">Hit regenerate:</span></span>  
   ![graphic4][graphic4]
6. <span data-ttu-id="919a4-125">Kopieer Hallo zojuist gegenereerde sleutel:</span><span class="sxs-lookup"><span data-stu-id="919a4-125">Copy hello newly generated key:</span></span>  
   ![graphic5][graphic5]
7. <span data-ttu-id="919a4-127">Blijven tooPart 2.</span><span class="sxs-lookup"><span data-stu-id="919a4-127">Continue tooPart 2.</span></span>

### <a name="event-hubs"></a><span data-ttu-id="919a4-128">Event hubs</span><span class="sxs-lookup"><span data-stu-id="919a4-128">Event hubs</span></span>
1. <span data-ttu-id="919a4-129">Ga toohello Service Bus-extensie op Hallo Azure Management portal:</span><span class="sxs-lookup"><span data-stu-id="919a4-129">Go toohello Service Bus extension on hello Azure Management portal:</span></span>  
   ![graphic6][graphic6]
2. <span data-ttu-id="919a4-131">Zoek naar Hallo Namespace van Service Bus gebruikt door de taak en gaat u in de App:</span><span class="sxs-lookup"><span data-stu-id="919a4-131">Locate hello Service Bus Namespace used by your job and go into it:</span></span>  
   ![graphic7][graphic7]
3. <span data-ttu-id="919a4-133">Als uw job een gedeeld toegangsbeleid op Hallo Namespace van Service Bus gebruikt, gaan toostep 6</span><span class="sxs-lookup"><span data-stu-id="919a4-133">If your job uses a shared access policy on hello Service Bus Namespace, jump toostep 6</span></span>  
4. <span data-ttu-id="919a4-134">Ga toohello Event Hubs tabblad:</span><span class="sxs-lookup"><span data-stu-id="919a4-134">Go toohello Event Hubs tab:</span></span>  
   ![graphic8][graphic8]
5. <span data-ttu-id="919a4-136">Zoek naar Hallo Event Hub gebruikt door de taak en gaat u in de App:</span><span class="sxs-lookup"><span data-stu-id="919a4-136">Locate hello Event Hub used by your job and go into it:</span></span>  
   ![graphic9][graphic9]
6. <span data-ttu-id="919a4-138">Ga toohello tabblad configureren:</span><span class="sxs-lookup"><span data-stu-id="919a4-138">Go toohello Configure Tab:</span></span>  
   ![graphic10][graphic10]
7. <span data-ttu-id="919a4-140">Zoek op Hallo beleidsnaam vervolgkeuzelijst, Hallo gedeeld toegangsbeleid gebruikt door de taak:</span><span class="sxs-lookup"><span data-stu-id="919a4-140">On hello Policy Name drop-down, locate hello shared access policy used by your job:</span></span>  
   ![graphic11][graphic11]
8. <span data-ttu-id="919a4-142">Tussen Hallo primaire sleutel en secundaire sleutel Hallo **Hallo niet gebruikt door uw werk kiezen**.</span><span class="sxs-lookup"><span data-stu-id="919a4-142">Between hello Primary Key and hello Secondary Key, **pick hello one not used by your job**.</span></span>  
9. <span data-ttu-id="919a4-143">Klik op opnieuw genereren:</span><span class="sxs-lookup"><span data-stu-id="919a4-143">Hit regenerate:</span></span>  
   ![graphic12][graphic12]
10. <span data-ttu-id="919a4-145">Kopieer Hallo zojuist gegenereerde sleutel:</span><span class="sxs-lookup"><span data-stu-id="919a4-145">Copy hello newly generated key:</span></span>  
   ![graphic13][graphic13]
11. <span data-ttu-id="919a4-147">Blijven tooPart 2.</span><span class="sxs-lookup"><span data-stu-id="919a4-147">Continue tooPart 2.</span></span>  

### <a name="sql-database"></a><span data-ttu-id="919a4-148">SQL Database</span><span class="sxs-lookup"><span data-stu-id="919a4-148">SQL Database</span></span>
> [!NOTE]
> <span data-ttu-id="919a4-149">Opmerking: u moet tooconnect toohello SQL Database-Service.</span><span class="sxs-lookup"><span data-stu-id="919a4-149">Note: you will need tooconnect toohello SQL Database Service.</span></span> <span data-ttu-id="919a4-150">We gaan tooshow hoe toodo beheerervaring op deze met Hallo hello Azure-beheerportal, maar u kunt ervoor kiezen toouse sommige clientzijde hulpprogramma ook zoals SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="919a4-150">We are going tooshow how toodo this using hello management experience on hello Azure Management portal but you may choose toouse some client-side tool such as SQL Server Management Studio as well.</span></span>
>
> 

1. <span data-ttu-id="919a4-151">Ga toohello SQL-Databases extensie op Hallo Azure Management portal:</span><span class="sxs-lookup"><span data-stu-id="919a4-151">Go toohello SQL Databases extension on hello Azure Management portal:</span></span>  
   ![graphic14][graphic14]
2. <span data-ttu-id="919a4-153">Hallo SQL-Database gebruikt door de taak vinden en **Klik op de server Hallo** koppelen op Hallo dezelfde regel:</span><span class="sxs-lookup"><span data-stu-id="919a4-153">Locate hello SQL Database used by your job and **click on hello server** link on hello same line:</span></span>  
   <span data-ttu-id="919a4-154">![graphic15][graphic15]</span><span class="sxs-lookup"><span data-stu-id="919a4-154">![graphic15][graphic15]</span></span>
3. <span data-ttu-id="919a4-155">Klik op Hallo beheren-opdracht:</span><span class="sxs-lookup"><span data-stu-id="919a4-155">Click hello Manage command:</span></span>  
   ![graphic16][graphic16]
4. <span data-ttu-id="919a4-157">Type Database Master:</span><span class="sxs-lookup"><span data-stu-id="919a4-157">Type Database Master:</span></span>  
   ![graphic17][graphic17]
5. <span data-ttu-id="919a4-159">Typ uw gebruikersnaam, wachtwoord, en klik op logboek op:</span><span class="sxs-lookup"><span data-stu-id="919a4-159">Type in your User Name, Password, and click Log on:</span></span>  
   ![graphic18][graphic18]
6. <span data-ttu-id="919a4-161">Klik op nieuwe Query:</span><span class="sxs-lookup"><span data-stu-id="919a4-161">Click New Query:</span></span>  
   ![graphic19][graphic19]
7. <span data-ttu-id="919a4-163">Type in Hallo volgende query waarbij < login_name > vervangt door uw gebruikersnaam en het vervangen van <enterStrongPasswordHere> met uw nieuwe wachtwoord:</span><span class="sxs-lookup"><span data-stu-id="919a4-163">Type in hello following query replacing <login_name> with your User Name and replacing <enterStrongPasswordHere> with your new password:</span></span>  
   `CREATE LOGIN <login_name> WITH PASSWORD = '<enterStrongPasswordHere>'`
8. <span data-ttu-id="919a4-164">Klik op uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="919a4-164">Click Run:</span></span>  
   ![graphic20][graphic20]
9. <span data-ttu-id="919a4-166">Ga terug toostep 2 en dit moment op Hallo database:</span><span class="sxs-lookup"><span data-stu-id="919a4-166">Go back toostep 2 and this time click hello database:</span></span>  
   ![graphic21][graphic21]
10. <span data-ttu-id="919a4-168">Klik op Hallo beheren-opdracht:</span><span class="sxs-lookup"><span data-stu-id="919a4-168">Click hello Manage command:</span></span>  
   ![graphic22][graphic22]
11. <span data-ttu-id="919a4-170">Typ uw gebruikersnaam, wachtwoord, en klik op aanmelden:</span><span class="sxs-lookup"><span data-stu-id="919a4-170">type in your User Name, Password, and click Logon:</span></span>  
   ![graphic23][graphic23]
12. <span data-ttu-id="919a4-172">Klik op nieuwe Query:</span><span class="sxs-lookup"><span data-stu-id="919a4-172">Click New Query:</span></span>  
   ![graphic24][graphic24]
13. <span data-ttu-id="919a4-174">Typ in de volgende query < gebruikersnaam > vervangen met een naam die u wilt dat tooidentify Hallo deze aanmelding in de context van deze database hello (u kunt opgeven Hallo dezelfde waarde die u < login_name > bijvoorbeeld gegeven) en < login_name > vervangen door de de gebruikersnaam van uw nieuwe:</span><span class="sxs-lookup"><span data-stu-id="919a4-174">Type in hello following query replacing <user_name> with a name by which you want tooidentify this login in hello context of this database (you can provide hello same value you gave for <login_name>, for example) and replacing <login_name> with your new user name:</span></span>  
   `CREATE USER <user_name> FROM LOGIN <login_name>`
14. <span data-ttu-id="919a4-175">Klik op uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="919a4-175">Click Run:</span></span>  
   ![graphic25][graphic25]
15. <span data-ttu-id="919a4-177">U moet nu de nieuwe gebruiker voorzien Hallo dezelfde functies en de oorspronkelijke gebruiker heeft bevoegdheden.</span><span class="sxs-lookup"><span data-stu-id="919a4-177">You should now provide your new user with hello same roles and privileges your original user had.</span></span>
16. <span data-ttu-id="919a4-178">Blijven tooPart 2.</span><span class="sxs-lookup"><span data-stu-id="919a4-178">Continue tooPart 2.</span></span>

## <a name="part-2-stopping-hello-stream-analytics-job"></a><span data-ttu-id="919a4-179">Deel 2: Stoppen Hallo Stream Analytics-taak</span><span class="sxs-lookup"><span data-stu-id="919a4-179">Part 2: Stopping hello Stream Analytics Job</span></span>
1. <span data-ttu-id="919a4-180">Ga toohello Stream Analytics-extensie op Hallo Azure Management portal:</span><span class="sxs-lookup"><span data-stu-id="919a4-180">Go toohello Stream Analytics extension on hello Azure Management portal:</span></span>  
   ![graphic26][graphic26]
2. <span data-ttu-id="919a4-182">Zoek uw taak en gaat u in de App:</span><span class="sxs-lookup"><span data-stu-id="919a4-182">Locate your job and go into it:</span></span>  
   ![graphic27][graphic27]
3. <span data-ttu-id="919a4-184">Ga toohello invoer tabblad of Hallo uitvoer op basis van of het roteren van Hallo referenties op invoer of uitvoer.</span><span class="sxs-lookup"><span data-stu-id="919a4-184">Go toohello Inputs tab or hello Outputs tab based on whether you are rotating hello credentials on an Input or on an Output.</span></span>  
   ![graphic28][graphic28]
4. <span data-ttu-id="919a4-186">Klik op de opdracht stoppen is Hallo en Bevestig Hallo-taak is gestopt:</span><span class="sxs-lookup"><span data-stu-id="919a4-186">Click hello Stop command and confirm hello job has stopped:</span></span>  
   <span data-ttu-id="919a4-187">![graphic29][graphic29] Hallo taak toostop wacht.</span><span class="sxs-lookup"><span data-stu-id="919a4-187">![graphic29][graphic29] Wait for hello job toostop.</span></span>
5. <span data-ttu-id="919a4-188">Zoek Hallo i/o-u wilt dat toorotate referenties op en gaat u in de App:</span><span class="sxs-lookup"><span data-stu-id="919a4-188">Locate hello input/output you want toorotate credentials on and go into it:</span></span>  
   ![graphic30][graphic30]
6. <span data-ttu-id="919a4-190">TooPart 3 worden voortgezet.</span><span class="sxs-lookup"><span data-stu-id="919a4-190">Proceed tooPart 3.</span></span>

## <a name="part-3-editing-hello-credentials-on-hello-stream-analytics-job"></a><span data-ttu-id="919a4-191">Deel 3: Bewerken Hallo-referenties op Hallo Stream Analytics-taak</span><span class="sxs-lookup"><span data-stu-id="919a4-191">Part 3: Editing hello credentials on hello Stream Analytics Job</span></span>
### <a name="blob-storagetable-storage"></a><span data-ttu-id="919a4-192">BLOB storage-/ tabelnaam-opslag</span><span class="sxs-lookup"><span data-stu-id="919a4-192">Blob storage/Table storage</span></span>
1. <span data-ttu-id="919a4-193">Hallo Opslagaccountsleutel veld vinden en uw zojuist gegenereerde sleutel plakken:</span><span class="sxs-lookup"><span data-stu-id="919a4-193">Find hello Storage Account Key field and paste your newly generated key into it:</span></span>  
   ![graphic31][graphic31]
2. <span data-ttu-id="919a4-195">Klik op de opdracht opslaan Hallo en Bevestig uw wijzigingen:</span><span class="sxs-lookup"><span data-stu-id="919a4-195">Click hello Save command and confirm saving your changes:</span></span>  
   ![graphic32][graphic32]
3. <span data-ttu-id="919a4-197">Een verbindingstest wordt automatisch gestart wanneer u de wijzigingen opslaan, zorg ervoor dat geslaagd is.</span><span class="sxs-lookup"><span data-stu-id="919a4-197">A connection test will automatically start when you save your changes, make sure that is has successfully passed.</span></span>
4. <span data-ttu-id="919a4-198">TooPart 4 worden voortgezet.</span><span class="sxs-lookup"><span data-stu-id="919a4-198">Proceed tooPart 4.</span></span>

### <a name="event-hubs"></a><span data-ttu-id="919a4-199">Event hubs</span><span class="sxs-lookup"><span data-stu-id="919a4-199">Event hubs</span></span>
1. <span data-ttu-id="919a4-200">Hallo Event Hub beleid sleutelveld vinden en uw zojuist gegenereerde sleutel plakken:</span><span class="sxs-lookup"><span data-stu-id="919a4-200">Find hello Event Hub Policy Key field and paste your newly generated key into it:</span></span>  
   ![graphic33][graphic33]
2. <span data-ttu-id="919a4-202">Klik op de opdracht opslaan Hallo en Bevestig uw wijzigingen:</span><span class="sxs-lookup"><span data-stu-id="919a4-202">Click hello Save command and confirm saving your changes:</span></span>  
   ![graphic34][graphic34]
3. <span data-ttu-id="919a4-204">Een verbindingstest wordt automatisch gestart wanneer u de wijzigingen opslaan, zorg ervoor dat met succes is verstreken.</span><span class="sxs-lookup"><span data-stu-id="919a4-204">A connection test will automatically start when you save your changes, make sure that it has successfully passed.</span></span>
4. <span data-ttu-id="919a4-205">TooPart 4 worden voortgezet.</span><span class="sxs-lookup"><span data-stu-id="919a4-205">Proceed tooPart 4.</span></span>

### <a name="power-bi"></a><span data-ttu-id="919a4-206">Power BI</span><span class="sxs-lookup"><span data-stu-id="919a4-206">Power BI</span></span>
1. <span data-ttu-id="919a4-207">Klik op Hallo vernieuwen autorisatie:</span><span class="sxs-lookup"><span data-stu-id="919a4-207">Click hello Renew authorization:</span></span>  

   ![graphic35][graphic35]
2. <span data-ttu-id="919a4-209">U ontvangt Hallo na de bevestiging:</span><span class="sxs-lookup"><span data-stu-id="919a4-209">You will get hello following confirmation:</span></span>  

   ![graphic36][graphic36]
3. <span data-ttu-id="919a4-211">Klik op de opdracht opslaan Hallo en Bevestig uw wijzigingen:</span><span class="sxs-lookup"><span data-stu-id="919a4-211">Click hello Save command and confirm saving your changes:</span></span>  
   ![graphic37][graphic37]
4. <span data-ttu-id="919a4-213">Een verbindingstest wordt automatisch gestart wanneer u uw wijzigingen hebt opgeslagen, zorg ervoor dat het heeft doorstaan.</span><span class="sxs-lookup"><span data-stu-id="919a4-213">A connection test will automatically start when you save your changes, make sure it has successfully passed.</span></span>
5. <span data-ttu-id="919a4-214">TooPart 4 worden voortgezet.</span><span class="sxs-lookup"><span data-stu-id="919a4-214">Proceed tooPart 4.</span></span>

### <a name="sql-database"></a><span data-ttu-id="919a4-215">SQL Database</span><span class="sxs-lookup"><span data-stu-id="919a4-215">SQL Database</span></span>
1. <span data-ttu-id="919a4-216">Hallo velden gebruikersnaam en wachtwoord te zoeken en plak de zojuist gemaakte set referenties in deze:</span><span class="sxs-lookup"><span data-stu-id="919a4-216">Find hello User Name and Password fields and paste your newly created set of credentials into them:</span></span>  
   ![graphic38][graphic38]
2. <span data-ttu-id="919a4-218">Klik op de opdracht opslaan Hallo en Bevestig uw wijzigingen:</span><span class="sxs-lookup"><span data-stu-id="919a4-218">Click hello Save command and confirm saving your changes:</span></span>  
   ![graphic39][graphic39]
3. <span data-ttu-id="919a4-220">Een verbindingstest wordt automatisch gestart wanneer u de wijzigingen opslaan, zorg ervoor dat met succes is verstreken.</span><span class="sxs-lookup"><span data-stu-id="919a4-220">A connection test will automatically start when you save your changes, make sure that it has successfully passed.</span></span>  
4. <span data-ttu-id="919a4-221">TooPart 4 worden voortgezet.</span><span class="sxs-lookup"><span data-stu-id="919a4-221">Proceed tooPart 4.</span></span>

## <a name="part-4-starting-your-job-from-last-stopped-time"></a><span data-ttu-id="919a4-222">Deel 4: De taak starten vanuit de tijd van laatste gestopt</span><span class="sxs-lookup"><span data-stu-id="919a4-222">Part 4: Starting your job from last stopped time</span></span>
1. <span data-ttu-id="919a4-223">Hallo Input/Output verlaat:</span><span class="sxs-lookup"><span data-stu-id="919a4-223">Navigate away from hello Input/Output:</span></span>  
   ![graphic40][graphic40]
2. <span data-ttu-id="919a4-225">Klik op de opdracht Start Hallo:</span><span class="sxs-lookup"><span data-stu-id="919a4-225">Click hello Start command:</span></span>  
   ![graphic41][graphic41]
3. <span data-ttu-id="919a4-227">Hallo laatste tijd geëindigd kiezen en klik op OK:</span><span class="sxs-lookup"><span data-stu-id="919a4-227">Pick hello Last Stopped Time and click OK:</span></span>  
   ![graphic42][graphic42]
4. <span data-ttu-id="919a4-229">TooPart 5 worden voortgezet.</span><span class="sxs-lookup"><span data-stu-id="919a4-229">Proceed tooPart 5.</span></span>  

## <a name="part-5-removing-hello-old-set-of-credentials"></a><span data-ttu-id="919a4-230">Deel 5: Verwijderen van Hallo oude set referenties</span><span class="sxs-lookup"><span data-stu-id="919a4-230">Part 5: Removing hello old set of credentials</span></span>
<span data-ttu-id="919a4-231">Dit onderdeel is van toepassing toohello invoer/uitvoer te volgen:</span><span class="sxs-lookup"><span data-stu-id="919a4-231">This part is applicable toohello following inputs/outputs:</span></span>

* <span data-ttu-id="919a4-232">Blob Storage</span><span class="sxs-lookup"><span data-stu-id="919a4-232">Blob Storage</span></span>
* <span data-ttu-id="919a4-233">Event Hubs</span><span class="sxs-lookup"><span data-stu-id="919a4-233">Event Hubs</span></span>
* <span data-ttu-id="919a4-234">SQL Database</span><span class="sxs-lookup"><span data-stu-id="919a4-234">SQL Database</span></span>
* <span data-ttu-id="919a4-235">Table Storage</span><span class="sxs-lookup"><span data-stu-id="919a4-235">Table Storage</span></span>

### <a name="blob-storagetable-storage"></a><span data-ttu-id="919a4-236">BLOB storage-/ tabelnaam-opslag</span><span class="sxs-lookup"><span data-stu-id="919a4-236">Blob storage/Table storage</span></span>
<span data-ttu-id="919a4-237">Deel 1 herhalen voor Hallo toegangssleutel die eerder werd gebruikt door uw taak toorenew Hallo nu ongebruikte toegangssleutel.</span><span class="sxs-lookup"><span data-stu-id="919a4-237">Repeat Part 1 for hello Access Key that was previously used by your job toorenew hello now unused Access Key.</span></span>

### <a name="event-hubs"></a><span data-ttu-id="919a4-238">Event hubs</span><span class="sxs-lookup"><span data-stu-id="919a4-238">Event hubs</span></span>
<span data-ttu-id="919a4-239">Deel 1 herhalen voor Hallo sleutel die eerder werd gebruikt door uw taak toorenew Hallo nu ongebruikte sleutel.</span><span class="sxs-lookup"><span data-stu-id="919a4-239">Repeat Part 1 for hello Key that was previously used by your job toorenew hello now unused Key.</span></span>

### <a name="sql-database"></a><span data-ttu-id="919a4-240">SQL Database</span><span class="sxs-lookup"><span data-stu-id="919a4-240">SQL Database</span></span>
1. <span data-ttu-id="919a4-241">Ga terug toohello queryvenster van deel 1 stap 7 en typt u Hallo query de volgende, waarbij < previous_login_name > vervangt door Hallo gebruikersnaam die eerder werd gebruikt door de taak:</span><span class="sxs-lookup"><span data-stu-id="919a4-241">Go back toohello query window from Part 1 Step 7 and type in hello following query, replacing <previous_login_name> with hello User Name that was previously used by your job:</span></span>  
   `DROP LOGIN <previous_login_name>`  
2. <span data-ttu-id="919a4-242">Klik op uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="919a4-242">Click Run:</span></span>  
   ![graphic43][graphic43]  

<span data-ttu-id="919a4-244">U moet Hallo na de bevestiging krijgen:</span><span class="sxs-lookup"><span data-stu-id="919a4-244">You should get hello following confirmation:</span></span> 

    Command(s) completed successfully.

## <a name="get-help"></a><span data-ttu-id="919a4-245">Help opvragen</span><span class="sxs-lookup"><span data-stu-id="919a4-245">Get help</span></span>
<span data-ttu-id="919a4-246">Voor verdere hulp kunt u mogelijk terecht op het [Azure Stream Analytics-forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="919a4-246">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="919a4-247">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="919a4-247">Next steps</span></span>
* [<span data-ttu-id="919a4-248">Inleiding tooAzure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="919a4-248">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="919a4-249">Aan de slag met Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="919a4-249">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="919a4-250">Azure Stream Analytics-taken schalen</span><span class="sxs-lookup"><span data-stu-id="919a4-250">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="919a4-251">Naslaggids voor Azure Stream Analytics Query</span><span class="sxs-lookup"><span data-stu-id="919a4-251">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="919a4-252">REST API-naslaggids voor Azure Stream Analytics Management</span><span class="sxs-lookup"><span data-stu-id="919a4-252">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

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


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
# <a name="rotate-login-credentials-for-inputs-and-outputs-in-stream-analytics-jobs"></a>Draaien aanmeldingsreferenties voor in- en uitgangen in Stream Analytics-taken
## <a name="abstract"></a>Abstracte
Azure Stream Analytics vandaag nog niet is toegestaan Hallo-referenties op een i/o vervangen terwijl Hallo-taak wordt uitgevoerd.

Terwijl Azure Stream Analytics biedt ondersteuning voor het hervatten van een taak van laatste uitvoer, wilden we tooshare Hallo gehele proces voor het minimaliseren Hallo vertraging tussen Hallo stoppen en starten van de taak Hallo en Hallo aanmeldingsreferenties draaien.

## <a name="part-1---prepare-hello-new-set-of-credentials"></a>Deel 1: voorbereiden Hallo nieuwe set referenties:
Dit onderdeel is van toepassing toohello invoer/uitvoer te volgen:

* Blob Storage
* Event Hubs
* SQL Database
* Table Storage

Voor andere invoer/uitvoer, gaat u verder met deel 2.

### <a name="blob-storagetable-storage"></a>BLOB storage-/ tabelnaam-opslag
1. Ga toohello opslag extensie op Hallo Azure Management portal:  
   ![graphic1][graphic1]
2. Zoek naar Hallo opslag van uw werk en gaat u in de App:  
   ![graphic2][graphic2]
3. Klik op Hallo toegangssleutels beheren-opdracht:  
   ![graphic3][graphic3]
4. Tussen Hallo primaire toegangssleutel en Hallo secundaire toegangssleutel, **Hallo niet gebruikt door uw werk kiezen**.
5. Klik op opnieuw genereren:  
   ![graphic4][graphic4]
6. Kopieer Hallo zojuist gegenereerde sleutel:  
   ![graphic5][graphic5]
7. Blijven tooPart 2.

### <a name="event-hubs"></a>Event hubs
1. Ga toohello Service Bus-extensie op Hallo Azure Management portal:  
   ![graphic6][graphic6]
2. Zoek naar Hallo Namespace van Service Bus gebruikt door de taak en gaat u in de App:  
   ![graphic7][graphic7]
3. Als uw job een gedeeld toegangsbeleid op Hallo Namespace van Service Bus gebruikt, gaan toostep 6  
4. Ga toohello Event Hubs tabblad:  
   ![graphic8][graphic8]
5. Zoek naar Hallo Event Hub gebruikt door de taak en gaat u in de App:  
   ![graphic9][graphic9]
6. Ga toohello tabblad configureren:  
   ![graphic10][graphic10]
7. Zoek op Hallo beleidsnaam vervolgkeuzelijst, Hallo gedeeld toegangsbeleid gebruikt door de taak:  
   ![graphic11][graphic11]
8. Tussen Hallo primaire sleutel en secundaire sleutel Hallo **Hallo niet gebruikt door uw werk kiezen**.  
9. Klik op opnieuw genereren:  
   ![graphic12][graphic12]
10. Kopieer Hallo zojuist gegenereerde sleutel:  
   ![graphic13][graphic13]
11. Blijven tooPart 2.  

### <a name="sql-database"></a>SQL Database
> [!NOTE]
> Opmerking: u moet tooconnect toohello SQL Database-Service. We gaan tooshow hoe toodo beheerervaring op deze met Hallo hello Azure-beheerportal, maar u kunt ervoor kiezen toouse sommige clientzijde hulpprogramma ook zoals SQL Server Management Studio.
>
> 

1. Ga toohello SQL-Databases extensie op Hallo Azure Management portal:  
   ![graphic14][graphic14]
2. Hallo SQL-Database gebruikt door de taak vinden en **Klik op de server Hallo** koppelen op Hallo dezelfde regel:  
   ![graphic15][graphic15]
3. Klik op Hallo beheren-opdracht:  
   ![graphic16][graphic16]
4. Type Database Master:  
   ![graphic17][graphic17]
5. Typ uw gebruikersnaam, wachtwoord, en klik op logboek op:  
   ![graphic18][graphic18]
6. Klik op nieuwe Query:  
   ![graphic19][graphic19]
7. Type in Hallo volgende query waarbij < login_name > vervangt door uw gebruikersnaam en het vervangen van <enterStrongPasswordHere> met uw nieuwe wachtwoord:  
   `CREATE LOGIN <login_name> WITH PASSWORD = '<enterStrongPasswordHere>'`
8. Klik op uitvoeren:  
   ![graphic20][graphic20]
9. Ga terug toostep 2 en dit moment op Hallo database:  
   ![graphic21][graphic21]
10. Klik op Hallo beheren-opdracht:  
   ![graphic22][graphic22]
11. Typ uw gebruikersnaam, wachtwoord, en klik op aanmelden:  
   ![graphic23][graphic23]
12. Klik op nieuwe Query:  
   ![graphic24][graphic24]
13. Typ in de volgende query < gebruikersnaam > vervangen met een naam die u wilt dat tooidentify Hallo deze aanmelding in de context van deze database hello (u kunt opgeven Hallo dezelfde waarde die u < login_name > bijvoorbeeld gegeven) en < login_name > vervangen door de de gebruikersnaam van uw nieuwe:  
   `CREATE USER <user_name> FROM LOGIN <login_name>`
14. Klik op uitvoeren:  
   ![graphic25][graphic25]
15. U moet nu de nieuwe gebruiker voorzien Hallo dezelfde functies en de oorspronkelijke gebruiker heeft bevoegdheden.
16. Blijven tooPart 2.

## <a name="part-2-stopping-hello-stream-analytics-job"></a>Deel 2: Stoppen Hallo Stream Analytics-taak
1. Ga toohello Stream Analytics-extensie op Hallo Azure Management portal:  
   ![graphic26][graphic26]
2. Zoek uw taak en gaat u in de App:  
   ![graphic27][graphic27]
3. Ga toohello invoer tabblad of Hallo uitvoer op basis van of het roteren van Hallo referenties op invoer of uitvoer.  
   ![graphic28][graphic28]
4. Klik op de opdracht stoppen is Hallo en Bevestig Hallo-taak is gestopt:  
   ![graphic29][graphic29] Hallo taak toostop wacht.
5. Zoek Hallo i/o-u wilt dat toorotate referenties op en gaat u in de App:  
   ![graphic30][graphic30]
6. TooPart 3 worden voortgezet.

## <a name="part-3-editing-hello-credentials-on-hello-stream-analytics-job"></a>Deel 3: Bewerken Hallo-referenties op Hallo Stream Analytics-taak
### <a name="blob-storagetable-storage"></a>BLOB storage-/ tabelnaam-opslag
1. Hallo Opslagaccountsleutel veld vinden en uw zojuist gegenereerde sleutel plakken:  
   ![graphic31][graphic31]
2. Klik op de opdracht opslaan Hallo en Bevestig uw wijzigingen:  
   ![graphic32][graphic32]
3. Een verbindingstest wordt automatisch gestart wanneer u de wijzigingen opslaan, zorg ervoor dat geslaagd is.
4. TooPart 4 worden voortgezet.

### <a name="event-hubs"></a>Event hubs
1. Hallo Event Hub beleid sleutelveld vinden en uw zojuist gegenereerde sleutel plakken:  
   ![graphic33][graphic33]
2. Klik op de opdracht opslaan Hallo en Bevestig uw wijzigingen:  
   ![graphic34][graphic34]
3. Een verbindingstest wordt automatisch gestart wanneer u de wijzigingen opslaan, zorg ervoor dat met succes is verstreken.
4. TooPart 4 worden voortgezet.

### <a name="power-bi"></a>Power BI
1. Klik op Hallo vernieuwen autorisatie:  

   ![graphic35][graphic35]
2. U ontvangt Hallo na de bevestiging:  

   ![graphic36][graphic36]
3. Klik op de opdracht opslaan Hallo en Bevestig uw wijzigingen:  
   ![graphic37][graphic37]
4. Een verbindingstest wordt automatisch gestart wanneer u uw wijzigingen hebt opgeslagen, zorg ervoor dat het heeft doorstaan.
5. TooPart 4 worden voortgezet.

### <a name="sql-database"></a>SQL Database
1. Hallo velden gebruikersnaam en wachtwoord te zoeken en plak de zojuist gemaakte set referenties in deze:  
   ![graphic38][graphic38]
2. Klik op de opdracht opslaan Hallo en Bevestig uw wijzigingen:  
   ![graphic39][graphic39]
3. Een verbindingstest wordt automatisch gestart wanneer u de wijzigingen opslaan, zorg ervoor dat met succes is verstreken.  
4. TooPart 4 worden voortgezet.

## <a name="part-4-starting-your-job-from-last-stopped-time"></a>Deel 4: De taak starten vanuit de tijd van laatste gestopt
1. Hallo Input/Output verlaat:  
   ![graphic40][graphic40]
2. Klik op de opdracht Start Hallo:  
   ![graphic41][graphic41]
3. Hallo laatste tijd geëindigd kiezen en klik op OK:  
   ![graphic42][graphic42]
4. TooPart 5 worden voortgezet.  

## <a name="part-5-removing-hello-old-set-of-credentials"></a>Deel 5: Verwijderen van Hallo oude set referenties
Dit onderdeel is van toepassing toohello invoer/uitvoer te volgen:

* Blob Storage
* Event Hubs
* SQL Database
* Table Storage

### <a name="blob-storagetable-storage"></a>BLOB storage-/ tabelnaam-opslag
Deel 1 herhalen voor Hallo toegangssleutel die eerder werd gebruikt door uw taak toorenew Hallo nu ongebruikte toegangssleutel.

### <a name="event-hubs"></a>Event hubs
Deel 1 herhalen voor Hallo sleutel die eerder werd gebruikt door uw taak toorenew Hallo nu ongebruikte sleutel.

### <a name="sql-database"></a>SQL Database
1. Ga terug toohello queryvenster van deel 1 stap 7 en typt u Hallo query de volgende, waarbij < previous_login_name > vervangt door Hallo gebruikersnaam die eerder werd gebruikt door de taak:  
   `DROP LOGIN <previous_login_name>`  
2. Klik op uitvoeren:  
   ![graphic43][graphic43]  

U moet Hallo na de bevestiging krijgen: 

    Command(s) completed successfully.

## <a name="get-help"></a>Help opvragen
Voor verdere hulp kunt u mogelijk terecht op het [Azure Stream Analytics-forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)

## <a name="next-steps"></a>Volgende stappen
* [Inleiding tooAzure Stream Analytics](stream-analytics-introduction.md)
* [Aan de slag met Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [Azure Stream Analytics-taken schalen](stream-analytics-scale-jobs.md)
* [Naslaggids voor Azure Stream Analytics Query](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [REST API-naslaggids voor Azure Stream Analytics Management](https://msdn.microsoft.com/library/azure/dn835031.aspx)

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


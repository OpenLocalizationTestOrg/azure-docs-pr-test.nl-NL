---
title: 'Stream Analytics-uitvoer: opties voor opslag, analyse | Microsoft Docs'
description: Meer informatie over Stream Analytics uitvoer Gegevensopties met inbegrip van Power BI voor analyseresultaten als doel.
keywords: gegevenstransformatie, analyseresultaten, opties voor opslag van gegevens
services: stream-analytics,documentdb,sql-database,event-hubs,service-bus,storage
documentationcenter: 
author: samacha
manager: jhubbard
editor: cgronlun
ms.assetid: ba6697ac-e90f-4be3-bafd-5cfcf4bd8f1f
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: samacha
ms.openlocfilehash: 99f8113f0464960e898293397fbe3de90d669857
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="stream-analytics-outputs-options-for-storage-analysis"></a>Stream Analytics-uitvoer: opties voor opslag, analyse
Houd rekening met hoe Hallo resulterende gegevens worden gebruikt bij het ontwerpen van een Stream Analytics-taak. Hoe wordt u Hallo resultaten van Hallo Stream Analytics-taak weergeven en waar wilt u deze opslaan?

Azure Stream Analytics heeft in volgorde tooenable tal van toepassing patronen, verschillende opties voor het opslaan van de uitvoer en weergeven van resultaten van de analyse. Dit maakt het eenvoudig tooview taakuitvoer en geeft u de extra flexibiliteit in Hallo verbruik en de opslag van de taakuitvoer Hallo voor gegevensopslag en andere doeleinden. Geen uitvoer geconfigureerd in het Hallo-taak moet bestaan voordat Hallo-taak is gestart en gebeurtenissen start stromende. Bijvoorbeeld, als u een Blob-opslag als uitvoer gebruikt, maakt Hallo-taak niet een opslagaccount automatisch. Het moet toobe gemaakt door gebruiker Hallo voordat Hallo ASA-taak is gestart.

## <a name="azure-data-lake-store"></a>Azure Data Lake Store
Stream Analytics ondersteunt [Azure Data Lake Store](https://azure.microsoft.com/services/data-lake-store/). Deze opslag kunt u toostore gegevens van elke grootte, type en opnamesnelheid snelheid voor operationele en experimentele analyses. Bovendien wordt geautoriseerd Stream Analytics behoeften toobe tooaccess Hallo Data Lake Store. Meer informatie over de autorisatie en hoe toosign voor Hallo Data Lake Store (indien nodig) worden besproken in Hallo [Data Lake uitvoer artikel](stream-analytics-data-lake-output.md).

### <a name="authorize-an-azure-data-lake-store"></a>Een Azure Data Lake Store toestaan
Wanneer Data Lake Storage als uitvoer in hello Azure-portal is geselecteerd, kunt u zich na vragen aan gebruiker tooauthorize een verbinding tooan bestaande Data Lake Store.  

![Data Lake Store toestaan](./media/stream-analytics-define-outputs/06-stream-analytics-define-outputs.png)  

Vul vervolgens Hallo-eigenschappen voor Hallo Data Lake Store uitvoer zoals hieronder wordt weergegeven:

![Data Lake Store toestaan](./media/stream-analytics-define-outputs/07-stream-analytics-define-outputs.png)  

Hallo in de volgende tabel geeft een lijst Hallo eigenschapnamen en hun beschrijving op die nodig zijn voor het maken van een Data Lake Store-uitvoer.

<table>
<tbody>
<tr>
<td><B>DE NAAM VAN EIGENSCHAP</B></td>
<td><B>BESCHRIJVING</B></td>
</tr>
<tr>
<td>Uitvoeraliassen</td>
<td>Dit is een beschrijvende naam die is gebruikt in query's toodirect Hallo query uitvoer toothis Data Lake Store.</td>
</tr>
<tr>
<td>Accountnaam</td>
<td>de naam van de Hallo Hallo Data Lake Storage-account waarin u de uitvoer wilt verzenden. U krijgt een vervolgkeuzelijst met Data Lake Store-accounts toowhich Hallo gebruiker aangemeld toohello portal toegang tot heeft.</td>
</tr>
<tr>
<td>Pad voorvoegsel patroon [<I>optionele</I>]</td>
<td>Hallo bestand pad gebruikt toowrite uw bestanden binnen Hallo Data Lake Store-Account opgegeven. <BR>{date} {time}<BR>Voorbeeld 1: Map1/logs / {date} / {time}<BR>Voorbeeld 2: Map1/logs / {date}</td>
</tr>
<tr>
<td>Datum notatie [<I>optionele</I>]</td>
<td>Als Hallo datum token in Hallo voorvoegsel pad wordt gebruikt, kunt u Hallo datumnotatie waarin de bestanden zijn ingedeeld. Voorbeeld: Jjjj/MM/DD</td>
</tr>
<tr>
<td>Tijdnotatie [<I>optionele</I>]</td>
<td>Als Hallo tijd token in Hallo voorvoegsel pad wordt gebruikt, geeft u de tijdnotatie Hallo waarin de bestanden zijn ingedeeld. Hallo alleen ondersteunde waarde is momenteel HH.</td>
</tr>
<tr>
<td>Gebeurtenis serialisatie-indeling</td>
<td>Serialisatie-indeling voor uitvoergegevens. JSON, CSV en Avro worden ondersteund.</td>
</tr>
<tr>
<td>Encoding</td>
<td>Als CSV- of JSON-indeling, moet een codering worden opgegeven. UTF-8 wordt de coderingsindeling Hallo alleen ondersteund op dit moment.</td>
</tr>
<tr>
<td>Scheidingsteken</td>
<td>Alleen van toepassing voor CSV-serialisatie. Stream Analytics ondersteunt een aantal algemene scheidingstekens voor het serialiseren van CSV-gegevens. Ondersteunde waarden zijn komma, puntkomma, spatie, tab en de verticale balk.</td>
</tr>
<tr>
<td>Indeling</td>
<td>Alleen van toepassing op JSON-serialisatie. Lijn gescheiden geeft aan dat Hallo uitvoer wordt ingedeeld door elk JSON-object dat is gescheiden door een nieuwe regel. Matrix geeft aan dat Hallo uitvoer wordt ingedeeld als een matrix met JSON-objecten.</td>
</tr>
</tbody>
</table>

### <a name="renew-data-lake-store-authorization"></a>Vernieuwen van Data Lake Store-autorisatie
U moet toore-verificatie van uw Data Lake Store-account als het wachtwoord is gewijzigd sinds de taak is gemaakt of laatst geverifieerd.

![Data Lake Store toestaan](./media/stream-analytics-define-outputs/08-stream-analytics-define-outputs.png)  

## <a name="sql-database"></a>SQL Database
[Azure SQL Database](https://azure.microsoft.com/services/sql-database/) kan worden gebruikt als uitvoer voor gegevens die relationele gegevens of voor toepassingen die afhankelijk zijn van de inhoud wordt gehost in een relationele database. Stream Analytics-taken worden de bestaande tabel tooan geschreven in een Azure SQL Database.  Houd er rekening mee dat Hallo het schema van tabel moet exact overeenkomen Hallo velden en hun typen wordt de uitvoer van de taak. Een [Azure SQL Data Warehouse](https://azure.microsoft.com/documentation/services/sql-data-warehouse/) kan ook worden opgegeven als uitvoer via Hallo SQL-Database output-optie ook (dit is een preview-functie). Hallo in de volgende tabel geeft een lijst Hallo eigenschapnamen en hun beschrijving voor het maken van de uitvoer van een SQL-Database.

| De naam van eigenschap | Beschrijving |
| --- | --- |
| Uitvoeraliassen |Dit is een beschrijvende naam die in query's toodirect Hallo query uitvoer toothis database gebruikt. |
| Database |Hallo-naam van Hallo-database waar u de uitvoer wilt verzenden |
| Servernaam |Hallo SQL Database-servernaam |
| Gebruikersnaam |Hallo gebruikersnaam waarvoor toegang toowrite toohello database |
| Wachtwoord |Hallo wachtwoord tooconnect toohello database |
| Tabel |Hallo-tabelnaam waar Hallo uitvoer worden geschreven. Hallo tabelnaam is hoofdlettergevoelig en Hallo-schema van deze tabel moet overeenkomen met exact toohello aantal velden en hun type wordt gegenereerd door de taakuitvoer. |

> [!NOTE]
> Hello Azure SQL Database aanbieding wordt momenteel ondersteund voor de taakuitvoer van een in de Stream Analytics. Een virtuele Machine van Azure met SQL Server met een database die is gekoppeld, wordt echter niet ondersteund. Dit is onderwerp toochange in toekomstige releases.
> 
> 

## <a name="blob-storage"></a>Blob Storage
BLOB storage vormt een rendabele en schaalbare oplossing voor het opslaan van grote hoeveelheden ongestructureerde gegevens in de cloud Hallo.  Zie voor een inleiding op Azure Blob-opslag en het gebruik ervan Hallo-documentatie op [hoe toouse Blobs](../storage/blobs/storage-dotnet-how-to-use-blobs.md).

Hallo in de volgende tabel geeft een lijst Hallo eigenschapnamen en hun beschrijving voor het maken van een blob-uitvoer.

<table>
<tbody>
<tr>
<td>DE NAAM VAN EIGENSCHAP</td>
<td>BESCHRIJVING</td>
</tr>
<tr>
<td>Uitvoeraliassen</td>
<td>Dit is een beschrijvende naam die is gebruikt in query's toodirect Hallo query uitvoer toothis blob-opslag.</td>
</tr>
<tr>
<td>Storage-Account</td>
<td>Hallo-naam van Hallo storage-account waarin u de uitvoer wilt verzenden.</td>
</tr>
<tr>
<td>De sleutel van opslagaccount</td>
<td>de geheime sleutel Hallo Hallo storage-account gekoppeld.</td>
</tr>
<tr>
<td>Storage-Container</td>
<td>Containers bieden een logische groepering van blobs die zijn opgeslagen in Hallo Microsoft Azure Blob-service. U moet een container voor blob opgeven tijdens het uploaden van een blob toohello Blob-service.</td>
</tr>
<tr>
<td>Pad voorvoegsel patroon [optioneel]</td>
<td>Hallo-bestandspad gebruikt toowrite uw blobs in de opgegeven container Hallo.<BR>Binnen Hallo pad, kunt u kiezen toouse een of meer exemplaren van Hallo 2 variabelen toospecify Hallo frequentie die zijn geschreven met blobs te volgen:<BR>{date} {time}<BR>Voorbeeld 1: cluster1/logs / {date} / {time}<BR>Voorbeeld 2: cluster1/logs / {date}</td>
</tr>
<tr>
<td>[Optioneel] datumnotatie</td>
<td>Als Hallo datum token in Hallo voorvoegsel pad wordt gebruikt, kunt u Hallo datumnotatie waarin de bestanden zijn ingedeeld. Voorbeeld: Jjjj/MM/DD</td>
</tr>
<tr>
<td>[Optioneel] tijdnotatie</td>
<td>Als Hallo tijd token in Hallo voorvoegsel pad wordt gebruikt, geeft u de tijdnotatie Hallo waarin de bestanden zijn ingedeeld. Hallo alleen ondersteunde waarde is momenteel HH.</td>
</tr>
<tr>
<td>Gebeurtenis serialisatie-indeling</td>
<td>Serialisatie-indeling voor uitvoergegevens.  JSON, CSV en Avro worden ondersteund.</td>
</tr>
<tr>
<td>Encoding</td>
<td>Als CSV- of JSON-indeling, moet een codering worden opgegeven. UTF-8 wordt de coderingsindeling Hallo alleen ondersteund op dit moment.</td>
</tr>
<tr>
<td>Scheidingsteken</td>
<td>Alleen van toepassing voor CSV-serialisatie. Stream Analytics ondersteunt een aantal algemene scheidingstekens voor het serialiseren van CSV-gegevens. Ondersteunde waarden zijn komma, puntkomma, spatie, tab en de verticale balk.</td>
</tr>
<tr>
<td>Indeling</td>
<td>Alleen van toepassing op JSON-serialisatie. Lijn gescheiden geeft aan dat Hallo uitvoer wordt ingedeeld door elk JSON-object dat is gescheiden door een nieuwe regel. Matrix geeft aan dat Hallo uitvoer wordt ingedeeld als een matrix met JSON-objecten. Deze matrix wordt alleen wanneer Hallo taak reageert of Stream Analytics is verplaatst op de volgende tijdvenster toohello worden gesloten. In het algemeen is het beter toouse lijn gescheiden JSON, omdat er geen speciale verwerking niet nodig tijdens het Hallo-uitvoerbestand nog steeds wordt geschreven.</td>
</tr>
</tbody>
</table>

## <a name="event-hub"></a>Event Hub
[Event Hubs](https://azure.microsoft.com/services/event-hubs/) is een uiterst schaalbare voor publiceren / abonneren event ingestor. Het kan miljoenen gebeurtenissen per seconde verzamelen.  Een gebruik van een Event Hub als uitvoer het is Hallo-uitvoer van een Stream Analytics-taak Hallo invoer van een ander streaming-taak.

Er zijn een aantal parameters die vereist tooconfigure Event Hub-gegevensstromen als uitvoer zijn.

| De naam van eigenschap | Beschrijving |
| --- | --- |
| Uitvoeraliassen |Dit is een beschrijvende naam die is gebruikt in query's toodirect Hallo query uitvoer toothis Event Hub. |
| Service Bus Namespace |Een Service Bus-naamruimte is een container voor een set berichtentiteiten. Wanneer u een nieuwe Event Hub hebt gemaakt, hebt u ook een Service Bus-naamruimte gemaakt |
| Event Hub |Hallo-naam van uw Event Hub-uitvoer |
| Naam Event Hub-beleid |beleid voor gedeelde toegang, die kan worden gemaakt op Hallo Event Hub configureren tabblad Hallo. Elk gedeeld toegangsbeleid wordt hebben een naam, machtigingen die u instelt en toegangssleutels |
| Event Hub beleidssleutel |Hallo toegang tot gedeelde sleutel gebruikt tooauthenticate toegang toohello Service Bus-naamruimte |
| Partitie-sleutelkolom [optioneel] |Deze kolom bevat de partitiesleutel Hallo voor uitvoer van de Event Hub. |
| Gebeurtenis serialisatie-indeling |Serialisatie-indeling voor uitvoergegevens.  JSON, CSV en Avro worden ondersteund. |
| Encoding |Voor de CSV en JSON wordt UTF-8 de coderingsindeling Hallo alleen ondersteund op dit moment |
| Scheidingsteken |Alleen van toepassing voor CSV-serialisatie. Stream Analytics ondersteunt een aantal algemene scheidingstekens om gegevens te serialiseren in csv-indeling. Ondersteunde waarden zijn komma, puntkomma, spatie, tab en de verticale balk. |
| Indeling |Alleen van toepassing op JSON-type. Lijn gescheiden geeft aan dat Hallo uitvoer wordt ingedeeld door elk JSON-object dat is gescheiden door een nieuwe regel. Matrix geeft aan dat Hallo uitvoer wordt ingedeeld als een matrix met JSON-objecten. |

## <a name="power-bi"></a>Power BI
[Power BI](https://powerbi.microsoft.com/) kan worden gebruikt als uitvoer voor een Stream Analytics-taak tooprovide voor een uitgebreide visualisatie-ervaring van de resultaten van de analyse. Deze mogelijkheid kan worden gebruikt voor de operationele dashboards, rapporten en metriek aangestuurd reporting.

### <a name="authorize-a-power-bi-account"></a>Een Power BI-account toestaan
1. Als Power BI als uitvoer in hello Azure-portal is geselecteerd, wordt u na vragen aan gebruiker tooauthorize worden een bestaande Power BI-gebruiker of toocreate een nieuw Power BI-account.  
   
   ![Power BI gebruiker autoriseren](./media/stream-analytics-define-outputs/01-stream-analytics-define-outputs.png)  
2. Maak een nieuw account als u niet nog een klik op nu autoriseren.  Een scherm Hallo volgende wordt weergegeven.  
   
   ![Azure-Account Power BI](./media/stream-analytics-define-outputs/02-stream-analytics-define-outputs.png)  
3. In deze stap bieden Hallo werk- of schoolaccount voor het autoriseren hello Power BI-uitvoer. Als u weet al niet aangemeld voor Power BI, kiest u nu Sign up. Hallo kan werk- of schoolaccount account dat u voor Power BI gebruikt afwijken van Hallo account in Azure-abonnement dat u momenteel bent aangemeld.

### <a name="configure-hello-power-bi-output-properties"></a>Hallo Power BI-uitvoereigenschappen configureren
Zodra u Hallo geverifieerde Power BI-account hebt, kunt u Hallo eigenschappen configureren voor uw Power BI-uitvoer. Hallo onderstaande tabel is Hallo lijst met namen van eigenschappen en hun beschrijving tooconfigure uw Power BI-uitvoer.

| De naam van eigenschap | Beschrijving |
| --- | --- |
| Uitvoeraliassen |Dit is een beschrijvende naam die is gebruikt in query's toodirect Hallo query uitvoer toothis Power BI-uitvoer. |
| Groep werkruimte |tooenable gegevens delen met andere gebruikers met Power BI kunt u groepen binnen uw Power BI-account of kies 'Mijn werkruimte' als u niet dat toowrite tooa groep wilt.  Bijwerken van een bestaande groep, vereist Hallo Power BI verificatie vernieuwt. |
| De naam van de gegevensset |Geef de naam van een dataset dat het nodig is voor Power BI Hallo toouse uitvoer |
| De tabelnaam van de |Geef een tabelnaam onder Hallo gegevensset Hallo die Power BI-uitvoer. Op dit moment kan Power BI-uitvoer van de Stream Analytics-taken alleen hebben één tabel in een gegevensset |

Zie voor een overzicht van de configuratie van een Power BI-uitvoer en het dashboard Hallo [Azure Stream Analytics & Power BI](stream-analytics-power-bi-dashboard.md) artikel.

> [!NOTE]
> Expliciet maken geen Hallo gegevensset en de tabel in Hallo Power BI-dashboard. Hallo worden gegevensset en de tabel automatisch ingevuld wanneer Hallo-taak is gestart en Hallo taak gemalen uitvoer naar Power BI begint. Houd er rekening mee dat als Hallo taak query resultaten, Hallo gegevensset niet genereren en de tabel wordt niet gemaakt. Zich bewust te zijn als Power BI al een gegevensset en een tabel met hello dezelfde naam als Hallo één opgegeven in deze Stream Analytics-taak, Hallo bestaande gegevens overschreven.
> 
> 

### <a name="schema-creation"></a>Schema maken
Azure Stream Analytics maakt een Power BI gegevensset en tabel namens de gebruiker Hallo als deze niet al bestaat. In andere gevallen wordt Hallo tabel bijgewerkt met nieuwe waarden. Er is een beperking Hallo die slechts één tabel binnen een dataset kan bestaan.

### <a name="data-type-conversion-from-asa-toopower-bi"></a>Conversie van ASA tooPower BI-gegevenstype
Azure Stream Analytics bijgewerkt Hallo-gegevensmodel dynamisch tijdens runtime als Hallo uitvoer wijzigingen in het schema. Alle worden wijzigingen in de kolom naam, wijzigingen van het type kolom, en Hallo toevoegen of verwijderen van de kolommen bijgehouden.

Deze tabel bevat informatie over de conversie van het gegevenstype Hallo van [Stream Analytics-gegevenstypen](https://msdn.microsoft.com/library/azure/dn835065.aspx) tooPower BIs [typen met Entity Data Model (EDP)](https://powerbi.microsoft.com/documentation/powerbi-developer-walkthrough-push-data/) als een gegevensset met POWER BI en de tabel niet bestaat.


Vanuit Stream Analytics | tooPower BI
-----|-----|------------
bigint | Int64
nvarchar(max) | Tekenreeks
Datum/tijd | Datum/tijd
Float | dubbele
Record matrix | String-type, constante waarde 'Irecords' of 'IArray'

### <a name="schema-update"></a>Schema-Update
Stream Analytics infereert Hallo data modelschema op basis van de eerste reeks gebeurtenissen in de uitvoer van de Hallo Hallo. Later, indien nodig, is Hallo model gegevensschema bijgewerkte tooaccommodate binnenkomende gebeurtenissen die mogelijk niet in de oorspronkelijke schema Hallo passen.

Hallo `SELECT *` query moet worden vermeden tooprevent dynamische schema-update in rijen. Bovendien prestatie van netwerkbestandsscenario toopotential, dit kan ook leiden tot indeterminacy van Hallo tijd voor het Hallo-resultaten. Hallo exacte velden die toobe weergegeven in Power BI-dashboard moeten moeten worden geselecteerd. Bovendien moeten Hallo gegevenswaarden compatibel zijn met Hallo gekozen gegevenstype.


Vorige/huidige | Int64 | Tekenreeks | Datum/tijd | dubbele
-----------------|-------|--------|----------|-------
Int64 | Int64 | Tekenreeks | Tekenreeks | dubbele
dubbele | dubbele | Tekenreeks | Tekenreeks | dubbele
Tekenreeks | Tekenreeks | Tekenreeks | Tekenreeks |  | Tekenreeks | 
Datum/tijd | Tekenreeks | Tekenreeks |  Datum/tijd | Tekenreeks


### <a name="renew-power-bi-authorization"></a>Vernieuwen van Power BI-autorisatie
U moet toore-verificatie van uw Power BI-account als het wachtwoord is gewijzigd sinds de taak is gemaakt of laatst geverifieerd. Als multi-factor Authentication (MFA) is geconfigureerd op de tenant van uw Azure Active Directory (AAD) moet u ook toorenew Power BI autorisatie elke 2 weken. Een symptoom zijn van dit probleem is geen taakuitvoer en een 'verifiëren gebruikersfout' in de Bewerkingslogboeken Hallo:

  ![Power BI vernieuwen fout](./media/stream-analytics-define-outputs/03-stream-analytics-define-outputs.png)  

tooresolve dit probleem op door de actieve taak stoppen en ga tooyour Power BI-uitvoer.  Klik op de koppeling 'Vernieuwen autorisatie' hello en start u de taak van Hallo laatste tijd geëindigd tooavoid gegevens verloren gaan.

  ![Power BI autorisatie vernieuwen](./media/stream-analytics-define-outputs/04-stream-analytics-define-outputs.png)  

## <a name="table-storage"></a>Table Storage
[Azure Table storage](../storage/common/storage-introduction.md) biedt maximaal beschikbare, sterk schaalbare opslag, zodat een toepassing kunt toomeet gebruikersvraag automatisch schalen. Tabelopslag is van Microsoft NoSQL sleutel-/ kenmerkopslag waarvoor een van voor gestructureerde gegevens met minder beperkingen op Hallo-schema gebruikmaken kan. Azure Table storage kan worden gebruikt toostore-gegevens voor de persistentie en efficiënte ophalen.

Hallo in de volgende tabel geeft een lijst Hallo eigenschapnamen en hun beschrijving voor het maken van de tabeluitvoer van een.

| De naam van eigenschap | Beschrijving |
| --- | --- |
| Uitvoeraliassen |Dit is een beschrijvende naam die wordt gebruikt in de query's toodirect Hallo query uitvoer toothis table storage. |
| Storage-Account |Hallo-naam van Hallo storage-account waarin u de uitvoer wilt verzenden. |
| De sleutel van opslagaccount |Hallo-toegangssleutel die is gekoppeld aan Hallo storage-account. |
| De tabelnaam van de |Hallo-naam van Hallo tabel. Hallo tabel gemaakt als deze niet bestaat. |
| Partitiesleutel |Hallo-naam van Hallo uitvoer kolom met Hallo-partitiesleutel. Hallo partitiesleutel is een unieke id voor Hallo partitie binnen een bepaalde tabel dat Hallo eerste deel van de primaire sleutel van een entiteit uitmaakt. Het is een tekenreekswaarde die mogelijk van too1 KB groot. |
| Rijsleutel |Hallo-naam van Hallo uitvoer kolom met Hallo rijsleutel. Hallo rijsleutel is een unieke id voor een entiteit binnen een bepaalde partitie. Het uitmaakt Hallo tweede deel van de primaire sleutel van een entiteit. Hallo rijsleutel is een tekenreekswaarde die mogelijk van too1 KB groot. |
| Batchgrootte |Hallo aantal records voor een batchbewerking. Hallo standaard is meestal voldoende voor de meeste taken, raadpleegt u toohello [tabel batchbewerking spec](https://msdn.microsoft.com/library/microsoft.windowsazure.storage.table.tablebatchoperation.aspx) voor meer informatie over het aanpassen van deze instelling. |

## <a name="service-bus-queues"></a>Service Bus-wachtrijen
[Service Bus-wachtrijen](https://msdn.microsoft.com/library/azure/hh367516.aspx) bieden een First In, eerste Out (FIFO) message delivery tooone of meer concurrerende consumenten. Berichten zijn meestal verwachte toobe ontvangen en verwerkt door de ontvangers Hallo in Hallo-tijdsvolgorde waarin ze zijn toohello wachtrij toegevoegd en elk bericht wordt ontvangen en verwerkt door slechts één berichtconsument.

Hallo in de volgende tabel geeft een lijst Hallo eigenschapnamen en hun beschrijving voor het maken van de uitvoer van een wachtrij.

| De naam van eigenschap | Beschrijving |
| --- | --- |
| Uitvoeraliassen |Dit is een beschrijvende naam die is gebruikt in query's toodirect Hallo query uitvoer toothis Service Bus-wachtrij. |
| Service Bus Namespace |Een Service Bus-naamruimte is een container voor een set berichtentiteiten. |
| De wachtrijnaam van de |de naam van de Hallo Hallo Service Bus-wachtrij. |
| Wachtrij-beleidsnaam |Wanneer u een wachtrij maakt, kunt u ook gedeeld toegangsbeleid maken op Hallo-tabblad wachtrij configureren. Elk gedeeld toegangsbeleid wordt hebben een naam, machtigingen die u instelt en toegangssleutels. |
| Wachtrij beleidssleutel |Hallo toegang tot gedeelde sleutel gebruikt tooauthenticate toegang toohello Service Bus-naamruimte |
| Gebeurtenis serialisatie-indeling |Serialisatie-indeling voor uitvoergegevens.  JSON, CSV en Avro worden ondersteund. |
| Encoding |Voor de CSV en JSON wordt UTF-8 de coderingsindeling Hallo alleen ondersteund op dit moment |
| Scheidingsteken |Alleen van toepassing voor CSV-serialisatie. Stream Analytics ondersteunt een aantal algemene scheidingstekens om gegevens te serialiseren in csv-indeling. Ondersteunde waarden zijn komma, puntkomma, spatie, tab en de verticale balk. |
| Indeling |Alleen van toepassing op JSON-type. Lijn gescheiden geeft aan dat Hallo uitvoer wordt ingedeeld door elk JSON-object dat is gescheiden door een nieuwe regel. Matrix geeft aan dat Hallo uitvoer wordt ingedeeld als een matrix met JSON-objecten. |

## <a name="service-bus-topics"></a>Service Bus-onderwerpen
Terwijl Service Bus-wachtrijen een methode voor clientcommunicatie met één tooone van afzender-tooreceiver bieden [Service Bus-onderwerpen](https://msdn.microsoft.com/library/azure/hh367516.aspx) een een-op-veel-vorm van communicatie bieden.

Hallo in de volgende tabel geeft een lijst Hallo eigenschapnamen en hun beschrijving voor het maken van de tabeluitvoer van een.

| De naam van eigenschap | Beschrijving |
| --- | --- |
| Uitvoeraliassen |Dit is een beschrijvende naam die is gebruikt in query's toodirect Hallo query uitvoer toothis Service Bus-onderwerp. |
| Service Bus Namespace |Een Service Bus-naamruimte is een container voor een set berichtentiteiten. Wanneer u een nieuwe Event Hub hebt gemaakt, hebt u ook een Service Bus-naamruimte gemaakt |
| Onderwerpnaam |Onderwerpen zijn berichtentiteiten entiteiten, vergelijkbare tooevent hubs en wachtrijen. Ze zijn ontworpen toocollect gebeurtenisstromen uit een aantal verschillende apparaten en services. Wanneer u een onderwerp maakt, is het ook een specifieke naam gegeven. Hallo-berichten verzonden tooa onderwerp is alleen beschikbaar als een abonnement is gemaakt, dus zorg ervoor er zijn een of meer abonnementen onder Hallo onderwerp |
| Onderwerp-beleidsnaam |Wanneer u een onderwerp maakt, kunt u ook gedeeld toegangsbeleid maken op Hallo-tabblad onderwerp configureren. Elk gedeeld toegangsbeleid wordt hebben een naam, machtigingen die u instelt en toegangssleutels |
| Onderwerp beleidssleutel |Hallo toegang tot gedeelde sleutel gebruikt tooauthenticate toegang toohello Service Bus-naamruimte |
| Gebeurtenis serialisatie-indeling |Serialisatie-indeling voor uitvoergegevens.  JSON, CSV en Avro worden ondersteund. |
| Encoding |Als CSV- of JSON-indeling, moet een codering worden opgegeven. UTF-8 wordt de coderingsindeling Hallo alleen ondersteund op dit moment |
| Scheidingsteken |Alleen van toepassing voor CSV-serialisatie. Stream Analytics ondersteunt een aantal algemene scheidingstekens om gegevens te serialiseren in csv-indeling. Ondersteunde waarden zijn komma, puntkomma, spatie, tab en de verticale balk. |

## <a name="azure-cosmos-db"></a>Azure Cosmos DB
[Azure Cosmos DB](https://azure.microsoft.com/services/documentdb/) is een volledig beheerde NoSQL-documentdatabaseservice die query en transacties via schemavrije gegevens, voorspelbare en betrouwbare prestaties en snelle ontwikkeling biedt.

Hallo onderstaande lijst details Hallo eigenschapnamen en hun beschrijving voor het maken van een Azure DB die Cosmos-uitvoer.

* **Uitvoer Alias** – een alias toorefer dit uitvoer in uw query ASA  
* **De accountnaam** – Hallo-naam of het eindpunt-URI van Hallo Cosmos-DB-account.  
* **Account van de sleutel** – Hallo gedeelde toegangssleutel voor Hallo Cosmos-DB-account.  
* **Database** – hello Cosmos DB databasenaam.  
* **Verzameling naampatroon** – Hallo verzamelingsnaam of hun patroon voor Hallo verzamelingen toobe gebruikt. indeling van de verzameling Hallo kan worden samengesteld met Hallo optionele {partition}-token, waarbij partities beginnen bij 0. Hieronder vindt u voorbeeld geldige invoer:  
  1\) MyCollection: een verzameling met de naam 'MyCollection' moet aanwezig zijn.  
  2\) MyCollection {partition} – deze verzamelingen moeten bestaan – 'MyCollection0', 'MyCollection1', 'MyCollection2', enzovoort.  
* **Partitie-sleutel** : optioneel. Dit is alleen nodig als u een token {partitie} in het patroon van de naam van verzameling. de naam van de Hallo van Hallo veld in de uitvoer gebeurtenissen die worden gebruikt toospecify Hallo sleutel voor het partitioneren van uitvoer in collecties. Voor één verzameling uitvoer, elke willekeurige uitvoerkolom kan worden gebruikt, bijvoorbeeld PartitionId.  
* **ID-document** : optioneel. Hallo-naam van Hallo veld in uitvoergebeurtenissen gebruikt toospecify Hallo primaire sleutel op welke insert of update bewerkingen zijn gebaseerd.  


## <a name="get-help"></a>Help opvragen
Voor verdere hulp kunt u mogelijk terecht op het [Azure Stream Analytics-forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)

## <a name="next-steps"></a>Volgende stappen
U hebt ingevoerd tooStream Analytics, een beheerde service voor streaminganalyse van gegevens van Hallo Internet der dingen zijn. toolearn meer informatie over deze service, Zie:

* [Aan de slag met Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [Azure Stream Analytics-taken schalen](stream-analytics-scale-jobs.md)
* [Naslaggids voor Azure Stream Analytics Query](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [REST API-naslaggids voor Azure Stream Analytics Management](https://msdn.microsoft.com/library/azure/dn835031.aspx)

<!--Link references-->
[stream.analytics.developer.guide]: ../stream-analytics-developer-guide.md
[stream.analytics.scale.jobs]: stream-analytics-scale-jobs.md
[stream.analytics.introduction]: stream-analytics-introduction.md
[stream.analytics.get.started]: stream-analytics-real-time-fraud-detection.md
[stream.analytics.query.language.reference]: http://go.microsoft.com/fwlink/?LinkID=513299
[stream.analytics.rest.api.reference]: http://go.microsoft.com/fwlink/?LinkId=517301

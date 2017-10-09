---
title: aaaUse hello Azure-opslagemulator voor ontwikkeling en testen | Microsoft Docs
description: een gratis lokale ontwikkelingsomgeving biedt Hello Azure-opslagemulator voor het ontwikkelen en testen van uw Azure Storage-toepassingen. Meer informatie over hoe aanvragen worden geverifieerd, hoe tooconnect toohello emulator van uw toepassing en hoe toouse Hallo opdrachtregelprogramma.
services: storage
documentationcenter: 
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: f480b059-df8a-4a63-b05a-7f2f5d1f5c2a
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/08/2017
ms.author: marsma
ms.openlocfilehash: 42637dcd9f476069e6ecd19ed04e7ed93fe38ff7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-azure-storage-emulator-for-development-and-testing"></a>Hello Azure-opslagemulator gebruiken voor ontwikkeling en testen

Hallo Microsoft Azure-opslagemulator biedt een lokale omgeving waarin hello Azure Blob, wachtrijen en tabellen services voor ontwikkelingsdoeleinden worden geëmuleerd. Hallo-opslagemulator kunt u uw toepassing op Hallo opslagservices lokaal testen zonder te maken van een Azure-abonnement of mogelijke kosten. Wanneer u tevreden bent over hoe uw toepassing in Hallo-emulator werkt, kunt u een Azure storage-account in de cloud Hallo toousing overschakelen.

## <a name="get-hello-storage-emulator"></a>Hallo-opslagemulator ophalen
Hallo-opslagemulator is beschikbaar als onderdeel van Hallo [Microsoft Azure SDK](https://azure.microsoft.com/downloads/). U kunt ook de opslagemulator Hallo installeren met behulp van Hallo [zelfstandig installatieprogramma](https://go.microsoft.com/fwlink/?linkid=717179&clcid=0x409) (directe download). tooinstall hello opslagemulator, u moet beheerdersbevoegdheden hebben op uw computer.

de opslagemulator Hallo momenteel wordt alleen uitgevoerd op Windows. Die u overweegt een opslagemulator voor Linux, één optie Hallo community onderhouden, open-source opslagemulator is [Azurite](https://github.com/arafato/azurite).

> [!NOTE]
> Gegevens die zijn gemaakt in een versie van de opslagemulator Hallo kan niet worden gegarandeerd toobe toegankelijk wanneer u een andere versie. Als u toopersist uw gegevens nodig voor de lange termijn hello, raden wij u die gegevens opslaat in Azure storage-account, in plaats van Hallo-opslagemulator.
> <p/>
> Hallo-opslagemulator is afhankelijk van specifieke versies van Hallo OData-bibliotheken. Hallo OData-dll's die worden gebruikt door de opslagemulator Hallo met andere versies vervangen wordt niet ondersteund en kan leiden tot onverwacht gedrag. Elke versie van de OData ondersteund door Hallo storage-service is echter mogelijk gebruikte toosend aanvragen toohello emulator.
>

## <a name="how-hello-storage-emulator-works"></a>De werking van de opslagemulator Hallo
Hallo-opslagemulator maakt gebruik van een lokaal exemplaar van Microsoft SQL Server en Hallo lokaal bestand system tooemulate Azure storage-services. Hallo-opslagemulator gebruikt standaard een database in Microsoft SQL Server 2012 Express LocalDB. U kunt een lokaal exemplaar van SQL Server in plaats van Hallo LocalDB-exemplaar tooconfigure Hallo storage emulator tooaccess. Zie voor meer informatie, Hallo [begin- en initialisatie Hallo opslagemulator](#start-and-initialize-the-storage-emulator) verderop in dit artikel.

de opslagemulator Hallo verbindt tooSQL Server of LocalDB met Windows-verificatie.

Een paar verschillen in functionaliteit bestaan tussen de opslagemulator hello en Azure storage-services. Zie voor meer informatie over deze verschillen, Hallo [verschillen tussen de opslagemulator hello en Azure Storage](#differences-between-the-storage-emulator-and-azure-storage) verderop in dit artikel.

## <a name="start-and-initialize-hello-storage-emulator"></a>Start en de opslagemulator Hallo initialiseren
toostart hello Azure-opslagemulator:
1. Selecteer Hallo **Start** of drukt u op Hallo **Windows** sleutel.
1. Begint te typen `Azure Storage Emulator`.
1. Selecteer Hallo-emulator in Hallo lijst van toepassingen weergegeven.

Wanneer de opslagemulator hello wordt gestart, verschijnt een opdrachtpromptvenster. U kunt deze console venster toostart en stop Hallo opslagemulator gebruiken, gegevens wissen, status ophalen en initialiseren Hallo-emulator. Zie voor meer informatie, Hallo [Storage emulator opdrachtregelprogramma verwijzing](#storage-emulator-command-line-tool-reference) verderop in dit artikel.

Wanneer het Hallo-emulator wordt uitgevoerd, ziet u een pictogram in systeemvak voor Windows hello.

Wanneer u Hallo storage emulator opdrachtpromptvenster sluit, blijven de opslagemulator hello toorun. toobring up Hallo Opslagemulator consolevenster volg opnieuw Hallo vorige stappen als Hallo opslagemulator wordt gestart.

Hallo wordt u eerste keer Hallo-opslagemulator uitvoert Hallo-omgeving voor lokale opslag geïnitialiseerd voor u. Hallo initialisatieproces maakt een database in LocalDB en HTTP-poorten voor elke service lokale opslag zijn gereserveerd.

Hallo-opslagemulator wordt standaard geïnstalleerd te`C:\Program Files (x86)\Microsoft SDKs\Azure\Storage Emulator`.

> [!TIP]
> U kunt Hallo [Microsoft Azure Storage Explorer](http://storageexplorer.com) toowork met lokale opslagemulatorresources. Zoek naar '(ontwikkeling)' onder 'Opslagaccounts' in de structuur van de resources Opslagverkenner Hallo nadat u hebt geïnstalleerd en gestart Hallo-opslagemulator.
>

### <a name="initialize-hello-storage-emulator-toouse-a-different-sql-database"></a>Hallo storage emulator toouse een andere SQL-database initialiseren
U kunt Hallo storage emulator opdrachtregelprogramma tooinitialize Hallo storage emulator toopoint tooa SQL database-instantie dan Hallo standaard LocalDB-exemplaar gebruiken:

1. Open Hallo Opslagemulator consolevenster zoals beschreven in Hallo [begin- en initialisatie Hallo opslagemulator](#start-and-initialize-the-storage-emulator) sectie.
1. Typ in het consolevenster Hallo, Hallo opdracht, na waar `<SQLServerInstance>` heet Hallo Hallo SQL Server-exemplaar. Geef toouse LocalDB, `(localdb)\MSSQLLocalDb` als Hallo SQL Server-exemplaar.

  `AzureStorageEmulator.exe init /server <SQLServerInstance>`

  U kunt ook Hallo na de opdracht die ervoor zorgt Hallo emulator toouse Hallo standaard SQL Server-exemplaar dat gebruiken:

  `AzureStorageEmulator.exe init /server .\\`

  Of u kunt na de opdracht die wordt opnieuw geïnitialiseerd Hallo database toohello-standaardexemplaar LocalDB Hallo:

  `AzureStorageEmulator.exe init /forceCreate`

Zie voor meer informatie over deze opdrachten [Storage emulator opdrachtregelprogramma verwijzing](#storage-emulator-command-line-tool-reference).

> [!TIP]
> U kunt Hallo [Microsoft SQL Server Management Studio](/sql/ssms/download-sql-server-management-studio-ssms) (SSMS) toomanage uw SQL Server-, inclusief Hallo LocalDB-installatie exemplaren. In Hallo SMSS **verbinding tooServer** dialoogvenster opgeven `(localdb)\MSSQLLocalDb` in Hallo **servernaam:** veld tooconnect toohello LocalDB-exemplaar.

## <a name="authenticating-requests-against-hello-storage-emulator"></a>Verificatie-aanvragen op basis van de opslagemulator Hallo
Nadat u hebt geïnstalleerd en gestart opslagemulator hello, kunt u uw code te vergelijken met het testen. Net als bij Azure Storage in de cloud hello, moet elke aanvraag die u op basis van de opslagemulator Hallo aanbrengt worden geverifieerd, tenzij het een anonieme aanvraag. U kunt aanvragen tegen Hallo opslagemulator met gedeelde sleutel verificatie of met een shared access signature (SAS) verifiëren.

### <a name="authenticate-with-shared-key-credentials"></a>Verifiëren met referenties van de gedeelde sleutel
[!INCLUDE [storage-emulator-connection-string-include](../../includes/storage-emulator-connection-string-include.md)]

Zie voor meer informatie over verbindingsreeksen [configureren Azure Storage-verbindingsreeksen](storage-configure-connection-string.md).

### <a name="authenticate-with-a-shared-access-signature"></a>Verificatie met een shared access signature
Sommige clientbibliotheken van Azure storage, zoals Hallo Xamarin-bibliotheek, is alleen ondersteuning voor verificatie met een shared access signature (SAS)-token. U kunt Hallo SAS-token met behulp van een hulpprogramma zoals Hallo maken [Opslagverkenner](http://storageexplorer.com/) of een andere toepassing die ondersteuning biedt voor verificatie met gedeelde sleutel.

U kunt ook een SAS-token genereren met behulp van Azure PowerShell. Hallo volgende voorbeeld genereert een SAS-token met volledige machtigingen tooa blob-container:

1. Azure PowerShell installeren als u nog niet gedaan hebt (met de nieuwste versie Hallo van hello Azure PowerShell-cmdlets wordt aanbevolen). Zie voor installatie-instructies [installeren en configureren van Azure PowerShell](/powershell/azure/install-azurerm-ps).
2. Open Azure PowerShell en Voer Hallo de volgende opdrachten en vervangt `ACCOUNT_NAME` en `ACCOUNT_KEY==` met uw eigen referenties en `CONTAINER_NAME` met een naam van uw keuze:

```powershell
$context = New-AzureStorageContext -StorageAccountName "ACCOUNT_NAME" -StorageAccountKey "ACCOUNT_KEY=="

New-AzureStorageContainer CONTAINER_NAME -Permission Off -Context $context

$now = Get-Date

New-AzureStorageContainerSASToken -Name CONTAINER_NAME -Permission rwdl -ExpiryTime $now.AddDays(1.0) -Context $context -FullUri
```

Hallo resulterende shared access signature voor URI voor de nieuwe container Hallo moet er ongeveer als:

```
https://storageaccount.blob.core.windows.net/sascontainer?sv=2012-02-12&se=2015-07-08T00%3A12%3A08Z&sr=c&sp=wl&sig=t%2BbzU9%2B7ry4okULN9S0wst%2F8MCUhTjrHyV9rDNLSe8g%3Dsss
```

Hallo shared access signature voor gemaakt met dit voorbeeld is geldig voor één dag. Hallo handtekening verleent tooblobs binnen Hallo container volledige toegang (lezen, schrijven, verwijderen, lijst).

Zie voor meer informatie over handtekeningen voor gedeelde toegang [Using shared access signatures (SAS) in Azure Storage](storage-dotnet-shared-access-signature-part-1.md).

## <a name="addressing-resources-in-hello-storage-emulator"></a>Bronnen in de opslagemulator Hallo adressering
service-eindpunten voor de opslagemulator Hallo Hallo zijn anders dan die van een Azure storage-account. Hallo verschil is omdat de lokale computer Hallo voert geen naamomzetting van het domein vereisen Hallo storage emulator eindpunten toobe lokale adressen.

Wanneer u een resource in Azure storage-account te houden, kunt u gebruiken Hallo schema te volgen. Hallo-accountnaam is onderdeel van Hallo URI-hostnaam en Hallo resource wordt behandeld maakt deel uit van het Hallo-URI-pad:

`<http|https>://<account-name>.<service-name>.core.windows.net/<resource-path>`

Hallo is volgende URI bijvoorbeeld een geldig adres voor een blob in Azure storage-account:

`https://myaccount.blob.core.windows.net/mycontainer/myblob.txt`

Hallo echter opslagemulator, omdat de lokale computer Hallo voert geen Domeinnaamomzetting, Hallo-accountnaam maakt deel uit van de URI-pad in plaats van de hostnaam Hallo Hallo. Hallo URI-notatie voor een resource in de opslagemulator Hallo volgende gebruiken:

`http://<local-machine-address>:<port>/<account-name>/<resource-path>`

Bijvoorbeeld: hello volgende adres kan worden gebruikt voor toegang tot een blob in Hallo-opslagemulator:

`http://127.0.0.1:10000/myaccount/mycontainer/myblob.txt`

service-eindpunten voor de opslagemulator Hallo Hallo zijn:

* BLOB-service:`http://127.0.0.1:10000/<account-name>/<resource-path>`
* Queue-service:`http://127.0.0.1:10001/<account-name>/<resource-path>`
* Tabelservice:`http://127.0.0.1:10002/<account-name>/<resource-path>`

### <a name="addressing-hello-account-secondary-with-ra-grs"></a>Hallo-account met RA-GRS secundaire adressering
Vanaf versie 3.1 is ondersteunt Hallo opslagemulator geografisch redundante replicatie van leestoegang (RA-GRS). Storage-resources in Hallo cloud en in lokale emulator Hallo, u kunt toegang tot de secundaire locatie Hallo door voegen - accountnaam secundaire toohello. Hallo volgende adres kan bijvoorbeeld worden gebruikt voor toegang tot een blob met behulp van de secundaire alleen-lezen Hallo in Hallo opslagemulator:

`http://127.0.0.1:10000/myaccount-secondary/mycontainer/myblob.txt`

> [!NOTE]
> Gebruik voor toegang op programmeerniveau toohello secundaire met opslagemulator hello, Hallo Storage-clientbibliotheek voor .NET versie 3.2 of hoger. Zie Hallo [Microsoft Azure Storage-clientbibliotheek voor .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx) voor meer informatie.
>
>

## <a name="storage-emulator-command-line-tool-reference"></a>Naslaginformatie over Storage emulator opdrachtregelprogramma
Vanaf versie 3.0 biedt wordt een consolevenster weergegeven wanneer u Hallo Opslagemulator start. Hallo-opdrachtregel in Hallo console venster toostart en stop Hallo-emulator, evenals een query voor de status van gebruik en andere bewerkingen uitvoeren.

> [!NOTE]
> Als u Hallo Microsoft Azure-rekenemulator geïnstalleerd hebt, wordt een pictogram in systeemvak voor system weergegeven als u Hallo Opslagemulator starten. Met de rechtermuisknop op Hallo pictogram tooreveal een menu waarmee een grafisch toostart en stop de Hallo-Opslagemulator.
>
>

### <a name="command-line-syntax"></a>De syntaxis van de opdrachtregel
`AzureStorageEmulator.exe [start] [stop] [status] [clear] [init] [help]`

### <a name="options"></a>Opties
tooview hello lijst met opties, type `/help` achter de opdrachtprompt Hallo.

| Optie | Beschrijving | Opdracht | Argumenten |
| --- | --- | --- | --- |
| **Beginnen** |Hallo-opslagemulator wordt opgestart. |`AzureStorageEmulator.exe start [-inprocess]` |*-inprocess*: Hallo emulator te starten in de huidige proces Hallo in plaats van een nieuw proces maken. |
| **Stoppen** |Stopt Hallo-opslagemulator. |`AzureStorageEmulator.exe stop` | |
| **Status** |Afdrukken bestellen Hallo status van de opslagemulator Hallo. |`AzureStorageEmulator.exe status` | |
| **Wissen** |Hallo-gegevens in alle services die zijn opgegeven op de opdrachtregel Hallo wist. |`AzureStorageEmulator.exe clear [blob] [table] [queue] [all]                                                    ` |*BLOB*: wist blob-gegevens. <br/>*wachtrij*: wist wachtrijgegevens. <br/>*tabel*: tabelgegevens worden gewist. <br/>*alle*: alle gegevens in alle services worden gewist. |
| **Init** |Voert eenmalig initialisatie tooset up Hallo-emulator. |<code>AzureStorageEmulator.exe init [-server serverName] [-sqlinstance instanceName] [-forcecreate&#124;-skipcreate] [-reserveports&#124;-unreserveports] [-inprocess]</code> |*-server Servernaam\exemplaarnaam*: Hiermee geeft u Hallo-server die als host fungeert voor de SQL-exemplaar Hallo. <br/>*-sqlinstance instanceName*: Hiermee geeft u de naam Hallo van Hallo SQL-exemplaar toobe gebruikt in een standaardexemplaar Hallo van server. <br/>*-forcecreate*: forceert de creatie van Hallo SQL-database, zelfs als deze al bestaat. <br/>*-skipcreate*: maken van Hallo SQL-database wordt overgeslagen. Dit heeft voorrang boven - forcecreate.<br/>*-reserveports*: probeert tooreserve Hallo HTTP-poorten die zijn gekoppeld aan het Hallo-services.<br/>*-unreserveports*: probeert tooremove reserveringen voor Hallo HTTP-poorten die zijn gekoppeld aan het Hallo-services. Dit heeft voorrang boven - reserveports.<br/>*-inprocess*: initialisatie uitvoert in de huidige proces Hallo in plaats van een nieuw proces te starten. het huidige proces Hallo moet worden gestart met verhoogde machtigingen als poort reserveringen wilt wijzigen. |

## <a name="differences-between-hello-storage-emulator-and-azure-storage"></a>Verschillen tussen de opslagemulator hello en Azure Storage
Omdat de opslagemulator Hallo een geëmuleerde omgeving uitgevoerd in een lokale SQL-exemplaar is, moet u er verschillen in functionaliteit tussen Hallo-emulator en een Azure storage-account in de cloud Hallo zijn:

* de opslagemulator Hallo ondersteunt slechts één vaste account en een bekende verificatiesleutel.
* Hallo-opslagemulator is geen service van schaalbare opslag en biedt geen ondersteuning voor een groot aantal gelijktijdige clients.
* Zoals beschreven in [adressering bronnen in de opslagemulator hello](#addressing-resources-in-the-storage-emulator), resources anders in de opslagemulator Hallo ten opzichte van een Azure storage-account worden behandeld. Dit verschil is omdat de domein-naamomzetting is beschikbaar in Hallo cloud, maar niet op Hallo lokale computer.
* Vanaf versie 3.1 is ondersteunt Hallo emulator opslagaccount geografisch redundante replicatie van leestoegang (RA-GRS). Alle accounts hebt ingeschakeld voor de RA-GRS in Hallo-emulator en er is nooit een vertraging tussen Hallo primaire en secundaire replica's. Hallo statistieken voor Blob-Service ophalen en statistieken van Queue-Service ophalen tabelstatistieken Service ophalen bewerkingen worden ondersteund op secundaire Hallo-account en wordt altijd retourwaarde Hallo Hallo `LastSyncTime` antwoord element als de huidige tijd volgens toohello onderliggende hello SQL-database.
* Hallo File-service en service-eindpunten voor SMB-protocol worden momenteel niet ondersteund in Hallo-opslagemulator.
* Als u een versie van de opslagservices Hallo die nog niet wordt ondersteund door de emulator Hallo gebruikt, geeft de opslagemulator Hallo een VersionNotSupportedByEmulator-fout (HTTP-statuscode 400 - Ongeldige aanvraag).

### <a name="differences-for-blob-storage"></a>Verschillen voor Blob-opslag
Hallo verschillen na tooBlob opslag in de emulator Hallo van toepassing:

* Hallo-opslagemulator biedt alleen ondersteuning voor blob-grootten van too2 GB.
* Incrementele kopie kunt momentopnamen van blobs overschreven-toobe gekopieerd, die een fout op Hallo-service retourneert.
* Get-paginabereiken Diff werkt niet tussen gekopieerd incrementele kopie Blob met momentopnamen.
* Een Blob Put-bewerking kan op basis van een blob of aanwezig is op de opslagemulator Hallo met een actieve lease slaagt, zelfs als Hallo lease-ID niet in Hallo-aanvraag opgegeven is.
* Toevoeg-Blob bewerkingen worden niet ondersteund door Hallo-emulator. Poging een bewerking op een toevoeg-blob resulteert in een FeatureNotSupportedByEmulator-fout (HTTP-statuscode 400 - Ongeldige aanvraag).

### <a name="differences-for-table-storage"></a>Verschillen voor Table storage
Hallo verschillen na tooTable opslag in de emulator Hallo van toepassing:

* Datumeigenschappen in tabel-service in de opslagemulator Hallo Hallo ondersteunen alleen Hallo bereik dat wordt ondersteund door SQL Server 2005 (ze zijn vereist toobe hoger is dan 1 januari 1753). Alle datums vóór 1 januari 1753 zijn gewijzigd toothis waarde. Hallo precisie van de datums is beperkt toohello precisie van de SQL Server 2005, wat betekent dat datums nauwkeurige too1 zijn/300th van een seconde.
* Hallo-opslagemulator biedt ondersteuning voor partitie sleutel sleuteleigenschap rijwaarden van minder dan 512 bytes. Bovendien Hallo totale grootte van Hallo-accountnaam, tabelnaam en de namen van de sleuteleigenschap samen kan niet langer zijn dan 900 bytes.
* totale grootte van een rij in een tabel in de opslagemulator Hallo Hallo is beperkt tooless dan 1 MB.
* Typ in het Hallo-opslagemulator eigenschappen van gegevens `Edm.Guid` of `Edm.Binary` ondersteuning alleen Hallo `Equal (eq)` en `NotEqual (ne)` vergelijkingsoperators in query filteren tekenreeksen.

### <a name="differences-for-queue-storage"></a>Verschillen voor Queue storage
Er zijn geen specifieke tooQueue verschillen opslag in Hallo-emulator.

## <a name="storage-emulator-release-notes"></a>Opmerkingen bij de release van de opslag-emulator
### <a name="version-52"></a>Versie 5.2
* Hallo-opslagemulator ondersteunt nu versie 2017-04-17 van Hallo storage-services voor blobs, wachtrijen en tabellen service-eindpunten.
* Een fout vastgesteld waar tabel eigenschapswaarden zijn niet wordt correct gecodeerd.

### <a name="version-51"></a>Versie 5.1
* Een bug vast waar de opslagemulator Hallo Hallo heeft geretourneerd `DataServiceVersion` header in sommige antwoorden waar Hallo-service niet is.

### <a name="version-50"></a>Versie 5.0
* Hallo storage emulator installatieprogramma controleert niet langer voor bestaande MSSQL en .NET Framework wordt geïnstalleerd.
* Hallo storage emulator installatieprogramma maakt niet langer Hallo-database als onderdeel van de installatie. Database wordt nog steeds gemaakt, indien nodig tijdens het opstarten.
* Database maken niet meer vereist bevoegdheden.
* Poort reserveringen zijn niet langer nodig voor opstarten.
* Hallo opties te volgen voegt`init`: `-reserveports` (hogere nodig is), `-unreserveports` (hogere nodig is), `-skipcreate`.
* Hallo Storage Emulator UI optie op een pictogram in systeemvak voor Hallo system nu start Hallo-opdrachtregelinterface. Hallo oude GUI is niet meer beschikbaar.
* Sommige DLL's zijn verwijderd of hernoemd.

### <a name="version-46"></a>Versie 4.6
* Hallo-opslagemulator ondersteunt nu versie 2016-05-31 van Hallo storage-services voor blobs, wachtrijen en tabellen service-eindpunten.

### <a name="version-45"></a>Versie 4.5
* Heeft een fout die initialisatie en de installatie van Hallo storage emulator toofail veroorzaakt wanneer Hallo back-ups maken van database is gewijzigd.

### <a name="version-44"></a>4.4-versie
* Hallo-opslagemulator ondersteunt nu versie 2015-12-11 van Hallo storage-services voor blobs, wachtrijen en tabellen service-eindpunten.
* Hallo is van de opslagemulator garbagecollection van blob-gegevens nu veel efficiënter wanneer omgaan met een groot aantal blobs.
* Een bug waardoor container ACL XML toobe iets anders gevalideerd vanuit hoe Hallo storage-service deze biedt vast.
* Een bug vast die soms veroorzaakt max en min datum/tijd-waarden toobe gerapporteerd in de verkeerde tijdzone Hallo.

### <a name="version-43"></a>Versie 4.3
* Hallo-opslagemulator ondersteunt nu versie 2015-07-08 van Hallo storage-services voor blobs, wachtrijen en tabellen service-eindpunten.

### <a name="version-42"></a>Versie 4.2
* Hallo-opslagemulator ondersteunt nu versie 2015-04-05 van Hallo storage-services voor blobs, wachtrijen en tabellen service-eindpunten.

### <a name="version-41"></a>Versie 4.1
* de opslagemulator Hallo ondersteunt nu versie 2015-02-21 van opslagservices Hallo op Blob, wachtrijen en tabellen service-eindpunten, met uitzondering van Hallo nieuwe toevoeg-Blob-functies.
* Als u een versie van de opslagservices Hallo die nog niet wordt ondersteund door de emulator Hallo gebruikt, stuurt het Hallo-emulator zinvolle foutbericht. U wordt aangeraden de nieuwste versie Hallo van Hallo-emulator. Als er een fout VersionNotSupportedByEmulator (HTTP-statuscode 400 - Ongeldige aanvraag) optreden, download de meest recente versie van de opslagemulator Hallo Hallo.
* Een fout vastgesteld waarin een race condition veroorzaakt tabel entiteit gegevens toobe onjuist bij gelijktijdige merge-bewerkingen.

### <a name="version-40"></a>Versie 4.0
* Hallo-opslagemulator uitvoerbare te heeft gekregen*AzureStorageEmulator.exe*.

### <a name="version-32"></a>Versie 3.2
* Hallo-opslagemulator biedt nu ondersteuning voor versie 2014-02-14 van opslagservices Hallo voor Blob, wachtrijen en tabellen service-eindpunten. Service-eindpunten die bestand zijn momenteel niet ondersteund in Hallo-opslagemulator. Zie [versiebeheer voor hello Azure Storage-Services](/rest/api/storageservices/Versioning-for-the-Azure-Storage-Services) voor meer informatie over versie 2014-02-14.

### <a name="version-31"></a>Versie 3.1
* Geografisch redundante opslag met leestoegang (RA-GRS) wordt nu ondersteund in Hallo-opslagemulator. Hallo ophalen van Blob-Service statistieken, statistieken voor Queue-Service ophalen en ophalen van tabel statistieken API's worden ondersteund voor secundaire Hallo-account en wordt altijd retourwaarde Hallo van Hallo LastSyncTime antwoord element Hallo volgens toohello van huidige tijd de onderliggende SQL de database. Gebruik voor toegang op programmeerniveau toohello secundaire met opslagemulator hello, Hallo Storage-clientbibliotheek voor .NET versie 3.2 of hoger. Zie Hallo Microsoft Azure Storage-clientbibliotheek voor .NET-verwijzing voor meer informatie.

### <a name="version-30"></a>Versie 3.0
* Hello Azure-opslagemulator is niet langer in hetzelfde als rekenemulator Hallo pakket Hallo verzonden.
* Hallo storage emulator grafische gebruikersinterface is vervangen door een scriptbare opdrachtregelinterface. Zie voor informatie over de opdrachtregelinterface hello, Storage Emulator Naslaggids hulpprogramma. Hallo grafische interface toobe aanwezig is in versie 3.0 wordt voortgezet, maar kan alleen worden benaderd wanneer Hallo Compute-Emulator is geïnstalleerd door met de rechtermuisknop op het pictogram in systeemvak voor Hallo system en Storage Emulator UI weergeven.
* Versie 2013-08-15 van hello Azure storage-services wordt nu volledig ondersteund. (Deze versie is eerder alleen ondersteund door de Opslagemulator versie 2.2.1 Preview.)

## <a name="next-steps"></a>Volgende stappen

* Hallo op verschillende platforms en community onderhouden open-source opslagemulator evalueren [Azurite](https://github.com/arafato/azurite). 
* [Voorbeelden van Azure Storage met .NET](storage-samples-dotnet.md) koppelingen tooseveral codevoorbeelden kunt u bij het ontwikkelen van uw toepassing bevat.
* U kunt Hallo [Microsoft Azure Storage Explorer](http://storageexplorer.com) toowork met resources in uw cloud-opslagaccount en in Hallo-opslagemulator.

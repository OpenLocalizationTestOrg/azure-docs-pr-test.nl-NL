---
title: een gesplitste samenvoegen service aaaDeploy | Microsoft Docs
description: Splitsen en samenvoegen met hulpprogramma's voor elastische database
services: sql-database
documentationcenter: 
author: ddove
manager: jhubbard
editor: 
ms.assetid: 9a993c0f-7052-46cd-aa59-073bea8d535a
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: 6fef641cbc1e73ce34a851c53298a072dade8f9d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-split-merge-service"></a>Een service voor splitsen en samenvoegen implementeren
Hallo gesplitste samenvoegen hulpprogramma kunt u gegevens verplaatsen tussen shard-databases. Zie [verplaatsen van gegevens tussen cloud uitgebreide databases](sql-database-elastic-scale-overview-split-and-merge.md)

## <a name="download-hello-split-merge-packages"></a>Hallo gesplitste samenvoegen pakketten downloaden
1. Hallo nieuwste NuGet versie downloaden van [NuGet](http://docs.nuget.org/docs/start-here/installing-nuget).
2. Open een opdrachtprompt en navigeer toohello map waar u nuget.exe hebt gedownload. Hallo download bevat PowerShell commmands.
3. Hallo nieuwste gesplitste samenvoegen pakket in de huidige map Hallo Hello onder opdracht downloaden:
   ```
   nuget install Microsoft.Azure.SqlDatabase.ElasticScale.Service.SplitMerge
   ```  

Hallo-bestanden worden geplaatst in een map met de naam **Microsoft.Azure.SqlDatabase.ElasticScale.Service.SplitMerge.x.x.xxx.x** waar *x.x.xxx.x* Hallo versienummer weerspiegelt. Hallo gesplitste samenvoegen Service-bestanden niet vinden in Hallo **content\splitmerge\service** onderliggende map en Hallo gesplitste samenvoegen PowerShell-scripts (en vereiste client-dll's) in Hallo **content\splitmerge\powershell** onderliggende map.

## <a name="prerequisites"></a>Vereisten
1. Maak een Azure SQL DB-database die wordt gebruikt als Hallo gesplitste samenvoegen status database. Ga toohello [Azure-portal](https://portal.azure.com). Maak een nieuwe **SQL-Database**. Hallo-database van een naam geven en maak een nieuwe beheerder en het wachtwoord. Worden ervoor toorecord Hallo naam en het wachtwoord voor later gebruik.
2. Zorg ervoor dat de server van uw Azure SQL DB Azure Services tooconnect tooit toestaat. In Hallo Hallo Portal **firewallinstellingen**, zorg ervoor dat Hallo **tooAzure-Services toegang toestaan** ingesteld te**op**. Klik op Hallo 'opgeslagen'-pictogram.
   
   ![Toegestane services][1]
3. Maak een Azure Storage-account dat wordt gebruikt voor diagnostische uitvoer. Ga toohello Azure-Portal. Klik in de linkerbalk Hallo op **nieuw**, klikt u op **gegevens en opslag**, klikt u vervolgens **opslag**.
4. Maak een Azure Cloud Service die uw service gesplitste Merge bevat.  Ga toohello Azure-Portal. Klik in de linkerbalk Hallo op **nieuw**, vervolgens **Compute**, **Cloudservice**, en **maken**. 

## <a name="configure-your-split-merge-service"></a>Configureer uw service gesplitste samenvoegen
### <a name="split-merge-service-configuration"></a>Configuratie gesplitste Merge-service
1. Hallo map waar u Hallo gesplitste samenvoegen assembly's hebt gedownload, maakt u een kopie van Hallo **ServiceConfiguration.Template.cscfg** -bestand dat naast verzonden **SplitMergeService.cspkg** en wijzig de naam **ServiceConfiguration.cscfg**.
2. Open **ServiceConfiguration.cscfg** in een teksteditor zoals Visual Studio die invoer zoals Hallo-indeling van certificaatvingerafdrukken valideert.
3. Een nieuwe database maken of kies een bestaande database tooserve als Hallo status database voor gesplitste samenvoegbewerkingen en Hallo verbindingsreeks van de database ophalen. 
   
   > [!IMPORTANT]
   > Op dit moment gebruik Hallo status database Hallo Latijnse sortering (SQL\_Latin1\_algemene\_CP1\_CI\_AS). Zie voor meer informatie [Windows Collation Name (Transact-SQL)](https://msdn.microsoft.com/library/ms188046.aspx).
   >

   Met Azure SQL DB heeft Hallo verbindingsreeks doorgaans Hallo vorm:
      ```
      Server=myservername.database.windows.net; Database=mydatabasename;User ID=myuserID; Password=mypassword; Encrypt=True; Connection Timeout=30
      ```

4. Deze verbindingsreeks invoeren in Hallo cscfg-bestand in beide Hallo **SplitMergeWeb** en **SplitMergeWorker** rol secties in Hallo ElasticScaleMetadata instelling.
5. Voor Hallo **SplitMergeWorker** rol, voer een geldige verbinding tekenreeks tooAzure opslag voor Hallo **WorkerRoleSynchronizationStorageAccountConnectionString** instelling.

### <a name="configure-security"></a>Beveiliging configureren
Raadpleeg voor gedetailleerde instructies tooconfigure Hallo beveiliging van de service Hallo toohello [gesplitste samenvoegen Beveiligingsconfiguratie](sql-database-elastic-scale-split-merge-security-configuration.md).

Een minimale set van configuratie stappen worden uitgevoerd voor Hallo toepassing van een eenvoudige test-implementatie voor deze zelfstudie wordt tooget Hallo service up-to-date en worden uitgevoerd. Deze stappen alleen Hallo één machine/account inschakelen deze toocommunicate met Hallo service uitvoert.

### <a name="create-a-self-signed-certificate"></a>Een zelfondertekend certificaat maken
Maak een nieuwe map en van deze directory execute Hallo volgende opdracht met behulp van een [opdrachtprompt voor ontwikkelaars voor Visual Studio](http://msdn.microsoft.com/library/ms229859.aspx) venster:

   ```
    makecert ^
    -n "CN=*.cloudapp.net" ^
    -r -cy end -sky exchange -eku "1.3.6.1.5.5.7.3.1,1.3.6.1.5.5.7.3.2" ^
    -a sha1 -len 2048 ^
    -sr currentuser -ss root ^
    -sv MyCert.pvk MyCert.cer
   ```

U wordt gevraagd een wachtwoord tooprotect Hallo persoonlijke sleutel. Voer een sterk wachtwoord in en Bevestig het. U wordt gevraagd voor Hallo wachtwoord toobe zodra er meer daarna gebruikt. Klik op **Ja** op Hallo end tooimport het toohello vertrouwde Certification Authorities basisarchief.

### <a name="create-a-pfx-file"></a>Een PFX-bestand maken
Uitvoeren van de volgende opdracht uit Hallo Hallo hetzelfde venster waar makecert is uitgevoerd. Gebruik Hallo hetzelfde wachtwoord dat u gebruikt toocreate Hallo certificaat:

    pvk2pfx -pvk MyCert.pvk -spc MyCert.cer -pfx MyCert.pfx -pi <password>

### <a name="import-hello-client-certificate-into-hello-personal-store"></a>Hallo-clientcertificaat importeren in het persoonlijke archief Hallo
1. Dubbelklik in Windows Verkenner op **MyCert.pfx**.
2. In Hallo **Wizard Certificaat importeren** Selecteer **huidige gebruiker** en klik op **volgende**.
3. Hallo-bestandspad bevestigen en klikt u op **volgende**.
4. Geef het wachtwoord hello, laat de eigenschap **alle uitgebreide eigenschappen bevatten** gecontroleerd en klikt u op **volgende**.
5. Laat **certificaatarchief automatisch Selecteer Hallo [...]**  gecontroleerd en klikt u op **volgende**.
6. Klik op **voltooien** en **OK**.

### <a name="upload-hello-pfx-file-toohello-cloud-service"></a>Toohello cloudservice voor Hallo PFX-bestand uploaden
1. Ga toohello [Azure Portal](https://portal.azure.com).
2. Selecteer **Cloudservices**.
3. Selecteer Hallo cloudservice die u hierboven hebt gemaakt voor Hallo gesplitste/Merge-service.
4. Klik op **certificaten** in het bovenste menu Hallo.
5. Klik op **uploaden** in de balk onderaan Hallo.
6. Selecteer Hallo PFX-bestand en Voer Hallo hetzelfde wachtwoord als hierboven.
7. Als voltooid, kopiëren van de certificaatvingerafdruk Hallo van Hallo nieuw item in de lijst Hallo.

### <a name="update-hello-service-configuration-file"></a>Hallo serviceconfiguratiebestand bijwerken
Vingerafdruk van het certificaat plakken Hallo gekopieerd hierboven in Hallo vingerafdrukwaarde/kenmerk van deze instellingen.
Voor de werkrol Hallo:
   ```
    <Setting name="DataEncryptionPrimaryCertificateThumbprint" value="" />
    <Certificate name="DataEncryptionPrimary" thumbprint="" thumbprintAlgorithm="sha1" />
   ```

Voor de Webrol Hallo:

   ```
    <Setting name="AdditionalTrustedRootCertificationAuthorities" value="" />
    <Setting name="AllowedClientCertificateThumbprints" value="" />
    <Setting name="DataEncryptionPrimaryCertificateThumbprint" value="" />
    <Certificate name="SSL" thumbprint="" thumbprintAlgorithm="sha1" />
    <Certificate name="CA" thumbprint="" thumbprintAlgorithm="sha1" />
    <Certificate name="DataEncryptionPrimary" thumbprint="" thumbprintAlgorithm="sha1" />
   ```

Houd er rekening mee dat voor implementaties in afzonderlijke certificaten moeten worden gebruikt voor de CA, Hallo voor versleuteling, Hallo servercertificaat en clientcertificaten. Zie voor gedetailleerde instructies voor dit [Beveiligingsconfiguratie](sql-database-elastic-scale-split-merge-security-configuration.md).

## <a name="deploy-your-service"></a>Uw service implementeren
1. Ga toohello [Azure-portal](https://manage.windowsazure.com).
2. Klik op Hallo **Cloudservices** tabblad aan de linkerkant hello, en selecteer Hallo cloudservice die u eerder hebt gemaakt.
3. Klik op **Dashboard**.
4. Kies Hallo staging-omgeving en klik vervolgens op **uploaden van een nieuwe implementatie van de staging**.
   
   ![Fasering][3]
5. Voer in het dialoogvenster hello, een implementatielabel. Klik voor 'Pakket' en 'Configuration', 'Van Local' en kies Hallo **SplitMergeService.cspkg** bestands- en uw cscfg-bestand dat u eerder hebt geconfigureerd.
6. Zorg ervoor dat Hallo selectievakje **toch implementeren als een of meer rollen met één exemplaar** is ingeschakeld.
7. Klik op Hallo maatstreepjes button in Hallo onderkant rechts toobegin Hallo implementatie. Verwacht tootake toocomplete met een paar minuten.

   ![Uploaden][4]

## <a name="troubleshoot-hello-deployment"></a>Hallo-implementatie oplossen
Als uw Webrol toocome online is mislukt, is het waarschijnlijk een probleem met Hallo beveiligingsconfiguratie. Controleer dat Hallo die SSL is geconfigureerd zoals hierboven is beschreven.

Als uw werkrol toocome online mislukt, maar de Webrol lukt, is het waarschijnlijk een probleem met de verbinding toohello status database die u eerder hebt gemaakt.

* Zorg ervoor dat de verbindingsreeks Hallo in uw cscfg nauwkeurig is.
* Controleer dat Hallo-server en database bestaan en dat het Hallo-gebruikersnaam en wachtwoord correct zijn.
* Voor Azure SQL DB moet de verbindingsreeks Hallo Hallo vorm:

   ```  
   Server=myservername.database.windows.net; Database=mydatabasename;User ID=myuserID; Password=mypassword; Encrypt=True; Connection Timeout=30
   ```

* Zorg ervoor dat servernaam Hallo begint niet met **https://**.
* Zorg ervoor dat de server van uw Azure SQL DB Azure Services tooconnect tooit toestaat. toodo, https://manage.windowsazure.com open, op 'SQL-Databases' Hallo links, klikt u op 'Servers' hello boven, en selecteer uw server. Klik op **configureren** op Hallo bovenste en ervoor te zorgen dat Hallo **Azure Services** ingesteld te 'Ja'. (Zie vereisten Hallo sectie Hallo boven aan dit artikel).

## <a name="test-hello-service-deployment"></a>Hallo-service-implementatie testen
### <a name="connect-with-a-web-browser"></a>Verbinding maken met een webbrowser
Hallo-web-eindpunt van uw service gesplitste samenvoegen bepalen. U kunt dit vinden in Hallo klassieke Azure-Portal door te gaan toohello **Dashboard** van uw cloudservice en zoeken onder **Site-URL** aan de rechterkant Hallo. Vervang **http://** met **https://** omdat standaardbeveiligingsinstellingen Hallo Hallo HTTP-eindpunt uitschakelen. Hallo-pagina voor deze URL worden geladen in uw browser.

### <a name="test-with-powershell-scripts"></a>Testen met PowerShell-scripts
Hallo-implementatie en uw omgeving kunnen worden getest door het uitvoeren van de voorbeeldscripts PowerShell Hallo opgenomen.

Hallo scriptbestanden opgenomen zijn:

1. **SetupSampleSplitMergeEnvironment.ps1** -stelt u een test-gegevenslaag voor gesplitste/Merge (Zie onderstaande tabel voor een gedetailleerde beschrijving)
2. **ExecuteSampleSplitMerge.ps1** -test-bewerkingen op Hallo test wordt uitgevoerd gegevens servicetier (Zie onderstaande tabel voor een gedetailleerde beschrijving)
3. **GetMappings.ps1** - site op het hoogste voorbeeldscript die de huidige status Hallo van Hallo shard toewijzingen wordt afgedrukt.
4. **ShardManagement.psm1** -helper-script dat verpakt Hallo ShardManagement API
5. **SqlDatabaseHelpers.psm1** -helper-script voor het maken en beheren van de SQL-databases
   
   <table style="width:100%">
     <tr>
       <th>PowerShell-bestand</th>
       <th>Stappen</th>
     </tr>
     <tr>
       <th rowspan="5">SetupSampleSplitMergeEnvironment.ps1</th>
       <td>1.    Hiermee maakt u een manager-database van de shard-kaart</td>
     </tr>
     <tr>
       <td>2.    2 shard-databases maakt.
     </tr>
     <tr>
       <td>3.    Maakt een shard-toewijzing voor deze database (verwijdert alle bestaande shard op die databases toegewezen). </td>
     </tr>
     <tr>
       <td>4.    Maakt een kleine voorbeeldtabel in beide Hallo shards en vult Hallo-tabel in een Hallo shards.</td>
     </tr>
     <tr>
       <td>5.    Verklaart Hallo SchemaInfo voor Hallo shard-tabel.</td>
     </tr>
   </table>
   <table style="width:100%">
     <tr>
       <th>PowerShell-bestand</th>
       <th>Stappen</th>
     </tr>
   <tr>
       <th rowspan="4">ExecuteSampleSplitMerge.ps1 </th>
       <td>1.    Een gesplitste aanvraag toohello gesplitste samenvoegen Service web front, die half Hallo gegevens van Hallo eerste shard toohello tweede shard splitst verzendt.</td>
     </tr>
     <tr>
       <td>2.    Polls Hallo web frontend voor Hallo gesplitste aanvraagstatus en wacht totdat het Hallo-aanvraag is voltooid.</td>
     </tr>
     <tr>
       <td>3.    Verzendt een merge aanvraag toohello gesplitste samenvoegen Service web front, die Hallo gegevens vanuit het Hallo tweede shard back toohello eerste shard verplaatst.</td>
     </tr>
     <tr>
       <td>4.    Polls Hallo web frontend voor Hallo samenvoegen aanvraagstatus en wordt er gewacht totdat het Hallo-aanvraag is voltooid.</td>
     </tr>
   </table>
   
## <a name="use-powershell-tooverify-your-deployment"></a>Gebruik PowerShell tooverify uw implementatie
1. Open een nieuw PowerShell-venster en navigeer toohello map waar u Hallo gesplitste samenvoegen pakket hebt gedownload en navigeer vervolgens naar Hallo 'powershell' directory.
2. Maak een Azure SQL database-server (of kies een bestaande server) waar Hallo shard-toewijzing manager en shards wordt gemaakt.
   
   > [!NOTE]
   > Hallo SetupSampleSplitMergeEnvironment.ps1 script maakt alle deze databases op Hallo dezelfde server door tookeep Hallo Standaardscript eenvoudig. Dit is geen beperking Hallo gesplitste samenvoegen Service zelf.
   >
   
   Een SQL-verificatie-aanmelding met lezen/schrijven toegang toohello die databases voor Hallo gesplitste Merge-servicegegevens toomove en updatetoewijzing hello shard vereist. Aangezien Hallo gesplitste Merge-Service wordt uitgevoerd in de cloud Hallo, ondersteunt het momenteel geen geïntegreerde verificatie.
   
   Controleer of hello Azure SQL-server is geconfigureerd tooallow toegang van Hallo IP-adres van deze scripts Hallo machine. U vindt deze instelling onder hello Azure SQL-server / configuration / IP-adressen toegestaan.
3. Hallo SetupSampleSplitMergeEnvironment.ps1 script toocreate Hallo Voorbeeldomgeving uitvoeren.
   
   Dit script uitvoert wordt wissen uit een bestaande shard management kaartgegevens structuren op Hallo shard kaart manager-database en Hallo shards. Het wellicht handig toorerun Hallo script desgewenst toore initialiseren Hallo shard-kaart of shards.
   
   Voorbeeld-opdrachtregel:

   ```   
     .\SetupSampleSplitMergeEnvironment.ps1 
   
         -UserName 'mysqluser' 
         -Password 'MySqlPassw0rd' 
         -ShardMapManagerServerName 'abcdefghij.database.windows.net'
   ```      
4. Hallo Getmappings.ps1 tooview Hallo scripttoewijzingen die momenteel aanwezig zijn in Hallo Voorbeeldomgeving uitvoeren.
   
   ```
     .\GetMappings.ps1 
   
         -UserName 'mysqluser' 
         -Password 'MySqlPassw0rd' 
         -ShardMapManagerServerName 'abcdefghij.database.windows.net'

   ```         
5. Hallo ExecuteSampleSplitMerge.ps1 script tooexecute een splitsbewerking (half Hallo gegevens verplaatst naar een Hallo eerste shard toohello tweede shard) en vervolgens een merge-bewerking (Hallo gegevens terug verplaatsen naar de eerste shard Hallo) worden uitgevoerd. Als u SSL- en http-eindpunt links Hallo uitgeschakeld hebt geconfigureerd, zorg er dan Hallo https:// eindpunt te gebruiken.
   
   Voorbeeld-opdrachtregel:

   ```   
     .\ExecuteSampleSplitMerge.ps1
   
         -UserName 'mysqluser' 
         -Password 'MySqlPassw0rd' 
         -ShardMapManagerServerName 'abcdefghij.database.windows.net' 
         -SplitMergeServiceEndpoint 'https://mysplitmergeservice.cloudapp.net' 
         -CertificateThumbprint '0123456789abcdef0123456789abcdef01234567'
   ```      
   
   Als u Hallo hieronder fout ontvangt, is het zeer waarschijnlijk een probleem met het certificaat van uw Web-eindpunt. Probeer verbinding te maken toohello Web-eindpunt met uw favoriete webbrowser en controleer of er een certificaatfout.
   
     ```
     Invoke-WebRequest : hello underlying connection was closed: Could not establish trust relationship for hello SSL/TLSsecure channel.
     ```
   
   Als deze is voltooid, worden Hallo uitvoer moet eruitzien als Hallo hieronder:
   
   ```
   > .\ExecuteSampleSplitMerge.ps1 -UserName 'mysqluser' -Password 'MySqlPassw0rd' -ShardMapManagerServerName 'abcdefghij.database.windows.net' -SplitMergeServiceEndpoint 'http://mysplitmergeservice.cloudapp.net' -CertificateThumbprint 0123456789abcdef0123456789abcdef01234567
   > Sending split request
   > Began split operation with id dc68dfa0-e22b-4823-886a-9bdc903c80f3
   > Polling split-merge request status. Press Ctrl-C tooend
   > Progress: 0% | Status: Queued | Details: [Informational] Queued request
   > Progress: 5% | Status: Starting | Details: [Informational] Starting split-merge state machine for request.
   > Progress: 5% | Status: Starting | Details: [Informational] Performing data consistency checks on target     shards.
   > Progress: 20% | Status: CopyingReferenceTables | Details: [Informational] Moving reference tables from     source tootarget shard.
   > Progress: 20% | Status: CopyingReferenceTables | Details: [Informational] Waiting for reference tables copy     completion.
   > Progress: 20% | Status: CopyingReferenceTables | Details: [Informational] Moving reference tables from     source tootarget shard.
   > Progress: 44% | Status: CopyingShardedTables | Details: [Informational] Moving key range [100:110) of     Sharded tables
   > Progress: 44% | Status: CopyingShardedTables | Details: [Informational] Successfully copied key range     [100:110) for table [dbo].[MyShardedTable]
   > ...
   > ...
   > Progress: 90% | Status: Completing | Details: [Informational] Successfully deleted shardlets in table     [dbo].[MyShardedTable].
   > Progress: 90% | Status: Completing | Details: [Informational] Deleting any temp tables that were created     while processing hello request.
   > Progress: 100% | Status: Succeeded | Details: [Informational] Successfully processed request.
   > Sending merge request
   > Began merge operation with id 6ffc308f-d006-466b-b24e-857242ec5f66
   > Polling request status. Press Ctrl-C tooend
   > Progress: 0% | Status: Queued | Details: [Informational] Queued request
   > Progress: 5% | Status: Starting | Details: [Informational] Starting split-merge state machine for request.
   > Progress: 5% | Status: Starting | Details: [Informational] Performing data consistency checks on target     shards.
   > Progress: 20% | Status: CopyingReferenceTables | Details: [Informational] Moving reference tables from     source tootarget shard.
   > Progress: 44% | Status: CopyingShardedTables | Details: [Informational] Moving key range [100:110) of     Sharded tables
   > Progress: 44% | Status: CopyingShardedTables | Details: [Informational] Successfully copied key range     [100:110) for table [dbo].[MyShardedTable]
   > ...
   > ...
   > Progress: 90% | Status: Completing | Details: [Informational] Successfully deleted shardlets in table     [dbo].[MyShardedTable].
   > Progress: 90% | Status: Completing | Details: [Informational] Deleting any temp tables that were created     while processing hello request.
   > Progress: 100% | Status: Succeeded | Details: [Informational] Successfully processed request.
   > 
   ```
6. Experimenteer met andere gegevenstypen! Alle deze scripts duren een optionele - ShardKeyType parameter waarmee u toospecify Hallo sleuteltype. Hallo standaard Int32 is, maar u kunt ook opgeven Int64, Guid of binair.

## <a name="create-requests"></a>Aanvragen maken
Hallo-service kan worden gebruikt via het Hallo-webgebruikersinterface of te importeren en gebruiken van Hallo SplitMerge.psm1 PowerShell-module die wordt uw aanvragen via Hallo Webrol indienen.

Hallo-service kunt gegevens in zowel de shard-tabellen en de verwijzingsdimensies verplaatsen. Een shard-tabel heeft een sharding-sleutelkolom en andere rijgegevens in elke shard heeft. Een verwijzing naar de tabel is niet shard zodat deze Hallo bevat dezelfde gegevens op elke shard rij. Verwijzingsdimensies zijn handig voor gegevens die niet vaak wijzigen en gebruikte tooJOIN met shard tabellen in query's.

In de volgorde tooperform samenvoegbewerking voor gesplitste, moet u Hallo shard-tabellen en tabellen die u wilt dat toohave verplaatst declareren. Dit wordt bewerkstelligd met Hallo **SchemaInfo** API. Deze API is in Hallo **Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.Schema** naamruimte.

1. Voor elke shard-tabel maken een **ShardedTableInfo** object met een beschrijving van de tabel Hallo bovenliggende schemanaam (optioneel, standaard te 'dbo'), Hallo tabelnaam en Hallo kolomnaam in de tabel die de Hallo sharding sleutel bevat.
2. Maak voor elke tabel verwijzing naar een **ReferenceTableInfo** object met een beschrijving van de tabel Hallo bovenliggende schemanaam (optioneel, standaardinstellingen te 'dbo') en de tabelnaam Hallo.
3. Hallo hierboven TableInfo objecten tooa nieuwe toevoegen **SchemaInfo** object.
4. Ophalen van een verwijzing tooa **ShardMapManager** object en de aanroep **GetSchemaInfoCollection**.
5. Hallo toevoegen **SchemaInfo** toohello **SchemaInfoCollection**, bieden Hallo shard toewijzingsnaam.

Een voorbeeld hiervan in Hallo SetupSampleSplitMergeEnvironment.ps1 script weergegeven.

Hallo gesplitste samenvoegen service maakt geen doeldatabase hello (of een schema voor alle tabellen in Hallo database) voor u. Ze moeten zijn vooraf gemaakte voordat een aanvraag toohello-service worden verzonden.

## <a name="troubleshooting"></a>Problemen oplossen
Bij het uitvoeren van powershell-Hallo voorbeeldscripts weergegeven Hallo onder bericht:

   ```
   Invoke-WebRequest : hello underlying connection was closed: Could not establish trust relationship for hello SSL/TLS secure channel.
   ```

Deze fout betekent dat uw SSL-certificaat is niet juist geconfigureerd. Volg de instructies Hallo in sectie 'Verbinding maken met een webbrowser'.

Als u geen aanvragen indienen mogelijk ziet u dit:

```
[Exception] System.Data.SqlClient.SqlException (0x80131904): Could not find stored procedure 'dbo.InsertRequest'. 
```

In dit geval, Controleer uw configuratiebestand in de instelling voor bepaalde Hallo **WorkerRoleSynchronizationStorageAccountConnectionString**. Deze fout geeft meestal aan dat werkrol Hallo kan metagegevensdatabase Hallo bij het eerste gebruik is niet initialiseren. 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-scale-configure-deploy-split-and-merge/allowed-services.png
[2]: ./media/sql-database-elastic-scale-configure-deploy-split-and-merge/manage.png
[3]: ./media/sql-database-elastic-scale-configure-deploy-split-and-merge/staging.png
[4]: ./media/sql-database-elastic-scale-configure-deploy-split-and-merge/upload.png
[5]: ./media/sql-database-elastic-scale-configure-deploy-split-and-merge/storage.png


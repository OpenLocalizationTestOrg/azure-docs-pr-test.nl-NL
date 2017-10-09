---
title: 'Fouten opsporen in Hadoop in HDInsight: logboekbestanden weergeven en foutberichten - Azure interpreteren | Microsoft Docs'
description: Meer informatie over Hallo foutberichten die kan worden weergegeven bij het beheren van HDInsight met behulp van PowerShell en de stappen die u toorecover kunt uitvoeren.
services: hdinsight
tags: azure-portal
editor: cgronlun
manager: jhubbard
author: mumian
documentationcenter: 
ms.assetid: 7e6ceb0e-8be8-4911-bc80-20714030a3ad
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/06/2017
ms.author: jgao
ms.openlocfilehash: 2f12a40e9dcac32ce2e11d66d60d8b3b212ecb53
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-hdinsight-logs"></a>HDInsight-logboekbestanden analyseren
Elke Hadoop-cluster in Azure HDInsight is een Azure storage-account gebruikt als het standaardbestandssysteem Hallo. Hallo storage-account wordt verwezen als Hallo Storage-standaardaccount. Cluster gebruikt hello Azure Table storage en Hallo Blob-opslag op Hallo default Storage account toostore de logboeken.  Zie toofind uit Hallo storage-standaardaccount voor uw cluster [beheren Hadoop-clusters in HDInsight](hdinsight-administer-use-management-portal.md#find-the-default-storage-account). Hallo logboeken behouden in Hallo Storage-account, zelfs nadat Hallo-cluster is verwijderd.

## <a name="logs-written-tooazure-tables"></a>Logboeken geschreven tooAzure tabellen
Hallo kunt Logboeken geschreven tooAzure tabellen u één niveau van inzicht in wat er met een HDInsight-cluster gebeurt.

Wanneer u een HDInsight-cluster maakt, worden automatisch 6 tabellen gemaakt voor op basis van Linux-clusters in de Hallo standaard Table storage:

* hdinsightagentlog
* syslog
* daemonlog
* hadoopservicelog
* ambariserverlog
* ambariagentlog

3 tabellen zijn gemaakt voor Windows gebaseerde clusters:

* bestand: logboek van gebeurtenissen/uitzonderingen aangetroffen in de inrichting/instellen van HDInsight-clusters.
* hadoopinstalllog: logboek van gebeurtenissen/uitzonderingen optreden tijdens het installeren van Hadoop op Hallo-cluster. Deze tabel kan nuttig zijn bij het opsporen van problemen worden gemaakt met aangepaste parameters tooclusters gerelateerd.
* hadoopservicelog: logboek van gebeurtenissen/uitzonderingen worden bijgehouden door alle Hadoop-services. Deze tabel mogelijk nuttig zijn bij het opsporen van problemen met gerelateerde toojob fouten op HDInsight-clusters.

Hallo tabel bestandsnamen zijn **u<ClusterName>DDMonYYYYatHHMMSSsss<TableName>**.

Deze tabellen bevat Hallo velden te volgen:

* ClusterDnsName
* ComponentName
* eventTimestamp
* Host
* MALoggingHash
* Bericht
* N
* PreciseTimeStamp
* Rol
* RowIndex
* Tenant
* TIJDSTEMPEL
* TraceLevel

### <a name="tools-for-accessing-hello-logs"></a>Hulpprogramma's voor het Hallo-Logboeken openen
Er zijn veel hulpprogramma's beschikbaar zijn voor toegang tot gegevens in deze tabellen:

* Visual Studio
* Azure Opslagverkenner
* Power Query voor Excel

#### <a name="use-power-query-for-excel"></a>Gebruik Power Query voor Excel
Power Query kan worden geïnstalleerd vanaf [www.microsoft.com/en-us/download/details.aspx?id=39379](http://www.microsoft.com/en-us/download/details.aspx?id=39379). Zie Hallo downloadpagina voor Hallo systeemvereisten

**toouse Power Query tooopen en analyseren van Hallo-serviceaccount voor aanmelden**

1. Open **Microsoft Excel**.
2. Van Hallo **Power Query** menu, klikt u op **van Azure**, en klik vervolgens op **van Microsoft Azure Table storage**.
   
    ![HDInsight Hadoop Excel PowerQuery openen Azure-tabelopslag](./media/hdinsight-debug-jobs/hdinsight-hadoop-analyze-logs-using-excel-power-query-open.png)
3. Voer opslagaccountnaam Hallo. Dit kan Hallo korte naam of FQDN-naam Hallo zijn.
4. Hallo opslagaccountsleutel invoeren. U ziet een lijst met tabellen:
   
    ![HDInsight Hadoop-logboeken die zijn opgeslagen in Azure Table storage](./media/hdinsight-debug-jobs/hdinsight-hadoop-analyze-logs-table-names.png)
5. Klik met de rechtermuisknop Hallo hadoopservicelog tabel in Hallo **Navigator** deelvenster en selecteer **bewerken**. U ziet 4 kolommen. Verwijder desgewenst, Hallo **partitiesleutel**, **rijsleutel**, en **tijdstempel** kolommen te selecteren en vervolgens op **kolommen verwijderen** Hallo-opties in Hallo-lint.
6. Klik op Hallo Uitvouwpictogram op Hallo kolom toochoose Hallo kolommen tooimport in Excel-werkblad Hallo van inhoud. Voor deze demonstratie gekozen TraceLevel en ComponentName: het mij basisinformatie waarop onderdelen problemen had kan geven.
   
    ![HDInsight Hadoop-logboeken kiezen kolommen](./media/hdinsight-debug-jobs/hdinsight-hadoop-analyze-logs-using-excel-power-query-filter.png)
7. Klik op **OK** tooimport Hallo gegevens.
8. Selecteer Hallo **TraceLevel**, rol, en **ComponentName** kolommen en klik vervolgens op **Group By** besturingselement in Hallo-lint.
9. Klik op **OK** in Hallo dialoogvenster Groeperen op
10. Klik op ** toepassen & sluiten **.

U kunt nu Excel toofilter en sorteren gebruiken indien nodig. Natuurlijk kunt u tooinclude andere kolommen (bijvoorbeeld bericht) in de volgorde toodrill omlaag in de problemen wanneer ze worden uitgevoerd, maar selecteren en groeperen Hallo kolommen die hierboven worden beschreven, een goede beeld biedt van wat er met Hadoop-services gebeurt. Hallo kan dezelfde idee worden toegepast toohello bestand en hadoopinstalllog tabellen.

#### <a name="use-visual-studio"></a>Visual Studio gebruiken
**toouse Visual Studio**

1. Open Visual Studio.
2. Van Hallo **weergave** menu, klikt u op **Cloud Explorer**. Of klik op **CTRL +\, CTRL + X**.
3. Van **Cloud Explorer**, selecteer **brontypen**.  Hallo andere beschikbare optie is **resourcegroepen**.
4. Vouw **Opslagaccounts**, Hallo storage-standaardaccount voor uw cluster en vervolgens **tabellen**.
5. Dubbelklik op **hadoopservicelog**.
6. Een filter toevoegen. Bijvoorbeeld:
   
        TraceLevel eq 'ERROR'
   
    ![HDInsight Hadoop-logboeken kiezen kolommen](./media/hdinsight-debug-jobs/hdinsight-hadoop-analyze-logs-visual-studio-filter.png)
   
    Zie voor meer informatie over het maken van filters [filtertekenreeksen opstellen voor Hallo tabelontwerp](../vs-azure-tools-table-designer-construct-filter-strings.md).

## <a name="logs-written-tooazure-blob-storage"></a>Logboeken schriftelijke tooAzure Blob-opslag
[Hallo-Logboeken geschreven tooAzure tabellen](#log-written-to-azure-tables) één niveau van inzicht in wat er met een HDInsight-cluster gebeurt. Deze tabellen bieden echter geen in taak niveau Logboeken, dit kunnen nuttig zijn bij het analyseren dieper in problemen wanneer deze optreden. tooprovide deze volgende detailniveau, kunt u HDInsight-clusters zijn geconfigureerd toowrite taak logboeken tooyour Blob Storage-account voor elke taak die wordt ingediend via Templeton. Dit betekent vrijwel, taken die worden verzonden met de Hallo Microsoft Azure PowerShell-cmdlets of Hallo .NET taak verzending van API's gebruiken, geen taken die worden verzonden via RDP/vanaf de opdrachtregel-line toegang, toohello cluster. 

tooview hello Logboeken, Zie [toepassingslogboeken op Linux gebaseerde HDInsight YARN toegang](hdinsight-hadoop-access-yarn-app-logs-linux.md).

Zie voor meer informatie over toepassingslogboeken [vereenvoudigen van beheer van de gebruiker-logboeken en toegang in YARN](http://hortonworks.com/blog/simplifying-user-logs-management-and-access-in-yarn/).

## <a name="view-cluster-health-and-job-logs"></a>Bekijk de logboeken van de status en taak cluster
### <a name="access-hadoop-ui"></a>Toegang tot de Hadoop-UI
Hallo Azure-portal, klik op een HDInsight-cluster naam tooopen Hallo cluster blade. Cluster-blade hello, klikt u op **Dashboard**.

![Starten van de cluster-dashboard](./media/hdinsight-debug-jobs/hdi-debug-launch-dashboard.png)

Voer desgevraagd beheerdersreferenties Hallo-cluster. In Hallo Query-Console die wordt geopend, klikt u op **Hadoop UI**.

![Hadoop-gebruikersinterface starten](./media/hdinsight-debug-jobs/hdi-debug-launch-dashboard-hadoop-ui.png)

### <a name="access-hello-yarn-ui"></a>Toegang tot gebruikersinterface van Yarn Hallo
Hallo Azure-portal, klik op een HDInsight-cluster naam tooopen Hallo cluster blade. Cluster-blade hello, klikt u op **Dashboard**. Voer desgevraagd beheerdersreferenties Hallo-cluster. In Hallo Query-Console die wordt geopend, klikt u op **gebruikersinterface van YARN**.

U kunt Hallo gebruikersinterface van YARN toodo Hallo volgende gebruiken:

* **Clusterstatus ophalen**. Vouw in het linkerdeelvenster hello, **Cluster**, en klik op **over**. Deze aanwezig cluster statusdetails zoals Totaal toegewezen geheugen, kernen gebruikt, de status van Hallo cluster resourcemanager, cluster-versie enzovoort.
  
    ![Starten van de cluster-dashboard](./media/hdinsight-debug-jobs/hdi-debug-yarn-cluster-state.png)
* **Knooppunt status ophalen voor**. Vouw in het linkerdeelvenster hello, **Cluster**, en klik op **knooppunten**. Hiermee worden alle Hallo knooppunten in cluster hello, HTTP-adres van elk knooppunt, resources toegewezen tooeach knooppunt, enzovoort.
* **Taakstatus controleren**. Vouw in het linkerdeelvenster hello, **Cluster**, en klik vervolgens op **toepassingen** toolist alle taken in het cluster Hallo Hallo. Als u wilt dat toolook op taken in een specifieke status (zoals nieuwe, verzonden, die wordt uitgevoerd, enzovoort), klikt u op Hallo koppeling onder **toepassingen**. Verder kunt u Hallo taak naam toofind voor meer informatie over Hallo taak dergelijke inclusief Hallo uitvoer, Logboeken, enzovoort.

### <a name="access-hello-hbase-ui"></a>Toegang tot Hallo HBase UI
Hallo Azure-portal, klik op een blade HDInsight HBase-cluster naam tooopen Hallo-cluster. Cluster-blade hello, klikt u op **Dashboard**. Voer desgevraagd beheerdersreferenties Hallo-cluster. In Hallo Query-Console die wordt geopend, klikt u op **HBase UI**.

## <a name="hdinsight-error-codes"></a>HDInsight-foutcodes
Hallo foutberichten gespecificeerd in deze sectie vindt u toohelp Hallo gebruikers van Hadoop in Azure HDInsight inzicht in mogelijke fouten die optreden kunnen bij het beheren van Hallo-service via Azure PowerShell en tooadvise ze op Hallo stappen Dit kunnen toorecover van Hallo fout worden genomen.

Sommige van deze foutberichten kan ook worden gezien in hello Azure-portal als het gebruikte toomanage HDInsight-clusters. Andere foutberichten die mogelijk optreden, maar er zijn minder gedetailleerd vanwege toohello beperkingen op Hallo corrigerende acties mogelijk in deze context. Andere foutberichten vindt u in het Hallo-contexten waarbij Hallo risicobeperking duidelijk is. 

### <a id="AtleastOneSqlMetastoreMustBeProvided"></a>AtleastOneSqlMetastoreMustBeProvided
* **Beschrijving**: Geef informatie over de Azure SQL database voor ten minste een onderdeel in volgorde toouse aangepaste instellingen voor Hive en Oozie metastores.
* **Risicobeperking**: Hallo gebruiker moet een geldige SQL Azure metastore en probeer het opnieuw Hallo aanvraag toosupply.  

### <a id="AzureRegionNotSupported"></a>AzureRegionNotSupported
* **Beschrijving**: kan geen cluster maken in regio *nameOfYourRegion*. Gebruik een geldige HDInsight-regio en de aanvraag opnieuw proberen.
* **Risicobeperking**: klant moet maken Hallo cluster regio die momenteel worden ondersteund: Zuidoost-Azië, West-Europa, VS-Oost, Noord-Europa of VS-West.  

### <a id="ClusterContainerRecordNotFound"></a>ClusterContainerRecordNotFound
* **Beschrijving**: Hallo-server niet kan vinden Hallo aangevraagd cluster record.  
* **Risicobeperking**: Voer Hallo-bewerking opnieuw uit.

### <a id="ClusterDnsNameInvalidReservedWord"></a>ClusterDnsNameInvalidReservedWord
* **Beschrijving**: Cluster DNS-naam *yourDnsName* is ongeldig. Zorg ervoor dat de naam begint en eindigt op alfanumerieke en mogen alleen '-' speciaal teken  
* **Risicobeperking**: Zorg ervoor dat u hebt een geldige DNS-naam gebruikt voor uw cluster die begint en eindigt op alfanumerieke en bevat geen speciale tekens dan Hallo dash '-' en probeer vervolgens opnieuw Hallo.

### <a id="ClusterNameUnavailable"></a>ClusterNameUnavailable
* **Beschrijving**: clusternaam *yourClusterName* is niet beschikbaar. Kies een andere naam.  
* **Risicobeperking**: Hallo gebruiker moet opgeven van een clusternaam die uniek is en niet bestaat en probeer het opnieuw. Als gebruiker Hallo Hallo Portal gebruikt, maakt u Hallo UI melden ze als een clusternaam al wordt gebruikt tijdens het Hallo stappen.

### <a id="ClusterPasswordInvalid"></a>ClusterPasswordInvalid
* **Beschrijving**: Cluster wachtwoord is ongeldig. Wachtwoord moet ten minste 10 tekens lang zijn en moet ten minste één cijfer, hoofdletter, kleine letter en speciale tekens zonder spaties bevatten en mogen geen Hallo gebruikersnaam als onderdeel van deze.  
* **Risicobeperking**: Geef een geldige clusternaam wachtwoord en probeer Hallo opnieuw.

### <a id="ClusterUserNameInvalid"></a>ClusterUserNameInvalid
* **Beschrijving**: Cluster gebruikersnaam is ongeldig. Zorg ervoor dat er geen gebruikersnaam bevat speciale tekens of spaties.  
* **Risicobeperking**: Geef een geldige clusternaam-gebruikersnaam en probeer Hallo opnieuw.

### <a id="ClusterUserNameInvalidReservedWord"></a>ClusterUserNameInvalidReservedWord
* **Beschrijving**: Cluster DNS-naam *yourDnsClusterName* is ongeldig. Zorg ervoor dat de naam begint en eindigt op alfanumerieke en mogen alleen '-' speciaal teken  
* **Risicobeperking**: Geef een geldige gebruikersnaam van de DNS-cluster en probeer Hallo opnieuw.

### <a id="ContainerNameMisMatchWithDnsName"></a>ContainerNameMisMatchWithDnsName
* **Beschrijving**: containernaam in URI *yourcontainerURI* en DNS-naam *yourDnsName* in de aanvraag hoofdtekst moet worden Hallo dezelfde.  
* **Risicobeperking**: Zorg ervoor dat de naam van de container en de DNS-naam zijn dezelfde Hallo en Voer Hallo-bewerking opnieuw uit.

### <a id="DataNodeDefinitionNotFound"></a>DataNodeDefinitionNotFound
* **Beschrijving**: ongeldige clusterconfiguratie. Kan geen toofind eventuele gegevensdefinities knooppunt in de grootte van knooppunt.  
* **Risicobeperking**: Voer Hallo-bewerking opnieuw uit.

### <a id="DeploymentDeletionFailure"></a>DeploymentDeletionFailure
* **Beschrijving**: verwijderen van de implementatie is mislukt voor Hallo Cluster  
* **Risicobeperking**: Hallo Voer verwijderbewerking opnieuw uit.

### <a id="DnsMappingNotFound"></a>DnsMappingNotFound
* **Beschrijving**: Service is een configuratiefout. Vereiste informatie in DNS-toewijzing niet vinden.  
* **Risicobeperking**: cluster verwijderen en een nieuw cluster maken.

### <a id="DuplicateClusterContainerRequest"></a>DuplicateClusterContainerRequest
* **Beschrijving**: dubbele cluster container maken poging. Record bestaat voor *nameOfYourContainer* maar Etags komen niet overeen.
* **Risicobeperking**: Geef een unieke naam voor het Hallo-container en probeer het opnieuw Hallo Maakbewerking.

### <a id="DuplicateClusterInHostedService"></a>DuplicateClusterInHostedService
* **Beschrijving**: de gehoste service *nameOfYourHostedService* bevat al een cluster. Een gehoste service kan niet meerdere clusters bevatten  
* **Risicobeperking**: Hallo-hostcluster in een andere gehoste service.

### <a id="FailureToUpdateDeploymentStatus"></a>FailureToUpdateDeploymentStatus
* **Beschrijving**: server Hallo Hallo status van de implementatie van het cluster Hallo kan niet worden bijgewerkt.  
* **Risicobeperking**: Voer Hallo-bewerking opnieuw uit. Als dit herhaaldelijk gebeurt, moet u contact op met CSS.

### <a id="HdiRestoreClusterAltered"></a>HdiRestoreClusterAltered
* **Beschrijving**: Cluster *yourClusterName* is verwijderd als onderdeel van onderhoudsmodus. Controleer opnieuw Hallo cluster maken.
* **Risicobeperking**: Maak Hallo-cluster.

### <a id="HeadNodeConfigNotFound"></a>HeadNodeConfigNotFound
* **Beschrijving**: ongeldige clusterconfiguratie. Hoofdknooppunt configuratie is niet gevonden in knooppuntgrootten vereist.
* **Risicobeperking**: Voer Hallo-bewerking opnieuw uit.

### <a id="HostedServiceCreationFailure"></a>HostedServiceCreationFailure
* **Beschrijving**: kan geen toocreate gehoste service *nameOfYourHostedService*. Probeer de aanvraag.  
* **Risicobeperking**: Hallo-aanvraag opnieuw.

### <a id="HostedServiceHasProductionDeployment"></a>HostedServiceHasProductionDeployment
* **Beschrijving**: gehoste Service *nameOfYourHostedService* heeft al een productie-implementatie. Een gehoste service kan niet meerdere productie-implementaties bevatten. Hallo-aanvraag met een andere clusternaam op opnieuw proberen.
* **Risicobeperking**: gebruik een andere clusternaam op en Hallo aanvraag opnieuw proberen.

### <a id="HostedServiceNotFound"></a>HostedServiceNotFound
* **Beschrijving**: gehoste Service *nameOfYourHostedService* voor Hallo-cluster is niet gevonden.  
* **Risicobeperking**: als Hallo cluster zich in een foutstatus, verwijderen en probeer het opnieuw.

### <a id="HostedServiceWithNoDeployment"></a>HostedServiceWithNoDeployment
* **Beschrijving**: gehoste Service *nameOfYourHostedService* heeft geen gekoppelde implementatie.  
* **Risicobeperking**: als Hallo cluster zich in een foutstatus, verwijderen en probeer het opnieuw.

### <a id="InsufficientResourcesCores"></a>InsufficientResourcesCores
* **Beschrijving**: Hallo SubscriptionId *yourSubscriptionId* heeft geen kernen links toocreate cluster *yourClusterName*. Vereist: *resourcesRequired*, beschikbaar: *resourcesAvailable*.  
* **Risicobeperking**: resources in uw abonnement vrij te maken of Hallo resources beschikbaar toohello abonnement te verhogen en probeer het toocreate Hallo cluster opnieuw.

### <a id="InsufficientResourcesHostedServices"></a>InsufficientResourcesHostedServices
* **Beschrijving**: abonnements-ID *yourSubscriptionId* heeft geen quota voor een nieuw cluster met HostedService toocreate *yourClusterName*.  
* **Risicobeperking**: resources in uw abonnement vrij te maken of Hallo resources beschikbaar toohello abonnement te verhogen en probeer het toocreate Hallo cluster opnieuw.

### <a id="InternalErrorRetryRequest"></a>InternalErrorRetryRequest
* **Beschrijving**: Hallo-server is een interne fout opgetreden. Probeer de aanvraag.  
* **Risicobeperking**: Hallo-aanvraag opnieuw.

### <a id="InvalidAzureStorageLocation"></a>InvalidAzureStorageLocation
* **Beschrijving**: Azure-opslaglocatie *dataRegionName* is geen geldige locatie. Controleer of de regio Hallo juist is en de aanvraag opnieuw proberen.
* **Risicobeperking**: Selecteer een opslaglocatie die ondersteuning biedt voor HDInsight, Controleer of het cluster geplaatst is en probeer Hallo opnieuw.

### <a id="InvalidNodeSizeForDataNode"></a>InvalidNodeSizeForDataNode
* **Beschrijving**: ongeldige VM-grootte voor gegevensknooppunten. Grootte van de grote virtuele machine alleen wordt ondersteund voor alle gegevensknooppunten.  
* **Risicobeperking**: Hallo ondersteund knooppuntgrootte opgeven voor Hallo gegevensknooppunt en probeer Hallo opnieuw.

### <a id="InvalidNodeSizeForHeadNode"></a>InvalidNodeSizeForHeadNode
* **Beschrijving**: ongeldige VM-grootte voor het hoofdknooppunt. Alleen de grootte 'Zijn VM' wordt ondersteund voor het hoofdknooppunt.  
* **Risicobeperking**: Hallo ondersteund knooppuntgrootte opgeven voor het hoofdknooppunt Hallo op en probeer opnieuw Hallo

### <a id="InvalidRightsForDeploymentDeletion"></a>InvalidRightsForDeploymentDeletion
* **Beschrijving**: abonnements-ID *yourSubscriptionId* gebruikte beschikt niet over voldoende machtigingen tooexecute delete-bewerking voor cluster *yourClusterName*.  
* **Risicobeperking**: als Hallo cluster zich in een foutstatus, zet het neer en probeer het opnieuw.  

### <a id="InvalidStorageAccountBlobContainerName"></a>InvalidStorageAccountBlobContainerName
* **Beschrijving**: externe blob-container opslagaccountnaam *yourContainerName* is ongeldig. Zorg ervoor dat de naam begint met een letter en bevat alleen kleine letters, cijfers en streepjes.  
* **Risicobeperking**: Geef een geldige blob-container opslagaccountnaam en probeer Hallo opnieuw.

### <a id="InvalidStorageAccountConfigurationSecretKey"></a>InvalidStorageAccountConfigurationSecretKey
* **Beschrijving**: configuratie voor externe opslagaccount *yourStorageAccountName* is vereist toohave details van de geheime sleutel toobe set.  
* **Risicobeperking**: Geef een geldige geheime sleutel voor Hallo storage-account en probeer Hallo opnieuw.

### <a id="InvalidVersionHeaderFormat"></a>InvalidVersionHeaderFormat
* **Beschrijving**: versiekop *yourVersionHeader* is geen geldige indeling jjjj-mm-dd.  
* **Risicobeperking**: Geef een geldige indeling voor Hallo versie-header en het Hallo-aanvraag opnieuw proberen.

### <a id="MoreThanOneHeadNode"></a>MoreThanOneHeadNode
* **Beschrijving**: ongeldige clusterconfiguratie. Meer dan één hoofdknooppunt configuratie gevonden.  
* **Risicobeperking**: bewerken Hallo configuratie zodanig dat slechts één hoofdknooppunt is opgegeven.

### <a id="OperationTimedOutRetryRequest"></a>OperationTimedOutRetryRequest
* **Beschrijving**: Hallo-bewerking kan niet worden voltooid binnen de toegestane tijd Hallo of het maximum aantal pogingen Hallo probeert mogelijk. Probeer de aanvraag.  
* **Risicobeperking**: Hallo-aanvraag opnieuw.

### <a id="ParameterNullOrEmpty"></a>ParameterNullOrEmpty
* **Beschrijving**: Parameter *yourParameterName* mag niet null of leeg.  
* **Risicobeperking**: Geef een geldige waarde voor parameter Hallo.

### <a id="PreClusterCreationValidationFailure"></a>PreClusterCreationValidationFailure
* **Beschrijving**: een of meer Hallo cluster maken aanvraag invoer is niet geldig. Zorg ervoor dat de invoerwaarden Hallo juist zijn en de aanvraag opnieuw proberen.  
* **Risicobeperking**: Controleer of de invoerwaarden Hallo juist zijn en de aanvraag opnieuw proberen.

### <a id="RegionCapabilityNotAvailable"></a>RegionCapabilityNotAvailable
* **Beschrijving**: regio mogelijkheid is niet beschikbaar voor de regio *yourRegionName* en abonnements-ID *yourSubscriptionId*.  
* **Risicobeperking**: Geef een regio die ondersteuning biedt voor HDInsight-clusters. Hallo openbaar ondersteunde regio's zijn: Zuidoost-Azië, West-Europa, VS-Oost, Noord-Europa of VS-West.

### <a id="StorageAccountNotColocated"></a>StorageAccountNotColocated
* **Beschrijving**: opslagaccount *yourStorageAccountName* bevindt zich in de regio *currentRegionName*. Dit moet hetzelfde zijn als Hallo cluster regio *yourClusterRegionName*.  
* **Risicobeperking**: Geef het een opslagaccount in dezelfde regio die het cluster in Hallo is of als uw gegevens al in het opslagaccount hello is, maakt u een nieuw cluster in Hallo dezelfde regio bevinden als de bestaande opslagaccount Hallo. Als u Hallo Portal Hallo UI ontvangt een melding van dit probleem van tevoren.

### <a id="SubscriptionIdNotActive"></a>SubscriptionIdNotActive
* **Beschrijving**: opgegeven abonnements-ID *yourSubscriptionId* is niet actief.  
* **Risicobeperking**: uw abonnement opnieuw activeren of een nieuw geldig abonnement ophalen.

### <a id="SubscriptionIdNotFound"></a>SubscriptionIdNotFound
* **Beschrijving**: abonnements-ID *yourSubscriptionId* is niet gevonden.  
* **Risicobeperking**: Controleer of uw abonnements-ID geldig is en probeer Hallo opnieuw.

### <a id="UnableToResolveDNS"></a>UnableToResolveDNS
* **Beschrijving**: kan geen tooresolve DNS *yourDnsUrl*. Controleer of de Hallo de FQDN-URL voor het eindpunt voor blob Hallo is opgegeven.  
* **Risicobeperking**: Geef een geldige blob-URL. Hallo-URL moet worden volledig geldig zijn, inclusief beginnen met *http://* en eindigt op *.com*.

### <a id="UnableToVerifyLocationOfResource"></a>UnableToVerifyLocationOfResource
* **Beschrijving**: locatie van bron kan niet tooverify *yourDnsUrl*. Controleer of de Hallo de FQDN-URL voor het eindpunt voor blob Hallo is opgegeven.  
* **Risicobeperking**: Geef een geldige blob-URL. Hallo-URL moet worden volledig geldig zijn, inclusief beginnen met *http://* en eindigt op *.com*.

### <a id="VersionCapabilityNotAvailable"></a>VersionCapabilityNotAvailable
* **Beschrijving**: versie mogelijkheid is niet beschikbaar voor versie *specifiedVersion* en abonnements-ID *yourSubscriptionId*.  
* **Risicobeperking**: Kies een versie die beschikbaar is en probeer Hallo opnieuw.

### <a id="VersionNotSupported"></a>VersionNotSupported
* **Beschrijving**: versie *specifiedVersion* niet ondersteund.
* **Risicobeperking**: Kies een versie die wordt ondersteund en probeer Hallo opnieuw.

### <a id="VersionNotSupportedInRegion"></a>VersionNotSupportedInRegion
* **Beschrijving**: versie *specifiedVersion* is niet beschikbaar in Azure-regio *specifiedRegion*.  
* **Risicobeperking**: Kies een versie die wordt ondersteund in Hallo regio is opgegeven en probeer Hallo opnieuw.

### <a id="WasbAccountConfigNotFound"></a>WasbAccountConfigNotFound
* **Beschrijving**: ongeldige clusterconfiguratie. Vereiste WASB-accountconfiguratie niet gevonden in externe accounts.  
* **Risicobeperking**: Controleer of Hallo account bestaat en correct is opgegeven in configuratie en probeer het opnieuw Hallo-bewerking.

## <a name="next-steps"></a>Volgende stappen
* [Ambari-weergaven toodebug Tez-taken op HDInsight gebruiken](hdinsight-debug-ambari-tez-view.md)
* [Dumpbestanden voor Hadoop-services op Linux gebaseerde HDInsight heap inschakelen](hdinsight-hadoop-collect-debug-heap-dump-linux.md)
* [HDInsight-clusters beheren met behulp van Hallo Ambari-Webgebruikersinterface](hdinsight-hadoop-manage-ambari.md)


---
title: aaaImport gegevens naar Machine Learning Studio uit gegevensbronnen voor online | Microsoft Docs
description: Hoe tooimport uw trainingsgegevens Azure Machine Learning Studio uit verschillende online bronnen.
keywords: gegevens, gegevensindeling, gegevenstypen, gegevensbronnen, trainingsgegevens importeren
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 701b93fe-765b-4d15-a1cf-9b607f17add6
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev;garye
ms.openlocfilehash: aae6907cdd0b4dc373ae08c2569caa276c198b49
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="import-data-into-azure-machine-learning-studio-from-various-online-data-sources-with-hello-import-data-module"></a>Gegevens importeren in Azure Machine Learning Studio van verschillende online gegevensbronnen met Hallo gegevens importeren-module
Dit artikel wordt beschreven Hallo-ondersteuning voor het online gegevens importeren uit diverse bronnen en Hallo informatie nodig toomove gegevens van deze bronnen in een Azure Machine Learning-experiment.

> [!NOTE]
> In dit artikel bevat algemene informatie over Hallo [importgegevens] [ import-data] module. Voor meer gedetailleerde informatie over Hallo typen gegevens die u toegang hebt tot indelingen, parameters en antwoorden toocommon vragen, u Hallo module-naslagonderwerp voor Hallo [importgegevens] [ import-data] module.
> 
> 

<!-- -->

[!INCLUDE [import-data-into-aml-studio-selector](../../includes/machine-learning-import-data-into-aml-studio.md)]

## <a name="introduction"></a>Inleiding
Met behulp van Hallo [importgegevens] [ import-data] -module, u kunt toegang tot gegevens van een van verschillende gegevensbronnen voor online terwijl uw experiment wordt uitgevoerd [Azure Machine Learning Studio](https://studio.azureml.net/Home):

* Een met behulp van HTTP-URL
* Hadoop HiveQL gebruiken
* Azure blob-opslag
* Azure-tabel
* Azure SQL database of SQL Server op Azure VM
* Lokale SQL Server-database.
* Een gegevensfeed momenteel OData-provider
* Azure CosmosDB (eerder DocumentDB genoemd)

tooaccess online gegevensbronnen in uw experiment Studio toevoegen Hallo [importgegevens] [ import-data] module tooyour, selecteer Hallo **gegevensbron**, en geef vervolgens Hallo-parameters zijn vereist tooaccess hello gegevens. Hallo online gegevensbronnen die worden ondersteund zijn in onderstaande tabel voor Hallo gespecificeerd. In deze tabel worden ook Hallo-bestandsindelingen die worden ondersteund en parameters die gebruikt tooaccess zijn Hallo gegevens.

Houd er rekening mee dat omdat deze trainingsgegevens wordt geopend terwijl uw experiment wordt uitgevoerd, alleen beschikbaar in deze experiment is. Vergelijking, zijn gegevens die zijn opgeslagen in een module gegevensset beschikbaar tooany experiment in uw werkruimte.

> [!IMPORTANT]
> Op dit moment Hallo [importgegevens] [ import-data] en [gegevens exporteren] [ export-data] modules kunnen lezen en schrijven van gegevens alleen naar Azure storage gemaakt met behulp van Hallo Klassieke implementatiemodel. Met andere woorden, Hallo nieuw type van de Azure Blob Storage-account dat een hot storage-toegangslaag biedt of cool storage-toegangslaag is nog niet ondersteund. 
> 
> In het algemeen een Azure storage-accounts die u mogelijk hebt gemaakt voordat u deze serviceoptie beschikbaar zijn geworden moet niet worden beïnvloed. 
> Als u een nieuw account toocreate nodig hebt, selecteert u **klassieke** voor Hallo Deployment model, of gebruik van resourcemanager en selecteer **algemeen** plaats **Blob storage** voor **Account kind**. 
> 
> Zie voor meer informatie [Azure Blob Storage: Hot en Cool Opslaglagen](../storage/blobs/storage-blob-storage-tiers.md).
> 
> 

## <a name="supported-online-data-sources"></a>Ondersteunde gegevensbronnen voor online
Azure Machine Learning **importgegevens** module biedt ondersteuning voor Hallo gegevensbronnen te volgen:

| Gegevensbron | Beschrijving | Parameters |
| --- | --- | --- |
| Web-URL via HTTP |Leest de gegevens in de door komma's gescheiden waarden (CSV), door tabs gescheiden waarden (TSV), kenmerkrelatie bestandsindeling (ARFF) en indelingen ondersteuning Vector Machines (SVM licht), uit een web-URL die HTTP gebruikt |<b>URL</b>: Hiermee geeft u de volledige naam van het Hallo-bestand, inclusief Hallo site-URL en bestandsnaam van de Hallo met een extensie Hallo. <br/><br/><b>Gegevensindeling</b>: Hiermee geeft u een van de gegevensbestanden Hallo ondersteund indelingen: CSV, TSV, ARFF of SVM licht. Als Hallo gegevens een rij met kolomkoppen heeft, is het gebruikte tooassign kolomnamen. |
| Hadoop/HDFS |Leest de gegevens van gedistribueerde opslag in Hadoop. U opgeven Hallo-gegevens die u wilt met behulp van HiveQL, een SQL-achtige querytaal. HiveQL kan ook worden gegevens van de gebruikte tooaggregate en uitvoeren van de gegevens filteren voordat u Hallo gegevens tooMachine Learning Studio toevoegen. |<b>Hive-databasequery</b>: Hiermee geeft u Hallo Hive-query gebruikt toogenerate Hallo gegevens.<br/><br/><b>HCatalog server-URI </b> : opgegeven Hallo-naam van het cluster met Hallo indeling  *&lt;uw clusternaam&gt;. azurehdinsight.net.*<br/><br/><b>Hadoop-gebruikersaccountnaam</b>: Hiermee geeft u Hallo Hadoop-gebruikersaccount naam tooprovision Hallo cluster gebruikt.<br/><br/><b>Wachtwoord voor gebruikersaccount Hadoop</b> : Hiermee geeft u op Hallo van referenties die worden gebruikt bij het inrichten van Hallo-cluster. Zie voor meer informatie [maken Hadoop-clusters in HDInsight](../hdinsight/hdinsight-provision-clusters.md).<br/><br/><b>Locatie van uitvoergegevens</b>: Hiermee geeft u op of Hallo gegevens worden opgeslagen in een Hadoop distributed file system (HDFS) of in Azure. <br/><ul>Als u uitvoergegevens in HDFS opslaat, geeft u de URI Hallo HDFS-server. (Ervoor toouse HDInsight Hallo clusternaam zonder Hallo HTTPS:// voorvoegsel zijn). <br/><br/>Als u de uitvoergegevens in Azure opslaat, moet u hello Azure storage-account, toegangssleutel voor opslag en opslag containernaam opgeven.</ul> |
| SQL-database |Leest de gegevens die zijn opgeslagen in een Azure SQL database of in een SQL Server-database die is uitgevoerd op een virtuele machine van Azure. |<b>Naam van de databaseserver</b>: Hiermee geeft u de naam Hallo van Hallo-server op welke Hallo database wordt uitgevoerd.<br/><ul>Voer in het geval van Azure SQL Database Hallo-servernaam die wordt gegenereerd. Deze heeft meestal Hallo formulier  *&lt;generated_identifier&gt;. database.windows.net.* <br/><br/>Voer in het geval van een SQL server gehost op een virtuele Azure-machine *tcp:&lt;DNS-naam van virtuele Machine&gt;, 1433*</ul><br/><b>Databasenaam </b>: Hiermee geeft u de naam Hallo van Hallo-database op Hallo-server. <br/><br/><b>De accountnaam van de gebruiker server</b>: Hiermee geeft u een gebruikersnaam voor een account met toegangsmachtigingen voor Hallo-database. <br/><br/><b>Het wachtwoord voor gebruikersaccount server</b>: Hiermee geeft u Hallo wachtwoord voor gebruikersaccount Hallo.<br/><br/><b>Een servercertificaat accepteren</b>: Gebruik deze optie (minder veilig) als u wilt dat tooskip Hallo sitecertificaat controleren voordat u uw gegevens leest.<br/><br/><b>Databasequery</b>: Voer een SQL-instructie waarmee Hallo gegevens u wilt dat tooread worden beschreven. |
| Lokale SQL-database. |Leest de gegevens die zijn opgeslagen in een lokale SQL-database. |<b>Gegevensgateway</b>: Hiermee geeft u de naam Hallo Hallo Data Management Gateway is geïnstalleerd op een computer waarop deze toegang hebben tot uw SQL Server-database. Zie voor meer informatie over het instellen van de gateway Hallo [advanced analytics met Azure Machine Learning met gegevens uit een lokale SQL server uitvoeren](machine-learning-use-data-from-an-on-premises-sql-server.md).<br/><br/><b>Naam van de databaseserver</b>: Hiermee geeft u de naam Hallo van Hallo-server op welke Hallo database wordt uitgevoerd.<br/><br/><b>Databasenaam </b>: Hiermee geeft u de naam Hallo van Hallo-database op Hallo-server. <br/><br/><b>De accountnaam van de gebruiker server</b>: Hiermee geeft u een gebruikersnaam voor een account met toegangsmachtigingen voor Hallo-database. <br/><br/><b>Gebruikersnaam en wachtwoord</b>: klik op <b>Voer waarden in</b> tooenter de databasereferenties van uw. U kunt Windows-verificatie of SQL Server-verificatie, al naar gelang hoe uw lokale SQL Server is geconfigureerd.<br/><br/><b>Databasequery</b>: Voer een SQL-instructie waarmee Hallo gegevens u wilt dat tooread worden beschreven. |
| Azure-tabel |Leest de gegevens van Hallo tabelservice in Azure Storage.<br/><br/>Als u minder vaak grote hoeveelheden gegevens gelezen, gebruikt u hello Azure Table-Service. Het biedt een flexibele, niet-relationele (NoSQL), sterk schaalbare, goedkope en maximaal beschikbare opslagoplossing. |opties in Hallo Hallo **importgegevens** wijzigen, afhankelijk van of u toegang tot openbare gegevens of een persoonlijke opslagaccount waarvoor aanmeldingsreferenties. Dit wordt bepaald door Hallo <b>verificatietype</b> die de waarde van 'PublicOrSAS' of 'Account', die elk een eigen set parameters heeft kunnen hebben. <br/><br/><b>Openbare of Shared Access Signature (SAS) URI</b>: Hallo parameters zijn:<br/><br/><ul><b>Tabel URI</b>: Hiermee geeft u Hallo openbare of SAS-URL voor Hallo tabel.<br/><br/><b>Hiermee geeft u op Hallo rijen tooscan voor namen van eigenschappen</b>: Hallo waarden zijn <i>TopN</i> tooscan Hallo opgegeven aantal rijen, of <i>ScanAll</i> tooget alle rijen in de tabel Hallo. <br/><br/>Als gegevens Hallo homogene en voorspelbaar is, wordt aanbevolen dat u selecteert *TopN* en voer een getal voor N. Voor grote tabellen, kan dit resulteren in sneller lezen tijden.<br/><br/>Als Hallo gegevens is opgebouwd met sets van eigenschappen die variëren op basis van Hallo diepte en positie van de tabel hello, kiest u Hallo *ScanAll* optie tooscan alle rijen. Dit zorgt ervoor Hallo integriteit van de resulterende eigenschap en de metagegevens van conversie.<br/><br/></ul><b>Persoonlijke Opslagaccount</b>: Hallo parameters zijn: <br/><br/><ul><b>Accountnaam</b>: Hiermee geeft u de naam Hallo Hallo-account dat Hallo tabel tooread bevat.<br/><br/><b>Accountsleutel</b>: Hiermee geeft u de opslagsleutel Hallo Hallo-account gekoppeld.<br/><br/><b>Tabelnaam</b> : Hiermee geeft u de naam Hallo van Hallo tabel met Hallo gegevens tooread.<br/><br/><b>Rijen tooscan voor eigenschapnamen</b>: Hallo waarden zijn <i>TopN</i> tooscan Hallo opgegeven aantal rijen, of <i>ScanAll</i> tooget alle rijen in de tabel Hallo.<br/><br/>Als Hallo gegevens homogene en voorspelbaar, het is raadzaam dat u selecteert *TopN* en voer een getal voor N. Voor grote tabellen, kan dit resulteren in sneller lezen tijden.<br/><br/>Als Hallo gegevens is opgebouwd met sets van eigenschappen die variëren op basis van Hallo diepte en positie van de tabel hello, kiest u Hallo *ScanAll* optie tooscan alle rijen. Dit zorgt ervoor Hallo integriteit van de resulterende eigenschap en de metagegevens van conversie.<br/><br/> |
| Azure Blob Storage |Leest de gegevens die zijn opgeslagen in de Blob-service Hallo in Azure Storage, met inbegrip van afbeeldingen, niet-gestructureerde tekst of binaire gegevens.<br/><br/>U kunt Hallo Blob-service toopublicly zichtbaar-gegevens of tooprivately store-toepassing. U kunt toegang tot uw gegevens vanaf elke locatie met behulp van HTTP of HTTPS-verbindingen. |opties in Hallo Hallo **importgegevens** module wijzigen, afhankelijk van of u toegang tot openbare gegevens of een persoonlijke opslagaccount waarvoor aanmeldingsreferenties. Dit wordt bepaald door Hallo <b>verificatietype</b> dit kan een waarde van 'PublicOrSAS' of 'Account' hebben.<br/><br/><b>Openbare of Shared Access Signature (SAS) URI</b>: Hallo parameters zijn:<br/><br/><ul><b>URI</b>: Hiermee geeft u Hallo openbare of SAS-URL voor Hallo storage-blob.<br/><br/><b>Bestandsindeling</b>: Hiermee geeft u de indeling Hallo Hallo gegevens in Hallo Blob-service. Hallo ondersteunde indelingen zijn CSV, TSV en ARFF.<br/><br/></ul><b>Persoonlijke Opslagaccount</b>: Hallo parameters zijn: <br/><br/><ul><b>Accountnaam</b>: Hiermee geeft u de naam Hallo van Hallo account Hallo blob die u wilt dat tooread bevat.<br/><br/><b>Accountsleutel</b>: Hiermee geeft u de opslagsleutel Hallo Hallo-account gekoppeld.<br/><br/><b>Pad toocontainer, map of blob </b> : Hiermee geeft u de naam Hallo van Hallo blob met Hallo gegevens tooread.<br/><br/><b>BLOB-bestandsindeling</b>: Hiermee geeft u de indeling Hallo Hallo gegevens in Hallo blob-service. Hallo ondersteunde indelingen zijn CSV, TSV, ARFF, CSV met een opgegeven codering en Excel. <br/><br/><ul>Als Hallo indeling CSV of TSV, moet u ervoor dat tooindicate of Hallo-bestand een veldnamenrij bevat.<br/><br/>U kunt Hallo optie tooread Excel-gegevens uit Excel-werkmappen gebruiken. In Hallo <i>Excel gegevensindeling</i> optie, geef aan of Hallo gegevens in een Excel-werkblad voor het bereik of in een Excel-tabel is. In Hallo <i>Excel-werkblad of ingesloten tabel </i>optie, Hallo naam opgeven van Hallo blad of de tabel die u wilt dat tooread uit.</ul><br/> |
| Feed-gegevensprovider |Leest de gegevens van een ondersteunde provider van de feed. Momenteel wordt alleen Hallo Open Data Protocol (OData)-indeling wordt ondersteund. |<b>Gegevens inhoudstype</b>: Hiermee geeft u Hallo OData-indeling.<br/><br/><b>Bron-URL</b>: geeft de volledige URL Hallo voor Hallo gegevensfeed. <br/>Bijvoorbeeld, Hallo volgende URL gelezen uit de voorbeelddatabase Northwind Hallo: http://services.odata.org/northwind/northwind.svc/ |

## <a name="next-steps"></a>Volgende stappen

[Azure ML webservices die gebruikmaken van gegevens importeren en exporteren van gegevens modules implementeren](machine-learning-web-services-that-use-import-export-modules.md)


<!-- Module References -->
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
[export-data]: https://msdn.microsoft.com/library/azure/7A391181-B6A7-4AD4-B82D-E419C0D6522C/

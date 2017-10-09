---
title: aaaGet gestart met een voorbeeld van HBase op HDInsight - Azure | Microsoft Docs
description: Volg deze Apache HBase voorbeeld toostart met hadoop op HDInsight. Tabellen maken van Hallo HBase-shell en hierin zoeken met Hive.
keywords: hbase-opdracht, hbase-voorbeeld
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 4d6a2658-6b19-4268-95ee-822890f5a33a
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/17/2017
ms.author: jgao
ms.openlocfilehash: 43419780142b320b16180a2b1f25020dee2f7a11
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-an-apache-hbase-example-in-hdinsight"></a>Aan de slag met een voorbeeld van Apache HBase in HDInsight

Ontdek hoe toocreate een HBase-cluster in HDInsight, HBase-tabellen maken en query uitvoeren op tabellen met Hive. Zie [Overzicht van HDInsight HBase][hdinsight-hbase-overview] voor algemene informatie over HBase.

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="prerequisites"></a>Vereisten
Voordat u probeert deze HBase-voorbeeld, hebt u de volgende items Hallo:

* **Een Azure-abonnement**. Zie [Gratis proefversie van Azure ophalen](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* [Secure Shell (SSH)](hdinsight-hadoop-linux-use-ssh-unix.md). 
* [curl](http://curl.haxx.se/download.html).

## <a name="create-hbase-cluster"></a>Een HBase-cluster maken
Hallo volgende procedure maakt gebruik van een Azure Resource Manager-sjabloon toocreate een versie 3.4 op basis van Linux HBase-cluster en Hallo afhankelijke Azure Storage-standaardaccount. Zie toounderstand Hallo parameters die worden gebruikt in de procedure Hallo en andere methoden voor het maken van cluster [maken Linux gebaseerde Hadoop-clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).

1. Klik op Hallo installatiekopie tooopen Hallo sjabloon in hello Azure-portal te volgen. Hallo-sjabloon bevindt zich in een openbare blob-container. 
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-hbase-linux%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-hbase-tutorial-get-started-linux/deploy-to-azure.png" alt="Deploy tooAzure"></a>
2. Van Hallo **aangepaste implementatie** blade Voer Hallo volgende waarden:
   
   * **Abonnement**: Selecteer uw Azure-abonnement dat is gebruikt toocreate Hallo-cluster.
   * **Resourcegroep**: maak een Azure-resourcebeheergroep of gebruik een bestaande.
   * **Locatie**: locatie van resourcegroep Hallo Hallo opgeven. 
   * **Clusternaam**: Voer een naam voor Hallo HBase-cluster.
   * **Cluster-aanmeldingsnaam en wachtwoord**: Hallo standaardaanmeldnaam is **admin**.
   * **SSH-gebruikersnaam en wachtwoord**: de standaardgebruikersnaam Hallo **sshuser**.  U kunt de naam wijzigen.
     
     Andere parameters zijn optioneel.  
     
     Elk cluster is afhankelijk van een Azure Storage-account. Nadat u een cluster hebt verwijderd, behoudt Hallo gegevens in Hallo storage-account. Hallo clusternaam van het standaardopslagaccount is Hallo naam waaraan 'store' is toegevoegd. Deze is vastgelegd in de sectie met sjabloonvariabelen Hallo.
3. Selecteer **ik ga akkoord toohello voorwaarden bovengenoemde**, en klik vervolgens op **aankoop**. Het duurt ongeveer 20 minuten toocreate een cluster.

> [!NOTE]
> Nadat een HBase-cluster wordt verwijderd, kunt u een ander HBase-cluster maken met behulp van Hallo dezelfde standaard blob-container. het nieuwe cluster Hallo hervat Hallo HBase-tabellen die u hebt gemaakt in het oorspronkelijke cluster Hallo. tooavoid inconsistenties, we raden aan Hallo HBase-tabellen uit te schakelen voordat u het Hallo-cluster verwijderen.
> 
> 

## <a name="create-tables-and-insert-data"></a>Tabellen maken en gegevens invoegen
U kunt SSH tooconnect tooHBase clusters gebruiken en gebruik vervolgens de HBase-Shell toocreate HBase-tabellen, gegevens en gegevens opvragen invoegen. Zie [SSH gebruiken met HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) voor meer informatie.

Gegevens worden weergegeven voor de meeste mensen in tabelvorm Hallo:

![Tabelgegevens in HDInsight HBase][img-hbase-sample-data-tabular]

In HBase (een implementatie van BigTable) lijkt hello dezelfde gegevens:

![BigTable-gegevens in HDInsight HBase][img-hbase-sample-data-bigtable]


**toouse hello HBase-shell**

1. Voer Hallo na HBase-opdracht uit in SSH:
   
    ```bash
    hbase shell
    ```

2. Maak een HBase met twee kolomfamilies:

    ```hbaseshell   
    create 'Contacts', 'Personal', 'Office'
    list
    ```
3. Voeg enkele gegeven in:
    
    ```hbaseshell   
    put 'Contacts', '1000', 'Personal:Name', 'John Dole'
    put 'Contacts', '1000', 'Personal:Phone', '1-425-000-0001'
    put 'Contacts', '1000', 'Office:Phone', '1-425-000-0002'
    put 'Contacts', '1000', 'Office:Address', '1111 San Gabriel Dr.'
    scan 'Contacts'
    ```
   
    ![HDInsight Hadoop HBase-shell][img-hbase-shell]
4. Een enkel rij ophalen
   
    ```hbaseshell
    get 'Contacts', '1000'
    ```
   
    U ziet Hallo dezelfde resultaten als het gebruik van de scanopdracht Hallo omdat er slechts één rij.
   
    Zie voor meer informatie over Hallo HBase-tabelschema [inleiding tooHBase schemaontwerp][hbase-schema]. Raadpleeg de [Snelzoekgids voor Apache HBase][hbase-quick-start] voor meer HBase-opdrachten.
5. Hallo-shell afsluiten
   
    ```hbaseshell
    exit
    ```

**toobulk load gegevens in HBase-tabel met contacten Hallo**

U kunt in HBase verschillende methoden gebruiken om gegevens in tabellen te laden.  Zie [Bulk loading](http://hbase.apache.org/book.html#arch.bulk.load) (Bulkgsgewijs laden) voor meer informatie.

Een voorbeeld van een gegevensbestand is te vinden in een openbare Azure Blob-container, *wasb://hbasecontacts@hditutorialdata.blob.core.windows.net/contacts.txt*.  Hallo-inhoud van het gegevensbestand Hallo is:

    8396    Calvin Raji      230-555-0191    230-555-0191    5415 San Gabriel Dr.
    16600   Karen Wu         646-555-0113    230-555-0192    9265 La Paz
    4324    Karl Xie         508-555-0163    230-555-0193    4912 La Vuelta
    16891   Jonn Jackson     674-555-0110    230-555-0194    40 Ellis St.
    3273    Miguel Miller    397-555-0155    230-555-0195    6696 Anchor Drive
    3588    Osa Agbonile     592-555-0152    230-555-0196    1873 Lion Circle
    10272   Julia Lee        870-555-0110    230-555-0197    3148 Rose Street
    4868    Jose Hayes       599-555-0171    230-555-0198    793 Crawford Street
    4761    Caleb Alexander  670-555-0141    230-555-0199    4775 Kentucky Dr.
    16443   Terry Chander    998-555-0171    230-555-0200    771 Northridge Drive

U kunt desgewenst een tekstbestand maken en uploaden Hallo bestand tooyour eigen opslagaccount. Zie voor instructies Hallo [gegevens voor Hadoop-taken in HDInsight uploaden][hdinsight-upload-data].

> [!NOTE]
> Deze procedure maakt gebruik van Hallo contactpersonen HBase-tabel die u hebt gemaakt in de laatste procedure Hallo.
> 

1. Uitvoeren vanuit SSH Hallo opdracht tootransform Hallo gegevens bestand tooStoreFiles en op te slaan op een relatief pad is opgegeven door Dimporttsv.bulk.output te volgen.  Als u zich in HBase-Shell, gebruikt u Hallo afsluiten opdracht tooexit.

    ```bash   
    hbase org.apache.hadoop.hbase.mapreduce.ImportTsv -Dimporttsv.columns="HBASE_ROW_KEY,Personal:Name,Personal:Phone,Office:Phone,Office:Address" -Dimporttsv.bulk.output="/example/data/storeDataFileOutput" Contacts wasb://hbasecontacts@hditutorialdata.blob.core.windows.net/contacts.txt
    ```

2. Voer Hallo volgende opdracht tooupload Hallo gegevens uit/storedatafileoutput toohello HBase-tabel:
   
    ```bash
    hbase org.apache.hadoop.hbase.mapreduce.LoadIncrementalHFiles /example/data/storeDataFileOutput Contacts
    ```

3. U kunt Hallo HBase-shell openen en Hallo scan opdracht toolist Hallo tabelinhoud gebruiken.

## <a name="use-hive-tooquery-hbase"></a>Gebruik Hive tooquery HBase

Met Hive kunt u een query uitvoeren op de gegevens in HBase-tabellen. In deze sectie maakt u een Hive-tabel die wordt toegewezen toohello HBase-tabel en gebruikt deze tooquery Hallo gegevens in uw HBase-tabel.

1. Open **PuTTY**, en maak verbinding toohello cluster.  Zie Hallo-instructies in de vorige procedure Hallo.
2. Gebruik van Hallo SSH-sessie, Hallo opdracht toostart Beeline te volgen:

    ```bash
    beeline -u 'jdbc:hive2://localhost:10001/;transportMode=http' -n admin
    ```

    Zie voor meer informatie over Beeline [Hive gebruiken met Hadoop in HDInsight met Beeline](hdinsight-hadoop-use-hive-beeline.md).
       
3. Voer Hallo volgende HiveQL-script toocreate een Hive-tabel die is toegewezen toohello HBase-tabel. Zorg ervoor dat u hebt gemaakt dat Hallo voorbeeldtabel waarnaar eerder in deze zelfstudie Hallo HBase-shell met voordat u deze instructie uitvoert.

    ```hiveql   
    CREATE EXTERNAL TABLE hbasecontacts(rowkey STRING, name STRING, homephone STRING, officephone STRING, officeaddress STRING)
    STORED BY 'org.apache.hadoop.hive.hbase.HBaseStorageHandler'
    WITH SERDEPROPERTIES ('hbase.columns.mapping' = ':key,Personal:Name,Personal:Phone,Office:Phone,Office:Address')
    TBLPROPERTIES ('hbase.table.name' = 'Contacts');
    ```

4. Hallo volgende HiveQL-script tooquery Hallo gegevens in HBase-tabel Hallo uitvoeren:

    ```hiveql   
    SELECT count(rowkey) FROM hbasecontacts;
    ```

## <a name="use-hbase-rest-apis-using-curl"></a>HBase REST API's gebruiken met Curl

Hallo REST API is beveiligd via [basisverificatie](http://en.wikipedia.org/wiki/Basic_access_authentication). U moet aanvragen altijd maken met behulp van beveiligde HTTP (HTTPS) toohelp ervoor te zorgen dat uw referenties veilig toohello server worden verzonden.

2. Gebruik Hallo opdracht toolist Hallo bestaande HBase-tabellen te volgen:

    ```bash
    curl -u <UserName>:<Password> \
    -G https://<ClusterName>.azurehdinsight.net/hbaserest/
    ```

3. Gebruik Hallo opdracht toocreate een nieuwe HBase-tabel met twee kolomfamilies te volgen:

    ```bash   
    curl -u <UserName>:<Password> \
    -X PUT "https://<ClusterName>.azurehdinsight.net/hbaserest/Contacts1/schema" \
    -H "Accept: application/json" \
    -H "Content-Type: application/json" \
    -d "{\"@name\":\"Contact1\",\"ColumnSchema\":[{\"name\":\"Personal\"},{\"name\":\"Office\"}]}" \
    -v
    ```

    Hallo-schema is opgegeven in Hallo JSon-indeling.
4. Gebruik Hallo volgende opdracht tooinsert sommige gegevens:

    ```bash   
    curl -u <UserName>:<Password> \
    -X PUT "https://<ClusterName>.azurehdinsight.net/hbaserest/Contacts1/false-row-key" \
    -H "Accept: application/json" \
    -H "Content-Type: application/json" \
    -d "{\"Row\":[{\"key\":\"MTAwMA==\",\"Cell\": [{\"column\":\"UGVyc29uYWw6TmFtZQ==\", \"$\":\"Sm9obiBEb2xl\"}]}]}" \
    -v
    ```
   
    U moet base64 Hallo opgegeven waarden in Hallo -d switch coderen. In het Hallo-voorbeeld:
   
   * MTAwMA==: 1000
   * UGVyc29uYWw6TmFtZQ==: Persoonlijk:Naam
   * Sm9obiBEb2xl: Joep Davids
     
     [False rijsleutel](https://hbase.apache.org/apidocs/org/apache/hadoop/hbase/rest/package-summary.html#operation_cell_store_single) tooinsert, kunt u meerdere waarden voor (batch).
5. Gebruik Hallo opdracht tooget een rij te volgen:
   
    ```bash 
    curl -u <UserName>:<Password> \
    -X GET "https://<ClusterName>.azurehdinsight.net/hbaserest/Contacts1/1000" \
    -H "Accept: application/json" \
    -v
    ```

Zie [Apache HBase Reference Guide](https://hbase.apache.org/book.html#_rest) (Snelzoekgids voor Apache HBase) voor meer informatie over HBase REST.

> [!NOTE]
> Thrift wordt niet ondersteund door HBase in HDInsight.
>
> Wanneer u Curl of andere REST-communicatie met WebHCat, moet u Hallo aanvragen verifiëren door het Hallo-gebruikersnaam en wachtwoord voor Hallo HDInsight Clusterbeheer. Als onderdeel van Hallo Uniform Resource Identifier (URI) toosend Hallo aanvragen toohello server gebruikt, moet u de clusternaam hello gebruiken:
> 
>   
>        curl -u <UserName>:<Password> \
>        -G https://<ClusterName>.azurehdinsight.net/templeton/v1/status
>   
>    U ontvangt een reactie vergelijkbaar toohello antwoord te volgen:
>   
>        {"status":"ok","version":"v1"}
   


## <a name="check-cluster-status"></a>De clusterstatus controleren
HBase in HDInsight wordt geleverd met een webgebruikersinterface voor het bewaken van clusters. Hallo Webgebruikersinterface gebruikt, kunt u statistieken of informatie over regio's aanvragen.

**tooaccess hello HBase Master UI**

1. Meld u aan bij Hallo Hallo Ambari-Webgebruikersinterface op https://&lt;Clustername >. azurehdinsight.net.
2. Klik op **HBase** in het linkermenu Hallo.
3. Klik op **snelle koppelingen** op Hallo bovenaan pagina hello, punt toohello actieve Zookeeper knooppunt koppeling, en klik vervolgens op **HBase Master UI**.  Hallo gebruikersinterface in een ander browsertabblad wordt geopend:

  ![HDInsight HBase HMaster-interface](./media/hdinsight-hbase-tutorial-get-started-linux/hdinsight-hbase-hmaster-ui.png)

  Hallo HBase Master UI bevat Hallo uit te voeren:

  - regioservers
  - back-upmasters
  - tabellen
  - taken
  - softwarekenmerken

## <a name="delete-hello-cluster"></a>Hallo-cluster verwijderen
tooavoid inconsistenties, we raden aan Hallo HBase-tabellen uit te schakelen voordat u het Hallo-cluster verwijderen.

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="troubleshoot"></a>Problemen oplossen

Zie [Vereisten voor toegangsbeheer](hdinsight-administer-use-portal-linux.md#create-clusters) als u problemen ondervindt met het maken van HDInsight-clusters.

## <a name="next-steps"></a>Volgende stappen
In dit artikel hebt u geleerd hoe toocreate een HBase-cluster en hoe toocreate tabellen en weergaven gegevens in deze tabellen vanuit Hallo Hallo HBase-shell. U hebt ook geleerd hoe toouse een Hive query uitvoeren op gegevens in HBase-tabellen en hoe toouse HBase C# REST API's toocreate Hallo een HBase-tabel en gegevens ophalen uit de tabel Hallo.

toolearn meer, Zie:

* [Overzicht van HDInsight HBase][hdinsight-hbase-overview]: HBase is een Apache, open-source NoSQL-database op basis van Hadoop. HBase biedt willekeurige toegang en een sterke consistentie voor grote hoeveelheden ongestructureerde en semigestructureerde gegevens.

[hdinsight-manage-portal]: hdinsight-administer-use-management-portal.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hbase-reference]: http://hbase.apache.org/book.html#importtsv
[hbase-schema]: http://0b4af6cdc2f0c5998459-c0245c5c937c5dedcca3f1764ecc9b2f.r43.cf2.rackcdn.com/9353-login1210_khurana.pdf
[hbase-quick-start]: http://hbase.apache.org/book.html#quickstart





[hdinsight-hbase-overview]: hdinsight-hbase-overview.md
[hdinsight-hbase-provision-vnet]: hdinsight-hbase-provision-vnet.md
[hdinsight-versions]: hdinsight-component-versioning.md
[hbase-twitter-sentiment]: hdinsight-hbase-analyze-twitter-sentiment.md
[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[azure-portal]: https://portal.azure.com/
[azure-create-storageaccount]: http://azure.microsoft.com/documentation/articles/storage-create-storage-account/

[img-hdinsight-hbase-cluster-quick-create]: ./media/hdinsight-hbase-tutorial-get-started-linux/hdinsight-hbase-quick-create.png
[img-hdinsight-hbase-hive-editor]: ./media/hdinsight-hbase-tutorial-get-started-linux/hdinsight-hbase-hive-editor.png
[img-hdinsight-hbase-file-browser]: ./media/hdinsight-hbase-tutorial-get-started-linux/hdinsight-hbase-file-browser.png
[img-hbase-shell]: ./media/hdinsight-hbase-tutorial-get-started-linux/hdinsight-hbase-shell.png
[img-hbase-sample-data-tabular]: ./media/hdinsight-hbase-tutorial-get-started-linux/hdinsight-hbase-contacts-tabular.png
[img-hbase-sample-data-bigtable]: ./media/hdinsight-hbase-tutorial-get-started-linux/hdinsight-hbase-contacts-bigtable.png

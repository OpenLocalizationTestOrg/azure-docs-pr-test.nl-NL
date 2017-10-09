---
title: beleid voor het Hive in HDInsight domein - Azure aaaConfigure | Microsoft Docs
description: Meer informatie...
services: hdinsight
documentationcenter: 
author: saurinsh
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 3fade1e5-c2e1-4ad5-b371-f95caea23f6d
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 10/25/2016
ms.author: saurinsh
ms.openlocfilehash: 56f2bf9d872abc5f772b886fcf91c2e2422092f4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-hive-policies-in-domain-joined-hdinsight-preview"></a>Hive-beleidsregels configureren in HDInsight dat is gekoppeld aan een domein (voorbeeld)
Meer informatie over hoe tooconfigure Apache Zwerver beleidsregels voor Hive. In dit artikel maakt u twee Zwerver beleid toorestrict toegang toohello hivesampletable. Hallo hivesampletable wordt geleverd met HDInsight-clusters. Nadat u Hallo beleidsregels hebt geconfigureerd, gebruikt u Excel en ODBC-stuurprogramma tooconnect tooHive tabellen in HDInsight.

## <a name="prerequisites"></a>Vereisten
* Een HDInsight-cluster dat is gekoppeld aan een domein. Zie [Configure Domain-joined HDInsight clusters](hdinsight-domain-joined-configure.md) (Aan een domein gekoppelde HDInsight-clusters configureren).
* Een werkstation met Office 2016, Office 2013 Professional Plus, Office 365 Pro Plus, een zelfstandige versie van Excel 2013 of Office 2010 Professional Plus.

## <a name="connect-tooapache-ranger-admin-ui"></a>Verbinding maken met tooApache Zwerver Admin-gebruikersinterface
**tooconnect tooRanger Admin UI**

1. Verbinding via een browser tooRanger Admin UI. Hallo-URL is https://&lt;ClusterName >.azurehdinsight.net/Ranger/.

   > [!NOTE]
   > Ranger maakt gebruik van andere referenties dan het Hadoop-cluster. tooprevent browsers referenties uit de cache Hadoop, met nieuwe InPrivate-browser venster tooconnect toohello Zwerver Admin gebruikersinterface gebruiken.
   >
   >
2. Meld u aan met Hallo cluster administrator domeingebruikersnaam en wachtwoord:

    ![Ranger-startpagina van HDInsight dat is gekoppeld aan een domein](./media/hdinsight-domain-joined-run-hive/hdinsight-domain-joined-ranger-home-page.png)

    Op dit moment werkt Ranger alleen met Yarn en Hive.

## <a name="create-domain-users"></a>Domeingebruikers maken
In [Configure Domain-joined HDInsight clusters](hdinsight-domain-joined-configure.md#create-and-configure-azure-ad-ds-for-your-azure-ad) (Aan een domein gekoppelde HDInsight-clusters configureren) hebt u hiveruser1 en hiveuser2 gemaakt. U gebruikt twee Hallo-gebruikersaccount in deze zelfstudie.

## <a name="create-ranger-policies"></a>Ranger-beleidsregels maken
In deze sectie maakt u twee Ranger-beleidsregels voor toegang tot de hivesampletable. U geeft de machtiging SELECT op voor verschillende sets kolommen. Beide gebruikers zijn gemaakt in [Configure Domain-joined HDInsight clusters](hdinsight-domain-joined-configure.md#create-and-configure-azure-ad-ds-for-your-azure-ad) (Aan een domein gekoppelde HDInsight-clusters configureren).  In de volgende sectie hello, wordt u testen Hallo twee beleidsregels in Excel.

**toocreate Zwerver beleid**

1. Open de beheerinterface van Ranger. Zie [tooApache Zwerver Admin gebruikersinterface verbinding](#connect-to-apache-ranager-admin-ui).
2. Klik op **&lt;ClusterName>_hive** onder **Hive**. Er worden twee vooraf geconfigureerde beleidsregels weergegeven.
3. Klik op **nieuw beleid toevoegen**, en voer vervolgens Hallo volgende waarden:

   * Beleidsnaam: read-hivesampletable-all
   * Hive-database: standaard
   * Tabel: hivesampletable
   * Hive-kolom:*
   * Gebruiker selecteren: hiveuser1
   * Machtigingen: SELECT

     ![Ranger Hive-beleidsregels van HDInsight dat is gekoppeld aan een domein configureren](./media/hdinsight-domain-joined-run-hive/hdinsight-domain-joined-configure-ranger-policy.png).

     > [!NOTE]
     > Als een domeingebruiker niet is ingevuld in Select User, wacht u enkele ogenblikken voor Zwerver toosync bij AAD.
     >
     >
4. Klik op **toevoegen** toosave Hallo beleid.
5. Hallo laatste twee stappen toocreate een ander beleid met de volgende eigenschappen Hallo herhalen:

   * Beleidsnaam: read-hivesampletable-devicemake
   * Hive-database: standaard
   * Tabel: hivesampletable
   * Hive-kolom: clientid, devicemake
   * Gebruiker selecteren: hiveuser2
   * Machtigingen: SELECT

## <a name="create-hive-odbc-data-source"></a>Hive ODBC-gegevensbron maken
Hallo-instructies vindt u in [maken Hive ODBC-gegevensbron](hdinsight-connect-excel-hive-odbc-driver.md).  

    Eigenschap|Beschrijving
    ---|---
    Naam van de gegevensbron|Geef een naam tooyour-gegevensbron
    Host|Voer &lt;HDInsightClusterName>.azurehdinsight.net in. Bijvoorbeeld: myHDICluster.azurehdinsight.net
    Poort|Gebruik <strong>443</strong>. (Deze poort is gewijzigd van 563 too443.)
    Database|Gebruik <strong>Standaard</strong>.
    Type Hive-server|Selecteer <strong>Hive Server 2</strong>
    Mechanisme|Selecteer <strong>Azure HDInsight Service</strong>
    HTTP-pad|Laat dit leeg.
    Gebruikersnaam|Voer hiveuser1@contoso158.onmicrosoft.com. Hallo-domeinnaam bijwerken als deze verschilt.
    Wachtwoord|Hallo wachtwoord opgeven voor hiveuser1.
    </table>

Zorg ervoor dat tooclick **Test** voordat u opslaat Hallo-gegevensbron.

## <a name="import-data-into-excel-from-hdinsight"></a>Gegevens in Excel importeren vanuit HDInsight
In de laatste sectie hello, kunt u twee beleidsregels hebt geconfigureerd.  hiveuser1 heeft Hallo machtiging voor alle Hallo kolommen te selecteren en hiveuser2 Hallo machtiging op twee kolommen te selecteren. In deze sectie imiteren u Hallo twee gebruikers tooimport gegevens in Excel.

1. Open een nieuwe of bestaande werkmap in Excel.
2. Van Hallo **gegevens** tabblad **van andere gegevensbronnen**, en klik vervolgens op **van Wizard Gegevensverbinding** toolaunch hello **Wizard Gegevensverbinding**.

    ![Open de Wizard Gegevensverbinding][img hdi simbahiveodbc.excel.dataconnection]
3. Selecteer **ODBC DSN** als Hallo gegevensbron en klik op **volgende**.
4. Van ODBC-gegevensbronnen, selecteer Hallo gegevensbron naam die u hebt gemaakt in de vorige stap Hallo en klik vervolgens op **volgende**.
5. Wachtwoord voor Hallo-cluster in de wizard Hallo Hallo opnieuw invoeren en klik vervolgens op **OK**. Wachten op Hallo **Database en tabel selecteren** dialoogvenster tooopen. Dit kan een paar seconden duren.
6. Selecteer **hivesampletable** en klik op **Volgende**.
7. Klik op **Voltooien**.
8. In Hallo **importgegevens** dialoogvenster kunt u wijzigen of Hallo query opgeven. toodo hiervoor, klikt u op **eigenschappen**. Dit kan een paar seconden duren.
9. Klik op Hallo **definitie** tabblad Hallo opdrachttekst is:

       SELECT * FROM "HIVE"."default"."hivesampletable"

   Hallo Zwerver beleid dat u hebt gedefinieerd, heeft hiveuser1 machtiging select voor alle Hallo-kolommen.  Deze query werkt dus met de referenties van hiveuser1, maar niet met de referenties van hiveuser2.

   ![Verbindingseigenschappen][img-hdi-simbahiveodbc-excel-connectionproperties]
10. Klik op **OK** tooclose Hallo verbindingseigenschappen dialoogvenster.
11. Klik op **OK** tooclose hello **importgegevens** dialoogvenster.  
12. Hallo-wachtwoord voor hiveuser1 opnieuw op en klik vervolgens op **OK**. Het duurt een paar seconden voordat gegevens geïmporteerde tooExcel opgehaald. Wanneer dit is voltooid, worden er 11 kolommen met gegevens weergegeven.

tootest hello tweede beleid (lezen hivesampletable devicemake) die u hebt gemaakt in de laatste sectie Hallo

1. Voeg een nieuw blad in Excel toe.
2. Ga als volgt Hallo laatste procedure tooimport Hallo gegevens.  Hallo enige wijziging die u neemt is toouse hiveuser2 van referenties in plaats van hiveuser1 van. Dit zal mislukken omdat hiveuser2 alleen machtiging toosee twee kolommen heeft. U moet ophalen Hallo volgende fout:

        [Microsoft][HiveODBC] (35) Error from Hive: error code: '40000' error message: 'Error while compiling statement: FAILED: HiveAccessControlException Permission denied: user [hiveuser2] does not have [SELECT] privilege on [default/hivesampletable/clientid,country ...]'.
3. Volg dezelfde Hallo procedure tooimport gegevens. Deze tijd gebruik hiveuser2 van referenties en Hallo select-instructie uit te wijzigen:

        SELECT * FROM "HIVE"."default"."hivesampletable"

    in:

        SELECT clientid, devicemake FROM "HIVE"."default"."hivesampletable"

    Wanneer dit is voltooid, worden er twee kolommen met geïmporteerde gegevens weergegeven.

## <a name="next-steps"></a>Volgende stappen
* Zie [Configure Domain-joined HDInsight clusters](hdinsight-domain-joined-configure.md) (Aan een domein gekoppelde HDInsight-clusters configureren) om een HDInsight-cluster te configureren dat is gekoppeld aan een domein.
* Zie [Manage Domain-joined HDInsight clusters](hdinsight-domain-joined-manage.md) (Aan een domein gekoppelde HDInsight-clusters beheren) om HDInsight-clusters te beheren die zijn gekoppeld aan een domein.
* Zie voor het uitvoeren van Hive-query's met SSH op domein HDInsight-clusters [SSH gebruiken met HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md#domainjoined).
* Zie voor Hive-verbinding te maken met behulp van Hive JDBC, [verbinding tooHive in Azure HDInsight met behulp van Hallo Hive JDBC-stuurprogramma](hdinsight-connect-hive-jdbc-driver.md)
* Zie voor verbindende Excel tooHadoop met behulp van Hive ODBC [tooHadoop Excel verbinding maken met de Hallo Microsoft Hive ODBC-station](hdinsight-connect-excel-hive-odbc-driver.md)
* Zie voor verbindende Excel tooHadoop met Power Query [tooHadoop Excel verbinding maken met Power Query](hdinsight-connect-excel-power-query.md)

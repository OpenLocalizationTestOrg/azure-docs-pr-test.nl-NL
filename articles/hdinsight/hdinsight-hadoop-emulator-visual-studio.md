---
title: aaaData Lake tools voor Visual Studio met Hortonworks Sandbox - Azure HDInsight | Microsoft Docs
description: Meer informatie over hoe toouse Azure Data Lake tools voor Visual Studio met Hallo Hortonworks sandbox uitgevoerd in een lokale virtuele machine Hallo. U kunt met deze hulpprogramma's, maken en Hive en Pig-taken uitvoeren op Hallo sandbox, en de taakuitvoer weergeven en de geschiedenis.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: e3434c45-95d1-4b96-ad4c-fb59870e2ff0
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/11/2017
ms.author: larryfr
ms.openlocfilehash: 7a3406b28d87d953e9b5be387faa86268f47b935
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-azure-data-lake-tools-for-visual-studio-with-hello-hortonworks-sandbox"></a>Gebruik hello Azure Data Lake tools voor Visual Studio met Hallo Hortonworks Sandbox

Azure Data Lake bevat hulpprogramma's voor het werken met algemene Hadoop-clusters. Dit document bevat Hallo stappen nodig Hallo toouse Hallo Data Lake tools met Hortonworks Sandbox uitgevoerd op een lokale virtuele machine.

Hallo Hortonworks Sandbox met kunt u toowork met Hadoop lokaal op uw ontwikkelomgeving. Nadat u een oplossing hebt ontwikkeld en toodeploy wilt dit op grote schaal, kunt u vervolgens tooan HDInsight-cluster te verplaatsen.

## <a name="prerequisites"></a>Vereisten

* Hello Hortonworks Sandbox, in een virtuele machine wordt uitgevoerd op uw ontwikkelomgeving. Dit document is geschreven en getest met de Hallo sandbox in Oracle VirtualBox uitgevoerd. Zie voor informatie over het instellen van de sandbox Hallo Hallo [aan de slag met Hallo Hortonworks sandbox.](hdinsight-hadoop-emulator-get-started.md) document.

* Visual Studio 2013, Visual Studio 2015 of Visual Studio 2017 (alle versies).

* Hallo [Azure SDK voor .NET](https://azure.microsoft.com/downloads/) 2.7.1 of hoger.

* Hallo [Azure Data Lake tools voor Visual Studio](https://www.microsoft.com/download/details.aspx?id=49504).

## <a name="configure-passwords-for-hello-sandbox"></a>Wachtwoorden voor Hallo sandbox configureren

Zorg ervoor dat Hallo die hortonworks Sandbox wordt uitgevoerd. Volg de stappen Hallo in Hallo [aan de slag in Hallo Hortonworks Sandbox](hdinsight-hadoop-emulator-get-started.md#set-sandbox-passwords) document. Met deze stappen configureert Hallo wachtwoord voor Hallo SSH `root` account en Hallo Ambari `admin` account. Deze wachtwoorden worden gebruikt wanneer u verbinding toohello sandbox vanuit Visual Studio maakt.

## <a name="connect-hello-tools-toohello-sandbox"></a>Verbinding maken met de Hallo extra toohello sandbox

1. Open Visual Studio, selecteer **weergave**, en selecteer vervolgens **Server Explorer**.

2. Van **Server Explorer**, klik met de rechtermuisknop Hallo **HDInsight** vermelding en selecteer vervolgens **tooHDInsight Emulator verbinding**.

    ![Schermopname van Server Explorer, met Connect tooHDInsight Emulator gemarkeerd](./media/hdinsight-hadoop-emulator-visual-studio/connect-emulator.png)

3. Van Hallo **tooHDInsight Emulator verbinding** dialoogvenster Voer Hallo wachtwoord die u hebt geconfigureerd voor Ambari.

    ![Schermopname van dialoogvenster met wachtwoord tekstvak gemarkeerd](./media/hdinsight-hadoop-emulator-visual-studio/enter-ambari-password.png)

    Selecteer **volgende** toocontinue.

4. Gebruik Hallo **wachtwoord** veld tooenter Hallo wachtwoord die u hebt geconfigureerd voor Hallo `root` account. Laat Hallo andere velden Hallo-standaardwaarde.

    ![Schermopname van dialoogvenster met wachtwoord tekstvak gemarkeerd](./media/hdinsight-hadoop-emulator-visual-studio/enter-root-password.png)

    Selecteer **volgende** toocontinue.

5. Validatie van Hallo services toofinish wacht. In sommige gevallen validatie mislukt en wordt u gevraagd tooupdate Hallo configuratie. Als validatie mislukt, selecteert u **Update**, en wachten op het Hallo-configuratie en controle voor Hallo service toofinish.

    ![Schermopname van dialoogvenster met de knop bijwerken gemarkeerd](./media/hdinsight-hadoop-emulator-visual-studio/fail-and-update.png)

    > [!NOTE]
    > Hallo updateproces Ambari toomodify hello Hortonworks Sandbox configuratie toowhat wordt verwacht door Hallo Data Lake tools voor Visual Studio gebruikt.

6. Nadat de validatie is voltooid, selecteert u **voltooien** toocomplete configuratie.
    ![Schermopname van dialoogvenster met de knop Voltooien gemarkeerd](./media/hdinsight-hadoop-emulator-visual-studio/finished-connect.png)

     >[!NOTE]
     > Afhankelijk van Hallo snelheid van uw ontwikkelomgeving en Hallo en de hoeveelheid geheugen toegewezen toohello virtuele machine, kan het tooconfigure van enkele minuten duren en Hallo services valideren.

Na deze stappen uitvoert, hebt u nu een **lokale HDInsight-cluster** vermelding in Server Explorer, onder Hallo **HDInsight** sectie.

## <a name="write-a-hive-query"></a>Een Hive-query schrijven

Hive biedt een SQL-achtige query language (HiveQL) voor het werken met gestructureerde gegevens. Volgende stappen toolearn hoe toorun op aanvraag een query op de lokale cluster Hallo Hallo gebruiken.

1. In **Server Explorer**, met de rechtermuisknop op het Hallo-vermelding voor het lokale cluster Hallo die u eerder hebt toegevoegd en selecteer vervolgens **een Hive-Query schrijven**.

    ![Schermopname van Server Explorer en schrijven naar een Hive-Query gemarkeerd](./media/hdinsight-hadoop-emulator-visual-studio/write-hive-query.png)

    Een nieuwe queryvenster wordt weergegeven. Hier kunt u snel schrijven en het verzenden van een query toohello lokaal cluster.

2. Voer in het nieuwe queryvenster hello, Hallo volgende opdracht:

        select count(*) from sample_08;

    toorun hello query, selecteer **indienen** Hallo boven aan het Hallo-venster. Laat Hallo andere waarden (**Batch** en servernaam) op Hallo standaardwaarden.

    ![Schermafbeelding van de query-venster met de knop verzenden Hallo gemarkeerd](./media/hdinsight-hadoop-emulator-visual-studio/submit-hive.png)

    U kunt ook de vervolgkeuzelijst Hallo naast te**indienen** tooselect **Geavanceerd**. Geavanceerde opties kunnen u extra opties tooprovide wanneer u de taak Hallo indient.

    ![Schermopname van Submit Script dialoogvenster](./media/hdinsight-hadoop-emulator-visual-studio/advanced-hive.png)

3. Nadat u Hallo query verzonden, wordt de taakstatus Hallo weergegeven. Hallo taakstatus geeft informatie weer over Hallo taak terwijl deze wordt verwerkt door Hadoop. **Taakstatus** Hallo Hallo taak status bevat. Hallo status wordt regelmatig bijgewerkt of u kunt de status van Hallo vernieuwen pictogram toorefresh Hallo handmatig gebruiken.

    ![Schermafbeelding van de weergave van de taak in het dialoogvenster met de status van de taak is gemarkeerd](./media/hdinsight-hadoop-emulator-visual-studio/job-state.png)

    Na het Hallo **taakstatus** wijzigingen te**voltooid**, een omgeleid acyclische grafiek (DAG) wordt weergegeven. Dit diagram beschrijft Hallo uitvoeringspad dat is bepaald door de Tez bij het verwerken van Hallo Hive-query. Tez is Hallo standaard engine voor het uitvoeren voor Hive op Hallo lokale cluster.

    > [!NOTE]
    > Tez is ook Hallo standaard wanneer u van Linux gebaseerde HDInsight-clusters gebruikmaakt. Het is niet standaard op HDInsight op basis van Windows hello. toouse deze er, moet u Hallo regel toevoegen `set hive.execution.engine = tez;` toohello begin van uw Hive-query.

    Gebruik Hallo **Taakuitvoer** tooview Hallo uitvoer koppelen. In dit geval is het 823, Hallo aantal rijen in Hallo sample_08 tabel. U kunt diagnostische gegevens over Hallo-taak weergeven met behulp van Hallo **taaklogboek** en **YARN-logboek downloaden** koppelingen.

4. U kunt ook Hive-taken interactief uitvoeren wijzigen Hallo **Batch** veld te**interactief**. Selecteer vervolgens **Execute**.

    ![Schermopname van interactieve en Execute knoppen gemarkeerd](./media/hdinsight-hadoop-emulator-visual-studio/interactive-query.png)

    Een interactieve query streams Hallo logboek gegenereerd tijdens de verwerking toohello **HiveServer2 uitvoer** venster.

    > [!NOTE]
    > Hallo informatie is Hallo dezelfde die beschikbaar is via Hallo **taaklogboek** koppelen nadat een taak is voltooid.

    ![Schermopname van het uitvoerlogboek](./media/hdinsight-hadoop-emulator-visual-studio/hiveserver2-output.png)

## <a name="create-a-hive-project"></a>Een Hive-project maken

U kunt ook een project met meerdere Hive-scripts maken. Een project gebruiken wanneer u scripts gerelateerde of toostore scripts in een versiebeheersysteem wilt.

1. Selecteer in Visual Studio **bestand**, **nieuw**, en vervolgens **Project**.

2. Vouw vanuit Hallo lijst met projecten, **sjablonen**, vouw **Azure Data Lake**, en selecteer vervolgens **HIVE (HDInsight)**. Selecteer in de lijst met sjablonen Hallo **Hive-voorbeeldquery**. Voer een naam en locatie en selecteer vervolgens **OK**.

    ![Schermopname van nieuw Project-venster met Azure Data Lake, HIVE, Hive-voorbeeldquery en OK gemarkeerd](./media/hdinsight-hadoop-emulator-visual-studio/new-hive-project.png)

Hallo **Hive-voorbeeldquery** -project bevat twee scripts **WebLogAnalysis.hql** en **SensorDataAnalysis.hql**. Dient u deze scripts met behulp van dezelfde Hallo **indienen** knop Hallo boven aan het Hallo-venster.

## <a name="create-a-pig-project"></a>Een Pig-project maken

Terwijl Hive een SQL-achtige taal bevat voor het werken met gestructureerde gegevens, werkt de Pig door transformaties uitvoeren op gegevens. Pig biedt een taal (Pig Latin) waarmee u toodevelop een pijplijn van transformaties. toouse Pig met het lokale cluster hello, als volgt te werk:

1. Open Visual Studio en selecteer **bestand**, **nieuw**, en vervolgens **Project**. Vouw vanuit Hallo lijst met projecten, **sjablonen**, vouw **Azure Data Lake**, en selecteer vervolgens **Pig (HDInsight)**. Selecteer in de lijst met sjablonen Hallo **Pig toepassing**. Voer een naam en locatie en selecteer vervolgens **OK**.

    ![Schermopname van nieuw Project-venster met Azure Data Lake, Pig, Pig-toepassing en OK gemarkeerd](./media/hdinsight-hadoop-emulator-visual-studio/new-pig.png)

2. Voer na de tekst hello inhoud Hallo Hallo **script.pig** -bestand dat is gemaakt met dit project.

        a = LOAD '/demo/data/Website/Website-Logs' AS (
            log_id:int,
            ip_address:chararray,
            date:chararray,
            time:chararray,
            landing_page:chararray,
            source:chararray);
        b = FILTER a BY (log_id > 100);
        c = GROUP b BY ip_address;
        DUMP c;

    Pig gebruikmaakt van een andere taal dan Hive, hoe u Hallo taken uitvoeren is consistent tussen de beide talen, via Hallo **indienen** knop. Selecteren Hallo-omlaag naast **indienen** wordt een dialoogvenster Geavanceerd verzenden voor Pig.

    ![Schermopname van Submit Script dialoogvenster](./media/hdinsight-hadoop-emulator-visual-studio/advanced-pig.png)

3. Hallo taakstatus en de uitvoer wordt weergegeven, dezelfde Hallo als een Hive-query.

    ![Schermafbeelding van een voltooide Pig-taak](./media/hdinsight-hadoop-emulator-visual-studio/completed-pig.png)

## <a name="view-jobs"></a>Taken weergeven

Data Lake tools kunnen u ook informatie over taken die zijn uitgevoerd op Hadoop tooeasily weergeven. Volgende stappen toosee Hallo taken die zijn uitgevoerd op de lokale cluster Hallo Hallo gebruiken.

1. Van **Server Explorer**, met de rechtermuisknop op het lokale cluster Hallo en selecteer vervolgens **taken weergeven**. Een lijst met taken die ingediend toohello cluster zijn wordt weergegeven.

    ![Schermopname van Server Explorer met de weergave taken die zijn gemarkeerd](./media/hdinsight-hadoop-emulator-visual-studio/view-jobs.png)

2. Hallo-lijst met taken, selecteer in een tooview Hallo taakdetails.

    ![Schermopname van Job Browser met een Hallo-taken die zijn gemarkeerd](./media/hdinsight-hadoop-emulator-visual-studio/view-job-details.png)

    Hallo-informatie weergegeven is vergelijkbaar toowhat die u na het uitvoeren van een query Hive of Pig, inclusief koppelingen tooview Hallo uitvoer en logboekbestanden informatie zien.

3. U kunt ook wijzigen en opnieuw indienen Hallo taak hier.

## <a name="view-hive-databases"></a>Weergave Hive-databases

1. In **Server Explorer**, vouw Hallo **lokale HDInsight-cluster** -item, en vouw vervolgens **Hive-Databases**. Hallo **standaard** en **xademo** databases op de lokale cluster Hallo worden weergegeven. Uitbreiden van een database bevat Hallo tabellen binnen Hallo-database.

    ![Schermopname van Server Explorer met uitgebreide databases](./media/hdinsight-hadoop-emulator-visual-studio/expanded-databases.png)

2. Uitbreiden van een tabel, worden Hallo kolommen voor die tabel weergegeven. Hallo gegevens van tooquickly weergeven met de rechtermuisknop op een tabel en selecteer **View Top 100 rijen**.

    ![Schermopname van Server Explorer met tabel uitgebreid en View Top 100 rijen geselecteerd](./media/hdinsight-hadoop-emulator-visual-studio/view-100.png)

### <a name="database-and-table-properties"></a>Eigenschappen van de database en tabel

U kunt de eigenschappen van een database of tabel Hallo weergeven. Selecteren **eigenschappen** worden in het venster Eigenschappen Hallo details voor Hallo geselecteerd item weergegeven. Zie bijvoorbeeld Hallo-informatie die wordt weergegeven in de volgende schermafbeelding Hallo:

![Schermopname van eigenschappen venster](./media/hdinsight-hadoop-emulator-visual-studio/properties.png)

### <a name="create-a-table"></a>Een tabel maken

toocreate een tabel met de rechtermuisknop op een database en selecteer vervolgens **Create Table**.

![Schermopname van Server Explorer, met Create Table gemarkeerd](./media/hdinsight-hadoop-emulator-visual-studio/create-table.png)

Vervolgens kunt u met behulp van een formulier Hallo-tabel maken. Hallo onderaan Hallo volgende schermafbeelding ziet u Hallo onbewerkte HiveQL die gebruikte toocreate Hallo tabel.

![Schermopname van Hallo formulier toocreate een tabel die wordt gebruikt](./media/hdinsight-hadoop-emulator-visual-studio/create-table-form.png)

## <a name="next-steps"></a>Volgende stappen

* [Learning Hallo kabels Hallo Hortonworks Sandbox](http://hortonworks.com/hadoop-tutorial/learning-the-ropes-of-the-hortonworks-sandbox/)
* [Hadoop-zelfstudie - aan de slag met HDP](http://hortonworks.com/hadoop-tutorial/hello-world-an-introduction-to-hadoop-hcatalog-hive-and-pig/)

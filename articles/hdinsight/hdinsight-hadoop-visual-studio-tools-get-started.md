---
title: aaaConnect tooAzure HDInsight met behulp van Data Lake Tools voor Visual Studio | Microsoft Docs
description: Meer informatie over hoe tooinstall en gebruik Data Lake Tools voor Visual Studio tooconnect tooHadoop-clusters in Azure HDInsight en Hive-query's uitvoeren.
keywords: hadoop-hulpprogramma's, hive-query, visual studio, visual studio hadoop
services: HDInsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: ce9c572a-1e98-46bf-9581-13a9767f1fa5
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/23/2017
ms.author: jgao
ms.openlocfilehash: ff5819a64bebe5f4ab3cf763ce6c45c81aa34b19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooazure-hdinsight-and-run-hive-queries-using-data-lake-tools-for-visual-studio"></a>Verbinding maken tooAzure HDInsight en uitvoeren van Hive-query's met Data Lake Tools voor Visual Studio

Meer informatie over hoe toouse Data Lake Tools voor Visual Studio tooconnect tooHadoop-clusters in [Azure HDInsight](hdinsight-hadoop-introduction.md) en het verzenden van Hive-query's. Zie voor meer informatie over het gebruik van HDInsight [inleiding tooHDInsight](hdinsight-hadoop-introduction.md) en [aan de slag met HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md). Zie voor meer informatie over het maken van verbinding tooa Storm-cluster [C#-topologieën ontwikkelen voor Apache Storm op HDInsight met behulp van Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).

Data Lake Tools voor Visual Studio kunt gebruikte tooaccess worden zowel Data Lake Analytics en HDInsight.  Zie voor informatie over Data Lake Tools Hallo [zelfstudie: U-SQL-scripts ontwikkelen met Data Lake Tools voor Visual Studio](../data-lake-analytics/data-lake-analytics-data-lake-tools-get-started.md).

**Vereisten**

toocomplete deze zelfstudie en gebruik Hallo Data Lake Tools in Visual Studio, moet u de volgende Hallo:

* Een Azure HDInsight-cluster: één, Zie toocreate [aan de slag met HDInsight op basis van Linux](hdinsight-hadoop-linux-tutorial-get-started.md)
* Een werkstation met Hallo software te volgen:
  
  * Windows 10, Windows 8.1, Windows 8 of Windows 7.
  * Visual Studio 2013/2015/2017.
    
    > [!NOTE]
    > Op dit moment Hallo Data Lake Tools voor Visual Studio alleen geleverd bij de Engelse versie Hallo.
    > 
    > 

## <a name="install-data-lake-tools-for-visual-studio"></a>Data Lake Tools voor Visual Studio installeren

Data Lake Tools is standaard geïnstalleerd voor Visual Studio 2017. Voor oudere versies kunt u installeren met behulp van Hallo [Web Platform Installer](https://www.microsoft.com/web/downloads/). U moet kiezen Hallo dat het overeenkomt met uw versie van Visual Studio. Als u geen Visual Studio is geïnstalleerd, kunt u installeren Hallo meest recente Visual Studio Community en Azure SDK met de Hallo [Web Platform Installer](https://www.microsoft.com/web/downloads/):

![Data Lake Tools voor Visual Studio Web Platform installer. ] (./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.wpi.png "Gebruik Web Platform Installer tooinstall Data Lake Tools voor Visual Studio")

## <a name="connect-tooazure-subscriptions"></a>Verbinding maken met tooAzure abonnementen
Data Lake Tools voor Visual Studio, u tooconnect tooyour HDInsight-clusters kunt, enkele eenvoudige beheerbewerkingen uitvoeren en Hive-query's uitvoeren.

> [!NOTE]
> Zie voor informatie over het maken van verbinding tooa algemeen Hadoop-cluster, [schrijven en het verzenden van Hive-query's met Visual Studio](http://blogs.msdn.com/b/xiaoyong/archive/2015/05/04/how-to-write-and-submit-hive-queries-using-visual-studio.aspx).
> 
> 

**tooconnect tooyour Azure-abonnement**

1. Open Visual Studio.
2. Van Hallo **weergave** menu, klikt u op **Server Explorer** tooopen Hallo Server Explorer-venster.
3. Vouw **Azure** uit en vouw vervolgens **HDInsight** uit.
   
   > [!NOTE]
   > Kennisgeving Hallo **taakoverzicht HDInsight** venster moet geopend zijn. Als u deze niet ziet, klikt u op **overige vensters** van Hallo **weergave** menu en klik vervolgens op **HDInsight-taak lijstvenster**.  
   > 
   > 
4. Voer de referenties voor uw Azure-abonnement in en klik vervolgens op **Aanmelden**. Dit is alleen vereist als u nog nooit een verbinding toohello Azure-abonnement vanuit Visual Studio op dit werkstation.
5. In Server Explorer wordt een lijst met bestaande HDInsight-clusters weergegeven. Als u niet alle clusters hebt, kunt u een via hello Azure-portal, Azure PowerShell of Hallo HDInsight SDK. Zie [HDInsight-clusters maken](hdinsight-hadoop-provision-linux-clusters.md) voor meer informatie.
   
   ![Lijst met clusters in Server Explorer van Data Lake Tools voor Visual Studio](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.server.explorer.png "Server Explorer van Data Lake Tools voor Visual Studio")
6. Een HDInsight-cluster uitbreiden. U ziet **Hive-databases**, een standaardopslagaccount, gekoppelde opslagaccounts en een **Hadoop Service-logboekbestand**. U kunt Hallo entiteiten verder uitbreiden.

Nadat u tooyour Azure-abonnement hebt verbonden, moet u kunnen toodo Hallo volgende:

**tooconnect toohello Azure-portal vanuit Visual Studio**

* Vouw in Server Explorer **Azure** > **HDInsight** uit, klik met de rechtermuisknop op een HDInsight-cluster en klik vervolgens op **Cluster beheren in Azure Portal**.

**tooask vragen en feedback geven vanuit Visual Studio**

* Van Hallo **extra** menu, klikt u op **HDInsight**, en klik vervolgens op **MSDN-Forum** tooask vragen, of klik op **Feedback geven**.

## <a name="navigate-hello-linked-resources"></a>Hallo gekoppelde resources navigeren
In Server Explorer ziet u het standaardopslagaccount hello en alle gekoppelde opslagaccounts weergegeven. Als u Hallo standaardopslagaccount uitvouwt, ziet u Hallo containers op Hallo storage-account. Hallo storage-standaardaccount en Hallo standaardcontainer worden gemarkeerd. U kunt ook met de rechtermuisknop op een van de Hallo containers tooview Hallo inhoud.

![Lijst met gekoppelde resources in Server Explorer van Data Lake Tools voor Visual Studio](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.linked.resources.png "lijst met gekoppelde resources")

Na het openen van een container, kunt u Hallo knoppen tooupload, verwijderen en de blobs downloaden te volgen:

![Blob-bewerkingen in Server Explorer van Data Lake Tools voor Visual Studio](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.blob.operations.png "blobs uploaden, verwijderen en downloaden")

## <a name="run-a-hive-query"></a>Een Hive-query uitvoeren
[Apache Hive](http://hive.apache.org) is een datawarehouse-infrastructuur die is gebouwd op Hadoop om overzichten, query's en analyses te leveren. Data Lake Tools voor Visual Studio biedt ondersteuning voor het uitvoeren van Hive-query's vanuit Visual Studio. Zie [Hive gebruiken met HDInsight](hdinsight-use-hive.md) voor meer informatie over Hive.

Het is tijd in beslag neemt tootest Hive-script op een HDInsight-cluster. Dit kan enkele minuten of langer duren. Data Lake Tools voor Visual Studio is staat Hive-script lokaal zonder verbinding tooa live cluster te valideren.

Data Lake Tools voor Visual Studio kunnen ook gebruikers toosee wat binnen Hallo Hive-taak is door het verzamelen en op te halen Hallo YARN-logboeken van bepaalde Hive-taken.

### <a name="view-hello-hivesampletable"></a>Weergave Hallo **hivesampletable**
Alle HDInsight-clusters bevatten een voorbeeld van een Hive-tabel met de naam*hivesampletable*. We gebruiken deze tabel tooshow u hoe toolist Hive-tabellen, Hallo-tabelschema weergeven en Hallo rijen in de lijst Hallo Hive tabel.

**toolist Hive-tabellen en Hive-tabelschema weergeven**

1. Van **Server Explorer**, vouw **Azure** > **HDInsight** > Hallo-cluster van uw keuze > **Hive-Databases**  >  **Standaard** > **hivesampletable** toosee Hallo-tabelschema.
2. Met de rechtermuisknop op **hivesampletable**, en klik vervolgens op **View Top 100 rijen** toolist Hallo rijen. Is het equivalent toorunning Hallo Hive-query met Hive ODBC-stuurprogramma te volgen:
   
     SELECTEER * UIT hivesampletable LIMIET 100
   
   U kunt de aantal rijen Hallo aanpassen.
   
   ![Data Lake Tools: HDInsight Hive Visual Studio-schemaquery](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.hive.schema.png "Resultaten van Hive-query")

### <a name="create-hive-tables"></a>Hive-tabellen maken
U kunt gebruiken Hallo GUI toocreate een Hive-tabel of Hive-query's. Zie [Hive-query's uitvoeren](#run.queries) voor meer informatie over het gebruik van Hive-query's.

**toocreate een Hive-tabel**

1. Vouw in **Server Explorer** achtereenvolgens **Azure** > **HDInsight-clusters** een HDInsight-cluster > **Hive-databases** uit. Klik vervolgens met de rechtermuisknop op **standaard** en klik op **Tabel maken**.
2. Configureer Hallo tabel.
3. Klik op **Create Table** toosubmit Hallo taak toocreate Hallo nieuwe Hive-tabel.
   
    ![Data Lake Tools: HDInsight Visual Studio Tools: Hive-tabel maken](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.create.hive.table.png "Hive-tabel maken")

### <a name="run.queries"></a>Hive-query’s valideren en uitvoeren
Er zijn twee manieren toocreate en Hive-query's uitvoeren:

* Ad-hocquery's maken
* Een Hive-toepassing maken

**toocreate, valideren en uitvoeren van ad-hocquery 's**

1. Vouw in **Server Explorer** achtereenvolgens **Azure** en **HDInsight-clusters** uit.
2. Klik met de rechtermuisknop Hallo cluster waar toorun Hallo query en klik vervolgens op **een Hive-Query schrijven**.
3. Voer Hallo Hive-query's. Kennisgeving Hallo Hive-editor biedt ondersteuning voor IntelliSense. Data Lake Tools voor Visual Studio ondersteuning voor het laden Hallo externe metagegevens wanneer u uw Hive-script bewerkt. Bijvoorbeeld, wanneer u typt 'SELECT * FROM", IntelliSense geeft Hallo Hallo alle voorgestelde tabelnamen. Wanneer een tabelnaam is opgegeven, worden de kolomnamen Hallo Hallo IntelliSense weergegeven. Hallo-hulpprogramma's ondersteunen bijna alle DML-instructies, subquery's en ingebouwde UDF's Hallo.
   
    ![Data Lake Tools: HDInsight Visual Studio Tools IntelliSense](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.intellisense.table.names.png "U-SQL IntelliSense")
   
    ![Data Lake Tools: HDInsight Visual Studio Tools IntelliSense](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.intellisense.column.names.png "U-SQL IntelliSense")
   
   > [!NOTE]
   > Alleen Hallo metagegevens van Hallo clusters die in HDInsight Toolbar is geselecteerd worden, voorgesteld.
   > 
   > 
4. (Optioneel): klik op **Script valideren** toocheck Hallo script op syntaxisfouten.
   
    ![Data Lake Tools: Data Lake Tools voor Visual Studio: lokale validatie](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.validate.hive.script.png "Script valideren")
5. Klik op **Verzenden** of **Verzenden (geavanceerd)**. Met de Hallo geavanceerde optie verzenden, configureert u **taaknaam**, **argumenten**, **aanvullende configuraties**, en **Statusmap**voor Hallo script:
   
    ![HDInsight Hadoop Hive-query](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.submit.jobs.advanced.png "Query's verzenden")
   
    Nadat u Hallo taak hebt verzonden, ziet u een **taakoverzicht Hive** venster.
   
    ![Samenvatting van een HDInsight Hadoop Hive-query](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.run.hive.job.summary.png "Samenvatting van Hive-taak")
6. Gebruik Hallo **vernieuwen** tooupdate Hallo status te totdat Hallo taak de status verandert knop**voltooid**.
7. Klik op Hallo koppelingen op Hallo onder toosee Hallo volgt: **Job Query**, **Taakuitvoer**, **taaklogboek**, of **Yarn-logboek**.

**toocreate en voer een Hive-oplossing**

1. Van Hallo **bestand** menu, klikt u op **nieuw**, en klik vervolgens op **Project**.
2. Selecteer **HDInsight** Selecteer in het linkerdeelvenster Hallo **Hive-toepassing** invoeren in het middelste deelvenster Hallo Hallo eigenschappen en klik vervolgens op **OK**.
   
    ![Data Lake Tools: HDInsight Visual Studio Tools: nieuw Hive-project](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.new.hive.project.png "Hive-toepassingen maken vanuit Visual Studio")
3. Van **Solution Explorer**, dubbelklikt u op **Script.hql** tooopen deze.
4. toovalidate hello Hive-script, klikt u op Hallo **Script valideren** knop of met de rechtermuisknop op het Hallo-script in Hallo Hive-editor en klik vervolgens op **Script valideren** in het contextmenu Hallo.

### <a name="view-hive-jobs"></a>Hive-taken weergeven
U kunt taakquery's, taakuitvoer, logboekbestanden van taken en Yarn-logboekbestanden voor Hive-taken weergeven. Zie de vorige schermafbeelding Hallo voor meer informatie.

de meest recente release Hallo Hallo-hulpprogramma's kunt u toosee wat is er in uw Hive-taken te verzamelen en op te halen YARN-Logboeken. Een YARN-logboek kan u helpen om prestatieproblemen te onderzoeken. Zie [Programmacode gebruiken om toegang te krijgen tot HDInsight-toepassingslogboeken](hdinsight-hadoop-access-yarn-app-logs.md) voor informatie over hoe HDInsight YARN-logboeken verzamelt.

**tooview Hive-taken**

1. Vouw in **Server Explorer** achtereenvolgens **Azure** en **HDInsight** uit.
2. Klik met de rechtermuisknop op een HDInsight-cluster en klik vervolgens op **Taken weergeven**. Hier ziet u een lijst met Hallo Hive-taken die zijn uitgevoerd op Hallo-cluster.
3. Klik op een taak in Hallo taak lijst tooselect en vervolgens gebruik Hallo **taakoverzicht Hive** venster tooopen **Job Query**, **Taakuitvoer**, **taaklogboek**, of **Yarn-logboek**.
   
    ![Data Lake Tools: Hive-taken in HDInsight Visual Studio Tools weergeven](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.view.hive.jobs.png "Hive-taken weergeven")

### <a name="faster-path-hive-execution-via-hiveserver2"></a>Sneller pad voor het uitvoeren van Hive via HiveServer2
> [!NOTE]
> Deze functie werkt alleen op HDInsight-cluster versie 3.2 en nieuwer.
> 
> 

Hallo Data Lake Tools gebruikt toosubmit Hive-taken via [WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) (ook wel bekend als Templeton). Het taakdetails heeft een tooreturn lang geduurd en informatie over de fout.
Dit probleem, Hallo Data Lake Tools wordt uitgevoerd Hive-taken rechtstreeks in het Hallo-cluster via HiveServer2, in volgorde toosolve zodat het RDP/SSH wordt omzeild.
Toevoeging toobetter prestaties, kunnen gebruikers ook bekijken Hive op Tez-grafieken en taakdetails Hallo.

Voor HDInsight-cluster versie 3.2 of hoger wordt de knop **Execute via HiveServer2** (Uitvoeren via HiveServer2) weergegeven:

![Data Lake Tools van Visual Studio uitvoeren via hiveserver2](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.execute.via.hiveserver2.png "Hive-query's uitvoeren met behulp van HiveServer2")

En u kunt Hallo Logboeken in realtime zien en ziet u de taakgrafieken Hallo als Hallo Hive-query wordt uitgevoerd in Tez.

![Data Lake Tools van Visual Studio: snel pad voor het uitvoeren van hive](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.fast.path.hive.execution.png "taakgrafieken bekijken")

**Het verschil tussen het uitvoeren van query's via HiveServer2 en het verzenden van query's via WebHCat**

Het uitvoeren van query's via HiveServer2 biedt verschillende prestatievoordelen biedt, maar heeft ook enkele beperkingen. Enkele van Hallo beperkingen zijn niet geschikt voor productiegebruik. Hallo ziet volgende tabel u Hallo verschillen:

|  | Via HiveServer2 uitvoeren | Verzenden via WebHCat |
| --- | --- | --- |
| Query's uitvoeren |Elimineert Hallo overhead in WebHCat (gestart een MapReduce Job met de naam 'TempletonControllerJob'). |Zolang een query wordt uitgevoerd via WebHCat, start WebHCat een MapReduce-taak die resulteert in extra latentie. |
| Logboeken terugstreamen |Bijna in realtime. |Hallo-logboekbestanden voor het uitvoeren van taak zijn alleen beschikbaar wanneer Hallo-taak is voltooid. |
| Taakgeschiedenis weergeven |Als een query wordt uitgevoerd via HiveServer2, blijft de taakgeschiedenis (taaklogboek, taakuitvoer) niet behouden. Hallo-toepassing kan worden weergegeven in de gebruikersinterface van YARN met beperkte informatie. |Als een query wordt uitgevoerd via WebHCat, blijft de taakgeschiedenis (taaklogboek, taakuitvoer) bewaard en kan deze worden weergegeven met Visual Studio/HDInsight SDK/PowerShell. |
| Venster sluiten |Uitvoeren via is HiveServer2 een 'synchrone' methode zodat u Hallo vensters geopend; moet houden Als windows hello worden gesloten vervolgens Hallo queryuitvoering geannuleerd. |Verzenden via WebHCat is een 'asynchrone' methode zodat u kunt Hallo query via WebHCat indienen en sluit u Visual Studio. U kunt terugkeren en Hallo resultaten op elk gewenst moment bekijken. |

### <a name="tez-hive-job-performance-graph"></a>Prestatiegrafiek Tez Hive-taak
Hallo Data Lake Tools ondersteuning van de prestatiegrafieken voor Hallo Hive-taken die worden uitgevoerd door Hallo Tez-uitvoeringsengine. Zie [Hive in HDInsight gebruiken](hdinsight-use-hive.md) voor informatie over het inschakelen van Tez. Nadat u hebt verzonden Hallo een component taak in Visual Studio, Visual Studio ziet u de grafiek wanneer Hallo-taak is voltooid.  Mogelijk moet u tooclick hello **vernieuwen** tooget Hallo meest recente taakstatus knop.

> [!NOTE]
> Deze functie is alleen beschikbaar voor HDInsight-clusters van versie 3.2.4.593 of hoger en werkt alleen voor voltooide taken (als u uw werk via WebHCat hebt verzonden). Deze grafiek wordt weergegeven wanneer u uw query uitvoert via HiveServer2. Dit werkt zowel voor Windows- als Linux-clusters.
> 
> 

![hadoop hive tez prestatiegrafiek](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.hive.tez.performance.graph.png "Taakstatus")

toohelp u inzicht in uw Hive query betere, Hallo hulpprogramma's voor de weergave Hive Operator Hallo toevoegen in deze release. U hoeft alleen maar toodouble en klikken op de hoekpunten van de taakgrafiek Hallo Hallo en ziet u alle Hallo operators in Hallo hoekpunt. U kunt ook de muisaanwijzer op een bepaalde operator tooview meer informatie over deze operator.

### <a name="task-execution-view-for-hive-on-tez-jobs"></a>Taakuitvoeringsweergave voor Hive op Tez-taken
Hallo taakuitvoeringsweergave voor Hive op Tez-taken kan worden gebruikt tooget gestructureerde en gevisualiseerde informatie voor Hive-taken en meer taakdetails. Wanneer er prestatieproblemen, kunt u Hallo weergave tooget meer informatie. Bijvoorbeeld, gedetailleerde hoe elke taak functioneert en Hallo informatie over elke taak (gegevens lezen/schrijven, start-schema-end time, enzovoort), zodat u de taakconfiguraties of de systeemarchitectuur op basis van de informatie die gevisualiseerd Hallo kunt afstemmen.

![Data Lake Visual Studio Tools taakuitvoeringsweergave](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.task.execution.view.png "Taakuitvoeringsweergave")

## <a name="run-pig-scripts"></a>Pig-scripts uitvoeren
Data Lake Tools voor Visual Studio ondersteunt het maken en verzenden van Pig-scripts tooHDInsight clusters. Gebruikers kunnen een Pig-project maken van sjabloon en vervolgens dient Hallo script tooHDInsight clusters.

## <a name="feedbacks--known-issues"></a>Feedback en bekende problemen
* Momenteel worden de HiveServer2-resultaten weergegeven als tekst. Dit is niet ideaal. Er wordt momenteel gewerkt aan een oplossing.
* Hallo resultaten die zijn gestart met NULL-waarden, worden momenteel Hallo resultaten niet weergegeven. We hebben dit probleem is opgelost en als u op dit probleem vastloopt, kunt u gratis toodrop ons een e-mailadres of neem contact op met ondersteuning voor team.
* Hallo HQL-script is gemaakt door Visual Studio is, afhankelijk van de lokale regio-instellingen van de gebruiker gecodeerd. Deze mogelijk niet correct uitgevoerd als de gebruiker Hallo script toocluster als binair bestand uploadt.

## <a name="next-steps"></a>Volgende stappen
In dit artikel hebt u geleerd hoe tooconnect tooHDInsight clusters vanuit Visual Studio, Hallo Data Lake (HDInsight) met hulpprogramma's en hoe toorun een Hive-query. Zie voor meer informatie:

* [Hadoop Hive in HDInsight gebruiken](hdinsight-use-hive.md)
* [Aan de slag met Hadoop in HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md)
* [Hadoop-taken opgeven in HDInsight](hdinsight-submit-hadoop-jobs-programmatically.md)
* [Twitter-gegevens met Hadoop analyseren in HDInsight](hdinsight-analyze-twitter-data.md)


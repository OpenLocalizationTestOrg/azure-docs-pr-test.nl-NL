---
title: aaaUse Apache Storm met Power BI - Azure HDInsight | Microsoft Docs
description: Maak een Power BI-rapport met gegevens uit een C#-topologie uitgevoerd op een Apache Storm-cluster in HDInsight.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 36fe3b9c-5232-4464-8d75-95403b6da7a1
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/31/2017
ms.author: larryfr
ms.openlocfilehash: 194cd8220bd60475af1d64a110e4b23ef92e1bc8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-power-bi-toovisualize-data-from-an-apache-storm-topology"></a>Gebruik Power BI toovisualize gegevens uit een Apache Storm-topologie

Power BI kunt u toovisually weergavegegevens als rapporten. Dit document bevat een voorbeeld van hoe toouse Apache Storm op HDInsight toogenerate gegevens voor Power BI.

> [!NOTE]
> Hallo stappen in dit document zijn afhankelijk van een Windows-ontwikkelomgeving met Visual Studio. Hallo gecompileerd project kan worden verzonden tooa Linux gebaseerde HDInsight-cluster. Alleen op basis van Linux-clusters gemaakt na 28-10-2016 ondersteuning SCP.NET topologieën.
>
> toouse een C#-topologie met een update Hallo Microsoft.SCP.Net.SDK NuGet-pakket gebruikt door uw project tooversion 0.10.0.6 of hoger van het cluster op basis van Linux. Hallo-versie van het Hallo-pakket moet ook overeenkomen met de Hallo primaire versie van Storm op HDInsight is geïnstalleerd. HDInsight-versies 3.3 en 3.4 gebruiken bijvoorbeeld Storm-versie 0.10.x en HDInsight 3.5 gebruikt Storm 1.0.x.
>
> C#-topologieën op Linux gebaseerde clusters moeten gebruiken, .NET 4.5 en het gebruik van Mono toorun op Hallo HDInsight-cluster. De meeste dingen werken. U moet echter Hallo controleren [Mono compatibiliteit](http://www.mono-project.com/docs/about-mono/compatibility/) document voor potentiële compatibiliteitsproblemen.
>
> Zie voor een Java-versie van dit project, met HDInsight op basis van Linux of op basis van Windows werkt, [verwerken van gebeurtenissen van Azure Event Hubs met Storm op HDInsight (Java)](hdinsight-storm-develop-java-event-hub-topology.md).

## <a name="prerequisites"></a>Vereisten

* Een Azure Active Directory-gebruiker met [Power BI](https://powerbi.com) toegang.
* Een HDInsight-cluster. Zie voor meer informatie [aan de slag met Storm op HDInsight](hdinsight-apache-storm-tutorial-get-started-linux.md).

  > [!IMPORTANT]
  > Linux is Hallo enige besturingssysteem gebruikt op HDInsight versie 3.4 of hoger. Zie [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (HDInsight buiten gebruik gestel voor Windows) voor meer informatie.

* Visual Studio (een van de volgende versies Hallo)

  * Visual Studio 2012 met [update 4](http://www.microsoft.com/download/details.aspx?id=39305)
  * Visual Studio 2013 met [update 4](http://www.microsoft.com/download/details.aspx?id=44921) of [Visual Studio 2013 Community](http://go.microsoft.com/fwlink/?linkid=517284&clcid=0x409)
  * [Visual Studio 2015](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx)
  * Visual Studio 2017 (alle versies)

* Hallo HDInsight Tools voor Visual Studio: Zie [aan de slag met Hallo HDInsight Tools voor Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md) voor meer informatie over installatie-informatie.

## <a name="how-it-works"></a>Hoe werkt het?

In dit voorbeeld bevat een C# Storm-topologie die willekeurig logboekgegevens van Internet Information Services (IIS genereert). Deze gegevens worden vervolgens tooa SQL-Database geschreven en van daaruit is gebruikte toogenerate rapporten in Power BI.

Hallo bestanden implementeren Hallo belangrijkste functionaliteit van dit voorbeeld te volgen:

* **SqlAzureBolt.cs**: schrijft informatie in Hallo Storm-topologie tooSQL Database geproduceerd.
* **IISLogsTable.sql**: Hallo Transact-SQL-instructies gebruikt toogenerate Hallo database die Hallo gegevens worden opgeslagen in.

> [!WARNING]
> Hallo-tabel maken in SQL-Database voordat het Hallo-topologie op uw HDInsight-cluster wordt gestart.

## <a name="download-hello-example"></a>Hallo voorbeeld downloaden

Hallo downloaden [HDInsight C# Storm Power BI-voorbeeld](https://github.com/Azure-Samples/hdinsight-dotnet-storm-powerbi). toodownload, ofwel fork/kloon met behulp van [git](http://git-scm.com/), of gebruik Hallo **downloaden** koppeling toodownload een .zip van Hallo-archief.

## <a name="create-a-database"></a>Een database maken

1. een database toocreate Hallo stappen in hello gebruiken [SQL Database-zelfstudie](../sql-database/sql-database-get-started.md) document.

2. Verbinding maken met toohello database door de volgende Hallo stappen voor het Hallo [tooa SQL-Database met Visual Studio verbinding](../sql-database/sql-database-connect-query.md) document.

3. In Object Explorer met de rechtermuisknop op het Hallo-database en selecteer **nieuwe Query**. Plak de inhoud Hallo Hallo **IISLogsTable.sql** op Hallo bestand project gedownload naar het queryvenster Hallo en vervolgens met Ctrl + Shift + E tooexecute Hallo query. U ontvangt een bericht dat Hallo opdrachten is voltooid.

## <a name="configure-hello-sample"></a>Hallo voorbeeld configureren

1. Van Hallo [Azure-portal](https://portal.azure.com), selecteert u uw SQL-database. Van Hallo **Essentials** sectie van Hallo SQL-database, selecteer **databaseverbindingsreeksen tonen**. Kopiëren van Hallo lijst die wordt weergegeven, Hallo **ADO.NET (SQL-verificatie)** informatie.

2. Hallo voorbeeld openen in Visual Studio. Van **Solution Explorer**Open Hallo **App.config** bestand en zoek Hallo vermelding te volgen:

        <add key="SqlAzureConnectionString" value="##TOBEFILLED##" />

    Vervang Hallo **# TOBEFILLED ##** waarde met de tekenreeks voor databaseverbinding Hallo in Hallo vorige stap hebt gekopieerd. Vervang **{uw\_username}** en **{uw\_wachtwoord}** met Hallo gebruikersnaam en wachtwoord voor Hallo-database.

3. Opslaan en sluiten Hallo-bestanden.

## <a name="deploy-hello-sample"></a>Hallo voorbeeld implementeren

1. Van **Solution Explorer**, klik met de rechtermuisknop Hallo **StormToSQL** project en selecteer **indienen tooStorm op HDInsight**. Selecteer Hallo HDInsight-cluster van Hallo **Storm-Cluster** dropdown dialoogvenster.

   > [!NOTE]
   > Het kan enkele seconden duren voor Hallo **Storm-Cluster** dropdown toopopulate met servernamen.
   >
   > Als u wordt gevraagd, voert u Hallo aanmeldingsreferenties voor uw Azure-abonnement. Als u meer dan één abonnement hebt, meldt u zich in toohello een bestand met uw Storm op HDInsight-cluster.

2. Wanneer het Hallo-topologie is ingediend, Hallo __topologie Viewer__ wordt weergegeven. tooview deze topologie, selecteer Hallo SqlAzureWriterTopology vermelding uit Hallo-lijst.

    ![Hallo-topologieën met Hallo-topologie die zijn geselecteerd](./media/hdinsight-storm-power-bi-topology/topologyview.png)

    U kunt gebruiken deze informatie weergeven toosee op Hallo topologie of dubbelklik op een vermelding (zoals hello SqlAzureBolt) toosee specifieke tooa onderdeel van de gegevens in Hallo-topologie.

3. Na het Hallo is topologie uitgevoerd voor een paar minuten return toohello SQL query-venster toocreate Hallo database die wordt gebruikt. De bestaande instructies Hallo vervangen door Hallo query te volgen:

        select * from iislogs;

    Gebruik Ctrl + Shift + E tooexecute Hallo query, en u ontvangt resultaten vergelijkbare toohello gegevens te volgen:

        1    2016-05-27 17:57:14.797    255.255.255.255    /bar    GET    200
        2    2016-05-27 17:57:14.843    127.0.0.1    /spam/eggs    POST    500
        3    2016-05-27 17:57:14.850    123.123.123.123    /eggs    DELETE    200
        4    2016-05-27 17:57:14.853    127.0.0.1    /foo    POST    404
        5    2016-05-27 17:57:14.853    10.9.8.7    /bar    GET    200
        6    2016-05-27 17:57:14.857    192.168.1.1    /spam    DELETE    200

    Deze gegevens is geschreven van Hallo Storm-topologie.

## <a name="create-a-report"></a>Een rapport maken

1. Verbinding maken met toohello [Azure SQL Database connector](https://app.powerbi.com/getdata/bigdata/azure-sql-database-with-live-connect) voor Power BI. 

2. Binnen **Databases**, selecteer **ophalen**.

3. Selecteer **Azure SQL Database**, en selecteer vervolgens **Connect**.

    > [!NOTE]
    > U wordt mogelijk gevraagd toodownload Hallo Power BI Desktop toocontinue. Als dit het geval is, gebruikt u Hallo tooconnect stappen te volgen:
    >
    > 1. Power BI Desktop openen en selecteer __gegevens ophalen__.
    > 2 Schakel __Azure__, en vervolgens __Azure SQL-database__.

4. Voer Hallo informatie tooconnect tooyour Azure SQL Database. U vindt deze informatie Hallo [Azure-portal](https://portal.azure.com) en de SQL-database te selecteren.

   > [!NOTE]
   > U kunt ook het vernieuwingsinterval Hallo en aangepaste filters instellen met behulp van **geavanceerde opties inschakelen** van Hallo dialoogvenster voor verbinden.

5. Nadat u verbinding hebt gemaakt, ziet u een nieuwe gegevensset met dezelfde naam als de database Hallo u verbonden met Hallo. Hallo gegevensset toobegin ontwerpen van een rapport selecteren.

6. Van **velden**, vouw Hallo **IISLOGS** vermelding. een rapport dat een lijst met URI Hallo komen voort, toocreate Hallo selectievakje selecteert voor **URISTEM**.

    ![Maken van een rapport](./media/hdinsight-storm-power-bi-topology/createreport.png)

7. En sleep de **methode** toohello rapport. Hallo rapport updates toolist Hallo komen voort en Hallo bijbehorende HTTP-methode gebruikt voor Hallo HTTP-aanvraag.

    ![Hallo methode gegevens toe te voegen](./media/hdinsight-storm-power-bi-topology/uristemandmethod.png)

8. Van Hallo **visualisaties** kolom, selecteer Hallo **velden** pictogram en selecteer vervolgens Hallo pijl-omlaag naast te**methode** in Hallo **waarden**sectie. toodisplay een telling van hoe vaak een URI is geopend, selecteer **aantal**.

    ![Het aantal methoden tooa wijzigen](./media/hdinsight-storm-power-bi-topology/count.png)

9. Selecteer vervolgens Hallo **gestapeld kolomdiagram** toochange hoe Hallo informatie wordt weergegeven.

    ![Veranderende tooa gestapelde grafiek](./media/hdinsight-storm-power-bi-topology/stackedcolumn.png)

10. toosave hello rapport, selecteer **opslaan** en voer een naam voor het Hallo-rapport.

## <a name="stop-hello-topology"></a>Hallo-topologie stoppen

Hallo-topologie wordt toorun vervolgd totdat u stoppen of verwijderen van Hallo Storm op HDInsight-cluster. toostop Hallo topologie, Hallo volgende stappen uit te voeren:

1. In Visual Studio toohello topologie viewer terug en selecteer Hallo-topologie.

2. Selecteer Hallo **Kill** knop toostop Hallo topologie.

    ![Kill-knop op Hallo topologie samenvatting](./media/hdinsight-storm-power-bi-topology/killtopology.png)

## <a name="delete-your-cluster"></a>Uw cluster verwijderen

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-steps"></a>Volgende stappen

In dit document hebt u geleerd hoe toosend gegevens van een Storm-topologie tooSQL Database, klikt u vervolgens Hallo gegevens visualiseren met Power BI. Voor meer informatie over toowork met andere Azure technologieën met Storm op HDInsight, Zie Hallo document te volgen:

* [Voorbeeldtopologieën van Storm op HDInsight](hdinsight-storm-example-topology.md)

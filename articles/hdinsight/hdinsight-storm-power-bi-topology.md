---
title: Apache Storm gebruiken met Power BI - Azure HDInsight | Microsoft Docs
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
ms.openlocfilehash: 36487c0c34e5a4bb955bbc15c8c96b9e838aeb44
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="use-power-bi-to-visualize-data-from-an-apache-storm-topology"></a>Power BI gebruiken om gegevens uit een Apache Storm-topologie te visualiseren

Power BI kunt u gegevens visueel weergeven als rapporten. Dit document bevat een voorbeeld van hoe u Apache Storm op HDInsight gebruiken om gegevens te genereren voor Power BI.

> [!NOTE]
> De stappen in dit document, is afhankelijk van een Windows-ontwikkelomgeving met Visual Studio. Het gecompileerde project kan worden verzonden naar een Linux gebaseerde HDInsight-cluster. Alleen op basis van Linux-clusters gemaakt na 28-10-2016 ondersteuning SCP.NET topologieën.
>
> Als u wilt gebruiken een C#-topologie met een cluster op basis van Linux, werk het Microsoft.SCP.Net.SDK NuGet-pakket gebruikt door uw project naar versie 0.10.0.6 of hoger. De versie van het pakket moet ook overeenkomen met de primaire versie van Storm die op HDInsight is geïnstalleerd. HDInsight-versies 3.3 en 3.4 gebruiken bijvoorbeeld Storm-versie 0.10.x en HDInsight 3.5 gebruikt Storm 1.0.x.
>
> C#-topologieën met op Linux gebaseerde clusters moeten .NET 4.5 en Mono gebruiken om op het HDInsight-cluster te worden uitgevoerd. De meeste dingen werken. U moet echter controleren de [Mono compatibiliteit](http://www.mono-project.com/docs/about-mono/compatibility/) document voor potentiële compatibiliteitsproblemen.
>
> Zie voor een Java-versie van dit project, met HDInsight op basis van Linux of op basis van Windows werkt, [verwerken van gebeurtenissen van Azure Event Hubs met Storm op HDInsight (Java)](hdinsight-storm-develop-java-event-hub-topology.md).

## <a name="prerequisites"></a>Vereisten

* Een Azure Active Directory-gebruiker met [Power BI](https://powerbi.com) toegang.
* Een HDInsight-cluster. Zie voor meer informatie [aan de slag met Storm op HDInsight](hdinsight-apache-storm-tutorial-get-started-linux.md).

  > [!IMPORTANT]
  > Linux is het enige besturingssysteem dat wordt gebruikt in HDInsight-versie 3.4 of hoger. Zie [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (HDInsight buiten gebruik gestel voor Windows) voor meer informatie.

* Visual Studio (een van de volgende versies)

  * Visual Studio 2012 met [update 4](http://www.microsoft.com/download/details.aspx?id=39305)
  * Visual Studio 2013 met [update 4](http://www.microsoft.com/download/details.aspx?id=44921) of [Visual Studio 2013 Community](http://go.microsoft.com/fwlink/?linkid=517284&clcid=0x409)
  * [Visual Studio 2015](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx)
  * Visual Studio 2017 (alle versies)

* De HDInsight Tools voor Visual Studio: Zie [aan de slag met HDInsight Tools voor Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md) voor meer informatie over installatie-informatie.

## <a name="how-it-works"></a>Hoe werkt het?

In dit voorbeeld bevat een C# Storm-topologie die willekeurig logboekgegevens van Internet Information Services (IIS genereert). Deze gegevens vervolgens naar een SQL-Database is geschreven en van daaruit wordt gebruikt om rapporten te genereren in Power BI.

De volgende bestanden implementeren van de belangrijkste functionaliteit van dit voorbeeld:

* **SqlAzureBolt.cs**: schrijft informatie in de Storm-topologie met SQL-Database wordt geproduceerd.
* **IISLogsTable.sql**: gebruikt voor het genereren van de database die de gegevens worden opgeslagen in de Transact-SQL-instructies.

> [!WARNING]
> De tabel in SQL-Database maken voordat u begint de topologie op uw HDInsight-cluster.

## <a name="download-the-example"></a>In het voorbeeld downloaden

Download de [HDInsight C# Storm Power BI-voorbeeld](https://github.com/Azure-Samples/hdinsight-dotnet-storm-powerbi). Als u wilt downloaden, ofwel fork/kloon met behulp van [git](http://git-scm.com/), of gebruik de **downloaden** koppeling voor het downloaden van een .zip van het archief.

## <a name="create-a-database"></a>Een database maken

1. Voor het maken van een database gebruikt u de stappen in de [SQL Database-zelfstudie](../sql-database/sql-database-get-started.md) document.

2. Verbinding maken met de database door de stappen in de [verbinding maken met een SQL-Database met Visual Studio](../sql-database/sql-database-connect-query.md) document.

3. In Object Explorer met de rechtermuisknop op de database en selecteer **nieuwe Query**. Plak de inhoud van de **IISLogsTable.sql** bestand opgenomen in het gedownloade project naar het queryvenster en gebruik vervolgens Ctrl + Shift + E de query uit te voeren. U ontvangt een bericht dat de opdrachten is voltooid.

## <a name="configure-the-sample"></a>Het voorbeeld configureren

1. Van de [Azure-portal](https://portal.azure.com), selecteert u uw SQL-database. Van de **Essentials** sectie van de SQL-database, selecteer **databaseverbindingsreeksen tonen**. In de lijst die wordt weergegeven, kopieert u de **ADO.NET (SQL-verificatie)** informatie.

2. Open het voorbeeld in Visual Studio. Van **Solution Explorer**, open de **App.config** bestand en zoek de volgende vermelding:

        <add key="SqlAzureConnectionString" value="##TOBEFILLED##" />

    Vervang de **# TOBEFILLED ##** waarde met de databaseverbindingsreeks in de vorige stap hebt gekopieerd. Vervang **{uw\_username}** en **{uw\_wachtwoord}** met de gebruikersnaam en wachtwoord voor de database.

3. Opslaan en sluiten van de bestanden.

## <a name="deploy-the-sample"></a>Het voorbeeld implementeren

1. Van **Solution Explorer**, met de rechtermuisknop op de **StormToSQL** project en selecteer **indienen Storm op HDInsight**. Selecteer het HDInsight-cluster van de **Storm-Cluster** dropdown dialoogvenster.

   > [!NOTE]
   > Kan het enkele seconden duren voor de **Storm-Cluster** dropdown te vullen met servernamen.
   >
   > Als u wordt gevraagd, voert u de aanmeldingsreferenties voor uw Azure-abonnement. Als u meer dan één abonnement hebt, moet u zich aanmelden bij de database met uw Storm op HDInsight-cluster.

2. Wanneer de topologie is ingediend, de __topologie Viewer__ wordt weergegeven. Als u wilt deze topologie weergeven, selecteert u de vermelding SqlAzureWriterTopology in de lijst.

    ![De topologieën, met de topologie die is geselecteerd](./media/hdinsight-storm-power-bi-topology/topologyview.png)

    U kunt het gebruik van deze weergave voor informatie over de topologie of dubbelklik op een item (zoals de SqlAzureBolt) voor informatie die specifiek zijn voor een onderdeel in de topologie.

3. Nadat de topologie is uitgevoerd voor een paar minuten, Ga terug naar het SQL-query-venster dat u gebruikt voor het maken van de database. Vervang de bestaande instructies aan de volgende query:

        select * from iislogs;

    Gebruik Ctrl + Shift + E uitvoeren van de query en u ontvangt resultaten vergelijkbaar met de volgende gegevens:

        1    2016-05-27 17:57:14.797    255.255.255.255    /bar    GET    200
        2    2016-05-27 17:57:14.843    127.0.0.1    /spam/eggs    POST    500
        3    2016-05-27 17:57:14.850    123.123.123.123    /eggs    DELETE    200
        4    2016-05-27 17:57:14.853    127.0.0.1    /foo    POST    404
        5    2016-05-27 17:57:14.853    10.9.8.7    /bar    GET    200
        6    2016-05-27 17:57:14.857    192.168.1.1    /spam    DELETE    200

    Deze gegevens is uit de Storm-topologie geschreven.

## <a name="create-a-report"></a>Een rapport maken

1. Verbinding maken met de [Azure SQL Database connector](https://app.powerbi.com/getdata/bigdata/azure-sql-database-with-live-connect) voor Power BI. 

2. Binnen **Databases**, selecteer **ophalen**.

3. Selecteer **Azure SQL Database**, en selecteer vervolgens **Connect**.

    > [!NOTE]
    > U wordt mogelijk gevraagd om te downloaden van de Power BI Desktop om door te gaan. Als dit het geval is, moet u de volgende stappen gebruiken om verbinding te:
    >
    > 1. Power BI Desktop openen en selecteer __gegevens ophalen__.
    > 2 Schakel __Azure__, en vervolgens __Azure SQL-database__.

4. Geef de informatie die verbinding maken met uw Azure SQL Database. U kunt deze informatie vinden in via de [Azure-portal](https://portal.azure.com) en de SQL-database te selecteren.

   > [!NOTE]
   > U kunt ook het vernieuwingsinterval en aangepaste filters instellen met behulp van **geavanceerde opties inschakelen** in het dialoogvenster verbinding maken.

5. Nadat u verbinding hebt gemaakt, ziet u een nieuwe gegevensset met dezelfde naam als de database die u met verbonden. Selecteer de gegevensset om te beginnen met het ontwerpen van een rapport.

6. Van **velden**, vouw de **IISLOGS** vermelding. Schakel het selectievakje voor een rapport te maken met een lijst met de URI-stammen, **URISTEM**.

    ![Maken van een rapport](./media/hdinsight-storm-power-bi-topology/createreport.png)

7. En sleep de **methode** aan het rapport. Het rapport bijwerken in de lijst is en de bijbehorende HTTP-methode gebruikt voor de HTTP-aanvraag.

    ![de methode gegevens worden toegevoegd](./media/hdinsight-storm-power-bi-topology/uristemandmethod.png)

8. Van de **visualisaties** kolom, selecteer de **velden** pictogram en selecteer vervolgens de pijl-omlaag naast **methode** in de **waarden** sectie. Als u wilt weergeven in een telling van het aantal keren dat een URI is geopend, selecteer **aantal**.

    ![Wijzigen in een aantal methoden](./media/hdinsight-storm-power-bi-topology/count.png)

9. Selecteer vervolgens de **gestapeld kolomdiagram** wijzigen hoe de gegevens worden weergegeven.

    ![Wijzigen naar een gestapelde grafiek](./media/hdinsight-storm-power-bi-topology/stackedcolumn.png)

10. Sla het rapport, selecteer **opslaan** en voer een naam voor het rapport.

## <a name="stop-the-topology"></a>De topologie stoppen

De topologie blijft actief totdat u stoppen of verwijderen van de Storm op HDInsight-cluster. Als u wilt de topologie stoppen, moet u de volgende stappen uitvoeren:

1. Terug naar de topologie-viewer in Visual Studio en selecteer de topologie.

2. Selecteer de **Kill** knop stoppen van de topologie.

    ![Kill-knop van de topologie samenvatting](./media/hdinsight-storm-power-bi-topology/killtopology.png)

## <a name="delete-your-cluster"></a>Uw cluster verwijderen

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-steps"></a>Volgende stappen

In dit document hebt u geleerd hoe gegevens verzenden vanuit een Storm-topologie met SQL-Database en vervolgens de gegevens visualiseren met Power BI. Zie voor informatie over het werken met andere Azure-technologieën met Storm op HDInsight, het volgende document:

* [Voorbeeldtopologieën van Storm op HDInsight](hdinsight-storm-example-topology.md)

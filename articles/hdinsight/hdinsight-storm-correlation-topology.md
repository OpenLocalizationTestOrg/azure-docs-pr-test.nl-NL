---
title: aaaCorrelate gebeurtenissen gedurende een periode met Storm en HBase in HDInsight
description: Meer informatie over hoe toocorrelate gebeurtenissen die op verschillende tijdstippen binnenkomen met behulp van Storm en HBase op HDInsight.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 17d11479-2d02-4790-8d29-05fb38351479
ms.service: hdinsight
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/07/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive
ms.openlocfilehash: f915eef77bbda5b02bfd02ad0b5a4923ff2f4f26
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="correlate-events-that-arrive-at-different-times-using-storm-and-hbase"></a>Gebeurtenissen die op verschillende tijdstippen binnenkomen correleren met Storm en HBase

Met behulp van een permanente gegevensopslag met Apache Storm, kunt u gegevens die op verschillende tijdstippen binnenkomen correleren. Bijvoorbeeld, koppelen aan- en afmelden gebeurtenissen voor een gebruiker sessie toocalculate hoe lang Hallo sessie heeft geduurd.

In dit document, leert u hoe toocreate een basic C# Storm-topologie die aanmelding en afmelding gebeurtenissen worden bijgehouden voor gebruikerssessies en Hallo duur van Hallo-sessie wordt berekend. Hallo-topologie gebruikt HBase als een permanente gegevensarchief. HBase kunt u ook tooperform batch-query's op Hallo historische gegevens tooproduce meer inzicht geboden. Bijvoorbeeld hoeveel gebruikerssessies zijn gestart of beëindigd tijdens een bepaalde periode.

## <a name="prerequisites"></a>Vereisten

* Visual Studio en hello wordt HDInsight tools voor Visual Studio. Zie voor meer informatie [aan de slag met Hallo HDInsight tools voor Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).

* Apache Storm op HDInsight-cluster (Windows-indeling).

  > [!WARNING]
  > SCP.NET topologieën worden wel ondersteund op Linux gebaseerde Storm-clusters die zijn gemaakt na 28-10-2016, werkt Hallo HBase SDK voor .NET-pakketten beschikbaar vanaf 28-10-2016 niet correct op Linux gebaseerde HDInsight

* Apache HBase op HDInsight-cluster (Linux of op Windows gebaseerde).

  > [!IMPORTANT]
  > Linux is Hallo enige besturingssysteem gebruikt op HDInsight versie 3.4 of hoger. Zie [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (HDInsight buiten gebruik gestel voor Windows) voor meer informatie.

* [Java](https://java.com) 1.7 of hoger op uw ontwikkelomgeving. Java is gebruikte toopackage Hallo topologie wanneer deze ingediende toohello HDInsight-cluster.

  * Hallo **JAVA_HOME** omgeving variabele moet punt toohello directory met Java.
  * Hallo **%JAVA_HOME%/bin** map zich in het Hallo-pad

## <a name="architecture"></a>Architectuur

![Diagram van de gegevensstroom Hallo via Hallo-topologie](./media/hdinsight-storm-correlation-topology/correlationtopology.png)

Correleren van gebeurtenissen, is een algemene id voor de gebeurtenisbron Hallo vereist. For example, een gebruikers-ID, sessie-ID of andere gegevenseenheid die is een) uniek en b) opgenomen in alle gegevens die worden verzonden tooStorm. In dit voorbeeld wordt een GUID-waarde toorepresent een sessie-ID.

In dit voorbeeld bestaat uit twee clusters met HDInsight:

* HBase: permanente gegevensopslag voor historische gegevens
* Storm: gebruikt tooingest binnenkomende gegevens

Hallo gegevens wordt willekeurig gegenereerd door Hallo Storm-topologie en bestaat uit Hallo volgende items:

* Sessie-ID: een GUID die een unieke identificatie van elke sessie
* Gebeurtenis: een begin- of -gebeurtenis. In dit voorbeeld START doet zich altijd voor einde
* Tijd: Hallo tijdstip Hallo-gebeurtenis.

Deze gegevens worden verwerkt en opgeslagen in HBase.

### <a name="storm-topology"></a>storm-topologie

Wanneer een sessie wordt gestart, een **START** gebeurtenis is ontvangen door het Hallo-topologie en tooHBase in het logboek geregistreerd. Wanneer een **END** gebeurtenis is ontvangen, Hallo topologie opgehaald Hallo **START** gebeurtenis en berekent Hallo tijd tussen twee Hallo gebeurtenissen. Dit **duur** waarde vervolgens wordt opgeslagen in HBase samen met de Hallo **END** informatie over de gebeurtenis.

> [!IMPORTANT]
> Terwijl deze topologie wordt gedemonstreerd basispatroon hello, moet een productie-oplossing tootake ontwerp voor Hallo volgen scenario's:
>
> * Gebeurtenissen volgorde binnenkomen
> * Dubbele gebeurtenissen
> * Verwijderde gebeurtenissen

Hallo voorbeeld topologie bestaat uit Hallo volgende onderdelen:

* Session.CS: simuleert een gebruikerssessie door het maken van een willekeurige sessie-ID, start tijdstip en hoe lang Hallo sessie duurt.

* Spout.CS: 100 sessies maakt, verzendt een startgebeurtenis, wordt gewacht Hallo willekeurige time-out voor elke sessie en vervolgens verzendt een END-gebeurtenis. Vervolgens wordt recyclet sessies toogenerate nieuwe beëindigd.

* HBaseLookupBolt.cs: maakt gebruik van Hallo sessie-ID toolook van de sessie-informatie van HBase. Wanneer een END-gebeurtenis wordt verwerkt, vindt het overeenkomende begingebeurtenis Hallo en Hallo duur van Hallo-sessie wordt berekend.

* HBaseBolt.cs: Bevat gegevens in HBase.

* TypeHelper.cs: Helpt met typeconversie bij het lezen van / schrijven tooHBase.

### <a name="hbase-schema"></a>HBase-schema

In HBase, Hallo gegevens opgeslagen in een tabel met Hallo schema-instellingen te volgen:

* Rijsleutel: Hallo-sessie-ID wordt gebruikt als de sleutel Hallo voor rijen in deze tabel.

* Kolomfamilie: familienaam Hallo 'cf' is. Kolommen die zijn opgeslagen in deze familie zijn:

  * gebeurtenis: begin of einde.

  * tijd: Hallo tijd in milliseconden dat Hallo gebeurtenis is opgetreden.

  * duur: Hallo lengte tussen de begin- en -gebeurtenis.

* VERSIES: Hallo 'cf' familie ingesteld tooretain 5-versies van elke rij.

  > [!NOTE]
  > Versies zijn een logboek van de vorige waarden voor de sleutel van een specifieke rij. HBase retourneert alleen Hallo-waarde voor de meest recente versie van een rij Hallo standaard. In dit geval wordt hello dezelfde rij gebruikt voor elke versie van een rij wordt geïdentificeerd door de tijdstempelwaarde Hallo alle gebeurtenissen (START en END.). Versies bieden een historisch overzicht gegeven van gebeurtenissen die zijn geregistreerd voor een specifieke-ID.

## <a name="download-hello-project"></a>Hallo-project downloaden

Hallo-voorbeeldproject kan worden gedownload vanaf [https://github.com/Azure-Samples/hdinsight-storm-dotnet-event-correlation](https://github.com/Azure-Samples/hdinsight-storm-dotnet-event-correlation).

Deze download bevat Hallo C#-projecten te volgen:

* CorrelationTopology: C# Storm-topologie die willekeurig begin- en gebeurtenissen voor gebruikerssessies verzendt. Elke sessie duurt tussen 1 en 5 minuten.

* SessionInfo: C#-consoletoepassing die maakt Hallo HBase-tabel en bevat voorbeeldquery tooreturn informatie over de opgeslagen sessiegegevens.

## <a name="create-hello-table"></a>Hallo-tabel maken

1. Open Hallo **SessionInfo** -project in Visual Studio.

2. In **Solution Explorer**, klik met de rechtermuisknop Hallo **SessionInfo** project en selecteer **eigenschappen**.

    ![Schermopname van menu met eigenschappen die zijn geselecteerd](./media/hdinsight-storm-correlation-topology/selectproperties.png)

3. Selecteer **instellingen**, en vervolgens set Hallo de volgende waarden:

   * HBaseClusterURL: Hallo URL tooyour HBase-cluster. Bijvoorbeeld: https://myhbasecluster.azurehdinsight.net.

   * HBaseClusterUserName: Hallo beheerder/HTTP-gebruikersaccount voor uw cluster

   * HBaseClusterPassword: Hallo wachtwoord voor Hallo beheerder/HTTP-gebruikersaccount

   * HBaseTableName: naam van Hallo van Hallo tabel toouse met dit voorbeeld

   * HBaseTableColumnFamily: Hallo kolom familienaam

     ![Afbeelding van dialoogvenster Instellingen](./media/hdinsight-storm-correlation-topology/settings.png)

4. Hallo-oplossing worden uitgevoerd. Wanneer u wordt gevraagd, selecteert u Hallo 'c' sleutel toocreate Hallo tabel op uw HBase-cluster.

## <a name="build-and-deploy-hello-storm-topology"></a>Bouw en implementeer Hallo Storm-topologie

1. Open Hallo **CorrelationTopology** oplossing in Visual Studio.

2. In **Solution Explorer**, klik met de rechtermuisknop Hallo **CorrelationTopology** project en selecteer Eigenschappen.

3. Selecteer in het venster Eigenschappen Hallo **instellingen** en Voer Hallo configuratiewaarden voor dit project. Hallo eerste 5 zijn Hallo dezelfde waarden gebruikt door Hallo **SessionInfo** project:

   * HBaseClusterURL: Hallo URL tooyour HBase-cluster. Bijvoorbeeld: https://myhbasecluster.azurehdinsight.net.

   * HBaseClusterUserName: Hallo beheerder/HTTP-gebruikersaccount voor uw cluster.

   * HBaseClusterPassword: Hallo wachtwoord voor Hallo beheerder/HTTP-gebruikersaccount.

   * HBaseTableName: naam van Hallo van Hallo tabel toouse met dit voorbeeld. Deze waarde dezelfde is Hallo tabelnaam zoals gebruikt in Hallo SessionInfo project.

   * HBaseTableColumnFamily: Hallo familie kolomnaam. Deze waarde is Hallo dezelfde familienaam kolom zoals gebruikt in Hallo SessionInfo project.

   > [!IMPORTANT]
   > Niet Hallo HBaseTableColumnNames, wijzigen, omdat zijn standaard Hallo Hallo namen die worden gebruikt door **SessionInfo** tooretrieve gegevens.

4. Hallo eigenschappen opslaan en vervolgens Hallo-project te bouwen.

5. In **Solution Explorer**, met de rechtermuisknop op het Hallo-project en selecteer **indienen tooStorm op HDInsight**. Als u wordt gevraagd, voert u Hallo referenties voor uw Azure-abonnement.

   ![Afbeelding van Hallo indienen toostorm menu-item](./media/hdinsight-storm-correlation-topology/submittostorm.png)

6. In Hallo **indienen topologie** dialoogvenster, selecteer Hallo Storm-cluster toodeploy deze topologie gewenste.

   > [!NOTE]
   > Hallo duurt eerst u een topologie dient een paar seconden tooretrieve Hallo-naam van uw HDInsight-clusters.

7. Zodra het Hallo-topologie is geüpload en ingediende toohello cluster, Hallo **Storm-Topologieweergave** wordt geopend en Hallo topologie wordt uitgevoerd. toorefresh hello gegevens, selecteer Hallo **CorrelationTopology** en gebruik de knop Vernieuwen Hallo op Hallo rechts op de pagina Hallo top.

   ![Afbeelding van Hallo Topologieweergave](./media/hdinsight-storm-correlation-topology/topologyview.png)

   Wanneer Hallo topologie begint het genereren van gegevens, de waarde in Hallo Hallo **lichten** kolom stappen.

   > [!NOTE]
   > Als hello **Storm-Topologieweergave** niet automatisch wordt geopend, gebruikt u Hallo volgende stappen tooopen het:
   >
   > 1. In **Solution Explorer**, vouw **Azure**, en vouw vervolgens **HDInsight**.
   > 2. Klik met de rechtermuisknop Hallo Storm-cluster die Hallo topologie wordt uitgevoerd op en selecteer vervolgens **Storm-topologieën weergeven**

## <a name="query-hello-data"></a>Hallo querygegevens

Zodra heeft gegevens zijn verzonden, gebruikt u Hallo stappen tooquery Hallo gegevens te volgen.

1. Retourneren van toohello **SessionInfo** project. Als niet wordt uitgevoerd, start u een nieuw exemplaar van deze.

2. Wanneer u wordt gevraagd, selecteert u **s** toosearch voor START-gebeurtenis. U bent na vragen aan gebruiker tooenter een start en end tijd toodefine een tijdsbereik - worden alleen gebeurtenissen tussen deze twee keer geretourneerd.

    Gebruik Hallo volgende formatteren bij het invoeren van Hallo begin- en eindtijden: uu: mm en de 'M' of 'pm'. Bijvoorbeeld: 23:20 uur.

    gebeurtenissen vastgelegd tooreturn, een begin-tijdstip voordat Hallo Storm-topologie is geïmplementeerd en eindtijd van nu gebruiken. Hallo beleidsretourgegevens bevat vermeldingen vergelijkbare toohello volgende tekst:

        Session e6992b3e-79be-4991-afcf-5cb47dd1c81c started at 6/5/2015 6:10:15 PM. Timestamp = 1433527820737

Zoeken naar einde gebeurtenissen works Hallo dezelfde als begin-gebeurtenissen. END-gebeurtenissen worden echter willekeurig gegenereerd tussen 1 en 5 minuten na Hallo startgebeurtenis. Mogelijk hebt u tootry enkele tijd bereiken toofind Hallo END gebeurtenissen. END-gebeurtenissen bevatten ook Hallo duur van Hallo sessie - Hallo verschil tussen Hallo gebeurtenis begintijd en eindtijd van de gebeurtenis. Hier volgt een voorbeeld van gegevens voor END-gebeurtenissen:

    Session fc9fa8e6-6892-4073-93b3-a587040d892e lasted 2 minutes, and ended at 6/5/2015 6:12:15 PM

> [!NOTE]
> Hoewel Hallo tijdwaarden die u invoert in de lokale tijd, is Hallo tijd geretourneerde Hallo query ingesteld op UTC.

## <a name="stop-hello-topology"></a>Hallo-topologie stoppen

Wanneer u klaar toostop Hallo-topologie bent, retourneren toohello **CorrelationTopology** -project in Visual Studio. In Hallo **Storm-Topologieweergave**, selecteert u Hallo topologie en gebruik vervolgens Hallo **Kill** knop Hallo boven aan het Hallo-topologie weergeven.

## <a name="delete-your-cluster"></a>Uw cluster verwijderen

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-steps"></a>Volgende stappen

Zie voor meer voorbeelden van Storm [voorbeeldtopologieën van Storm op HDInsight](hdinsight-storm-example-topology.md).

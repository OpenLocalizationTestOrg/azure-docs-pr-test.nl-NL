---
title: 'Analytics platforms: Apache Storm vergelijking tooStream Analytics | Microsoft Docs'
description: Lees hoe u een cloudplatform analytics kiezen met behulp van een Apache Storm vergelijking tooStream Analytics. Verschillen in functies en begrijpen.
keywords: Analytics platform, analytics platforms, cloudplatform analytics, storm-vergelijking
services: stream-analytics
documentationcenter: 
author: samacha
manager: jhubbard
editor: cgronlun
ms.assetid: b9aac017-9866-4d0a-b98f-6f03881e9339
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/27/2017
ms.author: samacha
ms.openlocfilehash: 5a0ec5b2439596f0da962f04b776472031660062
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="choosing-a-streaming-analytics-platform-comparing-apache-storm-and-azure-stream-analytics"></a>Een streaming analytics platform kiezen: vergelijking van Apache Storm en Azure Stream Analytics
Azure biedt verschillende oplossingen voor het analyseren van streaminggegevens: [Azure Streaming Analytics](https://docs.microsoft.com/azure/stream-analytics/) en [Apache Storm op Azure HDInsight](https://azure.microsoft.com/services/hdinsight/apache-storm/). Beide platforms analytics bieden Hallo voordelen van een PaaS-oplossing. Maar Hallo platforms hebben enkele belangrijke verschillen in hun mogelijkheden ook als u in hoe u configureren en beheren. 

Dit artikel bevat een side-by-side vergelijking van functies toohelp die u tussen Apache Storm en Azure Stream Analytics als een cloud analytics platform kiezen. 

## <a name="general-features"></a>Algemene functies

<table border="1" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td width="174" valign="top">
                <p>
                    <strong> </strong>
                </p>
            </td>
            <td width="204" valign="top">
                <p>
                    <strong>Azure Stream Analytics</strong>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
                    <strong>Apache Storm op HDInsight</strong>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p>
                    <strong>Open-source?</strong>
                </p>
            </td>
            <td width="204" valign="top">
                <p>
Nee. Azure Stream Analytics is een Microsoft-bedrijfseigen aanbieden.
                </p>
            </td>
            <td width="246" valign="top">
                <p>
Ja. Apache Storm is een technologie Apache in licentie gegeven.
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p>
                    <strong>Ondersteuning van Microsoft?</strong>
                </p>
            </td>
            <td width="204" valign="top">
                <p>
Ja </p>
            </td>
            <td width="246" valign="top">
                <p>
Ja </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p>
                    <strong>Hardwarevereisten</strong>
                </p>
            </td>
            <td width="204" valign="top">
                <p>
Geen. Azure Stream Analytics is een Azure-Service.
                </p>
            </td>
            <td width="246" valign="top">
                <p>
Geen. Apache Storm is een Azure-Service.
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p>
                    <strong>Op het hoogste niveau eenheid</strong>
                </p>
            </td>
            <td width="204" valign="top">
                <p>
Gebruikers implementeren en controleren van de streaming-taken.
                </p>
            </td>
            <td width="246" valign="top">
                <p>
Gebruikers implementeren en controleren van een hele cluster, wat hosten kan meerdere Storm-taken, evenals andere werkbelastingen (inclusief batch).
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p>
                    <strong>Prijzen</strong>
                </p>
            </td>
            <td width="204" valign="top">
                <p>
Prijs per volume van de gegevens die worden verwerkt en het aantal streaming-eenheden per uur wordt vereist die taak Hallo Hallo wordt uitgevoerd. 
                </p>
                    <p>Zie voor meer informatie <a href="http://azure.microsoft.com/pricing/details/stream-analytics/">Stream Analytics prijzen</a>.</p>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
Hallo-eenheid na aankoop op basis van het cluster is en u betaalt op Hallo tijd Hallo cluster wordt uitgevoerd, onafhankelijk van de taken die zijn geïmplementeerd.
                </p>
                <p>
Zie voor meer informatie <a href="http://azure.microsoft.com/pricing/details/hdinsight/">HDInsight prijzen</a>.
                </p>
            </td>
        </tr>
    </tbody>
</table>

## <a name="authoring"></a>Ontwerpen

<table border="1" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td width="174" valign="top">
                <p>
                    <strong> </strong>
                </p>
            </td>
            <td width="204" valign="top">
                <p>
                    <strong>Azure Stream Analytics</strong>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
                    <strong>Apache Storm op HDInsight</strong>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p>
                    <strong>Mogelijkheden: SQL DSL?</strong>
                </p>
            </td>
            <td width="204" valign="top">
                <p>
Ja. Stream Analytics biedt een SQL-achtige taal voor het maken van transformaties.
                </p>
            </td>
            <td width="246" valign="top">
                <p>
Nee. Gebruikers schrijven van code in Java of C# of Trident-API's gebruiken.
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p>
                    <strong>Mogelijkheden: Tijdelijke operators?</strong>
                </p>
            </td>
            <td width="204" valign="top">
                <p>
Functies in vensters en tijdelijke joins, worden standaard ondersteund.
                </p>
            </td>
            <td width="246" valign="top">
                <p>
Tijdelijke operators moeten worden geïmplementeerd door Hallo-gebruiker.
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p>
                    <strong>Ontwikkeling biedt</strong>
                </p>
            </td>
            <td width="204" valign="top">
                <p>
Gebruikers kunnen maken, foutopsporing, taken en bewaken via hello Azure-portal met voorbeeldgegevens die zijn afgeleid van een live stream.
                </p>
            </td>
            <td width="246" valign="top">
                <p>
Gebruikers met .NET kunnen ontwikkelen, fouten opsporen en controleren met Visual Studio. Gebruikers met behulp van Java of andere talen kunnen Hallo IDE van hun keuze gebruiken.
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p>
                    <strong>Ondersteuning voor foutopsporing</strong>
                </p>
            </td>
            <td width="204" valign="top">
                <p>
Algemene status en de bewerkingen taaklogboeken zijn beschikbaar toohelp foutopsporing. Stream Analytics momenteel kiest, kunnen gebruikers inhoud of hoeveel inhoud is opgenomen in het Hallo-Logboeken (dat wil zeggen, uitgebreide modus) opgeven.
                </p>
            </td>
            <td width="246" valign="top">
                <p>
Gedetailleerde logboeken zijn beschikbaar. Gebruikers hebben toegang tot logboeken in Visual Studio of door logboekregistratie in toohello cluster en rechtstreekse toegang tot Hallo Logboeken.
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p>
                    <strong>Uitbreidbaarheid met behulp van aangepaste code?</strong>
                </p>
            </td>
            <td width="204" valign="top">
                <p>
Ondersteuning voor gedeeltelijk met JavaScript UDF's. Zie voor meer informatie <a href="https://docs.microsoft.com/azure/stream-analytics/stream-analytics-javascript-user-defined-functions">integratie van JavaScript UDF</a>.
                </p>
            </td>
            <td width="246" valign="top">
                <p>
Ja. Gebruikers kunnen aangepaste code schrijven in C#, Java of een andere taal ondersteund op Storm.
                </p>
            </td>
        </tr>
    </tbody>
</table>

## <a name="data-sources-inputs-and-outputs"></a>Gegevensbronnen (invoer) en uitvoer ##

<table border="1" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td width="174" valign="top">
                <p>
                    <strong> </strong>
                </p>
            </td>
            <td width="204" valign="top">
                <p>
                    <strong>Azure Stream Analytics</strong>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
                    <strong>Apache Storm op HDInsight</strong>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p>
                 <strong>Invoer gegevensbronnen</strong>
                </p>
            </td>
            <td width="204" valign="top">
                <p>Azure Event Hubs en Azure Blob-opslag.
                </p>
            </td>
            <td width="246" valign="top">
                <p>
Connectors zijn beschikbaar voor Azure Event Hubs, Azure Service Bus en Kafka. Gebruikers kunnen aanvullende connectors met aangepaste code maken.
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p>
                    <strong>Invoergegevens indelingen</strong>
                </p>
            </td>
            <td width="204" valign="top">
                <p>
Avro JSON, CSV </p>
            </td>
            <td width="246" valign="top">
                <p>
Gebruikers kunnen een willekeurige indeling met aangepaste code implementeren.
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p>
                    <strong>Uitvoer</strong>
                </p>
            </td>
            <td width="204" valign="top">
                <p>
Een streaming-taak kan meerdere uitgangen hebben. Ondersteunde uitgangen zijn Azure Event Hubs, Azure Blob storage, Azure Table storage, Azure SQL DB en Power BI.
                </p>
            </td>
            <td width="246" valign="top">
                <p>
Storm ondersteunt vele uitvoer in een topologie en elke uitvoer kan aangepaste regels voor de downstreamverwerking hebben. Storm omvat connectors voor Power BI, Azure Event Hubs, Azure Blob storage, Azure Cosmos DB, SQL en HBase. Gebruikers kunnen aanvullende connectors met aangepaste code maken.    
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p>
                    <strong>Gegevenscodering indelingen</strong>
                </p>
            </td>
            <td width="204" valign="top">
                <p>
Gegevens moeten worden geformatteerd met UTF-8.
                </p>
            </td>   
            <td width="246" valign="top">
                <p>
Gebruikers kunnen gegevens de coderingsindeling met aangepaste code implementeren.
                </p>
            </td>
        </tr>
    </tbody>
</table>

## <a name="management-and-operations"></a>Beheer van en bewerkingen ##

<table border="1" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td width="174" valign="top">
                <p>
                    <strong> </strong>
                </p>
            </td>
            <td width="204" valign="top">
                <p>
                    <strong>Azure Stream Analytics</strong>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
                    <strong>Apache Storm op HDInsight</strong>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p>
                    <strong>Taak implementatiemodel</strong>
                </p>
            </td>
            <td width="204" valign="top">
                <p>
Azure-portal, PowerShell en REST-API's.
                </p>
            </td>
            <td width="246" valign="top">
                <p>
Azure-portal, PowerShell, Visual Studio en REST-API's.
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p>
                    <strong>Monitoring (statistieken, prestatiemeteritems, enz.)</strong>
                </p>
            </td>
            <td width="204" valign="top">
                <p>
Bewaking is geïmplementeerd met behulp van Azure-portal en de REST-API's. Gebruikers kunnen ook configureren voor waarschuwingen van Azure.
                </p>
            </td>
            <td width="246" valign="top">
                <p>
Bewaking is geïmplementeerd met behulp van Hallo Storm-gebruikersinterface en REST-API's.
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p>
                    <strong>Schaalbaarheid</strong>
                </p>
            </td>
            <td width="204" valign="top">
                <p>
Schaalbaarheid wordt bepaald door Hallo aantal Streaming Units (SUs) voor elke taak. Elke Streaming-eenheid van de processen van too1 MB per seconde, met een maximum 50 eenheden. Zie voor meer informatie <a href="https://docs.microsoft.com/azure/stream-analytics/stream-analytics-scale-jobs">Scale tooincrease doorvoer</a>.
                </p>
            </td>
            <td width="246" valign="top">
                <p>
Schaalbaarheid wordt bepaald door het aantal knooppunten in HDInsight Storm-cluster Hallo Hallo. Hallo bovenste limiet voor het aantal knooppunten hello wordt gedefinieerd door Azure quotum Hallo van de gebruiker.
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p>
                    <strong>Limieten voor gegevensverwerking</strong>
                </p>
            </td>
            <td width="204" valign="top">
                <p>
Gebruikers kunnen verhogen gegevensverwerking of kosten optimaliseren door het vergroten of verkleinen van Hallo aantal Streaming-eenheden met een bovengrens van 1 GB per seconde.
                </p>
            </td>
            <td width="246" valign="top">
                <p>
Gebruikers kunnen clustergrootte omhoog of omlaag schalen.
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p>
                    <strong>Stop/hervatten</strong>
                </p>
            </td>
            <td width="204" valign="top">
                <p>
Stoppen en hervatten van de laatste plaats gestopt.
                </p>
            </td>
            <td width="246" valign="top">
                <p>
Stoppen en hervatten van laatste gestopt plaats op basis van een watermerk.
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p>
                    <strong>Update-service en framework</strong>
                </p>
            </td>
            <td width="204" valign="top">
                <p>
Automatisch patchen zonder uitvaltijd.
                </p>
            </td>
            <td width="246" valign="top">
                <p>
Automatisch patchen zonder uitvaltijd.
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p>
                    <strong>Zakelijke continuïteit via een maximaal beschikbare Service met de gegarandeerde Sla 's</strong>
                </p>
            </td>
            <td width="204" valign="top">
                <ul>
                <li>SLA van 99,9% beschikbaarheid</li>
                <li>Automatisch herstel van fouten</li>
                <li>Ingebouwde herstel van stateful tijdelijke operators</li>
                </ul>
            </td>
            <td width="246" valign="top">
                <p>
SLA van 99,9% beschikbaarheid van Hallo Storm-cluster. 
                </p>
                <p>
Apache Storm is een fouttolerante streaming platform. Het is echter van Hallo gebruiker verantwoordelijkheid tooensure dat streaming uitvoeren ononderbroken taken.
                </p>
            </td>
        </tr>
    </tbody>
</table>

## <a name="advanced-features"></a>Geavanceerde functies ##

<table border="1" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td width="174" valign="top">
                <p>
                    <strong> </strong>
                </p>
            </td>
            <td width="204" valign="top">
                <p>
                    <strong>Azure Stream Analytics</strong>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
                    <strong>Apache Storm op HDInsight</strong>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p>
                    <strong>Laat aankomst en out-van-order gebeurtenisverwerking</strong>
                </p>
            </td>
            <td width="204" valign="top">
                <p>
Ingebouwde configureerbaar beleid kunnen opnieuw rangschikken van gebeurtenissen, verwijdert u gebeurtenissen of gebeurtenistijd aanpassen.
                </p>
            </td>
            <td width="246" valign="top">
                <p>
Gebruikers moeten logica toohandle dit scenario implementeren.
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p>
                    <strong>Referentiegegevens</strong>
                </p>
            </td>
            <td width="204" valign="top">
                <p>
Referentiegegevens is beschikbaar via Azure Blob-opslag met een maximum van 100 MB van de cache in het geheugen. Referentiegegevens wordt door Hallo-service vernieuwd.
                </p>
            </td>
            <td width="246" valign="top">
                <p>
Er zijn geen limieten op de omvang van gegevens. Connectors zijn beschikbaar voor HBase, Azure Cosmos DB, SQL Server en Azure. Gebruikers kunnen aanvullende connectors met aangepaste code maken. Referentiegegevens moeten worden vernieuwd met aangepaste code.
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p>
                    <strong>Integratie met Machine Learning</strong>
                </p>
            </td>
            <td width="204" valign="top">
                <p>
Azure Machine Learning-modellen als functies kunnen worden geconfigureerd tijdens het maken van de taak wordt gepubliceerd. Zie voor meer informatie <a href="https://docs.microsoft.com/azure/stream-analytics/stream-analytics-scale-with-machine-learning-functions">schaal voor Machine Learning-functies</a>.
                </p>
            </td>
            <td width="246" valign="top">
                <p>
Beschikbaar via Storm Bolts.
                </p>
            </td>
        </tr>
    </tbody>
</table>

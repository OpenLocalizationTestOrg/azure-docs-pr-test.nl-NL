---
title: aaaData Factory gebruiksvoorbeeld - aanbevelingen
description: "Meer informatie over een gebruiksvoorbeeld geïmplementeerd met behulp van Azure Data Factory samen met andere services."
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: 6f1523c7-46c3-4b8d-9ed6-b847ae5ec4ae
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: shlo
ms.openlocfilehash: d7912965fe4762d64e8ca3c28381ea6187f36631
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-case---product-recommendations"></a>Use case: productaanbevelingen
Azure Data Factory is een veel services gebruikt tooimplement Hallo Cortana Intelligence Suite van oplossing accelerators aan te schaffen.  Zie [Cortana Intelligence Suite](http://www.microsoft.com/cortanaanalytics) pagina voor meer informatie over dit pakket. Een algemene gebruiksvoorbeeld die Azure-gebruikers hebben al opgelost en geïmplementeerd met behulp van Azure Data Factory en andere Cortana Intelligence-onderdeel-services worden beschreven in dit document.

## <a name="scenario"></a>Scenario
Onlinewinkels wilt vaak tooentice hun klanten toopurchase producten in de vorm met producten ze waarschijnlijk toobe geïnteresseerd in, en daarom waarschijnlijk toobuy. tooaccomplish dit onlinewinkels moeten toocustomize hun online gebruikerservaring met behulp van aangepaste aanbevelingen voor die specifieke gebruiker. Deze persoonlijke aanbevelingen zijn gemaakt op basis van hun huidige en historische winkelwagen gedragsgegevens, productinformatie, toobe geïntroduceerd zojuist merken en product en klant segmentatie-gegevens.  Daarnaast kunnen ze Hallo gebruiker aanbevelingen op basis van de analyse van gedrag voor algemene informatie over het gebruik van hun gebruikers die zijn gecombineerd bieden.

Hallo-doel van deze winkels is toooptimize voor gebruiker klik naar verkoop conversies en hogere omzet behalen.  Zij bereiken deze conversie door het leveren van contextuele, op basis van gedrag aanbevelingen op basis van de klant interesses en acties. Dit geval gebruiken we onlinewinkels gebruiken als een voorbeeld van bedrijven die toooptimize voor hun klanten. Deze principes zijn echter tooany bedrijven die tooengage wil toepassen zijn klanten rond de goederen en services en verbeter hun klanten kopen ervaring met persoonlijke aanbevelingen.

## <a name="challenges"></a>Uitdagingen
Er zijn veel uitdagingen die face onlinewinkels bij het tooimplement dit soort gebruiksvoorbeeld. 

Gegevens van verschillende grootte en vormen moet eerst worden ingenomen uit meerdere gegevensbronnen, zowel on-premises en in de cloud Hallo. Deze gegevens omvatten productgegevens en gedrag van historische klantgegevens gebruikersgegevens, zoals Hallo gebruiker Hallo online retail-site bladert. 

Tweede, persoonlijke productaanbevelingen moeten worden redelijkerwijs en nauwkeurig berekend en voorspeld. Daarnaast moeten tooproduct, merk en gedrag en browser klantgegevens, onlinewinkels ook tooinclude feedback van afgelopen aankopen toofactor in Hallo bepaling van de beste productaanbevelingen Hallo voor Hallo-gebruiker. 

Hallo aanbevelingen moeten derde worden onmiddellijk product toohello gebruiker tooprovide een naadloze bladeren en ervaring aanschaffen en aanbevelingen in de meest recente en relevante Hallo. 

Ten slotte retailers toomeasure Hallo effectiviteit van hun keuze moeten door het bijhouden van de algehele Upsell cross-verkopen klikken voor conversie verkoop successen en tootheir toekomstige aanbevelingen aanpassen.

## <a name="solution-overview"></a>Overzicht van de oplossing
In dit voorbeeld gebruiksvoorbeeld is opgelost en geïmplementeerd door de echte Azure-gebruikers met behulp van Azure Data Factory en andere Cortana Intelligence componentservices, waaronder [HDInsight](https://azure.microsoft.com/services/hdinsight/) en [Power BI](https://powerbi.microsoft.com/).

Hallo online detailhandel maakt gebruik van een Azure Blob-opslag, een lokale SQL server, Azure SQL-database en een relationele datamart als hun opties voor het opslaan van gegevens in de gehele Hallo-werkstroom.  Hallo blob-archief bevat klantgegevens, klantgegevens gedrag en informatie van productgegevens. lokale Hallo productinformatie gegevens omvatten merk-productinformatie en een productcatalogus opgeslagen in een SQL datawarehouse. 

Alle Hallo-gegevens worden gecombineerd en in een aanbeveling system toodeliver persoonlijke aanbevelingen op basis van de klant interesses en acties, terwijl Hallo gebruiker bladert producten in de catalogus Hallo op Hallo website ingevoerd. Hallo klanten ook producten die betrekking hebben ze kijkt toohello-product op basis van algemene website gebruikspatronen die geen gerelateerde tooany één gebruiker worden weergegeven.

![use case-diagram](./media/data-factory-product-reco-usecase/diagram-1.png)

Gigabytes van onbewerkte web logboekbestanden worden dagelijks van Hallo online detailhandel website gegenereerd als semi-gestructureerde bestanden. Hallo onbewerkte web-logboekbestanden en Hallo klant en product catalogusgegevens regelmatig in een Azure Blob-opslag met behulp van de Data Factory globaal geïmplementeerde gegevensverplaatsing als een service wordt ingenomen. Hallo onbewerkte logboekbestanden voor Hallo dag worden gepartitioneerd (door jaar en maand) in de blobopslag voor langdurige opslag.  [Azure HDInsight](https://azure.microsoft.com/services/hdinsight/) gebruikte toopartition Hallo onbewerkte logboekbestanden in Hallo blob is store en proces Hallo ingenomen logboeken op grote schaal met behulp van zowel Hive en Pig-scripts. Hallo gepartitioneerde weblogboeken gegevens en verwerkte tooextract Hallo invoer nodig is voor een machine learning aanbeveling system toogenerate Hallo persoonlijke aanbevelingen.

Hallo aanbeveling systeem dat wordt gebruikt voor Hallo machine learning in dit voorbeeld is een open-source machine learning-aanbeveling platform van [Apache Mahout](http://mahout.apache.org/).  Alle [Azure Machine Learning](https://azure.microsoft.com/services/machine-learning/) of aangepaste model kan worden toegepast toohello scenario.  Hallo Mahout model is gebruikte toopredict Hallo overeenkomsten tussen items op Hallo-website op basis van algemene gebruikspatronen en toogenerate Hallo persoonlijke aanbevelingen op basis van afzonderlijke Hallo-gebruiker.

Ten slotte is de resultaatset Hallo van persoonlijke aanbevelingen verplaatste tooa relationele datamart voor verbruik door Hallo detailhandel website.  Hallo resultatenset door een andere toepassing ook rechtstreeks vanuit de blob-opslag kan worden geopend of tooadditional winkels voor andere consumenten en gebruiksvoorbeelden verplaatst.

## <a name="benefits"></a>Voordelen
Hallo oplossing voldaan door hun product aanbeveling strategie te optimaliseren en het afstemmen met doelen, Hallo online detailhandel aanbevelingen en doelstellingen marketing. Bovendien kunnen toooperationalize zijn en Hallo product aanbeveling werkstroom op een efficiënte, betrouwbare en rendabele manier beheren. Hallo benadering handomdraai voor hen tooupdate hun model en de effectiviteit op basis van metingen Hallo verkoop klikken voor conversie successen verfijnen. Met behulp van Azure Data Factory, ze kunnen tooabandon hun tijdrovend en kostbaar handmatige cloud resourcemanagement en waren tooon aanvraag cloud Resourcemanagement verplaatsen. Daarom kunnen toosave tijd, geld, zijn en hun toosolution tijd implementatie verminderen. Afkomst gegevensweergaven en operationele servicestatus eenvoudig toovisualize is geworden en problemen oplossen met Hallo intuïtieve Data Factory bewaking en beheer gebruikersinterface die beschikbaar is via hello Azure-portal. De oplossing kan nu worden gepland en beheerd zodat voltooide data betrouwbaar is gemaakt en geleverd toousers en gegevens en afhankelijkheden van de verwerking wordt automatisch beheerd zonder menselijke tussenkomst.

Dankzij deze persoonlijke ervaring hello online detailhandel gemaakt van een klant meer concurrerende, aantrekkelijke optreden en daarom verkoop en de algehele klanttevredenheid te verhogen.


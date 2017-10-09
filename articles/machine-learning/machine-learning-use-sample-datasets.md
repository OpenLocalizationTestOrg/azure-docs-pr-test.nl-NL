---
title: aaaUse hello voorbeeldgegevenssets in Machine Learning Studio | Microsoft Docs
description: Beschrijvingen van Hallo-gegevenssets die worden gebruikt in samplemodellen opgenomen in Machine Learning Studio. U kunt deze voorbeeldgegevenssets gebruiken voor uw experimenten.
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 03a0b844-e8a7-4896-996f-d3c7a0db7a50
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: garye
ms.openlocfilehash: c7786478db82d40aaf27c37b3947ded5f042dd70
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-sample-datasets-in-azure-machine-learning-studio"></a>Hallo voorbeeldgegevenssets in Azure Machine Learning Studio gebruiken
[top]: #machine-learning-sample-datasets

Wanneer u een nieuwe werkruimte in Azure Machine Learning maakt, worden een aantal voorbeeldgegevenssets en experimenten standaard opgenomen. Veel van deze voorbeeldgegevenssets worden gebruikt door Hallo samplemodellen in Hallo [Azure Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com/). Andere zijn opgenomen als voorbeelden van verschillende soorten gegevens doorgaans gebruikt in machine learning.

Sommige van deze gegevenssets zijn beschikbaar in Azure Blob-opslag. Voor deze gegevenssets biedt Hallo volgende tabel een rechtstreekse koppeling. U kunt deze gegevenssets in uw experimenten gebruiken met behulp van Hallo [importgegevens] [ import-data] module.

Hallo rest van deze voorbeeldgegevenssets die beschikbaar zijn in uw werkruimte **gegevenssets opgeslagen** in Hallo module palet toohello links van Hallo experimentcanvas bij het openen of maken van een nieuw experiment in Machine Learning Studio.
U kunt een van deze gegevenssets in uw eigen experimenten gebruiken door het experimentcanvas tooyour te slepen.


[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<table>

<tr>
  <th align=left>De naam van de gegevensset</th>
  <th align=left>Beschrijving van gegevensset</th>
</tr>

<tr>
  <td valign=top>Volwassenen inventarisering Income binaire classificatie gegevensset</td>
  <td valign=top>
Een subset van Hallo 1994 telling database, met behulp van de werkende volwassenen via Hallo leeftijd van 16 met een aangepaste inkomsten index met > 100.<p> </p><b>Gebruik:</b> classificeren van mensen met demografische gegevens toopredict of een persoon meer dan 50 K per jaar verdient.<p> </p><b>Verwante Research:</b> Kohavi, R., Becker, B., (1996). UCI Machine Learning-opslagplaats <a href="http://archive.ics.uci.edu/ml">http://archive.ics.uci.edu/ml</a>. Irvine, CA: Universiteit van Californië, School van gegevens en Computer wetenschappelijke </td>
</tr>

<tr ID=airport-codes-dataset>
  <td valign=top>Luchthaven Codes gegevensset</td>
  <td valign=top>
VS luchthaven codes.<p> </p>Deze gegevensset bevat een rij voor elke luchthaven VS, bieden Hallo luchthaven id-nummer en de naam samen met de Hallo locatie plaats en provincie.
  </td>
</tr>

<tr>
  <td valign=top>Auto price data (Raw)</td>
  <td valign=top>
Informatie over auto's door merk en model, inclusief Hallo prijs, functies, zoals Hallo aantal cilinders en MPG, evenals een verzekering risicoscore.<p> </p>Hallo risicoscore is in eerste instantie gekoppeld aan de prijs voor automatisch en vervolgens werkelijke risico's in een proces genaamd tooactuaries als symboling worden aangepast. Een waarde van + 3 geeft aan dat Hallo automatisch riskant, en een waarde van -3 dat deze waarschijnlijk veilig is.<p> </p><b>Gebruik:</b> risicoscore van Voorspellingslengte Hallo door onderdelen, met regressie of multivariate classificatie. <p> </p><b>Verwante Research:</b> Schlimmer, J.C. (1987). UCI Machine Learning-opslagplaats <a href="http://archive.ics.uci.edu/ml">http://archive.ics.uci.edu/ml</a>. Irvine, CA: Universiteit van Californië, School van gegevens en Computer wetenschappelijke </td>
</tr>

<tr ID=bike-rental-uci-dataset>
  <td valign=top>Fiets verhuur UCI gegevensset</td>
  <td valign=top>
UCI fiets verhuur gegevensset op basis van echte gegevens van kapitaal Bikeshare bedrijf dat een fiets verhuur-netwerk in Washington DC onderhoudt.<p> </p>Hallo gegevensset heeft een rij voor elk uur van elke dag in 2011 en 2012 voor een totaal van 17,379 rijen. Hallo-bereik van elk uur fiets huren loopt van 1 too977.

  </td>
</tr>

<tr ID=bill-gates-rgb-image>
  <td valign=top>Factuur poorten RGB-afbeelding</td>
  <td valign=top>
Openbaar installatiekopiebestand geconverteerd tooCSV gegevens.<p> </p>Hallo code voor het converteren van de installatiekopie van het Hallo wordt geleverd in Hallo <strong>kwantisatiefouten gebruik K-Means clustering kleur</strong> detailpagina model.
  </td>
</tr>

<tr>
  <td valign=top>Bloed donatie gegevens</td>
  <td valign=top>
Een subset van gegevens uit de database van Hallo bloed donor Hallo bloed transfusie Service Center van Hsin Chu stad, Taiwan.<p> </p>Donor gegevens omvatten Hallo maanden sinds de laatste donatie), en frequentie of Hallo totale aantal donaties, tijd sinds laatste donatie en hoeveelheid laatste officieel gedoneerd.<p> </p><b>Gebruik:</b> Hallo streeft toopredict via classificatie of Hallo donor gedoneerd bloed in maart 2007, waarbij 1 geeft aan een donor tijdens Hallo Doelperiode en 0 dat niet donor. <p> </p><b>Verwante Research:</b> Yeh I.C., (2008). UCI Machine Learning-opslagplaats <a href="http://archive.ics.uci.edu/ml">http://archive.ics.uci.edu/ml</a>. Irvine, CA: Universiteit van Californië, School van gegevens en Computer wetenschappelijke <p> </p>Yeh, ik-Cheng, Yang, koning-Jang en Ting, Tao-Ming ' Knowledge detectie op RFM model Bernoulli-reeks met ' Expert systemen met toepassingen, 2008 <a href="http://dx.doi.org/10.1016/j.eswa.2008.07.018">http://dx.doi.org/10.1016/j.eswa.2008.07.018</a>
  </td>
</tr>

<tr ID=book-reviews-from-amazon>
  <td valign=top>Beoordelingen van Amazon adresboek</td>
  <td valign=top>
Beoordelingen van books in Amazon, die afkomstig zijn uit Hallo amazon.com website door onderzoekers universiteit van Pennsylvania (<a href="http://www.cs.jhu.edu/~mdredze/datasets/sentiment/">gevoel</a>). Hallo onderzoeksrapport, Zie ' biografieën, Bollywood, giek vakken en Blenders: domein aanpassing voor gevoel classificatie ' John Blitzer, markeren Dredze en Fernando Pereira; Koppeling van rekenkundige Linguistics (ACL) 2007.<p> </p>de oorspronkelijke gegevensset Hallo heeft 975K beoordelingen met classificatie 1, 2, 3, 4 of 5. Hallo-beoordelingen zijn geschreven in het Engels en afkomstig zijn van Hallo periode 1997 2007. Deze gegevensset is too10K omlaag actieve beoordelingen zijn.
  </td>
</tr>

<tr>
  <td valign=top>Gegevens en</td>
  <td valign=top>
Een van drie kanker-gerelateerde gegevenssets geleverd door Hallo Oncology Institute die vaak in machine learning-documentatie verschijnt. Diagnostische gegevens met functies van een laboratorium-analyse van ongeveer 300 weefsel voorbeelden combineert.<p> </p><b>Gebruik:</b> Hallo type kanker classificeren, op basis van 9 kenmerken, waarvan sommige zijn lineaire en andere categorische. <p> </p><b>Verwante Research:</b> Wohlberg, W.H., straat, W.N. & Mangasarian, O.L. (1995). UCI Machine Learning-opslagplaats <a href="http://archive.ics.uci.edu/ml">http://archive.ics.uci.edu/ml</a>. Irvine, CA: Universiteit van Californië, School van gegevens en Computer wetenschappelijke </td>
</tr>

<tr ID=breast-cancer-features>
  <td valign=top>En kanker functies <td valign=top>
Hallo gegevensset bevat informatie voor 102K verdachte regio's (kandidaten) van volledige-installatiekopieën, door 117 functies beschreven. Hallo-mogelijkheden zijn eigen en hun betekenis niet door Hallo gegevensset auteurs (Siemens gezondheidszorg) wordt getoond. 
  </td>
</tr>

<tr ID=breast-cancer-info>
  <td valign=top>En kanker Info</td>
  <td valign=top>
Hallo gegevensset bevat aanvullende informatie voor elke verdachte regio van de volledige installatiekopie. Elk voorbeeld bevat informatie (bijv, label patiënt coördinaten van de patch relatieve toohello volledige afbeelding-ID) over Hallo bijbehorende rijnummer in hello en kanker functies gegevensset. Elke geduld heeft een aantal voorbeelden. Voorbeelden zijn positief voor patiënten die beschikken over een kanker, en sommige negatief zijn. Voor patiënten die niet beschikken over een kanker, zijn alle voorbeelden negatief. Hallo gegevensset heeft 102K voorbeelden. Hallo dataset is gericht, 0,6% Hallo punten positief zijn, Hallo rest negatief zijn. Hallo dataset is door Siemens gezondheidszorg beschikbaar gesteld.
  </td>
</tr>

<tr ID=crm-appetency-labels-shared>
  <td valign=top>CRM Appetency Labels gedeeld</td>
  <td valign=top>
Labels van Hallo KDD kop 2009 klant relatie voorspelling challenge (<a href="http://www.sigkdd.org/site/2009/files/orange_small_train_appetency.labels">orange_small_train_appetency.labels</a>).
  </td>
</tr>

<tr ID=crm-churn-labels-shared>
  <td valign=top>CRM verloop Labels gedeeld</td>
  <td valign=top>
Labels van Hallo KDD kop 2009 klant relatie voorspelling challenge (<a href="http://www.sigkdd.org/site/2009/files/orange_small_train_churn.labels">orange_small_train_churn.labels</a>).
  </td>
</tr>

<tr ID=crm-dataset-shared>
  <td valign=top>Gedeelde CRM-gegevensset</td>
  <td valign=top>
Deze gegevens zijn afkomstig van Hallo KDD kop 2009 klant relatie voorspelling challenge (<a href="http://www.sigkdd.org/kdd-cup-2009-customer-relationship-prediction - orange_small_train.data.zip">orange_small_train.data.zip</a>).<p> </p>Hallo gegevensset bevat 50K klanten uit Hallo Frans telecommunicatie bedrijf oranje. Elke klant heeft 230 geanonimiseerde functies, 190 waarvan numerieke worden en 40 zijn categorische. Hallo-functies zijn zeer verspreid.
  </td>
</tr>

<tr ID=crm-upselling-labels-shared>
  <td valign=top>CRM Upselling Labels gedeeld</td>
  <td valign=top>
Labels van Hallo KDD kop 2009 klant relatie voorspelling challenge (<a href="http://www.sigkdd.org/site/2009/files/orange_large_train_upselling.labels">orange_large_train_upselling.labels</a>).
  </td>
</tr>

<tr>
  <td valign=top>Energie-efficiëntie regressie gegevens</td>
  <td valign=top>
Een verzameling gesimuleerde energie-profielen, op basis van 12 ander gebouw vormen. Hallo gebouwen worden onderscheiden door 8 functies, zoals glas gebied Hallo glas gebied distribueren en de afdrukstand.<p> </p><b>Gebruik:</b> regressie of classificatie toopredict Hallo energie-efficiëntie classificatie gebaseerde als een van twee echt gewaardeerd antwoorden gebruiken. Voor meerdere klasse-classificatie is ronde Hallo antwoord variabele toohello dichtstbijzijnde integer. <p> </p><b>Verwante Research:</b> Xifara, A. & Tsanas, A. (2012). UCI Machine Learning-opslagplaats <a href="http://archive.ics.uci.edu/ml">http://archive.ics.uci.edu/ml</a>. Irvine, CA: Universiteit van Californië, School van gegevens en Computer wetenschappelijke </td>
</tr>

<tr ID=flight-delays-data>
  <td valign=top>Vlucht uitstelt gegevens</td>
  <td valign=top>
Passagiers vlucht tijdige prestatiegegevens die afkomstig zijn uit Hallo TranStats gegevensverzameling Hallo VS Afdeling transport (<a href="http://www.transtats.bts.gov/DL_SelectFields.asp?Table_ID=236&DB_Short_Name=On-Time">tijdige</a>).<p> </p>Hallo gegevensset bevat Hallo periode April oktober 2013. Voordat u uploadt tooAzure Machine Learning Studio, is als volgt Hallo gegevensset verwerkt:<ul><li>Hallo dataset is gefilterde toocover alleen Hallo 70 drukste luchthavens Hallo Europese VS</li><li>Geannuleerde vlucht zijn gelabeld als door meer dan 15 minuten vertraagd</li><li>Omgereden vlucht zijn gefilterd.</li><li>Hallo volgende kolommen zijn geselecteerd: jaar, maand, DayofMonth, DayOfWeek, Carrier, OriginAirportID, DestAirportID, CRSDepTime, DepDelay, DepDel15, CRSArrTime, ArrDelay, ArrDel15, geannuleerd</li></ul>
</td>
</tr>

<tr>
  <td valign=top>Vlucht over tijdige prestaties (Raw)</td>
  <td valign=top>
Records van het vliegtuig vlucht ontvangsten en afwijkingen in de Verenigde Staten van oktober 2011.<p> </p><b>Gebruik:</b> vertragingen te voorspellen. <p> </p><b>Verwante Research:</b> van VS afdeling transport <a href="http://www.transtats.bts.gov/DL_SelectFields.asp?Table_ID=236&DB_Short_Name=On-Time">http://www.transtats.bts.gov/DL_SelectFields.asp?Table_ID=236&DB_Short_Name=On-Time</a>.
  </td>
</tr>

<tr>
  <td valign=top>Bosbrandgegevens</td>
  <td valign=top>
Bevat de weergegevens, zoals temperatuur en vochtigheid indexen en o-snelheid van een gebied van noordoosten van Portugal, gecombineerd met records van bosbranden.<p> </p><b>Gebruik:</b> dit is een taak moeilijk regressie waarbij Hallo doel toopredict Hallo gebrand gebied van bosbranden. <p> </p><b>Verwante Research:</b> Cortez, P., & Morais, A. (2008). UCI Machine Learning-opslagplaats <a href="http://archive.ics.uci.edu/ml">http://archive.ics.uci.edu/ml</a>. Irvine, CA: Universiteit van Californië, School van gegevens en Computer wetenschappelijke <p> </p>[Cortez en Morais, 2007] P. Cortez en A. Morais. Een datamining benadering tooPredict bosbranden met behulp van meteorologische gegevens. In J. Neves, Dhr F. Hallo 13 EPIA 2007 - Portugees conferentie op kunstmatige intelligentie, December, Guimarães, Portugal p. 512-523, 2007 Santos en J. Machado Eds., nieuwe Trends in kunstmatige intelligentie, procedures. APPIA, ISBN 13 978-989-95618-0-9. Beschikbaar op: <a href="http://www.dsi.uminho.pt/~pcortez/fires.pdf">http://www.dsi.uminho.pt/~pcortez/fires.pdf</a>.
  </td>
</tr>

<tr ID=german-credit-card-uci-dataset>
  <td valign=top>Duits creditcard UCI gegevensset</td>
  <td valign=top>
Hallo UCI Statlog Duits creditcard gegevensset (<a href="http://archive.ics.uci.edu/ml/datasets/Statlog+(German+Credit+Data)">Statlog + Duits + tegoed + gegevens</a>), met behulp van Hallo german.data bestand.<p> </p>Hallo gegevensset classificeert personen, beschreven door een set kenmerken als lage of hoge kredietrisico's. Elk voorbeeld vertegenwoordigt een persoon. Er zijn functies van 20, numerieke en categorische, en een binaire label (Hallo tegoed risico waarde). Hoge tegoed risico vermeldingen label hebben = 2, lage tegoed risico vermeldingen label hebben = 1. Hallo kosten van een voorbeeld van een laag risico zo hoog onjuiste is 1, dat het Hallo-kosten van het onjuiste een voorbeeld van een hoog risico zo klein is 5.
  </td>
</tr>

<tr ID=imdb-movie-titles>
  <td valign=top>IMDB Filmtitels</td>
  <td valign=top>
Hallo gegevensset bevat informatie over films die zijn geclassificeerd in Twitter tweets: IMDB film-ID, naam film genre en productie jaar. Er zijn 17K films in Hallo gegevensset. Hallo dataset is geïntroduceerd in Hallo papier 'S. Dooms, T. De Pessemier en L. Martens. MovieTweetings: een classificatie van gegevensset film verzameld van Twitter. Workshop over Crowdsourcing en menselijke berekeningen voor Recommender systemen, CrowdRec op RecSys 2013."
  </td>
</tr>

<tr>
  <td valign=top>IRIS twee klassegegevens</td>
  <td valign=top>
Dit is mogelijk Hallo best bekende database toobe gevonden in de documentatie over Hallo patroon herkenning. Hallo dataset is relatief klein, met 50 voorbeelden van Bloemblad metingen van drie iris die.<p> </p><b>Gebruik:</b> voorspellen Hallo iris type uit Hallo metingen.  <p> </p><b>Verwante Research:</b> Fisher, R.A. (1988). UCI Machine Learning-opslagplaats <a href="http://archive.ics.uci.edu/ml">http://archive.ics.uci.edu/ml</a>. Irvine, CA: Universiteit van Californië, School van gegevens en Computer wetenschappelijke </td>
</tr>

<tr ID=movie-tweets>
  <td valign=top>Film Tweets</td>
  <td valign=top>
Hallo gegevensset is een uitgebreide versie van Hallo film Tweetings dataset. Hallo gegevensset heeft 170K classificaties voor films, opgehaald uit gestructureerde tweets op Twitter. Elk exemplaar vertegenwoordigt een tweet en is een tuple: gebruikersnaam, IMDB film-ID, classificatie, timestamp, aantal favorieten voor deze tweet en aantal retweets van deze tweet. Hallo dataset is beschikbaar gesteld door A. gezegd, S. Dooms, B. Loni en D. Tikk voor Recommender systemen uitdaging 2014.
  </td>
</tr>

<tr>
  <td valign=top>MPG-gegevens voor verschillende auto 's</td>
  <td valign=top>
Deze gegevensset is een enigszins gewijzigde versie van geleverd door Hallo StatLib bibliotheek van Carnegie Mellon universiteit Hallo-gegevensset. Hallo-gegevensset wordt gebruikt in Hallo 1983 American statistische koppeling handboek.<p> </p>Hallo gegevens toont brandstofverbruik voor verschillende auto's in mijl per gallon, samen met informatie dergelijke Hallo aantal cilinders, engine verplaatsing, paardenkracht, totale gewicht en versnelling.<p> </p><b>Gebruik:</b> voorspellen brandstofverbruik op basis van 3 met meerdere waarden discrete kenmerken en 5 doorlopende kenmerken. <p> </p><b>Verwante Research:</b> StatLib Carnegie Mellon universiteit, (1993). UCI Machine Learning-opslagplaats <a href="http://archive.ics.uci.edu/ml">http://archive.ics.uci.edu/ml</a>. Irvine, CA: Universiteit van Californië, School van gegevens en Computer wetenschappelijke </td>
</tr>

<tr>
  <td valign=top>Pima Indianen Diabetes binaire classificatie gegevensset</td>
  <td valign=top>
Een subset van gegevens uit de database National Institute Diabetes en spijsverteringskanaal en nier toegekend Hallo. Hallo dataset is gefilterde toofocus op vrouwelijke patiënten van Pima Indiase erfgoed. Hallo gegevens omvatten medische gegevens zoals glucose en of niveaus, evenals lifestyle factoren.<p> </p><b>Gebruik:</b> voorspellen of Hallo onderwerp diabetes (binaire classificatie) heeft. <p> </p><b>Verwante Research:</b> Sigillito, V. (1990). UCI Machine Learning-opslagplaats <a href="http://archive.ics.uci.edu/ml">http://archive.ics.uci.edu/ml '</a>. Irvine, CA: Universiteit van Californië, School van gegevens en Computer wetenschappelijke </td>
</tr>

<tr>
  <td valign=top>Klantgegevens restaurant</td>
  <td valign=top>
Een set van metagegevens over klanten, waaronder demografische gegevens en voorkeuren.<p> </p><b>Gebruik:</b> gebruik van deze gegevensset, Hallo in combinatie met de andere twee restaurant gegevenssets tootrain en testen van een systeem recommender. <p> </p><b>Verwante Research:</b> Bache, K. en Lichman, M. (2013). UCI Machine Learning-opslagplaats <a href="http://archive.ics.uci.edu/ml">http://archive.ics.uci.edu/ml</a>. Irvine, CA: Universiteit van Californië, School van gegevens en wetenschappelijke van de Computer.
  </td>
</tr>

<tr>
  <td valign=top>Gegevens van de functie restaurant</td>
  <td valign=top>
Een set van metagegevens over restaurant en hun functies, zoals voeding, consumentenscenario-stijl, en locatie.<p> </p><b>Gebruik:</b> gebruik van deze gegevensset, Hallo in combinatie met de andere twee restaurant gegevenssets tootrain en testen van een systeem recommender. <p> </p><b>Verwante Research:</b> Bache, K. en Lichman, M. (2013). UCI Machine Learning-opslagplaats <a href="http://archive.ics.uci.edu/ml">http://archive.ics.uci.edu/ml</a>. Irvine, CA: Universiteit van Californië, School van gegevens en wetenschappelijke van de Computer.
  </td>
</tr>

<tr>
  <td valign=top>Restaurant classificaties</td>
  <td valign=top>
De classificaties die door gebruikers toorestaurants op een schaal van 0 too2 bevat.<p> </p><b>Gebruik:</b> gebruik van deze gegevensset, Hallo in combinatie met de andere twee restaurant gegevenssets tootrain en testen van een systeem recommender. <p> </p><b>Verwante Research:</b> Bache, K. en Lichman, M. (2013). UCI Machine Learning-opslagplaats <a href="http://archive.ics.uci.edu/ml">http://archive.ics.uci.edu/ml</a>. Irvine, CA: Universiteit van Californië, School van gegevens en wetenschappelijke van de Computer.
  </td>
</tr>

<tr>
  <td valign=top>Stalen Annealing meerdere klasse-gegevensset</td>
  <td valign=top>
Deze gegevensset bevat een reeks van records uit staal aanhechten proefversies met fysieke kenmerken van hello (breedte, dikte, type (gesloten, blad, etc.) van het resulterende Hallo stalen typen.<p> </p><b>Gebruik:</b> een van twee numerieke klassenkenmerken; hardheid of sterkte te voorspellen. U kunt ook correlaties tussen kenmerken analyseren.<p> </p>Staalsoorten Volg een standaard set gedefinieerd door SAE en andere organisaties. U zoekt naar een specifieke 'hoogwaardige' (Hallo klassenvariabele) en u wilt toounderstand Hallo waarden die nodig zijn. <p> </p><b>Verwante Research:</b> pond, D. & Buntine, W. (NA). UCI Machine Learning-opslagplaats <a href="http://archive.ics.uci.edu/ml">http://archive.ics.uci.edu/ml</a>. Irvine, CA: Universiteit van Californië, School van gegevens en Computer wetenschappelijke <p> </p>Een handig handleiding toosteel cijfers vindt u hier: <a href="http://www.outokumpu.com/SiteCollectionDocuments/Outokumpu-steel-grades-properties-global-standards.pdf">http://www.outokumpu.com/SiteCollectionDocuments/Outokumpu-steel-grades-properties-global-standards.pdf</a>
  </td>
</tr>

<tr>
  <td valign=top>Telescoop gegevens</td>
  <td valign=top>
Records van hoge energie gamma partikel bursts samen met achtergrondruis, zowel in de simulatie via een Monte Carlo-proces.<p> </p>Hallo bedoeling van Hallo simulatie is tooimprove Hallo nauwkeurig op basis van een compleet de Cherenkov gamma kijkers, met behulp van statistische methoden toodifferentiate tussen Hallo gewenste signaal (Cherenkov straling douches) en achtergrondruis (hadronic douches gestart door cosmic stralen in in de lucht hoofdletters Hallo).<p> </p>Hallo gegevens zijn vooraf verwerkte toocreate-cluster met een lang Hallo lange as is gericht op Hallo camera center. Hallo parameters kunnen worden gebruikt voor onderscheid zijn Hallo kenmerken van deze knop met weglatingstekens (vaak Hillas parameters genoemd).<p> </p><b>Gebruik:</b> voorspellen of afbeelding van Welkom signaal of achtergrond ruis vertegenwoordigt.<p> </p><b>Opmerkingen:</b> nauwkeurigheid van de eenvoudige indeling is niet relevant zijn voor deze gegevens sinds het classificeren van een gebeurtenis achtergrond zoals signaal hoger is dan het classificeren van een signaalgebeurtenis achtergrond. Voor vergelijking van verschillende classificaties moet Hallo ROC grafiek worden gebruikt. Hallo kans op een gebeurtenis achtergrond accepteren als signaal moet hieronder een Hallo drempelwaarden te volgen: 0,01, 0,02, 0,05, 0,1 of 0,2.<p> </p>Merk ook op dat wordt Hallo achtergrond gebeurtenissen (voor hadronic douches h) aantal onderschat, terwijl in echte metingen Hallo h of ruis klasse Hallo meerderheid van gebeurtenissen staat. <p> </p><b>Verwante Research:</b> Bock, R.K. (1995). UCI Machine Learning-opslagplaats <a href="http://archive.ics.uci.edu/ml">http://archive.ics.uci.edu/ml</a>. Irvine, CA: Universiteit van Californië, School van gegevens </td>
</tr>

<tr ID=weather-dataset>
  <td valign=top>Dataset weer</td>
  <td valign=top>
Elk uur weer grond metingen uit NOAA (<a href="http://cdo.ncdc.noaa.gov/qclcd_ascii/, merged data from 201304 too201310">samenvoegen van gegevens van 201304 too201310</a>).<p> </p>Hallo weergegevens worden behandeld opmerkingen die door de luchthaven weer stations, die betrekking hebben op Hallo periode April oktober 2013. Voordat u uploadt tooAzure Machine Learning Studio, is als volgt Hallo gegevensset verwerkt:<ul><li>Station weer-id's zijn toegewezen toocorresponding luchthaven id 's</li><li>Weer stations die niet zijn gekoppeld aan Hallo 70 drukste luchthavens zijn gefilterd.</li><li>Hallo datumkolom is opgesplitst in afzonderlijke jaar, maand en dag kolommen</li><li>Hallo volgende kolommen zijn geselecteerd: AirportID, jaar, maand, dag, tijd, tijdzone, SkyCondition, zichtbaarheid, WeatherType, DryBulbFarenheit, DryBulbCelsius, WetBulbFarenheit, WetBulbCelsius, DewPointFarenheit, DewPointCelsius, RelativeHumidity, Windsnelheid, WindDirection, ValueForWindCharacter, StationPressure, PressureTendency, PressureChange, SeaLevelPressure, RecordType, HourlyPrecip, Altimeter</li></ul>
  </td>
</tr>

<tr ID=wikipedia-sp-500-dataset>
  <td valign=top>Wikipedia SP 500 gegevensset</td>
  <td valign=top>
Gegevens is afgeleid van Wikipedia (Engelstalig) (<a href="http://www.wikipedia.org/">http://www.wikipedia.org/</a>) op basis van de artikelen van elk bedrijf S & P 500 opgeslagen als XML-gegevens.<p> </p>Voordat u uploadt tooAzure Machine Learning Studio, is als volgt Hallo gegevensset verwerkt:<ul><li>Uitpakken van tekstinhoud voor elke specifieke bedrijf</li><li>Wiki opmaak verwijderen</li><li>Verwijder de niet-alfanumerieke tekens</li><li>Alle tekst toolowercase converteren</li><li>Bekende bedrijf categorieën zijn toegevoegd</li></ul><p> </p>Houd er rekening mee dat voor sommige bedrijven een artikel kan niet worden gevonden, zodat het aantal records Hallo minder dan 500.
  </td>
</tr>





<tr ID=direct-marketing>
  <td valign=top><a href="https://azuremlsampleexperiments.blob.core.windows.net/datasets/direct_marketing.csv">direct_marketing.csv</a></td>
  <td valign=top>
Hallo gegevensset bevat gegevens van de klant en aanwijzingen over hun antwoord tooa direct postadres campagne. Elke rij vertegenwoordigt een klant. Hallo gegevensset bevat 9 functies over gebruiker demografische gegevens en gedrag en 3 label kolommen uit het verleden (bezoekt, conversie en hoeven te besteden aan).  Bezoek is een binaire kolom die aangeeft dat een klant nadat hello marketingcampagne conversie duidt iets in een klant hebt aangeschaft, en hoeven te besteden aan bezocht Hallo hoeveelheid die is besteed.  Hallo dataset is beschikbaar gesteld door Kevin Hillstrom voor MineThatData e-Analytics en Data Mining uitdaging.
  </td>
</tr>

<tr ID=lyrl2004-tokens-test>
  <td valign=top><a href="https://azuremlsampleexperiments.blob.core.windows.net/datasets/lyrl2004_tokens_test.csv">lyrl2004_tokens_test.csv</a></td>
  <td valign=top>
Functies van de test-voorbeelden in Hallo RCV1 V2 Reuters nieuws gegevensset. Hallo dataset bevat 781K nieuwsartikelen samen met de id's (eerste kolom van Hallo gegevensset). Elk artikel is tokenized, stopworded, en voort. Hallo dataset is door David beschikbaar gesteld. D. Leistra.
  </td>
</tr>

<tr ID=lyrl2004-tokens-train>
  <td valign=top><a href="https://azuremlsampleexperiments.blob.core.windows.net/datasets/lyrl2004_tokens_train.csv">lyrl2004_tokens_train.csv</a></td>
  <td valign=top>
Functies van training voorbeelden in Hallo RCV1 V2 Reuters nieuws gegevensset. Hallo dataset bevat 23K nieuwsartikelen samen met de id's (eerste kolom van Hallo gegevensset). Elk artikel is tokenized, stopworded, en voort. Hallo dataset is door David beschikbaar gesteld. D. Leistra.
  </td>
</tr>

<tr ID=intrusion-detection>
  <td valign=top><a href="https://azuremlsampleexperiments.blob.core.windows.net/datasets/network_intrusion_detection.csv">network_intrusion_detection.csv</a><br></td>
  <td valign=top>
DataSet van Hallo KDD kop 1999 kennis detectie en Data Mining extra concurrentie (<a href="http://kdd.ics.uci.edu/databases/kddcup99/kddcup99.html">kddcup99.html</a>).<p> </p>Hallo dataset is gedownload en opgeslagen in Azure Blob storage (<a href="https://azuremlsampleexperiments.blob.core.windows.net/datasets/network_intrusion_detection.csv">network_intrusion_detection.csv</a>) en omvat zowel trainings- en testdoeleinden gegevenssets. Hallo training gegevensset heeft ongeveer 126K rijen en 43 kolommen, inclusief Hallo labels. Drie kolommen deel uitmaken van de labelgegevens Hallo en 40 kolommen, die bestaan uit numerieke en tekenreeks/categorische-functies zijn beschikbaar voor het Hallo-model te trainen. Hallo testgegevens heeft ongeveer 22,5 K voorbeelden met dezelfde 43 Hallo kolommen als in de trainingsgegevens Hallo testen.

  </td>
</tr>

<tr ID=rcv1-v2-topics-qrels>
  <td valign=top><a href="https://azuremlsampleexperiments.blob.core.windows.net/datasets/rcv1-v2.topics.qrels.csv">rcv1 v2.topics.qrels.csv</a></td>
  <td valign=top>
Onderwerp-toewijzingen voor nieuwsartikelen in Hallo RCV1 V2 Reuters nieuws gegevensset. Een nieuwsbericht worden tooseveral onderwerpen toegewezen. Hallo-indeling van elke rij is '&lt;onderwerpnaam&gt; &lt;document-id&gt; 1". Hallo gegevensset bevat 2.6M onderwerp toewijzingen. Hallo dataset is door David beschikbaar gesteld. D. Leistra.
  </td>
</tr>

<tr ID=student-performance>
  <td valign=top><a href="https://azuremlsampleexperiments.blob.core.windows.net/datasets/student_performance.txt">student_performance.txt</a></td>
  <td valign=top>
Deze gegevens zijn afkomstig van Hallo KDD kop 2010 studenten prestaties evaluatie challenge (<a href="http://www.kdd.org/kdd-cup-2010-student-performance-evaluation">studenten prestatieanalyse</a>). Hallo gebruikt is Hallo Algebra_2008_2009 trainingset (Stamper, J., Niculescu-Mizil, A., Ritter, S., drempel, G.J. & Koedinger, K.R. (2010). Wiskundige ik 2008-2009. Uitdaging gegevensset van KDD kop 2010 educatieve Data Mining uitdaging. Zoeken op het <a href="http://pslcdatashop.web.cmu.edu/KDDCup/downloads.jsp">downloads.jsp</a> of <a href="http://www.kdd.org/sites/default/files/kddcup/site/2010/files/algebra_2008_2009.zip">algebra_2008_2009.zip</a>.<p> </p>Hallo dataset is gedownload en opgeslagen in Azure Blob storage (<a href="https://azuremlsampleexperiments.blob.core.windows.net/datasets/student_performance.txt">student_performance.txt</a>) en logboekbestanden van een student Bijles system bevat. Hallo opgegeven functies omvatten probleem-ID en de korte beschrijving, student-ID, timestamp, en hoeveel probeert Hallo studenten vóór het oplossen van Hallo probleem in Hallo rechtermuisknop manier. de oorspronkelijke gegevensset Hallo heeft 8,9 M records. Deze gegevensset is de eerste 100K rijen omlaag actieve toohello. Hallo gegevensset heeft 23 door tabs gescheiden kolommen van verschillende typen: numerieke categorische, en een tijdstempel.

  </td>
</tr>




</table>


<!-- Module References -->
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/

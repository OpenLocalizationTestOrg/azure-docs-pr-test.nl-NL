---
title: aaaCustom velden in Log Analytics | Microsoft Docs
description: Hallo aangepaste velden functie van Log Analytics kunt u toocreate uw eigen doorzoekbare velden OMS-gegevens die toohello eigenschappen van een verzamelde record toevoegen.  In dit artikel beschrijft Hallo proces toocreate een aangepast veld en een gedetailleerd overzicht biedt een voorbeeld van de gebeurtenis.
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: 31572b51-6b57-4945-8208-ecfc3b5304fc
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/18/2016
ms.author: bwren
ms.openlocfilehash: 1aa0e497d5b1d7898b0da6a5ef40f568e63bc589
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="custom-fields-in-log-analytics"></a>Aangepaste velden in Log Analytics
Hallo **aangepaste velden** functie van Log Analytics kunt u bestaande records in de OMS-opslagplaats Hallo tooextend door uw eigen doorzoekbare velden toe te voegen.  Aangepaste velden worden automatisch ingevuld uit gegevens die zijn opgehaald uit de andere eigenschappen in Hallo dezelfde record.

![Overzicht van aangepaste velden](media/log-analytics-custom-fields/overview.png)

Voorbeeldrecord hello onderstaande heeft bijvoorbeeld nuttige gegevens in de gebeurtenisbeschrijving Hallo overspoeld.  Deze gegevens in te pakken op afzonderlijke eigenschappen, wordt het beschikbaar gemaakt voor deze acties als sorteren en filteren.

![Meld u knop Zoeken](media/log-analytics-custom-fields/sample-extract.png)

> [!NOTE]
> Hallo Preview bent u beperkt too100 aangepaste velden in uw werkruimte.  Deze limiet zal worden uitgebreid wanneer deze functie algemeen beschikbaar is bereikt.
> 
> 

## <a name="creating-a-custom-field"></a>Maken van een aangepast veld
Wanneer u een aangepast veld maakt, moet logboekanalyse begrijpen welke gegevens toouse toopopulate de waarde ervan.  Dit maakt gebruik van een technologie van Microsoft Research FlashExtract aangeroepen tooquickly deze gegevens identificeren.  In plaats van dat u expliciete instructies tooprovide logboekanalyse leert over Hallo gegevens u tooextract van voorbeelden die u opgeeft.

Hallo volgende secties bieden Hallo procedure voor het maken van een aangepast veld.  Hallo is onder aan dit artikel een overzicht van de extractie van een steekproef.

> [!NOTE]
> Hallo aangepaste veld wordt ingevuld als records overeenkomende Hallo criteria toohello OMS-gegevensarchief opgegeven, zijn toegevoegd, zodat er alleen op records verzameld nadat Hallo aangepast veld is gemaakt.  Hallo aangepast veld wordt niet toegevoegd toorecords die zich al in het gegevensarchief Hallo wanneer deze wordt gemaakt.
> 
> 

### <a name="step-1--identify-records-that-will-have-hello-custom-field"></a>Stap 1: records identificeren waarvoor Hallo aangepast veld
de eerste stap Hallo is tooidentify Hallo records die Hallo aangepast veld krijgt.  U kunt beginnen met een [standaard logboek zoeken](log-analytics-log-searches.md) en selecteer vervolgens een record tooact als Hallo model dat Log Analytics leert uit.  Wanneer u opgeeft dat u tooextract gegevens in een aangepast veld gaat, Hallo **veld extractie Wizard** is geopend, waarin u valideren en Verfijn Hallo criteria.

1. Ga te**logboek zoeken** en gebruiken een [tooretrieve Hallo records query](log-analytics-log-searches.md) waarvoor Hallo aangepast veld.
2. Selecteer een record dat Log Analytics tooact wordt gebruikt als een model voor het extraheren van gegevens toopopulate Hallo aangepast veld.  U geeft Hallo gegevens dat u wilt dat tooextract van deze record en Log Analytics deze informatie toodetermine Hallo logica toopopulate Hallo aangepast veld voor alle soortgelijke records gebruikt.
3. Klik op Hallo knop toohello links van elke eigenschap text van Hallo opnemen en selecteer **velden uit te pakken**.
4. Hallo **veld extractie Wizard wordt geopend**, en Hallo-record die u hebt geselecteerd worden weergegeven in Hallo **Main voorbeeld** kolom.  Hallo aangepast veld worden gedefinieerd voor de records met Hallo dezelfde waarden in Hallo-eigenschappen die zijn geselecteerd.  
5. Als Hallo selectie niet precies wat u wilt is, kunt u aanvullende velden toonarrow Hallo criteria selecteren.  Volgorde toochange Hallo veld waarden voor Hallo criteria, moet u annuleren en selecteer een andere record die overeenkomt met de gewenste Hallo criteria.

### <a name="step-2---perform-initial-extract"></a>Stap 2: initiële extract uitvoeren.
Zodra u hebt bepaald Hallo-records die Hallo aangepast veld hebben, kunt u Hallo-gegevens die u wilt dat tooextract identificeren.  Log Analytics gebruikt deze informatie tooidentify vergelijkbare patronen in soortgelijke records.  In stap Hallo na deze u kan toovalidate Hallo resultaten en verdere informatie opgeven voor logboekanalyse toouse in de analyse.

1. Markeer de tekst hello in Hallo voorbeeldrecord die u wilt dat toopopulate Hallo aangepast veld.  Vervolgens worden weergegeven met een tooprovide dialoogvenster-vak een naam op voor Hallo veld en tooperform Hallo initiële uitpakken.  Hallo tekens  **\_CF** automatisch worden toegevoegd.
2. Klik op **extraheren** tooperform een analyse van verzamelde records.  
3. Hallo **samenvatting** en **zoekresultaten** secties worden weergegeven, Hallo resultaten van Hallo extract zodat u kunt de nauwkeurigheid inspecteren.  **Samenvatting** Hallo criteria gebruikt tooidentify records en een telling weergegeven voor elke Hallo gegevenswaarden geïdentificeerd.  **Zoekresultaten** biedt een gedetailleerde lijst met records die Hallo criteria voldoen.

### <a name="step-3--verify-accuracy-of-hello-extract-and-create-custom-field"></a>Stap 3: Controleer de juistheid van Hallo extract en aangepast veld maken
Zodra u de initiële extract Hallo hebt uitgevoerd, weergegeven logboekanalyse de resultaten op basis van gegevens die al is verzameld.  Als het Hallo-resultaten zien er nauwkeurige kunt u de Hallo aangepast veld met niets verdere zakelijk maken.  Als dat niet het geval is, klikt u vervolgens kunt u resultaten Hallo verfijnen zodat logboekanalyse de logica kunnen verbeteren.

1. Als alle waarden in de initiële extract Hallo niet juist zijn, klikt u op Hallo **bewerken** pictogram volgende tooan onnauwkeurig record en selecteer **wijzigen van deze markering** in volgorde toomodify Hallo selectie.
2. Hallo vermelding is gekopieerde toohello **aanvullende voorbeelden gegeven** sectie onder Hallo **Main voorbeeld**.  U kunt aanpassen Hallo markeren hier toohelp Log Analytics begrijpen Hallo selectie moet hebt aangebracht.
3. Klik op **extraheren** toouse deze nieuwe informatie tooevaluate alle bestaande Hallo registreert.  Hallo-resultaten kunnen worden gewijzigd voor records dan Hallo een die zojuist gewijzigde op basis van deze nieuwe bedrijfsinformatie.
4. Blijven tooadd correcties totdat alle records in Hallo correct extraheren identificeren Hallo gegevens toopopulate Hallo nieuw aangepast veld.
5. Klik op **opslaan extraheren** wanneer u tevreden bent met Hallo resultaten.  Hallo aangepast veld is nu gedefinieerd, maar dit zal niet worden toegevoegd tooany records nog.
6. Wachten op nieuwe records overeenkomende Hallo opgegeven criteria toobe verzameld en Voer Hallo logboek zoeken opnieuw. Nieuwe records Hallo aangepast veld aanwezig zijn.
7. Gebruik aangepaste veld Hallo zoals andere record, eigenschap.  U kunt gebruiken deze tooaggregate-en groepsgegevens en gebruik zelfs tooproduce inzichten.

## <a name="viewing-custom-fields"></a>Aangepaste velden weergeven
U kunt een lijst van alle aangepaste velden weergeven in uw beheergroep vanuit Hallo **instellingen** tegel van Hallo OMS-dashboard.  Selecteer **gegevens** en vervolgens **aangepaste velden** voor een lijst met alle aangepaste velden in uw werkruimte.  

![Aangepaste velden](media/log-analytics-custom-fields/list.png)

## <a name="removing-a-custom-field"></a>Een aangepast veld verwijderen
Er zijn twee manieren tooremove een aangepast veld.  Hallo wordt eerst Hallo **verwijderen** optie voor elk veld wanneer u bekijkt hello volledige lijst zoals hierboven is beschreven.  Hallo is andere methode tooretrieve die een record en klik op Hallo knop toohello links van het Hallo-veld.  Hallo menu hebben een optie tooremove Hallo aangepast veld.

## <a name="sample-walkthrough"></a>Voorbeeld-overzicht
Hallo volgende sectie wordt uitgelegd een compleet voorbeeld van het maken van een aangepast veld.  In dit voorbeeld extraheert Hallo de naam van de service in Windows-gebeurtenissen die duiden op een service de status wordt gewijzigd.  Dit is afhankelijk van gebeurtenissen die zijn gemaakt door de Service Control Manager in het systeemlogboek Hallo op Windows-computers.  Als u wilt dat toofollow in dit voorbeeld, moet u [verzamelen van gebeurtenissen voor het systeemlogboek Hallo](log-analytics-data-sources-windows-events.md).

We Voer Hallo query tooreturn na alle gebeurtenissen van Service Control Manager met een gebeurtenis-ID van 7036 die Hallo-gebeurtenis die aangeeft van een service starten of stoppen.

![Query’s uitvoeren](media/log-analytics-custom-fields/query.png)

We Selecteer vervolgens een record met gebeurtenis-ID 7036.

![Bronrecord](media/log-analytics-custom-fields/source-record.png)

We willen Hallo-servicenaam die wordt weergegeven in Hallo **RenderedDescription** en selecteer Hallo knop volgende toothis eigenschap.

![Haal velden](media/log-analytics-custom-fields/extract-fields.png)

Hallo **veld extractie Wizard** wordt geopend en Hallo **EventLog** en **EventID** velden zijn geselecteerd in Hallo **Main voorbeeld** kolom.  Hiermee wordt aangegeven dat aangepaste veld Hallo voor gebeurtenissen van Hallo systeemlogboek met een gebeurtenis-ID van 7036 worden gedefinieerd.  Dit is voldoende dus we er geen tooselect andere velden moeten.

![Voorbeeld van de belangrijkste](media/log-analytics-custom-fields/main-example.png)

We Markeer de Hallo-naam van de service Hallo in Hallo **RenderedDescription** eigenschap en gebruik **Service** tooidentify Hallo servicenaam.  Hallo aangepast veld moet worden aangeroepen **Service_CF**.

![De titel](media/log-analytics-custom-fields/field-title.png)

We zien dat die Hallo servicenaam correct wordt geïdentificeerd voor sommige records, maar niet voor andere gebruikers.   Hallo **zoekresultaten** weergeven dat deel van naam Hallo voor Hallo **WMI-prestatieadapter** is niet geselecteerd.  Hallo **samenvatting** blijkt dat vier records met **DPRMA** service onjuist opgenomen een extra word en twee records geïdentificeerd **Modules Installer** in plaats van **Windows Modules Installer**.  

![Zoekresultaten](media/log-analytics-custom-fields/search-results-01.png)

We beginnen met Hallo **WMI-prestatieadapter** record.  We klikt u op het bewerkingspictogram en vervolgens **wijzigen van deze markering**.  

![Markering wijzigen](media/log-analytics-custom-fields/modify-highlight.png)

We Hallo markeren tooinclude Hallo word verhogen **WMI** en Voer Hallo uitpakken.  

![Nog een voorbeeld](media/log-analytics-custom-fields/additional-example-01.png)

Zien we dat Hallo vermeldingen voor **WMI-prestatieadapter** zijn opgelost, en ook gebruikt die informatie toocorrect Hallo-records voor logboekanalyse **Windows Module Installer**.  We zien in Hallo **samenvatting** echter sectie **DPMRA** nog steeds niet wordt aangeduid correct.

![Zoekresultaten](media/log-analytics-custom-fields/search-results-02.png)

We Schuif tooa record met Hallo DPMRA-service en dezelfde toocorrect die record verwerken hello gebruiken.

![Nog een voorbeeld](media/log-analytics-custom-fields/additional-example-02.png)

 Wanneer we Hallo extractie uitvoert, zien we dat alle onze resultaten nu juist zijn.

![Zoekresultaten](media/log-analytics-custom-fields/search-results-03.png)

We zien die **Service_CF** is gemaakt, maar tooany records nog niet is toegevoegd.

![Oorspronkelijke aantal](media/log-analytics-custom-fields/initial-count.png)

Na enige tijd is verstreken, zodat nieuwe gebeurtenissen worden verzameld, zien we dat Hallo **Service_CF** veld is nu toegevoegd toorecords die overeenkomen met de criteria.

![Definitieve resultaten](media/log-analytics-custom-fields/final-results.png)

We kunnen nu aangepaste veld Hallo zoals een andere record-eigenschap gebruiken.  tooillustrate, maken we een query die door Hallo nieuwe groepen **Service_CF** veld tooinspect welke services Hallo meest actief zijn.

![Groeperen op query](media/log-analytics-custom-fields/query-group.png)

## <a name="next-steps"></a>Volgende stappen
* Meer informatie over [Meld zoekopdrachten](log-analytics-log-searches.md) toobuild query's op basis van aangepaste velden voor de criteria.
* Monitor [aangepaste logboekbestanden](log-analytics-data-sources-custom-logs.md) die u met behulp van aangepaste velden parseren.


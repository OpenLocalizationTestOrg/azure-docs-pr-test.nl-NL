---
title: Mobile Engagement iOS SDK-releaseopmerkingen aaaAzure | Microsoft Docs
description: Meest recente updates en procedures voor iOS SDK voor Azure Mobile Engagement
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: a43ff0f6-90d5-4b3c-8d7a-a1db21bc776b
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 07/17/2017
ms.author: piyushjo
ms.openlocfilehash: ae29d200ebb1784357b29edbd1f66b71df0778cd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-mobile-engagement-ios-sdk-release-notes"></a>Azure Mobile Engagement iOS SDK-releaseopmerkingen

## <a name="410-07172017"></a>4.1.0 (07/17/2017)
* Vaste badges uitgeschakeld op de achtergrond.
* Vaste waarschuwingen op 9 over API's niet aangeroepen in hoofdwachtrij XCode.
* Een geheugenlek vast Reach polls.
* Ondersteuning voor iOS verwijderd 6.X. Vanaf deze versie Hallo implementatiedoel van uw toepassing moet ten minste iOS 7.

## <a name="401-12132016"></a>4.0.1 (12/13/2016)
* Verbeterde levering van het logboek op de achtergrond.

## <a name="400-09122016"></a>4.0.0 (09/12/2016)
* Vaste melding niet worden ondernomen op iOS-10-apparaten.
* Afschaffen XCode 7.

## <a name="324-06302016"></a>3.2.4 (06/30/2016)
* Vaste aggregatie tussen technische logboeken en andere logboeken.

## <a name="323-06072016"></a>3.2.3 (06/07/2016)
* Vaste Hallo bug waar de leveringsfeedback is niet gemeld wanneer de app op de achtergrond Hallo.
* Voor optimale Hallo technische logboeken worden verzonden.

## <a name="322-04072016"></a>3.2.2 (04/07/2016)
* Vaste bug op HTTP-aanvraag annulering waarmee toocrash soms wordt geleid.

## <a name="321-12112015"></a>3.2.1 (12/11/2015)
* Vaste Hallo vertraging wanneer een nieuw app-exemplaar wordt geactiveerd door een melding met dieptekoppelingen

## <a name="320-10082015"></a>3.2.0 (10/08/2015)
* Bitcode ingeschakeld in Hallo SDK toomake werkt deze met **Xcode 7**.
* Opgeloste gerelateerd tooin-app-meldingen.
* Hallo-in-app-meldingen betrouwbaarder in geval van een laag energieniveau en andere dergelijke scenario's gemaakt.
* Extra console-logboeken die worden gegenereerd door 3e partij bibliotheek verwijderd.

## <a name="310-08262015"></a>3.1.0 (08/26/2015)
* Oplossingen voor iOS 9-compatibiliteit met een bibliotheek van derden oplossen. Het is crashes veroorzaakt tijdens het verzenden van resultaten, toepassingsinformatie of extra gegevens worden opgevraagd.

## <a name="300-06192015"></a>3.0.0 (06/19/2015)
* Mobile Engagement gebruikt achtergrond-Pushmeldingen.
* Ondersteuning voor iOS verwijderd 4.X. Vanaf deze versie Hallo implementatiedoel van uw toepassing moet ten minste iOS 6.

## <a name="220-05212015"></a>2.2.0 (05/21/2015)
* Hallo Mobile Engagement apparaat-id voor apparaten < iOS 6 is nu gebaseerd op een GUID die wordt gegenereerd tijdens de installatie.

## <a name="210-04242015"></a>2.1.0 (04/24/2015)
* Toegevoegde Swift compatibiliteit.
* Wanneer op een melding te klikken, uitgevoerd Hallo actie-URL nu is rechts nadat de toepassing hello wordt geopend.
* Toegevoegde ontbrekende headerbestand in de SDK-pakket.
* Een probleem opgelost wanneer Hallo Mobile Engagement crash Rapportagefout is uitgeschakeld.

## <a name="200-02172015"></a>2.0.0 (02/17/2015)
* Initiële versie van Azure Mobile Engagement
* appId/sdkKey configuratie wordt vervangen door de configuratie van een verbinding-tekenreeks.
* API-toosend verwijderd en willekeurige XMPP berichten ontvangen van willekeurige XMPP entiteiten.
* API-toosend verwijderd en kunnen berichten tussen apparaten ontvangen.
* Verbeterde beveiliging.
* SmartAd bijhouden verwijderd.

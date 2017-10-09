---
title: aaaAzure Mobile Engagement Android SDK-integratie
description: Meest recente updates en -procedures voor Android-SDK voor Azure Mobile Engagement
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 585341f9-3f39-459a-af42-864e400a0128
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 07/17/2017
ms.author: piyushjo
ms.openlocfilehash: 16b098198674c49567d720d0c01d984cb763ed8a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="release-notes"></a>Releaseopmerkingen

## <a name="431-07172017"></a>4.3.1 (07/17/2017)
* Herstel van een crash die zelden optreden kan bij het aanroepen van `EngagementAgentUtils.isInDedicatedEngagementProcess`, die ook wordt gebruikt door Hallo `EngagementApplication` klasse.

## <a name="430-06272017"></a>4.3.0 (06/27/2017)
* Android 8-ondersteuning (vorige versies van Hallo SDK niet in Android 8 werken).
* Er is geen meer afhankelijkheid van ondersteuningsbibliotheek.
* Verwijder `EngagementFragmentActivity` klasse.
* Vervaldatum te[achtergrond uitvoering limieten](https://developer.android.com/preview/features/background.html) op Android 8 logboeken op de achtergrond kunnen worden uitgesteld totdat Hallo gebruiker werkt met Hallo-apparaat, wordt dit een invloed hebben op campagne Push **geleverd** en **Systeemmelding weergegeven** statistieken als Hallo-apparaat is in de slaapstand wordt uitgesteld (Hallo melding nog wel weergegeven, wordt ring en Trillen in realtime zonder problemen).
* Vervaldatum te[achtergrond locatie limieten](https://developer.android.com/preview/features/background-location-limits.html), Hallo realtime locatie op de achtergrond wordt niet vaak op Android 8 worden bijgewerkt.

## <a name="424-03302017"></a>4.2.4 (03/30/2017)
* Herstel in-app-melding tekstkleuren op Android 7 toobe Hallo dezelfde als oudere versies van Android.

## <a name="423-08102016"></a>4.2.3 (08/10/2016)
* Er is geen meer Wi-Fi-vergrendeling.
* Herstel een impasse aangetroffen bij het aanroepen van getDeviceId voordat init (fout die is geïntroduceerd in 4.2.0).

## <a name="422-05172016"></a>4.2.2 (05/17/2016)
* Verbeteringen in stabiliteit.

## <a name="421-05102016"></a>4.2.1 (05/10/2016)
* Beveiliging: uitschakelen webtoegang weergave lokaal bestand.
* Beveiliging: Verwijder `EngagementPreferenceActivity` klasse die uitgebreider is verouderd en niet-beveiligde `PreferenceActivity` klasse.
* Beveiliging: reach activiteiten nu zijn gedocumenteerd toouse `exported="false"`, deze vlag kan ook worden gebruikt in eerdere versies van de SDK.

## <a name="420-03112016"></a>4.2.0 (03/11/2016)
* Hallo SDK is nu een licentie verleend onder MIT.
* Toestaan dat een aangepast apparaat-id opgeven bij het initialiseren SDK.

## <a name="415-02012016"></a>4.1.5 (02/01/2016)
* Verbeteringen in stabiliteit.

## <a name="414-01262016"></a>4.1.4 (01/26/2016)
* Verbeteringen in stabiliteit.

## <a name="413-1292015"></a>4.1.3 (12/9/2015)
* Verbeteringen in stabiliteit.

## <a name="412-11252015"></a>4.1.2 (11/25/2015)
* Verbeteringen in stabiliteit.

## <a name="411-11042015"></a>4.1.1 (11/04/2015)
* Verbeteringen in stabiliteit.

## <a name="410-08252015"></a>4.1.0 (08/25/2015)
* Nieuw model voor machtiging verwerken voor Android M.
* Kunnen nu functies configureren voor locatie tijdens runtime in plaats van `AndroidManifest.xml`.
* Een machtiging fout oplossen: als u `ACCESS_FINE_LOCATION`, klikt u vervolgens `ACCESS_COARSE_LOCATION` niet meer nodig is.
* Verbeteringen in stabiliteit.

## <a name="400-07062015"></a>4.0.0 (07/06/2015)
* Interne protocol wijzigingen toomake analyses en pushmeldingen betrouwbaarder.
* Native pushberichten (GCM/ADM) is nu ook gebruikt voor in de app-meldingen zodat u Hallo native pushreferenties voor elk type pushcampagne moet configureren.
* Grote afbeelding melding oplossen: ze zijn weergegeven alleen per 10 na wordt gepusht.
* Herstel van een fout in de webweergave: Hallo standaard actie-URL is ook uitvoeren op een koppeling te klikken.
* Los het vastlopen van een zeldzame gerelateerde toolocal opslagbeheer.
* Los de dynamische configuratie tekenreeks management.
* Bijwerken van de gebruiksrechtovereenkomst.

## <a name="300-02172015"></a>3.0.0 (02/17/2015)
* Initiële versie van Azure Mobile Engagement
* appId-configuratie wordt vervangen door de configuratie van een verbinding-tekenreeks.
* API-toosend verwijderd en willekeurige XMPP berichten ontvangen van willekeurige XMPP entiteiten.
* API-toosend verwijderd en kunnen berichten tussen apparaten ontvangen.
* Verbeterde beveiliging.
* Google Play en SmartAd bijhouden verwijderd.


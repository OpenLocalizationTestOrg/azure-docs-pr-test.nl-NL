---
title: Azure CDN-inhoud door land aaaRestrict | Microsoft Docs
description: Meer informatie over hoe toorestrict toegang tooyour Azure CDN inhoud met behulp van Hallo Geo-filters.
services: cdn
documentationcenter: 
author: lichard
manager: akucer
editor: 
ms.assetid: 12c17cc5-28ee-4b0b-ba22-2266be2e786a
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: rli
ms.openlocfilehash: ffdd994612b6c9cfbf1a6e29d260709b4afa86e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="restrict-azure-cdn-content-by-country"></a>Azure CDN-inhoud per land beperken

## <a name="overview"></a>Overzicht
Wanneer een gebruiker wordt uw inhoud standaard aanvraagt, wordt inhoud Hallo geleverd ongeacht waar Hallo gebruiker gemaakt voor deze aanvraag uit. In sommige gevallen kunt u toorestrict toegang tot tooyour inhoud per land. Dit onderwerp wordt uitgelegd hoe toouse hello **Geo filteren** functie in volgorde tooconfigure Hallo service tooallow of de toegang blokkeert per land.

> [!IMPORTANT]
> Hallo Verizon en Akamai producten bieden dezelfde functionaliteit geo filteren Hallo maar hebben een klein verschil in landcodes te ondersteunen. Zie stap 3 voor een koppeling toohello verschillen.


Dit type beperking, Zie voor informatie over overwegingen die van toepassing tooconfiguring hello [overwegingen](cdn-restrict-access-by-country.md#considerations) sectie achter Hallo Hallo onderwerp.  

![Landen filteren](./media/cdn-filtering/cdn-country-filtering-akamai.png)

## <a name="step-1-define-hello-directory-path"></a>Stap 1: Hallo mappad definiëren
Selecteer uw eindpunt binnen Hallo-portal en Hallo Geo filteren tabblad op Hallo linkermenubalk toofind deze functie vindt.

Wanneer u een filter land configureert, moet u Hallo relatief pad toohello locatie toowhich gebruikers wordt toegestaan of toegang geweigerd. U kunt filteren van geo toepassen voor alle bestanden met '/' of de geselecteerde mappen door te geven mappaden '/ afbeeldingen /'. U kunt ook tooa geo filteren enkel bestand toepassen Hallo-bestand opgeven en daarbij afsluitende slash Hallo ' / afbeeldingen/stad.PNG '.

Voorbeeld van de directory pad filter:

    /                                 
    /Photos/
    /Photos/Strasbourg/
      /Photos/Strasbourg/city.png

## <a name="step-2-define-hello-action-block-or-allow"></a>Stap 2: Definiëren Hallo actie: blokkeren of toestaan
**Blokkeren:** gebruikers van Hallo opgegeven landen toegang tooassets aangevraagd bij dat recursieve pad wordt geweigerd. Als er geen andere land-filteropties zijn geconfigureerd voor die locatie, klikt u vervolgens alle andere gebruikers mogen toegang.

**Toestaan:** alleen gebruikers van Hallo opgegeven landen toegang tooassets aangevraagd bij dat pad recursieve worden toegestaan.

## <a name="step-3-define-hello-countries"></a>Stap 3: Hallo landen definiëren
Selecteer Hallo landen die u tooblock wilt of toestaan voor Hallo-pad. 

Hallo-regel van het blokkeren van /Photos/Straatsburg/wordt bijvoorbeeld bestanden met inbegrip van filteren:

    http://<endpoint>.azureedge.net/Photos/Strasbourg/1000.jpg
    http://<endpoint>.azureedge.net/Photos/Strasbourg/Cathedral/1000.jpg


### <a name="country-codes"></a>Landcodes
Hallo **Geo filteren** functie land codes toodefine Hallo landen waarin een aanvraag wordt toegestaan of geblokkeerd voor een beveiligde map gebruikt. U ziet Hallo landcodes in [Azure CDN landcodes](https://msdn.microsoft.com/library/mt761717.aspx). 

## <a id="considerations"></a>Overwegingen
* Het kan too90 minuten voor Verizon of voor wijzigingen tooyour land filteren configuratie tootake effect met Akamai, een paar minuten duren.
* Deze functie biedt geen ondersteuning voor jokertekens (bijvoorbeeld ' *').
* Hallo geo filteren configuratie die is gekoppeld met het relatieve pad Hallo worden toegepaste recursief toothat pad.
* Slechts één regel kan worden toegepast toohello hetzelfde relatieve pad (u kunt geen meerdere land filters te maken dat punt toohello hetzelfde relatieve pad. Een map hebben echter meerdere land filters. Dit is vanwege toohello recursieve aard van de filters land. Een submap van een eerder geconfigureerde map kan met andere woorden, een ander land filter toegewezen.


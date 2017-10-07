---
title: aaaSecuring Azure CDN activa met tokenverificatie | Microsoft Docs
description: Met behulp van tokenverificatie toosecure toegang tooyour Azure CDN activa.
services: cdn
documentationcenter: .net
author: zhangmanling
manager: zhangmanling
editor: 
ms.assetid: 837018e3-03e6-4f9c-a23e-4b63d5707a64
ms.service: cdn
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 11/11/2016
ms.author: mezha
ms.openlocfilehash: 5865bcb8eed7ced834970d52d30136252039265f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="securing-azure-cdn-assets-with-token-authentication"></a>Azure CDN activa met tokenverificatie beveiligen

[!INCLUDE [cdn-premium-feature](../../includes/cdn-premium-feature.md)]

##<a name="overview"></a>Overzicht

Tokenverificatie is een mechanisme waarmee u tooprevent Azure CDN van voor de activa toounauthorized clients.  Dit gebeurt meestal tooprevent 'hotlinking' van inhoud, waarbij een andere website, vaak een mededelingenbord uw assets zonder toestemming gebruikt.  Dit kan een invloed hebben op de kosten voor het leveren van inhoud. Als u deze functie op CDN inschakelt, wordt door rand CDN POP's voor het leveren van inhoud Hallo aanvragen worden geverifieerd. 

## <a name="how-it-works"></a>Hoe werkt het?

Tokenverificatie controleert u of aanvragen worden gegenereerd door een vertrouwde site doordat aanvragen toocontain een token waarde gecodeerde dat informatie bevat over Hallo aanvrager. Inhoud kan alleen worden geleverd toorequester wanneer Hallo gegevens Hallo voldoen aan vereisten gecodeerde, worden anders aanvragen geweigerd. U kunt Hallo vereiste met behulp van een of meer parameters die hieronder instellen.

- Land: toestaan of weigeren van aanvragen die afkomstig van bepaalde landen zijn.  [Lijst met geldige landcodes.](https://msdn.microsoft.com/library/mt761717.aspx) 
- URL: alleen opgegeven asset of pad toorequest toestaan.  
- Host: toestaan of weigeren-aanvragen via de opgegeven hosts in de aanvraagheader Hallo.
- Verwijzende site: toestaan of weigeren opgegeven verwijzende toorequest.
- IP-adres: ervoor zorgen dat alleen aanvragen die afkomstig van specifieke IP-adres of IP-subnet zijn.
- Protocol: toestaan of blokkeren-aanvragen op basis van Hallo protocol toorequest Hallo inhoud gebruikt.
- Verlooptijd: toewijzen van een datum en tijd van de periode tooensure dat een koppeling alleen geldig voor een beperkte periode blijven.

Zie het voorbeeld van de gedetailleerde configuratie van elke parameter.

## <a name="reference-architecture"></a>Referentiearchitectuur

Zie hieronder een referentiearchitectuur voor het instellen van tokenverificatie op CDN toowork met uw Web-App.

![Knop blade CDN-profiel beheren](./media/cdn-token-auth/cdn-token-auth-workflow2.png)

## <a name="token-validation-logic-on-cdn-endpoint"></a>Token validatielogica op CDN-eindpunt
    
Dit diagram wordt beschreven hoe Azure CDN clientaanvraag valideert wanneer tokenverificatie is geconfigureerd op de CDN-eindpunt.

![Knop blade CDN-profiel beheren](./media/cdn-token-auth/cdn-token-auth-validation-logic.png)

## <a name="setting-up-token-authentication"></a>Token verificatie instellen

1. Van Hallo [Azure-portal](https://portal.azure.com)bladeren tooyour CDN-profiel en klik vervolgens op Hallo **beheren** knop toolaunch Hallo aanvullende portal.

    ![Knop blade CDN-profiel beheren](./media/cdn-rules-engine/cdn-manage-btn.png)

2. Beweeg de muisaanwijzer over **HTTP grote**, en klik vervolgens op **Token Auth** in Hallo doel. Stelt u de versleutelingssleutel en versleuteling parameters op dit tabblad.

    1. Voer een unieke coderingssleutel voor **primaire sleutel**.  Voer een andere voor **back-up-sleutel**

        ![CDN-setup van token verificatiesleutel](./media/cdn-token-auth/cdn-token-auth-setupkey.png)
    
    2. Versleuteling parameters met versleuteling hulpprogramma instellen (toestaan of weigeren van aanvragen op basis van de verlooptijd, land, verwijzende, protocol, client-IP. U kunt elke combinatie.)

        ![Knop blade CDN-profiel beheren](./media/cdn-token-auth/cdn-token-auth-encrypttool.png)

        - EC-verloopt: wijst een Vervaltijd van een token na een opgegeven periode. Aanvragen verzonden nadat Hallo vervaltijd worden geweigerd. Deze parameter gebruikt Unix tijdstempel (op basis van seconden sinds standaard epoche van 1/1/1970 00:00:00 GMT. U kunt extra online tooprovide conversie tussen stnd. tijd- en Unix-tijd.)  Bijvoorbeeld, als u tooset Hallo token toobe verlopen op 31-12-2016 12:00:00 GMT, Hallo Unix tijd: 1483185600 gebruiken zoals hieronder:
    
        ![Knop blade CDN-profiel beheren](./media/cdn-token-auth/cdn-token-auth-expire2.png)
    
        - EC url toestaan: Hiermee kunt u tootailor tokens tooa bepaald actief of het pad. Hiermee beperkt u de toegang toorequests waarvan de URL beginnen met een specifieke relatief pad. U kunt meerdere paden elk pad scheiden met komma's invoeren. URL's zijn hoofdlettergevoelig. Afhankelijk van de vereiste hello, kunt u andere waarde tooprovide ander niveau van toegang instellen. Hieronder vindt u een aantal scenario's:
        
            Als u een URL: http://www.mydomain.com/pictures/city/strasbourg.png. Zie invoerwaarde "" en de toegang dienovereenkomstig serviceniveau

            1. Invoerwaarde '/': alle aanvragen kunnen worden
            2. Invoerwaarde '/ afbeeldingen': alle Hallo aanvragen volgen krijgt
            
                - http://www.mydomain.com/Pictures.PNG
                - http://www.mydomain.com/Pictures/City/Strasbourg.PNG
                - http://www.mydomain.com/picturesnew/City/strasbourgh.PNG
            3. Waarde '/ afbeeldingen /' worden ingevoerd: alleen aanvragen voor /pictures/ wordt toegestaan
            4. Invoerwaarde ' / pictures/city/strasbourg.png ': kunt u alleen aanvragen voor dit activum
    
        ![Knop blade CDN-profiel beheren](./media/cdn-token-auth/cdn-token-auth-url-allow4.png)
    
        - EC land is toegestaan: kunt alleen aanvragen die afkomstig uit een of meer opgegeven landen zijn. Aanvragen die afkomstig van alle andere landen zijn worden geweigerd. Gebruik land code tooset up Hallo parameters en elke landcode scheiden met komma's. Als u toegang van de Verenigde Staten en Frankrijk tooallow wilt, invoer ons FR in Hallo kolom als hieronder.  
        
        ![Knop blade CDN-profiel beheren](./media/cdn-token-auth/cdn-token-auth-country-allow.png)

        - EC land weigeren: aanvragen die afkomstig zijn uit een of meer opgegeven landen. Aanvragen die afkomstig van alle andere landen zijn kunnen worden. Gebruik land code tooset up Hallo parameters en elke landcode scheiden met komma's. Als u toegang van de Verenigde Staten en Frankrijk toodeny wilt, invoer ons FR in Hallo-kolom.
    
        - EC ref toestaan: staat alleen aanvragen van de opgegeven verwijzende site. Een verwijzende identificeert Hallo-URL van webpagina Hallo die gekoppeld toohello bron wordt aangevraagd. Hallo verwijzende parameterwaarde mag niet Hallo protocol bevatten. U kunt een hostnaam en/of een bepaalde pad op dat hostnaam invoeren. U kunt ook meerdere verwijzende sites binnen een enkele parameter scheiden met komma's toevoegen. Als u een waarde van verwijzende site hebt opgegeven, maar Hallo verwijzende site-informatie niet in de aanvraag Hallo vanwege de configuratie van de browser toosome verzonden wordt, wordt standaard deze aanvragen worden geweigerd. U kunt toewijzen 'Ontbreekt' of een lege waarde in Hallo parameter tooallow deze aanvragen met ontbrekende verwijzende site-informatie. U kunt ook gebruiken ' *. consoto.com ' tooallow alle subdomeinen van consoto.com.  Bijvoorbeeld, als u toegang tooallow voor aanvragen van www.consoto.com, alle subdomeinen onder consoto2.com en erquests met reffers leeg is of ontbreekt wilt, invoerwaarde hieronder:
        
        ![Knop blade CDN-profiel beheren](./media/cdn-token-auth/cdn-token-auth-referrer-allow2.png)
    
        - EC ref weigeren: Hiermee worden aanvragen van de opgegeven verwijzende geweigerd. Voorbeeld van de parameter 'ec-ref-toestaan' en toodetails verwijzen.
         
        - EC protocol toestaan: kunt alleen aanvragen van het opgegeven protocol. Bijvoorbeeld, http of https.
        
        ![Knop blade CDN-profiel beheren](./media/cdn-token-auth/cdn-token-auth-url-allow4.png)
            
        - EC protocol weigeren: Hiermee worden aanvragen van het opgegeven protocol geweigerd. Bijvoorbeeld, http of https.
    
        - EC-client-IP: beperkt toegang toospecified aanvrager IP-adres. Zowel IPV4 als IPV6 worden ondersteund. U kunt één aanvraag IP-adres of IP-subnet opgeven.
            
        ![Knop blade CDN-profiel beheren](./media/cdn-token-auth/cdn-token-auth-clientip.png)
        
    3. U kunt uw token met Hallo decodering hulpprogramma testen.

    4. U kunt ook Hallo-type van het antwoord dat toouser moet worden geretourneerd wanneer de aanvraag is geweigerd. We gebruiken standaard 403.

3. Klik nu op **regelengine** tabblad onder **HTTP grote**. U wordt gebruik deze functie tabblad toodefine paden tooapply Hallo Hallo tokenverificatie functie inschakelen en inschakelen aanvullende tokenverificatie gerelateerde mogelijkheden.

    - Gebruik 'Als' kolom toodefine asset of het pad dat u wilt dat de tokenverificatie tooapply. 
    - Klik op 'Token Auth' tooadd van Hallo functie dropdown tooenable tokenverificatie.
        
    ![Knop blade CDN-profiel beheren](./media/cdn-token-auth/cdn-rules-engine-enable2.png)

4. In Hallo **regelengine** tabblad, zijn er enkele aanvullende functies die u kunt inschakelen.
    
    - Autorisatiecode DOS-token: bepaalt Hallo type antwoord dat wordt geretourneerd toouser wanneer een aanvraag wordt geweigerd. Hallo DOS-code instellingen Hallo token auth tabblad overschreven in de regels die u hier instelt.
    - Token auth negeren: Hiermee wordt bepaald of de URL die wordt gebruikt toovalidate token hoofdlettergevoelig wordt.
    - Token auth-parameter: Wijzig de naam van Hallo token auth query tekenreeksparameter met in Hallo aangevraagde URL. 
        
    ![Knop blade CDN-profiel beheren](./media/cdn-token-auth/cdn-rules-engine2.png)

5. Uw token dat is een toepassing die een token voor de verificatiefuncties op basis van tokens genereert, kunt u aanpassen. Broncode kan hier worden geopend in [GitHub](https://github.com/VerizonDigital/ectoken).
Beschikbare talen zijn onder andere:
    
    - C
    - C#
    - PHP
    - Perl
    - Java
    - Python    


## <a name="azure-cdn-features-and-provider-pricing"></a>Azure CDN-functies en prijzen-provider

Zie Hallo [overzicht van CDN](cdn-overview.md) onderwerp.

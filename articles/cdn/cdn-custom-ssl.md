---
title: aaa "HTTPS op een aangepaste Azure CDN-domein inschakelen | Microsoft Docs'
description: Meer informatie over hoe tooenable HTTPS op uw Azure CDN-eindpunt met een aangepast domein.
services: cdn
documentationcenter: 
author: camsoper
manager: erikre
editor: 
ms.assetid: 10337468-7015-4598-9586-0b66591d939b
ms.service: cdn
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/03/2017
ms.author: casoper
ms.openlocfilehash: 93746222616c9ed7977ec3b22c38ac1d43b118f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="enable-https-on-an-azure-cdn-custom-domain"></a>HTTPS op een aangepast domein van Azure CDN inschakelen

[!INCLUDE [cdn-verizon-only](../../includes/cdn-verizon-only.md)]

HTTPS-ondersteuning voor Azure CDN aangepaste domeinen kan toodeliver beveiligde inhoud met behulp van uw eigen domein naam tooimprove Hallo beveiliging van gegevens die onderweg SSL-beveiliging. Hallo end-to-end werkstroom tooenable HTTPS voor uw aangepaste domein wordt vereenvoudigd, via één klik inschakelen, complete certificaatbeheer en alle met zonder extra kosten.

Kritieke tooensure Hallo privacy en integriteit van gegevens van al uw web-toepassingen gevoelige gegevens die onderweg is. Met behulp van HTTPS-protocol zorgt ervoor dat uw vertrouwelijke gegevens worden versleuteld wanneer deze wordt verzonden via Hallo Hallo internet. Het biedt vertrouwt, verificatie en uw webtoepassingen worden beschermd tegen aanvallen. Op dit moment ondersteunt Azure CDN HTTPS op een CDN-eindpunt. Als u een CDN-eindpunt vanaf Azure CDN (bijvoorbeeld https://contoso.azureedge.net) maakt, wordt HTTPS bijvoorbeeld standaard ingeschakeld. Nu met het aangepaste domein HTTPS kunt u beveiligde levering voor een aangepast domein (bijvoorbeeld https://www.contoso.com) ook. 

Enkele belangrijke kenmerken van de functie HTTPS Hallo zijn:

- Kan zonder extra kosten: Er zijn geen kosten voor het verkrijgen van het certificaat of vernieuwen en zonder extra kosten voor HTTPS-verkeer. U betaalt alleen voor uitgaande van Hallo CDN GB.

- Eenvoudige activering: één klik inrichting is beschikbaar via Hallo [Azure-portal](https://portal.azure.com). U kunt ook de REST-API of andere onderdeel developer tools tooenable hello gebruiken.

- Voltooien van Certificaatbeheer: alle aanschaf van het certificaat en u wordt beheerd. Certificaten automatisch worden ingericht en eerdere tooexpiration vernieuwd. Hiermee verwijdert u volledig Hallo risico's van de service wordt onderbroken als gevolg van een certificaat verloopt.

>[!NOTE] 
>Eerdere tooenabling HTTPS ondersteunen, u moet al hebt vastgesteld een [aangepaste Azure CDN-domein](./cdn-map-content-to-custom-domain.md).

## <a name="step-1-enabling-hello-feature"></a>Stap 1: Het inschakelen van Hallo-functie 

1. In Hallo [Azure-portal](https://portal.azure.com), bladeren tooyour Verizon standard of premium CDN-profiel.

2. Klik op Hallo-eindpunt met uw aangepaste domein in Hallo lijst met eindpunten.

3. Klik op Hallo aangepast domein waarvoor u tooenable HTTPS wilt.

    ![De blade een eindpunt](./media/cdn-custom-ssl/cdn-custom-domain.png)

4. Klik op **op** tooenable HTTPS en Hallo wijziging op te slaan.

    ![Dialoogvenster voor aangepaste HTTPS](./media/cdn-custom-ssl/cdn-enable-custom-ssl.png)


## <a name="step-2-domain-validation"></a>Stap 2: Validatie van domein

>[!IMPORTANT] 
>U moet domeinvalidatie voltooien voordat HTTPS actief op uw aangepaste domein zijn. U hebt 6 business dagen tooapprove Hallo-domein. Aanvraag worden met geen goedkeuring binnen 6 werkdagen geannuleerd.  

Nadat HTTPS op uw aangepaste domein is ingeschakeld, valideert onze certificaatprovider HTTPS DigiCert eigendom van uw domein contact opnemen met de Hallo registrant voor uw domein, op basis van WHOIS registrant informatie via e-mail (standaard) of telefoon. DigiCert verzonden hello verificatie e toohello hieronder adressen ook. Als WHOIS registrant informatie persoonlijke, zorg er dan voor dat u rechtstreeks vanuit een van deze adressen kan goedkeuren.

>beheerder @ beheerder < uw-domain-name.com > @< uw-domain-name.com >  
>webbeheerder @< uw-domain-name.com >  
>hostmaster @< uw-domain-name.com >  
>postbeheerder @< uw-domain-name.com >


Bij ontvangst Hallo e-mail, hebt u twee opties voor verificatie:

1. U kunt alle toekomstige orders geplaatst via Hallo dezelfde account voor Hallo goedkeuren dezelfde hoofddomein, bijvoorbeeld consoto.com. Dit is een aanbevolen benadering als u van plan bent tooadd aanvullende aangepaste domeinen in toekomstige voor Hallo Hallo dezelfde hoofddomein.
 
2. U kunt alleen Hallo specifieke hostnaam die wordt gebruikt in deze aanvraag goedkeuren. Aanvullende goedkeuring is vereist voor de volgende aanvragen.

    Voorbeeld e-mailadres:
    
    ![Dialoogvenster voor aangepaste HTTPS](./media/cdn-custom-ssl/domain-validation-email-example.png)

Na goedkeuring, wordt DigiCert uw aangepaste domein naam toohello SAN-certificaat toevoegen. Hallo-certificaat wordt één jaar geldig zijn en wordt automatisch vernieuwd voordat deze is verlopen.

## <a name="step-3-wait-for-hello-propagation-then-start-using-your-feature"></a>Stap 3: Wachten op Hallo doorgeven en start met behulp van de functie

Nadat de domeinnaam Hallo is gevalideerd wordt het Hallo aangepast domein HTTPS functie toobe active too6 8 uur duren. Nadat het Hallo-proces is voltooid, wordt Hallo 'aangepaste HTTPS'-status in hello Azure-portal te 'Enabled' worden ingesteld. HTTPS met uw aangepaste domein is nu gereed voor gebruik.

## <a name="frequently-asked-questions"></a>Veelgestelde vragen

1. *Wie is Hallo certificaatprovider en type van het certificaat dat wordt gebruikt?*

    We gebruiken namen met alternatieve onderwerp (SAN)-certificaat opgegeven door DigiCert. Een SAN-certificaat kan meerdere FQDN-namen met één certificaat kunt beveiligen.

2. *Kan ik mijn speciaal certificaatarchief gebruiken?*
    
    Momenteel niet, maar de op Hallo roadmap.

3. *Wat gebeurt er als ik ontvang geen Hallo domein bevestigingsmail van DigiCert?*

    Neem contact op met Microsoft als u een e-mailbericht niet binnen 24 uur ontvangt.

4. *Maakt gebruik van een SAN-certificaat minder veilig dan een speciaal certificaatarchief?*
    
    Een SAN-certificaat volgt Hallo dezelfde codering en beveiliging normen als een certificaat dat is toegewezen. Alle uitgegeven certificaten voor SSL gebruikt SHA-256 voor uitgebreide beveiliging.

5. *Kan ik het aangepaste domein HTTPS gebruiken met Azure CDN van Akamai?*

    Deze functie is momenteel alleen beschikbaar met Azure CDN van Verizon. We werken aan deze functie met Azure CDN van Akamai ondersteunende in de komende maanden Hallo.


## <a name="next-steps"></a>Volgende stappen

- Meer informatie over hoe tooset van een [aangepast domein op uw Azure CDN-eindpunt](./cdn-map-content-to-custom-domain.md)



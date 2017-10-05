---
title: HTTPS op een aangepaste Azure CDN-domein inschakelen | Microsoft Docs
description: Informatie over het inschakelen van HTTPS voor uw Azure CDN-eindpunt met een aangepast domein.
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
ms.openlocfilehash: b334ba6bbec1d0a7e23a514174bffae01c7fff05
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="enable-https-on-an-azure-cdn-custom-domain"></a>HTTPS op een aangepast domein van Azure CDN inschakelen

[!INCLUDE [cdn-verizon-only](../../includes/cdn-verizon-only.md)]

HTTPS-ondersteuning voor aangepaste domeinen Azure CDN kunt u beveiligde inhoud met SSL-beveiliging met behulp van uw eigen domeinnaam voor het verbeteren van de beveiliging van gegevens die onderweg leveren. De end-to-end werkstroom HTTPS inschakelen voor uw aangepaste domein wordt vereenvoudigd, via één klik inschakelen, Certificaatbeheer voltooid en alle met zonder extra kosten.

Het is essentieel om te controleren of de privacy en integriteit van gegevens van al uw web-toepassingen gevoelige gegevens die onderweg. Met behulp van het HTTPS-protocol, zorgt u ervoor dat uw vertrouwelijke gegevens worden versleuteld wanneer ze via internet worden verzonden. Het biedt vertrouwt, verificatie en uw webtoepassingen worden beschermd tegen aanvallen. Op dit moment ondersteunt Azure CDN HTTPS op een CDN-eindpunt. Als u een CDN-eindpunt vanaf Azure CDN (bijvoorbeeld https://contoso.azureedge.net) maakt, wordt HTTPS bijvoorbeeld standaard ingeschakeld. Nu met het aangepaste domein HTTPS kunt u beveiligde levering voor een aangepast domein (bijvoorbeeld https://www.contoso.com) ook. 

Enkele van de belangrijkste kenmerken van HTTPS-functie zijn:

- Kan zonder extra kosten: Er zijn geen kosten voor het verkrijgen van het certificaat of vernieuwen en zonder extra kosten voor HTTPS-verkeer. U betaalt alleen uitgaande GB vanaf de CDN.

- Eenvoudige activering: één klik inrichting is beschikbaar via de [Azure-portal](https://portal.azure.com). U kunt ook REST-API of andere ontwikkelhulpprogramma's gebruiken de functie in te schakelen.

- Voltooien van Certificaatbeheer: alle aanschaf van het certificaat en u wordt beheerd. Certificaten worden automatisch worden ingericht en vóór de vervaldatum worden vernieuwd. Hiermee verwijdert u volledig de risico's van de service wordt onderbroken als gevolg van een certificaat verloopt.

>[!NOTE] 
>Voordat het HTTPS-ondersteuning wordt ingeschakeld, u moet hebben al een [aangepaste Azure CDN-domein](./cdn-map-content-to-custom-domain.md).

## <a name="step-1-enabling-the-feature"></a>Stap 1: Het inschakelen van de functie 

1. In de [Azure-portal](https://portal.azure.com), blader naar uw Verizon standard of premium CDN-profiel.

2. Klik op het eindpunt met uw aangepaste domein in de lijst met eindpunten.

3. Klik op het aangepaste domein waarvoor u wilt inschakelen van HTTPS.

    ![De blade een eindpunt](./media/cdn-custom-ssl/cdn-custom-domain.png)

4. Klik op **op** HTTPS inschakelen en sla de wijziging op.

    ![Dialoogvenster voor aangepaste HTTPS](./media/cdn-custom-ssl/cdn-enable-custom-ssl.png)


## <a name="step-2-domain-validation"></a>Stap 2: Validatie van domein

>[!IMPORTANT] 
>U moet domeinvalidatie voltooien voordat HTTPS actief op uw aangepaste domein zijn. U hebt 6 werkdagen goedkeuren van het domein. Aanvraag worden met geen goedkeuring binnen 6 werkdagen geannuleerd.  

Nadat HTTPS op uw aangepaste domein is ingeschakeld, valideert onze certificaatprovider HTTPS DigiCert eigendom van uw domein Neem contact op met de registrant voor uw domein, op basis van WHOIS registrant informatie via e-mail (standaard) of telefoon. DigiCert ontvangt ook de e-verificatie aan de onderstaande adressen. Als WHOIS registrant informatie persoonlijke, zorg er dan voor dat u rechtstreeks vanuit een van deze adressen kan goedkeuren.

>beheerder @ beheerder < uw-domain-name.com > @< uw-domain-name.com >  
>webbeheerder @< uw-domain-name.com >  
>hostmaster @< uw-domain-name.com >  
>postbeheerder @< uw-domain-name.com >


Bij ontvangst van het e-mailbericht, hebt u twee opties voor verificatie:

1. U kunt alle toekomstige orders geplaatst via dezelfde account voor het domein in dezelfde hoofdmap, bijvoorbeeld consoto.com goedkeuren. Dit is een aanbevolen aanpak als u van plan bent extra aangepaste domeinen toevoegen in de toekomst voor het hoofddomein van dezelfde.
 
2. U kunt alleen de specifieke host-naam die in deze aanvraag goedkeuren. Aanvullende goedkeuring is vereist voor de volgende aanvragen.

    Voorbeeld e-mailadres:
    
    ![Dialoogvenster voor aangepaste HTTPS](./media/cdn-custom-ssl/domain-validation-email-example.png)

Na de goedkeuring, wordt de DigiCert uw aangepaste domeinnaam toevoegen aan de SAN-certificaat. Het certificaat wordt één jaar geldig zijn en wordt automatisch vernieuwd voordat deze is verlopen.

## <a name="step-3-wait-for-the-propagation-then-start-using-your-feature"></a>Stap 3: Wacht totdat de doorgifte en start met behulp van de functie

Het duurt maximaal 6-8 uur voor de functie aangepast domein HTTPS actief nadat de domeinnaam is gevalideerd. Nadat het proces voltooid is, wordt de status 'aangepaste HTTPS' in de Azure portal worden ingesteld op 'Enabled'. HTTPS met uw aangepaste domein is nu gereed voor gebruik.

## <a name="frequently-asked-questions"></a>Veelgestelde vragen

1. *Wie is de certificaatprovider en type van het certificaat dat wordt gebruikt?*

    We gebruiken namen met alternatieve onderwerp (SAN)-certificaat opgegeven door DigiCert. Een SAN-certificaat kan meerdere FQDN-namen met één certificaat kunt beveiligen.

2. *Kan ik mijn speciaal certificaatarchief gebruiken?*
    
    Momenteel niet, maar het is in het overzicht.

3. *Wat gebeurt er als ik ontvang geen bevestigingsmail van het domein van DigiCert?*

    Neem contact op met Microsoft als u een e-mailbericht niet binnen 24 uur ontvangt.

4. *Maakt gebruik van een SAN-certificaat minder veilig dan een speciaal certificaatarchief?*
    
    Een SAN-certificaat voldoet aan de dezelfde codering en beveiliging standaarden als een certificaat dat is toegewezen. Alle uitgegeven certificaten voor SSL gebruikt SHA-256 voor uitgebreide beveiliging.

5. *Kan ik het aangepaste domein HTTPS gebruiken met Azure CDN van Akamai?*

    Deze functie is momenteel alleen beschikbaar met Azure CDN van Verizon. We werken aan deze functie met Azure CDN van Akamai ondersteunende in de komende maanden.


## <a name="next-steps"></a>Volgende stappen

- Meer informatie over het instellen van een [aangepast domein op uw Azure CDN-eindpunt](./cdn-map-content-to-custom-domain.md)



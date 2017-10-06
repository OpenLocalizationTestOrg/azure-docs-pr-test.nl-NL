---
title: ontwerpoverwegingen voor aaaAzure Active Directory hybride identiteit - bepalen gegevensbeveiligingsvereisten | Microsoft Docs
description: Bij het plannen van uw oplossing voor hybride identiteit identificeren Hallo beveiligingsvereisten voor gegevens voor uw bedrijf en welke opties zijn beschikbaar toobest aan die vereisten voldoen.
documentationcenter: 
services: active-directory
author: billmath
manager: femila
editor: 
ms.assetid: 40dc4baa-fe82-4ab6-a3e4-f36fa9dcd0df
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 189abf9affbc2894c322f362d84222d4e33d472e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="plan-for-enhancing-data-security-through-strong-identity-solution"></a>Plan voor het verbeteren van de beveiliging van gegevens via de van de sterke-identiteitsoplossing
Hallo eerste stap tooprotect Hallo gegevens is bepalen wie toegang heeft tot die gegevens en als onderdeel van dit proces moet u toohave een oplossing die kan worden geïntegreerd met uw systeem tooprovide verificatie en autorisatie worden uitgebreid. Verificatie en autorisatie worden vaak verward met elkaar en hun rollen verkeerd begrepen. In werkelijkheid zijn ze heel anders, zoals wordt weergegeven in onderstaande afbeelding ziet Hallo:

![](./media/hybrid-id-design-considerations/mobile-devicemgt-lifecycle.png)

**Fasen van de levenscyclus van mobiele apparaten**

Bij het plannen van uw oplossing voor hybride identiteit moet u begrijpen Hallo beveiligingsvereisten voor gegevens voor uw bedrijf en welke opties zijn beschikbaar toobest voldoen aan deze vereisten.

> [!NOTE]
> Wanneer u klaar bent met het plannen van de beveiliging van gegevens controleren [vereisten multi-factor authentication bepalen](active-directory-hybrid-identity-design-considerations-multifactor-auth-requirements.md) tooensure dat uw selecties met betrekking tot vereisten multi-factor authentication is niet van invloed op Hallo beslissingen u hebt gemaakt in deze sectie.
> 
> 

## <a name="determine-data-protection-requirements"></a>Bepalen van de beveiligingsvereisten voor gegevens
Hallo leeftijd mobiliteit van de meeste bedrijven hebben een gemeenschappelijk doel: hun gebruikers toobe productief op hun mobiele apparaten als ze op kantoor of extern vanaf een willekeurige plaats in de volgorde tooincrease productiviteit inschakelen. Hoewel dit kan een gemeenschappelijk doel, worden bedrijven die vereist zijn om te gaan met betrekking tot Hallo hoeveelheid bedreigingen die moeten worden beperkt in volgorde tookeep van bedrijfsgegevens veilig en onderhouden van de privacy van gebruikers ook. Elk bedrijf heeft wellicht andere vereisten in dit opzicht; andere compatibiliteitsregels die variëren volgens toowhich bedrijfstak Hallo bedrijf fungeert wordt toodifferent ontwerpbeslissingen leiden. 

Er zijn echter enkele beveiligingsaspecten die moeten worden verkend en gevalideerd, ongeacht de branche hello, die worden beschreven in de volgende sectie Hallo.

## <a name="data-protection-paths"></a>Gegevenspaden voor beveiliging
![](./media/hybrid-id-design-considerations/data-protection-paths.png)

**Gegevenspaden voor beveiliging**

In Hallo bovenstaande diagram niet de onderdeel-id Hallo Hallo eerst een toobe geverifieerd voordat gegevens worden geopend. Deze gegevens kunnen zich in verschillende statussen tijdens het Hallo-tijd die is aangesproken. Elk getal in dit diagram vertegenwoordigt een pad waarin gegevens gevonden op een bepaald punt in tijd worden kunnen. Deze getallen worden hieronder beschreven:

1. Gegevensbescherming op apparaatniveau Hallo.
2. Gegevensbescherming onderweg.
3. Bescherming van cloudgegevens in rust lokale.
4. Bescherming van cloudgegevens in rust in Hallo.

Hoewel Hallo technische besturingselementen waarmee IT tooprotect Hallo gegevens zelf op elk van deze fasen niet rechtstreeks door Hallo hybride identiteitsoplossing aangeboden worden, is het nodig dat Hallo hybride identiteitsoplossing geschikt voor gebruik van zowel is on-premises en cloud identity management-resources tooidentify Hallo gebruiker voordat verlenen toegang tot toohello gegevens. Tijdens het plannen van uw oplossing voor hybride identiteit Zorg ervoor dat Hallo volgende worden vragen beantwoord de tooyour organisatievereisten op basis van:

## <a name="data-protection-at-rest"></a>Gegevensbescherming van in rust
Ongeacht waar Hallo gegevens in rust (apparaat, cloud of on-premises), is het belangrijk tooperform een beoordeling toounderstand Hallo organisatie moet in dit opzicht. Zorg ervoor dat Hallo volgende vragen worden gesteld voor dit gebied:

* Heeft uw bedrijf behoefte aan tooprotect gegevens in rust?
  * Zo ja, is Hallo hybride identiteit oplossing kunnen toointegrate met uw huidige on-premises infrastructuur?
  * Zo ja, is uw workloads die zich in de cloud Hallo Hallo hybride identiteit oplossing kunnen toointegrate?
* Hallo cloud identity management kunnen tooprotect Hallo de referenties van gebruiker en andere gegevens die zijn opgeslagen in de cloud Hallo is?

## <a name="data-protection-in-transit"></a>Gegevensbescherming onderweg
Gegevens onderweg tussen Hallo-apparaat en Hallo datacenter of Hallo-apparaat en Hallo cloud moeten worden beveiligd. Echter, worden in transit betekent niet noodzakelijkerwijs een proces voor communicatie met een component buiten uw cloudservice; verplaatst intern ook, bijvoorbeeld tussen twee virtuele netwerken. Zorg ervoor dat Hallo volgende vragen worden gesteld voor dit gebied:

* Heeft uw bedrijf behoefte aan tooprotect gegevens die onderweg?
  * Zo ja, is Hallo hybride identiteit oplossing kunnen toointegrate met veilige besturingselementen zoals SSL/TLS?
* Houdt Hallo cloud identity management Hallo verkeer tooand binnen Hallo directory-archief (binnen en tussen datacenters) ondertekend?

## <a name="compliance"></a>Naleving
Vereisten voor naleving van regelgeving, wettelijke en voorschriften varieert volgens toohello bedrijfstak die deel uitmaakt van uw bedrijf. Bedrijven in hoog gereglementeerde branches moeten identiteitsbeheer problemen toocompliance gerelateerde problemen op te lossen. Regelgeving zoals Sarbanes-Oxley (SOX), Hallo Health Insurance Portability and Accountability Act (HIPAA), Hallo Gramm-Leach-Bliley Act (GLBA) en Hallo Payment Card Industry Data Security Standard (PCI DSS) zijn zeer strikte met betrekking tot identiteits- en toegangsbeheer. Hallo hybride identiteitsoplossing die uw bedrijf invoert moet Hallo belangrijkste mogelijkheden die zal voldoen aan de vereisten van een of meer van deze voorschriften Hallo hebben. Zorg ervoor dat Hallo volgende vragen worden gesteld voor dit gebied:

* Hallo hybride identiteitsoplossing voldoen aan wettelijke vereisten voor uw bedrijf Hallo is?
* Biedt Hallo hybride identiteitsoplossing met ingebouwde mogelijkheden waarmee u uw bedrijf toobe compatibele wettelijke vereisten? 

> [!NOTE]
> Zorg ervoor dat tootake notities van elk antwoord en Hallo logica achter Hallo antwoord begrijpt. [Definieer de strategie voor gegevensbescherming](active-directory-hybrid-identity-design-considerations-data-protection-strategy.md) gaat over de beschikbare opties voor Hallo en de voor-en nadelen van elke optie.  Moet door deze vragen die u selecteert welke optie het beste past bij uw bedrijf te beantwoorden.
> 
> 

## <a name="next-steps"></a>Volgende stappen
 [Vereisten voor inhoudsbeheer bepalen](active-directory-hybrid-identity-design-considerations-contentmgt-requirements.md)

## <a name="see-also"></a>Zie ook
[Overzicht ontwerpoverwegingen](active-directory-hybrid-identity-design-considerations-overview.md)


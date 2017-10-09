---
title: Azure AD Connect Health with AD FS aaaUsing | Microsoft Docs
description: Dit is hello Azure AD Connect Health pagina hoe toomonitor uw on-premises AD FS-infrastructuur.
services: active-directory
documentationcenter: 
author: karavar
manager: femila
editor: curtand
ms.assetid: dc0e53d8-403e-462a-9543-164eaa7dd8b3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/18/2017
ms.author: billmath
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 0cd26e8762be65e09d22e1f113e5165c4f131715
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-ad-fs-using-azure-ad-connect-health"></a>AD FS bewaken met Azure AD Connect Health
Hallo volgende documentatie is specifiek toomonitoring uw AD FS-infrastructuur met Azure AD Connect Health. Zie [Using Azure AD Connect Health for Sync](active-directory-aadconnect-health-sync.md) (Engelstalig) voor informatie over het bewaken van Azure AD Connect (synchronisatie) met Azure AD Connect Health. Zie ook [Azure AD Connect Health gebruiken met AD DS](active-directory-aadconnect-health-adds.md) voor informatie over het bewaken van Active Directory Domain Services met Azure AD Connect Health.

## <a name="alerts-for-ad-fs"></a>Waarschuwingen voor AD FS
Hallo sectie Azure waarschuwingen AD Connect Health biedt Hallo van lijst met actieve waarschuwingen. Elke waarschuwing omvat relevante informatie, stappen voor het oplossen en koppelingen toorelated documentatie.

U kunt dubbelklikken op een waarschuwing, tooopen actief of opgelost een nieuwe blade met aanvullende informatie, stappen u kunt ondernemen tooresolve Hallo waarschuwing en koppelingen toorelevant documentatie. U kunt ook historische gegevens weergeven voor waarschuwingen die in de afgelopen Hallo zijn opgelost.

![Portal voor Azure AD Connect Health](./media/active-directory-aadconnect-health/alert2.png)

## <a name="usage-analytics-for-ad-fs"></a>Gebruiksanalyses voor AD FS
Azure AD Connect Health gebruiksanalyse analyseert het verificatieverkeer Hallo van uw federatieservers. U kunt dubbelklikken op Hallo het vakje voor gebruiksanalyses, tooopen Hallo blade met gebruiksanalyses, waarin u verschillende metrische gegevens en groeperingen kunt zien.

> [!NOTE]
> toouse gebruiksanalyses met AD FS, moet u controleren of AD FS-controle is ingeschakeld. Ga voor meer informatie naar [Controles voor AD FS inschakelen](active-directory-aadconnect-health-agent-install.md#enable-auditing-for-ad-fs).
>
>

![Portal voor Azure AD Connect Health](./media/active-directory-aadconnect-health/report1.png)

tooselect aanvullende gegevens, een tijdsbereik of toochange Hallo groepering opgeven, met de rechtermuisknop op Hallo grafiek met gebruiksanalyses en selecteer grafiek bewerken. U kunt vervolgens Hallo tijdsperiode opgeven, selecteer een andere waarde en Hallo groepering wijzigen. U kunt Hallo distributie van Hallo verificatieverkeer op basis van verschillende "gegevens" weergeven en alle gegevens met behulp van relevante 'groeperen op'-parameters die zijn beschreven in de volgende sectie Hallo groeperen:

**Metriek: totaal aantal verzoeken**: het totale aantal verzoeken dat door AD FS-servers is verwerkt.

|Groeperen op | Wat het betekent als Hallo groepering en waarom is het nuttig? |
| --- | --- |
| Alle | Hallo-telling van het totale aantal aanvragen dat is verwerkt door alle AD FS-servers bevat.|
| Toepassing | Groepen Hallo totaal aantal aanvragen op basis van de relying party Hallo gericht. Deze groepering is nuttig toounderstand welke toepassing welk percentage van totale Hallo-verkeer ontvangt. |
|  Server |Groepen Hallo totaal aantal aanvragen op basis van Hallo-server die Hallo aanvraag verwerkt. Deze groepering is nuttig toounderstand Hallo verdeling van het totale Hallo-verkeer.
| Werkplek koppelen |Groepen Hallo totaal aantal aanvragen op basis van of ze afkomstig zijn van apparaten die toegevoegd aan de werkplek zijn (bekend). Deze groepering is nuttig toounderstand als uw resources worden geopend met behulp van apparaten die onbekende toohello-infrastructuur voor identiteiten zijn. |
|  Verificatiemethode | Groepen Hallo totaal aantal aanvragen op basis van Hallo verificatiemethode wordt gebruikt voor verificatie. Deze groepering is nuttig toounderstand Hallo gemeenschappelijke verificatiemethode die wordt gebruikt voor verificatie. Hieronder volgen de mogelijke verificatiemethoden Hallo <ol> <li>Geïntegreerde Windows-verificatie (Windows)</li> <li>Op formulieren gebaseerde verificatie (formulieren)</li> <li>Optie voor eenmalige aanmelding (SSO)</li> <li>Op X509-certificaat gebaseerde verificatie (certificaat)</li> <br>Als federatieservers Hallo Hallo-aanvraag met een SSO-Cookie ontvangt, wordt die aanvraag geteld als eenmalige aanmelding (eenmalige aanmelding). In dergelijke gevallen Hallo cookie is geldig, Hallo gebruiker niet tooprovide referenties gevraagd als naadloze toegang toohello toepassing opgehaald. Dit gedrag is gebruikelijk dat als u meerdere relying party's beveiligd door Hallo federatieservers hebt. |
| Netwerklocatie | Groepen Hallo totaal aantal aanvragen op basis van de netwerklocatie Hallo van Hallo-gebruiker. Dit kan intranet of extranet zijn. Deze groepering is nuttig tooknow welk percentage van het Hallo-verkeer afkomstig is van Hallo intranet versus extranet. |


**Metrische: Totale mislukt aanvraag** -Hallo totaal aantal mislukte aanvragen verwerkt door Hallo federation-service. (Deze gegevens zijn alleen beschikbaar op AD FS voor Windows Server 2012 R2)

|Groeperen op | Wat het betekent als Hallo groepering en waarom is het nuttig? |
| --- | --- |
| Fouttype | Toont het aantal fouten op basis van vooraf gedefinieerde fouttypen Hallo. Deze groepering is nuttig toounderstand Hallo veelvoorkomende fouttypen. <ul><li>Onjuiste gebruikersnaam of wachtwoord: fouten vanwege tooincorrect gebruikersnaam of wachtwoord.</li> <li>"Extranet Lockout": fouten vanwege toohello aanvragen ontvangen van een gebruiker die is uitgesloten van extranet </li><li> 'Wachtwoord verlopen': fouten vanwege toousers aangemeld met een verlopen wachtwoord.</li><li>"Account uitgeschakeld": fouten vanwege toousers logboekregistratie met een uitgeschakeld account.</li><li>"Apparaatverificatie": fouten vanwege toousers mislukken tooauthenticate met behulp van Apparaatverificatie.</li><li>"Verificatie met gebruikerscertificaat": fouten vanwege tooauthenticate toousers mislukt vanwege een ongeldig certificaat.</li><li>"MFA": fouten vanwege toouser mislukken tooauthenticate met multi-factor Authentication.</li><li>"Andere referentie": "Autorisatie uitgifte": fouten vanwege tooauthorization fouten.</li><li>"Overdracht uitgifte": fouten vanwege fouten bij het tooissuance delegeren.</li><li>"Acceptatie token": fouten vanwege tooADFS weigeren Hallo-token van een derde partij ID-Provider.</li><li>"Protocol": mislukt vanwege tooprotocol fouten.</li><li>'Onbekend': algemene melding. Andere fouten die niet in het Hallo passen gedefinieerde categorieën.</li> |
| Server | Groepen Hallo fouten op basis van Hallo-server. Deze groepering is nuttig toounderstand Hallo fouten zijn verdeeld over servers. Een ongelijke verdeling kan wijzen op een server die in slechte staat is. |
| Netwerklocatie | Groepen Hallo fouten op basis van netwerklocatie op Hallo van Hallo verzoeken (intranet VS. extranet). Deze groepering is nuttig toounderstand Hallo type aanvragen die zijn mislukt. |
|  Toepassing | Groepen Hallo fouten op basis van Hallo gericht-applicatie (relying party). Deze groepering is nuttig toounderstand welke doeltoepassing de meeste aantal fouten. |

**Metriek: gebruikersaantal**: het gemiddelde aantal unieke gebruikers die actief verifiëren met AD FS

|Groeperen op | Wat het betekent als Hallo groepering en waarom is het nuttig? |
| --- | --- |
|Alle |Met deze metriek wordt een telling van gemiddelde aantal gebruikers met Hallo federation-service in de geselecteerde tijdvak Hallo. Hallo gebruikers zijn niet gegroepeerd. <br>Hallo gemiddelde is afhankelijk van Hallo geselecteerde tijdsperiode. |
| Toepassing |Groepen Hallo gemiddelde aantal gebruikers op basis van Hallo gericht toepassing (relying party). Deze groepering is nuttig toounderstand hoeveel gebruikers gebruikmaken van elke toepassing. |

## <a name="performance-monitoring-for-ad-fs"></a>Prestatiebewaking voor AD FS
Prestatiebewaking voor Azure AD Connect Health biedt bewakingsinformatie over de gegevens. Als u Hallo bewaking inschakelt, wordt een nieuwe blade geopend met gedetailleerde informatie over Hallo metrische gegevens.

![Portal voor Azure AD Connect Health](./media/active-directory-aadconnect-health/perf1.png)

Als u de filteroptie Hallo Hallo boven aan het Hallo-blade selecteert, kunt u filteren op server toosee metrische gegevens van een afzonderlijke server. toochange metriek, met de rechtermuisknop op de bewaking van de grafiek onder bewaking blade Hallo Hallo en selecteer grafiek bewerken (of selecteer Hallo grafiek bewerken knop). U kunt aanvullende gegevens selecteren uit de vervolgkeuzelijst Hallo en geef een tijdsbereik voor het weergeven van prestatiegegevens Hallo Hallo nieuwe blade die wordt geopend.

## <a name="reports-for-ad-fs"></a>Rapporten voor AD FS
Azure AD Connect Health biedt rapporten over de activiteit en prestaties van AD FS. Dankzij deze rapporten krijgen beheerders meer inzicht in de activiteiten op de AD FS-servers.

### <a name="top-50-users-with-failed-usernamepassword-logins"></a>Top 50 van gebruikers met mislukte aanmeldingen vanwege een verkeerde gebruikersnaam of verkeerd wachtwoord
Een van de Hallo veelvoorkomende redenen voor een mislukt verificatieverzoek op een AD FS-server is een verzoek met ongeldige referenties, dat wil zeggen, een onjuiste gebruikersnaam of wachtwoord. Meestal gebeurt toousers vanwege toocomplex wachtwoorden, vergeten wachtwoorden of typfouten.

Maar er zijn andere redenen die kunnen leiden tot een onverwacht aantal aanvragen dat wordt verwerkt door uw AD FS-servers, zoals: een toepassing die caches gebruikersreferenties en Hallo referenties verlopen of een kwaadwillende gebruiker toosign die bij een account met een reeks bekende wachtwoorden. De volgende twee voorbeelden zijn geldige redenen die tooa piek in aanvragen kunnen leiden.

Azure AD Connect Health voor AD FS biedt een rapport over top 50 van gebruikers met mislukte inlogpogingen vanwege tooinvalid gebruikersnaam of wachtwoord. Dit rapport wordt bereikt door het verwerken van Hallo controlegebeurtenissen die worden gegenereerd door alle Hallo AD FS-servers in het Hallo-farms

![Portal voor Azure AD Connect Health](./media/active-directory-aadconnect-health-adfs/report1a.png)

In dit rapport hebt u eenvoudig toegang toohello stukjes informatie te volgen:

* Totaal aantal mislukte verzoeken met een onjuiste gebruikersnaam en wachtwoord in Hallo afgelopen 30 dagen
* Gemiddeld aantal gebruikers per dag die zich proberen aan te melden met een onjuiste gebruikersnaam en wachtwoord.

Op dit deel te klikken, gaat u toohello hoofdrapport-blade waarmee de vindt u meer informatie. Deze blade bevat een grafiek met trends informatie toohelp tot stand brengen van een basislijn over aanvragen met een onjuiste gebruikersnaam of wachtwoord. Daarnaast biedt het Hallo-lijst van de bovenste 50 gebruikers met het aantal mislukte pogingen Hallo.

Hallo grafiek biedt Hallo volgende informatie:

* Hallo totaal aantal mislukte aanmeldingen vanwege tooa onjuiste gebruikersnaam en wachtwoord per dag.
* Hallo totale aantal unieke gebruikers met aanmeldingen per dag mislukte.
* Client IP-adres van de laatste aanvraag

![Portal voor Azure AD Connect Health](./media/active-directory-aadconnect-health-adfs/report3a.png)

Hallo rapport biedt Hallo volgende informatie:

| Rapportitem | Beschrijving |
| --- | --- |
| Gebruikers-ID |Toont Hallo gebruikers-ID die is gebruikt. Deze waarde is wat Hallo gebruiker hebt getypt, wat in sommige gevallen is Hallo onjuiste gebruikers-ID wordt gebruikt. |
| Mislukte pogingen |Toont hello totaal aantal mislukte pogingen voor die specifieke gebruikers-ID. Hallo-tabel is gesorteerd Hello meest aantal mislukte pogingen in aflopende volgorde. |
| Laatste fout |Hallo tijdstempel ziet wanneer Hallo laatste fout is opgetreden. |
| IP laatste fout |Hallo Client-IP-adres van de meest recente onjuiste aanvraag Hallo bevat. |

> [!NOTE]
> Dit rapport wordt automatisch bijgewerkt nadat elke twee uur Hello nieuwe informatie verzameld binnen die tijd. Als gevolg hiervan kunnen inlogpogingen van Hallo laatste twee uur niet worden opgenomen in Hallo rapport.
>
>

## <a name="related-links"></a>Verwante koppelingen
* [Azure AD Connect Health (Engelstalig)](active-directory-aadconnect-health.md)
* [De Azure AD Connect Health-agent installeren](active-directory-aadconnect-health-agent-install.md)
* [Azure AD Connect Health Operations](active-directory-aadconnect-health-operations.md) (Azure AD Connect Health-bewerkingen)
* [Azure AD Connect Health for Sync gebruiken](active-directory-aadconnect-health-sync.md)
* [Azure AD Connect Health gebruiken met AD DS](active-directory-aadconnect-health-adds.md)
* [Veelgestelde vragen over Azure AD Connect Health](active-directory-aadconnect-health-faq.md)
* [Versiegeschiedenis van Azure AD Connect Health](active-directory-aadconnect-health-version-history.md)
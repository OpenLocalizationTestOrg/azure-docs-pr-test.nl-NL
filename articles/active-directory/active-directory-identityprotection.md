---
title: 'Active Directory: Identity Protection aaaAzure | Microsoft Docs'
description: Meer informatie over hoe Azure AD Identity Protection kunt u toolimit Hallo mogelijkheid van een aanvaller tooexploit de identiteit van een verdachte of apparaat en toosecure een identiteit of een apparaat dat eerder verdachte of bekende toobe aangetast.
services: active-directory
keywords: beveiliging in Azure active directory-identiteit, cloud app discovery, het beheren van toepassingen, beveiliging, risico, risiconiveau, beveiligingsprobleem, beveiligingsbeleid
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: e7434eeb-4e98-4b6b-a895-b5598a6cccf1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: ecca4f3cdb65585687cf44a80024f26c7cab22ca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-identity-protection"></a>Azure Active Directory Identity Protection

Azure Active Directory: Identity Protection is een functie van Azure AD Premium-P2 Hallo edition waarmee u kunt:

- Detecteren van mogelijke beveiligingsproblemen die invloed hebben op de identiteiten van uw organisatie

- Automatische antwoorden toodetected verdachte acties die van de organisatie van de gerelateerde tooyour identiteiten configureren  

- Verdachte incidenten onderzoeken en tooresolve passende maatregelen nemen ze   


## <a name="getting-started"></a>Aan de slag

Microsoft beveiligt cloud-gebaseerde identiteiten voor meer dan een tien jaar. Met Azure Active Directory: Identity Protection in uw omgeving, kunt u Hallo toosecure identiteiten maakt gebruik van dezelfde systemen ter bescherming van Microsoft.

Hallo overgrote deel van de beveiliging schendingen nemen plaatsen wanneer aanvallers toegang tooan omgeving krijgen door de identiteit van een gebruiker te stelen. Hallo jaar zijn aanvallers steeds effectief gebruik van schendingen van derden en het gebruik van geavanceerde phishingaanvallen geworden. Als een aanvaller toegang tooeven gebruikersaccounts met lage bevoegdheden heeft, is het relatief gemakkelijk toe toogain toegang tooimportant bedrijfsbronnen via laterale verplaatsing.

Als gevolg hiervan moet u:

- Beveiligen van alle identiteiten ongeacht hun machtigingsniveau

- Proactief te voorkomen dat waarmee is geknoeid identiteiten geschonden

Detectie van verdachte identiteiten is geen eenvoudige taak. Azure Active Directory maakt gebruik van geavanceerde machine learning-algoritmen en methodiek toodetect afwijkingen en verdachte incidenten die mogelijk aangeven identiteiten waarmee is geknoeid. Met deze gegevens Identity Protection genereert rapporten en meldingen waarmee u tooevaluate Hallo heeft problemen gedetecteerd en het juiste risicobeperking of herstelacties duren.

Azure Active Directory: Identity Protection is meer dan een controle en rapportage. tooprotect identiteiten van uw organisatie, kunt u risico-beleidsregels die automatisch toodetected problemen reageren als een opgegeven risiconiveau is bereikt. Deze beleidsregels bovendien tooother voorwaardelijke toegang tot de besturingselementen die worden geleverd door Azure Active Directory en EMS, kunnen automatisch blokkeren of initiëren adaptieve herstelacties met inbegrip van wachtwoorden en afdwingen van multi-factor authentication-server.


#### <a name="identity-protection-capabilities"></a>Mogelijkheden voor preventie van identiteit

**Detecteren van zwakke plekken en riskant accounts:**  

* Aangepaste aanbevelingen tooimprove bieden algehele beveiligingsstatus beveiligingslekken markeert
* Aanmelden risiconiveaus berekenen
* Gebruiker risiconiveaus berekenen


**Bezig met het onderzoeken van risico's:**

* Verzenden van meldingen voor risico 's
* Het onderzoeken van risico's met behulp van de relevante en contextuele informatie
* Biedt eenvoudige werkstromen tootrack onderzoeken
* Eenvoudige toegang bieden tooremediation acties zoals het wachtwoord opnieuw instellen

**Beleid voor voorwaardelijke toegang op basis van risico's:**

* Beleid toomitigate riskant aanmeldingen door aanmeldingen blokkeren of uitdagingen voor meervoudige verificatie vereisen.
* Beleid tooblock of beveiligde riskant gebruikersaccounts
* Beleid toorequire gebruikers tooregister voor multi-factor authentication



## <a name="identity-protection-roles"></a>Identity Protection-functies

tooload saldo Hallo beheeractiviteiten rond de Identity Protection-implementatie, kunt u verschillende rollen toewijzen. Azure AD Identity Protection ondersteunt 3 directory-functies:

| Rol                         | Kan doen                          | Is niet mogelijk
| :--                          | ---                                |  ---   |
| Globale beheerder         | Volledige toegang tooIdentity, beveiliging, vrijgeven Identity Protection| |
| Beveiligingsbeheerder       | Volledige toegang tooIdentity beveiliging | Ingebouwde Identity Protection, wachtwoorden opnieuw instellen voor een gebruiker |
| Beveiligingslezer              | Klaar voor alleen-lezen toegang tooIdentity beveiliging | Ingebouwde Identity Protection, remidiate gebruikers,-beleid configureren, wachtwoorden opnieuw instellen |




Zie voor meer informatie [beheerdersrollen toewijzen in Azure Active Directory](active-directory-assign-admin-roles-azure-portal.md)



## <a name="detection"></a>Detectie

### <a name="vulnerabilities"></a>Beveiligingsproblemen

Azure Active Directory: Identity Protection analyses van uw configuratie en beveiligingsproblemen die invloed op uw gebruikers-id's hebben kunnen detecteert. Zie voor meer informatie [beveiligingsproblemen die worden gedetecteerd door Azure Active Directory: Identity Protection](active-directory-identityprotection-vulnerabilities.md).

### <a name="risk-events"></a>Risico 's

Azure Active Directory maakt gebruik van geavanceerde machine learning-algoritmen en methodiek toodetect verdachte acties die gerelateerd tooyour gebruikersidentiteiten zijn. Hallo system maakt een record voor elke gedetecteerde verdachte actie. Deze records worden ook wel bekend als risico's.  
Zie [Risicogebeurtenissen in Azure Active Directory](active-directory-identity-protection-risk-events.md) voor meer informatie.


## <a name="investigation"></a>Onderzoek
Uw reis door Identity Protection begint meestal met Hallo Identity Protection-dashboard.

![Herstel](./media/active-directory-identityprotection/1000.png "herstel")

Hallo-dashboard hebt u toegang hebt tot:

* Rapporten, zoals **gebruikers die zijn gemarkeerd voor risico**, **bestaat de kans dat gebeurtenissen** en **beveiligingsproblemen**
* Instellingen zoals Hallo configuratie van uw **beveiligingsbeleid**, **meldingen** en **multi-factor authentication-registratie**

Het is doorgaans het startpunt voor onderzoek, waardoor het Hallo-proces controleren Hallo activiteiten, logboeken en andere relevante informatie gerelateerde tooa risico gebeurtenis toodecide of herstel of afname stappen zijn nodig is, en hoe Hallo identiteit was geknoeid en begrijpen hoe Hallo geknoeid met de identiteit is gebruikt.

U kunt verbinden, uw onderzoek activiteiten toohello [meldingen](active-directory-identityprotection-notifications.md) Azure Active Directory Protection per e-mail verzendt.

Hallo volgende secties vindt u meer details en Hallo stappen die gerelateerd tooan onderzoek zijn.  


## <a name="risky-sign-ins"></a>Riskant aanmeldingen

Azure Active Directory detecteert [risico gebeurtenistypen](active-directory-reporting-risk-events.md#risk-event-types) in realtime en offline. Elke risicogebeurtenis dat is aangetroffen voor een aanmelding van een gebruiker bijdraagt tooa logisch concept is aangeroepen riskant aanmelden. Een riskante aanmelden is een indicator voor een aanmeldingspoging die mogelijk niet uitgevoerd door Hallo rechtmatige eigenaar van een gebruikersaccount.


### <a name="sign-in-risk-level"></a>Aanmelden risiconiveau

Een aanmeldingspagina risiconiveau geeft aan dat er (hoog, Gemiddeld of laag) Hallo kans een aanmeldingspoging is niet uitgevoerd door Hallo legitieme eigenaar van een gebruikersaccount.

### <a name="mitigating-sign-in-risk-events"></a>Beperkende aanmelden risico 's

Een beperking is een actie toolimit Hallo mogelijkheid van een aanvaller tooexploit een waarmee is geknoeid identiteit of het apparaat zonder herstelstatus Hallo identiteit of het apparaat tooa veilig. Een risicobeperking vorige aanmelden risicogebeurtenissen die zijn gekoppeld aan het Hallo-identiteit of het apparaat niet is opgelost.

toomitigate riskant aanmeldingen automatisch, kunt u aanmelden risico beveiliging policicies configureren. Met deze beleidsregels, u Overweeg Hallo risiconiveau van Hallo gebruiker of Hallo aanmelden tooblock riskant aanmeldingen of Hallo gebruiker tooperform meervoudige authenticatie. Deze acties kunnen voorkomen dat een aanvaller een gestolen identiteit toocause schade misbruik van, en mogelijk hebt u een bepaalde tijd toosecure Hallo identiteit.

### <a name="sign-in-risk-security-policy"></a>Beveiligingsbeleid Aanmelden risico
Een beleid voor aanmelden risico is een beleid voor voorwaardelijke toegang dat Hallo risico tooa specifieke aanmelden wordt geëvalueerd en oplossingen op basis van vooraf gedefinieerde voorwaarden en regels van toepassing is.

![Beleid voor aanmelden risico](./media/active-directory-identityprotection/1014.png "aanmelden risico beleid")

Azure AD Identity Protection helpt u Hallo risicobeperking van riskante aanmeldingen doordat u beheren:

* Set Hallo gebruikers en groepen Hallo beleid van toepassing op:

    ![Beleid voor aanmelden risico](./media/active-directory-identityprotection/1015.png "aanmelden risico beleid")
* Hallo aanmelden risico niveau drempel instellen (laag, Gemiddeld of hoog) waarmee de Hallo beleid wordt geactiveerd:

    ![Beleid voor aanmelden risico](./media/active-directory-identityprotection/1016.png "aanmelden risico beleid")
* Set Hallo besturingselementen toobe afgedwongen als het Hallo-beleid wordt geactiveerd:  

    ![Beleid voor aanmelden risico](./media/active-directory-identityprotection/1017.png "aanmelden risico beleid")
* Hallo-status van uw beleid switch:

    ![Registratieprocedure voor MFA](./media/active-directory-identityprotection/403.png "registratieprocedure voor MFA")
* Bekijken en evalueren Hallo gevolgen van een wijziging voordat u deze activeert:

    ![Beleid voor aanmelden risico](./media/active-directory-identityprotection/1018.png "aanmelden risico beleid")

#### <a name="what-you-need-tooknow"></a>Wat u nodig hebt tooknow
U kunt een aanmeldingspagina risico beveiliging beleid toorequire multi-factor authentication configureren:

![Beleid voor aanmelden risico](./media/active-directory-identityprotection/1017.png "aanmelden risico beleid")

Echter, uit veiligheidsoverwegingen deze instelling werkt alleen voor gebruikers die al zijn geregistreerd voor multi-factor authentication. Als Hallo voorwaarde toorequire meervoudige verificatie voor een gebruiker die nog niet is geregistreerd voor multi-factor authentication is voldaan, is Hallo gebruiker geblokkeerd.

Als het wordt aanbevolen als u wilt dat toorequire multi-factor authentication voor riskante aanmeldingen, moet u:

1. Hallo inschakelen [registratiebeleid multi-factorauthenticatie](#multi-factor-authentication-registration-policy) voor Hallo van invloed op gebruikers.
2. Hallo toologin gebruikers in een niet-riskant sessie tooperform invloed op een registratieprocedure voor MFA vereisen

U deze stappen uitvoert, zorgt u ervoor dat meervoudige verificatie is vereist voor een riskante aanmelden.

#### <a name="best-practices"></a>Aanbevolen procedures
U kiest een **hoge** drempelwaarde vermindert het aantal keren dat een beleid wordt geactiveerd en minimaliseert Hallo impact toousers Hallo.  

Echter, worden uitgesloten **laag** en **gemiddeld** aanmeldingen gemarkeerd voor kwetsbaar voor aanvallen via Hallo-beleid, dat een aanvaller gebruikmaakt van de identiteit van een verdachte kan niet worden geblokkeerd.

Wanneer de instelling beleid Hallo

* Gebruikers die geen / multi-factor authentication-server kunnen geen uitsluiten
* Gebruikers in landen waar inschakelen Hallo beleid is het niet praktisch uitsluiten (bijvoorbeeld geen toohelpdesk toegang)
* Voorkomen dat gebruikers die waarschijnlijk toogenerate veel ONWAAR-positieven (ontwikkelaars, beveiligingsanalisten zijn)
* Gebruik een **hoge** drempelwaarde tijdens de eerste beleid implementeert, of als u uitdagingen die zichtbaar zijn voor eindgebruikers minimaliseert.
* Gebruik een **laag** drempelwaarde als uw organisatie betere beveiliging vereist. Als u een **laag** drempelwaarde introduceert extra gebruiker aanmelden uitdagingen, maar een hogere beveiliging.

Hallo standaard aanbevolen voor de meeste organisaties tooconfigure is een regel voor een **gemiddeld** drempelwaarde toostrike een balans tussen bruikbaarheid en veiligheid.

Hallo aanmelden risico beleid is:

* Toegepaste tooall browserverkeer en aanmeldingen die moderne authenticatie gebruiken.
* Niet toegepast tooapplications met oudere-protocollen door Hallo WS-Trust-eindpunt op Hallo federatieve IDP, zoals ADFS uit te schakelen.

Hallo **Risicogebeurtenissen** worden alle gebeurtenissen op deze pagina in Hallo Identity Protection-console:

* Dit beleid is toegepast
* U kunt Hallo activiteiten controleren en bepalen of de actie Hallo juiste of niet is

Voor een overzicht van Hallo gerelateerde gebruikerservaring, Zie:

* [Herstel voor riskante aanmelden](active-directory-identityprotection-flows.md#risky-sign-in-recovery)
* [Riskant aanmelden geblokkeerd](active-directory-identityprotection-flows.md#risky-sign-in-blocked)  
* [Aanmelden-ervaring met Azure AD Identity Protection](active-directory-identityprotection-flows.md)  

**dialoogvenster tooopen Hallo-gerelateerde configuratie**:

- Op Hallo **Azure AD Identity Protection** blade in Hallo **configureren** sectie, klikt u op **aanmelden risico beleid**.

    ![Gebruikersbeleid ridk](./media/active-directory-identityprotection/1014.png "ridk gebruikersbeleid")



## <a name="users-flagged-for-risk"></a>Gebruikers voor wie wordt aangegeven dat ze risico lopen

Alle actieve [bestaat de kans dat gebeurtenissen](active-directory-identity-protection-risk-events.md) die zijn gedetecteerd door Azure Active Directory voor een gebruiker bijdragen tooa logisch concept is aangeroepen gebruiker risico. Een gebruiker die is gemarkeerd voor risico is een indicator voor een gebruikersaccount die mogelijk zijn aangetast.

![Gebruikers voor wie wordt aangegeven dat ze risico lopen](./media/active-directory-identityprotection/1200.png)


### <a name="user-risk-level"></a>Risiconiveau van gebruiker

Het risiconiveau van een gebruiker wordt aangegeven (hoog, Gemiddeld of laag) van de kans op Hallo Hallo gebruikersidentiteit is aangetast. Deze wordt berekend op basis van Hallo gebruiker risico's die gekoppeld aan de identiteit van een gebruiker zijn.

Hallo status van een risicogebeurtenis is een **Active** of **gesloten**. Alleen het risico van gebeurtenissen die zijn **Active** bijdragen toohello gebruiker risico niveau berekening.

Hallo gebruiker risiconiveau wordt berekend met behulp van Hallo invoer te volgen:

* Actieve risicogebeurtenissen die invloed hebben op Hallo-gebruiker
* Risiconiveau van deze gebeurtenissen
* Hiermee wordt aangegeven of welke herstelacties zijn gemaakt

![Gebruiker risico's](./media/active-directory-identityprotection/1031.png "gebruiker risico's")

U kunt gebruiken Hallo gebruiker risico niveaus toocreate beleidsregels voor voorwaardelijke toegang die riskant gebruikers aanmelden blokkeren, of zorgen dat ze toosecurely hun wachtwoord wijzigen.

### <a name="closing-risk-events-manually"></a>Risico's handmatig sluiten

In de meeste gevallen wordt u herstelacties uitvoeren, zoals een beveiligd wachtwoord opnieuw instellen van tooautomatically sluiten risico's. Echter, dit mogelijk niet altijd mogelijk.  
Dit is, bijvoorbeeld Hallo geval, wanneer:

* Een gebruiker met actieve risicogebeurtenissen is verwijderd
* Een onderzoek blijkt dat een risicogebeurtenis gemelde heeft zijn uitvoeren door Hallo legitieme gebruiker

Omdat de risico's die zijn **Active** bijdragen toohello gebruiker risico berekening, moet u wellicht toomanually een risiconiveau verlagen door het risico's handmatig te sluiten.  
In de loop van de Hallo van onderzoek, kunt u een van deze acties toochange Hallo status van een risicogebeurtenis tootake kiezen:

![Acties](./media/active-directory-identityprotection/34.png "acties")

* **Los** - als na een risicogebeurtenis onderzoeken, u een juiste herstelactie buiten Identity Protection heeft ondernomen, en u van mening dat risico Hallo gebeurtenis overwogen worden gesloten bent, Hallo-gebeurtenis markeren als opgelost. Opgelost gebeurtenissen Hallo risico's van de gebeurtenis status tooClosed wordt ingesteld en Hallo risicogebeurtenis wordt niet langer bijdragen toouser risico.
* **Markeren als fout-positieve** -In sommige gevallen kan u een risicogebeurtenis onderzoeken en onjuist is gemarkeerd als een riskante te detecteren. Kunt u beperken Hallo aantal dergelijke instanties door Hallo risicogebeurtenis als fout-positieve markeren. Dit helpt Hallo machine learning-algoritmen tooimprove Hallo classificatie van soortgelijke gebeurtenissen in toekomstige Hallo. Hallo-status van de fout-positieve gebeurtenissen is te**gesloten** en ze worden niet meer bij te dragen toouser risico.
* **Negeren** : als u een herstelactie niet hebt gemaakt, maar wilt Hallo risico gebeurtenis toobe verwijderd uit de actieve lijst hello, kunt u een risicogebeurtenis negeren markeren en Hallo gebeurtenisstatus worden gesloten. Genegeerd gebeurtenissen bijdragen niet toouser risico. Deze optie dient alleen ongebruikelijke omstandigheden worden gebruikt.
* **Opnieuw activeren** -gebeurtenissen die handmatig zijn gesloten risico (door te kiezen **los**, **fout-positief**, of **negeren**) kan opnieuw worden geactiveerd, Hallo instellen om de gebeurtenisstatus weer te**Active**. Opnieuw geactiveerde risicogebeurtenissen bijdragen toohello gebruiker risico niveau berekening. Risico's gesloten via herstel (zoals een beveiligd wachtwoord opnieuw instellen) kunnen niet opnieuw worden geactiveerd.

**dialoogvenster tooopen Hallo-gerelateerde configuratie**:

1. Op Hallo **Azure AD Identity Protection** blade onder **onderzoeken**, klikt u op **bestaat de kans dat gebeurtenissen**.

    ![Handmatige wachtwoordherstel](./media/active-directory-identityprotection/1002.png "handmatige wachtwoord opnieuw instellen")
2. In Hallo **bestaat de kans dat gebeurtenissen** lijst, klikt u op een risico.

    ![Handmatige wachtwoordherstel](./media/active-directory-identityprotection/1003.png "handmatige wachtwoord opnieuw instellen")
3. Hallo risico blade met de rechtermuisknop op een gebruiker.

    ![Handmatige wachtwoordherstel](./media/active-directory-identityprotection/1004.png "handmatige wachtwoord opnieuw instellen")

### <a name="closing-all-risk-events-for-a-user-manually"></a>Alle gebeurtenissen van de risico's voor een gebruiker sluiten handmatig
In plaats van handmatig sluiten afzonderlijk risico's voor een gebruiker, biedt Azure Active Directory: Identity Protection u ook een methode tooclose alle gebeurtenissen voor een gebruiker met één klik.

![Acties](./media/active-directory-identityprotection/2222.png "acties")

Wanneer u klikt op **sluiten alle gebeurtenissen**, alle gebeurtenissen zijn gesloten en Hallo van invloed op een gebruiker is niet langer risico.

### <a name="remediating-user-risk-events"></a>Beveiligingsstatus gebruiker risico 's

Een herstel is een actie toosecure een identiteit of een apparaat dat eerder is verdacht of toobe bekend is geknoeid. Een herstelactie Hallo identiteit of het apparaat tooa veilige status herstelt en vorige risico's die zijn gekoppeld aan het Hallo-identiteit of het apparaat wordt omgezet.

tooremediate-gebeurtenissen voor het risico van gebruikers, kunt u:

* Een beveiligd wachtwoord opnieuw instellen van tooremediate gebruiker risicogebeurtenissen handmatig uitvoeren
* Configureren van een gebruiker risico beveiliging beleid toomitigate of risicogebeurtenissen gebruiker automatisch herstellen
* Hallo geïnfecteerd apparaat herstellen met installatiekopie  

#### <a name="manual-secure-password-reset"></a>Handmatige beveiligd wachtwoord opnieuw instellen
Een beveiligd wachtwoord opnieuw instellen is een effectieve herstel voor veel risicogebeurtenissen en wanneer uitgevoerd, sluit u deze risicogebeurtenissen automatisch en risiconiveau Hallo-gebruiker opnieuw worden berekend. U kunt Hallo Identity Protection-dashboard tooinitiate een wachtwoord opnieuw instellen voor een gebruiker riskant.

Hallo gerelateerde dialoogvenster bevat twee verschillende methoden tooreset een wachtwoord:

**Wachtwoord opnieuw instellen** : Selecteer **Hallo gebruiker tooreset hun wachtwoord vereisen** tooallow Hallo gebruiker tooself herstellen als Hallo gebruiker is geregistreerd voor multi-factor authentication. Tijdens het Hallo van de gebruiker volgende aanmelden zijn Hallo gebruiker vereist toosolve is een multi-factor authentication-vraag en vervolgens, de geforceerde toochange Hallo wachtwoord. Deze optie niet beschikbaar als Hallo gebruikersaccount nog niet is geregistreerd multi-factor authentication-server.

**Tijdelijke wachtwoord** : Selecteer **genereren van een tijdelijk wachtwoord** tooimmediately Hallo bestaande wachtwoord ongeldig te maken en een nieuw tijdelijk wachtwoord voor gebruiker Hallo maken. Hallo nieuw tijdelijk wachtwoord tooan alternatieve e-mailadres voor Hallo gebruiker of toohello Gebruikersbeheer verzenden. Omdat Hallo wachtwoord tijdelijke, Hallo gebruiker worden opgegeven na vragen aan gebruiker toochange Hallo wachtwoord bij aanmelden.

![Beleid](./media/active-directory-identityprotection/1005.png "beleid")

**dialoogvenster tooopen Hallo-gerelateerde configuratie**:

1. Op Hallo **Azure AD Identity Protection** blade, klikt u op **gebruikers die zijn gemarkeerd voor risico**.

    ![Handmatige wachtwoordherstel](./media/active-directory-identityprotection/1006.png "handmatige wachtwoord opnieuw instellen")
2. Selecteer een gebruiker met ten minste één risicogebeurtenissen in Hallo lijst van gebruikers.

    ![Handmatige wachtwoordherstel](./media/active-directory-identityprotection/1007.png "handmatige wachtwoord opnieuw instellen")
3. Klik op Hallo gebruiker blade **wachtwoord opnieuw instellen**.

    ![Handmatige wachtwoordherstel](./media/active-directory-identityprotection/1008.png "handmatige wachtwoord opnieuw instellen")

### <a name="user-risk-security-policy"></a>Gebruiker risico beveiligingsbeleid
Een beveiligingsbeleid voor gebruiker risico is een beleid voor voorwaardelijke toegang dat Hallo risico niveau tooa specifieke gebruiker wordt geëvalueerd en herstel en risicobeperking op basis van vooraf gedefinieerde voorwaarden en regels maatregelen.

![Gebruikersbeleid ridk](./media/active-directory-identityprotection/1009.png "ridk gebruikersbeleid")

Azure AD Identity Protection helpt u Hallo risicobeperking en het doorvoeren van gebruikers die zijn gemarkeerd voor risico doordat u beheren:

* Set Hallo gebruikers en groepen Hallo beleid van toepassing op:

    ![Gebruikersbeleid ridk](./media/active-directory-identityprotection/1010.png "ridk gebruikersbeleid")
* Hallo gebruiker risico niveau drempelwaarde (laag, Gemiddeld of hoog) die Hallo beleid activeert instellen:

    ![Gebruikersbeleid ridk](./media/active-directory-identityprotection/1011.png "ridk gebruikersbeleid")
* Set Hallo besturingselementen toobe afgedwongen als het Hallo-beleid wordt geactiveerd:

    ![Gebruikersbeleid ridk](./media/active-directory-identityprotection/1012.png "ridk gebruikersbeleid")
* Hallo-status van uw beleid switch:

    ![Gebruikersbeleid ridk](./media/active-directory-identityprotection/403.png "registratieprocedure voor MFA")
* Bekijken en evalueren Hallo gevolgen van een wijziging voordat u deze activeert:

    ![Gebruikersbeleid ridk](./media/active-directory-identityprotection/1013.png "ridk gebruikersbeleid")

U kiest een **hoge** drempelwaarde vermindert het aantal keren dat een beleid wordt geactiveerd en minimaliseert Hallo impact toousers Hallo.
Echter, worden uitgesloten **laag** en **gemiddeld** gebruikers die zijn gemarkeerd voor kwetsbaar voor aanvallen via Hallo-beleid kan niet worden beveiligd identiteiten of apparaten die eerder zijn verdachte of bekend toobe aangetast.

Wanneer de instelling beleid Hallo

* Voorkomen dat gebruikers die waarschijnlijk toogenerate veel ONWAAR-positieven (ontwikkelaars, beveiligingsanalisten zijn)
* Gebruikers in landen waar inschakelen Hallo beleid is het niet praktisch uitsluiten (bijvoorbeeld geen toohelpdesk toegang)
* Gebruik een **hoge** drempelwaarde tijdens de eerste beleid implementeert, of als u uitdagingen die zichtbaar zijn voor eindgebruikers minimaliseert.
* Gebruik een **laag** drempelwaarde als uw organisatie betere beveiliging vereist. Als u een **laag** drempelwaarde introduceert extra gebruiker aanmelden uitdagingen, maar een hogere beveiliging.

Hallo standaard aanbevolen voor de meeste organisaties tooconfigure is een regel voor een **gemiddeld** drempelwaarde toostrike een balans tussen bruikbaarheid en veiligheid.

Voor een overzicht van Hallo gerelateerde gebruikerservaring, Zie:

* [Account recovery stroom geknoeid](active-directory-identityprotection-flows.md#compromised-account-recovery).  
* [Account geblokkeerd stroom geknoeid](active-directory-identityprotection-flows.md#compromised-account-blocked).  

**dialoogvenster tooopen Hallo-gerelateerde configuratie**:

- Op Hallo **Azure AD Identity Protection** blade in Hallo **configureren** sectie, klikt u op **risico gebruikersbeleid**.

    ![Gebruikersbeleid ridk](./media/active-directory-identityprotection/1009.png "ridk gebruikersbeleid")

### <a name="mitigating-user-risk-events"></a>Beperkende gebruiker risico 's
Beheerders kunnen een gebruiker risico beveiliging beleid tooblock gebruikers bij het aanmelden, afhankelijk van het risiconiveau Hallo instellen.

Een aanmeldingspagina blokkeren:

* Voorkomt dat Hallo genereren van de nieuwe gebruiker risicogebeurtenissen voor Hallo van invloed op een gebruiker
* Hiermee beheerders toomanually hello risicogebeurtenissen die invloed hebben op Hallo gebruikersidentiteit herstellen en herstel hem tooa beveiligde status



## <a name="multi-factor-authentication-registration-policy"></a>Registratiebeleid voor meervoudige verificatie
Azure multi-factor authentication-server is een methode om te controleren wie u bent die Hallo gebruik van meer dan alleen een gebruikersnaam en wachtwoord vereist. Het biedt een tweede beveiligingslaag beveiliging toouser aanmeldingen en transacties.  
We raden u aan Azure multi-factor authentication-server voor de gebruikersaanmeldingen omdat deze:

* Biedt geavanceerde verificatie met een bereik van eenvoudige verificatie-opties
* Speelt een belangrijke rol bij het voorbereiden van uw organisatie tooprotect en herstellen van account compromissen

![Gebruikersbeleid ridk](./media/active-directory-identityprotection/1019.png "ridk gebruikersbeleid")

Zie voor meer informatie [wat is Azure multi-factor Authentication?](../multi-factor-authentication/multi-factor-authentication.md)

Azure AD Identity Protection helpt u Hallo uitrollen van multi-factor authentication-registratie beheren door een beleid waarmee u kunt configureren:

* Set Hallo gebruikers en groepen Hallo beleid van toepassing op:

    ![MFA-beleid](./media/active-directory-identityprotection/1020.png "MFA-beleid")
* Set Hallo besturingselementen toobe afgedwongen wanneer Hallo beleid activeert::  

    ![MFA-beleid](./media/active-directory-identityprotection/1021.png "MFA-beleid")
* Hallo-status van uw beleid switch:

    ![MFA-beleid](./media/active-directory-identityprotection/403.png "MFA-beleid")
* Status van huidige registratie Hallo weergeven:

    ![MFA-beleid](./media/active-directory-identityprotection/1022.png "MFA-beleid")

Voor een overzicht van Hallo gerelateerde gebruikerservaring, Zie:

* [Registratie voor meervoudige authenticatiestroom](active-directory-identityprotection-flows.md#multi-factor-authentication-registration).  
* [Aanmelden-ervaringen met Azure AD Identity Protection](active-directory-identityprotection-flows.md).  

**dialoogvenster tooopen Hallo-gerelateerde configuratie**:

- Op Hallo **Azure AD Identity Protection** blade in Hallo **configureren** sectie, klikt u op **multi-factor authentication-registratie**.

    ![MFA-beleid](./media/active-directory-identityprotection/1019.png "MFA-beleid")

## <a name="next-steps"></a>Volgende stappen
* [Channel 9: Azure AD en Identity weergeven: Identity Protection Preview](https://channel9.msdn.com/Series/Azure-AD-Identity/Azure-AD-and-Identity-Show-Identity-Protection-Preview)

* [Inschakelen van beveiliging voor Azure Active Directory-identiteit](active-directory-identityprotection-enable.md)

* [Beveiligingsproblemen die worden gedetecteerd door Azure Active Directory: Identity Protection](active-directory-identityprotection-vulnerabilities.md)

* [Azure Active Directory-risicogebeurtenissen](active-directory-identity-protection-risk-events.md)

* [Azure Active Directory: Identity Protection-meldingen](active-directory-identityprotection-notifications.md)

* [Playbook voor Azure Active Directory: Identity Protection](active-directory-identityprotection-playbook.md)

* [Azure Active Directory: Identity Protection verklarende woordenlijst](active-directory-identityprotection-glossary.md)

* [Aanmelden-ervaring met Azure AD Identity Protection](active-directory-identityprotection-flows.md)

* [Azure Active Directory: Identity Protection - hoe toounblock gebruikers](active-directory-identityprotection-unblock-howto.md)

* [Aan de slag met Azure Active Directory: Identity Protection en Microsoft Graph](active-directory-identityprotection-graph-getting-started.md)

---
title: 'Veelgestelde vragen over: Azure AD SSPR | Microsoft Docs'
description: Veelgestelde vragen over Azure AD zelf uw wachtwoord opnieuw instellen
services: active-directory
keywords: Wachtwoordbeheer Active directory, wachtwoordbeheer, Azure AD self service voor wachtwoordherstel
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.reviewer: gahug
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: joflore
ms.custom: it-pro
ms.openlocfilehash: d04a9efeb3b35421aa605cadb2aa25f656a4d515
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="password-management-frequently-asked-questions"></a>Veelgestelde vragen over wachtwoordbeheer

Hallo na worden enkele veelgestelde vragen voor alle bewerkingen die betrekking hebben toopassword opnieuw instellen.

Als er een algemene vraag over Azure AD en zelf uw wachtwoord opnieuw instellen, die niet wordt beantwoord hier, kunt u vragen Hallo community om hulp op Hallo [Azure Ad-forums](https://social.msdn.microsoft.com/Forums/en-US/home?forum=WindowsAzureAD). Leden van de community Hallo opnemen Engineers, Product Managers, MVP's en fellow IT-Professionals.

Deze Veelgestelde vragen opgesplitst Hallo uit te voeren:

* [**Vragen over het registreren voor wachtwoord opnieuw instellen**](#password-reset-registration)
* [**Vragen over wachtwoordherstel**](#password-reset)
* [**Vragen over het wijzigen van wachtwoorden**](#password-change)
* [**Rapporten voor vragen over wachtwoordbeheer**](#password-management-reports)
* [**Vragen over Write-back van wachtwoord**](#password-writeback)

## <a name="password-reset-registration"></a>Registratie voor wachtwoord opnieuw instellen
* **V: kunnen mijn gebruikers registreren hun eigen wachtwoord opnieuw instellen van gegevens?**

  > **A:** Ja, zoals wachtwoord opnieuw instellen is ingeschakeld en worden ze in licentie gegeven, kunnen ze toohello registratie voor wachtwoord opnieuw instellen-portal op http://aka.ms/ssprsetup tooregister hun verificatiegegevens. Gebruikers kunnen ook registreren door toohello-Toegangsvenster gaan bij http://myapps.microsoft.com, tabblad Hallo-profiel en Hallo registreren voor wachtwoordherstel optie klikken.
  >
  >
* **V: kan ik wachtwoord opnieuw instellen van gegevens definiëren namens mijn gebruikers?**

  > **A:** Ja, u kunt dit doen met Azure AD Connect PowerShell Hallo [Azure-portal](https://portal.azure.com), of Hallo beheerder van Office-portal. Zie voor meer informatie artikel Hallo [gegevens die worden gebruikt door Azure AD selfservice voor wachtwoordherstel](active-directory-passwords-data.md).
  >
  >
* **V: kan ik gegevens voor vragen over de beveiliging van on-premises synchroniseren?**

  > **A:** dit niet mogelijk is vandaag de dag.
  >
  >
* **V: kunnen mijn gebruikers gegevens registreren zodanig dat deze gegevens door andere gebruikers niet zien?**

  > **A:** Ja, wanneer gebruikers zich registreren voor gegevens met behulp van Hallo opnieuw instellen-Portal voor Wachtwoordregistratie is opgeslagen in persoonlijke verificatie velden die alleen zichtbaar zijn door de gebruiker globale beheerders en Hallo.
    >
    > [!NOTE]
    > Als een **Azure Administrator-account** registreert hun telefoonnummer verificatie deze ook worden ingevuld in het veld van de mobiele telefoon Hallo en zichtbaar is.
    >
  >
  >
* **V: Mijn gebruikers hebt toobe geregistreerd voordat ze kunnen voor wachtwoordherstel gebruiken?**

  > **A:** Nee, als u onvoldoende verificatiegegevens namens hen definieert, gebruikers hebben geen tooregister. Wachtwoord opnieuw moet worden ingesteld als u hebt opgeslagen gegevens in de juiste velden in de map Hallo Hallo juist opgemaakt.
  >
  >
* **V: kan ik synchroniseren of instellen van de telefoon voor authenticatie, authenticatie E-mail of andere telefoon voor authenticatie velden Hallo namens mijn gebruikers?**

  > **A:** dit niet mogelijk is vandaag de dag.
  >
  >
* **V: hoe Hallo-portal voor wachtwoordregistratie weet welke opties tooshow Mijn gebruikers?**

  > **A:** Hallo wachtwoordherstel registratieportal alleen toont Hallo opties die u hebt ingeschakeld voor uw gebruikers. Deze opties zijn gevonden onder de sectie van de gebruiker opnieuw instellen wachtwoordbeleid van uw directory configureren tabblad Hallo. Dit betekent bijvoorbeeld dat als u vragen over de beveiliging niet inschakelt, klikt u vervolgens gebruikers zich niet kunnen tooregister voor die optie.
  >
  >
* **V: wanneer een gebruiker als beschouwd ingeschreven?**

  > **A:** een gebruiker wordt beschouwd geregistreerd voor SSPR, wanneer zij hebben geregistreerd ten minste Hallo **aantal methoden vereist tooreset** die u hebt ingesteld in Hallo [Azure-portal](https://portal.azure.com).
  >
  >
## <a name="password-reset"></a>Wachtwoord opnieuw instellen
* **V: hoe lang moet ik tooreceive wachten een e-mail, SMS of telefoongesprek van wachtwoord opnieuw instellen?**

  > **A:** SMS-berichten, e-mailadres en telefoongesprekken moet binnenkomen in onder één minuut aan normale Hallo-aanvraag wordt 5-20 seconden.
    >Als u hiervan geen melding voor Hallo binnen deze tijd:
        > * Controleer de map Ongewenste e-mail.
        > * Hallo nummer of e-mailbericht waarmee contact wordt opgenomen is Hallo een die u verwacht.
        > * Controleer Hallo verificatiegegevens in de directory Hallo is juist opgemaakt.
                >     * Voorbeeld: "+ 1 4255551234' of 'user@contoso.com'
  >
  >
* **V: welke talen worden ondersteund door het wachtwoord opnieuw instellen?**

  > **A:** Hallo wachtwoordherstel gebruikersinterface SMS-berichten en stem aanroepen zijn gelokaliseerd in Hallo dezelfde talen die worden ondersteund in Office 365.
  >
  >
* **V: welke onderdelen van Hallo wachtwoord opnieuw instellen van ervaring ophalen huisstijl wanneer ik ingesteld organisatie huisstijl in mijn directory het tabblad configureren?**

  > **A:** hello wachtwoordresetportal ziet u het logo van uw organisatie en kunt u tooconfigure Hallo Neem contact op met uw beheerder koppeling toopoint tooa aangepaste e-mailadres of URL. Een e-mailbericht dat wordt verzonden door het wachtwoord opnieuw instellen van uw organisatie logo, de kleuren, de naam bevat in Hallo hoofdtekst van e-mail Hallo en aangepast met de naam van.
  >
  >
* **V: hoe kan ik mijn moet u gebruikers informeren over waar toogo tooreset hun wachtwoorden?**

  > **A:** kunt u uw gebruikers toohttps://passwordreset.microsoftonline.com rechtstreeks verzenden, of u kunt opgeven dat ze tooclick hello **heeft geen toegang tot uw accountkoppeling** gevonden op eventuele werk of School-aanmeldingspagina. U kunt deze koppelingen ook publiceren in een plaats eenvoudig toegankelijk tooyour gebruikers.
  >
  >
* **V: kan ik deze pagina vanaf een mobiel apparaat gebruiken?**

  > **A:** Ja, deze pagina werkt op mobiele apparaten.
  >
  >
* **V: ondersteund ontgrendelen lokale active directory-accounts wanneer gebruikers hun wachtwoord opnieuw instellen?**

  > **A:** Ja, als hun wachtwoord opnieuw instellen van een gebruiker en wachtwoord terugschrijven is geïmplementeerd met Azure AD Connect, die gebruikersaccount is automatisch ontgrendeld wanneer ze hun wachtwoord opnieuw instellen.
  >
  >
* **V: hoe kan ik wachtwoordherstel rechtstreeks in mijn gebruiker aanmelden Bureaubladervaring worden geïntegreerd?**

  > **A:** als u een Azure AD Premium-klant bent, kunt u Microsoft Identity Manager installeren zonder extra kosten en implementeren van Hallo lokale wachtwoord opnieuw instellen van oplossing toomeet deze vereiste.
  >
  >
* **V: kan ik andere beveiligingsvragen voor verschillende talen instellen?**

  > **A:** dit niet mogelijk is vandaag de dag.
  >
  >
* **V: hoe zoveel mogelijk vragen kunt we voor Hallo beveiligingsvragen verificatieoptie configureren?**

  > **A:** kunt u aangepaste beveiligingsvragen too20 in Hallo [Azure-portal](https://portal.azure.com).
  >
  >
* **V: hoe lang mogelijk beveiligingsvragen?**

  > **A:** beveiligingsvragen mogelijk tussen 3 en 200 tekens bevatten.
  >
  >
* **V: hoe lang mogelijk antwoorden toosecurity vragen?**

  > **A:** antwoorden mogelijk 3 too40 tekens lang zijn.
  >
  >
* **V: zijn afgewezen dubbele antwoorden toosecurity vragen?**

  > **A:** Ja, er dubbele antwoorden toosecurity vragen afwijzen.
  >
  >
* **V: kan Hallo het registreren van een gebruiker dezelfde beveiligingsvraag het meer dan één keer?**

  > **A:** Nee, wanneer een gebruiker zich registreert voor een bepaald criterium, ze kunnen niet worden geregistreerd voor deze vraag een tweede keer.
  >
  >
* **V: is het mogelijk tooset de ondergrens van beveiligingsvragen voor registratie en opnieuw instellen?**

  > **A:** Ja, een limiet kan worden ingesteld voor registratie en een andere voor het opnieuw instellen. 3-5-beveiligingsvragen mogelijk zijn vereist voor inschrijving en 3-5 mogelijk zijn vereist voor opnieuw instellen.
  >
  >
* **V: als een gebruiker meer dan het maximum aantal vragen vereist tooreset Hallo is geregistreerd, hoe beveiligingsvragen geselecteerd tijdens het opnieuw instellen?**

  > **A:** N beveiliging vragen willekeurig geselecteerd uit Hallo kunt u het totaal aantal vragen een gebruiker is geregistreerd, waarbij N staat voor Hallo **aantal vragen vereist tooreset**. Bijvoorbeeld, als een gebruiker 5 beveiligingsvragen geregistreerd heeft, maar alleen 3 vereiste tooreset zijn, zijn 3 Hallo 5 willekeurig geselecteerd en gepresenteerd op opnieuw instellen. Als het Hallo-gebruiker afkomstig Hallo-antwoorden toohello vragen verkeerde, optreedt Hallo selectieproces tooprevent vraag hammering.
  >
  >
* **V: heb u voorkomen dat gebruikers vaak in een korte periode voor wachtwoordherstel probeert?**

  > **A:** Ja, er zijn ingebouwd in het wachtwoord opnieuw instellen van tooprotect tegen misbruik beveiligingsfuncties. Gebruikers kunnen alleen proberen opnieuw instellen van 5 wachtwoordpogingen binnen een uur voordat ze worden geblokkeerd voor 24 uur. Gebruikers kunnen toovalidate een telefoonnummer alleen proberen 5 maal binnen een uur voordat ze worden geblokkeerd voor 24 uur. Gebruikers kunnen alleen een één verificatiemethode proberen 5 maal binnen een uur voordat ze worden geblokkeerd voor 24 uur.
  >
  >
* **V: voor hoe lang Hallo e-mail en SMS eenmalige wachtwoordcode geldig zijn?**

  > **A:** Hallo levensduur van de sessie voor wachtwoordherstel is 105 minuten. Vanaf Hallo Hallo wachtwoordherstel bewerking, Hallo gebruiker 105 minuten tooreset hun wachtwoord heeft. Hallo zijn e-mail en SMS eenmalige wachtwoordcode ongeldig nadat deze periode is verstreken.
  >
  >

## <a name="password-change"></a>Wachtwoord wijzigen
* **V: waar moeten Mijn gebruikers gaan toochange hun wachtwoorden?**

  > **A:** gebruikers kunnen hun wachtwoord wijzigen waar ze hun profielfoto of pictogram ziet (zoals in Hallo rechterbovenhoek van hun [Office 365](https://portal.office.com) of [Toegangspaneel](https://myapps.microsoft.com) optreedt. Gebruikers kunnen hun wachtwoord wijzigen vanaf Hallo [Toegangspaneel profielpagina](https://account.activedirectory.windowsazure.com/r#/profile). Gebruikers kunnen ook worden toochange gevraagd hun wachtwoord automatisch hello Azure AD in het scherm als hun wachtwoord is verlopen. Ten slotte gebruikers toohello kunnen navigeren [Azure AD-wachtwoord wijzigen Portal](https://account.activedirectory.windowsazure.com/ChangePassword.aspx) rechtstreeks desgewenst toochange hun wachtwoorden.
  >
  >
* **V: kunnen mijn gebruikers worden gewaarschuwd in Office-Portal Hallo wanneer hun on-premises wachtwoord is verlopen?**

  > **A:** dit vandaag is mogelijk als u van AD FS gebruikmaakt door hier Hallo-instructies te volgen: [wachtwoord beleid Claims verzenden met AD FS](https://technet.microsoft.com/windows-server-docs/identity/ad-fs/operations/configure-ad-fs-to-send-password-expiry-claims?f=255&MSPPError=-2147217396). Als u synchronisatie van wachtwoordhash, is dit niet mogelijk vandaag. Dit is omdat we synchroniseert geen wachtwoordbeleid van on-premises, zodat het is niet mogelijk voor ons toopost verlopen-meldingen toocloud optreedt. In beide gevallen is het ook mogelijk te[Waarschuw gebruikers waarvan de wachtwoorden over tooexpire worden met behulp van PowerShell](https://social.technet.microsoft.com/wiki/contents/articles/23313.notify-active-directory-users-about-password-expiry-using-powershell.aspx).
  >
  >

## <a name="password-management-reports"></a>Wachtwoord-rapporten
* **V: hoe lang duurt het voor gegevens tooshow up op Hallo wachtwoord-rapporten?**

  > **A:** gegevens op Hallo wachtwoord-rapporten moet worden weergegeven in 5-10 minuten. Het aantal exemplaren het tooappear van tooan uur kan duren.
  >
  >
* **V: hoe kan ik Hallo wachtwoord-rapporten filteren?**

  > **A:** kunt u Hallo wachtwoord-rapporten filteren op Hallo kleine Vergrootglas toohello uiterst rechts van de kolomlabels hello, aan de bovenkant Hallo van Hallo-rapport te klikken. Als u toodo uitgebreidere filteren wilt, kunt u downloaden Hallo rapport tooexcel en een draaitabel maken.
  >
  >
* **V: wat Hallo kunt u het maximum aantal gebeurtenissen is in Hallo wachtwoord-rapporten worden opgeslagen?**

  > **A:** Up too75, 000 wachtwoord opnieuw instellen of het wachtwoord opnieuw instellen van registratie gebeurtenissen worden opgeslagen in Hallo wachtwoord-rapporten, maakt u een back-up van too30 dagen-spanning.  We werken tooexpand dit nummer tooinclude meer gebeurtenissen.
  >
  >
* **V: hoe ver terug Hallo wachtwoord-rapporten gaan?**

  > **A:** Hallo wachtwoordbeheer rapporten weergeven bewerkingen plaatsvinden binnen Hallo afgelopen 30 dagen. Op dit moment als u deze gegevens tooarchive moet kunt u downloaden Hallo rapporten periodiek en deze opslaan op een andere locatie.
  >
  >
* **V: is er een maximale aantal rijen dat kan worden weergegeven op Hallo wachtwoord-rapporten?**

  > **A:** Ja, maximaal 75.000 rijen kan worden weergegeven op een van de Hallo wachtwoord-rapporten of worden ze weergegeven Hallo UI of wordt gedownload.
  >
  >
* **V: is er een API-tooaccess Hallo wachtwoord opnieuw instellen of registratie rapportagegegevens?**

  > **A:** Ja, Zie Hallo na documentatie toolearn reporting gegevensstroom hoe u toegang hebt tot Hallo-wachtwoord instellen.  [Meer informatie over hoe tooaccess wachtwoordherstel rapportagegebeurtenissen programmatisch](https://msdn.microsoft.com/library/azure/mt126081.aspx#BKMK_SsprActivityEvent).
  >
  >

## <a name="password-writeback"></a>Wachtwoord terugschrijven
* **V: hoe werkt wachtwoord terugschrijven achter de schermen Hallo?**

  > **A:** Zie [de werking van wachtwoord terugschrijven](active-directory-passwords-writeback.md) voor een uitleg van wat er gebeurt als u terugschrijven van wachtwoord en hoe gegevens loopt via Hallo systeem terug naar uw on-premises-omgeving inschakelen.
  >
  >
* **V: hoe lang duurt wachtwoord terugschrijven toowork  Is er een vertraging synchronisatie zoals met wachtwoordhashsynchronisatie?**

  > **A:** wachtwoord terugschrijven is snel. Het is een synchrone pijplijn die fundamenteel anders dan de synchronisatie van wachtwoordhash werkt. Wachtwoord terugschrijven kan gebruikers tooget realtime feedback over geslaagde Hallo van hun wachtwoord opnieuw instellen of wijzigen van de bewerking. Hallo gemiddelde tijd voor een geslaagde write-back van een wachtwoord is onder 500 ms.
  >
  >
* **V: hoe wordt mijn account/toegang tot de cloud getroffen als mijn lokale account is uitgeschakeld?**

  > **A:** als uw lokale ID is uitgeschakeld, uw cloud-ID/access worden ook uitgeschakeld op de volgende synchronisatie-interval Hallo via AAD Connect byt standaard is dit elke 30 minuten.
  >
  >
* **V: als mijn lokale account wordt beperkt door een beleid on-premises Active Directory-wachtwoord, houdt SSPR zich aan dit beleid wanneer ik Hallo wachtwoord wijzigen?**

  > **A:** Ja, SSPR is afhankelijk van en houdt zich aan Hallo lokale AD-wachtwoordbeleid, met inbegrip van AD-domein wachtwoord standaardbeleid, evenals alle gedefinieerde fijnmazige wachtwoordbeleid gericht tooa toegekend.
  >
  >
* **V: wat typen accounts werkt wachtwoord terugschrijven voor?**

  > **A:** wachtwoord terugschrijven is geschikt voor gebruikers van federatieve en het wachtwoord-Hash gesynchroniseerd.
  >
  >
* **V: bevat wachtwoord terugschrijven mijn domein wachtwoordbeleid afdwingen?**

  > **A:** Ja, wachtwoord terugschrijven worden afgedwongen wachtwoord leeftijd, geschiedenis, complexiteit, filters en eventuele andere beperkingen die u in plaats van wachtwoorden in uw lokale domein kan plaatsen.
  >
  >
* **V: wachtwoord terugschrijven veilig is?  Hoe kan ik dat ik won't ingebroken zijn?**

  > **A:** Ja, Write-back van wachtwoord is beveiligd. tooread meer informatie over Hallo vier beveiligingslagen die door Hallo wachtwoord terugschrijven service is geïmplementeerd, bekijk Hallo [wachtwoord terugschrijven beveiligingsmodel](active-directory-passwords-writeback.md#password-writeback-security-model) sectie in de werking van wachtwoord terugschrijven.
  >
  >

## <a name="next-steps"></a>Volgende stappen

Hallo volgende koppelingen vindt u aanvullende informatie met betrekking tot het wachtwoord opnieuw instellen met behulp van Azure AD

* [**Snel starten**](active-directory-passwords-getting-started.md): aan de slag met self-service wachtwoordbeheer van Azure AD 
* [**Licentieverlening**](active-directory-passwords-licensing.md): uw Azure AD-licentieverlening configureren
* [**Gegevens** ](active-directory-passwords-data.md) - begrijpen Hallo-gegevens die nodig is en hoe deze wordt gebruikt voor wachtwoordbeheer
* [**Implementatie** ](active-directory-passwords-best-practices.md) -plannen en implementeren van SSPR tooyour gebruikers via Hallo richtlijnen hier gevonden
* [**Aanpassen** ](active-directory-passwords-customize.md) -Hallo uiterlijk Hallo SSPR ervaring voor uw bedrijf aanpassen.
* [**Rapportage**](active-directory-passwords-reporting.md): detecteren of, waar en wanneer uw gebruikers de functionaliteit voor self-service voor wachtwoordherstel gebruiken
* [**Beleid**](active-directory-passwords-policy.md): Azure AD-wachtwoordbeleid begrijpen en instellen
* [**Write-back van wachtwoord**](active-directory-passwords-writeback.md): hoe werkt write-back van wachtwoord met uw on-premises directory
* [**Technische diepgaand** ](active-directory-passwords-how-it-works.md) -Ga achter Hallo gordijn toounderstand hoe het werkt
* [**Problemen met** ](active-directory-passwords-troubleshoot.md) -informatie over hoe tooresolve algemene problemen zien we met SSPR

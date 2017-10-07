---
title: 'Azure AD Connect: Apparaat terugschrijven inschakelen | Microsoft Docs'
description: Dit document details hoe tooenable apparaat terugschrijven met Azure AD Connect
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: curtand
ms.assetid: c0ff679c-7ed5-4d6e-ac6c-b2b6392e7892
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 2566a514137fed85b21929207cf3230e6878ebbe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-enabling-device-writeback"></a>Azure AD Connect: Apparaat terugschrijven inschakelen
> [!NOTE]
> Een abonnement tooAzure AD Premium is vereist voor write-back van apparaat.
> 
> 

Hallo volgende documentatie bevat informatie over hoe tooenable Hallo apparaat terugschrijven functie in Azure AD Connect. Write-back van apparaat wordt gebruikt in Hallo volgen scenario's:

* Inschakelen van voorwaardelijke toegang op basis van apparaten tooADFS (2012 R2 of hoger) beveiligde toepassingen (relying partyvertrouwensrelaties).

Dit biedt extra beveiliging en zekerheid dat de toegang tot tooapplications krijgt alleen tootrusted apparaten. Zie voor meer informatie over voorwaardelijke toegang [risico beheren met voorwaardelijke toegang](../active-directory-conditional-access.md) en [instellen van On-premises voorwaardelijke toegang met behulp van Azure Active Directory-apparaatregistratie](../active-directory-conditional-access-automatic-device-registration-setup.md).

> [!IMPORTANT]
> <li>Apparaten moeten zich in dezelfde als gebruikers Hallo forest Hallo. Omdat apparaten moeten worden teruggeschreven tooa één forest, ondersteunt deze functie momenteel geen een implementatie met meerdere forests van de gebruiker.</li>
> <li>Slechts één apparaat registratie configuration-object kan worden toegevoegd als toohello lokale Active Directory-forest. Deze functie is niet compatibel met een topologie waarbij Hallo lokale Active Directory is gesynchroniseerde toomultiple Azure AD-mappen.</li>> 

## <a name="part-1-install-azure-ad-connect"></a>Deel 1: Installeer Azure AD Connect
1. Installeer Azure AD Connect met aangepaste of snelle instellingen. Microsoft raadt aan toostart met alle gebruikers en groepen die zijn gesynchroniseerd voordat u Write-back van apparaat inschakelt.

## <a name="part-2-prepare-active-directory"></a>Deel 2: Active Directory voorbereiden
Gebruik hello tooprepare voor het gebruik van apparaat terugschrijven stappen te volgen.

1. Start PowerShell met verhoogde bevoegdheid op Hallo machine waarop Azure AD Connect is geïnstalleerd.
2. Als Hallo Active Directory PowerShell-module niet is geïnstalleerd, installeert u met behulp van de volgende opdracht Hallo:
   
   `Add-WindowsFeature RSAT-AD-PowerShell`
3. Als hello Azure Active Directory PowerShell-module is niet geïnstalleerd, download en installeer vervolgens uit [Azure Active Directory-Module voor Windows PowerShell (64-bits versie)](http://go.microsoft.com/fwlink/p/?linkid=236297). Dit onderdeel heeft een afhankelijkheid op Hallo-aanmeldhulp, die met Azure AD Connect is geïnstalleerd.
4. Met enterprise-beheerdersreferenties, Hallo volgende opdrachten uitvoeren en sluit vervolgens af PowerShell.
   
   `Import-Module 'C:\Program Files\Microsoft Azure Active Directory Connect\AdPrep\AdSyncPrep.psm1'`
   
   `Initialize-ADSyncDeviceWriteback {Optional:–DomainName [name] Optional:-AdConnectorAccount [account]}`

Enterprise-beheerdersreferenties zijn vereist, omdat wijzigingen toohello configuratie naamruimte zijn vereist. De domeinbeheerder van een heeft niet voldoende machtigingen.

![PowerShell voor het apparaat terugschrijven inschakelen](./media/active-directory-aadconnect-feature-device-writeback/powershell.png)

Beschrijving:

* Als ze niet al bestaat, maakt en configureert u de nieuwe containers en objecten onder CN = configuratie van apparaatregistratie, CN = Services, CN = configuratie, [forest-dn].
* Als ze niet al bestaat, maakt en configureert u de nieuwe containers en objecten onder CN = Geregistreerdeapparaten, [domein-dn]. Apparaatobjecten wordt gemaakt in deze container.
* Benodigde machtigingen ingesteld op Hallo Azure AD-Connector-account toomanage apparaten in uw Active Directory.
* Hoeft slechts toorun op één forest, zelfs als Azure AD Connect wordt geïnstalleerd op meerdere forests.

Parameters:

* Domeinnaam: Active Directory-domein waar apparaatobjecten wordt gemaakt. Opmerking: Alle apparaten voor een opgegeven Active Directory-forest worden gemaakt in één domein.
* AdConnectorAccount: Active Directory-account dat wordt gebruikt door Azure AD Connect toomanage objecten in Hallo-directory. Dit is gebruikt door Azure AD Connect-synchronisatie tooconnect tooAD Hallo-account. Als u met expresinstellingen hebt geïnstalleerd, is het Hallo-account voorafgegaan door MSOL_.

## <a name="part-3-enable-device-writeback-in-azure-ad-connect"></a>Deel 3: Schakel apparaat terugschrijven in Azure AD Connect
Gebruik hello te volgen procedure tooenable apparaat terugschrijven in Azure AD Connect.

1. Hallo-installatiewizard opnieuw uitvoeren. Selecteer **aanpassen Synchronisatieopties** van aanvullende taken Hallo pagina en klik op **volgende**.
   ![Aangepaste installatie aanpassen synchronisatie-opties](./media/active-directory-aadconnect-feature-device-writeback/devicewriteback2.png)
2. Hallo optionele functies pagina Write-back van apparaat wordt niet meer worden lichter gekleurd weergegeven. Houd er rekening mee dat als hello Azure AD Connect prep stappen niet zijn voltooid Write-back van apparaat af op Hallo optionele functies pagina wordt beschikbaar. Hallo selectievakje voor write-back van apparaat en klikt u op **volgende**. Als u nog steeds Hallo selectievakje is uitgeschakeld, raadpleegt u Hallo [sectie troubleshooting](#the-writeback-checkbox-is-still-disabled).
   ![Aangepaste installatie optionele functies voor write-back van apparaat](./media/active-directory-aadconnect-feature-device-writeback/devicewriteback3.png)
3. Op Hallo Write-back-pagina ziet u als Hallo standaard apparaat terugschrijven forest Hallo opgegeven domein.
   ![Aangepaste installatie Write-back van apparaat doelforest](./media/active-directory-aadconnect-feature-device-writeback/devicewriteback4.png)
4. Hallo-installatie van de Wizard Hallo zonder aanvullende configuratiewijzigingen voltooid. Indien nodig, te verwijzen[aangepaste installatie van Azure AD Connect.](active-directory-aadconnect-get-started-custom.md)

## <a name="enable-conditional-access"></a>Voorwaardelijke toegang inschakelen (Engelstalig artikel)
Gedetailleerde instructies tooenable dit scenario zijn beschikbaar binnen [instellen van On-premises voorwaardelijke toegang met behulp van Azure Active Directory-apparaatregistratie](../active-directory-conditional-access-automatic-device-registration-setup.md).

## <a name="verify-devices-are-synchronized-tooactive-directory"></a>Controleer of de dat apparaten zijn gesynchroniseerd tooActive Directory
Apparaat terugschrijven moet nu goed werkt. Let erop dat het apparaat objecten toobe geschreven back tooAD too3 uur kan duren.  tooverify dat uw apparaten naar behoren zijn gesynchroniseerde Hallo volgen nadat Hallo sync regels hebt voltooid:

1. Start Active Directory-beheercentrum.
2. Vouw Geregistreerdeapparaten, binnen het Hallo-domein dat federated is.
   ![Active Directory-beheercentrum ingeschreven apparaten](./media/active-directory-aadconnect-feature-device-writeback/devicewriteback5.png)
3. Huidige geregistreerde apparaten worden er weergegeven.
   ![Active Directory-beheercentrum lijst met apparaten geregistreerd](./media/active-directory-aadconnect-feature-device-writeback/devicewriteback6.png)

## <a name="troubleshooting"></a>Problemen oplossen
### <a name="hello-writeback-checkbox-is-still-disabled"></a>Hallo Write-back van selectievakje is nog steeds uitgeschakeld
Als het selectievakje Hallo voor write-back van apparaat niet is ingeschakeld, hoewel u Hallo de bovenstaande stappen hebt gevolgd Hallo stappen te volgen helpt u bij de installatie van welke Hallo wizard controleert voordat Hallo selectievakje is ingeschakeld.

Eerste dingen eerste:

* Zorg ervoor dat ten minste één forest Windows Server 2012R2. Hallo apparaat objecttype moet aanwezig zijn.
* Als het Hallo-installatiewizard wordt al uitgevoerd en vervolgens wijzigingen niet gedetecteerd. In dit geval Hallo-installatiewizard voltooien en voer dit opnieuw.
* Zorg ervoor dat Hallo-account die u in Hallo Initialisatiescript opgeeft daadwerkelijk Hallo juiste gebruiker door Hallo Active Directory-Connector gebruikt. tooverify dit als volgt te werk:
  * Open in het menu start Hallo **synchronisatieservice**.
  * Open Hallo **Connectors** tabblad.
  * Hallo Connector met het type Active Directory Domain Services zoeken en te selecteren.
  * Onder **acties**, selecteer **eigenschappen**.
  * Ga te**tooActive Directory-Forest verbinding**. Controleer of u die Hallo-domein en gebruikersnaam naam zijn opgegeven op dit scherm overeen Hallo opgegeven account toohello script.
    ![Connector-account in Sync Service Manager](./media/active-directory-aadconnect-feature-device-writeback/connectoraccount.png)

Controleer of de configuratie in Active Directory:

* Controleren of deze Hallo Device Registration Service bevindt zich in de onderstaande Hallo locatie (CN DeviceRegistrationService, CN = apparaat registratie Services, CN = configuratie van apparaatregistratie, CN = Services, CN = = Configuration) onder de configuratienaamgevingscontext.

![Oplossen, DeviceRegistrationService in de naamruimte van de configuratie](./media/active-directory-aadconnect-feature-device-writeback/troubleshoot1.png)

* Controleer of er is slechts één configuratieobject door te zoeken naar Hallo configuratie naamruimte. Als er meer dan één, verwijderen Hallo duplicaat.

![Problemen oplossen, zoeken naar Hallo dubbele objecten](./media/active-directory-aadconnect-feature-device-writeback/troubleshoot2.png)

* Controleer of Hallo kenmerk msDS-DeviceLocation aanwezig is en een waarde op Hallo Device Registration Service-object. Lookup deze locatie en zorg ervoor dat het met Hallo objectType msDS-DeviceContainer aanwezig is.

![Oplossen, msDS-DeviceLocation](./media/active-directory-aadconnect-feature-device-writeback/troubleshoot3.png)

![Oplossen, Geregistreerdeapparaten objectklasse](./media/active-directory-aadconnect-feature-device-writeback/troubleshoot4.png)

* Controleer of Hallo account die wordt gebruikt door Hallo dat Active Directory-Connector heeft de vereiste machtigingen op Hallo geregistreerde apparaten container door de vorige stap Hallo gevonden. Dit is verwacht Hallo machtigingen voor deze container:

![Problemen oplossen, Controleer de machtigingen voor de container](./media/active-directory-aadconnect-feature-device-writeback/troubleshoot5.png)

* Controleer Hallo Active Directory-account is gemachtigd op Hallo CN = configuratie van apparaatregistratie, CN = Services, CN = Configuration-object.

![Problemen oplossen, Controleer de machtigingen voor de configuratie van apparaatregistratie](./media/active-directory-aadconnect-feature-device-writeback/troubleshoot6.png)

## <a name="additional-information"></a>Aanvullende informatie
* [Risico beheren met voorwaardelijke toegang](../active-directory-conditional-access.md)
* [Instellen van On-premises voorwaardelijke toegang met behulp van Azure Active Directory-apparaatregistratie](../active-directory-device-registration-on-premises-setup.md)

## <a name="next-steps"></a>Volgende stappen
Lees meer over het [integreren van uw on-premises identiteiten met Azure Active Directory](active-directory-aadconnect.md).


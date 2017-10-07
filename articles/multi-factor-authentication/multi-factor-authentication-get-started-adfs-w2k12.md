---
title: aaaMFA Server met AD FS in Windows Server | Microsoft Docs
description: Dit artikel wordt beschreven hoe tooget de slag met Azure multi-factor Authentication en AD FS in Windows Server 2012 R2 en 2016.
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: 57208068-1e55-45b6-840f-fdcd13723074
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/29/2017
ms.author: kgremban
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 656785abcc63a020add765a86670b488a3b84b51
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-azure-multi-factor-authentication-server-toowork-with-ad-fs-in-windows-server"></a>Azure multi-factor Authentication-Server toowork configureren met AD FS in Windows Server
Als u Active Directory Federation Services (AD FS) gebruiken en toosecure cloud of on-premises resources wilt, kunt u de Azure multi-factor Authentication-Server toowork met AD FS kunt configureren. Deze configuratie activeert verificatie in twee stappen voor waardevolle eindpunten.

In dit artikel wordt besproken hoe u de Azure Multi-Factor Authentication-server gebruikt met AD FS in Windows Server 2012 R2 of Windows Server 2016. Voor meer informatie lezen over het te[cloud en on-premises resources beveiligen met behulp van Azure multi-factor Authentication-Server met AD FS 2.0](multi-factor-authentication-get-started-adfs-adfs2.md).

## <a name="secure-windows-server-ad-fs-with-azure-multi-factor-authentication-server"></a>Windows Server AD FS beveiligen met Azure Multi-Factor Authentication-server
Wanneer u Azure multi-factor Authentication-Server installeert, hebt u Hallo volgende opties:

* Azure multi-factor Authentication-Server lokaal installeren op Hallo dezelfde server als AD FS
* Hello Azure multi-factor Authentication-adapter lokaal installeren op Hallo AD FS-server en installeer de multi-factor Authentication-Server op een andere computer

Voordat u begint, worden op de hoogte van de volgende informatie Hallo:

* U bent geen vereiste tooinstall Azure multi-factor Authentication-Server op uw AD FS-server. U moet echter Hallo multi-factor Authentication-adapter installeren voor AD FS op een Windows Server 2012 R2 of Windows Server 2016 met AD FS. U kunt Hallo-server installeren op een andere computer, als dit een ondersteunde versie is en u Hallo AD FS-adapter afzonderlijk op uw federatieve AD FS-server installeren. Hallo Zie volgende procedures toolearn hoe tooinstall Hallo adapter afzonderlijk.
* Als uw organisatie van SMS-berichten of mobiele app verificatiemethoden te gebruiken gebruikmaakt, Hallo tekenreeksen die zijn gedefinieerd in de bedrijfsinstellingen bevatten een tijdelijke aanduiding <$*toepassingsnaam*$>. In MFA Server v7.1 kunt u de naam van een toepassing opgeven die wordt gebruikt in plaats van deze tijdelijke aanduiding. In v7.0 of ouder, wordt deze tijdelijke aanduiding niet automatisch vervangen wanneer u Hallo AD FS-adapter. Verwijderen Hallo tijdelijke aanduiding voor deze oudere versies van de desbetreffende tekenreeksen Hallo wanneer u AD FS beveiligen.
* Hallo-account waarmee u toosign in moet gebruiker rechten toocreate beveiligingsgroepen hebben in uw Active Directory-service.
* installatiewizard Hallo multi-factor Authentication AD FS-adapter wordt gemaakt van een beveiligingsgroep met de naam PhoneFactor Admins in uw exemplaar van Active Directory. Vervolgens wordt Hallo AD FS-serviceaccount van uw federation service toothis groep toegevoegd. Controleer of op uw domeincontroller die Hallo PhoneFactor Admins-groep is gemaakt en dat Hallo AD FS-serviceaccount lid is van deze groep. Indien nodig, handmatig toevoegen van Hallo AD FS-service-account toohello PhoneFactor Admins-groep op uw domeincontroller.
* Lees voor informatie over het installeren van Hallo Web Service SDK met de gebruikersportal Hallo over [Hallo-gebruikersportal implementeren voor Azure multi-factor Authentication-Server.](multi-factor-authentication-get-started-portal.md)

### <a name="install-azure-multi-factor-authentication-server-locally-on-hello-ad-fs-server"></a>Azure multi-factor Authentication-Server lokaal installeren op Hallo AD FS-server
1. Download en installeer de Azure Multi-Factor Authentication-server op uw AD FS-server. Lees [Aan de slag met de Azure Multi-Factor Authentication-server](multi-factor-authentication-get-started-server.md) voor informatie over de installatie.
2. Klik in beheerconsole voor hello Azure multi-factor Authentication-Server op Hallo **AD FS** pictogram. Hallo-opties selecteren **gebruikersregistratie toestaan** en **toestaan dat gebruikers de methode tooselect**.
3. Selecteer eventueel aanvullende opties die u wilt toospecify voor uw organisatie.
4. Klik op **AD FS-adapter installeren**.
   
   <center>![Cloud](./media/multi-factor-authentication-get-started-adfs-w2k12/server.png)</center>

5. Als Hallo Active Directory-venster wordt weergegeven, betekent dit dat twee dingen. Uw computer is lid tooa domein en Hallo Active Directory-configuratie voor het beveiligen van communicatie tussen Hallo AD FS-adapter en Hallo multi-factor Authentication-service is voltooid. Klik op **volgende** tooautomatically deze configuratie te voltooien, of selecteer Hallo **automatische Active Directory-configuratie overslaan en instellingen handmatig** selectievakje. Klik op **Volgende**.
6. Als de lokale groep-windows hello wordt weergegeven, betekent dit dat twee dingen. Uw computer is geen gekoppelde tooa domein en Hallo lokale groep-configuratie voor het beveiligen van communicatie tussen Hallo AD FS-adapter en Hallo multi-factor Authentication-service is voltooid. Klik op **volgende** tooautomatically deze configuratie te voltooien, of selecteer Hallo **automatische lokale groep-configuratie overslaan en instellingen handmatig** selectievakje. Klik op **Volgende**.
7. Klik in de installatiewizard Hallo **volgende**. Azure multi-factor Authentication-Server maakt Hallo PhoneFactor Admins-groep en voegt Hallo AD FS-service-account toohello PhoneFactor Admins-groep.
   <center>![Cloud](./media/multi-factor-authentication-get-started-adfs-w2k12/adapter.png)</center>
8. Op Hallo **start het installatieprogramma** pagina, klikt u op **volgende**.
9. Klik in het installatieprogramma van Hallo multi-factor Authentication AD FS-adapter op **volgende**.
10. Klik op **sluiten** wanneer Hallo-installatie is voltooid.
11. Wanneer het Hallo-adapter is geïnstalleerd, moet u het registreren met AD FS. Open Windows PowerShell en Voer Hallo volgende opdracht uit:<br>
    `C:\Program Files\Multi-Factor Authentication Server\Register-MultiFactorAuthenticationAdfsAdapter.ps1`
    <center>![Cloud](./media/multi-factor-authentication-get-started-adfs-w2k12/pshell.png)</center>
12. toouse uw zojuist geregistreerde bewerken Hallo algemene verificatiebeleid in AD FS-adapter. Ga in de Hallo AD FS-beheerconsole toohello **verificatiebeleid** knooppunt. In Hallo **multi-factor Authentication** sectie, klikt u op Hallo **bewerken** koppelen van de volgende toohello **globale instellingen** sectie. In Hallo **algemeen verificatiebeleid bewerken** Selecteer **multi-Factor Authentication** als aanvullende authenticatiemethode en klik vervolgens op **OK**. Hallo-adapter wordt geregistreerd als WindowsAzureMultiFactorAuthentication. Hallo registratie tootake effect Hallo AD FS service opnieuw starten.

<center>![Cloud](./media/multi-factor-authentication-get-started-adfs-w2k12/global.png)</center>

Op dit moment is multi-factor Authentication-Server ingesteld toobe een extra authenticatie provider toouse met AD FS.

## <a name="install-a-standalone-instance-of-hello-ad-fs-adapter-by-using-hello-web-service-sdk"></a>Een zelfstandig exemplaar van Hallo AD FS-adapter installeren met behulp van Hallo Web Service SDK
1. Hallo Web Service SDK installeren op Hallo-server waarop multi-factor Authentication-Server wordt uitgevoerd.
2. Kopiëren Hallo volgende bestanden van Hallo \Program Files\Multi-Factor Authentication-Server directory toohello server waarop u van plan tooinstall Hallo AD FS-adapter bent:
   * MultiFactorAuthenticationAdfsAdapterSetup64.msi
   * Register-MultiFactorAuthenticationAdfsAdapter.ps1
   * Unregister-MultiFactorAuthenticationAdfsAdapter.ps1
   * MultiFactorAuthenticationAdfsAdapter.config
3. Hallo bestanden MultiFactorAuthenticationAdfsAdapterSetup64.msi-installatiebestand uitvoeren.
4. Klik in het installatieprogramma van Hallo multi-factor Authentication AD FS-adapter op **volgende** toostart Hallo-installatie.
5. Klik op **sluiten** wanneer Hallo-installatie is voltooid.

## <a name="edit-hello-multifactorauthenticationadfsadapterconfig-file"></a>Hallo MultiFactorAuthenticationAdfsAdapter.config bestand bewerken
Volg deze stappen tooedit hello MultiFactorAuthenticationAdfsAdapter.config bestand:

1. Set Hallo **UseWebServiceSdk** knooppunt te**true**.  
2. Hallo waarde instellen voor **webservicesdkurl in** toohello URL Hallo multi-factor Authentication Web Service SDK. Bijvoorbeeld: *https://contoso.com/&lt;certificatename&gt;/MultiFactorAuthWebServiceSdk/PfWsSdk.asmx*, waarbij *certificatename* Hallo-naam van uw certificaat.  
3. Hallo Register-MultiFactorAuthenticationAdfsAdapter.ps1 script bewerken door toe te voegen *- ConfigurationFilePath &lt;pad&gt;*  toohello einde van Hallo `Register-AdfsAuthenticationProvider` opdracht, waarbij  *&lt;pad&gt;*  Hallo volledig pad toohello MultiFactorAuthenticationAdfsAdapter.config-bestand.

### <a name="configure-hello-web-service-sdk-with-a-username-and-password"></a>Hallo Web Service SDK configureren met een gebruikersnaam en wachtwoord
Er zijn twee opties voor het configureren van Hallo Web Service SDK. Hallo eerst is met een gebruikersnaam en wachtwoord, hello tweede met een clientcertificaat. Volg deze stappen voor de eerste optie Hallo of overslaan voor Hallo tweede.  

1. Hallo waarde instellen voor **webservicesdkusername in** tooan-account dat lid is van Hallo beveiligingsgroep PhoneFactor Admins. Gebruik Hallo &lt;domein&gt;&#92;&lt; gebruikersnaam&gt; indeling.  
2. Hallo waarde instellen voor **webservicesdkpassword in** toohello geschikte accountwachtwoord.

### <a name="configure-hello-web-service-sdk-with-a-client-certificate"></a>Hallo Web Service SDK configureren met een clientcertificaat
Als u niet toouse een gebruikersnaam en wachtwoord wilt, volgt u deze stappen tooconfigure Hallo Web Service SDK met een clientcertificaat.

1. Verkrijg een certificaat van een certificeringsinstantie voor Hallo-server die als Hallo Web Service SDK wordt uitgevoerd. Meer informatie over hoe te[clientcertificaten verkrijgen](https://technet.microsoft.com/library/cc770328.aspx).  
2. Importeren Hallo client certificate toohello lokale computer persoonlijke certificaatarchief op Hallo-server waarop Hallo Web Service SDK wordt uitgevoerd. Zorg ervoor dat Hallo certificeringsinstantie openbaar certificaat is in het certificaatarchief Vertrouwde basiscertificaten.  
3. Hallo openbare en persoonlijke sleutels van Hallo client certificate tooa pfx-bestand exporteren.  
4. Exporteer de openbare sleutel Hallo in Base64-indeling tooa cer-bestand.  
5. Klik in Serverbeheer of dat Hallo webserver (IIS) \web verificatie van clientcertificaten toewijzen van deze functie is geïnstalleerd. Als dit niet is geïnstalleerd, selecteert u **functies en onderdelen toevoegen** tooadd deze functie.  
6. Dubbelklik in IIS-beheer **configuratie-Editor** op Hallo-website die Hallo Web Service SDK virtuele map bevat. Belangrijke tooselect Hallo website, niet Hallo virtuele map is.  
7. Ga toohello **system.webServer/security/authentication/iisClientCertificateMappingAuthentication** sectie.  
8. Set ingeschakeld te**true**.  
9. Stel oneToOneCertificateMappingsEnabled te**true**.  
10. Klik op Hallo **...**  volgende toooneToOneMappings knop en klik vervolgens op Hallo **toevoegen** koppeling.  
11. Open Hallo Base64 cer-bestand die u eerder hebt geëxporteerd. Verwijder *-----BEGIN CERTIFICATE-----*, *-----END CERTIFICATE-----* en alle regeleinden. Kopieer de resulterende tekenreeks Hallo.  
12. Certificaat set toohello-tekenreeks in de voorgaande stap Hallo hebt gekopieerd.  
13. Set ingeschakeld te**true**.  
14. Gebruikersnaam tooan account dat lid is van de beveiligingsgroep PhoneFactor Admins Hallo instellen. Gebruik Hallo &lt;domein&gt;&#92;&lt; gebruikersnaam&gt; indeling.  
15. Hallo wachtwoord toohello juiste accountwachtwoord instellen en sluit vervolgens configuratie-Editor.  
16. Klik op Hallo **toepassen** koppeling.  
17. Dubbelklik in Hallo virtuele map Web Service SDK en **verificatie**.  
18. Controleer of ASP.NET-imitatie en basisverificatie te ingesteld**ingeschakeld**, en dat alle overige items te zijn ingesteld**uitgeschakelde**.  
19. Dubbelklik in Hallo virtuele map Web Service SDK en **SSL-instellingen**.  
20. Stel clientcertificaten te**accepteren**, en klik vervolgens op **toepassen**.  
21. Hallo pfx-bestand geëxporteerd van eerdere toohello-server met AD FS-adapter Hallo kopiëren.  
22. Hallo pfx-bestand toohello lokale computer persoonlijke certificaatarchief importeren.  
23. Met de rechtermuisknop en selecteer **persoonlijke sleutels beheren**, en vervolgens Verleen leestoegang toohello account waarmee u toosign in toohello AD FS-service.  
24. Hallo client certificaat en de kopie Hallo vingerafdruk openen vanuit Hallo **Details** tabblad.  
25. Stel in het bestand MultiFactorAuthenticationAdfsAdapter.config hello **WebServiceSdkCertificateThumbprint** toohello tekenreeks in de vorige stap Hallo hebt gekopieerd.  

Ten slotte tooregister Hallo-adapter, Hallo \Program Files\Multi uitvoeren-Factor Authentication Server\Register-MultiFactorAuthenticationAdfsAdapter.ps1 script in PowerShell. Hallo-adapter wordt geregistreerd als WindowsAzureMultiFactorAuthentication. Hallo registratie tootake effect Hallo AD FS service opnieuw starten.

## <a name="secure-azure-ad-resources-using-ad-fs"></a>Azure AD-resources beveiligen met behulp van AD FS
toosecure uw cloudresource, instellen van een regel voor claims zodat Active Directory Federation Services Hallo multipleauthn claim verzendt wanneer een gebruiker wordt verificatie in twee stappen is uitgevoerd. Deze claim is tooAzure AD doorgegeven. Volg deze procedure toowalk Hallo stappen:

1. Open AD FS-beheer.
2. Selecteer aan de linkerkant Hallo **Relying Party-vertrouwensrelaties**.
3. Klik met de rechtermuisknop op **Identiteitsplatform van Microsoft Office 365** en selecteer **Claimregels bewerken...**

   ![Cloud](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip1.png)

4. Klik bij Uitgifte transformatieregels op **Regel toevoegen**.

   ![Cloud](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip2.png)

5. Op Hallo transformeren Wizard Claimregel voor toevoegen, selecteert u **doorgeven of filteren van een binnenkomende Claim** in Hallo vervolgkeuzelijst en klik op **volgende**.

   ![Cloud](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip3.png)

6. Geef de regel een naam.
7. Selecteer **Verwijdingen verificatiemethode** als Hallo binnenkomende claimtype.
8. Selecteer **Alle claimwaarden doorgeven**.
    ![Wizard Claimregel voor transformatie toevoegen](./media/multi-factor-authentication-get-started-adfs-cloud/configurewizard.png)
9. Klik op **Voltooien**. Sluit Hallo AD FS-beheerconsole.

## <a name="related-topics"></a>Verwante onderwerpen
Zie voor het oplossen van problemen Hallo [Azure multi-factor Authentication Veelgestelde vragen](multi-factor-authentication-faq.md)

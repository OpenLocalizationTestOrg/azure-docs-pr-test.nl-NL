---
title: Azure MFA-Server met AD FS 2.0 aaaUse | Microsoft Docs
description: Dit is hello Azure multi-factor authentication-pagina waarop wordt beschreven hoe tooget de slag met Azure MFA en AD FS 2.0.
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 96168849-241a-4499-a224-d829913caa7e
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/14/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: H1Hack27Feb2017, it-pro
ms.openlocfilehash: 15011a94ca69dc6e51aa3edf74f5db6cd44d697a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-azure-multi-factor-authentication-server-toowork-with-ad-fs-20"></a>Azure multi-factor Authentication-Server toowork configureren met AD FS 2.0
Dit artikel is voor organisaties die zijn gefedereerd met Azure Active Directory en wilt toosecure resources die zich on-premises of in Hallo cloud. Uw resources beveiligen door hello Azure multi-factor Authentication-Server en deze configureren toowork met AD FS zodat verificatie in twee stappen is geactiveerd voor waardevolle eindpunten.

Deze documentatie wordt beschreven hoe u van hello Azure multi-factor Authentication-Server met AD FS 2.0. Voor meer informatie over AD FS raadpleegt u [Uw cloudresources en on-premises resources beveiligen met behulp van de Azure Multi-Factor Authentication-server met AD FS in Windows Server 2012 R2](multi-factor-authentication-get-started-adfs-w2k12.md).

## <a name="secure-ad-fs-20-with-a-proxy"></a>AD FS 2.0 beveiligen met een proxy
toosecure AD FS 2.0 met een proxy hello Azure multi-factor Authentication-Server op Hallo AD FS proxy-server installeren.

### <a name="configure-iis-authentication"></a>IIS-verificatie configureren
1. In hello Azure multi-factor Authentication-Server, klikt u op Hallo **IIS-verificatie** pictogram in het linkermenu Hallo.
2. Klik op Hallo **op basis van formulieren** tabblad.
3. Klik op **Add**.

   <center>![Instellen](./media/multi-factor-authentication-get-started-adfs-adfs2/setup1.png)</center>

4. variabelen voor de gebruikersnaam, wachtwoord en domein toodetect automatisch, voert Hallo aanmeldings-URL (bijvoorbeeld https://sso.contoso.com/adfs/ls) in Hallo formulier-gebaseerde Website dialoogvenster in en klikt u op **OK**.
5. Controleer de Hallo **gebruikersovereenkomst vereist Azure multi-factor Authentication** vak als alle gebruikers zijn of worden geïmporteerd in Hallo Server en onderwerp tootwo stap verificatie. Als een groot aantal gebruikers nog niet is geïmporteerd in Hallo Server en/of vrijgesteld van verificatie in twee stappen zijn zal, laat u Hallo vakje uitgeschakeld.
6. Als de paginavariabelen Hallo kunnen niet automatisch worden gedetecteerd, klikt u op Hallo **handmatig opgeven...** knop in het dialoogvenster van Hallo formulier-gebaseerde Website.
7. Hallo formulier-gebaseerde Website in het dialoogvenster Hallo URL toohello AD FS-aanmeldingspagina Voer in het veld van Hallo indienings-URL (bijvoorbeeld https://sso.contoso.com/adfs/ls) en voer een toepassingsnaam in (optioneel). de naam van de toepassing Hello wordt weergegeven in de Azure multi-factor Authentication-rapporten en kan worden weergegeven in verificatieberichten via SMS of mobiele App.
8. Hallo Aanvraagindeling te ingesteld**POST of GET**.
9. Voer Hallo gebruikersnaamvariabele (ctl00$ ContentPlaceHolder1$ UsernameTextBox) en wachtwoordvariabele (ctl00$ ContentPlaceHolder1$ PasswordTextBox). Als uw formulier-gebaseerde aanmeldingspagina een tekstvak domein wordt weergegeven, voert u Hallo domeinvariabele. toofind hello namen van de invoervakken Hallo op Hallo-aanmeldingspagina, Ga toohello aanmeldingspagina in een webbrowser met de rechtermuisknop op het Hallo-pagina en selecteer **bron weergeven**.
10. Controleer de Hallo **gebruikersovereenkomst vereist Azure multi-factor Authentication** vak als alle gebruikers zijn of worden geïmporteerd in Hallo Server en onderwerp tootwo stap verificatie. Als een groot aantal gebruikers nog niet is geïmporteerd in Hallo Server en/of vrijgesteld van verificatie in twee stappen zijn zal, laat u Hallo vakje uitgeschakeld.
    <center>![Instellen](./media/multi-factor-authentication-get-started-adfs-adfs2/manual.png)</center>
11. Klik op **Geavanceerd...** tooreview geavanceerde instellingen. U kunt onder meer de volgende instellingen configureren:

    - Een aangepast bestand voor de weigeringspagina selecteren
    - Cache geslaagde verificaties toohello website gebruik van cookies
    - Selecteer hoe tooauthenticate Hallo primaire referenties

12. Aangezien Hallo AD FS-proxyserver is niet waarschijnlijk toobe lid toohello domein, kunt u LDAP tooconnect tooyour-domeincontroller voor het importeren van gebruikers en pre-authenticatie. Klik op Hallo Hallo Website van de opties in het dialoogvenster **primaire verificatie** tabblad en selecteer **LDAP-binding** voor Hallo type verificatie vooraf-verificatie.
13. Wanneer voltooid, klikt u op **OK** tooreturn in het dialoogvenster toohello formulier-gebaseerde Website.
14. Klik op **OK** tooclose Hallo dialoogvenster.
15. Eenmaal Hallo URL en paginavariabelen zijn gedetecteerd of ingevoerd, Hallo websitegegevens weergegeven in Hallo paneel op formulier gebaseerd.
16. Klik op Hallo **systeemeigen Module** tabblad en Hallo-server, Hallo-website die Hallo AD FS-proxy wordt uitgevoerd onder (zoals "Default Web Site"), selecteren of AD FS-proxy toepassing (zoals 'ls' onder 'adfs') tooenable Hallo IIS-invoegtoepassing op Hallo Hallo gewenste niveau.
17. Klik op Hallo **inschakelen IIS-verificatie** vak Hallo boven aan het welkomstscherm.

Hallo IIS-verificatie is nu ingeschakeld.

### <a name="configure-directory-integration"></a>Adreslijstintegratie configureren
IIS-verificatie is ingeschakeld, maar tooperform Hallo verificatie vooraf tooyour Active Directory (AD) via LDAP, moet u configureren Hallo LDAP verbinding toohello-domeincontroller.

1. Klik op Hallo **Adreslijstintegratie** pictogram.
2. Selecteer op het tabblad Instellingen Hallo Hallo **Gebruik specifieke LDAP-configuratie** keuzerondje.

   <center>![Instellen](./media/multi-factor-authentication-get-started-adfs-adfs2/ldap1.png)</center>

3. Klik op **Bewerken**.
4. Vul in Hallo LDAP-configuratie bewerken in het dialoogvenster Hallo velden met Hallo informatie vereist tooconnect toohello AD-domeincontroller. Beschrijvingen van Hallo velden zijn opgenomen in hello Azure multi-factor Authentication-Server help-bestand.
5. Hallo LDAP-verbinding testen door te klikken op Hallo **Test** knop.

   <center>![Instellen](./media/multi-factor-authentication-get-started-adfs-adfs2/ldap2.png)</center>

6. Als Hallo LDAP-verbindingstest geslaagd is, klikt u op **OK**.

### <a name="configure-company-settings"></a>Instellingen van het bedrijf configureren
1. Klik vervolgens op Hallo **Bedrijfsinstellingen** pictogram en selecteer Hallo **omzetting van gebruikersnaam** tabblad.
2. Selecteer Hallo **LDAP gebruiken kenmerk unieke id voor overeenkomende gebruikersnamen** keuzerondje.
3. Als gebruikers hun gebruikersnaam invoeren in de indeling 'domein\gebruikersnaam', moet Hallo Server toobe kunnen toostrip Hallo domein uit Hallo gebruikersnaam bij het maken van Hallo LDAP-query. Dat kan worden gedaan met behulp van een registerinstelling.
4. Open de Register-editor Hallo en ga tooHKEY_LOCAL_MACHINE/SOFTWARE/Wow6432Node/positieve Networks/PhoneFactor op een 64-bits-server. Als u zich op een 32-bits-server, nemen Hallo 'Wow6432Node' buiten het Hallo-pad. Maak een DWORD-registersleutel 'UsernameCxz_stripPrefixDomain' genoemd en Hallo waarde too1 ingesteld. Azure multi-factor Authentication is nu de beveiliging Hallo AD FS-proxy.

Zorg ervoor dat gebruikers uit Active Directory in Hallo Server zijn geïmporteerd. Zie Hallo [sectie goedgekeurde IP-adressen](#trusted-ips) als u toowhitelist interne IP-adressen wilt zodat verificatie in twee stappen niet vereist is als u zich aanmeldt toohello website vanaf die locaties.

<center>![Instellen](./media/multi-factor-authentication-get-started-adfs-adfs2/reg.png)</center>

## <a name="ad-fs-20-direct-without-a-proxy"></a>AD FS 2.0 Direct zonder een proxy
U kunt AD FS beveiligen wanneer Hallo AD FS-proxy niet wordt gebruikt. Hello Azure multi-factor Authentication-Server op Hallo AD FS-server installeren en configureren van Hallo Server per Hallo volgende stappen:

1. Binnen hello Azure multi-factor Authentication-Server, klikt u op Hallo **IIS-verificatie** pictogram in het linkermenu Hallo.
2. Klik op Hallo **HTTP** tabblad.
3. Klik op **Add**.
4. Voer Hallo-URL voor AD FS-website waarop HTTP-verificatie wordt uitgevoerd (bijvoorbeeld https://sso.domain.com/adfs/ls/auth/integrated) in veld Hallo Hallo in Hallo basis-URL toevoegen dialoog vak. Voer dan een toepassingsnaam in (optioneel). de naam van de toepassing Hello wordt weergegeven in de Azure multi-factor Authentication-rapporten en kan worden weergegeven in verificatieberichten via SMS of mobiele App.
5. Indien gewenst, aanpassen Hallo inactiviteit en voor maximale sessie tijden.
6. Controleer de Hallo **gebruikersovereenkomst vereist Azure multi-factor Authentication** vak als alle gebruikers zijn of worden geïmporteerd in Hallo Server en onderwerp tootwo stap verificatie. Als een groot aantal gebruikers nog niet is geïmporteerd in Hallo Server en/of vrijgesteld van verificatie in twee stappen zijn zal, laat u Hallo vakje uitgeschakeld.
7. Selectievakje Hallo cookie cache indien gewenst.

   <center>![Instellen](./media/multi-factor-authentication-get-started-adfs-adfs2/noproxy.png)</center>

8. Klik op **OK**.
9. Klik op Hallo **systeemeigen Module** tabblad en selecteer Hallo-server, Hallo-website (zoals "Default Web Site") of Hallo AD FS-toepassing (zoals 'ls' onder 'adfs') tooenable Hallo IIS-invoegtoepassing op Hallo gewenst niveau.
10. Klik op Hallo **inschakelen IIS-verificatie** vak Hallo boven aan het welkomstscherm.

AD FS wordt nu beveiligd met Azure Multi-Factor Authentication.

Zorg ervoor dat gebruikers uit Active Directory in Hallo Server zijn geïmporteerd. Zie Hallo sectie goedgekeurde IP-adressen als u toowhitelist intern IP-adres wilt adressen, zodat verificatie in twee stappen niet vereist is als u zich aanmeldt toohello website vanaf die locaties.

## <a name="trusted-ips"></a>Goedgekeurde IP-adressen
Goedgekeurde IP-adressen toestaan dat gebruikers toobypass Azure multi-factor Authentication voor websiteaanvragen die afkomstig zijn van specifieke IP-adressen of subnetten. U kunt bijvoorbeeld, tooexempt verificatie in twee stappen gebruikers wanneer ze zich vanaf Hallo office aanmelden. Hiervoor geeft u het subnet van kantoor Hallo als een goedgekeurde IP-adressen.

### <a name="tooconfigure-trusted-ips"></a>tooconfigure goedgekeurde IP-adressen
1. In de sectie IIS-verificatie hello, klikt u op Hallo **goedgekeurde IP-adressen** tabblad.
2. Klik op Hallo **toevoegen...** te klikken.
3. Wanneer het dialoogvenster voor Hallo goedgekeurde IP-adres toevoegen wordt weergegeven, selecteer een van de Hallo **één IP-adres**, **IP-bereik**, of **Subnet** keuzerondjes.
4. Voer Hallo IP-adres, bereik van IP-adressen of subnet op dat u wilt plaatsen. Als een subnet wilt invoeren, selecteer de geschikte netmasker en klikt u op Hallo Hallo **OK** knop. Hallo vertrouwd dat IP is toegevoegd.

<center>![Instellen](./media/multi-factor-authentication-get-started-adfs-adfs2/trusted.png)</center>

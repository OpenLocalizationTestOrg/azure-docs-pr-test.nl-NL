---
title: verificatie op basis van aaaHeader met PingAccess voor Azure AD-toepassingsproxy | Microsoft Docs
description: Toepassingen met PingAccess toepassingsproxy toosupport headers gebaseerde verificatie en publiceren.
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/23/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 38fe3e7a41a71f4ae6c75f014e44c722f773bd22
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="header-based-authentication-for-single-sign-on-with-application-proxy-and-pingaccess"></a>Verificatie op basis van een koptekst voor eenmalige aanmelding met toepassingsproxy en PingAccess

Azure Active Directory-toepassingsproxy en PingAccess hebben hun samen tooprovide Azure Active Directory-klanten met toegang tooeven meer toepassingen. PingAccess wordt uitgebreid Hallo [bestaande toepassingsproxy aanbiedingen](active-directory-application-proxy-get-started.md) tooinclude één aanmelding toegang tooapplications die headers voor verificatie gebruiken.

## <a name="what-is-pingaccess-for-azure-ad"></a>Wat is PingAccess voor Azure AD?

PingAccess voor Azure Active Directory is een aanbieding van PingAccess waarmee u toogive gebruikerstoegang en eenmalige aanmelding tooapplications die headers voor verificatie gebruiken. Toepassingsproxy behandelt deze apps zoals elke andere met behulp van Azure AD tooauthenticate toegang en vervolgens verkeer via Hallo-connectorservice wordt doorgegeven. PingAccess bevindt zich voor het Hallo-apps en zet Hallo toegangstoken van Azure AD in een koptekst zodat Hallo toepassing hello verificatie in Hallo-indeling die kan gelezen ontvangt.

Uw gebruikers won't iets anders zien wanneer ze zich toouse uw zakelijke apps aanmelden. Ze kunnen nog steeds overal werken uit op elk apparaat. 

Aangezien Hallo toepassingsproxy connectors extern verkeer tooall apps, ongeacht hun verificatietype directe, moeten ze tooload saldo blijven automatisch, maar ook.

## <a name="how-do-i-get-access"></a>Hoe krijg ik toegang?

Aangezien dit scenario wordt aangeboden via een samenwerking tussen Azure Active Directory en PingAccess, moet u licenties voor beide services. Azure Active Directory Premium-abonnementen bevatten echter een PingAccess standaardlicentie die betrekking heeft op up too20 toepassingen. Als u toopublish meer dan 20 header-toepassingen moet, kunt u een extra licentie aanschaffen bij PingAccess. 

Zie [Azure Active Directory-edities](active-directory-editions.md) voor meer informatie.

## <a name="publish-your-application-in-azure"></a>Uw toepassing publiceren in Azure

In dit artikel is bedoeld voor personen die een app met dit scenario voor Hallo eerst wilt publiceren. Er wordt uitgelegd hoe tooget met de toepassings- en PingAccess, Daarnaast toohello publishing stappen gestart. Als u beide services al hebt geconfigureerd, maar u wilt dat een refresher op Hallo stappen publiceren, kunt u overslaan Hallo-connector installeren en te verplaatsen op[toevoegen van uw app tooAzure AD met toepassingsproxy](#add-your-app-to-Azure-AD-with-Application-Proxy).

>[!NOTE]
>Omdat dit scenario een verbinding tussen Azure AD is en PingAccess, aantal Hallo instructies aanwezig zijn op Hallo identiteit van de Ping-site.

### <a name="install-an-application-proxy-connector"></a>Een Application Proxy connector installeren

Als u al Application Proxy ingeschakeld hebt en hebt een connector is geïnstalleerd, kunt u deze sectie overslaan en te verplaatsen op[toevoegen van uw app tooAzure AD met toepassingsproxy](#add-your-app-to-azure-ad-with-application-proxy).

Hallo Application Proxy connector is een Windows Server-service die Hallo verkeer van uw werknemers extern tooyour stuurt gepubliceerde apps. Zie voor meer installatie-instructies, [toepassingsproxy inschakelen in Azure-portal Hallo](active-directory-application-proxy-enable.md).

1. Meld u aan toohello [Azure-portal](https://portal.azure.com) als globale beheerder.
2. Selecteer **Azure Active Directory** > **toepassingsproxy**.
3. Selecteer **Connector downloaden** toostart Hallo Application Proxy connector downloaden. Hallo-installatie-instructies.

   ![Toepassingsproxy inschakelen en Hallo connector downloaden](./media/application-proxy-ping-access/install-connector.png)

4. Hallo connector downloaden moet automatisch toepassingsproxy inschakelen voor uw directory, maar als u dit niet kunt selecteren **Enable Application Proxy**.


### <a name="add-your-app-tooazure-ad-with-application-proxy"></a>Uw app tooAzure AD met toepassingsproxy toevoegen

Er zijn twee acties, moet u tootake in hello Azure-portal. U moet eerst uw toepassing met toepassingsproxy toopublish. Vervolgens moet u toocollect enige informatie over het Hallo-app die u kunt tijdens Hallo PingAccess stappen gebruiken.

Volg deze stappen toopublish uw app. Voor een meer overzicht van de stappen 1-8, Zie gedetailleerde [toepassingen publiceren met Azure AD-toepassingsproxy](application-proxy-publish-azure-portal.md).

1. Als dat niet in de laatste sectie Hallo aanmelden toohello [Azure-portal](https://portal.azure.com) als globale beheerder.
2. Selecteer **Azure Active Directory** > **bedrijfstoepassingen**.
3. Selecteer **toevoegen** Hallo boven aan het Hallo-blade.
4. Selecteer **On-premises toepassing**.
5. Vul de velden Hallo vereist met informatie over uw nieuwe app. Hallo volgen richtlijnen voor het Hallo-instellingen gebruiken:
   - **Interne URL**: normaal u Hallo-URL die u toohello-app-aanmelding op de pagina als u in het bedrijfsnetwerk Hallo opgeven. Voor dit scenario moet Hallo connector tootreat hello PingAccess proxy als Hallo voorpagina van Hallo-app. Gebruik de volgende notatie: `https://<host name of your PA server>:<port>`. Hallo-poort is 3000 standaard, maar u kunt deze configureren in PingAccess.
   - **Methode voor verificatie vooraf**: Azure Active Directory
   - **URL in de Headers vertalen**: Nee

   >[!NOTE]
   >Als dit uw eerste toepassing, gebruik van poort 3000 toostart en keert u terug tooupdate deze instelling als u de configuratie van uw PingAccess wijzigt. Als dit uw app tweede of hoger, moet dit toomatch Hallo Listener die u hebt geconfigureerd in PingAccess. Meer informatie over [luisteraars in PingAccess](https://documentation.pingidentity.com/pingaccess/pa31/index.shtml#Listeners.html).

6. Selecteer **toevoegen** Hallo Hallo blade onderaan in. Uw toepassing wordt toegevoegd en Hallo snel startmenu wordt geopend.
7. Selecteer in het menu snelle start Hallo **een gebruiker toewijzen voor het testen van**, en ten minste één gebruiker toohello toepassing toe te voegen. Zorg ervoor dat dit testaccount toegang toohello on-premises toepassing.
8. Selecteer **toewijzen** toosave Hallo test de gebruiker is toegewezen.
9. Selecteer op de blade Hallo app management, **eenmalige aanmelding**.
10. Kies **headers gebaseerde aanmelding** uit de vervolgkeuzelijst Hallo. Selecteer **Opslaan**.

   >[!TIP]
   >Als dit de eerste keer is op basis van een koptekst eenmalige aanmelding, moet u tooinstall PingAccess. toomake ervoor dat uw Azure-abonnement is automatisch gekoppeld aan uw PingAccess-installatie Hallo-verbinding op deze pagina voor eenmalige aanmelding toodownload PingAccess gebruiken. U kunt nu Hallo downloadsite openen of toothis pagina later terugkomen. 

   ![Selecteer op basis van een koptekst eenmalige aanmelding](./media/application-proxy-ping-access/sso-header.PNG)

11. Hallo Enterprise toepassingen blade sluiten of alle Hallo manier toohello links tooreturn toohello Azure Active Directory menu bladeren.
12. Selecteer **App registraties**.

   ![Selecteer de App-registraties](./media/application-proxy-ping-access/app-registrations.png)

13. Selecteer Hallo-app die u zojuist hebt toegevoegd, klikt u vervolgens **antwoord-URL's**.

   ![Selecteer de antwoord-URL 's](./media/application-proxy-ping-access/reply-urls.png)

14. Controleer de toosee als externe URL Hallo die u toegewezen tooyour app in stap 5 in de lijst met Hallo antwoord-URL's. Als dit niet het geval is, moet u deze nu toevoegen.
15. Selecteer op de blade Hallo app-instellingen, **vereist machtigingen**.

  ![Selecteer de vereiste machtigingen](./media/application-proxy-ping-access/required-permissions.png)

16. Selecteer **Toevoegen**. Kies voor Hallo API, **Windows Azure Active Directory**, klikt u vervolgens **Selecteer**. Hallo-machtigingen, kiest u **lezen en schrijven van alle toepassingen** en **aanmelden en gebruikersprofiel lezen**, vervolgens **Selecteer** en **gedaan**.  

  ![Selecteer machtigingen](./media/application-proxy-ping-access/select-permissions.png)

### <a name="collect-information-for-hello-pingaccess-steps"></a>Verzamelen van informatie voor Hallo PingAccess stappen

1. Selecteer op de blade van uw app-instellingen **eigenschappen**. 

  ![Eigenschappen selecteren](./media/application-proxy-ping-access/properties.png)

2. Hallo opslaan **toepassings-Id** waarde. Dit wordt gebruikt voor Hallo client-ID wanneer u PingAccess configureert.
3. Selecteer op de blade Hallo app-instellingen, **sleutels**.

  ![Selecteer sleutels](./media/application-proxy-ping-access/Keys.png)

4. Een sleutel door te voeren van een sleutel beschrijving en een vervaldatum kiezen uit de vervolgkeuzelijst Hallo maken.
5. Selecteer **Opslaan**. Een GUID wordt weergegeven in Hallo **waarde** veld.

  Sla deze waarde, als u niet kunt toosee het opnieuw nadat u dit venster nu sluiten.

  ![Maak een nieuwe sleutel](./media/application-proxy-ping-access/create-keys.png)

6. Hallo App registraties blade sluiten of alle Hallo manier toohello links tooreturn toohello Azure Active Directory menu bladeren.
7. Selecteer **eigenschappen**.
8. Hallo opslaan **map-ID** GUID.

### <a name="optional---update-graphapi-toosend-custom-fields"></a>Optioneel - Update GraphAPI toosend aangepaste velden

Zie voor een lijst van beveiligingstokens die door Azure AD voor verificatie verzonden, [Azure AD-tokenverwijzing](./develop/active-directory-token-and-claims.md). Als u een aangepaste claim die door andere tokens verzonden moet, gebruikt u GraphAPI tooset Hallo app veld *acceptMappedClaims* te**True**. U kunt deze configuratie Azure AD Graph Explorer of MS Graph toomake. 

In dit voorbeeld wordt een grafiek Explorer:

```
PATCH https://graph.windows.net/myorganization/applications/<object_id_GUID_of_your_application> 

{
  "acceptMappedClaims":true
}
```

## <a name="download-pingaccess-and-configure-your-app"></a>PingAccess downloaden en configureren van uw app

Nu dat u alle hello Azure Active Directory setup stappen hebt voltooid, kunt u op tooconfiguring PingAccess. 

Hallo gedetailleerde stappen voor het Hallo PingAccess deel uitmaken van dit scenario blijven Hallo identiteit van de Ping-documentatie, [PingAccess configureren voor Azure AD](https://docs.pingidentity.com/bundle/paaad_m_ConfigurePAforMSAzureADSolution_paaad43/page/pa_c_PAAzureSolutionOverview.html).

Deze stappen doorlopen Hallo-proces voor het ophalen van een account PingAccess als u er nog geen hebt, Hallo PingAccess Server installeren en een Azure AD OIDC providerverbinding maken met Hallo map-ID die u hebt gekopieerd uit hello Azure-portal. Vervolgens gebruikt u Hallo toepassings-ID en sleutel waarden toocreate een websessie op PingAccess. U kunt daarna Identiteitstoewijzing instellen en maken van een virtuele host, de site en de toepassing.

### <a name="test-your-app"></a>Uw app testen

Als u al deze stappen hebt voltooid, moet uw app actief en werkend. tootest, open een browser en ga toohello externe URL die u hebt gemaakt toen u Hallo-app in Azure hebt gepubliceerd. Meld u aan met Hallo testaccount die toegewezen toohello u app.

## <a name="next-steps"></a>Volgende stappen

- [PingAccess configureren voor Azure AD](https://docs.pingidentity.com/bundle/paaad_m_ConfigurePAforMSAzureADSolution_paaad43/page/pa_c_PAAzureSolutionOverview.html)
- [Hoe biedt Azure AD-toepassingsproxy eenmalige aanmelding](application-proxy-sso-overview.md)
- [Toepassingsproxy oplossen](active-directory-application-proxy-troubleshoot.md)

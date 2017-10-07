---
title: aaaPublish apps met Azure AD-toepassingsproxy | Microsoft Docs
description: Lokale toepassingen toohello cloud met Azure AD-toepassingsproxy in de klassieke portal Hallo publiceren.
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: d94ac3f4-cd33-4c51-9d19-544a528637d4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/14/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro; oldportal
ms.openlocfilehash: 7926998314c65521ae48aebcceb33cb0c67e0b87
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="publish-applications-using-azure-ad-application-proxy"></a>Toepassingen publiceren met Azure AD-toepassingsproxy

> [!div class="op_single_selector"]
> * [Azure Portal](application-proxy-publish-azure-portal.md)
> * [Klassieke Azure Portal](active-directory-application-proxy-publish.md)

Azure AD-toepassingsproxy kunt u ondersteuning voor externe werknemers door het publiceren van lokale toepassingen toobe toegankelijk is via Hallo internet. Door dit punt, moet u al hebben [toepassingsproxy hebt ingeschakeld in de klassieke Azure-portal Hallo](active-directory-application-proxy-enable.md). Dit artikel begeleidt u bij Hallo stappen toopublish toepassingen die worden uitgevoerd op uw lokale netwerk en bieden veilige externe toegang van buiten uw netwerk. Nadat u dit artikel hebt voltooid, zult u gereed tooconfigure Hallo toepassing met persoonlijke gegevens of beveiligingsvereisten.

> [!NOTE]
> Toepassingsproxy is een functie die is alleen beschikbaar als u een upgrade hebt uitgevoerd toohello Premium of Basic-editie van Azure Active Directory. Zie [Azure Active Directory-edities](active-directory-editions.md) voor meer informatie. Als u wilt dat toouse toepassingsproxy, kunt u [toepassingen publiceren in Azure-portal Hallo](application-proxy-publish-azure-portal.md).

## <a name="publish-an-app-using-hello-wizard"></a>Een app publiceren met Hallo-wizard
1. Meld u aan als een beheerder in Hallo [klassieke Azure-portal](https://manage.windowsazure.com/).
2. Ga tooActive Directory en selecteer Hallo directory waarin u toepassingsproxy hebt ingeschakeld.
   
    ![Active Directory - pictogram](./media/active-directory-application-proxy-publish/ad_icon.png)
3. Klik op Hallo **toepassingen** tabblad en klik vervolgens op Hallo **toevoegen** knop aan de onderkant Hallo van welkomstscherm
   
    ![Toepassing toevoegen](./media/active-directory-application-proxy-publish/aad_appproxy_selectdirectory.png)
4. Selecteer **Een toepassing publiceren die toegankelijk is van buiten uw netwerk**.
   
    ![Een toepassing publiceren die toegankelijk is van buiten uw netwerk](./media/active-directory-application-proxy-publish/aad_appproxy_addapp.png)
5. Bieden de volgende informatie over uw toepassing hello:
   
   * **Naam**: Hallo gebruiksvriendelijke naam voor uw toepassing. Deze naam moet uniek zijn in uw directory.
   * **Interne URL**: Hallo-adres dat Hallo Connector voor toepassingsproxy gebruikt tooaccess Hallo-toepassing uit binnen uw particuliere netwerk. U kunt een specifiek pad opgeven op Hallo back-end server toopublish terwijl Hallo overige Hallo-server niet gepubliceerd is. Op deze manier kunt u verschillende sites publiceren op dezelfde server Hallo en elk een eigen naam en toegangsregels geven.
     
     > [!TIP]
     > Als u een pad publiceert, ervoor zorgen dat deze alle benodigde Hallo-installatiekopieën, scripts en StyleSheets voor uw toepassing bevat. Bijvoorbeeld, als uw app op https://yourapp/app is en zich bevindt op https://yourapp/media installatiekopieën gebruikt, moet vervolgens u publiceren https://yourapp/ als Hallo-pad.
     > 
     > 
   * **Methode voor verificatie vooraf**: hoe Application Proxy gebruikers worden geverifieerd voordat ze deze toegang tooyour application te geven. Kies een van Hallo opties in de vervolgkeuzelijst Hallo.
     
     * Azure Active Directory: Gebruikers toosign met Azure AD dat hun machtigingen geverifieerd voor Hallo directory en de toepassing wordt doorgestuurd door Application Proxy.
     * Passthrough: Gebruikers hebben geen tooauthenticate tooaccess Hallo toepassing.
     
     ![Toepassingseigenschappen](./media/active-directory-application-proxy-publish/aad_appproxy_appproperties.png)  
6. wizard toofinish hello, klikt u op het vinkje Hallo Hallo onder welkomstscherm aan. Hallo-toepassing is nu gedefinieerd in Azure AD.

## <a name="assign-users-and-groups-toohello-application"></a>Gebruikers en groepen toewijzen toohello toepassing
In volgorde voor uw gebruikers tooaccess uw gepubliceerde toepassing, moet u tooassign ze afzonderlijk of in groepen. (Houd er rekening mee tooassign zelf toegang te.) Elke gebruiker die u toewijst, moet beschikken over een licentie voor Azure Basic of hoger. U kunt licenties afzonderlijk toewijzen of toogroups. Zie voor meer informatie [toewijzen van gebruikers tooan toepassing](active-directory-applications-guiding-developers-assigning-users.md). 

Voor apps die verificatie vooraf is vereist, verleent een gebruiker toewijzen machtiging toouse Hallo toepassing. Voor apps die niet nodig vooraf-verificatie, toewijzing aan een gebruiker betekent dat die gebruiker Hallo hebben toegang tot de toepassing hello via Hallo Toegangsvenster.

1. Nadat de wizard voltooien Hallo-App toevoegen ziet u Hallo snel starten-pagina voor uw toepassing. toomanage wie heeft toegang tot toohello app, selecteer **gebruikers en groepen**.
   
    ![Toepassingsproxy - gebruikers toewijzen via Snel starten - schermafbeelding](./media/active-directory-application-proxy-publish/aad_appproxy_usersgroups.png)
2. Zoek naar specifieke groepen in uw directory of geef alle gebruikers weer. toodisplay hello zoekresultaten wilt weergeven, klikt u op Hallo selectievakje is ingeschakeld.
   
      ![Zoeken naar groepen of gebruikers - schermafbeelding](./media/active-directory-application-proxy-publish/aad_appproxy_search.png)
3. Selecteer elke gebruiker of groep die u wilt tooassign toothis app en klik op **toewijzen**. U bent tooconfirm gevraagd deze actie.

> [!NOTE]
> Voor apps met geïntegreerde Windows-verificatie kunt u alleen gebruikers en groepen toewijzen die zijn gesynchroniseerd vanuit uw on-premises Active Directory. Gebruikers die zich aanmelden met een Microsoft-account en gasten kunnen niet worden toegewezen aan apps die zijn gepubliceerd met Azure Active Directory-toepassingsproxy. Zorg ervoor dat uw gebruikers zich aanmelden met referenties die deel van Hallo uitmaken hetzelfde domein als het Hallo-app die u publiceert.
> 
> 

## <a name="test-your-published-application"></a>Uw gepubliceerde toepassing testen
Wanneer u uw toepassing hebt gepubliceerd, kunt u het eerst mee kunt testen door te navigeren toohello-URL die u hebt gepubliceerd. Zorg ervoor dat u toegang toe hebt tot uw toepassing, dat deze correct wordt weergegeven en dat alles werkt zoals verwacht. Als u problemen ondervindt bij het of er een foutbericht weergegeven, probeert u het Hallo [probleemoplossingsgids](active-directory-application-proxy-troubleshoot.md).

## <a name="configure-your-application"></a>Uw toepassing configureren
U kunt gepubliceerde apps aanpassen of geavanceerde opties op de pagina configureren Hallo instellen. Op deze pagina kunt u uw app aanpassen door de naam van de Hallo wijzigen of een logo te uploaden. U kunt ook toegangsregels zoals Hallo methode voor verificatie vooraf of meervoudige verificatie beheren.

![Geavanceerde configuratie](./media/active-directory-application-proxy-publish/aad_appproxy_configure.png)

Nadat u toepassingen publiceren met toepassingsproxy van Azure Active Directory, ze worden weergegeven in de lijst met Hallo-toepassingen in Azure AD en u kunt ze daar beheren.

Als u services voor toepassingsproxy uitschakelt nadat u toepassingen hebt gepubliceerd, zijn Hallo toepassingen niet langer toegankelijk van buiten uw particuliere netwerk. Uw gebruikers kunnen nog steeds toegang Hallo toepassingen on-premises zoals gebruikelijk.

tooview een toepassing en zorg ervoor dat deze toegankelijk is, dubbelklik op de naam van de toepassing hello Hallo. Als Hallo service voor toepassingsproxy is uitgeschakeld en de toepassing hello niet beschikbaar is, wordt een waarschuwing weergegeven Hallo boven aan het welkomstscherm.

toodelete een toepassing, selecteert u een toepassing in Hallo lijst en klik vervolgens op **verwijderen**.

## <a name="next-steps"></a>Volgende stappen
* [Toepassingen publiceren met uw eigen domeinnaam](active-directory-application-proxy-custom-domains.md)
* [Eenmalige aanmelding inschakelen](active-directory-application-proxy-sso-using-kcd.md)
* [Voorwaardelijke toegang inschakelen](active-directory-application-proxy-conditional-access.md)
* [Werken met claim-compatibele toepassingen](active-directory-application-proxy-claims-aware-apps.md)

Bekijk voor Hallo laatste nieuws en updates Hallo [blog over toepassingsproxy](http://blogs.technet.com/b/applicationproxyblog/)


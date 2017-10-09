---
title: aaaPublish apps met Azure AD-toepassingsproxy | Microsoft Docs
description: Lokale toepassingen toohello cloud met Azure AD-toepassingsproxy in hello Azure-portal publiceren.
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: d94ac3f4-cd33-4c51-9d19-544a528637d4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/23/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: ed5458467fb7d4376f65a222f1ba5f23cfdfc57c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="publish-applications-using-azure-ad-application-proxy"></a>Toepassingen publiceren met Azure AD-toepassingsproxy

> [!div class="op_single_selector"]
> * [Azure Portal](application-proxy-publish-azure-portal.md)
> * [Klassieke Azure Portal](active-directory-application-proxy-publish.md)

Toepassingsproxy van Azure Active Directory (AD) kunt u ondersteuning voor externe werknemers door het publiceren van lokale toepassingen toobe toegankelijk is via Hallo internet. U kunt deze u toepassingen publiceert via hello Azure portal tooprovide veilige externe toegang van buiten uw netwerk.

Dit artikel begeleidt u bij Hallo stappen toopublish een lokale app met toepassingsproxy. Nadat u dit artikel hebt voltooid, uw gebruikers zullen worden tooaccess kunnen uw app op afstand. En u bent klaar tooconfigure extra functies voor de toepassing hello zoals eenmalige aanmelding, persoonlijke gegevens en beveiligingsvereisten.

Als u nieuwe tooApplication Proxy, meer informatie over deze functie met Hallo artikel [hoe tooprovide veilige externe toegang tot het tooon-premises toepassingen](active-directory-application-proxy-get-started.md).


## <a name="publish-an-on-premises-app-for-remote-access"></a>Publiceren van een lokale app voor externe toegang

Volg deze stappen toopublish uw apps met Application Proxy. Als u dit nog niet hebt al gedownload en een connector voor uw organisatie hebt geconfigureerd, gaat u verder te[aan de slag met Application Proxy en het Hallo-connector installeert](active-directory-application-proxy-enable.md) eerste, en vervolgens uw app te publiceren.

> [!TIP]
> Als u uit toepassingsproxy voor Hallo eerst test, kiest u een toepassing die ingesteld voor verificatie op basis van wachtwoorden. Toepassingsproxy biedt ondersteuning voor andere soorten authenticatie, maar apps op basis van wachtwoorden Hallo eenvoudigste tooget up snel gebruiksklaar zijn. 

1. Meld u aan als een beheerder in Hallo [Azure-portal](https://portal.azure.com/).
2. Selecteer **Azure Active Directory** > **bedrijfstoepassingen** > **nieuwe toepassing**.

  ![Een zakelijke toepassing toevoegen](./media/application-proxy-publish-azure-portal/add-app.png)

3. Selecteer **alle**, selecteer daarna **On-premises toepassing**.  

  ![Uw eigen toepassing toevoegen](./media/application-proxy-publish-azure-portal/add-your-own.png)

4. Bieden de volgende informatie over uw toepassing hello:

   - **Naam**: Hallo-naam van Hallo-toepassing die wordt weergegeven op het toegangsvenster hello en in hello Azure-portal. 

   - **Interne URL**: Hallo URL die u de toepassing hello tooaccess van binnen uw particuliere netwerk gebruikt. U kunt een specifiek pad opgeven op Hallo back-end server toopublish terwijl Hallo overige Hallo-server niet gepubliceerd is. Op deze manier kunt u verschillende sites publiceren op dezelfde server als verschillende apps Hallo en elk een eigen naam en toegangsregels geven.

     > [!TIP]
     > Als u een pad publiceert, ervoor zorgen dat deze alle benodigde Hallo-installatiekopieën, scripts en StyleSheets voor uw toepassing bevat. Bijvoorbeeld, als uw app op https://yourapp/app is en zich bevindt op https://yourapp/media installatiekopieën gebruikt, moet vervolgens u publiceren https://yourapp/ als Hallo-pad. Deze interne URL geen toobe Hallo-startpagina die uw gebruikers te zien. Zie voor meer informatie [instellen van een aangepaste startpagina van gepubliceerde apps](application-proxy-office365-app-launcher.md).

   - **Externe URL**: Hallo adres uw gebruikers gaan tooin volgorde tooaccess Hallo-app van buiten uw netwerk. Als u niet dat toouse Hallo standaarddomein toepassingsproxy wilt, leest u over [aangepaste domeinen in Azure AD-toepassingsproxy](active-directory-application-proxy-custom-domains.md).
   - **Verificatie vooraf**: hoe Application Proxy gebruikers worden geverifieerd voordat ze deze toegang tooyour application te geven. 

     - Azure Active Directory: Gebruikers toosign met Azure AD dat hun machtigingen geverifieerd voor Hallo directory en de toepassing wordt doorgestuurd door Application Proxy. We raden deze optie als de standaard hello, zodat u van Azure AD-beveiligingsfuncties zoals voorwaardelijke toegang en multi-factor Authentication profiteren kunt.
     - Passthrough: Gebruikers hebben geen tooauthenticate voor Azure Active Directory tooaccess Hallo toepassing. U kunt nog steeds verificatievereisten op Hallo back-end instellen.
   - **Connector-groep**: Connectors proces Hallo RAS tooyour toepassings- en connector groepen te ordenen connectors en apps per regio, netwerk of doel. Als u een connector groepen die zijn gemaakt nog niet hebt, uw app te toegewezen**standaard**.

   ![Uw toepassing configureren](./media/application-proxy-publish-azure-portal/configure-app.png)
5. Indien nodig, extra instellingen configureren. Voor de meeste toepassingen, moet u deze instellingen behouden de standaardwaarden hebben. 
   - **Back-end toepassing time-out**: Stel deze waarde te**lang** alleen als uw toepassing is tooauthenticate vertragen en verbinding maken. 
   - **URL's in de Headers vertalen**: deze waarde als behouden **Ja** tenzij uw toepassing hello oorspronkelijke host-header in de verificatieaanvraag Hallo vereist.
   - **URL's in de hoofdtekst van de toepassing te vertalen**: deze waarde als behouden **Nee** tenzij u hardcoded HTML koppelingen tooother on-premises toepassingen hebben en geen aangepaste domeinen gebruiken. Zie voor meer informatie [koppelen vertaling met toepassingsproxy](application-proxy-link-translation.md).
   
   ![Uw toepassing configureren](./media/application-proxy-publish-azure-portal/additional-settings.png)

6. Selecteer **Toevoegen**.


## <a name="add-a-test-user"></a>Een testgebruiker toevoegen 

tootest dat uw app correct is gepubliceerd een test-gebruikersaccount toevoegen. Controleer of dit account heeft al machtigingen tooaccess Hallo-app uit binnen het bedrijfsnetwerk Hallo.

1. Selecteer terug op de blade snel starten Hallo **een gebruiker toewijzen voor het testen van**.

  ![Een gebruiker toewijzen voor het testen](./media/application-proxy-publish-azure-portal/assign-user.png)

2. Selecteer op het Hallo-gebruikers en groepen blade, **toevoegen**.

  ![Een gebruiker of groep toevoegen](./media/application-proxy-publish-azure-portal/add-user.png)

3. Selecteer op het tabblad van het Hallo toevoegen toewijzing **gebruikers en groepen** kies vervolgens de gewenste tooadd Hallo-account. 
4. Selecteer **toewijzen**.

## <a name="test-your-published-app"></a>Uw gepubliceerde app testen

Navigeer in uw browser toohello externe URL die u hebt geconfigureerd tijdens het Hallo stap publiceren. U ziet het startscherm Hallo en kunnen toosign worden met Hallo testaccount instellen van.

![Uw gepubliceerde app testen](./media/application-proxy-publish-azure-portal/test-app.png)


## <a name="next-steps"></a>Volgende stappen
- [Downloaden van connectors](active-directory-application-proxy-enable.md) en [connector groepen maken](active-directory-application-proxy-connectors-azure-portal.md) toopublish toepassingen op afzonderlijke netwerken en locaties.

- [Instellen van eenmalige aanmelding](application-proxy-sso-azure-portal.md) voor uw zojuist gepubliceerde app

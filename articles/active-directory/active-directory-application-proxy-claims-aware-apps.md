---
title: aaaClaims-compatibele apps - toepassingsproxy van Azure AD | Microsoft Docs
description: Hoe toopublish een on-premises ASP.NET-toepassingen die AD FS-claims voor veilige externe toegang door uw gebruikers te accepteren.
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
editor: harshja
ms.assetid: 91e6211b-fe6a-42c6-bdb3-1fff0312db15
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: kgremban
ms.openlocfilehash: 7be633225de700226c7c94815eb91b3de2b61cb5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="working-with-claims-aware-apps-in-application-proxy"></a>Werken met claimbewuste toepassingen in de toepassingsproxy
[Claims-compatibele apps](https://msdn.microsoft.com/library/windows/desktop/bb736227.aspx) een omleiding toohello Security Token Service (STS) uitvoeren. Hallo STS vraagt om de referenties van gebruiker Hallo voor een token en stuurt vervolgens door Hallo-Gebruikerstoepassing toohello. Er zijn enkele manieren tooenable toepassingsproxy toowork met deze omleidingen. Gebruik dit artikel tooconfigure uw implementatie voor claims-compatibele apps. 

## <a name="prerequisites"></a>Vereisten
Zorg ervoor dat Hallo STS die Hallo claimbewuste app leidt toois beschikbaar buiten uw on-premises netwerk. U kunt Hallo STS beschikbaar maken door het beschikbaar te maken via een proxy of door ze buiten verbindingen. 

## <a name="publish-your-application"></a>Uw toepassing publiceren

1. Publiceer de toepassing op basis van toohello instructies die worden beschreven [publiceren van toepassingen met toepassingsproxy](application-proxy-publish-azure-portal.md).
2. Navigeer toohello toepassingspagina in Hallo portal en selecteert u een **eenmalige aanmelding**.
3. Als u hebt gekozen **Azure Active Directory** als uw **pre-authenticatie methode**, selecteer **Azure AD eenmalige aanmelding uitgeschakeld** als uw **intern Verificatiemethode**. Als u hebt gekozen **Passthrough** als uw **pre-authenticatie methode**, hoeft u niet toochange alles.

## <a name="configure-adfs"></a>AD FS configureren

U kunt AD FS voor claims-compatibele apps op twee manieren configureren. Hallo wordt eerst met behulp van aangepaste domeinen. Hallo is het tweede met WS-Federation. 

### <a name="option-1-custom-domains"></a>Optie 1: Aangepaste domeinen

Als alle Hallo interne URL's voor uw toepassingen volledig gekwalificeerde zijn domeinnamen (FQDN's), dan kunt u configureren [aangepaste domeinen](active-directory-application-proxy-custom-domains.md) voor uw toepassingen. Gebruik Hallo aangepaste domeinen toocreate externe URL's die zijn hetzelfde als de interne URL's Hallo Hallo. Als de externe URL's die overeenkomen met uw interne URL's, werken Hallo STS omleidingen of uw gebruikers on-premises of extern zijn. 

### <a name="option-2-ws-federation"></a>Optie 2: WS-Federation

1. Open AD FS-beheer.
2. Ga te**Relying Party-vertrouwensrelaties**, met de rechtermuisknop op het Hallo-app die u met toepassingsproxy publiceren wilt en kiest u **eigenschappen**.  

   ![Relying Party-vertrouwensrelaties met de rechtermuisknop op de naam van de app - schermafbeelding](./media/active-directory-application-proxy-claims-aware-apps/appproxyrelyingpartytrust.png)  

3. Op Hallo **eindpunten** tabblad onder **eindpunttype**, selecteer **WS-Federation**.
4. Onder **vertrouwde URL**, Voer Hallo-URL die u hebt ingevoerd in Hallo toepassingsproxy onder **externe URL** en klik op **OK**.  

   ![Toevoegen van een eindpunt - waarde vertrouwde URL - schermafbeelding](./media/active-directory-application-proxy-claims-aware-apps/appproxyendpointtrustedurl.png)  

## <a name="next-steps"></a>Volgende stappen
* [Schakel eenmalige aanmelding op](application-proxy-sso-overview.md) voor toepassingen die niet claimbewuste
* [Native client-apps toointeract met proxy toepassingen inschakelen](active-directory-application-proxy-native-client.md)



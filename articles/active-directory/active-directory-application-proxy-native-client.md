---
title: aaaPublish native client-apps - Azure AD | Microsoft Docs
description: Bevat informatie over hoe tooenable native client-apps toocommunicate met Azure AD-Application Proxy Connector tooprovide veilige externe toegang tooyour lokale apps.
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: f0cae145-e346-4126-948f-3f699747b96e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 0ed2be217bf992f034d8321d5e66569b4cace24f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooenable-native-client-apps-toointeract-with-proxy-applications"></a>Hoe tooenable native client-apps toointeract met proxy toepassingen

Azure Active Directory-toepassingsproxy kan toevoeging tooweb toepassingen, ook gebruikte toopublish native client-apps worden. Native client-apps verschillen van web-apps, omdat ze zijn geïnstalleerd op een apparaat, terwijl de web-apps via een browser worden geopend. 

Toepassingsproxy ondersteunt native client-apps door overnemende Azure AD uitgegeven tokens die standaard autoriseren HTTP-headers zijn verzonden.

![Relatie tussen eindgebruikers, Azure Active Directory en gepubliceerde toepassingen](./media/active-directory-application-proxy-native-client/richclientflow.png)

Hello Azure AD-Verificatiebibliotheek, die zorgt voor verificatie en biedt ondersteuning voor veel client omgevingen, toopublish systeemeigen toepassingen gebruiken. Toepassingsproxy in Hallo past [systeemeigen toepassing tooWeb API scenario](develop/active-directory-authentication-scenarios.md#native-application-to-web-api). Dit artikel begeleidt u bij Hallo vier stappen toopublish een systeemeigen toepassing met toepassingsproxy en hello Azure AD Authentication Library. 

## <a name="step-1-publish-your-application"></a>Stap 1: Uw toepassing publiceren
Uw proxy-toepassing te publiceren, net als elke andere toepassing en toewijzen van gebruikers tooaccess uw toepassing. Zie voor meer informatie [publiceren van toepassingen met toepassingsproxy](active-directory-application-proxy-publish.md).

## <a name="step-2-configure-your-application"></a>Stap 2: Uw toepassing configureren
Uw eigen toepassing als volgt configureren:

1. Meld u aan toohello [Azure-portal](https://portal.azure.com).
2. Navigeer te**Azure Active Directory** > **App registraties**.
3. Selecteer **registratie van de nieuwe toepassing**.
4. Geef een naam voor uw toepassing, selecteert **systeemeigen** als het toepassingstype hello, en geef Hallo omleidings-URI voor uw toepassing. 

   ![Maak een nieuwe app-registratie](./media/active-directory-application-proxy-native-client/create.png)
5. Selecteer **Maken**.

Zie voor meer informatie over het maken van een nieuwe app-registratie, [toepassingen integreren met Azure Active Directory](.//develop/active-directory-integrating-applications.md).


## <a name="step-3-grant-access-tooother-applications"></a>Stap 3: Verlenen toegang tooother toepassingen
Hallo systeemeigen toepassing toobe blootgesteld tooother toepassingen in uw directory inschakelen:

1. Nog steeds in **App registraties**, selecteer Hallo nieuwe systeemeigen toepassing die u zojuist hebt gemaakt.
2. Selecteer **vereist machtigingen**.
3. Selecteer **Toevoegen**.
4. Eerste stap van de Open Hallo **selecteert u een API**.
5. Hallo zoeken balk toofind Hallo toepassingsproxy app gebruiken die u hebt gepubliceerd in de eerste sectie Hallo. Kies deze app en klik vervolgens op **Selecteer**. 

   ![Zoeken naar Hallo proxy app](./media/active-directory-application-proxy-native-client/select_api.png)
6. Tweede stap van de Open Hallo **machtigingen selecteren**.
7. Hallo selectievakje toogrant uw toepassing systeemeigen toepassing toegang tooyour proxy gebruiken en klik vervolgens op **Selecteer**.

   ![Verleen toegang tooproxy app](./media/active-directory-application-proxy-native-client/select_perms.png)
8. Selecteer **gedaan**.


## <a name="step-4-edit-hello-active-directory-authentication-library"></a>Stap 4: Hallo Active Directory Authentication Library bewerken
Hallo systeemeigen toepassingscode bewerken in Hallo authentication context Hallo Active Directory Authentication Library (ADAL) tooinclude Hallo volgende tekst:

```
// Acquire Access Token from AAD for Proxy Application
AuthenticationContext authContext = new AuthenticationContext("https://login.microsoftonline.com/<Tenant ID>");
AuthenticationResult result = authContext.AcquireToken("< External Url of Proxy App >",
        "<App ID of hello Native app>",
        new Uri("<Redirect Uri of hello Native App>"),
        PromptBehavior.Never);

//Use hello Access Token tooaccess hello Proxy Application
HttpClient httpClient = new HttpClient();
httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", result.AccessToken);
HttpResponseMessage response = await httpClient.GetAsync("< Proxy App API Url >");
```

Hallo variabelen in de voorbeeldcode hello wordt vervangen als volgt:

* **Tenant-ID** vindt u in hello Azure-portal. Navigeer te**Azure Active Directory** > **eigenschappen** en kopiëren Hallo Directory-ID. 
* **Externe URL** Hallo front-URL die u hebt ingevoerd in de Proxy-toepassing hello is. toofind dit waarde, navigeer toohello **toepassingsproxy** sectie van Hallo proxy app.
* **App-ID** Hallo systeemeigen app vindt u op Hallo **eigenschappen** pagina van de systeemeigen toepassing hello.
* **Omleidings-URI van de systeemeigen app Hallo** vindt u op Hallo **omleidings-URI's** pagina van de systeemeigen toepassing hello.


## <a name="see-also"></a>Zie ook

Zie voor meer informatie over Hallo systeemeigen toepassing stroom [systeemeigen toepassing tooweb API](develop/active-directory-authentication-scenarios.md#native-application-to-web-api)

Bekijk voor Hallo laatste nieuws en updates Hallo [blog over toepassingsproxy](http://blogs.technet.com/b/applicationproxyblog/)

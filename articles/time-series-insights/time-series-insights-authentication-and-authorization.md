---
title: aaaConfigure verificatie en autorisatie voor een aangepaste toepassing die aanroept hello Azure Time Series Insights-API | Microsoft Docs
description: Deze zelfstudie wordt uitgelegd hoe tooconfigure verificatie en autorisatie voor een aangepaste toepassing die aanroept hello Azure Time Series Insights-API
keywords: 
services: time-series-insights
documentationcenter: 
author: dmdenmsft
manager: almineev
editor: cgronlun
ms.assetid: 
ms.service: time-series-insights
ms.devlang: na
ms.topic: how-to-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/24/2017
ms.author: dmden
ms.openlocfilehash: 5043468bfc2af3c0d27e8602508d92ba2848409e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="authentication-and-authorization-for-azure-time-series-insights-api"></a>Verificatie en autorisatie voor Azure Time Series Insights-API

Dit artikel wordt uitgelegd hoe een aangepaste toepassing die aanroept tooconfigure inzicht API van Azure Time Series Hallo.

## <a name="service-principal"></a>Service-principal

Deze sectie wordt uitgelegd hoe een toepassing tooaccess tooconfigure Time Series inzicht API Hallo namens de toepassing hello. Hallo-toepassing kunt vervolgens gegevens opvragen of referentiegegevens publiceren in Hallo Time Series Insights omgeving met referenties van de toepassing en geen Hallo gebruikersreferenties.

Wanneer u een toepassing die tooaccess Time Series inzichten nodig hebt, moet u een Azure Active Directory-toepassing instellen en toewijzen van Hallo gegevenstoegangsbeleid in Hallo Time Series Insights omgeving. Deze aanpak is beter toorunning Hallo app met uw eigen referenties, omdat:

* U kunt machtigingen toohello app identiteit die afwijken van uw eigen machtigingen toewijzen. Deze machtigingen zijn normaal gesproken beperkt tooexactly welke app Hallo moet toodo. U kunt bijvoorbeeld toestaan Hallo app tooonly lezen van gegevens in een bepaalde tijd reeks Insights-omgeving.
* U hebt geen toochange Hallo app referenties als uw verantwoordelijkheden wijzigt.
* U kunt een certificaat of een toepassing sleutel tooautomate authenticatie gebruiken wanneer u een script zonder toezicht uitvoert.

Dit artikel laat zien hoe deze stappen via tooperform hello Azure-portal. Het is gericht op een één-tenant-toepassing waarbij de toepassing hello beoogde toorun in slechts één organisatie is. Doorgaans gebruikt u toepassingen voor één tenant voor line-of-business-toepassingen die worden uitgevoerd in uw organisatie.

Hallo setup stroom bestaat uit drie hoofdstappen:

1. Een toepassing maakt in Azure Active Directory.
2. Toestaan dat deze toepassing tooaccess Hallo Time Series Insights-omgeving.
3. Gebruik Hallo toepassings-ID en sleutel tooacquire een token toohello `"https://api.timeseries.azure.com/"` doelgroep of resource. Hallo-token kan vervolgens worden gebruikte toocall Hallo Time Series Insights-API.

Hier volgen gedetailleerde stappen Hallo:

1. Selecteer in de Azure-portal Hallo, **Azure Active Directory** > **App registraties** > **registratie van de nieuwe toepassing**.

   ![Registratie van de nieuwe toepassing in Azure Active Directory](media/authentication-and-authorization/active-directory-new-application-registration.png)  

2. Hallo-toepassing een naam, selecteer Hallo type toobe geven **Web-app / API**, selecteer een geldige URI voor **aanmeldings-URL**, en klik op **maken**.

   ![Hallo-toepassing maken in Azure Active Directory](media/authentication-and-authorization/active-directory-create-web-api-application.png)

3. Uw nieuwe toepassing selecteren en kopiëren van de toepassing-ID tooyour favoriete teksteditor.

   ![Kopieer Hallo toepassings-ID](media/authentication-and-authorization/active-directory-copy-application-id.png)

4. Selecteer **sleutels**, Voer Hallo sleutelnaam, selecteer Hallo verlopen, en klik op **opslaan**.

   ![Sleutels van de toepassing selecteren](media/authentication-and-authorization/active-directory-application-keys.png)

   ![Hallo-sleutelnaam en verlopen en klik op Opslaan](media/authentication-and-authorization/active-directory-application-keys-save.png)

5. Kopieer Hallo sleutel tooyour favoriete teksteditor.

   ![Kopieer de sleutel van de toepassing hello](media/authentication-and-authorization/active-directory-copy-application-key.png)

6. Selecteer Hallo Time Series Insights omgeving **Gegevenstoegangsbeleid** en klik op **toevoegen**.

   ![Toevoegen van nieuwe data access-beleid toohello Time Series Insights-omgeving](media/authentication-and-authorization/time-series-insights-data-access-policies-add.png)

7. In Hallo **gebruiker selecteren** in het dialoogvenster, plakken Hallo toepassingsnaam (uit stap 2) of toepassings-ID (uit stap 3).

   ![Een toepassing niet vinden in het dialoogvenster voor Hallo gebruiker selecteren](media/authentication-and-authorization/time-series-insights-data-access-policies-select-user.png)

8. Selecteer Hallo-rol (**lezer** voor het opvragen van gegevens, **Inzender** voor het opvragen van gegevens en het wijzigen van referentiegegevens) en klik op **Ok**.

   ![Lezer of bijdrager kiezen in het dialoogvenster van Hallo rol selecteren](media/authentication-and-authorization/time-series-insights-data-access-policies-select-role.png)

9. Hallo beleid opslaan door te klikken op **Ok**.

10. Hallo toepassings-ID (uit stap 3) en de toepassing (uit stap 5) sleutel tooacquire Hallo token namens de toepassing hello gebruiken. Hallo token kan vervolgens worden doorgegeven in Hallo `Authorization` header bij het aanroepen van de toepassing hello Hallo Time Series Insights-API.

    Als u van C# gebruikmaakt, kunt u de volgende code tooacquire Hallo token namens Hallo toepassing hello kunt gebruiken. Zie voor een compleet codevoorbeeld [opvragen van gegevens met C#](time-series-insights-query-data-csharp.md).

    ```csharp
    var authenticationContext = new AuthenticationContext(
        "https://login.microsoftonline.com/common",
        TokenCache.DefaultShared);

    AuthenticationResult token = await authenticationContext.AcquireTokenAsync(
        // Set hello resource URI toohello Azure Time Series Insights API
        resource: "https://api.timeseries.azure.com/", 
        clientCredential: new ClientCredential(
            // Application ID of application registered in Azure Active Directory
            clientId: "1bc3af48-7e2f-4845-880a-c7649a6470b8", 
            // Application key of hello application that's registered in Azure Active Directory
            clientSecret: "aBcdEffs4XYxoAXzLB1n3R2meNCYdGpIGBc2YC5D6L2="));

    string accessToken = token.AccessToken;
    ```

## <a name="next-steps"></a>Volgende stappen

Hallo toepassings-ID en sleutel gebruiken in uw toepassing. Zie voor een voorbeeld van code die Hallo Time Series Insights-API aanroept, [opvragen van gegevens met C#](time-series-insights-query-data-csharp.md).

## <a name="see-also"></a>Zie ook

* [Query uitvoeren op API](/rest/api/time-series-insights/time-series-insights-reference-queryapi) voor Hallo volledige Query API-referentiemateriaal
* [Maken van een service principal in hello Azure-portal](../azure-resource-manager/resource-group-create-service-principal-portal.md)

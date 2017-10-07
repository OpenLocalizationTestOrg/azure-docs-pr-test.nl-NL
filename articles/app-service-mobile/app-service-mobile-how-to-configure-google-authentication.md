---
title: aaaHow tooconfigure Google-verificatie voor uw toepassing App Services
description: Meer informatie over hoe tooconfigure Google-verificatie voor uw App Services-toepassing.
services: app-service
documentationcenter: 
author: mattchenderson
manager: syntaxc4
editor: 
ms.assetid: 2b2f9abf-9120-4aac-ac5b-4a268d9b6e2b
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 10/01/2016
ms.author: mahender
ms.openlocfilehash: 9175c40b78c859e9e191504c41cd0bb9a3380ccd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-your-app-service-application-toouse-google-login"></a><span data-ttu-id="8274e-103">Hoe tooconfigure uw App Service-toepassing toouse Google aanmelding</span><span class="sxs-lookup"><span data-stu-id="8274e-103">How tooconfigure your App Service application toouse Google login</span></span>
[!INCLUDE [app-service-mobile-selector-authentication](../../includes/app-service-mobile-selector-authentication.md)]

<span data-ttu-id="8274e-104">Dit onderwerp leest u hoe tooconfigure Azure App Service toouse Google als een verificatieprovider.</span><span class="sxs-lookup"><span data-stu-id="8274e-104">This topic shows you how tooconfigure Azure App Service toouse Google as an authentication provider.</span></span>

<span data-ttu-id="8274e-105">toocomplete Hallo-procedure in dit onderwerp, moet u een Google-account met een geverifieerde e-mailadres hebben.</span><span class="sxs-lookup"><span data-stu-id="8274e-105">toocomplete hello procedure in this topic, you must have a Google account that has a verified email address.</span></span> <span data-ttu-id="8274e-106">toocreate een nieuw Google-account, gaat u te[accounts.google.com](http://go.microsoft.com/fwlink/p/?LinkId=268302).</span><span class="sxs-lookup"><span data-stu-id="8274e-106">toocreate a new Google account, go too[accounts.google.com](http://go.microsoft.com/fwlink/p/?LinkId=268302).</span></span>

## <span data-ttu-id="8274e-107"><a name="register"></a>Uw toepassing registreren met Google</span><span class="sxs-lookup"><span data-stu-id="8274e-107"><a name="register"> </a>Register your application with Google</span></span>
1. <span data-ttu-id="8274e-108">Meld u aan toohello [Azure-portal], en ga tooyour toepassing.</span><span class="sxs-lookup"><span data-stu-id="8274e-108">Log on toohello [Azure portal], and navigate tooyour application.</span></span> <span data-ttu-id="8274e-109">Kopieer uw **URL**, die u later tooconfigure uw Google-app gebruiken.</span><span class="sxs-lookup"><span data-stu-id="8274e-109">Copy your **URL**, which you use later tooconfigure your Google app.</span></span>
2. <span data-ttu-id="8274e-110">Navigeer toohello [Google API's](http://go.microsoft.com/fwlink/p/?LinkId=268303) website, meld u aan met de referenties van uw Google-account, klikt u op **Project maken**, bieden een **projectnaam**, klikt u vervolgens op  **Maak**.</span><span class="sxs-lookup"><span data-stu-id="8274e-110">Navigate toohello [Google apis](http://go.microsoft.com/fwlink/p/?LinkId=268303) website, sign in with your Google account credentials, click **Create Project**, provide a **Project name**, then click **Create**.</span></span>
3. <span data-ttu-id="8274e-111">Onder **sociale API's** klikt u op **Google + API** en vervolgens **inschakelen**.</span><span class="sxs-lookup"><span data-stu-id="8274e-111">Under **Social APIs** click **Google+ API** and then **Enable**.</span></span>
4. <span data-ttu-id="8274e-112">In de linkernavigatiebalk, Hallo **referenties** > **OAuth toestemming scherm**, selecteer vervolgens uw **e-mailadres**, voer een **Productnaam**, en klik op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="8274e-112">In hello left navigation, **Credentials** > **OAuth consent screen**, then select your **Email address**,  enter a **Product Name**, and click **Save**.</span></span>
5. <span data-ttu-id="8274e-113">In Hallo **referenties** tabblad **referenties maken** > **OAuth-Clientidentiteit**, selecteer daarna **webtoepassing**.</span><span class="sxs-lookup"><span data-stu-id="8274e-113">In hello **Credentials** tab, click **Create credentials** > **OAuth client ID**, then select **Web application**.</span></span>
6. <span data-ttu-id="8274e-114">Plakken Hallo App Service **URL** u eerder hebt gekopieerd in **geautoriseerd JavaScript oorsprongen**, plak uw redirect URI in **omleidings-URI is gemachtigd**.</span><span class="sxs-lookup"><span data-stu-id="8274e-114">Paste hello App Service **URL** you copied earlier into **Authorized JavaScript Origins**, then paste your redirect URI into **Authorized Redirect URI**.</span></span> <span data-ttu-id="8274e-115">Omleidings-URI Hallo-URL van uw toepassing met het Hallo-pad toegevoegd is Hallo */.auth/login/google/callback*.</span><span class="sxs-lookup"><span data-stu-id="8274e-115">hello redirect URI is hello URL of your application appended with hello path, */.auth/login/google/callback*.</span></span> <span data-ttu-id="8274e-116">Bijvoorbeeld `https://contoso.azurewebsites.net/.auth/login/google/callback`.</span><span class="sxs-lookup"><span data-stu-id="8274e-116">For example, `https://contoso.azurewebsites.net/.auth/login/google/callback`.</span></span> <span data-ttu-id="8274e-117">Zorg ervoor dat u van Hallo HTTPS-schema gebruikmaakt.</span><span class="sxs-lookup"><span data-stu-id="8274e-117">Make sure that you are using hello HTTPS scheme.</span></span> <span data-ttu-id="8274e-118">Klik vervolgens op **Maken**.</span><span class="sxs-lookup"><span data-stu-id="8274e-118">Then click **Create**.</span></span>
7. <span data-ttu-id="8274e-119">Op het volgende scherm hello, noteer Hallo waarden van Hallo client-ID en client geheim.</span><span class="sxs-lookup"><span data-stu-id="8274e-119">On hello next screen, make a note of hello values of hello client ID and client secret.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="8274e-120">Hallo clientgeheim is een belangrijke beveiligingsreferentie.</span><span class="sxs-lookup"><span data-stu-id="8274e-120">hello client secret is an important security credential.</span></span> <span data-ttu-id="8274e-121">Dit geheim met anderen delen of deze te distribueren vanuit een clienttoepassing niet.</span><span class="sxs-lookup"><span data-stu-id="8274e-121">Do not share this secret with anyone or distribute it within a client application.</span></span>


## <span data-ttu-id="8274e-122"><a name="secrets"></a>Toevoegen Google informatie tooyour toepassing</span><span class="sxs-lookup"><span data-stu-id="8274e-122"><a name="secrets"> </a>Add Google information tooyour application</span></span>
1. <span data-ttu-id="8274e-123">Terug in Hallo [Azure-portal], tooyour toepassing navigeren.</span><span class="sxs-lookup"><span data-stu-id="8274e-123">Back in hello [Azure portal], navigate tooyour application.</span></span> <span data-ttu-id="8274e-124">Klik op **instellingen**, en vervolgens **verificatie / autorisatie**.</span><span class="sxs-lookup"><span data-stu-id="8274e-124">Click **Settings**, and then **Authentication / Authorization**.</span></span>
2. <span data-ttu-id="8274e-125">Als Hallo verificatie / autorisatie-functie niet is ingeschakeld, schakelt u Hallo switch te**op**.</span><span class="sxs-lookup"><span data-stu-id="8274e-125">If hello Authentication / Authorization feature is not enabled, turn hello switch too**On**.</span></span>
3. <span data-ttu-id="8274e-126">Klik op **Google**.</span><span class="sxs-lookup"><span data-stu-id="8274e-126">Click **Google**.</span></span> <span data-ttu-id="8274e-127">Plak in Hallo App-ID en App-geheim waarden die u eerder hebt verkregen en optioneel in staat alle scopes die vereist zijn voor uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="8274e-127">Paste in hello App ID and App Secret values which you obtained previously, and optionally enable any scopes your application requires.</span></span> <span data-ttu-id="8274e-128">Klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="8274e-128">Then click **OK**.</span></span>
   
   ![][1]
   
   <span data-ttu-id="8274e-129">Standaard-App Service biedt verificatie maar niet beperkt geautoriseerde toegang tooyour site-inhoud en API's.</span><span class="sxs-lookup"><span data-stu-id="8274e-129">By default, App Service provides authentication but does not restrict authorized access tooyour site content and APIs.</span></span> <span data-ttu-id="8274e-130">U moet gebruikers machtigen in uw app-code.</span><span class="sxs-lookup"><span data-stu-id="8274e-130">You must authorize users in your app code.</span></span>
4. <span data-ttu-id="8274e-131">(Optioneel) toorestrict toegang tooyour site tooonly gebruikers zijn geverifieerd door Google en ingesteld **tootake actie wanneer de aanvraag is niet geverifieerd** te**Google**.</span><span class="sxs-lookup"><span data-stu-id="8274e-131">(Optional) toorestrict access tooyour site tooonly users authenticated by Google, set **Action tootake when request is not authenticated** too**Google**.</span></span> <span data-ttu-id="8274e-132">Dit vereist dat alle aanvragen worden geverifieerd en alle niet-geverifieerde aanvragen worden omgeleid tooGoogle voor verificatie.</span><span class="sxs-lookup"><span data-stu-id="8274e-132">This requires that all requests be authenticated, and all unauthenticated requests are redirected tooGoogle for authentication.</span></span>
5. <span data-ttu-id="8274e-133">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="8274e-133">Click **Save**.</span></span>

<span data-ttu-id="8274e-134">U bent nu klaar toouse Google voor verificatie in uw app.</span><span class="sxs-lookup"><span data-stu-id="8274e-134">You are now ready toouse Google for authentication in your app.</span></span>

## <span data-ttu-id="8274e-135"><a name="related-content"></a>Verwante inhoud</span><span class="sxs-lookup"><span data-stu-id="8274e-135"><a name="related-content"> </a>Related Content</span></span>
[!INCLUDE [app-service-mobile-related-content-get-started-users](../../includes/app-service-mobile-related-content-get-started-users.md)]

<!-- Anchors. -->

<!-- Images. -->

[0]: ./media/app-service-mobile-how-to-configure-google-authentication/mobile-app-google-redirect.png
[1]: ./media/app-service-mobile-how-to-configure-google-authentication/mobile-app-google-settings.png

<!-- URLs. -->

[Google apis]: http://go.microsoft.com/fwlink/p/?LinkId=268303

[Azure-portal]: https://portal.azure.com/


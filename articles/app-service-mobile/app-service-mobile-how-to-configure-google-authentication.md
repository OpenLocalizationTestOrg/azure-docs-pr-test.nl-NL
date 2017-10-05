---
title: Het configureren van Google-verificatie voor uw toepassing App Services
description: Informatie over het configureren van Google-verificatie voor uw App Services-toepassing.
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
ms.openlocfilehash: d6c1707f67d986487e5a45e76ffc9a02ddf16eb1
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-configure-your-app-service-application-to-use-google-login"></a><span data-ttu-id="1f701-103">Het configureren van uw App Service-toepassing gebruik van Google aanmelding</span><span class="sxs-lookup"><span data-stu-id="1f701-103">How to configure your App Service application to use Google login</span></span>
[!INCLUDE [app-service-mobile-selector-authentication](../../includes/app-service-mobile-selector-authentication.md)]

<span data-ttu-id="1f701-104">Dit onderwerp leest u over het configureren van Azure App Service voor het gebruik van Google als een verificatieprovider.</span><span class="sxs-lookup"><span data-stu-id="1f701-104">This topic shows you how to configure Azure App Service to use Google as an authentication provider.</span></span>

<span data-ttu-id="1f701-105">U moet een Google-account met een geverifieerde e-mailadres hebben voor de procedure in dit onderwerp.</span><span class="sxs-lookup"><span data-stu-id="1f701-105">To complete the procedure in this topic, you must have a Google account that has a verified email address.</span></span> <span data-ttu-id="1f701-106">Als u een nieuw Google-account wilt maken, gaat u naar [accounts.google.com](http://go.microsoft.com/fwlink/p/?LinkId=268302).</span><span class="sxs-lookup"><span data-stu-id="1f701-106">To create a new Google account, go to [accounts.google.com](http://go.microsoft.com/fwlink/p/?LinkId=268302).</span></span>

## <span data-ttu-id="1f701-107"><a name="register"></a>Uw toepassing registreren met Google</span><span class="sxs-lookup"><span data-stu-id="1f701-107"><a name="register"> </a>Register your application with Google</span></span>
1. <span data-ttu-id="1f701-108">Meld u aan bij de [Azure-portal], en navigeer naar uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="1f701-108">Log on to the [Azure portal], and navigate to your application.</span></span> <span data-ttu-id="1f701-109">Kopieer uw **URL**, die u later gebruiken voor het configureren van uw Google-app.</span><span class="sxs-lookup"><span data-stu-id="1f701-109">Copy your **URL**, which you use later to configure your Google app.</span></span>
2. <span data-ttu-id="1f701-110">Navigeer naar de [Google API's](http://go.microsoft.com/fwlink/p/?LinkId=268303) website, meld u aan met de referenties van uw Google-account, klikt u op **Project maken**, bieden een **projectnaam**, klikt u vervolgens op **maken**.</span><span class="sxs-lookup"><span data-stu-id="1f701-110">Navigate to the [Google apis](http://go.microsoft.com/fwlink/p/?LinkId=268303) website, sign in with your Google account credentials, click **Create Project**, provide a **Project name**, then click **Create**.</span></span>
3. <span data-ttu-id="1f701-111">Onder **sociale API's** klikt u op **Google + API** en vervolgens **inschakelen**.</span><span class="sxs-lookup"><span data-stu-id="1f701-111">Under **Social APIs** click **Google+ API** and then **Enable**.</span></span>
4. <span data-ttu-id="1f701-112">In het linkernavigatievenster **referenties** > **OAuth toestemming scherm**, selecteer vervolgens uw **e-mailadres**, voer een **Productnaam**, en klik op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="1f701-112">In the left navigation, **Credentials** > **OAuth consent screen**, then select your **Email address**,  enter a **Product Name**, and click **Save**.</span></span>
5. <span data-ttu-id="1f701-113">In de **referenties** tabblad **referenties maken** > **OAuth-Clientidentiteit**, selecteer daarna **webtoepassing**.</span><span class="sxs-lookup"><span data-stu-id="1f701-113">In the **Credentials** tab, click **Create credentials** > **OAuth client ID**, then select **Web application**.</span></span>
6. <span data-ttu-id="1f701-114">Plak de App Service **URL** u eerder hebt gekopieerd in **geautoriseerd JavaScript oorsprongen**, plak uw omleiding URI in **geautoriseerd omleidings-URI**.</span><span class="sxs-lookup"><span data-stu-id="1f701-114">Paste the App Service **URL** you copied earlier into **Authorized JavaScript Origins**, then paste your redirect URI into **Authorized Redirect URI**.</span></span> <span data-ttu-id="1f701-115">De omleidings-URI is de URL van uw toepassing toegevoegd aan het pad */.auth/login/google/callback*.</span><span class="sxs-lookup"><span data-stu-id="1f701-115">The redirect URI is the URL of your application appended with the path, */.auth/login/google/callback*.</span></span> <span data-ttu-id="1f701-116">Bijvoorbeeld `https://contoso.azurewebsites.net/.auth/login/google/callback`.</span><span class="sxs-lookup"><span data-stu-id="1f701-116">For example, `https://contoso.azurewebsites.net/.auth/login/google/callback`.</span></span> <span data-ttu-id="1f701-117">Zorg ervoor dat u van het HTTPS-schema gebruikmaakt.</span><span class="sxs-lookup"><span data-stu-id="1f701-117">Make sure that you are using the HTTPS scheme.</span></span> <span data-ttu-id="1f701-118">Klik vervolgens op **Maken**.</span><span class="sxs-lookup"><span data-stu-id="1f701-118">Then click **Create**.</span></span>
7. <span data-ttu-id="1f701-119">Maak een notitie van de waarden van de client-ID en clientgeheim op het volgende scherm.</span><span class="sxs-lookup"><span data-stu-id="1f701-119">On the next screen, make a note of the values of the client ID and client secret.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="1f701-120">Het clientgeheim is een belangrijke beveiligingsreferentie.</span><span class="sxs-lookup"><span data-stu-id="1f701-120">The client secret is an important security credential.</span></span> <span data-ttu-id="1f701-121">Dit geheim met anderen delen of deze te distribueren vanuit een clienttoepassing niet.</span><span class="sxs-lookup"><span data-stu-id="1f701-121">Do not share this secret with anyone or distribute it within a client application.</span></span>


## <span data-ttu-id="1f701-122"><a name="secrets"></a>Informatie Google toevoegen aan uw toepassing</span><span class="sxs-lookup"><span data-stu-id="1f701-122"><a name="secrets"> </a>Add Google information to your application</span></span>
1. <span data-ttu-id="1f701-123">Terug in de [Azure-portal], gaat u naar uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="1f701-123">Back in the [Azure portal], navigate to your application.</span></span> <span data-ttu-id="1f701-124">Klik op **instellingen**, en vervolgens **verificatie / autorisatie**.</span><span class="sxs-lookup"><span data-stu-id="1f701-124">Click **Settings**, and then **Authentication / Authorization**.</span></span>
2. <span data-ttu-id="1f701-125">Als de verificatie / autorisatie-functie niet is ingeschakeld, schakelt u de schakeloptie voor **op**.</span><span class="sxs-lookup"><span data-stu-id="1f701-125">If the Authentication / Authorization feature is not enabled, turn the switch to **On**.</span></span>
3. <span data-ttu-id="1f701-126">Klik op **Google**.</span><span class="sxs-lookup"><span data-stu-id="1f701-126">Click **Google**.</span></span> <span data-ttu-id="1f701-127">Plak in de App-ID en App-geheim waarden die u eerder hebt verkregen en optioneel in staat alle scopes die vereist zijn voor uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="1f701-127">Paste in the App ID and App Secret values which you obtained previously, and optionally enable any scopes your application requires.</span></span> <span data-ttu-id="1f701-128">Klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="1f701-128">Then click **OK**.</span></span>
   
   ![][1]
   
   <span data-ttu-id="1f701-129">Standaard-App Service biedt verificatie maar wordt niet geautoriseerde toegang beperkt tot uw site-inhoud en API's.</span><span class="sxs-lookup"><span data-stu-id="1f701-129">By default, App Service provides authentication but does not restrict authorized access to your site content and APIs.</span></span> <span data-ttu-id="1f701-130">U moet gebruikers machtigen in uw app-code.</span><span class="sxs-lookup"><span data-stu-id="1f701-130">You must authorize users in your app code.</span></span>
4. <span data-ttu-id="1f701-131">(Optioneel) Instellen om toegang te beperken tot uw site tot alleen gebruikers die zijn geverifieerd door Google, **te ondernemen actie wanneer de aanvraag is niet geverifieerd** naar **Google**.</span><span class="sxs-lookup"><span data-stu-id="1f701-131">(Optional) To restrict access to your site to only users authenticated by Google, set **Action to take when request is not authenticated** to **Google**.</span></span> <span data-ttu-id="1f701-132">Dit vereist dat alle aanvragen worden geverifieerd en alle niet-geverifieerde aanvragen worden omgeleid naar Google voor verificatie.</span><span class="sxs-lookup"><span data-stu-id="1f701-132">This requires that all requests be authenticated, and all unauthenticated requests are redirected to Google for authentication.</span></span>
5. <span data-ttu-id="1f701-133">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="1f701-133">Click **Save**.</span></span>

<span data-ttu-id="1f701-134">U bent nu klaar voor gebruik van Google voor verificatie in uw app.</span><span class="sxs-lookup"><span data-stu-id="1f701-134">You are now ready to use Google for authentication in your app.</span></span>

## <span data-ttu-id="1f701-135"><a name="related-content"></a>Verwante inhoud</span><span class="sxs-lookup"><span data-stu-id="1f701-135"><a name="related-content"> </a>Related Content</span></span>
[!INCLUDE [app-service-mobile-related-content-get-started-users](../../includes/app-service-mobile-related-content-get-started-users.md)]

<!-- Anchors. -->

<!-- Images. -->

[0]: ./media/app-service-mobile-how-to-configure-google-authentication/mobile-app-google-redirect.png
[1]: ./media/app-service-mobile-how-to-configure-google-authentication/mobile-app-google-settings.png

<!-- URLs. -->

[Google apis]: http://go.microsoft.com/fwlink/p/?LinkId=268303

[Azure-portal]: https://portal.azure.com/


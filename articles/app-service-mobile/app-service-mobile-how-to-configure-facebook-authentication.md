---
title: aaaHow tooconfigure Facebook-verificatie voor uw toepassing App Services
description: Meer informatie over hoe tooconfigure Facebook-verificatie voor uw App Services-toepassing.
services: app-service
documentationcenter: 
author: mattchenderson
manager: syntaxc4
editor: 
ms.assetid: b6b4f062-fcb4-47b3-b75a-ec4cb51a62fd
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 10/01/2016
ms.author: mahender
ms.openlocfilehash: 53d03445a2ad17de1d2f69f5e770d14385b48ad4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-your-app-service-application-toouse-facebook-login"></a><span data-ttu-id="bce9d-103">Hoe tooconfigure uw App Service-toepassing toouse Facebook-aanmelding</span><span class="sxs-lookup"><span data-stu-id="bce9d-103">How tooconfigure your App Service application toouse Facebook login</span></span>
[!INCLUDE [app-service-mobile-selector-authentication](../../includes/app-service-mobile-selector-authentication.md)]

<span data-ttu-id="bce9d-104">Dit onderwerp leest u hoe tooconfigure Azure App Service toouse Facebook als een verificatieprovider.</span><span class="sxs-lookup"><span data-stu-id="bce9d-104">This topic shows you how tooconfigure Azure App Service toouse Facebook as an authentication provider.</span></span>

<span data-ttu-id="bce9d-105">toocomplete Hallo-procedure in dit onderwerp, moet u een Facebook-account met een geverifieerde e-mailadres en een mobiel telefoonnummer hebben.</span><span class="sxs-lookup"><span data-stu-id="bce9d-105">toocomplete hello procedure in this topic, you must have a Facebook account that has a verified email address and a mobile phone number.</span></span> <span data-ttu-id="bce9d-106">toocreate een nieuwe Facebook-account, gaat u te[facebook.com].</span><span class="sxs-lookup"><span data-stu-id="bce9d-106">toocreate a new Facebook account, go too[facebook.com].</span></span>

## <span data-ttu-id="bce9d-107"><a name="register"></a>Uw toepassing registreren met Facebook</span><span class="sxs-lookup"><span data-stu-id="bce9d-107"><a name="register"> </a>Register your application with Facebook</span></span>
1. <span data-ttu-id="bce9d-108">Meld u aan toohello [Azure-portal], en ga tooyour toepassing.</span><span class="sxs-lookup"><span data-stu-id="bce9d-108">Log on toohello [Azure portal], and navigate tooyour application.</span></span> <span data-ttu-id="bce9d-109">Kopieer uw **URL**.</span><span class="sxs-lookup"><span data-stu-id="bce9d-109">Copy your **URL**.</span></span> <span data-ttu-id="bce9d-110">U gebruikt deze tooconfigure uw Facebook-app.</span><span class="sxs-lookup"><span data-stu-id="bce9d-110">You will use this tooconfigure your Facebook app.</span></span>
2. <span data-ttu-id="bce9d-111">Navigeer in een ander browservenster toohello [Facebook-ontwikkelaars] website en aanmelden met uw Facebook-accountreferenties.</span><span class="sxs-lookup"><span data-stu-id="bce9d-111">In another browser window, navigate toohello [Facebook Developers] website and sign-in with your Facebook account credentials.</span></span>
3. <span data-ttu-id="bce9d-112">(Optioneel) Als u nog niet hebt geregistreerd, klikt u op **Apps** > **registreren als een ontwikkelaar**, accepteert u Hallo beleid en registratie van Hallo stappen.</span><span class="sxs-lookup"><span data-stu-id="bce9d-112">(Optional) If you have not already registered, click **Apps** > **Register as a Developer**, then accept hello policy and follow hello registration steps.</span></span>
4. <span data-ttu-id="bce9d-113">Klik op **mijn Apps** > **toevoegen van een nieuwe App** > **Website** > **overslaan en App-ID maken**.</span><span class="sxs-lookup"><span data-stu-id="bce9d-113">Click **My Apps** > **Add a New App** > **Website** > **Skip and Create App ID**.</span></span> 
5. <span data-ttu-id="bce9d-114">In **weergavenaam**, typ een unieke naam voor uw app, type uw **Neem contact op met E-mail**, kies een **categorie** voor uw app, klik vervolgens op **App-ID maken**en Hallo beveiligingscontrole te voltooien.</span><span class="sxs-lookup"><span data-stu-id="bce9d-114">In **Display Name**, type a unique name for your app, type your **Contact Email**, choose a **Category** for your app, then click **Create App ID** and complete hello security check.</span></span> <span data-ttu-id="bce9d-115">Hiermee gaat u toohello dashboard voor ontwikkelaars voor uw nieuwe Facebook-app.</span><span class="sxs-lookup"><span data-stu-id="bce9d-115">This takes you toohello developer dashboard for your new Facebook app.</span></span>
6. <span data-ttu-id="bce9d-116">Klik onder 'Facebook aanmelding,' op **aan de slag**.</span><span class="sxs-lookup"><span data-stu-id="bce9d-116">Under "Facebook Login," click **Get Started**.</span></span> <span data-ttu-id="bce9d-117">Toevoegen van uw toepassing **omleidings-URI** te**geldig OAuth omleidings-URI's**, klikt u vervolgens op **wijzigingen opslaan**.</span><span class="sxs-lookup"><span data-stu-id="bce9d-117">Add your application's **Redirect URI** too**Valid OAuth redirect URIs**, then click **Save Changes**.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="bce9d-118">De omleidings-URI Hallo-URL van uw toepassing toegevoegd aan de Hallo pad is, */.auth/login/facebook/callback*.</span><span class="sxs-lookup"><span data-stu-id="bce9d-118">Your redirect URI is hello URL of your application appended with hello path, */.auth/login/facebook/callback*.</span></span> <span data-ttu-id="bce9d-119">Bijvoorbeeld `https://contoso.azurewebsites.net/.auth/login/facebook/callback`.</span><span class="sxs-lookup"><span data-stu-id="bce9d-119">For example, `https://contoso.azurewebsites.net/.auth/login/facebook/callback`.</span></span> <span data-ttu-id="bce9d-120">Zorg ervoor dat u van Hallo HTTPS-schema gebruikmaakt.</span><span class="sxs-lookup"><span data-stu-id="bce9d-120">Make sure that you are using hello HTTPS scheme.</span></span>
   > 
   > 
7. <span data-ttu-id="bce9d-121">Klik in de linkernavigatiebalk hello, **instellingen**.</span><span class="sxs-lookup"><span data-stu-id="bce9d-121">In hello left-hand navigation, click **Settings**.</span></span> <span data-ttu-id="bce9d-122">Op Hallo **App geheim** veld, klikt u op **weergeven**, geeft u uw wachtwoord als aangevraagd, maak een notitie van waarden van Hallo **App-ID** en **App geheim**.</span><span class="sxs-lookup"><span data-stu-id="bce9d-122">On hello **App Secret** field, click **Show**, provide your password if requested, then make a note of hello values of **App ID** and **App Secret**.</span></span> <span data-ttu-id="bce9d-123">U gebruikt deze later tooconfigure uw toepassing in Azure.</span><span class="sxs-lookup"><span data-stu-id="bce9d-123">You use these later tooconfigure your application in Azure.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="bce9d-124">Hallo app geheime sleutel is een belangrijke beveiligingsreferentie.</span><span class="sxs-lookup"><span data-stu-id="bce9d-124">hello app secret is an important security credential.</span></span> <span data-ttu-id="bce9d-125">Dit geheim met anderen delen of deze te distribueren vanuit een clienttoepassing niet.</span><span class="sxs-lookup"><span data-stu-id="bce9d-125">Do not share this secret with anyone or distribute it within a client application.</span></span>
   > 
   > 
8. <span data-ttu-id="bce9d-126">Hallo Facebook-account dat gebruikt tooregister Hallo toepassing is is een beheerder van Hallo-app.</span><span class="sxs-lookup"><span data-stu-id="bce9d-126">hello Facebook account which was used tooregister hello application is an administrator of hello app.</span></span> <span data-ttu-id="bce9d-127">Alleen beheerders kunnen op dit moment aanmelden bij deze toepassing.</span><span class="sxs-lookup"><span data-stu-id="bce9d-127">At this point, only administrators can sign into this application.</span></span> <span data-ttu-id="bce9d-128">tooauthenticate andere accounts Facebook, klikt u op **App revisie** en schakel **maken < uw app-naam > openbare** tooenable algemene openbare toegang met Facebook-verificatie.</span><span class="sxs-lookup"><span data-stu-id="bce9d-128">tooauthenticate other Facebook accounts, click **App Review** and enable **Make <your-app-name> public** tooenable general public access using Facebook authentication.</span></span>

## <span data-ttu-id="bce9d-129"><a name="secrets"></a>Toevoegen Facebook informatie tooyour-toepassing</span><span class="sxs-lookup"><span data-stu-id="bce9d-129"><a name="secrets"> </a>Add Facebook information tooyour application</span></span>
1. <span data-ttu-id="bce9d-130">Terug in Hallo [Azure-portal], tooyour toepassing navigeren.</span><span class="sxs-lookup"><span data-stu-id="bce9d-130">Back in hello [Azure portal], navigate tooyour application.</span></span> <span data-ttu-id="bce9d-131">Klik op **instellingen** > **verificatie / autorisatie**, en zorg ervoor dat **verificatie van App Service** is **op**.</span><span class="sxs-lookup"><span data-stu-id="bce9d-131">Click **Settings** > **Authentication / Authorization**, and make sure that **App Service Authentication** is **On**.</span></span>
2. <span data-ttu-id="bce9d-132">Klik op **Facebook**, plak in Hallo App-ID en App-geheim waarden die u eerder hebt verkregen, eventueel alle scopes die nodig is voor uw toepassing inschakelen en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="bce9d-132">Click **Facebook**, paste in hello App ID and App Secret values which you obtained previously, optionally enable any scopes needed by your application, then click **OK**.</span></span>
   
    ![][0]
   
    <span data-ttu-id="bce9d-133">Standaard-App Service biedt verificatie maar niet beperkt geautoriseerde toegang tooyour site-inhoud en API's.</span><span class="sxs-lookup"><span data-stu-id="bce9d-133">By default, App Service provides authentication but does not restrict authorized access tooyour site content and APIs.</span></span> <span data-ttu-id="bce9d-134">U moet gebruikers machtigen in uw app-code.</span><span class="sxs-lookup"><span data-stu-id="bce9d-134">You must authorize users in your app code.</span></span>
3. <span data-ttu-id="bce9d-135">(Optioneel) toorestrict toegang tooyour site tooonly gebruikers zijn geverifieerd door Facebook, ingesteld **tootake actie wanneer de aanvraag is niet geverifieerd** te**Facebook**.</span><span class="sxs-lookup"><span data-stu-id="bce9d-135">(Optional) toorestrict access tooyour site tooonly users authenticated by Facebook, set **Action tootake when request is not authenticated** too**Facebook**.</span></span> <span data-ttu-id="bce9d-136">Dit vereist dat alle aanvragen worden geverifieerd en alle niet-geverifieerde aanvragen worden omgeleid tooFacebook voor verificatie.</span><span class="sxs-lookup"><span data-stu-id="bce9d-136">This requires that all requests be authenticated, and all unauthenticated requests are redirected tooFacebook for authentication.</span></span>
4. <span data-ttu-id="bce9d-137">Wanneer u klaar verificatie configureren, klikt u op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="bce9d-137">When done configuring authentication, click **Save**.</span></span>

<span data-ttu-id="bce9d-138">U bent nu klaar toouse Facebook voor verificatie in uw app.</span><span class="sxs-lookup"><span data-stu-id="bce9d-138">You are now ready toouse Facebook for authentication in your app.</span></span>

## <span data-ttu-id="bce9d-139"><a name="related-content"></a>Verwante inhoud</span><span class="sxs-lookup"><span data-stu-id="bce9d-139"><a name="related-content"> </a>Related Content</span></span>
[!INCLUDE [app-service-mobile-related-content-get-started-users](../../includes/app-service-mobile-related-content-get-started-users.md)]

<!-- Images. -->
[0]: ./media/app-service-mobile-how-to-configure-facebook-authentication/mobile-app-facebook-settings.png

<!-- URLs. -->
[Facebook-ontwikkelaars]: http://go.microsoft.com/fwlink/p/?LinkId=268286
[facebook.com]: http://go.microsoft.com/fwlink/p/?LinkId=268285
[Get started with authentication]: /en-us/develop/mobile/tutorials/get-started-with-users-dotnet/
[Azure-portal]: https://portal.azure.com/

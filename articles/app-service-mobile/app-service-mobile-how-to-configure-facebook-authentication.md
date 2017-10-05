---
title: Facebook-verificatie voor uw toepassing App Services configureren
description: Informatie over het Facebook-verificatie voor uw toepassing App Services configureren.
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
ms.openlocfilehash: c1b4c91d384c56c4f55bf8d31ced250f51c0d837
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-configure-your-app-service-application-to-use-facebook-login"></a><span data-ttu-id="4d20e-103">Uw App Service-toepassing configureren voor het gebruik van Facebook-aanmelding</span><span class="sxs-lookup"><span data-stu-id="4d20e-103">How to configure your App Service application to use Facebook login</span></span>
[!INCLUDE [app-service-mobile-selector-authentication](../../includes/app-service-mobile-selector-authentication.md)]

<span data-ttu-id="4d20e-104">Dit onderwerp leest u over het configureren van Azure App Service voor het gebruik van Facebook als een verificatieprovider.</span><span class="sxs-lookup"><span data-stu-id="4d20e-104">This topic shows you how to configure Azure App Service to use Facebook as an authentication provider.</span></span>

<span data-ttu-id="4d20e-105">U moet een Facebook-account met een geverifieerde e-mailadres en een mobiel telefoonnummer hebben voor de procedure in dit onderwerp.</span><span class="sxs-lookup"><span data-stu-id="4d20e-105">To complete the procedure in this topic, you must have a Facebook account that has a verified email address and a mobile phone number.</span></span> <span data-ttu-id="4d20e-106">Om een nieuwe Facebook-account maken, gaat u naar [facebook.com].</span><span class="sxs-lookup"><span data-stu-id="4d20e-106">To create a new Facebook account, go to [facebook.com].</span></span>

## <span data-ttu-id="4d20e-107"><a name="register"></a>Uw toepassing registreren met Facebook</span><span class="sxs-lookup"><span data-stu-id="4d20e-107"><a name="register"> </a>Register your application with Facebook</span></span>
1. <span data-ttu-id="4d20e-108">Meld u aan bij de [Azure-portal], en navigeer naar uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="4d20e-108">Log on to the [Azure portal], and navigate to your application.</span></span> <span data-ttu-id="4d20e-109">Kopieer uw **URL**.</span><span class="sxs-lookup"><span data-stu-id="4d20e-109">Copy your **URL**.</span></span> <span data-ttu-id="4d20e-110">U gebruikt dit voor het configureren van uw Facebook-app.</span><span class="sxs-lookup"><span data-stu-id="4d20e-110">You will use this to configure your Facebook app.</span></span>
2. <span data-ttu-id="4d20e-111">In een ander browservenster en navigeer naar de [Facebook-ontwikkelaars] website en aanmelden met uw Facebook-accountreferenties.</span><span class="sxs-lookup"><span data-stu-id="4d20e-111">In another browser window, navigate to the [Facebook Developers] website and sign-in with your Facebook account credentials.</span></span>
3. <span data-ttu-id="4d20e-112">(Optioneel) Als u nog niet hebt geregistreerd, klikt u op **Apps** > **registreren als een ontwikkelaar**, accepteert u het beleid en volg de stappen voor inschrijving.</span><span class="sxs-lookup"><span data-stu-id="4d20e-112">(Optional) If you have not already registered, click **Apps** > **Register as a Developer**, then accept the policy and follow the registration steps.</span></span>
4. <span data-ttu-id="4d20e-113">Klik op **mijn Apps** > **toevoegen van een nieuwe App** > **Website** > **overslaan en App-ID maken**.</span><span class="sxs-lookup"><span data-stu-id="4d20e-113">Click **My Apps** > **Add a New App** > **Website** > **Skip and Create App ID**.</span></span> 
5. <span data-ttu-id="4d20e-114">In **weergavenaam**, typ een unieke naam voor uw app, type uw **Neem contact op met E-mail**, kies een **categorie** voor uw app, klik vervolgens op **App-ID maken**en voltooi de beveiligingscontrole.</span><span class="sxs-lookup"><span data-stu-id="4d20e-114">In **Display Name**, type a unique name for your app, type your **Contact Email**, choose a **Category** for your app, then click **Create App ID** and complete the security check.</span></span> <span data-ttu-id="4d20e-115">Hiermee gaat u naar het dashboard voor ontwikkelaars voor uw nieuwe Facebook-app.</span><span class="sxs-lookup"><span data-stu-id="4d20e-115">This takes you to the developer dashboard for your new Facebook app.</span></span>
6. <span data-ttu-id="4d20e-116">Klik onder 'Facebook aanmelding,' op **aan de slag**.</span><span class="sxs-lookup"><span data-stu-id="4d20e-116">Under "Facebook Login," click **Get Started**.</span></span> <span data-ttu-id="4d20e-117">Toevoegen van uw toepassing **omleidings-URI** naar **geldig OAuth omleidings-URI's**, klikt u vervolgens op **wijzigingen opslaan**.</span><span class="sxs-lookup"><span data-stu-id="4d20e-117">Add your application's **Redirect URI** to **Valid OAuth redirect URIs**, then click **Save Changes**.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="4d20e-118">De omleidings-URI de URL van uw toepassing toegevoegd aan het pad is */.auth/login/facebook/callback*.</span><span class="sxs-lookup"><span data-stu-id="4d20e-118">Your redirect URI is the URL of your application appended with the path, */.auth/login/facebook/callback*.</span></span> <span data-ttu-id="4d20e-119">Bijvoorbeeld `https://contoso.azurewebsites.net/.auth/login/facebook/callback`.</span><span class="sxs-lookup"><span data-stu-id="4d20e-119">For example, `https://contoso.azurewebsites.net/.auth/login/facebook/callback`.</span></span> <span data-ttu-id="4d20e-120">Zorg ervoor dat u van het HTTPS-schema gebruikmaakt.</span><span class="sxs-lookup"><span data-stu-id="4d20e-120">Make sure that you are using the HTTPS scheme.</span></span>
   > 
   > 
7. <span data-ttu-id="4d20e-121">Klik in de linkernavigatiebalk **instellingen**.</span><span class="sxs-lookup"><span data-stu-id="4d20e-121">In the left-hand navigation, click **Settings**.</span></span> <span data-ttu-id="4d20e-122">Op de **App geheim** veld, klikt u op **weergeven**, geeft u uw wachtwoord als aangevraagd, noteert u de waarden van **App-ID** en **App geheim** .</span><span class="sxs-lookup"><span data-stu-id="4d20e-122">On the **App Secret** field, click **Show**, provide your password if requested, then make a note of the values of **App ID** and **App Secret**.</span></span> <span data-ttu-id="4d20e-123">Met deze later kunt u uw toepassing configureren in Azure.</span><span class="sxs-lookup"><span data-stu-id="4d20e-123">You use these later to configure your application in Azure.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="4d20e-124">Het app-geheim is een belangrijke beveiligingsreferentie.</span><span class="sxs-lookup"><span data-stu-id="4d20e-124">The app secret is an important security credential.</span></span> <span data-ttu-id="4d20e-125">Dit geheim met anderen delen of deze te distribueren vanuit een clienttoepassing niet.</span><span class="sxs-lookup"><span data-stu-id="4d20e-125">Do not share this secret with anyone or distribute it within a client application.</span></span>
   > 
   > 
8. <span data-ttu-id="4d20e-126">De Facebook-account dat is gebruikt voor het registreren van de toepassing is een beheerder van de app.</span><span class="sxs-lookup"><span data-stu-id="4d20e-126">The Facebook account which was used to register the application is an administrator of the app.</span></span> <span data-ttu-id="4d20e-127">Alleen beheerders kunnen op dit moment aanmelden bij deze toepassing.</span><span class="sxs-lookup"><span data-stu-id="4d20e-127">At this point, only administrators can sign into this application.</span></span> <span data-ttu-id="4d20e-128">Om te verifiëren andere accounts Facebook, klikt u op **App revisie** en schakel **maken < uw app-naam > openbare** algemene openbare toegang met Facebook-verificatie inschakelen.</span><span class="sxs-lookup"><span data-stu-id="4d20e-128">To authenticate other Facebook accounts, click **App Review** and enable **Make <your-app-name> public** to enable general public access using Facebook authentication.</span></span>

## <span data-ttu-id="4d20e-129"><a name="secrets"></a>Toevoegen Facebook-informatie voor uw toepassing</span><span class="sxs-lookup"><span data-stu-id="4d20e-129"><a name="secrets"> </a>Add Facebook information to your application</span></span>
1. <span data-ttu-id="4d20e-130">Terug in de [Azure-portal], gaat u naar uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="4d20e-130">Back in the [Azure portal], navigate to your application.</span></span> <span data-ttu-id="4d20e-131">Klik op **instellingen** > **verificatie / autorisatie**, en zorg ervoor dat **verificatie van App Service** is **op**.</span><span class="sxs-lookup"><span data-stu-id="4d20e-131">Click **Settings** > **Authentication / Authorization**, and make sure that **App Service Authentication** is **On**.</span></span>
2. <span data-ttu-id="4d20e-132">Klik op **Facebook**, plakken in de App-ID en App-geheim waarden die u eerder hebt verkregen, eventueel alle scopes die nodig is voor uw toepassing inschakelen en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="4d20e-132">Click **Facebook**, paste in the App ID and App Secret values which you obtained previously, optionally enable any scopes needed by your application, then click **OK**.</span></span>
   
    ![][0]
   
    <span data-ttu-id="4d20e-133">Standaard-App Service biedt verificatie maar wordt niet geautoriseerde toegang beperkt tot uw site-inhoud en API's.</span><span class="sxs-lookup"><span data-stu-id="4d20e-133">By default, App Service provides authentication but does not restrict authorized access to your site content and APIs.</span></span> <span data-ttu-id="4d20e-134">U moet gebruikers machtigen in uw app-code.</span><span class="sxs-lookup"><span data-stu-id="4d20e-134">You must authorize users in your app code.</span></span>
3. <span data-ttu-id="4d20e-135">(Optioneel) Instellen om toegang te beperken tot uw site tot alleen gebruikers die zijn geverifieerd door Facebook, **te ondernemen actie wanneer de aanvraag is niet geverifieerd** naar **Facebook**.</span><span class="sxs-lookup"><span data-stu-id="4d20e-135">(Optional) To restrict access to your site to only users authenticated by Facebook, set **Action to take when request is not authenticated** to **Facebook**.</span></span> <span data-ttu-id="4d20e-136">Dit vereist dat alle aanvragen worden geverifieerd en alle niet-geverifieerde aanvragen worden omgeleid naar Facebook voor verificatie.</span><span class="sxs-lookup"><span data-stu-id="4d20e-136">This requires that all requests be authenticated, and all unauthenticated requests are redirected to Facebook for authentication.</span></span>
4. <span data-ttu-id="4d20e-137">Wanneer u klaar verificatie configureren, klikt u op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="4d20e-137">When done configuring authentication, click **Save**.</span></span>

<span data-ttu-id="4d20e-138">U bent nu klaar voor gebruik van Facebook voor verificatie in uw app.</span><span class="sxs-lookup"><span data-stu-id="4d20e-138">You are now ready to use Facebook for authentication in your app.</span></span>

## <span data-ttu-id="4d20e-139"><a name="related-content"></a>Verwante inhoud</span><span class="sxs-lookup"><span data-stu-id="4d20e-139"><a name="related-content"> </a>Related Content</span></span>
[!INCLUDE [app-service-mobile-related-content-get-started-users](../../includes/app-service-mobile-related-content-get-started-users.md)]

<!-- Images. -->
[0]: ./media/app-service-mobile-how-to-configure-facebook-authentication/mobile-app-facebook-settings.png

<!-- URLs. -->
<span data-ttu-id="4d20e-140">[Facebook-ontwikkelaars]: http://go.microsoft.com/fwlink/p/?LinkId=268286</span><span class="sxs-lookup"><span data-stu-id="4d20e-140">[Facebook Developers]: http://go.microsoft.com/fwlink/p/?LinkId=268286</span></span>
<span data-ttu-id="4d20e-141">[facebook.com]: http://go.microsoft.com/fwlink/p/?LinkId=268285</span><span class="sxs-lookup"><span data-stu-id="4d20e-141">[facebook.com]: http://go.microsoft.com/fwlink/p/?LinkId=268285</span></span>
[Get started with authentication]: /en-us/develop/mobile/tutorials/get-started-with-users-dotnet/
<span data-ttu-id="4d20e-142">[Azure-portal]: https://portal.azure.com/</span><span class="sxs-lookup"><span data-stu-id="4d20e-142">[Azure portal]: https://portal.azure.com/</span></span>

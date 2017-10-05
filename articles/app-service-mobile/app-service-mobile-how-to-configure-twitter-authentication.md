---
title: Twitter-verificatie voor uw toepassing App Services configureren
description: Informatie over het Twitter-verificatie voor uw toepassing App Services configureren.
services: app-service
documentationcenter: 
author: mattchenderson
manager: syntaxc4
editor: 
ms.assetid: c6dc91d7-30f6-448c-9f2d-8e91104cde73
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 10/01/2016
ms.author: mahender
ms.openlocfilehash: afde020b7817dc58ecea24eb4a09cf93d0986eb2
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-configure-your-app-service-application-to-use-twitter-login"></a><span data-ttu-id="b0f9c-103">Het configureren van uw App Service-toepassing Twitter aanmelding gebruiken</span><span class="sxs-lookup"><span data-stu-id="b0f9c-103">How to configure your App Service application to use Twitter login</span></span>
[!INCLUDE [app-service-mobile-selector-authentication](../../includes/app-service-mobile-selector-authentication.md)]

<span data-ttu-id="b0f9c-104">Dit onderwerp leest u over het configureren van Azure App Service voor het gebruik van Twitter als een verificatieprovider.</span><span class="sxs-lookup"><span data-stu-id="b0f9c-104">This topic shows you how to configure Azure App Service to use Twitter as an authentication provider.</span></span>

<span data-ttu-id="b0f9c-105">U moet een Twitter-account met een geverifieerde e-mailadres en telefoonnummer getal hebben voor de procedure in dit onderwerp.</span><span class="sxs-lookup"><span data-stu-id="b0f9c-105">To complete the procedure in this topic, you must have a Twitter account that has a verified email address and phone number.</span></span> <span data-ttu-id="b0f9c-106">Voor het maken van een nieuw Twitter-account, gaat u naar <a href="http://go.microsoft.com/fwlink/p/?LinkID=268287" target="_blank">twitter.com</a>.</span><span class="sxs-lookup"><span data-stu-id="b0f9c-106">To create a new Twitter account, go to <a href="http://go.microsoft.com/fwlink/p/?LinkID=268287" target="_blank">twitter.com</a>.</span></span>

## <span data-ttu-id="b0f9c-107"><a name="register"></a>Uw toepassing registreren met Twitter</span><span class="sxs-lookup"><span data-stu-id="b0f9c-107"><a name="register"> </a>Register your application with Twitter</span></span>
1. <span data-ttu-id="b0f9c-108">Meld u aan bij de [Azure-portal], en navigeer naar uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="b0f9c-108">Log on to the [Azure portal], and navigate to your application.</span></span> <span data-ttu-id="b0f9c-109">Kopieer uw **URL**.</span><span class="sxs-lookup"><span data-stu-id="b0f9c-109">Copy your **URL**.</span></span> <span data-ttu-id="b0f9c-110">U gebruikt dit voor het configureren van uw app Twitter.</span><span class="sxs-lookup"><span data-stu-id="b0f9c-110">You will use this to configure your Twitter app.</span></span>
2. <span data-ttu-id="b0f9c-111">Navigeer naar de [Twitter ontwikkelaars] website, meld u aan met de referenties van uw Twitter-account en klikt u op **nieuwe App maken**.</span><span class="sxs-lookup"><span data-stu-id="b0f9c-111">Navigate to the [Twitter Developers] website, sign in with your Twitter account credentials, and click **Create New App**.</span></span>
3. <span data-ttu-id="b0f9c-112">Typ in het **naam** en een **beschrijving** voor uw nieuwe app.</span><span class="sxs-lookup"><span data-stu-id="b0f9c-112">Type in the **Name** and a **Description** for your new app.</span></span> <span data-ttu-id="b0f9c-113">Plakken in uw toepassing **URL** voor de **Website** waarde.</span><span class="sxs-lookup"><span data-stu-id="b0f9c-113">Paste in your application's **URL** for the **Website** value.</span></span> <span data-ttu-id="b0f9c-114">Vervolgens voor de **retouraanroep URL**, plak de **retouraanroep URL** u eerder hebt gekopieerd.</span><span class="sxs-lookup"><span data-stu-id="b0f9c-114">Then, for the **Callback URL**, paste the **Callback URL** you copied earlier.</span></span> <span data-ttu-id="b0f9c-115">Dit is de gateway van uw mobiele App toegevoegd aan het pad */.auth/login/twitter/callback*.</span><span class="sxs-lookup"><span data-stu-id="b0f9c-115">This is your Mobile App gateway appended with the path, */.auth/login/twitter/callback*.</span></span> <span data-ttu-id="b0f9c-116">Bijvoorbeeld `https://contoso.azurewebsites.net/.auth/login/twitter/callback`.</span><span class="sxs-lookup"><span data-stu-id="b0f9c-116">For example, `https://contoso.azurewebsites.net/.auth/login/twitter/callback`.</span></span> <span data-ttu-id="b0f9c-117">Zorg ervoor dat u van het HTTPS-schema gebruikmaakt.</span><span class="sxs-lookup"><span data-stu-id="b0f9c-117">Make sure that you are using the HTTPS scheme.</span></span>
4. <span data-ttu-id="b0f9c-118">Lees en accepteer de voorwaarden aan de onderkant van de pagina.</span><span class="sxs-lookup"><span data-stu-id="b0f9c-118">At the bottom the page, read and accept the terms.</span></span> <span data-ttu-id="b0f9c-119">Klik vervolgens op **uw Twitter-toepassing maken**.</span><span class="sxs-lookup"><span data-stu-id="b0f9c-119">Then click **Create your Twitter application**.</span></span> <span data-ttu-id="b0f9c-120">Hiermee wordt de app wordt weergegeven de toepassingsgegevens.</span><span class="sxs-lookup"><span data-stu-id="b0f9c-120">This registers the app displays the application details.</span></span>
5. <span data-ttu-id="b0f9c-121">Klik op de **instellingen** tabblad selectievakje **toe dat deze toepassing worden gebruikt voor het aanmelden met Twitter**, klikt u vervolgens op **Update-instellingen**.</span><span class="sxs-lookup"><span data-stu-id="b0f9c-121">Click the **Settings** tab, check **Allow this application to be used to sign in with Twitter**, then click **Update Settings**.</span></span>
6. <span data-ttu-id="b0f9c-122">Selecteer de **sleutels en toegangstokens** tabblad.</span><span class="sxs-lookup"><span data-stu-id="b0f9c-122">Select the **Keys and Access Tokens** tab.</span></span> <span data-ttu-id="b0f9c-123">Noteer de waarden van **Consumer-sleutel (API-sleutel)** en **consumentgeheim (API geheim)**.</span><span class="sxs-lookup"><span data-stu-id="b0f9c-123">Make a note of the values of **Consumer Key (API Key)** and **Consumer secret (API Secret)**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="b0f9c-124">De consument geheime sleutel is een belangrijke beveiligingsreferentie.</span><span class="sxs-lookup"><span data-stu-id="b0f9c-124">The consumer secret is an important security credential.</span></span> <span data-ttu-id="b0f9c-125">Geen dit geheim met anderen delen of deze met uw app te distribueren.</span><span class="sxs-lookup"><span data-stu-id="b0f9c-125">Do not share this secret with anyone or distribute it with your app.</span></span>
   > 
   > 

## <span data-ttu-id="b0f9c-126"><a name="secrets"></a>Informatie Twitter toevoegen aan uw toepassing</span><span class="sxs-lookup"><span data-stu-id="b0f9c-126"><a name="secrets"> </a>Add Twitter information to your application</span></span>
1. <span data-ttu-id="b0f9c-127">Terug in de [Azure-portal], gaat u naar uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="b0f9c-127">Back in the [Azure portal], navigate to your application.</span></span> <span data-ttu-id="b0f9c-128">Klik op **instellingen**, en vervolgens **verificatie / autorisatie**.</span><span class="sxs-lookup"><span data-stu-id="b0f9c-128">Click **Settings**, and then **Authentication / Authorization**.</span></span>
2. <span data-ttu-id="b0f9c-129">Als de verificatie / autorisatie-functie niet is ingeschakeld, schakelt u de schakeloptie voor **op**.</span><span class="sxs-lookup"><span data-stu-id="b0f9c-129">If the Authentication / Authorization feature is not enabled, turn the switch to **On**.</span></span>
3. <span data-ttu-id="b0f9c-130">Klik op **Twitter**.</span><span class="sxs-lookup"><span data-stu-id="b0f9c-130">Click **Twitter**.</span></span> <span data-ttu-id="b0f9c-131">Plak in het App-ID en het App-geheim waarden die u eerder hebt verkregen.</span><span class="sxs-lookup"><span data-stu-id="b0f9c-131">Paste in the App ID and App Secret values which you obtained previously.</span></span> <span data-ttu-id="b0f9c-132">Klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="b0f9c-132">Then click **OK**.</span></span>
   
   ![][1]
   
   <span data-ttu-id="b0f9c-133">Standaard-App Service biedt verificatie maar wordt niet geautoriseerde toegang beperkt tot uw site-inhoud en API's.</span><span class="sxs-lookup"><span data-stu-id="b0f9c-133">By default, App Service provides authentication but does not restrict authorized access to your site content and APIs.</span></span> <span data-ttu-id="b0f9c-134">U moet gebruikers machtigen in uw app-code.</span><span class="sxs-lookup"><span data-stu-id="b0f9c-134">You must authorize users in your app code.</span></span>
4. <span data-ttu-id="b0f9c-135">(Optioneel) Instellen om toegang te beperken tot uw site tot alleen gebruikers die zijn geverifieerd door Twitter, **te ondernemen actie wanneer de aanvraag is niet geverifieerd** naar **Twitter**.</span><span class="sxs-lookup"><span data-stu-id="b0f9c-135">(Optional) To restrict access to your site to only users authenticated by Twitter, set **Action to take when request is not authenticated** to **Twitter**.</span></span> <span data-ttu-id="b0f9c-136">Dit vereist dat alle aanvragen worden geverifieerd en alle niet-geverifieerde aanvragen worden omgeleid naar Twitter voor verificatie.</span><span class="sxs-lookup"><span data-stu-id="b0f9c-136">This requires that all requests be authenticated, and all unauthenticated requests are redirected to Twitter for authentication.</span></span>
5. <span data-ttu-id="b0f9c-137">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="b0f9c-137">Click **Save**.</span></span>

<span data-ttu-id="b0f9c-138">U bent nu klaar voor gebruik van Twitter voor verificatie in uw app.</span><span class="sxs-lookup"><span data-stu-id="b0f9c-138">You are now ready to use Twitter for authentication in your app.</span></span>

## <span data-ttu-id="b0f9c-139"><a name="related-content"></a>Verwante inhoud</span><span class="sxs-lookup"><span data-stu-id="b0f9c-139"><a name="related-content"> </a>Related Content</span></span>
[!INCLUDE [app-service-mobile-related-content-get-started-users](../../includes/app-service-mobile-related-content-get-started-users.md)]

<!-- Images. -->

[0]: ./media/app-service-mobile-how-to-configure-twitter-authentication/app-service-twitter-redirect.png
[1]: ./media/app-service-mobile-how-to-configure-twitter-authentication/mobile-app-twitter-settings.png

<!-- URLs. -->

<span data-ttu-id="b0f9c-140">[Twitter ontwikkelaars]: http://go.microsoft.com/fwlink/p/?LinkId=268300</span><span class="sxs-lookup"><span data-stu-id="b0f9c-140">[Twitter Developers]: http://go.microsoft.com/fwlink/p/?LinkId=268300</span></span>
<span data-ttu-id="b0f9c-141">[Azure-portal]: https://portal.azure.com/</span><span class="sxs-lookup"><span data-stu-id="b0f9c-141">[Azure portal]: https://portal.azure.com/</span></span>
[xamarin]: ../app-services-mobile-app-xamarin-ios-get-started-users.md

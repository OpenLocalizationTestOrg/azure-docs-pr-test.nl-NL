---
title: aaaHow tooconfigure Twitter-verificatie voor uw toepassing App Services
description: Meer informatie over hoe tooconfigure Twitter-verificatie voor uw App Services-toepassing.
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
ms.openlocfilehash: 0d16ac44d7b54e3567b793a904059d31ab1d8911
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-your-app-service-application-toouse-twitter-login"></a><span data-ttu-id="4e042-103">Hoe tooconfigure uw App Service-toepassing toouse Twitter-aanmelding</span><span class="sxs-lookup"><span data-stu-id="4e042-103">How tooconfigure your App Service application toouse Twitter login</span></span>
[!INCLUDE [app-service-mobile-selector-authentication](../../includes/app-service-mobile-selector-authentication.md)]

<span data-ttu-id="4e042-104">Dit onderwerp leest u hoe tooconfigure Azure App Service toouse Twitter als een verificatieprovider.</span><span class="sxs-lookup"><span data-stu-id="4e042-104">This topic shows you how tooconfigure Azure App Service toouse Twitter as an authentication provider.</span></span>

<span data-ttu-id="4e042-105">toocomplete Hallo-procedure in dit onderwerp, moet u een Twitter-account met een geverifieerde e-mailadres en telefoonnummer nummer hebben.</span><span class="sxs-lookup"><span data-stu-id="4e042-105">toocomplete hello procedure in this topic, you must have a Twitter account that has a verified email address and phone number.</span></span> <span data-ttu-id="4e042-106">toocreate een nieuw Twitter-account, gaat u te<a href="http://go.microsoft.com/fwlink/p/?LinkID=268287" target="_blank">twitter.com</a>.</span><span class="sxs-lookup"><span data-stu-id="4e042-106">toocreate a new Twitter account, go too<a href="http://go.microsoft.com/fwlink/p/?LinkID=268287" target="_blank">twitter.com</a>.</span></span>

## <span data-ttu-id="4e042-107"><a name="register"></a>Uw toepassing registreren met Twitter</span><span class="sxs-lookup"><span data-stu-id="4e042-107"><a name="register"> </a>Register your application with Twitter</span></span>
1. <span data-ttu-id="4e042-108">Meld u aan toohello [Azure-portal], en ga tooyour toepassing.</span><span class="sxs-lookup"><span data-stu-id="4e042-108">Log on toohello [Azure portal], and navigate tooyour application.</span></span> <span data-ttu-id="4e042-109">Kopieer uw **URL**.</span><span class="sxs-lookup"><span data-stu-id="4e042-109">Copy your **URL**.</span></span> <span data-ttu-id="4e042-110">U gebruikt deze tooconfigure uw Twitter-app.</span><span class="sxs-lookup"><span data-stu-id="4e042-110">You will use this tooconfigure your Twitter app.</span></span>
2. <span data-ttu-id="4e042-111">Navigeer toohello [Twitter ontwikkelaars] website, meld u aan met de referenties van uw Twitter-account en klikt u op **nieuwe App maken**.</span><span class="sxs-lookup"><span data-stu-id="4e042-111">Navigate toohello [Twitter Developers] website, sign in with your Twitter account credentials, and click **Create New App**.</span></span>
3. <span data-ttu-id="4e042-112">Type in Hallo **naam** en een **beschrijving** voor uw nieuwe app.</span><span class="sxs-lookup"><span data-stu-id="4e042-112">Type in hello **Name** and a **Description** for your new app.</span></span> <span data-ttu-id="4e042-113">Plakken in uw toepassing **URL** voor Hallo **Website** waarde.</span><span class="sxs-lookup"><span data-stu-id="4e042-113">Paste in your application's **URL** for hello **Website** value.</span></span> <span data-ttu-id="4e042-114">Klik vervolgens voor Hallo **retouraanroep URL**, Hallo plakken **retouraanroep URL** u eerder hebt gekopieerd.</span><span class="sxs-lookup"><span data-stu-id="4e042-114">Then, for hello **Callback URL**, paste hello **Callback URL** you copied earlier.</span></span> <span data-ttu-id="4e042-115">Dit is de gateway van uw mobiele App toegevoegd aan de Hallo pad, */.auth/login/twitter/callback*.</span><span class="sxs-lookup"><span data-stu-id="4e042-115">This is your Mobile App gateway appended with hello path, */.auth/login/twitter/callback*.</span></span> <span data-ttu-id="4e042-116">Bijvoorbeeld `https://contoso.azurewebsites.net/.auth/login/twitter/callback`.</span><span class="sxs-lookup"><span data-stu-id="4e042-116">For example, `https://contoso.azurewebsites.net/.auth/login/twitter/callback`.</span></span> <span data-ttu-id="4e042-117">Zorg ervoor dat u van Hallo HTTPS-schema gebruikmaakt.</span><span class="sxs-lookup"><span data-stu-id="4e042-117">Make sure that you are using hello HTTPS scheme.</span></span>
4. <span data-ttu-id="4e042-118">Op de pagina voor Hallo onder hello, lees en accepteer Hallo voorwaarden.</span><span class="sxs-lookup"><span data-stu-id="4e042-118">At hello bottom hello page, read and accept hello terms.</span></span> <span data-ttu-id="4e042-119">Klik vervolgens op **uw Twitter-toepassing maken**.</span><span class="sxs-lookup"><span data-stu-id="4e042-119">Then click **Create your Twitter application**.</span></span> <span data-ttu-id="4e042-120">Deze registers Hallo app weergegeven Hallo Toepassingdetails.</span><span class="sxs-lookup"><span data-stu-id="4e042-120">This registers hello app displays hello application details.</span></span>
5. <span data-ttu-id="4e042-121">Klik op Hallo **instellingen** tabblad selectievakje **toestaan dat deze toepassing gebruikt toobe toosign met Twitter**, klikt u vervolgens op **Update-instellingen**.</span><span class="sxs-lookup"><span data-stu-id="4e042-121">Click hello **Settings** tab, check **Allow this application toobe used toosign in with Twitter**, then click **Update Settings**.</span></span>
6. <span data-ttu-id="4e042-122">Selecteer Hallo **sleutels en toegangstokens** tabblad. Maak een notitie van Hallo waarden van **Consumer-sleutel (API-sleutel)** en **consumentgeheim (API geheim)**.</span><span class="sxs-lookup"><span data-stu-id="4e042-122">Select hello **Keys and Access Tokens** tab. Make a note of hello values of **Consumer Key (API Key)** and **Consumer secret (API Secret)**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="4e042-123">Hallo consumer geheime sleutel is een belangrijke beveiligingsreferentie.</span><span class="sxs-lookup"><span data-stu-id="4e042-123">hello consumer secret is an important security credential.</span></span> <span data-ttu-id="4e042-124">Geen dit geheim met anderen delen of deze met uw app te distribueren.</span><span class="sxs-lookup"><span data-stu-id="4e042-124">Do not share this secret with anyone or distribute it with your app.</span></span>
   > 
   > 

## <span data-ttu-id="4e042-125"><a name="secrets"></a>Informatie tooyour-toepassing toevoegen Twitter</span><span class="sxs-lookup"><span data-stu-id="4e042-125"><a name="secrets"> </a>Add Twitter information tooyour application</span></span>
1. <span data-ttu-id="4e042-126">Terug in Hallo [Azure-portal], tooyour toepassing navigeren.</span><span class="sxs-lookup"><span data-stu-id="4e042-126">Back in hello [Azure portal], navigate tooyour application.</span></span> <span data-ttu-id="4e042-127">Klik op **instellingen**, en vervolgens **verificatie / autorisatie**.</span><span class="sxs-lookup"><span data-stu-id="4e042-127">Click **Settings**, and then **Authentication / Authorization**.</span></span>
2. <span data-ttu-id="4e042-128">Als Hallo verificatie / autorisatie-functie niet is ingeschakeld, schakelt u Hallo switch te**op**.</span><span class="sxs-lookup"><span data-stu-id="4e042-128">If hello Authentication / Authorization feature is not enabled, turn hello switch too**On**.</span></span>
3. <span data-ttu-id="4e042-129">Klik op **Twitter**.</span><span class="sxs-lookup"><span data-stu-id="4e042-129">Click **Twitter**.</span></span> <span data-ttu-id="4e042-130">Plak in Hallo App-ID en App-geheim waarden die u eerder hebt verkregen.</span><span class="sxs-lookup"><span data-stu-id="4e042-130">Paste in hello App ID and App Secret values which you obtained previously.</span></span> <span data-ttu-id="4e042-131">Klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="4e042-131">Then click **OK**.</span></span>
   
   ![][1]
   
   <span data-ttu-id="4e042-132">Standaard-App Service biedt verificatie maar niet beperkt geautoriseerde toegang tooyour site-inhoud en API's.</span><span class="sxs-lookup"><span data-stu-id="4e042-132">By default, App Service provides authentication but does not restrict authorized access tooyour site content and APIs.</span></span> <span data-ttu-id="4e042-133">U moet gebruikers machtigen in uw app-code.</span><span class="sxs-lookup"><span data-stu-id="4e042-133">You must authorize users in your app code.</span></span>
4. <span data-ttu-id="4e042-134">(Optioneel) toorestrict toegang tooyour site tooonly gebruikers zijn geverifieerd door Twitter, ingesteld **tootake actie wanneer de aanvraag is niet geverifieerd** te**Twitter**.</span><span class="sxs-lookup"><span data-stu-id="4e042-134">(Optional) toorestrict access tooyour site tooonly users authenticated by Twitter, set **Action tootake when request is not authenticated** too**Twitter**.</span></span> <span data-ttu-id="4e042-135">Dit vereist dat alle aanvragen worden geverifieerd en alle niet-geverifieerde aanvragen worden omgeleid tooTwitter voor verificatie.</span><span class="sxs-lookup"><span data-stu-id="4e042-135">This requires that all requests be authenticated, and all unauthenticated requests are redirected tooTwitter for authentication.</span></span>
5. <span data-ttu-id="4e042-136">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="4e042-136">Click **Save**.</span></span>

<span data-ttu-id="4e042-137">U bent nu klaar toouse Twitter voor verificatie in uw app.</span><span class="sxs-lookup"><span data-stu-id="4e042-137">You are now ready toouse Twitter for authentication in your app.</span></span>

## <span data-ttu-id="4e042-138"><a name="related-content"></a>Verwante inhoud</span><span class="sxs-lookup"><span data-stu-id="4e042-138"><a name="related-content"> </a>Related Content</span></span>
[!INCLUDE [app-service-mobile-related-content-get-started-users](../../includes/app-service-mobile-related-content-get-started-users.md)]

<!-- Images. -->

[0]: ./media/app-service-mobile-how-to-configure-twitter-authentication/app-service-twitter-redirect.png
[1]: ./media/app-service-mobile-how-to-configure-twitter-authentication/mobile-app-twitter-settings.png

<!-- URLs. -->

[Twitter ontwikkelaars]: http://go.microsoft.com/fwlink/p/?LinkId=268300
[Azure-portal]: https://portal.azure.com/
[xamarin]: ../app-services-mobile-app-xamarin-ios-get-started-users.md

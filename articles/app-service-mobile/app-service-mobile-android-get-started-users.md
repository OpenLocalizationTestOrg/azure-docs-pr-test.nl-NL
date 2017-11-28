---
title: aaaAdd verificatie op Android met Mobile Apps | Microsoft Docs
description: Meer informatie over hoe toouse Hallo functie Mobile Apps van Azure App Service tooauthenticate gebruikers van uw Android-app via een groot aantal identiteitsproviders, waaronder Google, Facebook, Twitter en Microsoft.
services: app-service\mobile
documentationcenter: android
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 1fc8e7c1-6c3c-40f4-9967-9cf5e21fc4e1
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: java
ms.topic: article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 01f608f996c931c643790ed2778df11cf590c903
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="add-authentication-tooyour-android-app"></a><span data-ttu-id="c7c6d-103">Verificatie tooyour Android-app toevoegen</span><span class="sxs-lookup"><span data-stu-id="c7c6d-103">Add authentication tooyour Android app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

## <a name="summary"></a><span data-ttu-id="c7c6d-104">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="c7c6d-104">Summary</span></span>
<span data-ttu-id="c7c6d-105">In deze zelfstudie maakt toevoegen u verificatie toohello todolist Quick Start-project op Android met behulp van een ondersteunde id-provider.</span><span class="sxs-lookup"><span data-stu-id="c7c6d-105">In this tutorial, you add authentication toohello todolist quickstart project on Android by using a supported identity provider.</span></span> <span data-ttu-id="c7c6d-106">Deze zelfstudie is gebaseerd op Hallo [aan de slag met Mobile Apps] zelfstudie die u moet eerst te voltooien.</span><span class="sxs-lookup"><span data-stu-id="c7c6d-106">This tutorial is based on hello [Get started with Mobile Apps] tutorial, which you must complete first.</span></span>

## <span data-ttu-id="c7c6d-107"><a name="register"></a>Uw app registreren voor verificatie en Azure App Service configureren</span><span class="sxs-lookup"><span data-stu-id="c7c6d-107"><a name="register"></a>Register your app for authentication and configure Azure App Service</span></span>
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

## <span data-ttu-id="c7c6d-108"><a name="redirecturl"></a>Uw app toohello toegestane externe Omleidings-URL's toevoegen</span><span class="sxs-lookup"><span data-stu-id="c7c6d-108"><a name="redirecturl"></a>Add your app toohello Allowed External Redirect URLs</span></span>

<span data-ttu-id="c7c6d-109">Veilige verificatie vereist dat u een nieuwe URL-schema voor uw app definiëren.</span><span class="sxs-lookup"><span data-stu-id="c7c6d-109">Secure authentication requires that you define a new URL scheme for your app.</span></span> <span data-ttu-id="c7c6d-110">Hierdoor Hallo verificatie system tooredirect back tooyour app zodra de Hallo verificatieproces is voltooid.</span><span class="sxs-lookup"><span data-stu-id="c7c6d-110">This allows hello authentication system tooredirect back tooyour app once hello authentication process is complete.</span></span> <span data-ttu-id="c7c6d-111">In deze zelfstudie gebruiken we Hallo URL-schema _appname_ in.</span><span class="sxs-lookup"><span data-stu-id="c7c6d-111">In this tutorial, we use hello URL scheme _appname_ throughout.</span></span> <span data-ttu-id="c7c6d-112">U kunt echter een URL-schema dat u kiest.</span><span class="sxs-lookup"><span data-stu-id="c7c6d-112">However, you can use any URL scheme you choose.</span></span> <span data-ttu-id="c7c6d-113">Deze moet uniek tooyour mobiele toepassing.</span><span class="sxs-lookup"><span data-stu-id="c7c6d-113">It should be unique tooyour mobile application.</span></span> <span data-ttu-id="c7c6d-114">Hallo-omleiding tooenable aan serverzijde Hallo:</span><span class="sxs-lookup"><span data-stu-id="c7c6d-114">tooenable hello redirection on hello server side:</span></span>

1. <span data-ttu-id="c7c6d-115">Selecteer in de Hallo [Azure portal], uw App Service.</span><span class="sxs-lookup"><span data-stu-id="c7c6d-115">In hello [Azure portal], select your App Service.</span></span>

2. <span data-ttu-id="c7c6d-116">Klik op Hallo **verificatie / autorisatie** menuoptie.</span><span class="sxs-lookup"><span data-stu-id="c7c6d-116">Click hello **Authentication / Authorization** menu option.</span></span>

3. <span data-ttu-id="c7c6d-117">In Hallo **toegestaan externe Omleidings-URL's**, voer `appname://easyauth.callback`.</span><span class="sxs-lookup"><span data-stu-id="c7c6d-117">In hello **Allowed External Redirect URLs**, enter `appname://easyauth.callback`.</span></span>  <span data-ttu-id="c7c6d-118">Hallo _appname_ in deze reeks is Hallo URL-schema voor uw mobiele toepassing.</span><span class="sxs-lookup"><span data-stu-id="c7c6d-118">hello _appname_ in this string is hello URL Scheme for your mobile application.</span></span>  <span data-ttu-id="c7c6d-119">Deze moet voldoen aan de normale URL-specificatie voor een protocol (Gebruik letters en cijfers alleen en begin met een letter).</span><span class="sxs-lookup"><span data-stu-id="c7c6d-119">It should follow normal URL specification for a protocol (use letters and numbers only, and start with a letter).</span></span>  <span data-ttu-id="c7c6d-120">U moet een notitie van Hallo-tekenreeks die u kiest, want u tooadjust uw code mobiele toepassing Hello URL-schema op verschillende plaatsen moet.</span><span class="sxs-lookup"><span data-stu-id="c7c6d-120">You should make a note of hello string that you choose as you will need tooadjust your mobile application code with hello URL Scheme in several places.</span></span>

4. <span data-ttu-id="c7c6d-121">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="c7c6d-121">Click **OK**.</span></span>

5. <span data-ttu-id="c7c6d-122">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="c7c6d-122">Click **Save**.</span></span>

## <span data-ttu-id="c7c6d-123"><a name="permissions"></a>Machtigingen tooauthenticated gebruikers beperken</span><span class="sxs-lookup"><span data-stu-id="c7c6d-123"><a name="permissions"></a>Restrict permissions tooauthenticated users</span></span>
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

* <span data-ttu-id="c7c6d-124">In Android Studio, opent u het Hallo-project u voltooid met Hallo zelfstudie [aan de slag met Mobile Apps].</span><span class="sxs-lookup"><span data-stu-id="c7c6d-124">In Android Studio, open hello project you completed with hello tutorial [Get started with Mobile Apps].</span></span> <span data-ttu-id="c7c6d-125">Van Hallo **uitvoeren** menu, klikt u op **app uitvoeren**, en controleer of dat een niet-verwerkte uitzondering met een statuscode van 401 (niet-geautoriseerd) treedt op nadat het Hallo-app wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="c7c6d-125">From hello **Run** menu, click **Run app**, and verify that an unhandled exception with a status code of 401 (Unauthorized) is raised after hello app starts.</span></span>

     <span data-ttu-id="c7c6d-126">Deze uitzondering komt doordat Hallo app pogingen tooaccess Hallo terug als een niet-geverifieerde gebruiker beëindigen, maar Hallo *TodoItem* tabel nu is verificatie vereist.</span><span class="sxs-lookup"><span data-stu-id="c7c6d-126">This exception happens because hello app attempts tooaccess hello back end as an unauthenticated user, but hello *TodoItem* table now requires authentication.</span></span>

<span data-ttu-id="c7c6d-127">Werk vervolgens Hallo app tooauthenticate gebruikers voordat u resources van Hallo die Mobile Apps back-end.</span><span class="sxs-lookup"><span data-stu-id="c7c6d-127">Next, you update hello app tooauthenticate users before requesting resources from hello Mobile Apps back end.</span></span> 

## <a name="add-authentication-toohello-app"></a><span data-ttu-id="c7c6d-128">Verificatie toohello app toevoegen</span><span class="sxs-lookup"><span data-stu-id="c7c6d-128">Add authentication toohello app</span></span>
[!INCLUDE [mobile-android-authenticate-app](../../includes/mobile-android-authenticate-app.md)]



## <span data-ttu-id="c7c6d-129"><a name="cache-tokens"></a>Cache verificatietokens op Hallo-client</span><span class="sxs-lookup"><span data-stu-id="c7c6d-129"><a name="cache-tokens"></a>Cache authentication tokens on hello client</span></span>
[!INCLUDE [mobile-android-authenticate-app-with-token](../../includes/mobile-android-authenticate-app-with-token.md)]

## <a name="next-steps"></a><span data-ttu-id="c7c6d-130">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="c7c6d-130">Next steps</span></span>
<span data-ttu-id="c7c6d-131">Nu dat u deze basisverificatie-zelfstudie hebt voltooid, kunt u overwegen tooone Hallo volgende zelfstudies verder te gaan:</span><span class="sxs-lookup"><span data-stu-id="c7c6d-131">Now that you completed this basic authentication tutorial, consider continuing on tooone of hello following tutorials:</span></span>

* <span data-ttu-id="c7c6d-132">[Push tooyour Android-app-meldingen toevoegen](app-service-mobile-android-get-started-push.md).</span><span class="sxs-lookup"><span data-stu-id="c7c6d-132">[Add push notifications tooyour Android app](app-service-mobile-android-get-started-push.md).</span></span>
  <span data-ttu-id="c7c6d-133">Meer informatie over hoe uw Mobile Apps back tooconfigure toouse Azure notification hubs toosend-pushmeldingen eindigen.</span><span class="sxs-lookup"><span data-stu-id="c7c6d-133">Learn how tooconfigure your Mobile Apps back end toouse Azure notification hubs toosend push notifications.</span></span>
* <span data-ttu-id="c7c6d-134">[Offlinesynchronisatie voor uw Android-app inschakelen](app-service-mobile-android-get-started-offline-data.md).</span><span class="sxs-lookup"><span data-stu-id="c7c6d-134">[Enable offline sync for your Android app](app-service-mobile-android-get-started-offline-data.md).</span></span>
  <span data-ttu-id="c7c6d-135">Meer informatie over hoe de offline tooadd tooyour app met behulp van een back-end van Mobile Apps ondersteunen.</span><span class="sxs-lookup"><span data-stu-id="c7c6d-135">Learn how tooadd offline support tooyour app by using a Mobile Apps back end.</span></span> <span data-ttu-id="c7c6d-136">Met het offline synchroniseren gebruikers kunnen communiceren met een mobiele app&mdash;weergeven, toevoegen of wijzigen van gegevens&mdash;zelfs wanneer er geen netwerkverbinding.</span><span class="sxs-lookup"><span data-stu-id="c7c6d-136">With offline sync, users can interact with a mobile app&mdash;viewing, adding, or modifying data&mdash;even when there is no network connection.</span></span>

<!-- Anchors. -->
[Register your app for authentication and configure Mobile Services]: #register
[Restrict table permissions tooauthenticated users]: #permissions
[Add authentication toohello app]: #add-authentication
[Store authentication tokens on hello client]: #cache-tokens
[Refresh expired tokens]: #refresh-tokens
[Next Steps]:#next-steps


<!-- URLs. -->
[aan de slag met Mobile Apps]: app-service-mobile-android-get-started.md

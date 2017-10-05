---
title: Verificatie toevoegen voor Android met Mobile Apps | Microsoft Docs
description: "Informatie over het verifiëren van gebruikers van uw Android-app via een groot aantal identiteitsproviders, waaronder Google, Facebook, Twitter en Microsoft met de functie Mobile Apps van Azure App Service."
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
ms.openlocfilehash: 81331142aa6110d4e29e6fb30a90ce6e3a853439
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="add-authentication-to-your-android-app"></a><span data-ttu-id="7f139-103">Verificatie toevoegen aan uw Android-app</span><span class="sxs-lookup"><span data-stu-id="7f139-103">Add authentication to your Android app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

## <a name="summary"></a><span data-ttu-id="7f139-104">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="7f139-104">Summary</span></span>
<span data-ttu-id="7f139-105">In deze zelfstudie maakt toevoegen u verificatie aan de todolist-Quick Start-project voor Android met behulp van een ondersteunde id-provider.</span><span class="sxs-lookup"><span data-stu-id="7f139-105">In this tutorial, you add authentication to the todolist quickstart project on Android by using a supported identity provider.</span></span> <span data-ttu-id="7f139-106">Deze zelfstudie is gebaseerd op de [aan de slag met Mobile Apps] zelfstudie die u moet eerst te voltooien.</span><span class="sxs-lookup"><span data-stu-id="7f139-106">This tutorial is based on the [Get started with Mobile Apps] tutorial, which you must complete first.</span></span>

## <span data-ttu-id="7f139-107"><a name="register"></a>Uw app registreren voor verificatie en Azure App Service configureren</span><span class="sxs-lookup"><span data-stu-id="7f139-107"><a name="register"></a>Register your app for authentication and configure Azure App Service</span></span>
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

## <span data-ttu-id="7f139-108"><a name="redirecturl"></a>Uw app toevoegen aan de toegestane externe Omleidings-URL 's</span><span class="sxs-lookup"><span data-stu-id="7f139-108"><a name="redirecturl"></a>Add your app to the Allowed External Redirect URLs</span></span>

<span data-ttu-id="7f139-109">Veilige verificatie vereist dat u een nieuwe URL-schema voor uw app definiëren.</span><span class="sxs-lookup"><span data-stu-id="7f139-109">Secure authentication requires that you define a new URL scheme for your app.</span></span> <span data-ttu-id="7f139-110">Hierdoor kan de verificatiesysteem terug te keren naar uw app zodra het verificatieproces voltooid is.</span><span class="sxs-lookup"><span data-stu-id="7f139-110">This allows the authentication system to redirect back to your app once the authentication process is complete.</span></span> <span data-ttu-id="7f139-111">In deze zelfstudie gebruiken we het URL-schema _appname_ in.</span><span class="sxs-lookup"><span data-stu-id="7f139-111">In this tutorial, we use the URL scheme _appname_ throughout.</span></span> <span data-ttu-id="7f139-112">U kunt echter een URL-schema dat u kiest.</span><span class="sxs-lookup"><span data-stu-id="7f139-112">However, you can use any URL scheme you choose.</span></span> <span data-ttu-id="7f139-113">Deze moet uniek zijn voor uw mobiele App.</span><span class="sxs-lookup"><span data-stu-id="7f139-113">It should be unique to your mobile application.</span></span> <span data-ttu-id="7f139-114">De omleiding op de server inschakelen:</span><span class="sxs-lookup"><span data-stu-id="7f139-114">To enable the redirection on the server side:</span></span>

1. <span data-ttu-id="7f139-115">Selecteer in de [Azure-portal] uw App Service.</span><span class="sxs-lookup"><span data-stu-id="7f139-115">In the [Azure portal], select your App Service.</span></span>

2. <span data-ttu-id="7f139-116">Klik op de **verificatie / autorisatie** menuoptie.</span><span class="sxs-lookup"><span data-stu-id="7f139-116">Click the **Authentication / Authorization** menu option.</span></span>

3. <span data-ttu-id="7f139-117">In de **toegestaan externe Omleidings-URL's**, voer `appname://easyauth.callback`.</span><span class="sxs-lookup"><span data-stu-id="7f139-117">In the **Allowed External Redirect URLs**, enter `appname://easyauth.callback`.</span></span>  <span data-ttu-id="7f139-118">De _appname_ in deze tekenreeks wordt het URL-schema voor uw mobiele toepassing.</span><span class="sxs-lookup"><span data-stu-id="7f139-118">The _appname_ in this string is the URL Scheme for your mobile application.</span></span>  <span data-ttu-id="7f139-119">Deze moet voldoen aan de normale URL-specificatie voor een protocol (Gebruik letters en cijfers alleen en begin met een letter).</span><span class="sxs-lookup"><span data-stu-id="7f139-119">It should follow normal URL specification for a protocol (use letters and numbers only, and start with a letter).</span></span>  <span data-ttu-id="7f139-120">U moet een notitie van de tekenreeks die u naar wens aanpassen van uw mobiele toepassingscode met het URL-schema op verschillende plaatsen.</span><span class="sxs-lookup"><span data-stu-id="7f139-120">You should make a note of the string that you choose as you will need to adjust your mobile application code with the URL Scheme in several places.</span></span>

4. <span data-ttu-id="7f139-121">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="7f139-121">Click **OK**.</span></span>

5. <span data-ttu-id="7f139-122">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="7f139-122">Click **Save**.</span></span>

## <span data-ttu-id="7f139-123"><a name="permissions"></a>Machtigingen beperken voor geverifieerde gebruikers</span><span class="sxs-lookup"><span data-stu-id="7f139-123"><a name="permissions"></a>Restrict permissions to authenticated users</span></span>
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

* <span data-ttu-id="7f139-124">In Android Studio, opent u het project u voltooid met de zelfstudie [aan de slag met Mobile Apps].</span><span class="sxs-lookup"><span data-stu-id="7f139-124">In Android Studio, open the project you completed with the tutorial [Get started with Mobile Apps].</span></span> <span data-ttu-id="7f139-125">Van de **uitvoeren** menu, klikt u op **app uitvoeren**, en controleer of dat een niet-verwerkte uitzondering met een statuscode van 401 (niet-geautoriseerd) treedt op nadat de app wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="7f139-125">From the **Run** menu, click **Run app**, and verify that an unhandled exception with a status code of 401 (Unauthorized) is raised after the app starts.</span></span>

     <span data-ttu-id="7f139-126">Deze uitzondering treedt op omdat de app probeert te krijgen tot de back-end als niet-geverifieerde gebruiker, maar de *TodoItem* tabel nu is verificatie vereist.</span><span class="sxs-lookup"><span data-stu-id="7f139-126">This exception happens because the app attempts to access the back end as an unauthenticated user, but the *TodoItem* table now requires authentication.</span></span>

<span data-ttu-id="7f139-127">Werk vervolgens de app om gebruikers te verifiëren voordat u resources van de back-end van Mobile Apps.</span><span class="sxs-lookup"><span data-stu-id="7f139-127">Next, you update the app to authenticate users before requesting resources from the Mobile Apps back end.</span></span> 

## <a name="add-authentication-to-the-app"></a><span data-ttu-id="7f139-128">Verificatie toevoegen aan de app.</span><span class="sxs-lookup"><span data-stu-id="7f139-128">Add authentication to the app</span></span>
[!INCLUDE [mobile-android-authenticate-app](../../includes/mobile-android-authenticate-app.md)]



## <span data-ttu-id="7f139-129"><a name="cache-tokens"></a>Verificatietokens cache op de client</span><span class="sxs-lookup"><span data-stu-id="7f139-129"><a name="cache-tokens"></a>Cache authentication tokens on the client</span></span>
[!INCLUDE [mobile-android-authenticate-app-with-token](../../includes/mobile-android-authenticate-app-with-token.md)]

## <a name="next-steps"></a><span data-ttu-id="7f139-130">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="7f139-130">Next steps</span></span>
<span data-ttu-id="7f139-131">Nu dat u deze basisverificatie-zelfstudie hebt voltooid, overweeg dan u verder gaat u aan bij een van de volgende zelfstudies:</span><span class="sxs-lookup"><span data-stu-id="7f139-131">Now that you completed this basic authentication tutorial, consider continuing on to one of the following tutorials:</span></span>

* <span data-ttu-id="7f139-132">[Pushmeldingen toevoegen aan uw Android-app](app-service-mobile-android-get-started-push.md).</span><span class="sxs-lookup"><span data-stu-id="7f139-132">[Add push notifications to your Android app](app-service-mobile-android-get-started-push.md).</span></span>
  <span data-ttu-id="7f139-133">Informatie over het configureren van uw back-end van Mobile Apps voor het gebruik van Azure notification hubs pushmeldingen verzendt.</span><span class="sxs-lookup"><span data-stu-id="7f139-133">Learn how to configure your Mobile Apps back end to use Azure notification hubs to send push notifications.</span></span>
* <span data-ttu-id="7f139-134">[Offlinesynchronisatie voor uw Android-app inschakelen](app-service-mobile-android-get-started-offline-data.md).</span><span class="sxs-lookup"><span data-stu-id="7f139-134">[Enable offline sync for your Android app](app-service-mobile-android-get-started-offline-data.md).</span></span>
  <span data-ttu-id="7f139-135">Informatie over het toevoegen van Offlineondersteuning aan uw app met behulp van een back-end van Mobile Apps.</span><span class="sxs-lookup"><span data-stu-id="7f139-135">Learn how to add offline support to your app by using a Mobile Apps back end.</span></span> <span data-ttu-id="7f139-136">Met het offline synchroniseren gebruikers kunnen communiceren met een mobiele app&mdash;weergeven, toevoegen of wijzigen van gegevens&mdash;zelfs wanneer er geen netwerkverbinding.</span><span class="sxs-lookup"><span data-stu-id="7f139-136">With offline sync, users can interact with a mobile app&mdash;viewing, adding, or modifying data&mdash;even when there is no network connection.</span></span>

<!-- Anchors. -->
[Register your app for authentication and configure Mobile Services]: #register
[Restrict table permissions to authenticated users]: #permissions
[Add authentication to the app]: #add-authentication
[Store authentication tokens on the client]: #cache-tokens
[Refresh expired tokens]: #refresh-tokens
[Next Steps]:#next-steps


<!-- URLs. -->
<span data-ttu-id="7f139-137">[aan de slag met Mobile Apps]: app-service-mobile-android-get-started.md</span><span class="sxs-lookup"><span data-stu-id="7f139-137">[Get started with Mobile Apps]: app-service-mobile-android-get-started.md</span></span>

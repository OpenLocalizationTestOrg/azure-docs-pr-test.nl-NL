---
title: Verificatie toevoegen op Apache Cordova met Mobile Apps | Microsoft Docs
description: "Informatie over het verifiëren van gebruikers van uw Apache Cordova-app via een groot aantal identiteitsproviders, waaronder Google, Facebook, Twitter en Microsoft met Mobile Apps in Azure App Service."
services: app-service\mobile
documentationcenter: javascript
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 10dd6dc9-ddf5-423d-8205-00ad74929f0d
ms.service: app-service-mobile
ms.workload: na
ms.tgt_pltfrm: mobile-html
ms.devlang: javascript
ms.topic: article
ms.date: 10/30/2016
ms.author: glenga
ms.openlocfilehash: b7362b7f26859de541f792e714502851d74c98e5
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="add-authentication-to-your-apache-cordova-app"></a><span data-ttu-id="b52f4-103">Verificatie toevoegen aan uw Apache Cordova-app</span><span class="sxs-lookup"><span data-stu-id="b52f4-103">Add authentication to your Apache Cordova app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

## <a name="summary"></a><span data-ttu-id="b52f4-104">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="b52f4-104">Summary</span></span>
<span data-ttu-id="b52f4-105">In deze zelfstudie kunt u verificatie toevoegen aan de todolist-Quick Start-project op Apache Cordova met behulp van een ondersteunde id-provider.</span><span class="sxs-lookup"><span data-stu-id="b52f4-105">In this tutorial, you add authentication to the todolist quickstart project on Apache Cordova using a supported identity provider.</span></span> <span data-ttu-id="b52f4-106">Deze zelfstudie is gebaseerd op de [aan de slag met Mobile Apps] zelfstudie die u moet eerst te voltooien.</span><span class="sxs-lookup"><span data-stu-id="b52f4-106">This tutorial is based on the [Get started with Mobile Apps] tutorial, which you must complete first.</span></span>

## <span data-ttu-id="b52f4-107"><a name="register"></a>Uw app registreren voor verificatie en de App Service configureren</span><span class="sxs-lookup"><span data-stu-id="b52f4-107"><a name="register"></a>Register your app for authentication and configure the App Service</span></span>
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

[<span data-ttu-id="b52f4-108">Bekijk een video van vergelijkbare stappen</span><span class="sxs-lookup"><span data-stu-id="b52f4-108">Watch a video showing similar steps</span></span>](https://channel9.msdn.com/series/Azure-connected-services-with-Cordova/Azure-connected-services-task-8-Azure-authentication)

## <span data-ttu-id="b52f4-109"><a name="permissions"></a>Machtigingen beperken voor geverifieerde gebruikers</span><span class="sxs-lookup"><span data-stu-id="b52f4-109"><a name="permissions"></a>Restrict permissions to authenticated users</span></span>
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

<span data-ttu-id="b52f4-110">Nu kunt u controleren of anonieme toegang tot uw back-end is uitgeschakeld.</span><span class="sxs-lookup"><span data-stu-id="b52f4-110">Now, you can verify that anonymous access to your backend has been disabled.</span></span> <span data-ttu-id="b52f4-111">In Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="b52f4-111">In Visual Studio:</span></span>

* <span data-ttu-id="b52f4-112">Open het project dat u hebt gemaakt toen u de zelfstudie voltooid [aan de slag met Mobile Apps].</span><span class="sxs-lookup"><span data-stu-id="b52f4-112">Open the project that you created when you completed the tutorial [Get started with Mobile Apps].</span></span>
* <span data-ttu-id="b52f4-113">Uw toepassing uitvoeren in de **Google Android-Emulator**.</span><span class="sxs-lookup"><span data-stu-id="b52f4-113">Run your application in the **Google Android Emulator**.</span></span>
* <span data-ttu-id="b52f4-114">Controleer of er een onverwachte fout in de verbinding wordt weergegeven nadat de app is gestart.</span><span class="sxs-lookup"><span data-stu-id="b52f4-114">Verify that an Unexpected Connection Failure is shown after the app starts.</span></span>

<span data-ttu-id="b52f4-115">Werk vervolgens de app om gebruikers te verifiëren voordat u resources van de back-end voor de mobiele App.</span><span class="sxs-lookup"><span data-stu-id="b52f4-115">Next, update the app to authenticate users before requesting resources from the Mobile App backend.</span></span>

## <span data-ttu-id="b52f4-116"><a name="add-authentication"></a>Verificatie toevoegen aan de app.</span><span class="sxs-lookup"><span data-stu-id="b52f4-116"><a name="add-authentication"></a>Add authentication to the app</span></span>
1. <span data-ttu-id="b52f4-117">Open het project in **Visual Studio**, open vervolgens de `www/index.html` bestand voor bewerken.</span><span class="sxs-lookup"><span data-stu-id="b52f4-117">Open your project in **Visual Studio**, then open the `www/index.html` file for editing.</span></span>
2. <span data-ttu-id="b52f4-118">Zoek de `Content-Security-Policy` meta-code in het gedeelte head.</span><span class="sxs-lookup"><span data-stu-id="b52f4-118">Locate the `Content-Security-Policy` meta tag in the head section.</span></span>  <span data-ttu-id="b52f4-119">De OAuth host toevoegt aan de lijst met toegestane bronnen.</span><span class="sxs-lookup"><span data-stu-id="b52f4-119">Add the OAuth host to the list of allowed sources.</span></span>

   | <span data-ttu-id="b52f4-120">Provider</span><span class="sxs-lookup"><span data-stu-id="b52f4-120">Provider</span></span> | <span data-ttu-id="b52f4-121">De naam van de SDK-Provider</span><span class="sxs-lookup"><span data-stu-id="b52f4-121">SDK Provider Name</span></span> | <span data-ttu-id="b52f4-122">OAuth-Host</span><span class="sxs-lookup"><span data-stu-id="b52f4-122">OAuth Host</span></span> |
   |:--- |:--- |:--- |
   | <span data-ttu-id="b52f4-123">Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b52f4-123">Azure Active Directory</span></span> | <span data-ttu-id="b52f4-124">AAD</span><span class="sxs-lookup"><span data-stu-id="b52f4-124">aad</span></span> | <span data-ttu-id="b52f4-125">https://login.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="b52f4-125">https://login.microsoftonline.com</span></span> |
   | <span data-ttu-id="b52f4-126">Facebook</span><span class="sxs-lookup"><span data-stu-id="b52f4-126">Facebook</span></span> | <span data-ttu-id="b52f4-127">Facebook</span><span class="sxs-lookup"><span data-stu-id="b52f4-127">facebook</span></span> | <span data-ttu-id="b52f4-128">https://www.Facebook.com</span><span class="sxs-lookup"><span data-stu-id="b52f4-128">https://www.facebook.com</span></span> |
   | <span data-ttu-id="b52f4-129">Google</span><span class="sxs-lookup"><span data-stu-id="b52f4-129">Google</span></span> | <span data-ttu-id="b52f4-130">Google</span><span class="sxs-lookup"><span data-stu-id="b52f4-130">google</span></span> | <span data-ttu-id="b52f4-131">https://accounts.Google.com</span><span class="sxs-lookup"><span data-stu-id="b52f4-131">https://accounts.google.com</span></span> |
   | <span data-ttu-id="b52f4-132">Microsoft</span><span class="sxs-lookup"><span data-stu-id="b52f4-132">Microsoft</span></span> | <span data-ttu-id="b52f4-133">MicrosoftAccount</span><span class="sxs-lookup"><span data-stu-id="b52f4-133">microsoftaccount</span></span> | <span data-ttu-id="b52f4-134">https://login.live.com</span><span class="sxs-lookup"><span data-stu-id="b52f4-134">https://login.live.com</span></span> |
   | <span data-ttu-id="b52f4-135">Twitter</span><span class="sxs-lookup"><span data-stu-id="b52f4-135">Twitter</span></span> | <span data-ttu-id="b52f4-136">Twitter</span><span class="sxs-lookup"><span data-stu-id="b52f4-136">twitter</span></span> | <span data-ttu-id="b52f4-137">https://API.Twitter.com</span><span class="sxs-lookup"><span data-stu-id="b52f4-137">https://api.twitter.com</span></span> |

    <span data-ttu-id="b52f4-138">Een voorbeeld van de inhoud-Security-beleid (toegepast voor Azure Active Directory) is als volgt:</span><span class="sxs-lookup"><span data-stu-id="b52f4-138">An example Content-Security-Policy (implemented for Azure Active Directory) is as follows:</span></span>

        <meta http-equiv="Content-Security-Policy" content="default-src 'self'
            data: gap: https://login.microsoftonline.com https://yourapp.azurewebsites.net; style-src 'self'">

    <span data-ttu-id="b52f4-139">Vervang `https://login.microsoftonline.com` met de OAuth-host uit de voorgaande tabel.</span><span class="sxs-lookup"><span data-stu-id="b52f4-139">Replace `https://login.microsoftonline.com` with the OAuth host from the preceding table.</span></span>  <span data-ttu-id="b52f4-140">Zie voor meer informatie over de inhoud beveiligingsbeleid meta-code, de [inhoud beveiligingsbeleid documentatie].</span><span class="sxs-lookup"><span data-stu-id="b52f4-140">For more information about the content-security-policy meta tag, see the [Content-Security-Policy documentation].</span></span>

    <span data-ttu-id="b52f4-141">Sommige verificatieproviders vereisen geen dat inhoud beveiligingsbeleid wijzigingen bij op de juiste mobiele apparaten.</span><span class="sxs-lookup"><span data-stu-id="b52f4-141">Some authentication providers do not require Content-Security-Policy changes when used on appropriate mobile devices.</span></span>  <span data-ttu-id="b52f4-142">Er zijn geen inhoud beveiligingsbeleid wijzigingen zijn vereist met Google-verificatie op een Android-apparaat.</span><span class="sxs-lookup"><span data-stu-id="b52f4-142">For example, no Content-Security-Policy changes are required when using Google authentication on an Android device.</span></span>

3. <span data-ttu-id="b52f4-143">Open de `www/js/index.js` voor het bewerken van het bestand, zoek de `onDeviceReady()` methode, en onder het maken van de client code toe te voegen met de volgende code:</span><span class="sxs-lookup"><span data-stu-id="b52f4-143">Open the `www/js/index.js` file for editing, locate the `onDeviceReady()` method, and under the client  creation code add the following code:</span></span>

        // Login to the service
        client.login('SDK_Provider_Name')
            .then(function () {

                // BEGINNING OF ORIGINAL CODE

                // Create a table reference
                todoItemTable = client.getTable('todoitem');

                // Refresh the todoItems
                refreshDisplay();

                // Wire up the UI Event Handler for the Add Item
                $('#add-item').submit(addItemHandler);
                $('#refresh').on('click', refreshDisplay);

                // END OF ORIGINAL CODE

            }, handleError);

    <span data-ttu-id="b52f4-144">Deze code vervangt de bestaande code die de tabelverwijzing maakt en de gebruikersinterface vernieuwt.</span><span class="sxs-lookup"><span data-stu-id="b52f4-144">This code replaces the existing code that creates the table reference and refreshes the UI.</span></span>

    <span data-ttu-id="b52f4-145">De methode login() begint verificatie met de provider.</span><span class="sxs-lookup"><span data-stu-id="b52f4-145">The login() method starts authentication with the provider.</span></span> <span data-ttu-id="b52f4-146">De methode login() is een async-functie die een JavaScript-belofte retourneert.</span><span class="sxs-lookup"><span data-stu-id="b52f4-146">The login() method is an async function that returns a JavaScript Promise.</span></span>  <span data-ttu-id="b52f4-147">De rest van de initialisatie van de wordt in het antwoord CTP geplaatst zodat deze wordt niet uitgevoerd totdat de login()-methode is voltooid.</span><span class="sxs-lookup"><span data-stu-id="b52f4-147">The rest of the initialization is placed inside the promise response so that it is not executed until the login() method completes.</span></span>

4. <span data-ttu-id="b52f4-148">Vervang in de code die u zojuist hebt toegevoegd, `SDK_Provider_Name` met de naam van de aanmeldingsprovider van uw.</span><span class="sxs-lookup"><span data-stu-id="b52f4-148">In the code that you just added, replace `SDK_Provider_Name` with the name of your login provider.</span></span> <span data-ttu-id="b52f4-149">Bijvoorbeeld: voor Azure Active Directory, gebruiken `client.login('aad')`.</span><span class="sxs-lookup"><span data-stu-id="b52f4-149">For example, for Azure Active Directory, use `client.login('aad')`.</span></span>
5. <span data-ttu-id="b52f4-150">Voer uw project.</span><span class="sxs-lookup"><span data-stu-id="b52f4-150">Run your project.</span></span>  <span data-ttu-id="b52f4-151">Wanneer het project is geïnitialiseerd, ziet uw toepassing de OAuth-aanmeldingspagina voor de gekozen verificatieprovider.</span><span class="sxs-lookup"><span data-stu-id="b52f4-151">When the project has finished initializing, your application shows the OAuth login page for the chosen authentication provider.</span></span>

## <span data-ttu-id="b52f4-152"><a name="next-steps"></a>Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="b52f4-152"><a name="next-steps"></a>Next Steps</span></span>
* <span data-ttu-id="b52f4-153">Meer informatie [over verificatie] met Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="b52f4-153">Learn more [About Authentication] with Azure App Service.</span></span>
* <span data-ttu-id="b52f4-154">De zelfstudie gaan door toe te voegen [Pushmeldingen] aan uw Apache Cordova-app.</span><span class="sxs-lookup"><span data-stu-id="b52f4-154">Continue the tutorial by adding [Push Notifications] to your Apache Cordova app.</span></span>

<span data-ttu-id="b52f4-155">Informatie over het gebruik van de SDK's.</span><span class="sxs-lookup"><span data-stu-id="b52f4-155">Learn how to use the SDKs.</span></span>

* <span data-ttu-id="b52f4-156">[Apache Cordova SDK]</span><span class="sxs-lookup"><span data-stu-id="b52f4-156">[Apache Cordova SDK]</span></span>
* <span data-ttu-id="b52f4-157">[ASP.NET Server SDK]</span><span class="sxs-lookup"><span data-stu-id="b52f4-157">[ASP.NET Server SDK]</span></span>
* <span data-ttu-id="b52f4-158">[Node.js Server SDK]</span><span class="sxs-lookup"><span data-stu-id="b52f4-158">[Node.js Server SDK]</span></span>

<!-- URLs. -->
<span data-ttu-id="b52f4-159">[aan de slag met Mobile Apps]: app-service-mobile-cordova-get-started.md</span><span class="sxs-lookup"><span data-stu-id="b52f4-159">[Get started with Mobile Apps]: app-service-mobile-cordova-get-started.md</span></span>
<span data-ttu-id="b52f4-160">[inhoud beveiligingsbeleid documentatie]: https://cordova.apache.org/docs/en/latest/guide/appdev/whitelist/index.html</span><span class="sxs-lookup"><span data-stu-id="b52f4-160">[Content-Security-Policy documentation]: https://cordova.apache.org/docs/en/latest/guide/appdev/whitelist/index.html</span></span>
<span data-ttu-id="b52f4-161">[Pushmeldingen]: app-service-mobile-cordova-get-started-push.md</span><span class="sxs-lookup"><span data-stu-id="b52f4-161">[Push Notifications]: app-service-mobile-cordova-get-started-push.md</span></span>
<span data-ttu-id="b52f4-162">[over verificatie]: app-service-mobile-auth.md</span><span class="sxs-lookup"><span data-stu-id="b52f4-162">[About Authentication]: app-service-mobile-auth.md</span></span>
<span data-ttu-id="b52f4-163">[Apache Cordova SDK]: app-service-mobile-cordova-how-to-use-client-library.md</span><span class="sxs-lookup"><span data-stu-id="b52f4-163">[Apache Cordova SDK]: app-service-mobile-cordova-how-to-use-client-library.md</span></span>
<span data-ttu-id="b52f4-164">[ASP.NET Server SDK]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md</span><span class="sxs-lookup"><span data-stu-id="b52f4-164">[ASP.NET Server SDK]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md</span></span>
<span data-ttu-id="b52f4-165">[Node.js Server SDK]: app-service-mobile-node-backend-how-to-use-server-sdk.md</span><span class="sxs-lookup"><span data-stu-id="b52f4-165">[Node.js Server SDK]: app-service-mobile-node-backend-how-to-use-server-sdk.md</span></span>

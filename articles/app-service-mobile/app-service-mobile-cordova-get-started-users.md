---
title: aaaAdd verificatie op Apache Cordova met Mobile Apps | Microsoft Docs
description: Meer informatie over hoe toouse Mobile Apps in Azure App Service tooauthenticate gebruikers van uw Apache Cordova-app via een groot aantal identiteitsproviders, waaronder Google, Facebook, Twitter en Microsoft.
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
ms.openlocfilehash: 61a05c5ac67fd0f0bc4c9d6920954a9b464a0a8d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="add-authentication-tooyour-apache-cordova-app"></a><span data-ttu-id="f3f19-103">Verificatie tooyour Apache Cordova-app toevoegen</span><span class="sxs-lookup"><span data-stu-id="f3f19-103">Add authentication tooyour Apache Cordova app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

## <a name="summary"></a><span data-ttu-id="f3f19-104">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="f3f19-104">Summary</span></span>
<span data-ttu-id="f3f19-105">In deze zelfstudie kunt u verificatie toohello todolist Quick Start-project toevoegen op Apache Cordova met behulp van een ondersteunde id-provider.</span><span class="sxs-lookup"><span data-stu-id="f3f19-105">In this tutorial, you add authentication toohello todolist quickstart project on Apache Cordova using a supported identity provider.</span></span> <span data-ttu-id="f3f19-106">Deze zelfstudie is gebaseerd op Hallo [aan de slag met Mobile Apps] zelfstudie die u moet eerst te voltooien.</span><span class="sxs-lookup"><span data-stu-id="f3f19-106">This tutorial is based on hello [Get started with Mobile Apps] tutorial, which you must complete first.</span></span>

## <span data-ttu-id="f3f19-107"><a name="register"></a>Uw app registreren voor verificatie en Hallo App Service configureren</span><span class="sxs-lookup"><span data-stu-id="f3f19-107"><a name="register"></a>Register your app for authentication and configure hello App Service</span></span>
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

[<span data-ttu-id="f3f19-108">Bekijk een video van vergelijkbare stappen</span><span class="sxs-lookup"><span data-stu-id="f3f19-108">Watch a video showing similar steps</span></span>](https://channel9.msdn.com/series/Azure-connected-services-with-Cordova/Azure-connected-services-task-8-Azure-authentication)

## <span data-ttu-id="f3f19-109"><a name="permissions"></a>Machtigingen tooauthenticated gebruikers beperken</span><span class="sxs-lookup"><span data-stu-id="f3f19-109"><a name="permissions"></a>Restrict permissions tooauthenticated users</span></span>
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

<span data-ttu-id="f3f19-110">U kunt nu controleren dat die back-end voor anonieme toegang tooyour is uitgeschakeld.</span><span class="sxs-lookup"><span data-stu-id="f3f19-110">Now, you can verify that anonymous access tooyour backend has been disabled.</span></span> <span data-ttu-id="f3f19-111">In Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="f3f19-111">In Visual Studio:</span></span>

* <span data-ttu-id="f3f19-112">Open Hallo-project dat u hebt gemaakt toen u Hallo-zelfstudie voltooid [aan de slag met Mobile Apps].</span><span class="sxs-lookup"><span data-stu-id="f3f19-112">Open hello project that you created when you completed hello tutorial [Get started with Mobile Apps].</span></span>
* <span data-ttu-id="f3f19-113">Uw toepassing uitvoeren in Hallo **Google Android-Emulator**.</span><span class="sxs-lookup"><span data-stu-id="f3f19-113">Run your application in hello **Google Android Emulator**.</span></span>
* <span data-ttu-id="f3f19-114">Controleer of er een onverwachte fout in de verbinding wordt weergegeven nadat Hallo app is gestart.</span><span class="sxs-lookup"><span data-stu-id="f3f19-114">Verify that an Unexpected Connection Failure is shown after hello app starts.</span></span>

<span data-ttu-id="f3f19-115">Werk vervolgens Hallo app tooauthenticate gebruikers voordat u resources van Hallo-end voor mobiele App.</span><span class="sxs-lookup"><span data-stu-id="f3f19-115">Next, update hello app tooauthenticate users before requesting resources from hello Mobile App backend.</span></span>

## <span data-ttu-id="f3f19-116"><a name="add-authentication"></a>Verificatie toohello app toevoegen</span><span class="sxs-lookup"><span data-stu-id="f3f19-116"><a name="add-authentication"></a>Add authentication toohello app</span></span>
1. <span data-ttu-id="f3f19-117">Open het project in **Visual Studio**, open vervolgens Hallo `www/index.html` bestand voor bewerken.</span><span class="sxs-lookup"><span data-stu-id="f3f19-117">Open your project in **Visual Studio**, then open hello `www/index.html` file for editing.</span></span>
2. <span data-ttu-id="f3f19-118">Zoek Hallo `Content-Security-Policy` meta-code in Hallo head-sectie.</span><span class="sxs-lookup"><span data-stu-id="f3f19-118">Locate hello `Content-Security-Policy` meta tag in hello head section.</span></span>  <span data-ttu-id="f3f19-119">Hallo OAuth host toohello lijst van toegestane bronnen toevoegen.</span><span class="sxs-lookup"><span data-stu-id="f3f19-119">Add hello OAuth host toohello list of allowed sources.</span></span>

   | <span data-ttu-id="f3f19-120">Provider</span><span class="sxs-lookup"><span data-stu-id="f3f19-120">Provider</span></span> | <span data-ttu-id="f3f19-121">De naam van de SDK-Provider</span><span class="sxs-lookup"><span data-stu-id="f3f19-121">SDK Provider Name</span></span> | <span data-ttu-id="f3f19-122">OAuth-Host</span><span class="sxs-lookup"><span data-stu-id="f3f19-122">OAuth Host</span></span> |
   |:--- |:--- |:--- |
   | <span data-ttu-id="f3f19-123">Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f3f19-123">Azure Active Directory</span></span> | <span data-ttu-id="f3f19-124">AAD</span><span class="sxs-lookup"><span data-stu-id="f3f19-124">aad</span></span> | <span data-ttu-id="f3f19-125">https://login.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="f3f19-125">https://login.microsoftonline.com</span></span> |
   | <span data-ttu-id="f3f19-126">Facebook</span><span class="sxs-lookup"><span data-stu-id="f3f19-126">Facebook</span></span> | <span data-ttu-id="f3f19-127">Facebook</span><span class="sxs-lookup"><span data-stu-id="f3f19-127">facebook</span></span> | <span data-ttu-id="f3f19-128">https://www.Facebook.com</span><span class="sxs-lookup"><span data-stu-id="f3f19-128">https://www.facebook.com</span></span> |
   | <span data-ttu-id="f3f19-129">Google</span><span class="sxs-lookup"><span data-stu-id="f3f19-129">Google</span></span> | <span data-ttu-id="f3f19-130">Google</span><span class="sxs-lookup"><span data-stu-id="f3f19-130">google</span></span> | <span data-ttu-id="f3f19-131">https://accounts.Google.com</span><span class="sxs-lookup"><span data-stu-id="f3f19-131">https://accounts.google.com</span></span> |
   | <span data-ttu-id="f3f19-132">Microsoft</span><span class="sxs-lookup"><span data-stu-id="f3f19-132">Microsoft</span></span> | <span data-ttu-id="f3f19-133">MicrosoftAccount</span><span class="sxs-lookup"><span data-stu-id="f3f19-133">microsoftaccount</span></span> | <span data-ttu-id="f3f19-134">https://login.live.com</span><span class="sxs-lookup"><span data-stu-id="f3f19-134">https://login.live.com</span></span> |
   | <span data-ttu-id="f3f19-135">Twitter</span><span class="sxs-lookup"><span data-stu-id="f3f19-135">Twitter</span></span> | <span data-ttu-id="f3f19-136">Twitter</span><span class="sxs-lookup"><span data-stu-id="f3f19-136">twitter</span></span> | <span data-ttu-id="f3f19-137">https://API.Twitter.com</span><span class="sxs-lookup"><span data-stu-id="f3f19-137">https://api.twitter.com</span></span> |

    <span data-ttu-id="f3f19-138">Een voorbeeld van de inhoud-Security-beleid (toegepast voor Azure Active Directory) is als volgt:</span><span class="sxs-lookup"><span data-stu-id="f3f19-138">An example Content-Security-Policy (implemented for Azure Active Directory) is as follows:</span></span>

        <meta http-equiv="Content-Security-Policy" content="default-src 'self'
            data: gap: https://login.microsoftonline.com https://yourapp.azurewebsites.net; style-src 'self'">

    <span data-ttu-id="f3f19-139">Vervang `https://login.microsoftonline.com` met OAuth host Hallo Hallo voorafgaand aan de tabel.</span><span class="sxs-lookup"><span data-stu-id="f3f19-139">Replace `https://login.microsoftonline.com` with hello OAuth host from hello preceding table.</span></span>  <span data-ttu-id="f3f19-140">Zie voor meer informatie over Hallo inhoud beveiligingsbeleid metatag Hallo [inhoud beveiligingsbeleid documentatie].</span><span class="sxs-lookup"><span data-stu-id="f3f19-140">For more information about hello content-security-policy meta tag, see hello [Content-Security-Policy documentation].</span></span>

    <span data-ttu-id="f3f19-141">Sommige verificatieproviders vereisen geen dat inhoud beveiligingsbeleid wijzigingen bij op de juiste mobiele apparaten.</span><span class="sxs-lookup"><span data-stu-id="f3f19-141">Some authentication providers do not require Content-Security-Policy changes when used on appropriate mobile devices.</span></span>  <span data-ttu-id="f3f19-142">Er zijn geen inhoud beveiligingsbeleid wijzigingen zijn vereist met Google-verificatie op een Android-apparaat.</span><span class="sxs-lookup"><span data-stu-id="f3f19-142">For example, no Content-Security-Policy changes are required when using Google authentication on an Android device.</span></span>

3. <span data-ttu-id="f3f19-143">Open Hallo `www/js/index.js` voor het bewerken van het bestand, zoek Hallo `onDeviceReady()` methode, en onder Hallo client maken code toe te voegen Hallo code te volgen:</span><span class="sxs-lookup"><span data-stu-id="f3f19-143">Open hello `www/js/index.js` file for editing, locate hello `onDeviceReady()` method, and under hello client  creation code add hello following code:</span></span>

        // Login toohello service
        client.login('SDK_Provider_Name')
            .then(function () {

                // BEGINNING OF ORIGINAL CODE

                // Create a table reference
                todoItemTable = client.getTable('todoitem');

                // Refresh hello todoItems
                refreshDisplay();

                // Wire up hello UI Event Handler for hello Add Item
                $('#add-item').submit(addItemHandler);
                $('#refresh').on('click', refreshDisplay);

                // END OF ORIGINAL CODE

            }, handleError);

    <span data-ttu-id="f3f19-144">Deze code vervangt de bestaande code Hallo die Hallo tabelverwijzing maakt en Hallo UI vernieuwt.</span><span class="sxs-lookup"><span data-stu-id="f3f19-144">This code replaces hello existing code that creates hello table reference and refreshes hello UI.</span></span>

    <span data-ttu-id="f3f19-145">verificatie begint Hallo login() methode met het Hallo-provider.</span><span class="sxs-lookup"><span data-stu-id="f3f19-145">hello login() method starts authentication with hello provider.</span></span> <span data-ttu-id="f3f19-146">Hallo login() methode is een async-functie die een JavaScript-belofte retourneert.</span><span class="sxs-lookup"><span data-stu-id="f3f19-146">hello login() method is an async function that returns a JavaScript Promise.</span></span>  <span data-ttu-id="f3f19-147">Hallo rest van de initialisatie van de Hallo wordt geplaatst in het antwoord van de belofte Hallo zodat deze wordt niet uitgevoerd totdat Hallo login() methode is voltooid.</span><span class="sxs-lookup"><span data-stu-id="f3f19-147">hello rest of hello initialization is placed inside hello promise response so that it is not executed until hello login() method completes.</span></span>

4. <span data-ttu-id="f3f19-148">Vervang in Hallo-code die u zojuist hebt toegevoegd, `SDK_Provider_Name` met Hallo-naam van uw aanmeldingsprovider.</span><span class="sxs-lookup"><span data-stu-id="f3f19-148">In hello code that you just added, replace `SDK_Provider_Name` with hello name of your login provider.</span></span> <span data-ttu-id="f3f19-149">Bijvoorbeeld: voor Azure Active Directory, gebruiken `client.login('aad')`.</span><span class="sxs-lookup"><span data-stu-id="f3f19-149">For example, for Azure Active Directory, use `client.login('aad')`.</span></span>
5. <span data-ttu-id="f3f19-150">Voer uw project.</span><span class="sxs-lookup"><span data-stu-id="f3f19-150">Run your project.</span></span>  <span data-ttu-id="f3f19-151">Wanneer het Hallo-project is geïnitialiseerd, ziet u uw toepassing hello OAuth-aanmeldingspagina voor Hallo verificatieprovider gekozen.</span><span class="sxs-lookup"><span data-stu-id="f3f19-151">When hello project has finished initializing, your application shows hello OAuth login page for hello chosen authentication provider.</span></span>

## <span data-ttu-id="f3f19-152"><a name="next-steps"></a>Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="f3f19-152"><a name="next-steps"></a>Next Steps</span></span>
* <span data-ttu-id="f3f19-153">Meer informatie [over verificatie] met Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="f3f19-153">Learn more [About Authentication] with Azure App Service.</span></span>
* <span data-ttu-id="f3f19-154">Hallo-zelfstudie gaan door toe te voegen [Pushmeldingen] tooyour Apache Cordova-app.</span><span class="sxs-lookup"><span data-stu-id="f3f19-154">Continue hello tutorial by adding [Push Notifications] tooyour Apache Cordova app.</span></span>

<span data-ttu-id="f3f19-155">Meer informatie over hoe toouse Hallo SDK's.</span><span class="sxs-lookup"><span data-stu-id="f3f19-155">Learn how toouse hello SDKs.</span></span>

* <span data-ttu-id="f3f19-156">[Apache Cordova SDK]</span><span class="sxs-lookup"><span data-stu-id="f3f19-156">[Apache Cordova SDK]</span></span>
* <span data-ttu-id="f3f19-157">[ASP.NET Server SDK]</span><span class="sxs-lookup"><span data-stu-id="f3f19-157">[ASP.NET Server SDK]</span></span>
* <span data-ttu-id="f3f19-158">[Node.js Server SDK]</span><span class="sxs-lookup"><span data-stu-id="f3f19-158">[Node.js Server SDK]</span></span>

<!-- URLs. -->
[aan de slag met Mobile Apps]: app-service-mobile-cordova-get-started.md
[inhoud beveiligingsbeleid documentatie]: https://cordova.apache.org/docs/en/latest/guide/appdev/whitelist/index.html
[Pushmeldingen]: app-service-mobile-cordova-get-started-push.md
[over verificatie]: app-service-mobile-auth.md
[Apache Cordova SDK]: app-service-mobile-cordova-how-to-use-client-library.md
[ASP.NET Server SDK]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[Node.js Server SDK]: app-service-mobile-node-backend-how-to-use-server-sdk.md

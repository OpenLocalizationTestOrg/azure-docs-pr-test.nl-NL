---
title: aaaHow tooconfigure Microsoft-Account verificatie voor uw toepassing App Services
description: Meer informatie over hoe tooconfigure Microsoft-Account verificatie voor uw App Services-toepassing.
author: mattchenderson
services: app-service
documentationcenter: 
manager: syntaxc4
editor: 
ms.assetid: ffbc6064-edf6-474d-971c-695598fd08bf
ms.service: app-service
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 10/01/2016
ms.author: mahender
ms.openlocfilehash: d86d8dab26a189f4454082fc18e44e3fb6e0a01d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-your-app-service-application-toouse-microsoft-account-login"></a><span data-ttu-id="03244-103">Hoe tooconfigure uw App Service-toepassing toouse-aanmelding met Microsoft-Account</span><span class="sxs-lookup"><span data-stu-id="03244-103">How tooconfigure your App Service application toouse Microsoft Account login</span></span>
[!INCLUDE [app-service-mobile-selector-authentication](../../includes/app-service-mobile-selector-authentication.md)]

<span data-ttu-id="03244-104">Dit onderwerp leest u hoe tooconfigure Azure App Service toouse Microsoft-Account als een verificatieprovider.</span><span class="sxs-lookup"><span data-stu-id="03244-104">This topic shows you how tooconfigure Azure App Service toouse Microsoft Account as an authentication provider.</span></span> 

## <span data-ttu-id="03244-105"><a name="register-microsoft-account"></a>Uw app registreren bij Microsoft-Account</span><span class="sxs-lookup"><span data-stu-id="03244-105"><a name="register-microsoft-account"> </a>Register your app with Microsoft Account</span></span>
1. <span data-ttu-id="03244-106">Meld u aan toohello [Azure-portal], en ga tooyour toepassing.</span><span class="sxs-lookup"><span data-stu-id="03244-106">Log on toohello [Azure portal], and navigate tooyour application.</span></span> <span data-ttu-id="03244-107">Kopieer uw **URL**, die u later gebruiken tooconfigure uw app met Microsoft-Account.</span><span class="sxs-lookup"><span data-stu-id="03244-107">Copy your **URL**, which later you use tooconfigure your app with Microsoft Account.</span></span>
2. <span data-ttu-id="03244-108">Navigeer toohello [mijn toepassingen] pagina in de Microsoft-Account Developer Center Hallo en meld u aan met uw Microsoft-account, indien nodig.</span><span class="sxs-lookup"><span data-stu-id="03244-108">Navigate toohello [My Applications] page in hello Microsoft Account Developer Center, and log on with your Microsoft account, if required.</span></span>
3. <span data-ttu-id="03244-109">Klik op **een app toevoegen**vervolgens typt u de naam van een toepassing en klik op **-toepassing maken**.</span><span class="sxs-lookup"><span data-stu-id="03244-109">Click **Add an app**, then type an application name, and click **Create application**.</span></span>
4. <span data-ttu-id="03244-110">Maak een notitie van Hallo **toepassings-ID**, zoals u deze later hebt.</span><span class="sxs-lookup"><span data-stu-id="03244-110">Make a note of hello **Application ID**, as you will need it later.</span></span> 
5. <span data-ttu-id="03244-111">Klik onder 'Platforms,' op **toevoegen Platform** en selecteert u 'Web'.</span><span class="sxs-lookup"><span data-stu-id="03244-111">Under "Platforms," click **Add Platform** and select "Web".</span></span>
6. <span data-ttu-id="03244-112">Klik onder 'Omleidings-URI' levering Hallo eindpunt voor uw toepassing, **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="03244-112">Under "Redirect URIs" supply hello endpoint for your application, then click **Save**.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="03244-113">De omleidings-URI Hallo-URL van uw toepassing toegevoegd aan de Hallo pad is, */.auth/login/microsoftaccount/callback*.</span><span class="sxs-lookup"><span data-stu-id="03244-113">Your redirect URI is hello URL of your application appended with hello path, */.auth/login/microsoftaccount/callback*.</span></span> <span data-ttu-id="03244-114">Bijvoorbeeld `https://contoso.azurewebsites.net/.auth/login/microsoftaccount/callback`.</span><span class="sxs-lookup"><span data-stu-id="03244-114">For example, `https://contoso.azurewebsites.net/.auth/login/microsoftaccount/callback`.</span></span>   
   > <span data-ttu-id="03244-115">Zorg ervoor dat u van Hallo HTTPS-schema gebruikmaakt.</span><span class="sxs-lookup"><span data-stu-id="03244-115">Make sure that you are using hello HTTPS scheme.</span></span>
   
7. <span data-ttu-id="03244-116">Klik onder 'Toepassing geheimen,' op **nieuw wachtwoord genereren**.</span><span class="sxs-lookup"><span data-stu-id="03244-116">Under "Application Secrets," click **Generate New Password**.</span></span> <span data-ttu-id="03244-117">Noteer Hallo-waarde die wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="03244-117">Make note of hello value that appears.</span></span> <span data-ttu-id="03244-118">Zodra u Hallo pagina verlaat, wordt deze niet opnieuw worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="03244-118">Once you leave hello page, it will not be displayed again.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="03244-119">Hallo-wachtwoord is een belangrijke beveiligingsreferentie.</span><span class="sxs-lookup"><span data-stu-id="03244-119">hello password is an important security credential.</span></span> <span data-ttu-id="03244-120">Hallo-wachtwoord met anderen delen of deze te distribueren vanuit een clienttoepassing niet.</span><span class="sxs-lookup"><span data-stu-id="03244-120">Do not share hello password with anyone or distribute it within a client application.</span></span>

## <span data-ttu-id="03244-121"><a name="secrets"></a>Microsoft-Account toevoegen informatie tooyour App Service-toepassing</span><span class="sxs-lookup"><span data-stu-id="03244-121"><a name="secrets"> </a>Add Microsoft Account information tooyour App Service application</span></span>
1. <span data-ttu-id="03244-122">Terug in Hallo [Azure-portal], tooyour toepassing navigeren, klik op **instellingen** > **verificatie / autorisatie**.</span><span class="sxs-lookup"><span data-stu-id="03244-122">Back in hello [Azure portal], navigate tooyour application, click **Settings** > **Authentication / Authorization**.</span></span>
2. <span data-ttu-id="03244-123">Als Hallo verificatie / autorisatie-functie is niet ingeschakeld, schakel deze **op**.</span><span class="sxs-lookup"><span data-stu-id="03244-123">If hello Authentication / Authorization feature is not enabled, switch it **On**.</span></span>
3. <span data-ttu-id="03244-124">Klik op **Microsoft-Account**.</span><span class="sxs-lookup"><span data-stu-id="03244-124">Click **Microsoft Account**.</span></span> <span data-ttu-id="03244-125">Plak in Hallo toepassings-ID en wachtwoord waarden die u eerder hebt verkregen en optioneel in staat alle scopes die vereist zijn voor uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="03244-125">Paste in hello Application ID and Password values which you obtained previously, and optionally enable any scopes your application requires.</span></span> <span data-ttu-id="03244-126">Klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="03244-126">Then click **OK**.</span></span>
   
    ![][1]
   
    <span data-ttu-id="03244-127">Standaard-App Service biedt verificatie maar niet beperkt geautoriseerde toegang tooyour site-inhoud en API's.</span><span class="sxs-lookup"><span data-stu-id="03244-127">By default, App Service provides authentication but does not restrict authorized access tooyour site content and APIs.</span></span> <span data-ttu-id="03244-128">U moet gebruikers machtigen in uw app-code.</span><span class="sxs-lookup"><span data-stu-id="03244-128">You must authorize users in your app code.</span></span>
4. <span data-ttu-id="03244-129">(Optioneel) toorestrict toegang tooyour site tooonly gebruikers zijn geverifieerd door de Microsoft-account ingesteld **tootake actie wanneer de aanvraag is niet geverifieerd** te**Microsoft-Account**.</span><span class="sxs-lookup"><span data-stu-id="03244-129">(Optional) toorestrict access tooyour site tooonly users authenticated by Microsoft account, set **Action tootake when request is not authenticated** too**Microsoft Account**.</span></span> <span data-ttu-id="03244-130">Dit is vereist dat alle aanvragen worden geverifieerd en alle niet-geverifieerde aanvragen worden omgeleid tooMicrosoft-account voor verificatie.</span><span class="sxs-lookup"><span data-stu-id="03244-130">This requires that all requests be authenticated, and all unauthenticated requests are redirected tooMicrosoft account for authentication.</span></span>
5. <span data-ttu-id="03244-131">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="03244-131">Click **Save**.</span></span>

<span data-ttu-id="03244-132">U bent nu klaar toouse Microsoft-Account voor verificatie in uw app.</span><span class="sxs-lookup"><span data-stu-id="03244-132">You are now ready toouse Microsoft Account for authentication in your app.</span></span>

## <span data-ttu-id="03244-133"><a name="related-content"></a>Verwante inhoud</span><span class="sxs-lookup"><span data-stu-id="03244-133"><a name="related-content"> </a>Related content</span></span>
[!INCLUDE [app-service-mobile-related-content-get-started-users](../../includes/app-service-mobile-related-content-get-started-users.md)]

<!-- Images. -->

[0]: ./media/app-service-mobile-how-to-configure-microsoft-authentication/app-service-microsoftaccount-redirect.png
[1]: ./media/app-service-mobile-how-to-configure-microsoft-authentication/mobile-app-microsoftaccount-settings.png

<!-- URLs. -->

[mijn toepassingen]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[Azure-portal]: https://portal.azure.com/

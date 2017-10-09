---
title: aaaSending Secure Pushmeldingen met Azure Notification Hubs
description: Meer informatie over hoe toosend beveiligde push-meldingen tooan Android-app van Azure. Codevoorbeelden geschreven in Java en C#.
documentationcenter: android
keywords: push-melding, pushmeldingen, push-berichten, android pushmeldingen
author: ysxu
manager: erikre
editor: 
services: notification-hubs
ms.assetid: daf3de1c-f6a9-43c4-8165-a76bfaa70893
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: android
ms.devlang: java
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: d07943c4691ed07acb987086228ef565e6281d57
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="sending-secure-push-notifications-with-azure-notification-hubs"></a><span data-ttu-id="07b00-105">Beveiligde Pushmeldingen verzenden met Azure Notification Hubs</span><span class="sxs-lookup"><span data-stu-id="07b00-105">Sending Secure Push Notifications with Azure Notification Hubs</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="07b00-106">Windows Universal</span><span class="sxs-lookup"><span data-stu-id="07b00-106">Windows Universal</span></span>](notification-hubs-aspnet-backend-windows-dotnet-wns-secure-push-notification.md)
> * [<span data-ttu-id="07b00-107">iOS</span><span class="sxs-lookup"><span data-stu-id="07b00-107">iOS</span></span>](notification-hubs-aspnet-backend-ios-push-apple-apns-secure-notification.md)
> * [<span data-ttu-id="07b00-108">Android</span><span class="sxs-lookup"><span data-stu-id="07b00-108">Android</span></span>](notification-hubs-aspnet-backend-android-secure-google-gcm-push-notification.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="07b00-109">Overzicht</span><span class="sxs-lookup"><span data-stu-id="07b00-109">Overview</span></span>
> [!IMPORTANT]
> <span data-ttu-id="07b00-110">toocomplete deze zelfstudie maakt u een actief Azure-account moet hebben.</span><span class="sxs-lookup"><span data-stu-id="07b00-110">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="07b00-111">Als u geen account hebt, kunt u binnen een paar minuten een account voor de gratis proefversie maken.</span><span class="sxs-lookup"><span data-stu-id="07b00-111">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="07b00-112">Zie [Gratis proefversie van Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fpartner-xamarin-notification-hubs-ios-get-started) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="07b00-112">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fpartner-xamarin-notification-hubs-ios-get-started).</span></span>
> 
> 

<span data-ttu-id="07b00-113">Push notification-ondersteuning in Microsoft Azure kunt u tooaccess een push eenvoudig te gebruiken, meerdere platforms, uitgebreid bericht-infrastructuur, die sterk vereenvoudigd Hallo-implementatie van pushmeldingen voor consumenten- en enterprise-toepassingen voor mobiele platforms.</span><span class="sxs-lookup"><span data-stu-id="07b00-113">Push notification support in Microsoft Azure enables you tooaccess an easy-to-use, multiplatform, scaled-out push message infrastructure, which greatly simplifies hello implementation of push notifications for both consumer and enterprise applications for mobile platforms.</span></span>

<span data-ttu-id="07b00-114">Vanwege beperkingen voor tooregulatory of beveiliging kunt soms een toepassing tooinclude iets in Hallo-bericht dat via Hallo standaard push notification-infrastructuur kan niet worden verzonden.</span><span class="sxs-lookup"><span data-stu-id="07b00-114">Due tooregulatory or security constraints, sometimes an application might want tooinclude something in hello notification that cannot be transmitted through hello standard push notification infrastructure.</span></span> <span data-ttu-id="07b00-115">Deze zelfstudie wordt beschreven hoe tooachieve dezelfde ervaring Hallo door te sturen van gevoelige gegevens via een veilige en geverifieerde verbinding tussen Hallo client Android-apparaat en back-end Hallo app.</span><span class="sxs-lookup"><span data-stu-id="07b00-115">This tutorial describes how tooachieve hello same experience by sending sensitive information through a secure, authenticated connection between hello client Android device and hello app backend.</span></span>

<span data-ttu-id="07b00-116">Op een hoog niveau is Hallo-stroom als volgt uit:</span><span class="sxs-lookup"><span data-stu-id="07b00-116">At a high level, hello flow is as follows:</span></span>

1. <span data-ttu-id="07b00-117">Hallo back-end van app:</span><span class="sxs-lookup"><span data-stu-id="07b00-117">hello app back-end:</span></span>
   * <span data-ttu-id="07b00-118">Winkels beveiligde nettolading in back-enddatabase.</span><span class="sxs-lookup"><span data-stu-id="07b00-118">Stores secure payload in back-end database.</span></span>
   * <span data-ttu-id="07b00-119">Hallo-ID van deze melding toohello Android-apparaat (geen beveiligde gegevens verzonden) verzendt.</span><span class="sxs-lookup"><span data-stu-id="07b00-119">Sends hello ID of this notification toohello Android device (no secure information is sent).</span></span>
2. <span data-ttu-id="07b00-120">Hallo-app op Hallo apparaat tijdens het Hallo-bericht ontvangen:</span><span class="sxs-lookup"><span data-stu-id="07b00-120">hello app on hello device, when receiving hello notification:</span></span>
   * <span data-ttu-id="07b00-121">Hallo Android-apparaat neemt contact op Hallo back-end aanvragende Hallo beveiligde nettolading.</span><span class="sxs-lookup"><span data-stu-id="07b00-121">hello Android device contacts hello back-end requesting hello secure payload.</span></span>
   * <span data-ttu-id="07b00-122">Hallo-app kunt Hallo nettolading weergeven als een melding op Hallo-apparaat.</span><span class="sxs-lookup"><span data-stu-id="07b00-122">hello app can show hello payload as a notification on hello device.</span></span>

<span data-ttu-id="07b00-123">Het is belangrijk dat in de voorgaande stroom Hallo (en in deze zelfstudie), gaan we ervan uit dat apparaat Hallo toonote slaat geen verificatietoken in lokale opslag nadat Hallo gebruiker zich aanmeldt.</span><span class="sxs-lookup"><span data-stu-id="07b00-123">It is important toonote that in hello preceding flow (and in this tutorial), we assume that hello device stores an authentication token in local storage, after hello user logs in.</span></span> <span data-ttu-id="07b00-124">Dit garandeert een volledig naadloze ervaring als apparaat Hallo Hallo melding van beveiligde nettolading met dit token kan ophalen.</span><span class="sxs-lookup"><span data-stu-id="07b00-124">This guarantees a completely seamless experience, as hello device can retrieve hello notification’s secure payload using this token.</span></span> <span data-ttu-id="07b00-125">Als uw toepassing slaat geen verificatietokens op Hallo-apparaat, of als deze tokens kunnen verlopen, moet een algemene melding vragen Hallo gebruiker toolaunch Hallo app Hallo apparaat app bij ontvangst van Hallo push-melding worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="07b00-125">If your application does not store authentication tokens on hello device, or if these tokens can be expired, hello device app, upon receiving hello push notification should display a generic notification prompting hello user toolaunch hello app.</span></span> <span data-ttu-id="07b00-126">Hallo-app vervolgens verifieert de gebruiker Hallo en toont de nettolading van de Hallo-meldingen.</span><span class="sxs-lookup"><span data-stu-id="07b00-126">hello app then authenticates hello user and shows hello notification payload.</span></span>

<span data-ttu-id="07b00-127">Deze zelfstudie laat zien hoe toosend beveiligde pushmeldingen.</span><span class="sxs-lookup"><span data-stu-id="07b00-127">This tutorial shows how toosend secure push notifications.</span></span> <span data-ttu-id="07b00-128">Dit is gebaseerd op Hallo [gebruikers waarschuwen](notification-hubs-aspnet-backend-gcm-android-push-to-user-google-notification.md) zelfstudie, dus u eerst te Hallo stappen in deze zelfstudie voltooien moet als u dat nog niet gedaan hebt.</span><span class="sxs-lookup"><span data-stu-id="07b00-128">It builds on hello [Notify Users](notification-hubs-aspnet-backend-gcm-android-push-to-user-google-notification.md) tutorial, so you should complete hello steps in that tutorial first if you haven't already.</span></span>

> [!NOTE]
> <span data-ttu-id="07b00-129">Deze zelfstudie wordt ervan uitgegaan dat u hebt gemaakt en uw notification hub geconfigureerd zoals beschreven in [aan de slag met Notification Hubs (Android)](notification-hubs-android-push-notification-google-gcm-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="07b00-129">This tutorial assumes that you have created and configured your notification hub as described in [Getting Started with Notification Hubs (Android)](notification-hubs-android-push-notification-google-gcm-get-started.md).</span></span>
> 
> 

[!INCLUDE [notification-hubs-aspnet-backend-securepush](../../includes/notification-hubs-aspnet-backend-securepush.md)]

## <a name="modify-hello-android-project"></a><span data-ttu-id="07b00-130">Hallo Android-project wijzigen</span><span class="sxs-lookup"><span data-stu-id="07b00-130">Modify hello Android project</span></span>
<span data-ttu-id="07b00-131">Nu dat u uw app back-end toosend alleen Hallo gewijzigd *id* van een push-melding hebt toochange uw Android-app toohandle melding en terugbellen secure uw back-end tooretrieve Hallo bericht toobe weergegeven.</span><span class="sxs-lookup"><span data-stu-id="07b00-131">Now that you modified your app back-end toosend just hello *id* of a push notification, you have toochange your Android app toohandle that notification and call back your back-end tooretrieve hello secure message toobe displayed.</span></span>
<span data-ttu-id="07b00-132">tooachieve deze doelstelling moeten er toomake ervoor dat uw Android-app weet hoe tooauthenticate zelf met uw back-end wanneer het Hallo-pushmeldingen ontvangt.</span><span class="sxs-lookup"><span data-stu-id="07b00-132">tooachieve this goal, you have toomake sure that your Android app knows how tooauthenticate itself with your back-end when it receives hello push notifications.</span></span>

<span data-ttu-id="07b00-133">Er wordt nu Hallo wijzigen *aanmelding* stroom in volgorde toosave Hallo verificatie headerwaarde in Hallo gedeelde voorkeuren van uw app.</span><span class="sxs-lookup"><span data-stu-id="07b00-133">We will now modify hello *login* flow in order toosave hello authentication header value in hello shared preferences of your app.</span></span> <span data-ttu-id="07b00-134">Vergelijkbaar mechanismen kunnen worden gebruikt toostore een verificatietoken (bijvoorbeeld OAuth tokens) voor die app Hallo toouse zonder gebruikersreferenties hebben.</span><span class="sxs-lookup"><span data-stu-id="07b00-134">Analogous mechanisms can be used toostore any authentication token (e.g. OAuth tokens) that hello app will have toouse without requiring user credentials.</span></span>

1. <span data-ttu-id="07b00-135">In uw Android-app-project toevoegen na constanten bovenaan Hallo HALLO hallo **MainActivity** klasse:</span><span class="sxs-lookup"><span data-stu-id="07b00-135">In your Android app project, add hello following constants at hello top of hello **MainActivity** class:</span></span>
   
        public static final String NOTIFY_USERS_PROPERTIES = "NotifyUsersProperties";
        public static final String AUTHORIZATION_HEADER_PROPERTY = "AuthorizationHeader";
2. <span data-ttu-id="07b00-136">Nog steeds in Hallo **MainActivity** klasse, update Hallo `getAuthorizationHeader()` methode toocontain Hallo code te volgen:</span><span class="sxs-lookup"><span data-stu-id="07b00-136">Still in hello **MainActivity** class, update hello `getAuthorizationHeader()` method toocontain hello following code:</span></span>
   
        private String getAuthorizationHeader() throws UnsupportedEncodingException {
            EditText username = (EditText) findViewById(R.id.usernameText);
            EditText password = (EditText) findViewById(R.id.passwordText);
            String basicAuthHeader = username.getText().toString()+":"+password.getText().toString();
            basicAuthHeader = Base64.encodeToString(basicAuthHeader.getBytes("UTF-8"), Base64.NO_WRAP);
   
            SharedPreferences sp = getSharedPreferences(NOTIFY_USERS_PROPERTIES, Context.MODE_PRIVATE);
            sp.edit().putString(AUTHORIZATION_HEADER_PROPERTY, basicAuthHeader).commit();
   
            return basicAuthHeader;
        }
3. <span data-ttu-id="07b00-137">Voeg de volgende Hallo `import` instructies boven Hallo Hallo **MainActivity** bestand:</span><span class="sxs-lookup"><span data-stu-id="07b00-137">Add hello following `import` statements at hello top of hello **MainActivity** file:</span></span>
   
        import android.content.SharedPreferences;

<span data-ttu-id="07b00-138">Nu wijzigen we Hallo-handler die wordt aangeroepen wanneer het Hallo-melding is ontvangen.</span><span class="sxs-lookup"><span data-stu-id="07b00-138">Now we will change hello handler that is called when hello notification is received.</span></span>

1. <span data-ttu-id="07b00-139">In Hallo **MyHandler** klasse wijzigen Hallo `OnReceive()` methode toocontain:</span><span class="sxs-lookup"><span data-stu-id="07b00-139">In hello **MyHandler** class change hello `OnReceive()` method toocontain:</span></span>
   
        public void onReceive(Context context, Bundle bundle) {
            ctx = context;
            String secureMessageId = bundle.getString("secureId");
            retrieveNotification(secureMessageId);
        }
2. <span data-ttu-id="07b00-140">Voeg vervolgens Hallo `retrieveNotification()` methode Hallo tijdelijke aanduiding vervangt `{back-end endpoint}` met Hallo backend-eindpunt is verkregen tijdens de implementatie van uw back-end:</span><span class="sxs-lookup"><span data-stu-id="07b00-140">Then add hello `retrieveNotification()` method, replacing hello placeholder `{back-end endpoint}` with hello back-end endpoint obtained while deploying your back-end:</span></span>
   
        private void retrieveNotification(final String secureMessageId) {
            SharedPreferences sp = ctx.getSharedPreferences(MainActivity.NOTIFY_USERS_PROPERTIES, Context.MODE_PRIVATE);
            final String authorizationHeader = sp.getString(MainActivity.AUTHORIZATION_HEADER_PROPERTY, null);
   
            new AsyncTask<Object, Object, Object>() {
                @Override
                protected Object doInBackground(Object... params) {
                    try {
                        HttpUriRequest request = new HttpGet("{back-end endpoint}/api/notifications/"+secureMessageId);
                        request.addHeader("Authorization", "Basic "+authorizationHeader);
                        HttpResponse response = new DefaultHttpClient().execute(request);
                        if (response.getStatusLine().getStatusCode() != HttpStatus.SC_OK) {
                            Log.e("MainActivity", "Error retrieving secure notification" + response.getStatusLine().getStatusCode());
                            throw new RuntimeException("Error retrieving secure notification");
                        }
                        String secureNotificationJSON = EntityUtils.toString(response.getEntity());
                        JSONObject secureNotification = new JSONObject(secureNotificationJSON);
                        sendNotification(secureNotification.getString("Payload"));
                    } catch (Exception e) {
                        Log.e("MainActivity", "Failed tooretrieve secure notification - " + e.getMessage());
                        return e;
                    }
                    return null;
                }
            }.execute(null, null, null);
        }

<span data-ttu-id="07b00-141">Deze methode roept uw back-end tooretrieve hello appmelding inhoud met behulp van Hallo referenties opgeslagen in Hallo gedeelde voorkeuren en geeft deze weer als een normale melding.</span><span class="sxs-lookup"><span data-stu-id="07b00-141">This method calls your app back-end tooretrieve hello notification content using hello credentials stored in hello shared preferences and displays it as a normal notification.</span></span> <span data-ttu-id="07b00-142">Hallo-melding ziet er toohello app gebruiker net als andere push-melding.</span><span class="sxs-lookup"><span data-stu-id="07b00-142">hello notification looks toohello app user exactly like any other push notification.</span></span>

<span data-ttu-id="07b00-143">Houd er rekening mee dat het is beter toohandle Hallo gevallen van eigenschap van de header ontbreekt verificatie of afwijzing door Hallo back-end.</span><span class="sxs-lookup"><span data-stu-id="07b00-143">Note that it is preferable toohandle hello cases of missing authentication header property or rejection by hello back-end.</span></span> <span data-ttu-id="07b00-144">Hallo specifieke verwerking van deze gevallen afhankelijk zijn van voornamelijk op de doel-gebruikerservaring.</span><span class="sxs-lookup"><span data-stu-id="07b00-144">hello specific handling of these cases depend mostly on your target user experience.</span></span> <span data-ttu-id="07b00-145">Een mogelijkheid is toodisplay een melding met een algemene Hallo tooauthenticate tooretrieve Hallo werkelijke gebruikersmelding wordt gevraagd.</span><span class="sxs-lookup"><span data-stu-id="07b00-145">One option is toodisplay a notification with a generic prompt for hello user tooauthenticate tooretrieve hello actual notification.</span></span>

## <a name="run-hello-application"></a><span data-ttu-id="07b00-146">Hallo toepassing uitvoeren</span><span class="sxs-lookup"><span data-stu-id="07b00-146">Run hello Application</span></span>
<span data-ttu-id="07b00-147">toorun toepassing hello, Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="07b00-147">toorun hello application, do hello following:</span></span>

1. <span data-ttu-id="07b00-148">Zorg ervoor dat **AppBackend** is geïmplementeerd in Azure.</span><span class="sxs-lookup"><span data-stu-id="07b00-148">Make sure **AppBackend** is deployed in Azure.</span></span> <span data-ttu-id="07b00-149">Als Visual Studio, voert u Hallo **AppBackend** Web API-toepassing.</span><span class="sxs-lookup"><span data-stu-id="07b00-149">If using Visual Studio, run hello **AppBackend** Web API application.</span></span> <span data-ttu-id="07b00-150">Een ASP.NET-webpagina wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="07b00-150">An ASP.NET web page is displayed.</span></span>
2. <span data-ttu-id="07b00-151">Voer in Eclipse Hallo-app op een fysieke Android-apparaat of Hallo-emulator.</span><span class="sxs-lookup"><span data-stu-id="07b00-151">In Eclipse, run hello app on a physical Android device or hello emulator.</span></span>
3. <span data-ttu-id="07b00-152">Voer een gebruikersnaam en wachtwoord in Hallo Android-app gebruikersinterface.</span><span class="sxs-lookup"><span data-stu-id="07b00-152">In hello Android app UI, enter a username and password.</span></span> <span data-ttu-id="07b00-153">Deze kunnen zich een willekeurige tekenreeks, maar ze moet dezelfde waarde Hallo.</span><span class="sxs-lookup"><span data-stu-id="07b00-153">These can be any string, but they must be hello same value.</span></span>
4. <span data-ttu-id="07b00-154">Klik in Hallo Android-app UI **aanmelden**.</span><span class="sxs-lookup"><span data-stu-id="07b00-154">In hello Android app UI, click **Log in**.</span></span> <span data-ttu-id="07b00-155">Klik vervolgens op **push verzenden**.</span><span class="sxs-lookup"><span data-stu-id="07b00-155">Then click **Send push**.</span></span>


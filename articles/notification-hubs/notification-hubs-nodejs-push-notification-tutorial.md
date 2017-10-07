---
title: aaaSending pushmeldingen kunt verzenden met Azure Notification Hubs en Node.js
description: Meer informatie over hoe toouse Notification Hubs toosend pushmeldingen vanuit een Node.js-toepassing.
keywords: push-bericht, push notifications,node.js push, ios push
services: notification-hubs
documentationcenter: nodejs
author: ysxu
manager: erikre
editor: 
ms.assetid: ded4749c-6c39-4ff8-b2cf-1927b3e92f93
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: article
ms.date: 10/25/2016
ms.author: yuaxu
ms.openlocfilehash: 151d224fa6dd07e4acdc3a4887c4e95ee03168c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="sending-push-notifications-with-azure-notification-hubs-and-nodejs"></a><span data-ttu-id="577b3-104">Pushmeldingen verzenden met Azure Notification Hubs en Node.js</span><span class="sxs-lookup"><span data-stu-id="577b3-104">Sending push notifications with Azure Notification Hubs and Node.js</span></span>
[!INCLUDE [notification-hubs-backend-how-to-selector](../../includes/notification-hubs-backend-how-to-selector.md)]

## <a name="overview"></a><span data-ttu-id="577b3-105">Overzicht</span><span class="sxs-lookup"><span data-stu-id="577b3-105">Overview</span></span>
> [!IMPORTANT]
> <span data-ttu-id="577b3-106">toocomplete deze zelfstudie maakt u een actief Azure-account moet hebben.</span><span class="sxs-lookup"><span data-stu-id="577b3-106">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="577b3-107">Als u geen account hebt, kunt u binnen een paar minuten een account voor de gratis proefversie maken.</span><span class="sxs-lookup"><span data-stu-id="577b3-107">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="577b3-108">Zie [Gratis proefversie van Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-nodejs-how-to-use-notification-hubs) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="577b3-108">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-nodejs-how-to-use-notification-hubs).</span></span>
> 
> 

<span data-ttu-id="577b3-109">Deze handleiding leert u hoe toosend pushmeldingen met Hallo help van Azure Notification Hubs rechtstreeks vanuit een Node.js-toepassing.</span><span class="sxs-lookup"><span data-stu-id="577b3-109">This guide will show you how toosend push notifications with hello help of Azure Notification Hubs directly from a Node.js application.</span></span> 

<span data-ttu-id="577b3-110">Hallo scenario's worden behandeld zijn push notifications tooapplications verzenden op Hallo volgende platforms:</span><span class="sxs-lookup"><span data-stu-id="577b3-110">hello scenarios covered include sending push notifications tooapplications on hello following platforms:</span></span>

* <span data-ttu-id="577b3-111">Android</span><span class="sxs-lookup"><span data-stu-id="577b3-111">Android</span></span>
* <span data-ttu-id="577b3-112">iOS</span><span class="sxs-lookup"><span data-stu-id="577b3-112">iOS</span></span>
* <span data-ttu-id="577b3-113">Windows Phone</span><span class="sxs-lookup"><span data-stu-id="577b3-113">Windows Phone</span></span>
* <span data-ttu-id="577b3-114">Universele Windows-Platform</span><span class="sxs-lookup"><span data-stu-id="577b3-114">Universal Windows Platform</span></span> 

<span data-ttu-id="577b3-115">Zie voor meer informatie over notification hubs Hallo [Vervolgstappen](#next) sectie.</span><span class="sxs-lookup"><span data-stu-id="577b3-115">For more information on notification hubs, see hello [Next Steps](#next) section.</span></span>

## <a name="what-are-notification-hubs"></a><span data-ttu-id="577b3-116">Wat is Notification Hubs?</span><span class="sxs-lookup"><span data-stu-id="577b3-116">What are Notification Hubs?</span></span>
<span data-ttu-id="577b3-117">Azure Notification Hubs bieden een eenvoudig te gebruiken, meerdere platforms, schaalbare infrastructuur voor het verzenden van pushmeldingen meldingen toomobile apparaten.</span><span class="sxs-lookup"><span data-stu-id="577b3-117">Azure Notification Hubs provide an easy-to-use, multi-platform, scalable infrastructure for sending push notifications toomobile devices.</span></span> <span data-ttu-id="577b3-118">Zie voor informatie over service-infrastructuur hello, Hallo [Azure Notification Hubs](http://msdn.microsoft.com/library/windowsazure/jj927170.aspx) pagina.</span><span class="sxs-lookup"><span data-stu-id="577b3-118">For details on hello service infrastructure, see hello [Azure Notification Hubs](http://msdn.microsoft.com/library/windowsazure/jj927170.aspx) page.</span></span>

## <a name="create-a-nodejs-application"></a><span data-ttu-id="577b3-119">Een Node.js-toepassing maken</span><span class="sxs-lookup"><span data-stu-id="577b3-119">Create a Node.js Application</span></span>
<span data-ttu-id="577b3-120">Hallo eerste stap in deze zelfstudie is een nieuwe lege Node.js-toepassing maken.</span><span class="sxs-lookup"><span data-stu-id="577b3-120">hello first step in this tutorial is creating a new blank Node.js application.</span></span> <span data-ttu-id="577b3-121">Zie voor instructies over het maken van een Node.js-toepassing [maken en implementeren van een Node.js-toepassing tooAzure website][nodejswebsite], [Node.js-Cloudservice] [ Node.js Cloud Service] met Windows PowerShell of [website met WebMatrix].</span><span class="sxs-lookup"><span data-stu-id="577b3-121">For instructions on creating a Node.js application, see [Create and deploy a Node.js application tooAzure Web Site][nodejswebsite], [Node.js Cloud Service][Node.js Cloud Service] using Windows PowerShell, or [Web Site with WebMatrix].</span></span>

## <a name="configure-your-application-toouse-notification-hubs"></a><span data-ttu-id="577b3-122">Configureren van uw toepassing tooUse Notification Hubs</span><span class="sxs-lookup"><span data-stu-id="577b3-122">Configure Your Application tooUse Notification Hubs</span></span>
<span data-ttu-id="577b3-123">Azure Notification Hubs toouse, moet u toodownload en gebruik Hallo Node.js [azure-pakket](https://www.npmjs.com/package/azure), waaronder een ingebouwde verzameling helper-bibliotheken die met Hallo push notification REST-services communiceren.</span><span class="sxs-lookup"><span data-stu-id="577b3-123">toouse Azure Notification Hubs, you need toodownload and use hello Node.js [azure package](https://www.npmjs.com/package/azure), which includes a built-in set of helper libraries that communicate with hello push notification REST services.</span></span>

### <a name="use-node-package-manager-npm-tooobtain-hello-package"></a><span data-ttu-id="577b3-124">Knooppunt Package Manager (NPM) tooobtain Hallo pakket gebruiken</span><span class="sxs-lookup"><span data-stu-id="577b3-124">Use Node Package Manager (NPM) tooobtain hello package</span></span>
1. <span data-ttu-id="577b3-125">Een opdrachtregelinterface gebruiken zoals **PowerShell** (Windows), **Terminal** (Mac) of **Bash** (Linux) en navigeer toohello map waar u uw lege toepassing hebt gemaakt. .</span><span class="sxs-lookup"><span data-stu-id="577b3-125">Use a command-line interface such as **PowerShell** (Windows), **Terminal** (Mac), or **Bash** (Linux) and navigate toohello folder where you created your blank application.</span></span>
2. <span data-ttu-id="577b3-126">Type **npm installeren azure sb** in Hallo-opdrachtvenster.</span><span class="sxs-lookup"><span data-stu-id="577b3-126">Type **npm install azure-sb** in hello command window.</span></span>
3. <span data-ttu-id="577b3-127">U kunt handmatig uitvoeren Hallo **ls** of **dir** tooverify opdracht die een **knooppunt\_modules** map is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="577b3-127">You can manually run hello **ls** or **dir** command tooverify that a **node\_modules** folder was created.</span></span> <span data-ttu-id="577b3-128">Hallo zoeken in die map **azure** , dit pakket bevat Hallo bibliotheken, moet u tooaccess Hallo Notification Hub.</span><span class="sxs-lookup"><span data-stu-id="577b3-128">Inside that folder, find hello **azure** package, which contains hello libraries you need tooaccess hello Notification Hub.</span></span>

> [!NOTE]
> <span data-ttu-id="577b3-129">U kunt meer informatie over het installeren van NPM op Hallo officiële [NPM blog](http://blog.npmjs.org/post/85484771375/how-to-install-npm).</span><span class="sxs-lookup"><span data-stu-id="577b3-129">You can learn more about installing NPM on hello official [NPM blog](http://blog.npmjs.org/post/85484771375/how-to-install-npm).</span></span> 
> 
> 

### <a name="import-hello-module"></a><span data-ttu-id="577b3-130">Hallo-module importeren</span><span class="sxs-lookup"><span data-stu-id="577b3-130">Import hello module</span></span>
<span data-ttu-id="577b3-131">Met een teksteditor toevoegen na toohello bovenaan Hallo Hallo **server.js** bestand van de toepassing hello:</span><span class="sxs-lookup"><span data-stu-id="577b3-131">Using a text editor, add hello following toohello top of hello **server.js** file of hello application:</span></span>

    var azure = require('azure');

### <a name="setup-an-azure-notification-hub-connection"></a><span data-ttu-id="577b3-132">Een Azure Notification Hub-verbinding instellen</span><span class="sxs-lookup"><span data-stu-id="577b3-132">Setup an Azure Notification Hub connection</span></span>
<span data-ttu-id="577b3-133">Hallo **NotificationHubService** object kunt u samenwerken met notification hubs.</span><span class="sxs-lookup"><span data-stu-id="577b3-133">hello **NotificationHubService** object lets you work with notification hubs.</span></span> <span data-ttu-id="577b3-134">Hallo volgende code maakt een **NotificationHubService** -object voor Hallo nofication hub met de naam **hubname**.</span><span class="sxs-lookup"><span data-stu-id="577b3-134">hello following code creates a **NotificationHubService** object for hello nofication hub named **hubname**.</span></span> <span data-ttu-id="577b3-135">Voeg deze toe aan de bovenkant Hallo Hallo **server.js** bestand na Hallo instructie tooimport hello azure module:</span><span class="sxs-lookup"><span data-stu-id="577b3-135">Add it near hello top of hello **server.js** file, after hello statement tooimport hello azure module:</span></span>

    var notificationHubService = azure.createNotificationHubService('hubname','connectionstring');

<span data-ttu-id="577b3-136">Hallo verbinding **connectionstring** waarde kan worden verkregen van Hallo [Azure Portal] door Hallo volgende stappen uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="577b3-136">hello connection **connectionstring** value can be obtained from hello [Azure Portal] by performing hello following steps:</span></span>

1. <span data-ttu-id="577b3-137">Klik in het Hallo navigatiedeelvenster links op **Bladeren**.</span><span class="sxs-lookup"><span data-stu-id="577b3-137">In hello left navigation pane, click **Browse**.</span></span>
2. <span data-ttu-id="577b3-138">Selecteer **Notification Hubs**, en vervolgens zoeken Hallo-hub gewenste toouse voor Hallo-voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="577b3-138">Select **Notification Hubs**, and then find hello hub you wish toouse for hello sample.</span></span> <span data-ttu-id="577b3-139">U kunt verwijzen toohello [Windows Store aan de slag zelfstudie](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) als u informatie over het maken van een nieuwe Notification Hub nodig.</span><span class="sxs-lookup"><span data-stu-id="577b3-139">You can refer toohello [Windows Store Getting Started tutorial](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) if you need help creating a new Notification Hub.</span></span>
3. <span data-ttu-id="577b3-140">Selecteer **instellingen**.</span><span class="sxs-lookup"><span data-stu-id="577b3-140">Select **Settings**.</span></span>
4. <span data-ttu-id="577b3-141">Klik op **toegangsbeleid**.</span><span class="sxs-lookup"><span data-stu-id="577b3-141">Click on **Access Policies**.</span></span> <span data-ttu-id="577b3-142">Hier ziet u beide verbindingsreeksen gedeelde en volledige toegang.</span><span class="sxs-lookup"><span data-stu-id="577b3-142">You will see both shared and full access connection strings.</span></span>

![Azure Portal - Notification Hubs](./media/notification-hubs-nodejs-how-to-use-notification-hubs/notification-hubs-portal.png)

> [!NOTE]
> <span data-ttu-id="577b3-144">U kunt ook ophalen verbindingsreeks Hallo Hallo met **Get-AzureSbNamespace** cmdlet geleverd door [Azure PowerShell](/powershell/azureps-cmdlets-docs) of Hallo **azure sb naamruimte weergeven** opdracht met Hallo [Azure-opdrachtregelinterface (Azure CLI)](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="577b3-144">You can also retrieve hello connection string using hello **Get-AzureSbNamespace** cmdlet provided by [Azure PowerShell](/powershell/azureps-cmdlets-docs) or hello **azure sb namespace show** command with hello [Azure Command-Line Interface (Azure CLI)](../cli-install-nodejs.md).</span></span>
> 
> 

## <a name="general-architecture"></a><span data-ttu-id="577b3-145">Algemene architectuur</span><span class="sxs-lookup"><span data-stu-id="577b3-145">General architecture</span></span>
<span data-ttu-id="577b3-146">Hallo **NotificationHubService** object beschrijft Hallo instanties van objecten voor het verzenden van pushmeldingen meldingen toospecific apparaten en toepassingen te volgen:</span><span class="sxs-lookup"><span data-stu-id="577b3-146">hello **NotificationHubService** object exposes hello following object instances for sending push notifications toospecific devices and applications:</span></span>

* <span data-ttu-id="577b3-147">**Android** -hello gebruiken **GcmService** object, dat beschikbaar is op **notificationHubService.gcm**</span><span class="sxs-lookup"><span data-stu-id="577b3-147">**Android** - use hello **GcmService** object, which is available at **notificationHubService.gcm**</span></span>
* <span data-ttu-id="577b3-148">**iOS** -hello gebruiken **ApnsService** -object, dat openen op **notificationHubService.apns**</span><span class="sxs-lookup"><span data-stu-id="577b3-148">**iOS** - use hello **ApnsService** object, which is accessible at **notificationHubService.apns**</span></span>
* <span data-ttu-id="577b3-149">**Windows Phone** -hello gebruiken **MpnsService** object, dat beschikbaar is op **notificationHubService.mpns**</span><span class="sxs-lookup"><span data-stu-id="577b3-149">**Windows Phone** - use hello **MpnsService** object, which is available at **notificationHubService.mpns**</span></span>
* <span data-ttu-id="577b3-150">**Universele Windows-Platform** -hello gebruiken **WnsService** object, dat beschikbaar is op **notificationHubService.wns**</span><span class="sxs-lookup"><span data-stu-id="577b3-150">**Universal Windows Platform** - use hello **WnsService** object, which is available at **notificationHubService.wns**</span></span>

### <a name="how-to-send-push-notifications-tooandroid-applications"></a><span data-ttu-id="577b3-151">Hoe: push notifications tooAndroid toepassingen verzenden</span><span class="sxs-lookup"><span data-stu-id="577b3-151">How to: Send push notifications tooAndroid applications</span></span>
<span data-ttu-id="577b3-152">Hallo **GcmService** -object biedt een **verzenden** methode die gebruikt toosend push notifications tooAndroid toepassingen worden kan.</span><span class="sxs-lookup"><span data-stu-id="577b3-152">hello **GcmService** object provides a **send** method that can be used toosend push notifications tooAndroid applications.</span></span> <span data-ttu-id="577b3-153">Hallo **verzenden** methode Hallo volgende parameters accepteert:</span><span class="sxs-lookup"><span data-stu-id="577b3-153">hello **send** method accepts hello following parameters:</span></span>

* <span data-ttu-id="577b3-154">**Labels** -Hallo label-id.</span><span class="sxs-lookup"><span data-stu-id="577b3-154">**Tags** - hello tag identifier.</span></span> <span data-ttu-id="577b3-155">Als er is geen code is opgegeven, wordt Hallo-bericht verzonden tooall clients.</span><span class="sxs-lookup"><span data-stu-id="577b3-155">If no tag is provided, hello notification will be sent tooall clients.</span></span>
* <span data-ttu-id="577b3-156">**Nettolading** -Hallo van bericht JSON of raw string nettolading.</span><span class="sxs-lookup"><span data-stu-id="577b3-156">**Payload** - hello message's JSON or raw string payload.</span></span>
* <span data-ttu-id="577b3-157">**Callback** -Hallo callback-functie.</span><span class="sxs-lookup"><span data-stu-id="577b3-157">**Callback** - hello callback function.</span></span>

<span data-ttu-id="577b3-158">Zie voor meer informatie over de indeling van nettolading hello, Hallo **nettolading** sectie Hallo [GCM Server implementeren](http://developer.android.com/google/gcm/server.html#payload) document.</span><span class="sxs-lookup"><span data-stu-id="577b3-158">For more information on hello payload format, see hello **Payload** section of hello [Implementing GCM Server](http://developer.android.com/google/gcm/server.html#payload) document.</span></span>

<span data-ttu-id="577b3-159">Hallo volgende code gebruikt Hallo **GcmService** exemplaar beschikbaar is gemaakt door Hallo **NotificationHubService** toosend een push notification-tooall ingeschreven clients.</span><span class="sxs-lookup"><span data-stu-id="577b3-159">hello following code uses hello **GcmService** instance exposed by hello **NotificationHubService** toosend a push notification tooall registered clients.</span></span>

    var payload = {
      data: {
        message: 'Hello!'
      }
    };
    notificationHubService.gcm.send(null, payload, function(error){
      if(!error){
        //notification sent
      }
    });

### <a name="how-to-send-push-notifications-tooios-applications"></a><span data-ttu-id="577b3-160">Hoe: push notifications tooiOS toepassingen verzenden</span><span class="sxs-lookup"><span data-stu-id="577b3-160">How to: Send push notifications tooiOS applications</span></span>
<span data-ttu-id="577b3-161">Dezelfde net als bij Android-toepassingen hierboven beschreven, Hallo **ApnsService** -object biedt een **verzenden** methode die gebruikt toosend push notifications tooiOS toepassingen worden kan.</span><span class="sxs-lookup"><span data-stu-id="577b3-161">Same as with Android applications described above, hello **ApnsService** object provides a **send** method that can be used toosend push notifications tooiOS applications.</span></span> <span data-ttu-id="577b3-162">Hallo **verzenden** methode Hallo volgende parameters accepteert:</span><span class="sxs-lookup"><span data-stu-id="577b3-162">hello **send** method accepts hello following parameters:</span></span>

* <span data-ttu-id="577b3-163">**Labels** -Hallo label-id.</span><span class="sxs-lookup"><span data-stu-id="577b3-163">**Tags** - hello tag identifier.</span></span> <span data-ttu-id="577b3-164">Als er is geen code is opgegeven, wordt Hallo-bericht verzonden tooall clients.</span><span class="sxs-lookup"><span data-stu-id="577b3-164">If no tag is provided, hello notification will be sent tooall clients.</span></span>
* <span data-ttu-id="577b3-165">**Nettolading** - Hallo van bericht JSON of string nettolading.</span><span class="sxs-lookup"><span data-stu-id="577b3-165">**Payload** - hello message's JSON or string payload.</span></span>
* <span data-ttu-id="577b3-166">**Callback** -Hallo callback-functie.</span><span class="sxs-lookup"><span data-stu-id="577b3-166">**Callback** - hello callback function.</span></span>

<span data-ttu-id="577b3-167">Zie voor meer informatie Hallo nettolading indeling Hallo **nettolading van de meldingen** sectie Hallo [Local and Push Notification Programming Guide](http://developer.apple.com/library/ios/#documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/ApplePushService/ApplePushService.html) document.</span><span class="sxs-lookup"><span data-stu-id="577b3-167">For more information hello payload format, see hello **Notification Payload** section of hello [Local and Push Notification Programming Guide](http://developer.apple.com/library/ios/#documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/ApplePushService/ApplePushService.html) document.</span></span>

<span data-ttu-id="577b3-168">Hallo volgende code gebruikt Hallo **ApnsService** exemplaar beschikbaar is gemaakt door Hallo **NotificationHubService** toosend een waarschuwing bericht tooall clients:</span><span class="sxs-lookup"><span data-stu-id="577b3-168">hello following code uses hello **ApnsService** instance exposed by hello **NotificationHubService** toosend an alert message tooall clients:</span></span>

    var payload={
        alert: 'Hello!'
      };
    notificationHubService.apns.send(null, payload, function(error){
      if(!error){
         // notification sent
      }
    });

### <a name="how-to-send-push-notifications-toowindows-phone-applications"></a><span data-ttu-id="577b3-169">Hoe: verzenden push notifications tooWindows Phone-toepassingen</span><span class="sxs-lookup"><span data-stu-id="577b3-169">How to: Send push notifications tooWindows Phone applications</span></span>
<span data-ttu-id="577b3-170">Hallo **MpnsService** -object biedt een **verzenden** methode die gebruikt toosend push notifications tooWindows Phone-toepassingen worden kan.</span><span class="sxs-lookup"><span data-stu-id="577b3-170">hello **MpnsService** object provides a **send** method that can be used toosend push notifications tooWindows Phone applications.</span></span> <span data-ttu-id="577b3-171">Hallo **verzenden** methode Hallo volgende parameters accepteert:</span><span class="sxs-lookup"><span data-stu-id="577b3-171">hello **send** method accepts hello following parameters:</span></span>

* <span data-ttu-id="577b3-172">**Labels** -Hallo label-id.</span><span class="sxs-lookup"><span data-stu-id="577b3-172">**Tags** - hello tag identifier.</span></span> <span data-ttu-id="577b3-173">Als er is geen code is opgegeven, wordt Hallo-bericht verzonden tooall clients.</span><span class="sxs-lookup"><span data-stu-id="577b3-173">If no tag is provided, hello notification will be sent tooall clients.</span></span>
* <span data-ttu-id="577b3-174">**Nettolading** -Hallo-bericht van de XML-nettolading.</span><span class="sxs-lookup"><span data-stu-id="577b3-174">**Payload** - hello message's XML payload.</span></span>
* <span data-ttu-id="577b3-175">**Doelnaam**  -  `toast` voor pop-upmeldingen.</span><span class="sxs-lookup"><span data-stu-id="577b3-175">**TargetName** - `toast` for toast notifications.</span></span> <span data-ttu-id="577b3-176">`token`voor meldingen van de tegel.</span><span class="sxs-lookup"><span data-stu-id="577b3-176">`token` for tile notifications.</span></span>
* <span data-ttu-id="577b3-177">**NotificationClass** -Hallo prioriteit Hallo-melding.</span><span class="sxs-lookup"><span data-stu-id="577b3-177">**NotificationClass** - hello priority of hello notification.</span></span> <span data-ttu-id="577b3-178">Zie Hallo **elementen voor HTTP-Header** sectie Hallo [Pushmeldingen vanaf een server](http://msdn.microsoft.com/library/hh221551.aspx) document voor geldige waarden.</span><span class="sxs-lookup"><span data-stu-id="577b3-178">See hello **HTTP Header Elements** section of hello [Push notifications from a server](http://msdn.microsoft.com/library/hh221551.aspx) document for valid values.</span></span>
* <span data-ttu-id="577b3-179">**Opties** : optioneel aanvraagheaders.</span><span class="sxs-lookup"><span data-stu-id="577b3-179">**Options** - optional request headers.</span></span>
* <span data-ttu-id="577b3-180">**Callback** -Hallo callback-functie.</span><span class="sxs-lookup"><span data-stu-id="577b3-180">**Callback** - hello callback function.</span></span>

<span data-ttu-id="577b3-181">Voor een lijst met geldige **TargetName**, **NotificationClass** en opties voor header uitchecken Hallo [Pushmeldingen vanaf een server](http://msdn.microsoft.com/library/hh221551.aspx) pagina.</span><span class="sxs-lookup"><span data-stu-id="577b3-181">For a list of valid **TargetName**, **NotificationClass** and header options, check out hello [Push notifications from a server](http://msdn.microsoft.com/library/hh221551.aspx) page.</span></span>

<span data-ttu-id="577b3-182">Hallo volgende voorbeeldcode maakt gebruik van Hallo **MpnsService** exemplaar beschikbaar is gemaakt door Hallo **NotificationHubService** toosend een pop-upmelding:</span><span class="sxs-lookup"><span data-stu-id="577b3-182">hello following sample code uses hello **MpnsService** instance exposed by hello **NotificationHubService** toosend a toast push notification:</span></span>

    var payload = '<?xml version="1.0" encoding="utf-8"?><wp:Notification xmlns:wp="WPNotification"><wp:Toast><wp:Text1>string</wp:Text1><wp:Text2>string</wp:Text2></wp:Toast></wp:Notification>';
    notificationHubService.mpns.send(null, payload, 'toast', 22, function(error){
      if(!error){
        //notification sent
      }
    });

### <a name="how-to-send-push-notifications-toouniversal-windows-platform-uwp-applications"></a><span data-ttu-id="577b3-183">Hoe: verzenden push notifications tooUniversal Windows Platform (UWP)-toepassingen</span><span class="sxs-lookup"><span data-stu-id="577b3-183">How to: Send push notifications tooUniversal Windows Platform (UWP) applications</span></span>
<span data-ttu-id="577b3-184">Hallo **WnsService** -object biedt een **verzenden** methode die gebruikt toosend push notifications tooUniversal Windows-Platform-toepassingen worden kan.</span><span class="sxs-lookup"><span data-stu-id="577b3-184">hello **WnsService** object provides a **send** method that can be used toosend push notifications tooUniversal Windows Platform applications.</span></span>  <span data-ttu-id="577b3-185">Hallo **verzenden** methode Hallo volgende parameters accepteert:</span><span class="sxs-lookup"><span data-stu-id="577b3-185">hello **send** method accepts hello following parameters:</span></span>

* <span data-ttu-id="577b3-186">**Labels** -Hallo label-id.</span><span class="sxs-lookup"><span data-stu-id="577b3-186">**Tags** - hello tag identifier.</span></span> <span data-ttu-id="577b3-187">Als er is geen code is opgegeven, wordt Hallo-bericht verzonden tooall ingeschreven clients.</span><span class="sxs-lookup"><span data-stu-id="577b3-187">If no tag is provided, hello notification will be sent tooall registered clients.</span></span>
* <span data-ttu-id="577b3-188">**Nettolading** -bericht Hallo de XML-nettolading.</span><span class="sxs-lookup"><span data-stu-id="577b3-188">**Payload** - hello XML message payload.</span></span>
* <span data-ttu-id="577b3-189">**Type** -Hallo meldingstype.</span><span class="sxs-lookup"><span data-stu-id="577b3-189">**Type** - hello notification type.</span></span>
* <span data-ttu-id="577b3-190">**Opties** : optioneel aanvraagheaders.</span><span class="sxs-lookup"><span data-stu-id="577b3-190">**Options** - optional request headers.</span></span>
* <span data-ttu-id="577b3-191">**Callback** -Hallo callback-functie.</span><span class="sxs-lookup"><span data-stu-id="577b3-191">**Callback** - hello callback function.</span></span>

<span data-ttu-id="577b3-192">Zie voor een lijst van geldige typen en aanvraagheaders [Push notification service aanvraag- en reactieheaders](http://msdn.microsoft.com/library/windows/apps/hh465435.aspx).</span><span class="sxs-lookup"><span data-stu-id="577b3-192">For a list of valid types and request headers, see [Push notification service request and response headers](http://msdn.microsoft.com/library/windows/apps/hh465435.aspx).</span></span>

<span data-ttu-id="577b3-193">Hallo volgende code gebruikt Hallo **WnsService** exemplaar beschikbaar is gemaakt door Hallo **NotificationHubService** toosend een pop-up push notification tooa UWP-app:</span><span class="sxs-lookup"><span data-stu-id="577b3-193">hello following code uses hello **WnsService** instance exposed by hello **NotificationHubService** toosend a toast push notification tooa UWP app:</span></span>

    var payload = '<toast><visual><binding template="ToastText01"><text id="1">Hello!</text></binding></visual></toast>';
    notificationHubService.wns.send(null, payload , 'wns/toast', function(error){
      if(!error){
         // notification sent
      }
    });

## <a name="next-steps"></a><span data-ttu-id="577b3-194">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="577b3-194">Next Steps</span></span>
<span data-ttu-id="577b3-195">Hallo voorbeeld codefragmenten hierboven kunnen u tooeasily build service infrastructuur toodeliver push notifications tooa grote verscheidenheid aan apparaten.</span><span class="sxs-lookup"><span data-stu-id="577b3-195">hello sample snippets above allow you tooeasily build service infrastructure toodeliver push notifications tooa wide variety of devices.</span></span> <span data-ttu-id="577b3-196">Nu u de basisbeginselen van het gebruik van Notification Hubs met behulp van node.js Hallo hebt geleerd, volgt u deze koppelingen toolearn meer informatie over hoe deze mogelijkheden verder kan worden uitgebreid.</span><span class="sxs-lookup"><span data-stu-id="577b3-196">Now that you've learned hello basics of using Notification Hubs with node.js, follow these links toolearn more about how you can extend these capabilities further.</span></span>

* <span data-ttu-id="577b3-197">Zie MSDN-documentatie voor Hallo [Azure Notification Hubs](https://msdn.microsoft.com/library/azure/jj927170.aspx).</span><span class="sxs-lookup"><span data-stu-id="577b3-197">See hello MSDN Reference for [Azure Notification Hubs](https://msdn.microsoft.com/library/azure/jj927170.aspx).</span></span>
* <span data-ttu-id="577b3-198">Ga naar Hallo [Azure SDK voor knooppunt] opslagplaats op GitHub voor meer voorbeelden en implementatiegegevens.</span><span class="sxs-lookup"><span data-stu-id="577b3-198">Visit hello [Azure SDK for Node] repository on GitHub for more samples and implementation details.</span></span>

[Azure SDK voor knooppunt]: https://github.com/WindowsAzure/azure-sdk-for-node
[Next Steps]: #nextsteps
[What are Service Bus Topics and Subscriptions?]: #what-are-service-bus-topics
[Create a Service Namespace]: #create-a-service-namespace
[Obtain hello Default Management Credentials for hello Namespace]: #obtain-default-credentials
[Create a Node.js Application]: #Create_a_Nodejs_Application
[Configure Your Application tooUse Service Bus]: #Configure_Your_Application_to_Use_Service_Bus
[How to: Create a Topic]: #How_to_Create_a_Topic
[How to: Create Subscriptions]: #How_to_Create_Subscriptions
[How to: Send Messages tooa Topic]: #How_to_Send_Messages_to_a_Topic
[How to: Receive Messages from a Subscription]: #How_to_Receive_Messages_from_a_Subscription
[How to: Handle Application Crashes and Unreadable Messages]: #How_to_Handle_Application_Crashes_and_Unreadable_Messages
[How to: Delete Topics and Subscriptions]: #How_to_Delete_Topics_and_Subscriptions
[1]: #Next_Steps
[Topic Concepts]: .media/notification-hubs-nodejs-how-to-use-notification-hubs/sb-topics-01.png
[Azure Classic Portal]: http://manage.windowsazure.com
[image]: .media/notification-hubs-nodejs-how-to-use-notification-hubs/sb-queues-03.png
[2]: .media/notification-hubs-nodejs-how-to-use-notification-hubs/sb-queues-04.png
[3]: .media/notification-hubs-nodejs-how-to-use-notification-hubs/sb-queues-05.png
[4]: .media/notification-hubs-nodejs-how-to-use-notification-hubs/sb-queues-06.png
[5]: .media/notification-hubs-nodejs-how-to-use-notification-hubs/sb-queues-07.png
[SqlFilter.SqlExpression]: http://msdn.microsoft.com/library/windowsazure/microsoft.servicebus.messaging.sqlfilter.sqlexpression.aspx
[Azure Service Bus Notification Hubs]: http://msdn.microsoft.com/library/windowsazure/jj927170.aspx
[SqlFilter]: http://msdn.microsoft.com/library/windowsazure/microsoft.servicebus.messaging.sqlfilter.aspx
[website met WebMatrix]: /develop/nodejs/tutorials/web-site-with-webmatrix/
[Node.js Cloud Service]: ../cloud-services/cloud-services-nodejs-develop-deploy-app.md
[Previous Management Portal]: .media/notification-hubs-nodejs-how-to-use-notification-hubs/previous-portal.png
[nodejswebsite]: /develop/nodejs/tutorials/create-a-website-(mac)/
[Node.js Cloud Service with Storage]: /develop/nodejs/tutorials/web-app-with-storage/
[Node.js Web Application with Storage]: /develop/nodejs/tutorials/web-site-with-storage/
[Azure Portal]: https://portal.azure.com

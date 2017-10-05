---
title: Azure Functions Notification Hub-binding | Microsoft Docs
description: Het gebruik van Azure Notification Hub-binding in Azure Functions begrijpen.
services: functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
keywords: Azure functions, functies, verwerking van gebeurtenissen, dynamische compute zonder server architectuur
ms.assetid: 0ff0c949-20bf-430b-8dd5-d72b7b6ee6f7
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 10/27/2016
ms.author: glenga
ms.openlocfilehash: fa3d37b963c1bb6b58127b9180cd657d7b1dabcc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-functions-notification-hub-output-binding"></a><span data-ttu-id="148b5-104">Azure Functions Notification Hub uitvoer binding</span><span class="sxs-lookup"><span data-stu-id="148b5-104">Azure Functions Notification Hub output binding</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="148b5-105">Dit artikel wordt uitgelegd hoe u configureert en bindingen van Azure Notification Hub code in Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="148b5-105">This article explains how to configure and code Azure Notification Hub bindings in Azure Functions.</span></span> 

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<span data-ttu-id="148b5-106">Uw functies kunnen verzenden van pushmeldingen in via een geconfigureerde Azure Notification Hub met een paar regels code.</span><span class="sxs-lookup"><span data-stu-id="148b5-106">Your functions can send push notifications using a configured Azure Notification Hub with a few lines of code.</span></span> <span data-ttu-id="148b5-107">De Azure Notification Hub moet worden geconfigureerd voor het Platform meldingen Services (PNS) u wilt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="148b5-107">However, the Azure Notification Hub must be configured for the Platform Notifications Services (PNS) you want to use.</span></span> <span data-ttu-id="148b5-108">Zie voor meer informatie over het configureren van een Azure Notification Hub en ontwikkelen van een clienttoepassingen registreren om meldingen te ontvangen [aan de slag met Notification Hubs](../notification-hubs/notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) en klik op het doelplatform voor de client aan de bovenkant.</span><span class="sxs-lookup"><span data-stu-id="148b5-108">For more information on configuring an Azure Notification Hub and developing a client applications that register to receive notifications, see [Getting started with Notification Hubs](../notification-hubs/notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) and click your target client platform at the top.</span></span>

<span data-ttu-id="148b5-109">De meldingen die u verzendt zijn systeemeigen meldingen of Sjabloonmeldingen.</span><span class="sxs-lookup"><span data-stu-id="148b5-109">The notifications you send can be native notifications or template notifications.</span></span> <span data-ttu-id="148b5-110">Systeemeigen meldingen zoals geconfigureerd in een specifieke bericht-platform als doel de `platform` eigenschap van de uitvoer-binding.</span><span class="sxs-lookup"><span data-stu-id="148b5-110">Native notifications target a specific notification platform as configured in the `platform` property of the output binding.</span></span> <span data-ttu-id="148b5-111">Een melding van de sjabloon kan worden gebruikt voor meerdere platforms.</span><span class="sxs-lookup"><span data-stu-id="148b5-111">A template notification can be used to target multiple platforms.</span></span>   

## <a name="notification-hub-output-binding-properties"></a><span data-ttu-id="148b5-112">Notification hub uitvoer bindingeigenschappen</span><span class="sxs-lookup"><span data-stu-id="148b5-112">Notification hub output binding properties</span></span>
<span data-ttu-id="148b5-113">Het bestand function.json biedt de volgende eigenschappen:</span><span class="sxs-lookup"><span data-stu-id="148b5-113">The function.json file provides the following properties:</span></span>

* <span data-ttu-id="148b5-114">`name`: Variabelenaam in functiecode gebruikt voor de notification hub-bericht.</span><span class="sxs-lookup"><span data-stu-id="148b5-114">`name` : Variable name used in function code for the notification hub message.</span></span>
* <span data-ttu-id="148b5-115">`type`: moet worden ingesteld op *'notificationHub'*.</span><span class="sxs-lookup"><span data-stu-id="148b5-115">`type` : must be set to *"notificationHub"*.</span></span>
* <span data-ttu-id="148b5-116">`tagExpression`: Code-expressies kunnen u opgeven dat meldingen worden geleverd aan een verzameling apparaten die zich hebben geregistreerd voor het ontvangen van meldingen die overeenkomen met de code-expressie.</span><span class="sxs-lookup"><span data-stu-id="148b5-116">`tagExpression` : Tag expressions allow you to specify that notifications be delivered to a set of devices who have registered to receive notifications that match the tag expression.</span></span>  <span data-ttu-id="148b5-117">Zie voor meer informatie [Routering en code-expressies](../notification-hubs/notification-hubs-tags-segment-push-message.md).</span><span class="sxs-lookup"><span data-stu-id="148b5-117">For more information, see [Routing and tag expressions](../notification-hubs/notification-hubs-tags-segment-push-message.md).</span></span>
* <span data-ttu-id="148b5-118">`hubName`: De naam van de notification hub-resource in de Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="148b5-118">`hubName` : Name of the notification hub resource in the Azure portal.</span></span>
* <span data-ttu-id="148b5-119">`connection`: Deze verbindingsreeks moet een **toepassingsinstelling** verbindingsreeks ingesteld op de *DefaultFullSharedAccessSignature* waarde voor uw notification hub.</span><span class="sxs-lookup"><span data-stu-id="148b5-119">`connection` : This connection string must be an **Application Setting** connection string set to the *DefaultFullSharedAccessSignature* value for your notification hub.</span></span>
* <span data-ttu-id="148b5-120">`direction`: moet worden ingesteld op *'out'*.</span><span class="sxs-lookup"><span data-stu-id="148b5-120">`direction` : must be set to *"out"*.</span></span> 
* <span data-ttu-id="148b5-121">`platform`: De platform-eigenschap geeft het platform notification uw doelen melding.</span><span class="sxs-lookup"><span data-stu-id="148b5-121">`platform` : The platform property indicates the notification platform your notification targets.</span></span> <span data-ttu-id="148b5-122">Dit moet een van de volgende waarden zijn:</span><span class="sxs-lookup"><span data-stu-id="148b5-122">Must be one of the following values:</span></span>
  * <span data-ttu-id="148b5-123">Standaard, als de eigenschap platform wordt weggelaten uit de uitvoer-binding kunnen Sjabloonmeldingen worden gebruikt als doel in elk platform dat is geconfigureerd op de Azure Notification Hub.</span><span class="sxs-lookup"><span data-stu-id="148b5-123">By default, if the platform property is omitted from the output binding, template notifications can be used to target any platform configured on the Azure Notification Hub.</span></span> <span data-ttu-id="148b5-124">Zie voor meer informatie over het gebruik van sjablonen in het algemeen verzenden cross-platform meldingen met een Azure Notification Hub [sjablonen](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md).</span><span class="sxs-lookup"><span data-stu-id="148b5-124">For more information on using templates in general to send cross platform notifications with an Azure Notification Hub, see [Templates](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md).</span></span>
  * <span data-ttu-id="148b5-125">`apns`: De Apple Push Notification Service.</span><span class="sxs-lookup"><span data-stu-id="148b5-125">`apns` : Apple Push Notification Service.</span></span> <span data-ttu-id="148b5-126">Zie voor meer informatie over het configureren van de notification hub voor APNS en ontvangst van de melding in een client-app [pushmeldingen verzenden naar iOS met Azure Notification Hubs](../notification-hubs/notification-hubs-ios-apple-push-notification-apns-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="148b5-126">For more information on configuring the notification hub for APNS and receiving the notification in a client app, see [Sending push notifications to iOS with Azure Notification Hubs](../notification-hubs/notification-hubs-ios-apple-push-notification-apns-get-started.md)</span></span> 
  * <span data-ttu-id="148b5-127">`adm`: [Amazon Device Messaging](https://developer.amazon.com/device-messaging).</span><span class="sxs-lookup"><span data-stu-id="148b5-127">`adm` : [Amazon Device Messaging](https://developer.amazon.com/device-messaging).</span></span> <span data-ttu-id="148b5-128">Zie voor meer informatie over het configureren van de notification hub voor ADM en ontvangst van de melding in een Kindle-app [aan de slag met Notification Hubs voor Kindle-apps](../notification-hubs/notification-hubs-kindle-amazon-adm-push-notification.md)</span><span class="sxs-lookup"><span data-stu-id="148b5-128">For more information on configuring the notification hub for ADM and receiving the notification in a Kindle app, see [Getting Started with Notification Hubs for Kindle apps](../notification-hubs/notification-hubs-kindle-amazon-adm-push-notification.md)</span></span> 
  * <span data-ttu-id="148b5-129">`gcm`: [Google Cloud Messaging](https://developers.google.com/cloud-messaging/).</span><span class="sxs-lookup"><span data-stu-id="148b5-129">`gcm` : [Google Cloud Messaging](https://developers.google.com/cloud-messaging/).</span></span> <span data-ttu-id="148b5-130">Firebase Cloud Messaging, dat de nieuwe versie van GCM is, wordt ook ondersteund.</span><span class="sxs-lookup"><span data-stu-id="148b5-130">Firebase Cloud Messaging, which is the new version of GCM, is also supported.</span></span> <span data-ttu-id="148b5-131">Zie voor meer informatie over het configureren van de notification hub voor GCM/FCM en ontvangst van de melding in een Android-clientapp [pushmeldingen verzenden naar Android met Azure Notification Hubs](../notification-hubs/notification-hubs-android-push-notification-google-fcm-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="148b5-131">For more information on configuring the notification hub for GCM/FCM and receiving the notification in an Android client app, see [Sending push notifications to Android with Azure Notification Hubs](../notification-hubs/notification-hubs-android-push-notification-google-fcm-get-started.md)</span></span>
  * <span data-ttu-id="148b5-132">`wns`: [Windows Push Notification Services](https://msdn.microsoft.com/en-us/windows/uwp/controls-and-patterns/tiles-and-notifications-windows-push-notification-services--wns--overview) die gericht is op Windows-platforms.</span><span class="sxs-lookup"><span data-stu-id="148b5-132">`wns` : [Windows Push Notification Services](https://msdn.microsoft.com/en-us/windows/uwp/controls-and-patterns/tiles-and-notifications-windows-push-notification-services--wns--overview) targeting Windows platforms.</span></span> <span data-ttu-id="148b5-133">Windows Phone 8.1 en hoger wordt ook ondersteund door WNS.</span><span class="sxs-lookup"><span data-stu-id="148b5-133">Windows Phone 8.1 and later is also supported by WNS.</span></span> <span data-ttu-id="148b5-134">Zie voor meer informatie over het configureren van de notification hub voor WNS en ontvangst van de melding in een Universal Windows Platform (UWP)-app [aan de slag met Notification Hubs voor universele Windows-Platform-Apps](../notification-hubs/notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md)</span><span class="sxs-lookup"><span data-stu-id="148b5-134">For more information on configuring the notification hub for WNS and receiving the notification in a Universal Windows Platform (UWP) app, see [Getting started with Notification Hubs for Windows Universal Platform Apps](../notification-hubs/notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md)</span></span>
  * <span data-ttu-id="148b5-135">`mpns`: [Microsoft Push Notification Service](https://msdn.microsoft.com/en-us/library/windows/apps/ff402558.aspx).</span><span class="sxs-lookup"><span data-stu-id="148b5-135">`mpns` : [Microsoft Push Notification Service](https://msdn.microsoft.com/en-us/library/windows/apps/ff402558.aspx).</span></span> <span data-ttu-id="148b5-136">Dit platform biedt ondersteuning voor Windows Phone 8 en eerdere Windows Phone-platforms.</span><span class="sxs-lookup"><span data-stu-id="148b5-136">This platform supports Windows Phone 8 and earlier Windows Phone platforms.</span></span> <span data-ttu-id="148b5-137">Zie voor meer informatie over de notification hub configureren voor MPNS en ontvangst van de melding in een Windows Phone-app [pushmeldingen verzenden met Azure Notification Hubs op Windows Phone](../notification-hubs/notification-hubs-windows-mobile-push-notifications-mpns.md)</span><span class="sxs-lookup"><span data-stu-id="148b5-137">For more information on configuring the notification hub for MPNS and receiving the notification in a Windows Phone app, see [Sending push notifications with Azure Notification Hubs on Windows Phone](../notification-hubs/notification-hubs-windows-mobile-push-notifications-mpns.md)</span></span>

<span data-ttu-id="148b5-138">Voorbeeld function.json:</span><span class="sxs-lookup"><span data-stu-id="148b5-138">Example function.json:</span></span>

```json
{
  "bindings": [
    {
      "name": "notification",
      "type": "notificationHub",
      "tagExpression": "",
      "hubName": "my-notification-hub",
      "connection": "MyHubConnectionString",
      "platform": "gcm",
      "direction": "out"
    }
  ],
  "disabled": false
}
```

## <a name="notification-hub-connection-string-setup"></a><span data-ttu-id="148b5-139">Notification hub verbinding tekenreeks instellen</span><span class="sxs-lookup"><span data-stu-id="148b5-139">Notification hub connection string setup</span></span>
<span data-ttu-id="148b5-140">U moet de verbindingsreeks voor de hub configureren voor het gebruik van een Notification hub-uitvoer binding.</span><span class="sxs-lookup"><span data-stu-id="148b5-140">To use a Notification hub output binding, you must configure the connection string for the hub.</span></span> <span data-ttu-id="148b5-141">Dit kan worden gedaan op de *integreren* tabblad door de notification hub of u een nieuwe maakt.</span><span class="sxs-lookup"><span data-stu-id="148b5-141">This can be done on the *Integrate* tab by selecting your notification hub or creating a new one.</span></span> 

<span data-ttu-id="148b5-142">U kunt ook handmatig een verbindingsreeks voor een bestaande hub toevoegen door het toevoegen van een verbindingsreeks voor de *DefaultFullSharedAccessSignature* naar uw notification hub.</span><span class="sxs-lookup"><span data-stu-id="148b5-142">You can also manually add a connection string for an existing hub by adding a connection string for the *DefaultFullSharedAccessSignature* to your notification hub.</span></span> <span data-ttu-id="148b5-143">Deze verbindingsreeks bevat de functie toegang toestemming om meldingsberichten te verzenden.</span><span class="sxs-lookup"><span data-stu-id="148b5-143">This connection string provides your function access permission to send notification messages.</span></span> <span data-ttu-id="148b5-144">De *DefaultFullSharedAccessSignature* gegevensbronwaarde toegankelijk is vanaf de **sleutels** knop op de hoofdblade van uw notification hub-resource in de Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="148b5-144">The *DefaultFullSharedAccessSignature* connection string value can be accessed from the **keys** button in the main blade of your notification hub resource in the Azure portal.</span></span> <span data-ttu-id="148b5-145">Om handmatig een verbindingsreeks voor uw hub toevoegen, gebruikt u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="148b5-145">To manually add a connection string for your hub, use the following steps:</span></span> 

1. <span data-ttu-id="148b5-146">Op de **functie-app** blade van de Azure-portal klikt u op **functie App-instellingen > Ga naar App Service-instellingen**.</span><span class="sxs-lookup"><span data-stu-id="148b5-146">On the **Function app** blade of the Azure portal, click **Function App Settings > Go to App Service settings**.</span></span>
2. <span data-ttu-id="148b5-147">In de **instellingen** blade, klikt u op **toepassingsinstellingen**.</span><span class="sxs-lookup"><span data-stu-id="148b5-147">In the **Settings** blade, click **Application Settings**.</span></span>
3. <span data-ttu-id="148b5-148">Schuif omlaag naar de **appinstellingen** sectie en toevoegen van een benoemde vermelding voor *DefaultFullSharedAccessSignature* waarde voor uw notification hub.</span><span class="sxs-lookup"><span data-stu-id="148b5-148">Scroll down to the **App settings** section, and add a named entry for *DefaultFullSharedAccessSignature* value for your notification hub.</span></span>
4. <span data-ttu-id="148b5-149">Verwijzen naar uw App tekenreeks naam van de instelling in de uitvoer-bindingen.</span><span class="sxs-lookup"><span data-stu-id="148b5-149">Reference your App setting string name in the output bindings.</span></span> <span data-ttu-id="148b5-150">Net als bij **MyHubConnectionString** gebruikt in het bovenstaande voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="148b5-150">Similar to **MyHubConnectionString** used in the example above.</span></span>

## <a name="apns-native-notifications-with-c-queue-triggers"></a><span data-ttu-id="148b5-151">Systeemeigen meldingen APNS met C# queue-triggers</span><span class="sxs-lookup"><span data-stu-id="148b5-151">APNS native notifications with C# queue triggers</span></span>
<span data-ttu-id="148b5-152">Dit voorbeeld ziet u het gebruik van typen die zijn gedefinieerd de [bibliotheek van Microsoft Azure Notification Hubs](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) een systeemeigen APNS-melding te verzenden.</span><span class="sxs-lookup"><span data-stu-id="148b5-152">This example shows how to use types defined in the [Microsoft Azure Notification Hubs Library](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) to send a native APNS notification.</span></span> 

```cs
#r "Microsoft.Azure.NotificationHubs"
#r "Newtonsoft.Json"

using System;
using Microsoft.Azure.NotificationHubs;
using Newtonsoft.Json;

public static async Task Run(string myQueueItem, IAsyncCollector<Notification> notification, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");

    // In this example the queue item is a new user to be processed in the form of a JSON string with 
    // a "name" value.
    //
    // The JSON format for a native APNS notification is ...
    // { "aps": { "alert": "notification message" }}  

    log.Info($"Sending APNS notification of a new user");    
    dynamic user = JsonConvert.DeserializeObject(myQueueItem);    
    string apnsNotificationPayload = "{\"aps\": {\"alert\": \"A new user wants to be added (" + 
                                        user.name + ")\" }}";
    log.Info($"{apnsNotificationPayload}");
    await notification.AddAsync(new AppleNotification(apnsNotificationPayload));        
}
```

## <a name="gcm-native-notifications-with-c-queue-triggers"></a><span data-ttu-id="148b5-153">Systeemeigen GCM-meldingen met C# queue-triggers</span><span class="sxs-lookup"><span data-stu-id="148b5-153">GCM native notifications with C# queue triggers</span></span>
<span data-ttu-id="148b5-154">Dit voorbeeld ziet u het gebruik van typen die zijn gedefinieerd de [bibliotheek van Microsoft Azure Notification Hubs](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) een systeemeigen GCM-melding te verzenden.</span><span class="sxs-lookup"><span data-stu-id="148b5-154">This example shows how to use types defined in the [Microsoft Azure Notification Hubs Library](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) to send a native GCM notification.</span></span> 

```cs
#r "Microsoft.Azure.NotificationHubs"
#r "Newtonsoft.Json"

using System;
using Microsoft.Azure.NotificationHubs;
using Newtonsoft.Json;

public static async Task Run(string myQueueItem, IAsyncCollector<Notification> notification, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");

    // In this example the queue item is a new user to be processed in the form of a JSON string with 
    // a "name" value.
    //
    // The JSON format for a native GCM notification is ...
    // { "data": { "message": "notification message" }}  

    log.Info($"Sending GCM notification of a new user");    
    dynamic user = JsonConvert.DeserializeObject(myQueueItem);    
    string gcmNotificationPayload = "{\"data\": {\"message\": \"A new user wants to be added (" + 
                                        user.name + ")\" }}";
    log.Info($"{gcmNotificationPayload}");
    await notification.AddAsync(new GcmNotification(gcmNotificationPayload));        
}
```

## <a name="wns-native-notifications-with-c-queue-triggers"></a><span data-ttu-id="148b5-155">WNS systeemeigen meldingen met C# queue-triggers</span><span class="sxs-lookup"><span data-stu-id="148b5-155">WNS native notifications with C# queue triggers</span></span>
<span data-ttu-id="148b5-156">Dit voorbeeld ziet u het gebruik van typen die zijn gedefinieerd de [bibliotheek van Microsoft Azure Notification Hubs](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) een systeemeigen WNS toast-melding te verzenden.</span><span class="sxs-lookup"><span data-stu-id="148b5-156">This example shows how to use types defined in the [Microsoft Azure Notification Hubs Library](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) to send a native WNS toast notification.</span></span> 

```cs
#r "Microsoft.Azure.NotificationHubs"
#r "Newtonsoft.Json"

using System;
using Microsoft.Azure.NotificationHubs;
using Newtonsoft.Json;

public static async Task Run(string myQueueItem, IAsyncCollector<Notification> notification, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");

    // In this example the queue item is a new user to be processed in the form of a JSON string with 
    // a "name" value.
    //
    // The XML format for a native WNS toast notification is ...
    // <?xml version="1.0" encoding="utf-8"?>
    // <toast>
    //      <visual>
    //     <binding template="ToastText01">
    //       <text id="1">notification message</text>
    //     </binding>
    //   </visual>
    // </toast>

    log.Info($"Sending WNS toast notification of a new user");    
    dynamic user = JsonConvert.DeserializeObject(myQueueItem);    
    string wnsNotificationPayload = "<?xml version=\"1.0\" encoding=\"utf-8\"?>" +
                                    "<toast><visual><binding template=\"ToastText01\">" +
                                        "<text id=\"1\">" + 
                                            "A new user wants to be added (" + user.name + ")" + 
                                        "</text>" +
                                    "</binding></visual></toast>";

    log.Info($"{wnsNotificationPayload}");
    await notification.AddAsync(new WindowsNotification(wnsNotificationPayload));        
}
```

## <a name="template-example-for-nodejs-timer-triggers"></a><span data-ttu-id="148b5-157">Voorbeeld van de sjabloon voor Node.js timer triggers</span><span class="sxs-lookup"><span data-stu-id="148b5-157">Template example for Node.js timer triggers</span></span>
<span data-ttu-id="148b5-158">In dit voorbeeld wordt een melding verzonden op een [sjabloon registratie](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) die bevat `location` en `message`.</span><span class="sxs-lookup"><span data-stu-id="148b5-158">This example sends a notification for a [template registration](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) that contains `location` and `message`.</span></span>

```javascript
module.exports = function (context, myTimer) {
    var timeStamp = new Date().toISOString();

    if(myTimer.isPastDue)
    {
        context.log('Node.js is running late!');
    }
    context.log('Node.js timer trigger function ran!', timeStamp);  
    context.bindings.notification = {
        location: "Redmond",
        message: "Hello from Node!"
    };
    context.done();
};
```

## <a name="template-example-for-f-timer-triggers"></a><span data-ttu-id="148b5-159">Voorbeeld van de sjabloon voor F # timer triggers</span><span class="sxs-lookup"><span data-stu-id="148b5-159">Template example for F# timer triggers</span></span>
<span data-ttu-id="148b5-160">In dit voorbeeld wordt een melding verzonden op een [sjabloon registratie](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) die bevat `location` en `message`.</span><span class="sxs-lookup"><span data-stu-id="148b5-160">This example sends a notification for a [template registration](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) that contains `location` and `message`.</span></span>

```fsharp
let Run(myTimer: TimerInfo, notification: byref<IDictionary<string, string>>) =
    notification = dict [("location", "Redmond"); ("message", "Hello from F#!")]
```

## <a name="template-example-using-an-out-parameter"></a><span data-ttu-id="148b5-161">Voorbeeld van de sjabloon met een out-parameter</span><span class="sxs-lookup"><span data-stu-id="148b5-161">Template example using an out parameter</span></span>
<span data-ttu-id="148b5-162">In dit voorbeeld wordt een melding verzonden op een [sjabloon registratie](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) die bevat een `message` aanduiding in de sjabloon.</span><span class="sxs-lookup"><span data-stu-id="148b5-162">This example sends a notification for a [template registration](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) that contains a `message` place holder in the template.</span></span>

```cs
using System;
using System.Threading.Tasks;
using System.Collections.Generic;

public static void Run(string myQueueItem,  out IDictionary<string, string> notification, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");
    notification = GetTemplateProperties(myQueueItem);
}

private static IDictionary<string, string> GetTemplateProperties(string message)
{
    Dictionary<string, string> templateProperties = new Dictionary<string, string>();
    templateProperties["message"] = message;
    return templateProperties;
}
```

## <a name="template-example-with-asynchronous-function"></a><span data-ttu-id="148b5-163">Voorbeeld van een sjabloon met asynchrone functie</span><span class="sxs-lookup"><span data-stu-id="148b5-163">Template example with asynchronous function</span></span>
<span data-ttu-id="148b5-164">Als u van asynchrone code gebruikmaakt, zijn out-parameters niet toegestaan.</span><span class="sxs-lookup"><span data-stu-id="148b5-164">If you are using asynchronous code, out parameters are not allowed.</span></span> <span data-ttu-id="148b5-165">In dit geval gebruiken `IAsyncCollector` te retourneren van de melding van uw sjabloon.</span><span class="sxs-lookup"><span data-stu-id="148b5-165">In this case use `IAsyncCollector` to return your template notification.</span></span> <span data-ttu-id="148b5-166">De volgende code is een asynchrone voorbeeld van de bovenstaande code.</span><span class="sxs-lookup"><span data-stu-id="148b5-166">The following code is an asynchronous example of the code above.</span></span> 

```cs
using System;
using System.Threading.Tasks;
using System.Collections.Generic;

public static async Task Run(string myQueueItem, IAsyncCollector<IDictionary<string,string>> notification, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");

    log.Info($"Sending Template Notification to Notification Hub");
    await notification.AddAsync(GetTemplateProperties(myQueueItem));    
}

private static IDictionary<string, string> GetTemplateProperties(string message)
{
    Dictionary<string, string> templateProperties = new Dictionary<string, string>();
    templateProperties["user"] = "A new user wants to be added : " + message;
    return templateProperties;
}
```

## <a name="template-example-using-json"></a><span data-ttu-id="148b5-167">Voorbeeld van de sjabloon met een JSON</span><span class="sxs-lookup"><span data-stu-id="148b5-167">Template example using JSON</span></span>
<span data-ttu-id="148b5-168">In dit voorbeeld wordt een melding verzonden op een [sjabloon registratie](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) die bevat een `message` aanduiding in de sjabloon met een geldig JSON-tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="148b5-168">This example sends a notification for a [template registration](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) that contains a `message` place holder in the template using a valid JSON string.</span></span>

```cs
using System;

public static void Run(string myQueueItem,  out string notification, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");
    notification = "{\"message\":\"Hello from C#. Processed a queue item!\"}";
}
```

## <a name="template-example-using-notification-hubs-library-types"></a><span data-ttu-id="148b5-169">Voorbeeld van de sjabloon met Notification Hubs bibliotheek typen</span><span class="sxs-lookup"><span data-stu-id="148b5-169">Template example using Notification Hubs library types</span></span>
<span data-ttu-id="148b5-170">Dit voorbeeld ziet u het gebruik van typen die zijn gedefinieerd de [bibliotheek van Microsoft Azure Notification Hubs](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span><span class="sxs-lookup"><span data-stu-id="148b5-170">This example shows how to use types defined in the [Microsoft Azure Notification Hubs Library](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span></span> 

```cs
#r "Microsoft.Azure.NotificationHubs"

using System;
using System.Threading.Tasks;
using Microsoft.Azure.NotificationHubs;

public static void Run(string myQueueItem,  out Notification notification, TraceWriter log)
{
   log.Info($"C# Queue trigger function processed: {myQueueItem}");
   notification = GetTemplateNotification(myQueueItem);
}

private static TemplateNotification GetTemplateNotification(string message)
{
    Dictionary<string, string> templateProperties = new Dictionary<string, string>();
    templateProperties["message"] = message;
    return new TemplateNotification(templateProperties);
}
```

## <a name="next-steps"></a><span data-ttu-id="148b5-171">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="148b5-171">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]


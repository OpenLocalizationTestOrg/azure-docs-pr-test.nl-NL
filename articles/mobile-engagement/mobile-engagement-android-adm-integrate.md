---
title: Azure Mobile Engagement Android SDK-integratie
description: Meest recente updates en -procedures voor Android-SDK voor Azure Mobile Engagement
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: a7d719ec-67b3-4be3-9d7f-0b61a57fe978
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 43987962ea2b7b825b88643d18b4db65f1f1670e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-integrate-adm-with-engagement"></a><span data-ttu-id="7fca3-103">Het integreren van ADM met Engagement</span><span class="sxs-lookup"><span data-stu-id="7fca3-103">How to Integrate ADM with Engagement</span></span>
> [!IMPORTANT]
> <span data-ttu-id="7fca3-104">U moet de integratie procedure beschreven in de manier waarop integreren engagement voor Android-document voordat u deze handleiding volgen.</span><span class="sxs-lookup"><span data-stu-id="7fca3-104">You must follow the integration procedure described in the How to Integrate Engagement on Android document before following this guide.</span></span>
> 
> <span data-ttu-id="7fca3-105">Dit document is alleen nuttig als u al is geïntegreerd de Reach-module en plannen voor de push-Amazon-apparaten.</span><span class="sxs-lookup"><span data-stu-id="7fca3-105">This document is useful only if you already integrated the Reach module and plan to push Amazon devices.</span></span> <span data-ttu-id="7fca3-106">Als u wilt integreren in uw toepassing Reach-campagnes, lees eerst integreren Engagement bereiken op Android.</span><span class="sxs-lookup"><span data-stu-id="7fca3-106">To integrate Reach campaigns in your application, please read first How to Integrate Engagement Reach on Android.</span></span>
> 
> 

## <a name="introduction"></a><span data-ttu-id="7fca3-107">Inleiding</span><span class="sxs-lookup"><span data-stu-id="7fca3-107">Introduction</span></span>
<span data-ttu-id="7fca3-108">Integratie van ADM kan uw toepassing worden geactiveerd wanneer de doelcomputer Amazon Android-apparaten.</span><span class="sxs-lookup"><span data-stu-id="7fca3-108">Integrating ADM allows your application to be pushed when targeting Amazon Android devices.</span></span>

<span data-ttu-id="7fca3-109">ADM-nettoladingen altijd naar de SDK gepusht bevatten de `azme` sleutel in het gegevensobject.</span><span class="sxs-lookup"><span data-stu-id="7fca3-109">ADM payloads pushed to the SDK always contain the `azme` key in the data object.</span></span> <span data-ttu-id="7fca3-110">Dus als u in uw toepassing ADM voor een ander doel gebruikt, kunt u filteren op basis van die sleutel pushes.</span><span class="sxs-lookup"><span data-stu-id="7fca3-110">Thus if you use ADM for another purpose in your application, you can filter pushes based on that key.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7fca3-111">Alleen Amazon Kindle apparaten met Android 4.0.3 of hoger worden ondersteund door de Amazon Device Messaging; u kunt echter deze code veilig op andere apparaten integreren.</span><span class="sxs-lookup"><span data-stu-id="7fca3-111">Only Amazon Kindle devices running Android 4.0.3 or above are supported by Amazon Device Messaging; however, you can integrate this code safely on other devices.</span></span>
> 
> 

## <a name="sign-up-to-adm"></a><span data-ttu-id="7fca3-112">Meld u aan ADM</span><span class="sxs-lookup"><span data-stu-id="7fca3-112">Sign up to ADM</span></span>
<span data-ttu-id="7fca3-113">Als u niet hebt gedaan, moet u de ADM inschakelen op de Amazon-account.</span><span class="sxs-lookup"><span data-stu-id="7fca3-113">If not already done, you must enable ADM on your Amazon account.</span></span>

<span data-ttu-id="7fca3-114">De procedure wordt beschreven op: [ <https://developer.amazon.com/sdk/adm/credentials.html>].</span><span class="sxs-lookup"><span data-stu-id="7fca3-114">The procedure is detailed at: [<https://developer.amazon.com/sdk/adm/credentials.html>].</span></span>

<span data-ttu-id="7fca3-115">U krijgt bij voltooiing van de procedure:</span><span class="sxs-lookup"><span data-stu-id="7fca3-115">Upon completing the procedure, you get:</span></span>

* <span data-ttu-id="7fca3-116">OAuth-referenties (een Client-ID en een Clientgeheim) voor Engagement kunnen uw apparaten te pushen.</span><span class="sxs-lookup"><span data-stu-id="7fca3-116">OAuth credentials (a Client ID and a Client Secret) for Engagement to be able to push your devices.</span></span>
* <span data-ttu-id="7fca3-117">Een API-sleutel die moet worden geïntegreerd in uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="7fca3-117">An API Key that must be integrated into your application.</span></span>

## <a name="sdk-integration"></a><span data-ttu-id="7fca3-118">SDK-integratie</span><span class="sxs-lookup"><span data-stu-id="7fca3-118">SDK integration</span></span>
### <a name="managing-device-registrations"></a><span data-ttu-id="7fca3-119">Het beheren van apparaat-registraties</span><span class="sxs-lookup"><span data-stu-id="7fca3-119">Managing device registrations</span></span>
<span data-ttu-id="7fca3-120">Elk apparaat een opdracht registratie moet verzenden naar de ADM-servers, anders ze kunnen niet worden bereikt.</span><span class="sxs-lookup"><span data-stu-id="7fca3-120">Each device must send a registration command to the ADM servers, otherwise they can't be reached.</span></span>

<span data-ttu-id="7fca3-121">Als u al gebruikt de [ADM-clientbibliotheek], en al [ADM geïntegreerd] rechtstreeks gaat u naar android-sdk-adm-ontvangen.</span><span class="sxs-lookup"><span data-stu-id="7fca3-121">If you already use the [ADM client library], and already have [integrated ADM] you can directly go to android-sdk-adm-receive.</span></span>

<span data-ttu-id="7fca3-122">Als u hebt geen ADM geïntegreerd, heeft Engagement een eenvoudigere manier om in te schakelen in uw toepassing:</span><span class="sxs-lookup"><span data-stu-id="7fca3-122">If you have not integrated ADM yet, Engagement has a simpler way to enable it in your application:</span></span>

<span data-ttu-id="7fca3-123">Bewerk uw `AndroidManifest.xml` bestand:</span><span class="sxs-lookup"><span data-stu-id="7fca3-123">Edit your `AndroidManifest.xml` file:</span></span>

* <span data-ttu-id="7fca3-124">Voeg de Amazon-naamruimte moet beginnen met het bestand als volgt:</span><span class="sxs-lookup"><span data-stu-id="7fca3-124">Add the Amazon namespace, the file should begin like this:</span></span>
  
      <?xml version="1.0" encoding="utf-8"?>
      <manifest xmlns:android="http://schemas.android.com/apk/res/android"
                xmlns:amazon="http://schemas.amazon.com/apk/res/android"
* <span data-ttu-id="7fca3-125">In de `<application/>` tag, het toevoegen van deze sectie:</span><span class="sxs-lookup"><span data-stu-id="7fca3-125">Inside the `<application/>` tag, add this section:</span></span>
  
      <amazon:enable-feature
         android:name="com.amazon.device.messaging"
         android:required="false"/>
  
      <meta-data android:name="engagement:adm:register" android:value="true" />
* <span data-ttu-id="7fca3-126">Na het toevoegen van de tag amazon mogelijk hebt u een opbouwfout als uw doel van de Projectbuild lager dan Android 2.1 is.</span><span class="sxs-lookup"><span data-stu-id="7fca3-126">After adding the amazon tag, you may have a build error if your Project Build Target is below Android 2.1.</span></span> <span data-ttu-id="7fca3-127">U moet gebruiken een **Android 2.1 +** doel bouwen (Maak je geen zorgen, kunt u nog steeds een `minSdkVersion` ingesteld op 4).</span><span class="sxs-lookup"><span data-stu-id="7fca3-127">You have to use an **Android 2.1+** build target (don't worry, you can still have a `minSdkVersion` set to 4).</span></span>
* <span data-ttu-id="7fca3-128">De ADM-API-sleutel integreren als een actief door [deze procedure].</span><span class="sxs-lookup"><span data-stu-id="7fca3-128">Integrate the ADM API Key as an asset by following [this procedure].</span></span>

<span data-ttu-id="7fca3-129">Volg de instructies van de volgende secties.</span><span class="sxs-lookup"><span data-stu-id="7fca3-129">Then follow the instructions of the next sections.</span></span>

### <a name="communicate-registration-id-to-the-engagement-push-service-and-receive-notifications"></a><span data-ttu-id="7fca3-130">Registratie-id voor de Engagement Push service communiceren en meldingen ontvangen</span><span class="sxs-lookup"><span data-stu-id="7fca3-130">Communicate registration id to the Engagement Push service and receive notifications</span></span>
<span data-ttu-id="7fca3-131">Om te communiceren de registratie-id van het apparaat naar de Engagement Push-service en de meldingen ontvangen, het volgende toevoegen aan uw `AndroidManifest.xml` bestand, binnen de `<application/>` tag (zelfs als u de ADM zonder Engagement gebruiken):</span><span class="sxs-lookup"><span data-stu-id="7fca3-131">In order to communicate the registration id of the device to the Engagement Push service and receive its notifications, add the following to your `AndroidManifest.xml` file, inside the `<application/>` tag (even if you use ADM without Engagement):</span></span>

        <receiver android:name="com.microsoft.azure.engagement.adm.EngagementADMEnabler"
          android:exported="false">
          <intent-filter>
            <action android:name="com.microsoft.azure.engagement.intent.action.APPID_GOT"/>
          </intent-filter>
        </receiver>

         <receiver android:name="com.microsoft.azure.engagement.adm.EngagementADMReceiver"
           android:permission="com.amazon.device.messaging.permission.SEND">
          <intent-filter>
            <action android:name="com.amazon.device.messaging.intent.REGISTRATION"/>
            <action android:name="com.amazon.device.messaging.intent.RECEIVE"/>
            <category android:name="<your_package_name>"/>
          </intent-filter>
        </receiver>   

<span data-ttu-id="7fca3-132">Zorg ervoor dat u hebt de volgende machtigingen uw `AndroidManifest.xml` (voordat de `</application>` label).</span><span class="sxs-lookup"><span data-stu-id="7fca3-132">Ensure you have the following permissions in your `AndroidManifest.xml` (before the `</application>` tag).</span></span>

        <uses-permission android:name="android.permission.WAKE_LOCK"/>
        <uses-permission android:name="com.amazon.device.messaging.permission.RECEIVE"/>
        <uses-permission android:name="<your_package_name>.permission.RECEIVE_ADM_MESSAGE"/>
        <permission android:name="<your_package_name>.permission.RECEIVE_ADM_MESSAGE" android:protectionLevel="signature"/>

## <a name="grant-engagement-oauth-credentials"></a><span data-ttu-id="7fca3-133">Verleen Engagement OAuth-referenties</span><span class="sxs-lookup"><span data-stu-id="7fca3-133">Grant Engagement OAuth credentials</span></span>
<span data-ttu-id="7fca3-134">Dien uw OAuth-referenties (Client-ID en Clientgeheim) in de Engagement-Portal.</span><span class="sxs-lookup"><span data-stu-id="7fca3-134">Submit your OAuth Credentials (Client ID and Client Secret) in Engagement Portal.</span></span>

<span data-ttu-id="7fca3-135">[< https://developer.amazon.com/sdk/adm/credentials.html>]:https://developer.amazon.com/sdk/adm/credentials.html</span><span class="sxs-lookup"><span data-stu-id="7fca3-135">[<https://developer.amazon.com/sdk/adm/credentials.html>]:https://developer.amazon.com/sdk/adm/credentials.html</span></span>
<span data-ttu-id="7fca3-136">[ADM-clientbibliotheek]:https://developer.amazon.com/sdk/adm/setup.html</span><span class="sxs-lookup"><span data-stu-id="7fca3-136">[ADM client library]:https://developer.amazon.com/sdk/adm/setup.html</span></span>
<span data-ttu-id="7fca3-137">[ADM geïntegreerd]:https://developer.amazon.com/sdk/adm/integrating-app.html</span><span class="sxs-lookup"><span data-stu-id="7fca3-137">[integrated ADM]:https://developer.amazon.com/sdk/adm/integrating-app.html</span></span>
<span data-ttu-id="7fca3-138">[deze procedure]:https://developer.amazon.com/sdk/adm/integrating-app.html#Asset</span><span class="sxs-lookup"><span data-stu-id="7fca3-138">[this procedure]:https://developer.amazon.com/sdk/adm/integrating-app.html#Asset</span></span>

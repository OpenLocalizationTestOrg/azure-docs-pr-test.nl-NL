---
title: aaaAzure Mobile Engagement Android SDK-integratie
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
ms.openlocfilehash: c57132ff49cf8c335627a72b37f9b78529e84f48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toointegrate-adm-with-engagement"></a><span data-ttu-id="8fdec-103">Hoe tooIntegrate ADM met Engagement</span><span class="sxs-lookup"><span data-stu-id="8fdec-103">How tooIntegrate ADM with Engagement</span></span>
> [!IMPORTANT]
> <span data-ttu-id="8fdec-104">U moet volgen Hallo integratie procedure wordt beschreven in Hallo hoe tooIntegrate Engagement op Android-document voordat u deze handleiding.</span><span class="sxs-lookup"><span data-stu-id="8fdec-104">You must follow hello integration procedure described in hello How tooIntegrate Engagement on Android document before following this guide.</span></span>
> 
> <span data-ttu-id="8fdec-105">Dit document is alleen nuttig als u al is geïntegreerd Hallo Reach-module en plan toopush Amazon-apparaten.</span><span class="sxs-lookup"><span data-stu-id="8fdec-105">This document is useful only if you already integrated hello Reach module and plan toopush Amazon devices.</span></span> <span data-ttu-id="8fdec-106">toointegrate Reach-campagnes in uw toepassing, lees eerst hoe tooIntegrate Engagement bereiken op Android.</span><span class="sxs-lookup"><span data-stu-id="8fdec-106">toointegrate Reach campaigns in your application, please read first How tooIntegrate Engagement Reach on Android.</span></span>
> 
> 

## <a name="introduction"></a><span data-ttu-id="8fdec-107">Inleiding</span><span class="sxs-lookup"><span data-stu-id="8fdec-107">Introduction</span></span>
<span data-ttu-id="8fdec-108">Integratie van ADM, kunt uw toepassing toobe gepusht wanneer de doelcomputer Amazon Android-apparaten.</span><span class="sxs-lookup"><span data-stu-id="8fdec-108">Integrating ADM allows your application toobe pushed when targeting Amazon Android devices.</span></span>

<span data-ttu-id="8fdec-109">ADM-nettoladingen toohello SDK altijd gepusht bevatten Hallo `azme` sleutel in het Hallo-gegevensobject.</span><span class="sxs-lookup"><span data-stu-id="8fdec-109">ADM payloads pushed toohello SDK always contain hello `azme` key in hello data object.</span></span> <span data-ttu-id="8fdec-110">Dus als u in uw toepassing ADM voor een ander doel gebruikt, kunt u filteren op basis van die sleutel pushes.</span><span class="sxs-lookup"><span data-stu-id="8fdec-110">Thus if you use ADM for another purpose in your application, you can filter pushes based on that key.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8fdec-111">Alleen Amazon Kindle apparaten met Android 4.0.3 of hoger worden ondersteund door de Amazon Device Messaging; u kunt echter deze code veilig op andere apparaten integreren.</span><span class="sxs-lookup"><span data-stu-id="8fdec-111">Only Amazon Kindle devices running Android 4.0.3 or above are supported by Amazon Device Messaging; however, you can integrate this code safely on other devices.</span></span>
> 
> 

## <a name="sign-up-tooadm"></a><span data-ttu-id="8fdec-112">TooADM aanmelden</span><span class="sxs-lookup"><span data-stu-id="8fdec-112">Sign up tooADM</span></span>
<span data-ttu-id="8fdec-113">Als u niet hebt gedaan, moet u de ADM inschakelen op de Amazon-account.</span><span class="sxs-lookup"><span data-stu-id="8fdec-113">If not already done, you must enable ADM on your Amazon account.</span></span>

<span data-ttu-id="8fdec-114">Hallo procedure wordt beschreven op: [ <https://developer.amazon.com/sdk/adm/credentials.html>].</span><span class="sxs-lookup"><span data-stu-id="8fdec-114">hello procedure is detailed at: [<https://developer.amazon.com/sdk/adm/credentials.html>].</span></span>

<span data-ttu-id="8fdec-115">U krijgt bij voltooiing van Hallo procedure:</span><span class="sxs-lookup"><span data-stu-id="8fdec-115">Upon completing hello procedure, you get:</span></span>

* <span data-ttu-id="8fdec-116">OAuth-referenties (een Client-ID en een Clientgeheim) voor Engagement toobe kunnen toopush uw apparaten.</span><span class="sxs-lookup"><span data-stu-id="8fdec-116">OAuth credentials (a Client ID and a Client Secret) for Engagement toobe able toopush your devices.</span></span>
* <span data-ttu-id="8fdec-117">Een API-sleutel die moet worden geïntegreerd in uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="8fdec-117">An API Key that must be integrated into your application.</span></span>

## <a name="sdk-integration"></a><span data-ttu-id="8fdec-118">SDK-integratie</span><span class="sxs-lookup"><span data-stu-id="8fdec-118">SDK integration</span></span>
### <a name="managing-device-registrations"></a><span data-ttu-id="8fdec-119">Het beheren van apparaat-registraties</span><span class="sxs-lookup"><span data-stu-id="8fdec-119">Managing device registrations</span></span>
<span data-ttu-id="8fdec-120">Elk apparaat een opdracht registratie toohello moet verzenden ADM-servers, anders ze kunnen niet worden bereikt.</span><span class="sxs-lookup"><span data-stu-id="8fdec-120">Each device must send a registration command toohello ADM servers, otherwise they can't be reached.</span></span>

<span data-ttu-id="8fdec-121">Als u al Hallo [ADM-clientbibliotheek], en al [ADM geïntegreerd] u rechtstreeks kunt gaan tooandroid-sdk-adm-ontvangen.</span><span class="sxs-lookup"><span data-stu-id="8fdec-121">If you already use hello [ADM client library], and already have [integrated ADM] you can directly go tooandroid-sdk-adm-receive.</span></span>

<span data-ttu-id="8fdec-122">Als u niet ADM geïntegreerd nog Engagement een eenvoudigere manier tooenable heeft in uw toepassing:</span><span class="sxs-lookup"><span data-stu-id="8fdec-122">If you have not integrated ADM yet, Engagement has a simpler way tooenable it in your application:</span></span>

<span data-ttu-id="8fdec-123">Bewerk uw `AndroidManifest.xml` bestand:</span><span class="sxs-lookup"><span data-stu-id="8fdec-123">Edit your `AndroidManifest.xml` file:</span></span>

* <span data-ttu-id="8fdec-124">Hallo Amazon-naamruimte, Hallo-bestand moet beginnen met het als volgt toevoegen:</span><span class="sxs-lookup"><span data-stu-id="8fdec-124">Add hello Amazon namespace, hello file should begin like this:</span></span>
  
      <?xml version="1.0" encoding="utf-8"?>
      <manifest xmlns:android="http://schemas.android.com/apk/res/android"
                xmlns:amazon="http://schemas.amazon.com/apk/res/android"
* <span data-ttu-id="8fdec-125">Hallo binnen `<application/>` tag, het toevoegen van deze sectie:</span><span class="sxs-lookup"><span data-stu-id="8fdec-125">Inside hello `<application/>` tag, add this section:</span></span>
  
      <amazon:enable-feature
         android:name="com.amazon.device.messaging"
         android:required="false"/>
  
      <meta-data android:name="engagement:adm:register" android:value="true" />
* <span data-ttu-id="8fdec-126">Na het toevoegen van Hallo amazon tag mogelijk hebt u een opbouwfout als uw doel van de Projectbuild lager dan Android 2.1 is.</span><span class="sxs-lookup"><span data-stu-id="8fdec-126">After adding hello amazon tag, you may have a build error if your Project Build Target is below Android 2.1.</span></span> <span data-ttu-id="8fdec-127">U hebt toouse een **Android 2.1 +** doel bouwen (Maak je geen zorgen, kunt u nog steeds een `minSdkVersion` too4 instellen).</span><span class="sxs-lookup"><span data-stu-id="8fdec-127">You have toouse an **Android 2.1+** build target (don't worry, you can still have a `minSdkVersion` set too4).</span></span>
* <span data-ttu-id="8fdec-128">Hallo ADM-API-sleutel integreren als een actief door [deze procedure].</span><span class="sxs-lookup"><span data-stu-id="8fdec-128">Integrate hello ADM API Key as an asset by following [this procedure].</span></span>

<span data-ttu-id="8fdec-129">Volg de instructies van de volgende secties Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="8fdec-129">Then follow hello instructions of hello next sections.</span></span>

### <a name="communicate-registration-id-toohello-engagement-push-service-and-receive-notifications"></a><span data-ttu-id="8fdec-130">Registratie-id toohello Engagement Push service communiceren en meldingen ontvangen</span><span class="sxs-lookup"><span data-stu-id="8fdec-130">Communicate registration id toohello Engagement Push service and receive notifications</span></span>
<span data-ttu-id="8fdec-131">In de volgorde toocommunicate Hallo registratie-id van Hallo apparaat toohello Engagement Push service en de meldingen ontvangen, Hallo na tooyour toevoegen `AndroidManifest.xml` bestand binnen Hallo `<application/>` tag (zelfs als u de ADM zonder Engagement gebruiken):</span><span class="sxs-lookup"><span data-stu-id="8fdec-131">In order toocommunicate hello registration id of hello device toohello Engagement Push service and receive its notifications, add hello following tooyour `AndroidManifest.xml` file, inside hello `<application/>` tag (even if you use ADM without Engagement):</span></span>

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

<span data-ttu-id="8fdec-132">Zorg ervoor dat u hebt Hallo volgende machtigingen in uw `AndroidManifest.xml` (voordat Hallo `</application>` label).</span><span class="sxs-lookup"><span data-stu-id="8fdec-132">Ensure you have hello following permissions in your `AndroidManifest.xml` (before hello `</application>` tag).</span></span>

        <uses-permission android:name="android.permission.WAKE_LOCK"/>
        <uses-permission android:name="com.amazon.device.messaging.permission.RECEIVE"/>
        <uses-permission android:name="<your_package_name>.permission.RECEIVE_ADM_MESSAGE"/>
        <permission android:name="<your_package_name>.permission.RECEIVE_ADM_MESSAGE" android:protectionLevel="signature"/>

## <a name="grant-engagement-oauth-credentials"></a><span data-ttu-id="8fdec-133">Verleen Engagement OAuth-referenties</span><span class="sxs-lookup"><span data-stu-id="8fdec-133">Grant Engagement OAuth credentials</span></span>
<span data-ttu-id="8fdec-134">Dien uw OAuth-referenties (Client-ID en Clientgeheim) in de Engagement-Portal.</span><span class="sxs-lookup"><span data-stu-id="8fdec-134">Submit your OAuth Credentials (Client ID and Client Secret) in Engagement Portal.</span></span>

[< https://developer.amazon.com/sdk/adm/credentials.html>]:https://developer.amazon.com/sdk/adm/credentials.html
[ADM-clientbibliotheek]:https://developer.amazon.com/sdk/adm/setup.html
[ADM geïntegreerd]:https://developer.amazon.com/sdk/adm/integrating-app.html
[deze procedure]:https://developer.amazon.com/sdk/adm/integrating-app.html#Asset

---
title: aaaAzure AD v2 Android aan de slag - Inleiding | Microsoft Docs
description: Hoe een Android-app kunt ophalen van een toegangstoken en Microsoft Graph API of API's waarvoor toegangstokens van Azure Active Directory-v2-eindpunt aanroepen
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.assetid: 820acdb7-d316-4c3b-8de9-79df48ba3b06
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andret
ms.custom: aaddev
ms.openlocfilehash: 7c76ab8bbf1a6c934ab672cccf85ae82f03f601a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="call-hello-microsoft-graph-api-from-an-android-app"></a><span data-ttu-id="e2943-103">Hallo Microsoft Graph API aanroepen vanuit een Android-app</span><span class="sxs-lookup"><span data-stu-id="e2943-103">Call hello Microsoft Graph API from an Android app</span></span>

<span data-ttu-id="e2943-104">Deze handleiding wordt uitgelegd hoe een systeemeigen Android-toepassing kunt ophalen van een toegangstoken en Microsoft Graph API of andere API's waarvoor toegangstokens van Azure Active Directory-v2-eindpunt niet aanroepen.</span><span class="sxs-lookup"><span data-stu-id="e2943-104">This guide demonstrates how a native Android application can get an access token and call Microsoft Graph API or other APIs that require access tokens from Azure Active Directory v2 endpoint.</span></span>

<span data-ttu-id="e2943-105">Aan het einde van de Hallo van deze handleiding, uw toepassing wordt kunnen toocall worden een beveiligde API met persoonlijke accounts (inclusief outlook.com, live.com en anderen), evenals werken en schoolaccounts van een bedrijf of organisatie die Azure Active Directory heeft.</span><span class="sxs-lookup"><span data-stu-id="e2943-105">At hello end of this guide, your application will be able toocall a protected API using personal accounts (including outlook.com, live.com, and others) as well as work and school accounts from any company or organization that has Azure Active Directory.</span></span>  

### <a name="how-this-sample-works"></a><span data-ttu-id="e2943-106">De werking van dit voorbeeld</span><span class="sxs-lookup"><span data-stu-id="e2943-106">How this sample works</span></span>
![De werking van dit voorbeeld](media/active-directory-mobileanddesktopapp-android-intro/android-intro.png)

<span data-ttu-id="e2943-108">Hallo-voorbeeld gemaakt door deze handleiding is gebaseerd op een scenario waarbij een Android-toepassing gebruikte tooquery een Web-API die tokens van Azure Active Directory v2-eindpunt: in dit geval Microsoft Graph API accepteert.</span><span class="sxs-lookup"><span data-stu-id="e2943-108">hello sample created by this guide is based on a scenario where an Android application is used tooquery a Web API that accepts tokens from Azure Active Directory v2 endpoint – in this case, Microsoft Graph API.</span></span> <span data-ttu-id="e2943-109">In dit scenario wordt een token tooHTTP-aanvragen via de autorisatie-header Hallo toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="e2943-109">For this scenario, a token is added tooHTTP requests via hello Authorization header.</span></span> <span data-ttu-id="e2943-110">Token verkrijgen en verlenging wordt verwerkt door Hallo Microsoft Authentication Library (MSAL).</span><span class="sxs-lookup"><span data-stu-id="e2943-110">Token acquisition and renewal is handled by hello Microsoft Authentication Library (MSAL).</span></span>

### <a name="pre-requisites"></a><span data-ttu-id="e2943-111">Vereisten</span><span class="sxs-lookup"><span data-stu-id="e2943-111">Pre-requisites</span></span>
* <span data-ttu-id="e2943-112">Deze Begeleide instelprocedure is gericht op Android Studio, maar ook alle andere Android-toepassing-ontwikkelomgeving aanvaardbaar is.</span><span class="sxs-lookup"><span data-stu-id="e2943-112">This guided setup is focused on Android Studio, but any other Android application development environment is also acceptable.</span></span> 
* <span data-ttu-id="e2943-113">Android SDK 21 of hoger is vereist (25 SDK wordt aanbevolen).</span><span class="sxs-lookup"><span data-stu-id="e2943-113">Android SDK 21 or newer is required (SDK 25 is recommended).</span></span>
* <span data-ttu-id="e2943-114">Google Chrome of een webbrowser met de tabbladen voor aangepaste is vereist voor deze release van Microsoft Authentication Library (MSAL) voor Android.</span><span class="sxs-lookup"><span data-stu-id="e2943-114">Google Chrome or a web browser using Custom Tabs is required for this release of Microsoft Authentication Library (MSAL) for Android.</span></span>

> <span data-ttu-id="e2943-115">Opmerking: Google Chrome is niet opgenomen in Visual Studio-Emulator voor Android.</span><span class="sxs-lookup"><span data-stu-id="e2943-115">Note: Google Chrome is not included on Visual Studio Emulator for Android.</span></span> <span data-ttu-id="e2943-116">We raden u tootest deze code die met Google Chrome geïnstalleerd op een Emulator met 25 API of een afbeelding met API-21 of hoger.</span><span class="sxs-lookup"><span data-stu-id="e2943-116">We recommend you tootest this code on an Emulator with API 25 or an image with API 21 or newer that has with Google Chrome installed.</span></span>


### <a name="how-toohandle-token-acquisition-tooaccess-a-protected-web-api"></a><span data-ttu-id="e2943-117">Hoe toohandle token overname tooaccess beveiligde Web-API</span><span class="sxs-lookup"><span data-stu-id="e2943-117">How toohandle token acquisition tooaccess a protected Web API</span></span>

<span data-ttu-id="e2943-118">Nadat Hallo gebruiker zich verifieert, ontvangt de voorbeeldtoepassing Hallo een token dat gebruikt tooquery Microsoft Graph API of een Web-API worden beveiligd door Microsoft Azure Active Directory-v2 worden kan.</span><span class="sxs-lookup"><span data-stu-id="e2943-118">After hello user authenticates, hello sample application receives a token that can be used tooquery Microsoft Graph API or a Web API secured by Microsoft Azure Active Directory v2.</span></span>

<span data-ttu-id="e2943-119">API's, zoals Microsoft Graph vereisen een access token tooallow toegang tot specifieke bronnen – bijvoorbeeld tooread een gebruikersprofiel, toegang tot de agenda gebruiker of een e-mailbericht verzenden.</span><span class="sxs-lookup"><span data-stu-id="e2943-119">APIs such as Microsoft Graph require an access token tooallow accessing specific resources – for example, tooread a user’s profile, access user’s calendar or send an email.</span></span> <span data-ttu-id="e2943-120">Uw toepassing kan een toegangstoken MSAL tooaccess met deze resources aanvragen door op te geven van de API-scopes.</span><span class="sxs-lookup"><span data-stu-id="e2943-120">Your application can request an access token using MSAL tooaccess these resources by specifying API scopes.</span></span> <span data-ttu-id="e2943-121">Deze toegangstoken is toegevoegd toohello HTTP-autorisatie-header voor elke aanroep ten opzichte van Hallo beveiligde resource.</span><span class="sxs-lookup"><span data-stu-id="e2943-121">This access token is then added toohello HTTP Authorization header for every call made against hello protected resource.</span></span> 

<span data-ttu-id="e2943-122">MSAL kunt opslaan in cache en vernieuwen toegangstokens voor u, zodat uw toepassing niet te hoeft beheren.</span><span class="sxs-lookup"><span data-stu-id="e2943-122">MSAL manages caching and refreshing access tokens for you, so your application doesn't need to.</span></span>

### <a name="libraries"></a><span data-ttu-id="e2943-123">Bibliotheken</span><span class="sxs-lookup"><span data-stu-id="e2943-123">Libraries</span></span>

<span data-ttu-id="e2943-124">Deze handleiding gebruikt Hallo bibliotheken te volgen:</span><span class="sxs-lookup"><span data-stu-id="e2943-124">This guide uses hello following libraries:</span></span>

|<span data-ttu-id="e2943-125">Bibliotheek</span><span class="sxs-lookup"><span data-stu-id="e2943-125">Library</span></span>|<span data-ttu-id="e2943-126">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="e2943-126">Description</span></span>|
|---|---|
|[<span data-ttu-id="e2943-127">com.Microsoft.Identity.client</span><span class="sxs-lookup"><span data-stu-id="e2943-127">com.microsoft.identity.client</span></span>](http://javadoc.io/doc/com.microsoft.identity.client/msal)|<span data-ttu-id="e2943-128">Microsoft-Verificatiebibliotheek (MSAL)</span><span class="sxs-lookup"><span data-stu-id="e2943-128">Microsoft Authentication Library (MSAL)</span></span>|

---
title: Azure AD v2 Android aan de slag - Inleiding | Microsoft Docs
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
ms.openlocfilehash: d933781713456f73aa76db557fdf35672dfb2a29
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="call-the-microsoft-graph-api-from-an-android-app"></a><span data-ttu-id="c639e-103">Microsoft Graph API aanroepen vanuit een Android-app</span><span class="sxs-lookup"><span data-stu-id="c639e-103">Call the Microsoft Graph API from an Android app</span></span>

<span data-ttu-id="c639e-104">Deze handleiding wordt uitgelegd hoe een systeemeigen Android-toepassing kunt ophalen van een toegangstoken en Microsoft Graph API of andere API's waarvoor toegangstokens van Azure Active Directory-v2-eindpunt niet aanroepen.</span><span class="sxs-lookup"><span data-stu-id="c639e-104">This guide demonstrates how a native Android application can get an access token and call Microsoft Graph API or other APIs that require access tokens from Azure Active Directory v2 endpoint.</span></span>

<span data-ttu-id="c639e-105">Aan het einde van deze handleiding, uw toepassing kan worden aanroepen van een beveiligde API met persoonlijke accounts (inclusief outlook.com, live.com en anderen) en de werk- en schoolaccounts van een bedrijf of organisatie die Azure Active Directory heeft.</span><span class="sxs-lookup"><span data-stu-id="c639e-105">At the end of this guide, your application will be able to call a protected API using personal accounts (including outlook.com, live.com, and others) as well as work and school accounts from any company or organization that has Azure Active Directory.</span></span>  

### <a name="how-this-sample-works"></a><span data-ttu-id="c639e-106">De werking van dit voorbeeld</span><span class="sxs-lookup"><span data-stu-id="c639e-106">How this sample works</span></span>
![De werking van dit voorbeeld](media/active-directory-mobileanddesktopapp-android-intro/android-intro.png)

<span data-ttu-id="c639e-108">Het voorbeeld dat is gemaakt door deze handleiding is gebaseerd op een scenario waarbij een Android-toepassing wordt gebruikt voor het zoeken van een Web-API die tokens van Azure Active Directory v2-eindpunt: in dit geval Microsoft Graph API accepteert.</span><span class="sxs-lookup"><span data-stu-id="c639e-108">The sample created by this guide is based on a scenario where an Android application is used to query a Web API that accepts tokens from Azure Active Directory v2 endpoint – in this case, Microsoft Graph API.</span></span> <span data-ttu-id="c639e-109">Voor dit scenario wordt een token toegevoegd om HTTP-aanvragen via de autorisatie-header.</span><span class="sxs-lookup"><span data-stu-id="c639e-109">For this scenario, a token is added to HTTP requests via the Authorization header.</span></span> <span data-ttu-id="c639e-110">Token verkrijgen en verlenging wordt verwerkt door de Microsoft Authentication Library (MSAL).</span><span class="sxs-lookup"><span data-stu-id="c639e-110">Token acquisition and renewal is handled by the Microsoft Authentication Library (MSAL).</span></span>

### <a name="pre-requisites"></a><span data-ttu-id="c639e-111">Vereisten</span><span class="sxs-lookup"><span data-stu-id="c639e-111">Pre-requisites</span></span>
* <span data-ttu-id="c639e-112">Deze Begeleide instelprocedure is gericht op Android Studio, maar ook alle andere Android-toepassing-ontwikkelomgeving aanvaardbaar is.</span><span class="sxs-lookup"><span data-stu-id="c639e-112">This guided setup is focused on Android Studio, but any other Android application development environment is also acceptable.</span></span> 
* <span data-ttu-id="c639e-113">Android SDK 21 of hoger is vereist (25 SDK wordt aanbevolen).</span><span class="sxs-lookup"><span data-stu-id="c639e-113">Android SDK 21 or newer is required (SDK 25 is recommended).</span></span>
* <span data-ttu-id="c639e-114">Google Chrome of een webbrowser met de tabbladen voor aangepaste is vereist voor deze release van Microsoft Authentication Library (MSAL) voor Android.</span><span class="sxs-lookup"><span data-stu-id="c639e-114">Google Chrome or a web browser using Custom Tabs is required for this release of Microsoft Authentication Library (MSAL) for Android.</span></span>

> <span data-ttu-id="c639e-115">Opmerking: Google Chrome is niet opgenomen in Visual Studio-Emulator voor Android.</span><span class="sxs-lookup"><span data-stu-id="c639e-115">Note: Google Chrome is not included on Visual Studio Emulator for Android.</span></span> <span data-ttu-id="c639e-116">We raden u aan deze code op een Emulator met 25 API of een afbeelding met API-21 of hoger die met Google Chrome geïnstalleerd testen.</span><span class="sxs-lookup"><span data-stu-id="c639e-116">We recommend you to test this code on an Emulator with API 25 or an image with API 21 or newer that has with Google Chrome installed.</span></span>


### <a name="how-to-handle-token-acquisition-to-access-a-protected-web-api"></a><span data-ttu-id="c639e-117">Hoe moet worden verwerkt token verkrijgen voor toegang tot een beveiligde Web-API</span><span class="sxs-lookup"><span data-stu-id="c639e-117">How to handle token acquisition to access a protected Web API</span></span>

<span data-ttu-id="c639e-118">Nadat de gebruiker zich verifieert, ontvangt de voorbeeldtoepassing een token dat kan worden gebruikt voor Microsoft Graph API of een Web-API worden beveiligd door Microsoft Azure Active Directory-v2 query.</span><span class="sxs-lookup"><span data-stu-id="c639e-118">After the user authenticates, the sample application receives a token that can be used to query Microsoft Graph API or a Web API secured by Microsoft Azure Active Directory v2.</span></span>

<span data-ttu-id="c639e-119">API's zoals Microsoft Graph vereisen een toegangstoken waarmee toegang tot specifieke bronnen – bijvoorbeeld een gebruikersprofiel, toegang tot de agenda gebruiker lezen of een e-mailbericht verzenden.</span><span class="sxs-lookup"><span data-stu-id="c639e-119">APIs such as Microsoft Graph require an access token to allow accessing specific resources – for example, to read a user’s profile, access user’s calendar or send an email.</span></span> <span data-ttu-id="c639e-120">Uw toepassing kan aanvragen van een toegangstoken MSAL gebruiken voor toegang tot deze bronnen door te geven van de API-scopes.</span><span class="sxs-lookup"><span data-stu-id="c639e-120">Your application can request an access token using MSAL to access these resources by specifying API scopes.</span></span> <span data-ttu-id="c639e-121">Deze toegangstoken wordt vervolgens toegevoegd aan de HTTP-autorisatie-header voor elke aanroep ten opzichte van de beveiligde bron.</span><span class="sxs-lookup"><span data-stu-id="c639e-121">This access token is then added to the HTTP Authorization header for every call made against the protected resource.</span></span> 

<span data-ttu-id="c639e-122">MSAL kunt opslaan in cache en vernieuwen toegangstokens voor u, zodat uw toepassing niet te hoeft beheren.</span><span class="sxs-lookup"><span data-stu-id="c639e-122">MSAL manages caching and refreshing access tokens for you, so your application doesn't need to.</span></span>

### <a name="libraries"></a><span data-ttu-id="c639e-123">Bibliotheken</span><span class="sxs-lookup"><span data-stu-id="c639e-123">Libraries</span></span>

<span data-ttu-id="c639e-124">Deze handleiding bevat de volgende bibliotheken:</span><span class="sxs-lookup"><span data-stu-id="c639e-124">This guide uses the following libraries:</span></span>

|<span data-ttu-id="c639e-125">Bibliotheek</span><span class="sxs-lookup"><span data-stu-id="c639e-125">Library</span></span>|<span data-ttu-id="c639e-126">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="c639e-126">Description</span></span>|
|---|---|
|[<span data-ttu-id="c639e-127">com.Microsoft.Identity.client</span><span class="sxs-lookup"><span data-stu-id="c639e-127">com.microsoft.identity.client</span></span>](http://javadoc.io/doc/com.microsoft.identity.client/msal)|<span data-ttu-id="c639e-128">Microsoft-Verificatiebibliotheek (MSAL)</span><span class="sxs-lookup"><span data-stu-id="c639e-128">Microsoft Authentication Library (MSAL)</span></span>|

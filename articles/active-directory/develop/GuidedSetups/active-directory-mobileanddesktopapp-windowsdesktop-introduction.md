---
title: aaaAzure AD v2 Windows Desktop aan de slag - Inleiding | Microsoft Docs
description: Hoe Windows Desktop .NET (XAML) toepassingen een API waarvoor toegangstokens door Azure Active Directory-v2-eindpunt kunnen aanroepen
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
ms.openlocfilehash: 89d98fc46190ba9e47b7c3095f91e32eca455fcc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="call-hello-microsoft-graph-api-from-a-windows-desktop-app"></a><span data-ttu-id="4b6e0-103">Hallo Microsoft Graph API aanroepen vanuit een Windows-bureaublad-app</span><span class="sxs-lookup"><span data-stu-id="4b6e0-103">Call hello Microsoft Graph API from a Windows Desktop app</span></span>

<span data-ttu-id="4b6e0-104">Deze handleiding wordt uitgelegd hoe een systeemeigen Windows Desktop .NET (XAML)-toepassing kunt ophalen van een toegangstoken en Microsoft Graph API of andere API's waarvoor toegangstokens van Azure Active Directory-v2-eindpunt niet aanroepen.</span><span class="sxs-lookup"><span data-stu-id="4b6e0-104">This guide demonstrates how a native Windows Desktop .NET (XAML) application can get an access token and call Microsoft Graph API or other APIs that require access tokens from Azure Active Directory v2 endpoint.</span></span>

<span data-ttu-id="4b6e0-105">Aan het einde van de Hallo van deze handleiding, uw toepassing wordt kunnen toocall worden een beveiligde API met persoonlijke accounts (inclusief outlook.com, live.com en anderen), evenals werken en schoolaccounts van een bedrijf of organisatie die Azure Active Directory heeft.</span><span class="sxs-lookup"><span data-stu-id="4b6e0-105">At hello end of this guide, your application will be able toocall a protected API using personal accounts (including outlook.com, live.com, and others) as well as work and school accounts from any company or organization that has Azure Active Directory.</span></span>  

> <span data-ttu-id="4b6e0-106">Deze handleiding is Visual Studio 2015 Update 3 of Visual Studio 2017 vereist.</span><span class="sxs-lookup"><span data-stu-id="4b6e0-106">This guide requires Visual Studio 2015 Update 3 or Visual Studio 2017.</span></span>  <span data-ttu-id="4b6e0-107">Hebt u geen deze?</span><span class="sxs-lookup"><span data-stu-id="4b6e0-107">Don’t have it?</span></span> [<span data-ttu-id="4b6e0-108">Visual Studio 2017 gratis downloaden</span><span class="sxs-lookup"><span data-stu-id="4b6e0-108">Download Visual Studio 2017 for free</span></span>](https://www.visualstudio.com/downloads/)

### <a name="how-this-guide-works"></a><span data-ttu-id="4b6e0-109">De werking van deze handleiding</span><span class="sxs-lookup"><span data-stu-id="4b6e0-109">How this guide works</span></span>

![De werking van deze handleiding](media/active-directory-mobileanddesktopapp-windowsdesktop-intro/windesktophowitworks.png)

<span data-ttu-id="4b6e0-111">Hallo-voorbeeldtoepassing die is gemaakt door deze handleiding kunt een Windows-bureaubladtoepassingen tooquery Microsoft Graph API of een Web-API die tokens van Azure Active Directory-v2-eindpunt accepteert.</span><span class="sxs-lookup"><span data-stu-id="4b6e0-111">hello sample application created by this guide enables a Windows Desktop Application tooquery Microsoft Graph API or a Web API that accepts tokens from Azure Active Directory v2 endpoint.</span></span> <span data-ttu-id="4b6e0-112">In dit scenario wordt een token tooHTTP-aanvragen via de autorisatie-header Hallo toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="4b6e0-112">For this scenario, a token is added tooHTTP requests via hello Authorization header.</span></span> <span data-ttu-id="4b6e0-113">Token verkrijgen en verlenging wordt verwerkt door Hallo Microsoft Authentication Library (MSAL).</span><span class="sxs-lookup"><span data-stu-id="4b6e0-113">Token acquisition and renewal is handled by hello Microsoft Authentication Library (MSAL).</span></span>


### <a name="handling-token-acquisition-for-accessing-protected-web-apis"></a><span data-ttu-id="4b6e0-114">Afhandeling van token verkrijgen voor toegang tot Web-API's beveiligd</span><span class="sxs-lookup"><span data-stu-id="4b6e0-114">Handling token acquisition for accessing protected Web APIs</span></span>

<span data-ttu-id="4b6e0-115">Nadat Hallo gebruiker zich verifieert, ontvangt de voorbeeldtoepassing Hallo een token dat gebruikt tooquery Microsoft Graph API of een Web-API worden beveiligd door Microsoft Azure Active Directory-v2 worden kan.</span><span class="sxs-lookup"><span data-stu-id="4b6e0-115">After hello user authenticates, hello sample application receives a token that can be used tooquery Microsoft Graph API or a Web API secured by Microsoft Azure Active Directory v2.</span></span>

<span data-ttu-id="4b6e0-116">API's, zoals Microsoft Graph vereisen een access token tooallow toegang tot specifieke bronnen – bijvoorbeeld tooread een gebruikersprofiel, toegang tot de agenda gebruiker of een e-mailbericht verzenden.</span><span class="sxs-lookup"><span data-stu-id="4b6e0-116">APIs such as Microsoft Graph require an access token tooallow accessing specific resources – for example, tooread a user’s profile, access user’s calendar or send an email.</span></span> <span data-ttu-id="4b6e0-117">Uw toepassing kan een toegangstoken MSAL tooaccess met deze resources aanvragen door op te geven van de API-scopes.</span><span class="sxs-lookup"><span data-stu-id="4b6e0-117">Your application can request an access token using MSAL tooaccess these resources by specifying API scopes.</span></span> <span data-ttu-id="4b6e0-118">Deze toegangstoken is toegevoegd toohello HTTP-autorisatie-header voor elke aanroep ten opzichte van Hallo beveiligde resource.</span><span class="sxs-lookup"><span data-stu-id="4b6e0-118">This access token is then added toohello HTTP Authorization header for every call made against hello protected resource.</span></span> 

<span data-ttu-id="4b6e0-119">MSAL kunt opslaan in cache en vernieuwen toegangstokens voor u, zodat uw toepassing niet te hoeft beheren.</span><span class="sxs-lookup"><span data-stu-id="4b6e0-119">MSAL manages caching and refreshing access tokens for you, so your application doesn't need to.</span></span>


### <a name="nuget-packages"></a><span data-ttu-id="4b6e0-120">NuGet-pakketten</span><span class="sxs-lookup"><span data-stu-id="4b6e0-120">NuGet Packages</span></span>

<span data-ttu-id="4b6e0-121">Deze handleiding gebruikt Hallo NuGet-pakketten te volgen:</span><span class="sxs-lookup"><span data-stu-id="4b6e0-121">This guide uses hello following NuGet packages:</span></span>

|<span data-ttu-id="4b6e0-122">Bibliotheek</span><span class="sxs-lookup"><span data-stu-id="4b6e0-122">Library</span></span>|<span data-ttu-id="4b6e0-123">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="4b6e0-123">Description</span></span>|
|---|---|
|[<span data-ttu-id="4b6e0-124">Microsoft.Identity.Client</span><span class="sxs-lookup"><span data-stu-id="4b6e0-124">Microsoft.Identity.Client</span></span>](https://www.nuget.org/packages/Microsoft.Identity.Client)|<span data-ttu-id="4b6e0-125">Microsoft-Verificatiebibliotheek (MSAL)</span><span class="sxs-lookup"><span data-stu-id="4b6e0-125">Microsoft Authentication Library (MSAL)</span></span>|


---
title: aaaAzure AD v2 ASP.NET Web Server aan de slag - Inleiding | Microsoft Docs
description: Implementeren van Microsoft-aanmeldingspagina op een ASP.NET-oplossing met een traditioneel browser gebaseerde webtoepassing met behulp van standaard OpenID Connect
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
ms.openlocfilehash: d6449926af2bdad24cbc8e91f74885a08f909103
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="add-sign-in-with-microsoft-tooan-aspnet-web-app"></a><span data-ttu-id="3332e-103">Aanmelden met Microsoft tooan ASP.NET-web-app toevoegen</span><span class="sxs-lookup"><span data-stu-id="3332e-103">Add sign-in with Microsoft tooan ASP.NET web app</span></span>

<span data-ttu-id="3332e-104">Deze handleiding wordt uitgelegd hoe tooimplement aanmelden bij Microsoft met behulp van een ASP.NET MVC-oplossing met een traditioneel browser gebaseerde webtoepassing met OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="3332e-104">This guide demonstrates how tooimplement sign-in with Microsoft using an ASP.NET MVC solution with a traditional web browser-based application using OpenID Connect.</span></span> 

<span data-ttu-id="3332e-105">Aan het einde van de Hallo van deze handleiding, wordt uw toepassing kunnen tooaccept aanmelding modules van persoonlijke accounts (inclusief outlook.com, live.com en anderen), evenals werken en schoolaccounts zijn uit een bedrijf of organisatie die is geïntegreerd met Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="3332e-105">At hello end of this guide, your application will be able tooaccept sign ins of personal accounts (including outlook.com, live.com, and others) as well as work and school accounts from any company or organization that has integrated with Azure Active Directory.</span></span> 

> <span data-ttu-id="3332e-106">Deze handleiding is Visual Studio 2015 Update 3 of Visual Studio 2017 vereist.</span><span class="sxs-lookup"><span data-stu-id="3332e-106">This guide requires Visual Studio 2015 Update 3 or Visual Studio 2017.</span></span>  <span data-ttu-id="3332e-107">Hebt u geen deze?</span><span class="sxs-lookup"><span data-stu-id="3332e-107">Don’t have it?</span></span>  [<span data-ttu-id="3332e-108">Visual Studio 2017 gratis downloaden</span><span class="sxs-lookup"><span data-stu-id="3332e-108">Download Visual Studio 2017 for free</span></span>](https://www.visualstudio.com/downloads/)

## <a name="how-this-guide-works"></a><span data-ttu-id="3332e-109">De werking van deze handleiding</span><span class="sxs-lookup"><span data-stu-id="3332e-109">How this guide works</span></span>

![De werking van deze handleiding](media/active-directory-serversidewebapp-aspnetwebappowin-intro/aspnetbrowsergeneral.png)

<span data-ttu-id="3332e-111">Deze handleiding is gebaseerd op Hallo scenario waarbij een browser toegang heeft tot een ASP.NET-website aanvragen van een gebruiker tooauthenticate via een knop aanmelden.</span><span class="sxs-lookup"><span data-stu-id="3332e-111">This guide is based on hello scenario where a browser accesses an ASP.NET web site, requesting a user tooauthenticate via a sign-in button.</span></span> <span data-ttu-id="3332e-112">In dit scenario wordt de meeste Hallo werk toorender Hallo-webpagina op Hallo serverzijde plaats.</span><span class="sxs-lookup"><span data-stu-id="3332e-112">In this scenario, most of hello work toorender hello web page occurs on hello server side.</span></span>

## <a name="libraries"></a><span data-ttu-id="3332e-113">Bibliotheken</span><span class="sxs-lookup"><span data-stu-id="3332e-113">Libraries</span></span>

<span data-ttu-id="3332e-114">Deze handleiding gebruikt Hallo bibliotheken te volgen:</span><span class="sxs-lookup"><span data-stu-id="3332e-114">This guide uses hello following libraries:</span></span>

|<span data-ttu-id="3332e-115">Bibliotheek</span><span class="sxs-lookup"><span data-stu-id="3332e-115">Library</span></span>|<span data-ttu-id="3332e-116">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="3332e-116">Description</span></span>|
|---|---|
|[<span data-ttu-id="3332e-117">Microsoft.Owin.Security.OpenIdConnect</span><span class="sxs-lookup"><span data-stu-id="3332e-117">Microsoft.Owin.Security.OpenIdConnect</span></span>](https://www.nuget.org/packages/Microsoft.Owin.Security.OpenIdConnect/)|<span data-ttu-id="3332e-118">Middleware waarmee een toepassing toouse OpenIdConnect voor verificatie</span><span class="sxs-lookup"><span data-stu-id="3332e-118">Middleware that enables an application toouse OpenIdConnect for authentication</span></span>|
|[<span data-ttu-id="3332e-119">Microsoft.Owin.Security.Cookies</span><span class="sxs-lookup"><span data-stu-id="3332e-119">Microsoft.Owin.Security.Cookies</span></span>](https://www.nuget.org/packages/Microsoft.Owin.Security.Cookies)|<span data-ttu-id="3332e-120">Middleware waarmee een toepassing toomaintain gebruikerssessie met behulp van cookies</span><span class="sxs-lookup"><span data-stu-id="3332e-120">Middleware that enables an application toomaintain user session using cookies</span></span>|
|[<span data-ttu-id="3332e-121">Microsoft.Owin.Host.SystemWeb</span><span class="sxs-lookup"><span data-stu-id="3332e-121">Microsoft.Owin.Host.SystemWeb</span></span>](https://www.nuget.org/packages/Microsoft.Owin.Host.SystemWeb)|<span data-ttu-id="3332e-122">Hiermee toorun OWIN-toepassingen op IIS met ASP.NET-aanvraag pipeline-Hallo</span><span class="sxs-lookup"><span data-stu-id="3332e-122">Enables OWIN-based applications toorun on IIS using hello ASP.NET request pipeline</span></span>|


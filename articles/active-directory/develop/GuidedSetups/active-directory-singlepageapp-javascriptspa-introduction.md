---
title: aaaAzure AD v2 JS SPA begeleide Setup - Inleiding | Microsoft Docs
description: Hoe een API waarvoor toegangstokens door Azure Active Directory-v2-eindpunt kunnen aanroepen in JavaScript SPA-toepassingen
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/01/2017
ms.author: andret
ms.openlocfilehash: 7e4250ccca837a17489a99603da167009cc2e3d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="call-hello-microsoft-graph-api-from-a-javascript-single-page-application-spa"></a><span data-ttu-id="a805e-103">Hallo Microsoft Graph API aanroepen vanuit een JavaScript één pagina toepassing (SPA)</span><span class="sxs-lookup"><span data-stu-id="a805e-103">Call hello Microsoft Graph API from a JavaScript Single Page Application (SPA)</span></span>

<span data-ttu-id="a805e-104">Deze handleiding wordt uitgelegd hoe een JavaScript één pagina toepassing (SPA) persoonlijk, werk kunt aanmelden en schoolaccounts, een toegangstoken ophalen en Hallo Microsoft Graph API aanroepen of andere API's waarvoor toegangstokens van hello Azure Active Directory-v2-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="a805e-104">This guide demonstrates how a JavaScript Single Page Application (SPA) can sign in personal, work and school accounts, get an access token, and call hello Microsoft Graph API or other APIs that require access tokens from hello Azure Active Directory v2 endpoint.</span></span>

### <a name="how-this-guide-works"></a><span data-ttu-id="a805e-105">De werking van deze handleiding</span><span class="sxs-lookup"><span data-stu-id="a805e-105">How this guide works</span></span>

![De werking van Hallo voorbeeld-app is gegenereerd door deze handleiding](media/active-directory-singlepageapp-javascriptspa-introduction/javascriptspa-intro.png)

<!--start-collapse-->
### <a name="more-information"></a><span data-ttu-id="a805e-107">Meer informatie</span><span class="sxs-lookup"><span data-stu-id="a805e-107">More Information</span></span>

<span data-ttu-id="a805e-108">Hallo-voorbeeldtoepassing die is gemaakt door deze handleiding laat een JavaScript-SPA tooquery Hallo Microsoft Graph API of een Web-API die tokens van Azure Active Directory-v2-eindpunt accepteert.</span><span class="sxs-lookup"><span data-stu-id="a805e-108">hello sample application created by this guide enables a JavaScript SPA tooquery hello Microsoft Graph API or a Web API that accepts tokens from Azure Active Directory v2 endpoint.</span></span> <span data-ttu-id="a805e-109">In dit scenario wordt een toegangstoken nadat een gebruiker zich aanmeldt, aangevraagde en toegevoegde tooHTTP-aanvragen via Hallo autorisatie-header.</span><span class="sxs-lookup"><span data-stu-id="a805e-109">For this scenario, after a user signs-in, an access token is requested and added tooHTTP requests via hello authorization header.</span></span> <span data-ttu-id="a805e-110">Token verkrijgen en verlenging worden afgehandeld door Hallo Microsoft Authentication Library (MSAL).</span><span class="sxs-lookup"><span data-stu-id="a805e-110">Token acquisition and renewal are handled by hello Microsoft Authentication Library (MSAL).</span></span>

<!--end-collapse-->

<!--start-collapse-->
### <a name="libraries"></a><span data-ttu-id="a805e-111">Bibliotheken</span><span class="sxs-lookup"><span data-stu-id="a805e-111">Libraries</span></span>

<span data-ttu-id="a805e-112">Deze handleiding gebruikt Hallo bibliotheek te volgen:</span><span class="sxs-lookup"><span data-stu-id="a805e-112">This guide uses hello following library:</span></span>

|<span data-ttu-id="a805e-113">Bibliotheek</span><span class="sxs-lookup"><span data-stu-id="a805e-113">Library</span></span>|<span data-ttu-id="a805e-114">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="a805e-114">Description</span></span>|
|---|---|
|[<span data-ttu-id="a805e-115">msal.js</span><span class="sxs-lookup"><span data-stu-id="a805e-115">msal.js</span></span>](https://github.com/AzureAD/microsoft-authentication-library-for-js)|<span data-ttu-id="a805e-116">Microsoft-Verificatiebibliotheek voor JavaScript-Preview</span><span class="sxs-lookup"><span data-stu-id="a805e-116">Microsoft Authentication Library for JavaScript Preview</span></span>|

> [!NOTE]
> <span data-ttu-id="a805e-117">*msal.js* doelen Hallo *Azure Active Directory-v2-eindpunt* -die Hiermee privé, school- als accounts toosign in- en tokens verkrijgen.</span><span class="sxs-lookup"><span data-stu-id="a805e-117">*msal.js* targets hello *Azure Active Directory v2 endpoint* - which enables personal, school and work accounts toosign in and acquire tokens.</span></span> <span data-ttu-id="a805e-118">Hallo *Azure Active Directory-v2-eindpunt* heeft [enkele beperkingen](..\active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="a805e-118">hello *Azure Active Directory v2 endpoint* has [some limitations](..\active-directory-v2-limitations.md).</span></span> <span data-ttu-id="a805e-119">Als u alleen geïnteresseerd in school- als accounts, gebruikt *adal.js* en Hallo *V1 eindpunt*.</span><span class="sxs-lookup"><span data-stu-id="a805e-119">If you are interested only in school and work accounts, use *adal.js* and hello *V1 endpoint*.</span></span> <span data-ttu-id="a805e-120">verschillen tussen de Hallo v1- en v2-eindpunten toounderstand lezen Hallo [v1-v2 vergelijking](..\active-directory-v2-compare.md).</span><span class="sxs-lookup"><span data-stu-id="a805e-120">toounderstand differences between hello v1 and v2 endpoints read hello [v1-v2 comparison](..\active-directory-v2-compare.md).</span></span>

<!--end-collapse-->

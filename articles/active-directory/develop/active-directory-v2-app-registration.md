---
title: een toepassing met hello Azure AD v2.0-eindpunt met behulp van de portal Hallo aaaRegister | Microsoft Docs
description: Hoe tooregister een app met Microsoft voor het inschakelen aanmelden en toegang tot Microsoft-services met behulp van Hallo v2.0-eindpunt
services: active-directory
documentationcenter: 
author: lnalepa
manager: mbaldwin
editor: 
ms.assetid: bb2f701f-3bc3-4759-94a5-8b9d53a8a0b6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/01/2017
ms.author: lenalepa
ms.custom: aaddev
ms.openlocfilehash: c56c98906656062435516e820cb318a04c03149c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooregister-an-app-with-hello-v20-endpoint"></a><span data-ttu-id="439b7-103">Hoe tooregister een app met Hallo v2.0-eindpunt</span><span class="sxs-lookup"><span data-stu-id="439b7-103">How tooregister an app with hello v2.0 endpoint</span></span>
<span data-ttu-id="439b7-104">een app die zowel MSA & Azure AD accepteert toobuild aanmelden, moet u eerst een app met Microsoft tooregister.</span><span class="sxs-lookup"><span data-stu-id="439b7-104">toobuild an app that accepts both MSA & Azure AD sign-in, you'll first need tooregister an app with Microsoft.</span></span>  <span data-ttu-id="439b7-105">Op dit moment kunt u won't kunnen toouse worden alle bestaande apps u met Azure AD hebt wellicht of MSA - u moet een merk nieuwe toocreate.</span><span class="sxs-lookup"><span data-stu-id="439b7-105">At this time, you won't be able toouse any existing apps you may have with Azure AD or MSA - you'll need toocreate a brand new one.</span></span>

> [!NOTE]
> <span data-ttu-id="439b7-106">Niet alle Azure Active Directory-scenario's en functies worden ondersteund door Hallo v2.0-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="439b7-106">Not all Azure Active Directory scenarios & features are supported by hello v2.0 endpoint.</span></span>  <span data-ttu-id="439b7-107">toodetermine als Hallo v2.0-eindpunt, moet u meer informatie over [v2.0 beperkingen](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="439b7-107">toodetermine if you should use hello v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 
> 

## <a name="visit-hello-microsoft-app-registration-portal"></a><span data-ttu-id="439b7-108">Ga naar Hallo-portal voor registratie van Microsoft-app</span><span class="sxs-lookup"><span data-stu-id="439b7-108">Visit hello Microsoft app registration portal</span></span>
<span data-ttu-id="439b7-109">Eerste dingen eerst - Navigeer te[https://apps.dev.microsoft.com/?deeplink=/appList](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList).</span><span class="sxs-lookup"><span data-stu-id="439b7-109">First things first - navigate too[https://apps.dev.microsoft.com/?deeplink=/appList](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList).</span></span>  <span data-ttu-id="439b7-110">Dit is een nieuwe app-portal voor wachtwoordregistratie waar u uw Microsoft-apps kunt beheren.</span><span class="sxs-lookup"><span data-stu-id="439b7-110">This is a new app registration portal where you can manage your Microsoft apps.</span></span>

<span data-ttu-id="439b7-111">Meld u aan met ofwel een persoonlijke of werk of school Microsoft-account.</span><span class="sxs-lookup"><span data-stu-id="439b7-111">Sign in with either a personal or work or school Microsoft account.</span></span>  <span data-ttu-id="439b7-112">Als u geen ofwel hebt, moet u zich aanmelden voor een nieuw persoonlijk account.</span><span class="sxs-lookup"><span data-stu-id="439b7-112">If you don't have either, sign up for a new personal account.</span></span> <span data-ttu-id="439b7-113">Opwekken, won't duurt lang - wij hier wachten.</span><span class="sxs-lookup"><span data-stu-id="439b7-113">Go ahead, it won't take long - we'll wait here.</span></span>

<span data-ttu-id="439b7-114">Uitgevoerd?</span><span class="sxs-lookup"><span data-stu-id="439b7-114">Done?</span></span> <span data-ttu-id="439b7-115">U moet nu worden kijken naar de lijst met Microsoft-apps, die waarschijnlijk leeg is.</span><span class="sxs-lookup"><span data-stu-id="439b7-115">You should now be looking at your list of Microsoft apps, which is probably empty.</span></span>  <span data-ttu-id="439b7-116">Hiermee kunt wijzigen.</span><span class="sxs-lookup"><span data-stu-id="439b7-116">Let's change that.</span></span>

<span data-ttu-id="439b7-117">Klik op **een app toevoegen**, en een naam geven.</span><span class="sxs-lookup"><span data-stu-id="439b7-117">Click **Add an app**, and give it a name.</span></span>  <span data-ttu-id="439b7-118">Hallo portal toewijzen uw app een globally unique identifier toepassings-Id die u later in uw code.</span><span class="sxs-lookup"><span data-stu-id="439b7-118">hello portal will assign your app a globally unique  Application Id that you'll use later in your code.</span></span>  <span data-ttu-id="439b7-119">Als uw app een serverzijde-onderdeel bevat dat toegangstokens moet voor aanroepen API's (nadenkt: Office, Azure of uw eigen web-API), moet u toocreate een **Toepassingsgeheim** hier ook.</span><span class="sxs-lookup"><span data-stu-id="439b7-119">If your app includes a server-side component that needs access tokens for calling APIs (think: Office, Azure, or your own web API), you'll want toocreate an **Application Secret** here as well.</span></span>

<span data-ttu-id="439b7-120">Voeg vervolgens Hallo Platforms die uw app wilt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="439b7-120">Next, add hello Platforms that your app will use.</span></span>

* <span data-ttu-id="439b7-121">Voor op basis van web-apps, geeft u een **omleidings-URI** waar aanmelden berichten kunnen worden verzonden.</span><span class="sxs-lookup"><span data-stu-id="439b7-121">For web based apps, provide a **Redirect URI** where sign-in messages can be sent.</span></span>
* <span data-ttu-id="439b7-122">Voor mobiele apps Noteer Hallo standaard omleidings-uri die automatisch voor u gemaakt.</span><span class="sxs-lookup"><span data-stu-id="439b7-122">For mobile apps, copy down hello default redirect uri automatically created for you.</span></span>

<span data-ttu-id="439b7-123">U kunt eventueel Hallo uiterlijk van de aanmeldingspagina in Hallo-profiel.</span><span class="sxs-lookup"><span data-stu-id="439b7-123">Optionally, you can customize hello look and feel of your sign-in page in hello Profile section.</span></span>  <span data-ttu-id="439b7-124">Zorg ervoor dat tooclick **opslaan** voordat u doorgaat.</span><span class="sxs-lookup"><span data-stu-id="439b7-124">Make sure tooclick **Save** before moving on.</span></span>

> [!NOTE]
> <span data-ttu-id="439b7-125">Wanneer u maakt een toepassing met behulp [https://apps.dev.microsoft.com/?deeplink=/appList](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), Hallo toepassing wordt geregistreerd in thuis Hallo-tenant van Hallo-account dat u toosign bij Hallo-portal.</span><span class="sxs-lookup"><span data-stu-id="439b7-125">When you create an application using [https://apps.dev.microsoft.com/?deeplink=/appList](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), hello application will be registered in hello home tenant of hello account that you use toosign into hello portal.</span></span>  <span data-ttu-id="439b7-126">Dit betekent dat u een toepassing in uw Azure AD-tenant met behulp van een persoonlijk Microsoft-account niet kunt registreren.</span><span class="sxs-lookup"><span data-stu-id="439b7-126">This means that you can not register an application in your Azure AD tenant using a personal Microsoft account.</span></span>  <span data-ttu-id="439b7-127">Als u expliciet tooregister een toepassing in een bepaalde tenant wenst, aanmelden met een account die oorspronkelijk is gemaakt in deze tenant.</span><span class="sxs-lookup"><span data-stu-id="439b7-127">If you explicitly wish tooregister an application in a particular tenant, sign in with an account originally created in that tenant.</span></span>
> 
> 

## <a name="build-a-quick-start-app"></a><span data-ttu-id="439b7-128">Een App snel starten</span><span class="sxs-lookup"><span data-stu-id="439b7-128">Build a quick start app</span></span>
<span data-ttu-id="439b7-129">Nu dat u een Microsoft-app hebt, kunt u een van onze v2.0 snel starten-zelfstudie te voltooien.</span><span class="sxs-lookup"><span data-stu-id="439b7-129">Now that you have a Microsoft app, you can complete one of our v2.0 quick start tutorials.</span></span>  <span data-ttu-id="439b7-130">Hier volgen enkele aanbevelingen:</span><span class="sxs-lookup"><span data-stu-id="439b7-130">Here are a few recommendations:</span></span>

[!INCLUDE [active-directory-v2-quickstart-table](../../../includes/active-directory-v2-quickstart-table.md)]


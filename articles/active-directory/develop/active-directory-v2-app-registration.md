---
title: Een toepassing registreren met het Azure AD v2.0-eindpunt met de portal | Microsoft Docs
description: Het registreren van een app met Microsoft voor het inschakelen aanmelden en toegang tot Microsoft-services met behulp van het v2.0-eindpunt
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
ms.openlocfilehash: e6202aa8665c906382666fe08a561421e50e0a8d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-register-an-app-with-the-v20-endpoint"></a><span data-ttu-id="3f696-103">Het registreren van een app met het v2.0-eindpunt</span><span class="sxs-lookup"><span data-stu-id="3f696-103">How to register an app with the v2.0 endpoint</span></span>
<span data-ttu-id="3f696-104">Als u wilt maken van een app die zowel MSA & Azure AD accepteert aanmelden, u moet eerst een app registreren bij Microsoft.</span><span class="sxs-lookup"><span data-stu-id="3f696-104">To build an app that accepts both MSA & Azure AD sign-in, you'll first need to register an app with Microsoft.</span></span>  <span data-ttu-id="3f696-105">Op dit moment niet mogelijk om eventuele bestaande apps u met Azure AD hebt wellicht te gebruiken of MSA - u moet een geheel nieuwe maken.</span><span class="sxs-lookup"><span data-stu-id="3f696-105">At this time, you won't be able to use any existing apps you may have with Azure AD or MSA - you'll need to create a brand new one.</span></span>

> [!NOTE]
> <span data-ttu-id="3f696-106">Niet alle Azure Active Directory-scenario's en functies worden ondersteund door het v2.0-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="3f696-106">Not all Azure Active Directory scenarios & features are supported by the v2.0 endpoint.</span></span>  <span data-ttu-id="3f696-107">Meer informatie over om te bepalen of moet u het v2.0-eindpunt, [v2.0 beperkingen](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="3f696-107">To determine if you should use the v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 
> 

## <a name="visit-the-microsoft-app-registration-portal"></a><span data-ttu-id="3f696-108">Ga naar de Microsoft app-registratieportal</span><span class="sxs-lookup"><span data-stu-id="3f696-108">Visit the Microsoft app registration portal</span></span>
<span data-ttu-id="3f696-109">Eerste dingen-: Ga naar [https://apps.dev.microsoft.com/?deeplink=/appList](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList).</span><span class="sxs-lookup"><span data-stu-id="3f696-109">First things first - navigate to [https://apps.dev.microsoft.com/?deeplink=/appList](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList).</span></span>  <span data-ttu-id="3f696-110">Dit is een nieuwe app-portal voor wachtwoordregistratie waar u uw Microsoft-apps kunt beheren.</span><span class="sxs-lookup"><span data-stu-id="3f696-110">This is a new app registration portal where you can manage your Microsoft apps.</span></span>

<span data-ttu-id="3f696-111">Meld u aan met ofwel een persoonlijke of werk of school Microsoft-account.</span><span class="sxs-lookup"><span data-stu-id="3f696-111">Sign in with either a personal or work or school Microsoft account.</span></span>  <span data-ttu-id="3f696-112">Als u geen ofwel hebt, moet u zich aanmelden voor een nieuw persoonlijk account.</span><span class="sxs-lookup"><span data-stu-id="3f696-112">If you don't have either, sign up for a new personal account.</span></span> <span data-ttu-id="3f696-113">Opwekken, won't duurt lang - wij hier wachten.</span><span class="sxs-lookup"><span data-stu-id="3f696-113">Go ahead, it won't take long - we'll wait here.</span></span>

<span data-ttu-id="3f696-114">Uitgevoerd?</span><span class="sxs-lookup"><span data-stu-id="3f696-114">Done?</span></span> <span data-ttu-id="3f696-115">U moet nu worden kijken naar de lijst met Microsoft-apps, die waarschijnlijk leeg is.</span><span class="sxs-lookup"><span data-stu-id="3f696-115">You should now be looking at your list of Microsoft apps, which is probably empty.</span></span>  <span data-ttu-id="3f696-116">Hiermee kunt wijzigen.</span><span class="sxs-lookup"><span data-stu-id="3f696-116">Let's change that.</span></span>

<span data-ttu-id="3f696-117">Klik op **een app toevoegen**, en een naam geven.</span><span class="sxs-lookup"><span data-stu-id="3f696-117">Click **Add an app**, and give it a name.</span></span>  <span data-ttu-id="3f696-118">De portal toewijzen uw app een globally unique identifier toepassings-Id die u later in uw code.</span><span class="sxs-lookup"><span data-stu-id="3f696-118">The portal will assign your app a globally unique  Application Id that you'll use later in your code.</span></span>  <span data-ttu-id="3f696-119">Als uw app een serverzijde-onderdeel bevat dat toegangstokens moet voor aanroepen API's (denkt: Office, Azure of uw eigen web-API), moet u maken een **Toepassingsgeheim** hier ook.</span><span class="sxs-lookup"><span data-stu-id="3f696-119">If your app includes a server-side component that needs access tokens for calling APIs (think: Office, Azure, or your own web API), you'll want to create an **Application Secret** here as well.</span></span>

<span data-ttu-id="3f696-120">Voeg vervolgens de Platforms die uw app wilt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="3f696-120">Next, add the Platforms that your app will use.</span></span>

* <span data-ttu-id="3f696-121">Voor op basis van web-apps, geeft u een **omleidings-URI** waar aanmelden berichten kunnen worden verzonden.</span><span class="sxs-lookup"><span data-stu-id="3f696-121">For web based apps, provide a **Redirect URI** where sign-in messages can be sent.</span></span>
* <span data-ttu-id="3f696-122">Noteer de standaard voor mobiele apps omleidings-uri die automatisch voor u gemaakt.</span><span class="sxs-lookup"><span data-stu-id="3f696-122">For mobile apps, copy down the default redirect uri automatically created for you.</span></span>

<span data-ttu-id="3f696-123">U kunt desgewenst het uiterlijk van de aanmeldingspagina in de sectie profiel aanpassen.</span><span class="sxs-lookup"><span data-stu-id="3f696-123">Optionally, you can customize the look and feel of your sign-in page in the Profile section.</span></span>  <span data-ttu-id="3f696-124">Zorg ervoor dat u **opslaan** voordat u doorgaat.</span><span class="sxs-lookup"><span data-stu-id="3f696-124">Make sure to click **Save** before moving on.</span></span>

> [!NOTE]
> <span data-ttu-id="3f696-125">Wanneer u maakt een toepassing met behulp [https://apps.dev.microsoft.com/?deeplink=/appList](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), de toepassing wordt geregistreerd in de oorspronkelijke tenant van het account waarmee u zich aanmeldt bij de portal.</span><span class="sxs-lookup"><span data-stu-id="3f696-125">When you create an application using [https://apps.dev.microsoft.com/?deeplink=/appList](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), the application will be registered in the home tenant of the account that you use to sign into the portal.</span></span>  <span data-ttu-id="3f696-126">Dit betekent dat u een toepassing in uw Azure AD-tenant met behulp van een persoonlijk Microsoft-account niet kunt registreren.</span><span class="sxs-lookup"><span data-stu-id="3f696-126">This means that you can not register an application in your Azure AD tenant using a personal Microsoft account.</span></span>  <span data-ttu-id="3f696-127">Als u expliciet een toepassing in een bepaalde tenant te registreren, aanmelden met een account die oorspronkelijk is gemaakt in deze tenant.</span><span class="sxs-lookup"><span data-stu-id="3f696-127">If you explicitly wish to register an application in a particular tenant, sign in with an account originally created in that tenant.</span></span>
> 
> 

## <a name="build-a-quick-start-app"></a><span data-ttu-id="3f696-128">Een App snel starten</span><span class="sxs-lookup"><span data-stu-id="3f696-128">Build a quick start app</span></span>
<span data-ttu-id="3f696-129">Nu dat u een Microsoft-app hebt, kunt u een van onze v2.0 snel starten-zelfstudie te voltooien.</span><span class="sxs-lookup"><span data-stu-id="3f696-129">Now that you have a Microsoft app, you can complete one of our v2.0 quick start tutorials.</span></span>  <span data-ttu-id="3f696-130">Hier volgen enkele aanbevelingen:</span><span class="sxs-lookup"><span data-stu-id="3f696-130">Here are a few recommendations:</span></span>

[!INCLUDE [active-directory-v2-quickstart-table](../../../includes/active-directory-v2-quickstart-table.md)]


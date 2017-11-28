---
title: aaaLearn over verificatie in twee stappen in de Azure MFA | Microsoft Docs
description: 'Wat is Azure multi-factor Authentication, MFA, meer informatie over Hallo multi-factor Authentication-client en de verschillende methoden Hallo en versies die beschikbaar zijn waarom gebruiken. '
keywords: Inleiding tooMFA mfa overzicht, wat is mfa
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: c40d7a34-1274-4496-96b0-784850c06e9b
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/03/2017
ms.author: kgremban
ms.openlocfilehash: a91b8d6941d2b6ce72a789a97c57e10e594e7ada
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-multi-factor-authentication"></a><span data-ttu-id="ffc1c-104">Wat is Azure Multi-Factor Authentication?</span><span class="sxs-lookup"><span data-stu-id="ffc1c-104">What is Azure Multi-Factor Authentication?</span></span>
<span data-ttu-id="ffc1c-105">Verificatie in twee stappen is een authenticatiemethode die meer dan één verificatiemethode is vereist en voegt een cruciale tweede beveiligingslaag van beveiliging toouser aanmeldingen en transacties.</span><span class="sxs-lookup"><span data-stu-id="ffc1c-105">Two-step verification is a method of authentication that requires more than one verification method and adds a critical second layer of security toouser sign-ins and transactions.</span></span> <span data-ttu-id="ffc1c-106">Het werkt door te vereisen van twee of meer van Hallo verificatiemethoden te volgen:</span><span class="sxs-lookup"><span data-stu-id="ffc1c-106">It works by requiring any two or more of hello following verification methods:</span></span>

* <span data-ttu-id="ffc1c-107">Iets u weet (doorgaans een wachtwoord)</span><span class="sxs-lookup"><span data-stu-id="ffc1c-107">Something you know (typically a password)</span></span>
* <span data-ttu-id="ffc1c-108">Iets er (een vertrouwd apparaat die niet eenvoudig wordt gedupliceerd, zoals een telefoon)</span><span class="sxs-lookup"><span data-stu-id="ffc1c-108">Something you have (a trusted device that is not easily duplicated, like a phone)</span></span>
* <span data-ttu-id="ffc1c-109">Iets dat u (biometrie)</span><span class="sxs-lookup"><span data-stu-id="ffc1c-109">Something you are (biometrics)</span></span>

<span data-ttu-id="ffc1c-110"><center>![Gebruikersnaam en wachtwoord](./media/multi-factor-authentication/pword.png) &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ![certificaten](./media/multi-factor-authentication/phone.png) &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ![Smart Phone](./media/multi-factor-authentication/hware.png) &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ![smartcard](./media/multi-factor-authentication/smart.png) &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ![virtuele smartcard](./media/multi-factor-authentication/vsmart.png) &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ![gebruikersnaam en wachtwoord](./media/multi-factor-authentication/cert.png)</center></span><span class="sxs-lookup"><span data-stu-id="ffc1c-110"><center>![Username and Password](./media/multi-factor-authentication/pword.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Certificates](./media/multi-factor-authentication/phone.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Smart Phone](./media/multi-factor-authentication/hware.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Smart Card](./media/multi-factor-authentication/smart.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Virtual Smart Card](./media/multi-factor-authentication/vsmart.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Username and Password](./media/multi-factor-authentication/cert.png)</center></span></span>

<span data-ttu-id="ffc1c-111">Azure Multi-Factor Authentication (MFA) is een Microsoft-oplossing voor verificatie in twee stappen.</span><span class="sxs-lookup"><span data-stu-id="ffc1c-111">Azure Multi-Factor Authentication (MFA) is Microsoft's two-step verification solution.</span></span> <span data-ttu-id="ffc1c-112">Azure MFA helpt beveiliging toegang toodata en toepassingen en te voldoen aan de behoeften van de gebruiker voor een eenvoudig proces aanmelden.</span><span class="sxs-lookup"><span data-stu-id="ffc1c-112">Azure MFA helps safeguard access toodata and applications while meeting user demand for a simple sign-in process.</span></span> <span data-ttu-id="ffc1c-113">Het biedt krachtige verificatie via een reeks verificatiemethoden waaronder verificatie per telefoon, sms of mobiele app.</span><span class="sxs-lookup"><span data-stu-id="ffc1c-113">It delivers strong authentication via a range of verification methods, including phone call, text message, or mobile app verification.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/WA-MFA-Overview/player]
>
>

## <a name="why-use-azure-multi-factor-authentication"></a><span data-ttu-id="ffc1c-114">Waarom Azure multi-factor Authentication gebruiken?</span><span class="sxs-lookup"><span data-stu-id="ffc1c-114">Why use Azure Multi-Factor Authentication?</span></span>
<span data-ttu-id="ffc1c-115">Vandaag de dag, meer dan ooit, zijn er steeds meer mensen verbonden.</span><span class="sxs-lookup"><span data-stu-id="ffc1c-115">Today, more than ever, people are increasingly connected.</span></span> <span data-ttu-id="ffc1c-116">Met slim telefoons, tablets, laptops en pc's hebben mensen verschillende opties op hoe ze tooconnect gaat en blijf op elk gewenst moment.</span><span class="sxs-lookup"><span data-stu-id="ffc1c-116">With smart phones, tablets, laptops, and PCs, people have several different options on how they are going tooconnect and stay connected at any time.</span></span> <span data-ttu-id="ffc1c-117">Gebruikers hebben toegang tot hun accounts en toepassingen vanaf elke locatie, wat betekent dat ze kunnen meer werk gedaan te krijgen en hun klanten fungeren beter.</span><span class="sxs-lookup"><span data-stu-id="ffc1c-117">People can access their accounts and applications from anywhere, which means that they can get more work done and serve their customers better.</span></span>

<span data-ttu-id="ffc1c-118">Azure multi-factor Authentication is een eenvoudig toouse, schaalbare en betrouwbare oplossing die biedt een tweede methode voor verificatie zodat uw gebruikers zijn altijd is beveiligd.</span><span class="sxs-lookup"><span data-stu-id="ffc1c-118">Azure Multi-Factor Authentication is an easy toouse, scalable, and reliable solution that provides a second method of authentication so your users are always protected.</span></span>

| ![Eenvoudig tooUse](./media/multi-factor-authentication/simple.png) | ![Schaalbaar](./media/multi-factor-authentication/scalable.png) | ![Altijd is beveiligd](./media/multi-factor-authentication/protected.png) | ![Betrouwbaar](./media/multi-factor-authentication/reliable.png) |
|:---:|:---:|:---:|:---:|
| <span data-ttu-id="ffc1c-123">**Eenvoudig toouse**</span><span class="sxs-lookup"><span data-stu-id="ffc1c-123">**Easy toouse**</span></span> |<span data-ttu-id="ffc1c-124">**Schaalbare**</span><span class="sxs-lookup"><span data-stu-id="ffc1c-124">**Scalable**</span></span> |<span data-ttu-id="ffc1c-125">**Altijd is beveiligd**</span><span class="sxs-lookup"><span data-stu-id="ffc1c-125">**Always Protected**</span></span> |<span data-ttu-id="ffc1c-126">**Betrouwbare**</span><span class="sxs-lookup"><span data-stu-id="ffc1c-126">**Reliable**</span></span> |

* <span data-ttu-id="ffc1c-127">**Eenvoudig tooUse** -Azure multi-factor Authentication is eenvoudig tooset up en gebruiken.</span><span class="sxs-lookup"><span data-stu-id="ffc1c-127">**Easy tooUse** - Azure Multi-Factor Authentication is simple tooset up and use.</span></span> <span data-ttu-id="ffc1c-128">Hallo kunt extra beveiliging die wordt geleverd met Azure multi-factor Authentication toomanage gebruikers hun eigen apparaten.</span><span class="sxs-lookup"><span data-stu-id="ffc1c-128">hello extra protection that comes with Azure Multi-Factor Authentication allows users toomanage their own devices.</span></span> <span data-ttu-id="ffc1c-129">Beste van alle in veel gevallen deze kan worden ingesteld met een paar eenvoudige klikken.</span><span class="sxs-lookup"><span data-stu-id="ffc1c-129">Best of all, in many instances it can be set up with just a few simple clicks.</span></span>
* <span data-ttu-id="ffc1c-130">**Schaalbare** -Azure multi-factor Authentication Hallo power van Hallo cloud gebruikt en kan worden geïntegreerd met uw on-premises AD en aangepaste apps.</span><span class="sxs-lookup"><span data-stu-id="ffc1c-130">**Scalable** - Azure Multi-Factor Authentication uses hello power of hello cloud and integrates with your on-premises AD and custom apps.</span></span> <span data-ttu-id="ffc1c-131">Deze beveiliging is zelfs uitgebreid tooyour hoog volume essentiële scenario's.</span><span class="sxs-lookup"><span data-stu-id="ffc1c-131">This protection is even extended tooyour high-volume, mission-critical scenarios.</span></span>
* <span data-ttu-id="ffc1c-132">**Altijd is beveiligd** -Azure multi-factor Authentication sterke verificatie met behulp van de hoogste industrienormen Hallo biedt.</span><span class="sxs-lookup"><span data-stu-id="ffc1c-132">**Always Protected** - Azure Multi-Factor Authentication provides strong authentication using hello highest industry standards.</span></span>
* <span data-ttu-id="ffc1c-133">**Betrouwbare** -wordt gegarandeerd dat de beschikbaarheid van 99,9% van de Azure multi-factor Authentication.</span><span class="sxs-lookup"><span data-stu-id="ffc1c-133">**Reliable** - We guarantee 99.9% availability of Azure Multi-Factor Authentication.</span></span> <span data-ttu-id="ffc1c-134">Hallo service wordt beschouwd als niet beschikbaar wanneer geen verzoeken voor de verificatie in twee stappen Hallo tooreceive of proces.</span><span class="sxs-lookup"><span data-stu-id="ffc1c-134">hello service is considered unavailable when it is unable tooreceive or process verification requests for hello two-step verification.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Windows-Azure-Multi-Factor-Authentication/player]


## <a name="next-steps"></a><span data-ttu-id="ffc1c-135">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="ffc1c-135">Next steps</span></span>

- <span data-ttu-id="ffc1c-136">Meer informatie over [de werking van Azure multi-factor Authentication](multi-factor-authentication-how-it-works.md)</span><span class="sxs-lookup"><span data-stu-id="ffc1c-136">Learn about [how Azure Multi-Factor Authentication works](multi-factor-authentication-how-it-works.md)</span></span>

- <span data-ttu-id="ffc1c-137">Meer informatie over andere Hallo [versies en verbruikmethoden voor Azure multi-factor Authentication](multi-factor-authentication-versions-plans.md)</span><span class="sxs-lookup"><span data-stu-id="ffc1c-137">Read about hello different [versions and consumption methods for Azure Multi-Factor Authentication](multi-factor-authentication-versions-plans.md)</span></span>

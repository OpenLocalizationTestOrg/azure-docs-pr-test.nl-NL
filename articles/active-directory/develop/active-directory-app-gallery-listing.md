---
title: aaaListing uw toepassing in hello Azure Active Directory-toepassingsgalerie
description: Hoe toolist een toepassing die ondersteuning biedt voor eenmalige aanmelding in Azure Active Directory-galerie Hallo | Microsoft Azure
services: active-directory
documentationcenter: dev-center-name
author: bryanla
manager: mbaldwin
editor: 
ms.assetid: 820acdb7-d316-4c3b-8de9-79df48ba3b06
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/27/2017
ms.author: bryanla
ms.custom: aaddev
ms.openlocfilehash: 09ccd3b4645a180059b9a9d502e39f1b8933c988
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="listing-your-application-in-hello-azure-active-directory-application-gallery"></a><span data-ttu-id="6ff1d-103">Uw toepassing in Azure Active Directory-toepassingsgalerie Hallo aanbieding</span><span class="sxs-lookup"><span data-stu-id="6ff1d-103">Listing your application in hello Azure Active Directory application gallery</span></span>
<span data-ttu-id="6ff1d-104">een toepassing die ondersteuning biedt voor eenmalige aanmelding bij Azure Active Directory in Hallo toolist [galerie van Azure AD](https://azure.microsoft.com/marketplace/active-directory/all/), Hallo toepassing moet eerst tooimplement Hallo integratie modi te volgen:</span><span class="sxs-lookup"><span data-stu-id="6ff1d-104">toolist an application that supports single sign-on with Azure Active Directory in hello [Azure AD gallery](https://azure.microsoft.com/marketplace/active-directory/all/), hello application first needs tooimplement one of hello following integration modes:</span></span>

* <span data-ttu-id="6ff1d-105">**OpenID Connect** - directe integratie met Azure AD met OpenID Connect voor verificatie en Azure AD toestemming API voor configuratie Hallo.</span><span class="sxs-lookup"><span data-stu-id="6ff1d-105">**OpenID Connect** - Direct integration with Azure AD using OpenID Connect for authentication and hello Azure AD consent API for configuration.</span></span> <span data-ttu-id="6ff1d-106">Als u een integratie net begint en SAML biedt geen ondersteuning voor uw toepassing, is dit Hallo aanbevolen modus.</span><span class="sxs-lookup"><span data-stu-id="6ff1d-106">If you are just starting an integration and your application does not support SAML, then this is hello recommend mode.</span></span>
* <span data-ttu-id="6ff1d-107">**SAML** – de toepassing al heeft Hallo mogelijkheid tooconfigure van derden id-providers met Hallo SAML-protocol.</span><span class="sxs-lookup"><span data-stu-id="6ff1d-107">**SAML** – Your application already has hello ability tooconfigure third-party identity providers using hello SAML protocol.</span></span>

<span data-ttu-id="6ff1d-108">Aanbieding-vereisten voor elke fase zijn hieronder.</span><span class="sxs-lookup"><span data-stu-id="6ff1d-108">Listing requirements for each mode are below.</span></span>

## <a name="openid-connect-integration"></a><span data-ttu-id="6ff1d-109">OpenID Connect-integratie</span><span class="sxs-lookup"><span data-stu-id="6ff1d-109">OpenID Connect Integration</span></span>
<span data-ttu-id="6ff1d-110">toointegrate uw toepassing met Azure AD, volgende Hallo [developer instructies](active-directory-authentication-scenarios.md).</span><span class="sxs-lookup"><span data-stu-id="6ff1d-110">toointegrate your application with Azure AD, following hello [developer instructions](active-directory-authentication-scenarios.md).</span></span> <span data-ttu-id="6ff1d-111">Vervolgens voltooien Hallo onderstaande vragen en te verzenden toowaadpartners@microsoft.com.</span><span class="sxs-lookup"><span data-stu-id="6ff1d-111">Then complete hello questions below and send toowaadpartners@microsoft.com.</span></span>

* <span data-ttu-id="6ff1d-112">Geef referenties voor een testtenant of een account met de toepassing die kan worden gebruikt door hello Azure AD-team tootest Hallo-integratie.</span><span class="sxs-lookup"><span data-stu-id="6ff1d-112">Provide credentials for a test tenant or account with your application that can be used by hello Azure AD team tootest hello integration.</span></span>  
* <span data-ttu-id="6ff1d-113">Bieden instructies over hoe hello Azure AD-team kunt aanmelden en verbinding maken met een exemplaar van Azure AD tooyour toepassing hello met [Azure AD toestemming framework](active-directory-integrating-applications.md#overview-of-the-consent-framework).</span><span class="sxs-lookup"><span data-stu-id="6ff1d-113">Provide instructions on how hello Azure AD team can sign in and connect an instance of Azure AD tooyour application using hello [Azure AD consent framework](active-directory-integrating-applications.md#overview-of-the-consent-framework).</span></span> 
* <span data-ttu-id="6ff1d-114">Geef eventuele verdere instructies nodig zijn voor hello Azure AD in een team tootest eenmalige aanmelding met uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="6ff1d-114">Provide any further instructions required for hello Azure AD team tootest single sign-on with your application.</span></span> 
* <span data-ttu-id="6ff1d-115">Geef Hallo gegevens hieronder:</span><span class="sxs-lookup"><span data-stu-id="6ff1d-115">Provide hello info below:</span></span>

> <span data-ttu-id="6ff1d-116">Bedrijfsnaam:</span><span class="sxs-lookup"><span data-stu-id="6ff1d-116">Company Name:</span></span>
> 
> <span data-ttu-id="6ff1d-117">De Website van het bedrijf:</span><span class="sxs-lookup"><span data-stu-id="6ff1d-117">Company Website:</span></span>
> 
> <span data-ttu-id="6ff1d-118">De naam van de toepassing:</span><span class="sxs-lookup"><span data-stu-id="6ff1d-118">Application Name:</span></span>
> 
> <span data-ttu-id="6ff1d-119">Beschrijving van de toepassing (maximaal 200 tekens):</span><span class="sxs-lookup"><span data-stu-id="6ff1d-119">Application Description (200 character limit):</span></span>
> 
> <span data-ttu-id="6ff1d-120">De Website van de toepassing is (informatief):</span><span class="sxs-lookup"><span data-stu-id="6ff1d-120">Application Website (informational):</span></span>
> 
> <span data-ttu-id="6ff1d-121">Website van de toepassing technische ondersteuning of contactgegevens:</span><span class="sxs-lookup"><span data-stu-id="6ff1d-121">Application Technical Support Website or Contact Info:</span></span>
> 
> <span data-ttu-id="6ff1d-122">ID van Hallo toepassing, zoals wordt weergegeven in Hallo App-details https://portal.azure.com:</span><span class="sxs-lookup"><span data-stu-id="6ff1d-122">Application  ID of hello application, as shown in hello application details at https://portal.azure.com:</span></span>
> 
> <span data-ttu-id="6ff1d-123">Wanneer klanten gaat toosign voor de URL van de toepassing aanmelden en/of kopen Hallo toepassing:</span><span class="sxs-lookup"><span data-stu-id="6ff1d-123">Application Sign-Up URL where customers go toosign up for and /or purchase hello application:</span></span>
> 
> <span data-ttu-id="6ff1d-124">Kies toothree categorieën voor uw toepassing toobe vermeld in (voor beschikbare categorieën Zie hello Azure Active Directory Marketplace):</span><span class="sxs-lookup"><span data-stu-id="6ff1d-124">Choose up toothree categories for your application toobe listed under (for available categories see hello Azure Active Directory Marketplace):</span></span>
> 
> <span data-ttu-id="6ff1d-125">Kleine pictogrammen van toepassing (PNG-bestand, 45px door 45px, effen achtergrondkleur) koppelen:</span><span class="sxs-lookup"><span data-stu-id="6ff1d-125">Attach Application Small Icon (PNG file, 45px by 45px, solid background color):</span></span>
> 
> <span data-ttu-id="6ff1d-126">Koppelen met grote pictogrammen van toepassing (PNG-bestand, 215px door 215px, effen achtergrondkleur):</span><span class="sxs-lookup"><span data-stu-id="6ff1d-126">Attach Application Large Icon (PNG file, 215px by 215px, solid background color):</span></span>
> 
> <span data-ttu-id="6ff1d-127">Logo van de toepassing (PNG-bestand, 150px door 122px, transparante achtergrondkleur) koppelen:</span><span class="sxs-lookup"><span data-stu-id="6ff1d-127">Attach Application Logo (PNG file, 150px by 122px, transparent background color):</span></span>
> 
> 

## <a name="saml-integration"></a><span data-ttu-id="6ff1d-128">SAML-integratie</span><span class="sxs-lookup"><span data-stu-id="6ff1d-128">SAML Integration</span></span>
<span data-ttu-id="6ff1d-129">Alle Apps die ondersteuning biedt voor SAML 2.0 kan rechtstreeks worden geïntegreerd met een Azure AD-tenant met behulp van [deze tooadd instructies een aangepaste toepassing](../active-directory-saas-custom-apps.md).</span><span class="sxs-lookup"><span data-stu-id="6ff1d-129">Any app that supports SAML 2.0 can be integrated directly with an Azure AD tenant using [these instructions tooadd a custom application](../active-directory-saas-custom-apps.md).</span></span> <span data-ttu-id="6ff1d-130">Nadat u hebt getest dat de integratie van uw toepassingen met Azure AD werkt, Hallo volgende informatie te verzenden<mailto:waadpartners@microsoft.com>.</span><span class="sxs-lookup"><span data-stu-id="6ff1d-130">Once you have tested that your application integration works with Azure AD, send hello following information too<mailto:waadpartners@microsoft.com>.</span></span>

* <span data-ttu-id="6ff1d-131">Geef referenties voor een testtenant of een account met de toepassing die kan worden gebruikt door hello Azure AD-team tootest Hallo-integratie.</span><span class="sxs-lookup"><span data-stu-id="6ff1d-131">Provide credentials for a test tenant or account with your application that can be used by hello Azure AD team tootest hello integration.</span></span>  
* <span data-ttu-id="6ff1d-132">Geef Hallo SAML aanmeldings-URL, URL-verlener (entiteit-ID) en antwoord-URL (assertion consumer-service)-waarden voor uw toepassing, zoals wordt beschreven [hier](../active-directory-saas-custom-apps.md).</span><span class="sxs-lookup"><span data-stu-id="6ff1d-132">Provide hello SAML Sign-On URL, Issuer URL (entity ID), and Reply URL (assertion consumer service) values for your application, as described [here](../active-directory-saas-custom-apps.md).</span></span> <span data-ttu-id="6ff1d-133">Als u doorgaans deze waarden als onderdeel van een metagegevensbestand SAML opgeeft, klikt u vervolgens kunt u sturen die ook.</span><span class="sxs-lookup"><span data-stu-id="6ff1d-133">If you typically provide these values as part of a SAML metadata file, then please send that as well.</span></span>
* <span data-ttu-id="6ff1d-134">Geef een korte beschrijving van hoe tooconfigure Azure AD als een id-provider in uw toepassing met behulp van SAML 2.0.</span><span class="sxs-lookup"><span data-stu-id="6ff1d-134">Provide a brief description of how tooconfigure Azure AD as an identity provider in your application using SAML 2.0.</span></span> <span data-ttu-id="6ff1d-135">Als uw toepassing het configureren van de Azure AD als een id-provider door middel van een administratieve selfserviceportal ondersteunt, vervolgens Controleer Hallo referenties bovenstaande omvatten Hallo mogelijkheid tooset dit up.</span><span class="sxs-lookup"><span data-stu-id="6ff1d-135">If your application supports configuring Azure AD as an identity provider through a self-service administrative portal, then please ensure hello credentials provided above include hello ability tooset this up.</span></span>
* <span data-ttu-id="6ff1d-136">Geef Hallo gegevens hieronder:</span><span class="sxs-lookup"><span data-stu-id="6ff1d-136">Provide hello info below:</span></span>

> <span data-ttu-id="6ff1d-137">Bedrijfsnaam:</span><span class="sxs-lookup"><span data-stu-id="6ff1d-137">Company Name:</span></span>
> 
> <span data-ttu-id="6ff1d-138">De Website van het bedrijf:</span><span class="sxs-lookup"><span data-stu-id="6ff1d-138">Company Website:</span></span>
> 
> <span data-ttu-id="6ff1d-139">De naam van de toepassing:</span><span class="sxs-lookup"><span data-stu-id="6ff1d-139">Application Name:</span></span>
> 
> <span data-ttu-id="6ff1d-140">Beschrijving van de toepassing (maximaal 200 tekens):</span><span class="sxs-lookup"><span data-stu-id="6ff1d-140">Application Description (200 character limit):</span></span>
> 
> <span data-ttu-id="6ff1d-141">De Website van de toepassing is (informatief):</span><span class="sxs-lookup"><span data-stu-id="6ff1d-141">Application Website (informational):</span></span>
> 
> <span data-ttu-id="6ff1d-142">Website van de toepassing technische ondersteuning of contactgegevens:</span><span class="sxs-lookup"><span data-stu-id="6ff1d-142">Application Technical Support Website or Contact Info:</span></span>
> 
> <span data-ttu-id="6ff1d-143">Wanneer klanten gaat toosign voor de URL van de toepassing aanmelden en/of kopen Hallo toepassing:</span><span class="sxs-lookup"><span data-stu-id="6ff1d-143">Application Sign-Up URL where customers go toosign up for and /or purchase hello application:</span></span>
> 
> <span data-ttu-id="6ff1d-144">Kies maximaal toothree categorieën voor uw toepassing toobe vermeld onder (voor beschikbare categorieën Zie Hallo [Azure Active Directory Marketplace](https://azure.microsoft.com/marketplace/active-directory/))):</span><span class="sxs-lookup"><span data-stu-id="6ff1d-144">Choose up toothree categories for your application toobe listed under (for available categories see hello [Azure Active Directory Marketplace](https://azure.microsoft.com/marketplace/active-directory/))):</span></span>
> 
> <span data-ttu-id="6ff1d-145">Kleine pictogrammen van toepassing (PNG-bestand, 45px door 45px, effen achtergrondkleur) koppelen:</span><span class="sxs-lookup"><span data-stu-id="6ff1d-145">Attach Application Small Icon (PNG file, 45px by 45px, solid background color):</span></span>
> 
> <span data-ttu-id="6ff1d-146">Koppelen met grote pictogrammen van toepassing (PNG-bestand, 215px door 215px, effen achtergrondkleur):</span><span class="sxs-lookup"><span data-stu-id="6ff1d-146">Attach Application Large Icon (PNG file, 215px by 215px, solid background color):</span></span>
> 
> <span data-ttu-id="6ff1d-147">Logo van de toepassing (PNG-bestand, 150px door 122px, transparante achtergrondkleur) koppelen:</span><span class="sxs-lookup"><span data-stu-id="6ff1d-147">Attach Application Logo (PNG file, 150px by 122px, transparent background color):</span></span>
> 
> 


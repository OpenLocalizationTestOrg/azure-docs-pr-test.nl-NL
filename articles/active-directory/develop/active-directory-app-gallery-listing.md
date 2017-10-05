---
title: Lijst van uw toepassing in de Azure Active Directory-toepassingsgalerie
description: Hoe u een toepassing die ondersteuning biedt voor eenmalige aanmelding in de galerie van Azure Active Directory | Microsoft Azure
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
ms.openlocfilehash: cf25772bd9d92b59401aa5da76e6bbd5fa5ee3e5
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="listing-your-application-in-the-azure-active-directory-application-gallery"></a><span data-ttu-id="3432f-103">Lijst van uw toepassing in de Azure Active Directory-toepassingsgalerie</span><span class="sxs-lookup"><span data-stu-id="3432f-103">Listing your application in the Azure Active Directory application gallery</span></span>
<span data-ttu-id="3432f-104">Voor een lijst met een toepassing die ondersteuning biedt voor eenmalige aanmelding bij Azure Active Directory in de [galerie van Azure AD](https://azure.microsoft.com/marketplace/active-directory/all/), moet eerst de toepassing voor het implementeren van een van de volgende integratie-modi:</span><span class="sxs-lookup"><span data-stu-id="3432f-104">To list an application that supports single sign-on with Azure Active Directory in the [Azure AD gallery](https://azure.microsoft.com/marketplace/active-directory/all/), the application first needs to implement one of the following integration modes:</span></span>

* <span data-ttu-id="3432f-105">**OpenID Connect** -directe integratie met Azure AD met OpenID Connect voor verificatie en de Azure AD API toestemming voor configuratie.</span><span class="sxs-lookup"><span data-stu-id="3432f-105">**OpenID Connect** - Direct integration with Azure AD using OpenID Connect for authentication and the Azure AD consent API for configuration.</span></span> <span data-ttu-id="3432f-106">Als u een integratie net begint en SAML biedt geen ondersteuning voor uw toepassing, is dit de aanbevolen modus.</span><span class="sxs-lookup"><span data-stu-id="3432f-106">If you are just starting an integration and your application does not support SAML, then this is the recommend mode.</span></span>
* <span data-ttu-id="3432f-107">**SAML** – de toepassing al heeft de mogelijkheid voor het configureren van derden identiteitsproviders met het SAML-protocol.</span><span class="sxs-lookup"><span data-stu-id="3432f-107">**SAML** – Your application already has the ability to configure third-party identity providers using the SAML protocol.</span></span>

<span data-ttu-id="3432f-108">Aanbieding-vereisten voor elke fase zijn hieronder.</span><span class="sxs-lookup"><span data-stu-id="3432f-108">Listing requirements for each mode are below.</span></span>

## <a name="openid-connect-integration"></a><span data-ttu-id="3432f-109">OpenID Connect-integratie</span><span class="sxs-lookup"><span data-stu-id="3432f-109">OpenID Connect Integration</span></span>
<span data-ttu-id="3432f-110">Uw toepassing integreren met Azure AD, na de [developer instructies](active-directory-authentication-scenarios.md).</span><span class="sxs-lookup"><span data-stu-id="3432f-110">To integrate your application with Azure AD, following the [developer instructions](active-directory-authentication-scenarios.md).</span></span> <span data-ttu-id="3432f-111">Vervolgens voltooien van de onderstaande vragen en verzenden naar waadpartners@microsoft.com.</span><span class="sxs-lookup"><span data-stu-id="3432f-111">Then complete the questions below and send to waadpartners@microsoft.com.</span></span>

* <span data-ttu-id="3432f-112">Geef referenties voor een testtenant of een account met de toepassing die door het team van Azure AD kan worden gebruikt voor het testen van de integratie.</span><span class="sxs-lookup"><span data-stu-id="3432f-112">Provide credentials for a test tenant or account with your application that can be used by the Azure AD team to test the integration.</span></span>  
* <span data-ttu-id="3432f-113">Bieden instructies over hoe het team van Azure AD kunt aanmelden en een instantie van Azure AD verbinden met uw toepassing met de [Azure AD toestemming framework](active-directory-integrating-applications.md#overview-of-the-consent-framework).</span><span class="sxs-lookup"><span data-stu-id="3432f-113">Provide instructions on how the Azure AD team can sign in and connect an instance of Azure AD to your application using the [Azure AD consent framework](active-directory-integrating-applications.md#overview-of-the-consent-framework).</span></span> 
* <span data-ttu-id="3432f-114">Geef eventuele verdere instructies nodig voor het Azure AD-team voor het testen van eenmalige aanmelding met uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="3432f-114">Provide any further instructions required for the Azure AD team to test single sign-on with your application.</span></span> 
* <span data-ttu-id="3432f-115">De onderstaande gegevens bieden:</span><span class="sxs-lookup"><span data-stu-id="3432f-115">Provide the info below:</span></span>

> <span data-ttu-id="3432f-116">Bedrijfsnaam:</span><span class="sxs-lookup"><span data-stu-id="3432f-116">Company Name:</span></span>
> 
> <span data-ttu-id="3432f-117">De Website van het bedrijf:</span><span class="sxs-lookup"><span data-stu-id="3432f-117">Company Website:</span></span>
> 
> <span data-ttu-id="3432f-118">De naam van de toepassing:</span><span class="sxs-lookup"><span data-stu-id="3432f-118">Application Name:</span></span>
> 
> <span data-ttu-id="3432f-119">Beschrijving van de toepassing (maximaal 200 tekens):</span><span class="sxs-lookup"><span data-stu-id="3432f-119">Application Description (200 character limit):</span></span>
> 
> <span data-ttu-id="3432f-120">De Website van de toepassing is (informatief):</span><span class="sxs-lookup"><span data-stu-id="3432f-120">Application Website (informational):</span></span>
> 
> <span data-ttu-id="3432f-121">Website van de toepassing technische ondersteuning of contactgegevens:</span><span class="sxs-lookup"><span data-stu-id="3432f-121">Application Technical Support Website or Contact Info:</span></span>
> 
> <span data-ttu-id="3432f-122">Toepassings-ID van de toepassing, zoals wordt weergegeven in de App-details https://portal.azure.com:</span><span class="sxs-lookup"><span data-stu-id="3432f-122">Application  ID of the application, as shown in the application details at https://portal.azure.com:</span></span>
> 
> <span data-ttu-id="3432f-123">Wanneer klanten gaat u naar zich aanmelden voor de URL van de toepassing aanmelden en/of kopen de toepassing:</span><span class="sxs-lookup"><span data-stu-id="3432f-123">Application Sign-Up URL where customers go to sign up for and /or purchase the application:</span></span>
> 
> <span data-ttu-id="3432f-124">Kies maximaal drie categorieën voor uw toepassing worden vermeld in (voor beschikbare categorieën Zie Azure Active Directory Marketplace):</span><span class="sxs-lookup"><span data-stu-id="3432f-124">Choose up to three categories for your application to be listed under (for available categories see the Azure Active Directory Marketplace):</span></span>
> 
> <span data-ttu-id="3432f-125">Kleine pictogrammen van toepassing (PNG-bestand, 45px door 45px, effen achtergrondkleur) koppelen:</span><span class="sxs-lookup"><span data-stu-id="3432f-125">Attach Application Small Icon (PNG file, 45px by 45px, solid background color):</span></span>
> 
> <span data-ttu-id="3432f-126">Koppelen met grote pictogrammen van toepassing (PNG-bestand, 215px door 215px, effen achtergrondkleur):</span><span class="sxs-lookup"><span data-stu-id="3432f-126">Attach Application Large Icon (PNG file, 215px by 215px, solid background color):</span></span>
> 
> <span data-ttu-id="3432f-127">Logo van de toepassing (PNG-bestand, 150px door 122px, transparante achtergrondkleur) koppelen:</span><span class="sxs-lookup"><span data-stu-id="3432f-127">Attach Application Logo (PNG file, 150px by 122px, transparent background color):</span></span>
> 
> 

## <a name="saml-integration"></a><span data-ttu-id="3432f-128">SAML-integratie</span><span class="sxs-lookup"><span data-stu-id="3432f-128">SAML Integration</span></span>
<span data-ttu-id="3432f-129">Alle Apps die ondersteuning biedt voor SAML 2.0 kan rechtstreeks worden geïntegreerd met een Azure AD-tenant met behulp van [deze instructies voor het toevoegen van een aangepaste toepassing](../active-directory-saas-custom-apps.md).</span><span class="sxs-lookup"><span data-stu-id="3432f-129">Any app that supports SAML 2.0 can be integrated directly with an Azure AD tenant using [these instructions to add a custom application](../active-directory-saas-custom-apps.md).</span></span> <span data-ttu-id="3432f-130">Nadat u hebt getest dat de integratie van uw toepassingen met Azure AD werkt, de volgende informatie om te verzenden < mailto:waadpartners@microsoft.com >.</span><span class="sxs-lookup"><span data-stu-id="3432f-130">Once you have tested that your application integration works with Azure AD, send the following information to <mailto:waadpartners@microsoft.com>.</span></span>

* <span data-ttu-id="3432f-131">Geef referenties voor een testtenant of een account met de toepassing die door het team van Azure AD kan worden gebruikt voor het testen van de integratie.</span><span class="sxs-lookup"><span data-stu-id="3432f-131">Provide credentials for a test tenant or account with your application that can be used by the Azure AD team to test the integration.</span></span>  
* <span data-ttu-id="3432f-132">De SAML aanmeldings-URL, de URL-verlener (entiteit-ID) en de antwoord-URL (assertion consumer-service)-waarden voor uw toepassing bieden, zoals beschreven [hier](../active-directory-saas-custom-apps.md).</span><span class="sxs-lookup"><span data-stu-id="3432f-132">Provide the SAML Sign-On URL, Issuer URL (entity ID), and Reply URL (assertion consumer service) values for your application, as described [here](../active-directory-saas-custom-apps.md).</span></span> <span data-ttu-id="3432f-133">Als u doorgaans deze waarden als onderdeel van een metagegevensbestand SAML opgeeft, klikt u vervolgens kunt u sturen die ook.</span><span class="sxs-lookup"><span data-stu-id="3432f-133">If you typically provide these values as part of a SAML metadata file, then please send that as well.</span></span>
* <span data-ttu-id="3432f-134">Geef een korte beschrijving van hoe u Azure AD configureren als een id-provider in uw toepassing met behulp van SAML 2.0.</span><span class="sxs-lookup"><span data-stu-id="3432f-134">Provide a brief description of how to configure Azure AD as an identity provider in your application using SAML 2.0.</span></span> <span data-ttu-id="3432f-135">Als uw toepassing ondersteuning biedt voor het configureren van de Azure AD als een id-provider door middel van een administratieve selfserviceportal, vervolgens controleert u de hierboven opgegeven referenties zijn de mogelijkheid om in te stellen dit.</span><span class="sxs-lookup"><span data-stu-id="3432f-135">If your application supports configuring Azure AD as an identity provider through a self-service administrative portal, then please ensure the credentials provided above include the ability to set this up.</span></span>
* <span data-ttu-id="3432f-136">De onderstaande gegevens bieden:</span><span class="sxs-lookup"><span data-stu-id="3432f-136">Provide the info below:</span></span>

> <span data-ttu-id="3432f-137">Bedrijfsnaam:</span><span class="sxs-lookup"><span data-stu-id="3432f-137">Company Name:</span></span>
> 
> <span data-ttu-id="3432f-138">De Website van het bedrijf:</span><span class="sxs-lookup"><span data-stu-id="3432f-138">Company Website:</span></span>
> 
> <span data-ttu-id="3432f-139">De naam van de toepassing:</span><span class="sxs-lookup"><span data-stu-id="3432f-139">Application Name:</span></span>
> 
> <span data-ttu-id="3432f-140">Beschrijving van de toepassing (maximaal 200 tekens):</span><span class="sxs-lookup"><span data-stu-id="3432f-140">Application Description (200 character limit):</span></span>
> 
> <span data-ttu-id="3432f-141">De Website van de toepassing is (informatief):</span><span class="sxs-lookup"><span data-stu-id="3432f-141">Application Website (informational):</span></span>
> 
> <span data-ttu-id="3432f-142">Website van de toepassing technische ondersteuning of contactgegevens:</span><span class="sxs-lookup"><span data-stu-id="3432f-142">Application Technical Support Website or Contact Info:</span></span>
> 
> <span data-ttu-id="3432f-143">Wanneer klanten gaat u naar zich aanmelden voor de URL van de toepassing aanmelden en/of kopen de toepassing:</span><span class="sxs-lookup"><span data-stu-id="3432f-143">Application Sign-Up URL where customers go to sign up for and /or purchase the application:</span></span>
> 
> <span data-ttu-id="3432f-144">Kies maximaal drie categorieën voor uw toepassing worden weergegeven onder (voor Zie beschikbare categorieën het [Azure Active Directory Marketplace](https://azure.microsoft.com/marketplace/active-directory/))):</span><span class="sxs-lookup"><span data-stu-id="3432f-144">Choose up to three categories for your application to be listed under (for available categories see the [Azure Active Directory Marketplace](https://azure.microsoft.com/marketplace/active-directory/))):</span></span>
> 
> <span data-ttu-id="3432f-145">Kleine pictogrammen van toepassing (PNG-bestand, 45px door 45px, effen achtergrondkleur) koppelen:</span><span class="sxs-lookup"><span data-stu-id="3432f-145">Attach Application Small Icon (PNG file, 45px by 45px, solid background color):</span></span>
> 
> <span data-ttu-id="3432f-146">Koppelen met grote pictogrammen van toepassing (PNG-bestand, 215px door 215px, effen achtergrondkleur):</span><span class="sxs-lookup"><span data-stu-id="3432f-146">Attach Application Large Icon (PNG file, 215px by 215px, solid background color):</span></span>
> 
> <span data-ttu-id="3432f-147">Logo van de toepassing (PNG-bestand, 150px door 122px, transparante achtergrondkleur) koppelen:</span><span class="sxs-lookup"><span data-stu-id="3432f-147">Attach Application Logo (PNG file, 150px by 122px, transparent background color):</span></span>
> 
> 


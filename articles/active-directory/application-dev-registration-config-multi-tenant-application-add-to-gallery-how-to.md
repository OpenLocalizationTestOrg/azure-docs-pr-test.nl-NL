---
title: Het toevoegen van een toepassing met meerdere tenants naar de galerie van Azure AD-toepassing | Microsoft Docs
description: Legt uit hoe u kunt uw aangepaste ontwikkelde multitenant toepassing weergeven in de Azure AD-Toepassingsgalerie
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 208f0d40bd7a8e8f35f16e1fcb09c305d833dbb2
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-add-a-multi-tenant-application-to-the-azure-ad-application-gallery"></a><span data-ttu-id="f2967-103">Het toevoegen van een multitenant-toepassing naar de Azure AD-toepassingsgalerie</span><span class="sxs-lookup"><span data-stu-id="f2967-103">How to add a multi-tenant application to the Azure AD application gallery</span></span>

## <a name="what-is-the-azure-ad-application-gallery"></a><span data-ttu-id="f2967-104">Wat is de Azure AD-Toepassingsgalerie?</span><span class="sxs-lookup"><span data-stu-id="f2967-104">What is the Azure AD Application Gallery?</span></span>

<span data-ttu-id="f2967-105">De Azure AD-Toepassingsgalerie is een uitstekende manier om uw toepassing voor alle miljoenen klanten Azure Active Directory uitbreiden van de impact en ze bereiken van uw toepassing in de marketplace.</span><span class="sxs-lookup"><span data-stu-id="f2967-105">The Azure AD Application Gallery is a great way to get your application in front of all the millions of Azure Active Directory customers to broaden the impact and reach of your application in the marketplace.</span></span> <span data-ttu-id="f2967-106">De onderstaande stappen uitgelegd hoe u uw toepassing in de Azure AD-Toepassingsgalerie kunt weergeven.</span><span class="sxs-lookup"><span data-stu-id="f2967-106">The below steps explain how you can list your application in the Azure AD Application Gallery.</span></span>

## <a name="if-your-application-supports-saml-or-openidconnect"></a><span data-ttu-id="f2967-107">Als uw toepassing biedt ondersteuning voor SAML- of OpenIDConnect</span><span class="sxs-lookup"><span data-stu-id="f2967-107">If your application supports SAML or OpenIDConnect</span></span>
<span data-ttu-id="f2967-108">Als u een multitenant-toepassing die u wilt weergeven in de Azure AD-Toepassingsgalerie hebt, moet u eerst controleren of uw toepassing een van de volgende eenmalige aanmelding technologieën ondersteunt:</span><span class="sxs-lookup"><span data-stu-id="f2967-108">If you have a multi-tenant application you'd like to list in the Azure AD Application Gallery, you must first make sure that your application supports one of the following single sign-on technologies:</span></span>

1. <span data-ttu-id="f2967-109">**OpenID Connect** -directe integratie met Azure AD met OpenID Connect voor verificatie en de Azure AD API toestemming voor configuratie.</span><span class="sxs-lookup"><span data-stu-id="f2967-109">**OpenID Connect** - Direct integration with Azure AD using OpenID Connect for authentication and the Azure AD consent API for configuration.</span></span> <span data-ttu-id="f2967-110">Als u een integratie net begint en SAML biedt geen ondersteuning voor uw toepassing, is dit de aanbevolen modus.</span><span class="sxs-lookup"><span data-stu-id="f2967-110">If you are just starting an integration and your application does not support SAML, then this is the recommend mode.</span></span>
2. <span data-ttu-id="f2967-111">**SAML** – de toepassing al heeft de mogelijkheid voor het configureren van derden identiteitsproviders met het SAML-protocol.</span><span class="sxs-lookup"><span data-stu-id="f2967-111">**SAML** – Your application already has the ability to configure third-party identity providers using the SAML protocol.</span></span>

<span data-ttu-id="f2967-112">Als uw toepassing ondersteuning biedt voor een van deze modi voor eenmalige aanmelding en u wilt uw toepassing met meerdere tenants in de Azure AD-Toepassingsgalerie weergeven, kunt u de stappen in het onderstaande document.</span><span class="sxs-lookup"><span data-stu-id="f2967-112">If your application supports one of these single sign-on modes and you'd like to list your multi-tenant application in the Azure AD Application Gallery, you can follow the steps in the document below.</span></span> <span data-ttu-id="f2967-113">Snel aan de slag sturen een e-mail naar  **waadpartners@microsoft.com** .</span><span class="sxs-lookup"><span data-stu-id="f2967-113">To get started quickly send an email to **waadpartners@microsoft.com**.</span></span>

## <a name="if-your-application-does-not-support-saml-or-openidconnect"></a><span data-ttu-id="f2967-114">Als uw toepassing biedt geen ondersteuning voor SAML of OpenIDConnect</span><span class="sxs-lookup"><span data-stu-id="f2967-114">If your application does not support SAML or OpenIDConnect</span></span>
<span data-ttu-id="f2967-115">Zelfs als uw toepassing biedt geen ondersteuning voor een van deze modi, kunnen we het nog steeds integreren in onze galerie met onze wachtwoord Single Sign-on-technologie.</span><span class="sxs-lookup"><span data-stu-id="f2967-115">Even if your application does not support one of these modes, we can still integrate it into our gallery using our Password Single Sign-on technology.</span></span> <span data-ttu-id="f2967-116">Als u wilt verkennen met deze optie kunt u een e-mailbericht te verzenden  **waadpartners@microsoft.com** .</span><span class="sxs-lookup"><span data-stu-id="f2967-116">If you'd like to explore this option, you can send an email to **waadpartners@microsoft.com**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f2967-117">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="f2967-117">Next steps</span></span>
[<span data-ttu-id="f2967-118">Hoe u uw toepassing in de Azure Active Directory-toepassingsgalerie</span><span class="sxs-lookup"><span data-stu-id="f2967-118">How to list your application in the Azure Active Directory application gallery</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-app-gallery-listing)

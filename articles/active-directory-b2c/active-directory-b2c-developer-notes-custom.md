---
title: 'Azure Active Directory B2C: Opmerkingen voor ontwikkelaars op het gebruik van aangepast beleid | Microsoft Docs'
description: Opmerkingen voor ontwikkelaars over het configureren en onderhouden van Azure AD B2C met aangepast beleid
services: active-directory-b2c
documentationcenter: 
author: rojasja
manager: krassk
editor: rojasja
ms.assetid: 
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 05/05/2017
ms.author: joroja
ms.openlocfilehash: a5f222e5b11e05286152a9f1cc55d2c3fc27a9dc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="release-notes-for-azure-active-directory-b2c-custom-policy-public-preview"></a><span data-ttu-id="b22d3-103">Releaseopmerkingen voor openbare preview van Azure Active Directory B2C aangepast beleid</span><span class="sxs-lookup"><span data-stu-id="b22d3-103">Release notes for Azure Active Directory B2C custom policy public preview</span></span>
<span data-ttu-id="b22d3-104">De functieset aangepast beleid is nu beschikbaar voor evaluatie van de openbare preview voor alle Azure Active Directory B2C (Azure AD B2C) klanten.</span><span class="sxs-lookup"><span data-stu-id="b22d3-104">The custom policy feature set is now available for evaluation under public preview for all Azure Active Directory B2C (Azure AD B2C) customers.</span></span> <span data-ttu-id="b22d3-105">Deze functieset is gericht op geavanceerde identiteit ontwikkelaars oplossingen die het meest complexe identiteit.</span><span class="sxs-lookup"><span data-stu-id="b22d3-105">This feature set is targeted at advanced identity developers building the most complex identity solutions.</span></span>  

<span data-ttu-id="b22d3-106">Vandaag de dag, vereist deze functieset ontwikkelaars voor het configureren van het Framework identiteit ervaring rechtstreeks via XML-bestand bewerken.</span><span class="sxs-lookup"><span data-stu-id="b22d3-106">Today, this feature set requires developers to configure the Identity Experience Framework directly via XML file editing.</span></span> <span data-ttu-id="b22d3-107">Deze methode van de configuratie is een krachtige en complexe.</span><span class="sxs-lookup"><span data-stu-id="b22d3-107">This method of configuration is powerful and complex.</span></span> <span data-ttu-id="b22d3-108">Geavanceerde identiteit ontwikkelaars met behulp van het kader van de gebruikerservaring identiteit moeten wilt investeren enige tijd voor het voltooien van de zelfstudies en verwijzing naar documenten te lezen.</span><span class="sxs-lookup"><span data-stu-id="b22d3-108">Advanced identity developers using the Identity Experience Framework should plan to invest some time completing walk-throughs and reading reference documents.</span></span> 

## <a name="features-included-in-this-public-preview"></a><span data-ttu-id="b22d3-109">Functies in deze openbare preview</span><span class="sxs-lookup"><span data-stu-id="b22d3-109">Features included in this public preview</span></span>
<span data-ttu-id="b22d3-110">Met de nieuwe functies geïntroduceerd in de openbare preview, kunnen ontwikkelaars de volgende taken uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="b22d3-110">With the new features introduced in the public preview, developers can perform the following tasks:</span></span><br>

* <span data-ttu-id="b22d3-111">Maken en uploaden aangepaste verificatie gebruiker trajecten met behulp van aangepast beleid.</span><span class="sxs-lookup"><span data-stu-id="b22d3-111">Author and upload custom authentication user journeys by using custom policies.</span></span> 
   * <span data-ttu-id="b22d3-112">Gebruikers reizen stapsgewijze als kunnen worden uitgewisseld tussen claimproviders beschrijven.</span><span class="sxs-lookup"><span data-stu-id="b22d3-112">Describe user journeys step-by-step as exchanges between claims providers.</span></span> 
   * <span data-ttu-id="b22d3-113">Definieer Voorwaardelijke vertakkingen in trajecten van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="b22d3-113">Define conditional branching in user journeys.</span></span> 
* <span data-ttu-id="b22d3-114">REST-API-diensten in uw aangepaste verificatie gebruiker trajecten worden geïntegreerd.</span><span class="sxs-lookup"><span data-stu-id="b22d3-114">Integrate REST API-enabled services in your custom authentication user journeys.</span></span>  
* <span data-ttu-id="b22d3-115">Federatie met de id-providers die compatibel met de standaard OpenIDConnect zijn toevoegen.</span><span class="sxs-lookup"><span data-stu-id="b22d3-115">Add federation with identity providers that are compliant with the OpenIDConnect standard.</span></span> <br>
* <span data-ttu-id="b22d3-116">Toevoegen van Federatie met de id-providers die aan het SAML 2.0-protocol voldoen.</span><span class="sxs-lookup"><span data-stu-id="b22d3-116">Add federation with identity providers that adhere to the SAML 2.0 protocol.</span></span> 

## <a name="terms-of-the-public-preview"></a><span data-ttu-id="b22d3-117">Voorwaarden van de openbare preview</span><span class="sxs-lookup"><span data-stu-id="b22d3-117">Terms of the public preview</span></span>

* <span data-ttu-id="b22d3-118">We raden u aan de nieuwe functies gebruiken voor evaluatiedoeleinden.</span><span class="sxs-lookup"><span data-stu-id="b22d3-118">We encourage you to use the new features for evaluation purposes only.</span></span><br>
* <span data-ttu-id="b22d3-119">De nieuwe functies zijn niet bedoeld voor gebruik in een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="b22d3-119">The new features are not intended for use in a production environment.</span></span><br>
* <span data-ttu-id="b22d3-120">Service level agreements (Sla) niet van toepassing op de nieuwe functies.</span><span class="sxs-lookup"><span data-stu-id="b22d3-120">Service level agreements (SLAs) do not apply to the new features.</span></span> <br>
* <span data-ttu-id="b22d3-121">Ondersteuningsaanvragen kunnen worden ingediend via reguliere ondersteuningskanalen.</span><span class="sxs-lookup"><span data-stu-id="b22d3-121">Support requests can be filed through regular support channels.</span></span> <br>
* <span data-ttu-id="b22d3-122">Er is geen toegezegde opgegeven voor algemene beschikbaarheid.</span><span class="sxs-lookup"><span data-stu-id="b22d3-122">There is no promised date for general availability.</span></span><br>
* <span data-ttu-id="b22d3-123">Onze goeddunken, en voor welke reden dan ook, kunt Microsoft markeren en weigeren of scenario's en gebruiker trajecten die groter is dan het bereik van de Azure AD B2C product Freelance moeten fungeren als een klant identiteits- en toegangsbeheer (CIAM) beheerplatform beperken.</span><span class="sxs-lookup"><span data-stu-id="b22d3-123">At our discretion, and for any reason, Microsoft can flag and reject or restrict scenarios and user journeys that exceed the scope of the Azure AD B2C product charter to serve as a customer identity and access management (CIAM) platform.</span></span>

## <a name="responsibilities-of-custom-policy-feature-set-developers"></a><span data-ttu-id="b22d3-124">De verantwoordelijkheden van aangepast beleid functieset ontwikkelaars</span><span class="sxs-lookup"><span data-stu-id="b22d3-124">Responsibilities of custom policy feature-set developers</span></span>
<span data-ttu-id="b22d3-125">Handmatige beleidsconfiguratie lager niveau toegang verleent tot het onderliggende platform van Azure AD B2C en resulteert in het maken van een unieke, volledig aanpasbare vertrouwensrelatie-framework.</span><span class="sxs-lookup"><span data-stu-id="b22d3-125">Manual policy configuration grants lower-level access to the underlying platform of Azure AD B2C and results in the creation of a unique, fully customizable trust framework.</span></span> <span data-ttu-id="b22d3-126">Het aantal mogelijke permutaties met aangepaste identiteitsproviders, vertrouwensrelaties, integraties met externe services en stapsgewijze werkstromen hogere eisen op plaatsen gevorderde ontwikkelaars die ze gebruiken.</span><span class="sxs-lookup"><span data-stu-id="b22d3-126">The possible permutations of custom identity providers, trust relationships, integrations with external services, and step-by-step workflows place greater demands on the advanced developers consuming them.</span></span>

<span data-ttu-id="b22d3-127">Om volledig profiteren van de openbare preview, is het raadzaam dat ontwikkelaars de functieset aangepast beleid gebruiken in overeenstemming zijn met de volgende richtlijnen:</span><span class="sxs-lookup"><span data-stu-id="b22d3-127">To fully benefit from the public preview, we suggest that developers consuming the custom policy feature set adhere to the following guidelines:</span></span>
* <span data-ttu-id="b22d3-128">Vertrouwd raken met de taal van de configuratie van de identiteit ervaring Engine en het beheer van de sleutel/geheimen.</span><span class="sxs-lookup"><span data-stu-id="b22d3-128">Become familiar with the configuration language of the Identity Experience Engine and key/secrets management.</span></span>
* <span data-ttu-id="b22d3-129">Eigenaar worden van scenario's en aangepaste integraties.</span><span class="sxs-lookup"><span data-stu-id="b22d3-129">Take ownership of scenarios and custom integrations.</span></span>
* <span data-ttu-id="b22d3-130">Methodisch scenariotests uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="b22d3-130">Perform methodical scenario testing.</span></span>
* <span data-ttu-id="b22d3-131">Ga als volgt software ontwikkelings- en staging-best practices met ten minste één ontwikkelings- en testomgeving en een productie-omgeving.</span><span class="sxs-lookup"><span data-stu-id="b22d3-131">Follow software development and staging best practices with a minimum of one development and testing environment and one production environment.</span></span>
* <span data-ttu-id="b22d3-132">Blijf op de hoogte over nieuwe ontwikkelingen in de id-providers en services die u met integreert.</span><span class="sxs-lookup"><span data-stu-id="b22d3-132">Stay informed about new developments from the identity providers and services you integrate with.</span></span> <span data-ttu-id="b22d3-133">Bijvoorbeeld: bijhouden van wijzigingen in geheimen en geplande en ongeplande wijzigingen in de service.</span><span class="sxs-lookup"><span data-stu-id="b22d3-133">For example, keep track of changes in secrets and of scheduled and unscheduled changes to the service.</span></span>
* <span data-ttu-id="b22d3-134">Actieve bewaking hebt ingesteld en bewaak de reactiesnelheid van productieomgevingen.</span><span class="sxs-lookup"><span data-stu-id="b22d3-134">Set up active monitoring, and monitor the responsiveness of production environments.</span></span>
* <span data-ttu-id="b22d3-135">Neem contact op met e-mailadressen actueel te houden en blijf reageert op de Microsoft live-site-team e-mailberichten.</span><span class="sxs-lookup"><span data-stu-id="b22d3-135">Keep contact email addresses current, and stay responsive to the Microsoft live-site team emails.</span></span>
* <span data-ttu-id="b22d3-136">Maatregelen tijdige wanneer aangeraden om dit te doen door het team van Microsoft live-site.</span><span class="sxs-lookup"><span data-stu-id="b22d3-136">Take timely action when advised to do so by the Microsoft live-site team.</span></span> 


>[!NOTE]
><span data-ttu-id="b22d3-137">Deze functies worden uiteindelijk misschien opgenomen in Azure AD ingebouwde beleid, zodat ze beter toegankelijk voor alle ontwikkelaars.</span><span class="sxs-lookup"><span data-stu-id="b22d3-137">These features might eventually be included in Azure AD built-in policies, making them more accessible to all developers.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b22d3-138">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="b22d3-138">Next steps</span></span>
<span data-ttu-id="b22d3-139">[Aan de slag met aangepaste beleidsregels](active-directory-b2c-get-started-custom.md).</span><span class="sxs-lookup"><span data-stu-id="b22d3-139">[Get started with custom policies](active-directory-b2c-get-started-custom.md).</span></span>

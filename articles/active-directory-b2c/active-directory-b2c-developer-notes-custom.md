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
ms.openlocfilehash: 979b8a264eb819ee4a208b9171a53a5ffbf062c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="release-notes-for-azure-active-directory-b2c-custom-policy-public-preview"></a><span data-ttu-id="7bce7-103">Releaseopmerkingen voor openbare preview van Azure Active Directory B2C aangepast beleid</span><span class="sxs-lookup"><span data-stu-id="7bce7-103">Release notes for Azure Active Directory B2C custom policy public preview</span></span>
<span data-ttu-id="7bce7-104">Hallo functieset aangepast beleid is nu beschikbaar voor evaluatie onder public preview voor alle Azure Active Directory B2C (Azure AD B2C) klanten.</span><span class="sxs-lookup"><span data-stu-id="7bce7-104">hello custom policy feature set is now available for evaluation under public preview for all Azure Active Directory B2C (Azure AD B2C) customers.</span></span> <span data-ttu-id="7bce7-105">Deze functieset is gericht op ontwikkelaars van geavanceerde identiteit Hallo meest complexe identiteitsoplossingen bouwen.</span><span class="sxs-lookup"><span data-stu-id="7bce7-105">This feature set is targeted at advanced identity developers building hello most complex identity solutions.</span></span>  

<span data-ttu-id="7bce7-106">Vandaag de dag, vereist deze functieset ontwikkelaars tooconfigure Hallo identiteit ervaring Framework rechtstreeks via XML-bestand bewerken.</span><span class="sxs-lookup"><span data-stu-id="7bce7-106">Today, this feature set requires developers tooconfigure hello Identity Experience Framework directly via XML file editing.</span></span> <span data-ttu-id="7bce7-107">Deze methode van de configuratie is een krachtige en complexe.</span><span class="sxs-lookup"><span data-stu-id="7bce7-107">This method of configuration is powerful and complex.</span></span> <span data-ttu-id="7bce7-108">Geavanceerde identiteit ontwikkelaars met Hallo moet identiteit ervaring Framework plannen tooinvest enige tijd voor het voltooien van de zelfstudies en verwijzing naar documenten te lezen.</span><span class="sxs-lookup"><span data-stu-id="7bce7-108">Advanced identity developers using hello Identity Experience Framework should plan tooinvest some time completing walk-throughs and reading reference documents.</span></span> 

## <a name="features-included-in-this-public-preview"></a><span data-ttu-id="7bce7-109">Functies in deze openbare preview</span><span class="sxs-lookup"><span data-stu-id="7bce7-109">Features included in this public preview</span></span>
<span data-ttu-id="7bce7-110">Hallo nieuwe functies geïntroduceerd in de openbare preview hello, kunnen ontwikkelaars Hallo volgende taken uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="7bce7-110">With hello new features introduced in hello public preview, developers can perform hello following tasks:</span></span><br>

* <span data-ttu-id="7bce7-111">Maken en uploaden aangepaste verificatie gebruiker trajecten met behulp van aangepast beleid.</span><span class="sxs-lookup"><span data-stu-id="7bce7-111">Author and upload custom authentication user journeys by using custom policies.</span></span> 
   * <span data-ttu-id="7bce7-112">Gebruikers reizen stapsgewijze als kunnen worden uitgewisseld tussen claimproviders beschrijven.</span><span class="sxs-lookup"><span data-stu-id="7bce7-112">Describe user journeys step-by-step as exchanges between claims providers.</span></span> 
   * <span data-ttu-id="7bce7-113">Definieer Voorwaardelijke vertakkingen in trajecten van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="7bce7-113">Define conditional branching in user journeys.</span></span> 
* <span data-ttu-id="7bce7-114">REST-API-diensten in uw aangepaste verificatie gebruiker trajecten worden geïntegreerd.</span><span class="sxs-lookup"><span data-stu-id="7bce7-114">Integrate REST API-enabled services in your custom authentication user journeys.</span></span>  
* <span data-ttu-id="7bce7-115">Federatie met de id-providers die compatibel met de Hallo OpenIDConnect standaard zijn toevoegen.</span><span class="sxs-lookup"><span data-stu-id="7bce7-115">Add federation with identity providers that are compliant with hello OpenIDConnect standard.</span></span> <br>
* <span data-ttu-id="7bce7-116">Toevoegen van Federatie met de id-providers die toohello SAML 2.0-protocol voldoen.</span><span class="sxs-lookup"><span data-stu-id="7bce7-116">Add federation with identity providers that adhere toohello SAML 2.0 protocol.</span></span> 

## <a name="terms-of-hello-public-preview"></a><span data-ttu-id="7bce7-117">Gebruiksvoorwaarden Hallo openbare preview</span><span class="sxs-lookup"><span data-stu-id="7bce7-117">Terms of hello public preview</span></span>

* <span data-ttu-id="7bce7-118">We raden u toouse Hallo nieuwe functies voor evaluatiedoeleinden.</span><span class="sxs-lookup"><span data-stu-id="7bce7-118">We encourage you toouse hello new features for evaluation purposes only.</span></span><br>
* <span data-ttu-id="7bce7-119">De nieuwe functies zijn niet bedoeld voor gebruik in een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="7bce7-119">The new features are not intended for use in a production environment.</span></span><br>
* <span data-ttu-id="7bce7-120">Service level agreements (Sla) toohello nieuwe functies zijn niet van toepassing.</span><span class="sxs-lookup"><span data-stu-id="7bce7-120">Service level agreements (SLAs) do not apply toohello new features.</span></span> <br>
* <span data-ttu-id="7bce7-121">Ondersteuningsaanvragen kunnen worden ingediend via reguliere ondersteuningskanalen.</span><span class="sxs-lookup"><span data-stu-id="7bce7-121">Support requests can be filed through regular support channels.</span></span> <br>
* <span data-ttu-id="7bce7-122">Er is geen toegezegde opgegeven voor algemene beschikbaarheid.</span><span class="sxs-lookup"><span data-stu-id="7bce7-122">There is no promised date for general availability.</span></span><br>
* <span data-ttu-id="7bce7-123">Onze goeddunken, en voor welke reden dan ook, kunt Microsoft markeren en weigeren of scenario's en gebruiker trajecten die groter is dan Hallo bereik van hello Azure AD B2C product Freelance tooserve als een klant identiteits- en toegangsbeheer (CIAM) beheerplatform beperken.</span><span class="sxs-lookup"><span data-stu-id="7bce7-123">At our discretion, and for any reason, Microsoft can flag and reject or restrict scenarios and user journeys that exceed hello scope of hello Azure AD B2C product charter tooserve as a customer identity and access management (CIAM) platform.</span></span>

## <a name="responsibilities-of-custom-policy-feature-set-developers"></a><span data-ttu-id="7bce7-124">De verantwoordelijkheden van aangepast beleid functieset ontwikkelaars</span><span class="sxs-lookup"><span data-stu-id="7bce7-124">Responsibilities of custom policy feature-set developers</span></span>
<span data-ttu-id="7bce7-125">Handmatige beleidsconfiguratie verleent toegang lager niveau toohello onderliggende platform van Azure AD B2C en resulteert in het Hallo maken van een unieke, volledig aanpasbare vertrouwensrelatie-framework.</span><span class="sxs-lookup"><span data-stu-id="7bce7-125">Manual policy configuration grants lower-level access toohello underlying platform of Azure AD B2C and results in hello creation of a unique, fully customizable trust framework.</span></span> <span data-ttu-id="7bce7-126">Het aantal mogelijke permutaties met aangepaste identiteitsproviders, vertrouwensrelaties, integraties met externe services en stapsgewijze werkstromen plaats hogere eisen op Hallo geavanceerde ontwikkelaars die ze gebruiken.</span><span class="sxs-lookup"><span data-stu-id="7bce7-126">The possible permutations of custom identity providers, trust relationships, integrations with external services, and step-by-step workflows place greater demands on hello advanced developers consuming them.</span></span>

<span data-ttu-id="7bce7-127">toofully voordeel van de openbare preview hello, het is raadzaam dat ontwikkelaars verbruikt Hallo aangepast beleid functieset toohello richtlijnen voldoen:</span><span class="sxs-lookup"><span data-stu-id="7bce7-127">toofully benefit from hello public preview, we suggest that developers consuming hello custom policy feature set adhere toohello following guidelines:</span></span>
* <span data-ttu-id="7bce7-128">Vertrouwd raken met de Hallo configuratie taal Hallo identiteit ervaring Engine en sleutel/geheimen management.</span><span class="sxs-lookup"><span data-stu-id="7bce7-128">Become familiar with hello configuration language of hello Identity Experience Engine and key/secrets management.</span></span>
* <span data-ttu-id="7bce7-129">Eigenaar worden van scenario's en aangepaste integraties.</span><span class="sxs-lookup"><span data-stu-id="7bce7-129">Take ownership of scenarios and custom integrations.</span></span>
* <span data-ttu-id="7bce7-130">Methodisch scenariotests uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="7bce7-130">Perform methodical scenario testing.</span></span>
* <span data-ttu-id="7bce7-131">Ga als volgt software ontwikkelings- en staging-best practices met ten minste één ontwikkelings- en testomgeving en een productie-omgeving.</span><span class="sxs-lookup"><span data-stu-id="7bce7-131">Follow software development and staging best practices with a minimum of one development and testing environment and one production environment.</span></span>
* <span data-ttu-id="7bce7-132">Blijf op de hoogte over nieuwe ontwikkelingen van Hallo id-providers en -services die u met integreert.</span><span class="sxs-lookup"><span data-stu-id="7bce7-132">Stay informed about new developments from hello identity providers and services you integrate with.</span></span> <span data-ttu-id="7bce7-133">Bijvoorbeeld: bijhouden van wijzigingen in geheimen en van geplande en ongeplande wijzigingen toohello service.</span><span class="sxs-lookup"><span data-stu-id="7bce7-133">For example, keep track of changes in secrets and of scheduled and unscheduled changes toohello service.</span></span>
* <span data-ttu-id="7bce7-134">Actieve bewaking hebt ingesteld en bewaak Hallo reactiesnelheid van productieomgevingen.</span><span class="sxs-lookup"><span data-stu-id="7bce7-134">Set up active monitoring, and monitor hello responsiveness of production environments.</span></span>
* <span data-ttu-id="7bce7-135">Neem contact op met e-mailadressen actueel te houden en blijven responsief toohello Microsoft live-site-team e-mailberichten.</span><span class="sxs-lookup"><span data-stu-id="7bce7-135">Keep contact email addresses current, and stay responsive toohello Microsoft live-site team emails.</span></span>
* <span data-ttu-id="7bce7-136">Tijdige actie ondernemen als aanbevolen toodo Hallo van Microsoft-team voor live-site.</span><span class="sxs-lookup"><span data-stu-id="7bce7-136">Take timely action when advised toodo so by hello Microsoft live-site team.</span></span> 


>[!NOTE]
><span data-ttu-id="7bce7-137">Deze functies worden uiteindelijk misschien opgenomen in Azure AD ingebouwde beleid, zodat ze beter toegankelijk tooall ontwikkelaars.</span><span class="sxs-lookup"><span data-stu-id="7bce7-137">These features might eventually be included in Azure AD built-in policies, making them more accessible tooall developers.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7bce7-138">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="7bce7-138">Next steps</span></span>
<span data-ttu-id="7bce7-139">[Aan de slag met aangepaste beleidsregels](active-directory-b2c-get-started-custom.md).</span><span class="sxs-lookup"><span data-stu-id="7bce7-139">[Get started with custom policies](active-directory-b2c-get-started-custom.md).</span></span>

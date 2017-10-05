---
title: 'Azure Active Directory B2C: Regio beschikbaarheid & gegevens hand vestigingsplaats | Microsoft Docs'
description: Een onderwerp over de verschillende typen tenants van Azure Active Directory B2C
services: active-directory-b2c
documentationcenter: 
author: gsacavdm
manager: krassk
editor: bryanla
ms.assetid: 8a0644da-b825-4edc-8ce9-541c3c976afb
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/10/2017
ms.author: gsacavdm
ms.openlocfilehash: facd66f0324e382ea7609a035de8129ba433846f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-active-directory-b2c-region-availability--data-residency"></a><span data-ttu-id="8970c-103">Azure Active Directory B2C: Regio beschikbaarheid & gegevens hand vestigingsplaats</span><span class="sxs-lookup"><span data-stu-id="8970c-103">Azure Active Directory B2C: Region availability & data residency</span></span>
<span data-ttu-id="8970c-104">Beschikbaarheid in regio's en de hand van gegevens vestigingsplaats zijn twee heel andere concepten die anders van toepassing op Azure AD B2C van de rest van Azure.</span><span class="sxs-lookup"><span data-stu-id="8970c-104">Region availability and data residency are two very different concepts that apply differently to Azure AD B2C from the rest of Azure.</span></span> <span data-ttu-id="8970c-105">In dit artikel wordt uitgelegd van de verschillen tussen deze twee concepten en vergelijken hoe ze van toepassing op Azure ten opzichte van Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="8970c-105">This article will explain the differences between these two concepts and compare how they apply to Azure versus Azure AD B2C.</span></span>

## <a name="summary"></a><span data-ttu-id="8970c-106">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="8970c-106">Summary</span></span>
<span data-ttu-id="8970c-107">Azure AD B2C wordt **algemeen beschikbaar wereldwijd** met de optie voor **hand vestigingsplaats gegevens in de Verenigde Staten of Europa**.</span><span class="sxs-lookup"><span data-stu-id="8970c-107">Azure AD B2C is **generally available worldwide** with the option for **data residency in United States or Europe**.</span></span>

## <a name="concepts"></a><span data-ttu-id="8970c-108">Concepten</span><span class="sxs-lookup"><span data-stu-id="8970c-108">Concepts</span></span>
* <span data-ttu-id="8970c-109">**Beschikbaarheid in regio's** verwijst naar waar een service beschikbaar voor gebruik is.</span><span class="sxs-lookup"><span data-stu-id="8970c-109">**Region availability** refers to where a service is available for use.</span></span>
* <span data-ttu-id="8970c-110">**De hand van gegevens vestigingsplaats** verwijst naar waar de gebruikersgegevens zijn opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="8970c-110">**Data residency** refers to where user data is stored.</span></span>

## <a name="region-availability"></a><span data-ttu-id="8970c-111">Beschikbaarheid in regio’s</span><span class="sxs-lookup"><span data-stu-id="8970c-111">Region availability</span></span>
<span data-ttu-id="8970c-112">Azure AD B2C is wereldwijd beschikbaar via de openbare Azure-cloud.</span><span class="sxs-lookup"><span data-stu-id="8970c-112">Azure AD B2C is available worldwide via the Azure public cloud.</span></span> 

<span data-ttu-id="8970c-113">Dit verschilt van het model meeste andere Azure-services volgen die Combineer beschikbaarheid aan de hand van gegevens vestigingsplaats.</span><span class="sxs-lookup"><span data-stu-id="8970c-113">This differs from the model most other Azure services follow which couple availability with data residency.</span></span> <span data-ttu-id="8970c-114">Ziet u voorbeelden van deze in beide Azure [beschikbare producten door regio](https://azure.microsoft.com/regions/services/) pagina en de [Active Directory B2C prijscategorie Rekenmachine](https://azure.microsoft.com/pricing/details/active-directory-b2c/).</span><span class="sxs-lookup"><span data-stu-id="8970c-114">You can see examples of this in both Azure's [Products Available By Region](https://azure.microsoft.com/regions/services/) page and the [Active Directory B2C pricing calculator](https://azure.microsoft.com/pricing/details/active-directory-b2c/).</span></span>

## <a name="data-residency"></a><span data-ttu-id="8970c-115">Gegevensresidentie</span><span class="sxs-lookup"><span data-stu-id="8970c-115">Data residency</span></span>
<span data-ttu-id="8970c-116">Azure AD B2C slaat gebruikersgegevens in de Verenigde Staten of Europa.</span><span class="sxs-lookup"><span data-stu-id="8970c-116">Azure AD B2C stores user data in either United States or Europe.</span></span>

<span data-ttu-id="8970c-117">De hand van gegevens vestigingsplaats wordt bepaald op basis van welke land/regio is geselecteerd als [maken van een Azure AD B2C-tenant](active-directory-b2c-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="8970c-117">Data residency is determined based on which country/region is selected when [creating an Azure AD B2C tenant](active-directory-b2c-get-started.md).</span></span>

![Schermopname van een tenant preview](./media/active-directory-b2c-reference-tenant-type/data-residency-b2c-tenant.png)

<span data-ttu-id="8970c-119">Gegevens bevinden zich in de Verenigde Staten voor de volgende landen/regio's:</span><span class="sxs-lookup"><span data-stu-id="8970c-119">Data resides in the United States for the following countries/regions:</span></span>

> <span data-ttu-id="8970c-120">Verenigde Staten, Canada, Costa Rica, Dominicaanse Republiek, El Salvador, Guatemala, Mexico, Panama, Portorico en Trinidad en Tobago</span><span class="sxs-lookup"><span data-stu-id="8970c-120">United States, Canada, Costa Rica, Dominican Republic, El Salvador, Guatemala, Mexico, Panama, Puerto Rico and Trinidad & Tobago</span></span>

<span data-ttu-id="8970c-121">Voor de volgende landen/regio's, bevindt zich in Europa gegevens:</span><span class="sxs-lookup"><span data-stu-id="8970c-121">Data resides in Europe for the following countries/regions:</span></span>

> <span data-ttu-id="8970c-122">Algerije, Oostenrijk, Azerbeidzjan, Bahrein, Belarus, België, Bulgarije, Kroatië, Cyprus, Tsjechië, Denemarken, Egypte, Estland, Finland, Frankrijk, Duitsland, Griekenland, Hongarije, IJsland, Ierland, Israël, Italië, Jordanië, Kazachstan, Kenia, Koeweit, Letland, Libanon, Liechtenstein, NNNNNN, Luxemburg, Macedonië Macedonisch, Malta, Montenegro, Marokko, Nederland, Nigeria, Noorwegen, Oman, Pakistan, Polen, Portugal, Qatar, Roemenië, Rusland, Saudi-Arabië, Servië, Slowakije, Slovenië, Zuid-Afrika, Spanje, Zweden, Zwitserland, Tunesië, Turkije, Oekraïne, VAE en Verenigd Koninkrijk.</span><span class="sxs-lookup"><span data-stu-id="8970c-122">Algeria, Austria, Azerbaijan, Bahrain, Belarus, Belgium, Bulgaria, Croatia, Cyprus, Czech Republic, Denmark, Egypt, Estonia, Finland, France, Germany, Greece, Hungary, Iceland, Ireland, Israel, Italy, Jordan, Kazakhstan, Kenya, Kuwait, Lativa, Lebanon, Liechtenstein, Lituania, Luxembourg, Macedonia FYRO, Malta, Montenegro, Morocco, Netherlands, Nigeria, Norway, Oman, Pakistan, Poland, Portugal, Qatar, Romania, Russia, Saudi Arabia, Serbia, Slovakia, Slovenia, South Africa, Spain, Sweden, Switzerland, Tunisia, Turkey, Ukraine, United Arab Emirates and United Kingdom.</span></span>

<span data-ttu-id="8970c-123">De overige landen/regio's zijn bezig met worden toegevoegd aan de lijst.</span><span class="sxs-lookup"><span data-stu-id="8970c-123">The remaining countries/regions are in the process of being added to the list.</span></span>  <span data-ttu-id="8970c-124">Op dit moment kunt u Azure AD B2C door een van de landen/regio's bovenstaande verzamelen.</span><span class="sxs-lookup"><span data-stu-id="8970c-124">For now, you can still use Azure AD B2C by picking any of the countries/regions above.</span></span>

> <span data-ttu-id="8970c-125">Afghanistan, Argentinië, Australië, Brazilië, onderliggende, Colombia, Ecuador, Hongkong SAR, India, Indonesië, Irak, Japan, Korea, Maleisië, Nieuw-Zeeland, Paraguay, Peru, Filipijnen, Singapore, Sri Lanka, Taiwan, Thailand, Uruguay en Venezuela.</span><span class="sxs-lookup"><span data-stu-id="8970c-125">Afghanistan, Argentina, Australia, Brazil, Chile, Colombia, Ecuador, Hong Kong SAR, India, Indonesia, Iraq, Japan, Korea, Malaysia, New Zealand, Paraguay, Peru, Philippines, Singapore, Sri Lanka, Taiwan, Thailand, Uruguay and Venezuela.</span></span>

## <a name="preview-tenant"></a><span data-ttu-id="8970c-126">Preview-tenant</span><span class="sxs-lookup"><span data-stu-id="8970c-126">Preview tenant</span></span>
<span data-ttu-id="8970c-127">Als u een B2C-tenant had gemaakt in Azure AD B2C preview-periode, is het waarschijnlijk dat uw **Tenant-type** zegt **Preview tenant**.</span><span class="sxs-lookup"><span data-stu-id="8970c-127">If you had created a B2C tenant during Azure AD B2C's preview period, it is likely that your **Tenant type** says **Preview tenant**.</span></span> <span data-ttu-id="8970c-128">Als dit het geval is, moet u uw tenant alleen voor ontwikkelings- en testdoeleinden en niet voor productie-apps gebruiken.</span><span class="sxs-lookup"><span data-stu-id="8970c-128">If this is the case, you MUST use your tenant only for development and testing purposes, and NOT for production apps.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8970c-129">Er is geen migratiepad van een preview B2C-tenant in een productie-scale B2C-tenant.</span><span class="sxs-lookup"><span data-stu-id="8970c-129">There is no migration path from a preview B2C tenant to a production-scale B2C tenant.</span></span> <span data-ttu-id="8970c-130">Let op: Er zijn bekende problemen wanneer u een voorbeeld B2C-tenant verwijderen en opnieuw maken van een productie-scale B2C-tenant met dezelfde domeinnaam.</span><span class="sxs-lookup"><span data-stu-id="8970c-130">Note that there are known issues when you delete a preview B2C tenant and re-create a production-scale B2C tenant with the same domain name.</span></span> <span data-ttu-id="8970c-131">U moet een productie-scale B2C-tenant maken met een andere domeinnaam.</span><span class="sxs-lookup"><span data-stu-id="8970c-131">You have to create a production-scale B2C tenant with a different domain name.</span></span>


![Schermopname van een tenant preview](./media/active-directory-b2c-reference-tenant-type/preview-b2c-tenant.png)

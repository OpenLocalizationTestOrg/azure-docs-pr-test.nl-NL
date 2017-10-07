---
title: 'Azure Active Directory B2C: Regio beschikbaarheid & gegevens hand vestigingsplaats | Microsoft Docs'
description: Een onderwerp op Hallo soorten tenants van Azure Active Directory B2C
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
ms.openlocfilehash: d382921fe9d62183b6d52c47d62f952dabd116c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-region-availability--data-residency"></a><span data-ttu-id="4d2ff-103">Azure Active Directory B2C: Regio beschikbaarheid & gegevens hand vestigingsplaats</span><span class="sxs-lookup"><span data-stu-id="4d2ff-103">Azure Active Directory B2C: Region availability & data residency</span></span>
<span data-ttu-id="4d2ff-104">Beschikbaarheid in regio's en de hand van gegevens vestigingsplaats zijn twee heel andere concepten die anders tooAzure AD B2C van de rest Hallo van Azure toepassen.</span><span class="sxs-lookup"><span data-stu-id="4d2ff-104">Region availability and data residency are two very different concepts that apply differently tooAzure AD B2C from hello rest of Azure.</span></span> <span data-ttu-id="4d2ff-105">In dit artikel wordt Hallo verschillen tussen deze twee concepten uitgelegd en vergelijken hoe ze tooAzure ten opzichte van Azure AD B2C van toepassing.</span><span class="sxs-lookup"><span data-stu-id="4d2ff-105">This article will explain hello differences between these two concepts and compare how they apply tooAzure versus Azure AD B2C.</span></span>

## <a name="summary"></a><span data-ttu-id="4d2ff-106">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="4d2ff-106">Summary</span></span>
<span data-ttu-id="4d2ff-107">Azure AD B2C wordt **algemeen beschikbaar wereldwijd** met de optie Hallo **hand vestigingsplaats gegevens in de Verenigde Staten of Europa**.</span><span class="sxs-lookup"><span data-stu-id="4d2ff-107">Azure AD B2C is **generally available worldwide** with hello option for **data residency in United States or Europe**.</span></span>

## <a name="concepts"></a><span data-ttu-id="4d2ff-108">Concepten</span><span class="sxs-lookup"><span data-stu-id="4d2ff-108">Concepts</span></span>
* <span data-ttu-id="4d2ff-109">**Beschikbaarheid in regio's** toowhere verwijst een service is beschikbaar voor gebruik.</span><span class="sxs-lookup"><span data-stu-id="4d2ff-109">**Region availability** refers toowhere a service is available for use.</span></span>
* <span data-ttu-id="4d2ff-110">**De hand van gegevens vestigingsplaats** verwijst toowhere gebruiker gegevens worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="4d2ff-110">**Data residency** refers toowhere user data is stored.</span></span>

## <a name="region-availability"></a><span data-ttu-id="4d2ff-111">Beschikbaarheid in regio’s</span><span class="sxs-lookup"><span data-stu-id="4d2ff-111">Region availability</span></span>
<span data-ttu-id="4d2ff-112">Azure AD B2C is wereldwijd beschikbaar via hello Azure openbare cloud.</span><span class="sxs-lookup"><span data-stu-id="4d2ff-112">Azure AD B2C is available worldwide via hello Azure public cloud.</span></span> 

<span data-ttu-id="4d2ff-113">Dit verschilt van Hallo model meeste andere Azure-services volgen die Combineer beschikbaarheid aan de hand van gegevens vestigingsplaats.</span><span class="sxs-lookup"><span data-stu-id="4d2ff-113">This differs from hello model most other Azure services follow which couple availability with data residency.</span></span> <span data-ttu-id="4d2ff-114">Ziet u voorbeelden van deze in beide Azure [beschikbare producten door regio](https://azure.microsoft.com/regions/services/) pagina en Hallo [Active Directory B2C prijscategorie Rekenmachine](https://azure.microsoft.com/pricing/details/active-directory-b2c/).</span><span class="sxs-lookup"><span data-stu-id="4d2ff-114">You can see examples of this in both Azure's [Products Available By Region](https://azure.microsoft.com/regions/services/) page and hello [Active Directory B2C pricing calculator](https://azure.microsoft.com/pricing/details/active-directory-b2c/).</span></span>

## <a name="data-residency"></a><span data-ttu-id="4d2ff-115">Gegevensresidentie</span><span class="sxs-lookup"><span data-stu-id="4d2ff-115">Data residency</span></span>
<span data-ttu-id="4d2ff-116">Azure AD B2C slaat gebruikersgegevens in de Verenigde Staten of Europa.</span><span class="sxs-lookup"><span data-stu-id="4d2ff-116">Azure AD B2C stores user data in either United States or Europe.</span></span>

<span data-ttu-id="4d2ff-117">De hand van gegevens vestigingsplaats wordt bepaald op basis van welke land/regio is geselecteerd als [maken van een Azure AD B2C-tenant](active-directory-b2c-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="4d2ff-117">Data residency is determined based on which country/region is selected when [creating an Azure AD B2C tenant](active-directory-b2c-get-started.md).</span></span>

![Schermopname van een tenant preview](./media/active-directory-b2c-reference-tenant-type/data-residency-b2c-tenant.png)

<span data-ttu-id="4d2ff-119">Gegevens zich in de Verenigde Staten Hallo voor Hallo landen/regio's te volgen:</span><span class="sxs-lookup"><span data-stu-id="4d2ff-119">Data resides in hello United States for hello following countries/regions:</span></span>

> <span data-ttu-id="4d2ff-120">Verenigde Staten, Canada, Costa Rica, Dominicaanse Republiek, El Salvador, Guatemala, Mexico, Panama, Portorico en Trinidad en Tobago</span><span class="sxs-lookup"><span data-stu-id="4d2ff-120">United States, Canada, Costa Rica, Dominican Republic, El Salvador, Guatemala, Mexico, Panama, Puerto Rico and Trinidad & Tobago</span></span>

<span data-ttu-id="4d2ff-121">Gegevens zich bevindt in Europa voor Hallo landen/regio's te volgen:</span><span class="sxs-lookup"><span data-stu-id="4d2ff-121">Data resides in Europe for hello following countries/regions:</span></span>

> <span data-ttu-id="4d2ff-122">Algerije, Oostenrijk, Azerbeidzjan, Bahrein, Belarus, België, Bulgarije, Kroatië, Cyprus, Tsjechië, Denemarken, Egypte, Estland, Finland, Frankrijk, Duitsland, Griekenland, Hongarije, IJsland, Ierland, Israël, Italië, Jordanië, Kazachstan, Kenia, Koeweit, Letland, Libanon, Liechtenstein, NNNNNN, Luxemburg, Macedonië Macedonisch, Malta, Montenegro, Marokko, Nederland, Nigeria, Noorwegen, Oman, Pakistan, Polen, Portugal, Qatar, Roemenië, Rusland, Saudi-Arabië, Servië, Slowakije, Slovenië, Zuid-Afrika, Spanje, Zweden, Zwitserland, Tunesië, Turkije, Oekraïne, VAE en Verenigd Koninkrijk.</span><span class="sxs-lookup"><span data-stu-id="4d2ff-122">Algeria, Austria, Azerbaijan, Bahrain, Belarus, Belgium, Bulgaria, Croatia, Cyprus, Czech Republic, Denmark, Egypt, Estonia, Finland, France, Germany, Greece, Hungary, Iceland, Ireland, Israel, Italy, Jordan, Kazakhstan, Kenya, Kuwait, Lativa, Lebanon, Liechtenstein, Lituania, Luxembourg, Macedonia FYRO, Malta, Montenegro, Morocco, Netherlands, Nigeria, Norway, Oman, Pakistan, Poland, Portugal, Qatar, Romania, Russia, Saudi Arabia, Serbia, Slovakia, Slovenia, South Africa, Spain, Sweden, Switzerland, Tunisia, Turkey, Ukraine, United Arab Emirates and United Kingdom.</span></span>

<span data-ttu-id="4d2ff-123">resterende Hallo-landen/regio's zijn in Hallo proces toohello lijst wordt toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="4d2ff-123">hello remaining countries/regions are in hello process of being added toohello list.</span></span>  <span data-ttu-id="4d2ff-124">Op dit moment kunt u Azure AD B2C door het verzamelen van Hallo landen/regio's hierboven.</span><span class="sxs-lookup"><span data-stu-id="4d2ff-124">For now, you can still use Azure AD B2C by picking any of hello countries/regions above.</span></span>

> <span data-ttu-id="4d2ff-125">Afghanistan, Argentinië, Australië, Brazilië, onderliggende, Colombia, Ecuador, Hongkong SAR, India, Indonesië, Irak, Japan, Korea, Maleisië, Nieuw-Zeeland, Paraguay, Peru, Filipijnen, Singapore, Sri Lanka, Taiwan, Thailand, Uruguay en Venezuela.</span><span class="sxs-lookup"><span data-stu-id="4d2ff-125">Afghanistan, Argentina, Australia, Brazil, Chile, Colombia, Ecuador, Hong Kong SAR, India, Indonesia, Iraq, Japan, Korea, Malaysia, New Zealand, Paraguay, Peru, Philippines, Singapore, Sri Lanka, Taiwan, Thailand, Uruguay and Venezuela.</span></span>

## <a name="preview-tenant"></a><span data-ttu-id="4d2ff-126">Preview-tenant</span><span class="sxs-lookup"><span data-stu-id="4d2ff-126">Preview tenant</span></span>
<span data-ttu-id="4d2ff-127">Als u een B2C-tenant had gemaakt in Azure AD B2C preview-periode, is het waarschijnlijk dat uw **Tenant-type** zegt **Preview tenant**.</span><span class="sxs-lookup"><span data-stu-id="4d2ff-127">If you had created a B2C tenant during Azure AD B2C's preview period, it is likely that your **Tenant type** says **Preview tenant**.</span></span> <span data-ttu-id="4d2ff-128">Als dit Hallo geval is, moet u uw tenant alleen voor ontwikkelings- en testdoeleinden en niet voor productie-apps gebruiken.</span><span class="sxs-lookup"><span data-stu-id="4d2ff-128">If this is hello case, you MUST use your tenant only for development and testing purposes, and NOT for production apps.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4d2ff-129">Er is geen migratiepad van een preview B2C-tenant tooa productie scale B2C-tenant.</span><span class="sxs-lookup"><span data-stu-id="4d2ff-129">There is no migration path from a preview B2C tenant tooa production-scale B2C tenant.</span></span> <span data-ttu-id="4d2ff-130">Let op: Er zijn bekende problemen bij het verwijderen van een preview B2C-tenant en maak opnieuw een productie-scale B2C-tenant met Hallo dezelfde domeinnaam.</span><span class="sxs-lookup"><span data-stu-id="4d2ff-130">Note that there are known issues when you delete a preview B2C tenant and re-create a production-scale B2C tenant with hello same domain name.</span></span> <span data-ttu-id="4d2ff-131">U hebt een productie-scale B2C-tenant met een andere domeinnaam toocreate.</span><span class="sxs-lookup"><span data-stu-id="4d2ff-131">You have toocreate a production-scale B2C tenant with a different domain name.</span></span>


![Schermopname van een tenant preview](./media/active-directory-b2c-reference-tenant-type/preview-b2c-tenant.png)

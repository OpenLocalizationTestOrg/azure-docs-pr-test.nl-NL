---
title: Azure CDN-inhoud per land beperken | Microsoft Docs
description: Informatie over het beperken van toegang tot uw Azure CDN-inhoud met de functie voor het filteren van Geo.
services: cdn
documentationcenter: 
author: lichard
manager: akucer
editor: 
ms.assetid: 12c17cc5-28ee-4b0b-ba22-2266be2e786a
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: rli
ms.openlocfilehash: 30160088d9c770400f342e67527e1cf1cabc4f6b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="restrict-azure-cdn-content-by-country"></a><span data-ttu-id="cced8-103">Azure CDN-inhoud per land beperken</span><span class="sxs-lookup"><span data-stu-id="cced8-103">Restrict Azure CDN content by country</span></span>

## <a name="overview"></a><span data-ttu-id="cced8-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="cced8-104">Overview</span></span>
<span data-ttu-id="cced8-105">Wanneer een gebruiker wordt uw inhoud standaard aanvraagt, wordt de inhoud aangeboden ongeacht waar de gebruiker gemaakt voor deze aanvraag uit.</span><span class="sxs-lookup"><span data-stu-id="cced8-105">When a user requests your content, by default, the content is served regardless of where the user made this request from.</span></span> <span data-ttu-id="cced8-106">In sommige gevallen wilt u mogelijk beperken van toegang tot uw inhoud door land.</span><span class="sxs-lookup"><span data-stu-id="cced8-106">In some cases, you may want to restrict access to your content by country.</span></span> <span data-ttu-id="cced8-107">In dit onderwerp wordt uitgelegd hoe u de **Geo filteren** functie om de service configureren voor het toestaan of blokkeren van toegang per land.</span><span class="sxs-lookup"><span data-stu-id="cced8-107">This topic explains how to use the **Geo-Filtering** feature in order to configure the service to allow or block access by country.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="cced8-108">De producten Verizon en Akamai bieden dezelfde functionaliteit geo filteren, maar hebben een klein verschil in landcodes te ondersteunen.</span><span class="sxs-lookup"><span data-stu-id="cced8-108">The Verizon and Akamai products provide the same geo-filtering functionality but have a small difference in te country codes they support.</span></span> <span data-ttu-id="cced8-109">Zie stap 3 voor een koppeling naar de verschillen.</span><span class="sxs-lookup"><span data-stu-id="cced8-109">See Step 3 for a link to the differences.</span></span>


<span data-ttu-id="cced8-110">Zie voor meer informatie over overwegingen die van toepassing zijn op de configuratie van dit type beperking de [overwegingen](cdn-restrict-access-by-country.md#considerations) sectie aan het einde van het onderwerp.</span><span class="sxs-lookup"><span data-stu-id="cced8-110">For information about considerations that apply to configuring this type of restriction, see the [Considerations](cdn-restrict-access-by-country.md#considerations) section at the end of the topic.</span></span>  

![Landen filteren](./media/cdn-filtering/cdn-country-filtering-akamai.png)

## <a name="step-1-define-the-directory-path"></a><span data-ttu-id="cced8-112">Stap 1: Het directorypad definiëren</span><span class="sxs-lookup"><span data-stu-id="cced8-112">Step 1: Define the directory path</span></span>
<span data-ttu-id="cced8-113">Selecteer uw eindpunt in de portal en het filteren van Geo-tabblad vinden op de linkernavigatiebalk voor deze functie vindt.</span><span class="sxs-lookup"><span data-stu-id="cced8-113">Select your endpoint within the portal, and find the Geo-Filtering tab on the left-hand navigation to find this feature.</span></span>

<span data-ttu-id="cced8-114">Wanneer u een filter land configureert, moet u het relatieve pad naar de locatie waarnaar gebruikers wordt toegestaan of toegang geweigerd.</span><span class="sxs-lookup"><span data-stu-id="cced8-114">When configuring a country filter, you must specify the relative path to the location to which users will be allowed or denied access.</span></span> <span data-ttu-id="cced8-115">U kunt filteren van geo toepassen voor alle bestanden met '/' of de geselecteerde mappen door te geven mappaden '/ afbeeldingen /'.</span><span class="sxs-lookup"><span data-stu-id="cced8-115">You can apply geo-filtering for all your files with "/" or selected folders by specifying directory paths "/pictures/".</span></span> <span data-ttu-id="cced8-116">U kunt ook een geografisch filteren in één bestand toepassen door te geven van het bestand en daarbij de afsluitende slash ' / afbeeldingen/stad.PNG '.</span><span class="sxs-lookup"><span data-stu-id="cced8-116">You can also apply geo-filtering to a single file by specifying the file, and leaving out the trailing slash "/pictures/city.png".</span></span>

<span data-ttu-id="cced8-117">Voorbeeld van de directory pad filter:</span><span class="sxs-lookup"><span data-stu-id="cced8-117">Example directory path filter:</span></span>

    /                                 
    /Photos/
    /Photos/Strasbourg/
      /Photos/Strasbourg/city.png

## <a name="step-2-define-the-action-block-or-allow"></a><span data-ttu-id="cced8-118">Stap 2: Definieer de actie: blokkeren of toestaan</span><span class="sxs-lookup"><span data-stu-id="cced8-118">Step 2: Define the action: block or allow</span></span>
<span data-ttu-id="cced8-119">**Blokkeren:** gebruikers van de opgegeven landen wordt de toegang geweigerd tot bedrijfsmiddelen aangevraagd bij dat recursieve-pad.</span><span class="sxs-lookup"><span data-stu-id="cced8-119">**Block:** Users from the specified countries will be denied access to assets requested from that recursive path.</span></span> <span data-ttu-id="cced8-120">Als er geen andere land-filteropties zijn geconfigureerd voor die locatie, klikt u vervolgens alle andere gebruikers mogen toegang.</span><span class="sxs-lookup"><span data-stu-id="cced8-120">If no other country filtering options have been configured for that location, then all other users will be allowed access.</span></span>

<span data-ttu-id="cced8-121">**Toestaan:** alleen uit de opgegeven landen gebruikers toegang tot bedrijfsmiddelen aangevraagd bij dat recursieve-pad kunnen.</span><span class="sxs-lookup"><span data-stu-id="cced8-121">**Allow:** Only users from the specified countries will be allowed access to assets requested from that recursive path.</span></span>

## <a name="step-3-define-the-countries"></a><span data-ttu-id="cced8-122">Stap 3: De landen definiëren</span><span class="sxs-lookup"><span data-stu-id="cced8-122">Step 3: Define the countries</span></span>
<span data-ttu-id="cced8-123">Selecteer de landen die u wilt blokkeren of toestaan voor het pad.</span><span class="sxs-lookup"><span data-stu-id="cced8-123">Select the countries that you want to block or allow for the path.</span></span> 

<span data-ttu-id="cced8-124">De regel van het blokkeren van /Photos/Straatsburg/wordt bijvoorbeeld bestanden met inbegrip van filteren:</span><span class="sxs-lookup"><span data-stu-id="cced8-124">For example, the rule of blocking /Photos/Strasbourg/ will filter files including:</span></span>

    http://<endpoint>.azureedge.net/Photos/Strasbourg/1000.jpg
    http://<endpoint>.azureedge.net/Photos/Strasbourg/Cathedral/1000.jpg


### <a name="country-codes"></a><span data-ttu-id="cced8-125">Landcodes</span><span class="sxs-lookup"><span data-stu-id="cced8-125">Country codes</span></span>
<span data-ttu-id="cced8-126">De **Geo filteren** functie landcodes gebruikt voor het definiëren van de landen waarin een aanvraag wordt toegestaan of geblokkeerd voor een beveiligde map.</span><span class="sxs-lookup"><span data-stu-id="cced8-126">The **Geo-Filtering** feature uses country codes to define the countries from which a request will be allowed or blocked for a secured directory.</span></span> <span data-ttu-id="cced8-127">U vindt de landcodes in [Azure CDN landcodes](https://msdn.microsoft.com/library/mt761717.aspx).</span><span class="sxs-lookup"><span data-stu-id="cced8-127">You will find the country codes in [Azure CDN  Country Codes](https://msdn.microsoft.com/library/mt761717.aspx).</span></span> 

## <span data-ttu-id="cced8-128"><a id="considerations"></a>Overwegingen</span><span class="sxs-lookup"><span data-stu-id="cced8-128"><a id="considerations"></a>Considerations</span></span>
* <span data-ttu-id="cced8-129">Het kan tot 90 minuten duren voor Verizon of een paar minuten met Akamai, voor wijzigingen in uw land filteren van de configuratie van kracht te laten worden.</span><span class="sxs-lookup"><span data-stu-id="cced8-129">It may take up to 90 minutes for Verizon, or a couple minutes with Akamai, for changes to your country filtering configuration to take effect.</span></span>
* <span data-ttu-id="cced8-130">Deze functie biedt geen ondersteuning voor jokertekens (bijvoorbeeld ' *').</span><span class="sxs-lookup"><span data-stu-id="cced8-130">This feature does not support wildcard characters (for example, ‘*’).</span></span>
* <span data-ttu-id="cced8-131">De configuratie van de geo-filteren die zijn gekoppeld aan het relatieve pad wordt recursief toegepast naar het opgegeven pad.</span><span class="sxs-lookup"><span data-stu-id="cced8-131">The geo-filtering configuration associated with the relative path will be applied recursively to that path.</span></span>
* <span data-ttu-id="cced8-132">Slechts één regel kan worden toegepast op hetzelfde relatieve pad (u kunt meerdere land filters die naar hetzelfde relatieve pad verwijzen niet maken.</span><span class="sxs-lookup"><span data-stu-id="cced8-132">Only one rule can be applied to the same relative path (you cannot create multiple country filters that point to the same relative path.</span></span> <span data-ttu-id="cced8-133">Een map hebben echter meerdere land filters.</span><span class="sxs-lookup"><span data-stu-id="cced8-133">However, a folder may have multiple country filters.</span></span> <span data-ttu-id="cced8-134">Dit komt door de recursieve aard van de filters land.</span><span class="sxs-lookup"><span data-stu-id="cced8-134">This is due to the recursive nature of country filters.</span></span> <span data-ttu-id="cced8-135">Een submap van een eerder geconfigureerde map kan met andere woorden, een ander land filter toegewezen.</span><span class="sxs-lookup"><span data-stu-id="cced8-135">In other words, a subfolder of a previously configured folder can be assigned a different country filter.</span></span>


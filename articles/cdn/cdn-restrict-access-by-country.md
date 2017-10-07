---
title: Azure CDN-inhoud door land aaaRestrict | Microsoft Docs
description: Meer informatie over hoe toorestrict toegang tooyour Azure CDN inhoud met behulp van Hallo Geo-filters.
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
ms.openlocfilehash: ffdd994612b6c9cfbf1a6e29d260709b4afa86e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="restrict-azure-cdn-content-by-country"></a><span data-ttu-id="79de1-103">Azure CDN-inhoud per land beperken</span><span class="sxs-lookup"><span data-stu-id="79de1-103">Restrict Azure CDN content by country</span></span>

## <a name="overview"></a><span data-ttu-id="79de1-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="79de1-104">Overview</span></span>
<span data-ttu-id="79de1-105">Wanneer een gebruiker wordt uw inhoud standaard aanvraagt, wordt inhoud Hallo geleverd ongeacht waar Hallo gebruiker gemaakt voor deze aanvraag uit.</span><span class="sxs-lookup"><span data-stu-id="79de1-105">When a user requests your content, by default, hello content is served regardless of where hello user made this request from.</span></span> <span data-ttu-id="79de1-106">In sommige gevallen kunt u toorestrict toegang tot tooyour inhoud per land.</span><span class="sxs-lookup"><span data-stu-id="79de1-106">In some cases, you may want toorestrict access tooyour content by country.</span></span> <span data-ttu-id="79de1-107">Dit onderwerp wordt uitgelegd hoe toouse hello **Geo filteren** functie in volgorde tooconfigure Hallo service tooallow of de toegang blokkeert per land.</span><span class="sxs-lookup"><span data-stu-id="79de1-107">This topic explains how toouse hello **Geo-Filtering** feature in order tooconfigure hello service tooallow or block access by country.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="79de1-108">Hallo Verizon en Akamai producten bieden dezelfde functionaliteit geo filteren Hallo maar hebben een klein verschil in landcodes te ondersteunen.</span><span class="sxs-lookup"><span data-stu-id="79de1-108">hello Verizon and Akamai products provide hello same geo-filtering functionality but have a small difference in te country codes they support.</span></span> <span data-ttu-id="79de1-109">Zie stap 3 voor een koppeling toohello verschillen.</span><span class="sxs-lookup"><span data-stu-id="79de1-109">See Step 3 for a link toohello differences.</span></span>


<span data-ttu-id="79de1-110">Dit type beperking, Zie voor informatie over overwegingen die van toepassing tooconfiguring hello [overwegingen](cdn-restrict-access-by-country.md#considerations) sectie achter Hallo Hallo onderwerp.</span><span class="sxs-lookup"><span data-stu-id="79de1-110">For information about considerations that apply tooconfiguring this type of restriction, see hello [Considerations](cdn-restrict-access-by-country.md#considerations) section at hello end of hello topic.</span></span>  

![Landen filteren](./media/cdn-filtering/cdn-country-filtering-akamai.png)

## <a name="step-1-define-hello-directory-path"></a><span data-ttu-id="79de1-112">Stap 1: Hallo mappad definiëren</span><span class="sxs-lookup"><span data-stu-id="79de1-112">Step 1: Define hello directory path</span></span>
<span data-ttu-id="79de1-113">Selecteer uw eindpunt binnen Hallo-portal en Hallo Geo filteren tabblad op Hallo linkermenubalk toofind deze functie vindt.</span><span class="sxs-lookup"><span data-stu-id="79de1-113">Select your endpoint within hello portal, and find hello Geo-Filtering tab on hello left-hand navigation toofind this feature.</span></span>

<span data-ttu-id="79de1-114">Wanneer u een filter land configureert, moet u Hallo relatief pad toohello locatie toowhich gebruikers wordt toegestaan of toegang geweigerd.</span><span class="sxs-lookup"><span data-stu-id="79de1-114">When configuring a country filter, you must specify hello relative path toohello location toowhich users will be allowed or denied access.</span></span> <span data-ttu-id="79de1-115">U kunt filteren van geo toepassen voor alle bestanden met '/' of de geselecteerde mappen door te geven mappaden '/ afbeeldingen /'.</span><span class="sxs-lookup"><span data-stu-id="79de1-115">You can apply geo-filtering for all your files with "/" or selected folders by specifying directory paths "/pictures/".</span></span> <span data-ttu-id="79de1-116">U kunt ook tooa geo filteren enkel bestand toepassen Hallo-bestand opgeven en daarbij afsluitende slash Hallo ' / afbeeldingen/stad.PNG '.</span><span class="sxs-lookup"><span data-stu-id="79de1-116">You can also apply geo-filtering tooa single file by specifying hello file, and leaving out hello trailing slash "/pictures/city.png".</span></span>

<span data-ttu-id="79de1-117">Voorbeeld van de directory pad filter:</span><span class="sxs-lookup"><span data-stu-id="79de1-117">Example directory path filter:</span></span>

    /                                 
    /Photos/
    /Photos/Strasbourg/
      /Photos/Strasbourg/city.png

## <a name="step-2-define-hello-action-block-or-allow"></a><span data-ttu-id="79de1-118">Stap 2: Definiëren Hallo actie: blokkeren of toestaan</span><span class="sxs-lookup"><span data-stu-id="79de1-118">Step 2: Define hello action: block or allow</span></span>
<span data-ttu-id="79de1-119">**Blokkeren:** gebruikers van Hallo opgegeven landen toegang tooassets aangevraagd bij dat recursieve pad wordt geweigerd.</span><span class="sxs-lookup"><span data-stu-id="79de1-119">**Block:** Users from hello specified countries will be denied access tooassets requested from that recursive path.</span></span> <span data-ttu-id="79de1-120">Als er geen andere land-filteropties zijn geconfigureerd voor die locatie, klikt u vervolgens alle andere gebruikers mogen toegang.</span><span class="sxs-lookup"><span data-stu-id="79de1-120">If no other country filtering options have been configured for that location, then all other users will be allowed access.</span></span>

<span data-ttu-id="79de1-121">**Toestaan:** alleen gebruikers van Hallo opgegeven landen toegang tooassets aangevraagd bij dat pad recursieve worden toegestaan.</span><span class="sxs-lookup"><span data-stu-id="79de1-121">**Allow:** Only users from hello specified countries will be allowed access tooassets requested from that recursive path.</span></span>

## <a name="step-3-define-hello-countries"></a><span data-ttu-id="79de1-122">Stap 3: Hallo landen definiëren</span><span class="sxs-lookup"><span data-stu-id="79de1-122">Step 3: Define hello countries</span></span>
<span data-ttu-id="79de1-123">Selecteer Hallo landen die u tooblock wilt of toestaan voor Hallo-pad.</span><span class="sxs-lookup"><span data-stu-id="79de1-123">Select hello countries that you want tooblock or allow for hello path.</span></span> 

<span data-ttu-id="79de1-124">Hallo-regel van het blokkeren van /Photos/Straatsburg/wordt bijvoorbeeld bestanden met inbegrip van filteren:</span><span class="sxs-lookup"><span data-stu-id="79de1-124">For example, hello rule of blocking /Photos/Strasbourg/ will filter files including:</span></span>

    http://<endpoint>.azureedge.net/Photos/Strasbourg/1000.jpg
    http://<endpoint>.azureedge.net/Photos/Strasbourg/Cathedral/1000.jpg


### <a name="country-codes"></a><span data-ttu-id="79de1-125">Landcodes</span><span class="sxs-lookup"><span data-stu-id="79de1-125">Country codes</span></span>
<span data-ttu-id="79de1-126">Hallo **Geo filteren** functie land codes toodefine Hallo landen waarin een aanvraag wordt toegestaan of geblokkeerd voor een beveiligde map gebruikt.</span><span class="sxs-lookup"><span data-stu-id="79de1-126">hello **Geo-Filtering** feature uses country codes toodefine hello countries from which a request will be allowed or blocked for a secured directory.</span></span> <span data-ttu-id="79de1-127">U ziet Hallo landcodes in [Azure CDN landcodes](https://msdn.microsoft.com/library/mt761717.aspx).</span><span class="sxs-lookup"><span data-stu-id="79de1-127">You will find hello country codes in [Azure CDN  Country Codes](https://msdn.microsoft.com/library/mt761717.aspx).</span></span> 

## <span data-ttu-id="79de1-128"><a id="considerations"></a>Overwegingen</span><span class="sxs-lookup"><span data-stu-id="79de1-128"><a id="considerations"></a>Considerations</span></span>
* <span data-ttu-id="79de1-129">Het kan too90 minuten voor Verizon of voor wijzigingen tooyour land filteren configuratie tootake effect met Akamai, een paar minuten duren.</span><span class="sxs-lookup"><span data-stu-id="79de1-129">It may take up too90 minutes for Verizon, or a couple minutes with Akamai, for changes tooyour country filtering configuration tootake effect.</span></span>
* <span data-ttu-id="79de1-130">Deze functie biedt geen ondersteuning voor jokertekens (bijvoorbeeld ' *').</span><span class="sxs-lookup"><span data-stu-id="79de1-130">This feature does not support wildcard characters (for example, ‘*’).</span></span>
* <span data-ttu-id="79de1-131">Hallo geo filteren configuratie die is gekoppeld met het relatieve pad Hallo worden toegepaste recursief toothat pad.</span><span class="sxs-lookup"><span data-stu-id="79de1-131">hello geo-filtering configuration associated with hello relative path will be applied recursively toothat path.</span></span>
* <span data-ttu-id="79de1-132">Slechts één regel kan worden toegepast toohello hetzelfde relatieve pad (u kunt geen meerdere land filters te maken dat punt toohello hetzelfde relatieve pad.</span><span class="sxs-lookup"><span data-stu-id="79de1-132">Only one rule can be applied toohello same relative path (you cannot create multiple country filters that point toohello same relative path.</span></span> <span data-ttu-id="79de1-133">Een map hebben echter meerdere land filters.</span><span class="sxs-lookup"><span data-stu-id="79de1-133">However, a folder may have multiple country filters.</span></span> <span data-ttu-id="79de1-134">Dit is vanwege toohello recursieve aard van de filters land.</span><span class="sxs-lookup"><span data-stu-id="79de1-134">This is due toohello recursive nature of country filters.</span></span> <span data-ttu-id="79de1-135">Een submap van een eerder geconfigureerde map kan met andere woorden, een ander land filter toegewezen.</span><span class="sxs-lookup"><span data-stu-id="79de1-135">In other words, a subfolder of a previously configured folder can be assigned a different country filter.</span></span>


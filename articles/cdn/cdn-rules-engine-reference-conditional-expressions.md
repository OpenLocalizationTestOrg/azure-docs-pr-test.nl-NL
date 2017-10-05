---
title: Azure CDN regels engine voorwaardelijke expressies | Microsoft Docs
description: Documentatie bij Azure CDN regels overeen motor en onderdelen.
services: cdn
documentationcenter: 
author: Lichard
manager: akucer
editor: 
ms.assetid: 669ef140-a6dd-4b62-9b9d-3f375a14215e
ms.service: cdn
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: rli
ms.openlocfilehash: 57e56c38e003cb83dcf44f455c4451d159db8a59
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-cdn-rules-engine-conditional-expressions"></a><span data-ttu-id="13eca-103">Voorwaardelijke expressies in de engine Azure CDN-regels</span><span class="sxs-lookup"><span data-stu-id="13eca-103">Azure CDN rules engine conditional expressions</span></span>
<span data-ttu-id="13eca-104">Dit onderwerp vindt u gedetailleerde beschrijvingen van de voorwaardelijke expressies voor Azure Content Delivery Network (CDN) [regelengine](cdn-rules-engine.md).</span><span class="sxs-lookup"><span data-stu-id="13eca-104">This topic lists detailed descriptions of the Conditional Expressions for Azure Content Delivery Network (CDN) [Rules Engine](cdn-rules-engine.md).</span></span>

<span data-ttu-id="13eca-105">Het eerste deel van een regel is de conditionele expressie.</span><span class="sxs-lookup"><span data-stu-id="13eca-105">The first part of a rule is the Conditional Expression.</span></span>

<span data-ttu-id="13eca-106">Voorwaardelijke expressies</span><span class="sxs-lookup"><span data-stu-id="13eca-106">Conditional Expression</span></span> | <span data-ttu-id="13eca-107">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="13eca-107">Description</span></span>
-----------------------|-------------
<span data-ttu-id="13eca-108">ALS</span><span class="sxs-lookup"><span data-stu-id="13eca-108">IF</span></span> | <span data-ttu-id="13eca-109">Een expressie als is altijd een deel van de eerste instructie in een regel.</span><span class="sxs-lookup"><span data-stu-id="13eca-109">An IF expression is always a part of the first statement in a rule.</span></span> <span data-ttu-id="13eca-110">Net als alle andere voorwaardelijke expressies, moet deze instructie worden gekoppeld aan een overeenkomst.</span><span class="sxs-lookup"><span data-stu-id="13eca-110">Like all other conditional expressions, this IF statement must be associated with a match.</span></span> <span data-ttu-id="13eca-111">Als er geen aanvullende voorwaardelijke expressies zijn opgegeven, bepaalt deze treffer het criterium dat moet worden voldaan voordat een aantal functies kan worden toegepast op een aanvraag.</span><span class="sxs-lookup"><span data-stu-id="13eca-111">If no additional conditional expressions are defined, then this match determines the criterion that must be met before a set of features may be applied to a request.</span></span>
<span data-ttu-id="13eca-112">EN ALS</span><span class="sxs-lookup"><span data-stu-id="13eca-112">AND IF</span></span> | <span data-ttu-id="13eca-113">EN als expressie kan alleen worden toegevoegd na de volgende soorten voorwaardelijke expressies: als, en als.</span><span class="sxs-lookup"><span data-stu-id="13eca-113">An AND IF expression may only be added after the following types of conditional expressions:IF,AND IF.</span></span> <span data-ttu-id="13eca-114">Dit geeft aan dat er nog een voorwaarde die moet worden voldaan om de eerste instructie.</span><span class="sxs-lookup"><span data-stu-id="13eca-114">It indicates that there is another condition that must be met for the initial IF statement.</span></span>
<span data-ttu-id="13eca-115">ANDERS ALS</span><span class="sxs-lookup"><span data-stu-id="13eca-115">ELSE IF</span></span>| <span data-ttu-id="13eca-116">Een expressie ELSE IF Hiermee geeft u een alternatieve voorwaarde die moet worden voldaan voordat een verzameling functies die specifiek zijn voor deze instructie ELSE IF plaatsvindt.</span><span class="sxs-lookup"><span data-stu-id="13eca-116">An ELSE IF expression specifies an alternative condition that must be met before a set of features specific to this ELSE IF statement takes place.</span></span> <span data-ttu-id="13eca-117">De aanwezigheid van een ELSE IF-instructie geeft het einde van de vorige instructie.</span><span class="sxs-lookup"><span data-stu-id="13eca-117">The presence of an ELSE IF statement indicates the end of the previous statement.</span></span> <span data-ttu-id="13eca-118">De alleen voorwaardelijke expressies die kan worden geplaatst nadat een ELSE IF-instructie een andere ELSE IF-instructie is.</span><span class="sxs-lookup"><span data-stu-id="13eca-118">The only conditional expression that may be placed after an ELSE IF statement is another ELSE IF statement.</span></span> <span data-ttu-id="13eca-119">Dit betekent dat een ELSE IF-instructie kan alleen worden gebruikt om op te geven van een enkele aanvullende voorwaarde die moet worden voldaan.</span><span class="sxs-lookup"><span data-stu-id="13eca-119">This means that an ELSE IF statement may only be used to specify a single additional condition that has to be met.</span></span>

<span data-ttu-id="13eca-120">**Voorbeeld**: ![CDN overeenkomen met de voorwaarde](./media/cdn-rules-engine-reference/cdn-rules-engine-conditional-expression.png)</span><span class="sxs-lookup"><span data-stu-id="13eca-120">**Example**: ![CDN match condition](./media/cdn-rules-engine-reference/cdn-rules-engine-conditional-expression.png)</span></span>

 > [!TIP]
   > <span data-ttu-id="13eca-121">Een volgende regel mogen de handelingen die zijn opgegeven door een vorige regel overschrijven.</span><span class="sxs-lookup"><span data-stu-id="13eca-121">A subsequent rule may override the actions specified by a previous rule.</span></span> <span data-ttu-id="13eca-122">Voorbeeld: Een regel catch all-beveiligt alle aanvragen via verificatie op basis van tokens.</span><span class="sxs-lookup"><span data-stu-id="13eca-122">Example: A catch-all rule secures all requests via Token-Based Authentication.</span></span> <span data-ttu-id="13eca-123">Een andere regel kan rechtstreeks onder om er een uitzondering voor bepaalde typen aanvragen worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="13eca-123">Another rule may be created directly below it to make an exception for certain types of requests.</span></span>

### <a name="next-steps"></a><span data-ttu-id="13eca-124">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="13eca-124">Next steps</span></span>
* [<span data-ttu-id="13eca-125">Overzicht van Azure CDN</span><span class="sxs-lookup"><span data-stu-id="13eca-125">Azure CDN Overview</span></span>](cdn-overview.md)
* [<span data-ttu-id="13eca-126">Regels Engine verwijzing</span><span class="sxs-lookup"><span data-stu-id="13eca-126">Rules Engine Reference</span></span>](cdn-rules-engine-reference.md)
* [<span data-ttu-id="13eca-127">De overeenkomst motor regels</span><span class="sxs-lookup"><span data-stu-id="13eca-127">Rules Engine Match Conditions</span></span>](cdn-rules-engine-reference-match-conditions.md)
* [<span data-ttu-id="13eca-128">Regels Engine functies</span><span class="sxs-lookup"><span data-stu-id="13eca-128">Rules Engine Features</span></span>](cdn-rules-engine-reference-features.md)
* [<span data-ttu-id="13eca-129">Standaardgedrag HTTP met de regelengine van</span><span class="sxs-lookup"><span data-stu-id="13eca-129">Overriding default HTTP behavior using the rules engine</span></span>](cdn-rules-engine.md)

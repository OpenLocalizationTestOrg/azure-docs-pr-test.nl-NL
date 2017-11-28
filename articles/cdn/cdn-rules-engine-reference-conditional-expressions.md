---
title: aaaAzure CDN regels engine voorwaardelijke expressies | Microsoft Docs
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
ms.openlocfilehash: 39d0754c34a577f77ca87b6fd92e2b6a9e4ff8fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cdn-rules-engine-conditional-expressions"></a><span data-ttu-id="f15cf-103">Voorwaardelijke expressies in de engine Azure CDN-regels</span><span class="sxs-lookup"><span data-stu-id="f15cf-103">Azure CDN rules engine conditional expressions</span></span>
<span data-ttu-id="f15cf-104">Dit onderwerp vindt u gedetailleerde beschrijvingen van Hallo voorwaardelijke expressies voor Azure Content Delivery Network (CDN) [regelengine](cdn-rules-engine.md).</span><span class="sxs-lookup"><span data-stu-id="f15cf-104">This topic lists detailed descriptions of hello Conditional Expressions for Azure Content Delivery Network (CDN) [Rules Engine](cdn-rules-engine.md).</span></span>

<span data-ttu-id="f15cf-105">Hallo eerste deel van een regel is Hallo voorwaardelijke expressies.</span><span class="sxs-lookup"><span data-stu-id="f15cf-105">hello first part of a rule is hello Conditional Expression.</span></span>

<span data-ttu-id="f15cf-106">Voorwaardelijke expressies</span><span class="sxs-lookup"><span data-stu-id="f15cf-106">Conditional Expression</span></span> | <span data-ttu-id="f15cf-107">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="f15cf-107">Description</span></span>
-----------------------|-------------
<span data-ttu-id="f15cf-108">ALS</span><span class="sxs-lookup"><span data-stu-id="f15cf-108">IF</span></span> | <span data-ttu-id="f15cf-109">Een expressie als is altijd een deel van de eerste instructie Hallo in een regel.</span><span class="sxs-lookup"><span data-stu-id="f15cf-109">An IF expression is always a part of hello first statement in a rule.</span></span> <span data-ttu-id="f15cf-110">Net als alle andere voorwaardelijke expressies, moet deze instructie worden gekoppeld aan een overeenkomst.</span><span class="sxs-lookup"><span data-stu-id="f15cf-110">Like all other conditional expressions, this IF statement must be associated with a match.</span></span> <span data-ttu-id="f15cf-111">Als er geen aanvullende voorwaardelijke expressies zijn opgegeven, bepaalt deze treffer Hallo criterium dat moet worden voldaan voordat een verzameling functies is mogelijk toegepaste tooa aanvraag.</span><span class="sxs-lookup"><span data-stu-id="f15cf-111">If no additional conditional expressions are defined, then this match determines hello criterion that must be met before a set of features may be applied tooa request.</span></span>
<span data-ttu-id="f15cf-112">EN ALS</span><span class="sxs-lookup"><span data-stu-id="f15cf-112">AND IF</span></span> | <span data-ttu-id="f15cf-113">Een expressie en als kan alleen worden toegevoegd na het Hallo typen voorwaardelijke expressies: als, en als volgt.</span><span class="sxs-lookup"><span data-stu-id="f15cf-113">An AND IF expression may only be added after hello following types of conditional expressions:IF,AND IF.</span></span> <span data-ttu-id="f15cf-114">Dit geeft aan dat er nog een voorwaarde die moet worden voldaan om Hallo initiële IF-instructie.</span><span class="sxs-lookup"><span data-stu-id="f15cf-114">It indicates that there is another condition that must be met for hello initial IF statement.</span></span>
<span data-ttu-id="f15cf-115">ANDERS ALS</span><span class="sxs-lookup"><span data-stu-id="f15cf-115">ELSE IF</span></span>| <span data-ttu-id="f15cf-116">Een expressie ELSE IF Hiermee geeft u een alternatieve voorwaarde die moet worden voldaan voordat een reeks functies specifieke toothis ELSE IF-instructie plaatsvindt.</span><span class="sxs-lookup"><span data-stu-id="f15cf-116">An ELSE IF expression specifies an alternative condition that must be met before a set of features specific toothis ELSE IF statement takes place.</span></span> <span data-ttu-id="f15cf-117">Hallo aanwezigheid van een ELSE IF-instructie geeft Hallo einde van de vorige instructie Hallo.</span><span class="sxs-lookup"><span data-stu-id="f15cf-117">hello presence of an ELSE IF statement indicates hello end of hello previous statement.</span></span> <span data-ttu-id="f15cf-118">Hallo alleen voorwaardelijke expressies die kan worden geplaatst nadat een ELSE IF-instructie een andere ELSE IF-instructie is.</span><span class="sxs-lookup"><span data-stu-id="f15cf-118">hello only conditional expression that may be placed after an ELSE IF statement is another ELSE IF statement.</span></span> <span data-ttu-id="f15cf-119">Dit betekent dat een ELSE IF-instructie gebruikte toospecify enige aanvullende voorwaarde is voldaan toobe is alleen mogelijk.</span><span class="sxs-lookup"><span data-stu-id="f15cf-119">This means that an ELSE IF statement may only be used toospecify a single additional condition that has toobe met.</span></span>

<span data-ttu-id="f15cf-120">**Voorbeeld**: ![CDN overeenkomen met de voorwaarde](./media/cdn-rules-engine-reference/cdn-rules-engine-conditional-expression.png)</span><span class="sxs-lookup"><span data-stu-id="f15cf-120">**Example**: ![CDN match condition](./media/cdn-rules-engine-reference/cdn-rules-engine-conditional-expression.png)</span></span>

 > [!TIP]
   > <span data-ttu-id="f15cf-121">Een volgende regel mogen Hallo handelingen die zijn opgegeven door een vorige regel overschrijven.</span><span class="sxs-lookup"><span data-stu-id="f15cf-121">A subsequent rule may override hello actions specified by a previous rule.</span></span> <span data-ttu-id="f15cf-122">Voorbeeld: Een regel catch all-beveiligt alle aanvragen via verificatie op basis van tokens.</span><span class="sxs-lookup"><span data-stu-id="f15cf-122">Example: A catch-all rule secures all requests via Token-Based Authentication.</span></span> <span data-ttu-id="f15cf-123">Een andere regel kan worden gemaakt onder het toomake een uitzondering voor bepaalde typen aanvragen.</span><span class="sxs-lookup"><span data-stu-id="f15cf-123">Another rule may be created directly below it toomake an exception for certain types of requests.</span></span>

### <a name="next-steps"></a><span data-ttu-id="f15cf-124">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="f15cf-124">Next steps</span></span>
* [<span data-ttu-id="f15cf-125">Overzicht van Azure CDN</span><span class="sxs-lookup"><span data-stu-id="f15cf-125">Azure CDN Overview</span></span>](cdn-overview.md)
* [<span data-ttu-id="f15cf-126">Regels Engine verwijzing</span><span class="sxs-lookup"><span data-stu-id="f15cf-126">Rules Engine Reference</span></span>](cdn-rules-engine-reference.md)
* [<span data-ttu-id="f15cf-127">De overeenkomst motor regels</span><span class="sxs-lookup"><span data-stu-id="f15cf-127">Rules Engine Match Conditions</span></span>](cdn-rules-engine-reference-match-conditions.md)
* [<span data-ttu-id="f15cf-128">Regels Engine functies</span><span class="sxs-lookup"><span data-stu-id="f15cf-128">Rules Engine Features</span></span>](cdn-rules-engine-reference-features.md)
* [<span data-ttu-id="f15cf-129">Standaardgedrag HTTP met Hallo regelengine</span><span class="sxs-lookup"><span data-stu-id="f15cf-129">Overriding default HTTP behavior using hello rules engine</span></span>](cdn-rules-engine.md)

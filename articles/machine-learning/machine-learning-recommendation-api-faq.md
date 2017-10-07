---
title: aaaSet up en gebruikt Machine Learning aanbevelingen API Hallo | Microsoft Docs
description: Microsoft aanbevelingen API gebouwd met veelgestelde vragen over Azure Machine Learning
services: machine-learning
documentationcenter: 
author: LuisCabrer
manager: jhubbard
editor: cgronlun
ms.assetid: 1ffc3c16-e040-4225-9d72-105129938dfa
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: luisca
ROBOTS: NOINDEX
redirect_url: machine-learning-datamarket-deprecation
redirect_document_id: True
ms.openlocfilehash: 980bf1a36f3291275d9ef0fee9b4446f7e0cbecf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="setting-up-and-using-machine-learning-recommendations-api-faq"></a><span data-ttu-id="b7fd2-103">Veelgestelde vragen over Recommendations-API voor Machine Learning instellen en gebruiken</span><span class="sxs-lookup"><span data-stu-id="b7fd2-103">Setting up and using Machine Learning Recommendations API FAQ</span></span>
<span data-ttu-id="b7fd2-104">**Wat is aanbevelingen?**</span><span class="sxs-lookup"><span data-stu-id="b7fd2-104">**What is RECOMMENDATIONS?**</span></span>

> [!NOTE]
> <span data-ttu-id="b7fd2-105">U moet beginnen met Hallo cognitieve aanbevelingen API-Service in plaats van deze versie.</span><span class="sxs-lookup"><span data-stu-id="b7fd2-105">You should start using hello Recommendations API Cognitive Service instead of this version.</span></span> <span data-ttu-id="b7fd2-106">Hallo aanbevelingen cognitieve Service vervangt deze service en alle nieuwe functies in Hallo er zal worden ontwikkeld.</span><span class="sxs-lookup"><span data-stu-id="b7fd2-106">hello Recommendations Cognitive Service will be replacing this service, and all hello new features will be developed there.</span></span> <span data-ttu-id="b7fd2-107">Heeft nieuwe mogelijkheden, zoals batchverwerking ondersteuning, beter API Explorer, een schonere API surface, consistente aanmelding/facturering ervaring, enzovoort.</span><span class="sxs-lookup"><span data-stu-id="b7fd2-107">It has new capabilities like batching support, a better API Explorer, a cleaner API surface, more consistent signup/billing experience, etc.</span></span>
> <span data-ttu-id="b7fd2-108">Meer informatie over [migreren toohello nieuwe cognitieve Service](http://aka.ms/recomigrate)</span><span class="sxs-lookup"><span data-stu-id="b7fd2-108">Learn more about [Migrating toohello new Cognitive Service](http://aka.ms/recomigrate)</span></span>
> 
> 

<span data-ttu-id="b7fd2-109">Voor organisaties en bedrijven die afhankelijk van aanbevelingen toocross-verkopen en Upsell-producten en services tootheir klanten zijn, bevat de aanbevelingen in Azure Machine Learning een aanbevelingen selfservice-engine.</span><span class="sxs-lookup"><span data-stu-id="b7fd2-109">For organizations and businesses that rely on recommendations toocross-sell and up-sell products and services tootheir customers, RECOMMENDATIONS in Azure Machine Learning provides a self-service recommendations engine.</span></span> <span data-ttu-id="b7fd2-110">Er is een implementatie van samenwerking filteren die gebruikmaakt van de matrix factoriseren als de core-algoritme.</span><span class="sxs-lookup"><span data-stu-id="b7fd2-110">It is an implementation of collaborative filtering that uses matrix factorization as its core algorithm.</span></span> <span data-ttu-id="b7fd2-111">Ontwikkelaars hebben toegang tot aanbevelingen met behulp van REST-API's.</span><span class="sxs-lookup"><span data-stu-id="b7fd2-111">Application developers can access RECOMMENDATIONS by using REST APIs.</span></span> 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="b7fd2-112">**Wat kan ik doen met aanbevelingen**</span><span class="sxs-lookup"><span data-stu-id="b7fd2-112">**What can I do with RECOMMENDATIONS?**</span></span>

<span data-ttu-id="b7fd2-113">AANBEVELINGEN neemt als invoer een item of een verzameling items en geeft een lijst met relevante aanbevelingen.</span><span class="sxs-lookup"><span data-stu-id="b7fd2-113">RECOMMENDATIONS takes as input an item or a set of items and returns a list of relevant recommendations.</span></span> <span data-ttu-id="b7fd2-114">Bijvoorbeeld: een klant van een online winkel klikt op een product.</span><span class="sxs-lookup"><span data-stu-id="b7fd2-114">For example: A customer of an online retailer clicks a product.</span></span> <span data-ttu-id="b7fd2-115">Hallo online detailhandel product verzendt als invoer tooRECOMMENDATIONS, in een lijst van producten opgehaald en besluit welke van deze producten toohello klant wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="b7fd2-115">hello online retailer sends that product as input tooRECOMMENDATIONS, gets a list of products in return, and decides which of these products will be shown toohello customer.</span></span> <span data-ttu-id="b7fd2-116">U kunt wilt toouse aanbevelingen toooptimize uw online winkel of zelfs tooinform uw binnen verkoop afdeling of aanroep center.</span><span class="sxs-lookup"><span data-stu-id="b7fd2-116">You may want toouse RECOMMENDATIONS toooptimize your online store or even tooinform your inside sales department or call center.</span></span>

<span data-ttu-id="b7fd2-117">**Zijn er beperkingen gebruik?**</span><span class="sxs-lookup"><span data-stu-id="b7fd2-117">**Are there any usage limitations?**</span></span>

<span data-ttu-id="b7fd2-118">Aanbevelingen heeft Hallo na gebruik beperkingen:</span><span class="sxs-lookup"><span data-stu-id="b7fd2-118">Recommendations has hello following usage limitations:</span></span>

* <span data-ttu-id="b7fd2-119">Maximumaantal modellen per abonnement: 10</span><span class="sxs-lookup"><span data-stu-id="b7fd2-119">Maximum number of models per subscription: 10</span></span>
* <span data-ttu-id="b7fd2-120">Maximum aantal items dat een catalogus kan bevatten: 100.000</span><span class="sxs-lookup"><span data-stu-id="b7fd2-120">Maximum number of items that a catalog can hold: 100,000</span></span>
* <span data-ttu-id="b7fd2-121">maximum aantal gebruik punten die blijven Hallo is ~ 5,000,000.</span><span class="sxs-lookup"><span data-stu-id="b7fd2-121">hello maximum number of usage points that are kept is ~5,000,000.</span></span> <span data-ttu-id="b7fd2-122">Hallo oudste worden verwijderd als nieuwe wordt geüpload of gerapporteerd.</span><span class="sxs-lookup"><span data-stu-id="b7fd2-122">hello oldest will be deleted if new ones will be uploaded or reported.</span></span>
* <span data-ttu-id="b7fd2-123">Maximale grootte van gegevens die kunnen worden verzonden via e-mail (bijvoorbeeld importeren catalogusgegevens, gebruiksgegevens importeren) is 200 MB</span><span class="sxs-lookup"><span data-stu-id="b7fd2-123">Maximum size of data that can be sent in email (for example, import catalog data, import usage data) is 200 MB</span></span>
* <span data-ttu-id="b7fd2-124">Het aantal transacties per seconde (TPS) voor een model-build van aanbevelingen die niet actief is ~ 2 TPS.</span><span class="sxs-lookup"><span data-stu-id="b7fd2-124">Number of transactions per second (TPS) for a Recommendations model build that is not active is ~2 TPS.</span></span> <span data-ttu-id="b7fd2-125">Een build voor het model van aanbevelingen die actief is, kunt too20 TPS houdt.</span><span class="sxs-lookup"><span data-stu-id="b7fd2-125">A Recommendations model build that is active can hold up too20 TPS.</span></span>

## <a name="purchase-and-billing"></a><span data-ttu-id="b7fd2-126">Kopen en facturering</span><span class="sxs-lookup"><span data-stu-id="b7fd2-126">Purchase and Billing</span></span>
<span data-ttu-id="b7fd2-127">**Hoeveel kost aanbevelingen periode Hallo starten?**</span><span class="sxs-lookup"><span data-stu-id="b7fd2-127">**How much does Recommendations cost during hello launch period?**</span></span>

<span data-ttu-id="b7fd2-128">Aanbevelingen is een service op basis van abonnement.</span><span class="sxs-lookup"><span data-stu-id="b7fd2-128">Recommendations is a subscription-based service.</span></span> <span data-ttu-id="b7fd2-129">Opladen is gebaseerd op het volume van transacties per maand.</span><span class="sxs-lookup"><span data-stu-id="b7fd2-129">Charging is based on volume of transactions per month.</span></span> <span data-ttu-id="b7fd2-130">U kunt controleren Hallo [bieden pagina](https://datamarket.azure.com/dataset/amla/recommendations) in Microsoft Azure Marketplace voor informatie over prijzen.</span><span class="sxs-lookup"><span data-stu-id="b7fd2-130">You can check hello [offer page](https://datamarket.azure.com/dataset/amla/recommendations) in Microsoft Azure Marketplace for pricing information.</span></span>

<span data-ttu-id="b7fd2-131">**Zijn er kosten in verband met de aanbevelingen die bijhouden en opslaan van Gebruikersactiviteit voor mij?**</span><span class="sxs-lookup"><span data-stu-id="b7fd2-131">**Are there any costs associated with having Recommendations track and store user activity for me?**</span></span>

<span data-ttu-id="b7fd2-132">Niet op Hallo moment.</span><span class="sxs-lookup"><span data-stu-id="b7fd2-132">Not at hello moment.</span></span>

<span data-ttu-id="b7fd2-133">**Heeft aanbevelingen voor een gratis proefversie**</span><span class="sxs-lookup"><span data-stu-id="b7fd2-133">**Does Recommendations have a free trial?**</span></span>

<span data-ttu-id="b7fd2-134">Er is een gratis spoor die beperkte too10, 000 transacties per maand.</span><span class="sxs-lookup"><span data-stu-id="b7fd2-134">There is a free trail which is restricted too10,000 transactions per month.</span></span>

<span data-ttu-id="b7fd2-135">**Wanneer wordt ik gefactureerd voor aanbevelingen?**</span><span class="sxs-lookup"><span data-stu-id="b7fd2-135">**When will I be billed for Recommendations?**</span></span>

<span data-ttu-id="b7fd2-136">Een betaald abonnement is geen abonnement waarvoor maandelijks een vast bedrag is.</span><span class="sxs-lookup"><span data-stu-id="b7fd2-136">A paid subscription is any subscription for which there is a monthly fee.</span></span> <span data-ttu-id="b7fd2-137">Wanneer u een betaald abonnement aanschaft, er zijn direct in rekening gebracht voor Hallo eerst gebruik van de maand.</span><span class="sxs-lookup"><span data-stu-id="b7fd2-137">When you purchase a paid subscription, you are immediately charged for hello first month's use.</span></span> <span data-ttu-id="b7fd2-138">U Hallo hoeveelheid die is gekoppeld aan Hallo aanbieding op de pagina Hallo-abonnement (plus btw) in rekening worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="b7fd2-138">You are charged hello amount that is associated with hello offer on hello subscription page (plus applicable taxes).</span></span> <span data-ttu-id="b7fd2-139">Deze maandelijkse kosten wordt gemaakt van elke maand op Hallo dezelfde datum als uw oorspronkelijke aankoop kalender totdat u Hallo abonnement annuleren.</span><span class="sxs-lookup"><span data-stu-id="b7fd2-139">This monthly charge is made each month on hello same calendar date as your original purchase until you cancel hello subscription.</span></span> 

<span data-ttu-id="b7fd2-140">**Hoe voer ik een upgrade tooa hogere tier-service?**</span><span class="sxs-lookup"><span data-stu-id="b7fd2-140">**How do I upgrade tooa higher tier service?**</span></span>

<span data-ttu-id="b7fd2-141">U kunt kopen of bijwerken van uw abonnement op Hallo [bieden pagina](https://datamarket.azure.com/dataset/amla/recommendations) pagina op Microsoft Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="b7fd2-141">You can buy or update your subscription from hello [offer page](https://datamarket.azure.com/dataset/amla/recommendations) page on Microsoft Azure Marketplace.</span></span>

<span data-ttu-id="b7fd2-142">Wanneer u een abonnement upgrade:</span><span class="sxs-lookup"><span data-stu-id="b7fd2-142">When you upgrade a subscription:</span></span>

* <span data-ttu-id="b7fd2-143">Transacties die op uw oude abonnement nog niet tooyour nieuw abonnement toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="b7fd2-143">Transactions that are remaining on your old subscription are not added tooyour new subscription.</span></span> 
* <span data-ttu-id="b7fd2-144">U betaalt volledige prijs voor het nieuwe abonnement hello, hoewel u hebt niet-gebruikte transacties op uw oude abonnement.</span><span class="sxs-lookup"><span data-stu-id="b7fd2-144">You pay full price for hello new subscription, even though you have unused transactions on your old subscription.</span></span>

<span data-ttu-id="b7fd2-145">Proces tooupgrade een abonnement:</span><span class="sxs-lookup"><span data-stu-id="b7fd2-145">Process tooupgrade a subscription:</span></span>

* <span data-ttu-id="b7fd2-146">Nevigate toohello [bieden pagina](https://datamarket.azure.com/dataset/amla/recommendations).</span><span class="sxs-lookup"><span data-stu-id="b7fd2-146">Nevigate toohello [offer page](https://datamarket.azure.com/dataset/amla/recommendations).</span></span>
* <span data-ttu-id="b7fd2-147">Meld u toohello Marketplace als u al bent niet aangemeld.</span><span class="sxs-lookup"><span data-stu-id="b7fd2-147">Sign in toohello Marketplace if you aren't already Signed in.</span></span>
* <span data-ttu-id="b7fd2-148">Klik in het rechterdeelvenster Hallo worden alle Hallo beschikbare abonnementen weergegeven.</span><span class="sxs-lookup"><span data-stu-id="b7fd2-148">In hello right pane, all hello available plans are listed.</span></span> <span data-ttu-id="b7fd2-149">Klik op het keuzerondje Hallo voor Hallo plan gewenste tooupgrade aan.</span><span class="sxs-lookup"><span data-stu-id="b7fd2-149">Click hello radio button for hello plan you want tooupgrade to.</span></span>
* <span data-ttu-id="b7fd2-150">Als u wilt dat tooupgrade, klikt u op **OK**.</span><span class="sxs-lookup"><span data-stu-id="b7fd2-150">If you want tooupgrade, click **OK**.</span></span> <span data-ttu-id="b7fd2-151">Als u niet dat tooupgrade wilt, klikt u op **annuleren**.</span><span class="sxs-lookup"><span data-stu-id="b7fd2-151">If you do not want tooupgrade, click **Cancel**.</span></span>

<span data-ttu-id="b7fd2-152">**Belangrijke** zorgvuldig lezen Hallo dialoogvenster voordat u bijwerkt, omdat er gevolgen voor facturering en het gebruik.</span><span class="sxs-lookup"><span data-stu-id="b7fd2-152">**Important** Carefully read hello dialog box before you upgrade because there are billing and use implications.</span></span>

<span data-ttu-id="b7fd2-153">**Wanneer wordt mijn abonnement tooRecommendations eindigen?**</span><span class="sxs-lookup"><span data-stu-id="b7fd2-153">**When will my subscription tooRecommendations end?**</span></span>

<span data-ttu-id="b7fd2-154">Uw abonnement wordt beëindigd als u deze annuleren.</span><span class="sxs-lookup"><span data-stu-id="b7fd2-154">Your subscription will end when you cancel it.</span></span> <span data-ttu-id="b7fd2-155">Als u toocancel wilt uw abonnementen, Zie Hallo instructies te volgen.</span><span class="sxs-lookup"><span data-stu-id="b7fd2-155">If you would like toocancel your subscriptions, see hello following instructions.</span></span>

<span data-ttu-id="b7fd2-156">**Hoe annuleer ik mijn abonnement aanbevelingen**</span><span class="sxs-lookup"><span data-stu-id="b7fd2-156">**How do I cancel my Recommendations subscription?**</span></span>

<span data-ttu-id="b7fd2-157">toocancel uw abonnement, gebruik hello te volgen stappen.</span><span class="sxs-lookup"><span data-stu-id="b7fd2-157">toocancel your subscription, use hello following steps.</span></span> <span data-ttu-id="b7fd2-158">Als uw huidige abonnement een betaald abonnement, wordt uw abonnement actief blijft tot einde van de huidige periode facturering Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="b7fd2-158">If your current subscription is a paid subscription, your subscription continues in effect until hello end of hello current billing period.</span></span> <span data-ttu-id="b7fd2-159">Als u moet de annulering toobe effectieve onmiddellijk hello, contact met ons op [Microsoft Support](https://support.microsoft.com/oas/default.aspx?gprid=17024&st=1&wfxredirect=1&sd=gn).</span><span class="sxs-lookup"><span data-stu-id="b7fd2-159">If you need hello cancellation toobe effective immediately, contact us at [Microsoft Support](https://support.microsoft.com/oas/default.aspx?gprid=17024&st=1&wfxredirect=1&sd=gn).</span></span>

<span data-ttu-id="b7fd2-160">**Opmerking** geen restitutie krijgt als u voordat Hallo einde van een factureringsperiode of voor niet-gebruikte transacties in een factureringsperiode annuleert.</span><span class="sxs-lookup"><span data-stu-id="b7fd2-160">**Note** No refund is given if you cancel before hello end of a billing period or for unused transactions in a billing period.</span></span>

* <span data-ttu-id="b7fd2-161">Navigeer toohello [bieden pagina](https://datamarket.azure.com/dataset/amla/recommendations).</span><span class="sxs-lookup"><span data-stu-id="b7fd2-161">Navigate toohello [offer page](https://datamarket.azure.com/dataset/amla/recommendations).</span></span>
* <span data-ttu-id="b7fd2-162">Meld u toohello Marketplace als u al bent niet aangemeld.</span><span class="sxs-lookup"><span data-stu-id="b7fd2-162">Sign in toohello Marketplace if you aren't already Signed in.</span></span>
* <span data-ttu-id="b7fd2-163">Klik op **annuleren** toohello rechts van de naam van de dataset Hallo en status.</span><span class="sxs-lookup"><span data-stu-id="b7fd2-163">Click **Cancel** toohello right of hello dataset name and status.</span></span> <span data-ttu-id="b7fd2-164">U kunt dit abonnement totdat het Hallo-einde van de huidige financieel periode of de Transactielimiet van uw Hallo is bereikt (indien dit eerder gebeurt eerst).</span><span class="sxs-lookup"><span data-stu-id="b7fd2-164">You can use this subscription until hello end of hello current billing period or your transaction limit is reached (whichever occurs first).</span></span>

<span data-ttu-id="b7fd2-165">Als u uw abonnement dat wilt onmiddellijk zodat u een nieuw abonnement kunt aanschaffen bestand een ticket op toocancel [Microsoft Support](https://support.microsoft.com/oas/default.aspx?gprid=17024&st=1&wfxredirect=1&sd=gn).</span><span class="sxs-lookup"><span data-stu-id="b7fd2-165">If you would like toocancel your subscription immediately so you can purchase a new subscription, file a ticket at [Microsoft Support](https://support.microsoft.com/oas/default.aspx?gprid=17024&st=1&wfxredirect=1&sd=gn).</span></span>

## <a name="getting-started-with-recommendations"></a><span data-ttu-id="b7fd2-166">Aan de slag met aanbevelingen</span><span class="sxs-lookup"><span data-stu-id="b7fd2-166">Getting started with Recommendations</span></span>
<span data-ttu-id="b7fd2-167">**Is de aanbevelingen voor mij?**</span><span class="sxs-lookup"><span data-stu-id="b7fd2-167">**Is Recommendations for me?**</span></span> 

<span data-ttu-id="b7fd2-168">Aanbevelingen in Machine Learning is bedoeld voor organisaties en bedrijven die afhankelijk van aanbevelingen toocross verkopen en Upsell producten of services tootheir klanten zijn.</span><span class="sxs-lookup"><span data-stu-id="b7fd2-168">Recommendations in Machine Learning is for organizations and businesses that rely on recommendations toocross-sell and up-sell products or services tootheir customers.</span></span> <span data-ttu-id="b7fd2-169">Als u beschikt over een website klantgerichte, een verkoopmedewerkers, een inwendige verkoopmedewerkers of een aanroep center, en als u een catalogus van meer dan een paar dozijn producten of services aanbiedt, uw bedrijfsresultaten kunnen profiteren van aanbevelingen.</span><span class="sxs-lookup"><span data-stu-id="b7fd2-169">If you have a customer-facing website, a sales force, an inside sales force, or a call center, and if you offer a catalog of more than a few dozen products or services, your bottom line may benefit from using Recommendations.</span></span> 

<span data-ttu-id="b7fd2-170">Experimenteren met aanbevelingen is ontworpen toobe redelijk eenvoudig.</span><span class="sxs-lookup"><span data-stu-id="b7fd2-170">Experimenting with Recommendations is designed toobe fairly simple.</span></span> <span data-ttu-id="b7fd2-171">Hallo huidige API-versie vereist basic programmeren.</span><span class="sxs-lookup"><span data-stu-id="b7fd2-171">hello current API-based version requires basic programming skills.</span></span> <span data-ttu-id="b7fd2-172">Als u hulp nodig hebt, contact met de Hallo leverancier die ontwikkeld van uw website.</span><span class="sxs-lookup"><span data-stu-id="b7fd2-172">If you need assistance, contact hello vendor who developed your website.</span></span> <span data-ttu-id="b7fd2-173">Als er een interne IT-afdeling of een interne ontwikkelaar, moeten ze kunnen tooget aanbevelingen toowork voor u zijn.</span><span class="sxs-lookup"><span data-stu-id="b7fd2-173">If you have an internal IT department or an in-house developer, they should be able tooget Recommendations toowork for you.</span></span> 

<span data-ttu-id="b7fd2-174">**Wat zijn de vereisten voor het instellen van aanbevelingen Hallo?**</span><span class="sxs-lookup"><span data-stu-id="b7fd2-174">**What are hello prerequisites for setting up Recommendations?**</span></span>

<span data-ttu-id="b7fd2-175">Aanbevelingen vereist dat u een logboek van de gebruiker te zien krijgt als deze zich verhoudt tooyour catalogus.</span><span class="sxs-lookup"><span data-stu-id="b7fd2-175">Recommendations requires that you have a log of user choices as it relates tooyour catalog.</span></span> <span data-ttu-id="b7fd2-176">Als u dergelijke logboek hebt en u een klant gerichte website hebt, kunnen aanbevelingen gebruikersactiviteit verzamelen voor u.</span><span class="sxs-lookup"><span data-stu-id="b7fd2-176">If you don't have such a log and you do have a customer facing website, Recommendations can collect user activity for you.</span></span> 

<span data-ttu-id="b7fd2-177">Aanbevelingen moet ook een catalogus met producten en services.</span><span class="sxs-lookup"><span data-stu-id="b7fd2-177">Recommendations also requires a catalog of your products or services.</span></span> <span data-ttu-id="b7fd2-178">Als u geen Hallo catalogus hebt, kunnen aanbevelingen Hallo werkelijke klant gebruiksgegevens gebruiken en een catalogus distill.</span><span class="sxs-lookup"><span data-stu-id="b7fd2-178">If you don't have hello catalog, Recommendations can use hello actual customer usage data and distill a catalog.</span></span> <span data-ttu-id="b7fd2-179">Een impliciete catalogus bevat items die niet zijn gemeld als onderdeel van de gebruikerstransacties.</span><span class="sxs-lookup"><span data-stu-id="b7fd2-179">An implied catalog will not include items that were not reported as part of user transactions.</span></span>

<span data-ttu-id="b7fd2-180">**Hoe stel ik aanbevelingen voor Hallo eerst?**</span><span class="sxs-lookup"><span data-stu-id="b7fd2-180">**How do I set up Recommendations for hello first time?**</span></span>

<span data-ttu-id="b7fd2-181">Na [geabonneerde](https://datamarket.azure.com/dataset/amla/recommendations) tooRecommendations, moet u Hallo API-documentatie in Hallo [aanbevelingen in Azure Machine Learning - introductiehandleiding](machine-learning-recommendation-api-quick-start-guide.md) tooset Hallo-service.</span><span class="sxs-lookup"><span data-stu-id="b7fd2-181">After [subscribing](https://datamarket.azure.com/dataset/amla/recommendations) tooRecommendations, you should use hello API documentation in hello [Azure Machine Learning Recommendations - Quick Start Guide](machine-learning-recommendation-api-quick-start-guide.md) tooset up hello service.</span></span>

<span data-ttu-id="b7fd2-182">**Waar vind ik API-documentatie**</span><span class="sxs-lookup"><span data-stu-id="b7fd2-182">**Where can I find API documentation?**</span></span> 

<span data-ttu-id="b7fd2-183">Hallo API-documentatie is [aanbevelingen voor Azure Machine Learning-introductiehandleiding](machine-learning-recommendation-api-quick-start-guide.md).</span><span class="sxs-lookup"><span data-stu-id="b7fd2-183">hello API documentation is [Azure Machine Learning Recommendations -Quick Start Guide](machine-learning-recommendation-api-quick-start-guide.md).</span></span>

<span data-ttu-id="b7fd2-184">**Wat opties doen er tooupload catalogus en gebruik gegevens tooRecommendations?**</span><span class="sxs-lookup"><span data-stu-id="b7fd2-184">**What options do I have tooupload catalog and usage data tooRecommendations?**</span></span>

<span data-ttu-id="b7fd2-185">Hebt u twee opties voor het uploaden van uw data catalog en het gebruik: U kunt Hallo gegevens exporteren uit uw CRM-systeem of andere logboeken en tooRecommendations te uploaden of u labels tooyour website die u activiteiten van gebruikers bijhouden wilt kunt toevoegen.</span><span class="sxs-lookup"><span data-stu-id="b7fd2-185">You have two options for uploading your catalog and usage data: You can export hello data from your CRM system or other logs and upload it tooRecommendations, or you can add tags tooyour website that will track user activities.</span></span> <span data-ttu-id="b7fd2-186">Als u de laatste Hallo-methode gebruikt, wordt de Hallo gegevens worden opgeslagen in Azure.</span><span class="sxs-lookup"><span data-stu-id="b7fd2-186">If you use hello latter method, hello data will be stored in Azure.</span></span>

## <a name="maintenance-and-support"></a><span data-ttu-id="b7fd2-187">Onderhoud en ondersteuning</span><span class="sxs-lookup"><span data-stu-id="b7fd2-187">Maintenance and support</span></span>
<span data-ttu-id="b7fd2-188">**Hoe groot mag mijn gegevensset zijn?**</span><span class="sxs-lookup"><span data-stu-id="b7fd2-188">**How large can my data set be?**</span></span>

<span data-ttu-id="b7fd2-189">Elke set gegevens kan bevatten too100, 000 catalogusitems en too2048 MB van gebruiksgegevens.</span><span class="sxs-lookup"><span data-stu-id="b7fd2-189">Each data set can contain up too100,000 catalog items and up too2048 MB of usage data.</span></span>
<span data-ttu-id="b7fd2-190">Bovendien kan een abonnement bevatten van gegevensverzamelingen too10 (modellen).</span><span class="sxs-lookup"><span data-stu-id="b7fd2-190">In addition, a subscription can contain up too10 data sets (models).</span></span>

<span data-ttu-id="b7fd2-191">**Waar vind ik technische ondersteuning voor aanbevelingen**</span><span class="sxs-lookup"><span data-stu-id="b7fd2-191">**Where can I get technical support for Recommendations?**</span></span>

<span data-ttu-id="b7fd2-192">Technische ondersteuning is beschikbaar op Hallo [ondersteuning van Microsoft Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=MachineLearning) site.</span><span class="sxs-lookup"><span data-stu-id="b7fd2-192">Technical support is available on hello [Microsoft Azure Support](https://social.msdn.microsoft.com/forums/azure/home?forum=MachineLearning) site.</span></span>

<span data-ttu-id="b7fd2-193">**Waar vind ik Hallo gebruiksvoorwaarden**</span><span class="sxs-lookup"><span data-stu-id="b7fd2-193">**Where can I find hello terms of use?**</span></span>

<span data-ttu-id="b7fd2-194">[Microsoft Azure Machine Learning-aanbevelingen API servicevoorwaarden](https://datamarket.azure.com/dataset/amla/recommendations#terms).</span><span class="sxs-lookup"><span data-stu-id="b7fd2-194">[Microsoft Azure Machine Learning Recommendations API Terms of Service](https://datamarket.azure.com/dataset/amla/recommendations#terms).</span></span>


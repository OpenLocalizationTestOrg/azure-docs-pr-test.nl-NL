---
title: Automatisch schalen en App Service-omgeving v1
description: Automatisch schalen en App-serviceomgeving
services: app-service
documentationcenter: 
author: btardif
manager: erikre
editor: 
ms.assetid: c23af2d8-d370-4b1f-9b3e-8782321ddccb
ms.service: app-service
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/11/2017
ms.author: ccompy
ms.openlocfilehash: f32affd285f3918feb0e893543f2a28f678b7b10
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="autoscaling-and-app-service-environment-v1"></a><span data-ttu-id="2727f-103">Automatisch schalen en App Service-omgeving v1</span><span class="sxs-lookup"><span data-stu-id="2727f-103">Autoscaling and App Service Environment v1</span></span>

> [!NOTE]
> <span data-ttu-id="2727f-104">In dit artikel gaat over de v1 App Service-omgeving.</span><span class="sxs-lookup"><span data-stu-id="2727f-104">This article is about the App Service Environment v1.</span></span>  <span data-ttu-id="2727f-105">Er is een nieuwere versie van de App Service-omgeving die eenvoudiger te gebruiken en wordt uitgevoerd op krachtiger infrastructuur.</span><span class="sxs-lookup"><span data-stu-id="2727f-105">There is a newer version of the App Service Environment that is easier  to use and runs on more powerful infrastructure.</span></span> <span data-ttu-id="2727f-106">Voor meer informatie over de nieuwe versie begin met het [Inleiding tot de App-serviceomgeving](../app-service/app-service-environment/intro.md).</span><span class="sxs-lookup"><span data-stu-id="2727f-106">To learn more about the new version start with the [Introduction to the App  Service Environment](../app-service/app-service-environment/intro.md).</span></span>
> 

<span data-ttu-id="2727f-107">Ondersteuning voor Azure App Service-omgevingen *automatisch schalen*.</span><span class="sxs-lookup"><span data-stu-id="2727f-107">Azure App Service environments support *autoscaling*.</span></span> <span data-ttu-id="2727f-108">U kunt afzonderlijke werknemersgroepen automatisch schalen op basis van de metrische gegevens of schema.</span><span class="sxs-lookup"><span data-stu-id="2727f-108">You can autoscale individual worker pools based on metrics or schedule.</span></span>

![Opties voor automatisch schalen voor een worker-groep.][intro]

<span data-ttu-id="2727f-110">Automatisch schalen optimaliseert uw Resourcegebruik door automatisch vergroten en verkleinen van een App Service-omgeving om aanpassen aan uw budget en of profiel laden.</span><span class="sxs-lookup"><span data-stu-id="2727f-110">Autoscaling optimizes your resource utilization by automatically growing and shrinking an App Service environment to fit your budget and or load profile.</span></span>

## <a name="configure-worker-pool-autoscale"></a><span data-ttu-id="2727f-111">Worker-groep automatisch schalen configureren</span><span class="sxs-lookup"><span data-stu-id="2727f-111">Configure worker pool autoscale</span></span>
<span data-ttu-id="2727f-112">U hebt toegang tot de functionaliteit voor automatisch schalen van de **instellingen** tabblad van de worker-groep.</span><span class="sxs-lookup"><span data-stu-id="2727f-112">You can access the autoscale functionality from the **Settings** tab of the worker pool.</span></span>

![Tabblad instellingen van de werknemer van toepassingen.][settings-scale]

<span data-ttu-id="2727f-114">Vanuit is dat de interface moet bekend zijn omdat het dat u ziet wanneer u een App Service-plan schalen dezelfde ervaring.</span><span class="sxs-lookup"><span data-stu-id="2727f-114">From there, the interface should be fairly familiar since it is the same experience that you see when you scale an App Service plan.</span></span> 

![De instellingen handmatig schalen.][scale-manual]

<span data-ttu-id="2727f-116">U kunt ook een profiel voor automatisch schalen configureren.</span><span class="sxs-lookup"><span data-stu-id="2727f-116">You can also configure an autoscale profile.</span></span>

![Instellingen voor automatisch schalen.][scale-profile]

<span data-ttu-id="2727f-118">Profielen voor automatisch schalen zijn handig om beperkingen op schaal.</span><span class="sxs-lookup"><span data-stu-id="2727f-118">Autoscale profiles are useful to set limits on your scale.</span></span> <span data-ttu-id="2727f-119">Op deze manier kunt u een consistente prestaties ervaren door een ondergrens schaalwaarde (1) en een voorspelbare uitgaven initiaal door in te stellen van een bovengrens (2) hebben.</span><span class="sxs-lookup"><span data-stu-id="2727f-119">This way, you can have a consistent performance experience by setting a lower bound scale value (1) and a predictable spend cap by setting an upper bound (2).</span></span>

![Scale-instellingen in het profiel.][scale-profile2]

<span data-ttu-id="2727f-121">Nadat u een profiel definieert, kunt u regels voor automatisch schalen schaal omhoog of omlaag het aantal exemplaren in de worker-groep binnen de grenzen die zijn gedefinieerd door het profiel kunt toevoegen.</span><span class="sxs-lookup"><span data-stu-id="2727f-121">After you define a profile, you can add autoscale rules to scale up or down the number of instances in the worker pool within the bounds defined by the profile.</span></span> <span data-ttu-id="2727f-122">Regels voor automatisch schalen die zijn gebaseerd op metrische gegevens.</span><span class="sxs-lookup"><span data-stu-id="2727f-122">Autoscale rules are based on metrics.</span></span>

![Schaalregel.][scale-rule]

 <span data-ttu-id="2727f-124">Een werknemersgroep of de front-metrische gegevens kan worden gebruikt voor het definiëren van regels voor automatisch schalen.</span><span class="sxs-lookup"><span data-stu-id="2727f-124">Any worker pool or front-end metrics can be used to define autoscale rules.</span></span> <span data-ttu-id="2727f-125">Deze metrische gegevens zijn dezelfde metrische gegevens kunt u meldingen instellen voor of bewaken in de resource-blade-grafieken.</span><span class="sxs-lookup"><span data-stu-id="2727f-125">These metrics are the same metrics you can monitor in the resource blade graphs or set alerts for.</span></span>

## <a name="autoscale-example"></a><span data-ttu-id="2727f-126">Voorbeeld voor automatisch schalen</span><span class="sxs-lookup"><span data-stu-id="2727f-126">Autoscale example</span></span>
<span data-ttu-id="2727f-127">Automatisch schalen van een App Service-omgeving kan best worden geïllustreerd door het doorlopen van een scenario.</span><span class="sxs-lookup"><span data-stu-id="2727f-127">Autoscale of an App Service environment can best be illustrated by walking through a scenario.</span></span>

<span data-ttu-id="2727f-128">Dit artikel wordt uitgelegd van de benodigde overwegingen bij het instellen van automatisch schalen.</span><span class="sxs-lookup"><span data-stu-id="2727f-128">This article explains all the necessary considerations when you set up autoscale.</span></span> <span data-ttu-id="2727f-129">Het artikel doorloopt u de interacties die een rol spelen als u automatisch schalen App Service-omgevingen die worden gehost in App Service-omgeving.</span><span class="sxs-lookup"><span data-stu-id="2727f-129">The article walks you through the interactions that come into play when you factor in autoscaling App Service environments that are hosted in App Service Environment.</span></span>

### <a name="scenario-introduction"></a><span data-ttu-id="2727f-130">Scenario Inleiding</span><span class="sxs-lookup"><span data-stu-id="2727f-130">Scenario introduction</span></span>
<span data-ttu-id="2727f-131">Frank is een sysadmin voor een onderneming die een deel van de werkbelastingen die hij beheert is gemigreerd naar een App Service-omgeving.</span><span class="sxs-lookup"><span data-stu-id="2727f-131">Frank is a sysadmin for an enterprise who has migrated a portion of the workloads that he manages to an App Service environment.</span></span>

<span data-ttu-id="2727f-132">De App Service-omgeving is geconfigureerd voor handmatige scale als volgt:</span><span class="sxs-lookup"><span data-stu-id="2727f-132">The App Service environment is configured to manual scale as follows:</span></span>

* <span data-ttu-id="2727f-133">**FrontPage-ends:** 3</span><span class="sxs-lookup"><span data-stu-id="2727f-133">**Front ends:** 3</span></span>
* <span data-ttu-id="2727f-134">**Worker-groep 1**: 10</span><span class="sxs-lookup"><span data-stu-id="2727f-134">**Worker pool 1**: 10</span></span>
* <span data-ttu-id="2727f-135">**Werknemersgroep 2**: 5</span><span class="sxs-lookup"><span data-stu-id="2727f-135">**Worker pool 2**: 5</span></span>
* <span data-ttu-id="2727f-136">**Werknemersgroep 3**: 5</span><span class="sxs-lookup"><span data-stu-id="2727f-136">**Worker pool 3**: 5</span></span>

<span data-ttu-id="2727f-137">Worker-groep 1 wordt gebruikt voor productieworkloads, hoewel werknemersgroep 2 en 3 van werknemersgroep worden gebruikt voor kwaliteit assurance (QA) en ontwikkeling werkbelastingen.</span><span class="sxs-lookup"><span data-stu-id="2727f-137">Worker pool 1 is used for production workloads, while worker pool 2 and worker pool 3 are used for quality assurance (QA) and development workloads.</span></span>

<span data-ttu-id="2727f-138">De App Service-abonnementen voor QA en dev zijn geconfigureerd voor handmatige schaal.</span><span class="sxs-lookup"><span data-stu-id="2727f-138">The App Service plans for QA and dev are configured to manual scale.</span></span> <span data-ttu-id="2727f-139">De productie-App Service-abonnement is ingesteld op automatisch schalen om te gaan met de verschillen in de belasting en verkeer.</span><span class="sxs-lookup"><span data-stu-id="2727f-139">The production App Service plan is set to autoscale to deal with variations in load and traffic.</span></span>

<span data-ttu-id="2727f-140">Frank zeer vertrouwd is met de toepassing.</span><span class="sxs-lookup"><span data-stu-id="2727f-140">Frank is very familiar with the application.</span></span> <span data-ttu-id="2727f-141">Hij weet dat de piekuren voor load tussen 9:00 uur en 18:00 uur zijn omdat dit een line-of-business (LOB)-toepassing die werknemers gebruiken terwijl ze op kantoor zijn.</span><span class="sxs-lookup"><span data-stu-id="2727f-141">He knows that the peak hours for load are between 9:00 AM and 6:00 PM because this is a line-of-business (LOB) application that employees use while they are in the office.</span></span> <span data-ttu-id="2727f-142">Gebruik zakt hierna wanneer gebruikers klaar bent voor die dag.</span><span class="sxs-lookup"><span data-stu-id="2727f-142">Usage drops after that when users are done for that day.</span></span> <span data-ttu-id="2727f-143">Buiten de piekuren is er nog steeds bepaalde laden omdat gebruikers toegang de app op afstand tot hebben via hun mobiele apparaten of thuiscomputers.</span><span class="sxs-lookup"><span data-stu-id="2727f-143">Outside peak hours, there is still some load because users can access the app remotely by using their mobile devices or home PCs.</span></span> <span data-ttu-id="2727f-144">De productie-App Service-abonnement is al geconfigureerd voor automatisch schalen op basis van CPU-gebruik met de volgende regels:</span><span class="sxs-lookup"><span data-stu-id="2727f-144">The production App Service plan is already configured to autoscale based on CPU usage with the following rules:</span></span>

![Specifieke instellingen voor LOB-app.][asp-scale]

| <span data-ttu-id="2727f-146">**Profiel voor automatisch schalen: weekdagen-App Service-abonnement**</span><span class="sxs-lookup"><span data-stu-id="2727f-146">**Autoscale profile – Weekdays – App Service plan**</span></span> | <span data-ttu-id="2727f-147">**Profiel voor automatisch schalen: tijdens het weekend-App Service-abonnement**</span><span class="sxs-lookup"><span data-stu-id="2727f-147">**Autoscale profile – Weekends – App Service plan**</span></span> |
| --- | --- |
| <span data-ttu-id="2727f-148">**Naam:** profiel weekdag</span><span class="sxs-lookup"><span data-stu-id="2727f-148">**Name:** Weekday profile</span></span> |<span data-ttu-id="2727f-149">**Naam:** profiel voor het Weekend</span><span class="sxs-lookup"><span data-stu-id="2727f-149">**Name:** Weekend profile</span></span> |
| <span data-ttu-id="2727f-150">**Schaal door:** regels voor planning en prestaties</span><span class="sxs-lookup"><span data-stu-id="2727f-150">**Scale by:** Schedule and performance rules</span></span> |<span data-ttu-id="2727f-151">**Schaal door:** regels voor planning en prestaties</span><span class="sxs-lookup"><span data-stu-id="2727f-151">**Scale by:** Schedule and performance rules</span></span> |
| <span data-ttu-id="2727f-152">**Profiel:** weekdagen</span><span class="sxs-lookup"><span data-stu-id="2727f-152">**Profile:** Weekdays</span></span> |<span data-ttu-id="2727f-153">**Profiel:** Weekend</span><span class="sxs-lookup"><span data-stu-id="2727f-153">**Profile:** Weekend</span></span> |
| <span data-ttu-id="2727f-154">**Type:** terugkeerpatroon</span><span class="sxs-lookup"><span data-stu-id="2727f-154">**Type:** Recurrence</span></span> |<span data-ttu-id="2727f-155">**Type:** terugkeerpatroon</span><span class="sxs-lookup"><span data-stu-id="2727f-155">**Type:** Recurrence</span></span> |
| <span data-ttu-id="2727f-156">**Doelbereik:** 5-20-exemplaren</span><span class="sxs-lookup"><span data-stu-id="2727f-156">**Target range:** 5 to 20 instances</span></span> |<span data-ttu-id="2727f-157">**Doelbereik:** 3 tot 10 exemplaren</span><span class="sxs-lookup"><span data-stu-id="2727f-157">**Target range:** 3 to 10 instances</span></span> |
| <span data-ttu-id="2727f-158">**Aantal dagen:** maandag, dinsdag, woensdag, donderdag en vrijdag</span><span class="sxs-lookup"><span data-stu-id="2727f-158">**Days:** Monday, Tuesday, Wednesday, Thursday, Friday</span></span> |<span data-ttu-id="2727f-159">**Aantal dagen:** zaterdag, zondag</span><span class="sxs-lookup"><span data-stu-id="2727f-159">**Days:** Saturday, Sunday</span></span> |
| <span data-ttu-id="2727f-160">**Begintijd:** 9:00 uur</span><span class="sxs-lookup"><span data-stu-id="2727f-160">**Start time:** 9:00 AM</span></span> |<span data-ttu-id="2727f-161">**Begintijd:** 9:00 uur</span><span class="sxs-lookup"><span data-stu-id="2727f-161">**Start time:** 9:00 AM</span></span> |
| <span data-ttu-id="2727f-162">**Tijdzone:** UTC-08</span><span class="sxs-lookup"><span data-stu-id="2727f-162">**Time zone:** UTC-08</span></span> |<span data-ttu-id="2727f-163">**Tijdzone:** UTC-08</span><span class="sxs-lookup"><span data-stu-id="2727f-163">**Time zone:** UTC-08</span></span> |
|  | |
| <span data-ttu-id="2727f-164">**Regel voor automatisch schalen (Omhoog schalen)**</span><span class="sxs-lookup"><span data-stu-id="2727f-164">**Autoscale rule (Scale Up)**</span></span> |<span data-ttu-id="2727f-165">**Regel voor automatisch schalen (Omhoog schalen)**</span><span class="sxs-lookup"><span data-stu-id="2727f-165">**Autoscale rule (Scale Up)**</span></span> |
| <span data-ttu-id="2727f-166">**Bron:** productie (App Service-omgeving)</span><span class="sxs-lookup"><span data-stu-id="2727f-166">**Resource:** Production (App Service Environment)</span></span> |<span data-ttu-id="2727f-167">**Bron:** productie (App Service-omgeving)</span><span class="sxs-lookup"><span data-stu-id="2727f-167">**Resource:** Production (App Service Environment)</span></span> |
| <span data-ttu-id="2727f-168">**Metrische gegevens:** CPU-percentage</span><span class="sxs-lookup"><span data-stu-id="2727f-168">**Metric:** CPU %</span></span> |<span data-ttu-id="2727f-169">**Metrische gegevens:** CPU-percentage</span><span class="sxs-lookup"><span data-stu-id="2727f-169">**Metric:** CPU %</span></span> |
| <span data-ttu-id="2727f-170">**Bewerking:** groter zijn dan 60%</span><span class="sxs-lookup"><span data-stu-id="2727f-170">**Operation:** Greater than 60%</span></span> |<span data-ttu-id="2727f-171">**Bewerking:** groter is dan 80%</span><span class="sxs-lookup"><span data-stu-id="2727f-171">**Operation:** Greater than 80%</span></span> |
| <span data-ttu-id="2727f-172">**Duur:** 5 minuten</span><span class="sxs-lookup"><span data-stu-id="2727f-172">**Duration:** 5 Minutes</span></span> |<span data-ttu-id="2727f-173">**Duur:** 10 minuten</span><span class="sxs-lookup"><span data-stu-id="2727f-173">**Duration:** 10 Minutes</span></span> |
| <span data-ttu-id="2727f-174">**Tijd aggregatie:** gemiddelde</span><span class="sxs-lookup"><span data-stu-id="2727f-174">**Time aggregation:** Average</span></span> |<span data-ttu-id="2727f-175">**Tijd aggregatie:** gemiddelde</span><span class="sxs-lookup"><span data-stu-id="2727f-175">**Time aggregation:** Average</span></span> |
| <span data-ttu-id="2727f-176">**Actie:** aantal verhogen door 2</span><span class="sxs-lookup"><span data-stu-id="2727f-176">**Action:** Increase count by 2</span></span> |<span data-ttu-id="2727f-177">**Actie:** aantal verhoogd met 1</span><span class="sxs-lookup"><span data-stu-id="2727f-177">**Action:** Increase count by 1</span></span> |
| <span data-ttu-id="2727f-178">**Cool omlaag (minuten):** 15</span><span class="sxs-lookup"><span data-stu-id="2727f-178">**Cool down (minutes):** 15</span></span> |<span data-ttu-id="2727f-179">**Cool omlaag (minuten):** 20</span><span class="sxs-lookup"><span data-stu-id="2727f-179">**Cool down (minutes):** 20</span></span> |
|  | |
| <span data-ttu-id="2727f-180">**Regel voor automatisch schalen (schaal omlaag)**</span><span class="sxs-lookup"><span data-stu-id="2727f-180">**Autoscale rule (Scale Down)**</span></span> |<span data-ttu-id="2727f-181">**Regel voor automatisch schalen (schaal omlaag)**</span><span class="sxs-lookup"><span data-stu-id="2727f-181">**Autoscale rule (Scale Down)**</span></span> |
| <span data-ttu-id="2727f-182">**Bron:** productie (App Service-omgeving)</span><span class="sxs-lookup"><span data-stu-id="2727f-182">**Resource:** Production (App Service Environment)</span></span> |<span data-ttu-id="2727f-183">**Bron:** productie (App Service-omgeving)</span><span class="sxs-lookup"><span data-stu-id="2727f-183">**Resource:** Production (App Service Environment)</span></span> |
| <span data-ttu-id="2727f-184">**Metrische gegevens:** CPU-percentage</span><span class="sxs-lookup"><span data-stu-id="2727f-184">**Metric:** CPU %</span></span> |<span data-ttu-id="2727f-185">**Metrische gegevens:** CPU-percentage</span><span class="sxs-lookup"><span data-stu-id="2727f-185">**Metric:** CPU %</span></span> |
| <span data-ttu-id="2727f-186">**Bewerking:** minder dan 30%</span><span class="sxs-lookup"><span data-stu-id="2727f-186">**Operation:** Less than 30%</span></span> |<span data-ttu-id="2727f-187">**Bewerking:** minder dan 20%</span><span class="sxs-lookup"><span data-stu-id="2727f-187">**Operation:** Less than 20%</span></span> |
| <span data-ttu-id="2727f-188">**Duur:** 10 minuten</span><span class="sxs-lookup"><span data-stu-id="2727f-188">**Duration:** 10 minutes</span></span> |<span data-ttu-id="2727f-189">**Duur:** 15 minuten</span><span class="sxs-lookup"><span data-stu-id="2727f-189">**Duration:** 15 minutes</span></span> |
| <span data-ttu-id="2727f-190">**Tijd aggregatie:** gemiddelde</span><span class="sxs-lookup"><span data-stu-id="2727f-190">**Time aggregation:** Average</span></span> |<span data-ttu-id="2727f-191">**Tijd aggregatie:** gemiddelde</span><span class="sxs-lookup"><span data-stu-id="2727f-191">**Time aggregation:** Average</span></span> |
| <span data-ttu-id="2727f-192">**Actie:** aantal verlagen door 1</span><span class="sxs-lookup"><span data-stu-id="2727f-192">**Action:** Decrease count by 1</span></span> |<span data-ttu-id="2727f-193">**Actie:** aantal verlagen door 1</span><span class="sxs-lookup"><span data-stu-id="2727f-193">**Action:** Decrease count by 1</span></span> |
| <span data-ttu-id="2727f-194">**Cool omlaag (minuten):** 20</span><span class="sxs-lookup"><span data-stu-id="2727f-194">**Cool down (minutes):** 20</span></span> |<span data-ttu-id="2727f-195">**Cool omlaag (minuten):** 10</span><span class="sxs-lookup"><span data-stu-id="2727f-195">**Cool down (minutes):** 10</span></span> |

### <a name="app-service-plan-inflation-rate"></a><span data-ttu-id="2727f-196">De snelheid van App Service-abonnement</span><span class="sxs-lookup"><span data-stu-id="2727f-196">App Service plan inflation rate</span></span>
<span data-ttu-id="2727f-197">App Service-abonnementen die zijn geconfigureerd voor automatisch schalen, doen dit met een maximale snelheid per uur.</span><span class="sxs-lookup"><span data-stu-id="2727f-197">App Service plans that are configured to autoscale do so at a maximum rate per hour.</span></span> <span data-ttu-id="2727f-198">Deze snelheid kan worden berekend op basis van de waarden op de regel voor automatisch schalen.</span><span class="sxs-lookup"><span data-stu-id="2727f-198">This rate can be calculated based on the values provided on the autoscale rule.</span></span>

<span data-ttu-id="2727f-199">Begrijpen en het berekenen van de *App Service plan de frequentie* is belangrijk voor App Service-omgeving voor automatisch schalen schaalwijzigingen in een werknemersgroep worden niet onmiddellijk.</span><span class="sxs-lookup"><span data-stu-id="2727f-199">Understanding and calculating the *App Service plan inflation rate* is important for App Service environment autoscale because scale changes to a worker pool are not instantaneous.</span></span>

<span data-ttu-id="2727f-200">De snelheid van App Service plan de is als volgt berekend:</span><span class="sxs-lookup"><span data-stu-id="2727f-200">The App Service plan inflation rate is calculated as follows:</span></span>

![De frequentie waarmee de berekening van App Service-abonnement.][ASP-Inflation]

<span data-ttu-id="2727f-202">Op basis van het automatisch schalen – omhoog schalen-regel voor het profiel werkdag van de productie-App Service-abonnement:</span><span class="sxs-lookup"><span data-stu-id="2727f-202">Based on the Autoscale – Scale Up rule for the Weekday profile of the production App Service plan:</span></span>

![App Service plan de snelheid voor weekdagen op basis van automatisch schalen – omhoog schalen-regel.][Equation1]

<span data-ttu-id="2727f-204">In het geval van het automatisch schalen – omhoog schalen-regel voor het Weekend profiel van de productie-App Service-abonnement, zou de formule omzetten in:</span><span class="sxs-lookup"><span data-stu-id="2727f-204">In the case of the Autoscale – Scale Up rule for the Weekend profile of the production App Service plan, the formula would resolve to:</span></span>

![App Service plan de snelheid voor het weekend op basis van automatisch schalen – omhoog schalen-regel.][Equation2]

<span data-ttu-id="2727f-206">Deze waarde kan ook worden berekend voor omlaag schalen bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="2727f-206">This value can also be calculated for scale-down operations.</span></span>

<span data-ttu-id="2727f-207">Op basis van het automatisch schalen: Scale omlaag regel voor het profiel werkdag van de productie-App Service-plan ziet dit er als volgt:</span><span class="sxs-lookup"><span data-stu-id="2727f-207">Based on the Autoscale – Scale Down rule for the Weekday profile of the production App Service plan, this would look as follows:</span></span>

![App Service plan de snelheid voor weekdagen op basis van automatisch schalen: Scale omlaag regel.][Equation3]

<span data-ttu-id="2727f-209">In het geval van het automatisch schalen: Scale omlaag regel voor het Weekend profiel van de productie-App Service-abonnement, zou de formule omzetten in:</span><span class="sxs-lookup"><span data-stu-id="2727f-209">In the case of the Autoscale – Scale Down rule for the Weekend profile of the production App Service plan, the formula would resolve to:</span></span>  

![App Service plan de snelheid voor het weekend op basis van automatisch schalen: Scale omlaag regel.][Equation4]

<span data-ttu-id="2727f-211">De productie-App Service-abonnement kan worden uitgebreid met een maximale snelheid van acht exemplaren per uur in de week en vier exemplaren per uur tijdens het weekend.</span><span class="sxs-lookup"><span data-stu-id="2727f-211">The production App Service plan can grow at a maximum rate of eight instances/hour during the week and four instances/hour during the weekend.</span></span> <span data-ttu-id="2727f-212">Deze kunt vrijgeven exemplaren met een maximale snelheid van vier exemplaren per uur in de week en zes exemplaren per uur tijdens het weekend.</span><span class="sxs-lookup"><span data-stu-id="2727f-212">It can release instances at a maximum rate of four instances/hour during the week and six instances/hour during weekends.</span></span>

<span data-ttu-id="2727f-213">Als meerdere App Service-abonnementen worden wordt gehost in een werknemersgroep, hebt u voor het berekenen van de *totale frequentie van de* als de som van de frequentie van de voor alle App Service-abonnementen die worden host in die worker-groep.</span><span class="sxs-lookup"><span data-stu-id="2727f-213">If multiple App Service plans are being hosted in a worker pool, you have to calculate the *total inflation rate* as the sum of the inflation rate for all the App Service plans that are being hosting in that worker pool.</span></span>

![De berekening van de totale frequentie van de voor meerdere App Service-abonnementen die in een werknemersgroep worden gehost.][ASP-Total-Inflation]

### <a name="use-the-app-service-plan-inflation-rate-to-define-worker-pool-autoscale-rules"></a><span data-ttu-id="2727f-215">Gebruik van de snelheid van App Service plan de worker-groep voor automatisch schalen regels definiëren</span><span class="sxs-lookup"><span data-stu-id="2727f-215">Use the App Service plan inflation rate to define worker pool autoscale rules</span></span>
<span data-ttu-id="2727f-216">Werknemer die host App Service-abonnementen die zijn geconfigureerd voor automatisch schalen moeten een buffer van de capaciteit worden toegewezen aan de groep.</span><span class="sxs-lookup"><span data-stu-id="2727f-216">Worker pools that host App Service plans that are configured to autoscale need to be allocated a buffer of capacity.</span></span> <span data-ttu-id="2727f-217">De buffer kunt u de bewerkingen voor automatisch schalen om te vergroten of verkleinen van de App Service-plan, indien nodig.</span><span class="sxs-lookup"><span data-stu-id="2727f-217">The buffer allows for the autoscale operations to grow and shrink the App Service plan as needed.</span></span> <span data-ttu-id="2727f-218">De minimale buffer zou de berekende totale App Service Plan de frequentie zijn.</span><span class="sxs-lookup"><span data-stu-id="2727f-218">The minimum buffer would be the calculated Total App Service Plan Inflation Rate.</span></span>

<span data-ttu-id="2727f-219">Omdat App Service-omgeving schaalbewerkingen even duren om toe te passen, wordt elke wijziging moet rekening houden met verder vraag verandert die optreden kunnen wanneer een schaalaanpassing uitgevoerd wordt.</span><span class="sxs-lookup"><span data-stu-id="2727f-219">Because App Service environment scale operations take some time to apply, any change should account for further demand changes that could happen while a scale operation is in progress.</span></span> <span data-ttu-id="2727f-220">Om te voldoen deze latentie, wordt u aangeraden de berekende totale App Service Plan de frequentie te gebruiken als het minimum aantal exemplaren die zijn toegevoegd voor elke bewerking automatisch schalen.</span><span class="sxs-lookup"><span data-stu-id="2727f-220">To accommodate this latency, we recommend that you use the calculated Total App Service Plan Inflation Rate as the minimum number of instances that are added for each autoscale operation.</span></span>

<span data-ttu-id="2727f-221">Met deze informatie kunt Frank het volgende profiel voor automatisch schalen en regels definiëren:</span><span class="sxs-lookup"><span data-stu-id="2727f-221">With this information, Frank can define the following autoscale profile and rules:</span></span>

![Regels voor automatisch schalen profiel voor LOB-voorbeeld.][Worker-Pool-Scale]

| <span data-ttu-id="2727f-223">**Profiel voor automatisch schalen: weekdagen**</span><span class="sxs-lookup"><span data-stu-id="2727f-223">**Autoscale profile – Weekdays**</span></span> | <span data-ttu-id="2727f-224">**Profiel voor automatisch schalen: tijdens het weekend**</span><span class="sxs-lookup"><span data-stu-id="2727f-224">**Autoscale profile – Weekends**</span></span> |
| --- | --- |
| <span data-ttu-id="2727f-225">**Naam:** profiel weekdag</span><span class="sxs-lookup"><span data-stu-id="2727f-225">**Name:** Weekday profile</span></span> |<span data-ttu-id="2727f-226">**Naam:** profiel voor het Weekend</span><span class="sxs-lookup"><span data-stu-id="2727f-226">**Name:** Weekend profile</span></span> |
| <span data-ttu-id="2727f-227">**Schaal door:** regels voor planning en prestaties</span><span class="sxs-lookup"><span data-stu-id="2727f-227">**Scale by:** Schedule and performance rules</span></span> |<span data-ttu-id="2727f-228">**Schaal door:** regels voor planning en prestaties</span><span class="sxs-lookup"><span data-stu-id="2727f-228">**Scale by:** Schedule and performance rules</span></span> |
| <span data-ttu-id="2727f-229">**Profiel:** weekdagen</span><span class="sxs-lookup"><span data-stu-id="2727f-229">**Profile:** Weekdays</span></span> |<span data-ttu-id="2727f-230">**Profiel:** Weekend</span><span class="sxs-lookup"><span data-stu-id="2727f-230">**Profile:** Weekend</span></span> |
| <span data-ttu-id="2727f-231">**Type:** terugkeerpatroon</span><span class="sxs-lookup"><span data-stu-id="2727f-231">**Type:** Recurrence</span></span> |<span data-ttu-id="2727f-232">**Type:** terugkeerpatroon</span><span class="sxs-lookup"><span data-stu-id="2727f-232">**Type:** Recurrence</span></span> |
| <span data-ttu-id="2727f-233">**Doelbereik:** 13 tot en met 25-exemplaren</span><span class="sxs-lookup"><span data-stu-id="2727f-233">**Target range:** 13 to 25 instances</span></span> |<span data-ttu-id="2727f-234">**Doelbereik:** 6 tot en met 15 exemplaren</span><span class="sxs-lookup"><span data-stu-id="2727f-234">**Target range:** 6 to 15 instances</span></span> |
| <span data-ttu-id="2727f-235">**Aantal dagen:** maandag, dinsdag, woensdag, donderdag en vrijdag</span><span class="sxs-lookup"><span data-stu-id="2727f-235">**Days:** Monday, Tuesday, Wednesday, Thursday, Friday</span></span> |<span data-ttu-id="2727f-236">**Aantal dagen:** zaterdag, zondag</span><span class="sxs-lookup"><span data-stu-id="2727f-236">**Days:** Saturday, Sunday</span></span> |
| <span data-ttu-id="2727f-237">**Begintijd:** 7:00 uur</span><span class="sxs-lookup"><span data-stu-id="2727f-237">**Start time:** 7:00 AM</span></span> |<span data-ttu-id="2727f-238">**Begintijd:** 9:00 uur</span><span class="sxs-lookup"><span data-stu-id="2727f-238">**Start time:** 9:00 AM</span></span> |
| <span data-ttu-id="2727f-239">**Tijdzone:** UTC-08</span><span class="sxs-lookup"><span data-stu-id="2727f-239">**Time zone:** UTC-08</span></span> |<span data-ttu-id="2727f-240">**Tijdzone:** UTC-08</span><span class="sxs-lookup"><span data-stu-id="2727f-240">**Time zone:** UTC-08</span></span> |
|  | |
| <span data-ttu-id="2727f-241">**Regel voor automatisch schalen (Omhoog schalen)**</span><span class="sxs-lookup"><span data-stu-id="2727f-241">**Autoscale rule (Scale Up)**</span></span> |<span data-ttu-id="2727f-242">**Regel voor automatisch schalen (Omhoog schalen)**</span><span class="sxs-lookup"><span data-stu-id="2727f-242">**Autoscale rule (Scale Up)**</span></span> |
| <span data-ttu-id="2727f-243">**Bron:** werknemersgroep 1</span><span class="sxs-lookup"><span data-stu-id="2727f-243">**Resource:** Worker pool 1</span></span> |<span data-ttu-id="2727f-244">**Bron:** werknemersgroep 1</span><span class="sxs-lookup"><span data-stu-id="2727f-244">**Resource:** Worker pool 1</span></span> |
| <span data-ttu-id="2727f-245">**Metrische gegevens:** WorkersAvailable</span><span class="sxs-lookup"><span data-stu-id="2727f-245">**Metric:** WorkersAvailable</span></span> |<span data-ttu-id="2727f-246">**Metrische gegevens:** WorkersAvailable</span><span class="sxs-lookup"><span data-stu-id="2727f-246">**Metric:** WorkersAvailable</span></span> |
| <span data-ttu-id="2727f-247">**Bewerking:** minder dan 8</span><span class="sxs-lookup"><span data-stu-id="2727f-247">**Operation:** Less than 8</span></span> |<span data-ttu-id="2727f-248">**Bewerking:** minder dan 3</span><span class="sxs-lookup"><span data-stu-id="2727f-248">**Operation:** Less than 3</span></span> |
| <span data-ttu-id="2727f-249">**Duur:** 20 minuten</span><span class="sxs-lookup"><span data-stu-id="2727f-249">**Duration:** 20 minutes</span></span> |<span data-ttu-id="2727f-250">**Duur:** 30 minuten</span><span class="sxs-lookup"><span data-stu-id="2727f-250">**Duration:** 30 minutes</span></span> |
| <span data-ttu-id="2727f-251">**Tijd aggregatie:** gemiddelde</span><span class="sxs-lookup"><span data-stu-id="2727f-251">**Time aggregation:** Average</span></span> |<span data-ttu-id="2727f-252">**Tijd aggregatie:** gemiddelde</span><span class="sxs-lookup"><span data-stu-id="2727f-252">**Time aggregation:** Average</span></span> |
| <span data-ttu-id="2727f-253">**Actie:** aantal verhogen door 8</span><span class="sxs-lookup"><span data-stu-id="2727f-253">**Action:** Increase count by 8</span></span> |<span data-ttu-id="2727f-254">**Actie:** aantal verhogen door 3</span><span class="sxs-lookup"><span data-stu-id="2727f-254">**Action:** Increase count by 3</span></span> |
| <span data-ttu-id="2727f-255">**Cool omlaag (minuten):** 180</span><span class="sxs-lookup"><span data-stu-id="2727f-255">**Cool down (minutes):** 180</span></span> |<span data-ttu-id="2727f-256">**Cool omlaag (minuten):** 180</span><span class="sxs-lookup"><span data-stu-id="2727f-256">**Cool down (minutes):** 180</span></span> |
|  | |
| <span data-ttu-id="2727f-257">**Regel voor automatisch schalen (schaal omlaag)**</span><span class="sxs-lookup"><span data-stu-id="2727f-257">**Autoscale rule (Scale Down)**</span></span> |<span data-ttu-id="2727f-258">**Regel voor automatisch schalen (schaal omlaag)**</span><span class="sxs-lookup"><span data-stu-id="2727f-258">**Autoscale rule (Scale Down)**</span></span> |
| <span data-ttu-id="2727f-259">**Bron:** werknemersgroep 1</span><span class="sxs-lookup"><span data-stu-id="2727f-259">**Resource:** Worker pool 1</span></span> |<span data-ttu-id="2727f-260">**Bron:** werknemersgroep 1</span><span class="sxs-lookup"><span data-stu-id="2727f-260">**Resource:** Worker pool 1</span></span> |
| <span data-ttu-id="2727f-261">**Metrische gegevens:** WorkersAvailable</span><span class="sxs-lookup"><span data-stu-id="2727f-261">**Metric:** WorkersAvailable</span></span> |<span data-ttu-id="2727f-262">**Metrische gegevens:** WorkersAvailable</span><span class="sxs-lookup"><span data-stu-id="2727f-262">**Metric:** WorkersAvailable</span></span> |
| <span data-ttu-id="2727f-263">**Bewerking:** groter is dan 8</span><span class="sxs-lookup"><span data-stu-id="2727f-263">**Operation:** Greater than 8</span></span> |<span data-ttu-id="2727f-264">**Bewerking:** groter is dan 3</span><span class="sxs-lookup"><span data-stu-id="2727f-264">**Operation:** Greater than 3</span></span> |
| <span data-ttu-id="2727f-265">**Duur:** 20 minuten</span><span class="sxs-lookup"><span data-stu-id="2727f-265">**Duration:** 20 minutes</span></span> |<span data-ttu-id="2727f-266">**Duur:** 15 minuten</span><span class="sxs-lookup"><span data-stu-id="2727f-266">**Duration:** 15 minutes</span></span> |
| <span data-ttu-id="2727f-267">**Tijd aggregatie:** gemiddelde</span><span class="sxs-lookup"><span data-stu-id="2727f-267">**Time aggregation:** Average</span></span> |<span data-ttu-id="2727f-268">**Tijd aggregatie:** gemiddelde</span><span class="sxs-lookup"><span data-stu-id="2727f-268">**Time aggregation:** Average</span></span> |
| <span data-ttu-id="2727f-269">**Actie:** aantal verlagen door 2</span><span class="sxs-lookup"><span data-stu-id="2727f-269">**Action:** Decrease count by 2</span></span> |<span data-ttu-id="2727f-270">**Actie:** aantal verlagen door 3</span><span class="sxs-lookup"><span data-stu-id="2727f-270">**Action:** Decrease count by 3</span></span> |
| <span data-ttu-id="2727f-271">**Cool omlaag (minuten):** 120</span><span class="sxs-lookup"><span data-stu-id="2727f-271">**Cool down (minutes):** 120</span></span> |<span data-ttu-id="2727f-272">**Cool omlaag (minuten):** 120</span><span class="sxs-lookup"><span data-stu-id="2727f-272">**Cool down (minutes):** 120</span></span> |

<span data-ttu-id="2727f-273">De doel-bereik dat is gedefinieerd in het profiel wordt berekend door de minimale exemplaren die zijn gedefinieerd in het profiel voor de App Service-abonnement + buffer.</span><span class="sxs-lookup"><span data-stu-id="2727f-273">The Target range defined in the profile is calculated by the minimum instances defined in the profile for the App Service plan + buffer.</span></span>

<span data-ttu-id="2727f-274">Het Maximum-bereik is de som van de maximale bereiken voor alle App Service-abonnementen die worden gehost in de worker-groep.</span><span class="sxs-lookup"><span data-stu-id="2727f-274">The Maximum range would be the sum of all the maximum ranges for all App Service plans hosted in the worker pool.</span></span>

<span data-ttu-id="2727f-275">Het aantal van de verhoging voor de schaal van regels moet worden ingesteld op ten minste 1 X-App Service Plan de frequentie voor scale-.</span><span class="sxs-lookup"><span data-stu-id="2727f-275">The Increase count for the scale up rules should be set to at least 1X the App Service Plan Inflation Rate for scale up.</span></span>

<span data-ttu-id="2727f-276">Verklein het aantal kan worden aangepast op een andere waarde tussen 1/2 X of 1 X-App Service Plan de frequentie voor schaal omlaag.</span><span class="sxs-lookup"><span data-stu-id="2727f-276">Decrease count can be adjusted to something between 1/2X or 1X the App Service Plan Inflation Rate for scale down.</span></span>

### <a name="autoscale-for-front-end-pool"></a><span data-ttu-id="2727f-277">Voor de front-toepassingen voor automatisch schalen</span><span class="sxs-lookup"><span data-stu-id="2727f-277">Autoscale for front-end pool</span></span>
<span data-ttu-id="2727f-278">Regels voor front-automatisch schalen zijn eenvoudiger dan voor werknemersgroepen.</span><span class="sxs-lookup"><span data-stu-id="2727f-278">Rules for front-end autoscale are simpler than for worker pools.</span></span> <span data-ttu-id="2727f-279">U dient voornamelijk om</span><span class="sxs-lookup"><span data-stu-id="2727f-279">Primarily, you should</span></span>  
<span data-ttu-id="2727f-280">Zorg ervoor dat de duur van de meting en de vernieuwingstimer cooldown rekening houdt scale-bewerkingen op een App Service-abonnement zijn niet onmiddellijk.</span><span class="sxs-lookup"><span data-stu-id="2727f-280">make sure that duration of the measurement and the cooldown timers consider that scale operations on an App Service plan are not instantaneous.</span></span>

<span data-ttu-id="2727f-281">In dit scenario weet Frank dat de frequentie van fouten neemt toe nadat front-ends CPU-gebruik 80% bereiken en stelt de regel voor automatisch schalen om te verhogen exemplaren als volgt:</span><span class="sxs-lookup"><span data-stu-id="2727f-281">For this scenario, Frank knows that the error rate increases after front ends reach 80% CPU utilization and sets the autoscale rule to increase instances as follows:</span></span>

![Instellingen voor automatisch schalen voor de front-toepassingen.][Front-End-Scale]

| <span data-ttu-id="2727f-283">**Profiel voor automatisch schalen: begin eindigt**</span><span class="sxs-lookup"><span data-stu-id="2727f-283">**Autoscale profile – Front ends**</span></span> |
| --- |
| <span data-ttu-id="2727f-284">**Naam:** automatisch schalen: begin eindigt</span><span class="sxs-lookup"><span data-stu-id="2727f-284">**Name:** Autoscale – Front ends</span></span> |
| <span data-ttu-id="2727f-285">**Schaal door:** regels voor planning en prestaties</span><span class="sxs-lookup"><span data-stu-id="2727f-285">**Scale by:** Schedule and performance rules</span></span> |
| <span data-ttu-id="2727f-286">**Profiel:** dagelijkse</span><span class="sxs-lookup"><span data-stu-id="2727f-286">**Profile:** Everyday</span></span> |
| <span data-ttu-id="2727f-287">**Type:** terugkeerpatroon</span><span class="sxs-lookup"><span data-stu-id="2727f-287">**Type:** Recurrence</span></span> |
| <span data-ttu-id="2727f-288">**Doelbereik:** 3 tot 10 exemplaren</span><span class="sxs-lookup"><span data-stu-id="2727f-288">**Target range:** 3 to 10 instances</span></span> |
| <span data-ttu-id="2727f-289">**Aantal dagen:** dagelijkse</span><span class="sxs-lookup"><span data-stu-id="2727f-289">**Days:** Everyday</span></span> |
| <span data-ttu-id="2727f-290">**Begintijd:** 9:00 uur</span><span class="sxs-lookup"><span data-stu-id="2727f-290">**Start time:** 9:00 AM</span></span> |
| <span data-ttu-id="2727f-291">**Tijdzone:** UTC-08</span><span class="sxs-lookup"><span data-stu-id="2727f-291">**Time zone:** UTC-08</span></span> |
|  |
| <span data-ttu-id="2727f-292">**Regel voor automatisch schalen (Omhoog schalen)**</span><span class="sxs-lookup"><span data-stu-id="2727f-292">**Autoscale rule (Scale Up)**</span></span> |
| <span data-ttu-id="2727f-293">**Bron:** front-groep</span><span class="sxs-lookup"><span data-stu-id="2727f-293">**Resource:** Front-end pool</span></span> |
| <span data-ttu-id="2727f-294">**Metrische gegevens:** CPU-percentage</span><span class="sxs-lookup"><span data-stu-id="2727f-294">**Metric:** CPU %</span></span> |
| <span data-ttu-id="2727f-295">**Bewerking:** groter zijn dan 60%</span><span class="sxs-lookup"><span data-stu-id="2727f-295">**Operation:** Greater than 60%</span></span> |
| <span data-ttu-id="2727f-296">**Duur:** 20 minuten</span><span class="sxs-lookup"><span data-stu-id="2727f-296">**Duration:** 20 minutes</span></span> |
| <span data-ttu-id="2727f-297">**Tijd aggregatie:** gemiddelde</span><span class="sxs-lookup"><span data-stu-id="2727f-297">**Time aggregation:** Average</span></span> |
| <span data-ttu-id="2727f-298">**Actie:** aantal verhogen door 3</span><span class="sxs-lookup"><span data-stu-id="2727f-298">**Action:** Increase count by 3</span></span> |
| <span data-ttu-id="2727f-299">**Cool omlaag (minuten):** 120</span><span class="sxs-lookup"><span data-stu-id="2727f-299">**Cool down (minutes):** 120</span></span> |
|  |
| <span data-ttu-id="2727f-300">**Regel voor automatisch schalen (schaal omlaag)**</span><span class="sxs-lookup"><span data-stu-id="2727f-300">**Autoscale rule (Scale Down)**</span></span> |
| <span data-ttu-id="2727f-301">**Bron:** werknemersgroep 1</span><span class="sxs-lookup"><span data-stu-id="2727f-301">**Resource:** Worker pool 1</span></span> |
| <span data-ttu-id="2727f-302">**Metrische gegevens:** CPU-percentage</span><span class="sxs-lookup"><span data-stu-id="2727f-302">**Metric:** CPU %</span></span> |
| <span data-ttu-id="2727f-303">**Bewerking:** minder dan 30%</span><span class="sxs-lookup"><span data-stu-id="2727f-303">**Operation:** Less than 30%</span></span> |
| <span data-ttu-id="2727f-304">**Duur:** 20 minuten</span><span class="sxs-lookup"><span data-stu-id="2727f-304">**Duration:** 20 Minutes</span></span> |
| <span data-ttu-id="2727f-305">**Tijd aggregatie:** gemiddelde</span><span class="sxs-lookup"><span data-stu-id="2727f-305">**Time aggregation:** Average</span></span> |
| <span data-ttu-id="2727f-306">**Actie:** aantal verlagen door 3</span><span class="sxs-lookup"><span data-stu-id="2727f-306">**Action:** Decrease count by 3</span></span> |
| <span data-ttu-id="2727f-307">**Cool omlaag (minuten):** 120</span><span class="sxs-lookup"><span data-stu-id="2727f-307">**Cool down (minutes):** 120</span></span> |

<!-- IMAGES -->
[intro]: ./media/app-service-environment-auto-scale/introduction.png
[settings-scale]: ./media/app-service-environment-auto-scale/settings-scale.png
[scale-manual]: ./media/app-service-environment-auto-scale/scale-manual.png
[scale-profile]: ./media/app-service-environment-auto-scale/scale-profile.png
[scale-profile2]: ./media/app-service-environment-auto-scale/scale-profile-2.png
[scale-rule]: ./media/app-service-environment-auto-scale/scale-rule.png
[asp-scale]: ./media/app-service-environment-auto-scale/asp-scale.png
[ASP-Inflation]: ./media/app-service-environment-auto-scale/asp-inflation-rate.png
[Equation1]: ./media/app-service-environment-auto-scale/equation1.png
[Equation2]: ./media/app-service-environment-auto-scale/equation2.png
[Equation3]: ./media/app-service-environment-auto-scale/equation3.png
[Equation4]: ./media/app-service-environment-auto-scale/equation4.png
[ASP-Total-Inflation]: ./media/app-service-environment-auto-scale/asp-total-inflation-rate.png
[Worker-Pool-Scale]: ./media/app-service-environment-auto-scale/wp-scale.png
[Front-End-Scale]: ./media/app-service-environment-auto-scale/fe-scale.png

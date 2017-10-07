---
title: aaaMicrosoft Threat Modeling hulpprogramma - Azure | Microsoft Docs
description: Meer informatie over alle Hallo functies die beschikbaar zijn in Hallo Threat Modeling hulpprogramma
services: security
documentationcenter: na
author: RodSan
manager: RodSan
editor: RodSan
ms.assetid: na
ms.service: security
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: rodsan
ms.openlocfilehash: f9ad5e623e7758063084cb7fc723c5735161a846
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="threat-modeling-tool-feature-overview"></a><span data-ttu-id="b74f3-103">Overzicht van Threat Modeling hulpprogramma-functies</span><span class="sxs-lookup"><span data-stu-id="b74f3-103">Threat Modeling Tool feature overview</span></span>

<span data-ttu-id="b74f3-104">We zijn blij dat u hebt gekozen toouse Hallo Threat Modeling hulpprogramma voor uw threat modeling behoeften!</span><span class="sxs-lookup"><span data-stu-id="b74f3-104">We are glad you chose toouse hello Threat Modeling Tool for your threat modeling needs!</span></span> <span data-ttu-id="b74f3-105">Als u dit nog niet hebt gedaan, gaat u naar  **[aan de slag met Hallo Threat Modeling hulpprogramma](./azure-security-threat-modeling-tool-getting-started.md)**  toolearn Hallo basisbeginselen.</span><span class="sxs-lookup"><span data-stu-id="b74f3-105">If you haven’t done so, visit **[Getting Started with hello Threat Modeling Tool](./azure-security-threat-modeling-tool-getting-started.md)** toolearn hello basics.</span></span>

> <span data-ttu-id="b74f3-106">Onze hulpprogramma vaak wordt bijgewerkt, dus controleer dit vaak toosee helpen onze nieuwste functies en verbeteringen.</span><span class="sxs-lookup"><span data-stu-id="b74f3-106">Our tool is updated often, so check this guide often toosee our latest features and improvements.</span></span>

<span data-ttu-id="b74f3-107">Te klikken op de knop 'Een nieuwe Model maken' hello wordt geopend, een lege startpagina, vergelijkbare toohello afbeelding hieronder:</span><span class="sxs-lookup"><span data-stu-id="b74f3-107">Clicking on hello "Create a New Model" button opens a blank start page, similar toohello image below:</span></span>

![Lege startpagina](./media/azure-security-threat-modeling-tool/tmtstart.png)

<span data-ttu-id="b74f3-109">Met behulp risicomodel Hallo gemaakt door ons team in Hallo  **[aan de slag](./azure-security-threat-modeling-tool-getting-started.md)**  voorbeeld gaan we Bekijk alle Hallo functies die beschikbaar zijn in Hallo hulpprogramma vandaag.</span><span class="sxs-lookup"><span data-stu-id="b74f3-109">Using hello threat model created by our team in hello **[Getting Started](./azure-security-threat-modeling-tool-getting-started.md)** example, let’s check out all hello features available in hello tool today.</span></span>

![Basic risicomodel](./media/azure-security-threat-modeling-tool/basictmt.png)

## <a name="navigation"></a><span data-ttu-id="b74f3-111">Navigatie</span><span class="sxs-lookup"><span data-stu-id="b74f3-111">Navigation</span></span>

<span data-ttu-id="b74f3-112">Vooraleer Hallo ingebouwde functies, gaan we via Hallo hoofdonderdelen gevonden in het Hallo-hulpprogramma</span><span class="sxs-lookup"><span data-stu-id="b74f3-112">Before diving into hello built-in features, let’s go over hello main components found in hello tool</span></span>

### <a name="menu-items"></a><span data-ttu-id="b74f3-113">Menu-items</span><span class="sxs-lookup"><span data-stu-id="b74f3-113">Menu items</span></span>

<span data-ttu-id="b74f3-114">Hallo-ervaring moet soortgelijke tooother Microsoft-producten.</span><span class="sxs-lookup"><span data-stu-id="b74f3-114">hello experience should be similar tooother Microsoft products.</span></span> <span data-ttu-id="b74f3-115">Laten we beginnen door te gaan via Hallo op het hoogste niveau menu-items:</span><span class="sxs-lookup"><span data-stu-id="b74f3-115">Let’s begin by going through hello top-level menu items:</span></span>

![Menu-Items](./media/azure-security-threat-modeling-tool/menuitems.png)

| <span data-ttu-id="b74f3-117">Label</span><span class="sxs-lookup"><span data-stu-id="b74f3-117">Label</span></span>                               | <span data-ttu-id="b74f3-118">Details</span><span class="sxs-lookup"><span data-stu-id="b74f3-118">Details</span></span>      |
| --------------------------------------- | ------------ |
| <span data-ttu-id="b74f3-119">**File**</span><span class="sxs-lookup"><span data-stu-id="b74f3-119">**File**</span></span> | <ul><li><span data-ttu-id="b74f3-120">Open, opslaan en sluiten van bestanden</span><span class="sxs-lookup"><span data-stu-id="b74f3-120">Open, Save and Close Files</span></span></li><li><span data-ttu-id="b74f3-121">Meld u in/out van OneDrive-accounts</span><span class="sxs-lookup"><span data-stu-id="b74f3-121">Sign In/Out of OneDrive accounts</span></span></li><li><span data-ttu-id="b74f3-122">Koppelingen (weergave + bewerken) te delen</span><span class="sxs-lookup"><span data-stu-id="b74f3-122">Share Links (View + Edit)</span></span></li><li><span data-ttu-id="b74f3-123">Bestandsgegevens weergeven</span><span class="sxs-lookup"><span data-stu-id="b74f3-123">View File Information</span></span></li><li><span data-ttu-id="b74f3-124">Toepassen van nieuwe sjabloon tooExisting modellen</span><span class="sxs-lookup"><span data-stu-id="b74f3-124">Apply New Template tooExisting Models</span></span></li></ul> |
| <span data-ttu-id="b74f3-125">**Bewerken**</span><span class="sxs-lookup"><span data-stu-id="b74f3-125">**Edit**</span></span> | <span data-ttu-id="b74f3-126">Ongedaan maken/opnieuw acties, als ook een kopie plakken en verwijderen</span><span class="sxs-lookup"><span data-stu-id="b74f3-126">Undo/redo actions, as well a copy, paste and delete</span></span> |
| <span data-ttu-id="b74f3-127">**Weergave**</span><span class="sxs-lookup"><span data-stu-id="b74f3-127">**View**</span></span> | <ul><li><span data-ttu-id="b74f3-128">Schakelen tussen **Analysis** en **ontwerp** weergaven</span><span class="sxs-lookup"><span data-stu-id="b74f3-128">Switch between **Analysis** and **Design** views</span></span></li><li><span data-ttu-id="b74f3-129">Open gesloten windows (e.g.stencils, eigenschappen van het element en berichten)</span><span class="sxs-lookup"><span data-stu-id="b74f3-129">Open closed windows (e.g.stencils, element properties and messages)</span></span></li><li><span data-ttu-id="b74f3-130">Lay-out toodefault instellingen opnieuw instellen</span><span class="sxs-lookup"><span data-stu-id="b74f3-130">Reset layout toodefault settings</span></span></li></ul> |
| <span data-ttu-id="b74f3-131">**Diagram**</span><span class="sxs-lookup"><span data-stu-id="b74f3-131">**Diagram**</span></span> | <span data-ttu-id="b74f3-132">Diagrammen toevoegen, verwijderen en door 'tabbladen' diagrammen navigeren</span><span class="sxs-lookup"><span data-stu-id="b74f3-132">Add/Delete diagrams and navigate through “tabs” of diagrams</span></span> |
| <span data-ttu-id="b74f3-133">**Rapporten**</span><span class="sxs-lookup"><span data-stu-id="b74f3-133">**Reports**</span></span> | <span data-ttu-id="b74f3-134">HTML-rapporten tooshare maken met anderen</span><span class="sxs-lookup"><span data-stu-id="b74f3-134">Create HTML reports tooshare with others</span></span> |
| <span data-ttu-id="b74f3-135">**Help**</span><span class="sxs-lookup"><span data-stu-id="b74f3-135">**Help**</span></span> | <span data-ttu-id="b74f3-136">Handleidingen toohelp u Hallo-hulpprogramma gebruiken</span><span class="sxs-lookup"><span data-stu-id="b74f3-136">Guides toohelp you use hello tool</span></span> |

<span data-ttu-id="b74f3-137">Hallo pictogrammen zijn snelkoppelingen voor Hallo op het hoogste niveau menu's:</span><span class="sxs-lookup"><span data-stu-id="b74f3-137">hello icons are shortcuts for hello top-level menus:</span></span>

| <span data-ttu-id="b74f3-138">Pictogram</span><span class="sxs-lookup"><span data-stu-id="b74f3-138">Icon</span></span>                               | <span data-ttu-id="b74f3-139">Details</span><span class="sxs-lookup"><span data-stu-id="b74f3-139">Details</span></span>      |
| --------------------------------------- | ------------ |
| <span data-ttu-id="b74f3-140">**Open**</span><span class="sxs-lookup"><span data-stu-id="b74f3-140">**Open**</span></span> | <span data-ttu-id="b74f3-141">Hiermee opent u een nieuw bestand</span><span class="sxs-lookup"><span data-stu-id="b74f3-141">Opens a new file</span></span> |
| <span data-ttu-id="b74f3-142">**Opslaan**</span><span class="sxs-lookup"><span data-stu-id="b74f3-142">**Save**</span></span> | <span data-ttu-id="b74f3-143">Huidige bestand wordt opgeslagen</span><span class="sxs-lookup"><span data-stu-id="b74f3-143">Saves current file</span></span> |
| <span data-ttu-id="b74f3-144">**Ontwerp**</span><span class="sxs-lookup"><span data-stu-id="b74f3-144">**Design**</span></span> | <span data-ttu-id="b74f3-145">In de ontwerpweergave gaat hier kunt u modellen maken</span><span class="sxs-lookup"><span data-stu-id="b74f3-145">Goes into design view, where you can create models</span></span> |
| <span data-ttu-id="b74f3-146">**Analyseren**</span><span class="sxs-lookup"><span data-stu-id="b74f3-146">**Analyze**</span></span> | <span data-ttu-id="b74f3-147">Toont gegenereerd bedreigingen en hun eigenschappen</span><span class="sxs-lookup"><span data-stu-id="b74f3-147">Shows generated threats and their properties</span></span> |
| <span data-ttu-id="b74f3-148">**Diagram toevoegen**</span><span class="sxs-lookup"><span data-stu-id="b74f3-148">**Add Diagram**</span></span> | <span data-ttu-id="b74f3-149">Nieuw diagram (vergelijkbaar toonew tabs in Excel) wordt toegevoegd</span><span class="sxs-lookup"><span data-stu-id="b74f3-149">Adds new diagram (similar toonew tabs in Excel)</span></span> |
| <span data-ttu-id="b74f3-150">**Diagram verwijderen**</span><span class="sxs-lookup"><span data-stu-id="b74f3-150">**Delete Diagram**</span></span> | <span data-ttu-id="b74f3-151">Hiermee verwijdert u Huidig diagram</span><span class="sxs-lookup"><span data-stu-id="b74f3-151">Deletes current diagram</span></span> |
| <span data-ttu-id="b74f3-152">**Knippen/kopiëren/plakken**</span><span class="sxs-lookup"><span data-stu-id="b74f3-152">**Copy/Cut/Paste**</span></span> | <span data-ttu-id="b74f3-153">Elementen delen-kopieën/geplakt</span><span class="sxs-lookup"><span data-stu-id="b74f3-153">Copies/cuts/pastes elements</span></span> |
| <span data-ttu-id="b74f3-154">**Ongedaan maken/opnieuw uitvoeren**</span><span class="sxs-lookup"><span data-stu-id="b74f3-154">**Undo/Redo**</span></span> | <span data-ttu-id="b74f3-155">Hiermee wordt ongedaan gemaakt/voert acties</span><span class="sxs-lookup"><span data-stu-id="b74f3-155">Undoes/redoes actions</span></span> |
| <span data-ttu-id="b74f3-156">**Inzoomen- / uitzoomen**</span><span class="sxs-lookup"><span data-stu-id="b74f3-156">**Zoom In/Zoom Out**</span></span> | <span data-ttu-id="b74f3-157">Zoomt in en uit Hallo diagram voor een beter beeld</span><span class="sxs-lookup"><span data-stu-id="b74f3-157">Zooms in and out of hello diagram for a better view</span></span> |
| <span data-ttu-id="b74f3-158">**Feedback**</span><span class="sxs-lookup"><span data-stu-id="b74f3-158">**Feedback**</span></span> | <span data-ttu-id="b74f3-159">Hiermee opent u Hallo MSDN-Forum</span><span class="sxs-lookup"><span data-stu-id="b74f3-159">Opens hello MSDN Forum</span></span> |

### <a name="canvas"></a><span data-ttu-id="b74f3-160">Canvas</span><span class="sxs-lookup"><span data-stu-id="b74f3-160">Canvas</span></span>

<span data-ttu-id="b74f3-161">Hallo ruimte waar u slepen en neerzetten van elementen in.</span><span class="sxs-lookup"><span data-stu-id="b74f3-161">hello space where you drag and drop elements into.</span></span> <span data-ttu-id="b74f3-162">Slepen en neerzetten is Hallo snelste en meest efficiënte manier toobuild modellen.</span><span class="sxs-lookup"><span data-stu-id="b74f3-162">Drag and drop is hello quickest and most efficient way toobuild models.</span></span> <span data-ttu-id="b74f3-163">U kunt ook met de rechtermuisknop op en selecteer in de Hallo menu, dat wordt toegevoegd algemene versies van het Hallo-elementen die u gebruikt, zoals hieronder wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="b74f3-163">You may also right click and select from hello menu, which adds generic versions of hello elements you’re using, as shown below.</span></span>

#### <a name="dropping-hello-stencil-on-hello-canvas"></a><span data-ttu-id="b74f3-164">Hallo stencil neer te zetten op Hallo canvas</span><span class="sxs-lookup"><span data-stu-id="b74f3-164">Dropping hello stencil on hello canvas</span></span>

![Canvas neerzetten](./media/azure-security-threat-modeling-tool/canvasdrop1.png)

#### <a name="clicking-on-hello-stencil"></a><span data-ttu-id="b74f3-166">Te klikken op Hallo stencil</span><span class="sxs-lookup"><span data-stu-id="b74f3-166">Clicking on hello stencil</span></span>

![Eigenschappen van het element](./media/azure-security-threat-modeling-tool/canvasdrop2.png)

### <a name="stencils"></a><span data-ttu-id="b74f3-168">Stencils</span><span class="sxs-lookup"><span data-stu-id="b74f3-168">Stencils</span></span>

<span data-ttu-id="b74f3-169">Wanneer u vindt stencils alle beschikbare toouse op basis van geselecteerde Hallo-sjabloon.</span><span class="sxs-lookup"><span data-stu-id="b74f3-169">Where you can find all stencils available toouse based on hello template selected.</span></span> <span data-ttu-id="b74f3-170">Als u de juiste elementen Hallo vinden kunt, probeer het opnieuw met een andere sjabloon of wijzigen van één toofit uw behoeften.</span><span class="sxs-lookup"><span data-stu-id="b74f3-170">If you can’t find hello right elements, try using another template, or modify one toofit your needs.</span></span> <span data-ttu-id="b74f3-171">In het algemeen moet u kunnen toofind een combinatie van categorieën zoals Hallo die hieronder:</span><span class="sxs-lookup"><span data-stu-id="b74f3-171">Generally, you should be able toofind a combination of categories like hello ones below:</span></span>

| <span data-ttu-id="b74f3-172">Stencilnaam</span><span class="sxs-lookup"><span data-stu-id="b74f3-172">Stencil Name</span></span>                               | <span data-ttu-id="b74f3-173">Details</span><span class="sxs-lookup"><span data-stu-id="b74f3-173">Details</span></span>      |
| --------------------------------------- | ------------ |
| <span data-ttu-id="b74f3-174">**Proces**</span><span class="sxs-lookup"><span data-stu-id="b74f3-174">**Process**</span></span> | <span data-ttu-id="b74f3-175">Toepassingen, Browser invoegtoepassingen, Threads, virtuele Machines</span><span class="sxs-lookup"><span data-stu-id="b74f3-175">Applications, Browser Plugins, Threads, Virtual Machines</span></span> |
| <span data-ttu-id="b74f3-176">**Externe interactie**</span><span class="sxs-lookup"><span data-stu-id="b74f3-176">**External Interactor**</span></span> | <span data-ttu-id="b74f3-177">Verificatieproviders, Browsers, gebruikers, webtoepassingen</span><span class="sxs-lookup"><span data-stu-id="b74f3-177">Authentication Providers, Browsers, Users, Web Applications</span></span> |
| <span data-ttu-id="b74f3-178">**Gegevensopslag**</span><span class="sxs-lookup"><span data-stu-id="b74f3-178">**Data Store**</span></span> | <span data-ttu-id="b74f3-179">Cache, opslag, configuratie-bestanden, Databases, register</span><span class="sxs-lookup"><span data-stu-id="b74f3-179">Cache, Storage, Configuration Files, Databases, Registry</span></span> |
| <span data-ttu-id="b74f3-180">**Gegevensstroom**</span><span class="sxs-lookup"><span data-stu-id="b74f3-180">**Data Flow**</span></span> | <span data-ttu-id="b74f3-181">Binaire ALPC, HTTP, HTTPS/TLS/SSL, IOCTL, IPSec, benoemde Pipe, RPC/DCOM, SMB, UDP</span><span class="sxs-lookup"><span data-stu-id="b74f3-181">Binary, ALPC, HTTP, HTTPS/TLS/SSL, IOCTL, IPSec, Named Pipe, RPC/DCOM, SMB, UDP</span></span> |
| <span data-ttu-id="b74f3-182">**Lijn grens vertrouwen**</span><span class="sxs-lookup"><span data-stu-id="b74f3-182">**Trust Line/Border Boundary**</span></span> | <span data-ttu-id="b74f3-183">Bedrijfsnetwerken, Internet, Machine, Sandbox, gebruiker/kernelmodus</span><span class="sxs-lookup"><span data-stu-id="b74f3-183">Corporate Networks, Internet, Machine, Sandbox, User/Kernel Mode</span></span> |

### <a name="notesmessages"></a><span data-ttu-id="b74f3-184">Opmerkingen bij de/Messages</span><span class="sxs-lookup"><span data-stu-id="b74f3-184">Notes/Messages</span></span>

| <span data-ttu-id="b74f3-185">Onderdeel</span><span class="sxs-lookup"><span data-stu-id="b74f3-185">Component</span></span>                               | <span data-ttu-id="b74f3-186">Details</span><span class="sxs-lookup"><span data-stu-id="b74f3-186">Details</span></span>      |
| --------------------------------------- | ------------ |
| <span data-ttu-id="b74f3-187">**Berichten**</span><span class="sxs-lookup"><span data-stu-id="b74f3-187">**Messages**</span></span> | <span data-ttu-id="b74f3-188">Interne hulpprogramma logica die gebruikers waarschuwt wanneer er een fout optreedt, zoals geen gegevensoverdrachten tussen elementen</span><span class="sxs-lookup"><span data-stu-id="b74f3-188">Internal tool logic that alerts users whenever there is an error, such as no data flows between elements</span></span> |
| <span data-ttu-id="b74f3-189">**Opmerkingen bij de**</span><span class="sxs-lookup"><span data-stu-id="b74f3-189">**Notes**</span></span> | <span data-ttu-id="b74f3-190">Opmerkingen bij de handmatige toegevoegde toohello bestands door engineering-teams in de rest Hallo ontwerp- en evaluatieproces</span><span class="sxs-lookup"><span data-stu-id="b74f3-190">Manual notes added toohello file by engineering teams throughout hello design and review process</span></span> |

### <a name="element-properties"></a><span data-ttu-id="b74f3-191">Eigenschappen van het element</span><span class="sxs-lookup"><span data-stu-id="b74f3-191">Element properties</span></span>

<span data-ttu-id="b74f3-192">Deze verschillen per Hallo-elementen die zijn geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="b74f3-192">These vary by hello elements selected.</span></span> <span data-ttu-id="b74f3-193">Alle andere elementen bevatten naast vertrouwen grenzen 3 algemene selecties:</span><span class="sxs-lookup"><span data-stu-id="b74f3-193">Apart from Trust Boundaries, all other elements contain 3 general selections:</span></span>

| <span data-ttu-id="b74f3-194">Eigenschap element</span><span class="sxs-lookup"><span data-stu-id="b74f3-194">Element Property</span></span>                               | <span data-ttu-id="b74f3-195">Details</span><span class="sxs-lookup"><span data-stu-id="b74f3-195">Details</span></span>      |
| --------------------------------------- | ------------ |
| <span data-ttu-id="b74f3-196">**Naam**</span><span class="sxs-lookup"><span data-stu-id="b74f3-196">**Name**</span></span> | <span data-ttu-id="b74f3-197">Handig is voor de naamgeving van uw processen, archieven, interacties en stromen toobe gemakkelijk kunt herkennen</span><span class="sxs-lookup"><span data-stu-id="b74f3-197">Useful for naming your processes, stores, interactors and flows toobe easily recognized</span></span> |
| <span data-ttu-id="b74f3-198">**Buiten het bereik**</span><span class="sxs-lookup"><span data-stu-id="b74f3-198">**Out of Scope**</span></span> | <span data-ttu-id="b74f3-199">Indien geselecteerd, wordt Hallo-element genomen buiten Hallo threat generatie matrix (niet aanbevolen)</span><span class="sxs-lookup"><span data-stu-id="b74f3-199">If selected, hello element is taken out of hello threat generation matrix (not recommended)</span></span> |
| <span data-ttu-id="b74f3-200">**Reden voor buiten het bereik**</span><span class="sxs-lookup"><span data-stu-id="b74f3-200">**Reason for Out of Scope**</span></span> | <span data-ttu-id="b74f3-201">Reden veld toolet gebruikers weten waarom buiten het bereik is geselecteerd</span><span class="sxs-lookup"><span data-stu-id="b74f3-201">Justification field toolet users know why out of scope was selected</span></span> |

<span data-ttu-id="b74f3-202">Eigenschappen worden onder elke categorie element gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="b74f3-202">Properties are changed under each element category.</span></span> <span data-ttu-id="b74f3-203">Klik op elk element tooinspect Hallo beschikbare opties of Hallo sjabloon toolearn meer openen.</span><span class="sxs-lookup"><span data-stu-id="b74f3-203">Click on each element tooinspect hello available options, or open hello template toolearn more.</span></span> <span data-ttu-id="b74f3-204">Hiermee kunt krijgen tot Hallo-functies.</span><span class="sxs-lookup"><span data-stu-id="b74f3-204">Let’s get into hello features.</span></span>

## <a name="welcome-screen"></a><span data-ttu-id="b74f3-205">Welkomstscherm</span><span class="sxs-lookup"><span data-stu-id="b74f3-205">Welcome screen</span></span>

<span data-ttu-id="b74f3-206">Hallo-welkomstscherm is Hallo eerste wat die u ziet wanneer u Hallo app opent.</span><span class="sxs-lookup"><span data-stu-id="b74f3-206">hello welcome screen is hello first thing you see when you open hello app.</span></span>

### <a name="open-a-model"></a><span data-ttu-id="b74f3-207">Een model openen</span><span class="sxs-lookup"><span data-stu-id="b74f3-207">Open A model</span></span>

<span data-ttu-id="b74f3-208">Muiswijzer op de knop 'Open een Model' ziet u 2 verborgen opties: 'Openen vanaf deze Computer' en "Openen vanuit OneDrive."</span><span class="sxs-lookup"><span data-stu-id="b74f3-208">Hovering over “Open a Model” button shows you 2 hidden options: “Open From this Computer” and “Open from OneDrive.”</span></span> <span data-ttu-id="b74f3-209">Hallo eerst bestand openen welkomstscherm wordt geopend terwijl Hallo tweede u Hallo aanmelden proces voor OneDrive doorloopt, zodat u bestanden en mappen toopick na een geslaagde verificatie.</span><span class="sxs-lookup"><span data-stu-id="b74f3-209">hello first opens hello File Open screen, while hello second takes you through hello sign in process for OneDrive, allowing you toopick folders and files after a successful authentication.</span></span>

![Model openen](./media/azure-security-threat-modeling-tool/openmodel.png)

![Openen van de Computer of OneDrive](./media/azure-security-threat-modeling-tool/openmodel2.png)

### <a name="feedback-suggestions-and-issues"></a><span data-ttu-id="b74f3-212">Feedback, suggesties en problemen</span><span class="sxs-lookup"><span data-stu-id="b74f3-212">Feedback, suggestions and issues</span></span>

<span data-ttu-id="b74f3-213">Als u deze optie selecteert, gaat u toohello MSDN-Forums voor SDL-hulpprogramma's.</span><span class="sxs-lookup"><span data-stu-id="b74f3-213">Selecting this option will take you toohello MSDN Forums for SDL Tools.</span></span> <span data-ttu-id="b74f3-214">Het is een uitstekende manier toocheck uit wat anderen hierover Hallo hulpprogramma, met inbegrip van tijdelijke oplossingen en nieuwe ideeën.</span><span class="sxs-lookup"><span data-stu-id="b74f3-214">It’s a great way toocheck out what other people are saying about hello tool, including workarounds and new ideas.</span></span>

![Feedback](./media/azure-security-threat-modeling-tool/feedback.png)

## <a name="design-view"></a><span data-ttu-id="b74f3-216">Ontwerpweergave</span><span class="sxs-lookup"><span data-stu-id="b74f3-216">Design view</span></span>

<span data-ttu-id="b74f3-217">Wanneer u opent of een nieuw model maakt, wordt u geleid toohello ontwerpweergave.</span><span class="sxs-lookup"><span data-stu-id="b74f3-217">Whenever you open or create a new model, you’ll be taken toohello design view.</span></span>

### <a name="adding-elements"></a><span data-ttu-id="b74f3-218">Het toevoegen van elementen</span><span class="sxs-lookup"><span data-stu-id="b74f3-218">Adding elements</span></span>

<span data-ttu-id="b74f3-219">Er zijn 2 manieren tooadd elementen op Hallo raster:</span><span class="sxs-lookup"><span data-stu-id="b74f3-219">There are 2 ways tooadd elements on hello grid:</span></span>

- <span data-ttu-id="b74f3-220">**Slepen en neerzetten** : Sleep Hallo gewenste element toohello raster en gebruikt u Hallo element eigenschappen tooprovide aanvullende informatie.</span><span class="sxs-lookup"><span data-stu-id="b74f3-220">**Drag and Drop** – drag hello desired element toohello grid, then use hello element properties tooprovide additional information.</span></span>
- <span data-ttu-id="b74f3-221">**Klik met de rechtermuisknop** : klik met de rechtermuisknop ergens op Hallo raster en selecteer in het vervolgkeuzemenu Hallo.</span><span class="sxs-lookup"><span data-stu-id="b74f3-221">**Right Click** – right click anywhere on hello grid and select from hello dropdown menu.</span></span> <span data-ttu-id="b74f3-222">Een algemene weergave van dat element worden weergegeven op het welkomstscherm.</span><span class="sxs-lookup"><span data-stu-id="b74f3-222">A generic representation of that element will appear on hello screen.</span></span>

### <a name="connecting-elements"></a><span data-ttu-id="b74f3-223">Verbinding maken met elementen</span><span class="sxs-lookup"><span data-stu-id="b74f3-223">Connecting elements</span></span>

<span data-ttu-id="b74f3-224">Er zijn 2 manieren elementen tooconnect in hulpprogramma Hallo:</span><span class="sxs-lookup"><span data-stu-id="b74f3-224">There are 2 ways tooconnect elements in hello tool:</span></span>

- <span data-ttu-id="b74f3-225">**Slepen en neerzetten** : Sleep Hallo gewenste gegevensstroom toohello raster en verbinding maken met beide uiteinden toohello geschikte elementen.</span><span class="sxs-lookup"><span data-stu-id="b74f3-225">**Drag and Drop** – drag hello desired dataflow toohello grid, and connect both ends toohello appropriate elements.</span></span>
- <span data-ttu-id="b74f3-226">**Klik op + Shift** : klik op de eerste Hallo-element (het versturen van gegevens) en houdt u Shift-toets ingedrukt Hallo en vervolgens selecteert Hallo tweede element (ontvangen van gegevens).</span><span class="sxs-lookup"><span data-stu-id="b74f3-226">**Click + Shift** – click on hello first element (sending data), press and hold hello Shift key, then select hello second element (receiving data).</span></span> <span data-ttu-id="b74f3-227">Klik met de rechtermuisknop en selecteer "Verbinding maken."</span><span class="sxs-lookup"><span data-stu-id="b74f3-227">Right click, and select “Connect.”</span></span> <span data-ttu-id="b74f3-228">Als u een bidirectionele-gegevensstroom, is Hallo volgorde niet als belangrijk.</span><span class="sxs-lookup"><span data-stu-id="b74f3-228">If you’re using a bi-directional dataflow, hello order is not as important.</span></span>

### <a name="properties"></a><span data-ttu-id="b74f3-229">Eigenschappen</span><span class="sxs-lookup"><span data-stu-id="b74f3-229">Properties</span></span>

<span data-ttu-id="b74f3-230">Bevat alle Hallo-eigenschappen die kunnen worden gewijzigd op Hallo stencils in Hallo diagram geplaatst.</span><span class="sxs-lookup"><span data-stu-id="b74f3-230">Shows all hello properties that can be modified on hello stencils placed in hello diagram.</span></span> <span data-ttu-id="b74f3-231">toosee hello eigenschappen, klikt u op Hallo stencil en Hallo informatie dienovereenkomstig worden ingevuld.</span><span class="sxs-lookup"><span data-stu-id="b74f3-231">toosee hello properties, just click on hello stencil and hello information will be populated accordingly.</span></span> <span data-ttu-id="b74f3-232">Hallo in het volgende voorbeeld ziet u voor en na een 'Database' stencil wordt gesleept Hallo diagram:</span><span class="sxs-lookup"><span data-stu-id="b74f3-232">hello example below shows before and after a "Database" stencil is dragged onto hello diagram:</span></span>

#### <a name="before"></a><span data-ttu-id="b74f3-233">Voordat u</span><span class="sxs-lookup"><span data-stu-id="b74f3-233">Before</span></span>

![Voordat u](./media/azure-security-threat-modeling-tool/properties1.png)

#### <a name="after"></a><span data-ttu-id="b74f3-235">Na</span><span class="sxs-lookup"><span data-stu-id="b74f3-235">After</span></span>

![Na](./media/azure-security-threat-modeling-tool/properties2.png)

### <a name="messages"></a><span data-ttu-id="b74f3-237">Berichten</span><span class="sxs-lookup"><span data-stu-id="b74f3-237">Messages</span></span>

<span data-ttu-id="b74f3-238">Als u een risicomodel maakt en gegevens tooconnect loopt tooelements vergeet, bericht berichtvenster Hallo tooact.</span><span class="sxs-lookup"><span data-stu-id="b74f3-238">If you create a threat model and forget tooconnect data flows tooelements, hello message window notifies you tooact.</span></span> <span data-ttu-id="b74f3-239">U kunt tooignore deze of Voer Hallo instructies toofix Hallo probleem.</span><span class="sxs-lookup"><span data-stu-id="b74f3-239">You can choose tooignore it or follow hello instructions toofix hello issue.</span></span> 

![Berichten](./media/azure-security-threat-modeling-tool/messages.png)

### <a name="notes"></a><span data-ttu-id="b74f3-241">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="b74f3-241">Notes</span></span>

<span data-ttu-id="b74f3-242">U tooadd notities tooyour diagram toocapture kunt alle uw ideeën schakelen tussen tabbladen van berichten tooNotes</span><span class="sxs-lookup"><span data-stu-id="b74f3-242">Switching tabs from Messages tooNotes allows you tooadd notes tooyour diagram toocapture all your thoughts</span></span>

## <a name="analysis-view"></a><span data-ttu-id="b74f3-243">Analyse weergeven</span><span class="sxs-lookup"><span data-stu-id="b74f3-243">Analysis view</span></span>

<span data-ttu-id="b74f3-244">Als u klaar bent voor het bouwen van uw diagram overschakelen via tooanalysis weergeven door te gaan toohello bovenste menuselecties en Hallo Vergrootglas volgende toohello paint palet kiezen.</span><span class="sxs-lookup"><span data-stu-id="b74f3-244">Once you're done building your diagram, switch over tooanalysis view by going toohello top menu selections and choosing hello magnifying glass next toohello paint palette.</span></span>

![Analyse weergeven](./media/azure-security-threat-modeling-tool/analysisview.png)

### <a name="generated-threat-selection"></a><span data-ttu-id="b74f3-246">Gegenereerde threat selectie</span><span class="sxs-lookup"><span data-stu-id="b74f3-246">Generated threat selection</span></span>

<span data-ttu-id="b74f3-247">Wanneer u op een bedreiging klikt, kunt u gebruikmaken van drie unieke functies:</span><span class="sxs-lookup"><span data-stu-id="b74f3-247">When you click on a threat, you can leverage three unique functions:</span></span>

| <span data-ttu-id="b74f3-248">Functie</span><span class="sxs-lookup"><span data-stu-id="b74f3-248">Feature</span></span>                               | <span data-ttu-id="b74f3-249">Info</span><span class="sxs-lookup"><span data-stu-id="b74f3-249">Info</span></span>      |
| --------------------------------------- | ------------ |
| <span data-ttu-id="b74f3-250">**Lees Indicator**</span><span class="sxs-lookup"><span data-stu-id="b74f3-250">**Read Indicator**</span></span> | <p><span data-ttu-id="b74f3-251">Bedreiging is nu gemarkeerd als gelezen die eenvoudig kunt u bijhouden van Hallo artikelen die u al hebben doorlopen</span><span class="sxs-lookup"><span data-stu-id="b74f3-251">Threat is now marked as read, which can easily help you keep track of hello items you already went through</span></span></p><p>![Lezen/ongelezen Indicator](./media/azure-security-threat-modeling-tool/readmode.png)</p> |
| <span data-ttu-id="b74f3-253">**Interactie Focus**</span><span class="sxs-lookup"><span data-stu-id="b74f3-253">**Interaction Focus**</span></span> | <p><span data-ttu-id="b74f3-254">Interactie in Hallo diagram die behoren toothat threat is gemarkeerd</span><span class="sxs-lookup"><span data-stu-id="b74f3-254">Interaction in hello diagram belonging toothat threat is highlighted</span></span></p><p>![Interactie Focus](./media/azure-security-threat-modeling-tool/interactionfocus.png)</p> |
| <span data-ttu-id="b74f3-256">**Eigenschappen van de Threat**</span><span class="sxs-lookup"><span data-stu-id="b74f3-256">**Threat Properties**</span></span> | <p><span data-ttu-id="b74f3-257">Als u meer informatie over Hallo dreiging wordt ingevuld in Hallo threat eigenschappenvenster</span><span class="sxs-lookup"><span data-stu-id="b74f3-257">Additional information about hello threat is populated in hello threat properties window</span></span></p><p>![Eigenschappen van de Threat](./media/azure-security-threat-modeling-tool/threatproperties.png)</p> |

### <a name="priority-change"></a><span data-ttu-id="b74f3-259">Prioriteit wijzigen</span><span class="sxs-lookup"><span data-stu-id="b74f3-259">Priority change</span></span>

<span data-ttu-id="b74f3-260">Hallo prioriteitsniveau van elke gegenereerde bedreiging ook wijzigt, worden hun toomake kleuren het eenvoudig tooidentify hoog, gemiddeld en laag prioriteit bedreigingen.</span><span class="sxs-lookup"><span data-stu-id="b74f3-260">Changing hello priority level of each generated threat also changes their colors toomake it easy tooidentify high, medium and low priority threats.</span></span>

![Prioriteit wijzigen](./media/azure-security-threat-modeling-tool/prioritychange.png)

### <a name="threat-properties-editable-fields"></a><span data-ttu-id="b74f3-262">Threat eigenschappen bewerkbare velden</span><span class="sxs-lookup"><span data-stu-id="b74f3-262">Threat properties editable fields</span></span>

<span data-ttu-id="b74f3-263">Zoals u in Hallo afbeelding hierboven, kunnen gebruikers wijzigen Hallo informatie die wordt gegenereerd door Hallo hulpprogramma een ook informatie toocertain velden, zoals rechtvaardiging toevoegen.</span><span class="sxs-lookup"><span data-stu-id="b74f3-263">As seen in hello image above, users can change hello information generated by hello tool an also add information toocertain fields, such as justification.</span></span> <span data-ttu-id="b74f3-264">Deze velden worden gegenereerd door de sjabloon hello, dus als u meer informatie nodig voor elke bedreiging, u ten zeerste toomake wijzigingen bent.</span><span class="sxs-lookup"><span data-stu-id="b74f3-264">These fields are generated by hello template, so if you need more information for each threat, you're encouraged toomake modifications.</span></span>

![Eigenschappen van de Threat](./media/azure-security-threat-modeling-tool/threatproperties.png)

## <a name="reports"></a><span data-ttu-id="b74f3-266">Rapporten</span><span class="sxs-lookup"><span data-stu-id="b74f3-266">Reports</span></span>

<span data-ttu-id="b74f3-267">Als u veranderende prioriteiten bent klaar en bijwerken Hallo-status van elke bedreiging gegenereerd, u kunt Hallo bestand opslaan en/of afdrukken door te gaan te 'rapporteren' en klik vervolgens 'volledige rapport maken."</span><span class="sxs-lookup"><span data-stu-id="b74f3-267">Once you're done changing priorities and updating hello status of each generated threat, you can save hello file and/or print out a report by going too"Report" and then "Create Full Report."</span></span> <span data-ttu-id="b74f3-268">U wordt gevraagd tooname Hallo rapport en zodra u dit doet, ziet u iets dergelijks toohello afbeelding hieronder:</span><span class="sxs-lookup"><span data-stu-id="b74f3-268">You'll be asked tooname hello report, and once you do, you should see something similar toohello image below:</span></span>

![Rapport](./media/azure-security-threat-modeling-tool/report.png)

## <a name="next-steps"></a><span data-ttu-id="b74f3-270">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="b74f3-270">Next steps</span></span>

<span data-ttu-id="b74f3-271">een sjabloon voor het Hallo-community toocontribute Ga tooour  **[GitHub](https://github.com/Microsoft/threat-modeling-templates)**  pagina.</span><span class="sxs-lookup"><span data-stu-id="b74f3-271">toocontribute a template for hello community, please go tooour **[GitHub](https://github.com/Microsoft/threat-modeling-templates)** page.</span></span> <span data-ttu-id="b74f3-272">**[Download](https://aka.ms/tmtpreview)**  Hallo hulpprogramma tooget Vandaag gestart.</span><span class="sxs-lookup"><span data-stu-id="b74f3-272">**[Download](https://aka.ms/tmtpreview)** hello tool tooget started today.</span></span>

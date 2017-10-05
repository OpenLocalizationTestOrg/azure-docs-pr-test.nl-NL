---
title: Beveiliging met Power BI Embedded
description: Meer informatie over beveiliging met Power BI Embedded
services: power-bi-embedded
documentationcenter: 
author: guyinacube
manager: erikre
editor: 
tags: 
ms.assetid: 7936ade5-2c75-435b-8314-ea7ca815867a
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 03/11/2017
ms.author: asaxton
ms.openlocfilehash: 1cde5b9ee4c716af07d427d4d0eb3f0775d456ac
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="row-level-security-with-power-bi-embedded"></a><span data-ttu-id="f47fa-103">Beveiliging op rijniveau in Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="f47fa-103">Row level security with Power BI Embedded</span></span>

<span data-ttu-id="f47fa-104">Beveiliging op rijniveau (RLS) kan gebruikerstoegang te beperken tot bepaalde gegevens binnen een rapport of de gegevensset, zodat meerdere verschillende gebruikers gebruiken hetzelfde rapport tijdens het weergeven van alle andere gegevens worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="f47fa-104">Row level security (RLS) can be used to restrict user access to particular data within a report or dataset, allowing for multiple different users to use the same report while all seeing different data.</span></span> <span data-ttu-id="f47fa-105">Power BI Embedded biedt nu ondersteuning voor gegevenssets die zijn geconfigureerd voor beveiliging op Rijniveau.</span><span class="sxs-lookup"><span data-stu-id="f47fa-105">Power BI Embedded now supports datasets configured with RLS.</span></span>

![](media/power-bi-embedded-rls/pbi-embedded-rls-flow-1.png)

<span data-ttu-id="f47fa-106">Om te profiteren van RLS, is het belangrijk dat u begrijpt dat drie belangrijkste concepten; Gebruikers, rollen en -regels.</span><span class="sxs-lookup"><span data-stu-id="f47fa-106">In order to take advantage of RLS, it’s important you understand three main concepts; Users, Roles, and Rules.</span></span> <span data-ttu-id="f47fa-107">Laten we dichter bij elke:</span><span class="sxs-lookup"><span data-stu-id="f47fa-107">Let’s take a closer look at each:</span></span>

<span data-ttu-id="f47fa-108">**Gebruikers** : deze worden de werkelijke eindgebruikers weergeven van rapporten.</span><span class="sxs-lookup"><span data-stu-id="f47fa-108">**Users** –  These are the actual end-users viewing reports.</span></span> <span data-ttu-id="f47fa-109">In Power BI Embedded worden gebruikers geïdentificeerd door de eigenschap username in een App-Token.</span><span class="sxs-lookup"><span data-stu-id="f47fa-109">In Power BI Embedded, users are identified by the username property in an App Token.</span></span>

<span data-ttu-id="f47fa-110">**Rollen** – gebruikers tot functies behoren.</span><span class="sxs-lookup"><span data-stu-id="f47fa-110">**Roles** – Users belong to roles.</span></span> <span data-ttu-id="f47fa-111">Een rol is een container voor regels en kan de naam zoals 'Sales Manager' of 'Vertegenwoordiger'.</span><span class="sxs-lookup"><span data-stu-id="f47fa-111">A role is a container for rules and can be named something like “Sales Manager” or “Sales Rep”.</span></span> <span data-ttu-id="f47fa-112">In Power BI Embedded worden gebruikers geïdentificeerd door de eigenschap rollen in een App-Token.</span><span class="sxs-lookup"><span data-stu-id="f47fa-112">In Power BI Embedded, users are identified by the roles property in an App Token.</span></span>

<span data-ttu-id="f47fa-113">**Regels** : rollen regels hebben en deze regels zijn de werkelijke filters die u op de gegevens worden toegepast.</span><span class="sxs-lookup"><span data-stu-id="f47fa-113">**Rules** – Roles have rules, and those rules are the actual filters that are going to be applied to the data.</span></span> <span data-ttu-id="f47fa-114">Dit wordt mogelijk net zo eenvoudig als ' land Verenigde Staten = ' of iets meer dynamische.</span><span class="sxs-lookup"><span data-stu-id="f47fa-114">This could be as simple as “Country = USA” or something much more dynamic.</span></span>

### <a name="example"></a><span data-ttu-id="f47fa-115">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="f47fa-115">Example</span></span>

<span data-ttu-id="f47fa-116">Voor de rest van dit artikel bieden we een voorbeeld van RLS ontwerpen en verbruikt die in een ingesloten toepassing.</span><span class="sxs-lookup"><span data-stu-id="f47fa-116">For the rest of this article, we’ll provide an example of authoring RLS, and then consuming that within an embedded application.</span></span> <span data-ttu-id="f47fa-117">Dit voorbeeld wordt de [Retail Analysis Sample](http://go.microsoft.com/fwlink/?LinkID=780547) PBIX-bestand.</span><span class="sxs-lookup"><span data-stu-id="f47fa-117">Our example uses the [Retail Analysis Sample](http://go.microsoft.com/fwlink/?LinkID=780547) PBIX file.</span></span>

![](media/power-bi-embedded-rls/pbi-embedded-rls-scenario-2.png)

<span data-ttu-id="f47fa-118">Onze Retail Analysis sample verkoopcijfers voor alle winkels in een bepaalde winkelketen.</span><span class="sxs-lookup"><span data-stu-id="f47fa-118">Our Retail Analysis sample shows sales for all the stores in a particular retail chain.</span></span> <span data-ttu-id="f47fa-119">Zonder RLS, ongeacht welke regionale manager zich aanmeldt en bekijkt het rapport, zien ze dezelfde gegevens.</span><span class="sxs-lookup"><span data-stu-id="f47fa-119">Without RLS, no matter which district manager signs in and views the report, they’ll see the same data.</span></span> <span data-ttu-id="f47fa-120">Senior management heeft elke regionale manager ziet alleen de verkoop voor de winkels die ze beheren en om dit te doen, gebruiken we RLS vastgesteld.</span><span class="sxs-lookup"><span data-stu-id="f47fa-120">Senior management has determined each district manager should only see the sales for the stores they manage, and to do this, we can use RLS.</span></span>

<span data-ttu-id="f47fa-121">RLS is geschreven in Power BI Desktop.</span><span class="sxs-lookup"><span data-stu-id="f47fa-121">RLS is authored in Power BI Desktop.</span></span> <span data-ttu-id="f47fa-122">Wanneer de gegevensset en het rapport wordt geopend, kunnen we overschakelen naar diagram weer te geven van het schema:</span><span class="sxs-lookup"><span data-stu-id="f47fa-122">When the dataset and report are opened, we can switch to diagram view to see the schema:</span></span>

![](media/power-bi-embedded-rls/pbi-embedded-rls-diagram-view-3.png)

<span data-ttu-id="f47fa-123">Hier volgen een aantal dingen opvalt met dit schema:</span><span class="sxs-lookup"><span data-stu-id="f47fa-123">Here are a few things to notice with this schema:</span></span>

* <span data-ttu-id="f47fa-124">Alle maateenheden zoals **totale verkoop**, worden opgeslagen in de **verkoop** feitentabel.</span><span class="sxs-lookup"><span data-stu-id="f47fa-124">All measures, like **Total Sales**, are stored in the **Sales** fact table.</span></span>
* <span data-ttu-id="f47fa-125">Er zijn vier extra gerelateerde dimensietabellen: **Item**, **tijd**, **Store**, en **regionale**.</span><span class="sxs-lookup"><span data-stu-id="f47fa-125">There are four additional related dimension tables: **Item**, **Time**, **Store**, and **District**.</span></span>
* <span data-ttu-id="f47fa-126">De pijlen op de relatie regels aangeven welke filters van één tabel naar een andere stromen kunnen manier.</span><span class="sxs-lookup"><span data-stu-id="f47fa-126">The arrows on the relationship lines indicate which way filters can flow from one table to another.</span></span> <span data-ttu-id="f47fa-127">Bijvoorbeeld, als een filter is geplaatst **tijd [datum]**, in het huidige schema deze alleen filtert u de waarden in de **verkoop** tabel.</span><span class="sxs-lookup"><span data-stu-id="f47fa-127">For example, if a filter is placed on **Time[Date]**, in the current schema it would only filter down values in the **Sales** table.</span></span> <span data-ttu-id="f47fa-128">Er zijn geen andere tabellen wordt beïnvloed door dit filter omdat alle van de pijlen op de relatie regels naar de tabel sales en niet verwijderd verwijzen.</span><span class="sxs-lookup"><span data-stu-id="f47fa-128">No other tables would be affected by this filter since all of the arrows on the relationship lines point to the sales table and not away.</span></span>
* <span data-ttu-id="f47fa-129">De **regionale** tabel geeft aan wie de manager is voor elk:</span><span class="sxs-lookup"><span data-stu-id="f47fa-129">The **District** table indicates who the manager is for each district:</span></span>
  
  ![](media/power-bi-embedded-rls/pbi-embedded-rls-district-table-4.png)

<span data-ttu-id="f47fa-130">Op basis van dit schema als we een filter toepassen op de **regionale Manager** kolom in de tabel regionale en als dat filter overeenkomt met de gebruiker het rapport weer te geven, met het filter ook omlaag worden gefilterd de **Store** en **verkoop** tabellen alleen gegevens weergeven die voor die specifieke regionale manager.</span><span class="sxs-lookup"><span data-stu-id="f47fa-130">Based on this schema, if we apply a filter to the **District Manager** column in the District table, and if that filter matches the user viewing the report, that filter will also filter down the **Store** and **Sales** tables to only show data for that particular district manager.</span></span>

<span data-ttu-id="f47fa-131">Hier ziet u hoe:</span><span class="sxs-lookup"><span data-stu-id="f47fa-131">Here’s how:</span></span>

1. <span data-ttu-id="f47fa-132">Klik op het tabblad modellering **rollen beheren**.</span><span class="sxs-lookup"><span data-stu-id="f47fa-132">On the Modeling tab, click **Manage Roles**.</span></span>  
   ![](media/power-bi-embedded-rls/pbi-embedded-rls-modeling-tab-5.png)
2. <span data-ttu-id="f47fa-133">Maak een nieuwe rol aangeroepen **Manager**.</span><span class="sxs-lookup"><span data-stu-id="f47fa-133">Create a new role called **Manager**.</span></span>  
   ![](media/power-bi-embedded-rls/pbi-embedded-rls-manager-role-6.png)
3. <span data-ttu-id="f47fa-134">In de **regionale** tabel voert de volgende DAX-expressie: **[regionale Manager] USERNAME() =**</span><span class="sxs-lookup"><span data-stu-id="f47fa-134">In the **District** table enter the following DAX expression: **[District Manager] = USERNAME()**</span></span>  
   ![](media/power-bi-embedded-rls/pbi-embedded-rls-manager-role-7.png)
4. <span data-ttu-id="f47fa-135">Om ervoor te zorgen dat de regels werkt, op de **modelleren** tabblad **weergave als rollen**, en voer de volgende:</span><span class="sxs-lookup"><span data-stu-id="f47fa-135">To make sure the rules are working, on the **Modeling** tab, click **View as Roles**, and then enter the following:</span></span>  
   ![](media/power-bi-embedded-rls/pbi-embedded-rls-view-as-roles-8.png)
   
   <span data-ttu-id="f47fa-136">Gegevens worden nu door de rapporten worden weergegeven alsof u zijn aangemeld als **Andrew Ma**.</span><span class="sxs-lookup"><span data-stu-id="f47fa-136">The reports will now show data as if you were signed in as **Andrew Ma**.</span></span>

<span data-ttu-id="f47fa-137">Filter toe te passen, de manier waarop werkwijze, wordt gefilterd op alle records in de **regionale**, **Store**, en **verkoop** tabellen.</span><span class="sxs-lookup"><span data-stu-id="f47fa-137">Applying the filter, the way we did here, will filter down all records in the **District**, **Store**, and **Sales** tables.</span></span> <span data-ttu-id="f47fa-138">Echter, vanwege de Filterrichting van de relaties tussen **verkoop** en **tijd**, **verkoop** en **Item**, en **Item** en **tijd** tabellen worden niet gefilterd omlaag.</span><span class="sxs-lookup"><span data-stu-id="f47fa-138">However, because of the filter direction on the relationships between **Sales** and **Time**, **Sales** and **Item**, and **Item** and **Time** tables will not be filtered down.</span></span>

![](media/power-bi-embedded-rls/pbi-embedded-rls-diagram-view-9.png)

<span data-ttu-id="f47fa-139">Die mogelijk voor deze vereiste ok, echter als we managers items waarvoor ze niet beschikken over een verkopen zien, niet wilt dat we kan bidirectionele cross-filteren voor de relatie inschakelen en het beveiligingsfilter in beide richtingen stromen.</span><span class="sxs-lookup"><span data-stu-id="f47fa-139">That may be ok for this requirement, however, if we don’t want managers to see items for which they don’t have any sales, we could turn on bidirectional cross-filtering for the relationship and flow the security filter in both directions.</span></span> <span data-ttu-id="f47fa-140">Dit kan worden gedaan door het bewerken van de relatie tussen **verkoop** en **Item**, zoals deze:</span><span class="sxs-lookup"><span data-stu-id="f47fa-140">This can be done by editing the relationship between **Sales** and **Item**, like this:</span></span>

![](media/power-bi-embedded-rls/pbi-embedded-rls-edit-relationship-10.png)

<span data-ttu-id="f47fa-141">Filters kunnen nu ook stromen van de verkoop-tabel om de **Item** tabel:</span><span class="sxs-lookup"><span data-stu-id="f47fa-141">Now, filters can also flow from the Sales table to the **Item** table:</span></span>

![](media/power-bi-embedded-rls/pbi-embedded-rls-diagram-view-11.png)

> [!NOTE]
> <span data-ttu-id="f47fa-142">Als u de modus DirectQuery voor uw gegevens, moet u inschakelen bidirectionele cross filteren op deze twee opties selecteren:</span><span class="sxs-lookup"><span data-stu-id="f47fa-142">If you're using DirectQuery mode for your data, you will need to enable bidirectional-cross filtering by selecting these two options:</span></span>

1. <span data-ttu-id="f47fa-143">**Bestand** -> **opties en instellingen** -> **Voorbeeldfuncties** -> **inschakelen kruislings filteren in beide richtingen voor DirectQuery**.</span><span class="sxs-lookup"><span data-stu-id="f47fa-143">**File** -> **Options and Settings** -> **Preview Features** -> **Enable cross filtering in both directions for DirectQuery**.</span></span>
2. <span data-ttu-id="f47fa-144">**Bestand** -> **opties en instellingen** -> **DirectQuery** -> **onbeperkte meting in DirectQuery-modus toestaan**.</span><span class="sxs-lookup"><span data-stu-id="f47fa-144">**File** -> **Options and Settings** -> **DirectQuery** -> **Allow unrestricted measure in DirectQuery mode**.</span></span>

<span data-ttu-id="f47fa-145">Voor meer informatie over bidirectionele cross-filtering, downloaden de [bidirectionele cross-filteren in SQL Server Analysis Services 2016 en Power BI Desktop](http://download.microsoft.com/download/2/7/8/2782DF95-3E0D-40CD-BFC8-749A2882E109/Bidirectional cross-filtering in Analysis Services 2016 and Power BI.docx) technisch document.</span><span class="sxs-lookup"><span data-stu-id="f47fa-145">To learn more about bidirectional cross-filtering, download the [Bidirectional cross-filtering in SQL Server Analysis Services 2016 and Power BI Desktop](http://download.microsoft.com/download/2/7/8/2782DF95-3E0D-40CD-BFC8-749A2882E109/Bidirectional cross-filtering in Analysis Services 2016 and Power BI.docx) whitepaper.</span></span>

<span data-ttu-id="f47fa-146">Dit wordt afgerond al het werk dat moet worden gedaan in Power BI Desktop, maar er is een meer stuk werk dat worden gedaan moet om de RLS regels dat hebben we werken in Power BI Embedded gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="f47fa-146">This wraps up all the work that needs to be done in Power BI Desktop, but there’s one more piece of work that needs to be done to make the RLS rules we defined work in Power BI Embedded.</span></span> <span data-ttu-id="f47fa-147">Gebruikers worden geverifieerd en geautoriseerd door uw toepassing en App-tokens worden gebruikt voor die gebruikerstoegang verlenen tot een specifiek Power BI Embedded rapport.</span><span class="sxs-lookup"><span data-stu-id="f47fa-147">Users are authenticated and authorized by your application and App tokens are used to grant that user access to a specific Power BI Embedded report.</span></span> <span data-ttu-id="f47fa-148">Power BI Embedded geen specifieke gegevens die op die de gebruiker is.</span><span class="sxs-lookup"><span data-stu-id="f47fa-148">Power BI Embedded doesn’t have any specific information on who your user is.</span></span> <span data-ttu-id="f47fa-149">Voor RLS werken, moet u enkele aanvullende context doorgeven als onderdeel van uw app-token:</span><span class="sxs-lookup"><span data-stu-id="f47fa-149">For RLS to work, you’ll need to pass some additional context as part of your app token:</span></span>

* <span data-ttu-id="f47fa-150">**gebruikersnaam** (optioneel) – gebruikt voor beveiliging op Rijniveau dit is een tekenreeks die kan worden gebruikt om vast te stellen van de gebruiker bij het toepassen van RLS regels.</span><span class="sxs-lookup"><span data-stu-id="f47fa-150">**username** (optional) – Used with RLS this is a string that can be used to help identify the user when applying RLS rules.</span></span> <span data-ttu-id="f47fa-151">Zie rij beveiliging op rijniveau met Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="f47fa-151">See Using Row Level Security with Power BI Embedded</span></span>
* <span data-ttu-id="f47fa-152">**rollen** : een tekenreeks met de rollen selecteren bij het toepassen van regels voor beveiliging op rijniveau.</span><span class="sxs-lookup"><span data-stu-id="f47fa-152">**roles** – A string containing the roles to select when applying Row Level Security rules.</span></span> <span data-ttu-id="f47fa-153">Als meer dan één rol wordt doorgegeven, moeten worden doorgegeven als een tekenreeksmatrix.</span><span class="sxs-lookup"><span data-stu-id="f47fa-153">If passing more than one role, they should be passed as a string array.</span></span>

<span data-ttu-id="f47fa-154">Maken van het token met behulp van de [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#Microsoft_PowerBI_Security_PowerBIToken_CreateReportEmbedToken_System_String_System_String_System_String_System_DateTime_System_String_System_Collections_Generic_IEnumerable_System_String__) methode.</span><span class="sxs-lookup"><span data-stu-id="f47fa-154">You create the token by using the [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#Microsoft_PowerBI_Security_PowerBIToken_CreateReportEmbedToken_System_String_System_String_System_String_System_DateTime_System_String_System_Collections_Generic_IEnumerable_System_String__) method.</span></span> <span data-ttu-id="f47fa-155">Als de eigenschap username aanwezig is, moet u ook ten minste één waarde doorgeven in rollen.</span><span class="sxs-lookup"><span data-stu-id="f47fa-155">If the username property is present, you must also pass at least one value in roles.</span></span>

<span data-ttu-id="f47fa-156">U kan bijvoorbeeld de EmbedSample wijzigen.</span><span class="sxs-lookup"><span data-stu-id="f47fa-156">For example, you could change the EmbedSample.</span></span> <span data-ttu-id="f47fa-157">DashboardController regel 55 kan worden bijgewerkt vanuit</span><span class="sxs-lookup"><span data-stu-id="f47fa-157">DashboardController line 55 could be updated from</span></span>

    var embedToken = PowerBIToken.CreateReportEmbedToken(this.workspaceCollection, this.workspaceId, report.Id);

<span data-ttu-id="f47fa-158">tot</span><span class="sxs-lookup"><span data-stu-id="f47fa-158">to</span></span>

    var embedToken = PowerBIToken.CreateReportEmbedToken(this.workspaceCollection, this.workspaceId, report.Id, "Andrew Ma", ["Manager"]);'

<span data-ttu-id="f47fa-159">Het volledige app-token wordt als volgt uitzien:</span><span class="sxs-lookup"><span data-stu-id="f47fa-159">The full app token will look something like this:</span></span>

![](media/power-bi-embedded-rls/pbi-embedded-rls-app-token-string-12.png)

<span data-ttu-id="f47fa-160">Nu met alle benodigde onderdelen samen zult wanneer iemand zich aanmeldt bij de toepassing om dit rapport weer te geven ze alleen kunnen zien van de gegevens die ze zien, kunnen zoals gedefinieerd door onze beveiliging.</span><span class="sxs-lookup"><span data-stu-id="f47fa-160">Now, with all the pieces together, when someone logs into our application to view this report, they’ll only be able to see the data that they are allowed to see, as defined by our row-level security.</span></span>

![](media/power-bi-embedded-rls/pbi-embedded-rls-dashboard-13.png)

## <a name="see-also"></a><span data-ttu-id="f47fa-161">Zie ook</span><span class="sxs-lookup"><span data-stu-id="f47fa-161">See also</span></span>

[<span data-ttu-id="f47fa-162">Beveiliging (RLS) met Power</span><span class="sxs-lookup"><span data-stu-id="f47fa-162">Row-level security (RLS) with Power</span></span>](https://powerbi.microsoft.com/en-us/documentation/powerbi-admin-rls/)  
[<span data-ttu-id="f47fa-163">Verifiëren en autoriseren in Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="f47fa-163">Authenticating and authorizing in Power BI Embedded</span></span>](power-bi-embedded-app-token-flow.md)  
[<span data-ttu-id="f47fa-164">Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="f47fa-164">Power BI Desktop</span></span>](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)  
[<span data-ttu-id="f47fa-165">Voorbeeld van ingesloten JavaScript</span><span class="sxs-lookup"><span data-stu-id="f47fa-165">JavaScript Embed Sample</span></span>](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
<span data-ttu-id="f47fa-166">Nog vragen?</span><span class="sxs-lookup"><span data-stu-id="f47fa-166">More questions?</span></span> [<span data-ttu-id="f47fa-167">Probeer de Power BI-community</span><span class="sxs-lookup"><span data-stu-id="f47fa-167">Try the Power BI Community</span></span>](http://community.powerbi.com/)


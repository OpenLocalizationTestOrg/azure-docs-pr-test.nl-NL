---
title: aaaRow beveiligingsniveau met Power BI Embedded
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
ms.openlocfilehash: 384f78826ecc710cf8f101b251ae68b074f3e98b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="row-level-security-with-power-bi-embedded"></a><span data-ttu-id="40a44-103">Beveiliging op rijniveau in Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="40a44-103">Row level security with Power BI Embedded</span></span>

<span data-ttu-id="40a44-104">Beveiliging op rijniveau (RLS) kan worden gebruikt toorestrict gebruiker toegang tot tooparticular gegevens binnen een rapport of de gegevensset, zodat voor meerdere verschillende gebruikers toouse Hallo hetzelfde rapport tijdens alle zien van andere gegevens.</span><span class="sxs-lookup"><span data-stu-id="40a44-104">Row level security (RLS) can be used toorestrict user access tooparticular data within a report or dataset, allowing for multiple different users toouse hello same report while all seeing different data.</span></span> <span data-ttu-id="40a44-105">Power BI Embedded biedt nu ondersteuning voor gegevenssets die zijn geconfigureerd voor beveiliging op Rijniveau.</span><span class="sxs-lookup"><span data-stu-id="40a44-105">Power BI Embedded now supports datasets configured with RLS.</span></span>

![](media/power-bi-embedded-rls/pbi-embedded-rls-flow-1.png)

<span data-ttu-id="40a44-106">Volgorde tootake profiteren van RLS is het belangrijk dat u begrijpt dat drie belangrijkste concepten; Gebruikers, rollen en -regels.</span><span class="sxs-lookup"><span data-stu-id="40a44-106">In order tootake advantage of RLS, it’s important you understand three main concepts; Users, Roles, and Rules.</span></span> <span data-ttu-id="40a44-107">Laten we dichter bij elke:</span><span class="sxs-lookup"><span data-stu-id="40a44-107">Let’s take a closer look at each:</span></span>

<span data-ttu-id="40a44-108">**Gebruikers** – deze bekijkt hello werkelijke eindgebruikers rapporten.</span><span class="sxs-lookup"><span data-stu-id="40a44-108">**Users** –  These are hello actual end-users viewing reports.</span></span> <span data-ttu-id="40a44-109">Gebruikers worden geïdentificeerd in Power BI Embedded door Hallo gebruikersnaam eigenschap in een App-Token.</span><span class="sxs-lookup"><span data-stu-id="40a44-109">In Power BI Embedded, users are identified by hello username property in an App Token.</span></span>

<span data-ttu-id="40a44-110">**Rollen** – gebruikers deel uitmaken van tooroles.</span><span class="sxs-lookup"><span data-stu-id="40a44-110">**Roles** – Users belong tooroles.</span></span> <span data-ttu-id="40a44-111">Een rol is een container voor regels en kan de naam zoals 'Sales Manager' of 'Vertegenwoordiger'.</span><span class="sxs-lookup"><span data-stu-id="40a44-111">A role is a container for rules and can be named something like “Sales Manager” or “Sales Rep”.</span></span> <span data-ttu-id="40a44-112">In Power BI Embedded worden gebruikers geïdentificeerd door de eigenschap Hallo rollen in een App-Token.</span><span class="sxs-lookup"><span data-stu-id="40a44-112">In Power BI Embedded, users are identified by hello roles property in an App Token.</span></span>

<span data-ttu-id="40a44-113">**Regels** : rollen regels hebben en deze regels zijn Hallo werkelijke filters die toobe toegepast toohello gegevens gaat.</span><span class="sxs-lookup"><span data-stu-id="40a44-113">**Rules** – Roles have rules, and those rules are hello actual filters that are going toobe applied toohello data.</span></span> <span data-ttu-id="40a44-114">Dit wordt mogelijk net zo eenvoudig als ' land Verenigde Staten = ' of iets meer dynamische.</span><span class="sxs-lookup"><span data-stu-id="40a44-114">This could be as simple as “Country = USA” or something much more dynamic.</span></span>

### <a name="example"></a><span data-ttu-id="40a44-115">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="40a44-115">Example</span></span>

<span data-ttu-id="40a44-116">Hallo rest van dit artikel bieden we een voorbeeld van RLS ontwerpen en verbruikt die in een ingesloten toepassing.</span><span class="sxs-lookup"><span data-stu-id="40a44-116">For hello rest of this article, we’ll provide an example of authoring RLS, and then consuming that within an embedded application.</span></span> <span data-ttu-id="40a44-117">Dit voorbeeld wordt Hallo [Retail Analysis Sample](http://go.microsoft.com/fwlink/?LinkID=780547) PBIX-bestand.</span><span class="sxs-lookup"><span data-stu-id="40a44-117">Our example uses hello [Retail Analysis Sample](http://go.microsoft.com/fwlink/?LinkID=780547) PBIX file.</span></span>

![](media/power-bi-embedded-rls/pbi-embedded-rls-scenario-2.png)

<span data-ttu-id="40a44-118">Onze Retail Analysis sample verkoopcijfers voor alle Hallo winkels in een bepaalde winkelketen.</span><span class="sxs-lookup"><span data-stu-id="40a44-118">Our Retail Analysis sample shows sales for all hello stores in a particular retail chain.</span></span> <span data-ttu-id="40a44-119">Zonder RLS, ongeacht welke regionale manager zich aanmeldt en weergaven hello rapport, ze ziet Hallo dezelfde gegevens.</span><span class="sxs-lookup"><span data-stu-id="40a44-119">Without RLS, no matter which district manager signs in and views hello report, they’ll see hello same data.</span></span> <span data-ttu-id="40a44-120">Senior management heeft bepaald dat elke regionale manager moet alleen zien Hallo sales voor Hallo winkels die ze beheren en toodo, kunnen we RLS gebruiken.</span><span class="sxs-lookup"><span data-stu-id="40a44-120">Senior management has determined each district manager should only see hello sales for hello stores they manage, and toodo this, we can use RLS.</span></span>

<span data-ttu-id="40a44-121">RLS is geschreven in Power BI Desktop.</span><span class="sxs-lookup"><span data-stu-id="40a44-121">RLS is authored in Power BI Desktop.</span></span> <span data-ttu-id="40a44-122">Hallo gegevensset en het rapport die worden geopend, kunnen we toodiagram weergave toosee Hallo schema switch:</span><span class="sxs-lookup"><span data-stu-id="40a44-122">When hello dataset and report are opened, we can switch toodiagram view toosee hello schema:</span></span>

![](media/power-bi-embedded-rls/pbi-embedded-rls-diagram-view-3.png)

<span data-ttu-id="40a44-123">Hier volgen enkele dingen toonotice met dit schema:</span><span class="sxs-lookup"><span data-stu-id="40a44-123">Here are a few things toonotice with this schema:</span></span>

* <span data-ttu-id="40a44-124">Alle maateenheden zoals **totale verkoop**, worden opgeslagen in Hallo **verkoop** feitentabel.</span><span class="sxs-lookup"><span data-stu-id="40a44-124">All measures, like **Total Sales**, are stored in hello **Sales** fact table.</span></span>
* <span data-ttu-id="40a44-125">Er zijn vier extra gerelateerde dimensietabellen: **Item**, **tijd**, **Store**, en **regionale**.</span><span class="sxs-lookup"><span data-stu-id="40a44-125">There are four additional related dimension tables: **Item**, **Time**, **Store**, and **District**.</span></span>
* <span data-ttu-id="40a44-126">Hallo pijlen op Hallo relatie regels aangeven hoe filters van één tabel tooanother stromen kunnen.</span><span class="sxs-lookup"><span data-stu-id="40a44-126">hello arrows on hello relationship lines indicate which way filters can flow from one table tooanother.</span></span> <span data-ttu-id="40a44-127">Bijvoorbeeld, als een filter is geplaatst **tijd [datum]**, in het huidige schema Hallo deze alleen filtert u omlaag waarden in Hallo **verkoop** tabel.</span><span class="sxs-lookup"><span data-stu-id="40a44-127">For example, if a filter is placed on **Time[Date]**, in hello current schema it would only filter down values in hello **Sales** table.</span></span> <span data-ttu-id="40a44-128">Er zijn geen andere tabellen wordt beïnvloed door dit filter sinds alle Hallo pijlen Hallo relatie punt toohello verkoop tabel en niet verwijderd.</span><span class="sxs-lookup"><span data-stu-id="40a44-128">No other tables would be affected by this filter since all of hello arrows on hello relationship lines point toohello sales table and not away.</span></span>
* <span data-ttu-id="40a44-129">Hallo **regionale** tabel geeft aan wie Hallo manager is voor elk:</span><span class="sxs-lookup"><span data-stu-id="40a44-129">hello **District** table indicates who hello manager is for each district:</span></span>
  
  ![](media/power-bi-embedded-rls/pbi-embedded-rls-district-table-4.png)

<span data-ttu-id="40a44-130">Op basis van dit schema als we een toohello filter toepassen **regionale Manager** kolom in tabel regionale Hallo en als Hallo gebruiker Hallo rapport weergeven met het filter overeenkomt met het filter ook omlaag hello wordt filteren **Store**en **verkoop** tabellen tooonly gegevens weergeven die voor die specifieke regionale manager.</span><span class="sxs-lookup"><span data-stu-id="40a44-130">Based on this schema, if we apply a filter toohello **District Manager** column in hello District table, and if that filter matches hello user viewing hello report, that filter will also filter down hello **Store** and **Sales** tables tooonly show data for that particular district manager.</span></span>

<span data-ttu-id="40a44-131">Hier ziet u hoe:</span><span class="sxs-lookup"><span data-stu-id="40a44-131">Here’s how:</span></span>

1. <span data-ttu-id="40a44-132">Klik op Hallo modellering tabblad op **rollen beheren**.</span><span class="sxs-lookup"><span data-stu-id="40a44-132">On hello Modeling tab, click **Manage Roles**.</span></span>  
   ![](media/power-bi-embedded-rls/pbi-embedded-rls-modeling-tab-5.png)
2. <span data-ttu-id="40a44-133">Maak een nieuwe rol aangeroepen **Manager**.</span><span class="sxs-lookup"><span data-stu-id="40a44-133">Create a new role called **Manager**.</span></span>  
   ![](media/power-bi-embedded-rls/pbi-embedded-rls-manager-role-6.png)
3. <span data-ttu-id="40a44-134">In Hallo **regionale** tabel Voer Hallo DAX-expressie te volgen: **[regionale Manager] USERNAME() =**</span><span class="sxs-lookup"><span data-stu-id="40a44-134">In hello **District** table enter hello following DAX expression: **[District Manager] = USERNAME()**</span></span>  
   ![](media/power-bi-embedded-rls/pbi-embedded-rls-manager-role-7.png)
4. <span data-ttu-id="40a44-135">toomake ervoor Hallo regels werken op Hallo **modelleren** tabblad **weergave als rollen**, en voer de volgende Hallo:</span><span class="sxs-lookup"><span data-stu-id="40a44-135">toomake sure hello rules are working, on hello **Modeling** tab, click **View as Roles**, and then enter hello following:</span></span>  
   ![](media/power-bi-embedded-rls/pbi-embedded-rls-view-as-roles-8.png)
   
   <span data-ttu-id="40a44-136">Hallo rapporten worden nu gegevens weergegeven als u zijn aangemeld als **Andrew Ma**.</span><span class="sxs-lookup"><span data-stu-id="40a44-136">hello reports will now show data as if you were signed in as **Andrew Ma**.</span></span>

<span data-ttu-id="40a44-137">Hallo-filter, Hallo manier werkwijze, toepassen worden gefilterd omlaag alle records in Hallo **regionale**, **Store**, en **verkoop** tabellen.</span><span class="sxs-lookup"><span data-stu-id="40a44-137">Applying hello filter, hello way we did here, will filter down all records in hello **District**, **Store**, and **Sales** tables.</span></span> <span data-ttu-id="40a44-138">Echter, vanwege de Filterrichting Hallo op Hallo relaties tussen **verkoop** en **tijd**, **verkoop** en **Item**, en **Item** en **tijd** tabellen worden niet gefilterd omlaag.</span><span class="sxs-lookup"><span data-stu-id="40a44-138">However, because of hello filter direction on hello relationships between **Sales** and **Time**, **Sales** and **Item**, and **Item** and **Time** tables will not be filtered down.</span></span>

![](media/power-bi-embedded-rls/pbi-embedded-rls-diagram-view-9.png)

<span data-ttu-id="40a44-139">Die mogelijk ok voor deze vereiste, maar als we managers toosee items waarvoor ze niet beschikken over een verkoop niet wilt, we kan inschakelen bidirectionele cross filteren voor Hallo relatie en stroom Hallo beveiligingsfilter in beide richtingen.</span><span class="sxs-lookup"><span data-stu-id="40a44-139">That may be ok for this requirement, however, if we don’t want managers toosee items for which they don’t have any sales, we could turn on bidirectional cross-filtering for hello relationship and flow hello security filter in both directions.</span></span> <span data-ttu-id="40a44-140">Dit kan worden gedaan door het Hallo-relatie tussen bewerken **verkoop** en **Item**, zoals deze:</span><span class="sxs-lookup"><span data-stu-id="40a44-140">This can be done by editing hello relationship between **Sales** and **Item**, like this:</span></span>

![](media/power-bi-embedded-rls/pbi-embedded-rls-edit-relationship-10.png)

<span data-ttu-id="40a44-141">Filters kunnen nu ook stromen van Hallo verkoop tabel toohello **Item** tabel:</span><span class="sxs-lookup"><span data-stu-id="40a44-141">Now, filters can also flow from hello Sales table toohello **Item** table:</span></span>

![](media/power-bi-embedded-rls/pbi-embedded-rls-diagram-view-11.png)

> [!NOTE]
> <span data-ttu-id="40a44-142">Als u de modus DirectQuery voor uw gegevens, moet u tooenable bidirectionele-cross filteren op deze twee opties selecteren:</span><span class="sxs-lookup"><span data-stu-id="40a44-142">If you're using DirectQuery mode for your data, you will need tooenable bidirectional-cross filtering by selecting these two options:</span></span>

1. <span data-ttu-id="40a44-143">**Bestand** -> **opties en instellingen** -> **Voorbeeldfuncties** -> **inschakelen kruislings filteren in beide richtingen voor DirectQuery**.</span><span class="sxs-lookup"><span data-stu-id="40a44-143">**File** -> **Options and Settings** -> **Preview Features** -> **Enable cross filtering in both directions for DirectQuery**.</span></span>
2. <span data-ttu-id="40a44-144">**Bestand** -> **opties en instellingen** -> **DirectQuery** -> **onbeperkte meting in DirectQuery-modus toestaan**.</span><span class="sxs-lookup"><span data-stu-id="40a44-144">**File** -> **Options and Settings** -> **DirectQuery** -> **Allow unrestricted measure in DirectQuery mode**.</span></span>

<span data-ttu-id="40a44-145">meer informatie over bidirectionele cross-filtering, download Hallo toolearn [bidirectionele cross-filteren in SQL Server Analysis Services 2016 en Power BI Desktop](http://download.microsoft.com/download/2/7/8/2782DF95-3E0D-40CD-BFC8-749A2882E109/Bidirectional cross-filtering in Analysis Services 2016 and Power BI.docx) technisch document.</span><span class="sxs-lookup"><span data-stu-id="40a44-145">toolearn more about bidirectional cross-filtering, download hello [Bidirectional cross-filtering in SQL Server Analysis Services 2016 and Power BI Desktop](http://download.microsoft.com/download/2/7/8/2782DF95-3E0D-40CD-BFC8-749A2882E109/Bidirectional cross-filtering in Analysis Services 2016 and Power BI.docx) whitepaper.</span></span>

<span data-ttu-id="40a44-146">Dit wordt afgerond alle Hallo-werk dat toobe in Power BI Desktop uitgevoerd moet, maar er is een meer stuk werk dat toobe gedaan toomake moet Hallo RLS regels hebben we werken in Power BI Embedded gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="40a44-146">This wraps up all hello work that needs toobe done in Power BI Desktop, but there’s one more piece of work that needs toobe done toomake hello RLS rules we defined work in Power BI Embedded.</span></span> <span data-ttu-id="40a44-147">Gebruikers worden geverifieerd en geautoriseerd door uw toepassing en App-tokens zijn gebruikte toogrant die gebruiker toegang tooa specifieke Power BI Embedded rapporteren.</span><span class="sxs-lookup"><span data-stu-id="40a44-147">Users are authenticated and authorized by your application and App tokens are used toogrant that user access tooa specific Power BI Embedded report.</span></span> <span data-ttu-id="40a44-148">Power BI Embedded geen specifieke gegevens die op die de gebruiker is.</span><span class="sxs-lookup"><span data-stu-id="40a44-148">Power BI Embedded doesn’t have any specific information on who your user is.</span></span> <span data-ttu-id="40a44-149">Voor RLS toowork moet u toopass enkele aanvullende context als onderdeel van uw app-token:</span><span class="sxs-lookup"><span data-stu-id="40a44-149">For RLS toowork, you’ll need toopass some additional context as part of your app token:</span></span>

* <span data-ttu-id="40a44-150">**gebruikersnaam** (optioneel) – gebruikt voor beveiliging op Rijniveau dit is een tekenreeks die kan worden gebruikt toohelp identificatie Hallo gebruiker bij het toepassen van RLS regels.</span><span class="sxs-lookup"><span data-stu-id="40a44-150">**username** (optional) – Used with RLS this is a string that can be used toohelp identify hello user when applying RLS rules.</span></span> <span data-ttu-id="40a44-151">Zie rij beveiliging op rijniveau met Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="40a44-151">See Using Row Level Security with Power BI Embedded</span></span>
* <span data-ttu-id="40a44-152">**rollen** : een tekenreeks met Hallo rollen tooselect bij het toepassen van regels voor beveiliging op rijniveau.</span><span class="sxs-lookup"><span data-stu-id="40a44-152">**roles** – A string containing hello roles tooselect when applying Row Level Security rules.</span></span> <span data-ttu-id="40a44-153">Als meer dan één rol wordt doorgegeven, moeten worden doorgegeven als een tekenreeksmatrix.</span><span class="sxs-lookup"><span data-stu-id="40a44-153">If passing more than one role, they should be passed as a string array.</span></span>

<span data-ttu-id="40a44-154">U Hallo-token maken met behulp van Hallo [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#Microsoft_PowerBI_Security_PowerBIToken_CreateReportEmbedToken_System_String_System_String_System_String_System_DateTime_System_String_System_Collections_Generic_IEnumerable_System_String__) methode.</span><span class="sxs-lookup"><span data-stu-id="40a44-154">You create hello token by using hello [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#Microsoft_PowerBI_Security_PowerBIToken_CreateReportEmbedToken_System_String_System_String_System_String_System_DateTime_System_String_System_Collections_Generic_IEnumerable_System_String__) method.</span></span> <span data-ttu-id="40a44-155">Als de eigenschap username Hallo aanwezig is, moet u ook ten minste één waarde doorgeven in rollen.</span><span class="sxs-lookup"><span data-stu-id="40a44-155">If hello username property is present, you must also pass at least one value in roles.</span></span>

<span data-ttu-id="40a44-156">U kan bijvoorbeeld Hallo EmbedSample wijzigen.</span><span class="sxs-lookup"><span data-stu-id="40a44-156">For example, you could change hello EmbedSample.</span></span> <span data-ttu-id="40a44-157">DashboardController regel 55 kan worden bijgewerkt vanuit</span><span class="sxs-lookup"><span data-stu-id="40a44-157">DashboardController line 55 could be updated from</span></span>

    var embedToken = PowerBIToken.CreateReportEmbedToken(this.workspaceCollection, this.workspaceId, report.Id);

<span data-ttu-id="40a44-158">tot</span><span class="sxs-lookup"><span data-stu-id="40a44-158">to</span></span>

    var embedToken = PowerBIToken.CreateReportEmbedToken(this.workspaceCollection, this.workspaceId, report.Id, "Andrew Ma", ["Manager"]);'

<span data-ttu-id="40a44-159">Hallo volledige app-token wordt als volgt uitzien:</span><span class="sxs-lookup"><span data-stu-id="40a44-159">hello full app token will look something like this:</span></span>

![](media/power-bi-embedded-rls/pbi-embedded-rls-app-token-string-12.png)

<span data-ttu-id="40a44-160">Nu met alle Hallo stukken samen zult wanneer iemand zich bij onze toepassing tooview dit rapport aanmeldt ze alleen kunnen toosee Hallo gegevens die ze toosee mogen, zoals gedefinieerd door onze beveiliging.</span><span class="sxs-lookup"><span data-stu-id="40a44-160">Now, with all hello pieces together, when someone logs into our application tooview this report, they’ll only be able toosee hello data that they are allowed toosee, as defined by our row-level security.</span></span>

![](media/power-bi-embedded-rls/pbi-embedded-rls-dashboard-13.png)

## <a name="see-also"></a><span data-ttu-id="40a44-161">Zie ook</span><span class="sxs-lookup"><span data-stu-id="40a44-161">See also</span></span>

[<span data-ttu-id="40a44-162">Beveiliging (RLS) met Power</span><span class="sxs-lookup"><span data-stu-id="40a44-162">Row-level security (RLS) with Power</span></span>](https://powerbi.microsoft.com/en-us/documentation/powerbi-admin-rls/)  
[<span data-ttu-id="40a44-163">Verifiëren en autoriseren in Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="40a44-163">Authenticating and authorizing in Power BI Embedded</span></span>](power-bi-embedded-app-token-flow.md)  
[<span data-ttu-id="40a44-164">Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="40a44-164">Power BI Desktop</span></span>](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)  
[<span data-ttu-id="40a44-165">Voorbeeld van ingesloten JavaScript</span><span class="sxs-lookup"><span data-stu-id="40a44-165">JavaScript Embed Sample</span></span>](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
<span data-ttu-id="40a44-166">Nog vragen?</span><span class="sxs-lookup"><span data-stu-id="40a44-166">More questions?</span></span> [<span data-ttu-id="40a44-167">Probeer Hallo Power BI-Community</span><span class="sxs-lookup"><span data-stu-id="40a44-167">Try hello Power BI Community</span></span>](http://community.powerbi.com/)


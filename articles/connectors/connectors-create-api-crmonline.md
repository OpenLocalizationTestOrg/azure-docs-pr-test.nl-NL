---
title: aaaConnect tooDynamics 365 (online) vanuit Azure Logic Apps | Microsoft Docs
description: Logic app werkstromen maken die Dynamics 365 (online) entiteiten via Hallo API die door de connector Hallo Dynamics 365 beheren
services: logic-apps
cloud: Azure Stack
author: Mattp123
manager: anneta
documentationcenter: 
tags: connectors
ms.assetid: 0dc2abef-7d2c-4a2d-87ca-fad21367d135
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/10/2017
ms.author: matp; LADocs
ms.openlocfilehash: 183d7a6b8e5d2c0eecc70da0da3806e06c382df4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-toodynamics-365-from-logic-app-workflows"></a><span data-ttu-id="9249b-103">Verbinding maken met tooDynamics 365 van logic app-werkstromen</span><span class="sxs-lookup"><span data-stu-id="9249b-103">Connect tooDynamics 365 from logic app workflows</span></span>

<span data-ttu-id="9249b-104">Met Logic Apps kunt u verbinding maken met tooDynamics 365 (online) en nuttig business stromen die records maken, bijwerken items of een lijst met records geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="9249b-104">With Logic Apps, you can connect tooDynamics 365 (online) and create useful business flows that create records, update items, or return a list of records.</span></span> <span data-ttu-id="9249b-105">U kunt met Hallo Dynamics 365-connector:</span><span class="sxs-lookup"><span data-stu-id="9249b-105">With hello Dynamics 365 connector, you can:</span></span>

* <span data-ttu-id="9249b-106">Bouw uw zakelijke flow op basis van Hallo gegevens die u van Dynamics 365 (online).</span><span class="sxs-lookup"><span data-stu-id="9249b-106">Build your business flow based on hello data you get from Dynamics 365 (online).</span></span>
* <span data-ttu-id="9249b-107">Gebruik de acties die reageert en vervolgens Hallo uitvoer beschikbaar voor andere acties.</span><span class="sxs-lookup"><span data-stu-id="9249b-107">Use actions that get a response and then make hello output available for other actions.</span></span> <span data-ttu-id="9249b-108">Wanneer een item wordt bijgewerkt in Dynamics 365 (online), kunt u bijvoorbeeld een e-mailbericht met Office 365 verzenden.</span><span class="sxs-lookup"><span data-stu-id="9249b-108">For example, when an item is updated in Dynamics 365 (online), you can send an email using Office 365.</span></span>

<span data-ttu-id="9249b-109">Dit onderwerp leest u hoe een logische app toocreate die maakt een taak in Dynamics 365 wanneer een nieuwe lead in Dynamics 365 wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="9249b-109">This topic shows you how toocreate a logic app that creates a task in Dynamics 365 whenever a new lead is created in Dynamics 365.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9249b-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="9249b-110">Prerequisites</span></span>
* <span data-ttu-id="9249b-111">Een Azure-account.</span><span class="sxs-lookup"><span data-stu-id="9249b-111">An Azure account.</span></span>
* <span data-ttu-id="9249b-112">Een account met Dynamics 365 (online).</span><span class="sxs-lookup"><span data-stu-id="9249b-112">A Dynamics 365 (online) account.</span></span>

## <a name="create-a-task-when-a-new-lead-is-created-in-dynamics-365"></a><span data-ttu-id="9249b-113">Een taak wordt gemaakt wanneer een nieuwe lead in Dynamics 365 wordt gemaakt</span><span class="sxs-lookup"><span data-stu-id="9249b-113">Create a task when a new lead is created in Dynamics 365</span></span>

1.  <span data-ttu-id="9249b-114">[Meld u aan tooAzure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="9249b-114">[Sign in tooAzure](https://portal.azure.com).</span></span>

2.  <span data-ttu-id="9249b-115">Typ in hello Azure search `Logic apps`, en druk op ENTER.</span><span class="sxs-lookup"><span data-stu-id="9249b-115">In hello Azure search box, type `Logic apps`, and press ENTER.</span></span>

      ![Logische Apps zoeken](./media/connectors-create-api-crmonline/find-logic-apps.png)

3.  <span data-ttu-id="9249b-117">Onder **Logic apps**, klikt u op **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="9249b-117">Under **Logic apps**, click **Add**.</span></span>

      ![LogicApp toevoegen](./media/connectors-create-api-crmonline/add-logic-app.png)

4.  <span data-ttu-id="9249b-119">toocreate hello logische app, volledige Hallo **naam**, **abonnement**, **resourcegroep**, en **locatie** velden en klik vervolgens op  **Maak**.</span><span class="sxs-lookup"><span data-stu-id="9249b-119">toocreate hello logic app, complete hello **Name**, **Subscription**, **Resource Group**, and **Location** fields, and then click **Create**.</span></span>

5.  <span data-ttu-id="9249b-120">Selecteer de nieuwe logische app Hallo.</span><span class="sxs-lookup"><span data-stu-id="9249b-120">Select hello new logic app.</span></span> <span data-ttu-id="9249b-121">Wanneer u Hallo ontvangt **implementatie is voltooid** melding, klikt u op **vernieuwen**.</span><span class="sxs-lookup"><span data-stu-id="9249b-121">When you receive hello **Deployment Succeeded** notification, click **Refresh**.</span></span>

6.  <span data-ttu-id="9249b-122">Onder **ontwikkelingsprogramma's**, klikt u op **Logic App-ontwerper**.</span><span class="sxs-lookup"><span data-stu-id="9249b-122">Under **Development Tools**, click **Logic App Designer**.</span></span> <span data-ttu-id="9249b-123">Klik in de lijst met sjablonen hello, **lege logische App**.</span><span class="sxs-lookup"><span data-stu-id="9249b-123">In hello template list, click **Blank Logic App**.</span></span>

7.  <span data-ttu-id="9249b-124">Typ in het zoekvak Hallo `Dynamics 365`.</span><span class="sxs-lookup"><span data-stu-id="9249b-124">In hello search box, type `Dynamics 365`.</span></span> <span data-ttu-id="9249b-125">Van Hallo Dynamics 365 lijst activeert, selecteert u **Dynamics 365 – wanneer een record gemaakt**.</span><span class="sxs-lookup"><span data-stu-id="9249b-125">From hello Dynamics 365 triggers list, select **Dynamics 365 – When a record is created**.</span></span>

8.  <span data-ttu-id="9249b-126">Als u na vragen aan gebruiker toosign in tooDynamics 365, moet u dat nu doen.</span><span class="sxs-lookup"><span data-stu-id="9249b-126">If you are prompted toosign in tooDynamics 365, do so now.</span></span>

9.  <span data-ttu-id="9249b-127">Voer in Hallo trigger details Hallo volgende informatie:</span><span class="sxs-lookup"><span data-stu-id="9249b-127">In hello trigger details, enter hello following information:</span></span>

  * <span data-ttu-id="9249b-128">**Naam van de organisatie**.</span><span class="sxs-lookup"><span data-stu-id="9249b-128">**Organization Name**.</span></span> <span data-ttu-id="9249b-129">Hallo Dynamics 365 exemplaar gewenste Hallo logic app toolisten te selecteren.</span><span class="sxs-lookup"><span data-stu-id="9249b-129">Select hello Dynamics 365 instance that you want hello logic app toolisten to.</span></span>

  * <span data-ttu-id="9249b-130">**Naam van de entiteit**.</span><span class="sxs-lookup"><span data-stu-id="9249b-130">**Entity Name**.</span></span> <span data-ttu-id="9249b-131">Hallo-entiteit die u wilt dat toolisten te selecteren.</span><span class="sxs-lookup"><span data-stu-id="9249b-131">Select hello entity that you want toolisten to.</span></span> <span data-ttu-id="9249b-132">Deze gebeurtenis fungeert als een trigger toostart Hallo logische app.</span><span class="sxs-lookup"><span data-stu-id="9249b-132">This event acts as a trigger toostart hello logic app.</span></span> 
  <span data-ttu-id="9249b-133">In dit overzicht **leidt** is geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="9249b-133">In this walkthrough, **Leads** is selected.</span></span>

  * <span data-ttu-id="9249b-134">**Hoe vaak wilt u toocheck voor artikelen?**</span><span class="sxs-lookup"><span data-stu-id="9249b-134">**How often do you want toocheck for items?**</span></span> <span data-ttu-id="9249b-135">Deze waarden instellen hoe vaak Hallo logische app controleert op updates gerelateerde toohello trigger.</span><span class="sxs-lookup"><span data-stu-id="9249b-135">These values set how often hello logic app checks for updates related toohello trigger.</span></span> <span data-ttu-id="9249b-136">de standaardinstelling Hallo is toocheck voor elke drie minuten-updates.</span><span class="sxs-lookup"><span data-stu-id="9249b-136">hello default setting is toocheck for updates every three minutes.</span></span>

    * <span data-ttu-id="9249b-137">**Frequentie**.</span><span class="sxs-lookup"><span data-stu-id="9249b-137">**Frequency**.</span></span> <span data-ttu-id="9249b-138">Selecteer seconden, minuten, uren of dagen.</span><span class="sxs-lookup"><span data-stu-id="9249b-138">Select seconds, minutes, hours, or days.</span></span>

    * <span data-ttu-id="9249b-139">**Interval**.</span><span class="sxs-lookup"><span data-stu-id="9249b-139">**Interval**.</span></span> <span data-ttu-id="9249b-140">Hallo aantal seconden, minuten, uren of dagen dat u wilt dat toopass voordat u het volgende selectievakje Hallo invoeren.</span><span class="sxs-lookup"><span data-stu-id="9249b-140">Enter hello number of seconds, minutes, hours, or days that you want toopass before hello next check.</span></span>

      ![Details van de logica voor App Trigger](./media/connectors-create-api-crmonline/trigger-details.png)

10. <span data-ttu-id="9249b-142">Klik op **nieuwe stap**, en klik vervolgens op **een actie toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="9249b-142">Click **New step**, and then click **Add an action**.</span></span>

11. <span data-ttu-id="9249b-143">Typ in het zoekvak Hallo `Dynamics 365`.</span><span class="sxs-lookup"><span data-stu-id="9249b-143">In hello search box, type `Dynamics 365`.</span></span> <span data-ttu-id="9249b-144">Selecteer in de lijst Acties Hallo **Dynamics 365: Maak een nieuwe record**.</span><span class="sxs-lookup"><span data-stu-id="9249b-144">From hello actions list, select **Dynamics 365 – Create a new record**.</span></span>

12. <span data-ttu-id="9249b-145">Voer Hallo volgende informatie:</span><span class="sxs-lookup"><span data-stu-id="9249b-145">Enter hello following information:</span></span>

    * <span data-ttu-id="9249b-146">**Naam van de organisatie**.</span><span class="sxs-lookup"><span data-stu-id="9249b-146">**Organization Name**.</span></span> <span data-ttu-id="9249b-147">Selecteer Hallo Dynamics 365 instantie waar u Hallo stroom toocreate Hallo record.</span><span class="sxs-lookup"><span data-stu-id="9249b-147">Select hello Dynamics 365 instance where you want hello flow toocreate hello record.</span></span> 
    <span data-ttu-id="9249b-148">U ziet dat deze instantie geen toobe Hallo dezelfde exemplaar waar Hallo gebeurtenis wordt geactiveerd vanuit.</span><span class="sxs-lookup"><span data-stu-id="9249b-148">Notice that this instance doesn’t have toobe hello same instance where hello event is triggered from.</span></span>

    * <span data-ttu-id="9249b-149">**Naam van de entiteit**.</span><span class="sxs-lookup"><span data-stu-id="9249b-149">**Entity Name**.</span></span> <span data-ttu-id="9249b-150">Selecteer Hallo entiteit die u wilt een record toocreate wanneer Hallo gebeurtenis wordt geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="9249b-150">Select hello entity that you want toocreate a record when hello event is triggered.</span></span> 
    <span data-ttu-id="9249b-151">In dit overzicht **taken** is geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="9249b-151">In this walkthrough, **Tasks** is selected.</span></span>

13. <span data-ttu-id="9249b-152">Klik in het Hallo **onderwerp** vak dat wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="9249b-152">Click in hello **Subject** box that appears.</span></span> <span data-ttu-id="9249b-153">Uit Hallo dynamische inhoud lijst die wordt weergegeven, kunt u een van deze velden selecteren:</span><span class="sxs-lookup"><span data-stu-id="9249b-153">From hello dynamic content list that appears, you can select either of these fields:</span></span>

    * <span data-ttu-id="9249b-154">**Achternaam**.</span><span class="sxs-lookup"><span data-stu-id="9249b-154">**Last Name**.</span></span> <span data-ttu-id="9249b-155">Als u dit veld voegt Hallo achternaam voor Hallo lead in het veld onderwerp Hallo voor Hallo-taak wanneer Hallo taakrecord wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="9249b-155">Selecting this field inserts hello last name for hello lead into hello Subject field for hello task, when hello task record is created.</span></span>
    * <span data-ttu-id="9249b-156">**Onderwerp**.</span><span class="sxs-lookup"><span data-stu-id="9249b-156">**Topic**.</span></span> <span data-ttu-id="9249b-157">Als u dit veld voegt Hallo onderwerpveld voor Hallo lead in het veld onderwerp Hallo voor Hallo taak selecteert, wanneer Hallo taakrecord wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="9249b-157">Selecting this field inserts hello Topic field for hello lead into hello Subject field for hello task, when hello task record is created.</span></span> 
    <span data-ttu-id="9249b-158">Klik op **onderwerp** tooadd die toohello **onderwerp** vak.</span><span class="sxs-lookup"><span data-stu-id="9249b-158">Click **Topic** tooadd that toohello **Subject** box.</span></span>

      ![Logische App maken nieuwe records details](./media/connectors-create-api-crmonline/create-record-details.png)

14. <span data-ttu-id="9249b-160">Op de werkbalk Logic App-ontwerper Hallo **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="9249b-160">On hello Logic App Designer toolbar, click **Save**.</span></span>

    ![Logic App-ontwerper werkbalk opslaan](./media/connectors-create-api-crmonline/designer-toolbar-save.png)

15. <span data-ttu-id="9249b-162">toostart hello logische App, klikt u op **uitvoeren**.</span><span class="sxs-lookup"><span data-stu-id="9249b-162">toostart hello Logic App, click **Run**.</span></span>

    ![Logic App-ontwerper werkbalk opslaan](./media/connectors-create-api-crmonline/designer-toolbar-run.png)

16. <span data-ttu-id="9249b-164">Nu een leadrecord maken in Dynamics 365 voor verkoop en uw flow in actie zien!</span><span class="sxs-lookup"><span data-stu-id="9249b-164">Now create a lead record in Dynamics 365 for Sales and see your flow in action!</span></span>

## <a name="set-advanced-options-for-a-logic-app-step"></a><span data-ttu-id="9249b-165">Geavanceerde opties voor de stap van een logische app instellen</span><span class="sxs-lookup"><span data-stu-id="9249b-165">Set advanced options for a logic app step</span></span>

<span data-ttu-id="9249b-166">hoe toofilter gegevens in logische app stap, klikt u op toospecify **geavanceerde opties weergeven** in deze stap voegt u een filter of de volgorde door query.</span><span class="sxs-lookup"><span data-stu-id="9249b-166">toospecify how toofilter data in a logic app step, click **Show advanced options** in that step, then add a filter or order by query.</span></span>

<span data-ttu-id="9249b-167">U kunt bijvoorbeeld een filter-query tooget alleen actieve accounts gebruiken en sorteren op het Hallo-accountnaam.</span><span class="sxs-lookup"><span data-stu-id="9249b-167">For example, you can use a filter query tooget only active accounts and order by hello account name.</span></span> <span data-ttu-id="9249b-168">tooperform dit taak Hallo OData-filter-query invoeren `statuscode eq 1`, en selecteer **accountnaam** van Hallo lijst van dynamische inhoud.</span><span class="sxs-lookup"><span data-stu-id="9249b-168">tooperform this task, enter hello OData filter query `statuscode eq 1`, and select **Account Name** from hello dynamic content list.</span></span> <span data-ttu-id="9249b-169">Meer informatie: [MSDN: $filter](https://msdn.microsoft.com/library/gg309461.aspx#Anchor_1) en [$orderby](https://msdn.microsoft.com/library/gg309461.aspx#Anchor_2).</span><span class="sxs-lookup"><span data-stu-id="9249b-169">More information: [MSDN: $filter](https://msdn.microsoft.com/library/gg309461.aspx#Anchor_1) and [$orderby](https://msdn.microsoft.com/library/gg309461.aspx#Anchor_2).</span></span>

![Geavanceerde opties voor logische-app](./media/connectors-create-api-crmonline/advanced-options.png)

### <a name="best-practices-when-using-advanced-options"></a><span data-ttu-id="9249b-171">Aanbevolen procedures voor het gebruik van geavanceerde opties</span><span class="sxs-lookup"><span data-stu-id="9249b-171">Best practices when using advanced options</span></span>

<span data-ttu-id="9249b-172">Wanneer u een veld waarde tooa toevoegt, moet u Hallo veldtype overeenkomen met of u typt u een waarde of Selecteer een waarde van het Hallo-lijst met dynamische inhoud.</span><span class="sxs-lookup"><span data-stu-id="9249b-172">When you add a value tooa field, you must match hello field type whether you type a value or select a value from hello dynamic content list.</span></span>

<span data-ttu-id="9249b-173">Veldtype</span><span class="sxs-lookup"><span data-stu-id="9249b-173">Field type</span></span>  |<span data-ttu-id="9249b-174">Hoe toouse</span><span class="sxs-lookup"><span data-stu-id="9249b-174">How toouse</span></span>  |<span data-ttu-id="9249b-175">Waar toofind</span><span class="sxs-lookup"><span data-stu-id="9249b-175">Where toofind</span></span>  |<span data-ttu-id="9249b-176">Naam</span><span class="sxs-lookup"><span data-stu-id="9249b-176">Name</span></span>  |<span data-ttu-id="9249b-177">Gegevenstype</span><span class="sxs-lookup"><span data-stu-id="9249b-177">Data type</span></span>  
---------|---------|---------|---------|---------
<span data-ttu-id="9249b-178">Tekstvelden</span><span class="sxs-lookup"><span data-stu-id="9249b-178">Text fields</span></span>|<span data-ttu-id="9249b-179">Tekstvelden vereisen een enkele regel tekst of dynamische inhoud die is een type tekstveld.</span><span class="sxs-lookup"><span data-stu-id="9249b-179">Text fields require a single line of text or dynamic content that is a text type field.</span></span> <span data-ttu-id="9249b-180">Voorbeelden zijn Hallo categorie en subcategorie velden.</span><span class="sxs-lookup"><span data-stu-id="9249b-180">Examples include hello Category and Sub-Category fields.</span></span>|<span data-ttu-id="9249b-181">Instellingen > Aanpassingen > aanpassen Hallo System > entiteiten > taak > velden</span><span class="sxs-lookup"><span data-stu-id="9249b-181">Settings > Customizations > Customize hello System > Entities > Task > Fields</span></span> |<span data-ttu-id="9249b-182">category</span><span class="sxs-lookup"><span data-stu-id="9249b-182">category</span></span> |<span data-ttu-id="9249b-183">Enkele regel tekst</span><span class="sxs-lookup"><span data-stu-id="9249b-183">Single Line of Text</span></span>        
<span data-ttu-id="9249b-184">Velden geheel getal</span><span class="sxs-lookup"><span data-stu-id="9249b-184">Integer fields</span></span> | <span data-ttu-id="9249b-185">Sommige velden vereist geheel getal of dynamische inhoud die een veld van het type geheel getal is.</span><span class="sxs-lookup"><span data-stu-id="9249b-185">Some fields require integer or dynamic content that is an integer type field.</span></span> <span data-ttu-id="9249b-186">Voorbeelden zijn percentage voltooid en duur.</span><span class="sxs-lookup"><span data-stu-id="9249b-186">Examples include Percent Complete and Duration.</span></span> |<span data-ttu-id="9249b-187">Instellingen > Aanpassingen > aanpassen Hallo System > entiteiten > taak > velden</span><span class="sxs-lookup"><span data-stu-id="9249b-187">Settings > Customizations > Customize hello System > Entities > Task > Fields</span></span> |<span data-ttu-id="9249b-188">PercentComplete</span><span class="sxs-lookup"><span data-stu-id="9249b-188">percentcomplete</span></span> |<span data-ttu-id="9249b-189">Geheel getal</span><span class="sxs-lookup"><span data-stu-id="9249b-189">Whole Number</span></span>         
<span data-ttu-id="9249b-190">Datumvelden</span><span class="sxs-lookup"><span data-stu-id="9249b-190">Date fields</span></span> | <span data-ttu-id="9249b-191">Sommige velden vereisen een datum is opgegeven in de notatie dd-mm-jjjj of dynamische inhoud die is een veld van het type datum.</span><span class="sxs-lookup"><span data-stu-id="9249b-191">Some fields require a date entered in mm/dd/yyyy format or dynamic content that is a date type field.</span></span> <span data-ttu-id="9249b-192">Voorbeelden zijn gemaakt op, begindatum, werkelijke begindatum laatste op de tijd houdt, Werkelijk einde en vervaldatum.</span><span class="sxs-lookup"><span data-stu-id="9249b-192">Examples include Created On, Start Date, Actual Start, Last on Hold Time, Actual End, and Due Date.</span></span> | <span data-ttu-id="9249b-193">Instellingen > Aanpassingen > aanpassen Hallo System > entiteiten > taak > velden</span><span class="sxs-lookup"><span data-stu-id="9249b-193">Settings > Customizations > Customize hello System > Entities > Task > Fields</span></span> |<span data-ttu-id="9249b-194">createdon</span><span class="sxs-lookup"><span data-stu-id="9249b-194">createdon</span></span> |<span data-ttu-id="9249b-195">Datum en tijd</span><span class="sxs-lookup"><span data-stu-id="9249b-195">Date and Time</span></span>
<span data-ttu-id="9249b-196">Typ velden waarvoor zowel een record-ID en lookup</span><span class="sxs-lookup"><span data-stu-id="9249b-196">Fields that require both a record ID and lookup type</span></span> |<span data-ttu-id="9249b-197">Sommige velden die verwijzen naar een andere entiteitsrecord vereist zowel Hallo record-ID en het Hallo lookup-type.</span><span class="sxs-lookup"><span data-stu-id="9249b-197">Some fields that reference another entity record require both hello record ID and hello lookup type.</span></span> |<span data-ttu-id="9249b-198">Instellingen > Aanpassingen > aanpassen Hallo System > entiteiten > Account > velden</span><span class="sxs-lookup"><span data-stu-id="9249b-198">Settings > Customizations > Customize hello System > Entities > Account > Fields</span></span>  | <span data-ttu-id="9249b-199">AccountId</span><span class="sxs-lookup"><span data-stu-id="9249b-199">accountid</span></span>  | <span data-ttu-id="9249b-200">Primaire sleutel</span><span class="sxs-lookup"><span data-stu-id="9249b-200">Primary Key</span></span>

### <a name="more-examples-of-fields-that-require-both-a-record-id-and-lookup-type"></a><span data-ttu-id="9249b-201">Typ voor meer voorbeelden van de velden die vereisen een record-ID en de lookup dat</span><span class="sxs-lookup"><span data-stu-id="9249b-201">More examples of fields that require both a record ID and lookup type</span></span>
<span data-ttu-id="9249b-202">Voortbouwend op de vorige tabel hello, vindt hier u meer voorbeelden van de velden die niet met waarden die in de lijst met dynamische inhoud Hallo geselecteerd werken.</span><span class="sxs-lookup"><span data-stu-id="9249b-202">Expanding on hello previous table, here are more examples of fields that don't work with values selected from hello dynamic content list.</span></span> <span data-ttu-id="9249b-203">Deze velden vereisen in plaats daarvan beide een lookup-ID en het recordtype in Hallo velden in PowerApps ingevoerd.</span><span class="sxs-lookup"><span data-stu-id="9249b-203">Instead, these fields require both a record ID and lookup type entered into hello fields in PowerApps.</span></span>  
* <span data-ttu-id="9249b-204">Eigenaar en eigenaarstype.</span><span class="sxs-lookup"><span data-stu-id="9249b-204">Owner and Owner Type.</span></span> <span data-ttu-id="9249b-205">Hallo eigenaarveld moet een geldige gebruiker of het team record-ID.</span><span class="sxs-lookup"><span data-stu-id="9249b-205">hello Owner field must be a valid user or team record ID.</span></span> <span data-ttu-id="9249b-206">Hallo Type eigenaar moet een **systemusers** of **teams**.</span><span class="sxs-lookup"><span data-stu-id="9249b-206">hello Owner Type must be either **systemusers** or **teams**.</span></span>
* <span data-ttu-id="9249b-207">De klant en het klanttype.</span><span class="sxs-lookup"><span data-stu-id="9249b-207">Customer and Customer Type.</span></span> <span data-ttu-id="9249b-208">Hallo klant veld moet een geldig account of neem contact op met de record-ID.</span><span class="sxs-lookup"><span data-stu-id="9249b-208">hello Customer field must be a valid account or contact record ID.</span></span> <span data-ttu-id="9249b-209">Hallo Type eigenaar moet een **accounts** of **contactpersonen**.</span><span class="sxs-lookup"><span data-stu-id="9249b-209">hello Owner Type must be either **accounts** or **contacts**.</span></span>
* <span data-ttu-id="9249b-210">Met betrekking tot en met betrekking tot Type.</span><span class="sxs-lookup"><span data-stu-id="9249b-210">Regarding and Regarding Type.</span></span> <span data-ttu-id="9249b-211">Hallo met betrekking tot veld moet een geldige record-ID, zoals een account of neem contact op met de record-ID.</span><span class="sxs-lookup"><span data-stu-id="9249b-211">hello Regarding field must be a valid record ID, such as an account or contact record ID.</span></span> <span data-ttu-id="9249b-212">Hallo met betrekking tot Type moet Hallo Zoektype voor Hallo-record, zoals **accounts** of **contactpersonen**.</span><span class="sxs-lookup"><span data-stu-id="9249b-212">hello Regarding Type must be hello lookup type for hello record, such as **accounts** or **contacts**.</span></span>

<span data-ttu-id="9249b-213">Hallo wordt volgende taak maken actie voorbeeld een record voor een account dat overeenkomt met toohello record-ID toe te voegen toohello met betrekking tot veld van Hallo-taak.</span><span class="sxs-lookup"><span data-stu-id="9249b-213">hello following task creation action example adds an account record that corresponds toohello record ID adding it toohello regarding field of hello task.</span></span>

![Stroom recordId en het type account](./media/connectors-create-api-crmonline/recordid-type-account.png)

<span data-ttu-id="9249b-215">In dit voorbeeld wijst ook Hallo taak tooa specifieke gebruiker op basis van een van de gebruiker Hallo record-ID.</span><span class="sxs-lookup"><span data-stu-id="9249b-215">This example also assigns hello task tooa specific user based on hello user's record ID.</span></span>

![Stroom recordId en het type account](./media/connectors-create-api-crmonline/recordid-type-user.png)

<span data-ttu-id="9249b-217">toofind een record-ID, van het Zie volgende sectie Hallo: *Hallo record-ID vinden*</span><span class="sxs-lookup"><span data-stu-id="9249b-217">toofind a record's ID, see hello following section: *Find hello record ID*</span></span>

## <a name="find-hello-record-id"></a><span data-ttu-id="9249b-218">Hallo record-ID vinden</span><span class="sxs-lookup"><span data-stu-id="9249b-218">Find hello record ID</span></span>

1. <span data-ttu-id="9249b-219">Open een record bestaat, zoals een record.</span><span class="sxs-lookup"><span data-stu-id="9249b-219">Open a record, such as an account record.</span></span>

2. <span data-ttu-id="9249b-220">Op de werkbalk Acties Hallo **Pop uit** ![popout record](./media/connectors-create-api-crmonline/popout-record.png).</span><span class="sxs-lookup"><span data-stu-id="9249b-220">On hello actions toolbar, click **Pop Out** ![popout record](./media/connectors-create-api-crmonline/popout-record.png).</span></span>
<span data-ttu-id="9249b-221">U kunt ook Hallo acties op de werkbalk toocopy Hallo volledige URL in het standaard e-mailprogramma **e-MAILBERICHT een koppeling**.</span><span class="sxs-lookup"><span data-stu-id="9249b-221">Alternatively, on hello actions toolbar, toocopy hello full URL into your default email program, click **EMAIL A LINK**.</span></span>

   <span data-ttu-id="9249b-222">Hallo record-ID wordt weergegeven tussen Hallo 7 ter en %7 %d tekens van Hallo URL-codering.</span><span class="sxs-lookup"><span data-stu-id="9249b-222">hello record ID is displayed in between hello %7b and %7d encoding characters of hello URL.</span></span>

   ![Stroom recordId en het type account](./media/connectors-create-api-crmonline/recordid.png)

## <a name="troubleshooting"></a><span data-ttu-id="9249b-224">Problemen oplossen</span><span class="sxs-lookup"><span data-stu-id="9249b-224">Troubleshooting</span></span>
<span data-ttu-id="9249b-225">een mislukte stap in een logische app, weergave Hallo Statusdetails van Hallo gebeurtenis tootroubleshoot.</span><span class="sxs-lookup"><span data-stu-id="9249b-225">tootroubleshoot a failed step in a logic app, view hello status details of hello event.</span></span>

1. <span data-ttu-id="9249b-226">Onder **Logic Apps**, selecteer uw logische app en klik vervolgens op **overzicht**.</span><span class="sxs-lookup"><span data-stu-id="9249b-226">Under **Logic Apps**, select your logic app, and then click **Overview**.</span></span> 

   <span data-ttu-id="9249b-227">Hallo samenvattingsgebied wordt weergegeven en bevat Hallo uitvoeren status voor Hallo logische app.</span><span class="sxs-lookup"><span data-stu-id="9249b-227">hello Summary area is shown and provides hello run status for hello logic app.</span></span> 

   ![Logische app uitvoeringsstatus](./media/connectors-create-api-crmonline/tshoot1.png)

2. <span data-ttu-id="9249b-229">tooview meer informatie over eventuele mislukte wordt uitgevoerd, klikt u op Hallo kan gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="9249b-229">tooview more information about any failed runs, click hello failed event.</span></span> <span data-ttu-id="9249b-230">een mislukte stap tooexpand klikt u op die stap.</span><span class="sxs-lookup"><span data-stu-id="9249b-230">tooexpand a failed step, click that step.</span></span>

   ![Vouw de mislukte stap](./media/connectors-create-api-crmonline/tshoot2.png)

   <span data-ttu-id="9249b-232">Hallo Stapgegevens worden weergegeven en Hallo oorzaak van Hallo probleem kunnen oplossen.</span><span class="sxs-lookup"><span data-stu-id="9249b-232">hello step details appear and can help troubleshoot hello cause of hello failure.</span></span>

   ![Details van de stap is mislukt](./media/connectors-create-api-crmonline/tshoot3.png)

<span data-ttu-id="9249b-234">Zie voor meer informatie over het oplossen van logische apps [logic app fouten opsporen](../logic-apps/logic-apps-diagnosing-failures.md).</span><span class="sxs-lookup"><span data-stu-id="9249b-234">For more information about troubleshooting logic apps, see [Diagnosing logic app failures](../logic-apps/logic-apps-diagnosing-failures.md).</span></span>

## <a name="connector-specific-details"></a><span data-ttu-id="9249b-235">Connector-specifieke details</span><span class="sxs-lookup"><span data-stu-id="9249b-235">Connector-specific details</span></span>

<span data-ttu-id="9249b-236">Alle triggers en acties die zijn gedefinieerd in swagger Hallo bekijken en ook bekijken in Hallo beperkingen [connector details](/connectors/crm/).</span><span class="sxs-lookup"><span data-stu-id="9249b-236">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/crm/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="9249b-237">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="9249b-237">Next steps</span></span>
<span data-ttu-id="9249b-238">Verken Hallo van andere beschikbare connectors in Logic Apps op onze [API's lijst](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="9249b-238">Explore hello other available connectors in Logic Apps at our [APIs list](apis-list.md).</span></span>

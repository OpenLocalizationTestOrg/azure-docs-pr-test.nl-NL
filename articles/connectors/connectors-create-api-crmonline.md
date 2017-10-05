---
title: Verbinding maken met Dynamics 365 (online) van Azure Logic Apps | Microsoft Docs
description: Logic app werkstromen maken die Dynamics 365 (online) entiteiten via de API die door de connector Dynamics 365 beheren
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
ms.openlocfilehash: d35647921ff540167a3a591fb489d3bab031a5c1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="connect-to-dynamics-365-from-logic-app-workflows"></a><span data-ttu-id="eee8d-103">Verbinding maken met Dynamics 365 vanuit logic app-werkstromen</span><span class="sxs-lookup"><span data-stu-id="eee8d-103">Connect to Dynamics 365 from logic app workflows</span></span>

<span data-ttu-id="eee8d-104">Met Logic Apps kunt u verbinding met Dynamics 365 (online) en nuttig business stromen die records maken, bijwerken items of retourneren een lijst met records maken.</span><span class="sxs-lookup"><span data-stu-id="eee8d-104">With Logic Apps, you can connect to Dynamics 365 (online) and create useful business flows that create records, update items, or return a list of records.</span></span> <span data-ttu-id="eee8d-105">Met de connector Dynamics 365 kunt u:</span><span class="sxs-lookup"><span data-stu-id="eee8d-105">With the Dynamics 365 connector, you can:</span></span>

* <span data-ttu-id="eee8d-106">Bouw uw zakelijke flow op basis van de gegevens die u vanuit Dynamics 365 (online).</span><span class="sxs-lookup"><span data-stu-id="eee8d-106">Build your business flow based on the data you get from Dynamics 365 (online).</span></span>
* <span data-ttu-id="eee8d-107">Gebruik de acties die reageert en vervolgens de uitvoer beschikbaar voor andere acties.</span><span class="sxs-lookup"><span data-stu-id="eee8d-107">Use actions that get a response and then make the output available for other actions.</span></span> <span data-ttu-id="eee8d-108">Wanneer een item wordt bijgewerkt in Dynamics 365 (online), kunt u bijvoorbeeld een e-mailbericht met Office 365 verzenden.</span><span class="sxs-lookup"><span data-stu-id="eee8d-108">For example, when an item is updated in Dynamics 365 (online), you can send an email using Office 365.</span></span>

<span data-ttu-id="eee8d-109">Dit onderwerp leest u het maken van een logische app die u een taak in Dynamics 365 maakt zodra er een nieuwe lead in Dynamics 365 is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="eee8d-109">This topic shows you how to create a logic app that creates a task in Dynamics 365 whenever a new lead is created in Dynamics 365.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="eee8d-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="eee8d-110">Prerequisites</span></span>
* <span data-ttu-id="eee8d-111">Een Azure-account.</span><span class="sxs-lookup"><span data-stu-id="eee8d-111">An Azure account.</span></span>
* <span data-ttu-id="eee8d-112">Een account met Dynamics 365 (online).</span><span class="sxs-lookup"><span data-stu-id="eee8d-112">A Dynamics 365 (online) account.</span></span>

## <a name="create-a-task-when-a-new-lead-is-created-in-dynamics-365"></a><span data-ttu-id="eee8d-113">Een taak wordt gemaakt wanneer een nieuwe lead in Dynamics 365 wordt gemaakt</span><span class="sxs-lookup"><span data-stu-id="eee8d-113">Create a task when a new lead is created in Dynamics 365</span></span>

1.  <span data-ttu-id="eee8d-114">[Aanmelden bij Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="eee8d-114">[Sign in to Azure](https://portal.azure.com).</span></span>

2.  <span data-ttu-id="eee8d-115">Typ in het Azure search `Logic apps`, en druk op ENTER.</span><span class="sxs-lookup"><span data-stu-id="eee8d-115">In the Azure search box, type `Logic apps`, and press ENTER.</span></span>

      ![Logische Apps zoeken](./media/connectors-create-api-crmonline/find-logic-apps.png)

3.  <span data-ttu-id="eee8d-117">Onder **Logic apps**, klikt u op **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="eee8d-117">Under **Logic apps**, click **Add**.</span></span>

      ![LogicApp toevoegen](./media/connectors-create-api-crmonline/add-logic-app.png)

4.  <span data-ttu-id="eee8d-119">Voor het maken van de logische app, voer de **naam**, **abonnement**, **resourcegroep**, en **locatie** velden en klik vervolgens op **Maken**.</span><span class="sxs-lookup"><span data-stu-id="eee8d-119">To create the logic app, complete the **Name**, **Subscription**, **Resource Group**, and **Location** fields, and then click **Create**.</span></span>

5.  <span data-ttu-id="eee8d-120">Selecteer de nieuwe logische app.</span><span class="sxs-lookup"><span data-stu-id="eee8d-120">Select the new logic app.</span></span> <span data-ttu-id="eee8d-121">Wanneer u ontvangt de **implementatie is voltooid** melding, klikt u op **vernieuwen**.</span><span class="sxs-lookup"><span data-stu-id="eee8d-121">When you receive the **Deployment Succeeded** notification, click **Refresh**.</span></span>

6.  <span data-ttu-id="eee8d-122">Onder **ontwikkelingsprogramma's**, klikt u op **Logic App-ontwerper**.</span><span class="sxs-lookup"><span data-stu-id="eee8d-122">Under **Development Tools**, click **Logic App Designer**.</span></span> <span data-ttu-id="eee8d-123">Klik in de lijst met sjablonen op **lege logische App**.</span><span class="sxs-lookup"><span data-stu-id="eee8d-123">In the template list, click **Blank Logic App**.</span></span>

7.  <span data-ttu-id="eee8d-124">Typ in het zoekvak `Dynamics 365`.</span><span class="sxs-lookup"><span data-stu-id="eee8d-124">In the search box, type `Dynamics 365`.</span></span> <span data-ttu-id="eee8d-125">Selecteer in de lijst van de triggers Dynamics 365 **Dynamics 365 – wanneer een record gemaakt**.</span><span class="sxs-lookup"><span data-stu-id="eee8d-125">From the Dynamics 365 triggers list, select **Dynamics 365 – When a record is created**.</span></span>

8.  <span data-ttu-id="eee8d-126">Als u wordt gevraagd aan te melden bij Dynamics 365, moet u dit nu doen.</span><span class="sxs-lookup"><span data-stu-id="eee8d-126">If you are prompted to sign in to Dynamics 365, do so now.</span></span>

9.  <span data-ttu-id="eee8d-127">Voer de volgende gegevens in de trigger-details:</span><span class="sxs-lookup"><span data-stu-id="eee8d-127">In the trigger details, enter the following information:</span></span>

  * <span data-ttu-id="eee8d-128">**Naam van de organisatie**.</span><span class="sxs-lookup"><span data-stu-id="eee8d-128">**Organization Name**.</span></span> <span data-ttu-id="eee8d-129">Selecteer het Dynamics 365-exemplaar dat u wilt dat de logische app om te luisteren.</span><span class="sxs-lookup"><span data-stu-id="eee8d-129">Select the Dynamics 365 instance that you want the logic app to listen to.</span></span>

  * <span data-ttu-id="eee8d-130">**Naam van de entiteit**.</span><span class="sxs-lookup"><span data-stu-id="eee8d-130">**Entity Name**.</span></span> <span data-ttu-id="eee8d-131">Selecteer de entiteit die u wilt luisteren.</span><span class="sxs-lookup"><span data-stu-id="eee8d-131">Select the entity that you want to listen to.</span></span> <span data-ttu-id="eee8d-132">Deze gebeurtenis fungeert als een trigger voor het starten van de logische app.</span><span class="sxs-lookup"><span data-stu-id="eee8d-132">This event acts as a trigger to start the logic app.</span></span> 
  <span data-ttu-id="eee8d-133">In dit overzicht **leidt** is geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="eee8d-133">In this walkthrough, **Leads** is selected.</span></span>

  * <span data-ttu-id="eee8d-134">**Hoe vaak wilt u om te controleren op items?**</span><span class="sxs-lookup"><span data-stu-id="eee8d-134">**How often do you want to check for items?**</span></span> <span data-ttu-id="eee8d-135">Deze waarden instellen hoe vaak de logische app controleert op updates met betrekking tot de trigger.</span><span class="sxs-lookup"><span data-stu-id="eee8d-135">These values set how often the logic app checks for updates related to the trigger.</span></span> <span data-ttu-id="eee8d-136">De standaardinstelling is om te controleren op updates elke drie minuten.</span><span class="sxs-lookup"><span data-stu-id="eee8d-136">The default setting is to check for updates every three minutes.</span></span>

    * <span data-ttu-id="eee8d-137">**Frequentie**.</span><span class="sxs-lookup"><span data-stu-id="eee8d-137">**Frequency**.</span></span> <span data-ttu-id="eee8d-138">Selecteer seconden, minuten, uren of dagen.</span><span class="sxs-lookup"><span data-stu-id="eee8d-138">Select seconds, minutes, hours, or days.</span></span>

    * <span data-ttu-id="eee8d-139">**Interval**.</span><span class="sxs-lookup"><span data-stu-id="eee8d-139">**Interval**.</span></span> <span data-ttu-id="eee8d-140">Voer het aantal seconden, minuten, uren of dagen dat u wilt laten verstrijken voordat de controle van de volgende.</span><span class="sxs-lookup"><span data-stu-id="eee8d-140">Enter the number of seconds, minutes, hours, or days that you want to pass before the next check.</span></span>

      ![Details van de logica voor App Trigger](./media/connectors-create-api-crmonline/trigger-details.png)

10. <span data-ttu-id="eee8d-142">Klik op **nieuwe stap**, en klik vervolgens op **een actie toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="eee8d-142">Click **New step**, and then click **Add an action**.</span></span>

11. <span data-ttu-id="eee8d-143">Typ in het zoekvak `Dynamics 365`.</span><span class="sxs-lookup"><span data-stu-id="eee8d-143">In the search box, type `Dynamics 365`.</span></span> <span data-ttu-id="eee8d-144">Selecteer in de lijst met acties **Dynamics 365 – Maak een nieuwe record**.</span><span class="sxs-lookup"><span data-stu-id="eee8d-144">From the actions list, select **Dynamics 365 – Create a new record**.</span></span>

12. <span data-ttu-id="eee8d-145">Voer de volgende informatie in:</span><span class="sxs-lookup"><span data-stu-id="eee8d-145">Enter the following information:</span></span>

    * <span data-ttu-id="eee8d-146">**Naam van de organisatie**.</span><span class="sxs-lookup"><span data-stu-id="eee8d-146">**Organization Name**.</span></span> <span data-ttu-id="eee8d-147">Selecteer de Dynamics 365 instantie waar u de stroom om de record te maken.</span><span class="sxs-lookup"><span data-stu-id="eee8d-147">Select the Dynamics 365 instance where you want the flow to create the record.</span></span> 
    <span data-ttu-id="eee8d-148">Merk op dat dit exemplaar hoeft te zijn van hetzelfde exemplaar waar de gebeurtenis wordt geactiveerd vanuit.</span><span class="sxs-lookup"><span data-stu-id="eee8d-148">Notice that this instance doesn’t have to be the same instance where the event is triggered from.</span></span>

    * <span data-ttu-id="eee8d-149">**Naam van de entiteit**.</span><span class="sxs-lookup"><span data-stu-id="eee8d-149">**Entity Name**.</span></span> <span data-ttu-id="eee8d-150">Selecteer de entiteit die u een record maken wilt als de gebeurtenis wordt geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="eee8d-150">Select the entity that you want to create a record when the event is triggered.</span></span> 
    <span data-ttu-id="eee8d-151">In dit overzicht **taken** is geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="eee8d-151">In this walkthrough, **Tasks** is selected.</span></span>

13. <span data-ttu-id="eee8d-152">Klik in de **onderwerp** vak dat wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="eee8d-152">Click in the **Subject** box that appears.</span></span> <span data-ttu-id="eee8d-153">In de dynamische inhoud lijst die wordt weergegeven, kunt u een van deze velden selecteren:</span><span class="sxs-lookup"><span data-stu-id="eee8d-153">From the dynamic content list that appears, you can select either of these fields:</span></span>

    * <span data-ttu-id="eee8d-154">**Achternaam**.</span><span class="sxs-lookup"><span data-stu-id="eee8d-154">**Last Name**.</span></span> <span data-ttu-id="eee8d-155">Voegt de achternaam van de lead als u dit veld in het veld onderwerp voor de taak in wanneer de taak wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="eee8d-155">Selecting this field inserts the last name for the lead into the Subject field for the task, when the task record is created.</span></span>
    * <span data-ttu-id="eee8d-156">**Onderwerp**.</span><span class="sxs-lookup"><span data-stu-id="eee8d-156">**Topic**.</span></span> <span data-ttu-id="eee8d-157">Als u dit veld voegt in het veld onderwerp voor de lead in het veld onderwerp voor de taak wanneer de taak wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="eee8d-157">Selecting this field inserts the Topic field for the lead into the Subject field for the task, when the task record is created.</span></span> 
    <span data-ttu-id="eee8d-158">Klik op **onderwerp** om toe te voegen die u wilt de **onderwerp** vak.</span><span class="sxs-lookup"><span data-stu-id="eee8d-158">Click **Topic** to add that to the **Subject** box.</span></span>

      ![Logische App maken nieuwe records details](./media/connectors-create-api-crmonline/create-record-details.png)

14. <span data-ttu-id="eee8d-160">Klik op de werkbalk Logic App-ontwerper **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="eee8d-160">On the Logic App Designer toolbar, click **Save**.</span></span>

    ![Logic App-ontwerper werkbalk opslaan](./media/connectors-create-api-crmonline/designer-toolbar-save.png)

15. <span data-ttu-id="eee8d-162">Voor het starten van de logische App, klikt u op **uitvoeren**.</span><span class="sxs-lookup"><span data-stu-id="eee8d-162">To start the Logic App, click **Run**.</span></span>

    ![Logic App-ontwerper werkbalk opslaan](./media/connectors-create-api-crmonline/designer-toolbar-run.png)

16. <span data-ttu-id="eee8d-164">Nu een leadrecord maken in Dynamics 365 voor verkoop en uw flow in actie zien!</span><span class="sxs-lookup"><span data-stu-id="eee8d-164">Now create a lead record in Dynamics 365 for Sales and see your flow in action!</span></span>

## <a name="set-advanced-options-for-a-logic-app-step"></a><span data-ttu-id="eee8d-165">Geavanceerde opties voor de stap van een logische app instellen</span><span class="sxs-lookup"><span data-stu-id="eee8d-165">Set advanced options for a logic app step</span></span>

<span data-ttu-id="eee8d-166">Als u wilt filteren van gegevens in een logische app stap opgeven, klikt u op **geavanceerde opties weergeven** in deze stap voegt u een filter of de volgorde door query.</span><span class="sxs-lookup"><span data-stu-id="eee8d-166">To specify how to filter data in a logic app step, click **Show advanced options** in that step, then add a filter or order by query.</span></span>

<span data-ttu-id="eee8d-167">Bijvoorbeeld, kunt u een filterquery alleen actieve accounts en volgorde ophalen door de accountnaam.</span><span class="sxs-lookup"><span data-stu-id="eee8d-167">For example, you can use a filter query to get only active accounts and order by the account name.</span></span> <span data-ttu-id="eee8d-168">Als u wilt uitvoeren van deze taak voert u de OData-filter-query `statuscode eq 1`, en selecteer **accountnaam** uit de lijst met dynamische inhoud.</span><span class="sxs-lookup"><span data-stu-id="eee8d-168">To perform this task, enter the OData filter query `statuscode eq 1`, and select **Account Name** from the dynamic content list.</span></span> <span data-ttu-id="eee8d-169">Meer informatie: [MSDN: $filter](https://msdn.microsoft.com/library/gg309461.aspx#Anchor_1) en [$orderby](https://msdn.microsoft.com/library/gg309461.aspx#Anchor_2).</span><span class="sxs-lookup"><span data-stu-id="eee8d-169">More information: [MSDN: $filter](https://msdn.microsoft.com/library/gg309461.aspx#Anchor_1) and [$orderby](https://msdn.microsoft.com/library/gg309461.aspx#Anchor_2).</span></span>

![Geavanceerde opties voor logische-app](./media/connectors-create-api-crmonline/advanced-options.png)

### <a name="best-practices-when-using-advanced-options"></a><span data-ttu-id="eee8d-171">Aanbevolen procedures voor het gebruik van geavanceerde opties</span><span class="sxs-lookup"><span data-stu-id="eee8d-171">Best practices when using advanced options</span></span>

<span data-ttu-id="eee8d-172">Wanneer u een waarde aan een veld toevoegt, moet u het veldtype overeenkomen met of u typt u een waarde of Selecteer een waarde in de lijst met dynamische inhoud.</span><span class="sxs-lookup"><span data-stu-id="eee8d-172">When you add a value to a field, you must match the field type whether you type a value or select a value from the dynamic content list.</span></span>

<span data-ttu-id="eee8d-173">Veldtype</span><span class="sxs-lookup"><span data-stu-id="eee8d-173">Field type</span></span>  |<span data-ttu-id="eee8d-174">Gebruiksinstructies</span><span class="sxs-lookup"><span data-stu-id="eee8d-174">How to use</span></span>  |<span data-ttu-id="eee8d-175">Waar vind ik</span><span class="sxs-lookup"><span data-stu-id="eee8d-175">Where to find</span></span>  |<span data-ttu-id="eee8d-176">Naam</span><span class="sxs-lookup"><span data-stu-id="eee8d-176">Name</span></span>  |<span data-ttu-id="eee8d-177">Gegevenstype</span><span class="sxs-lookup"><span data-stu-id="eee8d-177">Data type</span></span>  
---------|---------|---------|---------|---------
<span data-ttu-id="eee8d-178">Tekstvelden</span><span class="sxs-lookup"><span data-stu-id="eee8d-178">Text fields</span></span>|<span data-ttu-id="eee8d-179">Tekstvelden vereisen een enkele regel tekst of dynamische inhoud die is een type tekstveld.</span><span class="sxs-lookup"><span data-stu-id="eee8d-179">Text fields require a single line of text or dynamic content that is a text type field.</span></span> <span data-ttu-id="eee8d-180">Voorbeelden hiervan zijn de categorie en subcategorie velden.</span><span class="sxs-lookup"><span data-stu-id="eee8d-180">Examples include the Category and Sub-Category fields.</span></span>|<span data-ttu-id="eee8d-181">Instellingen > Aanpassingen > past u het systeem > entiteiten > taak > velden</span><span class="sxs-lookup"><span data-stu-id="eee8d-181">Settings > Customizations > Customize the System > Entities > Task > Fields</span></span> |<span data-ttu-id="eee8d-182">category</span><span class="sxs-lookup"><span data-stu-id="eee8d-182">category</span></span> |<span data-ttu-id="eee8d-183">Enkele regel tekst</span><span class="sxs-lookup"><span data-stu-id="eee8d-183">Single Line of Text</span></span>        
<span data-ttu-id="eee8d-184">Velden geheel getal</span><span class="sxs-lookup"><span data-stu-id="eee8d-184">Integer fields</span></span> | <span data-ttu-id="eee8d-185">Sommige velden vereist geheel getal of dynamische inhoud die een veld van het type geheel getal is.</span><span class="sxs-lookup"><span data-stu-id="eee8d-185">Some fields require integer or dynamic content that is an integer type field.</span></span> <span data-ttu-id="eee8d-186">Voorbeelden zijn percentage voltooid en duur.</span><span class="sxs-lookup"><span data-stu-id="eee8d-186">Examples include Percent Complete and Duration.</span></span> |<span data-ttu-id="eee8d-187">Instellingen > Aanpassingen > past u het systeem > entiteiten > taak > velden</span><span class="sxs-lookup"><span data-stu-id="eee8d-187">Settings > Customizations > Customize the System > Entities > Task > Fields</span></span> |<span data-ttu-id="eee8d-188">PercentComplete</span><span class="sxs-lookup"><span data-stu-id="eee8d-188">percentcomplete</span></span> |<span data-ttu-id="eee8d-189">Geheel getal</span><span class="sxs-lookup"><span data-stu-id="eee8d-189">Whole Number</span></span>         
<span data-ttu-id="eee8d-190">Datumvelden</span><span class="sxs-lookup"><span data-stu-id="eee8d-190">Date fields</span></span> | <span data-ttu-id="eee8d-191">Sommige velden vereisen een datum is opgegeven in de notatie dd-mm-jjjj of dynamische inhoud die is een veld van het type datum.</span><span class="sxs-lookup"><span data-stu-id="eee8d-191">Some fields require a date entered in mm/dd/yyyy format or dynamic content that is a date type field.</span></span> <span data-ttu-id="eee8d-192">Voorbeelden zijn gemaakt op, begindatum, werkelijke begindatum laatste op de tijd houdt, Werkelijk einde en vervaldatum.</span><span class="sxs-lookup"><span data-stu-id="eee8d-192">Examples include Created On, Start Date, Actual Start, Last on Hold Time, Actual End, and Due Date.</span></span> | <span data-ttu-id="eee8d-193">Instellingen > Aanpassingen > past u het systeem > entiteiten > taak > velden</span><span class="sxs-lookup"><span data-stu-id="eee8d-193">Settings > Customizations > Customize the System > Entities > Task > Fields</span></span> |<span data-ttu-id="eee8d-194">createdon</span><span class="sxs-lookup"><span data-stu-id="eee8d-194">createdon</span></span> |<span data-ttu-id="eee8d-195">Datum en tijd</span><span class="sxs-lookup"><span data-stu-id="eee8d-195">Date and Time</span></span>
<span data-ttu-id="eee8d-196">Typ velden waarvoor zowel een record-ID en lookup</span><span class="sxs-lookup"><span data-stu-id="eee8d-196">Fields that require both a record ID and lookup type</span></span> |<span data-ttu-id="eee8d-197">Sommige velden die verwijzen naar een andere entiteitsrecord vereisen zowel de record-ID en het Opzoektype.</span><span class="sxs-lookup"><span data-stu-id="eee8d-197">Some fields that reference another entity record require both the record ID and the lookup type.</span></span> |<span data-ttu-id="eee8d-198">Instellingen > Aanpassingen > past u het systeem > entiteiten > Account > velden</span><span class="sxs-lookup"><span data-stu-id="eee8d-198">Settings > Customizations > Customize the System > Entities > Account > Fields</span></span>  | <span data-ttu-id="eee8d-199">AccountId</span><span class="sxs-lookup"><span data-stu-id="eee8d-199">accountid</span></span>  | <span data-ttu-id="eee8d-200">Primaire sleutel</span><span class="sxs-lookup"><span data-stu-id="eee8d-200">Primary Key</span></span>

### <a name="more-examples-of-fields-that-require-both-a-record-id-and-lookup-type"></a><span data-ttu-id="eee8d-201">Typ voor meer voorbeelden van de velden die vereisen een record-ID en de lookup dat</span><span class="sxs-lookup"><span data-stu-id="eee8d-201">More examples of fields that require both a record ID and lookup type</span></span>
<span data-ttu-id="eee8d-202">Voortbouwend op de vorige tabel, vindt hier u meer voorbeelden van de velden die niet met waarden die in de lijst met dynamische inhoud geselecteerd werken.</span><span class="sxs-lookup"><span data-stu-id="eee8d-202">Expanding on the previous table, here are more examples of fields that don't work with values selected from the dynamic content list.</span></span> <span data-ttu-id="eee8d-203">Deze velden vereisen in plaats daarvan beide een lookup-ID en het recordtype in de velden in PowerApps ingevoerd.</span><span class="sxs-lookup"><span data-stu-id="eee8d-203">Instead, these fields require both a record ID and lookup type entered into the fields in PowerApps.</span></span>  
* <span data-ttu-id="eee8d-204">Eigenaar en eigenaarstype.</span><span class="sxs-lookup"><span data-stu-id="eee8d-204">Owner and Owner Type.</span></span> <span data-ttu-id="eee8d-205">Het veld eigenaar moet een geldige gebruiker of het team record-ID.</span><span class="sxs-lookup"><span data-stu-id="eee8d-205">The Owner field must be a valid user or team record ID.</span></span> <span data-ttu-id="eee8d-206">Het Type van de eigenaar moet een **systemusers** of **teams**.</span><span class="sxs-lookup"><span data-stu-id="eee8d-206">The Owner Type must be either **systemusers** or **teams**.</span></span>
* <span data-ttu-id="eee8d-207">De klant en het klanttype.</span><span class="sxs-lookup"><span data-stu-id="eee8d-207">Customer and Customer Type.</span></span> <span data-ttu-id="eee8d-208">Het veld moet een geldig account of neem contact op met de record-ID.</span><span class="sxs-lookup"><span data-stu-id="eee8d-208">The Customer field must be a valid account or contact record ID.</span></span> <span data-ttu-id="eee8d-209">Het Type van de eigenaar moet een **accounts** of **contactpersonen**.</span><span class="sxs-lookup"><span data-stu-id="eee8d-209">The Owner Type must be either **accounts** or **contacts**.</span></span>
* <span data-ttu-id="eee8d-210">Met betrekking tot en met betrekking tot Type.</span><span class="sxs-lookup"><span data-stu-id="eee8d-210">Regarding and Regarding Type.</span></span> <span data-ttu-id="eee8d-211">Het veld betreft moet een geldige record-ID, zoals een account of neem contact op met de record-ID.</span><span class="sxs-lookup"><span data-stu-id="eee8d-211">The Regarding field must be a valid record ID, such as an account or contact record ID.</span></span> <span data-ttu-id="eee8d-212">Het Type met betrekking tot moet het type lookup voor de record, zoals **accounts** of **contactpersonen**.</span><span class="sxs-lookup"><span data-stu-id="eee8d-212">The Regarding Type must be the lookup type for the record, such as **accounts** or **contacts**.</span></span>

<span data-ttu-id="eee8d-213">Het volgende voorbeeld van taak maken actie wordt een record voor een account dat overeenkomt met de id van de record toe te voegen aan het betreffende veld van de taak.</span><span class="sxs-lookup"><span data-stu-id="eee8d-213">The following task creation action example adds an account record that corresponds to the record ID adding it to the regarding field of the task.</span></span>

![Stroom recordId en het type account](./media/connectors-create-api-crmonline/recordid-type-account.png)

<span data-ttu-id="eee8d-215">In dit voorbeeld wordt de taak ook toegewezen aan een specifieke gebruiker op basis van de gebruiker record-ID.</span><span class="sxs-lookup"><span data-stu-id="eee8d-215">This example also assigns the task to a specific user based on the user's record ID.</span></span>

![Stroom recordId en het type account](./media/connectors-create-api-crmonline/recordid-type-user.png)

<span data-ttu-id="eee8d-217">Een record-ID, Zie de volgende sectie: *vinden van de record-ID*</span><span class="sxs-lookup"><span data-stu-id="eee8d-217">To find a record's ID, see the following section: *Find the record ID*</span></span>

## <a name="find-the-record-id"></a><span data-ttu-id="eee8d-218">De record-ID vinden</span><span class="sxs-lookup"><span data-stu-id="eee8d-218">Find the record ID</span></span>

1. <span data-ttu-id="eee8d-219">Open een record bestaat, zoals een record.</span><span class="sxs-lookup"><span data-stu-id="eee8d-219">Open a record, such as an account record.</span></span>

2. <span data-ttu-id="eee8d-220">Klik op de werkbalk Acties **Pop uit** ![popout record](./media/connectors-create-api-crmonline/popout-record.png).</span><span class="sxs-lookup"><span data-stu-id="eee8d-220">On the actions toolbar, click **Pop Out** ![popout record](./media/connectors-create-api-crmonline/popout-record.png).</span></span>
<span data-ttu-id="eee8d-221">U kunt ook de acties op de werkbalk om te kopiëren van de volledige URL in het standaard e-mailprogramma, **e-MAILBERICHT een koppeling**.</span><span class="sxs-lookup"><span data-stu-id="eee8d-221">Alternatively, on the actions toolbar, to copy the full URL into your default email program, click **EMAIL A LINK**.</span></span>

   <span data-ttu-id="eee8d-222">De record-ID wordt weergegeven tussen de 7 ter en %7 %d tekens van de URL-codering.</span><span class="sxs-lookup"><span data-stu-id="eee8d-222">The record ID is displayed in between the %7b and %7d encoding characters of the URL.</span></span>

   ![Stroom recordId en het type account](./media/connectors-create-api-crmonline/recordid.png)

## <a name="troubleshooting"></a><span data-ttu-id="eee8d-224">Problemen oplossen</span><span class="sxs-lookup"><span data-stu-id="eee8d-224">Troubleshooting</span></span>
<span data-ttu-id="eee8d-225">Voor het oplossen van een mislukte stap in een logische app, moet u de statusdetails van de gebeurtenis weergeven.</span><span class="sxs-lookup"><span data-stu-id="eee8d-225">To troubleshoot a failed step in a logic app, view the status details of the event.</span></span>

1. <span data-ttu-id="eee8d-226">Onder **Logic Apps**, selecteer uw logische app en klik vervolgens op **overzicht**.</span><span class="sxs-lookup"><span data-stu-id="eee8d-226">Under **Logic Apps**, select your logic app, and then click **Overview**.</span></span> 

   <span data-ttu-id="eee8d-227">In het samenvattingsgebied wordt weergegeven en de uitvoeringsstatus biedt voor de logische app.</span><span class="sxs-lookup"><span data-stu-id="eee8d-227">The Summary area is shown and provides the run status for the logic app.</span></span> 

   ![Logische app uitvoeringsstatus](./media/connectors-create-api-crmonline/tshoot1.png)

2. <span data-ttu-id="eee8d-229">Als u meer informatie over eventuele mislukte wordt uitgevoerd, klikt u op de gebeurtenis is mislukt.</span><span class="sxs-lookup"><span data-stu-id="eee8d-229">To view more information about any failed runs, click the failed event.</span></span> <span data-ttu-id="eee8d-230">Als een mislukte stap wilt uitbreiden, klikt u op die stap.</span><span class="sxs-lookup"><span data-stu-id="eee8d-230">To expand a failed step, click that step.</span></span>

   ![Vouw de mislukte stap](./media/connectors-create-api-crmonline/tshoot2.png)

   <span data-ttu-id="eee8d-232">De details van de stap worden weergegeven en de oorzaak van het probleem kunnen oplossen.</span><span class="sxs-lookup"><span data-stu-id="eee8d-232">The step details appear and can help troubleshoot the cause of the failure.</span></span>

   ![Details van de stap is mislukt](./media/connectors-create-api-crmonline/tshoot3.png)

<span data-ttu-id="eee8d-234">Zie voor meer informatie over het oplossen van logische apps [logic app fouten opsporen](../logic-apps/logic-apps-diagnosing-failures.md).</span><span class="sxs-lookup"><span data-stu-id="eee8d-234">For more information about troubleshooting logic apps, see [Diagnosing logic app failures](../logic-apps/logic-apps-diagnosing-failures.md).</span></span>

## <a name="connector-specific-details"></a><span data-ttu-id="eee8d-235">Connector-specifieke details</span><span class="sxs-lookup"><span data-stu-id="eee8d-235">Connector-specific details</span></span>

<span data-ttu-id="eee8d-236">Alle triggers en acties die zijn gedefinieerd in de swagger bekijken en ziet u ook de beperkingen in de [connector details](/connectors/crm/).</span><span class="sxs-lookup"><span data-stu-id="eee8d-236">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/crm/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="eee8d-237">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="eee8d-237">Next steps</span></span>
<span data-ttu-id="eee8d-238">Bekijk de beschikbare connectors in Logic Apps op onze [API's lijst](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="eee8d-238">Explore the other available connectors in Logic Apps at our [APIs list](apis-list.md).</span></span>

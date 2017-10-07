---
title: aaaDisaster herstel voor B2B-integratie account - Azure Logic Apps | Microsoft Docs
description: Logic Apps B2B-noodherstel
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: 
ms.assetid: cf44af18-1fe5-41d5-9e06-cc57a968207c
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/10/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: e86564a3c5a2607d22514936c606e2843cba0416
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="logic-apps-b2b-cross-region-disaster-recovery"></a><span data-ttu-id="731fa-103">Logic Apps B2B regio-overschrijdende noodherstel</span><span class="sxs-lookup"><span data-stu-id="731fa-103">Logic Apps B2B cross-region disaster recovery</span></span>

<span data-ttu-id="731fa-104">B2B-werkbelastingen hebben betrekking op geld transacties zoals orders en facturen.</span><span class="sxs-lookup"><span data-stu-id="731fa-104">B2B workloads involve money transactions like orders and invoices.</span></span> <span data-ttu-id="731fa-105">Tijdens een gebeurtenis na noodgevallen is het essentieel voor een zakelijke tooquickly herstellen toomeet Hallo die zakelijke serviceovereenkomsten met hun partners overeengekomen.</span><span class="sxs-lookup"><span data-stu-id="731fa-105">During a disaster event, it's critical for a business tooquickly recover toomeet hello business-level SLAs agreed upon with their partners.</span></span> <span data-ttu-id="731fa-106">In dit artikel laat zien hoe een zakelijke continuïteit toobuild plannen voor B2B-werkbelastingen.</span><span class="sxs-lookup"><span data-stu-id="731fa-106">This article demonstrates how toobuild a business continuity plan for B2B workloads.</span></span> 

* <span data-ttu-id="731fa-107">Gereedheid voor herstel na noodgevallen</span><span class="sxs-lookup"><span data-stu-id="731fa-107">Disaster Recovery readiness</span></span> 
* <span data-ttu-id="731fa-108">Toosecondary regio failover tijdens een gebeurtenis na noodgevallen</span><span class="sxs-lookup"><span data-stu-id="731fa-108">Fail over toosecondary region during a disaster event</span></span> 
* <span data-ttu-id="731fa-109">Tooprimary regio terugvallen na een gebeurtenis na noodgevallen</span><span class="sxs-lookup"><span data-stu-id="731fa-109">Fall back tooprimary region after a disaster event</span></span>

## <a name="disaster-recovery-readiness"></a><span data-ttu-id="731fa-110">Gereedheid voor herstel na noodgevallen</span><span class="sxs-lookup"><span data-stu-id="731fa-110">Disaster Recovery readiness</span></span>  

1. <span data-ttu-id="731fa-111">Een secundaire regio identificeert en maakt u een [integratie account](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md) in Hallo secundaire regio.</span><span class="sxs-lookup"><span data-stu-id="731fa-111">Identify a secondary region and create an [integration account](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md) in hello secondary region.</span></span>

2. <span data-ttu-id="731fa-112">Partners, schema's en overeenkomsten voor Hallo vereist bericht stromen waarin Hallo uitvoeringsstatus toobe gerepliceerd toosecondary regio integratie account moet toevoegen.</span><span class="sxs-lookup"><span data-stu-id="731fa-112">Add partners, schemas, and agreements for hello required message flows where hello run status needs toobe replicated toosecondary region integration account.</span></span>

   > [!TIP]
   > <span data-ttu-id="731fa-113">Zorg ervoor dat er consistentie in de naamgevingsconventie Hallo integratie account artefact van tussen regio's.</span><span class="sxs-lookup"><span data-stu-id="731fa-113">Make sure there's consistency in hello integration account artifact's naming convention across regions.</span></span> 

3. <span data-ttu-id="731fa-114">toopull hello status uitvoeren vanaf de primaire regio hello, een logische app maken in de secundaire regio Hallo.</span><span class="sxs-lookup"><span data-stu-id="731fa-114">toopull hello run status from hello primary region, create a logic app in hello secondary region.</span></span> 

   <span data-ttu-id="731fa-115">Deze logische app moet een *trigger* en een *actie*.</span><span class="sxs-lookup"><span data-stu-id="731fa-115">This logic app should have a *trigger* and an *action*.</span></span> 
   <span data-ttu-id="731fa-116">Hallo trigger moet verbinding maken tooprimary regio integratie account moet, en Hallo actie toosecondary regio integratie-account.</span><span class="sxs-lookup"><span data-stu-id="731fa-116">hello trigger should connect tooprimary region integration account, and hello action should connect toosecondary region integration account.</span></span> 
   <span data-ttu-id="731fa-117">Op basis van het tijdsinterval hello, Hallo trigger Hallo primaire regio uitvoeren statustabel worden opgevraagd en haalt nieuwe records hello, indien van toepassing.</span><span class="sxs-lookup"><span data-stu-id="731fa-117">Based on hello time interval, hello trigger polls hello primary region run status table and pulls hello new records, if any.</span></span> <span data-ttu-id="731fa-118">Hallo actie werkt ze toosecondary regio integratie-account.</span><span class="sxs-lookup"><span data-stu-id="731fa-118">hello action updates them toosecondary region integration account.</span></span> 
   <span data-ttu-id="731fa-119">Dit helpt tooget incrementele runtimestatus van de primaire regio toosecondary regio.</span><span class="sxs-lookup"><span data-stu-id="731fa-119">This helps tooget incremental runtime status from primary region toosecondary region.</span></span>

4. <span data-ttu-id="731fa-120">Zakelijke continuïteit in Logic Apps integratie-account is ontworpen op basis van B2B-protocollen - X12, AS2 en EDIFACT toosupport.</span><span class="sxs-lookup"><span data-stu-id="731fa-120">Business continuity in Logic Apps integration account is designed toosupport based on B2B protocols - X12, AS2, and EDIFACT.</span></span> <span data-ttu-id="731fa-121">toofind gedetailleerde stappen, selecteer Hallo respectieve koppelingen.</span><span class="sxs-lookup"><span data-stu-id="731fa-121">toofind detailed steps, select hello respective links.</span></span>

5. <span data-ttu-id="731fa-122">Hallo aanbeveling is toodeploy alle primaire regio resources in een secundaire regio te.</span><span class="sxs-lookup"><span data-stu-id="731fa-122">hello recommendation is toodeploy all primary region resources in a secondary region too.</span></span> 

   <span data-ttu-id="731fa-123">Primaire regio resources omvatten Azure SQL Database of Azure Cosmos DB, Azure Service Bus en Azure Event Hubs gebruikt voor messaging Azure API Management en hello Azure Logic Apps-functie in Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="731fa-123">Primary region resources include Azure SQL Database or Azure Cosmos DB, Azure Service Bus and Azure Event Hubs used for messaging, Azure API Management, and hello Azure Logic Apps feature in Azure App Service.</span></span>   

6. <span data-ttu-id="731fa-124">Stel een verbinding van een primaire regio tooa secundaire regio.</span><span class="sxs-lookup"><span data-stu-id="731fa-124">Establish a connection from a primary region tooa secondary region.</span></span> <span data-ttu-id="731fa-125">toopull hello status uitvoeren vanaf een primaire regio een logische app maken in een secundaire regio.</span><span class="sxs-lookup"><span data-stu-id="731fa-125">toopull hello run status from a primary region, create a logic app in a secondary region.</span></span> 

   <span data-ttu-id="731fa-126">Hallo logische app moet een trigger en een actie hebben.</span><span class="sxs-lookup"><span data-stu-id="731fa-126">hello logic app should have a trigger and an action.</span></span> 
   <span data-ttu-id="731fa-127">Hallo trigger moet tooa primaire regio integratie-account koppelen.</span><span class="sxs-lookup"><span data-stu-id="731fa-127">hello trigger should connect tooa primary region integration account.</span></span> 
   <span data-ttu-id="731fa-128">Hallo-actie moet tooa secundaire regio integratie-account koppelen.</span><span class="sxs-lookup"><span data-stu-id="731fa-128">hello action should connect tooa secondary region integration account.</span></span> 
   <span data-ttu-id="731fa-129">Op basis van het tijdsinterval hello, Hallo trigger Hallo primaire regio uitvoeren statustabel worden opgevraagd en haalt nieuwe records hello, indien van toepassing.</span><span class="sxs-lookup"><span data-stu-id="731fa-129">Based on hello time interval, hello trigger polls hello primary region run status table and pulls hello new records, if any.</span></span> 
   <span data-ttu-id="731fa-130">Hallo actie werkt ze tooa secundaire regio integratie-account.</span><span class="sxs-lookup"><span data-stu-id="731fa-130">hello action updates them tooa secondary region integration account.</span></span> 
   <span data-ttu-id="731fa-131">Dit proces helpt tooget incrementele runtimestatus van Hallo primaire regio toohello secundaire regio.</span><span class="sxs-lookup"><span data-stu-id="731fa-131">This process helps tooget incremental runtime status from hello primary region toohello secondary region.</span></span>

<span data-ttu-id="731fa-132">Zakelijke continuïteit in Logic Apps integratie-account biedt ondersteuning op basis van Hallo B2B-protocollen X12 en AS2, EDIFACT.</span><span class="sxs-lookup"><span data-stu-id="731fa-132">Business continuity in a Logic Apps integration account provides support based on hello B2B protocols X12, AS2, and EDIFACT.</span></span> <span data-ttu-id="731fa-133">Zie voor gedetailleerde stappen voor het gebruik van X12 en AS2 [X12](../logic-apps/logic-apps-enterprise-integration-b2b-business-continuity.md#x12) en [AS2](../logic-apps/logic-apps-enterprise-integration-b2b-business-continuity.md#as2) in dit artikel.</span><span class="sxs-lookup"><span data-stu-id="731fa-133">For detailed steps on using X12 and AS2, see [X12](../logic-apps/logic-apps-enterprise-integration-b2b-business-continuity.md#x12) and [AS2](../logic-apps/logic-apps-enterprise-integration-b2b-business-continuity.md#as2) in this article.</span></span>

## <a name="fail-over-tooa-secondary-region-during-a-disaster-event"></a><span data-ttu-id="731fa-134">De secundaire regio tooa failover tijdens een gebeurtenis na noodgevallen</span><span class="sxs-lookup"><span data-stu-id="731fa-134">Fail over tooa secondary region during a disaster event</span></span>

<span data-ttu-id="731fa-135">Tijdens een gebeurtenis na noodgevallen wanneer Hallo primaire regio niet beschikbaar voor bedrijfscontinuïteit, direct verkeer toohello secundaire regio.</span><span class="sxs-lookup"><span data-stu-id="731fa-135">During a disaster event, when hello primary region is not available for business continuity, direct traffic toohello secondary region.</span></span> <span data-ttu-id="731fa-136">Een secundaire regio helpt een toorecover zakelijke functies snel toomeet hello RPO/RTO overeengekomen door partners.</span><span class="sxs-lookup"><span data-stu-id="731fa-136">A secondary region helps a business toorecover functions quickly toomeet hello RPO/RTO agreed upon by their partners.</span></span> <span data-ttu-id="731fa-137">Ook minimaliseert uit één regio tooanother regio inspanningen toofail via.</span><span class="sxs-lookup"><span data-stu-id="731fa-137">It also minimizes efforts toofail over from one region tooanother region.</span></span> 

<span data-ttu-id="731fa-138">Er is een verwachte latentie tijdens het kopiëren van besturingselement cijfers van een primaire regio tooa secundaire regio.</span><span class="sxs-lookup"><span data-stu-id="731fa-138">There is an expected latency while copying control numbers from a primary region tooa secondary region.</span></span> <span data-ttu-id="731fa-139">dubbele gegenereerde besturingselement verzenden tooavoid getallen toopartners tijdens een gebeurtenis na noodgevallen, Hallo aanbeveling tooincrement Hallo besturingselement cijfers in Hallo secundaire regio overeenkomsten met behulp van [PowerShell-cmdlets](https://blogs.msdn.microsoft.com/david_burgs_blog/2017/03/09/fresh-of-the-press-new-azure-powershell-cmdlets-for-upcoming-x12-connector-disaster-recovery).</span><span class="sxs-lookup"><span data-stu-id="731fa-139">tooavoid sending duplicate generated control numbers toopartners during a disaster event, hello recommendation is tooincrement hello control numbers in hello secondary region agreements by using [PowerShell cmdlets](https://blogs.msdn.microsoft.com/david_burgs_blog/2017/03/09/fresh-of-the-press-new-azure-powershell-cmdlets-for-upcoming-x12-connector-disaster-recovery).</span></span>

## <a name="fall-back-tooa-primary-region-post-disaster-event"></a><span data-ttu-id="731fa-140">Terugvallen tooa primaire regio na noodgevallen gebeurtenis</span><span class="sxs-lookup"><span data-stu-id="731fa-140">Fall back tooa primary region post-disaster event</span></span>

<span data-ttu-id="731fa-141">toofall back tooa primaire regio wanneer deze beschikbaar is, is als volgt te werk:</span><span class="sxs-lookup"><span data-stu-id="731fa-141">toofall back tooa primary region when it is available, follow these steps:</span></span>

1. <span data-ttu-id="731fa-142">Stop de berichten van partners in Hallo secundaire regio worden geaccepteerd.</span><span class="sxs-lookup"><span data-stu-id="731fa-142">Stop accepting messages from partners in hello secondary region.</span></span>  

2. <span data-ttu-id="731fa-143">Hallo gegenereerd besturingselement cijfers voor alle Hallo primaire regio overeenkomsten verhogen met behulp van [PowerShell-cmdlets](https://blogs.msdn.microsoft.com/david_burgs_blog/2017/03/09/fresh-of-the-press-new-azure-powershell-cmdlets-for-upcoming-x12-connector-disaster-recovery).</span><span class="sxs-lookup"><span data-stu-id="731fa-143">Increment hello generated control numbers for all hello primary region agreements by using [PowerShell cmdlets](https://blogs.msdn.microsoft.com/david_burgs_blog/2017/03/09/fresh-of-the-press-new-azure-powershell-cmdlets-for-upcoming-x12-connector-disaster-recovery).</span></span>  

3. <span data-ttu-id="731fa-144">Directe verkeer van Hallo secundaire regio toohello primaire regio.</span><span class="sxs-lookup"><span data-stu-id="731fa-144">Direct traffic from hello secondary region toohello primary region.</span></span>

4. <span data-ttu-id="731fa-145">Controleer dat Hallo logische app gemaakt in de secundaire regio Hallo voor het ophalen van de status van uitvoeren vanaf de primaire regio Hallo is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="731fa-145">Check that hello logic app created in hello secondary region for pulling run status from hello primary region is enabled.</span></span>

## <a name="x12"></a><span data-ttu-id="731fa-146">X12</span><span class="sxs-lookup"><span data-stu-id="731fa-146">X12</span></span> 

<span data-ttu-id="731fa-147">Zakelijke continuïteit voor EDI X 12 documenten is gebaseerd op het besturingselement getallen:</span><span class="sxs-lookup"><span data-stu-id="731fa-147">Business continuity for EDI X12 documents is based on control numbers:</span></span>

> [!TIP]
> <span data-ttu-id="731fa-148">U kunt ook Hallo [X12 snel starten sjabloon](https://azure.microsoft.com/documentation/templates/201-logic-app-x12-disaster-recovery-replication/) toocreate logic apps.</span><span class="sxs-lookup"><span data-stu-id="731fa-148">You can also use hello [X12 quick start template](https://azure.microsoft.com/documentation/templates/201-logic-app-x12-disaster-recovery-replication/) toocreate logic apps.</span></span> <span data-ttu-id="731fa-149">Maken primaire en secundaire integratieaccounts zijn vereisten toouse Hallo sjabloon.</span><span class="sxs-lookup"><span data-stu-id="731fa-149">Creating primary and secondary integration accounts are prerequisites toouse hello template.</span></span> <span data-ttu-id="731fa-150">Hallo helpt sjabloon toocreate twee logic apps, één voor ontvangen besturingselement getallen en één voor de gegenereerde besturingselement cijfers.</span><span class="sxs-lookup"><span data-stu-id="731fa-150">hello template helps toocreate two logic apps, one for received control numbers and another for generated control numbers.</span></span> <span data-ttu-id="731fa-151">Respectieve triggers en acties worden in Hallo logic apps, Hallo trigger toohello primaire integratie account en toohello Hallo-secundaire integratie actieaccount verbinding gemaakt.</span><span class="sxs-lookup"><span data-stu-id="731fa-151">Respective triggers and actions are created in hello logic apps, connecting hello trigger toohello primary integration account and hello action toohello secondary integration account.</span></span>

<span data-ttu-id="731fa-152">**Vereisten**</span><span class="sxs-lookup"><span data-stu-id="731fa-152">**Prerequisites**</span></span>

<span data-ttu-id="731fa-153">tooenable noodherstel voor inkomende berichten Selecteer Hallo dubbele controle-instellingen in instellingen voor het ontvangen van Hallo X12-overeenkomst.</span><span class="sxs-lookup"><span data-stu-id="731fa-153">tooenable disaster recovery for inbound messages, select hello duplicate check settings in hello X12 agreement's Receive Settings.</span></span>

![Instellingen voor controle op dubbele items selecteren](./media/logic-apps-enterprise-integration-b2b-business-continuity/dupcheck.png)  

1. <span data-ttu-id="731fa-155">Maak een [logische app](../logic-apps/logic-apps-create-a-logic-app.md) in een secundaire regio.</span><span class="sxs-lookup"><span data-stu-id="731fa-155">Create a [logic app](../logic-apps/logic-apps-create-a-logic-app.md) in a secondary region.</span></span>    

2. <span data-ttu-id="731fa-156">Zoeken op **X12**, en selecteer **X12-als een getal van het besturingselement wordt gewijzigd**.</span><span class="sxs-lookup"><span data-stu-id="731fa-156">Search on **X12**, and select **X12 - When a control number is modified**.</span></span>   

   ![Zoeken naar X12](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn1.png)

   <span data-ttu-id="731fa-158">Hallo trigger vraagt u een account voor verbinding tooan integratie tooestablish.</span><span class="sxs-lookup"><span data-stu-id="731fa-158">hello trigger prompts you tooestablish a connection tooan integration account.</span></span> 
   <span data-ttu-id="731fa-159">Hallo trigger moet worden verbonden tooa primaire regio integratie-account.</span><span class="sxs-lookup"><span data-stu-id="731fa-159">hello trigger should be connected tooa primary region integration account.</span></span>

3. <span data-ttu-id="731fa-160">Geef de verbindingsnaam van een, selecteer uw *primaire regio integratie account* van Hallo lijst en kies **maken**.</span><span class="sxs-lookup"><span data-stu-id="731fa-160">Enter a connection name, select your *primary region integration account* from hello list, and choose **Create**.</span></span>   

   ![Primaire regio integratie-accountnaam](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn2.png)

4. <span data-ttu-id="731fa-162">Hallo **DateTime toostart besturingselement nummer sync** instelling is optioneel.</span><span class="sxs-lookup"><span data-stu-id="731fa-162">hello **DateTime toostart control number sync** setting is optional.</span></span> <span data-ttu-id="731fa-163">Hallo **frequentie** te kunnen worden ingesteld**dag**, **uur**, **minuut**, of **tweede** met een interval.</span><span class="sxs-lookup"><span data-stu-id="731fa-163">hello **Frequency** can be set too**Day**, **Hour**, **Minute**, or **Second** with an interval.</span></span>   

   ![Datum/tijd- en frequentie](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn3.png)

5. <span data-ttu-id="731fa-165">Selecteer **nieuwe stap** > **een actie toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="731fa-165">Select **New step** > **Add an action**.</span></span>

   ![Nieuwe stap, een actie toevoegen](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn4.png)

6. <span data-ttu-id="731fa-167">Zoeken op **X12**, en selecteer **X12-toevoegen of bijwerken van besturingselement cijfers**.</span><span class="sxs-lookup"><span data-stu-id="731fa-167">Search on **X12**, and select **X12 - Add or update control numbers**.</span></span>   

   ![Toevoegen of bijwerken van besturingselement cijfers](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn5.png)

7. <span data-ttu-id="731fa-169">tooconnect tooa secundaire regio integratie actieaccount, selecteer **verbinding wijzigen** > **nieuwe verbinding toevoegen** voor een lijst met beschikbare Hallo-integratieaccounts.</span><span class="sxs-lookup"><span data-stu-id="731fa-169">tooconnect an action tooa secondary region integration account, select **Change connection** > **Add new connection** for a list of hello available integration accounts.</span></span> <span data-ttu-id="731fa-170">Geef de verbindingsnaam van een, selecteer uw *secundaire regio integratie account* van Hallo lijst en kies **maken**.</span><span class="sxs-lookup"><span data-stu-id="731fa-170">Enter a connection name, select your *secondary region integration account* from hello list, and choose **Create**.</span></span> 

   ![Secundaire regio integratie-accountnaam](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn6.png)

8. <span data-ttu-id="731fa-172">Tooraw invoer switch door te klikken op Hallo-pictogram in de rechterbovenhoek.</span><span class="sxs-lookup"><span data-stu-id="731fa-172">Switch tooraw inputs by clicking on hello icon in upper right corner.</span></span>

   ![Switch tooraw invoer](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12rawinputs.png)

9. <span data-ttu-id="731fa-174">Selecteer hoofdtekst van dynamische inhoud objectkiezer Hallo en Hallo logic app wordt opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="731fa-174">Select Body from hello dynamic content picker, and save hello logic app.</span></span>

   ![Dynamische inhoud velden](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn7.png)

   <span data-ttu-id="731fa-176">Op basis van het tijdsinterval hello, Hallo trigger Hallo primaire regio ontvangen besturingselement nummer tabel worden opgevraagd en haalt Hallo nieuwe records.</span><span class="sxs-lookup"><span data-stu-id="731fa-176">Based on hello time interval, hello trigger polls hello primary region received control number table and pulls hello new records.</span></span> 
   <span data-ttu-id="731fa-177">Hallo actie werkt Hallo records in Hallo secundaire regio integratie-account.</span><span class="sxs-lookup"><span data-stu-id="731fa-177">hello action updates hello records in hello secondary region integration account.</span></span> 
   <span data-ttu-id="731fa-178">Als er geen updates zijn, Hallo trigger status weergegeven als **overgeslagen**.</span><span class="sxs-lookup"><span data-stu-id="731fa-178">If there are no updates, hello trigger status appears as **Skipped**.</span></span>   

   ![Besturingselement number tabel](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12recevicedcn8.png)

<span data-ttu-id="731fa-180">Op basis van het tijdsinterval hello, Hallo incrementele runtimestatus van een primaire regio tooa secundaire regio worden gerepliceerd.</span><span class="sxs-lookup"><span data-stu-id="731fa-180">Based on hello time interval, hello incremental runtime status replicates from a primary region tooa secondary region.</span></span> <span data-ttu-id="731fa-181">Tijdens een gebeurtenis na noodgevallen wanneer Hallo primaire regio niet beschikbaar, directe verkeer toohello secundaire regio voor bedrijfscontinuïteit.</span><span class="sxs-lookup"><span data-stu-id="731fa-181">During a disaster event, when hello primary region is not available, direct traffic toohello secondary region for business continuity.</span></span> 

## <a name="edifact"></a><span data-ttu-id="731fa-182">EDIFACT</span><span class="sxs-lookup"><span data-stu-id="731fa-182">EDIFACT</span></span> 

<span data-ttu-id="731fa-183">Zakelijke continuïteit voor EDI EDIFACT documenten is gebaseerd op het besturingselement cijfers.</span><span class="sxs-lookup"><span data-stu-id="731fa-183">Business continuity for EDI EDIFACT documents is based on control numbers.</span></span>

<span data-ttu-id="731fa-184">**Vereisten**</span><span class="sxs-lookup"><span data-stu-id="731fa-184">**Prerequisites**</span></span>

<span data-ttu-id="731fa-185">noodherstel tooenable voor inkomende berichten Hallo dubbele controle-instellingen te selecteren in instellingen voor het ontvangen van uw EDIFACT-overeenkomst.</span><span class="sxs-lookup"><span data-stu-id="731fa-185">tooenable disaster recovery for inbound messages, select hello duplicate check settings in your EDIFACT agreement's Receive Settings.</span></span>

![Instellingen voor controle op dubbele items selecteren](./media/logic-apps-enterprise-integration-b2b-business-continuity/edifactdupcheck.png)  

1. <span data-ttu-id="731fa-187">Maak een [logische app](../logic-apps/logic-apps-create-a-logic-app.md) in een secundaire regio.</span><span class="sxs-lookup"><span data-stu-id="731fa-187">Create a [logic app](../logic-apps/logic-apps-create-a-logic-app.md) in a secondary region.</span></span>    

2. <span data-ttu-id="731fa-188">Zoeken op **EDIFACT**, en selecteer **EDIFACT - als een getal van het besturingselement wordt gewijzigd**.</span><span class="sxs-lookup"><span data-stu-id="731fa-188">Search on **EDIFACT**, and select **EDIFACT - When a control number is modified**.</span></span>

   ![Zoeken naar EDIFACT](./media/logic-apps-enterprise-integration-b2b-business-continuity/edifactcn1.png)

   <span data-ttu-id="731fa-190">Hallo trigger vraagt u een account voor verbinding tooan integratie tooestablish.</span><span class="sxs-lookup"><span data-stu-id="731fa-190">hello trigger prompts you tooestablish a connection tooan integration account.</span></span> 
   <span data-ttu-id="731fa-191">Hallo trigger moet worden verbonden tooa primaire regio integratie-account.</span><span class="sxs-lookup"><span data-stu-id="731fa-191">hello trigger should be connected tooa primary region integration account.</span></span> 

3. <span data-ttu-id="731fa-192">Geef de verbindingsnaam van een, selecteer uw *primaire regio integratie account* van Hallo lijst en kies **maken**.</span><span class="sxs-lookup"><span data-stu-id="731fa-192">Enter a connection name, select your *primary region integration account* from hello list, and choose **Create**.</span></span>    

   ![Primaire regio integratie-accountnaam](./media/logic-apps-enterprise-integration-b2b-business-continuity/X12CN2.png)

4. <span data-ttu-id="731fa-194">Hallo **DateTime toostart besturingselement nummer sync** instelling is optioneel.</span><span class="sxs-lookup"><span data-stu-id="731fa-194">hello **DateTime toostart control number sync** setting is optional.</span></span> <span data-ttu-id="731fa-195">Hallo **frequentie** te kunnen worden ingesteld**dag**, **uur**, **minuut**, of **tweede** met een interval.</span><span class="sxs-lookup"><span data-stu-id="731fa-195">hello **Frequency** can be set too**Day**, **Hour**, **Minute**, or **Second** with an interval.</span></span>    

   ![Datum/tijd- en frequentie](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn3.png)

6. <span data-ttu-id="731fa-197">Selecteer **nieuwe stap** > **een actie toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="731fa-197">Select **New step** > **Add an action**.</span></span>    

   ![Nieuwe stap, een actie toevoegen](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn4.png)

7. <span data-ttu-id="731fa-199">Zoeken op **EDIFACT**, en selecteer **EDIFACT - toevoegen of bijwerken van besturingselement cijfers**.</span><span class="sxs-lookup"><span data-stu-id="731fa-199">Search on **EDIFACT**, and select **EDIFACT - Add or update control numbers**.</span></span>   

   ![Toevoegen of bijwerken van besturingselement cijfers](./media/logic-apps-enterprise-integration-b2b-business-continuity/EdifactChooseAction.png)

8. <span data-ttu-id="731fa-201">tooconnect tooa secundaire regio integratie actieaccount, selecteer **verbinding wijzigen** > **nieuwe verbinding toevoegen** voor een lijst met beschikbare Hallo-integratieaccounts.</span><span class="sxs-lookup"><span data-stu-id="731fa-201">tooconnect an action tooa secondary region integration account, select **Change connection** > **Add new connection** for a list of hello available integration accounts.</span></span> <span data-ttu-id="731fa-202">Geef de verbindingsnaam van een, selecteer uw *secundaire regio integratie account* van Hallo lijst en kies **maken**.</span><span class="sxs-lookup"><span data-stu-id="731fa-202">Enter a connection name, select your *secondary region integration account* from hello list, and choose **Create**.</span></span>

   ![Secundaire regio integratie-accountnaam](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn6.png)

9. <span data-ttu-id="731fa-204">Tooraw invoer switch door te klikken op Hallo-pictogram in de rechterbovenhoek.</span><span class="sxs-lookup"><span data-stu-id="731fa-204">Switch tooraw inputs by clicking on hello icon in upper right corner.</span></span>

   ![Switch tooraw invoer](./media/logic-apps-enterprise-integration-b2b-business-continuity/Edifactrawinputs.png)

10. <span data-ttu-id="731fa-206">Selecteer hoofdtekst van dynamische inhoud objectkiezer Hallo en Hallo logic app wordt opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="731fa-206">Select Body from hello dynamic content picker, and save hello logic app.</span></span>   

   ![Dynamische inhoud velden](./media/logic-apps-enterprise-integration-b2b-business-continuity/X12CN7.png)

   <span data-ttu-id="731fa-208">Op basis van het tijdsinterval hello, Hallo trigger Hallo primaire regio ontvangen besturingselement nummer tabel worden opgevraagd en haalt Hallo nieuwe records.</span><span class="sxs-lookup"><span data-stu-id="731fa-208">Based on hello time interval, hello trigger polls hello primary region received control number table and pulls hello new records.</span></span>
   <span data-ttu-id="731fa-209">Hallo actie bijgewerkt Hallo records toohello secundaire regio integratie-account.</span><span class="sxs-lookup"><span data-stu-id="731fa-209">hello action updates hello records toohello secondary region integration account.</span></span> 
   <span data-ttu-id="731fa-210">Als er geen updates zijn, Hallo trigger status weergegeven als **overgeslagen**.</span><span class="sxs-lookup"><span data-stu-id="731fa-210">If there are no updates, hello trigger status appears as **Skipped**.</span></span>

   ![Besturingselement number tabel](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12recevicedcn8.png)

<span data-ttu-id="731fa-212">Op basis van het tijdsinterval hello, Hallo incrementele runtimestatus van een primaire regio tooa secundaire regio worden gerepliceerd.</span><span class="sxs-lookup"><span data-stu-id="731fa-212">Based on hello time interval, hello incremental runtime status replicates from a primary region tooa secondary region.</span></span> <span data-ttu-id="731fa-213">Tijdens een gebeurtenis na noodgevallen wanneer Hallo primaire regio niet beschikbaar, directe verkeer toohello secundaire regio voor bedrijfscontinuïteit.</span><span class="sxs-lookup"><span data-stu-id="731fa-213">During a disaster event, when hello primary region is not available, direct traffic toohello secondary region for business continuity.</span></span> 

## <a name="as2"></a><span data-ttu-id="731fa-214">AS2</span><span class="sxs-lookup"><span data-stu-id="731fa-214">AS2</span></span> 

<span data-ttu-id="731fa-215">Zakelijke continuïteit voor documenten die gebruikmaken van Hallo AS2-protocol is gebaseerd op het Hallo-bericht-ID en Hallo MIC waarde.</span><span class="sxs-lookup"><span data-stu-id="731fa-215">Business continuity for documents that use hello AS2 protocol is based on hello message ID and hello MIC value.</span></span>

> [!TIP]
> <span data-ttu-id="731fa-216">U kunt ook Hallo [AS2 snel starten sjabloon](https://github.com/Azure/azure-quickstart-templates/pull/3302) toocreate logic apps.</span><span class="sxs-lookup"><span data-stu-id="731fa-216">You can also use hello [AS2 quick start template](https://github.com/Azure/azure-quickstart-templates/pull/3302) toocreate logic apps.</span></span> <span data-ttu-id="731fa-217">Maken primaire en secundaire integratieaccounts zijn vereisten toouse Hallo sjabloon.</span><span class="sxs-lookup"><span data-stu-id="731fa-217">Creating primary and secondary integration accounts are prerequisites toouse hello template.</span></span> <span data-ttu-id="731fa-218">Hallo-sjabloon kunt een logische app met een trigger en een actie maken.</span><span class="sxs-lookup"><span data-stu-id="731fa-218">hello template helps create a logic app that has a trigger and an action.</span></span> <span data-ttu-id="731fa-219">Hallo logische app maakt een verbinding van een trigger tooa primaire integratie-account en een actie tooa secundaire integratie-account.</span><span class="sxs-lookup"><span data-stu-id="731fa-219">hello logic app creates a connection from a trigger tooa primary integration account and an action tooa secondary integration account.</span></span>

1. <span data-ttu-id="731fa-220">Maak een [logische app](../logic-apps/logic-apps-create-a-logic-app.md) in Hallo secundaire regio.</span><span class="sxs-lookup"><span data-stu-id="731fa-220">Create a [logic app](../logic-apps/logic-apps-create-a-logic-app.md) in hello secondary region.</span></span>  

2. <span data-ttu-id="731fa-221">Zoeken op **AS2**, en selecteer **AS2 - waarde als een MIC is gemaakt**.</span><span class="sxs-lookup"><span data-stu-id="731fa-221">Search on **AS2**, and select **AS2 - When a MIC value is created**.</span></span>   

   ![Zoeken naar AS2](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid1.png)

   <span data-ttu-id="731fa-223">Een trigger wordt u gevraagd een verbindingsaccount voor de integratie van tooan tooestablish.</span><span class="sxs-lookup"><span data-stu-id="731fa-223">A trigger prompts you tooestablish a connection tooan integration account.</span></span> 
   <span data-ttu-id="731fa-224">Hallo trigger moet worden verbonden tooa primaire regio integratie-account.</span><span class="sxs-lookup"><span data-stu-id="731fa-224">hello trigger should be connected tooa primary region integration account.</span></span> 
   
3. <span data-ttu-id="731fa-225">Geef de verbindingsnaam van een, selecteer uw *primaire regio integratie account* van Hallo lijst en kies **maken**.</span><span class="sxs-lookup"><span data-stu-id="731fa-225">Enter a connection name, select your *primary region integration account* from hello list, and choose **Create**.</span></span>

   ![Primaire regio integratie-accountnaam](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid2.png)

4. <span data-ttu-id="731fa-227">Hallo **DateTime toostart MIC waarde sync** instelling is optioneel.</span><span class="sxs-lookup"><span data-stu-id="731fa-227">hello **DateTime toostart MIC value sync** setting is optional.</span></span> <span data-ttu-id="731fa-228">Hallo **frequentie** te kunnen worden ingesteld**dag**, **uur**, **minuut**, of **tweede** met een interval.</span><span class="sxs-lookup"><span data-stu-id="731fa-228">hello **Frequency** can be set too**Day**, **Hour**, **Minute**, or **Second** with an interval.</span></span>   

   ![Datum/tijd- en frequentie](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid3.png)

5. <span data-ttu-id="731fa-230">Selecteer **nieuwe stap** > **een actie toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="731fa-230">Select **New step** > **Add an action**.</span></span>  

   ![Nieuwe stap, een actie toevoegen](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid4.png)

6. <span data-ttu-id="731fa-232">Zoeken op **AS2**, en selecteer **AS2 - toevoegen of bijwerken van de inhoud van de MIC**.</span><span class="sxs-lookup"><span data-stu-id="731fa-232">Search on **AS2**, and select **AS2 - Add or update MIC contents**.</span></span>  

   ![MIC toevoegen of bijwerken](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid5.png)

7. <span data-ttu-id="731fa-234">tooconnect tooa secundaire integratie actieaccount, selecteer **verbinding wijzigen** > **nieuwe verbinding toevoegen** voor een lijst met beschikbare Hallo-integratieaccounts.</span><span class="sxs-lookup"><span data-stu-id="731fa-234">tooconnect an action tooa secondary integration account, select **Change connection** > **Add new connection** for a list of hello available integration accounts.</span></span> <span data-ttu-id="731fa-235">Geef de verbindingsnaam van een, selecteer uw *secundaire regio integratie account* van Hallo lijst en kies **maken**.</span><span class="sxs-lookup"><span data-stu-id="731fa-235">Enter a connection name, select your *secondary region integration account* from hello list, and choose **Create**.</span></span>

   ![Secundaire regio integratie-accountnaam](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid6.png)

8. <span data-ttu-id="731fa-237">Tooraw invoer switch door te klikken op Hallo-pictogram in de rechterbovenhoek.</span><span class="sxs-lookup"><span data-stu-id="731fa-237">Switch tooraw inputs by clicking on hello icon in upper right corner.</span></span>

   ![Switch tooraw invoer](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2rawinputs.png)

9. <span data-ttu-id="731fa-239">Selecteer hoofdtekst van dynamische inhoud objectkiezer Hallo en Hallo logic app wordt opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="731fa-239">Select Body from hello dynamic content picker, and save hello logic app.</span></span>   

   ![Dynamische inhoud](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid7.png)

   <span data-ttu-id="731fa-241">Op basis van het tijdsinterval hello, Hallo trigger Hallo primaire regio tabel worden opgevraagd en haalt Hallo nieuwe records.</span><span class="sxs-lookup"><span data-stu-id="731fa-241">Based on hello time interval, hello trigger polls hello primary region table and pulls hello new records.</span></span> <span data-ttu-id="731fa-242">Hallo actie werkt ze toohello secundaire regio integratie-account.</span><span class="sxs-lookup"><span data-stu-id="731fa-242">hello action updates them toohello secondary region integration account.</span></span> 
   <span data-ttu-id="731fa-243">Als er geen updates zijn, Hallo trigger status weergegeven als **overgeslagen**.</span><span class="sxs-lookup"><span data-stu-id="731fa-243">If there are no updates, hello trigger status appears as **Skipped**.</span></span>  

   ![Primaire regio tabel](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid8.png)

<span data-ttu-id="731fa-245">Op basis van het tijdsinterval hello, repliceert Hallo incrementele runtimestatus van Hallo primaire regio toohello secundaire regio.</span><span class="sxs-lookup"><span data-stu-id="731fa-245">Based on hello time interval, hello incremental runtime status replicates from hello primary region toohello secondary region.</span></span> <span data-ttu-id="731fa-246">Tijdens een gebeurtenis na noodgevallen wanneer Hallo primaire regio niet beschikbaar, directe verkeer toohello secundaire regio voor bedrijfscontinuïteit.</span><span class="sxs-lookup"><span data-stu-id="731fa-246">During a disaster event, when hello primary region is not available, direct traffic toohello secondary region for business continuity.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="731fa-247">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="731fa-247">Next steps</span></span>

[<span data-ttu-id="731fa-248">B2B-berichten bewaken</span><span class="sxs-lookup"><span data-stu-id="731fa-248">Monitor B2B messages</span></span>](logic-apps-monitor-b2b-message.md)


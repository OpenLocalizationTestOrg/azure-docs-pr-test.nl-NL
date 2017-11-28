---
title: aaaDiagnose fouten - Azure Logic Apps | Microsoft Docs
description: Algemene manieren toounderstand waar logische apps zijn mislukt
services: logic-apps
documentationcenter: .net,nodejs,java
author: jeffhollan
manager: anneta
editor: 
ms.assetid: a6727ebd-39bd-4298-9e68-2ae98738576e
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 10/18/2016
ms.author: LADocs; jehollan
ms.openlocfilehash: 46d318625820034c95e6df3a71ab84c58f076dd7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="diagnose-logic-app-failures"></a><span data-ttu-id="4bf11-103">Logic app mislukte diagnoses</span><span class="sxs-lookup"><span data-stu-id="4bf11-103">Diagnose logic app failures</span></span>
<span data-ttu-id="4bf11-104">Als u problemen of fouten met uw logische apps optreden, er zijn enkele manieren kunt u beter te begrijpen waar Hallo fouten afkomstig zijn uit.</span><span class="sxs-lookup"><span data-stu-id="4bf11-104">If you experience issues or failures with your logic apps, there are a few approaches can help you better understand where hello failures are coming from.</span></span>  

## <a name="azure-portal-tools"></a><span data-ttu-id="4bf11-105">Azure portal-hulpprogramma 's</span><span class="sxs-lookup"><span data-stu-id="4bf11-105">Azure portal tools</span></span>
<span data-ttu-id="4bf11-106">Hello Azure-portal biedt veel toodiagnose van hulpprogramma's voor elke logische app bij elke stap.</span><span class="sxs-lookup"><span data-stu-id="4bf11-106">hello Azure portal provides many tools toodiagnose each logic app at each step.</span></span>

### <a name="trigger-history"></a><span data-ttu-id="4bf11-107">Geschiedenis van de trigger</span><span class="sxs-lookup"><span data-stu-id="4bf11-107">Trigger history</span></span>

<span data-ttu-id="4bf11-108">Elke app logica heeft ten minste één trigger.</span><span class="sxs-lookup"><span data-stu-id="4bf11-108">Each logic app has at least one trigger.</span></span> <span data-ttu-id="4bf11-109">Als u merkt dat apps worden niet geactiveerd, zoek eerst Hallo trigger geschiedenis voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="4bf11-109">If you notice that apps aren't firing, look first at hello trigger history for more information.</span></span> <span data-ttu-id="4bf11-110">U kunt toegang tot geschiedenis van Hallo-trigger op Hallo logica app'ss hoofdblade.</span><span class="sxs-lookup"><span data-stu-id="4bf11-110">You can access hello trigger history on hello logic app'ss main blade.</span></span>

![Zoeken naar Hallo trigger geschiedenis][1]

<span data-ttu-id="4bf11-112">Hallo trigger geschiedenislijsten die alle pogingen die uw logische app activeren.</span><span class="sxs-lookup"><span data-stu-id="4bf11-112">hello trigger history lists all trigger attempts that your logic app made.</span></span> <span data-ttu-id="4bf11-113">U kunt klikken op elke poging trigger toodrill in Hallo details specifiek, een invoer of uitvoer die Hallo trigger poging gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="4bf11-113">You can click each trigger attempt toodrill into hello details, specifically, any inputs or outputs that hello trigger attempt generated.</span></span> <span data-ttu-id="4bf11-114">Als u mislukte triggers vinden, selecteer Hallo trigger poging en kies Hallo **uitvoer** koppelen tooreview eventuele gegenereerde foutberichten, bijvoorbeeld voor FTP-referenties die ongeldig zijn.</span><span class="sxs-lookup"><span data-stu-id="4bf11-114">If you find failed triggers, select hello trigger attempt and choose hello **Outputs** link tooreview any generated error messages, for example, for FTP credentials that aren't valid.</span></span>

<span data-ttu-id="4bf11-115">Hallo verschillende statussen ziet u mogelijk zijn:</span><span class="sxs-lookup"><span data-stu-id="4bf11-115">hello different statuses you might see are:</span></span>

* <span data-ttu-id="4bf11-116">**Overgeslagen**.</span><span class="sxs-lookup"><span data-stu-id="4bf11-116">**Skipped**.</span></span> <span data-ttu-id="4bf11-117">Hallo-eindpunt polled toocheck voor gegevens is en dat er geen gegevens beschikbaar was antwoord ontvangen.</span><span class="sxs-lookup"><span data-stu-id="4bf11-117">hello endpoint was polled toocheck for data and received a response that no data was available.</span></span>
* <span data-ttu-id="4bf11-118">**Geslaagd**.</span><span class="sxs-lookup"><span data-stu-id="4bf11-118">**Succeeded**.</span></span> <span data-ttu-id="4bf11-119">Hallo trigger ontvangen gegevens is beschikbaar antwoord.</span><span class="sxs-lookup"><span data-stu-id="4bf11-119">hello trigger received a response that data was available.</span></span> <span data-ttu-id="4bf11-120">Deze status kan worden veroorzaakt door een handmatige trigger, een terugkeerpatroon trigger of een polling-trigger.</span><span class="sxs-lookup"><span data-stu-id="4bf11-120">This status might result from a manual trigger, a recurrence trigger, or a polling trigger.</span></span> <span data-ttu-id="4bf11-121">Deze status wordt meestal vergezeld van Hallo **Fired** status, maar mogelijk niet als er een voorwaarde of SplitOn opdracht in de codeweergave die niet is voldaan.</span><span class="sxs-lookup"><span data-stu-id="4bf11-121">This status is usually accompanied by hello **Fired** status, but might not be if you have a condition or SplitOn command in code view that wasn't satisfied.</span></span>
* <span data-ttu-id="4bf11-122">**Kan geen**.</span><span class="sxs-lookup"><span data-stu-id="4bf11-122">**Failed**.</span></span> <span data-ttu-id="4bf11-123">Er is een fout gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="4bf11-123">An error was generated.</span></span>

#### <a name="start-a-trigger-manually"></a><span data-ttu-id="4bf11-124">Een trigger handmatig starten</span><span class="sxs-lookup"><span data-stu-id="4bf11-124">Start a trigger manually</span></span>

<span data-ttu-id="4bf11-125">Als u wilt dat Hallo logic app toocheck voor een beschikbare trigger onmiddellijk zonder te wachten op de volgende terugkeerpatroon hello, klikt u op **Trigger selecteren** op Hallo hoofdblade tooforce een controle.</span><span class="sxs-lookup"><span data-stu-id="4bf11-125">If you want hello logic app toocheck for an available trigger immediately without waiting for hello next recurrence, click **Select Trigger** on hello main blade tooforce a check.</span></span> <span data-ttu-id="4bf11-126">Bijvoorbeeld, te klikken op deze koppeling met een trigger Dropbox zorgt ervoor dat Hallo werkstroom tooimmediately poll Dropbox voor nieuwe bestanden.</span><span class="sxs-lookup"><span data-stu-id="4bf11-126">For example, clicking this link with a Dropbox trigger causes hello workflow tooimmediately poll Dropbox for new files.</span></span>

### <a name="run-history"></a><span data-ttu-id="4bf11-127">geschiedenis uitvoeren</span><span class="sxs-lookup"><span data-stu-id="4bf11-127">Run history</span></span>

<span data-ttu-id="4bf11-128">Elke gestarte trigger resulteert in een uitvoering.</span><span class="sxs-lookup"><span data-stu-id="4bf11-128">Every fired trigger results in a run.</span></span> <span data-ttu-id="4bf11-129">U kunt informatie over openen vanaf Hallo hoofdblade, met veel details die kunnen u helpen begrijpen wat is er gebeurd tijdens het Hallo-werkstroom.</span><span class="sxs-lookup"><span data-stu-id="4bf11-129">You can access run information from hello main blade, which contains many details that can help you understand what happened during hello workflow.</span></span>

![Zoeken naar Hallo geschiedenis uitvoeren][2]

<span data-ttu-id="4bf11-131">Een uitvoering geeft Hallo volgende statussen:</span><span class="sxs-lookup"><span data-stu-id="4bf11-131">A run displays one of hello following statuses:</span></span>

* <span data-ttu-id="4bf11-132">**Geslaagd**.</span><span class="sxs-lookup"><span data-stu-id="4bf11-132">**Succeeded**.</span></span> <span data-ttu-id="4bf11-133">Alle acties is voltooid.</span><span class="sxs-lookup"><span data-stu-id="4bf11-133">All actions succeeded.</span></span> <span data-ttu-id="4bf11-134">Als er een fout opgetreden, is die is mislukt door een actie die is opgetreden in de werkstroom hello later verwerkt.</span><span class="sxs-lookup"><span data-stu-id="4bf11-134">If a failure happened, that failure was handled by an action that occurred later in hello workflow.</span></span> <span data-ttu-id="4bf11-135">Dat wil zeggen, werd Hallo mislukt uitgevoerd door een actie die toorun na een mislukte actie is ingesteld.</span><span class="sxs-lookup"><span data-stu-id="4bf11-135">That is, hello failure was handled by an action that was set toorun after a failed action.</span></span>
* <span data-ttu-id="4bf11-136">**Kan geen**.</span><span class="sxs-lookup"><span data-stu-id="4bf11-136">**Failed**.</span></span> <span data-ttu-id="4bf11-137">Ten minste één actie heeft een fout die niet is verwerkt door de actie later in Hallo-werkstroom.</span><span class="sxs-lookup"><span data-stu-id="4bf11-137">At least one action had a failure that was not handled by an action later in hello workflow.</span></span>
* <span data-ttu-id="4bf11-138">**Geannuleerd**.</span><span class="sxs-lookup"><span data-stu-id="4bf11-138">**Cancelled**.</span></span> <span data-ttu-id="4bf11-139">Hallo werkstroom werd uitgevoerd, maar heeft een annuleringsaanvraag ontvangen.</span><span class="sxs-lookup"><span data-stu-id="4bf11-139">hello workflow was running but received a cancel request.</span></span>
* <span data-ttu-id="4bf11-140">**Met**.</span><span class="sxs-lookup"><span data-stu-id="4bf11-140">**Running**.</span></span> <span data-ttu-id="4bf11-141">Hallo werkstroom momenteel wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="4bf11-141">hello workflow is currently running.</span></span> <span data-ttu-id="4bf11-142">Deze status kan optreden voor beperkte werkstromen, of vanwege Hallo huidige plan prijzen.</span><span class="sxs-lookup"><span data-stu-id="4bf11-142">This status might occur for throttled workflows, or because of hello current pricing plan.</span></span> <span data-ttu-id="4bf11-143">Zie voor meer informatie [actie limieten op de pagina met prijzen Hallo](https://azure.microsoft.com/pricing/details/app-service/plans/).</span><span class="sxs-lookup"><span data-stu-id="4bf11-143">For details, see [action limits on hello pricing page](https://azure.microsoft.com/pricing/details/app-service/plans/).</span></span> <span data-ttu-id="4bf11-144">Configureren van diagnostische gegevens (Hallo grafieken die worden weergegeven onder Hallo geschiedenis uitvoeren) kunt bieden ook informatie over eventuele vertraging gebeurtenissen die zich voordoen.</span><span class="sxs-lookup"><span data-stu-id="4bf11-144">Configuring diagnostics (hello charts that appear under hello run history) also can provide information about any throttle events that happen.</span></span>

<span data-ttu-id="4bf11-145">Wanneer u een uitvoeringsgeschiedenis bekijkt, kunt u inzoomen voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="4bf11-145">When you are looking at a run history, you can drill in for more details.</span></span>  

#### <a name="trigger-outputs"></a><span data-ttu-id="4bf11-146">Trigger-uitvoer</span><span class="sxs-lookup"><span data-stu-id="4bf11-146">Trigger outputs</span></span>

<span data-ttu-id="4bf11-147">Trigger voert weergeven Hallo gegevens die afkomstig zijn van het Hallo-trigger.</span><span class="sxs-lookup"><span data-stu-id="4bf11-147">Trigger outputs show hello data that came from hello trigger.</span></span> <span data-ttu-id="4bf11-148">Deze uitvoer kunt u bepalen of alle eigenschappen naar verwachting geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="4bf11-148">These outputs can help you determine whether all properties returned as expected.</span></span>

> [!NOTE]
> <span data-ttu-id="4bf11-149">Als er inhoud die u niet begrijpt, informatie over hoe Azure Logic Apps [verschillende typen inhoud verwerkt](../logic-apps/logic-apps-content-type.md).</span><span class="sxs-lookup"><span data-stu-id="4bf11-149">If you see any content that you don't understand, learn how Azure Logic Apps [handles different content types](../logic-apps/logic-apps-content-type.md).</span></span>
> 

![Voorbeelden van trigger-uitvoer][3]

#### <a name="action-inputs-and-outputs"></a><span data-ttu-id="4bf11-151">Actie-invoer en uitvoer</span><span class="sxs-lookup"><span data-stu-id="4bf11-151">Action inputs and outputs</span></span>

<span data-ttu-id="4bf11-152">U kunt inzoomen op het Hallo-in- en uitgangen die een actie ontvangen.</span><span class="sxs-lookup"><span data-stu-id="4bf11-152">You can drill into hello inputs and outputs that an action received.</span></span> <span data-ttu-id="4bf11-153">Deze gegevens zijn handig om te begrijpen Hallo afmeting en vorm van Hallo outputs en voor het vinden van eventuele foutberichten die mogelijk zijn gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="4bf11-153">This data is useful for understanding hello size and shape of hello outputs, and also for finding any error messages that might have been generated.</span></span>

![Actie-invoer en uitvoer][4]

## <a name="debug-workflow-runtime"></a><span data-ttu-id="4bf11-155">Fouten opsporen in workflowruntime</span><span class="sxs-lookup"><span data-stu-id="4bf11-155">Debug workflow runtime</span></span>

<span data-ttu-id="4bf11-156">Samen met bewaking Hallo invoer, uitvoer en triggers van een reeks, kunt u sommige stappen tooa werkstroom die u helpen bij foutopsporing toevoegen.</span><span class="sxs-lookup"><span data-stu-id="4bf11-156">Along with monitoring hello inputs, outputs, and triggers of a run, you could add some steps tooa workflow that help with debugging.</span></span> 
<span data-ttu-id="4bf11-157">[RequestBin](http://requestb.in) is een krachtig hulpprogramma waarmee u als een stap in een werkstroom toevoegen kunt.</span><span class="sxs-lookup"><span data-stu-id="4bf11-157">[RequestBin](http://requestb.in) is a powerful tool that you can add as a step in a workflow.</span></span> <span data-ttu-id="4bf11-158">U kunt met behulp van RequestBin een HTTP-aanvraag inspector toodetermine Hallo exacte grootte, vorm en indeling van een HTTP-aanvraag instellen.</span><span class="sxs-lookup"><span data-stu-id="4bf11-158">By using RequestBin, you can set up an HTTP request inspector toodetermine hello exact size, shape, and format of an HTTP request.</span></span> <span data-ttu-id="4bf11-159">U kunt een RequestBin maken en plak de URL van de Hallo in een logische app HTTP POST-actie met de inhoud van de hoofdtekst is dat u wilt dat tootest, bijvoorbeeld, een expressie of een andere stap uitvoer.</span><span class="sxs-lookup"><span data-stu-id="4bf11-159">You can create a RequestBin and paste hello URL in a logic app HTTP POST action with body content that you want tootest, for example, an expression or another step output.</span></span> <span data-ttu-id="4bf11-160">Na het uitvoeren van Hallo logische app, kunt u uw RequestBin toosee hoe Hallo aanvraag werd gevormd wanneer gegenereerd vanuit Logic Apps-engine Hallo vernieuwen.</span><span class="sxs-lookup"><span data-stu-id="4bf11-160">After you run hello logic app, you can refresh your RequestBin toosee how hello request was formed when generated from hello Logic Apps engine.</span></span>

<!-- image references -->
[1]: ./media/logic-apps-diagnosing-failures/triggerhistory.png
[2]: ./media/logic-apps-diagnosing-failures/runhistory.png
[3]: ./media/logic-apps-diagnosing-failures/triggeroutputslink.png
[4]: ./media/logic-apps-diagnosing-failures/actionoutputs.png

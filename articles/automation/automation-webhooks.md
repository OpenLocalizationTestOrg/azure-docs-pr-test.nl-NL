---
title: Een Azure Automation-runbook beginnen met een webhook | Microsoft Docs
description: Een webhook waarmee een client een runbook in Azure Automation starten vanuit een aanroep van HTTP.  Dit artikel wordt beschreven voor het maken van een webhook en het aanroepen van een voor het starten van een runbook.
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: 9b20237c-a593-4299-bbdc-35c47ee9e55d
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: magoedte;bwren;sngun
ms.openlocfilehash: 6c65427fcd18e41a90dfb872aa9525f758b17b87
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="starting-an-azure-automation-runbook-with-a-webhook"></a><span data-ttu-id="061d0-104">Een Azure Automation-runbook beginnen met een webhook</span><span class="sxs-lookup"><span data-stu-id="061d0-104">Starting an Azure Automation runbook with a webhook</span></span>
<span data-ttu-id="061d0-105">Een *webhook* kunt u een bepaald runbook te starten in Azure Automation via één HTTP-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="061d0-105">A *webhook* allows you to start a particular runbook in Azure Automation through a single HTTP request.</span></span> <span data-ttu-id="061d0-106">Hierdoor kan externe services, zoals Visual Studio Team Services, GitHub, logboekanalyse van Microsoft Operations Management Suite of aangepaste toepassingen runbooks starten zonder het implementeren van een volledige oplossing met de Azure Automation-API.</span><span class="sxs-lookup"><span data-stu-id="061d0-106">This allows external services such as Visual Studio Team Services, GitHub, Microsoft Operations Management Suite Log Analytics, or custom applications to start runbooks without implementing a full solution using the Azure Automation API.</span></span>  
<span data-ttu-id="061d0-107">![WebhooksOverview](media/automation-webhooks/webhook-overview-image.png)</span><span class="sxs-lookup"><span data-stu-id="061d0-107">![WebhooksOverview](media/automation-webhooks/webhook-overview-image.png)</span></span>

<span data-ttu-id="061d0-108">U kunt vergelijken met webhooks aan andere methoden van een runbook starten [een runbook starten in Azure Automation](automation-starting-a-runbook.md)</span><span class="sxs-lookup"><span data-stu-id="061d0-108">You can compare webhooks to other methods of starting a runbook in [Starting a runbook in Azure Automation](automation-starting-a-runbook.md)</span></span>

## <a name="details-of-a-webhook"></a><span data-ttu-id="061d0-109">Details van een webhook</span><span class="sxs-lookup"><span data-stu-id="061d0-109">Details of a webhook</span></span>
<span data-ttu-id="061d0-110">De volgende tabel beschrijft de eigenschappen die u voor een webhook configureren moet.</span><span class="sxs-lookup"><span data-stu-id="061d0-110">The following table describes the properties that you must configure for a webhook.</span></span>

| <span data-ttu-id="061d0-111">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="061d0-111">Property</span></span> | <span data-ttu-id="061d0-112">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="061d0-112">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="061d0-113">Naam</span><span class="sxs-lookup"><span data-stu-id="061d0-113">Name</span></span> |<span data-ttu-id="061d0-114">U kunt elke gewenste naam voor een webhook omdat dit geen toegang heeft tot de client opgeven.</span><span class="sxs-lookup"><span data-stu-id="061d0-114">You can provide any name you want for a webhook since this is not exposed to the client.</span></span>  <span data-ttu-id="061d0-115">Dit wordt alleen gebruikt voor u te identificeren van het runbook in Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="061d0-115">It is only used for you to identify the runbook in Azure Automation.</span></span> <br>  <span data-ttu-id="061d0-116">Als een best practice moet u de webhook geeft een naam die betrekking hebben op de client die wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="061d0-116">As a best practice, you should give the webhook a name related to the client that will use it.</span></span> |
| <span data-ttu-id="061d0-117">URL</span><span class="sxs-lookup"><span data-stu-id="061d0-117">URL</span></span> |<span data-ttu-id="061d0-118">De URL van de webhook is het unieke adres waarmee een client wordt aangeroepen met een HTTP POST naar het runbook dat is gekoppeld aan de webhook starten.</span><span class="sxs-lookup"><span data-stu-id="061d0-118">The URL of the webhook is the unique address that a client calls with an HTTP POST to start the runbook linked to the webhook.</span></span>  <span data-ttu-id="061d0-119">Bij het maken van de webhook wordt automatisch gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="061d0-119">It is automatically generated when you create the webhook.</span></span>  <span data-ttu-id="061d0-120">U kunt een aangepaste URL niet opgeven.</span><span class="sxs-lookup"><span data-stu-id="061d0-120">You cannot specify a custom URL.</span></span> <br> <br>  <span data-ttu-id="061d0-121">De URL bevat een beveiligingstoken waarmee het runbook kan worden aangeroepen door een systeem van derden zonder verdere verificatie.</span><span class="sxs-lookup"><span data-stu-id="061d0-121">The URL contains a security token that allows the runbook to be invoked by a third party system with no further authentication.</span></span> <span data-ttu-id="061d0-122">Daarom moet het worden behandeld als een wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="061d0-122">For this reason, it should be treated like a password.</span></span>  <span data-ttu-id="061d0-123">Uit veiligheidsoverwegingen kunt u alleen de URL in de Azure portal weergeven op het moment dat de webhook is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="061d0-123">For security reasons, you can only view the URL in the Azure portal at the time the webhook is created.</span></span> <span data-ttu-id="061d0-124">Houd er rekening mee de URL in een veilige locatie voor toekomstig gebruik.</span><span class="sxs-lookup"><span data-stu-id="061d0-124">You should note the URL in a secure location for future use.</span></span> |
| <span data-ttu-id="061d0-125">Vervaldatum</span><span class="sxs-lookup"><span data-stu-id="061d0-125">Expiration date</span></span> |<span data-ttu-id="061d0-126">Zoals een certificaat heeft elke webhook een vervaldatum op dat moment kan niet meer worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="061d0-126">Like a certificate, each webhook has an expiration date at which time it can no longer be used.</span></span>  <span data-ttu-id="061d0-127">Deze vervaldatum kan worden gewijzigd nadat de webhook is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="061d0-127">This expiration date can be modified after the webhook is created.</span></span> |
| <span data-ttu-id="061d0-128">Ingeschakeld</span><span class="sxs-lookup"><span data-stu-id="061d0-128">Enabled</span></span> |<span data-ttu-id="061d0-129">Een webhook is standaard ingeschakeld wanneer deze wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="061d0-129">A webhook is enabled by default when it is created.</span></span>  <span data-ttu-id="061d0-130">Als u deze op uitgeschakeld, instellen wordt er geen client kunnen gebruiken.</span><span class="sxs-lookup"><span data-stu-id="061d0-130">If you set it to Disabled, then no client will be able to use it.</span></span>  <span data-ttu-id="061d0-131">U kunt instellen de **ingeschakeld** eigenschap bij het maken van de webhook of op elk gewenst moment eenmaal is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="061d0-131">You can set the **Enabled** property when you create the webhook or anytime once it is created.</span></span> |

### <a name="parameters"></a><span data-ttu-id="061d0-132">Parameters</span><span class="sxs-lookup"><span data-stu-id="061d0-132">Parameters</span></span>
<span data-ttu-id="061d0-133">Een webhook kunt waarden voor runbookparameters die worden gebruikt wanneer het runbook wordt gestart door die webhook definiëren.</span><span class="sxs-lookup"><span data-stu-id="061d0-133">A webhook can define values for runbook parameters that are used when the runbook is started by that webhook.</span></span> <span data-ttu-id="061d0-134">De webhook waarden voor de verplichte parameters van het runbook moet bevatten en waarden voor de volgende optionele parameters kan bevatten.</span><span class="sxs-lookup"><span data-stu-id="061d0-134">The webhook must include values for any mandatory parameters of the runbook and may include values for optional parameters.</span></span> <span data-ttu-id="061d0-135">Een parameterwaarde die is geconfigureerd voor een webhook kan zelfs na het maken van de webhoook worden gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="061d0-135">A parameter value configured to a webhook can be modified even after creating the webhoook.</span></span> <span data-ttu-id="061d0-136">Meerdere webhooks die zijn gekoppeld aan één runbook kunt elke andere parameterwaarden gebruiken.</span><span class="sxs-lookup"><span data-stu-id="061d0-136">Multiple webhooks linked to a single runbook can each use different parameter values.</span></span>

<span data-ttu-id="061d0-137">Wanneer een client wordt gestart van een runbook met behulp van een webhook, kan zij de parameterwaarden die zijn gedefinieerd in de webhook niet overschrijven.</span><span class="sxs-lookup"><span data-stu-id="061d0-137">When a client starts a runbook using a webhook, it cannot override the parameter values defined in the webhook.</span></span>  <span data-ttu-id="061d0-138">Om gegevens te ontvangen van de client, kan het runbook aangeroepen één parameter accepteren. **$WebhookData** van het type [object] die gegevens bevatten die de client in de POST-aanvraag bevat.</span><span class="sxs-lookup"><span data-stu-id="061d0-138">To receive data from the client, the runbook can accept a single parameter called **$WebhookData** of type [object] that will contain data that the client includes in the POST request.</span></span>

![Webhookdata-eigenschappen](media/automation-webhooks/webhook-data-properties.png)

<span data-ttu-id="061d0-140">De **$WebhookData** object heeft de volgende eigenschappen:</span><span class="sxs-lookup"><span data-stu-id="061d0-140">The **$WebhookData** object will have the following properties:</span></span>

| <span data-ttu-id="061d0-141">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="061d0-141">Property</span></span> | <span data-ttu-id="061d0-142">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="061d0-142">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="061d0-143">WebhookName</span><span class="sxs-lookup"><span data-stu-id="061d0-143">WebhookName</span></span> |<span data-ttu-id="061d0-144">De naam van de webhook.</span><span class="sxs-lookup"><span data-stu-id="061d0-144">The name of the webhook.</span></span> |
| <span data-ttu-id="061d0-145">RequestHeader</span><span class="sxs-lookup"><span data-stu-id="061d0-145">RequestHeader</span></span> |<span data-ttu-id="061d0-146">Hash-tabel met de headers van de binnenkomende POST-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="061d0-146">Hash table containing the headers of the incoming POST request.</span></span> |
| <span data-ttu-id="061d0-147">requestBody</span><span class="sxs-lookup"><span data-stu-id="061d0-147">RequestBody</span></span> |<span data-ttu-id="061d0-148">De hoofdtekst van de binnenkomende POST-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="061d0-148">The body of the incoming POST request.</span></span>  <span data-ttu-id="061d0-149">Hiermee behoudt alle opmaak zoals tekenreeks, JSON, XML, of formulier gecodeerde gegevens.</span><span class="sxs-lookup"><span data-stu-id="061d0-149">This will retain any formatting such as string, JSON, XML, or form encoded data.</span></span> <span data-ttu-id="061d0-150">Het runbook moet zijn geschreven met de indeling van gegevens die naar verwachting werkt.</span><span class="sxs-lookup"><span data-stu-id="061d0-150">The runbook must be written to work with the data format that is expected.</span></span> |

<span data-ttu-id="061d0-151">Er is geen configuratie van de webhook vereist ter ondersteuning van de **$WebhookData** parameter en het runbook is niet vereist te accepteren.</span><span class="sxs-lookup"><span data-stu-id="061d0-151">There is no configuration of the webhook required to support the **$WebhookData** parameter, and the runbook is not required to accept it.</span></span>  <span data-ttu-id="061d0-152">Als het runbook wordt niet gedefinieerd voor de parameter, worden er details van de aanvraag is verzonden vanaf de client genegeerd.</span><span class="sxs-lookup"><span data-stu-id="061d0-152">If the runbook does not define the parameter, then any details of the request sent from the client is ignored.</span></span>

<span data-ttu-id="061d0-153">Als u een waarde voor $WebhookData opgeven bij het maken van de webhook dat waarde overschreven worden zal wanneer u de webhook start het runbook met de gegevens van de client POST-aanvraag, zelfs als de client geen gegevens in de aanvraagtekst bevatten.</span><span class="sxs-lookup"><span data-stu-id="061d0-153">If you specify a value for $WebhookData when you create the webhook, that value will be overriden when the webhook starts the runbook with the data from the client POST request, even if the client does not include any data in the request body.</span></span>  <span data-ttu-id="061d0-154">Als u een runbook met een andere methode dan een webhook met $WebhookData start, kunt u een waarde opgeven voor $Webhookdata die wordt herkend door het runbook.</span><span class="sxs-lookup"><span data-stu-id="061d0-154">If you start a runbook that has $WebhookData using a method other than a webhook, you can provide a value for $Webhookdata that will be recognized by the runbook.</span></span>  <span data-ttu-id="061d0-155">Deze waarde moet een object met dezelfde [eigenschappen](#details-of-a-webhook) als $Webhookdata zodat het runbook correct ermee werken kunt alsof het was in combinatie met de werkelijke WebhookData doorgegeven door een webhook.</span><span class="sxs-lookup"><span data-stu-id="061d0-155">This value should be an object with the same [properties](#details-of-a-webhook) as $Webhookdata so that the runbook can properly work with it as if it was working with actual WebhookData passed by a webhook.</span></span>

<span data-ttu-id="061d0-156">Bijvoorbeeld, als u de volgende runbook vanuit de Azure-Portal starten zijn en doorgeven aantal voorbeelden WebhookData wilt voor testdoeleinden, aangezien WebhookData een object is, moet deze worden doorgegeven als JSON in de gebruikersinterface.</span><span class="sxs-lookup"><span data-stu-id="061d0-156">For example, if you are starting the following runbook from the Azure Portal and want to pass some sample WebhookData for testing, since WebhookData is an object, it should be passed as JSON in the UI.</span></span>

![De parameter WebhookData door de gebruikersinterface](media/automation-webhooks/WebhookData-parameter-from-UI.png)

<span data-ttu-id="061d0-158">Voor het bovenstaande runbook als u de volgende eigenschappen voor de parameter WebhookData hebt:</span><span class="sxs-lookup"><span data-stu-id="061d0-158">For the above runbook, if you have the following properties for the WebhookData parameter:</span></span>

1. <span data-ttu-id="061d0-159">WebhookName: *MyWebhook*</span><span class="sxs-lookup"><span data-stu-id="061d0-159">WebhookName: *MyWebhook*</span></span>
2. <span data-ttu-id="061d0-160">RequestHeader: *van de testgebruiker =*</span><span class="sxs-lookup"><span data-stu-id="061d0-160">RequestHeader: *From=Test User*</span></span>
3. <span data-ttu-id="061d0-161">RequestBody: *['VM1', 'VM2']*</span><span class="sxs-lookup"><span data-stu-id="061d0-161">RequestBody: *[“VM1”, “VM2”]*</span></span>

<span data-ttu-id="061d0-162">Vervolgens wilt u de volgende JSON-waarde in de gebruikersinterface voor de WebhookData-parameter doorgeven:</span><span class="sxs-lookup"><span data-stu-id="061d0-162">Then you would pass the following JSON value in the UI for the WebhookData parameter:</span></span>  

* <span data-ttu-id="061d0-163">{'WebhookName': 'MyWebhook', "RequestHeader": {'Van': 'Test gebruiker'}, "RequestBody": "[\"VM1\",\"VM2\"]"}</span><span class="sxs-lookup"><span data-stu-id="061d0-163">{"WebhookName":"MyWebhook", "RequestHeader":{"From":"Test User"}, "RequestBody":"[\"VM1\",\"VM2\"]"}</span></span>

![Parameter WebhookData starten door de gebruikersinterface](media/automation-webhooks/Start-WebhookData-parameter-from-UI.png)

> [!NOTE]
> <span data-ttu-id="061d0-165">De waarden van alle invoerparameters worden geregistreerd met de runbooktaak.</span><span class="sxs-lookup"><span data-stu-id="061d0-165">The values of all input parameters are logged with the runbook job.</span></span>  <span data-ttu-id="061d0-166">Dit betekent dat een opgegeven door de client in de aanvraag webhook invoer worden vastgelegd en toegankelijk voor iedereen met toegang tot de automation-taak.</span><span class="sxs-lookup"><span data-stu-id="061d0-166">This means that any input provided by the client in the webhook request will be logged and available to anyone with access to the automation job.</span></span>  <span data-ttu-id="061d0-167">Daarom moet u voorzichtig met gevoelige informatie in de webhook aanroepen.</span><span class="sxs-lookup"><span data-stu-id="061d0-167">For this reason, you should be cautious about including sensitive information in webhook calls.</span></span>
>

## <a name="security"></a><span data-ttu-id="061d0-168">Beveiliging</span><span class="sxs-lookup"><span data-stu-id="061d0-168">Security</span></span>
<span data-ttu-id="061d0-169">De beveiliging van een webhook is afhankelijk van de privacy van de URL die een beveiligingstoken dat toestaat dat deze bevat kan worden aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="061d0-169">The security of a webhook relies on the privacy of its URL which contains a security token that allows it to be invoked.</span></span> <span data-ttu-id="061d0-170">Azure Automation biedt verificatie niet uitvoeren op de aanvraag zo lang wordt gemaakt aan de juiste URL.</span><span class="sxs-lookup"><span data-stu-id="061d0-170">Azure Automation does not perform any authentication on the request as long as it is made to the correct URL.</span></span> <span data-ttu-id="061d0-171">Om deze reden moet webhooks niet worden gebruikt voor runbooks die uiterst gevoelige functies uitvoeren zonder gebruik van een alternatieve methode voor de aanvraag wordt gevalideerd.</span><span class="sxs-lookup"><span data-stu-id="061d0-171">For this reason, webhooks should not be used for runbooks that perform highly sensitive functions without using an alternate means of validating the request.</span></span>

<span data-ttu-id="061d0-172">U kunt opnemen logica binnen het runbook om te bepalen of deze door een webhook is aangeroepen door het controleren van de **WebhookName** eigenschap van de parameter $WebhookData.</span><span class="sxs-lookup"><span data-stu-id="061d0-172">You can include logic within the runbook to determine that it was called by a webhook by checking the **WebhookName** property of the $WebhookData parameter.</span></span> <span data-ttu-id="061d0-173">Het runbook kan verder validatie uitvoeren door te zoeken naar specifieke informatie in de **RequestHeader** of **RequestBody** eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="061d0-173">The runbook could perform further validation by looking for particular information in the **RequestHeader** or **RequestBody** properties.</span></span>

<span data-ttu-id="061d0-174">Een andere strategie is om het runbook sommige validatie van een externe voorwaarde uitvoeren wanneer het een webhook-aanvraag ontvangen.</span><span class="sxs-lookup"><span data-stu-id="061d0-174">Another strategy is to have the runbook perform some validation of an external condition when it received a webhook request.</span></span>  <span data-ttu-id="061d0-175">Neem bijvoorbeeld een runbook dat wordt aangeroepen door GitHub wanneer er een nieuwe doorvoeren naar een GitHub-opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="061d0-175">For example, consider a runbook that is called by GitHub whenever there is a new commit to a GitHub repository.</span></span>  <span data-ttu-id="061d0-176">Het runbook mogelijk verbinding met GitHub te valideren dat een nieuwe doorvoer eigenlijk gewoon voordat u doorgaat opgetreden.</span><span class="sxs-lookup"><span data-stu-id="061d0-176">The runbook might connect to GitHub to validate that a new commit had actually just occurred before continuing.</span></span>

## <a name="creating-a-webhook"></a><span data-ttu-id="061d0-177">Maken van een webhook</span><span class="sxs-lookup"><span data-stu-id="061d0-177">Creating a webhook</span></span>
<span data-ttu-id="061d0-178">Gebruik de volgende procedure voor het maken van een nieuwe webhook gekoppeld aan een runbook in de Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="061d0-178">Use the following procedure to create a new webhook linked to a runbook in the Azure portal.</span></span>

1. <span data-ttu-id="061d0-179">Van de **Runbooks blade** in de Azure-portal klikt u op het runbook waarmee de webhook wordt gestart om de blade details weer te geven.</span><span class="sxs-lookup"><span data-stu-id="061d0-179">From the **Runbooks blade** in the Azure portal, click the runbook that the webhook will start to view its detail blade.</span></span>
2. <span data-ttu-id="061d0-180">Klik op **Webhook** boven aan de blade opent de **Webhook toevoegen** blade.</span><span class="sxs-lookup"><span data-stu-id="061d0-180">Click **Webhook** at the top of the blade to open the **Add Webhook** blade.</span></span> <br><span data-ttu-id="061d0-181">
   ![Knop webhooks.](media/automation-webhooks/webhooks-button.png)</span><span class="sxs-lookup"><span data-stu-id="061d0-181">
![Webhooks button](media/automation-webhooks/webhooks-button.png)</span></span>
3. <span data-ttu-id="061d0-182">Klik op **maken van nieuwe webhook** openen de **webhook-blade maken**.</span><span class="sxs-lookup"><span data-stu-id="061d0-182">Click **Create new webhook** to open the **Create webhook blade**.</span></span>
4. <span data-ttu-id="061d0-183">Geef een **naam**, **vervaldatum** voor de webhook en Hiermee wordt aangegeven of moet worden ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="061d0-183">Specify a **Name**, **Expiration Date** for the webhook and whether it should be enabled.</span></span> <span data-ttu-id="061d0-184">Zie [Details van een webhook](#details-of-a-webhook) voor meer informatie deze eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="061d0-184">See [Details of a webhook](#details-of-a-webhook) for more information these properties.</span></span>
5. <span data-ttu-id="061d0-185">Klik op het pictogram kopiëren en druk op Ctrl + C om de URL van de webhook kopiëren.</span><span class="sxs-lookup"><span data-stu-id="061d0-185">Click the copy icon and press Ctrl+C to copy the URL of the webhook.</span></span>  <span data-ttu-id="061d0-186">Noteer de op een veilige plaats.</span><span class="sxs-lookup"><span data-stu-id="061d0-186">Then record it in a safe place.</span></span>  <span data-ttu-id="061d0-187">**Als u de webhook gemaakt, kan u de URL opnieuw niet ophalen.**</span><span class="sxs-lookup"><span data-stu-id="061d0-187">**Once you create the webhook, you cannot retrieve the URL again.**</span></span> <br><span data-ttu-id="061d0-188">
   ![Webhook-URL](media/automation-webhooks/copy-webhook-url.png)</span><span class="sxs-lookup"><span data-stu-id="061d0-188">
![Webhook URL](media/automation-webhooks/copy-webhook-url.png)</span></span>
6. <span data-ttu-id="061d0-189">Klik op **Parameters** waarden opgeven voor de runbookparameters.</span><span class="sxs-lookup"><span data-stu-id="061d0-189">Click **Parameters** to provide values for the runbook parameters.</span></span>  <span data-ttu-id="061d0-190">Als het runbook verplichte parameters heeft, klikt zich u niet kunnen maken van de webhook tenzij waarden zijn opgegeven.</span><span class="sxs-lookup"><span data-stu-id="061d0-190">If the runbook has mandatory parameters, then you will not be able to create the webhook unless values are provided.</span></span>
7. <span data-ttu-id="061d0-191">Klik op **maken** voor het maken van de webhook.</span><span class="sxs-lookup"><span data-stu-id="061d0-191">Click **Create** to create the webhook.</span></span>

## <a name="using-a-webhook"></a><span data-ttu-id="061d0-192">Met behulp van een webhook</span><span class="sxs-lookup"><span data-stu-id="061d0-192">Using a webhook</span></span>
<span data-ttu-id="061d0-193">Voor het gebruik van een webhook nadat deze is gemaakt, moet u de clienttoepassing een HTTP POST door de URL van de webhook verlenen.</span><span class="sxs-lookup"><span data-stu-id="061d0-193">To use a webhook after it has been created, your client application must issue an HTTP POST with the URL for the webhook.</span></span>  <span data-ttu-id="061d0-194">De syntaxis van de webhook bevindt zich in de volgende indeling.</span><span class="sxs-lookup"><span data-stu-id="061d0-194">The syntax of the webhook will be in the following format.</span></span>

    http://<Webhook Server>/token?=<Token Value>

<span data-ttu-id="061d0-195">De client ontvangt een van de volgende retourcodes van de POST-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="061d0-195">The client will receive one of the following return codes from the POST request.</span></span>  

| <span data-ttu-id="061d0-196">Code</span><span class="sxs-lookup"><span data-stu-id="061d0-196">Code</span></span> | <span data-ttu-id="061d0-197">Tekst</span><span class="sxs-lookup"><span data-stu-id="061d0-197">Text</span></span> | <span data-ttu-id="061d0-198">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="061d0-198">Description</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="061d0-199">202</span><span class="sxs-lookup"><span data-stu-id="061d0-199">202</span></span> |<span data-ttu-id="061d0-200">Geaccepteerd</span><span class="sxs-lookup"><span data-stu-id="061d0-200">Accepted</span></span> |<span data-ttu-id="061d0-201">De aanvraag is geaccepteerd en het runbook is in de wachtrij geplaatst.</span><span class="sxs-lookup"><span data-stu-id="061d0-201">The request was accepted, and the runbook was successfully queued.</span></span> |
| <span data-ttu-id="061d0-202">400</span><span class="sxs-lookup"><span data-stu-id="061d0-202">400</span></span> |<span data-ttu-id="061d0-203">Onjuiste aanvraag</span><span class="sxs-lookup"><span data-stu-id="061d0-203">Bad Request</span></span> |<span data-ttu-id="061d0-204">De aanvraag is niet geaccepteerd voor een van de volgende oorzaken hebben.</span><span class="sxs-lookup"><span data-stu-id="061d0-204">The request was not accepted for one of the following reasons.</span></span> <ul> <li><span data-ttu-id="061d0-205">De webhook is verlopen.</span><span class="sxs-lookup"><span data-stu-id="061d0-205">The webhook has expired.</span></span></li> <li><span data-ttu-id="061d0-206">De webhook is uitgeschakeld.</span><span class="sxs-lookup"><span data-stu-id="061d0-206">The webhook is disabled.</span></span></li> <li><span data-ttu-id="061d0-207">Het token in de URL is ongeldig.</span><span class="sxs-lookup"><span data-stu-id="061d0-207">The token in the URL is invalid.</span></span></li>  </ul> |
| <span data-ttu-id="061d0-208">404</span><span class="sxs-lookup"><span data-stu-id="061d0-208">404</span></span> |<span data-ttu-id="061d0-209">Niet gevonden</span><span class="sxs-lookup"><span data-stu-id="061d0-209">Not Found</span></span> |<span data-ttu-id="061d0-210">De aanvraag is niet geaccepteerd voor een van de volgende oorzaken hebben.</span><span class="sxs-lookup"><span data-stu-id="061d0-210">The request was not accepted for one of the following reasons.</span></span> <ul> <li><span data-ttu-id="061d0-211">De webhook is niet gevonden.</span><span class="sxs-lookup"><span data-stu-id="061d0-211">The webhook was not found.</span></span></li> <li><span data-ttu-id="061d0-212">Het runbook is niet gevonden.</span><span class="sxs-lookup"><span data-stu-id="061d0-212">The runbook was not found.</span></span></li> <li><span data-ttu-id="061d0-213">Het account is niet gevonden.</span><span class="sxs-lookup"><span data-stu-id="061d0-213">The account was not found.</span></span></li>  </ul> |
| <span data-ttu-id="061d0-214">500</span><span class="sxs-lookup"><span data-stu-id="061d0-214">500</span></span> |<span data-ttu-id="061d0-215">Interne serverfout</span><span class="sxs-lookup"><span data-stu-id="061d0-215">Internal Server Error</span></span> |<span data-ttu-id="061d0-216">De URL is geldig, maar er is een fout opgetreden.</span><span class="sxs-lookup"><span data-stu-id="061d0-216">The URL was valid, but an error occurred.</span></span>  <span data-ttu-id="061d0-217">Verzend de aanvraag.</span><span class="sxs-lookup"><span data-stu-id="061d0-217">Please resubmit the request.</span></span> |

<span data-ttu-id="061d0-218">Ervan uitgaande dat de aanvraag is voltooid, bevat het antwoord van de webhook de taak-id in JSON-indeling als volgt.</span><span class="sxs-lookup"><span data-stu-id="061d0-218">Assuming the request is successful, the webhook response contains the job id in JSON format as follows.</span></span> <span data-ttu-id="061d0-219">Bevat een enkele taak-id, maar de JSON-indeling kunt u mogelijke toekomstige verbeteringen.</span><span class="sxs-lookup"><span data-stu-id="061d0-219">It will contain a single job id, but the JSON format allows for potential future enhancements.</span></span>

    {"JobIds":["<JobId>"]}  

<span data-ttu-id="061d0-220">De client kan wanneer de runbooktaak is voltooid of de voltooiingsstatus ervan van de webhook niet vaststellen.</span><span class="sxs-lookup"><span data-stu-id="061d0-220">The client cannot determine when the runbook job completes or its completion status from the webhook.</span></span>  <span data-ttu-id="061d0-221">Dit kan bepalen dat deze gegevens met behulp van de taak-id met een andere methode, zoals [Windows PowerShell](http://msdn.microsoft.com/library/azure/dn690263.aspx) of de [Azure Automation-API](https://msdn.microsoft.com/library/azure/mt163826.aspx).</span><span class="sxs-lookup"><span data-stu-id="061d0-221">It can determine this information using the job id with another method such as [Windows PowerShell](http://msdn.microsoft.com/library/azure/dn690263.aspx) or the [Azure Automation API](https://msdn.microsoft.com/library/azure/mt163826.aspx).</span></span>

### <a name="example"></a><span data-ttu-id="061d0-222">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="061d0-222">Example</span></span>
<span data-ttu-id="061d0-223">Windows PowerShell wordt het volgende voorbeeld een runbook starten met een webhook.</span><span class="sxs-lookup"><span data-stu-id="061d0-223">The following example uses Windows PowerShell to start a runbook with a webhook.</span></span>  <span data-ttu-id="061d0-224">Houd er rekening mee dat elke taal die u van een HTTP-aanvraag maken kunt een webhook; kunt gebruiken Windows PowerShell wordt alleen gebruikt als voorbeeld hier.</span><span class="sxs-lookup"><span data-stu-id="061d0-224">Note that any language that can make an HTTP request can use a webhook; Windows PowerShell is just used here as an example.</span></span>

<span data-ttu-id="061d0-225">Het runbook is er een lijst met virtuele machines die zijn opgemaakt in JSON in de hoofdtekst van de aanvraag wordt verwacht.</span><span class="sxs-lookup"><span data-stu-id="061d0-225">The runbook is expecting a list of virtual machines formatted in JSON in the body of the request.</span></span> <span data-ttu-id="061d0-226">We zijn ook informatie over die wordt gestart, het runbook en de datum en tijd die wordt gestart in de koptekst van de aanvraag inclusief.</span><span class="sxs-lookup"><span data-stu-id="061d0-226">We also are including information about who is starting the runbook and the date and time it is being started in the header of the request.</span></span>      

    $uri = "https://s1events.azure-automation.net/webhooks?token=8ud0dSrSo%2fvHWpYbklW%3c8s0GrOKJZ9Nr7zqcS%2bIQr4c%3d"
    $headers = @{"From"="user@contoso.com";"Date"="05/28/2015 15:47:00"}

    $vms  = @(
                @{ Name="vm01";ServiceName="vm01"},
                @{ Name="vm02";ServiceName="vm02"}
            )
    $body = ConvertTo-Json -InputObject $vms

    $response = Invoke-RestMethod -Method Post -Uri $uri -Headers $headers -Body $body
    $jobid = ConvertFrom-Json $response


<span data-ttu-id="061d0-227">De volgende afbeelding toont de berichtkopinformatie (met behulp van een [Fiddler](http://www.telerik.com/fiddler) trace) van deze aanvraag.</span><span class="sxs-lookup"><span data-stu-id="061d0-227">The following image shows the header information (using a [Fiddler](http://www.telerik.com/fiddler) trace) from this request.</span></span> <span data-ttu-id="061d0-228">Dit omvat standaard headers van een HTTP-aanvraag naast de aangepaste datum en van de headers die we hebben toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="061d0-228">This includes standard headers of an HTTP request in addition to the custom Date and From headers that we added.</span></span>  <span data-ttu-id="061d0-229">Elk van deze waarden is beschikbaar voor het runbook in de **RequestHeaders** eigenschap van **WebhookData**.</span><span class="sxs-lookup"><span data-stu-id="061d0-229">Each of these values is available to the runbook in the **RequestHeaders** property of **WebhookData**.</span></span>

![Knop webhooks.](media/automation-webhooks/webhook-request-headers.png)

<span data-ttu-id="061d0-231">De volgende afbeelding toont de hoofdtekst van de aanvraag (met behulp van een [Fiddler](http://www.telerik.com/fiddler) trace) dat beschikbaar is voor het runbook in de **RequestBody** eigenschap van **WebhookData**.</span><span class="sxs-lookup"><span data-stu-id="061d0-231">The following image shows the body of the request (using a [Fiddler](http://www.telerik.com/fiddler) trace)  that is available to the runbook in the **RequestBody** property of **WebhookData**.</span></span> <span data-ttu-id="061d0-232">Dit is opgemaakt als JSON omdat die de indeling die is opgenomen in de hoofdtekst van de aanvraag is.</span><span class="sxs-lookup"><span data-stu-id="061d0-232">This is formatted as JSON because that was the format that was included in the body of the request.</span></span>     

![Knop webhooks.](media/automation-webhooks/webhook-request-body.png)

<span data-ttu-id="061d0-234">De volgende afbeelding toont de aanvraag worden verzonden vanaf de Windows PowerShell en het resulterende antwoord.</span><span class="sxs-lookup"><span data-stu-id="061d0-234">The following image shows the request being sent from Windows PowerShell and the resulting response.</span></span>  <span data-ttu-id="061d0-235">De taak-id is opgehaald uit het antwoord en geconverteerd naar een tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="061d0-235">The job id is extracted from the response and converted to a string.</span></span>

![Knop webhooks.](media/automation-webhooks/webhook-request-response.png)

<span data-ttu-id="061d0-237">Het volgende voorbeeldrunbook accepteert van het vorige voorbeeldaanvraag en start de virtuele machines dat is opgegeven in de aanvraagtekst.</span><span class="sxs-lookup"><span data-stu-id="061d0-237">The following sample runbook accepts the previous example request and starts the virtual machines specified in the request body.</span></span>

    workflow Test-StartVirtualMachinesFromWebhook
    {
        param (
            [object]$WebhookData
        )

        # If runbook was called from Webhook, WebhookData will not be null.
        if ($WebhookData -ne $null) {

            # Collect properties of WebhookData
            $WebhookName     =     $WebhookData.WebhookName
            $WebhookHeaders =     $WebhookData.RequestHeader
            $WebhookBody     =     $WebhookData.RequestBody

            # Collect individual headers. VMList converted from JSON.
            $From = $WebhookHeaders.From
            $VMList = ConvertFrom-Json -InputObject $WebhookBody
            Write-Output "Runbook started from webhook $WebhookName by $From."

            # Authenticate to Azure resources
            $Cred = Get-AutomationPSCredential -Name 'MyAzureCredential'
            Add-AzureAccount -Credential $Cred

            # Start each virtual machine
            foreach ($VM in $VMList)
            {
                $VMName = $VM.Name
                Write-Output "Starting $VMName"
                Start-AzureVM -Name $VM.Name -ServiceName $VM.ServiceName
            }
        }
        else {
            Write-Error "Runbook mean to be started only from webhook."
        }
    }


## <a name="starting-runbooks-in-response-to-azure-alerts"></a><span data-ttu-id="061d0-238">Starten van runbooks in reactie op waarschuwingen van Azure</span><span class="sxs-lookup"><span data-stu-id="061d0-238">Starting runbooks in response to Azure alerts</span></span>
<span data-ttu-id="061d0-239">Webhook ingeschakeld runbooks kunnen worden gebruikt om te reageren op [waarschuwingen van Azure](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="061d0-239">Webhook-enabled runbooks can be used to react to [Azure alerts](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span></span> <span data-ttu-id="061d0-240">Bronnen in Azure worden gecontroleerd door het verzamelen van de statistieken zoals prestaties, beschikbaarheid en gebruik met behulp van waarschuwingen van Azure.</span><span class="sxs-lookup"><span data-stu-id="061d0-240">Resources in Azure can be monitored by collecting the statistics like performance, availability and usage with the help of Azure alerts.</span></span> <span data-ttu-id="061d0-241">U kunt een waarschuwing op basis van de bewaking van metrische gegevens ontvangen of gebeurtenissen voor uw Azure-resources, momenteel Automation-Accounts ondersteunen alleen metrische gegevens.</span><span class="sxs-lookup"><span data-stu-id="061d0-241">You can receive an alert based on monitoring metrics or events for your Azure resources, currently Automation Accounts support only metrics.</span></span> <span data-ttu-id="061d0-242">Wanneer de waarde van een opgegeven waarde groter is dan de drempelwaarde die is toegewezen of als de geconfigureerde gebeurtenis wordt geactiveerd en vervolgens een melding wordt verzonden naar de servicebeheerder of co-beheerders de waarschuwing oplossen, voor meer informatie over metrische gegevens en gebeurtenissen Raadpleeg [waarschuwingen van Azure](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="061d0-242">When the value of a specified metric exceeds the threshold assigned or if the configured event is triggered then a notification is sent to the service admin or co-admins to resolve the alert, for more information on metrics and events please refer to [Azure alerts](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span></span>

<span data-ttu-id="061d0-243">Naast het gebruik van waarschuwingen van Azure als een waarschuwingssysteem, kunt u ook ere van runbooks in reactie op waarschuwingen.</span><span class="sxs-lookup"><span data-stu-id="061d0-243">Besides using Azure alerts as a notification system, you can also kick off runbooks in response to alerts.</span></span> <span data-ttu-id="061d0-244">Azure Automation biedt de mogelijkheid om uit te voeren webhook ingeschakeld runbooks met waarschuwingen van Azure.</span><span class="sxs-lookup"><span data-stu-id="061d0-244">Azure Automation provides the capability to run webhook-enabled runbooks with Azure alerts.</span></span> <span data-ttu-id="061d0-245">Wanneer een waarde groter is dan de geconfigureerde drempelwaarde vervolgens de waarschuwingsregel actief wordt en de automation-webhook die op zijn beurt wordt uitgevoerd het runbook wordt geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="061d0-245">When a metric exceeds the configured threshold value then the alert rule becomes active and triggers the automation webhook which in turn executes the runbook.</span></span>

![Webhooks.](media/automation-webhooks/webhook-alert.jpg)

### <a name="alert-context"></a><span data-ttu-id="061d0-247">Waarschuwingscontext</span><span class="sxs-lookup"><span data-stu-id="061d0-247">Alert context</span></span>
<span data-ttu-id="061d0-248">Houd rekening met een Azure-resource zoals een virtuele machine, CPU-gebruik van deze machine is een van de prestatie-metriek.</span><span class="sxs-lookup"><span data-stu-id="061d0-248">Consider an Azure resource such as a virtual machine, CPU utilization of this machine is one of the key performance metric.</span></span> <span data-ttu-id="061d0-249">Als het CPU-gebruik is 100% of meer dan een bepaald bedrag gedurende lange tijd weergegeven, is het raadzaam om opnieuw te starten van de virtuele machine om het probleem te verhelpen.</span><span class="sxs-lookup"><span data-stu-id="061d0-249">If the CPU utilization is 100% or more than a certain amount for long period of time, you might want to restart the virtual machine to fix the problem.</span></span> <span data-ttu-id="061d0-250">Dit kan worden opgelost door een waarschuwingsregel aan de virtuele machine configureren en deze regel gaat CPU-percentage als de metriek.</span><span class="sxs-lookup"><span data-stu-id="061d0-250">This can be solved by configuring an alert rule to the virtual machine and this rule takes CPU percentage as its metric.</span></span> <span data-ttu-id="061d0-251">Hier CPU-percentage wordt alleen gemaakt als voorbeeld, maar er zijn veel andere metrische gegevens die u voor uw Azure-resources configureren kunt en opnieuw starten van de virtuele machine is een actie die moet worden uitgevoerd om dit probleem te verhelpen, kunt u het runbook om andere acties te configureren.</span><span class="sxs-lookup"><span data-stu-id="061d0-251">CPU percentage here is just taken as an example but there are many other metrics that you can configure to your Azure resources and restarting the virtual machine is an action that is taken to fix this issue, you can configure the runbook to take other actions.</span></span>

<span data-ttu-id="061d0-252">Wanneer dit de waarschuwingsregel actief en activeert de runbook-webhook is ingeschakeld, verzendt het context van de waarschuwing aan het runbook.</span><span class="sxs-lookup"><span data-stu-id="061d0-252">When this the alert rule becomes active and triggers the webhook-enabled runbook, it sends the alert context to the runbook.</span></span> <span data-ttu-id="061d0-253">[Waarschuwingscontext](../monitoring-and-diagnostics/insights-receive-alert-notifications.md) bevat details, zoals **SubscriptionID**, **ResourceGroupName**, **ResourceName**, **ResourceType**, **ResourceId** en **tijdstempel** die zijn vereist voor het runbook de resource waarop deze actie te identificeren.</span><span class="sxs-lookup"><span data-stu-id="061d0-253">[Alert context](../monitoring-and-diagnostics/insights-receive-alert-notifications.md) contains details including **SubscriptionID**, **ResourceGroupName**, **ResourceName**, **ResourceType**, **ResourceId** and **Timestamp** which are required for the runbook to identify the resource on which it will be taking action.</span></span> <span data-ttu-id="061d0-254">Waarschuwing context is ingesloten in de hoofdtekst van de **WebhookData** object verzonden naar het runbook en deze kan worden geactiveerd met **Webhook.RequestBody** eigenschap</span><span class="sxs-lookup"><span data-stu-id="061d0-254">Alert context is embedded in the body part of the **WebhookData** object sent to the runbook and it can be accessed with **Webhook.RequestBody** property</span></span>

### <a name="example"></a><span data-ttu-id="061d0-255">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="061d0-255">Example</span></span>
<span data-ttu-id="061d0-256">Maken van een virtuele machine van Azure in uw abonnement en koppelen aan een [waarschuwing voor het bewaken van CPU-percentage metriek](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="061d0-256">Create an Azure virtual machine in your subscription and associate an [alert to monitor CPU percentage metric](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span></span> <span data-ttu-id="061d0-257">Zorg dat u het veld webhook met de URL van de webhook die is gegenereerd tijdens het maken van de webhook vullen tijdens het maken van de waarschuwing.</span><span class="sxs-lookup"><span data-stu-id="061d0-257">While creating the alert make sure you populate the webhook field with the URL of the webhook which was generated while creating the webhook.</span></span>

<span data-ttu-id="061d0-258">Het volgende voorbeeldrunbook wordt geactiveerd wanneer de waarschuwingsregel geactiveerd wordt en de context van de waarschuwing parameters die zijn vereist voor het runbook om te identificeren van de resource waarop deze actie te worden verzameld.</span><span class="sxs-lookup"><span data-stu-id="061d0-258">The following sample runbook is triggered when the alert rule becomes active and it collects the Alert context parameters which are required for the runbook to identify the resource on which it will be taking action.</span></span>

    workflow Invoke-RunbookUsingAlerts
    {
        param (      
            [object]$WebhookData
        )

        # If runbook was called from Webhook, WebhookData will not be null.
        if ($WebhookData -ne $null) {   
            # Collect properties of WebhookData.
            $WebhookName    =   $WebhookData.WebhookName
            $WebhookBody    =   $WebhookData.RequestBody
            $WebhookHeaders =   $WebhookData.RequestHeader

            # Outputs information on the webhook name that called This
            Write-Output "This runbook was started from webhook $WebhookName."


            # Obtain the WebhookBody containing the AlertContext
            $WebhookBody = (ConvertFrom-Json -InputObject $WebhookBody)
            Write-Output "`nWEBHOOK BODY"
            Write-Output "============="
            Write-Output $WebhookBody

            # Obtain the AlertContext     
            $AlertContext = [object]$WebhookBody.context

            # Some selected AlertContext information
            Write-Output "`nALERT CONTEXT DATA"
            Write-Output "==================="
            Write-Output $AlertContext.name
            Write-Output $AlertContext.subscriptionId
            Write-Output $AlertContext.resourceGroupName
            Write-Output $AlertContext.resourceName
            Write-Output $AlertContext.resourceType
            Write-Output $AlertContext.resourceId
            Write-Output $AlertContext.timestamp

            # Act on the AlertContext data, in our case restarting the VM.
            # Authenticate to your Azure subscription using Organization ID to be able to restart that Virtual Machine.
            $cred = Get-AutomationPSCredential -Name "MyAzureCredential"
            Add-AzureAccount -Credential $cred
            Select-AzureSubscription -subscriptionName "Visual Studio Ultimate with MSDN"

            #Check the status property of the VM
            Write-Output "Status of VM before taking action"
            Get-AzureVM -Name $AlertContext.resourceName -ServiceName $AlertContext.resourceName
            Write-Output "Restarting VM"

            # Restart the VM by passing VM name and Service name which are same in this case
            Restart-AzureVM -ServiceName $AlertContext.resourceName -Name $AlertContext.resourceName
            Write-Output "Status of VM after alert is active and takes action"
            Get-AzureVM -Name $AlertContext.resourceName -ServiceName $AlertContext.resourceName
        }
        else  
        {
            Write-Error "This runbook is meant to only be started from a webhook."  
        }  
    }



## <a name="next-steps"></a><span data-ttu-id="061d0-259">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="061d0-259">Next steps</span></span>
* <span data-ttu-id="061d0-260">Zie voor meer informatie over verschillende manieren om een runbook te starten [een Runbook starten](automation-starting-a-runbook.md).</span><span class="sxs-lookup"><span data-stu-id="061d0-260">For details on different ways to start a runbook, see [Starting a Runbook](automation-starting-a-runbook.md).</span></span>
* <span data-ttu-id="061d0-261">Raadpleeg voor informatie over het weergeven van de Status van een Runbook-Job [uitvoeren van Runbook in Azure Automation](automation-runbook-execution.md).</span><span class="sxs-lookup"><span data-stu-id="061d0-261">For information on viewing the Status of a Runbook Job, refer to [Runbook execution in Azure Automation](automation-runbook-execution.md).</span></span>
* <span data-ttu-id="061d0-262">Zie voor informatie over het gebruik van Azure Automation actie ondernemen op Azure-waarschuwingen, [Azure VM-waarschuwingen oplossen met Automation-Runbooks](automation-azure-vm-alert-integration.md).</span><span class="sxs-lookup"><span data-stu-id="061d0-262">To learn how to use Azure Automation to take action on Azure Alerts, see [Remediate Azure VM Alerts with Automation Runbooks](automation-azure-vm-alert-integration.md).</span></span>

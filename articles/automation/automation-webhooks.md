---
title: een Azure Automation-runbook met een webhook aaaStarting | Microsoft Docs
description: "Een webhook waarmee een client toostart een runbook in Azure Automation van een HTTP-aanroep.  Dit artikel wordt beschreven hoe een webhook toocreate en hoe toocall één toostart een runbook."
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
ms.openlocfilehash: ca6cde66b3784ceb5d0bc5921cee87aea74cb150
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="starting-an-azure-automation-runbook-with-a-webhook"></a><span data-ttu-id="d20da-104">Een Azure Automation-runbook beginnen met een webhook</span><span class="sxs-lookup"><span data-stu-id="d20da-104">Starting an Azure Automation runbook with a webhook</span></span>
<span data-ttu-id="d20da-105">Een *webhook* kunt u een bepaald runbook toostart in Azure Automation via één HTTP-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="d20da-105">A *webhook* allows you toostart a particular runbook in Azure Automation through a single HTTP request.</span></span> <span data-ttu-id="d20da-106">Hierdoor kan externe services, zoals Visual Studio Team Services, GitHub, logboekanalyse van Microsoft Operations Management Suite of aangepaste toepassingen toostart runbooks zonder het implementeren van een volledige oplossing met behulp van hello Azure Automation-API.</span><span class="sxs-lookup"><span data-stu-id="d20da-106">This allows external services such as Visual Studio Team Services, GitHub, Microsoft Operations Management Suite Log Analytics, or custom applications toostart runbooks without implementing a full solution using hello Azure Automation API.</span></span>  
<span data-ttu-id="d20da-107">![WebhooksOverview](media/automation-webhooks/webhook-overview-image.png)</span><span class="sxs-lookup"><span data-stu-id="d20da-107">![WebhooksOverview](media/automation-webhooks/webhook-overview-image.png)</span></span>

<span data-ttu-id="d20da-108">U kunt vergelijken met webhooks tooother methoden van een runbook starten [een runbook starten in Azure Automation](automation-starting-a-runbook.md)</span><span class="sxs-lookup"><span data-stu-id="d20da-108">You can compare webhooks tooother methods of starting a runbook in [Starting a runbook in Azure Automation](automation-starting-a-runbook.md)</span></span>

## <a name="details-of-a-webhook"></a><span data-ttu-id="d20da-109">Details van een webhook</span><span class="sxs-lookup"><span data-stu-id="d20da-109">Details of a webhook</span></span>
<span data-ttu-id="d20da-110">Hallo beschrijft volgende tabel Hallo-eigenschappen die u voor een webhook configureren moet.</span><span class="sxs-lookup"><span data-stu-id="d20da-110">hello following table describes hello properties that you must configure for a webhook.</span></span>

| <span data-ttu-id="d20da-111">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="d20da-111">Property</span></span> | <span data-ttu-id="d20da-112">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="d20da-112">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="d20da-113">Naam</span><span class="sxs-lookup"><span data-stu-id="d20da-113">Name</span></span> |<span data-ttu-id="d20da-114">U kunt opgeven dat elke gewenste naam voor een webhook aangezien dit toohello-client niet weergegeven.</span><span class="sxs-lookup"><span data-stu-id="d20da-114">You can provide any name you want for a webhook since this is not exposed toohello client.</span></span>  <span data-ttu-id="d20da-115">Het wordt alleen gebruikt voor u tooidentify hello runbook in Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="d20da-115">It is only used for you tooidentify hello runbook in Azure Automation.</span></span> <br>  <span data-ttu-id="d20da-116">Als een best practice moet u Hallo webhook geeft een naam gerelateerde toohello-client die wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="d20da-116">As a best practice, you should give hello webhook a name related toohello client that will use it.</span></span> |
| <span data-ttu-id="d20da-117">URL</span><span class="sxs-lookup"><span data-stu-id="d20da-117">URL</span></span> |<span data-ttu-id="d20da-118">Hallo-URL van de webhook Hallo is Hallo uniek adres dat een client met een HTTP POST toostart hello runbook aanroept toohello webhook gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="d20da-118">hello URL of hello webhook is hello unique address that a client calls with an HTTP POST toostart hello runbook linked toohello webhook.</span></span>  <span data-ttu-id="d20da-119">Bij het maken van de webhook hello wordt automatisch gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="d20da-119">It is automatically generated when you create hello webhook.</span></span>  <span data-ttu-id="d20da-120">U kunt een aangepaste URL niet opgeven.</span><span class="sxs-lookup"><span data-stu-id="d20da-120">You cannot specify a custom URL.</span></span> <br> <br>  <span data-ttu-id="d20da-121">Hallo-URL bevat een beveiligingstoken waarmee Hallo runbook toobe aangeroepen door een systeem van derden met geen verdere authenticatie.</span><span class="sxs-lookup"><span data-stu-id="d20da-121">hello URL contains a security token that allows hello runbook toobe invoked by a third party system with no further authentication.</span></span> <span data-ttu-id="d20da-122">Daarom moet het worden behandeld als een wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="d20da-122">For this reason, it should be treated like a password.</span></span>  <span data-ttu-id="d20da-123">Uit veiligheidsoverwegingen kunt u alleen weergave Hallo-URL in hello Azure-portal op Hallo tijd Hallo webhook is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="d20da-123">For security reasons, you can only view hello URL in hello Azure portal at hello time hello webhook is created.</span></span> <span data-ttu-id="d20da-124">Houd er rekening mee Hallo-URL op een veilige locatie voor toekomstig gebruik.</span><span class="sxs-lookup"><span data-stu-id="d20da-124">You should note hello URL in a secure location for future use.</span></span> |
| <span data-ttu-id="d20da-125">Vervaldatum</span><span class="sxs-lookup"><span data-stu-id="d20da-125">Expiration date</span></span> |<span data-ttu-id="d20da-126">Zoals een certificaat heeft elke webhook een vervaldatum op dat moment kan niet meer worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="d20da-126">Like a certificate, each webhook has an expiration date at which time it can no longer be used.</span></span>  <span data-ttu-id="d20da-127">Deze vervaldatum kan worden gewijzigd nadat Hallo webhook is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="d20da-127">This expiration date can be modified after hello webhook is created.</span></span> |
| <span data-ttu-id="d20da-128">Ingeschakeld</span><span class="sxs-lookup"><span data-stu-id="d20da-128">Enabled</span></span> |<span data-ttu-id="d20da-129">Een webhook is standaard ingeschakeld wanneer deze wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="d20da-129">A webhook is enabled by default when it is created.</span></span>  <span data-ttu-id="d20da-130">Als u deze tooDisabled hebt ingesteld, wordt geen client kunnen toouse deze.</span><span class="sxs-lookup"><span data-stu-id="d20da-130">If you set it tooDisabled, then no client will be able toouse it.</span></span>  <span data-ttu-id="d20da-131">U kunt instellen Hallo **ingeschakeld** eigenschap bij het maken van Hallo webhook of op elk gewenst moment eenmaal is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="d20da-131">You can set hello **Enabled** property when you create hello webhook or anytime once it is created.</span></span> |

### <a name="parameters"></a><span data-ttu-id="d20da-132">Parameters</span><span class="sxs-lookup"><span data-stu-id="d20da-132">Parameters</span></span>
<span data-ttu-id="d20da-133">Een webhook kunt waarden voor runbookparameters die worden gebruikt als Hallo runbook wordt gestart door die webhook definiëren.</span><span class="sxs-lookup"><span data-stu-id="d20da-133">A webhook can define values for runbook parameters that are used when hello runbook is started by that webhook.</span></span> <span data-ttu-id="d20da-134">Hallo webhook waarden voor de verplichte parameters van Hallo runbook moet bevatten en waarden voor de volgende optionele parameters kan bevatten.</span><span class="sxs-lookup"><span data-stu-id="d20da-134">hello webhook must include values for any mandatory parameters of hello runbook and may include values for optional parameters.</span></span> <span data-ttu-id="d20da-135">Een parameter die is geconfigureerd tooa webhook kan zelfs na het maken van Hallo webhoook worden gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="d20da-135">A parameter value configured tooa webhook can be modified even after creating hello webhoook.</span></span> <span data-ttu-id="d20da-136">Meerdere webhooks gekoppeld tooa één runbook kunt elke andere parameterwaarden gebruiken.</span><span class="sxs-lookup"><span data-stu-id="d20da-136">Multiple webhooks linked tooa single runbook can each use different parameter values.</span></span>

<span data-ttu-id="d20da-137">Wanneer een client wordt gestart van een runbook met behulp van een webhook, kan het Hallo-parameterwaarden die is gedefinieerd in Hallo webhook niet overschrijven.</span><span class="sxs-lookup"><span data-stu-id="d20da-137">When a client starts a runbook using a webhook, it cannot override hello parameter values defined in hello webhook.</span></span>  <span data-ttu-id="d20da-138">tooreceive gegevens van de client hello, Hallo runbook kan aangeroepen één parameter accepteren **$WebhookData** van het type [object] die gegevens bevat die client Hallo in Hallo POST-aanvraag bevat.</span><span class="sxs-lookup"><span data-stu-id="d20da-138">tooreceive data from hello client, hello runbook can accept a single parameter called **$WebhookData** of type [object] that will contain data that hello client includes in hello POST request.</span></span>

![Webhookdata-eigenschappen](media/automation-webhooks/webhook-data-properties.png)

<span data-ttu-id="d20da-140">Hallo **$WebhookData** object Hallo volgende eigenschappen hebben:</span><span class="sxs-lookup"><span data-stu-id="d20da-140">hello **$WebhookData** object will have hello following properties:</span></span>

| <span data-ttu-id="d20da-141">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="d20da-141">Property</span></span> | <span data-ttu-id="d20da-142">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="d20da-142">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="d20da-143">WebhookName</span><span class="sxs-lookup"><span data-stu-id="d20da-143">WebhookName</span></span> |<span data-ttu-id="d20da-144">Hallo-naam van de webhook Hallo.</span><span class="sxs-lookup"><span data-stu-id="d20da-144">hello name of hello webhook.</span></span> |
| <span data-ttu-id="d20da-145">RequestHeader</span><span class="sxs-lookup"><span data-stu-id="d20da-145">RequestHeader</span></span> |<span data-ttu-id="d20da-146">Hash-tabel met Hallo-kopteksten van Hallo binnenkomende POST-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="d20da-146">Hash table containing hello headers of hello incoming POST request.</span></span> |
| <span data-ttu-id="d20da-147">requestBody</span><span class="sxs-lookup"><span data-stu-id="d20da-147">RequestBody</span></span> |<span data-ttu-id="d20da-148">Hallo-hoofdtekst van Hallo binnenkomende POST-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="d20da-148">hello body of hello incoming POST request.</span></span>  <span data-ttu-id="d20da-149">Hiermee behoudt alle opmaak zoals tekenreeks, JSON, XML, of formulier gecodeerde gegevens.</span><span class="sxs-lookup"><span data-stu-id="d20da-149">This will retain any formatting such as string, JSON, XML, or form encoded data.</span></span> <span data-ttu-id="d20da-150">Hallo runbook moet worden geschreven als toowork met Hallo gegevensindeling die wordt verwacht.</span><span class="sxs-lookup"><span data-stu-id="d20da-150">hello runbook must be written toowork with hello data format that is expected.</span></span> |

<span data-ttu-id="d20da-151">Er is geen configuratie van Hallo webhook vereist toosupport hello **$WebhookData** parameter, en Hallo runbook is niet vereist tooaccept deze.</span><span class="sxs-lookup"><span data-stu-id="d20da-151">There is no configuration of hello webhook required toosupport hello **$WebhookData** parameter, and hello runbook is not required tooaccept it.</span></span>  <span data-ttu-id="d20da-152">Als Hallo runbook geen Hallo parameter gedefinieerd, wordt er details van Hallo-aanvraag is verzonden vanaf de client Hallo genegeerd.</span><span class="sxs-lookup"><span data-stu-id="d20da-152">If hello runbook does not define hello parameter, then any details of hello request sent from hello client is ignored.</span></span>

<span data-ttu-id="d20da-153">Als u een waarde voor $WebhookData opgeven bij het maken van de webhook hello, wordt die waarde worden onderdrukt wanneer Hallo webhook hello runbook met Hallo gegevens van Hallo client POST-aanvraag Start, zelfs als het Hallo-client geen gegevens in de aanvraagtekst Hallo bevatten.</span><span class="sxs-lookup"><span data-stu-id="d20da-153">If you specify a value for $WebhookData when you create hello webhook, that value will be overriden when hello webhook starts hello runbook with hello data from hello client POST request, even if hello client does not include any data in hello request body.</span></span>  <span data-ttu-id="d20da-154">Als u een runbook met een andere methode dan een webhook met $WebhookData start, kunt u een waarde opgeven voor $Webhookdata die wordt herkend door Hallo runbook.</span><span class="sxs-lookup"><span data-stu-id="d20da-154">If you start a runbook that has $WebhookData using a method other than a webhook, you can provide a value for $Webhookdata that will be recognized by hello runbook.</span></span>  <span data-ttu-id="d20da-155">Deze waarde moet een object met Hallo dezelfde [eigenschappen](#details-of-a-webhook) als $Webhookdata zodat dat runbook Hallo goed ermee werken kunt alsof het was in combinatie met de werkelijke WebhookData doorgegeven door een webhook.</span><span class="sxs-lookup"><span data-stu-id="d20da-155">This value should be an object with hello same [properties](#details-of-a-webhook) as $Webhookdata so that hello runbook can properly work with it as if it was working with actual WebhookData passed by a webhook.</span></span>

<span data-ttu-id="d20da-156">Bijvoorbeeld, als u begint Hallo na het runbook uit hello Azure-Portal en toopass sommige WebhookData voorbeeld voor het testen, aangezien WebhookData een object is wilt, moet deze worden doorgegeven als JSON in Hallo gebruikersinterface.</span><span class="sxs-lookup"><span data-stu-id="d20da-156">For example, if you are starting hello following runbook from hello Azure Portal and want toopass some sample WebhookData for testing, since WebhookData is an object, it should be passed as JSON in hello UI.</span></span>

![De parameter WebhookData door de gebruikersinterface](media/automation-webhooks/WebhookData-parameter-from-UI.png)

<span data-ttu-id="d20da-158">Voor Hallo hierboven runbook, als u de volgende eigenschappen voor de parameter WebhookData Hallo Hallo hebt:</span><span class="sxs-lookup"><span data-stu-id="d20da-158">For hello above runbook, if you have hello following properties for hello WebhookData parameter:</span></span>

1. <span data-ttu-id="d20da-159">WebhookName: *MyWebhook*</span><span class="sxs-lookup"><span data-stu-id="d20da-159">WebhookName: *MyWebhook*</span></span>
2. <span data-ttu-id="d20da-160">RequestHeader: *van de testgebruiker =*</span><span class="sxs-lookup"><span data-stu-id="d20da-160">RequestHeader: *From=Test User*</span></span>
3. <span data-ttu-id="d20da-161">RequestBody: *['VM1', 'VM2']*</span><span class="sxs-lookup"><span data-stu-id="d20da-161">RequestBody: *[“VM1”, “VM2”]*</span></span>

<span data-ttu-id="d20da-162">U zou vervolgens Hallo volgende JSON-waarde in Hallo UI voor Hallo WebhookData parameter doorgeven:</span><span class="sxs-lookup"><span data-stu-id="d20da-162">Then you would pass hello following JSON value in hello UI for hello WebhookData parameter:</span></span>  

* <span data-ttu-id="d20da-163">{'WebhookName': 'MyWebhook', "RequestHeader": {'Van': 'Test gebruiker'}, "RequestBody": "[\"VM1\",\"VM2\"]"}</span><span class="sxs-lookup"><span data-stu-id="d20da-163">{"WebhookName":"MyWebhook", "RequestHeader":{"From":"Test User"}, "RequestBody":"[\"VM1\",\"VM2\"]"}</span></span>

![Parameter WebhookData starten door de gebruikersinterface](media/automation-webhooks/Start-WebhookData-parameter-from-UI.png)

> [!NOTE]
> <span data-ttu-id="d20da-165">Hallo-waarden van alle invoerparameters worden geregistreerd met de runbooktaak Hallo.</span><span class="sxs-lookup"><span data-stu-id="d20da-165">hello values of all input parameters are logged with hello runbook job.</span></span>  <span data-ttu-id="d20da-166">Dit betekent dat een invoer zoals opgegeven door de client Hallo Hallo webhook aanvraag worden vastgelegd en beschikbaar tooanyone met toegang toohello automation-taak.</span><span class="sxs-lookup"><span data-stu-id="d20da-166">This means that any input provided by hello client in hello webhook request will be logged and available tooanyone with access toohello automation job.</span></span>  <span data-ttu-id="d20da-167">Daarom moet u voorzichtig met gevoelige informatie in de webhook aanroepen.</span><span class="sxs-lookup"><span data-stu-id="d20da-167">For this reason, you should be cautious about including sensitive information in webhook calls.</span></span>
>

## <a name="security"></a><span data-ttu-id="d20da-168">Beveiliging</span><span class="sxs-lookup"><span data-stu-id="d20da-168">Security</span></span>
<span data-ttu-id="d20da-169">Hallo beveiliging van een webhook is afhankelijk van Hallo privacy van de URL die bevat een beveiligingstoken waarmee dit toobe aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="d20da-169">hello security of a webhook relies on hello privacy of its URL which contains a security token that allows it toobe invoked.</span></span> <span data-ttu-id="d20da-170">Azure Automation biedt verificatie niet uitvoeren op aanvraag hello, zolang de juiste URL toohello wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="d20da-170">Azure Automation does not perform any authentication on hello request as long as it is made toohello correct URL.</span></span> <span data-ttu-id="d20da-171">Om deze reden moet webhooks niet worden gebruikt voor runbooks die uiterst gevoelige functies uitvoeren zonder gebruik van een alternatieve methode Hallo-aanvraag wordt gevalideerd.</span><span class="sxs-lookup"><span data-stu-id="d20da-171">For this reason, webhooks should not be used for runbooks that perform highly sensitive functions without using an alternate means of validating hello request.</span></span>

<span data-ttu-id="d20da-172">U kunt opnemen logica binnen Hallo runbook toodetermine dat deze door een webhook is aangeroepen door het controleren van Hallo **WebhookName** eigenschap van Hallo $WebhookData-parameter.</span><span class="sxs-lookup"><span data-stu-id="d20da-172">You can include logic within hello runbook toodetermine that it was called by a webhook by checking hello **WebhookName** property of hello $WebhookData parameter.</span></span> <span data-ttu-id="d20da-173">Hallo-runbook kan verder validatie uitvoeren door te zoeken naar specifieke informatie in Hallo **RequestHeader** of **RequestBody** eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="d20da-173">hello runbook could perform further validation by looking for particular information in hello **RequestHeader** or **RequestBody** properties.</span></span>

<span data-ttu-id="d20da-174">Een andere strategie die is toohave hello runbook validatie van een externe voorwaarde uitvoeren wanneer het een webhook-aanvraag ontvangen.</span><span class="sxs-lookup"><span data-stu-id="d20da-174">Another strategy is toohave hello runbook perform some validation of an external condition when it received a webhook request.</span></span>  <span data-ttu-id="d20da-175">Neem bijvoorbeeld een runbook dat wordt aangeroepen door GitHub wanneer er een nieuwe doorvoeren tooa GitHub-opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="d20da-175">For example, consider a runbook that is called by GitHub whenever there is a new commit tooa GitHub repository.</span></span>  <span data-ttu-id="d20da-176">Hallo runbook mogelijk verbinding tooGitHub toovalidate die eigenlijk gewoon een nieuwe doorvoer voordat u doorgaat opgetreden.</span><span class="sxs-lookup"><span data-stu-id="d20da-176">hello runbook might connect tooGitHub toovalidate that a new commit had actually just occurred before continuing.</span></span>

## <a name="creating-a-webhook"></a><span data-ttu-id="d20da-177">Maken van een webhook</span><span class="sxs-lookup"><span data-stu-id="d20da-177">Creating a webhook</span></span>
<span data-ttu-id="d20da-178">Hallo te volgen procedure toocreate een nieuw webhook gekoppeld tooa runbook in hello Azure-portal gebruiken.</span><span class="sxs-lookup"><span data-stu-id="d20da-178">Use hello following procedure toocreate a new webhook linked tooa runbook in hello Azure portal.</span></span>

1. <span data-ttu-id="d20da-179">Van Hallo **Runbooks blade** in hello Azure-portal, klikt u op Hallo runbook dat webhook Hallo gaat tooview de blade met details.</span><span class="sxs-lookup"><span data-stu-id="d20da-179">From hello **Runbooks blade** in hello Azure portal, click hello runbook that hello webhook will start tooview its detail blade.</span></span>
2. <span data-ttu-id="d20da-180">Klik op **Webhook** bovenaan Hallo Hallo blade tooopen hello **Webhook toevoegen** blade.</span><span class="sxs-lookup"><span data-stu-id="d20da-180">Click **Webhook** at hello top of hello blade tooopen hello **Add Webhook** blade.</span></span> <br><span data-ttu-id="d20da-181">
   ![Knop webhooks.](media/automation-webhooks/webhooks-button.png)</span><span class="sxs-lookup"><span data-stu-id="d20da-181">
![Webhooks button](media/automation-webhooks/webhooks-button.png)</span></span>
3. <span data-ttu-id="d20da-182">Klik op **maken van nieuwe webhook** tooopen hello **webhook-blade maken**.</span><span class="sxs-lookup"><span data-stu-id="d20da-182">Click **Create new webhook** tooopen hello **Create webhook blade**.</span></span>
4. <span data-ttu-id="d20da-183">Geef een **naam**, **vervaldatum** voor Hallo webhook en Hiermee wordt aangegeven of moet worden ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="d20da-183">Specify a **Name**, **Expiration Date** for hello webhook and whether it should be enabled.</span></span> <span data-ttu-id="d20da-184">Zie [Details van een webhook](#details-of-a-webhook) voor meer informatie deze eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="d20da-184">See [Details of a webhook](#details-of-a-webhook) for more information these properties.</span></span>
5. <span data-ttu-id="d20da-185">Klik op de pictogram kopiëren Hallo en druk op Ctrl + C toocopy Hallo-URL van de webhook Hallo.</span><span class="sxs-lookup"><span data-stu-id="d20da-185">Click hello copy icon and press Ctrl+C toocopy hello URL of hello webhook.</span></span>  <span data-ttu-id="d20da-186">Noteer de op een veilige plaats.</span><span class="sxs-lookup"><span data-stu-id="d20da-186">Then record it in a safe place.</span></span>  <span data-ttu-id="d20da-187">**Als u Hallo webhook gemaakt, kan u Hallo URL opnieuw niet ophalen.**</span><span class="sxs-lookup"><span data-stu-id="d20da-187">**Once you create hello webhook, you cannot retrieve hello URL again.**</span></span> <br><span data-ttu-id="d20da-188">
   ![Webhook-URL](media/automation-webhooks/copy-webhook-url.png)</span><span class="sxs-lookup"><span data-stu-id="d20da-188">
![Webhook URL](media/automation-webhooks/copy-webhook-url.png)</span></span>
6. <span data-ttu-id="d20da-189">Klik op **Parameters** tooprovide waarden voor de runbookparameters Hallo.</span><span class="sxs-lookup"><span data-stu-id="d20da-189">Click **Parameters** tooprovide values for hello runbook parameters.</span></span>  <span data-ttu-id="d20da-190">Als Hallo runbook verplichte parameters heeft, klikt u vervolgens zich u niet kunnen toocreate hello webhook tenzij waarden zijn opgegeven.</span><span class="sxs-lookup"><span data-stu-id="d20da-190">If hello runbook has mandatory parameters, then you will not be able toocreate hello webhook unless values are provided.</span></span>
7. <span data-ttu-id="d20da-191">Klik op **maken** toocreate hello webhook.</span><span class="sxs-lookup"><span data-stu-id="d20da-191">Click **Create** toocreate hello webhook.</span></span>

## <a name="using-a-webhook"></a><span data-ttu-id="d20da-192">Met behulp van een webhook</span><span class="sxs-lookup"><span data-stu-id="d20da-192">Using a webhook</span></span>
<span data-ttu-id="d20da-193">toouse een webhook nadat deze is gemaakt, de clienttoepassing moet een HTTP POST met Hallo-URL voor Hallo webhook verlenen.</span><span class="sxs-lookup"><span data-stu-id="d20da-193">toouse a webhook after it has been created, your client application must issue an HTTP POST with hello URL for hello webhook.</span></span>  <span data-ttu-id="d20da-194">Hallo syntaxis van de webhook Hallo zal Hallo na indeling zijn.</span><span class="sxs-lookup"><span data-stu-id="d20da-194">hello syntax of hello webhook will be in hello following format.</span></span>

    http://<Webhook Server>/token?=<Token Value>

<span data-ttu-id="d20da-195">Hallo client ontvangt een Hallo volgende retourcodes uit Hallo POST-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="d20da-195">hello client will receive one of hello following return codes from hello POST request.</span></span>  

| <span data-ttu-id="d20da-196">Code</span><span class="sxs-lookup"><span data-stu-id="d20da-196">Code</span></span> | <span data-ttu-id="d20da-197">Tekst</span><span class="sxs-lookup"><span data-stu-id="d20da-197">Text</span></span> | <span data-ttu-id="d20da-198">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="d20da-198">Description</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="d20da-199">202</span><span class="sxs-lookup"><span data-stu-id="d20da-199">202</span></span> |<span data-ttu-id="d20da-200">Geaccepteerd</span><span class="sxs-lookup"><span data-stu-id="d20da-200">Accepted</span></span> |<span data-ttu-id="d20da-201">Hallo-aanvraag is geaccepteerd en Hallo runbook is in de wachtrij geplaatst.</span><span class="sxs-lookup"><span data-stu-id="d20da-201">hello request was accepted, and hello runbook was successfully queued.</span></span> |
| <span data-ttu-id="d20da-202">400</span><span class="sxs-lookup"><span data-stu-id="d20da-202">400</span></span> |<span data-ttu-id="d20da-203">Onjuiste aanvraag</span><span class="sxs-lookup"><span data-stu-id="d20da-203">Bad Request</span></span> |<span data-ttu-id="d20da-204">Hallo-aanvraag is niet geaccepteerd voor een van de volgende redenen Hallo.</span><span class="sxs-lookup"><span data-stu-id="d20da-204">hello request was not accepted for one of hello following reasons.</span></span> <ul> <li><span data-ttu-id="d20da-205">Hallo webhook is verlopen.</span><span class="sxs-lookup"><span data-stu-id="d20da-205">hello webhook has expired.</span></span></li> <li><span data-ttu-id="d20da-206">Hallo webhook is uitgeschakeld.</span><span class="sxs-lookup"><span data-stu-id="d20da-206">hello webhook is disabled.</span></span></li> <li><span data-ttu-id="d20da-207">Hallo-token in Hallo-URL is ongeldig.</span><span class="sxs-lookup"><span data-stu-id="d20da-207">hello token in hello URL is invalid.</span></span></li>  </ul> |
| <span data-ttu-id="d20da-208">404</span><span class="sxs-lookup"><span data-stu-id="d20da-208">404</span></span> |<span data-ttu-id="d20da-209">Niet gevonden</span><span class="sxs-lookup"><span data-stu-id="d20da-209">Not Found</span></span> |<span data-ttu-id="d20da-210">Hallo-aanvraag is niet geaccepteerd voor een van de volgende redenen Hallo.</span><span class="sxs-lookup"><span data-stu-id="d20da-210">hello request was not accepted for one of hello following reasons.</span></span> <ul> <li><span data-ttu-id="d20da-211">Hallo webhook is niet gevonden.</span><span class="sxs-lookup"><span data-stu-id="d20da-211">hello webhook was not found.</span></span></li> <li><span data-ttu-id="d20da-212">Hallo runbook is niet gevonden.</span><span class="sxs-lookup"><span data-stu-id="d20da-212">hello runbook was not found.</span></span></li> <li><span data-ttu-id="d20da-213">Hallo-account is niet gevonden.</span><span class="sxs-lookup"><span data-stu-id="d20da-213">hello account was not found.</span></span></li>  </ul> |
| <span data-ttu-id="d20da-214">500</span><span class="sxs-lookup"><span data-stu-id="d20da-214">500</span></span> |<span data-ttu-id="d20da-215">Interne serverfout</span><span class="sxs-lookup"><span data-stu-id="d20da-215">Internal Server Error</span></span> |<span data-ttu-id="d20da-216">Hallo-URL is geldig, maar er is een fout opgetreden.</span><span class="sxs-lookup"><span data-stu-id="d20da-216">hello URL was valid, but an error occurred.</span></span>  <span data-ttu-id="d20da-217">Verzend Hallo-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="d20da-217">Please resubmit hello request.</span></span> |

<span data-ttu-id="d20da-218">Ervan uitgaande dat Hallo-aanvraag is gelukt, bevat antwoord van de webhook Hallo Hallo taak-id in JSON-indeling als volgt.</span><span class="sxs-lookup"><span data-stu-id="d20da-218">Assuming hello request is successful, hello webhook response contains hello job id in JSON format as follows.</span></span> <span data-ttu-id="d20da-219">Bevat een enkele taak-id, maar Hallo JSON-indeling kunt u mogelijke toekomstige verbeteringen.</span><span class="sxs-lookup"><span data-stu-id="d20da-219">It will contain a single job id, but hello JSON format allows for potential future enhancements.</span></span>

    {"JobIds":["<JobId>"]}  

<span data-ttu-id="d20da-220">Hallo-client kan niet bepalen wanneer Hallo runbooktaak is voltooid of de eindstatus van Hallo webhook.</span><span class="sxs-lookup"><span data-stu-id="d20da-220">hello client cannot determine when hello runbook job completes or its completion status from hello webhook.</span></span>  <span data-ttu-id="d20da-221">Dit kan bepalen dat deze informatie met taak-id Hallo met een andere methode, zoals [Windows PowerShell](http://msdn.microsoft.com/library/azure/dn690263.aspx) of Hallo [Azure Automation-API](https://msdn.microsoft.com/library/azure/mt163826.aspx).</span><span class="sxs-lookup"><span data-stu-id="d20da-221">It can determine this information using hello job id with another method such as [Windows PowerShell](http://msdn.microsoft.com/library/azure/dn690263.aspx) or hello [Azure Automation API](https://msdn.microsoft.com/library/azure/mt163826.aspx).</span></span>

### <a name="example"></a><span data-ttu-id="d20da-222">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="d20da-222">Example</span></span>
<span data-ttu-id="d20da-223">Hallo volgende voorbeeld maakt gebruik van Windows PowerShell toostart een runbook met een webhook.</span><span class="sxs-lookup"><span data-stu-id="d20da-223">hello following example uses Windows PowerShell toostart a runbook with a webhook.</span></span>  <span data-ttu-id="d20da-224">Houd er rekening mee dat elke taal die u van een HTTP-aanvraag maken kunt een webhook; kunt gebruiken Windows PowerShell wordt alleen gebruikt als voorbeeld hier.</span><span class="sxs-lookup"><span data-stu-id="d20da-224">Note that any language that can make an HTTP request can use a webhook; Windows PowerShell is just used here as an example.</span></span>

<span data-ttu-id="d20da-225">Hallo runbook is een lijst met virtuele machines die zijn opgemaakt in JSON in Hallo hoofdtekst van Hallo-aanvraag verwacht.</span><span class="sxs-lookup"><span data-stu-id="d20da-225">hello runbook is expecting a list of virtual machines formatted in JSON in hello body of hello request.</span></span> <span data-ttu-id="d20da-226">We zijn informatie over die wordt gestart Hallo runbook en Hallo datum en tijd wordt gestart in de header van Hallo aanvraag Hallo ook inclusief.</span><span class="sxs-lookup"><span data-stu-id="d20da-226">We also are including information about who is starting hello runbook and hello date and time it is being started in hello header of hello request.</span></span>      

    $uri = "https://s1events.azure-automation.net/webhooks?token=8ud0dSrSo%2fvHWpYbklW%3c8s0GrOKJZ9Nr7zqcS%2bIQr4c%3d"
    $headers = @{"From"="user@contoso.com";"Date"="05/28/2015 15:47:00"}

    $vms  = @(
                @{ Name="vm01";ServiceName="vm01"},
                @{ Name="vm02";ServiceName="vm02"}
            )
    $body = ConvertTo-Json -InputObject $vms

    $response = Invoke-RestMethod -Method Post -Uri $uri -Headers $headers -Body $body
    $jobid = ConvertFrom-Json $response


<span data-ttu-id="d20da-227">Hallo volgende afbeelding ziet u headerinformatie hello (met behulp van een [Fiddler](http://www.telerik.com/fiddler) trace) van deze aanvraag.</span><span class="sxs-lookup"><span data-stu-id="d20da-227">hello following image shows hello header information (using a [Fiddler](http://www.telerik.com/fiddler) trace) from this request.</span></span> <span data-ttu-id="d20da-228">Dit omvat standaard een HTTP-aanvraag-headers in toevoeging toohello aangepaste datum en van de headers die we hebben toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="d20da-228">This includes standard headers of an HTTP request in addition toohello custom Date and From headers that we added.</span></span>  <span data-ttu-id="d20da-229">Elk van deze waarden is beschikbaar toohello runbook in Hallo **RequestHeaders** eigenschap van **WebhookData**.</span><span class="sxs-lookup"><span data-stu-id="d20da-229">Each of these values is available toohello runbook in hello **RequestHeaders** property of **WebhookData**.</span></span>

![Knop webhooks.](media/automation-webhooks/webhook-request-headers.png)

<span data-ttu-id="d20da-231">Hallo volgende afbeelding toont Hallo hoofdtekst van Hallo-aanvraag (met behulp van een [Fiddler](http://www.telerik.com/fiddler) trace) die beschikbaar toohello runbook in Hallo **RequestBody** eigenschap van **WebhookData**.</span><span class="sxs-lookup"><span data-stu-id="d20da-231">hello following image shows hello body of hello request (using a [Fiddler](http://www.telerik.com/fiddler) trace)  that is available toohello runbook in hello **RequestBody** property of **WebhookData**.</span></span> <span data-ttu-id="d20da-232">Dit is opgemaakt als JSON omdat die was Hallo-indeling die is opgenomen in de hoofdtekst Hallo van Hallo-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="d20da-232">This is formatted as JSON because that was hello format that was included in hello body of hello request.</span></span>     

![Knop webhooks.](media/automation-webhooks/webhook-request-body.png)

<span data-ttu-id="d20da-234">Hallo toont volgende afbeelding worden verzonden vanaf de Windows PowerShell en de resulterende antwoord Hallo Hallo-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="d20da-234">hello following image shows hello request being sent from Windows PowerShell and hello resulting response.</span></span>  <span data-ttu-id="d20da-235">Hallo-taak-id is opgehaald uit het antwoord Hallo en geconverteerde tooa tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="d20da-235">hello job id is extracted from hello response and converted tooa string.</span></span>

![Knop webhooks.](media/automation-webhooks/webhook-request-response.png)

<span data-ttu-id="d20da-237">Hallo volgende voorbeeldrunbook accepteert van het vorige voorbeeldaanvraag Hallo en Hallo virtuele machines is opgegeven in de aanvraagtekst hello wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="d20da-237">hello following sample runbook accepts hello previous example request and starts hello virtual machines specified in hello request body.</span></span>

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

            # Authenticate tooAzure resources
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
            Write-Error "Runbook mean toobe started only from webhook."
        }
    }


## <a name="starting-runbooks-in-response-tooazure-alerts"></a><span data-ttu-id="d20da-238">Starten van runbooks in antwoord tooAzure waarschuwingen</span><span class="sxs-lookup"><span data-stu-id="d20da-238">Starting runbooks in response tooAzure alerts</span></span>
<span data-ttu-id="d20da-239">Webhook ingeschakeld runbooks kunnen worden gebruikt tooreact te[waarschuwingen van Azure](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="d20da-239">Webhook-enabled runbooks can be used tooreact too[Azure alerts](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span></span> <span data-ttu-id="d20da-240">Bronnen in Azure worden gecontroleerd door het verzamelen van statistieken Hallo zoals prestaties, beschikbaarheid en gebruik met Hallo hulp van waarschuwingen van Azure.</span><span class="sxs-lookup"><span data-stu-id="d20da-240">Resources in Azure can be monitored by collecting hello statistics like performance, availability and usage with hello help of Azure alerts.</span></span> <span data-ttu-id="d20da-241">U kunt een waarschuwing op basis van de bewaking van metrische gegevens ontvangen of gebeurtenissen voor uw Azure-resources, momenteel Automation-Accounts ondersteunen alleen metrische gegevens.</span><span class="sxs-lookup"><span data-stu-id="d20da-241">You can receive an alert based on monitoring metrics or events for your Azure resources, currently Automation Accounts support only metrics.</span></span> <span data-ttu-id="d20da-242">Als het Hallo-waarde van een opgegeven metriek overschrijdt Hallo drempelwaarde toegewezen of als Hallo geconfigureerd gebeurtenis wordt geactiveerd en vervolgens een melding wordt verzonden toohello service beheerder of co-beheerders tooresolve Hallo waarschuwing voor meer informatie over metrische gegevens en gebeurtenissen Raadpleeg te[ Waarschuwingen van Azure](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="d20da-242">When hello value of a specified metric exceeds hello threshold assigned or if hello configured event is triggered then a notification is sent toohello service admin or co-admins tooresolve hello alert, for more information on metrics and events please refer too[Azure alerts](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span></span>

<span data-ttu-id="d20da-243">Naast het gebruik van waarschuwingen van Azure als een waarschuwingssysteem, kunt u ook ere van runbooks in het antwoord tooalerts.</span><span class="sxs-lookup"><span data-stu-id="d20da-243">Besides using Azure alerts as a notification system, you can also kick off runbooks in response tooalerts.</span></span> <span data-ttu-id="d20da-244">Azure Automation biedt Hallo mogelijkheid toorun webhook ingeschakeld runbooks met waarschuwingen van Azure.</span><span class="sxs-lookup"><span data-stu-id="d20da-244">Azure Automation provides hello capability toorun webhook-enabled runbooks with Azure alerts.</span></span> <span data-ttu-id="d20da-245">Wanneer een waarde groter is dan geconfigureerd Hallo drempelwaarde Hallo waarschuwingsregel actief en triggers Hallo automation-webhook die op zijn beurt Hallo runbook worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="d20da-245">When a metric exceeds hello configured threshold value then hello alert rule becomes active and triggers hello automation webhook which in turn executes hello runbook.</span></span>

![Webhooks.](media/automation-webhooks/webhook-alert.jpg)

### <a name="alert-context"></a><span data-ttu-id="d20da-247">Waarschuwingscontext</span><span class="sxs-lookup"><span data-stu-id="d20da-247">Alert context</span></span>
<span data-ttu-id="d20da-248">Houd rekening met een Azure-resource zoals een virtuele machine, CPU-gebruik van deze machine is een van de Hallo prestatie metriek.</span><span class="sxs-lookup"><span data-stu-id="d20da-248">Consider an Azure resource such as a virtual machine, CPU utilization of this machine is one of hello key performance metric.</span></span> <span data-ttu-id="d20da-249">Als Hallo CPU-gebruik is 100% of meer dan een bepaald bedrag gedurende lange tijd weergegeven, kunt u toorestart Hallo virtuele machine toofix Hallo probleem.</span><span class="sxs-lookup"><span data-stu-id="d20da-249">If hello CPU utilization is 100% or more than a certain amount for long period of time, you might want toorestart hello virtual machine toofix hello problem.</span></span> <span data-ttu-id="d20da-250">Dit kan worden opgelost door een virtuele machine van de waarschuwingsregel toohello configureren en deze regel gaat CPU-percentage als de metriek.</span><span class="sxs-lookup"><span data-stu-id="d20da-250">This can be solved by configuring an alert rule toohello virtual machine and this rule takes CPU percentage as its metric.</span></span> <span data-ttu-id="d20da-251">Hier CPU-percentage wordt alleen gemaakt als voorbeeld, maar er zijn veel andere metrische gegevens kunt u tooyour Azure configureren bronnen en opnieuw starten Hallo virtuele machine is een actie die is genomen toofix dit probleem, kunt u Hallo runbook tootake andere acties configureren.</span><span class="sxs-lookup"><span data-stu-id="d20da-251">CPU percentage here is just taken as an example but there are many other metrics that you can configure tooyour Azure resources and restarting hello virtual machine is an action that is taken toofix this issue, you can configure hello runbook tootake other actions.</span></span>

<span data-ttu-id="d20da-252">Wanneer deze waarschuwingsregel Hallo actief en triggers Hallo runbook webhook is ingeschakeld, verzendt het Hallo waarschuwingscontext toohello runbook.</span><span class="sxs-lookup"><span data-stu-id="d20da-252">When this hello alert rule becomes active and triggers hello webhook-enabled runbook, it sends hello alert context toohello runbook.</span></span> <span data-ttu-id="d20da-253">[Waarschuwingscontext](../monitoring-and-diagnostics/insights-receive-alert-notifications.md) bevat details, zoals **SubscriptionID**, **ResourceGroupName**, **ResourceName**, **ResourceType**, **ResourceId** en **tijdstempel** die zijn vereist voor Hallo runbook tooidentify Hallo resource waarop deze actie duurt.</span><span class="sxs-lookup"><span data-stu-id="d20da-253">[Alert context](../monitoring-and-diagnostics/insights-receive-alert-notifications.md) contains details including **SubscriptionID**, **ResourceGroupName**, **ResourceName**, **ResourceType**, **ResourceId** and **Timestamp** which are required for hello runbook tooidentify hello resource on which it will be taking action.</span></span> <span data-ttu-id="d20da-254">Waarschuwing context is ingesloten in het hoofddeel Hallo Hallo **WebhookData** verzonden toohello runbook object en kan worden gebruikt met **Webhook.RequestBody** eigenschap</span><span class="sxs-lookup"><span data-stu-id="d20da-254">Alert context is embedded in hello body part of hello **WebhookData** object sent toohello runbook and it can be accessed with **Webhook.RequestBody** property</span></span>

### <a name="example"></a><span data-ttu-id="d20da-255">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="d20da-255">Example</span></span>
<span data-ttu-id="d20da-256">Maken van een virtuele machine van Azure in uw abonnement en koppelen aan een [toomonitor CPU-percentage metriek waarschuwing](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="d20da-256">Create an Azure virtual machine in your subscription and associate an [alert toomonitor CPU percentage metric](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span></span> <span data-ttu-id="d20da-257">Zorg dat u Hallo webhook veld met de Hallo-URL van Hallo webhook die is gegenereerd tijdens het maken van de webhook Hallo vullen tijdens het maken van Hallo waarschuwing.</span><span class="sxs-lookup"><span data-stu-id="d20da-257">While creating hello alert make sure you populate hello webhook field with hello URL of hello webhook which was generated while creating hello webhook.</span></span>

<span data-ttu-id="d20da-258">Hallo wordt volgende voorbeeldrunbook geactiveerd wanneer de waarschuwingsregel Hallo actief en Hallo waarschuwingscontext parameters die zijn vereist voor Hallo runbook tooidentify Hallo resource waarop deze actie te worden verzameld.</span><span class="sxs-lookup"><span data-stu-id="d20da-258">hello following sample runbook is triggered when hello alert rule becomes active and it collects hello Alert context parameters which are required for hello runbook tooidentify hello resource on which it will be taking action.</span></span>

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

            # Outputs information on hello webhook name that called This
            Write-Output "This runbook was started from webhook $WebhookName."


            # Obtain hello WebhookBody containing hello AlertContext
            $WebhookBody = (ConvertFrom-Json -InputObject $WebhookBody)
            Write-Output "`nWEBHOOK BODY"
            Write-Output "============="
            Write-Output $WebhookBody

            # Obtain hello AlertContext     
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

            # Act on hello AlertContext data, in our case restarting hello VM.
            # Authenticate tooyour Azure subscription using Organization ID toobe able toorestart that Virtual Machine.
            $cred = Get-AutomationPSCredential -Name "MyAzureCredential"
            Add-AzureAccount -Credential $cred
            Select-AzureSubscription -subscriptionName "Visual Studio Ultimate with MSDN"

            #Check hello status property of hello VM
            Write-Output "Status of VM before taking action"
            Get-AzureVM -Name $AlertContext.resourceName -ServiceName $AlertContext.resourceName
            Write-Output "Restarting VM"

            # Restart hello VM by passing VM name and Service name which are same in this case
            Restart-AzureVM -ServiceName $AlertContext.resourceName -Name $AlertContext.resourceName
            Write-Output "Status of VM after alert is active and takes action"
            Get-AzureVM -Name $AlertContext.resourceName -ServiceName $AlertContext.resourceName
        }
        else  
        {
            Write-Error "This runbook is meant tooonly be started from a webhook."  
        }  
    }



## <a name="next-steps"></a><span data-ttu-id="d20da-259">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="d20da-259">Next steps</span></span>
* <span data-ttu-id="d20da-260">Zie voor meer informatie op verschillende manieren toostart een runbook [een Runbook starten](automation-starting-a-runbook.md).</span><span class="sxs-lookup"><span data-stu-id="d20da-260">For details on different ways toostart a runbook, see [Starting a Runbook](automation-starting-a-runbook.md).</span></span>
* <span data-ttu-id="d20da-261">Voor informatie over Hallo weer te geven de Status van een Runbook-Job, Raadpleeg te[uitvoeren van Runbook in Azure Automation](automation-runbook-execution.md).</span><span class="sxs-lookup"><span data-stu-id="d20da-261">For information on viewing hello Status of a Runbook Job, refer too[Runbook execution in Azure Automation](automation-runbook-execution.md).</span></span>
* <span data-ttu-id="d20da-262">hoe toouse Azure Automation tootake actie op Azure-waarschuwingen zien toolearn [Azure VM-waarschuwingen oplossen met Automation-Runbooks](automation-azure-vm-alert-integration.md).</span><span class="sxs-lookup"><span data-stu-id="d20da-262">toolearn how toouse Azure Automation tootake action on Azure Alerts, see [Remediate Azure VM Alerts with Automation Runbooks](automation-azure-vm-alert-integration.md).</span></span>

---
title: gebeurtenissen voor Azure Event raster aaaCustom | Microsoft Docs
description: Gebruik Azure gebeurtenis raster toopublish een onderwerp en toothat gebeurtenis abonneren.
services: event-grid
keywords: 
author: djrosanova
ms.author: darosa
ms.date: 08/15/2017
ms.topic: hero-article
ms.service: event-grid
ms.openlocfilehash: 5055df1c970b043cadf06978a076f7f5c83501cd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-route-custom-events-with-azure-event-grid"></a><span data-ttu-id="c2e04-103">Aangepaste gebeurtenissen maken en routeren met behulp van Azure Event Grid</span><span class="sxs-lookup"><span data-stu-id="c2e04-103">Create and route custom events with Azure Event Grid</span></span>

<span data-ttu-id="c2e04-104">Azure Event raster is een gebeurtenisservice voor Hallo cloud.</span><span class="sxs-lookup"><span data-stu-id="c2e04-104">Azure Event Grid is an eventing service for hello cloud.</span></span> <span data-ttu-id="c2e04-105">In dit artikel gebruiken hello Azure CLI toocreate een eigen onderwerp, toohello onderwerp abonneren en Hallo gebeurtenis tooview Hallo resultaat activeren.</span><span class="sxs-lookup"><span data-stu-id="c2e04-105">In this article, you use hello Azure CLI toocreate a custom topic, subscribe toohello topic, and trigger hello event tooview hello result.</span></span> <span data-ttu-id="c2e04-106">Normaal gesproken verzendt u gebeurtenissen tooan eindpunt dat toohello gebeurtenis, zoals een webhook of een Azure-functie reageert.</span><span class="sxs-lookup"><span data-stu-id="c2e04-106">Typically, you send events tooan endpoint that responds toohello event, such as, a webhook or Azure Function.</span></span> <span data-ttu-id="c2e04-107">Toosimplify dit artikel, u Hallo gebeurtenissen tooa URL die alleen Hallo-berichten verzamelt verzenden.</span><span class="sxs-lookup"><span data-stu-id="c2e04-107">However, toosimplify this article, you send hello events tooa URL that merely collects hello messages.</span></span> <span data-ttu-id="c2e04-108">U maakt deze URL met behulp van een open source-hulpprogramma van derden, met de naam [RequestBin](https://requestb.in/).</span><span class="sxs-lookup"><span data-stu-id="c2e04-108">You create this URL by using an open source, third-party tool called [RequestBin](https://requestb.in/).</span></span>

>[!NOTE]
><span data-ttu-id="c2e04-109">**RequestBin** is een open source-hulpprogramma dat niet is bedoeld voor gebruik met een hoge doorvoer.</span><span class="sxs-lookup"><span data-stu-id="c2e04-109">**RequestBin** is an open source tool that is not intended for high throughput usage.</span></span> <span data-ttu-id="c2e04-110">Hallo-gebruik van Hallo hulpprogramma hier is puur demonstrative.</span><span class="sxs-lookup"><span data-stu-id="c2e04-110">hello use of hello tool here is purely demonstrative.</span></span> <span data-ttu-id="c2e04-111">Als u meer dan een gebeurtenis op een tijdstip pushen, ziet u mogelijk niet alle gebeurtenissen in Hallo-hulpprogramma.</span><span class="sxs-lookup"><span data-stu-id="c2e04-111">If you push more than one event at a time, you might not see all of your events in hello tool.</span></span>

<span data-ttu-id="c2e04-112">Wanneer u klaar bent, ziet u dat Hallo gebeurtenisgegevens tooan eindpunt is verzonden.</span><span class="sxs-lookup"><span data-stu-id="c2e04-112">When you are finished, you see that hello event data has been sent tooan endpoint.</span></span>

![Gebeurtenisgegevens](./media/custom-event-quickstart/request-result.png)

[!INCLUDE [quickstarts-free-trial-note.md](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="c2e04-114">Als u tooinstall kiest en Hallo CLI lokaal gebruiken, in dit artikel is vereist dat u altijd de meest recente versie Hallo van Azure CLI (2.0.14 of hoger).</span><span class="sxs-lookup"><span data-stu-id="c2e04-114">If you choose tooinstall and use hello CLI locally, this article requires that you are running hello latest version of Azure CLI (2.0.14 or later).</span></span> <span data-ttu-id="c2e04-115">toofind hello versie, voer `az --version`.</span><span class="sxs-lookup"><span data-stu-id="c2e04-115">toofind hello version, run `az --version`.</span></span> <span data-ttu-id="c2e04-116">Als u tooinstall of upgrade nodig hebt, raadpleegt u [2.0 voor Azure CLI installeren](/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="c2e04-116">If you need tooinstall or upgrade, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli).</span></span>

## <a name="create-a-resource-group"></a><span data-ttu-id="c2e04-117">Een resourcegroep maken</span><span class="sxs-lookup"><span data-stu-id="c2e04-117">Create a resource group</span></span>

<span data-ttu-id="c2e04-118">Event Grid-onderwerpen zijn Azure-resources en moeten in een Azure-resourcegroep worden geplaatst.</span><span class="sxs-lookup"><span data-stu-id="c2e04-118">Event Grid topics are Azure resources, and must be placed in an Azure resource group.</span></span> <span data-ttu-id="c2e04-119">Hallo-resourcegroep is een logische verzameling in welke Azure resources worden geïmplementeerd en beheerd.</span><span class="sxs-lookup"><span data-stu-id="c2e04-119">hello resource group is a logical collection into which Azure resources are deployed and managed.</span></span>

<span data-ttu-id="c2e04-120">Een resourcegroep maken met de Hallo [az groep maken](/cli/azure/group#create) opdracht.</span><span class="sxs-lookup"><span data-stu-id="c2e04-120">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span> 

<span data-ttu-id="c2e04-121">Hallo volgende voorbeeld maakt u een resourcegroep met de naam *gridResourceGroup* in Hallo *westus2* locatie.</span><span class="sxs-lookup"><span data-stu-id="c2e04-121">hello following example creates a resource group named *gridResourceGroup* in hello *westus2* location.</span></span>

```azurecli-interactive
az group create --name gridResourceGroup --location westus2
```

## <a name="create-a-custom-topic"></a><span data-ttu-id="c2e04-122">Een aangepast onderwerp maken</span><span class="sxs-lookup"><span data-stu-id="c2e04-122">Create a custom topic</span></span>

<span data-ttu-id="c2e04-123">Een onderwerp biedt een door de gebruiker gedefinieerd eindpunt waarop u de gebeurtenissen kunt posten.</span><span class="sxs-lookup"><span data-stu-id="c2e04-123">A topic provides a user-defined endpoint that you post your events to.</span></span> <span data-ttu-id="c2e04-124">Hallo maakt volgende voorbeeld Hallo onderwerp in de resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="c2e04-124">hello following example creates hello topic in your resource group.</span></span> <span data-ttu-id="c2e04-125">Vervang `<topic_name>` door een unieke naam voor het onderwerp.</span><span class="sxs-lookup"><span data-stu-id="c2e04-125">Replace `<topic_name>` with a unique name for your topic.</span></span> <span data-ttu-id="c2e04-126">Hallo onderwerp de naam moet uniek zijn omdat deze wordt vertegenwoordigd door een DNS-vermelding.</span><span class="sxs-lookup"><span data-stu-id="c2e04-126">hello topic name must be unique because it is represented by a DNS entry.</span></span> <span data-ttu-id="c2e04-127">Voor de preview-versie Hallo gebeurtenis raster ondersteunt **westus2** en **westcentralus** locaties.</span><span class="sxs-lookup"><span data-stu-id="c2e04-127">For hello preview release, Event Grid supports **westus2** and **westcentralus** locations.</span></span>

```azurecli-interactive
az eventgrid topic create --name <topic_name> -l westus2 -g gridResourceGroup
```

## <a name="create-a-message-endpoint"></a><span data-ttu-id="c2e04-128">Het eindpunt van een bericht maken</span><span class="sxs-lookup"><span data-stu-id="c2e04-128">Create a message endpoint</span></span>

<span data-ttu-id="c2e04-129">Voordat u zich abonneert toohello onderwerp, gaan we maken Hallo-eindpunt voor de gebeurtenis het Hallo-bericht.</span><span class="sxs-lookup"><span data-stu-id="c2e04-129">Before subscribing toohello topic, let's create hello endpoint for hello event message.</span></span> <span data-ttu-id="c2e04-130">In plaats van schrijven van code toorespond toohello gebeurtenis, maken we een eindpunt dat Hallo-berichten worden verzameld zodat u ze kunt weergeven.</span><span class="sxs-lookup"><span data-stu-id="c2e04-130">Rather than write code toorespond toohello event, let's create an endpoint that collects hello messages so you can view them.</span></span> <span data-ttu-id="c2e04-131">RequestBin is een open-source hulpprogramma van derden waarmee u een eindpunt toocreate en aanvragen weergeven die tooit worden verzonden.</span><span class="sxs-lookup"><span data-stu-id="c2e04-131">RequestBin is an open source, third-party tool that enables you toocreate an endpoint, and view requests that are sent tooit.</span></span> <span data-ttu-id="c2e04-132">Ga te[RequestBin](https://requestb.in/), en klik op **maken van een RequestBin**.</span><span class="sxs-lookup"><span data-stu-id="c2e04-132">Go too[RequestBin](https://requestb.in/), and click **Create a RequestBin**.</span></span>  <span data-ttu-id="c2e04-133">Kopieer de URL van Hallo-opslaglocatie, omdat u deze nodig hebt wanneer u zich abonneert toohello onderwerp.</span><span class="sxs-lookup"><span data-stu-id="c2e04-133">Copy hello bin URL, because you need it when subscribing toohello topic.</span></span>

## <a name="subscribe-tooa-topic"></a><span data-ttu-id="c2e04-134">Abonneren tooa onderwerp</span><span class="sxs-lookup"><span data-stu-id="c2e04-134">Subscribe tooa topic</span></span>

<span data-ttu-id="c2e04-135">U zich hebt geabonneerd tooa onderwerp tootell gebeurtenis raster welke gebeurtenissen u wilt dat tootrack.</span><span class="sxs-lookup"><span data-stu-id="c2e04-135">You subscribe tooa topic tootell Event Grid which events you want tootrack.</span></span> <span data-ttu-id="c2e04-136">Hallo volgende voorbeeld is geabonneerd toohello onderwerp hebt gemaakt Hallo-URL van RequestBin als Hallo-eindpunt voor gebeurtenismelding doorgegeven.</span><span class="sxs-lookup"><span data-stu-id="c2e04-136">hello following example subscribes toohello topic you created, and passes hello URL from RequestBin as hello endpoint for event notification.</span></span> <span data-ttu-id="c2e04-137">Vervang `<event_subscription_name>` met een unieke naam voor uw abonnement en `<URL_from_RequestBin>` Hallo waarde uit de voorgaande sectie Hallo.</span><span class="sxs-lookup"><span data-stu-id="c2e04-137">Replace `<event_subscription_name>` with a unique name for your subscription, and `<URL_from_RequestBin>` with hello value from hello preceding section.</span></span> <span data-ttu-id="c2e04-138">Als u zich abonneert, kunt u een eindpunt opgeeft, verwerkt gebeurtenis raster Hallo routering van gebeurtenissen toothat eindpunt.</span><span class="sxs-lookup"><span data-stu-id="c2e04-138">By specifying an endpoint when subscribing, Event Grid handles hello routing of events toothat endpoint.</span></span> <span data-ttu-id="c2e04-139">Voor `<topic_name>`, gebruik Hallo-waarde die u eerder hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="c2e04-139">For `<topic_name>`, use hello value you created earlier.</span></span> 

```azurecli-interactive
az eventgrid topic event-subscription create --name <event_subscription_name> \
  --endpoint <URL_from_RequestBin> \
  -g gridResourceGroup \
  --topic-name <topic_name>
```

## <a name="send-an-event-tooyour-topic"></a><span data-ttu-id="c2e04-140">Een gebeurtenis tooyour onderwerp verzenden</span><span class="sxs-lookup"><span data-stu-id="c2e04-140">Send an event tooyour topic</span></span>

<span data-ttu-id="c2e04-141">Nu gaan we een gebeurtenis toosee activeren hoe gebeurtenis raster Hallo-bericht tooyour eindpunt distribueert.</span><span class="sxs-lookup"><span data-stu-id="c2e04-141">Now, let's trigger an event toosee how Event Grid distributes hello message tooyour endpoint.</span></span> <span data-ttu-id="c2e04-142">Eerst laten we Hallo-URL ophalen en de sleutel voor Hallo onderwerp.</span><span class="sxs-lookup"><span data-stu-id="c2e04-142">First, let's get hello URL and key for hello topic.</span></span> <span data-ttu-id="c2e04-143">Gebruik opnieuw de onderwerpnaam voor `<topic_name>`.</span><span class="sxs-lookup"><span data-stu-id="c2e04-143">Again, use your topic name for `<topic_name>`.</span></span>

```azurecli-interactive
endpoint=$(az eventgrid topic show --name <topic_name> -g gridResourceGroup --query "endpoint" --output tsv)
key=$(az eventgrid topic key list --name <topic_name> -g gridResourceGroup --query "key1" --output tsv)
```

<span data-ttu-id="c2e04-144">toosimplify in dit artikel we een voorbeeld gebeurtenis gegevens toosend toohello onderwerp hebt ingesteld.</span><span class="sxs-lookup"><span data-stu-id="c2e04-144">toosimplify this article, we have set up sample event data toosend toohello topic.</span></span> <span data-ttu-id="c2e04-145">Een toepassing of service van Azure wilt verzenden doorgaans Hallo gebeurtenisgegevens.</span><span class="sxs-lookup"><span data-stu-id="c2e04-145">Typically, an application or Azure service would send hello event data.</span></span> <span data-ttu-id="c2e04-146">Hallo volgt opgehaald Hallo gebeurtenisgegevens:</span><span class="sxs-lookup"><span data-stu-id="c2e04-146">hello following example gets hello event data:</span></span>

```azurecli-interactive
body=$(eval echo "'$(curl https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/event-grid/customevent.json)'")
```

<span data-ttu-id="c2e04-147">Als u `echo "$body"` ziet u de volledige gebeurtenis Hallo.</span><span class="sxs-lookup"><span data-stu-id="c2e04-147">If you `echo "$body"` you can see hello full event.</span></span> <span data-ttu-id="c2e04-148">Hallo `data` Hallo JSON-element is Hallo nettolading van de gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="c2e04-148">hello `data` element of hello JSON is hello payload of your event.</span></span> <span data-ttu-id="c2e04-149">Elke juist opgemaakte JSON kan in dit veld worden ingevoerd.</span><span class="sxs-lookup"><span data-stu-id="c2e04-149">Any well-formed JSON can go in this field.</span></span> <span data-ttu-id="c2e04-150">U kunt ook het veld onderwerp hello gebruiken voor geavanceerde routering en filteren.</span><span class="sxs-lookup"><span data-stu-id="c2e04-150">You can also use hello subject field for advanced routing and filtering.</span></span>

<span data-ttu-id="c2e04-151">CURL is een hulpprogramma waarmee HTTP-aanvragen worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="c2e04-151">CURL is a utility that performs HTTP requests.</span></span> <span data-ttu-id="c2e04-152">In dit artikel gebruiken we CURL toosend Hallo gebeurtenis tooour onderwerp.</span><span class="sxs-lookup"><span data-stu-id="c2e04-152">In this article, we use CURL toosend hello event tooour topic.</span></span> 

```azurecli-interactive
curl -X POST -H "aeg-sas-key: $key" -d "$body" $endpoint
```

<span data-ttu-id="c2e04-153">U hebt Hallo-gebeurtenis geactiveerd en gebeurtenis raster Hallo-bericht toohello eindpunt die u geconfigureerd wanneer u zich abonneert verzonden.</span><span class="sxs-lookup"><span data-stu-id="c2e04-153">You have triggered hello event, and Event Grid sent hello message toohello endpoint you configured when subscribing.</span></span> <span data-ttu-id="c2e04-154">Blader toohello RequestBin-URL die u eerder hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="c2e04-154">Browse toohello RequestBin URL that you created earlier.</span></span> <span data-ttu-id="c2e04-155">Of klik in het geopende RequestBin-browservenster op Vernieuwen.</span><span class="sxs-lookup"><span data-stu-id="c2e04-155">Or, click refresh in your open RequestBin browser.</span></span> <span data-ttu-id="c2e04-156">U ziet Hallo-gebeurtenis die u zojuist hebt verzonden.</span><span class="sxs-lookup"><span data-stu-id="c2e04-156">You see hello event you just sent.</span></span> 

```json
[{
  "id": "1807",
  "eventType": "recordInserted",
  "subject": "myapp/vehicles/motorcycles",
  "eventTime": "2017-08-10T21:03:07+00:00",
  "data": {
    "make": "Ducati",
    "model": "Monster"
  },
  "topic": "/subscriptions/{subscription-id}/resourceGroups/{resource-group}/providers/Microsoft.EventGrid/topics/{topic}"
}]
```

## <a name="clean-up-resources"></a><span data-ttu-id="c2e04-157">Resources opschonen</span><span class="sxs-lookup"><span data-stu-id="c2e04-157">Clean up resources</span></span>
<span data-ttu-id="c2e04-158">Als u van plan toocontinue werken met deze gebeurtenis bent, gaat u als Hallo-resources die zijn gemaakt in dit artikel niet opruimen.</span><span class="sxs-lookup"><span data-stu-id="c2e04-158">If you plan toocontinue working with this event, do not clean up hello resources created in this article.</span></span> <span data-ttu-id="c2e04-159">Als u niet van plan toocontinue bent, gebruikt u Hallo opdracht toodelete Hallo-resources die u hebt gemaakt in dit artikel te volgen.</span><span class="sxs-lookup"><span data-stu-id="c2e04-159">If you do not plan toocontinue, use hello following command toodelete hello resources you created in this article.</span></span>

```azurecli-interactive
az group delete --name gridResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="c2e04-160">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="c2e04-160">Next steps</span></span>

<span data-ttu-id="c2e04-161">Als u weet hoe toocreate onderwerpen en abonnementen, meer informatie over welke gebeurtenis raster kunt u doen:</span><span class="sxs-lookup"><span data-stu-id="c2e04-161">Now that you know how toocreate topics and event subscriptions, learn more about what Event Grid can help you do:</span></span>

- [<span data-ttu-id="c2e04-162">Over Event Grid</span><span class="sxs-lookup"><span data-stu-id="c2e04-162">About Event Grid</span></span>](overview.md)
- <span data-ttu-id="c2e04-163">[Monitor virtual machine changes with Azure Event Grid and Logic Apps](monitor-virtual-machine-changes-event-grid-logic-app.md) (Wijzigingen in virtuele machines bewaken met Azure Event Grid en Logic Apps)</span><span class="sxs-lookup"><span data-stu-id="c2e04-163">[Monitor virtual machine changes with Azure Event Grid and Logic Apps](monitor-virtual-machine-changes-event-grid-logic-app.md)</span></span>

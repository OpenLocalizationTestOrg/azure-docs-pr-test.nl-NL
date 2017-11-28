---
title: Aangepaste gebeurtenissen voor Azure Event Grid | Microsoft Docs
description: Gebruik Azure Event Grid om een onderwerp te publiceren en u te abonneren op deze gebeurtenis.
services: event-grid
keywords: 
author: djrosanova
ms.author: darosa
ms.date: 08/15/2017
ms.topic: hero-article
ms.service: event-grid
ms.openlocfilehash: 0290836bebadb20085a3ce84dddc088c3af385da
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="create-and-route-custom-events-with-azure-event-grid"></a><span data-ttu-id="10bf1-103">Aangepaste gebeurtenissen maken en routeren met behulp van Azure Event Grid</span><span class="sxs-lookup"><span data-stu-id="10bf1-103">Create and route custom events with Azure Event Grid</span></span>

<span data-ttu-id="10bf1-104">Azure Event Grid is een gebeurtenisservice voor de cloud.</span><span class="sxs-lookup"><span data-stu-id="10bf1-104">Azure Event Grid is an eventing service for the cloud.</span></span> <span data-ttu-id="10bf1-105">In dit artikel gebruikt u de Azure CLI om een aangepast onderwerp te maken, u op het onderwerp te abonneren, en de gebeurtenis te activeren om het resultaat weer te geven.</span><span class="sxs-lookup"><span data-stu-id="10bf1-105">In this article, you use the Azure CLI to create a custom topic, subscribe to the topic, and trigger the event to view the result.</span></span> <span data-ttu-id="10bf1-106">Meestal stuurt u gebeurtenissen naar een eindpunt dat reageert op de gebeurtenis, zoals een webhook of Azure-functie.</span><span class="sxs-lookup"><span data-stu-id="10bf1-106">Typically, you send events to an endpoint that responds to the event, such as, a webhook or Azure Function.</span></span> <span data-ttu-id="10bf1-107">Ter vereenvoudiging van dit artikel stuurt u hier de gebeurtenissen echter naar een URL via welke de berichten alleen maar worden verzameld.</span><span class="sxs-lookup"><span data-stu-id="10bf1-107">However, to simplify this article, you send the events to a URL that merely collects the messages.</span></span> <span data-ttu-id="10bf1-108">U maakt deze URL met behulp van een open source-hulpprogramma van derden, met de naam [RequestBin](https://requestb.in/).</span><span class="sxs-lookup"><span data-stu-id="10bf1-108">You create this URL by using an open source, third-party tool called [RequestBin](https://requestb.in/).</span></span>

>[!NOTE]
><span data-ttu-id="10bf1-109">**RequestBin** is een open source-hulpprogramma dat niet is bedoeld voor gebruik met een hoge doorvoer.</span><span class="sxs-lookup"><span data-stu-id="10bf1-109">**RequestBin** is an open source tool that is not intended for high throughput usage.</span></span> <span data-ttu-id="10bf1-110">Het gebruik van het hulpprogramma hier is alleen om de mogelijkheden aan te tonen.</span><span class="sxs-lookup"><span data-stu-id="10bf1-110">The use of the tool here is purely demonstrative.</span></span> <span data-ttu-id="10bf1-111">Als u meer dan een gebeurtenis tegelijk pusht, ziet u mogelijk niet alle gebeurtenissen in het hulpprogramma.</span><span class="sxs-lookup"><span data-stu-id="10bf1-111">If you push more than one event at a time, you might not see all of your events in the tool.</span></span>

<span data-ttu-id="10bf1-112">Wanneer u klaar bent, ziet u dat de gebeurtenisgegevens naar een eindpunt zijn verzonden.</span><span class="sxs-lookup"><span data-stu-id="10bf1-112">When you are finished, you see that the event data has been sent to an endpoint.</span></span>

![Gebeurtenisgegevens](./media/custom-event-quickstart/request-result.png)

[!INCLUDE [quickstarts-free-trial-note.md](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="10bf1-114">Als u ervoor kiest om de CLI lokaal te installeren en te gebruiken, moet u voor dit artikel de nieuwste versie van Azure CLI (2.0.14 of hoger) uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="10bf1-114">If you choose to install and use the CLI locally, this article requires that you are running the latest version of Azure CLI (2.0.14 or later).</span></span> <span data-ttu-id="10bf1-115">Voer `az --version` uit om de versie te bekijken.</span><span class="sxs-lookup"><span data-stu-id="10bf1-115">To find the version, run `az --version`.</span></span> <span data-ttu-id="10bf1-116">Als u Azure CLI 2.0 wilt installeren of upgraden, raadpleegt u [Azure CLI 2.0 installeren](/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="10bf1-116">If you need to install or upgrade, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli).</span></span>

## <a name="create-a-resource-group"></a><span data-ttu-id="10bf1-117">Een resourcegroep maken</span><span class="sxs-lookup"><span data-stu-id="10bf1-117">Create a resource group</span></span>

<span data-ttu-id="10bf1-118">Event Grid-onderwerpen zijn Azure-resources en moeten in een Azure-resourcegroep worden geplaatst.</span><span class="sxs-lookup"><span data-stu-id="10bf1-118">Event Grid topics are Azure resources, and must be placed in an Azure resource group.</span></span> <span data-ttu-id="10bf1-119">De resourcegroep is een logische verzameling waarin Azure-resources worden geïmplementeerd en beheerd.</span><span class="sxs-lookup"><span data-stu-id="10bf1-119">The resource group is a logical collection into which Azure resources are deployed and managed.</span></span>

<span data-ttu-id="10bf1-120">Een resourcegroep maken met de opdracht [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="10bf1-120">Create a resource group with the [az group create](/cli/azure/group#create) command.</span></span> 

<span data-ttu-id="10bf1-121">In het volgende voorbeeld wordt een resourcegroep met de naam *gridResourceGroup* gemaakt op de locatie *westus2*.</span><span class="sxs-lookup"><span data-stu-id="10bf1-121">The following example creates a resource group named *gridResourceGroup* in the *westus2* location.</span></span>

```azurecli-interactive
az group create --name gridResourceGroup --location westus2
```

## <a name="create-a-custom-topic"></a><span data-ttu-id="10bf1-122">Een aangepast onderwerp maken</span><span class="sxs-lookup"><span data-stu-id="10bf1-122">Create a custom topic</span></span>

<span data-ttu-id="10bf1-123">Een onderwerp biedt een door de gebruiker gedefinieerd eindpunt waarop u de gebeurtenissen kunt posten.</span><span class="sxs-lookup"><span data-stu-id="10bf1-123">A topic provides a user-defined endpoint that you post your events to.</span></span> <span data-ttu-id="10bf1-124">In het volgende voorbeeld wordt een onderwerp gemaakt in de resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="10bf1-124">The following example creates the topic in your resource group.</span></span> <span data-ttu-id="10bf1-125">Vervang `<topic_name>` door een unieke naam voor het onderwerp.</span><span class="sxs-lookup"><span data-stu-id="10bf1-125">Replace `<topic_name>` with a unique name for your topic.</span></span> <span data-ttu-id="10bf1-126">De onderwerpnaam moet uniek zijn omdat deze wordt vertegenwoordigd door een DNS-vermelding.</span><span class="sxs-lookup"><span data-stu-id="10bf1-126">The topic name must be unique because it is represented by a DNS entry.</span></span> <span data-ttu-id="10bf1-127">Voor de preview-versie ondersteunt Event Grid de locaties **westus2** en **westcentralus**.</span><span class="sxs-lookup"><span data-stu-id="10bf1-127">For the preview release, Event Grid supports **westus2** and **westcentralus** locations.</span></span>

```azurecli-interactive
az eventgrid topic create --name <topic_name> -l westus2 -g gridResourceGroup
```

## <a name="create-a-message-endpoint"></a><span data-ttu-id="10bf1-128">Het eindpunt van een bericht maken</span><span class="sxs-lookup"><span data-stu-id="10bf1-128">Create a message endpoint</span></span>

<span data-ttu-id="10bf1-129">Voordat u zich abonneert op het onderwerp, gaan we het eindpunt voor het gebeurtenisbericht maken.</span><span class="sxs-lookup"><span data-stu-id="10bf1-129">Before subscribing to the topic, let's create the endpoint for the event message.</span></span> <span data-ttu-id="10bf1-130">In plaats van code te schrijven om op de gebeurtenis te reageren, maken we een eindpunt waarop de berichten worden verzameld, zodat u ze kunt weergeven.</span><span class="sxs-lookup"><span data-stu-id="10bf1-130">Rather than write code to respond to the event, let's create an endpoint that collects the messages so you can view them.</span></span> <span data-ttu-id="10bf1-131">RequestBin is een open source-hulpprogramma van derden waarmee u een eindpunt kunt maken en aanvragen kunt weergeven die naar dit eindpunt worden verzonden.</span><span class="sxs-lookup"><span data-stu-id="10bf1-131">RequestBin is an open source, third-party tool that enables you to create an endpoint, and view requests that are sent to it.</span></span> <span data-ttu-id="10bf1-132">Ga naar [RequestBin](https://requestb.in/) en klik op **Een RequestBin maken**.</span><span class="sxs-lookup"><span data-stu-id="10bf1-132">Go to [RequestBin](https://requestb.in/), and click **Create a RequestBin**.</span></span>  <span data-ttu-id="10bf1-133">Kopieer de URL. U hebt deze nodig wanneer u zich abonneert op het onderwerp.</span><span class="sxs-lookup"><span data-stu-id="10bf1-133">Copy the bin URL, because you need it when subscribing to the topic.</span></span>

## <a name="subscribe-to-a-topic"></a><span data-ttu-id="10bf1-134">Abonneren op een onderwerp</span><span class="sxs-lookup"><span data-stu-id="10bf1-134">Subscribe to a topic</span></span>

<span data-ttu-id="10bf1-135">U abonneert u op een onderwerp om Event Grid te laten weten welke gebeurtenissen u wilt traceren. In het volgende voorbeeld ziet u hoe u zich abonneert op het onderwerp dat u hebt gemaakt, en hoe de URL van RequestBin wordt doorgegeven als het eindpunt voor de gebeurtenismelding.</span><span class="sxs-lookup"><span data-stu-id="10bf1-135">You subscribe to a topic to tell Event Grid which events you want to track. The following example subscribes to the topic you created, and passes the URL from RequestBin as the endpoint for event notification.</span></span> <span data-ttu-id="10bf1-136">Vervang `<event_subscription_name>` door een unieke naam voor het abonnement, en `<URL_from_RequestBin>` door de waarde uit de voorgaande sectie.</span><span class="sxs-lookup"><span data-stu-id="10bf1-136">Replace `<event_subscription_name>` with a unique name for your subscription, and `<URL_from_RequestBin>` with the value from the preceding section.</span></span> <span data-ttu-id="10bf1-137">Door een eindpunt op te geven wanneer u zich abonneert, wordt via Event Grid de routering van gebeurtenissen naar dit eindpunt verwerkt.</span><span class="sxs-lookup"><span data-stu-id="10bf1-137">By specifying an endpoint when subscribing, Event Grid handles the routing of events to that endpoint.</span></span> <span data-ttu-id="10bf1-138">Gebruik voor `<topic_name>` de waarde die u eerder hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="10bf1-138">For `<topic_name>`, use the value you created earlier.</span></span> 

```azurecli-interactive
az eventgrid topic event-subscription create --name <event_subscription_name> \
  --endpoint <URL_from_RequestBin> \
  -g gridResourceGroup \
  --topic-name <topic_name>
```

## <a name="send-an-event-to-your-topic"></a><span data-ttu-id="10bf1-139">Een gebeurtenis verzenden naar het onderwerp</span><span class="sxs-lookup"><span data-stu-id="10bf1-139">Send an event to your topic</span></span>

<span data-ttu-id="10bf1-140">Nu gaan we een gebeurtenis activeren om te zien hoe het bericht via Event Grid naar het eindpunt wordt gedistribueerd.</span><span class="sxs-lookup"><span data-stu-id="10bf1-140">Now, let's trigger an event to see how Event Grid distributes the message to your endpoint.</span></span> <span data-ttu-id="10bf1-141">Eerst gaan we de URL en de sleutel voor het onderwerp ophalen.</span><span class="sxs-lookup"><span data-stu-id="10bf1-141">First, let's get the URL and key for the topic.</span></span> <span data-ttu-id="10bf1-142">Gebruik opnieuw de onderwerpnaam voor `<topic_name>`.</span><span class="sxs-lookup"><span data-stu-id="10bf1-142">Again, use your topic name for `<topic_name>`.</span></span>

```azurecli-interactive
endpoint=$(az eventgrid topic show --name <topic_name> -g gridResourceGroup --query "endpoint" --output tsv)
key=$(az eventgrid topic key list --name <topic_name> -g gridResourceGroup --query "key1" --output tsv)
```

<span data-ttu-id="10bf1-143">Ter vereenvoudiging van dit artikel hebben we voorbeeldgegevens voor de gebeurtenis ingesteld om naar het onderwerp te verzenden.</span><span class="sxs-lookup"><span data-stu-id="10bf1-143">To simplify this article, we have set up sample event data to send to the topic.</span></span> <span data-ttu-id="10bf1-144">Meestal worden de gebeurtenisgegevens verzonden via een toepassing of Azure-service.</span><span class="sxs-lookup"><span data-stu-id="10bf1-144">Typically, an application or Azure service would send the event data.</span></span> <span data-ttu-id="10bf1-145">In de volgende gegevens worden de gebeurtenisgegevens opgehaald:</span><span class="sxs-lookup"><span data-stu-id="10bf1-145">The following example gets the event data:</span></span>

```azurecli-interactive
body=$(eval echo "'$(curl https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/event-grid/customevent.json)'")
```

<span data-ttu-id="10bf1-146">Als u `echo "$body"` kunt u de volledige gebeurtenis zien.</span><span class="sxs-lookup"><span data-stu-id="10bf1-146">If you `echo "$body"` you can see the full event.</span></span> <span data-ttu-id="10bf1-147">Het element `data` van de JSON is de nettolading van de gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="10bf1-147">The `data` element of the JSON is the payload of your event.</span></span> <span data-ttu-id="10bf1-148">Elke juist opgemaakte JSON kan in dit veld worden ingevoerd.</span><span class="sxs-lookup"><span data-stu-id="10bf1-148">Any well-formed JSON can go in this field.</span></span> <span data-ttu-id="10bf1-149">U kunt het onderwerpveld ook gebruiken voor geavanceerd routeren en filteren.</span><span class="sxs-lookup"><span data-stu-id="10bf1-149">You can also use the subject field for advanced routing and filtering.</span></span>

<span data-ttu-id="10bf1-150">CURL is een hulpprogramma waarmee HTTP-aanvragen worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="10bf1-150">CURL is a utility that performs HTTP requests.</span></span> <span data-ttu-id="10bf1-151">In dit artikel gebruiken we CURL om de gebeurtenis naar het onderwerp te verzenden.</span><span class="sxs-lookup"><span data-stu-id="10bf1-151">In this article, we use CURL to send the event to our topic.</span></span> 

```azurecli-interactive
curl -X POST -H "aeg-sas-key: $key" -d "$body" $endpoint
```

<span data-ttu-id="10bf1-152">U hebt de gebeurtenis geactiveerd, en de gebeurtenis is via Event Grid verzonden naar het eindpunt dat u hebt geconfigureerd toen u zich abonneerde.</span><span class="sxs-lookup"><span data-stu-id="10bf1-152">You have triggered the event, and Event Grid sent the message to the endpoint you configured when subscribing.</span></span> <span data-ttu-id="10bf1-153">Blader naar de RequestBin-URL die u eerder hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="10bf1-153">Browse to the RequestBin URL that you created earlier.</span></span> <span data-ttu-id="10bf1-154">Of klik in het geopende RequestBin-browservenster op Vernieuwen.</span><span class="sxs-lookup"><span data-stu-id="10bf1-154">Or, click refresh in your open RequestBin browser.</span></span> <span data-ttu-id="10bf1-155">U ziet de gebeurtenis die u zojuist hebt verzonden.</span><span class="sxs-lookup"><span data-stu-id="10bf1-155">You see the event you just sent.</span></span> 

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

## <a name="clean-up-resources"></a><span data-ttu-id="10bf1-156">Resources opschonen</span><span class="sxs-lookup"><span data-stu-id="10bf1-156">Clean up resources</span></span>
<span data-ttu-id="10bf1-157">Als u verder wilt werken met deze gebeurtenis, schoont u de resources die u hebt gemaakt in dit artikel, niet op.</span><span class="sxs-lookup"><span data-stu-id="10bf1-157">If you plan to continue working with this event, do not clean up the resources created in this article.</span></span> <span data-ttu-id="10bf1-158">Als u niet verder wilt werken, gebruikt u de volgende opdracht om de resources te verwijderen die u in dit artikel hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="10bf1-158">If you do not plan to continue, use the following command to delete the resources you created in this article.</span></span>

```azurecli-interactive
az group delete --name gridResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="10bf1-159">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="10bf1-159">Next steps</span></span>

<span data-ttu-id="10bf1-160">U weet nu hoe u onderwerpen maakt en hoe u zich abonneert op een gebeurtenis. Kijk waar Event Grid u nog meer bij kan helpen:</span><span class="sxs-lookup"><span data-stu-id="10bf1-160">Now that you know how to create topics and event subscriptions, learn more about what Event Grid can help you do:</span></span>

- [<span data-ttu-id="10bf1-161">Over Event Grid</span><span class="sxs-lookup"><span data-stu-id="10bf1-161">About Event Grid</span></span>](overview.md)
- <span data-ttu-id="10bf1-162">[Monitor virtual machine changes with Azure Event Grid and Logic Apps](monitor-virtual-machine-changes-event-grid-logic-app.md) (Wijzigingen in virtuele machines bewaken met Azure Event Grid en Logic Apps)</span><span class="sxs-lookup"><span data-stu-id="10bf1-162">[Monitor virtual machine changes with Azure Event Grid and Logic Apps](monitor-virtual-machine-changes-event-grid-logic-app.md)</span></span>

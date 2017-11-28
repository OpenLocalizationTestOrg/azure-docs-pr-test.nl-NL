---
title: aaaAzure container register webhooks | Microsoft Docs
description: Azure-container register webhooks.
services: container-registry
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: acr, azure-container-registry
keywords: Docker, Containers ACR
ms.assetid: 
ms.service: container-registry
ms.devlang: na
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/06/2017
ms.author: nepeters
ms.openlocfilehash: adc2afec486007e2d54cd689e6f7ef8b1098db06
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-container-registry-webhooks---azure-portal"></a><span data-ttu-id="6e55f-104">Met behulp van Azure Container register webhooks - Azure-portal</span><span class="sxs-lookup"><span data-stu-id="6e55f-104">Using Azure Container Registry webhooks - Azure portal</span></span>

<span data-ttu-id="6e55f-105">Een Azure container registry opgeslagen en beheerd persoonlijke Docker-container installatiekopieën, vergelijkbare toohello manier Docker Hub openbare Docker-installatiekopieën worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="6e55f-105">An Azure container registry stores and manages private Docker container images, similar toohello way Docker Hub stores public Docker images.</span></span> <span data-ttu-id="6e55f-106">U webhooks tootrigger gebeurtenissen wanneer bepaalde acties uitgevoerd in een van de Register-opslagplaatsen.</span><span class="sxs-lookup"><span data-stu-id="6e55f-106">You use webhooks tootrigger events when certain actions take place in one of your registry repositories.</span></span> <span data-ttu-id="6e55f-107">Webhooks tooevents op Hallo register niveau kunnen reageren, of ze kunnen worden gericht op omlaag tooa specifieke opslagplaats label.</span><span class="sxs-lookup"><span data-stu-id="6e55f-107">Webhooks can respond tooevents at hello registry level or they can be scoped down tooa specific repository tag.</span></span> 

<span data-ttu-id="6e55f-108">Zie voor meer informatie over de achtergrond en concepten Hallo [overzicht](./container-registry-intro.md).</span><span class="sxs-lookup"><span data-stu-id="6e55f-108">For more background and concepts, see hello [overview](./container-registry-intro.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6e55f-109">Vereisten</span><span class="sxs-lookup"><span data-stu-id="6e55f-109">Prerequisites</span></span> 

- <span data-ttu-id="6e55f-110">Azure-container beheerd register - een register beheerde container maken in uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="6e55f-110">Azure container managed registry - Create a managed container registry in your Azure subscription.</span></span> <span data-ttu-id="6e55f-111">Bijvoorbeeld, gebruik hello Azure-portal of Azure CLI 2.0 Hallo.</span><span class="sxs-lookup"><span data-stu-id="6e55f-111">For example, use hello Azure portal or hello Azure CLI 2.0.</span></span> 
- <span data-ttu-id="6e55f-112">Docker CLI - tooset van uw lokale computer als een Docker-host en toegang Hallo Docker CLI-opdrachten, Docker-Engine installeren.</span><span class="sxs-lookup"><span data-stu-id="6e55f-112">Docker CLI - tooset up your local computer as a Docker host and access hello Docker CLI commands, install Docker Engine.</span></span> 

## <a name="create-webhook-azure-portal"></a><span data-ttu-id="6e55f-113">Maken van de webhook Azure-portal</span><span class="sxs-lookup"><span data-stu-id="6e55f-113">Create webhook Azure portal</span></span>

1. <span data-ttu-id="6e55f-114">Meld u bij toohello Azure-portal en navigeer toohello register waarin wordt gezocht toocreate webhooks.</span><span class="sxs-lookup"><span data-stu-id="6e55f-114">Log in toohello Azure portal and navigate toohello registry in which you want toocreate webhooks.</span></span> 

2. <span data-ttu-id="6e55f-115">Selecteer in de Hallo container blade Hallo 'Webhooks' tabblad.</span><span class="sxs-lookup"><span data-stu-id="6e55f-115">In hello container blade, select hello "Webhooks" tab.</span></span> 

3. <span data-ttu-id="6e55f-116">Selecteer "Toevoegen" hello webhook blade werkbalk van.</span><span class="sxs-lookup"><span data-stu-id="6e55f-116">Select "Add" from hello webhook blade toolbar.</span></span> 

4. <span data-ttu-id="6e55f-117">Volledige Hallo *Webhook maken* formulier Hello volgende informatie:</span><span class="sxs-lookup"><span data-stu-id="6e55f-117">Complete hello *Create Webhook* form with hello following information:</span></span>

| <span data-ttu-id="6e55f-118">Waarde</span><span class="sxs-lookup"><span data-stu-id="6e55f-118">Value</span></span> | <span data-ttu-id="6e55f-119">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="6e55f-119">Description</span></span> |
|---|---|
| <span data-ttu-id="6e55f-120">Naam</span><span class="sxs-lookup"><span data-stu-id="6e55f-120">Name</span></span> | <span data-ttu-id="6e55f-121">gewenste toogive toohello webhook Hallo-naam.</span><span class="sxs-lookup"><span data-stu-id="6e55f-121">hello name you want toogive toohello webhook.</span></span> <span data-ttu-id="6e55f-122">Kan alleen kleine letters en cijfers bevatten en tussen 5 tot 50 tekens bevatten.</span><span class="sxs-lookup"><span data-stu-id="6e55f-122">It can only contain lowercase letters and numbers and between 5-50 characters.</span></span> |
| <span data-ttu-id="6e55f-123">Service-URI</span><span class="sxs-lookup"><span data-stu-id="6e55f-123">Service URI</span></span> | <span data-ttu-id="6e55f-124">Hallo URI waar Hallo webhook POST meldingen te verzenden.</span><span class="sxs-lookup"><span data-stu-id="6e55f-124">hello URI where hello webhook should send POST notifications.</span></span> |
| <span data-ttu-id="6e55f-125">Aangepaste headers</span><span class="sxs-lookup"><span data-stu-id="6e55f-125">Custom headers</span></span> | <span data-ttu-id="6e55f-126">Headers gewenste toopass samen met de Hallo POST-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="6e55f-126">Headers you want toopass along with hello POST request.</span></span> <span data-ttu-id="6e55f-127">Ze moet ' sleutel: waarde ' indeling.</span><span class="sxs-lookup"><span data-stu-id="6e55f-127">They should be in "key: value" format.</span></span> |
| <span data-ttu-id="6e55f-128">Acties starten</span><span class="sxs-lookup"><span data-stu-id="6e55f-128">Trigger actions</span></span> | <span data-ttu-id="6e55f-129">Acties die Hallo webhook activeren.</span><span class="sxs-lookup"><span data-stu-id="6e55f-129">Actions that trigger hello webhook.</span></span> <span data-ttu-id="6e55f-130">Momenteel webhooks kan worden geactiveerd door push en/of acties tooan installatiekopie verwijderen.</span><span class="sxs-lookup"><span data-stu-id="6e55f-130">Currently webhooks can be triggered by push and/or delete actions tooan image.</span></span> |
| <span data-ttu-id="6e55f-131">Status</span><span class="sxs-lookup"><span data-stu-id="6e55f-131">Status</span></span> | <span data-ttu-id="6e55f-132">Hallo-status voor Hallo webhook nadat deze gemaakt.</span><span class="sxs-lookup"><span data-stu-id="6e55f-132">hello status for hello webhook after it's created.</span></span> <span data-ttu-id="6e55f-133">Dit standaard ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="6e55f-133">It's enabled by default.</span></span> |
| <span data-ttu-id="6e55f-134">Bereik</span><span class="sxs-lookup"><span data-stu-id="6e55f-134">Scope</span></span> | <span data-ttu-id="6e55f-135">Hallo-scope op welke Hallo webhook werkt.</span><span class="sxs-lookup"><span data-stu-id="6e55f-135">hello scope at which hello webhook works.</span></span> <span data-ttu-id="6e55f-136">Hallo-scope is standaard voor alle gebeurtenissen in het Hallo-register.</span><span class="sxs-lookup"><span data-stu-id="6e55f-136">By default hello scope is for all events in hello registry.</span></span> <span data-ttu-id="6e55f-137">Het kan worden opgegeven voor een bibliotheek of een tag met de indeling Hallo ' opslagplaats: code '.</span><span class="sxs-lookup"><span data-stu-id="6e55f-137">It can be specified for a repository or a tag by using hello format "repository: tag".</span></span> |

<span data-ttu-id="6e55f-138">Voorbeeld van de webhook formulier:</span><span class="sxs-lookup"><span data-stu-id="6e55f-138">Example webhook form:</span></span>

![DCOS GEBRUIKERSINTERFACE](./media/container-registry-webhook/webhook.png)

## <a name="create-webhook-azure-cli"></a><span data-ttu-id="6e55f-140">Azure CLI-webhook maken</span><span class="sxs-lookup"><span data-stu-id="6e55f-140">Create webhook Azure CLI</span></span>

<span data-ttu-id="6e55f-141">toocreate een webhook met Azure CLI, gebruik Hallo Hallo [az acr-webhook maken](/cli/azure/acr/webhook#create) opdracht.</span><span class="sxs-lookup"><span data-stu-id="6e55f-141">toocreate a webhook using hello Azure CLI, use hello [az acr webhook create](/cli/azure/acr/webhook#create) command.</span></span>

```azurecli-interactive
az acr webhook create --registry mycontainerregistry --name myacrwebhook01 --actions delete --uri http://webhookuri.com
```

## <a name="test-webhook"></a><span data-ttu-id="6e55f-142">Test webhook</span><span class="sxs-lookup"><span data-stu-id="6e55f-142">Test webhook</span></span>

### <a name="azure-portal"></a><span data-ttu-id="6e55f-143">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="6e55f-143">Azure portal</span></span>

<span data-ttu-id="6e55f-144">Eerdere toousing hello webhook voor container push installatiekopie en verwijderingsacties, kunnen worden getest met Hallo **Ping** knop.</span><span class="sxs-lookup"><span data-stu-id="6e55f-144">Prior toousing hello webhook on container image push and delete actions, it can be tested using hello **Ping** button.</span></span> <span data-ttu-id="6e55f-145">Wanneer gebruikt, stuurt Hallo Ping dat een toohello algemene post-aanvraag opgegeven eindpunt en logboeken Hallo antwoord.</span><span class="sxs-lookup"><span data-stu-id="6e55f-145">When used, hello Ping sends a generic post request toohello specified endpoint and logs hello response.</span></span> <span data-ttu-id="6e55f-146">Dit is handig tooverify die Hallo webhook is correct zijn ingesteld.</span><span class="sxs-lookup"><span data-stu-id="6e55f-146">This is helpful tooverify that hello webhook has been set up correctly.</span></span>

1. <span data-ttu-id="6e55f-147">Hallo-webhook u tootest wilt selecteren.</span><span class="sxs-lookup"><span data-stu-id="6e55f-147">Select hello webhook you want tootest.</span></span> 
2. <span data-ttu-id="6e55f-148">Selecteer in de bovenste werkbalk Hallo Hallo 'Pingen' actie.</span><span class="sxs-lookup"><span data-stu-id="6e55f-148">In hello top toolbar, select hello "Ping" action.</span></span> 
3. <span data-ttu-id="6e55f-149">Controleer Hallo-aanvraag en -antwoord.</span><span class="sxs-lookup"><span data-stu-id="6e55f-149">Check hello request and response.</span></span>

### <a name="azure-cli"></a><span data-ttu-id="6e55f-150">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="6e55f-150">Azure CLI</span></span>

<span data-ttu-id="6e55f-151">tootest een webhook ACR Hello Azure CLI gebruiken Hallo [az acr webhook ping](/cli/azure/acr/webhook#ping) opdracht.</span><span class="sxs-lookup"><span data-stu-id="6e55f-151">tootest an ACR webhook with hello Azure CLI, use hello [az acr webhook ping](/cli/azure/acr/webhook#ping) command.</span></span>

```azurecli-interactive
az acr webhook ping --registry mycontainerregistry --name myacrwebhook01
```

<span data-ttu-id="6e55f-152">toosee hello resultaten gebruiken Hallo [az acr webhook lijst-gebeurtenissen](/cli/azure/acr/webhook#list-events) opdracht.</span><span class="sxs-lookup"><span data-stu-id="6e55f-152">toosee hello results, use hello [az acr webhook list-events](/cli/azure/acr/webhook#list-events) command.</span></span> 

```azurecli-interactive
az acr webhook list-events --registry mycontainerregistry08 --name myacrwebhook01
```

## <a name="delete-webhook"></a><span data-ttu-id="6e55f-153">Webhook verwijderen</span><span class="sxs-lookup"><span data-stu-id="6e55f-153">Delete webhook</span></span>

### <a name="azure-portal"></a><span data-ttu-id="6e55f-154">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="6e55f-154">Azure portal</span></span>

<span data-ttu-id="6e55f-155">Elke webhook kan worden verwijderd door Hallo webhook en vervolgens Hallo verwijderen knop op Hallo Azure-portal te selecteren.</span><span class="sxs-lookup"><span data-stu-id="6e55f-155">Each webhook can be deleted by selecting hello webhook and then hello delete button on hello Azure portal.</span></span>

### <a name="azure-cli"></a><span data-ttu-id="6e55f-156">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="6e55f-156">Azure CLI</span></span>

```azurecli-interactive
az acr webhook delete --registry mycontainerregistry --name myacrwebhook01
```
---
title: aaaApplication of gebruikersspecifieke Marathon-service | Microsoft Docs
description: Een toepassings- of gebruikersspecifieke Marathon-service maken
services: container-service
documentationcenter: 
author: rgardler
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: Containers, Marathon, Micro-services, DC/OS, Azure
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/12/2016
ms.author: rogardle
ms.custom: mvc
ms.openlocfilehash: 1e6f69ed64e113a3a059788a71ddb57b6d3ad8da
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-or-user-specific-marathon-service"></a><span data-ttu-id="85eb0-104">Een toepassings- of gebruikersspecifieke Marathon-service maken</span><span class="sxs-lookup"><span data-stu-id="85eb0-104">Create an application or user-specific Marathon service</span></span>
<span data-ttu-id="85eb0-105">Azure Container Service voorziet in een set masterservers waarop we Apache Mesos en Marathon vooraf configureren.</span><span class="sxs-lookup"><span data-stu-id="85eb0-105">Azure Container Service provides a set of master servers on which we preconfigure Apache Mesos and Marathon.</span></span> <span data-ttu-id="85eb0-106">Deze kunnen zich gebruikte tooorchestrate uw toepassingen op Hallo-cluster, maar het beste niet toouse Hallo masterservers voor dit doel.</span><span class="sxs-lookup"><span data-stu-id="85eb0-106">These can be used tooorchestrate your applications on hello cluster, but it's best not toouse hello master servers for this purpose.</span></span> <span data-ttu-id="85eb0-107">Bijvoorbeeld Hallo configuratie van Marathon aanpassingen vereist aan te melden bij Hallo masterservers zelf en het aanbrengen van wijzigingen--dit gebruikers aangemoedigd unieke masterservers die enigszins verschillen van hello standard- en nodig toobe verzorgd beheerde en onafhankelijk van elkaar.</span><span class="sxs-lookup"><span data-stu-id="85eb0-107">For example, tweaking hello configuration of Marathon requires logging into hello master servers themselves and making changes--this encourages unique master servers that are a little different from hello standard and need toobe cared for and managed independently.</span></span> <span data-ttu-id="85eb0-108">Hallo configuratie uit te voeren door een team mogelijk ook geen Hallo optimale configuratie voor een ander team.</span><span class="sxs-lookup"><span data-stu-id="85eb0-108">Additionally, hello configuration required by one team might not be hello optimal configuration for another team.</span></span>

<span data-ttu-id="85eb0-109">In dit artikel wordt uitgelegd hoe tooadd een toepassing of gebruikersspecifieke Marathon-service.</span><span class="sxs-lookup"><span data-stu-id="85eb0-109">In this article, we'll explain how tooadd an application or user-specific Marathon service.</span></span>

<span data-ttu-id="85eb0-110">Aangezien deze service tooa één gebruiker of het team behoren wordt, worden ze gratis tooconfigure deze op een manier die ze willen.</span><span class="sxs-lookup"><span data-stu-id="85eb0-110">Because this service will belong tooa single user or team, they are free tooconfigure it in any way that they desire.</span></span> <span data-ttu-id="85eb0-111">Ook zorgt Azure Container Service ervoor dat de service Hallo toorun blijft.</span><span class="sxs-lookup"><span data-stu-id="85eb0-111">Also, Azure Container Service will ensure that hello service continues toorun.</span></span> <span data-ttu-id="85eb0-112">Als het Hallo-service is mislukt, opnieuw Azure Container Service het voor u.</span><span class="sxs-lookup"><span data-stu-id="85eb0-112">If hello service fails, Azure Container Service will restart it for you.</span></span> <span data-ttu-id="85eb0-113">Meestal zijn Hallo u won't zelfs niets merken van eventuele uitval.</span><span class="sxs-lookup"><span data-stu-id="85eb0-113">Most of hello time you won't even notice it had downtime.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="85eb0-114">Vereisten</span><span class="sxs-lookup"><span data-stu-id="85eb0-114">Prerequisites</span></span>
<span data-ttu-id="85eb0-115">[Implementeer een exemplaar van Azure Container Service](container-service-deployment.md) met orchestrator typen DC/OS en [Zorg dat de client verbinding maken met cluster tooyour](../container-service-connect.md).</span><span class="sxs-lookup"><span data-stu-id="85eb0-115">[Deploy an instance of Azure Container Service](container-service-deployment.md) with orchestrator type DC/OS and  [ensure that your client can connect tooyour cluster](../container-service-connect.md).</span></span> <span data-ttu-id="85eb0-116">Bovendien Hallo volgende stappen.</span><span class="sxs-lookup"><span data-stu-id="85eb0-116">Also, do hello following steps.</span></span>

[!INCLUDE [install hello DC/OS CLI](../../../includes/container-service-install-dcos-cli-include.md)]

## <a name="create-an-application-or-user-specific-marathon-service"></a><span data-ttu-id="85eb0-117">Een toepassings- of gebruikersspecifieke Marathon-service maken</span><span class="sxs-lookup"><span data-stu-id="85eb0-117">Create an application or user-specific Marathon service</span></span>
<span data-ttu-id="85eb0-118">Beginnen met het maken van een JSON-configuratiebestand die Hallo-naam van de toepassingsservice Hallo dat u wilt dat toocreate definieert.</span><span class="sxs-lookup"><span data-stu-id="85eb0-118">Begin by creating a JSON configuration file that defines hello name of hello application service that you want toocreate.</span></span> <span data-ttu-id="85eb0-119">Hier gebruiken we `marathon-alice` als Hallo framework naam.</span><span class="sxs-lookup"><span data-stu-id="85eb0-119">Here we use `marathon-alice` as hello framework name.</span></span> <span data-ttu-id="85eb0-120">Hallo-bestand opslaan als ongeveer `marathon-alice.json`:</span><span class="sxs-lookup"><span data-stu-id="85eb0-120">Save hello file as something like `marathon-alice.json`:</span></span>

```json
{"marathon": {"framework-name": "marathon-alice" }}
```

<span data-ttu-id="85eb0-121">Gebruik vervolgens Hallo DC/OS CLI tooinstall Hallo Marathon-exemplaar met Hallo-opties die in uw configuratiebestand zijn ingesteld:</span><span class="sxs-lookup"><span data-stu-id="85eb0-121">Next, use hello DC/OS CLI tooinstall hello Marathon instance with hello options that are set in your configuration file:</span></span>

```bash
dcos package install --options=marathon-alice.json marathon
```

<span data-ttu-id="85eb0-122">U ziet nu uw `marathon-alice` -service wordt uitgevoerd op het tabblad voor Hallo-Services van uw DC/OS-gebruikersinterface.</span><span class="sxs-lookup"><span data-stu-id="85eb0-122">You should now see your `marathon-alice` service running in hello Services tab of your DC/OS UI.</span></span> <span data-ttu-id="85eb0-123">Hallo gebruikersinterface worden `http://<hostname>/service/marathon-alice/` als u wilt dat tooaccess dit rechtstreeks.</span><span class="sxs-lookup"><span data-stu-id="85eb0-123">hello UI will be `http://<hostname>/service/marathon-alice/` if you want tooaccess it directly.</span></span>

## <a name="set-hello-dcos-cli-tooaccess-hello-service"></a><span data-ttu-id="85eb0-124">Hallo DC/OS CLI tooaccess Hallo service instellen</span><span class="sxs-lookup"><span data-stu-id="85eb0-124">Set hello DC/OS CLI tooaccess hello service</span></span>
<span data-ttu-id="85eb0-125">U kunt eventueel configureren uw DC/OS CLI tooaccess deze nieuwe service met instelling Hallo `marathon.url` eigenschap toopoint toohello `marathon-alice` exemplaar als volgt:</span><span class="sxs-lookup"><span data-stu-id="85eb0-125">You can optionally configure your DC/OS CLI tooaccess this new service by setting hello `marathon.url` property toopoint toohello `marathon-alice` instance as follows:</span></span>

```bash
dcos config set marathon.url http://<hostname>/service/marathon-alice/
```

<span data-ttu-id="85eb0-126">U kunt controleren welk exemplaar van Marathon die uw CLI met Hallo werkt `dcos config show` opdracht.</span><span class="sxs-lookup"><span data-stu-id="85eb0-126">You can verify which instance of Marathon that your CLI is working against with hello `dcos config show` command.</span></span> <span data-ttu-id="85eb0-127">U kunt terugkeren toousing uw Marathon-masterservice met de opdracht Hallo `dcos config unset marathon.url`.</span><span class="sxs-lookup"><span data-stu-id="85eb0-127">You can revert toousing your master Marathon service with hello command `dcos config unset marathon.url`.</span></span>


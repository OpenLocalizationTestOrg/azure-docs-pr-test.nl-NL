---
title: aaaCreate een pad op basis van een Azure-Portal - Azure Application Gateway - regel | Microsoft Docs
description: Meer informatie over hoe toocreate een regel op basis van het pad voor een toepassingsgateway met behulp van de portal Hallo
services: application-gateway
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 87bd93bc-e1a6-45db-a226-555948f1feb7
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/03/2017
ms.author: gwallace
ms.openlocfilehash: 21cb52c426ca5f7dfedf07a96e87fbc85d243647
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-path-based-rule-for-an-application-gateway-by-using-hello-portal"></a><span data-ttu-id="94362-103">Een regel op basis van het pad voor een toepassingsgateway maken met behulp van Hallo-portal</span><span class="sxs-lookup"><span data-stu-id="94362-103">Create a Path-based rule for an application gateway by using hello portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="94362-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="94362-104">Azure portal</span></span>](application-gateway-create-url-route-portal.md)
> * [<span data-ttu-id="94362-105">Azure Resource Manager PowerShell</span><span class="sxs-lookup"><span data-stu-id="94362-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-url-route-arm-ps.md)
> * [<span data-ttu-id="94362-106">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="94362-106">Azure CLI 2.0</span></span>](application-gateway-create-url-route-cli.md)

<span data-ttu-id="94362-107">URL-pad gebaseerde routering, kunt u tooassociate routes op basis van de URL-pad Hallo van Http-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="94362-107">URL Path-based routing enables you tooassociate routes based on hello URL path of Http request.</span></span> <span data-ttu-id="94362-108">Het wordt gecontroleerd of er een route tooa back-end-adresgroep geconfigureerd voor het Hallo-URL die wordt vermeld in Hallo Application Gateway is en verzendt Hallo netwerkverkeer toohello gedefinieerd back-end-pool.</span><span class="sxs-lookup"><span data-stu-id="94362-108">It checks if there is a route tooa back-end pool configured for hello URL listed in hello Application Gateway and sends hello network traffic toohello defined back-end pool.</span></span> <span data-ttu-id="94362-109">Vaak gebruikt voor het doorsturen van op basis van een URL is tooload van aanvragen verdelen over voor andere typen inhoud toodifferent back-end-servergroepen.</span><span class="sxs-lookup"><span data-stu-id="94362-109">A common use for URL-based routing is tooload balance requests for different content types toodifferent back-end server pools.</span></span>

<span data-ttu-id="94362-110">URL gebaseerde routering introduceert een nieuwe regel type tooapplication gateway.</span><span class="sxs-lookup"><span data-stu-id="94362-110">URL-based routing introduces a new rule type tooapplication gateway.</span></span> <span data-ttu-id="94362-111">Toepassingsgateway heeft twee regeltypen: basic-en op basis van het pad.</span><span class="sxs-lookup"><span data-stu-id="94362-111">Application gateway has two rule types: basic and path-based rules.</span></span> <span data-ttu-id="94362-112">Hallo basic regeltype, biedt een round robin-service voor Hallo back-end voor groepen tijdens het pad gebaseerde regels bovendien tooround robin distributie, ook rekening wordt gehouden pad patroon van de aanvraag-URL Hallo daarbij de juiste back-endpool Hallo.</span><span class="sxs-lookup"><span data-stu-id="94362-112">hello basic rule type, provides round-robin service for hello back-end pools while path-based rules in addition tooround robin distribution, also takes path pattern of hello request URL into account while choosing hello appropriate backend pool.</span></span>

## <a name="scenario"></a><span data-ttu-id="94362-113">Scenario</span><span class="sxs-lookup"><span data-stu-id="94362-113">Scenario</span></span>

<span data-ttu-id="94362-114">Hallo doorloopt volgende scenario maken van een regel op basis van een pad in een bestaande toepassingsgateway.</span><span class="sxs-lookup"><span data-stu-id="94362-114">hello following scenario goes through creating a Path-based rule in an existing application gateway.</span></span>
<span data-ttu-id="94362-115">Hallo scenario wordt ervan uitgegaan dat u al stappen hebt gevolgd hello te[een toepassingsgateway maken](application-gateway-create-gateway-portal.md).</span><span class="sxs-lookup"><span data-stu-id="94362-115">hello scenario assumes that you have already followed hello steps too[Create an Application Gateway](application-gateway-create-gateway-portal.md).</span></span>

![URL-route][scenario]

## <span data-ttu-id="94362-117"><a name="createrule"></a>Hallo-pad op basis van een regel maken</span><span class="sxs-lookup"><span data-stu-id="94362-117"><a name="createrule"></a>Create hello Path-based rule</span></span>

<span data-ttu-id="94362-118">Een regel op basis van het pad moet een eigen listener voordat Hallo regel maken die ervoor tooverify die u hebt een toouse beschikbaar listener worden.</span><span class="sxs-lookup"><span data-stu-id="94362-118">A Path-based rule requires its own listener, before creating hello rule be sure tooverify you have an available listener toouse.</span></span>

### <a name="step-1"></a><span data-ttu-id="94362-119">Stap 1</span><span class="sxs-lookup"><span data-stu-id="94362-119">Step 1</span></span>

<span data-ttu-id="94362-120">Navigeer toohello [Azure-portal](http://portal.azure.com) en selecteer een bestaande toepassing.</span><span class="sxs-lookup"><span data-stu-id="94362-120">Navigate toohello [Azure portal](http://portal.azure.com) and select an existing application gateway.</span></span> <span data-ttu-id="94362-121">Klik op **regels**</span><span class="sxs-lookup"><span data-stu-id="94362-121">Click **Rules**</span></span>

![Overzicht van Application Gateway][1]

### <a name="step-2"></a><span data-ttu-id="94362-123">Stap 2</span><span class="sxs-lookup"><span data-stu-id="94362-123">Step 2</span></span>

<span data-ttu-id="94362-124">Klik op **op basis van het pad** tooadd knop een nieuwe regel op basis van het pad.</span><span class="sxs-lookup"><span data-stu-id="94362-124">Click **Path-based** button tooadd a new Path-based rule.</span></span>

### <a name="step-3"></a><span data-ttu-id="94362-125">Stap 3</span><span class="sxs-lookup"><span data-stu-id="94362-125">Step 3</span></span>

<span data-ttu-id="94362-126">Hallo **toevoegen op basis van een pad regel** blade bevat twee secties.</span><span class="sxs-lookup"><span data-stu-id="94362-126">hello **Add path-based rule** blade has two sections.</span></span> <span data-ttu-id="94362-127">de eerste sectie Hallo is waar u Hallo listener, Hallo-naam van regel Hallo en Hallo pad standaardinstellingen gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="94362-127">hello first section is where you defined hello listener, hello name of hello rule and hello default path settings.</span></span> <span data-ttu-id="94362-128">Hallo zijn standaardinstellingen pad voor routes die niet onder Hallo aangepast op basis van een pad route vallen.</span><span class="sxs-lookup"><span data-stu-id="94362-128">hello default path settings are for routes that do not fall under hello custom path-based route.</span></span> <span data-ttu-id="94362-129">tweede gedeelte van Hallo Hallo **toevoegen op basis van een pad regel** blade is waar u Hallo pad gebaseerde regels zelf definiëren.</span><span class="sxs-lookup"><span data-stu-id="94362-129">hello second section of hello **Add path-based rule** blade is where you define hello path-based rules themselves.</span></span>

<span data-ttu-id="94362-130">**Basisinstellingen**</span><span class="sxs-lookup"><span data-stu-id="94362-130">**Basic Settings**</span></span>

* <span data-ttu-id="94362-131">**Naam** -deze waarde is een beschrijvende naam toohello regel die toegankelijk is in Hallo-portal.</span><span class="sxs-lookup"><span data-stu-id="94362-131">**Name** - This value is a friendly name toohello rule that is accessible in hello portal.</span></span>
* <span data-ttu-id="94362-132">**Listener** -deze waarde is Hallo-listener die wordt gebruikt voor het Hallo-regel.</span><span class="sxs-lookup"><span data-stu-id="94362-132">**Listener** - This value is hello listener that is used for hello rule.</span></span>
* <span data-ttu-id="94362-133">**Standaard back-endpool** -deze instelling is Hallo-instelling die Hallo back-end toobe gebruikt voor de standaardregel Hallo definieert</span><span class="sxs-lookup"><span data-stu-id="94362-133">**Default backend pool** - This setting is hello setting that defines hello back-end toobe used for hello default rule</span></span>
* <span data-ttu-id="94362-134">**Standaardinstellingen voor HTTP-** -deze instelling is Hallo-instelling die Hallo HTTP-instellingen toobe gebruikt voor de standaardregel Hallo definieert.</span><span class="sxs-lookup"><span data-stu-id="94362-134">**Default HTTP settings** - This setting is hello setting that defines hello HTTP settings toobe used for hello default rule.</span></span>

<span data-ttu-id="94362-135">**Regels op basis van het pad**</span><span class="sxs-lookup"><span data-stu-id="94362-135">**Path-based rules**</span></span>

* <span data-ttu-id="94362-136">**Naam** -deze waarde is een beschrijvende naam op basis van toopath regel.</span><span class="sxs-lookup"><span data-stu-id="94362-136">**Name** - This value is a friendly name toopath-based rule.</span></span>
* <span data-ttu-id="94362-137">**Paden** -deze instelling bepaalt Hallo pad Hallo regel zoekt doorsturen van verkeer</span><span class="sxs-lookup"><span data-stu-id="94362-137">**Paths** - This setting defines hello path hello rule looks for when forwarding traffic</span></span>
* <span data-ttu-id="94362-138">**Back-Endpool** -deze instelling is Hallo-instelling die Hallo back-end toobe gebruikt voor het Hallo-regel definieert</span><span class="sxs-lookup"><span data-stu-id="94362-138">**Backend Pool** - This setting is hello setting that defines hello back-end toobe used for hello rule</span></span>
* <span data-ttu-id="94362-139">**HTTP-instelling** -deze instelling is Hallo-instelling die Hallo HTTP-instellingen toobe gebruikt voor het Hallo-regel definieert.</span><span class="sxs-lookup"><span data-stu-id="94362-139">**HTTP setting** - This setting is hello setting that defines hello HTTP settings toobe used for hello rule.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="94362-140">Paden: lijst Hallo van pad patronen toomatch.</span><span class="sxs-lookup"><span data-stu-id="94362-140">Paths: hello list of path patterns toomatch.</span></span> <span data-ttu-id="94362-141">Elk moet beginnen met / en Hallo enige plaats waar een '\*' is toegestaan Hallo einde.</span><span class="sxs-lookup"><span data-stu-id="94362-141">Each must start with / and hello only place a "\*" is allowed is at hello end.</span></span> <span data-ttu-id="94362-142">Voorbeelden van geldige zijn/xyz, /xyz* of xyz / *.</span><span class="sxs-lookup"><span data-stu-id="94362-142">Valid examples are /xyz, /xyz* or /xyz/*.</span></span>  

![Een regel op basis van een pad blade met informatie is ingevuld toevoegen][2]

<span data-ttu-id="94362-144">Toevoegen van een regel op basis van het pad tooan is bestaande application gateway een eenvoudig proces via Hallo-portal.</span><span class="sxs-lookup"><span data-stu-id="94362-144">Adding a path-based rule tooan existing application gateway is an easy process through hello portal.</span></span> <span data-ttu-id="94362-145">Nadat een regel op basis van het pad is gemaakt, kan het bewerkte tooadd extra regels zijn.</span><span class="sxs-lookup"><span data-stu-id="94362-145">After a path-based rule has been created, it can be edited tooadd additional rules.</span></span> 

![Extra regels op basis van het pad toevoegen][3]

<span data-ttu-id="94362-147">Deze stap configureert u een route op basis van het pad.</span><span class="sxs-lookup"><span data-stu-id="94362-147">This step configures a path-based route.</span></span> <span data-ttu-id="94362-148">Het is belangrijk toounderstand aanvragen niet opnieuw geschreven, zoals aanvragen worden geleverd in de toepassingsgateway inspecteert Hallo-aanvraag en basic op Hallo url patroon verzendt Hallo aanvraag toohello juiste back-end.</span><span class="sxs-lookup"><span data-stu-id="94362-148">It is important toounderstand that requests are not rewritten, as requests come in application gateway inspects hello request and basic on hello url pattern sends hello request toohello appropriate back-end.</span></span>

## <a name="next-steps"></a><span data-ttu-id="94362-149">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="94362-149">Next steps</span></span>

<span data-ttu-id="94362-150">hoe tooconfigure SSL-Offloading met Azure Application Gateway, Zie toolearn [SSL-Offload configureren](application-gateway-ssl-portal.md)</span><span class="sxs-lookup"><span data-stu-id="94362-150">toolearn how tooconfigure SSL Offloading with Azure Application Gateway, see [Configure SSL Offload](application-gateway-ssl-portal.md)</span></span>

[1]: ./media/application-gateway-create-url-route-portal/figure1.png
[2]: ./media/application-gateway-create-url-route-portal/figure2.png
[3]: ./media/application-gateway-create-url-route-portal/figure3.png
[scenario]: ./media/application-gateway-create-url-route-portal/scenario.png

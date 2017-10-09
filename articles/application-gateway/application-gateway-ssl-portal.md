---
title: aaaConfigure SSL-offload - Azure Application Gateway - Azure Portal | Microsoft Docs
description: Deze pagina vindt u instructies toocreate een toepassingsgateway met SSL-offload met behulp van Hallo-portal
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 8373379a-a26a-45d2-aa62-dd282298eff3
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: gwallace
ms.openlocfilehash: e87ac0bbe10ac45e307c18802741c7bc31764a20
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-an-application-gateway-for-ssl-offload-by-using-hello-portal"></a><span data-ttu-id="de26e-103">Een toepassingsgateway voor SSL-offload configureren met behulp van Hallo-portal</span><span class="sxs-lookup"><span data-stu-id="de26e-103">Configure an application gateway for SSL offload by using hello portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="de26e-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="de26e-104">Azure portal</span></span>](application-gateway-ssl-portal.md)
> * [<span data-ttu-id="de26e-105">Azure Resource Manager PowerShell</span><span class="sxs-lookup"><span data-stu-id="de26e-105">Azure Resource Manager PowerShell</span></span>](application-gateway-ssl-arm.md)
> * [<span data-ttu-id="de26e-106">Azure Classic PowerShell</span><span class="sxs-lookup"><span data-stu-id="de26e-106">Azure Classic PowerShell</span></span>](application-gateway-ssl.md)
> * [<span data-ttu-id="de26e-107">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="de26e-107">Azure CLI 2.0</span></span>](application-gateway-ssl-cli.md)

<span data-ttu-id="de26e-108">Azure Application Gateway kan worden geconfigureerd tooterminate Hallo Secure Sockets Layer (SSL)-sessie op Hallo gateway tooavoid kostbare SSL ontsleuteling taken toohappen op Hallo-webfarm.</span><span class="sxs-lookup"><span data-stu-id="de26e-108">Azure Application Gateway can be configured tooterminate hello Secure Sockets Layer (SSL) session at hello gateway tooavoid costly SSL decryption tasks toohappen at hello web farm.</span></span> <span data-ttu-id="de26e-109">SSL-offload vereenvoudigt ook Hallo front-end-server instellen en beheren van Hallo-webtoepassing.</span><span class="sxs-lookup"><span data-stu-id="de26e-109">SSL offload also simplifies hello front-end server setup and management of hello web application.</span></span>

## <a name="scenario"></a><span data-ttu-id="de26e-110">Scenario</span><span class="sxs-lookup"><span data-stu-id="de26e-110">Scenario</span></span>

<span data-ttu-id="de26e-111">Hallo volgen scenario doorloopt configureren van SSL-offload op een bestaande toepassingsgateway.</span><span class="sxs-lookup"><span data-stu-id="de26e-111">hello following scenario goes through configuring SSL offload on an existing application gateway.</span></span> <span data-ttu-id="de26e-112">Hallo scenario wordt ervan uitgegaan dat u al stappen hebt gevolgd hello te[een toepassingsgateway maken](application-gateway-create-gateway-portal.md).</span><span class="sxs-lookup"><span data-stu-id="de26e-112">hello scenario assumes that you have already followed hello steps too[Create an Application Gateway](application-gateway-create-gateway-portal.md).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="de26e-113">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="de26e-113">Before you begin</span></span>

<span data-ttu-id="de26e-114">tooconfigure SSL-offload met een application gateway, een certificaat is vereist.</span><span class="sxs-lookup"><span data-stu-id="de26e-114">tooconfigure SSL offload with an application gateway, a certificate is required.</span></span> <span data-ttu-id="de26e-115">Dit certificaat is geladen in de toepassingsgateway Hallo en tooencrypt gebruikt en ontsleutelen van Hallo verkeer dat wordt verzonden via SSL.</span><span class="sxs-lookup"><span data-stu-id="de26e-115">This certificate is loaded on hello application gateway and used tooencrypt and decrypt hello traffic sent via SSL.</span></span> <span data-ttu-id="de26e-116">Hallo-certificaat moet toobe Personal Information Exchange (pfx)-indeling.</span><span class="sxs-lookup"><span data-stu-id="de26e-116">hello certificate needs toobe in Personal Information Exchange (pfx) format.</span></span> <span data-ttu-id="de26e-117">Deze bestandsindeling kunt Hallo persoonlijke sleutel toobe geëxporteerd die vereist wordt door Hallo application gateway tooperform Hallo versleuteling en ontsleuteling van verkeer.</span><span class="sxs-lookup"><span data-stu-id="de26e-117">This file format allows for hello private key toobe exported which is required by hello application gateway tooperform hello encryption and decryption of traffic.</span></span>

## <a name="add-an-https-listener"></a><span data-ttu-id="de26e-118">Toevoegen van een HTTPS-listener</span><span class="sxs-lookup"><span data-stu-id="de26e-118">Add an HTTPS listener</span></span>

<span data-ttu-id="de26e-119">Hallo HTTPS-listener zoekt verkeer op basis van de configuratie en helpt route Hallo verkeer toohello back-endpools.</span><span class="sxs-lookup"><span data-stu-id="de26e-119">hello HTTPS listener looks for traffic based on its configuration and helps route hello traffic toohello backend pools.</span></span>

### <a name="step-1"></a><span data-ttu-id="de26e-120">Stap 1</span><span class="sxs-lookup"><span data-stu-id="de26e-120">Step 1</span></span>

<span data-ttu-id="de26e-121">Gaat toohello Azure-portal en selecteert u een bestaande application gateway</span><span class="sxs-lookup"><span data-stu-id="de26e-121">Navigate toohello Azure portal and select an existing application gateway</span></span>

### <a name="step-2"></a><span data-ttu-id="de26e-122">Stap 2</span><span class="sxs-lookup"><span data-stu-id="de26e-122">Step 2</span></span>

<span data-ttu-id="de26e-123">Listeners en klik op de knop tooadd een listener voor Hallo toevoegen.</span><span class="sxs-lookup"><span data-stu-id="de26e-123">Click Listeners and click hello Add button tooadd a listener.</span></span>

![overzichtsblade van App-gateway][1]

### <a name="step-3"></a><span data-ttu-id="de26e-125">Stap 3</span><span class="sxs-lookup"><span data-stu-id="de26e-125">Step 3</span></span>

<span data-ttu-id="de26e-126">Vul het vereiste informatie voor de listener Hallo Hallo en uploaden Hallo pfx-certificaat, als u klaar klikt u op OK.</span><span class="sxs-lookup"><span data-stu-id="de26e-126">Fill out hello required information for hello listener and upload hello .pfx certificate, when complete click OK.</span></span>

<span data-ttu-id="de26e-127">**Naam** -deze waarde is een beschrijvende naam van het Hallo-listener.</span><span class="sxs-lookup"><span data-stu-id="de26e-127">**Name** - This value is a friendly name of hello listener.</span></span>

<span data-ttu-id="de26e-128">**Frontend-IP configuratie** -deze waarde is Hallo frontend-IP-configuratie die wordt gebruikt voor het Hallo-listener.</span><span class="sxs-lookup"><span data-stu-id="de26e-128">**Frontend IP configuration** - This value is hello frontend IP configuration that is used for hello listener.</span></span>

<span data-ttu-id="de26e-129">**Frontend-poort (naam/poort)** -een beschrijvende naam voor het Hallo-poort die wordt gebruikt op Hallo front-end van de toepassingsgateway Hallo en Hallo werkelijke poort die wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="de26e-129">**Frontend port (Name/Port)** - A friendly name for hello port used on hello front end of hello application gateway and hello actual port used.</span></span>

<span data-ttu-id="de26e-130">**Protocol** -een switch toodetermine als https of http wordt gebruikt voor het Hallo-front-end.</span><span class="sxs-lookup"><span data-stu-id="de26e-130">**Protocol** - A switch toodetermine if https or http is used for hello front end.</span></span>

<span data-ttu-id="de26e-131">**Certificaat (naam en wachtwoord)** - als SSL-offload wordt gebruikt, is een pfx-certificaat vereist voor deze instelling en een beschrijvende naam en wachtwoord zijn vereist.</span><span class="sxs-lookup"><span data-stu-id="de26e-131">**Certificate (Name/Password)** - If SSL offload is used, a .pfx certificate is required for this setting and a friendly name and password are required.</span></span>

![listener-blade toevoegen][2]

## <a name="create-a-rule-and-associate-it-toohello-listener"></a><span data-ttu-id="de26e-133">Een regel maken en koppelen toohello listener</span><span class="sxs-lookup"><span data-stu-id="de26e-133">Create a rule and associate it toohello listener</span></span>

<span data-ttu-id="de26e-134">Hallo-listener is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="de26e-134">hello listener has now been created.</span></span> <span data-ttu-id="de26e-135">Het is tijd toocreate het verkeer van een regel toohandle Hallo van Hallo listener.</span><span class="sxs-lookup"><span data-stu-id="de26e-135">It is time toocreate a rule toohandle hello traffic from hello listener.</span></span> <span data-ttu-id="de26e-136">Regels definiëren hoe verkeer wordt gerouteerd toohello back-endpools op basis van meerdere configuratie-instellingen, inclusief of sessie cookies gebaseerde affiniteit wordt gebruikt, protocol, poort en statuscontroles.</span><span class="sxs-lookup"><span data-stu-id="de26e-136">Rules define how traffic is routed toohello backend pools based on multiple configuration settings, including whether cookie-based session affinity is used, protocol, port, and health probes.</span></span>

### <a name="step-1"></a><span data-ttu-id="de26e-137">Stap 1</span><span class="sxs-lookup"><span data-stu-id="de26e-137">Step 1</span></span>

<span data-ttu-id="de26e-138">Klik op Hallo **regels** van toepassingsgateway hello, en klik vervolgens op toevoegen.</span><span class="sxs-lookup"><span data-stu-id="de26e-138">Click hello **Rules** of hello application gateway, and then click Add.</span></span>

![blade App gateway-regels][3]

### <a name="step-2"></a><span data-ttu-id="de26e-140">Stap 2</span><span class="sxs-lookup"><span data-stu-id="de26e-140">Step 2</span></span>

<span data-ttu-id="de26e-141">Op Hallo **basic regel toevoegen** blade Typ Hallo beschrijvende naam voor Hallo regel en kies Hallo-listener is gemaakt in de vorige stap Hallo.</span><span class="sxs-lookup"><span data-stu-id="de26e-141">On hello **Add basic rule** blade, type in hello friendly name for hello rule and choose hello listener created in hello previous step.</span></span> <span data-ttu-id="de26e-142">Kies Hallo juiste back-endpool en HTTP-instelling en klik op **OK**</span><span class="sxs-lookup"><span data-stu-id="de26e-142">Choose hello appropriate backend pool and http setting and click **OK**</span></span>

![venster van de instellingen voor HTTPS][4]

<span data-ttu-id="de26e-144">Hallo-instellingen worden nu opgeslagen toohello toepassingsgateway.</span><span class="sxs-lookup"><span data-stu-id="de26e-144">hello settings are now saved toohello application gateway.</span></span> <span data-ttu-id="de26e-145">Hallo Sla-proces voor deze instellingen duurt even voordat ze beschikbaar tooview via Hallo portal of PowerShell.</span><span class="sxs-lookup"><span data-stu-id="de26e-145">hello save process for these settings may take a while before they are available tooview through hello portal or through PowerShell.</span></span> <span data-ttu-id="de26e-146">Toepassingsgateway eenmaal opgeslagen Hallo verwerkt Hallo versleuteling en ontsleuteling van verkeer.</span><span class="sxs-lookup"><span data-stu-id="de26e-146">Once saved hello application gateway handles hello encryption and decryption of traffic.</span></span> <span data-ttu-id="de26e-147">Al het verkeer tussen de toepassingsgateway Hallo en Hallo back-end-webservers wordt verwerkt via http.</span><span class="sxs-lookup"><span data-stu-id="de26e-147">All traffic between hello application gateway and hello backend web servers will be handled over http.</span></span> <span data-ttu-id="de26e-148">Alle communicatie back toohello client als gestart via https geretourneerd toohello client versleuteld.</span><span class="sxs-lookup"><span data-stu-id="de26e-148">Any communication back toohello client if initiated over https will be returned toohello client encrypted.</span></span>

## <a name="next-steps"></a><span data-ttu-id="de26e-149">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="de26e-149">Next steps</span></span>

<span data-ttu-id="de26e-150">toolearn hoe tooconfigure een aangepaste health test met Azure Application Gateway, Zie [maken van een aangepaste health test](application-gateway-create-gateway-portal.md).</span><span class="sxs-lookup"><span data-stu-id="de26e-150">toolearn how tooconfigure a custom health probe with Azure Application Gateway, see [Create a custom health probe](application-gateway-create-gateway-portal.md).</span></span>

[1]: ./media/application-gateway-ssl-portal/figure1.png
[2]: ./media/application-gateway-ssl-portal/figure2.png
[3]: ./media/application-gateway-ssl-portal/figure3.png
[4]: ./media/application-gateway-ssl-portal/figure4.png

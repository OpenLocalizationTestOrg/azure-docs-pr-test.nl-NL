---
title: Configureren van SSL-offload - Azure Application Gateway - Azure-Portal | Microsoft Docs
description: Deze pagina vindt u instructies voor het maken van een toepassingsgateway met SSL-offload met behulp van de portal
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
ms.openlocfilehash: f61be0cc4c9274c9914f7c468ce48a2a3d0a4f4a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="configure-an-application-gateway-for-ssl-offload-by-using-the-portal"></a><span data-ttu-id="81ccd-103">Een toepassingsgateway voor SSL-offload configureren met behulp van de portal</span><span class="sxs-lookup"><span data-stu-id="81ccd-103">Configure an application gateway for SSL offload by using the portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="81ccd-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="81ccd-104">Azure portal</span></span>](application-gateway-ssl-portal.md)
> * [<span data-ttu-id="81ccd-105">Azure Resource Manager PowerShell</span><span class="sxs-lookup"><span data-stu-id="81ccd-105">Azure Resource Manager PowerShell</span></span>](application-gateway-ssl-arm.md)
> * [<span data-ttu-id="81ccd-106">Azure Classic PowerShell</span><span class="sxs-lookup"><span data-stu-id="81ccd-106">Azure Classic PowerShell</span></span>](application-gateway-ssl.md)
> * [<span data-ttu-id="81ccd-107">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="81ccd-107">Azure CLI 2.0</span></span>](application-gateway-ssl-cli.md)

<span data-ttu-id="81ccd-108">Azure Application Gateway kan zodanig worden geconfigureerd dat de Secure Sockets Layer-sessie (SSL) wordt beëindigd bij de gateway om kostbare SSL-ontsleutelingstaken te voorkomen die worden uitgevoerd in de webfarm.</span><span class="sxs-lookup"><span data-stu-id="81ccd-108">Azure Application Gateway can be configured to terminate the Secure Sockets Layer (SSL) session at the gateway to avoid costly SSL decryption tasks to happen at the web farm.</span></span> <span data-ttu-id="81ccd-109">Met SSL-offload worden ook het instellen van de front-endserver en het beheer van de webtoepassing eenvoudiger.</span><span class="sxs-lookup"><span data-stu-id="81ccd-109">SSL offload also simplifies the front-end server setup and management of the web application.</span></span>

## <a name="scenario"></a><span data-ttu-id="81ccd-110">Scenario</span><span class="sxs-lookup"><span data-stu-id="81ccd-110">Scenario</span></span>

<span data-ttu-id="81ccd-111">Het volgende scenario gaat het bij het configureren van SSL-offload op een bestaande toepassingsgateway.</span><span class="sxs-lookup"><span data-stu-id="81ccd-111">The following scenario goes through configuring SSL offload on an existing application gateway.</span></span> <span data-ttu-id="81ccd-112">Het scenario wordt ervan uitgegaan dat u de stappen voor het al hebt gevolgd [een toepassingsgateway maken](application-gateway-create-gateway-portal.md).</span><span class="sxs-lookup"><span data-stu-id="81ccd-112">The scenario assumes that you have already followed the steps to [Create an Application Gateway](application-gateway-create-gateway-portal.md).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="81ccd-113">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="81ccd-113">Before you begin</span></span>

<span data-ttu-id="81ccd-114">Er is een certificaat voor SSL-offload met een application gateway configureert, vereist.</span><span class="sxs-lookup"><span data-stu-id="81ccd-114">To configure SSL offload with an application gateway, a certificate is required.</span></span> <span data-ttu-id="81ccd-115">Dit certificaat wordt geladen in de toepassingsgateway en gebruikt voor het versleutelen en ontsleutelen van het verkeer dat wordt verzonden via SSL.</span><span class="sxs-lookup"><span data-stu-id="81ccd-115">This certificate is loaded on the application gateway and used to encrypt and decrypt the traffic sent via SSL.</span></span> <span data-ttu-id="81ccd-116">Het certificaat moet zich in de indeling Personal Information Exchange (pfx).</span><span class="sxs-lookup"><span data-stu-id="81ccd-116">The certificate needs to be in Personal Information Exchange (pfx) format.</span></span> <span data-ttu-id="81ccd-117">Deze bestandsindeling kunt u de persoonlijke sleutel exporteerbaar die voor de toepassingsgateway vereist is om uit te voeren voor de versleuteling en ontsleuteling van verkeer.</span><span class="sxs-lookup"><span data-stu-id="81ccd-117">This file format allows for the private key to be exported which is required by the application gateway to perform the encryption and decryption of traffic.</span></span>

## <a name="add-an-https-listener"></a><span data-ttu-id="81ccd-118">Toevoegen van een HTTPS-listener</span><span class="sxs-lookup"><span data-stu-id="81ccd-118">Add an HTTPS listener</span></span>

<span data-ttu-id="81ccd-119">De HTTPS-listener wordt gezocht naar verkeer op basis van de configuratie en helpt bij het verkeer naar de back-endpools sturen.</span><span class="sxs-lookup"><span data-stu-id="81ccd-119">The HTTPS listener looks for traffic based on its configuration and helps route the traffic to the backend pools.</span></span>

### <a name="step-1"></a><span data-ttu-id="81ccd-120">Stap 1</span><span class="sxs-lookup"><span data-stu-id="81ccd-120">Step 1</span></span>

<span data-ttu-id="81ccd-121">Navigeer naar de Azure-portal en selecteer een bestaande application gateway</span><span class="sxs-lookup"><span data-stu-id="81ccd-121">Navigate to the Azure portal and select an existing application gateway</span></span>

### <a name="step-2"></a><span data-ttu-id="81ccd-122">Stap 2</span><span class="sxs-lookup"><span data-stu-id="81ccd-122">Step 2</span></span>

<span data-ttu-id="81ccd-123">Listeners en klik op de knop toevoegen om het toevoegen van een listener.</span><span class="sxs-lookup"><span data-stu-id="81ccd-123">Click Listeners and click the Add button to add a listener.</span></span>

![overzichtsblade van App-gateway][1]

### <a name="step-3"></a><span data-ttu-id="81ccd-125">Stap 3</span><span class="sxs-lookup"><span data-stu-id="81ccd-125">Step 3</span></span>

<span data-ttu-id="81ccd-126">Vul de vereiste informatie voor de listener en upload het pfx-certificaat, als u klaar Klik op OK.</span><span class="sxs-lookup"><span data-stu-id="81ccd-126">Fill out the required information for the listener and upload the .pfx certificate, when complete click OK.</span></span>

<span data-ttu-id="81ccd-127">**Naam** -deze waarde is een beschrijvende naam van de listener.</span><span class="sxs-lookup"><span data-stu-id="81ccd-127">**Name** - This value is a friendly name of the listener.</span></span>

<span data-ttu-id="81ccd-128">**Frontend-IP configuratie** -deze waarde is de frontend-IP-configuratie die wordt gebruikt voor de listener.</span><span class="sxs-lookup"><span data-stu-id="81ccd-128">**Frontend IP configuration** - This value is the frontend IP configuration that is used for the listener.</span></span>

<span data-ttu-id="81ccd-129">**Frontend-poort (naam/poort)** : een beschrijvende naam voor de poort op de front-end van de toepassingsgateway gebruikt en de werkelijke poort gebruikt.</span><span class="sxs-lookup"><span data-stu-id="81ccd-129">**Frontend port (Name/Port)** - A friendly name for the port used on the front end of the application gateway and the actual port used.</span></span>

<span data-ttu-id="81ccd-130">**Protocol** -een schakeloptie om te bepalen als https of http voor de front-endserver gebruikt.</span><span class="sxs-lookup"><span data-stu-id="81ccd-130">**Protocol** - A switch to determine if https or http is used for the front end.</span></span>

<span data-ttu-id="81ccd-131">**Certificaat (naam en wachtwoord)** - als SSL-offload wordt gebruikt, is een pfx-certificaat vereist voor deze instelling en een beschrijvende naam en wachtwoord zijn vereist.</span><span class="sxs-lookup"><span data-stu-id="81ccd-131">**Certificate (Name/Password)** - If SSL offload is used, a .pfx certificate is required for this setting and a friendly name and password are required.</span></span>

![listener-blade toevoegen][2]

## <a name="create-a-rule-and-associate-it-to-the-listener"></a><span data-ttu-id="81ccd-133">Een regel maken en deze koppelen aan de listener</span><span class="sxs-lookup"><span data-stu-id="81ccd-133">Create a rule and associate it to the listener</span></span>

<span data-ttu-id="81ccd-134">De listener is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="81ccd-134">The listener has now been created.</span></span> <span data-ttu-id="81ccd-135">Is het tijd om een regel voor het afhandelen van het verkeer van de listener te maken.</span><span class="sxs-lookup"><span data-stu-id="81ccd-135">It is time to create a rule to handle the traffic from the listener.</span></span> <span data-ttu-id="81ccd-136">Regels definiëren hoe verkeer wordt doorgestuurd naar de back-end-adresgroepen op basis van meerdere configuratie-instellingen, inclusief of sessie cookies gebaseerde affiniteit wordt gebruikt, protocol, poort en statuscontroles.</span><span class="sxs-lookup"><span data-stu-id="81ccd-136">Rules define how traffic is routed to the backend pools based on multiple configuration settings, including whether cookie-based session affinity is used, protocol, port, and health probes.</span></span>

### <a name="step-1"></a><span data-ttu-id="81ccd-137">Stap 1</span><span class="sxs-lookup"><span data-stu-id="81ccd-137">Step 1</span></span>

<span data-ttu-id="81ccd-138">Klik op de **regels** van de toepassingsgateway, en klik vervolgens op toevoegen.</span><span class="sxs-lookup"><span data-stu-id="81ccd-138">Click the **Rules** of the application gateway, and then click Add.</span></span>

![blade App gateway-regels][3]

### <a name="step-2"></a><span data-ttu-id="81ccd-140">Stap 2</span><span class="sxs-lookup"><span data-stu-id="81ccd-140">Step 2</span></span>

<span data-ttu-id="81ccd-141">Op de **basic regel toevoegen** blade, typ de beschrijvende naam voor de regel en kies de listener is gemaakt in de vorige stap.</span><span class="sxs-lookup"><span data-stu-id="81ccd-141">On the **Add basic rule** blade, type in the friendly name for the rule and choose the listener created in the previous step.</span></span> <span data-ttu-id="81ccd-142">Kies de juiste back-endpool en HTTP-instelling en klikt u op **OK**</span><span class="sxs-lookup"><span data-stu-id="81ccd-142">Choose the appropriate backend pool and http setting and click **OK**</span></span>

![venster van de instellingen voor HTTPS][4]

<span data-ttu-id="81ccd-144">De instellingen zijn nu opgeslagen op de toepassingsgateway.</span><span class="sxs-lookup"><span data-stu-id="81ccd-144">The settings are now saved to the application gateway.</span></span> <span data-ttu-id="81ccd-145">Het opslaan verwerken voor deze instellingen kunnen even duren voordat ze beschikbaar zijn voor weergeven via de portal of PowerShell.</span><span class="sxs-lookup"><span data-stu-id="81ccd-145">The save process for these settings may take a while before they are available to view through the portal or through PowerShell.</span></span> <span data-ttu-id="81ccd-146">Wanneer de toepassingsgateway opgeslagen verwerkt de versleuteling en ontsleuteling van verkeer.</span><span class="sxs-lookup"><span data-stu-id="81ccd-146">Once saved the application gateway handles the encryption and decryption of traffic.</span></span> <span data-ttu-id="81ccd-147">Al het verkeer tussen de toepassingsgateway en de back-end-webservers wordt verwerkt via http.</span><span class="sxs-lookup"><span data-stu-id="81ccd-147">All traffic between the application gateway and the backend web servers will be handled over http.</span></span> <span data-ttu-id="81ccd-148">Alle communicatie naar de client als gestart via https wordt geretourneerd naar de client die is versleuteld.</span><span class="sxs-lookup"><span data-stu-id="81ccd-148">Any communication back to the client if initiated over https will be returned to the client encrypted.</span></span>

## <a name="next-steps"></a><span data-ttu-id="81ccd-149">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="81ccd-149">Next steps</span></span>

<span data-ttu-id="81ccd-150">Zie voor meer informatie over het configureren van een aangepaste health test met Azure Application Gateway, [maken van een aangepaste health test](application-gateway-create-gateway-portal.md).</span><span class="sxs-lookup"><span data-stu-id="81ccd-150">To learn how to configure a custom health probe with Azure Application Gateway, see [Create a custom health probe](application-gateway-create-gateway-portal.md).</span></span>

[1]: ./media/application-gateway-ssl-portal/figure1.png
[2]: ./media/application-gateway-ssl-portal/figure2.png
[3]: ./media/application-gateway-ssl-portal/figure3.png
[4]: ./media/application-gateway-ssl-portal/figure4.png

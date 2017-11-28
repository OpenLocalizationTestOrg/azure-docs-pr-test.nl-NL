---
title: aaaCreate een toepassingsgateway met Azure - sjablonen | Microsoft Docs
description: Deze pagina bevat instructies toocreate een toepassingsgateway met hello Azure Resource Manager-sjabloon
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: gwallace
ms.openlocfilehash: fc18e553852551326d6a302abe2c7f8a08c2eb6c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-gateway-by-using-hello-azure-resource-manager-template"></a><span data-ttu-id="e6529-103">Een toepassingsgateway maken met behulp van hello Azure Resource Manager-sjabloon</span><span class="sxs-lookup"><span data-stu-id="e6529-103">Create an application gateway by using hello Azure Resource Manager template</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="e6529-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="e6529-104">Azure portal</span></span>](application-gateway-create-gateway-portal.md)
> * [<span data-ttu-id="e6529-105">Azure Resource Manager PowerShell</span><span class="sxs-lookup"><span data-stu-id="e6529-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-gateway-arm.md)
> * [<span data-ttu-id="e6529-106">Azure Classic PowerShell</span><span class="sxs-lookup"><span data-stu-id="e6529-106">Azure Classic PowerShell</span></span>](application-gateway-create-gateway.md)
> * [<span data-ttu-id="e6529-107">Azure Resource Manager-sjabloon</span><span class="sxs-lookup"><span data-stu-id="e6529-107">Azure Resource Manager template</span></span>](application-gateway-create-gateway-arm-template.md)
> * [<span data-ttu-id="e6529-108">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="e6529-108">Azure CLI</span></span>](application-gateway-create-gateway-cli.md)

<span data-ttu-id="e6529-109">Azure Application Gateway is een load balancer in laag 7.</span><span class="sxs-lookup"><span data-stu-id="e6529-109">Azure Application Gateway is a layer-7 load balancer.</span></span> <span data-ttu-id="e6529-110">Het biedt de failover- en HTTP-aanvragen routeren tussen verschillende servers, ongeacht of deze op Hallo cloud of on-premises.</span><span class="sxs-lookup"><span data-stu-id="e6529-110">It provides failover and performance-routing HTTP requests between different servers, whether they are on hello cloud or on-premises.</span></span> <span data-ttu-id="e6529-111">Application Gateway bevat veel ADC-functies (Application Delivery Controller), waaronder HTTP-taakverdeling, op cookies gebaseerde sessieaffiniteit, SSL-offload (Secure Sockets Layer), aangepaste statustests en ondersteuning voor meerdere locaties.</span><span class="sxs-lookup"><span data-stu-id="e6529-111">Application Gateway provides many application delivery controller (ADC) features including HTTP load balancing, cookie-based session affinity, Secure Sockets Layer (SSL) offload, custom health probes, support for multi-site, and many others.</span></span> <span data-ttu-id="e6529-112">toofind een volledige lijst van ondersteunde functies, gaat u naar [Application Gateway-overzicht](application-gateway-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="e6529-112">toofind a complete list of supported features, visit [Application Gateway overview](application-gateway-introduction.md)</span></span>

<span data-ttu-id="e6529-113">Dit artikel begeleidt u bij het downloaden en wijzigen van een bestaande Azure Resource Manager-sjabloon vanuit GitHub en Hallo sjabloon vanuit GitHub, PowerShell en Azure CLI Hallo implementeren.</span><span class="sxs-lookup"><span data-stu-id="e6529-113">This article walks you through downloading and modifying an existing Azure Resource Manager template from GitHub and deploying hello template from GitHub, PowerShell, and hello Azure CLI.</span></span>

<span data-ttu-id="e6529-114">Als u hello Azure Resource Manager-sjabloon rechtstreeks vanuit GitHub zonder wijzigingen wilt implementeren, slaat u een sjabloon toodeploy vanuit GitHub.</span><span class="sxs-lookup"><span data-stu-id="e6529-114">If you are simply deploying hello Azure Resource Manager template directly from GitHub without any changes, skip toodeploy a template from GitHub.</span></span>

## <a name="scenario"></a><span data-ttu-id="e6529-115">Scenario</span><span class="sxs-lookup"><span data-stu-id="e6529-115">Scenario</span></span>

<span data-ttu-id="e6529-116">In dit scenario:</span><span class="sxs-lookup"><span data-stu-id="e6529-116">In this scenario you will:</span></span>

* <span data-ttu-id="e6529-117">Een toepassingsgateway maken met web application firewall.</span><span class="sxs-lookup"><span data-stu-id="e6529-117">Create an application gateway with web application firewall.</span></span>
* <span data-ttu-id="e6529-118">Maakt u een virtueel netwerk met de naam VirtualNetwork1 met een gereserveerd CIDR-blok van 10.0.0.0/16.</span><span class="sxs-lookup"><span data-stu-id="e6529-118">Create a virtual network named VirtualNetwork1 with a reserved CIDR block of 10.0.0.0/16.</span></span>
* <span data-ttu-id="e6529-119">Maakt u een subnet met de naam Appgatewaysubnet dat gebruikmaakt van 10.0.0.0/28 als CIDR-blok.</span><span class="sxs-lookup"><span data-stu-id="e6529-119">Create a subnet called Appgatewaysubnet that uses 10.0.0.0/28 as its CIDR block.</span></span>
* <span data-ttu-id="e6529-120">Instellen van twee eerder geconfigureerde back-end-IP-adressen voor webservers Hallo u tooload saldo Hallo verkeer.</span><span class="sxs-lookup"><span data-stu-id="e6529-120">Set up two previously configured back-end IPs for hello web servers you want tooload balance hello traffic.</span></span> <span data-ttu-id="e6529-121">In dit voorbeeld sjabloon hello back-end-IP-adressen zijn 10.0.1.10 en 10.0.1.11 gebruikt.</span><span class="sxs-lookup"><span data-stu-id="e6529-121">In this template example, hello back-end IPs are 10.0.1.10 and 10.0.1.11.</span></span>

> [!NOTE]
> <span data-ttu-id="e6529-122">Deze instellingen zijn Hallo parameters voor deze sjabloon.</span><span class="sxs-lookup"><span data-stu-id="e6529-122">Those settings are hello parameters for this template.</span></span> <span data-ttu-id="e6529-123">toocustomize hello sjabloon, kunt u regels, Hallo listener, SSL en andere opties in de bestand azuredeploy.json Hallo wijzigen.</span><span class="sxs-lookup"><span data-stu-id="e6529-123">toocustomize hello template, you can change rules, hello listener, SSL, and other options in hello azuredeploy.json file.</span></span>

![Scenario](./media/application-gateway-create-gateway-arm-template/scenario.png)

## <a name="download-and-understand-hello-azure-resource-manager-template"></a><span data-ttu-id="e6529-125">Hello Azure Resource Manager-sjabloon downloaden en begrijpen</span><span class="sxs-lookup"><span data-stu-id="e6529-125">Download and understand hello Azure Resource Manager template</span></span>

<span data-ttu-id="e6529-126">U kunt downloaden Hallo bestaande Azure Resource Manager-sjabloon toocreate een virtueel netwerk en twee subnets vanuit GitHub, breng eventuele wijzigingen die u mogelijk wilt gebruiken en het opnieuw gebruiken.</span><span class="sxs-lookup"><span data-stu-id="e6529-126">You can download hello existing Azure Resource Manager template toocreate a virtual network and two subnets from GitHub, make any changes you might want, and reuse it.</span></span> <span data-ttu-id="e6529-127">toodo gebruik dus Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="e6529-127">toodo so, use hello following steps:</span></span>

1. <span data-ttu-id="e6529-128">Navigeer te[toepassingsgateway maken met web application firewall ingeschakeld](https://github.com/Azure/azure-quickstart-templates/tree/master/101-application-gateway-waf).</span><span class="sxs-lookup"><span data-stu-id="e6529-128">Navigate too[Create Application Gateway with web application firewall enabled](https://github.com/Azure/azure-quickstart-templates/tree/master/101-application-gateway-waf).</span></span>
1. <span data-ttu-id="e6529-129">Klik op **azuredeploy.json** en vervolgens op **RAW**.</span><span class="sxs-lookup"><span data-stu-id="e6529-129">Click **azuredeploy.json**, and then click **RAW**.</span></span>
1. <span data-ttu-id="e6529-130">Sla Hallo bestand tooa lokale map op uw computer.</span><span class="sxs-lookup"><span data-stu-id="e6529-130">Save hello file tooa local folder on your computer.</span></span>
1. <span data-ttu-id="e6529-131">Als u bekend met Azure Resource Manager-sjablonen bent, slaat u toostep 7.</span><span class="sxs-lookup"><span data-stu-id="e6529-131">If you are familiar with Azure Resource Manager templates, skip toostep 7.</span></span>
1. <span data-ttu-id="e6529-132">Open Hallo-bestand dat u hebt opgeslagen en bekijkt hello inhoud onder **parameters** in regel</span><span class="sxs-lookup"><span data-stu-id="e6529-132">Open hello file that you saved and look at hello contents under **parameters** in line</span></span>
1. <span data-ttu-id="e6529-133">Azure Resource Manager-sjabloonparameters bieden een tijdelijke aanduiding voor waarden die kunnen worden ingevuld tijdens de implementatie.</span><span class="sxs-lookup"><span data-stu-id="e6529-133">Azure Resource Manager template parameters provide a placeholder for values that can be filled out during deployment.</span></span>

  | <span data-ttu-id="e6529-134">Parameter</span><span class="sxs-lookup"><span data-stu-id="e6529-134">Parameter</span></span> | <span data-ttu-id="e6529-135">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="e6529-135">Description</span></span> |
  | --- | --- |
  | <span data-ttu-id="e6529-136">**subnetPrefix**</span><span class="sxs-lookup"><span data-stu-id="e6529-136">**subnetPrefix**</span></span> |<span data-ttu-id="e6529-137">CIDR-blokkering voor het subnet Hallo toepassingsgateway.</span><span class="sxs-lookup"><span data-stu-id="e6529-137">CIDR block for hello application gateway subnet.</span></span> |
  | <span data-ttu-id="e6529-138">**applicationGatewaySize**</span><span class="sxs-lookup"><span data-stu-id="e6529-138">**applicationGatewaySize**</span></span> | <span data-ttu-id="e6529-139">De grootte van de toepassingsgateway Hallo.</span><span class="sxs-lookup"><span data-stu-id="e6529-139">Size of hello application gateway.</span></span>  <span data-ttu-id="e6529-140">WAF kunt alleen middelgrote en grote.</span><span class="sxs-lookup"><span data-stu-id="e6529-140">WAF only allows medium and large.</span></span> |
  | <span data-ttu-id="e6529-141">**backendIpaddress1**</span><span class="sxs-lookup"><span data-stu-id="e6529-141">**backendIpaddress1**</span></span> |<span data-ttu-id="e6529-142">IP-adres van de eerste webserver Hallo.</span><span class="sxs-lookup"><span data-stu-id="e6529-142">IP address of hello first web server.</span></span> |
  | <span data-ttu-id="e6529-143">**backendIpaddress2**</span><span class="sxs-lookup"><span data-stu-id="e6529-143">**backendIpaddress2**</span></span> |<span data-ttu-id="e6529-144">IP-adres van de tweede webserver Hallo.</span><span class="sxs-lookup"><span data-stu-id="e6529-144">IP address of hello second web server.</span></span> |
  | <span data-ttu-id="e6529-145">**wafEnabled**</span><span class="sxs-lookup"><span data-stu-id="e6529-145">**wafEnabled**</span></span> | <span data-ttu-id="e6529-146">Instelling toodetermine als WAF is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="e6529-146">Setting toodetermine if WAF is enabled.</span></span>|
  | <span data-ttu-id="e6529-147">**wafMode**</span><span class="sxs-lookup"><span data-stu-id="e6529-147">**wafMode**</span></span> | <span data-ttu-id="e6529-148">Modus van Hallo web application firewall.</span><span class="sxs-lookup"><span data-stu-id="e6529-148">Mode of hello web application firewall.</span></span>  <span data-ttu-id="e6529-149">Beschikbare opties zijn **preventie** of **detectie**.</span><span class="sxs-lookup"><span data-stu-id="e6529-149">Available options are **prevention** or **detection**.</span></span>|
  | <span data-ttu-id="e6529-150">**wafRuleSetType**</span><span class="sxs-lookup"><span data-stu-id="e6529-150">**wafRuleSetType**</span></span> | <span data-ttu-id="e6529-151">RuleSet-type voor WAF.</span><span class="sxs-lookup"><span data-stu-id="e6529-151">Ruleset type for WAF.</span></span>  <span data-ttu-id="e6529-152">OWASP is momenteel Hallo optie wordt alleen ondersteund.</span><span class="sxs-lookup"><span data-stu-id="e6529-152">Currently OWASP is hello only supported option.</span></span> |
  | <span data-ttu-id="e6529-153">**wafRuleSetVersion**</span><span class="sxs-lookup"><span data-stu-id="e6529-153">**wafRuleSetVersion**</span></span> |<span data-ttu-id="e6529-154">RuleSet-versie.</span><span class="sxs-lookup"><span data-stu-id="e6529-154">Ruleset version.</span></span> <span data-ttu-id="e6529-155">OWASP CRS 2.2.9 en 3.0 zijn momenteel ondersteund Hallo-opties.</span><span class="sxs-lookup"><span data-stu-id="e6529-155">OWASP CRS 2.2.9 and 3.0 are currently hello supported options.</span></span> |

1. <span data-ttu-id="e6529-156">Controleer de inhoud Hallo onder **resources** en kennisgeving Hallo volgende eigenschappen:</span><span class="sxs-lookup"><span data-stu-id="e6529-156">Check hello content under **resources** and notice hello following properties:</span></span>

   * <span data-ttu-id="e6529-157">**type**.</span><span class="sxs-lookup"><span data-stu-id="e6529-157">**type**.</span></span> <span data-ttu-id="e6529-158">Type resource dat door Hallo sjabloon wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="e6529-158">Type of resource being created by hello template.</span></span> <span data-ttu-id="e6529-159">In dit geval Hallo type is `Microsoft.Network/applicationGateways`, die staat voor een toepassingsgateway.</span><span class="sxs-lookup"><span data-stu-id="e6529-159">In this case, hello type is `Microsoft.Network/applicationGateways`, which represents an application gateway.</span></span>
   * <span data-ttu-id="e6529-160">**Naam**.</span><span class="sxs-lookup"><span data-stu-id="e6529-160">**name**.</span></span> <span data-ttu-id="e6529-161">Naam voor Hallo resource.</span><span class="sxs-lookup"><span data-stu-id="e6529-161">Name for hello resource.</span></span> <span data-ttu-id="e6529-162">Kennisgeving Hallo gebruik van `[parameters('applicationGatewayName')]`, wat betekent dat deze Hallo-naam is opgegeven als invoer door u of door een parameterbestand tijdens de implementatie.</span><span class="sxs-lookup"><span data-stu-id="e6529-162">Notice hello use of `[parameters('applicationGatewayName')]`, which means that hello name is provided as input by you or by a parameter file during deployment.</span></span>
   * <span data-ttu-id="e6529-163">**Eigenschappen**.</span><span class="sxs-lookup"><span data-stu-id="e6529-163">**properties**.</span></span> <span data-ttu-id="e6529-164">Lijst met eigenschappen voor Hallo resource.</span><span class="sxs-lookup"><span data-stu-id="e6529-164">List of properties for hello resource.</span></span> <span data-ttu-id="e6529-165">Deze sjabloon maakt gebruik van virtueel netwerk Hallo en openbare IP-adres tijdens het maken van de toepassingsgateway.</span><span class="sxs-lookup"><span data-stu-id="e6529-165">This template uses hello virtual network and public IP address during application gateway creation.</span></span>

   > [!NOTE]
   > <span data-ttu-id="e6529-166">Voor meer informatie over sjablonen gaat u naar: [verwijzing naar Resource Manager-sjablonen](/templates/)</span><span class="sxs-lookup"><span data-stu-id="e6529-166">For more information on templates visit: [Resource Manager templates reference](/templates/)</span></span>

1. <span data-ttu-id="e6529-167">Navigeer terug te[https://github.com/Azure/azure-quickstart-templates/blob/master/101-application-gateway-waf/](https://github.com/Azure/azure-quickstart-templates/blob/master/101-application-gateway-waf).</span><span class="sxs-lookup"><span data-stu-id="e6529-167">Navigate back too[https://github.com/Azure/azure-quickstart-templates/blob/master/101-application-gateway-waf/](https://github.com/Azure/azure-quickstart-templates/blob/master/101-application-gateway-waf).</span></span>
1. <span data-ttu-id="e6529-168">Klik op **azuredeploy-parameters.json**, en klik vervolgens op **RAW**.</span><span class="sxs-lookup"><span data-stu-id="e6529-168">Click **azuredeploy-parameters.json**, and then click **RAW**.</span></span>
1. <span data-ttu-id="e6529-169">Sla Hallo bestand tooa lokale map op uw computer.</span><span class="sxs-lookup"><span data-stu-id="e6529-169">Save hello file tooa local folder on your computer.</span></span>
1. <span data-ttu-id="e6529-170">Open Hallo-bestand dat u hebt opgeslagen en bewerk Hallo waarden voor Hallo-parameters.</span><span class="sxs-lookup"><span data-stu-id="e6529-170">Open hello file that you saved and edit hello values for hello parameters.</span></span> <span data-ttu-id="e6529-171">Gebruik hello waarden toodeploy Hallo toepassingsgateway beschreven in ons scenario te volgen.</span><span class="sxs-lookup"><span data-stu-id="e6529-171">Use hello following values toodeploy hello application gateway described in our scenario.</span></span>

    ```json
    {
        "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
        "contentVersion": "1.0.0.0",
        "parameters": {
            "addressPrefix": {
            "value": "10.0.0.0/16"
            },
            "subnetPrefix": {
            "value": "10.0.0.0/28"
            },
            "applicationGatewaySize": {
            "value": "WAF_Medium"
            },
            "capacity": {
            "value": 2
            },
            "backendIpAddress1": {
            "value": "10.0.1.10"
            },
            "backendIpAddress2": {
            "value": "10.0.1.11"
            },
            "wafEnabled": {
            "value": true
            },
            "wafMode": {
            "value": "Detection"
            },
            "wafRuleSetType": {
            "value": "OWASP"
            },
            "wafRuleSetVersion": {
            "value": "3.0"
            }
        }
    }
    ```

1. <span data-ttu-id="e6529-172">Hallo-bestand opslaan.</span><span class="sxs-lookup"><span data-stu-id="e6529-172">Save hello file.</span></span> <span data-ttu-id="e6529-173">U kunt Hallo JSON-sjabloon en testen met online JSON-validatiehulpprogramma's zoals [JSlint.com](http://www.jslint.com/).</span><span class="sxs-lookup"><span data-stu-id="e6529-173">You can test hello JSON template and parameter template by using online JSON validation tools like [JSlint.com](http://www.jslint.com/).</span></span>

## <a name="deploy-hello-azure-resource-manager-template-by-using-powershell"></a><span data-ttu-id="e6529-174">Hello Azure Resource Manager-sjabloon implementeren met behulp van PowerShell</span><span class="sxs-lookup"><span data-stu-id="e6529-174">Deploy hello Azure Resource Manager template by using PowerShell</span></span>

<span data-ttu-id="e6529-175">Als u Azure PowerShell nog nooit hebt gebruikt, gaat u naar: [hoe tooinstall en configureren van Azure PowerShell](/powershell/azure/overview) en volg Hallo instructies toosign in Azure en uw abonnement te selecteren.</span><span class="sxs-lookup"><span data-stu-id="e6529-175">If you have never used Azure PowerShell, visit: [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) and follow hello instructions toosign into Azure and select your subscription.</span></span>

1. <span data-ttu-id="e6529-176">Aanmelding tooPowerShell</span><span class="sxs-lookup"><span data-stu-id="e6529-176">Login tooPowerShell</span></span>

    ```powershell
    Login-AzureRmAccount
    ```

1. <span data-ttu-id="e6529-177">Controleer de abonnementen Hallo voor Hallo-account.</span><span class="sxs-lookup"><span data-stu-id="e6529-177">Check hello subscriptions for hello account.</span></span>

    ```powershell
    Get-AzureRmSubscription
    ```

    <span data-ttu-id="e6529-178">Vraag tooauthenticate bent u met uw referenties.</span><span class="sxs-lookup"><span data-stu-id="e6529-178">You are prompted tooauthenticate with your credentials.</span></span>

1. <span data-ttu-id="e6529-179">Kies welke van uw Azure-abonnementen toouse.</span><span class="sxs-lookup"><span data-stu-id="e6529-179">Choose which of your Azure subscriptions toouse.</span></span>

    ```powershell
    Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
    ```

1. <span data-ttu-id="e6529-180">Maak indien nodig een resourcegroep via Hallo **New-AzureResourceGroup** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="e6529-180">If needed, create a resource group by using hello **New-AzureResourceGroup** cmdlet.</span></span> <span data-ttu-id="e6529-181">In de Hallo voorbeeld te volgen, maakt u een resourcegroep met de naam AppgatewayRG op de locatie VS-Oost.</span><span class="sxs-lookup"><span data-stu-id="e6529-181">In hello following example, you create a resource group called AppgatewayRG in East US location.</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name AppgatewayRG -Location "West US"
    ```

1. <span data-ttu-id="e6529-182">Voer Hallo **New-AzureRmResourceGroupDeployment** cmdlet toodeploy Hallo nieuw virtueel netwerk met behulp van Hallo voorafgaand aan de sjabloon en de parameter-bestanden die u hebt gedownload en gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="e6529-182">Run hello **New-AzureRmResourceGroupDeployment** cmdlet toodeploy hello new virtual network by using hello preceding template and parameter files you downloaded and modified.</span></span>
    
    ```powershell
    New-AzureRmResourceGroupDeployment -Name TestAppgatewayDeployment -ResourceGroupName AppgatewayRG `
    -TemplateFile C:\ARM\azuredeploy.json -TemplateParameterFile C:\ARM\azuredeploy-parameters.json
    ```

## <a name="deploy-hello-azure-resource-manager-template-by-using-hello-azure-cli"></a><span data-ttu-id="e6529-183">Hello Azure Resource Manager-sjabloon implementeren met behulp van hello Azure CLI</span><span class="sxs-lookup"><span data-stu-id="e6529-183">Deploy hello Azure Resource Manager template by using hello Azure CLI</span></span>

<span data-ttu-id="e6529-184">toodeploy hello Azure Resource Manager-sjabloon die u hebt gedownload met Azure CLI, volg Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="e6529-184">toodeploy hello Azure Resource Manager template you downloaded by using Azure CLI, follow hello following steps:</span></span>

1. <span data-ttu-id="e6529-185">Als u Azure CLI nog nooit hebt gebruikt, raadpleegt u [installeren en configureren van Azure CLI Hallo](/cli/azure/install-azure-cli) en volg de instructies Hallo toohello punt waar u uw Azure-account en abonnement selecteren.</span><span class="sxs-lookup"><span data-stu-id="e6529-185">If you have never used Azure CLI, see [Install and configure hello Azure CLI](/cli/azure/install-azure-cli) and follow hello instructions up toohello point where you select your Azure account and subscription.</span></span>

1. <span data-ttu-id="e6529-186">Indien nodig, voer hello `az group create` opdracht toocreate een resourcegroep, zoals wordt weergegeven in het volgende codefragment Hallo.</span><span class="sxs-lookup"><span data-stu-id="e6529-186">If necessary, run hello `az group create` command toocreate a resource group, as shown in hello following code snippet.</span></span> <span data-ttu-id="e6529-187">U ziet Hallo-uitvoer van Hallo-opdracht.</span><span class="sxs-lookup"><span data-stu-id="e6529-187">Notice hello output of hello command.</span></span> <span data-ttu-id="e6529-188">Hallo-lijst die wordt weergegeven na Hallo uitvoer wordt uitgelegd Hallo parameters die worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="e6529-188">hello list shown after hello output explains hello parameters used.</span></span> <span data-ttu-id="e6529-189">Zie voor meer informatie over resourcegroepen [Overzicht van Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e6529-189">For more information about resource groups, visit [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>

    ```azurecli
    az group create --location westus --name appgatewayRG
    ```
    
    <span data-ttu-id="e6529-190">**-n (of --naam)**.</span><span class="sxs-lookup"><span data-stu-id="e6529-190">**-n (or --name)**.</span></span> <span data-ttu-id="e6529-191">Naam voor de nieuwe resourcegroep Hallo.</span><span class="sxs-lookup"><span data-stu-id="e6529-191">Name for hello new resource group.</span></span> <span data-ttu-id="e6529-192">In ons scenario is dit *appgatewayRG*.</span><span class="sxs-lookup"><span data-stu-id="e6529-192">For our scenario, it's *appgatewayRG*.</span></span>
    
    <span data-ttu-id="e6529-193">**-l (of --locatie)**.</span><span class="sxs-lookup"><span data-stu-id="e6529-193">**-l (or --location)**.</span></span> <span data-ttu-id="e6529-194">Azure-regio waar de nieuwe resourcegroep hello wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="e6529-194">Azure region where hello new resource group is created.</span></span> <span data-ttu-id="e6529-195">In ons scenario heeft *westus*.</span><span class="sxs-lookup"><span data-stu-id="e6529-195">For our scenario, it's *westus*.</span></span>

1. <span data-ttu-id="e6529-196">Voer Hallo `az group deployment create` cmdlet toodeploy Hallo nieuw virtueel netwerk met behulp van Hallo sjabloon en de parameterbestanden die u hebt gedownload en gewijzigd in de voorgaande stap Hallo.</span><span class="sxs-lookup"><span data-stu-id="e6529-196">Run hello `az group deployment create` cmdlet toodeploy hello new virtual network by using hello template and parameter files you downloaded and modified in hello preceding step.</span></span> <span data-ttu-id="e6529-197">Hallo-lijst die wordt weergegeven na Hallo uitvoer wordt uitgelegd Hallo parameters die worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="e6529-197">hello list shown after hello output explains hello parameters used.</span></span>

    ```azurecli
    az group deployment create --resource-group appgatewayRG --name TestAppgatewayDeployment --template-file azuredeploy.json --parameters @azuredeploy-parameters.json
    ```

## <a name="deploy-hello-azure-resource-manager-template-by-using-click-to-deploy"></a><span data-ttu-id="e6529-198">Hello Azure Resource Manager-sjabloon implementeren met click-to-deploy</span><span class="sxs-lookup"><span data-stu-id="e6529-198">Deploy hello Azure Resource Manager template by using click-to-deploy</span></span>

<span data-ttu-id="e6529-199">Click-to-deploy is een andere manier toouse Azure Resource Manager-sjablonen.</span><span class="sxs-lookup"><span data-stu-id="e6529-199">Click-to-deploy is another way toouse Azure Resource Manager templates.</span></span> <span data-ttu-id="e6529-200">Het is een eenvoudige manier toouse sjablonen Hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="e6529-200">It's an easy way toouse templates with hello Azure portal.</span></span>

1. <span data-ttu-id="e6529-201">Ga te[een toepassingsgateway maken met web application firewall](https://azure.microsoft.com/documentation/templates/101-application-gateway-waf/).</span><span class="sxs-lookup"><span data-stu-id="e6529-201">Go too[Create an application gateway with web application firewall](https://azure.microsoft.com/documentation/templates/101-application-gateway-waf/).</span></span>

1. <span data-ttu-id="e6529-202">Klik op **tooAzure implementeren**.</span><span class="sxs-lookup"><span data-stu-id="e6529-202">Click **Deploy tooAzure**.</span></span>

    ![TooAzure implementeren](./media/application-gateway-create-gateway-arm-template/deploytoazure.png)
    
1. <span data-ttu-id="e6529-204">Vul Hallo parameters voor de implementatiesjabloon Hallo op Hallo-portal en klikt u op **OK**.</span><span class="sxs-lookup"><span data-stu-id="e6529-204">Fill out hello parameters for hello deployment template on hello portal and click **OK**.</span></span>

    ![Parameters](./media/application-gateway-create-gateway-arm-template/ibiza1.png)
    
1. <span data-ttu-id="e6529-206">Selecteer **ik ga akkoord toohello voorwaarden bovengenoemde** en klik op **aankoop**.</span><span class="sxs-lookup"><span data-stu-id="e6529-206">Select **I agree toohello terms and conditions stated above** and click **Purchase**.</span></span>

1. <span data-ttu-id="e6529-207">Klik op de blade voor aangepaste implementatie hello, **maken**.</span><span class="sxs-lookup"><span data-stu-id="e6529-207">On hello Custom deployment blade, click **Create**.</span></span>

## <a name="providing-certificate-data-tooresource-manager-templates"></a><span data-ttu-id="e6529-208">Certificaat gegevens tooResource bieden Manager-sjablonen</span><span class="sxs-lookup"><span data-stu-id="e6529-208">Providing certificate data tooResource Manager templates</span></span>

<span data-ttu-id="e6529-209">Als u SSL met een sjabloon, moet Hallo certificaat toobe opgegeven in een base64-tekenreeks in plaats van wordt geüpload.</span><span class="sxs-lookup"><span data-stu-id="e6529-209">When using SSL with a template, hello certificate needs toobe provided in a base64 string instead of being uploaded.</span></span> <span data-ttu-id="e6529-210">tooconvert een .pfx- of .cer tooa base64-tekenreeks gebruik een van de volgende opdrachten Hallo.</span><span class="sxs-lookup"><span data-stu-id="e6529-210">tooconvert a .pfx or .cer tooa base64 string use one of hello following commands.</span></span> <span data-ttu-id="e6529-211">Hallo converteren volgende opdrachten Hallo certificaat tooa base64-tekenreeks, die toohello sjabloon kan worden opgegeven.</span><span class="sxs-lookup"><span data-stu-id="e6529-211">hello following commands convert hello certificate tooa base64 string, which can be provided toohello template.</span></span> <span data-ttu-id="e6529-212">Hallo verwacht uitvoer is een tekenreeks die kan worden opgeslagen in een variabele en geplakt in Hallo-sjabloon.</span><span class="sxs-lookup"><span data-stu-id="e6529-212">hello expected output is a string that can be stored in a variable and pasted in hello template.</span></span>

### <a name="macos"></a><span data-ttu-id="e6529-213">macOS</span><span class="sxs-lookup"><span data-stu-id="e6529-213">macOS</span></span>
```bash
cert=$( base64 <certificate path and name>.pfx )
echo $cert
```

### <a name="windows"></a><span data-ttu-id="e6529-214">Windows</span><span class="sxs-lookup"><span data-stu-id="e6529-214">Windows</span></span>
```powershell
[System.Convert]::ToBase64String([System.IO.File]::ReadAllBytes("<certificate path and name>.pfx"))
```

## <a name="delete-all-resources"></a><span data-ttu-id="e6529-215">Alle resources verwijderen</span><span class="sxs-lookup"><span data-stu-id="e6529-215">Delete all resources</span></span>

<span data-ttu-id="e6529-216">toodelete alle resources die worden gemaakt in dit artikel wordt voltooid één Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="e6529-216">toodelete all resources created in this article, complete one of hello following steps:</span></span>

### <a name="powershell"></a><span data-ttu-id="e6529-217">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e6529-217">PowerShell</span></span>

```powershell
Remove-AzureRmResourceGroup -Name appgatewayRG
```

### <a name="azure-cli"></a><span data-ttu-id="e6529-218">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="e6529-218">Azure CLI</span></span>

```azurecli
az group delete --name appgatewayRG
```

## <a name="next-steps"></a><span data-ttu-id="e6529-219">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="e6529-219">Next steps</span></span>

<span data-ttu-id="e6529-220">Als u wilt dat tooconfigure SSL-offload, gaat u naar: [een toepassingsgateway voor SSL-offload configureren](application-gateway-ssl.md).</span><span class="sxs-lookup"><span data-stu-id="e6529-220">If you want tooconfigure SSL offload, visit: [Configure an application gateway for SSL offload](application-gateway-ssl.md).</span></span>

<span data-ttu-id="e6529-221">Als u wilt dat tooconfigure een toouse application gateway met een interne load balancer, gaat u naar: [een toepassingsgateway maken met een interne load balancer (ILB)](application-gateway-ilb.md).</span><span class="sxs-lookup"><span data-stu-id="e6529-221">If you want tooconfigure an application gateway toouse with an internal load balancer, visit: [Create an application gateway with an internal load balancer (ILB)](application-gateway-ilb.md).</span></span>

<span data-ttu-id="e6529-222">Als u meer informatie wilt over de algemene opties voor taakverdeling, gaat u naar:</span><span class="sxs-lookup"><span data-stu-id="e6529-222">If you want more information about load balancing options in general, visit:</span></span>

* [<span data-ttu-id="e6529-223">Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="e6529-223">Azure Load Balancer</span></span>](https://azure.microsoft.com/documentation/services/load-balancer/)
* [<span data-ttu-id="e6529-224">Azure Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="e6529-224">Azure Traffic Manager</span></span>](https://azure.microsoft.com/documentation/services/traffic-manager/)


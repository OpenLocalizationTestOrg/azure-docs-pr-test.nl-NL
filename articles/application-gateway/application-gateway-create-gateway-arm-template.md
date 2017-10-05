---
title: Een toepassingsgateway met Azure - sjablonen maken | Microsoft Docs
description: Op deze pagina staan instructies voor het maken van een toepassingsgateway met de Azure Resource Manager-sjabloon
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
ms.openlocfilehash: 46cca89ccb5bd77d57fabc3e9027fcebd38da8e7
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="create-an-application-gateway-by-using-the-azure-resource-manager-template"></a><span data-ttu-id="c6c03-103">Een toepassingsgateway maken met de Azure Resource Manager-sjabloon</span><span class="sxs-lookup"><span data-stu-id="c6c03-103">Create an application gateway by using the Azure Resource Manager template</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="c6c03-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="c6c03-104">Azure portal</span></span>](application-gateway-create-gateway-portal.md)
> * [<span data-ttu-id="c6c03-105">Azure Resource Manager PowerShell</span><span class="sxs-lookup"><span data-stu-id="c6c03-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-gateway-arm.md)
> * [<span data-ttu-id="c6c03-106">Azure Classic PowerShell</span><span class="sxs-lookup"><span data-stu-id="c6c03-106">Azure Classic PowerShell</span></span>](application-gateway-create-gateway.md)
> * [<span data-ttu-id="c6c03-107">Azure Resource Manager-sjabloon</span><span class="sxs-lookup"><span data-stu-id="c6c03-107">Azure Resource Manager template</span></span>](application-gateway-create-gateway-arm-template.md)
> * [<span data-ttu-id="c6c03-108">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="c6c03-108">Azure CLI</span></span>](application-gateway-create-gateway-cli.md)

<span data-ttu-id="c6c03-109">Azure Application Gateway is een load balancer in laag 7.</span><span class="sxs-lookup"><span data-stu-id="c6c03-109">Azure Application Gateway is a layer-7 load balancer.</span></span> <span data-ttu-id="c6c03-110">De gateway biedt opties voor failovers en het routeren van HTTP-aanvragen tussen servers (on-premises en in de cloud).</span><span class="sxs-lookup"><span data-stu-id="c6c03-110">It provides failover and performance-routing HTTP requests between different servers, whether they are on the cloud or on-premises.</span></span> <span data-ttu-id="c6c03-111">Application Gateway bevat veel ADC-functies (Application Delivery Controller), waaronder HTTP-taakverdeling, op cookies gebaseerde sessieaffiniteit, SSL-offload (Secure Sockets Layer), aangepaste statustests en ondersteuning voor meerdere locaties.</span><span class="sxs-lookup"><span data-stu-id="c6c03-111">Application Gateway provides many application delivery controller (ADC) features including HTTP load balancing, cookie-based session affinity, Secure Sockets Layer (SSL) offload, custom health probes, support for multi-site, and many others.</span></span> <span data-ttu-id="c6c03-112">Ga voor een volledige lijst met ondersteunde functies naar [Application Gateway-overzicht](application-gateway-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="c6c03-112">To find a complete list of supported features, visit [Application Gateway overview](application-gateway-introduction.md)</span></span>

<span data-ttu-id="c6c03-113">Dit artikel begeleidt u bij het downloaden en wijzigen van een bestaande Azure Resource Manager-sjabloon vanuit GitHub en implementeren van de sjabloon vanuit GitHub, PowerShell en de Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="c6c03-113">This article walks you through downloading and modifying an existing Azure Resource Manager template from GitHub and deploying the template from GitHub, PowerShell, and the Azure CLI.</span></span>

<span data-ttu-id="c6c03-114">Als u de Azure Resource Manager-sjabloon rechtstreeks vanuit GitHub wilt implementeren zonder deze te wijzigen, gaat u naar Een sjabloon implementeren vanuit GitHub.</span><span class="sxs-lookup"><span data-stu-id="c6c03-114">If you are simply deploying the Azure Resource Manager template directly from GitHub without any changes, skip to deploy a template from GitHub.</span></span>

## <a name="scenario"></a><span data-ttu-id="c6c03-115">Scenario</span><span class="sxs-lookup"><span data-stu-id="c6c03-115">Scenario</span></span>

<span data-ttu-id="c6c03-116">In dit scenario:</span><span class="sxs-lookup"><span data-stu-id="c6c03-116">In this scenario you will:</span></span>

* <span data-ttu-id="c6c03-117">Een toepassingsgateway maken met web application firewall.</span><span class="sxs-lookup"><span data-stu-id="c6c03-117">Create an application gateway with web application firewall.</span></span>
* <span data-ttu-id="c6c03-118">Maakt u een virtueel netwerk met de naam VirtualNetwork1 met een gereserveerd CIDR-blok van 10.0.0.0/16.</span><span class="sxs-lookup"><span data-stu-id="c6c03-118">Create a virtual network named VirtualNetwork1 with a reserved CIDR block of 10.0.0.0/16.</span></span>
* <span data-ttu-id="c6c03-119">Maakt u een subnet met de naam Appgatewaysubnet dat gebruikmaakt van 10.0.0.0/28 als CIDR-blok.</span><span class="sxs-lookup"><span data-stu-id="c6c03-119">Create a subnet called Appgatewaysubnet that uses 10.0.0.0/28 as its CIDR block.</span></span>
* <span data-ttu-id="c6c03-120">Stelt u twee eerder geconfigureerde back-end-IP-adressen in voor de webservers die load balancing moeten verzorgen voor het verkeer.</span><span class="sxs-lookup"><span data-stu-id="c6c03-120">Set up two previously configured back-end IPs for the web servers you want to load balance the traffic.</span></span> <span data-ttu-id="c6c03-121">In deze voorbeeldsjabloon worden de back-end-IP-adressen 10.0.1.10 en 10.0.1.11 gebruikt.</span><span class="sxs-lookup"><span data-stu-id="c6c03-121">In this template example, the back-end IPs are 10.0.1.10 and 10.0.1.11.</span></span>

> [!NOTE]
> <span data-ttu-id="c6c03-122">Deze instellingen zijn de parameters voor deze sjabloon.</span><span class="sxs-lookup"><span data-stu-id="c6c03-122">Those settings are the parameters for this template.</span></span> <span data-ttu-id="c6c03-123">U kunt regels, de listener, SSL en andere opties in het bestand azuredeploy.json wijzigen voor het aanpassen van de sjabloon.</span><span class="sxs-lookup"><span data-stu-id="c6c03-123">To customize the template, you can change rules, the listener, SSL, and other options in the azuredeploy.json file.</span></span>

![Scenario](./media/application-gateway-create-gateway-arm-template/scenario.png)

## <a name="download-and-understand-the-azure-resource-manager-template"></a><span data-ttu-id="c6c03-125">De Azure Resource Manager-sjabloon downloaden en begrijpen</span><span class="sxs-lookup"><span data-stu-id="c6c03-125">Download and understand the Azure Resource Manager template</span></span>

<span data-ttu-id="c6c03-126">U kunt de bestaande Azure Resource Manager-sjabloon downloaden om een virtueel netwerk en twee subnets vanuit GitHub te maken. Vervolgens kunt u wijzigingen aanbrengen en de sjabloon opnieuw gebruiken.</span><span class="sxs-lookup"><span data-stu-id="c6c03-126">You can download the existing Azure Resource Manager template to create a virtual network and two subnets from GitHub, make any changes you might want, and reuse it.</span></span> <span data-ttu-id="c6c03-127">Volg hiervoor de volgende stappen:</span><span class="sxs-lookup"><span data-stu-id="c6c03-127">To do so, use the following steps:</span></span>

1. <span data-ttu-id="c6c03-128">Navigeer naar [toepassingsgateway maken met web application firewall ingeschakeld](https://github.com/Azure/azure-quickstart-templates/tree/master/101-application-gateway-waf).</span><span class="sxs-lookup"><span data-stu-id="c6c03-128">Navigate to [Create Application Gateway with web application firewall enabled](https://github.com/Azure/azure-quickstart-templates/tree/master/101-application-gateway-waf).</span></span>
1. <span data-ttu-id="c6c03-129">Klik op **azuredeploy.json** en vervolgens op **RAW**.</span><span class="sxs-lookup"><span data-stu-id="c6c03-129">Click **azuredeploy.json**, and then click **RAW**.</span></span>
1. <span data-ttu-id="c6c03-130">Sla het bestand op in een lokale map op uw computer.</span><span class="sxs-lookup"><span data-stu-id="c6c03-130">Save the file to a local folder on your computer.</span></span>
1. <span data-ttu-id="c6c03-131">Als u bekend bent met Azure Resource Manager-sjablonen, kunt u doorgaan naar stap 7.</span><span class="sxs-lookup"><span data-stu-id="c6c03-131">If you are familiar with Azure Resource Manager templates, skip to step 7.</span></span>
1. <span data-ttu-id="c6c03-132">Open het bestand dat u hebt opgeslagen en bekijk de inhoud onder **parameters** in regel</span><span class="sxs-lookup"><span data-stu-id="c6c03-132">Open the file that you saved and look at the contents under **parameters** in line</span></span>
1. <span data-ttu-id="c6c03-133">Azure Resource Manager-sjabloonparameters bieden een tijdelijke aanduiding voor waarden die kunnen worden ingevuld tijdens de implementatie.</span><span class="sxs-lookup"><span data-stu-id="c6c03-133">Azure Resource Manager template parameters provide a placeholder for values that can be filled out during deployment.</span></span>

  | <span data-ttu-id="c6c03-134">Parameter</span><span class="sxs-lookup"><span data-stu-id="c6c03-134">Parameter</span></span> | <span data-ttu-id="c6c03-135">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="c6c03-135">Description</span></span> |
  | --- | --- |
  | <span data-ttu-id="c6c03-136">**subnetPrefix**</span><span class="sxs-lookup"><span data-stu-id="c6c03-136">**subnetPrefix**</span></span> |<span data-ttu-id="c6c03-137">CIDR-blokkering voor het subnet voor de toepassingsgateway.</span><span class="sxs-lookup"><span data-stu-id="c6c03-137">CIDR block for the application gateway subnet.</span></span> |
  | <span data-ttu-id="c6c03-138">**applicationGatewaySize**</span><span class="sxs-lookup"><span data-stu-id="c6c03-138">**applicationGatewaySize**</span></span> | <span data-ttu-id="c6c03-139">Grootte van de toepassingsgateway.</span><span class="sxs-lookup"><span data-stu-id="c6c03-139">Size of the application gateway.</span></span>  <span data-ttu-id="c6c03-140">WAF kunt alleen middelgrote en grote.</span><span class="sxs-lookup"><span data-stu-id="c6c03-140">WAF only allows medium and large.</span></span> |
  | <span data-ttu-id="c6c03-141">**backendIpaddress1**</span><span class="sxs-lookup"><span data-stu-id="c6c03-141">**backendIpaddress1**</span></span> |<span data-ttu-id="c6c03-142">IP-adres van de eerste webserver.</span><span class="sxs-lookup"><span data-stu-id="c6c03-142">IP address of the first web server.</span></span> |
  | <span data-ttu-id="c6c03-143">**backendIpaddress2**</span><span class="sxs-lookup"><span data-stu-id="c6c03-143">**backendIpaddress2**</span></span> |<span data-ttu-id="c6c03-144">IP-adres van de tweede webserver.</span><span class="sxs-lookup"><span data-stu-id="c6c03-144">IP address of the second web server.</span></span> |
  | <span data-ttu-id="c6c03-145">**wafEnabled**</span><span class="sxs-lookup"><span data-stu-id="c6c03-145">**wafEnabled**</span></span> | <span data-ttu-id="c6c03-146">Instelling om te bepalen of WAF is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="c6c03-146">Setting to determine if WAF is enabled.</span></span>|
  | <span data-ttu-id="c6c03-147">**wafMode**</span><span class="sxs-lookup"><span data-stu-id="c6c03-147">**wafMode**</span></span> | <span data-ttu-id="c6c03-148">Modus van de web application firewall.</span><span class="sxs-lookup"><span data-stu-id="c6c03-148">Mode of the web application firewall.</span></span>  <span data-ttu-id="c6c03-149">Beschikbare opties zijn **preventie** of **detectie**.</span><span class="sxs-lookup"><span data-stu-id="c6c03-149">Available options are **prevention** or **detection**.</span></span>|
  | <span data-ttu-id="c6c03-150">**wafRuleSetType**</span><span class="sxs-lookup"><span data-stu-id="c6c03-150">**wafRuleSetType**</span></span> | <span data-ttu-id="c6c03-151">RuleSet-type voor WAF.</span><span class="sxs-lookup"><span data-stu-id="c6c03-151">Ruleset type for WAF.</span></span>  <span data-ttu-id="c6c03-152">OWASP is momenteel de enige ondersteunde optie.</span><span class="sxs-lookup"><span data-stu-id="c6c03-152">Currently OWASP is the only supported option.</span></span> |
  | <span data-ttu-id="c6c03-153">**wafRuleSetVersion**</span><span class="sxs-lookup"><span data-stu-id="c6c03-153">**wafRuleSetVersion**</span></span> |<span data-ttu-id="c6c03-154">RuleSet-versie.</span><span class="sxs-lookup"><span data-stu-id="c6c03-154">Ruleset version.</span></span> <span data-ttu-id="c6c03-155">OWASP CRS 2.2.9 en 3.0 zijn momenteel ondersteunde opties.</span><span class="sxs-lookup"><span data-stu-id="c6c03-155">OWASP CRS 2.2.9 and 3.0 are currently the supported options.</span></span> |

1. <span data-ttu-id="c6c03-156">Controleer de inhoud onder **resources** en Let op de volgende eigenschappen:</span><span class="sxs-lookup"><span data-stu-id="c6c03-156">Check the content under **resources** and notice the following properties:</span></span>

   * <span data-ttu-id="c6c03-157">**type**.</span><span class="sxs-lookup"><span data-stu-id="c6c03-157">**type**.</span></span> <span data-ttu-id="c6c03-158">Het type resource dat door de sjabloon wordt aangemaakt.</span><span class="sxs-lookup"><span data-stu-id="c6c03-158">Type of resource being created by the template.</span></span> <span data-ttu-id="c6c03-159">In dit geval wordt het type is `Microsoft.Network/applicationGateways`, die staat voor een toepassingsgateway.</span><span class="sxs-lookup"><span data-stu-id="c6c03-159">In this case, the type is `Microsoft.Network/applicationGateways`, which represents an application gateway.</span></span>
   * <span data-ttu-id="c6c03-160">**Naam**.</span><span class="sxs-lookup"><span data-stu-id="c6c03-160">**name**.</span></span> <span data-ttu-id="c6c03-161">Naam voor de resource.</span><span class="sxs-lookup"><span data-stu-id="c6c03-161">Name for the resource.</span></span> <span data-ttu-id="c6c03-162">Let op het gebruik van `[parameters('applicationGatewayName')]`, wat betekent dat de naam is opgegeven als invoer door u of door een parameterbestand tijdens de implementatie.</span><span class="sxs-lookup"><span data-stu-id="c6c03-162">Notice the use of `[parameters('applicationGatewayName')]`, which means that the name is provided as input by you or by a parameter file during deployment.</span></span>
   * <span data-ttu-id="c6c03-163">**Eigenschappen**.</span><span class="sxs-lookup"><span data-stu-id="c6c03-163">**properties**.</span></span> <span data-ttu-id="c6c03-164">Lijst met eigenschappen voor de resource.</span><span class="sxs-lookup"><span data-stu-id="c6c03-164">List of properties for the resource.</span></span> <span data-ttu-id="c6c03-165">Deze sjabloon maakt tijdens het maken van de toepassingsgateway gebruik van het virtuele netwerk en het openbare IP-adres.</span><span class="sxs-lookup"><span data-stu-id="c6c03-165">This template uses the virtual network and public IP address during application gateway creation.</span></span>

   > [!NOTE]
   > <span data-ttu-id="c6c03-166">Voor meer informatie over sjablonen gaat u naar: [verwijzing naar Resource Manager-sjablonen](/templates/)</span><span class="sxs-lookup"><span data-stu-id="c6c03-166">For more information on templates visit: [Resource Manager templates reference](/templates/)</span></span>

1. <span data-ttu-id="c6c03-167">Ga terug naar [https://github.com/Azure/azure-quickstart-templates/blob/master/101-application-gateway-waf/](https://github.com/Azure/azure-quickstart-templates/blob/master/101-application-gateway-waf).</span><span class="sxs-lookup"><span data-stu-id="c6c03-167">Navigate back to [https://github.com/Azure/azure-quickstart-templates/blob/master/101-application-gateway-waf/](https://github.com/Azure/azure-quickstart-templates/blob/master/101-application-gateway-waf).</span></span>
1. <span data-ttu-id="c6c03-168">Klik op **azuredeploy-parameters.json**, en klik vervolgens op **RAW**.</span><span class="sxs-lookup"><span data-stu-id="c6c03-168">Click **azuredeploy-parameters.json**, and then click **RAW**.</span></span>
1. <span data-ttu-id="c6c03-169">Sla het bestand op in een lokale map op uw computer.</span><span class="sxs-lookup"><span data-stu-id="c6c03-169">Save the file to a local folder on your computer.</span></span>
1. <span data-ttu-id="c6c03-170">Open het bestand dat u hebt opgeslagen en bewerk de waarden voor de parameters.</span><span class="sxs-lookup"><span data-stu-id="c6c03-170">Open the file that you saved and edit the values for the parameters.</span></span> <span data-ttu-id="c6c03-171">Gebruik de volgende waarden voor het implementeren van de toepassingsgateway die in ons scenario wordt beschreven.</span><span class="sxs-lookup"><span data-stu-id="c6c03-171">Use the following values to deploy the application gateway described in our scenario.</span></span>

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

1. <span data-ttu-id="c6c03-172">Sla het bestand op.</span><span class="sxs-lookup"><span data-stu-id="c6c03-172">Save the file.</span></span> <span data-ttu-id="c6c03-173">U kunt de JSON-sjabloon en parametersjabloon testen met online JSON-validatiehulpprogramma’s zoals [JSlint.com](http://www.jslint.com/).</span><span class="sxs-lookup"><span data-stu-id="c6c03-173">You can test the JSON template and parameter template by using online JSON validation tools like [JSlint.com](http://www.jslint.com/).</span></span>

## <a name="deploy-the-azure-resource-manager-template-by-using-powershell"></a><span data-ttu-id="c6c03-174">De Azure Resource Manager-sjabloon implementeren met PowerShell</span><span class="sxs-lookup"><span data-stu-id="c6c03-174">Deploy the Azure Resource Manager template by using PowerShell</span></span>

<span data-ttu-id="c6c03-175">Als u Azure PowerShell nog nooit hebt gebruikt, gaat u naar: [installeren en configureren van Azure PowerShell](/powershell/azure/overview) en volg de instructies om te melden bij Azure en uw abonnement te selecteren.</span><span class="sxs-lookup"><span data-stu-id="c6c03-175">If you have never used Azure PowerShell, visit: [How to install and configure Azure PowerShell](/powershell/azure/overview) and follow the instructions to sign into Azure and select your subscription.</span></span>

1. <span data-ttu-id="c6c03-176">Meld u aan bij PowerShell</span><span class="sxs-lookup"><span data-stu-id="c6c03-176">Login to PowerShell</span></span>

    ```powershell
    Login-AzureRmAccount
    ```

1. <span data-ttu-id="c6c03-177">Controleer de abonnementen voor het account.</span><span class="sxs-lookup"><span data-stu-id="c6c03-177">Check the subscriptions for the account.</span></span>

    ```powershell
    Get-AzureRmSubscription
    ```

    <span data-ttu-id="c6c03-178">U wordt gevraagd om u te verifiëren met uw referenties.</span><span class="sxs-lookup"><span data-stu-id="c6c03-178">You are prompted to authenticate with your credentials.</span></span>

1. <span data-ttu-id="c6c03-179">Kies welk Azure-abonnement u wilt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="c6c03-179">Choose which of your Azure subscriptions to use.</span></span>

    ```powershell
    Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
    ```

1. <span data-ttu-id="c6c03-180">Indien nodig kunt u een resourcegroep maken met de cmdlet **New-AzureResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="c6c03-180">If needed, create a resource group by using the **New-AzureResourceGroup** cmdlet.</span></span> <span data-ttu-id="c6c03-181">In het volgende voorbeeld maakt u een resourcegroep met de naam AppgatewayRG op de locatie VS - oost.</span><span class="sxs-lookup"><span data-stu-id="c6c03-181">In the following example, you create a resource group called AppgatewayRG in East US location.</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name AppgatewayRG -Location "West US"
    ```

1. <span data-ttu-id="c6c03-182">Voer de cmdlet **New-AzureRmResourceGroupDeployment** uit om het nieuwe virtuele netwerk te implementeren met de vorige sjabloon en parameterbestanden die u hebt gedownload en gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="c6c03-182">Run the **New-AzureRmResourceGroupDeployment** cmdlet to deploy the new virtual network by using the preceding template and parameter files you downloaded and modified.</span></span>
    
    ```powershell
    New-AzureRmResourceGroupDeployment -Name TestAppgatewayDeployment -ResourceGroupName AppgatewayRG `
    -TemplateFile C:\ARM\azuredeploy.json -TemplateParameterFile C:\ARM\azuredeploy-parameters.json
    ```

## <a name="deploy-the-azure-resource-manager-template-by-using-the-azure-cli"></a><span data-ttu-id="c6c03-183">De Azure Resource Manager-sjabloon implementeren met de Azure CLI</span><span class="sxs-lookup"><span data-stu-id="c6c03-183">Deploy the Azure Resource Manager template by using the Azure CLI</span></span>

<span data-ttu-id="c6c03-184">Volg de volgende stappen uit voor het implementeren van de Azure Resource Manager-sjabloon die u hebt gedownload met Azure CLI:</span><span class="sxs-lookup"><span data-stu-id="c6c03-184">To deploy the Azure Resource Manager template you downloaded by using Azure CLI, follow the following steps:</span></span>

1. <span data-ttu-id="c6c03-185">Als u Azure CLI nog nooit hebt gebruikt, raadpleegt u [De Azure CLI installeren en configureren](/cli/azure/install-azure-cli) en volgt u de instructies tot het punt waar u uw Azure-account en -abonnement moet selecteren.</span><span class="sxs-lookup"><span data-stu-id="c6c03-185">If you have never used Azure CLI, see [Install and configure the Azure CLI](/cli/azure/install-azure-cli) and follow the instructions up to the point where you select your Azure account and subscription.</span></span>

1. <span data-ttu-id="c6c03-186">Voer indien nodig de `az group create` opdracht voor het maken van een resourcegroep, zoals wordt weergegeven in het volgende codefragment.</span><span class="sxs-lookup"><span data-stu-id="c6c03-186">If necessary, run the `az group create` command to create a resource group, as shown in the following code snippet.</span></span> <span data-ttu-id="c6c03-187">Hier ziet u de uitvoer van de opdracht.</span><span class="sxs-lookup"><span data-stu-id="c6c03-187">Notice the output of the command.</span></span> <span data-ttu-id="c6c03-188">De lijst die na de uitvoer wordt weergegeven, beschrijft de gebruikte parameters.</span><span class="sxs-lookup"><span data-stu-id="c6c03-188">The list shown after the output explains the parameters used.</span></span> <span data-ttu-id="c6c03-189">Zie voor meer informatie over resourcegroepen [Overzicht van Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c6c03-189">For more information about resource groups, visit [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>

    ```azurecli
    az group create --location westus --name appgatewayRG
    ```
    
    <span data-ttu-id="c6c03-190">**-n (of --name)**.</span><span class="sxs-lookup"><span data-stu-id="c6c03-190">**-n (or --name)**.</span></span> <span data-ttu-id="c6c03-191">Naam voor de nieuwe resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="c6c03-191">Name for the new resource group.</span></span> <span data-ttu-id="c6c03-192">In ons scenario is dit *appgatewayRG*.</span><span class="sxs-lookup"><span data-stu-id="c6c03-192">For our scenario, it's *appgatewayRG*.</span></span>
    
    <span data-ttu-id="c6c03-193">**-l (of --location)**.</span><span class="sxs-lookup"><span data-stu-id="c6c03-193">**-l (or --location)**.</span></span> <span data-ttu-id="c6c03-194">De Azure-regio waar de nieuwe resourcegroep wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="c6c03-194">Azure region where the new resource group is created.</span></span> <span data-ttu-id="c6c03-195">In ons scenario heeft *westus*.</span><span class="sxs-lookup"><span data-stu-id="c6c03-195">For our scenario, it's *westus*.</span></span>

1. <span data-ttu-id="c6c03-196">Voer de `az group deployment create` cmdlet voor het implementeren van het nieuwe virtuele netwerk met behulp van de sjabloon en de parameterbestanden die u hebt gedownload en gewijzigd in de vorige stap.</span><span class="sxs-lookup"><span data-stu-id="c6c03-196">Run the `az group deployment create` cmdlet to deploy the new virtual network by using the template and parameter files you downloaded and modified in the preceding step.</span></span> <span data-ttu-id="c6c03-197">De lijst die na de uitvoer wordt weergegeven, beschrijft de gebruikte parameters.</span><span class="sxs-lookup"><span data-stu-id="c6c03-197">The list shown after the output explains the parameters used.</span></span>

    ```azurecli
    az group deployment create --resource-group appgatewayRG --name TestAppgatewayDeployment --template-file azuredeploy.json --parameters @azuredeploy-parameters.json
    ```

## <a name="deploy-the-azure-resource-manager-template-by-using-click-to-deploy"></a><span data-ttu-id="c6c03-198">De Azure Resource Manager-sjabloon implementeren met click-to-deploy</span><span class="sxs-lookup"><span data-stu-id="c6c03-198">Deploy the Azure Resource Manager template by using click-to-deploy</span></span>

<span data-ttu-id="c6c03-199">U kunt de Azure Resource Manager-sjablonen ook gebruiken via click-to-deploy.</span><span class="sxs-lookup"><span data-stu-id="c6c03-199">Click-to-deploy is another way to use Azure Resource Manager templates.</span></span> <span data-ttu-id="c6c03-200">Dit is een eenvoudige manier om sjablonen te gebruiken in de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="c6c03-200">It's an easy way to use templates with the Azure portal.</span></span>

1. <span data-ttu-id="c6c03-201">Ga naar [een toepassingsgateway maken met web application firewall](https://azure.microsoft.com/documentation/templates/101-application-gateway-waf/).</span><span class="sxs-lookup"><span data-stu-id="c6c03-201">Go to [Create an application gateway with web application firewall](https://azure.microsoft.com/documentation/templates/101-application-gateway-waf/).</span></span>

1. <span data-ttu-id="c6c03-202">Klik op **Implementeren in Azure**.</span><span class="sxs-lookup"><span data-stu-id="c6c03-202">Click **Deploy to Azure**.</span></span>

    ![Implementeren in Azure](./media/application-gateway-create-gateway-arm-template/deploytoazure.png)
    
1. <span data-ttu-id="c6c03-204">Vul de parameters voor de implementatiesjabloon in in de portal en klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="c6c03-204">Fill out the parameters for the deployment template on the portal and click **OK**.</span></span>

    ![Parameters](./media/application-gateway-create-gateway-arm-template/ibiza1.png)
    
1. <span data-ttu-id="c6c03-206">Selecteer **ik ga akkoord met de voorwaarden en bepalingen hierboven** en klik op **aankoop**.</span><span class="sxs-lookup"><span data-stu-id="c6c03-206">Select **I agree to the terms and conditions stated above** and click **Purchase**.</span></span>

1. <span data-ttu-id="c6c03-207">Klik op de blade voor aangepaste implementatie en klik op **Maken**.</span><span class="sxs-lookup"><span data-stu-id="c6c03-207">On the Custom deployment blade, click **Create**.</span></span>

## <a name="providing-certificate-data-to-resource-manager-templates"></a><span data-ttu-id="c6c03-208">Certificaat-gegevens voor Resource Manager-sjablonen</span><span class="sxs-lookup"><span data-stu-id="c6c03-208">Providing certificate data to Resource Manager templates</span></span>

<span data-ttu-id="c6c03-209">Als u SSL met een sjabloon, wordt het certificaat moet worden opgegeven in een base64-tekenreeks in plaats van wordt geüpload.</span><span class="sxs-lookup"><span data-stu-id="c6c03-209">When using SSL with a template, the certificate needs to be provided in a base64 string instead of being uploaded.</span></span> <span data-ttu-id="c6c03-210">Als u wilt converteren gebruik een .pfx- of .cer naar een base64-tekenreeks een van de volgende opdrachten.</span><span class="sxs-lookup"><span data-stu-id="c6c03-210">To convert a .pfx or .cer to a base64 string use one of the following commands.</span></span> <span data-ttu-id="c6c03-211">Het certificaat converteren de volgende opdrachten naar een base64-tekenreeks kan worden opgegeven voor de sjabloon.</span><span class="sxs-lookup"><span data-stu-id="c6c03-211">The following commands convert the certificate to a base64 string, which can be provided to the template.</span></span> <span data-ttu-id="c6c03-212">De verwachte uitvoer is een tekenreeks die kan worden opgeslagen in een variabele en geplakt in de sjabloon.</span><span class="sxs-lookup"><span data-stu-id="c6c03-212">The expected output is a string that can be stored in a variable and pasted in the template.</span></span>

### <a name="macos"></a><span data-ttu-id="c6c03-213">macOS</span><span class="sxs-lookup"><span data-stu-id="c6c03-213">macOS</span></span>
```bash
cert=$( base64 <certificate path and name>.pfx )
echo $cert
```

### <a name="windows"></a><span data-ttu-id="c6c03-214">Windows</span><span class="sxs-lookup"><span data-stu-id="c6c03-214">Windows</span></span>
```powershell
[System.Convert]::ToBase64String([System.IO.File]::ReadAllBytes("<certificate path and name>.pfx"))
```

## <a name="delete-all-resources"></a><span data-ttu-id="c6c03-215">Alle resources verwijderen</span><span class="sxs-lookup"><span data-stu-id="c6c03-215">Delete all resources</span></span>

<span data-ttu-id="c6c03-216">Voor het verwijderen van alle resources in dit artikel hebt gemaakt, voert u een van de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="c6c03-216">To delete all resources created in this article, complete one of the following steps:</span></span>

### <a name="powershell"></a><span data-ttu-id="c6c03-217">PowerShell</span><span class="sxs-lookup"><span data-stu-id="c6c03-217">PowerShell</span></span>

```powershell
Remove-AzureRmResourceGroup -Name appgatewayRG
```

### <a name="azure-cli"></a><span data-ttu-id="c6c03-218">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="c6c03-218">Azure CLI</span></span>

```azurecli
az group delete --name appgatewayRG
```

## <a name="next-steps"></a><span data-ttu-id="c6c03-219">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="c6c03-219">Next steps</span></span>

<span data-ttu-id="c6c03-220">Ga naar: [Configure an application gateway for SSL offload](application-gateway-ssl.md) (Een toepassingsgateway voor SSL-offload configureren) als u SSL-offload wilt configureren.</span><span class="sxs-lookup"><span data-stu-id="c6c03-220">If you want to configure SSL offload, visit: [Configure an application gateway for SSL offload](application-gateway-ssl.md).</span></span>

<span data-ttu-id="c6c03-221">Ga naar: [Create an application gateway with an internal load balancer (ILB)](application-gateway-ilb.md) (Een toepassingsgateway met een interne load balancer (ILB) maken) als u een toepassingsgateway wilt configureren voor gebruik met een interne load balancer.</span><span class="sxs-lookup"><span data-stu-id="c6c03-221">If you want to configure an application gateway to use with an internal load balancer, visit: [Create an application gateway with an internal load balancer (ILB)](application-gateway-ilb.md).</span></span>

<span data-ttu-id="c6c03-222">Als u meer informatie wilt over de algemene opties voor taakverdeling, gaat u naar:</span><span class="sxs-lookup"><span data-stu-id="c6c03-222">If you want more information about load balancing options in general, visit:</span></span>

* [<span data-ttu-id="c6c03-223">Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="c6c03-223">Azure Load Balancer</span></span>](https://azure.microsoft.com/documentation/services/load-balancer/)
* [<span data-ttu-id="c6c03-224">Azure Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="c6c03-224">Azure Traffic Manager</span></span>](https://azure.microsoft.com/documentation/services/traffic-manager/)


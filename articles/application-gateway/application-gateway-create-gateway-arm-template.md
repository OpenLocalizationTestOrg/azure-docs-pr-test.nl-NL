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
# <a name="create-an-application-gateway-by-using-hello-azure-resource-manager-template"></a>Een toepassingsgateway maken met behulp van hello Azure Resource Manager-sjabloon

> [!div class="op_single_selector"]
> * [Azure Portal](application-gateway-create-gateway-portal.md)
> * [Azure Resource Manager PowerShell](application-gateway-create-gateway-arm.md)
> * [Azure Classic PowerShell](application-gateway-create-gateway.md)
> * [Azure Resource Manager-sjabloon](application-gateway-create-gateway-arm-template.md)
> * [Azure CLI](application-gateway-create-gateway-cli.md)

Azure Application Gateway is een load balancer in laag 7. Het biedt de failover- en HTTP-aanvragen routeren tussen verschillende servers, ongeacht of deze op Hallo cloud of on-premises. Application Gateway bevat veel ADC-functies (Application Delivery Controller), waaronder HTTP-taakverdeling, op cookies gebaseerde sessieaffiniteit, SSL-offload (Secure Sockets Layer), aangepaste statustests en ondersteuning voor meerdere locaties. toofind een volledige lijst van ondersteunde functies, gaat u naar [Application Gateway-overzicht](application-gateway-introduction.md)

Dit artikel begeleidt u bij het downloaden en wijzigen van een bestaande Azure Resource Manager-sjabloon vanuit GitHub en Hallo sjabloon vanuit GitHub, PowerShell en Azure CLI Hallo implementeren.

Als u hello Azure Resource Manager-sjabloon rechtstreeks vanuit GitHub zonder wijzigingen wilt implementeren, slaat u een sjabloon toodeploy vanuit GitHub.

## <a name="scenario"></a>Scenario

In dit scenario:

* Een toepassingsgateway maken met web application firewall.
* Maakt u een virtueel netwerk met de naam VirtualNetwork1 met een gereserveerd CIDR-blok van 10.0.0.0/16.
* Maakt u een subnet met de naam Appgatewaysubnet dat gebruikmaakt van 10.0.0.0/28 als CIDR-blok.
* Instellen van twee eerder geconfigureerde back-end-IP-adressen voor webservers Hallo u tooload saldo Hallo verkeer. In dit voorbeeld sjabloon hello back-end-IP-adressen zijn 10.0.1.10 en 10.0.1.11 gebruikt.

> [!NOTE]
> Deze instellingen zijn Hallo parameters voor deze sjabloon. toocustomize hello sjabloon, kunt u regels, Hallo listener, SSL en andere opties in de bestand azuredeploy.json Hallo wijzigen.

![Scenario](./media/application-gateway-create-gateway-arm-template/scenario.png)

## <a name="download-and-understand-hello-azure-resource-manager-template"></a>Hello Azure Resource Manager-sjabloon downloaden en begrijpen

U kunt downloaden Hallo bestaande Azure Resource Manager-sjabloon toocreate een virtueel netwerk en twee subnets vanuit GitHub, breng eventuele wijzigingen die u mogelijk wilt gebruiken en het opnieuw gebruiken. toodo gebruik dus Hallo stappen te volgen:

1. Navigeer te[toepassingsgateway maken met web application firewall ingeschakeld](https://github.com/Azure/azure-quickstart-templates/tree/master/101-application-gateway-waf).
1. Klik op **azuredeploy.json** en vervolgens op **RAW**.
1. Sla Hallo bestand tooa lokale map op uw computer.
1. Als u bekend met Azure Resource Manager-sjablonen bent, slaat u toostep 7.
1. Open Hallo-bestand dat u hebt opgeslagen en bekijkt hello inhoud onder **parameters** in regel
1. Azure Resource Manager-sjabloonparameters bieden een tijdelijke aanduiding voor waarden die kunnen worden ingevuld tijdens de implementatie.

  | Parameter | Beschrijving |
  | --- | --- |
  | **subnetPrefix** |CIDR-blokkering voor het subnet Hallo toepassingsgateway. |
  | **applicationGatewaySize** | De grootte van de toepassingsgateway Hallo.  WAF kunt alleen middelgrote en grote. |
  | **backendIpaddress1** |IP-adres van de eerste webserver Hallo. |
  | **backendIpaddress2** |IP-adres van de tweede webserver Hallo. |
  | **wafEnabled** | Instelling toodetermine als WAF is ingeschakeld.|
  | **wafMode** | Modus van Hallo web application firewall.  Beschikbare opties zijn **preventie** of **detectie**.|
  | **wafRuleSetType** | RuleSet-type voor WAF.  OWASP is momenteel Hallo optie wordt alleen ondersteund. |
  | **wafRuleSetVersion** |RuleSet-versie. OWASP CRS 2.2.9 en 3.0 zijn momenteel ondersteund Hallo-opties. |

1. Controleer de inhoud Hallo onder **resources** en kennisgeving Hallo volgende eigenschappen:

   * **type**. Type resource dat door Hallo sjabloon wordt gemaakt. In dit geval Hallo type is `Microsoft.Network/applicationGateways`, die staat voor een toepassingsgateway.
   * **Naam**. Naam voor Hallo resource. Kennisgeving Hallo gebruik van `[parameters('applicationGatewayName')]`, wat betekent dat deze Hallo-naam is opgegeven als invoer door u of door een parameterbestand tijdens de implementatie.
   * **Eigenschappen**. Lijst met eigenschappen voor Hallo resource. Deze sjabloon maakt gebruik van virtueel netwerk Hallo en openbare IP-adres tijdens het maken van de toepassingsgateway.

   > [!NOTE]
   > Voor meer informatie over sjablonen gaat u naar: [verwijzing naar Resource Manager-sjablonen](/templates/)

1. Navigeer terug te[https://github.com/Azure/azure-quickstart-templates/blob/master/101-application-gateway-waf/](https://github.com/Azure/azure-quickstart-templates/blob/master/101-application-gateway-waf).
1. Klik op **azuredeploy-parameters.json**, en klik vervolgens op **RAW**.
1. Sla Hallo bestand tooa lokale map op uw computer.
1. Open Hallo-bestand dat u hebt opgeslagen en bewerk Hallo waarden voor Hallo-parameters. Gebruik hello waarden toodeploy Hallo toepassingsgateway beschreven in ons scenario te volgen.

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

1. Hallo-bestand opslaan. U kunt Hallo JSON-sjabloon en testen met online JSON-validatiehulpprogramma's zoals [JSlint.com](http://www.jslint.com/).

## <a name="deploy-hello-azure-resource-manager-template-by-using-powershell"></a>Hello Azure Resource Manager-sjabloon implementeren met behulp van PowerShell

Als u Azure PowerShell nog nooit hebt gebruikt, gaat u naar: [hoe tooinstall en configureren van Azure PowerShell](/powershell/azure/overview) en volg Hallo instructies toosign in Azure en uw abonnement te selecteren.

1. Aanmelding tooPowerShell

    ```powershell
    Login-AzureRmAccount
    ```

1. Controleer de abonnementen Hallo voor Hallo-account.

    ```powershell
    Get-AzureRmSubscription
    ```

    Vraag tooauthenticate bent u met uw referenties.

1. Kies welke van uw Azure-abonnementen toouse.

    ```powershell
    Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
    ```

1. Maak indien nodig een resourcegroep via Hallo **New-AzureResourceGroup** cmdlet. In de Hallo voorbeeld te volgen, maakt u een resourcegroep met de naam AppgatewayRG op de locatie VS-Oost.

    ```powershell
    New-AzureRmResourceGroup -Name AppgatewayRG -Location "West US"
    ```

1. Voer Hallo **New-AzureRmResourceGroupDeployment** cmdlet toodeploy Hallo nieuw virtueel netwerk met behulp van Hallo voorafgaand aan de sjabloon en de parameter-bestanden die u hebt gedownload en gewijzigd.
    
    ```powershell
    New-AzureRmResourceGroupDeployment -Name TestAppgatewayDeployment -ResourceGroupName AppgatewayRG `
    -TemplateFile C:\ARM\azuredeploy.json -TemplateParameterFile C:\ARM\azuredeploy-parameters.json
    ```

## <a name="deploy-hello-azure-resource-manager-template-by-using-hello-azure-cli"></a>Hello Azure Resource Manager-sjabloon implementeren met behulp van hello Azure CLI

toodeploy hello Azure Resource Manager-sjabloon die u hebt gedownload met Azure CLI, volg Hallo stappen te volgen:

1. Als u Azure CLI nog nooit hebt gebruikt, raadpleegt u [installeren en configureren van Azure CLI Hallo](/cli/azure/install-azure-cli) en volg de instructies Hallo toohello punt waar u uw Azure-account en abonnement selecteren.

1. Indien nodig, voer hello `az group create` opdracht toocreate een resourcegroep, zoals wordt weergegeven in het volgende codefragment Hallo. U ziet Hallo-uitvoer van Hallo-opdracht. Hallo-lijst die wordt weergegeven na Hallo uitvoer wordt uitgelegd Hallo parameters die worden gebruikt. Zie voor meer informatie over resourcegroepen [Overzicht van Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).

    ```azurecli
    az group create --location westus --name appgatewayRG
    ```
    
    **-n (of --naam)**. Naam voor de nieuwe resourcegroep Hallo. In ons scenario is dit *appgatewayRG*.
    
    **-l (of --locatie)**. Azure-regio waar de nieuwe resourcegroep hello wordt gemaakt. In ons scenario heeft *westus*.

1. Voer Hallo `az group deployment create` cmdlet toodeploy Hallo nieuw virtueel netwerk met behulp van Hallo sjabloon en de parameterbestanden die u hebt gedownload en gewijzigd in de voorgaande stap Hallo. Hallo-lijst die wordt weergegeven na Hallo uitvoer wordt uitgelegd Hallo parameters die worden gebruikt.

    ```azurecli
    az group deployment create --resource-group appgatewayRG --name TestAppgatewayDeployment --template-file azuredeploy.json --parameters @azuredeploy-parameters.json
    ```

## <a name="deploy-hello-azure-resource-manager-template-by-using-click-to-deploy"></a>Hello Azure Resource Manager-sjabloon implementeren met click-to-deploy

Click-to-deploy is een andere manier toouse Azure Resource Manager-sjablonen. Het is een eenvoudige manier toouse sjablonen Hello Azure-portal.

1. Ga te[een toepassingsgateway maken met web application firewall](https://azure.microsoft.com/documentation/templates/101-application-gateway-waf/).

1. Klik op **tooAzure implementeren**.

    ![TooAzure implementeren](./media/application-gateway-create-gateway-arm-template/deploytoazure.png)
    
1. Vul Hallo parameters voor de implementatiesjabloon Hallo op Hallo-portal en klikt u op **OK**.

    ![Parameters](./media/application-gateway-create-gateway-arm-template/ibiza1.png)
    
1. Selecteer **ik ga akkoord toohello voorwaarden bovengenoemde** en klik op **aankoop**.

1. Klik op de blade voor aangepaste implementatie hello, **maken**.

## <a name="providing-certificate-data-tooresource-manager-templates"></a>Certificaat gegevens tooResource bieden Manager-sjablonen

Als u SSL met een sjabloon, moet Hallo certificaat toobe opgegeven in een base64-tekenreeks in plaats van wordt geüpload. tooconvert een .pfx- of .cer tooa base64-tekenreeks gebruik een van de volgende opdrachten Hallo. Hallo converteren volgende opdrachten Hallo certificaat tooa base64-tekenreeks, die toohello sjabloon kan worden opgegeven. Hallo verwacht uitvoer is een tekenreeks die kan worden opgeslagen in een variabele en geplakt in Hallo-sjabloon.

### <a name="macos"></a>macOS
```bash
cert=$( base64 <certificate path and name>.pfx )
echo $cert
```

### <a name="windows"></a>Windows
```powershell
[System.Convert]::ToBase64String([System.IO.File]::ReadAllBytes("<certificate path and name>.pfx"))
```

## <a name="delete-all-resources"></a>Alle resources verwijderen

toodelete alle resources die worden gemaakt in dit artikel wordt voltooid één Hallo stappen te volgen:

### <a name="powershell"></a>PowerShell

```powershell
Remove-AzureRmResourceGroup -Name appgatewayRG
```

### <a name="azure-cli"></a>Azure CLI

```azurecli
az group delete --name appgatewayRG
```

## <a name="next-steps"></a>Volgende stappen

Als u wilt dat tooconfigure SSL-offload, gaat u naar: [een toepassingsgateway voor SSL-offload configureren](application-gateway-ssl.md).

Als u wilt dat tooconfigure een toouse application gateway met een interne load balancer, gaat u naar: [een toepassingsgateway maken met een interne load balancer (ILB)](application-gateway-ilb.md).

Als u meer informatie wilt over de algemene opties voor taakverdeling, gaat u naar:

* [Azure Load Balancer](https://azure.microsoft.com/documentation/services/load-balancer/)
* [Azure Traffic Manager](https://azure.microsoft.com/documentation/services/traffic-manager/)


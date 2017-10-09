---
title: aaaCreate een internetgerichte load balancer - Azure-sjabloon | Microsoft Docs
description: Meer informatie over hoe de toocreate een Internet gerichte load balancer in Resource Manager, met een sjabloon
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-resource-manager
ms.assetid: b24f4729-4559-4458-8527-71009d242647
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 2bce8cb87303838f3bc732d51228ab46d8015552
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="creating-an-internet-facing-load-balancer-using-a-template"></a>Aan de slag met het maken van een internetgerichte load balancer met een sjabloon

> [!div class="op_single_selector"]
> * [Portal](../load-balancer/load-balancer-get-started-internet-portal.md)
> * [PowerShell](../load-balancer/load-balancer-get-started-internet-arm-ps.md)
> * [Azure CLI](../load-balancer/load-balancer-get-started-internet-arm-cli.md)
> * [Sjabloon](../load-balancer/load-balancer-get-started-internet-arm-template.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

In dit artikel bevat informatie over Hallo Resource Manager-implementatiemodel. U kunt ook [meer informatie over hoe een internetverbinding toocreate netwerktaakverdeler met klassieke implementatiemodel](load-balancer-get-started-internet-classic-portal.md)

[!INCLUDE [load-balancer-get-started-internet-scenario-include.md](../../includes/load-balancer-get-started-internet-scenario-include.md)]

## <a name="deploy-hello-template-by-using-click-toodeploy"></a>Hallo-sjabloon implementeren met Klik toodeploy

Hallo voorbeeldsjabloon beschikbaar in de openbare opslagplaats Hallo maakt gebruik van een parameterbestand met Hallo standaard waarden gebruikt toogenerate Hallo scenario die hierboven worden beschreven. toodeploy toodeploy, het gebruik van deze sjabloon Klik Volg [deze koppeling](http://go.microsoft.com/fwlink/?LinkId=544801), klikt u op **tooAzure implementeren**, vervang Hallo standaardparameterwaarden indien nodig en volg de instructies Hallo in Hallo-portal.

## <a name="deploy-hello-template-by-using-powershell"></a>Hallo-sjabloon implementeren met behulp van PowerShell

toodeploy hello sjabloon die u hebt gedownload met behulp van PowerShell, Hallo volgende stappen.

1. Als u Azure PowerShell nog nooit hebt gebruikt, raadpleegt u [hoe tooInstall en configureer Azure PowerShell](/powershell/azure/overview) en volg de instructies Hallo alle Hallo manier toohello toosign beëindigen in Azure en uw abonnement te selecteren.
2. Voer Hallo **New-AzureRmResourceGroupDeployment** cmdlet toocreate een resource-groep met Hallo sjabloon.

    ```powershell
    New-AzureRmResourceGroupDeployment -Name TestRG -Location uswest `
        -TemplateFile 'https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-2-vms-loadbalancer-lbrules/azuredeploy.json' `
        -TemplateParameterFile 'https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-2-vms-loadbalancer-lbrules/azuredeploy.parameters.json'
    ```

## <a name="deploy-hello-template-by-using-hello-azure-cli"></a>Hallo-sjabloon implementeren met hello Azure CLI

toodeploy hello sjabloon via Azure CLI Hallo Hallo volgende stappen.

1. Als u Azure CLI nog nooit hebt gebruikt, raadpleegt u [installeren en configureren van Azure CLI Hallo](../cli-install-nodejs.md) en volg de instructies Hallo toohello punt waar u uw Azure-account en abonnement selecteren.
2. Voer Hallo **azure config mode** opdracht tooswitch tooResource modus Manager, zoals hieronder wordt weergegeven.

    ```azurecli
    azure config mode arm
    ```

    Dit is verwacht Hallo uitvoer voor Hallo bovenstaande opdracht:

        info:    New mode is arm

3. Vanuit de browser te navigeren[Snelstartsjabloon met de Hallo](https://github.com/Azure/azure-quickstart-templates/tree/master/201-2-vms-loadbalancer-lbrules), Hallo inhoud van Hallo json-bestand kopiëren en plakken in een nieuw bestand op uw computer. In dit scenario voor u het Hallo-waarden onder tooa-bestand met de naam zou kopiëren **c:\lb\azuredeploy.parameters.json**.
4. Voer Hallo **implementatie van de azure-groep maken** cmdlet toodeploy Hallo nieuwe load balancer met behulp van Hallo sjabloon en de parameterbestanden die u hebt gedownload en hierboven zijn gewijzigd. Hallo-lijst die wordt weergegeven na Hallo uitvoer wordt uitgelegd Hallo parameters die worden gebruikt.

    ```azurecli
    azure group create --name TestRG --location westus --template-file 'https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-2-vms-loadbalancer-lbrules/azuredeploy.json' --parameters-file 'c:\lb\azuredeploy.parameters.json'
    ```

## <a name="next-steps"></a>Volgende stappen

[Aan de slag met het configureren van een interne load balancer](load-balancer-get-started-ilb-arm-ps.md)

[Een distributiemodus voor de load balancer configureren](load-balancer-distribution-mode.md)

[TCP-time-outinstellingen voor inactiviteit voor de load balancer configureren](load-balancer-tcp-idle-timeout.md)

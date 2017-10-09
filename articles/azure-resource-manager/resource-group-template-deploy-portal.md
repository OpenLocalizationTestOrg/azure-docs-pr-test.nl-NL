---
title: Azure portal toodeploy aaaUse Azure-resources | Microsoft Docs
description: Azure portal en Azure Resource Manager toodeploy uw resources gebruiken.
services: azure-resource-manager,azure-portal
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 2c98a4aa-8d9f-4a0a-b764-214dbe8ed009
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/19/2016
ms.author: tomfitz
ms.openlocfilehash: 5a5217f94c8dfc0c1ebd613903ea3dcbe1197bfc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-resources-with-resource-manager-templates-and-azure-portal"></a>Resources implementeren met Resource Manager-sjablonen en Azure Portal
> [!div class="op_single_selector"]
> * [PowerShell](resource-group-template-deploy.md)
> * [Azure CLI](resource-group-template-deploy-cli.md)
> * [Portal](resource-group-template-deploy-portal.md)
> * [REST API](resource-group-template-deploy-rest.md)
> 
> 

Dit onderwerp wordt beschreven hoe toouse hello [Azure-portal](https://portal.azure.com) met [Azure Resource Manager](resource-group-overview.md) toodeploy uw Azure-resources. Zie toolearn over het beheren van uw resources [beheren Azure-resources via de portal](resource-group-portal.md).

Op dit moment ondersteunt niet elke service Hallo portal of de Resource Manager. Voor deze services, moet u toouse hello [klassieke portal](https://manage.windowsazure.com). Zie voor Hallo status van elke service, [Azure portal beschikbaarheid grafiek](https://azure.microsoft.com/features/azure-portal/availability/).

## <a name="create-resource-group"></a>Een resourcegroep maken
1. Selecteer toocreate een lege resourcegroep **nieuw** > **Management** > **resourcegroep**.
   
    ![lege resourcegroep maken](./media/resource-group-template-deploy-portal/create-empty-group.png)
2. Wijs hieraan een naam en locatie en, indien nodig, selecteert u een abonnement. Moet u tooprovide een locatie voor resourcegroep Hallo omdat resourcegroep Hallo metagegevens over Hallo resources worden opgeslagen. U kunt om wettelijke redenen toospecify waar deze metagegevens worden opgeslagen. In het algemeen is het raadzaam dat u een locatie waar de meeste van uw resources opgeven. Met behulp van dezelfde Hallo locatie kunt u de sjabloon vereenvoudigen.
   
    ![setwaarden](./media/resource-group-template-deploy-portal/set-group-properties.png)

## <a name="deploy-resources-from-marketplace"></a>Resources van Marketplace implementeren
Nadat u een resourcegroep hebt gemaakt, kunt u resources tooit van Hallo Marketplace kunt implementeren. Hallo Marketplace biedt vooraf gedefinieerde oplossingen voor algemene scenario's.

1. toostart een implementatie, selecteer **nieuw** en het Hallo-type van resource gewenst toodeploy. Zoek voor bepaalde versie van Hallo resource Hallo gewenst toodeploy.
   
    ![resource implementeren](./media/resource-group-template-deploy-portal/deploy-resource.png)
2. Als u bepaalde Hallo-oplossing u graag toodeploy niet ziet, kunt u Hallo Marketplace voor het zoeken.
   
    ![zoeken marketplace](./media/resource-group-template-deploy-portal/search-resource.png)
3. Afhankelijk van het type Hallo van geselecteerde bron hebt u een verzameling van de relevante eigenschappen tooset vóór de implementatie. Deze opties wordt hier niet weergegeven als ze afhankelijk van het resourcetype variëren. Voor alle typen, moet u een resourcegroep bestemming. Hallo volgende afbeelding toont hoe toocreate een web-app en implementeert u het toohello-resourcegroep die u hebt gemaakt.
   
    ![resourcegroep maken](./media/resource-group-template-deploy-portal/select-existing-group.png)
   
    U kunt ook kunt u een resourcegroep toocreate bepalen bij het implementeren van uw resources. Selecteer **nieuw** en Hallo resourcegroep een naam geven.
   
    ![nieuwe resourcegroep maken](./media/resource-group-template-deploy-portal/select-new-group.png)
4. Uw implementatie begint. Hallo-implementatie kan enkele minuten duren. Als het Hallo-implementatie is voltooid, ziet u een melding.
   
    ![melding weergeven](./media/resource-group-template-deploy-portal/view-notification.png)
5. Na implementatie van uw resources, kunt u meer resources toohello-resourcegroep toevoegen met behulp van Hallo **toevoegen** opdracht op Hallo resourcegroepblade.
   
    ![resource toevoegen](./media/resource-group-template-deploy-portal/add-resource.png)

## <a name="deploy-resources-from-custom-template"></a>Resources met aangepaste sjabloon implementeren
Als u tooexecute een implementatie wilt, maar u geen gebruik van Hallo sjablonen in Hallo Marketplace, kunt u een aangepaste sjabloon die Hallo-infrastructuur voor uw oplossing definieert. toolearn over het maken van sjablonen, Zie [Azure Resource Manager-sjablonen samenstellen](resource-group-authoring-templates.md).

1. toodeploy een aangepaste sjabloon via Hallo-portal, selecteer **nieuw**, en beginnen met zoeken voor **sjabloonimplementatie** totdat u deze in Hallo opties kunt selecteren.
   
    ![de sjabloonimplementatie zoeken](./media/resource-group-template-deploy-portal/search-template.png)
2. Selecteer **sjabloonimplementatie** van Hallo beschikbare bronnen.
   
    ![sjabloonimplementatie selecteren](./media/resource-group-template-deploy-portal/select-template.png)
3. Open na het starten van de sjabloonimplementatie Hallo Hallo lege sjabloon die beschikbaar is voor het aanpassen.
   
    ![Sjabloon maken](./media/resource-group-template-deploy-portal/show-custom-template.png)
   
    Toevoegen in de editor Hallo Hallo JSON syntaxis die Hallo-bronnen die u wilt dat toodeploy definieert. Selecteer **opslaan** wanneer u klaar bent. Zie voor instructies over het schrijven van Hallo JSON syntaxis [overzicht voor Resource Manager-sjabloon](resource-manager-template-walkthrough.md).
   
    ![sjabloon bewerken](./media/resource-group-template-deploy-portal/edit-template.png)
4. Of u kunt een bestaande sjabloon kiezen uit Hallo [Azure-snelstartsjablonen](https://azure.microsoft.com/documentation/templates/). Deze sjablonen zijn die is bijgedragen door Hallo-community. Deze omvatten algemene scenario's en iemand een sjabloon die is vergelijkbaar toowhat die u probeert toodeploy hebt toegevoegd. U kunt zoeken Hallo sjablonen toofind iets dat overeenkomt met het scenario.
   
    ![Quick Start-sjabloon selecteren](./media/resource-group-template-deploy-portal/select-quickstart-template.png)
   
    U kunt de geselecteerde sjabloon Hallo in Hallo-editor weergeven.
5. Na het Hallo alle andere waarden opgeven, selecteert u **maken** toodeploy Hallo sjabloon. 
   
    ![sjabloon implementeren](./media/resource-group-template-deploy-portal/create-custom-deploy.png)

## <a name="deploy-resources-from-a-template-saved-tooyour-account"></a>Resources van een sjabloon opgeslagen tooyour account implementeren
Hallo-portal kunt u een sjabloon tooyour Azure-account toosave en later opnieuw te implementeren. Voor meer informatie over het werken met deze sjablonen, opgeslagen [aan de slag met persoonlijke sjablonen in Azure-portal Hallo](../marketplace-consumer/mytemplates-getstarted.md).

1. toofind uw opgeslagen sjablonen selecteren **Bladeren** > **sjablonen**.
   
    ![Bladeren in sjablonen](./media/resource-group-template-deploy-portal/browse-templates.png)
2. Selecteer één u wilt dat toowork op Hallo in Hallo lijst met sjablonen tooyour account opgeslagen.
   
    ![opgeslagen sjablonen](./media/resource-group-template-deploy-portal/saved-templates.png)
3. Selecteer **implementeren** tooredeploy dit sjabloon opgeslagen.
   
    ![opgeslagen sjabloon implementeren](./media/resource-group-template-deploy-portal/deploy-saved-template.png)

## <a name="next-steps"></a>Volgende stappen
* controlelogboeken tooview, Zie [bewerkingen met Resource Manager controleren](resource-group-audit.md).
* implementatiefouten tootroubleshoot, Zie [implementatiebewerkingen weergeven](resource-manager-deployment-operations.md).
* een sjabloon van een implementatie of de resourcegroep, tooretrieve Zie [Azure Resource Manager-sjabloon exporteren uit bestaande resources](resource-manager-export-template.md).
* Abonnementen voor instructies over hoe ondernemingen tooeffectively Resource Manager kunt beheren, Zie [Azure enterprise scaffold - prescriptieve abonnement governance](resource-manager-subscription-governance.md).


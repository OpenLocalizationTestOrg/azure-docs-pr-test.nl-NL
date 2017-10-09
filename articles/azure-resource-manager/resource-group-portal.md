---
title: Azure portal toomanage aaaUse Azure-resources | Microsoft Docs
description: Azure portal en Azure Resource Manager toomanage uw resources gebruiken. Toont hoe toowork met dashboards toomonitor resources.
services: azure-resource-manager,azure-portal
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 0725bbf2-5913-4c07-af6e-24e11d957fbc
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/19/2016
ms.author: tomfitz
ms.openlocfilehash: 0c89a197a31c5b6dd03ba457cb4d1fdf9f6d00f6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-resources-through-portal"></a>Azure-resources via de portal beheren
> [!div class="op_single_selector"]
> * [Azure PowerShell](powershell-azure-resource-manager.md)
> * [Azure-CLI](xplat-cli-azure-resource-manager.md)
> * [Portal](resource-group-portal.md) 
> * [REST API](resource-manager-rest-api.md)
> 
> 

Dit onderwerp wordt beschreven hoe toouse hello [Azure-portal](https://portal.azure.com) met [Azure Resource Manager](resource-group-overview.md) toomanage uw Azure-resources. toolearn over het implementeren van resources via de portal hello, Zie [implementeren van resources met Resource Manager-sjablonen en Azure-portal](resource-group-template-deploy-portal.md).

Op dit moment ondersteunt niet elke service Hallo portal of de Resource Manager. Voor deze services, moet u toouse hello [klassieke portal](https://manage.windowsazure.com). Zie voor Hallo status van elke service, [Azure portal beschikbaarheid grafiek](https://azure.microsoft.com/features/azure-portal/availability/).

## <a name="manage-resource-groups"></a>Resourcegroepen beheren

Een resourcegroep is een container met verwante resources voor een Azure-oplossing. Hallo resourcegroep kan alle Hallo resources voor Hallo oplossing of alleen de gewenste toomanage als een groep resources bevatten. U bepalen hoe u resources tooallocate tooresource groepen op basis van het wat zinvol Hallo meeste voor uw organisatie. In het algemeen toevoegen resources die Hallo delen dezelfde levenscyclus toohello dezelfde resource groeperen, zodat u kunt eenvoudig implementeren, bijwerken en deze als een groep te verwijderen. 

Hallo resourcegroep slaat metagegevens over Hallo resources. Daarom wanneer u een locatie voor resourcegroep Hallo opgeeft, geeft u aan waar de metagegevens worden opgeslagen. Om wettelijke redenen, moet u mogelijk tooensure die uw gegevens worden opgeslagen in een bepaald gebied.

1. alle Hallo resourcegroepen in uw abonnement, selecteert u toosee **resourcegroepen**.
   
    ![resourcegroepen bladeren](./media/resource-group-portal/browse-groups.png)
2. Selecteer toocreate een lege resourcegroep **toevoegen**.
   
    ![toevoegen van resourcegroep](./media/resource-group-portal/add-resource-group.png)
3. Geef een naam en locatie voor de nieuwe resourcegroep Hallo. Selecteer **Maken**.
   
    ![resourcegroep maken](./media/resource-group-portal/create-empty-group.png)
4. Mogelijk moet u tooselect **vernieuwen** toosee Hallo onlangs gemaakt resourcegroep.
   
    ![vernieuwen van resourcegroep](./media/resource-group-portal/refresh-resource-groups.png)
5. toocustomize hello informatie weergegeven voor de bronnengroepen selecteren **kolommen**.
   
    ![kolommen aanpassen](./media/resource-group-portal/select-columns.png)
6. Hallo kolommen tooadd selecteren en selecteer vervolgens **Update**.
   
    ![kolommen toevoegen](./media/resource-group-portal/add-columns.png)
7. Zie toolearn over het implementeren van resources tooyour nieuwe resourcegroep [implementeren van resources met Resource Manager-sjablonen en Azure-portal](resource-group-template-deploy-portal.md).
8. U kunt voor snelle toegang tooa resourcegroep, Hallo blade tooyour dashboard vastmaken.
   
    ![pincode resourcegroep](./media/resource-group-portal/pin-group.png)
9. Hallo dashboard toont de Hallo resourcegroep en de bijbehorende bronnen. U kunt resourcegroepen hello of een van de resources toonavigate toohello item selecteren.
   
    ![pincode resourcegroep](./media/resource-group-portal/show-resource-group-dashboard.png)

## <a name="tag-resources"></a>Tag resources
U kunt tags tooresource groepen toepassen en resources toologically uw assets ordenen. Zie voor meer informatie over het werken met labels [Using tags tooorganize uw Azure-resources](resource-group-using-tags.md).

[!INCLUDE [resource-manager-tag-resource](../../includes/resource-manager-tag-resources.md)]

## <a name="monitor-resources"></a>Resources controleren
Wanneer u een resource selecteert, geeft de resourceblade Hallo standaard grafieken en tabellen voor bewaking van dat resourcetype.

1. Selecteer een resource en kennisgeving Hallo **bewaking** sectie. Dit omvat grafieken die relevant toohello resourcetype zijn. Hallo toont volgende afbeelding Hallo standaardinstellingen voor bewaking van gegevens voor een opslagaccount.
   
    ![bewaking weergeven](./media/resource-group-portal/show-monitoring.png)
2. U kunt een gedeelte van Hallo blade tooyour dashboard vastmaken Hallo weglatingsteken (...) boven Hallo sectie selecteert. U kunt ook Hallo grootte Hallo sectie Hallo blade aanpassen of verwijder deze volledig. Hallo volgende afbeelding ziet u hoe toopin, aanpassen of verwijderen van Hallo CPU en geheugen-sectie.
   
    ![sectie van de pincode](./media/resource-group-portal/pin-cpu-section.png)
3. Na het Hallo sectie toohello dashboard vastmaken, ziet u Hallo samenvatting op Hallo-dashboard. En onmiddellijk selecteren gaat u gegevens over Hallo toomore.
   
    ![weergave-dashboard](./media/resource-group-portal/view-startboard.png)
4. toocompletely aanpassen Hallo gegevens controleren via de portal hello, navigeer tooyour standaarddashboard en selecteer **nieuwe dashboard**.
   
    ![dashboard](./media/resource-group-portal/dashboard.png)
5. Geef een naam op voor uw nieuwe dashboard en sleep tegels op Hallo-dashboard. Hallo tegels worden gefilterd door verschillende opties.
   
    ![dashboard](./media/resource-group-portal/create-dashboard.png)
   
     toolearn over het werken met dashboards, Zie [maken en delen van dashboards in hello Azure-portal](../azure-portal/azure-portal-dashboards.md).

## <a name="manage-resources"></a>Resources beheren
In Hallo blade voor een resource ziet u opties voor het beheren van Hallo resource Hallo. Hallo portal geeft beheeropties voor die bepaald resourcetype. Opdrachten voor het beheer van Hallo ziet u aan de bovenkant Hallo van Hallo resourceblade en aan de linkerkant Hallo.

![Resources beheren](./media/resource-group-portal/manage-resources.png)

U kunt bewerkingen zoals het starten en stoppen van een virtuele machine of Hallo eigenschappen van Hallo virtuele machine opnieuw uitvoeren van deze opties.

## <a name="move-resources"></a>Resources verplaatsen
Als u toomove resources tooanother resourcegroep of een ander abonnement nodig hebt, raadpleegt u [verplaatsen van resources toonew resourcegroep of abonnement](resource-group-move-resources.md).

## <a name="lock-resources"></a>Resources vergrendelen
U kunt vergrendelen een abonnement, resourcegroep of resource tooprevent andere gebruikers in uw organisatie per ongeluk worden kritieke bronnen wijzigen of verwijderen. Zie voor meer informatie [Resources vergrendelen met Azure Resource Manager](resource-group-lock-resources.md).

[!INCLUDE [resource-manager-lock-resources](../../includes/resource-manager-lock-resources.md)]

## <a name="view-your-subscription-and-costs"></a>Uw abonnement en kosten weergeven
U kunt informatie over uw abonnement en Hallo samengevouwen kosten weergeven voor al uw resources. Selecteer **abonnementen** en gewenste toosee Hallo-abonnement. U wellicht slechts één abonnement tooselect.

![abonnement](./media/resource-group-portal/select-subscription.png)

Binnen abonnementsblade hello ziet u een frequentie branden.

![frequentie branden](./media/resource-group-portal/burn-rate.png)

En een uitsplitsing van de kosten per resourcetype.

![de kosten van resource](./media/resource-group-portal/cost-by-resource.png)

## <a name="export-template"></a>Sjabloon exporteren
Na het instellen van de resourcegroep, kunt u tooview Hallo Resource Manager-sjabloon voor de resourcegroep Hallo. Uitvoer Hallo sjabloon biedt twee voordelen:

1. Omdat het Hallo-sjabloon bevat alle Hallo volledige infrastructuur, kunt u eenvoudig toekomstige implementaties van Hallo oplossing automatiseren.
2. U kunt meer vertrouwd raken met de sjabloonsyntaxis van de door te kijken Hallo notatie JSON (JavaScript Object) dat uw oplossing vertegenwoordigt.

Zie voor stapsgewijze instructies [Azure Resource Manager-sjabloon exporteren uit bestaande resources](resource-manager-export-template.md).

## <a name="delete-resource-group-or-resources"></a>Resourcegroep of resources verwijderen
Verwijderen van een resourcegroep, worden alle Hallo resources daarin verwijderd. U kunt ook afzonderlijke resources binnen een resourcegroep verwijderen. Gewenste tooexercise voorzichtig wanneer u een resourcegroep verwijderen omdat er mogelijk resources in andere resourcegroepen die gekoppelde tooit zijn. Resource Manager wordt niet gekoppelde resources verwijderd, maar ze werken mogelijk niet goed zonder Hallo verwacht bronnen.

![Groep verwijderen](./media/resource-group-portal/delete-group.png)

## <a name="next-steps"></a>Volgende stappen
* tooview activiteitenlogboeken, Zie [bewerkingen met Resource Manager controleren](resource-group-audit.md).
* Zie details over een implementatie tooview [implementatiebewerkingen weergeven](resource-manager-deployment-operations.md).
* toodeploy resources via de portal hello, Zie [implementeren van resources met Resource Manager-sjablonen en Azure-portal](resource-group-template-deploy-portal.md).
* toomanage toegang tooresources, Zie [rol toewijzingen toomanage toegang tooyour Azure-abonnementresources gebruiken](../active-directory/role-based-access-control-configure.md).
* Abonnementen voor instructies over hoe ondernemingen tooeffectively Resource Manager kunt beheren, Zie [Azure enterprise scaffold - prescriptieve abonnement governance](resource-manager-subscription-governance.md).


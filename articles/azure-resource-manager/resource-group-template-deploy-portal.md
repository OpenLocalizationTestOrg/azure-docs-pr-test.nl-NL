---
title: Azure portal gebruiken voor het implementeren van Azure-resources | Microsoft Docs
description: Azure portal en Azure Resource Manager gebruiken voor het implementeren van uw resources.
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
ms.openlocfilehash: a4cac5834c667976b0a2d1f2748e4309a166d16a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="deploy-resources-with-resource-manager-templates-and-azure-portal"></a>Resources implementeren met Resource Manager-sjablonen en Azure Portal
> [!div class="op_single_selector"]
> * [PowerShell](resource-group-template-deploy.md)
> * [Azure CLI](resource-group-template-deploy-cli.md)
> * [Portal](resource-group-template-deploy-portal.md)
> * [REST API](resource-group-template-deploy-rest.md)
> 
> 

Dit onderwerp wordt beschreven hoe u de [Azure-portal](https://portal.azure.com) met [Azure Resource Manager](resource-group-overview.md) voor het implementeren van uw Azure-resources. Zie voor meer informatie over het beheren van uw resources, [beheren Azure-resources via de portal](resource-group-portal.md).

Op dit moment ondersteunt niet elke service de portal of de resourcemanager. Voor deze services die u wilt gebruiken, de [klassieke portal](https://manage.windowsazure.com). Zie voor de status van elke service, [Azure portal beschikbaarheid grafiek](https://azure.microsoft.com/features/azure-portal/availability/).

## <a name="create-resource-group"></a>Een resourcegroep maken
1. U maakt een lege resourcegroep selecteren **nieuw** > **Management** > **resourcegroep**.
   
    ![lege resourcegroep maken](./media/resource-group-template-deploy-portal/create-empty-group.png)
2. Wijs hieraan een naam en locatie en, indien nodig, selecteert u een abonnement. U moet een locatie opgeven voor de resourcegroep omdat de resourcegroep metagegevens over de bronnen worden opgeslagen. Om wettelijke redenen kan u wilt opgeven waar de metagegevens worden opgeslagen. In het algemeen is het raadzaam dat u een locatie waar de meeste van uw resources opgeven. Met behulp van dezelfde locatie, kan de sjabloon vereenvoudigen.
   
    ![setwaarden](./media/resource-group-template-deploy-portal/set-group-properties.png)

## <a name="deploy-resources-from-marketplace"></a>Resources van Marketplace implementeren
Nadat u een resourcegroep hebt gemaakt, kunt u kunt resources van de Marketplace implementeren. De Marketplace biedt vooraf gedefinieerde oplossingen voor algemene scenario's.

1. Selecteer voor het starten van een implementatie **nieuw** en het type resource dat u wilt implementeren. Vervolgens zoekt u naar de specifieke versie van de resource die u wilt implementeren.
   
    ![resource implementeren](./media/resource-group-template-deploy-portal/deploy-resource.png)
2. Als u de specifieke oplossing die u wilt implementeren niet ziet, kunt u de Marketplace voor het zoeken.
   
    ![zoeken marketplace](./media/resource-group-template-deploy-portal/search-resource.png)
3. Afhankelijk van het type geselecteerde bron hebt u een verzameling van de relevante eigenschappen in te stellen vóór de implementatie. Deze opties wordt hier niet weergegeven als ze afhankelijk van het resourcetype variëren. Voor alle typen, moet u een resourcegroep bestemming. De volgende afbeelding laat zien hoe een web-app maken en deze implementeren in de resourcegroep die u hebt gemaakt.
   
    ![resourcegroep maken](./media/resource-group-template-deploy-portal/select-existing-group.png)
   
    U kunt ook een resourcegroep maken bij het implementeren van uw resources. Selecteer **nieuw** en geef de resourcegroep een naam.
   
    ![nieuwe resourcegroep maken](./media/resource-group-template-deploy-portal/select-new-group.png)
4. Uw implementatie begint. De implementatie kan enkele minuten duren. Als de implementatie is voltooid, ziet u een melding.
   
    ![melding weergeven](./media/resource-group-template-deploy-portal/view-notification.png)
5. Na implementatie van uw resources, kunt u meer resources toevoegen aan de resourcegroep met behulp van de **toevoegen** opdracht op de blade met resourcegroepen.
   
    ![resource toevoegen](./media/resource-group-template-deploy-portal/add-resource.png)

## <a name="deploy-resources-from-custom-template"></a>Resources met aangepaste sjabloon implementeren
Als u wilt uitvoeren van een implementatie, maar geen gebruik van de sjablonen in de Marketplace, kunt u een aangepaste sjabloon die de infrastructuur voor uw oplossing definieert. Zie voor meer informatie over het maken van sjablonen, [Azure Resource Manager-sjablonen samenstellen](resource-group-authoring-templates.md).

1. Voor het implementeren van een aangepaste sjabloon via de portal, selecteer **nieuw**, en beginnen met zoeken voor **sjabloonimplementatie** totdat u deze in de opties kunt selecteren.
   
    ![de sjabloonimplementatie zoeken](./media/resource-group-template-deploy-portal/search-template.png)
2. Selecteer **sjabloonimplementatie** uit de beschikbare bronnen.
   
    ![sjabloonimplementatie selecteren](./media/resource-group-template-deploy-portal/select-template.png)
3. Open de lege sjabloon die beschikbaar is voor het aanpassen van na het starten van de sjabloonimplementatie.
   
    ![Sjabloon maken](./media/resource-group-template-deploy-portal/show-custom-template.png)
   
    Voeg de syntaxis van de JSON die definieert de resources die u wilt implementeren in de editor. Selecteer **opslaan** wanneer u klaar bent. Zie voor instructies over het schrijven van de JSON-syntaxis [overzicht voor Resource Manager-sjabloon](resource-manager-template-walkthrough.md).
   
    ![sjabloon bewerken](./media/resource-group-template-deploy-portal/edit-template.png)
4. Of, kunt u een bestaande sjabloon van de [Azure-snelstartsjablonen](https://azure.microsoft.com/documentation/templates/). Deze sjablonen worden aangeleverd door de community. Deze omvatten algemene scenario's en iemand een sjabloon die is vergelijkbaar met wat u probeert te implementeren hebt toegevoegd. U kunt de sjablonen om te vinden die overeenkomt met het scenario zoeken.
   
    ![Quick Start-sjabloon selecteren](./media/resource-group-template-deploy-portal/select-quickstart-template.png)
   
    U kunt de geselecteerde sjabloon weergeven in de editor.
5. Na het opgeven van de waarden, selecteer **maken** om de sjabloon te implementeren. 
   
    ![sjabloon implementeren](./media/resource-group-template-deploy-portal/create-custom-deploy.png)

## <a name="deploy-resources-from-a-template-saved-to-your-account"></a>Resources van een sjabloon die is opgeslagen in uw account implementeren
De portal kunt u een sjabloon opslaan in uw Azure-account en het later opnieuw te implementeren. Voor meer informatie over het werken met deze sjablonen, opgeslagen [aan de slag met persoonlijke sjablonen in de Azure portal](../marketplace-consumer/mytemplates-getstarted.md).

1. Selecteer uw opgeslagen sjablonen vindt **Bladeren** > **sjablonen**.
   
    ![Bladeren in sjablonen](./media/resource-group-template-deploy-portal/browse-templates.png)
2. Selecteer in de lijst met sjablonen die zijn opgeslagen in uw account, degene die u werken wilt op.
   
    ![opgeslagen sjablonen](./media/resource-group-template-deploy-portal/saved-templates.png)
3. Selecteer **implementeren** deze opgeslagen sjabloon opnieuw implementeren.
   
    ![opgeslagen sjabloon implementeren](./media/resource-group-template-deploy-portal/deploy-saved-template.png)

## <a name="next-steps"></a>Volgende stappen
* Controlelogboeken Zie [bewerkingen met Resource Manager controleren](resource-group-audit.md).
* Zie voor het oplossen van implementatiefouten [implementatiebewerkingen weergeven](resource-manager-deployment-operations.md).
* Zie voor het ophalen van een sjabloon van een implementatie of de resourcegroep, [Azure Resource Manager-sjabloon exporteren uit bestaande resources](resource-manager-export-template.md).
* Voor begeleiding bij de manier waarop ondernemingen Resource Manager effectief kunnen gebruiken voor het beheer van abonnementen, gaat u naar [Azure enterprise-platform - Prescriptieve abonnementsgovernance](resource-manager-subscription-governance.md).


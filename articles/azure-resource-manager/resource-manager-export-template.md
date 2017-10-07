---
title: aaaExport Azure Resource Manager-sjabloon | Microsoft Docs
description: Azure Resource Manager tooexport een sjabloon van een bestaande resourcegroep gebruiken.
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 5f5ca940-eef8-4125-b6a0-f44ba04ab5ab
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/06/2017
ms.author: tomfitz
ms.openlocfilehash: 94daa4812da2fec705044ca31c8e74e6d59bd53f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="export-an-azure-resource-manager-template-from-existing-resources"></a>Een Azure Resource Manager-sjabloon uit bestaande resources exporteren
In dit artikel leert u hoe tooexport Resource Manager-sjabloon uit bestaande resources in uw abonnement. U kunt deze gegenereerde sjabloon toogain een beter begrip van de sjabloonsyntaxis van de gebruiken.

Er zijn twee manieren tooexport een sjabloon:

* U kunt exporteren Hallo **werkelijke sjabloon die wordt gebruikt voor de implementatie van**. Hallo geëxporteerde sjabloon bevat alle Hallo parameters en variabelen exact zo worden weergegeven in de oorspronkelijke sjabloon Hallo. Deze methode is handig als u resources via de portal Hallo geïmplementeerd en wilt toosee Hallo sjabloon toocreate die bronnen. Deze sjabloon kan ongewijzigd worden gebruikt. 
* U kunt exporteren een **sjabloon met de huidige status van de resourcegroep Hallo Hallo gegenereerd**. Hallo geëxporteerde sjabloon is niet op basis van een sjabloon die u voor implementatie gebruikt. In plaats daarvan wordt een sjabloon die een momentopname van de resourcegroep Hallo is gemaakt. geëxporteerde sjabloon Hallo heeft veel vastgelegde waarden en waarschijnlijk niet zoveel parameters zoals u normaal gesproken zou definiëren. Deze methode is handig wanneer u Hallo resourcegroep hebt gewijzigd na de implementatie. Deze sjabloon moet meestal worden aangepast voordat deze kan worden gebruikt.

Dit onderwerp bevat beide benaderingen via Hallo-portal.

## <a name="deploy-resources"></a>Resources implementeren
Laten we beginnen door het implementeren van resources tooAzure die u gebruiken kunt voor het exporteren als een sjabloon. Als u al een resourcegroep in uw abonnement dat u wilt dat tooexport tooa sjabloon hebt, kunt u deze sectie overslaan. Hallo rest van dit artikel wordt ervan uitgegaan dat u hebt geïmplementeerd Hallo WebApp en SQL database-oplossing in deze sectie wordt weergegeven. Als u een andere oplossing gebruikt, wordt uw ervaring mogelijk enigszins verschillen, maar Hallo stappen zijn van een sjabloon tooexport Hallo dezelfde. 

1. In Hallo [Azure-portal](https://portal.azure.com), selecteer **nieuw**.
   
      ![Nieuw selecteren](./media/resource-manager-export-template/new.png)
2. Zoeken naar **webtoepassing + SQL** en selecteer het uit de beschikbare opties Hallo.
   
      ![zoeken naar web-app + SQL](./media/resource-manager-export-template/webapp-sql.png)

3. Selecteer **Maken**.

      ![Maken selecteren](./media/resource-manager-export-template/create.png)

4. Hallo vereist waarden opgeven voor het Hallo-webtoepassing en SQL-database. Selecteer **Maken**.

      ![waarden voor web-app en SQL-database opgeven](./media/resource-manager-export-template/provide-web-values.png)

Hallo-implementatie kan een paar minuten duren. Nadat het Hallo-implementatie is voltooid, bevat uw abonnement Hallo-oplossing.

## <a name="view-template-from-deployment-history"></a>Sjabloon weergeven vanuit implementatiegeschiedenis
1. Ga toohello resourcegroepblade voor uw nieuwe resourcegroep. Let op dat die blade Hallo Hallo resultaten van de laatste implementatie Hallo weergegeven. Selecteer deze koppeling.
   
      ![resourcegroepblade](./media/resource-manager-export-template/select-deployment.png)
2. U ziet een geschiedenis van de implementaties voor Hallo-groep. In uw geval bevat Hallo blade waarschijnlijk slechts een implementatie. Selecteer deze implementatie.
   
     ![laatste implementatie](./media/resource-manager-export-template/select-history.png)
3. Hallo-blade geeft een samenvatting van Hallo-implementatie. Hallo samenvatting bevat Hallo status van Hallo-implementatie en bewerkingen en Hallo-waarden die u hebt opgegeven voor de parameters. toosee hello sjabloon die u voor implementatie hello, selecteer gebruikt **sjabloon weergeven**.
   
     ![implementatiesamenvatting bekijken](./media/resource-manager-export-template/view-template.png)
4. Resource Manager haalt Hallo zeven bestanden voor u te volgen:
   
   1. **Sjabloon** -Hallo-sjabloon die Hallo-infrastructuur voor uw oplossing definieert. Tijdens het maken van Hallo storage-account via de portal Hallo Resource Manager een sjabloon toodeploy gebruikt deze en de sjabloon is opgeslagen voor toekomstig gebruik.
   2. **Parameters** -een parameterbestand dat u toopass waarden tijdens de implementatie kunt. Hallo waarden bevat die u hebt opgegeven tijdens de eerste implementatie Hallo. U kunt deze waarden wijzigen wanneer u Hallo sjabloon opnieuw implementeert.
   3. **CLI** -Azure vanaf de opdrachtregel-line-interface (CLI) scriptbestand dat u toodeploy Hallo sjabloon kunt gebruiken.
   3. **CLI 2.0** -Azure vanaf de opdrachtregel-line-interface (CLI) scriptbestand dat u toodeploy Hallo sjabloon kunt gebruiken.
   4. **PowerShell** -een Azure PowerShell-scriptbestand dat u toodeploy Hallo sjabloon kunt gebruiken.
   5. **.NET** -A .NET-klasse die u toodeploy Hallo sjabloon kunt gebruiken.
   6. **Ruby** -A Ruby-klasse die u toodeploy Hallo sjabloon kunt gebruiken.
      
      Hallo-bestanden zijn beschikbaar via de koppelingen tussen Hallo-blade. Standaard worden Hallo blade Hallo sjabloon weergegeven.
      
       ![sjabloon weergeven](./media/resource-manager-export-template/see-template.png)
      
Deze sjabloon is de werkelijke sjabloon Hallo toocreate gebruikt uw web-app en de SQL-database. U ziet dat deze parameters waarmee u verschillende waarden voor de tooprovide tijdens de implementatie bevat. Zie toolearn meer informatie over het Hallo-structuur van een sjabloon [Azure Resource Manager-sjablonen samenstellen](resource-group-authoring-templates.md).

## <a name="export-hello-template-from-resource-group"></a>Hallo-sjabloon uit de resourcegroep exporteren
Als u handmatig gewijzigd van uw resources of resources toegevoegd in meerdere implementaties, komt bij het ophalen van een sjabloon van Hallo implementatiegeschiedenis niet overeen met huidige status van de resourcegroep Hallo Hallo. Deze sectie leest u hoe tooexport een sjabloon die overeenkomt met de huidige status van de resourcegroep Hallo Hallo. 

> [!NOTE]
> U kunt geen sjablonen voor een resourcegroep met meer dan 200 bronnen exporteren.
> 
> 

1. tooview hello sjabloon voor een resourcegroep, selecteer **automatiseringsscript**.
   
      ![resourcegroep exporteren](./media/resource-manager-export-template/select-automation.png)
   
     Resource Manager Hallo resources in de resourcegroep Hallo geëvalueerd en genereert een sjabloon voor deze resources. Niet alle brontypen Hallo export sjabloonfunctie. Mogelijk ziet u een foutmelding weergegeven dat er een probleem met Hallo exporteren is. U leert hoe toohandle die problemen bij Hallo [problemen met het exporteren van Fix](#fix-export-issues) sectie.
2. Er wordt opnieuw zes Hallo-bestanden die u tooredeploy Hallo oplossing kunt gebruiken. Deze tijd Hallo-sjabloon is echter enigszins anders. U ziet dat deze gegenereerde sjabloon Hallo bevat minder parameters dan Hallo-sjabloon in de vorige sectie. Veel van de waarden hello (zoals de locatie en de SKU-waarden) zijn ook hardgecodeerd in deze sjabloon in plaats van een parameterwaarde accepteren. Vóór het hergebruik van deze sjabloon kunt u tooedit Hallo sjabloon toomake beter gebruik van parameters. 
   
3. U hebt een aantal opties voor u doorgaat toowork met deze sjabloon. Hallo-sjabloon downloaden en deze lokaal werkt met een JSON-editor. Of u kunt de sjabloonbibliotheek tooyour Hallo opslaan en werken via Hallo-portal.
   
     Als u vertrouwd met een JSON-editor zoals bent [tegenover Code](https://code.visualstudio.com/) of [Visual Studio](vs-azure-tools-resource-groups-deployment-projects-create-deploy.md), werkt u liever lokaal Hallo-sjabloon downloaden en gebruiken van deze editor. toowork lokaal, selecteer **downloaden**.
   
      ![sjabloon downloaden](./media/resource-manager-export-template/download-template.png)
   
     Als u niet zijn ingesteld met een JSON-editor, kunt u liever bewerken Hallo sjabloon via Hallo-portal. Hallo rest van dit onderwerp wordt ervan uitgegaan dat u hebt de sjabloonbibliotheek tooyour Hallo opgeslagen in Hallo-portal. U er echter Hallo dezelfde syntaxis toohello sjabloon wijzigt of lokaal werkt met een JSON-editor of via het Hallo-portal. toowork via Hallo-portal, selecteer **toolibrary toevoegen**.
   
      ![toolibrary toevoegen](./media/resource-manager-export-template/add-to-library.png)
   
     Wanneer u een sjabloon toohello bibliotheek toevoegt, geeft u Hallo sjabloon een naam en beschrijving. Selecteer vervolgens **Opslaan**.
   
     ![sjabloonwaarden instellen](./media/resource-manager-export-template/save-library-template.png)
4. Selecteer een sjabloon in de bibliotheek opgeslagen tooview **meer services**, type **sjablonen** toofilter resultaten, selecteer **sjablonen**.
   
      ![sjablonen zoeken](./media/resource-manager-export-template/find-templates.png)
5. Selecteer de sjabloon Hallo met Hallo-naam die u hebt opgeslagen.
   
      ![sjabloon selecteren](./media/resource-manager-export-template/select-saved-template.png)

## <a name="customize-hello-template"></a>Hallo-sjabloon aanpassen
Hallo geëxporteerde sjabloon werkt goed dat als u wilt dat toocreate Hallo dezelfde web-app en SQL-database voor elke implementatie. Resource Manager biedt echter opties die u in staat stellen sjablonen met veel meer flexibiliteit te implementeren. Dit artikel laat zien hoe tooadd parameters op voor het Hallo-database de beheerdersnaam van de en het wachtwoord. U kunt deze dezelfde benadering tooadd meer flexibiliteit voor andere waarden in de sjabloon Hallo.

1. toocustomize hello sjabloon, selecteer **bewerken**.
   
     ![sjabloon weergeven](./media/resource-manager-export-template/select-edit.png)
2. Hallo-sjabloon selecteren.
   
     ![sjabloon bewerken](./media/resource-manager-export-template/select-added-template.png)
3. toobe kunnen toopass Hallo waarden die u toospecify tijdens de implementatie wellicht toevoegen Hallo na twee parameters toohello **parameters** sectie in Hallo sjabloon:

   ```json
   "administratorLogin": {
       "type": "String"
   },
   "administratorLoginPassword": {
       "type": "SecureString"
   },
   ```

4. toouse hello nieuwe parameters, Hallo SQL server-definitie in Hallo vervangen **resources** sectie. U ziet dat **administratorLogin** en **administratorLoginPassword** nu parameterwaarden gebruiken.

   ```json
   {
       "comments": "Generalized from resource: '/subscriptions/{subscription-id}/resourceGroups/exportsite/providers/Microsoft.Sql/servers/tfserverexport'.",
       "type": "Microsoft.Sql/servers",
       "kind": "v12.0",
       "name": "[parameters('servers_tfserverexport_name')]",
       "apiVersion": "2014-04-01-preview",
       "location": "South Central US",
       "scale": null,
       "properties": {
           "administratorLogin": "[parameters('administratorLogin')]",
           "administratorLoginPassword": "[parameters('administratorLoginPassword')]",
           "version": "12.0"
       },
       "dependsOn": []
   },
   ```

6. Selecteer **OK** als u klaar bewerken Hallo-sjabloon.
7. Selecteer **opslaan** toosave Hallo wijzigingen toohello sjabloon.
   
     ![sjabloon opslaan](./media/resource-manager-export-template/save-template.png)
8. tooredeploy hello bijgewerkt sjabloon, selecteer **implementeren**.
   
     ![sjabloon implementeren](./media/resource-manager-export-template/redeploy-template.png)
9. Parameterwaarden opgeven en selecteer een resource groep toodeploy Hallo bronnen.


## <a name="fix-export-issues"></a>Problemen met exports oplossen
Niet alle brontypen Hallo export sjabloonfunctie. Dit probleem handmatig tooresolve Hallo ontbrekende resources toevoegen terug in de sjabloon. Fout bij het Hallo-bericht bevat Hallo brontypen die niet kunnen worden geëxporteerd. Zoek dat resourcetype in de Engelstalige [naslaghandleiding over sjablonen](/azure/templates/). Bijvoorbeeld, toomanually toevoegen van een virtuele netwerkgateway, Zie [Microsoft.Network/virtualNetworkGateways sjabloonverwijzing](/azure/templates/microsoft.network/virtualnetworkgateways).

> [!NOTE]
> Exporteren geeft alleen problemen bij het exporteren vanuit een resourcegroep, niet bij het exporteren vanuit de geschiedenis van uw implementatie. Als uw laatste implementatie nauwkeurig Hallo huidige status van de resourcegroep hello vertegenwoordigt, moet u Hallo sjabloon exporteren uit Hallo implementatiegeschiedenis in plaats van vanaf Hallo resourcegroep. Alleen exporteren uit een resourcegroep wanneer u wijzigingen toohello resourcegroep die niet zijn gedefinieerd in één sjabloon hebt gemaakt.
> 
> 

## <a name="next-steps"></a>Volgende stappen
U hebt geleerd hoe een sjabloon uit resources die u hebt gemaakt in de portal Hallo tooexport.

* U kunt een sjabloon implementeren via [PowerShell](resource-group-template-deploy.md), [Azure CLI](resource-group-template-deploy-cli.md) of [REST API](resource-group-template-deploy-rest.md).
* hoe een sjabloon via PowerShell, tooexport zien toosee [Azure PowerShell gebruiken met Azure Resource Manager](powershell-azure-resource-manager.md).
* hoe een sjabloon via Azure CLI tooexport zien toosee [gebruik hello Azure CLI voor Mac, Linux en Windows Azure Resource Manager](xplat-cli-azure-resource-manager.md).


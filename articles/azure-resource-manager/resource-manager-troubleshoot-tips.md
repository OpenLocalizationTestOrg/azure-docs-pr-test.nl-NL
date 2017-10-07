---
title: de Azure implementatiefouten aaaUnderstand | Microsoft Docs
description: Hierin wordt beschreven hoe toolearn over Azure-implementatiefouten.
services: azure-resource-manager
documentationcenter: 
tags: top-support-issue
author: tfitzmac
manager: timlt
editor: tysonn
keywords: Fout in de implementatie, azure-implementatie implementeren tooazure
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: support-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/12/2017
ms.author: tomfitz
ms.openlocfilehash: a335e121e9b908a763374907e34b1f6e823d6e96
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="understand-azure-deployment-errors"></a>Fouten van de Azure-implementatie begrijpen
Dit onderwerp beschrijft implementatiefouten en hoe u meer informatie over een fout kunt detecteren. Zie voor oplossingen toocommon implementatiefouten, [oplossen van veelvoorkomende fouten voor Azure-implementatie met Azure Resource Manager](resource-manager-common-deployment-errors.md).

## <a name="two-types-of-errors"></a>Twee soorten fouten
Er zijn twee typen fouten die u kunt ontvangen:

* Validatiefouten
* Implementatiefouten

Hallo volgende afbeelding toont Hallo activiteitenlogboek voor een abonnement. Hiermee geeft u twee implementaties. In een implementatie Hallo sjabloon validatie is mislukt (**valideren**) en niet worden voortgezet. Hallo in andere implementatie, Hallo sjabloon gevalideerd, maar is mislukt bij het maken van Hallo resources (**schrijven implementaties**). 

![foutcode weergeven](./media/resource-manager-troubleshoot-tips/show-activity-log.png)

Validatiefouten worden veroorzaakt door scenario's die vóór de implementatie kunnen worden bepaald. Ze bevatten syntaxisfouten in de sjabloon of tijdens toodeploy resources die uw abonnement quota's zou overschrijden. Implementatiefouten worden veroorzaakt door de voorwaarden die tijdens het implementatieproces Hallo optreden. Ze bevatten tooaccess probeert een resource die parallel wordt geïmplementeerd.

Beide soorten fouten retourneren een foutcode tootroubleshoot Hallo implementatie te gebruiken. Beide soorten fouten worden weergegeven in Hallo [activiteitenlogboek](resource-group-audit.md). Validatiefouten worden echter niet weergegeven in de geschiedenis van uw implementatie omdat Hallo implementatie nooit gestart.

## <a name="determine-error-code"></a>Foutcode bepalen

U kunt meer informatie over een fout door te kijken fout het Hallo-bericht en Hallo-foutcode. Hallo [oplossen van veelvoorkomende fouten voor Azure-implementatie met Azure Resource Manager](resource-manager-common-deployment-errors.md) artikel geeft oplossingen-foutcode. Dit onderwerp leest hoe toouse hello Azure portal toodiscover Hallo-foutcode.

### <a name="validation-errors"></a>Validatiefouten

Bij het implementeren via de portal hello, ziet u een validatiefout opgetreden na het verzenden van uw waarden.

![Fout bij de portal validatie weergeven](./media/resource-manager-troubleshoot-tips/validation-error.png)

Selecteer het Hallo-bericht voor meer informatie. In Hallo installatiekopie te volgen, ziet u een **InvalidTemplateDeployment** fout en een bericht verschijnt dat een beleid voor implementatie wordt geblokkeerd.

![validatie details weergeven](./media/resource-manager-troubleshoot-tips/validation-details.png)

### <a name="deployment-errors"></a>Implementatiefouten

Als het Hallo-bewerking is geslaagd, maar niet tijdens de implementatie, ziet u Hallo-fout bij het Hallo-meldingen. Selecteer Hallo-bericht.

![Fout bij wijzigingsbericht](./media/resource-manager-troubleshoot-tips/notification.png)

Ziet u meer informatie over het Hallo-implementatie. Selecteer Hallo optie toofind meer informatie over Hallo-fout.

![implementatie is mislukt](./media/resource-manager-troubleshoot-tips/deployment-failed.png)

Ziet u Hallo-bericht en de fout-foutcodes. Er zijn twee foutcodes. eerste foutcode Hallo (**implementatie mislukt**) is een algemene fout die biedt geen Hallo details u moet toosolve Hallo-fout. tweede foutcode Hallo (**StorageAccountNotFound**) biedt Hallo informatie die u nodig hebt. 

![Details van fouten](./media/resource-manager-troubleshoot-tips/error-details.png)

## <a name="enable-debug-logging"></a>Inschakelen van logboekregistratie voor foutopsporing
Soms moet u meer informatie over het Hallo-aanvraag en -antwoord toodiscover wat er mis ging. U kunt met behulp van PowerShell of Azure CLI aanvragen dat aanvullende informatie wordt geregistreerd tijdens een implementatie.

- PowerShell

   In PowerShell instellen Hallo **DeploymentDebugLogLevel** parameter tooAll, ResponseContent of RequestContent.

  ```powershell
  New-AzureRmResourceGroupDeployment -ResourceGroupName examplegroup -TemplateFile c:\Azure\Templates\storage.json -DeploymentDebugLogLevel All
  ```

   Bekijk Hallo aanvraaginhoud Hello volgende cmdlet:

  ```powershell
  (Get-AzureRmResourceGroupDeploymentOperation -DeploymentName storageonly -ResourceGroupName startgroup).Properties.request | ConvertTo-Json
  ```

   Of Hallo antwoord inhoud met:

  ```powershell
  (Get-AzureRmResourceGroupDeploymentOperation -DeploymentName storageonly -ResourceGroupName startgroup).Properties.response | ConvertTo-Json
  ```

   Deze informatie kunt u bepalen of een waarde in de sjabloon Hallo onjuist wordt ingesteld.

- Azure CLI

   Controleer Hallo implementatiebewerkingen Hello volgende opdracht:

  ```azurecli
  az group deployment operation list --resource-group ExampleGroup --name vmlinux
  ```

- Geneste sjabloon

   toolog foutopsporingsgegevens voor een geneste sjabloon gebruik Hallo **debugSetting** element.

  ```json
  {
      "apiVersion": "2016-09-01",
      "name": "nestedTemplate",
      "type": "Microsoft.Resources/deployments",
      "properties": {
          "mode": "Incremental",
          "templateLink": {
              "uri": "{template-uri}",
              "contentVersion": "1.0.0.0"
          },
          "debugSetting": {
             "detailLevel": "requestContent, responseContent"
          }
      }
  }
  ```


## <a name="create-a-troubleshooting-template"></a>Maken van een sjabloon voor het oplossen van problemen
In sommige gevallen Hallo gemakkelijkste manier tootroubleshoot uw sjabloon is tootest onderdelen hiervan. U kunt een vereenvoudigde sjabloon waarmee u toofocus maken op Hallo-onderdeel dat u van mening bent Hallo fout veroorzaakt. Stel bijvoorbeeld dat u ontvangt een fout opgetreden bij het verwijzen naar een resource. In plaats van te moeten omgaan met een volledige sjabloon, een sjabloon die als resultaat geeft Hallo-onderdeel dat wordt veroorzaakt door het probleem te maken. Dit kunt u bepalen of u aan de juiste parameters hello doorgeeft, met behulp van de sjabloonfuncties correct en Hallo bron ophalen die u verwacht.

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "storageName": {
        "type": "string"
    },
    "storageResourceGroup": {
        "type": "string"
    }
  },
  "variables": {},
  "resources": [],
  "outputs": {
    "exampleOutput": {
        "value": "[reference(resourceId(parameters('storageResourceGroup'), 'Microsoft.Storage/storageAccounts', parameters('storageName')), '2016-05-01')]",
        "type" : "object"
    }
  }
}
```

Of stel fouten implementatie die u van mening bent zijn gerelateerd tooincorrectly afhankelijkheden instellen. Test uw sjabloon door in vereenvoudigde sjablonen op te splitsen. Maak eerst een sjabloon die slechts één bron (zoals een SQL-Server) implementeert. Als u zeker dat u die correct gedefinieerd resource hebt, kunt u een resource die afhankelijk zijn van deze (zoals een SQL-Database) toevoegen. Wanneer u deze twee bronnen onjuist is gedefinieerd hebt, moet u andere afhankelijke resources (zoals controlebeleid) toevoegen. Verwijder Hallo groep toomake zeker dat u voldoende testen Hallo bronafhankelijkheden tussen elke testimplementatie. 

## <a name="check-deployment-sequence"></a>Controleer de volgorde van de implementatie

Veel implementatiefouten gebeuren wanneer een onverwachte reeks resources worden geïmplementeerd. Deze fouten zich voordoen als afhankelijkheden niet correct zijn ingesteld. Wanneer er ontbreekt een vereiste afhankelijkheid, kunt u probeert een resource toouse een waarde op voor een andere bron, maar andere Hallo nog niet bestaat. U krijgt een foutmelding weergegeven dat een bron is niet gevonden. U kunt dit type fout afwisselend tegenkomen, omdat de implementatietijd Hallo voor elke resource kan verschillen. Bijvoorbeeld de eerste poging toodeploy uw resources is gelukt, omdat een vereiste bron willekeurig tijdstip is voltooid. De tweede poging mislukt echter omdat Hallo vereiste resource is niet op tijd voltooid. 

Maar u wilt dat tooavoid instelling afhankelijkheden die niet nodig zijn. Wanneer u onnodige afhankelijkheden hebt, wordt het Hallo-duur van Hallo implementatie verlengen door te voorkomen dat de bronnen die niet afhankelijk van elkaar worden geïmplementeerd parallel. U kunt bovendien circulaire afhankelijkheden die Hallo implementatie blokkeren maken. Hallo [verwijzing](resource-group-template-functions-resource.md#reference) functie maakt een impliciete afhankelijkheid voor de bron waarnaar wordt verwezen hello, als deze bron wordt geïmplementeerd op Hallo dezelfde sjabloon. Daarom wellicht hebt u meer afhankelijkheden dan Hallo afhankelijkheden die zijn opgegeven in Hallo **dependsOn** eigenschap. Hallo [resourceId](resource-group-template-functions-resource.md#resourceid) functie niet maken van een impliciete afhankelijkheid of valideren dat Hallo resource bestaat.

Wanneer u afhankelijkheid problemen ondervindt, moet u toogain inzicht in de Hallo volgorde van de resource-implementatie. tooview hello bewerkingsvolgorde implementatie:

1. Selecteer de implementatiegeschiedenis Hallo voor de resourcegroep.

   ![Geschiedenis van implementatie selecteren](./media/resource-manager-troubleshoot-tips/select-deployment.png)

2. Selecteer een implementatie van Hallo geschiedenis en selecteer **gebeurtenissen**.

   ![gebeurtenissen van de implementatie selecteren](./media/resource-manager-troubleshoot-tips/select-deployment-events.png)

3. Bekijk Hallo reeks gebeurtenissen voor elke resource. Betalen aandacht toohello status van elke bewerking. Hallo ziet volgende afbeelding u bijvoorbeeld drie storage-accounts die geïmplementeerd parallel. U ziet dat Hallo drie storage-accounts zijn gestart op Hallo hetzelfde moment.

   ![Parallelle implementatie](./media/resource-manager-troubleshoot-tips/deployment-events-parallel.png)

   Hallo volgende afbeelding ziet u drie opslagaccounts die niet zijn geïmplementeerd parallel. Hallo tweede storage-account is afhankelijk van Hallo eerste storage-account en Hallo derde storage-account is afhankelijk van Hallo tweede storage-account. Daarom wordt Hallo eerste storage-account gestart, geaccepteerd en voltooid voordat de volgende Hallo is gestart.

   ![sequentiële implementatie](./media/resource-manager-troubleshoot-tips/deployment-events-sequence.png)

Zelfs voor een meer complexe scenario's, kunt u dezelfde techniek toodiscover Hallo toen deze implementatie is gestart en voltooid voor elke resource. Bekijk uw implementatie gebeurtenissen toosee als Hallo sequence anders is dan u verwacht. Zo ja, herzie Hallo afhankelijkheden voor deze bron.

Resource Manager identificeert circulaire afhankelijkheden tijdens de validatie van de sjabloon. Retourneert een foutbericht weergegeven waarin wordt vermeld specifiek een circulaire afhankelijkheid bestaat. toosolve een circulaire afhankelijkheid:

1. In de sjabloon vinden Hallo resource in Hallo circulaire afhankelijkheid geïdentificeerd. 
2. Voor die bron onderzoeken Hallo **dependsOn** eigenschap en elk gebruik van Hallo **verwijzing** toosee welke resources afhankelijk van is werken. 
3. Bekijk deze resources toosee welke bronnen ze afhankelijk zijn. Volg Hallo afhankelijkheden totdat u een resource die afhankelijk van de oorspronkelijke bron Hallo is merkt.
5. Voor Hallo bronnen die zijn betrokken bij Hallo circulaire afhankelijkheid zorgvuldig al gebruik van Hallo **dependsOn** eigenschap tooidentify eventuele afhankelijkheden die niet nodig zijn. Verwijder deze afhankelijkheden. Als u niet zeker weet dat er een afhankelijkheid is vereist, probeert u het verwijdert. 
6. Hallo-sjabloon implementeren.

Verwijderen van waarden uit Hallo **dependsOn** eigenschap kan fouten veroorzaken wanneer u Hallo sjabloon implementeert. Als er een fout optreden, moet u de afhankelijkheid Hallo terug naar het Hallo-sjabloon toevoegen. 

Als deze aanpak Hallo circulaire afhankelijkheid niet wordt opgelost, kunt u deel uitmaakt van uw implementatie logica verplaatsen naar onderliggende resources (zoals extensies of configuratie-instellingen). Deze onderliggende resources toodeploy na Hallo resources van Hallo circulaire afhankelijkheid configureren. Stel bijvoorbeeld dat u twee virtuele machines implementeert, maar u moet eigenschappen instellen voor elk veld dat toohello andere verwijzen. U kunt deze implementeren in Hallo volgorde:

1. vm1
2. vm2
3. Extensie op vm1, is afhankelijk van vm1 en vm2. Hallo-extensie waarden ingesteld op vm1 die van vm2 krijgt.
4. Extensie op vm2, is afhankelijk van vm1 en vm2. Hallo-extensie waarden ingesteld op vm2 van van vm1 krijgt.

Hallo dezelfde methode voor App Service-apps werkt. Overweeg configuratiewaarden verplaatsen naar een onderliggende resource van resource Hallo-app. U kunt twee web-apps in Hallo volgorde kunt implementeren:

1. webapp1
2. webapp2
3. configuratie voor webapp1, is afhankelijk van webapp1 en webapp2. Het bevat app-instellingen met waarden uit webapp2.
4. configuratie voor webapp2, is afhankelijk van webapp1 en webapp2. Het bevat app-instellingen met waarden uit webapp1.


## <a name="next-steps"></a>Volgende stappen
* Zie voor oplossingen toocommon implementatiefouten, [oplossen van veelvoorkomende fouten voor Azure-implementatie met Azure Resource Manager](resource-manager-common-deployment-errors.md).
* toolearn over het controleren van acties, Zie [bewerkingen met Resource Manager controleren](resource-group-audit.md).
* Zie toolearn over acties toodetermine Hallo fouten tijdens de implementatie van [implementatiebewerkingen weergeven](resource-manager-deployment-operations.md).

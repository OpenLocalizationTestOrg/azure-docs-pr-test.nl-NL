---
title: aaaView Azure activiteit logboeken toomonitor resources | Microsoft Docs
description: Gebruik Hallo activiteit logboeken tooreview-gebruikersacties en fouten. Toont PowerShell voor Azure Portal, Azure CLI en REST.
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: fcdb3125-13ce-4c3b-9087-f514c5e41e73
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: tomfitz
ms.openlocfilehash: 8430ed2a9c1dfe5f13423a55d358e590b0facb22
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="view-activity-logs-tooaudit-actions-on-resources"></a>Activiteit weergeven registreert tooaudit acties voor bronnen
Via activiteitenlogboeken, kunt u bepalen:

* welke bewerkingen zijn uitgevoerd op Hallo van resources in uw abonnement
* wie Hallo-bewerking gestart (Hoewel de bewerkingen die zijn gestart door een back-endservice niet retourneren een gebruiker als Hallo aanroeper)
* Wanneer Hallo-bewerking heeft plaatsgevonden
* Hallo-status van Hallo-bewerking
* Hallo-waarden van andere eigenschappen die u kunnen helpen onderzoek Hallo-bewerking

[!INCLUDE [resource-manager-audit-limitations](../../includes/resource-manager-audit-limitations.md)]

U kunt informatie ophalen uit Hallo activiteitenlogboeken via Hallo portal, PowerShell, Azure CLI, inzicht REST API of [Insights .NET-bibliotheek](https://www.nuget.org/packages/Microsoft.Azure.Insights/).

## <a name="portal"></a>Portal
1. tooview hello activiteitenlogboeken via Hallo-portal, selecteer **Monitor**.
   
    ![Selecteer activiteitenlogboeken](./media/resource-group-audit/select-monitor.png)

   Of tooautomatically filter Hallo-logboek voor een bepaalde bron of de resourcegroep, selecteer **activiteitenlogboek** van die resourceblade. U ziet dat activiteitenlogboek hello wordt automatisch gefilterd op Hallo geselecteerd resource.
   
    ![filteren op resource](./media/resource-group-audit/filtered-by-resource.png)
2. In Hallo **activiteitenlogboek** blade ziet u een overzicht van recente bewerkingen.
   
    ![acties weergeven](./media/resource-group-audit/audit-summary.png)
3. toorestrict hello aantal bewerkingen die worden weergegeven, met selecteren verschillende voorwaarden. Hallo volgende afbeelding ziet u bijvoorbeeld Hallo **Timespan** en **gebeurtenis wordt gestart door** velden gewijzigd tooview Hallo acties die door een bepaalde gebruiker of toepassing voor Hallo afgelopen maand. Selecteer **toepassen** tooview Hallo resultaten van de query.
   
    ![Stel filteropties](./media/resource-group-audit/set-filter.png)

4. Als u toorun Hallo query later nodig hebt, selecteert u **opslaan** en Hallo query een naam geven.
   
    ![query opslaan](./media/resource-group-audit/save-query.png)
5. tooquickly een query uitvoert, kunt u een van de ingebouwde Hallo-query's zoals mislukte implementatie.

    ![query selecteren](./media/resource-group-audit/select-quick-query.png)

   de geselecteerde query Hallo wordt automatisch ingesteld filterwaarden Hallo vereist.

    ![implementatie-fouten weergeven](./media/resource-group-audit/view-failed-deployment.png)   

6. Selecteer een van de Hallo operations toosee een samenvatting van Hallo-gebeurtenis.

    ![de bewerking weergeven](./media/resource-group-audit/view-operation.png)  

## <a name="powershell"></a>PowerShell
1. de logboekvermeldingen tooretrieve, Hallo uitvoeren **Get-AzureRmLog** opdracht. U vindt aanvullende parameters toofilter Hallo lijst met items. Als u een begin- en -tijd niet opgeeft, worden vermeldingen voor laatste uur Hallo geretourneerd. Bijvoorbeeld: tooretrieve Hallo-bewerkingen voor een resourcegroep tijdens Hallo afgelopen uur uitgevoerd:

  ```powershell
  Get-AzureRmLog -ResourceGroup ExampleGroup
  ```
   
    Hallo volgende voorbeeld ziet u hoe toouse Hallo activiteit Meld tooresearch bewerkingen die zijn uitgevoerd tijdens een opgegeven periode. Hallo zijn begin- en einddatums opgegeven in een datumnotatie.

  ```powershell
  Get-AzureRmLog -ResourceGroup ExampleGroup -StartTime 2015-08-28T06:00 -EndTime 2015-09-10T06:00
  ```

    Of u kunt functies toospecify Hallo datum datumbereik, zoals Hallo afgelopen 14 dagen.
   
  ```powershell 
  Get-AzureRmLog -ResourceGroup ExampleGroup -StartTime (Get-Date).AddDays(-14)
  ```

2. Afhankelijk van het Hallo-begintijd die u opgeeft, kunnen Hallo eerdere opdrachten een lange lijst met bewerkingen voor Hallo resourcegroep geretourneerd. U kunt filteren Hallo resultaten voor wat u zoekt dankzij de zoekcriteria voldoen. Als u tooresearch hoe een web-app is gestopt probeert, kunt u bijvoorbeeld Hallo volgende opdracht uitvoeren:

  ```powershell
  Get-AzureRmLog -ResourceGroup ExampleGroup -StartTime (Get-Date).AddDays(-14) | Where-Object OperationName -eq Microsoft.Web/sites/stop/action
  ```

    Die in dit voorbeeld ziet u dat een stopactie is uitgevoerd door someone@contoso.com. 

  ```powershell 
  Authorization     :
  Scope     : /subscriptions/xxxxx/resourcegroups/ExampleGroup/providers/Microsoft.Web/sites/ExampleSite
  Action    : Microsoft.Web/sites/stop/action
  Role      : Subscription Admin
  Condition :
  Caller            : someone@contoso.com
  CorrelationId     : 84beae59-92aa-4662-a6fc-b6fecc0ff8da
  EventSource       : Administrative
  EventTimestamp    : 8/28/2015 4:08:18 PM
  OperationName     : Microsoft.Web/sites/stop/action
  ResourceGroupName : ExampleGroup
  ResourceId        : /subscriptions/xxxxx/resourcegroups/ExampleGroup/providers/Microsoft.Web/sites/ExampleSite
  Status            : Succeeded
  SubscriptionId    : xxxxx
  SubStatus         : OK
  ```

3. U kunt opzoeken Hallo-acties die door een bepaalde gebruiker, zelfs voor een resourcegroep die niet meer bestaat.

  ```powershell 
  Get-AzureRmLog -ResourceGroup deletedgroup -StartTime (Get-Date).AddDays(-14) -Caller someone@contoso.com
  ```

4. U kunt filteren op mislukte bewerkingen.

  ```powershell
  Get-AzureRmLog -ResourceGroup ExampleGroup -Status Failed
  ```

5. U kunt zich richten op één fout door te kijken Hallo statusbericht voor dat item.
   
        ((Get-AzureRmLog -Status Failed -ResourceGroup ExampleGroup -DetailedOutput).Properties[1].Content["statusMessage"] | ConvertFrom-Json).error
   
    Die wordt geretourneerd:
   
        code           message                                                                        
        ----           -------                                                                        
        DnsRecordInUse DNS record dns.westus.cloudapp.azure.com is already used by another public IP. 


## <a name="azure-cli"></a>Azure CLI
* logboekvermeldingen tooretrieve, u Hallo uitvoeren **azure-groep logboek weergeven** opdracht.

  ```azurecli
  azure group log show ExampleGroup --json
  ```


## <a name="rest-api"></a>REST API
Hallo REST-bewerkingen voor het werken met Hallo activiteitenlogboek deel uitmaken van Hallo [Insights REST-API](https://msdn.microsoft.com/library/azure/dn931943.aspx). tooretrieve activiteit logboekgebeurtenissen, Zie [lijst Hallo management gebeurtenissen in een abonnement](https://msdn.microsoft.com/library/azure/dn931934.aspx).

## <a name="next-steps"></a>Volgende stappen
* Azure activiteitenlogboeken kunnen worden gebruikt met Power BI toogain meer inzicht over Hallo-acties in uw abonnement. Zie [weergeven en analyseren van Azure activiteitenlogboeken in Power BI en meer](https://azure.microsoft.com/blog/analyze-azure-audit-logs-in-powerbi-more/).
* toolearn over het instellen van beveiligingsbeleid, Zie [toegangsbeheer op basis van rollen in Azure](../active-directory/role-based-access-control-configure.md).
* toolearn over Hallo-opdrachten voor het weergeven van implementatiebewerkingen, Zie [implementatiebewerkingen weergeven](resource-manager-deployment-operations.md).
* hoe tooprevent verwijderingen van een resource voor alle gebruikers zien toolearn [resources met Azure Resource Manager vergrendelen](resource-group-lock-resources.md).


---
title: Service Fabric-toepassingen met behulp van logboekanalyse aaaAssess hello Azure-portal | Microsoft Docs
description: U kunt Hallo Service Fabric oplossing gebruiken in hello Azure portal tooassess Hallo risico en status van uw Service Fabric-toepassingen met logboekanalyse micro-services, knooppunten en clusters.
services: log-analytics
documentationcenter: 
author: niniikhena
manager: jochan
editor: 
ms.assetid: 9c91aacb-c48e-466c-b792-261f25940c0c
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: nini
ms.openlocfilehash: 891c7f6e5ed511ac18599bdc280ab3dc09700fbe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="assess-service-fabric-applications-and-micro-services-with-hello-azure-portal"></a>Evalueer Service Fabric-toepassingen en micro-services met hello Azure-portal

> [!div class="op_single_selector"]
> * [Resource Manager](log-analytics-service-fabric-azure-resource-manager.md)
> * [PowerShell](log-analytics-service-fabric.md)
>
>

![Service Fabric symbool](./media/log-analytics-service-fabric/service-fabric-assessment-symbol.png)

Dit artikel wordt beschreven hoe toouse Hallo Service Fabric-oplossing in logboekanalyse toohelp identificeren en oplossen van problemen in uw Service Fabric-cluster.

Hallo Service Fabric-oplossing gebruikt Azure Diagnostics-gegevens van uw virtuele machines van Service Fabric door het verzamelen van deze gegevens uit uw af van de Azure-tabellen. Log Analytics leest vervolgens de Service Fabric framework gebeurtenissen, met inbegrip van **betrouwbare servicegebeurtenissen**, **Actor gebeurtenissen**, **operationele gebeurtenissen**, en **aangepaste ETW-gebeurtenissen**. Dashboard van de oplossing hello bent u problemen die aandacht vereisen kunnen tooview en relevante gebeurtenissen in uw omgeving Service Fabric.

tooget gestart met Hallo-oplossing, moet u tooconnect uw Service Fabric-werkruimte voor logboekanalyse cluster tooa. Hier volgen drie scenario's tooconsider:

1. Als u uw Service Fabric-cluster niet hebt geïmplementeerd, gebruikt u de stappen Hallo in ***implementeren van een werkruimte voor logboekanalyse tooa Service Fabric-Cluster aangesloten*** toodeploy een nieuw cluster en hebt geconfigureerd tooreport tooLog Analytics.
2. Als u toocollect prestatiemeteritems uit uw hosts toouse andere OMS-oplossingen zoals beveiliging op uw Service Fabric-Cluster moet, stappen Hallo in ***implementeren van een werkruimte voor logboekanalyse tooa Service Fabric-Cluster verbonden met het VM-extensie geïnstalleerd.***
3. Als u al uw Service Fabric-cluster hebt geïmplementeerd en tooconnect wilt het tooLog Analytics, Hallo stappen in ***toevoegen van een bestaande opslag account tooLog Analytics.***

## <a name="deploy-a-service-fabric-cluster-connected-tooa-log-analytics-workspace"></a>Implementeer een werkruimte voor logboekanalyse tooa Service Fabric-Cluster is verbonden.
Deze sjabloon Hallo te volgen:

1. Een Azure Service Fabric-werkruimte voor logboekanalyse cluster al verbonden tooa implementeert. U hebt een nieuwe werkruimte Hallo optie toocreate tijdens het Hallo-sjabloon of invoer Hallo-naam van een bestaande werkruimte voor logboekanalyse implementeren.
2. Werkruimte voor logboekanalyse van Hallo diagnostische storage account toohello toegevoegd.
3. Hiermee schakelt u Hallo Service Fabric-oplossing in de werkruimte voor logboekanalyse.

[![TooAzure implementeren](./media/log-analytics-service-fabric/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fazure%2Fazure-quickstart-templates%2Fmaster%2Fservice-fabric-oms%2F%2Fazuredeploy.json)

Als u hebt geselecteerd wordt Hallo hierboven op de knop implementeren, hello Azure portal wordt geopend met de parameters voor u tooedit. Worden toocreate ervoor een nieuwe resourcegroep als invoer van de naam van een nieuwe Log Analytics-werkruimte:

![Service Fabric](./media/log-analytics-service-fabric/2.png)

![Service Fabric](./media/log-analytics-service-fabric/3.png)

Accepteer de juridische voorwaarden Hallo en klik op **maken** toostart Hallo-implementatie. Zodra het Hallo-implementatie is voltooid, moet u nieuwe werkruimte Hallo en cluster gemaakt zien en Hallo WADServiceFabric * gebeurtenissen, WADWindowsEventLogs en WADETWEvent tabellen die zijn toegevoegd:

![Service Fabric](./media/log-analytics-service-fabric/4.png)

## <a name="deploy-a-service-fabric-cluster-connected-tooa-log-analytics-workspace-with-vm-extension-installed"></a>Implementeer een werkruimte voor logboekanalyse tooa Service Fabric-Cluster verbonden met VM-extensie is geïnstalleerd.

Deze sjabloon Hallo te volgen:

1. Een Azure Service Fabric-werkruimte voor logboekanalyse cluster al verbonden tooa implementeert. U kunt een nieuwe werkruimte maken of een bestaande gebruiken.
2. Werkruimte voor logboekanalyse van Hallo diagnostische storage accounts toohello toegevoegd.
3. Hiermee schakelt u Hallo Service Fabric-oplossing in de werkruimte voor logboekanalyse Hallo.
4. Hallo MMA agentextensie installeert in elke virtuele-machineschaalset ingesteld in het Service Fabric-cluster. Hallo MMA agent is geïnstalleerd, bent u maatstaven voor prestaties kunnen tooview over uw knooppunten.

[![TooAzure implementeren](./media/log-analytics-service-fabric/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fazure%2Fazure-quickstart-templates%2Fmaster%2Fservice-fabric-vmss-oms%2F%2Fazuredeploy.json)

Hieronder worden dezelfde stappen hierboven benodigde parameters op invoer Hallo Hallo en ere van een implementatie. Weer ziet u de nieuwe werkruimte hello, cluster en af tabellen alle gemaakte:

![Service Fabric](./media/log-analytics-service-fabric/5.png)

### <a name="viewing-performance-data"></a>Weergeven van prestatiegegevens

tooview prestatiegegevens van de knooppunten:


[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

- Start Hallo werkruimte voor logboekanalyse van hello Azure-portal.
  ![Service Fabric](./media/log-analytics-service-fabric/6.png)
- TooSettings gaat op Hallo linkerdeelvenster en selecteer gegevens >> Windows-prestatiemeteritems >> 'hello toevoegen geselecteerd prestatiemeteritems': ![Service Fabric](./media/log-analytics-service-fabric/7.png)
- In logboek zoeken, gebruikt u Hallo toodelve query's in de belangrijkste metrische gegevens over uw knooppunten te volgen:

    a. Vergelijken gemiddelde CPU-gebruik op alle knooppunten in Hallo laatste één uur toosee welke knooppunten hebben problemen met het Hallo en met welke tijdsinterval een knooppunt dat opnieuw moest een piek:

    ```
    Type=Perf ObjectName=Processor CounterName="% Processor Time"|measure avg(CounterValue) by Computer Interval 1HOUR.
    ```

    ![Service Fabric](./media/log-analytics-service-fabric/10.png)

    b. Vergelijkbare lijndiagrammen voor het beschikbare geheugen op elk knooppunt in deze query weergeven:

    ```
    Type=Perf ObjectName=Memory CounterName="Available MBytes Memory" | measure avg(CounterValue) by Computer Interval 1HOUR.
    ```

    een lijst met alle knooppunten, waarbij Hallo exacte gemiddelde waarde voor beschikbare megabytes (MB) voor elk knooppunt tooview Gebruik deze query:

    ```
    Type=Perf (ObjectName=Memory) (CounterName="Available MBytes") | measure avg(CounterValue) by Computer
    ```

    ![Service Fabric](./media/log-analytics-service-fabric/11.png)

    c. In geval van Hallo gewenste toodrill omlaag in een specifiek knooppunt door in elk uur gemiddelde hello, minimum, maximum en 75 percentiel CPU-gebruik, je kunt toodo dit door met behulp van deze query (vervangen veld Computer):

    ```
    Type=Perf CounterName="% Processor Time" InstanceName=_Total Computer="BaconDC01.BaconLand.com"| measure min(CounterValue), avg(CounterValue), percentile75(CounterValue), max(CounterValue) by Computer Interval 1HOUR
    ```

    ![Service Fabric](./media/log-analytics-service-fabric/12.png)

Meer informatie lezen over maatstaven voor prestaties in logboekanalyse op Hallo [Operations Management Suite-blog](https://blogs.technet.microsoft.com/msoms/tag/metrics/).


## <a name="adding-an-existing-storage-account-toolog-analytics"></a>Toevoegen van een bestaande opslag account tooLog Analytics

Deze sjabloon wordt gewoon de bestaande opslag accounts tooa nieuwe of bestaande werkruimte voor logboekanalyse toevoegen

[![TooAzure implementeren](./media/log-analytics-service-fabric/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Foms-existing-storage-account%2Fazuredeploy.json)

> [!NOTE]
> Als u met een bestaande werkruimte voor logboekanalyse werkt, selecteert u bij het selecteren van een resourcegroep 'Bestaande gebruiken' en zoek naar de resourcegroep Hallo met Hallo Log Analytics-werkruimte. Maak een nieuwe één als anders.
> ![Service Fabric](./media/log-analytics-service-fabric/8.png)
>
>

Nadat u deze sjabloon is geïmplementeerd, kunt u zich kunt toosee Hallo storage account verbonden tooyour logboekanalyse werkruimte. In dit exemplaar toegevoegd ik een meer storage account toohello Exchange werkruimte ik die eerder is gemaakt.
![Service Fabric](./media/log-analytics-service-fabric/9.png)

## <a name="view-service-fabric-events"></a>Service Fabric-gebeurtenissen weergeven

Eenmaal Hallo implementaties zijn voltooid en Hallo Service Fabric-oplossing in uw werkruimte is ingeschakeld, selecteert u Hallo **Service Fabric** -tegel in Hallo logboekanalyse portal toolaunch Hallo Service Fabric dashboard. Hallo dashboard bevat Hallo kolommen in de volgende tabel Hallo. Elke kolom bevat Hallo bovenste 10 gebeurtenissen door het aantal die overeenkomt met dat van de kolom criteria voor Hallo tijdbereik opgegeven. U kunt een zoekopdracht logboek waarmee de volledige lijst Hallo door te klikken op uitvoeren **alle** onderin Hallo rechts van elke kolom, of door te klikken op de kolomkop Hallo.

| **Service Fabric-gebeurtenis** | **Beschrijving** |
| --- | --- |
| Problemen die aandacht vereisen |Een weergave van de problemen zoals RunAsyncFailures RunAsynCancellations en keuzelijsten knooppunt. |
| Operationele gebeurtenissen |Operationele gebeurtenissen zoals upgrade van de toepassing en implementaties aandacht vereisen. |
| Gebeurtenissen van betrouwbare Service |Opmerkelijke betrouwbare servicegebeurtenissen dergelijke Runasyncinvocations. |
| Actor-gebeurtenissen |Opmerkelijke actor-gebeurtenissen die worden gegenereerd door uw micro-services, zoals uitzonderingen worden veroorzaakt door een actormethode, actor-activeringen en deactivations, enzovoort. |
| Toepassingsgebeurtenissen |Alle aangepaste ETW-gebeurtenissen die worden gegenereerd door uw toepassingen. |

![Service Fabric-dashboard](./media/log-analytics-service-fabric/sf3.png)

![Service Fabric-dashboard](./media/log-analytics-service-fabric/sf4.png)

Hallo volgende tabel bevat de methoden van de collectie en andere informatie over hoe gegevens worden verzameld voor Service Fabric.

| Platform | Directe Agent | Operations Manager-agent | Azure Storage | Operations Manager is vereist? | Operations Manager-agent gegevens verzonden via de beheergroep | Frequentie van de verzameling |
| --- | --- | --- | --- | --- | --- | --- |
| Windows |  |  | &#8226; |  |  |10 minuten |

> [!NOTE]
> U kunt Hallo bereik van deze gebeurtenissen in Service Fabric-oplossing Hallo wijzigen door te klikken op **gegevens op basis van de afgelopen 7 dagen** Hallo boven aan het Hallo-dashboard. U kunt ook gebeurtenissen gegenereerd binnen Hallo afgelopen zeven dagen een dag of zes uur weergeven. U kunt ook selecteren **aangepaste** toospecify een aangepast datumbereik.
>
>

## <a name="next-steps"></a>Volgende stappen

* Gebruik [logboek van zoekopdrachten in logboekanalyse](log-analytics-log-searches.md) tooview gedetailleerde gegevens voor Service Fabric-gebeurtenis.

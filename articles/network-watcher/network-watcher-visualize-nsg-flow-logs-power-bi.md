---
title: aaaVisualizing Netwerkbeveiligingsgroep Azure stroom logboeken met Power BI | Microsoft Docs
description: Deze pagina wordt beschreven hoe toovisualize NSG stroom registreert met Power BI.
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 1e4f95fa-f5f0-4e03-bc25-008fbfc4934c
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: d9adcf256df8fed68c39be1a026ca64cc6b5c6d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="visualizing-network-security-group-flow-logs-with-power-bi"></a>Netwerkbeveiligingsgroep visualizing stroom logboeken met Power BI

Netwerkbeveiligingsgroep stroom logboeken toestaan tooview informatie over inkomende en uitgaande IP-verkeer op Netwerkbeveiligingsgroepen. Deze stroom logboeken weergeven uitgaande en inkomende stromen per regel op basis van een Hallo NIC Hallo stroom is van toepassing op 5-tuple informatie over het Hallo-stroom (IP bron/het doel, bron/het doel-poort Protocol) en als Hallo verkeer is toegestaan of geweigerd.

Het kan lastig toogain inzicht in de logboekregistratie van gegevens door te zoeken handmatig logboekbestanden Hallo stroom zijn. In dit artikel bieden we een oplossing toovisualize uw meest recente flow logboeken en meer informatie over verkeer op uw netwerk.

## <a name="scenario"></a>Scenario

We verbinding Power BI desktop toohello storage-account die we voor onze gegevens NSG stromen logboekregistratie hebt geconfigureerd als sink Hallo Hallo scenario te volgen, maken. Nadat we tooour storage-account verbinding hebt gemaakt, wordt in Power BI downloadt en parseert Hallo logboeken tooprovide een visuele representatie van het Hallo-verkeer dat is vastgelegd door netwerkbeveiligingsgroepen.

Met behulp van Hallo visuele elementen die zijn opgegeven in het Hallo-sjabloon die u kunt controleren:

* Bovenste Talkers
* Tijd stromen reeksgegevens richting en regel beschikking
* Stromen door Network Interface-MAC-adres
* Stromen door het NSG en de regel
* Stromen door doelpoort

Hallo sjabloon kan worden bewerkt zodat u kunt deze nieuwe gegevens tooadd, visuele elementen, wijzigen of bewerken van query's toosuit uw behoeften.

## <a name="setup"></a>Instellen

Voordat u begint, kunt u Network Security groep stromen-logboekregistratie is ingeschakeld op een of meer Netwerkbeveiligingsgroepen in uw account moet hebben. Voor instructies over het inschakelen van netwerkbeveiliging stromen Logboeken, raadpleeg dan toohello volgende artikel: [inleiding tooflow logboekregistratie voor Netwerkbeveiligingsgroepen](network-watcher-nsg-flow-logging-overview.md).

U moet ook Hallo Power BI Desktop client is geïnstalleerd op uw computer en genoeg ruimte vrij op uw machine toodownload en de belasting Hallo logboekgegevens die in uw storage-account voorkomt hebben.

![Visio-diagram][1]

### <a name="steps"></a>Stappen

1. De download- en open Hallo volgende van Power BI-sjabloon in Power BI Desktop toepassing hello [netwerk-Watcher Power BI-stroom logboeken sjabloon](https://aka.ms/networkwatcherpowerbiflowlogstemplate)
1. Voer de queryparameters Hallo vereist
    1. **StorageAccountName** – geeft toohello naam van Hallo storage-account met Hallo NSG stroom logboeken die u wilt tooload en visualiseren.
    1. **NumberOfLogFiles** – Hiermee geeft u het aantal logboekbestanden dat u wilt toodownload en in Power BI visualiseren Hallo. Bijvoorbeeld, als 50 is opgegeven, Hallo 50 meest recente logboekbestanden. FF hebben we 2 nsg's ingeschakeld en geconfigureerd toosend NSG stroom logboeken toothis account vervolgens hello afgelopen 25 uur aan logbestanden kunnen worden weergegeven.

    ![Power BI main][2]

1. Voer Hallo toegangssleutel voor uw opslagaccount. U kunt geldig toegangstoetsen vinden door te navigeren tooyour storage-account in hello Azure portal en selecteert **toegangstoetsen** in Hallo-instellingen. Klik op **Connect** past u wijzigingen toe.

    ![Toegangstoetsen][3]

    ![toegangssleutel 2][4]

4.  Uw logboeken worden gedownload en geparseerd en kunt u nu gebruikmaken van vooraf gemaakte visuele elementen Hallo.

## <a name="understanding-hello-visuals"></a>Understanding Hallo visuele elementen

Opgegeven in Hallo sjabloon zijn een set van visuele elementen waarmee logisch Hallo NSG stromen logboekgegevens. Hallo volgende afbeeldingen ziet u een voorbeeld van welke dashboard Hallo eruit wanneer gevuld met gegevens. Hieronder wordt elke visual met meer details onderzoeken 

![Power BI][5]
 
Hallo boven Talkers visual toont Hallo IP-adressen die zijn geïnitieerd Hallo meeste verbindingen via Hallo opgegeven periode. Hallo-grootte van de vakken Hallo komt overeen toohello relatieve aantal verbindingen. 

![toptalkers][6]

Hallo weergeven volgende time series-grafieken Hallo aantal overdrachten Hallo periode. Hallo bovenste grafiek wordt gesegmenteerd op Hallo stroomrichting en lagere hello wordt gesegmenteerd op Hallo beslissingen (toestaan of weigeren). Met dit visuele element, kunt u onderzoeken van uw verkeer trends na verloop van tijd en eventuele abnormale pieken herkennen of daling van verkeer of verkeer segmentering.

![flowsoverperiod][7]

Hallo volgende grafieken wordt aangegeven Hallo stromen per netwerkinterface met Hallo bovenste gesegmenteerd op stroomrichting en Hallo lagere gesegmenteerd op beslissingen. Met deze informatie krijgt u inzicht in welke van uw virtuele machines gecommuniceerd meeste relatieve tooothers hello, en als verkeer tooa specifieke virtuele machine wordt toegestaan of geweigerd.

![flowspernic][8]

Hallo na ring wheel-grafiek kunt een uitsplitsing van stromen door doelpoort. Met deze informatie vindt u Hallo meest gebruikte doelpoorten gebruikt binnen Hallo opgegeven periode.

![Ring][9]

Hallo ziet volgende staafdiagram Hallo stroom door het NSG en de regel. Met deze informatie ziet u nsg's die verantwoordelijk is voor Hallo Hallo meeste verkeer en Hallo uitsplitsing van verkeer op een NSG door regel.

![barchart][10]
 
Hallo volgende informatief grafieken weergave-informatie over Nsg Hallo aanwezig is in Logboeken hello, Hallo aantal overdrachten vastgelegd via hello, en -datum Hallo van Hallo vroegste logboek vastgelegd. Deze informatie kunt u een idee van welke nsg's worden vastgelegd en Hallo datumbereik van stromen.

![infochart1][11]

![infochart2][12]

Deze sjabloon bevat Hallo volgende slicers tooallow u tooview enige Hallo gegevens u meest geïnteresseerd bent in. U kunt filteren op uw resourcegroepen, nsg's en regels. U kunt ook filteren op 5-tuple informatie, besluit en Hallo tijd Hallo-logboek is geschreven.

![slicers][13]

## <a name="conclusion"></a>Conclusie

We bleek in dit scenario dat via het netwerk beveiliging groep overgebracht logboeken die worden geleverd door Power BI en netwerk-Watcher we kunnen toovisualize en Hallo-verkeer begrijpen. Met behulp van de sjabloon Hallo opgegeven Power BI Hallo logboeken rechtstreeks uit storage downloadt en verwerkt deze lokaal. Gebruikte tijd tooload Hallo sjabloon varieert al naar gelang het aantal bestanden die zijn aangevraagd Hallo en totale grootte van bestanden worden gedownload.

U kunt gratis toocustomize deze sjabloon voor uw behoeften. Er zijn veel verschillende manieren u Power BI kunt gebruiken met het netwerk groep stromen beveiligingslogboeken. 

## <a name="notes"></a>Opmerkingen

* Logboeken standaard worden opgeslagen in`https://{storageAccountName}.blob.core.windows.net/insights-logs-networksecuritygroupflowevent/`

    * Als andere gegevens in een andere directory bestaat deze query's toopull Hallo en proces Hallo gegevens moeten worden gewijzigd.

* Hallo opgegeven sjabloon wordt niet aanbevolen voor gebruik met meer dan 1 GB van Logboeken.

* Als u een grote hoeveelheid Logboeken hebt, raden wij onderzoeken van een oplossing met behulp van een ander gegevensarchief zoals Data Lake of SQL server.

## <a name="next-steps"></a>Volgende stappen

Meer informatie over hoe toovisualize uw NSG-flow registreert Hello Elastick Stack in via [visualiseren netwerkverkeer patronen tooand van uw virtuele machines met open-source hulpprogramma's](network-watcher-using-open-source-tools.md)

[1]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure1.png
[2]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure2.png
[3]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure3.png
[4]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure4.png
[5]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure5.png
[6]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure6.png
[7]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure7.png
[8]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure8.png
[9]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure9.png
[10]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure10.png
[11]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure11.png
[12]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure12.png
[13]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure13.png

---
title: patronen in aaaVisualize het netwerkverkeer met Azure-netwerk-Watcher en open-source hulpprogramma's | Microsoft Docs
description: Deze pagina wordt beschreven hoe toouse netwerk-Watcher pakket vastleggen met Capanalysis toovisualize verkeer patronen tooand van uw virtuele machines.
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 936d881b-49f9-4798-8e45-d7185ec9fe89
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: fca9a226729162cd90d412c7b699ac54d2257a0d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="visualize-network-traffic-patterns-tooand-from-your-vms-using-open-source-tools"></a>Visualiseren netwerkverkeer patronen tooand van uw virtuele machines met open-source hulpprogramma 's

Pakket opnamen bevatten gegevens van het netwerk waarmee u tooperform netwerk forensisch en grondige inspecties van pakketten. Er zijn veel wordt geopend, source hulpprogramma's kunt u tooanalyze pakket opnamen toogain inzicht te krijgen over uw netwerk. Een van deze programma is CapAnalysis, een visualisatie pakket open-source hulpprogramma. Pakket vastleggen gegevens te visualiseren is een waardevolle manier tooquickly afgeleid insights op patronen en afwijkingen in uw netwerk. Visualisaties bieden ook een manier om dergelijke insights te delen op een manier eenvoudig worden gebruikt.

Azure netwerk-Watcher biedt dat u de mogelijkheid toocapture deze waardevolle gegevens doordat u tooperform pakket vastgelegd Hallo in uw netwerk. We bieden een overzicht van hoe toovisualize en beter inzicht in het pakket worden vastgelegd met behulp van CapAnalysis met netwerk-Watcher in dit artikel.

## <a name="scenario"></a>Scenario

Hebt u een eenvoudige webtoepassing geïmplementeerd op een virtuele machine in Azure wilt toouse open-source hulpprogramma's voor toovisualize de netwerk-verkeer tooquickly stroom patronen en eventuele mogelijke afwijkingen identificeren. U kunt met de netwerk-Watcher verkrijgen van een pakketopname van uw netwerkomgeving en bewaar deze rechtstreeks van uw opslagaccount. CapAnalysis kunt opnemen pakketopname van Hallo rechtstreeks van Hallo storage-blob en visualiseren van de inhoud ervan.

![scenario][1]

## <a name="steps"></a>Stappen

### <a name="install-capanalysis"></a>CapAnalysis installeren

tooinstall CapAnalysis op een virtuele machine, raadpleegt u de officiële instructies toohello hier https://www.capanalysis.net/ca/how-to-install-capanalysis.
In volgorde extern toegang tot CapAnalysis, moeten we tooopen poort 9877 op de virtuele machine door een nieuwe beveiligingsregel voor binnenkomende toe te voegen. Voor meer informatie over het maken van regels in Netwerkbeveiligingsgroepen, Raadpleeg te[regels maken in een bestaande NSG](../virtual-network/virtual-networks-create-nsg-arm-pportal.md#create-rules-in-an-existing-nsg). Zodra het Hallo-regel is toegevoegd, moet u kunnen tooaccess CapAnalysis uit`http://<PublicIP>:9877`

### <a name="use-azure-network-watcher-toostart-a-packet-capture-session"></a>Azure-netwerk-Watcher toostart een pakket vastleggen sessie gebruiken

Netwerk-Watcher kunt u toocapture pakketten tootrack binnenkomend en uitgaand verkeer een virtuele machine. U kunt verwijzen toohello instructies op de [beheren pakket worden vastgelegd met de netwerk-Watcher](network-watcher-packet-capture-manage-portal.md) toostart een pakket vastleggen sessie. Deze pakketopname kan worden opgeslagen in een opslag-blob toobe toegankelijk is voor CapAnalysis.

### <a name="upload-a-packet-capture-toocapanalysis"></a>Uploaden van een pakket vastleggen tooCapAnalysis
U kunt rechtstreeks uploaden een pakketopname die door de netwerk-watcher Hallo 'Importeren van URL' tabblad en het geven van een koppeling toohello storage-blob waar Hallo pakketopname wordt opgeslagen.

Wanneer een koppeling tooCapAnalysis biedt, zorg ervoor dat tooappend een SAS-token toohello storage blob-URL.  toodo, tooShared toegangshandtekening van het opslagaccount Hallo navigeren, Hallo toegestane machtigingen toewijzen en druk op Hallo SAS genereren knop toocreate een token. Vervolgens kunt u deze SAS-token toohello pakket vastleggen opslag blob-URL toevoegen.

Hallo resulterende URL ziet er ongeveer als volgt: http://storageaccount.blob.core.windows.net/container/location?addSASkeyhere


### <a name="analyzing-packet-captures"></a>Analyseren van pakket worden vastgelegd

CapAnalysis biedt verschillende opties toovisualize uw pakketopname, elke verstrekken analyse vanuit een ander perspectief. U kunt met deze visual samenvattingen inzicht in uw netwerkverkeer trends en snel een ongewone activiteit te herkennen. Enkele van deze functies worden weergegeven in Hallo volgende lijst:

1. Stroom tabellen

    Deze tabel geeft u lijst met stromen in pakketgegevens Hallo Hallo, Hallo tijdstempel Hallo stromen gekoppeld en Hallo van verschillende protocollen die zijn gekoppeld aan het Hallo-stroom, evenals de IP-bron- en doelserver.

    ![capanalysis stroom pagina][5]

1. Overzicht van Protocol

    Dit deelvenster kunt u tooquickly Zie Hallo distributie van netwerkverkeer via Hallo verschillende protocollen en -locaties.

    ![overzicht van capanalysis protocol][6]

1. statistieken

    Dit deelvenster kunt u tooview netwerkverkeer statistics – bytes verzonden en ontvangen van de bron en doel-IP-adressen, stromen voor elk van de Hallo bron en doel-IP-adressen,-protocol gebruikt voor verschillende stromen en Hallo duur van stromen.

    ![capanalysis statistieken][7]

1. geomap

    Dit deelvenster biedt u een overzichtsweergave van het netwerkverkeer met kleuren toohello hoeveelheid verkeer vanuit elk land schalen. U kunt gemarkeerde landen tooview extra stroom statistieken zoals Hallo deel van de gegevens worden verzonden en ontvangen van IP-adressen in dat land selecteren.

    ![geomap][8]

1. Filters

    CapAnalysis biedt een set met filters voor snelle analyse van specifieke pakketten. U kunt bijvoorbeeld toofilter Hallo gegevens door protocol toogain specifieke insights op deze subset van verkeer.

    ![filters][11]

    Ga naar [https://www.capanalysis.net/ca/#about](https://www.capanalysis.net/ca/#about) toolearn meer over de mogelijkheden van alle CapAnalysis.

## <a name="conclusion"></a>Conclusie

Netwerk-Watcher pakket vastleggen functie kunt u toocapture Hallo gegevens nodig tooperform netwerk forensische en het netwerkverkeer beter te begrijpen. In dit scenario wordt beschreven hoe pakket schermopnamen van netwerk-Watcher eenvoudig worden geïntegreerd met open-source hulpprogramma's. U kunt met open-source hulpprogramma's zoals CapAnalysis toovisualize pakketten worden vastgelegd, grondige pakketinspecties uitvoeren en snel trends te identificeren binnen het netwerkverkeer.

## <a name="next-steps"></a>Volgende stappen

toolearn meer informatie over het NSG-logboeken stroom, gaat u naar [stroom NSG-Logboeken](network-watcher-nsg-flow-logging-overview.md)

Meer informatie over hoe toovisualize uw NSG-flow registreert met Power BI in via [visualiseren NSG loopt logboeken met Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)
<!--Image references-->

[1]: ./media/network-watcher-using-open-source-tools/figure1.png
[2]: ./media/network-watcher-using-open-source-tools/figure2.png
[3]: ./media/network-watcher-using-open-source-tools/figure3.png
[4]: ./media/network-watcher-using-open-source-tools/figure4.png
[5]: ./media/network-watcher-using-open-source-tools/figure5.png
[6]: ./media/network-watcher-using-open-source-tools/figure6.png
[7]: ./media/network-watcher-using-open-source-tools/figure7.png
[8]: ./media/network-watcher-using-open-source-tools/figure8.png
[9]: ./media/network-watcher-using-open-source-tools/figure9.png
[10]: ./media/network-watcher-using-open-source-tools/figure10.png
[11]: ./media/network-watcher-using-open-source-tools/figure11.png

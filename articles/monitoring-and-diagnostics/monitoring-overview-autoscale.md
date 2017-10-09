---
title: aaaOverview van automatisch schalen in Microsoft Azure Virtual Machines en Cloud Services-Web-Apps | Microsoft Docs
description: Overzicht van automatisch schalen in Microsoft Azure. Geldt tooVirtual Machines, Cloud Services en Web-Apps.
author: rboucher
manager: carmonm
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 74bf03be-e658-4239-a214-c12424b53e4c
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/02/2016
ms.author: robb
ms.openlocfilehash: ef68b722ea22c4149a7d7a89c5855ba761db9247
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-autoscale-in-microsoft-azure-virtual-machines-cloud-services-and-web-apps"></a>Overzicht van automatisch schalen in Microsoft Azure Virtual Machines en Cloud Services-Web-Apps
Dit artikel wordt beschreven welke Microsoft Azure-automatisch schalen is, de voordelen en hoe het gebruik van tooget wordt gestart.  

Monitor voor automatisch schalen die Azure geldt alleen te[virtuele-Machineschaalsets](https://azure.microsoft.com/services/virtual-machine-scale-sets/), [Cloudservices](https://azure.microsoft.com/services/cloud-services/), en [App Service - Web-Apps](https://azure.microsoft.com/services/app-service/web/).

> [!NOTE]
> Azure heeft twee methoden voor automatisch schalen. Een oudere versie van automatisch schalen is van toepassing tooVirtual Machines (beschikbaarheidssets). Deze functie is beperkte ondersteuning en het is raadzaam migreren toovirtual machineschaalsets voor ondersteuning voor automatisch schalen die sneller en betrouwbaarder. Een koppeling op hoe toouse Hallo oudere technologie is opgenomen in dit artikel.  
>
>

## <a name="what-is-autoscale"></a>Wat is automatisch schalen?
Automatisch schalen kunt u toohave Hallo juiste hoeveelheid resources toohandle Hallo load uitgevoerd op uw toepassing. Hiermee kunt u resources tooadd toohandle toename in laden en ook geld besparen door het verwijderen van de resources die niet-actieve zit. U geeft een minimum en maximum aantal exemplaren toorun en toevoegen of verwijderen van virtuele machines automatisch op basis van een reeks regels. Met een minimale zorgt ervoor dat uw toepassing wordt altijd uitgevoerd zelfs geen load. Met een beperkt mogelijk van uw totale per uur kosten. U wordt automatisch schalen tussen deze twee uiterste met regels die u maakt.

 ![Automatisch schalen, worden beschreven. Toevoegen en verwijderen van virtuele machines](./media/monitoring-overview-autoscale/AutoscaleConcept.png)

Wanneer de regelvoorwaarden wordt voldaan, worden een of meer acties voor automatisch schalen geactiveerd. U kunt toevoegen en verwijderen van virtuele machines of andere acties worden uitgevoerd. Hallo ziet volgende conceptueel diagram u dit proces.  

 ![Stroomdiagram voor automatisch schalen](./media/monitoring-overview-autoscale/Autoscale_Overview_v4.png)

Hallo geldt volgende uitleg toohello stukjes Hallo vorige diagram.   

## <a name="resource-metrics"></a>Metrische gegevens voor resources
Resources metrische gegevens verzenden, worden deze metrische gegevens later door regels worden verwerkt. Metrische gegevens worden geleverd via andere methoden.
Virtuele-machineschaalsets gebruik telemetriegegevens van Azure diagnostics agents dat telemetrie voor cloudservices en Web-apps vandaan rechtstreeks hello Azure-infrastructuur. Een aantal veelgebruikte statistieken omvatten CPU-gebruik, geheugengebruik, aantallen threads, wachtrijlengte en schijfgebruik. Zie voor een overzicht van wat u kunt telemetriegegevens [algemene metrische gegevens voor automatisch schalen](insights-autoscale-common-metrics.md).

## <a name="custom-metrics"></a>Aangepaste metrische gegevens
U kunt ook gebruikmaken van uw eigen aangepaste metrische gegevens die uw toepassingen kunnen verzenden. Als u uw toepassing(en) toosend metrische gegevens tooApplication Insights kunt u gebruikmaken van deze metrische gegevens toomake besluiten op of u hebt geconfigureerd tooscale of niet. 

## <a name="time"></a>Time
Planning gebaseerde regels zijn gebaseerd op UTC. Bij het instellen van uw regels, moet u uw eigen tijdzone correct ingesteld.  

## <a name="rules"></a>Regels
Hallo diagram ziet u slechts één regel voor automatisch schalen, maar u kunt veel van deze hebben. U kunt complexe overlappende regels maken die nodig zijn voor uw situatie.  Regeltypen opnemen  

* **Op basis van een metriek** -met deze actie bijvoorbeeld doen wanneer het CPU-gebruik hoger is dan 50%.
* **Op basis van tijd** - bijvoorbeeld trigger een webhook elke 8 uur op zaterdag in een bepaalde tijdzone.

Metriek gebaseerde regels toepassing werklast meten en toevoegen of verwijderen van virtuele machines op basis van de taak. Regels op basis van een planning kunt u tooscale, wanneer u tijdnotatie weergeven in uw laden en wilt tooscale voordat u een verhoging van het mogelijke load of verminderen.  

## <a name="actions-and-automation"></a>Acties en automatisering
Regels kunnen een of meer typen acties activeren.

* **Schaal** -Scale VM's in- of uitzoomen
* **E-mailadres** -verzenden van e-mailadres toosubscription beheerders, co-beheerders en/of extra e-mailadres die u opgeeft
* **Automatiseren via webhooks** -aanroepen van webhooks, waarmee meerdere complexe acties binnen of buiten Azure kan worden geactiveerd. In Azure, kunt u een Azure Automation-runbook, Azure-functie of Azure Logic App kunt starten. Voorbeeld van derden URL buiten Azure services zoals Slack en Twilio bevatten.

## <a name="autoscale-settings"></a>Instellingen voor automatisch schalen
Automatisch schalen gebruikt Hallo volgende terminologie en de structuur.

- Een **instelling voor automatisch schalen** kan worden gelezen door Hallo automatisch schalen engine toodetermine of tooscale omhoog of omlaag. Het bevat een of meer profielen, informatie over de doelbron Hallo en instellingen voor meldingen.

    - Een **automatisch schalen profiel** is een combinatie van a:

        - **instelling van de capaciteit**, wat aangeeft dat de minimum, maximum Hallo en standaardwaarden voor het aantal exemplaren.
        - **reeks regels**, die elk een trigger (tijd of metrisch) en een schaalactie (omhoog of omlaag) bevat.
        - **terugkeerpatroon**, waarmee wordt aangegeven wanneer automatisch schalen moet dit profiel tot stand is gebracht.

        U kunt meerdere profielen, waarmee u tootake antwoord verschillende overlappende vereisten hebben. U kunt bijvoorbeeld verschillende profielen voor verschillende tijdstippen van de dag of dagen van week hello, hebben.

    - Een **instelling** wordt gedefinieerd welke meldingen moeten plaatsvinden wanneer een gebeurtenis voor automatisch schalen op basis van die voldoet aan de criteria Hallo van een van de profielen Hallo automatisch schalen van de instelling plaatsvindt. Automatisch schalen kan melding van een of meer e-mailadressen of aanroepen tooone of meer webhooks maken.


![Instelling voor Azure automatisch schalen, profiel en regelstructuur](./media/monitoring-overview-autoscale/AzureResourceManagerRuleStructure3.png)

Hallo volledige lijst met configureerbare velden en beschrijvingen is beschikbaar in Hallo [REST-API voor automatisch schalen](https://msdn.microsoft.com/library/dn931928.aspx).

Zie voor codevoorbeelden van

* [Geavanceerde automatisch schalen configuratie met Resource Manager-sjablonen voor VM-Schaalsets](insights-advanced-autoscale-virtual-machine-scale-sets.md)  
* [REST-API voor automatisch schalen](https://msdn.microsoft.com/library/dn931953.aspx)

## <a name="horizontal-vs-vertical-scaling"></a>Horizontale tegenover verticaal schalen
Automatisch schalen alleen schaalt horizontaal, die een stijging ('uit') of te verlagen ('in') in Hallo aantal VM-exemplaren.  Horizontale biedt meer flexibiliteit in een situatie met een cloud omdat deze opdracht u toorun mogelijk duizenden virtuele machines toohandle belast kunt.

Daarentegen verschilt verticaal schalen. Dit houdt Hallo hetzelfde aantal virtuele machines, maar zorgt ervoor dat virtuele machines ('actief') meer of minder ('omlaag') krachtige Hallo. Power wordt gemeten in het geheugen, CPU-snelheid, schijfruimte, enz.  Verticale schaling heeft meer beperkingen. Dit is afhankelijk van de beschikbaarheid Hallo van grotere hardware, waarbij snel een bovenlimiet treffers en kan verschillen per regio. Verticale schalen normaal gesproken ook een VM-toostop vereist en opnieuw opstarten.

Zie voor meer informatie [verticaal schalen Azure virtuele machine met Azure Automation](../virtual-machines/linux/vertical-scaling-automation.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="methods-of-access"></a>Toegangsmethoden
U kunt via voor automatisch schalen instellen

* [Azure Portal](insights-how-to-scale.md)
* [PowerShell](insights-powershell-samples.md#create-and-manage-autoscale-settings)
* [Platformoverschrijdende opdrachtregelinterface (CLI)](insights-cli-samples.md#autoscale)
* [Monitor voor Azure REST-API](https://msdn.microsoft.com/library/azure/dn931953.aspx)

## <a name="supported-services-for-autoscale"></a>Ondersteunde services voor automatisch schalen
| Service | Schema & Docs |
| --- | --- |
| Web Apps |[Schalen van Web-Apps](insights-how-to-scale.md) |
| Cloudservices |[Een Cloudservice voor automatisch schalen](../cloud-services/cloud-services-how-to-scale.md) |
| Virtuele Machines: klassieke |[Beschikbaarheidssets voor vergroten/verkleinen klassieke virtuele Machine](https://blogs.msdn.microsoft.com/kaevans/2015/02/20/autoscaling-azurevirtual-machines/) |
| Virtuele Machines: Windows-Schaalsets |[Virtuele-machineschaalset schalen wordt ingesteld in Windows](../virtual-machine-scale-sets/virtual-machine-scale-sets-windows-autoscale.md) |
| Virtuele Machines: Linux Scale ingesteld |[Virtuele-machineschaalset schalen stelt in Linux](../virtual-machine-scale-sets/virtual-machine-scale-sets-linux-autoscale.md) |
| Virtuele Machines: Voorbeeld van de Windows |[Geavanceerde automatisch schalen configuratie met Resource Manager-sjablonen voor VM-Schaalsets](insights-advanced-autoscale-virtual-machine-scale-sets.md) |

## <a name="next-steps"></a>Volgende stappen
toolearn meer informatie over automatisch schalen, Hallo Autoscale Walkthroughs eerder vermelde Raadpleeg of toohello resources te volgen:

* [Azure Monitor voor automatisch schalen die de algemene metrische gegevens](insights-autoscale-common-metrics.md)
* [Aanbevolen procedures voor het Azure-Monitor voor automatisch schalen](insights-autoscale-best-practices.md)
* [Automatisch schalen acties toosend e-mail en -webhook waarschuwingsmeldingen gebruiken](insights-autoscale-to-webhook-email.md)
* [REST-API voor automatisch schalen](https://msdn.microsoft.com/library/dn931953.aspx)
* [Het oplossen van problemen virtuele Machine Scale Sets-automatisch schalen](../virtual-machine-scale-sets/virtual-machine-scale-sets-troubleshoot.md)

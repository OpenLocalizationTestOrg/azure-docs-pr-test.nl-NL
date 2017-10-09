---
title: aaaTroubleshoot automatisch geschaald met virtuele-Machineschaalsets | Microsoft Docs
description: Problemen oplossen met virtuele-Machineschaalsets voor automatisch schalen. Typische problemen aangetroffen begrijpen en hoe tooresolve ze.
services: virtual-machine-scale-sets
documentationcenter: 
author: gbowerman
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: c7d87b72-ee24-4e52-9377-a42f337f76fa
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: windows
ms.devlang: na
ms.topic: article
ms.date: 10/28/2016
ms.author: guybo
ms.openlocfilehash: 4c9a70992348d87fb43646421a90a027bf400a17
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-autoscale-with-virtual-machine-scale-sets"></a>Het oplossen van problemen met virtuele-Machineschaalsets voor automatisch schalen
**Probleem** : u hebt gemaakt een infrastructuur voor automatisch schalen in Azure Resource Manager met behulp van de VM-Schaalsets – bijvoorbeeld door het implementeren van een sjabloon als volgt: https://github.com/Azure/azure-quickstart-templates/tree/master/201- vmss-bottle-automatisch schalen: u hebt uw scale-regels gedefinieerd en werkt geweldig, behalve dat ongeacht hoeveel belasting u van Hallo virtuele machines, het automatisch schalen won't.

## <a name="troubleshooting-steps"></a>Stappen voor probleemoplossing
Sommige tooconsider dingen omvatten:

* Het aantal kernen heeft elke virtuele machine en laadt u elke core? Hello Azure Quickstart voorbeeldsjabloon bovenstaande heeft een script do_work.php, die één kern wordt geladen. Als u een virtuele machine die groter is dan één kern VM-grootte zoals Standard_A1 of D1 en u toorun deze laadbewerking meerdere keren moet. Controleren hoeveel cores uw virtuele machines aan de hand van [grootten voor Windows virtuele machines in Azure](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* Hoeveel virtuele machines in VM-Schaalset, Hallo gaat het werk voor elk criterium?
  
    Een scale-out-gebeurtenis wordt alleen plaatsvinden als Hallo gemiddelde CPU-via **alle** Hallo virtuele machines in een set scale Hallo drempelwaarde, gedurende een periode van Hallo interne gedefinieerd in de regels voor automatisch schalen Hallo overschrijdt.
* Hebt u geen gebeurtenissen scale hoofd gezien?
  
    Controleer de auditlogboeken Hallo in hello Azure-portal voor scale-gebeurtenissen. Misschien er is een schaal en een schaal omlaag dat is overgeslagen. U kunt filteren op 'Schaal'...
  
    ![Controlelogboeken][audit]
* De schaal in en scale-out drempelwaarden voldoende verschillend zijn?
  
    Stel dat u een regel tooscale uit wanneer gemiddelde CPU is groter dan 50% meer dan 5 minuten en tooscale instellen in wanneer gemiddelde CPU minder dan 50 is %. Hierdoor zou een probleem 'flapping' wanneer het CPU-gebruik is sluiten toothis drempelwaarde, met de schaalacties voortdurend vergroten of verkleinen Hallo grootte van Hallo is ingesteld. Als gevolg hiervan probeert Hallo automatisch schalen service tooprevent 'op en neer', die licht kunnen als niet schalen. Controleer daarom dat de drempelwaarden voor scale-out en de schaal zijn voldoende verschillende tooallow vrij Between schalen ruimte.
* U uw eigen JSON-sjabloon schrijft?
  
    Is eenvoudig toomake fouten, dus beginnen met een sjabloon zoals Hallo is een waarboven toowork bewezen en klein incrementele wijzigingen aanbrengen. 
* Kunt u handmatig schalen in- of?
  
    Probeer het opnieuw distribueren Hallo VM-Schaalset resource met een andere 'capaciteit' instelling toochange Hallo aantal virtuele machines handmatig. Een voorbeeld van de sjabloon toodo dit hier is: https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-scale-existing – mogelijk moet u tooedit Hallo sjabloon toomake ervoor deze Hallo heeft dezelfde machine grootte als uw Schaalset wordt gebruikt. Als u het aantal virtuele machines Hallo is handmatig wijzigen kunt, weet u Hallo probleem is geïsoleerd tooautoscale.
* Controleer uw Microsoft.Compute/virtualMachineScaleSet en Microsoft.Insights resources Hallo [Azure Resource Explorer](https://resources.azure.com/)
  
    Dit is een beslist hulpprogramma waarin u kunt zien voor probleemoplossing Hallo van uw Azure Resource Manager-resources. Klik op uw abonnement en bekijkt hello resourcegroep die u wilt oplossen. Bij de Hallo Compute resourceprovider bekijkt hello VM-Schaalset u hebt gemaakt en controleer Hallo Instantieweergave waarin de status van een implementatie Hallo. Instantieweergave van virtuele machines in VM-Schaalset Hallo Hallo ook controleren. Vervolgens gaat u naar Hallo Microsoft.Insights resourceprovider en controleer Hallo automatisch schalen regels goed.
* Is Hallo diagnostische extensie werkt en prestatiegegevens verzenden?
  
    **Update:** Azure automatisch schalen is verbeterde toouse pijplijn van metrische gegevens die niet langer een diagnostics extensie toobe geïnstalleerd vereist op basis van een host. Dit betekent dat Hallo komende leden niet langer van toepassing als u een toepassing automatisch schalen op basis van de nieuwe pijplijn Hallo maakt. Een voorbeeld van Azure-sjablonen die geconverteerd toouse Hallo host pijplijn zijn is: https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-bottle-autoscale. 
  
    Met behulp van de host op basis van metrische gegevens voor automatisch schalen is beter geschikt voor Hallo volgende redenen:
  
  * Minder bewegende onderdelen als er worden geen extensies diagnostics moeten toobe geïnstalleerd.
  * Eenvoudiger sjablonen. Alleen toe te voegen insights automatisch schalen regels tooan bestaande schaalset sjabloon.
  * Betrouwbaarder rapportage en snellere starten van de nieuwe virtuele machines.
    
    Hallo zou alleen redenen dat kunt u met behulp van een extensie voor diagnostische tookeep zijn als u geheugen diagnostics reporting/schalen moet. Host op basis van metrische gegevens rapporteren niet geheugen.
    
    Met daarom alleen volgen Hallo rest van dit artikel als u nog steeds diagnostische uitbreidingen voor uw automatisch schalen.
    
    Automatisch schalen in Azure Resource Manager kunt werken (maar niet meer heeft tot) met behulp van een VM-extensie aangeroepen Hallo extensie voor diagnostische gegevens. Hiermee plaatst u de prestaties gegevens tooa opslagaccount die u in de sjabloon Hallo definiëren. Deze gegevens wordt vervolgens door hello Azure Monitor-service geaggregeerd.
    
    Als Hallo Insights-service kan geen gegevens uit Hallo virtuele machines lezen, het toosend moet u een e-mailbericht: bijvoorbeeld als Hallo VM's zijn, Controleer dus uw e-mailadres (hello een hebt opgegeven toen u hello Azure-account).
    
    U kunt ook gaan en bekijkt hello gegevens zelf. Bekijkt hello Azure storage-account met behulp van een cloud explorer. Bijvoorbeeld met behulp van Hallo [Visual Studio Cloud Explorer](https://visualstudiogallery.msdn.microsoft.com/aaef6e67-4d99-40bc-aacf-662237db85a2), aanmelden en hello Azure-abonnement u kiest en Hallo naam waarnaar wordt verwezen in Hallo uitbreidingsdefinitie diagnostische gegevens in uw implementatie opslagaccount voor diagnostische gegevens sjabloon...
    
    ![Cloud Explorer][explorer]
    
    Hier ziet u een aantal tabellen waarbij Hallo gegevens van elke virtuele machine worden opgeslagen. Linux- en Hallo CPU metriek als voorbeeld duurt, de meest recente rijen Hallo bekijken. Hallo Visual Studio cloud explorer biedt ondersteuning voor een querytaal zodat u kunt een query zoals uitvoeren ' tijdstempel gt datetime'2016-02-02T21:20:00Z' ' toomake zeker dat u de meest recente gebeurtenissen hello (uitgaan van tijd in UTC). Schaalt Hallo-gegevens die u ziet in er overeenkomen toohello regels die u instelt? Hallo onderstaand voorbeeld Hallo CPU voor machine 20 gestart too100% verhogen via Hallo laatste vijf minuten...
    
    ![Storage-tabellen][tables]
    
    Als er geen Hallo gegevens aanwezig is, vervolgens wordt verwezen naar Hallo probleem is met diagnostische Hallo-extensie uitgevoerd in de Hallo virtuele machines. Als Hallo gegevens aanwezig is, betekent dit dat er is een probleem met uw scale-regels of met Hallo Insights-service. Controleer [Azure Status](https://azure.microsoft.com/status/).
    
    Zodra u via deze stappen zijn hebt als u steeds problemen automatisch schalen die nog u kan probeert Hallo forums [MSDN](https://social.msdn.microsoft.com/forums/azure/home?category=windowsazureplatform%2Cazuremarketplace%2Cwindowsazureplatformctp), of [Stack-overloop](http://stackoverflow.com/questions/tagged/azure), of in te loggen van een aanroep van ondersteuning. Worden voorbereid tooshare Hallo sjabloon en een weergave van Hallo prestatiegegevens.

[audit]: ./media/virtual-machine-scale-sets-troubleshoot/image3.png
[explorer]: ./media/virtual-machine-scale-sets-troubleshoot/image1.png
[tables]: ./media/virtual-machine-scale-sets-troubleshoot/image4.png

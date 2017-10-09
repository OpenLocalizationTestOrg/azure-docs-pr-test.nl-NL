---
title: aaaAzure virtuele-machineschaalsets overzicht | Microsoft Docs
description: Meer informatie over virtuele-machineschaalsets in Azure
services: virtual-machine-scale-sets
documentationcenter: 
author: gbowerman
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 76ac7fd7-2e05-4762-88ca-3b499e87906e
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/03/2017
ms.author: guybo
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 788b2d1636e0bf4ef3fbf94aed9b3303c5fafa82
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="what-are-virtual-machine-scale-sets-in-azure"></a>Wat zijn virtuele-machineschaalsets in Azure?
Virtuele-machineschaalsets zijn een Azure compute-resource toodeploy gebruiken en beheren van een set van identieke virtuele machines. Met alle virtuele machines die zijn geconfigureerd dezelfde hello, schaalsets zijn ontworpen toosupport true automatisch schalen en geen vooraf inrichten van virtuele machines is vereist. Het is daarom eenvoudiger toobuild grootschalige services die zijn gericht op big compute, big data en beperkte workloads.

Voor toepassingen die tooscale rekenresources uit- en scale moeten worden operations impliciet gelijkmatig over probleem- en -domeinen. Voor een verdere inleiding tooscale wordt ingesteld, Raadpleeg toohello [Azure blog aankondiging](https://azure.microsoft.com/blog/azure-virtual-machine-scale-sets-ga/).

Bekijk voor meer informatie over schaalsets deze video's:

* [Mark Russinovich vertelt over Azure-schaalsets](https://channel9.msdn.com/Blogs/Regular-IT-Guy/Mark-Russinovich-Talks-Azure-Scale-Sets/)  
* [Guy Bowerman over virtuele-machineschaalsets](https://channel9.msdn.com/Shows/Cloud+Cover/Episode-191-Virtual-Machine-Scale-Sets-with-Guy-Bowerman)

## <a name="creating-and-managing-scale-sets"></a>Schaalsets maken en beheren
Kunt u een schaal instellen in Hallo [Azure-portal](https://portal.azure.com) door te selecteren **nieuwe** en typen **scale** op Hallo zoekbalk. **Virtuele-machineschaalset** wordt weergegeven in het Hallo-resultaten. U kunt daar Hallo vereist velden toocustomize invullen en implementeren van uw scale set. Hebt u ook opties tooset basic automatisch schalen regels op basis van CPU-gebruik in Hallo-portal.

U kunt schaalsets definiëren en implementeren met behulp van JSON-sjablonen en [REST API's](https://msdn.microsoft.com/library/mt589023.aspx), net als individuele virtuele machines in Azure Resource Manager. U kunt daarom alle standaardimplementatiemethoden van Azure Resource Manager gebruiken. Zie [Azure Resource Manager-sjablonen samenstellen](../azure-resource-manager/resource-group-authoring-templates.md) voor meer informatie over sjablonen.

U vindt een reeks voorbeeld sjablonen voor virtuele-machineschaalset wordt ingesteld in Hallo [Azure Quickstart-sjablonen GitHub-opslagplaats](https://github.com/Azure/azure-quickstart-templates). (Zoek naar de sjablonen met **vmss** in Hallo titel.)

Voor voorbeelden van Hallo Quick Start-sjabloon, een knop 'tooAzure implementeren' in hello Leesmij-bestand voor elk onderdeel sjabloon koppelingen toohello portal-implementatie. toodeploy hello schaal instellen, klikt u op Hallo en vul vervolgens de parameters die in het Hallo-portal vereist zijn. 

## <a name="scaling-a-scale-set-out-and-in"></a>Een schaalset in- en uitschalen
U kunt wijzigen Hallo-capaciteit van een schaal instellen in hello Azure-portal door te klikken op Hallo **schaal** onder sectie **instellingen**. 

toochange schaalset op Hallo-opdrachtregel, gebruikt u Hallo **scale** opdracht in [Azure CLI](https://github.com/Azure/azure-cli). Gebruik bijvoorbeeld deze opdracht tooset een scale set tooa capaciteit van 10 virtuele machines:

```bash
az vmss scale -g resourcegroupname -n scalesetname --new-capacity 10 
```

tooset hello aantal VM's in een schaal instellen met behulp van PowerShell, gebruikt u Hallo **Update AzureRmVmss** opdracht:

```PowerShell
$vmss = Get-AzureRmVmss -ResourceGroupName resourcegroupname -VMScaleSetName scalesetname  
$vmss.Sku.Capacity = 10
Update-AzureRmVmss -ResourceGroupName resourcegroupname -Name scalesetname -VirtualMachineScaleSet $vmss
```

tooincrease of afname Hallo aantal virtuele machines in een schaal instellen met behulp van een Azure Resource Manager-sjabloon, Hallo wijzigen **capaciteit** eigenschap en de implementatie opnieuw Hallo-sjabloon. Deze eenvoud maakt het eenvoudig toointegrate-schaalsets met Azure automatisch schalen of uw eigen aangepaste vergroten/verkleinen laag als u toodefine aangepaste schaal gebeurtenissen voor automatisch schalen die Azure moet biedt geen ondersteuning voor toowrite. 

Als u opnieuw van een Azure Resource Manager sjabloon toochange Hallo capaciteit distribueren, kunt u een veel kleinere sjabloon waarin alleen Hallo definiëren **SKU** eigenschap pakket Hello capaciteit bijgewerkt. [Hier volgt een voorbeeld](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-scale-existing).

## <a name="autoscale"></a>Automatisch schalen

Een schaalset kan eventueel worden geconfigureerd met instellingen voor automatisch schalen wanneer deze wordt gemaakt in hello Azure-portal. het aantal virtuele machines Hallo kan vervolgens worden verhoogd of verlaagd op basis van het gemiddelde CPU-gebruik. 

Veel van Hallo set sjablonen schalen in Hallo [Azure-snelstartsjablonen](https://github.com/Azure/azure-quickstart-templates) definieert u de instellingen voor automatisch schalen. U kunt ook automatisch schalen instellingen tooan bestaande scale set toevoegen. Dit Azure PowerShell-script wordt bijvoorbeeld automatisch schalen op basis van CPU tooa scale set toegevoegd:

```PowerShell

$subid = "yoursubscriptionid"
$rgname = "yourresourcegroup"
$vmssname = "yourscalesetname"
$location = "yourlocation" # e.g. southcentralus

$rule1 = New-AzureRmAutoscaleRule -MetricName "Percentage CPU" -MetricResourceId /subscriptions/$subid/resourceGroups/$rgname/providers/Microsoft.Compute/virtualMachineScaleSets/$vmssname -Operator GreaterThan -MetricStatistic Average -Threshold 60 -TimeGrain 00:01:00 -TimeWindow 00:05:00 -ScaleActionCooldown 00:05:00 -ScaleActionDirection Increase -ScaleActionValue 1
$rule2 = New-AzureRmAutoscaleRule -MetricName "Percentage CPU" -MetricResourceId /subscriptions/$subid/resourceGroups/$rgname/providers/Microsoft.Compute/virtualMachineScaleSets/$vmssname -Operator LessThan -MetricStatistic Average -Threshold 30 -TimeGrain 00:01:00 -TimeWindow 00:05:00 -ScaleActionCooldown 00:05:00 -ScaleActionDirection Decrease -ScaleActionValue 1
$profile1 = New-AzureRmAutoscaleProfile -DefaultCapacity 2 -MaximumCapacity 10 -MinimumCapacity 2 -Rules $rule1,$rule2 -Name "autoprofile1"
Add-AzureRmAutoscaleSetting -Location $location -Name "autosetting1" -ResourceGroup $rgname -TargetResourceId /subscriptions/$subid/resourceGroups/$rgname/providers/Microsoft.Compute/virtualMachineScaleSets/$vmssname -AutoscaleProfiles $profile1
```

U vindt een lijst met geldige metrische gegevens tooscale op [ondersteund met een Azure-Monitor](../monitoring-and-diagnostics/monitoring-supported-metrics.md) onder de kop 'Microsoft.Compute/virtualMachineScaleSets.' Hallo Meer geavanceerde opties voor automatisch schalen zijn ook beschikbaar is, met inbegrip van automatisch schalen op basis van een planning en het gebruik van webhooks toointegrate met waarschuwing systemen.

## <a name="monitoring-your-scale-set"></a>Uw schaalset controleren
Hallo [Azure-portal](https://portal.azure.com) lijsten schaal ingesteld en hun eigenschappen bevat. Hallo-portal biedt ook ondersteuning voor beheertaken uit te voeren. U kunt beheerbewerkingen zowel op schaalsets uitvoeren als op afzonderlijke VM's binnen een schaalset. Hallo-portal biedt ook een gebruiksgrafiek aanpasbare resource. 

Als u toosee moet of JSON-definitie van een Azure-resource onderliggende hello bewerkt, kunt u ook gebruiken [Azure Resource Explorer](https://resources.azure.com). Schaalsets zijn een resource onder hello Microsoft.Compute Azure-resourceprovider. Vanuit deze site, kunt u ze zien door het uitbreiden van Hallo koppelingen te volgen:

**Abonnementen** > **uw abonnement** > **resourceGroups** > **providers** > **Microsoft.Compute** > **virtualMachineScaleSets** > **uw schaalset** > enzovoort.

## <a name="scale-set-scenarios"></a>Scenario's voor schaalsets
In dit gedeelte wordt een aantal typische scenario's voor schaalsets genoemd. Deze scenario's worden toegepast voor een aantal van de hogere Azure-services, zoals Batch, Service Fabric en Container Service.

* **Gebruik RDP of SSH tooconnect tooscale Stel exemplaren**: een scale set wordt gemaakt binnen een virtueel netwerk en openbare IP-adressen niet standaard afzonderlijke virtuele machines in de schaalset Hallo zijn toegewezen. Dit beleid voorkomt Hallo onkosten en beheer de overhead van afzonderlijke openbare IP-adres toewijzen adressen tooall Hallo knooppunten in het raster compute. Als u direct externe verbindingen tooscale VMs ingesteld moet, kunt u een scale set tooautomatically toewijzen openbare IP-adressen toonew virtuele machines kunt configureren. U kunt ook tooVMs verbinden van andere bronnen in uw virtuele netwerk dat wordt toegewezen openbare IP-adressen, bijvoorbeeld zelfstandige virtuele machines en netwerktaakverdelers. 
* **TooVMs verbinding met behulp van NAT-regels**: een openbaar IP-adres maken, wijs het tooa load balancer toe en definiëren van een binnenkomende NAT-pool. Deze acties worden toegewezen poorten op Hallo IP-adres tooa poort op een virtuele machine in de schaalset Hallo. Bijvoorbeeld:
  
  | Bron | Bronpoort | Doel | Doelpoort |
  | --- | --- | --- | --- |
  |  Openbare IP |Poort 50000 |vmss\_0 |Poort 22 |
  |  Openbare IP |Poort 50001 |vmss\_1 |Poort 22 |
  |  Openbare IP |Poort 50002 |vmss\_2 |Poort 22 |
  
   In [in dit voorbeeld](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-linux-nat), NAT-regels zijn gedefinieerde tooenable een SSH-verbinding tooevery VM in een schaalset, met behulp van een enkele openbare IP-adres.
  
   [In dit voorbeeld](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-windows-nat) dezelfde met RDP en Windows hello.
* **TooVMs verbinding via een 'jumpbox'**: als u een scale-set en een zelfstandige VM in hetzelfde virtuele netwerk maken, Hallo Hallo zelfstandige virtuele machine en Hallo scale set VM verbinding maken met een andere met behulp van hun interne IP-adressen, tooone zoals gedefinieerd door Hallo virtuele netwerk of subnet. Als u een openbaar IP-adres maken en deze toohello zelfstandige VM toewijzen, kunt u RDP of SSH tooconnect toohello zelfstandige VM. U kunt vervolgens met de verbinden van dat tooyour exemplaren machineschaalset. Het valt u misschien op dat een eenvoudige schaalset inherent veiliger is dan een eenvoudige zelfstandige VM met een openbaar IP-adres in de standaardconfiguratie.
  
   [Deze sjabloon](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-linux-jumpbox) implementeert bijvoorbeeld een eenvoudige schaalset met een zelfstandige VM. 
* **Taakverdeling tooscale set exemplaren**: als u toodeliver werk tooa compute cluster van virtuele machines wilt met behulp van een benadering van round robin, kunt u een Azure load balancer dienovereenkomstig configureren met laag-4-taakverdeling regels. U kunt tests definiëren tooverify die uw toepassing wordt uitgevoerd door de ping-poorten met een opgegeven protocol, interval en Aanvraagpad. [Azure Application Gateway](https://azure.microsoft.com/services/application-gateway/) ondersteunt ook schaalsets, naast Layer-7 en complexere scenario's voor taakverdeling.
  
   [In dit voorbeeld](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-ubuntu-web-ssl) maakt u een scale-set die wordt uitgevoerd Apache-webservers en maakt gebruik van een load balancer toobalance Hallo belasting die elke VM ontvangt. (Bekijkt hello Microsoft.Network/loadBalancers brontype en Schaalaanpassingsset en extensionProfile in virtualMachineScaleSet.)

   In [dit Linux-voorbeeld](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-ubuntu-app-gateway) en [dit Windows-voorbeeld](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-windows-app-gateway) wordt de toepassingsgateway gebruikt.  

* **Een schaalset implementeren als een rekencluster in PaaS-clusterbeheer**: schaalsets worden soms omschreven als de werkrol van de volgende generatie. Hoewel een geldige beschrijving kan worden uitgevoerd Hallo risico verwarrend scale set functies met Azure Cloud Services-functies. In zekere zin bieden schaalsets een echte werkrol of worker-resource. Schaalsets zijn een gegeneraliseerde compute-resource die onafhankelijk is van platform/runtime, aanpasbaar is en kan worden geïntegreerd met Azure Resource Manager-IaaS.
  
   Een worker-rol in Cloud Services is beperkt met betrekking tot platform/runtime-ondersteuning (alleen installatiekopieën van Windows-platform). Maar deze omvat ook services zoals wisselen van VIP, configureerbare instellingen voor upgraden en specifieke instellingen voor runtime/app-implementatie. Deze services zijn *nog niet* beschikbaar voor schaalsets of ze worden geleverd met andere PaaS-services van een hoger niveau, zoals Azure Service Fabric. U kunt schaalsets zien als een infrastructuur die ondersteuning biedt voor PaaS. PaaS-oplossingen zoals [Service Fabric](https://azure.microsoft.com/services/service-fabric/) zijn gebaseerd op deze infrastructuur.
  
   In [dit voorbeeld](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-dcos) van deze benadering wordt met [Azure Container Service](https://azure.microsoft.com/services/container-service/) een cluster geïmplementeerd op basis van schaalsets met een container-orchestrator.

## <a name="scale-set-performance-and-scale-guidance"></a>Richtlijnen voor prestaties en schaal van schaalsets
* Een schaalset ondersteunt up too1, 000 virtuele machines. Als u maken en uploaden van uw eigen aangepaste VM-installatiekopieën, is het Hallo-limiet 100. Zie [Werken met grote schaalsets voor virtuele machines](virtual-machine-scale-sets-placement-groups.md) voor overwegingen bij het gebruik van grote virtuele-machineschaalsets.
* U hebt geen toopre-schaalsets van Azure storage-accounts toouse maken. Ondersteuning van de sets Scale Azure beheerd schijven die problemen met prestaties Hallo aantal schijven per storage-account dat. Zie voor meer informatie [Schaalsets en beheerde schijven voor virtuele Azure-machines](virtual-machine-scale-sets-managed-disks.md).
* Overweeg om Azure Premium-opslag te gebruiken in plaats van Azure-opslag voor snellere, beter te voorspellen VM-inrichting en verbeterde IO-prestaties.
* Hallo kerngeheugenquotum in Hallo regio waarin u implementeert beperkt Hallo aantal virtuele machines die u kunt maken. Mogelijk moet u toocontact Customer Support tooincrease uw quotumlimiet compute, zelfs als u een hoge limiet van kernen voor gebruik met Azure Cloud Services vandaag hebt. tooquery uw quotum, deze Azure CLI-opdracht uitvoeren: `azure vm list-usage`. Of voer deze PowerShell-opdracht uit: `Get-AzureRmVMUsage`.

## <a name="frequently-asked-questions-for-scale-sets"></a>Veelgestelde vragen over schaalsets
**V:** Hoeveel virtuele machines kan een schaalset bevatten?

**A:** Een scale-set kan 0 too1, 000 VM's op basis van installatiekopieën van het platform, of 0 too100 virtuele machines op basis van aangepaste installatiekopieën. 

**V:** Worden gegevensschijven binnen schaalsets ondersteund?

**A:** Ja. Een schaalset kunt definiëren een gegevensblok schijven configuratie die van toepassing tooall virtuele machines in Hallo set is. Zie [Schaalsets en gekoppelde gegevensschijven in Azure](virtual-machine-scale-sets-attached-disks.md) voor meer informatie. Andere opties voor het opslaan van gegevens zijn:

* Azure-bestanden (gedeelde SMB-stations)
* Station van het besturingssysteem
* Tijdelijk station (lokaal, niet ondersteund met Azure Storage)
* Azure-gegevensservice (bijvoorbeeld Azure-tabellen, Azure-blobs)
* Externe gegevensservice (bijvoorbeeld externe database)

**V:** Welke Azure-regio's ondersteunen schaalsets?

**A:** Alle regio's ondersteunen schaalsets.

**V:** Hoe maak ik een schaalset met behulp van een aangepaste installatiekopie?

**A:** Maak een beheerde schijf op basis van uw aangepaste installatiekopie-VHD en verwijs ernaar in de sjabloon van de schaalset. [Hier volgt een voorbeeld](https://github.com/chagarw/MDPP/tree/master/101-vmss-custom-os).

**V:** Als ik mijn schaalset van 20 too15, dat virtuele machines worden verwijderd?

**A:** Virtuele machines worden verwijderd van Hallo scale gelijkmatig instellen voor een update-domeinen en fout met betrekking tot domeinen toomaximize beschikbaarheid. Als u virtuele machines met Hallo die hoogste id's eerst worden verwijderd.

**V:** Wat gebeurt er als het Hallo-capaciteit van 15 too18 vervolgens vergroten?

**A:** Als u capaciteit too18 verhoogt, dan 3 nieuwe VM's gemaakt. Elke keer wordt Hallo VM exemplaar-ID verhoogd van Hallo vorige hoogste waarde (bijvoorbeeld 20, 21, 22). VM's worden verdeeld over foutdomeinen en updatedomeinen.

**V:** Kan ik een uitvoeringsvolgorde toepassen wanneer ik meerdere extensies in een schaalset gebruik?

**A:** Niet rechtstreeks, maar voor de extensie customScript hello, uw script kunt wachten op een andere extensie toofinish. U kunt extra hulp krijgen op extensie sequentiëren in Hallo blogbericht [extensie sequentiëren in Azure VM-Schaalsets](https://msftstack.wordpress.com/2016/05/12/extension-sequencing-in-azure-vm-scale-sets/).

**V:** Maken schaalsets gebruik van beschikbaarheidssets van Azure?

**A:** Ja. Een schaalset is een impliciete beschikbaarheidsset met vijf foutdomeinen en vijf updatedomeinen. Schaal sets van meer dan 100 virtuele machines span meerdere *plaatsing groepen*, die gelijkwaardig toomultiple beschikbaarheidssets zijn. Zie voor meer informatie over de plaatsing van groepen [Werken met grote schaalsets voor virtuele machines](virtual-machine-scale-sets-placement-groups.md). Een beschikbaarheidsset van virtuele machines kan bestaan in Hallo hetzelfde virtuele netwerk als een scale-set van virtuele machines. Een algemene configuratie is tooput beheerknooppunt VMs (die vaak vereisen unieke configuratie) in de beschikbaarheidsset instellen en gegevensknooppunten plaatsen in de schaalset Hallo.

U vindt meer antwoorden tooquestions over schalen wordt ingesteld in Hallo [Azure virtuele-machineschaalsets Veelgestelde vragen over](virtual-machine-scale-sets-faq.md).

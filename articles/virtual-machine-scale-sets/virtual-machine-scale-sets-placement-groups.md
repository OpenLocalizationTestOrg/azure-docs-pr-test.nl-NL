---
title: aaaWorking met grote Azure virtuele-Machineschaalsets | Microsoft Docs
description: Wat u moet tooknow toouse grote virtuele machine van Azure sets schalen
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
ms.date: 2/7/2017
ms.author: guybo
ms.openlocfilehash: a39aab25925d7fc50763f0a20148b1f2213b492f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="working-with-large-virtual-machine-scale-sets"></a>Werken met grote virtuele-machineschaalsets
U kunt nu Azure maken [virtuele-machineschaalsets](/azure/virtual-machine-scale-sets/) met een capaciteit van up too1, 000 virtuele machines. In dit document, een _grote virtuele-machineschaalset_ is gedefinieerd als een schaal ingesteld geschikt is voor het schalen van toogreater dan 100 virtuele machines. Deze mogelijkheid wordt ingesteld met een schaalseteigenschap (_singlePlacementGroup=False_). 

Bepaalde aspecten van grote schaal wordt ingesteld, zoals load balancing en fouttolerantie domeinen zich anders gedragen tooa standaardschaal set. Dit document wordt uitgelegd Hallo kenmerken van grote schaalsets en wordt beschreven wat u moet tooknow toosuccessfully ze gebruiken in uw toepassingen. 

Een gemeenschappelijke aanpak voor het implementeren van cloudinfrastructuur op grote schaal toocreate is een reeks _schaaleenheden_, bijvoorbeeld door het maken van meerdere virtuele machines sets schalen op meerdere VNETs en storage-accounts. Deze aanpak geeft u eenvoudiger beheer vergeleken toosingle VM's en meerdere schaaleenheden zijn handig voor veel toepassingen, met name de waarvoor andere stapelbare onderdelen, zoals meerdere virtuele netwerken en eindpunten. Als uw toepassing echter een grote cluster vereist, kan het eenvoudiger toodeploy één scale van too1, 000 VM's instellen zijn. Voorbeeldscenario's zijn gecentraliseerde big data-implementaties, of rekenrasters die een eenvoudig beheer van een grote groep werkrolknooppunten vereisen. In combinatie met VM-schaalaanpassingsset [gegevensschijven gekoppeld](virtual-machine-scale-sets-attached-disks.md), grote schaal stelt u in staat stellen toodeploy een schaalbare infrastructuur, die bestaan uit duizenden kernen en petabytes aan opslag, als een enkele bewerking.

## <a name="placement-groups"></a>Plaatsingsgroepen 
Wat maakt een _grote_ schaal instelt speciale is geen Hallo aantal virtuele machines, maar Hallo aantal _plaatsing groepen_ bevat. Een groep plaatsing is een constructie vergelijkbare tooan Azure beschikbaarheidsset, met een eigen domeinen met fouten en upgradedomeinen. Standaard bestaat een schaalset uit één plaatsingsgroep met een omvang van maximaal 100 virtuele machines. Als de eigenschap met de naam van een schaalset _singlePlacementGroup_ too_false_, is ingesteld Hallo scale set kunnen moet bestaan uit meerdere plaatsing groepen en heeft een bereik van 0-1000 virtuele machines. Als de standaardwaarde toohello van ingesteld _true_, een scale-set bestaat uit een groep één plaatsing en heeft een bereik van 0-100 virtuele machines.

## <a name="checklist-for-using-large-scale-sets"></a>Controlelijst voor het gebruik van grote schaalsets
toodecide of uw toepassing kunt aanbrengen effectief gebruik van grote schaalsets, kunt u overwegen Hallo volgens de vereisten:

- Grote schaalsets vereisen Azure Managed Disks. Voor schaalsets die niet worden gemaakt met Managed Disks zijn meerdere opslagaccounts vereist (één voor elke 20 virtuele machines). Grote schaalsets zijn ontworpen toowork uitsluitend met schijven beheerd tooreduce uw storage management overhead en tooavoid Hallo risico van het uitvoeren van abonnement is beperkt voor opslagaccounts. Als u geen beheerde schijven gebruikt, is uw schaalset beperkt too100 virtuele machines.
- Gemaakt op basis van installatiekopieën van Azure Marketplace-schaalsets kunnen opschalen van too1, 000 virtuele machines.
- Gemaakt op basis van aangepaste installatiekopieën (VM-installatiekopieën u maken en uploaden zelf)-schaalsets kunnen momenteel opschalen van too100 virtuele machines.
- Laag 4 taakverdeling met hello Azure Load Balancer is nog niet ondersteund voor schaalsets bestaat uit meerdere groepen voor plaatsing. Als u toouse hello Azure Load Balancer Zorg ervoor dat Hallo schaal instelt moet is een groep één plaatsing, wat de standaardinstelling Hallo is geconfigureerde toouse.
- Laag 7 taakverdeling met hello Azure Application Gateway wordt ondersteund voor alle-schaalsets.
- Een scale-set is gedefinieerd met één subnet: Zorg ervoor dat uw subnet is een adresruimte die groot genoeg zijn voor alle Hallo VM die u nodig hebt. Standaard een schaal overprovisions ingesteld (leidt tot extra virtuele machines tijdens de implementatie of het uitbreiden, die u niet weet in rekening gebracht voor) tooimprove implementatie betrouwbaarheid en prestaties. Toestaan dat voor een groter dan het aantal virtuele machines die u van plan bent tooscale op Hallo van adresruimte 20%.
- Als u van plan bent toodeploy veel VM's, moet de quotalimieten voor uw berekenings-core toobe verhoogd.
- Fout- en upgradedomeinen zijn alleen consistent binnen een plaatsingsgroep. Deze architectuur wordt niet gewijzigd Hallo algemene beschikbaarheid van een schaal instellen, zoals virtuele machines gelijkmatig worden verdeeld over verschillende fysieke hardware, maar wordt uitgevoerd betekent dat als u twee virtuele machines op andere hardware zijn tooguarantee moet zorg ervoor dat ze zich in verschillende domeinen met fouten domeinen in dezelfde groep van de plaatsing Hallo. Fout domein en de plaatsing groeps-ID worden weergegeven in Hallo _weergave exemplaar_ instellen van een schaal VM. U kunt Hallo instantieweergave van een VM-schaalset bevatten weergeven in Hallo [Azure Resource Explorer](https://resources.azure.com/).


## <a name="creating-a-large-scale-set"></a>Een grote schaalset maken
Wanneer u een schaal instellen in hello Azure-portal maakt, kunt u toestaan deze tooscale toomultiple plaatsing groepen door Hallo instelling _limiet tooa één plaatsing groep_ optie too_False_ in Hallo _basisbeginselen_ blade. Met deze optie set too_False_, kunt u een _aantal exemplaar_ waarde van too1, 000.

![](./media/virtual-machine-scale-sets-placement-groups/portal-large-scale.png)

Kunt u een VM grootschalige ingesteld met Hallo [Azure CLI](https://github.com/Azure/azure-cli) _az vmss maken_ opdracht. Met deze opdracht ingesteld intelligent standaardinstellingen zoals subnetgrootte op basis van Hallo _aantal exemplaren_ argument:

```bash
az group create -l southcentralus -n biginfra
az vmss create -g biginfra -n bigvmss --image ubuntults --instance-count 1000
```
Houd er rekening mee dat Hallo _vmss maken_ wordt standaard een bepaalde configuratiewaarden als u ze niet opgeven. toosee hello beschikbare opties die u kunt onderdrukken, probeer:
```bash
az vmss create --help
```

Als u een grote schaal ingesteld door het opstellen van een Azure Resource Manager-sjabloon maakt, zorg er dan voor dat Hallo-sjabloon maakt u een scale-set op basis van beheerde Azure-schijven. U kunt instellen Hallo _singlePlacementGroup_ eigenschap too_false_ in Hallo _eigenschappen_ sectie Hallo _Microsoft.Compute/virtualMAchineScaleSets_ resource. Hallo volgende JSON-fragment toont Hallo begin van een scale set sjabloon, inclusief Hallo 1.000 VM-capaciteit en Hallo _'singlePlacementGroup': false_ instelling:
```json
{
  "type": "Microsoft.Compute/virtualMachineScaleSets",
  "location": "australiaeast",
  "name": "bigvmss",
  "sku": {
    "name": "Standard_DS1_v2",
    "tier": "Standard",
    "capacity": 1000
  },
  "properties": {
    "singlePlacementGroup": false,
    "upgradePolicy": {
      "mode": "Automatic"
    }
```
Voor een compleet voorbeeld van een grote schaal stelt u de sjabloon, raadpleeg dan te[https://github.com/gbowerman/azure-myriad/blob/master/bigtest/bigbottle.json](https://github.com/gbowerman/azure-myriad/blob/master/bigtest/bigbottle.json).

## <a name="converting-an-existing-scale-set-toospan-multiple-placement-groups"></a>Toospan instellen meerdere plaatsing groepen converteren van een bestaande schaal
toomake een bestaande VM-geschikt is schaalset voor het schalen van toomore dan 100 virtuele machines, moet u toochange hello _singplePlacementGroup_ eigenschap too_false_ in Hallo scale model instelt. U kunt testen met het wijzigen van deze eigenschap Hello [Azure Resource Explorer](https://resources.azure.com/). Zoeken naar een bestaande schaalset, selecteer _bewerken_ en wijzig Hallo _singlePlacementGroup_ eigenschap. Als u deze eigenschap niet ziet, kan worden weergegeven, Hallo scale ingesteld met een oudere versie van Hallo Microsoft.Compute-API.

>[!NOTE] 
U kunt een ingesteld op basis van een enkele plaatsing groep alleen (Hallo standaardgedrag) tooa ondersteunen meerdere plaatsing groepen ondersteunende schaal wijzigen, maar Hallo andersom kan niet worden geconverteerd. Zorg daarom dat u weet Hallo eigenschappen van grote schaalsets voordat deze wordt geconverteerd. Zorg in het bijzonder, hoeft u geen laag 4 taakverdeling met hello Azure Load Balancer.



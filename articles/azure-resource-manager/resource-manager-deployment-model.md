---
title: aaaResource Manager en klassieke implementatie | Microsoft Docs
description: Hierin wordt beschreven Hallo verschillen tussen Hallo Resource Manager-implementatiemodel en klassieke hello (of Service Management)-implementatiemodel.
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 7ae0ffa3-c8da-4151-bdcc-8f4f69290fb4
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/09/2017
ms.author: tomfitz
ms.openlocfilehash: fbf1959991b100547a459bf88a29c0afbc8592e8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-resource-manager-vs-classic-deployment-understand-deployment-models-and-hello-state-of-your-resources"></a>Azure Resource Manager versus klassieke implementatie: implementatiemodellen begrijpen en de status van uw resources Hallo
In dit onderwerp leert u Azure Resource Manager en het klassieke implementatiemodel, Hallo status van uw resources en waarom uw resources zijn geïmplementeerd met een of andere Hallo. Hallo Resource Manager en de klassieke implementatiemodellen vertegenwoordigen twee verschillende manieren voor het implementeren en beheren van uw Azure-oplossingen. U ermee via twee verschillende sets in de API en Hallo geïmplementeerd resources kunnen bevatten belangrijke verschillen. Hallo twee modellen zijn niet volledig compatibel met elkaar. Dit onderwerp beschrijft die verschillen.

toosimplify hello implementatie en beheer van resources, is het raadzaam om gebruik te maken van Resource Manager voor alle nieuwe resources. Indien mogelijk, wordt aangeraden dat u bestaande resources via Resource Manager opnieuw implementeren.

Als u nieuwe tooResource Manager bent, kunt u toofirst revisie Hallo terminologie is gedefinieerd in Hallo [overzicht van Azure Resource Manager](resource-group-overview.md).

## <a name="history-of-hello-deployment-models"></a>Geschiedenis van Hallo-implementatiemodellen
Door Azure geleverde oorspronkelijk alleen Hallo-klassieke implementatiemodel. In dit model bestonden elke resource afzonderlijk; Er kon geen enkele manier toogroup verwante resources samen. In plaats daarvan moest u toomanually bijhouden welke resources bestaat uit uw oplossing of de toepassing en onthouden toomanage ze in een gecoördineerde benadering. een oplossing toodeploy, moest u tooeither elke resource afzonderlijk via de klassieke portal Hallo maken of een script maken dat alle Hallo resources in de juiste volgorde Hallo geïmplementeerd. een oplossing toodelete, moest u toodelete elke resource afzonderlijk. U kan niet eenvoudig toepassen en bijwerken van beleid voor toegangsbeheer voor verwante resources. Ten slotte kunt u codes tooresources toolabel ze met voorwaarden die u helpen uw resources bewaken en beheren van facturering niet toepassen.

In 2014 geïntroduceerd Azure Resource Manager, dat Hallo concept van een resourcegroep wordt toegevoegd. Een resourcegroep is een container voor resources die een gemeenschappelijk levenscyclus delen. Hallo Resource Manager-implementatiemodel biedt verschillende voordelen:

* U kunt implementeren, beheren en bewaken van alle Hallo-services voor uw oplossing als een groep in plaats van deze services afzonderlijk te verwerken.
* U kunt herhaaldelijk implementeren van uw oplossing gedurende de levenscyclus en erop vertrouwen dat uw resources worden geïmplementeerd in een consistente status.
* U kunt toegang tot besturingselement tooall bronnen toepassen in de resourcegroep en deze beleidsregels worden automatisch toegepast wanneer nieuwe resources toohello resourcegroep worden toegevoegd.
* U kunt tags toepassen tooresources toologically organiseren alle Hallo resources in uw abonnement.
* U kunt de notatie JSON (JavaScript Object) toodefine Hallo infrastructuur voor uw oplossing. Hallo JSON-bestand staat bekend als Resource Manager-sjabloon.
* U kunt Hallo afhankelijkheden tussen resources zo ze zijn geïmplementeerd in de juiste volgorde Hallo definiëren.

Wanneer het Resource Manager werd toegevoegd, zijn alle resources met terugwerkende kracht toodefault resourcegroepen toegevoegd. Als u een resource via nu klassieke implementatie maakt, wordt automatisch Hallo resource gemaakt binnen een standaardresourcegroep voor de service, ondanks dat u niet die resourcegroep op implementatie aangegeven hebt. Echter betekent alleen bestaande binnen een resourcegroep niet dat Hallo resource geconverteerde toohello Resource Manager-model is. Leert hier hoe twee implementatiemodellen in de volgende sectie Hallo Hallo worden verwerkt door elke service. 

## <a name="understand-support-for-hello-models"></a>Ondersteuning voor Hallo modellen begrijpen
Wanneer u beslist welke toouse deployment model voor uw resources, zijn er drie scenario's toobe op de hoogte van:

1. Hallo-service biedt ondersteuning voor Resource Manager en biedt slechts één type.
2. Hallo service biedt ondersteuning voor Resource Manager, maar biedt twee typen: één voor Resource Manager en één voor klassieke. Dit scenario geldt alleen toovirtual machines, opslagaccounts en virtuele netwerken.
3. Hallo-service biedt geen ondersteuning voor Resource Manager.

toodiscover of Resource Manager biedt ondersteuning voor een service bekijken [resourceproviders en typen](resource-manager-supported-services.md).

Als u wenst dat toouse Hallo-service biedt geen ondersteuning voor Resource Manager, moet u verder met behulp van klassieke implementatie.

Als het Hallo-service ondersteunt Resource Manager en **is niet** een virtuele machine, de storage-account of het virtuele netwerk, kunt u Resource Manager gebruiken zonder eventuele problemen.

Voor virtuele machines, opslagaccounts en virtuele netwerken, als Hallo resource is gemaakt via de klassieke implementatie, moet u blijven toooperate erop via de klassieke bewerkingen. Als Hallo virtuele machine, storage-account of virtueel netwerk is gemaakt via de implementatie van Resource Manager, moet u verder met Resource Manager-bewerkingen. Dit verschil krijgt verwarrend wanneer uw abonnement een combinatie van resources via de Resource Manager en klassieke implementatie gemaakt bevat. Deze combinatie van resources onverwachte resultaten kunt maken, omdat het Hallo-bronnen bieden geen ondersteuning voor dezelfde bewerkingen Hallo.

In sommige gevallen kan een Resource Manager-opdracht kan informatie ophalen over een bron via de klassieke implementatie gemaakt of een beheertaak zoals het verplaatsen van een resourcegroep voor klassieke resource tooanother kunt uitvoeren. Maar deze gevallen geeft geen Hallo indruk dat Hallo type Resource Manager-bewerkingen ondersteunt. Stel dat u hebt een resourcegroep met een virtuele machine die is gemaakt met het klassieke implementatiemodel. Als u Hallo volgende Resource Manager PowerShell-opdracht uitvoeren:

```powershell
Get-AzureRmResource -ResourceGroupName ExampleGroup -ResourceType Microsoft.ClassicCompute/virtualMachines
```

Deze retourneert Hallo virtuele machine:

```powershell
Name              : ExampleClassicVM
ResourceId        : /subscriptions/{guid}/resourceGroups/ExampleGroup/providers/Microsoft.ClassicCompute/virtualMachines/ExampleClassicVM
ResourceName      : ExampleClassicVM
ResourceType      : Microsoft.ClassicCompute/virtualMachines
ResourceGroupName : ExampleGroup
Location          : westus
SubscriptionId    : {guid}
```

Resource Manager-cmdlet echter Hallo **Get-AzureRmVM** retourneert alleen virtuele machines die zijn geïmplementeerd via Resource Manager. Hallo retourneert volgende opdracht geen Hallo virtuele machine via de klassieke implementatie gemaakt.

```powershell
Get-AzureRmVM -ResourceGroupName ExampleGroup
```

Alleen bronnen via Resource Manager support-tags is gemaakt. U kunt tags tooclassic resources niet toepassen.

## <a name="resource-manager-characteristics"></a>Resource Manager-kenmerken
toohelp u begrijpt Hallo twee modellen, gaan we bekijkt hello kenmerken van Resource Manager-typen:

* Via de Hallo gemaakt [Azure-portal](https://portal.azure.com/).
  
     ![Azure Portal](./media/resource-manager-deployment-model/portal.png)
  
     Voor berekening, opslag en netwerkresources, hebt u Hallo-optie van het gebruik van Resource Manager of klassiek implementatie. Selecteer **Resource Manager**.
  
     ![Implementatie van Resource Manager](./media/resource-manager-deployment-model/select-resource-manager.png)
* Gemaakt met Resource Manager-versie Hallo Hallo Azure PowerShell-cmdlets. Deze opdrachten gelden Hallo indeling *term AzureRmNoun*.

  ```powershell
  New-AzureRmResourceGroupDeployment
  ```

* Via de Hallo gemaakt [REST-API van Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/) voor REST-bewerkingen.
* Via de Azure CLI-opdrachten uitvoeren in Hallo gemaakt **arm** modus.
  
  ```azurecli
  azure config mode arm
  azure group deployment create
  ```

* Hallo brontype bevat geen **(klassiek)** in Hallo-naam. Hallo volgende afbeelding toont Hallo type als **opslagaccount**.
  
    ![web-app](./media/resource-manager-deployment-model/resource-manager-type.png)

## <a name="classic-deployment-characteristics"></a>Klassieke implementatie kenmerken
Mogelijk weet u ook het klassieke implementatiemodel Hallo als Hallo Service Management-model.

Resources die zijn gemaakt in Hallo classic deployment model share Hallo kenmerken te volgen:

* Via de Hallo gemaakt [klassieke portal](https://manage.windowsazure.com)
  
     ![Klassieke portal](./media/resource-manager-deployment-model/classic-portal.png)
  
     Of, hello Azure-portal en u geeft **klassieke** implementatie (voor berekening, opslag en netwerken).
  
     ![Klassieke implementatie](./media/resource-manager-deployment-model/select-classic.png)
* Via de versie van Service Management Hallo Hallo Azure PowerShell-cmdlets is gemaakt. Deze opdrachtnamen Hallo-indeling hebben *term AzureNoun*.

  ```powershell
  New-AzureVM
  ```

* Via de Hallo gemaakt [REST API van Opslagservicebeheer](https://msdn.microsoft.com/library/azure/ee460799.aspx) voor REST-bewerkingen.
* Gemaakt via Azure CLI-opdrachten uitvoeren in **asm** modus.

  ```azurecli
  azure config mode asm
  azure vm create
  ```
   
* Hallo brontype omvat **(klassiek)** in Hallo-naam. Hallo volgende afbeelding toont Hallo type als **Storage-account (klassiek)**.
  
    ![klassieke type](./media/resource-manager-deployment-model/classic-type.png)

U kunt hello Azure portal toomanage resources die zijn gemaakt via de klassieke implementatie gebruiken.

## <a name="changes-for-compute-network-and-storage"></a>Wijzigingen voor compute, netwerk en opslag
Hallo toont volgende diagram compute, netwerk en opslag resources die zijn geïmplementeerd via Resource Manager.

![Resource Manager-architectuur](./media/resource-manager-deployment-model/arm_arch3.png)

Houd er rekening mee Hallo relaties tussen Hallo-resources te volgen:

* Alle Hallo resources bestaan binnen een resourcegroep.
* Hallo virtuele machine is afhankelijk van een specifieke opslagaccount gedefinieerd in Hallo Storage resource provider toostore de schijven in de blob-opslag (vereist).
* Hallo virtuele machine verwijst naar een specifieke NIC die is gedefinieerd in Hallo netwerkresourceprovider (vereist) en een beschikbaarheidsset gedefinieerd in de resourceprovider voor Compute hello (optioneel).
* Hallo NIC verwijzingen Hallo van virtuele machine toegewezen IP-adres (vereist), Hallo subnet van het virtuele netwerk Hallo voor Hallo virtuele machine (vereist) en tooa Netwerkbeveiligingsgroep (optioneel).
* Hallo subnet binnen een virtueel netwerk verwijst naar een Netwerkbeveiligingsgroep (optioneel).
* Hallo load balancer exemplaar verwijst naar de back-endpool Hallo van IP-adressen met Hallo NIC van een virtuele machine (optioneel) en verwijst naar een load balancer openbare of particuliere IP-adres (optioneel).

Hier volgen Hallo-onderdelen en hun relaties voor klassieke implementatie:

![klassieke architectuur](./media/resource-manager-deployment-model/arm_arch1.png)

Hallo-classic-oplossing voor het hosten van een virtuele machine omvat:

* Een vereiste cloudservice die als een container fungeert voor het hosten van virtuele machines (berekenen). Virtuele machines worden automatisch voorzien van een netwerkinterfacekaart (NIC) en een IP-adres wordt toegewezen door Azure. Hallo-cloudservice bevat tevens een externe load balancer-exemplaar, een openbare IP-adres en standaard eindpunten tooallow extern bureaublad en externe PowerShell verkeer voor virtuele machines op basis van Windows en Secure Shell (SSH) voor op basis van Linux virtuele machines.
* Een vereiste storage-account dat winkels hello van VHD's voor een virtuele machine, met inbegrip van Hallo-besturingssysteem, tijdelijk en extra gegevensschijven (opslag).
* Een optioneel virtueel netwerk dat fungeert als een extra container waarin u kunt een structuur in een subnet maken en toewijzen Hallo-subnet op welke Hallo virtuele machine zich bevindt (netwerk).

Hallo volgende tabel beschrijft de wijzigingen in de wisselwerking tussen resourceproviders voor Compute, netwerk en opslag:

| Item | Klassiek | Resource Manager |
| --- | --- | --- |
| Cloudservice voor virtuele machines |Cloudservice is een container voor de opslag van Hallo virtuele machines die de beschikbaarheid van Hallo-platform en taakverdeling vereist. |Cloudservice is niet langer een object dat is vereist voor het maken van een virtuele Machine via het nieuwe model Hallo. |
| Virtuele netwerken |Een virtueel netwerk is optioneel voor Hallo virtuele machine. Als opgenomen, kan niet Hallo virtueel netwerk met Resource Manager worden geïmplementeerd. |Virtuele machine vereist een virtueel netwerk dat is geïmplementeerd met Resource Manager. |
| Opslagaccounts |Hallo virtuele machine vereist een opslagaccount die Hallo VHD's voor het besturingssysteem hello, tijdelijk en extra gegevensschijven opslaat. |Hallo virtuele machine vereist een toostore storage-account de schijven in de blob-opslag. |
| Beschikbaarheidssets |Beschikbaarheid toohello platform werd aangegeven door het configureren van Hallo dezelfde "AvailabilitySetName" op Hallo van virtuele Machines. Hallo kunt u het maximum aantal foutdomeinen was 2. |Beschikbaarheidsset is een resource die beschikbaar wordt gesteld door Microsoft.Compute-provider. Virtuele Machines die uiterst beschikbaar moeten worden opgenomen in Hallo Beschikbaarheidsset. Hallo kunt u het maximum aantal foutdomeinen is nu 3. |
| Affiniteitsgroepen |Voor het maken van virtuele netwerken waren affiniteitsgroepen vereist. Met de Hallo introductie van regionale virtuele netwerken, die was echter niet vereist meer. |toosimplify, concept van Affiniteitsgroepen Hallo bestaat niet in Hallo API's beschikbaar gesteld via Azure Resource Manager. |
| Taakverdeling |Het maken van een Cloudservice biedt een impliciete load balancer voor Hallo virtuele Machines die zijn geïmplementeerd. |Hallo Load Balancer is een resource die beschikbaar zijn gesteld door Microsoft.COMPUTE-provider Hallo. moet de primaire netwerkinterface Hallo Hallo virtuele Machines die toobe gelijkmatig verdeeld moet verwijzen naar Hallo load balancer. Load balancers kunnen intern of extern zijn. Een load balancer-exemplaar verwijst naar de back-endpool Hallo van IP-adressen met Hallo NIC van een virtuele machine (optioneel) en verwijst naar een load balancer openbare of particuliere IP-adres (optioneel). [Meer informatie.](../virtual-network/resource-groups-networking.md) |
| Virtueel IP-adres |Cloudservices krijgen een standaard VIP (virtuele IP-adres) wanneer een virtuele machine tooa-cloudservice wordt toegevoegd. Hallo virtueel IP-adres is Hallo-adres die zijn gekoppeld aan Hallo impliciete load balancer. |Openbaar IP-adres is een resource die beschikbaar zijn gesteld door Microsoft.COMPUTE-provider Hallo. Een openbaar IP-adres kan statisch (gereserveerd) of dynamisch zijn. Dynamische openbare IP-adressen kunnen worden toegewezen als tooa Load Balancer. Openbare IP-adressen kunnen worden beveiligd met beveiligingsgroepen. |
| Gereserveerd IP-adres |U kunt een IP-adres in Azure en koppel deze met een Cloudservice tooensure die Hallo IP-adres is vergrendeld reserveren. |Openbaar IP-adres kunnen worden gemaakt in de 'Statische' modus en het Hallo biedt dezelfde mogelijkheden als een ' gereserveerde IP-adres'. Statische openbare IP-adressen kunnen alleen worden toegewezen tooa Load balancer nu. |
| Openbaar IP-adres (PIP) per VM |Openbare IP-adressen kunnen ook rechtstreeks worden gekoppeld tooa VM. |Openbaar IP-adres is een resource die beschikbaar zijn gesteld door Microsoft.COMPUTE-provider Hallo. Een openbaar IP-adres kan statisch (gereserveerd) of dynamisch zijn. Echter zijn alleen dynamische openbare IP-adressen toegewezen tooa netwerkinterface tooget openbare IP-adres per VM nu. |
| Eindpunten |Invoer eindpunten nodig toobe geconfigureerd op een virtuele Machine toobe open connectiviteit voor bepaalde poorten. Een van de algemene modi Hallo van het verbinden van toovirtual machines wordt gerealiseerd door het instellen van invoereindpunten. |Binnenkomende NAT-regels kunnen worden geconfigureerd op de Load Balancers tooachieve Hallo eindpunten op bepaalde poorten voor het verbinden van virtuele machines toohello schakelen. |
| DNS-naam |Een cloudservice krijgt een impliciete, globaal unieke DNS-naam. Bijvoorbeeld: `mycoffeeshop.cloudapp.net`. |DNS-namen zijn optionele parameters die voor de resource van een openbaar IP-adres kunnen worden opgegeven. Hallo FQDN-naam is in de volgende Hallo indeling - `<domainlabel>.<region>.cloudapp.azure.com`. |
| Netwerkinterfaces |Primaire en secundaire netwerkinterface en de bijbehorende eigenschappen werden gedefinieerd als de netwerkconfiguratie van een virtuele machine. |De netwerkinterface is een resource die beschikbaar wordt gesteld door de Microsoft.Compute-provider. Hallo levenscyclus van Hallo die netwerkinterface niet is gekoppeld tooa virtuele Machine. Hierin wordt verwezen naar Hallo virtuele machine toegewezen IP-adres (vereist), Hallo subnet van het virtuele netwerk Hallo voor Hallo virtuele machine (vereist) en tooa Netwerkbeveiligingsgroep (optioneel). |

toolearn over het verbinden van virtuele netwerken vanuit verschillende implementatiemodellen, Zie [verbinding maken met virtuele netwerken vanuit verschillende implementatiemodellen in Hallo portal](../vpn-gateway/vpn-gateway-connect-different-deployment-models-portal.md).

## <a name="migrate-from-classic-tooresource-manager"></a>Migreren van klassieke tooResource Manager
Als u bent klaar toomigrate Zie uw resources van klassieke implementatie tooResource deployment Manager:

1. [Technische deep dive op platform ondersteund migratie van klassiek tooAzure Resource Manager](../virtual-machines/windows/migration-classic-resource-manager-deep-dive.md)
2. [Ondersteund platform migratie van IaaS-resources van klassieke tooAzure Resource Manager](../virtual-machines/windows/migration-classic-resource-manager-overview.md)
3. [Migreren van IaaS-resources van klassieke tooAzure Resource Manager met behulp van Azure PowerShell](../virtual-machines/windows/migration-classic-resource-manager-ps.md)
4. [Migreren van IaaS-resources van klassieke tooAzure Resource Manager met behulp van Azure CLI](../virtual-machines/virtual-machines-linux-cli-migration-classic-resource-manager.md)

## <a name="frequently-asked-questions"></a>Veelgestelde vragen
**Kan ik een virtuele machine met Azure Resource Manager toodeploy in een virtueel netwerk gemaakt met behulp van klassieke implementatie maken?**

Dit wordt niet ondersteund. U kunt Azure Resource Manager toodeploy een virtuele machine niet gebruiken in een virtueel netwerk dat is gemaakt met de klassieke implementatie.

**Kan ik maken een virtuele machine met hello Azure Resource Manager van een gebruikersinstallatiekopie die is gemaakt met hello Azure Service Management API's?**

Dit wordt niet ondersteund. U kunt echter Hallo VHD-bestanden kopiëren van een opslagaccount die is gemaakt met de Hallo Service Management-API's en voeg ze tooa nieuwe account gemaakt via Azure Resource Manager toe.

**Wat is Hallo impact op Hallo quotum voor mijn abonnement?**

Hallo-quota's voor het Hallo virtuele machines, virtuele netwerken en opslagaccounts die zijn gemaakt via hello Azure Resource Manager zijn gescheiden van andere quota. Elk abonnement opgehaald quota toocreate Hallo resources met behulp van Hallo nieuwe API's. U kunt meer lezen over de extra quota Hallo [hier](../azure-subscription-service-limits.md).

**Kan ik niet verder toouse mijn geautomatiseerde scripts voor het inrichten van virtuele machines, virtuele netwerken en opslagaccounts via Hallo Resource Manager-API's?**

Alle Hallo automatisering en scripts die u hebt gemaakt blijven toowork Hallo bestaande virtuele machines, virtuele netwerken die zijn gemaakt met de Hallo Azure Service Management-modus. Hallo scripts hebben echter toobe bijgewerkte toouse Hallo nieuwe schema voor het maken van Hallo dezelfde resources via de modus Resource Manager Hallo.

**Waar vind ik voorbeelden van Azure Resource Manager-sjablonen**

Een uitgebreide set startsjablonen vindt u op [Azure Resource Manager Quick Start-sjablonen](https://azure.microsoft.com/documentation/templates/).

## <a name="next-steps"></a>Volgende stappen
* toowalk via Hallo maken van een sjabloon met een definitie van een virtuele machine, opslagaccount en virtueel netwerk, Zie [overzicht voor Resource Manager-sjabloon](resource-manager-template-walkthrough.md).
* Zie toosee Hallo-opdrachten voor het implementeren van een sjabloon [Implementeer een toepassing met Azure Resource Manager-sjabloon](resource-group-template-deploy.md).


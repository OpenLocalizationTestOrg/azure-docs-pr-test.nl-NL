---
title: aaaMigrate VMs tooResource Manager met Azure CLI | Microsoft Docs
description: Dit artikel begeleidt u bij Hallo platform ondersteund migratie van resources van klassieke tooAzure Resource Manager met Azure CLI
services: virtual-machines-linux
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: d6f5a877-05b6-4127-a545-3f5bede4e479
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 03/30/2017
ms.author: kasing
ms.openlocfilehash: 0b11f4bb1b4658b3e88bf7629147ed953b678556
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-iaas-resources-from-classic-tooazure-resource-manager-by-using-azure-cli"></a>Migreren van IaaS-resources van klassieke tooAzure Resource Manager met behulp van Azure CLI
Deze stappen ziet u hoe Azure-opdrachtregelinterface (CLI) toouse toomigrate infrastructuur opdrachten als een dienst (IaaS) resources vanuit Hallo classic deployment model toohello Azure Resource Manager-implementatiemodel. Hallo artikel vereist Hallo [Azure CLI](../../cli-install-nodejs.md).

> [!NOTE]
> Alle Hallo bewerkingen hier beschreven zijn idempotent. Als er een probleem dan een niet-ondersteunde functie of een configuratiefout, raden wij aan dat u opnieuw Hallo proberen voorbereiden, afgebroken of doorgevoerd, bewerking. Hallo actie opnieuw wordt en probeer het Hallo-platform.
> 
> 

<br>
Hier volgt een stroomdiagram tooidentify Hallo volgorde waarin stappen toobe uitgevoerd tijdens een migratie moeten

![Schermafbeelding van de migratiestappen Hallo](../windows/media/migration-classic-resource-manager/migration-flow.png)

## <a name="step-1-prepare-for-migration"></a>Stap 1: Voorbereiden voor migratie
Hier volgen enkele aanbevolen procedures die wij adviseren kijkt u bij het evalueren van IaaS-Resourcemigratie van klassieke tooResource Manager:

* Lees Hallo [lijst met niet-ondersteunde configuraties of functies](../windows/migration-classic-resource-manager-overview.md). Als u virtuele machines die gebruikmaken van niet-ondersteunde configuraties of functies hebt, raden wij wachten op Hallo functie of configuratieserver ondersteuning toobe aangekondigd. U kunt ook kunt u deze functie verwijderen of verplaatsen buiten de migratie van die configuratie tooenable als deze bij uw behoeften past.
* Als u scripts die uw infrastructuur en toepassingen vandaag implementeert geautomatiseerde, kunt u toocreate instellingen voor een vergelijkbaar met behulp van deze scripts voor de migratie. U kunt ook voorbeeld omgevingen instellen met behulp van hello Azure-portal.

> [!IMPORTANT]
> Toepassingsgateways worden momenteel niet ondersteund voor migratie van klassiek tooResource Manager. Hallo gateway toomigrate een klassiek virtueel netwerk met een toepassingsgateway verwijderen voordat u een netwerk voorbereiden bewerking toomove Hallo uitvoert. Nadat u Hallo migratie hebt voltooid, sluit u Hallo gateway in Azure Resource Manager. 
>
>ExpressRoute-gateways die verbinding maken met tooExpressRoute circuits in een ander abonnement kunnen niet automatisch worden gemigreerd. In dergelijke gevallen Hallo ExpressRoute-gateway verwijderen, Migreer het virtuele netwerk Hallo en maak Hallo-gateway. Zie [migreren ExpressRoute-circuits en bijbehorende virtuele netwerken vanuit Hallo klassieke toohello Resource Manager-implementatiemodel](../../expressroute/expressroute-migration-classic-resource-manager.md) voor meer informatie.
> 
> 

## <a name="step-2-set-your-subscription-and-register-hello-provider"></a>Stap 2: Stel uw abonnement en Hallo provider registreren
Voor migratiescenario's, moet u tooset van uw omgeving voor zowel klassieke en het Resource Manager. [Azure CLI installeren](../../cli-install-nodejs.md) en [Selecteer uw abonnement](../../xplat-cli-connect.md).

Aanmelden tooyour-account.

    azure login

Selecteer hello Azure-abonnement met behulp van de volgende opdracht Hallo.

    azure account set "<azure-subscription-name>"

> [!NOTE]
> Registratie is een eenmalige stap maar behoeften toobe eenmaal voordat u de migratie wordt uitgevoerd. Zonder te registreren ziet u Hallo volgende foutbericht wordt weergegeven 
> 
> *BadRequest: Abonnement is niet geregistreerd voor migratie.* 
> 
> 

Registreren bij de Hallo migratie resourceprovider met behulp van de volgende opdracht Hallo. Houd er rekening mee dat in sommige gevallen kan deze opdracht time-out. Hallo-registratie is gelukt.

    azure provider register Microsoft.ClassicInfrastructureMigrate

Wacht vijf minuten voor Hallo registratie toofinish. U kunt de status van de Hallo van Hallo goedkeuring controleren met behulp van de volgende opdracht Hallo. Zorg ervoor dat RegistrationState `Registered` voordat u doorgaat.

    azure provider show Microsoft.ClassicInfrastructureMigrate

Schakel nu over CLI toohello `asm` modus.

    azure config mode asm

## <a name="step-3-make-sure-you-have-enough-azure-resource-manager-virtual-machine-cores-in-hello-azure-region-of-your-current-deployment-or-vnet"></a>Stap 3: Controleer of er voldoende virtuele Machine van Azure Resource Manager kernen in hello Azure-regio van uw huidige implementatie of VNET
Voor deze stap moet u tooswitch te`arm` modus. Dit doen met de volgende opdracht Hallo.

```
azure config mode arm
```

U kunt Hallo na CLI opdracht toocheck Hallo huidige hoeveelheid kernen hebt u in Azure Resource Manager gebruiken. toolearn meer informatie over quota core, Zie [limieten en hello Azure Resource Manager](../../azure-subscription-service-limits.md#limits-and-the-azure-resource-manager)

```
azure vm list-usage -l "<Your VNET or Deployment's Azure region"
```

Als u klaar bent voor het verifiëren van deze stap kunt u schakelen terug te`asm` modus.

    azure config mode asm


## <a name="step-4-option-1---migrate-virtual-machines-in-a-cloud-service"></a>Stap 4: Optie 1 - migreren van virtuele machines in een cloudservice
Haal de lijst Hallo van cloud-services met behulp van de volgende opdracht Hallo en kies Hallo cloudservice die u wilt toomigrate. Houd er rekening mee dat als Hallo virtuele machines in de cloudservice Hallo in een virtueel netwerk zijn of als ze web/worker rollen hebben, u een foutbericht weergegeven ontvangt.

    azure service list

Hallo volgende tooget Hallo implementatie opdrachtnaam voor cloudservice Hallo uit Hallo uitgebreide uitvoer worden uitgevoerd. In de meeste gevallen is implementatienaam Hallo Hallo dezelfde is als Hallo cloud service-naam.

    azure service show <serviceName> -vv

Eerst valideren als u met behulp van de volgende opdrachten Hallo Hallo-cloudservice kunt migreren:

```shell
azure service deployment validate-migration <serviceName> <deploymentName> new "" "" ""
```

Bereid Hallo virtuele machines in de cloudservice Hallo voor migratie. U hebt twee opties toochoose uit.

Als u toomigrate Hallo VMs tooa platform gemaakt virtueel netwerk wilt, gebruikt u Hallo opdracht te volgen.

    azure service deployment prepare-migration <serviceName> <deploymentName> new "" "" ""

Als u toomigrate tooan bestaande virtuele netwerk in Hallo Resource Manager-implementatiemodel wilt, gebruikt u Hallo opdracht te volgen.

    azure service deployment prepare-migration <serviceName> <deploymentName> existing <destinationVNETResourceGroupName> <subnetName> <vnetName>

Nadat het Hallo voorbereiden bewerking is voltooid, kunt u bekijkt hello uitgebreide uitvoer tooget Hallo migratiestatus Hallo VM's en ervoor te zorgen dat ze Hallo `Prepared` status.

    azure vm show <vmName> -vv

Controleer de configuratie van Hallo voor Hallo voorbereid resources met behulp van de CLI of hello Azure-portal. Als u niet klaar voor de migratie bent en u toogo back toohello oude status wilt, gebruik Hallo opdracht te volgen.

    azure service deployment abort-migration <serviceName> <deploymentName>

Als Hallo voorbereide configuratie er goed uitziet, kunt u verder gaan en Hallo resources met behulp van de volgende opdracht Hallo doorvoeren.

    azure service deployment commit-migration <serviceName> <deploymentName>



## <a name="step-4-option-2----migrate-virtual-machines-in-a-virtual-network"></a>Stap 4: Optie 2: migreren van virtuele machines in een virtueel netwerk
Pick Hallo virtueel netwerk dat u wilt dat toomigrate. Houd er rekening mee dat als Hallo virtueel netwerk web/werkrollen of VM's met niet-ondersteunde configuraties bevat, u een validatiefoutbericht krijgt.

Alle Hallo virtuele netwerken in Hallo abonnement ophalen met behulp van de volgende opdracht Hallo.

    azure network vnet list

Hallo-uitvoer ziet er ongeveer als volgt:

![Schermopname van het Hallo-opdrachtregel met de naam van de hele virtuele netwerk Hallo gemarkeerd.](../media/virtual-machines-linux-cli-migration-classic-resource-manager/vnet.png)

Hallo in Hallo hierboven voorbeeld **virtualNetworkName** is de volledige naam Hallo **'Groep classicubuntu16 classicubuntu16'**.

Eerst valideren als u Hallo virtueel netwerk met behulp van de volgende opdracht Hallo kunt migreren:

```shell
azure network vnet validate-migration <virtualNetworkName>
```

Hallo virtueel netwerk van uw keuze voorbereiden voor migratie met behulp van de volgende opdracht Hallo.

    azure network vnet prepare-migration <virtualNetworkName>

Controleer de configuratie van Hallo voor Hallo voorbereid virtuele machines met behulp van de CLI of hello Azure-portal. Als u niet klaar voor de migratie bent en u toogo back toohello oude status wilt, gebruik Hallo opdracht te volgen.

    azure network vnet abort-migration <virtualNetworkName>

Als Hallo voorbereide configuratie er goed uitziet, kunt u verder gaan en Hallo resources met behulp van de volgende opdracht Hallo doorvoeren.

    azure network vnet commit-migration <virtualNetworkName>

## <a name="step-5-migrate-a-storage-account"></a>Stap 5: Een opslagaccount migreren
Zodra u klaar bent met het migreren van Hallo virtuele machines, wordt u aangeraden dat u migreert Hallo storage-account.

Hallo opslagaccount voorbereiden voor migratie met behulp van de volgende opdracht Hallo

    azure storage account prepare-migration <storageAccountName>

Controleer de configuratie van Hallo voor Hallo met CLI of Azure-portal Hallo voorbereid storage-account. Als u niet klaar voor de migratie bent en u toogo back toohello oude status wilt, gebruik Hallo opdracht te volgen.

    azure storage account abort-migration <storageAccountName>

Als Hallo voorbereide configuratie er goed uitziet, kunt u verder gaan en Hallo resources met behulp van de volgende opdracht Hallo doorvoeren.

    azure storage account commit-migration <storageAccountName>

## <a name="next-steps"></a>Volgende stappen

* [Overzicht van de migratie van IaaS-resources van klassieke tooAzure Resource Manager-platform ondersteund](migration-classic-resource-manager-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Technische deep dive op platform ondersteund migratie van klassiek tooAzure Resource Manager](migration-classic-resource-manager-deep-dive.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Migratie van IaaS-resources van klassieke tooAzure Resource Manager plannen](migration-classic-resource-manager-plan.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [PowerShell toomigrate IaaS resources van klassieke tooAzure Resource Manager gebruiken](../windows/migration-classic-resource-manager-ps.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Community-hulpprogramma's voor hulp bij de migratie van IaaS-resources van klassieke tooAzure Resource Manager](../windows/migration-classic-resource-manager-community-tools.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Bekijk de meest voorkomende migratiefouten](migration-classic-resource-manager-errors.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Bekijk Hallo veelgestelde meest vragen over migreren IaaS resources van klassieke tooAzure Resource Manager](migration-classic-resource-manager-faq.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

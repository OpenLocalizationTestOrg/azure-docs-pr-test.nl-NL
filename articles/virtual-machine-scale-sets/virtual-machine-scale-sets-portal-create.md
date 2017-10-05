---
title: Maak een virtuele-Machineschaalset met de Azure portal | Microsoft Docs
description: Met Azure portal-schaalsets implementeren.
keywords: Virtuele-machineschaalsets
services: virtual-machine-scale-sets
documentationcenter: 
author: gatneil
manager: madhana
editor: tysonn
tags: azure-resource-manager
ms.assetid: 9c1583f0-bcc7-4b51-9d64-84da76de1fda
ms.service: virtual-machine-scale-sets
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm
ms.devlang: na
ms.topic: article
ms.date: 05/01/2017
ms.author: negat
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 7157a429829974b45dad29ac53fb5fb46c71f821
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-create-a-virtual-machine-scale-set-with-the-azure-portal"></a>Het maken van een virtuele-Machineschaalset met de Azure-portal
Deze zelfstudie laat zien hoe eenvoudig het is een virtuele-Machineschaalset maken in een paar minuten met behulp van de Azure-portal. Als u nog geen abonnement op Azure hebt, maak dan een [gratis account](https://azure.microsoft.com/free/) aan voordat u begint.

## <a name="choose-the-vm-image-from-the-marketplace"></a>Een installatiekopie voor de virtuele machine kiezen in de marketplace
U kunt een schaal CentOS, virtuele CoreOS, Debian, Open Suse, Red Hat Enterprise Linux, SUSE Linux Enterprise Server, Ubuntu Server of installatiekopieën van Windows Server in te stellen eenvoudig implementeren vanuit de portal.

Eerst, navigeer naar de [Azure-portal](https://portal.azure.com) in een webbrowser. Klik op `New`, zoeken naar `scale set`, en selecteer vervolgens de `Virtual machine scale set` post:

![ScaleSetPortalOverview](./media/virtual-machine-scale-sets-portal-create/ScaleSetPortalOverview.PNG)

## <a name="create-the-scale-set"></a>De schaalset maken
U kunt nu de standaardinstellingen gebruiken en de schaalaanpassingsset snel maken.

* Op de `Basics` blade een naam voor de scale-set. Deze naam wordt het grondtal van de FQDN-naam van de load balancer voor de schaalaanpassingsset, dus zorg ervoor dat de naam uniek is in alle Azure.
* Selecteer het gewenste besturingssysteem typt u de gewenste gebruikersnaam invoeren en selecteren welke verificatiemethode typt u liever. Als u een wachtwoord kiest, moet deze zijn minstens 12 tekens lang en drie van de volgende vier complexiteitsvereisten voldoen aan: één kleine letter, één hoofdletter, één cijfer en één speciaal teken. Zie meer informatie over [vereisten voor gebruikersnaam en wachtwoord](../virtual-machines/windows/faq.md#what-are-the-username-requirements-when-creating-a-vm). Als u ervoor kiest `SSH public key`, zorg ervoor dat alleen plakken in uw openbare sleutel niet uw persoonlijke sleutel:

![ScaleSetPortalBasics](./media/virtual-machine-scale-sets-portal-create/ScaleSetPortalBasics.PNG)

* Kies of u wilt beperken van de schaal is ingesteld op een groep één plaatsing of of dit meerdere plaatsing groepen moet omvatten. Schaal kunt u de schaal is ingesteld op span plaatsing groepen toe, stelt u meer dan 100 virtuele machines in capaciteit (maximaal 1000) met bepaalde beperkingen. Zie voor meer informatie [deze documentatie](./virtual-machine-scale-sets-placement-groups.md).
* Voer uw gewenste Resourcegroepnaam en de locatie en klik vervolgens op `OK`.
* Op de `Virtual machine scale set service settings` blade: Geef de gewenste domeinnaamlabel (de basis van de FQDN-naam voor de load balancer voor de schaalaanpassingsset). Dit label moet uniek zijn binnen alle Azure.
* Kies uw schijfimage gewenste besturingssysteem, het aantal exemplaren en de grootte van de machine.
* De gewenste schijf kiezen: beheerd of onbeheerd. Zie voor meer informatie [deze documentatie](./virtual-machine-scale-sets-managed-disks.md). Als u hebt gekozen om de schaal instelt span meerdere plaatsing groepen, deze optie niet meer beschikbaar omdat de beheerde schijf is vereist voor schaalsets meerdere groepen voor plaatsing.
* In- of uitschakelen voor automatisch schalen en configureren als ingeschakeld:

![ScaleSetPortalService](./media/virtual-machine-scale-sets-portal-create/ScaleSetPortalService.PNG)

* Op de `Summary` blade als validatie is voltooid, klikt u op `OK` ingesteld voor het starten van de schaal implementatie.


## <a name="connect-to-a-vm-in-the-scale-set"></a>Verbinding maken met een virtuele machine in de schaalset
Als u wilt beperken schaal ingesteld op een enkele plaatsing-groep, wordt klikt u vervolgens de schaalaanpassingsset geïmplementeerd met NAT-regels geconfigureerd waarmee u verbinding maken met de schaal eenvoudig ingesteld (zo niet, verbinding maken met de virtuele machines in de schaalset, u waarschijnlijk hoeft te maken van een jumpbox in dezelfde  virtueel netwerk als de schaal instellen). Om ze te bekijken, gaat u naar de `Inbound NAT Rules` tabblad van de load balancer voor de schaalaanpassingsset:

![ScaleSetPortalNatRules](./media/virtual-machine-scale-sets-portal-create/ScaleSetPortalNatRules.PNG)

U kunt verbinding maken met elke virtuele machine in de schaal instelt met behulp van deze NAT-regels. Bijvoorbeeld: voor een Windows-scale set, als er een NAT-regel op de binnenkomende poort 50000 u kan verbinding maken met die machine via RDP op `<load-balancer-ip-address>:50000`. Voor een Linux-scale set, zou u verbinding met de opdracht `ssh -p 50000 <username>@<load-balancer-ip-address>`.

## <a name="next-steps"></a>Volgende stappen
Zie voor documentatie over het implementeren van de schaal wordt ingesteld vanuit de CLI, [deze documentatie](virtual-machine-scale-sets-cli-quick-create.md).

Zie voor documentatie over het implementeren van de schaal wordt ingesteld vanuit PowerShell, [deze documentatie](virtual-machine-scale-sets-windows-create.md).

Zie voor documentatie over het implementeren van de schaal wordt ingesteld vanuit Visual Studio, [deze documentatie](virtual-machine-scale-sets-vs-create.md).

Bekijk voor algemene documentatie, de [documentatie overzichtspagina voor schaalsets](virtual-machine-scale-sets-overview.md).

Bekijk voor algemene informatie, de [belangrijkste startpagina voor schaalsets](https://azure.microsoft.com/services/virtual-machine-scale-sets/).


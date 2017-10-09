---
title: een virtuele-Machineschaalset met aaaCreate hello Azure-portal | Microsoft Docs
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
ms.openlocfilehash: 23c88f4b1ba99994a38f8886f60735da74e5c17e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-virtual-machine-scale-set-with-hello-azure-portal"></a>Hoe toocreate een virtuele-Machineschaalset met hello Azure-portal
Deze zelfstudie laat zien hoe eenvoudig het is een virtuele-Machineschaalset toocreate in een paar minuten met behulp van hello Azure-portal. Als u nog geen abonnement op Azure hebt, maak dan een [gratis account](https://azure.microsoft.com/free/) aan voordat u begint.

## <a name="choose-hello-vm-image-from-hello-marketplace"></a>Kies Hallo VM-installatiekopie in marketplace Hallo
U kunt eenvoudig een schaal CentOS, virtuele CoreOS, Debian, Open Suse, Red Hat Enterprise Linux, SUSE Linux Enterprise Server, Ubuntu Server of installatiekopieën van Windows Server in te stellen vanuit de portal Hallo implementeren.

Ga eerst toohello [Azure-portal](https://portal.azure.com) in een webbrowser. Klik op `New`, zoeken naar `scale set`, en selecteer vervolgens Hallo `Virtual machine scale set` post:

![ScaleSetPortalOverview](./media/virtual-machine-scale-sets-portal-create/ScaleSetPortalOverview.PNG)

## <a name="create-hello-scale-set"></a>Hallo scale set maken
U kunt nu Hallo standaardinstellingen gebruiken en snel maken Hallo schaalset.

* Op Hallo `Basics` blade een naam voor het Hallo-schaalset. Deze naam wordt Hallo base Hallo FQDN Hallo load balancer voor schaalset hello, zorg er dus Hallo naam uniek is in alle Azure.
* Selecteer het gewenste besturingssysteem typt u de gewenste gebruikersnaam invoeren en selecteren welke verificatiemethode typt u liever. Als u een wachtwoord kiest, moet deze zijn minstens 12 tekens lang en drie buiten Hallo de volgende vier complexiteitsvereisten voldoen aan: één kleine letter, één hoofdletter, één cijfer en één speciaal teken. Zie meer informatie over [vereisten voor gebruikersnaam en wachtwoord](../virtual-machines/windows/faq.md#what-are-the-username-requirements-when-creating-a-vm). Als u ervoor kiest `SSH public key`, ervoor tooonly plakken in uw openbare sleutel niet uw persoonlijke sleutel:

![ScaleSetPortalBasics](./media/virtual-machine-scale-sets-portal-create/ScaleSetPortalBasics.PNG)

* Kies of u zou doen zoals toolimit hello tooa plaatsing van één groep schaalset of dat dit meerdere plaatsing groepen moet omvatten. Bij het toestaan van Hallo schaalset toospan plaatsing groepen kan voor de schaal wordt meer dan 100 virtuele machines in capaciteit (omhoog too1, 000) met bepaalde beperkingen. Zie voor meer informatie [deze documentatie](./virtual-machine-scale-sets-placement-groups.md).
* Voer uw gewenste Resourcegroepnaam en de locatie en klik vervolgens op `OK`.
* Op Hallo `Virtual machine scale set service settings` blade: Geef de gewenste domeinnaamlabel (basis Hallo Hallo FQDN-naam voor de load balancer Hallo voor Hallo schaalset). Dit label moet uniek zijn binnen alle Azure.
* Kies uw schijfimage gewenste besturingssysteem, het aantal exemplaren en de grootte van de machine.
* De gewenste schijf kiezen: beheerd of onbeheerd. Zie voor meer informatie [deze documentatie](./virtual-machine-scale-sets-managed-disks.md). Als u hebt gekozen toohave hello schaalset span meerdere plaatsing groepen, deze optie niet meer beschikbaar omdat de beheerde schijf is vereist voor schaal sets toospan plaatsing groepen.
* In- of uitschakelen voor automatisch schalen en configureren als ingeschakeld:

![ScaleSetPortalService](./media/virtual-machine-scale-sets-portal-create/ScaleSetPortalService.PNG)

* Op Hallo `Summary` blade als validatie is voltooid, klikt u op `OK` toostart hello schaalset implementatie.


## <a name="connect-tooa-vm-in-hello-scale-set"></a>Verbinding maken met tooa VM in de schaalset Hallo
Als u hebt gekozen toolimit schaal ingesteld tooa plaatsing van één groep, wordt de Hallo scale set wordt geïmplementeerd met NAT-regels geconfigureerd toolet u toohello scale ingesteld eenvoudig verbinding maken (als u niet het geval is, tooconnect toohello virtuele machines in Hallo scale is ingesteld, moet u waarschijnlijk toocreate een jumpbox in Hallo hetzelfde virtuele netwerk als Hallo schaalset). toosee, gaat u toohello `Inbound NAT Rules` tabblad Hallo load balancer voor Hallo scale set:

![ScaleSetPortalNatRules](./media/virtual-machine-scale-sets-portal-create/ScaleSetPortalNatRules.PNG)

U kunt deze NAT-regels met een VM in het Hallo-scale set tooeach verbinden. Bijvoorbeeld: voor een Windows-scale set, als er een NAT-regel op de binnenkomende poort 50000 u kan verbinding maken toothat machine via RDP op `<load-balancer-ip-address>:50000`. Voor een Linux-schaalset zou u verbinding met de opdracht Hallo `ssh -p 50000 <username>@<load-balancer-ip-address>`.

## <a name="next-steps"></a>Volgende stappen
Zie voor documentatie op hoe toodeploy scale ingesteld van Hallo CLI [deze documentatie](virtual-machine-scale-sets-cli-quick-create.md).

Zie voor documentatie over hoe toodeploy scale ingesteld van PowerShell, [deze documentatie](virtual-machine-scale-sets-windows-create.md).

Zie voor documentatie over hoe toodeploy schaal wordt ingesteld vanuit Visual Studio, [deze documentatie](virtual-machine-scale-sets-vs-create.md).

Bekijk voor algemene documentatie Hallo [documentatie overzichtspagina voor schaalsets](virtual-machine-scale-sets-overview.md).

Raadpleeg voor algemene informatie Hallo [belangrijkste startpagina voor schaalsets](https://azure.microsoft.com/services/virtual-machine-scale-sets/).


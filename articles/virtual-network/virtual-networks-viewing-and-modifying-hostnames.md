---
title: aaaViewing en hostnamen wijzigen | Microsoft Docs
description: Hoe tooview en wijzig de hostnamen voor Azure virtual machines web- en werkrollen voor naamomzetting
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
ms.assetid: c668cd8e-4e43-4d05-acc3-db64fa78d828
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/27/2016
ms.author: jdial
ms.openlocfilehash: 17d0dd7911754a94db3f37b924b4687da1c70aca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="viewing-and-modifying-hostnames"></a>Weergeven en wijzigen van hostnamen
tooallow uw rol exemplaren toobe waarnaar wordt verwezen door de hostnaam, moet u Hallo-waarde voor de hostnaam Hallo instellen in Hallo serviceconfiguratiebestand voor elke rol. U doet dit door toe te voegen Hallo gewenst host naam toohello **vmName** kenmerk Hallo **rol** element. waarde van Hallo Hallo **vmName** kenmerk wordt gebruikt als basis voor de hostnaam Hallo van elk rolexemplaar. Bijvoorbeeld, als **vmName** is *webrole* en er zijn drie exemplaren van deze rol, hostnamen Hallo Hallo exemplaren van *webrole0*, *webrole1* , en *webrole2*. U hoeft niet toospecify een hostnaam voor virtuele machines in het configuratiebestand hello, omdat de hostnaam Hallo voor een virtuele machine is ingevuld op basis van de naam van de virtuele machine Hallo. Zie voor meer informatie over het configureren van een Microsoft Azure-service [configuratieschema voor Azure-Service (.cscfg-bestand)](https://msdn.microsoft.com/library/azure/ee758710.aspx)

## <a name="viewing-hostnames"></a>Hostnamen weergeven
U kunt hostnamen Hallo van virtuele machines en rolexemplaren in een cloudservice weergeven via een van onderstaande Hallo hulpprogramma's.

### <a name="azure-portal"></a>Azure Portal
U kunt Hallo [Azure-portal](http://portal.azure.com) tooview Hallo hostnamen voor virtuele machines op de overzichtsblade Hallo voor een virtuele machine. Houd er rekening mee dat Hallo blade ziet u een waarde voor **naam** en **hostnaam**. Hoewel deze in eerste instantie Hallo wordt dezelfde hostnaam Hallo wijzigen Hallo-naam van Hallo virtuele machine of rolinstantie niet wijzigen.

Rolinstanties kunnen ook worden weergegeven in hello Azure-portal, maar wanneer u Hallo-exemplaren in een cloudservice, Hallo hostnaam niet wordt weergegeven. Ziet u een naam voor elk exemplaar, maar deze naam vertegenwoordigt geen Hallo-hostnaam.

### <a name="service-configuration-file"></a>Serviceconfiguratiebestand
U kunt Hallo serviceconfiguratiebestand voor een geïmplementeerde service downloaden van Hallo **configureren** blade van Hallo-service in hello Azure-portal. U kunt vervolgens zoeken Hallo **vmName** kenmerk voor Hallo **rolnaam** elementnaam toosee Hallo host. Houd er rekening mee dat deze hostnaam wordt gebruikt als basis voor de hostnaam Hallo van elk rolexemplaar. Bijvoorbeeld, als **vmName** is *webrole* en er zijn drie exemplaren van deze rol, hostnamen Hallo Hallo exemplaren van *webrole0*, *webrole1* , en *webrole2*.

### <a name="remote-desktop"></a>Extern bureaublad
Nadat u extern bureaublad (Windows), Windows PowerShell voor externe toegang (Windows) of SSH (Linux- en Windows-) verbindingen tooyour virtuele machines of rolinstanties inschakelt, kunt u Hallo-hostnaam van een actieve verbinding met extern bureaublad op verschillende manieren weergeven:

* Hostname Typ achter de opdrachtprompt Hallo of SSH-terminal.
* Typ ipconfig/alle achter Hallo opdracht prompt (alleen Windows).
* Weergave Hallo computernaam in Hallo systeem instellingen (alleen Windows).

### <a name="azure-service-management-rest-api"></a>Azure Service Management REST-API
Volg deze instructies in een REST-client:

1. Zorg ervoor dat u een client certificate tooconnect toohello Azure-portal. een clientcertificaat tooobtain stappen Hallo die zijn gepresenteerd in [hoe: downloaden en importeren publicatie-instellingen en abonnementsgegevens](https://msdn.microsoft.com/library/dn385850.aspx). 
2. Stel een header fragment x-ms-version met een waarde van 2013-11-01.
3. Een aanvraag verzenden in de volgende indeling Hallo: https://management.core.windows.net/\<subscrition-id\>/services/hostedservices/\<servicenaam\>? insluiten detail = true
4. Zoek naar Hallo **hostnaam** element voor elk **RoleInstance** element.

> [!WARNING]
> U kunt ook Hallo interne domeinachtervoegsel voor de cloudservice van Hallo REST-aanroep antwoord weergeven door te controleren Hallo **InternalDnsSuffix** element, of door het uitvoeren van ipconfig/alle vanaf een opdrachtprompt in een extern bureaublad-sessie (Windows) of door actieve cat /etc/resolv.conf van een SSH-terminal (Linux).
> 
> 

## <a name="modifying-a-hostname"></a>Een hostnaam wijzigen
U kunt Hallo-hostnaam voor elke virtuele machine of rolinstantie wijzigen door het uploaden van een configuratiebestand gewijzigde service of door het wijzigen van Hallo computer uit een extern bureaublad-sessie.

## <a name="next-steps"></a>Volgende stappen
[Naamomzetting (DNS)](virtual-networks-name-resolution-for-vms-and-role-instances.md)

[Het configuratieschema Azure-Service (.cscfg)](https://msdn.microsoft.com/library/windowsazure/ee758710.aspx)

[Azure Virtual Network-configuratieschema](http://go.microsoft.com/fwlink/?LinkId=248093)

[DNS-instellingen met behulp van de configuratiebestanden netwerk opgeven](virtual-networks-specifying-a-dns-settings-in-a-virtual-network-configuration-file.md)


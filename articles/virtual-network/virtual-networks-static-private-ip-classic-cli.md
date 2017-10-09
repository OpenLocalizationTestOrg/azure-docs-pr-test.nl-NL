---
title: "privé IP-adressen voor virtuele machines (klassiek) - Azure CLI 1.0 aaaConfigure | Microsoft Docs"
description: "Meer informatie over hoe tooconfigure privé IP-adressen voor virtuele machines (klassiek) met Azure-opdrachtregelinterface (CLI) 1.0 Hallo."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 17386acf-c708-4103-9b22-ff9bf04b778d
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 417a57181bcf5c2e6101bf3bdf63fc94ebc99df5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-private-ip-addresses-for-a-virtual-machine-classic-using-hello-azure-cli-10"></a>Privé IP-adressen voor een virtuele machine (klassiek) met behulp van Azure CLI 1.0 Hallo configureren

[!INCLUDE [virtual-networks-static-private-ip-selectors-classic-include](../../includes/virtual-networks-static-private-ip-selectors-classic-include.md)]

[!INCLUDE [virtual-networks-static-private-ip-intro-include](../../includes/virtual-networks-static-private-ip-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

In dit artikel bevat informatie over Hallo klassieke implementatiemodel. U kunt ook [een statisch privé IP-adres in Hallo Resource Manager-implementatiemodel beheren](virtual-networks-static-private-ip-arm-cli.md).

Hello Azure CLI Voorbeeldopdrachten onderstaande verwacht een eenvoudige omgeving al gemaakt. Als u toorun Hallo opdrachten wilt zoals ze worden weergegeven in dit document, eerst bouwen Hallo testomgeving beschreven in [een vnet maken](virtual-networks-create-vnet-classic-cli.md).

## <a name="how-toospecify-a-static-private-ip-address-when-creating-a-vm"></a>Hoe toospecify een statisch privé IP-adres bij het maken van een virtuele machine
een nieuwe virtuele machine met de naam toocreate *DNS01* in een nieuwe cloudservice met de naam *TestService* op basis van de bovenstaande Hallo scenario, als volgt te werk:

1. Als u Azure CLI nog nooit hebt gebruikt, raadpleegt u [installeren en configureren van Azure CLI Hallo](../cli-install-nodejs.md) en volg de instructies Hallo toohello punt waar u uw Azure-account en abonnement selecteren.
2. Voer Hallo **azure service maken** opdracht toocreate Hallo-cloudservice.
   
        azure service create TestService --location uscentral
   
    Verwachte uitvoer:
   
        info:    Executing command service create
        info:    Creating cloud service
        data:    Cloud service name TestService
        info:    service create command OK
3. Voer Hallo **azure virtuele machine maken** opdracht toocreate Hallo VM. Let op Hallo-waarde voor een statisch privé IP-adres. Hallo-lijst die wordt weergegeven na Hallo uitvoer wordt uitgelegd Hallo parameters die worden gebruikt.
   
        azure vm create -l centralus -n DNS01 -w TestVNet -S "192.168.1.101" TestService bd507d3a70934695bc2128e3e5a255ba__RightImage-Windows-2012R2-x64-v14.2 adminuser AdminP@ssw0rd
   
    Verwachte uitvoer:
   
        info:    Executing command vm create
        warn:    --vm-size has not been specified. Defaulting too"Small".
        info:    Looking up image bd507d3a70934695bc2128e3e5a255ba__RightImage-Windows-2012R2-x64-v14.2
        info:    Looking up virtual network
        info:    Looking up cloud service
        warn:    --location option will be ignored
        info:    Getting cloud service properties
        info:    Looking up deployment
        info:    Retrieving storage accounts
        info:    Creating VM
        info:    OK
        info:    vm create command OK
   
   * **-l (of --locatie)**. Azure-regio waar Hallo VM wordt gemaakt. In ons scenario *centralus*.
   * **-n (of--vm-naam)**. Naam van Hallo VM toobe gemaakt.
   * **-w (of--virtuele-netwerknaam)**. Naam van Hallo VNet waar Hallo VM wordt gemaakt. 
   * **-S (of--statisch ip-)**. Statisch privé IP-adres Hallo VM.
   * **TestService**. Naam van de cloudservice Hallo waar Hallo VM wordt gemaakt.
   * **bd507d3a70934695bc2128e3e5a255ba__RightImage-Windows-2012R2-x64-v14.2**. Afbeelding die wordt gebruikt toocreate hello VM.
   * **adminuser**. Lokale beheerder voor de virtuele machine van Windows hello.
   * **AdminP@ssw0rd**. Lokale administrator-wachtwoord voor de virtuele machine van Windows hello.

## <a name="how-tooretrieve-static-private-ip-address-information-for-a-vm"></a>Hoe de gegevens voor een VM voor het adres van tooretrieve statische privé-IP
tooview hello statische privé-IP adresgegevens voor Hallo VM gemaakt met bovenstaande Hallo-script uitvoeren hello Azure CLI-opdracht te volgen en bekijk Hallo-waarde voor *netwerk StaticIP*:

    azure vm static-ip show DNS01

Verwachte uitvoer:

    info:    Executing command vm static-ip show
    info:    Getting virtual machines
    data:    Network StaticIP "192.168.1.101"
    info:    vm static-ip show command OK

## <a name="how-tooremove-a-static-private-ip-address-from-a-vm"></a>Hoe tooremove een statisch privé IP-adres van een virtuele machine
tooremove hello statisch privé IP-adres toegevoegd toohello VM in Hallo script hierboven uitvoeren hello Azure CLI-opdracht te volgen:

    azure vm static-ip remove DNS01

Verwachte uitvoer:

    info:    Executing command vm static-ip remove
    info:    Getting virtual machines
    info:    Reading network configuration
    info:    Updating network configuration
    info:    vm static-ip remove command OK

## <a name="how-tooadd-a-static-private-ip-tooan-existing-vm"></a>Hoe een statisch privé IP-tooan tooadd bestaande VM
tooadd een statisch privé IP-adres toohello VM gemaakt Hallo script hierboven runt met de volgende opdracht:

    azure vm static-ip set DNS01 192.168.1.101

Verwachte uitvoer:

    info:    Executing command vm static-ip set
    info:    Getting virtual machines
    info:    Looking up virtual network
    info:    Reading network configuration
    info:    Updating network configuration
    info:    vm static-ip set command OK

## <a name="next-steps"></a>Volgende stappen
* Meer informatie over [gereserveerde openbare IP-adres](virtual-networks-reserved-public-ip.md) adressen.
* Meer informatie over [instantieniveau openbare IP (ILPIP)](virtual-networks-instance-level-public-ip.md) adressen.
* Raadpleeg Hallo [gereserveerde IP-REST-API's](https://msdn.microsoft.com/library/azure/dn722420.aspx).


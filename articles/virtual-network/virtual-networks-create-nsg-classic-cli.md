---
title: aaaHow toocreate nsg's bij het gebruik van de klassieke modus hello Azure CLI | Microsoft Docs
description: Meer informatie over hoe toocreate en nsg's implementeren in de klassieke modus hello Azure CLI gebruiken
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
tags: azure-service-management
ms.assetid: 17d98950-5fbb-4653-bef6-d822ab37541e
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2016
ms.author: jdial
ms.openlocfilehash: eb78861e10a0dd950bb2c3783ee957d1cce55016
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-nsgs-classic-in-hello-azure-cli"></a>Hoe toocreate nsg's (klassiek) in de Azure CLI Hallo
[!INCLUDE [virtual-networks-create-nsg-selectors-classic-include](../../includes/virtual-networks-create-nsg-selectors-classic-include.md)]

[!INCLUDE [virtual-networks-create-nsg-intro-include](../../includes/virtual-networks-create-nsg-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

In dit artikel bevat informatie over Hallo klassieke implementatiemodel. U kunt ook [nsg's maken in de Resource Manager-implementatiemodel Hallo](virtual-networks-create-nsg-arm-cli.md).

[!INCLUDE [virtual-networks-create-nsg-scenario-include](../../includes/virtual-networks-create-nsg-scenario-include.md)]

Hello Azure CLI Voorbeeldopdrachten onderstaande verwacht een eenvoudige omgeving al gemaakt op basis van Hallo bovenstaande scenario. Als u toorun Hallo opdrachten wilt zoals ze worden weergegeven in dit document, eerst Hallo testomgeving door bouwen [maken van een VNet](virtual-networks-create-vnet-classic-cli.md).

## <a name="how-toocreate-hello-nsg-for-hello-front-end-subnet"></a>Hoe toocreate NSG Hallo voor Hallo front-end-subnet
toocreate een NSG met de naam met de naam **NSG-FrontEnd** op basis van de bovenstaande scenario voor hello, Hallo volgende stappen.

1. Als u Azure CLI nog nooit hebt gebruikt, raadpleegt u [installeren en configureren van Azure CLI Hallo](../cli-install-nodejs.md) en volg de instructies Hallo toohello punt waar u uw Azure-account en abonnement selecteren.
2. Voer Hallo  **`azure config mode`**  tooswitch tooclassic opdrachtmodus, zoals hieronder wordt weergegeven.
   
        azure config mode asm
   
    Verwachte uitvoer:
   
        info:    New mode is asm
3. Voer Hallo  **`azure network nsg create`**  opdracht toocreate een NSG.
   
        azure network nsg create -l uswest -n NSG-FrontEnd
   
    Verwachte uitvoer:
   
        info:    Executing command network nsg create
        info:    Creating a network security group "NSG-FrontEnd"
        info:    Looking up hello network security group "NSG-FrontEnd"
        data:    Name                            : NSG-FrontEnd
        data:    Location                        : West US
        data:    Security group rules:
        data:    Name                               Source IP           Source Port  Destination IP   Destination Port  Protocol  Type      Action  Prior
        ity  Default
        data:    ---------------------------------  ------------------  -----------  ---------------  ----------------  --------  --------  ------  -----
        ---  -------
        data:    ALLOW VNET OUTBOUND                VIRTUAL_NETWORK     *            VIRTUAL_NETWORK  *                 *         Outbound  Allow   65000
             true   
        data:    ALLOW VNET INBOUND                 VIRTUAL_NETWORK     *            VIRTUAL_NETWORK  *                 *         Inbound   Allow   65000
             true   
        data:    ALLOW AZURE LOAD BALANCER INBOUND  AZURE_LOADBALANCER  *            *                *                 *         Inbound   Allow   65001
             true   
        data:    ALLOW INTERNET OUTBOUND            *                   *            INTERNET         *                 *         Outbound  Allow   65001
             true   
        data:    DENY ALL OUTBOUND                  *                   *            *                *                 *         Outbound  Deny    65500
             true   
        data:    DENY ALL INBOUND                   *                   *            *                *                 *         Inbound   Deny    65500
             true   
        info:    network nsg create command OK
   
    Parameters:
   
   * **-l (of --locatie)**. Azure-regio waar hello nieuwe NSG wordt gemaakt. In ons scenario *westus*.
   * **-n (of --naam)**. Naam voor Hallo nieuwe NSG. In ons scenario *NSG-FrontEnd*.
4. Voer Hallo  **`azure network nsg rule create`**  opdracht toocreate een regel waarmee toegang tooport 3389 (RDP) van Hallo Internet.
   
        azure network nsg rule create -a NSG-FrontEnd -n rdp-rule -c Allow -p Tcp -r Inbound -y 100 -f Internet -o * -e * -u 3389
   
    Verwachte uitvoer:
   
        info:    Executing command network nsg rule create
        info:    Looking up hello network security group "NSG-FrontEnd"
        info:    Creating a network security rule "rdp-rule"
        info:    Looking up hello network security group "NSG-FrontEnd"
        data:    Name                            : rdp-rule
        data:    Source address prefix           : INTERNET
        data:    Source Port                     : *
        data:    Destination address prefix      : *
        data:    Destination Port                : 3389
        data:    Protocol                        : TCP
        data:    Type                            : Inbound
        data:    Action                          : Allow
        data:    Priority                        : 100
        info:    network nsg rule create command OK
   
    Parameters:
   
   * **-a (of--nsg-naam)**. Naam van Hallo NSG in welke Hallo regel wordt gemaakt. In ons scenario *NSG-FrontEnd*.
   * **-n (of --naam)**. Naam voor de nieuwe regel Hallo. In ons scenario *rdp-regel*.
   * **-c (of--actie)**. Toegangsniveau voor Hallo regel (weigeren of toestaan).
   * **-p (of--protocol)**. Protocol (Tcp, Udp of *) voor Hallo regel.
   * **-r (of--type)**. Richting van de verbinding (inkomend of uitgaand).
   * **-y (of--prioriteit)**. Prioriteit voor het Hallo-regel.
   * **-f (of--bron adresvoorvoegsel)**. Voorvoegsel voor bronadres in CIDR- of met standaardlabels.
   * **-o (of--bronpoortbereik)**. Bronpoort, of een poortbereik.
   * **-e (of--bestemming adresvoorvoegsel)**. Voorvoegsel voor doeladres in CIDR- of met standaardlabels.
   * **-u (of--doelpoortbereik)**. Doelpoort, of een poortbereik.
5. Voer Hallo  **`azure network nsg rule create`**  opdracht toocreate een regel waarmee toegang tooport 80 (HTTP) van Hallo Internet.
   
        azure network nsg rule create -a NSG-FrontEnd -n web-rule -c Allow -p Tcp -r Inbound -y 200 -f Internet -o * -e * -u 80
   
    Verwachte putput:
   
        info:    Executing command network nsg rule create
        info:    Looking up hello network security group "NSG-FrontEnd"
        info:    Creating a network security rule "web-rule"
        info:    Looking up hello network security group "NSG-FrontEnd"
        data:    Name                            : web-rule
        data:    Source address prefix           : INTERNET
        data:    Source Port                     : *
        data:    Destination address prefix      : *
        data:    Destination Port                : 80
        data:    Protocol                        : TCP
        data:    Type                            : Inbound
        data:    Action                          : Allow
        data:    Priority                        : 200
        info:    network nsg rule create command OK
6. Voer Hallo  **`azure network nsg subnet add`**  opdracht toolink hello NSG toohello front-end-subnet.
   
        azure network nsg subnet add -a NSG-FrontEnd --vnet-name TestVNet --subnet-name FrontEnd
   
    Verwachte uitvoer:
   
        info:    Executing command network nsg subnet add
        info:    Looking up hello network security group "NSG-FrontEnd"
        info:    Looking up hello subnet "FrontEnd"
        info:    Looking up network configuration
        info:    Creating a network security group "NSG-FrontEnd"
        info:    network nsg subnet add command OK

## <a name="how-toocreate-hello-nsg-for-hello-back-end-subnet"></a>Hoe toocreate hello NSG voor Hallo terug subnet beëindigen
toocreate een NSG met de naam met de naam *NSG-back-end* op basis van de bovenstaande scenario voor hello, Hallo volgende stappen.

1. Voer Hallo  **`azure network nsg create`**  opdracht toocreate een NSG.
   
        azure network nsg create -l uswest -n NSG-BackEnd
   
    Verwachte uitvoer:
   
        info:    Executing command network nsg create
        info:    Creating a network security group "NSG-BackEnd"
        info:    Looking up hello network security group "NSG-BackEnd"
        data:    Name                            : NSG-BackEnd
        data:    Location                        : West US
        data:    Security group rules:
        data:    Name                               Source IP           Source Port  Destination IP   Destination Port  Protocol  Type      Action  Prior
        ity  Default
        data:    ---------------------------------  ------------------  -----------  ---------------  ----------------  --------  --------  ------  -----
        ---  -------
        data:    ALLOW VNET OUTBOUND                VIRTUAL_NETWORK     *            VIRTUAL_NETWORK  *                 *         Outbound  Allow   65000
             true   
        data:    ALLOW VNET INBOUND                 VIRTUAL_NETWORK     *            VIRTUAL_NETWORK  *                 *         Inbound   Allow   65000
             true   
        data:    ALLOW AZURE LOAD BALANCER INBOUND  AZURE_LOADBALANCER  *            *                *                 *         Inbound   Allow   65001
             true   
        data:    ALLOW INTERNET OUTBOUND            *                   *            INTERNET         *                 *         Outbound  Allow   65001
             true   
        data:    DENY ALL OUTBOUND                  *                   *            *                *                 *         Outbound  Deny    65500
             true   
        data:    DENY ALL INBOUND                   *                   *            *                *                 *         Inbound   Deny    65500
             true   
        info:    network nsg create command OK
   
    Parameters:
   
   * **-l (of --locatie)**. Azure-regio waar hello nieuwe NSG wordt gemaakt. In ons scenario *westus*.
   * **-n (of --naam)**. Naam voor Hallo nieuwe NSG. In ons scenario *NSG-FrontEnd*.
2. Voer Hallo  **`azure network nsg rule create`**  opdracht toocreate een regel waarmee toegang tooport 1433 (SQL) van Hallo front-end-subnet.
   
        azure network nsg rule create -a NSG-BackEnd -n sql-rule -c Allow -p Tcp -r Inbound -y 100 -f 192.168.1.0/24 -o * -e * -u 1433
   
    Verwachte uitvoer:
   
        info:    Executing command network nsg rule create
        info:    Looking up hello network security group "NSG-BackEnd"
        info:    Creating a network security rule "sql-rule"
        info:    Looking up hello network security group "NSG-BackEnd"
        data:    Name                            : sql-rule
        data:    Source address prefix           : 192.168.1.0/24
        data:    Source Port                     : *
        data:    Destination address prefix      : *
        data:    Destination Port                : 1433
        data:    Protocol                        : TCP
        data:    Type                            : Inbound
        data:    Action                          : Allow
        data:    Priority                        : 100
        info:    network nsg rule create command OK
3. Voer Hallo  **`azure network nsg rule create`**  opdracht toocreate een regel waarmee toegang toohello Internet weigert.
   
        azure network nsg rule create -a NSG-BackEnd -n web-rule -c Deny -p Tcp -r Outbound -y 200 -f * -o * -e Internet -u 80
   
    Verwachte putput:
   
        info:    Executing command network nsg rule create
        info:    Looking up hello network security group "NSG-BackEnd"
        info:    Creating a network security rule "web-rule"
        info:    Looking up hello network security group "NSG-BackEnd"
        data:    Name                            : web-rule
        data:    Source address prefix           : *
        data:    Source Port                     : *
        data:    Destination address prefix      : INTERNET
        data:    Destination Port                : 80
        data:    Protocol                        : TCP
        data:    Type                            : Outbound
        data:    Action                          : Deny
        data:    Priority                        : 200
        info:    network nsg rule create command OK
4. Voer Hallo  **`azure network nsg subnet add`**  opdracht toolink hello NSG toohello back-end subnet.
   
        azure network nsg subnet add -a NSG-BackEnd --vnet-name TestVNet --subnet-name BackEnd
   
    Verwachte uitvoer:
   
        info:    Executing command network nsg subnet add
        info:    Looking up hello network security group "NSG-BackEndX"
        info:    Looking up hello subnet "BackEnd"
        info:    Looking up network configuration
        info:    Creating a network security group "NSG-BackEndX"
        info:    network nsg subnet add command OK


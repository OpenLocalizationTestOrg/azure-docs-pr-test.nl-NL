---
title: Azure Redis-Cache met behulp van Azure CLI aaaManage | Microsoft Docs
description: Meer informatie over hoe tooinstall hello Azure CLI op elk platform hoe toouse het tooconnect tooyour Azure-account, en hoe toocreate en een Redis-cache beheren vanaf hello Azure CLI.
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: 964ff245-859d-4bc1-bccf-62e4b3c1169f
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: sdanie
ms.openlocfilehash: e8ee30090133e6b4edea93dcd13fd171e75989bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-and-manage-azure-redis-cache-using-hello-azure-command-line-interface-azure-cli"></a>Hoe toocreate en beheren van Azure Redis-Cache met behulp van hello Azure-opdrachtregelinterface (Azure CLI)
> [!div class="op_single_selector"]
> * [PowerShell](cache-howto-manage-redis-cache-powershell.md)
> * [Azure-CLI](cache-manage-cli.md)
>
>

Hello Azure CLI is een uitstekende manier toomanage uw Azure-infrastructuur van een willekeurig platform. Dit artikel ziet u hoe toocreate en beheren van uw Azure Redis-Cache-exemplaren die gebruikmaken van hello Azure CLI.

> [!NOTE]
> In dit artikel is van toepassing tooa eerdere versie van Azure CLI. Zie voor Hallo nieuwste Azure CLI 2.0 voorbeeldscripts [CLI van Azure Redis-cache-voorbeelden](cli-samples.md).
> 
> 

## <a name="prerequisites"></a>Vereisten
toocreate en beheren van Azure Redis-Cache-exemplaren die gebruikmaken van Azure CLI, moet u Hallo stappen te volgen.

* U moet een Azure-account hebben. Als u niet hebt, kunt u een [gratis account](https://azure.microsoft.com/pricing/free-trial/) in slechts enkele ogenblikken.
* [Hello Azure CLI installeren](../cli-install-nodejs.md).
* Verbinding maken met de Azure CLI-installatie met een persoonlijke Azure-account of met een werk of school Azure-account en zich aanmelden vanaf hello Azure CLI met Hallo `azure login` opdracht. toounderstand Hallo verschillen en kies, Zie [tooan Azure-abonnement van hello Azure-opdrachtregelinterface (Azure CLI) verbinding](../xplat-cli-connect.md).
* Voordat met een van de volgende opdrachten Hallo, hello Azure CLI in de modus Resource Manager-switch door te voeren Hallo `azure config mode arm` opdracht. Zie voor meer informatie [hello Azure CLI toomanage Azure gebruiken resources en resourcegroepen](../xplat-cli-azure-resource-manager.md).

## <a name="redis-cache-properties"></a>Redis-Cache-eigenschappen
Hallo worden volgende eigenschappen gebruikt bij het maken en bijwerken van Redis-Cache-exemplaren.

| Eigenschap | Switch | Beschrijving |
| --- | --- | --- |
| naam |-n,--naam |Naam van Hallo Redis-Cache. |
| resourcegroep |-g,--resourcegroep |Naam van Hallo resourcegroep. |
| location |-l,--locatie |Locatie toocreate cache. |
| Grootte |-z,--grootte |Grootte van Hallo Redis-Cache. Geldige waarden: [C0, C1, C2, C3, C4, C5, C6, P1, P2, P3, P4] |
| SKU |-x--sku |Redis SKU. Moet een van: [Basic, Standard, Premium] |
| EnableNonSslPort |-e,--enable-niet-ssl-poort |De eigenschap EnableNonSslPort Hallo Redis-Cache. Deze markering toevoegen als u wilt dat tooenable Hallo niet-SSL-poort voor uw cache |
| Configuratie van redis |-c,--redis-configuratie |Redis-configuratie. Geef een string in JSON-indeling van de van configuratiesleutels en waarden die hier. Indeling: ' {' ': "","": ""} " |
| Configuratie van redis |-f,--redis-configuratiebestand |Redis-configuratie. Hallo-pad van een bestand met configuratiesleutels en waarden die hier invoeren. Indeling voor de vermelding in het Hallo: {"": "","": ""} |
| Aantal shard |-r,--shard-telling |Het aantal Shards toocreate op een Cluster Premium Cache met clustering. |
| Virtual Network |-v,--virtueel netwerk |Bij het hosten van uw cache in een VNET Hallo exacte ARM bron-ID van Hallo virtueel netwerk toodeploy hello redis-cache in. Voorbeeld van de indeling: /subscriptions/{subid}/resourceGroups/{resourceGroupName}/Microsoft.ClassicNetwork/VirtualNetworks/vnet1 |
| sleuteltype |-t,--sleutel-type |Het type van de belangrijkste toorenew. Geldige waarden: [primaire, secundaire] |
| StaticIP |-p,--statisch ip-< statisch ip-> |Bij het hosten van uw cache in een VNET, geeft een uniek IP-adres in Hallo-subnet voor Hallo-cache. Als niet wordt opgegeven, wordt een gekozen voor u van Hallo subnet. |
| Subnet |t,--subnet<subnet> |Bij het hosten van uw cache in een VNET, geeft Hallo-naam van Hallo subnet in welke toodeploy Hallo-cache. |
| VirtualNetwork |-v,--virtueel netwerk < virtuele-netwerk > |Bij het hosten van uw cache in een VNET Hallo exacte ARM bron-ID van Hallo virtueel netwerk toodeploy hello redis-cache in. Voorbeeld van de indeling: /subscriptions/{subid}/resourceGroups/{resourceGroupName}/Microsoft.ClassicNetwork/VirtualNetworks/vnet1 |
| Abonnement |-s,--abonnement |Hallo abonnements-id. |

## <a name="see-all-redis-cache-commands"></a>Zie alle opdrachten voor Redis-Cache
toosee alle opdrachten voor Redis-Cache en de bijbehorende parameters gebruiken Hallo `azure rediscache -h` opdracht.

    C:\>azure rediscache -h
    help:    Commands toomanage your Azure Redis Cache(s)
    help:
    help:    Create a Redis Cache
    help:      rediscache create [--name <name> --resource-group <resource-group> --location <location> [options]]
    help:
    help:    Delete an existing Redis Cache
    help:      rediscache delete [--name <name> --resource-group <resource-group> ]
    help:
    help:    List all Redis Caches within your Subscription or Resource Group
    help:      rediscache list [options]
    help:
    help:    Show properties of an existing Redis Cache
    help:      rediscache show [--name <name> --resource-group <resource-group>]
    help:
    help:    Change settings of an existing Redis Cache
    help:      rediscache set [--name <name> --resource-group <resource-group> --redis-configuration <redis-configuration>/--redis-configuration-file <redisConfigurationFile>]
    help:
    help:    Renew hello authentication key for an existing Redis Cache
    help:      rediscache renew-key [--name <name> --resource-group <resource-group> ]
    help:
    help:    Lists Primary and Secondary key of an existing Redis Cache
    help:      rediscache list-keys [--name <name> --resource-group <resource-group>]
    help:
    help:    Options:
    help:      -h, --help  output usage information
    help:
    help:    Current Mode: arm (Azure Resource Management)

## <a name="create-a-redis-cache"></a>Een Redis-cache maken
toocreate Redis-Cache gebruiken Hallo volgende opdracht:

    azure rediscache create [--name <name> --resource-group <resource-group> --location <location> [options]]

Voor meer informatie over deze opdracht uitvoeren Hallo `azure rediscache create -h` opdracht.

    C:\>azure rediscache create -h
    help:    Create a Redis Cache
    help:
    help:    Usage: rediscache create [--name <name> --resource-group <resource-group> --location <location> [options]]
    help:
    help:    Options:
    help:      -h, --help                                               output usage information
    help:      -v, --verbose                                            use verbose output
    help:      -vv                                                      more verbose with debug output
    help:      --json                                                   use json output
    help:      -n, --name <name>                                        Name of hello Redis Cache.
    help:      -g, --resource-group <resource-group>                    Name of hello Resource Group
    help:      -l, --location <location>                                Location toocreate cache.
    help:      -z, --size <size>                                        Size of hello Redis Cache. Valid values: [C0, C1, C2, C3, C4, C5, C6, P1, P2, P3, P4]
    help:      -x, --sku <sku>                                          Redis SKU. Should be one of : [Basic, Standard, Premium]
    help:      -e, --enable-non-ssl-port                                EnableNonSslPort property of hello Redis Cache. Add this flag if you want tooenable hello Non SSL Port for your cache
    help:      -c, --redis-configuration <redis-configuration>          Redis Configuration. Enter a JSON formatted string of configuration keys and values here. Format:"{"<key1>":"<value1>","<key2>":"<value2>"}"
    help:      -f, --redis-configuration-file <redisConfigurationFile>  Redis Configuration. Enter hello path of a file containing configuration keys and values here. Format for hello file entry: {"<key1>":"<value1>","<key2>":"<value2>"}
    help:      -r, --shard-count <shard-count>                          Number of Shards toocreate on a Premium Cluster Cache
    help:      -v, --virtual-network <virtual-network>                  hello exact ARM resource ID of hello virtual network toodeploy hello redis cache in. Example format: /subscriptions/{subid}/resourceGroups/{resourceGroupName}/Microsoft.ClassicNetwork/VirtualNetworks/vnet1
    help:      -t, --subnet <subnet>                                    Required when deploying a redis cache inside an existing Azure Virtual Network
    help:      -p, --static-ip <static-ip>                              Required when deploying a redis cache inside an existing Azure Virtual Network
    help:      -s, --subscription <id>                                  hello subscription identifier
    help:
    help:    Current Mode: arm (Azure Resource Management)

## <a name="delete-an-existing-redis-cache"></a>Verwijderen van een bestaande Redis-Cache
toodelete Redis-Cache gebruiken Hallo volgende opdracht:

    azure rediscache delete [--name <name> --resource-group <resource-group> ]

Voor meer informatie over deze opdracht uitvoeren Hallo `azure rediscache delete -h` opdracht.

    C:\>azure rediscache delete -h
    help:    Delete an existing Redis Cache
    help:
    help:    Usage: rediscache delete [--name <name> --resource-group <resource-group> ]
    help:
    help:    Options:
    help:      -h, --help                             output usage information
    help:      -v, --verbose                          use verbose output
    help:      -vv                                    more verbose with debug output
    help:      --json                                 use json output
    help:      -n, --name <name>                      Name of hello Redis Cache.
    help:      -g, --resource-group <resource-group>  Name of hello Resource Group under which hello cache exists
    help:      -s, --subscription <subscription>      hello subscription identifier
    help:
    help:    Current Mode: arm (Azure Resource Management)

## <a name="list-all-redis-caches-within-your-subscription-or-resource-group"></a>Lijst van alle Redis-Caches binnen uw abonnement of resourcegroep
alle Redis-Caches binnen uw abonnement of resourcegroep, gebruikt u toolist Hallo volgende opdracht:

    azure rediscache list [options]

Voor meer informatie over deze opdracht uitvoeren Hallo `azure rediscache list -h` opdracht.

    C:\>azure rediscache list -h
    help:    List all Redis Caches within your Subscription or Resource Group
    help:
    help:    Usage: rediscache list [options]
    help:
    help:    Options:
    help:      -h, --help                             output usage information
    help:      -v, --verbose                          use verbose output
    help:      -vv                                    more verbose with debug output
    help:      --json                                 use json output
    help:      -g, --resource-group <resource-group>  Name of hello Resource Group
    help:      -s, --subscription <subscription>      hello subscription identifier
    help:
    help:    Current Mode: arm (Azure Resource Management)

## <a name="show-properties-of-an-existing-redis-cache"></a>Eigenschappen van een bestaande Redis-Cache weergeven
tooshow eigenschappen van een bestaande Redis-Cache, Hallo volgende opdracht gebruiken:

    azure rediscache show [--name <name> --resource-group <resource-group>]

Voor meer informatie over deze opdracht uitvoeren Hallo `azure rediscache show -h` opdracht.

    C:\>azure rediscache show -h
    help:    Show properties of an existing Redis Cache
    help:
    help:    Usage: rediscache show [--name <name> --resource-group <resource-group>]
    help:
    help:    Options:
    help:      -h, --help                             output usage information
    help:      -v, --verbose                          use verbose output
    help:      -vv                                    more verbose with debug output
    help:      --json                                 use json output
    help:      -n, --name <name>                      Name of hello Redis Cache.
    help:      -g, --resource-group <resource-group>  Name of hello Resource Group
    help:      -s, --subscription <subscription>      hello subscription identifier
    help:
    help:    Current Mode: arm (Azure Resource Management)

<a name="scale"></a>

## <a name="change-settings-of-an-existing-redis-cache"></a>Instellingen van een bestaande Redis-Cache wijzigen
toochange instellingen van een bestaande Redis-Cache, gebruik Hallo volgende opdracht:

    azure rediscache set [--name <name> --resource-group <resource-group> --redis-configuration <redis-configuration>/--redis-configuration-file <redisConfigurationFile>]

Voor meer informatie over deze opdracht uitvoeren Hallo `azure rediscache set -h` opdracht.

    C:\>azure rediscache set -h
    help:    Change settings of an existing Redis Cache
    help:
    help:    Usage: rediscache set [--name <name> --resource-group <resource-group> --redis-configuration <redis-configuration>/--redis-configuration-file <redisConfigurationFile>]
    help:
    help:    Options:
    help:      -h, --help                                               output usage information
    help:      -v, --verbose                                            use verbose output
    help:      -vv                                                      more verbose with debug output
    help:      --json                                                   use json output
    help:      -n, --name <name>                                        Name of hello Redis Cache.
    help:      -g, --resource-group <resource-group>                    Name of hello Resource Group
    help:      -c, --redis-configuration <redis-configuration>          Redis Configuration. Enter a JSON formatted string of configuration keys and values here.
    help:      -f, --redis-configuration-file <redisConfigurationFile>  Redis Configuration. Enter hello path of a file containing configuration keys and values here.
    help:      -s, --subscription <subscription>                        hello subscription identifier
    help:
    help:    Current Mode: arm (Azure Resource Management)

## <a name="renew-hello-authentication-key-for-an-existing-redis-cache"></a>Hallo-verificatiesleutel vernieuwen voor een bestaande Redis-Cache
toorenew Hallo-verificatiesleutel voor een bestaande Redis-Cache, gebruik Hallo volgende opdracht:

    azure rediscache renew-key [--name <name> --resource-group <resource-group> --key-type <key-type>]

Geef `Primary` of `Secondary` voor `key-type`.

Voor meer informatie over deze opdracht uitvoeren Hallo `azure rediscache renew-key -h` opdracht.

    C:\>azure rediscache renew-key -h
    help:    Renew hello authentication key for an existing Redis Cache
    help:
    help:    Usage: rediscache renew-key [--name <name> --resource-group <resource-group> ]
    help:
    help:    Options:
    help:      -h, --help                             output usage information
    help:      -v, --verbose                          use verbose output
    help:      -vv                                    more verbose with debug output
    help:      --json                                 use json output
    help:      -n, --name <name>                      Name of hello Redis Cache.
    help:      -g, --resource-group <resource-group>  Name of hello Resource Group under which cache exists
    help:      -t, --key-type <key-type>              type of key toorenew. Valid values are: 'Primary', 'Secondary'.
    help:      -s, --subscription <subscription>      hello subscription identifier
    help:
    help:    Current Mode: arm (Azure Resource Management)

## <a name="list-primary-and-secondary-keys-of-an-existing-redis-cache"></a>Lijst met primaire en secundaire sleutels van een bestaande Redis-Cache
de primaire en secundaire sleutels toolist van een bestaande Redis-Cache, Hallo volgende opdracht gebruiken:

    azure rediscache list-keys [--name <name> --resource-group <resource-group>]

Voor meer informatie over deze opdracht uitvoeren Hallo `azure rediscache list-keys -h` opdracht.

    C:\>azure rediscache list-keys -h
    help:    Lists Primary and Secondary key of an existing Redis Cache
    help:
    help:    Usage: rediscache list-keys [--name <name> --resource-group <resource-group>]
    help:
    help:    Options:
    help:      -h, --help                             output usage information
    help:      -v, --verbose                          use verbose output
    help:      -vv                                    more verbose with debug output
    help:      --json                                 use json output
    help:      -n, --name <name>                      Name of hello Redis Cache.
    help:      -g, --resource-group <resource-group>  Name of hello Resource Group under which Cache exists
    help:      -s, --subscription <subscription>      hello subscription identifier
    help:
    help:    Current Mode: arm (Azure Resource Management)

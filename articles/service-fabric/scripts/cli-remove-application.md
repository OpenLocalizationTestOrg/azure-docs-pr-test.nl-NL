---
title: Service Fabric CLI verwijderen voorbeeldscript aaaAzure
description: Een toepassing verwijderen van een Azure Service Fabric-cluster met behulp van hello Azure Service Fabric CLI
services: service-fabric
documentationcenter: 
author: thraka
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: service-fabric
ms.workload: multiple
ms.devlang: na
ms.topic: article
ms.date: 08/22/2017
ms.author: adegeo
ms.custom: mvc
ms.openlocfilehash: 3ccefd4a04c5b7af71a2f959e11da6e402f25881
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="remove-an-application-from-a-service-fabric-cluster"></a>Een toepassing verwijderen van een Service Fabric-cluster

Dit voorbeeldscript wordt verwijderd van een actief exemplaar van de Service Fabric-toepassing, heft de registratie van een toepassingstype en -versie van het Hallo-cluster.  Verwijderen van het Hallo-toepassingsexemplaar verwijdert tevens alle Hallo service-exemplaren die zijn gekoppeld aan de toepassing uitgevoerd. Hallo toepassingsbestanden worden vervolgens verwijderd uit de installatiekopieopslag Hallo. 

Installeer zo nodig Hallo [Service Fabric CLI](../service-fabric-cli.md).

## <a name="sample-script"></a>Voorbeeld van een script

[!code-sh[main](../../../cli_scripts/service-fabric/remove-application/remove-application.sh "Remove an application from a cluster")]

## <a name="next-steps"></a>Volgende stappen

Zie voor meer informatie, Hallo [Service Fabric CLI documentatie](../service-fabric-cli.md).

Extra Service Fabric CLI steekproeven voor de Azure Service Fabric vindt u in Hallo [Service Fabric CLI voorbeelden](../samples-cli.md).

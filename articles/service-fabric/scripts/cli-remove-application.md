---
title: Azure Service Fabric CLI-voorbeeldscript verwijderen
description: Een toepassing verwijderen van een Azure Service Fabric-cluster met de Azure Service Fabric-CLI
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
ms.openlocfilehash: d86f195d2c37a71e476c5ba4eec040dd46931d23
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="remove-an-application-from-a-service-fabric-cluster"></a>Een toepassing verwijderen van een Service Fabric-cluster

Dit voorbeeldscript wordt verwijderd van een actief exemplaar van de Service Fabric-toepassing, heft de registratie van een toepassingstype en -versie van het cluster.  Het toepassingsexemplaar ook verwijdert alle uitgevoerd service-exemplaren die zijn gekoppeld aan die toepassing. De toepassingsbestanden worden vervolgens verwijderd uit de image store. 

Installeer zo nodig de [Service Fabric CLI](../service-fabric-cli.md).

## <a name="sample-script"></a>Voorbeeld van een script

[!code-sh[belangrijkste](../../../cli_scripts/service-fabric/remove-application/remove-application.sh "een toepassing verwijderen uit een cluster")]

## <a name="next-steps"></a>Volgende stappen

Zie voor meer informatie de [Service Fabric CLI documentatie](../service-fabric-cli.md).

Extra Service Fabric CLI steekproeven voor de Azure Service Fabric vindt u in de [Service Fabric CLI voorbeelden](../samples-cli.md).

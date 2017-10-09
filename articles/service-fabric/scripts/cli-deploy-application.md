---
title: Service Fabric CLI implementeren voorbeeldscript aaaAzure
description: Een toepassing tooan Azure Service Fabric-cluster met behulp van Azure Service Fabric CLI Hallo implementeren
services: service-fabric
documentationcenter: 
author: Thraka
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
ms.openlocfilehash: aaec7042a4fd7ed32ad706cde70361f23d18fb48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-application-tooa-service-fabric-cluster"></a>Een toepassing tooa Service Fabric-cluster implementeren

Dit voorbeeldscript gekopieerd van een toepassing pakket tooa cluster image store, registreert Hallo toepassingstype in Hallo cluster en maakt een toepassingsexemplaar van toepassingstype Hallo. Alle services die standaard worden ook op dit moment gemaakt.

Installeer zo nodig Hallo [Service Fabric CLI](../service-fabric-cli.md).

## <a name="sample-script"></a>Voorbeeld van een script

[!code-sh[main](../../../cli_scripts/service-fabric/deploy-application/deploy-application.sh "Deploy an application tooa cluster")]

## <a name="clean-up-deployment"></a>Opschonen van implementatie

Wanneer u klaar bent, Hallo [verwijderen](cli-remove-application.md) script gebruikte tooremove Hallo toepassing kan worden. Hallo verwijderen script Hallo toepassingsexemplaar verwijdert, heft de registratie van toepassingstype Hallo en Hallo toepassingspakket verwijdert uit de image store.

## <a name="next-steps"></a>Volgende stappen

Zie voor meer informatie, Hallo [Service Fabric CLI documentatie](../service-fabric-cli.md).

Extra Service Fabric CLI steekproeven voor de Azure Service Fabric vindt u in Hallo [Service Fabric CLI voorbeelden](../samples-cli.md).

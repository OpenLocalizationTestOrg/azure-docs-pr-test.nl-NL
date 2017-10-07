---
title: aaaAuthenticate met een Azure container registry | Microsoft Docs
description: Hoe toolog in tooan Azure container register met een Azure Active Directory service-principal of een beheerdersaccount te gebruiken
services: container-registry
documentationcenter: 
author: stevelas
manager: balans
editor: cristyg
tags: 
keywords: 
ms.assetid: 128a937a-766a-415b-b9fc-35a6c2f27417
ms.service: container-registry
ms.devlang: na
ms.topic: how-to-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/24/2017
ms.author: stevelas
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a0b0462e8432b2567689debca322e2426baa7fa2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="authenticate-with-a-private-docker-container-registry"></a>Verificatie met een persoonlijke Docker-container register
toowork met afbeeldingen in het register van een Azure container container u zich aanmelden met behulp van Hallo `docker login` opdracht. U kunt aanmelden met behulp van een  **[Azure Active Directory-service-principal](../active-directory/active-directory-application-objects.md)**  of een register-specifieke **beheerdersaccount**. Dit artikel vindt meer informatie over deze identiteiten.



## <a name="service-principal"></a>Service-principal

U kunt [toewijzen van een service-principal](container-registry-get-started-azure-cli.md#assign-a-service-principal) tooyour register en deze gebruiken voor eenvoudige Docker-authenticatie. Met behulp van een service-principal wordt aanbevolen voor de meeste scenario's. Hallo app-ID en wachtwoord van Hallo service principal toohello `docker login` opdracht, zoals wordt weergegeven in Hallo voorbeeld te volgen:

```
docker login myregistry.azurecr.io -u xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx -p myPassword
```

Nadat u bent aangemeld, Docker in de cache opgeslagen referenties hello, dus u hoeft tooremember Hallo app-ID.

> [!TIP]
> Als u wilt, kunt u Hallo-wachtwoord van een service-principal opnieuw genereren door het uitvoeren van Hallo `az ad sp reset-credentials` opdracht.
>


Service-principals toestaan [toegangsgroepen op basis van](../active-directory/role-based-access-control-configure.md) tooa register. Beschikbare rollen zijn:
  * Lezer (alleen pull-toegang).
  * Inzender (pull-abonnementen en push).
  * Eigenaar (pull-, push- en toewijzen rollen tooother gebruikers).

Anonieme toegang is niet beschikbaar op Azure Container registers. U kunt gebruiken voor openbare afbeeldingen [Docker Hub](https://docs.docker.com/docker-hub/).

U kunt meerdere service-principals tooa register, waarmee u toegang tot toodefine voor verschillende gebruikers of toepassingen kunt toewijzen. Service-principals ook inschakelen 'headless' connectiviteit tooa register in ontwikkelaar of DevOps-scenario's zoals Hallo volgen voorbeelden:

  * Containerimplementaties van een register tooorchestration systemen zoals DC/OS, Docker Swarm en Kubernetes. U kunt ook pull-container registers toorelated Azure-services zoals [Containerservice](../container-service/index.yml), [App Service](../app-service/index.md), [Batch](../batch/index.md), [Service Fabric](/azure/service-fabric/), en andere.

  * Continue integratie en implementatie-oplossingen (zoals Visual Studio Team Services of Jenkins) die container images maken en toepassen tooa register.





## <a name="admin-account"></a>Beheerdersaccount
Een beheerdersaccount opgehaald met elke register die u maakt, automatisch gemaakt. Hallo-account is standaard uitgeschakeld, maar u kunt deze inschakelen en Hallo referenties beheren, bijvoorbeeld via Hallo [portal](container-registry-get-started-portal.md#manage-registry-settings) of met behulp van Hallo [Azure CLI 2.0 opdrachten](container-registry-get-started-azure-cli.md#manage-admin-credentials). Elke beheerdersaccount wordt geleverd met twee wachtwoorden, die beide kunnen worden hersteld. Hallo twee wachtwoorden kunnen u toomaintain verbindingen toohello register met een wachtwoord tijdens het genereren van Hallo andere wachtwoord. Als het Hallo-account is ingeschakeld, kunt u doorgeven Hallo-gebruikersnaam en een wachtwoord toohello `docker login` opdracht voor basisverificatie toohello register. Bijvoorbeeld:

```
docker login myregistry.azurecr.io -u myAdminName -p myPassword1
```

> [!IMPORTANT]
> Hallo-beheerdersaccount is ontworpen voor een register één gebruiker tooaccess hello, hoofdzakelijk voor testdoeleinden. Het is niet raadzaam tooshare Hallo beheerder accountreferenties met andere gebruikers. Alle gebruikers worden weergegeven als een enkele gebruiker toohello-register. Hiermee schakelt u toegang tot het register voor alle gebruikers die gebruikmaken van Hallo referenties wijzigen of dit account uitschakelen.
>


### <a name="next-steps"></a>Volgende stappen
* [Uw eerste installatiekopie met behulp van Docker CLI Hallo push](container-registry-get-started-docker-cli.md).
* Zie voor meer informatie over verificatie in voorbeeld van het register van de Container Hallo Hallo [blogbericht](https://blogs.msdn.microsoft.com/stevelasker/2016/11/17/azure-container-registry-user-accounts/).

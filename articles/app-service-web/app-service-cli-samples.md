---
title: aaaAzure steekproeven CLI - App Service | Microsoft Docs
description: Voorbeelden van Azure CLI - App Service
services: app-service
documentationcenter: app-service
author: syntaxc4
manager: erikre
editor: ggailey777
tags: azure-service-management
ms.assetid: 53e6a15a-370a-48df-8618-c6737e26acec
ms.service: app-service
ms.devlang: na
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: app-service
ms.date: 03/08/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: a943ccffb59c5d30a44cf1ce513fd2eac46101f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cli-samples"></a>Voorbeelden van Azure CLI

Hallo bevat volgende tabel koppelingen toobash scripts gebouwd met behulp van hello Azure CLI.

| | |
|-|-|
|**App maken**||
| [Een web-app maken en code implementeren vanuit GitHub](./scripts/app-service-cli-deploy-github.md?toc=%2fcli%2fazure%2ftoc.json)| Een Azure-web-app maakt en implementeert de code van een openbare GitHub-opslagplaats. |
| [Een web-app maken met doorlopende implementatie vanuit GitHub](./scripts/app-service-cli-continuous-deployment-github.md?toc=%2fcli%2fazure%2ftoc.json)| Hiermee maakt een Azure-web-app met continue publiceren vanaf een GitHub-opslagplaats die u bezit. |
| [Een web-app maken en code implementeren vanuit een lokale Git-opslagplaats](./scripts/app-service-cli-deploy-local-git.md?toc=%2fcli%2fazure%2ftoc.json) | Een Azure-web-app maakt en configureert u code push van een lokale Git-opslagplaats. |
| [Een web-app maken en implementeren van code tooa staging-omgeving](./scripts/app-service-cli-deploy-staging-environment.md?toc=%2fcli%2fazure%2ftoc.json) | Een Azure-web-app maakt met een implementatiesleuf voor het Faseren van codewijzigingen. |
| [Een ASP.NET Core-web-app maken in een Docker-container](./scripts/app-service-cli-linux-docker-aspnetcore.md?toc=%2fcli%2fazure%2ftoc.json)| Een Azure-web-app maakt op Linux en laadt een Docker-afbeelding van Docker-Hub. |
|**App configureren**||
| [Toewijzen van een aangepast domein tooa web-app](./scripts/app-service-cli-configure-custom-domain.md?toc=%2fcli%2fazure%2ftoc.json)| Een Azure-web-app maakt en een aangepast domein naam tooit wordt toegewezen. |
| [Binden van een aangepaste SSL-certificaat tooa web-app](./scripts/app-service-cli-configure-ssl-certificate.md?toc=%2fcli%2fazure%2ftoc.json)| Een Azure-web-app maakt en koppelt Hallo SSL-certificaat van een aangepast domein naam tooit. |
|**Scale-app**||
| [Een web-app handmatig schalen](./scripts/app-service-cli-scale-manual.md?toc=%2fcli%2fazure%2ftoc.json) | Een Azure-web-app maakt en over 2 exemplaren op schaal. |
| [Een web-app wereldwijd schalen met een architectuur voor hoge beschikbaarheid](./scripts/app-service-cli-scale-high-availability.md?toc=%2fcli%2fazure%2ftoc.json) | Maakt twee Azure-web-apps in twee verschillende geografische regio's en maakt u ze beschikbaar zijn via één eindpunt met behulp van Azure Traffic Manager. |
|**Verbinding maken met app-tooresources**||
| [Verbinding maken met een web-app tooa SQL-Database](./scripts/app-service-cli-app-service-sql.md?toc=%2fcli%2fazure%2ftoc.json)| Maakt een Azure-web-app en een SQL-database en vervolgens voegt Hallo tekenreeks toohello appinstellingen voor de databaseverbinding. |
| [Verbinding maken met een web-app tooa storage-account](./scripts/app-service-cli-app-service-storage.md?toc=%2fcli%2fazure%2ftoc.json)| Hiermee maakt u een Azure-web-app en een opslagaccount en vervolgens voegt Hallo opslag toohello app verbindingstekenreeksinstellingen. |
| [Verbinding maken met een web-app tooa redis-cache](./scripts/app-service-cli-app-service-redis.md?toc=%2fcli%2fazure%2ftoc.json) | Hiermee maakt u een Azure-web-app en een redis-cache en vervolgens voegt Hallo redis details toohello app verbindingsinstellingen.) |
| [Verbinding maken met een web-app tooCosmos DB](./scripts/app-service-cli-app-service-documentdb.md?toc=%2fcli%2fazure%2ftoc.json) | Maakt een Azure-web-app en een Cosmos-database en vervolgens voegt Hallo Cosmos DB details toohello app verbindingsinstellingen. |
|**App controleren**||
| [Een web-app bewaken met webserverlogboeken](./scripts/app-service-cli-monitor.md?toc=%2fcli%2fazure%2ftoc.json) | Een Azure-web-app maakt, schakelt logboekregistratie voor het en downloadt Hallo logboeken tooyour lokale computer. |
| | |
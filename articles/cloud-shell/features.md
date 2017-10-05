---
title: Functies van Azure Cloud-Shell (Preview) | Microsoft Docs
description: Overzicht van de functies van Azure Cloud Shell
services: 
documentationcenter: 
author: jluk
manager: timlt
tags: azure-resource-manager
ms.assetid: 
ms.service: azure
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: juluk
ms.openlocfilehash: 67f03d5857e37b253ac57536e289b5468d69e9b5
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="features-and-tools-for-azure-cloud-shell"></a>Functies en hulpprogramma's voor Azure-Cloud-Shell
Azure Cloud-Shell is een browser gebaseerde shell-ervaring te beheren en ontwikkelen van Azure-resources.

Cloud-Shell biedt een shell browser toegankelijk, vooraf is geconfigureerd voor het beheren van Azure-resources zonder de overhead voor het installeren van versies, en onderhouden van een machine.

Cloud-Shell richt machines op basis van per aanvraag en als gevolg hiervan MACHINESTATUS niet behouden over de sessies. Aangezien Cloud Shell is gebouwd voor interactieve sessies, wordt de houders automatisch opgeheven na 20 minuten van inactiviteit shell.

## <a name="bash-in-cloud-shell"></a>In de Cloud-Shell Bash
### <a name="tools"></a>Hulpprogramma's
|Category   |Naam   |
|---|---|
|Linux shell-interpreter|Bash<br> servicel               |
|Azure-hulpprogramma 's            |[Azure CLI 2.0](https://github.com/Azure/azure-cli) en [1.0](https://github.com/Azure/azure-xplat-cli)<br> [AzCopy](https://docs.microsoft.com/azure/storage/storage-use-azcopy)<br> [Batch Shipyard](https://github.com/Azure/batch-shipyard)     |
|Teksteditors           |VIM<br> nano<br> emacs       |
|Resourcebeheer         |GIT                    |
|Hulpprogramma's van build            |Maken<br> maven<br> npm<br> PIP         |
|Containers             |[Docker CLI](https://github.com/docker/cli)/[Docker-Machine](https://github.com/docker/machine)<br> [Kubectl](https://kubernetes.io/docs/user-guide/kubectl-overview/)<br> [Concept](https://github.com/Azure/draft)<br> [DC/OS CLI](https://github.com/dcos/dcos-cli)         |
|Databases              |MySQL-client<br> PostgreSql-client<br> [Sqlcmd-hulpprogramma](https://docs.microsoft.com/sql/tools/sqlcmd-utility)<br> [MSSQL-scripts](https://github.com/Microsoft/sql-xplat-cli) |
|Overige                  |iPython Client<br> [Cloud Foundry CLI](https://github.com/cloudfoundry/cli)<br> |

### <a name="language-support"></a>Taalondersteuning
|Taal   |Versie   |
|---|---|
|.NET       |1.01       |
|Aan de slag         |1.7        |
|Java       |1.8        |
|Node.js    |6.9.4      |
|Python     |2.7 en 3.5 (standaard)|

## <a name="secure-automatic-authentication"></a>Automatische verificatie beveiligen
Cloud-Shell verifieert veilig en automatisch accounttoegang voor Azure CLI 2.0.

## <a name="azure-files-persistence"></a>Azure bestanden persistentie
Omdat Cloud Shell is toegewezen op basis van gebruik van een tijdelijke machine per aanvraag, bestanden buiten de status van uw $Home en de machine zijn niet permanent opgeslagen over de sessies.
Om te blijven behouden bestanden over de sessies, helpt Cloud Shell u bij het koppelen van een Azure-bestandsshare op de eerste keer opstarten.
Wanneer u klaar Cloud Shell wordt automatisch koppelen van uw opslag voor alle toekomstige sessies.

[Meer informatie over de Azure-bestandsshares gekoppeld aan Cloud Shell.](persisting-shell-storage.md)

## <a name="next-steps"></a>Volgende stappen
[Cloud-Shell Quick Start](quickstart.md) <br>
[Meer informatie over Azure CLI 2.0](https://docs.microsoft.com/cli/azure/) <br>
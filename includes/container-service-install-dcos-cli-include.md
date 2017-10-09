---
title: aaaInstall hello DC/OS CLI | Microsoft Docs
description: Hallo DC/OS CLI installeren.
services: container-service
documentationcenter: 
author: rgardler
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: Containers, Micro-services, DC/OS, Azure
ms.service: container-service
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/10/2016
ms.author: rogardle
ms.openlocfilehash: b077c05beff9a5638486ea5efe9df31089e32701
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
> [!NOTE]
> Dit is voor als u met op DC/OS gebaseerde ACS-clusters werkt. Er is geen toodo moet dit voor Swarm gebaseerde ACS-clusters.
> 
> 

Eerst [tooyour DC/OS gebaseerde ACS-cluster verbinding](../articles/container-service/container-service-connect.md). Als u dit hebt gedaan, kunt u Hallo DC/OS CLI installeren op de clientcomputer met onderstaande Hallo-opdrachten:

```bash
sudo pip install virtualenv
mkdir dcos && cd dcos
wget https://raw.githubusercontent.com/mesosphere/dcos-cli/master/bin/install/install-optout-dcos-cli.sh
chmod +x install-optout-dcos-cli.sh
./install-optout-dcos-cli.sh . http://localhost --add-path yes
```

Als u een oude versie van Python gebruikt, is het mogelijk dat u een aantal 'InsecurePlatformWarnings'-waarschuwingen krijgt te zien. U kunt deze gewoon negeren.

In de volgorde tooget gestart zonder de shell opnieuw te starten, uitvoeren:

```bash
source ~/.bashrc
```

De stap is niet nodig als u nieuwe shells start.

U kunt nu controleren die Hallo die CLI is geïnstalleerd:

```bash
dcos --help
```
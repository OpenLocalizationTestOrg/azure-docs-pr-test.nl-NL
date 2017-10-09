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
> <span data-ttu-id="63c3c-104">Dit is voor als u met op DC/OS gebaseerde ACS-clusters werkt.</span><span class="sxs-lookup"><span data-stu-id="63c3c-104">This is for working with DC/OS-based ACS clusters.</span></span> <span data-ttu-id="63c3c-105">Er is geen toodo moet dit voor Swarm gebaseerde ACS-clusters.</span><span class="sxs-lookup"><span data-stu-id="63c3c-105">There is no need toodo this for Swarm-based ACS clusters.</span></span>
> 
> 

<span data-ttu-id="63c3c-106">Eerst [tooyour DC/OS gebaseerde ACS-cluster verbinding](../articles/container-service/container-service-connect.md).</span><span class="sxs-lookup"><span data-stu-id="63c3c-106">First, [connect tooyour DC/OS-based ACS cluster](../articles/container-service/container-service-connect.md).</span></span> <span data-ttu-id="63c3c-107">Als u dit hebt gedaan, kunt u Hallo DC/OS CLI installeren op de clientcomputer met onderstaande Hallo-opdrachten:</span><span class="sxs-lookup"><span data-stu-id="63c3c-107">Once you have done this, you can install hello DC/OS CLI on your client machine with hello commands below:</span></span>

```bash
sudo pip install virtualenv
mkdir dcos && cd dcos
wget https://raw.githubusercontent.com/mesosphere/dcos-cli/master/bin/install/install-optout-dcos-cli.sh
chmod +x install-optout-dcos-cli.sh
./install-optout-dcos-cli.sh . http://localhost --add-path yes
```

<span data-ttu-id="63c3c-108">Als u een oude versie van Python gebruikt, is het mogelijk dat u een aantal 'InsecurePlatformWarnings'-waarschuwingen krijgt te zien.</span><span class="sxs-lookup"><span data-stu-id="63c3c-108">If you are using an old version of Python, you may notice some "InsecurePlatformWarnings".</span></span> <span data-ttu-id="63c3c-109">U kunt deze gewoon negeren.</span><span class="sxs-lookup"><span data-stu-id="63c3c-109">You can safely ignore these.</span></span>

<span data-ttu-id="63c3c-110">In de volgorde tooget gestart zonder de shell opnieuw te starten, uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="63c3c-110">In order tooget started without restarting your shell, run:</span></span>

```bash
source ~/.bashrc
```

<span data-ttu-id="63c3c-111">De stap is niet nodig als u nieuwe shells start.</span><span class="sxs-lookup"><span data-stu-id="63c3c-111">This step will not be necessary when you start new shells.</span></span>

<span data-ttu-id="63c3c-112">U kunt nu controleren die Hallo die CLI is geïnstalleerd:</span><span class="sxs-lookup"><span data-stu-id="63c3c-112">Now you can confirm that hello CLI is installed:</span></span>

```bash
dcos --help
```
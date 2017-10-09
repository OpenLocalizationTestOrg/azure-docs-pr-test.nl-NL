---
title: een Docker-Host met VirtualBox aaaConfigure | Microsoft Docs
description: Stapsgewijze instructies tooconfigure standaard Docker-exemplaar met behulp van Docker-Machine en VirtualBox
services: azure-container-service
documentationcenter: na
author: mlearned
manager: douge
editor: 
ms.assetid: 0b1335a2-7720-42a8-8260-4e06fc00c9f6
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 06/08/2016
ms.author: mlearned
ms.openlocfilehash: 1df2da4482444a803d05e413e019edcc57269062
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-docker-host-with-virtualbox"></a>Een Docker-Host met VirtualBox configureren
## <a name="overview"></a>Overzicht
In dit artikel begeleidt u bij het configureren van een standaard Docker-exemplaar met behulp van Docker-Machine en VirtualBox. Als u Hallo [Docker voor Windows beta](http://beta.docker.com/), deze configuratie is niet nodig.

## <a name="prerequisites"></a>Vereisten
Hallo moeten volgende hulpprogramma's toobe geïnstalleerd.

* [Docker-werkset](https://www.docker.com/products/overview#/docker_toolbox)

## <a name="configuring-hello-docker-client-with-windows-powershell"></a>Hallo Docker-client configureren met Windows PowerShell
tooconfigure een Docker-client gewoon opent u Windows PowerShell en Voer Hallo stappen te volgen:

1. Maak een standaardexemplaar van de docker-host.
   
    ```PowerShell
    docker-machine create --driver virtualbox default
    ```
2. Controleer of het standaardexemplaar Hallo geconfigureerd en actief zijn. (U ziet een exemplaar met de naam 'default' uitgevoerd.
   
    ```PowerShell
    docker-machine ls 
    ```
   
    ![docker-machine ls-uitvoer][0]
3. Als de huidige host Hallo instellen en configureren van de shell.
   
    ```PowerShell
    docker-machine env default | Invoke-Expression
    ```
4. Hallo active Docker-containers worden weergegeven. Hallo lijst mag niet leeg zijn.
   
    ```PowerShell
    docker ps
    ```
   
    ![docker ps-uitvoer][1]

> [!NOTE]
> Telkens wanneer die u opnieuw opstarten van uw ontwikkelcomputer, moet u toorestart uw lokale docker-host.
> toodo deze, probleem-Hallo volgende opdracht achter de opdrachtprompt: `docker-machine start default`.
> 
> 

[0]: ./media/vs-azure-tools-docker-setup/docker-machine-ls.png
[1]: ./media/vs-azure-tools-docker-setup/docker-ps.png

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
# <a name="configure-a-docker-host-with-virtualbox"></a><span data-ttu-id="db757-103">Een Docker-Host met VirtualBox configureren</span><span class="sxs-lookup"><span data-stu-id="db757-103">Configure a Docker Host with VirtualBox</span></span>
## <a name="overview"></a><span data-ttu-id="db757-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="db757-104">Overview</span></span>
<span data-ttu-id="db757-105">In dit artikel begeleidt u bij het configureren van een standaard Docker-exemplaar met behulp van Docker-Machine en VirtualBox.</span><span class="sxs-lookup"><span data-stu-id="db757-105">This article guides you through configuring a default Docker instance using Docker Machine and VirtualBox.</span></span> <span data-ttu-id="db757-106">Als u Hallo [Docker voor Windows beta](http://beta.docker.com/), deze configuratie is niet nodig.</span><span class="sxs-lookup"><span data-stu-id="db757-106">If you’re using hello [Docker for Windows beta](http://beta.docker.com/), this configuration is not necessary.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="db757-107">Vereisten</span><span class="sxs-lookup"><span data-stu-id="db757-107">Prerequisites</span></span>
<span data-ttu-id="db757-108">Hallo moeten volgende hulpprogramma's toobe geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="db757-108">hello following tools need toobe installed.</span></span>

* [<span data-ttu-id="db757-109">Docker-werkset</span><span class="sxs-lookup"><span data-stu-id="db757-109">Docker Toolbox</span></span>](https://www.docker.com/products/overview#/docker_toolbox)

## <a name="configuring-hello-docker-client-with-windows-powershell"></a><span data-ttu-id="db757-110">Hallo Docker-client configureren met Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="db757-110">Configuring hello Docker client with Windows PowerShell</span></span>
<span data-ttu-id="db757-111">tooconfigure een Docker-client gewoon opent u Windows PowerShell en Voer Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="db757-111">tooconfigure a Docker client, simply open Windows PowerShell, and perform hello following steps:</span></span>

1. <span data-ttu-id="db757-112">Maak een standaardexemplaar van de docker-host.</span><span class="sxs-lookup"><span data-stu-id="db757-112">Create a default docker host instance.</span></span>
   
    ```PowerShell
    docker-machine create --driver virtualbox default
    ```
2. <span data-ttu-id="db757-113">Controleer of het standaardexemplaar Hallo geconfigureerd en actief zijn.</span><span class="sxs-lookup"><span data-stu-id="db757-113">Verify hello default instance is configured and running.</span></span> <span data-ttu-id="db757-114">(U ziet een exemplaar met de naam 'default' uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="db757-114">(You should see an instance named \`default' running.</span></span>
   
    ```PowerShell
    docker-machine ls 
    ```
   
    ![docker-machine ls-uitvoer][0]
3. <span data-ttu-id="db757-116">Als de huidige host Hallo instellen en configureren van de shell.</span><span class="sxs-lookup"><span data-stu-id="db757-116">Set default as hello current host, and configure your shell.</span></span>
   
    ```PowerShell
    docker-machine env default | Invoke-Expression
    ```
4. <span data-ttu-id="db757-117">Hallo active Docker-containers worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="db757-117">Display hello active Docker containers.</span></span> <span data-ttu-id="db757-118">Hallo lijst mag niet leeg zijn.</span><span class="sxs-lookup"><span data-stu-id="db757-118">hello list should be empty.</span></span>
   
    ```PowerShell
    docker ps
    ```
   
    ![docker ps-uitvoer][1]

> [!NOTE]
> <span data-ttu-id="db757-120">Telkens wanneer die u opnieuw opstarten van uw ontwikkelcomputer, moet u toorestart uw lokale docker-host.</span><span class="sxs-lookup"><span data-stu-id="db757-120">Each time you reboot your development machine, you’ll need toorestart your local docker host.</span></span>
> <span data-ttu-id="db757-121">toodo deze, probleem-Hallo volgende opdracht achter de opdrachtprompt: `docker-machine start default`.</span><span class="sxs-lookup"><span data-stu-id="db757-121">toodo this, issue hello following command at a command prompt: `docker-machine start default`.</span></span>
> 
> 

[0]: ./media/vs-azure-tools-docker-setup/docker-machine-ls.png
[1]: ./media/vs-azure-tools-docker-setup/docker-ps.png

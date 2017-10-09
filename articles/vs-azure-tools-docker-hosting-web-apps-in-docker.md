---
title: een ASP.NET Core Linux Docker-container tooa externe Docker host aaaDeploy | Microsoft Docs
description: Meer informatie over hoe toouse Visual Studio Tools for Docker toodeploy een ASP.NET Core web-app tooa Docker-container uitgevoerd op een virtuele machine van Azure Docker Host Linux
services: azure-container-service
documentationcenter: .net
author: mlearned
manager: douge
editor: 
ms.assetid: e5e81c5e-dd18-4d5a-a24d-a932036e78b9
ms.service: azure-container-service
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/08/2016
ms.author: mlearned
ms.openlocfilehash: 27b0c6420628c73220200bc071b47a4cd89fff58
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-aspnet-container-tooa-remote-docker-host"></a><span data-ttu-id="0e942-103">Een ASP.NET-container tooa externe Docker-host implementeren</span><span class="sxs-lookup"><span data-stu-id="0e942-103">Deploy an ASP.NET container tooa remote Docker host</span></span>
## <a name="overview"></a><span data-ttu-id="0e942-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="0e942-104">Overview</span></span>
<span data-ttu-id="0e942-105">Docker is een lichtgewicht container-engine, in een aantal manieren tooa virtuele machine, die u kunt vergelijkbare toohost toepassingen en services.</span><span class="sxs-lookup"><span data-stu-id="0e942-105">Docker is a lightweight container engine, similar in some ways tooa virtual machine, which you can use toohost applications and services.</span></span>
<span data-ttu-id="0e942-106">Deze zelfstudie leert u met behulp van Hallo [Visual Studio Tools for Docker](https://docs.microsoft.com/en-us/dotnet/articles/core/docker/visual-studio-tools-for-docker) extensie toodeploy een ASP.NET Core app tooa Docker-host op Azure met behulp van PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0e942-106">This tutorial walks you through using hello [Visual Studio Tools for Docker](https://docs.microsoft.com/en-us/dotnet/articles/core/docker/visual-studio-tools-for-docker) extension toodeploy an ASP.NET Core app tooa Docker host on Azure using PowerShell.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0e942-107">Vereisten</span><span class="sxs-lookup"><span data-stu-id="0e942-107">Prerequisites</span></span>
<span data-ttu-id="0e942-108">Hallo volgende vereiste toocomplete in deze zelfstudie is:</span><span class="sxs-lookup"><span data-stu-id="0e942-108">hello following is required toocomplete this tutorial:</span></span>

* <span data-ttu-id="0e942-109">Maak een virtuele machine in Azure Docker-Host, zoals beschreven in [hoe toouse docker-machine met Azure](virtual-machines/linux/docker-machine.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="0e942-109">Create an Azure Docker Host VM as described in [How toouse docker-machine with Azure](virtual-machines/linux/docker-machine.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>
* <span data-ttu-id="0e942-110">Installeer de nieuwste versie Hallo van [Visual Studio](https://www.visualstudio.com/downloads/)</span><span class="sxs-lookup"><span data-stu-id="0e942-110">Install hello latest version of [Visual Studio](https://www.visualstudio.com/downloads/)</span></span>
* <span data-ttu-id="0e942-111">Hallo downloaden [Microsoft ASP.NET Core 1.0 SDK](https://go.microsoft.com/fwlink/?LinkID=809122)</span><span class="sxs-lookup"><span data-stu-id="0e942-111">Download hello [Microsoft ASP.NET Core 1.0 SDK](https://go.microsoft.com/fwlink/?LinkID=809122)</span></span>
* <span data-ttu-id="0e942-112">Installeer [Docker voor Windows](https://docs.docker.com/docker-for-windows/install/)</span><span class="sxs-lookup"><span data-stu-id="0e942-112">Install [Docker for Windows](https://docs.docker.com/docker-for-windows/install/)</span></span>

## <a name="1-create-an-aspnet-core-web-app"></a><span data-ttu-id="0e942-113">1. Een ASP.NET Core web-app maken</span><span class="sxs-lookup"><span data-stu-id="0e942-113">1. Create an ASP.NET Core web app</span></span>
<span data-ttu-id="0e942-114">Hallo volgende stappen begeleiden u bij het maken van een eenvoudige ASP.NET Core-app die wordt gebruikt in deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="0e942-114">hello following steps guide you through creating a basic ASP.NET Core app that will be used in this tutorial.</span></span>

[!INCLUDE [create-aspnet5-app](../includes/create-aspnet5-app.md)]

## <a name="2-add-docker-support"></a><span data-ttu-id="0e942-115">2. Docker-ondersteuning toevoegen</span><span class="sxs-lookup"><span data-stu-id="0e942-115">2. Add Docker support</span></span>
[!INCLUDE [create-aspnet5-app](../includes/vs-azure-tools-docker-add-docker-support.md)]

## <a name="3-use-hello-dockertaskps1-powershell-script"></a><span data-ttu-id="0e942-116">3. Hallo DockerTask.ps1 PowerShell-Script gebruiken</span><span class="sxs-lookup"><span data-stu-id="0e942-116">3. Use hello DockerTask.ps1 PowerShell Script</span></span>
1. <span data-ttu-id="0e942-117">Open een PowerShell-prompt toohello hoofdmap van uw project.</span><span class="sxs-lookup"><span data-stu-id="0e942-117">Open a PowerShell prompt toohello root directory of your project.</span></span> 
   
   ```
   PS C:\Src\WebApplication1>
   ```
2. <span data-ttu-id="0e942-118">Valideren Hallo externe host wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="0e942-118">Validate hello remote host is running.</span></span> <span data-ttu-id="0e942-119">U ziet de status actief =</span><span class="sxs-lookup"><span data-stu-id="0e942-119">You should see state = Running</span></span> 
   
   ```
   docker-machine ls
   NAME         ACTIVE   DRIVER   STATE     URL                        SWARM   DOCKER    ERRORS
   MyDockerHost -        azure    Running   tcp://xxx.xxx.xxx.xxx:2376         v1.10.3
   ```
   
3. <span data-ttu-id="0e942-120">Build Hallo app met behulp Hallo - Build-parameter</span><span class="sxs-lookup"><span data-stu-id="0e942-120">Build hello app using hello -Build parameter</span></span>
   
   ```
   PS C:\Src\WebApplication1> .\Docker\DockerTask.ps1 -Build -Environment Release -Machine mydockerhost
   ```  

   > ```
   > PS C:\Src\WebApplication1> .\Docker\DockerTask.ps1 -Build -Environment Release 
   > ```  
   > 
   > 
4. <span data-ttu-id="0e942-121">Hallo-app uitvoeren met behulp van Hallo - parameter uitvoeren</span><span class="sxs-lookup"><span data-stu-id="0e942-121">Run hello app, using hello -Run parameter</span></span>
   
   ```
   PS C:\Src\WebApplication1> .\Docker\DockerTask.ps1 -Run -Environment Release -Machine mydockerhost
   ```
   
   > ```
   > PS C:\Src\WebApplication1> .\Docker\DockerTask.ps1 -Run -Environment Release 
   > ```
   > 
   > 
   
   <span data-ttu-id="0e942-122">Wanneer de docker is voltooid, kunt u resultaten vergelijkbare toohello volgende moeten zien:</span><span class="sxs-lookup"><span data-stu-id="0e942-122">Once docker completes, you should see results similar toohello following:</span></span>
   
   ![Uw app weergeven][3]

[0]:./media/vs-azure-tools-docker-hosting-web-apps-in-docker/docker-props-in-solution-explorer.png
[1]:./media/vs-azure-tools-docker-hosting-web-apps-in-docker/change-docker-machine-name.png
[2]:./media/vs-azure-tools-docker-hosting-web-apps-in-docker/launch-application.png
[3]:./media/vs-azure-tools-docker-hosting-web-apps-in-docker/view-application.png

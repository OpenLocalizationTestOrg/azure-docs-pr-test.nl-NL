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
# <a name="deploy-an-aspnet-container-tooa-remote-docker-host"></a>Een ASP.NET-container tooa externe Docker-host implementeren
## <a name="overview"></a>Overzicht
Docker is een lichtgewicht container-engine, in een aantal manieren tooa virtuele machine, die u kunt vergelijkbare toohost toepassingen en services.
Deze zelfstudie leert u met behulp van Hallo [Visual Studio Tools for Docker](https://docs.microsoft.com/en-us/dotnet/articles/core/docker/visual-studio-tools-for-docker) extensie toodeploy een ASP.NET Core app tooa Docker-host op Azure met behulp van PowerShell.

## <a name="prerequisites"></a>Vereisten
Hallo volgende vereiste toocomplete in deze zelfstudie is:

* Maak een virtuele machine in Azure Docker-Host, zoals beschreven in [hoe toouse docker-machine met Azure](virtual-machines/linux/docker-machine.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* Installeer de nieuwste versie Hallo van [Visual Studio](https://www.visualstudio.com/downloads/)
* Hallo downloaden [Microsoft ASP.NET Core 1.0 SDK](https://go.microsoft.com/fwlink/?LinkID=809122)
* Installeer [Docker voor Windows](https://docs.docker.com/docker-for-windows/install/)

## <a name="1-create-an-aspnet-core-web-app"></a>1. Een ASP.NET Core web-app maken
Hallo volgende stappen begeleiden u bij het maken van een eenvoudige ASP.NET Core-app die wordt gebruikt in deze zelfstudie.

[!INCLUDE [create-aspnet5-app](../includes/create-aspnet5-app.md)]

## <a name="2-add-docker-support"></a>2. Docker-ondersteuning toevoegen
[!INCLUDE [create-aspnet5-app](../includes/vs-azure-tools-docker-add-docker-support.md)]

## <a name="3-use-hello-dockertaskps1-powershell-script"></a>3. Hallo DockerTask.ps1 PowerShell-Script gebruiken
1. Open een PowerShell-prompt toohello hoofdmap van uw project. 
   
   ```
   PS C:\Src\WebApplication1>
   ```
2. Valideren Hallo externe host wordt uitgevoerd. U ziet de status actief = 
   
   ```
   docker-machine ls
   NAME         ACTIVE   DRIVER   STATE     URL                        SWARM   DOCKER    ERRORS
   MyDockerHost -        azure    Running   tcp://xxx.xxx.xxx.xxx:2376         v1.10.3
   ```
   
3. Build Hallo app met behulp Hallo - Build-parameter
   
   ```
   PS C:\Src\WebApplication1> .\Docker\DockerTask.ps1 -Build -Environment Release -Machine mydockerhost
   ```  

   > ```
   > PS C:\Src\WebApplication1> .\Docker\DockerTask.ps1 -Build -Environment Release 
   > ```  
   > 
   > 
4. Hallo-app uitvoeren met behulp van Hallo - parameter uitvoeren
   
   ```
   PS C:\Src\WebApplication1> .\Docker\DockerTask.ps1 -Run -Environment Release -Machine mydockerhost
   ```
   
   > ```
   > PS C:\Src\WebApplication1> .\Docker\DockerTask.ps1 -Run -Environment Release 
   > ```
   > 
   > 
   
   Wanneer de docker is voltooid, kunt u resultaten vergelijkbare toohello volgende moeten zien:
   
   ![Uw app weergeven][3]

[0]:./media/vs-azure-tools-docker-hosting-web-apps-in-docker/docker-props-in-solution-explorer.png
[1]:./media/vs-azure-tools-docker-hosting-web-apps-in-docker/change-docker-machine-name.png
[2]:./media/vs-azure-tools-docker-hosting-web-apps-in-docker/launch-application.png
[3]:./media/vs-azure-tools-docker-hosting-web-apps-in-docker/view-application.png

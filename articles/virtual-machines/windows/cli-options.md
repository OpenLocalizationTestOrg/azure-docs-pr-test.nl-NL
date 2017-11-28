---
title: aaaUsing hello Azure CLI in Windows | Microsoft Docs
description: Met behulp van hello Azure CLI in Windows
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 02/14/2017
ms.author: nepeters
ms.openlocfilehash: edca4a2701a7dfc0fc54df5649e8a5e7afc95490
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-azure-cli-on-windows"></a><span data-ttu-id="c4d26-103">Met behulp van hello Azure CLI in Windows</span><span class="sxs-lookup"><span data-stu-id="c4d26-103">Using hello Azure CLI on Windows</span></span>

<span data-ttu-id="c4d26-104">Hello Azure-opdrachtregelinterface (CLI) biedt een opdrachtregel en scriptomgeving op servers voor het maken en beheren van Azure-resources.</span><span class="sxs-lookup"><span data-stu-id="c4d26-104">hello Azure Command Line Interface (CLI) provides a command line and scripting environment for creating and managing Azure resources.</span></span> <span data-ttu-id="c4d26-105">Hello Azure CLI is beschikbaar voor Mac OS-, Linux- en Windows-besturingssystemen.</span><span class="sxs-lookup"><span data-stu-id="c4d26-105">hello Azure CLI is available for macOS, Linux, and Windows operating systems.</span></span> <span data-ttu-id="c4d26-106">In deze besturingssystemen zijn Hallo CLI-opdrachten identiek, maar de specifieke scriptsyntaxis besturingssysteem kan verschillen.</span><span class="sxs-lookup"><span data-stu-id="c4d26-106">Across these operating systems, hello CLI commands are identical, however operating system specific scripting syntax can differ.</span></span>

<span data-ttu-id="c4d26-107">Dit document details Hallo manieren waarop u Azure CLI Hallo kan worden geïnstalleerd en uitgevoerd op Windows en details syntactische overwegingen voor elke.</span><span class="sxs-lookup"><span data-stu-id="c4d26-107">This document details hello ways that hello Azure CLI can be installed and run on Windows and details syntactical considerations for each.</span></span> <span data-ttu-id="c4d26-108">Zie in de gedetailleerde Azure CLI-documentatie voor [documentatie van Azure CLI]( https://docs.microsoft.com/en-us/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="c4d26-108">For in-depth Azure CLI documentation see, [Azure CLI documentation]( https://docs.microsoft.com/en-us/cli/azure/overview).</span></span>

## <a name="windows-subsystem-for-linux"></a><span data-ttu-id="c4d26-109">Windows-subsysteem voor Linux</span><span class="sxs-lookup"><span data-stu-id="c4d26-109">Windows Subsystem for Linux</span></span>

<span data-ttu-id="c4d26-110">Hallo Windows-subsysteem voor Linux (WSL) biedt een omgeving Ubuntu Linux op Windows 10 Verjaardag en latere versies.</span><span class="sxs-lookup"><span data-stu-id="c4d26-110">hello Windows Subsystem for Linux (WSL) provides an Ubuntu Linux environment on Windows 10 Anniversary and later editions.</span></span> <span data-ttu-id="c4d26-111">Wanneer ingeschakeld, WSL levert een systeemeigen Bash-ervaring die kan worden gebruikt voor het maken en uitvoeren van scripts voor Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="c4d26-111">When enabled, WSL provides a native Bash experience, which can be used for creating and running Azure CLI scripts.</span></span> <span data-ttu-id="c4d26-112">Omdat WSL een systeemeigen Bash-ervaring biedt, kunnen Azure CLI-scripts worden gedeeld tussen Mac OS-, Linux- en Windows zonder aanpassing.</span><span class="sxs-lookup"><span data-stu-id="c4d26-112">Because WSL provides a native Bash experience, Azure CLI scripts can be shared between macOS, Linux, and Windows without modification.</span></span>

<span data-ttu-id="c4d26-113">toouse hello Azure CLI in WSL, Hallo volgende voltooien.</span><span class="sxs-lookup"><span data-stu-id="c4d26-113">toouse hello Azure CLI in WSL, complete hello following.</span></span>

|<span data-ttu-id="c4d26-114">Taak</span><span class="sxs-lookup"><span data-stu-id="c4d26-114">Task</span></span> | <span data-ttu-id="c4d26-115">Instructies</span><span class="sxs-lookup"><span data-stu-id="c4d26-115">Instructions</span></span> |
|---|---|
| <span data-ttu-id="c4d26-116">WSL inschakelen</span><span class="sxs-lookup"><span data-stu-id="c4d26-116">Enable WSL</span></span> | [<span data-ttu-id="c4d26-117">WSL documentatie installeren</span><span class="sxs-lookup"><span data-stu-id="c4d26-117">Install WSL documentation </span></span>](https://msdn.microsoft.com/en-us/commandline/wsl/install_guide) |
| <span data-ttu-id="c4d26-118">Hello Azure CLI installeren</span><span class="sxs-lookup"><span data-stu-id="c4d26-118">Install hello Azure CLI</span></span> |[<span data-ttu-id="c4d26-119">Hallo CLI installeren op WSL/Ubuntu 14.04</span><span class="sxs-lookup"><span data-stu-id="c4d26-119">Install hello CLI on WSL/Ubuntu 14.04</span></span>](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2#ubuntu)|

## <a name="powershell"></a><span data-ttu-id="c4d26-120">PowerShell</span><span class="sxs-lookup"><span data-stu-id="c4d26-120">PowerShell</span></span>

<span data-ttu-id="c4d26-121">Hello Azure CLI kunt systeemeigen in Windows worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="c4d26-121">hello Azure CLI can be run natively in Windows.</span></span> <span data-ttu-id="c4d26-122">In deze configuratie hello Azure CLI-pakket is geïnstalleerd op Windows-besturingssysteem Hallo en opdrachten kunnen worden uitgevoerd vanuit PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c4d26-122">In this configuration, hello Azure CLI package is installed on hello Windows operating system, and commands can be run from PowerShell.</span></span> <span data-ttu-id="c4d26-123">In deze configuratie, kunnen Azure CLI-opdrachten en scripts worden uitgevoerd op een ondersteunde versie van Windows, maar de specifieke scriptsyntaxis platform vereist is.</span><span class="sxs-lookup"><span data-stu-id="c4d26-123">In this configuration, Azure CLI commands and scripts can be run on any supported version of Windows, however platform specific scripting syntax is required.</span></span> <span data-ttu-id="c4d26-124">Als gevolg hiervan kunnen geen scripts altijd worden gedeeld tussen Mac OS-, Linux- en Windows zonder aanpassingen.</span><span class="sxs-lookup"><span data-stu-id="c4d26-124">Because of this, scripts cannot necessarily be shared between macOS, Linux, and Windows without modification.</span></span>

<span data-ttu-id="c4d26-125">toouse hello Azure CLI op Windows hello pakket installeren via deze instructies [installeren Hallo CLI in Windows](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2#windows).</span><span class="sxs-lookup"><span data-stu-id="c4d26-125">toouse hello Azure CLI on Windows, install hello package using these instructions, [Install hello CLI on Windows](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2#windows).</span></span>

## <a name="docker-image"></a><span data-ttu-id="c4d26-126">Docker-afbeelding</span><span class="sxs-lookup"><span data-stu-id="c4d26-126">Docker Image</span></span>

<span data-ttu-id="c4d26-127">Wanneer u Docker voor Windows, kan een Docker-installatiekopie worden gestart met hello Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="c4d26-127">When using Docker for Windows, a Docker image can be started that includes hello Azure CLI.</span></span> <span data-ttu-id="c4d26-128">Deze installatiekopie is gebaseerd op Linux en bevat een systeemeigen Bash-ervaring.</span><span class="sxs-lookup"><span data-stu-id="c4d26-128">This image is based off of Linux, and includes a native Bash experience.</span></span>  <span data-ttu-id="c4d26-129">Als u Docker voor Windows en hello Azure CLI-installatiekopie, scripts toobe gedeeld tussen Mac OS-, Linux- en Windows.</span><span class="sxs-lookup"><span data-stu-id="c4d26-129">When using Docker for Windows and hello Azure CLI image, scripts toobe shared between macOS, Linux, and Windows.</span></span> 

<span data-ttu-id="c4d26-130">toouse hello Azure CLI op Docker voor Windows, zorg ervoor dat Docker voor Windows wordt uitgevoerd en Hallo volgende opdracht uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="c4d26-130">toouse hello Azure CLI on Docker for Windows, ensure that Docker for Windows is running and run hello following command.</span></span>

```bash
docker run -it azuresdk/azure-cli-python:latest bash
```

<span data-ttu-id="c4d26-131">Zodra de voltooid, wordt een sessie wordt gestart, dat wil Bash vooraf geladen met hello Azure CLI-hulpprogramma's.</span><span class="sxs-lookup"><span data-stu-id="c4d26-131">Once completed, a Bash session will start that is preloaded with hello Azure CLI tools.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c4d26-132">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="c4d26-132">Next Steps</span></span>

[<span data-ttu-id="c4d26-133">Voorbeeld voor virtuele machines van Azure CLI</span><span class="sxs-lookup"><span data-stu-id="c4d26-133">CLI sample for Azure virtual machines</span></span>](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[<span data-ttu-id="c4d26-134">Voorbeelden voor Web-Apps van Azure CLI</span><span class="sxs-lookup"><span data-stu-id="c4d26-134">CLI samples for Azure Web Apps</span></span>](../../app-service-web/app-service-cli-samples.md)

[<span data-ttu-id="c4d26-135">Voorbeelden voor SQL Azure CLI</span><span class="sxs-lookup"><span data-stu-id="c4d26-135">CLI samples for Azure SQL</span></span>](../../sql-database/sql-database-cli-samples.md)

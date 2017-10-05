---
title: De Azure CLI gebruiken op Windows | Microsoft Docs
description: De Azure CLI gebruiken in Windows
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
ms.openlocfilehash: be02ad0d7752cb08f092deeb5a86dcd126403237
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="using-the-azure-cli-on-windows"></a><span data-ttu-id="79189-103">De Azure CLI gebruiken in Windows</span><span class="sxs-lookup"><span data-stu-id="79189-103">Using the Azure CLI on Windows</span></span>

<span data-ttu-id="79189-104">De Azure-opdrachtregelinterface (CLI) biedt een opdrachtregel en scriptomgeving op servers voor het maken en beheren van Azure-resources.</span><span class="sxs-lookup"><span data-stu-id="79189-104">The Azure Command Line Interface (CLI) provides a command line and scripting environment for creating and managing Azure resources.</span></span> <span data-ttu-id="79189-105">De Azure CLI is beschikbaar voor Mac OS-, Linux- en Windows-besturingssystemen.</span><span class="sxs-lookup"><span data-stu-id="79189-105">The Azure CLI is available for macOS, Linux, and Windows operating systems.</span></span> <span data-ttu-id="79189-106">In deze besturingssystemen zijn de CLI-opdrachten identiek, maar de specifieke scriptsyntaxis besturingssysteem kan verschillen.</span><span class="sxs-lookup"><span data-stu-id="79189-106">Across these operating systems, the CLI commands are identical, however operating system specific scripting syntax can differ.</span></span>

<span data-ttu-id="79189-107">In dit document worden de manieren dat de Azure CLI kan worden geïnstalleerd en uitgevoerd op Windows en details syntactische overwegingen voor elke.</span><span class="sxs-lookup"><span data-stu-id="79189-107">This document details the ways that the Azure CLI can be installed and run on Windows and details syntactical considerations for each.</span></span> <span data-ttu-id="79189-108">Zie in de gedetailleerde Azure CLI-documentatie voor [documentatie van Azure CLI]( https://docs.microsoft.com/en-us/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="79189-108">For in-depth Azure CLI documentation see, [Azure CLI documentation]( https://docs.microsoft.com/en-us/cli/azure/overview).</span></span>

## <a name="windows-subsystem-for-linux"></a><span data-ttu-id="79189-109">Windows-subsysteem voor Linux</span><span class="sxs-lookup"><span data-stu-id="79189-109">Windows Subsystem for Linux</span></span>

<span data-ttu-id="79189-110">Het Windows-subsysteem voor Linux (WSL) biedt een omgeving Ubuntu Linux op Windows 10 Verjaardag en latere versies.</span><span class="sxs-lookup"><span data-stu-id="79189-110">The Windows Subsystem for Linux (WSL) provides an Ubuntu Linux environment on Windows 10 Anniversary and later editions.</span></span> <span data-ttu-id="79189-111">Wanneer ingeschakeld, WSL levert een systeemeigen Bash-ervaring die kan worden gebruikt voor het maken en uitvoeren van scripts voor Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="79189-111">When enabled, WSL provides a native Bash experience, which can be used for creating and running Azure CLI scripts.</span></span> <span data-ttu-id="79189-112">Omdat WSL een systeemeigen Bash-ervaring biedt, kunnen Azure CLI-scripts worden gedeeld tussen Mac OS-, Linux- en Windows zonder aanpassing.</span><span class="sxs-lookup"><span data-stu-id="79189-112">Because WSL provides a native Bash experience, Azure CLI scripts can be shared between macOS, Linux, and Windows without modification.</span></span>

<span data-ttu-id="79189-113">Als u de Azure CLI in WSL, voert u de volgende.</span><span class="sxs-lookup"><span data-stu-id="79189-113">To use the Azure CLI in WSL, complete the following.</span></span>

|<span data-ttu-id="79189-114">Taak</span><span class="sxs-lookup"><span data-stu-id="79189-114">Task</span></span> | <span data-ttu-id="79189-115">Instructies</span><span class="sxs-lookup"><span data-stu-id="79189-115">Instructions</span></span> |
|---|---|
| <span data-ttu-id="79189-116">WSL inschakelen</span><span class="sxs-lookup"><span data-stu-id="79189-116">Enable WSL</span></span> | [<span data-ttu-id="79189-117">WSL documentatie installeren</span><span class="sxs-lookup"><span data-stu-id="79189-117">Install WSL documentation </span></span>](https://msdn.microsoft.com/en-us/commandline/wsl/install_guide) |
| <span data-ttu-id="79189-118">Azure-CLI installeren</span><span class="sxs-lookup"><span data-stu-id="79189-118">Install the Azure CLI</span></span> |[<span data-ttu-id="79189-119">De CLI installeren op WSL/Ubuntu 14.04</span><span class="sxs-lookup"><span data-stu-id="79189-119">Install the CLI on WSL/Ubuntu 14.04</span></span>](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2#ubuntu)|

## <a name="powershell"></a><span data-ttu-id="79189-120">PowerShell</span><span class="sxs-lookup"><span data-stu-id="79189-120">PowerShell</span></span>

<span data-ttu-id="79189-121">De Azure CLI kunt systeemeigen in Windows worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="79189-121">The Azure CLI can be run natively in Windows.</span></span> <span data-ttu-id="79189-122">In deze configuratie is de Azure CLI-pakket is geïnstalleerd op de Windows-besturingssysteem en opdrachten kunnen worden uitgevoerd vanuit PowerShell.</span><span class="sxs-lookup"><span data-stu-id="79189-122">In this configuration, the Azure CLI package is installed on the Windows operating system, and commands can be run from PowerShell.</span></span> <span data-ttu-id="79189-123">In deze configuratie, kunnen Azure CLI-opdrachten en scripts worden uitgevoerd op een ondersteunde versie van Windows, maar de specifieke scriptsyntaxis platform vereist is.</span><span class="sxs-lookup"><span data-stu-id="79189-123">In this configuration, Azure CLI commands and scripts can be run on any supported version of Windows, however platform specific scripting syntax is required.</span></span> <span data-ttu-id="79189-124">Als gevolg hiervan kunnen geen scripts altijd worden gedeeld tussen Mac OS-, Linux- en Windows zonder aanpassingen.</span><span class="sxs-lookup"><span data-stu-id="79189-124">Because of this, scripts cannot necessarily be shared between macOS, Linux, and Windows without modification.</span></span>

<span data-ttu-id="79189-125">Installeer het pakket deze instructies voor het gebruik van de Azure CLI in Windows, [CLI installeren op Windows](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2#windows).</span><span class="sxs-lookup"><span data-stu-id="79189-125">To use the Azure CLI on Windows, install the package using these instructions, [Install the CLI on Windows](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2#windows).</span></span>

## <a name="docker-image"></a><span data-ttu-id="79189-126">Docker-afbeelding</span><span class="sxs-lookup"><span data-stu-id="79189-126">Docker Image</span></span>

<span data-ttu-id="79189-127">Wanneer u Docker voor Windows, kan een Docker-installatiekopie worden gestart met de Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="79189-127">When using Docker for Windows, a Docker image can be started that includes the Azure CLI.</span></span> <span data-ttu-id="79189-128">Deze installatiekopie is gebaseerd op Linux en bevat een systeemeigen Bash-ervaring.</span><span class="sxs-lookup"><span data-stu-id="79189-128">This image is based off of Linux, and includes a native Bash experience.</span></span>  <span data-ttu-id="79189-129">Als u Docker voor Windows en de installatiekopie van het Azure CLI-scripts kunnen worden gedeeld tussen Mac OS-, Linux- en Windows.</span><span class="sxs-lookup"><span data-stu-id="79189-129">When using Docker for Windows and the Azure CLI image, scripts to be shared between macOS, Linux, and Windows.</span></span> 

<span data-ttu-id="79189-130">Zorg ervoor dat Docker voor Windows wordt uitgevoerd voor het gebruik van de Azure CLI op Docker voor Windows, en voer de volgende opdracht.</span><span class="sxs-lookup"><span data-stu-id="79189-130">To use the Azure CLI on Docker for Windows, ensure that Docker for Windows is running and run the following command.</span></span>

```bash
docker run -it azuresdk/azure-cli-python:latest bash
```

<span data-ttu-id="79189-131">Als voltooid, wordt een sessie wordt gestart, dat wil Bash vooraf geladen met de Azure CLI-hulpprogramma's.</span><span class="sxs-lookup"><span data-stu-id="79189-131">Once completed, a Bash session will start that is preloaded with the Azure CLI tools.</span></span>

## <a name="next-steps"></a><span data-ttu-id="79189-132">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="79189-132">Next Steps</span></span>

[<span data-ttu-id="79189-133">Voorbeeld voor virtuele machines van Azure CLI</span><span class="sxs-lookup"><span data-stu-id="79189-133">CLI sample for Azure virtual machines</span></span>](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[<span data-ttu-id="79189-134">Voorbeelden voor Web-Apps van Azure CLI</span><span class="sxs-lookup"><span data-stu-id="79189-134">CLI samples for Azure Web Apps</span></span>](../../app-service-web/app-service-cli-samples.md)

[<span data-ttu-id="79189-135">Voorbeelden voor SQL Azure CLI</span><span class="sxs-lookup"><span data-stu-id="79189-135">CLI samples for Azure SQL</span></span>](../../sql-database/sql-database-cli-samples.md)

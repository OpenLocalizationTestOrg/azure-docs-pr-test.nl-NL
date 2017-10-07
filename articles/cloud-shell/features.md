---
title: functies van aaaAzure Cloud Shell (Preview) | Microsoft Docs
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
ms.openlocfilehash: 65482ca6caeac01dda18a6b12eabe943e3d68a96
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="features-and-tools-for-azure-cloud-shell"></a><span data-ttu-id="6a59a-103">Functies en hulpprogramma's voor Azure-Cloud-Shell</span><span class="sxs-lookup"><span data-stu-id="6a59a-103">Features and Tools for Azure Cloud Shell</span></span>
<span data-ttu-id="6a59a-104">Azure Cloud-Shell is een browser gebaseerde shell-ervaring toomanage en ontwikkelen van Azure-resources.</span><span class="sxs-lookup"><span data-stu-id="6a59a-104">Azure Cloud Shell is a browser-based shell experience toomanage and develop Azure resources.</span></span>

<span data-ttu-id="6a59a-105">Cloud-Shell biedt een browser toegankelijk, vooraf geconfigureerde shell-ervaring voor het beheren van Azure-resources zonder Hallo-overhead voor het installeren van versies, en onderhouden van een machine.</span><span class="sxs-lookup"><span data-stu-id="6a59a-105">Cloud Shell offers a browser-accessible, pre-configured shell experience for managing Azure resources without hello overhead of installing, versioning, and maintaining a machine yourself.</span></span>

<span data-ttu-id="6a59a-106">Cloud-Shell richt machines op basis van per aanvraag en als gevolg hiervan MACHINESTATUS niet behouden over de sessies.</span><span class="sxs-lookup"><span data-stu-id="6a59a-106">Cloud Shell provisions machines on a per-request basis and as a result machine state will not persist across sessions.</span></span> <span data-ttu-id="6a59a-107">Aangezien Cloud Shell is gebouwd voor interactieve sessies, wordt de houders automatisch opgeheven na 20 minuten van inactiviteit shell.</span><span class="sxs-lookup"><span data-stu-id="6a59a-107">Since Cloud Shell is built for interactive sessions, shells automatically terminate after 20 minutes of shell inactivity.</span></span>

## <a name="bash-in-cloud-shell"></a><span data-ttu-id="6a59a-108">In de Cloud-Shell Bash</span><span class="sxs-lookup"><span data-stu-id="6a59a-108">Bash in Cloud Shell</span></span>
### <a name="tools"></a><span data-ttu-id="6a59a-109">Hulpprogramma's</span><span class="sxs-lookup"><span data-stu-id="6a59a-109">Tools</span></span>
|<span data-ttu-id="6a59a-110">Category</span><span class="sxs-lookup"><span data-stu-id="6a59a-110">Category</span></span>   |<span data-ttu-id="6a59a-111">Naam</span><span class="sxs-lookup"><span data-stu-id="6a59a-111">Name</span></span>   |
|---|---|
|<span data-ttu-id="6a59a-112">Linux shell-interpreter</span><span class="sxs-lookup"><span data-stu-id="6a59a-112">Linux shell interpreter</span></span>|<span data-ttu-id="6a59a-113">Bash</span><span class="sxs-lookup"><span data-stu-id="6a59a-113">Bash</span></span><br> <span data-ttu-id="6a59a-114">servicel</span><span class="sxs-lookup"><span data-stu-id="6a59a-114">sh</span></span>               |
|<span data-ttu-id="6a59a-115">Azure-hulpprogramma 's</span><span class="sxs-lookup"><span data-stu-id="6a59a-115">Azure tools</span></span>            |<span data-ttu-id="6a59a-116">[Azure CLI 2.0](https://github.com/Azure/azure-cli) en [1.0](https://github.com/Azure/azure-xplat-cli)</span><span class="sxs-lookup"><span data-stu-id="6a59a-116">[Azure CLI 2.0](https://github.com/Azure/azure-cli) and [1.0](https://github.com/Azure/azure-xplat-cli)</span></span><br> [<span data-ttu-id="6a59a-117">AzCopy</span><span class="sxs-lookup"><span data-stu-id="6a59a-117">AzCopy</span></span>](https://docs.microsoft.com/azure/storage/storage-use-azcopy)<br> [<span data-ttu-id="6a59a-118">Batch Shipyard</span><span class="sxs-lookup"><span data-stu-id="6a59a-118">Batch Shipyard</span></span>](https://github.com/Azure/batch-shipyard)     |
|<span data-ttu-id="6a59a-119">Teksteditors</span><span class="sxs-lookup"><span data-stu-id="6a59a-119">Text editors</span></span>           |<span data-ttu-id="6a59a-120">VIM</span><span class="sxs-lookup"><span data-stu-id="6a59a-120">vim</span></span><br> <span data-ttu-id="6a59a-121">nano</span><span class="sxs-lookup"><span data-stu-id="6a59a-121">nano</span></span><br> <span data-ttu-id="6a59a-122">emacs</span><span class="sxs-lookup"><span data-stu-id="6a59a-122">emacs</span></span>       |
|<span data-ttu-id="6a59a-123">Resourcebeheer</span><span class="sxs-lookup"><span data-stu-id="6a59a-123">Source control</span></span>         |<span data-ttu-id="6a59a-124">GIT</span><span class="sxs-lookup"><span data-stu-id="6a59a-124">git</span></span>                    |
|<span data-ttu-id="6a59a-125">Hulpprogramma's van build</span><span class="sxs-lookup"><span data-stu-id="6a59a-125">Build tools</span></span>            |<span data-ttu-id="6a59a-126">Maken</span><span class="sxs-lookup"><span data-stu-id="6a59a-126">make</span></span><br> <span data-ttu-id="6a59a-127">maven</span><span class="sxs-lookup"><span data-stu-id="6a59a-127">maven</span></span><br> <span data-ttu-id="6a59a-128">npm</span><span class="sxs-lookup"><span data-stu-id="6a59a-128">npm</span></span><br> <span data-ttu-id="6a59a-129">PIP</span><span class="sxs-lookup"><span data-stu-id="6a59a-129">pip</span></span>         |
|<span data-ttu-id="6a59a-130">Containers</span><span class="sxs-lookup"><span data-stu-id="6a59a-130">Containers</span></span>             |<span data-ttu-id="6a59a-131">[Docker CLI](https://github.com/docker/cli)/[Docker-Machine](https://github.com/docker/machine)</span><span class="sxs-lookup"><span data-stu-id="6a59a-131">[Docker CLI](https://github.com/docker/cli)/[Docker Machine](https://github.com/docker/machine)</span></span><br> [<span data-ttu-id="6a59a-132">Kubectl</span><span class="sxs-lookup"><span data-stu-id="6a59a-132">Kubectl</span></span>](https://kubernetes.io/docs/user-guide/kubectl-overview/)<br> [<span data-ttu-id="6a59a-133">Concept</span><span class="sxs-lookup"><span data-stu-id="6a59a-133">Draft</span></span>](https://github.com/Azure/draft)<br> [<span data-ttu-id="6a59a-134">DC/OS CLI</span><span class="sxs-lookup"><span data-stu-id="6a59a-134">DC/OS CLI</span></span>](https://github.com/dcos/dcos-cli)         |
|<span data-ttu-id="6a59a-135">Databases</span><span class="sxs-lookup"><span data-stu-id="6a59a-135">Databases</span></span>              |<span data-ttu-id="6a59a-136">MySQL-client</span><span class="sxs-lookup"><span data-stu-id="6a59a-136">MySQL client</span></span><br> <span data-ttu-id="6a59a-137">PostgreSql-client</span><span class="sxs-lookup"><span data-stu-id="6a59a-137">PostgreSql client</span></span><br> [<span data-ttu-id="6a59a-138">Sqlcmd-hulpprogramma</span><span class="sxs-lookup"><span data-stu-id="6a59a-138">sqlcmd Utility</span></span>](https://docs.microsoft.com/sql/tools/sqlcmd-utility)<br> [<span data-ttu-id="6a59a-139">MSSQL-scripts</span><span class="sxs-lookup"><span data-stu-id="6a59a-139">mssql-scripter</span></span>](https://github.com/Microsoft/sql-xplat-cli) |
|<span data-ttu-id="6a59a-140">Overige</span><span class="sxs-lookup"><span data-stu-id="6a59a-140">Other</span></span>                  |<span data-ttu-id="6a59a-141">iPython Client</span><span class="sxs-lookup"><span data-stu-id="6a59a-141">iPython Client</span></span><br> [<span data-ttu-id="6a59a-142">Cloud Foundry CLI</span><span class="sxs-lookup"><span data-stu-id="6a59a-142">Cloud Foundry CLI</span></span>](https://github.com/cloudfoundry/cli)<br> |

### <a name="language-support"></a><span data-ttu-id="6a59a-143">Taalondersteuning</span><span class="sxs-lookup"><span data-stu-id="6a59a-143">Language support</span></span>
|<span data-ttu-id="6a59a-144">Taal</span><span class="sxs-lookup"><span data-stu-id="6a59a-144">Language</span></span>   |<span data-ttu-id="6a59a-145">Versie</span><span class="sxs-lookup"><span data-stu-id="6a59a-145">Version</span></span>   |
|---|---|
|<span data-ttu-id="6a59a-146">.NET</span><span class="sxs-lookup"><span data-stu-id="6a59a-146">.NET</span></span>       |<span data-ttu-id="6a59a-147">1.01</span><span class="sxs-lookup"><span data-stu-id="6a59a-147">1.01</span></span>       |
|<span data-ttu-id="6a59a-148">Aan de slag</span><span class="sxs-lookup"><span data-stu-id="6a59a-148">Go</span></span>         |<span data-ttu-id="6a59a-149">1.7</span><span class="sxs-lookup"><span data-stu-id="6a59a-149">1.7</span></span>        |
|<span data-ttu-id="6a59a-150">Java</span><span class="sxs-lookup"><span data-stu-id="6a59a-150">Java</span></span>       |<span data-ttu-id="6a59a-151">1.8</span><span class="sxs-lookup"><span data-stu-id="6a59a-151">1.8</span></span>        |
|<span data-ttu-id="6a59a-152">Node.js</span><span class="sxs-lookup"><span data-stu-id="6a59a-152">Node.js</span></span>    |<span data-ttu-id="6a59a-153">6.9.4</span><span class="sxs-lookup"><span data-stu-id="6a59a-153">6.9.4</span></span>      |
|<span data-ttu-id="6a59a-154">Python</span><span class="sxs-lookup"><span data-stu-id="6a59a-154">Python</span></span>     |<span data-ttu-id="6a59a-155">2.7 en 3.5 (standaard)</span><span class="sxs-lookup"><span data-stu-id="6a59a-155">2.7 and 3.5 (default)</span></span>|

## <a name="secure-automatic-authentication"></a><span data-ttu-id="6a59a-156">Automatische verificatie beveiligen</span><span class="sxs-lookup"><span data-stu-id="6a59a-156">Secure automatic authentication</span></span>
<span data-ttu-id="6a59a-157">Cloud-Shell verifieert veilig en automatisch accounttoegang voor hello Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="6a59a-157">Cloud Shell securely and automatically authenticates account access for hello Azure CLI 2.0.</span></span>

## <a name="azure-files-persistence"></a><span data-ttu-id="6a59a-158">Azure bestanden persistentie</span><span class="sxs-lookup"><span data-stu-id="6a59a-158">Azure Files persistence</span></span>
<span data-ttu-id="6a59a-159">Omdat Cloud Shell is toegewezen op basis van gebruik van een tijdelijke machine per aanvraag, bestanden buiten de status van uw $Home en de machine zijn niet permanent opgeslagen over de sessies.</span><span class="sxs-lookup"><span data-stu-id="6a59a-159">Since Cloud Shell is allocated on a per-request basis using a temporary machine, files outside of your $Home and machine state are not persisted across sessions.</span></span>
<span data-ttu-id="6a59a-160">toopersist bestanden voor volgende sessies Cloud Shell begeleidt u bij het koppelen van een Azure-bestand delen op de eerste keer opstarten.</span><span class="sxs-lookup"><span data-stu-id="6a59a-160">toopersist files across sessions, Cloud Shell walks you through attaching an Azure file share on first launch.</span></span>
<span data-ttu-id="6a59a-161">Wanneer u klaar Cloud Shell wordt automatisch koppelen van uw opslag voor alle toekomstige sessies.</span><span class="sxs-lookup"><span data-stu-id="6a59a-161">Once completed Cloud Shell will automatically attach your storage for all future sessions.</span></span>

[<span data-ttu-id="6a59a-162">Meer informatie over het koppelen van Azure file shares tooCloud Shell.</span><span class="sxs-lookup"><span data-stu-id="6a59a-162">Learn more about attaching Azure file shares tooCloud Shell.</span></span>](persisting-shell-storage.md)

## <a name="next-steps"></a><span data-ttu-id="6a59a-163">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="6a59a-163">Next steps</span></span>
[<span data-ttu-id="6a59a-164">Cloud-Shell Quick Start</span><span class="sxs-lookup"><span data-stu-id="6a59a-164">Cloud Shell Quickstart</span></span>](quickstart.md) <br><span data-ttu-id="6a59a-165">
[Meer informatie over Azure CLI 2.0](https://docs.microsoft.com/cli/azure/)</span><span class="sxs-lookup"><span data-stu-id="6a59a-165">
[Learn about Azure CLI 2.0](https://docs.microsoft.com/cli/azure/)</span></span> <br>
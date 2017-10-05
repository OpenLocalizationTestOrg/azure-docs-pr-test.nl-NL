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
# <a name="features-and-tools-for-azure-cloud-shell"></a><span data-ttu-id="abedb-103">Functies en hulpprogramma's voor Azure-Cloud-Shell</span><span class="sxs-lookup"><span data-stu-id="abedb-103">Features and Tools for Azure Cloud Shell</span></span>
<span data-ttu-id="abedb-104">Azure Cloud-Shell is een browser gebaseerde shell-ervaring te beheren en ontwikkelen van Azure-resources.</span><span class="sxs-lookup"><span data-stu-id="abedb-104">Azure Cloud Shell is a browser-based shell experience to manage and develop Azure resources.</span></span>

<span data-ttu-id="abedb-105">Cloud-Shell biedt een shell browser toegankelijk, vooraf is geconfigureerd voor het beheren van Azure-resources zonder de overhead voor het installeren van versies, en onderhouden van een machine.</span><span class="sxs-lookup"><span data-stu-id="abedb-105">Cloud Shell offers a browser-accessible, pre-configured shell experience for managing Azure resources without the overhead of installing, versioning, and maintaining a machine yourself.</span></span>

<span data-ttu-id="abedb-106">Cloud-Shell richt machines op basis van per aanvraag en als gevolg hiervan MACHINESTATUS niet behouden over de sessies.</span><span class="sxs-lookup"><span data-stu-id="abedb-106">Cloud Shell provisions machines on a per-request basis and as a result machine state will not persist across sessions.</span></span> <span data-ttu-id="abedb-107">Aangezien Cloud Shell is gebouwd voor interactieve sessies, wordt de houders automatisch opgeheven na 20 minuten van inactiviteit shell.</span><span class="sxs-lookup"><span data-stu-id="abedb-107">Since Cloud Shell is built for interactive sessions, shells automatically terminate after 20 minutes of shell inactivity.</span></span>

## <a name="bash-in-cloud-shell"></a><span data-ttu-id="abedb-108">In de Cloud-Shell Bash</span><span class="sxs-lookup"><span data-stu-id="abedb-108">Bash in Cloud Shell</span></span>
### <a name="tools"></a><span data-ttu-id="abedb-109">Hulpprogramma's</span><span class="sxs-lookup"><span data-stu-id="abedb-109">Tools</span></span>
|<span data-ttu-id="abedb-110">Category</span><span class="sxs-lookup"><span data-stu-id="abedb-110">Category</span></span>   |<span data-ttu-id="abedb-111">Naam</span><span class="sxs-lookup"><span data-stu-id="abedb-111">Name</span></span>   |
|---|---|
|<span data-ttu-id="abedb-112">Linux shell-interpreter</span><span class="sxs-lookup"><span data-stu-id="abedb-112">Linux shell interpreter</span></span>|<span data-ttu-id="abedb-113">Bash</span><span class="sxs-lookup"><span data-stu-id="abedb-113">Bash</span></span><br> <span data-ttu-id="abedb-114">servicel</span><span class="sxs-lookup"><span data-stu-id="abedb-114">sh</span></span>               |
|<span data-ttu-id="abedb-115">Azure-hulpprogramma 's</span><span class="sxs-lookup"><span data-stu-id="abedb-115">Azure tools</span></span>            |<span data-ttu-id="abedb-116">[Azure CLI 2.0](https://github.com/Azure/azure-cli) en [1.0](https://github.com/Azure/azure-xplat-cli)</span><span class="sxs-lookup"><span data-stu-id="abedb-116">[Azure CLI 2.0](https://github.com/Azure/azure-cli) and [1.0](https://github.com/Azure/azure-xplat-cli)</span></span><br> [<span data-ttu-id="abedb-117">AzCopy</span><span class="sxs-lookup"><span data-stu-id="abedb-117">AzCopy</span></span>](https://docs.microsoft.com/azure/storage/storage-use-azcopy)<br> [<span data-ttu-id="abedb-118">Batch Shipyard</span><span class="sxs-lookup"><span data-stu-id="abedb-118">Batch Shipyard</span></span>](https://github.com/Azure/batch-shipyard)     |
|<span data-ttu-id="abedb-119">Teksteditors</span><span class="sxs-lookup"><span data-stu-id="abedb-119">Text editors</span></span>           |<span data-ttu-id="abedb-120">VIM</span><span class="sxs-lookup"><span data-stu-id="abedb-120">vim</span></span><br> <span data-ttu-id="abedb-121">nano</span><span class="sxs-lookup"><span data-stu-id="abedb-121">nano</span></span><br> <span data-ttu-id="abedb-122">emacs</span><span class="sxs-lookup"><span data-stu-id="abedb-122">emacs</span></span>       |
|<span data-ttu-id="abedb-123">Resourcebeheer</span><span class="sxs-lookup"><span data-stu-id="abedb-123">Source control</span></span>         |<span data-ttu-id="abedb-124">GIT</span><span class="sxs-lookup"><span data-stu-id="abedb-124">git</span></span>                    |
|<span data-ttu-id="abedb-125">Hulpprogramma's van build</span><span class="sxs-lookup"><span data-stu-id="abedb-125">Build tools</span></span>            |<span data-ttu-id="abedb-126">Maken</span><span class="sxs-lookup"><span data-stu-id="abedb-126">make</span></span><br> <span data-ttu-id="abedb-127">maven</span><span class="sxs-lookup"><span data-stu-id="abedb-127">maven</span></span><br> <span data-ttu-id="abedb-128">npm</span><span class="sxs-lookup"><span data-stu-id="abedb-128">npm</span></span><br> <span data-ttu-id="abedb-129">PIP</span><span class="sxs-lookup"><span data-stu-id="abedb-129">pip</span></span>         |
|<span data-ttu-id="abedb-130">Containers</span><span class="sxs-lookup"><span data-stu-id="abedb-130">Containers</span></span>             |<span data-ttu-id="abedb-131">[Docker CLI](https://github.com/docker/cli)/[Docker-Machine](https://github.com/docker/machine)</span><span class="sxs-lookup"><span data-stu-id="abedb-131">[Docker CLI](https://github.com/docker/cli)/[Docker Machine](https://github.com/docker/machine)</span></span><br> [<span data-ttu-id="abedb-132">Kubectl</span><span class="sxs-lookup"><span data-stu-id="abedb-132">Kubectl</span></span>](https://kubernetes.io/docs/user-guide/kubectl-overview/)<br> [<span data-ttu-id="abedb-133">Concept</span><span class="sxs-lookup"><span data-stu-id="abedb-133">Draft</span></span>](https://github.com/Azure/draft)<br> [<span data-ttu-id="abedb-134">DC/OS CLI</span><span class="sxs-lookup"><span data-stu-id="abedb-134">DC/OS CLI</span></span>](https://github.com/dcos/dcos-cli)         |
|<span data-ttu-id="abedb-135">Databases</span><span class="sxs-lookup"><span data-stu-id="abedb-135">Databases</span></span>              |<span data-ttu-id="abedb-136">MySQL-client</span><span class="sxs-lookup"><span data-stu-id="abedb-136">MySQL client</span></span><br> <span data-ttu-id="abedb-137">PostgreSql-client</span><span class="sxs-lookup"><span data-stu-id="abedb-137">PostgreSql client</span></span><br> [<span data-ttu-id="abedb-138">Sqlcmd-hulpprogramma</span><span class="sxs-lookup"><span data-stu-id="abedb-138">sqlcmd Utility</span></span>](https://docs.microsoft.com/sql/tools/sqlcmd-utility)<br> [<span data-ttu-id="abedb-139">MSSQL-scripts</span><span class="sxs-lookup"><span data-stu-id="abedb-139">mssql-scripter</span></span>](https://github.com/Microsoft/sql-xplat-cli) |
|<span data-ttu-id="abedb-140">Overige</span><span class="sxs-lookup"><span data-stu-id="abedb-140">Other</span></span>                  |<span data-ttu-id="abedb-141">iPython Client</span><span class="sxs-lookup"><span data-stu-id="abedb-141">iPython Client</span></span><br> [<span data-ttu-id="abedb-142">Cloud Foundry CLI</span><span class="sxs-lookup"><span data-stu-id="abedb-142">Cloud Foundry CLI</span></span>](https://github.com/cloudfoundry/cli)<br> |

### <a name="language-support"></a><span data-ttu-id="abedb-143">Taalondersteuning</span><span class="sxs-lookup"><span data-stu-id="abedb-143">Language support</span></span>
|<span data-ttu-id="abedb-144">Taal</span><span class="sxs-lookup"><span data-stu-id="abedb-144">Language</span></span>   |<span data-ttu-id="abedb-145">Versie</span><span class="sxs-lookup"><span data-stu-id="abedb-145">Version</span></span>   |
|---|---|
|<span data-ttu-id="abedb-146">.NET</span><span class="sxs-lookup"><span data-stu-id="abedb-146">.NET</span></span>       |<span data-ttu-id="abedb-147">1.01</span><span class="sxs-lookup"><span data-stu-id="abedb-147">1.01</span></span>       |
|<span data-ttu-id="abedb-148">Aan de slag</span><span class="sxs-lookup"><span data-stu-id="abedb-148">Go</span></span>         |<span data-ttu-id="abedb-149">1.7</span><span class="sxs-lookup"><span data-stu-id="abedb-149">1.7</span></span>        |
|<span data-ttu-id="abedb-150">Java</span><span class="sxs-lookup"><span data-stu-id="abedb-150">Java</span></span>       |<span data-ttu-id="abedb-151">1.8</span><span class="sxs-lookup"><span data-stu-id="abedb-151">1.8</span></span>        |
|<span data-ttu-id="abedb-152">Node.js</span><span class="sxs-lookup"><span data-stu-id="abedb-152">Node.js</span></span>    |<span data-ttu-id="abedb-153">6.9.4</span><span class="sxs-lookup"><span data-stu-id="abedb-153">6.9.4</span></span>      |
|<span data-ttu-id="abedb-154">Python</span><span class="sxs-lookup"><span data-stu-id="abedb-154">Python</span></span>     |<span data-ttu-id="abedb-155">2.7 en 3.5 (standaard)</span><span class="sxs-lookup"><span data-stu-id="abedb-155">2.7 and 3.5 (default)</span></span>|

## <a name="secure-automatic-authentication"></a><span data-ttu-id="abedb-156">Automatische verificatie beveiligen</span><span class="sxs-lookup"><span data-stu-id="abedb-156">Secure automatic authentication</span></span>
<span data-ttu-id="abedb-157">Cloud-Shell verifieert veilig en automatisch accounttoegang voor Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="abedb-157">Cloud Shell securely and automatically authenticates account access for the Azure CLI 2.0.</span></span>

## <a name="azure-files-persistence"></a><span data-ttu-id="abedb-158">Azure bestanden persistentie</span><span class="sxs-lookup"><span data-stu-id="abedb-158">Azure Files persistence</span></span>
<span data-ttu-id="abedb-159">Omdat Cloud Shell is toegewezen op basis van gebruik van een tijdelijke machine per aanvraag, bestanden buiten de status van uw $Home en de machine zijn niet permanent opgeslagen over de sessies.</span><span class="sxs-lookup"><span data-stu-id="abedb-159">Since Cloud Shell is allocated on a per-request basis using a temporary machine, files outside of your $Home and machine state are not persisted across sessions.</span></span>
<span data-ttu-id="abedb-160">Om te blijven behouden bestanden over de sessies, helpt Cloud Shell u bij het koppelen van een Azure-bestandsshare op de eerste keer opstarten.</span><span class="sxs-lookup"><span data-stu-id="abedb-160">To persist files across sessions, Cloud Shell walks you through attaching an Azure file share on first launch.</span></span>
<span data-ttu-id="abedb-161">Wanneer u klaar Cloud Shell wordt automatisch koppelen van uw opslag voor alle toekomstige sessies.</span><span class="sxs-lookup"><span data-stu-id="abedb-161">Once completed Cloud Shell will automatically attach your storage for all future sessions.</span></span>

[<span data-ttu-id="abedb-162">Meer informatie over de Azure-bestandsshares gekoppeld aan Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="abedb-162">Learn more about attaching Azure file shares to Cloud Shell.</span></span>](persisting-shell-storage.md)

## <a name="next-steps"></a><span data-ttu-id="abedb-163">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="abedb-163">Next steps</span></span>
[<span data-ttu-id="abedb-164">Cloud-Shell Quick Start</span><span class="sxs-lookup"><span data-stu-id="abedb-164">Cloud Shell Quickstart</span></span>](quickstart.md) <br><span data-ttu-id="abedb-165">
[Meer informatie over Azure CLI 2.0](https://docs.microsoft.com/cli/azure/)</span><span class="sxs-lookup"><span data-stu-id="abedb-165">
[Learn about Azure CLI 2.0](https://docs.microsoft.com/cli/azure/)</span></span> <br>
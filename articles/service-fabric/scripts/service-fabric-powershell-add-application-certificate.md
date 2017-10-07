---
title: aaaAzure PowerShell-voorbeeldscript - toepassing cert tooa cluster toevoegen | Microsoft Docs
description: Azure PowerShell-Script voorbeeld - een toepassing certificaat tooa Service Fabric-cluster toevoegen.
services: service-fabric
documentationcenter: 
author: rwike77
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: service-fabric
ms.workload: multiple
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: ryanwi
ms.custom: mvc
ms.openlocfilehash: aba62598e2e4775012f89b5070bef5e61aec64f6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="add-an-application-certificate-tooa-service-fabric-cluster"></a><span data-ttu-id="102c0-103">Een toepassing certificaat tooa Service Fabric-cluster toevoegen</span><span class="sxs-lookup"><span data-stu-id="102c0-103">Add an application certificate tooa Service Fabric cluster</span></span>

<span data-ttu-id="102c0-104">Dit voorbeeldscript wordt gemaakt van een zelfondertekend certificaat in Hallo opgegeven Azure sleutelkluis en installeert deze tooall knooppunten van Hallo Service Fabric-cluster.</span><span class="sxs-lookup"><span data-stu-id="102c0-104">This sample script creates a self-signed certificate in hello specified Azure key vault and installs it tooall nodes of hello Service Fabric cluster.</span></span> <span data-ttu-id="102c0-105">Hallo-certificaat gedownload ook tooa lokale map.</span><span class="sxs-lookup"><span data-stu-id="102c0-105">hello certificate also downloads tooa local folder.</span></span> <span data-ttu-id="102c0-106">Hallo-naam van Hallo gedownload certificaat is dezelfde is als naam van het certificaat in de sleutelkluis Hallo Hallo HALLO hallo.</span><span class="sxs-lookup"><span data-stu-id="102c0-106">hello name of hello downloaded certificate is hello same as hello name of hello certificate in hello key vault.</span></span> <span data-ttu-id="102c0-107">Hallo parameters aanpassen indien nodig.</span><span class="sxs-lookup"><span data-stu-id="102c0-107">Customize hello parameters as needed.</span></span>

<span data-ttu-id="102c0-108">Installeer zo nodig hello Azure PowerShell met de instructie Hallo in Hallo gevonden [Azure PowerShell handleiding](/powershell/azure/overview) en voer vervolgens `Login-AzureRmAccount` toocreate een verbinding met Azure.</span><span class="sxs-lookup"><span data-stu-id="102c0-108">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](/powershell/azure/overview) and then run `Login-AzureRmAccount` toocreate a connection with Azure.</span></span> 

## <a name="sample-script"></a><span data-ttu-id="102c0-109">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="102c0-109">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/service-fabric/add-application-certificate/add-new-application-certificate.ps1 "Add an application certificate tooa cluster")]

## <a name="script-explanation"></a><span data-ttu-id="102c0-110">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="102c0-110">Script explanation</span></span>

<span data-ttu-id="102c0-111">Dit script maakt gebruik van Hallo opdrachten te volgen: elke opdracht in de tabel Hallo koppelingen toocommand specifieke documentatie.</span><span class="sxs-lookup"><span data-stu-id="102c0-111">This script uses hello following commands: Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="102c0-112">Opdracht</span><span class="sxs-lookup"><span data-stu-id="102c0-112">Command</span></span> | <span data-ttu-id="102c0-113">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="102c0-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="102c0-114">Voeg AzureRmServiceFabricApplicationCertificate</span><span class="sxs-lookup"><span data-stu-id="102c0-114">Add-AzureRmServiceFabricApplicationCertificate</span></span>](/powershell/module/azurerm.servicefabric/Add-AzureRmServiceFabricApplicationCertificate) | <span data-ttu-id="102c0-115">Voeg dat een nieuwe toepassing certificaat toohello virtuele-machineschaalset waaruit Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="102c0-115">Add a new application certificate toohello virtual machine scale set that make up hello cluster.</span></span>  |

## <a name="next-steps"></a><span data-ttu-id="102c0-116">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="102c0-116">Next steps</span></span>

<span data-ttu-id="102c0-117">Zie voor meer informatie over hello Azure PowerShell-module [documentatie van Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="102c0-117">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="102c0-118">Aanvullende voorbeelden van de Azure Powershell voor Azure Service Fabric vindt u in Hallo [voorbeelden van Azure PowerShell](../service-fabric-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="102c0-118">Additional Azure Powershell samples for Azure Service Fabric can be found in hello [Azure PowerShell samples](../service-fabric-powershell-samples.md).</span></span>

---
title: Azure PowerShell-Script steekproef - certificaat van de toepassing toevoegen aan een cluster | Microsoft Docs
description: 'Azure PowerShell-Script voorbeeld: een toepassingscertificaat toevoegen aan een Service Fabric-cluster.'
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
ms.openlocfilehash: 9ccd6bb0458bc03e52103fa70cad26bd6bf98bd5
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/29/2017
---
# <a name="add-an-application-certificate-to-a-service-fabric-cluster"></a><span data-ttu-id="64e0b-103">Het toepassingscertificaat van een toevoegen aan een Service Fabric-cluster</span><span class="sxs-lookup"><span data-stu-id="64e0b-103">Add an application certificate to a Service Fabric cluster</span></span>

<span data-ttu-id="64e0b-104">Dit voorbeeldscript wordt een zelfondertekend certificaat gemaakt in de opgegeven Azure sleutelkluis en installeert deze met alle knooppunten van het Service Fabric-cluster.</span><span class="sxs-lookup"><span data-stu-id="64e0b-104">This sample script creates a self-signed certificate in the specified Azure key vault and installs it to all nodes of the Service Fabric cluster.</span></span> <span data-ttu-id="64e0b-105">Het certificaat kan ook worden gedownload naar een lokale map.</span><span class="sxs-lookup"><span data-stu-id="64e0b-105">The certificate also downloads to a local folder.</span></span> <span data-ttu-id="64e0b-106">De naam van het gedownloade certificaat is dezelfde als de naam van het certificaat in de sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="64e0b-106">The name of the downloaded certificate is the same as the name of the certificate in the key vault.</span></span> <span data-ttu-id="64e0b-107">Pas de parameters zo nodig.</span><span class="sxs-lookup"><span data-stu-id="64e0b-107">Customize the parameters as needed.</span></span>

<span data-ttu-id="64e0b-108">Installeer zo nodig de Azure PowerShell met de instructie gevonden in de [Azure PowerShell handleiding](/powershell/azure/overview) en voer vervolgens `Login-AzureRmAccount` geen verbinding maken met Azure.</span><span class="sxs-lookup"><span data-stu-id="64e0b-108">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](/powershell/azure/overview) and then run `Login-AzureRmAccount` to create a connection with Azure.</span></span> 

## <a name="sample-script"></a><span data-ttu-id="64e0b-109">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="64e0b-109">Sample script</span></span>

<span data-ttu-id="64e0b-110">[!code-powershell[belangrijkste](../../../powershell_scripts/service-fabric/add-application-certificate/add-new-application-certificate.ps1 "een toepassingscertificaat toevoegen aan een cluster")]</span><span class="sxs-lookup"><span data-stu-id="64e0b-110">[!code-powershell[main](../../../powershell_scripts/service-fabric/add-application-certificate/add-new-application-certificate.ps1 "Add an application certificate to a cluster")]</span></span>

## <a name="script-explanation"></a><span data-ttu-id="64e0b-111">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="64e0b-111">Script explanation</span></span>

<span data-ttu-id="64e0b-112">Dit script maakt gebruik van de volgende opdrachten: elke opdracht in de tabel is gekoppeld aan de specifieke documentatie opdracht.</span><span class="sxs-lookup"><span data-stu-id="64e0b-112">This script uses the following commands: Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="64e0b-113">Opdracht</span><span class="sxs-lookup"><span data-stu-id="64e0b-113">Command</span></span> | <span data-ttu-id="64e0b-114">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="64e0b-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="64e0b-115">Voeg AzureRmServiceFabricApplicationCertificate</span><span class="sxs-lookup"><span data-stu-id="64e0b-115">Add-AzureRmServiceFabricApplicationCertificate</span></span>](/powershell/module/azurerm.servicefabric/Add-AzureRmServiceFabricApplicationCertificate) | <span data-ttu-id="64e0b-116">Een nieuw toepassingscertificaat toevoegen aan de virtuele-machineschaalset waaruit het cluster.</span><span class="sxs-lookup"><span data-stu-id="64e0b-116">Add a new application certificate to the virtual machine scale set that make up the cluster.</span></span>  |

## <a name="next-steps"></a><span data-ttu-id="64e0b-117">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="64e0b-117">Next steps</span></span>

<span data-ttu-id="64e0b-118">Zie voor meer informatie over de Azure PowerShell-module [documentatie van Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="64e0b-118">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="64e0b-119">Aanvullende voorbeelden van de Azure Powershell voor Azure Service Fabric vindt u in de [voorbeelden van Azure PowerShell](../service-fabric-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="64e0b-119">Additional Azure Powershell samples for Azure Service Fabric can be found in the [Azure PowerShell samples](../service-fabric-powershell-samples.md).</span></span>

---
title: Azure PowerShell-klassiek de load balancer - aaaCreate een internetgerichte | Microsoft Docs
description: Meer informatie over hoe de toocreate een Internet gerichte load balancer in de klassieke modus met behulp van PowerShell
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-service-management
ms.assetid: 73e8bfa4-8086-4ef0-9e35-9e00b24be319
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 76d9a712a0acda223fc86b80be9c35c0ed9f3a50
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-creating-an-internet-facing-load-balancer-classic-in-powershell"></a><span data-ttu-id="d08f6-103">Aan de slag met het maken van een internetgerichte load balancer (klassiek) in PowerShell</span><span class="sxs-lookup"><span data-stu-id="d08f6-103">Get started creating an Internet facing load balancer (classic) in PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="d08f6-104">klassieke Azure-portal</span><span class="sxs-lookup"><span data-stu-id="d08f6-104">Azure classic portal</span></span>](../load-balancer/load-balancer-get-started-internet-classic-portal.md)
> * [<span data-ttu-id="d08f6-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d08f6-105">PowerShell</span></span>](../load-balancer/load-balancer-get-started-internet-classic-ps.md)
> * [<span data-ttu-id="d08f6-106">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="d08f6-106">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-internet-classic-cli.md)
> * [<span data-ttu-id="d08f6-107">Azure Cloud Services</span><span class="sxs-lookup"><span data-stu-id="d08f6-107">Azure Cloud Services</span></span>](../load-balancer/load-balancer-get-started-internet-classic-cloud.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

> [!IMPORTANT]
> <span data-ttu-id="d08f6-108">Voordat u met Azure-resources werkt, is het belangrijk toounderstand dat Azure momenteel twee implementatiemodellen heeft: Azure Resource Manager en het klassieke model.</span><span class="sxs-lookup"><span data-stu-id="d08f6-108">Before you work with Azure resources, it's important toounderstand that Azure currently has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="d08f6-109">Zorg ervoor dat u begrijpt wat [implementatiemodellen en hulpprogramma's](../azure-classic-rm.md) zijn voordat u met een Azure-resource gaat werken.</span><span class="sxs-lookup"><span data-stu-id="d08f6-109">Make sure you understand [deployment models and tools](../azure-classic-rm.md) before you work with any Azure resource.</span></span> <span data-ttu-id="d08f6-110">U kunt Hallo-documentatie voor verschillende hulpprogramma's bekijken door te klikken op de tabbladen Hallo Hallo boven aan dit artikel.</span><span class="sxs-lookup"><span data-stu-id="d08f6-110">You can view hello documentation for different tools by clicking hello tabs at hello top of this article.</span></span> <span data-ttu-id="d08f6-111">In dit artikel bevat informatie over Hallo klassieke implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="d08f6-111">This article covers hello classic deployment model.</span></span> <span data-ttu-id="d08f6-112">U kunt ook [meer informatie over hoe een internetverbinding toocreate netwerktaakverdeler met Azure Resource Manager](load-balancer-get-started-internet-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="d08f6-112">You can also [Learn how toocreate an Internet facing load balancer using Azure Resource Manager](load-balancer-get-started-internet-arm-ps.md).</span></span>

[!INCLUDE [load-balancer-get-started-internet-scenario-include.md](../../includes/load-balancer-get-started-internet-scenario-include.md)]

## <a name="set-up-load-balancer-using-powershell"></a><span data-ttu-id="d08f6-113">Een load balancer instellen met behulp van PowerShell</span><span class="sxs-lookup"><span data-stu-id="d08f6-113">Set up load balancer using PowerShell</span></span>

<span data-ttu-id="d08f6-114">tooset van een load balancer met behulp van powershell, Hallo volgende stappen:</span><span class="sxs-lookup"><span data-stu-id="d08f6-114">tooset up a load balancer using powershell, follow hello steps below:</span></span>

1. <span data-ttu-id="d08f6-115">Als u Azure PowerShell nog nooit hebt gebruikt, raadpleegt u [hoe tooInstall en configureer Azure PowerShell](/powershell/azure/overview) en volg de instructies Hallo alle Hallo manier toohello toosign beëindigen in Azure en uw abonnement te selecteren.</span><span class="sxs-lookup"><span data-stu-id="d08f6-115">If you have never used Azure PowerShell, see [How tooInstall and Configure Azure PowerShell](/powershell/azure/overview) and follow hello instructions all hello way toohello end toosign into Azure and select your subscription.</span></span>
2. <span data-ttu-id="d08f6-116">Nadat een virtuele machine is gemaakt, kunt u PowerShell-cmdlets tooadd een load balancer tooa virtuele machine binnen Hallo dezelfde cloudservice.</span><span class="sxs-lookup"><span data-stu-id="d08f6-116">After creating a virtual machine, you can use PowerShell cmdlets tooadd a load balancer tooa virtual machine within hello same cloud service.</span></span>

<span data-ttu-id="d08f6-117">In Hallo naam volgende voorbeeld voegt u toe een load balancer-set aangeroepen toocloud 'webfarm' service 'mytestcloud' (of myctestcloud.cloudapp.net) toe te voegen Hallo eindpunten voor Hallo load balancer toovirtual machines 'web1' en 'web2'.</span><span class="sxs-lookup"><span data-stu-id="d08f6-117">In hello following example you will add a load balancer set called "webfarm" toocloud service "mytestcloud" (or myctestcloud.cloudapp.net) , adding hello endpoints for hello load balancer toovirtual machines named "web1" and "web2".</span></span> <span data-ttu-id="d08f6-118">Hallo load balancer ontvangt netwerkverkeer op poort 80 en een compromis tussen de werklast tussen Hallo virtuele machines zijn gedefinieerd door het lokale eindpunt hello (in dit geval poort 80) via TCP.</span><span class="sxs-lookup"><span data-stu-id="d08f6-118">hello load balancer receives network traffic on port 80 and load balances between hello virtual machines defined by hello local endpoint (in this case port 80) using TCP.</span></span>

### <a name="step-1"></a><span data-ttu-id="d08f6-119">Stap 1</span><span class="sxs-lookup"><span data-stu-id="d08f6-119">Step 1</span></span>

<span data-ttu-id="d08f6-120">Een eindpunt van de taakverdeling voor de eerste VM 'web1' hello maken</span><span class="sxs-lookup"><span data-stu-id="d08f6-120">Create a load balanced endpoint for hello first VM "web1"</span></span>

```powershell
Get-AzureVM -ServiceName "mytestcloud" -Name "web1" | Add-AzureEndpoint -Name "HttpIn" -Protocol "tcp" -PublicPort 80 -LocalPort 80 -LBSetName "WebFarm" -ProbePort 80 -ProbeProtocol "http" -ProbePath '/' | Update-AzureVM
```

### <a name="step-2"></a><span data-ttu-id="d08f6-121">Stap 2</span><span class="sxs-lookup"><span data-stu-id="d08f6-121">Step 2</span></span>

<span data-ttu-id="d08f6-122">Maken van een ander eindpunt voor hello tweede VM 'web2' hello met dezelfde load balancer setnaam</span><span class="sxs-lookup"><span data-stu-id="d08f6-122">Create another endpoint for hello second VM  "web2" using hello same load balancer set name</span></span>

```powershell
Get-AzureVM -ServiceName "mytestcloud" -Name "web2" | Add-AzureEndpoint -Name "HttpIn" -Protocol "tcp" -PublicPort 80 -LocalPort 80 -LBSetName "WebFarm" -ProbePort 80 -ProbeProtocol "http" -ProbePath '/' | Update-AzureVM
```

## <a name="remove-a-virtual-machine-from-a-load-balancer"></a><span data-ttu-id="d08f6-123">Verwijder een virtuele machine uit een load balancer</span><span class="sxs-lookup"><span data-stu-id="d08f6-123">Remove a virtual machine from a load balancer</span></span>

<span data-ttu-id="d08f6-124">U kunt verwijderen AzureEndpoint tooremove een eindpunt van de virtuele machine van Hallo load balancer</span><span class="sxs-lookup"><span data-stu-id="d08f6-124">You can use Remove-AzureEndpoint tooremove a virtual machine endpoint from hello load balancer</span></span>

```powershell
Get-azureVM -ServiceName mytestcloud  -Name web1 |Remove-AzureEndpoint -Name httpin | Update-AzureVM
```

## <a name="next-steps"></a><span data-ttu-id="d08f6-125">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="d08f6-125">Next steps</span></span>

<span data-ttu-id="d08f6-126">U kunt ook [aan de slag gaan met het maken van een interne load balancer](load-balancer-get-started-ilb-classic-ps.md) en configureren welk type [distributiemodus](load-balancer-distribution-mode.md) er moet worden gebruikt voor specifiek gedrag voor netwerkverkeer van de load balancer.</span><span class="sxs-lookup"><span data-stu-id="d08f6-126">You can also [get started creating an internal load balancer](load-balancer-get-started-ilb-classic-ps.md) and configure what type of [distribution mode](load-balancer-distribution-mode.md) for a specific load balancer network traffic behavior.</span></span>

<span data-ttu-id="d08f6-127">Als uw toepassing tookeep verbindingen voor servers achter een load balancer actief is moet, kunt u meer begrip over [inactieve TCP-time-outinstellingen voor een load balancer](load-balancer-tcp-idle-timeout.md).</span><span class="sxs-lookup"><span data-stu-id="d08f6-127">If your application needs tookeep connections alive for servers behind a load balancer, you can understand more about [idle TCP timeout settings for a load balancer](load-balancer-tcp-idle-timeout.md).</span></span> <span data-ttu-id="d08f6-128">Dit helpt toolearn over niet-actieve Verbindingsgedrag wanneer u van Azure Load Balancer gebruikmaakt.</span><span class="sxs-lookup"><span data-stu-id="d08f6-128">It will help toolearn about idle connection behavior when you are using Azure Load Balancer.</span></span>

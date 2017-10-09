---
title: een Azure-cloud-service in Windows PowerShell aaaScale | Microsoft Docs
description: (klassiek) Meer informatie over hoe toouse PowerShell tooscale een Webrol of worker-rol in of uit in Azure.
services: cloud-services
documentationcenter: 
author: mmccrory
manager: timlt
editor: 
ms.assetid: ee37dd8c-6714-4c61-adb8-03d6bbf76c9a
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/01/2016
ms.author: mmccrory
ms.openlocfilehash: cfac6660e84f8ae24e4e9bdd5bf2016fb9cd7045
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooscale-a-cloud-service-in-powershell"></a><span data-ttu-id="9072f-103">Hoe tooscale een cloud-service in PowerShell</span><span class="sxs-lookup"><span data-stu-id="9072f-103">How tooscale a cloud service in PowerShell</span></span>

<span data-ttu-id="9072f-104">Kunt u Windows PowerShell tooscale een Webrol of worker-rol in- of door toe te voegen of te verwijderen van exemplaren.</span><span class="sxs-lookup"><span data-stu-id="9072f-104">You can use Windows PowerShell tooscale a web role or worker role in or out by adding or removing instances.</span></span>  

## <a name="log-in-tooazure"></a><span data-ttu-id="9072f-105">Meld u bij tooAzure</span><span class="sxs-lookup"><span data-stu-id="9072f-105">Log in tooAzure</span></span>

<span data-ttu-id="9072f-106">Voordat u geen bewerkingen uit op uw abonnement via PowerShell uitvoeren kunt, moet u zich aanmeldt:</span><span class="sxs-lookup"><span data-stu-id="9072f-106">Before you can perform any operations on your subscription through PowerShell, you must log in:</span></span>

```powershell
Add-AzureAccount
```

<span data-ttu-id="9072f-107">Als u meerdere abonnementen die zijn gekoppeld aan uw account hebt, moet u mogelijk toochange Hallo huidige abonnement, afhankelijk van waar uw cloudservice zich bevindt.</span><span class="sxs-lookup"><span data-stu-id="9072f-107">If you have multiple subscriptions associated with your account, you may need toochange hello current subscription depending on where your cloud service resides.</span></span> <span data-ttu-id="9072f-108">toocheck hello huidige abonnement, uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="9072f-108">toocheck hello current subscription, run:</span></span>

```powershell
Get-AzureSubscription -Current
```

<span data-ttu-id="9072f-109">Als u toochange Hallo huidige abonnement moet, uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="9072f-109">If you need toochange hello current subscription, run:</span></span>

```powershell
Set-AzureSubscription -SubscriptionId <subscription_id>
```

## <a name="check-hello-current-instance-count-for-your-role"></a><span data-ttu-id="9072f-110">Hallo huidige aantal exemplaren voor uw rol controleren</span><span class="sxs-lookup"><span data-stu-id="9072f-110">Check hello current instance count for your role</span></span>

<span data-ttu-id="9072f-111">toocheck hello huidige status van uw rol uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="9072f-111">toocheck hello current state of your role, run:</span></span>

```powershell
Get-AzureRole -ServiceName '<your_service_name>' -RoleName '<your_role_name>'
```

<span data-ttu-id="9072f-112">Ontvangt u informatie over het Hallo-functie, inclusief de huidige OS-versie en exemplaar aantal.</span><span class="sxs-lookup"><span data-stu-id="9072f-112">You should get back information about hello role, including its current OS version and instance count.</span></span> <span data-ttu-id="9072f-113">In dit geval heeft Hallo rol één exemplaar.</span><span class="sxs-lookup"><span data-stu-id="9072f-113">In this case, hello role has a single instance.</span></span>

![Informatie over het Hallo-rol](./media/cloud-services-how-to-scale-powershell/get-azure-role.png)

## <a name="scale-out-hello-role-by-adding-more-instances"></a><span data-ttu-id="9072f-115">Hallo rol uitbreiden door meer exemplaren toe te voegen</span><span class="sxs-lookup"><span data-stu-id="9072f-115">Scale out hello role by adding more instances</span></span>

<span data-ttu-id="9072f-116">tooscale uit uw rol pass Hallo gewenst aantal exemplaren als Hallo **aantal** parameter toohello **Set AzureRole** cmdlet:</span><span class="sxs-lookup"><span data-stu-id="9072f-116">tooscale out your role, pass hello desired number of instances as hello **Count** parameter toohello **Set-AzureRole** cmdlet:</span></span>

```powershell
Set-AzureRole -ServiceName '<your_service_name>' -RoleName '<your_role_name>' -Slot <target_slot> -Count <desired_instances>
```

<span data-ttu-id="9072f-117">Hallo cmdlet blokken tijdelijk worden tijdens het Hallo nieuwe exemplaren worden ingericht en gestart.</span><span class="sxs-lookup"><span data-stu-id="9072f-117">hello cmdlet blocks momentarily while hello new instances are provisioned and started.</span></span> <span data-ttu-id="9072f-118">Tijdens deze periode, als u een nieuwe PowerShell-venster en aanroep openen **Get-AzureRole** zoals eerder besproken, ziet u de nieuwe doel Hallo-exemplaren.</span><span class="sxs-lookup"><span data-stu-id="9072f-118">During this time, if you open a new PowerShell window and call **Get-AzureRole** as shown earlier, you will see hello new target instance count.</span></span> <span data-ttu-id="9072f-119">En als u Hallo Rolstatus in Hallo-portal inspecteren, ziet u Hallo nieuw exemplaar gestart:</span><span class="sxs-lookup"><span data-stu-id="9072f-119">And if you inspect hello role status in hello portal, you should see hello new instance starting up:</span></span>

![VM-instantie in de portal wordt gestart](./media/cloud-services-how-to-scale-powershell/role-instance-starting.png)

<span data-ttu-id="9072f-121">Zodra nieuwe exemplaren van Hallo hebt gestart, wordt Hallo cmdlet is geretourneerd:</span><span class="sxs-lookup"><span data-stu-id="9072f-121">Once hello new instances have started, hello cmdlet will return successfully:</span></span>

![Rol exemplaar toename geslaagd](./media/cloud-services-how-to-scale-powershell/set-azure-role-success.png)

## <a name="scale-in-hello-role-by-removing-instances"></a><span data-ttu-id="9072f-123">In de rol Hallo schalen door het verwijderen van instanties</span><span class="sxs-lookup"><span data-stu-id="9072f-123">Scale in hello role by removing instances</span></span>

<span data-ttu-id="9072f-124">U kunt schalen in een rol door het verwijderen van instanties in Hallo dezelfde manier.</span><span class="sxs-lookup"><span data-stu-id="9072f-124">You can scale in a role by removing instances in hello same way.</span></span> <span data-ttu-id="9072f-125">Set Hallo **aantal** parameter op **Set AzureRole** toohello aantal exemplaren dat u wilt toohave nadat Hallo schaal in de bewerking voltooid is.</span><span class="sxs-lookup"><span data-stu-id="9072f-125">Set hello **Count** parameter on **Set-AzureRole** toohello number of instances you want toohave after hello scale in operation is complete.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9072f-126">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="9072f-126">Next steps</span></span>

<span data-ttu-id="9072f-127">Het is niet mogelijk tooconfigure automatisch geschaald voor cloudservices van PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9072f-127">It is not possible tooconfigure auto-scale for cloud services from PowerShell.</span></span> <span data-ttu-id="9072f-128">toodo die Zie [hoe tooauto schalen voor een cloudservice](cloud-services-how-to-scale-portal.md).</span><span class="sxs-lookup"><span data-stu-id="9072f-128">toodo that, see [How tooauto scale a cloud service](cloud-services-how-to-scale-portal.md).</span></span>

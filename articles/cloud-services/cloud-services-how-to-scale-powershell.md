---
title: Een Azure-cloud-service schalen in Windows PowerShell | Microsoft Docs
description: (klassiek) Informatie over het gebruiken van PowerShell een Webrol of worker-rol in of uit te schalen in Azure.
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
ms.openlocfilehash: a7ae8ff202d403dff19b8c9a6a09492235db27ac
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-scale-a-cloud-service-in-powershell"></a><span data-ttu-id="08103-103">Schalen van een cloudservice in PowerShell</span><span class="sxs-lookup"><span data-stu-id="08103-103">How to scale a cloud service in PowerShell</span></span>

<span data-ttu-id="08103-104">Windows PowerShell kunt u een Webrol of worker-rol in- of schalen door het toevoegen of verwijderen van exemplaren.</span><span class="sxs-lookup"><span data-stu-id="08103-104">You can use Windows PowerShell to scale a web role or worker role in or out by adding or removing instances.</span></span>  

## <a name="log-in-to-azure"></a><span data-ttu-id="08103-105">Meld u aan bij Azure.</span><span class="sxs-lookup"><span data-stu-id="08103-105">Log in to Azure</span></span>

<span data-ttu-id="08103-106">Voordat u geen bewerkingen uit op uw abonnement via PowerShell uitvoeren kunt, moet u zich aanmeldt:</span><span class="sxs-lookup"><span data-stu-id="08103-106">Before you can perform any operations on your subscription through PowerShell, you must log in:</span></span>

```powershell
Add-AzureAccount
```

<span data-ttu-id="08103-107">Als u meerdere abonnementen die zijn gekoppeld aan uw account hebt, moet u wellicht wijzigen van het huidige abonnement, afhankelijk van waar uw cloudservice zich bevindt.</span><span class="sxs-lookup"><span data-stu-id="08103-107">If you have multiple subscriptions associated with your account, you may need to change the current subscription depending on where your cloud service resides.</span></span> <span data-ttu-id="08103-108">Als u wilt controleren in het huidige abonnement, uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="08103-108">To check the current subscription, run:</span></span>

```powershell
Get-AzureSubscription -Current
```

<span data-ttu-id="08103-109">Als u wijzigen van het huidige abonnement wilt, uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="08103-109">If you need to change the current subscription, run:</span></span>

```powershell
Set-AzureSubscription -SubscriptionId <subscription_id>
```

## <a name="check-the-current-instance-count-for-your-role"></a><span data-ttu-id="08103-110">Controleer het huidige aantal exemplaren voor uw rol</span><span class="sxs-lookup"><span data-stu-id="08103-110">Check the current instance count for your role</span></span>

<span data-ttu-id="08103-111">Als u wilt controleren in de huidige status van uw rol, worden uitgevoerd:</span><span class="sxs-lookup"><span data-stu-id="08103-111">To check the current state of your role, run:</span></span>

```powershell
Get-AzureRole -ServiceName '<your_service_name>' -RoleName '<your_role_name>'
```

<span data-ttu-id="08103-112">Ontvangt u informatie over de functie, inclusief de huidige OS-versie en exemplaar aantal.</span><span class="sxs-lookup"><span data-stu-id="08103-112">You should get back information about the role, including its current OS version and instance count.</span></span> <span data-ttu-id="08103-113">In dit geval heeft de rol één exemplaar.</span><span class="sxs-lookup"><span data-stu-id="08103-113">In this case, the role has a single instance.</span></span>

![Informatie over de rol](./media/cloud-services-how-to-scale-powershell/get-azure-role.png)

## <a name="scale-out-the-role-by-adding-more-instances"></a><span data-ttu-id="08103-115">De rol uitbreiden door meer exemplaren toe te voegen</span><span class="sxs-lookup"><span data-stu-id="08103-115">Scale out the role by adding more instances</span></span>

<span data-ttu-id="08103-116">Als u wilt uitbreiden uw rol, geeft u het gewenste aantal exemplaren als de **aantal** -parameter voor de **Set AzureRole** cmdlet:</span><span class="sxs-lookup"><span data-stu-id="08103-116">To scale out your role, pass the desired number of instances as the **Count** parameter to the **Set-AzureRole** cmdlet:</span></span>

```powershell
Set-AzureRole -ServiceName '<your_service_name>' -RoleName '<your_role_name>' -Slot <target_slot> -Count <desired_instances>
```

<span data-ttu-id="08103-117">De cmdlet-blokken tijdelijk worden tijdens de nieuwe exemplaren worden ingericht en gestart.</span><span class="sxs-lookup"><span data-stu-id="08103-117">The cmdlet blocks momentarily while the new instances are provisioned and started.</span></span> <span data-ttu-id="08103-118">Tijdens deze periode, als u een nieuwe PowerShell-venster en aanroep openen **Get-AzureRole** zoals eerder besproken, ziet u de nieuwe doel-exemplaren.</span><span class="sxs-lookup"><span data-stu-id="08103-118">During this time, if you open a new PowerShell window and call **Get-AzureRole** as shown earlier, you will see the new target instance count.</span></span> <span data-ttu-id="08103-119">En als u de Rolstatus van de in de portal inspecteren, ziet u het nieuwe exemplaar wordt opgestart:</span><span class="sxs-lookup"><span data-stu-id="08103-119">And if you inspect the role status in the portal, you should see the new instance starting up:</span></span>

![VM-instantie in de portal wordt gestart](./media/cloud-services-how-to-scale-powershell/role-instance-starting.png)

<span data-ttu-id="08103-121">Nadat de nieuwe exemplaren hebt gestart, wordt de cmdlet is geretourneerd:</span><span class="sxs-lookup"><span data-stu-id="08103-121">Once the new instances have started, the cmdlet will return successfully:</span></span>

![Rol exemplaar toename geslaagd](./media/cloud-services-how-to-scale-powershell/set-azure-role-success.png)

## <a name="scale-in-the-role-by-removing-instances"></a><span data-ttu-id="08103-123">In de rol schalen door het verwijderen van instanties</span><span class="sxs-lookup"><span data-stu-id="08103-123">Scale in the role by removing instances</span></span>

<span data-ttu-id="08103-124">U kunt een rol schalen door het verwijderen van instanties op dezelfde manier.</span><span class="sxs-lookup"><span data-stu-id="08103-124">You can scale in a role by removing instances in the same way.</span></span> <span data-ttu-id="08103-125">Stel de **aantal** parameter op **Set AzureRole** aan het aantal exemplaren dat u hebben wilt nadat de schaal in de bewerking voltooid is.</span><span class="sxs-lookup"><span data-stu-id="08103-125">Set the **Count** parameter on **Set-AzureRole** to the number of instances you want to have after the scale in operation is complete.</span></span>

## <a name="next-steps"></a><span data-ttu-id="08103-126">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="08103-126">Next steps</span></span>

<span data-ttu-id="08103-127">Het is niet mogelijk automatisch geschaald voor cloudservices vanuit PowerShell configureren.</span><span class="sxs-lookup"><span data-stu-id="08103-127">It is not possible to configure auto-scale for cloud services from PowerShell.</span></span> <span data-ttu-id="08103-128">Zie hiervoor [automatisch schalen een cloudservice](cloud-services-how-to-scale-portal.md).</span><span class="sxs-lookup"><span data-stu-id="08103-128">To do that, see [How to auto scale a cloud service](cloud-services-how-to-scale-portal.md).</span></span>

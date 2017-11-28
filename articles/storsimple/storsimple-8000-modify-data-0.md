---
title: Wijzigen van de DATA 0-instellingen op StorSimple 8000 series apparaat | Microsoft Docs
description: Informatie over het gebruik van Windows PowerShell voor StorSimple opnieuw configureren van de DATA 0-netwerkinterface op uw StorSimple-apparaat.
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/27/2017
ms.author: alkohli
ms.openlocfilehash: 90df43e22f17fd32fe642514df098b72700e77af
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="modify-the-data-0-network-interface-settings-on-your-storsimple-8000-series-device"></a><span data-ttu-id="5244e-103">De DATA 0 netwerkinterface-instellingen op uw StorSimple 8000 series apparaat wijzigen</span><span class="sxs-lookup"><span data-stu-id="5244e-103">Modify the DATA 0 network interface settings on your StorSimple 8000 series device</span></span>

## <a name="overview"></a><span data-ttu-id="5244e-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="5244e-104">Overview</span></span>

<span data-ttu-id="5244e-105">Uw Microsoft Azure StorSimple-apparaat heeft zes netwerkinterfaces van DATA 0 tot en met 5 van de gegevens.</span><span class="sxs-lookup"><span data-stu-id="5244e-105">Your Microsoft Azure StorSimple device has six network interfaces, from DATA 0 to DATA 5.</span></span> <span data-ttu-id="5244e-106">De DATA 0-interface is altijd geconfigureerd via de Windows PowerShell-interface of de seriële console en is automatisch ingeschakeld voor de cloud.</span><span class="sxs-lookup"><span data-stu-id="5244e-106">The DATA 0 interface is always configured through the Windows PowerShell interface or the serial console, and is automatically cloud-enabled.</span></span> <span data-ttu-id="5244e-107">Houd er rekening mee dat u kunt DATA 0-netwerkinterface via de Azure portal niet configureren.</span><span class="sxs-lookup"><span data-stu-id="5244e-107">Note that you cannot configure DATA 0 network interface through the Azure portal.</span></span>

<span data-ttu-id="5244e-108">De DATA 0 interface eerst wordt geconfigureerd via de wizard setup tijdens de eerste implementatie van het StorSimple-apparaat.</span><span class="sxs-lookup"><span data-stu-id="5244e-108">The DATA 0 interface is first configured through the setup wizard during initial deployment of the StorSimple device.</span></span> <span data-ttu-id="5244e-109">Wanneer het apparaat zich in een bedrijfsmodus, moet u mogelijk opnieuw configureren van DATA 0 instellingen.</span><span class="sxs-lookup"><span data-stu-id="5244e-109">When the device is in an operational mode, you may need to reconfigure DATA 0 settings.</span></span> <span data-ttu-id="5244e-110">Deze zelfstudie bestaat uit twee methoden voor het wijzigen van de DATA 0 netwerk beide via Windows PowerShell voor StorSimple-instellingen.</span><span class="sxs-lookup"><span data-stu-id="5244e-110">This tutorial provides two methods to modify DATA 0 network settings, both through Windows PowerShell for StorSimple.</span></span>

<span data-ttu-id="5244e-111">Na het lezen van deze zelfstudie, kunt u zich kunt:</span><span class="sxs-lookup"><span data-stu-id="5244e-111">After reading this tutorial, you will be able to:</span></span>

* <span data-ttu-id="5244e-112">Wijzigen van de DATA 0-instelling via de wizard setup-netwerk</span><span class="sxs-lookup"><span data-stu-id="5244e-112">Modify DATA 0 network setting through the setup wizard</span></span>
* <span data-ttu-id="5244e-113">Wijzigen van de DATA 0 netwerkinstellingen via de `Set-HcsNetInterface` cmdlet</span><span class="sxs-lookup"><span data-stu-id="5244e-113">Modify DATA 0 network settings through the `Set-HcsNetInterface` cmdlet</span></span>

## <a name="modify-data-0-network-settings-through-setup-wizard"></a><span data-ttu-id="5244e-114">DATA 0 netwerkinstellingen via de wizard setup wijzigen</span><span class="sxs-lookup"><span data-stu-id="5244e-114">Modify DATA 0 network settings through setup wizard</span></span>
<span data-ttu-id="5244e-115">U kunt DATA 0-netwerkinstellingen configureren door verbinding te maken met de Windows PowerShell-interface van uw StorSimple-apparaat en het starten van een sessie van de wizard setup.</span><span class="sxs-lookup"><span data-stu-id="5244e-115">You can reconfigure DATA 0 network settings by connecting to the Windows PowerShell interface of your StorSimple device and launching a setup wizard session.</span></span> <span data-ttu-id="5244e-116">Voer de volgende stappen uit voor het wijzigen van de DATA 0 instellingen:</span><span class="sxs-lookup"><span data-stu-id="5244e-116">Perform the following steps to modify DATA 0 settings:</span></span>

#### <a name="to-modify-data-0-network-settings-through-setup-wizard"></a><span data-ttu-id="5244e-117">Instellingen voor DATA 0 netwerk via de wizard setup wijzigen</span><span class="sxs-lookup"><span data-stu-id="5244e-117">To modify DATA 0 network settings through setup wizard</span></span>
1. <span data-ttu-id="5244e-118">Kies in het menu van de seriële console optie 1, **aanmelden met volledige toegang**.</span><span class="sxs-lookup"><span data-stu-id="5244e-118">In the serial console menu, choose option 1, **Log in with full access**.</span></span> <span data-ttu-id="5244e-119">Als u wordt gevraagd bieden de **wachtwoord apparaatbeheerder**.</span><span class="sxs-lookup"><span data-stu-id="5244e-119">When prompted provide the **device administrator password**.</span></span> <span data-ttu-id="5244e-120">Is het standaardwachtwoord `Password1`.</span><span class="sxs-lookup"><span data-stu-id="5244e-120">The default password is `Password1`.</span></span>
2. <span data-ttu-id="5244e-121">Typ het volgende achter de opdrachtprompt:</span><span class="sxs-lookup"><span data-stu-id="5244e-121">At the command prompt, type:</span></span>
   
    `Invoke-HcsSetupWizard`
3. <span data-ttu-id="5244e-122">Een setup-wizard wordt weergegeven om u te helpen bij het configureren van de DATA 0-interface van het apparaat.</span><span class="sxs-lookup"><span data-stu-id="5244e-122">A setup wizard appears to help configure the DATA 0 interface of your device.</span></span> <span data-ttu-id="5244e-123">Nieuwe waarden opgeven voor de IP-adres, de gateway en de IP-masker.</span><span class="sxs-lookup"><span data-stu-id="5244e-123">Provide new values for the IP address, gateway, and netmask.</span></span>

> [!NOTE]
> <span data-ttu-id="5244e-124">De vaste IP-adressen-controllers moet opnieuw worden geconfigureerd via de **instellingen** blade van het StorSimple-apparaat in de Azure portal.</span><span class="sxs-lookup"><span data-stu-id="5244e-124">The fixed controllers IPs will need to be reconfigured through the **Network settings** blade of the StorSimple device in the Azure portal.</span></span> <span data-ttu-id="5244e-125">Ga voor meer informatie naar [netwerkinterfaces wijzigen](storsimple-8000-modify-device-config.md#modify-network-interfaces).</span><span class="sxs-lookup"><span data-stu-id="5244e-125">For more information, go to [Modify network interfaces](storsimple-8000-modify-device-config.md#modify-network-interfaces).</span></span>

## <a name="modify-data-0-network-settings-through-set-hcsnetinterface-cmdlet"></a><span data-ttu-id="5244e-126">DATA 0 netwerkinstellingen via de cmdlet Set-HcsNetInterface wijzigen</span><span class="sxs-lookup"><span data-stu-id="5244e-126">Modify DATA 0 network settings through Set-HcsNetInterface cmdlet</span></span>
<span data-ttu-id="5244e-127">Een andere methode voor het configureren van de DATA 0-netwerkinterface met behulp van is de `Set-HcsNetInterface` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="5244e-127">An alternate way to reconfigure DATA 0 network interface is through the use of the `Set-HcsNetInterface` cmdlet.</span></span> <span data-ttu-id="5244e-128">De cmdlet wordt uitgevoerd vanuit de Windows PowerShell-interface van uw StorSimple-apparaat.</span><span class="sxs-lookup"><span data-stu-id="5244e-128">The cmdlet is executed from the Windows PowerShell interface of your StorSimple device.</span></span> <span data-ttu-id="5244e-129">Wanneer u deze procedure gebruikt, kan de controller vaste IP-adressen ook hier worden geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="5244e-129">When using this procedure, the controller fixed IPs can also be configured here.</span></span> <span data-ttu-id="5244e-130">Voer de volgende stappen uit voor het wijzigen van de DATA 0 instellingen:</span><span class="sxs-lookup"><span data-stu-id="5244e-130">Perform the following steps to modify the DATA 0 settings:</span></span> 

#### <a name="to-modify-data-0-network-settings-through-the-set-hcsnetinterface-cmdlet"></a><span data-ttu-id="5244e-131">Instellingen voor DATA 0-netwerk via de cmdlet Set-HcsNetInterface wijzigen</span><span class="sxs-lookup"><span data-stu-id="5244e-131">To modify DATA 0 network settings through the Set-HcsNetInterface cmdlet</span></span>
1. <span data-ttu-id="5244e-132">Kies in het menu van de seriële console optie 1, **aanmelden met volledige toegang**.</span><span class="sxs-lookup"><span data-stu-id="5244e-132">In the serial console menu, choose option 1, **Log in with full access**.</span></span> <span data-ttu-id="5244e-133">Als u wordt gevraagd het beheerderswachtwoord van het apparaat te bieden.</span><span class="sxs-lookup"><span data-stu-id="5244e-133">When prompted provide the device administrator password.</span></span> <span data-ttu-id="5244e-134">Is het standaardwachtwoord `Password1`.</span><span class="sxs-lookup"><span data-stu-id="5244e-134">The default password is `Password1`.</span></span>
2. <span data-ttu-id="5244e-135">Typ het volgende achter de opdrachtprompt:</span><span class="sxs-lookup"><span data-stu-id="5244e-135">At the command prompt, type:</span></span>
   
    `Set-HCSNetInterface -InterfaceAlias Data0 -IPv4Address <> -IPv4Netmask <> -IPv4Gateway <> -Controller0IPv4Address <> -Controller1IPv4Address <> -IsiScsiEnabled 1 -IsCloudEnabled 1`
   
    <span data-ttu-id="5244e-136">Typ de volgende waarden voor de DATA 0 in de punthaken:</span><span class="sxs-lookup"><span data-stu-id="5244e-136">In the angled brackets, type the following values for DATA 0:</span></span>
   
   * <span data-ttu-id="5244e-137">IPv4-adres</span><span class="sxs-lookup"><span data-stu-id="5244e-137">IPv4 address</span></span>
   * <span data-ttu-id="5244e-138">IPv4-gateway</span><span class="sxs-lookup"><span data-stu-id="5244e-138">IPv4 gateway</span></span>
   * <span data-ttu-id="5244e-139">IPv4-subnetmasker</span><span class="sxs-lookup"><span data-stu-id="5244e-139">IPv4 subnet mask</span></span>
   * <span data-ttu-id="5244e-140">Vaste IPv4-adressen voor Controller 0</span><span class="sxs-lookup"><span data-stu-id="5244e-140">Fixed IPv4 address for Controller 0</span></span>
   * <span data-ttu-id="5244e-141">Vaste IPv4-adres voor de Controller 1</span><span class="sxs-lookup"><span data-stu-id="5244e-141">Fixed IPv4 address for Controller 1</span></span>
     
     <span data-ttu-id="5244e-142">Ga voor meer informatie over het gebruik van deze cmdlet naar [Windows PowerShell voor StorSimple cmdlet-verwijzing](https://technet.microsoft.com/library/dn688161.aspx).</span><span class="sxs-lookup"><span data-stu-id="5244e-142">For more information on the use of this cmdlet, go to [Windows PowerShell for StorSimple cmdlet reference](https://technet.microsoft.com/library/dn688161.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="5244e-143">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="5244e-143">Next steps</span></span>
* <span data-ttu-id="5244e-144">Als u wilt configureren netwerkinterfaces, behalve DATA 0, kunt u de [netwerkinstellingen configureren in de Azure-portal](storsimple-8000-modify-device-config.md).</span><span class="sxs-lookup"><span data-stu-id="5244e-144">To configure network interfaces other than DATA 0, you can use the [Configure network settings in the Azure portal](storsimple-8000-modify-device-config.md).</span></span> 
* <span data-ttu-id="5244e-145">Als u problemen ondervindt bij het configureren van uw netwerkinterfaces, raadpleegt u [implementatieproblemen oplossen](storsimple-troubleshoot-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="5244e-145">If you experience any issues when configuring your network interfaces, refer to [Troubleshoot deployment issues](storsimple-troubleshoot-deployment.md).</span></span>


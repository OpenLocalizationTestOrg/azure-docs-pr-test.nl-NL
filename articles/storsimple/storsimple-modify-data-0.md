---
title: aaaModify hello DATA 0-instellingen op een StorSimple-apparaat | Microsoft Docs
description: Meer informatie over hoe toouse Windows PowerShell voor StorSimple tooreconfigure Hallo DATA 0-netwerkinterface op uw StorSimple-apparaat.
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 58e3d509-f425-4a7f-b650-d496a7c85193
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: caec51c3344d953299253301c2a0d7577d553c6e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="modify-hello-data-0-network-interface-settings-on-your-storsimple-device"></a><span data-ttu-id="5a55e-103">Hallo DATA 0 netwerkinterface-instellingen op uw StorSimple-apparaat wijzigen</span><span class="sxs-lookup"><span data-stu-id="5a55e-103">Modify hello DATA 0 network interface settings on your StorSimple device</span></span>
## <a name="overview"></a><span data-ttu-id="5a55e-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="5a55e-104">Overview</span></span>
<span data-ttu-id="5a55e-105">Uw Microsoft Azure StorSimple-apparaat heeft zes netwerkinterfaces, van de DATA 0 tooDATA 5.</span><span class="sxs-lookup"><span data-stu-id="5a55e-105">Your Microsoft Azure StorSimple device has six network interfaces, from DATA 0 tooDATA 5.</span></span> <span data-ttu-id="5a55e-106">Hallo DATA 0-interface is altijd geconfigureerd via Windows PowerShell-interface Hallo of Hallo seriële console en is automatisch ingeschakeld voor de cloud.</span><span class="sxs-lookup"><span data-stu-id="5a55e-106">hello DATA 0 interface is always configured through hello Windows PowerShell interface or hello serial console, and is automatically cloud-enabled.</span></span> <span data-ttu-id="5a55e-107">Houd er rekening mee dat u kunt DATA 0-netwerkinterface via de klassieke Azure-portal Hallo niet configureren.</span><span class="sxs-lookup"><span data-stu-id="5a55e-107">Note that you cannot configure DATA 0 network interface through hello Azure classic portal.</span></span> 

<span data-ttu-id="5a55e-108">Hallo DATA 0 interface eerst via de wizard setup Hallo tijdens de eerste installatie van Hallo StorSimple-apparaat is geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="5a55e-108">hello DATA 0 interface is first configured through hello setup wizard during initial deployment of hello StorSimple device.</span></span> <span data-ttu-id="5a55e-109">Wanneer het Hallo-apparaat is een bedrijfsmodus, moet u wellicht tooreconfigure DATA 0 instellingen.</span><span class="sxs-lookup"><span data-stu-id="5a55e-109">When hello device is in an operational mode, you may need tooreconfigure DATA 0 settings.</span></span> <span data-ttu-id="5a55e-110">Deze zelfstudie biedt twee methoden toomodify DATA 0 netwerkinstellingen, beide via Windows PowerShell voor StorSimple.</span><span class="sxs-lookup"><span data-stu-id="5a55e-110">This tutorial provides two methods toomodify DATA 0 network settings, both through Windows PowerShell for StorSimple.</span></span>

<span data-ttu-id="5a55e-111">Na het lezen van deze zelfstudie, kunt u zich kunt:</span><span class="sxs-lookup"><span data-stu-id="5a55e-111">After reading this tutorial, you will be able to:</span></span>

* <span data-ttu-id="5a55e-112">Wijzigen van de DATA 0-instelling via de wizard setup Hallo-netwerk</span><span class="sxs-lookup"><span data-stu-id="5a55e-112">Modify DATA 0 network setting through hello setup wizard</span></span>
* <span data-ttu-id="5a55e-113">DATA 0 netwerkinstellingen via Hallo wijzigen `Set-HcsNetInterface` cmdlet</span><span class="sxs-lookup"><span data-stu-id="5a55e-113">Modify DATA 0 network settings through hello `Set-HcsNetInterface` cmdlet</span></span>

## <a name="modify-data-0-network-settings-through-setup-wizard"></a><span data-ttu-id="5a55e-114">DATA 0 netwerkinstellingen via de wizard setup wijzigen</span><span class="sxs-lookup"><span data-stu-id="5a55e-114">Modify DATA 0 network settings through setup wizard</span></span>
<span data-ttu-id="5a55e-115">U kunt DATA 0-netwerkinstellingen configureren door verbinding te maken van Windows PowerShell-interface toohello van uw StorSimple-apparaat en het starten van een sessie van de wizard setup.</span><span class="sxs-lookup"><span data-stu-id="5a55e-115">You can reconfigure DATA 0 network settings by connecting toohello Windows PowerShell interface of your StorSimple device and launching a setup wizard session.</span></span> <span data-ttu-id="5a55e-116">Uitvoeren van de volgende stappen toomodify DATA 0 Hallo instellingen:</span><span class="sxs-lookup"><span data-stu-id="5a55e-116">Perform hello following steps toomodify DATA 0 settings:</span></span>

#### <a name="toomodify-data-0-network-settings-through-setup-wizard"></a><span data-ttu-id="5a55e-117">toomodify DATA 0 netwerkinstellingen via de wizard setup</span><span class="sxs-lookup"><span data-stu-id="5a55e-117">toomodify DATA 0 network settings through setup wizard</span></span>
1. <span data-ttu-id="5a55e-118">In het menu van de seriële console hello, kies optie 1, **aanmelden met volledige toegang**.</span><span class="sxs-lookup"><span data-stu-id="5a55e-118">In hello serial console menu, choose option 1, **Log in with full access**.</span></span> <span data-ttu-id="5a55e-119">Als u wordt gevraagd Hallo bieden **wachtwoord apparaatbeheerder**.</span><span class="sxs-lookup"><span data-stu-id="5a55e-119">When prompted provide hello **device administrator password**.</span></span> <span data-ttu-id="5a55e-120">Hallo standaardwachtwoord is `Password1`.</span><span class="sxs-lookup"><span data-stu-id="5a55e-120">hello default password is `Password1`.</span></span>
2. <span data-ttu-id="5a55e-121">Typ het volgende achter de opdrachtprompt Hallo:</span><span class="sxs-lookup"><span data-stu-id="5a55e-121">At hello command prompt, type:</span></span>
   
    `Invoke-HcsSetupWizard`
3. <span data-ttu-id="5a55e-122">Een setup-wizard verschijnt toohelp configureren van Hallo DATA 0-interface van het apparaat.</span><span class="sxs-lookup"><span data-stu-id="5a55e-122">A setup wizard will appear toohelp you configure hello DATA 0 interface of your device.</span></span> <span data-ttu-id="5a55e-123">Nieuwe waarden opgeven voor Hallo IP-adres, gateway en IP-masker.</span><span class="sxs-lookup"><span data-stu-id="5a55e-123">Provide new values for hello IP address, gateway, and netmask.</span></span>

> [!NOTE]
> <span data-ttu-id="5a55e-124">Hallo vaste IP-adressen opnieuw worden geconfigureerd via Hallo toobe moet domeincontrollers **configureren** pagina van Hallo StorSimple-apparaat in Hallo klassieke Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="5a55e-124">hello fixed controllers IPs will need toobe reconfigured through hello **Configure** page of hello StorSimple device in hello Azure classic portal.</span></span> <span data-ttu-id="5a55e-125">Voor meer informatie gaat te[netwerkinterfaces wijzigen](storsimple-modify-device-config.md#modify-network-interfaces).</span><span class="sxs-lookup"><span data-stu-id="5a55e-125">For more information, go too[Modify network interfaces](storsimple-modify-device-config.md#modify-network-interfaces).</span></span>
> 
> 

## <a name="modify-data-0-network-settings-through-set-hcsnetinterface-cmdlet"></a><span data-ttu-id="5a55e-126">DATA 0 netwerkinstellingen via de cmdlet Set-HcsNetInterface wijzigen</span><span class="sxs-lookup"><span data-stu-id="5a55e-126">Modify DATA 0 network settings through Set-HcsNetInterface cmdlet</span></span>
<span data-ttu-id="5a55e-127">Een andere manier tooreconfigure DATA 0-netwerkinterface via het gebruik van de Hallo Hallo is `Set-HcsNetInterface` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="5a55e-127">An alternate way tooreconfigure DATA 0 network interface is through hello use of  hello `Set-HcsNetInterface` cmdlet.</span></span> <span data-ttu-id="5a55e-128">Hallo-cmdlet wordt uitgevoerd vanuit de Windows PowerShell-interface Hallo van uw StorSimple-apparaat.</span><span class="sxs-lookup"><span data-stu-id="5a55e-128">hello cmdlet is executed from hello Windows PowerShell interface of your StorSimple device.</span></span> <span data-ttu-id="5a55e-129">Wanneer u deze procedure gebruikt, kan Hallo controller vaste IP-adressen ook hier worden geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="5a55e-129">When using this procedure, hello controller fixed IPs can also be configured here.</span></span> <span data-ttu-id="5a55e-130">Uitvoeren van de volgende stappen toomodify Hallo DATA 0 Hallo instellingen:</span><span class="sxs-lookup"><span data-stu-id="5a55e-130">Perform hello following steps toomodify hello DATA 0 settings:</span></span> 

#### <a name="toomodify-data-0-network-settings-through-hello-set-hcsnetinterface-cmdlet"></a><span data-ttu-id="5a55e-131">toomodify DATA 0 netwerkinstellingen via de cmdlet Set-HcsNetInterface Hallo</span><span class="sxs-lookup"><span data-stu-id="5a55e-131">toomodify DATA 0 network settings through hello Set-HcsNetInterface cmdlet</span></span>
1. <span data-ttu-id="5a55e-132">In het menu van de seriële console hello, kies optie 1, **aanmelden met volledige toegang**.</span><span class="sxs-lookup"><span data-stu-id="5a55e-132">In hello serial console menu, choose option 1, **Log in with full access**.</span></span> <span data-ttu-id="5a55e-133">Als u wordt gevraagd wachtwoord apparaatbeheerder Hallo bieden.</span><span class="sxs-lookup"><span data-stu-id="5a55e-133">When prompted provide hello device administrator password.</span></span> <span data-ttu-id="5a55e-134">Hallo standaardwachtwoord is `Password1`.</span><span class="sxs-lookup"><span data-stu-id="5a55e-134">hello default password is `Password1`.</span></span>
2. <span data-ttu-id="5a55e-135">Typ het volgende achter de opdrachtprompt Hallo:</span><span class="sxs-lookup"><span data-stu-id="5a55e-135">At hello command prompt, type:</span></span>
   
    `Set-HCSNetInterface -InterfaceAlias Data0 -IPv4Address <> -IPv4Netmask <> -IPv4Gateway <> -Controller0IPv4Address <> -Controller1IPv4Address <> -IsiScsiEnabled 1 -IsCloudEnabled 1`
   
    <span data-ttu-id="5a55e-136">Typ in de hoek Hallo vierkante haken, Hallo volgende waarden op voor de DATA 0:</span><span class="sxs-lookup"><span data-stu-id="5a55e-136">In hello angled brackets, type hello following values for DATA 0:</span></span>
   
   * <span data-ttu-id="5a55e-137">IPv4-adres</span><span class="sxs-lookup"><span data-stu-id="5a55e-137">IPv4 address</span></span>
   * <span data-ttu-id="5a55e-138">IPv4-gateway</span><span class="sxs-lookup"><span data-stu-id="5a55e-138">IPv4 gateway</span></span>
   * <span data-ttu-id="5a55e-139">IPv4-subnetmasker</span><span class="sxs-lookup"><span data-stu-id="5a55e-139">IPv4 subnet mask</span></span>
   * <span data-ttu-id="5a55e-140">Vaste IPv4-adressen voor Controller 0</span><span class="sxs-lookup"><span data-stu-id="5a55e-140">Fixed IPv4 address for Controller 0</span></span>
   * <span data-ttu-id="5a55e-141">Vaste IPv4-adres voor de Controller 1</span><span class="sxs-lookup"><span data-stu-id="5a55e-141">Fixed IPv4 address for Controller 1</span></span>
     
     <span data-ttu-id="5a55e-142">Voor meer informatie over Hallo gebruik van deze cmdlet, gaat u te[Windows PowerShell voor StorSimple cmdlet-verwijzing](https://technet.microsoft.com/library/dn688161.aspx).</span><span class="sxs-lookup"><span data-stu-id="5a55e-142">For more information on hello use of this cmdlet, go too[Windows PowerShell for StorSimple cmdlet reference](https://technet.microsoft.com/library/dn688161.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="5a55e-143">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="5a55e-143">Next steps</span></span>
* <span data-ttu-id="5a55e-144">tooconfigure netwerkinterfaces, behalve DATA 0, kunt u Hallo [pagina configureren in de klassieke Azure-portal Hallo](storsimple-modify-device-config.md).</span><span class="sxs-lookup"><span data-stu-id="5a55e-144">tooconfigure network interfaces other than DATA 0, you can use hello [Configure page in hello Azure classic portal](storsimple-modify-device-config.md).</span></span> 
* <span data-ttu-id="5a55e-145">Als u problemen ondervindt bij het configureren van uw netwerkinterfaces, raadpleeg dan te[implementatieproblemen oplossen](storsimple-troubleshoot-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="5a55e-145">If you experience any issues when configuring your network interfaces, refer too[Troubleshoot deployment issues](storsimple-troubleshoot-deployment.md).</span></span>


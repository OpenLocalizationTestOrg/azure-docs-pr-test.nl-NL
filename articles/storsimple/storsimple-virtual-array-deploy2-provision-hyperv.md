---
title: Inrichten van virtuele StorSimple-matrix in Hyper-V | Microsoft Docs
description: Deze tweede zelfstudie in virtuele StorSimple-matrix implementatie omvat het inrichten van een virtuele-matrix in Hyper-V.
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 4354963c-e09d-41ac-9c8b-f21abeae9913
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 03/15/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: bad431c8958f7d381bb9c0410caa3a57c6e75c19
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-storsimple-virtual-array---provision-in-hyper-v"></a><span data-ttu-id="0b151-103">StorSimple virtuele matrix - inrichten in Hyper-V implementeren</span><span class="sxs-lookup"><span data-stu-id="0b151-103">Deploy StorSimple Virtual Array - Provision in Hyper-V</span></span>
![](./media/storsimple-virtual-array-deploy2-provision-hyperv/hyperv4.png)

## <a name="overview"></a><span data-ttu-id="0b151-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="0b151-104">Overview</span></span>
<span data-ttu-id="0b151-105">Deze zelfstudie wordt beschreven hoe u voor het inrichten van een virtueel StorSimple-matrix op een hostsysteem met Hyper-V op Windows Server 2012 R2, Windows Server 2012 of Windows Server 2008 R2.</span><span class="sxs-lookup"><span data-stu-id="0b151-105">This tutorial describes how to provision a StorSimple Virtual Array on a host system running Hyper-V on Windows Server 2012 R2, Windows Server 2012, or Windows Server 2008 R2.</span></span> <span data-ttu-id="0b151-106">In dit artikel is van toepassing op de implementatie van het virtuele StorSimple-matrices in Azure portal en Microsoft Azure Government Cloud.</span><span class="sxs-lookup"><span data-stu-id="0b151-106">This article applies to the deployment of StorSimple Virtual Arrays in Azure portal and Microsoft Azure Government Cloud.</span></span>

<span data-ttu-id="0b151-107">U moet administrator-bevoegdheden om in te richten en configureren van een virtuele-matrix.</span><span class="sxs-lookup"><span data-stu-id="0b151-107">You need administrator privileges to provision and configure a virtual array.</span></span> <span data-ttu-id="0b151-108">De inrichting en de initiële installatie kan ongeveer 10 minuten duren om te voltooien.</span><span class="sxs-lookup"><span data-stu-id="0b151-108">The provisioning and initial setup can take around 10 minutes to complete.</span></span>

## <a name="provisioning-prerequisites"></a><span data-ttu-id="0b151-109">Vereiste onderdelen inrichten</span><span class="sxs-lookup"><span data-stu-id="0b151-109">Provisioning prerequisites</span></span>
<span data-ttu-id="0b151-110">Hier vindt u de vereisten voor het inrichten van een virtuele-matrix op een hostsysteem met Hyper-V op Windows Server 2012 R2, Windows Server 2012 of Windows Server 2008 R2.</span><span class="sxs-lookup"><span data-stu-id="0b151-110">Here you will find the prerequisites to provision a virtual array on a host system running Hyper-V on Windows Server 2012 R2, Windows Server 2012, or Windows Server 2008 R2.</span></span>

### <a name="for-the-storsimple-device-manager-service"></a><span data-ttu-id="0b151-111">Voor de StorSimple-apparaatbeheerfunctie</span><span class="sxs-lookup"><span data-stu-id="0b151-111">For the StorSimple Device Manager service</span></span>
<span data-ttu-id="0b151-112">Zorg voordat u begint voor het volgende:</span><span class="sxs-lookup"><span data-stu-id="0b151-112">Before you begin, make sure that:</span></span>

* <span data-ttu-id="0b151-113">U hebt de stappen in [voorbereiden van de portal voor virtuele StorSimple-matrix](storsimple-virtual-array-deploy1-portal-prep.md).</span><span class="sxs-lookup"><span data-stu-id="0b151-113">You have completed all the steps in [Prepare the portal for StorSimple Virtual Array](storsimple-virtual-array-deploy1-portal-prep.md).</span></span>
* <span data-ttu-id="0b151-114">Voor Hyper-V hebt u de installatiekopie van het virtuele matrix gedownload vanuit de Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="0b151-114">You have downloaded the virtual array image for Hyper-V from the Azure portal.</span></span> <span data-ttu-id="0b151-115">Zie voor meer informatie **stap 3: Download de installatiekopie van het virtuele matrix** van [voorbereiden van de portal voor het virtuele StorSimple-matrix handleiding](storsimple-virtual-array-deploy1-portal-prep.md).</span><span class="sxs-lookup"><span data-stu-id="0b151-115">For more information, see **Step 3: Download the virtual array image** of [Prepare the portal for StorSimple Virtual Array guide](storsimple-virtual-array-deploy1-portal-prep.md).</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="0b151-116">De software die wordt uitgevoerd op de virtuele StorSimple-matrix kan alleen worden gebruikt met de service Manager voor StorSimple-apparaat.</span><span class="sxs-lookup"><span data-stu-id="0b151-116">The software running on the StorSimple Virtual Array may only be used with the StorSimple Device Manager service.</span></span>
  >
  >

### <a name="for-the-storsimple-virtual-array"></a><span data-ttu-id="0b151-117">Voor de virtuele StorSimple-matrix</span><span class="sxs-lookup"><span data-stu-id="0b151-117">For the StorSimple Virtual Array</span></span>
<span data-ttu-id="0b151-118">Voordat u een virtuele-matrix implementeert, zorg ervoor dat:</span><span class="sxs-lookup"><span data-stu-id="0b151-118">Before you deploy a virtual array, make sure that:</span></span>

* <span data-ttu-id="0b151-119">U hebt toegang tot een hostsysteem met Hyper-V in Windows Server 2008 R2 of hoger die kan worden gebruikt voor een voorziening van een apparaat.</span><span class="sxs-lookup"><span data-stu-id="0b151-119">You have access to a host system running Hyper-V on Windows Server 2008 R2 or later that can be used to a provision a device.</span></span>
* <span data-ttu-id="0b151-120">Het hostsysteem kan toe te wijzen aan de volgende bronnen voor het inrichten van uw virtuele matrix:</span><span class="sxs-lookup"><span data-stu-id="0b151-120">The host system is able to dedicate the following resources to provision your virtual array:</span></span>

  * <span data-ttu-id="0b151-121">Een minimum van 4 kernen.</span><span class="sxs-lookup"><span data-stu-id="0b151-121">A minimum of 4 cores.</span></span>
  * <span data-ttu-id="0b151-122">Ten minste 8 GB aan RAM-geheugen.</span><span class="sxs-lookup"><span data-stu-id="0b151-122">At least 8 GB of RAM.</span></span> <span data-ttu-id="0b151-123">Als u van plan bent de virtuele matrix als bestandsserver te configureren, ondersteunt 8 GB minder dan 2 miljoen bestanden.</span><span class="sxs-lookup"><span data-stu-id="0b151-123">If you plan to configure the virtual array as file server, 8 GB supports less than 2 million files.</span></span> <span data-ttu-id="0b151-124">U moet 16 GB RAM-geheugen voor de ondersteuning van 2-4 miljoen bestanden.</span><span class="sxs-lookup"><span data-stu-id="0b151-124">You need 16 GB RAM to support 2 - 4 million files.</span></span>
  * <span data-ttu-id="0b151-125">Één netwerkinterface.</span><span class="sxs-lookup"><span data-stu-id="0b151-125">One network interface.</span></span>
  * <span data-ttu-id="0b151-126">Een 500 GB virtuele schijf voor gegevens.</span><span class="sxs-lookup"><span data-stu-id="0b151-126">A 500 GB virtual disk for data.</span></span>

### <a name="for-the-network-in-the-datacenter"></a><span data-ttu-id="0b151-127">Voor het netwerk in het datacenter</span><span class="sxs-lookup"><span data-stu-id="0b151-127">For the network in the datacenter</span></span>
<span data-ttu-id="0b151-128">Voordat u begint, controleert u de netwerkvereisten implementeren van een virtueel StorSimple-matrix en het datacenternetwerk op de juiste wijze configureren.</span><span class="sxs-lookup"><span data-stu-id="0b151-128">Before you begin, review the networking requirements to deploy a StorSimple Virtual Array and configure the datacenter network appropriately.</span></span> <span data-ttu-id="0b151-129">Zie voor meer informatie [virtuele StorSimple-matrix netwerkvereisten](storsimple-ova-system-requirements.md#networking-requirements).</span><span class="sxs-lookup"><span data-stu-id="0b151-129">For more information, see [StorSimple Virtual Array networking requirements](storsimple-ova-system-requirements.md#networking-requirements).</span></span>

## <a name="step-by-step-provisioning"></a><span data-ttu-id="0b151-130">Stapsgewijze inrichten</span><span class="sxs-lookup"><span data-stu-id="0b151-130">Step-by-step provisioning</span></span>
<span data-ttu-id="0b151-131">Als u wilt inrichten en verbinding maken met een virtuele-matrix, moet u de volgende stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="0b151-131">To provision and connect to a virtual array, you need to perform the following steps:</span></span>

1. <span data-ttu-id="0b151-132">Zorg ervoor dat het hostsysteem voldoende resources heeft om te voldoen aan de vereisten voor de minimale virtuele matrix.</span><span class="sxs-lookup"><span data-stu-id="0b151-132">Ensure that the host system has sufficient resources to meet the minimum virtual array requirements.</span></span>
2. <span data-ttu-id="0b151-133">Inrichten van een virtuele-matrix in de hypervisor.</span><span class="sxs-lookup"><span data-stu-id="0b151-133">Provision a virtual array in your hypervisor.</span></span>
3. <span data-ttu-id="0b151-134">Start de virtuele matrix en het IP-adres.</span><span class="sxs-lookup"><span data-stu-id="0b151-134">Start the virtual array and get the IP address.</span></span>

<span data-ttu-id="0b151-135">Elk van deze stappen wordt uitgelegd in de volgende secties.</span><span class="sxs-lookup"><span data-stu-id="0b151-135">Each of these steps is explained in the following sections.</span></span>

## <a name="step-1-ensure-that-the-host-system-meets-minimum-virtual-array-requirements"></a><span data-ttu-id="0b151-136">Stap 1: Zorg ervoor dat het hostsysteem aan minimale virtuele matrix vereisten voldoet.</span><span class="sxs-lookup"><span data-stu-id="0b151-136">Step 1: Ensure that the host system meets minimum virtual array requirements</span></span>
<span data-ttu-id="0b151-137">Voor het maken van een virtuele-matrix, hebt u het volgende nodig:</span><span class="sxs-lookup"><span data-stu-id="0b151-137">To create a virtual array, you need:</span></span>

* <span data-ttu-id="0b151-138">De Hyper-V-rol geïnstalleerd op Windows Server 2012 R2, Windows Server 2012 of Windows Server 2008 R2 SP1.</span><span class="sxs-lookup"><span data-stu-id="0b151-138">The Hyper-V role installed on Windows Server 2012 R2, Windows Server 2012, or Windows Server 2008 R2 SP1.</span></span>
* <span data-ttu-id="0b151-139">Microsoft Hyper-V Manager op een Microsoft Windows-client is verbonden met de host.</span><span class="sxs-lookup"><span data-stu-id="0b151-139">Microsoft Hyper-V Manager on a Microsoft Windows client connected to the host.</span></span>

<span data-ttu-id="0b151-140">Zorg ervoor dat de onderliggende hardware (hostsysteem), waarop u de virtuele matrix maakt, kan het reserveren van de volgende bronnen voor uw virtuele matrix:</span><span class="sxs-lookup"><span data-stu-id="0b151-140">Make sure that the underlying hardware (host system) on which you are creating the virtual array is able to dedicate the following resources to your virtual array:</span></span>

* <span data-ttu-id="0b151-141">Een minimum van 4 kernen.</span><span class="sxs-lookup"><span data-stu-id="0b151-141">A minimum of 4 cores.</span></span>
* <span data-ttu-id="0b151-142">Ten minste 8 GB aan RAM-geheugen.</span><span class="sxs-lookup"><span data-stu-id="0b151-142">At least 8 GB of RAM.</span></span> <span data-ttu-id="0b151-143">Als u van plan bent de virtuele matrix als bestandsserver te configureren, ondersteunt 8 GB minder dan 2 miljoen bestanden.</span><span class="sxs-lookup"><span data-stu-id="0b151-143">If you plan to configure the virtual array as file server, 8 GB supports less than 2 million files.</span></span> <span data-ttu-id="0b151-144">U moet 16 GB RAM-geheugen voor de ondersteuning van 2-4 miljoen bestanden.</span><span class="sxs-lookup"><span data-stu-id="0b151-144">You need 16 GB RAM to support 2 - 4 million files.</span></span>
* <span data-ttu-id="0b151-145">Één netwerkinterface.</span><span class="sxs-lookup"><span data-stu-id="0b151-145">One network interface.</span></span>
* <span data-ttu-id="0b151-146">500 GB virtuele schijf voor systeemgegevens.</span><span class="sxs-lookup"><span data-stu-id="0b151-146">A 500 GB virtual disk for system data.</span></span>

## <a name="step-2-provision-a-virtual-array-in-hypervisor"></a><span data-ttu-id="0b151-147">Stap 2: Een virtuele-matrix in hypervisor inrichten</span><span class="sxs-lookup"><span data-stu-id="0b151-147">Step 2: Provision a virtual array in hypervisor</span></span>
<span data-ttu-id="0b151-148">Voer de volgende stappen uit voor het inrichten van een apparaat in de hypervisor.</span><span class="sxs-lookup"><span data-stu-id="0b151-148">Perform the following steps to provision a device in your hypervisor.</span></span>

#### <a name="to-provision-a-virtual-array"></a><span data-ttu-id="0b151-149">Voor het inrichten van een virtuele-matrix</span><span class="sxs-lookup"><span data-stu-id="0b151-149">To provision a virtual array</span></span>
1. <span data-ttu-id="0b151-150">Kopiëren van de virtuele matrix-installatiekopie naar een lokaal station op de host Windows Server.</span><span class="sxs-lookup"><span data-stu-id="0b151-150">On your Windows Server host, copy the virtual array image to a local drive.</span></span> <span data-ttu-id="0b151-151">U hebt deze afbeelding (VHD of VHDX) gedownload via de Azure portal.</span><span class="sxs-lookup"><span data-stu-id="0b151-151">You downloaded this image (VHD or VHDX) through the Azure portal.</span></span> <span data-ttu-id="0b151-152">Noteer de locatie waar u de installatiekopie gekopieerd wanneer u deze installatiekopie later in de procedure gebruikt.</span><span class="sxs-lookup"><span data-stu-id="0b151-152">Make a note of the location where you copied the image as you are using this image later in the procedure.</span></span>
2. <span data-ttu-id="0b151-153">Open **Serverbeheer**.</span><span class="sxs-lookup"><span data-stu-id="0b151-153">Open **Server Manager**.</span></span> <span data-ttu-id="0b151-154">Klik in de rechterbovenhoek op **extra** en selecteer **Hyper-V-beheer**.</span><span class="sxs-lookup"><span data-stu-id="0b151-154">In the top right corner, click **Tools** and select **Hyper-V Manager**.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image1.png)  

   <span data-ttu-id="0b151-155">Als u Windows Server 2008 R2 uitvoert, opent u de Hyper-V-beheer.</span><span class="sxs-lookup"><span data-stu-id="0b151-155">If you are running Windows Server 2008 R2, open the Hyper-V Manager.</span></span> <span data-ttu-id="0b151-156">Klik in Serverbeheer op **functies > Hyper-V > Hyper-V-beheer**.</span><span class="sxs-lookup"><span data-stu-id="0b151-156">In Server Manager, click **Roles > Hyper-V > Hyper-V Manager**.</span></span>
3. <span data-ttu-id="0b151-157">In **Hyper-V-beheer**, in het deelvenster bereik met de rechtermuisknop op uw systeem knooppunt uit om het contextmenu te openen en klik vervolgens op **nieuw** > **virtuele Machine**.</span><span class="sxs-lookup"><span data-stu-id="0b151-157">In **Hyper-V Manager**, in the scope pane, right-click your system node to open the context menu, and then click **New** > **Virtual Machine**.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image2.png)
4. <span data-ttu-id="0b151-158">Op de **voordat u begint met** pagina van de Wizard Nieuwe virtuele Machine, klikt u op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="0b151-158">On the **Before you begin** page of the New Virtual Machine Wizard, click **Next**.</span></span>
5. <span data-ttu-id="0b151-159">Op de **naam en locatie opgeven** pagina een **naam** voor uw virtuele matrix.</span><span class="sxs-lookup"><span data-stu-id="0b151-159">On the **Specify name and location** page, provide a **Name** for your virtual array.</span></span> <span data-ttu-id="0b151-160">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="0b151-160">Click **Next**.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image4.png)
6. <span data-ttu-id="0b151-161">Op de **generatie opgeven** pagina, kies het apparaattype en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="0b151-161">On the **Specify generation** page, choose the device image type, and then click **Next**.</span></span> <span data-ttu-id="0b151-162">Deze pagina wordt niet weergegeven als u Windows Server 2008 R2.</span><span class="sxs-lookup"><span data-stu-id="0b151-162">This page doesn't appear if you're using Windows Server 2008 R2.</span></span>

   * <span data-ttu-id="0b151-163">Kies **generatie 2** als u een .vhdx-installatiekopie voor Windows Server 2012 of hoger hebt gedownload.</span><span class="sxs-lookup"><span data-stu-id="0b151-163">Choose **Generation 2** if you downloaded a .vhdx image for Windows Server 2012 or later.</span></span>
   * <span data-ttu-id="0b151-164">Kies **generatie 1** als u een VHD-installatiekopie voor Windows Server 2008 R2 of hoger hebt gedownload.</span><span class="sxs-lookup"><span data-stu-id="0b151-164">Choose **Generation 1** if you downloaded a .vhd image for Windows Server 2008 R2 or later.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image5.png)
7. <span data-ttu-id="0b151-165">Op de **toewijzen van geheugen** pagina, geeft u een **opstartgeheugen** van ten minste **8192 MB**niet inschakelen van dynamisch geheugen en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="0b151-165">On the **Assign memory** page, specify a **Startup memory** of at least **8192 MB**, don't enable dynamic memory, and then click **Next**.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image6.png)  
8. <span data-ttu-id="0b151-166">Op de **netwerk configureren** pagina, geef de virtuele switch die is verbonden met Internet en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="0b151-166">On the **Configure networking** page, specify the virtual switch that is connected to the Internet and then click **Next**.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image7.png)
9. <span data-ttu-id="0b151-167">Op de **virtuele harde schijf aansluiten** pagina **gebruik een bestaande virtuele harde schijf**, geef de locatie van de installatiekopie van het virtuele matrix (vhdx of VHD) en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="0b151-167">On the **Connect virtual hard disk** page, choose **Use an existing virtual hard disk**, specify the location of the virtual array image (.vhdx or .vhd), and then click **Next**.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image8m.png)
10. <span data-ttu-id="0b151-168">Controleer de **samenvatting** en klik vervolgens op **voltooien** voor het maken van de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="0b151-168">Review the **Summary** and then click **Finish** to create the virtual machine.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image9.png)
11. <span data-ttu-id="0b151-169">Om te voldoen aan de minimale vereisten voldoet, moet u 4 kernen.</span><span class="sxs-lookup"><span data-stu-id="0b151-169">To meet the minimum requirements, you need 4 cores.</span></span> <span data-ttu-id="0b151-170">Selecteer uw hostsysteem in om 4 virtuele processors toe de **Hyper-V-beheer** venster.</span><span class="sxs-lookup"><span data-stu-id="0b151-170">To add 4 virtual processors, select your host system in the **Hyper-V Manager** window.</span></span> <span data-ttu-id="0b151-171">In het rechterdeelvenster onder de lijst met **virtuele Machines**, Ga naar de virtuele machine die u zojuist hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="0b151-171">In the right-pane under the list of **Virtual Machines**, locate the virtual machine you just created.</span></span> <span data-ttu-id="0b151-172">Selecteer en met de rechtermuisknop op de naam van de machine en selecteer **instellingen**.</span><span class="sxs-lookup"><span data-stu-id="0b151-172">Select and right-click the machine name and select **Settings**.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image10.png)
12. <span data-ttu-id="0b151-173">Op de **instellingen** pagina in het linkerdeelvenster klikt u op **Processor**.</span><span class="sxs-lookup"><span data-stu-id="0b151-173">On the **Settings** page, in the left-pane, click **Processor**.</span></span> <span data-ttu-id="0b151-174">Stel in het rechterdeelvenster **aantal virtuele processors** 4 (of meer).</span><span class="sxs-lookup"><span data-stu-id="0b151-174">In the right-pane, set **number of virtual processors** to 4 (or more).</span></span> <span data-ttu-id="0b151-175">Klik op **Toepassen**.</span><span class="sxs-lookup"><span data-stu-id="0b151-175">Click **Apply**.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image11.png)
13. <span data-ttu-id="0b151-176">Om te voldoen aan de minimale vereisten voldoet, moet u ook een 500 GB gegevens van virtuele schijf toe te voegen.</span><span class="sxs-lookup"><span data-stu-id="0b151-176">To meet the minimum requirements, you also need to add a 500 GB virtual data disk.</span></span> <span data-ttu-id="0b151-177">In de **instellingen** pagina:</span><span class="sxs-lookup"><span data-stu-id="0b151-177">In the **Settings** page:</span></span>

    1. <span data-ttu-id="0b151-178">Selecteer in het linkerdeelvenster **SCSI-Controller**.</span><span class="sxs-lookup"><span data-stu-id="0b151-178">In the left pane, select **SCSI Controller**.</span></span>
    2. <span data-ttu-id="0b151-179">Selecteer in het rechterdeelvenster **harde schijf** en klik op **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="0b151-179">In the right pane, select **Hard Drive,** and click **Add**.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image12.png)
14. <span data-ttu-id="0b151-180">Op de **harde schijf** pagina de **virtuele hardeschijf** optie en klik op **nieuw**.</span><span class="sxs-lookup"><span data-stu-id="0b151-180">On the **Hard drive** page, select the **Virtual hard disk** option and click **New**.</span></span> <span data-ttu-id="0b151-181">De **Wizard Nieuwe virtuele hardeschijf** wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="0b151-181">The **New Virtual Hard Disk Wizard** starts.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image13.png)
15. <span data-ttu-id="0b151-182">Op de **voordat u begint met** pagina van de Wizard Nieuwe virtuele hardeschijf, klikt u op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="0b151-182">On the **Before you begin** page of the New Virtual Hard Disk Wizard, click **Next**.</span></span>
16. <span data-ttu-id="0b151-183">Op de **schijfindeling kiezen pagina**, accepteer de standaardwaarde van **VHDX** indeling.</span><span class="sxs-lookup"><span data-stu-id="0b151-183">On the **Choose Disk Format page**, accept the default option of **VHDX** format.</span></span> <span data-ttu-id="0b151-184">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="0b151-184">Click **Next**.</span></span> <span data-ttu-id="0b151-185">Dit scherm niet wordt weergegeven als Windows Server 2008 R2 wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="0b151-185">This screen is not presented if running Windows Server 2008 R2.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image15.png)
17. <span data-ttu-id="0b151-186">Op de **schijftype kiezen pagina**, instellen van het type virtuele harde schijf als **dynamisch uitbreidbare** (aanbevolen).</span><span class="sxs-lookup"><span data-stu-id="0b151-186">On the **Choose Disk Type page**, set virtual hard disk type as **Dynamically expanding** (recommended).</span></span> <span data-ttu-id="0b151-187">**Een vaste grootte** schijf wilt werken, maar mogelijk moet u een lange wachttijd.</span><span class="sxs-lookup"><span data-stu-id="0b151-187">**Fixed size** disk would work but you may need to wait a long time.</span></span> <span data-ttu-id="0b151-188">Het is raadzaam dat u niet gebruikt de **Differencing** optie.</span><span class="sxs-lookup"><span data-stu-id="0b151-188">We recommend that you do not use the **Differencing** option.</span></span> <span data-ttu-id="0b151-189">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="0b151-189">Click **Next**.</span></span> <span data-ttu-id="0b151-190">In Windows Server 2012 R2 en Windows Server 2012 **dynamisch uitbreidbare** is de standaardoptie dat in Windows Server 2008 R2, de standaardwaarde is **een vaste grootte**.</span><span class="sxs-lookup"><span data-stu-id="0b151-190">In Windows Server 2012 R2 and Windows Server 2012, **Dynamically expanding** is the default option whereas in Windows Server 2008 R2, the default is **Fixed size**.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image16.png)
18. <span data-ttu-id="0b151-191">Op de **naam en locatie opgeven** pagina een **naam** , evenals **locatie** (u kunt bladeren naar een) voor de gegevensschijf.</span><span class="sxs-lookup"><span data-stu-id="0b151-191">On the **Specify Name and Location** page, provide a **name** as well as **location** (you can browse to one) for the data disk.</span></span> <span data-ttu-id="0b151-192">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="0b151-192">Click **Next**.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image17.png)
19. <span data-ttu-id="0b151-193">Op de **schijf configureren** pagina, selecteert u de optie **maken van een nieuwe lege virtuele harde-schijf** en geef de grootte als **500 GB** (of meer).</span><span class="sxs-lookup"><span data-stu-id="0b151-193">On the **Configure Disk** page, select the option **Create a new blank virtual hard disk** and specify the size as **500 GB** (or more).</span></span> <span data-ttu-id="0b151-194">500 GB is de minimumvereiste, kunt u altijd een grotere schijf inrichten.</span><span class="sxs-lookup"><span data-stu-id="0b151-194">While 500 GB is the minimum requirement, you can always provision a larger disk.</span></span> <span data-ttu-id="0b151-195">Houd er rekening mee u niet kunt uitbreiden of verkleinen van de schijf eenmaal ingericht.</span><span class="sxs-lookup"><span data-stu-id="0b151-195">Note that you cannot expand or shrink the disk once provisioned.</span></span> <span data-ttu-id="0b151-196">Raadpleeg voor meer informatie over de grootte van de schijf om in te richten de sizing-sectie in het [best practices document](storsimple-ova-best-practices.md).</span><span class="sxs-lookup"><span data-stu-id="0b151-196">For more information on the size of disk to provision, review the sizing section in the [best practices document](storsimple-ova-best-practices.md).</span></span> <span data-ttu-id="0b151-197">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="0b151-197">Click **Next**.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image18.png)
20. <span data-ttu-id="0b151-198">Op de **samenvatting** pagina, bekijk de details van de van virtuele gegevensschijf en als u tevreden bent, klikt u op **voltooien** om de schijf te maken.</span><span class="sxs-lookup"><span data-stu-id="0b151-198">On the **Summary** page, review the details of your virtual data disk and if satisfied, click **Finish** to create the disk.</span></span> <span data-ttu-id="0b151-199">De wizard wordt gesloten en een virtuele harde schijf wordt toegevoegd aan uw computer.</span><span class="sxs-lookup"><span data-stu-id="0b151-199">The wizard closes and a virtual hard disk is added to your machine.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image19.png)
21. <span data-ttu-id="0b151-200">Ga terug naar de **instellingen** pagina.</span><span class="sxs-lookup"><span data-stu-id="0b151-200">Return to the **Settings** page.</span></span> <span data-ttu-id="0b151-201">Klik op **OK** sluiten de **instellingen** pagina en terug te keren naar Hyper-V-beheer.</span><span class="sxs-lookup"><span data-stu-id="0b151-201">Click **OK** to close the **Settings** page and return to Hyper-V Manager window.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image20.png)

## <a name="step-3-start-the-virtual-array-and-get-the-ip"></a><span data-ttu-id="0b151-202">Stap 3: Start de virtuele matrix en het IP-adres ophalen</span><span class="sxs-lookup"><span data-stu-id="0b151-202">Step 3: Start the virtual array and get the IP</span></span>
<span data-ttu-id="0b151-203">Voer de volgende stappen uit uw virtuele matrix starten en verbinding maken met het.</span><span class="sxs-lookup"><span data-stu-id="0b151-203">Perform the following steps to start your virtual array and connect to it.</span></span>

#### <a name="to-start-the-virtual-array"></a><span data-ttu-id="0b151-204">Starten van de virtuele matrix</span><span class="sxs-lookup"><span data-stu-id="0b151-204">To start the virtual array</span></span>
1. <span data-ttu-id="0b151-205">Start de virtuele-matrix.</span><span class="sxs-lookup"><span data-stu-id="0b151-205">Start the virtual array.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image21.png)
2. <span data-ttu-id="0b151-206">Nadat het apparaat wordt uitgevoerd, selecteert u het apparaat, klik met de rechtermuisknop en selecteer **Connect**.</span><span class="sxs-lookup"><span data-stu-id="0b151-206">After the device is running, select the device, right click, and select **Connect**.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image22.png)
3. <span data-ttu-id="0b151-207">U moet 5-10 minuten wachten voor het apparaat niet gereed.</span><span class="sxs-lookup"><span data-stu-id="0b151-207">You may have to wait 5-10 minutes for the device to be ready.</span></span> <span data-ttu-id="0b151-208">Een statusbericht wordt weergegeven op de console om de voortgang te geven.</span><span class="sxs-lookup"><span data-stu-id="0b151-208">A status message is displayed on the console to indicate the progress.</span></span> <span data-ttu-id="0b151-209">Nadat het apparaat klaar is, gaat u naar **actie**.</span><span class="sxs-lookup"><span data-stu-id="0b151-209">After the device is ready, go to **Action**.</span></span> <span data-ttu-id="0b151-210">Druk op `Ctrl + Alt + Delete` zich aanmelden bij de virtuele-matrix.</span><span class="sxs-lookup"><span data-stu-id="0b151-210">Press `Ctrl + Alt + Delete` to log in to the virtual array.</span></span> <span data-ttu-id="0b151-211">De standaardgebruiker is *StorSimpleAdmin* en is het standaardwachtwoord *Wachtwoord1*.</span><span class="sxs-lookup"><span data-stu-id="0b151-211">The default user is *StorSimpleAdmin* and the default password is *Password1*.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image23.png)
4. <span data-ttu-id="0b151-212">Uit veiligheidsoverwegingen verloopt het beheerderswachtwoord van het apparaat bij de eerste aanmelding.</span><span class="sxs-lookup"><span data-stu-id="0b151-212">For security reasons, the device administrator password expires at the first logon.</span></span> <span data-ttu-id="0b151-213">U wordt gevraagd het wachtwoord te wijzigen.</span><span class="sxs-lookup"><span data-stu-id="0b151-213">You are prompted to change the password.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image24.png)

   <span data-ttu-id="0b151-214">Voer een wachtwoord dat ten minste 8 tekens bevat.</span><span class="sxs-lookup"><span data-stu-id="0b151-214">Enter a password that contains at least 8 characters.</span></span> <span data-ttu-id="0b151-215">Het wachtwoord moet ten minste 3 buiten de volgende 4 vereisten voldoen: hoofdletters, kleine letters, numerieke en speciale tekens.</span><span class="sxs-lookup"><span data-stu-id="0b151-215">The password must satisfy at least 3 out of the following 4 requirements: uppercase, lowercase, numeric, and special characters.</span></span> <span data-ttu-id="0b151-216">Geef het wachtwoord ter bevestiging opnieuw.</span><span class="sxs-lookup"><span data-stu-id="0b151-216">Reenter the password to confirm it.</span></span> <span data-ttu-id="0b151-217">U wordt gewaarschuwd dat het wachtwoord is gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="0b151-217">You are notified that the password has changed.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image25.png)
5. <span data-ttu-id="0b151-218">Nadat het wachtwoord is gewijzigd, kunnen de virtuele matrix mogelijk opnieuw opgestart.</span><span class="sxs-lookup"><span data-stu-id="0b151-218">After the password is successfully changed, the virtual array may restart.</span></span> <span data-ttu-id="0b151-219">Wachten op het apparaat te starten.</span><span class="sxs-lookup"><span data-stu-id="0b151-219">Wait for the device to start.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image26.png)

    <span data-ttu-id="0b151-220">De Windows PowerShell-console van het apparaat wordt samen met een voortgangsbalk weergegeven.</span><span class="sxs-lookup"><span data-stu-id="0b151-220">The Windows PowerShell console of the device is displayed along with a progress bar.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image27.png)
6. <span data-ttu-id="0b151-221">Stap 6-8 zijn alleen van toepassing wanneer in een omgeving met niet-DHCP-up wordt opgestart.</span><span class="sxs-lookup"><span data-stu-id="0b151-221">Steps 6-8 only apply when booting up in a non-DHCP environment.</span></span> <span data-ttu-id="0b151-222">Als u zich in een DHCP-omgeving, slaat u deze stappen over en gaat u naar stap 9.</span><span class="sxs-lookup"><span data-stu-id="0b151-222">If you are in a DHCP environment, then skip these steps and go to step 9.</span></span> <span data-ttu-id="0b151-223">Als u van uw apparaat in niet-DHCP-omgeving opgestart, ziet u het volgende scherm.</span><span class="sxs-lookup"><span data-stu-id="0b151-223">If you booted up your device in non-DHCP environment, you will see the following screen.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image28m.png)

    <span data-ttu-id="0b151-224">Configureer vervolgens het netwerk.</span><span class="sxs-lookup"><span data-stu-id="0b151-224">Next, configure the network.</span></span>
7. <span data-ttu-id="0b151-225">Gebruik de `Get-HcsIpAddress` opdracht om een lijst van de netwerkinterfaces die zijn ingeschakeld op uw virtuele matrix.</span><span class="sxs-lookup"><span data-stu-id="0b151-225">Use the `Get-HcsIpAddress` command to list the network interfaces enabled on your virtual array.</span></span> <span data-ttu-id="0b151-226">Als uw apparaat één netwerkinterface is ingeschakeld heeft, wordt de standaardnaam die wordt toegewezen aan deze interface is `Ethernet`.</span><span class="sxs-lookup"><span data-stu-id="0b151-226">If your device has a single network interface enabled, the default name assigned to this interface is `Ethernet`.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image29m.png)
8. <span data-ttu-id="0b151-227">Gebruik de `Set-HcsIpAddress` cmdlet voor het configureren van het netwerk.</span><span class="sxs-lookup"><span data-stu-id="0b151-227">Use the `Set-HcsIpAddress` cmdlet to configure the network.</span></span> <span data-ttu-id="0b151-228">Zie het volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="0b151-228">See the following example:</span></span>

    `Set-HcsIpAddress –Name Ethernet –IpAddress 10.161.22.90 –Netmask 255.255.255.0 –Gateway 10.161.22.1`

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image30.png)
9. <span data-ttu-id="0b151-229">Nadat de eerste installatie voltooid is en het apparaat is opgestart, ziet u de bannertekst apparaat.</span><span class="sxs-lookup"><span data-stu-id="0b151-229">After the initial setup is complete and the device has booted up, you will see the device banner text.</span></span> <span data-ttu-id="0b151-230">Noteer het IP-adres en de URL weergegeven in de bannertekst de apparaten te beheren.</span><span class="sxs-lookup"><span data-stu-id="0b151-230">Make a note of the IP address and the URL displayed in the banner text to manage the device.</span></span> <span data-ttu-id="0b151-231">Gebruik dit IP-adres verbinding maken met de webgebruikersinterface van uw virtuele matrix en de lokale installatie en registratie te voltooien.</span><span class="sxs-lookup"><span data-stu-id="0b151-231">Use this IP address to connect to the web UI of your virtual array and complete the local setup and registration.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image31m.png)
10. <span data-ttu-id="0b151-232">(Optioneel) Deze stap alleen uitvoeren als u uw apparaat in de Cloud Government implementeert.</span><span class="sxs-lookup"><span data-stu-id="0b151-232">(Optional) Perform this step only if you are deploying your device in the Government Cloud.</span></span> <span data-ttu-id="0b151-233">U kunt nu de modus van de Verenigde Staten Federal Information Processing Standard (FIPS) op uw apparaat.</span><span class="sxs-lookup"><span data-stu-id="0b151-233">You will now enable the United States Federal Information Processing Standard (FIPS) mode on your device.</span></span> <span data-ttu-id="0b151-234">De FIPS 140-standaard definieert cryptografische algoritmen die zijn goedgekeurd voor gebruik door ons Federal government computersystemen voor de bescherming van gevoelige gegevens.</span><span class="sxs-lookup"><span data-stu-id="0b151-234">The FIPS 140 standard defines cryptographic algorithms approved for use by US Federal government computer systems for the protection of sensitive data.</span></span>

    1. <span data-ttu-id="0b151-235">Als u de FIPS-modus, voert u de volgende cmdlet:</span><span class="sxs-lookup"><span data-stu-id="0b151-235">To enable the FIPS mode, run the following cmdlet:</span></span>

        `Enable-HcsFIPSMode`
    2. <span data-ttu-id="0b151-236">Start opnieuw op uw apparaat wanneer u de FIPS-modus hebt ingeschakeld, zodat de cryptografische validaties te treden laten.</span><span class="sxs-lookup"><span data-stu-id="0b151-236">Reboot your device after you have enabled the FIPS mode so that the cryptographic validations take effect.</span></span>

       > [!NOTE]
       > <span data-ttu-id="0b151-237">U kunt inschakelen of uitschakelen van FIPS-modus op uw apparaat.</span><span class="sxs-lookup"><span data-stu-id="0b151-237">You can either enable or disable FIPS mode on your device.</span></span> <span data-ttu-id="0b151-238">Het apparaat tussen FIPS- en niet FIPS-modus afwisselende wordt niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="0b151-238">Alternating the device between FIPS and non-FIPS mode is not supported.</span></span>
       >
       >

<span data-ttu-id="0b151-239">Als uw apparaat voldoet niet aan de minimale configuratievereisten voor, ziet u de volgende fout in de bannertekst (Zie hieronder).</span><span class="sxs-lookup"><span data-stu-id="0b151-239">If your device does not meet the minimum configuration requirements, you see the following error in the banner text (shown below).</span></span> <span data-ttu-id="0b151-240">Configuratie van het apparaat zodanig aanpassen dat de machine voldoende resources heeft om te voldoen aan de minimumvereisten.</span><span class="sxs-lookup"><span data-stu-id="0b151-240">Modify the device configuration so that the machine has adequate resources to meet the minimum requirements.</span></span> <span data-ttu-id="0b151-241">U kunt starten en verbinding maken met het apparaat.</span><span class="sxs-lookup"><span data-stu-id="0b151-241">You can then restart and connect to the device.</span></span> <span data-ttu-id="0b151-242">Raadpleeg de minimale configuratievereisten voor in [stap 1: Zorg ervoor dat het hostsysteem voldoet met minimale virtuele matrix](#step-1-ensure-that-the-host-system-meets-minimum-virtual-device-requirements).</span><span class="sxs-lookup"><span data-stu-id="0b151-242">Refer to the minimum configuration requirements in [Step 1: Ensure that the host system meets minimum virtual array requirements](#step-1-ensure-that-the-host-system-meets-minimum-virtual-device-requirements).</span></span>

![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image32.png)

<span data-ttu-id="0b151-243">Als u een andere fout tijdens de eerste configuratie via de lokale webgebruikersinterface geconfronteerd, raadpleegt u de volgende werkstromen:</span><span class="sxs-lookup"><span data-stu-id="0b151-243">If you face any other error during the initial configuration using the local web UI, refer to the following workflows:</span></span>

* <span data-ttu-id="0b151-244">Diagnostische tests uitvoeren om te [web UI setup oplossen](storsimple-ova-web-ui-admin.md#troubleshoot-web-ui-setup-errors).</span><span class="sxs-lookup"><span data-stu-id="0b151-244">Run diagnostic tests to [troubleshoot web UI setup](storsimple-ova-web-ui-admin.md#troubleshoot-web-ui-setup-errors).</span></span>
* <span data-ttu-id="0b151-245">[Logboek pakket genereren en logboekbestanden weergeven](storsimple-ova-web-ui-admin.md#generate-a-log-package).</span><span class="sxs-lookup"><span data-stu-id="0b151-245">[Generate log package and view log files](storsimple-ova-web-ui-admin.md#generate-a-log-package).</span></span>

## <a name="next-steps"></a><span data-ttu-id="0b151-246">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="0b151-246">Next steps</span></span>
* [<span data-ttu-id="0b151-247">Uw virtuele StorSimple-matrix instellen als bestandsserver</span><span class="sxs-lookup"><span data-stu-id="0b151-247">Set up your StorSimple Virtual Array as a file server</span></span>](storsimple-virtual-array-deploy3-fs-setup.md)
* [<span data-ttu-id="0b151-248">Uw virtuele StorSimple-matrix ingesteld als een iSCSI-server</span><span class="sxs-lookup"><span data-stu-id="0b151-248">Set up your StorSimple Virtual Array as an iSCSI server</span></span>](storsimple-virtual-array-deploy3-iscsi-setup.md)

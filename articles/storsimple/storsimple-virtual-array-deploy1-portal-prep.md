---
title: Portal prep voor virtuele StorSimple-matrix | Microsoft Docs
description: Eerste zelfstudie voor het implementeren van virtuele StorSimple-matrix bestaat uit het voorbereiden van de Azure-portal
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 68a4cfd3-94c9-46cb-805c-46217290ce02
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 3d0801053721f98ce7a2b0fcbe3c65da8dbdd8d3
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="deploy-storsimple-virtual-array---prepare-the-azure-portal"></a><span data-ttu-id="59555-103">StorSimple virtuele matrix implementeren: voorbereiden van de Azure-portal</span><span class="sxs-lookup"><span data-stu-id="59555-103">Deploy StorSimple Virtual Array - Prepare the Azure portal</span></span>

![](./media/storsimple-virtual-array-deploy1-portal-prep/getstarted4.png)
## <a name="overview"></a><span data-ttu-id="59555-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="59555-104">Overview</span></span>

<span data-ttu-id="59555-105">Dit is het eerste artikel in de reeks van zelfstudies voor implementatie vereist voor het implementeren van uw virtuele matrix volledig als een bestandsserver of een iSCSI-server met het Resource Manager-model.</span><span class="sxs-lookup"><span data-stu-id="59555-105">This is the first article in the series of deployment tutorials required to completely deploy your virtual array as a file server or an iSCSI server using the Resource Manager model.</span></span> <span data-ttu-id="59555-106">In dit artikel beschrijft de voorbereiding is vereist voor het maken en configureren van uw StorSimple-apparaat Manager-service voorafgaand aan het inrichten van een virtuele-matrix.</span><span class="sxs-lookup"><span data-stu-id="59555-106">This article describes the preparation required to create and configure your StorSimple Device Manager service prior to provisioning a virtual array.</span></span> <span data-ttu-id="59555-107">In dit artikel bevat ook koppelingen uit naar een Configuratiecontrolelijst voor implementatie en configuratie vereisten.</span><span class="sxs-lookup"><span data-stu-id="59555-107">This article also links out to a deployment configuration checklist and configuration prerequisites.</span></span>

<span data-ttu-id="59555-108">U hebt beheerdersbevoegdheden nodig om het installatie- en configuratieproces uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="59555-108">You need administrator privileges to complete the setup and configuration process.</span></span> <span data-ttu-id="59555-109">Het is raadzaam om de configuratiecontrolelijst voor implementatie te controleren voordat u begint.</span><span class="sxs-lookup"><span data-stu-id="59555-109">We recommend that you review the deployment configuration checklist before you begin.</span></span> <span data-ttu-id="59555-110">De portal voorbereiding duurt minder dan 10 minuten.</span><span class="sxs-lookup"><span data-stu-id="59555-110">The portal preparation takes less than 10 minutes.</span></span>

<span data-ttu-id="59555-111">De informatie die is gepubliceerd in dit artikel geldt voor de implementatie van het virtuele StorSimple-matrices in de Azure-portal en Microsoft Azure Government Cloud.</span><span class="sxs-lookup"><span data-stu-id="59555-111">The information published in this article applies to the deployment of StorSimple Virtual Arrays in the Azure portal and Microsoft Azure Government Cloud.</span></span>

### <a name="get-started"></a><span data-ttu-id="59555-112">Aan de slag</span><span class="sxs-lookup"><span data-stu-id="59555-112">Get started</span></span>
<span data-ttu-id="59555-113">De implementatiewerkstroom bestaat uit het voorbereiden van de portal, het inrichten van een virtuele-matrix in uw gevirtualiseerde omgeving en de installatie voltooien.</span><span class="sxs-lookup"><span data-stu-id="59555-113">The deployment workflow consists of preparing the portal, provisioning a virtual array in your virtualized environment, and completing the setup.</span></span> <span data-ttu-id="59555-114">Om te beginnen met de implementatie van het virtuele StorSimple-matrix als een bestandsserver of een server met iSCSI-, moet u verwijzen naar de volgende gebruikmaking bronnen.</span><span class="sxs-lookup"><span data-stu-id="59555-114">To get started with the StorSimple Virtual Array deployment as a file server or an iSCSI server, you need to refer to the following tabulated resources.</span></span>

#### <a name="deployment-articles"></a><span data-ttu-id="59555-115">Artikelen over implementatie</span><span class="sxs-lookup"><span data-stu-id="59555-115">Deployment articles</span></span>

<span data-ttu-id="59555-116">Raadpleeg de volgende artikelen in de voorgeschreven volgorde voor het implementeren van uw virtuele StorSimple-matrix.</span><span class="sxs-lookup"><span data-stu-id="59555-116">To deploy your StorSimple Virtual Array, refer to the following articles in the prescribed sequence.</span></span>

| **#** | <span data-ttu-id="59555-117">**In deze stap**</span><span class="sxs-lookup"><span data-stu-id="59555-117">**In this step**</span></span> | <span data-ttu-id="59555-118">**U dit wilt doen...**</span><span class="sxs-lookup"><span data-stu-id="59555-118">**You do this …**</span></span> | <span data-ttu-id="59555-119">**En gebruik van deze documenten.**</span><span class="sxs-lookup"><span data-stu-id="59555-119">**And use these documents.**</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="59555-120">1.</span><span class="sxs-lookup"><span data-stu-id="59555-120">1.</span></span> |<span data-ttu-id="59555-121">**De Azure portal instellen**</span><span class="sxs-lookup"><span data-stu-id="59555-121">**Set up the Azure portal**</span></span> |<span data-ttu-id="59555-122">Maak en configureer uw StorSimple-apparaat Manager-service vóór het inrichten van een virtueel StorSimple-matrix.</span><span class="sxs-lookup"><span data-stu-id="59555-122">Create and configure your StorSimple Device Manager service prior to provisioning a StorSimple Virtual Array.</span></span> |[<span data-ttu-id="59555-123">Voorbereiden van de portal</span><span class="sxs-lookup"><span data-stu-id="59555-123">Prepare the portal</span></span>](storsimple-virtual-array-deploy1-portal-prep.md) |
| <span data-ttu-id="59555-124">2.</span><span class="sxs-lookup"><span data-stu-id="59555-124">2.</span></span> |<span data-ttu-id="59555-125">**De virtuele matrix inrichten**</span><span class="sxs-lookup"><span data-stu-id="59555-125">**Provision the Virtual Array**</span></span> |<span data-ttu-id="59555-126">Voor Hyper-V, inrichten en verbinding maken met een virtueel StorSimple-matrix op een hostsysteem met Hyper-V op Windows Server 2012 R2, Windows Server 2012 of Windows Server 2008 R2.</span><span class="sxs-lookup"><span data-stu-id="59555-126">For Hyper-V, provision and connect to a StorSimple Virtual Array on a host system running Hyper-V on Windows Server 2012 R2, Windows Server 2012, or Windows Server 2008 R2.</span></span> <br></br> <br></br> <span data-ttu-id="59555-127">Voor VMware, inrichten en verbinding maken met een virtueel StorSimple-matrix op een hostsysteem met VMware ESXi 5.5 en hoger.</span><span class="sxs-lookup"><span data-stu-id="59555-127">For VMware, provision and connect to a StorSimple Virtual Array on a host system running VMware ESXi 5.5 and above.</span></span><br></br> |[<span data-ttu-id="59555-128">Inrichten van een virtuele-matrix in Hyper-V</span><span class="sxs-lookup"><span data-stu-id="59555-128">Provision a virtual array in Hyper-V</span></span>](storsimple-virtual-array-deploy2-provision-hyperv.md) <br></br> <br></br> [<span data-ttu-id="59555-129">Een virtuele-matrix in VMware inrichten</span><span class="sxs-lookup"><span data-stu-id="59555-129">Provision a virtual array in VMware</span></span>](storsimple-virtual-array-deploy2-provision-vmware.md) |
| <span data-ttu-id="59555-130">3.</span><span class="sxs-lookup"><span data-stu-id="59555-130">3.</span></span> |<span data-ttu-id="59555-131">**Instellen van de virtuele matrix**</span><span class="sxs-lookup"><span data-stu-id="59555-131">**Set up the Virtual Array**</span></span> |<span data-ttu-id="59555-132">Eerste installatie uitvoeren, registreren van uw StorSimple-bestandsserver en de Apparaatinstelling voor uw bestandsserver.</span><span class="sxs-lookup"><span data-stu-id="59555-132">For your file server, perform initial setup, register your StorSimple file server, and complete the device setup.</span></span> <span data-ttu-id="59555-133">Vervolgens kunt u SMB-shares inrichten.</span><span class="sxs-lookup"><span data-stu-id="59555-133">You can then provision SMB shares.</span></span> <br></br> <br></br> <span data-ttu-id="59555-134">Eerste installatie uitvoeren voor uw server met iSCSI-, uw StorSimple iSCSI-server registreren en voltooit de installatie van het apparaat.</span><span class="sxs-lookup"><span data-stu-id="59555-134">For your iSCSI server, perform initial setup, register your StorSimple iSCSI server, and complete the device setup.</span></span> <span data-ttu-id="59555-135">Vervolgens kunt u iSCSI-volumes inrichten.</span><span class="sxs-lookup"><span data-stu-id="59555-135">You can then provision iSCSI volumes.</span></span> |[<span data-ttu-id="59555-136">Virtuele matrix instellen als bestandsserver</span><span class="sxs-lookup"><span data-stu-id="59555-136">Set up virtual array as file server</span></span>](storsimple-virtual-array-deploy3-fs-setup.md)<br></br> <br></br>[<span data-ttu-id="59555-137">Virtuele matrix ingesteld als iSCSI-server</span><span class="sxs-lookup"><span data-stu-id="59555-137">Set up virtual array as iSCSI server</span></span>](storsimple-virtual-array-deploy3-iscsi-setup.md) |

<span data-ttu-id="59555-138">U kunt nu beginnen met het instellen van de Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="59555-138">You can now begin to set up the Azure portal.</span></span>

## <a name="configuration-checklist"></a><span data-ttu-id="59555-139">Configuratiecontrolelijst</span><span class="sxs-lookup"><span data-stu-id="59555-139">Configuration checklist</span></span>

<span data-ttu-id="59555-140">De Configuratiecontrolelijst bevat de informatie die u verzamelen moet voordat u de software op uw virtuele StorSimple-matrix configureren.</span><span class="sxs-lookup"><span data-stu-id="59555-140">The configuration checklist describes the information that you need to collect before you configure the software on your StorSimple Virtual Array.</span></span> <span data-ttu-id="59555-141">Deze informatie tevoren voorbereid helpt bij het stroomlijnen van de implementatie van het StorSimple-apparaat in uw omgeving.</span><span class="sxs-lookup"><span data-stu-id="59555-141">Preparing this information ahead of time helps streamline the process of deploying the StorSimple device in your environment.</span></span> <span data-ttu-id="59555-142">Afhankelijk van het feit of uw virtuele StorSimple-matrix is geïmplementeerd als een bestandsserver of een iSCSI-server, moet u een van de volgende controlelijsten.</span><span class="sxs-lookup"><span data-stu-id="59555-142">Depending upon whether your StorSimple Virtual Array is deployed as a file server or an iSCSI server, you need one of the following checklists.</span></span>

* <span data-ttu-id="59555-143">Download de [Server Configuratiecontrolelijst voor StorSimple virtuele matrix bestand](http://download.microsoft.com/download/E/E/6/EE690BB0-B442-4B84-8165-4731EE727ACF/MicrosoftAzureStorSimpleVirtualArrayFileServerConfigurationChecklist.pdf).</span><span class="sxs-lookup"><span data-stu-id="59555-143">Download the [StorSimple Virtual Array File Server Configuration Checklist](http://download.microsoft.com/download/E/E/6/EE690BB0-B442-4B84-8165-4731EE727ACF/MicrosoftAzureStorSimpleVirtualArrayFileServerConfigurationChecklist.pdf).</span></span>
* <span data-ttu-id="59555-144">Download de [virtuele StorSimple-matrix iSCSI Server Configuratiecontrolelijst](http://download.microsoft.com/download/E/E/6/EE690BB0-B442-4B84-8165-4731EE727ACF/MicrosoftAzureStorSimpleVirtualArrayiSCSIServerConfigurationChecklist.pdf).</span><span class="sxs-lookup"><span data-stu-id="59555-144">Download the [StorSimple Virtual Array iSCSI Server Configuration Checklist](http://download.microsoft.com/download/E/E/6/EE690BB0-B442-4B84-8165-4731EE727ACF/MicrosoftAzureStorSimpleVirtualArrayiSCSIServerConfigurationChecklist.pdf).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="59555-145">Vereisten</span><span class="sxs-lookup"><span data-stu-id="59555-145">Prerequisites</span></span>

<span data-ttu-id="59555-146">Hier vindt u de configuratievereisten voor uw StorSimple-apparaat Manager-service, uw virtuele StorSimple-matrix en het datacenternetwerk.</span><span class="sxs-lookup"><span data-stu-id="59555-146">Here you find the configuration prerequisites for your StorSimple Device Manager service, your StorSimple Virtual Array, and the datacenter network.</span></span>

### <a name="for-the-storsimple-device-manager-service"></a><span data-ttu-id="59555-147">Voor de StorSimple-apparaatbeheerfunctie</span><span class="sxs-lookup"><span data-stu-id="59555-147">For the StorSimple Device Manager service</span></span>

<span data-ttu-id="59555-148">Zorg voordat u begint voor het volgende:</span><span class="sxs-lookup"><span data-stu-id="59555-148">Before you begin, make sure that:</span></span>

* <span data-ttu-id="59555-149">U hebt een Microsoft-account met toegangsreferenties.</span><span class="sxs-lookup"><span data-stu-id="59555-149">You have your Microsoft account with access credentials.</span></span>
* <span data-ttu-id="59555-150">U hebt een Microsoft Azure Storage-account met toegangsreferenties.</span><span class="sxs-lookup"><span data-stu-id="59555-150">You have your Microsoft Azure storage account with access credentials.</span></span>
* <span data-ttu-id="59555-151">Uw Microsoft Azure-abonnement moet worden ingeschakeld voor Apparaatbeheer van StorSimple-service.</span><span class="sxs-lookup"><span data-stu-id="59555-151">Your Microsoft Azure subscription should be enabled for StorSimple Device Manager service.</span></span>

### <a name="for-the-storsimple-virtual-array"></a><span data-ttu-id="59555-152">Voor de virtuele StorSimple-matrix</span><span class="sxs-lookup"><span data-stu-id="59555-152">For the StorSimple Virtual Array</span></span>

<span data-ttu-id="59555-153">Voordat u een virtuele-matrix implementeert, zorg ervoor dat:</span><span class="sxs-lookup"><span data-stu-id="59555-153">Before you deploy a virtual array, make sure that:</span></span>

* <span data-ttu-id="59555-154">U hebt toegang tot een hostsysteem met Hyper-V in Windows Server 2008 R2 of later of VMware (ESXi 5.5 of hoger) die kan worden gebruikt voor een voorziening van een apparaat.</span><span class="sxs-lookup"><span data-stu-id="59555-154">You have access to a host system running Hyper-V on Windows Server 2008 R2 or later or VMware (ESXi 5.5 or later) that can be used to a provision a device.</span></span>
* <span data-ttu-id="59555-155">Het hostsysteem kan toe te wijzen aan de volgende bronnen voor het inrichten van uw virtuele matrix:</span><span class="sxs-lookup"><span data-stu-id="59555-155">The host system is able to dedicate the following resources to provision your virtual array:</span></span>
  
  * <span data-ttu-id="59555-156">Een minimum van 4 kernen.</span><span class="sxs-lookup"><span data-stu-id="59555-156">A minimum of 4 cores.</span></span>
  * <span data-ttu-id="59555-157">Ten minste 8 GB aan RAM-geheugen.</span><span class="sxs-lookup"><span data-stu-id="59555-157">At least 8 GB of RAM.</span></span> <span data-ttu-id="59555-158">Als u van plan bent de virtuele matrix als bestandsserver te configureren, ondersteunt 8 GB 2 miljoen bestanden.</span><span class="sxs-lookup"><span data-stu-id="59555-158">If you plan to configure the virtual array as file server, 8 GB supports 2 million files.</span></span> <span data-ttu-id="59555-159">U moet 16 GB RAM-geheugen voor de ondersteuning van 2-4 miljoen bestanden.</span><span class="sxs-lookup"><span data-stu-id="59555-159">You need 16 GB RAM to support 2 - 4 million files.</span></span>
  * <span data-ttu-id="59555-160">Één netwerkinterface.</span><span class="sxs-lookup"><span data-stu-id="59555-160">One network interface.</span></span>
  * <span data-ttu-id="59555-161">500 GB virtuele schijf voor systeemgegevens.</span><span class="sxs-lookup"><span data-stu-id="59555-161">A 500 GB virtual disk for system data.</span></span>

### <a name="for-the-datacenter-network"></a><span data-ttu-id="59555-162">Voor het datacenternetwerk</span><span class="sxs-lookup"><span data-stu-id="59555-162">For the datacenter network</span></span>

<span data-ttu-id="59555-163">Zorg voordat u begint voor het volgende:</span><span class="sxs-lookup"><span data-stu-id="59555-163">Before you begin, make sure that:</span></span>

* <span data-ttu-id="59555-164">Het netwerk in uw datacenter is geconfigureerd volgens de vereisten voor uw StorSimple-apparaat.</span><span class="sxs-lookup"><span data-stu-id="59555-164">The network in your datacenter is configured as per the networking requirements for your StorSimple device.</span></span> <span data-ttu-id="59555-165">Zie voor meer informatie de [StorSimple virtuele matrix systeemvereisten](storsimple-ova-system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="59555-165">For more information, see the [StorSimple Virtual Array System Requirements](storsimple-ova-system-requirements.md).</span></span>
* <span data-ttu-id="59555-166">Uw virtuele StorSimple-matrix heeft een speciale 5 Mbps internetbandbreedte (of meer) beschikbaar te allen tijde.</span><span class="sxs-lookup"><span data-stu-id="59555-166">Your StorSimple Virtual Array has a dedicated 5 Mbps Internet bandwidth (or more) available at all times.</span></span> <span data-ttu-id="59555-167">Deze bandbreedte mag niet worden gedeeld met andere toepassingen.</span><span class="sxs-lookup"><span data-stu-id="59555-167">This bandwidth should not be shared with any other applications.</span></span>

## <a name="step-by-step-preparation"></a><span data-ttu-id="59555-168">Stapsgewijze voorbereiding</span><span class="sxs-lookup"><span data-stu-id="59555-168">Step-by-step preparation</span></span>

<span data-ttu-id="59555-169">Gebruik de volgende stapsgewijze instructies voor het voorbereiden van de portal voor de service Manager voor StorSimple-apparaat.</span><span class="sxs-lookup"><span data-stu-id="59555-169">Use the following step-by-step instructions to prepare your portal for the StorSimple Device Manager service.</span></span>

## <a name="step-1-create-a-new-service"></a><span data-ttu-id="59555-170">Stap 1: een nieuwe service maken</span><span class="sxs-lookup"><span data-stu-id="59555-170">Step 1: Create a new service</span></span>

<span data-ttu-id="59555-171">Slechts één exemplaar van de service Manager voor StorSimple-apparaat kunt beheren meerdere virtuele StorSimple-matrices.</span><span class="sxs-lookup"><span data-stu-id="59555-171">A single instance of the StorSimple Device Manager service can manage multiple StorSimple Virtual Arrays.</span></span> <span data-ttu-id="59555-172">Voer de volgende stappen uit om een exemplaar van de StorSimple-apparaatbeheerfunctie uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="59555-172">Perform the following steps to create an instance of the StorSimple Device Manager service.</span></span> <span data-ttu-id="59555-173">Als u een bestaande service Manager voor StorSimple-apparaat voor het beheren van uw virtuele matrices hebt, deze stap overslaan en gaat u naar [stap 2: de serviceregistratiesleutel ophalen](#step-2-get-the-service-registration-key).</span><span class="sxs-lookup"><span data-stu-id="59555-173">If you have an existing StorSimple Device Manager service to manage your virtual arrays, skip this step and go to [Step 2: Get the service registration key](#step-2-get-the-service-registration-key).</span></span>

[!INCLUDE [storsimple-virtual-array-create-new-service](../../includes/storsimple-virtual-array-create-new-service.md)]

> [!IMPORTANT]
> <span data-ttu-id="59555-174">Als u de service niet hebt ingeschakeld om automatisch een opslagaccount te maken, moet u minimaal één opslagaccount maken nadat u een service hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="59555-174">If you did not enable the automatic creation of a storage account with your service, you will need to create at least one storage account after you have successfully created a service.</span></span>
> 
> * <span data-ttu-id="59555-175">Als u niet automatisch een opslagaccount hebt gemaakt, gaat u naar [Een nieuw opslagaccount voor de service configureren](#optional-step-configure-a-new-storage-account-for-the-service) voor gedetailleerde instructies.</span><span class="sxs-lookup"><span data-stu-id="59555-175">If you did not create a storage account automatically, go to [Configure a new storage account for the service](#optional-step-configure-a-new-storage-account-for-the-service) for detailed instructions.</span></span>
> * <span data-ttu-id="59555-176">Als u het automatisch maken van een opslagaccount hebt ingeschakeld, gaat u naar [Stap 2: de serviceregistratiesleutel ophalen](#step-2-get-the-service-registration-key).</span><span class="sxs-lookup"><span data-stu-id="59555-176">If you enabled the automatic creation of a storage account, go to [Step 2: Get the service registration key](#step-2-get-the-service-registration-key).</span></span>
> 
> 

## <a name="step-2-get-the-service-registration-key"></a><span data-ttu-id="59555-177">Stap 2: de serviceregistratiesleutel ophalen</span><span class="sxs-lookup"><span data-stu-id="59555-177">Step 2: Get the service registration key</span></span>

<span data-ttu-id="59555-178">Wanneer de StorSimple-apparaatbeheerfunctie bedrijfsklaar is, moet u de serviceregistratiesleutel ophalen.</span><span class="sxs-lookup"><span data-stu-id="59555-178">After the StorSimple Device Manager service is up and running, you will need to get the service registration key.</span></span> <span data-ttu-id="59555-179">Deze sleutel wordt gebruikt om het StorSimple-apparaat te registreren en te verbinden met de service.</span><span class="sxs-lookup"><span data-stu-id="59555-179">This key is used to register and connect your StorSimple device with the service.</span></span>

<span data-ttu-id="59555-180">Voer de volgende stappen uit in de [Azure-portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="59555-180">Perform the following steps in the [Azure portal](https://portal.azure.com/).</span></span>

[!INCLUDE [storsimple-virtual-array-get-service-registration-key](../../includes/storsimple-virtual-array-get-service-registration-key.md)]

> [!NOTE]
> <span data-ttu-id="59555-181">De serviceregistratiesleutel wordt gebruikt voor het registreren van alle Apparaatbeheer StorSimple-apparaten die moeten worden geregistreerd bij uw StorSimple-apparaat Manager-service.</span><span class="sxs-lookup"><span data-stu-id="59555-181">The service registration key is used to register all the StorSimple Device Manager devices that need to register with your StorSimple Device Manager service.</span></span>
> 
> 

## <a name="step-3-download-the-virtual-array-image"></a><span data-ttu-id="59555-182">Stap 3: Download de installatiekopie van het virtuele matrix</span><span class="sxs-lookup"><span data-stu-id="59555-182">Step 3: Download the virtual array image</span></span>

<span data-ttu-id="59555-183">Nadat u de serviceregistratiesleutel hebt, moet u de installatiekopie van het juiste virtuele matrix voor het inrichten van een virtuele-matrix op uw hostsysteem downloaden.</span><span class="sxs-lookup"><span data-stu-id="59555-183">After you have the service registration key, you will need to download the appropriate virtual array image to provision a virtual array on your host system.</span></span> <span data-ttu-id="59555-184">Installatiekopieën van het virtuele matrix zijn specifiek besturingssysteem en kunnen worden gedownload vanaf de pagina snel starten in de Azure portal.</span><span class="sxs-lookup"><span data-stu-id="59555-184">The virtual array images are operating system specific and can be downloaded from the Quick Start page in the Azure portal.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="59555-185">De software die wordt uitgevoerd op de virtuele StorSimple-matrix kan alleen worden gebruikt met de service Manager voor StorSimple-apparaat.</span><span class="sxs-lookup"><span data-stu-id="59555-185">The software running on the StorSimple Virtual Array may only be used with the StorSimple Device Manager service.</span></span>
> 
> 

<span data-ttu-id="59555-186">Voer de volgende stappen uit in de [Azure-portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="59555-186">Perform the following steps in the [Azure portal](https://portal.azure.com/).</span></span>

#### <a name="to-get-the-virtual-array-image"></a><span data-ttu-id="59555-187">De installatiekopie van het virtuele matrix ophalen</span><span class="sxs-lookup"><span data-stu-id="59555-187">To get the virtual array image</span></span>

1. <span data-ttu-id="59555-188">Meld u aan bij de [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="59555-188">Sign into the [Azure portal](https://portal.azure.com/).</span></span> 
2. <span data-ttu-id="59555-189">Klik in de Azure-portal op **Bladeren > Managers voor apparaatregistratie StorSimple**.</span><span class="sxs-lookup"><span data-stu-id="59555-189">In the Azure portal, click **Browse > StorSimple Device Managers**.</span></span>
3. <span data-ttu-id="59555-190">Selecteer een bestaande Apparaatbeheer StorSimple-service.</span><span class="sxs-lookup"><span data-stu-id="59555-190">Select an existing StorSimple Device Manager service.</span></span> <span data-ttu-id="59555-191">In de **StorSimple Apparaatbeheer** blade, klikt u op **Quick Start**.</span><span class="sxs-lookup"><span data-stu-id="59555-191">In the **StorSimple Device Manager** blade, click **Quick Start**.</span></span> 
4. <span data-ttu-id="59555-192">Klik op de koppeling die overeenkomt met de installatiekopie die u wilt downloaden uit het Microsoft Download Center.</span><span class="sxs-lookup"><span data-stu-id="59555-192">Click the link corresponding to the image that you want to download from the Microsoft Download Center.</span></span> <span data-ttu-id="59555-193">De afbeeldingsbestanden zijn ongeveer 4,8 GB.</span><span class="sxs-lookup"><span data-stu-id="59555-193">The image files are approximately 4.8 GB.</span></span>
   
   * <span data-ttu-id="59555-194">VHDX voor Hyper-V op Windows Server 2012 en hoger</span><span class="sxs-lookup"><span data-stu-id="59555-194">VHDX for Hyper-V on Windows Server 2012 and later</span></span>
   * <span data-ttu-id="59555-195">VHD voor Hyper-V in Windows Server 2008 R2 en hoger</span><span class="sxs-lookup"><span data-stu-id="59555-195">VHD for Hyper-V on Windows Server 2008 R2 and later</span></span>
   * <span data-ttu-id="59555-196">VMDK voor VMWare ESXi 5.5 en hoger</span><span class="sxs-lookup"><span data-stu-id="59555-196">VMDK for VMWare ESXi 5.5 and later</span></span>
5. <span data-ttu-id="59555-197">Download en pak het bestand naar een lokaal station, waardoor een notitie van waarin de uitgepakte bestand zich bevindt.</span><span class="sxs-lookup"><span data-stu-id="59555-197">Download and unzip the file to a local drive, making a note of where the unzipped file is located.</span></span>

## <a name="optional-step-configure-a-new-storage-account-for-the-service"></a><span data-ttu-id="59555-198">Optionele stap: een nieuw opslagaccount voor de service configureren</span><span class="sxs-lookup"><span data-stu-id="59555-198">Optional step: Configure a new storage account for the service</span></span>

<span data-ttu-id="59555-199">Deze stap is optioneel en moet worden uitgevoerd alleen als u het automatisch maken van een opslagaccount met uw service niet hebt ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="59555-199">This step is optional and should be performed only if you did not enable the automatic creation of a storage account with your service.</span></span>

<span data-ttu-id="59555-200">Als u maken van een Azure storage-account in een andere regio wilt, Zie [het maken van een opslagaccount](../storage/common/storage-create-storage-account.md#create-a-storage-account) voor stapsgewijze instructies.</span><span class="sxs-lookup"><span data-stu-id="59555-200">If you need to create an Azure storage account in a different region, see [How to create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) for step-by-step instructions.</span></span>

<span data-ttu-id="59555-201">Voer de volgende stappen uit in de [Azure-portal](https://ms.portal.azure.com/) op de pagina van de service Manager voor StorSimple-apparaat toevoegen van een bestaand Microsoft Azure-opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="59555-201">Perform the following steps in the [Azure portal](https://ms.portal.azure.com/) on the StorSimple Device Manager service page to add an existing Microsoft Azure storage account.</span></span>

#### <a name="to-add-a-storage-account-credential-that-has-the-same-azure-subscription-as-the-device-manager-service"></a><span data-ttu-id="59555-202">Toevoegen van een referentie storage-account met de dezelfde Azure-abonnement als de service voor Apparaatbeheer</span><span class="sxs-lookup"><span data-stu-id="59555-202">To add a storage account credential that has the same Azure subscription as the Device Manager service</span></span>

1. <span data-ttu-id="59555-203">Navigeer naar uw service Apparaatbeheer, selecteert en dubbelklik erop.</span><span class="sxs-lookup"><span data-stu-id="59555-203">Navigate to your Device Manager service, select and double-click it.</span></span> <span data-ttu-id="59555-204">Hiermee opent u de **overzicht** blade.</span><span class="sxs-lookup"><span data-stu-id="59555-204">This opens the **Overview** blade.</span></span>
2. <span data-ttu-id="59555-205">Selecteer **opslagaccountreferenties** binnen de **configuratie** sectie.</span><span class="sxs-lookup"><span data-stu-id="59555-205">Select **Storage account credentials** within the **Configuration** section.</span></span>
3. <span data-ttu-id="59555-206">Klik op **Add**.</span><span class="sxs-lookup"><span data-stu-id="59555-206">Click **Add**.</span></span>
4. <span data-ttu-id="59555-207">In de **een opslagaccount toevoegen** blade het volgende doen:</span><span class="sxs-lookup"><span data-stu-id="59555-207">In the **Add a storage account** blade, do the following:</span></span>
   
    1. <span data-ttu-id="59555-208">Voor **abonnement**, selecteer **huidige**.</span><span class="sxs-lookup"><span data-stu-id="59555-208">For **Subscription**, select **Current**.</span></span>
   
    2. <span data-ttu-id="59555-209">Geef de naam van uw Azure storage-account.</span><span class="sxs-lookup"><span data-stu-id="59555-209">Provide the name of your Azure storage account.</span></span>
   
    3. <span data-ttu-id="59555-210">Selecteer **inschakelen** voor het maken van een beveiligd kanaal voor netwerkcommunicatie tussen uw StorSimple-apparaat en de cloud.</span><span class="sxs-lookup"><span data-stu-id="59555-210">Select **Enable** to create a secure channel for network communication between your StorSimple device and the cloud.</span></span> <span data-ttu-id="59555-211">Selecteer **uitschakelen** alleen als u in een privécloud werkt.</span><span class="sxs-lookup"><span data-stu-id="59555-211">Select **Disable** only if you are operating within a private cloud.</span></span>
   
    4. <span data-ttu-id="59555-212">Klik op **Add**.</span><span class="sxs-lookup"><span data-stu-id="59555-212">Click **Add**.</span></span> <span data-ttu-id="59555-213">U wordt gewaarschuwd nadat het opslagaccount is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="59555-213">You are notified after the storage account is successfully created.</span></span><br></br>
   
     ![Een bestaande referentie voor de storage-account toevoegen](./media/storsimple-virtual-array-manage-storage-accounts/ova-add-storageacct.png)

## <a name="next-step"></a><span data-ttu-id="59555-215">Volgende stap</span><span class="sxs-lookup"><span data-stu-id="59555-215">Next step</span></span>

<span data-ttu-id="59555-216">De volgende stap is het inrichten van een virtuele machine voor uw virtuele StorSimple-matrix.</span><span class="sxs-lookup"><span data-stu-id="59555-216">The next step is to provision a virtual machine for your StorSimple Virtual Array.</span></span> <span data-ttu-id="59555-217">Raadpleeg de gedetailleerde instructies in, afhankelijk van uw hostbesturingssysteem:</span><span class="sxs-lookup"><span data-stu-id="59555-217">Depending on your host operating system, see the detailed instructions in:</span></span>

* [<span data-ttu-id="59555-218">Inrichten van een virtueel StorSimple-matrix in Hyper-V</span><span class="sxs-lookup"><span data-stu-id="59555-218">Provision a StorSimple Virtual Array in Hyper-V</span></span>](storsimple-virtual-array-deploy2-provision-hyperv.md)
* [<span data-ttu-id="59555-219">Een virtueel StorSimple-matrix in VMware inrichten</span><span class="sxs-lookup"><span data-stu-id="59555-219">Provision a StorSimple Virtual Array in VMware</span></span>](storsimple-virtual-array-deploy2-provision-vmware.md)


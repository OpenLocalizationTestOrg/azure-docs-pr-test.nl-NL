---
title: aaaPortal prep voor virtuele StorSimple-matrix | Microsoft Docs
description: Eerste zelfstudie toodeploy virtuele StorSimple-matrix bestaat uit het voorbereiden van hello Azure-portal
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
ms.openlocfilehash: 5332b235e7296a9274f2e7dafcdf72f4b9cdadf6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-storsimple-virtual-array---prepare-hello-azure-portal"></a><span data-ttu-id="2ee88-103">StorSimple virtuele matrix implementeren: voorbereiden hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="2ee88-103">Deploy StorSimple Virtual Array - Prepare hello Azure portal</span></span>

![](./media/storsimple-virtual-array-deploy1-portal-prep/getstarted4.png)
## <a name="overview"></a><span data-ttu-id="2ee88-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="2ee88-104">Overview</span></span>

<span data-ttu-id="2ee88-105">Dit is Hallo eerste van het artikel in Hallo reeks zelfstudies voor implementatie vereist toocompletely uw virtuele matrix implementeren als een bestandsserver of een iSCSI-server met behulp van Hallo Resource Manager-model.</span><span class="sxs-lookup"><span data-stu-id="2ee88-105">This is hello first article in hello series of deployment tutorials required toocompletely deploy your virtual array as a file server or an iSCSI server using hello Resource Manager model.</span></span> <span data-ttu-id="2ee88-106">Dit artikel beschrijft Hallo vereiste voorbereiding toocreate en configureren van uw StorSimple-apparaat Manager service voorafgaande tooprovisioning een virtuele-matrix.</span><span class="sxs-lookup"><span data-stu-id="2ee88-106">This article describes hello preparation required toocreate and configure your StorSimple Device Manager service prior tooprovisioning a virtual array.</span></span> <span data-ttu-id="2ee88-107">In dit artikel bevat ook koppelingen uit tooa configuration checklist- en vereisten voor implementatie.</span><span class="sxs-lookup"><span data-stu-id="2ee88-107">This article also links out tooa deployment configuration checklist and configuration prerequisites.</span></span>

<span data-ttu-id="2ee88-108">U moet administrator-bevoegdheden toocomplete Hallo installatie- en configuratieproces.</span><span class="sxs-lookup"><span data-stu-id="2ee88-108">You need administrator privileges toocomplete hello setup and configuration process.</span></span> <span data-ttu-id="2ee88-109">U wordt aangeraden Hallo Configuratiecontrolelijst voor implementatie te controleren voordat u begint.</span><span class="sxs-lookup"><span data-stu-id="2ee88-109">We recommend that you review hello deployment configuration checklist before you begin.</span></span> <span data-ttu-id="2ee88-110">Hallo portal voorbereiding duurt minder dan 10 minuten.</span><span class="sxs-lookup"><span data-stu-id="2ee88-110">hello portal preparation takes less than 10 minutes.</span></span>

<span data-ttu-id="2ee88-111">Hallo-informatie in dit artikel wordt gepubliceerd geldt toohello implementatie van het virtuele StorSimple-matrices in hello Azure-portal en Microsoft Azure Government Cloud.</span><span class="sxs-lookup"><span data-stu-id="2ee88-111">hello information published in this article applies toohello deployment of StorSimple Virtual Arrays in hello Azure portal and Microsoft Azure Government Cloud.</span></span>

### <a name="get-started"></a><span data-ttu-id="2ee88-112">Aan de slag</span><span class="sxs-lookup"><span data-stu-id="2ee88-112">Get started</span></span>
<span data-ttu-id="2ee88-113">werkstroom Hallo-implementatie bestaat uit Hallo portal voorbereiden, het inrichten van een virtuele-matrix in uw gevirtualiseerde omgeving en Hallo setup is voltooid.</span><span class="sxs-lookup"><span data-stu-id="2ee88-113">hello deployment workflow consists of preparing hello portal, provisioning a virtual array in your virtualized environment, and completing hello setup.</span></span> <span data-ttu-id="2ee88-114">tooget gestart met Hallo virtuele StorSimple-matrix implementatie als een bestandsserver of een iSCSI-server, moet u toorefer toohello gebruikmaking resources te volgen.</span><span class="sxs-lookup"><span data-stu-id="2ee88-114">tooget started with hello StorSimple Virtual Array deployment as a file server or an iSCSI server, you need toorefer toohello following tabulated resources.</span></span>

#### <a name="deployment-articles"></a><span data-ttu-id="2ee88-115">Artikelen over implementatie</span><span class="sxs-lookup"><span data-stu-id="2ee88-115">Deployment articles</span></span>

<span data-ttu-id="2ee88-116">toodeploy uw virtuele StorSimple-matrix, Raadpleeg toohello artikelen in de reeks voorgeschreven hello te volgen.</span><span class="sxs-lookup"><span data-stu-id="2ee88-116">toodeploy your StorSimple Virtual Array, refer toohello following articles in hello prescribed sequence.</span></span>

| **#** | <span data-ttu-id="2ee88-117">**In deze stap**</span><span class="sxs-lookup"><span data-stu-id="2ee88-117">**In this step**</span></span> | <span data-ttu-id="2ee88-118">**U dit wilt doen...**</span><span class="sxs-lookup"><span data-stu-id="2ee88-118">**You do this …**</span></span> | <span data-ttu-id="2ee88-119">**En gebruik van deze documenten.**</span><span class="sxs-lookup"><span data-stu-id="2ee88-119">**And use these documents.**</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="2ee88-120">1.</span><span class="sxs-lookup"><span data-stu-id="2ee88-120">1.</span></span> |<span data-ttu-id="2ee88-121">**Hello Azure-portal instellen**</span><span class="sxs-lookup"><span data-stu-id="2ee88-121">**Set up hello Azure portal**</span></span> |<span data-ttu-id="2ee88-122">Maak en configureer uw StorSimple-apparaat Manager service voorafgaande tooprovisioning een virtueel StorSimple-matrix.</span><span class="sxs-lookup"><span data-stu-id="2ee88-122">Create and configure your StorSimple Device Manager service prior tooprovisioning a StorSimple Virtual Array.</span></span> |[<span data-ttu-id="2ee88-123">Hallo portal voorbereiden</span><span class="sxs-lookup"><span data-stu-id="2ee88-123">Prepare hello portal</span></span>](storsimple-virtual-array-deploy1-portal-prep.md) |
| <span data-ttu-id="2ee88-124">2.</span><span class="sxs-lookup"><span data-stu-id="2ee88-124">2.</span></span> |<span data-ttu-id="2ee88-125">**Hallo virtuele matrix inrichten**</span><span class="sxs-lookup"><span data-stu-id="2ee88-125">**Provision hello Virtual Array**</span></span> |<span data-ttu-id="2ee88-126">Voor Hyper-V, inrichten en maak verbinding tooa virtuele StorSimple-matrix op een hostsysteem met Hyper-V op Windows Server 2012 R2, Windows Server 2012 of Windows Server 2008 R2.</span><span class="sxs-lookup"><span data-stu-id="2ee88-126">For Hyper-V, provision and connect tooa StorSimple Virtual Array on a host system running Hyper-V on Windows Server 2012 R2, Windows Server 2012, or Windows Server 2008 R2.</span></span> <br></br> <br></br> <span data-ttu-id="2ee88-127">Voor VMware, inrichten en verbinding maken met virtuele StorSimple-matrix tooa op een hostsysteem met VMware ESXi 5.5 en hoger.</span><span class="sxs-lookup"><span data-stu-id="2ee88-127">For VMware, provision and connect tooa StorSimple Virtual Array on a host system running VMware ESXi 5.5 and above.</span></span><br></br> |[<span data-ttu-id="2ee88-128">Inrichten van een virtuele-matrix in Hyper-V</span><span class="sxs-lookup"><span data-stu-id="2ee88-128">Provision a virtual array in Hyper-V</span></span>](storsimple-virtual-array-deploy2-provision-hyperv.md) <br></br> <br></br> [<span data-ttu-id="2ee88-129">Een virtuele-matrix in VMware inrichten</span><span class="sxs-lookup"><span data-stu-id="2ee88-129">Provision a virtual array in VMware</span></span>](storsimple-virtual-array-deploy2-provision-vmware.md) |
| <span data-ttu-id="2ee88-130">3.</span><span class="sxs-lookup"><span data-stu-id="2ee88-130">3.</span></span> |<span data-ttu-id="2ee88-131">**Hallo virtuele matrix instellen**</span><span class="sxs-lookup"><span data-stu-id="2ee88-131">**Set up hello Virtual Array**</span></span> |<span data-ttu-id="2ee88-132">Voor uw bestandsserver uitvoeren van de eerste installatie Apparaatinstelling Hallo en registreren van uw StorSimple-bestandsserver.</span><span class="sxs-lookup"><span data-stu-id="2ee88-132">For your file server, perform initial setup, register your StorSimple file server, and complete hello device setup.</span></span> <span data-ttu-id="2ee88-133">Vervolgens kunt u SMB-shares inrichten.</span><span class="sxs-lookup"><span data-stu-id="2ee88-133">You can then provision SMB shares.</span></span> <br></br> <br></br> <span data-ttu-id="2ee88-134">Eerste installatie uitvoeren voor uw server met iSCSI-, uw StorSimple iSCSI-server registreren en Apparaatinstelling Hallo.</span><span class="sxs-lookup"><span data-stu-id="2ee88-134">For your iSCSI server, perform initial setup, register your StorSimple iSCSI server, and complete hello device setup.</span></span> <span data-ttu-id="2ee88-135">Vervolgens kunt u iSCSI-volumes inrichten.</span><span class="sxs-lookup"><span data-stu-id="2ee88-135">You can then provision iSCSI volumes.</span></span> |[<span data-ttu-id="2ee88-136">Virtuele matrix instellen als bestandsserver</span><span class="sxs-lookup"><span data-stu-id="2ee88-136">Set up virtual array as file server</span></span>](storsimple-virtual-array-deploy3-fs-setup.md)<br></br> <br></br>[<span data-ttu-id="2ee88-137">Virtuele matrix ingesteld als iSCSI-server</span><span class="sxs-lookup"><span data-stu-id="2ee88-137">Set up virtual array as iSCSI server</span></span>](storsimple-virtual-array-deploy3-iscsi-setup.md) |

<span data-ttu-id="2ee88-138">U kunt nu beginnen met tooset up hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="2ee88-138">You can now begin tooset up hello Azure portal.</span></span>

## <a name="configuration-checklist"></a><span data-ttu-id="2ee88-139">Configuratiecontrolelijst</span><span class="sxs-lookup"><span data-stu-id="2ee88-139">Configuration checklist</span></span>

<span data-ttu-id="2ee88-140">Hallo Configuratiecontrolelijst beschrijft Hallo-gegevens die u toocollect nodig voordat u software Hallo op uw virtuele StorSimple-matrix configureren.</span><span class="sxs-lookup"><span data-stu-id="2ee88-140">hello configuration checklist describes hello information that you need toocollect before you configure hello software on your StorSimple Virtual Array.</span></span> <span data-ttu-id="2ee88-141">Deze informatie tevoren tijd helpt voorbereiden stroomlijnen Hallo proces voor het implementeren van Hallo StorSimple-apparaat in uw omgeving.</span><span class="sxs-lookup"><span data-stu-id="2ee88-141">Preparing this information ahead of time helps streamline hello process of deploying hello StorSimple device in your environment.</span></span> <span data-ttu-id="2ee88-142">Afhankelijk van het feit of uw virtuele StorSimple-matrix is geïmplementeerd als een bestandsserver of een iSCSI-server, moet u een van de volgende controlelijsten Hallo.</span><span class="sxs-lookup"><span data-stu-id="2ee88-142">Depending upon whether your StorSimple Virtual Array is deployed as a file server or an iSCSI server, you need one of hello following checklists.</span></span>

* <span data-ttu-id="2ee88-143">Hallo downloaden [StorSimple virtuele matrix bestand Server Configuratiecontrolelijst](http://download.microsoft.com/download/E/E/6/EE690BB0-B442-4B84-8165-4731EE727ACF/MicrosoftAzureStorSimpleVirtualArrayFileServerConfigurationChecklist.pdf).</span><span class="sxs-lookup"><span data-stu-id="2ee88-143">Download hello [StorSimple Virtual Array File Server Configuration Checklist](http://download.microsoft.com/download/E/E/6/EE690BB0-B442-4B84-8165-4731EE727ACF/MicrosoftAzureStorSimpleVirtualArrayFileServerConfigurationChecklist.pdf).</span></span>
* <span data-ttu-id="2ee88-144">Hallo downloaden [virtuele StorSimple-matrix iSCSI Server Configuratiecontrolelijst](http://download.microsoft.com/download/E/E/6/EE690BB0-B442-4B84-8165-4731EE727ACF/MicrosoftAzureStorSimpleVirtualArrayiSCSIServerConfigurationChecklist.pdf).</span><span class="sxs-lookup"><span data-stu-id="2ee88-144">Download hello [StorSimple Virtual Array iSCSI Server Configuration Checklist](http://download.microsoft.com/download/E/E/6/EE690BB0-B442-4B84-8165-4731EE727ACF/MicrosoftAzureStorSimpleVirtualArrayiSCSIServerConfigurationChecklist.pdf).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2ee88-145">Vereisten</span><span class="sxs-lookup"><span data-stu-id="2ee88-145">Prerequisites</span></span>

<span data-ttu-id="2ee88-146">U vindt hier Hallo configuratievereisten voor uw StorSimple-apparaat Manager-service, uw virtuele StorSimple-matrix en Hallo datacenternetwerk.</span><span class="sxs-lookup"><span data-stu-id="2ee88-146">Here you find hello configuration prerequisites for your StorSimple Device Manager service, your StorSimple Virtual Array, and hello datacenter network.</span></span>

### <a name="for-hello-storsimple-device-manager-service"></a><span data-ttu-id="2ee88-147">Voor Hallo StorSimple-apparaat Manager-service</span><span class="sxs-lookup"><span data-stu-id="2ee88-147">For hello StorSimple Device Manager service</span></span>

<span data-ttu-id="2ee88-148">Zorg voordat u begint voor het volgende:</span><span class="sxs-lookup"><span data-stu-id="2ee88-148">Before you begin, make sure that:</span></span>

* <span data-ttu-id="2ee88-149">U hebt een Microsoft-account met toegangsreferenties.</span><span class="sxs-lookup"><span data-stu-id="2ee88-149">You have your Microsoft account with access credentials.</span></span>
* <span data-ttu-id="2ee88-150">U hebt een Microsoft Azure Storage-account met toegangsreferenties.</span><span class="sxs-lookup"><span data-stu-id="2ee88-150">You have your Microsoft Azure storage account with access credentials.</span></span>
* <span data-ttu-id="2ee88-151">Uw Microsoft Azure-abonnement moet worden ingeschakeld voor Apparaatbeheer van StorSimple-service.</span><span class="sxs-lookup"><span data-stu-id="2ee88-151">Your Microsoft Azure subscription should be enabled for StorSimple Device Manager service.</span></span>

### <a name="for-hello-storsimple-virtual-array"></a><span data-ttu-id="2ee88-152">Hallo voor virtuele StorSimple-matrix</span><span class="sxs-lookup"><span data-stu-id="2ee88-152">For hello StorSimple Virtual Array</span></span>

<span data-ttu-id="2ee88-153">Voordat u een virtuele-matrix implementeert, zorg ervoor dat:</span><span class="sxs-lookup"><span data-stu-id="2ee88-153">Before you deploy a virtual array, make sure that:</span></span>

* <span data-ttu-id="2ee88-154">U hebt toegang tot tooa-hostsysteem met Hyper-V in Windows Server 2008 R2 of later of VMware (ESXi 5.5 of hoger) die kan worden gebruikt tooa inrichten van een apparaat.</span><span class="sxs-lookup"><span data-stu-id="2ee88-154">You have access tooa host system running Hyper-V on Windows Server 2008 R2 or later or VMware (ESXi 5.5 or later) that can be used tooa provision a device.</span></span>
* <span data-ttu-id="2ee88-155">Hallo-hostsysteem is kunnen toodedicate Hallo na tooprovision resources van uw virtuele matrix:</span><span class="sxs-lookup"><span data-stu-id="2ee88-155">hello host system is able toodedicate hello following resources tooprovision your virtual array:</span></span>
  
  * <span data-ttu-id="2ee88-156">Een minimum van 4 kernen.</span><span class="sxs-lookup"><span data-stu-id="2ee88-156">A minimum of 4 cores.</span></span>
  * <span data-ttu-id="2ee88-157">Ten minste 8 GB aan RAM-geheugen.</span><span class="sxs-lookup"><span data-stu-id="2ee88-157">At least 8 GB of RAM.</span></span> <span data-ttu-id="2ee88-158">Als u van plan tooconfigure Hallo virtuele matrix als bestandsserver bent, ondersteunt 8 GB 2 miljoen bestanden.</span><span class="sxs-lookup"><span data-stu-id="2ee88-158">If you plan tooconfigure hello virtual array as file server, 8 GB supports 2 million files.</span></span> <span data-ttu-id="2ee88-159">U moet 16 GB RAM-geheugen toosupport 2-4 miljoen bestanden.</span><span class="sxs-lookup"><span data-stu-id="2ee88-159">You need 16 GB RAM toosupport 2 - 4 million files.</span></span>
  * <span data-ttu-id="2ee88-160">Één netwerkinterface.</span><span class="sxs-lookup"><span data-stu-id="2ee88-160">One network interface.</span></span>
  * <span data-ttu-id="2ee88-161">500 GB virtuele schijf voor systeemgegevens.</span><span class="sxs-lookup"><span data-stu-id="2ee88-161">A 500 GB virtual disk for system data.</span></span>

### <a name="for-hello-datacenter-network"></a><span data-ttu-id="2ee88-162">Voor het datacenternetwerk Hallo</span><span class="sxs-lookup"><span data-stu-id="2ee88-162">For hello datacenter network</span></span>

<span data-ttu-id="2ee88-163">Zorg voordat u begint voor het volgende:</span><span class="sxs-lookup"><span data-stu-id="2ee88-163">Before you begin, make sure that:</span></span>

* <span data-ttu-id="2ee88-164">Hallo-netwerk in uw datacenter is geconfigureerd volgens Hallo netwerkvereisten voor uw StorSimple-apparaat.</span><span class="sxs-lookup"><span data-stu-id="2ee88-164">hello network in your datacenter is configured as per hello networking requirements for your StorSimple device.</span></span> <span data-ttu-id="2ee88-165">Zie voor meer informatie, Hallo [StorSimple virtuele matrix systeemvereisten](storsimple-ova-system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="2ee88-165">For more information, see hello [StorSimple Virtual Array System Requirements](storsimple-ova-system-requirements.md).</span></span>
* <span data-ttu-id="2ee88-166">Uw virtuele StorSimple-matrix heeft een speciale 5 Mbps internetbandbreedte (of meer) beschikbaar te allen tijde.</span><span class="sxs-lookup"><span data-stu-id="2ee88-166">Your StorSimple Virtual Array has a dedicated 5 Mbps Internet bandwidth (or more) available at all times.</span></span> <span data-ttu-id="2ee88-167">Deze bandbreedte mag niet worden gedeeld met andere toepassingen.</span><span class="sxs-lookup"><span data-stu-id="2ee88-167">This bandwidth should not be shared with any other applications.</span></span>

## <a name="step-by-step-preparation"></a><span data-ttu-id="2ee88-168">Stapsgewijze voorbereiding</span><span class="sxs-lookup"><span data-stu-id="2ee88-168">Step-by-step preparation</span></span>

<span data-ttu-id="2ee88-169">Hallo volgen Stapsgewijze instructies tooprepare uw portal voor Hallo StorSimple-apparaat Manager-service gebruiken.</span><span class="sxs-lookup"><span data-stu-id="2ee88-169">Use hello following step-by-step instructions tooprepare your portal for hello StorSimple Device Manager service.</span></span>

## <a name="step-1-create-a-new-service"></a><span data-ttu-id="2ee88-170">Stap 1: een nieuwe service maken</span><span class="sxs-lookup"><span data-stu-id="2ee88-170">Step 1: Create a new service</span></span>

<span data-ttu-id="2ee88-171">Slechts één exemplaar van Hallo Apparaatbeheer StorSimple-service kan meerdere virtuele StorSimple-matrices beheren.</span><span class="sxs-lookup"><span data-stu-id="2ee88-171">A single instance of hello StorSimple Device Manager service can manage multiple StorSimple Virtual Arrays.</span></span> <span data-ttu-id="2ee88-172">Hallo te volgen stappen toocreate een exemplaar van Hallo Apparaatbeheer StorSimple-service uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="2ee88-172">Perform hello following steps toocreate an instance of hello StorSimple Device Manager service.</span></span> <span data-ttu-id="2ee88-173">Als u een bestaande toomanage voor Apparaatbeheer van StorSimple-service op uw virtuele matrices hebt, deze stap overslaan en ga te[stap 2: Get Hallo serviceregistratiesleutel](#step-2-get-the-service-registration-key).</span><span class="sxs-lookup"><span data-stu-id="2ee88-173">If you have an existing StorSimple Device Manager service toomanage your virtual arrays, skip this step and go too[Step 2: Get hello service registration key](#step-2-get-the-service-registration-key).</span></span>

[!INCLUDE [storsimple-virtual-array-create-new-service](../../includes/storsimple-virtual-array-create-new-service.md)]

> [!IMPORTANT]
> <span data-ttu-id="2ee88-174">Als u met uw service niet Hallo automatisch maken van een opslagaccount hebt ingeschakeld, moet u toocreate ten minste één opslagaccount nadat u een service hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="2ee88-174">If you did not enable hello automatic creation of a storage account with your service, you will need toocreate at least one storage account after you have successfully created a service.</span></span>
> 
> * <span data-ttu-id="2ee88-175">Als u een opslagaccount niet automatisch gemaakt, gaat u verder te[configureren van een nieuw opslagaccount voor Hallo service](#optional-step-configure-a-new-storage-account-for-the-service) voor gedetailleerde instructies.</span><span class="sxs-lookup"><span data-stu-id="2ee88-175">If you did not create a storage account automatically, go too[Configure a new storage account for hello service](#optional-step-configure-a-new-storage-account-for-the-service) for detailed instructions.</span></span>
> * <span data-ttu-id="2ee88-176">Als u Hallo automatisch maken van een opslagaccount hebt ingeschakeld, gaat u verder te[stap 2: Get Hallo serviceregistratiesleutel](#step-2-get-the-service-registration-key).</span><span class="sxs-lookup"><span data-stu-id="2ee88-176">If you enabled hello automatic creation of a storage account, go too[Step 2: Get hello service registration key](#step-2-get-the-service-registration-key).</span></span>
> 
> 

## <a name="step-2-get-hello-service-registration-key"></a><span data-ttu-id="2ee88-177">Stap 2: Hallo serviceregistratiesleutel ophalen</span><span class="sxs-lookup"><span data-stu-id="2ee88-177">Step 2: Get hello service registration key</span></span>

<span data-ttu-id="2ee88-178">Nadat de Hallo StorSimple-apparaat Manager-service actief is, moet u tooget hello serviceregistratiesleutel.</span><span class="sxs-lookup"><span data-stu-id="2ee88-178">After hello StorSimple Device Manager service is up and running, you will need tooget hello service registration key.</span></span> <span data-ttu-id="2ee88-179">Deze sleutel is gebruikte tooregister en verbinding maken met uw StorSimple-apparaat met Hallo-service.</span><span class="sxs-lookup"><span data-stu-id="2ee88-179">This key is used tooregister and connect your StorSimple device with hello service.</span></span>

<span data-ttu-id="2ee88-180">Uitvoeren van de stappen te volgen in Hallo Hallo [Azure-portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="2ee88-180">Perform hello following steps in hello [Azure portal](https://portal.azure.com/).</span></span>

[!INCLUDE [storsimple-virtual-array-get-service-registration-key](../../includes/storsimple-virtual-array-get-service-registration-key.md)]

> [!NOTE]
> <span data-ttu-id="2ee88-181">Hallo serviceregistratiesleutel is gebruikte tooregister alle Hallo Apparaatbeheer StorSimple-apparaten die tooregister met uw StorSimple-apparaat Manager-service moeten.</span><span class="sxs-lookup"><span data-stu-id="2ee88-181">hello service registration key is used tooregister all hello StorSimple Device Manager devices that need tooregister with your StorSimple Device Manager service.</span></span>
> 
> 

## <a name="step-3-download-hello-virtual-array-image"></a><span data-ttu-id="2ee88-182">Stap 3: Hallo virtuele matrix installatiekopie downloaden</span><span class="sxs-lookup"><span data-stu-id="2ee88-182">Step 3: Download hello virtual array image</span></span>

<span data-ttu-id="2ee88-183">Nadat u de serviceregistratiesleutel Hallo hebt, moet u op uw hostsysteem toodownload Hallo juiste virtuele matrix installatiekopie tooprovision een virtuele-matrix.</span><span class="sxs-lookup"><span data-stu-id="2ee88-183">After you have hello service registration key, you will need toodownload hello appropriate virtual array image tooprovision a virtual array on your host system.</span></span> <span data-ttu-id="2ee88-184">Hallo virtuele matrix afbeeldingen zijn specifiek besturingssysteem en kunnen worden gedownload vanaf Hallo pagina snel starten in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="2ee88-184">hello virtual array images are operating system specific and can be downloaded from hello Quick Start page in hello Azure portal.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2ee88-185">Hallo software die wordt uitgevoerd op Hallo virtuele StorSimple-matrix kan alleen worden gebruikt met Hallo StorSimple-apparaat Manager-service.</span><span class="sxs-lookup"><span data-stu-id="2ee88-185">hello software running on hello StorSimple Virtual Array may only be used with hello StorSimple Device Manager service.</span></span>
> 
> 

<span data-ttu-id="2ee88-186">Uitvoeren van de stappen te volgen in Hallo Hallo [Azure-portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="2ee88-186">Perform hello following steps in hello [Azure portal](https://portal.azure.com/).</span></span>

#### <a name="tooget-hello-virtual-array-image"></a><span data-ttu-id="2ee88-187">tooget hello virtuele matrix installatiekopie</span><span class="sxs-lookup"><span data-stu-id="2ee88-187">tooget hello virtual array image</span></span>

1. <span data-ttu-id="2ee88-188">Meld u aan bij Hallo [Azure-portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="2ee88-188">Sign into hello [Azure portal](https://portal.azure.com/).</span></span> 
2. <span data-ttu-id="2ee88-189">Klik in hello Azure-portal, op **Bladeren > Managers voor apparaatregistratie StorSimple**.</span><span class="sxs-lookup"><span data-stu-id="2ee88-189">In hello Azure portal, click **Browse > StorSimple Device Managers**.</span></span>
3. <span data-ttu-id="2ee88-190">Selecteer een bestaande Apparaatbeheer StorSimple-service.</span><span class="sxs-lookup"><span data-stu-id="2ee88-190">Select an existing StorSimple Device Manager service.</span></span> <span data-ttu-id="2ee88-191">In Hallo **StorSimple Apparaatbeheer** blade, klikt u op **Quick Start**.</span><span class="sxs-lookup"><span data-stu-id="2ee88-191">In hello **StorSimple Device Manager** blade, click **Quick Start**.</span></span> 
4. <span data-ttu-id="2ee88-192">Klik op Hallo koppeling bijbehorende toohello afbeelding die u wilt dat toodownload van Hallo Microsoft Download Center.</span><span class="sxs-lookup"><span data-stu-id="2ee88-192">Click hello link corresponding toohello image that you want toodownload from hello Microsoft Download Center.</span></span> <span data-ttu-id="2ee88-193">Hallo-installatiekopiebestanden zijn ongeveer 4,8 GB.</span><span class="sxs-lookup"><span data-stu-id="2ee88-193">hello image files are approximately 4.8 GB.</span></span>
   
   * <span data-ttu-id="2ee88-194">VHDX voor Hyper-V op Windows Server 2012 en hoger</span><span class="sxs-lookup"><span data-stu-id="2ee88-194">VHDX for Hyper-V on Windows Server 2012 and later</span></span>
   * <span data-ttu-id="2ee88-195">VHD voor Hyper-V in Windows Server 2008 R2 en hoger</span><span class="sxs-lookup"><span data-stu-id="2ee88-195">VHD for Hyper-V on Windows Server 2008 R2 and later</span></span>
   * <span data-ttu-id="2ee88-196">VMDK voor VMWare ESXi 5.5 en hoger</span><span class="sxs-lookup"><span data-stu-id="2ee88-196">VMDK for VMWare ESXi 5.5 and later</span></span>
5. <span data-ttu-id="2ee88-197">Download en pak Hallo bestand tooa lokale schijf, waardoor een notitie van waarin de uitgepakte bestand Hallo zich bevindt.</span><span class="sxs-lookup"><span data-stu-id="2ee88-197">Download and unzip hello file tooa local drive, making a note of where hello unzipped file is located.</span></span>

## <a name="optional-step-configure-a-new-storage-account-for-hello-service"></a><span data-ttu-id="2ee88-198">Optionele stap: een nieuw opslagaccount voor Hallo service configureren</span><span class="sxs-lookup"><span data-stu-id="2ee88-198">Optional step: Configure a new storage account for hello service</span></span>

<span data-ttu-id="2ee88-199">Deze stap is optioneel en moet worden uitgevoerd alleen als u niet Hallo automatisch maken van een opslagaccount met uw service hebt ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="2ee88-199">This step is optional and should be performed only if you did not enable hello automatic creation of a storage account with your service.</span></span>

<span data-ttu-id="2ee88-200">Als u een Azure storage-account in een andere regio toocreate nodig hebt, raadpleegt u [hoe toocreate een opslagaccount](../storage/common/storage-create-storage-account.md#create-a-storage-account) voor stapsgewijze instructies.</span><span class="sxs-lookup"><span data-stu-id="2ee88-200">If you need toocreate an Azure storage account in a different region, see [How toocreate a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) for step-by-step instructions.</span></span>

<span data-ttu-id="2ee88-201">Uitvoeren van de stappen te volgen in Hallo Hallo [Azure-portal](https://ms.portal.azure.com/) op Hallo StorSimple Apparaatbeheer service pagina tooadd een bestaand Microsoft Azure-opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="2ee88-201">Perform hello following steps in hello [Azure portal](https://ms.portal.azure.com/) on hello StorSimple Device Manager service page tooadd an existing Microsoft Azure storage account.</span></span>

#### <a name="tooadd-a-storage-account-credential-that-has-hello-same-azure-subscription-as-hello-device-manager-service"></a><span data-ttu-id="2ee88-202">een storage account referentie tooadd Hallo hetzelfde Azure-abonnement als Hallo Apparaatbeheer service</span><span class="sxs-lookup"><span data-stu-id="2ee88-202">tooadd a storage account credential that has hello same Azure subscription as hello Device Manager service</span></span>

1. <span data-ttu-id="2ee88-203">Ga tooyour Apparaatbeheer, selecteer service en dubbelklik erop.</span><span class="sxs-lookup"><span data-stu-id="2ee88-203">Navigate tooyour Device Manager service, select and double-click it.</span></span> <span data-ttu-id="2ee88-204">Hiermee opent u Hallo **overzicht** blade.</span><span class="sxs-lookup"><span data-stu-id="2ee88-204">This opens hello **Overview** blade.</span></span>
2. <span data-ttu-id="2ee88-205">Selecteer **opslagaccountreferenties** binnen Hallo **configuratie** sectie.</span><span class="sxs-lookup"><span data-stu-id="2ee88-205">Select **Storage account credentials** within hello **Configuration** section.</span></span>
3. <span data-ttu-id="2ee88-206">Klik op **Add**.</span><span class="sxs-lookup"><span data-stu-id="2ee88-206">Click **Add**.</span></span>
4. <span data-ttu-id="2ee88-207">In Hallo **een opslagaccount toevoegen** blade Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="2ee88-207">In hello **Add a storage account** blade, do hello following:</span></span>
   
    1. <span data-ttu-id="2ee88-208">Voor **abonnement**, selecteer **huidige**.</span><span class="sxs-lookup"><span data-stu-id="2ee88-208">For **Subscription**, select **Current**.</span></span>
   
    2. <span data-ttu-id="2ee88-209">Hallo-naam van uw Azure storage-account opgeven.</span><span class="sxs-lookup"><span data-stu-id="2ee88-209">Provide hello name of your Azure storage account.</span></span>
   
    3. <span data-ttu-id="2ee88-210">Selecteer **inschakelen** toocreate een beveiligd kanaal voor netwerkcommunicatie tussen uw StorSimple-apparaat en het Hallo-cloud.</span><span class="sxs-lookup"><span data-stu-id="2ee88-210">Select **Enable** toocreate a secure channel for network communication between your StorSimple device and hello cloud.</span></span> <span data-ttu-id="2ee88-211">Selecteer **uitschakelen** alleen als u in een privécloud werkt.</span><span class="sxs-lookup"><span data-stu-id="2ee88-211">Select **Disable** only if you are operating within a private cloud.</span></span>
   
    4. <span data-ttu-id="2ee88-212">Klik op **Add**.</span><span class="sxs-lookup"><span data-stu-id="2ee88-212">Click **Add**.</span></span> <span data-ttu-id="2ee88-213">U wordt gewaarschuwd nadat Hallo storage-account is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="2ee88-213">You are notified after hello storage account is successfully created.</span></span><br></br>
   
     ![Een bestaande referentie voor de storage-account toevoegen](./media/storsimple-virtual-array-manage-storage-accounts/ova-add-storageacct.png)

## <a name="next-step"></a><span data-ttu-id="2ee88-215">Volgende stap</span><span class="sxs-lookup"><span data-stu-id="2ee88-215">Next step</span></span>

<span data-ttu-id="2ee88-216">de volgende stap Hallo is tooprovision een virtuele machine voor uw virtuele StorSimple-matrix.</span><span class="sxs-lookup"><span data-stu-id="2ee88-216">hello next step is tooprovision a virtual machine for your StorSimple Virtual Array.</span></span> <span data-ttu-id="2ee88-217">Zie het volgende, afhankelijk van uw hostbesturingssysteem Hallo gedetailleerde instructies in:</span><span class="sxs-lookup"><span data-stu-id="2ee88-217">Depending on your host operating system, see hello detailed instructions in:</span></span>

* [<span data-ttu-id="2ee88-218">Inrichten van een virtueel StorSimple-matrix in Hyper-V</span><span class="sxs-lookup"><span data-stu-id="2ee88-218">Provision a StorSimple Virtual Array in Hyper-V</span></span>](storsimple-virtual-array-deploy2-provision-hyperv.md)
* [<span data-ttu-id="2ee88-219">Een virtueel StorSimple-matrix in VMware inrichten</span><span class="sxs-lookup"><span data-stu-id="2ee88-219">Provision a StorSimple Virtual Array in VMware</span></span>](storsimple-virtual-array-deploy2-provision-vmware.md)


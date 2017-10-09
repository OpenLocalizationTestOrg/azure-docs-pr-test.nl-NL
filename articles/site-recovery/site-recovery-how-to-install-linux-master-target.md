---
title: aaaHow tooinstall een Linux-hoofddoel-server voor failover van Azure tooon-premises | Microsoft Docs
description: Voordat een virtuele Linux-machine opnieuw te beveiligen, moet u een Linux-hoofddoelserver. Meer informatie over hoe tooinstall een.
services: site-recovery
documentationcenter: 
author: ruturaj
manager: gauravd
editor: 
ms.assetid: 44813a48-c680-4581-a92e-cecc57cc3b1e
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 08/11/2017
ms.author: ruturajd
ms.openlocfilehash: d7c55d115712b9862414979f89efb1f177c5f0dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="install-a-linux-master-target-server"></a><span data-ttu-id="613cb-104">Een Linux-hoofddoel-server installeren</span><span class="sxs-lookup"><span data-stu-id="613cb-104">Install a Linux master target server</span></span>
<span data-ttu-id="613cb-105">Nadat u uw virtuele machines failover, kunt u back-Hallo virtuele machines toohello lokale site kan mislukken.</span><span class="sxs-lookup"><span data-stu-id="613cb-105">After you fail over your virtual machines, you can fail back hello virtual machines toohello on-premises site.</span></span> <span data-ttu-id="613cb-106">terug toofail, moet u tooreprotect Hallo virtuele machine van Azure toohello lokale site.</span><span class="sxs-lookup"><span data-stu-id="613cb-106">toofail back, you need tooreprotect hello virtual machine from Azure toohello on-premises site.</span></span> <span data-ttu-id="613cb-107">U moet een lokale hoofddoel tooreceive Hallo verkeer van een server voor dit proces.</span><span class="sxs-lookup"><span data-stu-id="613cb-107">For this process, you need an on-premises master target server tooreceive hello traffic.</span></span> 

<span data-ttu-id="613cb-108">Als de beveiligde virtuele machine een virtuele Windows-computer is, moet u een Windows-hoofddoel.</span><span class="sxs-lookup"><span data-stu-id="613cb-108">If your protected virtual machine is a Windows virtual machine, then you need a Windows master target.</span></span> <span data-ttu-id="613cb-109">Voor een virtuele Linux-machine moet u een Linux-hoofddoel.</span><span class="sxs-lookup"><span data-stu-id="613cb-109">For a Linux virtual machine, you need a Linux master target.</span></span> <span data-ttu-id="613cb-110">Lees Hallo volgende stappen uit toolearn hoe toocreate en installeer een Linux-doel master.</span><span class="sxs-lookup"><span data-stu-id="613cb-110">Read hello following steps toolearn how toocreate and install a Linux master target.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="613cb-111">Vanaf versie van de hoofddoelserver hello 9.10.0, Hallo nieuwste hoofddoelserver kan worden alleen geïnstalleerd op een server Ubuntu 16.04.</span><span class="sxs-lookup"><span data-stu-id="613cb-111">Starting with release of hello 9.10.0 master target server, hello latest master target server can be only installed on an Ubuntu 16.04 server.</span></span> <span data-ttu-id="613cb-112">Nieuwe installaties zijn niet toegestaan voor CentOS6.6 servers.</span><span class="sxs-lookup"><span data-stu-id="613cb-112">New installations aren't allowed on  CentOS6.6 servers.</span></span> <span data-ttu-id="613cb-113">U kunt echter doorgaan tooupgrade uw oude hoofdsleutel doelservers met Hallo 9.10.0 versie.</span><span class="sxs-lookup"><span data-stu-id="613cb-113">However, you can continue tooupgrade your old master target servers by using hello 9.10.0 version.</span></span>

## <a name="overview"></a><span data-ttu-id="613cb-114">Overzicht</span><span class="sxs-lookup"><span data-stu-id="613cb-114">Overview</span></span>
<span data-ttu-id="613cb-115">In dit artikel bevat instructies voor hoe tooinstall een Linux-doel master.</span><span class="sxs-lookup"><span data-stu-id="613cb-115">This article provides instructions for how tooinstall a Linux master target.</span></span>

<span data-ttu-id="613cb-116">Opmerkingen of vragen plaatsen aan Hallo einde van dit artikel of op Hallo [Azure Recovery Services-Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="613cb-116">Post comments or questions at hello end of this article or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="613cb-117">Vereisten</span><span class="sxs-lookup"><span data-stu-id="613cb-117">Prerequisites</span></span>

* <span data-ttu-id="613cb-118">toochoose hello host op welke Hallo hoofddoel van toodeploy, bepalen als Hallo failback toobe tooan bestaande on-premises virtuele machine of tooa nieuwe virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="613cb-118">toochoose hello host on which toodeploy hello master target, determine if hello failback is going toobe tooan existing on-premises virtual machine or tooa new virtual machine.</span></span> 
    * <span data-ttu-id="613cb-119">Voor een bestaande virtuele machine hebben host van het hoofddoel Hallo Hallo toegang toohello gegevensarchieven van Hallo virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="613cb-119">For an existing virtual machine, hello host of hello master target should have access toohello data stores of hello virtual machine.</span></span>
    * <span data-ttu-id="613cb-120">Als Hallo on-premises virtuele machine niet bestaat, wordt op dezelfde als hoofddoel Hallo host Hallo Hallo failback van virtuele machine gemaakt.</span><span class="sxs-lookup"><span data-stu-id="613cb-120">If hello on-premises virtual machine does not exist, hello failback virtual machine is created on hello same host as hello master target.</span></span> <span data-ttu-id="613cb-121">U kunt een willekeurige host ESXi tooinstall Hallo hoofddoel.</span><span class="sxs-lookup"><span data-stu-id="613cb-121">You can choose any ESXi host tooinstall hello master target.</span></span>
* <span data-ttu-id="613cb-122">Hallo hoofddoel moet zich op een netwerk dat met de Hallo processerver en de configuratieserver Hallo communiceren kan.</span><span class="sxs-lookup"><span data-stu-id="613cb-122">hello master target should be on a network that can communicate with hello process server and hello configuration server.</span></span>
* <span data-ttu-id="613cb-123">Hallo-versie van het hoofddoel Hallo moet gelijk tooor ouder is dan het Hallo-versies van Hallo processerver en de configuratieserver Hallo.</span><span class="sxs-lookup"><span data-stu-id="613cb-123">hello version of hello master target must be equal tooor earlier than hello versions of hello process server and hello configuration server.</span></span> <span data-ttu-id="613cb-124">Bijvoorbeeld, als Hallo-versie van de configuratieserver Hallo 9.4, kan Hallo-versie van het hoofddoel Hallo worden 9.4 of 9.3 maar niet 9.5.</span><span class="sxs-lookup"><span data-stu-id="613cb-124">For example, if hello version of hello configuration server is 9.4, hello version of hello master target can be 9.4 or 9.3 but not 9.5.</span></span>
* <span data-ttu-id="613cb-125">Hallo hoofddoel kan alleen worden een virtuele VMware-machine en niet op een fysieke server.</span><span class="sxs-lookup"><span data-stu-id="613cb-125">hello master target can only be a VMware virtual machine and not a physical server.</span></span>

## <a name="create-hello-master-target-according-toohello-sizing-guidelines"></a><span data-ttu-id="613cb-126">Hallo hoofddoel volgens toohello sizing richtlijnen maken</span><span class="sxs-lookup"><span data-stu-id="613cb-126">Create hello master target according toohello sizing guidelines</span></span>

<span data-ttu-id="613cb-127">Maak Hallo hoofddoel in overeenstemming met Hallo sizing richtlijnen te volgen:</span><span class="sxs-lookup"><span data-stu-id="613cb-127">Create hello master target in accordance with hello following sizing guidelines:</span></span>
- <span data-ttu-id="613cb-128">**RAM-geheugen**: 6 GB of meer</span><span class="sxs-lookup"><span data-stu-id="613cb-128">**RAM**: 6 GB or more</span></span>
- <span data-ttu-id="613cb-129">**OS-schijfgrootte**: 100 GB of meer (tooinstall CentOS6.6)</span><span class="sxs-lookup"><span data-stu-id="613cb-129">**OS disk size**: 100 GB or more (tooinstall CentOS6.6)</span></span>
- <span data-ttu-id="613cb-130">**Aanvullende schijfgrootte voor bewaarstation**: 1 TB</span><span class="sxs-lookup"><span data-stu-id="613cb-130">**Additional disk size for retention drive**: 1 TB</span></span>
- <span data-ttu-id="613cb-131">**CPU-kernen**: 4 kernen of meer</span><span class="sxs-lookup"><span data-stu-id="613cb-131">**CPU cores**: 4 cores or more</span></span>

<span data-ttu-id="613cb-132">Hallo volgende ondersteund Ubuntu kernels worden ondersteund.</span><span class="sxs-lookup"><span data-stu-id="613cb-132">hello following supported Ubuntu kernels are supported.</span></span>


|<span data-ttu-id="613cb-133">Kernel-reeks</span><span class="sxs-lookup"><span data-stu-id="613cb-133">Kernel Series</span></span>  |<span data-ttu-id="613cb-134">Ondersteuning voor maximaal te</span><span class="sxs-lookup"><span data-stu-id="613cb-134">Support up too</span></span> |
|---------|---------|
|<span data-ttu-id="613cb-135">4.4</span><span class="sxs-lookup"><span data-stu-id="613cb-135">4.4</span></span>      |<span data-ttu-id="613cb-136">4.4.0-81-Generic</span><span class="sxs-lookup"><span data-stu-id="613cb-136">4.4.0-81-generic</span></span>         |
|<span data-ttu-id="613cb-137">4.8</span><span class="sxs-lookup"><span data-stu-id="613cb-137">4.8</span></span>      |<span data-ttu-id="613cb-138">4.8.0-56-Generic</span><span class="sxs-lookup"><span data-stu-id="613cb-138">4.8.0-56-generic</span></span>         |
|<span data-ttu-id="613cb-139">4.10</span><span class="sxs-lookup"><span data-stu-id="613cb-139">4.10</span></span>     |<span data-ttu-id="613cb-140">4.10.0-24-Generic</span><span class="sxs-lookup"><span data-stu-id="613cb-140">4.10.0-24-generic</span></span>        |


## <a name="deploy-hello-master-target-server"></a><span data-ttu-id="613cb-141">De hoofddoelserver Hallo implementeren</span><span class="sxs-lookup"><span data-stu-id="613cb-141">Deploy hello master target server</span></span>

### <a name="install-ubuntu-16042-minimal"></a><span data-ttu-id="613cb-142">Ubuntu 16.04.2 installeren minimale</span><span class="sxs-lookup"><span data-stu-id="613cb-142">Install Ubuntu 16.04.2 Minimal</span></span>

<span data-ttu-id="613cb-143">Hallo Hallo stappen tooinstall Hallo Ubuntu 16.04.2 64-bits-besturingssysteem te volgen in beslag nemen.</span><span class="sxs-lookup"><span data-stu-id="613cb-143">Take hello following hello steps tooinstall hello Ubuntu 16.04.2 64-bit operating system.</span></span>

<span data-ttu-id="613cb-144">**Stap 1:** gaat toohello [downloadkoppeling](https://www.ubuntu.com/download/server/thank-you?version=16.04.2&architecture=amd64) en kies de dichtstbijzijnde mirror Hallo van waarmee Ubuntu 16.04.2 minimaal 64-bits ISO downloaden.</span><span class="sxs-lookup"><span data-stu-id="613cb-144">**Step 1:** Go toohello [download link](https://www.ubuntu.com/download/server/thank-you?version=16.04.2&architecture=amd64) and choose hello closest mirror from which download an Ubuntu 16.04.2 minimal 64-bit ISO.</span></span>

<span data-ttu-id="613cb-145">Houd een Ubuntu 16.04.2 minimaal 64-bits ISO Hallo DVD-station en start Hallo systeem.</span><span class="sxs-lookup"><span data-stu-id="613cb-145">Keep an Ubuntu 16.04.2 minimal 64-bit ISO in hello DVD drive and start hello system.</span></span>

<span data-ttu-id="613cb-146">**Stap 2:** Selecteer **Engels** als uw voorkeurstaal en selecteer vervolgens **Enter**.</span><span class="sxs-lookup"><span data-stu-id="613cb-146">**Step 2:** Select **English** as your preferred language, and then select **Enter**.</span></span>

![Een taal selecteren](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image1.png)

<span data-ttu-id="613cb-148">**Stap 3:** Selecteer **Ubuntu Server installeren**, en selecteer vervolgens **Enter**.</span><span class="sxs-lookup"><span data-stu-id="613cb-148">**Step 3:** Select **Install Ubuntu Server**, and then select **Enter**.</span></span>

![Selecteer installeren Ubuntu Server](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image2.png)

<span data-ttu-id="613cb-150">**Stap 4:** Selecteer **Engels** als uw voorkeurstaal en selecteer vervolgens **Enter**.</span><span class="sxs-lookup"><span data-stu-id="613cb-150">**Step 4:** Select **English** as your preferred language, and then select **Enter**.</span></span>

![Engels als uw voorkeurstaal selecteren](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image3.png)

<span data-ttu-id="613cb-152">**Stap 5:** Selecteer optie van Hallo Hallo **tijdzone** optielijst en selecteer vervolgens **Enter**.</span><span class="sxs-lookup"><span data-stu-id="613cb-152">**Step 5:** Select hello appropriate option from hello **Time Zone** options list, and then select **Enter**.</span></span>

![Selecteer de juiste tijdzone Hallo](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image4.png)

<span data-ttu-id="613cb-154">**Stap 6:** Selecteer **Nee** (hello standaardoptie), en selecteer vervolgens **Enter**.</span><span class="sxs-lookup"><span data-stu-id="613cb-154">**Step 6:** Select **No** (hello default option), and then select **Enter**.</span></span>


![Hallo toetsenbord configureren](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image5.png)

<span data-ttu-id="613cb-156">**Stap 7:** Selecteer **Engels (V.S.)** als Hallo land van oorsprong voor Hallo toetsenbord en selecteert u vervolgens **Enter**.</span><span class="sxs-lookup"><span data-stu-id="613cb-156">**Step 7:** Select **English (US)** as hello country of origin for hello keyboard, and then select **Enter**.</span></span>

![VS als Hallo land van oorsprong selecteren](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image6.png)

<span data-ttu-id="613cb-158">**Stap 8:** Selecteer **Engels (V.S.)** als Hallo toetsenbordindeling en selecteer vervolgens **Enter**.</span><span class="sxs-lookup"><span data-stu-id="613cb-158">**Step 8:** Select **English (US)** as hello keyboard layout, and then select **Enter**.</span></span>

![Selecteer Amerikaans Engels als Hallo toetsenbordindeling](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image7.png)

<span data-ttu-id="613cb-160">**Stap 9:** Voer Hallo-hostnaam voor uw server in Hallo **hostnaam** vak en selecteer vervolgens **doorgaan**.</span><span class="sxs-lookup"><span data-stu-id="613cb-160">**Step 9:** Enter hello hostname for your server in hello **Hostname** box, and then select **Continue**.</span></span>

![Voer Hallo-hostnaam voor de server](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image8.png)

<span data-ttu-id="613cb-162">**Stap 10:** toocreate een gebruikersaccount, voer de naam van de gebruiker Hallo en selecteer vervolgens **doorgaan**.</span><span class="sxs-lookup"><span data-stu-id="613cb-162">**Step 10:** toocreate a user account, enter hello user name, and then select **Continue**.</span></span>

![Een gebruikersaccount maken](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image9.png)

<span data-ttu-id="613cb-164">**Stap 11:** Hallo wachtwoord invoeren voor het nieuwe gebruikersaccount Hallo en selecteer vervolgens **doorgaan**.</span><span class="sxs-lookup"><span data-stu-id="613cb-164">**Step 11:** Enter hello password for hello new user account, and then select **Continue**.</span></span>

![Hallo wachtwoord invoeren](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image10.png)

<span data-ttu-id="613cb-166">**Stap 12:** Bevestig het wachtwoord voor de nieuwe gebruiker Hallo Hallo en selecteer vervolgens **doorgaan**.</span><span class="sxs-lookup"><span data-stu-id="613cb-166">**Step 12:** Confirm hello password for hello new user, and then select **Continue**.</span></span>

![Hallo wachtwoorden bevestigen](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image11.png)

<span data-ttu-id="613cb-168">**Stap 13:** Selecteer **Nee** (hello standaardoptie), en selecteer vervolgens **Enter**.</span><span class="sxs-lookup"><span data-stu-id="613cb-168">**Step 13:** Select **No** (hello default option), and then select **Enter**.</span></span>

![Gebruikers en wachtwoorden instellen](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image12.png)

<span data-ttu-id="613cb-170">**Step 14:** als Hallo tijdzone die wordt weergegeven correct is, selecteert u **Ja** (hello standaardoptie), en selecteer vervolgens **Enter**.</span><span class="sxs-lookup"><span data-stu-id="613cb-170">**Step 14:** If hello time zone that's displayed is correct, select **Yes** (hello default option), and then select **Enter**.</span></span>

<span data-ttu-id="613cb-171">tooreconfigure uw tijdzone, selecteer **Nee**.</span><span class="sxs-lookup"><span data-stu-id="613cb-171">tooreconfigure your time zone, select **No**.</span></span>

![Hallo klok configureren](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image13.png)

<span data-ttu-id="613cb-173">**Stap 15:** Hallo opties voor de methode partitioneren, selecteer **begeleide - volledige schijf gebruiken**, en selecteer vervolgens **Enter**.</span><span class="sxs-lookup"><span data-stu-id="613cb-173">**Step 15:** From hello partitioning method options, select **Guided - use entire disk**, and then select **Enter**.</span></span>

![Selecteer optie methode partitioneren Hallo](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image14.png)

<span data-ttu-id="613cb-175">**Stap 16:** Selecteer Hallo geschikte schijf van Hallo **Selecteer schijf toopartition** opties en selecteer vervolgens **Enter**.</span><span class="sxs-lookup"><span data-stu-id="613cb-175">**Step 16:** Select hello appropriate disk from hello **Select disk toopartition** options, and then select **Enter**.</span></span>


![Hallo schijf selecteren](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image15.png)

<span data-ttu-id="613cb-177">**Stap 17:** Selecteer **Ja** toowrite Hallo wijzigingen toodisk en selecteer vervolgens **Enter**.</span><span class="sxs-lookup"><span data-stu-id="613cb-177">**Step 17:** Select **Yes** toowrite hello changes toodisk, and then select **Enter**.</span></span>

![Hallo wijzigingen toodisk schrijven](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image16.png)

<span data-ttu-id="613cb-179">**Stap 18:** Hallo standaardoptie selecteert, selecteert u **doorgaan**, en selecteer vervolgens **Enter**.</span><span class="sxs-lookup"><span data-stu-id="613cb-179">**Step 18:** Select hello default option, select **Continue**, and then select **Enter**.</span></span>

![Selecteer de standaardoptie Hallo](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image17.png)

<span data-ttu-id="613cb-181">**Stap 19:** Selecteer de relevante optie Hallo voor het beheren van upgrades op uw systeem, en selecteer vervolgens **Enter**.</span><span class="sxs-lookup"><span data-stu-id="613cb-181">**Step 19:** Select hello appropriate option for managing upgrades on your system, and then select **Enter**.</span></span>

![Selecteer hoe toomanage wordt bijgewerkt](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image18.png)

> [!WARNING]
> <span data-ttu-id="613cb-183">Omdat hello Azure Site Recovery hoofddoelserver een specifieke versie van Hallo Ubuntu vereist, moet u op tooensure die Hallo kernel upgrades zijn uitgeschakeld voor Hallo virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="613cb-183">Because hello Azure Site Recovery master target server requires a very specific version of hello Ubuntu, you need tooensure that hello kernel upgrades are disabled for hello virtual machine.</span></span> <span data-ttu-id="613cb-184">Als ze zijn ingeschakeld, veroorzaken eventuele upgrades voor reguliere Hallo hoofddoel server toomalfunction.</span><span class="sxs-lookup"><span data-stu-id="613cb-184">If they are enabled, then any regular upgrades cause hello master target server toomalfunction.</span></span> <span data-ttu-id="613cb-185">Zorg ervoor dat u selecteert Hallo **geen automatische updates** optie.</span><span class="sxs-lookup"><span data-stu-id="613cb-185">Make sure you select hello **No automatic updates** option.</span></span>


<span data-ttu-id="613cb-186">**Stap 20:** standaardopties selecteren.</span><span class="sxs-lookup"><span data-stu-id="613cb-186">**Step 20:** Select default options.</span></span> <span data-ttu-id="613cb-187">Als u openSSH wilt voor SSH-verbinding maken, selecteert u Hallo **OpenSSH server** optie en selecteer vervolgens **doorgaan**.</span><span class="sxs-lookup"><span data-stu-id="613cb-187">If you want openSSH for SSH connect, select hello **OpenSSH server** option, and then select **Continue**.</span></span>

![Selecteer de software](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image19.png)

<span data-ttu-id="613cb-189">**Stap 21:** Selecteer **Ja**, en selecteer vervolgens **Enter**.</span><span class="sxs-lookup"><span data-stu-id="613cb-189">**Step 21:** Select **Yes**, and then select **Enter**.</span></span>

![Doelsessie Hallo WORMGATEN opstartlaadprogramma](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image20.png)

<span data-ttu-id="613cb-191">**Stap 22:** Selecteer Hallo juiste apparaatstuurprogramma voor Hallo boot loader installatie (bij voorkeur **/dev/sda**), en selecteer vervolgens **Enter**.</span><span class="sxs-lookup"><span data-stu-id="613cb-191">**Step 22:** Select hello appropriate device for hello boot loader installation (preferably **/dev/sda**), and then select **Enter**.</span></span>

![Selecteer een apparaat voor opstarten laadprogramma installeren](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image21.png)

<span data-ttu-id="613cb-193">**Stap 23:** Selecteer **doorgaan**, en selecteer vervolgens **Enter** toofinish Hallo-installatie.</span><span class="sxs-lookup"><span data-stu-id="613cb-193">**Step 23:** Select **Continue**, and then select **Enter** toofinish hello installation.</span></span>

![Hallo-installatie voltooien](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image22.png)

<span data-ttu-id="613cb-195">Nadat het Hallo-installatie is voltooid, meld u aan toohello VM met de nieuwe gebruikersgegevens Hallo.</span><span class="sxs-lookup"><span data-stu-id="613cb-195">After hello installation has finished, sign in toohello VM with hello new user credentials.</span></span> <span data-ttu-id="613cb-196">(Raadpleeg te**stap 10** voor meer informatie.)</span><span class="sxs-lookup"><span data-stu-id="613cb-196">(Refer too**Step 10** for more information.)</span></span>

<span data-ttu-id="613cb-197">Hallo-stappen die worden beschreven in de volgende screenshot tooset Hallo hoofdmap Hallo gebruikerswachtwoord ondernemen.</span><span class="sxs-lookup"><span data-stu-id="613cb-197">Take hello steps that are described in hello following screenshot tooset hello ROOT user password.</span></span> <span data-ttu-id="613cb-198">Meld u vervolgens aan als hoofdgebruiker.</span><span class="sxs-lookup"><span data-stu-id="613cb-198">Then sign in as ROOT user.</span></span>

![Hallo hoofdmap gebruiker-wachtwoord instellen](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image23.png)


### <a name="prepare-hello-machine-for-configuration-as-a-master-target-server"></a><span data-ttu-id="613cb-200">Hallo-machine voor configuratie als een hoofddoelserver voorbereiden</span><span class="sxs-lookup"><span data-stu-id="613cb-200">Prepare hello machine for configuration as a master target server</span></span>
<span data-ttu-id="613cb-201">Hallo-machine voor de configuratie vervolgens voorbereiden als een hoofddoelserver.</span><span class="sxs-lookup"><span data-stu-id="613cb-201">Next, prepare hello machine for configuration as a master target server.</span></span>

<span data-ttu-id="613cb-202">tooget Hallo-ID voor elke harde SCSI-schijf in een virtuele machine met Linux inschakelen Hallo **schijf. EnableUUID = TRUE** parameter.</span><span class="sxs-lookup"><span data-stu-id="613cb-202">tooget hello ID for each SCSI hard disk in a Linux virtual machine, enable hello **disk.EnableUUID = TRUE** parameter.</span></span>

<span data-ttu-id="613cb-203">tooenable deze parameter, nemen Hallo volgende stappen:</span><span class="sxs-lookup"><span data-stu-id="613cb-203">tooenable this parameter, take hello following steps:</span></span>

1. <span data-ttu-id="613cb-204">De virtuele machine afgesloten.</span><span class="sxs-lookup"><span data-stu-id="613cb-204">Shut down your virtual machine.</span></span>

2. <span data-ttu-id="613cb-205">Met de rechtermuisknop op het Hallo-vermelding voor Hallo virtuele machine in het linkerdeelvenster Hallo en selecteer vervolgens **instellingen bewerken**.</span><span class="sxs-lookup"><span data-stu-id="613cb-205">Right-click hello entry for hello virtual machine in hello left pane, and then select **Edit Settings**.</span></span>

3. <span data-ttu-id="613cb-206">Selecteer Hallo **opties** tabblad.</span><span class="sxs-lookup"><span data-stu-id="613cb-206">Select hello **Options** tab.</span></span>

4. <span data-ttu-id="613cb-207">Selecteer in het linkerdeelvenster Hallo **Geavanceerd** > **algemene**, en selecteer vervolgens Hallo **configuratieparameters** knop op Hallo rechtsonder deel uit van welkomstscherm.</span><span class="sxs-lookup"><span data-stu-id="613cb-207">In hello left pane, select **Advanced** > **General**, and then select hello **Configuration Parameters** button on hello lower-right part of hello screen.</span></span>

    ![Tabblad Opties](./media/site-recovery-how-to-install-linux-master-target/media/image20.png)

    <span data-ttu-id="613cb-209">Hallo **configuratieparameters** optie is niet beschikbaar wanneer Hallo machine wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="613cb-209">hello **Configuration Parameters** option is not available when hello machine is running.</span></span> <span data-ttu-id="613cb-210">toomake op dit tabblad actief, Hallo virtuele machine afgesloten.</span><span class="sxs-lookup"><span data-stu-id="613cb-210">toomake this tab active, shut down hello virtual machine.</span></span>

5. <span data-ttu-id="613cb-211">Zie of een rij met **schijf. EnableUUID** bestaat al.</span><span class="sxs-lookup"><span data-stu-id="613cb-211">See whether a row with **disk.EnableUUID** already exists.</span></span>

    - <span data-ttu-id="613cb-212">Als Hallo waarde bestaat en is ingesteld te**False**, Hallo waarde te wijzigen**True**.</span><span class="sxs-lookup"><span data-stu-id="613cb-212">If hello value exists and is set too**False**, change hello value too**True**.</span></span> <span data-ttu-id="613cb-213">(Hallo waarden zijn niet hoofdlettergevoelig).</span><span class="sxs-lookup"><span data-stu-id="613cb-213">(hello values are not case-sensitive.)</span></span>

    - <span data-ttu-id="613cb-214">Als Hallo waarde bestaat en is ingesteld te**True**, selecteer **annuleren**.</span><span class="sxs-lookup"><span data-stu-id="613cb-214">If hello value exists and is set too**True**, select **Cancel**.</span></span>

    - <span data-ttu-id="613cb-215">Als het Hallo-waarde niet bestaat, selecteert u **rij toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="613cb-215">If hello value does not exist, select **Add Row**.</span></span>

    - <span data-ttu-id="613cb-216">In de kolom naam Hallo toevoegen **schijf. EnableUUID**, en stel Hallo waarde te**TRUE**.</span><span class="sxs-lookup"><span data-stu-id="613cb-216">In hello name column, add **disk.EnableUUID**, and then set hello value too**TRUE**.</span></span>

    ![Controleren of schijf. Er bestaat al een EnableUUID](./media/site-recovery-how-to-install-linux-master-target/media/image21.png)

#### <a name="disable-kernel-upgrades"></a><span data-ttu-id="613cb-218">Kernel-upgrades uitschakelen</span><span class="sxs-lookup"><span data-stu-id="613cb-218">Disable kernel upgrades</span></span>

<span data-ttu-id="613cb-219">Azure Site Recovery-hoofddoelserver vereist een specifieke versie van Hallo Ubuntu, zorg ervoor dat de Hallo kernel upgrades voor Hallo virtuele machine zijn uitgeschakeld.</span><span class="sxs-lookup"><span data-stu-id="613cb-219">Azure Site Recovery master target server requires a very specific version of hello Ubuntu, ensure that hello kernel upgrades are disabled for hello virtual machine.</span></span>

<span data-ttu-id="613cb-220">Als upgrades van de kernel zijn ingeschakeld, veroorzaken eventuele upgrades voor reguliere Hallo hoofddoel server toomalfunction.</span><span class="sxs-lookup"><span data-stu-id="613cb-220">If kernel upgrades are enabled, then any regular upgrades cause hello master target server toomalfunction.</span></span>

#### <a name="download-and-install-additional-packages"></a><span data-ttu-id="613cb-221">Extra pakketten downloaden en installeren</span><span class="sxs-lookup"><span data-stu-id="613cb-221">Download and install additional packages</span></span>

> [!NOTE]
> <span data-ttu-id="613cb-222">Zorg ervoor dat u Internet connectiviteit toodownload en extra pakketten installeren.</span><span class="sxs-lookup"><span data-stu-id="613cb-222">Make sure that you have Internet connectivity toodownload and install additional packages.</span></span> <span data-ttu-id="613cb-223">Als u geen verbinding met Internet, moet u toomanually deze RPM-pakketten zoeken en te installeren.</span><span class="sxs-lookup"><span data-stu-id="613cb-223">If you don't have Internet connectivity, you need toomanually find these RPM packages and install them.</span></span>

```
apt-get install -y multipath-tools lsscsi python-pyasn1 lvm2 kpartx
```

### <a name="get-hello-installer-for-setup"></a><span data-ttu-id="613cb-224">Hallo-installatieprogramma niet ophalen voor setup</span><span class="sxs-lookup"><span data-stu-id="613cb-224">Get hello installer for setup</span></span>

<span data-ttu-id="613cb-225">Als uw hoofddoel verbinding met Internet heeft, kunt u Hallo stappen toodownload Hallo installatieprogramma te volgen.</span><span class="sxs-lookup"><span data-stu-id="613cb-225">If your master target has Internet connectivity, you can use hello following steps toodownload hello installer.</span></span> <span data-ttu-id="613cb-226">U kunt anders Hallo installatieprogramma kopiëren vanuit de processerver Hallo en u deze vervolgens installeren.</span><span class="sxs-lookup"><span data-stu-id="613cb-226">Otherwise, you can copy hello installer from hello process server and then install it.</span></span>

#### <a name="download-hello-master-target-installation-packages"></a><span data-ttu-id="613cb-227">Hallo hoofddoel installatiepakketten downloaden</span><span class="sxs-lookup"><span data-stu-id="613cb-227">Download hello master target installation packages</span></span>

<span data-ttu-id="613cb-228">[Hallo nieuwste Linux hoofddoel installatie bits downloaden](https://aka.ms/latestlinuxmobsvc).</span><span class="sxs-lookup"><span data-stu-id="613cb-228">[Download hello latest Linux master target installation bits](https://aka.ms/latestlinuxmobsvc).</span></span>

<span data-ttu-id="613cb-229">toodownload deze via Linux, type:</span><span class="sxs-lookup"><span data-stu-id="613cb-229">toodownload it by using Linux, type:</span></span>

```
wget https://aka.ms/latestlinuxmobsvc -O latestlinuxmobsvc.tar.gz
```

<span data-ttu-id="613cb-230">Zorg ervoor dat u downloaden en uitpakken van Hallo installer in de basismap.</span><span class="sxs-lookup"><span data-stu-id="613cb-230">Make sure that you download and unzip hello installer in your home directory.</span></span> <span data-ttu-id="613cb-231">Als u te pakken**/usr/Local**, mislukt de installatie van de Hallo.</span><span class="sxs-lookup"><span data-stu-id="613cb-231">If you unzip too**/usr/Local**, then hello installation  fails.</span></span>


#### <a name="access-hello-installer-from-hello-process-server"></a><span data-ttu-id="613cb-232">Toegang Hallo installatieprogramma van de processerver Hallo</span><span class="sxs-lookup"><span data-stu-id="613cb-232">Access hello installer from hello process server</span></span>

1. <span data-ttu-id="613cb-233">Op de processerver hello, gaat u te**C:\Program Files (x86) \Microsoft Azure Site Recovery\home\svsystems\pushinstallsvc\repository**.</span><span class="sxs-lookup"><span data-stu-id="613cb-233">On hello process server, go too**C:\Program Files (x86)\Microsoft Azure Site Recovery\home\svsystems\pushinstallsvc\repository**.</span></span>

2. <span data-ttu-id="613cb-234">Hallo vereist installer-bestand kopiëren vanuit de processerver Hallo en sla het bestand als **latestlinuxmobsvc.tar.gz** in de basismap.</span><span class="sxs-lookup"><span data-stu-id="613cb-234">Copy hello required installer file from hello process server, and save it as **latestlinuxmobsvc.tar.gz** in your home directory.</span></span>


### <a name="apply-custom-configuration-changes"></a><span data-ttu-id="613cb-235">Aangepaste configuratiewijzigingen toepassen</span><span class="sxs-lookup"><span data-stu-id="613cb-235">Apply custom configuration changes</span></span>

<span data-ttu-id="613cb-236">aangepaste configuratiewijzigingen tooapply gebruik Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="613cb-236">tooapply custom configuration changes, use hello following steps:</span></span>


1. <span data-ttu-id="613cb-237">Hallo na de opdracht toountar Hallo binair worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="613cb-237">Run hello following command toountar hello binary.</span></span>
    ```
    tar -zxvf latestlinuxmobsvc.tar.gz
    ```
    ![Schermopname van Hallo opdracht toorun](./media/site-recovery-how-to-install-linux-master-target/image16.png)

2. <span data-ttu-id="613cb-239">Voer Hallo opdracht toogive machtiging te volgen.</span><span class="sxs-lookup"><span data-stu-id="613cb-239">Run hello following command toogive permission.</span></span>
    ```
    chmod 755 ./ApplyCustomChanges.sh
    ```

3. <span data-ttu-id="613cb-240">Hallo opdrachtscript toorun Hallo volgende worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="613cb-240">Run hello following command toorun hello script.</span></span>
    ```
    ./ApplyCustomChanges.sh
    ```
> [!NOTE]
> <span data-ttu-id="613cb-241">Hallo script slechts eenmaal op Hallo server uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="613cb-241">Run hello script only once on hello server.</span></span> <span data-ttu-id="613cb-242">Hallo server afsluiten.</span><span class="sxs-lookup"><span data-stu-id="613cb-242">Shut down hello server.</span></span> <span data-ttu-id="613cb-243">Start opnieuw op Hallo server nadat u een schijf toevoegen zoals beschreven in de volgende sectie Hallo.</span><span class="sxs-lookup"><span data-stu-id="613cb-243">Then restart hello server after you add a disk, as described in hello next section.</span></span>

### <a name="add-a-retention-disk-toohello-linux-master-target-virtual-machine"></a><span data-ttu-id="613cb-244">Een bewaarperiode schijf toohello Linux hoofddoel virtuele machine toevoegen</span><span class="sxs-lookup"><span data-stu-id="613cb-244">Add a retention disk toohello Linux master target virtual machine</span></span>

<span data-ttu-id="613cb-245">Volgende stappen toocreate een bewaarschijf Hallo gebruiken:</span><span class="sxs-lookup"><span data-stu-id="613cb-245">Use hello following steps toocreate a retention disk:</span></span>

1. <span data-ttu-id="613cb-246">Een nieuwe schijf van 1 TB toohello Linux hoofddoel virtuele machine koppelen en vervolgens Hallo machine starten.</span><span class="sxs-lookup"><span data-stu-id="613cb-246">Attach a new 1-TB disk toohello Linux master target virtual machine, and then start hello machine.</span></span>

2. <span data-ttu-id="613cb-247">Gebruik Hallo **multipath -lle** opdracht toolearn Hallo multipath-ID van de bewaarschijf Hallo.</span><span class="sxs-lookup"><span data-stu-id="613cb-247">Use hello **multipath -ll** command toolearn hello multipath ID of hello retention disk.</span></span>

    ```
    multipath -ll
    ```
    ![Hallo multipath-ID van de bewaarschijf Hallo](./media/site-recovery-how-to-install-linux-master-target/media/image22.png)

3. <span data-ttu-id="613cb-249">Hallo station formatteren, en maak vervolgens een bestandssysteem op Hallo nieuwe schijf.</span><span class="sxs-lookup"><span data-stu-id="613cb-249">Format hello drive, and then create a file system on hello new drive.</span></span>

    ```
    mkfs.ext4 /dev/mapper/<Retention disk's multipath id>
    ```
    ![Een bestandssysteem maken op Hallo station](./media/site-recovery-how-to-install-linux-master-target/media/image23.png)

4. <span data-ttu-id="613cb-251">Nadat u het bestandssysteem Hallo hebt gemaakt, kunt u Hallo bewaren schijf koppelen.</span><span class="sxs-lookup"><span data-stu-id="613cb-251">After you create hello file system, mount hello retention disk.</span></span>
    ```
    mkdir /mnt/retention
    mount /dev/mapper/<Retention disk's multipath id> /mnt/retention
    ```
    ![Hallo-bewaarschijf koppelen](./media/site-recovery-how-to-install-linux-master-target/media/image24.png)

5. <span data-ttu-id="613cb-253">Hallo maken **fstab** vermelding toomount hello bewaarstation telkens wanneer Hallo-systeem wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="613cb-253">Create hello **fstab** entry toomount hello retention drive every time hello system starts.</span></span>
    ```
    vi /etc/fstab
    ```
    <span data-ttu-id="613cb-254">Selecteer **invoegen** toobegin Hallo-bestand te bewerken.</span><span class="sxs-lookup"><span data-stu-id="613cb-254">Select **Insert** toobegin editing hello file.</span></span> <span data-ttu-id="613cb-255">Maak een nieuwe regel en voeg vervolgens de volgende tekst hello.</span><span class="sxs-lookup"><span data-stu-id="613cb-255">Create a new line, and then insert hello following text.</span></span> <span data-ttu-id="613cb-256">Hallo schijf multipath-ID op basis van Hallo gemarkeerd multipath-ID van de vorige opdracht Hallo bewerken.</span><span class="sxs-lookup"><span data-stu-id="613cb-256">Edit hello disk multipath ID based on hello highlighted multipath ID from hello previous command.</span></span>

    <span data-ttu-id="613cb-257"> **/dev/mapper/ <Retention disks multipath id> /mnt/bewaren ext4 rw 0 0**</span><span class="sxs-lookup"><span data-stu-id="613cb-257">**/dev/mapper/<Retention disks multipath id> /mnt/retention ext4 rw 0 0**</span></span>

    <span data-ttu-id="613cb-258">Selecteer **Esc**, en typ vervolgens **: wq** (schrijven en afsluiten) tooclose Hallo-editorvenster.</span><span class="sxs-lookup"><span data-stu-id="613cb-258">Select **Esc**, and then type **:wq** (write and quit) tooclose hello editor window.</span></span>

### <a name="install-hello-master-target"></a><span data-ttu-id="613cb-259">Hallo hoofddoel installeren</span><span class="sxs-lookup"><span data-stu-id="613cb-259">Install hello master target</span></span>

> [!IMPORTANT]
> <span data-ttu-id="613cb-260">Hallo-versie van de hoofddoelserver Hallo moet gelijk tooor ouder is dan het Hallo-versies van Hallo processerver en de configuratieserver Hallo.</span><span class="sxs-lookup"><span data-stu-id="613cb-260">hello version of hello master target server must be equal tooor earlier than hello versions of hello process server and hello configuration server.</span></span> <span data-ttu-id="613cb-261">Als dit probleem niet wordt voldaan, beveiligt is geslaagd, maar mislukt de replicatie.</span><span class="sxs-lookup"><span data-stu-id="613cb-261">If this condition is not met, reprotect succeeds, but replication fails.</span></span>


> [!NOTE]
> <span data-ttu-id="613cb-262">Voordat u Hallo hoofddoelserver installeert, controleert u dat Hallo **/etc/hosts** -bestand op Hallo virtuele machine bevat items die zijn toegewezen Hallo lokale hostnaam toohello IP-adressen die gekoppeld aan alle netwerkadapters zijn.</span><span class="sxs-lookup"><span data-stu-id="613cb-262">Before you install hello master target server, check that hello **/etc/hosts** file on hello virtual machine contains entries that map hello local hostname toohello IP addresses that are associated with all network adapters.</span></span>

1. <span data-ttu-id="613cb-263">Kopieer Hallo wachtwoordzin van **C:\ProgramData\Microsoft Azure Site Recovery\private\connection.passphrase** op Hallo configuratieserver.</span><span class="sxs-lookup"><span data-stu-id="613cb-263">Copy hello passphrase from **C:\ProgramData\Microsoft Azure Site Recovery\private\connection.passphrase** on hello configuration server.</span></span> <span data-ttu-id="613cb-264">Sla het als **passphrase.txt** in Hallo Hallo dezelfde lokale map door te voeren opdracht op te volgen:</span><span class="sxs-lookup"><span data-stu-id="613cb-264">Then save it as **passphrase.txt** in hello same local directory by running hello following command:</span></span>

    ```
    echo <passphrase> >passphrase.txt
    ```
    <span data-ttu-id="613cb-265">Voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="613cb-265">Example:</span></span> 
    
    ```
    echo itUx70I47uxDuUVY >passphrase.txt
    ```

2. <span data-ttu-id="613cb-266">Houd er rekening mee Hallo configuratieserver IP-adres.</span><span class="sxs-lookup"><span data-stu-id="613cb-266">Note hello configuration server's IP address.</span></span> <span data-ttu-id="613cb-267">U moet deze in de volgende stap Hallo.</span><span class="sxs-lookup"><span data-stu-id="613cb-267">You need it in hello next step.</span></span>

3. <span data-ttu-id="613cb-268">Hallo na de opdracht tooinstall hello hoofddoelserver worden uitgevoerd en Hallo-server registreren met de configuratieserver Hallo.</span><span class="sxs-lookup"><span data-stu-id="613cb-268">Run hello following command tooinstall hello master target server and register hello server with hello configuration server.</span></span>

    ```
    ./install -q -d /usr/local/ASR -r MT -v VmWare
    /usr/local/ASR/Vx/bin/UnifiedAgentConfigurator.sh -i <ConfigurationServer IP Address> -P passphrase.txt
    ```

    <span data-ttu-id="613cb-269">Voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="613cb-269">Example:</span></span> 
    
    ```
    /usr/local/ASR/Vx/bin/UnifiedAgentConfigurator.sh -i 104.40.75.37 -P passphrase.txt
    ```

    <span data-ttu-id="613cb-270">Wacht totdat het Hallo-script is voltooid.</span><span class="sxs-lookup"><span data-stu-id="613cb-270">Wait until hello script finishes.</span></span> <span data-ttu-id="613cb-271">Als het hoofddoel Hallo is geregistreerd, hoofddoel Hallo wordt weergegeven op Hallo **Site Recovery-infrastructuur** pagina van het Hallo-portal.</span><span class="sxs-lookup"><span data-stu-id="613cb-271">If hello master target registers sucessfully, hello master target is listed on hello **Site Recovery Infrastructure** page of hello portal.</span></span>


#### <a name="install-hello-master-target-by-using-interactive-installation"></a><span data-ttu-id="613cb-272">Hallo hoofddoel installeren met behulp van interactieve installatie</span><span class="sxs-lookup"><span data-stu-id="613cb-272">Install hello master target by using interactive installation</span></span>

1. <span data-ttu-id="613cb-273">Hallo na de opdracht tooinstall hello hoofddoelserver worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="613cb-273">Run hello following command tooinstall hello master target.</span></span> <span data-ttu-id="613cb-274">Voor de rol van de agent hello, kies **hoofddoel**.</span><span class="sxs-lookup"><span data-stu-id="613cb-274">For hello agent role, choose **Master Target**.</span></span>

    ```
    ./install
    ```

2. <span data-ttu-id="613cb-275">Kies Hallo standaardlocatie voor installatie en selecteer vervolgens **Enter** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="613cb-275">Choose hello default location for installation, and then select **Enter** toocontinue.</span></span>

    ![Een standaardlocatie voor installatie van het hoofddoel kiezen](./media/site-recovery-how-to-install-linux-master-target/image17.png)

<span data-ttu-id="613cb-277">Nadat het Hallo-installatie is voltooid, kunt u de Hallo configuratieserver registreren via de opdrachtregel Hallo.</span><span class="sxs-lookup"><span data-stu-id="613cb-277">After hello installation has finished, register hello configuration server by using hello command line.</span></span>

1. <span data-ttu-id="613cb-278">Houd er rekening mee Hallo IP-adres van de configuratieserver Hallo.</span><span class="sxs-lookup"><span data-stu-id="613cb-278">Note hello IP address of hello configuration server.</span></span> <span data-ttu-id="613cb-279">U moet deze in de volgende stap Hallo.</span><span class="sxs-lookup"><span data-stu-id="613cb-279">You need it in hello next step.</span></span>

2. <span data-ttu-id="613cb-280">Hallo na de opdracht tooinstall hello hoofddoelserver worden uitgevoerd en Hallo-server registreren met de configuratieserver Hallo.</span><span class="sxs-lookup"><span data-stu-id="613cb-280">Run hello following command tooinstall hello master target server and register hello server with hello configuration server.</span></span>

    ```
    ./install -q -d /usr/local/ASR -r MT -v VmWare
    /usr/local/ASR/Vx/bin/UnifiedAgentConfigurator.sh -i <ConfigurationServer IP Address> -P passphrase.txt
    ```
    <span data-ttu-id="613cb-281">Voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="613cb-281">Example:</span></span> 

    ```
    /usr/local/ASR/Vx/bin/UnifiedAgentConfigurator.sh -i 104.40.75.37 -P passphrase.txt
    ```

   <span data-ttu-id="613cb-282">Wacht totdat het Hallo-script is voltooid.</span><span class="sxs-lookup"><span data-stu-id="613cb-282">Wait until hello script finishes.</span></span> <span data-ttu-id="613cb-283">Als het hoofddoel hello geregistreerd met succes is wordt, hoofddoel Hallo wordt vermeld op Hallo **Site Recovery-infrastructuur** pagina van het Hallo-portal.</span><span class="sxs-lookup"><span data-stu-id="613cb-283">If hello master target is registered succesfully, hello master target is listed on hello **Site Recovery Infrastructure** page of hello portal.</span></span>


### <a name="upgrade-hello-master-target"></a><span data-ttu-id="613cb-284">Hallo hoofddoel upgraden</span><span class="sxs-lookup"><span data-stu-id="613cb-284">Upgrade hello master target</span></span>

<span data-ttu-id="613cb-285">Hallo-installatieprogramma wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="613cb-285">Run hello installer.</span></span> <span data-ttu-id="613cb-286">Er wordt automatisch gedetecteerd dat die Hallo-agent is geïnstalleerd op het hoofddoel Hallo.</span><span class="sxs-lookup"><span data-stu-id="613cb-286">It automatically detects that hello agent is installed on hello master target.</span></span> <span data-ttu-id="613cb-287">tooupgrade, selecteer **Y**.  Nadat het Hallo-setup is voltooid, controleert u Hallo-versie van het hoofddoel Hallo geïnstalleerd met behulp van de volgende opdracht Hallo.</span><span class="sxs-lookup"><span data-stu-id="613cb-287">tooupgrade, select **Y**.  After hello setup has been completed, check hello version of hello master target installed by using hello following command.</span></span>

    ```
    cat /usr/local/.vx_version
    ```

<span data-ttu-id="613cb-288">U kunt zien die Hallo **versie** veld kunt Hallo versienummer van het hoofddoel Hallo.</span><span class="sxs-lookup"><span data-stu-id="613cb-288">You can see that hello **Version** field gives hello version number of hello master target.</span></span>

### <a name="install-vmware-tools-on-hello-master-target-server"></a><span data-ttu-id="613cb-289">VMware-hulpprogramma's installeren op de hoofddoelserver Hallo</span><span class="sxs-lookup"><span data-stu-id="613cb-289">Install VMware tools on hello master target server</span></span>

<span data-ttu-id="613cb-290">U moet tooinstall VMware tools op het hoofddoel Hallo zodat het Hallo-gegevensarchieven kan detecteren.</span><span class="sxs-lookup"><span data-stu-id="613cb-290">You need tooinstall VMware tools on hello master target so that it can discover hello data stores.</span></span> <span data-ttu-id="613cb-291">Als Hallo-hulpprogramma's zijn niet geïnstalleerd, is niet in de gegevensarchieven Hallo beveiligt welkomstscherm vermeld.</span><span class="sxs-lookup"><span data-stu-id="613cb-291">If hello tools are not installed, hello reprotect screen isn't listed in hello data stores.</span></span> <span data-ttu-id="613cb-292">Na installatie van Hallo VMware tools moet u toorestart.</span><span class="sxs-lookup"><span data-stu-id="613cb-292">After installation of hello VMware tools, you need toorestart.</span></span>

## <a name="next-steps"></a><span data-ttu-id="613cb-293">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="613cb-293">Next steps</span></span>
<span data-ttu-id="613cb-294">Nadat het Hallo-installatie en registratie van het hoofddoel Hallo heeft finsihed, ziet u Hallo hoofddoel worden weergegeven op Hallo **hoofddoel** in sectie **Site Recovery-infrastructuur**, onder Hallo overzicht van configuratie-server.</span><span class="sxs-lookup"><span data-stu-id="613cb-294">After hello installation and registration of hello master target has finsihed, you can see hello master target appear on hello **Master Target** section in **Site Recovery Infrastructure**, under hello configuration server overview.</span></span>

<span data-ttu-id="613cb-295">U kunt nu doorgaan met [beveiligingspoging](site-recovery-how-to-reprotect.md), gevolgd door de failback.</span><span class="sxs-lookup"><span data-stu-id="613cb-295">You can now proceed with [reprotection](site-recovery-how-to-reprotect.md), followed by failback.</span></span>

## <a name="common-issues"></a><span data-ttu-id="613cb-296">Algemene problemen</span><span class="sxs-lookup"><span data-stu-id="613cb-296">Common issues</span></span>

* <span data-ttu-id="613cb-297">Zorg ervoor dat u inschakelt Storage vMotion op eventuele management-onderdelen, zoals een hoofddoel.</span><span class="sxs-lookup"><span data-stu-id="613cb-297">Make sure you do not turn on Storage vMotion on any management components such as a master target.</span></span> <span data-ttu-id="613cb-298">Als hoofddoel Hallo na een geslaagde beveiligt verplaatst, kan de schijven van de virtuele machine hello (VMDKs) kunnen niet worden losgekoppeld.</span><span class="sxs-lookup"><span data-stu-id="613cb-298">If hello master target moves after a successful reprotect, hello virtual machine disks (VMDKs) cannot be detached.</span></span> <span data-ttu-id="613cb-299">In dit geval failback is mislukt.</span><span class="sxs-lookup"><span data-stu-id="613cb-299">In this case, failback fails.</span></span>

* <span data-ttu-id="613cb-300">Hallo hoofddoel mag geen eventuele momentopnamen op Hallo virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="613cb-300">hello master target should not have any snapshots on hello virtual machine.</span></span> <span data-ttu-id="613cb-301">Als momentopnamen bevat, mislukt de failback.</span><span class="sxs-lookup"><span data-stu-id="613cb-301">If there are snapshots, failback fails.</span></span>

* <span data-ttu-id="613cb-302">Hallo-netwerkinterface tijdens het opstarten is uitgeschakeld vanwege toosome aangepaste NIC configuraties op sommige klanten, en Hallo hoofddoel agent kan niet worden geïnitialiseerd.</span><span class="sxs-lookup"><span data-stu-id="613cb-302">Due toosome custom NIC configurations at some customers, hello network interface is disabled during startup, and hello master target agent cannot initialize.</span></span> <span data-ttu-id="613cb-303">Zorg ervoor dat Hallo volgende eigenschappen correct zijn ingesteld.</span><span class="sxs-lookup"><span data-stu-id="613cb-303">Make sure that hello following properties are correctly set.</span></span> <span data-ttu-id="613cb-304">Controleer deze eigenschappen in Hallo Ethernet-kaart van het bestand /etc/sysconfig/network-scripts/ifcfg-eth *.</span><span class="sxs-lookup"><span data-stu-id="613cb-304">Check these properties in hello Ethernet card file's /etc/sysconfig/network-scripts/ifcfg-eth*.</span></span>
    * <span data-ttu-id="613cb-305">BOOTPROTO = dhcp</span><span class="sxs-lookup"><span data-stu-id="613cb-305">BOOTPROTO=dhcp</span></span>
    * <span data-ttu-id="613cb-306">ONBOOT = yes</span><span class="sxs-lookup"><span data-stu-id="613cb-306">ONBOOT=yes</span></span>

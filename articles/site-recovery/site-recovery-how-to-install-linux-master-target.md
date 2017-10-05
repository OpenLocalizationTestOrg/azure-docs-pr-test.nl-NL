---
title: Het installeren van een Linux-hoofddoelserver voor failover van Azure met on-premises | Microsoft Docs
description: Voordat een virtuele Linux-machine opnieuw te beveiligen, moet u een Linux-hoofddoelserver. Informatie over het installeren van een.
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
ms.openlocfilehash: 5341e3e56e0c366079958dd9a885f6ee3e8436cb
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="install-a-linux-master-target-server"></a><span data-ttu-id="3e30e-104">Een Linux-hoofddoel-server installeren</span><span class="sxs-lookup"><span data-stu-id="3e30e-104">Install a Linux master target server</span></span>
<span data-ttu-id="3e30e-105">Nadat u uw virtuele machines failover, u kunt een failback uit op de virtuele machines naar de lokale site.</span><span class="sxs-lookup"><span data-stu-id="3e30e-105">After you fail over your virtual machines, you can fail back the virtual machines to the on-premises site.</span></span> <span data-ttu-id="3e30e-106">Als u wilt een failback uit, moet u beveiligt u de virtuele machine van Azure naar de lokale site opnieuw.</span><span class="sxs-lookup"><span data-stu-id="3e30e-106">To fail back, you need to reprotect the virtual machine from Azure to the on-premises site.</span></span> <span data-ttu-id="3e30e-107">Voor dit proces moet u de doelserver van een lokale voor het ontvangen van het verkeer.</span><span class="sxs-lookup"><span data-stu-id="3e30e-107">For this process, you need an on-premises master target server to receive the traffic.</span></span> 

<span data-ttu-id="3e30e-108">Als de beveiligde virtuele machine een virtuele Windows-computer is, moet u een Windows-hoofddoel.</span><span class="sxs-lookup"><span data-stu-id="3e30e-108">If your protected virtual machine is a Windows virtual machine, then you need a Windows master target.</span></span> <span data-ttu-id="3e30e-109">Voor een virtuele Linux-machine moet u een Linux-hoofddoel.</span><span class="sxs-lookup"><span data-stu-id="3e30e-109">For a Linux virtual machine, you need a Linux master target.</span></span> <span data-ttu-id="3e30e-110">Lees de volgende stappen uit voor informatie over het maken en een Linux-hoofddoel te installeren.</span><span class="sxs-lookup"><span data-stu-id="3e30e-110">Read the following steps to learn how to create and install a Linux master target.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3e30e-111">Vanaf versie van de 9.10.0 hoofddoelserver, de meest recente hoofddoelserver kan alleen worden geïnstalleerd op een 16.04 Ubuntu server.</span><span class="sxs-lookup"><span data-stu-id="3e30e-111">Starting with release of the 9.10.0 master target server, the latest master target server can be only installed on an Ubuntu 16.04 server.</span></span> <span data-ttu-id="3e30e-112">Nieuwe installaties zijn niet toegestaan voor CentOS6.6 servers.</span><span class="sxs-lookup"><span data-stu-id="3e30e-112">New installations aren't allowed on  CentOS6.6 servers.</span></span> <span data-ttu-id="3e30e-113">U kunt echter doorgaan naar de oude hoofdsleutel doelservers upgraden met behulp van de 9.10.0 versie.</span><span class="sxs-lookup"><span data-stu-id="3e30e-113">However, you can continue to upgrade your old master target servers by using the 9.10.0 version.</span></span>

## <a name="overview"></a><span data-ttu-id="3e30e-114">Overzicht</span><span class="sxs-lookup"><span data-stu-id="3e30e-114">Overview</span></span>
<span data-ttu-id="3e30e-115">In dit artikel bevat instructies voor het installeren van een Linux-hoofddoel.</span><span class="sxs-lookup"><span data-stu-id="3e30e-115">This article provides instructions for how to install a Linux master target.</span></span>

<span data-ttu-id="3e30e-116">Opmerkingen of vragen plaatsen aan het einde van dit artikel of op de [Azure Recovery Services-Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="3e30e-116">Post comments or questions at the end of this article or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3e30e-117">Vereisten</span><span class="sxs-lookup"><span data-stu-id="3e30e-117">Prerequisites</span></span>

* <span data-ttu-id="3e30e-118">Als u de host waarop voor het implementeren van het hoofddoel, bepalen als de failback is het verstandig om een bestaande on-premises virtuele machine of een nieuwe virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="3e30e-118">To choose the host on which to deploy the master target, determine if the failback is going to be to an existing on-premises virtual machine or to a new virtual machine.</span></span> 
    * <span data-ttu-id="3e30e-119">Voor een bestaande virtuele machine, moet de host van het hoofddoel toegang hebben tot de gegevensarchieven van de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="3e30e-119">For an existing virtual machine, the host of the master target should have access to the data stores of the virtual machine.</span></span>
    * <span data-ttu-id="3e30e-120">Als de on-premises virtuele machine niet bestaat, wordt de failback van virtuele machine gemaakt op dezelfde host als het hoofddoel.</span><span class="sxs-lookup"><span data-stu-id="3e30e-120">If the on-premises virtual machine does not exist, the failback virtual machine is created on the same host as the master target.</span></span> <span data-ttu-id="3e30e-121">U kunt een willekeurige host ESXi voor het installeren van het hoofddoel.</span><span class="sxs-lookup"><span data-stu-id="3e30e-121">You can choose any ESXi host to install the master target.</span></span>
* <span data-ttu-id="3e30e-122">Het hoofddoel moet zich op een netwerk dat met de processerver en de configuratieserver communiceren kan.</span><span class="sxs-lookup"><span data-stu-id="3e30e-122">The master target should be on a network that can communicate with the process server and the configuration server.</span></span>
* <span data-ttu-id="3e30e-123">De versie van het hoofddoel moet gelijk zijn aan of ouder is dan de versies van de processerver en de configuratieserver.</span><span class="sxs-lookup"><span data-stu-id="3e30e-123">The version of the master target must be equal to or earlier than the versions of the process server and the configuration server.</span></span> <span data-ttu-id="3e30e-124">Bijvoorbeeld, als de versie van de configuratieserver 9.4, kan de versie van het hoofddoel worden 9.4 of 9.3 maar niet 9.5.</span><span class="sxs-lookup"><span data-stu-id="3e30e-124">For example, if the version of the configuration server is 9.4, the version of the master target can be 9.4 or 9.3 but not 9.5.</span></span>
* <span data-ttu-id="3e30e-125">Het hoofddoel mag alleen een virtuele VMware-machine en niet op een fysieke server.</span><span class="sxs-lookup"><span data-stu-id="3e30e-125">The master target can only be a VMware virtual machine and not a physical server.</span></span>

## <a name="create-the-master-target-according-to-the-sizing-guidelines"></a><span data-ttu-id="3e30e-126">Het hoofddoel overeenkomstig de richtlijnen van het formaat maken</span><span class="sxs-lookup"><span data-stu-id="3e30e-126">Create the master target according to the sizing guidelines</span></span>

<span data-ttu-id="3e30e-127">Het hoofddoel in overeenstemming met de volgende richtlijnen voor schaling maken:</span><span class="sxs-lookup"><span data-stu-id="3e30e-127">Create the master target in accordance with the following sizing guidelines:</span></span>
- <span data-ttu-id="3e30e-128">**RAM-geheugen**: 6 GB of meer</span><span class="sxs-lookup"><span data-stu-id="3e30e-128">**RAM**: 6 GB or more</span></span>
- <span data-ttu-id="3e30e-129">**OS-schijfgrootte**: 100 GB of meer (om te installeren CentOS6.6)</span><span class="sxs-lookup"><span data-stu-id="3e30e-129">**OS disk size**: 100 GB or more (to install CentOS6.6)</span></span>
- <span data-ttu-id="3e30e-130">**Aanvullende schijfgrootte voor bewaarstation**: 1 TB</span><span class="sxs-lookup"><span data-stu-id="3e30e-130">**Additional disk size for retention drive**: 1 TB</span></span>
- <span data-ttu-id="3e30e-131">**CPU-kernen**: 4 kernen of meer</span><span class="sxs-lookup"><span data-stu-id="3e30e-131">**CPU cores**: 4 cores or more</span></span>

<span data-ttu-id="3e30e-132">De volgende ondersteunde Ubuntu kernels worden ondersteund.</span><span class="sxs-lookup"><span data-stu-id="3e30e-132">The following supported Ubuntu kernels are supported.</span></span>


|<span data-ttu-id="3e30e-133">Kernel-reeks</span><span class="sxs-lookup"><span data-stu-id="3e30e-133">Kernel Series</span></span>  |<span data-ttu-id="3e30e-134">Ondersteuning voor maximaal</span><span class="sxs-lookup"><span data-stu-id="3e30e-134">Support up to</span></span>  |
|---------|---------|
|<span data-ttu-id="3e30e-135">4.4</span><span class="sxs-lookup"><span data-stu-id="3e30e-135">4.4</span></span>      |<span data-ttu-id="3e30e-136">4.4.0-81-Generic</span><span class="sxs-lookup"><span data-stu-id="3e30e-136">4.4.0-81-generic</span></span>         |
|<span data-ttu-id="3e30e-137">4.8</span><span class="sxs-lookup"><span data-stu-id="3e30e-137">4.8</span></span>      |<span data-ttu-id="3e30e-138">4.8.0-56-Generic</span><span class="sxs-lookup"><span data-stu-id="3e30e-138">4.8.0-56-generic</span></span>         |
|<span data-ttu-id="3e30e-139">4.10</span><span class="sxs-lookup"><span data-stu-id="3e30e-139">4.10</span></span>     |<span data-ttu-id="3e30e-140">4.10.0-24-Generic</span><span class="sxs-lookup"><span data-stu-id="3e30e-140">4.10.0-24-generic</span></span>        |


## <a name="deploy-the-master-target-server"></a><span data-ttu-id="3e30e-141">De hoofddoelserver implementeren</span><span class="sxs-lookup"><span data-stu-id="3e30e-141">Deploy the master target server</span></span>

### <a name="install-ubuntu-16042-minimal"></a><span data-ttu-id="3e30e-142">Ubuntu 16.04.2 installeren minimale</span><span class="sxs-lookup"><span data-stu-id="3e30e-142">Install Ubuntu 16.04.2 Minimal</span></span>

<span data-ttu-id="3e30e-143">Met het volgende de stappen voor het installeren van de Ubuntu 16.04.2 64-bits besturingssysteem.</span><span class="sxs-lookup"><span data-stu-id="3e30e-143">Take the following the steps to install the Ubuntu 16.04.2 64-bit operating system.</span></span>

<span data-ttu-id="3e30e-144">**Stap 1:** gaat u naar de [downloadkoppeling](https://www.ubuntu.com/download/server/thank-you?version=16.04.2&architecture=amd64) en kies de dichtstbijzijnde spiegelen uit welke downloaden Ubuntu 16.04.2 minimaal 64-bits ISO.</span><span class="sxs-lookup"><span data-stu-id="3e30e-144">**Step 1:** Go to the [download link](https://www.ubuntu.com/download/server/thank-you?version=16.04.2&architecture=amd64) and choose the closest mirror from which download an Ubuntu 16.04.2 minimal 64-bit ISO.</span></span>

<span data-ttu-id="3e30e-145">Ubuntu 16.04.2 minimaal 64-bits ISO houden in het DVD-station en start het systeem.</span><span class="sxs-lookup"><span data-stu-id="3e30e-145">Keep an Ubuntu 16.04.2 minimal 64-bit ISO in the DVD drive and start the system.</span></span>

<span data-ttu-id="3e30e-146">**Stap 2:** Selecteer **Engels** als uw voorkeurstaal en selecteer vervolgens **Enter**.</span><span class="sxs-lookup"><span data-stu-id="3e30e-146">**Step 2:** Select **English** as your preferred language, and then select **Enter**.</span></span>

![Een taal selecteren](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image1.png)

<span data-ttu-id="3e30e-148">**Stap 3:** Selecteer **Ubuntu Server installeren**, en selecteer vervolgens **Enter**.</span><span class="sxs-lookup"><span data-stu-id="3e30e-148">**Step 3:** Select **Install Ubuntu Server**, and then select **Enter**.</span></span>

![Selecteer installeren Ubuntu Server](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image2.png)

<span data-ttu-id="3e30e-150">**Stap 4:** Selecteer **Engels** als uw voorkeurstaal en selecteer vervolgens **Enter**.</span><span class="sxs-lookup"><span data-stu-id="3e30e-150">**Step 4:** Select **English** as your preferred language, and then select **Enter**.</span></span>

![Engels als uw voorkeurstaal selecteren](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image3.png)

<span data-ttu-id="3e30e-152">**Stap 5:** Selecteer de relevante optie van de **tijdzone** optielijst en selecteer vervolgens **Enter**.</span><span class="sxs-lookup"><span data-stu-id="3e30e-152">**Step 5:** Select the appropriate option from the **Time Zone** options list, and then select **Enter**.</span></span>

![Selecteer de juiste tijdzone](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image4.png)

<span data-ttu-id="3e30e-154">**Stap 6:** Selecteer **Nee** (de standaardoptie) en selecteer vervolgens **Enter**.</span><span class="sxs-lookup"><span data-stu-id="3e30e-154">**Step 6:** Select **No** (the default option), and then select **Enter**.</span></span>


![Het toetsenbord configureren](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image5.png)

<span data-ttu-id="3e30e-156">**Stap 7:** Selecteer **Engels (V.S.)** als het land van oorsprong voor het toetsenbord en selecteer vervolgens **Enter**.</span><span class="sxs-lookup"><span data-stu-id="3e30e-156">**Step 7:** Select **English (US)** as the country of origin for the keyboard, and then select **Enter**.</span></span>

![VS selecteren als het land van oorsprong](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image6.png)

<span data-ttu-id="3e30e-158">**Stap 8:** Selecteer **Engels (V.S.)** als de toetsenbordindeling en selecteer vervolgens **Enter**.</span><span class="sxs-lookup"><span data-stu-id="3e30e-158">**Step 8:** Select **English (US)** as the keyboard layout, and then select **Enter**.</span></span>

![Als de toetsenbordindeling Amerikaans Engels selecteren](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image7.png)

<span data-ttu-id="3e30e-160">**Stap 9:** Geef de hostnaam op voor uw server in de **hostnaam** vak en selecteer vervolgens **doorgaan**.</span><span class="sxs-lookup"><span data-stu-id="3e30e-160">**Step 9:** Enter the hostname for your server in the **Hostname** box, and then select **Continue**.</span></span>

![Geef de hostnaam op voor uw server](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image8.png)

<span data-ttu-id="3e30e-162">**Stap 10:** voor het maken van een gebruikersaccount, voer de gebruikersnaam en selecteer vervolgens **doorgaan**.</span><span class="sxs-lookup"><span data-stu-id="3e30e-162">**Step 10:** To create a user account, enter the user name, and then select **Continue**.</span></span>

![Een gebruikersaccount maken](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image9.png)

<span data-ttu-id="3e30e-164">**Stap 11:** Voer het wachtwoord voor het nieuwe gebruikersaccount en selecteer vervolgens **doorgaan**.</span><span class="sxs-lookup"><span data-stu-id="3e30e-164">**Step 11:** Enter the password for the new user account, and then select **Continue**.</span></span>

![Voer het wachtwoord](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image10.png)

<span data-ttu-id="3e30e-166">**Stap 12:** Bevestig het wachtwoord voor de nieuwe gebruiker en selecteer vervolgens **doorgaan**.</span><span class="sxs-lookup"><span data-stu-id="3e30e-166">**Step 12:** Confirm the password for the new user, and then select **Continue**.</span></span>

![De wachtwoorden bevestigen](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image11.png)

<span data-ttu-id="3e30e-168">**Stap 13:** Selecteer **Nee** (de standaardoptie) en selecteer vervolgens **Enter**.</span><span class="sxs-lookup"><span data-stu-id="3e30e-168">**Step 13:** Select **No** (the default option), and then select **Enter**.</span></span>

![Gebruikers en wachtwoorden instellen](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image12.png)

<span data-ttu-id="3e30e-170">**Step 14:** als de tijdzone die wordt weergegeven correct is, selecteert u **Ja** (de standaardoptie) en selecteer vervolgens **Enter**.</span><span class="sxs-lookup"><span data-stu-id="3e30e-170">**Step 14:** If the time zone that's displayed is correct, select **Yes** (the default option), and then select **Enter**.</span></span>

<span data-ttu-id="3e30e-171">Selecteer om opnieuw te uw tijdzone, **Nee**.</span><span class="sxs-lookup"><span data-stu-id="3e30e-171">To reconfigure your time zone, select **No**.</span></span>

![Configureer de klok](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image13.png)

<span data-ttu-id="3e30e-173">**Stap 15:** uit de partitionering opties van de methode selecteren **begeleide - volledige schijf gebruiken**, en selecteer vervolgens **Enter**.</span><span class="sxs-lookup"><span data-stu-id="3e30e-173">**Step 15:** From the partitioning method options, select **Guided - use entire disk**, and then select **Enter**.</span></span>

![Selecteer de partitionering methode-optie](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image14.png)

<span data-ttu-id="3e30e-175">**Stap 16:** selecteert u de juiste virtuele schijf van de **Select disk aan partitie** opties en selecteer vervolgens **Enter**.</span><span class="sxs-lookup"><span data-stu-id="3e30e-175">**Step 16:** Select the appropriate disk from the **Select disk to partition** options, and then select **Enter**.</span></span>


![Selecteer de schijf](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image15.png)

<span data-ttu-id="3e30e-177">**Stap 17:** Selecteer **Ja** schrijven van de wijzigingen naar schijf en selecteer vervolgens **Enter**.</span><span class="sxs-lookup"><span data-stu-id="3e30e-177">**Step 17:** Select **Yes** to write the changes to disk, and then select **Enter**.</span></span>

![De wijzigingen naar de schijf te schrijven](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image16.png)

<span data-ttu-id="3e30e-179">**Stap 18:** selecteert u de standaardoptie **doorgaan**, en selecteer vervolgens **Enter**.</span><span class="sxs-lookup"><span data-stu-id="3e30e-179">**Step 18:** Select the default option, select **Continue**, and then select **Enter**.</span></span>

![Selecteer de standaardoptie](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image17.png)

<span data-ttu-id="3e30e-181">**Stap 19:** Selecteer de relevante optie voor het beheren van upgrades op uw systeem en selecteer vervolgens **Enter**.</span><span class="sxs-lookup"><span data-stu-id="3e30e-181">**Step 19:** Select the appropriate option for managing upgrades on your system, and then select **Enter**.</span></span>

![Selecteer het beheren van upgrades](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image18.png)

> [!WARNING]
> <span data-ttu-id="3e30e-183">Omdat de Azure Site Recovery hoofddoelserver een specifieke versie van de Ubuntu vereist, moet u ervoor te zorgen dat de kernel upgrades zijn uitgeschakeld voor de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="3e30e-183">Because the Azure Site Recovery master target server requires a very specific version of the Ubuntu, you need to ensure that the kernel upgrades are disabled for the virtual machine.</span></span> <span data-ttu-id="3e30e-184">Als ze zijn ingeschakeld, dan eventuele reguliere upgrades voor zorgen dat de hoofddoelserver is niet goed.</span><span class="sxs-lookup"><span data-stu-id="3e30e-184">If they are enabled, then any regular upgrades cause the master target server to malfunction.</span></span> <span data-ttu-id="3e30e-185">Zorg ervoor dat u selecteert de **geen automatische updates** optie.</span><span class="sxs-lookup"><span data-stu-id="3e30e-185">Make sure you select the **No automatic updates** option.</span></span>


<span data-ttu-id="3e30e-186">**Stap 20:** standaardopties selecteren.</span><span class="sxs-lookup"><span data-stu-id="3e30e-186">**Step 20:** Select default options.</span></span> <span data-ttu-id="3e30e-187">Als u openSSH wilt voor SSH-verbinding maken, selecteer de **OpenSSH server** optie en selecteer vervolgens **doorgaan**.</span><span class="sxs-lookup"><span data-stu-id="3e30e-187">If you want openSSH for SSH connect, select the **OpenSSH server** option, and then select **Continue**.</span></span>

![Selecteer de software](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image19.png)

<span data-ttu-id="3e30e-189">**Stap 21:** Selecteer **Ja**, en selecteer vervolgens **Enter**.</span><span class="sxs-lookup"><span data-stu-id="3e30e-189">**Step 21:** Select **Yes**, and then select **Enter**.</span></span>

![Het opstartlaadprogramma WORMGATEN doelsessie](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image20.png)

<span data-ttu-id="3e30e-191">**Stap 22:** selecteert u het juiste apparaat voor de installatie van het laadprogramma voor opstarten (bij voorkeur **/dev/sda**), en selecteer vervolgens **Enter**.</span><span class="sxs-lookup"><span data-stu-id="3e30e-191">**Step 22:** Select the appropriate device for the boot loader installation (preferably **/dev/sda**), and then select **Enter**.</span></span>

![Selecteer een apparaat voor opstarten laadprogramma installeren](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image21.png)

<span data-ttu-id="3e30e-193">**Stap 23:** Selecteer **doorgaan**, en selecteer vervolgens **Enter** om de installatie te voltooien.</span><span class="sxs-lookup"><span data-stu-id="3e30e-193">**Step 23:** Select **Continue**, and then select **Enter** to finish the installation.</span></span>

![De installatie voltooien](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image22.png)

<span data-ttu-id="3e30e-195">Nadat de installatie is voltooid, moet u zich aanmelden bij de virtuele machine met de nieuwe gebruikersgegevens.</span><span class="sxs-lookup"><span data-stu-id="3e30e-195">After the installation has finished, sign in to the VM with the new user credentials.</span></span> <span data-ttu-id="3e30e-196">(Raadpleeg **stap 10** voor meer informatie.)</span><span class="sxs-lookup"><span data-stu-id="3e30e-196">(Refer to **Step 10** for more information.)</span></span>

<span data-ttu-id="3e30e-197">Voer de stappen die worden beschreven in de volgende schermafbeelding om in te stellen het hoofdwachtwoord van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="3e30e-197">Take the steps that are described in the following screenshot to set the ROOT user password.</span></span> <span data-ttu-id="3e30e-198">Meld u vervolgens aan als hoofdgebruiker.</span><span class="sxs-lookup"><span data-stu-id="3e30e-198">Then sign in as ROOT user.</span></span>

![De hoofdmap gebruikerswachtwoord instellen](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image23.png)


### <a name="prepare-the-machine-for-configuration-as-a-master-target-server"></a><span data-ttu-id="3e30e-200">Voorbereiden van de machine voor configuratie als een hoofddoelserver</span><span class="sxs-lookup"><span data-stu-id="3e30e-200">Prepare the machine for configuration as a master target server</span></span>
<span data-ttu-id="3e30e-201">Bereid de machine voor de configuratie vervolgens als een hoofddoelserver.</span><span class="sxs-lookup"><span data-stu-id="3e30e-201">Next, prepare the machine for configuration as a master target server.</span></span>

<span data-ttu-id="3e30e-202">Als u de ID voor elke harde SCSI-schijf in een virtuele Linux-machine, schakel de **schijf. EnableUUID = TRUE** parameter.</span><span class="sxs-lookup"><span data-stu-id="3e30e-202">To get the ID for each SCSI hard disk in a Linux virtual machine, enable the **disk.EnableUUID = TRUE** parameter.</span></span>

<span data-ttu-id="3e30e-203">Voor deze parameter inschakelt, moet u de volgende stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="3e30e-203">To enable this parameter, take the following steps:</span></span>

1. <span data-ttu-id="3e30e-204">De virtuele machine afgesloten.</span><span class="sxs-lookup"><span data-stu-id="3e30e-204">Shut down your virtual machine.</span></span>

2. <span data-ttu-id="3e30e-205">Met de rechtermuisknop op de vermelding voor de virtuele machine in het linkerdeelvenster en selecteer vervolgens **instellingen bewerken**.</span><span class="sxs-lookup"><span data-stu-id="3e30e-205">Right-click the entry for the virtual machine in the left pane, and then select **Edit Settings**.</span></span>

3. <span data-ttu-id="3e30e-206">Selecteer de **opties** tabblad.</span><span class="sxs-lookup"><span data-stu-id="3e30e-206">Select the **Options** tab.</span></span>

4. <span data-ttu-id="3e30e-207">Selecteer in het linkerdeelvenster **Geavanceerd** > **algemene**, en selecteer vervolgens de **configuratieparameters** knop in het gedeelte rechts van het scherm.</span><span class="sxs-lookup"><span data-stu-id="3e30e-207">In the left pane, select **Advanced** > **General**, and then select the **Configuration Parameters** button on the lower-right part of the screen.</span></span>

    ![Tabblad Opties](./media/site-recovery-how-to-install-linux-master-target/media/image20.png)

    <span data-ttu-id="3e30e-209">De **configuratieparameters** optie is niet beschikbaar wanneer de machine wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="3e30e-209">The **Configuration Parameters** option is not available when the machine is running.</span></span> <span data-ttu-id="3e30e-210">Sluit de virtuele machine om op dit tabblad te activeren.</span><span class="sxs-lookup"><span data-stu-id="3e30e-210">To make this tab active, shut down the virtual machine.</span></span>

5. <span data-ttu-id="3e30e-211">Zie of een rij met **schijf. EnableUUID** bestaat al.</span><span class="sxs-lookup"><span data-stu-id="3e30e-211">See whether a row with **disk.EnableUUID** already exists.</span></span>

    - <span data-ttu-id="3e30e-212">Als de waarde bestaat en is ingesteld op **False**, wijzig de waarde in **True**.</span><span class="sxs-lookup"><span data-stu-id="3e30e-212">If the value exists and is set to **False**, change the value to **True**.</span></span> <span data-ttu-id="3e30e-213">(De waarden zijn niet hoofdlettergevoelig).</span><span class="sxs-lookup"><span data-stu-id="3e30e-213">(The values are not case-sensitive.)</span></span>

    - <span data-ttu-id="3e30e-214">Als de waarde bestaat en is ingesteld op **True**, selecteer **annuleren**.</span><span class="sxs-lookup"><span data-stu-id="3e30e-214">If the value exists and is set to **True**, select **Cancel**.</span></span>

    - <span data-ttu-id="3e30e-215">Als de waarde niet bestaat, selecteert u **rij toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="3e30e-215">If the value does not exist, select **Add Row**.</span></span>

    - <span data-ttu-id="3e30e-216">Voeg in de naamkolom **schijf. EnableUUID**, en stel de waarde op **TRUE**.</span><span class="sxs-lookup"><span data-stu-id="3e30e-216">In the name column, add **disk.EnableUUID**, and then set the value to **TRUE**.</span></span>

    ![Controleren of schijf. Er bestaat al een EnableUUID](./media/site-recovery-how-to-install-linux-master-target/media/image21.png)

#### <a name="disable-kernel-upgrades"></a><span data-ttu-id="3e30e-218">Kernel-upgrades uitschakelen</span><span class="sxs-lookup"><span data-stu-id="3e30e-218">Disable kernel upgrades</span></span>

<span data-ttu-id="3e30e-219">Azure Site Recovery-hoofddoelserver vereist een specifieke versie van de Ubuntu, zorg ervoor dat de kernel-upgrades voor de virtuele machine zijn uitgeschakeld.</span><span class="sxs-lookup"><span data-stu-id="3e30e-219">Azure Site Recovery master target server requires a very specific version of the Ubuntu, ensure that the kernel upgrades are disabled for the virtual machine.</span></span>

<span data-ttu-id="3e30e-220">Als upgrades van de kernel zijn ingeschakeld, dan eventuele upgrades voor reguliere voor zorgen dat de hoofddoelserver is niet goed.</span><span class="sxs-lookup"><span data-stu-id="3e30e-220">If kernel upgrades are enabled, then any regular upgrades cause the master target server to malfunction.</span></span>

#### <a name="download-and-install-additional-packages"></a><span data-ttu-id="3e30e-221">Extra pakketten downloaden en installeren</span><span class="sxs-lookup"><span data-stu-id="3e30e-221">Download and install additional packages</span></span>

> [!NOTE]
> <span data-ttu-id="3e30e-222">Zorg ervoor dat er verbinding met Internet te downloaden en installeren van extra pakketten.</span><span class="sxs-lookup"><span data-stu-id="3e30e-222">Make sure that you have Internet connectivity to download and install additional packages.</span></span> <span data-ttu-id="3e30e-223">Als u geen verbinding met Internet, moet u handmatig deze RPM-pakketten zoeken en te installeren.</span><span class="sxs-lookup"><span data-stu-id="3e30e-223">If you don't have Internet connectivity, you need to manually find these RPM packages and install them.</span></span>

```
apt-get install -y multipath-tools lsscsi python-pyasn1 lvm2 kpartx
```

### <a name="get-the-installer-for-setup"></a><span data-ttu-id="3e30e-224">Ophalen van het installatieprogramma voor installatie</span><span class="sxs-lookup"><span data-stu-id="3e30e-224">Get the installer for setup</span></span>

<span data-ttu-id="3e30e-225">Als uw hoofddoel verbinding met Internet heeft, kunt u de volgende stappen uit voor het downloaden van het installatieprogramma.</span><span class="sxs-lookup"><span data-stu-id="3e30e-225">If your master target has Internet connectivity, you can use the following steps to download the installer.</span></span> <span data-ttu-id="3e30e-226">U kunt anders kopiëren van het installatieprogramma van de processerver en u deze vervolgens installeren.</span><span class="sxs-lookup"><span data-stu-id="3e30e-226">Otherwise, you can copy the installer from the process server and then install it.</span></span>

#### <a name="download-the-master-target-installation-packages"></a><span data-ttu-id="3e30e-227">De installatiepakketten hoofddoel downloaden</span><span class="sxs-lookup"><span data-stu-id="3e30e-227">Download the master target installation packages</span></span>

<span data-ttu-id="3e30e-228">[Download de meest recente Linux-hoofddoel installatie bits](https://aka.ms/latestlinuxmobsvc).</span><span class="sxs-lookup"><span data-stu-id="3e30e-228">[Download the latest Linux master target installation bits](https://aka.ms/latestlinuxmobsvc).</span></span>

<span data-ttu-id="3e30e-229">Als u wilt downloaden met behulp van Linux, typt u:</span><span class="sxs-lookup"><span data-stu-id="3e30e-229">To download it by using Linux, type:</span></span>

```
wget https://aka.ms/latestlinuxmobsvc -O latestlinuxmobsvc.tar.gz
```

<span data-ttu-id="3e30e-230">Zorg ervoor dat u downloaden en uitpakken van het installatieprogramma in de basismap.</span><span class="sxs-lookup"><span data-stu-id="3e30e-230">Make sure that you download and unzip the installer in your home directory.</span></span> <span data-ttu-id="3e30e-231">Als u naar uitpakken **/usr/Local**, zal de installatie mislukken.</span><span class="sxs-lookup"><span data-stu-id="3e30e-231">If you unzip to **/usr/Local**, then the installation  fails.</span></span>


#### <a name="access-the-installer-from-the-process-server"></a><span data-ttu-id="3e30e-232">Toegang tot het installatieprogramma vanaf de processerver</span><span class="sxs-lookup"><span data-stu-id="3e30e-232">Access the installer from the process server</span></span>

1. <span data-ttu-id="3e30e-233">Ga op de processerver naar **C:\Program Files (x86) \Microsoft Azure Site Recovery\home\svsystems\pushinstallsvc\repository**.</span><span class="sxs-lookup"><span data-stu-id="3e30e-233">On the process server, go to **C:\Program Files (x86)\Microsoft Azure Site Recovery\home\svsystems\pushinstallsvc\repository**.</span></span>

2. <span data-ttu-id="3e30e-234">Kopieer het vereiste installer-bestand van de processerver en sla het bestand als **latestlinuxmobsvc.tar.gz** in de basismap.</span><span class="sxs-lookup"><span data-stu-id="3e30e-234">Copy the required installer file from the process server, and save it as **latestlinuxmobsvc.tar.gz** in your home directory.</span></span>


### <a name="apply-custom-configuration-changes"></a><span data-ttu-id="3e30e-235">Aangepaste configuratiewijzigingen toepassen</span><span class="sxs-lookup"><span data-stu-id="3e30e-235">Apply custom configuration changes</span></span>

<span data-ttu-id="3e30e-236">Aangepaste configuratiewijzigingen wilt toepassen, gebruikt u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="3e30e-236">To apply custom configuration changes, use the following steps:</span></span>


1. <span data-ttu-id="3e30e-237">Voer de volgende opdracht om het binaire bestand untar.</span><span class="sxs-lookup"><span data-stu-id="3e30e-237">Run the following command to untar the binary.</span></span>
    ```
    tar -zxvf latestlinuxmobsvc.tar.gz
    ```
    ![Schermafbeelding van de opdracht uitvoeren](./media/site-recovery-how-to-install-linux-master-target/image16.png)

2. <span data-ttu-id="3e30e-239">Voer de volgende opdracht om toestemming te geven.</span><span class="sxs-lookup"><span data-stu-id="3e30e-239">Run the following command to give permission.</span></span>
    ```
    chmod 755 ./ApplyCustomChanges.sh
    ```

3. <span data-ttu-id="3e30e-240">Voer de volgende opdracht het script uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="3e30e-240">Run the following command to run the script.</span></span>
    ```
    ./ApplyCustomChanges.sh
    ```
> [!NOTE]
> <span data-ttu-id="3e30e-241">Voer het script slechts eenmaal op de server.</span><span class="sxs-lookup"><span data-stu-id="3e30e-241">Run the script only once on the server.</span></span> <span data-ttu-id="3e30e-242">De server afsluiten.</span><span class="sxs-lookup"><span data-stu-id="3e30e-242">Shut down the server.</span></span> <span data-ttu-id="3e30e-243">De server opnieuw opstarten nadat u een schijf toevoegen zoals beschreven in de volgende sectie.</span><span class="sxs-lookup"><span data-stu-id="3e30e-243">Then restart the server after you add a disk, as described in the next section.</span></span>

### <a name="add-a-retention-disk-to-the-linux-master-target-virtual-machine"></a><span data-ttu-id="3e30e-244">Een bewaarperiode schijf toevoegen aan de Linux-hoofddoel virtuele machine</span><span class="sxs-lookup"><span data-stu-id="3e30e-244">Add a retention disk to the Linux master target virtual machine</span></span>

<span data-ttu-id="3e30e-245">Gebruik de volgende stappen voor het maken van een schijf bewaren:</span><span class="sxs-lookup"><span data-stu-id="3e30e-245">Use the following steps to create a retention disk:</span></span>

1. <span data-ttu-id="3e30e-246">Koppelen van een nieuwe schijf van 1 TB aan de Linux-hoofddoel virtuele machine en de machine start.</span><span class="sxs-lookup"><span data-stu-id="3e30e-246">Attach a new 1-TB disk to the Linux master target virtual machine, and then start the machine.</span></span>

2. <span data-ttu-id="3e30e-247">Gebruik de **multipath -lle** opdracht voor meer informatie over de multipath-ID van de schijf bewaren.</span><span class="sxs-lookup"><span data-stu-id="3e30e-247">Use the **multipath -ll** command to learn the multipath ID of the retention disk.</span></span>

    ```
    multipath -ll
    ```
    ![De multipath-ID van de retentie-schijf](./media/site-recovery-how-to-install-linux-master-target/media/image22.png)

3. <span data-ttu-id="3e30e-249">Formatteren van de schijf en maak vervolgens een bestandssysteem op het nieuwe station.</span><span class="sxs-lookup"><span data-stu-id="3e30e-249">Format the drive, and then create a file system on the new drive.</span></span>

    ```
    mkfs.ext4 /dev/mapper/<Retention disk's multipath id>
    ```
    ![Een bestandssysteem maken op het station](./media/site-recovery-how-to-install-linux-master-target/media/image23.png)

4. <span data-ttu-id="3e30e-251">Nadat u het bestandssysteem gemaakt, moet u de bewaarperiode schijf koppelen.</span><span class="sxs-lookup"><span data-stu-id="3e30e-251">After you create the file system, mount the retention disk.</span></span>
    ```
    mkdir /mnt/retention
    mount /dev/mapper/<Retention disk's multipath id> /mnt/retention
    ```
    ![De retentie-schijf koppelen](./media/site-recovery-how-to-install-linux-master-target/media/image24.png)

5. <span data-ttu-id="3e30e-253">Maak de **fstab** vermelding koppelen van het bewaarstation telkens wanneer het systeem wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="3e30e-253">Create the **fstab** entry to mount the retention drive every time the system starts.</span></span>
    ```
    vi /etc/fstab
    ```
    <span data-ttu-id="3e30e-254">Selecteer **invoegen** om te beginnen met het bewerken van het bestand.</span><span class="sxs-lookup"><span data-stu-id="3e30e-254">Select **Insert** to begin editing the file.</span></span> <span data-ttu-id="3e30e-255">Maak een nieuwe regel en voeg vervolgens de volgende tekst.</span><span class="sxs-lookup"><span data-stu-id="3e30e-255">Create a new line, and then insert the following text.</span></span> <span data-ttu-id="3e30e-256">De schijf multipath-ID op basis van de gemarkeerde multipath-ID van de vorige opdracht bewerken.</span><span class="sxs-lookup"><span data-stu-id="3e30e-256">Edit the disk multipath ID based on the highlighted multipath ID from the previous command.</span></span>

    <span data-ttu-id="3e30e-257"> **/dev/mapper/ <Retention disks multipath id> /mnt/bewaren ext4 rw 0 0**</span><span class="sxs-lookup"><span data-stu-id="3e30e-257">**/dev/mapper/<Retention disks multipath id> /mnt/retention ext4 rw 0 0**</span></span>

    <span data-ttu-id="3e30e-258">Selecteer **Esc**, en typ vervolgens **: wq** (schrijven en sluiten) het editorvenster te sluiten.</span><span class="sxs-lookup"><span data-stu-id="3e30e-258">Select **Esc**, and then type **:wq** (write and quit) to close the editor window.</span></span>

### <a name="install-the-master-target"></a><span data-ttu-id="3e30e-259">Het hoofddoel installeren</span><span class="sxs-lookup"><span data-stu-id="3e30e-259">Install the master target</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3e30e-260">De versie van de hoofddoelserver moet gelijk zijn aan of ouder is dan de versies van de processerver en de configuratieserver.</span><span class="sxs-lookup"><span data-stu-id="3e30e-260">The version of the master target server must be equal to or earlier than the versions of the process server and the configuration server.</span></span> <span data-ttu-id="3e30e-261">Als dit probleem niet wordt voldaan, beveiligt is geslaagd, maar mislukt de replicatie.</span><span class="sxs-lookup"><span data-stu-id="3e30e-261">If this condition is not met, reprotect succeeds, but replication fails.</span></span>


> [!NOTE]
> <span data-ttu-id="3e30e-262">Voordat u de hoofddoelserver installeert, Controleer of de **/etc/hosts** -bestand op de virtuele machine bevat items die de lokale hostnaam worden toegewezen aan de IP-adressen die gekoppeld aan alle netwerkadapters zijn.</span><span class="sxs-lookup"><span data-stu-id="3e30e-262">Before you install the master target server, check that the **/etc/hosts** file on the virtual machine contains entries that map the local hostname to the IP addresses that are associated with all network adapters.</span></span>

1. <span data-ttu-id="3e30e-263">Kopieer de wachtwoordzin van **C:\ProgramData\Microsoft Azure Site Recovery\private\connection.passphrase** op de configuratieserver.</span><span class="sxs-lookup"><span data-stu-id="3e30e-263">Copy the passphrase from **C:\ProgramData\Microsoft Azure Site Recovery\private\connection.passphrase** on the configuration server.</span></span> <span data-ttu-id="3e30e-264">Sla het als **passphrase.txt** in dezelfde lokale map met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="3e30e-264">Then save it as **passphrase.txt** in the same local directory by running the following command:</span></span>

    ```
    echo <passphrase> >passphrase.txt
    ```
    <span data-ttu-id="3e30e-265">Voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="3e30e-265">Example:</span></span> 
    
    ```
    echo itUx70I47uxDuUVY >passphrase.txt
    ```

2. <span data-ttu-id="3e30e-266">Noteer de configuratieserver IP-adres.</span><span class="sxs-lookup"><span data-stu-id="3e30e-266">Note the configuration server's IP address.</span></span> <span data-ttu-id="3e30e-267">U moet deze in de volgende stap.</span><span class="sxs-lookup"><span data-stu-id="3e30e-267">You need it in the next step.</span></span>

3. <span data-ttu-id="3e30e-268">Voer de volgende opdracht voor het installeren van de hoofddoelserver en de server geregistreerd met de configuratieserver.</span><span class="sxs-lookup"><span data-stu-id="3e30e-268">Run the following command to install the master target server and register the server with the configuration server.</span></span>

    ```
    ./install -q -d /usr/local/ASR -r MT -v VmWare
    /usr/local/ASR/Vx/bin/UnifiedAgentConfigurator.sh -i <ConfigurationServer IP Address> -P passphrase.txt
    ```

    <span data-ttu-id="3e30e-269">Voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="3e30e-269">Example:</span></span> 
    
    ```
    /usr/local/ASR/Vx/bin/UnifiedAgentConfigurator.sh -i 104.40.75.37 -P passphrase.txt
    ```

    <span data-ttu-id="3e30e-270">Wacht totdat het script is voltooid.</span><span class="sxs-lookup"><span data-stu-id="3e30e-270">Wait until the script finishes.</span></span> <span data-ttu-id="3e30e-271">Als het hoofddoel wordt geregistreerd is, het hoofddoel wordt weergegeven op de **Site Recovery-infrastructuur** pagina van de portal.</span><span class="sxs-lookup"><span data-stu-id="3e30e-271">If the master target registers sucessfully, the master target is listed on the **Site Recovery Infrastructure** page of the portal.</span></span>


#### <a name="install-the-master-target-by-using-interactive-installation"></a><span data-ttu-id="3e30e-272">Het hoofddoel installeren met behulp van interactieve installatie</span><span class="sxs-lookup"><span data-stu-id="3e30e-272">Install the master target by using interactive installation</span></span>

1. <span data-ttu-id="3e30e-273">Voer de volgende opdracht voor het installeren van het hoofddoel.</span><span class="sxs-lookup"><span data-stu-id="3e30e-273">Run the following command to install the master target.</span></span> <span data-ttu-id="3e30e-274">Kies voor de rol agent **hoofddoel**.</span><span class="sxs-lookup"><span data-stu-id="3e30e-274">For the agent role, choose **Master Target**.</span></span>

    ```
    ./install
    ```

2. <span data-ttu-id="3e30e-275">Kies de standaardlocatie voor installatie en selecteer vervolgens **Enter** om door te gaan.</span><span class="sxs-lookup"><span data-stu-id="3e30e-275">Choose the default location for installation, and then select **Enter** to continue.</span></span>

    ![Een standaardlocatie voor installatie van het hoofddoel kiezen](./media/site-recovery-how-to-install-linux-master-target/image17.png)

<span data-ttu-id="3e30e-277">Nadat de installatie is voltooid, moet u de configuratieserver registreren met behulp van de opdrachtregel.</span><span class="sxs-lookup"><span data-stu-id="3e30e-277">After the installation has finished, register the configuration server by using the command line.</span></span>

1. <span data-ttu-id="3e30e-278">Noteer de IP-adres van de configuratieserver.</span><span class="sxs-lookup"><span data-stu-id="3e30e-278">Note the IP address of the configuration server.</span></span> <span data-ttu-id="3e30e-279">U moet deze in de volgende stap.</span><span class="sxs-lookup"><span data-stu-id="3e30e-279">You need it in the next step.</span></span>

2. <span data-ttu-id="3e30e-280">Voer de volgende opdracht voor het installeren van de hoofddoelserver en de server geregistreerd met de configuratieserver.</span><span class="sxs-lookup"><span data-stu-id="3e30e-280">Run the following command to install the master target server and register the server with the configuration server.</span></span>

    ```
    ./install -q -d /usr/local/ASR -r MT -v VmWare
    /usr/local/ASR/Vx/bin/UnifiedAgentConfigurator.sh -i <ConfigurationServer IP Address> -P passphrase.txt
    ```
    <span data-ttu-id="3e30e-281">Voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="3e30e-281">Example:</span></span> 

    ```
    /usr/local/ASR/Vx/bin/UnifiedAgentConfigurator.sh -i 104.40.75.37 -P passphrase.txt
    ```

   <span data-ttu-id="3e30e-282">Wacht totdat het script is voltooid.</span><span class="sxs-lookup"><span data-stu-id="3e30e-282">Wait until the script finishes.</span></span> <span data-ttu-id="3e30e-283">Als het hoofddoel geregistreerd met succes is is, het hoofddoel wordt weergegeven op de **Site Recovery-infrastructuur** pagina van de portal.</span><span class="sxs-lookup"><span data-stu-id="3e30e-283">If the master target is registered succesfully, the master target is listed on the **Site Recovery Infrastructure** page of the portal.</span></span>


### <a name="upgrade-the-master-target"></a><span data-ttu-id="3e30e-284">Het hoofddoel upgraden</span><span class="sxs-lookup"><span data-stu-id="3e30e-284">Upgrade the master target</span></span>

<span data-ttu-id="3e30e-285">Het installatieprogramma uitvoert.</span><span class="sxs-lookup"><span data-stu-id="3e30e-285">Run the installer.</span></span> <span data-ttu-id="3e30e-286">Automatisch wordt gedetecteerd dat de agent is geïnstalleerd op het hoofddoel.</span><span class="sxs-lookup"><span data-stu-id="3e30e-286">It automatically detects that the agent is installed on the master target.</span></span> <span data-ttu-id="3e30e-287">Als u wilt bijwerken, selecteert u **Y**.  Nadat de installatie is voltooid, controleert u de versie van het hoofddoel geïnstalleerd met behulp van de volgende opdracht.</span><span class="sxs-lookup"><span data-stu-id="3e30e-287">To upgrade, select **Y**.  After the setup has been completed, check the version of the master target installed by using the following command.</span></span>

    ```
    cat /usr/local/.vx_version
    ```

<span data-ttu-id="3e30e-288">Kunt u zien dat de **versie** veld kunt u het versienummer van het hoofddoel.</span><span class="sxs-lookup"><span data-stu-id="3e30e-288">You can see that the **Version** field gives the version number of the master target.</span></span>

### <a name="install-vmware-tools-on-the-master-target-server"></a><span data-ttu-id="3e30e-289">Installeer VMware tools op de hoofddoelserver</span><span class="sxs-lookup"><span data-stu-id="3e30e-289">Install VMware tools on the master target server</span></span>

<span data-ttu-id="3e30e-290">U moet VMware tools installeren op het hoofddoel zodat deze de gegevensarchieven kan detecteren.</span><span class="sxs-lookup"><span data-stu-id="3e30e-290">You need to install VMware tools on the master target so that it can discover the data stores.</span></span> <span data-ttu-id="3e30e-291">Als de hulpprogramma's zijn niet geïnstalleerd, wordt het scherm beveiligt niet vermeld in de gegevensarchieven.</span><span class="sxs-lookup"><span data-stu-id="3e30e-291">If the tools are not installed, the reprotect screen isn't listed in the data stores.</span></span> <span data-ttu-id="3e30e-292">Na installatie van de VMware-hulpprogramma's moet u opnieuw opstarten.</span><span class="sxs-lookup"><span data-stu-id="3e30e-292">After installation of the VMware tools, you need to restart.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3e30e-293">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="3e30e-293">Next steps</span></span>
<span data-ttu-id="3e30e-294">Nadat de installatie en registratie van het hoofddoel heeft finsihed, ziet u het hoofddoel worden weergegeven op de **hoofddoel** in sectie **Site Recovery-infrastructuur**, onder de configuratie overzicht van de server.</span><span class="sxs-lookup"><span data-stu-id="3e30e-294">After the installation and registration of the master target has finsihed, you can see the master target appear on the **Master Target** section in **Site Recovery Infrastructure**, under the configuration server overview.</span></span>

<span data-ttu-id="3e30e-295">U kunt nu doorgaan met [beveiligingspoging](site-recovery-how-to-reprotect.md), gevolgd door de failback.</span><span class="sxs-lookup"><span data-stu-id="3e30e-295">You can now proceed with [reprotection](site-recovery-how-to-reprotect.md), followed by failback.</span></span>

## <a name="common-issues"></a><span data-ttu-id="3e30e-296">Algemene problemen</span><span class="sxs-lookup"><span data-stu-id="3e30e-296">Common issues</span></span>

* <span data-ttu-id="3e30e-297">Zorg ervoor dat u inschakelt Storage vMotion op eventuele management-onderdelen, zoals een hoofddoel.</span><span class="sxs-lookup"><span data-stu-id="3e30e-297">Make sure you do not turn on Storage vMotion on any management components such as a master target.</span></span> <span data-ttu-id="3e30e-298">Als het hoofddoel na een geslaagde beveiligt wordt, kan de virtuele machine-schijven (VMDKs) kunnen niet worden losgekoppeld.</span><span class="sxs-lookup"><span data-stu-id="3e30e-298">If the master target moves after a successful reprotect, the virtual machine disks (VMDKs) cannot be detached.</span></span> <span data-ttu-id="3e30e-299">In dit geval failback is mislukt.</span><span class="sxs-lookup"><span data-stu-id="3e30e-299">In this case, failback fails.</span></span>

* <span data-ttu-id="3e30e-300">Het hoofddoel mag geen eventuele momentopnamen op de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="3e30e-300">The master target should not have any snapshots on the virtual machine.</span></span> <span data-ttu-id="3e30e-301">Als momentopnamen bevat, mislukt de failback.</span><span class="sxs-lookup"><span data-stu-id="3e30e-301">If there are snapshots, failback fails.</span></span>

* <span data-ttu-id="3e30e-302">De netwerkinterface tijdens het opstarten is uitgeschakeld als gevolg van een aantal aangepaste configuraties voor NIC op sommige klanten en de hoofddoelserver-agent kan niet worden geïnitialiseerd.</span><span class="sxs-lookup"><span data-stu-id="3e30e-302">Due to some custom NIC configurations at some customers, the network interface is disabled during startup, and the master target agent cannot initialize.</span></span> <span data-ttu-id="3e30e-303">Zorg ervoor dat de volgende eigenschappen correct zijn ingesteld.</span><span class="sxs-lookup"><span data-stu-id="3e30e-303">Make sure that the following properties are correctly set.</span></span> <span data-ttu-id="3e30e-304">Controleer deze eigenschappen in de Ethernet-kaart van het bestand /etc/sysconfig/network-scripts/ifcfg-eth *.</span><span class="sxs-lookup"><span data-stu-id="3e30e-304">Check these properties in the Ethernet card file's /etc/sysconfig/network-scripts/ifcfg-eth*.</span></span>
    * <span data-ttu-id="3e30e-305">BOOTPROTO = dhcp</span><span class="sxs-lookup"><span data-stu-id="3e30e-305">BOOTPROTO=dhcp</span></span>
    * <span data-ttu-id="3e30e-306">ONBOOT = yes</span><span class="sxs-lookup"><span data-stu-id="3e30e-306">ONBOOT=yes</span></span>

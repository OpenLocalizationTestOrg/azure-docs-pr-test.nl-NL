---
title: aaaUpdate hello Azure Linux Agent vanuit GitHub | Microsoft Docs
description: Meer informatie over hoe tooupdate Azure Linux Agent voor uw Linux-VM in Azure toohello meest recente versie van GitHub
services: virtual-machines-linux
documentationcenter: 
author: SuperScottz
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: f1f19300-987d-4f29-9393-9aba866f049c
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: mingzhan
ms.openlocfilehash: 4ce7c56efc1e6563e6415f7687573f9fb9e7b4c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooupdate-hello-azure-linux-agent-on-a-vm"></a><span data-ttu-id="42a38-103">Hoe tooupdate hello Azure Linux Agent op een virtuele machine</span><span class="sxs-lookup"><span data-stu-id="42a38-103">How tooupdate hello Azure Linux Agent on a VM</span></span>

<span data-ttu-id="42a38-104">tooupdate uw [Azure Linux Agent](https://github.com/Azure/WALinuxAgent) op een Linux-VM in Azure, moet u al hebben:</span><span class="sxs-lookup"><span data-stu-id="42a38-104">tooupdate your [Azure Linux Agent](https://github.com/Azure/WALinuxAgent) on a Linux VM in Azure, you must already have:</span></span>

- <span data-ttu-id="42a38-105">Een actieve Linux VM in Azure.</span><span class="sxs-lookup"><span data-stu-id="42a38-105">A running Linux VM in Azure.</span></span>
- <span data-ttu-id="42a38-106">Een verbinding toothat Linux VM via SSH.</span><span class="sxs-lookup"><span data-stu-id="42a38-106">A connection toothat Linux VM using SSH.</span></span>

<span data-ttu-id="42a38-107">U moet altijd eerst in voor een pakket in Hallo Linux distro opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="42a38-107">You should always check for a package in hello Linux distro repository first.</span></span> <span data-ttu-id="42a38-108">Het is mogelijk Hallo pakket beschikbaar mogelijk niet de nieuwste versie Hallo, echter inschakelen autoupdate waarborgt Hallo Linux-Agent altijd de meest recente update Hallo krijgen.</span><span class="sxs-lookup"><span data-stu-id="42a38-108">It is possible hello package available may not be hello latest version, however, enabling autoupdate will ensure hello Linux Agent will always get hello latest update.</span></span> <span data-ttu-id="42a38-109">Hebt u problemen met het installeren van Hallo pakket managers, moet u ondersteuning van Hallo distro leverancier zoeken.</span><span class="sxs-lookup"><span data-stu-id="42a38-109">Should you have issues installing from hello package managers, you should seek support from hello distro vendor.</span></span>

## <a name="updating-hello-azure-linux-agent"></a><span data-ttu-id="42a38-110">Hello Azure Linux Agent bijwerken</span><span class="sxs-lookup"><span data-stu-id="42a38-110">Updating hello Azure Linux Agent</span></span>

## <a name="ubuntu"></a><span data-ttu-id="42a38-111">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="42a38-111">Ubuntu</span></span>

#### <a name="check-your-current-package-version"></a><span data-ttu-id="42a38-112">Controleer uw huidige Pakketversie</span><span class="sxs-lookup"><span data-stu-id="42a38-112">Check your current package version</span></span>

```bash
apt list --installed | grep walinuxagent
```

#### <a name="update-package-cache"></a><span data-ttu-id="42a38-113">Update-pakket-cache</span><span class="sxs-lookup"><span data-stu-id="42a38-113">Update package cache</span></span>

```bash
sudo apt-get -qq update
```

#### <a name="install-hello-latest-package-version"></a><span data-ttu-id="42a38-114">Installeer de meest recente Pakketversie Hallo</span><span class="sxs-lookup"><span data-stu-id="42a38-114">Install hello latest package version</span></span>

```bash
sudo apt-get install walinuxagent
```

#### <a name="ensure-auto-update-is-enabled"></a><span data-ttu-id="42a38-115">Zorg ervoor dat automatische updates is ingeschakeld</span><span class="sxs-lookup"><span data-stu-id="42a38-115">Ensure auto update is enabled</span></span>

<span data-ttu-id="42a38-116">Controleer eerst toosee als deze is ingeschakeld:</span><span class="sxs-lookup"><span data-stu-id="42a38-116">First, check toosee if it is enabled:</span></span>

```bash
cat /etc/waagent.conf
```

<span data-ttu-id="42a38-117">'AutoUpdate.Enabled' vinden.</span><span class="sxs-lookup"><span data-stu-id="42a38-117">Find 'AutoUpdate.Enabled'.</span></span> <span data-ttu-id="42a38-118">Als u deze uitvoer ziet, is het ingeschakeld:</span><span class="sxs-lookup"><span data-stu-id="42a38-118">If you see this output, it is enabled:</span></span>

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

<span data-ttu-id="42a38-119">tooenable uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="42a38-119">tooenable run:</span></span>

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="restart-hello-waagent-service"></a><span data-ttu-id="42a38-120">Hallo waagent-service opnieuw starten</span><span class="sxs-lookup"><span data-stu-id="42a38-120">Restart hello waagent service</span></span>

#### <a name="restart-agent-for-1404"></a><span data-ttu-id="42a38-121">Agent opnieuw starten om 14.04</span><span class="sxs-lookup"><span data-stu-id="42a38-121">Restart agent for 14.04</span></span>

```bash
initctl restart walinuxagent
```

#### <a name="restart-agent-for-1604--1704"></a><span data-ttu-id="42a38-122">Agent opnieuw starten om 16.04 / 17.04</span><span class="sxs-lookup"><span data-stu-id="42a38-122">Restart agent for 16.04 / 17.04</span></span>

```bash
systemctl restart walinuxagent.service
```

## <a name="debian"></a><span data-ttu-id="42a38-123">Debian</span><span class="sxs-lookup"><span data-stu-id="42a38-123">Debian</span></span>

### <a name="debian-7-wheezy"></a><span data-ttu-id="42a38-124">Debian 7 'Wheezy'</span><span class="sxs-lookup"><span data-stu-id="42a38-124">Debian 7 “Wheezy”</span></span>

#### <a name="check-your-current-package-version"></a><span data-ttu-id="42a38-125">Controleer uw huidige Pakketversie</span><span class="sxs-lookup"><span data-stu-id="42a38-125">Check your current package version</span></span>

```bash
dpkg -l | grep waagent
```

#### <a name="update-package-cache"></a><span data-ttu-id="42a38-126">Update-pakket-cache</span><span class="sxs-lookup"><span data-stu-id="42a38-126">Update package cache</span></span>

```bash
sudo apt-get -qq update
```

#### <a name="install-hello-latest-package-version"></a><span data-ttu-id="42a38-127">Installeer de meest recente Pakketversie Hallo</span><span class="sxs-lookup"><span data-stu-id="42a38-127">Install hello latest package version</span></span>

```bash
sudo apt-get install waagent
```

#### <a name="enable-agent-auto-update"></a><span data-ttu-id="42a38-128">Agent automatisch bijwerken inschakelen</span><span class="sxs-lookup"><span data-stu-id="42a38-128">Enable agent auto update</span></span>
<span data-ttu-id="42a38-129">Deze versie van Debian beschikt niet over een versie > = 2.0.16, automatisch bijwerken is daarom niet beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="42a38-129">This version of Debian does not have a version >= 2.0.16, therefore AutoUpdate is not available for it.</span></span> <span data-ttu-id="42a38-130">Hallo-uitvoer van Hallo hierboven opdracht ziet u als Hallo-pakket bijgewerkt is.</span><span class="sxs-lookup"><span data-stu-id="42a38-130">hello output from hello above command will show you if hello package is up-to-date.</span></span>

### <a name="debian-8-jessie--debian-9-stretch"></a><span data-ttu-id="42a38-131">Debian 8 'Jessie' / Debian 9 'Stretch'</span><span class="sxs-lookup"><span data-stu-id="42a38-131">Debian 8 “Jessie” / Debian 9 “Stretch”</span></span>

#### <a name="check-your-current-package-version"></a><span data-ttu-id="42a38-132">Controleer uw huidige Pakketversie</span><span class="sxs-lookup"><span data-stu-id="42a38-132">Check your current package version</span></span>

```bash
apt list --installed | grep walinuxagent
```

#### <a name="update-package-cache"></a><span data-ttu-id="42a38-133">Update-pakket-cache</span><span class="sxs-lookup"><span data-stu-id="42a38-133">Update package cache</span></span>

```bash
sudo apt-get -qq update
```

#### <a name="install-hello-latest-package-version"></a><span data-ttu-id="42a38-134">Installeer de meest recente Pakketversie Hallo</span><span class="sxs-lookup"><span data-stu-id="42a38-134">Install hello latest package version</span></span>

```bash
sudo apt-get install waagent
```
#### <a name="ensure-auto-update-is-enabled"></a><span data-ttu-id="42a38-135">Zorg ervoor dat automatische updates is ingeschakeld</span><span class="sxs-lookup"><span data-stu-id="42a38-135">Ensure auto update is enabled</span></span> 

<span data-ttu-id="42a38-136">Controleer eerst toosee als deze is ingeschakeld:</span><span class="sxs-lookup"><span data-stu-id="42a38-136">First, check toosee if it is enabled:</span></span>

```bash
cat /etc/waagent.conf
```

<span data-ttu-id="42a38-137">'AutoUpdate.Enabled' vinden.</span><span class="sxs-lookup"><span data-stu-id="42a38-137">Find 'AutoUpdate.Enabled'.</span></span> <span data-ttu-id="42a38-138">Als u deze uitvoer ziet, is het ingeschakeld:</span><span class="sxs-lookup"><span data-stu-id="42a38-138">If you see this output, it is enabled:</span></span>

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

<span data-ttu-id="42a38-139">tooenable uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="42a38-139">tooenable run:</span></span>

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="restart-hello-waagent-service"></a><span data-ttu-id="42a38-140">Hallo waagent-service opnieuw starten</span><span class="sxs-lookup"><span data-stu-id="42a38-140">Restart hello waagent service</span></span>

```
sudo systemctl restart walinuxagent.service
```

## <a name="redhat--centos"></a><span data-ttu-id="42a38-141">RedHat / CentOS</span><span class="sxs-lookup"><span data-stu-id="42a38-141">Redhat / CentOS</span></span>

### <a name="rhelcentos-6"></a><span data-ttu-id="42a38-142">RHEL/CentOS 6</span><span class="sxs-lookup"><span data-stu-id="42a38-142">RHEL/CentOS 6</span></span>

#### <a name="check-your-current-package-version"></a><span data-ttu-id="42a38-143">Controleer uw huidige Pakketversie</span><span class="sxs-lookup"><span data-stu-id="42a38-143">Check your current package version</span></span>

```bash
sudo yum list WALinuxAgent
```

#### <a name="check-available-updates"></a><span data-ttu-id="42a38-144">Beschikbare updates controleren</span><span class="sxs-lookup"><span data-stu-id="42a38-144">Check available updates</span></span>

```bash
sudo yum check-update WALinuxAgent
```

#### <a name="install-hello-latest-package-version"></a><span data-ttu-id="42a38-145">Installeer de meest recente Pakketversie Hallo</span><span class="sxs-lookup"><span data-stu-id="42a38-145">Install hello latest package version</span></span>

```bash
sudo yum install WALinuxAgent
```

#### <a name="ensure-auto-update-is-enabled"></a><span data-ttu-id="42a38-146">Zorg ervoor dat automatische updates is ingeschakeld</span><span class="sxs-lookup"><span data-stu-id="42a38-146">Ensure auto update is enabled</span></span> 

<span data-ttu-id="42a38-147">Controleer eerst toosee als deze is ingeschakeld:</span><span class="sxs-lookup"><span data-stu-id="42a38-147">First, check toosee if it is enabled:</span></span>

```bash
cat /etc/waagent.conf
```

<span data-ttu-id="42a38-148">'AutoUpdate.Enabled' vinden.</span><span class="sxs-lookup"><span data-stu-id="42a38-148">Find 'AutoUpdate.Enabled'.</span></span> <span data-ttu-id="42a38-149">Als u deze uitvoer ziet, is het ingeschakeld:</span><span class="sxs-lookup"><span data-stu-id="42a38-149">If you see this output, it is enabled:</span></span>

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

<span data-ttu-id="42a38-150">tooenable uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="42a38-150">tooenable run:</span></span>

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="restart-hello-waagent-service"></a><span data-ttu-id="42a38-151">Hallo waagent-service opnieuw starten</span><span class="sxs-lookup"><span data-stu-id="42a38-151">Restart hello waagent service</span></span>

```
sudo service waagent restart
```

### <a name="rhelcentos-7"></a><span data-ttu-id="42a38-152">RHEL/CentOS 7</span><span class="sxs-lookup"><span data-stu-id="42a38-152">RHEL/CentOS 7</span></span>

#### <a name="check-your-current-package-version"></a><span data-ttu-id="42a38-153">Controleer uw huidige Pakketversie</span><span class="sxs-lookup"><span data-stu-id="42a38-153">Check your current package version</span></span>

```bash
sudo yum list WALinuxAgent
```

#### <a name="check-available-updates"></a><span data-ttu-id="42a38-154">Beschikbare updates controleren</span><span class="sxs-lookup"><span data-stu-id="42a38-154">Check available updates</span></span>

```bash
sudo yum check-update WALinuxAgent
```

#### <a name="install-hello-latest-package-version"></a><span data-ttu-id="42a38-155">Installeer de meest recente Pakketversie Hallo</span><span class="sxs-lookup"><span data-stu-id="42a38-155">Install hello latest package version</span></span>

```bash
sudo yum install WALinuxAgent  
```

#### <a name="ensure-auto-update-is-enabled"></a><span data-ttu-id="42a38-156">Zorg ervoor dat automatische updates is ingeschakeld</span><span class="sxs-lookup"><span data-stu-id="42a38-156">Ensure auto update is enabled</span></span> 

<span data-ttu-id="42a38-157">Controleer eerst toosee als deze is ingeschakeld:</span><span class="sxs-lookup"><span data-stu-id="42a38-157">First, check toosee if it is enabled:</span></span>

```bash
cat /etc/waagent.conf
```

<span data-ttu-id="42a38-158">'AutoUpdate.Enabled' vinden.</span><span class="sxs-lookup"><span data-stu-id="42a38-158">Find 'AutoUpdate.Enabled'.</span></span> <span data-ttu-id="42a38-159">Als u deze uitvoer ziet, is het ingeschakeld:</span><span class="sxs-lookup"><span data-stu-id="42a38-159">If you see this output, it is enabled:</span></span>

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

<span data-ttu-id="42a38-160">tooenable uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="42a38-160">tooenable run:</span></span>

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="restart-hello-waagent-service"></a><span data-ttu-id="42a38-161">Hallo waagent-service opnieuw starten</span><span class="sxs-lookup"><span data-stu-id="42a38-161">Restart hello waagent service</span></span>

```bash
sudo systemctl restart waagent.service
```

## <a name="suse-sles"></a><span data-ttu-id="42a38-162">SUSE SLES</span><span class="sxs-lookup"><span data-stu-id="42a38-162">SUSE SLES</span></span>

### <a name="suse-sles-11-sp4"></a><span data-ttu-id="42a38-163">SUSE SLES 11 SP4</span><span class="sxs-lookup"><span data-stu-id="42a38-163">SUSE SLES 11 SP4</span></span>

#### <a name="check-your-current-package-version"></a><span data-ttu-id="42a38-164">Controleer uw huidige Pakketversie</span><span class="sxs-lookup"><span data-stu-id="42a38-164">Check your current package version</span></span>

```bash
zypper info python-azure-agent
```

#### <a name="check-available-updates"></a><span data-ttu-id="42a38-165">Beschikbare updates controleren</span><span class="sxs-lookup"><span data-stu-id="42a38-165">Check available updates</span></span>

<span data-ttu-id="42a38-166">Hallo bovenstaande uitvoer ziet u als toodate Hallo-pakket is.</span><span class="sxs-lookup"><span data-stu-id="42a38-166">hello above output will show you if hello package is up toodate.</span></span>

#### <a name="install-hello-latest-package-version"></a><span data-ttu-id="42a38-167">Installeer de meest recente Pakketversie Hallo</span><span class="sxs-lookup"><span data-stu-id="42a38-167">Install hello latest package version</span></span>

```bash
sudo zypper install python-azure-agent
```

#### <a name="ensure-auto-update-is-enabled"></a><span data-ttu-id="42a38-168">Zorg ervoor dat automatische updates is ingeschakeld</span><span class="sxs-lookup"><span data-stu-id="42a38-168">Ensure auto update is enabled</span></span> 

<span data-ttu-id="42a38-169">Controleer eerst toosee als deze is ingeschakeld:</span><span class="sxs-lookup"><span data-stu-id="42a38-169">First, check toosee if it is enabled:</span></span>

```bash
cat /etc/waagent.conf
```

<span data-ttu-id="42a38-170">'AutoUpdate.Enabled' vinden.</span><span class="sxs-lookup"><span data-stu-id="42a38-170">Find 'AutoUpdate.Enabled'.</span></span> <span data-ttu-id="42a38-171">Als u deze uitvoer ziet, is het ingeschakeld:</span><span class="sxs-lookup"><span data-stu-id="42a38-171">If you see this output, it is enabled:</span></span>

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

<span data-ttu-id="42a38-172">tooenable uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="42a38-172">tooenable run:</span></span>

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="restart-hello-waagent-service"></a><span data-ttu-id="42a38-173">Hallo waagent-service opnieuw starten</span><span class="sxs-lookup"><span data-stu-id="42a38-173">Restart hello waagent service</span></span>

```bash
sudo /etc/init.d/waagent restart
```

### <a name="suse-sles-12-sp2"></a><span data-ttu-id="42a38-174">SUSE SLES 12 SP2</span><span class="sxs-lookup"><span data-stu-id="42a38-174">SUSE SLES 12 SP2</span></span>

#### <a name="check-your-current-package-version"></a><span data-ttu-id="42a38-175">Controleer uw huidige Pakketversie</span><span class="sxs-lookup"><span data-stu-id="42a38-175">Check your current package version</span></span>

```bash
zypper info python-azure-agent
```

#### <a name="check-available-updates"></a><span data-ttu-id="42a38-176">Beschikbare updates controleren</span><span class="sxs-lookup"><span data-stu-id="42a38-176">Check available updates</span></span>

<span data-ttu-id="42a38-177">In de uitvoer van de bovenstaande Hallo Hallo ziet hier u als Hallo pakket maximaal datum is.</span><span class="sxs-lookup"><span data-stu-id="42a38-177">In hello output from hello above, this will show you if hello package is upto date.</span></span>

#### <a name="install-hello-latest-package-version"></a><span data-ttu-id="42a38-178">Installeer de meest recente Pakketversie Hallo</span><span class="sxs-lookup"><span data-stu-id="42a38-178">Install hello latest package version</span></span>

```bash
sudo zypper install python-azure-agent
```

#### <a name="ensure-auto-update-is-enabled"></a><span data-ttu-id="42a38-179">Zorg ervoor dat automatische updates is ingeschakeld</span><span class="sxs-lookup"><span data-stu-id="42a38-179">Ensure auto update is enabled</span></span> 

<span data-ttu-id="42a38-180">Controleer eerst toosee als deze is ingeschakeld:</span><span class="sxs-lookup"><span data-stu-id="42a38-180">First, check toosee if it is enabled:</span></span>

```bash
cat /etc/waagent.conf
```

<span data-ttu-id="42a38-181">'AutoUpdate.Enabled' vinden.</span><span class="sxs-lookup"><span data-stu-id="42a38-181">Find 'AutoUpdate.Enabled'.</span></span> <span data-ttu-id="42a38-182">Als u deze uitvoer ziet, is het ingeschakeld:</span><span class="sxs-lookup"><span data-stu-id="42a38-182">If you see this output, it is enabled:</span></span>

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

<span data-ttu-id="42a38-183">tooenable uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="42a38-183">tooenable run:</span></span>

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="restart-hello-waagent-service"></a><span data-ttu-id="42a38-184">Hallo waagent-service opnieuw starten</span><span class="sxs-lookup"><span data-stu-id="42a38-184">Restart hello waagent service</span></span>

```bash
sudo systemctl restart waagent.service
```

## <a name="oracle-6-and-7"></a><span data-ttu-id="42a38-185">Oracle 6 en 7</span><span class="sxs-lookup"><span data-stu-id="42a38-185">Oracle 6 and 7</span></span>

<span data-ttu-id="42a38-186">Oracle Linux, zorg ervoor dat Hallo `Addons` opslagplaats is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="42a38-186">For Oracle Linux, make sure that hello `Addons` repository is enabled.</span></span> <span data-ttu-id="42a38-187">Kies tooedit Hallo bestand `/etc/yum.repos.d/public-yum-ol6.repo`(Oracle Linux 6) of `/etc/yum.repos.d/public-yum-ol7.repo`(Oracle Linux), en wijzig Hallo regel `enabled=0` te`enabled=1` onder **[ol6_addons]** of **[ol7_addons]** in dit bestand.</span><span class="sxs-lookup"><span data-stu-id="42a38-187">Choose tooedit hello file `/etc/yum.repos.d/public-yum-ol6.repo`(Oracle Linux 6) or `/etc/yum.repos.d/public-yum-ol7.repo`(Oracle Linux), and change hello line `enabled=0` too`enabled=1` under **[ol6_addons]** or **[ol7_addons]** in this file.</span></span>

<span data-ttu-id="42a38-188">Vervolgens tooinstall Hallo meest recente versie van hello Azure Linux Agent, type:</span><span class="sxs-lookup"><span data-stu-id="42a38-188">Then, tooinstall hello latest version of hello Azure Linux Agent, type:</span></span>

```bash
sudo yum install WALinuxAgent
```

<span data-ttu-id="42a38-189">Als u niet kunt Hallo invoegtoepassing opslagplaats vinden kunt u deze regels kunt gewoon op Hallo einde van uw .repo bestand volgens tooyour Oracle Linux release toevoegen:</span><span class="sxs-lookup"><span data-stu-id="42a38-189">If you don't find hello add-on repository you can simply add these lines at hello end of your .repo file according tooyour Oracle Linux release:</span></span>

<span data-ttu-id="42a38-190">Voor Oracle Linux 6 virtuele machines:</span><span class="sxs-lookup"><span data-stu-id="42a38-190">For Oracle Linux 6 virtual machines:</span></span>

```sh
[ol6_addons]
name=Add-Ons for Oracle Linux $releasever ($basearch)
baseurl=http://public-yum.oracle.com/repo/OracleLinux/OL6/addons/x86_64
gpgkey=http://public-yum.oracle.com/RPM-GPG-KEY-oracle-ol6
gpgcheck=1
enabled=1
```

<span data-ttu-id="42a38-191">Voor Oracle Linux 7 virtuele machines:</span><span class="sxs-lookup"><span data-stu-id="42a38-191">For Oracle Linux 7 virtual machines:</span></span>

```sh
[ol7_addons]
name=Oracle Linux $releasever Add ons ($basearch)
baseurl=http://public-yum.oracle.com/repo/OracleLinux/OL7/addons/$basearch/
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-oracle
gpgcheck=1
enabled=0
```

<span data-ttu-id="42a38-192">Typ vervolgens:</span><span class="sxs-lookup"><span data-stu-id="42a38-192">Then type:</span></span>

```bash
sudo yum update WALinuxAgent
```

<span data-ttu-id="42a38-193">Dit is normaal alles wat die u nodig hebt, maar als voor een bepaalde reden moet u tooinstall uit https://github.com rechtstreeks gebruik hello te volgen stappen.</span><span class="sxs-lookup"><span data-stu-id="42a38-193">Typically this is all you need, but if for some reason you need tooinstall it from https://github.com directly, use hello following steps.</span></span>


## <a name="update-hello-linux-agent-when-no-agent-package-exists-for-distribution"></a><span data-ttu-id="42a38-194">Hallo Linux-Agent bijwerken wanneer er geen agentpakket voor distributie bestaat</span><span class="sxs-lookup"><span data-stu-id="42a38-194">Update hello Linux Agent when no agent package exists for distribution</span></span>

<span data-ttu-id="42a38-195">Wget (Er zijn een aantal distributies dat niet het standaard, zoals Redhat en CentOS, Oracle Linux versies, 6.4 en 6.5) installeren door te typen `sudo yum install wget` op Hallo-opdrachtregel.</span><span class="sxs-lookup"><span data-stu-id="42a38-195">Install wget (there are some distros that don't install it by default, such as Redhat, CentOS, and Oracle Linux versions 6.4 and 6.5) by typing `sudo yum install wget` on hello command line.</span></span>

### <a name="1-download-hello-latest-version"></a><span data-ttu-id="42a38-196">1. Download de nieuwste versie Hallo</span><span class="sxs-lookup"><span data-stu-id="42a38-196">1. Download hello latest version</span></span>
<span data-ttu-id="42a38-197">Open [Hallo release van Azure Linux Agent in GitHub](https://github.com/Azure/WALinuxAgent/releases) in een webpagina en uitzoeken Hallo-nummer voor meest recente versie.</span><span class="sxs-lookup"><span data-stu-id="42a38-197">Open [hello release of Azure Linux Agent in GitHub](https://github.com/Azure/WALinuxAgent/releases) in a web page, and find out hello latest version number.</span></span> <span data-ttu-id="42a38-198">(U kunt uw huidige versie vinden door te typen `waagent --version`.)</span><span class="sxs-lookup"><span data-stu-id="42a38-198">(You can locate your current version by typing `waagent --version`.)</span></span>

#### <a name="for-version-22x-or-later-type"></a><span data-ttu-id="42a38-199">Voor versie 2.2.x of hoger, typ:</span><span class="sxs-lookup"><span data-stu-id="42a38-199">For version 2.2.x or later, type:</span></span>
```bash
wget https://github.com/Azure/WALinuxAgent/archive/v2.2.x.zip
unzip v2.2.x.zip.zip
cd WALinuxAgent-2.2.x
```

<span data-ttu-id="42a38-200">Hallo wordt volgende regel versie 2.2.0 als voorbeeld gebruikt:</span><span class="sxs-lookup"><span data-stu-id="42a38-200">hello following line uses version 2.2.0 as an example:</span></span>

```bash
wget https://github.com/Azure/WALinuxAgent/archive/v2.2.14.zip
unzip v2.2.14.zip  
cd WALinuxAgent-2.2.14
```

### <a name="2-install-hello-azure-linux-agent"></a><span data-ttu-id="42a38-201">2. Hello Azure Linux Agent installeren</span><span class="sxs-lookup"><span data-stu-id="42a38-201">2. Install hello Azure Linux Agent</span></span>

#### <a name="for-version-22x-use"></a><span data-ttu-id="42a38-202">Voor versie 2.2.x, gebruiken:</span><span class="sxs-lookup"><span data-stu-id="42a38-202">For version 2.2.x, use:</span></span>
<span data-ttu-id="42a38-203">Mogelijk moet u tooinstall Hallo pakket `setuptools` eerst--Zie [hier](https://pypi.python.org/pypi/setuptools).</span><span class="sxs-lookup"><span data-stu-id="42a38-203">You may need tooinstall hello package `setuptools` first--see [here](https://pypi.python.org/pypi/setuptools).</span></span> <span data-ttu-id="42a38-204">Voer vervolgens:</span><span class="sxs-lookup"><span data-stu-id="42a38-204">Then run:</span></span>

```bash
sudo python setup.py install
```

#### <a name="ensure-auto-update-is-enabled"></a><span data-ttu-id="42a38-205">Zorg ervoor dat automatische updates is ingeschakeld</span><span class="sxs-lookup"><span data-stu-id="42a38-205">Ensure auto update is enabled</span></span>

<span data-ttu-id="42a38-206">Controleer eerst toosee als deze is ingeschakeld:</span><span class="sxs-lookup"><span data-stu-id="42a38-206">First, check toosee if it is enabled:</span></span>

```bash
cat /etc/waagent.conf
```

<span data-ttu-id="42a38-207">'AutoUpdate.Enabled' vinden.</span><span class="sxs-lookup"><span data-stu-id="42a38-207">Find 'AutoUpdate.Enabled'.</span></span> <span data-ttu-id="42a38-208">Als u deze uitvoer ziet, is het ingeschakeld:</span><span class="sxs-lookup"><span data-stu-id="42a38-208">If you see this output, it is enabled:</span></span>

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

<span data-ttu-id="42a38-209">tooenable uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="42a38-209">tooenable run:</span></span>

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="3-restart-hello-waagent-service"></a><span data-ttu-id="42a38-210">3. Hallo waagent-service opnieuw starten</span><span class="sxs-lookup"><span data-stu-id="42a38-210">3. Restart hello waagent service</span></span>
<span data-ttu-id="42a38-211">Voor het merendeel van Linux-distributies:</span><span class="sxs-lookup"><span data-stu-id="42a38-211">For most of Linux distros:</span></span>

```bash
sudo service waagent restart
```

<span data-ttu-id="42a38-212">Ubuntu, gebruikt u in:</span><span class="sxs-lookup"><span data-stu-id="42a38-212">For Ubuntu, use:</span></span>

```bash
sudo service walinuxagent restart
```

<span data-ttu-id="42a38-213">Voor virtuele CoreOS, gebruiken:</span><span class="sxs-lookup"><span data-stu-id="42a38-213">For CoreOS, use:</span></span>

```bash
sudo systemctl restart waagent
```

### <a name="4-confirm-hello-azure-linux-agent-version"></a><span data-ttu-id="42a38-214">4. Hello Azure Linux Agent versie bevestigen</span><span class="sxs-lookup"><span data-stu-id="42a38-214">4. Confirm hello Azure Linux Agent version</span></span>
    
```bash
waagent -version
```

<span data-ttu-id="42a38-215">Voor virtuele CoreOS, Hallo hierboven opdracht werkt mogelijk niet.</span><span class="sxs-lookup"><span data-stu-id="42a38-215">For CoreOS, hello above command may not work.</span></span>

<span data-ttu-id="42a38-216">U ziet dat hello Azure Linux Agent versie is bijgewerkt toohello nieuwe versie.</span><span class="sxs-lookup"><span data-stu-id="42a38-216">You will see that hello Azure Linux Agent version has been updated toohello new version.</span></span>

<span data-ttu-id="42a38-217">Zie voor meer informatie over hello Azure Linux Agent [Azure Linux Agent Leesmij](https://github.com/Azure/WALinuxAgent).</span><span class="sxs-lookup"><span data-stu-id="42a38-217">For more information regarding hello Azure Linux Agent, see [Azure Linux Agent README](https://github.com/Azure/WALinuxAgent).</span></span>

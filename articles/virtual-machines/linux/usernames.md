---
title: Gebruikersnamen voor Linux selecteren | Microsoft Docs
description: Informatie over het selecteren van gebruikersnamen voor een virtuele Linux-machine in Azure.
services: virtual-machines-linux
documentationcenter: 
author: szarkos
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: 33b50c97-92f1-46c9-a623-e37f67459c5c
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/02/2017
ms.author: szark
ms.openlocfilehash: 1874d72e5f88816036667932371ff28704d186c8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="selecting-user-names-for-linux-on-azure"></a><span data-ttu-id="c7ba7-103">Gebruikersnamen selecteren voor Linux op Azure</span><span class="sxs-lookup"><span data-stu-id="c7ba7-103">Selecting User Names for Linux on Azure</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="c7ba7-104">Wanneer u een virtuele Linux-machine in Azure inrichten, moet u de naam van een niet-hoofdgebruiker die u later gebruiken kunt voor aanmelding bij de virtuele machine opgeven.</span><span class="sxs-lookup"><span data-stu-id="c7ba7-104">When you provision a Linux virtual machine on Azure you must specify the name of a non-root user that you can later use to log into the VM.</span></span> <span data-ttu-id="c7ba7-105">U kunt de naam van de nieuwe gebruiker of als inrichting via de klassieke Azure portal kunt u de standaard de naam 'azureuser' accepteren.</span><span class="sxs-lookup"><span data-stu-id="c7ba7-105">You may choose the name of the new user, or if provisioning via the Azure classic portal you can accept the default name "azureuser".</span></span>

<span data-ttu-id="c7ba7-106">In de meeste gevallen wordt deze gebruiker won't bestaan op de basisinstallatiekopie en tijdens het inrichtingsproces wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="c7ba7-106">In most cases this user won't exist on the base image and will be created during the provisioning process.</span></span> <span data-ttu-id="c7ba7-107">Als de gebruiker op de basisinstallatiekopie van de virtuele machine bestaat, configureert de Azure Linux-agent gewoon vervolgens het wachtwoord en/of de SSH-sleutel voor die gebruiker op basis van de informatie die u hebt opgegeven bij het maken van de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="c7ba7-107">If the user exists on the base VM image, then the Azure Linux agent simply configures the password and/or SSH key for that user based on the information you specified when creating the VM.</span></span>

<span data-ttu-id="c7ba7-108">**Echter**, Linux definieert een set namen van gebruikers die niet worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="c7ba7-108">**However**, Linux defines a set of user names that should not be used.</span></span> <span data-ttu-id="c7ba7-109">Tijdens het inrichtingsproces wordt **mislukken** als u probeert te creëren van een Linux-VM met behulp van een bestaande systeemgebruiker, die is gedefinieerd als een gebruiker met UID 0 en 99 liggen.</span><span class="sxs-lookup"><span data-stu-id="c7ba7-109">The provisioning process will **fail** if you try to provision a Linux VM using an existing system user, which is defined as a user with UID 0-99.</span></span> <span data-ttu-id="c7ba7-110">Een typisch voorbeeld is de `root` gebruiker UID 0 is.</span><span class="sxs-lookup"><span data-stu-id="c7ba7-110">A typical example is the `root` user, which has UID 0.</span></span>

* <span data-ttu-id="c7ba7-111">Zie ook: [Linux standaard Base - gebruiker-ID bereiken](http://refspecs.linuxfoundation.org/LSB_4.1.0/LSB-Core-generic/LSB-Core-generic/uidrange.html)</span><span class="sxs-lookup"><span data-stu-id="c7ba7-111">See also: [Linux Standard Base - User ID Ranges](http://refspecs.linuxfoundation.org/LSB_4.1.0/LSB-Core-generic/LSB-Core-generic/uidrange.html)</span></span>

<span data-ttu-id="c7ba7-112">Hier volgt een lijst met algemene ingebouwd systeem-gebruikers voor CentOS en Ubuntu dat moet u niet gebruiken bij het inrichten van een virtuele Linux-machine in Azure.</span><span class="sxs-lookup"><span data-stu-id="c7ba7-112">The following is a list of common built-in system users for CentOS and Ubuntu that you should avoid using when provisioning a Linux virtual machine on Azure.</span></span> <span data-ttu-id="c7ba7-113">Deze lijst is slechts een voorbeeld, Raadpleeg de documentatie voor uw distributiepunt om ervoor te zorgen dat de gebruikersnaam die u ervoor kiezen geen met een bestaande gebruiker conflict.</span><span class="sxs-lookup"><span data-stu-id="c7ba7-113">This list is just an example, please refer to the documentation for your distribution to ensure that the username you choose does not conflict with an existing system user.</span></span>

## <a name="centos"></a><span data-ttu-id="c7ba7-114">CentOS</span><span class="sxs-lookup"><span data-stu-id="c7ba7-114">CentOS</span></span>
* <span data-ttu-id="c7ba7-115">abrt</span><span class="sxs-lookup"><span data-stu-id="c7ba7-115">abrt</span></span>
* <span data-ttu-id="c7ba7-116">adm</span><span class="sxs-lookup"><span data-stu-id="c7ba7-116">adm</span></span>
* <span data-ttu-id="c7ba7-117">audio</span><span class="sxs-lookup"><span data-stu-id="c7ba7-117">audio</span></span>
* <span data-ttu-id="c7ba7-118">opslaglocatie</span><span class="sxs-lookup"><span data-stu-id="c7ba7-118">bin</span></span>
* <span data-ttu-id="c7ba7-119">cd-rom</span><span class="sxs-lookup"><span data-stu-id="c7ba7-119">cdrom</span></span>
* <span data-ttu-id="c7ba7-120">cgred</span><span class="sxs-lookup"><span data-stu-id="c7ba7-120">cgred</span></span>
* <span data-ttu-id="c7ba7-121">daemon</span><span class="sxs-lookup"><span data-stu-id="c7ba7-121">daemon</span></span>
* <span data-ttu-id="c7ba7-122">dbus</span><span class="sxs-lookup"><span data-stu-id="c7ba7-122">dbus</span></span>
* <span data-ttu-id="c7ba7-123">bellen</span><span class="sxs-lookup"><span data-stu-id="c7ba7-123">dialout</span></span>
* <span data-ttu-id="c7ba7-124">DIP</span><span class="sxs-lookup"><span data-stu-id="c7ba7-124">dip</span></span>
* <span data-ttu-id="c7ba7-125">schijf</span><span class="sxs-lookup"><span data-stu-id="c7ba7-125">disk</span></span>
* <span data-ttu-id="c7ba7-126">diskettestations</span><span class="sxs-lookup"><span data-stu-id="c7ba7-126">floppy</span></span>
* <span data-ttu-id="c7ba7-127">FTP</span><span class="sxs-lookup"><span data-stu-id="c7ba7-127">ftp</span></span>
* <span data-ttu-id="c7ba7-128">FTP</span><span class="sxs-lookup"><span data-stu-id="c7ba7-128">ftp</span></span>
* <span data-ttu-id="c7ba7-129">games</span><span class="sxs-lookup"><span data-stu-id="c7ba7-129">games</span></span>
* <span data-ttu-id="c7ba7-130">Gopher</span><span class="sxs-lookup"><span data-stu-id="c7ba7-130">gopher</span></span>
* <span data-ttu-id="c7ba7-131">haldaemon</span><span class="sxs-lookup"><span data-stu-id="c7ba7-131">haldaemon</span></span>
* <span data-ttu-id="c7ba7-132">is gestopt</span><span class="sxs-lookup"><span data-stu-id="c7ba7-132">halt</span></span>
* <span data-ttu-id="c7ba7-133">kmem</span><span class="sxs-lookup"><span data-stu-id="c7ba7-133">kmem</span></span>
* <span data-ttu-id="c7ba7-134">vergrendelen</span><span class="sxs-lookup"><span data-stu-id="c7ba7-134">lock</span></span>
* <span data-ttu-id="c7ba7-135">LP</span><span class="sxs-lookup"><span data-stu-id="c7ba7-135">lp</span></span>
* <span data-ttu-id="c7ba7-136">E-mail</span><span class="sxs-lookup"><span data-stu-id="c7ba7-136">mail</span></span>
* <span data-ttu-id="c7ba7-137">Man</span><span class="sxs-lookup"><span data-stu-id="c7ba7-137">man</span></span>
* <span data-ttu-id="c7ba7-138">geheugentoewijzing</span><span class="sxs-lookup"><span data-stu-id="c7ba7-138">mem</span></span>
* <span data-ttu-id="c7ba7-139">nfsnobody</span><span class="sxs-lookup"><span data-stu-id="c7ba7-139">nfsnobody</span></span>
* <span data-ttu-id="c7ba7-140">niemand</span><span class="sxs-lookup"><span data-stu-id="c7ba7-140">nobody</span></span>
* <span data-ttu-id="c7ba7-141">NTP</span><span class="sxs-lookup"><span data-stu-id="c7ba7-141">ntp</span></span>
* <span data-ttu-id="c7ba7-142">Operator</span><span class="sxs-lookup"><span data-stu-id="c7ba7-142">operator</span></span>
* <span data-ttu-id="c7ba7-143">oprofile</span><span class="sxs-lookup"><span data-stu-id="c7ba7-143">oprofile</span></span>
* <span data-ttu-id="c7ba7-144">postdrop</span><span class="sxs-lookup"><span data-stu-id="c7ba7-144">postdrop</span></span>
* <span data-ttu-id="c7ba7-145">postfix</span><span class="sxs-lookup"><span data-stu-id="c7ba7-145">postfix</span></span>
* <span data-ttu-id="c7ba7-146">qpidd</span><span class="sxs-lookup"><span data-stu-id="c7ba7-146">qpidd</span></span>
* <span data-ttu-id="c7ba7-147">hoofdmap</span><span class="sxs-lookup"><span data-stu-id="c7ba7-147">root</span></span>
* <span data-ttu-id="c7ba7-148">RPC</span><span class="sxs-lookup"><span data-stu-id="c7ba7-148">rpc</span></span>
* <span data-ttu-id="c7ba7-149">rpcuser</span><span class="sxs-lookup"><span data-stu-id="c7ba7-149">rpcuser</span></span>
* <span data-ttu-id="c7ba7-150">saslauth</span><span class="sxs-lookup"><span data-stu-id="c7ba7-150">saslauth</span></span>
* <span data-ttu-id="c7ba7-151">afsluiten</span><span class="sxs-lookup"><span data-stu-id="c7ba7-151">shutdown</span></span>
* <span data-ttu-id="c7ba7-152">slocate</span><span class="sxs-lookup"><span data-stu-id="c7ba7-152">slocate</span></span>
* <span data-ttu-id="c7ba7-153">sshd</span><span class="sxs-lookup"><span data-stu-id="c7ba7-153">sshd</span></span>
* <span data-ttu-id="c7ba7-154">stapdev</span><span class="sxs-lookup"><span data-stu-id="c7ba7-154">stapdev</span></span>
* <span data-ttu-id="c7ba7-155">stapusr</span><span class="sxs-lookup"><span data-stu-id="c7ba7-155">stapusr</span></span>
* <span data-ttu-id="c7ba7-156">Synchronisatie</span><span class="sxs-lookup"><span data-stu-id="c7ba7-156">sync</span></span>
* <span data-ttu-id="c7ba7-157">sys</span><span class="sxs-lookup"><span data-stu-id="c7ba7-157">sys</span></span>
* <span data-ttu-id="c7ba7-158">tape</span><span class="sxs-lookup"><span data-stu-id="c7ba7-158">tape</span></span>
* <span data-ttu-id="c7ba7-159">Test</span><span class="sxs-lookup"><span data-stu-id="c7ba7-159">test</span></span>
* <span data-ttu-id="c7ba7-160">tcpdump</span><span class="sxs-lookup"><span data-stu-id="c7ba7-160">tcpdump</span></span>
* <span data-ttu-id="c7ba7-161">TTY</span><span class="sxs-lookup"><span data-stu-id="c7ba7-161">tty</span></span>
* <span data-ttu-id="c7ba7-162">gebruikers</span><span class="sxs-lookup"><span data-stu-id="c7ba7-162">users</span></span>
* <span data-ttu-id="c7ba7-163">utempter</span><span class="sxs-lookup"><span data-stu-id="c7ba7-163">utempter</span></span>
* <span data-ttu-id="c7ba7-164">utmp</span><span class="sxs-lookup"><span data-stu-id="c7ba7-164">utmp</span></span>
* <span data-ttu-id="c7ba7-165">uucp</span><span class="sxs-lookup"><span data-stu-id="c7ba7-165">uucp</span></span>
* <span data-ttu-id="c7ba7-166">vcsa</span><span class="sxs-lookup"><span data-stu-id="c7ba7-166">vcsa</span></span>
* <span data-ttu-id="c7ba7-167">video</span><span class="sxs-lookup"><span data-stu-id="c7ba7-167">video</span></span>
* <span data-ttu-id="c7ba7-168">Wheel</span><span class="sxs-lookup"><span data-stu-id="c7ba7-168">wheel</span></span>

## <a name="ubuntu"></a><span data-ttu-id="c7ba7-169">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="c7ba7-169">Ubuntu</span></span>
* <span data-ttu-id="c7ba7-170">adm</span><span class="sxs-lookup"><span data-stu-id="c7ba7-170">adm</span></span>
* <span data-ttu-id="c7ba7-171">Beheerder</span><span class="sxs-lookup"><span data-stu-id="c7ba7-171">admin</span></span>
* <span data-ttu-id="c7ba7-172">audio</span><span class="sxs-lookup"><span data-stu-id="c7ba7-172">audio</span></span>
* <span data-ttu-id="c7ba7-173">Back-up</span><span class="sxs-lookup"><span data-stu-id="c7ba7-173">backup</span></span>
* <span data-ttu-id="c7ba7-174">opslaglocatie</span><span class="sxs-lookup"><span data-stu-id="c7ba7-174">bin</span></span>
* <span data-ttu-id="c7ba7-175">cd-rom</span><span class="sxs-lookup"><span data-stu-id="c7ba7-175">cdrom</span></span>
* <span data-ttu-id="c7ba7-176">crontab</span><span class="sxs-lookup"><span data-stu-id="c7ba7-176">crontab</span></span>
* <span data-ttu-id="c7ba7-177">daemon</span><span class="sxs-lookup"><span data-stu-id="c7ba7-177">daemon</span></span>
* <span data-ttu-id="c7ba7-178">bellen</span><span class="sxs-lookup"><span data-stu-id="c7ba7-178">dialout</span></span>
* <span data-ttu-id="c7ba7-179">DIP</span><span class="sxs-lookup"><span data-stu-id="c7ba7-179">dip</span></span>
* <span data-ttu-id="c7ba7-180">schijf</span><span class="sxs-lookup"><span data-stu-id="c7ba7-180">disk</span></span>
* <span data-ttu-id="c7ba7-181">Faxserver</span><span class="sxs-lookup"><span data-stu-id="c7ba7-181">fax</span></span>
* <span data-ttu-id="c7ba7-182">diskettestations</span><span class="sxs-lookup"><span data-stu-id="c7ba7-182">floppy</span></span>
* <span data-ttu-id="c7ba7-183">integreert</span><span class="sxs-lookup"><span data-stu-id="c7ba7-183">fuse</span></span>
* <span data-ttu-id="c7ba7-184">games</span><span class="sxs-lookup"><span data-stu-id="c7ba7-184">games</span></span>
* <span data-ttu-id="c7ba7-185">gnats</span><span class="sxs-lookup"><span data-stu-id="c7ba7-185">gnats</span></span>
* <span data-ttu-id="c7ba7-186">IRC</span><span class="sxs-lookup"><span data-stu-id="c7ba7-186">irc</span></span>
* <span data-ttu-id="c7ba7-187">kmem</span><span class="sxs-lookup"><span data-stu-id="c7ba7-187">kmem</span></span>
* <span data-ttu-id="c7ba7-188">Liggend</span><span class="sxs-lookup"><span data-stu-id="c7ba7-188">landscape</span></span>
* <span data-ttu-id="c7ba7-189">libuuid</span><span class="sxs-lookup"><span data-stu-id="c7ba7-189">libuuid</span></span>
* <span data-ttu-id="c7ba7-190">lijst</span><span class="sxs-lookup"><span data-stu-id="c7ba7-190">list</span></span>
* <span data-ttu-id="c7ba7-191">LP</span><span class="sxs-lookup"><span data-stu-id="c7ba7-191">lp</span></span>
* <span data-ttu-id="c7ba7-192">E-mail</span><span class="sxs-lookup"><span data-stu-id="c7ba7-192">mail</span></span>
* <span data-ttu-id="c7ba7-193">Man</span><span class="sxs-lookup"><span data-stu-id="c7ba7-193">man</span></span>
* <span data-ttu-id="c7ba7-194">MessageBus</span><span class="sxs-lookup"><span data-stu-id="c7ba7-194">messagebus</span></span>
* <span data-ttu-id="c7ba7-195">mlocate</span><span class="sxs-lookup"><span data-stu-id="c7ba7-195">mlocate</span></span>
* <span data-ttu-id="c7ba7-196">netdev</span><span class="sxs-lookup"><span data-stu-id="c7ba7-196">netdev</span></span>
* <span data-ttu-id="c7ba7-197">Nieuws</span><span class="sxs-lookup"><span data-stu-id="c7ba7-197">news</span></span>
* <span data-ttu-id="c7ba7-198">niemand</span><span class="sxs-lookup"><span data-stu-id="c7ba7-198">nobody</span></span>
* <span data-ttu-id="c7ba7-199">nogroup</span><span class="sxs-lookup"><span data-stu-id="c7ba7-199">nogroup</span></span>
* <span data-ttu-id="c7ba7-200">Operator</span><span class="sxs-lookup"><span data-stu-id="c7ba7-200">operator</span></span>
* <span data-ttu-id="c7ba7-201">plugdev</span><span class="sxs-lookup"><span data-stu-id="c7ba7-201">plugdev</span></span>
* <span data-ttu-id="c7ba7-202">Proxy</span><span class="sxs-lookup"><span data-stu-id="c7ba7-202">proxy</span></span>
* <span data-ttu-id="c7ba7-203">hoofdmap</span><span class="sxs-lookup"><span data-stu-id="c7ba7-203">root</span></span>
* <span data-ttu-id="c7ba7-204">SASL</span><span class="sxs-lookup"><span data-stu-id="c7ba7-204">sasl</span></span>
* <span data-ttu-id="c7ba7-205">Shadow</span><span class="sxs-lookup"><span data-stu-id="c7ba7-205">shadow</span></span>
* <span data-ttu-id="c7ba7-206">src</span><span class="sxs-lookup"><span data-stu-id="c7ba7-206">src</span></span>
* <span data-ttu-id="c7ba7-207">SSH</span><span class="sxs-lookup"><span data-stu-id="c7ba7-207">ssh</span></span>
* <span data-ttu-id="c7ba7-208">sshd</span><span class="sxs-lookup"><span data-stu-id="c7ba7-208">sshd</span></span>
* <span data-ttu-id="c7ba7-209">medewerkers</span><span class="sxs-lookup"><span data-stu-id="c7ba7-209">staff</span></span>
* <span data-ttu-id="c7ba7-210">sudo</span><span class="sxs-lookup"><span data-stu-id="c7ba7-210">sudo</span></span>
* <span data-ttu-id="c7ba7-211">Synchronisatie</span><span class="sxs-lookup"><span data-stu-id="c7ba7-211">sync</span></span>
* <span data-ttu-id="c7ba7-212">sys</span><span class="sxs-lookup"><span data-stu-id="c7ba7-212">sys</span></span>
* <span data-ttu-id="c7ba7-213">syslog</span><span class="sxs-lookup"><span data-stu-id="c7ba7-213">syslog</span></span>
* <span data-ttu-id="c7ba7-214">tape</span><span class="sxs-lookup"><span data-stu-id="c7ba7-214">tape</span></span>
* <span data-ttu-id="c7ba7-215">TTY</span><span class="sxs-lookup"><span data-stu-id="c7ba7-215">tty</span></span>
* <span data-ttu-id="c7ba7-216">gebruikers</span><span class="sxs-lookup"><span data-stu-id="c7ba7-216">users</span></span>
* <span data-ttu-id="c7ba7-217">utmp</span><span class="sxs-lookup"><span data-stu-id="c7ba7-217">utmp</span></span>
* <span data-ttu-id="c7ba7-218">uucp</span><span class="sxs-lookup"><span data-stu-id="c7ba7-218">uucp</span></span>
* <span data-ttu-id="c7ba7-219">video</span><span class="sxs-lookup"><span data-stu-id="c7ba7-219">video</span></span>
* <span data-ttu-id="c7ba7-220">Voice-over</span><span class="sxs-lookup"><span data-stu-id="c7ba7-220">voice</span></span>
* <span data-ttu-id="c7ba7-221">whoopsie</span><span class="sxs-lookup"><span data-stu-id="c7ba7-221">whoopsie</span></span>
* <span data-ttu-id="c7ba7-222">www-gegevens</span><span class="sxs-lookup"><span data-stu-id="c7ba7-222">www-data</span></span>


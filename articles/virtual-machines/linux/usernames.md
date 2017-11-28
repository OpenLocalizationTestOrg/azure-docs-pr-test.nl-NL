---
title: aaaSelecting gebruikersnamen voor Linux | Microsoft Docs
description: Meer informatie over hoe de namen van tooselect gebruiker voor een virtuele Linux-machine in Azure.
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
ms.openlocfilehash: c65e2ac46f40bb8c9d74cccbaf248a070c0fa6cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="selecting-user-names-for-linux-on-azure"></a><span data-ttu-id="c3936-103">Gebruikersnamen selecteren voor Linux op Azure</span><span class="sxs-lookup"><span data-stu-id="c3936-103">Selecting User Names for Linux on Azure</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="c3936-104">Wanneer u een virtuele Linux-machine in Azure inricht, kunt u Hallo-naam van een niet-hoofdgebruiker waarmee u later toolog in Hallo VM kunt moet opgeven.</span><span class="sxs-lookup"><span data-stu-id="c3936-104">When you provision a Linux virtual machine on Azure you must specify hello name of a non-root user that you can later use toolog into hello VM.</span></span> <span data-ttu-id="c3936-105">U kunt ervoor kiezen de naam van de nieuwe gebruiker Hallo Hallo of als inrichting via Hallo klassieke Azure-portal kunt u accepteren Hallo standaard de naam 'azureuser'.</span><span class="sxs-lookup"><span data-stu-id="c3936-105">You may choose hello name of hello new user, or if provisioning via hello Azure classic portal you can accept hello default name "azureuser".</span></span>

<span data-ttu-id="c3936-106">In de meeste gevallen wordt deze gebruiker op Hallo basisinstallatiekopie won't bestaan en wordt gemaakt tijdens het inrichtingsproces Hallo.</span><span class="sxs-lookup"><span data-stu-id="c3936-106">In most cases this user won't exist on hello base image and will be created during hello provisioning process.</span></span> <span data-ttu-id="c3936-107">Als gebruiker Hallo op Hallo basisinstallatiekopie VM bestaat, configureert hello Azure Linux agent gewoon vervolgens Hallo wachtwoord en/of SSH-sleutel voor die gebruiker op basis van Hallo informatie die u hebt opgegeven bij het maken van Hallo VM.</span><span class="sxs-lookup"><span data-stu-id="c3936-107">If hello user exists on hello base VM image, then hello Azure Linux agent simply configures hello password and/or SSH key for that user based on hello information you specified when creating hello VM.</span></span>

<span data-ttu-id="c3936-108">**Echter**, Linux definieert een set namen van gebruikers die niet worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="c3936-108">**However**, Linux defines a set of user names that should not be used.</span></span> <span data-ttu-id="c3936-109">Hallo inrichting proces wordt **mislukken** als u probeert tooprovision een Linux-VM met behulp van een bestaande systeemgebruiker, die is gedefinieerd als een gebruiker met UID 0 en 99 liggen.</span><span class="sxs-lookup"><span data-stu-id="c3936-109">hello provisioning process will **fail** if you try tooprovision a Linux VM using an existing system user, which is defined as a user with UID 0-99.</span></span> <span data-ttu-id="c3936-110">Een typisch voorbeeld is Hallo `root` gebruiker UID 0 is.</span><span class="sxs-lookup"><span data-stu-id="c3936-110">A typical example is hello `root` user, which has UID 0.</span></span>

* <span data-ttu-id="c3936-111">Zie ook: [Linux standaard Base - gebruiker-ID bereiken](http://refspecs.linuxfoundation.org/LSB_4.1.0/LSB-Core-generic/LSB-Core-generic/uidrange.html)</span><span class="sxs-lookup"><span data-stu-id="c3936-111">See also: [Linux Standard Base - User ID Ranges](http://refspecs.linuxfoundation.org/LSB_4.1.0/LSB-Core-generic/LSB-Core-generic/uidrange.html)</span></span>

<span data-ttu-id="c3936-112">Hallo Hieronder volgt een lijst met algemene ingebouwd systeem-gebruikers voor CentOS en Ubuntu dat moet u niet gebruiken bij het inrichten van een virtuele Linux-machine in Azure.</span><span class="sxs-lookup"><span data-stu-id="c3936-112">hello following is a list of common built-in system users for CentOS and Ubuntu that you should avoid using when provisioning a Linux virtual machine on Azure.</span></span> <span data-ttu-id="c3936-113">Deze lijst is slechts een voorbeeld, raadpleegt u toohello-documentatie voor uw tooensure distributie die u niet in conflict met een bestaande systeemgebruiker Hallo-gebruikersnaam.</span><span class="sxs-lookup"><span data-stu-id="c3936-113">This list is just an example, please refer toohello documentation for your distribution tooensure that hello username you choose does not conflict with an existing system user.</span></span>

## <a name="centos"></a><span data-ttu-id="c3936-114">CentOS</span><span class="sxs-lookup"><span data-stu-id="c3936-114">CentOS</span></span>
* <span data-ttu-id="c3936-115">abrt</span><span class="sxs-lookup"><span data-stu-id="c3936-115">abrt</span></span>
* <span data-ttu-id="c3936-116">adm</span><span class="sxs-lookup"><span data-stu-id="c3936-116">adm</span></span>
* <span data-ttu-id="c3936-117">audio</span><span class="sxs-lookup"><span data-stu-id="c3936-117">audio</span></span>
* <span data-ttu-id="c3936-118">opslaglocatie</span><span class="sxs-lookup"><span data-stu-id="c3936-118">bin</span></span>
* <span data-ttu-id="c3936-119">cd-rom</span><span class="sxs-lookup"><span data-stu-id="c3936-119">cdrom</span></span>
* <span data-ttu-id="c3936-120">cgred</span><span class="sxs-lookup"><span data-stu-id="c3936-120">cgred</span></span>
* <span data-ttu-id="c3936-121">daemon</span><span class="sxs-lookup"><span data-stu-id="c3936-121">daemon</span></span>
* <span data-ttu-id="c3936-122">dbus</span><span class="sxs-lookup"><span data-stu-id="c3936-122">dbus</span></span>
* <span data-ttu-id="c3936-123">bellen</span><span class="sxs-lookup"><span data-stu-id="c3936-123">dialout</span></span>
* <span data-ttu-id="c3936-124">DIP</span><span class="sxs-lookup"><span data-stu-id="c3936-124">dip</span></span>
* <span data-ttu-id="c3936-125">schijf</span><span class="sxs-lookup"><span data-stu-id="c3936-125">disk</span></span>
* <span data-ttu-id="c3936-126">diskettestations</span><span class="sxs-lookup"><span data-stu-id="c3936-126">floppy</span></span>
* <span data-ttu-id="c3936-127">FTP</span><span class="sxs-lookup"><span data-stu-id="c3936-127">ftp</span></span>
* <span data-ttu-id="c3936-128">FTP</span><span class="sxs-lookup"><span data-stu-id="c3936-128">ftp</span></span>
* <span data-ttu-id="c3936-129">games</span><span class="sxs-lookup"><span data-stu-id="c3936-129">games</span></span>
* <span data-ttu-id="c3936-130">Gopher</span><span class="sxs-lookup"><span data-stu-id="c3936-130">gopher</span></span>
* <span data-ttu-id="c3936-131">haldaemon</span><span class="sxs-lookup"><span data-stu-id="c3936-131">haldaemon</span></span>
* <span data-ttu-id="c3936-132">is gestopt</span><span class="sxs-lookup"><span data-stu-id="c3936-132">halt</span></span>
* <span data-ttu-id="c3936-133">kmem</span><span class="sxs-lookup"><span data-stu-id="c3936-133">kmem</span></span>
* <span data-ttu-id="c3936-134">vergrendelen</span><span class="sxs-lookup"><span data-stu-id="c3936-134">lock</span></span>
* <span data-ttu-id="c3936-135">LP</span><span class="sxs-lookup"><span data-stu-id="c3936-135">lp</span></span>
* <span data-ttu-id="c3936-136">E-mail</span><span class="sxs-lookup"><span data-stu-id="c3936-136">mail</span></span>
* <span data-ttu-id="c3936-137">Man</span><span class="sxs-lookup"><span data-stu-id="c3936-137">man</span></span>
* <span data-ttu-id="c3936-138">geheugentoewijzing</span><span class="sxs-lookup"><span data-stu-id="c3936-138">mem</span></span>
* <span data-ttu-id="c3936-139">nfsnobody</span><span class="sxs-lookup"><span data-stu-id="c3936-139">nfsnobody</span></span>
* <span data-ttu-id="c3936-140">niemand</span><span class="sxs-lookup"><span data-stu-id="c3936-140">nobody</span></span>
* <span data-ttu-id="c3936-141">NTP</span><span class="sxs-lookup"><span data-stu-id="c3936-141">ntp</span></span>
* <span data-ttu-id="c3936-142">Operator</span><span class="sxs-lookup"><span data-stu-id="c3936-142">operator</span></span>
* <span data-ttu-id="c3936-143">oprofile</span><span class="sxs-lookup"><span data-stu-id="c3936-143">oprofile</span></span>
* <span data-ttu-id="c3936-144">postdrop</span><span class="sxs-lookup"><span data-stu-id="c3936-144">postdrop</span></span>
* <span data-ttu-id="c3936-145">postfix</span><span class="sxs-lookup"><span data-stu-id="c3936-145">postfix</span></span>
* <span data-ttu-id="c3936-146">qpidd</span><span class="sxs-lookup"><span data-stu-id="c3936-146">qpidd</span></span>
* <span data-ttu-id="c3936-147">hoofdmap</span><span class="sxs-lookup"><span data-stu-id="c3936-147">root</span></span>
* <span data-ttu-id="c3936-148">RPC</span><span class="sxs-lookup"><span data-stu-id="c3936-148">rpc</span></span>
* <span data-ttu-id="c3936-149">rpcuser</span><span class="sxs-lookup"><span data-stu-id="c3936-149">rpcuser</span></span>
* <span data-ttu-id="c3936-150">saslauth</span><span class="sxs-lookup"><span data-stu-id="c3936-150">saslauth</span></span>
* <span data-ttu-id="c3936-151">afsluiten</span><span class="sxs-lookup"><span data-stu-id="c3936-151">shutdown</span></span>
* <span data-ttu-id="c3936-152">slocate</span><span class="sxs-lookup"><span data-stu-id="c3936-152">slocate</span></span>
* <span data-ttu-id="c3936-153">sshd</span><span class="sxs-lookup"><span data-stu-id="c3936-153">sshd</span></span>
* <span data-ttu-id="c3936-154">stapdev</span><span class="sxs-lookup"><span data-stu-id="c3936-154">stapdev</span></span>
* <span data-ttu-id="c3936-155">stapusr</span><span class="sxs-lookup"><span data-stu-id="c3936-155">stapusr</span></span>
* <span data-ttu-id="c3936-156">Synchronisatie</span><span class="sxs-lookup"><span data-stu-id="c3936-156">sync</span></span>
* <span data-ttu-id="c3936-157">sys</span><span class="sxs-lookup"><span data-stu-id="c3936-157">sys</span></span>
* <span data-ttu-id="c3936-158">tape</span><span class="sxs-lookup"><span data-stu-id="c3936-158">tape</span></span>
* <span data-ttu-id="c3936-159">Test</span><span class="sxs-lookup"><span data-stu-id="c3936-159">test</span></span>
* <span data-ttu-id="c3936-160">tcpdump</span><span class="sxs-lookup"><span data-stu-id="c3936-160">tcpdump</span></span>
* <span data-ttu-id="c3936-161">TTY</span><span class="sxs-lookup"><span data-stu-id="c3936-161">tty</span></span>
* <span data-ttu-id="c3936-162">gebruikers</span><span class="sxs-lookup"><span data-stu-id="c3936-162">users</span></span>
* <span data-ttu-id="c3936-163">utempter</span><span class="sxs-lookup"><span data-stu-id="c3936-163">utempter</span></span>
* <span data-ttu-id="c3936-164">utmp</span><span class="sxs-lookup"><span data-stu-id="c3936-164">utmp</span></span>
* <span data-ttu-id="c3936-165">uucp</span><span class="sxs-lookup"><span data-stu-id="c3936-165">uucp</span></span>
* <span data-ttu-id="c3936-166">vcsa</span><span class="sxs-lookup"><span data-stu-id="c3936-166">vcsa</span></span>
* <span data-ttu-id="c3936-167">video</span><span class="sxs-lookup"><span data-stu-id="c3936-167">video</span></span>
* <span data-ttu-id="c3936-168">Wheel</span><span class="sxs-lookup"><span data-stu-id="c3936-168">wheel</span></span>

## <a name="ubuntu"></a><span data-ttu-id="c3936-169">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="c3936-169">Ubuntu</span></span>
* <span data-ttu-id="c3936-170">adm</span><span class="sxs-lookup"><span data-stu-id="c3936-170">adm</span></span>
* <span data-ttu-id="c3936-171">Beheerder</span><span class="sxs-lookup"><span data-stu-id="c3936-171">admin</span></span>
* <span data-ttu-id="c3936-172">audio</span><span class="sxs-lookup"><span data-stu-id="c3936-172">audio</span></span>
* <span data-ttu-id="c3936-173">Back-up</span><span class="sxs-lookup"><span data-stu-id="c3936-173">backup</span></span>
* <span data-ttu-id="c3936-174">opslaglocatie</span><span class="sxs-lookup"><span data-stu-id="c3936-174">bin</span></span>
* <span data-ttu-id="c3936-175">cd-rom</span><span class="sxs-lookup"><span data-stu-id="c3936-175">cdrom</span></span>
* <span data-ttu-id="c3936-176">crontab</span><span class="sxs-lookup"><span data-stu-id="c3936-176">crontab</span></span>
* <span data-ttu-id="c3936-177">daemon</span><span class="sxs-lookup"><span data-stu-id="c3936-177">daemon</span></span>
* <span data-ttu-id="c3936-178">bellen</span><span class="sxs-lookup"><span data-stu-id="c3936-178">dialout</span></span>
* <span data-ttu-id="c3936-179">DIP</span><span class="sxs-lookup"><span data-stu-id="c3936-179">dip</span></span>
* <span data-ttu-id="c3936-180">schijf</span><span class="sxs-lookup"><span data-stu-id="c3936-180">disk</span></span>
* <span data-ttu-id="c3936-181">Faxserver</span><span class="sxs-lookup"><span data-stu-id="c3936-181">fax</span></span>
* <span data-ttu-id="c3936-182">diskettestations</span><span class="sxs-lookup"><span data-stu-id="c3936-182">floppy</span></span>
* <span data-ttu-id="c3936-183">integreert</span><span class="sxs-lookup"><span data-stu-id="c3936-183">fuse</span></span>
* <span data-ttu-id="c3936-184">games</span><span class="sxs-lookup"><span data-stu-id="c3936-184">games</span></span>
* <span data-ttu-id="c3936-185">gnats</span><span class="sxs-lookup"><span data-stu-id="c3936-185">gnats</span></span>
* <span data-ttu-id="c3936-186">IRC</span><span class="sxs-lookup"><span data-stu-id="c3936-186">irc</span></span>
* <span data-ttu-id="c3936-187">kmem</span><span class="sxs-lookup"><span data-stu-id="c3936-187">kmem</span></span>
* <span data-ttu-id="c3936-188">Liggend</span><span class="sxs-lookup"><span data-stu-id="c3936-188">landscape</span></span>
* <span data-ttu-id="c3936-189">libuuid</span><span class="sxs-lookup"><span data-stu-id="c3936-189">libuuid</span></span>
* <span data-ttu-id="c3936-190">lijst</span><span class="sxs-lookup"><span data-stu-id="c3936-190">list</span></span>
* <span data-ttu-id="c3936-191">LP</span><span class="sxs-lookup"><span data-stu-id="c3936-191">lp</span></span>
* <span data-ttu-id="c3936-192">E-mail</span><span class="sxs-lookup"><span data-stu-id="c3936-192">mail</span></span>
* <span data-ttu-id="c3936-193">Man</span><span class="sxs-lookup"><span data-stu-id="c3936-193">man</span></span>
* <span data-ttu-id="c3936-194">MessageBus</span><span class="sxs-lookup"><span data-stu-id="c3936-194">messagebus</span></span>
* <span data-ttu-id="c3936-195">mlocate</span><span class="sxs-lookup"><span data-stu-id="c3936-195">mlocate</span></span>
* <span data-ttu-id="c3936-196">netdev</span><span class="sxs-lookup"><span data-stu-id="c3936-196">netdev</span></span>
* <span data-ttu-id="c3936-197">Nieuws</span><span class="sxs-lookup"><span data-stu-id="c3936-197">news</span></span>
* <span data-ttu-id="c3936-198">niemand</span><span class="sxs-lookup"><span data-stu-id="c3936-198">nobody</span></span>
* <span data-ttu-id="c3936-199">nogroup</span><span class="sxs-lookup"><span data-stu-id="c3936-199">nogroup</span></span>
* <span data-ttu-id="c3936-200">Operator</span><span class="sxs-lookup"><span data-stu-id="c3936-200">operator</span></span>
* <span data-ttu-id="c3936-201">plugdev</span><span class="sxs-lookup"><span data-stu-id="c3936-201">plugdev</span></span>
* <span data-ttu-id="c3936-202">Proxy</span><span class="sxs-lookup"><span data-stu-id="c3936-202">proxy</span></span>
* <span data-ttu-id="c3936-203">hoofdmap</span><span class="sxs-lookup"><span data-stu-id="c3936-203">root</span></span>
* <span data-ttu-id="c3936-204">SASL</span><span class="sxs-lookup"><span data-stu-id="c3936-204">sasl</span></span>
* <span data-ttu-id="c3936-205">Shadow</span><span class="sxs-lookup"><span data-stu-id="c3936-205">shadow</span></span>
* <span data-ttu-id="c3936-206">src</span><span class="sxs-lookup"><span data-stu-id="c3936-206">src</span></span>
* <span data-ttu-id="c3936-207">SSH</span><span class="sxs-lookup"><span data-stu-id="c3936-207">ssh</span></span>
* <span data-ttu-id="c3936-208">sshd</span><span class="sxs-lookup"><span data-stu-id="c3936-208">sshd</span></span>
* <span data-ttu-id="c3936-209">medewerkers</span><span class="sxs-lookup"><span data-stu-id="c3936-209">staff</span></span>
* <span data-ttu-id="c3936-210">sudo</span><span class="sxs-lookup"><span data-stu-id="c3936-210">sudo</span></span>
* <span data-ttu-id="c3936-211">Synchronisatie</span><span class="sxs-lookup"><span data-stu-id="c3936-211">sync</span></span>
* <span data-ttu-id="c3936-212">sys</span><span class="sxs-lookup"><span data-stu-id="c3936-212">sys</span></span>
* <span data-ttu-id="c3936-213">syslog</span><span class="sxs-lookup"><span data-stu-id="c3936-213">syslog</span></span>
* <span data-ttu-id="c3936-214">tape</span><span class="sxs-lookup"><span data-stu-id="c3936-214">tape</span></span>
* <span data-ttu-id="c3936-215">TTY</span><span class="sxs-lookup"><span data-stu-id="c3936-215">tty</span></span>
* <span data-ttu-id="c3936-216">gebruikers</span><span class="sxs-lookup"><span data-stu-id="c3936-216">users</span></span>
* <span data-ttu-id="c3936-217">utmp</span><span class="sxs-lookup"><span data-stu-id="c3936-217">utmp</span></span>
* <span data-ttu-id="c3936-218">uucp</span><span class="sxs-lookup"><span data-stu-id="c3936-218">uucp</span></span>
* <span data-ttu-id="c3936-219">video</span><span class="sxs-lookup"><span data-stu-id="c3936-219">video</span></span>
* <span data-ttu-id="c3936-220">Voice-over</span><span class="sxs-lookup"><span data-stu-id="c3936-220">voice</span></span>
* <span data-ttu-id="c3936-221">whoopsie</span><span class="sxs-lookup"><span data-stu-id="c3936-221">whoopsie</span></span>
* <span data-ttu-id="c3936-222">www-gegevens</span><span class="sxs-lookup"><span data-stu-id="c3936-222">www-data</span></span>


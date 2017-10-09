---
title: aaaConfiguring DHCPv6 voor virtuele Linux-machines | Microsoft Docs
description: Hoe tooconfigure DHCPv6 voor virtuele Linux-machines.
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: 
keywords: IPv6-, azure load balancer, dual-stack, openbare IP-adres, systeemeigen ipv6, mobiele, iot
ms.assetid: b32719b6-00e8-4cd0-ba7f-e60e8146084b
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/14/2016
ms.author: kumud
ms.openlocfilehash: abd5a98c3496b189946f59bab1d9c20dcd0aa2c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-dhcpv6-for-linux-vms"></a><span data-ttu-id="511ad-104">DHCPv6 configureren voor Linux VM's</span><span class="sxs-lookup"><span data-stu-id="511ad-104">Configuring DHCPv6 for Linux VMs</span></span>

<span data-ttu-id="511ad-105">Aantal Hallo Linux installatiekopieën van virtuele machines in Azure Marketplace Hallo geen DHCPv6 standaard geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="511ad-105">Some of hello Linux virtual machine images in hello Azure Marketplace do not have DHCPv6 configured by default.</span></span> <span data-ttu-id="511ad-106">toosupport IPv6, DHCPv6 moet worden geconfigureerd in binnen Hallo Linux-besturingssysteem distributie die u gebruikt.</span><span class="sxs-lookup"><span data-stu-id="511ad-106">toosupport IPv6, DHCPv6 must be configured in within hello Linux OS distribution that you are using.</span></span> <span data-ttu-id="511ad-107">Verschillende Linux-distributies zijn verschillende manieren van het configureren van DHCPv6 omdat ze verschillende pakketten gebruiken.</span><span class="sxs-lookup"><span data-stu-id="511ad-107">Different Linux distributions have different ways of configuring DHCPv6 because they use different packages.</span></span>

> [!NOTE]
> <span data-ttu-id="511ad-108">Recente SUSE Linux- en virtuele CoreOS-installatiekopieën in hello Azure Marketplace zijn vooraf geconfigureerd met DHCPv6.</span><span class="sxs-lookup"><span data-stu-id="511ad-108">Recent SUSE Linux and CoreOS images in hello Azure Marketplace have been pre-configured with DHCPv6.</span></span> <span data-ttu-id="511ad-109">Er zijn geen aanvullende wijzigingen vereist wanneer u deze afbeeldingen.</span><span class="sxs-lookup"><span data-stu-id="511ad-109">No additional changes are required when using those images.</span></span>

<span data-ttu-id="511ad-110">Dit document wordt beschreven hoe tooenable DHCPv6 zodat uw virtuele Linux-machine verkrijgt een IPv6-adres.</span><span class="sxs-lookup"><span data-stu-id="511ad-110">This document describes how tooenable DHCPv6 so that your Linux virtual machine obtains an IPv6 address.</span></span>

> [!WARNING]
> <span data-ttu-id="511ad-111">Onjuist bewerken van netwerk-configuratiebestanden, kunt u toolose netwerk toegang tooyour VM veroorzaken.</span><span class="sxs-lookup"><span data-stu-id="511ad-111">Improperly editing network configuration files can cause you toolose network access tooyour VM.</span></span> <span data-ttu-id="511ad-112">Het is raadzaam om uw configuratiewijzigingen op niet-productieve systemen te testen.</span><span class="sxs-lookup"><span data-stu-id="511ad-112">We recommended that you test your configuration changes on non-production systems.</span></span> <span data-ttu-id="511ad-113">Hallo-instructies in dit artikel zijn getest op Hallo nieuwste versies van Linux-installatiekopieën Hallo in hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="511ad-113">hello instructions in this article have been tested on hello latest versions of hello Linux images in hello Azure Marketplace.</span></span> <span data-ttu-id="511ad-114">Hallo documentatie voor uw specifieke versie van Linux voor gedetailleerde instructies.</span><span class="sxs-lookup"><span data-stu-id="511ad-114">Consult hello documentation for your specific version of Linux for more detailed instructions.</span></span>

## <a name="ubuntu"></a><span data-ttu-id="511ad-115">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="511ad-115">Ubuntu</span></span>

1. <span data-ttu-id="511ad-116">Hallo-bestand bewerken `/etc/dhcp/dhclient6.conf` en Hallo volgt regel toe te voegen:</span><span class="sxs-lookup"><span data-stu-id="511ad-116">Edit hello file `/etc/dhcp/dhclient6.conf` and add hello following line:</span></span>

        timeout 10;

2. <span data-ttu-id="511ad-117">Hallo-netwerkconfiguratie voor Hallo eth0 interface Hello na configuratie bewerken:</span><span class="sxs-lookup"><span data-stu-id="511ad-117">Edit hello network configuration for hello eth0 interface with hello following configuration:</span></span>

   * <span data-ttu-id="511ad-118">Op **Ubuntu 12.04 en 14.04**, Hallo bestand bewerken`/etc/network/interfaces.d/eth0.cfg`</span><span class="sxs-lookup"><span data-stu-id="511ad-118">On **Ubuntu 12.04 and 14.04**, edit hello file `/etc/network/interfaces.d/eth0.cfg`</span></span>
   * <span data-ttu-id="511ad-119">Op **Ubuntu 16.04**, Hallo bestand bewerken`/etc/network/interfaces.d/50-cloud-init.cfg`</span><span class="sxs-lookup"><span data-stu-id="511ad-119">On **Ubuntu 16.04**, edit hello file `/etc/network/interfaces.d/50-cloud-init.cfg`</span></span>

         iface eth0 inet6 auto
             up sleep 5
             up dhclient -1 -6 -cf /etc/dhcp/dhclient6.conf -lf /var/lib/dhcp/dhclient6.eth0.leases -v eth0 || true

3. <span data-ttu-id="511ad-120">IPv6-adres verlengen:</span><span class="sxs-lookup"><span data-stu-id="511ad-120">Renew IPv6 address:</span></span>

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

## <a name="debian"></a><span data-ttu-id="511ad-121">Debian</span><span class="sxs-lookup"><span data-stu-id="511ad-121">Debian</span></span>

1. <span data-ttu-id="511ad-122">Hallo-bestand bewerken `/etc/dhcp/dhclient6.conf` en Hallo volgt regel toe te voegen:</span><span class="sxs-lookup"><span data-stu-id="511ad-122">Edit hello file `/etc/dhcp/dhclient6.conf` and add hello following line:</span></span>

        timeout 10;

2. <span data-ttu-id="511ad-123">Hallo-bestand bewerken `/etc/network/interfaces` en Hallo na configuratie toe te voegen:</span><span class="sxs-lookup"><span data-stu-id="511ad-123">Edit hello file `/etc/network/interfaces` and add hello following configuration:</span></span>

        iface eth0 inet6 auto
            up sleep 5
            up dhclient -1 -6 -cf /etc/dhcp/dhclient6.conf -lf /var/lib/dhcp/dhclient6.eth0.leases -v eth0 || true

3. <span data-ttu-id="511ad-124">IPv6-adres verlengen:</span><span class="sxs-lookup"><span data-stu-id="511ad-124">Renew IPv6 address:</span></span>

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

## <a name="rhel--centos--oracle-linux"></a><span data-ttu-id="511ad-125">RHEL / CentOS / Oracle Linux</span><span class="sxs-lookup"><span data-stu-id="511ad-125">RHEL / CentOS / Oracle Linux</span></span>

1. <span data-ttu-id="511ad-126">Hallo-bestand bewerken `/etc/sysconfig/network` en Hallo parameter volgende toevoegen:</span><span class="sxs-lookup"><span data-stu-id="511ad-126">Edit hello file `/etc/sysconfig/network` and add hello following parameter:</span></span>

        NETWORKING_IPV6=yes

2. <span data-ttu-id="511ad-127">Hallo-bestand bewerken `/etc/sysconfig/network-scripts/ifcfg-eth0` en Hallo na twee parameters toe te voegen:</span><span class="sxs-lookup"><span data-stu-id="511ad-127">Edit hello file `/etc/sysconfig/network-scripts/ifcfg-eth0` and add hello following two parameters:</span></span>

        IPV6INIT=yes
        DHCPV6C=yes

3. <span data-ttu-id="511ad-128">IPv6-adres verlengen:</span><span class="sxs-lookup"><span data-stu-id="511ad-128">Renew IPv6 address:</span></span>

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

## <a name="sles-11--opensuse-13"></a><span data-ttu-id="511ad-129">SLES 11 & openSUSE 13</span><span class="sxs-lookup"><span data-stu-id="511ad-129">SLES 11 & openSUSE 13</span></span>

<span data-ttu-id="511ad-130">Recente SLES en openSUSE afbeeldingen in Azure is vooraf geconfigureerd met DHCPv6.</span><span class="sxs-lookup"><span data-stu-id="511ad-130">Recent SLES and openSUSE images in Azure have been pre-configured with DHCPv6.</span></span> <span data-ttu-id="511ad-131">Er zijn geen aanvullende wijzigingen vereist wanneer u deze afbeeldingen.</span><span class="sxs-lookup"><span data-stu-id="511ad-131">No additional changes are required when using those images.</span></span> <span data-ttu-id="511ad-132">Als u een virtuele machine op basis van een installatiekopie van een oudere of aangepaste SUSE hebt, gebruikt u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="511ad-132">If you have a VM based on an older or custom SUSE image, use hello following steps:</span></span>

1. <span data-ttu-id="511ad-133">Hallo installeren `dhcp-client` inpakken, indien nodig:</span><span class="sxs-lookup"><span data-stu-id="511ad-133">Install hello `dhcp-client` package, if needed:</span></span>

    ```bash
    sudo zypper install dhcp-client
    ```

2. <span data-ttu-id="511ad-134">Hallo-bestand bewerken `/etc/sysconfig/network/ifcfg-eth0` en Hallo parameter volgende toevoegen:</span><span class="sxs-lookup"><span data-stu-id="511ad-134">Edit hello file `/etc/sysconfig/network/ifcfg-eth0` and add hello following parameter:</span></span>

        DHCLIENT6_MODE='managed'

3. <span data-ttu-id="511ad-135">Hallo IPv6-adres verlengen:</span><span class="sxs-lookup"><span data-stu-id="511ad-135">Renew hello IPv6 address:</span></span>

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

## <a name="sles-12-and-opensuse-leap"></a><span data-ttu-id="511ad-136">SLES 12 en openSUSE Leap</span><span class="sxs-lookup"><span data-stu-id="511ad-136">SLES 12 and openSUSE Leap</span></span>

<span data-ttu-id="511ad-137">Recente SLES en openSUSE afbeeldingen in Azure is vooraf geconfigureerd met DHCPv6.</span><span class="sxs-lookup"><span data-stu-id="511ad-137">Recent SLES and openSUSE images in Azure have been pre-configured with DHCPv6.</span></span> <span data-ttu-id="511ad-138">Er zijn geen aanvullende wijzigingen vereist wanneer u deze afbeeldingen.</span><span class="sxs-lookup"><span data-stu-id="511ad-138">No additional changes are required when using those images.</span></span> <span data-ttu-id="511ad-139">Als u een virtuele machine op basis van een installatiekopie van een oudere of aangepaste SUSE hebt, gebruikt u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="511ad-139">If you have a VM based on an older or custom SUSE image, use hello following steps:</span></span>

1. <span data-ttu-id="511ad-140">Hallo-bestand bewerken `/etc/sysconfig/network/ifcfg-eth0` en vervang deze parameter</span><span class="sxs-lookup"><span data-stu-id="511ad-140">Edit hello file `/etc/sysconfig/network/ifcfg-eth0` and replace this parameter</span></span>

        #BOOTPROTO='dhcp4'

    <span data-ttu-id="511ad-141">Hello waarde te volgen:</span><span class="sxs-lookup"><span data-stu-id="511ad-141">with hello following value:</span></span>

        BOOTPROTO='dhcp'

2. <span data-ttu-id="511ad-142">Hallo parameter te volgen toevoegen`/etc/sysconfig/network/ifcfg-eth0`:</span><span class="sxs-lookup"><span data-stu-id="511ad-142">Add hello following parameter too`/etc/sysconfig/network/ifcfg-eth0`:</span></span>

        DHCLIENT6_MODE='managed'

3. <span data-ttu-id="511ad-143">Hallo IPv6-adres verlengen:</span><span class="sxs-lookup"><span data-stu-id="511ad-143">Renew hello IPv6 address:</span></span>

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

## <a name="coreos"></a><span data-ttu-id="511ad-144">CoreOS</span><span class="sxs-lookup"><span data-stu-id="511ad-144">CoreOS</span></span>

<span data-ttu-id="511ad-145">Recente virtuele CoreOS-afbeeldingen in Azure is vooraf geconfigureerd met DHCPv6.</span><span class="sxs-lookup"><span data-stu-id="511ad-145">Recent CoreOS images in Azure have been pre-configured with DHCPv6.</span></span> <span data-ttu-id="511ad-146">Er zijn geen aanvullende wijzigingen vereist wanneer u deze afbeeldingen.</span><span class="sxs-lookup"><span data-stu-id="511ad-146">No additional changes are required when using those images.</span></span> <span data-ttu-id="511ad-147">Als u een virtuele machine op basis van een virtuele CoreOS oudere of aangepaste installatiekopie hebt, gebruikt u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="511ad-147">If you have a VM based on an older or custom CoreOS image, use hello following steps:</span></span>

1. <span data-ttu-id="511ad-148">Hallo-bestand bewerken`/etc/systemd/network/10_dhcp.network`</span><span class="sxs-lookup"><span data-stu-id="511ad-148">Edit hello file `/etc/systemd/network/10_dhcp.network`</span></span>

        [Match]
        eth0

        [Network]
        DHCP=ipv6

2. <span data-ttu-id="511ad-149">Hallo IPv6-adres verlengen:</span><span class="sxs-lookup"><span data-stu-id="511ad-149">Renew hello IPv6 address:</span></span>

    ```bash
    sudo systemctl restart systemd-networkd
    ```

---
title: DHCPv6 configureren voor virtuele Linux-machines | Microsoft Docs
description: Klik hier voor meer informatie over het configureren van DHCPv6 voor virtuele Linux-machines.
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
ms.openlocfilehash: 5c591e7f1838c86ca74caea9dd3a5e8f874fd8a7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="configuring-dhcpv6-for-linux-vms"></a><span data-ttu-id="aac36-104">DHCPv6 configureren voor Linux VM's</span><span class="sxs-lookup"><span data-stu-id="aac36-104">Configuring DHCPv6 for Linux VMs</span></span>

<span data-ttu-id="aac36-105">Sommige van de installatiekopieën van het Linux-virtuele machine in Azure Marketplace hebben geen DHCPv6 standaard geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="aac36-105">Some of the Linux virtual machine images in the Azure Marketplace do not have DHCPv6 configured by default.</span></span> <span data-ttu-id="aac36-106">Ter ondersteuning van IPv6 moet DHCPv6 worden geconfigureerd in binnen de distributie van Linux-besturingssysteem die u gebruikt.</span><span class="sxs-lookup"><span data-stu-id="aac36-106">To support IPv6, DHCPv6 must be configured in within the Linux OS distribution that you are using.</span></span> <span data-ttu-id="aac36-107">Verschillende Linux-distributies zijn verschillende manieren van het configureren van DHCPv6 omdat ze verschillende pakketten gebruiken.</span><span class="sxs-lookup"><span data-stu-id="aac36-107">Different Linux distributions have different ways of configuring DHCPv6 because they use different packages.</span></span>

> [!NOTE]
> <span data-ttu-id="aac36-108">Recente SUSE Linux- en virtuele CoreOS-installatiekopieën in Azure Marketplace zijn vooraf geconfigureerd met DHCPv6.</span><span class="sxs-lookup"><span data-stu-id="aac36-108">Recent SUSE Linux and CoreOS images in the Azure Marketplace have been pre-configured with DHCPv6.</span></span> <span data-ttu-id="aac36-109">Er zijn geen aanvullende wijzigingen vereist wanneer u deze afbeeldingen.</span><span class="sxs-lookup"><span data-stu-id="aac36-109">No additional changes are required when using those images.</span></span>

<span data-ttu-id="aac36-110">Dit document wordt beschreven hoe DHCPv6 inschakelen zodat uw virtuele Linux-machine verkrijgt een IPv6-adres.</span><span class="sxs-lookup"><span data-stu-id="aac36-110">This document describes how to enable DHCPv6 so that your Linux virtual machine obtains an IPv6 address.</span></span>

> [!WARNING]
> <span data-ttu-id="aac36-111">Onjuist bewerken van netwerkbestanden configuratie kan leiden tot verliest u toegang tot uw virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="aac36-111">Improperly editing network configuration files can cause you to lose network access to your VM.</span></span> <span data-ttu-id="aac36-112">Het is raadzaam om uw configuratiewijzigingen op niet-productieve systemen te testen.</span><span class="sxs-lookup"><span data-stu-id="aac36-112">We recommended that you test your configuration changes on non-production systems.</span></span> <span data-ttu-id="aac36-113">De instructies in dit artikel zijn getest op de nieuwste versies van de Linux-installatiekopieën in Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="aac36-113">The instructions in this article have been tested on the latest versions of the Linux images in the Azure Marketplace.</span></span> <span data-ttu-id="aac36-114">Raadpleeg de documentatie voor uw specifieke versie van Linux voor gedetailleerde instructies.</span><span class="sxs-lookup"><span data-stu-id="aac36-114">Consult the documentation for your specific version of Linux for more detailed instructions.</span></span>

## <a name="ubuntu"></a><span data-ttu-id="aac36-115">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="aac36-115">Ubuntu</span></span>

1. <span data-ttu-id="aac36-116">Bewerk het bestand `/etc/dhcp/dhclient6.conf` en voeg de volgende regel:</span><span class="sxs-lookup"><span data-stu-id="aac36-116">Edit the file `/etc/dhcp/dhclient6.conf` and add the following line:</span></span>

        timeout 10;

2. <span data-ttu-id="aac36-117">Bewerk de netwerkconfiguratie voor de interface eth0 met de volgende configuratie:</span><span class="sxs-lookup"><span data-stu-id="aac36-117">Edit the network configuration for the eth0 interface with the following configuration:</span></span>

   * <span data-ttu-id="aac36-118">Op **Ubuntu 12.04 en 14.04**, bewerk het bestand`/etc/network/interfaces.d/eth0.cfg`</span><span class="sxs-lookup"><span data-stu-id="aac36-118">On **Ubuntu 12.04 and 14.04**, edit the file `/etc/network/interfaces.d/eth0.cfg`</span></span>
   * <span data-ttu-id="aac36-119">Op **Ubuntu 16.04**, bewerk het bestand`/etc/network/interfaces.d/50-cloud-init.cfg`</span><span class="sxs-lookup"><span data-stu-id="aac36-119">On **Ubuntu 16.04**, edit the file `/etc/network/interfaces.d/50-cloud-init.cfg`</span></span>

         iface eth0 inet6 auto
             up sleep 5
             up dhclient -1 -6 -cf /etc/dhcp/dhclient6.conf -lf /var/lib/dhcp/dhclient6.eth0.leases -v eth0 || true

3. <span data-ttu-id="aac36-120">IPv6-adres verlengen:</span><span class="sxs-lookup"><span data-stu-id="aac36-120">Renew IPv6 address:</span></span>

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

## <a name="debian"></a><span data-ttu-id="aac36-121">Debian</span><span class="sxs-lookup"><span data-stu-id="aac36-121">Debian</span></span>

1. <span data-ttu-id="aac36-122">Bewerk het bestand `/etc/dhcp/dhclient6.conf` en voeg de volgende regel:</span><span class="sxs-lookup"><span data-stu-id="aac36-122">Edit the file `/etc/dhcp/dhclient6.conf` and add the following line:</span></span>

        timeout 10;

2. <span data-ttu-id="aac36-123">Bewerk het bestand `/etc/network/interfaces` en voeg de volgende configuratie:</span><span class="sxs-lookup"><span data-stu-id="aac36-123">Edit the file `/etc/network/interfaces` and add the following configuration:</span></span>

        iface eth0 inet6 auto
            up sleep 5
            up dhclient -1 -6 -cf /etc/dhcp/dhclient6.conf -lf /var/lib/dhcp/dhclient6.eth0.leases -v eth0 || true

3. <span data-ttu-id="aac36-124">IPv6-adres verlengen:</span><span class="sxs-lookup"><span data-stu-id="aac36-124">Renew IPv6 address:</span></span>

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

## <a name="rhel--centos--oracle-linux"></a><span data-ttu-id="aac36-125">RHEL / CentOS / Oracle Linux</span><span class="sxs-lookup"><span data-stu-id="aac36-125">RHEL / CentOS / Oracle Linux</span></span>

1. <span data-ttu-id="aac36-126">Bewerk het bestand `/etc/sysconfig/network` en voeg de volgende parameter:</span><span class="sxs-lookup"><span data-stu-id="aac36-126">Edit the file `/etc/sysconfig/network` and add the following parameter:</span></span>

        NETWORKING_IPV6=yes

2. <span data-ttu-id="aac36-127">Bewerk het bestand `/etc/sysconfig/network-scripts/ifcfg-eth0` en voeg de volgende twee parameters:</span><span class="sxs-lookup"><span data-stu-id="aac36-127">Edit the file `/etc/sysconfig/network-scripts/ifcfg-eth0` and add the following two parameters:</span></span>

        IPV6INIT=yes
        DHCPV6C=yes

3. <span data-ttu-id="aac36-128">IPv6-adres verlengen:</span><span class="sxs-lookup"><span data-stu-id="aac36-128">Renew IPv6 address:</span></span>

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

## <a name="sles-11--opensuse-13"></a><span data-ttu-id="aac36-129">SLES 11 & openSUSE 13</span><span class="sxs-lookup"><span data-stu-id="aac36-129">SLES 11 & openSUSE 13</span></span>

<span data-ttu-id="aac36-130">Recente SLES en openSUSE afbeeldingen in Azure is vooraf geconfigureerd met DHCPv6.</span><span class="sxs-lookup"><span data-stu-id="aac36-130">Recent SLES and openSUSE images in Azure have been pre-configured with DHCPv6.</span></span> <span data-ttu-id="aac36-131">Er zijn geen aanvullende wijzigingen vereist wanneer u deze afbeeldingen.</span><span class="sxs-lookup"><span data-stu-id="aac36-131">No additional changes are required when using those images.</span></span> <span data-ttu-id="aac36-132">Als u een virtuele machine op basis van een installatiekopie van een oudere of aangepaste SUSE hebt, gebruikt u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="aac36-132">If you have a VM based on an older or custom SUSE image, use the following steps:</span></span>

1. <span data-ttu-id="aac36-133">Installeer de `dhcp-client` inpakken, indien nodig:</span><span class="sxs-lookup"><span data-stu-id="aac36-133">Install the `dhcp-client` package, if needed:</span></span>

    ```bash
    sudo zypper install dhcp-client
    ```

2. <span data-ttu-id="aac36-134">Bewerk het bestand `/etc/sysconfig/network/ifcfg-eth0` en voeg de volgende parameter:</span><span class="sxs-lookup"><span data-stu-id="aac36-134">Edit the file `/etc/sysconfig/network/ifcfg-eth0` and add the following parameter:</span></span>

        DHCLIENT6_MODE='managed'

3. <span data-ttu-id="aac36-135">Het IPv6-adres verlengen:</span><span class="sxs-lookup"><span data-stu-id="aac36-135">Renew the IPv6 address:</span></span>

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

## <a name="sles-12-and-opensuse-leap"></a><span data-ttu-id="aac36-136">SLES 12 en openSUSE Leap</span><span class="sxs-lookup"><span data-stu-id="aac36-136">SLES 12 and openSUSE Leap</span></span>

<span data-ttu-id="aac36-137">Recente SLES en openSUSE afbeeldingen in Azure is vooraf geconfigureerd met DHCPv6.</span><span class="sxs-lookup"><span data-stu-id="aac36-137">Recent SLES and openSUSE images in Azure have been pre-configured with DHCPv6.</span></span> <span data-ttu-id="aac36-138">Er zijn geen aanvullende wijzigingen vereist wanneer u deze afbeeldingen.</span><span class="sxs-lookup"><span data-stu-id="aac36-138">No additional changes are required when using those images.</span></span> <span data-ttu-id="aac36-139">Als u een virtuele machine op basis van een installatiekopie van een oudere of aangepaste SUSE hebt, gebruikt u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="aac36-139">If you have a VM based on an older or custom SUSE image, use the following steps:</span></span>

1. <span data-ttu-id="aac36-140">Bewerk het bestand `/etc/sysconfig/network/ifcfg-eth0` en vervang deze parameter</span><span class="sxs-lookup"><span data-stu-id="aac36-140">Edit the file `/etc/sysconfig/network/ifcfg-eth0` and replace this parameter</span></span>

        #BOOTPROTO='dhcp4'

    <span data-ttu-id="aac36-141">met de volgende waarde:</span><span class="sxs-lookup"><span data-stu-id="aac36-141">with the following value:</span></span>

        BOOTPROTO='dhcp'

2. <span data-ttu-id="aac36-142">Voeg de volgende parameter `/etc/sysconfig/network/ifcfg-eth0`:</span><span class="sxs-lookup"><span data-stu-id="aac36-142">Add the following parameter to `/etc/sysconfig/network/ifcfg-eth0`:</span></span>

        DHCLIENT6_MODE='managed'

3. <span data-ttu-id="aac36-143">Het IPv6-adres verlengen:</span><span class="sxs-lookup"><span data-stu-id="aac36-143">Renew the IPv6 address:</span></span>

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

## <a name="coreos"></a><span data-ttu-id="aac36-144">CoreOS</span><span class="sxs-lookup"><span data-stu-id="aac36-144">CoreOS</span></span>

<span data-ttu-id="aac36-145">Recente virtuele CoreOS-afbeeldingen in Azure is vooraf geconfigureerd met DHCPv6.</span><span class="sxs-lookup"><span data-stu-id="aac36-145">Recent CoreOS images in Azure have been pre-configured with DHCPv6.</span></span> <span data-ttu-id="aac36-146">Er zijn geen aanvullende wijzigingen vereist wanneer u deze afbeeldingen.</span><span class="sxs-lookup"><span data-stu-id="aac36-146">No additional changes are required when using those images.</span></span> <span data-ttu-id="aac36-147">Als u een virtuele machine op basis van een virtuele CoreOS oudere of aangepaste installatiekopie hebt, gebruikt u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="aac36-147">If you have a VM based on an older or custom CoreOS image, use the following steps:</span></span>

1. <span data-ttu-id="aac36-148">Bewerk het bestand`/etc/systemd/network/10_dhcp.network`</span><span class="sxs-lookup"><span data-stu-id="aac36-148">Edit the file `/etc/systemd/network/10_dhcp.network`</span></span>

        [Match]
        eth0

        [Network]
        DHCP=ipv6

2. <span data-ttu-id="aac36-149">Het IPv6-adres verlengen:</span><span class="sxs-lookup"><span data-stu-id="aac36-149">Renew the IPv6 address:</span></span>

    ```bash
    sudo systemctl restart systemd-networkd
    ```

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
# <a name="configuring-dhcpv6-for-linux-vms"></a>DHCPv6 configureren voor Linux VM's

Aantal Hallo Linux installatiekopieën van virtuele machines in Azure Marketplace Hallo geen DHCPv6 standaard geconfigureerd. toosupport IPv6, DHCPv6 moet worden geconfigureerd in binnen Hallo Linux-besturingssysteem distributie die u gebruikt. Verschillende Linux-distributies zijn verschillende manieren van het configureren van DHCPv6 omdat ze verschillende pakketten gebruiken.

> [!NOTE]
> Recente SUSE Linux- en virtuele CoreOS-installatiekopieën in hello Azure Marketplace zijn vooraf geconfigureerd met DHCPv6. Er zijn geen aanvullende wijzigingen vereist wanneer u deze afbeeldingen.

Dit document wordt beschreven hoe tooenable DHCPv6 zodat uw virtuele Linux-machine verkrijgt een IPv6-adres.

> [!WARNING]
> Onjuist bewerken van netwerk-configuratiebestanden, kunt u toolose netwerk toegang tooyour VM veroorzaken. Het is raadzaam om uw configuratiewijzigingen op niet-productieve systemen te testen. Hallo-instructies in dit artikel zijn getest op Hallo nieuwste versies van Linux-installatiekopieën Hallo in hello Azure Marketplace. Hallo documentatie voor uw specifieke versie van Linux voor gedetailleerde instructies.

## <a name="ubuntu"></a>Ubuntu

1. Hallo-bestand bewerken `/etc/dhcp/dhclient6.conf` en Hallo volgt regel toe te voegen:

        timeout 10;

2. Hallo-netwerkconfiguratie voor Hallo eth0 interface Hello na configuratie bewerken:

   * Op **Ubuntu 12.04 en 14.04**, Hallo bestand bewerken`/etc/network/interfaces.d/eth0.cfg`
   * Op **Ubuntu 16.04**, Hallo bestand bewerken`/etc/network/interfaces.d/50-cloud-init.cfg`

         iface eth0 inet6 auto
             up sleep 5
             up dhclient -1 -6 -cf /etc/dhcp/dhclient6.conf -lf /var/lib/dhcp/dhclient6.eth0.leases -v eth0 || true

3. IPv6-adres verlengen:

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

## <a name="debian"></a>Debian

1. Hallo-bestand bewerken `/etc/dhcp/dhclient6.conf` en Hallo volgt regel toe te voegen:

        timeout 10;

2. Hallo-bestand bewerken `/etc/network/interfaces` en Hallo na configuratie toe te voegen:

        iface eth0 inet6 auto
            up sleep 5
            up dhclient -1 -6 -cf /etc/dhcp/dhclient6.conf -lf /var/lib/dhcp/dhclient6.eth0.leases -v eth0 || true

3. IPv6-adres verlengen:

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

## <a name="rhel--centos--oracle-linux"></a>RHEL / CentOS / Oracle Linux

1. Hallo-bestand bewerken `/etc/sysconfig/network` en Hallo parameter volgende toevoegen:

        NETWORKING_IPV6=yes

2. Hallo-bestand bewerken `/etc/sysconfig/network-scripts/ifcfg-eth0` en Hallo na twee parameters toe te voegen:

        IPV6INIT=yes
        DHCPV6C=yes

3. IPv6-adres verlengen:

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

## <a name="sles-11--opensuse-13"></a>SLES 11 & openSUSE 13

Recente SLES en openSUSE afbeeldingen in Azure is vooraf geconfigureerd met DHCPv6. Er zijn geen aanvullende wijzigingen vereist wanneer u deze afbeeldingen. Als u een virtuele machine op basis van een installatiekopie van een oudere of aangepaste SUSE hebt, gebruikt u Hallo stappen te volgen:

1. Hallo installeren `dhcp-client` inpakken, indien nodig:

    ```bash
    sudo zypper install dhcp-client
    ```

2. Hallo-bestand bewerken `/etc/sysconfig/network/ifcfg-eth0` en Hallo parameter volgende toevoegen:

        DHCLIENT6_MODE='managed'

3. Hallo IPv6-adres verlengen:

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

## <a name="sles-12-and-opensuse-leap"></a>SLES 12 en openSUSE Leap

Recente SLES en openSUSE afbeeldingen in Azure is vooraf geconfigureerd met DHCPv6. Er zijn geen aanvullende wijzigingen vereist wanneer u deze afbeeldingen. Als u een virtuele machine op basis van een installatiekopie van een oudere of aangepaste SUSE hebt, gebruikt u Hallo stappen te volgen:

1. Hallo-bestand bewerken `/etc/sysconfig/network/ifcfg-eth0` en vervang deze parameter

        #BOOTPROTO='dhcp4'

    Hello waarde te volgen:

        BOOTPROTO='dhcp'

2. Hallo parameter te volgen toevoegen`/etc/sysconfig/network/ifcfg-eth0`:

        DHCLIENT6_MODE='managed'

3. Hallo IPv6-adres verlengen:

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

## <a name="coreos"></a>CoreOS

Recente virtuele CoreOS-afbeeldingen in Azure is vooraf geconfigureerd met DHCPv6. Er zijn geen aanvullende wijzigingen vereist wanneer u deze afbeeldingen. Als u een virtuele machine op basis van een virtuele CoreOS oudere of aangepaste installatiekopie hebt, gebruikt u Hallo stappen te volgen:

1. Hallo-bestand bewerken`/etc/systemd/network/10_dhcp.network`

        [Match]
        eth0

        [Network]
        DHCP=ipv6

2. Hallo IPv6-adres verlengen:

    ```bash
    sudo systemctl restart systemd-networkd
    ```

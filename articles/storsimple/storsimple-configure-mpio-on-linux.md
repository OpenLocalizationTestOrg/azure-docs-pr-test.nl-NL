---
title: aaaConfigure MPIO op StorSimple Linux-host | Microsoft Docs
description: MPIO op StorSimple verbonden tooa Linux-host met CentOS 6.6 configureren
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: tysonn
ms.assetid: ca289eed-12b7-4e2e-9117-adf7e2034f2f
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/01/2016
ms.author: alkohli
ms.openlocfilehash: d9f7e02903243494c909313fb2c33ac690764274
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-mpio-on-a-storsimple-host-running-centos"></a><span data-ttu-id="7cdf9-103">MPIO configureren op een StorSimple-host waarop van CentOS</span><span class="sxs-lookup"><span data-stu-id="7cdf9-103">Configure MPIO on a StorSimple host running CentOS</span></span>
<span data-ttu-id="7cdf9-104">Dit artikel wordt uitgelegd Hallo stappen vereist tooconfigure Multipath I/O (MPIO) op uw Centos 6.6 host-server.</span><span class="sxs-lookup"><span data-stu-id="7cdf9-104">This article explains hello steps required tooconfigure Multipathing IO (MPIO) on your Centos 6.6 host server.</span></span> <span data-ttu-id="7cdf9-105">Hallo host-server is verbonden tooyour Microsoft Azure StorSimple-apparaat voor hoge beschikbaarheid via iSCSI-initiators.</span><span class="sxs-lookup"><span data-stu-id="7cdf9-105">hello host server is connected tooyour Microsoft Azure StorSimple device for high availability via iSCSI initiators.</span></span> <span data-ttu-id="7cdf9-106">Hierin wordt beschreven in detail Hallo automatische detectie van meerdere paden apparaten en specifieke instellingen Hallo alleen voor StorSimple-volumes</span><span class="sxs-lookup"><span data-stu-id="7cdf9-106">It describes in detail hello automatic discovery of multipath devices and hello specific setup only for StorSimple volumes.</span></span>

<span data-ttu-id="7cdf9-107">Deze procedure is van toepassing tooall Hallo modellen van apparaten voor StorSimple 8000-serie.</span><span class="sxs-lookup"><span data-stu-id="7cdf9-107">This procedure is applicable tooall hello models of StorSimple 8000 series devices.</span></span>

> [!NOTE]
> <span data-ttu-id="7cdf9-108">Deze procedure kan niet worden gebruikt voor een virtueel StorSimple-apparaat.</span><span class="sxs-lookup"><span data-stu-id="7cdf9-108">This procedure cannot be used for a StorSimple virtual device.</span></span> <span data-ttu-id="7cdf9-109">Zie voor meer informatie hoe tooconfigure hostservers voor uw virtuele apparaat.</span><span class="sxs-lookup"><span data-stu-id="7cdf9-109">For more information, see how tooconfigure host servers for your virtual device.</span></span>
> 
> 

## <a name="about-multipathing"></a><span data-ttu-id="7cdf9-110">Over het gebruik van meerdere paden</span><span class="sxs-lookup"><span data-stu-id="7cdf9-110">About multipathing</span></span>
<span data-ttu-id="7cdf9-111">Hallo Multipath-functie kunt u tooconfigure meerdere i/o-paden tussen een hostserver en een opslagapparaat.</span><span class="sxs-lookup"><span data-stu-id="7cdf9-111">hello multipathing feature allows you tooconfigure multiple I/O paths between a host server and a storage device.</span></span> <span data-ttu-id="7cdf9-112">Deze i/o-paden zijn fysieke SAN-verbindingen die afzonderlijke kabels, switches, netwerkinterfaces en domeincontrollers kunnen opnemen.</span><span class="sxs-lookup"><span data-stu-id="7cdf9-112">These I/O paths are physical SAN connections that can include separate cables, switches, network interfaces, and controllers.</span></span> <span data-ttu-id="7cdf9-113">Gebruik van meerdere paden aggregeert Hallo i/o-paden, tooconfigure een nieuw apparaat dat is gekoppeld aan alle paden Hallo geaggregeerd.</span><span class="sxs-lookup"><span data-stu-id="7cdf9-113">Multipathing aggregates hello I/O paths, tooconfigure a new device that is associated with all of hello aggregated paths.</span></span>

<span data-ttu-id="7cdf9-114">Hallo-doel van meerdere paden is tweeledig:</span><span class="sxs-lookup"><span data-stu-id="7cdf9-114">hello purpose of multipathing is two-fold:</span></span>

* <span data-ttu-id="7cdf9-115">**Hoge beschikbaarheid**: biedt een alternatief pad als elk element van Hallo i/o-pad (zoals een kabel, switch, netwerkinterface of domeincontroller) is mislukt.</span><span class="sxs-lookup"><span data-stu-id="7cdf9-115">**High availability**: It provides an alternate path if any element of hello I/O path (such as a cable, switch, network interface, or controller) fails.</span></span>
* <span data-ttu-id="7cdf9-116">**Taakverdeling**: afhankelijk van de configuratie van de Hallo van uw opslagapparaat, deze prestaties kan verbeteren Hallo belasting op Hallo i/o-paden te detecteren en dynamisch herverdeling de belasting.</span><span class="sxs-lookup"><span data-stu-id="7cdf9-116">**Load balancing**: Depending on hello configuration of your storage device, it can improve hello performance by detecting loads on hello I/O paths and dynamically rebalancing those loads.</span></span>

### <a name="about-multipathing-components"></a><span data-ttu-id="7cdf9-117">Over het gebruik van meerdere paden onderdelen</span><span class="sxs-lookup"><span data-stu-id="7cdf9-117">About multipathing components</span></span>
<span data-ttu-id="7cdf9-118">Gebruik van meerdere paden in Linux bestaat uit de kernel als gebruikersruimte componenten zoals hieronder in een tabel.</span><span class="sxs-lookup"><span data-stu-id="7cdf9-118">Multipathing in Linux consists of kernel components and user-space components as tabulated below.</span></span>

* <span data-ttu-id="7cdf9-119">**Kernel**: Hallo hoofdonderdeel is Hallo *apparaat mapper* die wordt omgeleid i/o en failover voor paden en pad groepen ondersteunt.</span><span class="sxs-lookup"><span data-stu-id="7cdf9-119">**Kernel**: hello main component is hello *device-mapper* that reroutes I/O and supports failover for paths and path groups.</span></span>

* <span data-ttu-id="7cdf9-120">**Gebruikersruimte innemen**: dit zijn *multipath-tools* die welke toodo multipathed apparaten door multipath apparaat mapper-module Hallo beheren.</span><span class="sxs-lookup"><span data-stu-id="7cdf9-120">**User-space**: These are *multipath-tools* that manage multipathed devices by instructing hello device-mapper multipath module what toodo.</span></span> <span data-ttu-id="7cdf9-121">Hallo-hulpprogramma's bestaan uit:</span><span class="sxs-lookup"><span data-stu-id="7cdf9-121">hello tools consist of:</span></span>
   
   * <span data-ttu-id="7cdf9-122">**Multipath**: geeft een lijst van en multipathed apparaten configureert.</span><span class="sxs-lookup"><span data-stu-id="7cdf9-122">**Multipath**: lists and configures multipathed devices.</span></span>
   * <span data-ttu-id="7cdf9-123">**Multipathd**: daemon die multipath en monitors Hallo-paden wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="7cdf9-123">**Multipathd**: daemon that executes multipath and monitors hello paths.</span></span>
   * <span data-ttu-id="7cdf9-124">**Naam van de Devmap**: biedt een zinvolle apparaatnaam tooudev voor devmaps.</span><span class="sxs-lookup"><span data-stu-id="7cdf9-124">**Devmap-name**: provides a meaningful device-name tooudev for devmaps.</span></span>
   * <span data-ttu-id="7cdf9-125">**Kpartx**: lineaire devmaps toodevice partities toomake multipath maps partitioneerbare wordt toegewezen.</span><span class="sxs-lookup"><span data-stu-id="7cdf9-125">**Kpartx**: maps linear devmaps toodevice partitions toomake multipath maps partitionable.</span></span>
   * <span data-ttu-id="7cdf9-126">**Multipath.conf**: configuratiebestand voor multipath-daemon is gebruikte toooverwrite Hallo ingebouwde configuratietabel.</span><span class="sxs-lookup"><span data-stu-id="7cdf9-126">**Multipath.conf**: configuration file for multipath daemon that is used toooverwrite hello built-in configuration table.</span></span>

### <a name="about-hello-multipathconf-configuration-file"></a><span data-ttu-id="7cdf9-127">Over Hallo multipath.conf-configuratiebestand</span><span class="sxs-lookup"><span data-stu-id="7cdf9-127">About hello multipath.conf configuration file</span></span>
<span data-ttu-id="7cdf9-128">Hallo-configuratiebestand `/etc/multipath.conf` maakt veel Hallo Multipath-functies kunnen worden geconfigureerd met een gebruiker.</span><span class="sxs-lookup"><span data-stu-id="7cdf9-128">hello configuration file `/etc/multipath.conf` makes many of hello multipathing features user-configurable.</span></span> <span data-ttu-id="7cdf9-129">Hallo `multipath` opdracht en Hallo kernel-daemon `multipathd` gebruik informatie gevonden in dit bestand.</span><span class="sxs-lookup"><span data-stu-id="7cdf9-129">hello `multipath` command and hello kernel daemon `multipathd` use information found in this file.</span></span> <span data-ttu-id="7cdf9-130">Hallo-bestand is geraadpleegd alleen tijdens het Hallo-configuratie van MPIO Hallo-apparaten.</span><span class="sxs-lookup"><span data-stu-id="7cdf9-130">hello file is consulted only during hello configuration of hello multipath devices.</span></span> <span data-ttu-id="7cdf9-131">Zorg ervoor dat alle wijzigingen worden aangebracht voordat u Hallo uitvoert `multipath` opdracht.</span><span class="sxs-lookup"><span data-stu-id="7cdf9-131">Make sure that all changes are made before you run hello `multipath` command.</span></span> <span data-ttu-id="7cdf9-132">Als u Hallo bestand wijzigt daarna u moet toostop en multipathd voor Hallo wijzigingen tootake effect nogmaals te starten.</span><span class="sxs-lookup"><span data-stu-id="7cdf9-132">If you modify hello file afterwards, you will need toostop and start multipathd again for hello changes tootake effect.</span></span>

<span data-ttu-id="7cdf9-133">Hallo multipath.conf heeft vijf secties:</span><span class="sxs-lookup"><span data-stu-id="7cdf9-133">hello multipath.conf has five sections:</span></span>

- <span data-ttu-id="7cdf9-134">**Niveau standaardsysteemwaarden** *(standaardwaarden)*: U kunt niveau standaardwaarden van het systeem onderdrukken.</span><span class="sxs-lookup"><span data-stu-id="7cdf9-134">**System level defaults** *(defaults)*: You can override system level defaults.</span></span>
- <span data-ttu-id="7cdf9-135">**Apparaten gebeurd** *(blacklist)*: U kunt opgeven dat Hallo lijst met apparaten die niet moeten worden gecontroleerd door apparaat toewijzen.</span><span class="sxs-lookup"><span data-stu-id="7cdf9-135">**Blacklisted devices** *(blacklist)*: You can specify hello list of devices that should not be controlled by device-mapper.</span></span>
- <span data-ttu-id="7cdf9-136">**Uitzonderingen afgekeurde** *(blacklist_exceptions)*: U specifieke apparaten toobe behandeld als multipath-apparaten, zelfs als wordt weergegeven in zwarte lijst Hallo kunt identificeren.</span><span class="sxs-lookup"><span data-stu-id="7cdf9-136">**Blacklist exceptions** *(blacklist_exceptions)*: You can identify specific devices toobe treated as multipath devices even if listed in hello blacklist.</span></span>
- <span data-ttu-id="7cdf9-137">**Specifieke instellingen voor de controller opslag** *(apparaten)*: U kunt configuratie-instellingen die worden toegepast toodevices waarvoor leverancier-en productinformatie opgeven.</span><span class="sxs-lookup"><span data-stu-id="7cdf9-137">**Storage controller specific settings** *(devices)*: You can specify configuration settings that will be applied toodevices that have Vendor and Product information.</span></span>
- <span data-ttu-id="7cdf9-138">**Specifieke apparaatinstellingen** *(multipaths)*: U kunt deze sectie toofine afstemmen Hallo configuratie-instellingen voor afzonderlijke LUN's.</span><span class="sxs-lookup"><span data-stu-id="7cdf9-138">**Device specific settings** *(multipaths)*: You can use this section toofine-tune hello configuration settings for individual LUNs.</span></span>

## <a name="configure-multipathing-on-storsimple-connected-toolinux-host"></a><span data-ttu-id="7cdf9-139">Gebruik van meerdere paden op StorSimple verbonden tooLinux host configureren</span><span class="sxs-lookup"><span data-stu-id="7cdf9-139">Configure multipathing on StorSimple connected tooLinux host</span></span>
<span data-ttu-id="7cdf9-140">Een StorSimple-apparaat aansluit tooa Linux-host kan worden geconfigureerd voor hoge beschikbaarheid en taakverdeling.</span><span class="sxs-lookup"><span data-stu-id="7cdf9-140">A StorSimple device connected tooa Linux host can be configured for high availability and load balancing.</span></span> <span data-ttu-id="7cdf9-141">Bijvoorbeeld, als Hallo Linux-host heeft twee interfaces zijn verbonden toohello hello en SAN-apparaat heeft twee interfaces verbonden toohello SAN zodat deze interfaces worden op hetzelfde subnet Hallo en er zijn 4 paden beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="7cdf9-141">For example, if hello Linux host has two interfaces connected toohello SAN and hello device has two interfaces connected toohello SAN such that these interfaces are on hello same subnet, then there will be 4 paths available.</span></span> <span data-ttu-id="7cdf9-142">Echter, als elke interface gegevens op het apparaat en host interface Hallo op een ander IP-subnet (en niet-routeerbaar), vervolgens alleen 2 paden zijn beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="7cdf9-142">However, if each DATA interface on hello device and host interface are on a different IP subnet (and not routable), then only 2 paths will be available.</span></span> <span data-ttu-id="7cdf9-143">U kunt meerdere paden tooautomatically detecteren van alle beschikbare Hallo-paden, kiest u een taakverdelingsalgoritme voor die paden, toepassen specifieke configuratie-instellingen voor alleen-StorSimple-volumes, inschakelen en controleer of u gebruik van meerdere paden.</span><span class="sxs-lookup"><span data-stu-id="7cdf9-143">You can configure multipathing tooautomatically discover all hello available paths, choose a load-balancing algorithm for those paths, apply specific configuration settings for StorSimple-only volumes, and then enable and verify multipathing.</span></span>

<span data-ttu-id="7cdf9-144">Hallo volgende procedure wordt beschreven waarom de tooconfigure Multipath wanneer een StorSimple-apparaat met twee netwerkinterfaces verbonden tooa host met twee netwerkinterfaces.</span><span class="sxs-lookup"><span data-stu-id="7cdf9-144">hello following procedure describes how tooconfigure multipathing when a StorSimple device with two network interfaces is connected tooa host with two network interfaces.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7cdf9-145">Vereisten</span><span class="sxs-lookup"><span data-stu-id="7cdf9-145">Prerequisites</span></span>
<span data-ttu-id="7cdf9-146">Deze sectie beschrijft Hallo configuratievereisten voor CentOS-server en het StorSimple-apparaat.</span><span class="sxs-lookup"><span data-stu-id="7cdf9-146">This section details hello configuration prerequisites for CentOS server and your StorSimple device.</span></span>

### <a name="on-centos-host"></a><span data-ttu-id="7cdf9-147">Op de host CentOS</span><span class="sxs-lookup"><span data-stu-id="7cdf9-147">On CentOS host</span></span>
1. <span data-ttu-id="7cdf9-148">Zorg ervoor dat uw CentOS-host 2 netwerkinterfaces ingeschakeld heeft.</span><span class="sxs-lookup"><span data-stu-id="7cdf9-148">Make sure that your CentOS host has 2 network interfaces enabled.</span></span> <span data-ttu-id="7cdf9-149">Type:</span><span class="sxs-lookup"><span data-stu-id="7cdf9-149">Type:</span></span>
   
    `ifconfig`
   
    <span data-ttu-id="7cdf9-150">Hallo volgende voorbeeld ziet u uitvoer Hallo wanneer twee netwerkinterfaces (`eth0` en `eth1`) aanwezig zijn op Hallo host.</span><span class="sxs-lookup"><span data-stu-id="7cdf9-150">hello following example shows hello output when two network interfaces (`eth0` and `eth1`) are present on hello host.</span></span>
   
        [root@centosSS ~]# ifconfig
        eth0  Link encap:Ethernet  HWaddr 00:15:5D:A2:33:41  
          inet addr:10.126.162.65  Bcast:10.126.163.255  Mask:255.255.252.0
          inet6 addr: 2001:4898:4010:3012:215:5dff:fea2:3341/64 Scope:Global
          inet6 addr: fe80::215:5dff:fea2:3341/64 Scope:Link
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
         RX packets:36536 errors:0 dropped:0 overruns:0 frame:0
          TX packets:6312 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000
          RX bytes:13994127 (13.3 MiB)  TX bytes:645654 (630.5 KiB)
   
        eth1  Link encap:Ethernet  HWaddr 00:15:5D:A2:33:42  
          inet addr:10.126.162.66  Bcast:10.126.163.255  Mask:255.255.252.0
          inet6 addr: 2001:4898:4010:3012:215:5dff:fea2:3342/64 Scope:Global
          inet6 addr: fe80::215:5dff:fea2:3342/64 Scope:Link
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:25962 errors:0 dropped:0 overruns:0 frame:0
          TX packets:11 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000
          RX bytes:2597350 (2.4 MiB)  TX bytes:754 (754.0 b)
   
        loLink encap:Local Loopback  
          inet addr:127.0.0.1  Mask:255.0.0.0
          inet6 addr: ::1/128 Scope:Host
          UP LOOPBACK RUNNING  MTU:65536  Metric:1
          RX packets:12 errors:0 dropped:0 overruns:0 frame:0
          TX packets:12 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:0
          RX bytes:720 (720.0 b)  TX bytes:720 (720.0 b)
2. <span data-ttu-id="7cdf9-151">Installeer *iSCSI-initiator-utils* op uw server CentOS.</span><span class="sxs-lookup"><span data-stu-id="7cdf9-151">Install *iSCSI-initiator-utils* on your CentOS server.</span></span> <span data-ttu-id="7cdf9-152">Volgende stappen tooinstall Hallo uitvoeren *iSCSI-initiator-utils*.</span><span class="sxs-lookup"><span data-stu-id="7cdf9-152">Perform hello following steps tooinstall *iSCSI-initiator-utils*.</span></span>
   
   1. <span data-ttu-id="7cdf9-153">Meld u aan als `root` in uw CentOS-host.</span><span class="sxs-lookup"><span data-stu-id="7cdf9-153">Log on as `root` into your CentOS host.</span></span>
   2. <span data-ttu-id="7cdf9-154">Hallo installeren *iSCSI-initiator-utils*.</span><span class="sxs-lookup"><span data-stu-id="7cdf9-154">Install hello *iSCSI-initiator-utils*.</span></span> <span data-ttu-id="7cdf9-155">Type:</span><span class="sxs-lookup"><span data-stu-id="7cdf9-155">Type:</span></span>
      
       `yum install iscsi-initiator-utils`
   3. <span data-ttu-id="7cdf9-156">Na het Hallo *iSCSI-Initiator-utils* met succes is geïnstalleerd, start Hallo iSCSI-service.</span><span class="sxs-lookup"><span data-stu-id="7cdf9-156">After hello *iSCSI-Initiator-utils* is successfully installed, start hello iSCSI service.</span></span> <span data-ttu-id="7cdf9-157">Type:</span><span class="sxs-lookup"><span data-stu-id="7cdf9-157">Type:</span></span>
      
       `service iscsid start`
      
       <span data-ttu-id="7cdf9-158">In gevallen `iscsid` mogelijk niet daadwerkelijk start en Hallo `--force` optie zijn mogelijk vereist</span><span class="sxs-lookup"><span data-stu-id="7cdf9-158">On occasions, `iscsid` may not actually start and hello `--force` option may be needed</span></span>
   4. <span data-ttu-id="7cdf9-159">tooensure dat uw iSCSI-initiator is ingeschakeld tijdens het opstarten, gebruik Hallo `chkconfig` opdracht tooenable Hallo-service.</span><span class="sxs-lookup"><span data-stu-id="7cdf9-159">tooensure that your iSCSI initiator is enabled during boot time, use hello `chkconfig` command tooenable hello service.</span></span>
      
       `chkconfig iscsi on`
   5. <span data-ttu-id="7cdf9-160">tooverify dat deze goed is instellen, Hallo-opdracht uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="7cdf9-160">tooverify that that it was properly setup, run hello command:</span></span>
      
       `chkconfig --list | grep iscsi`
      
       <span data-ttu-id="7cdf9-161">Hieronder ziet u een voorbeeld van de uitvoer.</span><span class="sxs-lookup"><span data-stu-id="7cdf9-161">A sample output is shown below.</span></span>
      
           iscsi   0:off   1:off   2:on3:on4:on5:on6:off
           iscsid  0:off   1:off   2:on3:on4:on5:on6:off
      
       <span data-ttu-id="7cdf9-162">Van Hallo hierboven voorbeeld ziet u dat uw omgeving iSCSI op opstarten op uitvoeren niveaus 2, 3, 4 en 5 wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="7cdf9-162">From hello above example, you can see that your iSCSI environment will run on boot time on run levels 2, 3, 4, and 5.</span></span>
3. <span data-ttu-id="7cdf9-163">Installeer *apparaat-mapper-multipath*.</span><span class="sxs-lookup"><span data-stu-id="7cdf9-163">Install *device-mapper-multipath*.</span></span> <span data-ttu-id="7cdf9-164">Type:</span><span class="sxs-lookup"><span data-stu-id="7cdf9-164">Type:</span></span>
   
    `yum install device-mapper-multipath`
   
    <span data-ttu-id="7cdf9-165">Hallo-installatie wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="7cdf9-165">hello installation will start.</span></span> <span data-ttu-id="7cdf9-166">Type **Y** toocontinue wanneer u om bevestiging wordt gevraagd.</span><span class="sxs-lookup"><span data-stu-id="7cdf9-166">Type **Y** toocontinue when prompted for confirmation.</span></span>

### <a name="on-storsimple-device"></a><span data-ttu-id="7cdf9-167">Op het StorSimple-apparaat</span><span class="sxs-lookup"><span data-stu-id="7cdf9-167">On StorSimple device</span></span>
<span data-ttu-id="7cdf9-168">Uw StorSimple-apparaat moet hebben:</span><span class="sxs-lookup"><span data-stu-id="7cdf9-168">Your StorSimple device should have:</span></span>

* <span data-ttu-id="7cdf9-169">Minimaal twee interfaces zijn ingeschakeld voor iSCSI.</span><span class="sxs-lookup"><span data-stu-id="7cdf9-169">A minimum of two interfaces enabled for iSCSI.</span></span> <span data-ttu-id="7cdf9-170">tooverify dat twee interfaces zijn ingeschakeld voor iSCSI op uw StorSimple-apparaat, voert u stappen te volgen in de klassieke Azure-portal voor uw StorSimple-apparaat Hallo Hallo:</span><span class="sxs-lookup"><span data-stu-id="7cdf9-170">tooverify that two interfaces are iSCSI-enabled on your StorSimple device, perform hello following steps in hello Azure classic portal for your StorSimple device:</span></span>
  
  1. <span data-ttu-id="7cdf9-171">Meld u aan bij de klassieke portal Hallo voor uw StorSimple-apparaat.</span><span class="sxs-lookup"><span data-stu-id="7cdf9-171">Log into hello classic portal for your StorSimple device.</span></span>
  2. <span data-ttu-id="7cdf9-172">Selecteer uw StorSimple Manager-service, klikt u op **apparaten** en kies Hallo specifieke StorSimple-apparaat.</span><span class="sxs-lookup"><span data-stu-id="7cdf9-172">Select your StorSimple Manager service, click **Devices** and choose hello specific StorSimple device.</span></span> <span data-ttu-id="7cdf9-173">Klik op **configureren** en controleer of Hallo netwerkinterface-instellingen.</span><span class="sxs-lookup"><span data-stu-id="7cdf9-173">Click **Configure** and verify hello network interface settings.</span></span> <span data-ttu-id="7cdf9-174">Een schermafbeelding met twee netwerkinterfaces zijn ingeschakeld voor iSCSI-worden hieronder weergegeven.</span><span class="sxs-lookup"><span data-stu-id="7cdf9-174">A screenshot with two iSCSI-enabled network interfaces is shown below.</span></span> <span data-ttu-id="7cdf9-175">Hier DATA 2 en DATA 3, beide 10 GbE interfaces zijn ingeschakeld voor iSCSI.</span><span class="sxs-lookup"><span data-stu-id="7cdf9-175">Here DATA 2 and DATA 3, both 10 GbE interfaces are enabled for iSCSI.</span></span>
     
      ![Configuratie van MPIO StorsSimple DATA 2](./media/storsimple-configure-mpio-on-linux/IC761347.png)
     
      ![MPIO StorSimple gegevens 3 Config](./media/storsimple-configure-mpio-on-linux/IC761348.png)
     
      <span data-ttu-id="7cdf9-178">In Hallo **configureren** pagina</span><span class="sxs-lookup"><span data-stu-id="7cdf9-178">In hello **Configure** page</span></span>
     
     1. <span data-ttu-id="7cdf9-179">Zorg ervoor dat beide netwerkinterfaces iSCSI-functionaliteit.</span><span class="sxs-lookup"><span data-stu-id="7cdf9-179">Ensure that both network interfaces are iSCSI-enabled.</span></span> <span data-ttu-id="7cdf9-180">Hallo **iSCSI ingeschakeld** veld te moet worden ingesteld**Ja**.</span><span class="sxs-lookup"><span data-stu-id="7cdf9-180">hello **iSCSI enabled** field should be set too**Yes**.</span></span>
     2. <span data-ttu-id="7cdf9-181">Zorg ervoor dat de netwerkinterfaces Hallo Hallo hebben dezelfde snelheid beide moet 1 GbE- of 10 GbE.</span><span class="sxs-lookup"><span data-stu-id="7cdf9-181">Ensure that hello network interfaces have hello same speed, both should be 1 GbE or 10 GbE.</span></span>
     3. <span data-ttu-id="7cdf9-182">Houd er rekening mee Hallo IPv4-adressen van Hallo ingeschakeld voor iSCSI-interfaces en opslaan voor toekomstig gebruik op Hallo host.</span><span class="sxs-lookup"><span data-stu-id="7cdf9-182">Note hello IPv4 addresses of hello iSCSI-enabled interfaces and save for later use on hello host.</span></span>
* <span data-ttu-id="7cdf9-183">Hallo iSCSI-interfaces op uw StorSimple-apparaat moet bereikbaar is vanaf Hallo CentOS-server.</span><span class="sxs-lookup"><span data-stu-id="7cdf9-183">hello iSCSI interfaces on your StorSimple device should be reachable from hello CentOS server.</span></span>
      <span data-ttu-id="7cdf9-184">tooverify, moet u tooprovide Hallo IP-adressen van uw StorSimple-ingeschakeld voor iSCSI-netwerkinterfaces op de hostserver.</span><span class="sxs-lookup"><span data-stu-id="7cdf9-184">tooverify this, you need tooprovide hello IP addresses of your StorSimple iSCSI-enabled network interfaces on your host server.</span></span> <span data-ttu-id="7cdf9-185">Hallo opdrachten die worden gebruikt en de bijbehorende uitvoer met DATA2 Hallo (10.126.162.25) en DATA3 (10.126.162.26) worden hieronder weergegeven:</span><span class="sxs-lookup"><span data-stu-id="7cdf9-185">hello commands used and hello corresponding output with DATA2 (10.126.162.25) and DATA3 (10.126.162.26) is shown below:</span></span>
  
        [root@centosSS ~]# iscsiadm -m discovery -t sendtargets -p 10.126.162.25:3260
        10.126.162.25:3260,1 iqn.1991-05.com.microsoft:storsimple8100-shx0991003g44mt-target
        10.126.162.26:3260,1 iqn.1991-05.com.microsoft:storsimple8100-shx0991003g44mt-target

### <a name="hardware-configuration"></a><span data-ttu-id="7cdf9-186">Hardwareconfiguratie</span><span class="sxs-lookup"><span data-stu-id="7cdf9-186">Hardware configuration</span></span>
<span data-ttu-id="7cdf9-187">Het is raadzaam dat u verbinding Hallo twee iSCSI-netwerkinterfaces op afzonderlijke paden voor de redundantie maakt.</span><span class="sxs-lookup"><span data-stu-id="7cdf9-187">We recommend that you connect hello two iSCSI network interfaces on separate paths for redundancy.</span></span> <span data-ttu-id="7cdf9-188">Hallo afbeelding hieronder ziet u de aanbevolen hardwareconfiguratie Hallo voor hoge beschikbaarheid en taakverdeling gebruik van meerdere paden voor uw CentOS-server en het StorSimple-apparaat.</span><span class="sxs-lookup"><span data-stu-id="7cdf9-188">hello figure below shows hello recommended hardware configuration for high availability and load-balancing multipathing for your CentOS server and StorSimple device.</span></span>

![MPIO-hardwareconfiguratie voor StorSimple tooLinux host](./media/storsimple-configure-mpio-on-linux/MPIOHardwareConfigurationStorSimpleToLinuxHost2M.png)

<span data-ttu-id="7cdf9-190">Zoals u in de voorgaande afbeelding Hallo:</span><span class="sxs-lookup"><span data-stu-id="7cdf9-190">As shown in hello preceding figure:</span></span>

* <span data-ttu-id="7cdf9-191">Uw StorSimple-apparaat zich in een actief / passief-configuratie met twee domeincontrollers.</span><span class="sxs-lookup"><span data-stu-id="7cdf9-191">Your StorSimple device is in an active-passive configuration with two controllers.</span></span>
* <span data-ttu-id="7cdf9-192">Twee SAN-switches zijn verbonden tooyour apparaatcontrollers.</span><span class="sxs-lookup"><span data-stu-id="7cdf9-192">Two SAN switches are connected tooyour device controllers.</span></span>
* <span data-ttu-id="7cdf9-193">Twee iSCSI-initiators zijn ingeschakeld op uw StorSimple-apparaat.</span><span class="sxs-lookup"><span data-stu-id="7cdf9-193">Two iSCSI initiators are enabled on your StorSimple device.</span></span>
* <span data-ttu-id="7cdf9-194">Twee netwerkinterfaces zijn ingeschakeld op uw host CentOS.</span><span class="sxs-lookup"><span data-stu-id="7cdf9-194">Two network interfaces are enabled on your CentOS host.</span></span>

<span data-ttu-id="7cdf9-195">Hallo hierboven configuratie resulteert 4 afzonderlijke paden tussen uw apparaat en het Hallo-host als Hallo host- en interfaces routeerbaar zijn.</span><span class="sxs-lookup"><span data-stu-id="7cdf9-195">hello above configuration will yield 4 separate paths between your device and hello host if hello host and data interfaces are routable.</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="7cdf9-196">Het is raadzaam dat u niet door elkaar 1 GbE- en 10 GbE-netwerkinterfaces voor gebruik van meerdere paden.</span><span class="sxs-lookup"><span data-stu-id="7cdf9-196">We recommend that you do not mix 1 GbE and 10 GbE network interfaces for multipathing.</span></span> <span data-ttu-id="7cdf9-197">Wanneer u twee netwerkinterfaces, moeten beide interfaces Hallo Hallo identiek type zijn.</span><span class="sxs-lookup"><span data-stu-id="7cdf9-197">When using two network interfaces, both hello interfaces should be hello identical type.</span></span>
> * <span data-ttu-id="7cdf9-198">Op uw StorSimple-apparaat DATA0, bestand1, DATA4 en DATA5 zijn 1 GbE-interfaces DATA2 en DATA3 10 GbE-netwerkinterfaces zijn. |</span><span class="sxs-lookup"><span data-stu-id="7cdf9-198">On your StorSimple device, DATA0, DATA1, DATA4 and DATA5 are 1 GbE interfaces whereas DATA2 and DATA3 are 10 GbE network interfaces.|</span></span>
> 
> 

## <a name="configuration-steps"></a><span data-ttu-id="7cdf9-199">Configuratiestappen</span><span class="sxs-lookup"><span data-stu-id="7cdf9-199">Configuration steps</span></span>
<span data-ttu-id="7cdf9-200">Hallo configuratiestappen voor gebruik van meerdere paden hebben betrekking op Hallo beschikbare paden voor automatische detectie, geven Hallo-taakverdeling algoritme toouse, gebruik van meerdere paden inschakelen en ten slotte Hallo-configuratie controleren configureren.</span><span class="sxs-lookup"><span data-stu-id="7cdf9-200">hello configuration steps for multipathing involve configuring hello available paths for automatic discovery, specifying hello load-balancing algorithm toouse, enabling multipathing and finally verifying hello configuration.</span></span> <span data-ttu-id="7cdf9-201">Elk van deze stappen wordt uitgebreid beschreven in Hallo uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="7cdf9-201">Each of these steps is discussed in detail in hello following sections.</span></span>

### <a name="step-1-configure-multipathing-for-automatic-discovery"></a><span data-ttu-id="7cdf9-202">Stap 1: Configureer meerdere paden voor automatische detectie</span><span class="sxs-lookup"><span data-stu-id="7cdf9-202">Step 1: Configure multipathing for automatic discovery</span></span>
<span data-ttu-id="7cdf9-203">Hallo multipath-ondersteunde apparaten kunnen automatisch worden gedetecteerd en geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="7cdf9-203">hello multipath-supported devices can be automatically discovered and configured.</span></span>

1. <span data-ttu-id="7cdf9-204">Initialiseren `/etc/multipath.conf` bestand.</span><span class="sxs-lookup"><span data-stu-id="7cdf9-204">Initialize `/etc/multipath.conf` file.</span></span> <span data-ttu-id="7cdf9-205">Type:</span><span class="sxs-lookup"><span data-stu-id="7cdf9-205">Type:</span></span>
   
     `mpathconf --enable`
   
    <span data-ttu-id="7cdf9-206">Hallo bovenstaande opdracht maakt een `sample/etc/multipath.conf` bestand.</span><span class="sxs-lookup"><span data-stu-id="7cdf9-206">hello above command will create a `sample/etc/multipath.conf` file.</span></span>
2. <span data-ttu-id="7cdf9-207">Multipath-service starten.</span><span class="sxs-lookup"><span data-stu-id="7cdf9-207">Start multipath service.</span></span> <span data-ttu-id="7cdf9-208">Type:</span><span class="sxs-lookup"><span data-stu-id="7cdf9-208">Type:</span></span>
   
    `service multipathd start`
   
    <span data-ttu-id="7cdf9-209">Hier ziet u Hallo volgende uitvoer:</span><span class="sxs-lookup"><span data-stu-id="7cdf9-209">You will see hello following output:</span></span>
   
    `Starting multipathd daemon:`
3. <span data-ttu-id="7cdf9-210">Automatische detectie van multipaths inschakelen.</span><span class="sxs-lookup"><span data-stu-id="7cdf9-210">Enable automatic discovery of multipaths.</span></span> <span data-ttu-id="7cdf9-211">Type:</span><span class="sxs-lookup"><span data-stu-id="7cdf9-211">Type:</span></span>
   
    `mpathconf --find_multipaths y`
   
    <span data-ttu-id="7cdf9-212">Dit wijzigt Hallo standaardwaarden gedeelte van uw `multipath.conf` zoals hieronder wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="7cdf9-212">This will modify hello defaults section of your `multipath.conf` as shown below:</span></span>
   
        defaults {
        find_multipaths yes
        user_friendly_names yes
        path_grouping_policy multibus
        }

### <a name="step-2-configure-multipathing-for-storsimple-volumes"></a><span data-ttu-id="7cdf9-213">Stap 2: Configureer meerdere paden voor StorSimple-volumes</span><span class="sxs-lookup"><span data-stu-id="7cdf9-213">Step 2: Configure multipathing for StorSimple volumes</span></span>
<span data-ttu-id="7cdf9-214">Standaard worden alle apparaten zwart zijn vermeld in Hallo multipath.conf bestand en zal worden overgeslagen.</span><span class="sxs-lookup"><span data-stu-id="7cdf9-214">By default, all devices are black listed in hello multipath.conf file and will be bypassed.</span></span> <span data-ttu-id="7cdf9-215">U moet toocreate blacklist uitzonderingen tooallow gebruik van meerdere paden voor volumes van StorSimple-apparaten.</span><span class="sxs-lookup"><span data-stu-id="7cdf9-215">You will need toocreate blacklist exceptions tooallow multipathing for volumes from StorSimple devices.</span></span>

1. <span data-ttu-id="7cdf9-216">Hallo bewerken `/etc/mulitpath.conf` bestand.</span><span class="sxs-lookup"><span data-stu-id="7cdf9-216">Edit hello `/etc/mulitpath.conf` file.</span></span> <span data-ttu-id="7cdf9-217">Type:</span><span class="sxs-lookup"><span data-stu-id="7cdf9-217">Type:</span></span>
   
    `vi /etc/multipath.conf`
2. <span data-ttu-id="7cdf9-218">Hallo blacklist_exceptions sectie in Hallo multipath.conf bestand vinden.</span><span class="sxs-lookup"><span data-stu-id="7cdf9-218">Locate hello blacklist_exceptions section in hello multipath.conf file.</span></span> <span data-ttu-id="7cdf9-219">Uw StorSimple-apparaat moet toobe vermeld als een zwarte lijst uitzondering in deze sectie.</span><span class="sxs-lookup"><span data-stu-id="7cdf9-219">Your StorSimple device needs toobe listed as a blacklist exception in this section.</span></span> <span data-ttu-id="7cdf9-220">U kunt opmerkingen bij de relevante regels in dit bestand toomodify het hieronder (Gebruik alleen Hallo specifieke model van Hallo apparaat dat u gebruikt):</span><span class="sxs-lookup"><span data-stu-id="7cdf9-220">You can uncomment relevant lines in this file toomodify it as shown below (use only hello specific model of hello device you are using):</span></span>
   
        blacklist_exceptions {
            device {
                       vendor  "MSFT"
                       product "STORSIMPLE 8100*"
            }
            device {
                       vendor  "MSFT"
                       product "STORSIMPLE 8600*"
            }
           }

### <a name="step-3-configure-round-robin-multipathing"></a><span data-ttu-id="7cdf9-221">Stap 3: Gebruik van meerdere paden round robin configureren</span><span class="sxs-lookup"><span data-stu-id="7cdf9-221">Step 3: Configure round-robin multipathing</span></span>
<span data-ttu-id="7cdf9-222">Deze load balancing-algoritme maakt gebruik van alle Hallo beschikbaar multipaths toohello actieve controller taakverdeling, round-robin toewijst.</span><span class="sxs-lookup"><span data-stu-id="7cdf9-222">This load-balancing algorithm uses all hello available multipaths toohello active controller in a balanced, round-robin fashion.</span></span>

1. <span data-ttu-id="7cdf9-223">Hallo bewerken `/etc/multipath.conf` bestand.</span><span class="sxs-lookup"><span data-stu-id="7cdf9-223">Edit hello `/etc/multipath.conf` file.</span></span> <span data-ttu-id="7cdf9-224">Type:</span><span class="sxs-lookup"><span data-stu-id="7cdf9-224">Type:</span></span>
   
    `vi /etc/multipath.conf`
2. <span data-ttu-id="7cdf9-225">Onder Hallo `defaults` sectie, set Hallo `path_grouping_policy` te`multibus`.</span><span class="sxs-lookup"><span data-stu-id="7cdf9-225">Under hello `defaults` section, set hello `path_grouping_policy` too`multibus`.</span></span> <span data-ttu-id="7cdf9-226">Hallo `path_grouping_policy` Hallo standaard pad groepering beleid tooapply toounspecified multipaths bevat.</span><span class="sxs-lookup"><span data-stu-id="7cdf9-226">hello `path_grouping_policy` specifies hello default path grouping policy tooapply toounspecified multipaths.</span></span> <span data-ttu-id="7cdf9-227">Hallo standaardwaarden sectie eruit zoals hieronder wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="7cdf9-227">hello defaults section will look as shown below.</span></span>
   
        defaults {
                user_friendly_names yes
                path_grouping_policy multibus
        }

> [!NOTE]
> <span data-ttu-id="7cdf9-228">meest voorkomende waarden van Hallo `path_grouping_policy` omvatten:</span><span class="sxs-lookup"><span data-stu-id="7cdf9-228">hello most common values of `path_grouping_policy` include:</span></span>
> 
> * <span data-ttu-id="7cdf9-229">failover = 1 pad per groep prioriteit</span><span class="sxs-lookup"><span data-stu-id="7cdf9-229">failover = 1 path per priority group</span></span>
> * <span data-ttu-id="7cdf9-230">multibus = alle geldige paden in de groep 1 prioriteit</span><span class="sxs-lookup"><span data-stu-id="7cdf9-230">multibus = all valid paths in 1 priority group</span></span>
> 
> 

### <a name="step-4-enable-multipathing"></a><span data-ttu-id="7cdf9-231">Stap 4: Enable meerdere paden</span><span class="sxs-lookup"><span data-stu-id="7cdf9-231">Step 4: Enable multipathing</span></span>
1. <span data-ttu-id="7cdf9-232">Opnieuw opstarten Hallo `multipathd` daemon.</span><span class="sxs-lookup"><span data-stu-id="7cdf9-232">Restart hello `multipathd` daemon.</span></span> <span data-ttu-id="7cdf9-233">Type:</span><span class="sxs-lookup"><span data-stu-id="7cdf9-233">Type:</span></span>
   
    `service multipathd restart`
2. <span data-ttu-id="7cdf9-234">Hallo-uitvoer zijn zoals hieronder wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="7cdf9-234">hello output will be as shown below:</span></span>
   
        [root@centosSS ~]# service multipathd start
        Starting multipathd daemon:  [OK]

### <a name="step-5-verify-multipathing"></a><span data-ttu-id="7cdf9-235">Stap 5: Controleren of gebruik van meerdere paden</span><span class="sxs-lookup"><span data-stu-id="7cdf9-235">Step 5: Verify multipathing</span></span>
1. <span data-ttu-id="7cdf9-236">Eerst voor zorgen dat dat iSCSI-verbinding tot stand is gebracht met Hallo StorSimple-apparaat als volgt:</span><span class="sxs-lookup"><span data-stu-id="7cdf9-236">First make sure that iSCSI connection is established with hello StorSimple device as follows:</span></span>
   
   <span data-ttu-id="7cdf9-237">a.</span><span class="sxs-lookup"><span data-stu-id="7cdf9-237">a.</span></span> <span data-ttu-id="7cdf9-238">Detecteren van uw StorSimple-apparaat.</span><span class="sxs-lookup"><span data-stu-id="7cdf9-238">Discover your StorSimple device.</span></span> <span data-ttu-id="7cdf9-239">Type:</span><span class="sxs-lookup"><span data-stu-id="7cdf9-239">Type:</span></span>
      
    ```
    iscsiadm -m discovery -t sendtargets -p  <IP address of network interface on hello device>:<iSCSI port on StorSimple device>
    ```
    
    <span data-ttu-id="7cdf9-240">Hallo uitvoer wanneer IP-adres voor DATA0 10.126.162.25 en poort 3260 wordt geopend op Hallo StorSimple-apparaat voor uitgaande iSCSI-verkeer is zoals hieronder wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="7cdf9-240">hello output when IP address for DATA0 is 10.126.162.25 and port 3260 is opened on hello StorSimple device for outbound iSCSI traffic is as shown below:</span></span>
    
    ```
    10.126.162.25:3260,1 iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target
    10.126.162.26:3260,1 iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target
    ```

    <span data-ttu-id="7cdf9-241">Kopiëren Hallo IQN van uw StorSimple-apparaat `iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target`, van Hallo voorafgaand aan de uitvoer.</span><span class="sxs-lookup"><span data-stu-id="7cdf9-241">Copy hello IQN of your StorSimple device, `iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target`, from hello preceding output.</span></span>

   <span data-ttu-id="7cdf9-242">b.</span><span class="sxs-lookup"><span data-stu-id="7cdf9-242">b.</span></span> <span data-ttu-id="7cdf9-243">Verbinding maken met doel IQN toohello-apparaat.</span><span class="sxs-lookup"><span data-stu-id="7cdf9-243">Connect toohello device using target IQN.</span></span> <span data-ttu-id="7cdf9-244">Hallo StorSimple-apparaat is hier Hallo iSCSI-doel.</span><span class="sxs-lookup"><span data-stu-id="7cdf9-244">hello StorSimple device is hello iSCSI target here.</span></span> <span data-ttu-id="7cdf9-245">Type:</span><span class="sxs-lookup"><span data-stu-id="7cdf9-245">Type:</span></span>

    ```
    iscsiadm -m node --login -T <IQN of iSCSI target>
    ```

    <span data-ttu-id="7cdf9-246">Hallo volgende voorbeeld ziet u uitvoer met een doel IQN van `iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target`.</span><span class="sxs-lookup"><span data-stu-id="7cdf9-246">hello following example shows output with a target IQN of `iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target`.</span></span> <span data-ttu-id="7cdf9-247">Hallo-uitvoer geeft aan dat u verbinding hebt gemaakt toohello twee ingeschakeld voor iSCSI-netwerkinterfaces op uw apparaat.</span><span class="sxs-lookup"><span data-stu-id="7cdf9-247">hello output indicates that you have successfully connected toohello two iSCSI-enabled network interfaces on your device.</span></span>

    ```
    Logging in too[iface: eth0, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.25,3260] (multiple)
    Logging in too[iface: eth1, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.25,3260] (multiple)
    Logging in too[iface: eth0, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.26,3260] (multiple)
    Logging in too[iface: eth1, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.26,3260] (multiple)
    Login too[iface: eth0, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.25,3260] successful.
    Login too[iface: eth1, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.25,3260] successful.
    Login too[iface: eth0, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.26,3260] successful.
    Login too[iface: eth1, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.26,3260] successful.
    ```

    <span data-ttu-id="7cdf9-248">Als u slechts één host-interface en twee paden Hier ziet, moet u tooenable beide Hallo-interfaces op de host voor iSCSI.</span><span class="sxs-lookup"><span data-stu-id="7cdf9-248">If you see only one host interface and two paths here, then you need tooenable both hello interfaces on host for iSCSI.</span></span> <span data-ttu-id="7cdf9-249">U kunt volgen Hallo [gedetailleerde instructies in de documentatie van Linux](https://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/5/html/Online_Storage_Reconfiguration_Guide/iscsioffloadmain.html).</span><span class="sxs-lookup"><span data-stu-id="7cdf9-249">You can follow hello [detailed instructions in Linux documentation](https://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/5/html/Online_Storage_Reconfiguration_Guide/iscsioffloadmain.html).</span></span>

2. <span data-ttu-id="7cdf9-250">Een volume is blootgestelde toohello CentOS server uit Hallo StorSimple-apparaat.</span><span class="sxs-lookup"><span data-stu-id="7cdf9-250">A volume is exposed toohello CentOS server from hello StorSimple device.</span></span> <span data-ttu-id="7cdf9-251">Zie voor meer informatie [stap 6: een volume maken](storsimple-deployment-walkthrough.md#step-6-create-a-volume) via Hallo klassieke Azure-portal op uw StorSimple-apparaat.</span><span class="sxs-lookup"><span data-stu-id="7cdf9-251">For more information, see [Step 6: Create a volume](storsimple-deployment-walkthrough.md#step-6-create-a-volume) via hello Azure classic portal on your StorSimple device.</span></span>

3. <span data-ttu-id="7cdf9-252">Controleer of de beschikbare paden Hallo.</span><span class="sxs-lookup"><span data-stu-id="7cdf9-252">Verify hello available paths.</span></span> <span data-ttu-id="7cdf9-253">Type:</span><span class="sxs-lookup"><span data-stu-id="7cdf9-253">Type:</span></span>

      ```
      multipath –l
      ```

      <span data-ttu-id="7cdf9-254">Hallo volgende voorbeeld ziet u de uitvoer Hallo voor twee netwerkinterfaces op de netwerkinterface van StorSimple-apparaat verbonden tooa één host met twee beschikbare paden.</span><span class="sxs-lookup"><span data-stu-id="7cdf9-254">hello following example shows hello output for two network interfaces on a StorSimple device connected tooa single host network interface with two available paths.</span></span>

        ```
        mpathb (36486fd20cc081f8dcd3fccb992d45a68) dm-3 MSFT,STORSIMPLE 8100
        size=100G features='0' hwhandler='0' wp=rw
        `-+- policy='round-robin 0' prio=0 status=active
        |- 7:0:0:1 sdc 8:32 active undef running
        `- 6:0:0:1 sdd 8:48 active undef running
        ```

        hello following example shows hello output for two network interfaces on a StorSimple device connected tootwo host network interfaces with four available paths.

        ```
        mpathb (36486fd27a23feba1b096226f11420f6b) dm-2 MSFT,STORSIMPLE 8100
        size=100G features='0' hwhandler='0' wp=rw
        `-+- policy='round-robin 0' prio=0 status=active
        |- 17:0:0:0 sdb 8:16 active undef running
        |- 15:0:0:0 sdd 8:48 active undef running
        |- 14:0:0:0 sdc 8:32 active undef running
        `- 16:0:0:0 sde 8:64 active undef running
        ```

        After hello paths are configured, refer toohello specific instructions on your host operating system (Centos 6.6) toomount and format this volume.

## <a name="troubleshoot-multipathing"></a><span data-ttu-id="7cdf9-255">Problemen met meerdere paden</span><span class="sxs-lookup"><span data-stu-id="7cdf9-255">Troubleshoot multipathing</span></span>
<span data-ttu-id="7cdf9-256">Deze sectie bevat enkele nuttige tips als u problemen ondervindt tijdens het gebruik van meerdere paden configureren uitvoert.</span><span class="sxs-lookup"><span data-stu-id="7cdf9-256">This section provides some helpful tips if you run into any issues during multipathing configuration.</span></span>

<span data-ttu-id="7cdf9-257">Q.</span><span class="sxs-lookup"><span data-stu-id="7cdf9-257">Q.</span></span> <span data-ttu-id="7cdf9-258">Zie ik niet Hallo wijzigingen in `multipath.conf` bestand die van kracht.</span><span class="sxs-lookup"><span data-stu-id="7cdf9-258">I do not see hello changes in `multipath.conf` file taking effect.</span></span>

<span data-ttu-id="7cdf9-259">A.</span><span class="sxs-lookup"><span data-stu-id="7cdf9-259">A.</span></span> <span data-ttu-id="7cdf9-260">Als u toohello wijzigingen hebt aangebracht `multipath.conf` -bestand, moet u toorestart Hallo Multipath-service.</span><span class="sxs-lookup"><span data-stu-id="7cdf9-260">If you have made any changes toohello `multipath.conf` file, you will need toorestart hello multipathing service.</span></span> <span data-ttu-id="7cdf9-261">Type Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="7cdf9-261">Type hello following command:</span></span>

    service multipathd restart

<span data-ttu-id="7cdf9-262">Q.</span><span class="sxs-lookup"><span data-stu-id="7cdf9-262">Q.</span></span> <span data-ttu-id="7cdf9-263">Ik heb twee netwerkinterfaces op Hallo StorSimple-apparaat en twee netwerkinterfaces op de host Hallo ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="7cdf9-263">I have enabled two network interfaces on hello StorSimple device and two network interfaces on hello host.</span></span> <span data-ttu-id="7cdf9-264">Wanneer ik de lijst beschikbare paden hello, zie ik slechts twee paden.</span><span class="sxs-lookup"><span data-stu-id="7cdf9-264">When I list hello available paths, I see only two paths.</span></span> <span data-ttu-id="7cdf9-265">Toosee vier beschikbare paden wordt verwacht.</span><span class="sxs-lookup"><span data-stu-id="7cdf9-265">I expected toosee four available paths.</span></span>

<span data-ttu-id="7cdf9-266">A.</span><span class="sxs-lookup"><span data-stu-id="7cdf9-266">A.</span></span> <span data-ttu-id="7cdf9-267">Zorg ervoor dat Hallo twee paden op Hallo hetzelfde subnet en routeerbaar.</span><span class="sxs-lookup"><span data-stu-id="7cdf9-267">Make sure that hello two paths are on hello same subnet and routable.</span></span> <span data-ttu-id="7cdf9-268">Als de netwerkinterfaces Hallo zich op verschillende VLAN's en niet routeerbaar te maken, u slechts twee paden ziet.</span><span class="sxs-lookup"><span data-stu-id="7cdf9-268">If hello network interfaces are on different vLANs and not routable, you will see only two paths.</span></span> <span data-ttu-id="7cdf9-269">Eenzijdige tooverify dit is toomake ervoor dat u beide interfaces Hallo host van een netwerkinterface op Hallo StorSimple-apparaat kan bereiken.</span><span class="sxs-lookup"><span data-stu-id="7cdf9-269">One way tooverify this is toomake sure that you can reach both hello host interfaces from a network interface on hello StorSimple device.</span></span> <span data-ttu-id="7cdf9-270">U moet te[contact op met Microsoft Support](storsimple-contact-microsoft-support.md) zoals deze verificatie kan alleen worden uitgevoerd via een ondersteuningssessie voor.</span><span class="sxs-lookup"><span data-stu-id="7cdf9-270">You will need too[contact Microsoft Support](storsimple-contact-microsoft-support.md) as this verification can only be done via a support session.</span></span>

<span data-ttu-id="7cdf9-271">Q.</span><span class="sxs-lookup"><span data-stu-id="7cdf9-271">Q.</span></span> <span data-ttu-id="7cdf9-272">Wanneer ik de lijst beschikbare paden, zie ik niet geen uitvoer.</span><span class="sxs-lookup"><span data-stu-id="7cdf9-272">When I list available paths, I do not see any output.</span></span>

<span data-ttu-id="7cdf9-273">A.</span><span class="sxs-lookup"><span data-stu-id="7cdf9-273">A.</span></span> <span data-ttu-id="7cdf9-274">Normaal gesproken een probleem met de Hallo Multipath-daemon niet ziet multipathed paden voorgesteld en is waarschijnlijk dat hier probleem veroorzaakt door Hallo `multipath.conf` bestand.</span><span class="sxs-lookup"><span data-stu-id="7cdf9-274">Typically, not seeing any multipathed paths suggests a problem with hello multipathing daemon, and it’s most likely that any problem here lies in hello `multipath.conf` file.</span></span>

<span data-ttu-id="7cdf9-275">Het is ook waard controleren dat u daadwerkelijk een aantal schijven zien kunt nadat u hebt aangesloten toohello doel, omdat er geen reactie van Hallo multipath aanbiedingen kan ook betekenen er geen schijven.</span><span class="sxs-lookup"><span data-stu-id="7cdf9-275">It would also be worth checking that you can actually see some disks after connecting toohello target, as no response from hello multipath listings could also mean you don’t have any disks.</span></span>

* <span data-ttu-id="7cdf9-276">Gebruik Hallo opdracht toorescan Hallo SCSI-bus te volgen:</span><span class="sxs-lookup"><span data-stu-id="7cdf9-276">Use hello following command toorescan hello SCSI bus:</span></span>
  
    <span data-ttu-id="7cdf9-277">`$ rescan-scsi-bus.sh `(onderdeel van het pakket sg3_utils)</span><span class="sxs-lookup"><span data-stu-id="7cdf9-277">`$ rescan-scsi-bus.sh `(part of sg3_utils package)</span></span>
* <span data-ttu-id="7cdf9-278">Type Hallo volgende opdrachten:</span><span class="sxs-lookup"><span data-stu-id="7cdf9-278">Type hello following commands:</span></span>
  
    `$ dmesg | grep sd*`
     
     <span data-ttu-id="7cdf9-279">of</span><span class="sxs-lookup"><span data-stu-id="7cdf9-279">Or</span></span>
  
    `$ fdisk –l`
  
    <span data-ttu-id="7cdf9-280">Deze wordt details van onlangs toegevoegde schijven geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="7cdf9-280">These will return details of recently added disks.</span></span>
* <span data-ttu-id="7cdf9-281">toodetermine of het om een schijf StorSimple gebruiken Hallo volgende opdrachten:</span><span class="sxs-lookup"><span data-stu-id="7cdf9-281">toodetermine whether it is a StorSimple disk, use hello following commands:</span></span>
  
    `cat /sys/block/<DISK>/device/model`
  
    <span data-ttu-id="7cdf9-282">Hiermee wordt een tekenreeks, die bepaalt of het een StorSimple-schijf is geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="7cdf9-282">This will return a string, which will determine if it’s a StorSimple disk.</span></span>

<span data-ttu-id="7cdf9-283">Een minder waarschijnlijk maar mogelijke oorzaak kan ook worden de verlopen iscsid pid.</span><span class="sxs-lookup"><span data-stu-id="7cdf9-283">A less likely but possible cause could also be stale iscsid pid.</span></span> <span data-ttu-id="7cdf9-284">Hallo opdracht toolog volgende uitschakelen uit Hallo iSCSI-sessies gebruiken:</span><span class="sxs-lookup"><span data-stu-id="7cdf9-284">Use hello following command toolog off from hello iSCSI sessions:</span></span>

    iscsiadm -m node --logout -p <Target_IP>

<span data-ttu-id="7cdf9-285">Herhaal deze opdracht voor alle Hallo verbonden netwerkinterfaces op Hallo iSCSI target, dit uw StorSimple-apparaat is.</span><span class="sxs-lookup"><span data-stu-id="7cdf9-285">Repeat this command for all hello connected network interfaces on hello iSCSI target, which is your StorSimple device.</span></span> <span data-ttu-id="7cdf9-286">Nadat u afgemeld bij alle Hallo iSCSI-sessies bent, gebruikt u Hallo iSCSI-doel IQN tooreestablish Hallo iSCSI-sessie.</span><span class="sxs-lookup"><span data-stu-id="7cdf9-286">Once you have logged off from all hello iSCSI sessions, use hello iSCSI target IQN tooreestablish hello iSCSI session.</span></span> <span data-ttu-id="7cdf9-287">Type Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="7cdf9-287">Type hello following command:</span></span>

    iscsiadm -m node --login -T <TARGET_IQN>


<span data-ttu-id="7cdf9-288">Q.</span><span class="sxs-lookup"><span data-stu-id="7cdf9-288">Q.</span></span> <span data-ttu-id="7cdf9-289">Ik wil niet zeker weet of het apparaat wilt plaatsen is.</span><span class="sxs-lookup"><span data-stu-id="7cdf9-289">I am not sure if my device is whitelisted.</span></span>

<span data-ttu-id="7cdf9-290">A.</span><span class="sxs-lookup"><span data-stu-id="7cdf9-290">A.</span></span> <span data-ttu-id="7cdf9-291">tooverify of uw apparaat wilt plaatsen, is gebruik Hallo voor probleemoplossing interactief opdracht te volgen:</span><span class="sxs-lookup"><span data-stu-id="7cdf9-291">tooverify whether your device is whitelisted, use hello following troubleshooting interactive command:</span></span>

    multipathd –k
    multipathd> show devices
    available block devices:
    ram0 devnode blacklisted, unmonitored
    ram1 devnode blacklisted, unmonitored
    ram2 devnode blacklisted, unmonitored
    ram3 devnode blacklisted, unmonitored
    ram4 devnode blacklisted, unmonitored
    ram5 devnode blacklisted, unmonitored
    ram6 devnode blacklisted, unmonitored
    ram7 devnode blacklisted, unmonitored
    ram8 devnode blacklisted, unmonitored
    ram9 devnode blacklisted, unmonitored
    ram10 devnode blacklisted, unmonitored
    ram11 devnode blacklisted, unmonitored
    ram12 devnode blacklisted, unmonitored
    ram13 devnode blacklisted, unmonitored
    ram14 devnode blacklisted, unmonitored
    ram15 devnode blacklisted, unmonitored
    loop0 devnode blacklisted, unmonitored
    loop1 devnode blacklisted, unmonitored
    loop2 devnode blacklisted, unmonitored
    loop3 devnode blacklisted, unmonitored
    loop4 devnode blacklisted, unmonitored
    loop5 devnode blacklisted, unmonitored
    loop6 devnode blacklisted, unmonitored
    loop7 devnode blacklisted, unmonitored
    sr0 devnode blacklisted, unmonitored
    sda devnode whitelisted, monitored
    dm-0 devnode blacklisted, unmonitored
    dm-1 devnode blacklisted, unmonitored
    dm-2 devnode blacklisted, unmonitored
    sdb devnode whitelisted, monitored
    sdc devnode whitelisted, monitored
    dm-3 devnode blacklisted, unmonitored


<span data-ttu-id="7cdf9-292">Voor meer informatie gaat te[probleemoplossing interactief opdracht voor het gebruik van meerdere paden gebruiken](http://www.centos.org/docs/5/html/5.1/DM_Multipath/multipath_config_confirm.html).</span><span class="sxs-lookup"><span data-stu-id="7cdf9-292">For more information, go too[use troubleshooting interactive command for multipathing](http://www.centos.org/docs/5/html/5.1/DM_Multipath/multipath_config_confirm.html).</span></span>

## <a name="list-of-useful-commands"></a><span data-ttu-id="7cdf9-293">Lijst met opdrachten nuttig</span><span class="sxs-lookup"><span data-stu-id="7cdf9-293">List of useful commands</span></span>
| <span data-ttu-id="7cdf9-294">Type</span><span class="sxs-lookup"><span data-stu-id="7cdf9-294">Type</span></span> | <span data-ttu-id="7cdf9-295">Opdracht</span><span class="sxs-lookup"><span data-stu-id="7cdf9-295">Command</span></span> | <span data-ttu-id="7cdf9-296">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="7cdf9-296">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="7cdf9-297">**iSCSI**</span><span class="sxs-lookup"><span data-stu-id="7cdf9-297">**iSCSI**</span></span> |`service iscsid start` |<span data-ttu-id="7cdf9-298">ISCSI-service starten</span><span class="sxs-lookup"><span data-stu-id="7cdf9-298">Start iSCSI service</span></span> |
| &nbsp; |`service iscsid stop` |<span data-ttu-id="7cdf9-299">ISCSI-service stoppen</span><span class="sxs-lookup"><span data-stu-id="7cdf9-299">Stop iSCSI service</span></span> |
| &nbsp; |`service iscsid restart` |<span data-ttu-id="7cdf9-300">ISCSI-service opnieuw starten</span><span class="sxs-lookup"><span data-stu-id="7cdf9-300">Restart iSCSI service</span></span> |
| &nbsp; |`iscsiadm -m discovery -t sendtargets -p <TARGET_IP>` |<span data-ttu-id="7cdf9-301">Detecteren van beschikbare doelen op Hallo opgegeven adres</span><span class="sxs-lookup"><span data-stu-id="7cdf9-301">Discover available targets on hello specified address</span></span> |
| &nbsp; |`iscsiadm -m node --login -T <TARGET_IQN>` |<span data-ttu-id="7cdf9-302">Meld u bij toohello iSCSI-doel</span><span class="sxs-lookup"><span data-stu-id="7cdf9-302">Log in toohello iSCSI target</span></span> |
| &nbsp; |`iscsiadm -m node --logout -p <Target_IP>` |<span data-ttu-id="7cdf9-303">Meld u af van Hallo iSCSI-doel</span><span class="sxs-lookup"><span data-stu-id="7cdf9-303">Log out from hello iSCSI target</span></span> |
| &nbsp; |`cat /etc/iscsi/initiatorname.iscsi` |<span data-ttu-id="7cdf9-304">Naam van de iSCSI-initiator afdrukken</span><span class="sxs-lookup"><span data-stu-id="7cdf9-304">Print iSCSI initiator name</span></span> |
| &nbsp; |`iscsiadm –m session –s <sessionid> -P 3` |<span data-ttu-id="7cdf9-305">Controleer de status van de Hallo van Hallo iSCSI-sessie en het volume dat is gedetecteerd op Hallo host</span><span class="sxs-lookup"><span data-stu-id="7cdf9-305">Check hello state of hello iSCSI session and volume discovered on hello host</span></span> |
| &nbsp; |`iscsi –m session` |<span data-ttu-id="7cdf9-306">Bevat alle Hallo iSCSI-sessies tot stand gebracht tussen het Hallo-host en Hallo StorSimple-apparaat</span><span class="sxs-lookup"><span data-stu-id="7cdf9-306">Shows all hello iSCSI sessions established between hello host and hello StorSimple device</span></span> |
|  | | |
| <span data-ttu-id="7cdf9-307">**Gebruik van meerdere paden**</span><span class="sxs-lookup"><span data-stu-id="7cdf9-307">**Multipathing**</span></span> |`service multipathd start` |<span data-ttu-id="7cdf9-308">Multipath-daemon starten</span><span class="sxs-lookup"><span data-stu-id="7cdf9-308">Start multipath daemon</span></span> |
| &nbsp; |`service multipathd stop` |<span data-ttu-id="7cdf9-309">Multipath-daemon stoppen</span><span class="sxs-lookup"><span data-stu-id="7cdf9-309">Stop multipath daemon</span></span> |
| &nbsp; |`service multipathd restart` |<span data-ttu-id="7cdf9-310">Multipath-daemon starten</span><span class="sxs-lookup"><span data-stu-id="7cdf9-310">Restart multipath daemon</span></span> |
| &nbsp; |`chkconfig multipathd on` </br> <span data-ttu-id="7cdf9-311">OF</span><span class="sxs-lookup"><span data-stu-id="7cdf9-311">OR</span></span> </br> `mpathconf –with_chkconfig y` |<span data-ttu-id="7cdf9-312">Schakel multipath-daemon toostart tijdens het opstarten</span><span class="sxs-lookup"><span data-stu-id="7cdf9-312">Enable multipath daemon toostart at boot time</span></span> |
| &nbsp; |`multipathd –k` |<span data-ttu-id="7cdf9-313">Hallo interactieve console voor probleemoplossing starten</span><span class="sxs-lookup"><span data-stu-id="7cdf9-313">Start hello interactive console for troubleshooting</span></span> |
| &nbsp; |`multipath –l` |<span data-ttu-id="7cdf9-314">Lijst met meerdere paden verbindingen en apparaten</span><span class="sxs-lookup"><span data-stu-id="7cdf9-314">List multipath connections and devices</span></span> |
| &nbsp; |`mpathconf --enable` |<span data-ttu-id="7cdf9-315">Maken van een voorbeeldbestand mulitpath.conf in`/etc/mulitpath.conf`</span><span class="sxs-lookup"><span data-stu-id="7cdf9-315">Create a sample mulitpath.conf file in `/etc/mulitpath.conf`</span></span> |
|  | | |

## <a name="next-steps"></a><span data-ttu-id="7cdf9-316">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="7cdf9-316">Next steps</span></span>
<span data-ttu-id="7cdf9-317">Als u de MPIO op Linux-host configureert, moet u ook toorefer toohello CentoS 6.6 documenten te volgen:</span><span class="sxs-lookup"><span data-stu-id="7cdf9-317">As you are configuring MPIO on Linux host, you may also need toorefer toohello following CentoS 6.6 documents:</span></span>

* [<span data-ttu-id="7cdf9-318">Instellen van MPIO op CentOS</span><span class="sxs-lookup"><span data-stu-id="7cdf9-318">Setting up MPIO on CentOS</span></span>](http://www.centos.org/docs/5/html/5.1/DM_Multipath/setup_procedure.html)
* [<span data-ttu-id="7cdf9-319">Linux Training handleiding</span><span class="sxs-lookup"><span data-stu-id="7cdf9-319">Linux Training Guide</span></span>](http://linux-training.be/files/books/LinuxAdm.pdf)


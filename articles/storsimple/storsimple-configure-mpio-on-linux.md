---
title: MPIO op StorSimple Linux-host configureren | Microsoft Docs
description: MPIO configureren op verbonden met een Linux-host CentOS 6.6 met StorSimple
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
ms.openlocfilehash: add539351066f9ff94febeebfd5334773b360e8f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="configure-mpio-on-a-storsimple-host-running-centos"></a><span data-ttu-id="9fde3-103">MPIO configureren op een StorSimple-host waarop van CentOS</span><span class="sxs-lookup"><span data-stu-id="9fde3-103">Configure MPIO on a StorSimple host running CentOS</span></span>
<span data-ttu-id="9fde3-104">Dit artikel wordt uitgelegd hoe u Multipath I/O (MPIO) configureren op de hostserver Centos 6.6.</span><span class="sxs-lookup"><span data-stu-id="9fde3-104">This article explains the steps required to configure Multipathing IO (MPIO) on your Centos 6.6 host server.</span></span> <span data-ttu-id="9fde3-105">De host-server is verbonden met uw Microsoft Azure StorSimple-apparaat voor hoge beschikbaarheid via iSCSI-initiators.</span><span class="sxs-lookup"><span data-stu-id="9fde3-105">The host server is connected to your Microsoft Azure StorSimple device for high availability via iSCSI initiators.</span></span> <span data-ttu-id="9fde3-106">Deze beschrijving gedetailleerde van de automatische detectie van multipath-apparaten en de specifieke instellingen alleen van StorSimple-volumes.</span><span class="sxs-lookup"><span data-stu-id="9fde3-106">It describes in detail the automatic discovery of multipath devices and the specific setup only for StorSimple volumes.</span></span>

<span data-ttu-id="9fde3-107">Deze procedure is van toepassing op alle modellen van apparaten voor StorSimple 8000-serie.</span><span class="sxs-lookup"><span data-stu-id="9fde3-107">This procedure is applicable to all the models of StorSimple 8000 series devices.</span></span>

> [!NOTE]
> <span data-ttu-id="9fde3-108">Deze procedure kan niet worden gebruikt voor een virtueel StorSimple-apparaat.</span><span class="sxs-lookup"><span data-stu-id="9fde3-108">This procedure cannot be used for a StorSimple virtual device.</span></span> <span data-ttu-id="9fde3-109">Zie voor meer informatie het configureren van hostservers voor uw virtuele apparaat.</span><span class="sxs-lookup"><span data-stu-id="9fde3-109">For more information, see how to configure host servers for your virtual device.</span></span>
> 
> 

## <a name="about-multipathing"></a><span data-ttu-id="9fde3-110">Over het gebruik van meerdere paden</span><span class="sxs-lookup"><span data-stu-id="9fde3-110">About multipathing</span></span>
<span data-ttu-id="9fde3-111">De functie multipath kunt u meerdere i/o-paden tussen een hostserver en een opslagapparaat configureren.</span><span class="sxs-lookup"><span data-stu-id="9fde3-111">The multipathing feature allows you to configure multiple I/O paths between a host server and a storage device.</span></span> <span data-ttu-id="9fde3-112">Deze i/o-paden zijn fysieke SAN-verbindingen die afzonderlijke kabels, switches, netwerkinterfaces en domeincontrollers kunnen opnemen.</span><span class="sxs-lookup"><span data-stu-id="9fde3-112">These I/O paths are physical SAN connections that can include separate cables, switches, network interfaces, and controllers.</span></span> <span data-ttu-id="9fde3-113">Gebruik van meerdere paden cumuleert de i/o-paden voor het configureren van een nieuw apparaat dat is gekoppeld aan alle geaggregeerde paden.</span><span class="sxs-lookup"><span data-stu-id="9fde3-113">Multipathing aggregates the I/O paths, to configure a new device that is associated with all of the aggregated paths.</span></span>

<span data-ttu-id="9fde3-114">Het doel van het gebruik van meerdere paden is tweeledig:</span><span class="sxs-lookup"><span data-stu-id="9fde3-114">The purpose of multipathing is two-fold:</span></span>

* <span data-ttu-id="9fde3-115">**Hoge beschikbaarheid**: biedt een alternatief pad als elk element van het i/o-pad (zoals een kabel, switch, netwerkinterface of domeincontroller) is mislukt.</span><span class="sxs-lookup"><span data-stu-id="9fde3-115">**High availability**: It provides an alternate path if any element of the I/O path (such as a cable, switch, network interface, or controller) fails.</span></span>
* <span data-ttu-id="9fde3-116">**Taakverdeling**: afhankelijk van de configuratie van uw opslagapparaat, kan deze de prestaties verbeteren door de belasting op de i/o-paden te detecteren en dynamisch herverdeling de belasting.</span><span class="sxs-lookup"><span data-stu-id="9fde3-116">**Load balancing**: Depending on the configuration of your storage device, it can improve the performance by detecting loads on the I/O paths and dynamically rebalancing those loads.</span></span>

### <a name="about-multipathing-components"></a><span data-ttu-id="9fde3-117">Over het gebruik van meerdere paden onderdelen</span><span class="sxs-lookup"><span data-stu-id="9fde3-117">About multipathing components</span></span>
<span data-ttu-id="9fde3-118">Gebruik van meerdere paden in Linux bestaat uit de kernel als gebruikersruimte componenten zoals hieronder in een tabel.</span><span class="sxs-lookup"><span data-stu-id="9fde3-118">Multipathing in Linux consists of kernel components and user-space components as tabulated below.</span></span>

* <span data-ttu-id="9fde3-119">**Kernel**: het belangrijkste onderdeel is het *apparaat mapper* die wordt omgeleid i/o en failover voor paden en pad groepen ondersteunt.</span><span class="sxs-lookup"><span data-stu-id="9fde3-119">**Kernel**: The main component is the *device-mapper* that reroutes I/O and supports failover for paths and path groups.</span></span>

* <span data-ttu-id="9fde3-120">**Gebruikersruimte innemen**: dit zijn *multipath-tools* die multipathed apparaten beheren door de multipath apparaat mapper-module wat te doen.</span><span class="sxs-lookup"><span data-stu-id="9fde3-120">**User-space**: These are *multipath-tools* that manage multipathed devices by instructing the device-mapper multipath module what to do.</span></span> <span data-ttu-id="9fde3-121">De hulpprogramma's bestaan uit:</span><span class="sxs-lookup"><span data-stu-id="9fde3-121">The tools consist of:</span></span>
   
   * <span data-ttu-id="9fde3-122">**Multipath**: geeft een lijst van en multipathed apparaten configureert.</span><span class="sxs-lookup"><span data-stu-id="9fde3-122">**Multipath**: lists and configures multipathed devices.</span></span>
   * <span data-ttu-id="9fde3-123">**Multipathd**: daemon die wordt uitgevoerd multipath en bewaakt de paden.</span><span class="sxs-lookup"><span data-stu-id="9fde3-123">**Multipathd**: daemon that executes multipath and monitors the paths.</span></span>
   * <span data-ttu-id="9fde3-124">**Naam van de Devmap**: biedt een zinvolle apparaatnaam naar udev voor devmaps.</span><span class="sxs-lookup"><span data-stu-id="9fde3-124">**Devmap-name**: provides a meaningful device-name to udev for devmaps.</span></span>
   * <span data-ttu-id="9fde3-125">**Kpartx**: lineaire devmaps wordt toegewezen aan de partities die apparaten kunnen multipath maps partitioneerbare.</span><span class="sxs-lookup"><span data-stu-id="9fde3-125">**Kpartx**: maps linear devmaps to device partitions to make multipath maps partitionable.</span></span>
   * <span data-ttu-id="9fde3-126">**Multipath.conf**: configuratiebestand voor multipath-daemon die wordt gebruikt voor de configuratietabel van de ingebouwde overschreven.</span><span class="sxs-lookup"><span data-stu-id="9fde3-126">**Multipath.conf**: configuration file for multipath daemon that is used to overwrite the built-in configuration table.</span></span>

### <a name="about-the-multipathconf-configuration-file"></a><span data-ttu-id="9fde3-127">Over het configuratiebestand multipath.conf</span><span class="sxs-lookup"><span data-stu-id="9fde3-127">About the multipath.conf configuration file</span></span>
<span data-ttu-id="9fde3-128">Het configuratiebestand `/etc/multipath.conf` kunt u veel van de functies van het gebruik van meerdere paden gebruiker worden geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="9fde3-128">The configuration file `/etc/multipath.conf` makes many of the multipathing features user-configurable.</span></span> <span data-ttu-id="9fde3-129">De `multipath` opdracht en de kernel-daemon `multipathd` gebruik informatie gevonden in dit bestand.</span><span class="sxs-lookup"><span data-stu-id="9fde3-129">The `multipath` command and the kernel daemon `multipathd` use information found in this file.</span></span> <span data-ttu-id="9fde3-130">Het bestand is alleen tijdens de configuratie van de apparaten multipath geraadpleegd.</span><span class="sxs-lookup"><span data-stu-id="9fde3-130">The file is consulted only during the configuration of the multipath devices.</span></span> <span data-ttu-id="9fde3-131">Zorg ervoor dat alle wijzigingen worden aangebracht voordat u de `multipath` opdracht.</span><span class="sxs-lookup"><span data-stu-id="9fde3-131">Make sure that all changes are made before you run the `multipath` command.</span></span> <span data-ttu-id="9fde3-132">Als u het bestand later wijzigt, moet u stoppen en starten multipathd opnieuw om de wijzigingen van kracht te laten worden.</span><span class="sxs-lookup"><span data-stu-id="9fde3-132">If you modify the file afterwards, you will need to stop and start multipathd again for the changes to take effect.</span></span>

<span data-ttu-id="9fde3-133">De multipath.conf heeft vijf secties:</span><span class="sxs-lookup"><span data-stu-id="9fde3-133">The multipath.conf has five sections:</span></span>

- <span data-ttu-id="9fde3-134">**Niveau standaardsysteemwaarden** *(standaardwaarden)*: U kunt niveau standaardwaarden van het systeem onderdrukken.</span><span class="sxs-lookup"><span data-stu-id="9fde3-134">**System level defaults** *(defaults)*: You can override system level defaults.</span></span>
- <span data-ttu-id="9fde3-135">**Apparaten gebeurd** *(blacklist)*: U kunt de lijst met apparaten die niet moeten worden beheerd door apparaat mapper opgeven.</span><span class="sxs-lookup"><span data-stu-id="9fde3-135">**Blacklisted devices** *(blacklist)*: You can specify the list of devices that should not be controlled by device-mapper.</span></span>
- <span data-ttu-id="9fde3-136">**Uitzonderingen afgekeurde** *(blacklist_exceptions)*: U specifieke apparaten moet worden behandeld als multipath apparaten, zelfs als die worden vermeld in de zwarte lijst kunt identificeren.</span><span class="sxs-lookup"><span data-stu-id="9fde3-136">**Blacklist exceptions** *(blacklist_exceptions)*: You can identify specific devices to be treated as multipath devices even if listed in the blacklist.</span></span>
- <span data-ttu-id="9fde3-137">**Specifieke instellingen voor de controller opslag** *(apparaten)*: U kunt configuratieinstellingen die worden toegepast op apparaten met de leverancier-en productinformatie opgeven.</span><span class="sxs-lookup"><span data-stu-id="9fde3-137">**Storage controller specific settings** *(devices)*: You can specify configuration settings that will be applied to devices that have Vendor and Product information.</span></span>
- <span data-ttu-id="9fde3-138">**Specifieke apparaatinstellingen** *(multipaths)*: U kunt in deze sectie verfijnen van de configuratie-instellingen voor afzonderlijke LUN's.</span><span class="sxs-lookup"><span data-stu-id="9fde3-138">**Device specific settings** *(multipaths)*: You can use this section to fine-tune the configuration settings for individual LUNs.</span></span>

## <a name="configure-multipathing-on-storsimple-connected-to-linux-host"></a><span data-ttu-id="9fde3-139">Gebruik van meerdere paden op StorSimple die zijn verbonden met het Linux-host configureren</span><span class="sxs-lookup"><span data-stu-id="9fde3-139">Configure multipathing on StorSimple connected to Linux host</span></span>
<span data-ttu-id="9fde3-140">Een StorSimple-apparaat is verbonden met een Linux-host kan worden geconfigureerd voor hoge beschikbaarheid en taakverdeling.</span><span class="sxs-lookup"><span data-stu-id="9fde3-140">A StorSimple device connected to a Linux host can be configured for high availability and load balancing.</span></span> <span data-ttu-id="9fde3-141">Bijvoorbeeld, als de Linux-host twee interfaces zijn verbonden met het SAN heeft en het apparaat twee interfaces zijn verbonden met het SAN heeft, dat deze interfaces op hetzelfde subnet bevinden worden, wordt er 4 paden beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="9fde3-141">For example, if the Linux host has two interfaces connected to the SAN and the device has two interfaces connected to the SAN such that these interfaces are on the same subnet, then there will be 4 paths available.</span></span> <span data-ttu-id="9fde3-142">Echter, als elke interface gegevens op het apparaat en host-interface op een ander IP-subnet (en niet-routeerbaar), vervolgens alleen 2 paden zijn beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="9fde3-142">However, if each DATA interface on the device and host interface are on a different IP subnet (and not routable), then only 2 paths will be available.</span></span> <span data-ttu-id="9fde3-143">U kunt meerdere paden voor het automatisch detecteren van de beschikbare paden, kiest u een taakverdelingsalgoritme voor die paden, toepassen specifieke configuratie-instellingen voor alleen-StorSimple-volumes, en vervolgens inschakelen en controleren van meerdere paden configureren.</span><span class="sxs-lookup"><span data-stu-id="9fde3-143">You can configure multipathing to automatically discover all the available paths, choose a load-balancing algorithm for those paths, apply specific configuration settings for StorSimple-only volumes, and then enable and verify multipathing.</span></span>

<span data-ttu-id="9fde3-144">De volgende procedure beschrijft het gebruik van meerdere paden configureren wanneer een StorSimple-apparaat met twee netwerkinterfaces is verbonden met een host met twee netwerkinterfaces.</span><span class="sxs-lookup"><span data-stu-id="9fde3-144">The following procedure describes how to configure multipathing when a StorSimple device with two network interfaces is connected to a host with two network interfaces.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9fde3-145">Vereisten</span><span class="sxs-lookup"><span data-stu-id="9fde3-145">Prerequisites</span></span>
<span data-ttu-id="9fde3-146">Deze sectie beschrijft de configuratievereisten voor CentOS-server en het StorSimple-apparaat.</span><span class="sxs-lookup"><span data-stu-id="9fde3-146">This section details the configuration prerequisites for CentOS server and your StorSimple device.</span></span>

### <a name="on-centos-host"></a><span data-ttu-id="9fde3-147">Op de host CentOS</span><span class="sxs-lookup"><span data-stu-id="9fde3-147">On CentOS host</span></span>
1. <span data-ttu-id="9fde3-148">Zorg ervoor dat uw CentOS-host 2 netwerkinterfaces ingeschakeld heeft.</span><span class="sxs-lookup"><span data-stu-id="9fde3-148">Make sure that your CentOS host has 2 network interfaces enabled.</span></span> <span data-ttu-id="9fde3-149">Type:</span><span class="sxs-lookup"><span data-stu-id="9fde3-149">Type:</span></span>
   
    `ifconfig`
   
    <span data-ttu-id="9fde3-150">Het volgende voorbeeld ziet u de uitvoer wanneer twee netwerkinterfaces (`eth0` en `eth1`) aanwezig zijn op de host.</span><span class="sxs-lookup"><span data-stu-id="9fde3-150">The following example shows the output when two network interfaces (`eth0` and `eth1`) are present on the host.</span></span>
   
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
2. <span data-ttu-id="9fde3-151">Installeer *iSCSI-initiator-utils* op uw server CentOS.</span><span class="sxs-lookup"><span data-stu-id="9fde3-151">Install *iSCSI-initiator-utils* on your CentOS server.</span></span> <span data-ttu-id="9fde3-152">Voer de volgende stappen uit voor het installeren van *iSCSI-initiator-utils*.</span><span class="sxs-lookup"><span data-stu-id="9fde3-152">Perform the following steps to install *iSCSI-initiator-utils*.</span></span>
   
   1. <span data-ttu-id="9fde3-153">Meld u aan als `root` in uw CentOS-host.</span><span class="sxs-lookup"><span data-stu-id="9fde3-153">Log on as `root` into your CentOS host.</span></span>
   2. <span data-ttu-id="9fde3-154">Installeer de *iSCSI-initiator-utils*.</span><span class="sxs-lookup"><span data-stu-id="9fde3-154">Install the *iSCSI-initiator-utils*.</span></span> <span data-ttu-id="9fde3-155">Type:</span><span class="sxs-lookup"><span data-stu-id="9fde3-155">Type:</span></span>
      
       `yum install iscsi-initiator-utils`
   3. <span data-ttu-id="9fde3-156">Na de *iSCSI-Initiator-utils* met succes is geïnstalleerd, start de iSCSI-service.</span><span class="sxs-lookup"><span data-stu-id="9fde3-156">After the *iSCSI-Initiator-utils* is successfully installed, start the iSCSI service.</span></span> <span data-ttu-id="9fde3-157">Type:</span><span class="sxs-lookup"><span data-stu-id="9fde3-157">Type:</span></span>
      
       `service iscsid start`
      
       <span data-ttu-id="9fde3-158">In gevallen `iscsid` mogelijk niet daadwerkelijk wordt gestart en de `--force` optie zijn mogelijk vereist</span><span class="sxs-lookup"><span data-stu-id="9fde3-158">On occasions, `iscsid` may not actually start and the `--force` option may be needed</span></span>
   4. <span data-ttu-id="9fde3-159">Om ervoor te zorgen dat uw iSCSI-initiator tijdens het opstarten is ingeschakeld, gebruikt u de `chkconfig` opdracht uit om de service.</span><span class="sxs-lookup"><span data-stu-id="9fde3-159">To ensure that your iSCSI initiator is enabled during boot time, use the `chkconfig` command to enable the service.</span></span>
      
       `chkconfig iscsi on`
   5. <span data-ttu-id="9fde3-160">Om te verifiëren dat het goed is ingesteld, moet u de opdracht uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="9fde3-160">To verify that that it was properly setup, run the command:</span></span>
      
       `chkconfig --list | grep iscsi`
      
       <span data-ttu-id="9fde3-161">Hieronder ziet u een voorbeeld van de uitvoer.</span><span class="sxs-lookup"><span data-stu-id="9fde3-161">A sample output is shown below.</span></span>
      
           iscsi   0:off   1:off   2:on3:on4:on5:on6:off
           iscsid  0:off   1:off   2:on3:on4:on5:on6:off
      
       <span data-ttu-id="9fde3-162">In het bovenstaande voorbeeld ziet u dat uw omgeving iSCSI op opstarten op uitvoeren niveaus 2, 3, 4 en 5 wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="9fde3-162">From the above example, you can see that your iSCSI environment will run on boot time on run levels 2, 3, 4, and 5.</span></span>
3. <span data-ttu-id="9fde3-163">Installeer *apparaat-mapper-multipath*.</span><span class="sxs-lookup"><span data-stu-id="9fde3-163">Install *device-mapper-multipath*.</span></span> <span data-ttu-id="9fde3-164">Type:</span><span class="sxs-lookup"><span data-stu-id="9fde3-164">Type:</span></span>
   
    `yum install device-mapper-multipath`
   
    <span data-ttu-id="9fde3-165">De installatie wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="9fde3-165">The installation will start.</span></span> <span data-ttu-id="9fde3-166">Type **Y** om door te gaan wanneer u om bevestiging wordt gevraagd.</span><span class="sxs-lookup"><span data-stu-id="9fde3-166">Type **Y** to continue when prompted for confirmation.</span></span>

### <a name="on-storsimple-device"></a><span data-ttu-id="9fde3-167">Op het StorSimple-apparaat</span><span class="sxs-lookup"><span data-stu-id="9fde3-167">On StorSimple device</span></span>
<span data-ttu-id="9fde3-168">Uw StorSimple-apparaat moet hebben:</span><span class="sxs-lookup"><span data-stu-id="9fde3-168">Your StorSimple device should have:</span></span>

* <span data-ttu-id="9fde3-169">Minimaal twee interfaces zijn ingeschakeld voor iSCSI.</span><span class="sxs-lookup"><span data-stu-id="9fde3-169">A minimum of two interfaces enabled for iSCSI.</span></span> <span data-ttu-id="9fde3-170">Om te controleren dat twee interfaces ingeschakeld voor iSCSI op uw StorSimple-apparaat zijn, moet u de volgende stappen uitvoeren in de klassieke Azure portal voor uw StorSimple-apparaat:</span><span class="sxs-lookup"><span data-stu-id="9fde3-170">To verify that two interfaces are iSCSI-enabled on your StorSimple device, perform the following steps in the Azure classic portal for your StorSimple device:</span></span>
  
  1. <span data-ttu-id="9fde3-171">Meld u aan bij de klassieke portal voor uw StorSimple-apparaat.</span><span class="sxs-lookup"><span data-stu-id="9fde3-171">Log into the classic portal for your StorSimple device.</span></span>
  2. <span data-ttu-id="9fde3-172">Selecteer uw StorSimple Manager-service, klikt u op **apparaten** en kies de specifieke StorSimple-apparaat.</span><span class="sxs-lookup"><span data-stu-id="9fde3-172">Select your StorSimple Manager service, click **Devices** and choose the specific StorSimple device.</span></span> <span data-ttu-id="9fde3-173">Klik op **configureren** en controleer of de netwerkinterface-instellingen.</span><span class="sxs-lookup"><span data-stu-id="9fde3-173">Click **Configure** and verify the network interface settings.</span></span> <span data-ttu-id="9fde3-174">Een schermafbeelding met twee netwerkinterfaces zijn ingeschakeld voor iSCSI-worden hieronder weergegeven.</span><span class="sxs-lookup"><span data-stu-id="9fde3-174">A screenshot with two iSCSI-enabled network interfaces is shown below.</span></span> <span data-ttu-id="9fde3-175">Hier DATA 2 en DATA 3, beide 10 GbE interfaces zijn ingeschakeld voor iSCSI.</span><span class="sxs-lookup"><span data-stu-id="9fde3-175">Here DATA 2 and DATA 3, both 10 GbE interfaces are enabled for iSCSI.</span></span>
     
      ![Configuratie van MPIO StorsSimple DATA 2](./media/storsimple-configure-mpio-on-linux/IC761347.png)
     
      ![MPIO StorSimple gegevens 3 Config](./media/storsimple-configure-mpio-on-linux/IC761348.png)
     
      <span data-ttu-id="9fde3-178">In de **configureren** pagina</span><span class="sxs-lookup"><span data-stu-id="9fde3-178">In the **Configure** page</span></span>
     
     1. <span data-ttu-id="9fde3-179">Zorg ervoor dat beide netwerkinterfaces iSCSI-functionaliteit.</span><span class="sxs-lookup"><span data-stu-id="9fde3-179">Ensure that both network interfaces are iSCSI-enabled.</span></span> <span data-ttu-id="9fde3-180">De **iSCSI ingeschakeld** veld moet worden ingesteld op **Ja**.</span><span class="sxs-lookup"><span data-stu-id="9fde3-180">The **iSCSI enabled** field should be set to **Yes**.</span></span>
     2. <span data-ttu-id="9fde3-181">Zorg dat de netwerkinterfaces hebben dezelfde snelheid, of beide moet 1 GbE- of 10 GbE.</span><span class="sxs-lookup"><span data-stu-id="9fde3-181">Ensure that the network interfaces have the same speed, both should be 1 GbE or 10 GbE.</span></span>
     3. <span data-ttu-id="9fde3-182">Noteer de IPv4-adressen van de interfaces iSCSI-functionaliteit en opslaan voor toekomstig gebruik op de host.</span><span class="sxs-lookup"><span data-stu-id="9fde3-182">Note the IPv4 addresses of the iSCSI-enabled interfaces and save for later use on the host.</span></span>
* <span data-ttu-id="9fde3-183">De iSCSI-interfaces op uw StorSimple-apparaat moet bereikbaar is vanaf de CentOS-server.</span><span class="sxs-lookup"><span data-stu-id="9fde3-183">The iSCSI interfaces on your StorSimple device should be reachable from the CentOS server.</span></span>
      <span data-ttu-id="9fde3-184">Om dit te controleren, moet u de IP-adressen van uw StorSimple iSCSI-functionaliteit netwerkinterfaces op uw host-server opgeven.</span><span class="sxs-lookup"><span data-stu-id="9fde3-184">To verify this, you need to provide the IP addresses of your StorSimple iSCSI-enabled network interfaces on your host server.</span></span> <span data-ttu-id="9fde3-185">De opdrachten die worden gebruikt en de bijbehorende uitvoer met DATA2 (10.126.162.25) en DATA3 (10.126.162.26) worden hieronder weergegeven:</span><span class="sxs-lookup"><span data-stu-id="9fde3-185">The commands used and the corresponding output with DATA2 (10.126.162.25) and DATA3 (10.126.162.26) is shown below:</span></span>
  
        [root@centosSS ~]# iscsiadm -m discovery -t sendtargets -p 10.126.162.25:3260
        10.126.162.25:3260,1 iqn.1991-05.com.microsoft:storsimple8100-shx0991003g44mt-target
        10.126.162.26:3260,1 iqn.1991-05.com.microsoft:storsimple8100-shx0991003g44mt-target

### <a name="hardware-configuration"></a><span data-ttu-id="9fde3-186">Hardwareconfiguratie</span><span class="sxs-lookup"><span data-stu-id="9fde3-186">Hardware configuration</span></span>
<span data-ttu-id="9fde3-187">Het is raadzaam dat u verbinding de twee iSCSI-netwerkinterfaces op afzonderlijke paden voor de redundantie maakt.</span><span class="sxs-lookup"><span data-stu-id="9fde3-187">We recommend that you connect the two iSCSI network interfaces on separate paths for redundancy.</span></span> <span data-ttu-id="9fde3-188">De onderstaande afbeelding ziet u de aanbevolen hardwareconfiguratie voor hoge beschikbaarheid en taakverdeling gebruik van meerdere paden voor uw CentOS-server en het StorSimple-apparaat.</span><span class="sxs-lookup"><span data-stu-id="9fde3-188">The figure below shows the recommended hardware configuration for high availability and load-balancing multipathing for your CentOS server and StorSimple device.</span></span>

![MPIO hardwareconfiguratie voor StorSimple Linux-host](./media/storsimple-configure-mpio-on-linux/MPIOHardwareConfigurationStorSimpleToLinuxHost2M.png)

<span data-ttu-id="9fde3-190">Zoals u in de voorgaande afbeelding:</span><span class="sxs-lookup"><span data-stu-id="9fde3-190">As shown in the preceding figure:</span></span>

* <span data-ttu-id="9fde3-191">Uw StorSimple-apparaat zich in een actief / passief-configuratie met twee domeincontrollers.</span><span class="sxs-lookup"><span data-stu-id="9fde3-191">Your StorSimple device is in an active-passive configuration with two controllers.</span></span>
* <span data-ttu-id="9fde3-192">Twee SAN-switches zijn verbonden met uw apparaat-domeincontrollers.</span><span class="sxs-lookup"><span data-stu-id="9fde3-192">Two SAN switches are connected to your device controllers.</span></span>
* <span data-ttu-id="9fde3-193">Twee iSCSI-initiators zijn ingeschakeld op uw StorSimple-apparaat.</span><span class="sxs-lookup"><span data-stu-id="9fde3-193">Two iSCSI initiators are enabled on your StorSimple device.</span></span>
* <span data-ttu-id="9fde3-194">Twee netwerkinterfaces zijn ingeschakeld op uw host CentOS.</span><span class="sxs-lookup"><span data-stu-id="9fde3-194">Two network interfaces are enabled on your CentOS host.</span></span>

<span data-ttu-id="9fde3-195">De bovenstaande configuratie resulteert 4 afzonderlijke paden tussen het apparaat en de host als de host- en interfaces routeerbaar zijn.</span><span class="sxs-lookup"><span data-stu-id="9fde3-195">The above configuration will yield 4 separate paths between your device and the host if the host and data interfaces are routable.</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="9fde3-196">Het is raadzaam dat u niet door elkaar 1 GbE- en 10 GbE-netwerkinterfaces voor gebruik van meerdere paden.</span><span class="sxs-lookup"><span data-stu-id="9fde3-196">We recommend that you do not mix 1 GbE and 10 GbE network interfaces for multipathing.</span></span> <span data-ttu-id="9fde3-197">Wanneer u twee netwerkinterfaces, moet de interfaces die zowel het identieke type.</span><span class="sxs-lookup"><span data-stu-id="9fde3-197">When using two network interfaces, both the interfaces should be the identical type.</span></span>
> * <span data-ttu-id="9fde3-198">Op uw StorSimple-apparaat DATA0, bestand1, DATA4 en DATA5 zijn 1 GbE-interfaces DATA2 en DATA3 10 GbE-netwerkinterfaces zijn. |</span><span class="sxs-lookup"><span data-stu-id="9fde3-198">On your StorSimple device, DATA0, DATA1, DATA4 and DATA5 are 1 GbE interfaces whereas DATA2 and DATA3 are 10 GbE network interfaces.|</span></span>
> 
> 

## <a name="configuration-steps"></a><span data-ttu-id="9fde3-199">Configuratiestappen</span><span class="sxs-lookup"><span data-stu-id="9fde3-199">Configuration steps</span></span>
<span data-ttu-id="9fde3-200">De configuratiestappen voor gebruik van meerdere paden betrekking hebben op voor het configureren van de beschikbare paden voor automatische detectie, geven de taakverdelingsalgoritme moet worden gebruikt, gebruik van meerdere paden inschakelen en ten slotte de configuratie te controleren.</span><span class="sxs-lookup"><span data-stu-id="9fde3-200">The configuration steps for multipathing involve configuring the available paths for automatic discovery, specifying the load-balancing algorithm to use, enabling multipathing and finally verifying the configuration.</span></span> <span data-ttu-id="9fde3-201">Elk van deze stappen wordt uitgebreid beschreven in de volgende secties.</span><span class="sxs-lookup"><span data-stu-id="9fde3-201">Each of these steps is discussed in detail in the following sections.</span></span>

### <a name="step-1-configure-multipathing-for-automatic-discovery"></a><span data-ttu-id="9fde3-202">Stap 1: Configureer meerdere paden voor automatische detectie</span><span class="sxs-lookup"><span data-stu-id="9fde3-202">Step 1: Configure multipathing for automatic discovery</span></span>
<span data-ttu-id="9fde3-203">De multipath-ondersteunde apparaten kunnen automatisch worden gedetecteerd en geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="9fde3-203">The multipath-supported devices can be automatically discovered and configured.</span></span>

1. <span data-ttu-id="9fde3-204">Initialiseren `/etc/multipath.conf` bestand.</span><span class="sxs-lookup"><span data-stu-id="9fde3-204">Initialize `/etc/multipath.conf` file.</span></span> <span data-ttu-id="9fde3-205">Type:</span><span class="sxs-lookup"><span data-stu-id="9fde3-205">Type:</span></span>
   
     `mpathconf --enable`
   
    <span data-ttu-id="9fde3-206">De bovenstaande opdracht maakt een `sample/etc/multipath.conf` bestand.</span><span class="sxs-lookup"><span data-stu-id="9fde3-206">The above command will create a `sample/etc/multipath.conf` file.</span></span>
2. <span data-ttu-id="9fde3-207">Multipath-service starten.</span><span class="sxs-lookup"><span data-stu-id="9fde3-207">Start multipath service.</span></span> <span data-ttu-id="9fde3-208">Type:</span><span class="sxs-lookup"><span data-stu-id="9fde3-208">Type:</span></span>
   
    `service multipathd start`
   
    <span data-ttu-id="9fde3-209">Hier ziet u de volgende uitvoer:</span><span class="sxs-lookup"><span data-stu-id="9fde3-209">You will see the following output:</span></span>
   
    `Starting multipathd daemon:`
3. <span data-ttu-id="9fde3-210">Automatische detectie van multipaths inschakelen.</span><span class="sxs-lookup"><span data-stu-id="9fde3-210">Enable automatic discovery of multipaths.</span></span> <span data-ttu-id="9fde3-211">Type:</span><span class="sxs-lookup"><span data-stu-id="9fde3-211">Type:</span></span>
   
    `mpathconf --find_multipaths y`
   
    <span data-ttu-id="9fde3-212">Dit wordt wijzigt u de sectie standaardinstellingen van uw `multipath.conf` zoals hieronder wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="9fde3-212">This will modify the defaults section of your `multipath.conf` as shown below:</span></span>
   
        defaults {
        find_multipaths yes
        user_friendly_names yes
        path_grouping_policy multibus
        }

### <a name="step-2-configure-multipathing-for-storsimple-volumes"></a><span data-ttu-id="9fde3-213">Stap 2: Configureer meerdere paden voor StorSimple-volumes</span><span class="sxs-lookup"><span data-stu-id="9fde3-213">Step 2: Configure multipathing for StorSimple volumes</span></span>
<span data-ttu-id="9fde3-214">Standaard worden alle apparaten zwart zijn vermeld in het bestand multipath.conf en zal worden overgeslagen.</span><span class="sxs-lookup"><span data-stu-id="9fde3-214">By default, all devices are black listed in the multipath.conf file and will be bypassed.</span></span> <span data-ttu-id="9fde3-215">U moet een zwarte lijst uitzonderingen zodat meerdere paden voor volumes van StorSimple-apparaten maken.</span><span class="sxs-lookup"><span data-stu-id="9fde3-215">You will need to create blacklist exceptions to allow multipathing for volumes from StorSimple devices.</span></span>

1. <span data-ttu-id="9fde3-216">Bewerk de `/etc/mulitpath.conf` bestand.</span><span class="sxs-lookup"><span data-stu-id="9fde3-216">Edit the `/etc/mulitpath.conf` file.</span></span> <span data-ttu-id="9fde3-217">Type:</span><span class="sxs-lookup"><span data-stu-id="9fde3-217">Type:</span></span>
   
    `vi /etc/multipath.conf`
2. <span data-ttu-id="9fde3-218">Zoek de blacklist_exceptions-sectie in het bestand multipath.conf.</span><span class="sxs-lookup"><span data-stu-id="9fde3-218">Locate the blacklist_exceptions section in the multipath.conf file.</span></span> <span data-ttu-id="9fde3-219">Uw StorSimple-apparaat moet worden weergegeven als een zwarte lijst uitzondering in deze sectie.</span><span class="sxs-lookup"><span data-stu-id="9fde3-219">Your StorSimple device needs to be listed as a blacklist exception in this section.</span></span> <span data-ttu-id="9fde3-220">U kunt opmerkingen bij relevante regels in dit bestand te wijzigen zoals hieronder (Gebruik alleen het specifieke model van het apparaat dat u gebruikt):</span><span class="sxs-lookup"><span data-stu-id="9fde3-220">You can uncomment relevant lines in this file to modify it as shown below (use only the specific model of the device you are using):</span></span>
   
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

### <a name="step-3-configure-round-robin-multipathing"></a><span data-ttu-id="9fde3-221">Stap 3: Gebruik van meerdere paden round robin configureren</span><span class="sxs-lookup"><span data-stu-id="9fde3-221">Step 3: Configure round-robin multipathing</span></span>
<span data-ttu-id="9fde3-222">Deze load balancing-algoritme maakt gebruik van alle beschikbare multipaths met de actieve controller taakverdeling, round-robin toewijst.</span><span class="sxs-lookup"><span data-stu-id="9fde3-222">This load-balancing algorithm uses all the available multipaths to the active controller in a balanced, round-robin fashion.</span></span>

1. <span data-ttu-id="9fde3-223">Bewerk de `/etc/multipath.conf` bestand.</span><span class="sxs-lookup"><span data-stu-id="9fde3-223">Edit the `/etc/multipath.conf` file.</span></span> <span data-ttu-id="9fde3-224">Type:</span><span class="sxs-lookup"><span data-stu-id="9fde3-224">Type:</span></span>
   
    `vi /etc/multipath.conf`
2. <span data-ttu-id="9fde3-225">Onder de `defaults` sectie, stelt u de `path_grouping_policy` naar `multibus`.</span><span class="sxs-lookup"><span data-stu-id="9fde3-225">Under the `defaults` section, set the `path_grouping_policy` to `multibus`.</span></span> <span data-ttu-id="9fde3-226">De `path_grouping_policy` Hiermee geeft u het standaardpad beleid toepassen op niet-gespecificeerde multipaths groeperen.</span><span class="sxs-lookup"><span data-stu-id="9fde3-226">The `path_grouping_policy` specifies the default path grouping policy to apply to unspecified multipaths.</span></span> <span data-ttu-id="9fde3-227">De sectie standaardwaarden wordt gezocht, zoals hieronder wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="9fde3-227">The defaults section will look as shown below.</span></span>
   
        defaults {
                user_friendly_names yes
                path_grouping_policy multibus
        }

> [!NOTE]
> <span data-ttu-id="9fde3-228">De meest voorkomende waarden van `path_grouping_policy` omvatten:</span><span class="sxs-lookup"><span data-stu-id="9fde3-228">The most common values of `path_grouping_policy` include:</span></span>
> 
> * <span data-ttu-id="9fde3-229">failover = 1 pad per groep prioriteit</span><span class="sxs-lookup"><span data-stu-id="9fde3-229">failover = 1 path per priority group</span></span>
> * <span data-ttu-id="9fde3-230">multibus = alle geldige paden in de groep 1 prioriteit</span><span class="sxs-lookup"><span data-stu-id="9fde3-230">multibus = all valid paths in 1 priority group</span></span>
> 
> 

### <a name="step-4-enable-multipathing"></a><span data-ttu-id="9fde3-231">Stap 4: Enable meerdere paden</span><span class="sxs-lookup"><span data-stu-id="9fde3-231">Step 4: Enable multipathing</span></span>
1. <span data-ttu-id="9fde3-232">Start opnieuw op de `multipathd` daemon.</span><span class="sxs-lookup"><span data-stu-id="9fde3-232">Restart the `multipathd` daemon.</span></span> <span data-ttu-id="9fde3-233">Type:</span><span class="sxs-lookup"><span data-stu-id="9fde3-233">Type:</span></span>
   
    `service multipathd restart`
2. <span data-ttu-id="9fde3-234">De uitvoer zijn zoals hieronder wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="9fde3-234">The output will be as shown below:</span></span>
   
        [root@centosSS ~]# service multipathd start
        Starting multipathd daemon:  [OK]

### <a name="step-5-verify-multipathing"></a><span data-ttu-id="9fde3-235">Stap 5: Controleren of gebruik van meerdere paden</span><span class="sxs-lookup"><span data-stu-id="9fde3-235">Step 5: Verify multipathing</span></span>
1. <span data-ttu-id="9fde3-236">Eerst voor zorgen dat dat iSCSI-verbinding tot stand is gebracht met de StorSimple-apparaat als volgt:</span><span class="sxs-lookup"><span data-stu-id="9fde3-236">First make sure that iSCSI connection is established with the StorSimple device as follows:</span></span>
   
   <span data-ttu-id="9fde3-237">a.</span><span class="sxs-lookup"><span data-stu-id="9fde3-237">a.</span></span> <span data-ttu-id="9fde3-238">Detecteren van uw StorSimple-apparaat.</span><span class="sxs-lookup"><span data-stu-id="9fde3-238">Discover your StorSimple device.</span></span> <span data-ttu-id="9fde3-239">Type:</span><span class="sxs-lookup"><span data-stu-id="9fde3-239">Type:</span></span>
      
    ```
    iscsiadm -m discovery -t sendtargets -p  <IP address of network interface on the device>:<iSCSI port on StorSimple device>
    ```
    
    <span data-ttu-id="9fde3-240">De uitvoer wanneer IP-adres voor DATA0 10.126.162.25 en poort 3260 wordt geopend op het StorSimple-apparaat voor uitgaande iSCSI-verkeer is zoals hieronder wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="9fde3-240">The output when IP address for DATA0 is 10.126.162.25 and port 3260 is opened on the StorSimple device for outbound iSCSI traffic is as shown below:</span></span>
    
    ```
    10.126.162.25:3260,1 iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target
    10.126.162.26:3260,1 iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target
    ```

    <span data-ttu-id="9fde3-241">Kopieer het IQN van uw StorSimple-apparaat `iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target`, uit de bovenstaande uitvoer.</span><span class="sxs-lookup"><span data-stu-id="9fde3-241">Copy the IQN of your StorSimple device, `iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target`, from the preceding output.</span></span>

   <span data-ttu-id="9fde3-242">b.</span><span class="sxs-lookup"><span data-stu-id="9fde3-242">b.</span></span> <span data-ttu-id="9fde3-243">Verbinding maken met het apparaat doel IQN gebruikt.</span><span class="sxs-lookup"><span data-stu-id="9fde3-243">Connect to the device using target IQN.</span></span> <span data-ttu-id="9fde3-244">Het StorSimple-apparaat is het iSCSI-doel.</span><span class="sxs-lookup"><span data-stu-id="9fde3-244">The StorSimple device is the iSCSI target here.</span></span> <span data-ttu-id="9fde3-245">Type:</span><span class="sxs-lookup"><span data-stu-id="9fde3-245">Type:</span></span>

    ```
    iscsiadm -m node --login -T <IQN of iSCSI target>
    ```

    <span data-ttu-id="9fde3-246">Het volgende voorbeeld ziet u uitvoer met een doel IQN van `iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target`.</span><span class="sxs-lookup"><span data-stu-id="9fde3-246">The following example shows output with a target IQN of `iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target`.</span></span> <span data-ttu-id="9fde3-247">De uitvoer geeft aan dat u hebt is verbonden met de twee netwerkinterfaces voor iSCSI-functionaliteit op uw apparaat.</span><span class="sxs-lookup"><span data-stu-id="9fde3-247">The output indicates that you have successfully connected to the two iSCSI-enabled network interfaces on your device.</span></span>

    ```
    Logging in to [iface: eth0, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.25,3260] (multiple)
    Logging in to [iface: eth1, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.25,3260] (multiple)
    Logging in to [iface: eth0, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.26,3260] (multiple)
    Logging in to [iface: eth1, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.26,3260] (multiple)
    Login to [iface: eth0, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.25,3260] successful.
    Login to [iface: eth1, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.25,3260] successful.
    Login to [iface: eth0, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.26,3260] successful.
    Login to [iface: eth1, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.26,3260] successful.
    ```

    <span data-ttu-id="9fde3-248">Als u slechts één host-interface en twee paden Hier ziet, moet u zowel de interfaces op de host voor iSCSI-inschakelen.</span><span class="sxs-lookup"><span data-stu-id="9fde3-248">If you see only one host interface and two paths here, then you need to enable both the interfaces on host for iSCSI.</span></span> <span data-ttu-id="9fde3-249">U kunt volgen de [gedetailleerde instructies in de documentatie van Linux](https://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/5/html/Online_Storage_Reconfiguration_Guide/iscsioffloadmain.html).</span><span class="sxs-lookup"><span data-stu-id="9fde3-249">You can follow the [detailed instructions in Linux documentation](https://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/5/html/Online_Storage_Reconfiguration_Guide/iscsioffloadmain.html).</span></span>

2. <span data-ttu-id="9fde3-250">Een volume wordt blootgesteld aan de server CentOS van het StorSimple-apparaat.</span><span class="sxs-lookup"><span data-stu-id="9fde3-250">A volume is exposed to the CentOS server from the StorSimple device.</span></span> <span data-ttu-id="9fde3-251">Zie voor meer informatie [stap 6: een volume maken](storsimple-deployment-walkthrough.md#step-6-create-a-volume) via de klassieke Azure portal op uw StorSimple-apparaat.</span><span class="sxs-lookup"><span data-stu-id="9fde3-251">For more information, see [Step 6: Create a volume](storsimple-deployment-walkthrough.md#step-6-create-a-volume) via the Azure classic portal on your StorSimple device.</span></span>

3. <span data-ttu-id="9fde3-252">Controleer of de beschikbare paden.</span><span class="sxs-lookup"><span data-stu-id="9fde3-252">Verify the available paths.</span></span> <span data-ttu-id="9fde3-253">Type:</span><span class="sxs-lookup"><span data-stu-id="9fde3-253">Type:</span></span>

      ```
      multipath –l
      ```

      <span data-ttu-id="9fde3-254">Het volgende voorbeeld ziet u de uitvoer voor twee netwerkinterfaces op een StorSimple-apparaat is verbonden met een netwerkinterface één host met twee beschikbare paden.</span><span class="sxs-lookup"><span data-stu-id="9fde3-254">The following example shows the output for two network interfaces on a StorSimple device connected to a single host network interface with two available paths.</span></span>

        ```
        mpathb (36486fd20cc081f8dcd3fccb992d45a68) dm-3 MSFT,STORSIMPLE 8100
        size=100G features='0' hwhandler='0' wp=rw
        `-+- policy='round-robin 0' prio=0 status=active
        |- 7:0:0:1 sdc 8:32 active undef running
        `- 6:0:0:1 sdd 8:48 active undef running
        ```

        The following example shows the output for two network interfaces on a StorSimple device connected to two host network interfaces with four available paths.

        ```
        mpathb (36486fd27a23feba1b096226f11420f6b) dm-2 MSFT,STORSIMPLE 8100
        size=100G features='0' hwhandler='0' wp=rw
        `-+- policy='round-robin 0' prio=0 status=active
        |- 17:0:0:0 sdb 8:16 active undef running
        |- 15:0:0:0 sdd 8:48 active undef running
        |- 14:0:0:0 sdc 8:32 active undef running
        `- 16:0:0:0 sde 8:64 active undef running
        ```

        After the paths are configured, refer to the specific instructions on your host operating system (Centos 6.6) to mount and format this volume.

## <a name="troubleshoot-multipathing"></a><span data-ttu-id="9fde3-255">Problemen met meerdere paden</span><span class="sxs-lookup"><span data-stu-id="9fde3-255">Troubleshoot multipathing</span></span>
<span data-ttu-id="9fde3-256">Deze sectie bevat enkele nuttige tips als u problemen ondervindt tijdens het gebruik van meerdere paden configureren uitvoert.</span><span class="sxs-lookup"><span data-stu-id="9fde3-256">This section provides some helpful tips if you run into any issues during multipathing configuration.</span></span>

<span data-ttu-id="9fde3-257">Q.</span><span class="sxs-lookup"><span data-stu-id="9fde3-257">Q.</span></span> <span data-ttu-id="9fde3-258">Zie ik niet de wijzigingen in `multipath.conf` bestand die van kracht.</span><span class="sxs-lookup"><span data-stu-id="9fde3-258">I do not see the changes in `multipath.conf` file taking effect.</span></span>

<span data-ttu-id="9fde3-259">A.</span><span class="sxs-lookup"><span data-stu-id="9fde3-259">A.</span></span> <span data-ttu-id="9fde3-260">Als u aangebrachte wijzigingen in de `multipath.conf` -bestand, moet u het gebruik van meerdere paden-service opnieuw starten.</span><span class="sxs-lookup"><span data-stu-id="9fde3-260">If you have made any changes to the `multipath.conf` file, you will need to restart the multipathing service.</span></span> <span data-ttu-id="9fde3-261">Typ de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="9fde3-261">Type the following command:</span></span>

    service multipathd restart

<span data-ttu-id="9fde3-262">Q.</span><span class="sxs-lookup"><span data-stu-id="9fde3-262">Q.</span></span> <span data-ttu-id="9fde3-263">Ik heb twee netwerkinterfaces op de StorSimple-apparaat en twee netwerkinterfaces op de host ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="9fde3-263">I have enabled two network interfaces on the StorSimple device and two network interfaces on the host.</span></span> <span data-ttu-id="9fde3-264">Wanneer ik de beschikbare paden, zie ik slechts twee paden.</span><span class="sxs-lookup"><span data-stu-id="9fde3-264">When I list the available paths, I see only two paths.</span></span> <span data-ttu-id="9fde3-265">Ik verwachtte vier beschikbare paden.</span><span class="sxs-lookup"><span data-stu-id="9fde3-265">I expected to see four available paths.</span></span>

<span data-ttu-id="9fde3-266">A.</span><span class="sxs-lookup"><span data-stu-id="9fde3-266">A.</span></span> <span data-ttu-id="9fde3-267">Zorg ervoor dat de twee paden zich op hetzelfde subnet en routeerbaar.</span><span class="sxs-lookup"><span data-stu-id="9fde3-267">Make sure that the two paths are on the same subnet and routable.</span></span> <span data-ttu-id="9fde3-268">Als de netwerkinterfaces zich op verschillende VLAN's en niet routeerbaar te maken, u slechts twee paden ziet.</span><span class="sxs-lookup"><span data-stu-id="9fde3-268">If the network interfaces are on different vLANs and not routable, you will see only two paths.</span></span> <span data-ttu-id="9fde3-269">Er is een manier om dit te controleren om ervoor te zorgen dat u zowel de hostinterfaces van de netwerkinterface op het StorSimple-apparaat kunt bereiken.</span><span class="sxs-lookup"><span data-stu-id="9fde3-269">One way to verify this is to make sure that you can reach both the host interfaces from a network interface on the StorSimple device.</span></span> <span data-ttu-id="9fde3-270">U moet [contact op met Microsoft Support](storsimple-contact-microsoft-support.md) zoals deze verificatie kan alleen worden uitgevoerd via een ondersteuningssessie voor.</span><span class="sxs-lookup"><span data-stu-id="9fde3-270">You will need to [contact Microsoft Support](storsimple-contact-microsoft-support.md) as this verification can only be done via a support session.</span></span>

<span data-ttu-id="9fde3-271">Q.</span><span class="sxs-lookup"><span data-stu-id="9fde3-271">Q.</span></span> <span data-ttu-id="9fde3-272">Wanneer ik de lijst beschikbare paden, zie ik niet geen uitvoer.</span><span class="sxs-lookup"><span data-stu-id="9fde3-272">When I list available paths, I do not see any output.</span></span>

<span data-ttu-id="9fde3-273">A.</span><span class="sxs-lookup"><span data-stu-id="9fde3-273">A.</span></span> <span data-ttu-id="9fde3-274">Normaal gesproken niet ziet multipathed paden stelt een probleem met het gebruik van meerdere paden daemon en het is zeer waarschijnlijk dat er probleem hier ligt in de `multipath.conf` bestand.</span><span class="sxs-lookup"><span data-stu-id="9fde3-274">Typically, not seeing any multipathed paths suggests a problem with the multipathing daemon, and it’s most likely that any problem here lies in the `multipath.conf` file.</span></span>

<span data-ttu-id="9fde3-275">Het is ook waard controleren dat u daadwerkelijk een aantal schijven zien kunt nadat u het doel als er geen reactie van de lijsten van multipath kan ook betekenen er geen schijven.</span><span class="sxs-lookup"><span data-stu-id="9fde3-275">It would also be worth checking that you can actually see some disks after connecting to the target, as no response from the multipath listings could also mean you don’t have any disks.</span></span>

* <span data-ttu-id="9fde3-276">Gebruik de volgende opdracht om te scannen van de SCSI-bus:</span><span class="sxs-lookup"><span data-stu-id="9fde3-276">Use the following command to rescan the SCSI bus:</span></span>
  
    <span data-ttu-id="9fde3-277">`$ rescan-scsi-bus.sh `(onderdeel van het pakket sg3_utils)</span><span class="sxs-lookup"><span data-stu-id="9fde3-277">`$ rescan-scsi-bus.sh `(part of sg3_utils package)</span></span>
* <span data-ttu-id="9fde3-278">Typ de volgende opdrachten:</span><span class="sxs-lookup"><span data-stu-id="9fde3-278">Type the following commands:</span></span>
  
    `$ dmesg | grep sd*`
     
     <span data-ttu-id="9fde3-279">of</span><span class="sxs-lookup"><span data-stu-id="9fde3-279">Or</span></span>
  
    `$ fdisk –l`
  
    <span data-ttu-id="9fde3-280">Deze wordt details van onlangs toegevoegde schijven geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="9fde3-280">These will return details of recently added disks.</span></span>
* <span data-ttu-id="9fde3-281">Om te bepalen of het een StorSimple-schijf is, gebruik de volgende opdrachten:</span><span class="sxs-lookup"><span data-stu-id="9fde3-281">To determine whether it is a StorSimple disk, use the following commands:</span></span>
  
    `cat /sys/block/<DISK>/device/model`
  
    <span data-ttu-id="9fde3-282">Hiermee wordt een tekenreeks, die bepaalt of het een StorSimple-schijf is geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="9fde3-282">This will return a string, which will determine if it’s a StorSimple disk.</span></span>

<span data-ttu-id="9fde3-283">Een minder waarschijnlijk maar mogelijke oorzaak kan ook worden de verlopen iscsid pid.</span><span class="sxs-lookup"><span data-stu-id="9fde3-283">A less likely but possible cause could also be stale iscsid pid.</span></span> <span data-ttu-id="9fde3-284">Gebruik de volgende opdracht af te melden bij de iSCSI-sessies:</span><span class="sxs-lookup"><span data-stu-id="9fde3-284">Use the following command to log off from the iSCSI sessions:</span></span>

    iscsiadm -m node --logout -p <Target_IP>

<span data-ttu-id="9fde3-285">Herhaal deze opdracht voor de verbonden netwerkinterfaces op de iSCSI-doel, uw StorSimple-apparaat is.</span><span class="sxs-lookup"><span data-stu-id="9fde3-285">Repeat this command for all the connected network interfaces on the iSCSI target, which is your StorSimple device.</span></span> <span data-ttu-id="9fde3-286">Nadat u afgemeld bij alle iSCSI-sessies bent, gebruikt u de iSCSI-doel IQN te hervatten van de iSCSI-sessie.</span><span class="sxs-lookup"><span data-stu-id="9fde3-286">Once you have logged off from all the iSCSI sessions, use the iSCSI target IQN to reestablish the iSCSI session.</span></span> <span data-ttu-id="9fde3-287">Typ de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="9fde3-287">Type the following command:</span></span>

    iscsiadm -m node --login -T <TARGET_IQN>


<span data-ttu-id="9fde3-288">Q.</span><span class="sxs-lookup"><span data-stu-id="9fde3-288">Q.</span></span> <span data-ttu-id="9fde3-289">Ik wil niet zeker weet of het apparaat wilt plaatsen is.</span><span class="sxs-lookup"><span data-stu-id="9fde3-289">I am not sure if my device is whitelisted.</span></span>

<span data-ttu-id="9fde3-290">A.</span><span class="sxs-lookup"><span data-stu-id="9fde3-290">A.</span></span> <span data-ttu-id="9fde3-291">Gebruik de volgende opdracht voor probleemoplossing interactief om te controleren of uw apparaat wilt plaatsen:</span><span class="sxs-lookup"><span data-stu-id="9fde3-291">To verify whether your device is whitelisted, use the following troubleshooting interactive command:</span></span>

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


<span data-ttu-id="9fde3-292">Ga voor meer informatie naar [probleemoplossing interactief opdracht voor het gebruik van meerdere paden gebruiken](http://www.centos.org/docs/5/html/5.1/DM_Multipath/multipath_config_confirm.html).</span><span class="sxs-lookup"><span data-stu-id="9fde3-292">For more information, go to [use troubleshooting interactive command for multipathing](http://www.centos.org/docs/5/html/5.1/DM_Multipath/multipath_config_confirm.html).</span></span>

## <a name="list-of-useful-commands"></a><span data-ttu-id="9fde3-293">Lijst met opdrachten nuttig</span><span class="sxs-lookup"><span data-stu-id="9fde3-293">List of useful commands</span></span>
| <span data-ttu-id="9fde3-294">Type</span><span class="sxs-lookup"><span data-stu-id="9fde3-294">Type</span></span> | <span data-ttu-id="9fde3-295">Opdracht</span><span class="sxs-lookup"><span data-stu-id="9fde3-295">Command</span></span> | <span data-ttu-id="9fde3-296">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="9fde3-296">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="9fde3-297">**iSCSI**</span><span class="sxs-lookup"><span data-stu-id="9fde3-297">**iSCSI**</span></span> |`service iscsid start` |<span data-ttu-id="9fde3-298">ISCSI-service starten</span><span class="sxs-lookup"><span data-stu-id="9fde3-298">Start iSCSI service</span></span> |
| &nbsp; |`service iscsid stop` |<span data-ttu-id="9fde3-299">ISCSI-service stoppen</span><span class="sxs-lookup"><span data-stu-id="9fde3-299">Stop iSCSI service</span></span> |
| &nbsp; |`service iscsid restart` |<span data-ttu-id="9fde3-300">ISCSI-service opnieuw starten</span><span class="sxs-lookup"><span data-stu-id="9fde3-300">Restart iSCSI service</span></span> |
| &nbsp; |`iscsiadm -m discovery -t sendtargets -p <TARGET_IP>` |<span data-ttu-id="9fde3-301">Beschikbare doelen op het opgegeven adres detecteren</span><span class="sxs-lookup"><span data-stu-id="9fde3-301">Discover available targets on the specified address</span></span> |
| &nbsp; |`iscsiadm -m node --login -T <TARGET_IQN>` |<span data-ttu-id="9fde3-302">Aanmelden bij de iSCSI-doel</span><span class="sxs-lookup"><span data-stu-id="9fde3-302">Log in to the iSCSI target</span></span> |
| &nbsp; |`iscsiadm -m node --logout -p <Target_IP>` |<span data-ttu-id="9fde3-303">Meld u af van de iSCSI-doel</span><span class="sxs-lookup"><span data-stu-id="9fde3-303">Log out from the iSCSI target</span></span> |
| &nbsp; |`cat /etc/iscsi/initiatorname.iscsi` |<span data-ttu-id="9fde3-304">Naam van de iSCSI-initiator afdrukken</span><span class="sxs-lookup"><span data-stu-id="9fde3-304">Print iSCSI initiator name</span></span> |
| &nbsp; |`iscsiadm –m session –s <sessionid> -P 3` |<span data-ttu-id="9fde3-305">Controleer de status van de iSCSI-sessie en het volume dat is gedetecteerd op de host</span><span class="sxs-lookup"><span data-stu-id="9fde3-305">Check the state of the iSCSI session and volume discovered on the host</span></span> |
| &nbsp; |`iscsi –m session` |<span data-ttu-id="9fde3-306">Bevat alle iSCSI-sessies tot stand gebracht tussen de host en het StorSimple-apparaat</span><span class="sxs-lookup"><span data-stu-id="9fde3-306">Shows all the iSCSI sessions established between the host and the StorSimple device</span></span> |
|  | | |
| <span data-ttu-id="9fde3-307">**Gebruik van meerdere paden**</span><span class="sxs-lookup"><span data-stu-id="9fde3-307">**Multipathing**</span></span> |`service multipathd start` |<span data-ttu-id="9fde3-308">Multipath-daemon starten</span><span class="sxs-lookup"><span data-stu-id="9fde3-308">Start multipath daemon</span></span> |
| &nbsp; |`service multipathd stop` |<span data-ttu-id="9fde3-309">Multipath-daemon stoppen</span><span class="sxs-lookup"><span data-stu-id="9fde3-309">Stop multipath daemon</span></span> |
| &nbsp; |`service multipathd restart` |<span data-ttu-id="9fde3-310">Multipath-daemon starten</span><span class="sxs-lookup"><span data-stu-id="9fde3-310">Restart multipath daemon</span></span> |
| &nbsp; |`chkconfig multipathd on` </br> <span data-ttu-id="9fde3-311">OF</span><span class="sxs-lookup"><span data-stu-id="9fde3-311">OR</span></span> </br> `mpathconf –with_chkconfig y` |<span data-ttu-id="9fde3-312">Schakel multipath-daemon te starten tijdens het opstarten</span><span class="sxs-lookup"><span data-stu-id="9fde3-312">Enable multipath daemon to start at boot time</span></span> |
| &nbsp; |`multipathd –k` |<span data-ttu-id="9fde3-313">Start de interactieve console voor probleemoplossing</span><span class="sxs-lookup"><span data-stu-id="9fde3-313">Start the interactive console for troubleshooting</span></span> |
| &nbsp; |`multipath –l` |<span data-ttu-id="9fde3-314">Lijst met meerdere paden verbindingen en apparaten</span><span class="sxs-lookup"><span data-stu-id="9fde3-314">List multipath connections and devices</span></span> |
| &nbsp; |`mpathconf --enable` |<span data-ttu-id="9fde3-315">Maken van een voorbeeldbestand mulitpath.conf in`/etc/mulitpath.conf`</span><span class="sxs-lookup"><span data-stu-id="9fde3-315">Create a sample mulitpath.conf file in `/etc/mulitpath.conf`</span></span> |
|  | | |

## <a name="next-steps"></a><span data-ttu-id="9fde3-316">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="9fde3-316">Next steps</span></span>
<span data-ttu-id="9fde3-317">Als u de MPIO op Linux-host configureert, moet u mogelijk ook om te verwijzen naar de volgende documenten voor CentoS 6.6:</span><span class="sxs-lookup"><span data-stu-id="9fde3-317">As you are configuring MPIO on Linux host, you may also need to refer to the following CentoS 6.6 documents:</span></span>

* [<span data-ttu-id="9fde3-318">Instellen van MPIO op CentOS</span><span class="sxs-lookup"><span data-stu-id="9fde3-318">Setting up MPIO on CentOS</span></span>](http://www.centos.org/docs/5/html/5.1/DM_Multipath/setup_procedure.html)
* [<span data-ttu-id="9fde3-319">Linux Training handleiding</span><span class="sxs-lookup"><span data-stu-id="9fde3-319">Linux Training Guide</span></span>](http://linux-training.be/files/books/LinuxAdm.pdf)


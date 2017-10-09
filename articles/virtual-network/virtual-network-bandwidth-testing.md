---
title: aaaTesting Azure VM netwerkdoorvoer | Microsoft Docs
description: Meer informatie over hoe tootest virtuele machine van Azure-netwerk doorvoer.
services: virtual-network
documentationcenter: na
author: steveesp
manager: Gerald DeGrace
editor: 
ms.assetid: 
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/21/2017
ms.author: steveesp
ms.openlocfilehash: 2da85c27bc8d16a443b215891f4cd0460f41926f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="bandwidththroughput-testing-ntttcp"></a><span data-ttu-id="55be0-103">Bandbreedte/doorvoer (NTTTCP) testen</span><span class="sxs-lookup"><span data-stu-id="55be0-103">Bandwidth/Throughput testing (NTTTCP)</span></span>

<span data-ttu-id="55be0-104">Bij het testen van prestaties van de netwerkdoorvoer in Azure, is het beste toouse een hulpprogramma dat gericht is op Hallo netwerk voor het testen en minimaliseert Hallo gebruik van andere bronnen die kan invloed hebben op prestaties.</span><span class="sxs-lookup"><span data-stu-id="55be0-104">When testing network throughput performance in Azure, it's best toouse a tool that targets hello network for testing and minimizes hello use of other resources that could impact performance.</span></span> <span data-ttu-id="55be0-105">NTTTCP wordt aanbevolen.</span><span class="sxs-lookup"><span data-stu-id="55be0-105">NTTTCP is recommended.</span></span>

<span data-ttu-id="55be0-106">Hallo hulpprogramma tootwo Azure Virtual machines Hallo kopiëren dezelfde grootte hebben.</span><span class="sxs-lookup"><span data-stu-id="55be0-106">Copy hello tool tootwo Azure VMs of hello same size.</span></span> <span data-ttu-id="55be0-107">Één virtuele machine fungeert als de afzender en Hallo andere als ontvanger.</span><span class="sxs-lookup"><span data-stu-id="55be0-107">One VM functions as SENDER and hello other as RECEIVER.</span></span>

#### <a name="deploying-vms-for-testing"></a><span data-ttu-id="55be0-108">Implementeren van virtuele machines voor testdoeleinden</span><span class="sxs-lookup"><span data-stu-id="55be0-108">Deploying VMs for testing</span></span>
<span data-ttu-id="55be0-109">Voor Hallo doeleinden van deze test, is Hallo twee virtuele machines moeten zich in dezelfde Cloudservice Hallo of Hallo dezelfde Beschikbaarheidsset zodat we kunnen hun intern IP-adressen gebruiken en Hallo Load Balancers van Hallo test uitsluiten.</span><span class="sxs-lookup"><span data-stu-id="55be0-109">For hello purposes of this test, hello two VMs should be in either hello same Cloud Service or hello same Availability Set so that we can use their internal IPs and exclude hello Load Balancers from hello test.</span></span> <span data-ttu-id="55be0-110">Het is mogelijk tootest Hello VIP maar dit soort testen valt buiten bereik Hallo van dit document.</span><span class="sxs-lookup"><span data-stu-id="55be0-110">It is possible tootest with hello VIP but this kind of testing is outside hello scope of this document.</span></span>
 
<span data-ttu-id="55be0-111">Noteer Hallo-ontvanger IP-adres.</span><span class="sxs-lookup"><span data-stu-id="55be0-111">Make a note of hello RECEIVER's IP address.</span></span> <span data-ttu-id="55be0-112">We bellen die IP 'a.b.c.r'</span><span class="sxs-lookup"><span data-stu-id="55be0-112">Let's call that IP "a.b.c.r"</span></span>

<span data-ttu-id="55be0-113">Noteer het aantal kernen Hallo op Hallo VM.</span><span class="sxs-lookup"><span data-stu-id="55be0-113">Make a note of hello number of cores on hello VM.</span></span> <span data-ttu-id="55be0-114">Laten we dit noemen '\#num\_kernen '</span><span class="sxs-lookup"><span data-stu-id="55be0-114">Let's call this "\#num\_cores"</span></span>
 
<span data-ttu-id="55be0-115">Voer Hallo NTTTCP testen voor 300 seconden (of 5 minuten) op Hallo afzender VM en ontvanger VM.</span><span class="sxs-lookup"><span data-stu-id="55be0-115">Run hello NTTTCP test for 300 seconds (or 5 minutes) on hello sender VM and receiver VM.</span></span>

<span data-ttu-id="55be0-116">Tip: Bij het instellen van deze test voor Hallo eerst, u mogelijk probeer een kortere periode tooget feedback voor test sneller.</span><span class="sxs-lookup"><span data-stu-id="55be0-116">Tip: When setting up this test for hello first time, you might try a shorter test period tooget feedback sooner.</span></span> <span data-ttu-id="55be0-117">Nadat het hulpprogramma voor Hallo werkt zoals verwacht, uitbreiden Hallo test periode too300 seconden voor de meest nauwkeurige resultaten Hallo.</span><span class="sxs-lookup"><span data-stu-id="55be0-117">Once hello tool is working as expected, extend hello test period too300 seconds for hello most accurate results.</span></span>

> [!NOTE]
> <span data-ttu-id="55be0-118">Hallo afzender **en** ontvanger moet opgeven **Hallo dezelfde** testen duur van de parameter (-t).</span><span class="sxs-lookup"><span data-stu-id="55be0-118">hello sender **and** receiver must specify **hello same** test duration parameter (-t).</span></span>

<span data-ttu-id="55be0-119">tootest één stream TCP 10 seconden:</span><span class="sxs-lookup"><span data-stu-id="55be0-119">tootest a single TCP stream for 10 seconds:</span></span>

<span data-ttu-id="55be0-120">Ontvanger parameters: ntttcp - r -t 10 - P 1</span><span class="sxs-lookup"><span data-stu-id="55be0-120">Receiver parameters: ntttcp -r -t 10 -P 1</span></span>

<span data-ttu-id="55be0-121">Parameters van de afzender: ntttcp-s10.27.33.7 -t 10 - n 1 -P 1</span><span class="sxs-lookup"><span data-stu-id="55be0-121">Sender parameters: ntttcp -s10.27.33.7 -t 10 -n 1 -P 1</span></span>

> [!NOTE]
> <span data-ttu-id="55be0-122">Hallo voorgaande voorbeeld mogen alleen worden gebruikt tooconfirm uw configuratie.</span><span class="sxs-lookup"><span data-stu-id="55be0-122">hello preceding sample should only be used tooconfirm your configuration.</span></span> <span data-ttu-id="55be0-123">Aantal voorbeelden van testen worden verderop in dit document besproken.</span><span class="sxs-lookup"><span data-stu-id="55be0-123">Valid examples of testing are covered later in this document.</span></span>

## <a name="testing-vms-running-windows"></a><span data-ttu-id="55be0-124">Testen van virtuele machines waarop WINDOWS wordt uitgevoerd:</span><span class="sxs-lookup"><span data-stu-id="55be0-124">Testing VMs running WINDOWS:</span></span>

#### <a name="get-ntttcp-onto-hello-vms"></a><span data-ttu-id="55be0-125">NTTTCP terechtkomen Hallo virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="55be0-125">Get NTTTCP onto hello VMs.</span></span>

<span data-ttu-id="55be0-126">Download de nieuwste versie Hallo: <https://gallery.technet.microsoft.com/NTttcp-Version-528-Now-f8b12769></span><span class="sxs-lookup"><span data-stu-id="55be0-126">Download hello latest version: <https://gallery.technet.microsoft.com/NTttcp-Version-528-Now-f8b12769></span></span>

<span data-ttu-id="55be0-127">Of zoekt u het als verplaatst: <https://www.bing.com/search?q=ntttcp+download> \< --moet eerst worden bereikt</span><span class="sxs-lookup"><span data-stu-id="55be0-127">Or search for it if moved: <https://www.bing.com/search?q=ntttcp+download>\< -- should be first hit</span></span>

<span data-ttu-id="55be0-128">Overweeg NTTTCP plaatsen in een afzonderlijke map, zoals c:\\hulpprogramma's</span><span class="sxs-lookup"><span data-stu-id="55be0-128">Consider putting NTTTCP in separate folder, like c:\\tools</span></span>

#### <a name="allow-ntttcp-through-hello-windows-firewall"></a><span data-ttu-id="55be0-129">NTTTCP toestaan via Hallo Windows firewall</span><span class="sxs-lookup"><span data-stu-id="55be0-129">Allow NTTTCP through hello Windows firewall</span></span>
<span data-ttu-id="55be0-130">Maak een regel voor toestaan op Hallo Windows Firewall tooallow de NTTTCP verkeer tooarrive op Hallo ontvanger.</span><span class="sxs-lookup"><span data-stu-id="55be0-130">On hello RECEIVER, create an Allow rule on hello Windows Firewall tooallow the NTTTCP traffic tooarrive.</span></span> <span data-ttu-id="55be0-131">Het is eenvoudigste tooallow Hallo volledige NTTTCP programma met de naam in plaats van inkomende tooallow bepaalde TCP-poorten.</span><span class="sxs-lookup"><span data-stu-id="55be0-131">It's easiest tooallow hello entire NTTTCP program by name rather than tooallow specific TCP ports inbound.</span></span>

<span data-ttu-id="55be0-132">Toestaan dat ntttcp via Windows Firewall Hallo als volgt:</span><span class="sxs-lookup"><span data-stu-id="55be0-132">Allow ntttcp through hello Windows Firewall like this:</span></span>

<span data-ttu-id="55be0-133">Netsh advfirewall firewall regel programma toevoegen =\<pad\>\\ntttcp.exe name = "ntttcp" protocol eventuele dir = in actie = = toestaan inschakelen = yes profile = ANY</span><span class="sxs-lookup"><span data-stu-id="55be0-133">netsh advfirewall firewall add rule program=\<PATH\>\\ntttcp.exe name="ntttcp" protocol=any dir=in action=allow enable=yes profile=ANY</span></span>

<span data-ttu-id="55be0-134">Bijvoorbeeld, als u ntttcp.exe toohello gekopieerd ' c:\\extra ' map, zou dit Hallo-opdracht:</span><span class="sxs-lookup"><span data-stu-id="55be0-134">For example, if you copied ntttcp.exe toohello "c:\\tools" folder, this would be hello command:</span></span> 

<span data-ttu-id="55be0-135">Netsh advfirewall firewall regel programma toevoegen = c:\\hulpprogramma's\\ntttcp.exe naam = 'ntttcp' protocol eventuele dir = in actie = = toestaan inschakelen = yes profile = ANY</span><span class="sxs-lookup"><span data-stu-id="55be0-135">netsh advfirewall firewall add rule program=c:\\tools\\ntttcp.exe name="ntttcp" protocol=any dir=in action=allow enable=yes profile=ANY</span></span>

#### <a name="running-ntttcp-tests"></a><span data-ttu-id="55be0-136">NTTTCP tests die worden uitgevoerd</span><span class="sxs-lookup"><span data-stu-id="55be0-136">Running NTTTCP tests</span></span>

<span data-ttu-id="55be0-137">Start NTTTCP op Hallo ontvanger (**uitvoeren vanaf CMD**, niet vanuit PowerShell):</span><span class="sxs-lookup"><span data-stu-id="55be0-137">Start NTTTCP on hello RECEIVER (**run from CMD**, not from PowerShell):</span></span>

<span data-ttu-id="55be0-138">ntttcp - r-m [2\*\#num\_kernen],\*, 300 a.b.c.r -t</span><span class="sxs-lookup"><span data-stu-id="55be0-138">ntttcp -r –m [2\*\#num\_cores],\*,a.b.c.r -t 300</span></span>

<span data-ttu-id="55be0-139">Als Hallo VM vier kernen en het IP-adres 10.0.0.4 heeft, wordt deze eruit als volgt:</span><span class="sxs-lookup"><span data-stu-id="55be0-139">If hello VM has four cores and an IP address of 10.0.0.4, it would look like this:</span></span>

<span data-ttu-id="55be0-140">ntttcp - r – m 8,\*, 10.0.0.4 -t 300</span><span class="sxs-lookup"><span data-stu-id="55be0-140">ntttcp -r –m 8,\*,10.0.0.4 -t 300</span></span>


<span data-ttu-id="55be0-141">Start NTTTCP op Hallo afzender (**uitvoeren vanaf CMD**, niet vanuit PowerShell):</span><span class="sxs-lookup"><span data-stu-id="55be0-141">Start NTTTCP on hello SENDER (**run from CMD**, not from PowerShell):</span></span>

<span data-ttu-id="55be0-142">ntttcp -s-m 8,\*, 10.0.0.4 -t 300</span><span class="sxs-lookup"><span data-stu-id="55be0-142">ntttcp -s –m 8,\*,10.0.0.4 -t 300</span></span> 

<span data-ttu-id="55be0-143">Wachten op Hallo resultaten.</span><span class="sxs-lookup"><span data-stu-id="55be0-143">Wait for hello results.</span></span>


## <a name="testing-vms-running-linux"></a><span data-ttu-id="55be0-144">Testen van virtuele machines waarop LINUX wordt uitgevoerd:</span><span class="sxs-lookup"><span data-stu-id="55be0-144">Testing VMs running LINUX:</span></span>

<span data-ttu-id="55be0-145">Gebruik nttcp voor linux.</span><span class="sxs-lookup"><span data-stu-id="55be0-145">Use nttcp-for-linux.</span></span> <span data-ttu-id="55be0-146">Deze beschikbaar is via <https://github.com/Microsoft/ntttcp-for-linux></span><span class="sxs-lookup"><span data-stu-id="55be0-146">It is available from <https://github.com/Microsoft/ntttcp-for-linux></span></span>

<span data-ttu-id="55be0-147">Op Hallo virtuele Linux-machines (ZENDER en ontvanger), moet u deze opdrachten om voor te bereiden ntttcp voor linux op uw virtuele machines uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="55be0-147">On hello Linux VMs (both SENDER and RECEIVER), run these commands to prepare ntttcp-for-linux on your VMs:</span></span>

<span data-ttu-id="55be0-148">CentOS - Git installeren:</span><span class="sxs-lookup"><span data-stu-id="55be0-148">CentOS - Install Git:</span></span>
``` bash
  yum install gcc -y  
  yum install git -y
```
<span data-ttu-id="55be0-149">Ubuntu - Git installeren:</span><span class="sxs-lookup"><span data-stu-id="55be0-149">Ubuntu - Install Git:</span></span>
``` bash
 apt-get -y install build-essential  
 apt-get -y install git
```
<span data-ttu-id="55be0-150">Maken en te installeren op beide:</span><span class="sxs-lookup"><span data-stu-id="55be0-150">Make and Install on both:</span></span>
``` bash
 git clone <https://github.com/Microsoft/ntttcp-for-linux>
 cd ntttcp-for-linux/src
 make && make install
```

<span data-ttu-id="55be0-151">Als in voorbeeld van de Windows hello Aannemende dat Hallo Linux ontvanger IP-adres is 10.0.0.4</span><span class="sxs-lookup"><span data-stu-id="55be0-151">As in hello Windows example, we assume hello Linux RECEIVER's IP is 10.0.0.4</span></span>

<span data-ttu-id="55be0-152">Start NTTTCP voor Linux op Hallo ontvanger:</span><span class="sxs-lookup"><span data-stu-id="55be0-152">Start NTTTCP-for-Linux on hello RECEIVER:</span></span>

``` bash
ntttcp -r -t 300
```

<span data-ttu-id="55be0-153">En op Hallo afzender, uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="55be0-153">And on hello SENDER, run:</span></span>

``` bash
ntttcp -s10.0.0.4 -t 300
```
 
<span data-ttu-id="55be0-154">Test lengte standaardwaarden too60 seconden als er is geen tijdsparameter is gegeven</span><span class="sxs-lookup"><span data-stu-id="55be0-154">Test length defaults too60 seconds if no time parameter is given</span></span>

## <a name="testing-between-vms-running-windows-and-linux"></a><span data-ttu-id="55be0-155">Testen tussen VM's met Windows en LINUX:</span><span class="sxs-lookup"><span data-stu-id="55be0-155">Testing between VMs running Windows and LINUX:</span></span>

<span data-ttu-id="55be0-156">Op deze scenario's moeten we Hallo Nee-sync-modus inschakelen zodat Hallo test kunt uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="55be0-156">On this scenarios we should enable hello no-sync mode so hello test can run.</span></span> <span data-ttu-id="55be0-157">Dit wordt gedaan met behulp van Hallo **-N vlag** voor Linux en **-ns vlag** voor Windows.</span><span class="sxs-lookup"><span data-stu-id="55be0-157">This is done by using hello **-N flag** for Linux, and **-ns flag** for Windows.</span></span>

#### <a name="from-linux-toowindows"></a><span data-ttu-id="55be0-158">Van Linux tooWindows:</span><span class="sxs-lookup"><span data-stu-id="55be0-158">From Linux tooWindows:</span></span>

<span data-ttu-id="55be0-159">Ontvanger <Windows>:</span><span class="sxs-lookup"><span data-stu-id="55be0-159">Receiver <Windows>:</span></span>

``` bash
ntttcp -r -m <2 x nr cores>,*,<Windows server IP>
```

<span data-ttu-id="55be0-160">Afzender <Linux> :</span><span class="sxs-lookup"><span data-stu-id="55be0-160">Sender <Linux> :</span></span>

``` bash
ntttcp -s -m <2 x nr cores>,*,<Windows server IP> -N -t 300
```

#### <a name="from-windows-toolinux"></a><span data-ttu-id="55be0-161">Vanaf Windows tooLinux:</span><span class="sxs-lookup"><span data-stu-id="55be0-161">From Windows tooLinux:</span></span>

<span data-ttu-id="55be0-162">Ontvanger <Linux>:</span><span class="sxs-lookup"><span data-stu-id="55be0-162">Receiver <Linux>:</span></span>

``` bash
ntttcp -r -m <2 x nr cores>,*,<Linux server IP>
```

<span data-ttu-id="55be0-163">Afzender <Windows>:</span><span class="sxs-lookup"><span data-stu-id="55be0-163">Sender <Windows>:</span></span>

``` bash
ntttcp -s -m <2 x nr cores>,*,<Linux  server IP> -ns -t 300
```

## <a name="next-steps"></a><span data-ttu-id="55be0-164">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="55be0-164">Next steps</span></span>
* <span data-ttu-id="55be0-165">Afhankelijk van de resultaten, kunnen er ruimte te[netwerk doorvoer machines optimaliseren](virtual-network-optimize-network-bandwidth.md) voor uw scenario.</span><span class="sxs-lookup"><span data-stu-id="55be0-165">Depending on results, there may be room too[Optimize network throughput machines](virtual-network-optimize-network-bandwidth.md) for your scenario.</span></span>
* <span data-ttu-id="55be0-166">Klik hier als u meer wilt weten met [Azure Virtual Network Veelgestelde vragen (FAQ)](virtual-networks-faq.md)</span><span class="sxs-lookup"><span data-stu-id="55be0-166">Learn more wtih [Azure Virtual Network frequently asked questions (FAQ)](virtual-networks-faq.md)</span></span>

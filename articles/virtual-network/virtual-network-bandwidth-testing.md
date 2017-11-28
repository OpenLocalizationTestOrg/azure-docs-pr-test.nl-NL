---
title: Test virtuele machine van Azure netwerkdoorvoer | Microsoft Docs
description: Informatie over het testen van de netwerkdoorvoer van de virtuele machine van Azure.
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
ms.openlocfilehash: ccebc722386a19014674d7a59757a3685bd50793
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="bandwidththroughput-testing-ntttcp"></a><span data-ttu-id="18b2a-103">Bandbreedte/doorvoer (NTTTCP) testen</span><span class="sxs-lookup"><span data-stu-id="18b2a-103">Bandwidth/Throughput testing (NTTTCP)</span></span>

<span data-ttu-id="18b2a-104">Bij het testen van prestaties van de netwerkdoorvoer in Azure, is het raadzaam te gebruiken van een hulpprogramma dat gericht is op het netwerk voor het testen en het gebruik van andere bronnen die kan invloed hebben op prestaties geminimaliseerd.</span><span class="sxs-lookup"><span data-stu-id="18b2a-104">When testing network throughput performance in Azure, it's best to use a tool that targets the network for testing and minimizes the use of other resources that could impact performance.</span></span> <span data-ttu-id="18b2a-105">NTTTCP wordt aanbevolen.</span><span class="sxs-lookup"><span data-stu-id="18b2a-105">NTTTCP is recommended.</span></span>

<span data-ttu-id="18b2a-106">Kopieer het hulpprogramma naar twee Azure VM's van dezelfde grootte hebben.</span><span class="sxs-lookup"><span data-stu-id="18b2a-106">Copy the tool to two Azure VMs of the same size.</span></span> <span data-ttu-id="18b2a-107">Een virtuele machine fungeert als de afzender en de andere als ontvanger.</span><span class="sxs-lookup"><span data-stu-id="18b2a-107">One VM functions as SENDER and the other as RECEIVER.</span></span>

#### <a name="deploying-vms-for-testing"></a><span data-ttu-id="18b2a-108">Implementeren van virtuele machines voor testdoeleinden</span><span class="sxs-lookup"><span data-stu-id="18b2a-108">Deploying VMs for testing</span></span>
<span data-ttu-id="18b2a-109">Voor de doeleinden van deze test moet de twee virtuele machines in dezelfde Cloud Service of in dezelfde Beschikbaarheidsset zodat we kunnen hun interne IP-adressen gebruiken en de Load Balancers van de test uitsluiten.</span><span class="sxs-lookup"><span data-stu-id="18b2a-109">For the purposes of this test, the two VMs should be in either the same Cloud Service or the same Availability Set so that we can use their internal IPs and exclude the Load Balancers from the test.</span></span> <span data-ttu-id="18b2a-110">Het is mogelijk om te testen met het VIP, maar dit soort testen is buiten het bereik van dit document.</span><span class="sxs-lookup"><span data-stu-id="18b2a-110">It is possible to test with the VIP but this kind of testing is outside the scope of this document.</span></span>
 
<span data-ttu-id="18b2a-111">Maak een notitie van IP-adres van de ontvanger.</span><span class="sxs-lookup"><span data-stu-id="18b2a-111">Make a note of the RECEIVER's IP address.</span></span> <span data-ttu-id="18b2a-112">We bellen die IP 'a.b.c.r'</span><span class="sxs-lookup"><span data-stu-id="18b2a-112">Let's call that IP "a.b.c.r"</span></span>

<span data-ttu-id="18b2a-113">Noteer het aantal kernen op de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="18b2a-113">Make a note of the number of cores on the VM.</span></span> <span data-ttu-id="18b2a-114">Laten we dit noemen '\#num\_kernen '</span><span class="sxs-lookup"><span data-stu-id="18b2a-114">Let's call this "\#num\_cores"</span></span>
 
<span data-ttu-id="18b2a-115">Voert de test NTTTCP voor 300 seconden (of 5 minuten) op de VM-verzender en ontvanger VM.</span><span class="sxs-lookup"><span data-stu-id="18b2a-115">Run the NTTTCP test for 300 seconds (or 5 minutes) on the sender VM and receiver VM.</span></span>

<span data-ttu-id="18b2a-116">Tip: Als deze test voor de eerste keer instelt, probeer u mogelijk een kortere testperiode om feedback sneller.</span><span class="sxs-lookup"><span data-stu-id="18b2a-116">Tip: When setting up this test for the first time, you might try a shorter test period to get feedback sooner.</span></span> <span data-ttu-id="18b2a-117">Zodra de tool werkt zoals verwacht, breid u de testperiode aan 300 seconden voor de meest nauwkeurige resultaten.</span><span class="sxs-lookup"><span data-stu-id="18b2a-117">Once the tool is working as expected, extend the test period to 300 seconds for the most accurate results.</span></span>

> [!NOTE]
> <span data-ttu-id="18b2a-118">De afzender **en** ontvanger moet opgeven **dezelfde** testen duur van de parameter (-t).</span><span class="sxs-lookup"><span data-stu-id="18b2a-118">The sender **and** receiver must specify **the same** test duration parameter (-t).</span></span>

<span data-ttu-id="18b2a-119">Voor het testen van één TCP-stroom voor 10 seconden:</span><span class="sxs-lookup"><span data-stu-id="18b2a-119">To test a single TCP stream for 10 seconds:</span></span>

<span data-ttu-id="18b2a-120">Ontvanger parameters: ntttcp - r -t 10 - P 1</span><span class="sxs-lookup"><span data-stu-id="18b2a-120">Receiver parameters: ntttcp -r -t 10 -P 1</span></span>

<span data-ttu-id="18b2a-121">Parameters van de afzender: ntttcp-s10.27.33.7 -t 10 - n 1 -P 1</span><span class="sxs-lookup"><span data-stu-id="18b2a-121">Sender parameters: ntttcp -s10.27.33.7 -t 10 -n 1 -P 1</span></span>

> [!NOTE]
> <span data-ttu-id="18b2a-122">Het vorige voorbeeld mag alleen worden gebruikt om te bevestigen dat de configuratie.</span><span class="sxs-lookup"><span data-stu-id="18b2a-122">The preceding sample should only be used to confirm your configuration.</span></span> <span data-ttu-id="18b2a-123">Aantal voorbeelden van testen worden verderop in dit document besproken.</span><span class="sxs-lookup"><span data-stu-id="18b2a-123">Valid examples of testing are covered later in this document.</span></span>

## <a name="testing-vms-running-windows"></a><span data-ttu-id="18b2a-124">Testen van virtuele machines waarop WINDOWS wordt uitgevoerd:</span><span class="sxs-lookup"><span data-stu-id="18b2a-124">Testing VMs running WINDOWS:</span></span>

#### <a name="get-ntttcp-onto-the-vms"></a><span data-ttu-id="18b2a-125">NTTTCP op de virtuele machines worden opgehaald.</span><span class="sxs-lookup"><span data-stu-id="18b2a-125">Get NTTTCP onto the VMs.</span></span>

<span data-ttu-id="18b2a-126">Download de nieuwste versie: <https://gallery.technet.microsoft.com/NTttcp-Version-528-Now-f8b12769></span><span class="sxs-lookup"><span data-stu-id="18b2a-126">Download the latest version: <https://gallery.technet.microsoft.com/NTttcp-Version-528-Now-f8b12769></span></span>

<span data-ttu-id="18b2a-127">Of zoekt u het als verplaatst: <https://www.bing.com/search?q=ntttcp+download> \< --moet eerst worden bereikt</span><span class="sxs-lookup"><span data-stu-id="18b2a-127">Or search for it if moved: <https://www.bing.com/search?q=ntttcp+download>\< -- should be first hit</span></span>

<span data-ttu-id="18b2a-128">Overweeg NTTTCP plaatsen in een afzonderlijke map, zoals c:\\hulpprogramma's</span><span class="sxs-lookup"><span data-stu-id="18b2a-128">Consider putting NTTTCP in separate folder, like c:\\tools</span></span>

#### <a name="allow-ntttcp-through-the-windows-firewall"></a><span data-ttu-id="18b2a-129">NTTTCP toestaan via de Windows-firewall</span><span class="sxs-lookup"><span data-stu-id="18b2a-129">Allow NTTTCP through the Windows firewall</span></span>
<span data-ttu-id="18b2a-130">Maak een regel voor toestaan op de Windows Firewall zodat het verkeer NTTTCP moet worden uitgevoerd op de ontvanger.</span><span class="sxs-lookup"><span data-stu-id="18b2a-130">On the RECEIVER, create an Allow rule on the Windows Firewall to allow the NTTTCP traffic to arrive.</span></span> <span data-ttu-id="18b2a-131">Het gemakkelijkst om toe te staan van het volledige NTTTCP programma met de naam in plaats van dat specifieke TCP-poorten inkomend.</span><span class="sxs-lookup"><span data-stu-id="18b2a-131">It's easiest to allow the entire NTTTCP program by name rather than to allow specific TCP ports inbound.</span></span>

<span data-ttu-id="18b2a-132">Toestaan dat ntttcp via de Windows Firewall als volgt:</span><span class="sxs-lookup"><span data-stu-id="18b2a-132">Allow ntttcp through the Windows Firewall like this:</span></span>

<span data-ttu-id="18b2a-133">Netsh advfirewall firewall regel programma toevoegen =\<pad\>\\ntttcp.exe name = "ntttcp" protocol eventuele dir = in actie = = toestaan inschakelen = yes profile = ANY</span><span class="sxs-lookup"><span data-stu-id="18b2a-133">netsh advfirewall firewall add rule program=\<PATH\>\\ntttcp.exe name="ntttcp" protocol=any dir=in action=allow enable=yes profile=ANY</span></span>

<span data-ttu-id="18b2a-134">Bijvoorbeeld, als u hebt gekopieerd ntttcp.exe aan de ' c:\\extra ' map, zou dit de opdracht:</span><span class="sxs-lookup"><span data-stu-id="18b2a-134">For example, if you copied ntttcp.exe to the "c:\\tools" folder, this would be the command:</span></span> 

<span data-ttu-id="18b2a-135">Netsh advfirewall firewall regel programma toevoegen = c:\\hulpprogramma's\\ntttcp.exe naam = 'ntttcp' protocol eventuele dir = in actie = = toestaan inschakelen = yes profile = ANY</span><span class="sxs-lookup"><span data-stu-id="18b2a-135">netsh advfirewall firewall add rule program=c:\\tools\\ntttcp.exe name="ntttcp" protocol=any dir=in action=allow enable=yes profile=ANY</span></span>

#### <a name="running-ntttcp-tests"></a><span data-ttu-id="18b2a-136">NTTTCP tests die worden uitgevoerd</span><span class="sxs-lookup"><span data-stu-id="18b2a-136">Running NTTTCP tests</span></span>

<span data-ttu-id="18b2a-137">NTTTCP starten op de ontvanger (**uitvoeren vanaf CMD**, niet vanuit PowerShell):</span><span class="sxs-lookup"><span data-stu-id="18b2a-137">Start NTTTCP on the RECEIVER (**run from CMD**, not from PowerShell):</span></span>

<span data-ttu-id="18b2a-138">ntttcp - r-m [2\*\#num\_kernen],\*, 300 a.b.c.r -t</span><span class="sxs-lookup"><span data-stu-id="18b2a-138">ntttcp -r –m [2\*\#num\_cores],\*,a.b.c.r -t 300</span></span>

<span data-ttu-id="18b2a-139">Als de virtuele machine vier kernen en het IP-adres 10.0.0.4 heeft, wordt deze eruit als volgt:</span><span class="sxs-lookup"><span data-stu-id="18b2a-139">If the VM has four cores and an IP address of 10.0.0.4, it would look like this:</span></span>

<span data-ttu-id="18b2a-140">ntttcp - r – m 8,\*, 10.0.0.4 -t 300</span><span class="sxs-lookup"><span data-stu-id="18b2a-140">ntttcp -r –m 8,\*,10.0.0.4 -t 300</span></span>


<span data-ttu-id="18b2a-141">NTTTCP starten op de afzender (**uitvoeren vanaf CMD**, niet vanuit PowerShell):</span><span class="sxs-lookup"><span data-stu-id="18b2a-141">Start NTTTCP on the SENDER (**run from CMD**, not from PowerShell):</span></span>

<span data-ttu-id="18b2a-142">ntttcp -s-m 8,\*, 10.0.0.4 -t 300</span><span class="sxs-lookup"><span data-stu-id="18b2a-142">ntttcp -s –m 8,\*,10.0.0.4 -t 300</span></span> 

<span data-ttu-id="18b2a-143">Wacht totdat de resultaten.</span><span class="sxs-lookup"><span data-stu-id="18b2a-143">Wait for the results.</span></span>


## <a name="testing-vms-running-linux"></a><span data-ttu-id="18b2a-144">Testen van virtuele machines waarop LINUX wordt uitgevoerd:</span><span class="sxs-lookup"><span data-stu-id="18b2a-144">Testing VMs running LINUX:</span></span>

<span data-ttu-id="18b2a-145">Gebruik nttcp voor linux.</span><span class="sxs-lookup"><span data-stu-id="18b2a-145">Use nttcp-for-linux.</span></span> <span data-ttu-id="18b2a-146">Deze beschikbaar is via <https://github.com/Microsoft/ntttcp-for-linux></span><span class="sxs-lookup"><span data-stu-id="18b2a-146">It is available from <https://github.com/Microsoft/ntttcp-for-linux></span></span>

<span data-ttu-id="18b2a-147">Op de virtuele Linux-machines (ZENDER en ontvanger), moet u deze opdrachten om voor te bereiden ntttcp voor linux op uw virtuele machines uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="18b2a-147">On the Linux VMs (both SENDER and RECEIVER), run these commands to prepare ntttcp-for-linux on your VMs:</span></span>

<span data-ttu-id="18b2a-148">CentOS - Git installeren:</span><span class="sxs-lookup"><span data-stu-id="18b2a-148">CentOS - Install Git:</span></span>
``` bash
  yum install gcc -y  
  yum install git -y
```
<span data-ttu-id="18b2a-149">Ubuntu - Git installeren:</span><span class="sxs-lookup"><span data-stu-id="18b2a-149">Ubuntu - Install Git:</span></span>
``` bash
 apt-get -y install build-essential  
 apt-get -y install git
```
<span data-ttu-id="18b2a-150">Maken en te installeren op beide:</span><span class="sxs-lookup"><span data-stu-id="18b2a-150">Make and Install on both:</span></span>
``` bash
 git clone <https://github.com/Microsoft/ntttcp-for-linux>
 cd ntttcp-for-linux/src
 make && make install
```

<span data-ttu-id="18b2a-151">Zoals in het Windows-voorbeeld gaan we ervan uit dat IP-adres van de Linux-ontvanger is 10.0.0.4</span><span class="sxs-lookup"><span data-stu-id="18b2a-151">As in the Windows example, we assume the Linux RECEIVER's IP is 10.0.0.4</span></span>

<span data-ttu-id="18b2a-152">Start NTTTCP voor Linux op de ontvanger:</span><span class="sxs-lookup"><span data-stu-id="18b2a-152">Start NTTTCP-for-Linux on the RECEIVER:</span></span>

``` bash
ntttcp -r -t 300
```

<span data-ttu-id="18b2a-153">En voer op de afzender:</span><span class="sxs-lookup"><span data-stu-id="18b2a-153">And on the SENDER, run:</span></span>

``` bash
ntttcp -s10.0.0.4 -t 300
```
 
<span data-ttu-id="18b2a-154">Test lengte van de standaardwaarde is 60 seconden als er is geen tijdsparameter is gegeven</span><span class="sxs-lookup"><span data-stu-id="18b2a-154">Test length defaults to 60 seconds if no time parameter is given</span></span>

## <a name="testing-between-vms-running-windows-and-linux"></a><span data-ttu-id="18b2a-155">Testen tussen VM's met Windows en LINUX:</span><span class="sxs-lookup"><span data-stu-id="18b2a-155">Testing between VMs running Windows and LINUX:</span></span>

<span data-ttu-id="18b2a-156">Op deze scenario's moeten we de Nee-sync-modus inschakelen zodat de test kunt uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="18b2a-156">On this scenarios we should enable the no-sync mode so the test can run.</span></span> <span data-ttu-id="18b2a-157">Dit wordt gedaan met behulp van de **-N vlag** voor Linux en **-ns vlag** voor Windows.</span><span class="sxs-lookup"><span data-stu-id="18b2a-157">This is done by using the **-N flag** for Linux, and **-ns flag** for Windows.</span></span>

#### <a name="from-linux-to-windows"></a><span data-ttu-id="18b2a-158">Van Linux bij Windows:</span><span class="sxs-lookup"><span data-stu-id="18b2a-158">From Linux to Windows:</span></span>

<span data-ttu-id="18b2a-159">Ontvanger <Windows>:</span><span class="sxs-lookup"><span data-stu-id="18b2a-159">Receiver <Windows>:</span></span>

``` bash
ntttcp -r -m <2 x nr cores>,*,<Windows server IP>
```

<span data-ttu-id="18b2a-160">Afzender <Linux> :</span><span class="sxs-lookup"><span data-stu-id="18b2a-160">Sender <Linux> :</span></span>

``` bash
ntttcp -s -m <2 x nr cores>,*,<Windows server IP> -N -t 300
```

#### <a name="from-windows-to-linux"></a><span data-ttu-id="18b2a-161">Van Windows naar Linux:</span><span class="sxs-lookup"><span data-stu-id="18b2a-161">From Windows to Linux:</span></span>

<span data-ttu-id="18b2a-162">Ontvanger <Linux>:</span><span class="sxs-lookup"><span data-stu-id="18b2a-162">Receiver <Linux>:</span></span>

``` bash
ntttcp -r -m <2 x nr cores>,*,<Linux server IP>
```

<span data-ttu-id="18b2a-163">Afzender <Windows>:</span><span class="sxs-lookup"><span data-stu-id="18b2a-163">Sender <Windows>:</span></span>

``` bash
ntttcp -s -m <2 x nr cores>,*,<Linux  server IP> -ns -t 300
```

## <a name="next-steps"></a><span data-ttu-id="18b2a-164">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="18b2a-164">Next steps</span></span>
* <span data-ttu-id="18b2a-165">Afhankelijk van de resultaten, kunnen er ruimte is om te [netwerk doorvoer machines optimaliseren](virtual-network-optimize-network-bandwidth.md) voor uw scenario.</span><span class="sxs-lookup"><span data-stu-id="18b2a-165">Depending on results, there may be room to [Optimize network throughput machines](virtual-network-optimize-network-bandwidth.md) for your scenario.</span></span>
* <span data-ttu-id="18b2a-166">Klik hier als u meer wilt weten met [Azure Virtual Network Veelgestelde vragen (FAQ)](virtual-networks-faq.md)</span><span class="sxs-lookup"><span data-stu-id="18b2a-166">Learn more wtih [Azure Virtual Network frequently asked questions (FAQ)](virtual-networks-faq.md)</span></span>

---
title: Valideren van de VPN-doorvoer tooa Microsoft Azure Virtual Network | Microsoft Docs
description: Hallo doel van dit document is toohelp een gebruiker valideren Hallo netwerkdoorvoer van hun lokale bronnen tooan virtuele machine van Azure.
services: vpn-gateway
documentationcenter: na
author: chadmath
manager: jasmc
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/10/2017
ms.author: radwiv;chadmat;genli
ms.openlocfilehash: 9cf0b67145645a3c2a9556b0cc910066cc62a9ab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toovalidate-vpn-throughput-tooa-virtual-network"></a><span data-ttu-id="80feb-103">Hoe toovalidate VPN-doorvoer tooa virtueel netwerk</span><span class="sxs-lookup"><span data-stu-id="80feb-103">How toovalidate VPN throughput tooa virtual network</span></span>

<span data-ttu-id="80feb-104">Een VPN-gatewayverbinding kunt u tooestablish veilige, cross-premises-connectiviteit tussen uw virtuele netwerk in Azure en uw on-premises IT-infrastructuur.</span><span class="sxs-lookup"><span data-stu-id="80feb-104">A VPN gateway connection enables you tooestablish secure, cross-premises connectivity between your Virtual Network within Azure and your on-premises IT infrastructure.</span></span>

<span data-ttu-id="80feb-105">Dit artikel laat zien hoe de netwerkdoorvoer toovalidate van Hallo lokale bronnen tooan virtuele machine van Azure.</span><span class="sxs-lookup"><span data-stu-id="80feb-105">This article shows how toovalidate network throughput from hello on-premises resources tooan Azure virtual machine.</span></span> <span data-ttu-id="80feb-106">Het bevat ook richtlijnen voor probleemoplossing.</span><span class="sxs-lookup"><span data-stu-id="80feb-106">It also provides troubleshooting guidance.</span></span>

>[!NOTE]
><span data-ttu-id="80feb-107">Dit artikel is bedoeld toohelp opsporen en oplossen van veelvoorkomende problemen.</span><span class="sxs-lookup"><span data-stu-id="80feb-107">This article is intended toohelp diagnose and fix common issues.</span></span> <span data-ttu-id="80feb-108">Als u niet kan toosolve Hallo probleem met behulp van informatie na Hallo [contact op met ondersteuning](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span><span class="sxs-lookup"><span data-stu-id="80feb-108">If you're unable toosolve hello issue by using hello following information, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span></span>
>
>

## <a name="overview"></a><span data-ttu-id="80feb-109">Overzicht</span><span class="sxs-lookup"><span data-stu-id="80feb-109">Overview</span></span>

<span data-ttu-id="80feb-110">Hallo VPN-gatewayverbinding omvat Hallo volgende onderdelen:</span><span class="sxs-lookup"><span data-stu-id="80feb-110">hello VPN gateway connection involves hello following components:</span></span>

- <span data-ttu-id="80feb-111">On-premises VPN-apparaat (een lijst weergeven met [gevalideerde VPN-apparaten)](vpn-gateway-about-vpn-devices.md#devicetable).</span><span class="sxs-lookup"><span data-stu-id="80feb-111">On-premises VPN device (view a list of [validated VPN devices)](vpn-gateway-about-vpn-devices.md#devicetable).</span></span>
- <span data-ttu-id="80feb-112">Openbare Internet</span><span class="sxs-lookup"><span data-stu-id="80feb-112">Public Internet</span></span>
- <span data-ttu-id="80feb-113">Azure VPN-gateway</span><span class="sxs-lookup"><span data-stu-id="80feb-113">Azure VPN gateway</span></span>
- <span data-ttu-id="80feb-114">virtuele Azure-machine</span><span class="sxs-lookup"><span data-stu-id="80feb-114">Azure virtual machine</span></span>

<span data-ttu-id="80feb-115">Hallo volgende diagram toont Hallo logische verbinding van een lokaal netwerk tooan virtuele Azure-netwerk via VPN-verbinding.</span><span class="sxs-lookup"><span data-stu-id="80feb-115">hello following diagram shows hello logical connectivity of an on-premises network tooan Azure virtual network through VPN.</span></span>

![Logische connectiviteit van het netwerk klant tooMSFT netwerk via een VPN](./media/vpn-gateway-validate-throughput-to-vnet/VPNPerf.png)

## <a name="calculate-hello-maximum-expected-ingressegress"></a><span data-ttu-id="80feb-117">Hallo maximale verwachte inkomend en uitgaand berekenen</span><span class="sxs-lookup"><span data-stu-id="80feb-117">Calculate hello maximum expected ingress/egress</span></span>

1.  <span data-ttu-id="80feb-118">Bepaal de basisvereisten voor doorvoer van uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="80feb-118">Determine your application's baseline throughput requirements.</span></span>
2.  <span data-ttu-id="80feb-119">Bepaal de doorvoerlimieten van uw Azure VPN-gateway.</span><span class="sxs-lookup"><span data-stu-id="80feb-119">Determine your Azure VPN gateway throughput limits.</span></span> <span data-ttu-id="80feb-120">Zie voor meer informatie Hallo 'geaggregeerde doorvoer per SKU en VPN-type'-sectie van [Planning en ontwerp voor VPN-Gateway](vpn-gateway-plan-design.md).</span><span class="sxs-lookup"><span data-stu-id="80feb-120">For help, see hello "Aggregate throughput by SKU and VPN type" section of [Planning and design for VPN Gateway](vpn-gateway-plan-design.md).</span></span>
3.  <span data-ttu-id="80feb-121">Hallo bepalen [Azure VM doorvoer richtlijnen](../virtual-machines/virtual-machines-windows-sizes.md) voor uw VM-grootte.</span><span class="sxs-lookup"><span data-stu-id="80feb-121">Determine hello [Azure VM throughput guidance](../virtual-machines/virtual-machines-windows-sizes.md) for your VM size.</span></span>
4.  <span data-ttu-id="80feb-122">Bepaal uw bandbreedte Internetproviderverbindingen (ISP).</span><span class="sxs-lookup"><span data-stu-id="80feb-122">Determine your Internet Service Provider (ISP) bandwidth.</span></span>
5.  <span data-ttu-id="80feb-123">Berekenen van de verwachte doorvoer - minimale bandbreedte van (ISP VM,-Gateway) * 0,8.</span><span class="sxs-lookup"><span data-stu-id="80feb-123">Calculate your expected throughput - Least bandwidth of (VM, Gateway, ISP) * 0.8.</span></span>

<span data-ttu-id="80feb-124">Als uw berekende doorvoer voldoet niet aan de basisvereisten doorvoer van uw toepassing, moet u tooincrease Hallo bandbreedte van Hallo resource die u hebt geïdentificeerd als Hallo knelpunt.</span><span class="sxs-lookup"><span data-stu-id="80feb-124">If your calculated throughput does not meet your application's baseline throughput requirements, you need tooincrease hello bandwidth of hello resource that you identified as hello bottleneck.</span></span> <span data-ttu-id="80feb-125">Zie voor een Azure VPN-Gateway tooresize [wijzigen van een gateway-SKU](https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-about-vpn-gateway-settings.md#gwsku).</span><span class="sxs-lookup"><span data-stu-id="80feb-125">tooresize an Azure VPN Gateway, see [Changing a gateway SKU](https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-about-vpn-gateway-settings.md#gwsku).</span></span> <span data-ttu-id="80feb-126">Zie voor een virtuele machine, tooresize [vergroten of verkleinen van een virtuele machine](../virtual-machines/virtual-machines-windows-resize-vm.md).</span><span class="sxs-lookup"><span data-stu-id="80feb-126">tooresize a virtual machine, see [Resize a VM](../virtual-machines/virtual-machines-windows-resize-vm.md).</span></span> <span data-ttu-id="80feb-127">Als u niet de verwachte internetbandbreedte ondervindt nog, kunt u ook toocontact uw Internetprovider.</span><span class="sxs-lookup"><span data-stu-id="80feb-127">If you are not experiencing expected Internet bandwidth, you may also want toocontact your ISP.</span></span>

## <a name="validate-network-throughput-by-using-performance-tools"></a><span data-ttu-id="80feb-128">Netwerkdoorvoer valideren met behulp van hulpprogramma's voor prestaties</span><span class="sxs-lookup"><span data-stu-id="80feb-128">Validate network throughput by using performance tools</span></span>

<span data-ttu-id="80feb-129">Deze validatie moet worden uitgevoerd tijdens daluren, zoals VPN-tunnel doorvoer verzadiging tijdens het testen geen nauwkeurige resultaten geeft.</span><span class="sxs-lookup"><span data-stu-id="80feb-129">This validation should be performed during non-peak hours, as VPN tunnel throughput saturation during testing does not give accurate results.</span></span>

<span data-ttu-id="80feb-130">Hallo-hulpprogramma we voor deze test gebruiken is iPerf die werkt op Windows- en Linux- en heeft zowel client als server modi.</span><span class="sxs-lookup"><span data-stu-id="80feb-130">hello tool we use for this test is iPerf, which works on both Windows and Linux and has both client and server modes.</span></span> <span data-ttu-id="80feb-131">Beperkte too3 Gbps voor VM's van Windows is.</span><span class="sxs-lookup"><span data-stu-id="80feb-131">It is limited too3 Gbps for Windows VMs.</span></span>

<span data-ttu-id="80feb-132">Dit hulpprogramma voert bewerkingen lezen/schrijven toodisk.</span><span class="sxs-lookup"><span data-stu-id="80feb-132">This tool does not perform any read/write operations toodisk.</span></span> <span data-ttu-id="80feb-133">Zelfgegenereerd TCP-verkeer van één end toohello andere produceert uitsluitend.</span><span class="sxs-lookup"><span data-stu-id="80feb-133">It solely produces self-generated TCP traffic from one end toohello other.</span></span> <span data-ttu-id="80feb-134">Deze statistieken op basis van experimenten die Hallo bandbreedte tussen client en server knooppunten beschikbaar meet zijn gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="80feb-134">It generated statistics based on experimentation that measures hello bandwidth available between client and server nodes.</span></span> <span data-ttu-id="80feb-135">Bij het testen van tussen twee knooppunten, fungeert een als Hallo-server en Hallo andere als een client.</span><span class="sxs-lookup"><span data-stu-id="80feb-135">When testing between two nodes, one acts as hello server and hello other as a client.</span></span> <span data-ttu-id="80feb-136">Als deze test is voltooid, wordt u aangeraden dat u Hallo rollen tootest beide uploaden en downloaden van doorvoer op beide knooppunten ongedaan maken.</span><span class="sxs-lookup"><span data-stu-id="80feb-136">Once this test is completed, we recommend that you reverse hello roles tootest both upload and download throughput on both nodes.</span></span>

### <a name="download-iperf"></a><span data-ttu-id="80feb-137">IPerf downloaden</span><span class="sxs-lookup"><span data-stu-id="80feb-137">Download iPerf</span></span>
<span data-ttu-id="80feb-138">Download [iPerf](https://iperf.fr/download/iperf_3.1/iperf-3.1.2-win64.zip).</span><span class="sxs-lookup"><span data-stu-id="80feb-138">Download [iPerf](https://iperf.fr/download/iperf_3.1/iperf-3.1.2-win64.zip).</span></span> <span data-ttu-id="80feb-139">Zie voor meer informatie [iPerf documentatie](https://iperf.fr/iperf-doc.php).</span><span class="sxs-lookup"><span data-stu-id="80feb-139">For details, see [iPerf documentation](https://iperf.fr/iperf-doc.php).</span></span>

 >[!NOTE]
 ><span data-ttu-id="80feb-140">Hallo van derden producten die in dit artikel wordt beschreven, zijn geproduceerd door bedrijven die onafhankelijk van Microsoft zijn.</span><span class="sxs-lookup"><span data-stu-id="80feb-140">hello third-party products that this article discusses are manufactured by companies that are independent of Microsoft.</span></span> <span data-ttu-id="80feb-141">Microsoft geeft geen garantie, impliciet of anderszins over Hallo prestaties of de betrouwbaarheid van deze producten.</span><span class="sxs-lookup"><span data-stu-id="80feb-141">Microsoft makes no warranty, implied or otherwise, about hello performance or reliability of these products.</span></span>
 >
 >

### <a name="run-iperf-iperf3exe"></a><span data-ttu-id="80feb-142">Voer iPerf (iperf3.exe)</span><span class="sxs-lookup"><span data-stu-id="80feb-142">Run iPerf (iperf3.exe)</span></span>
1. <span data-ttu-id="80feb-143">Een NSG/ACL-regel Hallo-verkeer (voor openbare IP-adres testen op Azure VM) inschakelen.</span><span class="sxs-lookup"><span data-stu-id="80feb-143">Enable an NSG/ACL rule allowing hello traffic (for public IP address testing on Azure VM).</span></span>

2. <span data-ttu-id="80feb-144">Schakel een firewall-uitzondering voor poort 5001 op beide knooppunten.</span><span class="sxs-lookup"><span data-stu-id="80feb-144">On both nodes, enable a firewall exception for port 5001.</span></span>

    <span data-ttu-id="80feb-145">**Windows:** uitvoeren Hallo volgende opdracht uit als beheerder:</span><span class="sxs-lookup"><span data-stu-id="80feb-145">**Windows:** Run hello following command as an administrator:</span></span>

    ```CMD
    netsh advfirewall firewall add rule name="Open Port 5001" dir=in action=allow protocol=TCP localport=5001
    ```

    <span data-ttu-id="80feb-146">tooremove hello regel bij het testen is voltooid, voert u deze opdracht:</span><span class="sxs-lookup"><span data-stu-id="80feb-146">tooremove hello rule when testing is complete, run this command:</span></span>

    ```CMD
    netsh advfirewall firewall delete rule name="Open Port 5001" protocol=TCP localport=5001
    ```
    </br>
    <span data-ttu-id="80feb-147">**Azure Linux:** Azure Linux afbeeldingen hebt strikte firewalls.</span><span class="sxs-lookup"><span data-stu-id="80feb-147">**Azure Linux:**  Azure Linux images have permissive firewalls.</span></span> <span data-ttu-id="80feb-148">Als er een toepassing naar een poort luistert, wordt door Hallo verkeer toegestaan.</span><span class="sxs-lookup"><span data-stu-id="80feb-148">If there is an application listening on a port, hello traffic is allowed through.</span></span> <span data-ttu-id="80feb-149">Aangepaste installatiekopieën die zijn beveiligd wellicht poorten expliciet geopend.</span><span class="sxs-lookup"><span data-stu-id="80feb-149">Custom images that are secured may need ports opened explicitly.</span></span> <span data-ttu-id="80feb-150">Algemene firewalls voor Linux OS-laag omvatten `iptables`, `ufw`, of `firewalld`.</span><span class="sxs-lookup"><span data-stu-id="80feb-150">Common Linux OS-layer firewalls include `iptables`, `ufw`, or `firewalld`.</span></span>

3. <span data-ttu-id="80feb-151">Op de server-knooppunt Hallo wijzigen toohello directory waar iperf3.exe is uitgepakt.</span><span class="sxs-lookup"><span data-stu-id="80feb-151">On hello server node, change toohello directory where iperf3.exe is extracted.</span></span> <span data-ttu-id="80feb-152">Vervolgens iPerf in de servermodus en stel deze toolisten op poort 5001 als Hallo volgende opdrachten:</span><span class="sxs-lookup"><span data-stu-id="80feb-152">Then run iPerf in server mode and set it toolisten on port 5001 as hello following commands:</span></span>

     ```CMD
     cd c:\iperf-3.1.2-win65

     iperf3.exe -s -p 5001
     ```

4. <span data-ttu-id="80feb-153">Op de client-knooppunt Hallo wijzigen toohello directory waarbij iperf hulpprogramma uitgepakt en Voer Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="80feb-153">On hello client node, change toohello directory where iperf tool is extracted and then run hello following command:</span></span>

    ```CMD
    iperf3.exe -c <IP of hello iperf Server> -t 30 -p 5001 -P 32
    ```

    <span data-ttu-id="80feb-154">Hallo-client wordt verkeer op poort 5001 toohello server veroorzaken gedurende 30 seconden.</span><span class="sxs-lookup"><span data-stu-id="80feb-154">hello client is inducing traffic on port 5001 toohello server for 30 seconds.</span></span> <span data-ttu-id="80feb-155">vlag Hallo '-P ' die aangeeft dat we 32 knooppunten van gelijktijdige verbindingen toohello server gebruiken.</span><span class="sxs-lookup"><span data-stu-id="80feb-155">hello flag '-P ' that indicates we are using 32 simultaneous connections toohello server node.</span></span>

    <span data-ttu-id="80feb-156">Hallo ziet volgende scherm Hallo-uitvoer van dit voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="80feb-156">hello following screen shows hello output from this example:</span></span>

    ![Uitvoer](./media/vpn-gateway-validate-throughput-to-vnet/06theoutput.png)

5. <span data-ttu-id="80feb-158">(Optioneel) toopreserve Hallo testresultaten deze opdracht uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="80feb-158">(OPTIONAL) toopreserve hello testing results, run this command:</span></span>

    ```CMD
    iperf3.exe -c IPofTheServerToReach -t 30 -p 5001 -P 32  >> output.txt
    ```

6. <span data-ttu-id="80feb-159">Uitvoeren na het voltooien van de vorige stappen Hallo Hallo dezelfde stappen Hallo-functies is teruggedraaid, zodat hello serverknooppunt nu Hallo-client en vice versa worden kan.</span><span class="sxs-lookup"><span data-stu-id="80feb-159">After completing hello previous steps, execute hello same steps with hello roles reversed, so that hello server node will now be hello client and vice-versa.</span></span>

## <a name="address-slow-file-copy-issues"></a><span data-ttu-id="80feb-160">Problemen met adres trage bestanden kopiëren</span><span class="sxs-lookup"><span data-stu-id="80feb-160">Address slow file copy issues</span></span>
<span data-ttu-id="80feb-161">Er kunnen optreden langzaam bestand kopiëren wanneer u Windows Verkenner of slepen en neerzetten via een RDP-sessie.</span><span class="sxs-lookup"><span data-stu-id="80feb-161">You may experience slow file coping when using Windows Explorer or dragging and dropping through an RDP session.</span></span> <span data-ttu-id="80feb-162">Dit probleem is normaal gesproken vervaldatum tooone of beide Hallo volgende factoren:</span><span class="sxs-lookup"><span data-stu-id="80feb-162">This problem is normally due tooone or both of hello following factors:</span></span>

- <span data-ttu-id="80feb-163">Bestand kopiëren toepassingen, zoals Windows Verkenner en RDP, meerdere threads niet gebruiken tijdens het kopiëren van bestanden.</span><span class="sxs-lookup"><span data-stu-id="80feb-163">File copy applications, such as Windows Explorer and RDP, do not use multiple threads when copying files.</span></span> <span data-ttu-id="80feb-164">Gebruik voor betere prestaties een kopie-toepassing met meerdere threads bestand, zoals [Richcopy](https://technet.microsoft.com/en-us/magazine/2009.04.utilityspotlight.aspx) toocopy bestanden met behulp van 16 of 32 threads.</span><span class="sxs-lookup"><span data-stu-id="80feb-164">For better performance, use a multi-threaded file copy application such as [Richcopy](https://technet.microsoft.com/en-us/magazine/2009.04.utilityspotlight.aspx) toocopy files by using 16 or 32 threads.</span></span> <span data-ttu-id="80feb-165">toochange hello thread nummer voor het kopiëren van bestanden in Richcopy, klikt u op **actie** > **opties kopiëren** > **bestanden zijn gekopieerd**.</span><span class="sxs-lookup"><span data-stu-id="80feb-165">toochange hello thread number for file copy in Richcopy, click **Action** > **Copy options** > **File copy**.</span></span><br><br><span data-ttu-id="80feb-166">
![Problemen met trage bestanden kopiëren](./media/vpn-gateway-validate-throughput-to-vnet/Richcopy.png)</span><span class="sxs-lookup"><span data-stu-id="80feb-166">
![Slow file copy issues](./media/vpn-gateway-validate-throughput-to-vnet/Richcopy.png)</span></span><br>
- <span data-ttu-id="80feb-167">Onvoldoende VM schijf lezen/schrijven-snelheid.</span><span class="sxs-lookup"><span data-stu-id="80feb-167">Insufficient VM disk read/write speed.</span></span> <span data-ttu-id="80feb-168">Zie voor meer informatie [Azure Storage probleemoplossing](../storage/common/storage-e2e-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="80feb-168">For more information, see [Azure Storage Troubleshooting](../storage/common/storage-e2e-troubleshooting.md).</span></span>

## <a name="on-premises-device-external-facing-interface"></a><span data-ttu-id="80feb-169">Lokale apparaat extern gerichte interface</span><span class="sxs-lookup"><span data-stu-id="80feb-169">On-premises device external facing interface</span></span>
<span data-ttu-id="80feb-170">Als Hallo lokale VPN-apparaat internetgerichte IP-adres is opgenomen in Hallo [lokale netwerk](vpn-gateway-howto-site-to-site-resource-manager-portal.md#LocalNetworkGateway) definitie in Azure, treden onvermogen toobring Hallo VPN, sporadisch verbinding wordt verbroken of prestatieproblemen.</span><span class="sxs-lookup"><span data-stu-id="80feb-170">If hello on-premises VPN device Internet-facing IP address is included in hello [local network](vpn-gateway-howto-site-to-site-resource-manager-portal.md#LocalNetworkGateway) definition in Azure, you may experience inability toobring up hello VPN, sporadic disconnects, or performance issues.</span></span>

## <a name="checking-latency"></a><span data-ttu-id="80feb-171">Latentie controleren</span><span class="sxs-lookup"><span data-stu-id="80feb-171">Checking latency</span></span>
<span data-ttu-id="80feb-172">Tracert tootrace tooMicrosoft Azure rand apparaat toodetermine gebruiken als er meer dan 100 milliseconden tussen hops vertragingen.</span><span class="sxs-lookup"><span data-stu-id="80feb-172">Use tracert tootrace tooMicrosoft Azure Edge device toodetermine if there are any delays exceeding 100 ms between hops.</span></span>

<span data-ttu-id="80feb-173">Voer vanuit Hallo on-premises netwerk, *tracert* toohello VIP van hello Azure Gateway of VM.</span><span class="sxs-lookup"><span data-stu-id="80feb-173">From hello on-premises network, run *tracert* toohello VIP of hello Azure Gateway or VM.</span></span> <span data-ttu-id="80feb-174">Eenmaal u alleen ziet * geretourneerd, u weet hello Azure rand is bereikt.</span><span class="sxs-lookup"><span data-stu-id="80feb-174">Once you see only * returned, you know you have reached hello Azure edge.</span></span> <span data-ttu-id="80feb-175">Als u DNS-namen met 'MSN' geretourneerd ziet, weet u dat Hallo Microsoft backbone is bereikt.</span><span class="sxs-lookup"><span data-stu-id="80feb-175">When you see DNS names that include "MSN" returned, you know you have reached hello Microsoft backbone.</span></span><br><br><span data-ttu-id="80feb-176">
![Latentie controleren](./media/vpn-gateway-validate-throughput-to-vnet/08checkinglatency.png)</span><span class="sxs-lookup"><span data-stu-id="80feb-176">
![Checking Latency](./media/vpn-gateway-validate-throughput-to-vnet/08checkinglatency.png)</span></span>

## <a name="next-steps"></a><span data-ttu-id="80feb-177">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="80feb-177">Next steps</span></span>
<span data-ttu-id="80feb-178">Bekijk voor meer informatie en hulp Hallo koppelingen te volgen:</span><span class="sxs-lookup"><span data-stu-id="80feb-178">For more information or help, check out hello following links:</span></span>

- [<span data-ttu-id="80feb-179">Netwerkdoorvoer voor Azure virtual machines optimaliseren</span><span class="sxs-lookup"><span data-stu-id="80feb-179">Optimize network throughput for Azure virtual machines</span></span>](../virtual-network/virtual-network-optimize-network-bandwidth.md)
- [<span data-ttu-id="80feb-180">Microsoft-ondersteuning</span><span class="sxs-lookup"><span data-stu-id="80feb-180">Microsoft Support</span></span>](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade)

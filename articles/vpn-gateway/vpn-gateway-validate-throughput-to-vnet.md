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
# <a name="how-toovalidate-vpn-throughput-tooa-virtual-network"></a>Hoe toovalidate VPN-doorvoer tooa virtueel netwerk

Een VPN-gatewayverbinding kunt u tooestablish veilige, cross-premises-connectiviteit tussen uw virtuele netwerk in Azure en uw on-premises IT-infrastructuur.

Dit artikel laat zien hoe de netwerkdoorvoer toovalidate van Hallo lokale bronnen tooan virtuele machine van Azure. Het bevat ook richtlijnen voor probleemoplossing.

>[!NOTE]
>Dit artikel is bedoeld toohelp opsporen en oplossen van veelvoorkomende problemen. Als u niet kan toosolve Hallo probleem met behulp van informatie na Hallo [contact op met ondersteuning](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).
>
>

## <a name="overview"></a>Overzicht

Hallo VPN-gatewayverbinding omvat Hallo volgende onderdelen:

- On-premises VPN-apparaat (een lijst weergeven met [gevalideerde VPN-apparaten)](vpn-gateway-about-vpn-devices.md#devicetable).
- Openbare Internet
- Azure VPN-gateway
- virtuele Azure-machine

Hallo volgende diagram toont Hallo logische verbinding van een lokaal netwerk tooan virtuele Azure-netwerk via VPN-verbinding.

![Logische connectiviteit van het netwerk klant tooMSFT netwerk via een VPN](./media/vpn-gateway-validate-throughput-to-vnet/VPNPerf.png)

## <a name="calculate-hello-maximum-expected-ingressegress"></a>Hallo maximale verwachte inkomend en uitgaand berekenen

1.  Bepaal de basisvereisten voor doorvoer van uw toepassing.
2.  Bepaal de doorvoerlimieten van uw Azure VPN-gateway. Zie voor meer informatie Hallo 'geaggregeerde doorvoer per SKU en VPN-type'-sectie van [Planning en ontwerp voor VPN-Gateway](vpn-gateway-plan-design.md).
3.  Hallo bepalen [Azure VM doorvoer richtlijnen](../virtual-machines/virtual-machines-windows-sizes.md) voor uw VM-grootte.
4.  Bepaal uw bandbreedte Internetproviderverbindingen (ISP).
5.  Berekenen van de verwachte doorvoer - minimale bandbreedte van (ISP VM,-Gateway) * 0,8.

Als uw berekende doorvoer voldoet niet aan de basisvereisten doorvoer van uw toepassing, moet u tooincrease Hallo bandbreedte van Hallo resource die u hebt geïdentificeerd als Hallo knelpunt. Zie voor een Azure VPN-Gateway tooresize [wijzigen van een gateway-SKU](https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-about-vpn-gateway-settings.md#gwsku). Zie voor een virtuele machine, tooresize [vergroten of verkleinen van een virtuele machine](../virtual-machines/virtual-machines-windows-resize-vm.md). Als u niet de verwachte internetbandbreedte ondervindt nog, kunt u ook toocontact uw Internetprovider.

## <a name="validate-network-throughput-by-using-performance-tools"></a>Netwerkdoorvoer valideren met behulp van hulpprogramma's voor prestaties

Deze validatie moet worden uitgevoerd tijdens daluren, zoals VPN-tunnel doorvoer verzadiging tijdens het testen geen nauwkeurige resultaten geeft.

Hallo-hulpprogramma we voor deze test gebruiken is iPerf die werkt op Windows- en Linux- en heeft zowel client als server modi. Beperkte too3 Gbps voor VM's van Windows is.

Dit hulpprogramma voert bewerkingen lezen/schrijven toodisk. Zelfgegenereerd TCP-verkeer van één end toohello andere produceert uitsluitend. Deze statistieken op basis van experimenten die Hallo bandbreedte tussen client en server knooppunten beschikbaar meet zijn gegenereerd. Bij het testen van tussen twee knooppunten, fungeert een als Hallo-server en Hallo andere als een client. Als deze test is voltooid, wordt u aangeraden dat u Hallo rollen tootest beide uploaden en downloaden van doorvoer op beide knooppunten ongedaan maken.

### <a name="download-iperf"></a>IPerf downloaden
Download [iPerf](https://iperf.fr/download/iperf_3.1/iperf-3.1.2-win64.zip). Zie voor meer informatie [iPerf documentatie](https://iperf.fr/iperf-doc.php).

 >[!NOTE]
 >Hallo van derden producten die in dit artikel wordt beschreven, zijn geproduceerd door bedrijven die onafhankelijk van Microsoft zijn. Microsoft geeft geen garantie, impliciet of anderszins over Hallo prestaties of de betrouwbaarheid van deze producten.
 >
 >

### <a name="run-iperf-iperf3exe"></a>Voer iPerf (iperf3.exe)
1. Een NSG/ACL-regel Hallo-verkeer (voor openbare IP-adres testen op Azure VM) inschakelen.

2. Schakel een firewall-uitzondering voor poort 5001 op beide knooppunten.

    **Windows:** uitvoeren Hallo volgende opdracht uit als beheerder:

    ```CMD
    netsh advfirewall firewall add rule name="Open Port 5001" dir=in action=allow protocol=TCP localport=5001
    ```

    tooremove hello regel bij het testen is voltooid, voert u deze opdracht:

    ```CMD
    netsh advfirewall firewall delete rule name="Open Port 5001" protocol=TCP localport=5001
    ```
    </br>
    **Azure Linux:** Azure Linux afbeeldingen hebt strikte firewalls. Als er een toepassing naar een poort luistert, wordt door Hallo verkeer toegestaan. Aangepaste installatiekopieën die zijn beveiligd wellicht poorten expliciet geopend. Algemene firewalls voor Linux OS-laag omvatten `iptables`, `ufw`, of `firewalld`.

3. Op de server-knooppunt Hallo wijzigen toohello directory waar iperf3.exe is uitgepakt. Vervolgens iPerf in de servermodus en stel deze toolisten op poort 5001 als Hallo volgende opdrachten:

     ```CMD
     cd c:\iperf-3.1.2-win65

     iperf3.exe -s -p 5001
     ```

4. Op de client-knooppunt Hallo wijzigen toohello directory waarbij iperf hulpprogramma uitgepakt en Voer Hallo volgende opdracht:

    ```CMD
    iperf3.exe -c <IP of hello iperf Server> -t 30 -p 5001 -P 32
    ```

    Hallo-client wordt verkeer op poort 5001 toohello server veroorzaken gedurende 30 seconden. vlag Hallo '-P ' die aangeeft dat we 32 knooppunten van gelijktijdige verbindingen toohello server gebruiken.

    Hallo ziet volgende scherm Hallo-uitvoer van dit voorbeeld:

    ![Uitvoer](./media/vpn-gateway-validate-throughput-to-vnet/06theoutput.png)

5. (Optioneel) toopreserve Hallo testresultaten deze opdracht uitvoeren:

    ```CMD
    iperf3.exe -c IPofTheServerToReach -t 30 -p 5001 -P 32  >> output.txt
    ```

6. Uitvoeren na het voltooien van de vorige stappen Hallo Hallo dezelfde stappen Hallo-functies is teruggedraaid, zodat hello serverknooppunt nu Hallo-client en vice versa worden kan.

## <a name="address-slow-file-copy-issues"></a>Problemen met adres trage bestanden kopiëren
Er kunnen optreden langzaam bestand kopiëren wanneer u Windows Verkenner of slepen en neerzetten via een RDP-sessie. Dit probleem is normaal gesproken vervaldatum tooone of beide Hallo volgende factoren:

- Bestand kopiëren toepassingen, zoals Windows Verkenner en RDP, meerdere threads niet gebruiken tijdens het kopiëren van bestanden. Gebruik voor betere prestaties een kopie-toepassing met meerdere threads bestand, zoals [Richcopy](https://technet.microsoft.com/en-us/magazine/2009.04.utilityspotlight.aspx) toocopy bestanden met behulp van 16 of 32 threads. toochange hello thread nummer voor het kopiëren van bestanden in Richcopy, klikt u op **actie** > **opties kopiëren** > **bestanden zijn gekopieerd**.<br><br>
![Problemen met trage bestanden kopiëren](./media/vpn-gateway-validate-throughput-to-vnet/Richcopy.png)<br>
- Onvoldoende VM schijf lezen/schrijven-snelheid. Zie voor meer informatie [Azure Storage probleemoplossing](../storage/common/storage-e2e-troubleshooting.md).

## <a name="on-premises-device-external-facing-interface"></a>Lokale apparaat extern gerichte interface
Als Hallo lokale VPN-apparaat internetgerichte IP-adres is opgenomen in Hallo [lokale netwerk](vpn-gateway-howto-site-to-site-resource-manager-portal.md#LocalNetworkGateway) definitie in Azure, treden onvermogen toobring Hallo VPN, sporadisch verbinding wordt verbroken of prestatieproblemen.

## <a name="checking-latency"></a>Latentie controleren
Tracert tootrace tooMicrosoft Azure rand apparaat toodetermine gebruiken als er meer dan 100 milliseconden tussen hops vertragingen.

Voer vanuit Hallo on-premises netwerk, *tracert* toohello VIP van hello Azure Gateway of VM. Eenmaal u alleen ziet * geretourneerd, u weet hello Azure rand is bereikt. Als u DNS-namen met 'MSN' geretourneerd ziet, weet u dat Hallo Microsoft backbone is bereikt.<br><br>
![Latentie controleren](./media/vpn-gateway-validate-throughput-to-vnet/08checkinglatency.png)

## <a name="next-steps"></a>Volgende stappen
Bekijk voor meer informatie en hulp Hallo koppelingen te volgen:

- [Netwerkdoorvoer voor Azure virtual machines optimaliseren](../virtual-network/virtual-network-optimize-network-bandwidth.md)
- [Microsoft-ondersteuning](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade)

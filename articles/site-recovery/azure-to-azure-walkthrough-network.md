---
title: toegang voor VMware tooAzure replicatie met Site Recovery aaaPlan | Microsoft Docs
description: Dit artikel wordt beschreven netwerkplanning vereist bij het repliceren van virtuele machines van Azure met Azure Site Recovery
services: site-recovery
documentationcenter: 
author: sujayt
manager: rochakm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 08/01/2017
ms.author: sujayt
ms.openlocfilehash: e4036351ca707bd4966cf2a855d4a162f88153e8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="step-3-plan-networking-for-azure-vm-replication"></a>Stap 3: De netwerken voor virtuele machine van Azure replicatie plannen

Nadat u hebt gecontroleerd Hallo [implementatievereisten](azure-to-azure-walkthrough-prerequisites.md), Lees dit artikel toounderstand Hallo networking overwegingen bij het repliceren en herstellen van de virtuele Azure-machines (VM's) van een Azure-regio tooanother, met behulp van Hallo Azure Site Recovery-service. 

- Wanneer u klaar bent met Hallo artikel, moet u een duidelijk inzicht in hoe tooset up uitgaande toegang tot voor Azure Virtual machines u wilt dat tooreplicate en hoe tooconnect van uw on-premises site toothose virtuele machines.
- Eventuele opmerkingen onder Hallo van dit artikel plaatsen of vragen in Hallo [Azure Recovery Services-Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

>[!NOTE]
> Azure VM-replicatie met Site Recovery is momenteel in preview.



## <a name="network-overview"></a>Overzicht van het netwerk

Doorgaans uw Azure VM's bevinden zich in een Azure virtuele netwerk-en subnet en er is een verbinding tussen uw lokale site tooAzure met Azure ExpressRoute of een VPN-verbinding.

Netwerken zijn meestal beveiligd met behulp van firewalls en/of netwerkbeveiligingsgroepen (nsg's). Firewalls kunnen gebruiken op basis van een URL op IP gebaseerd lijsten, toocontrol netwerkverbinding. Nsg's IP-adresbereik gebaseerde regels gebruiken. 


Site Recovery toowork verwacht, moet u toomake enkele wijzigingen in de uitgaande netwerkconnectiviteit van VM's die u tooreplicate wilt. Site Recovery biedt geen ondersteuning voor gebruik van een proxy voor verificatie toocontrol netwerkverbinding. Als er een verificatieproxy, kan niet replicatie worden ingeschakeld. 


Hallo ziet volgende diagram u een typische omgeving voor een toepassing die wordt uitgevoerd op Azure Virtual machines.

![klant-omgeving](./media/azure-to-azure-walkthrough-network/source-environment.png)

**Azure VM-omgeving**

Mogelijk hebt u ook een verbinding tooAzure instellen van uw on-premises site, met behulp van Azure ExpressRoute of een VPN-verbinding. 

![klant-omgeving](./media/azure-to-azure-walkthrough-network/source-environment-expressroute.png)

**Lokale verbinding tooAzure**



## <a name="outbound-connectivity-for-urls"></a>Uitgaande verbinding voor URL 's

Als u een URL-gebaseerde firewall proxy toocontrol uitgaande verbinding gebruikt, controleert u of dat u deze URL's die worden gebruikt door Site Recovery toestaan

**URL** | **Details**  
--- | ---
*.blob.core.windows.net | Hiermee kunt gegevens toobe geschreven van Hallo VM, toohello cache storage-account in Hallo bron regio.
Login.microsoftonline.com | Autorisatie en verificatie tooSite bevat Recovery service-URL's.
*.hypervrecoverymanager.windowsazure.com | Kan de communicatie met de Hallo Hallo VM Site Recovery-service.
*. servicebus.windows.net | Vereist zodat Hallo Site Recovery controle en diagnostische gegevens van Hallo VM kan worden geschreven.

## <a name="outbound-connectivity-for-ip-address-ranges"></a>Uitgaande verbinding voor IP-adresbereiken

- U kunt automatisch Hallo vereist regels maken op Hallo NSG door downloaden en uitvoeren van [dit script](https://gallery.technet.microsoft.com/Azure-Recovery-script-to-0c950702).
- U wordt aangeraden Hallo vereist NSG-regels maken op een test NSG en controleren of er geen problemen zijn voordat u Hallo regels voor een productie-NSG maken.
- toocreate hello vereist aantal NSG-regels, zorg ervoor dat uw abonnement wilt plaatsen. Neem contact op met ondersteuning tooincrease hello NSG Regellimiet in uw abonnement.
Als u van een IP-gebaseerde firewallproxy of het NSG-regels toocontrol uitgaande verbinding gebruikmaakt, moeten hello volgende IP-adresbereiken toobe goedgekeurde lijst, afhankelijk van de bron- en doellocaties Hallo Hallo virtuele machines:

    - Alle IP-adresbereiken die overeenkomen met de bronlocatie toohello. Download Hallo [bereiken](https://www.microsoft.com/download/confirmation.aspx?id=41653).) Whitelisting is vereist, zodat gegevens kunnen toohello cache storage-account worden geschreven van Hallo VM.
    - Alle IP-adresbereiken die overeenkomen met tooOffice 365 [authenticatie en identiteit IP V4-eindpunten](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2#bkmk_identity). Als het nieuwe IP-adressen zijn tooOffice 365 IP-adresbereiken toegevoegd, moet u toocreate nieuwe NSG-regels.
-     Site Recovery-service-eindpunt IP-adressen ([beschikbaar zijn in een XML-bestand](https://aka.ms/site-recovery-public-ips)), die afhankelijk zijn van de doellocatie van uw: 

   **TARGET-locatie** | **Site Recovery-service IP-adressen** |  **Site Recovery IP bewaken**
   --- | --- | ---
   Oost-Azië | 52.175.17.132</br>40.83.121.61 | 13.94.47.61
   Zuidoost-Azië | 52.187.58.193</br>52.187.169.104 | 13.76.179.223
   Centraal-India | 52.172.187.37</br>52.172.157.193 | 104.211.98.185
   Zuid-India | 52.172.46.220</br>52.172.13.124 | 104.211.224.190
   Noord-centraal VS | 23.96.195.247</br>23.96.217.22 | 168.62.249.226
   Noord-Europa | 40.69.212.238</br>13.74.36.46 | 52.169.18.8
   West-Europa | 52.166.13.64</br>52.166.6.245 | 40.68.93.145
   VS - oost | 13.82.88.226</br>40.71.38.173 | 104.45.147.24
   VS - west | 40.83.179.48</br>13.91.45.163 | 104.40.26.199
   Zuid-centraal VS | 13.84.148.14</br>13.84.172.239 | 104.210.146.250
   VS - midden | 40.69.144.231</br>40.69.167.116 | 52.165.34.144
   VS - oost 2 | 52.184.158.163</br>52.225.216.31 | 40.79.44.59
   Japan - oost | 52.185.150.140</br>13.78.87.185 | 138.91.1.105
   Japan - west | 52.175.146.69</br>52.175.145.200 | 138.91.17.38
   Brazilië - zuid | 191.234.185.172</br>104.41.62.15 | 23.97.97.36
   Australië - oost | 104.210.113.114</br>40.126.226.199 | 191.239.64.144
   Australië - zuidoost | 13.70.159.158</br>13.73.114.68 | 191.239.160.45
   Canada - midden | 52.228.36.192</br>52.228.39.52 | 40.85.226.62
   Canada - oost | 52.229.125.98</br>52.229.126.170 | 40.86.225.142
   West-centraal VS | 52.161.20.168</br>13.78.230.131 | 13.78.149.209
   VS - west 2 | 52.183.45.166</br>52.175.207.234 | 13.66.228.204
   Verenigd Koninkrijk West | 51.141.3.203</br>51.140.226.176 | 51.141.14.113
   Verenigd Koninkrijk Zuid | 51.140.43.158</br>51.140.29.146 | 51.140.189.52

## <a name="example-nsg-configuration"></a>Voorbeeldconfiguratie voor NSG

Deze sectie wordt beschreven hoe tooconfigure NSG regels, zodat replicaties is geschikt voor een virtuele machine. Als u uitgaande connectiviteit voor toocontrol NSG-regels gebruikt, kunt u de 'HTTPS uitgaande toestaan' regels gebruiken voor alle IP-adresbereiken van Hallo vereist.

In dit voorbeeld is Hallo VM bronlocatie 'VS-Oost'. Hallo replicatie target-locatie is VS-midden.


### <a name="example"></a>Voorbeeld

#### <a name="east-us"></a>VS - oost

1. Regels die overeenkomen met te maken[Oost, VS IP-bereiken](https://www.microsoft.com/download/confirmation.aspx?id=41653). Dit is vereist zodat gegevens kunnen toohello cache storage-account worden geschreven van Hallo VM.
2. Regels maken voor alle IP-adresbereiken die overeenkomen met tooOffice 365 [authenticatie en identiteit IP V4-eindpunten](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2#bkmk_identity).
3. Regels die overeenkomen met de doellocatie toohello maken:

   **Locatie** | **Site Recovery-service IP-adressen** |  **Site Recovery IP bewaken**
    --- | --- | ---
   VS - midden | 40.69.144.231</br>40.69.167.116 | 52.165.34.144

#### <a name="central-us"></a>VS - midden

Deze regels zijn vereist, zodat de replicatie na een failover uit Hallo doel regio toohello brongebied kan worden ingeschakeld.

1. Regels die overeenkomen met te maken[centraal VS-IP-bereiken](https://www.microsoft.com/download/confirmation.aspx?id=41653).
2. Regels maken voor alle IP-adresbereiken die overeenkomen met tooOffice 365 [authenticatie en identiteit IP V4-eindpunten](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2#bkmk_identity).
3. Regels die overeenkomen met de bronlocatie toohello maken:

   **Locatie** | **Site Recovery-service IP-adressen** |  **Site Recovery IP bewaken**
    --- | --- | ---
   VS - oost | 13.82.88.226</br>40.71.38.173 | 104.45.147.24


## <a name="existing-on-premises-connection"></a>Bestaande on-premises verbinding

Als u een ExpressRoute- of VPN-verbinding tussen uw lokale site en de bronlocatie Hallo in Azure hebt, volgt u deze richtlijnen:

**Configuratie** | **Details**
--- | ---
**Geforceerde tunneling** | Doorgaans een standaardroute (0.0.0.0/0) zorgt ervoor dat uitgaand verkeer van internet-tooflow via Hallo on-premises locatie. Wordt niet aanbevolen. Replicatieverkeer en communicatie van Site Recovery moet blijven binnen Azure.<br/><br/> Toevoegen als een oplossing de gebruiker gedefinieerde routes (udr's) voor [deze IP-adresbereiken](#outbound-connectivity-for-azure-site-recovery-ip-ranges), zodat verkeer Hallo biedt geen lokale gaan.
**Connectiviteit** | Als apps tooconnect tooon-premises machines moeten of lokale clients toohello app via lokale via VPN en ExpressRoute verbinden, zorg ervoor dat u hebt ten minste een [site-naar-site-verbinding](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md), tussen Hallo doel Azure-regio en Hallo lokale site.<br/><br/> Als verkeersstromen hoge tussen Hallo doel Azure-regio en Hallo on-premises-site, maakt u een andere [ExpressRoute-verbinding](../expressroute/expressroute-introduction.md), tussen Hallo doelregio en on-premises.<br/><br/> Als u tooretain IP-adressen voor virtuele machines na een failover wilt, houd Hallo doelregio site-naar-site en ExpressRoute-verbinding verbroken. Dit zorgt ervoor dat er zijn geen bereik is strijdig tussen Hallo bron en doel-IP-adresbereiken.
**ExpressRoute** | Maak een ExpressRoute-circuit in Hallo bron en doel-regio's.<br/><br/> Maak een verbinding tussen Hallo Bronnetwerk en Hallo ExpressRoute-circuit en tussen Hallo doelnetwerk en Hallo circuit.<br/><br/> Het is raadzaam dat u verschillende IP-adresbereiken in bron en doel-regio's. Hallo circuit niet kunnen tooconnect toomore dan één Azure-met Hallo dezelfde netwerken IP-adresbereiken op Hallo hetzelfde moment.<br/><br/> U kunt virtuele netwerken maken met de Hallo dezelfde IP bereiken in beide regio's en maak vervolgens de ExpressRoute-circuits in beide regio's. Voor failover, Verbreek de verbinding tussen Hallo circuit Hallo bron virtueel netwerk en Hallo-circuit in Hallo doel virtueel netwerk verbinden.<br/><br/> Als de primaire regio Hallo volledig omlaag, Hallo verbreken bewerking mislukken. In dit geval won't Hallo doel virtueel netwerk de ExpressRoute-verbinding ophalen.
**ExpressRoute Premium** | Voor het maken van circuits in Hallo dezelfde geopolitieke regio.<br/><br/> toocreate circuits in andere geopolitieke regio's, moet u Azure ExpressRoute Premium.<br/><br/> Met Premium is het Hallo-kosten incrementele. Als u al wordt gebruikt, is er geen extra kosten.<br/><br/> Meer informatie over [locaties](../expressroute/expressroute-locations.md#azure-regions-to-expressroute-locations-within-a-geopolitical-region) en [prijzen](https://azure.microsoft.com/pricing/details/expressroute/).



## <a name="next-steps"></a>Volgende stappen

Ga te[stap 4: een kluis maken](azure-to-azure-walkthrough-vault.md)


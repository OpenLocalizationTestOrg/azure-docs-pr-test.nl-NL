---
title: Site Recovery netwerken richtlijnen voor het repliceren van virtuele machines van Azure tooAzure aaaAzure | Microsoft Docs
description: Richtlijnen voor het repliceren van virtuele machines van Azure toegang
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
ms.date: 05/13/2017
ms.author: sujayt
ms.openlocfilehash: 3a3391b8c3512932d243458fd17d2a2b39248448
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="networking-guidance-for-replicating-azure-virtual-machines"></a>Richtlijnen voor het repliceren van virtuele machines van Azure toegang

>[!NOTE]
> Site Recovery replicatie voor virtuele machines in Azure is momenteel in preview.

Dit artikel details hello richtlijnen voor Azure Site Recovery netwerken als u bent bezig met repliceren en herstellen van virtuele machines in Azure uit één regio tooanother regio. Zie voor meer informatie over de vereisten voor Azure Site Recovery Hallo [vereisten](site-recovery-prereq.md) artikel.

## <a name="site-recovery-architecture"></a>Site Recovery-architectuur

Site Recovery biedt een eenvoudige en eenvoudige manier tooreplicate toepassingen die worden uitgevoerd op virtuele machines in Azure tooanother Azure-regio zodat ze kunnen worden hersteld als er een onderbreking in de primaire regio Hallo. Meer informatie over [in dit scenario en de Site Recovery-architectuur](site-recovery-azure-to-azure-architecture.md).

## <a name="your-network-infrastructure"></a>Uw netwerkinfrastructuur

Hallo illustreert volgende diagram Hallo typische Azure-omgeving voor een toepassing die wordt uitgevoerd op virtuele machines in Azure:

![klant-omgeving](./media/site-recovery-azure-to-azure-architecture/source-environment.png)

Als u van Azure ExpressRoute of een VPN-verbinding van een lokaal netwerk tooAzure gebruikmaakt, uitziet Hallo omgeving:

![klant-omgeving](./media/site-recovery-azure-to-azure-architecture/source-environment-expressroute.png)

Normaal gesproken beveiligen klanten hun netwerken die gebruikmaken van firewalls en/of netwerkbeveiligingsgroepen (nsg's). Hallo firewalls kunnen op op basis van een URL of op basis van IP-whitelisting gebruiken voor het beheren van netwerkverbindingen. Nsg's kunnen regels voor het gebruik van IP-adresbereiken toocontrol netwerkverbinding.

>[!IMPORTANT]
> Als u van een geverifieerde proxyserver toocontrol verbinding met het netwerk gebruikmaakt, wordt niet ondersteund en replicatie van Site Recovery kan niet worden ingeschakeld. 

Hallo volgende secties worden besproken Hallo uitgaande Verbindingswijzigingen in het netwerk die van Azure virtuele machines voor de Site Recovery replicatie toowork vereist zijn.

## <a name="outbound-connectivity-for-azure-site-recovery-urls"></a>Uitgaande verbinding voor Azure Site Recovery-URL

Als u een URL-gebaseerde firewall proxy toocontrol uitgaande verbinding gebruikt, moet u ervoor toowhitelist deze vereist Azure Site Recovery-service-URL's:


**URL** | **Doel**  
--- | ---
*.blob.core.windows.net | Vereist dat gegevens kunnen worden geschreven toohello cache storage-account in Hallo bron regio van Hallo VM.
Login.microsoftonline.com | Vereist voor autorisatie en verificatie toohello Site Recovery-service-URL's.
*.hypervrecoverymanager.windowsazure.com | Vereist zodat Hallo Site Recovery servicecommunicatie zich van Hallo VM voordoen kan.
*. servicebus.windows.net | Vereist zodat Hallo Site Recovery controle en diagnostische gegevens van Hallo VM kan worden geschreven.

## <a name="outbound-connectivity-for-azure-site-recovery-ip-ranges"></a>Uitgaande verbinding voor Azure Site Recovery IP-adresbereiken

>[!NOTE]
> tooautomatically hello vereist NSG-regels op Hallo netwerkbeveiligingsgroep maken, kunt u [downloaden en gebruiken van dit script](https://gallery.technet.microsoft.com/Azure-Recovery-script-to-0c950702).

>[!IMPORTANT]
> * U wordt aangeraden dat u Hallo vereist NSG-regels op een netwerkbeveiligingsgroep voor het testen maken en controleren of er geen problemen zijn voordat u Hallo regels op een netwerkbeveiligingsgroep voor productie maken.
> * toocreate hello vereist aantal NSG-regels, zorg ervoor dat uw abonnement wilt plaatsen. Neem contact op met ondersteuning tooincrease hello NSG Regellimiet in uw abonnement.

Als u van een IP-gebaseerde firewallproxy of het NSG-regels toocontrol uitgaande verbinding gebruikmaakt, moeten hello volgende IP-adresbereiken toobe goedgekeurde lijst, afhankelijk van de bron- en doellocaties Hallo Hallo virtuele machines:

- Alle IP-adresbereiken die overeenkomen met de bronlocatie toohello. (U kunt downloaden Hallo [IP-adresbereiken](https://www.microsoft.com/download/confirmation.aspx?id=41653).) Whitelisting is vereist, zodat gegevens kunnen toohello cache storage-account worden geschreven van Hallo VM.

- Alle IP-adresbereiken die overeenkomen met tooOffice 365 [authenticatie en identiteit IP V4-eindpunten](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2#bkmk_identity).

    >[!NOTE]
    > Als het nieuwe IP-adressen ophalen tooOffice 365 IP-adresbereiken in toekomstige Hallo hebt toegevoegd, moet u toocreate nieuwe NSG-regels.
    
- Site Recovery service-eindpunt IP-adressen ([beschikbaar zijn in een XML-bestand](https://aka.ms/site-recovery-public-ips)), die afhankelijk zijn van de doellocatie van uw: 

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

## <a name="sample-nsg-configuration"></a>Voorbeeldconfiguratie voor NSG
Deze sectie wordt uitgelegd Hallo stappen tooconfigure NSG-regels, zodat replicatie van Site Recovery op een virtuele machine werken kunt. Als u uitgaande connectiviteit voor toocontrol NSG-regels gebruikt, kunt u de 'HTTPS uitgaande toestaan' regels gebruiken voor alle IP-adresbereiken van Hallo vereist.

>[!Note]
> tooautomatically hello vereist NSG-regels op Hallo netwerkbeveiligingsgroep maken, kunt u [downloaden en gebruiken van dit script](https://gallery.technet.microsoft.com/Azure-Recovery-script-to-0c950702).

Bijvoorbeeld, als de bronlocatie van de VM is 'VS-Oost' en de doellocatie van de replicatie is 'Centraal, VS', stappen Hallo in de volgende twee secties Hallo.

>[!IMPORTANT]
> * U wordt aangeraden dat u Hallo vereist NSG-regels op een netwerkbeveiligingsgroep voor het testen maken en controleren of er geen problemen zijn voordat u Hallo regels op een netwerkbeveiligingsgroep voor productie maken.
> * toocreate hello vereist aantal NSG-regels, zorg ervoor dat uw abonnement wilt plaatsen. Neem contact op met ondersteuning tooincrease hello NSG Regellimiet in uw abonnement. 

### <a name="nsg-rules-on-hello-east-us-network-security-group"></a>NSG-regels op Hallo VS-Oost netwerkbeveiligingsgroep

* Regels die overeenkomen met te maken[Oost, VS IP-bereiken](https://www.microsoft.com/download/confirmation.aspx?id=41653). Dit is vereist zodat gegevens kunnen toohello cache storage-account worden geschreven van Hallo VM.

* Regels maken voor alle IP-adresbereiken die overeenkomen met tooOffice 365 [authenticatie en identiteit IP V4-eindpunten](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2#bkmk_identity).

* Regels die overeenkomen met de doellocatie toohello maken:

   **Locatie** | **Site Recovery-service IP-adressen** |  **Site Recovery IP bewaken**
    --- | --- | ---
   VS - midden | 40.69.144.231</br>40.69.167.116 | 52.165.34.144

### <a name="nsg-rules-on-hello-central-us-network-security-group"></a>NSG-regels op Hallo VS-midden netwerkbeveiligingsgroep

Deze regels zijn vereist, zodat de replicatie van Hallo doel regio toohello bron regio na een failover kan worden ingeschakeld:

* Regels die overeenkomen met te[centraal VS-IP-bereiken](https://www.microsoft.com/download/confirmation.aspx?id=41653). Dit zijn vereist, zodat gegevens kunnen toohello cache storage-account worden geschreven van Hallo VM.

* Regels voor alle IP-adresbereiken die overeenkomen met tooOffice 365 [authenticatie en identiteit IP V4-eindpunten](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2#bkmk_identity).

* Regels die overeenkomen met de bronlocatie toohello:

   **Locatie** | **Site Recovery-service IP-adressen** |  **Site Recovery IP bewaken**
    --- | --- | ---
   VS - oost | 13.82.88.226</br>40.71.38.173 | 104.45.147.24


## <a name="guidelines-for-existing-azure-to-on-premises-expressroutevpn-configuration"></a>Richtlijnen voor het bestaande Azure-naar-on-premises ExpressRoute/VPN-configuratie

Als er een ExpressRoute- of VPN-verbinding tussen on-premises en Hallo bronlocatie in Azure, voert u de richtlijnen in deze sectie Hallo.

### <a name="forced-tunneling-configuration"></a>Geforceerde tunneling configureren

Een algemene configuratie van de klant is toodefine een standaardroute (0.0.0.0/0) dat ervoor zorgt uitgaand verkeer van Internet-tooflow via Hallo on-premises locatie dat. We raden niet dit. Hallo-replicatieverkeer en communicatie van Site Recovery-service laat niet hello Azure grens. Hallo-oplossing is tooadd gebruiker gedefinieerde routes (udr's) voor [deze IP-adresbereiken](#outbound-connectivity-for-azure-site-recovery-ip-ranges) zodat Hallo replicatieverkeer geen lokale gaan.

### <a name="connectivity-between-hello-target-and-on-premises-location"></a>Connectiviteit tussen de doel- en on-premises locatie Hallo

Volg deze richtlijnen voor verbindingen tussen de doellocatie Hallo en Hallo on-premises locatie:
- Als uw toepassing tooconnect toohello lokale computers moet of als er clients die verbinding toohello toepassing van on-premises via VPN en ExpressRoute maken, zorg ervoor dat er ten minste een [site-naar-site-verbinding](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md) tussen uw doel-Azure-regio en Hallo on-premises datacenter.

- Als u verwacht veel verkeer tooflow tussen uw doel-Azure-regio en Hallo on-premises datacentrum dat, moet u een andere maken [ExpressRoute-verbinding](../expressroute/expressroute-introduction.md) tussen Hallo doel-Azure-regio en Hallo on-premises datacenter.

- Als u tooretain IP-adressen voor virtuele machines die Hallo wilt nadat ze een failover, houd Hallo doelregio site-naar-site en ExpressRoute-verbinding verbroken. Dit is toomake ervoor dat er geen bereik-conflict tussen Hallo bron regio IP-adresbereiken en van de doelregio-IP-adresbereiken.

### <a name="best-practices-for-expressroute-configuration"></a>Aanbevolen procedures voor het ExpressRoute-configuratie
Volg deze aanbevolen procedures voor de ExpressRoute-configuratie:

- U moet toocreate een ExpressRoute-circuit in beide Hallo bron en doel regio's. U moet vervolgens een verbinding tussen toocreate:
  - Hallo bron virtuele netwerk en Hallo ExpressRoute-circuit.
  - Hallo doel virtuele netwerk en Hallo ExpressRoute-circuit.

- U kunt als onderdeel van de standaard ExpressRoute circuits maken in Hallo dezelfde geopolitieke regio. ExpressRoute-circuits toocreate in andere geopolitieke regio's, Azure ExpressRoute Premium is vereist, die betrekking heeft op een incrementele kosten. (Als u al van ExpressRoute Premium gebruikmaakt, er is geen extra kosten verbonden.) Zie voor meer informatie, Hallo [ExpressRoute-locaties document](../expressroute/expressroute-locations.md#azure-regions-to-expressroute-locations-within-a-geopolitical-region) en [ExpressRoute prijzen](https://azure.microsoft.com/pricing/details/expressroute/).

- Het is raadzaam dat u verschillende IP-adresbereiken in bron en doel-regio's. Hallo ExpressRoute-circuit niet mogelijk tooconnect met twee virtuele netwerken van Azure Hallo hetzelfde IP-adresbereiken op Hallo hetzelfde moment.

- U kunt virtuele netwerken maken met de Hallo dezelfde IP-bereiken in beide regio's en maak ExpressRoute-circuits in beide regio's. In geval van een failover-gebeurtenis Hallo Verbreek de verbinding tussen Hallo circuit Hallo bron virtueel netwerk en Hallo-circuit in Hallo doel virtueel netwerk verbinden.

 >[!IMPORTANT]
 > Als de primaire regio Hallo volledig omlaag, Hallo verbreken van de verbinding kan mislukken. Die wordt voorkomen dat virtuele doelnetwerk Hallo ExpressRoute-verbinding ophalen.

## <a name="next-steps"></a>Volgende stappen
Beginnen met het beveiligen van uw werkbelastingen door [virtuele Azure-machines repliceren](site-recovery-azure-to-azure.md).

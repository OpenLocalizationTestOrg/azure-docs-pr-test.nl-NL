---
title: maken van RemoteApp hybride verzamelingen aaaTroubleshoot | Microsoft Docs
description: Meer informatie over hoe tootroubleshoot RemoteApp hybride verzameling maken van fouten
services: remoteapp
documentationcenter: 
author: vkbucha
manager: mbaldwin
ms.assetid: b32033ee-8d52-4e74-bb78-86ca873c34e2
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: cc426f24bd0c349a8862d54acbafa9cf84446f4a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-creating-azure-remoteapp-hybrid-collections"></a>Problemen met het maken van hybride Azure RemoteApp-verzamelingen oplossen
> [!IMPORTANT]
> Azure RemoteApp wordt op 31 augustus 2017 buiten gebruik gesteld. Lees Hallo [aankondiging](https://go.microsoft.com/fwlink/?linkid=821148) voor meer informatie.
> 
> 

Een hybride verzameling wordt gehost in en slaat gegevens op in hello Azure-cloud, maar ook kiest, kunnen gebruikers toegang tot gegevens en resources die zijn opgeslagen op uw lokale netwerk. Gebruikers hebben toegang tot apps door zich aan te melden met hun bedrijfsreferenties die zijn gesynchroniseerd of verenigd met Azure Active Directory. U kunt een hybride verzameling die gebruikmaakt van een bestaand virtueel netwerk in Azure implementeren of u kunt een nieuw virtueel netwerk maken. U wordt aangeraden dat u maakt of gebruik een virtueel netwerksubnet met een CIDR-bereik groot genoeg zijn voor toekomstige groei van de verwachte voor Azure RemoteApp.

Uw verzameling nog niet hebt worden gemaakt? Zie [een hybride verzameling maken](remoteapp-create-hybrid-deployment.md) voor Hallo stappen.

Als u problemen ondervindt bij het maken van de verzameling, of als Hallo verzameling niet werkt, u denkt dat het Hallo-manier moet, Raadpleeg Hallo informatie te volgen.

## <a name="your-image-is-invalid"></a>Uw installatiekopie is ongeldig
Als u een bericht zoals 'GoldImageInvalid' ziet wanneer u Azure tooprovision uw verzameling wacht, betekent dit dat de installatiekopie van uw sjabloon Hallo voldoet niet aan [installatiekopie vereisten gedefinieerd](remoteapp-imagereqs.md). Ja, Ga lezen die [vereisten](remoteapp-imagereqs.md). Corrigeer de afbeelding, en probeer toocreate uw verzameling opnieuw.

## <a name="does-your-vnet-have-network-security-groups-defined"></a>Heeft uw VNET netwerkbeveiligingsgroepen die zijn gedefinieerd
Als u netwerkbeveiligingsgroepen die zijn gedefinieerd op Hallo subnet die u voor uw verzameling gebruikt hebt, controleert u of deze [URL's en poorten](remoteapp-ports.md) toegankelijk vanuit het subnet zijn.

U kunt extra netwerk beveiliging groepen toohello VM's geïmplementeerd door u op Hallo-subnet voor meer controle toevoegen.

## <a name="are-you-using-your-own-dns-servers-and-are-they-accessible-from-your-vnet-subnet"></a>Gebruikt u uw eigen DNS-servers? En zijn ze toegankelijk is vanaf uw VNET subnet?
> [!NOTE]
> U hebt ervoor toomake-Hallo DNS-servers in uw VNET altijd actief zijn en altijd kunnen tooresolve Hallo virtuele machines die worden gehost in Hallo VNET. Gebruik geen Google DNS voor deze.
> 
> 

Voor hybride verzamelingen gebruikt u uw eigen DNS-servers. U ze in uw network-configuratieschema of via de beheerportal Hallo bij het maken van het virtuele netwerk. DNS-servers worden gebruikt in Hallo volgorde waarin ze worden opgegeven in een failover-manier (als tegengestelde tooround robin).  
Raadpleeg het te[naamomzetting voor VM's en Rolexemplaren](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md) toomake ervoor dat uw DNS-servers zijn geconfigureerd correcly.

Zorg ervoor dat Hallo DNS-servers voor uw verzameling zijn toegankelijk en beschikbaar vanuit Hallo VNET subnet dat u hebt opgegeven voor deze verzameling.

Bijvoorbeeld:

    <VirtualNetworkConfiguration>
    <Dns>
      <DnsServers>
        <DnsServer name="" IPAddress=""/>
      </DnsServers>
    </Dns>
    </VirtualNetworkConfiguration>

![Uw DNS definiëren](./media/remoteapp-hybridtrouble/dnsvpn.png)

## <a name="are-you-using-an-active-directory-domain-controller-in-your-collection"></a>Gebruikt u een Active Directory-domeincontroller in uw verzameling?
Op dit moment slechts één Active Directory-domein gekoppeld aan Azure RemoteApp zijn. Hallo hybride verzameling ondersteunt alleen Azure Active Directory-accounts die zijn gesynchroniseerd met DirSync-hulpprogramma op een Windows Server Active Directory-implementatie; in het bijzonder hetzij gesynchroniseerd met de optie Wachtwoordsynchronisatie Hallo of gesynchroniseerd met Active Directory Federation Services (AD FS) federation geconfigureerd. U moet een aangepast domein die overeenkomt met de Hallo UPN-achtervoegsel voor domein voor uw domein lokale toocreate en Active directory-integratie instellen.

Zie [Active Directory configureren voor Azure RemoteApp](remoteapp-ad.md) voor meer informatie.

Zorg ervoor dat Hallo domein details opgegeven geldig zijn en Hallo domeincontroller bereikbaar is vanaf Hallo die VM in Hallo subnet dat wordt gebruikt voor Azure RemoteApp gemaakt. Controleer ook of Hallo service-account opgegeven referenties hebben machtigingen tooadd computers toohello opgegeven domein en dat de naam van de AD Hallo opgegeven kan worden opgelost van Hallo DNS in het Hallo VNET.

## <a name="what-domain-name-did-you-specify-when-you-created-your-collection"></a>Welke domeinnaam hebt u opgegeven tijdens het maken van uw verzameling?
Hallo domeinnaam u hebt gemaakt of toegevoegd moet een interne domeinnaam (niet uw Azure AD domain name) en moet worden omgezet DNS-indeling (contoso.local). Bijvoorbeeld: u hebt een interne Active Directory-naam (contoso.local) en een Active Directory-UPN (contoso.com) - u hebt toouse Hallo interne naam bij het maken van uw verzameling.


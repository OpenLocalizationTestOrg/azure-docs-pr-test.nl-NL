---
title: Maken van RemoteApp hybride verzamelingen oplossen | Microsoft Docs
description: Meer informatie over het oplossen van fouten bij RemoteApp hybride verzameling maken
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
ms.openlocfilehash: a486dcb3f994cd78311ee86521a6792a4d57438e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-creating-azure-remoteapp-hybrid-collections"></a>Problemen met het maken van hybride Azure RemoteApp-verzamelingen oplossen
> [!IMPORTANT]
> Azure RemoteApp wordt op 31 augustus 2017 buiten gebruik gesteld. Lees de [aankondiging](https://go.microsoft.com/fwlink/?linkid=821148) voor meer informatie.
> 
> 

Een hybride verzameling wordt gehost in en slaat gegevens op in de Azure-cloud, maar ook kiest, kunnen gebruikers toegang tot gegevens en resources die zijn opgeslagen op uw lokale netwerk. Gebruikers hebben toegang tot apps door zich aan te melden met hun bedrijfsreferenties die zijn gesynchroniseerd of verenigd met Azure Active Directory. U kunt een hybride verzameling die gebruikmaakt van een bestaand virtueel netwerk in Azure implementeren of u kunt een nieuw virtueel netwerk maken. U wordt aangeraden dat u maakt of gebruik een virtueel netwerksubnet met een CIDR-bereik groot genoeg zijn voor toekomstige groei van de verwachte voor Azure RemoteApp.

Uw verzameling nog niet hebt worden gemaakt? Zie [een hybride verzameling maken](remoteapp-create-hybrid-deployment.md) voor de stappen.

Als u problemen ondervindt bij het maken van de verzameling, of als de verzameling niet, de manier waarop werkt u denkt dat nodig is, controleert u de volgende informatie.

## <a name="your-image-is-invalid"></a>Uw installatiekopie is ongeldig
Als u een bericht zoals 'GoldImageInvalid' ziet wanneer u Azure voor het inrichten van uw verzameling wacht, betekent dit dat de installatiekopie van uw sjabloon voldoet niet aan de [installatiekopie vereisten gedefinieerd](remoteapp-imagereqs.md). Ja, Ga lezen die [vereisten](remoteapp-imagereqs.md). Corrigeer de afbeelding, en probeer uw verzameling opnieuw maken.

## <a name="does-your-vnet-have-network-security-groups-defined"></a>Heeft uw VNET netwerkbeveiligingsgroepen die zijn gedefinieerd
Als u netwerkbeveiligingsgroepen die zijn gedefinieerd op het subnet dat u voor uw verzameling gebruikt hebt, controleert u of deze [URL's en poorten](remoteapp-ports.md) toegankelijk vanuit het subnet zijn.

U kunt aanvullende netwerkbeveiligingsgroepen toevoegen aan de virtuele machines die door u geïmplementeerd in het subnet voor strikter besturingselement.

## <a name="are-you-using-your-own-dns-servers-and-are-they-accessible-from-your-vnet-subnet"></a>Gebruikt u uw eigen DNS-servers? En zijn ze toegankelijk is vanaf uw VNET subnet?
> [!NOTE]
> U moet Controleer of dat de DNS-servers in uw VNET altijd actief zijn en altijd kunnen omzetten van de virtuele machines in het VNET. Gebruik geen Google DNS voor deze.
> 
> 

Voor hybride verzamelingen gebruikt u uw eigen DNS-servers. U ze in uw network-configuratieschema of via de beheerportal bij het maken van het virtuele netwerk. DNS-servers worden gebruikt in de volgorde waarin ze worden opgegeven op een manier failover (in plaats van round-robin).  
Raadpleeg [naamomzetting voor VM's en Rolexemplaren](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md) om te controleren of uw DNS-servers geconfigureerd correcly zijn.

Controleer of de DNS-servers voor uw verzameling toegankelijk zijn en beschikbaar is via het VNET subnet dat u hebt opgegeven voor deze verzameling.

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
Op dit moment slechts één Active Directory-domein gekoppeld aan Azure RemoteApp zijn. De hybride verzameling ondersteunt alleen Azure Active Directory-accounts die zijn gesynchroniseerd met DirSync-hulpprogramma op een Windows Server Active Directory-implementatie; in het bijzonder hetzij gesynchroniseerd met de optie Wachtwoordsynchronisatie of gesynchroniseerd met Active Directory Federation Services (AD FS) federation geconfigureerd. U moet een aangepast domein die overeenkomt met het domein UPN-achtervoegsel voor uw lokale domein maken en instellen van Active directory-integratie.

Zie [Active Directory configureren voor Azure RemoteApp](remoteapp-ad.md) voor meer informatie.

Zorg ervoor dat de details van het domein opgegeven geldig zijn en de domeincontroller bereikbaar is vanaf de virtuele machine gemaakt in het subnet dat wordt gebruikt voor Azure RemoteApp. Controleer ook of de service-account opgegeven referenties gemachtigd computers toevoegen aan het opgegeven domein en dat de opgegeven AD-naam omgezet vanaf de DNS-server die is opgegeven in het VNET worden kan.

## <a name="what-domain-name-did-you-specify-when-you-created-your-collection"></a>Welke domeinnaam hebt u opgegeven tijdens het maken van uw verzameling?
De domeinnaam die u hebt gemaakt of toegevoegd, moet de naam van een interne domein (niet uw Azure AD domain name) en moet worden omgezet DNS-indeling (contoso.local). Bijvoorbeeld, hebt u een interne Active Directory-naam (contoso.local) en een Active Directory-UPN (contoso.com) - u moet de interne naam gebruiken bij het maken van uw verzameling.


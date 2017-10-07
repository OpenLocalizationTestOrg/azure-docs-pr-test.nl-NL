---
title: 'Azure AD Domain Services: Netwerken richtlijnen | Microsoft Docs'
description: Overwegingen voor Azure Active Directory Domain Services netwerken
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 23a857a5-2720-400a-ab9b-1ba61e7b145a
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: maheshu
ms.openlocfilehash: 804d4ea7d1b3b07b6d224855c7adb90bdfe24022
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="networking-considerations-for-azure-ad-domain-services"></a>Overwegingen voor Azure AD Domain Services netwerken
## <a name="how-tooselect-an-azure-virtual-network"></a>Hoe tooselect virtueel netwerk van Azure
Hallo kunnen volgende richtlijnen u een virtueel netwerk toouse met Azure AD Domain Services selecteren.

### <a name="type-of-azure-virtual-network"></a>Type virtuele Azure-netwerk
* U kunt Azure AD Domain Services in een klassiek virtueel netwerk van Azure inschakelen.
* Azure AD Domain Services **kan niet worden ingeschakeld in virtuele netwerken die zijn gemaakt met Azure Resource Manager**.
* U kunt verbinding maken met een virtueel netwerk op basis van een Resource Manager tooa klassiek virtueel netwerk waarin Azure AD Domain Services is ingeschakeld. Daarna kunt u Azure AD Domain Services in Hallo Resource Manager gebaseerde virtuele netwerk. Zie voor meer informatie, Hallo [netwerkverbinding](active-directory-ds-networking.md#network-connectivity) sectie.
* **Regionale virtuele netwerken**: als u een bestaand virtueel netwerk toouse plant, moet u zorgen dat het een regionaal virtueel netwerk.

  * Virtuele netwerken die gebruikmaken van Hallo verouderde affiniteitsgroepen mechanisme kunnen niet worden gebruikt met Azure AD Domain Services.
  * Azure AD Domain Services toouse [verouderde virtuele netwerken tooregional virtuele netwerken migreren](../virtual-network/virtual-networks-migrate-to-regional-vnet.md).

### <a name="azure-region-for-hello-virtual-network"></a>Azure-regio voor het virtuele netwerk Hallo
* Uw Azure AD Domain Services beheerd domein wordt geïmplementeerd in dezelfde Azure-regio als Hallo virtuele netwerk die u kiest tooenable Hallo-service in Hallo.
* Selecteer een virtueel netwerk in een Azure-regio wordt ondersteund door Azure AD Domain Services.
* Zie Hallo [Azure-services per regio](https://azure.microsoft.com/regions/#services/) pagina tooknow hello Azure-regio's waar Azure AD Domain Services beschikbaar is.

### <a name="requirements-for-hello-virtual-network"></a>Vereisten voor het virtuele netwerk Hallo
* **Nabijheid tooyour Azure werkbelastingen**: Selecteer Hallo virtueel netwerk dat momenteel fungeert als host/host fungeert voor virtuele machines die toegang moeten hebben tot tooAzure AD Domain Services.
* **DNS-servers aangepaste/bring your own**: Zorg ervoor dat er geen aangepaste DNS-servers geconfigureerd voor het virtuele netwerk Hallo.
* **Bestaande domeinen met dezelfde domeinnaam Hallo**: Zorg ervoor dat u geen een bestaand domein met Hallo hebt dezelfde domeinnaam beschikbaar is op dit virtuele netwerk. Bijvoorbeeld, wordt ervan uitgegaan hebben van een domein genaamd 'contoso.com' al beschikbaar op Hallo van de geselecteerde virtuele netwerk. Later kunt u een beheerd domein van Azure AD Domain Services met Hallo tooenable probeert dezelfde domeinnaam (dat wil zeggen 'contoso.com') op dit virtuele netwerk. Er optreedt een fout bij een poging tooenable Azure AD Domain Services. Deze fout is vanwege conflicten tooname voor Hallo-domeinnaam op dit virtuele netwerk. In dit geval moet u een andere naam tooset van uw Azure AD Domain Services beheerd domein. U kunt ook ongedaan inrichten Hallo bestaand domein en vervolgens doorgaan tooenable Azure AD Domain Services.

> [!WARNING]
> U kunt Domain Services tooa ander virtueel netwerk niet verplaatsen wanneer u Hallo service hebt ingeschakeld.
>
>

## <a name="network-security-groups-and-subnet-design"></a>Netwerkbeveiligingsgroepen en subnet ontwerp
Een [Netwerkbeveiligingsgroep (NSG)](../virtual-network/virtual-networks-nsg.md) bevat een lijst met regels voor lijst ACL (Access Control) toestaan of weigeren netwerkverkeer tooyour VM-exemplaren in een virtueel netwerk. NSG's kunnen worden gekoppeld aan subnetten of afzonderlijke VM-exemplaren in dat subnet. Wanneer een NSG gekoppeld aan een subnet is, toepassing hello ACL-regels tooall Hallo VM-exemplaren in dat subnet. Bovendien verkeer tooan afzonderlijke VM kan worden beperkt door een NSG koppelen verdere rechtstreeks toothat VM.

![Aanbevolen subnet ontwerp](./media/active-directory-domain-services-design-guide/vnet-subnet-design.png)

### <a name="best-practices-for-choosing-a-subnet"></a>Aanbevolen procedures voor het kiezen van een subnet
* Azure AD Domain Services tooa implementeren **scheiden toegewezen subnet** binnen uw virtuele Azure-netwerk.
* Nsg's toohello toegewezen subnet voor uw beheerde domein zijn niet van toepassing. Als u nsg's toohello toegewezen subnet toepassen moet, moet u **niet blokkeren Hallo poorten vereist tooservice en beheren van uw domein**.
* Niet overmatig beperken Hallo aantal IP-adressen beschikbaar binnen Hallo toegewezen subnet voor uw beheerde domein. Deze beperking wordt voorkomen dat Hallo service twee domeincontrollers beschikbaar maken voor uw beheerde domein.
* **Schakel geen Azure AD Domain Services in het gatewaysubnet hello** van het virtuele netwerk.

> [!WARNING]
> Als u koppelt een NSG aan een subnet waarin Azure AD Domain Services is ingeschakeld, u kunt Microsoft mogelijkheid tooservice verstoren en Hallo domein beheren. Bovendien wordt de synchronisatie tussen uw Azure AD-tenant en uw beheerde domein onderbroken. **Hallo SLA toodeployments waarbij een NSG is toegepast, die blokkeert Azure AD Domain Services uit bijwerken en het beheren van uw domein is niet van toepassing.**
>
>

### <a name="ports-required-for-azure-ad-domain-services"></a>Poorten die nodig zijn voor Azure AD Domain Services
Hallo volgende poorten zijn vereist voor Azure AD Domain Services tooservice en onderhouden van uw beheerde domein. Zorg ervoor dat deze poorten worden niet geblokkeerd voor Hallo subnet waarin u uw beheerde domein hebt ingeschakeld.

| Poortnummer | Doel |
| --- | --- |
| 443 |Synchronisatie met uw Azure AD-tenant |
| 3389 |Beheer van uw domein |
| 5986 |Beheer van uw domein |
| 636 |Beveiligde LDAP (LDAPS) toegang tooyour beheerd domein |

### <a name="sample-nsg-for-virtual-networks-with-azure-ad-domain-services"></a>Voorbeeld NSG voor virtuele netwerken met Azure AD Domain Services
Hallo volgende tabel ziet u een voorbeeld van een NSG die u voor een virtueel netwerk met een beheerd domein van Azure AD Domain Services configureren kunt. Deze regel kunnen binnenkomend verkeer van Hallo hierboven opgegeven poorten tooensure uw beheerde domein blijft een patch uitgevoerd, bijgewerkt en kunnen worden bewaakt door Microsoft. Hallo 'DenyAll' standaardregel geldt tooall andere binnenkomend verkeer van Hallo internet.

Bovendien Hallo NSG ook ziet u hoe toolock omlaag beveiligde LDAP toegang via internet Hallo. Deze regel overslaan als u beveiligde LDAP toegang tooyour beheerd domein niet hebt ingeschakeld via Hallo internet. Hallo NSG bevat een reeks regels waarmee binnenkomende LDAPS toegang via TCP-poort 636 alleen uit een opgegeven set van IP-adressen. Hallo NSG regel tooallow LDAPS toegang via Hallo internet vanaf de opgegeven IP-adressen heeft een hogere prioriteit dan Hallo DenyAll NSG-regel.

![Voorbeeld NSG toosecure LDAPS toegang via internet Hallo](./media/active-directory-domain-services-admin-guide/secure-ldap-sample-nsg.png)

**Meer informatie** - [maken van een Netwerkbeveiligingsgroep](../virtual-network/virtual-networks-create-nsg-arm-pportal.md).


## <a name="network-connectivity"></a>Netwerkverbinding
Een beheerd domein van Azure AD Domain Services kan alleen binnen een enkele klassiek virtueel netwerk in Azure worden ingeschakeld. Virtuele netwerken die zijn gemaakt met Azure Resource Manager worden niet ondersteund.

### <a name="scenarios-for-connecting-azure-networks"></a>Scenario's voor het verbinden van netwerken in Azure
Verbinding maken met virtuele netwerken van Azure toouse Hallo beheerd domein in een van de volgende implementatiescenario's Hallo:

#### <a name="use-hello-managed-domain-in-more-than-one-azure-classic-virtual-network"></a>Gebruik Hallo beheerd domein in meer dan één Azure klassiek virtueel netwerk
U kunt verbinding maken voor andere Azure klassieke virtuele netwerken toohello Azure klassiek virtueel netwerk waarin u Azure AD Domain Services hebt ingeschakeld. Deze VPN-verbinding, kunt u toouse Hallo beheerde domein met uw werkbelastingen die zijn geïmplementeerd in een andere virtuele netwerken.

![Klassieke virtuele netwerkverbindingen](./media/active-directory-domain-services-design-guide/classic-vnet-connectivity.png)

#### <a name="use-hello-managed-domain-in-a-resource-manager-based-virtual-network"></a>Hallo beheerde domein in een virtueel netwerk met Resource Manager gebaseerde gebruiken
U kunt verbinding maken met een virtueel netwerk op basis van een Resource Manager toohello Azure klassiek virtueel netwerk waarin u Azure AD Domain Services hebt ingeschakeld. Deze verbinding, kunt u toouse Hallo beheerde domein met uw werkbelastingen die zijn geïmplementeerd in Hallo Resource Manager gebaseerde virtueel netwerk.

![Resource Manager tooclassic virtuele netwerkverbindingen](./media/active-directory-domain-services-design-guide/classic-arm-vnet-connectivity.png)

### <a name="network-connection-options"></a>Opties voor een netwerkverbinding
* **VNet-naar-VNet-verbindingen met behulp van site-naar-site VPN-verbindingen**: verbinding maken met een virtueel netwerk tooanother virtueel netwerk (VNet-naar-VNet) is vergelijkbaar tooconnecting een virtueel netwerk tooan on-premises-locatie. Beide connectiviteitstypen wordt een VPN-gateway tooprovide een beveiligde tunnel met IPsec/IKE.

    ![Verbinding met het virtuele netwerk met behulp van VPN-Gateway](./media/active-directory-domain-services-design-guide/vnet-connection-vpn-gateway.jpg)

    [Meer informatie - verbinding maken met virtuele netwerken met behulp van VPN-gateway](../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md)
* **VNet-naar-VNet-verbindingen met virtuele netwerk peering**: peering virtueel netwerk is een mechanisme dat verbinding twee virtuele netwerken in Hallo maakt dezelfde regio via hello Azure-backbone-netwerk. Als peer is ingesteld, wordt Hallo twee virtuele netwerken weergegeven als een voor alle connectiviteit doeleinden. Ze worden nog steeds beheerd als afzonderlijke resources, maar virtuele machines in deze virtuele netwerken kunnen met elkaar communiceren via privé-IP-adressen.

    ![Verbinding met het virtuele netwerk met behulp van peering](./media/active-directory-domain-services-design-guide/vnet-peering.png)

    [Meer informatie - virtuele netwerk peering](../virtual-network/virtual-network-peering-overview.md)

<br>

## <a name="related-content"></a>Gerelateerde inhoud
* [Virtueel netwerk van Azure-peering](../virtual-network/virtual-network-peering-overview.md)
* [Een VNet-naar-VNet-verbinding voor het klassieke implementatiemodel Hallo configureren](../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md)
* [Beveiligingsgroepen voor Azure-netwerk](../virtual-network/virtual-networks-nsg.md)
* [Een Netwerkbeveiligingsgroep maken](../virtual-network/virtual-networks-create-nsg-arm-pportal.md)

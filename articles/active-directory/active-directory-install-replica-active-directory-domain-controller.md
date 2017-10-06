---
title: aaaInstall replica Active Directory-domeincontroller in Azure | Microsoft Docs
description: Een zelfstudie waarin wordt uitgelegd hoe tooinstall een domeincontroller in een lokale Active Directory-forest op een virtuele machine van Azure.
services: virtual-network
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 8c9ebf1b-289a-4dd6-9567-a946450005c0
ms.service: virtual-network
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/24/2017
ms.author: curtand
ms.custom: oldportal;it-pro;
ms.openlocfilehash: 74876fce2ca2a29f02c2828f9b3a21227248233a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="install-a-replica-active-directory-domain-controller-in-an-azure-virtual-network"></a>Een replica Active Directory-domeincontroller installeren in een Azure-netwerk
Dit onderwerp wordt beschreven hoe tooinstall extra domeincontrollers (ook wel bekend als replica DC's) voor de lokale Active Directory-domein op Azure virtuele machines (VM's) in een Azure-netwerk.

> [!IMPORTANT]
> Microsoft raadt aan dat u Azure AD beheren met Hallo [Azure AD-beheercentrum](https://aad.portal.azure.com) in Hallo hello Azure-portal in plaats van de klassieke Azure-portal waarnaar wordt verwezen in dit artikel.

U is mogelijk ook geïnteresseerd in de volgende Verwante onderwerpen:

* U kunt desgewenst een nieuw Active Directory-forest installeren op een virtuele Azure-netwerk. Zie voor deze stappen [een nieuw Active Directory-forest installeren op een virtuele Azure-netwerk](active-directory-new-forest-virtual-machine.md).
* Raadpleeg voor algemene richtlijnen over het installeren van Active Directory Domain Services (AD DS) op een virtuele Azure-netwerk [richtlijnen voor het implementeren van Windows Server Active Directory op Azure Virtual Machines](https://msdn.microsoft.com/library/azure/jj156090.aspx).

## <a name="scenario-diagram"></a>Scenario-diagram
In dit scenario moeten de externe gebruikers tooaccess toepassingen die worden uitgevoerd op servers die lid zijn van een domein. Hallo virtuele machines die worden uitgevoerd Hallo-toepassingsservers en Hallo replica DC's worden geïnstalleerd in een Azure-netwerk. Hallo virtueel netwerk kan worden verbonden toohello on-premises netwerk door een [site-naar-site VPN](../vpn-gateway/vpn-gateway-site-to-site-create.md) verbinding, zoals wordt weergegeven in de volgende Hallo diagram, of u kunt gebruiken [ExpressRoute](../expressroute/expressroute-locations-providers.md) voor een snellere verbinding.

Hallo-toepassingsservers en Hallo DC's worden geïmplementeerd in afzonderlijke cloudservices compute toodistribute verwerking en binnen [beschikbaarheidssets](../virtual-machines/windows/manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) voor verbeterde fouttolerantie.
Hallo-DC's repliceren met elkaar en met lokale DC's met behulp van Active Directory-replicatie. Er zijn geen hulpprogramma's voor de synchronisatie nodig.

![Diagram pf replica Active Directory-domeincontroller een Azure vnet][1]

## <a name="create-an-active-directory-site-for-hello-azure-virtual-network"></a>Een Active Directory-site voor Hallo virtuele Azure-netwerk maken
Het is een goed idee toocreate een site in Active Directory die Hallo netwerk regio bijbehorende toohello virtueel netwerk vertegenwoordigt. Die helpt het optimaliseren van verificatie, replicatie en andere bewerkingen DC-locatie. Hallo volgende stappen wordt uitgelegd hoe toocreate een site en Zie voor meer achtergrondinformatie [toevoegen van een nieuwe Site](https://technet.microsoft.com/library/cc781496.aspx).

1. Open Active Directory-Sites en Services: **Serverbeheer** > **extra** > **Active Directory-Sites en Services**.
2. Maak een site toorepresent Hallo regio waar u een Azure-netwerk gemaakt: klik op **Sites** > **actie** > **nieuwe site** > type Hallo-naam van de nieuwe site hello, zoals Azure VS-West > Selecteer een sitekoppeling > **OK**.
3. Een subnet maken en koppelen aan de nieuwe site Hallo: Dubbelklik op **Sites** > met de rechtermuisknop op **subnetten** > **nieuw subnet** > Hallo IP-adresbereik van type Hallo virtueel netwerk (zoals 10.1.0.0/16 in Hallo scenario diagram) > Selecteer Hallo nieuwe Azure site > **OK**.

## <a name="create-an-azure-virtual-network"></a>Een Azure-netwerk maken
1. In Hallo [klassieke Azure-portal](https://manage.windowsazure.com), klikt u op **nieuw** > **netwerkservices** > **virtueel netwerk**  >  **Aangepast maken** en gebruik Hallo volgende toocomplete Hallo wizard waarden.

   | Op deze wizardpagina... | Deze waarden opgeven |
   | --- | --- |
   |  **Details van virtueel netwerk** |<p>Naam: Typ een naam voor het virtuele netwerk hello, zoals WestUSVNet.</p><p>Regio: Kies Hallo dichtstbijzijnde regio.</p> |
   |  **DNS- en VPN-verbinding** |<p>DNS-Servers: Geef Hallo naam en IP-adres van een of meer lokale DNS-servers.</p><p>Connectiviteit: Selecteer **een site-naar-site-VPN configureren**.</p><p>Lokale netwerk: Geef een nieuw lokaal netwerk.</p><p>Als u ExpressRoute gebruikt in plaats van een VPN, Zie [configureren van een ExpressRoute-verbinding via een Exchange-Provider](../expressroute/expressroute-locations-providers.md).</p> |
   |  **Site-naar-site-connectiviteit** |<p>Naam: Typ een naam voor Hallo on-premises netwerk.</p><p>VPN-apparaat IP-adres: Hallo openbare IP-adres van Hallo-apparaat waarmee verbinding wordt gemaakt van het virtuele netwerk toohello opgeven. Hallo VPN-apparaat kan zich niet achter een NAT bevinden.</p><p>Adres: Geef Hallo-adresbereiken voor uw on-premises netwerk (zoals 192.168.0.0/16 in Hallo scenario diagram).</p> |
   |  **Adresruimten voor virtueel netwerk** |<p>Adresruimte: Hallo IP-adresbereik voor virtuele machines die u wilt dat toorun in Hallo virtuele Azure-netwerk (zoals 10.1.0.0/16 in Hallo scenario diagram) opgeven. Dit adresbereik overlappen niet met adresbereiken Hallo van Hallo on-premises netwerk.</p><p>Subnetten: Geef een naam en adres voor een subnet voor toepassingsservers hello (zoals front-end 10.1.1.0/24) en voor Hallo DC's (zoals back-end 10.1.2.0/24).</p><p>Klik op **gatewaysubnet toevoegen**.</p> |
2. Vervolgens configureert u Hallo virtueel netwerk gateway toocreate een veilige site-naar-site VPN-verbinding. Zie [configureren van een virtuele netwerkgateway](../vpn-gateway/vpn-gateway-configure-vpn-gateway-mp.md) voor Hallo-instructies.
3. Hallo site-naar-site VPN-verbinding maken tussen Hallo nieuw virtueel netwerk en een on-premises VPN-apparaat. Zie [configureren van een virtuele netwerkgateway](../vpn-gateway/vpn-gateway-configure-vpn-gateway-mp.md) voor Hallo-instructies.

## <a name="create-azure-vms-for-hello-dc-roles"></a>Azure VM's voor Hallo DC-rollen maken
Herhaal Hallo stappen toocreate VMs toohost Hallo DC rol naar behoefte te volgen. U moet ten minste twee virtuele DC's tooprovide fouttolerantie en redundantie implementeren. Als u hello virtuele Azure-netwerk bevat ten minste twee domeincontrollers die op dezelfde manier zijn geconfigureerd (ze zijn beide aangegeven, voer DNS-server, en geen van beide bevat FSMO-functie, enzovoort) plaatst Hallo virtuele machines die worden uitgevoerd die DC's in een beschikbaarheidsset voor verbeterde fouttolerantie.
Zie toocreate Hallo VM's met Windows PowerShell in plaats van Hallo-gebruikersinterface [toocreate gebruik Azure PowerShell en vooraf configureren van virtuele Machines op basis van Windows](../virtual-machines/windows/classic/create-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

1. In Hallo [klassieke Azure-portal](https://manage.windowsazure.com), klikt u op **nieuw** > **Compute** > **virtuele Machine**  >  **Vanuit galerie**. Gebruik hello waarden toocomplete Hallo wizard volgen. Accepteer de standaardwaarde Hallo voor een instelling tenzij een andere waarde wordt voorgesteld of vereist.

   | Op deze wizardpagina... | Deze waarden opgeven |
   | --- | --- |
   |  **Een afbeelding kiezen** |Windows Server 2012 R2 Datacenter |
   |  **Configuratie van virtuele Machine** |<p>De naam van de virtuele Machine: Typ een naam met één label (zoals AzureDC1).</p><p>Nieuwe gebruikersnaam: Typ Hallo-naam van een gebruiker. Deze gebruiker is lid van de lokale beheerdersgroep op Hallo VM Hallo. U moet deze naam toosign in toohello VM voor Hallo eerst. de ingebouwde account Hallo beheerder werkt niet.</p><p>Nieuwe wachtwoord/bevestigen: Typ een wachtwoord</p> |
   |  **Configuratie van virtuele Machine** |<p>Cloudservice: Kies <b>Maak een nieuwe cloudservice</b> voor Hallo eerste virtuele machine en selecteer die dezelfde servicenaam cloud bij het maken van meer virtuele machines die als host fungeert Hallo DC-rol.</p><p>Cloud-Service DNS-naam: Geef een globaal unieke naam</p><p>Regio/Affiniteitsgroep/virtuele netwerk: Geef Hallo virtueel netwerk op (zoals WestUSVNet).</p><p>Storage-Account: Kies <b>een automatisch gegenereerde opslagaccount gebruiken</b> voor Hallo eerste virtuele machine en selecteer hetzelfde opslagaccount naam bij het maken van meer virtuele machines die als host fungeert Hallo DC-rol.</p><p>Beschikbaarheidsset: Kies <b>maken van een beschikbaarheidsset</b>.</p><p>Beschikbaarheidsset: Typ een naam voor Hallo beschikbaarheidsset bij het maken van eerste VM Hallo en selecteer vervolgens dezelfde naam als u meer virtuele machines maakt.</p> |
   |  **Configuratie van virtuele Machine** |<p>Selecteer <b>installeren Hallo VM-Agent</b> en eventuele andere uitbreidingen die u nodig hebt.</p> |
2. Voeg een schijf tooeach VM die Hallo DC-serverfunctie wordt uitgevoerd. Hallo extra schijf is benodigde toostore Hallo AD database, logboekbestanden en SYSVOL. Geef een grootte voor het Hallo-schijf (zoals 10 GB) en laat Hallo **Host Cache voorkeur** instellen te**geen**. Zie voor stappen Hallo [hoe tooAttach een gegevensschijf tooa virtuele Windows-Machine](../virtual-machines/windows/classic/attach-disk.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).
3. Nadat u toohello VM voor het eerst aanmelden, opent u **Serverbeheer** > **File and Storage Services** toocreate een volume op deze schijf met NTFS.
4. Reserveer een statisch IP-adres voor virtuele machines die Hallo DC-rol wordt uitgevoerd. een statisch IP-adres tooreserve Hallo Microsoft Web Platform Installer downloaden en [Azure PowerShell installeren](/powershell/azure/overview) en voer de cmdlet Set-AzureStaticVNetIP Hallo uit. Bijvoorbeeld:

    ' Get-AzureVM - ServiceName AzureDC1-naam AzureDC1 | Set-AzureStaticVNetIP - IP-adres 10.0.0.4 | Update-AzureVM

Zie voor meer informatie over het instellen van een statisch IP-adres [een statische interne IP-adres configureren voor een virtuele machine](../virtual-network/virtual-networks-reserved-private-ip.md).

## <a name="install-ad-ds-on-azure-vms"></a>Installatie van AD DS op virtuele machines in Azure
Tooa VM aanmelden en controleren of u verbinding over Hallo site-naar-site VPN- of ExpressRoute-verbinding tooresources op uw on-premises netwerk hebt. AD DS installeert op Hallo virtuele Azure-machines. U kunt hetzelfde proces dat u een extra domeincontroller tooinstall op uw on-premises netwerk (gebruikersinterface, Windows PowerShell of een antwoordbestand) gebruiken. Als u AD DS installeert, zorg er dan voor dat u opgeeft Hallo nieuw volume voor de locatie van de Hallo Hallo AD-database, logboekbestanden en SYSVOL. Als u een refresher op AD DS-installatie moet, Zie [Install Active Directory Domain Services (Level 100)](https://technet.microsoft.com/library/hh472162.aspx) of [een Replica Windows Server 2012-domeincontroller installeren in een bestaand domein (niveau 200)](https://technet.microsoft.com/library/jj574134.aspx).

## <a name="reconfigure-dns-server-for-hello-virtual-network"></a>DNS-server voor het virtuele netwerk Hallo opnieuw configureren
1. In Hallo [Azure-portal](https://portal.azure.com), in Hallo **zoeken bronnen** Voer *virtuele netwerken*, klikt u vervolgens op **virtuele netwerken (klassiek)** in Hallo zoekresultaten. Klik op de naam Hallo van Hallo virtueel netwerk, en vervolgens [Hallo DNS-server IP-adressen voor het virtuele netwerk configureren](../virtual-network/virtual-network-manage-network.md#dns-servers) toouse Hallo statische IP-adressen toegewezen toohello replica DC's in plaats van Hallo IP-adressen van een lokale DNS-server -servers.
2. tooensure dat alle Hallo replica VMs DC op Hallo virtueel netwerk zijn geconfigureerd met toouse DNS-servers op Hallo virtueel netwerk, klikt u op **virtuele Machines**Hallo in de statuskolom voor elke virtuele machine op en klik vervolgens op **opnieuw starten** . Wacht totdat het Hallo VM toont **met** voordat u toosign in deze probeert status.

## <a name="create-vms-for-application-servers"></a>Virtuele machines voor toepassingsservers maken
1. Herhaal stappen toocreate VMs toorun volgen als toepassingsservers Hallo. Accepteer de standaardwaarde Hallo voor een instelling tenzij een andere waarde wordt voorgesteld of vereist.

   | Op deze wizardpagina... | Deze waarden opgeven |
   | --- | --- |
   |  **Een afbeelding kiezen** |Windows Server 2012 R2 Datacenter |
   |  **Configuratie van virtuele Machine** |<p>De naam van de virtuele Machine: Typ een naam met één label (zoals AppServer1).</p><p>Nieuwe gebruikersnaam: Typ Hallo-naam van een gebruiker. Deze gebruiker is lid van de lokale beheerdersgroep op Hallo VM Hallo. U moet deze naam toosign in toohello VM voor Hallo eerst. de ingebouwde account Hallo beheerder werkt niet.</p><p>Nieuwe wachtwoord/bevestigen: Typ een wachtwoord</p> |
   |  **Configuratie van virtuele Machine** |<p>Cloudservice: Kies **Maak een nieuwe cloudservice** voor Hallo eerste VM en selecteert u dezelfde servicenaam cloud bij het maken van meer virtuele machines die de toepassing hello zal hosten.</p><p>Cloud-Service DNS-naam: Geef een globaal unieke naam</p><p>Regio/Affiniteitsgroep/virtuele netwerk: Geef Hallo virtueel netwerk op (zoals WestUSVNet).</p><p>Storage-Account: Kies **een automatisch gegenereerde opslagaccount gebruiken** voor Hallo eerste VM en selecteer hetzelfde opslagaccount naam bij het maken van meer virtuele machines die toepassing hello zal hosten.</p><p>Beschikbaarheidsset: Kies **maken van een beschikbaarheidsset**.</p><p>Beschikbaarheidsset: Typ een naam voor Hallo beschikbaarheidsset bij het maken van eerste VM Hallo en selecteer vervolgens dezelfde naam als u meer virtuele machines maakt.</p> |
   |  **Configuratie van virtuele Machine** |<p>Selecteer <b>installeren Hallo VM-Agent</b> en eventuele andere uitbreidingen die u nodig hebt.</p> |
2. Nadat elke virtuele machine is ingericht, aanmelden en lid worden van het toohello domein. In **Serverbeheer**, klikt u op **lokale Server** > **werkgroep** > **wijzigen...** en selecteer vervolgens **domein** en Hallo typenaam van het lokale domein. Geef referenties op van een domeingebruiker en start Hallo VM toocomplete Hallo-domein.

Zie toocreate Hallo VM's met Windows PowerShell in plaats van Hallo-gebruikersinterface [toocreate gebruik Azure PowerShell en vooraf configureren van virtuele Machines op basis van Windows](../virtual-machines/windows/classic/create-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

Zie voor meer informatie over het gebruik van Windows PowerShell [aan de slag met Azure-Cmdlets](/powershell/azure/overview) en [Azure Cmdlet Reference](/powershell/azure/get-started-azureps).

## <a name="additional-resources"></a>Aanvullende bronnen
* [Richtlijnen voor het implementeren van Windows Server Active Directory op virtuele Machines in Azure](https://msdn.microsoft.com/library/azure/jj156090.aspx)
* [Hoe tooupload bestaande on-premises Hyper-V domain controllers tooAzure met behulp van Azure PowerShell](http://support.microsoft.com/kb/2904015)
* [Een nieuw Active Directory-forest installeren op een virtuele Azure-netwerk](active-directory-new-forest-virtual-machine.md)
* [Azure Virtual Network](../virtual-network/virtual-networks-overview.md)
* [Microsoft Azure IT Pro IaaS: grondbeginselen (01) virtuele Machine](http://channel9.msdn.com/Series/Windows-Azure-IT-Pro-IaaS/01)
* [Microsoft Azure IT Pro IaaS: (05) maken van virtuele netwerken en Cross-Premises connectiviteit](http://channel9.msdn.com/Series/Windows-Azure-IT-Pro-IaaS/05)
* [Azure PowerShell](/powershell/azure/overview)
* [Azure Management-Cmdlets](/powershell/module/azurerm.compute/#virtual_machines)

<!--Image references-->
[1]: ./media/active-directory-install-replica-active-directory-domain-controller/ReplicaDCsOnAzureVNet.png

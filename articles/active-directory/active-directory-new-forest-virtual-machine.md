---
title: een Active Directory-forest op een virtuele Azure-netwerk aaaInstall | Microsoft Docs
description: Een zelfstudie waarin wordt uitgelegd hoe toocreate een nieuwe Active Directory-forest op een virtuele machine (VM) op een Azure Virtual Network.
services: active-directory, virtual-network
keywords: 'Active directory virtuele machine van de active directory-forest installeren, azure active directory-video ''s '
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
tags: 
ms.assetid: eb7170d0-266a-4caa-adce-1855589d65d1
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/06/2017
ms.author: joflore
ms.openlocfilehash: 08121130777cc3c206d7b5b38974982884dca1c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="install-a-new-active-directory-forest-on-an-azure-virtual-network"></a>Een nieuw Active Directory-forest installeren op een virtuele Azure-netwerk
Dit onderwerp wordt beschreven hoe een nieuwe Windows Server Active Directory toocreate omgeving op een virtuele Azure-netwerk op een virtuele machine (VM) op een [virtuele Azure-netwerk](../virtual-network/virtual-networks-overview.md). In dit geval is Hallo virtuele Azure-netwerk niet verbonden tooan on-premises netwerk.

U is mogelijk ook geïnteresseerd in de volgende Verwante onderwerpen:

* Zie voor een video ziet u deze stappen [hoe tooinstall een nieuwe Active Directory-forest op een virtuele Azure-netwerk](http://channel9.msdn.com/Series/Microsoft-Azure-Tutorials/How-to-install-a-new-Active-Directory-forest-on-an-Azure-virtual-network)
* U kunt eventueel [een site-naar-site-VPN configureren](../vpn-gateway/vpn-gateway-site-to-site-create.md) en vervolgens een nieuw forest installeert of uitbreiden van een lokale forest tooan virtuele Azure-netwerk. Zie voor deze stappen [een Replica Active Directory-domeincontroller installeren in een Azure Virtual Network](active-directory-install-replica-active-directory-domain-controller.md).
* Raadpleeg voor algemene richtlijnen over het installeren van Active Directory Domain Services (AD DS) op een virtuele Azure-netwerk [richtlijnen voor het implementeren van Windows Server Active Directory op Azure Virtual Machines](https://msdn.microsoft.com/library/azure/jj156090.aspx).

## <a name="scenario-diagram"></a>Scenario-Diagram
In dit scenario moeten de externe gebruikers tooaccess toepassingen die worden uitgevoerd op servers die lid zijn van een domein. Hallo virtuele machines die worden uitgevoerd Hallo-toepassingsservers en Hallo uitgevoerd domeincontrollers zijn geïnstalleerd in hun eigen cloudservice in een Azure-netwerk. Ze zijn ook opgenomen in een beschikbaarheidsset voor verbeterde fouttolerantie.

![Active Directory-forest op een virtuele machines in Azure Virtual Network ][1] 7

## <a name="how-does-this-differ-from-on-premises"></a>Hoe verschilt dit van on-premises?
Er is niet het verschil tussen een domeincontroller installeren in Azure tegenover on-premises. de belangrijkste verschillen Hallo worden vermeld in de volgende tabel Hallo.

| tooconfigure... | On-premises | Azure Virtual Network |
| --- | --- | --- |
| **IP-adres voor het Hallo-domeincontroller** |Statische IP-adres op de eigenschappen van netwerkadapter Hallo toewijzen |Voer Hallo Set AzureStaticVNetIP cmdlet tooassign een statisch IP-adres |
| **DNS-clientresolver** |Voorkeur en alternatieve DNS-serveradres ingesteld op Hallo van domeinleden eigenschappen van netwerkadapter |DNS-serveradres ingesteld voor eigenschappen van virtueel netwerk Hallo Hallo |
| **Active Directory-database-opslag** |Wijzig eventueel Hallo standaardopslaglocatie van C:\ |Moet u de standaardopslaglocatie van C:\ toochange |

## <a name="create-an-azure-virtual-network"></a>Een Azure-netwerk maken
1. Meld u aan toohello klassieke Azure-portal.
2. Een virtueel netwerk maken. Klik op **netwerken** > **een virtueel netwerk maken**. Gebruik Hallo waarden in Hallo toocomplete Hallo-wizard tabel te volgen.

   | Op deze wizardpagina... | Deze waarden opgeven |
   | --- | --- |
   |  **Details van virtueel netwerk** |<p>Naam: Geef een naam voor het virtuele netwerk</p><p>Regio: Hallo dichtstbijzijnde regio kiezen</p> |
   |  **DNS- en VPN** |<p>DNS-server leeg laten</p><p>Een VPN-optie niet selecteert</p> |
   |  **Adresruimten voor virtueel netwerk** |<p>Subnetnaam: Voer een naam voor uw subnet</p><p>Eerste IP: <b>10.0.0.0</b></p><p>CIDR: <b>/24 (256)</b></p> |

## <a name="create-vms-toorun-hello-domain-controller-and-dns-server-roles"></a>Maken van virtuele machines toorun Hallo-domeincontroller en DNS-serverfuncties
Herhaal Hallo stappen toocreate VMs toohost Hallo DC rol naar behoefte te volgen. U moet ten minste twee virtuele DC's tooprovide fouttolerantie en redundantie implementeren. Als u hello virtuele Azure-netwerk bevat ten minste twee domeincontrollers die op dezelfde manier zijn geconfigureerd (ze zijn beide aangegeven, voer DNS-server, en geen van beide bevat FSMO-functie, enzovoort) plaatst Hallo virtuele machines die worden uitgevoerd die DC's in een beschikbaarheidsset voor verbeterde fouttolerantie.

Zie toocreate Hallo VM's met Windows PowerShell in plaats van Hallo-gebruikersinterface [toocreate gebruik Azure PowerShell en vooraf configureren van virtuele Machines op basis van Windows](../virtual-machines/windows/classic/create-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

1. Klik in de klassieke portal Hallo op **nieuw** > **Compute** > **virtuele Machine** > **uit galerie**. Gebruik hello waarden toocomplete Hallo wizard volgen. Accepteer de standaardwaarde Hallo voor een instelling tenzij een andere waarde wordt voorgesteld of vereist.

   | Op deze wizardpagina... | Deze waarden opgeven |
   | --- | --- |
   |  **Een afbeelding kiezen** |Windows Server 2012 R2 Datacenter |
   |  **Configuratie van virtuele Machine** |<p>De naam van de virtuele Machine: Typ een naam met één label (zoals AzureDC1).</p><p>Nieuwe gebruikersnaam: Typ Hallo-naam van een gebruiker. Deze gebruiker is lid van de lokale beheerdersgroep op Hallo VM Hallo. U moet deze naam toosign in toohello VM voor Hallo eerst. de ingebouwde account Hallo beheerder werkt niet.</p><p>Nieuwe wachtwoord/bevestigen: Typ een wachtwoord</p> |
   |  **Configuratie van virtuele Machine** |<p>Cloudservice: Kies <b>Maak een nieuwe cloudservice</b> voor Hallo eerste virtuele machine en selecteer die dezelfde servicenaam cloud bij het maken van meer virtuele machines die als host fungeert Hallo DC-rol.</p><p>Cloud-Service DNS-naam: Geef een globaal unieke naam</p><p>Regio/Affiniteitsgroep/virtuele netwerk: Geef Hallo virtueel netwerk op (zoals WestUSVNet).</p><p>Storage-Account: Kies <b>een automatisch gegenereerde opslagaccount gebruiken</b> voor Hallo eerste virtuele machine en selecteer hetzelfde opslagaccount naam bij het maken van meer virtuele machines die als host fungeert Hallo DC-rol.</p><p>Beschikbaarheidsset: Kies <b>maken van een beschikbaarheidsset</b>.</p><p>Beschikbaarheidsset: Typ een naam voor Hallo beschikbaarheidsset bij het maken van eerste VM Hallo en selecteer vervolgens dezelfde naam als u meer virtuele machines maakt.</p> |
   |  **Configuratie van virtuele Machine** |<p>Selecteer <b>installeren Hallo VM-Agent</b> en eventuele andere uitbreidingen die u nodig hebt.</p> |
2. Voeg een schijf tooeach VM die Hallo DC-serverfunctie wordt uitgevoerd. Hallo extra schijf is benodigde toostore Hallo AD database, logboekbestanden en SYSVOL. Geef een grootte voor het Hallo-schijf (zoals 10 GB) en laat Hallo **Host Cache voorkeur** instellen te**geen**. Zie voor stappen Hallo [hoe tooAttach een gegevensschijf tooa virtuele Windows-Machine](../virtual-machines/windows/classic/attach-disk.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).
3. Nadat u toohello VM voor het eerst aanmelden, opent u **Serverbeheer** > **File and Storage Services** toocreate een volume op deze schijf met NTFS.
4. Reserveer een statisch IP-adres voor virtuele machines die Hallo DC-rol wordt uitgevoerd. een statisch IP-adres tooreserve Hallo Microsoft Web Platform Installer downloaden en [Azure PowerShell installeren](/powershell/azure/overview) en voer de cmdlet Set-AzureStaticVNetIP Hallo uit. Bijvoorbeeld:

    `Get-AzureVM -ServiceName AzureDC1 -Name AzureDC1 | Set-AzureStaticVNetIP -IPAddress 10.0.0.4 | Update-AzureVM`

Zie voor meer informatie over het instellen van een statisch IP-adres [een statische interne IP-adres configureren voor een virtuele machine](../virtual-network/virtual-networks-reserved-private-ip.md).

## <a name="install-windows-server-active-directory"></a>Windows Server Active Directory installeren
Gebruik dezelfde routine te Hallo[installatie van AD DS](https://technet.microsoft.com/library/jj574166.aspx) dat u lokale (dat wil zeggen, kunt u Hallo UI, een antwoordbestand of Windows PowerShell). U moet tooprovide beheerder referenties tooinstall een nieuw forest. toospecify Hallo locatie voor Hallo Active Directory-database, logboekbestanden en SYSVOL, wijzigt Hallo standaardopslaglocatie van Hallo station toohello aanvullende gegevensschijf van besturingssysteem dat u toohello VM gekoppeld.

Nadat Hallo DC-installatie is voltooid, toohello VM opnieuw verbinding te maken en meld u aan toohello DC. Houd er rekening mee toospecify domeinreferenties.

## <a name="reset-hello-dns-server-for-hello-azure-virtual-network"></a>Hallo DNS-server voor Hallo virtuele Azure-netwerk instellen
1. Hallo DNS-doorstuurserver instelling op Hallo nieuwe domeincontroller en DNS-server opnieuw.
   1. Klik in Serverbeheer op **extra** > **DNS**.
   2. In **DNS-beheer**, met de rechtermuisknop op Hallo van Hallo DNS-server en klik op **eigenschappen**.
   3. Op Hallo **doorstuurservers** tabblad Hallo IP-adres van de doorstuurserver Hallo op en klik **bewerken**.  Hallo IP-adres selecteren en op **verwijderen**.
   4. Klik op **OK** tooclose Hallo-editor en **Ok** opnieuw tooclose Hallo DNS-servereigenschappen.
2. Hallo DNS-serverinstellingen voor het virtuele netwerk Hallo bijwerken.
   1. Klik op **virtuele netwerken** > Dubbelklik op Hallo virtuele netwerk die u hebt gemaakt > **configureren** > **DNS-servers**en typ de naam Hallo Hallo DIP van een van Hallo virtuele machines met Hallo domeincontroller en DNS-serverfunctie en klik op **opslaan**.
   2. Selecteer Hallo VM en klik op **opnieuw** tootrigger Hallo VM tooconfigure instellingen DNS-omzetter met IP-adres Hallo Hallo nieuwe DNS-server.

## <a name="create-vms-for-domain-members"></a>Maken van virtuele machines voor leden van een domein
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

## <a name="see-also"></a>Zie ook
* [Hoe tooinstall een nieuwe Active Directory-forest op een virtuele Azure-netwerk](http://channel9.msdn.com/Series/Microsoft-Azure-Tutorials/How-to-install-a-new-Active-Directory-forest-on-an-Azure-virtual-network)
* [Richtlijnen voor het implementeren van Windows Server Active Directory op virtuele Machines in Azure](https://msdn.microsoft.com/library/azure/jj156090.aspx)
* [Een Site-naar-Site-VPN configureren](../vpn-gateway/vpn-gateway-site-to-site-create.md)
* [Een Replica Active Directory-domeincontroller installeren in een Azure-netwerk](active-directory-install-replica-active-directory-domain-controller.md)
* [Microsoft Azure IT Pro IaaS: grondbeginselen (01) virtuele Machine](http://channel9.msdn.com/Series/Windows-Azure-IT-Pro-IaaS/01)
* [Microsoft Azure IT Pro IaaS: (05) maken van virtuele netwerken en Cross-Premises connectiviteit](http://channel9.msdn.com/Series/Windows-Azure-IT-Pro-IaaS/05)
* [Overzicht van Virtual Network](../virtual-network/virtual-networks-overview.md)
* [Hoe tooinstall Azure PowerShell en configureren](/powershell/azure/overview)
* [Azure PowerShell](/powershell/azure/overview)
* [Azure-cmdlet-naslaginformatie](/powershell/azure/get-started-azureps)
* [Azure VM statische IP-adres instellen](http://windowsitpro.com/windows-azure/set-azure-vm-static-ip-address)
* [Hoe tooassign statische IP-tooAzure VM](http://www.bhargavs.com/index.php/2014/03/13/how-to-assign-static-ip-to-azure-vm/)
* [Een nieuwe Active Directory-Forest installeren](https://technet.microsoft.com/library/jj574166.aspx)
* [Inleiding tooActive Directory Domain Services (AD DS) Virtualization (Level 100)](https://technet.microsoft.com/library/hh831734.aspx)

<!--Image references-->
[1]: ./media/active-directory-new-forest-virtual-machine/AD_Forest.png

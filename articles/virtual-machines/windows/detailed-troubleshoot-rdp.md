---
title: de extern bureaublad aaaDetailed probleemoplossing in Azure | Microsoft Docs
description: Bekijk de gedetailleerde stappen voor het externe bureaublad fouten waar u kunt geen tooa Windows virtuele machines in Azure
services: virtual-machines-windows
documentationcenter: 
author: genlin
manager: timlt
editor: 
tags: top-support-issue,azure-service-management,azure-resource-manager
keywords: kan geen verbinding maken tooremote bureaublad, problemen met extern bureaublad, extern bureaublad geen verbinding maken, extern bureaublad-fouten, probleemoplossing extern bureaublad, problemen met extern bureaublad
ms.assetid: 9da36f3d-30dd-44af-824b-8ce5ef07e5e0
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: support-article
ms.date: 07/25/2017
ms.author: genli
ms.openlocfilehash: fcb0d06aa66b748f3ebbbbe3431471d3cbe7c60d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="detailed-troubleshooting-steps-for-remote-desktop-connection-issues-toowindows-vms-in-azure"></a>Gedetailleerde stappen voor verbinding met extern bureaublad problemen tooWindows virtuele machines in Azure
In dit artikel biedt gedetailleerde stappen voor probleemoplossing toodiagnose en fix complexe extern bureaublad-fouten voor op basis van Windows Azure virtual machines.

> [!IMPORTANT]
> tooeliminate Hallo veelvoorkomende fouten van extern bureaublad, zorg ervoor dat tooread [Hallo basic probleemoplossingsartikel voor extern bureaublad](troubleshoot-rdp-connection.md) voordat u doorgaat.

U kunt tegenkomen een extern bureaublad foutbericht die op een van de specifieke foutberichten Hallo niet lijken behandeld in [basic extern bureaublad probleemoplossingsgids Hallo](troubleshoot-rdp-connection.md). Volg deze stappen toodetermine waarom Hallo Remote Desktop (RDP)-client kan geen tooconnect toohello RDP-service op Hallo Azure VM is.

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

Als u meer hulp op elk gewenst moment in dit artikel nodig hebt, kunt u raadplegen hello Azure deskundigen op [hello Azure MSDN en forums Stack Overflow Hallo](https://azure.microsoft.com/support/forums/). U kunt ook kunt u ook een incident voor ondersteuning van Azure bestand. Ga toohello [ondersteuning van Azure site](https://azure.microsoft.com/support/options/) en klik op **Get Support**. Lees voor informatie over het gebruik van Azure-ondersteuning Hallo [Veelgestelde vragen over Microsoft Azure-ondersteuning](https://azure.microsoft.com/support/faq/).

## <a name="components-of-a-remote-desktop-connection"></a>Onderdelen van een extern bureaublad-verbinding
Hallo na onderdelen betrokken zijn bij een RDP-verbinding:

![](./media/detailed-troubleshoot-rdp/tshootrdp_0.png)

Voordat u doorgaat, kan het handig zijn toomentally bekijken wat is gewijzigd sinds Hallo laatste geslaagde extern bureaublad verbinding toohello VM. Bijvoorbeeld:

* openbaar IP-adres van Hallo VM of Hallo cloudservice met VM Hallo Hallo (ook wel Hallo virtueel IP-adres [VIP](https://en.wikipedia.org/wiki/Virtual_IP_address)) is gewijzigd. Hallo RDP-fout kan worden, omdat de DNS client-cache nog steeds Hallo heeft *oude IP-adres* geregistreerd voor Hallo DNS-naam. Uw DNS-client-cache leegmaken en probeer opnieuw verbinding te maken Hallo VM. Of probeer verbinding te maken met het nieuwe VIP Hallo rechtstreeks.
* U gebruikt een toepassing van derden toomanage uw extern bureaublad-verbindingen in plaats van Hallo-verbinding die worden gegenereerd door hello Azure-portal. Controleer of dat de configuratie van die toepassing hello Hallo juiste TCP-poort voor extern bureaublad-verkeer Hallo bevat. U kunt deze poort voor een klassieke virtuele machine in Hallo controleren [Azure-portal](https://portal.azure.com), door te klikken op Hallo van de virtuele machine-instellingen > eindpunten.

## <a name="preliminary-steps"></a>Voorbereidende stappen
Voordat u doorgaat toohello gedetailleerde probleemoplossing

* Status van Hallo virtuele machine in Azure-portal voor eventuele problemen met de hand liggende Hallo Hallo controleren.
* Ga als volgt Hallo [quick fix voor veelvoorkomende RDP-fouten in het Hallo oplossen stappen](troubleshoot-rdp-connection.md#quick-troubleshooting-steps).

Probeer opnieuw verbinding te maken toohello VM via Extern bureaublad na deze stappen.

## <a name="detailed-troubleshooting-steps"></a>Gedetailleerde stappen voor het oplossen van problemen
Hallo extern bureaublad-client mogelijk niet kunnen tooreach Hallo extern bureaublad-service op Azure VM Hallo vanwege tooissues op Hallo de volgende bronnen:

* [Extern-bureaubladclient computer](#source-1-remote-desktop-client-computer)
* [Organisatie intranet randapparaat](#source-2-organization-intranet-edge-device)
* [De cloud service-eindpunt en toegangsbeheerlijsten (ACL)](#source-3-cloud-service-endpoint-and-acl)
* [Netwerkbeveiligingsgroepen](#source-4-network-security-groups)
* [Op basis van Windows Azure VM](#source-5-windows-based-azure-vm)

## <a name="source-1-remote-desktop-client-computer"></a>: 1 extern-bureaubladclient broncomputer
Controleer of dat de computer extern bureaublad kunt aanbrengen verbindingen tooanother lokaal, op basis van Windows-computer.

![](./media/detailed-troubleshoot-rdp/tshootrdp_1.png)

Als u niet controleren op Hallo instellingen op uw computer te volgen:

* Een lokale firewall-instelling wordt extern bureaublad-verkeer blokkeert.
* Lokaal geïnstalleerde clientsoftware proxy dat voorkomt extern bureaublad-verbindingen dat.
* Lokaal geïnstalleerde software die wordt verhinderd door een extern bureaublad-verbindingen voor netwerkbeheer.
* Andere typen beveiligingssoftware die om verkeer te controleren of in een specifieke typen verkeer dat wordt verhinderd door een extern bureaublad-verbindingen toestaan/weigeren.

In dergelijke gevallen tijdelijk Hallo software uit te schakelen en probeer het tooconnect tooan lokale computer via Extern bureaublad. Als u hier de werkelijke oorzaak Hallo op deze manier vindt, samen met uw beheerder toocorrect Hallo software instellingen tooallow extern bureaublad netwerkverbindingen.

## <a name="source-2-organization-intranet-edge-device"></a>Bron 2: Organisatie intranet randapparaat
Controleer of dat een computer rechtstreeks verbonden toohello die Internet extern bureaublad-verbindingen tooyour Azure virtuele machine kunt maken.

![](./media/detailed-troubleshoot-rdp/tshootrdp_2.png)

Als u een computer die rechtstreeks verbonden zijn met toohello Internet niet hebt, maakt en testen met een nieuwe Azure virtuele machine in een bronservice groep of cloud. Zie voor meer informatie [maken van een virtuele machine waarop Windows wordt uitgevoerd in Azure](../virtual-machines-windows-hero-tutorial.md). U kunt Hallo virtuele machine en de resourcegroep Hallo of Hallo-cloudservice, verwijderen nadat Hallo testen.

Als u een extern bureaublad-verbinding met een computer die rechtstreeks zijn gekoppeld toohello Internet maken kunt, controleert u het apparaat aan uw organisatie intranet rand voor:

* Een interne firewall HTTPS-verbindingen toohello Internet blokkeren.
* Een proxyserver extern bureaublad-verbindingen te blokkeren.
* Inbraakdetectie of software die wordt uitgevoerd op apparaten in uw netwerk rand dat voorkomt extern bureaublad-verbindingen dat voor netwerkbeheer.

Werken met uw beheerder toocorrect Hallo netwerkinstellingen van uw organisatie intranet rand apparaat tooallow extern bureaublad HTTPS gebaseerde verbindingen toohello Internet.

## <a name="source-3-cloud-service-endpoint-and-acl"></a>Bron 3: De Cloud service-eindpunt en ACL
Voor virtuele machines die zijn gemaakt met behulp van Hallo klassieke implementatiemodel, Controleer of een andere virtuele machine van Azure die kunt Hallo moeten dezelfde cloudservice of virtuele netwerk extern bureaublad-verbindingen tooyour Azure VM.

![](./media/detailed-troubleshoot-rdp/tshootrdp_3.png)

> [!NOTE]
> Voor virtuele machines is gemaakt in de Resource Manager, overslaan te[bron 4: Netwerkbeveiligingsgroepen](#source-4-network-security-groups).

Als u beschikt niet over een andere virtuele machine in dezelfde cloudservice of een virtueel netwerk hello, maakt u een. Volg de stappen Hallo in [maken van een virtuele machine waarop Windows wordt uitgevoerd in Azure](../virtual-machines-windows-hero-tutorial.md). Hallo test-virtuele machine verwijderen nadat het Hallo-test is voltooid.

Als u verbinding via Extern bureaublad tooa virtuele machine in Hallo maken kunt dezelfde service of het virtuele netwerk, cloud voor deze instellingen controleren:

* Hallo eindpuntconfiguratie voor extern bureaublad-verkeer op Hallo doel VM: Hallo persoonlijke TCP-poort van het Hallo-eindpunt moet overeenkomen met de Hallo TCP-poort op welke Hallo van de virtuele machine extern bureaublad-service luistert (de standaardwaarde is 3389).
* Hallo ACL voor Hallo extern bureaublad-verkeer eindpunt op Hallo doel VM: ACL's kunnen u toospecify toegestaan of geweigerd inkomend verkeer van Internet op basis van de IP-bronadres Hallo. Onjuist geconfigureerde ACL's kunnen voorkomen dat binnenkomende toohello eindpunt van de extern bureaublad-verkeer. Controleer de ACL's tooensure dat binnenkomend verkeer van uw openbare IP-adressen van uw proxy of andere edge-server is toegestaan. Zie voor meer informatie [wat is er een netwerk lijst ACL (Access Control)?](../../virtual-network/virtual-networks-acl.md)

toocheck als Hallo eindpunt Hallo bron van Hallo probleem, verwijderen van huidige Hallo-eindpunt en maak een nieuwe, een willekeurige poort te kiezen in Hallo bereik 49152 – 65535 voor de externe poortnummer Hallo. Zie voor meer informatie [hoe tooset eindpunten tooa virtuele machine](classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

## <a name="source-4-network-security-groups"></a>Bron 4: Netwerkbeveiligingsgroepen
Netwerkbeveiligingsgroepen toestaan meer gedetailleerd beheer van toegestane binnenkomend en uitgaand verkeer. U kunt maken van regels spanning subnetten en cloudservices in een Azure-netwerk.

Gebruik [IP-stroom controleren](../../network-watcher/network-watcher-check-ip-flow-verify-portal.md) tooconfirm als een regel in een Netwerkbeveiligingsgroep tooor van een virtuele machine verkeer blokkeert. U kunt ook effectieve beveiligingsgroep tooensure inkomende 'Toestaan' NSG regels regel bestaat en is geplaatst voor RDP-poort (standaard 3389) bekijken. Zie voor meer informatie [effectieve beveiligingsregels voor verbindingen met behulp van tootroubleshoot VM verkeer stroom](../../virtual-network/virtual-network-nsg-troubleshoot-portal.md#using-effective-security-rules-to-troubleshoot-vm-traffic-flow).

## <a name="source-5-windows-based-azure-vm"></a>Bron 5: Op basis van Windows Azure VM
![](./media/detailed-troubleshoot-rdp/tshootrdp_5.png)

Volg de instructies in Hallo [in dit artikel](reset-rdp.md). In dit artikel stelt Hallo extern bureaublad-service op Hallo virtuele machine:

* Hallo 'Extern bureaublad' Windows Firewall standaardregel (TCP-poort 3389) inschakelen.
* Extern bureaublad-verbindingen inschakelen door in te stellen Hallo HKLM\System\CurrentControlSet\Control\Terminal Server\fDenyTSConnections register waarde too0.

Hallo verbinding tussen uw computer opnieuw proberen. Als u nog steeds niet kunt tooconnect via Extern bureaublad, controleren op Hallo mogelijke problemen met het volgende:

* Hallo extern bureaublad-service wordt niet uitgevoerd op het Hallo-doel VM.
* Hallo extern bureaublad-service luistert niet op TCP-poort 3389.
* Windows Firewall of een andere lokale firewall heeft een uitgaande regel dat voorkomt extern bureaublad-verkeer dat.
* Inbraakdetectie of -software die wordt uitgevoerd op virtuele machine van Azure Hallo netwerkbewaking houdt extern bureaublad-verbindingen.

Voor virtuele machines gemaakt met het klassieke implementatiemodel hello, kunt u een externe toohello Azure PowerShell-sessie virtuele machine van Azure. Eerst moet u een certificaat tooinstall voor hosting cloudservice Hallo virtuele machine. Ga te[beveiligde externe PowerShell toegang configureren tooAzure virtuele Machines](http://gallery.technet.microsoft.com/scriptcenter/Configures-Secure-Remote-b137f2fe) en download Hallo **InstallWinRMCertAzureVM.ps1** script bestand tooyour lokale computer.

Vervolgens installeert u Azure PowerShell als u dat nog niet gedaan hebt. Zie [hoe tooinstall en configureren van Azure PowerShell](/powershell/azure/overview).

Open een Azure PowerShell-opdrachtprompt en Hallo huidige toohello locatie wijzigen Hallo **InstallWinRMCertAzureVM.ps1** scriptbestand. toorun een Azure PowerShell-script, moet u de juiste uitvoeringsbeleid Hallo instellen. Voer Hallo **Get-ExecutionPolicy** toodetermine uw huidige beleidsniveau opdracht. Zie voor meer informatie over het instellen van het juiste niveau Hallo [Set-ExecutionPolicy](https://technet.microsoft.com/library/hh849812.aspx).

Vul vervolgens de naam van uw Azure-abonnement, Hallo cloudservicenaam en de naam van uw virtuele machine (Hallo < en > tekens verwijderen) en voer vervolgens deze opdrachten.

```powershell
$subscr="<Name of your Azure subscription>"
$serviceName="<Name of hello cloud service that contains hello target virtual machine>"
$vmName="<Name of hello target virtual machine>"
.\InstallWinRMCertAzureVM.ps1 -SubscriptionName $subscr -ServiceName $serviceName -Name $vmName
```

Kunt u de naam van de juiste abonnement Hallo krijgen via Hallo *SubscriptionName* eigenschap van het Hallo-weergave van Hallo **Get-AzureSubscription** opdracht. U kunt Hallo cloudservicenaam voor Hallo virtuele machine ophalen uit Hallo *ServiceName* kolom in de weergave Hallo Hallo **Get-AzureVM** opdracht.

Controleer of u het nieuwe certificaat Hallo hebt. Een module Certificaten voor de huidige gebruiker Hallo opent en bekijkt hello **Trusted Root Certification certificeringsinstanties\certificaten** map. Er is een certificaat met de Hallo DNS-naam van de cloudservice in Hallo verleend toocolumn (voorbeeld: cloudservice4testing.cloudapp.net).

Vervolgens een externe Azure PowerShell-sessie starten met behulp van deze opdrachten.

```powershell
$uri = Get-AzureWinRMUri -ServiceName $serviceName -Name $vmName
$creds = Get-Credential
Enter-PSSession -ConnectionUri $uri -Credential $creds
```

Na het invoeren van geldige beheerdersreferenties, ziet u iets dergelijks toohello Azure PowerShell-prompt te volgen:

```powershell
[cloudservice4testing.cloudapp.net]: PS C:\Users\User1\Documents>
```

Hallo eerste deel van deze vraag is de naam van uw cloud-service met Hallo doel VM, die kan afwijken van 'cloudservice4testing.cloudapp.net'. U kunt nu uitgeven Azure PowerShell-opdrachten voor deze cloud service tooinvestigate Hallo problemen vermeld en Hallo configuratie corrigeren.

### <a name="toomanually-correct-hello-remote-desktop-services-listening-tcp-port"></a>toomanually juiste Hallo luisteren TCP-poort van extern bureaublad-Services
Een opdrachtprompt Hallo externe Azure PowerShell-sessie, kunt u deze opdracht uitvoeren.

```powershell
Get-ItemProperty -Path "HKLM:\System\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp" -Name "PortNumber"
```

Hallo eigenschap PortNumber ziet u het huidige poortnummer Hallo. Indien nodig, Hallo extern bureaublad-poort nummer back tooits standaardwaarde wijzigen (3389) met deze opdracht.

```powershell
Set-ItemProperty -Path "HKLM:\System\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp" -Name "PortNumber" -Value 3389
```

Controleer of dat Hallo-poort gewijzigd too3389 is met deze opdracht.

```powershell
Get-ItemProperty -Path "HKLM:\System\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp" -Name "PortNumber"
```

De externe Azure PowerShell-sessie Hallo sluiten met deze opdracht.

```powershell
Exit-PSSession
```

Controleer of de dat TCP-poort 3398 ook als de interne poort die Hallo extern bureaublad-eindpunt voor hello Azure VM wordt gebruikt. Opnieuw opstarten hello Azure VM en probeer het opnieuw Hallo extern bureaublad-verbinding.

## <a name="additional-resources"></a>Aanvullende bronnen
[Hoe tooreset een wachtwoord of Hallo extern bureaublad voor virtuele machines van Windows-service](reset-rdp.md)

[Hoe tooinstall Azure PowerShell en configureren](/powershell/azure/overview)

[Secure Shell (SSH) verbindingen tooa op basis van Linux virtuele machine van Azure oplossen](../linux/troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[Toegang tooan toepassing die wordt uitgevoerd op een virtuele machine van Azure oplossen](../linux/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)


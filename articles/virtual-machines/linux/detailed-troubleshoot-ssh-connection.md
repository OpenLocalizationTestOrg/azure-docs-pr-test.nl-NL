---
title: aaaDetailed SSH voor probleemoplossing voor een virtuele machine in Azure | Microsoft Docs
description: Gedetailleerde probleemoplossing voor problemen die verbinding maken met virtuele machine van Azure tooan SSH
keywords: SSH verbinding geweigerd, ssh fout, azure ssh, SSH-verbinding is mislukt
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: top-support-issue,azure-service-management,azure-resource-manager
ms.assetid: b8e8be5f-e8a6-489d-9922-9df8de32e839
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: support-article
ms.date: 07/06/2017
ms.author: iainfou
ms.openlocfilehash: 3f711e53a8251f8c06dbb589a258222566a4ae1e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="detailed-ssh-troubleshooting-steps-for-issues-connecting-tooa-linux-vm-in-azure"></a>Gedetailleerde SSH probleemoplossing voor problemen die verbinding maken met tooa Linux VM in Azure
Er zijn veel mogelijke oorzaken dat die Hallo SSH-client mogelijk niet kunnen tooreach Hallo SSH-service op Hallo VM. Als u meer via Hallo hebt gevolgd [algemene SSH stappen voor probleemoplossing](troubleshoot-ssh-connection.md), moet u toofurther Hallo verbindingsprobleem op te lossen. In dit artikel begeleidt u gedetailleerde probleemoplossing stappen toodetermine waar Hallo SSH-verbinding is mislukt en hoe tooresolve deze.

## <a name="take-preliminary-steps"></a>Voorbereidende stappen uitvoeren
Hallo toont volgende diagram Hallo-onderdelen die betrokken zijn.

![Diagram waarin de onderdelen van SSH-service](./media/detailed-troubleshoot-ssh-connection/ssh-tshoot1.png)

Hallo helpen volgende stappen u Hallo bron van Hallo fout isoleren en oplossingen of tijdelijke oplossingen te achterhalen.

1. Controleer de status van de Hallo Hallo VM in Hallo-portal.
   In Hallo [Azure-portal](https://portal.azure.com), selecteer **virtuele machines** > *VM-naam*.

   Hallo statusvenster Hallo VM moet worden weergegeven **met**. Schuif naar beneden tooshow recente activiteiten voor de berekenings-, opslag- en netwerkbronnen.

2. Selecteer **instellingen** tooexamine eindpunten, IP-adressen, beveiligingsgroepen en andere instellingen.

   Hallo VM moet een eindpunt dat is gedefinieerd voor de SSH-verkeer dat u kunt bekijken in **eindpunten** of  **[netwerkbeveiligingsgroep](../../virtual-network/virtual-networks-nsg.md)**. Eindpunten in virtuele machines die zijn gemaakt met Resource Manager worden opgeslagen in een netwerkbeveiligingsgroep. Controleer ook dat Hallo regels toegepaste toohello netwerkbeveiligingsgroep is en dat ze wordt verwezen in Hallo subnet.

netwerkverbinding tooverify Hallo geconfigureerd eindpunten te zien als u Hallo VM via een ander protocol, zoals HTTP- of een andere service kan bereiken.

Na deze stappen Hallo SSH-verbinding opnieuw te proberen.

## <a name="find-hello-source-of-hello-issue"></a>Hallo-bron van het probleem Hallo vinden
Hallo SSH-client op uw computer mislukken tooreach Hallo SSH-service op Azure VM Hallo vervaldatum tooissues of configuratiefouten in Hallo gebieden te volgen:

* [SSH-clientcomputer](#source-1-ssh-client-computer)
* [Randapparaat organisatie](#source-2-organization-edge-device)
* [De cloud service-eindpunt en toegangsbeheerlijsten (ACL)](#source-3-cloud-service-endpoint-and-acl)
* [Netwerkbeveiligingsgroepen](#source-4-network-security-groups)
* [Azure virtuele machine op basis van Linux](#source-5-linux-based-azure-virtual-machine)

## <a name="source-1-ssh-client-computer"></a>Bron 1: SSH clientcomputer
tooeliminate uw computer als de bron Hallo Hallo mislukt, Controleer of dat het SSH-verbindingen tooanother on-premises kunt maken op basis van Linux-computer.

![Diagram illustreert de onderdelen voor clientcomputers SSH](./media/detailed-troubleshoot-ssh-connection/ssh-tshoot2.png)

Als Hallo verbinding mislukt, controleert u de Hallo problemen op uw computer te volgen:

* Een instelling van lokale firewall binnenkomende of uitgaande SSH-verkeer (TCP 22 blokkeert)
* Lokaal geïnstalleerde clientsoftware proxy waardoor SSH-verbindingen
* Lokaal geïnstalleerde software die wordt verhinderd door een SSH-verbindingen voor netwerkbeheer
* Andere typen beveiligingssoftware die om verkeer te controleren of in een specifieke soorten verkeer toestaan/weigeren

Als een van deze voorwaarden van toepassing, tijdelijk Hallo software uit te schakelen en probeer het een SSH-verbinding tooan lokale computer toofind uit Hallo reden Hallo verbinding wordt geblokkeerd op uw computer. Vervolgens kunt u samenwerken met uw beheerder toocorrect Hallo software instellingen tooallow SSH netwerkverbindingen.

Als u verificatie via certificaat gebruikt, controleert u of u deze machtigingen toohello SSH-map in de basismap hebt:

* Type chmod 700 ~/.ssh
* Type chmod 644 ~/.ssh/\*.pub
* Type chmod 600 ~/.ssh/id_rsa (of andere bestanden die opgeslagen in deze persoonlijke sleutels zijn)
* Type chmod 644 ~/.ssh/known_hosts (bevat dat u verbinding hebt gemaakt toovia SSH-hosts)

## <a name="source-2-organization-edge-device"></a>Bron 2: Organisatie randapparaat
tooeliminate uw organisatie randapparaat als bron Hallo Hallo mislukt, Controleer of dat een computer die direct toohello Internet is verbonden SSH-verbindingen tooyour virtuele Azure-machine kunt maken. Als u Hallo VM via een VPN site-naar-site of een Azure ExpressRoute-verbinding benaderen wilt, gaat u verder te[bron 4: Netwerkbeveiligingsgroepen](#nsg).

![Diagram die organisatie randapparaat markeert](./media/detailed-troubleshoot-ssh-connection/ssh-tshoot3.png)

Als u een computer die rechtstreeks verbonden zijn met toohello Internet geen hebt, een nieuwe Azure-virtuele machine maken in een eigen bronservice of cloudbereik en worden gebruikt. Zie voor meer informatie [maken van een virtuele machine waarop Linux wordt uitgevoerd in Azure](quick-create-cli.md). Hallo-resource groep of virtuele machine en cloud-service verwijderen wanneer u met het testen bent klaar.

Als u een SSH-verbinding met een computer die direct toohello Internet is verbonden maken kunt, controleert u het apparaat van rand voor uw organisatie voor:

* Een interne firewall verkeer SSH Hello Internet blokkeert
* Een proxyserver die wordt verhinderd door een SSH-verbindingen
* Inbraakdetectie of software die wordt uitgevoerd op apparaten in uw netwerk rand waardoor SSH-verbindingen voor netwerkbeheer

Werken met uw beheerder toocorrect Hallo netwerkinstellingen van uw organisatie rand apparaten tooallow SSH verkeer Hello Internet.

## <a name="source-3-cloud-service-endpoint-and-acl"></a>Bron 3: De Cloud service-eindpunt en ACL
> [!NOTE]
> Deze bron is van toepassing alleen tooVMs die zijn gemaakt met het klassieke implementatiemodel Hallo. Voor virtuele machines die zijn gemaakt met Resource Manager, overslaan te[4 bron: Netwerkbeveiligingsgroepen](#nsg).

tooeliminate Hallo cloud service-eindpunt en ACL als bron Hallo Hallo mislukt, Controleer of een andere Azure virtuele machine in Hallo hetzelfde virtuele netwerk kunt SSH-verbindingen tooyour VM maken.

![Diagram cloud service-eindpunt en ACL illustreert](./media/detailed-troubleshoot-ssh-connection/ssh-tshoot4.png)

Als u geen een andere virtuele machine in Hallo hetzelfde virtuele netwerk, kunt u gemakkelijk maken. Zie voor meer informatie [maken van een Linux-VM op Azure met behulp van Hallo CLI](quick-create-cli.md). Verwijder extra VM Hallo wanneer u klaar bent met het testen.

Als u een SSH-verbinding kunt maken met een VM in Hallo hetzelfde virtuele netwerk, Controleer Hallo gebieden te volgen:

* **Hallo eindpuntconfiguratie voor SSH-verkeer op Hallo doel VM.** Hallo persoonlijke TCP-poort van het Hallo-eindpunt moet overeenkomen met de Hallo TCP-poort op welke Hallo SSH-service op Hallo VM luistert. (de standaardpoort Hallo is 22). Hallo SSH TCP-poortnummer in hello Azure-portal controleren door te selecteren **virtuele machines** > *VM-naam* > **instellingen**  >  **Eindpunten**.
* **Hallo ACL voor Hallo SSH verkeer eindpunt op Hallo doel-virtuele machine.** Een ACL kunt u toospecify toegestaan of geweigerd inkomend verkeer van Hallo Internet, op basis van de bron-IP-adres. Onjuist geconfigureerde ACL's kunnen voorkomen dat binnenkomende toohello eindpunt van de SSH-verkeer. Controleer de ACL's tooensure dat binnenkomend verkeer van openbare IP-adressen van uw proxy of andere edge-server Hallo is toegestaan. Zie voor meer informatie [over toegang tot het netwerk toegangsbeheerlijsten (ACL's)](../../virtual-network/virtual-networks-acl.md).

tooeliminate hello eindpunt als bron van Hallo probleem, verwijderen van de huidige endpoint hello, maken van een ander eindpunt en Hallo SSH-naam (TCP-poort 22 voor openbare en persoonlijke poortnummer Hallo) opgeven. Zie voor meer informatie [-eindpunten op een virtuele machine in Azure instellen](../windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

<a id="nsg"></a>

## <a name="source-4-network-security-groups"></a>Bron 4: Netwerkbeveiligingsgroepen
Netwerkbeveiligingsgroepen kunnen u toohave gedetailleerde controle over de toegestane binnenkomend en uitgaand verkeer. U kunt regels die subnetten omvatten en cloudservices in een Azure-netwerk maken. Controleer uw netwerk beveiliging groep regels tooensure die SSH-verkeer tooand van Hallo die Internet is toegestaan.
Zie voor meer informatie [over netwerkbeveiligingsgroepen](../../virtual-network/virtual-networks-nsg.md).

U kunt ook toovalidate hello NSG-configuratie verifiëren van IP-gebruiken. Zie voor meer informatie [Azure-netwerk bewakingsoverzicht](https://docs.microsoft.com/en-us/azure/network-watcher/network-watcher-monitoring-overview). 

## <a name="source-5-linux-based-azure-virtual-machine"></a>Bron 5: Op basis van Linux virtuele machine van Azure
Hallo laatste bron van mogelijke problemen is hello Azure virtuele machine zelf.

![Diagram die worden gemarkeerd op basis van Linux virtuele machine van Azure](./media/detailed-troubleshoot-ssh-connection/ssh-tshoot5.png)

Als u dit nog niet hebt gedaan, volgt u Hallo instructies [tooreset een wachtwoord of SSH voor virtuele machines op basis van Linux](classic/reset-access.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).

Probeer opnieuw verbinding te maken van uw computer. Als het nog steeds mislukt, volgen Hallo enkele mogelijke problemen Hallo:

* Hallo SSH-service wordt niet uitgevoerd op de virtuele doelmachine Hallo.
* Hallo SSH-service luistert niet op TCP-poort 22. tootest, installeer een Telnet-client op uw lokale computer en voer ' telnet *cloudServiceName*. cloudapp.net 22 '. Deze stap bepaalt als Hallo virtuele machine binnenkomende en uitgaande communicatie toohello SSH-eindpunt kunt.
* Hallo lokale firewall op de virtuele doelmachine Hallo heeft regels die verhinderen binnenkomend of uitgaand verkeer van SSH dat.
* Inbraakdetectie of -software die wordt uitgevoerd op virtuele machine van Azure Hallo netwerkbewaking houdt SSH-verbindingen.

## <a name="additional-resources"></a>Aanvullende bronnen
Zie voor meer informatie over het oplossen van toegang tot toepassingen [problemen met toegang tooan toepassing die wordt uitgevoerd op een virtuele machine van Azure](troubleshoot-app-connection.md)

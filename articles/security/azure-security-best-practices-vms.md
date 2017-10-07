---
title: aanbevolen beveiligingsprocedures aaaAzure virtuele machine | Microsoft Docs
description: In dit artikel biedt tal van security best practices toobe gebruikt in virtuele machines in Azure.
services: security
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: 5e757abe-16f6-41d5-b1be-e647100036d8
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/19/2017
ms.author: yurid
ms.openlocfilehash: b03bcc75fde6d49897f9a7f6f15aec87456edd0a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="best-practices-for-azure-vm-security"></a>Aanbevolen procedures voor beveiliging van de virtuele machine in Azure

In de meeste infrastructuur als een dienst (IaaS)-scenario's [virtuele Azure-machines (VM's)](https://docs.microsoft.com/en-us/azure/virtual-machines/) zijn de belangrijkste werkbelasting Hallo voor organisaties die gebruikmaken van de cloud computing. Dit is vooral duidelijk in [hybride scenario's](https://social.technet.microsoft.com/wiki/contents/articles/18120.hybrid-cloud-infrastructure-design-considerations.aspx) waar de werkbelastingen toohello cloud voor het migreren van organisaties willen tooslowly. In dergelijke scenario's, voert u de Hallo [algemene beveiligingsoverwegingen voor IaaS](https://social.technet.microsoft.com/wiki/contents/articles/3808.security-considerations-for-infrastructure-as-a-service-iaas.aspx), en toepassen van security best practices tooall uw virtuele machines.

Dit artikel worden de verschillende VM best practices voor beveiliging, elk afgeleid van onze klanten en ons eigen direct ervaringen met virtuele machines.

Hallo best practices zijn gebaseerd op een consensus van advies en ze werken met de huidige Azure-platformmogelijkheden en functies sets. Omdat adviezen en technologieën na verloop van tijd veranderen kunnen, we tooupdate van plan dit artikel regelmatig tooreflect deze wijzigingen.

Voor elke best practice Hallo artikel wordt beschreven:

* Welke Hallo aanbevolen procedure is.
* Daarom is het een goed idee tooenable deze.
* Hoe meer u tooenable deze.
* Wat kan gebeuren als u tooenable mislukken deze.
* Mogelijke alternatieven toohello best practices.

Hallo artikel onderzoekt Hallo VM aanbevolen beveiligingsprocedures volgen:

* VM-verificatie en toegangsbeheer
* Toegang tot de beschikbaarheid en netwerken van de virtuele machine
* Gegevens in rust in virtuele machines beveiligen door af te dwingen van versleuteling
* Uw VM-updates beheren
* Uw beveiligingspostuur VM beheren
* VM-prestaties bewaken

## <a name="vm-authentication-and-access-control"></a>VM-verificatie en toegangsbeheer

Hallo eerste stap bij het beveiligen van uw virtuele machine is tooensure dat alleen gemachtigde gebruikers kunnen tooset van nieuwe virtuele machines. U kunt [Azure Resource Manager-beleid](../azure-resource-manager/resource-manager-policy.md) tooestablish conventies voor bronnen in uw organisatie aangepaste beleidsregels maken en deze tooresources beleid van toepassing zoals [resourcegroepen](../azure-resource-manager/resource-group-overview.md).

Virtuele machines die deel uitmaken van de resourcegroep tooa natuurlijk neemt de beleidsregels. Het wordt aangeraden deze benadering toomanaging virtuele machines, u kunt ook beheren toegang tooindividual VM beleid met behulp van [op rollen gebaseerde toegangsbeheer (RBAC)](../active-directory/role-based-access-control-configure.md).

Wanneer u beleidsregels voor Resource Manager en RBAC toocontrol VM toegang inschakelt, kunt u helpen verbeteren de algehele beveiliging van de virtuele machine. Het is raadzaam dat u virtuele machines met dezelfde levenscyclus cyclus in Hallo Hallo consolideren dezelfde resourcegroep. Met behulp van resourcegroepen kunt u implementeren, bewaken en samengevouwen facturering kosten voor uw resources. tooenable gebruikers tooaccess en stelt u de virtuele machines, gebruiken een [minimale bevoegdheid benadering](https://technet.microsoft.com/en-us/windows-server-docs/identity/ad-ds/plan/security-best-practices/implementing-least-privilege-administrative-models). En wanneer u bevoegdheden toousers toewijst, plan toouse Hallo ingebouwde Azure rollen te volgen:

- [Virtual Machine Contributor](../active-directory/role-based-access-built-in-roles.md#virtual-machine-contributor): kunnen virtuele machines beheren, maar niet Hallo virtuele netwerk of opslag account toowhich-ze zijn verbonden.
- [Klassieke Virtual Machine Contributor](../active-directory/role-based-access-built-in-roles.md#classic-virtual-machine-contributor): virtuele machines die zijn gemaakt met behulp van het klassieke implementatiemodel hello, maar niet Hallo virtuele netwerk of opslag account toowhich Hallo zijn verbonden met virtuele machines kunt beheren.
- [Beveiligingsbeheer](../active-directory/role-based-access-built-in-roles.md#security-manager): beveiligingsonderdelen, beveiligingsbeleid en virtuele machines kunt beheren.
- [DevTest Labs gebruiker](../active-directory/role-based-access-built-in-roles.md#devtest-labs-user): kunt Alles weergeven en verbinding maken, starten, opnieuw opstarten en afsluiten van virtuele machines.

Deel geen accounts en wachtwoorden tussen beheerders en gebruik wachtwoorden niet niet meerdere gebruikersaccounts of services, met name de wachtwoorden voor sociale media of andere niet-administratieve activiteiten. In het ideale geval moet u [Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md) sjablonen tooset van uw virtuele machines veilig. U kunt met deze benadering versterking van uw implementatie-instellingen en beveiligingsinstellingen in de gehele Hallo implementatie afdwingen.

Organisaties die gegevens toegangsbeheer niet afdwingen door gebruik te maken van mogelijkheden, zoals RBAC mogelijk verleend op basis van hun gebruikers meer bevoegdheden beschikt dan noodzakelijk is. Ongeschikte toegang toocertain gebruikersgegevens kunt die gegevens rechtstreeks beschadigen.

## <a name="vm-availability-and-network-access"></a>Toegang tot de beschikbaarheid en netwerken van de virtuele machine

Als uw virtuele machine wordt uitgevoerd voor kritieke toepassingen die toohave hoge beschikbaarheid moeten, wordt aangeraden dat u meerdere virtuele machines. Voor betere beschikbaarheid, kunt u ten minste twee virtuele machines maken in Hallo [beschikbaarheidsset](../virtual-machines/windows/tutorial-availability-sets.md).

[Azure Load Balancer](../load-balancer/load-balancer-overview.md) vereist ook dat netwerktaakverdeling VMs toohello horen dezelfde beschikbaarheidsset. Als deze virtuele machines moeten worden geopend vanuit Hallo Internet, moet u een [Internet gerichte load balancer](../load-balancer/load-balancer-internet-overview.md).

Bij virtuele machines blootgestelde toohello Internet zijn, is het belangrijk dat u [netwerkverkeer met netwerkbeveiligingsgroepen (nsg's) bepalen](../virtual-network/virtual-networks-nsg.md). Omdat nsg's toegepaste toosubnets zijn kunnen, kunt u Hallo aantal nsg's minimaliseren door uw resources groeperen per subnet en vervolgens nsg's toohello subnetten toe te passen. Hallo bedoeling is een laag van netwerkisolatie, u doen kunt door het juist configureren Hallo toocreate [netwerkbeveiliging](../best-practices-network-security.md) mogelijkheden in Azure.

U kunt ook Hallo just in time (Just in time) VM-access-functie van Azure Security Center toocontrol die externe toegang tooa heeft specifieke virtuele machine, en hoe lang.

Organisaties die netwerk toegangsbeperkingen tooInternet gerichte VM's zijn niet afdwingen blootgesteld toosecurity risico's, zoals een beveiligingsaanval van Remote Desktop Protocol (RDP).

## <a name="protect-data-at-rest-in-your-vms-by-enforcing-encryption"></a>Gegevens in rust in uw virtuele machines beveiligen door af te dwingen van versleuteling

[Gegevensversleuteling in rust](https://blogs.microsoft.com/cybertrust/2015/09/10/cloud-security-controls-series-encrypting-data-at-rest/) is een verplichte stap naar privacy, naleving en gegevens onafhankelijkheid van gegevens. [Azure Disk Encryption](../security/azure-security-disk-encryption.md) kunnen IT-beheerders tooencrypt Windows en Linux IaaS VM-schijven. Schijfversleuteling combineert Hallo industriestandaard Windows BitLocker-onderdeel en Hallo Linux dm-crypt functie tooprovide versleuteling voor volumes voor hello OS- en gegevensschijven Hallo.

U kunt toepassen schijfversleuteling toohelp beveiligt uw gegevens toomeet uw organisatorische vereisten voor beveiliging en naleving. Uw organisatie moet rekening houden met behulp van versleuteling toohelp beperken van toegang tot de gegevens van de risico's gerelateerde toounauthorized. Bovendien aangeraden om uw stations te versleutelen, voordat u gevoelige gegevens toothem schrijven.

Worden tooencrypt ervoor dat uw VM-gegevens volumes tooprotect, plaatst u ze op in uw Azure storage-account. Hallo versleutelingssleutels en geheim beschermen met behulp van [Azure Key Vault](https://azure.microsoft.com/en-us/documentation/articles/key-vault-whatis/).

Organisaties die niet gegevensversleuteling afdwingen zijn meer blootgestelde toodata-problemen met de gegevensintegriteit. Onbevoegde of rogue gebruikers kunnen bijvoorbeeld gestolen gegevens in de accounts waarmee is geknoeid of onbevoegde toegang toodata gecodeerd in ClearFormat krijgen. Naast nemen op dergelijke risico's, toocomply met regelgeving vanuit de sector, moeten bedrijven bewijzen dat zij toewijding inzetten oefent en tooenhance hun gegevens beveiligen met behulp van de juiste beveiligingsgroep bepaalt.

Zie toolearn meer informatie over Disk Encryption [Azure Disk Encryption for Windows en Linux IaaS VM's](azure-security-disk-encryption.md).


## <a name="manage-your-vm-updates"></a>Uw VM-updates beheren

Omdat de virtuele machines van Azure, net als alle on-premises virtuele machines zijn beoogde toobe gebruikers wordt beheerd, Azure biedt geen Windows-updates toothem push. U bent, echter aangemoedigd tooleave Hallo automatisch Windows Update-instelling is ingeschakeld. Een andere optie is toodeploy [Windows Server Update Services (WSUS)](https://technet.microsoft.com/windowsserver/bb332157.aspx) of een ander geschikte updatebeheer product op een andere virtuele machine of on-premises. Houd virtuele machines huidige zowel WSUS als Windows Update. Ook wordt aangeraden dat u een scannen product tooverify die alle IaaS-VM's actief toodate zijn.

Voorraad afbeeldingen geleverd door Azure worden regelmatig bijgewerkt tooinclude Hallo meest recente afronden van Windows-updates. Er is echter geen garantie dat de Hallo afbeeldingen huidige tijdens de implementatie worden. Een kleine vertraging (van niet meer dan een paar weken) na openbare releases mogelijk. Controleren en installeren van alle Windows-updates moet de eerste stap Hallo van elke implementatie. Deze meting is vooral belangrijk tooapply bij het implementeren van installatiekopieën die afkomstig van u of uw eigen bibliotheek zijn. Installatiekopieën die worden geleverd als onderdeel van hello Azure Marketplace worden standaard automatisch bijgewerkt.

Organisaties die geen software-update-beleid af te dwingen zijn meer blootgestelde toothreats die gebruikmaken van bekende, eerder vaste beveiligingsproblemen. Behalve dat u dergelijke bedreigingen, toocomply met regelgeving vanuit de sector, moeten bedrijven bewijzen dat ze toewijding inzetten oefent en met behulp van de juiste beveiligingsgroep besturingselementen toohelp Hallo beveiliging van hun werkbelasting in Hallo cloud bevindt.

Het is belangrijk tooemphasize die software-update best practices voor traditionele datacentra en Azure IaaS hebben veel overeenkomsten. Daarom raden we aan dat u uw huidige software-update-beleid-tooinclude VMs evalueren.

## <a name="manage-your-vm-security-posture"></a>Uw beveiligingspostuur VM beheren

Cyberbeveiliging bedreigingen zijn in ontwikkeling en beveiliging van uw virtuele machines moet een uitgebreide bewaking mogelijkheid die u kunnen snel bedreigingen te detecteren, te voorkomen dat onbevoegde toegang tooyour resources waarschuwing is geactiveerd en fout-positieven te reduceren. Hallo beveiligingspostuur voor dergelijke workload omvat alle beveiligingsaspecten van Hallo VM, van update management toosecure netwerktoegang.

toomonitor hello beveiligingsstatus van uw [Windows](../security-center/security-center-virtual-machine.md) en [virtuele Linux-machines](../security-center/security-center-linux-virtual-machine.md), gebruik [Azure Security Center](../security-center/security-center-intro.md). In Azure Security Center bescherming van uw virtuele machines door gebruik te maken van Hallo volgende mogelijkheden:

* OS-beveiligingsinstellingen aan de regels van de aanbevolen configuratie toepassen
* Identificeren en beveiliging van het systeem en essentiële updates ontbreken mogelijk downloaden
* Eindpunt antimalware bescherming aanbevelingen implementeren
* Schijfversleuteling valideren
* Beoordelen en herstellen van beveiligingsproblemen
* Bedreigingen detecteren

Security Center actief voor bedreigingen kunt bewaken en mogelijke bedreigingen worden weergegeven onder **beveiligingswaarschuwingen**. Gecorreleerde bedreigingen zijn geaggregeerd in één weergave aangeroepen **Security Incident**.

toounderstand hoe Security Center kunt u identificeren mogelijke bedreigingen in uw virtuele machines die zich in Azure, bekijkt hello video te volgen:

<iframe src="https://channel9.msdn.com/Blogs/Azure-Security-Videos/Azure-Security-Center-in-Incident-Response/player" width="960" height="540" allowFullScreen frameBorder="0"></iframe>

Organisaties die een sterke beveiligingspostuur niet voor hun virtuele machines afdwingen blijven niet op de hoogte van mogelijke pogingen door onbevoegden tot stand gebracht toocircumvent beveiligingsmechanismen.

## <a name="monitor-vm-performance"></a>VM-prestaties bewaken

Misbruik van de resource is een probleem als VM processen meer bronnen dan zou moeten gebruiken. Prestatieproblemen met een VM kunnen leiden die niet voldoet aan de beveiligingsprincipal Hallo van beschikbaarheid tooservice wordt onderbroken. Daarom is het imperatieve toomonitor VM toegang niet alleen reactief, terwijl er een probleem optreedt, maar ook proactief tegen basislijn gemeten tijdens normale werking.

Door te analyseren [Azure diagnostische logboekbestanden](https://azure.microsoft.com/en-us/blog/windows-azure-virtual-machine-monitoring-with-wad-extension/), kunt u uw VM-resources bewaken en mogelijke problemen die op de prestaties en beschikbaarheid hebben kunnen. Hallo-extensie voor diagnostische gegevens van Azure biedt mogelijkheden voor controle en diagnostische gegevens op Windows gebaseerde virtuele machines. U kunt deze mogelijkheden inschakelen door uitbreiding Hallo als onderdeel van Hallo [Azure Resource Manager-sjabloon](../virtual-machines/windows/extensions-diagnostics-template.md).

U kunt ook [Azure Monitor](../monitoring-and-diagnostics/monitoring-overview-metrics.md) toogain inzicht in de status van uw resources.

Organisaties die geen VM-prestaties bewaken zijn niet kan toodetermine of bepaalde wijzigingen in prestatiepatronen normale of abnormale zijn. Als Hallo VM meer bronnen dan normaal verbruikt, kan bij een aanval van een externe resource of een waarmee is geknoeid proces in Hallo VM duiden op een dergelijke afwijkingsdetectie.

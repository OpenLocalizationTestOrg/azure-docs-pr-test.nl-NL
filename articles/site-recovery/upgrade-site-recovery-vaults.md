---
title: een Site Recovery-kluis aaaUpgrade tooan Azure Recovery Services-kluis
description: Meer informatie over hoe een Azure Site Recovery-kluis tooupgrade tooa Recovery Services-kluis
documentationcenter: 
author: rajani-janaki-ram
manager: rochakm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/31/2017
ms.author: rajani-janaki-ram
ms.openlocfilehash: a18a923ee3bad91873e654c9b9b5bf8b83acc123
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-a-site-recovery-vault-tooan-azure-resource-manager-based-recovery-services-vault"></a>Upgrade van een Site Recovery-kluis tooan Azure Resource Manager gebaseerde Recovery Services-kluis

Dit artikel wordt beschreven hoe tooupgrade Azure Site Recovery-Service voor herstel op basis van een Resource Manager-kluizen tooAzure zonder invloed op de lopende replicatie kluizen. Zie voor meer informatie over Azure Resource Manager-functies en voordelen [overzicht van Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).

## <a name="introduction"></a>Inleiding
Een Recovery Services-kluis is een Azure Resource Manager-bron voor het beheren van back-up en herstel na noodgevallen in Hallo cloud ingebouwd. Is een uniform kluis die u kunt gebruiken in Hallo nieuwe Azure-portal en vervangt deze Hallo klassieke back-up en kluizen van Site Recovery.

Recovery Services-kluizen bieden een matrix van functies, waaronder:

* Ondersteuning van Azure Resource Manager: U kunt beveiligen en uw virtuele machines en fysieke machines failover in een Azure Resource Manager-stack.

* Schijf uitsluiten: als u tijdelijke bestanden of hoge verloop gegevens die u niet wilt toouse uw bandbreedte voor hebt, kunt u de volumes uitsluiten van replicatie. Deze mogelijkheid is ingeschakeld op dit moment in *VMware tooAzure* en *Hyper-V tooAzure* en ook tooother-scenario's wordt uitgebreid.

* Ondersteuning voor premium en lokaal redundante opslag: U kunt nu servers beveiligen in premium-opslag accounts waarmee klanten tooprotect toepassingen met hogere i/o-bewerkingen per seconde (IOPS). Deze mogelijkheid is momenteel ingeschakeld in *VMware tooAzure*.

* Gestroomlijnde ervaring aan de slag: Hallo verbeterde aan de slag ervaring is ontworpen toomake herstel na noodgevallen setup eenvoudig.

* Back-up en het beheer van de Site Recovery uit dezelfde kluis Hallo: U kunt nu servers voor herstel na noodgevallen beveiligen of back-up van Hallo dezelfde kluis, waardoor uw beheer overhead aanzienlijk kan verminderen.

Zie voor meer informatie over functies en gebruikerservaring Hallo bijgewerkt Hallo [opslag, back-up en herstel blog](https://azure.microsoft.com/blog/azure-site-recovery-now-available-in-a-new-experience-with-support-for-arm-and-csp/).

## <a name="salient-features"></a>Opvallende kenmerken

* Er zijn geen gevolgen voor de lopende replicatie: lopende replicaties doorgaan zonder een onderbreking tijdens en na de upgrade.

* Kan zonder extra kosten: ophalen van een volledige set van bijgewerkte mogelijkheden zonder extra kosten.

* Er is geen gegevensverlies: omdat dit proces een upgrade en niet een migratie is, bestaande herstelpunten voor replicatie en -instellingen blijven behouden tijdens en na de upgrade Hallo.


## <a name="what-happens-during-hello-vault-upgrade"></a>Wat gebeurt er tijdens de upgrade van Hallo kluis?

Tijdens de upgrade hello, kunt u bewerkingen zoals het registreren van een nieuwe server of het inschakelen van replicatie voor een virtuele machine (VM) niet uitvoeren. Bewerkingen met betrekking tot het lezen van gegevens uit of schrijven van gegevens toohello kluis, zoals de lopende replicatie van beveiligde items toohello kluis, niet wordt onderbroken.

### <a name="changes-tooautomation-and-tooling-after-hello-upgrade"></a>Tooautomation en tooling na Hallo upgrade wijzigen
Als u een upgrade uitvoert van Hallo kluis type vanuit Hallo classic deployment model toohello Resource Manager-implementatiemodel, bestaande automatisering Hallo of tooling tooensure dat het toowork na de upgrade Hallo blijft bijwerken.

### <a name="prepare-your-environment-for-hello-upgrade"></a>Uw omgeving voorbereiden voor upgrade Hallo

* [PowerShell installeren of upgraden tooversion 5 of hoger](https://www.microsoft.com/download/details.aspx?id=50395)
* [Hallo meest recente versie van MSI van Azure PowerShell installeren](https://github.com/Azure/azure-powershell/releases)
* [Recovery Services-kluis upgradescript Hallo downloaden](https://aka.ms/vaultupgradescript)

### <a name="prerequisites"></a>Vereisten
tooupgrade van Site Recovery-Service voor herstel op basis van een Resource Manager-kluizen tooAzure kluizen, moet u Hallo volgens de vereisten voldoen:

* Minimale agent-versie: Hallo-versie van Azure Site Recovery Provider is geïnstalleerd op de server moet 5.1.1700.0 of hoger.

* Ondersteunde configuratie: U kunt uw kluis niet configureren met storage area network (SAN) of SQL Server AlwaysOn-beschikbaarheidsgroepen. Alle andere configuraties worden ondersteund.

    >[!NOTE]
    >Na de upgrade hello, kunt u de toewijzing van opslag via de PowerShell beheren.

* Ondersteunde implementatiescenario: uw kluis Hallo mag niet *VMware tooAzure* verouderde implementatiemodel. Voordat u doorgaat, moet u eerst de verbeterde implementatiemodel toohello verplaatsen.

* Geen actieve gebruiker gestart taken die betrekking hebben op management vlak operations: omdat tijdens de upgrade toegang toohello management vlak beperkt is, Voer uw acties voor de vlak management voordat u de upgrade Hallo activeren. Dit proces omvat niet lopende replicatie.

## <a name="frequently-asked-questions"></a>Veelgestelde vragen

**Deze upgrade invloed heeft op Mijn lopende replicatie?**

Nee. De lopende replicatie blijft onderbroken tijdens en na de upgrade Hallo.

**Wat gebeurt er toonetwork instellingen zoals site-naar-site VPN- en IP-instellingen?**

Hallo upgrade heeft geen invloed op Hallo netwerkinstellingen. Alle Azure-naar-on-premises verbindingen blijven behouden.

**Wat gebeurt er toomy kluizen als ik niet van plan tooupgrade in Hallo nabije toekomst bent?**

Ondersteuning voor de Site Recovery-kluis in Hallo oude Azure-portal zullen worden afgeschaft vanaf September 2017. Het is raadzaam Hallo upgradefunctie toomove toohello nieuwe portal te gebruiken.

**Wat betekent dit migratieplan voor mijn bestaande tooling?**  

Bijwerken van uw tooling toohello Resource Manager-implementatiemodel is een van de belangrijkste Hallo-wijzigingen die u in uw upgrade plan moet rekening houden met. Hallo Recovery Services-kluizen zijn gebaseerd op Hallo Resource Manager-implementatiemodel. 

**Hoe lang Hallo management vlak uitvaltijd laatste zijn?**

Hallo upgrade duurt normaal gesproken ongeveer 15 minuten voor too30 en het kan duren voordat tooa maximaal één uur.

**Kan ik terugdraaien na de upgrade?**

Nee. Terugdraaien wordt niet ondersteund nadat Hallo resources hebt geüpgraded.

**Kan ik mijn abonnement of valideren resources toosee of ze kunnen worden bijgewerkt?**

Ja. Hallo eerste stap bij het Hallo-upgrade is in Hallo platform ondersteund upgrade-optie, toovalidate dat Hallo-resources geschikt voor een upgrade zijn. Als Hallo validatie mislukt, ontvangt u passende foutberichten of waarschuwingen.

**Hoe kan ik een probleem met de Hallo upgrade melden?**

Als er fouten tijdens de upgrade hello optreden, houd er rekening mee Hallo bewerkings-ID die opgenomen in het Hallo-fout. Microsoft Support proactief te laten werken op het oplossen van Hallo probleem. U kunt ook contact opnemen met het ondersteuningsteam Hallo met uw abonnements-ID, de kluisnaam en de bewerking-ID. Ondersteuning werkt tooresolve Hallo probleem zo snel mogelijk. Probeer de bewerking Hallo niet opnieuw tenzij u expliciet gebruiksaanwijzing toodo zo is door Microsoft.

## <a name="run-hello-script"></a>Hallo-script uitvoeren

Voer in PowerShell Hallo volgende opdracht:

    PS > .\RecoveryServicesVaultUpgrade-1.0.0.ps1 -SubscriptionID <subscriptionID>  -VaultName <vaultname> -Location <location> -ResourceType HyperVRecoveryManagerVault -TargetResourceGroupName <rgname>

* Abonnements-id: Hallo abonnements-ID die is gekoppeld aan het Hallo-kluis die u een upgrade uitvoert.

* VaultName: naam van Hallo van Hallo kluis die u een upgrade uitvoert.

* Locatie: locatie van Hallo van Hallo kluis die u een upgrade uitvoert.

* ResourceType: HyperVRecoveryManagerVault voor Site Recovery-kluizen.

* TargetResourceGroupName: Hallo resourcegroep waarin u wilt dat Hallo bijgewerkt kluis toobe geplaatst. TargetResourceGroupName kan een bestaande resourcegroep in Azure Resource Manager of een nieuwe zijn. Als Hallo TargetResourceGroupName dat wordt meegeleverd niet bestaat, wordt deze gemaakt als onderdeel van de upgrade Hallo in Hallo dezelfde locatie als Hallo-kluis. Zie voor meer informatie Hallo 'Resourcegroepen' sectie [overzicht van Azure Resource Manager](../azure-resource-manager/resource-group-overview.md#resource-groups).

    >[!NOTE]
    >Naamgeving van de resource-groep is onderwerp toocertain beperkingen. tooprevent kluis upgrade mislukt, ervoor tooobserve Hallo naamgevingsconventie zorgvuldig worden.
    >
    >Bijvoorbeeld:
    >
    >.\RecoveryServicesVaultUpgrade-1.0.0.ps1 - SubscriptionId 1234-54123-354354-56416-8645 - VaultName gen2dr-locatie 'Noord-Europa' - ResourceType hypervrecoverymanagervault - TargetResourceGroupName abc

U kunt ook Hallo na script uitvoeren. Hallo-waarden opgeven voor Hallo vereiste parameters.

    PS > .\RecoveryServicesVaultUpgrade-1.0.0.ps1
    cmdlet RecoveryServicesVaultUpgrade-1.0.0.ps1 at command pipeline position 1

    Supply values for hello following parameters:
    SubscriptionId:
    VaultName:
    Location:
    ResourceType:
    TargetResourceGroupName:

1. Hallo PowerShell-script wordt tooenter u gevraagd uw referenties. Voer deze twee keer eenmaal voor Hallo classic deployment model account en eenmaal voor hello Azure Resource Manager-account.

2. Nadat u uw referenties hebt ingevoerd, wordt in het Hallo-script een selectievakje toodetermine wordt uitgevoerd of uw Hallo infrastructuur setup voldoet aan vereisten voor het eerder opgemerkt.

3. Nadat het Hallo-vereisten zijn gecontroleerd en bevestigd, bent u na vragen aan gebruiker tooproceed Hallo kluis voortzet. Hallo-upgradeproces start een upgrade van uw kluis. Hallo volledige upgrade kunt toocomplete van 15 too30 minuten duren.

4. Nadat het Hallo-upgrade is voltooid, kunt u de bijgewerkte kluis in de nieuwe Azure portal Hallo Hallo openen.

## <a name="post-upgrade-vault-management"></a>Na de upgrade kluis management

### <a name="replicate-by-using-azure-site-recovery-in-hello-recovery-services-vault"></a>Repliceren met behulp van Azure Site Recovery in Hallo die Recovery Services-kluis

* U kunt nu uw Azure VM's beveiligen tegen tooanother één regio. Zie voor meer informatie [Azure-machines repliceren tussen regio's met Azure Site Recovery](site-recovery-azure-to-azure.md).

* Zie voor meer informatie over het repliceren van virtuele VMware-machines tooAzure [tooAzure VMware-machines repliceren met Site Recovery](vmware-walkthrough-overview.md).

* Zie voor meer informatie over het repliceren van Hyper-V-machines (zonder VMM) tooAzure [repliceren Hyper-V virtuele machines (zonder VMM) tooAzure](hyper-v-site-walkthrough-overview.md).

* Zie voor meer informatie over het repliceren van Hyper-V-machines (met VMM) tooAzure [repliceren Hyper-V virtuele machines in VMM-clouds tooAzure met Site Recovery in de Azure-portal Hallo](vmm-to-azure-walkthrough-overview.md).

* Zie voor meer informatie over Hyper-VM's (met VMM) tooa secundaire site repliceren [repliceren Hyper-V virtuele machines in VMM clouds tooa secundaire VMM site met behulp van Azure-portal Hallo](site-recovery-vmm-to-vmm.md).

* Zie voor meer informatie over het repliceren van virtuele VMware-machines tooa secundaire site [repliceren lokale virtuele VMware-machines of fysieke servers tooa secundaire site in de klassieke Azure portal Hallo](site-recovery-vmware-to-vmware.md).

### <a name="view-your-replicated-items"></a>De gerepliceerde items weergeven

Hallo toont volgende afbeelding Hallo Recovery Services-kluis dashboardpagina die belangrijke entiteiten voor Hallo kluis wordt weergegeven. selecteert u een lijst met beveiligde entiteiten in de kluis hello, tooview **siteherstel** > **gerepliceerde items**.


![Gerepliceerde items](./media/upgrade-site-recovery-vaults/replicateditems.png)

Hallo volgende afbeelding toont Hallo-werkstroom voor het weergeven van uw gerepliceerde items en Hallo **Failover** opdracht voor het initiëren van een failover.

![Gerepliceerde items](./media/upgrade-site-recovery-vaults/failover.png)

### <a name="view-your-replication-settings"></a>Replicatie-instellingen weergeven

In de Site Recovery-kluis hello, is elke beveiligingsgroep worden geconfigureerd met kopieerfrequentie, herstelpunt bewaartermijn, frequentie van toepassingsconsistente momentopnamen en andere replicatie-instellingen. In de Recovery Services-kluis hello, worden deze instellingen geconfigureerd als een beleids-replicatie. Hallo Hallo beleid is Hallo-naam van het Hallo-beveiligingsgroep of Hallo *primarycloud_Policy*.

Zie voor meer informatie over beleid voor wachtwoordreplicatie [beheren replicatiebeleid voor VMware tooAzure](site-recovery-setup-replication-settings-vmware.md).

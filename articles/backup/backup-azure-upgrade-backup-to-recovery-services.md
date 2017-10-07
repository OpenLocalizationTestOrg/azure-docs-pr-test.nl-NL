---
title: aaaUpgrade een Backup-kluis tooa Recovery Services-kluis (Preview) | Microsoft Docs
description: Instructies en ondersteuning informatie tooupgrade uw Azure Backup-kluis tooa Recovery Services-kluis.
services: backup
documentationcenter: dev-center-name
author: markgalioto
manager: carmonm
ms.assetid: 228fef19-2f6b-4067-acc3-fb6e501afb88
ms.service: backup
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 08/03/2017
ms.author: sogup;markgal;arunak
ms.openlocfilehash: 49062ca4556a009c82f143bb3a60ec71748bed01
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-a-backup-vault-tooa-recovery-services-vault"></a>Upgrade van een Backup-kluis tooa Recovery Services-kluis

Dit artikel wordt uitgelegd hoe een back-upkluis tooupgrade tooa Recovery Services-kluis. Hallo-upgradeproces heeft geen invloed op een back-uptaken en back-gegevens niet verloren. Hallo primaire redenen tooupgrade een back-up kluis tooa Recovery Services-kluis:
- Alle functies van een back-upkluis worden bewaard in een Recovery Services-kluis.
- Recovery Services-kluizen bieden meer functionaliteit dan Backup-kluizen, met inbegrip van: betere beveiliging, geïntegreerd bewaking, snellere herstelacties en herstelacties op itemniveau.
- Back-items beheren vanuit de portal voor een betere en vereenvoudigd.
- Nieuwe functies tooRecovery Services-kluizen alleen van toepassing.

## <a name="impact-toooperations-during-upgrade"></a>Impact toooperations tijdens de upgrade

Bij het bijwerken van een Backup-kluis tooa Recovery Services-kluis, zijn er geen gevolgen tooyour vlak gegevensbewerkingen. Alle back-uptaken normaal gaan en eventuele actieve hersteltaken zonder onderbreking voortgezet. Tijdens de upgrade Hallo beheerbewerkingen rekening worden gebracht een korte uitvaltijd en u kunt geen nieuwe items beveiligen of ad-hoc taken van de back-ups maken. Het herstellen van taken voor IaaS VM's uitvoeren tijdens de upgrade Hallo niet. Hallo kluis upgrade duurt onder een toocomplete uur. Eenmaal is voltooid, vervangt een Recovery Services-kluis Hallo Backup-kluis.

## <a name="changes-tooyour-automation-and-tool-after-upgrading"></a>Hulpprogramma na de upgrade en wijzigingen tooyour automation

Tijdens het voorbereiden van uw infrastructuur voor upgrade van de kluis hello, moet u uw bestaande automatisering bijwerken of tooling tooensure dat deze toowork blijft na de upgrade Hallo.
Raadpleeg Hallo PowerShell-cmdlets verwijzingen voor Hallo [Service Manager-implementatiemodel](backup-client-automation-classic.md) en Hallo [Resource Manager-implementatiemodel](backup-client-automation.md).


## <a name="before-you-upgrade"></a>Voordat u een upgrade

Controleer de volgende Hallo-problemen voordat u een upgrade uw Backup-kluizen tooRecovery Service kluizen.

- **Minimale agentversie**: tooupgrade uw kluis, zorg ervoor dat Hallo Microsoft Azure Recovery Services (MARS) agent is ten minste versie 2.0.9070.0. Als Hallo MARS-agent ouder dan 2.0.9070.0 is, moet u Hallo agent bijwerken voordat u de upgrade start Hallo.
- **Op basis van het exemplaar factureringsmodel**: Recovery Services-kluizen ondersteunen alleen facturering model Hallo op basis van het exemplaar. Als u een back-upkluis die Hallo oudere Storage gebaseerd facturering model hebt, converteren Hallo factureringsmodel tijdens de upgrade.
- **Er zijn geen bewerkingen van dagelijkse back-upconfiguratie**: tijdens de upgrade, toegang toohello management vlak is beperkt. Voltooi alle beheeracties vlak en start Hallo upgrade.

## <a name="using-powershell-scripts-tooupgrade-your-vaults"></a>Met behulp van PowerShell-scripts tooupgrade uw kluizen

PowerShell-scripts tooupgrade kunt u uw back-upkluizen tooRecovery Services-kluizen. Controleer of u hebt Hallo vereist PowerShell onderdelen tootrigger Hallo kluis upgrade. PowerShell-scripts voor de Backup-kluizen werken niet voor de Recovery Services-kluizen. Uw omgeving voorbereiden tooupgrade Hallo kluizen:

1. Installeren of upgraden [Windows Management Framework (WMF) tooversion 5](https://www.microsoft.com/download/details.aspx?id=50395) of hoger.
2. [Installeer Azure PowerShell MSI](https://github.com/Azure/azure-powershell/releases/download/v3.8.0-April2017/azure-powershell.3.8.0.msi).
3. Hallo downloaden [PowerShell-script](https://aka.ms/vaultupgradescript2) tooupgrade uw kluizen.

### <a name="run-hello-powershell-script"></a>Hallo PowerShell-script uitvoeren

Gebruik Hallo volgende script tooupgrade uw kluizen. Hallo volgende voorbeeldscript heeft uitleg van Hallo parameters.

RecoveryServicesVaultUpgrade 1.0.2.ps1 **- SubscriptionID** `<subscriptionID>` **- VaultName** `<vaultname>` **-locatie** `<location>` **- ResourceType** `BackupVault` **- TargetResourceGroupName**`<rgname>`

**SubscriptionID** -Hallo abonnement-id-nummer van Hallo kluis dat wordt bijgewerkt.<br/>
**VaultName** - hello naam van het Hallo Backup-kluis en dat wordt bijgewerkt.<br/>
**Locatie** -locatie van Hallo kluis wordt bijgewerkt.<br/>
**ResourceType** -BackupVault gebruiken.<br/>
**TargetResourceGroupName** - omdat u een upgrade Hallo kluis tooa Resource Manager gebaseerde implementatie van een resourcegroep opgeven. U kunt een bestaande resourcegroep gebruiken of een door een nieuwe naam maken. Als u de naam van een resourcegroep Hallo gespeld, kunt u een nieuwe resourcegroep kunt maken. toolearn meer informatie over resourcegroepen Lees dit [overzicht over resourcegroepen](../azure-resource-manager/resource-group-overview.md#resource-groups).

>[!NOTE]
> Namen van de resourcegroep hebben beperkingen. Worden ervoor toofollow Hallo richtlijnen; Fout toodo kan dus kluis upgrades toofail veroorzaken.
>
>

Hallo is volgende codefragment een voorbeeld van welke uw PowerShell-opdracht als eruitzien moet:

```
RecoveryServicesVaultUpgrade.ps1 -SubscriptionID 53a3c692-5283-4f0a-baf6-49412f5ebefe -VaultName "TestVault" -Location "Australia East" -ResourceType BackupVault -TargetResourceGroupName "ContosoRG"
```

U kunt ook Hallo script zonder parameters uitvoeren en wordt u gevraagd tooprovide invoer om alle vereiste parameters.

Hallo PowerShell-script wordt tooenter u gevraagd uw referenties. Voer uw referenties tweemaal: eenmaal voor Hallo Service Manager-account en een tweede keer voor Hallo Resource Manager-account.

### <a name="pre-requisites-checking"></a>Vereisten controleren
Nadat u uw Azure-referenties hebt ingevoerd, Azure wordt gecontroleerd of uw omgeving voldoet aan de vereisten volgen Hallo:

- **Minimale agentversie** -upgraden van back-up kluizen tooRecovery Services-kluizen Hallo MARS-agent toobe moet ten minste versie 2.0.9070. Als u items tooa Backup-kluis geregistreerd met een agent ouder is dan 2.0.9070, Hallo controle van vereisten mislukt. Hallo-controle mislukt, Hallo agent bijwerken als tooupgrade Hallo kluis probeer het opnieuw. U kunt de nieuwste versie Hallo van Hallo-agent van downloaden [http://download.microsoft.com/download/F/4/B/F4B06356-150F-4DB0-8AD8-95B4DB4BBF7C/MARSAgentInstaller.exe](http://download.microsoft.com/download/F/4/B/F4B06356-150F-4DB0-8AD8-95B4DB4BBF7C/MARSAgentInstaller.exe).
- **Continu configuratie taken**: als iemand taak configureren is voor een back-upkluis ingesteld toobe bijgewerkt of het registreren van een item, Hallo controle van vereisten mislukt. Hallo-configuratie voltooien of voltooien Hallo item registreren en Hallo kluis upgradeproces start.
- **Opslag op basis van een factureringsmodel**: Recovery Services-kluizen ondersteuning Hallo exemplaar, op basis van facturering model. Als u Hallo kluis upgrade uitvoert op een back-upkluis dat gebruikt Hallo facturering model op basis van opslag, kunt u na vragen aan gebruiker tooupgrade uw factureringsmodel samen met de Hallo-kluis. Anders kunt u het factureringsmodel eerst bijwerken en voer vervolgens de upgrade van Hallo-kluis.
- Identificeer een resourcegroep voor Hallo Recovery Services-kluis. tootake profiteren van Hallo Resource Manager-functies voor implementatie, moet u een Recovery Services-kluis plaatsen in een resourcegroep. Als u niet welke toouse resourcegroep weet, geeft u een naam en het Hallo-upgradeproces Hallo resourcegroep voor u gemaakt. Hallo-upgradeproces ook Hallo kluis koppelt met Hallo nieuwe resourcegroep.

Zodra het Hallo-upgradeproces is voltooid Hallo vereisten controleren, vraagt Hallo proces u toostart Hallo kluis upgrade. Nadat u hebt bevestigd, vindt het upgradeproces Hallo meestal rond toocomplete 15-20 minuten, afhankelijk van Hallo grootte van uw kluis. Als u een grote kluis hebt, kan een upgrade duren too90 minuten.

## <a name="managing-your-recovery-services-vaults"></a>Het beheren van de Recovery Services-kluizen

Hallo volgende schermen ziet u een nieuwe Recovery Services-kluis bijgewerkt van de Backup-kluis in hello Azure-portal. Hallo eerste scherm toont Hallo kluisdashboard die belangrijke entiteiten voor Hallo kluis wordt weergegeven.

![Voorbeeld van een upgrade uitgevoerd van een back-upkluis Recovery Services-kluis](./media/backup-azure-upgrade-backup-to-recovery-services/upgraded-rs-vault-in-dashboard.png)

tweede welkomstscherm toont Hallo help-koppelingen beschikbaar toohelp die u aan de slag met Hallo Recovery Services-kluis.

![Help-koppelingen in de blade snel starten Hallo](./media/backup-azure-upgrade-backup-to-recovery-services/quick-start-w-help-links.png)

## <a name="post-upgrade-steps"></a>Stappen na de upgrade
Recovery Services-kluis ondersteunt geven informatie over de tijdzone in de back-upbeleid. Nadat de kluis upgrade is voltooid, gaat tooBackup beleidsregels in kluis-instellingen en Hallo tijdzone-informatie voor elke Hallo beleid dat is geconfigureerd in de kluis Hallo bijwerken. Dit scherm toont al Hallo back-upschema tijd is opgegeven als per lokale tijdzone die wordt gebruikt wanneer u beleid hebt gemaakt. 

## <a name="enhanced-security"></a>Verbeterde beveiliging

Wanneer een back-upkluis geüpdatet tooa Recovery Services-kluis, Hallo beveiligingsinstellingen voor de kluis die automatisch zijn ingeschakeld. Wanneer Hallo beveiligingsinstellingen op bepaalde bewerkingen zoals het verwijderen van de back-ups, of het wijzigen van een wachtwoordzin vereist een [Azure multi-factor Authentication](../multi-factor-authentication/multi-factor-authentication.md) PINCODE. Zie voor meer informatie over de Hallo verbeterde beveiliging Hallo artikel [tooprotect hybride back-ups van beveiligingsfuncties](backup-azure-security-feature.md). 

Wanneer Hallo verbeterde beveiliging is ingeschakeld, wordt too14 dagen nadat de herstelgegevens punt Hallo is verwijderd uit de kluis Hallo gegevens bewaard. Klanten wordt gefactureerd voor opslag van deze beveiligingsgegevens. Bewaren van gegevens voor beveiliging is van toepassing toorecovery punten voor hello Azure backup-agent, Azure Backup-Server en System Center Data Protection Manager. 

## <a name="gather-data-on-your-vault"></a>Gegevens verzamelen over uw kluis

Na de upgrade van de Recovery Services-kluis tooa rapporten configureren voor Azure Backup (voor IaaS VM's en Microsoft Azure Recovery Services (MARS)) en gebruik van Power BI tooaccess Hallo-rapporten. Zie voor meer informatie over het verzamelen van gegevens Hallo artikel [Azure Backup configureren rapporten](backup-azure-configure-reports.md).

## <a name="frequently-asked-questions"></a>Veelgestelde vragen

**Hallo upgrade-abonnement invloed heeft op Mijn lopende back-ups?**</br>
Nee. Uw actieve back-ups niet wordt onderbroken tijdens en na de upgrade.

**Als ik niet van plan bent over het upgraden van snel, maar wat gebeurt er toomy kluizen?**</br>
Omdat alle functies van de nieuwe toepassing alleen tooRecovery Services-kluizen, wij raden ten zeerste tooupgrade u uw kluizen. Microsoft zal uiteindelijk afschaffen Hallo klassieke portal. Vanaf 1 September 2017 Microsoft gaat verder met het upgraden van automatische back-upkluizen tooRecovery Services-kluizen. Per 1 November 2017 voltooit Microsoft hello upgradeproces. Uw kluis kan automatisch worden bijgewerkt tijdens September of oktober. Microsoft raadt dat u uw kluis zo snel mogelijk bijwerken.

**Wat houdt de upgrade voor mijn bestaande tooling?**</br>
Werk uw tooling toohello Resource Manager-implementatiemodel. Recovery Services-kluizen zijn gemaakt voor gebruik in Hallo Resource Manager-implementatiemodel. Planning voor Hallo Resource Manager-implementatiemodel en accounting voor Hallo verschil in uw kluizen zijn belangrijk. 

**Tijdens het Hallo-upgrade is er veel uitvaltijd?**</br>
Dit is afhankelijk van Hallo aantal resources die wordt bijgewerkt. Hallo hele upgrade moet minder dan 20 minuten duren voordat voor kleinere implementaties (enkele tientallen van beveiligde instanties). Voor grotere implementaties moet het maximaal een uur duren.

**Kan ik terugdraaien na de upgrade?**</br>
Nee. Terugdraaien wordt niet ondersteund nadat Hallo resources hebt geüpgraded.

**Kan ik mijn abonnement of resources toosee valideren als ze geschikt is voor upgrade?**</br>
Ja. Hallo eerste stap bij een upgrade wordt gevalideerd of Hallo resources kunnen van upgrade. Indien Hallo validatie van vereisten mislukt, kunt u berichten ontvangen alle Hallo redenen Hallo upgrade kan niet worden voltooid.

**Welke machtigingen moet ik heb tootrigger kluis upgrade?**</br>
tooperform hello vault upgrade, moet u toegevoegd als medebeheerder voor Hallo-abonnement in Hallo klassieke Azure-portal. Dit is vereist, zelfs als u al als eigenaar in hello Azure-portal worden weergegeven. Probeer tooadd medebeheerder voor Hallo-abonnement in Azure classic portal toofind uit als u medebeheerder voor Hallo-abonnement. Als u niet kunt tooadd medebeheerder, moet u contact op met een servicebeheerder of medebeheerder voor Hallo-abonnement, die u als medebeheerder toevoegen kunt.

**Kan ik mijn back-up op basis van een CSP-kluis bijwerken?**</br>
Nee. U kunt back-upkluizen op basis van een CSP op dit moment niet upgraden. Er wordt ondersteuning voor het upgraden van de CSP gebaseerde Backup-kluizen in de volgende versies Hallo toevoegen.

**Kan ik mijn klassieke kluis na het bijwerken weergeven?**</br>
Nee. U kunt weergeven of beheren van uw klassieke kluis na het bijwerken. U kunt toouse Hallo nieuwe Azure-portal voor alle acties op Hallo kluis alleen worden.

**De upgrade is mislukt, maar Hallo-machine die vastgehouden Hallo-agent die niet meer bijgewerkt, bestaat. Wat moet ik doen in dat geval**</br>
Als u toouse Hallo store moet, Hallo back-ups van deze computer voor lange bewaartermijn, dan hebt u niet meer worden kunnen tooupgrade Hallo kluis. In toekomstige releases voegt ondersteuning voor het upgraden van een dergelijke kluis toe.
Als u geen toostore Hallo back-ups van deze machine hoeft meer en neem deze machine uit kluis Hallo registratie en Hallo upgrade opnieuw.

**Waarom zie ik niet Hallo taken informatie voor mijn lokale bronnen na de upgrade**</br>
Bewaking voor lokale back-ups (MARS-agent, DPM en de Azure Backup-Server) is een nieuwe functie die u krijgt wanneer u een upgrade uitvoert van uw Backup-kluis tooRecovery Services-kluis. Hallo controlegegevens neemt too12 uren toosync met Hallo-service.

**Hoe kan ik een probleem melden?**</br>
Als een gedeelte van de kluis Hallo upgrade mislukt, opmerking Hallo OperationId Hallo fout vermeld. Microsoft Support werkt proactief tooresolve Hallo probleem. U kunt bereiken tooSupport of een e-mail sturen naar rsvaultupgrade@service.microsoft.com met uw abonnements-ID, de kluisnaam van de en OperationId. Zo spoedig mogelijk zullen we tooresolve Hallo probleem proberen. Probeer de bewerking Hallo niet opnieuw tenzij expliciet toodo zo is door Microsoft.


## <a name="next-steps"></a>Volgende stappen
Hallo volgende artikel om te gebruiken:</br>
[Back-up van een IaaS VM](backup-azure-arm-vms-prepare.md)</br>
[Back-up van een Azure Backup-Server](backup-azure-microsoft-azure-backup.md)</br>
[Maak een back-up van een Windows-Server](backup-configure-vault.md).

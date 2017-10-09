---
title: aaaSAP HANA Azure back-up op basis van opslag-momentopnamen | Microsoft Docs
description: Er zijn twee primaire back-mogelijkheden voor SAP HANA op virtuele machines in Azure, in dit artikel bevat informatie over SAP HANA-back-up op basis van opslag-momentopnamen
services: virtual-machines-linux
documentationcenter: 
author: hermanndms
manager: timlt
editor: 
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ums.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 3/13/2017
ms.author: rclaus
ms.openlocfilehash: 32bb80f5a928a2cf63699bfe4f4cf5bbad81e6fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="sap-hana-backup-based-on-storage-snapshots"></a>Back-up van SAP HANA op basis van opslagmomentopnamen

## <a name="introduction"></a>Inleiding

Dit maakt deel uit van een reeks drie delen met verwante artikelen op SAP HANA back-up. [Back-handleiding voor SAP HANA op Azure Virtual Machines](sap-hana-backup-guide.md) biedt een overzicht en informatie over het aan de slag, en [SAP HANA Azure Backup op bestandsniveau](sap-hana-backup-file-level.md) dekt Hallo optie back-up op basis van bestanden.

Wanneer u een VM-back-upfunctie voor een single instance alles in één demo-systeem, moet een rekening houden met een VM-back-in plaats van het beheren van HANA back-ups op Hallo OS niveau doen. Een alternatief is tootake Azure blob momentopnamen toocreate kopieën van afzonderlijke virtuele schijven die zijn aangesloten tooa virtuele machine en Hallo HANA gegevensbestanden bewaren. Maar een kritiek punt app consistentie bij het maken van een VM-momentopname voor back-up of schijf tijdens het Hallo-systeem actief is en actief is. Zie _SAP HANA gegevensconsistentie bij het maken van opslag-momentopnamen_ in de bijbehorende artikel Hallo [back-up-handleiding voor SAP HANA op Azure Virtual Machines](sap-hana-backup-guide.md). SAP HANA bevat een functie die ondersteuning biedt voor dit soort opslag-momentopnamen.

## <a name="sap-hana-snapshots"></a>SAP HANA-momentopnamen

Er is een functie in SAP HANA die ondersteuning biedt voor maken van een momentopname van de opslag. Vanaf December 2016 is er echter een beperking toosingle-container systemen. Multitenant container configuraties bieden geen ondersteuning voor dit soort databasemomentopname (Zie [momentopname maken van een opslaggroep (SAP HANA Studio)](https://help.sap.com/saphelp_hanaplatform/helpdata/en/a0/3f8f08501e44d89115db3c5aa08e3f/content.htm)).

Dit werkt als volgt:

- Voorbereiden van een momentopname van de opslag via Hallo SAP HANA momentopname initiëren
- Hallo opslag momentopname (Azure blob momentopname bijvoorbeeld) uitvoert
- Hallo SAP HANA momentopname bevestigen

![Deze schermafbeelding ziet u dat de momentopname van een SAP HANA-gegevens kan worden gemaakt via een SQL-instructie](media/sap-hana-backup-storage-snapshots/image011.png)

Deze schermafbeelding ziet u dat de momentopname van een SAP HANA-gegevens kan worden gemaakt via een SQL-instructie.

![Hallo vervolgens een momentopname wordt ook weergegeven in de back-upcatalogus Hallo in SAP HANA-Studio](media/sap-hana-backup-storage-snapshots/image012.png)

Hallo vervolgens een momentopname wordt ook weergegeven in de back-upcatalogus Hallo in SAP HANA Studio.

![Op de schijf, Hallo momentopname wordt weergegeven in Hallo SAP HANA-gegevensmap](media/sap-hana-backup-storage-snapshots/image013.png)

Op de schijf, Hallo momentopname wordt weergegeven in Hallo SAP HANA-gegevensmap.

Een heeft tooensure die Hallo consistentie van het bestandssysteem ook voordat Hallo opslag momentopname worden uitgevoerd terwijl een SAP HANA Hallo momentopname voorbereidingsmodus wordt gegarandeerd. Zie _SAP HANA gegevensconsistentie bij het maken van opslag-momentopnamen_ in de bijbehorende artikel Hallo [back-up-handleiding voor SAP HANA op Azure Virtual Machines](sap-hana-backup-guide.md).

Als Hallo opslag momentopname is voltooid, gaat het kritieke tooconfirm Hallo SAP HANA-momentopname. Er is een bijbehorende SQL-instructie toorun: sluiten MOMENTOPNAME van de gegevens back-up (Zie [gegevens sluiten MOMENTOPNAME instructie BACKUP (back-up en herstel)](https://help.sap.com/saphelp_hanaplatform/helpdata/en/c3/9739966f7f4bd5818769ad4ce6a7f8/content.htm)).

> [!IMPORTANT]
> Bevestig Hallo HANA momentopname. Vervaldatum te&quot;kopiëren bij schrijven&quot; SAP HANA mogelijk extra schijfruimte in momentopname-voorbereiden modus en is niet mogelijk toostart nieuwe back-ups tot Hallo SAP HANA momentopname is bevestigd.

## <a name="hana-vm-backup-via-azure-backup-service"></a>HANA VM back-ups via Azure Backup-service

Vanaf December 2016, zijn de back-upagent Hallo Hallo Azure Backup-service is niet beschikbaar voor virtuele Linux-machines. toomake gebruik van Azure backup op Hallo bestand/map niveau, zou een SAP HANA back-upbestanden tooa Windows VM kopiëren en gebruik vervolgens Hallo backup-agent. Anders wordt is alleen een volledige Linux VM back-up mogelijk via hello Azure Backup-service. Zie [overzicht van Hallo functies in Azure Backup](../../../backup/backup-introduction-to-azure-backup.md) toofind meer informatie.

Hello Azure Backup-service biedt een optie tooback up en herstel van een virtuele machine. Meer informatie over deze service en hoe het werkt vindt u in het artikel Hallo [plannen van uw back-infrastructuur van de virtuele machine in Azure](../../../backup/backup-azure-vms-introduction.md).

Er zijn twee belangrijke overwegingen volgens toothat artikel:

_&quot;Voor virtuele Linux-machines zijn alleen bestandsconsistente back-ups mogelijk, aangezien Linux geen een tooVSS gelijkwaardige platform.&quot;_

_&quot;Toepassingen tooimplement moeten hun eigen &quot;-reparatietabel&quot; mechanisme op Hallo gegevens hebt hersteld.&quot;_

Daarom heeft een toomake of SAP HANA in een consistente status op de schijf wanneer Hallo back-up wordt gestart. Zie _SAP HANA momentopnamen_ eerder in Hallo document beschreven. Maar er is een mogelijk probleem wanneer SAP HANA in deze momentopname voorbereiding-modus blijft. Zie [momentopname maken van een opslaggroep (SAP HANA Studio)](https://help.sap.com/saphelp_hanaplatform/helpdata/en/a0/3f8f08501e44d89115db3c5aa08e3f/content.htm) voor meer informatie.

Dit artikel staat:

_&quot;Het is raadzaam tooconfirm of zo snel mogelijk een opslag-momentopnamen afbreken nadat deze is gemaakt. Tijdens het Hallo opslag momentopname wordt voorbereid of gemaakt, Hallo is momentopname relevante gegevens geblokkeerd. Terwijl de momentopname-relevante gegevens Hallo bevroren blijft, kunnen nog steeds wijzigingen worden aangebracht in Hallo-database. Dergelijke wijzigingen leidt niet tot Hallo bevroren momentopname relevante gegevens toobe gewijzigd. In plaats daarvan worden Hallo wijzigingen toopositions geschreven in Hallo gegevensgebied die gescheiden zijn van Hallo opslag momentopname. Wijzigingen zijn ook toohello logboek geschreven. Echter Hallo langer Hallo momentopname relevante gegevens bevroren wordt bewaard, Hallo meer Hallo gegevensvolume op dat kan worden uitgebreid.&quot;_

Azure back-up zorgt voor consistentie van het bestandssysteem Hallo via Azure VM-extensies. Deze uitbreidingen zijn niet beschikbaar zelfstandige en werkt alleen in combinatie met Azure Backup-service. Het is echter nog steeds een vereiste toomanage een SAP HANA momentopname tooguarantee app consistentie.

Azure Backup bestaat uit twee belangrijke fasen:

- Momentopname
- Overdracht van gegevens toovault

Nadat de hello Azure Backup-service-fase van het maken van een momentopname is voltooid, kan dus een Hallo SAP HANA-momentopname bevestigen. Het duurt enkele minuten toosee in hello Azure-portal.

![Deze afbeelding ziet u deel van de lijst met de Hallo back-uptaak van een Azure Backup-service](media/sap-hana-backup-storage-snapshots/image014.png)

Deze afbeelding ziet u onderdeel van Hallo back-uptaak lijst met een Azure Backup-service, die gebruikt tooback up Hallo HANA test-VM is.

![taakdetails tooshow hello, klikt u op back-uptaak Hallo in hello Azure-portal](media/sap-hana-backup-storage-snapshots/image015.png)

taakdetails tooshow hello, klikt u op back-uptaak Hallo in hello Azure-portal. Hier kunt zien Hallo twee fasen. Het duurt enkele minuten totdat er Hallo momentopname fase wordt weergegeven als voltooid. Meestal zijn Hallo is besteed in Hallo gegevensoverdracht fase.

## <a name="hana-vm-backup-automation-via-azure-backup-service"></a>Back-automatisering HANA VM via Azure Backup-service

Een kan Hallo SAP HANA momentopname handmatig bevestigen zodra hello Azure Backup momentopname fase is voltooid, zoals eerder beschreven, maar het is nuttig tooconsider automation omdat een beheerder niet Hallo back-uptaak lijst in hello Azure-portal bewaakt mogelijk.

Hier volgt een uitleg hoe deze kan worden bereikt via Azure PowerShell-cmdlets.

![Een Azure Backup-service is gemaakt met de naam Hallo hana-backup-kluis](media/sap-hana-backup-storage-snapshots/image016.png)

Een Azure Backup-service is gemaakt met de naam van de Hallo &quot;hana-back-up-kluis.&quot; Hallo PS-opdracht **Get-AzureRmRecoveryServicesVault-naam hana-backup-kluis** haalt Hallo bijbehorende object. Dit object zich bevindt, wordt het gebruikte tooset Hallo back-context weergegeven op de volgende figuur Hallo.

![Een kunt controleren of de back-uptaak Hallo momenteel bezig](media/sap-hana-backup-storage-snapshots/image017.png)

Na de juiste context instelling hello, kan een controleren voor de back-uptaak Hallo momenteel bezig en zoekt u de taakdetails. Hallo subtaak lijst bevat als Hallo momentopname fase waarin hello Azure back-uptaak al is voltooid:

```
$ars = Get-AzureRmRecoveryServicesVault -Name hana-backup-vault
Set-AzureRmRecoveryServicesVaultContext -Vault $ars
$jid = Get-AzureRmRecoveryServicesBackupJob -Status InProgress | select -ExpandProperty jobid
Get-AzureRmRecoveryServicesBackupJobDetails -Jobid $jid | select -ExpandProperty subtasks
```

![Poll Hallo waarde in een lus tot tooCompleted](media/sap-hana-backup-storage-snapshots/image018.png)

Zodra de taakdetails Hallo zijn opgeslagen in een variabele, is gewoon PS syntaxis tooget toohello eerste matrixvermelding en Hallo statuswaarde wordt opgehaald. toocomplete hello automatiseringsscript poll Hallo waarde in een lus totdat het schakelt te&quot;voltooid.&quot;

```
$st = Get-AzureRmRecoveryServicesBackupJobDetails -Jobid $jid | select -ExpandProperty subtasks
$st[0] | select -ExpandProperty status
```

## <a name="hana-license-key-and-vm-restore-via-azure-backup-service"></a>De licentiesleutel HANA en VM herstellen via de Azure Backup-service

Hello Azure Backup-service is ontworpen toocreate een nieuwe virtuele machine tijdens het terugzetten. Er is geen juiste nu toodo een &quot;in-place&quot; terugzetten van een bestaande virtuele machine in Azure.

![Deze afbeelding ziet u de hersteloptie Hallo Hallo Azure-service in hello Azure-portal](media/sap-hana-backup-storage-snapshots/image019.png)

Deze afbeelding ziet de hersteloptie Hallo Hallo Azure-service in hello Azure-portal. Een kunt kiezen tussen het maken van een virtuele machine tijdens het terugzetten of het herstellen van Hallo-schijven. Na het terugzetten van Hallo schijven is het nog steeds nodig toocreate een nieuwe virtuele machine toe. Wanneer een nieuwe virtuele machine wordt gemaakt op Azure Hallo unieke ID van VM-wijzigingen (Zie [toegang tot en met behulp van Azure VM unieke ID](https://azure.microsoft.com/blog/accessing-and-using-azure-vm-unique-id/)).

![Deze afbeelding ziet u hello Azure VM unieke ID voor en na Hallo herstellen via de Azure Backup-service](media/sap-hana-backup-storage-snapshots/image020.png)

Deze afbeelding ziet u hello Azure VM unieke ID voor en na Hallo herstellen via de Azure Backup-service. Hallo SAP hardwaresleutel, die wordt gebruikt voor SAP-licentieverlening, met behulp van deze unieke id voor de virtuele machine. Als gevolg hiervan is een nieuwe SAP-licentie toobe na het terugzetten van een virtuele machine is geïnstalleerd.

Een nieuwe Azure Backup-functie is opgenomen in de voorbeeldmodus tijdens het maken van deze back-handleiding Hallo. Kunt u een bestand niveau te herstellen op basis van Hallo VM-momentopname die is uitgevoerd voor Hallo VM back-up. Hiermee voorkomt u Hallo nodig toodeploy een nieuwe virtuele machine, en daarom Hallo unieke ID van VM blijft Hallo dezelfde en geen nieuwe sleutel voor SAP HANA-licentie is vereist. Meer documentatie over deze functie wordt worden opgegeven nadat het volledig is getest.

Azure Backup wordt uiteindelijk back-up van afzonderlijke Azure virtuele schijven toestaan, plus de bestanden en mappen uit binnen Hallo VM. Een belangrijk voordeel van Azure Backup is het beheer van alle Hallo back-ups opslaan Hallo klant opheft toodo deze. Als een herstelbewerking niet meer nodig, wordt Azure Backup geselecteerd Hallo juiste back-toouse.

## <a name="sap-hana-vm-backup-via-manual-disk-snapshot"></a>SAP HANA VM back-ups via handmatige schijf momentopname

In plaats van hello Azure Backup-service, kan een een afzonderlijke back-upoplossing configureren door het maken van momentopnamen van de blob van Azure VHD's handmatig via PowerShell. Zie [Using blob momentopnamen met PowerShell](https://blogs.msdn.microsoft.com/cie/2016/05/17/using-blob-snapshots-with-powershell/) voor een beschrijving van Hallo stappen.

Biedt meer flexibiliteit, maar Hallo problemen beschreven eerder in dit document kan niet worden omgezet:

- Een moet nog steeds ervoor zorgen dat de SAP HANA zich in een consistente status
- Hallo besturingssysteemschijf kan niet worden overschreven, zelfs als Hallo die VM toewijzing ongedaan wordt gemaakt vanwege een fout met de mededeling dat een lease bestaat. Deze functie werkt alleen nadat het verwijderen van virtuele machine, waardoor tooa nieuwe unieke ID van de virtuele machine en Hallo nodig tooinstall een nieuwe SAP-licentie Hallo.

![Het is mogelijk toorestore alleen Hallo gegevensschijven van een Azure VM](media/sap-hana-backup-storage-snapshots/image021.png)

Het is mogelijk toorestore alleen gegevensschijven Hallo van een virtuele machine van Azure, Hallo probleem van het ophalen van een nieuwe unieke ID voor VM vermijden en daarom ongeldig Hallo SAP licentie:

- Hallo-test twee Azure gegevensschijven zijn aangesloten tooa VM en software-RAID boven op ze is gedefinieerd 
- Is bevestigd dat SAP HANA in een consistente status door de functie voor SAP HANA-momentopname
- Bestandssysteem blokkeren (Zie _SAP HANA gegevensconsistentie bij het maken van opslag-momentopnamen_ in de bijbehorende artikel Hallo [back-up-handleiding voor SAP HANA op Azure Virtual Machines](sap-hana-backup-guide.md))
- BLOB momentopnamen zijn vanaf beide gegevensschijven
- Bestandssysteem blokkering opheffen
- Bevestiging voor SAP HANA-momentopname
- gegevensschijven toorestore hello, Hallo VM is afgesloten en beide schijven losgekoppeld
- Na het loskoppelen van Hallo schijven zijn ze overschreven met Hallo voormalige blob momentopnamen
- Vervolgens Hallo hersteld virtuele schijven die zijn gekoppeld opnieuw toohello VM
- Nadat de momentopname begin Hallo VM alles op Hallo software RAID prima en terug toohello blob is ingesteld
- HANA is terug toohello HANA momentopname ingesteld

Als deze mogelijk tooshut omlaag SAP HANA voordat Hallo blob momentopnamen, zou Hallo procedure minder complex zijn. In dat geval kan een Hallo HANA momentopname overslaan en als niets in Hallo-systeem gebeurt er, ook Hallo bestand system bevriezing overslaan. Extra complexiteit wordt geleverd in Hallo afbeelding wanneer deze nodig toodo momentopnamen terwijl alles online is. Zie _SAP HANA gegevensconsistentie bij het maken van opslag-momentopnamen_ in de bijbehorende artikel Hallo [back-up-handleiding voor SAP HANA op Azure Virtual Machines](sap-hana-backup-guide.md).

## <a name="next-steps"></a>Volgende stappen
* [Back-handleiding voor SAP HANA op Azure Virtual Machines](sap-hana-backup-guide.md) biedt een overzicht en informatie over aan de slag.
* [SAP HANA back-up die is gebaseerd op bestandsniveau](sap-hana-backup-file-level.md) dekt Hallo optie back-up op basis van bestanden.
* hoe tooestablish hoge beschikbaarheid en herstel na noodgevallen van SAP HANA plannen in Azure (grote exemplaren), Zie toolearn [SAP HANA (grote exemplaren) hoge beschikbaarheid en herstel na noodgevallen op Azure](hana-overview-high-availability-disaster-recovery.md).

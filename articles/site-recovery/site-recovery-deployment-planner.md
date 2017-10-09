---
title: aaaAzure Site Recovery-implementatie plannen voor VMware naar Azure | Microsoft Docs
description: Dit is de planner gebruikershandleiding voor hello Azure Site Recovery-implementatie.
services: site-recovery
documentationcenter: 
author: nsoneji
manager: garavd
editor: 
ms.assetid: 
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 08/28/2017
ms.author: nisoneji
ms.openlocfilehash: a8c13cd47850575769e0186528807bc525bdeec7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-site-recovery-deployment-planner"></a>Azure Site Recovery-implementatieplanner
Dit artikel is hello Azure Site Recovery implementatie Planner gebruikershandleiding voor de productie-implementaties van VMware naar Azure.

## <a name="overview"></a>Overzicht

Voordat u begint met het beveiligen van een virtuele VMware-machines (VM's) met behulp van Site Recovery, voldoende bandbreedte toewijzen op basis van uw dagelijkse gegevens wijzigen, toomeet uw gewenste beoogd herstelpunt (RPO). Ervoor toodeploy Hallo juiste aantal configuratieservers en proces servers on-premises worden.

U moet ook toocreate Hallo juiste type en aantal doel-Azure storage-accounts. U kunt kiezen tussen Standard- of Premium Storage-accounts, waarbij u rekening moet houden met groei van uw productieservers door toegenomen gebruik na verloop van tijd. U kiest Hallo opslagtype per virtuele machine, op basis van kenmerken werkbelasting (bijvoorbeeld lezen/schrijven bewerkingen per seconde (IOPS)] of gegevensverloop) en siteherstel beperkt.

Hallo Site Recovery implementatie planner openbare preview is een opdrachtregelprogramma dat is momenteel alleen beschikbaar voor Hallo VMware naar Azure scenario. U kunt op afstand profiel van uw virtuele VMware-machines met behulp van dit hulpprogramma (met zonder productie impact beeïndigen) toounderstand Hallo bandbreedte en Azure Storage-vereisten voor geslaagde replicatie en failover testen. U kunt Hallo hulpprogramma uitvoeren zonder dat u een Site Recovery-onderdelen op lokale installeert. Echter tooget nauwkeurige doorvoerresultaten bereikt, wordt aangeraden Hallo planner uit te voeren op een Windows-Server die voldoet aan Hallo minimale vereisten van Site Recovery-configuratieserver Hallo dat u uiteindelijk toodeploy als een van de eerste stappen Hallo moet zou in productie-implementatie.

Hallo hulpprogramma biedt Hallo volgende details:

**Beoordeling van compatibiliteit**

* Beoordeling van geschiktheid van een VM op basis van het aantal schijven, schijfgrootte, IOPS, verloop en opstarttype (EFI/BIOS)
* Hallo geschatte netwerkbandbreedte die zijn voor replicatie van verschillen vereist

**Vereiste netwerkbandbreedte versus RPO-evaluatie**

* Hallo geschatte netwerkbandbreedte die zijn voor replicatie van verschillen vereist
* Hallo-doorvoer die Site Recovery uit lokale tooAzure ophalen kunt
* aantal virtuele machines toobatch, op basis van Hallo Hallo geschatte bandbreedte toocomplete initiële replicatie in een bepaalde tijd

**Vereisten voor Azure-infrastructuur**

* Hallo opslagvereisten type (standard of premium storage-account) voor elke virtuele machine
* Totaal aantal standard en premium storage-accounts toobe ingesteld voor replicatie Hallo
* Suggesties voor naamgeving van opslagaccounts op basis van Azure Storage-richtlijnen
* Hallo-opslagaccount plaatsing voor alle virtuele machines
* Hallo aantal Azure kernen toobe instellen voordat de testfailover of failover op Hallo-abonnement
* Hello Azure VM aanbevolen grootte voor elke lokale VM

**On-premises infrastructuurvereisten**
* Hallo het vereiste aantal configuratieservers en proces servers toobe lokale geïmplementeerd

>[!IMPORTANT]
>
>Omdat informatie over het gebruik waarschijnlijk tooincrease gedurende een bepaalde periode, alle voorgaande hulpprogramma berekeningen worden uitgevoerd, ervan uitgaande dat een factor van 30 procent groei in kenmerken werkbelasting en het gebruik van een 95e percentielwaarde van alle Hallo profilering metrische gegevens Hallo (lezen/schrijven IOP's, verloop, en kan dus vermeld). Beide elementen (groeifactor en percentielberekening) kunnen worden geconfigureerd. toolearn meer informatie over de groeifactor, Zie Hallo 'groeifactor overwegingen' sectie. toolearn meer informatie over de percentielwaarde, Zie Hallo 'Percentielwaarde gebruikt voor de berekening Hallo' sectie.
>

## <a name="requirements"></a>Vereisten
Hallo hulpprogramma heeft twee belangrijke fasen: profileren van en rapportage. Er is ook een derde optie toocalculate doorvoer alleen. Hallo-vereisten voor Hallo-server van welke Hallo profilering en doorvoer meting wordt geïnitieerd worden weergegeven in de volgende tabel Hallo:

| Serververeiste | Beschrijving|
|---|---|
|Profileren en meten van doorvoer| <ul><li>Besturingssysteem: Microsoft Windows Server 2012 R2<br>(in het ideale geval die overeenkomt met ten minste Hallo [grootte aanbevelingen voor de configuratieserver Hallo](https://aka.ms/asr-v2a-on-prem-components))</li><li>Machineconfiguratie: 8 vCPU's, 16 GB RAM, 300 GB harde schijf</li><li>[Microsoft .NET Framework 4.5](https://aka.ms/dotnet-framework-45)</li><li>[VMware vSphere PowerCLI 6.0 R3](https://aka.ms/download_powercli)</li><li>[Microsoft Visual C++ Redistributable voor Visual Studio 2012](https://aka.ms/vcplusplus-redistributable)</li><li>Internet toegang tooAzure van deze server</li><li>Azure Storage-account</li><li>Beheerderstoegang op Hallo-server</li><li>Minimaal 100 GB vrije schijfruimte (uitgaande van 1000 virtuele machines met een gemiddelde van elk drie schijven, geprofileerd voor 30 dagen)</li><li>VMware vCenter statistieken-instellingen moeten worden ingesteld too2 of hoog niveau</li><li>Poort 443 toestaan: ASR implementatie Planner gebruikt deze poort tooconnect toovCenter server/ESXi-host</ul></ul>|
| Rapporten genereren | Een Windows-pc of Windows-server met Microsoft Excel 2013 of hoger |
| Gebruikersmachtigingen | Alleen-lezen-machtiging voor Hallo-gebruikersaccount dat tooaccess Hallo VMware vCenter server/VMware vSphere ESXi-host heeft gebruikt tijdens het samenstellen van profiel |

> [!NOTE]
>
>Hallo-hulpprogramma kan alleen virtuele machines met VMDK- en RDM schijven profiel. Profilering van virtuele machines met iSCSI- of NFS-schijven is niet mogelijk. Site Recovery biedt ondersteuning voor iSCSI en NFS-schijven voor VMware-servers maar Hallo implementatie planner is niet binnen Hallo gastbesturingssysteem en deze profielen alleen met behulp van de vCenter-prestatiemeteritems, Hallo hulpprogramma heeft geen zichtbaarheid van deze schijftypen.
>

## <a name="download-and-extract-hello-public-preview"></a>Downloaden en uitpakken van Hallo openbare preview
1. Download de nieuwste versie Hallo Hallo [openbare preview van Site Recovery implementatie planner](https://aka.ms/asr-deployment-planner).  
Hallo-hulpprogramma wordt verpakt in een map .zip. Hallo huidige versie van Hallo hulpprogramma ondersteunt alleen Hallo VMware naar Azure scenario.

2. Hallo .zip map toohello WindowsServer van waaruit u toorun Hallo hulpprogramma wilt kopiëren.  
U kunt Hallo hulpprogramma uitvoeren vanaf Windows Server 2012 R2 als Hallo-server heeft toegang tooconnect toohello vCenter-server/vSphere ESXi netwerkhost die Hallo VMs toobe profiel bevat. We raden u echter aan Hallo hulpprogramma uit te voeren op een server waarvan de hardwareconfiguratie voldoet aan Hallo [configuratie server sizing richtlijn](https://aka.ms/asr-v2a-on-prem-components). Als u Site Recovery-onderdelen op de lokale al hebt geïmplementeerd, kunt u de Hallo hulpprogramma uitvoeren vanaf de configuratieserver Hallo.

 We raden u aan Hallo dezelfde hardwareconfiguratie als Hallo configuratieserver (die een ingebouwde processerver heeft) op Hallo-server waarop u Hallo hulpprogramma uitvoert. Een dergelijke configuratie zorgt ervoor dat doorvoer Hallo bereikt die Hallo hulpprogramma rapporten komt overeen met Hallo werkelijke doorvoer die Site Recovery tijdens de replicatie bereiken kunt. Hallo doorvoer berekening, is afhankelijk van de beschikbare netwerkbandbreedte op Hallo-server en de hardwareconfiguratie van de server hello (CPU, opslag, enzovoort). Als u Hallo hulpprogramma vanaf een andere server uitvoeren, worden Hallo doorvoer wordt berekend op basis van die server tooMicrosoft Azure. Ook, omdat de hardwareconfiguratie Hallo van server Hallo van die van de configuratieserver Hallo afwijken, Hallo bereikt doorvoer die Hallo hulpprogramma rapporten is mogelijk onnauwkeurig.

3. Pak de map .zip Hallo.  
Hallo-map bevat meerdere bestanden en submappen. Hallo uitvoerbare bestand is ASRDeploymentPlanner.exe in Hallo bovenliggende map.

    Voorbeeld:  
    Hallo ZIP-bestand tooE kopiëren: \ station en pak het bestand.
   E:\ASR Deployment Planner-Preview_v1.2.zip

    E:\ASR Deployment Planner-Preview_v1.2\ ASR Deployment Planner-Preview_v1.2\ ASRDeploymentPlanner.exe

## <a name="capabilities"></a>Functionaliteit
Hallo-opdrachtregelprogramma (ASRDeploymentPlanner.exe) kunt u in een van drie beschikbare modi na Hallo uitvoeren:

1. Profileren  
2. Rapporten genereren
3. Doorvoer bepalen

Voer eerst Hallo hulpprogramma in de modus toogather VM gegevensverloop en IOPS-profilering. Voer Hallo hulpprogramma toogenerate Hallo rapport toofind Hallo bandbreedte en opslag netwerkvereisten.

## <a name="profiling"></a>Profileren
In de modus profilering verbindt Hallo planner implementatieprogramma toohello vCenter-server/vSphere ESXi-host toocollect prestatiegegevens over Hallo VM.

* Profileren van heeft geen invloed op prestaties Hallo Hallo productie virtuele machines, omdat er geen rechtstreekse verbinding toothem wordt gemaakt. Alle prestatiegegevens worden verzameld uit Hallo vCenter server vSphere/ESXi-host.
* tooensure dat er een te verwaarlozen invloed op Hallo server is vanwege profilering, Hallo hulpprogramma query's Hallo vCenter server vSphere/ESXi-host om de 15 minuten. Deze query-interval niet in gevaar brengt profilering nauwkeurigheid omdat Hallo hulpprogramma elke minuut prestatiemeteritem-gegevens worden opgeslagen.

### <a name="create-a-list-of-vms-tooprofile"></a>Een lijst met virtuele machines tooprofile maken
Eerst moet u een lijst met Hallo VMs toobe profiling wordt gestart. U krijgt alle Hallo namen van virtuele machines op een vCenter-server/vSphere ESXi-host via Hallo VMware vSphere PowerCLI opdrachten in Hallo procedure te volgen. U kunt ook kunt u weergeven in een bestand Hallo beschrijvende namen of IP-adressen van virtuele machines dat u wilt dat tooprofile handmatig Hallo.

1. Meld u aan toohello die VMware vSphere PowerCLI is geïnstalleerd in de VM.
2. Open de Hallo VMware vSphere PowerCLI console.
3. Zorg ervoor dat het uitvoeringsbeleid Hallo is ingeschakeld voor Hallo-script. Als deze is uitgeschakeld, start Hallo VMware vSphere PowerCLI console in de beheerdersmodus en vervolgens door het uitvoeren van de volgende opdracht Hallo in te schakelen:

            Set-ExecutionPolicy –ExecutionPolicy AllSigned

4. U kunt optionly nodig toorun Hallo volgende opdracht als Connect VIServer niet wordt herkend als Hallo-naam van cmdlet.
 
            Add-PSSnapin VMware.VimAutomation.Core 

5. tooget alle Hallo namen van virtuele machines op een vCenter-server/vSphere ESXi hosten en Hallo lijst opslaan in een txt-bestand uitvoeren Hallo twee opdrachten die hier worden vermeld.
Vervang &lsaquo;servernaam&rsaquo;, &lsaquo;gebruikersnaam&rsaquo;, &lsaquo;wachtwoord&rsaquo;, &lsaquo;outputfile.txt&rsaquo;; door uw invoer.

            Connect-VIServer -Server <server name> -User <user name> -Password <password>

            Get-VM |  Select Name | Sort-Object -Property Name >  <outputfile.txt>

6. Hallo-uitvoerbestand openen in Kladblok en kopieer vervolgens Hallo namen van alle virtuele machines die u wilt dat tooprofile tooanother bestand (bijvoorbeeld ProfileVMList.txt) per regel één VM-naam. Dit bestand wordt gebruikt als invoer toohello *- VMListFile* parameter van het opdrachtregelprogramma Hallo.

    ![Lijst van de VM-naam in Hallo-implementatie plannen](./media/site-recovery-deployment-planner/profile-vm-list.png)

### <a name="start-profiling"></a>Profileren starten
Nadat u Hallo lijst met virtuele machines toobe profiling wordt gestart hebt, kunt u kunt Hallo hulpprogramma uitvoeren in de modus profilering. Hier volgt Hallo-lijst van verplichte en optionele parameters van Hallo hulpprogramma toorun in de modus voor profielservices gegeven.

ASRDeploymentPlanner.exe -Operation StartProfiling /?

| Parameternaam | Beschrijving |
|---|---|
| -Operation | StartProfiling |
| -Server | Hallo FQDN-naam of IP-adres van Hallo vCenter server vSphere/ESXi-host waarvan VM's toobe profiling wordt gestart zijn.|
| -User | Hallo gebruiker naam tooconnect toohello vCenter server vSphere/ESXi-host. Hallo gebruiker nodig toohave alleen-lezen toegang, minimaal.|
| -VMListFile | Hallo-bestand dat Hallo lijst met virtuele machines toobe profiel bevat. Hallo-bestandspad kan absoluut of relatief zijn. Hallo-bestand moet één VM-naam of het IP-adres per regel bevatten. De naam van de virtuele machine is opgegeven in Hallo-bestand moet Hallo dezelfde is als Hallo VM-naam op Hallo vCenter server vSphere/ESXi-host.<br>Hallo bestand VMList.txt bevat bijvoorbeeld Hallo VM's te volgen:<ul><li>virtual_machine_A</li><li>10.150.29.110</li><li>virtual_machine_B</li><ul> |
| -NoOfDaysToProfile | het aantal dagen op dat voor welke profilering toobe Hallo uitgevoerd. Het is raadzaam dat u meer dan 15 dagen tooensure die het patroon van de werkbelasting in uw omgeving over Hallo Hallo opgegeven periode is waargenomen en gebruikt een nauwkeurige aanbeveling tooprovide profilering uitvoert. |
| -Directory | (Optioneel) Hallo universal naming convention (UNC) of een lokale map pad toostore profileringsgegevens gegenereerd tijdens het samenstellen van profiel. Als een mapnaam niet opgegeven is, wordt als de standaardmap Hallo Hallo-map met de naam 'ProfiledData' onder de huidige pad Hallo gebruikt. |
| -Password | (Optioneel) Hallo wachtwoord toouse tooconnect toohello vCenter server vSphere/ESXi-host. Als u niets nu opgeeft, wordt u gevraagd om bij het Hallo-opdracht is uitgevoerd.|
| -StorageAccountName | (Optioneel) Hallo opslag-accountnaam op die is gebruikt toofind Hallo doorvoer haalbare voor replicatie van gegevens uit een on-premises tooAzure. Hallo hulpprogramma uploads test toothis storage account toocalculate gegevensdoorvoer.|
| -StorageAccountKey | (Optioneel) Hallo opslagaccount sleutel die tooaccess Hallo storage-account heeft gebruikt. Toohello Azure-portal gaat > opslagaccounts ><*opslagaccountnaam*>> Instellingen > Sneltoetsen > Key1 (of primaire toegangssleutel voor klassieke storage-account). |
| -Environment | (optioneel) Dit is uw doelomgeving voor het Azure Storage-account. Dit kan een van de volgende drie waarden zijn: AzureCloud, AzureUSGovernment, AzureChinaCloud. De standaardwaarde is AzureCloud. Hallo-parameter gebruiken wanneer het doel-Azure-regio Azure US Government of Azure China clouds is. |


Het is raadzaam dat u uw virtuele machines ten minste 15 dagen van de too30 profiel. Tijdens het Hallo profilering periode, blijft ASRDeploymentPlanner.exe actief. Hallo hulpprogramma haalt profilering tijdsinvoer in dagen. Als u tooprofile voor enkele uren of minuten voor een snelle test van Hallo hulpprogramma openbare preview hello wilt, moet u tooconvert Hallo tijd in Hallo gelijkwaardige meting van dagen. Hallo invoer moet bijvoorbeeld tooprofile gedurende 30 minuten 30/(60*24) = 0.021 dagen. Hallo minimale toegestane tijd profilering is 30 minuten.

Tijdens het samenstellen van profiel, kunt u eventueel een opslag-accountnaam en sleutels toofind Hallo doorvoer die Site Recovery op Hallo moment van replicatie vanaf de configuratieserver Hallo of proces server tooAzure bereiken kunt doorgeven. Als het Hallo-opslag-accountnaam en de sleutel niet worden doorgegeven tijdens het samenstellen van profiel, berekend Hallo hulpprogramma geen haalbare doorvoer.

U kunt meerdere exemplaren van Hallo-hulpprogramma voor verschillende sets van virtuele machines uitvoeren. Zorg ervoor dat Hallo VM-namen niet worden herhaald in een Hallo profilering sets. Bijvoorbeeld, als u tien VM's hebben profiel (VM1 via VM10) en na enkele dagen gewenste tooprofile een andere vijf VMs (VM11 via VM15), kunt u Hallo-hulpprogramma uitvoeren vanaf een andere opdrachtregelconsole voor Hallo tweede set van virtuele machines (VM11 via VM15). Zorg ervoor dat Hallo tweede set van virtuele machines hebben geen een VM-namen van de eerste profilering exemplaar Hallo of u een andere uitvoermap voor Hallo tweede uitvoeren. Als twee exemplaren van het hulpprogramma hello worden gebruikt voor het samenstellen van profiel hello dezelfde VM's en gebruik Hallo dezelfde uitvoermap, Hallo gegenereerd rapport wordt mogelijk onjuist.

VM-configuraties zijn eenmaal aan begin Hallo Hallo profileren bewerking vastgelegd en opgeslagen in een bestand met de naam VMDetailList.xml. Deze informatie wordt gebruikt wanneer het Hallo-rapport wordt gegenereerd. Eventuele wijzigingen in de VM-configuratie (bijvoorbeeld een verhoogde aantal kernen, schijven of NIC's) van Hallo begin toohello einde van het samenstellen van profiel gebruikt niet vastgelegd. Als profiled VM-configuratie is gewijzigd tijdens Hallo profilering Hallo openbare preview, is hier Hallo tijdelijke oplossing tooget laatste VM gegevens bij het Hallo-rapport genereren:

* Back-up VMdetailList.xml en verwijder het Hallo-bestand van de huidige locatie.
* Doorgeven - gebruiker en -wachtwoord argumenten Hallo gelijktijdig genereren van rapporten.

Hallo profilering opdracht genereert meerdere bestanden in Hallo profilering directory. Verwijder Hallo-bestanden niet, omdat dit dus gevolgen heeft voor het genereren van rapporten.

#### <a name="example-1-profile-vms-for-30-days-and-find-hello-throughput-from-on-premises-tooazure"></a>Voorbeeld 1: Profiel voor virtuele machines voor 30 dagen en zoeken Hallo doorvoer van lokale tooAzure
```
ASRDeploymentPlanner.exe -Operation StartProfiling -Directory “E:\vCenter1_ProfiledData” -Server vCenter1.contoso.com -VMListFile “E:\vCenter1_ProfiledData\ProfileVMList1.txt”  -NoOfDaysToProfile  30  -User vCenterUser1 -StorageAccountName  asrspfarm1 -StorageAccountKey Eby8vdM02xNOcqFlqUwJPLlmEtlCDXJ1OUzFT50uSRZ6IFsuFq2UVErCz4I6tq/K1SZFPTOtr/KBHBeksoGMGw==
```

#### <a name="example-2-profile-vms-for-15-days"></a>Voorbeeld 2: virtuele machines 15 dagen profileren

```
ASRDeploymentPlanner.exe -Operation StartProfiling -Directory “E:\vCenter1_ProfiledData” -Server vCenter1.contoso.com -VMListFile “E:\vCenter1_ProfiledData\ProfileVMList1.txt”  -NoOfDaysToProfile  15  -User vCenterUser1
```

#### <a name="example-3-profile-vms-for-1-hour-for-a-quick-test-of-hello-tool"></a>Voorbeeld 3: Profiel VMs 1 uur voor een snelle test van Hallo-hulpprogramma
```
ASRDeploymentPlanner.exe -Operation StartProfiling -Directory “E:\vCenter1_ProfiledData” -Server vCenter1.contoso.com -VMListFile “E:\vCenter1_ProfiledData\ProfileVMList1.txt”  -NoOfDaysToProfile  0.04  -User vCenterUser1
```

>[!NOTE]
>
>* Als server Hallo dat Hallo-hulpprogramma uitgevoerd op de opnieuw wordt opgestart of is gecrasht, of als u sluiten Hallo hulpprogramma met behulp van Ctrl + C, Hallo profiel gegevens behouden blijven. Er is echter een kans ontbrekende Hallo afgelopen 15 minuten van profiel gegevens. In een exemplaar opnieuw u Hallo hulpprogramma in de modus profilering uitgevoerd nadat het Hallo-server opnieuw is opgestart.
>* Wanneer Hallo opslagaccount naam en sleutel worden doorgegeven, Hallo hulpprogramma metingen Hallo doorvoer op Hallo laatste stap van het samenstellen van profiel. Als Hallo hulpprogramma is gesloten voordat profilering is voltooid, wordt er geen Hallo doorvoer berekend. toofind hello doorvoer vóór het genereren van Hallo rapport, kunt u Hallo GetThroughput bewerking van Hallo opdrachtregelconsole uitvoeren. Hallo gegenereerde rapport bevat anders niet Hallo doorvoer informatie.


## <a name="generate-a-report"></a>Een rapport genereren
Hallo-programma genereert macro's Microsoft Excel-bestand (XLSM-bestand) als Hallo rapportuitvoer, een overzicht van alle Hallo aanbevelingen voor de implementatie. Hallo rapport heet DeploymentPlannerReport_ <*unieke numerieke id*> xlsm en geplaatste in Hallo opgegeven map.

Nadat het samenstellen van profiel is voltooid, kunt u Hallo hulpprogramma uitvoeren in de modus voor genereren van rapporten. Hallo volgende tabel bevat een lijst met hulpprogramma verplichte en optionele parameters toorun in de modus voor genereren van rapporten.

`ASRDeploymentPlanner.exe -Operation GenerateReport /?`

|Parameternaam | Beschrijving |
|-|-|
| -Operation | GenerateReport |
| -Server |  Hallo vCenter/vSphere server volledig gekwalificeerde domeinnaam of IP-adres (gebruik Hallo dezelfde naam of IP-adres dat u hebt gebruikt bij Hallo profilering) waar de virtuele machines waarvan rapport gegenereerd toobe is voor het profiel van Hallo zich bevinden. Houd er rekening mee dat als u een vCenter-server op Hallo moment profilering gebruikt, kunt u een vSphere-server voor het genereren van rapporten en vice versa.|
| -VMListFile | Hallo-bestand met het aantal profiel virtuele machines die rapport Hallo Hallo is toobe gegenereerd voor. Hallo-bestandspad kan absoluut of relatief zijn. Hallo-bestand moet bevatten één VM-naam of IP-adres per regel. Hallo VM-namen die zijn opgegeven in het Hallo-bestand moet hetzelfde zijn als de VM-namen Hallo op Hallo vCenter server vSphere/ESXi-host en de overeenkomst die is gebruikt tijdens het samenstellen van profiel Hallo.|
| -Directory | (Optioneel) Hallo UNC of lokale directorypad waar de gegevens (bestanden die zijn gegenereerd tijdens het samenstellen van profiel) voor het profiel van Hallo wordt opgeslagen. Deze gegevens is vereist voor het Hallo-rapport te genereren. Als u deze parameter niet opgeeft, wordt de directory ProfiledData gebruikt. |
| -GoalToCompleteIR | (Optioneel) Hallo aantal uren in welke Hallo Hallo initiële replicatie voor virtuele machines profiel moet toobe voltooid. Hallo gegenereerd rapport bevat het aantal virtuele machines waarvoor de initiële replicatie kan worden voltooid in Hallo opgegeven Hallo tijd. Hallo standaardwaarde is 72 uur. |
| -User | (Optioneel) Hallo gebruiker naam toouse tooconnect toohello vCenter/vSphere-server. Hallo-naam is gebruikte toofetch Hallo meest recente configuratie-informatie van Hallo VM's, zoals het aantal schijven Hallo aantal kernen en aantal NIC's, toouse in Hallo rapport. Als het Hallo-naam is niet opgegeven, wordt Hallo verzamelde gegevens aan begin Hallo Hallo beleggen profilering gebruikt. |
| -Password | (Optioneel) Hallo wachtwoord toouse tooconnect toohello vCenter server vSphere/ESXi-host. Als Hallo wachtwoord niet is opgegeven als parameter, wordt u gevraagd om later wanneer Hallo-opdracht wordt uitgevoerd. |
| -DesiredRPO | (Optioneel) Hallo gewenste beoogd herstelpunt, in minuten. Hallo standaardwaarde is 15 minuten.|
| -Bandwidth | De bandbreedte in Mbps. Hallo parameter toouse toocalculate hello RPO die kan worden bereikt voor Hallo opgegeven bandbreedte. |
| -StartDate | (Optioneel) Hallo begindatum en -tijd in MM-DD-YYYY:HH:MM (24-uursnotatie). Als u *StartDate* opgeeft, moet u ook *EndDate* opgeven. Wanneer StartDate wordt opgegeven, wordt voor Hallo profiel gegevens die worden verzameld tussen StartDate en EndDate bevat Hallo rapport gegenereerd. |
| -EndDate | (Optioneel) Hallo einddatum en eindtijd in MM-DD-YYYY:HH:MM (24-uursnotatie). Als u *EndDate* opgeeft, moet u ook *StartDate* opgeven. Wanneer EndDate wordt opgegeven, wordt voor Hallo profiel gegevens die worden verzameld tussen StartDate en EndDate bevat Hallo rapport gegenereerd. |
| -GrowthFactor | (Optioneel) Hallo-groeifactor, uitgedrukt als percentage. Hallo standaardwaarde is 30 procent. |
| -UseManagedDisks | (Optioneel) UseManagedDisks - Ja/Nee. Standaard is Ja. Hallo aantal virtuele machines die in een enkel opslagaccount kunnen worden geplaatst wordt in overweging of Failover en testen van failover van virtuele machines wordt uitgevoerd op de beheerde schijf in plaats van niet-beheerde schijf berekend. |

#### <a name="example-1-generate-a-report-with-default-values-when-hello-profiled-data-is-on-hello-local-drive"></a>Voorbeeld 1: Een rapport genereren met standaardwaarden als Hallo profiel gegevens op de lokale schijf Hallo
```
ASRDeploymentPlanner.exe -Operation GenerateReport -Server vCenter1.contoso.com -Directory “\\PS1-W2K12R2\vCenter1_ProfiledData” -VMListFile “\\PS1-W2K12R2\vCenter1_ProfiledData\ProfileVMList1.txt”
```

#### <a name="example-2-generate-a-report-when-hello-profiled-data-is-on-a-remote-server"></a>Voorbeeld 2: Een rapport genereren wanneer Hallo profiel gegevens op een externe server
U moet lees-/ schrijftoegang hebben voor de externe map Hallo.
```
ASRDeploymentPlanner.exe -Operation GenerateReport -Server vCenter1.contoso.com -Directory “\\PS1-W2K12R2\vCenter1_ProfiledData” -VMListFile “\\PS1-W2K12R2\vCenter1_ProfiledData\ProfileVMList1.txt”
```

#### <a name="example-3-generate-a-report-with-a-specific-bandwidth-and-goal-toocomplete-ir-within-specified-time"></a>Voorbeeld 3: Een rapport met een specifieke bandbreedte en doel toocomplete IR genereren binnen de opgegeven periode
```
ASRDeploymentPlanner.exe -Operation GenerateReport -Server vCenter1.contoso.com -Directory “E:\vCenter1_ProfiledData” -VMListFile “E:\vCenter1_ProfiledData\ProfileVMList1.txt” -Bandwidth 100 -GoalToCompleteIR 24
```

#### <a name="example-4-generate-a-report-with-a-5-percent-growth-factor-instead-of-hello-default-30-percent"></a>Voorbeeld 4: Een rapport met een 5 procent groeifactor in plaats van Hallo standaard 30 procent genereren
```
ASRDeploymentPlanner.exe -Operation GenerateReport -Server vCenter1.contoso.com -Directory “E:\vCenter1_ProfiledData” -VMListFile “E:\vCenter1_ProfiledData\ProfileVMList1.txt” -GrowthFactor 5
```

#### <a name="example-5-generate-a-report-with-a-subset-of-profiled-data"></a>Voorbeeld 5: een rapport genereren met een subset geprofileerde gegevens
Bijvoorbeeld: u hebt 30 dagen aan gegevens profiling wordt gestart en toogenerate een rapport wilt slechts 20 dagen.
```
ASRDeploymentPlanner.exe -Operation GenerateReport -Server vCenter1.contoso.com -Directory “E:\vCenter1_ProfiledData” -VMListFile “E:\vCenter1_ProfiledData\ProfileVMList1.txt” -StartDate  01-10-2017:12:30 -EndDate 01-19-2017:12:30
```

#### <a name="example-6-generate-a-report-for-5-minute-rpo"></a>Voorbeeld 6: een rapport genereren voor 5 minuten RPO
```
ASRDeploymentPlanner.exe -Operation GenerateReport -Server vCenter1.contoso.com -Directory “E:\vCenter1_ProfiledData” -VMListFile “E:\vCenter1_ProfiledData\ProfileVMList1.txt”  -DesiredRPO 5
```

## <a name="percentile-value-used-for-hello-calculation"></a>Gebruikt voor de berekening Hallo percentielwaarde
**Welke standaardwaarde percentiel maatstaven voor prestaties Hallo verzameld tijdens het samenstellen van profiel biedt Hallo hulpprogramma gebruiken bij het genereren van een rapport?**

Hallo hulpprogramma standaardwaarden toohello 95e percentiel waarden van IOPS, lezen/schrijven schrijven IOPS en gegevensverloop die zijn verzameld tijdens het samenstellen van profiel voor alle Hallo VM's. Met deze metriek zorgt ervoor dat 100E percentiel-piek van hello, uw VM's vanwege tijdelijke gebeurtenissen ziet wordt niet gebruikt toodetermine vereisten van uw doel-opslagaccount en de bron-bandbreedte. Voorbeelden van tijdelijke gebeurtenissen zijn het één keer per dag uitvoeren van een back-up, het periodiek indexeren van een database, het genereren van analyserapporten en andere vergelijkbare activiteiten die op een bepaald moment actief zijn.

Met behulp van 95e percentiel waarden Hallo biedt beschikt u over een waar beeld van de werkelijke werkbelasting kenmerken, en het beste prestaties wanneer Hallo werkbelastingen worden uitgevoerd op Azure. We verwachten niet dat u toochange dit nummer moet. Als u Hallo-waarde (toohello 90 percentiel, bijvoorbeeld) wijzigt, kunt u het configuratiebestand Hallo bijwerken *ASRDeploymentPlanner.exe.config* in de standaardmap Hallo en toogenerate een nieuw rapport op Hallo bestaande profiel opslaan gegevens.
```
<add key="WriteIOPSPercentile" value="95" />      
<add key="ReadWriteIOPSPercentile" value="95" />      
<add key="DataChurnPercentile" value="95" />
```

## <a name="growth-factor-considerations"></a>Overwegingen voor groeifactor
**Waarom moet ik rekening houden met een groeifactor bij het plannen van implementaties?**

Het is essentieel tooaccount groei van uw werkbelasting kenmerken, ervan uitgaande dat een mogelijke toename van gebruik gedurende een bepaalde periode. Nadat de beveiliging is aanwezig is, als uw werkbelasting kenmerken wijzigt, kunt u niet tooa ander opslagaccount voor beveiliging overschakelen zonder uitschakelen en het Hallo-beveiliging opnieuw in te schakelen.

Stel dat uw virtuele machine op dit moment voldoende heeft aan een Standard Storage-replicatie-account. Hallo zijn drie maanden, verschillende wijzigingen waarschijnlijk toooccur:

* het aantal gebruikers van Hallo-toepassing die wordt uitgevoerd op Hallo VM Hello wordt verhoogd.
* Hallo resulterende toegenomen verloop op Hallo VM wordt Hallo VM toogo toopremium opslag nodig, zodat de replicatie van Site Recovery kunt blijven.
* Als gevolg daarvan kan u toodisable en opnieuw inschakelen van beveiliging tooa premium storage-account.

Het is raadzaam dat u van plan voor groei bent tijdens de implementatie plannen en tijdens het Hallo-standaardwaarde is 30 procent. U bent Hallo deskundige op uw toepassing gebruik patroon en groei projecties en u kunt dit nummer dienovereenkomstig wijzigen tijdens het genereren van een rapport. Bovendien kunt u meerdere rapporten genereren met verschillende groei factoren Hello dezelfde gegevens profiel en bepalen welke aanbevelingen doel opslag- en bandbreedte geschikt zijn voor u.

Microsoft Excel-rapport gegenereerd Hallo bevat Hallo volgende informatie:

* [Invoer](site-recovery-deployment-planner.md#input)
* [Aanbevelingen](site-recovery-deployment-planner.md#recommendations-with-desired-rpo-as-input)
* [Aanbevelingen bandbreedte](site-recovery-deployment-planner.md#recommendations-with-available-bandwidth-as-input)
* [VM<->Opslagplaatsing](site-recovery-deployment-planner.md#vm-storage-placement)
* [Compatibele VM's](site-recovery-deployment-planner.md#compatible-vms)
* [Niet-compatibele VM's](site-recovery-deployment-planner.md#incompatible-vms)

![Implementatieplanner](./media/site-recovery-deployment-planner/dp-report.png)

## <a name="get-throughput"></a>Doorvoer bepalen

tooestimate hello doorvoer die Site Recovery van bereiken kunt lokale tooAzure tijdens replicatie, Hallo hulpprogramma uitvoeren in de modus GetThroughput. Hallo hulpprogramma berekent Hallo doorvoer van Hallo-server die als Hallo hulpprogramma wordt uitgevoerd op. In het ideale geval worden deze server is gebaseerd op Hallo server sizing configuratiehandleiding. Als u Site Recovery-onderdelen on-premises identiteitsinfrastructuur al hebt geïmplementeerd, kunt u de Hallo hulpprogramma uitvoeren op Hallo configuratieserver.

Open een opdrachtregelconsole en implementatie van Site Recovery toohello hulpprogramma map plannen gaat. Voer ASRDeploymentPlanner.exe uit met de volgende parameters.

`ASRDeploymentPlanner.exe -Operation GetThroughput /?`

|Parameternaam | Beschrijving |
|-|-|
| -Operation | GetThroughput |
| -Directory | (Optioneel) Hallo UNC of lokale directorypad waar de gegevens (bestanden die zijn gegenereerd tijdens het samenstellen van profiel) voor het profiel van Hallo wordt opgeslagen. Deze gegevens is vereist voor het Hallo-rapport te genereren. Als u geen directory opgeeft, wordt de directory 'ProfiledData' gebruikt. |
| -StorageAccountName | Hallo-opslag-accountnaam die voor replicatie van gegevens van de lokale tooAzure toofind Hallo bandbreedte gebruikt. Hallo hulpprogramma uploads test gegevens toothis storage account toofind Hallo bandbreedte. |
| -StorageAccountKey | Hallo-opslagaccount gebruikt die tooaccess Hallo storage-account gebruikt. Ga toohello Azure-portal > opslagaccounts ><*opslagaccountnaam*>> Instellingen > Sneltoetsen > Key1 (of een primaire toegangssleutel voor een klassieke storage-account). |
| -VMListFile | Hallo-bestand waarin Hallo lijst met virtuele machines toobe profiel voor het berekenen van Hallo bandbreedte. Hallo-bestandspad kan absoluut of relatief zijn. Hallo-bestand moet één VM-naam of het IP-adres per regel bevatten. Hallo VM-namen is opgegeven in Hallo-bestand moet Hallo dezelfde Hallo VM namen op Hallo vCenter server vSphere/ESXi-host.<br>Hallo bestand VMList.txt bevat bijvoorbeeld Hallo VM's te volgen:<ul><li>VM_A</li><li>10.150.29.110</li><li>VM_B</li></ul>|
| -Environment | (optioneel) Dit is uw doelomgeving voor het Azure Storage-account. Dit kan een van de volgende drie waarden zijn: AzureCloud, AzureUSGovernment, AzureChinaCloud. De standaardwaarde is AzureCloud. Hallo-parameter gebruiken wanneer het doel-Azure-regio Azure US Government of Azure China clouds is. |

Hallo hulpprogramma maakt verschillende 64 MB asrvhdfile <> # .vhd-bestanden ("#" is het aantal bestanden Hallo) op de opgegeven map Hallo. Hallo hulpprogramma bestandsuploads Hallo bestanden toohello storage account toofind Hallo doorvoer. Hallo doorvoer wordt gemeten, verwijderd Hallo hulpprogramma nadat alle Hallo-bestanden uit Hallo storage-account en Hallo lokale server. Als Hallo hulpprogramma wordt beëindigd om welke reden terwijl deze doorvoer berekent, verwijderen niet het Hallo bestanden van Hallo opslag of van de lokale server Hallo. Hebt u toodelete ze handmatig.

Hallo doorvoer wordt gemeten op een bepaald punt in tijd en is Hallo maximale doorvoer die Site Recovery tijdens replicatie bereiken kunt, op voorwaarde dat alle andere factoren blijven Hallo dezelfde. Als bijvoorbeeld een toepassing wordt gestart die meer bandbreedte op Hallo hetzelfde netwerk, de werkelijke doorvoer Hallo tijdens de replicatie varieert. Als u Hallo GetThroughput opdracht vanaf een configuratieserver uitvoert, is Hallo hulpprogramma niet op de hoogte van alle beveiligde virtuele machines en de lopende replicatie. resultaat van Hallo gemeten doorvoer is Hello verschillende als Hallo GetThroughput wordt uitgevoerd wanneer Hallo virtuele machines beveiligde hoge gegevens verloop. Het is raadzaam dat u Hallo hulpprogramma uitvoeren op verschillende momenten tijdens het samenstellen van profiel toounderstand welke doorvoer kan worden bereikt op verschillende tijdstippen. In Hallo-rapport toont Hallo hulpprogramma Hallo laatste gemeten doorvoer.

### <a name="example"></a>Voorbeeld
```
ASRDeploymentPlanner.exe -Operation GetThroughput -Directory  E:\vCenter1_ProfiledData -VMListFile E:\vCenter1_ProfiledData\ProfileVMList1.txt  -StorageAccountName  asrspfarm1 -StorageAccountKey by8vdM02xNOcqFlqUwJPLlmEtlCDXJ1OUzFT50uSRZ6IFsuFq2UVErCz4I6tq/K1SZFPTOtr/KBHBeksoGMGw==
```

>[!NOTE]
>
> Hallo-hulpprogramma uitvoeren op een server waarop Hallo dezelfde opslag- en CPU-kenmerken als Hallo configuratieserver.
>
> Voor replicatie aanbevolen set Hallo bandbreedte toomeet hello RPO 100 procent Hallo tijd. Nadat u de juiste bandbreedte hello, ingesteld als u een toename van Hallo bereikt doorvoer gemeld door Hallo hulpprogramma niet ziet, Hallo te volgen:
>
>  1. Toodetermine controleren of er is een netwerk Quality of Service (QoS) die de Site Recovery-doorvoer wordt beperkt.
>
>  2. Controleer toodetermine of uw Site Recovery-kluis in Hallo dichtstbijzijnde fysiek ondersteunde Microsoft Azure-regio toominimize-netwerklatentie.
>
>  3. Controleer uw lokale opslag kenmerken toodetermine of kunt u de Hallo hardware (bijvoorbeeld HDD tooSSD) te verbeteren.
>
>  4. Site Recovery-instellingen in de processerver Hallo Hallo ook wijzigen[vergroot Hallo hoeveelheid netwerkbandbreedte die wordt gebruikt voor replicatie](./site-recovery-plan-capacity-vmware.md#control-network-bandwidth).

## <a name="recommendations-with-desired-rpo-as-input"></a>Aanbevelingen met gewenste RPO als invoer

### <a name="profiled-data"></a>Geprofileerde gegevens

![Hallo profiel gegevens weergeven in Hallo-implementatie plannen](./media/site-recovery-deployment-planner/profiled-data-period.png)

**Profiel gegevensperiode**: Hallo-periode gedurende welke Hallo profilering is uitgevoerd. Hallo hulpprogramma bevat standaard alle profiled gegevens in de berekening Hallo, tenzij er Hallo rapport gegenereerd voor een bepaalde periode met behulp van StartDate en EndDate bevat opties tijdens het genereren van rapporten.

**Servernaam**: Hallo-naam of IP-adres van VMware vCenter-Hallo of ESXi-host waarvan VM's rapport is gegenereerd.

**Gewenste RPO**: Hallo beoogde herstelpunt voor uw implementatie. Standaard vereist Hallo netwerkbandbreedte wordt berekend voor de RPO-waarden van 15, 30 en 60 minuten. Op basis van de selectie hello, zijn Hallo van invloed op een waarden bijgewerkt op Hallo blad. Als u hebt gebruikt Hallo *DesiredRPOinMin* parameter tijdens het Hallo-rapport die waarde wordt weergegeven in Hallo RPO gewenst resultaat te genereren.

### <a name="profiling-overview"></a>Overzicht van profilering

![Profileren van resulteert in het Hallo-implementatie plannen](./media/site-recovery-deployment-planner/profiling-overview.png)

**Totaal aantal virtuele Machines profiel**: Hallo totale aantal VM's waarvan profiled gegevens beschikbaar zijn. Hallo VMListFile namen van alle virtuele machines die niet zijn profiel heeft, die virtuele machines worden niet meegenomen in Hallo rapporten te genereren als worden uitgesloten van Hallo profiel VMs totaalaantal.

**Compatibele virtuele Machines**: Hallo aantal virtuele machines die beveiligde tooAzure worden kunnen door Site Recovery te gebruiken. Het is totale aantal compatibele virtuele machines voor welke Hallo vereist netwerkbandbreedte, aantal storage-accounts, het aantal kernen voor Azure en aantal configuratieservers en aanvullende processen servers worden berekend Hallo. Hallo-details van elke compatibel VM zijn beschikbaar in de sectie 'Compatibel VMs' Hallo.

**Niet-compatibele virtuele Machines**: Hallo aantal profiel VM's die niet compatibel voor beveiliging met Site Recovery zijn. Hallo redenen voor incompatibiliteit worden vermeld in de sectie 'Incompatibel VMs' Hallo. Als Hallo VMListFile namen van alle virtuele machines die niet zijn profiel heeft, worden deze VMs uitgesloten van Hallo incompatibel VMs count. Deze virtuele machines worden weergegeven als 'Gegevens niet ' aan Hallo einde van Hallo 'incompatibel VMs' gedeelte gevonden.

**Gewenste RPO**: het gewenste beoogde herstelpunt (Recovery Point Objective [RPO]) in minuten. Hallo-rapport is gegenereerd voor drie RPO-waarden: 15 (standaard), 30 en 60 minuten. Hallo bandbreedte aanbeveling in Hallo rapport wordt op basis van uw selectie in de lijst Hallo gewenst RPO omlaag rechts bovenaan Hallo van Hallo blad gewijzigd. Als u Hallo rapport hebt gegenereerd met behulp van Hallo *- DesiredRPO* parameter met een aangepaste waarde voor deze aangepaste waarde wordt weergegeven als Hallo standaard in de lijst Hallo RPO gewenst vervolgkeuzelijst.

### <a name="required-network-bandwidth-mbps"></a>Vereiste netwerkbandbreedte (Mbps)

![Vereiste netwerkbandbreedte in Hallo-implementatie plannen](./media/site-recovery-deployment-planner/required-network-bandwidth.png)

**toomeet RPO 100 procent Hallo tijd:** Hallo aanbevolen bandbreedte in Mbps toobe toomeet uw gewenste RPO 100 procent toegewezen van Hallo tijd. Deze hoeveelheid bandbreedte moet zijn speciaal ontworpen is voor replicatie van verschillen van de actieve status van uw compatibel VMs tooavoid eventuele schendingen RPO.

**toomeet RPO 90 procent van Hallo tijd**: vanwege breedband prijzen of andere reden, als u niet Hallo bandbreedte nodig toomeet uw gewenste RPO 100 procent van de tijd hello instellen, kunt u kiezen toogo met een lagere bandbreedte instellen die kan voorzien in uw gewenste RPO 90 procent van het Hallo-tijd. toounderstand hello gevolgen van het instellen van deze lagere bandbreedte, Hallo rapport bevat een wat-als-analyse van Hallo aantal en de duur van RPO schendingen tooexpect.

**Gerealiseerde doorvoer:** Hallo doorvoer van Hallo server waarop u hebt Hallo GetThroughput opdracht toohello Microsoft Azure-regio waar Hallo storage-account zich bevindt. Dit nummer doorvoer geeft Hallo geschatte niveau die u bereiken kan bij het beveiligen van Hallo compatibele virtuele machines met behulp van de Site is hersteld, mits de configuratieserver of proces server opslag en netwerk kenmerken blijven Hallo dezelfde als die van Hallo-server van waaruit u Hallo-hulpprogramma hebt uitgevoerd.

U moet Hallo aanbevolen bandbreedte toomeet hello RPO 100 procent Hallo tijd instellen voor replicatie. Nadat u Hallo bandbreedte, ingesteld als er geen een toename in doorvoer Hallo bereikt, zoals gemeld door het hulpprogramma hello, doen hello te volgen:

1. Toosee controleren of er is een netwerk Quality of Service (QoS) die de Site Recovery-doorvoer wordt beperkt.

2. Controleer toosee of uw Site Recovery-kluis in Hallo dichtstbijzijnde fysiek ondersteunde Microsoft Azure-regio toominimize-netwerklatentie.

3. Controleer uw lokale opslag kenmerken toodetermine of kunt u de Hallo hardware (bijvoorbeeld HDD tooSSD) te verbeteren.

4. Site Recovery-instellingen in de processerver Hallo Hallo ook wijzigen[verhogen Hallo hoeveelheid netwerkbandbreedte gebruikt voor replicatie](./site-recovery-plan-capacity-vmware.md#control-network-bandwidth).

Als u Hallo-hulpprogramma op een configuratieserver of de processerver die al is beveiligd van virtuele machines uitvoert, moet u Hallo hulpprogramma een paar keer uitvoeren. Hallo bereikt doorvoer verandert, afhankelijk van Hallo hoeveelheid verloop op dat moment wordt verwerkt.

Voor alle Enterprise-implementaties van Site Recovery wordt het gebruik van [ExpressRoute](https://aka.ms/expressroute) aanbevolen.

### <a name="required-storage-accounts"></a>Vereiste opslagaccounts
grafiek-toont Hallo kunt u het totale aantal opslag (standard en premium) accounts die vereist tooprotect alle zijn volgende Hallo Hallo compatibele virtuele machines. welke storage account toouse voor elke VM toolearn Zie Hallo 'VM-opslag plaatsing' sectie.

![Vereiste storage-accounts in het Hallo-implementatie plannen](./media/site-recovery-deployment-planner/required-azure-storage-accounts.png)

### <a name="required-number-of-azure-cores"></a>Vereiste aantal Azure-kerngeheugens
Dit resultaat is Hallo totaal aantal kernen toobe instellen voordat een failover of test failover van alle Hallo compatibele virtuele machines. Als er te weinig kernen in Hallo abonnement beschikbaar zijn, Site Recovery toocreate VMs mislukt gelijktijdig Hallo met failover of failover testen.

![Het aantal Azure kernen in Hallo-implementatie plannen](./media/site-recovery-deployment-planner/required-number-of-azure-cores.png)

### <a name="required-on-premises-infrastructure"></a>Vereiste on-premises infrastructuur
Deze afbeelding is het totaal aantal Hallo van configuratieservers en aanvullende processen servers toobe geconfigureerd die tooprotect voldoende zou Hallo alle compatibele virtuele machines. Afhankelijk van Hallo ondersteund [grootte aanbevelingen voor de configuratieserver Hallo](https://aka.ms/asr-v2a-on-prem-components), Hallo hulpprogramma aanbevelen extra servers. Hallo-aanbeveling is gebaseerd op Hallo grotere van Hallo per dag verloop of Hallo kunt u het maximum aantal beveiligde virtuele machines (uitgaande van een gemiddelde van drie schijven per VM), afhankelijk van wat is bereikt, wordt de eerste op Hallo configuratie of Hallo aanvullende processen server. Hallo-details van de totale verloop per dag en het totale aantal beveiligde schijven vindt u in de sectie 'Invoer' Hallo.

![Vereiste on-premises infrastructuur in Hallo-implementatie plannen](./media/site-recovery-deployment-planner/required-on-premises-infrastructure.png)

### <a name="what-if-analysis"></a>Wat als-analyse
Deze analyse geeft een overzicht van hoeveel schendingen kunnen zich voordoen tijdens Hallo profilering periode tijdens het instellen van dat een lagere bandbreedte voor Hallo gewenst RPO toobe voldaan slechts 90 procent van het Hallo-tijd. Op elke dag kunnen er een of meer RPO-schendingen optreden. Hallo grafiek toont Hallo piek RPO van Hallo dag.
Op basis van deze analyse, kunt u beslissen als Hallo aantal schendingen RPO voor alle dagen en piek RPO treffers per dag met acceptabele Hallo lagere bandbreedte opgegeven. Als het is acceptabel is, dat kunt u Hallo lagere bandbreedte toewijzen voor replicatie, moet u anders Hallo hogere bandbreedte als voorgestelde toomeet Hallo RPO 100 procent Hallo tijd gewenst toewijzen.

![Wat-als-analyse in Hallo-implementatie plannen](./media/site-recovery-deployment-planner/what-if-analysis.png)

### <a name="recommended-vm-batch-size-for-initial-replication"></a>Aanbevolen VM-batchgrootte voor de initiële replicatie
In deze sectie wordt u aangeraden Hallo aantal VM's die kunnen worden beveiligd in de initiële replicatie van parallelle toocomplete Hallo binnen 72 uur Hello voorgestelde bandbreedte toomeet gewenst RPO 100 procent Hallo tijd wordt ingesteld. Deze waarde is kunt u aanpassen. toochange het gelijktijdig genereren van rapporten, gebruik Hallo *GoalToCompleteIR* parameter.

Hallo grafiek Hier ziet u een bereik van waarden van de bandbreedte en een berekende VM batch grootte aantal toocomplete initiële replicatie in 72 uur, op basis van de gemiddelde Hallo gedetecteerd VM grootte voor alle Hallo compatibele virtuele machines.

In de openbare preview Hallo geeft Hallo rapport geen welke virtuele machines moeten worden opgenomen in een batch. U kunt gebruiken Hallo schijfgrootte wordt weergegeven in Hallo 'compatibel VMs"sectie toofind elke VM-grootte en deze te selecteren voor een batch of kunt u Hallo VM's op basis van bekende werkbelasting kenmerken. Hallo voltooiingstijd van Hallo initiële replicatie worden wijzigingen proportioneel, op basis van de werkelijke VM Hallo-schijfgrootte, schijfruimte vrij en beschikbaar netwerkdoorvoer gebruikt.

![Aanbevolen VM-batchgrootte](./media/site-recovery-deployment-planner/recommended-vm-batch-size.png)

### <a name="growth-factor-and-percentile-values-used"></a>Groeifactor en gebruikte percentielwaarden
Deze sectie onderin Hallo Hallo blad bevat Hallo-percentielwaarde gebruikt voor alle Hallo prestatiemeteritems van Hallo profiel virtuele machines (de standaardwaarde is 95e percentiel) en Hallo groeifactor (de standaardwaarde is 30 procent) die wordt gebruikt in alle Hallo berekeningen.

![Groeifactor en gebruikte percentielwaarden](./media/site-recovery-deployment-planner/max-iops-and-data-churn-setting.png)

## <a name="recommendations-with-available-bandwidth-as-input"></a>Aanbevelingen met beschikbare bandbreedte als invoer

![Aanbevelingen met beschikbare bandbreedte als invoer](./media/site-recovery-deployment-planner/profiling-overview-bandwidth-input.png)

Het is mogelijk dat u om wat voor reden dan ook niet meer dan x Mbps bandbreedte kunt instellen voor Site Recovery-replicatie. Hallo-hulpprogramma kunt u de beschikbare bandbreedte tooinput (met behulp van Hallo - bandbreedte parameter tijdens het genereren van rapporten) en get haalbare RPO Hallo in minuten. Met deze haalbare RPO-waarde, kunt u beslissen of u tooset van extra bandbreedte nodig of u een oplossing voor het herstel na noodgevallen met deze RPO hoeven in orde zijn.

![Haalbare RPO voor 500 Mbps bandbreedte](./media/site-recovery-deployment-planner/achievable-rpos.png)

## <a name="input"></a>Invoer
Hallo invoer werkblad biedt dat een overzicht van Hallo profiel VMware-omgeving.

![Overzicht van Hallo profiel VMware-omgeving](./media/site-recovery-deployment-planner/Input.png)

**Begindatum** en **einddatum**: Hallo begin- en einddatums Hallo profileringsgegevens in aanmerking voor het genereren van rapporten. Hallo-begindatum is standaard Hallo datum wanneer profilering wordt gestart, en de einddatum Hallo is Hallo-datum wanneer profilering stopt. Dit kan Hallo 'StartDate' en 'EndDate' waarden zijn als het Hallo-rapport is gegenereerd met de volgende parameters.

**Totaal aantal dagen profilering**: totaal aantal dagen tussen Hallo profilering Hallo beginnen en eindigen datums voor welke Hallo rapport is gegenereerd.

**Aantal compatibele virtuele machines**: Hallo totale aantal compatibel VM's voor welke netwerkbandbreedte Hallo vereist, vereiste aantal storage-accounts, Microsoft Azure-kernen, configuratieservers en aanvullende processen servers zijn berekend.

**Totaal aantal schijven voor alle compatibele virtuele machines**: Hallo nummer dat wordt gebruikt als een Hallo-ingangen toodecide Hallo aantal configuratieservers en aanvullende processen servers toobe gebruikt in Hallo-implementatie.

**Gemiddeld aantal schijven per compatibele virtuele machine**: gemiddelde aantal schijven Hallo berekend over alle compatibel VM's.

**Gemiddelde grootte van de schijf (GB)**: Hallo gemiddelde schijfgrootte berekend over alle compatibel VM's.

**Gewenste RPO (minuten)**: beide Hallo standaard doelstelling of Hallo waarde herstelpunt doorgegeven voor Hallo 'DesiredRPO' parameter gelijktijdig Hallo met rapport generatie tooestimate vereist bandbreedte.

**Gewenste bandbreedte (Mbps)**: waarde die u hebt doorgegeven voor de parameter 'Bandbreedte' Hallo Hallo gelijktijdig met rapport generatie tooestimate Hallo haalbare RPO.

**Waargenomen typische gegevensverloop per dag (GB)**: Hallo gemiddelde gegevensverloop waargenomen over alle profilering dagen. Dit nummer wordt gebruikt als een Hallo invoer toodecide Hallo aantal configuratieservers en aanvullende processen servers toobe gebruikt in Hallo-implementatie.


## <a name="vm-storage-placement"></a>VM-opslagplaatsing

![VM-opslagplaatsing](./media/site-recovery-deployment-planner/vm-storage-placement.png)

**Opslag schijftype**: ofwel een standard- of premium storage-account, namelijk gebruikte tooreplicate alle bijbehorende virtuele machines die worden vermeld in Hallo Hallo **VMs tooPlace** kolom.

**Voorgestelde voorvoegsel**: Hallo voorgestelde drie tekens voorvoegsel op dat kan worden gebruikt voor de naamgeving van Hallo storage-account. U kunt uw eigen voorvoegsel gebruiken, maar Hallo-hulpprogramma suggestie volgt Hallo [naamgevingsconventie voor storage-accounts partitie](https://aka.ms/storage-performance-checklist).

**Voorgestelde accountnaam**: Hallo-opslagaccountnaam nadat u de voorgestelde voorvoegsel Hallo opnemen. Vervang Hallo naam binnen Hallo punthaken (< en >) met uw aangepaste invoer.

**Meld u Opslagaccount**: alle Hallo replicatielogboeken worden opgeslagen in een standard-opslagaccount. Premium-opslagaccount instellen een extra standard-opslagaccount voor de opslag van het logboek voor virtuele machines die tooa repliceren. Eén Standard-account voor het opslaan van logboeken kan worden gebruikt door meerdere Premium-opslagaccounts voor replicatie. Virtuele machines die gerepliceerd toostandard storage zijn-accounts gebruiken Hallo hetzelfde opslagaccount voor Logboeken.

**Voorgestelde Account logboeknaam**: uw logboek opslagaccountnaam nadat u de voorgestelde voorvoegsel Hallo opnemen. Vervang Hallo naam binnen Hallo punthaken (< en >) met uw aangepaste invoer.

**Samenvatting van de plaatsing**: een samenvatting van Hallo totale belasting van de VM's op Hallo storage-account op Hallo tijdstip van de replicatie en failover of failover testen. Het bevat totale aantal virtuele machines toegewezen toohello storage-account, totale lezen/schrijven IOP's over alle VM's in dit opslagaccount, de totale wordt geplaatst schrijven (replicatie) IOP's, de grootte van de totale installatie voor alle schijven en totaal aantal schijven Hallo.

**Virtuele Machines tooPlace**: een lijst met alle Hallo virtuele machines die moeten worden geplaatst op Hallo storage-account opgegeven voor optimale prestaties en het gebruik.

## <a name="compatible-vms"></a>Compatibele VM's
![Excel-werkblad met compatibele VM's](./media/site-recovery-deployment-planner/compatible-vms.png)

**VM-naam**: Hallo VM-naam of IP-adres dat wordt gebruikt in Hallo VMListFile wanneer een rapport wordt gegenereerd. Deze kolom bevat ook Hallo-schijven (VMDKs) die aangesloten toohello VM's zijn. toodistinguish vCenter VM's met dubbele namen of IP-adressen, Hallo namen bevatten Hallo ESXi-hostnaam. Hallo vermelde ESXi-host is Hallo een waar hello VM is geplaatst als Hallo hulpprogramma aangetroffen tijdens het Hallo profilering periode.

**VM-compatibiliteit**: de mogelijke waarden zijn **Ja** en **Ja**\*. **Ja** \* is voor exemplaren in welke Hallo VM is een geschikt is voor [Azure Premium-opslag](https://aka.ms/premium-storage-workload). Hier Hallo profiel hoge verloop of IOPS schijf past in Hallo P20 of P30 categorie, maar Hallo grootte van Hallo schijf ervoor zorgt dat toobe omlaag tooa P10 of P20 toegewezen. Hallo storage-account, besluit welke opslagschijf premium Typ toomap een schijf, op basis van de grootte. Bijvoorbeeld:
* <128 GB is een P10.
* 128 GB too512 GB is een P20.
* 512 GB too1024 GB is een P30.
* 1025 GB too2048 GB is een p 40.
* 2049 GB too4095 GB is een P50.

Als Hallo werkbelasting kenmerken van een schijf in Hallo P20 of P30 categorie plaatsen, maar Hallo grootte deze naar beneden tooa lagere premium type opslagschijf wijst, Hallo hulpprogramma die VM als markeert **Ja**\*. Hallo-hulpprogramma wordt ook aangeraden dat u Wijzig Hallo bron schijf grootte toofit in Hallo type opslagschijf premium aanbevolen of wijzig Hallo doel schijf type na een failover.

**Opslagtype**: Standard of Premium.

**Voorgestelde voorvoegsel**: Hallo drie tekens opslagaccount voorvoegsel.

**Storage-Account**: Hallo-naam die Hallo voorgestelde opslagaccount voorvoegsel gebruikt.

**R/W IOP's (met groeifactor)**: Hallo piek werkbelasting lezen/schrijven IOPS op Hallo schijf (standaard is 95e percentiel), met inbegrip van toekomstige groeifactor hello (de standaardwaarde is 30 procent). Let op Hallo van totale lezen/schrijven IOPS van een virtuele machine is niet altijd Hallo som van Hallo van de virtuele machine afzonderlijke schijven lezen/schrijven IOP's, omdat Hallo piek lezen/schrijven IOPS Hallo VM Hallo piek Hallo som van de afzonderlijke schijven lezen/schrijven IOPS tijdens elke minuut Hallo profileren van periode.

**Gegevens verloop in Mbps (met groeifactor)**: Hallo piek verloop op Hallo schijf (standaard is 95e percentiel), met inbegrip van toekomstige groeifactor hello (de standaardwaarde is 30 procent). Houd er rekening mee dat Hallo totale gegevensverloop Hallo VM is niet altijd Hallo som van gegevensverloop Hallo van de virtuele machine afzonderlijke schijven, omdat Hallo piek gegevensverloop Hallo VM Hallo piek Hallo som van de afzonderlijke schijven verloop tijdens elke minuut Hallo profilering periode.

**Azure VM-grootte**: ideaal hello Azure Cloud Services de grootte van virtuele machines worden toegewezen voor dit on-premises VM. Hallo-toewijzing is gebaseerd op Hallo lokale VM geheugen, aantal kernen-schijven-netwerkinterfacekaarten en IOPS lezen/schrijven. Hallo-aanbeveling is altijd Hallo laagste Azure VM-grootte dat voldoet aan alle Hallo lokale VM kenmerken.

**Aantal schijven**: totaal aantal schijven op virtuele machine (VMDKs) op Hallo VM Hallo.

**Schijfgrootte (GB)**: Hallo setup totale grootte van alle schijven van Hallo VM. Hallo schijfgrootte voor afzonderlijke schijven Hallo weergegeven Hallo hulpprogramma ook in Hallo VM.

**Kernen**: het aantal CPU Hallo cores op Hallo VM.

**Geheugen (MB)**: Hallo RAM-geheugen op Hallo VM.

**NIC's**: Hallo aantal NIC's op Hallo VM.

**Type opstarten**: het opstarten type Hallo VM is. Dit kan BIOS of EFI zijn. Op dit moment ondersteunt Azure Site Recovery alleen BIOS-opstarttypen. Alle Hallo virtuele machines van het type van EFI-opstarten worden vermeld in het werkblad voor niet-compatibele virtuele machines.

**Type besturingssysteem**: Hallo Hallo VM type besturingssysteem is. Dit kan Windows, Linux of een ander besturingssysteem zijn.

## <a name="incompatible-vms"></a>Niet-compatibele VM's

![Excel-werkblad met niet-compatibele VM's](./media/site-recovery-deployment-planner/incompatible-vms.png)

**VM-naam**: Hallo VM-naam of IP-adres dat wordt gebruikt in Hallo VMListFile wanneer een rapport wordt gegenereerd. Deze kolom bevat ook Hallo VMDKs die aangesloten toohello virtuele machines zijn. toodistinguish vCenter VM's met dubbele namen of IP-adressen, Hallo namen bevatten Hallo ESXi-hostnaam. Hallo vermelde ESXi-host is Hallo een waar hello VM is geplaatst als Hallo hulpprogramma aangetroffen tijdens het Hallo profilering periode.

**VM-compatibiliteit**: Hiermee wordt aangegeven waarom Hallo gegeven van de virtuele machine is niet compatibel voor gebruik met Site Recovery. Hello redenen zijn voor elke niet-compatibele schijf Hallo VM beschreven en, gebaseerd op gepubliceerd [opslaglimieten](https://aka.ms/azure-storage-scalbility-performance), mag geen van de volgende Hallo:

* De schijf is groter dan 4095 GB. Azure Storage biedt momenteel geen ondersteuning voor gegevensschijven groter dan 4095 GB.
* De besturingssysteemschijf is groter dan 2048 GB. Azure Storage biedt momenteel geen ondersteuning voor besturingssysteemschijven groter dan 2048 GB.
* Opstarttype is EFI. Azure Site Recovery ondersteunt op dit moment alleen virtuele machines met het BIOS-opstarttype.

* Totaal aantal VM-grootte (replicatie + TFO) overschrijdt Hallo ondersteund opslagaccount grootte (35 TB). Dit probleem treedt meestal op wanneer één schijf in Hallo VM heeft een prestatiekenmerk die langer is dan Hallo maximaal ondersteunde Azure- of Site Recovery limieten voor standard-opslag. Deze configuratie duwt Hallo VM naar Hallo premium-opslag-zone. Maximaal ondersteunde grootte van een premium storage-account is 35 TB en één beveiligd VM Hallo worden niet echter tussen meerdere opslagaccounts beveiligd. Let ook op dat als een testfailover wordt uitgevoerd op een beveiligde virtuele machine, deze Hallo voert hetzelfde opslagaccount waarin de replicatie wordt uitgevoerd. In dit exemplaar 2 x Hallo grootte van Hallo schijf voor replicatie tooprogress instellen en testen van failover toosucceed parallel.
* De bron-IOPS is groter dan de ondersteunde IOPS-limiet voor opslag van 5000 per schijf.
* De bron-IOPS is groter dan de ondersteunde IOPS-limiet voor opslag van 80.000 per schijf.
* Gemiddelde gegevensverloop overschrijdt de ondersteunde limiet van Site Recovery gegevensverloop van 10 MBps voor de gemiddelde i/o-grootte voor Hallo schijf.
* Totale gegevensverloop over alle schijven op Hallo VM overschrijdt maximale ondersteund Hallo Site Recovery gegevensverloop limiet van 54 MBps per VM.
* Gemiddelde effectieve schrijven IOPS overschrijdt Hallo ondersteund Site Recovery IOPS limiet van 840 voor schijf.
* De opslag van berekende momentopname overschrijdt Hallo ondersteund momentopname opslaglimiet van 10 TB.

**R/W IOP's (met groeifactor)**: Hallo piek werkbelasting IOPS op Hallo schijf (standaard is 95e percentiel), met inbegrip van toekomstige groeifactor hello (de standaardwaarde is 30 procent). Let op Hallo van totale lezen/schrijven IOPS Hallo VM is niet altijd Hallo som van Hallo van de virtuele machine afzonderlijke schijven lezen/schrijven IOP's, omdat Hallo piek lezen/schrijven IOPS Hallo VM Hallo piek Hallo som van de afzonderlijke schijven lezen/schrijven IOPS tijdens elke minuut Hallo profileren van periode.

**Gegevens in Mbps (met groeifactor) verloop**: Hallo piek verloop op Hallo schijf (standaard 95e percentiel), met inbegrip van toekomstige groeifactor hello (standaard 30 procent). Houd er rekening mee dat Hallo totale gegevensverloop Hallo VM is niet altijd Hallo som van gegevensverloop Hallo van de virtuele machine afzonderlijke schijven, omdat Hallo piek gegevensverloop Hallo VM Hallo piek Hallo som van de afzonderlijke schijven verloop tijdens elke minuut Hallo profilering periode.

**Aantal schijven**: totaal aantal VMDKs op Hallo VM Hallo.

**Schijfgrootte (GB)**: Hallo setup totale grootte van alle schijven van Hallo VM. Hallo schijfgrootte voor afzonderlijke schijven Hallo weergegeven Hallo hulpprogramma ook in Hallo VM.

**Kernen**: het aantal CPU Hallo cores op Hallo VM.

**Geheugen (MB)**: Hallo hoeveelheid RAM-geheugen op Hallo VM.

**NIC's**: Hallo aantal NIC's op Hallo VM.

**Type opstarten**: het opstarten type Hallo VM is. Dit kan BIOS of EFI zijn. Op dit moment ondersteunt Azure Site Recovery alleen BIOS-opstarttypen. Alle Hallo virtuele machines van het type van EFI-opstarten worden vermeld in het werkblad voor niet-compatibele virtuele machines.

**Type besturingssysteem**: Hallo Hallo VM type besturingssysteem is. Dit kan Windows, Linux of een ander besturingssysteem zijn.


## <a name="site-recovery-limits"></a>Site Recovery-limieten

**Beoogde replicatieopslag** | **Gemiddelde I/O-grootte van bronschijf** |**Gemiddeld gegevensverloop van bronschijf** | **Totale gegevensverloop van bronschijf per dag**
---|---|---|---
Standard Storage | 8 kB | 2 Mbps | 168 GB per schijf
Premium P10-schijf | 8 kB | 2 Mbps | 168 GB per schijf
Premium P10-schijf | 16 kB | 4 Mbps | 336 GB per schijf
Premium P10-schijf | 32 kB of meer | 8 MBps | 672 GB per schijf
Premium P20- of P30-schijf | 8 kB  | 5 Mbps | 421 GB per schijf
Premium P20- of P30-schijf | 16 kB of meer |10 Mbps | 842 GB per schijf

Dit zijn gemiddelden uitgaande van een I/O-overlapping van 30%. Site Recovery kan een hogere doorvoer verwerken op basis van overlappingsverhouding, grotere schrijfgrootten en daadwerkelijk workload-I/O-gedrag. Hallo voorgaande cijfers wordt ervan uitgegaan dat een typische achterstand van ongeveer vijf minuten. Dat wil zeggen dat de gegevens na het uploaden binnen vijf minuten worden verwerkt en er een herstelpunt is gemaakt.

Deze limieten zijn gebaseerd op onze tests, maar dekken niet alle mogelijke toepassings-I/O-combinaties. De werkelijke resultaten kunnen variëren op basis van uw toepassings-I/O-combinatie. Voor de beste resultaten, zelfs na de implementatie plannen, altijd wordt aangeraden dat u uitgebreide toepassing testen met behulp van een failover tooget Hallo waar prestaties testafbeelding uitvoert.

## <a name="updating-hello-deployment-planner"></a>Hallo implementatie planner bijwerken
tooupdate hello implementatie planner Hallo te volgen:

1. Download de nieuwste versie Hallo Hallo [Azure Site Recovery implementatie planner](https://aka.ms/asr-deployment-planner).

2. Kopiëren Hallo .zip map tooa server die u wilt dat toorun op.

3. Pak de map .zip Hallo.

4. Hallo volgende doen:
 * Als de meest recente versie Hallo een profilering oplossing bevat geen en profilering al uitgevoerd op uw huidige versie van de planner hello wordt, blijven Hallo profilering.
 * Als de meest recente versie Hallo een profilering fix bevat, raden wij profilering op uw huidige versie te beëindigen Hallo profilering met de nieuwe versie Hallo opnieuw.

  >[!NOTE]
  >
  >Wanneer u met Hallo nieuwe versie, pass Hallo dat hetzelfde pad naar map uitvoer begint zodat hello hulpprogramma voegt profielgegevens op profilering Hallo bestaande bestanden. Een volledige set gegevens profiel worden toogenerate Hallo rapport gebruikt. Als u een andere uitvoermap doorgeven, nieuwe bestanden gemaakt en oud profiel gegevens wordt niet gebruikt toogenerate Hallo rapport.
  >
  >Elke nieuwe implementatie-planner is een cumulatieve update van Hallo ZIP-bestand. U hoeft niet toocopy Hallo nieuwste bestanden toohello vorige map. U kunt een nieuwe map maken en deze gebruiken.


## <a name="version-history"></a>Versiegeschiedenis

### <a name="131"></a>1.3.1
Bijgewerkt: 19 juli 2017

De volgende nieuwe functie is toegevoegd:

* Er is ondersteuning toegevoegd voor grote schijven (> 1 TB) bij het genereren van rapporten. U kunt nu implementatie planner tooplan replicatie voor virtuele machines die groter is dan 1 TB (maximaal 4095 GB) schijfgrootten hebben.
Meer informatie over [ondersteuning voor grote schijven in Azure Site Recovery](https://azure.microsoft.com/en-us/blog/azure-site-recovery-large-disks/)


### <a name="13"></a>1.3
Bijgewerkt: 9 mei 2017

De volgende nieuwe functie is toegevoegd:

* Toegevoegd is ondersteuning voor beheerde schijven bij het genereren van rapporten. Hallo aantal virtuele machines kan worden geplaatst tooa één opslag-account is berekende op basis van als schijf wordt beheerd voor Failover en testen failover is geselecteerd.        


### <a name="12"></a>1.2
Bijgewerkt: 7 april 2017

De volgende oplossingen zijn toegevoegd:

* Toegevoegde opstarten type (BIOS- of EFI) controleren op elke virtuele machine toodetermine of Hallo virtuele machine is compatibel of niet compatibel voor Hallo-beveiliging.
* Toegevoegde OS-type-informatie voor elke virtuele machine in Hallo compatibele virtuele machines en werkbladen voor niet-compatibele virtuele machines.
* Hallo GetThroughput bewerking wordt nu ondersteund in US Government en Microsoft Azure voor China Hallo-regio's.
* Er zijn meer controles op vereisten toegevoegd voor vCenter en ESXi Server.
* Onjuiste rapport is ophalen gegenereerd als de landinstellingen toonon Engels is ingesteld.


### <a name="11"></a>1.1
Bijgewerkt: 9 maart 2017

Vaste Hallo problemen te volgen:

* Hallo-hulpprogramma kan geen virtuele machines profiel als Hallo vCenter twee heeft of meer virtuele machines met dezelfde naam of IP-adres Hallo over verschillende ESXi-hosts.
* Kopiëren en zoeken is voor Hallo compatibel VM's en niet-compatibele virtuele machines werkbladen uitgeschakeld.

### <a name="10"></a>1.0
Bijgewerkt: 23 februari 2017

Openbare preview van Azure Site Recovery implementatie Planner 1.0 heeft Hallo volgende bekende problemen (toobe in toekomstige updates verholpen):

* Hallo hulpprogramma werkt alleen voor scenario's voor VMware naar Azure, niet voor Hyper-V-Azure-implementaties. Gebruik voor scenario's met Hyper-V-Azure Hallo [Capaciteitsplanner voor Hyper-V](./site-recovery-capacity-planning-for-hyper-v-replication.md).
* Hallo GetThroughput bewerking wordt niet ondersteund in US Government en Microsoft Azure voor China Hallo-regio's.
* Hallo-hulpprogramma kan geen virtuele machines profiel als Hallo vCenter-server twee heeft of meer virtuele machines met dezelfde naam of IP-adres Hallo over verschillende ESXi-hosts. In deze versie Hallo hulpprogramma wordt overgeslagen voor dubbele VM-namen of IP-adressen in Hallo VMListFile profilering. Hallo tijdelijke oplossing is tooprofile Hallo virtuele machines met behulp van een ESXi-host in plaats van Hallo vCenter-server. U moet voor elke ESXi-host één exemplaar uitvoeren.

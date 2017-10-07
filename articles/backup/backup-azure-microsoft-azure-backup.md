---
title: aaaUse Azure Backup-Server tooback up werkbelastingen tooAzure | Microsoft Docs
description: Azure Backup-Server tooprotect gebruiken of back-up van werkbelastingen toohello Azure-portal.
services: backup
documentationcenter: 
author: PVRK
manager: shivamg
editor: 
keywords: Azure Backup-server; beveiligen van workloads; back-up van werkbelastingen
ms.assetid: e7fb1907-9dc1-4ca1-8c61-50423d86540c
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/20/2017
ms.author: masaran;trinadhk;pullabhk;markgal
ms.openlocfilehash: a99b2919ffd44c6133960e3a935038a2bb1281c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="preparing-tooback-up-workloads-using-azure-backup-server"></a>Tooback van de werkbelasting met behulp van Azure Backup-Server voorbereiden
> [!div class="op_single_selector"]
> * [Azure Backup Server](backup-azure-microsoft-azure-backup.md)
> * [SCDPM](backup-azure-dpm-introduction.md)
>
>

Dit artikel wordt uitgelegd hoe tooprepare uw omgeving tooback van de werkbelasting met behulp van Azure Backup-Server. U kunt de toepassing werkbelastingen zoals Hyper-V-machines, Microsoft SQL Server, SharePoint Server, Microsoft Exchange en Windows-clients vanuit één console beveiligen met Azure Backup-Server.

> [!NOTE]
> Azure Backup-Server kan de VMware-machines nu beveiligen en biedt mogelijkheden voor betere beveiliging. Hallo-product te installeren, zoals uitgelegd in Hallo secties hieronder; Update 1 toepassen en Hallo meest recente Azure Backup Agent. toolearn meer informatie over back-ups van VMware-servers met Azure Backup-Server, Zie Hallo artikel [tooback gebruik Azure back-upserver van een server met VMware](backup-azure-backup-server-vmware.md). toolearn over de beveiligingsmogelijkheden van de te verwijzen[Azure-back-beveiliging biedt documentatie](backup-azure-security-feature.md).
>
>

U kunt ook infrastructuur beveiligen als een Service (IaaS) werkbelastingen, zoals virtuele machines in Azure.

> [!NOTE]
> Azure heeft twee implementatiemodellen voor het maken en werken met resources: [Resource Manager en classic](../azure-resource-manager/resource-manager-deployment-model.md). Dit artikel bevat Hallo informatie en procedures voor het herstellen van virtuele machines die zijn geïmplementeerd met behulp van Hallo Resource Manager-model.
>
>

Azure Backup-Server neemt veel van de back-functionaliteit voor Hallo werkbelasting van Data Protection Manager (DPM). In dit artikel koppelingen tooDPM documentatie tooexplain enkele Hallo gedeelde functionaliteit. Hoewel Azure Backup-Server veel Hallo deelt dezelfde functionaliteit als DPM. Azure Backup-Server heeft geen back-up tootape of is deze dan geïntegreerd met System Center.

## <a name="1-choose-an-installation-platform"></a>1. Kies een installatieplatform
de eerste stap Hallo naar slag hello Azure Backup-Server is tooset van een Windows-Server. Uw server worden in Azure of on-premises.

### <a name="using-a-server-in-azure"></a>Gebruik van een server in Azure
Bij het kiezen van een server voor het uitvoeren van Azure Backup-Server, kunt dat u beginnen met een afbeelding van Windows Server 2012 R2 Datacenter. Hallo-artikel [uw eerste virtuele Windows-machine maken in Azure-portal Hallo](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json), biedt een zelfstudie voor aan de slag met Hallo virtuele machine in Azure aanbevolen, zelfs als u nooit Azure al eerder hebt gebruikt. Hallo aanbevolen minimale vereisten voor een virtuele machine (VM) voor Hallo server moet: A2 Standard met twee kernen en 3.5 GB RAM-geheugen.

Werklasten beveiligen met Azure Backup-Server heeft veel nuances. Hallo-artikel [DPM installeren als een virtuele machine van Azure](https://technet.microsoft.com/library/jj852163.aspx), helpt deze nuances uitgelegd. Lees dit artikel volledig voordat het Hallo-machine is geïmplementeerd.

### <a name="using-an-on-premises-server"></a>Met behulp van een on-premises server
Als u niet dat toorun Hallo base-server in Azure wilt, kunt u Hallo-server kunt uitvoeren op een Hyper-V-machine, een VMware-VM of een fysieke host. Hallo aanbevolen minimale vereisten voor de serverhardware Hallo zijn twee kernen en 4 GB RAM-geheugen. Hallo ondersteunde besturingssystemen worden vermeld in de volgende tabel Hallo:

| Besturingssysteem | Platform | SKU |
|:--- | --- |:--- |
| Windows Server 2012 R2 en de meest recente SP's |64 bits |Standard, Datacenter, Foundation |
| Windows Server 2012 en de meest recente SP's |64 bits |Datacenter, Foundation, Standard |
| Windows Storage Server 2012 R2 en de meest recente SP's |64 bits |Standard, Workgroup |
| Windows Storage Server 2012 en de meest recente SP's |64 bits |Standard, Workgroup |

U kunt Hallo DPM-opslag met behulp van Windows Server-Ontdubbeling ontdubbelen. Meer informatie over het [DPM en Ontdubbeling](https://technet.microsoft.com/library/dn891438.aspx) samenwerken als geïmplementeerd in Hyper-V-machines.

> [!NOTE]
> Azure Backup-Server is ontworpen toorun op een speciale server met één doel. U kunt Azure Backup-Server niet installeren op:
> - Een computer die als een domeincontroller
> - Een computer op welke Hallo Application Server-rol is geïnstalleerd
> - Een computer die een System Center Operations Manager-beheerserver
> - Een computer waarop Exchange Server wordt uitgevoerd
> - Een computer die een knooppunt van een cluster

Altijd lid te worden van domein van Azure Backup-Server tooa. Als u van plan toomove Hallo server tooa ander domein bent, is het raadzaam om lid te maken van Hallo server toohello nieuw domein voordat u Azure Backup-Server installeert. Het verplaatsen van een bestaande back-upserver van Azure machine tooa nieuw domein nadat implementatie *niet ondersteund*.

## <a name="2-recovery-services-vault"></a>2. Recovery Services-kluis
Of u back-upgegevens tooAzure verzenden of lokaal houden, moet Hallo software tooAzure toobe verbonden. toobe meer specifiek, hello Azure Backup-Server-machine moet toobe geregistreerd bij een recovery services-kluis.

toocreate een recovery services-kluis:

1. Meld u aan toohello [Azure-portal](https://portal.azure.com/).
2. Klik op het menu Hub Hallo **Bladeren** en typt u in de lijst met resources Hallo **Recovery Services**. Als u te typen begint, Hallo lijstfilters op basis van uw invoer. Klik op **Recovery Services-kluis**.

    ![Een Recovery Services-kluis maken, stap 1](./media/backup-azure-microsoft-azure-backup/open-recovery-services-vault.png) <br/>

    Hallo-lijst met Recovery Services-kluizen wordt weergegeven.
3. Op Hallo **Recovery Services-kluizen** menu, klikt u op **toevoegen**.

    ![Een Recovery Services-kluis maken, stap 2](./media/backup-azure-microsoft-azure-backup/rs-vault-menu.png)

    Hallo Recovery Services vault blade wordt geopend, waarin u wordt gevraagd tooprovide een **naam**, **abonnement**, **resourcegroep**, en **locatie**.

    ![Een Recovery Services-kluis maken, stap 5](./media/backup-azure-microsoft-azure-backup/rs-vault-attributes.png)
4. Voor **naam**, voer een beschrijvende naam tooidentify Hallo-kluis. de naam van de Hallo moet toobe unieke voor hello Azure-abonnement. Typ een naam die tussen 2 en 50 tekens bevat. De naam moet beginnen met een letter en mag alleen letters, cijfers en afbreekstreepjes bevatten.
5. Klik op **abonnement** toosee Hallo lijst met beschikbare abonnementen. Als u niet zeker weet welk abonnement toouse Hallo standaard gebruiken (of voorgestelde) abonnement. Er zijn alleen meerdere mogelijkheden als uw organisatieaccount is gekoppeld aan meerdere Azure-abonnementen.
6. Klik op **resourcegroep** toosee Hallo beschikbare lijst met resourcegroepen, of klik op **nieuw** toocreate een nieuwe resourcegroep. Zie [Overzicht van Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) voor meer informatie over resourcegroepen.
7. Klik op **locatie** tooselect Hallo geografische regio voor Hallo kluis.
8. Klik op **Create**. Het kan even duren voordat Hallo Recovery Services-kluis toobe gemaakt. Hallo statusmeldingen Hallo rechtsboven in de portal Hallo bewaken.
   Zodra uw kluis is gemaakt, wordt het in de portal Hallo geopend.

### <a name="set-storage-replication"></a>Opslagreplicatie instellen
optie voor opslagreplicatie Hallo kunt u toochoose tussen geografisch redundante opslag en lokaal redundante opslag. Uw kluis heeft standaard geografisch redundante opslag. Als deze kluis uw primaire kluis is, laat u Hallo opslag optie set toogeo-redundante opslag. Kies lokaal redundante opslag als u een goedkopere optie wilt die niet zo duurzaam is. Lees meer over [geografisch redundante](../storage/common/storage-redundancy.md#geo-redundant-storage) en [lokaal redundante](../storage/common/storage-redundancy.md#locally-redundant-storage) opslagopties in Hallo [overzicht van Azure Storage-replicatie](../storage/common/storage-redundancy.md).

replicatie-instelling voor tooedit Hallo opslag

1. Selecteer uw kluis tooopen hello kluisdashboard en de blade instellingen Hallo. Als hello **instellingen** blade niet wordt geopend, klikt u op **alle instellingen** in Hallo kluisdashboard.
2. Op Hallo **instellingen** blade, klikt u op **back-upinfrastructuur** > **back-upconfiguratie** tooopen hello **back-upconfiguratie** blade. Op Hallo **back-upconfiguratie** blade Hallo optie voor opslagreplicatie voor uw kluis kiezen.

    ![Lijst met back-upkluizen](./media/backup-azure-vms-first-look-arm/choose-storage-configuration-rs-vault.png)

    Nadat u hebt gekozen Hallo opslagoptie voor uw kluis, bent u klaar tooassociate Hallo VM met Hallo kluis. toobegin Hallo-koppeling, die u moet detecteren en registreren Hallo van virtuele machines in Azure.

## <a name="3-software-package"></a>3. Softwarepakket
### <a name="downloading-hello-software-package"></a>Hallo softwarepakket downloaden
1. Meld u aan toohello [Azure-portal](https://portal.azure.com/).
2. Als u al een Recovery Services-kluis openen, gaat u verder toostep 3. Als u geen een Recovery Services-kluis is geopend hebt, maar in hello Azure-portal op Hallo Hub-menu zijn, klikt u op **Bladeren**.

   * Typ in de lijst met resources Hallo **Recovery Services**.
   * Als u te typen begint, Hallo lijst gefilterd op basis van uw invoer. Wanneer **Recovery Services-kluizen** wordt weergegeven, klikt u erop.

     ![Een Recovery Services-kluis maken, stap 1](./media/backup-azure-microsoft-azure-backup/open-recovery-services-vault.png)

     Hallo-lijst met Recovery Services-kluizen wordt weergegeven.
   * Selecteer in Hallo lijst met Recovery Services-kluizen een kluis.

     Hallo geselecteerde kluisdashboard wordt geopend.

     ![Blade Kluis openen](./media/backup-azure-microsoft-azure-backup/vault-dashboard.png)
3. Hallo **instellingen** blade wordt geopend standaard. Als dit is gesloten, klikt u op **instellingen** blade tooopen Hallo-instellingen.

    ![Blade Kluis openen](./media/backup-azure-microsoft-azure-backup/vault-setting.png)
4. Klik op **back-up** tooopen Hallo wizard aan de slag.

    ![Back-up aan de slag](./media/backup-azure-microsoft-azure-backup/getting-started-backup.png)

    In Hallo **aan de slag met back-up** blade die wordt geopend, **back-doelen** worden automatisch geselecteerd.

    ![Back-up-doelen-standaard-geopend](./media/backup-azure-microsoft-azure-backup/getting-started.png)

5. In Hallo **back-updoel** blade van Hallo **waar wordt uw workload uitgevoerd** selecteert u **On-premises**.

    ![on-premises en werkbelastingen als doelstellingen](./media/backup-azure-microsoft-azure-backup/backup-goals-azure-backup-server.png)

    Van Hallo **wat wilt u wilt dat toobackup?** vervolgkeuzelijst, selecteer Hallo werkbelastingen u wilt tooprotect met behulp van Azure Backup-Server en klik vervolgens op **OK**.

    Hallo **aan de slag met back-up** wizard switches Hallo **infrastructuur voorbereiden** optie tooback up tooAzure werkbelastingen.

   > [!NOTE]
   > Als u wilt dat alleen tooback van bestanden en mappen, raden wij aan hello Azure backup-agent en Hallo-instructies in het Hallo-artikel [eerste kennismaking: Maak een back-up van bestanden en mappen](backup-try-azure-backup-in-10-mins.md). Als u tooprotect gaat meer dan de bestanden en mappen of u van plan bent tooexpand Hallo beveiliging moet in de toekomst hello, selecteer deze werkbelastingen.
   >
   >

    ![Getting Started wizard wijzigen](./media/backup-azure-microsoft-azure-backup/getting-started-prep-infra.png)

6. In Hallo **infrastructuur voorbereiden** blade wordt geopend, klikt u op Hallo **downloaden** koppelingen voor Azure Backup-Server installeren en de kluisreferenties downloaden. U referenties voor de kluis hello gebruiken tijdens de registratie van Azure Backup-Server toohello recovery services-kluis. Hallo koppelingen komt u toohello van Downloadcentrum waar hello softwarepakket kan worden gedownload.

    ![Infrastructuur voorbereiden voor Azure Backup-Server](./media/backup-azure-microsoft-azure-backup/azure-backup-server-prep-infra.png)

7. Selecteer alle Hallo-bestanden en klik op **volgende**. Alle bestanden afkomstig van Microsoft Azure Backup-downloadpagina Hallo Hallo gedownload en plaats die alle bestanden in Hallo Hallo dezelfde map.

    ![Download center 1](./media/backup-azure-microsoft-azure-backup/downloadcenter.png)

    Omdat hello downloadgrootte van alle Hallo-bestanden samen > 3G, op een 10 Mbps downloadkoppeling die het too60 kan duren downloaden minuten Hallo toocomplete.

### <a name="extracting-hello-software-package"></a>Hallo softwarepakket uitpakken
Nadat u alle Hallo-bestanden hebt gedownload, klikt u op **MicrosoftAzureBackupInstaller.exe**. Hiermee start u Hallo **Wizard Setup van Microsoft Azure Backup** tooextract Hallo installatiebestanden tooa locatie door u opgegeven. Hallo wizard vervolgen, en klik op Hallo **extraheren** knop toobegin Hallo uitpakken gestart.

> [!WARNING]
> Ten minste 4GB aan vrije ruimte is vereist tooextract Hallo setup-bestanden.
>
>

![Back-installatiewizard voor Microsoft Azure](./media/backup-azure-microsoft-azure-backup/extract/03.png)

Eenmaal Hallo uitpakken worden voltooid selectievakje Hallo vak toolaunch Hallo vers uitgepakt *setup.exe* toobegin Microsoft Azure Backup-Server installeren en klik op Hallo **voltooien** knop.

### <a name="installing-hello-software-package"></a>Hallo softwarepakket installeren
1. Klik op **Microsoft Azure Backup** toolaunch Hallo-installatiewizard.

    ![Back-installatiewizard voor Microsoft Azure](./media/backup-azure-microsoft-azure-backup/launch-screen2.png)
2. Klik op het welkomstscherm Hallo Hallo **volgende** knop. Hiermee gaat u toohello *vereiste controleert* sectie. Klik op dit scherm **controleren** toodetermine als Hallo hardware en software-vereisten voor Azure Backup-Server wordt voldaan. Als aan alle vereisten zijn voldaan is, ziet u een bericht weergegeven dat aangeeft dat machine Hallo Hallo voldoet. Klik op Hallo **volgende** knop.

    ![Azure Backup-Server - welkomstpagina en de vereisten controleren](./media/backup-azure-microsoft-azure-backup/prereq/prereq-screen2.png)
3. Microsoft Azure Backup-Server vereist dat SQL Server Standard en hello Azure Backup-Server-installatiepakket wordt geleverd met Hallo geschikte SQL Server binaire bestanden die nodig zijn. Wanneer u start met een nieuwe installatie van de Azure Backup-Server, kiest u Hallo optie **nieuw exemplaar van SQL Server installeren met deze installatie** en klik op Hallo **controleren en installeren** knop. Zodra het Hallo-vereisten zijn geïnstalleerd, klikt u op **volgende**.

    ![Azure Backup-Server - controle van SQL](./media/backup-azure-microsoft-azure-backup/sql/01.png)

    Als een fout met een aanbeveling toorestart Hallo-machine optreedt, doen en klikt u op **opnieuw controleren**.

   > [!NOTE]
   > Azure Backup-Server komt niet overeen met een extern exemplaar van SQL Server. Hallo-exemplaar wordt gebruikt door Azure Backup-Server moet lokale toobe.
   >
   >
4. Geef een locatie voor het Hallo-installatie van bestanden van Microsoft Azure Backup-server en klik op **volgende**.

    ![Back-PreReq2 van Microsoft Azure](./media/backup-azure-microsoft-azure-backup/space-screen.png)

    Hallo scratchruimte locatie is een vereiste voor back-up tooAzure. Zorg ervoor dat Hallo scratchruimte locatie is ten minste 5% van de gegevens Hallo geplande back-up toohello cloud toobe. Voor bescherming van de schijf moeten afzonderlijke schijven toobe geconfigureerd wanneer de Hallo-installatie is voltooid. Zie voor meer informatie over opslaggroepen [Configureer de opslaggroepen en schijfruimte](https://technet.microsoft.com/library/hh758075.aspx).
5. Geef een sterk wachtwoord voor beperkte lokale gebruikersaccounts en klik op **volgende**.

    ![Back-PreReq2 van Microsoft Azure](./media/backup-azure-microsoft-azure-backup/security-screen.png)
6. Kies of u toouse wilt *Microsoft Update* toocheck voor updates en klik op **volgende**.

   > [!NOTE]
   > U wordt aangeraden met Windows Update u tooMicrosoft Update beveiligingsupdates en belangrijke updates voor Windows en andere producten, zoals Microsoft Azure Backup-Server biedt.
   >
   >

    ![Back-PreReq2 van Microsoft Azure](./media/backup-azure-microsoft-azure-backup/update-opt-screen2.png)
7. Bekijk Hallo *samenvatting van instellingen* en klik op **installeren**.

    ![Back-PreReq2 van Microsoft Azure](./media/backup-azure-microsoft-azure-backup/summary-screen.png)
8. Hallo installatie gebeurt in fasen. In de eerste fase Hallo Hallo is Microsoft Azure Recovery Services-Agent geïnstalleerd op Hallo-server. Hallo wizard controleert ook of de verbinding met Internet. Als de verbinding met Internet beschikbaar kunt u doorgaan met installatie, zo niet, moet u tooprovide proxy details tooconnect toohello Internet.

    de volgende stap Hallo is tooconfigure Hallo Microsoft Azure Recovery Services Agent. Als onderdeel van het Hallo-configuratie, hebt u tooprovide uw kluis referenties tooregister Hallo machine toohello recovery services kluis. U wordt ook een wachtwoordzin tooencrypt/ontsleutelen Hallo gegevens die worden verzonden tussen Azure en uw bedrijf opgeven. U kunt automatisch genereren van een wachtwoordzin of uw eigen minimaal 16 tekens wachtwoordzin opgeven. Ga door met Hallo wizard totdat het Hallo-agent is geconfigureerd.

    ![Azure Backup Serer PreReq2](./media/backup-azure-microsoft-azure-backup/mars/04.png)
9. Nadat de registratie van Hallo Microsoft Azure Backup-server is voltooid, voortgezet hello algehele installatiewizard toohello installatie en configuratie van SQL Server en hello Azure Backup-Server-onderdelen. Zodra Hallo installatie van SQL Server-onderdelen is voltooid, zijn hello Azure Backup-Server-onderdelen geïnstalleerd.

    ![Azure Backup-server](./media/backup-azure-microsoft-azure-backup/final-install/venus-installation-screen.png)

Wanneer Hallo installatiestap is voltooid, wordt hello bureaubladpictogrammen van het product gemaakt ook. Dubbelklik op Hallo pictogram toolaunch Hallo product.

### <a name="add-backup-storage"></a>Back-upopslag toevoegen
Hallo eerste back-up wordt opgeslagen op opslag die is gekoppeld toohello machine van Azure Backup-Server. Zie voor meer informatie over het toevoegen van schijven [Configureer de opslaggroepen en schijfruimte](https://technet.microsoft.com/library/hh758075.aspx).

> [!NOTE]
> Zelfs als u van plan toosend gegevens tooAzure bent moet u de back-upopslag tooadd. In de huidige architectuur van Azure Backup-Server Hallo hello Azure Backup-kluis bevat Hallo *tweede* kopie van Hallo gegevens terwijl de lokale opslag Hallo Hallo eerste (en verplichte) back-up bevat.
>
>

## <a name="4-network-connectivity"></a>4. Netwerkverbinding
Azure Backup-Server is connectiviteit toohello Azure Backup-service voor Hallo product toowork is vereist. toovalidate of Hallo machine Hallo connectiviteit tooAzure, heeft gebruiken Hallo ```Get-DPMCloudConnection``` cmdlet in hello Azure back-up Server PowerShell-console. Als hello uitvoer van de cmdlet Hallo TRUE is en vervolgens de verbinding is, anders er is geen netwerkverbinding.

Daarnaast hello Azure-abonnement moet op Hallo toobe in een foutloze toestand bevindt. toofind hello status van uw abonnement en toomanage het logboek in toohello [abonnement portal](https://account.windowsazure.com/Subscriptions).

Zodra u Hallo status van hello Azure connectiviteit en hello Azure-abonnement weet, kunt u onderstaande toofind uit Hallo impact Hallo-tabel op Hallo back-up/herstel functionaliteit beschikbaar wordt gesteld.

| Status connectiviteit | Azure-abonnement | Back-up tooAzure | Back-up toodisk | Herstellen van Azure | Herstellen van de schijf |
| --- | --- | --- | --- | --- | --- |
| Verbonden |Actief |Toegestaan |Toegestaan |Toegestaan |Toegestaan |
| Verbonden |Verlopen |Stopped |Stopped |Toegestaan |Toegestaan |
| Verbonden |Gemaakt |Stopped |Stopped |Gestopt en Azure herstelpunten verwijderd |Stopped |
| Verloren connectiviteit > 15 dagen |Actief |Stopped |Stopped |Toegestaan |Toegestaan |
| Verloren connectiviteit > 15 dagen |Verlopen |Stopped |Stopped |Toegestaan |Toegestaan |
| Verloren connectiviteit > 15 dagen |Gemaakt |Stopped |Stopped |Gestopt en Azure herstelpunten verwijderd |Stopped |

### <a name="recovering-from-loss-of-connectivity"></a>Herstellen van het verlies van verbinding
Als er een firewall of een proxy die toegang tooAzure houdt, moet u toowhitelist Hallo domein adressen in Hallo firewall/proxy-profiel te volgen:

* www.msftncsi.com
* \*.Microsoft.com
* \*.WindowsAzure.com
* \*.microsoftonline.com
* \*.windows.net

Als verbinding tooAzure herstelde toohello Azure Backup-Server-machine is, wordt Hallo-bewerkingen die kunnen worden uitgevoerd worden bepaald door hello Azure-abonnement staat. Hallo bovenstaande tabel bevat informatie over toegestaan wanneer een machine Hallo 'verbinding' Hallo-bewerkingen.

### <a name="handling-subscription-states"></a>Afhandeling van abonnementsstatussen
Het is mogelijk tootake een Azure-abonnement van een *verlopen* of *Deprovisioned* status toohello *Active* status. Maar dit sommige gevolgen heeft op Hallo product gedrag tijdens het Hallo-status is niet *Active*:

* Een *Deprovisioned* abonnement verliest functionaliteit voor Hallo periode dat deze is gemaakt. In te schakelen *Active*, Hallo functionaliteit van het product van de back-up/herstel wordt weer actief. back-upgegevens op de lokale schijf Hallo Hallo kunnen ook worden opgehaald als deze is gehouden met een groot genoeg bewaarperiode. Hallo back-upgegevens in Azure is echter onherstelbaar verloren zodra het Hallo-abonnement voert Hallo *Deprovisioned* status.
* Een *verlopen* functionaliteit voor het abonnement alleen verliest totdat deze is gemaakt *Active* opnieuw. Een geplande back-ups gedurende Hallo die Hallo abonnement is *verlopen* kan niet worden uitgevoerd.

## <a name="troubleshooting"></a>Problemen oplossen
Als u Microsoft Azure Backup-server is mislukt met fouten tijdens de installatiefase hello (of back-up of herstellen), raadpleegt u toothis [fout codes document](https://support.microsoft.com/kb/3041338) voor meer informatie.
U kunt ook te verwijzen[Azure Backup gerelateerde Veelgestelde vragen](backup-azure-backup-faq.md)

## <a name="next-steps"></a>Volgende stappen
U kunt gedetailleerde informatie ophalen over [uw omgeving voorbereiden voor DPM](https://technet.microsoft.com/library/hh758176.aspx) op Hallo Microsoft TechNet-website. Het bevat ook informatie over ondersteunde configuraties waarop Azure Backup-Server kan worden geïmplementeerd en gebruikt.

U kunt deze artikelen toogain een beter begrip van de beveiliging van werkbelastingen met behulp van Microsoft Azure Backup-server gebruiken.

* [Back-up van SQL Server](backup-azure-backup-sql.md)
* [Back-up van SharePoint server](backup-azure-backup-sharepoint.md)
* [Alternatieve server back-up](backup-azure-alternate-dpm-server.md)

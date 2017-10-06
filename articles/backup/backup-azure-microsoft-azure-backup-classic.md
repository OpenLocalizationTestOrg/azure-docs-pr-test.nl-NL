---
title: aaaUse Azure Backup-Server tooback van werkbelastingen tooAzure klassieke portal | Microsoft Docs
description: Zorg ervoor dat uw omgeving is tooback van de werkbelasting met behulp van Azure Backup-Server juist is voorbereid
services: backup
documentationcenter: 
author: pvrk
manager: shivamg
editor: 
keywords: Azure Backup-server; back-upkluis
ms.assetid: d86450e8-da63-4283-8fd7-2ee629fa14ab
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: masaran;trinadhk;pullabhk;markgal
ms.openlocfilehash: 7b574824c448096e0c0ba74a872ab8f2a434f6a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="preparing-tooback-up-workloads-using-azure-backup-server"></a>Tooback van de werkbelasting met behulp van Azure Backup-Server voorbereiden
> [!div class="op_single_selector"]
> * [Azure Backup Server](backup-azure-microsoft-azure-backup.md)
> * [SCDPM](backup-azure-dpm-introduction.md)
> * [Azure Backup-Server (klassiek)](backup-azure-microsoft-azure-backup-classic.md)
> * [SCDPM (klassiek)](backup-azure-dpm-introduction-classic.md)
>
>

Dit artikel is over het voorbereiden van uw omgeving tooback van de werkbelasting met behulp van Azure Backup-Server. U kunt de toepassing werkbelastingen zoals Hyper-V-machines, Microsoft SQL Server, SharePoint Server, Microsoft Exchange en Windows-clients vanuit één console beveiligen met Azure Backup-Server.

> [!WARNING]
> Azure Backup-Server neemt over Hallo functionaliteit van Data Protection Manager (DPM) voor back-up werkbelasting. U vindt aanwijzers tooDPM-documentatie voor sommige van deze mogelijkheden. Echter Azure Backup-Server biedt geen beveiliging op tape of integreren met System Center.
>
>

## <a name="1-windows-server-machine"></a>1. Windows Server-machine
![step1](./media/backup-azure-microsoft-azure-backup/step1.png)

de eerste stap Hallo naar slag hello Azure Backup-Server is toohave een Windows Server-machine.

| Locatie | Minimale vereisten | Aanvullende instructies |
| --- | --- | --- |
| Azure |Virtuele machine van Azure IaaS<br><br>A2 Standaard: 2 kernen, 3.5GB RAM-geheugen |U kunt beginnen met een eenvoudige afbeelding van Windows Server 2012 R2 Datacenter. [IaaS-werkbelastingen met Azure Backup-Server (DPM) beveiligt](https://technet.microsoft.com/library/jj852163.aspx) veel nuances heeft. Zorg ervoor dat u Hallo artikel volledig gelezen voordat het Hallo-machine is geïmplementeerd. |
| On-premises |Hyper-V VM<br> VMWare-virtuele machine<br> of een fysieke host.<br><br>2 kernen en 4GB RAM-geheugen |U kunt Hallo DPM-opslag met behulp van Windows Server-Ontdubbeling ontdubbelen. Meer informatie over het [DPM en Ontdubbeling](https://technet.microsoft.com/library/dn891438.aspx) samenwerken als geïmplementeerd in Hyper-V-machines. |

> [!NOTE]
> Het verdient aanbeveling dat Azure Backup-Server worden geïnstalleerd op een computer met Windows Server 2012 R2 Datacenter. Veel Hallo vereisten zijn met de meest recente versie van besturingssysteem van Windows hello Hallo gedekt.
>
>

Als u van plan toojoin Azure Backup-Server tooa domein bent, verdient het aanbeveling Hallo fysieke server of virtuele machine toohello domein te koppelen voordat u hello Azure Backup-Server software installeert. Verplaatsen van een back-upserver van Azure tooa nieuw domein na implementatie *niet ondersteund*.

## <a name="2-backup-vault"></a>2. Back-upkluis
![step2](./media/backup-azure-microsoft-azure-backup/step2.png)

Of u back-upgegevens tooAzure verzenden of lokaal houden, moet hello Azure Backup-Server geregistreerd tooa kluis. Als u een nieuwe gebruiker in de Azure Backup en toouse Azure Backup-Server wilt, raadpleegt u hello Azure portal versie van dit artikel - [tooback van de werkbelasting met behulp van Azure Backup-Server voorbereiden](backup-azure-microsoft-azure-backup.md).

> [!IMPORTANT]
> Vanaf maart 2017, kunt u niet meer gebruiken Hallo klassieke portal toocreate Backup-kluizen.
> U kunt nu uw back-up kluizen tooRecovery Services-kluizen upgraden. Zie voor meer informatie artikel Hallo [upgraden van een back-up kluis tooa Recovery Services-kluis](backup-azure-upgrade-backup-to-recovery-services.md). Microsoft raadt u tooupgrade uw back-upkluizen tooRecovery Services-kluizen.<br/> U kunt PowerShell toocreate Backup-kluizen niet gebruiken na 15 oktober 2017. **Per 1 november 2017**:
>- Alle resterende Backup-kluizen worden automatisch bijgewerkt tooRecovery Services-kluizen.
>- U niet kunt tooaccess uw back-upgegevens in de klassieke portal Hallo. In plaats daarvan gebruik hello Azure portal tooaccess uw back-upgegevens in Recovery Services-kluizen.
>



## <a name="3-software-package"></a>3. Softwarepakket
![stap 3](./media/backup-azure-microsoft-azure-backup/step3.png)

### <a name="downloading-hello-software-package"></a>Hallo softwarepakket downloaden
Vergelijkbare toovault referenties, kunt u Microsoft Azure Backup voor downloaden toepassingsworkloads van Hallo **pagina snel starten** van Hallo back-upkluis.

1. Klik op **voor Toepassingsworkloads (schijf tooDisk tooCloud)**. Hiermee gaat u toohello Downloadcentrum pagina uit het waar Hallo softwarepakket kan worden gedownload.

    ![Microsoft Azure Backup-welkomstscherm](./media/backup-azure-microsoft-azure-backup/dpm-venus1.png)
2. Klik op **Downloaden**.

    ![Download center 1](./media/backup-azure-microsoft-azure-backup/downloadcenter1.png)
3. Selecteer alle Hallo-bestanden en klik op **volgende**. Alle bestanden afkomstig van Microsoft Azure Backup-downloadpagina Hallo Hallo gedownload en plaats die alle bestanden in Hallo Hallo dezelfde map.
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
2. Klik op het welkomstscherm Hallo Hallo **volgende** knop. Hiermee gaat u toohello *vereiste controleert* sectie. Klik op dit scherm op Hallo **controleren** toodetermine knop als Hallo hardware en software-vereisten voor Azure Backup-Server wordt voldaan. Als alle Hallo vereisten is voldaan is, ziet u een bericht weergegeven dat aangeeft dat machine Hallo Hallo voldoet. Klik op Hallo **volgende** knop.

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

    de volgende stap Hallo is tooconfigure Hallo Microsoft Azure Recovery Services Agent. Als onderdeel van het Hallo-configuratie hebt u tooprovide uw Hallo kluis referenties tooregister Hallo machine toohello back-upkluis. U wordt ook een wachtwoordzin tooencrypt/ontsleutelen Hallo gegevens die worden verzonden tussen Azure en uw bedrijf opgeven. U kunt automatisch genereren van een wachtwoordzin of uw eigen minimaal 16 tekens wachtwoordzin opgeven. Ga door met Hallo wizard totdat het Hallo-agent is geconfigureerd.

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
![step4](./media/backup-azure-microsoft-azure-backup/step4.png)

Azure Backup-Server is connectiviteit toohello Azure Backup-service voor Hallo product toowork is vereist. toovalidate of Hallo machine Hallo connectiviteit tooAzure, heeft gebruiken Hallo ```Get-DPMCloudConnection``` commandlet in hello Azure back-up Server PowerShell-console. Als hello uitvoer van Hallo commandlet TRUE is en vervolgens de verbinding is, anders er is geen netwerkverbinding.

Daarnaast hello Azure-abonnement moet op Hallo toobe in een foutloze toestand bevindt. toofind hello status van uw abonnement en toomanage het logboek in toohello [abonnement portal](https://account.windowsazure.com/Subscriptions).

Zodra u Hallo status van hello Azure connectiviteit en hello Azure-abonnement weet, kunt u onderstaande toofind uit Hallo impact Hallo-tabel op Hallo back-up/herstel functionaliteit beschikbaar wordt gesteld.

| Status connectiviteit | Azure-abonnement | Back-tooAzure | Back-toodisk | Herstellen van Azure | Herstellen van de schijf |
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

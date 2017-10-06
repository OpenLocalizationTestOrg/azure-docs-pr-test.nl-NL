---
title: aaaUse DPM tooback van werkbelastingen tooAzure portal | Microsoft Docs
description: Een inleiding toobacking DPM-servers installeren met behulp van hello Azure Backup-service
services: backup
documentationcenter: 
author: adigan
manager: nkolli
editor: 
keywords: System Center Data Protection Manager, data protection manager, back-up van dpm
ms.assetid: c8c322cf-f5eb-422c-a34c-04a4801bfec7
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: adigan;giridham;jimpark;markgal;trinadhk
ms.openlocfilehash: 1dd988ae55012ac7dc485d2416458542c60b6ae3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="preparing-tooback-up-workloads-tooazure-with-dpm"></a>Tooback up werkbelastingen tooAzure met DPM wordt voorbereid
> [!div class="op_single_selector"]
> * [Azure Backup Server](backup-azure-microsoft-azure-backup.md)
> * [SCDPM](backup-azure-dpm-introduction.md)
> * [Azure Backup-Server (klassiek)](backup-azure-microsoft-azure-backup-classic.md)
> * [SCDPM (klassiek)](backup-azure-dpm-introduction-classic.md)
>
>

Dit artikel bevat een inleiding toousing Microsoft Azure Backup tooprotect uw System Center Data Protection Manager (DPM)-servers en werkbelastingen. Deze leest, moet u het volgende weten:

* De werking van Azure DPM-server back-up
* Hallo vereisten tooachieve een goede back-ervaring
* Hallo typische fouten zijn opgetreden en hoe toodeal met hen
* Ondersteunde scenario 's

> [!NOTE]
> Azure heeft twee implementatiemodellen voor het maken en werken met resources: [Resource Manager en classic](../azure-resource-manager/resource-manager-deployment-model.md). Dit artikel bevat Hallo informatie en procedures voor het herstellen van virtuele machines die zijn geïmplementeerd met behulp van Hallo Resource Manager-model.
>
>

System Center DPM een back-up bestand-en toepassingsgegevens. Gegevensback-ups tooDPM worden opgeslagen op tape op schijf of een back-up tooAzure bij Microsoft Azure Backup. DPM communiceert met Azure Backup als volgt:

* **DPM geïmplementeerd als een fysieke server of on-premises virtuele machine** — als DPM wordt geïmplementeerd als een fysieke server of als een lokale Hyper-V virtuele machine back-up van gegevens tooa Recovery Services-kluis bovendien toodisk en tapeback-up.
* **DPM geïmplementeerd als een virtuele machine van Azure** : van System Center 2012 R2 met Update 3, kan DPM worden geïmplementeerd als een virtuele machine van Azure. Als DPM wordt geïmplementeerd als een virtuele machine van Azure u kunt back-up van gegevens tooAzure schijven toohello DPM Azure virtuele machine gekoppeld of u kunt Hallo gegevensopslag offload van de door de back-up tooa die Recovery Services-kluis.

## <a name="why-backup-from-dpm-tooazure"></a>Waarom back-up van DPM tooAzure?
Hallo zakelijke voordelen van het gebruik van Azure Backup voor back-ups van DPM-servers zijn:

* Voor on-premises DPM-implementatie, kunt u Azure gebruiken als een alternatieve toolong termijn implementatie tootape.
* Voor implementaties van DPM in Azure kunt Azure Backup u toooffload opslag hello Azure-schijf, zodat u tooscale up door oudere gegevens zijn opgeslagen in de Recovery Services-kluis en nieuwe gegevens op schijf.

## <a name="prerequisites"></a>Vereisten
Azure Backup tooback up DPM-gegevens als volgt voorbereiden:

1. **Een Recovery Services-kluis maken** : een kluis maken in Azure portal.
2. **Kluisreferenties downloaden** : Hallo referenties waarmee u tooregister Hallo DPM server tooRecovery Services-kluis downloaden.
3. **Hello Azure Backup Agent installeren** — van Azure Backup Hallo-agent installeren op elke DPM-server.
4. **Hallo-server registreren** : Register Hallo DPM server tooRecovery Services-kluis.

### <a name="1-create-a-recovery-services-vault"></a>1. Een Recovery Services-kluis maken
toocreate een recovery services-kluis:

1. Meld u aan toohello [Azure-portal](https://portal.azure.com/).
2. Klik op het menu Hub Hallo **Bladeren** en typt u in de lijst met resources Hallo **Recovery Services**. Als u te typen begint, Hallo lijst gefilterd op basis van uw invoer. Klik op **Recovery Services-kluis**.

    ![Een Recovery Services-kluis maken, stap 1](./media/backup-azure-dpm-introduction/open-recovery-services-vault.png)

    Hallo-lijst met Recovery Services-kluizen wordt weergegeven.
3. Op Hallo **Recovery Services-kluizen** menu, klikt u op **toevoegen**.

    ![Een Recovery Services-kluis maken, stap 2](./media/backup-azure-dpm-introduction/rs-vault-menu.png)

    Hallo Recovery Services vault blade wordt geopend, waarin u wordt gevraagd tooprovide een **naam**, **abonnement**, **resourcegroep**, en **locatie**.

    ![Een Recovery Services-kluis maken, stap 5](./media/backup-azure-dpm-introduction/rs-vault-attributes.png)
4. Voor **naam**, voer een beschrijvende naam tooidentify Hallo-kluis. de naam van de Hallo moet toobe unieke voor hello Azure-abonnement. Typ een naam die tussen 2 en 50 tekens bevat. De naam moet beginnen met een letter en mag alleen letters, cijfers en afbreekstreepjes bevatten.
5. Klik op **abonnement** toosee Hallo lijst met beschikbare abonnementen. Als u niet zeker weet welk abonnement toouse Hallo standaard gebruiken (of voorgestelde) abonnement. Er zijn alleen meerdere mogelijkheden als uw organisatieaccount is gekoppeld aan meerdere Azure-abonnementen.
6. Klik op **resourcegroep** toosee Hallo beschikbare lijst met resourcegroepen, of klik op **nieuw** toocreate een nieuwe resourcegroep. Zie [Overzicht van Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) voor meer informatie over resourcegroepen.
7. Klik op **locatie** tooselect Hallo geografische regio voor Hallo kluis.
8. Klik op **Create**. Het kan even duren voordat Hallo Recovery Services-kluis toobe gemaakt. Hallo statusmeldingen Hallo rechtsboven in de portal Hallo bewaken.
   Zodra uw kluis is gemaakt, wordt het in de portal Hallo geopend.

### <a name="set-storage-replication"></a>Opslagreplicatie instellen
optie voor opslagreplicatie Hallo kunt u toochoose tussen geografisch redundante opslag en lokaal redundante opslag. Uw kluis heeft standaard geografisch redundante opslag. Laat Hallo optie set toogeo redundante opslag als dit uw primaire back-up. Kies lokaal redundante opslag als u een goedkopere optie wilt die niet zo duurzaam is. Lees meer over [geografisch redundante](../storage/common/storage-redundancy.md#geo-redundant-storage) en [lokaal redundante](../storage/common/storage-redundancy.md#locally-redundant-storage) opslagopties in Hallo [overzicht van Azure Storage-replicatie](../storage/common/storage-redundancy.md).

replicatie-instelling voor tooedit Hallo opslag

1. Selecteer uw kluis tooopen hello kluisdashboard en de blade instellingen Hallo. Als hello **instellingen** blade niet wordt geopend, klikt u op **alle instellingen** in Hallo kluisdashboard.
2. Op Hallo **instellingen** blade, klikt u op **back-upinfrastructuur** > **back-upconfiguratie** tooopen hello **back-upconfiguratie** blade. Op Hallo **back-upconfiguratie** blade Hallo optie voor opslagreplicatie voor uw kluis kiezen.

    ![Lijst met back-upkluizen](./media/backup-azure-vms-first-look-arm/choose-storage-configuration-rs-vault.png)

    Nadat u hebt gekozen Hallo opslagoptie voor uw kluis, bent u klaar tooassociate Hallo VM met Hallo kluis. toobegin Hallo-koppeling, die u moet detecteren en registreren Hallo van virtuele machines in Azure.

### <a name="2-download-vault-credentials"></a>2. Kluisreferenties downloaden
Hallo kluisreferentiebestand is een certificaat dat is gegenereerd door Hallo-portal voor elke back-upkluis. Hallo portal geüpload en Hallo openbare sleutel toohello Access Control Service (ACS). persoonlijke sleutel van certificaat Hallo Hallo wordt beschikbaar toohello gebruiker als onderdeel van het Hallo-werkstroom die is opgegeven als invoer in Hallo machine registratiewerkstroom gemaakt. Hiermee wordt geverifieerd Hallo machine toosend back-upgegevens tooan geïdentificeerd kluis in hello Azure Backup-service.

Hallo kluisreferentie wordt alleen gebruikt tijdens de registratiewerkstroom Hallo. Het is van de gebruiker Hallo verantwoordelijkheid tooensure die Hallo kluisreferenties bestand niet is geknoeid. Als het kluisreferentiebestand in handen Hallo van een rogue-gebruiker, Hallo kluisreferentiebestand kan worden gebruikt tooregister andere machines bij dezelfde kluis Hallo. Als de back-upgegevens Hallo is versleuteld met een wachtwoordzin die deel uitmaakt van de klant toohello, kan niet u bestaande back-upgegevens geschonden. toomitigate dit te voorkomen, de kluisreferenties tooexpire in 48hrs. U kunt Hallo kluisreferenties een recovery Services downloaden vaak – maar alleen Hallo nieuwste kluisreferentiebestand is van toepassing tijdens de registratiewerkstroom Hallo.

Hallo kluisreferentiebestand is gedownload via een beveiligd kanaal van hello Azure-portal. Hello Azure Backup-service is niet op de hoogte van de persoonlijke sleutel van certificaat Hallo Hallo en Hallo persoonlijke sleutel is niet permanent in het Hallo-portal of Hallo-service. Gebruik hello te volgen stappen toodownload Hallo kluis referentie bestand tooa lokale computer.

1. Meld u aan toohello [Azure-portal](https://portal.azure.com/).
2. Open Recovery Services-kluis toowhich toowhich gewenste tooregister DPM-machine.
3. Instellingenblade wordt standaard zijn geopend. Als dit is gesloten, klikt u op **instellingen** op de blade voor de kluis dashboard tooopen Hallo-instellingen. Op de blade instellingen, klikt u op **eigenschappen**.

    ![Blade Kluis openen](./media/backup-azure-dpm-introduction/vault-settings-dpm.png)
4. Klik op de pagina eigenschappen Hallo **downloaden** onder **back-up referenties**. Hallo portal genereert Hallo kluisreferentiebestand, die beschikbaar is gemaakt voor downloaden.

    ![Downloaden](./media/backup-azure-dpm-introduction/vault-credentials.png)

Hallo portal genereert een kluisreferentie met behulp van een combinatie van Hallo kluisnaam en Hallo huidige datum. Klik op **opslaan** toodownload Hallo kluis referenties toohello lokale account van de map downloads of selecteer OpslaanAls een van de Hallo Sla menu toospecify een locatie voor de kluisreferenties Hallo. Het duurt om tooa minuut voor Hallo bestand toobe gegenereerd.

### <a name="note"></a>Opmerking
* Zorg ervoor dat Hallo kluisreferentiebestand is opgeslagen op een locatie die toegankelijk is vanaf uw computer. Als deze is opgeslagen in een bestand share/SMB, controleert u de toegangsmachtigingen Hallo.
* Hallo kluisreferentiebestand wordt alleen gebruikt tijdens de registratiewerkstroom Hallo.
* Hallo kluisreferentiebestand na 48hrs verlopen en kan worden gedownload vanaf het Hallo-portal.

### <a name="3-install-backup-agent"></a>3. Back-Agent installeren
Nadat hello Azure Backup-kluis is gemaakt, moet een agent worden geïnstalleerd op elk van uw Windows-machines (Windows Server, Windows-client, System Center Data Protection Manager-server of Azure Backup-Server-machine) waarmee een back-up van gegevens en toepassingen tooAzure.

1. Open Recovery Services-kluis toowhich toowhich gewenste tooregister DPM-machine.
2. Instellingenblade wordt standaard zijn geopend. Als dit is gesloten, klikt u op **instellingen** blade tooopen Hallo-instellingen. Op de blade instellingen, klikt u op **eigenschappen**.

    ![Blade Kluis openen](./media/backup-azure-dpm-introduction/vault-settings-dpm.png)
3. Klik op de pagina instellingen Hallo **downloaden** onder **Azure Backup Agent**.

    ![Downloaden](./media/backup-azure-dpm-introduction/azure-backup-agent.png)

   Zodra het Hallo-agent wordt gedownload, dubbelklikt u op MARSAgentInstaller.exe toolaunch Hallo installatie van hello Azure Backup agent. Hallo-installatiemap en de tijdelijke map is vereist voor de agent Hallo kiezen. Hallo cachelocatie opgegeven moet vrije ruimte die ten minste 5% van de back-upgegevens Hallo hebben.
4. Als u een proxy server tooconnect toohello internet in Hallo **proxyconfiguratie** scherm, Voer Hallo proxy server-gegevens. Als u een geverifieerde proxyserver gebruikt, voert u Hallo naam en het wachtwoord gebruikersgegevens in dit scherm.
5. Hello Azure backup-agent installeert u .NET Framework 4.5 en Windows PowerShell (indien deze nog niet beschikbaar is) toocomplete Hallo installatie.
6. Zodra het Hallo-agent is geïnstalleerd, **sluiten** Hallo-venster.

   ![Sluiten](../../includes/media/backup-install-agent/dpm_FinishInstallation.png)
7. te**registreren Hallo DPM-Server** toohello kluis, in Hallo **Management** tabblad, klik op **Online**. Selecteer **registreren**. Hallo registreren installatiewizard wordt geopend.
8. Als u een proxy server tooconnect toohello internet in Hallo **proxyconfiguratie** scherm, Voer Hallo proxy server-gegevens. Als u een geverifieerde proxyserver gebruikt, voert u Hallo naam en het wachtwoord gebruikersgegevens in dit scherm.

    ![Proxy-configuratie](../../includes/media/backup-install-agent/DPM_SetupOnlineBackup_Proxy.png)
9. Blader in welkomstscherm kluis referenties, tooand Selecteer Hallo kluisreferentiebestand die eerder zijn gedownload.

    ![Referenties voor de kluis](../../includes/media/backup-install-agent/DPM_SetupOnlineBackup_Credentials.jpg)

    Hallo kluisreferentiebestand is alleen geldig voor 48 uur (nadat deze gedownload vanuit de portal Hallo). Als er een fout in dit scherm (bijvoorbeeld 'Vault referenties opgegeven bestand is verlopen'), aanmelding toohello Azure portal en download Hallo kluisreferentiebestand opnieuw.

    Zorg ervoor dat Hallo kluisreferentiebestand is beschikbaar in een locatie die toegankelijk zijn voor het Hallo-installatieprogramma. Als u toegang tot gerelateerde fouten Hallo kluis referenties tooa tijdelijke bestandslocatie op deze machine te kopiëren en probeer Hallo opnieuw.

    Als er een ongeldige kluis referentie-fout optreedt (bijvoorbeeld ' kluis ongeldige referenties opgegeven') Hallo-bestand is beschadigd of geen meest recente referenties die zijn gekoppeld aan de herstelservice Hallo hebben Hallo. Probeer opnieuw na het downloaden van een nieuw kluisreferentiebestand via de portal Hallo Hallo. Deze fout wordt doorgaans te zien of gebruiker op Hallo Hallo **kluisreferentie downloaden** optie in hello Azure-portal, snel achter elkaar. In dit geval wordt is alleen Hallo tweede kluisreferentiebestand geldig.
10. toocontrol hello gebruik van netwerkbandbreedte tijdens het werk en niet-werkuren, in Hallo **Beperkingsinstelling** scherm, u kunt limieten voor bandbreedtegebruik Hallo instellen en definiëren Hallo werk en niet-werk uren.

    ![Beperking van de instelling](../../includes/media/backup-install-agent/DPM_SetupOnlineBackup_Throttling.png)
11. In Hallo **herstel mapinstelling** scherm, blader voor Hallo map waar Hallo bestanden gedownload van Azure tijdelijk tijdelijk opgeslagen.

    ![Instellingen van de map Recovery](../../includes/media/backup-install-agent/DPM_SetupOnlineBackup_RecoveryFolder.png)
12. In Hallo **versleutelingsinstelling** scherm kunt u een wachtwoordzin genereren of geef een wachtwoordzin (minimaal 16 tekens). Houd er rekening mee toosave Hallo wachtwoordzin op een veilige locatie.

    ![Versleuteling](../../includes/media/backup-install-agent/DPM_SetupOnlineBackup_Encryption.png)

    > [!WARNING]
    > Als hello wachtwoordzin kwijtraakt of vergeet; Microsoft kan niet helpen bij het herstellen van back-upgegevens Hallo. Hallo gebruiker eigenaar is van Hallo-wachtwoordzin voor versleuteling en Microsoft heeft geen zichtbaarheid van Hallo wachtwoordzin die wordt gebruikt door de eindgebruiker Hallo. Sla Hallo-bestand op een veilige locatie als dit nodig tijdens een herstelbewerking wordt uitgevoerd is.
    >
    >
13. Nadat u op Hallo **registreren** knop, hello computer wordt geregistreerd met succes toohello kluis en u bent nu klaar toostart back-ups van tooMicrosoft Azure.
14. Als u Data Protection Manager, kunt u Hallo-instellingen die zijn opgegeven tijdens de registratiewerkstroom Hallo door te klikken op Hallo **configureren** optie door te selecteren **Online** onder Hallo  **Management** tabblad.

## <a name="requirements-and-limitations"></a>Vereisten (en beperkingen)
* DPM kan worden uitgevoerd als een fysieke server of een Hyper-V virtuele machine is geïnstalleerd op System Center 2012 SP1 of System Center 2012 R2. Kan ook worden uitgevoerd als een virtuele machine van Azure met System Center 2012 R2 met ten minste DPM 2012 R2 updatepakket 3 of een virtuele Windows-machine in VMWare uitgevoerd op System Center 2012 R2 met ten minste updatepakket 5.
* Als u DPM met System Center 2012 SP1 uitvoert moet u installeren Update Roll up 2 voor System Center Data Protection Manager SP1. Dit is vereist voordat u hello Azure Backup Agent kunt installeren.
* Hallo DPM-server moet Windows PowerShell en .net Framework 4.5 geïnstalleerd.
* DPM kan back-up van de meeste werkbelastingen tooAzure back-up. Voor een volledige lijst met wat is er Zie ondersteund hello Azure Backup ondersteunt de volgende items.
* Gegevens die zijn opgeslagen in Azure Backup kunnen niet worden hersteld met 'kopiëren tootape' Hallo-optie.
* U hebt een Azure-account nodig hello Azure Backup-functie is ingeschakeld. Als u geen account hebt, kunt u binnen een paar minuten een account voor de gratis proefversie maken. Meer informatie over [prijzen van Azure Backup](https://azure.microsoft.com/pricing/details/backup/).
* Hello Azure Backup Agent toobe geïnstalleerd op Hallo-servers die u tooback-up wilt maken met Azure Backup worden vereist. Elke server moet ten minste 5% van de grootte Hallo Hallo-gegevens die worden back-up, beschikbaar als lokale vrije opslagruimte hebben. Bijvoorbeeld, vereist een back-up 100 GB aan gegevens een minimum van 5 GB vrije ruimte op Hallo scratchruimte locatie.
* Gegevens worden opgeslagen in hello Azure kluis opslag. Hallo van een gegevensbron (bijvoorbeeld een virtuele machine of een database) mag niet groter zijn dan 54400 GB, maar er is geen limiet toohello bedrag van gegevens die u kunt back-ups tooan Azure Backup-kluis.

Deze bestandstypen worden ondersteund voor back-up tooAzure:

* Versleuteld (volledige back-ups alleen)
* Gecomprimeerd (incrementele back-ups ondersteund)
* Sparse (incrementele back-ups ondersteund)
* Gecomprimeerd en sparse (behandeld als Sparse)

En deze worden niet ondersteund:

* Servers op hoofdlettergevoelige bestandssystemen worden niet ondersteund.
* Vaste koppelingen (overgeslagen)
* Reparsepunten (overgeslagen)
* Versleuteld en gecomprimeerd (overgeslagen)
* Versleuteld en sparse (overgeslagen)
* Gecomprimeerde stream
* Sparse stream

> [!NOTE]
> Van in System Center 2012 DPM met SP1 en hoger u kunt back-up-werkbelastingen beveiligd met DPM tooAzure met Microsoft Azure Backup.
>
>

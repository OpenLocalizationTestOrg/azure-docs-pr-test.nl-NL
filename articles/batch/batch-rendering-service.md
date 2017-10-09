---
title: aaaUse hello opbouwen van Azure Batch service toorender in de cloud Hallo | Microsoft Docs
description: Taken rechtstreeks vanuit Maya renderen op virtuele Azure-machines en betalen op basis van per gebruik.
services: batch
author: tamram
manager: timlt
ms.service: batch
ms.topic: hero-article
ms.date: 07/31/2017
ms.author: tamram
ms.openlocfilehash: 3fb78d883311bbc3ab62743b7d1b111ffad177cd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-batch-rendering-service"></a>Aan de slag met Hallo opbouwen van de Batch-service

Hallo Rendering van Azure Batch-service biedt mogelijkheden voor cloud-scale-rendering op basis van betalen per gebruik. Hallo opbouwen van de Batch-service verwerkt taakplanning en wachtrij, het beheer van fouten en nieuwe pogingen en automatisch schalen voor uw taak weergeven. Hallo opbouwen van de Batch-service ondersteunt Autodesk Maya, 3ds Max en Arnold met ondersteuning voor andere toepassingen die binnenkort beschikbaar. Hallo-invoegtoepassing voor Maya 2017 Batch maakt het eenvoudig toostart een renderingjob op Azure vanaf uw bureaublad. 

## <a name="supported-applications"></a>Ondersteunde toepassingen

Hallo opbouwen van de Batch-service ondersteunt momenteel Hallo toepassingen te volgen:

- Autodesk Maya
- Autodesk 3ds Max
- Autodesk Arnold

## <a name="prerequisites"></a>Vereisten

toouse hello opbouwen van de Batch-service, moet u de:

- Een [Azure-account](https://azure.microsoft.com/free/). 
- **Een Azure Batch-account.** Zie voor instructies over het maken van een Batch-account in Azure-portal Hallo [een Batch-account maken met Azure-portal Hallo](batch-account-create-portal.md).
- Een **Azure Storage-account.** gebruikt voor uw renderingjob Hallo-activa zijn opgeslagen in Azure Storage. U kunt automatisch een opslagaccount maken bij het instellen van uw Batch-account. U kunt ook een bestaand opslagaccount gebruiken. toolearn meer informatie over de Storage-accounts, Zie [hoe toocreate, beheren of verwijderen van een opslagaccount in hello Azure-portal](https://docs.microsoft.com/azure/storage/storage-create-storage-account).

toouse hello Batch invoegtoepassing voor Maya, die u nodig:

- **Maya 2017**
- **Arnold voor Maya**

U kunt ook Hallo [Azure-portal](https://portal.azure.com) toocreate pools van virtuele machines die vooraf geconfigureerd met Maya, 3ds zijn Max en Arnold. U kunt Hallo portal toomonitor taken gebruiken en mislukte taken onderzoeken toepassingslogboeken downloaden en door tooindividual virtuele machines met RDP of SSH op afstand verbinding te maken.

## <a name="basic-batch-concepts"></a>Basisconcepten voor Batch

Voordat u met Hallo opbouwen van de Batch-service begint, is het handig toobe bekend zijn met een paar concepten van Batch, met inbegrip van rekenknooppunten, pools en jobs. Zie informatie over Azure Batch in het algemeen toolearn [intrinsiek parallelle workloads worden uitgevoerd met Batch](batch-technical-overview.md).

### <a name="pools"></a>Pools

Batch is een platformservice voor het uitvoeren van rekenintensief werk, zoals rendering, in een **pool** van **rekenknooppunten**. Elk rekenknooppunt in een pool is een virtuele Azure-machine (VM) met Linux of Windows. 

Zie voor meer informatie over Batch-pools en rekenknooppunten hello [groep](batch-api-basics.md#pool) en [rekenknooppunt](batch-api-basics.md#compute-node) secties in [ontwikkelen grootschalige parallelle compute-oplossingen met Batch](batch-api-basics.md).

### <a name="jobs"></a>Taken

Een Batch **taak** is een verzameling taken die worden uitgevoerd op Hallo rekenknooppunten in een pool. Wanneer u een taak rendering indient, Batch-taak Hallo verdeelt in taken en Hallo taken toohello rekenknooppunten in Hallo groep toorun distribueert.

Zie voor meer informatie over batchtaken Hallo [taak](batch-api-basics.md#job) in sectie [ontwikkelen grootschalige parallelle compute-oplossingen met Batch](batch-api-basics.md).

## <a name="use-hello-batch-plug-in-for-maya-toosubmit-a-render-job"></a>Hallo Batch invoegtoepassing gebruiken voor Maya toosubmit een taak weergeven

Met de Batch-invoegtoepassing voor Maya hello, kunt u een taak toohello opbouwen van de Batch-service vanaf Maya indienen. Hallo volgende secties wordt beschreven hoe tooconfigure taak in de invoegtoepassing Hallo Hallo en verzend het. 

### <a name="load-hello-batch-plug-in-in-maya"></a>Hallo Batch invoegtoepassing in Maya laden

Hallo invoegtoepassing Batch is beschikbaar op [GitHub](https://github.com/Azure/azure-batch-maya/releases). Pak Hallo archiefdirectory tooa van uw keuze. U kunt Hallo invoegtoepassing laden rechtstreeks vanuit Hallo *azure_batch_maya* directory.

tooload hello invoegtoepassing in Maya:

1. Voer Maya uit.
2. Open **Voorkeuren voor**  > **computervensterinstellingen** > **Invoegtoepassingenbeheer**.
3. Klik op **Bladeren**.
4. Navigeer tooand Selecteer *azure_batch_maya/plug-in/AzureBatch.py*.

### <a name="authenticate-access-tooyour-batch-and-storage-accounts"></a>Verifiëren van toegang tooyour Batch- en Storage-accounts

toouse Hallo invoegtoepassing, moet u tooauthenticate met uw Azure Batch en sleutels voor Azure Storage-account. tooretrieve uw sleutels account:

1. Weergave hello invoegtoepassing in Maya en selecteer Hallo **Config** tabblad.
2. Navigeer toohello [Azure-portal](https://portal.azure.com).
3. Selecteer **Batch-Accounts** in Hallo links menu. Klik indien nodig op **Meer services** en filter op _Batch_.
4. Hallo gewenst Batch-account niet vinden in het Hallo-lijst.
5. Selecteer Hallo **sleutels** menuopdracht toodisplay uw accountnaam, account-URL en toegangstoetsen:
    - Plak Hallo Batch-account-URL in Hallo **Service** veld Hallo Batch invoegtoepassing.
    - Plakken Hallo-accountnaam in Hallo **Batch-Account** veld.
    - Plakken Hallo primaire sleutel in Hallo **Batch sleutel** veld.
7. Selecteer de Storage-Accounts in Hallo links. Klik indien nodig op **Meer services** en filter op _Opslag_.
8. Hallo gewenst Storage-account niet vinden in het Hallo-lijst.
9. Selecteer Hallo **toegangstoetsen** menu-item toodisplay Hallo-opslag-accountnaam en sleutels.
    - Plakken Hallo opslagaccountnaam in Hallo **Opslagaccount** veld Hallo Batch invoegtoepassing.
    - Plakken Hallo primaire sleutel in Hallo **opslagsleutel** veld.
10. Klik op **verifiëren** tooensure die Hallo invoegtoepassing hebben toegang tot beide accounts.

Nadat u bent geverifieerd, Hallo Hallo invoegtoepassing sets statusveld te**geverifieerde**: 

![Uw Batch- en Storage-account verifiëren](./media/batch-rendering-service/authentication.png)

### <a name="configure-a-pool-for-a-render-job"></a>Een pool voor een renderingtaak configureren

Nadat u uw Batch- en Storage-account hebt geverifieerd, stelt u een pool in voor uw renderingtaak. Hallo invoegtoepassing Hiermee slaat u uw selecties tussen sessies. Zodra u de configuratie van uw voorkeur hebt ingesteld, hoeft u geen toomodify deze tenzij verandert.

Hallo volgende secties helpt u bij het Hallo beschikbare opties beschikbaar op Hallo **indienen** tabblad:

#### <a name="specify-a-new-or-existing-pool"></a>Een nieuwe of bestaande pool opgeven

toospecify een pool op welke toorun Hallo render taak, selecteer Hallo **indienen** tabblad. Dit tabblad biedt opties voor het maken van een pool of het selecteren van een bestaande pool:

- U kunt **automatisch inrichten van een groep voor deze taak** (Hallo standaardoptie). Als u deze optie kiest, Batch maakt Hallo groep uitsluitend bedoeld is voor de huidige taak Hallo en automatisch verwijderingen Hallo pool wanneer Hallo renderen taak is voltooid. Deze optie wordt aanbevolen wanneer u een taak één render toocomplete hebt.
- U kunt **een bestaande permanente pool opnieuw gebruiken**. Hebt u een bestaande toepassingen die niet actief is, kunt u die toepassingen voor actieve Hallo render taak opgeven door deze te selecteren in de vervolgkeuzelijst Hallo. Hallo tijd die nodig is tooprovision Hallo groep hergebruiken van een bestaande permanente toepassingen worden opgeslagen.  
- U kunt **een nieuwe permanente pool maken**. Als u deze optie kiest, maakt een nieuwe pool voor het Hallo-taak uitvoeren. Hallo-groep worden niet verwijderd wanneer het Hallo-taak is voltooid, zodat u het opnieuw voor toekomstige taken gebruiken kunt. Selecteer deze optie wanneer u een continue nodig toorun taken weergeven. Op de volgende taken kunt u selecteren **opnieuw gebruiken van een bestaande pool voor permanente** toouse Hallo permanente van toepassingen die u hebt gemaakt voor de eerste taak Hallo.

![Een pool, installatiekopie van het besturingssysteem, VM-grootte en licentie opgeven](./media/batch-rendering-service/submit.png)

Zie voor meer informatie over hoe de kosten voor Azure Virtual machines doorlopen, Hallo [Linux prijzen Veelgestelde vragen over](https://azure.microsoft.com/pricing/details/virtual-machines/linux/#faq) en [prijzen Veelgestelde vragen over Windows](https://azure.microsoft.com/pricing/details/virtual-machines/windows/#faq).

#### <a name="specify-hello-os-image-tooprovision"></a>Hallo OS-installatiekopie tooprovision opgeven

U kunt opgeven Hallo-type van OS-installatiekopie toouse tooprovision-rekenknooppunten in de groep Hallo op Hallo **Env** tabblad (omgeving). Batch ondersteunt momenteel Hallo opties voor de afbeelding voor het weergeven van taken te volgen:

|Besturingssysteem  |Installatiekopie  |
|---------|---------|
|Linux     |Batch CentOS Preview |
|Windows     |Batch Windows Preview |

#### <a name="choose-a-vm-size"></a>Een VM-grootte kiezen

U kunt de VM-grootte Hallo opgeven op Hallo **Env** tabblad. Zie [Linux VM-grootten in Azure](https://docs.microsoft.com/azure/virtual-machines/linux/sizes) en [Windows VM-grootten in Azure](https://docs.microsoft.com/azure/virtual-machines/windows/sizes) voor meer informatie over beschikbare VM-grootten. 

![Hallo VM OS-installatiekopie en de grootte opgeven op Hallo Env tabblad](./media/batch-rendering-service/environment.png)

#### <a name="specify-licensing-options"></a>Licentieopties opgeven

U kunt opgeven dat Hallo licenties die u wilt dat toouse op Hallo **Env** tabblad. Een aantal opties:

- **Maya**, dat standaard is ingeschakeld.
- **Arnold**, die als Arnold wordt gedetecteerd als Hallo active render-engine in Maya is ingeschakeld.

 Als u met behulp van uw eigen licentie toorender wenst, kunt u uw licentie-eindpunt configureren Hallo omgeving variabelen toohello tabel toe te voegen. Niet zeker toodeselect Hallo standaard licentie-opties als u doet dit.

> [!IMPORTANT]
> U wordt gefactureerd voor gebruik van licenties Hallo terwijl virtuele machines worden uitgevoerd in de groep hello, zelfs als Hallo virtuele machines op dit moment niet worden gebruikt voor de rendering. tooavoid extra kosten Navigeer toohello **Pools** tabblad en het formaat Hallo groep too0 knooppunten totdat u klaar toorun bent een andere render taak. 
>
>

#### <a name="manage-persistent-pools"></a>Permanente pools beheren

U kunt een bestaande permanente pool op Hallo beheren **Pools** tabblad. Een groep selecteren in lijst Hallo weergeven Hallo huidige status van Hallo-toepassingen

Van Hallo **Pools** tabblad ook Hallo-groep verwijderen en het aantal virtuele machines in de groep Hallo Hallo vergroten of verkleinen. U kunt de grootte van een groep too0 knooppunten tooavoid steeds kosten Between-werkbelastingen.

![Pools weergeven, vergroten of verkleinen en verwijderen](./media/batch-rendering-service/pools.png)

### <a name="configure-a-render-job-for-submission"></a>Een renderingtaak configureren voor verzending

Wanneer u hebt opgegeven Hallo parameters op voor het Hallo-groep die Hallo render taak wordt uitgevoerd, Hallo-taak zelf configureren. 

#### <a name="specify-scene-parameters"></a>Scène-parameters opgeven

Hallo Batch invoegtoepassing detecteert welke Afbeeldingsweergave-engine die u momenteel gebruikt in Maya en geeft Hallo toepasselijke instellingen op Hallo renderen **indienen** tabblad. Deze instellingen omvatten Hallo start frame, end-frame, uitvoer voorvoegsel en Framestap. U kunt Hallo scene bestand Renderinstellingen overschrijven door te geven van verschillende instellingen in het Hallo-invoegtoepassing. Wijzigingen die u aanbrengt toohello instellingen voor de invoegtoepassing zijn niet persistent gemaakte back toohello scene renderinstellingen, zodat u wijzigingen op basis van de taak met taak aanbrengen kunt zonder tooreupload Hallo scene bestand.

Hallo invoegtoepassing waarschuwt u als Hallo-engine die u hebt geselecteerd in Maya renderen wordt niet ondersteund.

Als u een nieuwe scene laden terwijl Hallo invoegtoepassing geopend is, klikt u op Hallo **vernieuwen** knop toomake ervoor Hallo instellingen worden bijgewerkt.

#### <a name="resolve-asset-paths"></a>Assetpaden omzetten

Wanneer u Hallo invoegtoepassing laadt, scant het Hallo-scènes bestand alle verwijzingen extern bestand. Deze referenties worden weergegeven in Hallo **activa** tabblad. Als een waarnaar wordt verwezen pad kan niet worden omgezet, probeert Hallo invoegtoepassing toolocate Hallo-bestand in enkele standaardlocaties, met inbegrip van:

- Hallo-locatie van Hallo scene-bestand 
- Hallo van het huidige project _sourceimages_ directory
- Hallo huidige werkmap. 

Als Hallo asset nog steeds kan niet gevonden worden, is het met een waarschuwingspictogram weergegeven:

![Ontbrekende assets worden weergegeven met een waarschuwingspictogram](./media/batch-rendering-service/missing_assets.png)

Als u Hallo-locatie van een verwijzing naar niet-omgezette bestand weet, kunt u Hallo waarschuwing pictogram toobe tooadd gevraagd een zoekpad. Hallo invoegtoepassing vervolgens gebruikt deze zoekopdracht pad tooattempt tooresolve eventuele ontbrekende activa. U kunt een willekeurig aantal aanvullende zoekpaden toevoegen.

Wanneer een verwijzing is omgezet, wordt deze weergegeven met een pictogram met een groen lampje:

![Omgezette assets weergeven met een pictogram met een groen lampje](./media/batch-rendering-service/found_assets.png)

Als uw scene andere bestanden vereist is die Hallo invoegtoepassing niet gedetecteerd, kunt u aanvullende bestanden of mappen toevoegen. Gebruik Hallo **bestanden toevoegen** en **map toevoegen** knoppen. Als u een nieuwe scene laadt terwijl Hallo invoegtoepassing geopend is, worden ervoor tooclick **vernieuwen** tooupdate Hallo scene verwijzingen.

#### <a name="upload-assets-tooan-asset-project"></a>Activa tooan asset project uploaden

Bestanden weergeven in Hallo wanneer dient u een taak render hello verwezen **activa** tabblad automatisch geüploade tooAzure opslag als een project actief zijn. U kunt ook uploaden Hallo assetbestanden onafhankelijk van een taak weergeven met behulp van Hallo **uploaden** knop op Hallo **activa** tabblad Hallo asset projectnaam is opgegeven in Hallo **Project**veld en wordt standaard na Hallo huidige Maya project de naam. Wanneer assetbestanden zijn geüpload, wordt de lokale bestandsstructuur Hallo bewaard. 

Na het uploaden kan door een willekeurig aantal renderingtaken naar assets worden verwezen. Alle geüploade activa zijn beschikbaar tooany taak die verwijst naar Hallo asset project, of ze zijn opgenomen in de scene Hallo of niet. toochange hello asset project waarnaar wordt verwezen door de volgende taak Hallo naam wijzigen in Hallo **Project** veld Hallo **activa** tabblad. Als er bestanden die u wenst dat tooexclude van uploaden waarnaar wordt verwezen, selectie met behulp van Hallo groene knop naast Hallo aanbieding.

#### <a name="submit-and-monitor-hello-render-job"></a>Dien en monitor Hallo taak weergeven

Nadat u Hallo render taak in Hallo invoegtoepassing hebt geconfigureerd, klikt u op Hallo **Submit Job** knop op Hallo **indienen** toosubmit Hallo taak tooBatch tabblad:

![Hallo render taak verzenden](./media/batch-rendering-service/submit_job.png)

U kunt een taak die wordt uitgevoerd van Hallo bewaken **taken** tabblad op Hallo invoegtoepassing. Selecteer een taak vanuit Hallo lijst toodisplay Hallo huidige status van Hallo-taak. U kunt ook dit tabblad toocancel gebruiken en verwijderen van taken, evenals toodownload Hallo uitvoer en logboeken weergeven. 

toodownload-uitvoer wijzigen Hallo **levert** veld tooset Hallo gewenste doelmap. Klik op Hallo tandwielpictogram pictogram toostart een achtergrondproces die Hallo taak controleert en downloadt uitvoer wanneer die: 

![Taakstatus bekijken en uitvoer downloaden](./media/batch-rendering-service/jobs.png)

U kunt Maya sluiten zonder het downloadproces Hallo verstoren.

## <a name="next-steps"></a>Volgende stappen

toolearn meer informatie over Batch, Zie [intrinsiek parallelle workloads worden uitgevoerd met Batch](batch-technical-overview.md).

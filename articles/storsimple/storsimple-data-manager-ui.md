---
title: aaaMicrosoft Azure StorSimple Data Manager UI | Microsoft Docs
description: Hierin wordt beschreven hoe toouse StorSimple Data Manager service UI (afgeschermd voorbeeld)
services: storsimple
documentationcenter: NA
author: vidarmsft
manager: syadav
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 11/22/2016
ms.author: vidarmsft
ms.openlocfilehash: b0ee12b3e495400b54e48eb1a98c68b1af2e5f7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-using-hello-storsimple-data-manager-service-ui-private-preview"></a>Beheren met behulp van Hallo StorSimple Data Manager service UI (afgeschermd voorbeeld)

Dit artikel wordt uitgelegd hoe u Hallo StorSimple Data Manager UI tooperform gegevenstransformatie kunt gebruiken voor gegevens die zich op apparaten Hallo StorSimple 8000-serie. Hallo kunnen getransformeerde gegevens vervolgens worden gebruikt door andere Azure-services zoals Azure Media Services, Azure HDInsight Azure Machine Learning en Azure Search. 


## <a name="use-storsimple-data-transformation"></a>StorSimple gegevenstransformatie gebruiken

Hallo StorSimple Data Manager is Hallo resource waarbinnen gegevenstransformatie kan worden gemaakt. Hallo Data Transformation service kunt u gegevens van uw StorSimple lokale apparaat tooblobs in Azure-opslag verplaatsen. Daarom in de werkstroom moet u toospecify Hallo details over uw StorSimple-apparaat en Hallo gegevens van belang dat u wilt dat toomove toohello storage-account.

### <a name="create-a-storsimple-data-manager-service"></a>Een StorSimple Data Manager-service maken

Hallo te volgen stappen toocreate een StorSimple Data Manager-service uitvoeren.

1. toocreate StorSimple Data Manager-service te gaan[https://aka.ms/HybridDataManager](https://aka.ms/HybridDataManager)

2. Klik op Hallo  **+**  pictogram en de zoekcriteria voor StorSimple Data Manager. Klik op uw StorSimple Data Manager-service en klik vervolgens op **maken**.

3. Als uw abonnement voor het maken van deze service is ingeschakeld, ziet u Hallo blade te volgen.

    ![Maak een resource StorSimple gegevens Managers](./media/storsimple-data-manager-ui/create-new-data-manager-service.png)

4. Voer Hallo invoer en klik op **maken**. Hallo opgegeven locatie moet Hallo een met uw storage-accounts en uw StorSimple Manager-service. Op dit moment worden alleen VS-West en West-Europa regio's ondersteund. Daarom gekoppelde uw StorSimple Manager-service, Data Manager-service en Hallo storage-account moet worden in Hallo voorgaande ondersteunde regio's. Het duurt een minuut toocreate Hallo-service.

### <a name="create-a-data-transformation-job-definition"></a>Een definitie van de transformatie-taak maken

Binnen een StorSimple Data Manager-service moet u toocreate een taakdefinitie voor transformatie van gegevens. De taakdefinitie van een geeft details over Hallo gegevens dat u geïnteresseerd bent in het verplaatsen naar een opslagaccount in systeemeigen Hallo-indeling. 

Hallo na toocreate stappen een nieuwe data transformation taakdefinitie uitvoeren.

1.  Navigeer toohello-service die u hebt gemaakt. Klik op **+ taak definitie**.

    ![Klik op + taakdefinitie](./media/storsimple-data-manager-ui/click-add-job-definition.png)

2. Hallo nieuwe definitie taakblade wordt geopend. Geef een naam op voor de taakdefinitie van de en klik op **bron**. In Hallo **gegevensbron configureren** blade Geef details op Hallo van uw StorSimple-apparaat en Hallo van gegevens van belang.

    ![Taakdefinitie maken](./media/storsimple-data-manager-ui//create-new-job-deifnition.png)

3. Aangezien dit een nieuwe Data Manager-service, worden geen gegevens opslagplaatsen geconfigureerd. Klik op tooadd uw StorSimple Manager als een gegevensopslagplaats **nieuwe toevoegen** in Hallo gegevens opslagplaats vervolgkeuzelijst en klik vervolgens op **gegevensopslagplaats toevoegen**.

4. Kies **StorSimple 8000-serie Manager** als Hallo-opslagplaats te typen eigenschappen van Hallo en uw **StorSimple Manager**. Voor Hallo **Resource-Id** veld, moet u tooenter Hallo nummer voordat Hallo **:** in de registratiesleutel Hallo van uw StorSimple manager.

    ![Gegevensbron maken](./media/storsimple-data-manager-ui/create-new-data-source.png)

5.  Klik op **OK** wanneer u klaar bent. Hiermee slaat u de gegevensopslagplaats van uw en deze StorSimple Manager in andere taakdefinities zonder opnieuw invoeren van deze parameters kunnen worden gebruikt. Het duurt enkele seconden nadat u op **OK** voor Hallo StorSimple Manager tooshow up Hallo vervolgkeuzelijst.

6.  In Hallo **gegevensbron configureren** blade Voer Hallo apparaatnaam en Hallo volumenaam met uw gegevens van belang.

7.  In Hallo **Filter** subsectie, voert u Hallo-hoofdmap waarin de gegevens van belang (dit veld moet beginnen met een `\`). U kunt ook een bestandsfilters hier toevoegen.

8.  Hallo data transformation-service werkt op Hallo-gegevens die wordt doorgeschoven up toohello Azure via momentopnamen. Wanneer deze taak wordt uitgevoerd, kunt u tootake een back-up elke keer dat deze taak wordt uitgevoerd (toowork op de meest recente gegevens) of toouse laatste bestaande back-up in de cloud Hallo Hallo (als u werkt op sommige gearchiveerde gegevens).

    ![Nieuwe details van gegevensbron](./media/storsimple-data-manager-ui/new-data-source-details.png)

9. Vervolgens moeten Hallo-doelinstellingen toobe geconfigureerd. Er zijn 2 soorten ondersteunde doelen – Azure Storage-accounts en Azure Media Services-accounts. Storage-accounts tooput-bestanden in BLOB's in het account kiezen. Media services-account tooput-bestanden in de activa in het account kiezen. Opnieuw, moeten we tooadd een opslagplaats. Selecteer in de vervolgkeuzelijst Hallo **nieuwe toevoegen** en vervolgens **configureren**.

    ![Gegevens sink maken](./media/storsimple-data-manager-ui/create-new-data-sink.png)

10. Hier kunt u Hallo-type van de opslagplaats die u wilt dat tooadd en Hallo andere parameters die zijn gekoppeld aan het Hallo-opslagplaats. In beide gevallen worden de storage-wachtrij wordt gemaakt wanneer Hallo-taak wordt uitgevoerd. Deze wachtrij wordt gevuld met berichten over getransformeerde blobs wanneer deze gereed zijn. Hallo-naam van deze wachtrij is hetzelfde als de naam van de taakdefinitie Hallo HALLO hallo. Als u selecteert **Media Services** als type Hallo-opslagplaats, vervolgens kunt u ook opgeven opslagaccountreferenties waar Hallo wachtrij wordt gemaakt.

    ![Nieuwe gegevens sink-details](./media/storsimple-data-manager-ui/new-data-sink-details.png)

11. Na het toevoegen van Hallo data opslagplaats (die duurt een paar seconden) vindt u Hallo-opslagplaats in de vervolgkeuzelijst Hallo in Hallo **doel-accountnaam**.  Kies Hallo doelmap die u nodig hebt.

12. Klik op **OK** toocreate Hallo taakdefinitie. De taakdefinitie van de is nu ingesteld. U kunt deze taakdefinitie meerdere keren via Hallo gebruikersinterface gebruiken.

    ![Nieuwe taakdefinitie toevoegen](./media/storsimple-data-manager-ui/add-new-job-definition.png)

### <a name="run-hello-job-definition"></a>Hallo taakdefinitie uitvoeren

Als u toomove gegevens van StorSimple toohello storage-account dat u hebt opgegeven in de taakdefinitie hello moet, moet u tooinvoke deze. Er is enige flexibiliteit in Hallo parameters wijzigen telkens wanneer u Hallo taak aanroept. Hallo stappen zijn als volgt:

1. Selecteer uw StorSimple Data Manager-service en ga te**bewaking**. Klik op **nu uitvoeren**.

    ![De definitie van de trigger](./media/storsimple-data-manager-ui/run-now.png)

2. Hallo taakdefinitie kiezen dat u wilt dat toorun. Klik op **instellingen uitvoeren** toomodify alle instellingen die u toochange voor deze taak uitvoeren wilt mogelijk.

    ![Taakinstellingen uitvoeren](./media/storsimple-data-manager-ui/run-settings.png)

3. Klik op **OK** en klik vervolgens op **uitvoeren** toolaunch uw taak. toomonitor deze taak, Ga toohello **taken** pagina in uw StorSimple Data Manager.

    ![Takenlijst met en status](./media/storsimple-data-manager-ui/jobs-list-and-status.png)

4. In aanvulling toomonitoring in Hallo **taken** blade, u kunt ook luisteren op Hallo opslagwachtrij waar een bericht telkens wanneer een bestand wordt verplaatst van StorSimple toohello storage-account is toegevoegd.


## <a name="next-steps"></a>Volgende stappen

[Gebruik de .NET SDK toolaunch StorSimple Data Manager taken](storsimple-data-manager-dotnet-jobs.md).

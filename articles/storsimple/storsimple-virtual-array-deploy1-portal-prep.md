---
title: aaaPortal prep voor virtuele StorSimple-matrix | Microsoft Docs
description: Eerste zelfstudie toodeploy virtuele StorSimple-matrix bestaat uit het voorbereiden van hello Azure-portal
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 68a4cfd3-94c9-46cb-805c-46217290ce02
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 5332b235e7296a9274f2e7dafcdf72f4b9cdadf6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-storsimple-virtual-array---prepare-hello-azure-portal"></a>StorSimple virtuele matrix implementeren: voorbereiden hello Azure-portal

![](./media/storsimple-virtual-array-deploy1-portal-prep/getstarted4.png)
## <a name="overview"></a>Overzicht

Dit is Hallo eerste van het artikel in Hallo reeks zelfstudies voor implementatie vereist toocompletely uw virtuele matrix implementeren als een bestandsserver of een iSCSI-server met behulp van Hallo Resource Manager-model. Dit artikel beschrijft Hallo vereiste voorbereiding toocreate en configureren van uw StorSimple-apparaat Manager service voorafgaande tooprovisioning een virtuele-matrix. In dit artikel bevat ook koppelingen uit tooa configuration checklist- en vereisten voor implementatie.

U moet administrator-bevoegdheden toocomplete Hallo installatie- en configuratieproces. U wordt aangeraden Hallo Configuratiecontrolelijst voor implementatie te controleren voordat u begint. Hallo portal voorbereiding duurt minder dan 10 minuten.

Hallo-informatie in dit artikel wordt gepubliceerd geldt toohello implementatie van het virtuele StorSimple-matrices in hello Azure-portal en Microsoft Azure Government Cloud.

### <a name="get-started"></a>Aan de slag
werkstroom Hallo-implementatie bestaat uit Hallo portal voorbereiden, het inrichten van een virtuele-matrix in uw gevirtualiseerde omgeving en Hallo setup is voltooid. tooget gestart met Hallo virtuele StorSimple-matrix implementatie als een bestandsserver of een iSCSI-server, moet u toorefer toohello gebruikmaking resources te volgen.

#### <a name="deployment-articles"></a>Artikelen over implementatie

toodeploy uw virtuele StorSimple-matrix, Raadpleeg toohello artikelen in de reeks voorgeschreven hello te volgen.

| **#** | **In deze stap** | **U dit wilt doen...** | **En gebruik van deze documenten.** |
| --- | --- | --- | --- |
| 1. |**Hello Azure-portal instellen** |Maak en configureer uw StorSimple-apparaat Manager service voorafgaande tooprovisioning een virtueel StorSimple-matrix. |[Hallo portal voorbereiden](storsimple-virtual-array-deploy1-portal-prep.md) |
| 2. |**Hallo virtuele matrix inrichten** |Voor Hyper-V, inrichten en maak verbinding tooa virtuele StorSimple-matrix op een hostsysteem met Hyper-V op Windows Server 2012 R2, Windows Server 2012 of Windows Server 2008 R2. <br></br> <br></br> Voor VMware, inrichten en verbinding maken met virtuele StorSimple-matrix tooa op een hostsysteem met VMware ESXi 5.5 en hoger.<br></br> |[Inrichten van een virtuele-matrix in Hyper-V](storsimple-virtual-array-deploy2-provision-hyperv.md) <br></br> <br></br> [Een virtuele-matrix in VMware inrichten](storsimple-virtual-array-deploy2-provision-vmware.md) |
| 3. |**Hallo virtuele matrix instellen** |Voor uw bestandsserver uitvoeren van de eerste installatie Apparaatinstelling Hallo en registreren van uw StorSimple-bestandsserver. Vervolgens kunt u SMB-shares inrichten. <br></br> <br></br> Eerste installatie uitvoeren voor uw server met iSCSI-, uw StorSimple iSCSI-server registreren en Apparaatinstelling Hallo. Vervolgens kunt u iSCSI-volumes inrichten. |[Virtuele matrix instellen als bestandsserver](storsimple-virtual-array-deploy3-fs-setup.md)<br></br> <br></br>[Virtuele matrix ingesteld als iSCSI-server](storsimple-virtual-array-deploy3-iscsi-setup.md) |

U kunt nu beginnen met tooset up hello Azure-portal.

## <a name="configuration-checklist"></a>Configuratiecontrolelijst

Hallo Configuratiecontrolelijst beschrijft Hallo-gegevens die u toocollect nodig voordat u software Hallo op uw virtuele StorSimple-matrix configureren. Deze informatie tevoren tijd helpt voorbereiden stroomlijnen Hallo proces voor het implementeren van Hallo StorSimple-apparaat in uw omgeving. Afhankelijk van het feit of uw virtuele StorSimple-matrix is geïmplementeerd als een bestandsserver of een iSCSI-server, moet u een van de volgende controlelijsten Hallo.

* Hallo downloaden [StorSimple virtuele matrix bestand Server Configuratiecontrolelijst](http://download.microsoft.com/download/E/E/6/EE690BB0-B442-4B84-8165-4731EE727ACF/MicrosoftAzureStorSimpleVirtualArrayFileServerConfigurationChecklist.pdf).
* Hallo downloaden [virtuele StorSimple-matrix iSCSI Server Configuratiecontrolelijst](http://download.microsoft.com/download/E/E/6/EE690BB0-B442-4B84-8165-4731EE727ACF/MicrosoftAzureStorSimpleVirtualArrayiSCSIServerConfigurationChecklist.pdf).

## <a name="prerequisites"></a>Vereisten

U vindt hier Hallo configuratievereisten voor uw StorSimple-apparaat Manager-service, uw virtuele StorSimple-matrix en Hallo datacenternetwerk.

### <a name="for-hello-storsimple-device-manager-service"></a>Voor Hallo StorSimple-apparaat Manager-service

Zorg voordat u begint voor het volgende:

* U hebt een Microsoft-account met toegangsreferenties.
* U hebt een Microsoft Azure Storage-account met toegangsreferenties.
* Uw Microsoft Azure-abonnement moet worden ingeschakeld voor Apparaatbeheer van StorSimple-service.

### <a name="for-hello-storsimple-virtual-array"></a>Hallo voor virtuele StorSimple-matrix

Voordat u een virtuele-matrix implementeert, zorg ervoor dat:

* U hebt toegang tot tooa-hostsysteem met Hyper-V in Windows Server 2008 R2 of later of VMware (ESXi 5.5 of hoger) die kan worden gebruikt tooa inrichten van een apparaat.
* Hallo-hostsysteem is kunnen toodedicate Hallo na tooprovision resources van uw virtuele matrix:
  
  * Een minimum van 4 kernen.
  * Ten minste 8 GB aan RAM-geheugen. Als u van plan tooconfigure Hallo virtuele matrix als bestandsserver bent, ondersteunt 8 GB 2 miljoen bestanden. U moet 16 GB RAM-geheugen toosupport 2-4 miljoen bestanden.
  * Één netwerkinterface.
  * 500 GB virtuele schijf voor systeemgegevens.

### <a name="for-hello-datacenter-network"></a>Voor het datacenternetwerk Hallo

Zorg voordat u begint voor het volgende:

* Hallo-netwerk in uw datacenter is geconfigureerd volgens Hallo netwerkvereisten voor uw StorSimple-apparaat. Zie voor meer informatie, Hallo [StorSimple virtuele matrix systeemvereisten](storsimple-ova-system-requirements.md).
* Uw virtuele StorSimple-matrix heeft een speciale 5 Mbps internetbandbreedte (of meer) beschikbaar te allen tijde. Deze bandbreedte mag niet worden gedeeld met andere toepassingen.

## <a name="step-by-step-preparation"></a>Stapsgewijze voorbereiding

Hallo volgen Stapsgewijze instructies tooprepare uw portal voor Hallo StorSimple-apparaat Manager-service gebruiken.

## <a name="step-1-create-a-new-service"></a>Stap 1: een nieuwe service maken

Slechts één exemplaar van Hallo Apparaatbeheer StorSimple-service kan meerdere virtuele StorSimple-matrices beheren. Hallo te volgen stappen toocreate een exemplaar van Hallo Apparaatbeheer StorSimple-service uitvoeren. Als u een bestaande toomanage voor Apparaatbeheer van StorSimple-service op uw virtuele matrices hebt, deze stap overslaan en ga te[stap 2: Get Hallo serviceregistratiesleutel](#step-2-get-the-service-registration-key).

[!INCLUDE [storsimple-virtual-array-create-new-service](../../includes/storsimple-virtual-array-create-new-service.md)]

> [!IMPORTANT]
> Als u met uw service niet Hallo automatisch maken van een opslagaccount hebt ingeschakeld, moet u toocreate ten minste één opslagaccount nadat u een service hebt gemaakt.
> 
> * Als u een opslagaccount niet automatisch gemaakt, gaat u verder te[configureren van een nieuw opslagaccount voor Hallo service](#optional-step-configure-a-new-storage-account-for-the-service) voor gedetailleerde instructies.
> * Als u Hallo automatisch maken van een opslagaccount hebt ingeschakeld, gaat u verder te[stap 2: Get Hallo serviceregistratiesleutel](#step-2-get-the-service-registration-key).
> 
> 

## <a name="step-2-get-hello-service-registration-key"></a>Stap 2: Hallo serviceregistratiesleutel ophalen

Nadat de Hallo StorSimple-apparaat Manager-service actief is, moet u tooget hello serviceregistratiesleutel. Deze sleutel is gebruikte tooregister en verbinding maken met uw StorSimple-apparaat met Hallo-service.

Uitvoeren van de stappen te volgen in Hallo Hallo [Azure-portal](https://portal.azure.com/).

[!INCLUDE [storsimple-virtual-array-get-service-registration-key](../../includes/storsimple-virtual-array-get-service-registration-key.md)]

> [!NOTE]
> Hallo serviceregistratiesleutel is gebruikte tooregister alle Hallo Apparaatbeheer StorSimple-apparaten die tooregister met uw StorSimple-apparaat Manager-service moeten.
> 
> 

## <a name="step-3-download-hello-virtual-array-image"></a>Stap 3: Hallo virtuele matrix installatiekopie downloaden

Nadat u de serviceregistratiesleutel Hallo hebt, moet u op uw hostsysteem toodownload Hallo juiste virtuele matrix installatiekopie tooprovision een virtuele-matrix. Hallo virtuele matrix afbeeldingen zijn specifiek besturingssysteem en kunnen worden gedownload vanaf Hallo pagina snel starten in hello Azure-portal.

> [!IMPORTANT]
> Hallo software die wordt uitgevoerd op Hallo virtuele StorSimple-matrix kan alleen worden gebruikt met Hallo StorSimple-apparaat Manager-service.
> 
> 

Uitvoeren van de stappen te volgen in Hallo Hallo [Azure-portal](https://portal.azure.com/).

#### <a name="tooget-hello-virtual-array-image"></a>tooget hello virtuele matrix installatiekopie

1. Meld u aan bij Hallo [Azure-portal](https://portal.azure.com/). 
2. Klik in hello Azure-portal, op **Bladeren > Managers voor apparaatregistratie StorSimple**.
3. Selecteer een bestaande Apparaatbeheer StorSimple-service. In Hallo **StorSimple Apparaatbeheer** blade, klikt u op **Quick Start**. 
4. Klik op Hallo koppeling bijbehorende toohello afbeelding die u wilt dat toodownload van Hallo Microsoft Download Center. Hallo-installatiekopiebestanden zijn ongeveer 4,8 GB.
   
   * VHDX voor Hyper-V op Windows Server 2012 en hoger
   * VHD voor Hyper-V in Windows Server 2008 R2 en hoger
   * VMDK voor VMWare ESXi 5.5 en hoger
5. Download en pak Hallo bestand tooa lokale schijf, waardoor een notitie van waarin de uitgepakte bestand Hallo zich bevindt.

## <a name="optional-step-configure-a-new-storage-account-for-hello-service"></a>Optionele stap: een nieuw opslagaccount voor Hallo service configureren

Deze stap is optioneel en moet worden uitgevoerd alleen als u niet Hallo automatisch maken van een opslagaccount met uw service hebt ingeschakeld.

Als u een Azure storage-account in een andere regio toocreate nodig hebt, raadpleegt u [hoe toocreate een opslagaccount](../storage/common/storage-create-storage-account.md#create-a-storage-account) voor stapsgewijze instructies.

Uitvoeren van de stappen te volgen in Hallo Hallo [Azure-portal](https://ms.portal.azure.com/) op Hallo StorSimple Apparaatbeheer service pagina tooadd een bestaand Microsoft Azure-opslagaccount.

#### <a name="tooadd-a-storage-account-credential-that-has-hello-same-azure-subscription-as-hello-device-manager-service"></a>een storage account referentie tooadd Hallo hetzelfde Azure-abonnement als Hallo Apparaatbeheer service

1. Ga tooyour Apparaatbeheer, selecteer service en dubbelklik erop. Hiermee opent u Hallo **overzicht** blade.
2. Selecteer **opslagaccountreferenties** binnen Hallo **configuratie** sectie.
3. Klik op **Add**.
4. In Hallo **een opslagaccount toevoegen** blade Hallo te volgen:
   
    1. Voor **abonnement**, selecteer **huidige**.
   
    2. Hallo-naam van uw Azure storage-account opgeven.
   
    3. Selecteer **inschakelen** toocreate een beveiligd kanaal voor netwerkcommunicatie tussen uw StorSimple-apparaat en het Hallo-cloud. Selecteer **uitschakelen** alleen als u in een privécloud werkt.
   
    4. Klik op **Add**. U wordt gewaarschuwd nadat Hallo storage-account is gemaakt.<br></br>
   
     ![Een bestaande referentie voor de storage-account toevoegen](./media/storsimple-virtual-array-manage-storage-accounts/ova-add-storageacct.png)

## <a name="next-step"></a>Volgende stap

de volgende stap Hallo is tooprovision een virtuele machine voor uw virtuele StorSimple-matrix. Zie het volgende, afhankelijk van uw hostbesturingssysteem Hallo gedetailleerde instructies in:

* [Inrichten van een virtueel StorSimple-matrix in Hyper-V](storsimple-virtual-array-deploy2-provision-hyperv.md)
* [Een virtueel StorSimple-matrix in VMware inrichten](storsimple-virtual-array-deploy2-provision-vmware.md)


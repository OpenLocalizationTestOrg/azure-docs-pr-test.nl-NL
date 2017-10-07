---
title: aaaSet up Hallo bron en doel voor Hyper-V-replicatie tooa secundaire site met Azure Site Recovery | Microsoft Docs
description: Beschrijft hoe tooset omhoog Hallo bron en doel wanneer toosecondary VMM site Hyper-V-machines repliceren met Azure Site Recovery.
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: fa7809f1-7633-425f-b25d-d10d004e8d0b
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/30/2017
ms.author: raynew
ms.openlocfilehash: 451cb4413ca5c09777a7faf512b1c8ea43e695f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="step-6-set-up-hello-replication-source-and-target"></a>Stap 6: Instellen Hallo replicatiebron en doel


Na het maken van een Recovery Services-kluis voor Hyper-V-replicatie tooa secundaire VMM-site met [Azure Site Recovery](site-recovery-overview.md), gebruikt u dit artikel tooset up Hallo bron en doel van de locaties van de replicatie. 

Lees dit artikel en eventuele opmerkingen posten Hallo onderin of op Hallo [Azure Recovery Services-Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).




## <a name="set-up-hello-source-environment"></a>Hallo bronomgeving instellen

Hello Azure Site Recovery Provider installeren op VMM-servers en detecteren en beheerservers in Hallo kluis registreren.

1. Klik op **stap 1: infrastructuur voorbereiden** > **bron**.

    ![Bron instellen](./media/vmm-to-vmm-walkthrough-source-target/goals-source.png)
2. In **bron voorbereiden**, klikt u op **+ VMM** tooadd een VMM-server.

    ![Bron instellen](./media/vmm-to-vmm-walkthrough-source-target/set-source1.png)
3. In **Server toevoegen**, controleert u of **System Center VMM-server** wordt weergegeven in **servertype** en die Hallo VMM-server voldoet aan Hallo [vereisten](#prerequisites).
4. Download hello Azure Site Recovery Provider-installatiebestand.
5. Download de registratiesleutel Hallo. U hebt deze nodig wanneer u de installatie uitvoert. Hallo-sleutel is vijf dagen na het genereren ervan geldig.

    ![Bron instellen](./media/vmm-to-vmm-walkthrough-source-target/set-source3.png)
6. Hello Azure Site Recovery Provider installeren op Hallo VMM-server. U hoeft niet tooexplicitly niets mee geïnstalleerd op Hyper-V-hostservers.


## <a name="install-hello-azure-site-recovery-provider"></a>Hello Azure Site Recovery Provider installeren

1. Hallo Provider setup-bestand op elke VMM-server wordt uitgevoerd. Als VMM is geïmplementeerd in een cluster, voert u Hallo Hallo na eerste keer dat u installeert:
    -  Hallo-provider installeren op een actief knooppunt en Hallo installatie tooregister Hallo VMM-server in de kluis Hallo voltooien.
    - Vervolgens installeert u Hallo Provider op Hallo andere knooppunten. Clusterknooppunten moeten alle Hallo uitgevoerd dezelfde versie van Provider Hallo.
2. Setup enkele vereiste controles uitgevoerd en vraagt toestemming toostop Hallo VMM-service. Hallo VMM-service wordt opnieuw opgestart nadat setup is voltooid. Als u op een VMM-cluster installeert, bent u na vragen aan gebruiker toostop Hallo Cluster-rol.
3. In **Microsoft Update**, kunt u ervoor kiezen in toospecify dat de provider-updates zijn geïnstalleerd in overeenstemming met uw Microsoft Update-beleid.
4. In **installatie**, accepteer of wijzig Hallo standaardlocatie voor installatie, en klikt u op **installeren**.

    ![Installatielocatie](./media/vmm-to-vmm-walkthrough-source-target/provider-location.png)
5. Nadat de installatie is voltooid, klikt u op **registreren** tooregister Hallo-server in Hallo kluis.

    ![Installatielocatie](./media/vmm-to-vmm-walkthrough-source-target/provider-register.png)
6. In **kluisnaam**, Controleer de naam van de Hallo van Hallo kluis in welke Hallo server wordt geregistreerd. Klik op *Volgende*.

    ![Serverregistratie](./media/vmm-to-vmm-walkthrough-source-target/vaultcred.png)
7. In **internetverbinding**, opgeven hoe Hallo-provider die wordt uitgevoerd op de VMM-server Hallo tooAzure verbindt.

    ![Instellingen voor internet](./media/vmm-to-vmm-walkthrough-source-target/proxydetails.png)

   - U kunt opgeven die Hallo-provider moet rechtstreeks verbinding gemaakt toohello internet, of via een proxyserver.
   - Proxy-instellingen opgeven, indien nodig.
   - Als u een proxy gebruikt, een VMM RunAs-account (DRAProxyAccount) wordt automatisch gemaakt met Hallo opgegeven proxyreferenties. Hallo-proxyserver zodanig configureren dat dit account kan worden geverifieerd. Hallo RunAs-Accountinstellingen kunnen worden gewijzigd in de VMM-console Hallo > **instellingen** > **beveiliging** > **Run As-Accounts**. Hallo VMM servicewijzigingen tooupdate opnieuw opstarten
8. In **registratiesleutel**, selecteer Hallo sleutel gedownload uit Azure Site Recovery uit te voeren en toohello VMM-server gekopieerd.
9. Hallo-instelling voor wachtwoordversleuteling wordt alleen gebruikt wanneer u Hyper-V-machines in VMM-clouds tooAzure repliceert. Als u tooa secundaire site repliceert wordt het niet gebruikt.
10. In **servernaam**, Geef een beschrijvende naam tooidentify Hallo VMM-server in Hallo kluis. Geef in een clusterconfiguratie Hallo VMM-clusterrolnaam op.
11. In **cloudmetagegevens synchroniseren**Selecteer of u voor alle clouds op de VMM-server met de kluis Hallo Hallo toosynchronize metagegevens wilt instellen. Deze actie hoeft alleen toohappen eenmaal op elke server. Als u niet toosynchronize alle clouds wilt, kunt u laat u deze instelling uitgeschakeld en synchroniseert u elke cloud afzonderlijk in de eigenschappen van de cloud Hallo in Hallo VMM-console.
12. Klik op **volgende** toocomplete Hallo proces. Na registratie worden metagegevens van Hallo VMM-server opgehaald door Azure Site Recovery. Hallo-server wordt weergegeven op Hallo **VMM-Servers** tabblad op Hallo **Servers** pagina in Hallo kluis.

    ![Server](./media/vmm-to-vmm-walkthrough-source-target/provider13.png)
13. Nadat het Hallo-server is beschikbaar in Hallo Site Recovery-console, in **bron** > **bron voorbereiden** Selecteer Hallo VMM-server en selecteer Hallo cloud welke Hallo Hyper-V host bevindt. Klik vervolgens op **OK**.

U kunt ook Hallo-provider installeren vanaf de opdrachtregel Hallo:

[!INCLUDE [site-recovery-rw-provider-command-line](../../includes/site-recovery-rw-provider-command-line.md)]


## <a name="set-up-hello-target-environment"></a>Hallo doelomgeving instellen

Hallo doel-VMM-server en cloud selecteren:

1. Klik op **infrastructuur voorbereiden** > **doel**, en selecteer Hallo doel VMM-server die u wilt dat toouse.
2. Clouds op Hallo-server die zijn gesynchroniseerd met Site Recovery wordt weergegeven. Selecteer de doelcloud Hallo.

   ![doel](./media/vmm-to-vmm-walkthrough-source-target/target-vmm.png)



## <a name="next-steps"></a>Volgende stappen

Ga te[stap 7: netwerktoewijzing configureren](vmm-to-vmm-walkthrough-network-mapping.md).

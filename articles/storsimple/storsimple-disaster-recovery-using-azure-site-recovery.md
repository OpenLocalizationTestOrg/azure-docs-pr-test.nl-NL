---
title: aaaAutomate StorSimple fileshare DR met Azure Site Recovery | Microsoft Docs
description: Hierin wordt beschreven Hallo stappen en best practices voor het maken van een noodherstel voor bestandsshares die worden gehost op Microsoft Azure StorSimple-opslag.
services: storsimple
documentationcenter: NA
author: vidarmsft
manager: syadav
editor: 
ms.assetid: 23049a2c-055e-4d0e-b8f5-af2a87ecf53f
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/09/2017
ms.author: vidarmsft
ms.openlocfilehash: fa3e8d4e77ca0f6a7b5f9bbb956a4de12547642e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="automated-disaster-recovery-solution-using-azure-site-recovery-for-file-shares-hosted-on-storsimple"></a>Automatisch herstel na noodgevallen oplossing met Azure Site Recovery voor bestandsshares die worden gehost op StorSimple
## <a name="overview"></a>Overzicht
Microsoft Azure StorSimple is een hybride cloud-opslagoplossing die adressen Hallo complexiteit van niet-gestructureerde gegevens die betrekking hebben op bestandsshares. StorSimple maakt gebruik van cloud-opslag als een uitbreiding van Hallo on-premises-oplossing en automatisch gegevens over opslag voor lokale en cloud-opslag lagen. Gegevensbescherming, geïntegreerd met lokale en cloud worden opgeslagen, niet meer nodig voor een weids opslaginfrastructuur Hallo.

[Azure Site Recovery](../site-recovery/site-recovery-overview.md) is een Azure-service disaster recovery (DR biedt) door te organiseren replicatie, failovers en herstel van virtuele machines. Azure Site Recovery ondersteunt een aantal replicatie technologieën tooconsistently repliceren, beveiligen en naadloos failover van virtuele machines en toepassingen tooprivate/public of gehoste clouds.

Met Azure Site Recovery, replicatie voor virtuele machines en StorSimple snapshot cloudfuncties, kunt u Hallo volledig bestand serveromgeving beveiligen. In geval van een onderbreking van de Hallo kunt u een enkele klik toobring uw bestandsshares online in Azure in een paar minuten.

Dit document wordt gedetailleerd uitgelegd hoe u kunt een noodherstel voor uw bestandsshares die worden gehost op een StorSimple-opslag maken en uitvoeren van geplande, niet-geplande en testfailovers met behulp van een herstelplan met één klik. In wezen zien hoe u Hallo herstelplan kunt wijzigen in uw Azure Site Recovery-kluis tooenable StorSimple failovers tijdens na noodgevallen scenario's. Bovendien beschrijft ondersteunde configuraties en vereisten. Dit document wordt ervan uitgegaan dat u bekend met Hallo basisbeginselen van Azure Site Recovery en StorSimple-architecturen bent.

## <a name="supported-azure-site-recovery-deployment-options"></a>Ondersteunde opties voor Azure Site Recovery-implementatie
Klanten kunnen bestandsservers implementeren als fysieke servers of virtuele machines (VM's) op de Hyper-V- of VMware en vervolgens bestandsshares te maken van volumes oppervlaktevariaties buiten het StorSimple-opslag. Azure Site Recovery kunt beide implementaties van fysieke en virtuele tooeither beveiligen een secundaire site of tooAzure. Dit document bevat informatie over de details van een oplossing voor DR met Azure als Hallo herstelsite voor een virtuele machine wordt gehost op Hyper-V server en bestandsshares op het StorSimple-opslag. Andere scenario's in welke bestandsserver Hallo VM bevindt zich op een VMware-VM of een fysieke computer kunnen op dezelfde manier worden geïmplementeerd.

## <a name="prerequisites"></a>Vereisten
Implementatie van een éénkliks-noodherstel die gebruikmaakt van Azure Site Recovery voor bestandsshares die worden gehost op een StorSimple-opslag heeft Hallo volgende vereisten:

* De lokale virtuele machine wordt gehost op Hyper-V- of VMware- of een fysieke computer bestand van Windows Server 2012 R2-server
* StorSimple opslag on-premises apparaten die zijn geregistreerd bij Azure StorSimple manager
* StorSimple Cloud toestel gemaakt in hello Azure StorSimple manager (dit kan worden bewaard in staat afsluiten)
* Bestandsshares die worden gehost op Hallo volumes die zijn geconfigureerd op Hallo StorSimple-opslagapparaat
* [Azure Site Recovery services-kluis](../site-recovery/site-recovery-vmm-to-vmm.md) gemaakt in een Microsoft Azure-abonnement

Daarnaast uitgevoerd als Azure uw site recovery, Hallo [Azure virtuele Machine Readiness Assessment tool](http://azure.microsoft.com/downloads/vm-readiness-assessment/) services op virtuele machines tooensure dat ze compatibel met Azure VM's en Azure Site Recovery zijn.

problemen tooavoid latentie (dit kunnen leiden tot hogere kosten), zorg ervoor dat u het apparaat in uw StorSimple-Cloud, automation-account maakt en opslagaccounts in dezelfde regio Hallo.

## <a name="enable-dr-for-storsimple-file-shares"></a>DR inschakelen voor StorSimple-bestandsshares
Elk onderdeel van Hallo lokale omgeving moet toobe beveiligd tooenable replicatie is voltooid en herstel. Deze sectie wordt beschreven hoe:

* Instellen van de Active Directory en DNS-replicatie (optioneel)
* Azure Site Recovery tooenable bescherming van bestandsserver Hallo VM gebruiken
* Schakel de beveiliging van StorSimple-volumes
* Hallo netwerk configureren

### <a name="set-up-active-directory-and-dns-replication-optional"></a>Instellen van de Active Directory en DNS-replicatie (optioneel)
Als u wilt beveiligen tooprotect Hallo machines met Active Directory en DNS zodat ze beschikbaar op Hallo DR-site zijn, moet u tooexplicitly ze (zodat bestandsservers Hallo na een failover uitvoeren met verificatie toegankelijk zijn). Er zijn twee aanbevolen opties op basis van de complexiteit Hallo van van de klant Hallo on-premises omgeving.

#### <a name="option-1"></a>Optie 1
Als klant Hallo een klein aantal toepassingen heeft, één domeincontroller voor Hallo volledige on-premises site, en zal worden failover Hallo hele site, wordt aangeraden Azure Site Recovery replicatie tooreplicate Hallo domain controller machine de secundaire site tooa (dit is van toepassing voor zowel de site-naar-site en de site naar Azure).

#### <a name="option-2"></a>Optie 2
Als klant Hallo heeft een groot aantal toepassingen, een Active Directory-forest wordt uitgevoerd en failover wordt uitgevoerd een paar toepassingen op een tijdstip, wordt aangeraden een extra domeincontroller op Hallo DR-site instellen (een secundaire site of in Azure).

Raadpleeg het te[automatisch DR-oplossing voor Active Directory en DNS met Azure Site Recovery](../site-recovery/site-recovery-active-directory.md) voor instructies wanneer het beschikbaar maken van een domeincontroller op Hallo DR-site. Hallo rest van dit document, wordt er uitgegaan dat een domeincontroller beschikbaar is op Hallo DR-site.

### <a name="use-azure-site-recovery-tooenable-protection-of-hello-file-server-vm"></a>Azure Site Recovery tooenable bescherming van bestandsserver Hallo VM gebruiken
Deze stap is vereist dat u Hallo on-premises bestand serveromgeving voorbereiden, maken en voorbereiden van een Azure Site Recovery-kluis en bestandsbeveiliging Hallo VM inschakelen.

#### <a name="tooprepare-hello-on-premises-file-server-environment"></a>tooprepare hello on-premises bestand serveromgeving
1. Set Hallo **User Account Control** te**nooit waarschuwen**. Dit is vereist zodat u Azure automation-scripts tooconnect Hallo iSCSI-doelen na het mislukken door Azure Site Recovery kunt.

   1. Druk op Hallo Windows-toets + Q en zoek naar **UAC**.
   2. Selecteer **instellingen voor Gebruikersaccountbeheer wijzigen**.
   3. Sleep Hallo balk toohello onder naar **nooit waarschuwen**.
   4. Klik op **OK** en selecteer vervolgens **Ja** wanneer u wordt gevraagd.

      ![](./media/storsimple-disaster-recovery-using-azure-site-recovery/image1.png)
2. Hallo VM-Agent installeren op elke bestandsserver Hallo virtuele machines. Dit is vereist zodat u Azure automatiseringsscripts op Hallo failover van virtuele machines uitvoeren kunt.

   1. [Hallo-agent downloaden](http://aka.ms/vmagentwin) te`C:\\Users\\<username>\\Downloads`.
   2. Open Windows PowerShell in de beheerdersmodus (als Administrator uitvoeren) en voer vervolgens de volgende opdracht toonavigate toohello downloadlocatie Hallo:

      `cd C:\\Users\\<username>\\Downloads\\WindowsAzureVmAgent.2.6.1198.718.rd\_art\_stable.150415-1739.fre.msi`

      > [!NOTE]
      > Hallo-bestandsnaam kan worden gewijzigd, afhankelijk van Hallo-versie.
      >
      >
3. Klik op **Volgende**.
4. Hallo accepteren **voorwaarden van de overeenkomst** en klik vervolgens op **volgende**.
5. Klik op **Voltooien**.
6. Bestandsshares maken met volumes oppervlaktevariaties buiten het StorSimple-opslag. Zie voor meer informatie [hello StorSimple Manager-service toomanage volumes gebruiken](storsimple-manage-volumes.md).

   1. Op uw lokale virtuele machines, drukt u op Hallo Windows-toets + Q en zoek naar **iSCSI**.
   2. Selecteer **iSCSI-initiator**.
   3. Selecteer Hallo **configuratie** Hallo-initiatornaam tabblad en kopiëren.
   4. Meld u bij toohello [Azure-portal](https://portal.azure.com/).
   5. Selecteer Hallo **StorSimple** tabblad en vervolgens selecteert Hallo StorSimple Manager-Service die het fysieke apparaat Hallo bevat.
   6. Maken van volume container (s) en maak vervolgens een of meer volumes. (Deze volumes zijn voor Hallo file share (s) op de bestandsserver Hallo VM's). Naam van de initiator Hallo kopiëren en geef een passende naam voor Hallo Access Control Records wanneer u Hallo volumes maken.
   7. Selecteer Hallo **configureren** tabblad en noteer Hallo IP-adres van het Hallo-apparaat.
   8. Ga op uw lokale virtuele machines, toohello **iSCSI-initiator** opnieuw en Voer Hallo IP in Hallo sectie snel verbinding maken. Klik op **snelle verbinding** (Hallo apparaat moet nu worden verbonden).
   9. Open hello Azure-portal en selecteer Hallo **Volumes en apparaten** tabblad. Klik op **automatisch configureren**. Hallo-volume dat u zojuist hebt gemaakt, worden weergegeven.
   10. Selecteer in de portal Hallo Hallo **apparaten** tabblad en selecteer vervolgens **een nieuw virtueelapparaat maken.** (Dit virtuele apparaat wordt gebruikt als er een failover optreedt). Deze nieuwe virtuele apparaat kan worden bewaard in een status offline heeft tooavoid extra kosten. tootake Hallo virtueel apparaat offline, gaat u toohello **virtuele Machines** sectie op Hallo Portal en sluit deze af.
   11. Ga terug toohello lokale VM's en open Schijfbeheer (druk op Hallo Windows-toets + X en selecteer **Schijfbeheer**).
   12. Hier ziet u een aantal extra schijven (afhankelijk van de Hallo aantal volumes die u hebt gemaakt). Klik met de rechtermuisknop Hallo eerste, selecteer **schijf initialiseren**, en selecteer **OK**. Klik met de rechtermuisknop Hallo **Unallocated** sectie **Nieuw eenvoudig Volume**, een stationsletter toewijzen en voltooi de wizard Hallo.
   13. Herhaal stap l voor alle Hallo-schijven. Nu ziet u alle Hallo schijven op **deze PC** in Hallo Windows Verkenner.
   14. Hallo File and Storage Services rol toocreate-bestandsshares gebruiken op deze volumes.

#### <a name="toocreate-and-prepare-an-azure-site-recovery-vault"></a>toocreate en voorbereiden van een Azure Site Recovery-kluis
Raadpleeg toohello [documentatie van Azure Site Recovery](../site-recovery/site-recovery-hyper-v-site-to-azure.md) tooget starten met Azure Site Recovery voordat het Hallo-bestandsserver VM beveiligt.

#### <a name="tooenable-protection"></a>tooenable beveiliging
1. Hallo iSCSI verbreken doel(en) van Hallo lokale virtuele machines die u wilt dat tooprotect via Azure Site Recovery:

   1. Druk op Windows-toets + Q en zoek naar **iSCSI**.
   2. Selecteer **instellen van iSCSI-initiator**.
   3. Verbinding verbreken Hallo StorSimple-apparaat die u eerder hebt gekoppeld. U kunt ook de bestandsserver Hallo uitschakelen voor een paar minuten bij het inschakelen van beveiliging.

   > [!NOTE]
   > Hierdoor wordt Hallo bestandsshares toobe tijdelijk niet beschikbaar.
   >
   >
2. [Schakel de beveiliging van de virtuele machine](../site-recovery/site-recovery-hyper-v-site-to-azure.md) van Hallo bestandsserver VM van hello Azure Site Recovery-portal.
3. Wanneer de initiële synchronisatie Hallo begint, kunt u Hallo doel opnieuw. Ga toohello iSCSI-initiator, Hallo StorSimple-apparaat te selecteren en op **Connect**.
4. Wanneer Hallo synchronisatie is voltooid en Hallo status Hallo VM **beveiligde**, selecteert u Hallo VM, selecteer Hallo **configureren** tabblad en dienovereenkomstig Hallo netwerk Hallo VM bijwerken (dit is Hallo netwerk die Hallo VM('s) failover wordt een deel uitmaken van). Als het Hallo-netwerk niet wordt weergegeven, betekent dit Hallo sync er nog steeds op.

### <a name="enable-protection-of-storsimple-volumes"></a>Schakel de beveiliging van StorSimple-volumes
Als u hebt geen Hallo geselecteerd **een standaardback-up voor dit volume inschakelen** optie voor Hallo StorSimple-volumes, gaat u te**back-upbeleid** Hallo StorSimple Manager-service en een geschikte back-up maken beleid voor alle Hallo volumes. Het is raadzaam dat u Hallo frequentie van back-ups toohello beoogd herstelpunt (RPO) dat u toosee voor de toepassing hello wilt ingesteld.

### <a name="configure-hello-network"></a>Hallo netwerk configureren
Voor de bestandsserver VM hello, netwerkinstellingen configureren in Azure Site Recovery zodat Hallo VM-netwerken aangesloten toohello juiste DR netwerk na een failover zijn.

U kunt Hallo VM selecteren in Hallo **gerepliceerde items** tabblad tooconfigure Hallo netwerkinstellingen, zoals wordt weergegeven in de volgende illustratie Hallo.

![](./media/storsimple-disaster-recovery-using-azure-site-recovery/image2.png)

## <a name="create-a-recovery-plan"></a>Een herstelplan maken
U kunt een herstelplan maken in ASR tooautomate Hallo failoverproces van het Hallo-bestandsshares. Als er een onderbreking van de optreedt, kunt u dan Hallo-bestandsshares over een paar minuten met één klik. tooenable deze automatisering, moet u een Azure automation-account.

#### <a name="toocreate-an-automation-account"></a>toocreate een Automation-account
1. Ga toohello Azure-portal &gt; **Automation** sectie.
2. Klik op **+ toevoegen** knop klikt, wordt hieronder blade geopend.

   ![](./media/storsimple-disaster-recovery-using-azure-site-recovery/image11.png)

   * Geef een naam - Voer een nieuw automatiseringsaccount
   * Abonnement - abonnement kiezen
   * Resource group - nieuwe/Kies bestaande resourcegroep maken
   * Locatie - locatie kiezen, houd Hallo hetzelfde geo of dezelfde regio in welke Hallo StorSimple Cloud toestel en Storage-Accounts zijn gemaakt.
   * Maken van Azure uitvoeren als-account - selecteer **Ja** optie.

3. Ga toohello Automation-account, klikt u op **Runbooks** &gt; **bladeren galerie** tooimport alle Hallo runbooks in Hallo automation-account vereist.
4. Hallo runbooks te volgen door te zoeken toevoegen **herstel na noodgevallen** -tag in Hallo Galerij:

   * Opruimen van de StorSimple-volumes na Test Failover (TFO)
   * Failover StorSimple volumecontainers
   * Koppelen van volumes op de StorSimple-apparaat na een failover
   * Verwijderen van extensie voor aangepaste scripts in Azure VM
   * Virtueel StorSimple-apparaat starten

     ![](./media/storsimple-disaster-recovery-using-azure-site-recovery/image3.png)

5. Publicatie van alle Hallo scripts Hallo runbook door in te schakelen Hallo automation-account en klik op **bewerken** &gt; **publiceren** en vervolgens **Ja** toohello verificatie Bericht. Na deze stap Hallo **Runbooks** tabblad wordt als volgt uitzien:

    ![](./media/storsimple-disaster-recovery-using-azure-site-recovery/image4.png)

6. Selecteer Hallo in Hallo automation-account, **activa** tabblad &gt; klikt u op **variabelen** &gt; **toevoegen van een variabele** en Hallo na variabelen toe te voegen. U kunt deze activa tooencrypt. Deze variabelen zijn recovery plan-specifieke. Als uw herstelplan (die u maakt in de volgende stap Hallo) is de naam van TestPlan, wordt de variabelen moet TestPlan StorSimRegKey, TestPlan AzureSubscriptionName, enzovoort.

   * *RecoveryPlanName***- StorSimRegKey**: Hallo registratiecode voor Hallo StorSimple Manager-service.
   * *RecoveryPlanName***- AzureSubscriptionName**: Hallo-naam van hello Azure-abonnement.
   * *RecoveryPlanName***- ResourceName**: naam Hallo Hallo StorSimple-resource met Hallo StorSimple-apparaat.
   * *RecoveryPlanName***- DeviceName**: Hallo apparaat toobe failover heeft.
   * *RecoveryPlanName***- VolumeContainers**: een door komma's gescheiden reeks volumecontainers aanwezig is op Hallo-apparaat die toobe kan niet meer dan; bijvoorbeeld: moeten volcon1, volcon2, volcon3.
   * *RecoveryPlanName***- TargetDeviceName**: Hallo StorSimple Cloud toestel op welke Hallo containers toobe zijn failover.
   * *RecoveryPlanName***- TargetDeviceDnsName**: Hallo servicenaam van het doelapparaat hello (dit vindt u in Hallo **virtuele Machine** sectie: Hallo servicenaam is dezelfde als Hallo Hallo DNS-naam).
   * *RecoveryPlanName***- StorageAccountName**: Hallo opslagaccountnaam in welke Hallo-script (die toorun op Hallo failover VM) wordt opgeslagen. Dit is opslagaccount met sommige ruimte toostore Hallo script tijdelijk.
   * *RecoveryPlanName***- StorageAccountKey**: Hallo-toegangssleutel voor Hallo hierboven storage-account.
   * *RecoveryPlanName***- ScriptContainer**: Hallo-naam van Hallo-container op welke Hallo script in Hallo cloud worden opgeslagen. Als het Hallo-container bestaat niet, wordt deze gemaakt.
   * *RecoveryPlanName***- VMGUIDS**: bij het beveiligen van een virtuele machine Azure Site Recovery elke VM een unieke ID toegewezen die deze code informatie Hallo Hallo VM failover geeft. tooobtain hello VMGUID, selecteer Hallo **Recovery Services** tabblad en klik op **beveiligd Item** &gt; **beveiligingsgroepen** &gt; **Machines** &gt; **eigenschappen**. Als u meerdere virtuele machines hebt, moet u vervolgens Hallo GUID's toevoegen als een door komma's gescheiden tekenreeks.
   * *RecoveryPlanName***- AutomationAccountName** – hello naam van het Hallo automation-account waarin u Hallo runbooks en activa Hallo hebt toegevoegd.

  Bijvoorbeeld, als hello naam van het herstelplan Hallo is fileServerpredayRP, en vervolgens uw **referenties** & **variabelen** tabbladen moeten als volgt worden weergegeven nadat u alle Hallo activa toevoegen.

   ![](./media/storsimple-disaster-recovery-using-azure-site-recovery/image5.png)

7. Ga toohello **Recovery Services** sectie en selecteer hello Azure Site Recovery-kluis die u eerder hebt gemaakt.
8. Selecteer Hallo **herstelplannen (Site Recovery)** optie van **beheren** groeperen en maakt u een nieuwe herstelplan als volgt:

   a.  Klik op **+ herstellen plan** knop klikt, wordt hieronder blade geopend.

      ![](./media/storsimple-disaster-recovery-using-azure-site-recovery/image6.png)

   b.  Voer een naam in recovery plan, kies bron, doel & Deployment model waarden.

   c.  Hallo VM's selecteren uit de beveiligingsgroep Hallo gewenste tooinclude in het herstelplan Hallo en klik op **OK** knop.

   d.  Plan voor herstel die u eerder hebt gemaakt, klik op **aanpassen** tooopen Hallo herstel aanpassing abonnementsweergave van de knop.

   e.  Klik met de rechtermuisknop op **alle groepen afsluiten** en klik op **pre-actie toevoegen**.

   f.  Hiermee opent u actie blade invoegen, voer een naam, selecteer **primaire kant** optie in waar toorun-optie Automation-account (waarbij u toegevoegd Hallo runbooks) en selecteer vervolgens Hallo  **Failover-StorSimple-Volume-Containers** runbook.

   g.  Klik met de rechtermuisknop op **groep 1: Start** en klik op **toevoegen beveiligde items** optie en selecteer het Hallo-virtuele machines die zijn toobe beveiligd in het herstelplan Hallo en klik op **Ok** knop. Optioneel, als deze al is geselecteerd virtuele machines.

   h.  Klik met de rechtermuisknop op **groep 1: Start** en klik op **boeken actie** optie toegevoegd en voeg vervolgens alle Hallo volgende scripts:

   * Runbook starten-StorSimple-virtueel-apparaat
   * Over StorSimple-volume containers runbook mislukt
   * Runbook koppelen volumes na failover
   * Verwijderen-aangepaste--scriptextensie runbook

   ik.  Een handmatige actie toevoegen nadat Hallo hierboven 4 scripts in Hallo dezelfde **groep 1: na stappen** sectie. Deze actie is Hallo-punt waarmee u controleren kunt of alles correct werkt. Deze actie hoeft toobe toegevoegd als onderdeel van de testfailover (dus alleen Selecteer Hallo **Testfailover** selectievakje).

   j.  Na de handmatige actie hello, toevoegen Hallo **opschonen** script met behulp van dezelfde procedure die u voor Hallo gebruikt Hallo andere runbooks. **Sla** Hallo herstelplan.

    > [!NOTE]
    > Wanneer een testfailover wordt uitgevoerd, moet u controleren of alles op Hallo handmatige Actiestap omdat Hallo StorSimple-volumes die op het doelapparaat Hallo had is gekloond wordt verwijderd als onderdeel van Hallo opschoning nadat Hallo handmatige actie is voltooid.
    >

    ![](./media/storsimple-disaster-recovery-using-azure-site-recovery/image7.png)

## <a name="perform-a-test-failover"></a>Een testfailover uitvoeren
Raadpleeg toohello [Active Directory-DR-oplossing](../site-recovery/site-recovery-active-directory.md) aanvullende handleiding voor overwegingen met betrekking tot specifieke tooActive Directory tijdens de testfailover Hallo. Hallo lokale setup is niet op alle Distributed wanneer Hallo testfailover plaatsvindt. Hallo StorSimple-volumes die zijn gekoppeld toohello lokale VM zijn gekloonde toohello StorSimple Cloud toestel op Azure. Een virtuele machine voor testdoeleinden wordt opgeroepen in Azure en hello gekloonde volumes zijn aangesloten toohello VM.

#### <a name="tooperform-hello-test-failover"></a>tooperform hello testfailover
1. In hello Azure-portal, selecteer uw site recovery-kluis.
2. Klik op Hallo herstelplan is gemaakt voor de bestandsserver Hallo VM.
3. Klik op **Testfailover**.
4. Selecteer Hallo virtuele Azure-netwerk toowhich die virtuele Azure-machines moeten worden verbonden nadat er failover plaatsvindt.

   ![](./media/storsimple-disaster-recovery-using-azure-site-recovery/image8.png)
5. Klik op **OK** toobegin Hallo failover. U kunt de voortgang volgen door te klikken op Hallo VM tooopen eigenschappen of op Hallo **Test failover-taak** in kluisnaam &gt; **taken** &gt; **Site Recovery-taken**.
6. Nadat de failover Hallo is voltooid, dient u zich kunt toosee Hallo replica machine van Azure in hello Azure-portal weergegeven &gt; **virtuele Machines**. U kunt uw controles uitvoeren.
7. Nadat het Hallo-controles worden uitgevoerd, klikt u op **validaties voltooid**. Dit wordt opschonen hello StorSimple-Volumes en afsluiten Hallo StorSimple Cloud toestel.
8. Wanneer u bent klaar, klikt u op **testfailover opschonen** op Hallo herstelplan. In de opmerkingen bij de record en sla eventuele opmerkingen die zijn gekoppeld aan Hallo failover testen. Hiermee verwijdert u Hallo virtuele machine die zijn gemaakt tijdens de testfailover.

## <a name="perform-a-planned-failover"></a>Voer een geplande failover
   Tijdens een geplande failover bestandsserver Hallo lokale die virtuele machine correct wordt afgesloten en een cloud back-upmomentopname van Hallo volumes op de StorSimple-apparaat wordt uitgevoerd. Hallo StorSimple-volumes wordt een failover uitgevoerd toohello virtueel apparaat, een replica virtuele machine is opgeroepen in Azure, en de volumes Hallo gekoppelde toohello VM.

#### <a name="tooperform-a-planned-failover"></a>tooperform een geplande failover
1. Selecteer in hello Azure-portal, **herstelservices** kluis &gt; **herstelplannen (siteherstel)** &gt; **recoveryplan_name** gemaakt voor Hallo-bestandsserver VM.
2. Klik op Hallo Recovery plan blade **meer** &gt; **geplande failover**.  

   ![](./media/storsimple-disaster-recovery-using-azure-site-recovery/image9.png)
3. Op Hallo **geplande Failover bevestigen** blade Kies Hallo-bron- en doellocaties en selecteer doelnetwerk en klik op Hallo pictogram ✓ toostart Hallo failover-proces.
4. Nadat de replica virtuele machines worden gemaakt die ze in behandeling status zijn. Klik op **doorvoeren** toocommit Hallo failover.
5. Nadat de replicatie is voltooid, Hallo virtuele machines gestart op de secundaire locatie Hallo.

## <a name="perform-a-failover"></a>Een failover uitvoeren
Tijdens een niet-geplande failover Hallo StorSimple-volumes wordt een failover uitgevoerd toohello virtueel apparaat, een replica virtuele machine wordt opgeroepen in Azure, en Hallo volumes zijn aangesloten toohello VM.

#### <a name="tooperform-a-failover"></a>tooperform een failover
1. Selecteer in hello Azure-portal, **herstelservices** kluis &gt; **herstelplannen (siteherstel)** &gt; **recoveryplan_name** gemaakt voor Hallo-bestandsserver VM.
2. Klik op Hallo Recovery plan blade **meer** &gt; **Failover**.  
3. Op Hallo **bevestigen Failover** blade Hallo bron kiezen en -locaties doel.
4. Selecteer **virtuele machines afsluiten en het synchroniseren van de meest recente gegevens Hallo** toospecify dat Site Recovery moet tooshut omlaag Hallo beveiligde virtuele machine proberen en Hallo gegevens synchroniseren zodat hello meest recente versie van het Hallo-gegevens de failover.
5. Na een failover Hallo zijn Hallo virtuele machines in behandeling status. Klik op **doorvoeren** toocommit Hallo failover.


## <a name="perform-a-failback"></a>Een failback uitvoeren
Tijdens een failback volumecontainers StorSimple wordt een failover uitgevoerd back toohello fysiek apparaat nadat een back-up wordt genomen.

#### <a name="tooperform-a-failback"></a>tooperform een failback
1. Selecteer in de Azure-portal hello, **herstelservices** kluis &gt; **herstelplannen (Site Recovery)** &gt; **recoveryplan_name** gemaakt voor Hallo-bestandsserver VM.
2. Klik op Hallo Recovery plan blade **meer** &gt; **geplande Failover**.  
3. Hallo bron- en doellocaties en selecteer Hallo juiste gegevenssynchronisatie en opties voor het maken van virtuele machine kiest.
4. Klik op **OK** knop toostart Hallo failback proces.

   ![](./media/storsimple-disaster-recovery-using-azure-site-recovery/image10.png)

## <a name="best-practices"></a>Beste praktijken
### <a name="capacity-planning-and-readiness-assessment"></a>Capaciteit plannen en readiness assessment
#### <a name="hyper-v-site"></a>Hyper-V-site
Gebruik Hallo [gebruiker Capaciteitsplanner](http://www.microsoft.com/download/details.aspx?id=39057) toodesign Hallo server-, opslag- en netwerkinfrastructuur voor uw Hyper-V replica-omgeving.

#### <a name="azure"></a>Azure
U kunt uitvoeren Hallo [Azure virtuele Machine Readiness Assessment tool](http://azure.microsoft.com/downloads/vm-readiness-assessment/) op virtuele machines tooensure dat ze compatibel met Azure VM's en Azure Site Recovery-Services zijn. Hallo Readiness Assessment Tool controleert VM configuraties en waarschuwt wanneer configuraties niet compatibel met Azure zijn. Deze geeft bijvoorbeeld een waarschuwing als een station C: groter dan 127 GB is.

Capaciteitsplanning bestaat uit ten minste twee belangrijke processen:

* Toewijzing een on-premises Hyper-V-machines tooAzure VM-grootten (zoals A6, A7, A8 en A9).
* Hallo bepalen vereist internetbandbreedte.

## <a name="limitations"></a>Beperkingen
* Op dit moment slechts 1 StorSimple-apparaat voor failover (tooa eenmalige StorSimple Cloud toestel). Hallo scenario van een bestandsserver die meerdere StorSimple-apparaten omvat is nog niet ondersteund.
* Als u een fout opgetreden krijgt tijdens het inschakelen van beveiliging voor een virtuele machine, ervoor zorgen dat de verbinding hebt verbroken Hallo iSCSI-doelen.
* Alle Hallo volumecontainers die samen zijn gegroepeerd vanwege back-upbeleid over volumecontainers wordt samen failover worden uitgevoerd.
* Hallo volumes in Hallo volumecontainers die u hebt ervoor gekozen wordt failover worden uitgevoerd.
* Volumes die samen toomore dan 64 TB kan geen failover worden omdat Hallo maximale capaciteit van een enkel StorSimple Cloud toestel 64 TB is.
* Als Hallo geplande/niet-geplande failover is mislukt en Hallo virtuele machines worden gemaakt in Azure, Hallo kan niet opschoning van virtuele machines. In plaats daarvan een failback doen. Als u virtuele machines Hallo verwijdert vervolgens Hallo lokale virtuele machines kunnen niet opnieuw worden ingeschakeld.
* Na een failover, als u niet kunt toosee Hallo volumes, Ga toohello virtuele machines, opent u Schijfbeheer, Hallo schijven opnieuw controleren en ze online brengt.
* In sommige gevallen kan Hallo stationsletters in Hallo DR-site Hallo letters lokale anders zijn. Als dit het geval is, moet u toomanually juiste Hallo probleem nadat Hallo failover is voltooid.
* Multi-factor authentication-server moet zijn uitgeschakeld voor hello wordt ingevoerd in Hallo automation-account als een actief Azure-referentie. Als deze verificatie niet is uitgeschakeld, scripts niet kunnen worden toorun automatisch en Hallo herstelplan zal mislukken.
* De time-out van de failover-taak: Hallo StorSimple script time-out wordt als Hallo failover van volumecontainers langer duurt dan de limiet van de Azure Site Recovery Hallo per script (momenteel 120 minuten).
* Back-uptaak time-out: Hallo StorSimple script een time-out optreedt als Hallo back-up van volumes langer dan de limiet van de Azure Site Recovery Hallo per script (momenteel 120 minuten duurt).

  > [!IMPORTANT]
  > Hallo back-up handmatig uitvoeren vanuit hello Azure-portal en voer het herstelplan Hallo vervolgens opnieuw.

* Time-out van taak klonen: Hallo StorSimple script een time-out optreedt als Hallo klonen van volumes langer dan de limiet van de Azure Site Recovery Hallo per script (momenteel 120 minuten duurt).
* Synchronisatiefout tijd: Hallo StorSimple scripts fouten uit zeggen dat Hallo back-ups mislukt was Hoewel Hallo back-up voltooid in Hallo-portal is. Een mogelijke oorzaak hiervoor is mogelijk dat Hallo StorSimple toestel tijd is mogelijk niet gesynchroniseerd met de Hallo huidige tijd in de tijdzone Hallo.

  > [!IMPORTANT]
  > Hallo toestel synchronisatietijd Hello huidige tijd in Hallo-tijdzone.

* Toestel failover-fout: Hallo StorSimple-script kan mislukken als er een failover toestel wanneer Hallo herstelplan wordt uitgevoerd.

  > [!IMPORTANT]
  > Voer Hallo herstelplan nadat Hallo toestel failover voltooid is.


## <a name="summary"></a>Samenvatting
Met Azure Site Recovery kunt u een herstelplan volledig geautomatiseerd noodherstel voor een bestandsserver VM maken met bestandsshares die worden gehost op een StorSimple-opslag. U kunt het Hallo failover initiëren binnen enkele seconden vanaf elke locatie in Hallo-gebeurtenis van een onderbreking van de en krijgt u de toepassing hello binnen een paar minuten.

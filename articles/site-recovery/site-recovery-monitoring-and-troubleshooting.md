---
title: aaaMonitor en beveiliging voor virtuele machines en fysieke servers oplossen | Microsoft Docs
description: "Azure Site Recovery coördineert Hallo replicatie, failovers en herstel van virtuele machines op de lokale servers tooAzure of een secundair datacenter. Gebruik dit artikel toomonitor en problemen met beveiliging van Virtual Machine Manager- of Hyper-V-site."
services: site-recovery
documentationcenter: 
author: ruturaj
manager: mkjain
editor: 
ms.assetid: 0fc8e368-0c0e-4bb1-9d50-cffd5ad0853f
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/05/2017
ms.author: rajanaki
ms.openlocfilehash: d790375db5f30e98f009c8d8272558188c51934c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-troubleshoot-protection-for-virtual-machines-and-physical-servers"></a>Controleren en problemen oplossen van beveiliging voor virtuele machines en fysieke servers
Deze bewaking en probleemoplossing van handleiding helpt u leert hoe tootrack replicatiestatus en technieken voor Azure Site Recovery oplossen.

## <a name="understand-hello-components"></a>Inzicht in Hallo-onderdelen
### <a name="vmware-virtual-machine-or-physical-server-site-deployment-for-replication-between-on-premises-and-azure"></a>Virtuele VMware-machine of fysieke server site-implementatie voor replicatie tussen de on-premises en Azure
tooset up databaseherstel tussen een on-premises VMware virtuele machine of fysieke server en Azure, moet u tooset van configuratieserver hello, hoofddoelserver en serveronderdelen proces op de virtuele machine of de server. Wanneer u beveiliging voor de bronserver Hallo inschakelt, installeert Azure Site Recovery Hallo Mobile Apps-functie van Microsoft Azure App Service. Na een storing van de lokale en Hallo bron server een failover tooAzure moeten klanten tooset van een processerver in Azure en een hoofddoelserver op lokale toorebuild Hallo-bronserver on-premises.

![VMware of fysieke-site-implementatie voor replicatie tussen de on-premises en Azure](media/site-recovery-monitoring-and-troubleshooting/image18.png)

### <a name="virtual-machine-manager-site-deployment-for-replication-between-on-premises-sites"></a>Implementatie van de Virtual Machine Manager-sites voor replicatie tussen on-premises sites
tooset up databaseherstel tussen twee on-premises locaties, u moet toodownload hello Azure Site Recovery provider en op Hallo Virtual Machine Manager-beheerserver installeren. Hallo-provider moet Internet connectiviteit tooensure dat alle Hallo-bewerkingen die zijn geactiveerd vanuit hello Azure-portal vertaalde tooon-premises bewerkingen ophalen.

![Implementatie van de Virtual Machine Manager-sites voor replicatie tussen on-premises sites](media/site-recovery-monitoring-and-troubleshooting/image1.png)

### <a name="virtual-machine-manager-site-deployment-for-replication-between-on-premises-locations-and-azure"></a>Implementatie van de Virtual Machine Manager-sites voor replicatie tussen lokale locaties en Azure
Bij het instellen van databaseherstel tussen lokale locaties en Azure, kunt u toodownload hello Azure Site Recovery provider nodig en deze op Hallo Virtual Machine Manager-beheerserver installeren. U moet ook tooinstall hello Azure Recovery Services Agent, die toobe geïnstalleerd op elke Hyper-V-host moet. [Meer informatie](site-recovery-hyper-v-azure-architecture.md) voor meer informatie.

![Implementatie van de Virtual Machine Manager-sites voor replicatie tussen lokale locaties en Azure](media/site-recovery-monitoring-and-troubleshooting/image2.png)

### <a name="hyper-v-site-deployment-for-replication-between-on-premises-locations-and-azure"></a>Hyper-V-site-implementatie voor replicatie tussen lokale locaties en Azure
Dit proces is vergelijkbaar tooVirtual Machine Manager-implementatie. Hallo enige verschil is dat hello Azure Site Recovery provider en de Azure Recovery Services Agent geïnstalleerd op Hallo Hyper-V-host zelf. [Meer informatie](site-recovery-hyper-v-azure-architecture.md). .

## <a name="monitor-configuration-protection-and-recovery-operations"></a>Bewaak de bewerkingen van configuratie-, beveiligings- en hersteltaken
Elke bewerking in de Azure Site Recovery wordt gecontroleerd en bijgehouden onder Hallo **taken** tabblad. Ga voor een configuratie, beveiliging of herstel fout, toohello **taken** tabblad en zoekt u fouten.

![Hallo mislukt filter in het tabblad Hallo-taken](media/site-recovery-monitoring-and-troubleshooting/image3.png)

Als u fouten optreden bij Hallo vinden **taken** tabblad Hallo-taak op en klik op **FOUTDETAILS** voor die taak.

![Hallo FOUTDETAILS knop](media/site-recovery-monitoring-and-troubleshooting/image4.png)

Hallo foutdetails kunt u een mogelijke oorzaak en de aanbeveling voor Hallo probleem identificeren.

![Dialoogvenster met daarin de foutdetails voor een specifieke taak](media/site-recovery-monitoring-and-troubleshooting/image5.png)

In het vorige voorbeeld hello er een andere bewerking die bezig is toobe Hallo beveiliging configuratie toofail veroorzaakt. Hallo oplossen op basis van Hallo aanbeveling en klik vervolgens op **RESART** tooinitiate Hallo opnieuw.

![Hallo opnieuw opstarten om op tabblad Hallo-taken](media/site-recovery-monitoring-and-troubleshooting/image6.png)

Hallo **opnieuw** optie is niet beschikbaar voor alle bewerkingen. Als er een bewerking geen Hallo **opnieuw** optie, gaat u terug toohello object en opnieuw Hallo opnieuw. U kunt elke taak die in voortgang annuleren met behulp van Hallo **annuleren** knop.

![de knop Annuleren Hallo](media/site-recovery-monitoring-and-troubleshooting/image7.png)

## <a name="monitor-replication-health-for-virtual-machines"></a>Status van de replicatie voor virtuele machines controleren
U kunt hello Azure portal tooremotely monitor Azure Site Recovery-providers gebruiken voor elk beveiligd Hallo entiteiten. Klik op **beveiligde ITEMS**, en klik vervolgens op **VMM-CLOUDS** of **BEVEILIGINGSGROEPEN**. Hallo **VMM-CLOUDS** tabblad is alleen beschikbaar voor implementaties die zijn gebaseerd op Virtual Machine Manager. Hallo beveiligd entiteiten zijn voor andere scenario's, onder Hallo **BEVEILIGINGSGROEPEN** tabblad.

![Hallo VMM-Clouds en BEVEILIGINGSGROEPEN opties](media/site-recovery-monitoring-and-troubleshooting/image8.png)

Klik op een beveiligde entiteit onder Hallo respectieve cloud of protection groep toosee die alle beschikbare bewerkingen worden weergegeven in het onderste deelvenster van Hallo.

![Beschikbare opties voor een geselecteerde beveiligde entiteit](media/site-recovery-monitoring-and-troubleshooting/image9.png)

Zoals u in de vorige schermafbeelding hello, status van de virtuele machine Hallo is **Kritiek**. U kunt klikken op Hallo **FOUTDETAILS** knop op Hallo onder toosee Hallo fout. Op basis van Hallo **mogelijke oorzaken** en **aanbeveling**, Hallo-probleem opgelost.

![Hallo foutdetails knop](media/site-recovery-monitoring-and-troubleshooting/image10.png)

![Fouten en aanbevelingen in het dialoogvenster van Hallo foutdetails](media/site-recovery-monitoring-and-troubleshooting/image11.png)

> [!NOTE]
> Als er geen actieve bewerkingen worden uitgevoerd of is mislukt, gaat u toohello **taken** als genoemde eerdere tooview Hallo fout voor een specifieke taak weergeven.
>
>

## <a name="troubleshoot-on-premises-hyper-v-issues"></a>Problemen met lokale Hyper-V
Verbind toohello lokale Hyper-V manager-console selecteert Hallo virtuele machine, en Zie Hallo replicatiestatus.

![Optie tooview replicatiestatus in Hallo Hyper-V manager-console](media/site-recovery-monitoring-and-troubleshooting/image12.png)

In dit geval **replicatiestatus** is **Kritiek**. Met de rechtermuisknop op Hallo virtuele machine en klik vervolgens op **replicatie** > **replicatiestatus weergeven** toosee Hallo details.

![Status van de replicatie voor een specifieke virtuele machine](media/site-recovery-monitoring-and-troubleshooting/image13.png)

Als replicatie is onderbroken voor Hallo virtuele machine, met de rechtermuisknop op Hallo virtuele machine en klik vervolgens op **replicatie** > **replicatie hervatten**.

![Optie tooresume replicatie in Hallo Hyper-V manager-console](media/site-recovery-monitoring-and-troubleshooting/image19.png)

Als een virtuele machine wordt gemigreerd een nieuwe Hyper-V-host die zich binnen het Hallo-cluster of een zelfstandige computer en Hallo Hyper-V-host via de Azure Site Recovery is geconfigureerd, kunt u replicatie voor virtuele-machine Hallo wouldn't beïnvloed. Zorg ervoor dat nieuwe Hyper-V-host van Hallo voldoet aan alle vereisten voor Hallo en wordt geconfigureerd met behulp van Azure Site Recovery.

### <a name="event-log"></a>Gebeurtenislogboek
| Bronnen van gebeurtenissen | Details |
| --- |:--- |
| **Toepassingen en Service-logboeken/Microsoft/beheer voor virtuele machines/Server/Admin** (Virtual Machine Manager-beheerserver) |Biedt nuttige logboekregistratie tootroubleshoot veel verschillende Virtual Machine Manager-problemen. |
| **Toepassingen en Service MicrosoftAzureRecoveryServices-logboeken/replicatie** (Hyper-V-host) |Biedt nuttige logboekregistratie tootroubleshoot veel problemen met Microsoft Azure Recovery Services Agent. <br/> ![Locatie van de gebeurtenisbron replicatie voor Hyper-V-host](media/site-recovery-monitoring-and-troubleshooting/eventviewer03.png) |
| **Toepassingen en Service Microsoft-logboeken/Azure Site Recovery/Provider/operationeel** (Hyper-V-host) |Biedt nuttige logboekregistratie tootroubleshoot veel problemen met Microsoft Azure Site Recovery Service. <br/> ![Locatie van de bron van de operationele gebeurtenissen voor Hyper-V-host](media/site-recovery-monitoring-and-troubleshooting/eventviewer02.png) |
| **Toepassingen en Service-logboeken/Microsoft/Windows/Hyper-V-VMMS/Admin** (Hyper-V-host) |Biedt nuttige logboekregistratie tootroubleshoot veel management problemen van de Hyper-V virtuele machine. <br/> ![Locatie van de Virtual Machine Manager-gegevensbron voor Hyper-V-host](media/site-recovery-monitoring-and-troubleshooting/eventviewer01.png) |

### <a name="hyper-v-replication-logging-options"></a>Opties voor logboekregistratie van Hyper-V-replicatie
Alle gebeurtenissen die betrekking tooHyper-V-replicatie hebben worden vastgelegd in Hyper-V-VMMS hello\\bevindt zich onder logboeken toepassingen en Services van beheerder logboek\\Microsoft\\Windows. U kunt bovendien een analytische logboek voor Hallo Hyper-V Virtual Machine Management-Service inschakelen. tooenable dit zich aanmeldt, eerst Hallo analyse en foutopsporing Logboeken in Logboeken Hallo kan worden weergegeven. Open Logboeken en klik vervolgens op **weergave** > **analytische weergeven logboeken en foutopsporing**.

![Hallo optie analytische weergeven en logboeken voor foutopsporing](media/site-recovery-monitoring-and-troubleshooting/image14.png)

Er is een analytische logboek zichtbaar onder **Hyper-V-VMMS**.

![Hallo analysen Hallo logboeken structuur aanmelden](media/site-recovery-monitoring-and-troubleshooting/image15.png)

In Hallo **acties** deelvenster, klikt u op **logboek inschakelen**. Nadat deze ingeschakeld, wordt deze weergegeven in **Prestatiemeter** als een **gebeurtenistraceersessies** zich onder **gegevensverzamelaarsets.**

![Gebeurtenistraceersessies in Hallo Prestatiemeter structuur](media/site-recovery-monitoring-and-troubleshooting/image16.png)

tooview Hallo verzamelde gegevens, eerst Hallo-traceringssessie stoppen door Hallo logboek uit te schakelen. Hallo-logboek, opslaan en opnieuw openen in Logboeken of gebruik een andere tooconvert hulpprogramma's voor het gewenste.

## <a name="reach-out-for-microsoft-support"></a>Voor Microsoft Support bereiken
### <a name="log-collection"></a>Logboekgegevens verzameld
Raadpleeg te voor beveiliging van de Virtual Machine Manager-site,[Azure Site Recovery logboekgegevens verzameld met ondersteuning Diagnostics Platform (SDP) hulpprogramma](http://social.technet.microsoft.com/wiki/contents/articles/28198.asr-data-collection-and-analysis-using-the-vmm-support-diagnostics-platform-sdp-tool.aspx) toocollect Hallo logboeken vereist.

Voor de beveiliging van Hyper-V-site, downloadt u de [hulpprogramma](https://dcupload.microsoft.com/tools/win7files/DIAG_ASRHyperV_global.DiagCab) en uit te voeren op Hallo Hyper-V-host toocollect Hallo Logboeken.

Raadpleeg te voor VMware of fysieke-serverscenario's[Azure Site Recovery logboekgegevens verzameld voor VMware en fysieke site beveiliging](http://social.technet.microsoft.com/wiki/contents/articles/30677.azure-site-recovery-log-collection-for-vmware-and-physical-site-protection.aspx) toocollect Hallo logboeken vereist.

Hallo hulpprogramma verzamelt logboeken Hallo lokaal in een willekeurige naam submap onder % LocalAppData%\ElevatedDiagnostics.

![Voorbeeldstappen uit de beveiliging van Hyper-V-site.](media/site-recovery-monitoring-and-troubleshooting/animate01.gif)

### <a name="open-a-support-ticket"></a>Een ondersteuningsticket opent
een ondersteuningsticket voor Azure Site Recovery tooraise bereiken tooAzure ondersteuning via de URL op <http://aka.ms/getazuresupport>.

## <a name="kb-articles"></a>KB-artikelen
* [Hoe toopreserve Hallo stationsletter voor virtuele machines die zijn failover of gemigreerd tooAzure beveiligd](http://support.microsoft.com/kb/3031135)
* [Hoe toomanage lokale tooAzure beveiliging gebruik van netwerkbandbreedte](https://support.microsoft.com/kb/3056159)
* [Azure Site Recovery: 'hello clusterbron kan niet worden gevonden' fout wanneer u tooenable beveiliging voor een virtuele machine probeert](http://support.microsoft.com/kb/3010979)
* [Begrijpen en oplossen van Hyper-V-replicatie helpen](http://social.technet.microsoft.com/wiki/contents/articles/21948.hyper-v-replica-troubleshooting-guide.aspx)

## <a name="common-azure-site-recovery-errors-and-their-resolutions"></a>Veelvoorkomende fouten voor Azure Site Recovery en hun oplossingen
Hieronder vindt u veelvoorkomende fouten en hun oplossingen. Elke fout wordt beschreven in een afzonderlijke wiki-pagina.

### <a name="general"></a>Algemeen
* <span style="color:green;">NIEUWE</span> [taken mislukken met fout "Er is een bewerking is uitgevoerd." Fout bij het 505, 514, 532.](http://social.technet.microsoft.com/wiki/contents/articles/32190.azure-site-recovery-jobs-failing-with-error-an-operation-is-in-progress-error-505-514-532.aspx)
* <span style="color:green;">NIEUWE</span> [taken mislukken met fout 'De Server niet verbonden toohello Internet'. Fout bij het 25018.](http://social.technet.microsoft.com/wiki/contents/articles/32192.azure-site-recovery-jobs-failing-with-error-server-isn-t-connected-to-the-internet-error-25018.aspx)

### <a name="setup"></a>Instellen
* [Hallo Virtual Machine Manager-beheerserver kan niet worden geregistreerd vanwege een interne fout tooan. Raadpleeg de taakweergave toohello in Hallo Site Recovery-portal voor meer informatie over het Hallo-fout. Voer setup opnieuw tooregister Hallo-server.](http://social.technet.microsoft.com/wiki/contents/articles/25570.the-vmm-server-cannot-be-registered-due-to-an-internal-error-please-refer-to-the-jobs-view-in-the-site-recovery-portal-for-more-details-on-the-error-run-setup-again-to-register-the-server.aspx)
* [Een verbinding kan niet tot stand gebrachte toohello Hyper-V Recovery Manager kluis. Controleer of Hallo proxy-instellingen of probeer het later opnieuw.](http://social.technet.microsoft.com/wiki/contents/articles/25571.a-connection-cant-be-established-to-the-hyper-v-recovery-manager-vault-verify-the-proxy-settings-or-try-again-later.aspx)

### <a name="configuration"></a>Configuratie
* [Kan geen toocreate beveiligingsgroep: Er is een fout opgetreden tijdens het ophalen van lijst met servers Hallo.](http://blogs.technet.com/b/somaning/archive/2015/08/12/unable-to-create-the-protection-group-in-azure-site-recovery-portal.aspx)
* [Hyper-V-hostcluster bevat ten minste één statische netwerkadapter of er zijn geen verbonden adapters geconfigureerd toouse DHCP zijn.](http://social.technet.microsoft.com/wiki/contents/articles/25498.hyper-v-host-cluster-contains-at-least-one-static-network-adapter-or-no-connected-adapters-are-configured-to-use-dhcp.aspx)
* [Virtual Machine Manager heeft geen machtigingen toocomplete een actie.](http://social.technet.microsoft.com/wiki/contents/articles/31110.vmm-does-not-have-permissions-to-complete-an-action.aspx)
* [Kan geen opslagaccount Hallo binnen Hallo abonnement tijdens het configureren van beveiliging selecteren.](http://social.technet.microsoft.com/wiki/contents/articles/32027.can-t-select-the-storage-account-within-the-subscription-while-configuring-protection.aspx)

### <a name="protection"></a>Beveiliging
* <span style="color:green;">NIEUWE</span> [beveiliging inschakelen is mislukt met fout "Kan beveiliging niet configureren voor de virtuele machine van Hallo". Fout 60007, 40003.](http://social.technet.microsoft.com/wiki/contents/articles/32194.azure-site-recovery-enable-protection-failing-with-error-protection-couldn-t-be-configured-for-the-virtual-machine-error-60007-40003.aspx)
* <span style="color:green;">NIEUWE</span> [beveiliging inschakelen is mislukt met fout 'Beveiliging kan niet worden ingeschakeld voor Hallo virtuele machine'. Fout bij het 70094.](http://social.technet.microsoft.com/wiki/contents/articles/32195.azure-site-recovery-enable-protection-failing-with-error-protection-couldn-t-be-enabled-for-the-virtual-machine-error-70094.aspx)
* <span style="color:green;">NIEUWE</span> [livemigratie fout 23848 - Hallo virtuele machine verplaatst met type Live toobe gaat. Hierdoor kan Hallo beschermingsstatus voor herstel van virtuele machine van Hallo verbroken.](http://social.technet.microsoft.com/wiki/contents/articles/32021.live-migration-error-23848-the-virtual-machine-is-going-to-be-moved-using-type-live-this-could-break-the-recovery-protection-status-of-the-virtual-machine.aspx)
* [Schakel de beveiliging is mislukt, omdat de Agent is niet geïnstalleerd op de hostmachine.](http://social.technet.microsoft.com/wiki/contents/articles/31105.enable-protection-failed-since-agent-not-installed-on-host-machine.aspx)
* [Is geen geschikte host voor Hallo replica virtuele machine kan niet gevonden - vervaldatum toolow rekenresources.](http://social.technet.microsoft.com/wiki/contents/articles/25501.a-suitable-host-for-the-replica-virtual-machine-can-t-be-found-due-to-low-compute-resources.aspx)
* [Is geen geschikte host voor Hallo replica virtuele machine kan niet worden gevonden - vanwege toono logisch netwerk gekoppeld.](http://social.technet.microsoft.com/wiki/contents/articles/25502.a-suitable-host-for-the-replica-virtual-machine-can-t-be-found-due-to-no-logical-network-attached.aspx)
* [Kan geen verbinding maken toohello replica hostmachine - kan geen verbinding worden gemaakt.](http://social.technet.microsoft.com/wiki/contents/articles/31106.cannot-connect-to-the-replica-host-machine-connection-could-not-be-established.aspx)

### <a name="recovery"></a>Herstel
* Virtual Machine Manager kan geen Hallo hostbewerking niet voltooien:
  * [Failover-toohello geselecteerd herstelpunt voor de virtuele machine: algemene fout: toegang geweigerd.](http://social.technet.microsoft.com/wiki/contents/articles/25504.fail-over-to-the-selected-recovery-point-for-virtual-machine-general-access-denied-error.aspx)
  * [Hyper-V mislukte toofail via toohello geselecteerd herstelpunt voor de virtuele machine: bewerking is afgebroken.  Probeer een meer recente herstelpunt. (0x80004004).](http://social.technet.microsoft.com/wiki/contents/articles/25503.hyper-v-failed-to-fail-over-to-the-selected-recovery-point-for-virtual-machine-operation-aborted-try-a-more-recent-recovery-point-0x80004004.aspx)
  * Een verbinding met Hallo-server kan niet worden vastgesteld (0x00002EFD).
    * [Hyper-V is mislukt tooenable omgekeerde replicatie voor virtuele machine.](http://social.technet.microsoft.com/wiki/contents/articles/25505.a-connection-with-the-server-could-not-be-established-0x00002efd-hyper-v-failed-to-enable-reverse-replication-for-virtual-machine.aspx)
    * [Hyper-V tooenable-replicatie voor virtuele machine virtuele machine is mislukt.](http://social.technet.microsoft.com/wiki/contents/articles/25506.a-connection-with-the-server-could-not-be-established-0x00002efd-hyper-v-failed-to-enable-replication-for-virtual-machine-virtual-machine.aspx)
  * [Failover voor virtuele machine kan niet worden doorgevoerd.](http://social.technet.microsoft.com/wiki/contents/articles/25508.could-not-commit-failover-for-virtual-machine.aspx)
* [Hallo herstelplan bevat virtuele machines die niet gereed voor geplande failover.](http://social.technet.microsoft.com/wiki/contents/articles/25509.the-recovery-plan-contains-virtual-machines-which-are-not-ready-for-planned-failover.aspx)
* [Hallo virtuele machine is niet gereed voor geplande failover.](http://social.technet.microsoft.com/wiki/contents/articles/25507.the-virtual-machine-isn-t-ready-for-planned-failover.aspx)
* [Virtuele machine wordt niet uitgevoerd en wordt niet uitgeschakeld.](http://social.technet.microsoft.com/wiki/contents/articles/25510.virtual-machine-is-not-running-and-is-not-powered-off.aspx)
* [Buiten-band-bewerking opgetreden op een virtuele machine en de doorvoering van de failover is mislukt.](http://social.technet.microsoft.com/wiki/contents/articles/25507.the-virtual-machine-isn-t-ready-for-planned-failover.aspx)
* Testfailover
  * [Failover kan niet worden gestart omdat de testfailover wordt uitgevoerd.](http://social.technet.microsoft.com/wiki/contents/articles/31111.failover-could-not-be-initiated-since-test-failover-is-in-progress.aspx)
* <span style="color:green;">NIEUWE</span> Failover een time-out optreedt bij PreFailoverWorkflow taak WaitForScriptExecutionTaskTimeout vanwege toohello configuratie-instellingen op Hallo Netwerkbeveiligingsgroep gekoppeld aan de virtuele Machine Hallo of Hallo subnet toowhich Hallo machine behoort. Raadpleeg te[PreFailoverWorkflow taak WaitForScriptExecutionTaskTimeout](https://aka.ms/troubleshoot-nsg-issue-azure-site-recovery) voor meer informatie.

### <a name="configuration-server-process-server-master-target"></a>Configuratieserver, processerver, hoofddoel
* [Hallo ESXi-host op welke Hallo PS/CS wordt gehost als een virtuele machine is mislukt met een paarse scherm.](http://social.technet.microsoft.com/wiki/contents/articles/31107.vmware-esxi-host-experiences-a-purple-screen-of-death.aspx)

### <a name="remote-desktop-troubleshooting-after-failover"></a>Extern bureaublad probleemoplossing na een failover
* Veel klanten hebben geconfronteerd met problemen tooconnect toohello failover van virtuele machine in Azure. [Gebruik Hallo document tooRDP probleemoplossing naar Hallo virtuele machine](http://social.technet.microsoft.com/wiki/contents/articles/31666.troubleshooting-remote-desktop-connection-after-failover-using-asr.aspx).

#### <a name="adding-a-public-ip-on-a-resource-manager-virtual-machine"></a>Een openbaar IP-adres toe te voegen op een virtuele machine van de resource manager
Als hello **Connect** knop in Hallo portal grijs wordt weergegeven, en u niet bent verbonden tooAzure via een Express Route of Site-naar-Site VPN-verbinding, wordt u toocreate nodig hebt en uw virtuele machine een openbare IP-adres toewijzen voordat u extern kunt Bureaublad/gedeeld Shell. Vervolgens kunt u een openbaar IP-adres toevoegen aan de netwerkinterface Hallo van Hallo virtuele machine.  

![Virtuele machine toe te voegen een openbaar IP-adres op de netwerkinterface Hallo van failover](media/site-recovery-monitoring-and-troubleshooting/createpublicip.gif)

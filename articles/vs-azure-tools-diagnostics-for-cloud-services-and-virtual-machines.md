---
title: Diagnostische gegevens voor Azure Cloud Services en virtuele Machines aaaConfiguring | Microsoft Docs
description: Hierin wordt beschreven hoe tooconfigure diagnostische gegevens voor het opsporen van Azure cloude services en virtuele machines (VM's) in Visual Studio.
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: e70cd7b4-6298-43aa-adea-6fd618414c26
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 11/11/2016
ms.author: kraigb
ms.openlocfilehash: 74cdf49413d6d89a84195070dd9d817da2463373
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-diagnostics-for-azure-cloud-services-and-virtual-machines"></a>Configuratie van diagnostische gegevens voor Azure-Cloudservices en virtuele Machines
Wanneer u tootroubleshoot een Azure-cloudservice of virtuele machine van Azure moet, kunt u gemakkelijker Azure diagnostics configureren met behulp van Visual Studio. Azure diagnostics vastgelegd systeem en gegevens van de logboekregistratie op Hallo virtuele machines en virtuele machine-exemplaren die uw cloudservice worden uitgevoerd en die gegevens overgebracht naar een opslagaccount van uw keuze. Zie [logboekregistratie van diagnostische gegevens van web-apps in Azure App Service](app-service-web/web-sites-enable-diagnostic-log.md) voor meer informatie over diagnostische gegevens van logboekregistratie in Azure.

Dit onderwerp leest u hoe tooenable en configureren van Azure diagnostics in Visual Studio, zowel voor en na de implementatie, evenals in virtuele machines in Azure. Hier ook ziet u hoe tooselect Hallo typen diagnostische informatie toocollect en hoe tooview Hallo informatie nadat deze worden verzameld.

U kunt Azure Diagnostics configureren in de volgende manieren Hallo:

* U kunt configuratie-instellingen voor diagnostische gegevens via Hallo wijzigen **configuratie van diagnostische** dialoogvenster in Visual Studio. Hallo-instellingen worden opgeslagen in een bestand met de naam diagnostics.wadcfgx (diagnostics.wadcfg in Azure SDK 2.4 of eerder). U kunt ook rechtstreeks Hallo configuratiebestand wijzigen. Als u handmatig Hallo bestand bijwerkt, wordt Hallo configuratiewijzigingen treden Hallo volgende keer dat u Hallo cloud service tooAzure of Voer Hallo-service in Hallo-emulator implementeert.
* Gebruik **Cloud Explorer** of **Server Explorer** in Visual Studio toochange Hallo diagnostische instellingen voor een actieve cloudservice of virtuele machine.

## <a name="azure-26-diagnostics-changes"></a>2.6 Azure diagnostics wijzigingen
Azure SDK 2.6-projecten in Visual Studio, zijn Hallo volgende wijzigingen aangebracht. (Deze wijzigingen gelden ook toolater versies van Azure SDK.)

* Hallo lokale emulator ondersteunt nu de diagnostische gegevens. Dit betekent dat u kunt het verzamelen van diagnostische gegevens en zorg ervoor dat uw toepassing maakt Hallo rechts traceringen tijdens het ontwikkelen en testen in Visual Studio. Hallo verbindingsreeks `UseDevelopmentStorage=true` kunt verzamelen van diagnostische gegevens, terwijl u uw cloudserviceproject in Visual Studio uitvoert met behulp van hello Azure-opslagemulator. Alle diagnostische gegevens worden verzameld in opslagaccount hello (ontwikkeling opslag).
* Hallo diagnostics account verbindingsreeks voor opslag (Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString) wordt nog een keer opgeslagen in hello (.cscfg) serviceconfiguratiebestand. In de Azure SDK 2.5 is Hallo diagnostics storage-account opgegeven in Hallo diagnostics.wadcfgx bestand.

Er zijn enkele belangrijke verschillen tussen hoe Hallo-verbindingsreeks in de Azure SDK 2.4 en eerder gegaan en hoe het werkt in de Azure SDK 2.6 en hoger.

* In de Azure SDK 2.4 en eerder is Hallo-verbindingsreeks gebruikt als een runtime door Hallo diagnostics tooget Hallo storage account informatie over de invoegtoepassing voor het overdragen van diagnostische logboeken.
* In Azure SDK 2.6 en hoger worden Hallo diagnostics verbindingsreeks wordt gebruikt door de extensie voor Visual Studio tooconfigure Hallo diagnostische gegevens met gegevens van de juiste opslag Hallo tijdens de publicatie. Hallo-verbindingsreeks kunt u verschillende opslagaccounts voor verschillende configuraties die door Visual Studio wordt gebruikt bij het publiceren van definiëren. Omdat Hallo diagnostics-invoegtoepassing (na de Azure SDK 2,5) niet langer beschikbaar is, kan niet Hallo cscfg-bestand zelf echter Hallo extensie voor diagnostische gegevens inschakelen. U hebt tooenable Hallo extensie afzonderlijk via hulpprogramma's zoals Visual Studio of PowerShell.
* toosimplify hello proces van het Hallo-extensie voor diagnostische gegevens configureren met PowerShell, Hallo pakket uitvoer vanuit Visual Studio bevat ook Hallo openbare configuratie-XML voor Hallo-extensie voor diagnostische gegevens voor elke rol. Visual Studio gebruikt Hallo diagnostics toopopulate Hallo storage account verbindingsinformatie aanwezig is in de openbare configuratie Hallo. Hallo openbare config-bestanden worden gemaakt in de map extensies Hallo en Hallo patroon PaaSDiagnostics volgen. &lt;RoleName >. PubConfig.xml. Alle implementaties op basis van PowerShell kunnen gebruiken dit patroon toomap elke configuratie tooa rol.
* Hallo-verbindingsreeks in Hallo .cscfg-bestand wordt ook gebruikt door Hallo [Azure-portal](http://go.microsoft.com/fwlink/p/?LinkID=525040) tooaccess Hallo diagnostics-gegevens, zodat het kan worden weergegeven in Hallo **bewaking** tabblad Hallo-verbindingsreeks is vereist tooconfigure hello service tooshow uitgebreide bewakingsgegevens in Hallo-portal.

## <a name="migrating-projects-tooazure-sdk-26-and-later"></a>Migreren projecten tooAzure SDK 2.6 en hoger
Bij het migreren van Azure SDK 2.5 tooAzure SDK 2.6 of hoger, als u een opslagaccount voor diagnostische gegevens opgegeven in Hallo .wadcfgx bestand had vervolgens blijft er. tootake profiteren van Hallo flexibiliteit voor het gebruik van andere opslag van accounts voor opslagconfiguraties verschillende, hebt u toomanually Hallo connection string tooyour project toevoegen. Als u een project waarnaar u migreert van Azure SDK 2.4 of eerdere tooAzure SDK 2.6, Hallo vervolgens diagnostics verbindingsreeksen behouden blijven. Let echter Hallo wijzigingen in hoe verbindingsreeksen worden behandeld in de Azure SDK 2.6 zoals opgegeven in de vorige sectie Hallo.

### <a name="how-visual-studio-determines-hello-diagnostics-storage-account"></a>Hoe Visual Studio bepaalt Hallo opslagaccount voor diagnostische gegevens
* Als een verbindingsreeks diagnostische gegevens is opgegeven in het .cscfg-bestand hello, Visual Studio gebruikt deze extensie voor diagnostische gegevens van tooconfigure Hallo bij het publiceren en bij het genereren van Hallo openbare configuratie voor XML-bestanden tijdens de verpakking.
* Als geen verbindingsreeks diagnostics is opgegeven in het .cscfg-bestand hello, klikt u vervolgens terugvalt Visual Studio toousing Hallo storage-account opgegeven in Hallo .wadcfgx bestand tooconfigure Hallo extensie voor diagnostische gegevens bij het publiceren en Hallo openbare genereren XML-configuratiebestanden wanneer verpakken.
* Hallo diagnostics verbindingsreeks in Hallo .cscfg-bestand heeft voorrang op Hallo storage-account in Hallo .wadcfgx bestand. Als u een verbindingsreeks diagnostics is opgegeven in Hallo cscfg-bestand, vervolgens Visual Studio wordt gebruikt, wordt en Hallo storage-account in .wadcfgx worden genegeerd.

### <a name="what-does-hello-update-development-storage-connection-strings-checkbox-do"></a>Wat Hallo 'Bijwerken ontwikkeling storage-verbindingsreeksen...' selectievakje doen?
selectievakje voor Hallo **bijwerken van ontwikkeling storage-verbindingsreeksen voor diagnostische gegevens en opslaan in cache met Microsoft Azure storage-accountreferenties bij het publiceren van tooMicrosoft Azure** beschikt u over een handige manier tooupdate ieder ontwikkeling opslagaccountverbindingsreeksen met hello Azure storage-account is opgegeven tijdens de publicatie.

Stel bijvoorbeeld dat u dit selectievakje inschakelt en Hallo diagnostics verbindingsreeks `UseDevelopmentStorage=true`. Wanneer u Hallo project tooAzure publiceert, wordt Visual Studio Hallo diagnostics verbindingsreeks automatisch bijgewerkt met de Hallo storage-account die u hebt opgegeven in de wizard Publiceren Hallo. Echter, als een echte storage-account is opgegeven als Hallo diagnostische gegevens van de verbindingsreeks, vervolgens dat account wordt gebruikt in plaats daarvan.

## <a name="diagnostics-functionality-differences-between-azure-sdk-24-and-earlier-and-azure-sdk-25-and-later"></a>Diagnostische functionaliteit verschillen tussen Azure SDK 2.4 en eerder en Azure SDK 2,5 en hoger
Als u een uw project van Azure SDK 2.4 tooAzure SDK 2.5 of hoger upgrade uitvoert, moet u er rekening mee Hallo volgende diagnostische functionaliteit verschillen vergeet.

* **Configuratie-API's zijn afgeschaft** – programmatische configuratie van diagnostische gegevens is beschikbaar in de Azure SDK 2.4 of eerdere versies, maar is afgeschaft in Azure SDK 2.5 en hoger. Als uw configuratie van diagnostische momenteel in de code is gedefinieerd, moet u tooreconfigure die instellingen vanaf het begin in gemigreerde Hallo-project in volgorde van diagnostische gegevens tookeep werken. Hallo diagnostics-configuratiebestand voor de Azure SDK 2.4 is diagnostics.wadcfg en diagnostics.wadcfgx voor Azure SDK 2.5 of hoger.
* **Diagnostische gegevens voor cloud-servicetoepassingen kan alleen worden geconfigureerd op Hallo rolniveau, niet op instantieniveau Hallo.**
* **Telkens wanneer u uw app implementeert, configuratie van diagnostische hello wordt bijgewerkt** : dit kan pariteit problemen veroorzaken als u de configuratie van de diagnostische gegevens in Server Explorer te wijzigen en vervolgens uw app te implementeren.
* **In de Azure SDK 2.5 en hoger crashdumps zijn geconfigureerd in Hallo diagnostics-configuratiebestand niet in de code** – als u geconfigureerd in de code crashdumps hebt, hebt u toomanually overdracht Hallo configuratie uit het configuratiebestand van de code toohello, omdat Hallo crashdumps worden niet overgedragen tijdens Hallo migratie tooAzure SDK 2.6.

## <a name="enable-diagnostics-in-cloud-service-projects-before-deploying-them"></a>Diagnostische gegevens in cloudserviceprojecten inschakelen voordat u ze implementeert
U kunt in Visual Studio toocollect diagnostics-gegevens voor rollen die worden uitgevoerd in Azure, wanneer u Hallo-service in Hallo emulator uitvoert voordat u deze implementeert. Alle wijzigingen toodiagnostics-instellingen in Visual Studio worden opgeslagen in het configuratiebestand voor Hallo diagnostics.wadcfgx. Deze configuratie-instellingen opgeven Hallo opslagaccount waar diagnostische gegevens worden opgeslagen wanneer u uw cloudservice implementeert.

[!INCLUDE [cloud-services-wad-warning](../includes/cloud-services-wad-warning.md)]

### <a name="tooenable-diagnostics-in-visual-studio-before-deployment"></a>tooenable diagnostische gegevens in Visual Studio vóór de implementatie
1. Kies in het snelmenu Hallo voor Hallo-rol die u bent geïnteresseerd, **eigenschappen**, en kies vervolgens Hallo **configuratie** tabblad in Hallo-rol **eigenschappen** venster.
2. In Hallo **Diagnostics** sectie, zorg ervoor dat Hallo **diagnostische gegevens inschakelen** selectievakje is ingeschakeld.
   
    ![Toegang tot de optie voor Hallo diagnostische gegevens inschakelen](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC796660.png)
3. Hallo weglatingsteken (...) knop toospecify hello opslagaccount kiezen waar u Hallo diagnostische gegevens toobe opgeslagen. Hallo-opslagaccount die u kiest worden Hallo-locatie waar diagnostische gegevens worden opgeslagen.
   
    ![Hallo storage account toouse opgeven](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC796661.png)
4. In Hallo **Create Storage Connection String** dialoogvenster vak, opgeven of u wilt dat tooconnect hello Azure-Opslagemulator, een Azure-abonnement met of referenties handmatig worden ingevoerd.
   
    ![Dialoogvenster Storage-account](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC796662.png)
   
   * Als u Hallo Microsoft Azure-Opslagemulator optie kiest, Hallo verbindingsreeks tooUseDevelopmentStorage ingesteld = true.
   * Als u optie Hallo uw abonnement, kunt u hello Azure-abonnement u wilt dat toouse en Hallo accountnaam. U kunt dat uw Azure-abonnementen voor knop toomanage Hallo-Accounts beheren.
   * Als u handmatig ingevoerd Hallo referenties optie kiest, bent u na vragen aan gebruiker tooenter Hallo naam en sleutel Hallo gewenste toouse Azure-account.
5. Kies Hallo **configureren** knop tooview hello **configuratie van diagnostische** in het dialoogvenster. Elk tabblad (met uitzondering van **algemene** en **logboek mappen**) vertegenwoordigt een diagnostische gegevensbron die u kunt verzamelen. Hallo standaardtabblad, **algemene**, biedt u Hallo na opties van diagnostische gegevens voor het verzamelen van gegevens: **alleen fouten**, **alle informatie**, en **aangepaste plan** . Hallo standaardoptie **alleen fouten**, vergt Hallo zo min mogelijk opslag omdat het geen waarschuwingen of tracering berichten over te dragen. Hallo alle informatie optie overdrachten Hallo de meeste gegevens en is, wordt daarom Hallo meest dure optie in termen van opslag.
   
    ![Azure diagnostics- en configuratie inschakelen](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC758144.png)
6. Selecteer voor dit voorbeeld Hallo **aangepaste plan** optie zodat u Hallo gegevens aanpassen kunt verzameld.
7. Hallo **schijfquotum in MB** geeft aan hoeveel ruimte u tooallocate wilt in uw storage-account voor diagnostische gegevens. U kunt de standaardwaarde Hallo wijzigen als u wilt.
8. Op elk tabblad van diagnostische gegevens u wilt dat toocollect, selecteer de **inschakelen overdragen van <log type>**  selectievakje. Als u toocollect toepassingslogboeken wilt, Selecteer bijvoorbeeld Hallo **inschakelen van de overdracht van toepassingslogboeken** selectievakje op Hallo **toepassingslogboeken** tabblad. Geef ook andere informatie die vereist zijn voor elk gegevenstype diagnostische gegevens. Zie de sectie Hallo **gegevensbronnen van diagnostische gegevens configureren** verderop in dit onderwerp voor configuratie-informatie op elk tabblad.
9. Nadat u de verzameling van alle Hallo diagnostische gegevens die u wilt hebt ingeschakeld, kiest u Hallo **OK** knop.
10. Uw Azure-cloud service-project in Visual Studio gewoon uitgevoerd. Als u uw toepassing gebruikt, opgeslagen Hallo logboekgegevens die u hebt ingeschakeld toohello Azure storage-account opgegeven.

## <a name="enable-diagnostics-in-azure-virtual-machines"></a>Diagnostische gegevens in Azure virtuele machines inschakelen
U kunt in Visual Studio toocollect diagnostics-gegevens voor Azure virtual machines.

### <a name="tooenable-diagnostics-in-azure-virtual-machines"></a>tooenable diagnostische gegevens in Azure virtuele machines
1. In **Server Explorer**, kies hello Azure knooppunt en maak verbinding tooyour Azure-abonnement als u nog niet bent verbonden.
2. Vouw Hallo **virtuele Machines** knooppunt. U kunt maken van een nieuwe virtuele machine of Selecteer een die er al.
3. Kies in het snelmenu Hallo voor Hallo virtuele machine die u bent geïnteresseerd, **configureren**. Dit betekent Hallo virtuele machine in het dialoogvenster configuratie.
   
    ![Een virtuele machine van Azure configureren](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC796663.png)
4. Als deze nog niet is geïnstalleerd, moet u Hallo Microsoft Monitoring Agent Diagnostics-extensie toevoegen. Deze extensie kunt u het verzamelen van diagnostische gegevens voor hello Azure virtuele machine. In de lijst van de extensies geïnstalleerd hello, kies Hallo Selecteer een vervolgkeuzelijst met beschikbare extensie menu en kies vervolgens Microsoft Monitoring Agent diagnostische gegevens.
   
    ![Installeren van een virtuele machine van Azure-extensie](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC766024.png)
   
   > [!NOTE]
   > Andere extensies diagnostische gegevens zijn beschikbaar voor uw virtuele machines. Zie voor meer informatie, de Azure VM-extensies en functies.
   > 
   > 
5. Kies Hallo **toevoegen** knop tooadd Hallo-uitbreiding en bekijk de **configuratie van diagnostische** in het dialoogvenster.
6. Kies Hallo **configureren** knop toospecify storage-account en kies vervolgens Hallo **OK** knop.
   
    Elk tabblad (met uitzondering van **algemene** en **logboek mappen**) vertegenwoordigt een diagnostische gegevensbron die u kunt verzamelen.
   
    ![Azure diagnostics- en configuratie inschakelen](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC758144.png)
   
    Hallo standaardtabblad, **algemene**, biedt u Hallo na opties van diagnostische gegevens voor het verzamelen van gegevens: **alleen fouten**, **alle informatie**, en **aangepaste plan** . Hallo standaardoptie **alleen fouten**, vergt Hallo zo min mogelijk opslag omdat het geen waarschuwingen of tracering berichten over te dragen. Hallo **alle informatie** optie overschrijvingen Hallo de meeste gegevens en is daarom meest dure optie Hallo in termen van opslag.
7. Selecteer voor dit voorbeeld Hallo **aangepaste plan** optie zodat u Hallo gegevens aanpassen kunt verzameld.
8. Hallo **schijfquotum in MB** geeft aan hoeveel ruimte u tooallocate wilt in uw storage-account voor diagnostische gegevens. U kunt de standaardwaarde Hallo wijzigen als u wilt.
9. Op elk tabblad van diagnostische gegevens u wilt dat toocollect, selecteer de **inschakelen overdragen van <log type>**  selectievakje.
   
    Als u toocollect toepassingslogboeken wilt, Selecteer bijvoorbeeld Hallo **inschakelen van de overdracht van toepassingslogboeken** selectievakje op Hallo **toepassingslogboeken** tabblad. Geef ook andere informatie die vereist zijn voor elk gegevenstype diagnostische gegevens. Zie de sectie Hallo **gegevensbronnen van diagnostische gegevens configureren** verderop in dit onderwerp voor configuratie-informatie op elk tabblad.
10. Nadat u de verzameling van alle Hallo diagnostische gegevens die u wilt hebt ingeschakeld, kiest u Hallo **OK** knop.
11. Hallo bijgewerkt project opslaan.
    
     U ziet een bericht in Hallo **Microsoft Azure Activity Log** venster dat Hallo van virtuele machine is bijgewerkt.

## <a name="configure-diagnostics-data-sources"></a>Gegevensbronnen van diagnostische gegevens configureren
Nadat u het verzamelen van diagnostische gegevens inschakelen, kunt u precies welke gegevensbronnen die u wilt dat toocollect en welke informatie wordt verzameld. Hallo Hieronder volgt een lijst van tabbladen in Hallo **configuratie van diagnostische** in het dialoogvenster en elke configuratieoptie betekent.

### <a name="application-logs"></a>Toepassingslogboeken
**Toepassingslogboeken** diagnostische informatie die wordt geproduceerd door een webtoepassing bevatten. Als u toocapture toepassingslogboeken wilt, selecteert u Hallo **inschakelen van de overdracht van toepassingslogboeken** selectievakje. U kunt vergroten of verkleinen het aantal minuten op wanneer de toepassingslogboeken Hallo worden overgebracht Hallo tooyour storage-account door het wijzigen van Hallo **Transfer periode (min)** waarde. U kunt ook Hallo en de hoeveelheid gegevens die zijn vastgelegd in logboek Hallo door Hallo logboek-niveau waarde wijzigen. U kunt bijvoorbeeld **uitgebreid** tooget meer informatie of kies **Kritiek** toocapture alleen kritieke fouten. Als u een specifieke diagnostics-provider die u toepassingslogboeken verzendt hebt, kunt u ze vastleggen door toe te voegen van de provider Hallo GUID toohello **Provider GUID** vak.

  ![Toepassingslogboeken](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC758145.png)

  Zie [logboekregistratie van diagnostische gegevens van web-apps in Azure App Service](app-service-web/web-sites-enable-diagnostic-log.md) voor meer informatie over toepassingslogboeken.

### <a name="windows-event-logs"></a>Windows-gebeurtenislogboeken
Als u wilt dat de Windows-gebeurtenislogboeken toocapture, selecteert u Hallo **overdracht van het Windows-gebeurtenislogboeken inschakelen** selectievakje. U kunt vergroten of verkleinen het aantal minuten wanneer Hallo gebeurtenislogboeken worden overgebracht Hallo tooyour storage-account door het wijzigen van Hallo **Transfer periode (min)** waarde. Schakel de selectievakjes Hallo voor Hallo typen gebeurtenissen die u tootrack wilt.

  ![Gebeurtenislogboeken](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC796664.png)

Als u Azure SDK 2.6 of hoger gebruikt en een aangepaste gegevensbron toospecify, voert u deze in Hallo  **<Data source name>**  tekst vak en klik vervolgens op Hallo **toevoegen** knop volgende tooit. Hallo-gegevensbron is toohello diagnostics.cfcfg bestand toegevoegd.

Als u Azure SDK 2.5 gebruikt en een aangepaste gegevensbron toospecify wilt, kunt u deze toevoegen toohello `WindowsEventLog` sectie van Hallo diagnostics.wadcfgx bestand, zoals in het volgende voorbeeld Hallo.

```
<WindowsEventLog scheduledTransferPeriod="PT1M">
   <DataSource name="Application!*" />
   <DataSource name="CustomDataSource!*" />
</WindowsEventLog>
```
### <a name="performance-counters"></a>Prestatiemeteritems
Gegevens van prestatiemeteritems kunt u vinden knelpunten in het systeem en systeem- en -prestaties afstemmen. Zie [maken en prestatiemeteritems voor gebruik in een Azure-toepassing](https://msdn.microsoft.com/library/azure/hh411542.aspx) voor meer informatie. Als u prestatiemeteritems toocapture, selecteert u Hallo **overdracht van prestatiemeteritems inschakelen** selectievakje. U kunt vergroten of verkleinen het aantal minuten wanneer Hallo gebeurtenislogboeken worden overgebracht Hallo tooyour storage-account door het wijzigen van Hallo **Transfer periode (min)** waarde. Schakel de selectievakjes Hallo voor hello prestatiemeteritems die u tootrack wilt.

  ![Prestatiemeteritems](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC758147.png)

Voer tootrack een prestatiemeteritem die niet is vermeld, met behulp van deze Hallo voorgestelde syntaxis en kies vervolgens Hallo **toevoegen** knop. Hallo-besturingssysteem op Hallo virtuele machine bepaalt welke prestatiemeteritems die u kunt volgen. Zie voor meer informatie over de syntaxis [geven een itempad](https://msdn.microsoft.com/library/windows/desktop/aa373193.aspx).

### <a name="infrastructure-logs"></a>Logboeken van de infrastructuur
Als u Logboeken toocapture infrastructuur die informatie over Hallo diagnostische Azure-infrastructuur, Hallo RemoteAccess-module en Hallo RemoteForwarder-module bevatten, selecteert u Hallo **inschakelen van de overdracht van infrastructuur logboeken**selectievakje. U kunt vergroten of verkleinen het aantal minuten wanneer Hallo logboeken worden overgebracht Hallo tooyour storage-account door Hallo Transfer periode (min) waarde te wijzigen.

  ![Diagnostische gegevens infrastructuur Logboeken](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC758148.png)

  Zie [Logboekregistratiegegevens verzamelen met behulp van Azure Diagnostics](https://msdn.microsoft.com/library/azure/gg433048.aspx) voor meer informatie.

### <a name="log-directories"></a>Logboek mappen
Als u mappen toocapture logboek dat gegevens verzameld van logboek-mappen voor aanvragen van Internet Information Services (IIS) bevatten, mislukte aanvragen of mappen die u kiest, schakelt Hallo **inschakelen van de overdracht van logboek mappen**selectievakje. U kunt vergroten of verkleinen het aantal minuten wanneer Hallo logboeken worden overgebracht Hallo tooyour storage-account door het wijzigen van Hallo **Transfer periode (min)** waarde.

Kunt u de vakken Hallo Hallo logboeken die u wilt dat toocollect, zoals **IIS-logboeken** en **kan aanvragen** Logboeken. Standaard opslag containernamen worden opgegeven, maar u kunt Hallo namen wijzigen als u wilt.

U kunt ook de logboeken van de map vastleggen. NET Hallo pad opgeeft in Hallo **logboek van Directory Absolute** sectie en kies vervolgens Hallo **map toevoegen** knop. Hallo Logboeken wordt vastgelegd toohello containers opgegeven.

  ![Logboek mappen](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC796665.png)

### <a name="etw-logs"></a>ETW-Logboeken
Als u [Event Tracing for Windows](https://msdn.microsoft.com/library/windows/desktop/bb968803\(v=vs.85\).aspx) (ETW) en toocapture ETW Logboeken, selecteer hello wilt **overdracht van ETW-Logboeken inschakelen** selectievakje. U kunt vergroten of verkleinen het aantal minuten wanneer Hallo logboeken worden overgebracht Hallo tooyour storage-account door het wijzigen van Hallo **Transfer periode (min)** waarde.

Hallo-gebeurtenissen worden vastgelegd van bronnen van gebeurtenissen en het gebeurtenismanifesten die u opgeeft. toospecify een gebeurtenisbron, voer een naam in Hallo **gebeurtenisbronnen** sectie en kies vervolgens Hallo **gebeurtenisbron toevoegen** knop. Op deze manier kunt u een manifest van de gebeurtenis opgeven in Hallo **gebeurtenis manifesten** sectie en kies vervolgens Hallo **toevoegen gebeurtenis Manifest** knop.

  ![ETW-Logboeken](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC766025.png)

  Hallo ETW-framework wordt in ASP.NET ondersteund door de klassen in Hallo [System.Diagnostics.aspx] (naamruimte https://msdn.microsoft.com/library/system.diagnostics (v=vs.110). Hallo Microsoft.WindowsAzure.Diagnostics naamruimte overneemt en breidt standaard [System.Diagnostics.aspx] (klassen https://msdn.microsoft.com/library/system.diagnostics (v=vs.110), schakelt Hallo gebruik van () [System.Diagnostics.aspx] https://msdn.Microsoft.com/library/System.Diagnostics (v=vs.110) als een framework voor logboekregistratie in hello Azure-omgeving. Zie voor meer informatie [besturingselement nemen van logboekregistratie en tracering in Microsoft Azure](https://msdn.microsoft.com/magazine/ff714589.aspx) en [diagnostische gegevens inschakelen in Azure Cloud Services en virtuele Machines](cloud-services/cloud-services-dotnet-diagnostics.md).

### <a name="crash-dumps"></a>Crashdumps
Als u toocapture informatie wilt over wanneer een rolinstantie is vastgelopen, selecteert u Hallo **inschakelen van de overdracht van Crash dumpen** selectievakje. (Omdat ASP.NET de meeste uitzonderingen verwerkt, dit is doorgaans alleen nuttig voor werkrollen.) U kunt vergroten of verkleinen Hallo percentage van de opslag ruimte gewijd toohello crashdumps door het wijzigen van Hallo **Directory quotum (%)** waarde. Hallo storage-container waar Hallo crashdumps worden opgeslagen en u kunt aangeven of u wilt dat toocapture kunt u een **volledige** of **Mini** dump.

Hallo-processen die momenteel worden bijgehouden, worden weergegeven. Schakel de selectievakjes Hallo voor Hallo processen die u toocapture wilt. tooadd een ander proces toohello lijst, Voer Hallo procesnaam en kies vervolgens Hallo **proces toevoegen** knop.

  ![Crashdumps](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC766026.png)

  Zie [besturingselement nemen van logboekregistratie en tracering in Microsoft Azure](https://msdn.microsoft.com/magazine/ff714589.aspx) en [Microsoft Azure Diagnostics deel 4: aangepaste logboekregistratie onderdelen en Azure Diagnostics 1.3 wijzigingen](http://justazure.com/microsoft-azure-diagnostics-part-4-custom-logging-components-azure-diagnostics-1-3-changes/) voor meer informatie.

## <a name="view-hello-diagnostics-data"></a>Hallo diagnostics-gegevens weergeven
Als u Hallo diagnostics-gegevens voor een cloudservice of een virtuele machine hebt verzameld, kunt u het kunt weergeven.

### <a name="tooview-cloud-service-diagnostics-data"></a>tooview cloud service diagnostics-gegevens
1. Implementeer uw cloudservice als normaal en vervolgens uit te voeren.
2. U kunt Hallo diagnostics-gegevens weergeven in een rapport met Visual Studio gegenereerd of tabellen in uw opslagaccount. tooview hello gegevens in een rapport openen **Cloud Explorer** of **Server Explorer**, snelmenu Hallo van knooppunt voor Hallo-rol die u interesseert Hallo openen en kies vervolgens **diagnostische gegevens weergeven** .
   
    ![De Diagnostics-gegevens weergeven](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC748912.png)
   
    Een rapport met de beschikbare gegevens hello wordt weergegeven.
   
    ![Rapport van de Microsoft Azure Diagnostics in Visual Studio](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC796666.png)
   
    Als de meest recente gegevens Hallo niet wordt weergegeven, kunt u toowait voor Hallo overdracht periode tooelapse wellicht.
   
    Kies Hallo **vernieuwen** tooimmediately update Hallo gegevens koppelen of kies een interval in Hallo **automatisch vernieuwen** dropdown vak toohave Hallo lijstgegevens automatisch bijgewerkt. Foutgegevens tooexport hello, kies Hallo **tooCSV exporteren** knop toocreate een CSV-bestand u in een werkblad openen kunt.
   
    In **Cloud Explorer** of **Server Explorer**, open Hallo storage-account die is gekoppeld aan het Hallo-implementatie.
3. Open Hallo diagnostics tabellen in de viewer voor Hallo-tabel en controleer Hallo-gegevens die u hebt verzameld. U kunt een blob-container openen voor IIS-logboeken en aangepaste logboeken. U vindt aan de hand van de volgende tabel Hallo Hallo tabel of blob-container die Hallo gegevens bevat die u bent geïnteresseerd. Bovendien toohello gegevens voor die logboekbestand, Hallo tabelvermeldingen EventTickCount, DeploymentId, rol bevatten en RoleInstance toohelp u identificeren welke virtuele machine en de rol Hallo gegevens gegenereerd en wanneer. 
   
   | Diagnostische gegevens | Beschrijving | Locatie |
   | --- | --- | --- |
   | Toepassingslogboeken |De logboeken die uw code wordt gegenereerd door het aanroepen van methoden van Hallo System.Diagnostics.Trace klasse. |WADLogsTable |
   | Gebeurtenislogboeken |Deze gegevens is van het Windows-gebeurtenislogboeken Hallo op Hallo virtuele machines. Slaat Windows de informatie in deze logboeken, maar toepassingen en services ook gebruik van tooreport fouten of logboekgegevens. |WADWindowsEventLogsTable |
   | Prestatiemeteritems |U kunt gegevens verzamelen op elk prestatiemeteritem dat beschikbaar is op Hallo virtuele machine. Hallo-besturingssysteem biedt prestatiemeteritems, waaronder veel statistische gegevens zoals geheugen en de processor tijd. |WADPerformanceCountersTable |
   | Logboeken van de infrastructuur |Deze logboeken worden gegenereerd vanuit Hallo diagnostics infrastructuur zelf. |WADDiagnosticInfrastructureLogsTable |
   | IIS-logboeken |Deze logboeken vastleggen webaanvragen. Als uw cloudservice een aanzienlijke hoeveelheid verkeer ontvangt, zijn deze logboeken behoorlijk langdurige, dus u moet verzamelen en opslaan van deze gegevens alleen wanneer u deze nodig. |U vindt is mislukt-aanvraag wordt geregistreerd in de blob-container Hallo onder af iis failedreqlogs onder een pad op voor deze implementatie, rol en exemplaar. U vindt de volledige Logboeken onder af-iis-logboekbestanden. Vermeldingen voor elk bestand zijn aangebracht in Hallo WADDirectories tabel. |
   | Crashdumps |Deze informatie biedt binaire installatiekopieën van uw cloudservice-proces (meestal een werkrol). |af-crush-dumpbestanden voor blob-container |
   | Aangepaste logboekbestanden |Logboeken van de gegevens die u vooraf gedefinieerd. |U kunt opgeven in code Hallo locatie van aangepaste logboekbestanden in uw opslagaccount. U kunt bijvoorbeeld een aangepaste blob-container opgeven. |
4. Als de gegevens van een willekeurig type worden afgekapt, kunt u proberen toenemende Hallo buffer voor die gegevenstype of korten Hallo interval tussen de overdracht van gegevens van Hallo virtuele machine tooyour storage-account.
5. (optioneel) Opschonen van gegevens uit Hallo storage account van tijd tot tijd tooreduce algehele kosten voor opslag.
6. Wanneer u een volledige implementatie doet, Hallo diagnostics.cscfg-bestand (.wadcfgx voor Azure SDK 2.5) wordt bijgewerkt in Azure en uw cloudservice opneemt in een willekeurige configuratie wijzigingen tooyour diagnostische gegevens. Als u, in plaats daarvan een bestaande implementatie hebt bijgewerkt, worden Hallo cscfg-bestand niet bijgewerkt in Azure. U kunt nog steeds diagnostische instellingen echter wijzigen door de stappen in de volgende sectie Hallo Hallo. Zie voor meer informatie over het uitvoeren van een volledige implementatie en het bijwerken van een bestaande implementatie [Publish Azure Application Wizard](vs-azure-tools-publish-azure-application-wizard.md).

### <a name="tooview-virtual-machine-diagnostics-data"></a>Diagnostische gegevens van tooview virtuele machines
1. Kies in het snelmenu Hallo voor Hallo virtuele machine, **weergave Diagnostics-gegevens**.
   
    ![Diagnostische gegevens weergeven in de virtuele machine van Azure](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC766027.png)
   
    Hiermee opent u Hallo **Diagnostics samenvatting** venster.
   
    ![Virtuele machine van Azure diagnostics samenvatting](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC796667.png)  
   
    Als de meest recente gegevens Hallo niet wordt weergegeven, kunt u toowait voor Hallo overdracht periode tooelapse wellicht.
   
    Kies Hallo **vernieuwen** tooimmediately update Hallo gegevens koppelen of kies een interval in Hallo **automatisch vernieuwen** dropdown vak toohave Hallo lijstgegevens automatisch bijgewerkt. Foutgegevens tooexport hello, kies Hallo **tooCSV exporteren** knop toocreate een CSV-bestand u in een werkblad openen kunt.

## <a name="configure-cloud-service-diagnostics-after-deployment"></a>Cloud service diagnostische gegevens configureren na implementatie
Als u een probleem met een cloudservice die al wordt uitgevoerd onderzoeken, kunt u toocollect gegevens die u hebt opgegeven voordat u oorspronkelijk geïmplementeerde Hallo-rol. In dit geval kunt u starten toocollect die gegevens met behulp van Hallo-instellingen in Server Explorer. U kunt diagnostische gegevens voor één exemplaar of alle exemplaren van Hallo configureren in een rol, afhankelijk van of u in het dialoogvenster Hallo-configuratie van diagnostische in het snelmenu Hallo Hallo-exemplaar of Hallo-rol opent. Als u Hallo rol knooppunt configureert, eventuele wijzigingen tooall exemplaren gelden. Als u Hallo exemplaar knooppunt configureert, eventuele wijzigingen toothat exemplaar alleen gelden.

### <a name="tooconfigure-diagnostics-for-a-running-cloud-service"></a>tooconfigure diagnostische gegevens voor een actieve cloudservice
1. Vouw in Server Explorer Hallo **Cloudservices** knooppunt, en vouw vervolgens knooppunten toolocate Hallo rol of -exemplaar dat u tooinvestigate of beide wilt.
   
    ![Configuratie van diagnostische gegevens](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC748913.png)
2. Kies in het snelmenu Hallo voor een knooppunt van het exemplaar of een knooppunt van de rol, **Update diagnostische instellingen**, en kies vervolgens Hallo diagnostische instellingen die u toocollect wilt.
   
    Zie voor meer informatie over de configuratie-instellingen Hallo **gegevensbronnen van diagnostische gegevens configureren** in dit onderwerp. Zie voor meer informatie over hoe tooview diagnostics-gegevens Hallo **Hallo diagnostische gegevens bekijken** in dit onderwerp.
   
    Als u het verzamelen van gegevens in wijzigt **Server Explorer**, deze wijzigingen blijven van kracht totdat u de cloudservice volledig opnieuw implementeren. Als u Hallo standaard publicatie-instellingen, Hallo wijzigingen zijn niet overschreven, aangezien Hallo standaard publiceren instelling tooupdate Hallo bestaande implementatie, in plaats van komen een volledig opnieuw implementeren gaande is. toomake ervoor Hallo instellingen wissen tijdens de implementatie gaat toohello **geavanceerde instellingen** tabblad in de wizard Publiceren Hallo en wissen Hallo **implementatie-update** selectievakje. Wanneer u opnieuw met dit selectievakje is uitgeschakeld implementeert, terugzetten Hallo instellingen toothose in Hallo .wadcfgx (of .wadcfg) bestand als set via Hallo Eigenschappeneditor voor Hallo rol. Als u uw implementatie hebt bijgewerkt, houdt Azure Hallo oude instellingen.

## <a name="troubleshoot-azure-cloud-service-issues"></a>Problemen met Azure cloud service
Als er problemen met uw cloudserviceprojecten, zoals een rol die blijft in 'bezet' status steken opgehaald herhaaldelijk wordt gerecycled of er een interne serverfout, er zijn hulpprogramma's en technieken die u kunt gebruiken toodiagnose en los deze problemen. Zie voor specifieke voorbeelden van algemene problemen en oplossingen, evenals een overzicht van het Hallo-concepten en hulpprogramma's toodiagnose gebruikt en corrigeer deze fouten, [Azure PaaS Compute Diagnostics-gegevens](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx).

## <a name="q--a"></a>Vragen en antwoorden
**Wat Hallo buffergrootte is en hoe lang deze moet?**

Op elk exemplaar van de virtuele machine beperken quota's hoeveel diagnostische gegevens kan worden opgeslagen op het lokale bestandssysteem Hallo. Bovendien het opgeven van een buffergrootte voor elk type diagnostische gegevens die beschikbaar is. Deze buffergrootte fungeert als een quotum voor dit type gegevens. Hallo-onder in het dialoogvenster van Hallo inschakelt, kunt u bepalen Hallo algehele quota en Hallo en de hoeveelheid geheugen die overblijft. Als u groter buffers of meerdere typen gegevens opgeeft, moet u benadert Hallo algehele quotum. U kunt wijzigen Hallo algehele quotum doordat Hallo diagnostics.wadcfg/.wadcfgx-configuratiebestand. Hallo diagnostische gegevens worden opgeslagen op Hallo hetzelfde bestandssysteem als uw toepassingsgegevens, zodat als uw toepassing gebruikmaakt van een groot aantal schijfruimte, u Hallo mag niet meer algemene diagnostics quotum.

**Wat is er Hallo overdracht periode en hoe lang deze moet?**

Hallo overdracht periode is Hallo hoeveelheid tijd die is verstreken tussen gegevens worden vastgelegd. Na elke periode overdracht gegevens verplaatst van het lokale bestandssysteem Hallo op een virtuele machine tootables in uw opslagaccount. Hallo hoeveelheid gegevens die worden verzameld overschrijdt Hallo quotum voor Hallo einde van een overdracht-periode, oudere gegevens verwijderd. U kunt toodecrease Hallo overdracht periode als u gegevens verliest omdat uw gegevens groter is dan de buffergrootte Hallo of Hallo algehele quotum.

**Welke tijdzone zijn Hallo tijdstempels in?**

Hallo tijdstempels zijn in Hallo lokale tijdzone van Hallo datacenter dat als host fungeert voor uw cloudservice. Hallo worden volgende drie timestamp-kolommen in Hallo logboek tabellen gebruikt.

* **PreciseTimeStamp** Hallo ETW tijdstempel van Hallo-gebeurtenis. Dat wil zeggen, wordt Hallo tijd Hallo gebeurtenis geregistreerd in Hallo-client.
* **TIJDSTEMPEL** PreciseTimeStamp naar beneden afgerond toohello uploaden frequentie grens. Dus als uw uploadfrequentie 5 minuten en Hallo gebeurtenis tijd 00:17:12 is, TIMESTAMP worden 00:15:00.
* **Tijdstempel** Hallo tijdstempel op welke Hallo entiteit in hello Azure-tabel is gemaakt.

**Hoe beheer ik kosten bij het verzamelen van diagnostische gegevens?**

Hallo standaardinstellingen (**Meld niveau** instellen te**fout** en **overdracht periode** instellen te**1 minuut**) zijn ontworpen toominimize kosten. De compute-kosten wordt verhoogd als u meer diagnostische gegevens verzamelen of verklein Hallo overdracht periode. Niet meer gegevens dan u nodig hebt en niet de gegevensverzameling toodisable vergeet wanneer u niet langer verzamelen. U kunt altijd het opnieuw inschakelen, zelfs tijdens runtime, zoals wordt weergegeven in de vorige sectie Hallo.

**Hoe ik Logboeken is mislukt-aanvragen verzamelen uit IIS?**

Standaard verzamelen niet IIS logboeken is mislukt-aanvragen. U kunt IIS toocollect ze als u het bestand web.config voor de Webrol Hallo configureren.

**Ik ben traceringsinformatie niet ophalen uit RoleEntryPoint methoden zoals OnStart. Wat is er aan de hand?**

Hallo-methoden van RoleEntryPoint worden genoemd in de context Hallo van WAIISHost.exe, niet in IIS. Daarom Hallo configuratiegegevens in web.config die normaal gesproken schakelt tracering niet van toepassing. tooresolve dit probleem op door een .config-bestand tooyour-webproject rol toevoegen en Hallo bestand toomatch Hallo uitvoer assembly Hallo RoleEntryPoint code met de naam. Hallo-naam van Hallo .config-bestand wordt in het Hallo-webrolproject voor standaard WAIISHost.exe.config. Voeg vervolgens Hallo volgende toothis regels toe:

```
<system.diagnostics>
  <trace>
      <listeners>
          <add name “AzureDiagnostics” type=”Microsoft.WindowsAzure.Diagnostics.DiagnosticMonitorTraceListener”>
              <filter type=”” />
          </add>
      </listeners>
  </trace>
</system.diagnostics>
```

Nu in Hallo **eigenschappen** venster, set Hallo **tooOutput Directory kopiëren** eigenschap te**altijd kopiëren**.

## <a name="next-steps"></a>Volgende stappen
toolearn meer informatie over diagnostische gegevens van logboekregistratie in Azure, Zie [diagnostische gegevens inschakelen in Azure Cloud Services en virtuele Machines](cloud-services/cloud-services-dotnet-diagnostics.md) en [logboekregistratie van diagnostische gegevens van web-apps in Azure App Service](app-service-web/web-sites-enable-diagnostic-log.md).


---
title: Diagnostische gegevens configureren voor Azure-Cloudservices en virtuele Machines | Microsoft Docs
description: Beschrijft hoe diagnostische gegevens voor het opsporen van Azure cloude services en virtuele machines (VM's) in Visual Studio configureren.
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
ms.openlocfilehash: 2516c0eb8ce470577731db9b844d5b9038465477
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="configuring-diagnostics-for-azure-cloud-services-and-virtual-machines"></a>Configuratie van diagnostische gegevens voor Azure-Cloudservices en virtuele Machines
Wanneer u problemen met een Azure-cloudservice of virtuele machine van Azure, kunt u gemakkelijker Azure diagnostics configureren met behulp van Visual Studio. Azure diagnostics vastgelegd system en logboekregistratie-gegevens op de virtuele machines en de virtuele machine-exemplaren die uitvoeren van uw cloudservice en die gegevens overgebracht naar een opslagaccount van uw keuze. Zie [logboekregistratie van diagnostische gegevens van web-apps in Azure App Service](app-service-web/web-sites-enable-diagnostic-log.md) voor meer informatie over diagnostische gegevens van logboekregistratie in Azure.

Dit onderwerp leest u hoe inschakelen en configureren van Azure diagnostics in Visual Studio, zowel voor en na de implementatie, evenals in virtuele machines in Azure. Deze ook ziet u hoe u selecteert de soorten informatie voor het verzamelen van diagnostische gegevens en het weergeven van de informatie verzamelde.

U kunt Azure Diagnostics configureren op de volgende manieren:

* Kunt u configuratie-instellingen voor diagnostische gegevens via de **configuratie van diagnostische** dialoogvenster in Visual Studio. De instellingen worden opgeslagen in een bestand met de naam diagnostics.wadcfgx (diagnostics.wadcfg in Azure SDK 2.4 of eerder). U kunt ook kunt u het configuratiebestand rechtstreeks wijzigen. Als u het bestand handmatig bijwerken, wijzigingen in de configuratie te laten treden de volgende implementatie van de cloud service naar Azure of de service wordt uitgevoerd in de emulator.
* Gebruik **Cloud Explorer** of **Server Explorer** in Visual Studio om de instellingen voor diagnostische gegevens voor een actieve cloudservice of virtuele machine wijzigen.

## <a name="azure-26-diagnostics-changes"></a>2.6 Azure diagnostics wijzigingen
Azure SDK 2.6-projecten in Visual Studio, zijn de volgende wijzigingen aangebracht. (Deze wijzigingen ook van toepassing op latere versies van Azure SDK.)

* De lokale emulator ondersteunt nu de diagnostische gegevens. Dit betekent dat u kunt het verzamelen van diagnostische gegevens en zorg ervoor dat uw toepassing wordt gemaakt door de juiste traceringen tijdens het ontwikkelen en testen in Visual Studio. De verbindingsreeks `UseDevelopmentStorage=true` kunt verzamelen van diagnostische gegevens, terwijl u uw cloudserviceproject in Visual Studio uitvoert met behulp van de Azure-opslagemulator. Alle diagnostische gegevens worden verzameld in het opslagaccount (ontwikkeling opslag).
* De verbindingsreeks van diagnostische gegevens storage-account (Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString) wordt nog een keer opgeslagen in het service-configuratiebestand (.cscfg). In de Azure SDK 2.5 is de opslagaccount voor diagnostische gegevens opgegeven in het bestand diagnostics.wadcfgx.

Er zijn enkele belangrijke verschillen tussen hoe de verbindingsreeks in de Azure SDK 2.4 en eerder heeft gewerkt, en hoe het werkt in de Azure SDK 2.6 en hoger.

* In Azure SDK 2.4 en eerdere versies, is de verbindingsreeks gebruikt als een runtime door de invoegtoepassing diagnostische gegevens ophalen van de accountgegevens voor de opslag voor het overdragen van diagnostische logboeken.
* In Azure SDK 2.6 en hoger, wordt de verbindingsreeks van de diagnostische gegevens door Visual Studio gebruikt voor het configureren van de extensie voor diagnostische gegevens met de juiste opslag gegevens tijdens de publicatie. De verbindingsreeks kunt u verschillende opslagaccounts voor verschillende configuraties die door Visual Studio wordt gebruikt bij het publiceren van definiëren. Omdat de diagnostics-invoegtoepassing (na de Azure SDK 2,5) niet langer beschikbaar is, kan niet het cscfg-bestand zelf echter de extensie voor diagnostische gegevens inschakelen. U moet de extensie afzonderlijk via hulpprogramma's zoals Visual Studio of PowerShell inschakelen.
* De uitvoer van het pakket van Visual Studio bevat ook de openbare configuratie-XML voor de extensie voor diagnostische gegevens voor elke rol voor het vereenvoudigen van de extensie voor diagnostische gegevens configureren met PowerShell. De verbindingsreeks diagnostics Visual Studio gebruikt voor het vullen van de opslag-accountgegevens die aanwezig zijn in de openbare configuratie. De openbare configuratiebestanden worden gemaakt in de map extensies en volg het patroon PaaSDiagnostics. &lt;RoleName >. PubConfig.xml. Alle implementaties op basis van PowerShell kunnen dit patroon gebruiken voor elke configuratie worden toegewezen aan een rol.
* De verbindingsreeks in het .cscfg-bestand wordt ook gebruikt door de [Azure-portal](http://go.microsoft.com/fwlink/p/?LinkID=525040) toegang krijgen tot de diagnostics-gegevens, zodat het kan worden weergegeven de **bewaking** tabblad. De verbindingsreeks is nodig voor de service configureren voor het uitgebreide bewakingsgegevens weergeven in de portal.

## <a name="migrating-projects-to-azure-sdk-26-and-later"></a>Migreren projecten op Azure SDK 2.6 en hoger
Wanneer u migreert van Azure SDK 2.5 naar Azure SDK 2.6 of hoger, als u een opslagaccount voor diagnostische gegevens opgegeven in het bestand .wadcfgx had, vervolgens blijft er. Als u wilt profiteren van de flexibiliteit van het gebruik van verschillende storage-accounts voor opslagconfiguraties verschillende, hebt u de verbindingsreeks handmatig toevoegen aan uw project. Als u een project waarnaar u migreert van Azure SDK 2.4 of eerder in Azure SDK 2.6, blijven de verbindingsreeksen van diagnostische gegevens behouden. Let echter de wijzigingen in hoe verbindingsreeksen worden behandeld in de Azure SDK 2.6 zoals opgegeven in de vorige sectie.

### <a name="how-visual-studio-determines-the-diagnostics-storage-account"></a>Hoe de opslagaccount voor diagnostische gegevens in Visual Studio wordt bepaald
* Als een verbindingsreeks diagnostische gegevens in het .cscfg-bestand is opgegeven, wordt het in Visual Studio gebruikt voor het configureren van de extensie voor diagnostische gegevens bij het publiceren en bij het genereren van de openbare configuratie-xml-bestanden tijdens pakketten.
* Als geen diagnostische gegevens verbindingsreeks is opgegeven in het .cscfg-bestand, klikt u vervolgens terugvalt Visual Studio op het storage-account opgegeven in het bestand .wadcfgx met de extensie voor diagnostische gegevens bij het publiceren van en het genereren van de openbare configuratie-xml-bestanden configureren Wanneer verpakken.
* De verbindingsreeks voor diagnostische gegevens in het .cscfg-bestand heeft voorrang op de storage-account in het bestand .wadcfgx. Als een verbindingsreeks diagnostics is opgegeven in het .cscfg-bestand, Visual Studio die wordt gebruikt en het opslagaccount in .wadcfgx worden genegeerd.

### <a name="what-does-the-update-development-storage-connection-strings-checkbox-do"></a>Wat doet de 'Update ontwikkeling storage-verbindingsreeksen..." selectievakje doen?
Het selectievakje voor **bijwerken van ontwikkeling storage-verbindingsreeksen voor diagnostische gegevens en opslaan in cache met Microsoft Azure storage-accountreferenties bij het publiceren van Microsoft Azure** biedt u een handige manier om bij te werken van alle ontwikkeling opslagaccountverbindingsreeksen met de Azure storage-account dat is opgegeven tijdens de publicatie.

Stel bijvoorbeeld dat u dit selectievakje inschakelt en de verbindingsreeks voor diagnostische gegevens `UseDevelopmentStorage=true`. Wanneer u het project naar Azure publiceert, wordt Visual Studio de verbindingsreeks van diagnostische gegevens automatisch bijgewerkt met de storage-account dat u hebt opgegeven in de wizard publiceren. Echter, als een echte storage-account is opgegeven als de verbindingsreeks van diagnostische gegevens, klikt u vervolgens dat account wordt gebruikt in plaats daarvan.

## <a name="diagnostics-functionality-differences-between-azure-sdk-24-and-earlier-and-azure-sdk-25-and-later"></a>Diagnostische functionaliteit verschillen tussen Azure SDK 2.4 en eerder en Azure SDK 2,5 en hoger
Als u een uw project van Azure SDK 2.4 naar Azure SDK 2.5 of hoger upgrade uitvoert, moet u vergeet de volgende verschillen van de diagnostics-functionaliteit.

* **Configuratie-API's zijn afgeschaft** – programmatische configuratie van diagnostische gegevens is beschikbaar in de Azure SDK 2.4 of eerdere versies, maar is afgeschaft in Azure SDK 2.5 en hoger. Als uw configuratie van diagnostische momenteel in de code is gedefinieerd, moet u die instellingen vanaf het begin in het gemigreerde project in de volgorde voor diagnostische gegevens blijven werken opnieuw configureren. Het configuratiebestand van de diagnostische gegevens voor Azure SDK 2.4 is diagnostics.wadcfg en diagnostics.wadcfgx voor Azure SDK 2.5 of hoger.
* **Diagnostische gegevens voor cloud-servicetoepassingen kan alleen worden geconfigureerd op het niveau van de functie niet op het niveau van het exemplaar.**
* **Telkens wanneer u uw app implementeert, wordt de configuratie van diagnostische bijgewerkt** : dit kan pariteit problemen veroorzaken als u de configuratie van de diagnostische gegevens in Server Explorer te wijzigen en vervolgens uw app te implementeren.
* **In de Azure SDK 2.5 en hoger crashdumps zijn geconfigureerd in het configuratiebestand van de diagnostische gegevens niet in de code** – als u geconfigureerd in de code crashdumps hebt, hebt u de configuratie van code handmatig te zetten naar het configuratiebestand, omdat de crashdumps worden niet tijdens de migratie naar Azure SDK 2.6 overgedragen.

## <a name="enable-diagnostics-in-cloud-service-projects-before-deploying-them"></a>Diagnostische gegevens in cloudserviceprojecten inschakelen voordat u ze implementeert
In Visual Studio kunt u kiezen voor het verzamelen van diagnostische gegevens voor rollen die worden uitgevoerd in Azure, wanneer u de service in de emulator uitvoert voordat u deze implementeert. Alle wijzigingen in de diagnostische instellingen in Visual Studio zijn opgeslagen in het configuratiebestand diagnostics.wadcfgx. Deze configuratie-instellingen opgeven voor het opslagaccount waar diagnostische gegevens worden opgeslagen wanneer u uw cloudservice implementeert.

[!INCLUDE [cloud-services-wad-warning](../includes/cloud-services-wad-warning.md)]

### <a name="to-enable-diagnostics-in-visual-studio-before-deployment"></a>Diagnostische gegevens in Visual Studio vóór de implementatie inschakelen
1. Kies in het snelmenu voor de rol die u interesseert **eigenschappen**, en kies vervolgens de **configuratie** tabblad in de rol **eigenschappen** venster.
2. In de **Diagnostics** sectie, zorg ervoor dat de **diagnostische gegevens inschakelen** selectievakje is ingeschakeld.
   
    ![Toegang tot de optie diagnostische gegevens inschakelen](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC796660.png)
3. Kies de knop met het weglatingsteken (...) om op te geven van het opslagaccount waar u de diagnostische gegevens worden opgeslagen. Het opslagaccount dat u kiest, worden de locatie waar diagnostische gegevens worden opgeslagen.
   
    ![Geef het storage-account gebruiken](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC796661.png)
4. In de **Create Storage Connection String** dialoogvenster vak, opgeven of u wilt verbinden met de Azure-Opslagemulator een Azure-abonnement of referenties handmatig worden ingevoerd.
   
    ![Dialoogvenster Storage-account](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC796662.png)
   
   * Als u ervoor kiest de Microsoft Azure-Opslagemulator optie, de verbindingsreeks is ingesteld op UseDevelopmentStorage = true.
   * Als u ervoor kiest de uw abonnement, kunt u de Azure-abonnement u wilt gebruiken en de accountnaam. U kunt de knop Accounts beheren voor het beheren van uw Azure-abonnementen.
   * Als u de optie handmatig ingevoerde referenties kiest, wordt u gevraagd de naam en sleutel van het Azure-account dat u wilt gebruiken in te voeren.
5. Kies de **configureren** knop om weer te geven de **configuratie van diagnostische** in het dialoogvenster. Elk tabblad (met uitzondering van **algemene** en **logboek mappen**) vertegenwoordigt een diagnostische gegevensbron die u kunt verzamelen. Het standaardtabblad **algemene**, biedt de volgende opties van diagnostische gegevens verzameling: **alleen fouten**, **alle informatie**, en **aangepaste plan**. De standaardoptie **alleen fouten**, zo min mogelijk opslag vereist omdat deze geen waarschuwingen of tracering berichten over te dragen. De optie om alle brengt de meeste informatie en is daarom de optie meest kostbaar in termen van opslag.
   
    ![Azure diagnostics- en configuratie inschakelen](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC758144.png)
6. Selecteer voor dit voorbeeld wordt de **aangepaste plan** optie zodat u de gegevens kunt worden verzameld.
7. De **schijfquotum in MB** vak geeft aan hoeveel ruimte u in uw opslagaccount voor diagnostische gegevens wilt toewijzen. U kunt de standaardwaarde als u wilt wijzigen.
8. Op elk tabblad van diagnostische gegevens u wilt verzamelen, selecteer de **inschakelen overdragen van <log type>**  selectievakje. Bijvoorbeeld, als u wenst te verzamelen van toepassingslogboeken, selecteert u de **inschakelen van de overdracht van toepassingslogboeken** selectievakje op het **toepassingslogboeken** tabblad. Geef ook andere informatie die vereist zijn voor elk gegevenstype diagnostische gegevens. Zie de sectie **gegevensbronnen van diagnostische gegevens configureren** verderop in dit onderwerp voor configuratie-informatie op elk tabblad.
9. Nadat u de verzameling van alle diagnostics-gegevens die u hebt ingeschakeld, kiest u de **OK** knop.
10. Uw Azure-cloud service-project in Visual Studio gewoon uitgevoerd. Terwijl u uw toepassing gebruikt, wordt de informatie die u hebt ingeschakeld in het foutenlogboek wordt opgeslagen in de Azure storage-account dat u hebt opgegeven.

## <a name="enable-diagnostics-in-azure-virtual-machines"></a>Diagnostische gegevens in Azure virtuele machines inschakelen
In Visual Studio kunt u voor het verzamelen van diagnostische gegevens voor Azure virtual machines.

### <a name="to-enable-diagnostics-in-azure-virtual-machines"></a>Diagnostische gegevens in Azure virtuele machines inschakelen
1. In **Server Explorer**, kies het Azure-knooppunt en maak verbinding met uw Azure-abonnement als u nog niet bent verbonden.
2. Vouw de **virtuele Machines** knooppunt. U kunt maken van een nieuwe virtuele machine of Selecteer een die er al.
3. Kies in het snelmenu voor de virtuele machine die u interesseert **configureren**. Geeft het dialoogvenster configuratie van virtuele machine.
   
    ![Een virtuele machine van Azure configureren](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC796663.png)
4. Als deze nog niet is geïnstalleerd, moet u de Microsoft Monitoring Agent Diagnostics-extensie toevoegen. Deze extensie kunt u het verzamelen van diagnostische gegevens voor de virtuele machine van Azure. In de lijst extensies geïnstalleerd kies het selecteren van een vervolgkeuzelijst met beschikbare extensie en kies vervolgens Microsoft Monitoring Agent diagnostische gegevens.
   
    ![Installeren van een virtuele machine van Azure-extensie](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC766024.png)
   
   > [!NOTE]
   > Andere extensies diagnostische gegevens zijn beschikbaar voor uw virtuele machines. Zie voor meer informatie, de Azure VM-extensies en functies.
   > 
   > 
5. Kies de **toevoegen** om toe te voegen van de extensie en bekijk de **configuratie van diagnostische** in het dialoogvenster.
6. Kies de **configureren** knop storage-account opgeven en klik vervolgens op de **OK** knop.
   
    Elk tabblad (met uitzondering van **algemene** en **logboek mappen**) vertegenwoordigt een diagnostische gegevensbron die u kunt verzamelen.
   
    ![Azure diagnostics- en configuratie inschakelen](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC758144.png)
   
    Het standaardtabblad **algemene**, biedt de volgende opties van diagnostische gegevens verzameling: **alleen fouten**, **alle informatie**, en **aangepaste plan**. De standaardoptie **alleen fouten**, zo min mogelijk opslag vereist omdat deze geen waarschuwingen of tracering berichten over te dragen. De **alle informatie** optie de meeste gegevens worden overgebracht en is daarom de optie meest kostbaar in termen van opslag.
7. Selecteer voor dit voorbeeld wordt de **aangepaste plan** optie zodat u de gegevens kunt worden verzameld.
8. De **schijfquotum in MB** vak geeft aan hoeveel ruimte u in uw opslagaccount voor diagnostische gegevens wilt toewijzen. U kunt de standaardwaarde als u wilt wijzigen.
9. Op elk tabblad van diagnostische gegevens u wilt verzamelen, selecteer de **inschakelen overdragen van <log type>**  selectievakje.
   
    Bijvoorbeeld, als u wenst te verzamelen van toepassingslogboeken, selecteert u de **inschakelen van de overdracht van toepassingslogboeken** selectievakje op het **toepassingslogboeken** tabblad. Geef ook andere informatie die vereist zijn voor elk gegevenstype diagnostische gegevens. Zie de sectie **gegevensbronnen van diagnostische gegevens configureren** verderop in dit onderwerp voor configuratie-informatie op elk tabblad.
10. Nadat u de verzameling van alle diagnostics-gegevens die u hebt ingeschakeld, kiest u de **OK** knop.
11. Sla het bijgewerkte project.
    
     U ziet een bericht in de **Microsoft Azure Activity Log** venster dat de virtuele machine is bijgewerkt.

## <a name="configure-diagnostics-data-sources"></a>Gegevensbronnen van diagnostische gegevens configureren
Nadat u het verzamelen van diagnostische gegevens inschakelen, kunt u precies welke gegevensbronnen die u wenst te verzamelen en welke informatie wordt verzameld. Hieronder volgt een lijst van tabbladen in de **configuratie van diagnostische** in het dialoogvenster en elke configuratieoptie betekent.

### <a name="application-logs"></a>Toepassingslogboeken
**Toepassingslogboeken** diagnostische informatie die wordt geproduceerd door een webtoepassing bevatten. Als u vastleggen toepassingslogboeken wilt, selecteert u de **inschakelen van de overdracht van toepassingslogboeken** selectievakje. U kunt vergroten of verkleinen het aantal minuten wanneer de toepassingslogboeken worden overgebracht naar uw opslagaccount door het wijzigen van de **Transfer periode (min)** waarde. U kunt ook de hoeveelheid gegevens die zijn vastgelegd in het logboek door de waarde van logboek-niveau wijzigen. U kunt bijvoorbeeld **uitgebreid** met meer informatie of kies een **Kritiek** om vast te leggen alleen kritieke fouten. Als u een specifieke diagnostics-provider die u toepassingslogboeken verzendt hebt, kunt u ze vastleggen door toe te voegen GUID van de provider de **Provider GUID** vak.

  ![Toepassingslogboeken](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC758145.png)

  Zie [logboekregistratie van diagnostische gegevens van web-apps in Azure App Service](app-service-web/web-sites-enable-diagnostic-log.md) voor meer informatie over toepassingslogboeken.

### <a name="windows-event-logs"></a>Windows-gebeurtenislogboeken
Als u vastleggen van Windows-gebeurtenislogboeken wilt, selecteert u de **overdracht van het Windows-gebeurtenislogboeken inschakelen** selectievakje. U kunt vergroten of verkleinen het aantal minuten wanneer de gebeurtenislogboeken worden overgebracht naar uw opslagaccount door het wijzigen van de **Transfer periode (min)** waarde. Schakel de selectievakjes voor de typen gebeurtenissen die u wilt traceren.

  ![Gebeurtenislogboeken](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC796664.png)

Als u Azure SDK 2.6 of hoger en een aangepaste gegevensbron opgeven, typt u dit in de  **<Data source name>**  tekst vak en kies vervolgens de **toevoegen** knop ernaast. De gegevensbron is toegevoegd aan het bestand diagnostics.cfcfg.

Als u Azure SDK 2.5 en geef een aangepaste gegevensbron wilt, kunt u het toevoegen aan de `WindowsEventLog` sectie van de diagnostics.wadcfgx bestand, zoals in het volgende voorbeeld.

```
<WindowsEventLog scheduledTransferPeriod="PT1M">
   <DataSource name="Application!*" />
   <DataSource name="CustomDataSource!*" />
</WindowsEventLog>
```
### <a name="performance-counters"></a>Prestatiemeteritems
Gegevens van prestatiemeteritems kunt u vinden knelpunten in het systeem en systeem- en -prestaties afstemmen. Zie [maken en prestatiemeteritems voor gebruik in een Azure-toepassing](https://msdn.microsoft.com/library/azure/hh411542.aspx) voor meer informatie. Als u vastleggen, prestatiemeteritems wilt, selecteert u de **overdracht van prestatiemeteritems inschakelen** selectievakje. U kunt vergroten of verkleinen het aantal minuten wanneer de gebeurtenislogboeken worden overgebracht naar uw opslagaccount door het wijzigen van de **Transfer periode (min)** waarde. Schakel de selectievakjes voor de prestatiemeteritems die u wilt traceren.

  ![Prestatiemeteritems](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC758147.png)

Voer deze met behulp van de voorgestelde syntaxis voor het bijhouden van een prestatiemeteritem die niet is vermeld, en kies vervolgens de **toevoegen** knop. Het besturingssysteem op de virtuele machine bepaalt welke prestatiemeteritems die u kunt volgen. Zie voor meer informatie over de syntaxis [geven een itempad](https://msdn.microsoft.com/library/windows/desktop/aa373193.aspx).

### <a name="infrastructure-logs"></a>Logboeken van de infrastructuur
Als u wilt om vast te leggen van infrastructuur-logboeken die informatie over de diagnostische Azure-infrastructuur bevatten, de module RemoteAccess en RemoteForwarder-module, selecteert de **overdracht van infrastructuur Logboeken inschakelen** controleren vak. U kunt vergroten of verkleinen van het aantal minuten wanneer de logboeken worden overgebracht naar uw opslagaccount door de waarde overbrengen periode (min) te wijzigen.

  ![Diagnostische gegevens infrastructuur Logboeken](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC758148.png)

  Zie [Logboekregistratiegegevens verzamelen met behulp van Azure Diagnostics](https://msdn.microsoft.com/library/azure/gg433048.aspx) voor meer informatie.

### <a name="log-directories"></a>Logboek mappen
Als u vastleggen van logboek-mappen die gegevens verzameld van logboek-mappen voor aanvragen van Internet Information Services (IIS) bevat wilt, mislukte aanvragen of mappen die u kiest, schakelt u de **overdracht van logboek mappen inschakelen** selectievakje. U kunt vergroten of verkleinen het aantal minuten wanneer de logboeken worden overgebracht naar uw opslagaccount door het wijzigen van de **Transfer periode (min)** waarde.

Kunt u de selectievakjes van de logboeken die u verzamelen wilt, zoals **IIS-logboeken** en **kan aanvragen** Logboeken. Standaard opslag containernamen worden opgegeven, maar u kunt de namen wijzigen als u wilt.

U kunt ook de logboeken van de map vastleggen. Alleen het pad opgeven in de **logboek van Directory Absolute** sectie en kies vervolgens de **map toevoegen** knop. De logboeken wordt aan de opgegeven containers worden vastgelegd.

  ![Logboek mappen](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC796665.png)

### <a name="etw-logs"></a>ETW-Logboeken
Als u [Event Tracing for Windows](https://msdn.microsoft.com/library/windows/desktop/bb968803\(v=vs.85\).aspx) (ETW) en wilt vastleggen ETW-Logboeken, selecteer de **overdracht van ETW-Logboeken inschakelen** selectievakje. U kunt vergroten of verkleinen het aantal minuten wanneer de logboeken worden overgebracht naar uw opslagaccount door het wijzigen van de **Transfer periode (min)** waarde.

De gebeurtenissen worden vastgelegd van bronnen van gebeurtenissen en het gebeurtenismanifesten die u opgeeft. Als u een gebeurtenisbron, voer een naam in de **gebeurtenisbronnen** sectie en kies vervolgens de **gebeurtenisbron toevoegen** knop. Op deze manier kunt u een manifest van de gebeurtenis in de **gebeurtenis manifesten** sectie en kies vervolgens de **toevoegen gebeurtenis Manifest** knop.

  ![ETW-Logboeken](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC766025.png)

  Het ETW-framework wordt in ASP.NET ondersteund door de klassen in [System.Diagnostics.aspx] (naamruimte https://msdn.microsoft.com/library/system.diagnostics (v=vs.110). De Microsoft.WindowsAzure.Diagnostics naamruimte overneemt en standard [System.Diagnostics.aspx] breidt (https://msdn.microsoft.com/library/system.diagnostics (v=vs.110) klassen, maakt het gebruik van [System.Diagnostics.aspx] (https : //msdn.microsoft.com/library/system.diagnostics(v=vs.110) als een framework voor logboekregistratie in de Azure-omgeving. Zie voor meer informatie [besturingselement nemen van logboekregistratie en tracering in Microsoft Azure](https://msdn.microsoft.com/magazine/ff714589.aspx) en [diagnostische gegevens inschakelen in Azure Cloud Services en virtuele Machines](cloud-services/cloud-services-dotnet-diagnostics.md).

### <a name="crash-dumps"></a>Crashdumps
Als u wilt vastleggen van gegevens over wanneer een rolinstantie is vastgelopen, selecteert u de **inschakelen van de overdracht van Crash dumpen** selectievakje. (Omdat ASP.NET de meeste uitzonderingen verwerkt, dit is doorgaans alleen nuttig voor werkrollen.) U kunt vergroten of verkleinen van het percentage van de opslagruimte die aan de crashdumps besteed door het wijzigen van de **Directory quotum (%)** waarde. U kunt de opslagcontainer waarin de crashdumps worden opgeslagen en u kunt aangeven of u wilt vastleggen wijzigen een **volledige** of **Mini** dump.

De processen die momenteel worden bijgehouden, worden weergegeven. Schakel de selectievakjes voor de processen die u wilt vastleggen. Een ander proces toevoegen aan de lijst, voer de procesnaam en kies vervolgens de **proces toevoegen** knop.

  ![Crashdumps](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC766026.png)

  Zie [besturingselement nemen van logboekregistratie en tracering in Microsoft Azure](https://msdn.microsoft.com/magazine/ff714589.aspx) en [Microsoft Azure Diagnostics deel 4: aangepaste logboekregistratie onderdelen en Azure Diagnostics 1.3 wijzigingen](http://justazure.com/microsoft-azure-diagnostics-part-4-custom-logging-components-azure-diagnostics-1-3-changes/) voor meer informatie.

## <a name="view-the-diagnostics-data"></a>De diagnostics-gegevens weergeven
Als u de diagnostics-gegevens voor een cloudservice of een virtuele machine hebt verzameld, kunt u het kunt weergeven.

### <a name="to-view-cloud-service-diagnostics-data"></a>Cloud service diagnostische gegevens weergeven
1. Implementeer uw cloudservice als normaal en vervolgens uit te voeren.
2. U kunt de diagnostics-gegevens weergeven in een rapport met Visual Studio gegenereerd of tabellen in uw opslagaccount. U kunt de gegevens in een rapport bekijken **Cloud Explorer** of **Server Explorer**, open het snelmenu van het knooppunt voor de rol die u interesseert en kies vervolgens **weergave diagnostische gegevens**.
   
    ![De Diagnostics-gegevens weergeven](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC748912.png)
   
    Een rapport met de beschikbare gegevens wordt weergegeven.
   
    ![Rapport van de Microsoft Azure Diagnostics in Visual Studio](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC796666.png)
   
    Als de meest recente gegevens niet wordt weergegeven, moet u wellicht wacht u totdat de overdracht is verstreken.
   
    Kies de **vernieuwen** koppelen aan de gegevens direct bijwerken of kies een interval in de **automatisch vernieuwen** vervolgkeuzelijst om de gegevens automatisch bijgewerkt. De om foutgegevens te exporteren, kies de **exporteren naar CSV** knop een door komma's gescheiden waarde-bestand dat u in een werkblad openen kunt te maken.
   
    In **Cloud Explorer** of **Server Explorer**, opent u het opslagaccount dat is gekoppeld aan de implementatie.
3. Open de diagnostics-tabellen in de tabel viewer en controleer de gegevens die u hebt verzameld. U kunt een blob-container openen voor IIS-logboeken en aangepaste logboeken. Aan de hand van de volgende tabel vindt u de tabel of blob-container die de gegevens bevat die u bent geïnteresseerd. Naast de gegevens voor die logboekbestand items in de tabel bevatten EventTickCount, DeploymentId rol en RoleInstance om te identificeren welke virtuele machine en de rol van de gegevens gegenereerd en wanneer. 
   
   | Diagnostische gegevens | Beschrijving | Locatie |
   | --- | --- | --- |
   | Toepassingslogboeken |De logboeken die uw code wordt gegenereerd door het aanroepen van methoden van de klasse System.Diagnostics.Trace. |WADLogsTable |
   | Gebeurtenislogboeken |Deze gegevens zijn uit de Windows-gebeurtenislogboeken op de virtuele machines. Slaat Windows de informatie in deze logboeken, maar toepassingen en services ook gebruiken om te rapporteren van fouten of logboekgegevens. |WADWindowsEventLogsTable |
   | Prestatiemeteritems |U kunt gegevens verzamelen op elk prestatiemeteritem dat beschikbaar is op de virtuele machine. Het besturingssysteem biedt prestatiemeteritems, waaronder veel statistische gegevens zoals geheugen en de processor tijd. |WADPerformanceCountersTable |
   | Logboeken van de infrastructuur |Deze logboeken worden gegenereerd op basis van de infrastructuur van diagnostische gegevens zelf. |WADDiagnosticInfrastructureLogsTable |
   | IIS-logboeken |Deze logboeken vastleggen webaanvragen. Als uw cloudservice een aanzienlijke hoeveelheid verkeer ontvangt, zijn deze logboeken behoorlijk langdurige, dus u moet verzamelen en opslaan van deze gegevens alleen wanneer u deze nodig. |U vindt is mislukt-aanvraag wordt geregistreerd in de blob-container onder af iis failedreqlogs onder een pad op voor deze implementatie, rol en exemplaar. U vindt de volledige Logboeken onder af-iis-logboekbestanden. Vermeldingen voor elk bestand worden in de tabel WADDirectories gedaan. |
   | Crashdumps |Deze informatie biedt binaire installatiekopieën van uw cloudservice-proces (meestal een werkrol). |af-crush-dumpbestanden voor blob-container |
   | Aangepaste logboekbestanden |Logboeken van de gegevens die u vooraf gedefinieerd. |U kunt in de code de locatie opgeven van aangepaste logboekbestanden in uw opslagaccount. U kunt bijvoorbeeld een aangepaste blob-container opgeven. |
4. Als u gegevens van een willekeurig type worden afgekapt, kunt u proberen verhogen van de buffer voor die gegevens type of verkort het interval tussen de overdracht van gegevens van de virtuele machine naar uw opslagaccount.
5. (optioneel) Gegevens verwijderen uit het opslagaccount van tijd tot tijd om de algehele opslagkosten te verlagen.
6. Wanneer u een volledige implementatie, het bestand diagnostics.cscfg (.wadcfgx voor Azure SDK 2.5) wordt bijgewerkt in Azure en uw cloudservice neemt over wijzigingen in de configuratie van de diagnostische gegevens. Als u, in plaats daarvan een bestaande implementatie hebt bijgewerkt, wordt het cscfg-bestand is niet bijgewerkt in Azure. U kunt nog steeds de diagnostische instellingen echter wijzigen door de stappen in de volgende sectie. Zie voor meer informatie over het uitvoeren van een volledige implementatie en het bijwerken van een bestaande implementatie [Publish Azure Application Wizard](vs-azure-tools-publish-azure-application-wizard.md).

### <a name="to-view-virtual-machine-diagnostics-data"></a>Virtuele machine diagnostische gegevens weergeven
1. Kies in het snelmenu voor de virtuele machine **weergave Diagnostics-gegevens**.
   
    ![Diagnostische gegevens weergeven in de virtuele machine van Azure](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC766027.png)
   
    Hiermee opent u de **Diagnostics samenvatting** venster.
   
    ![Virtuele machine van Azure diagnostics samenvatting](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC796667.png)  
   
    Als de meest recente gegevens niet wordt weergegeven, moet u wellicht wacht u totdat de overdracht is verstreken.
   
    Kies de **vernieuwen** koppelen aan de gegevens direct bijwerken of kies een interval in de **automatisch vernieuwen** vervolgkeuzelijst om de gegevens automatisch bijgewerkt. De om foutgegevens te exporteren, kies de **exporteren naar CSV** knop een door komma's gescheiden waarde-bestand dat u in een werkblad openen kunt te maken.

## <a name="configure-cloud-service-diagnostics-after-deployment"></a>Cloud service diagnostische gegevens configureren na implementatie
Als u bij het onderzoeken van een probleem met een cloud service die al wordt uitgevoerd, kunt u voor het verzamelen van gegevens die u hebt opgegeven voordat u de rol oorspronkelijk geïmplementeerd. U kunt in dit geval starten voor het verzamelen van gegevens met behulp van de instellingen in Server Explorer. U kunt diagnostische gegevens voor één exemplaar of alle exemplaren in een rol, afhankelijk van of u het dialoogvenster configuratie van diagnostische vanuit het snelmenu voor het exemplaar of de functie openen configureren. Als u het knooppunt rol configureert, worden eventuele wijzigingen gelden voor alle exemplaren. Als u het knooppunt exemplaar configureert, worden eventuele wijzigingen gelden voor alleen dat exemplaar.

### <a name="to-configure-diagnostics-for-a-running-cloud-service"></a>Diagnostische gegevens voor een actieve cloudservice configureren
1. Vouw in Server Explorer de **Cloudservices** knooppunt, en vouw de knooppunten om te zoeken van de rol of -exemplaar dat u wilt onderzoeken of beide.
   
    ![Configuratie van diagnostische gegevens](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC748913.png)
2. Kies in het snelmenu voor het knooppunt van een exemplaar of een knooppunt van de rol **Update diagnostische instellingen**, en kies vervolgens de diagnostische instellingen die u wilt verzamelen.
   
    Zie voor informatie over de configuratie-instellingen, **gegevensbronnen van diagnostische gegevens configureren** in dit onderwerp. Zie voor meer informatie over het weergeven van de diagnostics-gegevens **de diagnostics-gegevens weergeven** in dit onderwerp.
   
    Als u het verzamelen van gegevens in wijzigt **Server Explorer**, deze wijzigingen blijven van kracht totdat u de cloudservice volledig opnieuw implementeren. Als u de standaardwaarde gebruiken publicatie-instellingen, de wijzigingen niet worden overschreven, omdat het publiceren van de standaard-instelling is bijwerken van de bestaande implementatie in plaats van een volledig opnieuw implementeren gaande doen. Om er zeker van te zijn de instellingen tijdens de implementatie wissen, gaat u naar de **geavanceerde instellingen** tabblad in de wizard Publiceren en wis de **implementatie-update** selectievakje. Wanneer u opnieuw met dit selectievakje is uitgeschakeld implementeert, terug de instellingen die in het bestand .wadcfgx (of .wadcfg) zoals ingesteld via de eigenschappen van editor voor de rol. Als u uw implementatie hebt bijgewerkt, houdt Azure de oude instellingen.

## <a name="troubleshoot-azure-cloud-service-issues"></a>Problemen met Azure cloud service
Als er problemen met uw cloudserviceprojecten, zoals een rol die blijft in 'bezet' status steken opgehaald herhaaldelijk wordt gerecycled of er een interne serverfout, er zijn hulpprogramma's en technieken die u kunt opsporen en oplossen van deze problemen. Zie voor specifieke voorbeelden van algemene problemen en oplossingen, evenals een overzicht van de concepten en hulpprogramma's voor het opsporen en oplossen van dergelijke fouten, [Azure PaaS Compute Diagnostics-gegevens](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx).

## <a name="q--a"></a>Vragen en antwoorden
**Wat de buffergrootte is en hoe lang deze moet?**

Op elk exemplaar van de virtuele machine beperken quota's hoeveel diagnostische gegevens kan worden opgeslagen op het lokale bestandssysteem. Bovendien het opgeven van een buffergrootte voor elk type diagnostische gegevens die beschikbaar is. Deze buffergrootte fungeert als een quotum voor dit type gegevens. U kunt de algehele quota en de hoeveelheid geheugen die overblijft bepalen door het controleren van de onderkant van het dialoogvenster. Als u groter buffers of meerdere typen gegevens opgeeft, moet u de algehele quota benaderen. U kunt de algehele quota wijzigen door het wijzigen van het configuratiebestand diagnostics.wadcfg/.wadcfgx. De diagnostics-gegevens worden opgeslagen op het bestandssysteem dezelfde als de gegevens van uw toepassing, dus als uw toepassing gebruikmaakt van een groot aantal schijfruimte, u kunt de algehele diagnostics quotum mag niet verhogen.

**Wat is de periode voor de overdracht en hoe lang deze moet?**

De overdracht periode is de hoeveelheid tijd die is verstreken tussen gegevens worden vastgelegd. Na elke periode overdracht worden gegevens verplaatst uit het lokale bestandssysteem op een virtuele machine aan tabellen in uw opslagaccount. Als de hoeveelheid gegevens die worden verzameld het quotum voor het einde van een overdracht-periode overschrijdt, wordt de oudere gegevens verwijderd. Mogelijk wilt de periode overdracht verlagen als u bent verlies van gegevens omdat de gegevens groter is dan de buffergrootte of het algehele quotum.

**Welke tijdzone zijn de tijdstempels in?**

De tijdstempels zijn in de lokale tijdzone van het datacenter dat als host fungeert voor uw cloudservice. De volgende drie timestamp-kolommen in de tabellen logboek worden gebruikt.

* **PreciseTimeStamp** de ETW-tijdstempel van de gebeurtenis. Dat wil zeggen de tijd van de client wordt de gebeurtenis vastgelegd.
* **TIJDSTEMPEL** wordt PreciseTimeStamp omlaag afgerond op de grens van de frequentie uploaden. Dus als uw uploadfrequentie 5 minuten en de gebeurtenis tijd 00:17:12 is, TIMESTAMP worden 00:15:00.
* **Tijdstempel** de tijdstempel waarop de entiteit is gemaakt in de Azure-tabel.

**Hoe beheer ik kosten bij het verzamelen van diagnostische gegevens?**

De standaardinstellingen (**Meld niveau** ingesteld op **fout** en **overdracht periode** ingesteld op **1 minuut**) zijn ontworpen om kosten te minimaliseren. De compute-kosten wordt verhoogd als u meer diagnostische gegevens verzamelen of verklein de periode voor overdracht. Niet meer gegevens dan u nodig hebt en u niet vergeten om het verzamelen van gegevens uitschakelen wanneer u niet langer verzamelen. U kunt altijd het opnieuw inschakelen, zelfs tijdens runtime, zoals wordt weergegeven in de vorige sectie.

**Hoe ik Logboeken is mislukt-aanvragen verzamelen uit IIS?**

Standaard verzamelen niet IIS logboeken is mislukt-aanvragen. U kunt IIS voor het verzamelen van deze als u het bestand web.config voor de Webrol bewerken configureren.

**Ik ben traceringsinformatie niet ophalen uit RoleEntryPoint methoden zoals OnStart. Wat is er aan de hand?**

De methoden van RoleEntryPoint worden genoemd in de context van WAIISHost.exe, niet in IIS. Daarom de configuratiegegevens in web.config die normaal gesproken schakelt tracering niet van toepassing. U lost dit probleem, een .config-bestand toevoegen aan uw webrolproject en noem het bestand overeenkomen met de uitvoer-assembly die de RoleEntryPoint-code bevat. In het webrolproject standaard is de naam van het .config-bestand WAIISHost.exe.config. Voeg vervolgens de volgende regels toe aan dit bestand:

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

Nu in de **eigenschappen** Stel venster de **naar uitvoermap kopiëren** eigenschap **altijd kopiëren**.

## <a name="next-steps"></a>Volgende stappen
Zie voor meer informatie over diagnostische gegevens van logboekregistratie in Azure, [diagnostische gegevens inschakelen in Azure Cloud Services en virtuele Machines](cloud-services/cloud-services-dotnet-diagnostics.md) en [logboekregistratie van diagnostische gegevens van web-apps in Azure App Service](app-service-web/web-sites-enable-diagnostic-log.md).


---
title: aaaData Management Gateway voor Data Factory | Microsoft Docs
description: Instellen van een data gateway toomove gegevens tussen on-premises en Hallo cloud. Gebruik van Data Management Gateway in Azure Data Factory toomove uw gegevens.
services: data-factory
documentationcenter: 
author: nabhishek
manager: jhubbard
editor: monicar
ms.assetid: b9084537-2e1c-4e96-b5bc-0e2044388ffd
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: abnarain
ms.openlocfilehash: 6f523891a6230cbc7b407f46f4b02d91dfd2cf46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="data-management-gateway"></a>Gegevensbeheergateway
Hallo Data management gateway is een clientagent waarmee u in uw on-premises omgeving toocopy gegevens tussen cloud en on-premises gegevensarchieven moet installeren. Hallo on-premises gegevens opslaat die worden ondersteund door Data Factory worden vermeld in Hallo [ondersteunde gegevensbronnen](data-factory-data-movement-activities.md#supported-data-stores-and-formats) sectie.

In dit artikel is een aanvulling op Hallo-scenario in Hallo [gegevens verplaatsen tussen on-premises en cloud gegevensarchieven](data-factory-move-data-between-onprem-and-cloud.md) artikel. In het Hallo-scenario maakt u een pijplijn die Hallo gateway toomove gegevens uit een lokale SQL Server-database tooan Azure-blob gebruikt. Dit artikel bevat gedetailleerde informatie over het Hallo data management gateway. 

U kunt een data management gateway uitbreiden door meerdere lokale computers koppelen aan Hallo-gateway. U kunt schalen omhoog door het aantal data movement taken die kunnen tegelijkertijd worden uitgevoerd op een knooppunt te verhogen. Deze functie is ook beschikbaar voor een logische gateway met één knooppunt. Zie [schaal data management gateway in Azure Data Factory](data-factory-data-management-gateway-high-availability-scalability.md) artikel voor meer informatie.

> [!NOTE]
> Gateway ondersteunt momenteel alleen Hallo kopiëren en opgeslagen procedure activiteit in de Data Factory. Het is niet mogelijk toouse Hallo gateway van een aangepaste activiteit tooaccess on-premises-gegevensbronnen.      

## <a name="overview"></a>Overzicht
### <a name="capabilities-of-data-management-gateway"></a>Mogelijkheden van data management gateway
Data management gateway biedt Hallo volgende mogelijkheden:

* Model on-premises gegevensbronnen en cloud-gegevensbronnen binnen dezelfde gegevensfactory Hallo en gegevens verplaatsen.
* Een door één venster voor bewaking en beheer inzicht in de gateway de status van Hallo Data Factory pagina hebben.
* Toegang tot tooon-premises gegevensbronnen veilig beheren.
  * Er zijn geen wijzigingen vereist toocorporate firewall. Gateway, wordt alleen uitgaande HTTP-gebaseerde verbindingen tooopen internet.
  * Referenties voor uw on-premises gegevensopslagexemplaren met uw certificaat niet versleutelen.
* Gegevens efficiënt te verplaatsen: de gegevens worden overgebracht in parallelle, robuuste toointermittent netwerkproblemen met automatische Pogingslogica.

### <a name="command-flow-and-data-flow"></a>Opdracht stroom en de gegevensstroom
Wanneer u een kopie toocopy activiteitsgegevens tussen on-premises en cloud, Hallo activiteit maakt gebruik van een gateway tootransfer gegevens van lokale gegevensbron toocloud en vice versa.

Hier volgt Hallo op hoog niveau gegevensstroom voor en overzicht van stappen voor het kopiëren met gegevensgateway: ![gegevensstroom met gateway](./media/data-factory-data-management-gateway/data-flow-using-gateway.png)

1. Gegevens ontwikkelaars een gateway maakt voor een Azure Data Factory met beide Hallo [Azure-portal](https://portal.azure.com) of [PowerShell-Cmdlet](https://msdn.microsoft.com/library/dn820234.aspx).
2. Een gekoppelde service voor een on-premises gegevensopslag maakt gegevens developer door te geven Hallo-gateway. Als onderdeel van het instellen van Hallo service gekoppelde, gebruikt de gegevens developer Hallo instelling referenties toospecify verificatie toepassingstypen en referenties.  Hallo instelling referenties dialoogvenster toepassing met de Hallo gegevens communiceert tootest verbinding en Hallo gateway toosave referenties opgeslagen.
3. Gateway versleutelt Hallo-referenties met Hallo-certificaat dat is gekoppeld met Hallo-gateway (opgegeven door de ontwikkelaar gegevens), voordat Hallo-referenties in Hallo cloud worden opgeslagen.
4. Data Factory-service communiceert met de gateway Hallo voor planning en beheer van taken via een besturingskanaal die gebruikmaakt van een gedeelde Azure service bus-wachtrij. Wanneer een taak kopiëren activiteit toobe gestarte moet, wachtrijen Data Factory Hallo aanvraag samen met de referentie-informatie. Gateway serversysteemstatus Hallo taak na polling Hallo wachtrij.
5. Hallo gateway ontsleutelt Hallo-referenties met Hallo hetzelfde certificaat en vervolgens toohello on-premises gegevensopslag verbindt met de juiste authenticatietype en referenties.
6. Hallo-gateway worden gegevens gekopieerd van een lokale store tooa cloud-opslag of omgekeerd, afhankelijk van hoe Hallo Kopieeractiviteit in Hallo gegevens pijplijn is geconfigureerd. Voor deze stap communiceert Hallo-gateway rechtstreeks met cloud-gebaseerde storage-services zoals Azure Blob Storage via een beveiligd kanaal voor (HTTPS).

### <a name="considerations-for-using-gateway"></a>Overwegingen voor het gebruik van gateway
* Één exemplaar van data management gateway kan worden gebruikt voor meerdere on-premises-gegevensbronnen. Echter, **één gatewayexemplaar is gebonden tooonly één Azure-gegevensfactory** en kan niet worden gedeeld met een andere data factory.
* U kunt hebben **slechts één exemplaar van data management gateway** geïnstalleerd op een enkele computer. Stel dat u hebt twee gegevensfactory's die tooaccess on-premises gegevensbronnen moeten, moet u de gateways tooinstall op twee on-premises computers. Met andere woorden, is een gateway gebonden tooa specifieke data factory
* Hallo **gateway niet hoeft toobe op dezelfde computer als de gegevensbron Hallo Hallo**. Gateway dichter toohello gegevensbron met minder echter Hallo-tijd voor Hallo gateway tooconnect toohello-gegevensbron. Het is raadzaam dat u Hallo-gateway installeert op een machine die verschilt van Hallo een die hosts on-premises-gegevensbron. Wanneer het Hallo-gateway en de gegevensbron zich op verschillende computers bevinden, Hallo gateway niet zou concurreren voor bronnen met de gegevensbron.
* U kunt hebben **meerdere gateways op verschillende computers verbinding maken met toohello dezelfde lokale gegevensbron**. Bijvoorbeeld wellicht hebt u twee gateways voor de twee gegevensfactory maar Hallo dezelfde on-premises-gegevensbron is geregistreerd bij beide Hallo data Factory.
* Als u al een gateway geïnstalleerd op uw computer voor een **Power BI** scenario installeert een **afzonderlijke gateway voor Azure Data Factory** op een andere computer.
* Gateway moet worden gebruikt, zelfs wanneer u **ExpressRoute**.
* Uw gegevensbron behandelen als een lokale gegevensbron (die zich achter een firewall) zelfs als u werkt met **ExpressRoute**. Gebruik Hallo gateway tooestablish-verbinding tussen Hallo-service en het Hallo-gegevensbron.
* U moet **Hallo-gateway gebruiken** zelfs als het Hallo-gegevensarchief is het Hallo-cloud op een **Azure IaaS VM**.

## <a name="installation"></a>Installeren
### <a name="prerequisites"></a>Vereisten
* Hallo ondersteund **besturingssysteem** versies zijn Windows 7, Windows 8/8.1, Windows 10, Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2. Installatie van Hallo data management gateway op een domeincontroller wordt momenteel niet ondersteund.
* .NET framework 4.5.1 of hoger is vereist. Als u gateway op een computer met Windows 7 installeert, installeert u .NET Framework 4.5 of hoger. Zie [.NET Framework-systeemvereisten](https://msdn.microsoft.com/library/8z6watww.aspx) voor meer informatie.
* Hallo aanbevolen **configuratie** voor Hallo gatewaycomputer ten minste 2 GHz, 4 kernen, 8 GB RAM-geheugen en schijf 80 GB is.
* Als de hostmachine Hallo in de slaapstand, reageert Hallo gateway toodata aanvragen niet. Configureer daarom een geschikte **energiebeheerschema** op Hallo computer voordat u Hallo-gateway installeert. Als Hallo machine geconfigureerde toohibernate is, vraagt Hallo gateway-installatie een bericht.
* U moet een beheerder op Hallo machine tooinstall en Hallo data management gateway is configureren. U kunt extra gebruikers toohello toevoegen **data management gateway gebruikers** lokale Windows-groep. Hallo-leden van deze groep zijn kunnen toouse hello **Data Management Gateway Configuration Manager** hulpprogramma tooconfigure Hallo gateway.

U kopieert geval activiteit wordt uitgevoerd op een specifieke frequentie, volgt hello Resourcegebruik op de machine hello (CPU, geheugen) ook Hallo hetzelfde patroon met piek- en niet-actieve tijd. Resourcegebruik ook afhankelijk van geheugenlatentie hello en de hoeveelheid gegevens worden verplaatst. Als meerdere kopie taken uitgevoerd worden, ziet u Resourcegebruik tijdens piektijden omhoog gaan.

### <a name="installation-options"></a>Opties voor de installatie
Data management gateway kan worden geïnstalleerd in de volgende manieren Hallo:

* Door een MSI-installatiepakket downloaden van Hallo [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=39717).  Hallo MSI kan ook worden gebruikt tooupgrade bestaande data management gateway toohello nieuwste versie, met alle instellingen behouden.
* Door te klikken op **downloaden en installeren van de gegevensgateway** koppeling onder handmatige installatie of **rechtstreeks op deze computer installeren** onder snelle installatie. Zie [gegevens verplaatsen tussen on-premises en cloud](data-factory-move-data-between-onprem-and-cloud.md) artikel voor stapsgewijze instructies over het gebruik van de snelle installatie. Hallo handmatige stap gaat u toohello Downloadcentrum.  Hallo-instructies voor het downloaden en installeren van de gateway Hallo van Downloadcentrum zijn in de volgende sectie Hallo.

### <a name="installation-best-practices"></a>Best practices voor installatie:
1. Energiebeheerschema op de hostmachine Hallo voor Hallo gateway zodanig configureren dat hello machine niet in slaapstand. Als de hostmachine Hallo in de slaapstand, reageert Hallo gateway toodata aanvragen niet.
2. Back-up Hallo-certificaat dat is gekoppeld met Hallo-gateway.

### <a name="install-hello-gateway-from-download-center"></a>Hallo-gateway installeren van Downloadcentrum
1. Navigeer te[Microsoft Data Management Gateway-downloadpagina](https://www.microsoft.com/download/details.aspx?id=39717).
2. Klik op **downloaden**, selecteer de juiste versie Hallo (**32-bits** vs. **64-bits**), en klik op **volgende**.
3. Voer Hallo **MSI** rechtstreeks of sla deze tooyour hardeschijf en worden uitgevoerd.
4. Op Hallo **Welkom** pagina een **taal** klikt u op **volgende**.
5. **Accepteer** Hallo gebruiksrechtovereenkomst en klik op **volgende**.
6. Selecteer **map** tooinstall Hallo gateway en klikt u op **volgende**.
7. Op Hallo **gereed tooinstall** pagina, klikt u op **installeren**.
8. Klik op **voltooien** toocomplete-installatie.
9. Hallo-sleutel ophalen uit hello Azure-portal. Zie de volgende sectie Hallo voor stapsgewijze instructies.
10. Op Hallo **gateway registreren** pagina van **Data Management Gateway Configuration Manager** uitgevoerd op uw machine Hallo volgende stappen:
    1. Hallo-sleutel in Hallo tekst te plakken.
    2. Klik desgewenst op **weergeven gatewaycode** toosee Hallo Sleuteltekst.
    3. Klik op **registreren**.

### <a name="register-gateway-using-key"></a>Registreer gateway met sleutel
#### <a name="if-you-havent-already-created-a-logical-gateway-in-hello-portal"></a>Als u een logische gateway al hebt gemaakt in Hallo-portal
een gateway in Hallo-portal en get Hallo sleutel vanuit Hallo toocreate **configureren** pagina, volg de stappen van de procedures in Hallo [gegevens verplaatsen tussen on-premises en cloud](data-factory-move-data-between-onprem-and-cloud.md) artikel.    

#### <a name="if-you-have-already-created-hello-logical-gateway-in-hello-portal"></a>Als u al logische Hallo-gateway hebt gemaakt in Hallo-portal
1. Navigeer in Azure portal toohello **Data Factory** pagina en klik op **gekoppelde Services** tegel.

    ![Data Factory-pagina](media/data-factory-data-management-gateway/data-factory-blade.png)
2. In Hallo **gekoppelde Services** pagina, selecteer Hallo logische **gateway** u in het Hallo-portal hebt gemaakt.

    ![logische gateway](media/data-factory-data-management-gateway/data-factory-select-gateway.png)  
3. In Hallo **Data Gateway** pagina, klikt u op **downloaden en installeren van de gegevensgateway**.

    ![Koppeling in de portal Hallo downloaden](media/data-factory-data-management-gateway/download-and-install-link-on-portal.png)   
4. In Hallo **configureren** pagina, klikt u op **Maak sleutel**. Klik op Ja op Hallo waarschuwing na het lezen van deze zorgvuldig.

    ![Sleutel opnieuw maken](media/data-factory-data-management-gateway/recreate-key-button.png)
5. Klik op kopiëren knop volgende toohello sleutel. Hallo-sleutel is gekopieerd toohello Klembord.

    ![Kopieer sleutel](media/data-factory-data-management-gateway/copy-gateway-key.png)

### <a name="system-tray-icons-notifications"></a>Pictogrammen in systeemvak / meldingen
Hallo volgende afbeelding ziet u enkele Hallo pictogrammen in systeemvak die u ziet.

![pictogrammen in systeemvak](./media/data-factory-data-management-gateway/gateway-tray-icons.png)

Als u de cursor op Hallo system lade pictogram/Meldingsbericht plaatst, ziet u gegevens over Hallo status van de bewerking van de Hallo gateway/bijwerken in een pop-upvenster.

### <a name="ports-and-firewall"></a>Poorten en firewall
Er zijn twee firewalls, moet u tooconsider: **bedrijfsfirewall** uitgevoerd op de centrale Hallo-router van de organisatie hello, en **Windows firewall** geconfigureerd als een daemon op de lokale machine Hallo waar hello gateway is geïnstalleerd.  

![firewalls](./media/data-factory-data-management-gateway/firewalls2.png)

Op het niveau van de firewall van het bedrijf, moet u configureren Hallo volgende domeinen en uitgaande poorten:

| Domeinnamen | Poorten | Beschrijving |
| --- | --- | --- |
| *. servicebus.windows.net |443, 80 |Gebruikt voor communicatie met Data Movement Service back-end |
| *. core.windows.net |443 |Gebruikt voor de tijdelijke kopie met behulp van Azure-Blob (indien geconfigureerd)|
| *. frontend.clouddatahub.net |443 |Gebruikt voor communicatie met Data Movement Service back-end |


Deze uitgaande poorten zijn normaal gesproken op niveau van Windows firewall is ingeschakeld. Als u niet het geval is, kunt u Hallo domeinen en poorten dienovereenkomstig op gateway-apparaat.

> [!NOTE]
> 1. Op basis van de bron / put wellicht hebt u extra domeinen toowhitelist en uitgaande poorten in uw zakelijke/Windows firewall.
> 2. Voor sommige Databases van de Cloud (bijvoorbeeld: [Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-configure-firewall-settings), [Azure Data Lake](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-secure-data#set-ip-address-range-for-data-access), enzovoort), moet u mogelijk toowhitelist IP-adres van de computer met de Gateway op de firewallconfiguratie.
>
>


#### <a name="copy-data-from-a-source-data-store-tooa-sink-data-store"></a>Gegevens kopiëren van een data store tooa sink brongegevensarchief
Zorg ervoor dat Hallo firewallregels correct zijn ingeschakeld op Hallo bedrijfsfirewall, Windows firewall op Hallo gateway-apparaat en Hallo gegevensarchief zelf. Inschakelen van deze regels kan Hallo gateway tooconnect tooboth bron en sink is. Regels voor elke gegevensopslag die bij de kopieerbewerking Hallo betrokken is inschakelen.

Bijvoorbeeld, toocopy van **een sink lokale gegevens store tooan Azure SQL Database of een Azure SQL Data Warehouse sink**, Hallo volgende stappen:

* Uitgaand verkeer toestaan **TCP** -communicatie op poort **1433** voor Windows firewall- en firewall van het bedrijf.
* Hallo firewall-instellingen van Azure SQL server tooadd Hallo IP-adres van Hallo gateway machine toohello lijst met toegestane IP-adressen configureren.

> [!NOTE]
> Als uw firewall kan geen uitgaande poort 1433, Gateway kan niet rechtstreeks toegang hebben tot Azure SQL. U kunt in dit geval [kopie gefaseerde](https://docs.microsoft.com/azure/data-factory/data-factory-copy-activity-performance#staged-copy) tooSQL Azure Database / SQL Azure DW. In dit scenario zou u alleen HTTPS (poort 443) voor gegevensverplaatsing Hallo vereisen.
>
>


### <a name="proxy-server-considerations"></a>Overwegingen voor proxy-server
Als uw zakelijke netwerkomgeving gebruikmaakt van een proxy server tooaccess Hallo internet, data management gateway toouse juiste proxy-instellingen configureren. U kunt Hallo proxy tijdens de initiële registratie-fase Hallo instellen.

![Set-proxy tijdens de registratie](media/data-factory-data-management-gateway/SetProxyDuringRegistration.png)

Gateway gebruikt Hallo proxy server tooconnect toohello cloud-service. Klik op **wijziging** koppeling tijdens de eerste configuratie. U ziet Hallo **proxyinstelling** dialoogvenster.

![Set-proxy met Configuratiebeheer](media/data-factory-data-management-gateway/SetProxySettings.png)

Er zijn drie opties:

* **Gebruik geen proxy**: Gateway geen expliciet proxy tooconnect toocloud services gebruikt.
* **Gebruik system proxy**: Gateway Hallo proxyinstelling is geconfigureerd in diahost.exe.config en diawp.exe.config gebruikt.  Als geen proxy is geconfigureerd in diahost.exe.config en diawp.exe.config, verbindt gatewayserver toocloud service rechtstreeks zonder gebruik te maken via proxy.
* **Aangepaste proxy gebruikt**: Hallo HTTP-proxy-instelling toouse voor de gateway in plaats van configuraties in diahost.exe.config en diawp.exe.config configureren.  Adres en poort zijn vereist.  Gebruikersnaam en wachtwoord zijn optioneel, afhankelijk van uw proxyserver verificatie-instelling.  Alle instellingen zijn versleuteld met Hallo-referentiecertificaat van het Hallo-gateway en die lokaal zijn opgeslagen op de hostmachine Hallo-gateway.

Hallo data management gateway Host Service wordt automatisch opnieuw opgestart nadat u Hallo bijgewerkt proxy-instellingen hebt opgeslagen.

Nadat de gateway is geregistreerd, als u wilt dat tooview of proxy-instellingen bijwerken, gebruikt u Data Management Gateway Configuration Manager.

1. Start **Data Management Gateway Configuration Manager**.
2. Overschakelen van toohello **instellingen** tabblad.
3. Klik op **wijziging** koppelen **HTTP-Proxy** sectie toolaunch hello **Set HTTP-Proxy** dialoogvenster.  
4. Nadat u op Hallo **volgende** knop klikt, ziet u een waarschuwingsdialoogvenster vragen voor uw machtiging toosave Hallo proxy-instellingen en start opnieuw Hallo Gateway Host Service.

U kunt weergeven en bijwerken van HTTP-proxy met behulp van Configuration Manager-hulpprogramma.

![Set-proxy met Configuratiebeheer](media/data-factory-data-management-gateway/SetProxyConfigManager.png)

> [!NOTE]
> Als u een proxyserver met NTLM-verificatie hebt ingesteld, is Gateway Host Service wordt uitgevoerd onder Hallo domeinaccount. Als u een wachtwoord voor domeinaccount later Hallo Hallo wijzigt, houd er rekening mee tooupdate configuratie-instellingen voor Hallo-service en dienovereenkomstig opnieuw. We raden dat u een speciale domein account tooaccess Hallo proxyserver gebruiken die u niet tooupdate Hallo wachtwoord regelmatig hoeft vanwege toothis-vereiste.
>
>

### <a name="configure-proxy-server-settings"></a>Proxyserverinstellingen configureren
Als u selecteert **system proxy gebruiken** instellen voor Hallo HTTP-proxy, gateway Hallo proxy-instellingen in diahost.exe.config en diawp.exe.config gebruikt.  Als er geen proxyserver is opgegeven in diahost.exe.config en diawp.exe.config, verbindt gatewayserver toocloud service rechtstreeks zonder gebruik te maken via proxy. Hallo bevat volgende procedure instructies voor het bijwerken van Hallo diahost.exe.config bestand.  

1. Het oorspronkelijke bestand Hallo vormen een veilige kopie van C:\Program Files\Microsoft Data Management Gateway\2.0\Shared\diahost.exe.config tooback in Windows Verkenner.
2. Starten van Notepad.exe uitgevoerd als administrator en open tekstbestand "C:\Program Files\Microsoft Data Management Gateway\2.0\Shared\diahost.exe.config. U vinden Hallo standaardlabel voor system.net zoals weergegeven in de volgende code Hallo:

         <system.net>
             <defaultProxy useDefaultCredentials="true" />
         </system.net>    

   Vervolgens kunt u proxy-servergegevens zoals weergegeven in het volgende voorbeeld Hallo toevoegen:

         <system.net>
               <defaultProxy enabled="true">
                     <proxy bypassonlocal="true" proxyaddress="http://proxy.domain.org:8888/" />
               </defaultProxy>
         </system.net>

   Aanvullende eigenschappen zijn toegestaan in Hallo tag toospecify Hallo vereist proxyinstellingen zoals scriptLocation. Raadpleeg te[proxy Element (netwerkinstellingen)](https://msdn.microsoft.com/library/sa91de1e.aspx) op syntaxis.

         <proxy autoDetect="true|false|unspecified" bypassonlocal="true|false|unspecified" proxyaddress="uriString" scriptLocation="uriString" usesystemdefault="true|false|unspecified "/>
3. Hallo-configuratiebestand opslaan in de oorspronkelijke locatie Hallo, start daarna Hallo Data Management Gateway Host service, die Hallo wijzigingen opneemt. toorestart hello service: Gebruik de applet services in Hallo van het Configuratiescherm, of van Hallo **Data Management Gateway Configuration Manager** > klikt u op Hallo **Service stoppen** klik vervolgens op Hallo **-Service starten**. Als het Hallo-service niet wordt gestart, is het waarschijnlijk dat er een onjuiste syntaxis van de XML-label is toegevoegd in het configuratiebestand van het Hallo-toepassing die is bewerkt.

> [!IMPORTANT]
> Vergeet niet tooupdate **beide** diahost.exe.config en diawp.exe.config.  


Bovendien toothese verwijst, moet u ook toomake of de Microsoft Azure in uw bedrijf goedgekeurde IP-adressen. Hallo-lijst met geldige Microsoft Azure-IP-adressen kan worden gedownload vanuit Hallo [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=41653).

#### <a name="possible-symptoms-for-firewall-and-proxy-server-related-issues"></a>Mogelijke problemen voor firewall en proxy server-problemen
Als u fouten vergelijkbare toohello volgende toepassingsgroepen ondervindt, is het waarschijnlijk vanwege tooimproper configuratie van Hallo-firewall of proxy server, die de gateway van verbindende tooData Factory tooauthenticate zelf wordt geblokkeerd. Raadpleeg tooprevious sectie tooensure uw firewall en proxy-server correct zijn geconfigureerd.

1. Wanneer u tooregister Hallo gateway probeert, krijgt u Hallo volgende fout: "is mislukt voor tooregister hello gatewaycode. Voordat u opnieuw probeert tooregister hello gatewaycode, bevestig Hallo data management gateway verbonden is en Hallo Data Management Gateway Host Service wordt gestart."
2. Wanneer u Configuration Manager opent, ziet u status als 'Verbinding verbroken' of "Verbinden." Tijdens het weergeven van Windows-gebeurtenislogboeken onder 'Logboeken' > 'Toepassingen en Services Logs' > 'Data Management Gateway', ziet u foutberichten zoals Hallo volgende fout:`Unable tooconnect toohello remote server`
   `A component of Data Management Gateway has become unresponsive and restarts automatically. Component name: Gateway.`

### <a name="open-port-8050-for-credential-encryption"></a>Open poort 8050 voor referentieversleuteling.
Hallo **instelling referenties** toepassing gebruikt de binnenkomende poort Hallo **8050** toorelay referenties toohello gateway bij het instellen van een on-premises gekoppelde service in hello Azure-portal. Tijdens de installatie van de gateway wordt standaard gateway-installatie Hallo geopend op Hallo gateway-apparaat.

Als u een firewall van derden gebruikt, kunt u handmatig Hallo poort 8050 openen. Als u in de firewallprobleem tijdens de gatewayinstallatie uitvoert, kunt u proberen met behulp van Hallo opdracht tooinstall Hallo gateway volgen zonder het Hallo-firewall configureren.

    msiexec /q /i DataManagementGateway.msi NOFIREWALL=1

Als u ervoor geen tooopen Hallo poort 8050 op de gatewaycomputer hello kiest, gebruikgemaakt van mechanismen dan Hallo **instelling referenties** tooconfigure toepassingsgegevens referenties opgeslagen. U kunt bijvoorbeeld [nieuw AzureRmDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) PowerShell-cmdlet. Zie [instelling referenties en beveiliging](#set-credentials-and-securityy) sectie op hoe de referenties voor het opslaan van gegevens kan worden ingesteld.

## <a name="update"></a>Update
Data management gateway wordt standaard automatisch bijgewerkt wanneer een nieuwere versie van Hallo gateway beschikbaar is. Hallo-gateway is niet bijgewerkt totdat alle Hallo geplande taken worden uitgevoerd. Er is geen verdere taken worden verwerkt door Hallo gateway totdat Hallo update-bewerking is voltooid. Als Hallo-update mislukt, gateway teruggedraaid toohello oude versie.

U ziet Hallo geplande updatetijd in Hallo plaatsen te volgen:

* Hallo gateway pagina voor cloudeigenschappen in hello Azure-portal.
* Startpagina van Hallo Data Management Gateway Configuration Manager
* Melding voor systeem-systeemvak.

Hallo tabblad Start Hallo Data Management Gateway Configuration Manager geeft Hallo updateplanning en Hallo laatste tijd Hallo gateway is geïnstalleerd/bijgewerkt.

![Updates plannen](media/data-factory-data-management-gateway/UpdateSection.png)

U kunt meteen Hallo-update geïnstalleerd of wacht op Hallo gateway toobe automatisch bijgewerkt op Hallo gepland tijdstip. Bijvoorbeeld: hello volgende afbeelding ziet u een melding weergegeven in Hallo Gateway Configuration Manager samen met de knop bijwerken Hallo u kunt klikken op tooinstall deze onmiddellijk Hallo.

![Update in DMG Configuration Manager](./media/data-factory-data-management-gateway/gateway-auto-update-config-manager.png)

melding het Hallo-bericht in het systeemvak Hallo eruit zoals in Hallo installatiekopie te volgen:

![Systeemvak systeembericht](./media/data-factory-data-management-gateway/gateway-auto-update-tray-message.png)

Hallo-status van update-bewerking (handmatig of automatisch) in het systeemvak Hallo weergegeven. Wanneer u Gateway Configuration Manager volgende keer start, ziet u een bericht op Hallo meldingsbalk die Hallo-gateway is bijgewerkt samen met een koppeling te[wat is er nieuw onderwerp](data-factory-gateway-release-notes.md).

### <a name="toodisableenable-auto-update-feature"></a>toodisable/enable-functie voor automatisch bijwerken
U kunt inschakelen/uitschakelen Hallo-functie voor automatisch bijwerken als volgt Hallo stappen te volgen:

[Voor één knooppunt gateway]
1. Start Windows PowerShell op Hallo gateway-apparaat.
2. Overschakelen toohello C:\Program Files\Microsoft Data Management Gateway\2.0\PowerShellScript map.
3. Voer Hallo opdracht tooturn Hallo automatisch bijwerken te volgen functie uit te schakelen.   

    ```PowerShell
    .\GatewayAutoUpdateToggle.ps1  -off
    ```
4. tooturn weer ingeschakeld:

    ```PowerShell
    .\GatewayAutoUpdateToggle.ps1  -on  
    ```
[[Voor meerdere knooppunten maximaal beschikbare en schaalbare gateway (preview)](data-factory-data-management-gateway-high-availability-scalability.md)]
1. Start Windows PowerShell op Hallo gateway-apparaat.
2. Overschakelen toohello C:\Program Files\Microsoft Data Management Gateway\2.0\PowerShellScript map.
3. Voer Hallo opdracht tooturn Hallo automatisch bijwerken te volgen functie uit te schakelen.   

    Een extra AuthKey param is vereist voor de gateway met hoge beschikbaarheid-functie (preview).
    ```PowerShell
    .\GatewayAutoUpdateToggle.ps1  -off -AuthKey <your auth key>
    ```
4. tooturn weer ingeschakeld:

    ```PowerShell
    .\GatewayAutoUpdateToggle.ps1  -on -AuthKey <your auth key> 


## Configuration Manager
Once you install hello gateway, you can launch Data Management Gateway Configuration Manager in one of hello following ways:

1. In hello **Search** window, type **Data Management Gateway** tooaccess this utility.
2. Run hello executable **ConfigManager.exe** in hello folder: **C:\Program Files\Microsoft Data Management Gateway\2.0\Shared**

### Home page
hello Home page allows you toodo hello following actions:

* View status of hello gateway (connected toohello cloud service etc.).
* **Register** using a key from hello portal.
* **Stop** and start hello **Data Management Gateway Host service** on hello gateway machine.
* **Schedule updates** at a specific time of hello days.
* View hello date when hello gateway was **last updated**.

### Settings page
hello Settings page allows you toodo hello following actions:

* View, change, and export **certificate** used by hello gateway. This certificate is used tooencrypt data source credentials.
* Change **HTTPS port** for hello endpoint. hello gateway opens a port for setting hello data source credentials.
* **Status** of hello endpoint
* View **SSL certificate** is used for SSL communication between portal and hello gateway tooset credentials for data sources.  

### Diagnostics page
hello Diagnostics page allows you toodo hello following actions:

* Enable verbose **logging**, view logs in event viewer, and send logs tooMicrosoft if there was a failure.
* **Test connection** tooa data source.  

### Help page
hello Help page displays hello following information:  

* Brief description of hello gateway
* Version number
* Links tooonline help, privacy statement, and license agreement.  

## Monitor gateway in hello portal
In hello Azure portal, you can view near-real time snapshot of resource utilization (CPU, memory, network(in/out), etc.) on a gateway machine.  

1. In Azure portal, navigate toohello home page for your data factory, and click **Linked services** tile. 

    ![Data factory home page](./media/data-factory-data-management-gateway/monitor-data-factory-home-page.png) 
2. Select hello **gateway** in hello **Linked services** page.

    ![Linked services page](./media/data-factory-data-management-gateway/monitor-linked-services-blade.png)
3. In hello **Gateway** page, you can see hello memory and CPU usage of hello gateway.

    ![CPU and memory usage of gateway](./media/data-factory-data-management-gateway/gateway-simple-monitoring.png) 
4. Enable **Advanced settings** toosee more details such as network usage.
    
    ![Advanced monitoring of gateway](./media/data-factory-data-management-gateway/gateway-advanced-monitoring.png)

hello following table provides descriptions of columns in hello **Gateway Nodes** list:  

Monitoring Property | Description
:------------------ | :---------- 
Name | Name of hello logical gateway and nodes associated with hello gateway. Node is an on-premises Windows machine that has hello gateway installed on it. For information on having more than one node (up toofour nodes) in a single logical gateway, see [Data Management Gateway - high availability and scalability](data-factory-data-management-gateway-high-availability-scalability.md).    
Status | Status of hello logical gateway and hello gateway nodes. Example: Online/Offline/Limited/etc. For information about these statuses, See [Gateway status](#gateway-status) section. 
Version | Shows hello version of hello logical gateway and each gateway node. hello version of hello logical gateway is determined based on version of majority of nodes in hello group. If there are nodes with different versions in hello logical gateway setup, only hello nodes with hello same version number as hello logical gateway function properly. Others are in hello limited mode and need toobe manually updated (only in case auto-update fails). 
Available memory | Available memory on a gateway node. This value is a near real-time snapshot. 
CPU utilization | CPU utilization of a gateway node. This value is a near real-time snapshot. 
Networking (In/Out) | Network utilization of a gateway node. This value is a near real-time snapshot. 
Concurrent Jobs (Running/ Limit) | Number of jobs or tasks running on each node. This value is a near real-time snapshot. Limit signifies hello maximum concurrent jobs for each node. This value is defined based on hello machine size. You can increase hello limit tooscale up concurrent job execution in advanced scenarios, where CPU/memory/network is under-utilized, but activities are timing out. This capability is also available with a single-node gateway (even when hello scalability and availability feature is not enabled).  
Role | There are two types of roles in a multi-node gateway – Dispatcher and worker. All nodes are workers, which means they can all be used tooexecute jobs. There is only one dispatcher node, which is used toopull tasks/jobs from cloud services and dispatch them toodifferent worker nodes (including itself).

In this page, you see some settings that make more sense when there are two or more nodes (scale out scenario) in hello gateway. See [Data Management Gateway - high availability and scalability](data-factory-data-management-gateway-high-availability-scalability.md) for details about setting up a multi-node gateway.

### Gateway status
hello following table provides possible statuses of a **gateway node**: 

Status  | Comments/Scenarios
:------- | :------------------
Online | Node connected tooData Factory service.
Offline | Node is offline.
Upgrading | hello node is being auto-updated.
Limited | Due tooConnectivity issue. May be due tooHTTP port 8050 issue, service bus connectivity issue, or credential sync issue. 
Inactive | Node is in a configuration different from hello configuration of other majority nodes.<br/><br/> A node can be inactive when it cannot connect tooother nodes. 


hello following table provides possible statuses of a **logical gateway**. hello gateway status depends on statuses of hello gateway nodes. 

Status | Comments
:----- | :-------
Needs Registration | No node is yet registered toothis logical gateway
Online | Gateway Nodes are online
Offline | No node in online status.
Limited | Not all nodes in this gateway are in healthy state. This status is a warning that some node might be down! <br/><br/>Could be due toocredential sync issue on dispatcher/worker node. 

## Scale up gateway
You can configure hello number of **concurrent data movement jobs** that can run on a node tooscale up hello capability of moving data between on-premises and cloud data stores. 

When hello available memory and CPU are not utilized well, but hello idle capacity is 0, you should scale up by increasing hello number of concurrent jobs that can run on a node. You may also want tooscale up when activities are timing out because hello gateway is overloaded. In hello advanced settings of a gateway node, you can increase hello maximum capacity for a node. 
  

## Troubleshooting gateway issues
See [Troubleshooting gateway issues](data-factory-troubleshoot-gateway-issues.md) article for information/tips for troubleshooting issues with using hello data management gateway.  

## Move gateway from one machine tooanother
This section provides steps for moving gateway client from one machine tooanother machine.

1. In hello portal, navigate toohello **Data Factory home page**, and click hello **Linked Services** tile.

    ![Data Gateways Link](./media/data-factory-data-management-gateway/DataGatewaysLink.png)
2. Select your gateway in hello **DATA GATEWAYS** section of hello **Linked Services** page.

    ![Linked Services page with gateway selected](./media/data-factory-data-management-gateway/LinkedServiceBladeWithGateway.png)
3. In hello **Data gateway** page, click **Download and install data gateway**.

    ![Download gateway link](./media/data-factory-data-management-gateway/DownloadGatewayLink.png)
4. In hello **Configure** page, click **Download and install data gateway**, and follow instructions tooinstall hello data gateway on hello machine.

    ![Configure page](./media/data-factory-data-management-gateway/ConfigureBlade.png)
5. Keep hello **Microsoft Data Management Gateway Configuration Manager** open.

    ![Configuration Manager](./media/data-factory-data-management-gateway/ConfigurationManager.png)    
6. In hello **Configure** page in hello portal, click **Recreate key** on hello command bar, and click **Yes** for hello warning message. Click **copy button** next tookey text that copies hello key toohello clipboard. hello gateway on hello old machine stops functioning as soon you recreate hello key.  

    ![Recreate key](./media/data-factory-data-management-gateway/RecreateKey.png)
7. Paste hello **key** into text box in hello **Register Gateway** page of hello **Data Management Gateway Configuration Manager** on your machine. (optional) Click **Show gateway key** check box toosee hello key text.

    ![Copy key and Register](./media/data-factory-data-management-gateway/CopyKeyAndRegister.png)
8. Click **Register** tooregister hello gateway with hello cloud service.
9. On hello **Settings** tab, click **Change** tooselect hello same certificate that was used with hello old gateway, enter hello **password**, and click **Finish**.

   ![Specify Certificate](./media/data-factory-data-management-gateway/SpecifyCertificate.png)

   You can export a certificate from hello old gateway by doing hello following steps: launch Data Management Gateway Configuration Manager on hello old machine, switch toohello **Certificate** tab, click **Export** button and follow hello instructions.
10. After successful registration of hello gateway, you should see hello **Registration** set too**Registered** and **Status** set too**Started** on hello Home page of hello Gateway Configuration Manager.

## Encrypting credentials
tooencrypt credentials in hello Data Factory Editor, do hello following steps:

1. Launch web browser on hello **gateway machine**, navigate too[Azure portal](http://portal.azure.com). Search for your data factory if needed, open data factory in hello **DATA FACTORY** page and then click **Author & Deploy** toolaunch Data Factory Editor.   
2. Click an existing **linked service** in hello tree view toosee its JSON definition or create a linked service that requires a data management gateway (for example: SQL Server or Oracle).
3. In hello JSON editor, for hello **gatewayName** property, enter hello name of hello gateway.
4. Enter server name for hello **Data Source** property in hello **connectionString**.
5. Enter database name for hello **Initial Catalog** property in hello **connectionString**.    
6. Click **Encrypt** button on hello command bar that launches hello click-once **Credential Manager** application. You should see hello **Setting Credentials** dialog box.

    ![Setting credentials dialog](./media/data-factory-data-management-gateway/setting-credentials-dialog.png)
7. In hello **Setting Credentials** dialog box, do hello following steps:
   1. Select **authentication** that you want hello Data Factory service toouse tooconnect toohello database.
   2. Enter name of hello user who has access toohello database for hello **USERNAME** setting.
   3. Enter password for hello user for hello **PASSWORD** setting.  
   4. Click **OK** tooencrypt credentials and close hello dialog box.
8. You should see a **encryptedCredential** property in hello **connectionString** now.

    ```JSON
    {
        "name": "SqlServerLinkedService",
        "properties": {
            "type": "OnPremisesSqlServer",
            "description": "",
            "typeProperties": {
                "connectionString": "data source=myserver;initial catalog=mydatabase;Integrated Security=False;EncryptedCredential=eyJDb25uZWN0aW9uU3R",
                "gatewayName": "adftutorialgateway"
            }
        }
    }
    ```
Als u Hallo portal vanaf een machine die verschilt van de gatewaycomputer hello openen, moet u ervoor zorgen dat Hallo Referentiebeheer toepassing toohello gateway-apparaat verbinding kan maken. Als de toepassing hello niet kan Hallo gatewaycomputer bereiken, mag er geen u tooset referenties voor gegevensbron Hallo en tootest verbinding toohello-gegevensbron.  

Wanneer u Hallo gebruikt **instelling referenties** -toepassing hello portal versleutelt Hallo referenties met Hallo certificaat is opgegeven in Hallo **certificaat** tabblad Hallo **Gateway Configuration Manager** op Hallo gateway-apparaat.

Als u een API-gebaseerde benadering voor het versleutelen van Hallo referenties zoekt, kunt u Hallo [nieuw AzureRmDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) PowerShell cmdlet tooencrypt-referenties. Hallo-cmdlet gebruikt Hallo-certificaat-gateway die is geconfigureerd toouse tooencrypt Hallo referenties. Toevoegen van versleutelde referenties toohello **EncryptedCredential** element Hallo **connectionString** in Hallo JSON. U Hallo JSON gebruikt met Hallo [New-AzureRmDataFactoryLinkedService](https://msdn.microsoft.com/library/mt603647.aspx) cmdlet of in Hallo Data Factory-Editor.

```JSON
"connectionString": "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=True;EncryptedCredential=<encrypted credential>",
```

Er is een meer aanpak voor het instellen van referenties met behulp van de Data Factory-Editor. Als u een SQL-Server gekoppeld service met behulp van Hallo-editor en u referenties invoeren als tekst zonder opmaak, Hallo referenties zijn versleuteld met een Hallo Data Factory-service-certificaat. Het wordt Hallo-certificaat-gateway die is geconfigureerd toouse gebruikt. Tijdens deze benadering is mogelijk iets sneller in sommige gevallen, is het minder veilig. Daarom raden we aan dat u deze methode alleen voor ontwikkeling/testdoeleinden volgt.

## <a name="powershell-cmdlets"></a>PowerShell-cmdlets
Deze sectie wordt beschreven hoe toocreate en registreren van een gateway met behulp van Azure PowerShell-cmdlets.

1. Start **Azure PowerShell** in de beheerdersmodus.
2. Meld u bij tooyour Azure-account door het uitvoeren van Hallo de volgende opdracht en uw Azure-referenties in te voeren.

    ```PowerShell
    Login-AzureRmAccount
    ```
3. Gebruik Hallo **nieuw AzureRmDataFactoryGateway** cmdlet toocreate een logische gateway als volgt:

    ```PowerShell
    $MyDMG = New-AzureRmDataFactoryGateway -Name <gatewayName> -DataFactoryName <dataFactoryName> -ResourceGroupName ADF –Description <desc>
    ```
    **Van de voorbeeldopdracht en uitvoer**:

    ```
    PS C:\> $MyDMG = New-AzureRmDataFactoryGateway -Name MyGateway -DataFactoryName $df -ResourceGroupName ADF –Description “gateway for walkthrough”

    Name              : MyGateway
    Description       : gateway for walkthrough
    Version           :
    Status            : NeedRegistration
    VersionStatus     : None
    CreateTime        : 9/28/2014 10:58:22
    RegisterTime      :
    LastConnectTime   :
    ExpiryTime        :
    ProvisioningState : Succeeded
    Key               : ADF#00000000-0000-4fb8-a867-947877aef6cb@fda06d87-f446-43b1-9485-78af26b8bab0@4707262b-dc25-4fe5-881c-c8a7c3c569fe@wu#nfU4aBlq/heRyYFZ2Xt/CD+7i73PEO521Sj2AFOCmiI
    ```

1. In Azure PowerShell overschakelen toohello map: **C:\Program Files\Microsoft Data Management Gateway\2.0\PowerShellScript\**. Voer **RegisterGateway.ps1** die zijn gekoppeld aan de lokale variabele Hallo **$Key** zoals weergegeven in de volgende opdracht Hallo. Dit script registreert Hallo-clientagent is geïnstalleerd op uw computer met Hallo logische gateway die u eerder hebt gemaakt.

    ```PowerShell
    PS C:\> .\RegisterGateway.ps1 $MyDMG.Key
    ```
    ```
    Agent registration is successful!
    ```
    Hallo-gateway op een externe computer kunt u met behulp van Hallo IsRegisterOnRemoteMachine parameter registreren. Voorbeeld:

    ```PowerShell
    .\RegisterGateway.ps1 $MyDMG.Key -IsRegisterOnRemoteMachine true
    ```
2. U kunt Hallo **Get-AzureRmDataFactoryGateway** cmdlet tooget Hallo lijst met Gateways in uw gegevensfactory. Wanneer Hallo **Status** toont **online**, betekent dit uw gateway is klaar toouse.

    ```PowerShell        
    Get-AzureRmDataFactoryGateway -DataFactoryName <dataFactoryName> -ResourceGroupName ADF
    ```
Kunt u een gateway met behulp van Hallo **verwijderen AzureRmDataFactoryGateway** cmdlet en update beschrijving voor een gateway met behulp van Hallo **Set AzureRmDataFactoryGateway** cmdlets. Zie voor de syntaxis en andere details over deze cmdlets Data Factory Cmdlet Reference.  

### <a name="list-gateways-using-powershell"></a>Lijst met gateways met behulp van PowerShell

```PowerShell
Get-AzureRmDataFactoryGateway -DataFactoryName jasoncopyusingstoredprocedure -ResourceGroupName ADF_ResourceGroup
```

### <a name="remove-gateway-using-powershell"></a>Verwijderen van de gateway met PowerShell

```PowerShell
Remove-AzureRmDataFactoryGateway -Name JasonHDMG_byPSRemote -ResourceGroupName ADF_ResourceGroup -DataFactoryName jasoncopyusingstoredprocedure -Force
```


## <a name="next-steps"></a>Volgende stappen
* Zie [gegevens verplaatsen tussen on-premises en cloud gegevensarchieven](data-factory-move-data-between-onprem-and-cloud.md) artikel. In het Hallo-scenario maakt u een pijplijn die Hallo gateway toomove gegevens uit een lokale SQL Server-database tooan Azure-blob gebruikt.  

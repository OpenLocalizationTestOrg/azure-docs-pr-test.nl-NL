---
title: Data Management Gateway voor Data Factory | Microsoft Docs
description: Stel een gegevensgateway in om gegevens te verplaatsen tussen on-premises en de cloud. Gebruik Data Management Gateway in Azure Data Factory om uw gegevens te verplaatsen.
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
ms.openlocfilehash: 9e40eba285aeb1cce6b77311d1b69a6b96967a0b
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="data-management-gateway"></a>Gegevensbeheergateway
Data management gateway is een clientagent waarmee u in uw on-premises omgeving installeren moet kopiëren van gegevens tussen cloud en on-premises gegevensopslagexemplaren. De on-premises gegevens opslaat die worden ondersteund door Data Factory worden vermeld in de [ondersteunde gegevensbronnen](data-factory-data-movement-activities.md#supported-data-stores-and-formats) sectie.

In dit artikel is een aanvulling op de procedures in de [gegevens verplaatsen tussen on-premises en cloud gegevensarchieven](data-factory-move-data-between-onprem-and-cloud.md) artikel. In de procedure maakt u een pijplijn die de gateway gebruikt om gegevens te verplaatsen van een on-premises SQL Server database naar een Azure-blob. Dit artikel bevat gedetailleerde informatie over het data management gateway. 

U kunt een data management gateway uitbreiden door meerdere lokale computers koppelen aan de gateway. U kunt schalen omhoog door het aantal data movement taken die kunnen tegelijkertijd worden uitgevoerd op een knooppunt te verhogen. Deze functie is ook beschikbaar voor een logische gateway met één knooppunt. Zie [schaal data management gateway in Azure Data Factory](data-factory-data-management-gateway-high-availability-scalability.md) artikel voor meer informatie.

> [!NOTE]
> Gateway ondersteunt momenteel alleen de kopieeractiviteit en de activiteit opgeslagen procedure in de Data Factory. Het is niet mogelijk is op de gateway van een aangepaste activiteit voor toegang tot on-premises gegevensbronnen.      

## <a name="overview"></a>Overzicht
### <a name="capabilities-of-data-management-gateway"></a>Mogelijkheden van data management gateway
Data management gateway biedt de volgende mogelijkheden:

* On-premises gegevensbronnen model en cloud gegevensbronnen binnen de dezelfde gegevensfactory en gegevens te verplaatsen.
* Een door één venster voor bewaking en beheer inzicht in de gateway de status van de Data Factory-pagina hebben.
* Toegang tot on-premises gegevensbronnen veilig beheren.
  * Er zijn geen wijzigingen vereist voor de firewall van het bedrijf. Gateway alleen uitgaande HTTP-gebaseerde verbindingen maakt met internet te openen.
  * Referenties voor uw on-premises gegevensopslagexemplaren met uw certificaat niet versleutelen.
* Gegevens efficiënt te verplaatsen: de gegevens worden overgedragen parallel flexibel omgaan met onregelmatige netwerkproblemen met automatisch Pogingslogica.

### <a name="command-flow-and-data-flow"></a>Opdracht stroom en de gegevensstroom
Wanneer u een kopieeractiviteit om gegevens tussen on-premises en cloud te kopiëren, de activiteit maakt gebruik van een gateway voor gegevensoverdracht van on-premises gegevensbron naar de cloud en vice versa.

Hier is de gegevensstroom op hoog niveau voor en overzicht van stappen voor het kopiëren met gegevensgateway: ![gegevensstroom met gateway](./media/data-factory-data-management-gateway/data-flow-using-gateway.png)

1. Gegevens ontwikkelaars een gateway maakt voor een Azure Data Factory met behulp van de [Azure-portal](https://portal.azure.com) of [PowerShell-Cmdlet](https://msdn.microsoft.com/library/dn820234.aspx).
2. Een gekoppelde service voor een on-premises gegevensopslag gegevens developer gemaakt door te geven van de gateway. Als onderdeel van het instellen van de gekoppelde service gebruikt gegevens ontwikkelaar de instelling referenties toepassing verificatietypen en referenties op te geven.  Het dialoogvenster instelling referenties toepassing communiceert met de gegevensopslag voor het testen van verbinding en de gateway naar de referenties op te slaan.
3. Gateway versleutelt de referenties met het certificaat dat is gekoppeld aan de gateway (opgegeven door de ontwikkelaar gegevens), voordat de referenties worden opgeslagen in de cloud.
4. Data Factory-service communiceert met de gateway voor planning en beheer van taken via een besturingskanaal die gebruikmaakt van een gedeelde Azure service bus-wachtrij. Wanneer een taak kopiëren activiteit worden gestart moet, wachtrijen Data Factory de aanvraag samen met de referentie-informatie. Gateway is serversysteemstatus van de taak na polling van de wachtrij.
5. De gateway, ontsleutelt de referenties met hetzelfde certificaat en maakt vervolgens verbinding met het lokale gegevensarchief met de juiste authenticatietype en referenties.
6. De gateway kopiëren bij een winkel lokale gegevens naar een cloudopslag of omgekeerd, afhankelijk van hoe de kopieerbewerking is geconfigureerd in de pijplijn gegevens. Voor deze stap worden de gateway rechtstreeks communiceert met de opslag op basis van een cloud-services zoals Azure Blob Storage via een beveiligd kanaal voor (HTTPS).

### <a name="considerations-for-using-gateway"></a>Overwegingen voor het gebruik van gateway
* Één exemplaar van data management gateway kan worden gebruikt voor meerdere on-premises-gegevensbronnen. Echter, **één gatewayexemplaar is gekoppeld aan slechts één Azure data factory** en kan niet worden gedeeld met een andere data factory.
* U kunt hebben **slechts één exemplaar van data management gateway** geïnstalleerd op een enkele computer. Stel dat u hebt twee gegevensfactory's die toegang moeten krijgen tot on-premises gegevensbronnen, moet u om gateways te installeren op twee lokale computers. Met andere woorden, is een gateway gekoppeld aan een specifieke gegevensfactory
* De **gateway niet hoeft te worden op dezelfde computer als de gegevensbron**. Echter minder dichter gateway met de gegevensbron met tijd voor de gateway verbinding maken met de gegevensbron. Het is raadzaam dat u de gateway installeren op een machine die verschilt van de naam die als host fungeert voor on-premises gegevensbron. Wanneer de gateway en de gegevensbron zich op verschillende computers bevinden, de gateway niet zou concurreren voor bronnen met de gegevensbron.
* U kunt hebben **meerdere gateways op verschillende computers verbinding maken met dezelfde lokale gegevensbron**. Bijvoorbeeld wellicht hebt u twee gateways voor de twee data Factory, maar dezelfde lokale gegevensbron is geregistreerd bij de gegevensfactory.
* Als u al een gateway geïnstalleerd op uw computer voor een **Power BI** scenario installeert een **afzonderlijke gateway voor Azure Data Factory** op een andere computer.
* Gateway moet worden gebruikt, zelfs wanneer u **ExpressRoute**.
* Uw gegevensbron behandelen als een lokale gegevensbron (die zich achter een firewall) zelfs als u werkt met **ExpressRoute**. De gateway gebruiken om verbinding tussen de service en de gegevensbron te maken.
* U moet **gebruik van de gateway** zelfs als het gegevensarchief is in de cloud op een **Azure IaaS VM**.

## <a name="installation"></a>Installeren
### <a name="prerequisites"></a>Vereisten
* De ondersteunde **besturingssysteem** versies zijn Windows 7, Windows 8/8.1, Windows 10, Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2. Installatie van data management gateway op een domeincontroller is momenteel niet ondersteund.
* .NET framework 4.5.1 of hoger is vereist. Als u gateway op een computer met Windows 7 installeert, installeert u .NET Framework 4.5 of hoger. Zie [.NET Framework-systeemvereisten](https://msdn.microsoft.com/library/8z6watww.aspx) voor meer informatie.
* De aanbevolen **configuratie** voor de gateway machine ten minste 2 GHz, 4 kernen, 8 GB RAM-geheugen en schijf 80 GB is.
* Als de hostmachine in de slaapstand, reageert de gateway niet op gegevensaanvragen. Configureer daarom een geschikte **energiebeheerschema** op de computer voordat de gateway is geïnstalleerd. Als de machine is geconfigureerd voor de sluimerstand, wordt een bericht gevraagd in de installatie van de gateway.
* U moet een beheerder op de computer installeren en configureren van de data management gateway is. U kunt extra gebruikers toevoegen aan de **data management gateway gebruikers** lokale Windows-groep. De leden van deze groep kunnen gebruiken om zich de **Data Management Gateway Configuration Manager** hulpprogramma om de gateway te configureren.

Als kopie activiteiten bij uitvoering op een specifieke frequentie gebeuren, volgt het brongebruik (CPU, geheugen) op de machine ook hetzelfde patroon met piek- en niet-actieve tijd. Resourcegebruik ook afhankelijk van geheugenlatentie de hoeveelheid gegevens worden verplaatst. Als meerdere kopie taken uitgevoerd worden, ziet u Resourcegebruik tijdens piektijden omhoog gaan.

### <a name="installation-options"></a>Opties voor de installatie
Data management gateway kan worden geïnstalleerd op de volgende manieren:

* Downloaden van een MSI-installatiepakket van de [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=39717).  Het MSI-bestand kan ook worden gebruikt om te upgraden van bestaande data management gateway naar de nieuwste versie met alle instellingen behouden.
* Door te klikken op **downloaden en installeren van de gegevensgateway** koppeling onder handmatige installatie of **rechtstreeks op deze computer installeren** onder snelle installatie. Zie [gegevens verplaatsen tussen on-premises en cloud](data-factory-move-data-between-onprem-and-cloud.md) artikel voor stapsgewijze instructies over het gebruik van de snelle installatie. De handmatige stap gaat u naar het download center.  De instructies voor het downloaden en installeren van de gateway van Downloadcentrum zijn in de volgende sectie.

### <a name="installation-best-practices"></a>Best practices voor installatie:
1. Energiebeheerschema op de hostcomputer voor de gateway zodanig configureren dat de machine sluimerstand niet. Als de hostmachine in de slaapstand, reageert de gateway niet op gegevensaanvragen.
2. Back-up van het certificaat dat hoort bij de gateway.

### <a name="install-the-gateway-from-download-center"></a>Installeer de gateway van Downloadcentrum
1. Navigeer naar [Microsoft Data Management Gateway-downloadpagina](https://www.microsoft.com/download/details.aspx?id=39717).
2. Klik op **downloaden**, selecteer de juiste versie (**32-bits** vs. **64-bits**), en klik op **volgende**.
3. Voer de **MSI** rechtstreeks of sla het op uw harde schijf en uitvoeren.
4. Op de **Welkom** pagina een **taal** klikt u op **volgende**.
5. **Accepteer** de gebruiksrechtovereenkomst en klik op **volgende**.
6. Selecteer **map** installeren van de gateway en klikt u op **volgende**.
7. Op de **gereed voor installatie** pagina, klikt u op **installeren**.
8. Klik op **voltooien** om installatie te voltooien.
9. De sleutel ophalen van de Azure-portal. Zie de volgende sectie voor stapsgewijze instructies.
10. Op de **gateway registreren** pagina van **Data Management Gateway Configuration Manager** op uw computer de volgende stappen uitvoeren:
    1. De sleutel in de tekst te plakken.
    2. Klik desgewenst op **gatewaycode weergeven** om te zien van de belangrijkste tekst.
    3. Klik op **registreren**.

### <a name="register-gateway-using-key"></a>Registreer gateway met sleutel
#### <a name="if-you-havent-already-created-a-logical-gateway-in-the-portal"></a>Als u een logische gateway al hebt gemaakt in de portal
Als u wilt maken van een gateway in de portal en de sleutel van de **configureren** pagina, volg de stappen van de procedures in de [gegevens verplaatsen tussen on-premises en cloud](data-factory-move-data-between-onprem-and-cloud.md) artikel.    

#### <a name="if-you-have-already-created-the-logical-gateway-in-the-portal"></a>Als u de logische gateway al hebt gemaakt in de portal
1. Navigeer in Azure portal naar de **Data Factory** pagina en klik op **gekoppelde Services** tegel.

    ![Data Factory-pagina](media/data-factory-data-management-gateway/data-factory-blade.png)
2. In de **gekoppelde Services** pagina, selecteert u de logische **gateway** in de portal worden gemaakt.

    ![logische gateway](media/data-factory-data-management-gateway/data-factory-select-gateway.png)  
3. In de **Data Gateway** pagina, klikt u op **downloaden en installeren van de gegevensgateway**.

    ![Download de koppeling in de portal](media/data-factory-data-management-gateway/download-and-install-link-on-portal.png)   
4. In de **configureren** pagina, klikt u op **Maak sleutel**. Klik op Ja in het waarschuwingsbericht staan aangegeven na het lezen van deze zorgvuldig.

    ![Sleutel opnieuw maken](media/data-factory-data-management-gateway/recreate-key-button.png)
5. Klik op de knop kopiëren naast de sleutel. De sleutel wordt gekopieerd naar het Klembord.

    ![Kopieer sleutel](media/data-factory-data-management-gateway/copy-gateway-key.png)

### <a name="system-tray-icons-notifications"></a>Pictogrammen in systeemvak / meldingen
De volgende afbeelding ziet u enkele van de pictogrammen in systeemvak die u ziet.

![pictogrammen in systeemvak](./media/data-factory-data-management-gateway/gateway-tray-icons.png)

Als u de cursor op het systeem/Meldingsbericht voor een pictogram systeemvak plaatst, ziet u details over de status van de gateway updatebewerking in een pop-upvenster.

### <a name="ports-and-firewall"></a>Poorten en firewall
Er zijn twee firewalls, moet u rekening houden: **bedrijfsfirewall** uitgevoerd op de centrale router van de organisatie en **Windows firewall** geconfigureerd als een daemon op de lokale computer waarop de gateway is geïnstalleerd.  

![firewalls](./media/data-factory-data-management-gateway/firewalls2.png)

Op het niveau van de firewall van het bedrijf, moet u de volgende domeinen en uitgaande poorten configureren:

| Domeinnamen | Poorten | Beschrijving |
| --- | --- | --- |
| *. servicebus.windows.net |443, 80 |Gebruikt voor communicatie met Data Movement Service back-end |
| *. core.windows.net |443 |Gebruikt voor de tijdelijke kopie met behulp van Azure-Blob (indien geconfigureerd)|
| *. frontend.clouddatahub.net |443 |Gebruikt voor communicatie met Data Movement Service back-end |


Deze uitgaande poorten zijn normaal gesproken op niveau van Windows firewall is ingeschakeld. Als u niet het geval is, kunt u de domeinen en poorten dienovereenkomstig op gateway-apparaat.

> [!NOTE]
> 1. Op basis van de bron / put u wellicht aanvullende domeinen van goedgekeurde IP-adressen en uitgaande poorten in uw zakelijke/Windows firewall.
> 2. Voor sommige Databases van de Cloud (bijvoorbeeld: [Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-configure-firewall-settings), [Azure Data Lake](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-secure-data#set-ip-address-range-for-data-access), enzovoort), mogelijk moet u geaccepteerde IP-adres van de computer met de Gateway op de firewallconfiguratie.
>
>


#### <a name="copy-data-from-a-source-data-store-to-a-sink-data-store"></a>Gegevens kopiëren van een brongegevensarchief naar een gegevensarchief sink
Zorg ervoor dat de firewallregels correct zijn ingeschakeld op de firewall van het bedrijf, Windows firewall op de gatewaycomputer en opslaan van de gegevens zelf. Inschakelen van deze regels kunt de gateway verbinding maken met zowel bron en sink is. Schakel regels voor elke gegevensopslag die bij de kopieerbewerking betrokken is.

Bijvoorbeeld: voor het kopiëren van **een on-premises gegevensopslag een sink Azure SQL Database of een Azure SQL Data Warehouse sink**, moet u de volgende stappen uitvoeren:

* Uitgaand verkeer toestaan **TCP** -communicatie op poort **1433** voor Windows firewall- en firewall van het bedrijf.
* Configureer de firewallinstellingen van Azure SQL-server om toe te voegen van de IP-adres van het gateway-apparaat aan de lijst met toegestane IP-adressen.

> [!NOTE]
> Als uw firewall kan geen uitgaande poort 1433, Gateway kan niet rechtstreeks toegang hebben tot Azure SQL. U kunt in dit geval [kopie gefaseerde](https://docs.microsoft.com/azure/data-factory/data-factory-copy-activity-performance#staged-copy) naar Azure SQL Database / SQL Azure DW. In dit scenario zou u alleen HTTPS (poort 443) nodig voor de verplaatsing van gegevens.
>
>


### <a name="proxy-server-considerations"></a>Overwegingen voor proxy-server
Als uw zakelijke netwerkomgeving een proxyserver gebruikt voor toegang tot het internet, configureert u de data management gateway voor het gebruik van de juiste proxy-instellingen. U kunt de proxy instellen tijdens de registratie van de eerste fase.

![Set-proxy tijdens de registratie](media/data-factory-data-management-gateway/SetProxyDuringRegistration.png)

De proxyserver gateway gebruikt om verbinding met de cloudservice. Klik op **wijziging** koppeling tijdens de eerste configuratie. U ziet de **proxyinstelling** dialoogvenster.

![Set-proxy met Configuratiebeheer](media/data-factory-data-management-gateway/SetProxySettings.png)

Er zijn drie opties:

* **Gebruik geen proxy**: Gateway expliciet gebruikt geen elke proxy verbinding maken met cloudservices.
* **Gebruik system proxy**: Gateway maakt gebruik van de proxy-instelling is geconfigureerd in diahost.exe.config en diawp.exe.config.  Als geen proxy is geconfigureerd in diahost.exe.config en diawp.exe.config, gateway wordt verbonden met cloudservice rechtstreeks zonder gebruik te maken via proxy.
* **Aangepaste proxy gebruikt**: de HTTP-proxy-instellingen te gebruiken voor de gateway in plaats van configuraties in diahost.exe.config en diawp.exe.config configureren.  Adres en poort zijn vereist.  Gebruikersnaam en wachtwoord zijn optioneel, afhankelijk van uw proxyserver verificatie-instelling.  Alle instellingen zijn versleuteld met de referenties van het certificaat van de gateway en die lokaal zijn opgeslagen op de hostcomputer van de gateway.

Data management gateway Host Service wordt automatisch opnieuw opgestart nadat u de bijgewerkte proxy-instellingen opslaan.

Nadat de gateway is geregistreerd, als u wilt weergeven of bijwerken van proxy-instellingen, gebruikt u Data Management Gateway Configuration Manager.

1. Start **Data Management Gateway Configuration Manager**.
2. Overschakelen naar de **instellingen** tabblad.
3. Klik op **wijziging** koppelen **HTTP-Proxy** sectie starten de **Set HTTP-Proxy** dialoogvenster.  
4. Nadat u op de **volgende** knop klikt, ziet u een waarschuwingsdialoogvenster waarin wordt gevraagd uw toestemming voor het opslaan van de proxy-instelling en start de Gateway-hostservice opnieuw op.

U kunt weergeven en bijwerken van HTTP-proxy met behulp van Configuration Manager-hulpprogramma.

![Set-proxy met Configuratiebeheer](media/data-factory-data-management-gateway/SetProxyConfigManager.png)

> [!NOTE]
> Als u een proxyserver met NTLM-verificatie hebt ingesteld, is Gateway Host Service wordt uitgevoerd onder het domeinaccount. Als u het wachtwoord voor het domeinaccount later wijzigt, moet u configuratie-instellingen voor de service bijwerken en dienovereenkomstig aan het programma opnieuw. Vanwege deze vereiste raden we dat u een specifiek domeinaccount gebruiken voor toegang tot de proxyserver die vereist niet dat u het wachtwoord regelmatig bijwerken.
>
>

### <a name="configure-proxy-server-settings"></a>Proxyserverinstellingen configureren
Als u selecteert **system proxy gebruiken** instellen voor de HTTP-proxy, gateway maakt gebruik van de proxy-instelling in diahost.exe.config en diawp.exe.config.  Als er geen proxyserver is opgegeven in diahost.exe.config en diawp.exe.config, gateway wordt verbonden met cloudservice rechtstreeks zonder gebruik te maken via proxy. De volgende procedure bevat instructies voor het bijwerken van het bestand diahost.exe.config.  

1. Maak een veilige kopie van C:\Program Files\Microsoft Data Management Gateway\2.0\Shared\diahost.exe.config back-up van het oorspronkelijke bestand in Verkenner.
2. Starten van Notepad.exe uitgevoerd als administrator en open tekstbestand "C:\Program Files\Microsoft Data Management Gateway\2.0\Shared\diahost.exe.config. U kunt het standaardlabel voor system.net vinden zoals weergegeven in de volgende code:

         <system.net>
             <defaultProxy useDefaultCredentials="true" />
         </system.net>    

   Vervolgens kunt u proxy-servergegevens toevoegen, zoals wordt weergegeven in het volgende voorbeeld:

         <system.net>
               <defaultProxy enabled="true">
                     <proxy bypassonlocal="true" proxyaddress="http://proxy.domain.org:8888/" />
               </defaultProxy>
         </system.net>

   Aanvullende eigenschappen zijn toegestaan in de tag proxy om op te geven van de vereiste instellingen zoals scriptLocation. Raadpleeg [proxy Element (netwerkinstellingen)](https://msdn.microsoft.com/library/sa91de1e.aspx) op syntaxis.

         <proxy autoDetect="true|false|unspecified" bypassonlocal="true|false|unspecified" proxyaddress="uriString" scriptLocation="uriString" usesystemdefault="true|false|unspecified "/>
3. Start de Data Management Gateway Host service, die de wijzigingen neemt vervolgens het configuratiebestand in de oorspronkelijke locatie op te slaan. De service te starten: Gebruik de applet services in het Configuratiescherm, of vanuit de **Data Management Gateway Configuration Manager** > Klik op de **Service stoppen** knop en klik vervolgens op de **Service starten**. Als de service niet wordt gestart, is het waarschijnlijk dat er een onjuiste syntaxis van de XML-label is toegevoegd in het toepassingsconfiguratiebestand die is bewerkt.

> [!IMPORTANT]
> Vergeet niet om bij te werken **beide** diahost.exe.config en diawp.exe.config.  


Naast deze punten moet u ook om te controleren of Microsoft Azure in goedgekeurde lijst van uw bedrijf. De lijst met geldige Microsoft Azure-IP-adressen kan worden gedownload vanuit de [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=41653).

#### <a name="possible-symptoms-for-firewall-and-proxy-server-related-issues"></a>Mogelijke problemen voor firewall en proxy server-problemen
Als u fouten overeen met de volgende procedures optreden, is het waarschijnlijk door onjuiste configuratie van de firewall of proxyserver server gateway verbinding maken met de Data Factory blokkeert zichzelf verifiëren. Raadpleeg de vorige sectie om te controleren of uw firewall en proxy-server correct zijn geconfigureerd.

1. Wanneer u probeert om de gateway te registreren, wordt de volgende fout: 'kan niet de gatewaycode registreren. Voordat u probeert de gatewaycode opnieuw registreren, Controleer of de data management gateway verbonden is en Data Management Gateway Host Service wordt gestart."
2. Wanneer u Configuration Manager opent, ziet u status als 'Verbinding verbroken' of "Verbinden." Tijdens het weergeven van Windows-gebeurtenislogboeken onder 'Logboeken' > 'Toepassingen en Services Logs' > 'Data Management Gateway', ziet u foutberichten, zoals de volgende fout:`Unable to connect to the remote server`
   `A component of Data Management Gateway has become unresponsive and restarts automatically. Component name: Gateway.`

### <a name="open-port-8050-for-credential-encryption"></a>Open poort 8050 voor referentieversleuteling.
De **instelling referenties** toepassing gebruikmaakt van de binnenkomende poort **8050** relay referenties naar de gateway bij het instellen van een lokaal gekoppelde service in de Azure-portal. Tijdens de installatie van de gateway wordt standaard de installatie van de gateway geopend op de gateway-apparaat.

Als u een firewall van derden gebruikt, kunt u handmatig de poort 8050 openen. Als u in de firewallprobleem tijdens de gatewayinstallatie uitvoert, kunt u proberen met de volgende opdracht voor het installeren van de gateway zonder het configureren van de firewall.

    msiexec /q /i DataManagementGateway.msi NOFIREWALL=1

Als u niet de poort te openen 8050 op de gatewaycomputer, gebruikgemaakt van mechanismen dan met behulp van de **instelling referenties** toepassing voor het configureren van referenties voor gegevensopslag. U kunt bijvoorbeeld [nieuw AzureRmDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) PowerShell-cmdlet. Zie [instelling referenties en beveiliging](#set-credentials-and-securityy) sectie op hoe de referenties voor het opslaan van gegevens kan worden ingesteld.

## <a name="update"></a>Update
Data management gateway wordt standaard automatisch bijgewerkt wanneer een nieuwere versie van de gateway beschikbaar is. De gateway is niet bijgewerkt tot de geplande taken kunt uitvoeren. Geen verdere taken worden verwerkt door de gateway, totdat de updatebewerking is voltooid. Als de update is mislukt, is gateway teruggedraaid naar de oude versie.

De geplande updatetijd ziet u in de volgende locaties:

* De eigenschappenpagina van de gateway in de Azure portal.
* Startpagina van de Data Management Gateway Configuration Manager
* Melding voor systeem-systeemvak.

Het tabblad Start van de Data Management Gateway Configuration Manager geeft de updateplanning en de laatste keer dat de gateway is geïnstalleerd/bijgewerkt.

![Updates plannen](media/data-factory-data-management-gateway/UpdateSection.png)

U kunt de update onmiddellijk te installeren of wacht u totdat de gateway worden automatisch bijgewerkt op het geplande tijdstip. Bijvoorbeeld de volgende afbeelding ziet u de melding wordt weergegeven in de Gateway Configuration Manager samen met de knop bijwerken waarop u klikken kunt om onmiddellijk te installeren.

![Update in DMG Configuration Manager](./media/data-factory-data-management-gateway/gateway-auto-update-config-manager.png)

Het meldingsbericht in het systeemvak eruit zoals weergegeven in de volgende afbeelding:

![Systeemvak systeembericht](./media/data-factory-data-management-gateway/gateway-auto-update-tray-message.png)

U ziet de status van updatebewerking (handmatig of automatisch) in het systeemvak. Als u Gateway Configuration Manager volgende keer start, ziet u een bericht op de meldingsbalk dat samen met een koppeling naar de gateway is bijgewerkt [wat is er nieuw onderwerp](data-factory-gateway-release-notes.md).

### <a name="to-disableenable-auto-update-feature"></a>Aan de functie voor automatisch bijwerken inschakelen/uitschakelen
U kunt inschakelen/uitschakelen de functie voor automatisch bijwerken door de volgende stappen uit te voeren:

[Voor één knooppunt gateway]
1. Start Windows PowerShell op de gateway-apparaat.
2. Ga naar de map C:\Program Files\Microsoft Data Management Gateway\2.0\PowerShellScript.
3. Voer de volgende opdracht om de automatische updates inschakelen functie uit te schakelen.   

    ```PowerShell
    .\GatewayAutoUpdateToggle.ps1  -off
    ```
4. Aan deze weer inschakelen:

    ```PowerShell
    .\GatewayAutoUpdateToggle.ps1  -on  
    ```
[[Voor meerdere knooppunten maximaal beschikbare en schaalbare gateway (preview)](data-factory-data-management-gateway-high-availability-scalability.md)]
1. Start Windows PowerShell op de gateway-apparaat.
2. Ga naar de map C:\Program Files\Microsoft Data Management Gateway\2.0\PowerShellScript.
3. Voer de volgende opdracht om de automatische updates inschakelen functie uit te schakelen.   

    Een extra AuthKey param is vereist voor de gateway met hoge beschikbaarheid-functie (preview).
    ```PowerShell
    .\GatewayAutoUpdateToggle.ps1  -off -AuthKey <your auth key>
    ```
4. Aan deze weer inschakelen:

    ```PowerShell
    .\GatewayAutoUpdateToggle.ps1  -on -AuthKey <your auth key> 


## Configuration Manager
Once you install the gateway, you can launch Data Management Gateway Configuration Manager in one of the following ways:

1. In the **Search** window, type **Data Management Gateway** to access this utility.
2. Run the executable **ConfigManager.exe** in the folder: **C:\Program Files\Microsoft Data Management Gateway\2.0\Shared**

### Home page
The Home page allows you to do the following actions:

* View status of the gateway (connected to the cloud service etc.).
* **Register** using a key from the portal.
* **Stop** and start the **Data Management Gateway Host service** on the gateway machine.
* **Schedule updates** at a specific time of the days.
* View the date when the gateway was **last updated**.

### Settings page
The Settings page allows you to do the following actions:

* View, change, and export **certificate** used by the gateway. This certificate is used to encrypt data source credentials.
* Change **HTTPS port** for the endpoint. The gateway opens a port for setting the data source credentials.
* **Status** of the endpoint
* View **SSL certificate** is used for SSL communication between portal and the gateway to set credentials for data sources.  

### Diagnostics page
The Diagnostics page allows you to do the following actions:

* Enable verbose **logging**, view logs in event viewer, and send logs to Microsoft if there was a failure.
* **Test connection** to a data source.  

### Help page
The Help page displays the following information:  

* Brief description of the gateway
* Version number
* Links to online help, privacy statement, and license agreement.  

## Monitor gateway in the portal
In the Azure portal, you can view near-real time snapshot of resource utilization (CPU, memory, network(in/out), etc.) on a gateway machine.  

1. In Azure portal, navigate to the home page for your data factory, and click **Linked services** tile. 

    ![Data factory home page](./media/data-factory-data-management-gateway/monitor-data-factory-home-page.png) 
2. Select the **gateway** in the **Linked services** page.

    ![Linked services page](./media/data-factory-data-management-gateway/monitor-linked-services-blade.png)
3. In the **Gateway** page, you can see the memory and CPU usage of the gateway.

    ![CPU and memory usage of gateway](./media/data-factory-data-management-gateway/gateway-simple-monitoring.png) 
4. Enable **Advanced settings** to see more details such as network usage.
    
    ![Advanced monitoring of gateway](./media/data-factory-data-management-gateway/gateway-advanced-monitoring.png)

The following table provides descriptions of columns in the **Gateway Nodes** list:  

Monitoring Property | Description
:------------------ | :---------- 
Name | Name of the logical gateway and nodes associated with the gateway. Node is an on-premises Windows machine that has the gateway installed on it. For information on having more than one node (up to four nodes) in a single logical gateway, see [Data Management Gateway - high availability and scalability](data-factory-data-management-gateway-high-availability-scalability.md).    
Status | Status of the logical gateway and the gateway nodes. Example: Online/Offline/Limited/etc. For information about these statuses, See [Gateway status](#gateway-status) section. 
Version | Shows the version of the logical gateway and each gateway node. The version of the logical gateway is determined based on version of majority of nodes in the group. If there are nodes with different versions in the logical gateway setup, only the nodes with the same version number as the logical gateway function properly. Others are in the limited mode and need to be manually updated (only in case auto-update fails). 
Available memory | Available memory on a gateway node. This value is a near real-time snapshot. 
CPU utilization | CPU utilization of a gateway node. This value is a near real-time snapshot. 
Networking (In/Out) | Network utilization of a gateway node. This value is a near real-time snapshot. 
Concurrent Jobs (Running/ Limit) | Number of jobs or tasks running on each node. This value is a near real-time snapshot. Limit signifies the maximum concurrent jobs for each node. This value is defined based on the machine size. You can increase the limit to scale up concurrent job execution in advanced scenarios, where CPU/memory/network is under-utilized, but activities are timing out. This capability is also available with a single-node gateway (even when the scalability and availability feature is not enabled).  
Role | There are two types of roles in a multi-node gateway – Dispatcher and worker. All nodes are workers, which means they can all be used to execute jobs. There is only one dispatcher node, which is used to pull tasks/jobs from cloud services and dispatch them to different worker nodes (including itself).

In this page, you see some settings that make more sense when there are two or more nodes (scale out scenario) in the gateway. See [Data Management Gateway - high availability and scalability](data-factory-data-management-gateway-high-availability-scalability.md) for details about setting up a multi-node gateway.

### Gateway status
The following table provides possible statuses of a **gateway node**: 

Status  | Comments/Scenarios
:------- | :------------------
Online | Node connected to Data Factory service.
Offline | Node is offline.
Upgrading | The node is being auto-updated.
Limited | Due to Connectivity issue. May be due to HTTP port 8050 issue, service bus connectivity issue, or credential sync issue. 
Inactive | Node is in a configuration different from the configuration of other majority nodes.<br/><br/> A node can be inactive when it cannot connect to other nodes. 


The following table provides possible statuses of a **logical gateway**. The gateway status depends on statuses of the gateway nodes. 

Status | Comments
:----- | :-------
Needs Registration | No node is yet registered to this logical gateway
Online | Gateway Nodes are online
Offline | No node in online status.
Limited | Not all nodes in this gateway are in healthy state. This status is a warning that some node might be down! <br/><br/>Could be due to credential sync issue on dispatcher/worker node. 

## Scale up gateway
You can configure the number of **concurrent data movement jobs** that can run on a node to scale up the capability of moving data between on-premises and cloud data stores. 

When the available memory and CPU are not utilized well, but the idle capacity is 0, you should scale up by increasing the number of concurrent jobs that can run on a node. You may also want to scale up when activities are timing out because the gateway is overloaded. In the advanced settings of a gateway node, you can increase the maximum capacity for a node. 
  

## Troubleshooting gateway issues
See [Troubleshooting gateway issues](data-factory-troubleshoot-gateway-issues.md) article for information/tips for troubleshooting issues with using the data management gateway.  

## Move gateway from one machine to another
This section provides steps for moving gateway client from one machine to another machine.

1. In the portal, navigate to the **Data Factory home page**, and click the **Linked Services** tile.

    ![Data Gateways Link](./media/data-factory-data-management-gateway/DataGatewaysLink.png)
2. Select your gateway in the **DATA GATEWAYS** section of the **Linked Services** page.

    ![Linked Services page with gateway selected](./media/data-factory-data-management-gateway/LinkedServiceBladeWithGateway.png)
3. In the **Data gateway** page, click **Download and install data gateway**.

    ![Download gateway link](./media/data-factory-data-management-gateway/DownloadGatewayLink.png)
4. In the **Configure** page, click **Download and install data gateway**, and follow instructions to install the data gateway on the machine.

    ![Configure page](./media/data-factory-data-management-gateway/ConfigureBlade.png)
5. Keep the **Microsoft Data Management Gateway Configuration Manager** open.

    ![Configuration Manager](./media/data-factory-data-management-gateway/ConfigurationManager.png)    
6. In the **Configure** page in the portal, click **Recreate key** on the command bar, and click **Yes** for the warning message. Click **copy button** next to key text that copies the key to the clipboard. The gateway on the old machine stops functioning as soon you recreate the key.  

    ![Recreate key](./media/data-factory-data-management-gateway/RecreateKey.png)
7. Paste the **key** into text box in the **Register Gateway** page of the **Data Management Gateway Configuration Manager** on your machine. (optional) Click **Show gateway key** check box to see the key text.

    ![Copy key and Register](./media/data-factory-data-management-gateway/CopyKeyAndRegister.png)
8. Click **Register** to register the gateway with the cloud service.
9. On the **Settings** tab, click **Change** to select the same certificate that was used with the old gateway, enter the **password**, and click **Finish**.

   ![Specify Certificate](./media/data-factory-data-management-gateway/SpecifyCertificate.png)

   You can export a certificate from the old gateway by doing the following steps: launch Data Management Gateway Configuration Manager on the old machine, switch to the **Certificate** tab, click **Export** button and follow the instructions.
10. After successful registration of the gateway, you should see the **Registration** set to **Registered** and **Status** set to **Started** on the Home page of the Gateway Configuration Manager.

## Encrypting credentials
To encrypt credentials in the Data Factory Editor, do the following steps:

1. Launch web browser on the **gateway machine**, navigate to [Azure portal](http://portal.azure.com). Search for your data factory if needed, open data factory in the **DATA FACTORY** page and then click **Author & Deploy** to launch Data Factory Editor.   
2. Click an existing **linked service** in the tree view to see its JSON definition or create a linked service that requires a data management gateway (for example: SQL Server or Oracle).
3. In the JSON editor, for the **gatewayName** property, enter the name of the gateway.
4. Enter server name for the **Data Source** property in the **connectionString**.
5. Enter database name for the **Initial Catalog** property in the **connectionString**.    
6. Click **Encrypt** button on the command bar that launches the click-once **Credential Manager** application. You should see the **Setting Credentials** dialog box.

    ![Setting credentials dialog](./media/data-factory-data-management-gateway/setting-credentials-dialog.png)
7. In the **Setting Credentials** dialog box, do the following steps:
   1. Select **authentication** that you want the Data Factory service to use to connect to the database.
   2. Enter name of the user who has access to the database for the **USERNAME** setting.
   3. Enter password for the user for the **PASSWORD** setting.  
   4. Click **OK** to encrypt credentials and close the dialog box.
8. You should see a **encryptedCredential** property in the **connectionString** now.

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
Als u de portal vanaf een machine die verschilt van het gateway-apparaat openen, moet u ervoor zorgen dat de toepassing Referentiebeheer verbinding met de gateway-machine maken kan. Als de toepassing niet kan van het gateway-apparaat bereiken, kunt niet u referenties voor de gegevensbron in te stellen en om verbinding met de gegevensbron te testen.  

Wanneer u gebruikt de **instelling referenties** toepassing, de portal versleutelt de referenties met het certificaat dat is opgegeven in de **certificaat** tabblad van de **Gateway Configuration Manager** op de gateway-apparaat.

Als u voor een API-gebaseerde methode voor het versleutelen van de referenties op zoek bent, kunt u de [nieuw AzureRmDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) PowerShell-cmdlet om referenties te versleutelen. Het certificaat wordt gebruikt door de cmdlet die gateway is geconfigureerd om te gebruiken om de referenties te versleutelen. Toevoegen van versleutelde referenties voor de **EncryptedCredential** element van de **connectionString** in de JSON. U gebruikt de JSON met de [New-AzureRmDataFactoryLinkedService](https://msdn.microsoft.com/library/mt603647.aspx) cmdlet of in de Data Factory-Editor.

```JSON
"connectionString": "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=True;EncryptedCredential=<encrypted credential>",
```

Er is een meer aanpak voor het instellen van referenties met behulp van de Data Factory-Editor. Als u een SQL Server gekoppelde service maken met behulp van de editor en u referenties als tekst zonder opmaak invoeren, kan de referenties zijn versleuteld met behulp van een Data Factory-service-certificaat. Gebruikt het certificaat niet dat gateway is geconfigureerd voor gebruik. Tijdens deze benadering is mogelijk iets sneller in sommige gevallen, is het minder veilig. Daarom raden we aan dat u deze methode alleen voor ontwikkeling/testdoeleinden volgt.

## <a name="powershell-cmdlets"></a>PowerShell-cmdlets
Deze sectie beschrijft het maken en registreren van een gateway met behulp van Azure PowerShell-cmdlets.

1. Start **Azure PowerShell** in de beheerdersmodus.
2. Meld u aan bij uw Azure-account door de volgende opdracht uit te voeren en uw Azure-referenties in te voeren.

    ```PowerShell
    Login-AzureRmAccount
    ```
3. Gebruik de **nieuw AzureRmDataFactoryGateway** cmdlet voor het maken van een logische gateway als volgt:

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

1. Ga naar de map in Azure PowerShell: **C:\Program Files\Microsoft Data Management Gateway\2.0\PowerShellScript\**. Voer **RegisterGateway.ps1** die zijn gekoppeld aan de lokale variabele **$Key** zoals weergegeven in de volgende opdracht. Dit script registreert de clientagent is geïnstalleerd op uw computer met de logische gateway die u eerder hebt gemaakt.

    ```PowerShell
    PS C:\> .\RegisterGateway.ps1 $MyDMG.Key
    ```
    ```
    Agent registration is successful!
    ```
    U kunt de gateway op een externe computer met de parameter IsRegisterOnRemoteMachine registreren. Voorbeeld:

    ```PowerShell
    .\RegisterGateway.ps1 $MyDMG.Key -IsRegisterOnRemoteMachine true
    ```
2. U kunt de **Get-AzureRmDataFactoryGateway** cmdlet om de lijst met Gateways in uw gegevensfactory. Wanneer de **Status** toont **online**, betekent dit uw gateway is klaar voor gebruik.

    ```PowerShell        
    Get-AzureRmDataFactoryGateway -DataFactoryName <dataFactoryName> -ResourceGroupName ADF
    ```
Kunt u een gateway met de **verwijderen AzureRmDataFactoryGateway** cmdlet en update beschrijving voor een gateway met de **Set AzureRmDataFactoryGateway** cmdlets. Zie voor de syntaxis en andere details over deze cmdlets Data Factory Cmdlet Reference.  

### <a name="list-gateways-using-powershell"></a>Lijst met gateways met behulp van PowerShell

```PowerShell
Get-AzureRmDataFactoryGateway -DataFactoryName jasoncopyusingstoredprocedure -ResourceGroupName ADF_ResourceGroup
```

### <a name="remove-gateway-using-powershell"></a>Verwijderen van de gateway met PowerShell

```PowerShell
Remove-AzureRmDataFactoryGateway -Name JasonHDMG_byPSRemote -ResourceGroupName ADF_ResourceGroup -DataFactoryName jasoncopyusingstoredprocedure -Force
```


## <a name="next-steps"></a>Volgende stappen
* Zie [gegevens verplaatsen tussen on-premises en cloud gegevensarchieven](data-factory-move-data-between-onprem-and-cloud.md) artikel. In de procedure maakt u een pijplijn die de gateway gebruikt om gegevens te verplaatsen van een on-premises SQL Server database naar een Azure-blob.  

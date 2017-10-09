---
title: aaaAzure AD Connect Health-Agent-installatie | Microsoft Docs
description: Dit is Hallo Azure AD Connect Health-pagina waarop wordt beschreven installatie van de agent voor AD FS en Sync Hallo.
services: active-directory
documentationcenter: 
author: karavar
manager: samueld
editor: curtand
ms.assetid: 1cc8ae90-607d-4925-9c30-6770a4bd1b4e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 9019628ec1d4c477496e08910cfd668ed1933a62
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-health-agent-installation"></a>De Azure AD Connect Health-agent installeren
Dit document helpt u bij het installeren en configureren van hello Azure AD Connect Health-Agents. U kunt downloaden Hallo-agenten van [hier](active-directory-aadconnect-health.md#download-and-install-azure-ad-connect-health-agent).

## <a name="requirements"></a>Vereisten
Hallo volgende tabel wordt een lijst met vereisten voor het gebruik van Azure AD Connect Health.

| Vereiste | Beschrijving |
| --- | --- |
| Azure AD Premium |Azure AD Connect Health is een Azure AD Premium-functie waarvoor Azure AD Premium is vereist. </br></br>Zie voor meer informatie [Aan de slag met Azure AD Premium](../active-directory-get-started-premium.md) </br>Zie voor een gratis proefversie van 30 dagen toostart [een proefversie starten.](https://azure.microsoft.com/trial/get-started-active-directory/) |
| U moet een globale beheerder van uw Azure AD-tooget de slag met Azure AD Connect Health |Standaard kunnen alleen Hallo globale beheerders installeren en configureren Hallo health-agents tooget gestart, toegang Hallo-portal en bewerkingen uitvoeren in Azure AD Connect Health. Voor meer informatie raadpleegt u [Uw Azure AD-directory beheren](../active-directory-administer.md). <br><br> Met behulp van op rollen gebaseerd toegangsbeheer kunt u toestaan toegang tooAzure AD Connect Health tooother gebruikers in uw organisatie. Zie voor meer informatie [Op rollen gebaseerd toegangsbeheer voor Azure AD Connect Health](active-directory-aadconnect-health-operations.md#manage-access-with-role-based-access-control). </br></br>**Belangrijk:** Hallo account die wordt gebruikt voor het Hallo-agents installeren, moet een werk- of schoolaccount-account. Het mag geen Microsoft-account zijn. Voor meer informatie raadpleegt u [Als organisatie registreren voor Azure](../sign-up-organization.md) |
| De Azure AD Connect Health-agent wordt geïnstalleerd op elke doelserver | Azure AD Connect Health vereist Hallo Health-Agents toobe geïnstalleerd en geconfigureerd op de doelservers tooreceive Hallo gegevens en bieden Hallo bewaking en analytische gegevens mogelijkheden </br></br>Bijvoorbeeld: tooget gegevens van uw AD FS-infrastructuur Hallo-agent moet worden geïnstalleerd op Hallo AD FS en Webtoepassingsproxy-servers. Op deze manier tooget gegevens op uw on-premises AD DS-infrastructuur, Hallo-agent moet worden geïnstalleerd op Hallo-domeincontrollers. </br></br> |
| Uitgaande verbinding toohello Azure service-eindpunten | Hallo-agent vereist tijdens de installatie en runtime connectiviteit tooAzure AD Connect Health service-eindpunten. Als uitgaande verbinding is geblokkeerd met behulp van Firewalls, zorg ervoor dat Hallo volgende eindpunten toohello lijst met toegestane worden toegevoegd: </br></br><li>&#42;.blob.core.windows.net </li><li>&#42;.servicebus.windows.net - Poort: 5671 </li><li>&#42;.adhybridhealth.azure.com/</li><li>https://management.azure.com </li><li>https://policykeyservice.dc.ad.msft.net/</li><li>https://login.windows.net</li><li>https://login.microsoftonline.com</li><li>https://secure.aadcdn.microsoftonline-p.com</li> |
|Uitgaande verbindingen op basis van IP-adressen | Voor IP-adres op basis van toohello filteren op firewalls, Raadpleeg [Azure IP-adresbereiken](https://www.microsoft.com/en-us/download/details.aspx?id=41653).|
| SSL-controle voor uitgaand verkeer is gefilterd of uitgeschakeld | Hallo agent registratie stap of gegevens uploadbewerkingen kunnen mislukken als er SSL-inspectie of beëindiging voor uitgaand verkeer op Hallo netwerklaag. |
| Firewall-poorten op Hallo-server waarop Hallo-agent wordt uitgevoerd. |Hallo-agent vereist Hallo firewallpoorten toobe openen om Hallo agent toocommunicate met hello Azure AD Health service-eindpunten te volgen.</br></br><li>TCP-poort 443</li><li>TCP-poort 5671</li> |
| Toestaan dat Hallo websites volgen als verbeterde beveiliging van Internet Explorer is ingeschakeld |Als Verbeterde beveiliging van Internet Explorer is ingeschakeld, moet klikt u vervolgens hello volgende websites worden toegestaan op Hallo-server die momenteel toohave Hallo-agent is geïnstalleerd.</br></br><li>https://login.microsoftonline.com</li><li>https://secure.aadcdn.microsoftonline-p.com</li><li>https://login.windows.net</li><li>Hallo federation-server voor uw organisatie worden vertrouwd door Azure Active Directory. Bijvoorbeeld: https://sts.contoso.com</li> |
|FIPS uitschakelen|FIPS wordt niet ondersteund door Azure AD Connect Health-agents.|

## <a name="installing-hello-azure-ad-connect-health-agent-for-ad-fs"></a>Hello Azure AD Connect Health-Agent voor AD FS installeren
toostart Hallo installatie van de agent, dubbelklikt u op Hallo .exe-bestand dat u hebt gedownload. Klik op installeren op de eerste welkomstscherm.

![Azure AD Connect Health verifiëren](./media/active-directory-aadconnect-health-requirements/install1.png)

Zodra het Hallo-installatie is voltooid, klikt u op nu configureren.

![Azure AD Connect Health verifiëren](./media/active-directory-aadconnect-health-requirements/install2.png)

Een PowerShell-venster tooinitiate Hallo agent registratieproces wordt gestart. Wanneer u wordt gevraagd, aanmelden met een Azure AD-account dat toegang tooperform agentregistratie is. Hallo globale beheerdersaccount heeft standaard toegang.

![Azure AD Connect Health verifiëren](./media/active-directory-aadconnect-health-requirements/install3.png)

Na het aanmelden gaat PowerShell door. Zodra deze is voltooid, kunt u PowerShell sluiten en Hallo-configuratie is voltooid.

Op dit moment hello agent services moeten worden gestart automatisch waardoor Hallo agent uploaden Hallo vereist gegevens toohello cloud-service op een veilige manier.

Als u niet alle Hallo vereisten die worden beschreven in de vorige secties Hallo voldaan, worden waarschuwingen weergegeven in Hallo PowerShell-venster. Ervoor toocomplete Hallo worden [vereisten](active-directory-aadconnect-health-agent-install.md#requirements) voordat u Hallo agent installeert. Hallo volgende schermafbeelding is een voorbeeld van deze fouten.

![Azure AD Connect Health verifiëren](./media/active-directory-aadconnect-health-requirements/install4.png)

tooverify Hallo-agent is geïnstalleerd, zoek naar de volgende services op de server Hallo Hallo. Als u Hallo configuratie hebt voltooid, moeten ze al worden uitgevoerd. Anders zijn ze gestopt totdat het Hallo-configuratie is voltooid.

* Azure AD Connect Health AD FS Diagnostics-service
* Azure AD Connect Health AD FS Insights-service
* Azure AD Connect Health AD FS Monitoring-service

![Azure AD Connect Health verifiëren](./media/active-directory-aadconnect-health-requirements/install5.png)

### <a name="agent-installation-on-windows-server-2008-r2-servers"></a>De agent installeren op Windows Server 2008 R2-servers
Stappen voor Windows Server 2008 R2-servers:

1. Zorg ervoor dat Hallo-server wordt uitgevoerd met Service Pack 1 of hoger.
2. Verbeterde beveiliging van Internet Explorer uitschakelen voor de installatie van agents:
3. Installeer Windows PowerShell 4.0 op elk van de servers Hallo tevoren Hallo AD Health-agent installeren. tooinstall Windows PowerShell 4.0:
   * Installeer [Microsoft .NET Framework 4.5](https://www.microsoft.com/download/details.aspx?id=40779) met Hallo koppeling toodownload Hallo offline-installatieprogramma te volgen.
   * PowerShell ISE (van Windows-onderdelen) installeren
   * Hallo installeren [Windows Management Framework 4.0.](https://www.microsoft.com/download/details.aspx?id=40855)
   * Installeer Internet Explorer versie 10 of hoger op Hallo-server. (Vereist door Hallo Health-Service tooauthenticate, met behulp van uw Azure-beheerdersreferenties).
4. Zie voor meer informatie over het installeren van Windows PowerShell 4.0 voor Windows Server 2008 R2 Hallo wiki-artikel [hier](http://social.technet.microsoft.com/wiki/contents/articles/20623.step-by-step-upgrading-the-powershell-version-4-on-2008-r2.aspx).

### <a name="enable-auditing-for-ad-fs"></a>Controle inschakelen voor AD FS
> [!NOTE]
> Deze sectie is alleen van toepassing tooAD FS-servers. U hebt deze stappen uit op Hallo Webtoepassingsproxyservers niet toofollow.
>

Gegevens, hello Azure AD Connect Health-agent moet informatie in Hallo AD FS-auditlogboeken Hallo om Hallo gebruiksanalyse functie toogather en analyseren. Deze logboeken worden niet standaard ingeschakeld. Gebruik hello volgende procedures tooenable AD FS-controle- en toolocate Hallo AD FS controlelogboeken, op uw AD FS-servers.

#### <a name="tooenable-auditing-for-ad-fs-on-windows-server-2008-r2"></a>tooenable controles voor AD FS in Windows Server 2008 R2
1. Klik op **Start**, te verwijzen**programma's**, wijst u te**Systeembeheer**, en klik vervolgens op **lokaal beveiligingsbeleid**.
2. Navigeer toohello **beveiliging Beveiligingsinstellingen\Lokaal Beleid\gebruikersrechtenbeheer** map, en dubbelklik op Beveiligingscontrole genereren.
3. Op Hallo **lokale beveiligingsinstelling** tabblad, controleert u of dat Hallo AD FS 2.0-serviceaccount wordt vermeld. Als dit niet aanwezig is, klikt u op **gebruiker of groep toevoegen** toe te voegen toohello lijst en klik vervolgens op **OK**.
4. tooenable controle, open een opdrachtprompt met verhoogde bevoegdheden en Voer Hallo volgende opdracht uit:<code>auditpol.exe /set /subcategory:"Application Generated" /failure:enable /success:enable</code>
5. Sluit Lokaal beveiligingsbeleid en open vervolgens Hallo-beheermodule. tooopen Hallo-beheermodule, klikt u op **Start**, wijst u te**programma's**, wijst u te**Systeembeheer**, en klik vervolgens op AD FS 2.0-beheer.
6. Klik in het deelvenster Acties Hallo eigenschappen van Federation Service bewerken.
7. In Hallo **eigenschappen van Federation Service** dialoogvenster vak, klikt u op Hallo **gebeurtenissen** tabblad.
8. Selecteer Hallo **geslaagde** en **mislukte controles** selectievakjes uit.
9. Klik op **OK**.

#### <a name="tooenable-auditing-for-ad-fs-on-windows-server-2012-r2"></a>tooenable controles voor AD FS in Windows Server 2012 R2
1. Open **lokaal beveiligingsbeleid** door het openen van **Serverbeheer** op Hallo startscherm of Server Manager in de taakbalk Hallo op Hallo bureaublad en klik vervolgens op **extra/lokaal beveiligingsbeleid voor**.
2. Navigeer toohello **beveiliging Beveiligingsinstellingen\Lokaal beleid\gebruikersrechten toewijzen** map en dubbelklik vervolgens op **Beveiligingscontrole genereren**.
3. Op Hallo **lokale beveiligingsinstelling** tabblad, controleert u of Hallo AD FS-serviceaccount wordt vermeld. Als dit niet aanwezig is, klikt u op **gebruiker of groep toevoegen** toe te voegen toohello lijst en klik vervolgens op **OK**.
4. tooenable controle, open een opdrachtprompt met verhoogde bevoegdheden en Voer Hallo volgende opdracht: ```auditpol.exe /set /subcategory:"Application Generated" /failure:enable /success:enable```.
5. Sluit **lokaal beveiligingsbeleid**, en open vervolgens Hallo **AD FS-beheer** -module (in Serverbeheer klikt u op Extra en selecteer vervolgens AD FS-beheer).
6. Klik in het deelvenster Acties Hallo op **eigenschappen van Federation Service bewerken**.
7. Klik in de Hallo Federation Service-eigenschappen in het dialoogvenster op Hallo **gebeurtenissen** tabblad.
8. Selecteer Hallo **geslaagde en mislukte controles** selectievakjes en klik vervolgens op **OK**.

#### <a name="tooenable-auditing-for-ad-fs-on-windows-server-2016"></a>tooenable controle voor AD FS in Windows Server 2016
1. Open **lokaal beveiligingsbeleid** door het openen van **Serverbeheer** op Hallo startscherm of Server Manager in de taakbalk Hallo op Hallo bureaublad en klik vervolgens op **extra/lokaal beveiligingsbeleid voor**.
2. Navigeer toohello **beveiliging Beveiligingsinstellingen\Lokaal beleid\gebruikersrechten toewijzen** map en dubbelklik vervolgens op **Beveiligingscontrole genereren**.
3. Op Hallo **lokale beveiligingsinstelling** tabblad, controleert u of Hallo AD FS-serviceaccount wordt vermeld. Als dit niet aanwezig is, klikt u op **gebruiker of groep toevoegen** Hallo AD FS-service-account toohello lijst toevoegen en klik vervolgens op **OK**.
4. tooenable controle, open een opdrachtprompt met verhoogde bevoegdheden en Voer Hallo volgende opdracht uit:<code>auditpol.exe /set /subcategory:"Application Generated" /failure:enable /success:enable.</code>
5. Sluit **lokaal beveiligingsbeleid**, en open vervolgens Hallo **AD FS-beheer** -module (in Serverbeheer klikt u op Extra en selecteer vervolgens AD FS-beheer).
6. Klik in het deelvenster Acties Hallo op **eigenschappen van Federation Service bewerken**.
7. Klik in de Hallo Federation Service-eigenschappen in het dialoogvenster op Hallo **gebeurtenissen** tabblad.
8. Selecteer Hallo **geslaagde en mislukte controles** selectievakjes en klik vervolgens op **OK**. Deze moeten standaard zijn ingeschakeld.
9. Open een PowerShell-venster en Hallo volgende opdracht uitvoeren: ```Set-AdfsProperties -AuditLevel Verbose```.

Het basiscontroleniveau is standaard ingeschakeld. Lees meer over Hallo [uitbreiding van AD FS-controle in Windows Server 2016](https://technet.microsoft.com/en-us/windows-server-docs/identity/ad-fs/operations/auditing-enhancements-to-ad-fs-in-windows-server-2016)


#### <a name="toolocate-hello-ad-fs-audit-logs"></a>toolocate hello AD FS-auditlogboeken
1. Open **Logboeken**.
2. Ga tooWindows logboeken en selecteer **beveiliging**.
3. Klik op de juiste hello, **huidige Logboeken filteren**.
4. Selecteer onder Gebeurtenisbron **AD FS-controle**.

![AD FS-auditlogboeken](./media/active-directory-aadconnect-health-requirements/adfsaudit.png)

> [!WARNING]
> Met een groepsbeleid kan AD FS-controle worden uitgeschakeld. Als AD FS-controle is uitgeschakeld, zijn er geen gebruiksanalyses beschikbaar over aanmeldactiviteiten. Zorg ervoor dat u geen groepsbeleid hebt waarmee AD FS-controle wordt uitgeschakeld.>
>


## <a name="installing-hello-azure-ad-connect-health-agent-for-sync"></a>Hello Azure AD Connect Health-agent voor synchronisatie installeren
Hello Azure AD Connect Health-agent voor synchronisatie wordt automatisch geïnstalleerd in de laatste build Hallo van Azure AD Connect. Azure AD Connect toouse voor synchronisatie, u moet toodownload Hallo meest recente versie van Azure AD Connect en deze installeren. U kunt de meest recente versie Hallo downloaden [hier](http://www.microsoft.com/download/details.aspx?id=47594).

tooverify Hallo-agent is geïnstalleerd, zoek naar de volgende services op de server Hallo Hallo. Als u Hallo configuratie hebt voltooid, moeten ze al worden uitgevoerd. Anders zijn ze gestopt totdat het Hallo-configuratie is voltooid.

* Azure AD Connect Health Sync Insights-service
* Azure AD Connect Health Sync Monitoring-service

![Azure AD Connect Health for Sync verifiëren](./media/active-directory-aadconnect-health-sync/services.png)

> [!NOTE]
> Als u Azure AD Connect Health wilt gebruiken, is Azure AD Premium vereist. Als u geen Azure AD Premium, bent u toocomplete Hallo configuratie in hello Azure-portal. Zie voor meer informatie, Hallo [pagina vereisten](active-directory-aadconnect-health-agent-install.md#requirements).
>
>

## <a name="manual-azure-ad-connect-health-for-sync-registration"></a>Handmatige Azure AD Connect Health for Sync-registratie
Als hello Azure AD Connect Health for Sync-agent-registratie mislukt nadat Azure AD Connect met succes installeert, kunt u de volgende PowerShell-opdracht toomanually Hallo agent registreren Hallo gebruiken.

> [!IMPORTANT]
> Met de volgende PowerShell-opdracht is alleen vereist als het registreren van Hallo agent mislukt nadat Azure AD Connect installeert.
>
>

Hallo volgende PowerShell-opdracht is vereist alleen wanneer het registreren van Hallo health agent mislukt zelfs na een geslaagde installatie en configuratie van Azure AD Connect. Hello Azure AD Connect Health-services wordt gestart nadat het Hallo-agent is geregistreerd.

U kunt handmatig hello Azure AD Connect Health-agent voor synchronisatie met behulp van de volgende PowerShell-opdracht Hallo registreren:

`Register-AzureADConnectHealthSyncAgent -AttributeFiltering $false -StagingMode $false`

Hallo-opdracht worden de volgende parameters:

* AttributeFiltering: $true (standaard) - als Azure AD Connect Hallo kenmerk standaardset niet synchroniseert en aangepaste toouse een gefilterde kenmerk is ingesteld. $false in andere gevallen.
* StagingMode: $false (standaard) - als hello Azure AD Connect-server zich niet in de faseringsmodus bevindt, $true als Hallo-server is geconfigureerd in de faseringsmodus toobe.

Als u wordt gevraagd voor verificatie moet u hetzelfde hoofdbeheerdersaccount Hallo (zoals admin@domain.onmicrosoft.com) die is gebruikt voor het configureren van Azure AD Connect.

## <a name="installing-hello-azure-ad-connect-health-agent-for-ad-ds"></a>Hello Azure AD Connect Health-Agent voor AD DS installeren
toostart Hallo installatie van de agent, dubbelklikt u op Hallo .exe-bestand dat u hebt gedownload. Klik op installeren op de eerste welkomstscherm.

![Azure AD Connect Health verifiëren](./media/active-directory-aadconnect-health/aadconnect-health-adds-agent-install1.png)

Zodra het Hallo-installatie is voltooid, klikt u op nu configureren.

![Azure AD Connect Health verifiëren](./media/active-directory-aadconnect-health/aadconnect-health-adds-agent-install2.png)

Er wordt een opdrachtprompt geopend, waarna PowerShell wordt gebruikt om Register-AzureADConnectHealthADDSAgent uit te voeren. Wanneer na vragen aan gebruiker toosign in tooAzure, gaat u verder gaan en meld u aan.

![Azure AD Connect Health verifiëren](./media/active-directory-aadconnect-health/aadconnect-health-adds-agent-install3.png)

Na het aanmelden gaat PowerShell door. Zodra deze is voltooid, kunt u PowerShell sluiten en Hallo-configuratie is voltooid.

Op dit moment Hallo services moeten worden gestart zodat automatisch Hallo agent toomonitor en verzamelen van gegevens. Als u niet alle Hallo vereisten die worden beschreven in de vorige secties Hallo voldaan, worden waarschuwingen weergegeven in Hallo PowerShell-venster. Ervoor toocomplete Hallo worden [vereisten](active-directory-aadconnect-health-agent-install.md#requirements) voordat u Hallo agent installeert. Hallo volgende schermafbeelding is een voorbeeld van deze fouten.

![Azure AD Connect Health voor AD DS verifiëren](./media/active-directory-aadconnect-health/aadconnect-health-adds-agent-install4.png)

tooverify Hallo-agent is geïnstalleerd, zoek naar de volgende services op de domeincontroller Hallo Hallo.

* Azure AD Connect Health AD DS Insights-service
* Azure AD Connect Health AD DS Monitoring-service

Als u Hallo configuratie hebt voltooid, moeten al deze services worden uitgevoerd. Anders zijn ze gestopt totdat het Hallo-configuratie is voltooid.

![Azure AD Connect Health verifiëren](./media/active-directory-aadconnect-health/aadconnect-health-adds-agent-install5.png)


### <a name="agent-registration-using-powershell"></a>Agentregistratie met behulp van PowerShell
U kunt na de installatie van Hallo desbetreffende agent setup.exe Hallo registratiestap voor agent met behulp van de volgende PowerShell-opdrachten, afhankelijk van de rol Hallo Hallo uitvoeren. Open een PowerShell-venster en de juiste Hallo-opdracht uitvoeren:

```
    Register-AzureADConnectHealthADFSAgent
    Register-AzureADConnectHealthADDSAgent
    Register-AzureADConnectHealthSyncAgent

```

Deze opdrachten accepteren 'Referenties' als een parameter toocomplete Hallo registreren in een niet-interactieve wijze of op een Server Core-computer.
* Hallo referentie kan worden vastgelegd in een PowerShell-variabele die wordt doorgegeven als parameter.
* U kunt een Azure AD Identity die toegang tooregister Hallo agents en heeft geen MFA ingeschakeld opgeven.
* Globale beheerders hebben standaard toegang tooperform agentregistratie. U kunt ook toestaan dat andere minder bevoegde identiteiten tooperform deze stap. Meer informatie over [Toegangsbeheer op basis van rollen](active-directory-aadconnect-health-operations.md#manage-access-with-role-based-access-control).

```
    $cred = Get-Credential
    Register-AzureADConnectHealthADFSAgent -Credential $cred

```

## <a name="configure-azure-ad-connect-health-agents-toouse-http-proxy"></a>Azure AD Connect Health-Agents toouse HTTP-Proxy configureren
U kunt Azure AD Connect Health-Agents toowork configureren met een HTTP-Proxy.

> [!NOTE]
> * Gebruik 'Netsh WinHttp set ProxyServerAddress' wordt niet ondersteund als Hallo agent System.Net toomake webaanvragen in plaats van Microsoft Windows HTTP Services gebruikt.
> * Hallo is geconfigureerde Http-Proxy-adres gebruikte toopass via versleutelde Https-berichten.
> * Proxy’s die zijn geverifieerd (met HTTPBasic), worden niet ondersteund.
>
>

### <a name="change-health-agent-proxy-configuration"></a>De Health Agent-proxyconfiguratie wijzigen
U hebt Hallo opties tooconfigure Azure AD Connect Health-Agent toouse een HTTP-Proxy te volgen.

> [!NOTE]
> Alle Azure AD Connect Health Agent-services moeten opnieuw worden gestart, in volgorde voor Hallo proxy-instellingen toobe bijgewerkt. Hallo volgende opdracht uitvoeren:<br>
> Restart-Service AdHealth*
>
>

#### <a name="import-existing-proxy-settings"></a>Bestaande proxyinstellingen importeren
##### <a name="import-from-internet-explorer"></a>Importeren vanuit Internet Explorer
Internet Explorer HTTP-proxy-instellingen kunnen worden geïmporteerd, toobe door Hallo gebruikt met Azure AD Connect Health-Agents. Uitvoeren op elk van Hallo-servers waarop Hallo Health agent wordt uitgevoerd, Hallo volgende PowerShell-opdracht:

    Set-AzureAdConnectHealthProxySettings -ImportFromInternetSettings

##### <a name="import-from-winhttp"></a>Importeren vanaf WinHTTP
WinHTTP proxy-instellingen kunnen worden geïmporteerd, toobe door Hallo gebruikt met Azure AD Connect Health-Agents. Uitvoeren op elk van Hallo-servers waarop Hallo Health agent wordt uitgevoerd, Hallo volgende PowerShell-opdracht:

    Set-AzureAdConnectHealthProxySettings -ImportFromWinHttp

#### <a name="specify-proxy-addresses-manually"></a>Handmatig proxyadressen opgeven
U kunt handmatig een proxyserver opgeven op Hallo Health-Agent uitgevoerd door het uitvoeren van de volgende PowerShell-opdracht Hallo Hallo-servers:

    Set-AzureAdConnectHealthProxySettings -HttpsProxyAddress address:port

Voorbeeld: *Set-AzureAdConnectHealthProxySettings -HttpsProxyAddress myproxyserver:443*

* Het adres kan een oplosbare DNS-servernaam of een IPv4-adres zijn
* U hoeft geen poort op te geven. Indien u geen poort opgeeft, wordt 443 gekozen als standaardpoort.

#### <a name="clear-existing-proxy-configuration"></a>De bestaande proxyconfiguratie wissen
U kunt Hallo bestaande proxyconfiguratie wissen door het uitvoeren van de volgende opdracht Hallo:

    Set-AzureAdConnectHealthProxySettings -NoProxy


### <a name="read-current-proxy-settings"></a>De huidige proxyinstellingen lezen
Hallo momenteel zodanig geconfigureerd dat de proxy-instellingen kunt u door het uitvoeren van de volgende opdracht Hallo lezen:

    Get-AzureAdConnectHealthProxySettings


## <a name="test-connectivity-tooazure-ad-connect-health-service"></a>Test de connectiviteit tooAzure AD Connect Health-Service
Het is mogelijk dat problemen optreden waardoor hello Azure AD Connect Health agent toolose connectiviteit met hello Azure AD Connect Health-service. Hierbij kan het gaan om netwerkproblemen, problemen met de machtigingen of andere problemen.

Als Hallo-agent kan geen toosend gegevens toohello Azure AD Connect Health-service langer dan twee uur is, wordt Hiermee wordt aangegeven met de volgende waarschuwing in de portal Hallo Hallo: 'Health-servicegegevens is niet van toodate.' U kunt controleren als Hallo van invloed op een Azure AD Connect Health agent kunnen tooupload gegevens toohello Azure AD Connect Health-service wordt door het volgende PowerShell-opdracht Hallo uitvoeren:

    Test-AzureADConnectHealthConnectivity -Role ADFS

Hallo rolparameter heeft momenteel Hallo volgende waarden:

* ADFS
* Sync
* ADDS

U kunt de vlag - ShowResults Hallo Hallo opdracht tooview gedetailleerde logboeken. Gebruik Hallo voorbeeld te volgen:

    Test-AzureADConnectHealthConnectivity -Role Sync -ShowResult

> [!NOTE]
> toouse hello connectiviteitshulpprogramma, moet u de eerste volledige Hallo agentregistratie. Als u niet kunt toocomplete hello agentregistratie, controleert u of u alle Hallo hebt voldaan [vereisten](active-directory-aadconnect-health-agent-install.md#requirements) voor Azure AD Connect Health. Deze connectiviteitstest wordt standaard uitgevoerd tijdens de agentregistratie.
>
>

## <a name="related-links"></a>Verwante koppelingen
* [Azure AD Connect Health (Engelstalig)](active-directory-aadconnect-health.md)
* [Azure AD Connect Health Operations](active-directory-aadconnect-health-operations.md) (Azure AD Connect Health-bewerkingen)
* [Azure AD Connect Health gebruiken met AD FS](active-directory-aadconnect-health-adfs.md)
* [Azure AD Connect Health for Sync gebruiken](active-directory-aadconnect-health-sync.md)
* [Azure AD Connect Health gebruiken met AD DS](active-directory-aadconnect-health-adds.md)
* [Veelgestelde vragen over Azure AD Connect Health](active-directory-aadconnect-health-faq.md)
* [Versiegeschiedenis van Azure AD Connect Health](active-directory-aadconnect-health-version-history.md)

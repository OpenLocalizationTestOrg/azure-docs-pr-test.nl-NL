---
title: aaaCreate Azure BizTalk Services in hello Azure-portal | Microsoft Docs
description: Meer informatie over hoe tooprovision of Azure BizTalk Services maken in hello Azure-portal; MABS, WABS
services: biztalk-services
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: 3ad18876-a649-40d6-9aa0-1509c1d62c43
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 11/07/2016
ms.author: mandia
ms.openlocfilehash: 6781cadada8ac9c84e1fe045d2b0f995811f75b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-biztalk-services-using-hello-azure-portal"></a>BizTalk Services maken met hello Azure-portal

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]


> [!TIP]
> toosign in toohello Azure-portal, moet u een Azure-account en de Azure-abonnement. Als u geen account hebt, kunt u binnen een paar minuten een account voor de gratis proefversie maken. Zie [Gratis proefversie van Azure](http://go.microsoft.com/fwlink/p/?LinkID=239738).


## <a name="CreateService"></a>Een BizTalk Service maken
Afhankelijk van het Hallo-versie die u kiest, kunnen niet alle BizTalk Service-instellingen beschikbaar zijn.

1. Meld u aan toohello [Azure-portal](http://go.microsoft.com/fwlink/p/?LinkID=213885).
2. Selecteer in het onderste navigatievenster Hallo **nieuw**:  
   ![Selecteer de nieuwe knop Hallo][NEWButton]
3. Selecteer **APP SERVICES** > **BIZTALK SERVICE** > **AANGEPAST MAKEN**:  
   ![Selecteer BizTalk Service en selecteer Aangepast maken][NewBizTalkService]
4. Voer Hallo BizTalk Service-instellingen:
   
    <table border="1">
    <tr>
    <td><strong>De naam van de BizTalk Service</strong></td>
    <td>U kunt elke willekeurige naam invoeren, maar houd deze specifiek. Voorbeelden zijn:<br/><br/>
    <em>mijnbedrijf</em>.biztalk.windows.net<br/>
    <em>mijnbedrijfmijntoepassing</em>.biztalk.windows.net<br/>
    <em>mijntoepassing</em>.biztalk.windows.net<br/><br/>'. biztalk.windows.net ' wordt automatisch toegevoegd toohello naam die u invoert. Hiermee maakt u een URL die is gebruikt tooaccess uw BizTalk Service, zoals <strong>https://<em>mijntoepassing</em>. biztalk.windows.net</strong>.
    </td>
    </tr>
    <tr>
    <td><strong>Editie</strong></td>
    <td>Als u zich in Hallo test-/ ontwikkelingsfase bevindt, kiest u <strong>Developer</strong>. Als u zich in de productiefase hello, gebruikt u Hallo <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302279">BizTalk Services: grafiek van edities</a> toodetermine als <strong>Premium</strong>, <strong>standaard</strong>, of <strong>Basic</strong>hello juiste keuze is voor uw bedrijfsscenario.
    </td>
    </tr>
    <tr>
    <td><strong>Regio</strong></td>
    <td>Selecteer Hallo geografische regio toohost uw BizTalk Service.</td>
    </tr>
    <tr>
    <td><strong>Domein-URL</strong></td>
    <td><strong>Optioneel</strong>. Hallo domein-URL is standaard <em>Naamvanuwbiztalkservice</em>. biztalk.windows.net. U kunt ook een aangepast domein invoeren. Als uw domein bijvoorbeeld <em>contoso</em> is, kunt u het volgende opgeven: <br/><br/>
    <em>MijnBedrijf</em>.contoso.com<br/>
    <em>MijnBedrijfMijnToepassing</em>.contoso.com<br/>
    <em>MijnToepassing</em>.contoso.com<br/>
    <em>NaamVanUwBizTalkService</em>.contoso.com<br/>
    </td>
    </tr>
    </table>
Selecteer Hallo pijl Volgende.
5. Voer Hallo opslag en Database-instellingen:  <table border="1">
    <tr>
    <td><strong>Opslagaccount voor bewaken/archiveren</strong></td>
    <td>Selecteer een bestaand opslagaccount of maak een nieuw opslagaccount. <br/><br/>Als u een nieuw opslagaccount maakt, voert u Hallo <strong>Opslagaccountnaam</strong>.</td>
    </tr>
    <tr>
    <td><strong>Traceringsdatabase</strong></td>
    <td>Als u een bestaande Azure SQL Database gebruikt, kan deze niet worden gebruikt door een andere BizTalk Service. U moet het Hallo-aanmeldingsnaam en wachtwoord ingevoerd wanneer die Azure SQL Database-Server is gemaakt.<br/><br/><strong>TIP</strong> maken Hallo-traceringsdatabase en het opslagaccount voor bewaken/archiveren in dezelfde regio Hallo zoals Hallo BizTalk Service.</td>
    </tr>
    </table>
Selecteer Hallo pijl Volgende.
6. Voer Hallo Database-instellingen:  <table border="1">
    <tr>
    <td><strong>Naam</strong></td>
    <td>Beschikbaar als <strong>Maak een nieuw exemplaar van SQL-Database</strong> is geselecteerd in het vorige scherm Hallo.
    <br/><br/>
Voer een SQL-Database de naam van toobe die wordt gebruikt door uw BizTalk Service.</td>
    </tr>
    <tr>
    <td><strong>Server</strong></td>
    <td>Beschikbaar als <strong>Maak een nieuw exemplaar van SQL-Database</strong> is geselecteerd in het vorige scherm Hallo.
    <br/><br/>
Selecteer een bestaande SQL Database-server of maak een nieuwe SQL Database-server.</td>
    </tr>
    <tr>
    <td><strong>Aanmeldingsnaam voor server</strong></td>
    <td>Voer Hallo aanmeldingsnaam in.</td>
    </tr>
    <tr>
    <td><strong>Aanmeldingswachtwoord voor server</strong></td>
    <td>Voer het aanmeldingswachtwoord Hallo.</td>
    </tr>
    <tr>
    <td><strong>Regio</strong></td>
    <td>Beschikbaar als <strong>Een nieuw SQL Database-exemplaar</strong> is geselecteerd. Selecteer Hallo geografische regio toohost uw SQL-Database.</td>
    </tr>
    </table>

Hallo vinkje toocomplete Hallo wizard selecteren. Hallo voortgangspictogram wordt weergegeven:  
![Het voortgangspictogram wordt weergegeven als u klaar bent][ProgressComplete]

Als u klaar is hello Azure BizTalk Service gemaakt en is klaar voor uw toepassingen. Hallo standaardinstellingen zijn voldoende. Als u toochange Hallo standaardinstellingen wilt, selecteer **BIZTALK SERVICES** in Hallo navigatiedeelvenster links en selecteer vervolgens uw BizTalk Service. Er worden extra instellingen weergegeven in Hallo [tabbladen Dashboard, bewaken en schalen](biztalk-dashboard-monitor-scale-tabs.md) Hallo bovenaan.

Afhankelijk van de status van de Hallo Hallo BizTalk Service zijn er bepaalde bewerkingen die kunnen niet worden voltooid. Voor een lijst van deze bewerkingen te gaan[Statusgrafiek van BizTalk Services](biztalk-service-state-chart.md).

## <a name="post-provisioning-steps"></a>Stappen na de inrichting
* [Hallo-certificaat installeren op een lokale computer](#InstallCert)
* [Een certificaat dat gereed is voor productie toevoegen](#AddCert)
* [Hallo Access Control-naamruimte ophalen](#ACS)

#### <a name="InstallCert"></a>Hallo-certificaat installeren op een lokale computer
Bij het inrichten van de BizTalk Service wordt er een zelfondertekend certificaat gemaakt en gekoppeld aan uw BizTalk Service-abonnement. U moet dit certificaat downloaden en installeren op computers waarop u BizTalk Service-toepassingen implementeren of verzenden van berichten tooa BizTalk Service-eindpunt.

1. Meld u aan toohello [Azure-portal](http://go.microsoft.com/fwlink/p/?LinkID=213885).
2. Selecteer **BIZTALK SERVICES** in het linkernavigatievenster Hallo en selecteer vervolgens uw BizTalk Service-abonnement.
3. Selecteer Hallo **Dashboard** tabblad.
4. Selecteer **SSL-certificaat downloaden**:  
   ![SSL-certificaat wijzigen][QuickGlance]
5. Dubbelklik op Hallo-certificaat en doorloop Hallo wizard tooinstall Hallo certificaat. Zorg ervoor dat u Hallo certificaat installeert in Hallo **vertrouwde basiscertificeringsinstanties** opslaan.

#### <a name="AddCert"></a>Een certificaat dat gereed is voor productie toevoegen
Hallo zelfondertekend certificaat dat automatisch wordt gemaakt wanneer BizTalk Services maken is bedoeld voor gebruik in ontwikkelomgevingen alleen. Vervang het in productiescenario's door een certificaat dat gereed is voor productie.

1. Op Hallo **Dashboard** tabblad **SSL-certificaat bijwerken**.
2. Blader tooyour persoonlijke SSL-certificaat (*CertificateName*.pfx) die de naam van uw BizTalk Service bevat en klik vervolgens op het vinkje Hallo Hallo wachtwoord invoeren.

#### <a name="ACS"></a>Hallo Access Control-naamruimte ophalen
1. Meld u aan toohello [Azure-portal](http://go.microsoft.com/fwlink/p/?LinkID=213885).
2. Selecteer **BIZTALK SERVICES** in Hallo navigatiedeelvenster links en selecteer vervolgens uw BizTalk Service.
3. Selecteer in de taakbalk Hallo **verbindingsgegevens**:  
   ![Verbindingsgegevens selecteren][ACSConnectInfo]
4. Kopieer Hallo Access Control-waarden.

Wanneer u een BizTalk Service-project implementeert vanuit Visual Studio, voert u deze Access Control-naamruimte in. Hallo Access Control-naamruimte wordt automatisch gemaakt voor uw BizTalk Service.

Hallo Access Control-waarden kunnen worden gebruikt met elke toepassing. Wanneer u Azure BizTalk Services maakt, bepaalt deze Access Control-naamruimte Hallo verificatie met uw BizTalk Service-implementatie. Als u toochange Hallo abonnement of Hallo naamruimte wilt beheren, selecteert u **ACTIVE DIRECTORY** in Hallo navigatiedeelvenster links en selecteer vervolgens de naamruimte. Hallo taakbalk ziet u de opties.

Te klikken op **beheren** wordt geopend Hallo Access Control-beheerportal. Hallo BizTalk Service gebruikt in Hallo Access Control-beheerportal, **Service-identiteiten**:  
![ACS-Service-identiteiten in Hallo Access Control-beheerportal][ACSServiceIdentities]

Hallo Access Control service-identiteit is een set referenties waarmee toepassingen of clients tooauthenticate rechtstreeks via Access Control en geen token ontvangen.

> [!IMPORTANT]
> Hallo BizTalk Service gebruikt **eigenaar** voor Hallo standaardservice-identiteit en Hallo **wachtwoord** waarde. Als u de waarde symmetrische sleutel hello in plaats van Hallo waarde wachtwoord gebruiken, optreden hello volgende fout.<br/><br/>*Kan geen verbinding maken toohello Access Control-beheerserviceaccount met Hallo opgegeven referenties*
> 
> 

[Uw ACS-naamruimte beheren](https://msdn.microsoft.com/library/azure/hh674478.aspx) geeft een lijst weer met de volgende richtlijnen en aanbevelingen.

## <a name="requirements-explained"></a>Uitleg van de vereisten
Deze vereisten zijn niet van toepassing toohello editie Free.

<table border="1">
<tr bgcolor="FAF9F9">
        <td><strong>Wat u nodig hebt</strong></td>
        <td><strong>Waarom u dit nodig hebt</strong></td>
</tr>
<tr>
<td>Azure-abonnement</td>
<td>Hallo abonnement bepaalt wie toohello Azure-portal kunt aanmelden. Hallo accounthouder maakt Hallo-abonnement op <a HREF="https://account.windowsazure.com/Subscriptions"> Azure-abonnementen</a>.
<br/><br/>
Hello Azure-account kan meerdere abonnementen hebben en kan worden beheerd door iedereen die is toegestaan. De houder van uw Azure-account maakt bijvoorbeeld een abonnement met de naam <em>Biztalkserviceabonnement</em> en biedt Hallo BizTalk-beheerders binnen uw bedrijf (bijvoorbeeld ContosoBTSAdmins@live.com) toegang tot toothis abonnement. In dit scenario Hallo BizTalk-beheerders toohello Azure-portal aanmelden en hebben volledige beheerder rechten tooall Hallo gehoste services in Hallo abonnement, met inbegrip van Azure BizTalk Services. Hallo BizTalk-beheerders zijn niet hello Azure-account houders en daarom geen toegang tot tooany factureringsgegevens.
<br/><br/>
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=267577">Abonnementen en Opslagaccounts beheren in Azure-portal Hallo</a> vindt u meer informatie.
</td>
</tr>
<tr>
<td>Azure SQL Database</td>
<td>Hallo-tabellen, weergaven en opgeslagen procedures die worden gebruikt door de BizTalk Service, inclusief de traceringsgegevens Hallo Hallo opslaat.
<br/><br/>
Wanneer u een BizTalk Service maakt, kunt u een bestaande Azure SQL Server of Azure SQL Database gebruiken. U kunt ook automatisch een nieuwe server of database maken.
<br/><br/>
Hallo schaal van de SQL-Database wordt automatisch geconfigureerd. Normaal gesproken is Hallo standaardschaal voldoende voor een BizTalk Service. Veranderende Hallo schaal heeft impact op de prijzen. Zie <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=234930"> Accounts en facturering in Azure SQL Database</a>
<br/><br/>
<strong>Opmerkingen</strong>
<br/>
<ul>
<li> Wanneer u een nieuwe Azure SQL Server en Database maakt, wordt Azure Services automatisch ingeschakeld. Hallo BizTalk Service vereist dat Azure Services zijn ingeschakeld.</li>
<li>Als u een nieuwe Azure SQL Database op een bestaande Azure SQL-Server maakt, Hallo firewallregels Hallo Server niet worden gewijzigd. Het is daarom mogelijk dat andere Azure-Services zijn niet toegestaan voor toegang tot toohello Server-databases.</li>
</ul>
</td>
</tr>
<tr>
<td>Azure Access Control-naamruimte</td>
<td>Voert de verificatie met Azure BizTalk Services uit. Wanneer u een BizTalk Service-project implementeert vanuit Visual Studio, voert u deze Access Control-naamruimte in. Wanneer u een BizTalk Service maakt, wordt automatisch Hallo Access Control-naamruimte gemaakt.</td>
</tr>

<tr>
<td>Azure-opslagaccount</td>
<td>Geeft toegang tot tootables, blobs en wachtrijen die door uw BizTalk Service toosave Hallo volgende gebruikt:

<ul>
<li>Logboekbestanden voor die monitor Hallo BizTalk Service. Hallo uitvoer bewaking wordt ook weergegeven in Hallo **bewaking** tabblad in hello Azure-portal.</li>
<li>Bij het maken van een X12 of AS2-overeenkomst tussen partners, kunt u toostore berichteigenschappen voor Hallo archiveren functie inschakelen. Deze gegevens worden opgeslagen in Hallo Storage-account.</li>
</ul>
<br/>
Wanneer u een BizTalk Service maakt, kunt u een bestaand opslagaccount gebruiken of automatisch een nieuw opslagaccount maken.
<br/><br/>
Hallo standaardinstellingen voor opslag zijn voldoende voor een BizTalk Service.
<br/><br/>
Wanneer u een opslagaccount maakt, worden automatisch een primaire en secundaire sleutel gemaakt. Deze sleutels beheren de toegang tooyour Storage-account. Hallo BizTalk Service gebruikt automatisch Hallo primaire sleutel.
<br/><br/>
Zie <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=285671">Opslag</a> voor meer informatie.
</td>
</tr>

<tr>
<td>Persoonlijk SSL-certificaat</td>
<td>
Wanneer er een Azure BizTalk Service wordt gemaakt, wordt er ook een HTTPS-URL met de naam van uw BizTalk Service gemaakt. Deze URL is automatisch geconfigureerde toouse een zelfondertekend certificaat voor de ontwikkeling van alleen-lezen. Voor de productie hebt u een persoonlijk SSL-certificaat nodig.
<br/><br/>
<strong>Belangrijke informatie over SSL-certificaten</strong>

<ul>
<li>vervaldatum van certificaat Hallo moet kleiner zijn dan 5 jaar.</li>
<li>Voor alle persoonlijke certificaten is een wachtwoord vereist. Onthoud dit wachtwoord. U doet er verstandig aan het wachtwoord te delen met uw beheerders.</li>
<li>Zelfondertekende certificaten worden gebruikt in een test-/ontwikkelingsomgeving. Bij gebruik van zelfondertekende certificaten importeren Hallo certificaat tooyour persoonlijke certificaatarchief en Hallo certificaatarchief van vertrouwde basiscertificeringsinstanties.</li>
</ul>
<br/>Bij het verzenden van de certificeringsinstantie van Hallo productie certificaat aanvraag tooyour geven Hallo certificaateigenschappen te volgen:
<br/>

<ul>
<li><strong>Verbeterd sleutelgebruik</strong>: voor Azure BizTalk Services is minimaal serververificatie vereist.</li>
<li><strong>Algemene naam</strong>: Hallo volledig gekwalificeerde domeinnaam (FQDN) van uw Azure BizTalk Service-URL invoeren. Zie <a HREF="#CreateService">Een BizTalk Service maken</a> in dit artikel.</li>
</ul>
<br/>
Een nieuw of ander certificaat kan worden toegevoegd nadat Hallo BizTalk Service is gemaakt.
</td>
</tr>
</table>
<!---Loc Comment: Please, check link [Create a BizTalk Service] since it is not redirecting tooany location.--->



## <a name="hybrid-connections"></a>Hybride verbindingen
Wanneer u een Azure BizTalk Service maakt, Hallo **hybride verbindingen** tabblad is beschikbaar:

![Tabblad Hybride verbindingen][HybridConnectionTab]

Hybride verbindingen zijn gebruikte tooconnect een Azure-website of mobiele service van Azure tooany lokale resource die gebruikmaakt van een statische TCP-poort, zoals SQL Server, MySQL, HTTP-Web-API's, Mobile Services en de meeste aangepaste webservices.  Hybride verbindingen en Hallo BizTalk Adapter Service zijn verschillend. Hallo BizTalk Adapter Service is gebruikte tooconnect Azure BizTalk Services tooan on-premises regel van Business (LOB)-systeem.

 Zie [hybride verbindingen](integration-hybrid-connection-overview.md) toolearn meer, inclusief het maken en beheren van hybride verbindingen.

## <a name="next-steps"></a>Volgende stappen
Nu een BizTalk Service is gemaakt, tijd om uzelf bekend met verschillende Hallo [BizTalk Services: de tabbladen Dashboard, bewaken en schalen](biztalk-dashboard-monitor-scale-tabs.md). U kunt nu toepassingen maken met uw BizTalk Service. toostart te maken van toepassingen, ga[Azure BizTalk Services](http://go.microsoft.com/fwlink/p/?LinkID=235197).

## <a name="see-also"></a>Zie ook
* [BizTalk Services: grafiek van edities](biztalk-editions-feature-chart.md)<br/>
* [BizTalk Services: statusgrafiek](biztalk-service-state-chart.md)<br/>
* [BizTalk Services: back-ups maken en herstellen](biztalk-backup-restore.md)<br/>
* [BizTalk Services: beperking](biztalk-throttling-thresholds.md)<br/>
* [BizTalk Services: naam en sleutel van verlener](biztalk-issuer-name-issuer-key.md)<br/>
* [Hoe gaan gebruiken Azure BizTalk Services SDK Hallo](http://go.microsoft.com/fwlink/p/?LinkID=302335)<br/>
* [Hybride verbindingen](integration-hybrid-connection-overview.md)

[NewBizTalkService]: ./media/biztalk-provision-services/WABS_NewBizTalkService.png
[NEWButton]: ./media/biztalk-provision-services/WABS_New.png
[ProgressComplete]: ./media/biztalk-provision-services/WABS_ProgressComplete.png
[ACSConnectInfo]: ./media/biztalk-provision-services/WABS_ACSConnectInformation.png
[QuickGlance]: ./media/biztalk-provision-services/WABS_QuickGlance.png
[ACSServiceIdentities]: ./media/biztalk-provision-services/WABS_ACSServiceIdentities.png
[HybridConnectionTab]: ./media/biztalk-provision-services/WABS_HybridConnectionTab.png

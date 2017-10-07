---
title: problemen met Data Management Gateway aaaTroubleshoot | Microsoft Docs
description: Biedt tips tootroubleshoot problemen gerelateerde tooData Management Gateway.
services: data-factory
author: nabhishek
manager: jhubbard
editor: monicar
ms.assetid: c6756c37-4e5a-4d1e-ab52-365f149b4128
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: abnarain
published: True
ms.openlocfilehash: 85dacc8a1e8d574d6e7d5b556c995cebdc148fde
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-issues-with-using-data-management-gateway"></a>Problemen oplossen met behulp van Data Management Gateway
In dit artikel bevat informatie over het oplossen van problemen met het gebruik van Data Management Gateway.

> [!NOTE]
> Zie Hallo [Data Management Gateway](data-factory-data-management-gateway.md) artikel voor meer informatie over het Hallo-gateway. Zie Hallo [gegevens verplaatsen tussen on-premises en cloud](data-factory-move-data-between-onprem-and-cloud.md) artikel voor een overzicht van het verplaatsen van gegevens vanuit een lokale SQL Server-database tooMicrosoft Azure Blob-opslag met behulp van Hallo-gateway.
>
>

## <a name="failed-tooinstall-or-register-gateway"></a>Mislukte tooinstall of Registreer gateway
### <a name="1-problem"></a>1. Probleem
U ziet dit foutbericht werd weergegeven bij het installeren en registreren van een gateway in het bijzonder tijdens het downloaden van Hallo gateway-installatiebestand.

`Unable tooconnect toohello remote server". Please check your local settings (Error Code: 10003).`

#### <a name="cause"></a>Oorzaak
Hallo-machine waarop u tooinstall Hallo gateway probeert is toodownload Hallo nieuwste gateway-bestand voor installatie van Downloadcentrum Hallo vanwege tooa netwerkprobleem mislukt.

#### <a name="resolution"></a>Oplossing
Controleer uw firewall proxy server instellingen toosee of Hallo instellingen Hallo netwerkverbinding van Hallo computer toohello blokkeren [Downloadcentrum](https://download.microsoft.com/), en het Hallo-instellingen bijwerken dienovereenkomstig.

U kunt ook Hallo-installatiebestand voor de nieuwste gateway Hallo downloaden van Hallo [Downloadcentrum](https://www.microsoft.com/download/details.aspx?id=39717) op andere computers die toegang heeft tot Hallo Downloadcentrum. U kunt vervolgens kopiëren Hallo installer-bestand toohello gateway hostcomputer en voer deze handmatig tooinstall en update Hallo-gateway.

### <a name="2-problem"></a>2. Probleem
Deze fout te zien wanneer u een gateway tooinstall probeert door te klikken op **rechtstreeks op deze computer installeren** in hello Azure-portal.

`Error:  Abort installing a new gateway on this computer because this computer has an existing installed gateway and a computer without any installed gateway is required for installing a new gateway.`  

#### <a name="cause"></a>Oorzaak
Een gateway is al geïnstalleerd op Hallo-machine.

#### <a name="resolution"></a>Oplossing
Verwijderen van de bestaande gateway Hallo op Hallo machine en klik op Hallo **rechtstreeks op deze computer installeren** opnieuw koppelen.

### <a name="3-problem"></a>3. Probleem
U ziet deze fout bij het registreren van een nieuwe gateway.

`Error: hello gateway has encountered an error during registration.`

#### <a name="cause"></a>Oorzaak
U ziet dit bericht voor een van de volgende redenen Hallo:

* Hallo-indeling van Hallo gatewaycode is ongeldig.
* Hallo gatewaycode is ongeldig gemaakt.
* Hallo gatewaycode is opnieuw vanuit de portal Hallo is gegenereerd.  

#### <a name="resolution"></a>Oplossing
Controleer of u Hallo rechts gatewaycode via Hallo-portal. Indien nodig, een sleutel opnieuw genereren en Hallo sleutel tooregister Hallo gateway gebruiken.

### <a name="4-problem"></a>4. Probleem
U ziet Hallo volgende foutbericht weergegeven wanneer u bij het registreren van een gateway.

`Error: hello content or format of hello gateway key "{gatewayKey}" is invalid, please go tooazure portal toocreate one new gateway or regenerate hello gateway key.`



![Inhoud of de indeling van de sleutel is ongeldig](media/data-factory-troubleshoot-gateway-issues/invalid-format-gateway-key.png)

#### <a name="cause"></a>Oorzaak
Hallo is inhoud of de indeling van de invoer gatewaycode Hallo onjuist. Een van de redenen Hallo kan zijn dat u alleen een deel van de sleutel Hallo gekopieerd uit Hallo-portal of u een ongeldige sleutel.

#### <a name="resolution"></a>Oplossing
Een gatewaysleutel genereren in Hallo-portal en Hallo kopie knop toocopy Hallo gehele sleutel gebruiken. Plak deze in dit venster tooregister Hallo-gateway.

### <a name="5-problem"></a>5. Probleem
U ziet Hallo volgende foutbericht weergegeven wanneer u bij het registreren van een gateway.

`Error: hello gateway key is invalid or empty. Specify a valid gateway key from hello portal.`

![Gatewaycode is ongeldig of leeg](media/data-factory-troubleshoot-gateway-issues/gateway-key-is-invalid-or-empty.png)

#### <a name="cause"></a>Oorzaak
Hallo gatewaycode is gegenereerd of Hallo gateway is verwijderd op Hallo Azure-portal. Het kan ook gebeuren als Hallo Data Management Gateway-installatie niet nieuwste is.

#### <a name="resolution"></a>Oplossing
Controleer als Hallo Data Management Gateway-installatie de meest recente versie hello is, kunt u de meest recente versie Hallo vinden op Hallo Microsoft [Downloadcentrum](https://go.microsoft.com/fwlink/p/?LinkId=271260).

Als setup is de huidige / nieuwste en gateway nog op de Portal bestaat, lezensleutel Hallo gateway in hello Azure-portal en Hallo kopie knop toocopy Hallo gehele sleutel gebruiken en plak deze in dit venster tooregister Hallo-gateway. Anders Hallo-gateway opnieuw maken en begin opnieuw.

### <a name="6-problem"></a>6. Probleem
U ziet Hallo volgende foutbericht weergegeven wanneer u bij het registreren van een gateway.

`Error: Gateway has been online for a while, then shows “Gateway is not registered” with hello status “Gateway key is invalid”`

![Gatewaycode is ongeldig of leeg](media/data-factory-troubleshoot-gateway-issues/gateway-not-registered-key-invalid.png)

#### <a name="cause"></a>Oorzaak
Deze fout kan optreden omdat Hallo gateway is verwijderd of Hallo verbonden gatewaycode is gegenereerd.

#### <a name="resolution"></a>Oplossing
Als het Hallo-gateway is verwijderd, Hallo gateway vanuit Hallo portal opnieuw te maken, klikt u op **registreren**, kopieer Hallo-sleutel van het Hallo-portal, plakt u deze en probeer tooregister Hallo gateway.

Als Hallo gateway nog bestaat, maar de sleutel is gegenereerd, gebruikt u Hallo nieuwe sleutel tooregister Hallo gateway. Als er geen sleutel hello, Hallo-sleutel opnieuw vanuit het Hallo-portal opnieuw genereren.

### <a name="7-problem"></a>7. Probleem
Wanneer u een gateway registreren wilt, moet u mogelijk tooenter pad en het wachtwoord voor een certificaat.

![Certificaat opgeven](media/data-factory-troubleshoot-gateway-issues/specify-certificate.png)

#### <a name="cause"></a>Oorzaak
Hallo-gateway is geregistreerd op andere computers voordat. Tijdens de initiële registratie van een gateway Hallo is een versleutelingscertificaat gekoppeld aan het Hallo-gateway. Hallo certificaat kan automatisch worden gegenereerd door Hallo gateway of opgegeven door de gebruiker Hallo.  Dit certificaat is gebruikte tooencrypt referenties van het gegevensarchief hello (gekoppelde service).  

![Certificaat exporteren](media/data-factory-troubleshoot-gateway-issues/export-certificate.png)

Wanneer herstellen Hallo-gateway op een andere hostmachine, wordt u gevraagd de wizard Registratie Hallo voor dit certificaat toodecrypt eerder referenties gecodeerd met dit certificaat.  Hallo referenties kunnen niet worden ontsleuteld door de nieuwe gateway Hallo en latere kopie activiteit uitvoeringen die zijn gekoppeld aan deze nieuwe gateway kunnen geen zonder dit certificaat.  

#### <a name="resolution"></a>Oplossing
Als u Hallo referentiecertificaat hebt geëxporteerd uit de oorspronkelijke gatewaycomputer Hallo via Hallo **exporteren** knop op Hallo **instellingen** tabblad in Data Management Gateway Configuration Manager, gebruikt u Hallo Hier certificaat.

U kunt deze fase niet overslaan tijdens het herstellen van een gateway. Als Hallo certificaat ontbreekt, u moet toodelete Hallo gateway vanuit Hallo-portal en opnieuw maken van een nieuwe gateway.  Daarnaast werkt u alle gekoppelde services die gerelateerd toohello gateway zijn door hun referenties opnieuw invoeren.

### <a name="8-problem"></a>8. Probleem
U ziet Hallo volgende foutbericht wordt weergegeven.

`Error: hello remote server returned an error: (407) Proxy Authentication Required.`

#### <a name="cause"></a>Oorzaak
Deze fout treedt op wanneer uw gateway in een omgeving die een HTTP-proxy tooaccess internetbronnen vereist is of uw Proxywachtwoord verificatie is gewijzigd, maar deze niet dienovereenkomstig bijgewerkt in uw gateway.

#### <a name="resolution"></a>Oplossing
Volg de instructies Hallo in Hallo [overwegingen voor Proxy server](#proxy-server-considerations) sectie van dit artikel en proxy-instellingen configureren met Data Management Gateway Configuration Manager.

## <a name="gateway-is-online-with-limited-functionality"></a>Gateway is online via beperkte functionaliteit
### <a name="1-problem"></a>1. Probleem
Hallo-status van Hallo gateway worden weergegeven als online met beperkte functionaliteit.

#### <a name="cause"></a>Oorzaak
Hallo-status van Hallo gateway die u met beperkte functionaliteit voor een van de volgende redenen Hallo als on line zien:

* Gateway kan geen toocloud service verbinding via Azure Service Bus.
* Cloudservice kan geen toogateway verbinding via Service Bus.

Wanneer Hallo gateway online met beperkte functionaliteit is, mogelijk niet kunnen toouse Hallo Data Factory-Wizard kopiëren toocreate gegevenspijplijnen voor het kopiëren van gegevens tooor van on-premises gegevensopslagexemplaren. Als tijdelijke oplossing kunt u Data Factory-Editor in Hallo portal voor Visual Studio of Azure PowerShell.

#### <a name="resolution"></a>Oplossing
Oplossing voor dit probleem (online met beperkte functionaliteit) is gebaseerd op of Hallo gateway kan geen verbinding maken met cloudservice toohello of Hallo andere manier. Hallo volgende secties bieden deze oplossingen.

### <a name="2-problem"></a>2. Probleem
U zien Hallo volgende fout.

`Error: Gateway cannot connect toocloud service through service bus`

![Gateway kan geen toocloud-service verbinding](media/data-factory-troubleshoot-gateway-issues/gateway-cannot-connect-to-cloud-service.png)

#### <a name="cause"></a>Oorzaak
Gateway kan geen verbinding met het maken van de cloudservice toohello via Service Bus.

#### <a name="resolution"></a>Oplossing
Volg deze stappen tooget Hallo gateway weer online:

1. IP-adres uitgaande regels op de gatewaycomputer Hallo en Hallo bedrijfsfirewall toestaan. Vindt u IP-adressen uit het gebeurtenislogboek van Windows hello (ID == 401): een poging is gedaan tooaccess een socket op een manier die volgens de toegangsmachtigingen XX is niet toegestaan. XX. XX. XX:9350.
* Proxy-instellingen configureren op Hallo-gateway. Zie Hallo [overwegingen voor Proxy server](#proxy-server-considerations) sectie voor meer informatie.
* Uitgaande poort 5671 en 9350-9354 op beide Hallo Windows Firewall op de gatewaycomputer Hallo en Hallo bedrijfsfirewall inschakelen. Zie Hallo [poorten en firewall](#ports-and-firewall) sectie voor meer informatie. Deze stap is optioneel, maar we raden aan voor prestaties overweging.

### <a name="3-problem"></a>3. Probleem
U zien Hallo volgende fout.

`Error: Cloud service cannot connect toogateway through service bus.`

#### <a name="cause"></a>Oorzaak
Een tijdelijke fout in verbinding met het netwerk.

#### <a name="resolution"></a>Oplossing
Volg deze stappen tooget Hallo gateway weer online:

1. Wacht een paar minuten, Hallo connectiviteit worden automatisch hersteld wanneer Hallo-fout is verwijderd.
* Als Hallo fout zich blijft voordoen, start u Hallo gateway-service opnieuw.

## <a name="failed-tooauthor-linked-service"></a>Mislukte tooauthor gekoppelde service
### <a name="problem"></a>Probleem
U kunt deze fout tegenkomen wanneer u Referentiebeheer toouse Hallo portal tooinput referenties voor een nieuwe gekoppelde service probeert of referenties voor een bestaande gekoppelde service bijwerken.

`Error: hello data store '<Server>/<Database>' cannot be reached. Check connection settings for hello data source.`

Wanneer u deze fout ziet, Hallo instellingenpagina van Data Management Gateway Configuration Manager als volgt uitzien Hallo volgende schermopname.

![Database kan niet worden bereikt](media/data-factory-troubleshoot-gateway-issues/database-cannot-be-reached.png)

#### <a name="cause"></a>Oorzaak
Hallo SSL-certificaat is mogelijk verloren gegaan op Hallo gateway-apparaat. Hallo gatewaycomputer kan Hallo certificaat momenteel dat wordt gebruikt voor SSL-versleuteling niet laden. U ziet ook een foutbericht weergegeven in het Hallo-gebeurtenislogboek dat vergelijkbare toohello volgende bericht is.

 `Unable tooget hello gateway settings from cloud service. Check hello gateway key and hello network connection. (Certificate with thumbprint cannot be loaded.)`

#### <a name="resolution"></a>Oplossing
Volg deze stappen toosolve Hallo probleem:

1. Start de Data Management Gateway Configuration Manager.
2. Overschakelen van toohello **instellingen** tabblad.  
3. Klik op Hallo **wijziging** knop toochange Hallo SSL-certificaat.

   ![De knop certificaat wijzigen](media/data-factory-troubleshoot-gateway-issues/change-button-ssl-certificate.png)
4. Selecteer een nieuw certificaat als Hallo SSL-certificaat. U kunt een SSL-certificaat dat is gegenereerd door u of elke organisatie gebruiken.

   ![Certificaat opgeven](media/data-factory-troubleshoot-gateway-issues/specify-http-end-point.png)

## <a name="copy-activity-fails"></a>Kopieeractiviteit mislukt
### <a name="problem"></a>Probleem
Hallo na 'UserErrorFailedToConnectToSqlserver' fout na het instellen van een pijplijn in de portal hello, zult u merken.

`Error: Copy activity encountered a user error: ErrorCode=UserErrorFailedToConnectToSqlServer,'Type=Microsoft.DataTransfer.Common.Shared.HybridDeliveryException,Message=Cannot connect tooSQL Server`

#### <a name="cause"></a>Oorzaak
Dit kan gebeuren om verschillende redenen en risicobeperking varieert dienovereenkomstig.

#### <a name="resolution"></a>Oplossing
Uitgaande TCP-verbindingen via TCP-poort/1433 op Hallo Data Management Gateway-clientzijde toestaan voordat u verbinding maakt tooan SQL-database.

Als de doeldatabase Hallo een Azure SQL database is, controleert u SQL Server firewall-instellingen voor Azure ook.

Zie de volgende sectie tootest Hallo verbinding toohello on-premises met gegevensopslag Hallo.

## <a name="data-store-connection-or-driver-related-errors"></a>Gegevens opslaan verbinding of stuurprogramma gerelateerde fouten
Als u gegevens opslaan verbinding of stuurprogramma gerelateerde fouten ziet, voert u Hallo stappen te volgen:

1. Start de Data Management Gateway Configuration Manager op Hallo gateway-apparaat.
2. Overschakelen van toohello **Diagnostics** tabblad.
3. In **testverbinding**, Hallo gateway groep waarden toevoegen.
4. Klik op **Test** toosee als u verbinding met toohello maken kunt on-premises gegevensbron uit de gatewaycomputer Hallo door met de verbindingsgegevens Hallo en referenties. Als de testverbinding Hallo nog steeds niet na de installatie van een stuurprogramma, opnieuw opstarten hello gateway voor het toopick van laatste wijziging Hallo.

![Testverbinding in tabblad Diagnostische gegevens](media/data-factory-troubleshoot-gateway-issues/test-connection-in-diagnostics-tab.png)

## <a name="gateway-logs"></a>Gateway-Logboeken
### <a name="send-gateway-logs-toomicrosoft"></a>Gateway-logboeken tooMicrosoft verzenden
Wanneer u contact opneemt met Microsoft Support tooget hulp bij het oplossen van problemen met de gateway, wordt u mogelijk gevraagd tooshare uw gateway-Logboeken. Hallo-versie van gateway Hallo, kunt u logboeken met twee knop klikken in Data Management Gateway Configuration Manager vereist gateway delen.    

1. Overschakelen van toohello **Diagnostics** tabblad in Data Management Gateway Configuration Manager.

    ![Tabblad van Data Management Gateway diagnostische gegevens](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-diagnostics-tab.png)
2. Klik op **logboeken verzenden** toosee Hallo volgen in het dialoogvenster.

    ![Data Management Gateway verzenden Logboeken](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-send-logs-dialog.png)
3. (Optioneel) Klik op **logboeken bekijken** tooreview Logboeken in Logboeken Hallo.
4. (Optioneel) Klik op **privacy** privacyverklaring tooreview Microsoft web services.
5. Wanneer u tevreden bent met wat u van tooupload zijn, klikt u op **logboeken verzenden** tooactually Hallo logboeken verzenden vanuit Hallo laatste zeven dagen tooMicrosoft voor het oplossen van problemen. U ziet Hallo status van Hallo verzenden logboeken bewerking zoals weergegeven in de volgende schermafbeelding Hallo.

    ![Data Management Gateway verzenden logboeken status](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-send-logs-status.png)
6. Nadat het Hallo-bewerking is voltooid, ziet u een dialoogvenster, zoals wordt weergegeven in de volgende schermafbeelding Hallo.

    ![Data Management Gateway verzenden logboeken status](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-send-logs-result.png)
7. Hallo opslaan **rapport ID** en delen met Microsoft Support. Hallo rapport-ID is gebruikte toolocate Hallo gateway-logboeken die u hebt geüpload voor het oplossen van problemen.  Hallo lijst-ID wordt ook opgeslagen in de logboeken Hallo.  U kunt vinden door te kijken naar Hallo gebeurtenis-ID '25', en controleren van Hallo datum en tijd.

    ![Data Management Gateway verzenden Logboeken lijst-ID](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-send-logs-report-id.png)    

### <a name="archive-gateway-logs-on-gateway-host-machine"></a>Archief gateway-logboeken op de hostmachine gateway
Er zijn enkele scenario's waarbij u problemen met de gateway hebt en u gateway-logboeken rechtstreeks niet delen:

* U handmatig Hallo gateway gateway installeren en registreren Hallo.
* U probeert tooregister Hallo gateway met een opnieuw gegenereerde sleutel in Data Management Gateway Configuration Manager.
* U probeert toosend logboeken en Hallo gateway-hostservice kan niet worden verbonden.

Voor deze scenario's, kunt u de gateway-Logboeken als een zip-bestand opslaan en delen wanneer u contact opneemt met Microsoft ondersteuning. Bijvoorbeeld als er een fout opgetreden tijdens het registreren van Hallo-gateway als weergegeven in de volgende schermafbeelding Hallo.   

![Data Management Gateway-Registratiefout](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-registration-error.png)

Klik op Hallo **gateway-logboeken archiveren** tooarchive koppelen en Logboeken opslaan en vervolgens Hallo zip-bestand delen met Microsoft ondersteuning.

![Data Management Gateway archief Logboeken](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-archive-logs.png)

### <a name="locate-gateway-logs"></a>Naar de gateway-Logboeken
U vindt gedetailleerde gateway logboekgegevens in Hallo Windows-gebeurtenislogboeken.

1. Start Windows **logboeken**.
2. Logboeken niet vinden in Hallo **toepassings- en servicelogboeken** > **Data Management Gateway** map.

 Wanneer u bent het oplossen van problemen met de gateway, zoek naar niveau foutgebeurtenissen in Hallo-Logboeken.

![Data Management Gateway wordt geregistreerd in Logboeken](media/data-factory-troubleshoot-gateway-issues/gateway-logs-event-viewer.png)

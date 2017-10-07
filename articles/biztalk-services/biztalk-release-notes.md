---
title: Opmerkingen bij de aaaRelease voor Azure BizTalk Services | Microsoft Docs
description: Een lijst met bekende problemen voor Azure BizTalk Services Hallo
services: biztalk-services
documentationcenter: 
author: msftman
manager: erikre
editor: 
ms.assetid: f4906fdc-4cd9-4a57-a007-a88c2e51a18f
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2016
ms.author: deonhe
ms.openlocfilehash: ea53d6c40ed58badf4141453dc77d28dcfc6407f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="release-notes-for-azure-biztalk-services"></a>Releaseopmerkingen voor Azure BizTalk Services

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

Hallo release-opmerkingen voor Hallo Microsoft Azure BizTalk Services bevatten Hallo bekende problemen in deze release.

## <a name="whats-new-in-hello-november-update-of-biztalk-services"></a>Wat is er nieuw in update voor Hallo November van BizTalk Services
* Codering in rust kan worden ingeschakeld in Hallo BizTalk Services-Portal. Zie [Schakel versleuteling in rust in BizTalk Services-Portal](https://msdn.microsoft.com/library/azure/dn874052.aspx).

## <a name="update-history"></a>Historie van updates
### <a name="october-update"></a>Update van oktober
* Organisatieaccounts worden ondersteund:  
  * **Scenario**: U een BizTalk Service-implementatie met behulp van een Microsoft-account geregistreerd (zoals user@live.com). In dit scenario Hallo alleen Microsoft-Account gebruikers kunnen beheren BizTalk Service met behulp van Hallo BizTalk Services-portal. Een organisatie-account kan niet worden gebruikt.  
  * **Scenario**: U een BizTalk Service-implementatie met een organisatie-account in een Azure Active Directory geregistreerd (zoals user@fabrikam.com of user@contoso.com). In dit scenario Hallo alleen Azure Active Directory-gebruikers binnen dezelfde organisatie kunt beheren Hallo BizTalk Service met behulp van Hallo BizTalk Services-portal. Een Microsoft-account kan niet worden gebruikt.  
* Wanneer u een BizTalk Service in de klassieke Azure-portal hello maakt, wordt u automatisch geregistreerd in Hallo BizTalk Services-Portal.
  * **Scenario**: je je aanmelden bij de klassieke Azure-portal Hallo een BizTalk Service maakt en selecteer vervolgens **beheren** voor de eerste keer Hallo. Hallo BizTalk Services-portal wordt geopend, Hallo BizTalk Service automatisch wordt geregistreerd als gereed is voor uw implementaties.  
    Zie [registreren en bijwerken van een BizTalk Service-implementatie op Hallo van BizTalk Services-Portal](https://msdn.microsoft.com/library/azure/hh689837.aspx).  

### <a name="august-14-update"></a>14 augustus Update
* Overeenkomst en bridge ontkoppeling – Trading partner-overeenkomsten en bruggen worden nu losgekoppeld in Hallo BizTalk Services-Portal. U nu overeenkomsten en bruggen afzonderlijk maken en bij runtime bruggen los tooan overeenkomst op basis van waarden Hallo in EDI het Hallo-bericht. Zie [overeenkomsten maken in Azure BizTalk Services](https://msdn.microsoft.com/library/azure/hh689908.aspx), [een EDI-brug met behulp van BizTalk Services Portal maken](https://msdn.microsoft.com/library/azure/dn793986.aspx), [een AS2 brug met behulp van BizTalk Services Portal maken](https://msdn.microsoft.com/library/azure/dn793993.aspx), en [ Hoe los bruggen overeenkomsten tijdens runtime](https://msdn.microsoft.com/library/azure/dn794001.aspx)  
* Hallo optie toocreate sjablonen voor overeenkomsten is stopgezet.  
* Voor Hallo verzendkant overeenkomst, kunt u nu verschillende scheidingsteken ingesteld voor elk schema opgeven. Deze configuratie is opgegeven bij instellingen van het protocol voor send aan clientzijde overeenkomst. Zie voor meer informatie [maken een X12 overeenkomst in de Azure BizTalk Services](https://msdn.microsoft.com/library/azure/hh689847.aspx) en [maken van een overeenkomst EDIFACT in Azure BizTalk Services](https://msdn.microsoft.com/library/azure/dn606267.aspx). Twee nieuwe entiteiten worden ook toegevoegd aan toohello TPM OM API voor Hallo hetzelfde doel. Zie [X12DelimiterOverrides](https://msdn.microsoft.com/library/azure/dn798749.aspx) en [EDIFACTDelimiterOverride](https://msdn.microsoft.com/library/azure/dn798748.aspx).  
* Standaard XSD-constructs, met inbegrip van afgeleide typen worden nu ondersteund. Zie [Gebruik standaard XSD-constructs in uw maps](https://msdn.microsoft.com/library/azure/dn793987.aspx) en [gebruik afgeleide typen in de toewijzing van scenario's en voorbeelden](https://msdn.microsoft.com/library/azure/dn793997.aspx).  
* AS2 biedt ondersteuning voor nieuwe MIC voor het ondertekenen van berichten en nieuwe versleutelingsalgoritmen. Zie [een AS2-overeenkomst Maak in Azure BizTalk Services](https://msdn.microsoft.com/library/azure/hh689890.aspx).  
  ## <a name="know-issues"></a>Bekende problemen

### <a name="connectivity-issues-after-biztalk-services-portal-update"></a>Verbindingsproblemen na BizTalk Services-Portal bijwerken
  Als u Hallo BizTalk Services-Portal openen terwijl BizTalk Services is bijgewerkt tooroll in toohello service wijzigt, loopt u verbindingsproblemen met de Hallo BizTalk Services-Portal.  
  Als tijdelijke oplossing kan u Hallo browser starten, Hallo browsercache verwijderen of Hallo-portal te starten in de privé-modus.  

### <a name="visual-studio-ide-cannot-locate-hello-artifact-if-you-click-an-error-or-warning-in-a-biztalk-services-project"></a>Hallo artefact kan niet worden gevonden in Visual Studio IDE als u klikt op een fout of waarschuwing in een project BizTalk Services
Installeer Visual Studio 2012 Update 3 RC 1 Hallo toofix Hallo probleem.  

### <a name="custom-binding-project-reference"></a>Aangepaste binding project een verwijzing
Houd rekening met Hallo situaties met een BizTalk Services-project in Visual Studio-oplossing te volgen:  

* In dezelfde Visual Studio-oplossing Hallo, er is een BizTalk Services-project en een aangepaste binding-project. Hallo BizTalk Service-project heeft een projectbestand verwijzing toothis aangepaste binding.
* Hallo BizTalk Service-project bevat een verwijzing tooa aangepaste/bindingsgedrag dll-bestand.

U 'Build' Hallo oplossing in Visual Studio met succes. Vervolgens 'Opnieuw samenstellen' of opschonen Hallo-oplossing. Hierna is wanneer u opnieuw samenstellen of opschonen opnieuw Hallo na optreedt fout:  
  Kan geen toocopy bestand <Path tooDLL> too"bin\Debug\FileName.dll '. Hallo-proces heeft geen toegang tot bestand Hallo 'bin\Debug\FileName.dll' omdat deze wordt gebruikt door een ander proces.  

#### <a name="workaround"></a>Tijdelijke oplossing
* Als [Visual Studio 2012 Update 3](https://www.microsoft.com/download/details.aspx?id=39305) is geïnstalleerd, hebt u Hallo na twee opties:
  
  * Start Visual Studio opnieuw of
  * Opnieuw opstarten Hallo-oplossing. Voer alleen een Build op Hallo-oplossing.  
* Als [Visual Studio 2012 Update 3](https://www.microsoft.com/download/details.aspx?id=39305) is niet geïnstalleerd, opent u Taakbeheer, klik op tabblad Hallo-processen, klikt u op Hallo MSBuild.exe proces en klik op Hallo proces beëindigen knop.  

### <a name="routing-toobasichttprelay-endpoints-is-not-supported-from-bridges-and-biztalk-services-portal-if-non-printable-characters-are-promoted-as-http-headers"></a>TooBasicHttpRelay eindpunten routering wordt niet ondersteund bij bruggen en BizTalk Services-Portal als niet-afdrukbare tekens worden gepromoveerd tot HTTP-headers
Als u niet-afdrukbare tekens als onderdeel van de gepromoveerde eigenschappen voor berichten gebruikt, kunnen deze berichten gerouteerde toorelay bestemmingen die gebruikmaken van Hallo BasicHttpRelay binding niet. Hallo gepromoveerd ook eigenschappen die beschikbaar zijn als onderdeel van het bijhouden van URL-codering voor blobs en niet gecodeerde voor bestemmingen zijn.  

### <a name="mdn-is-sent-asynchronously-even-if-hello-send-asynchronous-mdn-option-is-unchecked"></a>MDN wordt asynchroon verzonden, zelfs als Hallo verzendt asynchrone MDN-optie is uitgeschakeld
Houd rekening met dit scenario: als u Hallo selecteert **verzenden van asynchrone MDN** selectievakje en geef een URL toosend Hallo asynchrone MDN aan, en schakelt u Hallo **verzenden van asynchrone MDN** selectievakje opnieuw Hallo MDN nog steeds URL verzonden toohello opgegeven Hoewel Hallo optie toosend asynchrone MDNs niet is ingeschakeld.  
Als tijdelijke oplossing, moet u het selectievakje Hallo URL opgegeven voordat Hallo apparaatverificatie **verzenden van asynchrone MDN** selectievakje en vervolgens implementeert Hallo AS2-overeenkomst.  

### <a name="whitespace-characters-beyond-a-valid-interchange-cause-an-empty-message-toobe-sent-toohello-suspend-endpoint"></a>Tekens dan witruimte buiten een geldig interchange oorzaak een leeg bericht verzonden toobe toohello onderbreken eindpunt
Als er spaties buiten een segment IEA, wordt Hallo disassembler wordt dit beschouwd als einde van het huidige knooppunt en Hallo volgende reeks spaties als een volgende bericht wordt bekeken. Omdat dit geen geldige interchange is, u merkt wellicht dat een geslaagde bericht toohello route bestemming is verzonden en een leeg Hallo bericht eindpunt onderbreken.  

### <a name="tracking-in-biztalk-services-portal"></a>BizTalk Services-Portal bijhouden
Bijhouden gebeurtenissen worden vastgelegd toohello EDI-berichtverwerking en eventuele correlatie. Als een bericht niet buiten Hallo Protocol fase, kunnen bijhouden wordt weergegeven als geslaagd. In dit geval verwijzen toohello uplogboekgedeelte onder Hallo **Details** kolom in **bijhouden** foutdetails.
Hallo X12 ontvangen en verzenden van instellingen ([maken een X12 overeenkomst in de Azure BizTalk Services](https://msdn.microsoft.com/library/azure/hh689847.aspx)) bieden informatie over het Hallo Protocol-fase.  

### <a name="update-agreement"></a>Bijwerken van de overeenkomst
Hallo BizTalk Services-Portal kunt u toomodify Hallo kwalificatie van een identiteit, wanneer een overeenkomst is geconfigureerd. Dit kan resulteren in de eigenschappen van is inconsistent. Er is bijvoorbeeld een overeenkomst met ZZ:1234567 en ZZ:7654321 Hallo kwalificatie. In de profielinstellingen van Hallo BizTalk Services-Portal wijzigt u ZZ:1234567 toobe 01:ChangedValue. U opent Hallo overeenkomst en 01:ChangedValue wordt weergegeven in plaats van ZZ:1234567.
toomodify hello kwalificatie van een identiteit, delete Hallo overeenkomst bijwerken **identiteiten** in Hallo Partnerprofiel en vervolgens opnieuw maken Hallo overeenkomst.  

> AZURE. Dit gedrag waarschuwing invloed X12 en AS2.  
> 
> 

### <a name="as2-attachments"></a>AS2-bijlagen
Bijlagen voor berichten worden niet ondersteund in AS2 verzenden of ontvangen. In het bijzonder bijlagen achtergrond worden genegeerd en de berichttekst hello wordt verwerkt als een reguliere AS2-bericht.  

### <a name="resources-remembering-path"></a>Resources: Onthoud pad
Bij het toevoegen van **Resources**, Hallo dialoogvenster mogelijk niet meer weet Hallo pad eerder gebruikt tooadd een resource. tooremember hello eerder gebruikt pad, voegt u Hallo BizTalk Services-Portal-website te**vertrouwde websites** in Internet Explorer.  

### <a name="if-you-rename-hello-entity-name-of-a-bridge-and-close-hello-project-without-saving-changes-opening-hello-entity-again-results-in-an-error"></a>Als u de naam van de entiteit van een brug en sluiten Hallo project Hallo naam zonder wijzigingen worden opgeslagen, Hallo entiteit opnieuw openen resulteert in een fout opgetreden
Houd rekening met een scenario in Hallo volgorde:  

* Een brug (bijvoorbeeld een XML-One-Way brug) tooa BizTalk Service-project toevoegen  
* Wijzig Hallo brug door een waarde opgeeft voor Hallo entiteit Name-eigenschap. Hiermee wijzigt u Hallo gekoppeld .bridgeconfig bestand met door u opgegeven naam Hallo.  
* Hallo .bcs bestand (door het Hallo-tabblad in Visual Studio sluiten) sluiten zonder Hallo wijzigingen worden opgeslagen.  
* Hallo .bcs bestand opnieuw openen vanuit Solution Explorer Hallo.  
  U ziet dat terwijl Hallo gekoppeld .bridgeconfig bestand Hallo nieuwe naam die u hebt opgegeven heeft, naam van de entiteit op Hallo ontwerpoppervlak Hallo nog steeds de oude naam Hallo. Als u tooopen Hallo Bridge configuratie probeert door te dubbelklikken op Hallo bridge onderdeel, krijgt u Hallo volgende fout:  
  `‘<old name>’ Entity’s associated file ‘<old name>.bridgeconfig’ does not exist`tooavoid die worden uitgevoerd in dit scenario, zorg ervoor dat u wijzigingen hebt opgeslagen, nadat u de naam Hallo entiteiten in een BizTalk Service-project.  
  
### <a name="biztalk-service-project-builds-successfully-even-if-an-artifact-has-been-excluded-from-a-visual-studio-project"></a>BizTalk Service-project bouwt is zelfs als een artefact is uitgesloten van een Visual Studio-project
Neem bijvoorbeeld een scenario waarin u een artefact (bijvoorbeeld een XSD-bestand) tooa BizTalk Service-project toevoegen, opnemen die artefacten in Hallo Bridge configuratie (bijvoorbeeld door te geven deze als een aanvraag berichttype) en vervolgens uitgesloten van het Hallo Visual Studio-project. In dat geval Hallo project bouwen niet krijgt elke fout zolang Hallo verwijderd artefact beschikbaar op de schijf op Hallo Hallo is dezelfde locatie vanaf waar deze is opgenomen in de Hallo Visual Studio-project.
  
### <a name="hello-biztalk-service-project-does-not-check-for-schema-availability-while-configuring-hello-bridges"></a>Hallo BizTalk Service-project controleert niet op schema beschikbaarheid tijdens het Hallo bruggen configureren
In een BizTalk Service-project als een schema dat wordt toegevoegd toohello project importeert een ander schema wordt Hallo BizTalk Service-project niet gecontroleerd of de geïmporteerde schema Hallo toohello project wordt toegevoegd. Als u toobuild dergelijk project probeert, krijgt u niet alle fouten in de build.
  
### <a name="hello-response-message-for-a-xml-request-reply-bridge-is-always-of-charset-utf-8"></a>Hallo-antwoordbericht voor een XML-Request-Reply brug is altijd van charset UTF-8
Voor deze release Hallo charset van Hallo response-bericht in een XML-Request-Reply Bridge tooUTF 8 altijd ingesteld.
  
### <a name="user-defined-datatypes"></a>Gebruiker gedefinieerde gegevenstypen
Hallo BizTalk Adapter Pack adapters binnen Hallo BizTalk Adapter Service-functie kunnen gebruikmaken van gebruiker gedefinieerde gegevenstypen voor bewerkingen van de adapter.
Bij gebruik van de gebruiker gedefinieerde gegevenstypen Hallo-bestanden (.dll) toodrive:\Program Files\Microsoft BizTalk Adapter Service\BAServiceRuntime\bin\ of toohello Global Assembly Cache (GAC) op Hallo-server die als host Hallo BizTalk Adapter Service service kopiëren. Anders treedt op Hallo client Hallo volgende fout:  
```
<s:Fault xmlns:s="http://schemas.xmlsoap.org/soap/envelope/">
<faultcode>s:Client</faultcode>
<faultstring xml:lang="en-US">hello UDT with FullName "File, FileUDT, Version=Value, Culture=Value, PublicKeyToken=Value" could not be loaded. Try placing hello assembly containing hello UDT definition in hello Global Assembly Cache.</faultstring>
<detail>
  <AFConnectRuntimeFault xmlns="http://Microsoft.ApplicationServer.Integration.AFConnect/2011" xmlns:i="http://www.w3.org/2001/XMLSchema-instance">
    <ExceptionCode>ERROR_IN_SENDING_MESSAGE</ExceptionCode>
  </AFConnectRuntimeFault>
</detail>
</s:Fault>
```  
  
> [!IMPORTANT]
> Het is aanbevolen toouse GACUtil.exe tooinstall een bestand in Hallo Global Assembly Cache. GACUtil.exe documenten hoe toouse deze hulpprogramma's en Hallo Visual Studio opdrachtregelopties.  
> 
> 

### <a name="restarting-hello-biztalk-adapter-service-web-site"></a>Hallo BizTalk Adapter Service-website opnieuw te starten
Installeren Hallo **BizTalk Adapter Service Runtime*** Hallo maakt **BizTalk Adapter Service** website in IIS met Hallo **BAService** toepassing. **BAService** toepassing intern relay binding tooextend Hallo bereik van de lokale service-eindpunt toohello cloud gebruikt. Voor een service die wordt gehost on-premises, wordt Hallo bijbehorende relay-eindpunt wordt geregistreerd op Hallo Service Bus alleen wanneer Hallo lokale service wordt gestart.  

Als u stoppen en starten van een toepassing, wordt niet gehonoreerd Hallo-configuratie voor het automatisch starten van een toepassing gebruikt. In dat geval wanneer **BAService** is gestopt, moet u altijd opnieuw opstarten Hallo **BizTalk Adapter Service** website in plaats daarvan. Niet starten of stoppen Hallo **BAService** toepassing.

### <a name="special-characters-should-not-be-used-for-address-and-entity-names-of-lob-components"></a>Speciale tekens mag niet worden gebruikt voor de namen van-adres en de entiteit van LOB-onderdelen
U moet speciale tekens niet gebruiken voor adressen en entiteit namen van LOB-onderdelen. Als u doet dit, krijgt u een fout opgetreden tijdens het implementeren van Hallo BizTalk Service-project. Voor bepaalde tekens bevatten zoals '%' hello BizTalk Adapter Service website mogelijk Ga in een gestopte status en hebt uitgevoerd, start u deze toomanually.

### <a name="test-map-with-get-context-property"></a>Testen van de Map met de eigenschap Get-Context
Als een transformatie bevat een **contexteigenschap ophalen** kaart bewerking, **Test kaart** zal mislukken. Als tijdelijke oplossing vervangen Hallo **contexteigenschap ophalen** kaart opnieuw met een tekenreeks wilt samenvoegen kaart bewerking met dummy-gegevens. Hiermee wordt de Hallo doelschema vullen en kunt dat u andere transformatie-functionaliteit testen.

### <a name="test-map-property-does-not-display"></a>De eigenschap toewijzen test weergegeven niet
Hallo **Test kaart** eigenschappen niet weergeven in Visual Studio. Dit kan gebeuren als hello **eigenschappen** venster en Hallo **Solution Explorer** venster niet tegelijkertijd worden gekoppeld. tooresolve deze, Hallo dock **eigenschappen** en Hallo **Solution Explorer** windows.  

### <a name="datetime-reformat-drop-down-is-grayed-out"></a>Datum/tijd opmaken vervolgkeuzelijst is niet beschikbaar
Bij het toevoegen van een datum/tijd opnieuw indelen kaart bewerking ontwerp toohello water en geconfigureerd, Hallo indeling vervolgkeuzelijst kan worden lichter gekleurd weergegeven. Dit kan gebeuren als de computer Hallo weergave is ingesteld **gemiddeld: 125%** of **groter – 150%**. tooresolve, Hallo weergave te ingesteld**kleiner: 100% (standaard)** gebruik Hallo stappen hieronder:  

1. Open Hallo **Configuratiescherm** en klik op **vormgeving en persoonlijke instellingen**.
2. Klik op **weergave**.
3. Klik op **kleiner: 100% (standaard)** en klik op **toepassen**.

Hallo **indeling** vervolgkeuzelijst moet nu werkt zoals verwacht.

### <a name="duplicate-agreements-in-hello-biztalk-services-portal"></a>Dubbele overeenkomsten in Hallo BizTalk Services-Portal
Houd rekening met Hallo scenario te volgen:

1. Maak een overeenkomst met Hallo handel Partner Management OM API.
2. Open Hallo overeenkomst Hallo BizTalk Services-Portal in twee verschillende tabbladen.
3. Hallo-overeenkomst van beide tabbladen Hallo implementeren.
4. Als gevolg hiervan beide overeenkomsten Hallo geïmplementeerd waardoor dubbele vermeldingen in Hallo BizTalk Services-Portal

**Tijdelijke oplossing**. Open een van de dubbele overeenkomsten Hallo in Hallo BizTalk Services-Portal en worden geïmplementeerd.  

### <a name="bridges-do-not-use-updated-certificate-even-after-a-certificate-has-been-updated-in-hello-artifact-store"></a>Bruggen gebruik geen bijgewerkte certificaat, zelfs nadat u een certificaat in Hallo artefact store is bijgewerkt
Houd rekening met Hallo volgen scenario's:  

**Scenario 1: Vingerafdruk gebaseerde certificaten gebruiken voor het beveiligen van bericht overdracht vanaf een brug tooa service-eindpunt**  
Neem bijvoorbeeld een scenario waarin het gebruik van certificaten op basis van een vingerafdruk in uw BizTalk Service-project. U werkt Hallo certificaat in Hallo BizTalk Services-Portal met Hallo dezelfde naam maar een andere vingerafdruk maar Hallo BizTalk Service-project niet dienovereenkomstig bijgewerkt. In een dergelijk scenario mogelijk Hallo bridge tooprocess Hallo-berichten doorgaan, omdat de gegevens van oudere Hallo certificaat mogelijk toch in Hallo kanaal cache. Hierna mislukt de berichtverwerking.  

**Tijdelijke oplossing**: Hallo certificaat in Hallo BizTalk Service-project bijwerken en implementeren van Hallo-project.  

**Scenario 2: Gedrag op basis van naam tooidentify certificaten gebruiken voor het beveiligen van bericht overdracht vanaf een brug tooa service-eindpunt**

Neem bijvoorbeeld een scenario waar u het gedrag op basis van naam tooidentify certificaten in uw BizTalk Service-project gebruiken. Hallo-certificaat in Hallo BizTalk Services-Portal bijwerken, maar Hallo BizTalk Service-project niet dienovereenkomstig bijgewerkt. In een dergelijk scenario mogelijk Hallo bridge tooprocess Hallo-berichten doorgaan, omdat de gegevens van oudere Hallo certificaat mogelijk toch in Hallo kanaal cache. Hierna mislukt de berichtverwerking.  

**Tijdelijke oplossing**: Hallo certificaat in Hallo BizTalk Service-project bijwerken en implementeren van Hallo-project.  

### <a name="bridges-continue-tooprocess-messages-even-when-hello-sql-database-is-offline"></a>Bruggen gaan tooprocess berichten, zelfs wanneer Hallo SQL-database offline is
Hallo BizTalk Services bruggen worden tooprocess berichten even, zelfs als Hallo Microsoft Azure SQL Database (die worden opgeslagen met informatie, zoals geïmplementeerde artefacten en pijplijnen Hallo), offline is. Dit is omdat BizTalk Services wordt gebruikt in de cache opgeslagen Hallo artefacten en configuratie van brug.
Als u niet Hallo bruggen tooprocess berichten wilt wanneer Hallo SQL-Database offline is, kunt u Hallo BizTalk Services PowerShell-cmdlets toostop gebruiken of onderbreken Hallo BizTalk Service. Zie [Azure BizTalk Service Management Sample](http://go.microsoft.com/fwlink/p/?LinkID=329019) voor Hallo Windows PowerShell-cmdlets toomanage-bewerkingen.  

### <a name="reading-hello-xml-message-within-a-bridges-custom-code-component-includes-an-extra-bom-character"></a>Lezen van het XML-Hallo-bericht in het onderdeel van een brug aangepaste code bevat een extra BOM-teken
Overweeg een scenario waar u tooread een XML-bericht in een brug aangepaste code. Als u Hallo .NET API System.Text.Encoding.UTF8.GetString(bytes) gebruikt wordt een extra BOM teken opgenomen in de uitvoer Hallo aan Hallo begin van het Hallo-bericht. Dus als u niet dat Hallo uitvoer tooinclude Hallo wilt extra BOM teken, moet u ```System.IO.StreamReader().ReadToEnd()```.

### <a name="sending-messages-tooa-bridge-using-wcf-does-not-scale"></a>Verzenden van berichten tooa bridge met WCF niet kan worden uitgebreid
Berichten tooa bridge met WCF niet kan worden uitgebreid. Als u een schaalbare client wilt, moet u in plaats daarvan HttpWebRequest gebruiken.

### <a name="upgrade-token-provider-error-after-upgrading-from-biztalk-services-preview-toogeneral-availability-ga"></a>UPGRADE: Token providerfout na de upgrade van BizTalk Services Preview tooGeneral beschikbaarheid (GA)
Er is een EDI- of AS2-overeenkomst met actieve batches. Wanneer Hallo BizTalk Service is bijgewerkt van Preview tooGA, optreden Hallo volgende:

* Fout: Hallo tokenprovider kan geen tooprovide een beveiligingstoken. Tokenprovider heeft bericht geretourneerd: Hallo externe naam kan niet worden omgezet.
* Batch-taken geannuleerd.

**Tijdelijke oplossing**: nadat Hallo BizTalk Service is bijgewerkt tooGeneral beschikbaarheid (GA), Hallo overeenkomst implementeren.  

### <a name="upgrade-toolbox-shows-hello-old-bridge-icons-after-upgrading-hello-biztalk-services-sdk"></a>UPGRADE: Werkset Hallo oude bridge pictogrammen worden na de upgrade Hallo BizTalk Services SDK
Na de upgrade van een eerdere versie van Hallo BizTalk Services SDK, waarin het naamelement oude pictogrammen voor van Hallo bruggen, blijft Hallo werkset tooshow Hallo oude pictogrammen voor Hallo bruggen. Als u een brug tooBizTalk Service project ontwerpoppervlak toevoegt, toont Hallo oppervlak Hallo nieuwe pictogram.  

**Tijdelijke oplossing**. U kunt dit probleem omzeilen door het verwijderen van Hallo .tbd bestanden onder <system drive>: \Users\<gebruiker > \AppData\Local\Microsoft\VisualStudio\11.0.  

### <a name="upgrade-biztalk-portal-update-from-preview-tooga-might-show-an-error-indicating-that-hello-edi-capability-is-not-available"></a>UPGRADE: BizTalk Portal bijwerken in Preview tooGA mogelijk een foutbericht dat aangeeft dat Hallo EDI-functionaliteit is niet beschikbaar weergeven
Als u bent aangemeld bij Hallo BizTalk Services-Portal tijdens het Hallo BizTalk Services is bijgewerkt van Preview tooGA, krijgt u mogelijk Hallo volgende fout op Hallo-portal:  

Deze mogelijkheid is niet beschikbaar als onderdeel van deze editie van Microsoft Azure BizTalk Services. toouse deze mogelijkheden overschakelen tooan gewenste editie.  

**Resolutie**: van Hallo-portal, sluiten en open Hallo browser en meld u aan bij de portal Hallo voor afmelden.  

### <a name="upgrade-new-tracking-data-does-not-show-up-after-biztalk-services-is-upgraded-tooga"></a>UPGRADE: Nieuwe traceergegevens wordt niet weergegeven nadat de BizTalk Services is een bijgewerkte tooGA
Stel een scenario waarin u een XML-bridge geïmplementeerd op Preview van BizTalk Services-abonnement hebben. Verzenden van berichten toohello bridge en bijbehorende traceergegevens Hallo is beschikbaar op Hallo BizTalk Services-Portal. Nu als Hallo BizTalk Services-Portal en BizTalk Services runtime bits zijn bijgewerkte tooGA en verzenden van een bericht toohello hetzelfde bridge eindpunt eerder hebt geïmplementeerd, Hallo traceergegevens wordt niet weergegeven voor berichten die na de upgrade is verzonden.  

### <a name="pipelines-versus-bridges"></a>Pijplijnen versus bruggen
In dit document worden Hallo term 'pijplijnen' en 'bruggen' door elkaar gebruikt. Beide in wezen betekenen Hallo dezelfde dingen die zich bevindt, een bericht processing unit geïmplementeerd op BizTalk Services.  

### <a name="concepts"></a>Concepten
[BizTalk Services](https://msdn.microsoft.com/library/azure/hh689864.aspx)   


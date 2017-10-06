---
title: aaaConnector versiegeschiedenis van Release | Microsoft Docs
description: In dit onderwerp geeft een lijst van alle versies van Hallo Connectors voor Forefront Identity Manager (FIM) en Microsoft Identity Manager (MIM)
services: active-directory
documentationcenter: 
author: fimguy
manager: femila
editor: 
ms.assetid: 6a0c66ab-55df-4669-a0c7-1fe1a091a7f9
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/24/2017
ms.author: fimguy
ms.openlocfilehash: 3522f17c30e46542eaa367ecdefdfd2fc47f71a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="connector-version-release-history"></a>Releasegeschiedenis van connectorversie
Hallo-Connectors voor Forefront Identity Manager (FIM) en Microsoft Identity Manager (MIM) worden regelmatig bijgewerkt.

> [!NOTE]
> In dit onderwerp is alleen van FIM en MIM. Deze Connectors worden niet ondersteund voor installatie op Azure AD Connect. Uitgebrachte Connectors zijn vooraf geïnstalleerd op de AADConnect bij een upgrade toospecified Build.

In dit onderwerp lijst van alle versies van Hallo Connectors die zijn uitgebracht.

Verwante koppelingen:

* [Download de meest recente Connectors](http://go.microsoft.com/fwlink/?LinkId=717495)
* [Algemene LDAP-Connector](active-directory-aadconnectsync-connector-genericldap.md) documentatie verwijst naar
* [Algemene SQL-Connector](active-directory-aadconnectsync-connector-genericsql.md) documentatie verwijst naar
* [Web-Services-Connector](http://go.microsoft.com/fwlink/?LinkID=226245) documentatie verwijst naar
* [PowerShell Connector](active-directory-aadconnectsync-connector-powershell.md) documentatie verwijst naar
* [Lotus Domino-Connector](active-directory-aadconnectsync-connector-domino.md) documentatie verwijst naar


## <a name="116040-aadconnect-pending-release"></a>1.1.604.0 (AADConnect in behandeling zijnde Release)


### <a name="fixed-issues"></a>Opgeloste problemen:

* Algemene webservices:
  * Een probleem dat verhindert dat er een SOAP-project wordt gemaakt wanneer er twee of meer eindpunten zijn opgelost.
* Algemene SQL:
  * In bewerking van import Hallo Hallo GSQL is niet converteren van een tijd correct wanneer opgeslagen tooconnector ruimte. Hallo is standaard datum en tijd-indeling voor connectorgebied Hallo GSQL gewijzigd van 'jjjj-MM-dd: ssZ' too'yyyy-MM-dd: ssZ '.

## <a name="115510-aadconnect-115530"></a>1.1.551.0 (AADConnect 1.1.553.0)

### <a name="fixed-issues"></a>Opgeloste problemen:

* Algemene webservices:
  * Hallo Wsconfig hulpprogramma heeft niet juist geconverteerd Hallo Json-matrix van"voorbeeld" voor de methode voor de REST Hallo. Dit veroorzaakt problemen met serialisatie deze Json-matrix voor Hallo REST-aanvraag.
  * Web Service-Connector Configuration Tool biedt geen ondersteuning voor informatie over het gebruik van symbolen ruimte in JSON-kenmerknamen 
    * Het patroon van een vervanging kan handmatig worden toegevoegd toohello WSConfigTool.exe.config bestand, bijvoorbeeld```<appSettings> <add key=”JSONSpaceNamePattern” value="__" /> </appSettings>```

* Lotus Notes:
  * Wanneer Hallo optie **aangepaste certifiers toestaan voor organisatie/organisatorische eenheden** is uitgeschakeld en vervolgens Hallo connector mislukt tijdens het exporteren (Update) na Hallo export stromen alle kenmerken geëxporteerde tooDomino zijn maar gelijktijdig Hallo met exporteren een KeyNotFoundException tooSync geretourneerd. 
    * Dit komt doordat Hallo wijzigen mislukt als er wordt geprobeerd toochange DN-naam (kenmerk UserName) door het wijzigen van een van onderstaande Hallo-kenmerken:  
      - Achternaam
      - Voornaam
      - MiddleInitial
      - AltFullName
      - AltFullNameLanguage
      - organisatie-eenheid
      - altcommonname

  * Wanneer **aangepaste certifiers toestaan voor organisatie/organisatorische eenheden** optie is ingeschakeld, maar vereist certifiers zijn nog steeds leeg vervolgens KeyNotFoundException optreedt.

### <a name="enhancements"></a>Verbeteringen:

* Algemene SQL:
  * **Scenario: aangepast geïmplementeerd:** ' * ' functie
  * **Beschrijving van oplossing:** gewijzigd benadering voor [met meerdere waarden verwijzing kenmerken verwerking](active-directory-aadconnectsync-connector-genericsql.md).


### <a name="fixed-issues"></a>Opgeloste problemen:

* Algemene webservices:
  * Serverconfiguratie kan niet worden geïmporteerd als WebService Connector aanwezig is
  * WebService-Connector werkt niet met meerdere Web-Services

* Algemene SQL:
  * Er is geen objecttypen worden vermeld voor één waarde waarnaar wordt verwezen kenmerk
  * Delta-import voor wijzigingen bijhouden strategie verwijderingen object wanneer de waarde wordt verwijderd uit de tabel met meerdere waarden
  * OverflowException in GSQL connector met de DB2 op AS / 400

Lotus:
  * Toegevoegde optie tooenable\disable OE's voor het openen van GlobalParameters pagina zoeken

## <a name="114430"></a>1.1.443.0

Uitgebracht: 2017 maart

### <a name="enhancements"></a>Verbeteringen

* Algemene SQL:</br>
  **Scenario symptomen:** is een bekende beperking Hello SQL Connector waar we alleen toestaan van een verwijzingstype tooone-object en vereisen kruisverwijzingen met leden. </br>
  **Beschrijving van oplossing:** In Hallo verwerkingsstap voor verwijzingen zijn ' * ' optie is gekozen, alle combinaties van objecttypen back toohello synchronisatie-engine wordt geretourneerd.

>[!Important]
- Hiermee maakt u veel tijdelijke aanduidingen
- Het is vereiste toomake ervoor dat Hallo naming uniek kruislings objecttypen.


* Algemene LDAP:</br>
 **Scenario:** wanneer slechts enkele containers in specifieke partitie zijn geselecteerd, klikt u vervolgens Hallo zoeken nog wordt uitgevoerd in hele partitie. Specifieke worden gefilterd door de synchronisatieservice, maar niet door MA wat kan leiden tot verminderde prestaties. </br>

 **Beschrijving van oplossing:** GLDAP gewijzigd-connector code toomake op het dan mogelijk doorlopen alle containers en objecten zoeken in elk van deze in plaats van zoeken in de hele partitie Hallo.


* Lotus Domino:

  **Scenario:** Domino e-mailondersteuning voor verwijderen van een persoon worden verwijderd tijdens het exporteren van een. </br>
  **Oplossing:** ondersteuning voor het verwijderen van een persoon worden verwijderd tijdens het exporteren van een configureerbare e.

### <a name="fixed-issues"></a>Opgeloste problemen:
* Algemene webservices:
 * Bij het wijzigen van Hallo service-URL in standaard via de WebService-configuratieprogramma projecten SAP wsconfig en vervolgens de volgende fout Hallo gebeurt: kan een deel van Hallo pad niet vinden

      ``'C:\Users\cstpopovaz\AppData\Local\Temp\2\e2c9d9b0-0d8a-4409-b059-dceeb900a2b3\b9bedcc0-88ac-454c-8c69-7d6ea1c41d17\cfg.config\cloneconfig.xml'. ``

* Algemene LDAP:
 * GLDAP Connector ondersteunt niet alle kenmerken in AD LDS-raadpleegt u
 * Wizard einden wanneer geen UPN-kenmerken worden gedetecteerd vanuit Hallo LDAP-directory-schema
 * Delta-invoer is mislukt met detectie-fouten is niet aanwezig zijn tijdens de volledige import, als 'objectclass'-kenmerk niet is geselecteerd
 * Een pagina van de configuratie 'Partities en hiërarchieën configureren' wordt niet weergegeven objecten welk type is gelijk toohello partitie voor nieuwe servers in algemene Hallo  
MA LDAP. Ze hebt u geleerd alleen objecten van de RootDSE-partitie.


* Algemene SQL:
 * Herstel voor algemene SQL watermerk bug van Delta-Import-kenmerk met meerdere waarden niet worden geïmporteerd
 * Bij het exporteren van deleted\added waarden van het kenmerk met meerdere waarden, maar ze zijn geen deleted\added in gegevensbron.  


* Lotus Notes:
 * Een bepaald veld 'Volledige naam' wordt weergegeven in Hallo metaverse correct echter als uitvoer tooNotes Hallo waarde voor kenmerk Hallo Null of leeg is.
 * Voor dubbele Certifier fout oplossen
 * Wanneer Hallo Object zonder gegevens is geselecteerd op hello Lotus Domino-Connector met andere objecten ontvangt er de Detectiefout Hallo tijdens het uitvoeren van volledige Import.
 * Wanneer de Delta-Import wordt uitgevoerd op hello Lotus Domino-Connector op Hallo einde van dat uitvoeren, Hallo Microsoft.IdentityManagement.MA.LotusDomino.Service.exe service soms een toepassing een fout retourneert.
 * Groep lidmaatschap algehele werkt goed samen en wordt onderhouden, behalve wanneer een gebruiker wordt uitgevoerd Hallo export tootry tooremove lidmaatschap van een als succesvol kunnen werken met een update bevat, maar Hallo gebruiker niet daadwerkelijk ophalen verwijderd uit het lidmaatschap van Lotus Notes.
 * Een kans toochoose modus van uitvoer als 'Append Item onderin' is toegevoegd in configuratie GUI Lotus MA tooappend nieuwe items onderin tijdens het Hallo exporteren voor kenmerken met meerdere waarden.
 * Connector voegt Hallo nodig logica toodelete Hallo-bestand van Hallo e-mailmap en ID-kluis.
 * Verwijderen van lidmaatschap voor cross-NAB lid niet werkt.
 * Waarden moeten worden verwijderd uit een kenmerk met meerdere waarden

## <a name="111170"></a>1.1.117.0
Uitgebracht: 2016 maart

**Nieuwe verbindingslijn**  
Initiële release van Hallo [algemene SQL-Connector](active-directory-aadconnectsync-connector-genericsql.md).

**Nieuwe functies:**

* Algemene LDAP-Connector:
  * Ondersteuning toegevoegd voor de delta-import met Isode.
* Web Services-Connector:
  * Bijgewerkte Hallo csEntryChangeResult activiteit en setImportErrorCode activiteit tooallow object fouten toobe geretourneerde back toohello synchronisatie-engine.
  * Bijgewerkte Hallo SAP6 en SAP6User sjablonen toouse Hallo nieuwe object foutniveau functionaliteit.
* Lotus Domino-Connector:
  * Voor het exporteren moet u één certifier per adresboek. U kunt nu gebruik Hallo hetzelfde wachtwoord voor alle certifiers toomake Hallo beheer eenvoudiger.

**Opgeloste problemen:**

* Algemene LDAP-Connector:
  * Voor IBM Tivoli DS, sommige reference-kenmerken zijn niet correct is gedetecteerd.
  * Voor Open LDAP tijdens een delta-import zijn spaties aan Hallo begin en einde van tekenreeksen afgekapt.
  * Voor Novell en NetIQ exporteren van een die een object tussen de organisatie-eenheden/containers en op Hallo verplaatst dezelfde tijd hernoemde Hallo-object is mislukt.
* Web Services-Connector:
  * Als het Hallo-web-service heeft meerdere eindpunten voor dezelfde binding, is vervolgens hello Connector niet correct detecteren deze eindpunten.
* Lotus Domino-Connector:
  * Exporteren van een van de Hallo fullName kenmerk tooa mail in database werkt niet.
  * Exporteren van een waarvoor de toegevoegde en verwijderde uit een groep alleen geëxporteerd Hallo toegevoegd leden.
  * Als een Notes-Document ongeldig is (Hallo kenmerk isValid ingesteld toofalse), vervolgens Hallo Connector mislukt.

## <a name="older-releases"></a>Oudere versies
Hallo-Connectors zijn vóór maart 2016 uitgebracht als ondersteuning onderwerpen.

**Algemene LDAP**

* [KB3078617](https://support.microsoft.com/kb/3078617) -1.0.0597, September 2015
* [KB3044896](https://support.microsoft.com/kb/3044896) -1.0.0549, van maart 2015
* [KB3031009](https://support.microsoft.com/kb/3031009) -1.0.0534, januari 2015
* [KB3008177](https://support.microsoft.com/kb/3008177) -1.0.0419, September 2014
* [KB2936070](https://support.microsoft.com/kb/2936070) -4.3.1082, 2014 maart

**WebServices**

* [KB3008178](https://support.microsoft.com/kb/3008178) -1.0.0419, September 2014

**PowerShell**

* [KB3008179](https://support.microsoft.com/kb/3008179) -1.0.0419, September 2014

**Lotus Domino**

* [KB3096533](https://support.microsoft.com/kb/3096533) -1.0.0597, September 2015
* [KB3044895](https://support.microsoft.com/kb/3044895) -1.0.0549, van maart 2015
* [KB2977286](https://support.microsoft.com/kb/2977286) -5.3.0712, 2014-augustus
* [KB2932635](https://support.microsoft.com/kb/2932635) -5.3.1003, februari 2014  
* [KB2899874](https://support.microsoft.com/kb/2899874) -5.3.0721, oktober 2013
* [KB2875551](https://support.microsoft.com/kb/2875551) -5.3.0534, 2013-augustus

## <a name="next-steps"></a>Volgende stappen
Meer informatie over Hallo [Azure AD Connect-synchronisatie](active-directory-aadconnectsync-whatis.md) configuratie.

Lees meer over het [integreren van uw on-premises identiteiten met Azure Active Directory ](active-directory-aadconnect.md).

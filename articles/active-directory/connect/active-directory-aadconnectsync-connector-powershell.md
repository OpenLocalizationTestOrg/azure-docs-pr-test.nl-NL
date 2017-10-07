---
title: aaaPowerShell Connector | Microsoft Docs
description: Dit artikel wordt beschreven hoe van tooconfigure Microsoft Windows PowerShell-Connector.
services: active-directory
documentationcenter: 
author: AndKjell
manager: femila
editor: 
ms.assetid: 6dba8e34-a874-4ff0-90bc-bd2b0a4199b5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 44ff6b1f53283000b72e15f861e0f86c21afe12b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="windows-powershell-connector-technical-reference"></a>Technische documentatie van Windows PowerShell-Connector
Dit artikel wordt beschreven Hallo Windows PowerShell-Connector. Hallo-artikel geldt toohello producten te volgen:

* Microsoft Identity Manager 2016 (MIM2016)
* Forefront Identity Manager 2010 R2 (FIM2010R2)
  * Hotfix 4.1.3671.0 moet gebruiken of later [KB3092178](https://support.microsoft.com/kb/3092178).

Voor MIM2016 en FIM2010R2 Hallo Connector is beschikbaar als een download van Hallo [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=717495).

## <a name="overview-of-hello-powershell-connector"></a>Overzicht van Hallo PowerShell Connector
Hallo PowerShell Connector kunt u het Hallo-synchronisatieservice toointegrate met externe systemen die worden geboden door dat Windows PowerShell gebaseerde API's. Hallo connector biedt een brug tussen het Hallo-mogelijkheden van de agent voor extensible connectivity op basis van oproep Hallo 2 (ECMA2) framework en Windows PowerShell. Zie voor meer informatie over Hallo ECMA framework Hallo [Extensible Connectivity 2.2 Management Agent Reference](https://msdn.microsoft.com/library/windows/desktop/hh859557.aspx).

### <a name="prerequisites"></a>Vereisten
Zorg voordat u Hallo Connector gebruikt, hebt u Hallo volgende op de server voor de synchronisatie Hallo:

* Microsoft.NET 4.5.2 of hoger
* Windows PowerShell 2.0, 3.0 of 4.0

Hallo-uitvoeringsbeleid op Hallo synchronisatieservice server moet geconfigureerde tooallow Hallo connector toorun Windows PowerShell-scripts. Tenzij Hallo scripts Hallo-connector wordt uitgevoerd digitaal zijn ondertekend, configureert u Hallo uitvoeringsbeleid door deze opdracht uit te voeren:  
`Set-ExecutionPolicy -ExecutionPolicy RemoteSigned`

## <a name="create-a-new-connector"></a>Een nieuwe Connector maken
een Windows PowerShell-connector in-synchronisatieservice Hallo toocreate, moet u een reeks Windows PowerShell-scripts die worden aangevraagd door de synchronisatieservice Hallo Hallo-stappen uitvoeren opgeven. Afhankelijk van het Hallo-gegevensbron verbinding van tooand Hallo functionaliteit die u nodig hebt, varieert Hallo-scripts moeten worden geïmplementeerd. Deze sectie bevat een overzicht van elk van de Hallo scripts die kunnen worden geïmplementeerd en wanneer ze zijn vereist.

Hallo ontworpen Windows PowerShell-connector is toostore Hallo-scripts in Hallo synchronisatieservice database. Het is mogelijk toorun scripts die zijn opgeslagen op Hallo bestandssysteem, is het gemakkelijker tooinsert Hallo-hoofdtekst van elk script rechtstreeks in toohello connectorconfiguratie.

tooCreate een PowerShell-connector in **synchronisatieservice** Selecteer **beheeragent** en **maken**. Selecteer Hallo **PowerShell (Microsoft)** Connector.

![Connector maken](./media/active-directory-aadconnectsync-connector-powershell/createconnector.png)

### <a name="connectivity"></a>Connectiviteit
Parameters voor de configuratie voor het verbinden van externe systeem tooa op te geven. Deze waarden zijn veilig opgeslagen door Hallo Synchronization Service en Windows PowerShell-scripts beschikbaar tooyour gedaan wanneer Hallo-connector wordt uitgevoerd.

![Connectiviteit](./media/active-directory-aadconnectsync-connector-powershell/connectivity.png)

U kunt Hallo connectiviteit parameters volgende configureren:

**Connectiviteit**

| Parameter | Standaardwaarde | Doel |
| --- | --- | --- |
| Server |<Blank> |De naam van de server die connector Hallo verbinding moet maken. |
| Domein |<Blank> |Domein van Hallo referentie toostore voor gebruik bij het Hallo-connector wordt uitgevoerd. |
| Gebruiker |<Blank> |Gebruikersnaam van Hallo referentie toostore voor gebruik bij het Hallo-connector wordt uitgevoerd. |
| Wachtwoord |<Blank> |Wachtwoord van Hallo referentie toostore voor gebruik bij het Hallo-connector wordt uitgevoerd. |
| Connector-Account imiteren |False |Indien true, wordt Hallo-synchronisatieservice Hallo Windows PowerShell-scripts uitgevoerd in de context van referenties Hallo Hallo. Indien mogelijk wordt het verdient aanbeveling dat Hallo **$Credentials** parameter is doorgegeven tooeach script wordt gebruikt in plaats van imitatie. Zie voor meer informatie over aanvullende machtigingen die zijn vereist toouse deze optie, [aanvullende configuratie voor imitatie](#additional-configuration-for-impersonation). |
| Gebruikersprofiel laden als u imitatie |False |Hiermee geeft u Windows tooload Hallo gebruikersprofiel Hallo-connector referenties tijdens de imitatie. Als de geïmiteerde gebruiker Hallo een zwervend profiel heeft, Hallo connector Hallo zwervend profiel niet geladen. Zie voor meer informatie over aanvullende machtigingen die zijn vereist toouse deze parameter, [aanvullende configuratie voor imitatie](#additional-configuration-for-impersonation). |
| Aanmeldingstype als u imitatie |Geen |Aanmeldingstype tijdens de imitatie. Zie voor meer informatie, Hallo [dwLogonType] [ dw] documentatie. |
| Alleen ondertekende Scripts |False |Indien waar, valideert Hallo Windows PowerShell connector of elk script een geldige digitale handtekening heeft. Als het ONWAAR is, zorg ervoor dat Windows PowerShell-uitvoeringsbeleid Hallo synchronisatieservice server RemoteSigned of onbeperkt. |

**Algemene Module**  
Hallo-connector kunt u toostore gedeelde Windows PowerShell-module in Hallo-configuratie. Wanneer het Hallo-connector een script wordt uitgevoerd, hello Windows PowerShell-module is geëxtraheerd toohello bestandssysteem zodat deze kan worden geïmporteerd door elk script.

Voor Import, Export en Wachtwoordsynchronisatie, scripts is de algemene module Hallo uitgepakte toohello-connector MAData map. Voor detectie-scripts, Schema, validatie, hiërarchie en partitie is de algemene module Hallo map uitgepakte toohello % TEMP %. In beide gevallen geëxtraheerd Hallo algemene Module script heeft de naam volgens de instelling van de algemene naam van de Module Script toohello.

een module tooload FIMPowerShellConnectorModule.psm1 aangeroepen vanuit Hallo MAData map, gebruikt u Hallo-instructie:`Import-Module (Join-Path -Path [Microsoft.MetadirectoryServices.MAUtils]::MAFolder -ChildPath "FIMPowerShellConnectorModule.psm1")`

een module tooload FIMPowerShellConnectorModule.psm1 aangeroepen vanuit de map Hallo % TEMP %, gebruikt u Hallo-instructie:`Import-Module (Join-Path -Path $env:TEMP -ChildPath "FIMPowerShellConnectorModule.psm1")`

**De validatie van parameter**  
Hallo validatiescript is een optionele Windows PowerShell-script dat kan worden gebruikt tooensure connector configuratieparameters geleverd door Hallo beheerder zijn geldig. Validerende server, verbindingsreferenties en connectiviteit parameters zijn algemene gebruik van het validatiescript Hallo. Hallo wordt validatiescript aangeroepen nadat hello volgende tabbladen en dialoogvensters worden gewijzigd:

* Connectiviteit
* Globale Parameters
* Partitieconfiguratie

Hallo validatiescript ontvangt Hallo volgende parameters uit Hallo-connector:

| Naam | Gegevenstype | Beschrijving |
| --- | --- | --- |
| ConfigParameterPage |[ConfigParameterPage][cpp] |tabblad Hallo-configuratie of dialoogvenster die Hallo-validatieaanvraag geactiveerd. |
| ConfigParameters |[KeyedCollection] [ keyk] [tekenreeks, [ConfigParameter][cp]] |Tabel met configuratieparameters voor Hallo Connector. |
| Referentie |[PSCredential][pscred] |Bevat alle referenties door Hallo beheerder zijn op Hallo connectiviteit tabblad ingevoerd. |

Hallo validatiescript moet één ParameterValidationResult object toohello pijplijn retourneren.

**Schema-detectie**  
Hallo Schema detectiescript is verplicht. Dit script retourneert Hallo-objecttypen, kenmerken en kenmerk beperkingen die Hallo die synchronisatieservice wordt gebruikt voor het kenmerk stroomregels configureren. Hallo detectiescript Schema wordt uitgevoerd tijdens het maken van connector en Hallo-connector schema gevuld. Dit wordt ook gebruikt door Hallo Schema vernieuwen in Hallo Synchronization Service Manager in te grijpen.

Hallo schema detectiescript ontvangt Hallo volgende parameters uit Hallo-connector:

| Naam | Gegevenstype | Beschrijving |
| --- | --- | --- |
| ConfigParameters |[KeyedCollection] [ keyk] [tekenreeks, [ConfigParameter][cp]] |Tabel met configuratieparameters voor Hallo Connector. |
| Referentie |[PSCredential][pscred] |Bevat alle referenties door Hallo beheerder zijn op Hallo connectiviteit tabblad ingevoerd. |

Hallo script moet een enkel retourneren [Schema] [ schema] object toohello pijplijn. Hallo schemaobject bestaat uit [SchemaType] [ schemaT] objecten die objecttypen vertegenwoordigen (bijvoorbeeld: gebruikers en groepen). Hallo SchemaType object bevat een verzameling van [SchemaAttribute] [ schemaA] -objecten met daarin Hallo kenmerken (bijvoorbeeld: voornaam en achternaam postadres) van het Hallo-type.

**Extra Parameters**  
Bovendien toohello standaard configuratie-instellingen, kunt u aanvullende aangepaste configuratie-instellingen die specifieke toohello exemplaar van Hallo Connector zijn. Deze parameters kunnen worden opgegeven op het Hallo-connector partitie, of Voer stap niveaus en is toegankelijk vanuit Hallo relevante Windows PowerShell-script. Aangepaste configuratie-instellingen kunnen worden opgeslagen in het Hallo-synchronisatieservice database in tekst zonder opmaak of ze kunnen worden versleuteld. Hallo-synchronisatieservice automatisch versleutelt en ontsleutelt veilige configuratie-instellingen, indien nodig.

toospecify aangepaste configuratie-instellingen, afzonderlijke Hallo-naam van elke parameter met een komma (,).

tooaccess aangepaste configuratie-instellingen van een script, moet u achtervoegsel Hallo-naam met een onderstrepingsteken ( \_ ) en het Hallo-bereik van Hallo-parameter (Global, partitie of RunStep). Bijvoorbeeld: tooaccess Hallo globale FileName-parameter, gebruikt u dit codefragment:`$ConfigurationParameters["FileName_Global"].Value`

### <a name="capabilities"></a>Functionaliteit
Hallo mogelijkheden tabblad Hallo Management Agent Designer definieert Hallo gedrag en de functionaliteit van Hallo-connector. Hallo selecties op dit tabblad worden niet gewijzigd wanneer Hallo-connector is gemaakt. Deze tabel bevat instellingen voor apparaatfuncties Hallo.

![Functionaliteit](./media/active-directory-aadconnectsync-connector-powershell/capabilities.png)

| Mogelijkheid | Beschrijving |
| --- | --- |
| [Stijl van de DN-naam][dnstyle] |Hiermee wordt aangegeven als Hallo connector DN-namen ondersteunt en als het geval is, wat stijl. |
| [Type exporteren][exportT] |Hallo type objecten die worden aangeboden toohello exportscript bepaalt. <li>AttributeReplace – omvat Hallo volledige set waarden voor een kenmerk met meerdere waarden wanneer Hallo kenmerk verandert.</li><li>AttributeUpdate – bevat alleen Hallo delta's tooa kenmerk met meerdere waarden als Hallo kenmerk verandert.</li><li>MultivaluedReferenceAttributeUpdate - bevat een volledige set met waarden voor niet-verwijzingsvariant met meerdere waarden kenmerken en alleen delta's voor verwijzingskenmerken met meerdere waarden.</li><li>ObjectReplace – bevat alle kenmerken voor een object wanneer een kenmerk wijzigingen</li> |
| [Gegevensnormalisatie][DataNorm] |Hiermee geeft u Hallo synchronisatieservice toonormalize anker kenmerken voordat ze tooscripts worden aangeboden. |
| [Bevestiging van object][oconf] |Hallo in behandeling zijnde importeren gedrag configureert in Hallo Synchronization Service. <li>Normaal – standaardgedrag die alle geëxporteerde wijzigingen toobe bevestigd via importeren verwacht</li><li>NoDeleteConfirmation – is wanneer een object wordt verwijderd, er geen in behandeling zijnde importeren die zijn gegenereerd.</li><li>NoAddAndDeleteConfirmation – is wanneer een object wordt gemaakt of verwijderd, geen in behandeling zijnde importeren die zijn gegenereerd.</li> |
| DN-naam gebruiken als anker |Als hello Distinguished Name stijl is ingesteld tooLDAP, is Hallo ankerkenmerk voor connectorgebied Hallo ook Hallo DN-naam. |
| Gelijktijdige bewerkingen van verschillende Connectors |Wanneer dit selectievakje inschakelt, kunnen meerdere Windows PowerShell-connectors gelijktijdig uitgevoerd. |
| Partities |Wanneer dit selectievakje inschakelt, wordt Hallo connector ondersteunt meerdere partities en detectie van de partitie. |
| hiërarchie |Wanneer dit selectievakje inschakelt, ondersteunt Hallo connector een hiërarchische structuur voor LDAP-stijl. |
| Importeren inschakelen |Wanneer dit selectievakje inschakelt, importeert Hallo connector gegevens via scripts voor het importeren. |
| Delta-Import inschakelen |Wanneer dit selectievakje inschakelt, kan Hallo connector aanvragen delta's van Hallo scripts importeren. |
| Exporteren inschakelen |Wanneer dit selectievakje inschakelt, exporteert u Hallo connector gegevens via de export-scripts. |
| Volledige exporteren inschakelen |Wanneer dit selectievakje inschakelt, exporteren Hallo scripts ondersteuning exporteren Hallo gehele connectorgebied overgebracht. toouse die deze optie inschakelen exporteren, moet ook worden gecontroleerd. |
| Er is geen referentiewaarden In eerste Export Pass |Wanneer dit selectievakje inschakelt, worden in een tweede stap van de export verwijzingskenmerken geëxporteerd. |
| Wijzig de naam van Object inschakelen |Wanneer dit selectievakje inschakelt, kunnen de DN-namen worden gewijzigd. |
| Als u vervanging verwijderen toevoegen |Wanneer dit selectievakje inschakelt, delete-toevoegen bewerkingen worden geëxporteerd als één vervanging. |
| Wachtwoord Operations inschakelen |Wanneer dit selectievakje inschakelt, worden wachtwoord synchronisatiescripts ondersteund. |
| Wachtwoord van de Export in de eerste keer inschakelen |Wanneer dit selectievakje inschakelt, worden de wachtwoorden zijn ingesteld tijdens het inrichten geëxporteerd wanneer Hallo-object wordt gemaakt. |

### <a name="global-parameters"></a>Globale Parameters
Hallo globale Parameters tabblad in Hallo Management Agent Designer kunt u tooconfigure Hallo Windows PowerShell-scripts die worden uitgevoerd door Hallo-connector. U kunt ook algemene waarden voor aangepaste configuratie-instellingen die zijn gedefinieerd op Hallo connectiviteit tabblad configureren.

**Detectie van de partitie**  
Een partitie is een afzonderlijke naamruimte binnen één gedeelde schema. In Active Directory bijvoorbeeld is elk domein een partitie binnen een forest. Een partitie is een logische groepering van Hallo voor importeren en exporteren van bewerkingen. Importeren en exporteren hebben partitie wat een context en alle bewerkingen in deze context. Partities moeten toorepresent een hiërarchie in LDAP. Hallo DN-naam van een partitie wordt gebruikt in import tooverify dat alle objecten zijn binnen het bereik van een partitie Hallo geretourneerd. Hallo partitie DN-naam wordt ook gebruikt tijdens het inrichten van Hallo metaverse toohello connector ruimte toodetermine Hallo partitie is die een object gekoppeld tijdens het exporteren worden moet.

Hallo partitie detectiescript ontvangt Hallo volgende parameters uit Hallo-connector:

| Naam | Gegevenstype | Beschrijving |
| --- | --- | --- |
| ConfigParameters |[KeyedCollection][keyk][tekenreeks, [ConfigParameter][cp]] |Tabel met configuratieparameters voor Hallo Connector. |
| Referentie |[PSCredential][pscred] |Bevat alle referenties door Hallo beheerder zijn op Hallo connectiviteit tabblad ingevoerd. |

Hallo script moet retourneren een ofwel één [partitie] [ part] object of een lijst [T] van partitie objecten toohello pijplijn.

**Detectie hiërarchieën**  
Hallo hiërarchie detectiescript wordt alleen gebruikt wanneer Hallo Distinguished Name stijl mogelijkheid LDAP is. Hallo-script is gebruikte tooallow u toobrowse en selecteer een set van containers die wordt beschouwd als in of buiten het bereik van importeren en exporteren van bewerkingen. Hallo script dient alleen een lijst met knooppunten die directe onderliggende elementen van Hallo hoofdmap opgegeven toohello knooppuntscript.

Hallo hiërarchie detectiescript ontvangt Hallo volgende parameters uit Hallo-connector:

| Naam | Gegevenstype | Beschrijving |
| --- | --- | --- |
| ConfigParameters |[KeyedCollection][keyk][tekenreeks, [ConfigParameter][cp]] |Tabel met configuratieparameters voor Hallo Connector. |
| Referentie |[PSCredential][pscred] |Bevat alle referenties door Hallo beheerder zijn op Hallo connectiviteit tabblad ingevoerd. |
| ParentNode |[HierarchyNode][hn] |hoofdknooppunt Hallo van Hallo hiërarchie onder welke Hallo script directe onderliggende elementen moet retourneren. |

Hallo script moet een ofwel een HierarchyNode één onderliggend object of een lijst [T] van onderliggende HierarchyNode objecten toohello pijplijn retourneren.

#### <a name="import"></a>Importeren
Connectors die ondersteuning bieden voor importbewerkingen moeten drie scripts implementeren.

**Beginnen met importeren**  
Hallo importeren begint script wordt uitgevoerd op Hallo begin van een stap importeren uitvoert. Tijdens deze stap kunt u tot stand brengen van een verbinding toohello-bronsysteem en voorbereidende stappen uitvoeren voordat het importeren van gegevens van Hallo systeem verbonden.

Hallo importeren begint script ontvangt Hallo volgende parameters uit Hallo-connector:

| Naam | Gegevenstype | Beschrijving |
| --- | --- | --- |
| ConfigParameters |[KeyedCollection][keyk][tekenreeks, [ConfigParameter][cp]] |Tabel met configuratieparameters voor Hallo Connector. |
| Referentie |[PSCredential][pscred] |Bevat alle referenties door Hallo beheerder zijn op Hallo connectiviteit tabblad ingevoerd. |
| OpenImportConnectionRunStep |[OpenImportConnectionRunStep][oicrs] |Hallo script informeert over Hallo type importeren uitvoeren (delta of volledige) partitie, hiërarchie watermerk en verwachte paginagrootte. |
| Typen |[Schema][schema] |Schema voor Hallo connectorruimte die is geïmporteerd. |

Hallo script moet een enkel retourneren [OpenImportConnectionResults] [ oicres] object toohello pipeline, bijvoorbeeld:`Write-Output (New-Object Microsoft.MetadirectoryServices.OpenImportConnectionResults)`

**Gegevens importeren**  
Hallo-importscript gegevens wordt aangeroepen door Hallo connector totdat Hallo script geeft aan dat er geen meer gegevens tooimport. Hallo Windows PowerShell-connector heeft een paginagrootte van 9.999 objecten. Als uw script meer dan 9.999 objecten voor importeren retourneert, moet u ondersteuning voor paginering. Hallo connector gegarandeerd dat een aangepaste eigenschap waarmee u tooa store een watermerk kunt zodat elke keer Hallo importeren script voor gegevens wordt genoemd, uw script hervatten importeren van objecten waarop dit werd afgebroken.

Hallo-importscript gegevens ontvangt Hallo volgende parameters uit Hallo-connector:

| Naam | Gegevenstype | Beschrijving |
| --- | --- | --- |
| ConfigParameters |[KeyedCollection][keyk][tekenreeks, [ConfigParameter][cp]] |Tabel met configuratieparameters voor Hallo Connector. |
| Referentie |[PSCredential][pscred] |Bevat alle referenties door Hallo beheerder zijn op Hallo connectiviteit tabblad ingevoerd. |
| GetImportEntriesRunStep |[ImportRunStep][irs] |Blokkeringen Hallo watermerk (CustomData) die kan worden gebruikt tijdens wisselbare invoer en delta importeert. |
| OpenImportConnectionRunStep |[OpenImportConnectionRunStep][oicrs] |Hallo script informeert over Hallo type importeren uitvoeren (delta of volledige) partitie, hiërarchie watermerk en verwachte paginagrootte. |
| Typen |[Schema][schema] |Schema voor Hallo connectorruimte die is geïmporteerd. |

Hallo importscript gegevens moet schrijven, een lijst [[CSEntryChange][csec]] object toohello pijplijn. Deze verzameling bestaat uit CSEntryChange kenmerken voor elk object dat wordt geïmporteerd. Deze verzameling moet een volledige set met CSEntryChange-objecten met alle kenmerken voor elk object hebben tijdens de uitvoering van een volledige Import. Tijdens een Delta-Import moet Hallo CSEntryChange object Hallo kenmerk niveau delta's voor elke tooimport object of een volledige weergave van Hallo-objecten die zijn gewijzigd (modus vervangen) bevatten.

**Einde importeren**  
Op Hallo sluiting van Hallo importeren uitvoert, wordt Hallo End importeren script uitgevoerd. Dit script moet een Opschoningstaken nodig (bijvoorbeeld sluiten verbindingen toosystems en gereageerd had toofailures) uitvoeren.

Hallo end importscript ontvangt Hallo volgende parameters uit Hallo-connector:

| Naam | Gegevenstype | Beschrijving |
| --- | --- | --- |
| ConfigParameters |[KeyedCollection][keyk][tekenreeks, [ConfigParameter][cp]] |Tabel met configuratieparameters voor Hallo Connector. |
| Referentie |[PSCredential][pscred] |Bevat alle referenties door Hallo beheerder zijn op Hallo connectiviteit tabblad ingevoerd. |
| OpenImportConnectionRunStep |[OpenImportConnectionRunStep][oicrs] |Hallo script informeert over Hallo type importeren uitvoeren (delta of volledige) partitie, hiërarchie watermerk en verwachte paginagrootte. |
| CloseImportConnectionRunStep |[CloseImportConnectionRunStep][cecrs] |Hallo script informeert over Hallo reden Hallo import is beëindigd. |

Hallo script moet een enkel retourneren [CloseImportConnectionResults] [ cicres] object toohello pipeline, bijvoorbeeld:`Write-Output (New-Object Microsoft.MetadirectoryServices.CloseImportConnectionResults)`

#### <a name="export"></a>Exporteren
Identieke toohello importeren architectuur van Hallo-connector, connectors die ondersteuning bieden voor uitvoer moeten drie scripts implementeren.

**Begin exporteren**  
Hallo begint export script wordt uitgevoerd op Hallo begin van een stap exporteren worden uitgevoerd. Tijdens deze stap kunt u tot stand brengen van een verbinding toohello-bronsysteem en eventuele voorbereidende stappen uitvoeren voordat het exporteren van gegevens toohello verbonden systeem.

Hallo begint export script ontvangt Hallo volgende parameters uit Hallo-connector:

| Naam | Gegevenstype | Beschrijving |
| --- | --- | --- |
| ConfigParameters |[KeyedCollection][keyk][tekenreeks, [ConfigParameter][cp]] |Tabel met configuratieparameters voor Hallo Connector. |
| Referentie |[PSCredential][pscred] |Bevat alle referenties door Hallo beheerder zijn op Hallo connectiviteit tabblad ingevoerd. |
| OpenExportConnectionRunStep |[OpenExportConnectionRunStep][oecrs] |Hallo script informeert over Hallo type export uitvoeren (delta of volledige) partitie, hiërarchie en verwachte paginagrootte. |
| Typen |[Schema][schema] |Schema voor Hallo connectorruimte die wordt geëxporteerd. |

Hallo script moet worden eventuele uitvoer toohello pijplijn niet geretourneerd.

**Gegevens exporteren**  
Hallo-synchronisatieservice roept Hallo gegevens exporteren script zo vaak als nodig tooprocess alle in behandeling zijnde uitvoer is. Als Hallo connectorgebied overgebracht meer in behandeling zijnde uitvoer heeft dan de paginagrootte van connector hello, Hallo Hallo export script voor gegevens mogelijk meerdere keren worden aangeroepen en mogelijk meerdere keren voor hetzelfde object.

Hallo-exportscript gegevens ontvangt Hallo volgende parameters uit Hallo-connector:

| Naam | Gegevenstype | Beschrijving |
| --- | --- | --- |
| ConfigParameters |[KeyedCollection][keyk][tekenreeks, [ConfigParameter][cp]] |Tabel met configuratieparameters voor Hallo Connector. |
| Referentie |[PSCredential][pscred] |Bevat alle referenties door Hallo beheerder zijn op Hallo connectiviteit tabblad ingevoerd. |
| CSEntries |IList[CSEntryChange][csec] |Lijst met alle Hallo connectorruimte objecten met in behandeling zijnde uitvoer toobe verwerkt tijdens deze fase. |
| OpenExportConnectionRunStep |[OpenExportConnectionRunStep][oecrs] |Hallo script informeert over Hallo type export uitvoeren (delta of volledige) partitie, hiërarchie en verwachte paginagrootte. |
| Typen |[Schema][schema] |Schema voor Hallo connectorruimte die wordt geëxporteerd. |

Hallo exportscript gegevens moet retourneren een [PutExportEntriesResults] [ peeres] object toohello pijplijn. Dit object heeft geen tooinclude resultaat informatie nodig voor elk geëxporteerde connector tenzij er een fout of een wijziging toohello-ankerkenmerk optreedt. Bijvoorbeeld, tooreturn een PutExportEntriesResults object toohello pijplijn:`Write-Output (New-Object Microsoft.MetadirectoryServices.PutExportEntriesResults)`

**Einde exporteren**  
Hallo-conclusie van Hallo uitvoer uitvoeren, Hallo script toorun End exporteren. Dit script moet een Opschoningstaken nodig (bijvoorbeeld sluiten verbindingen toosystems en gereageerd had toofailures) uitvoeren.

Hallo end exportscript ontvangt Hallo volgende parameters uit Hallo-connector:

| Naam | Gegevenstype | Beschrijving |
| --- | --- | --- |
| ConfigParameters |[KeyedCollection][keyk][tekenreeks, [ConfigParameter][cp]] |Tabel met configuratieparameters voor Hallo Connector. |
| Referentie |[PSCredential][pscred] |Bevat alle referenties door Hallo beheerder zijn op Hallo connectiviteit tabblad ingevoerd. |
| OpenExportConnectionRunStep |[OpenExportConnectionRunStep][oecrs] |Hallo script informeert over Hallo type export uitvoeren (delta of volledige) partitie, hiërarchie en verwachte paginagrootte. |
| CloseExportConnectionRunStep |[CloseExportConnectionRunStep][cecrs] |Hallo script informeert over Hallo reden Hallo exporteren is beëindigd. |

Hallo script moet worden eventuele uitvoer toohello pijplijn niet geretourneerd.

#### <a name="password-synchronization"></a>Wachtwoordsynchronisatie
Windows PowerShell-connectors kunnen worden gebruikt als doel voor wachtwoorden wijzigingen.

Hallo wachtwoord script ontvangt Hallo volgende parameters uit Hallo-connector:

| Naam | Gegevenstype | Beschrijving |
| --- | --- | --- |
| ConfigParameters |[KeyedCollection][keyk][tekenreeks, [ConfigParameter][cp]] |Tabel met configuratieparameters voor Hallo Connector. |
| Referentie |[PSCredential][pscred] |Bevat alle referenties door Hallo beheerder zijn op Hallo connectiviteit tabblad ingevoerd. |
| Partitie |[Partitie][part] |Directorypartitie die Hallo CSEntry heeft. |
| CSEntry |[CSEntry][cse] |Connector ruimte vermelding voor Hallo-object dat is ontvangen een wachtwoord wijzigen of opnieuw instellen. |
| OperationType |Tekenreeks |Hiermee wordt aangegeven of Hallo-bewerking opnieuw instellen (**SetPassword**) of een wijziging (**ChangePassword**). |
| PasswordOptions |[PasswordOptions][pwdopt] |Vlaggen die Hallo aangeven bedoeld gedrag voor wachtwoord opnieuw instellen. Deze parameter is alleen beschikbaar als OperationType **SetPassword**. |
| OudWachtwoord |Tekenreeks |Ingevuld met oud wachtwoord voor wachtwoordwijzigingen Hallo-object. Deze parameter is alleen beschikbaar als OperationType **ChangePassword**. |
| NieuwWachtwoord |Tekenreeks |Ingevuld met het nieuwe wachtwoord Hallo-object die Hallo script moet worden ingesteld. |

Hallo wachtwoord script is niet de verwachte tooreturn eventuele resultaten toohello Windows PowerShell-pijplijn. Als er een fout optreedt in Hallo wachtwoord script moet een van de volgende uitzonderingen tooinform Hallo synchronisatieservice over Hallo probleem Hallo Hallo script genereert:

* [PasswordPolicyViolationException] [ pwdex1] – gegenereerd als het Hallo-wachtwoord niet voldoet aan het wachtwoordbeleid Hallo in Hallo verbonden systeem.
* [PasswordIllFormedException] [ pwdex2] – gegenereerd als het Hallo-wachtwoord is niet geschikt voor Hallo verbonden systeem.
* [PasswordExtension] [ pwdex3] – gegenereerd voor alle andere fouten in Hallo wachtwoord script.

## <a name="sample-connectors"></a>Voorbeeld-Connectors
Zie voor een volledig overzicht van Hallo beschikbaar voorbeeld connectors [Windows PowerShell Connector voorbeeld Connector verzameling][samp].

## <a name="other-notes"></a>Aanvullende opmerkingen
### <a name="additional-configuration-for-impersonation"></a>Aanvullende configuratie voor imitatie
Hallo-gebruiker die geïmiteerde hello volgende machtigingen op Hallo synchronisatieservice server verlenen:

Leestoegang toohello volgende registersleutels:

* HKEY_USERS\\\Software\Microsoft\PowerShell [SynchronizationServiceServiceAccountSID]
* HKEY_USERS\\\Environment [SynchronizationServiceServiceAccountSID]

toodetermine hello SID (Security Identifier) van Hallo Synchronization Service-serviceaccount, Hallo volgende PowerShell-opdrachten uitvoeren:

```
$account = New-Object System.Security.Principal.NTAccount "<domain>\<username>"
$account.Translate([System.Security.Principal.SecurityIdentifier]).Value
```

Leestoegang toohello mappen van het bestandssysteem te volgen:

* %ProgramFiles%\Microsoft forefront Identity Manager\2010\Synchronization Service\Extensions
* %ProgramFiles%\Microsoft forefront Identity Manager\2010\Synchronization Service\ExtensionsCache
* %ProgramFiles%\Microsoft forefront Identity Manager\2010\Synchronization Service\MaData\\{ConnectorName}

Hallo-naam van Hallo Windows PowerShell connector voor tijdelijke aanduiding voor Hallo {ConnectorName} vervangen.

## <a name="troubleshooting"></a>Problemen oplossen
* Zie voor informatie over hoe logboekregistratie tooenable tootroubleshoot connector Hallo Hallo [hoe tooEnable ETW-tracering voor Connectors](http://go.microsoft.com/fwlink/?LinkId=335731).

<!--Reference style links - using these makes hello source content way more readable than using inline links-->
[cpp]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.configparameterpage.aspx
[keyk]: https://msdn.microsoft.com/library/ms132438.aspx
[cp]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.configparameter.aspx
[pscred]: https://msdn.microsoft.com/library/system.management.automation.pscredential.aspx
[schema]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.schema.aspx
[schemaT]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.schematype.aspx
[schemaA]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.schemaattribute.aspx
[dnstyle]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.madistinguishednamestyle.aspx
[exportT]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.maexporttype.aspx
[DataNorm]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.manormalizations.aspx
[oconf]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.maobjectconfirmation.aspx
[dw]: https://msdn.microsoft.com/library/windows/desktop/aa378184.aspx
[part]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.partition.aspx
[hn]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.hierarchynode.aspx
[oicrs]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.openimportconnectionrunstep.aspx
[cecrs]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.closeexportconnectionrunstep.aspx
[oicres]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.openimportconnectionresults.aspx
[cecrs]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.closeexportconnectionrunstep.aspx
[cicres]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.closeimportconnectionresults.aspx
[oecrs]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.openexportconnectionrunstep.aspx
[irs]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.importrunstep.aspx
[cse]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.csentry.aspx
[csec]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.csentrychange.aspx
[peeres]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.putexportentriesresults.aspx
[pwdopt]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.passwordoptions.aspx
[pwdex1]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.passwordpolicyviolationexception.aspx
[pwdex2]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.passwordillformedexception.aspx
[pwdex3]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.passwordextensionexception.aspx
[samp]: http://go.microsoft.com/fwlink/?LinkId=394291

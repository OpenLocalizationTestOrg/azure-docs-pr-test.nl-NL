---
title: Validatie - Microsoft Threat Modeling Tool - Azure aaaInput | Microsoft Docs
description: oplossingen voor bedreigingen die worden weergegeven in Hallo Threat Modeling hulpprogramma
services: security
documentationcenter: na
author: RodSan
manager: RodSan
editor: RodSan
ms.assetid: na
ms.service: security
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: rodsan
ms.openlocfilehash: 823503881f4bae292ef021834d5e64acf2a0f54a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="security-frame-input-validation--mitigations"></a>Beveiliging Frame: Invoervalidatie | Oplossingen 
| Product/Service | Artikel |
| --------------- | ------- |
| **Webtoepassing** | <ul><li>[Schakel XSLT uitvoeren van scripts voor alle transformaties met behulp van niet-vertrouwde opmaakmodellen](#disable-xslt)</li><li>[Zorg ervoor dat elke pagina waarvan de gebruiker instelbare inhoud buiten automatische MIME-controle kiest](#out-sniffing)</li><li>[Beperken of XML-entiteit omzetting uitschakelen](#xml-resolution)</li><li>[Toepassingen die gebruikmaken van http.sys uitvoeren URL standaardisatie verificatie](#app-verification)</li><li>[Zorg passende controles zijn geïmplementeerd tijdens het accepteren van bestanden van gebruikers](#controls-users)</li><li>[Zorg ervoor dat type veilig parameters in webtoepassing worden gebruikt voor toegang tot gegevens](#typesafe)</li><li>[Afzonderlijke model binding klassen of massaopslag toewijzing beveiligingslek in het filter lijsten tooprevent MVC-binding gebruiken](#binding-mvc)</li><li>[Niet-vertrouwde web uitvoer voorafgaande toorendering coderen](#rendering)</li><li>[Validatie voor invoer- en filteren op alle tekenreekstype modeleigenschappen uitvoeren](#typemodel)</li><li>[Opschoning moet worden toegepast op formuliervelden die tekens, bijvoorbeeld, RTF-editor accepteren](#richtext)</li><li>[DOM elementen toosinks waarvoor geen ingebouwde codering niet toe te wijzen](#inbuilt-encode)</li><li>[Valideer alle omleidingen in toepassing hello zijn gesloten of veilig gedaan](#redirect-safe)</li><li>[Validatie voor invoer op alle tekenreeks typeparameters geaccepteerd door de methoden van de domeincontroller implementeren](#string-method)</li><li>[Time-out voor bovengrens instellen voor reguliere expressie voor het verwerken van tooprevent DoS vanwege toobad reguliere expressies](#dos-expression)</li><li>[Vermijd het gebruik van Html.Raw in Razor weergaven](#html-razor)</li></ul> | 
| **Database** | <ul><li>[Gebruik geen dynamische query's in de opgeslagen procedures](#stored-proc)</li></ul> |
| **Web-API** | <ul><li>[Zorg ervoor dat de validatie is uitgevoerd voor Web-API-methoden](#validation-api)</li><li>[Validatie voor invoer op alle tekenreeks typeparameters geaccepteerd door de methoden van de Web-API implementeren](#string-api)</li><li>[Zorg ervoor dat type veilig parameters in Web-API worden gebruikt voor toegang tot gegevens](#typesafe-api)</li></ul> | 
| **Azure Documentdb** | <ul><li>[SQL-query's constructorreeks mag gebruiken voor DocumentDB](#sql-docdb)</li></ul> | 
| **WCF** | <ul><li>[Validatie van de WCF-invoer via schemabinding](#schema-binding)</li><li>[Validatie van de WCF - invoer via Parameter Inspectors](#parameters)</li></ul> |

## <a id="disable-xslt"></a>Schakel XSLT uitvoeren van scripts voor alle transformaties met behulp van niet-vertrouwde opmaakmodellen

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Webtoepassing | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | Algemene |
| **Kenmerken**              | N.v.t.  |
| **Verwijzingen**              | [Beveiliging van de XSLT-](https://msdn.microsoft.com/library/ms763800(v=vs.85).aspx), [eigenschap XsltSettings.EnableScript](http://msdn.microsoft.com/library/system.xml.xsl.xsltsettings.enablescript.aspx) |
| **Stappen** | XSLT ondersteunt scripting binnen StyleSheets Hallo met `<msxml:script>` element. Hiermee kunt aangepaste functies toobe gebruikt in een XSLT-transformatie. Hallo-script wordt uitgevoerd in de context Hallo van Hallo proces Hallo transformatie uitvoeren. XSLT-script moet worden uitgeschakeld in de uitvoering van een niet-vertrouwde omgeving tooprevent van niet-vertrouwde code. *Als met .NET:* XSLT-scripting is standaard uitgeschakeld; echter, moet u ervoor zorgen dat deze is niet expliciet ingeschakeld via Hallo `XsltSettings.EnableScript` eigenschap.|

### <a name="example"></a>Voorbeeld 

```C#
XsltSettings settings = new XsltSettings();
settings.EnableScript = true; // WRONG: THIS SHOULD BE SET toofalse
```

### <a name="example"></a>Voorbeeld
Als u met behulp van MSXML 6.0, is XSLT-scripting standaard uitgeschakeld. echter, moet u ervoor zorgen dat deze is niet expliciet ingeschakeld via de eigenschap AllowXsltScript van Hallo XML DOM-object. 

```C#
doc.setProperty("AllowXsltScript", true); // WRONG: THIS SHOULD BE SET toofalse
```

### <a name="example"></a>Voorbeeld
Als u van MSXML 5 gebruikmaakt of hieronder XSLT-scripting is standaard ingeschakeld en u expliciet moet uitschakelen. Hallo XML DOM-object eigenschap AllowXsltScript toofalse ingesteld. 

```C#
doc.setProperty("AllowXsltScript", false); // CORRECT. Setting toofalse disables XSLT scripting.
```

## <a id="out-sniffing"></a>Zorg ervoor dat elke pagina waarvan de gebruiker instelbare inhoud buiten automatische MIME-controle kiest

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Webtoepassing | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | Algemene |
| **Kenmerken**              | N.v.t.  |
| **Verwijzingen**              | [IE8 Beveiliging deel V - Uitgebreide beveiliging](http://blogs.msdn.com/ie/archive/2008/07/02/ie8-security-part-v-comprehensive-protection.aspx)  |
| **Stappen** | <p>Voor elke pagina die gebruiker instelbare inhoud kan bevatten, moet u HTTP-Header Hallo `X-Content-Type-Options:nosniff`. toocomply aan deze eis wordt voldaan, kunt u een set Hallo vereiste header per pagina voor deze pagina's die mogelijk door de gebruiker instelbare inhoud bevatten of u kunt deze globaal instellen voor alle pagina's in de toepassing hello.</p><p>Elk type bestand geleverd door een webserver heeft een bijbehorende [MIME-type](http://en.wikipedia.org/wiki/Mime_type) (ook wel een *inhoudstype*) die worden beschreven Hallo aard van Hallo-inhoud (dat wil zeggen, image, tekst, toepassing, enz.)</p><p>Hallo X-inhoud--opties voor het Type-header is een HTTP-header waarmee ontwikkelaars toospecify dat zijn inhoud mag geen MIME-sniff. Deze header is ontworpen toomitigate bekijken van MIME-aanvallen. Ondersteuning voor deze header is toegevoegd in Internet Explorer 8 (IE8)</p><p>Alleen gebruikers van Internet Explorer 8 (IE8) profiteren van de X-inhoud-Type-opties. Vorige versies van Internet Explorer bieden momenteel geen ondersteuning voor Hallo X-inhoud--opties voor het Type-header</p><p>Internet Explorer 8 (of hoger) zijn alleen belangrijke browsers tooimplement MIME-bekijken opt-out functie Hallo. Als andere belangrijke browsers (Firefox, Safari, Chrome) soortgelijke functies implementeren, worden deze aanbeveling bijgewerkte tooinclude syntaxis voor deze browsers ook</p>|

### <a name="example"></a>Voorbeeld
tooenable hello vereiste header globaal voor alle pagina's in de toepassing hello, kunt u een van de volgende Hallo kunt doen: 

* Hallo-header in Hallo web.config-bestand toevoegen als de toepassing hello wordt gehost door Internet Information Services (IIS) 7 

```
<system.webServer> 
  <httpProtocol> 
    <customHeaders> 
      <add name=""X-Content-Type-Options"" value=""nosniff""/>
    </customHeaders>
  </httpProtocol>
</system.webServer> 
```

* Hallo-header via Hallo toevoegen globale toepassing\_BeginRequest 

``` 
void Application_BeginRequest(object sender, EventArgs e)
{
  this.Response.Headers[""X-Content-Type-Options""] = ""nosniff"";
} 
```

* Aangepaste HTTP-module implementeren 

``` 
public class XContentTypeOptionsModule : IHttpModule 
  {
    #region IHttpModule Members 
    public void Dispose() 
    { 

    } 
    public void Init(HttpApplication context)
    { 
      context.PreSendRequestHeaders += newEventHandler(context_PreSendRequestHeaders); 
    } 
    #endregion 
    void context_PreSendRequestHeaders(object sender, EventArgs e) 
      { 
        HttpApplication application = sender as HttpApplication; 
        if (application == null) 
          return; 
        if (application.Response.Headers[""X-Content-Type-Options ""] != null) 
          return; 
        application.Response.Headers.Add(""X-Content-Type-Options "", ""nosniff""); 
      } 
  } 

``` 

* Door deze toe te voegen tooindividual reacties kunt u de vereiste header Hallo alleen voor specifieke's inschakelen: 

```
this.Response.Headers[""X-Content-Type-Options""] = ""nosniff""; 
``` 

## <a id="xml-resolution"></a>Beperken of XML-entiteit omzetting uitschakelen

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Webtoepassing | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | Algemene |
| **Kenmerken**              | N.v.t.  |
| **Verwijzingen**              | [XML-entiteit uitbreiding](http://capec.mitre.org/data/definitions/197.html), [XML Denial of Service-aanvallen en beveiliging](http://msdn.microsoft.com/magazine/ee335713.aspx), [MSXML beveiligingsoverzicht](http://msdn.microsoft.com/library/ms754611(v=VS.85).aspx), [aanbevolen procedures voor het beveiligen van MSXML Code](http://msdn.microsoft.com/library/ms759188(VS.85).aspx), [NSXMLParserDelegate Protocolnaslaginformatie](http://developer.apple.com/library/ios/#documentation/cocoa/reference/NSXMLParserDelegate_Protocol/Reference/Reference.html), [het omzetten van externe verwijzingen](https://msdn.microsoft.com/library/5fcwybb2.aspx) |
| **Stappen**| <p>Hoewel deze optie niet veel gebruikt is, is er een functie van XML waarmee Hallo XML-parser tooexpand macro entiteiten met waarden die zijn gedefinieerd binnen het Hallo-document zelf of van externe bronnen. Hallo-document kan bijvoorbeeld een entiteit 'NaamBedrijf' Hallo-waarde 'Microsoft', definiëren, zodat telkens wanneer de tekst hello '&companyname;' wordt weergegeven in het Hallo-document, wordt deze automatisch vervangen door de tekst hello Microsoft. Of Hallo document een entiteit 'MSFTStock' dat verwijst naar een externe service toofetch Hallo huidige waarde van Microsoft stock kunt definiëren.</p><p>Klik op elk gewenst moment '&MSFTStock;' wordt weergegeven in het Hallo-document, wordt deze automatisch vervangen door de huidige aandelenkoersen Hallo. Deze functionaliteit kan echter zijn dat het doelwit toocreate denial of service (DoS) voorwaarden. Een aanvaller kan meerdere entiteiten toocreate een uitbreiding van de exponentiële XML bomb die al het beschikbare geheugen op Hallo systeem verbruikt nesten. </p><p>U kunt ook hij een oneindige hoeveelheid gegevens kunt maken voor een externe verwijzing die back-streams of die eenvoudig hello thread is vastgelopen. Als gevolg hiervan moeten alle teams interne en/of externe XML-entiteit resolutie uitschakelen volledig als de toepassing niet worden gebruikt of handmatig Hallo hoeveelheid geheugen en het tijdstip waarop de toepassing hello voor het omzetten van de entiteit gebruiken kan als deze functionaliteit is beperken dit echt nodig is. Als de omzetting van de entiteit niet door uw toepassing vereist is, klikt u vervolgens het uitschakelen. </p>|

### <a name="example"></a>Voorbeeld
Voor .NET Framework-code, kunt u Hallo benaderingen te volgen:

```C#
XmlTextReader reader = new XmlTextReader(stream);
reader.ProhibitDtd = true;

XmlReaderSettings settings = new XmlReaderSettings();
settings.ProhibitDtd = true;
XmlReader reader = XmlReader.Create(stream, settings);

// for .NET 4
XmlReaderSettings settings = new XmlReaderSettings();
settings.DtdProcessing = DtdProcessing.Prohibit;
XmlReader reader = XmlReader.Create(stream, settings);
```
Houd er rekening mee dat standaardwaarde Hallo van `ProhibitDtd` in `XmlReaderSettings` is ingesteld op true, maar in `XmlTextReader` ONWAAR is. Als u XmlReaderSettings gebruikt, hoeft u geen tooset ProhibitDtd tootrue expliciet, maar het wordt aanbevolen voor veiligheid verjaardagen doen. Let op: Hallo XmlDocument-klasse kunt ook entiteit resolutie standaard. 

### <a name="example"></a>Voorbeeld
toodisable entiteit omzetting voor XmlDocuments, gebruik Hallo `XmlDocument.Load(XmlReader)` overbelasting van de Hallo methode laden en Hallo juiste eigenschappen instellen in Hallo XmlReader argument toodisable resolutie, zoals geïllustreerd in de volgende code Hallo: 

```C#
XmlReaderSettings settings = new XmlReaderSettings();
settings.ProhibitDtd = true;
XmlReader reader = XmlReader.Create(stream, settings);
XmlDocument doc = new XmlDocument();
doc.Load(reader);
```

### <a name="example"></a>Voorbeeld
Als uitschakelen van de omzetting van de entiteit niet mogelijk voor uw toepassing is, Hallo XmlReaderSettings.MaxCharactersFromEntities eigenschap tooa redelijke waarde instellen op basis van de behoeften van de toepassing tooyour. Hiermee beperkt u Hallo gevolgen van het potentiële exponentiële uitbreiding DoS-aanvallen. Hallo volgende code toont een voorbeeld van deze benadering: 

```C#
XmlReaderSettings settings = new XmlReaderSettings();
settings.ProhibitDtd = false;
settings.MaxCharactersFromEntities = 1000;
XmlReader reader = XmlReader.Create(stream, settings);
```

### <a name="example"></a>Voorbeeld
Als u tooresolve inline entiteiten moet, maar geen tooresolve externe entiteiten hoeft, stelt u Hallo XmlReaderSettings.XmlResolver eigenschap toonull. Bijvoorbeeld: 

```C#
XmlReaderSettings settings = new XmlReaderSettings();
settings.ProhibitDtd = false;
settings.MaxCharactersFromEntities = 1000;
settings.XmlResolver = null;
XmlReader reader = XmlReader.Create(stream, settings);
```
Houd er rekening mee dat in MSXML6, ProhibitDTD tootrue (DTD-verwerking uitschakelen) standaard ingesteld. Apple iOS-OS x-code, er zijn twee XML-parsers kunt u: NSXMLParser en libXML2. 

## <a id="app-verification"></a>Toepassingen die gebruikmaken van http.sys uitvoeren URL standaardisatie verificatie

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Webtoepassing | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | Algemene |
| **Kenmerken**              | N.v.t.  |
| **Verwijzingen**              | N.v.t.  |
| **Stappen** | <p>Een toepassing die gebruikmaakt van http.sys moet als volgt:</p><ul><li>Hallo URL-lengte toono meer dan 16.384 tekens (ASCII of Unicode) beperken. Dit is Hallo absolute maximale URL-lengte op basis van de standaardinstelling voor Internet Information Services (IIS) 6 Hallo. Websites moeten streven voor korter is dan deze indien mogelijk</li><li>Hallo standaard .NET Framework i/o-bestand klassen (zoals FileStream) gebruiken, zoals deze van Hallo-regels in Hallo .NET FX profiteren</li><li>Expliciet samen een toestaan-lijst met bekende bestandsnamen</li><li>Expliciet afwijzen bekende bestandstypen die u niet voor de UrlScan geweigerd: exe, bat-, cmd, com, htw, ida, idq, htr, idc, shtm-[l], stm, printer, ini, pol, dat bestanden</li><li>Catch Hallo volgende uitzonderingen:<ul><li>System.ArgumentException (voor apparaatnamen)</li><li>System.NotSupportedException (voor gegevensstromen)</li><li>System.IO.FileNotFoundException (voor ongeldige escape-teken bestandsnamen)</li><li>System.IO.DirectoryNotFoundException (voor ongeldige escape-teken dir-opdrachten)</li></ul></li><li>*Geen* tooWin32 bestand I/O APIs houden. Op een ongeldige URL probleemloos retourneert een 400-fout toohello gebruiker en Hallo echte fout vastgelegd.</li></ul>|

## <a id="controls-users"></a>Zorg passende controles zijn geïmplementeerd tijdens het accepteren van bestanden van gebruikers

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Webtoepassing | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | Algemene |
| **Kenmerken**              | N.v.t.  |
| **Verwijzingen**              | [Bestand uploaden onbeperkte](https://www.owasp.org/index.php/Unrestricted_File_Upload), [bestand handtekening tabel](http://www.garykessler.net/library/file_sigs.html) |
| **Stappen** | <p>Geüploade bestanden vertegenwoordigen een aanzienlijke risico tooapplications.</p><p>Hallo eerste stap bij veel aanvallen is tooget sommige code toohello system toobe aangevallen. Hallo-aanval moet vervolgens alleen toofind een manier tooget Hallo-code die wordt uitgevoerd. Met uploaden van een bestand, kunt u Hallo aanvaller Hallo eerste stap bereiken. Hallo gevolgen van het uploaden van een bestand kunnen variëren, met inbegrip van volledige systeem overname, een overbelaste bestandssysteem of het doorsturen van aanvallen tooback-end-systemen en eenvoudige defacement-database.</p><p>Dit is afhankelijk van welke toepassing hello komt met Hallo geüpload bestand en vooral waar het is opgeslagen. Server side validatie van bestandsuploads ontbreekt. Volgende beveiligingsmechanismen moet worden geïmplementeerd voor functionaliteit bestand laden:</p><ul><li>Extensie bestandscontrole (een geldige reeks toegestane bestandstype moet worden geaccepteerd)</li><li>Limiet voor de maximale grootte</li><li>Bestand mag geen geüploade toowebroot; Hallo-locatie moet een map op niet-systeemstation</li><li>Naamgevingsconventie moet worden aangehouden zodat hello geüploade bestandsnaam hebben sommige aanvraaggrootte, dus als tooprevent bestand worden overschreven</li><li>Bestanden moeten worden gecontroleerd voor anti-virus voordat toohello schijf worden geschreven</li><li>Zorg ervoor dat Hallo-bestandsnaam en andere metagegevens (zoals een bestandspad) worden gevalideerd voor schadelijke tekens</li><li>Indeling van bestandshandtekening moet worden gecontroleerd, tooprevent een gebruiker vanuit een masqueraded bestand uploaden (bijvoorbeeld een exe-bestand uploaden door het wijzigen van de extensie tootxt)</li></ul>| 

### <a name="example"></a>Voorbeeld
Raadpleeg voor laatste punt Hallo met betrekking tot de validatie van handtekening bestand, toohello klasse hieronder voor meer informatie: 

```C#
        private static Dictionary<string, List<byte[]>> fileSignature = new Dictionary<string, List<byte[]>>
                    {
                    { ".DOC", new List<byte[]> { new byte[] { 0xD0, 0xCF, 0x11, 0xE0, 0xA1, 0xB1, 0x1A, 0xE1 } } },
                    { ".DOCX", new List<byte[]> { new byte[] { 0x50, 0x4B, 0x03, 0x04 } } },
                    { ".PDF", new List<byte[]> { new byte[] { 0x25, 0x50, 0x44, 0x46 } } },
                    { ".ZIP", new List<byte[]> 
                                            {
                                              new byte[] { 0x50, 0x4B, 0x03, 0x04 },
                                              new byte[] { 0x50, 0x4B, 0x4C, 0x49, 0x54, 0x55 },
                                              new byte[] { 0x50, 0x4B, 0x53, 0x70, 0x58 },
                                              new byte[] { 0x50, 0x4B, 0x05, 0x06 },
                                              new byte[] { 0x50, 0x4B, 0x07, 0x08 },
                                              new byte[] { 0x57, 0x69, 0x6E, 0x5A, 0x69, 0x70 }
                                                }
                                            },
                    { ".PNG", new List<byte[]> { new byte[] { 0x89, 0x50, 0x4E, 0x47, 0x0D, 0x0A, 0x1A, 0x0A } } },
                    { ".JPG", new List<byte[]>
                                    {
                                              new byte[] { 0xFF, 0xD8, 0xFF, 0xE0 },
                                              new byte[] { 0xFF, 0xD8, 0xFF, 0xE1 },
                                              new byte[] { 0xFF, 0xD8, 0xFF, 0xE8 }
                                    }
                                    },
                    { ".JPEG", new List<byte[]>
                                        { 
                                            new byte[] { 0xFF, 0xD8, 0xFF, 0xE0 },
                                            new byte[] { 0xFF, 0xD8, 0xFF, 0xE2 },
                                            new byte[] { 0xFF, 0xD8, 0xFF, 0xE3 }
                                        }
                                        },
                    { ".XLS", new List<byte[]>
                                            {
                                              new byte[] { 0xD0, 0xCF, 0x11, 0xE0, 0xA1, 0xB1, 0x1A, 0xE1 },
                                              new byte[] { 0x09, 0x08, 0x10, 0x00, 0x00, 0x06, 0x05, 0x00 },
                                              new byte[] { 0xFD, 0xFF, 0xFF, 0xFF }
                                            }
                                            },
                    { ".XLSX", new List<byte[]> { new byte[] { 0x50, 0x4B, 0x03, 0x04 } } },
                    { ".GIF", new List<byte[]> { new byte[] { 0x47, 0x49, 0x46, 0x38 } } }
                };

        public static bool IsValidFileExtension(string fileName, byte[] fileData, byte[] allowedChars)
        {
            if (string.IsNullOrEmpty(fileName) || fileData == null || fileData.Length == 0)
            {
                return false;
            }

            bool flag = false;
            string ext = Path.GetExtension(fileName);
            if (string.IsNullOrEmpty(ext))
            {
                return false;
            }

            ext = ext.ToUpperInvariant();

            if (ext.Equals(".TXT") || ext.Equals(".CSV") || ext.Equals(".PRN"))
            {
                foreach (byte b in fileData)
                {
                    if (b > 0x7F)
                    {
                        if (allowedChars != null)
                        {
                            if (!allowedChars.Contains(b))
                            {
                                return false;
                            }
                        }
                        else
                        {
                            return false;
                        }
                    }
                }

                return true;
            }

            if (!fileSignature.ContainsKey(ext))
            {
                return true;
            }

            List<byte[]> sig = fileSignature[ext];
            foreach (byte[] b in sig)
            {
                var curFileSig = new byte[b.Length];
                Array.Copy(fileData, curFileSig, b.Length);
                if (curFileSig.SequenceEqual(b))
                {
                    flag = true;
                    break;
                }
            }

            return flag;
        }
```

## <a id="typesafe"></a>Zorg ervoor dat type veilig parameters in webtoepassing worden gebruikt voor toegang tot gegevens

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Webtoepassing | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | Algemene |
| **Kenmerken**              | N.v.t.  |
| **Verwijzingen**              | N.v.t.  |
| **Stappen** | <p>Als u de parameterverzameling Hallo gebruikt, is SQL beschouwen Hallo invoer als een letterlijke waarde in plaats als uitvoerbare code. Hallo parameterverzameling kan gebruikte tooenforce type en de lengte-beperkingen voor de invoergegevens zijn. Waarden die buiten het bereik van Hallo activeren een uitzondering. Als u geen type-safe SQL-parameters gebruikt, mogelijk aanvallers kunnen tooexecute injectieaanvallen die zijn ingesloten in de invoer Hallo niet gefilterd.</p><p>Gebruik veilige typeparameters wanneer tooavoid mogelijk SQL-injectieaanvallen die zich met ongefilterde invoer voordoen kunnen construeren SQL query. U kunt veilig typeparameters met opgeslagen procedures en dynamische SQL-instructies. Parameters worden behandeld als letterlijke waarden door Hallo-database en niet als uitvoerbare code. Parameters zijn ook gecontroleerd op type en de lengte.</p>|

### <a name="example"></a>Voorbeeld 
Hallo volgende code toont hoe toouse Typ veilige parameters Hello SqlParameterCollection bij het aanroepen van een opgeslagen procedure. 

```C#
using System.Data;
using System.Data.SqlClient;

using (SqlConnection connection = new SqlConnection(connectionString))
{ 
DataSet userDataset = new DataSet(); 
SqlDataAdapter myCommand = new SqlDataAdapter(LoginStoredProcedure", connection); 
myCommand.SelectCommand.CommandType = CommandType.StoredProcedure; 
myCommand.SelectCommand.Parameters.Add("@au_id", SqlDbType.VarChar, 11); 
myCommand.SelectCommand.Parameters["@au_id"].Value = SSN.Text; 
myCommand.Fill(userDataset);
}  
```
Hallo voorgaande codevoorbeeld, mag Hallo invoerwaarde niet langer zijn dan 11 tekens. Als Hallo gegevens niet overeen komen toohello type of de lengte die zijn gedefinieerd door de parameter hello, er Hallo SqlParameter klasse een uitzondering gegenereerd. 

## <a id="binding-mvc"></a>Afzonderlijke model binding klassen of massaopslag toewijzing beveiligingslek in het filter lijsten tooprevent MVC-binding gebruiken

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Webtoepassing | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | MVC5, MVC6 |
| **Kenmerken**              | N.v.t.  |
| **Verwijzingen**              | [Metagegevenskenmerken](http://msdn.microsoft.com/library/system.componentmodel.dataannotations.metadatatypeattribute), [openbare sleutel beveiligingslek en Beveiligingsrisicobeperking](https://github.com/blog/1068-public-key-security-vulnerability-and-mitigation), [beveiligingsgids tooMass toewijzing in ASP.NET MVC](http://odetocode.com/Blogs/scott/archive/2012/03/11/complete-guide-to-mass-assignment-in-asp-net-mvc.aspx), [aan de slag met EF met MVC](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application#overpost) |
| **Stappen** | <ul><li>**Wanneer moet ik letten te veel boeken beveiligingslekken? -** Te veel boeken beveiligingsproblemen kan optreden als een willekeurige plaats u modelklassen binding uit de invoer van de gebruiker. Frameworks zoals MVC kunnen gebruikersgegevens in aangepaste .NET-klassen, met inbegrip van gewone oude CLR-objecten (POCOs) vertegenwoordigen. MVC wordt automatisch gevuld deze modelklassen met de gegevens van de aanvraag hello, bieden een handige weergave voor het omgaan met invoer van gebruiker. Wanneer deze klassen eigenschappen die niet moeten worden ingesteld door de gebruiker hello bevatten, kan de toepassing hello kwetsbaar tooover boeken-aanvallen Gebruikersbeheer van gegevens die nooit toepassing hello bedoeld zijn. Net als modelbinding MVC ondersteuning database technologieën zoals object relationele mappers zoals Entity Framework vaak ook voor het gebruik POCO objecten toorepresent databasegegevens. Deze gegevens modelklassen Hallo bieden dezelfde gebruiksgemak omgaan met gegevens uit een database, zoals MVC in omgaan met invoer van gebruiker. Omdat zowel MVC en Hallo database ondersteunt soortgelijke modellen, zoals POCO-objecten, lijkt het eenvoudig tooreuse Hallo dezelfde voor beide doeleinden klassen. Deze praktijk mislukt toopreserve scheiding van problemen en is een algemene gebied waar onbedoelde eigenschappen zijn blootgesteld toomodel binding, het inschakelen van te veel boeken aanvallen.</li><li>**Waarom mag niet ik mijn modelklassen ongefilterde database gebruiken als parameters toomy MVC acties? -** Omdat MVC modelbinding in deze klasse wordt gebonden. Zelfs als hello gegevens worden niet weergegeven in de weergave dat een kwaadwillende gebruiker kan een HTTP-aanvraag verzenden met deze gegevens worden opgenomen en MVC graag binden wordt omdat de actie wordt gemeld dat database klasse Hallo vorm van gegevens moet deze accepteren voor invoer van gebruiker.</li><li>**Waarom moet ik Hallo vorm gebruikt voor het modelbinding interesseren? -** Met behulp van ASP.NET MVC modelbinding met makkelijk modellen beschrijft een toepassing tooover boeken aanvallen. Te veel boeken aanvallers toochange toepassingsgegevens afgezien van wat Hallo ontwikkelaars is bedoeld, zoals het overschrijven van Hallo prijs voor een artikel of Hallo beveiligingsbevoegdheden voor een account kan worden ingeschakeld. Toepassingen voor welke niet-vertrouwde invoer tooallow via modelbinding specifieke acties binding modellen (of specifieke toegestane filter eigenschappenlijsten) tooprovide een expliciete contract gebruiken.</li><li>**Afzonderlijke binding modellen NET dupliceren code heeft? -** Nee, is een kwestie van scheiding van problemen. Als u de databasemodellen in actiemethoden hergebruikt, wordt u een eigenschap (of een onderliggende eigenschap) gezegd in deze klasse kan worden ingesteld door de gebruiker Hallo in een HTTP-aanvraag. Als u niet wilt dat MVC toodo, moet u een filterlijst of een afzonderlijke klasse vorm tooshow MVC welke gegevens afkomstig van gebruikersinvoer in plaats daarvan zijn kunnen.</li><li>**Als ik afzonderlijke binding modellen voor invoer van de gebruiker hebt, heb ik tooduplicate mijn kenmerken voor de aantekening gegevens? -** Niet noodzakelijkerwijs. U kunt MetadataTypeAttribute op Hallo model klasse toolink toohello databasemetagegevens voor een model binding-klasse. Alleen Let Hallo type waarnaar wordt verwezen door Hallo MetadataTypeAttribute moet een subset van Hallo die verwijzen naar type (mogelijk minder eigenschappen, maar niet meer).</li><li>**Verplaatsen van gegevens heen en weer tussen de gebruiker invoer modellen en databasemodellen is omslachtig. Kan ik alleen kopiëren via alle eigenschappen met reflectie? -** Ja. Hallo zijn alleen eigenschappen die worden weergegeven in Hallo binding modellen Hallo die u hebt vastgesteld toobe veilig voor invoer van de gebruiker. Er is geen reden beveiliging waarmee wordt voorkomen dat via reflectie toocopy over alle eigenschappen die gemeenschappelijk tussen deze twee modellen bestaan.</li><li>**Hoe zit [binden (uitsluiten = "¦ â €")]. Kan ik die in plaats van afzonderlijke binding modellen gebruiken? -** Deze methode wordt niet aanbevolen. Met behulp van [binden (uitsluiten = "¦ â €")] betekent dat een nieuwe eigenschap bindbare standaard. Wanneer een nieuwe eigenschap wordt toegevoegd, er is een extra stap tooremember tookeep dingen veilige plaats Hallo ontwerp zijn standaard veilig. Afhankelijk van het Hallo-ontwikkelaars is het riskant deze lijst controleren telkens wanneer een eigenschap wordt toegevoegd.</li><li>**Is [binden (inclusief = "¦ â €")] handig voor het bewerken? -** Nee. [Binden (inclusief = "¦ â €")] is alleen geschikt voor INSERT-stijl-bewerkingen (toevoegen van nieuwe gegevens). Voor bewerkingen van UPDATE-stijl (herziening van bestaande gegevens), gebruikt u een andere methode, zoals afzonderlijke binding modellen hebben of een expliciete lijst van toegestane eigenschappen tooUpdateModel of TryUpdateModel wordt doorgegeven. Toevoegen van een [binden (opnemen = 'â €¦')] kenmerk voor een bewerking betekent dat MVC wordt een objectexemplaar maken en ingesteld alleen Hallo vermelde eigenschappen van alle andere gebruikers op hun standaardwaarden verlaten. Wanneer het Hallo-gegevens worden bewaard, wordt volledig Hallo bestaande entiteit, opnieuw instellen van waarden voor elk weggelaten eigenschappen tootheir standaardinstellingen Hallo vervangen. Bijvoorbeeld, als IsAdmin is weggelaten uit een [binden (opnemen = "â €¦")]-kenmerk op een bewerking, een gebruiker waarvan de naam is bewerkt via deze actie reset tooIsAdmin zou zijn = false (elke gebruiker bewerkte verliezen status van de administrator). Als u tooprevent updates toocertain eigenschappen wilt, gebruik een van de Hallo andere benaderingen hierboven. Houd er rekening mee dat sommige versies van MVC-tooling Controllerklassen met genereren [binden (inclusief = 'â €¦')] acties bewerken en impliceren dat een eigenschap te verwijderen uit de lijst u te veel boeken aanvallen voorkomt. Echter zoals hierboven wordt beschreven, die benadering niet naar behoren werkt en in plaats daarvan wordt opnieuw ingesteld gegevens in Hallo weggelaten eigenschappen tootheir standaardwaarden.</li><li>**Voor de bewerkingen maken, zijn er aanvullende opmerkingen met [binden (opnemen = "¦ â €")] in plaats van afzonderlijke binding modellen? -** Ja. Deze methode werkt eerst niet voor scenario's bewerken, vereisen van twee afzonderlijke methoden voor alle te veel boeken zwakke plekken beperkende onderhouden. Tweede, afzonderlijk binding modellen Dwing scheiding van zorgen tussen Hallo vorm gebruikt voor de gebruiker invoer- en Hallo vorm gebruikt voor persistentie, af iets [binden (inclusief = "â €¦")] wordt niet. Derde, houd er rekening mee dat [binden (inclusief = 'â €¦')] zijn alleen geschikt voor eigenschappen op het hoogste niveau. u mag geen alleen gedeelten van de onderliggende eigenschappen (zoals 'Details.Name') in het Hallo-kenmerk. Tot slot en mogelijk belangrijker is, met behulp van [binden (opnemen = "¦ â €")] voegt een extra stap dat elke keer Hallo-klasse wordt gebruikt voor het modelbinding moet onthouden. Als een nieuwe actiemethode toohello gegevensklasse rechtstreeks wordt gekoppeld en tooinclude vergeet een [binden (opnemen = "â €¦")]-kenmerk, dit kan zijn kwetsbaar tooover boeken aanvallen, dus Hallo [binden (opnemen = 'â €¦')] benadering standaard wat minder veilig is. Als u [binden (inclusief = 'â €¦')], behandelen altijd tooremember toospecify deze telkens wanneer de gegevensklassen van uw worden weergegeven als actie-methodeparameters.</li><li>**Voor bewerkingen maken, wat over het samenvoegen van Hallo [binden (inclusief = 'â €¦')]-kenmerk op Hallo modelklasse zelf? Voorkomt dat niet van deze benadering Hallo nodig tooremember stellen Hallo-kenmerk op elke actiemethode? -** Deze benadering in sommige gevallen werkt. Met behulp van [binden (opnemen = 'â €¦')] op Hallo modeltype zelf (in plaats van op Actieparameters in met behulp van deze klasse), voorkomt dat Hallo nodig tooremember tooinclude Hallo [binden (opnemen = 'â €¦')] kenmerk voor elke methode in te grijpen. Met behulp van Hallo kenmerk rechtstreeks op Hallo klasse effectief, maakt een afzonderlijke surface area van deze klasse voor model binding doeleinden. Deze methode kan echter slechts voor één model binding vorm per modelklasse. Als één actiemethode moet tooallow modelbinding van een veld (bijvoorbeeld een alleen-lezen beheerder actie die gebruikersrollen updates) en andere acties tooprevent modelbinding van dit veld moeten, werkt deze methode niet. Elke klasse kan slechts één vorm van binding; hebben. Als u verschillende acties moeten een ander model binding vormen, moeten ze toorepresent deze scheiden met een afzonderlijke model binding-klassen vormen of afzonderlijke [binden (opnemen = "¦ â €")] kenmerken op Hallo actiemethoden.</li><li>**Wat zijn het binden van modellen? Zijn dat ze Hallo hetzelfde is als modellen weergeven? -** Dit twee verwante concepten zijn. Hallo-term binding model tooa modelklasse gebruikt in een actie verwijst is parameterlijst (Hallo vorm van MVC-model binding toohello actiemethode doorgegeven). Hallo term weergave model verwijst tooa modelklasse van weergave met een actie methode tooa doorgegeven. Met behulp van een weergave-specifieke model is een algemene benadering voor het doorgeven van gegevens uit een actie methode tooa weergave. Vaak worden deze vorm is ook geschikt voor modelbinding en Hallo term weergave model kan worden gebruikt toorefer Hallo hetzelfde model op beide plaatsen worden gebruikt. toobe nauwkeurige, deze procedure wordt gesproken over de binding van modellen, te focussen op Hallo vorm doorgegeven toohello-actie is wat belangrijk is voor massaopslag toewijzing doeleinden.</li></ul>| 

## <a id="rendering"></a>Niet-vertrouwde web uitvoer voorafgaande toorendering coderen

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Webtoepassing | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | Algemeen, Web Forms, MVC5, MVC6 |
| **Kenmerken**              | N.v.t.  |
| **Verwijzingen**              | [Hoe tooprevent Cross-site scripting in ASP.NET](http://msdn.microsoft.com/library/ms998274.aspx), [Cross-site Scripting](http://cwe.mitre.org/data/definitions/79.html), [XSS (Cross-Site Scripting) preventie cheats blad](https://www.owasp.org/index.php/XSS_(Cross_Site_Scripting)_Prevention_Cheat_Sheet) |
| **Stappen** | Cross-site scripting (vaak afgekort als XSS) is een aanvalsvector voor online services of een toepassing/onderdeel is dat invoer van Hallo web verbruikt. XSS beveiligingsproblemen kunnen een aanvaller tooexecute script op de computer een andere gebruiker via een kwetsbaar webtoepassing. Schadelijke scripts worden cookies gebruikt toosteal en anders kunnen knoeien met de machine van een slachtoffer via JavaScript. XSS wordt voorkomen door het valideren van invoer van gebruiker, zodat is opgemaakt en codering voordat deze wordt weergegeven in een webpagina. Validatie voor invoer en uitvoercodering kunnen worden gedaan met behulp van Web-bibliotheek voor beveiliging. Voor beheerde code (C\#, VB.net, enz.), gebruikt u een of meer codering methoden van Hallo Web beveiliging (Anti-XSS)-bibliotheek, afhankelijk van waar de gebruikersinvoer Hallo opgehaald gemanifesteerd Hallo-context van toepassing:| 

### <a name="example"></a>Voorbeeld

```C#
* Encoder.HtmlEncode 
* Encoder.HtmlAttributeEncode 
* Encoder.JavaScriptEncode 
* Encoder.UrlEncode
* Encoder.VisualBasicScriptEncode 
* Encoder.XmlEncode 
* Encoder.XmlAttributeEncode 
* Encoder.CssEncode 
* Encoder.LdapEncode 
```

## <a id="typemodel"></a>Validatie voor invoer- en filteren op alle tekenreekstype modeleigenschappen uitvoeren

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Webtoepassing | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | Algemeen, MVC5, MVC6 |
| **Kenmerken**              | N.v.t.  |
| **Verwijzingen**              | [Toe te voegen validatie](http://www.asp.net/mvc/overview/getting-started/introduction/adding-validation), [modelgegevens valideren in een MVC-toepassing](http://msdn.microsoft.com/library/dd410404(v=vs.90).aspx), [richtsnoer voor uw ASP.NET MVC-toepassingen](http://msdn.microsoft.com/magazine/dd942822.aspx) |
| **Stappen** | <p>Alle Hallo invoerparameters moeten worden gevalideerd voordat ze worden gebruikt in Hallo toepassing tooensure dat de toepassing hello zijn beveiligd tegen schadelijke gebruikersinvoer. Hallo invoerwaarden met reguliere expressie validaties aan serverzijde met een strategie voor een lijst met geaccepteerde validatie valideren. Gebruikersinvoer unsanitized / parameters doorgegeven toohello methoden kunnen leiden tot code injectie beveiligingsproblemen.</p><p>Voor webtoepassingen bevatten toegangspunten ook formuliervelden, QueryStrings, cookies, HTTP-headers en web serviceparameters.</p><p>Hallo moeten controles van de volgende validatie voor invoer worden uitgevoerd bij modelbinding:</p><ul><li>Hallo modeleigenschappen moeten worden gemarkeerd met RegularExpression aantekening, voor het accepteren van toegestane aantal tekens en maximaal toegestane lengte</li><li>Hallo-controllermethoden ModelState geldigheid moeten worden uitgevoerd</li></ul>|

## <a id="richtext"></a>Opschoning moet worden toegepast op formuliervelden die tekens, bijvoorbeeld, RTF-editor accepteren

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Webtoepassing | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | Algemene |
| **Kenmerken**              | N.v.t.  |
| **Verwijzingen**              | [Onveilige invoer coderen](https://msdn.microsoft.com/library/ff647397.aspx#paght000003_step3), [HTML Sanitizer](https://github.com/mganss/HtmlSanitizer) |
| **Stappen** | <p>Identificeer alle statische markup labels die u toouse wilt. Een gebruikelijk is toorestrict opmaak toosafe HTML-elementen, zoals `<b>` (vet weergegeven) en `<i>` (cursief).</p><p>Hallo-gegevens, HTML en coderen gebufferd voordat deze. Dit zorgt ervoor dat eventuele schadelijke scripts veilig waardoor toobe behandeld als tekst, niet als uitvoerbare code.</p><ol><li>Schakel ASP.NET-aanvraag validatie door Hallo toe te voegen Hallo ValidateRequest = 'false' kenmerk toohello @ pagina-instructie</li><li>Hallo tekenreeksinvoer met Hallo HtmlEncode methode coderen</li><li>Gebruik een StringBuilder en de aanroep van de methode vervangen tooselectively Hallo codering op Hallo HTML-elementen die u wilt dat toopermit verwijderen</li></ol><p>Hallo Hallo-pagina in verwijzingen wordt uitgeschakeld ASP.NET aanvraag gevalideerd door `ValidateRequest="false"`. Het HTML-codeert Hallo invoer- en kunt u selectief Hallo `<b>` en `<i>` ook een .NET-bibliotheek voor HTML-opschoning kan ook worden gebruikt.</p><p>HtmlSanitizer is een .NET-bibliotheek voor het reinigen HTML-fragmenten en documenten van constructies die tooXSS aanvallen kunnen leiden. Het AngleSharp tooparse gebruikt, bewerken en HTML en CSS weergeven. HtmlSanitizer kan worden geïnstalleerd als een NuGet-pakket en gebruikersinvoer Hallo kan worden doorgegeven via relevante HTML of CSS-opschoning methoden, indien van toepassing op Hallo serverzijde. Houd er rekening mee dat opschoning als een beveiligingscontrole alleen als een laatste optie moet worden beschouwd.</p><p>Validatie voor invoer en uitvoercodering worden beschouwd als de besturingselementen voor betere beveiliging.</p> |

## <a id="inbuilt-encode"></a>DOM elementen toosinks waarvoor geen ingebouwde codering niet toe te wijzen

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Webtoepassing | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | Algemene |
| **Kenmerken**              | N.v.t.  |
| **Verwijzingen**              | N.v.t.  |
| **Stappen** | Veel javascript-functies doen niet codering standaard. Als u niet-vertrouwde invoer tooDOM elementen via dergelijke functies toewijst, kan leiden tot cross-site-script (XSS) uitvoeringen.| 

### <a name="example"></a>Voorbeeld
Hieronder vindt u onveilige voorbeelden: 

```
document.getElementByID("div1").innerHtml = value;
$("#userName").html(res.Name);
return $('<div/>').html(value)
$('body').append(resHTML);   
```
Gebruik geen `innerHtml`; gebruik in plaats daarvan `innerText`. Op deze manier in plaats van `$("#elm").html()`, gebruiken`$("#elm").text()` 

## <a id="redirect-safe"></a>Valideer alle omleidingen in toepassing hello zijn gesloten of veilig gedaan

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Webtoepassing | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | Algemene |
| **Kenmerken**              | N.v.t.  |
| **Verwijzingen**              | [Hallo Framework voor autorisatie van OAuth 2.0 - Open Redirectors](http://tools.ietf.org/html/rfc6749#section-10.15) |
| **Stappen** | <p>Ontwerp van de toepassing waarvoor omleiding tooa gebruiker opgegeven locatie moet Hallo mogelijke omleiding doelen tooa vooraf gedefinieerde "veilig" lijst met sites of domeinen beperken. Alle omleidingen in Hallo toepassing moeten worden gesloten/veilig.</p><p>toodo dit:</p><ul><li>Alle omleidingen identificeren</li><li>Een juiste Risicobeperking voor het omleiden van elke implementeren. Juiste oplossingen omvatten omleiding goedgekeurde IP-adressen of gebruiker bevestigen. Als een website of de service met een beveiligingslek open omleiding identiteitsproviders OAuth-Facebook/OpenID gebruikt, kan een aanvaller stelen van een gebruiker aanmeldingstokens en die gebruiker imiteren. Dit risico is wanneer met behulp van OAuth, die wordt beschreven in RFC 6749 'Hallo OAuth 2.0 autorisatie Framework', sectie 10.15 'Open leidt' op dezelfde manier, referenties van gebruikers kunnen worden aangetast door spear phishing-aanvallen met open omleidingen</li></ul>|

## <a id="string-method"></a>Validatie voor invoer op alle tekenreeks typeparameters geaccepteerd door de methoden van de domeincontroller implementeren

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Webtoepassing | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | Algemeen, MVC5, MVC6 |
| **Kenmerken**              | N.v.t.  |
| **Verwijzingen**              | [Valideren van modelgegevens in een MVC-toepassing](http://msdn.microsoft.com/library/dd410404(v=vs.90).aspx), [richtsnoer voor uw ASP.NET MVC-toepassingen](http://msdn.microsoft.com/magazine/dd942822.aspx) |
| **Stappen** | Methoden die primitief gegevenstype en geen modellen als argument accepteert, moet met een reguliere expressie voor validatie voor invoer worden gedaan. Hier moet Regex.IsMatch worden gebruikt met een geldige regex-patroon. Hallo invoer komt niet overeen met Hallo opgegeven reguliere expressie, besturingselement moet niet verder als een passende waarschuwing met betrekking tot mislukte validatie moet worden weergegeven.| 

## <a id="dos-expression"></a>Time-out voor bovengrens instellen voor reguliere expressie voor het verwerken van tooprevent DoS vanwege toobad reguliere expressies

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Webtoepassing | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | Algemeen, Web Forms, MVC5, MVC6  |
| **Kenmerken**              | N.v.t.  |
| **Verwijzingen**              | [De eigenschap DefaultRegexMatchTimeout](https://msdn.microsoft.com/library/system.web.configuration.httpruntimesection.defaultregexmatchtimeout.aspx) |
| **Stappen** | tooensure denial-of service-aanvallen op onjuist gemaakt reguliere expressies, waardoor een groot aantal backtracing als Hallo globale standaardtime-out ingesteld. Als de verwerkingstijd van Hallo langer duurt dan Hallo bovengrens gedefinieerd, zou deze time-out-uitzondering genereren. Als er niets is geconfigureerd, zou Hallo time-out oneindig zijn.| 

### <a name="example"></a>Voorbeeld
Bijvoorbeeld: hello volgende configuratie genereert een RegexMatchTimeoutException als Hallo verwerking langer dan 5 seconden duurt: 

```C#
<httpRuntime targetFramework="4.5" defaultRegexMatchTimeout="00:00:05" />
```

## <a id="html-razor"></a>Vermijd het gebruik van Html.Raw in Razor weergaven

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Webtoepassing | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | MVC5, MVC6 |
| **Kenmerken**              | N.v.t.  |
| **Verwijzingen**              | N.v.t.  |
| Stap | ASP.Net-webpagina's (Razor) uitvoeren van automatische HTML-codering. Alle tekenreeksen die worden afgedrukt door ingesloten code nuggets (@ blokken) zijn automatisch HTML-codering. Echter, wanneer `HtmlHelper.Raw` methode wordt aangeroepen, resulteert dit in de opmaak die is geen HTML-codering. Als `Html.Raw()` Help-methode wordt gebruikt, wordt omzeild Hallo automatische codering bescherming die Razor biedt.|

### <a name="example"></a>Voorbeeld
Hieronder volgt een onbeveiligde voorbeeld: 

```C#
<div class="form-group">
            @Html.Raw(Model.AccountConfirmText)
        </div>
        <div class="form-group">
            @Html.Raw(Model.PaymentConfirmText)
        </div>
</div>
```
Gebruik geen `Html.Raw()` tenzij u toodisplay opmaak nodig. Deze methode voert geen uitvoer impliciet codering. Gebruik andere helpers ASP.NET bijv.`@Html.DisplayFor()` 

## <a id="stored-proc"></a>Gebruik geen dynamische query's in de opgeslagen procedures

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Database | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | Algemene |
| **Kenmerken**              | N.v.t.  |
| **Verwijzingen**              | N.v.t.  |
| **Stappen** | <p>Een SQL-injectieaanvallen gebruikmaakt van kwetsbaarheden in validatie voor invoer toorun willekeurige opdrachten in Hallo-database. Dit kan optreden wanneer de toepassing gebruikmaakt van invoer tooconstruct dynamische SQL-instructies tooaccess Hallo database. Het kan ook optreden als opgeslagen procedures die zijn doorgegeven tekenreeksen met onbewerkte gebruikersinvoer wordt gebruikt in uw code. Met behulp van SQL-injectieaanvallen Hallo uitvoeren Hallo aanvaller willekeurige opdrachten in Hallo-database. De parameters van alle SQL-instructies (inclusief Hallo SQL-instructies in de opgeslagen procedures) moeten worden gebruikt. SQL-instructies met parameters accepteert tekens die op een speciale betekenis tooSQL (zoals enkel aanhalingsteken) zonder problemen omdat ze sterk getypeerd zijn. |

### <a name="example"></a>Voorbeeld
Hieronder volgt een voorbeeld van onbeveiligde dynamische opgeslagen Procedure: 

```C#
CREATE PROCEDURE [dbo].[uspGetProductsByCriteria]
(
  @productName nvarchar(200) = NULL,
  @startPrice float = NULL,
  @endPrice float = NULL
)
AS
 BEGIN
  DECLARE @sql nvarchar(max)
  SELECT @sql = ' SELECT ProductID, ProductName, Description, UnitPrice, ImagePath' +
       ' FROM dbo.Products WHERE 1 = 1 '
       PRINT @sql
  IF @productName IS NOT NULL
     SELECT @sql = @sql + ' AND ProductName LIKE ''%' + @productName + '%'''
  IF @startPrice IS NOT NULL
     SELECT @sql = @sql + ' AND UnitPrice > ''' + CONVERT(VARCHAR(10),@startPrice) + ''''
  IF @endPrice IS NOT NULL
     SELECT @sql = @sql + ' AND UnitPrice < ''' + CONVERT(VARCHAR(10),@endPrice) + ''''

  PRINT @sql
  EXEC(@sql)
 END
```

### <a name="example"></a>Voorbeeld
Hieronder vindt u Hallo dezelfde opgeslagen procedure veilig geïmplementeerd: 
```C#
CREATE PROCEDURE [dbo].[uspGetProductsByCriteriaSecure]
(
             @productName nvarchar(200) = NULL,
             @startPrice float = NULL,
             @endPrice float = NULL
)
AS
       BEGIN
             SELECT ProductID, ProductName, Description, UnitPrice, ImagePath
             FROM dbo.Products where
             (@productName IS NULL or ProductName like '%'+ @productName +'%')
             AND
             (@startPrice IS NULL or UnitPrice > @startPrice)
             AND
             (@endPrice IS NULL or UnitPrice < @endPrice)         
       END
```

## <a id="validation-api"></a>Zorg ervoor dat de validatie is uitgevoerd voor Web-API-methoden

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Web-API | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | MVC5, MVC6 |
| **Kenmerken**              | N.v.t.  |
| **Verwijzingen**              | [Modelvalidatie van het in ASP.NET-Web-API](http://www.asp.net/web-api/overview/formats-and-model-binding/model-validation-in-aspnet-web-api) |
| **Stappen** | Wanneer een client gegevens tooa web-API verzendt, is het verplichte toovalidate Hallo gegevens voordat u de verwerking. Gebruik gegevens aantekeningen op modellen tooset validatieregels voor Hallo eigenschappen van het Hallo-model voor ASP.NET Web-API's die modellen als invoer accepteren.|

### <a name="example"></a>Voorbeeld
Hallo volgende code toont dezelfde Hallo: 

```C#
using System.ComponentModel.DataAnnotations;

namespace MyApi.Models
{
    public class Product
    {
        public int Id { get; set; }
        [Required]
        [RegularExpression(@"^[a-zA-Z0-9]*$", ErrorMessage="Only alphanumeric characters are allowed.")]
        public string Name { get; set; }
        public decimal Price { get; set; }
        [Range(0, 999)]
        public double Weight { get; set; }
    }
}
```

### <a name="example"></a>Voorbeeld
In actiemethode Hallo Hallo API-controllers heeft de geldigheid van Hallo model toobe expliciet gecontroleerd zoals hieronder wordt weergegeven: 

```C#
namespace MyApi.Controllers
{
    public class ProductsController : ApiController
    {
        public HttpResponseMessage Post(Product product)
        {
            if (ModelState.IsValid)
            {
                // Do something with hello product (not shown).

                return new HttpResponseMessage(HttpStatusCode.OK);
            }
            else
            {
                return Request.CreateErrorResponse(HttpStatusCode.BadRequest, ModelState);
            }
        }
    }
}
```

## <a id="string-api"></a>Validatie voor invoer op alle tekenreeks typeparameters geaccepteerd door de methoden van de Web-API implementeren

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Web-API | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | Algemene MVC 5, 6 MVC |
| **Kenmerken**              | N.v.t.  |
| **Verwijzingen**              | [Valideren van modelgegevens in een MVC-toepassing](http://msdn.microsoft.com/library/dd410404(v=vs.90).aspx), [richtsnoer voor uw ASP.NET MVC-toepassingen](http://msdn.microsoft.com/magazine/dd942822.aspx) |
| **Stappen** | Methoden die primitief gegevenstype en geen modellen als argument accepteert, moet met een reguliere expressie voor validatie voor invoer worden gedaan. Hier moet Regex.IsMatch worden gebruikt met een geldige regex-patroon. Hallo invoer komt niet overeen met Hallo opgegeven reguliere expressie, besturingselement moet niet verder als een passende waarschuwing met betrekking tot mislukte validatie moet worden weergegeven.|

## <a id="typesafe-api"></a>Zorg ervoor dat type veilig parameters in Web-API worden gebruikt voor toegang tot gegevens

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Web-API | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | Algemene |
| **Kenmerken**              | N.v.t.  |
| **Verwijzingen**              | N.v.t.  |
| **Stappen** | <p>Als u de parameterverzameling Hallo gebruikt, is SQL beschouwen Hallo invoer als een letterlijke waarde in plaats als uitvoerbare code. Hallo parameterverzameling kan gebruikte tooenforce type en de lengte-beperkingen voor de invoergegevens zijn. Waarden die buiten het bereik van Hallo activeren een uitzondering. Als u geen type-safe SQL-parameters gebruikt, mogelijk aanvallers kunnen tooexecute injectieaanvallen die zijn ingesloten in de invoer Hallo niet gefilterd.</p><p>Gebruik veilige typeparameters wanneer tooavoid mogelijk SQL-injectieaanvallen die zich met ongefilterde invoer voordoen kunnen construeren SQL query. U kunt veilig typeparameters met opgeslagen procedures en dynamische SQL-instructies. Parameters worden behandeld als letterlijke waarden door Hallo-database en niet als uitvoerbare code. Parameters zijn ook gecontroleerd op type en de lengte.</p>|

### <a name="example"></a>Voorbeeld
Hallo volgende code toont hoe toouse Typ veilige parameters Hello SqlParameterCollection bij het aanroepen van een opgeslagen procedure. 

```C#
using System.Data;
using System.Data.SqlClient;

using (SqlConnection connection = new SqlConnection(connectionString))
{ 
DataSet userDataset = new DataSet(); 
SqlDataAdapter myCommand = new SqlDataAdapter(LoginStoredProcedure", connection); 
myCommand.SelectCommand.CommandType = CommandType.StoredProcedure; 
myCommand.SelectCommand.Parameters.Add("@au_id", SqlDbType.VarChar, 11); 
myCommand.SelectCommand.Parameters["@au_id"].Value = SSN.Text; 
myCommand.Fill(userDataset);
}  
```
Hallo voorgaande codevoorbeeld, mag Hallo invoerwaarde niet langer zijn dan 11 tekens. Als Hallo gegevens niet overeen komen toohello type of de lengte die zijn gedefinieerd door de parameter hello, er Hallo SqlParameter klasse een uitzondering gegenereerd. 

## <a id="sql-docdb"></a>SQL-query's constructorreeks mag gebruiken voor Cosmos-DB

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Azure Documentdb | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | Algemene |
| **Kenmerken**              | N.v.t.  |
| **Verwijzingen**              | [SQL-Parameterisering in DocumentDB aangekondigd](https://azure.microsoft.com/blog/announcing-sql-parameterization-in-documentdb/) |
| **Stappen** | Hoewel DocumentDB biedt alleen ondersteuning voor alleen-lezen-query's, is SQL-injectie nog steeds mogelijk als de query's worden gemaakt met cookievalidatie met invoer van gebruiker. Het is mogelijk dat een gebruiker toogain toegang toodata ze toegang binnen Hallo mag niet tot dezelfde verzameling door schadelijke SQL-query's. Gebruik SQL-query's met parameters als de query's zijn samengesteld op basis van gebruikersinvoer. |

## <a id="schema-binding"></a>Validatie van de WCF-invoer via schemabinding

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | WCF | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | Algemeen, NET Framework 3 |
| **Kenmerken**              | N.v.t.  |
| **Verwijzingen**              | [MSDN](https://msdn.microsoft.com/library/ff647820.aspx) |
| **Stappen** | <p>Gebrek aan validatie leidt toodifferent type injectieaanvallen.</p><p>Berichtverificatie vertegenwoordigt één regel verdediging in Hallo beveiliging van uw WCF-toepassing. Met deze methode kunt u berichten met behulp van schema's tooprotect WCF servicebewerkingen tegen een aanval door een schadelijke client valideren. Alle berichten ontvangen door Hallo tooprotect Hallo cliënt tegen een aanval door een kwaadwillende service valideren. Berichtverificatie maakt het mogelijk toovalidate berichten wanneer bewerkingen verbruiken bericht contracten of gegevenscontracten, kunnen niet worden uitgevoerd met behulp van de validatie van parameters. Berichtverificatie kunt u toocreate validatielogica binnen schema's, waardoor meer flexibiliteit en minder tijd. Schema's kunnen opnieuw worden gebruikt door verschillende toepassingen binnen de organisatie hello, standaarden voor weergave van gegevens maken. Bovendien kunt berichtverificatie u bewerkingen tooprotect wanneer ze complexe gegevenstypen met betrekking tot contracten die zakelijke logica verbruiken.</p><p>Berichtverificatie tooperform, u opbouwen eerst een schema dat Hallo bewerkingen van uw service en Hallo gegevenstypen die door deze bewerkingen worden gebruikt vertegenwoordigt. Vervolgens maakt u een .NET-klasse die een aangepaste clientinstellingen bericht inspector en aangepaste dispatcher bericht inspector toovalidate Hallo-berichten verzonden/ontvangen van Hallo service implementeert. U kunt vervolgens een aangepaste eindpunt gedrag tooenable bericht validatie implementeren op Hallo-client en service Hallo. Ten slotte implementeren u een aangepaste configuratie-element op Hallo klasse waarmee u tooexpose Hallo uitgebreid aangepaste eindpuntgedrag in het configuratiebestand Hallo Hallo service of client Hallo'</p>|

## <a id="parameters"></a>Validatie van de WCF - invoer via Parameter Inspectors

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | WCF | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | Algemeen, NET Framework 3 |
| **Kenmerken**              | N.v.t.  |
| **Verwijzingen**              | [MSDN](https://msdn.microsoft.com/library/ff647875.aspx) |
| **Stappen** | <p>Invoer en gegevensvalidatie vertegenwoordigt een belangrijke line-of ingrijpende Hallo beveiliging van uw WCF-toepassing. U moet alle parameters die worden weergegeven in de WCF-service operations tooprotect Hallo service tegen een aanval door een schadelijke client valideren. Als u daarentegen, moet u ook alle retourwaarden ontvangen door Hallo tooprotect Hallo cliënt tegen een aanval door een kwaadwillende service valideren</p><p>WCF biedt andere uitbreidbaarheidspunten waarmee u toocustomize Hallo WCF runtimegedrag door het maken van aangepaste extensies. Bericht Inspectors en Parameter Inspectors zijn twee uitbreidbaarheid mechanismen gebruikt toogain meer controle over Hallo gegevens tussen een client en een service wordt doorgegeven. U moet de parameter inspectors gebruiken voor validatie voor invoer en inspectors bericht alleen gebruiken wanneer u tooinspect Hallo hele bericht dat naar en vanuit een service nodig hebt.</p><p>tooperform Invoervalidatie, u bouwt u een .NET-klasse en een aangepaste parameter inspector in volgorde toovalidate parameters van bewerkingen in uw service implementeren. Vervolgens implementeert u een aangepaste eindpunt gedrag tooenable validatie op Hallo-client en Hallo-service. Ten slotte wilt u een aangepaste configuratie-element op Hallo klasse waarmee u tooexpose Hallo uitgebreid aangepaste eindpuntgedrag in het configuratiebestand Hallo Hallo service of client hello implementeren</p>|

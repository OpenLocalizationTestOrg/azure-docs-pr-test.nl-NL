---
title: 'Azure AD Connect-synchronisatie: functieverwijzing | Microsoft Docs'
description: Verwijzing van expressies declaratieve inrichting in Azure AD Connect-synchronisatie.
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 4f525ca0-be0e-4a2e-8da1-09b6b567ed5f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: fbe0df856ca2efda965650fb85c7e831a0be32c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-functions-reference"></a>Azure AD Connect-synchronisatie: functieverwijzing
In Azure AD Connect zijn functies gebruikte toomanipulate een kenmerkwaarde tijdens de synchronisatie.  
Hallo syntaxis van Hallo functies wordt uitgedrukt met Hallo volgende indeling:  
`<output type> FunctionName(<input type> <position name>, ..)`

Als een functie is overbelast en meerdere syntaxes accepteert, worden alle geldige syntaxis vermeld.  
Hallo-functies zijn sterk getypeerd en ze controleren dat het Hallo-type komt overeen met Hallo beschreven type doorgegeven.  
Als het Hallo-type komt niet overeen, wordt een fout gegenereerd.

Hallo-typen worden uitgedrukt Hello de volgende syntaxis:

* **opslaglocatie** – binaire
* **BOOL** – Booleaanse
* **DT** – UTC-datum/tijd
* **Enum** – opsomming van de bekende constanten
* **EXP** – expressie verwacht tooevaluate tooa Booleaanse waarde
* **mvbin** – meerwaardige binaire
* **mvstr** – meerwaardige tekenreeks
* **mvref** – meerwaardige verwijzing
* **NUM** – numerieke
* **REF** : verwijzing
* **Str** – tekenreeks
* **VAR** : een variant van (bijna) alle andere type
* **VOID** – geen waarde als resultaat

functies met typen Hallo Hallo **mvbin**, **mvstr**, en **mvref** kunt werken alleen op kenmerken met meerdere waarden. Functies met **bin**, **str**, en **ref** werk op de kenmerken van zowel één waarde en meerdere waarden.

## <a name="functions-reference"></a>Functieverwijzing
| Lijst met functies |  |  |  |  |
| --- | --- | --- | --- | --- | --- |
| **Certificaat** | | | | |
| [CertExtensionOids](#certextensionoids) |[CertFormat](#certformat) |[CertFriendlyName](#certfriendlyname) |[CertHashString](#certhashstring) | |
| [CertIssuer](#certissuer) |[CertIssuerDN](#certissuerdn) |[CertIssuerOid](#certissueroid) |[CertKeyAlgorithm](#certkeyalgorithm) | |
| [CertKeyAlgorithmParams](#certkeyalgorithmparams) |[CertNameInfo](#certnameinfo) |[CertNotAfter](#certnotafter) |[CertNotBefore](#certnotbefore) | |
| [CertPublicKeyOid](#certpublickeyoid) |[CertPublicKeyParametersOid](#certpublickeyparametersoid) |[CertSerialNumber](#certserialnumber) |[CertSignatureAlgorithmOid](#certsignaturealgorithmoid) | |
| [CertSubject](#certsubject) |[CertSubjectNameDN](#certsubjectnamedn) |[CertSubjectNameOid](#certsubjectnameoid) |[CertThumbprint](#certthumbprint) | |
[CertVersion](#certversion) |[IsCert](#iscert) | | | |
| **Conversie** | | | | |
| [CBool](#cbool) |[CDate](#cdate) |[CGuid](#cguid) |[ConvertFromBase64](#convertfrombase64) | |
| [ConvertToBase64](#converttobase64) |[ConvertFromUTF8Hex](#convertfromutf8hex) |[ConvertToUTF8Hex](#converttoutf8hex) |[CNum](#cnum) | |
| [CRef](#cref) |[CStr](#cstr) |[StringFromGuid](#StringFromGuid) |[StringFromSid](#stringfromsid) | |
| **Datum / tijd** | | | | |
| [DateAdd](#dateadd) |[DateFromNum](#datefromnum) |[FormatDateTime](#formatdatetime) |[Nu](#now) | |
| [NumFromDate](#numfromdate) | | | | |
| **Directory** | | | | |
| [DNComponent](#dncomponent) |[DNComponentRev](#dncomponentrev) |[EscapeDNComponent](#escapedncomponent) | | |
| **Evaluatie** | | | | |
| [IsBitSet](#isbitset) |[IsDate](#isdate) |[IsEmpty](#isempty) |[IsGuid](#isguid) | |
| [IsNull](#isnull) |[IsNullOrEmpty](#isnullorempty) |[IsNumeric](#isnumeric) |[IsPresent](#ispresent) | |
| [IsString](#isstring) | | | | |
| **Math** | | | | |
| [BitAnd](#bitand) |[BitOr](#bitor) |[RandomNum](#randomnum) | | |
| **Met meerdere waarden** | | | | |
| [Bevat](#contains) |[Aantal](#count) |[Item](#item) |[ItemOrNull](#itemornull) | |
| [Koppelen](#join) |[RemoveDuplicates](#removeduplicates) |[Splitsen](#split) | | |
| **Programma-overdracht** | | | | |
| [Fout](#error) |[IIF](#iif) |[Selecteren](#select) |[Switch](#switch) | |
| [Waar](#where) |[Met](#with) | | | |
| **Tekst** | | | | |
| [GUID](#guid) |[InStr](#instr) |[InStrRev](#instrrev) |[LCase](#lcase) | |
| [Links](#left) |[Len](#len) |[LTrim](#ltrim) |[Mid](#mid) | |
| [PadLeft](#padleft) |[PadRight](#padright) |[PCase](#pcase) |[Vervangen](#replace) | |
| [ReplaceChars](#replacechars) |[Rechts](#right) |[RTrim](#rtrim) |[Trim](#trim) | |
| [UCase](#ucase) |[Word](#word) | | | |

- - -
### <a name="bitand"></a>BitAnd
**Beschrijving:**  
Hallo functie BitAnd wordt opgegeven bits ingesteld op een waarde.

**Syntaxis:**  
`num BitAnd(num value1, num value2)`

* Value1, value2: numerieke waarden die functiesleutels samen moeten worden

**Opmerkingen:**  
Deze functie worden geconverteerd van beide parameters toohello binaire voorstelling en iets op:

* 0 - als een of beide van de bijbehorende bits in Hallo *masker* en *vlag* 0 zijn
* 1 - als de bijbehorende bits Hallo 1 zijn.

Met andere woorden, resultaat het 0 in alle gevallen, behalve wanneer de bijbehorende bits Hallo van beide parameters 1.

**Voorbeeld:**  
`BitAnd(&HF, &HF7)`  
Retourneert 7 omdat hexadecimale 'F' en 'F7' toothis waarde evalueren.

- - -
### <a name="bitor"></a>BitOr
**Beschrijving:**  
Hallo functie BitOr wordt opgegeven bits ingesteld op een waarde.

**Syntaxis:**  
`num BitOr(num value1, num value2)`

* Value1, value2: numerieke waarden die samen worden moeten

**Opmerkingen:**  
Deze functie converteert beide parameters toohello binaire voorstelling en een too1 bits ingesteld als een of beide van de bijbehorende bits Hallo in masker en markering 1 en too0 zijn als de bijbehorende bits Hallo 0 zijn. Met andere woorden, retourneert 1 in alle gevallen behalve wanneer de bijbehorende bits Hallo van beide parameters 0.

- - -
### <a name="cbool"></a>CBool
**Beschrijving:**  
Hallo CBool functie retourneert een Booleaanse waarde die is gebaseerd op Hallo geëvalueerd expressie

**Syntaxis:**  
`bool CBool(exp Expression)`

**Opmerkingen:**  
Als Hallo expressie tooa andere waarde dan nul, resulteert en True CBool retourneert, anders wordt onwaar.

**Voorbeeld:**  
`CBool([attrib1] = [attrib2])`  

Retourneert waar als beide kenmerken hebben dezelfde waarde Hallo.

- - -
### <a name="cdate"></a>CDate
**Beschrijving:**  
Hallo functie CDate retourneert een UTC datetime-waarde van een tekenreeks. Datum/tijd is niet een systeemeigen kenmerktype synchroon maar wordt gebruikt door een aantal functies.

**Syntaxis:**  
`dt CDate(str value)`

* Waarde: Een tekenreeks met een datum, tijd en eventueel tijdzone

**Opmerkingen:**  
Hallo geretourneerde tekenreeks is altijd ingesteld op UTC.

**Voorbeeld:**  
`CDate([employeeStartTime])`  
Retourneert een datum-/ op basis van de begintijd van de werknemer Hallo

`CDate("2013-01-10 4:00 PM -8")`  
Retourneert een DateTime-waarde die aangeeft ' 2013-01-11-12:00 AM '








- - -
### <a name="certextensionoids"></a>CertExtensionOids
**Beschrijving:**  
Retourneert Hallo Oid-waarden van alle Hallo kritieke uitbreidingen van een certificaatobject.

**Syntaxis:**  
`mvstr CertExtensionOids(binary certificateRawData)`  
*   certificateRawData: Byte matrix representatie van een X.509-certificaat. Hallo-byte-matrix mag binair (DER), gecodeerd of Base64-gecodeerd x.509-gegevens.

- - -
### <a name="certformat"></a>CertFormat
**Beschrijving:**  
Retourneert Hallo naam van het Hallo-indeling van deze X.509v3-certificaat.

**Syntaxis:**  
`str CertFormat(binary certificateRawData)`  
*   certificateRawData: Byte matrix representatie van een X.509-certificaat. Hallo-byte-matrix mag binair (DER), gecodeerd of Base64-gecodeerd x.509-gegevens.

- - -
### <a name="certfriendlyname"></a>CertFriendlyName
**Beschrijving:**  
Retourneert Hallo alias voor een certificaat dat is gekoppeld.

**Syntaxis:**  
`str CertFriendlyName(binary certificateRawData)`  
*   certificateRawData: Byte matrix representatie van een X.509-certificaat. Hallo-byte-matrix mag binair (DER), gecodeerd of Base64-gecodeerd x.509-gegevens.

- - -
### <a name="certhashstring"></a>CertHashString
**Beschrijving:**  
Retourneert Hallo SHA1-hash-waarde voor Hallo X.509v3-certificaat als hexadecimale tekenreeks.

**Syntaxis:**  
`str CertHashString(binary certificateRawData)`  
*   certificateRawData: Byte matrix representatie van een X.509-certificaat. Hallo-byte-matrix mag binair (DER), gecodeerd of Base64-gecodeerd x.509-gegevens.

- - -
### <a name="certissuer"></a>CertIssuer
**Beschrijving:**  
Retourneert Hallo naam van certificeringsinstantie Hallo die Hallo X.509v3-certificaat heeft uitgegeven.

**Syntaxis:**  
`str CertIssuer(binary certificateRawData)`  
*   certificateRawData: Byte matrix representatie van een X.509-certificaat. Hallo-byte-matrix mag binair (DER), gecodeerd of Base64-gecodeerd x.509-gegevens.

- - -
### <a name="certissuerdn"></a>CertIssuerDN
**Beschrijving:**  
Retourneert Hallo DN-naam van de certificaatverlener Hallo.

**Syntaxis:**  
`str CertIssuerDN(binary certificateRawData)`  
*   certificateRawData: Byte matrix representatie van een X.509-certificaat. Hallo-byte-matrix mag binair (DER), gecodeerd of Base64-gecodeerd x.509-gegevens.

- - -
### <a name="certissueroid"></a>CertIssuerOid
**Beschrijving:**  
Retourneert Hallo Oid Hallo van verlener van certificaten.

**Syntaxis:**  
`str CertIssuerOid(binary certificateRawData)`  
*   certificateRawData: Byte matrix representatie van een X.509-certificaat. Hallo-byte-matrix mag binair (DER), gecodeerd of Base64-gecodeerd x.509-gegevens.

- - -
### <a name="certkeyalgorithm"></a>CertKeyAlgorithm
**Beschrijving:**  
Retourneert Hallo sleutelalgoritme informatie voor deze X.509v3-certificaat als een tekenreeks.

**Syntaxis:**  
`str CertKeyAlgorithm(binary certificateRawData)`  
*   certificateRawData: Byte matrix representatie van een X.509-certificaat. Hallo-byte-matrix mag binair (DER), gecodeerd of Base64-gecodeerd x.509-gegevens.

- - -
### <a name="certkeyalgorithmparams"></a>CertKeyAlgorithmParams
**Beschrijving:**  
Retourneert een hexadecimale tekenreeks Hallo sleutelalgoritme parameters voor Hallo X.509v3-certificaat.

**Syntaxis:**  
`str CertKeyAlgorithm(binary certificateRawData)`  
*   certificateRawData: Byte matrix representatie van een X.509-certificaat. Hallo-byte-matrix mag binair (DER), gecodeerd of Base64-gecodeerd x.509-gegevens.

- - -
### <a name="certnameinfo"></a>CertNameInfo
**Beschrijving:**  
Retourneert Hallo onderwerp en de verlener namen van een certificaat.

**Syntaxis:**  
`str CertNameInfo(binary certificateRawData, str x509NameType, bool includesIssuerName)`  
*   certificateRawData: Byte matrix representatie van een X.509-certificaat. Hallo-byte-matrix mag binair (DER), gecodeerd of Base64-gecodeerd x.509-gegevens.
*   X509NameType: hello X509NameType waarde voor Hallo onderwerp.
*   includesIssuerName: true tooinclude Hallo certificaatverlener; anders wordt onwaar.

- - -
### <a name="certnotafter"></a>CertNotAfter
**Beschrijving:**  
Retourneert Hallo datum in plaatselijke tijd waarna een certificaat niet meer geldig is.

**Syntaxis:**  
`dt CertNotAfter(binary certificateRawData)`  
*   certificateRawData: Byte matrix representatie van een X.509-certificaat. Hallo-byte-matrix mag binair (DER), gecodeerd of Base64-gecodeerd x.509-gegevens.

- - -
### <a name="certnotbefore"></a>CertNotBefore
**Beschrijving:**  
Retourneert Hallo datum in plaatselijke tijd waarop een certificaat geldig wordt.

**Syntaxis:**  
`dt CertNotBefore(binary certificateRawData)`  
*   certificateRawData: Byte matrix representatie van een X.509-certificaat. Hallo-byte-matrix mag binair (DER), gecodeerd of Base64-gecodeerd x.509-gegevens.

- - -
### <a name="certpublickeyoid"></a>CertPublicKeyOid
**Beschrijving:**  
Retourneert Hallo Oid van de openbare sleutel Hallo voor Hallo X.509v3-certificaat.

**Syntaxis:**  
`str CertKeyAlgorithm(binary certificateRawData)`  
*   certificateRawData: Byte matrix representatie van een X.509-certificaat. Hallo-byte-matrix mag binair (DER), gecodeerd of Base64-gecodeerd x.509-gegevens.

- - -
### <a name="certpublickeyparametersoid"></a>CertPublicKeyParametersOid
**Beschrijving:**  
Retourneert Hallo Oid van Hallo openbare sleutel parameters voor Hallo X.509v3-certificaat.

**Syntaxis:**  
`str CertPublicKeyParametersOid(binary certificateRawData)`  
*   certificateRawData: Byte matrix representatie van een X.509-certificaat. Hallo-byte-matrix mag binair (DER), gecodeerd of Base64-gecodeerd x.509-gegevens.

- - -
### <a name="certserialnumber"></a>CertSerialNumber
**Beschrijving:**  
Retourneert het serienummer Hallo van Hallo X.509v3-certificaat.

**Syntaxis:**  
`str CertSerialNumber(binary certificateRawData)`  
*   certificateRawData: Byte matrix representatie van een X.509-certificaat. Hallo-byte-matrix mag binair (DER), gecodeerd of Base64-gecodeerd x.509-gegevens.

- - -
### <a name="certsignaturealgorithmoid"></a>CertSignatureAlgorithmOid
**Beschrijving:**  
Retourneert Hallo Oid van Hallo algoritme toocreate Hallo handtekening van een certificaat gebruikt.

**Syntaxis:**  
`str CertSignatureAlgorithmOid(binary certificateRawData)`  
*   certificateRawData: Byte matrix representatie van een X.509-certificaat. Hallo-byte-matrix mag binair (DER), gecodeerd of Base64-gecodeerd x.509-gegevens.

- - -
### <a name="certsubject"></a>CertSubject
**Beschrijving:**  
Opgehaald Hallo onderwerp DN-naam van een certificaat.

**Syntaxis:**  
`str CertSubject(binary certificateRawData)`  
*   certificateRawData: Byte matrix representatie van een X.509-certificaat. Hallo-byte-matrix mag binair (DER), gecodeerd of Base64-gecodeerd x.509-gegevens.

- - -
### <a name="certsubjectnamedn"></a>CertSubjectNameDN
**Beschrijving:**  
Retourneert Hallo onderwerp DN-naam van een certificaat.

**Syntaxis:**  
`str CertSubjectNameDN(binary certificateRawData)`  
*   certificateRawData: Byte matrix representatie van een X.509-certificaat. Hallo-byte-matrix mag binair (DER), gecodeerd of Base64-gecodeerd x.509-gegevens.

- - -
### <a name="certsubjectnameoid"></a>CertSubjectNameOid
**Beschrijving:**  
Retourneert Hallo Oid van Hallo onderwerp de naam van een certificaat.

**Syntaxis:**  
`str CertSubjectNameOid(binary certificateRawData)`  
*   certificateRawData: Byte matrix representatie van een X.509-certificaat. Hallo-byte-matrix mag binair (DER), gecodeerd of Base64-gecodeerd x.509-gegevens.

- - -
### <a name="certthumbprint"></a>certThumbprint
**Beschrijving:**  
Retourneert Hallo vingerafdruk van een certificaat.

**Syntaxis:**  
`str CertThumbprint(binary certificateRawData)`  
*   certificateRawData: Byte matrix representatie van een X.509-certificaat. Hallo-byte-matrix mag binair (DER), gecodeerd of Base64-gecodeerd x.509-gegevens.

- - -
### <a name="certversion"></a>CertVersion
**Beschrijving:**  
Retourneert Hallo versie van het X.509-indeling van een certificaat.

**Syntaxis:**  
`str CertThumbprint(binary certificateRawData)`  
*   certificateRawData: Byte matrix representatie van een X.509-certificaat. Hallo-byte-matrix mag binair (DER), gecodeerd of Base64-gecodeerd x.509-gegevens.

- - -
### <a name="cguid"></a>CGuid
**Beschrijving:**  
Hallo CGuid functie converteert Hallo tekenreeksweergave van een binaire voorstelling van GUID tooits.

**Syntaxis:**  
`bin CGuid(str GUID)`

* Een tekenreeks in dit patroon worden opgemaakt: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx of {xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}

- - -
### <a name="contains"></a>Contains
**Beschrijving:**  
Hallo bevat functie zoekt een tekenreeks binnen een kenmerk met meerdere waarden

**Syntaxis:**  
`num Contains (mvstring attribute, str search)`-hoofdlettergevoelig  
`num Contains (mvstring attribute, str search, enum Casetype)`  
`num Contains (mvref attribute, str search)`-hoofdlettergevoelig

* kenmerk: Hallo kenmerk met meerdere waarden toosearch.
* zoeken: string toofind in Hallo-kenmerk.
* Casetype: CaseInsensitive of CaseSensitive.

Retourneert index in een kenmerk met meerdere waarden Hallo waar Hallo-tekenreeks is gevonden. 0 wordt geretourneerd als het Hallo-tekenreeks is niet gevonden.

**Opmerkingen:**  
Voor tekenreekskenmerken met meerdere waarden Hallo gezocht subtekenreeksen in Hallo waarden.  
Voor verwijzingskenmerken moet hello gezochte tekenreeks exact overeenkomen Hallo waarde toobe beschouwd als een overeenkomst.

**Voorbeeld:**  
`IIF(Contains([proxyAddresses],"SMTP:")>0,[proxyAddresses],Error("No primary SMTP address found."))`  
Als Hallo proxyAddresses kenmerk een primaire e-mailadres heeft (aangeduid door hoofdletters ' SMTP: '), Ga daarna terug Hallo proxyAddress kenmerk, anders retourneren een foutmelding.

- - -
### <a name="convertfrombase64"></a>ConvertFromBase64
**Beschrijving:**  
Hallo ConvertFromBase64 functie converteert Hallo base64-gecodeerde waarde tooa reguliere tekenreeks opgegeven.

**Syntaxis:**  
`str ConvertFromBase64(str source)`-wordt ervan uitgegaan dat Unicode voor codering  
`str ConvertFromBase64(str source, enum Encoding)`

* bron: Base64-gecodeerde tekenreeks  
* -Codering: Unicode, ASCII, UTF8

**Voorbeeld**  
`ConvertFromBase64("SABlAGwAbABvACAAdwBvAHIAbABkACEA")`  
`ConvertFromBase64("SGVsbG8gd29ybGQh", UTF8)`

Beide voorbeelden retourneren '*Hello world!*'

- - -
### <a name="convertfromutf8hex"></a>ConvertFromUTF8Hex
**Beschrijving:**  
Hallo ConvertFromUTF8Hex functie converteert Hallo UTF8 hexadecimaal gecodeerde waarde tooa tekenreeks opgegeven.

**Syntaxis:**  
`str ConvertFromUTF8Hex(str source)`

* bron: UTF8 2-bytes gecodeerde String

**Opmerkingen:**  
Hallo verschil tussen deze functie en ConvertFromBase64([],UTF8) in die resulteren Hallo is beschrijvende voor Hallo DN-kenmerk.  
Deze indeling wordt gebruikt door Azure Active Directory als de DN-naam.

**Voorbeeld:**  
`ConvertFromUTF8Hex("48656C6C6F20776F726C6421")`  
Retourneert '*Hello world!*'

- - -
### <a name="converttobase64"></a>ConvertToBase64
**Beschrijving:**  
Hallo ConvertToBase64 functie zet een tekenreeks tooa Unicode base64-tekenreeks.  
Converteert Hallo-waarde van een matrix van gehele getallen tooits gelijkwaardige tekenreeksweergave die is gecodeerd met base 64-cijfers.

**Syntaxis:**  
`str ConvertToBase64(str source)`

**Voorbeeld:**  
`ConvertToBase64("Hello world!")`  
Retourneert 'SABlAGwAbABvACAAdwBvAHIAbABkACEA'

- - -
### <a name="converttoutf8hex"></a>ConvertToUTF8Hex
**Beschrijving:**  
Hallo ConvertToUTF8Hex functie zet een tekenreeks tooa UTF8 hexadecimaal gecodeerde waarde.

**Syntaxis:**  
`str ConvertToUTF8Hex(str source)`

**Opmerkingen:**  
Hallo de indeling van de uitvoer van deze functie wordt gebruikt door Azure Active Directory als de indeling van het kenmerk DN-naam.

**Voorbeeld:**  
`ConvertToUTF8Hex("Hello world!")`  
Retourneert 48656C6C6F20776F726C6421

- - -
### <a name="count"></a>Count
**Beschrijving:**  
Hallo functie Count retourneert Hallo aantal elementen in een kenmerk met meerdere waarden

**Syntaxis:**  
`num Count(mvstr attribute)`

- - -
### <a name="cnum"></a>CNum
**Beschrijving:**  
Hallo CNum functie een tekenreeks en retourneert een numeriek gegevenstype.

**Syntaxis:**  
`num CNum(str value)`

- - -
### <a name="cref"></a>CRef
**Beschrijving:**  
Zet een tekenreeks tooa-verwijzingskenmerk

**Syntaxis:**  
`ref CRef(str value)`

**Voorbeeld:**  
`CRef("CN=LC Services,CN=Microsoft,CN=lcspool01,CN=Pools,CN=RTC Service," & %Forest.LDAP%)`

- - -
### <a name="cstr"></a>CStr
**Beschrijving:**  
Hallo CStr functie converteert tooa tekenreeksgegevenstype.

**Syntaxis:**  
`str CStr(num value)`  
`str CStr(ref value)`  
`str CStr(bool value)`  

* waarde: een numerieke waarde, verwijzingskenmerk of Booleaanse waarde.

**Voorbeeld:**  
`CStr([dn])`  
Kan retourneren "cn = Jan, dc = contoso, dc = com"

- - -
### <a name="dateadd"></a>DateAdd
**Beschrijving:**  
Retourneert een datum met een datum toowhich die een opgegeven tijdsinterval is toegevoegd.

**Syntaxis:**  
`dt DateAdd(str interval, num value, dt date)`

* interval: tekenreeksexpressie die Hallo tijdsinterval tooadd gewenste. Hallo-tekenreeks moet een van de Hallo volgende waarden hebben:
  * JJJJ jaar
  * q kwartaal
  * m maand
  * y-dag van jaar
  * d dag
  * w weekdag
  * ww Week
  * h uur
  * n minuut
  * s tweede
* waarde: Hallo aantal eenheden dat u wilt dat tooadd. Kan een positieve waarde (tooget datums in toekomstige Hallo) of negatief (tooget datums in de afgelopen Hallo).
* datum: DateTime die toowhich Hallo datuminterval is toegevoegd.

**Voorbeeld:**  
`DateAdd("m", 3, CDate("2001-01-01"))`  
Drie maanden worden toegevoegd en retourneert een datetime-waarde die aangeeft '2001-04-01'.

- - -
### <a name="datefromnum"></a>DateFromNum
**Beschrijving:**  
Hallo DateFromNum functie converteert een waarde in de AD-datum notatie tooa DateTime-type.

**Syntaxis:**  
`dt DateFromNum(num value)`

**Voorbeeld:**  
`DateFromNum([lastLogonTimestamp])`  
`DateFromNum(129699324000000000)`  
Retourneert een datetime-waarde die aangeeft 01-01-2012 23:00:00 uur

- - -
### <a name="dncomponent"></a>DNComponent
**Beschrijving:**  
Hallo DNComponent functie retourneert Hallo-waarde van een opgegeven DN-onderdeel van links.

**Syntaxis:**  
`str DNComponent(ref dn, num ComponentNumber)`

* DN-naam: Hallo verwijzing kenmerk toointerpret
* ComponentNumber: hello onderdeel in Hallo DN tooreturn

**Voorbeeld:**  
`DNComponent([dn],1)`  
Als een DN-naam is "cn Kees, ou = =..., ' Jan wordt

- - -
### <a name="dncomponentrev"></a>DNComponentRev
**Beschrijving:**  
Hallo DNComponentRev functie retourneert Hallo-waarde van een opgegeven DN-onderdeel van rechts (Hallo end).

**Syntaxis:**  
`str DNComponentRev(ref dn, num ComponentNumber)`  
`str DNComponentRev(ref dn, num ComponentNumber, enum Options)`

* DN-naam: Hallo verwijzing kenmerk toointerpret
* ComponentNumber - hello onderdeel in Hallo DN tooreturn
* -Opties: DC-alle onderdelen met negeren ' dc = "

**Voorbeeld:**  
Als een DN-naam is "cn Kees, ou = Atlanta, ou = GA, ou = = US, dc = contoso, dc = com" vervolgens  
`DNComponentRev([dn],3)`  
`DNComponentRev([dn],1,"DC")`  
Beide retourneren ons.

- - -
### <a name="error"></a>Fout
**Beschrijving:**  
Hallo functie Error is gebruikte tooreturn een aangepaste fout.

**Syntaxis:**  
`void Error(str ErrorMessage)`

**Voorbeeld:**  
`IIF(IsPresent([accountName]),[accountName],Error("AccountName is required"))`  
Als Hallo attribuut accountName niet aanwezig is, genereert u een fout op Hallo-object.

- - -
### <a name="escapedncomponent"></a>EscapeDNComponent
**Beschrijving:**  
Hallo EscapeDNComponent functie duurt één onderdeel van een DN-naam en verlaat u zodat deze kan worden weergegeven in LDAP.

**Syntaxis:**  
`str EscapeDNComponent(str value)`

**Voorbeeld:**  
`EscapeDNComponent("cn=" & [displayName]) & "," & %ForestLDAP%)`  
Weet u zeker Hallo object kan worden gemaakt in een LDAP-adreslijst, zelfs wanneer Hallo displayName kenmerk tekens bevat die moeten worden voorafgegaan in LDAP.

- - -
### <a name="formatdatetime"></a>formatDateTime
**Beschrijving:**  
Hallo FormatDateTime functie is gebruikte tooformat DateTime tooa tekenreeks met de opgegeven notatie

**Syntaxis:**  
`str FormatDateTime(dt value, str format)`

* waarde: een waarde in Hallo datum-/ tijdindeling
* indeling: een Hallo indeling tooconvert naar type string.

**Opmerkingen:**  
Hallo mogelijke waarden voor Hallo indeling u hier vindt: [door de gebruiker gedefinieerde datum-/ tijdnotaties (functie Format)](http://msdn2.microsoft.com/library/73ctwf33\(VS.90\).aspx)

**Voorbeeld:**  

`FormatDateTime(CDate("12/25/2007"),"yyyy-mm-dd")`  
De resultaten in '2007-12-25'.

`FormatDateTime(DateFromNum([pwdLastSet]),"yyyyMMddHHmmss.0Z")`  
Kan leiden tot '20140905081453.0Z'

- - -
### <a name="guid"></a>GUID
**Beschrijving:**  
Hallo functie GUID genereert een nieuwe willekeurige GUID

**Syntaxis:**  
`str GUID()`

- - -
### <a name="iif"></a>IIF
**Beschrijving:**  
Hallo functie IIF retourneert een van de mogelijke waarden op basis van een opgegeven voorwaarde.

**Syntaxis:**  
`var IIF(exp condition, var valueIfTrue, var valueIfFalse)`

* voorwaarde: een waarde of expressie die kan worden geëvalueerd tootrue of ONWAAR.
* waardeindienwaar: als Hallo voorwaarde wordt geëvalueerd tootrue, Hallo waarde geretourneerd.
* WaardeAlsOnwaar: als Hallo voorwaarde wordt geëvalueerd toofalse, Hallo waarde geretourneerd.

**Voorbeeld:**  
`IIF([employeeType]="Intern","t-" & [alias],[alias])`  
 Als Hallo gebruiker een intern is, retourneert de alias van een gebruiker met 't-' hello toegevoegd toohello begin van deze anders retourneert Hallo gebruikersalias is.

- - -
### <a name="instr"></a>InStr
**Beschrijving:**  
Hallo functie InStr Hallo eerste exemplaar van een subtekenreeks wordt gevonden in een tekenreeks

**Syntaxis:**  

`num InStr(str stringcheck, str stringmatch)`  
`num InStr(str stringcheck, str stringmatch, num start)`  
`num InStr(str stringcheck, str stringmatch, num start , enum compare)`

* reekscontroleren: string toobe doorzocht
* reeksvergelijken: string toobe gevonden
* Start: positie toofind Hallo subtekenreeks wordt gestart
* Vergelijk: vbTextCompare of vbBinaryCompare

**Opmerkingen:**  
Retourneert Hallo positie waar Hallo subtekenreeks is gevonden, of 0 als niet gevonden.

**Voorbeeld:**  
`InStr("hello quick brown fox","quick")`  
Evalues too5

`InStr("repEated","e",3,vbBinaryCompare)`  
Evalueert too7

- - -
### <a name="instrrev"></a>InStrRev
**Beschrijving:**  
Hallo functie InStrRev Hallo laatste exemplaar van een subtekenreeks wordt gevonden in een tekenreeks

**Syntaxis:**  
`num InstrRev(str stringcheck, str stringmatch)`  
`num InstrRev(str stringcheck, str stringmatch, num start)`  
`num InstrRev(str stringcheck, str stringmatch, num start, enum compare)`

* reekscontroleren: string toobe doorzocht
* reeksvergelijken: string toobe gevonden
* Start: positie toofind Hallo subtekenreeks wordt gestart
* Vergelijk: vbTextCompare of vbBinaryCompare

**Opmerkingen:**  
Retourneert Hallo positie waar Hallo subtekenreeks is gevonden, of 0 als niet gevonden.

**Voorbeeld:**  
`InStrRev("abbcdbbbef","bb")`  
Retourneert 7

- - -
### <a name="isbitset"></a>IsBitSet
**Beschrijving:**  
Hallo-functie IsBitSet netwerktests als een bit is ingesteld of niet

**Syntaxis:**  
`bool IsBitSet(num value, num flag)`

* waarde: een numerieke waarde die is evaluated.flag: een numerieke waarde die Hallo is bit toobe geëvalueerd

**Voorbeeld:**  
`IsBitSet(&HF,4)`  
Retourneert True als omdat "4"-bit is ingesteld in Hallo hexadecimale waarde 'F'

- - -
### <a name="isdate"></a>IsDate
**Beschrijving:**  
Als het Hallo-expressie kan worden geëvalueerd als een DateTime-type vervolgens Hallo functie IsDate tooTrue evalueert.

**Syntaxis:**  
`bool IsDate(var Expression)`

**Opmerkingen:**  
Toodetermine gebruikt als CDate() uitgevoerd worden kan.

- - -
### <a name="iscert"></a>IsCert
**Beschrijving:**  
Retourneert waar als Hallo onbewerkte gegevens kunnen worden geserialiseerd in .NET X509Certificate2 certificaat-object.

**Syntaxis:**  
`bool CertThumbprint(binary certificateRawData)`  
*   certificateRawData: Byte matrix representatie van een X.509-certificaat. Hallo-byte-matrix mag binair (DER), gecodeerd of Base64-gecodeerd x.509-gegevens.
- - -
### <a name="isempty"></a>IsEmpty
**Beschrijving:**  
Als Hallo kenmerk aanwezig is in Hallo CS of MV maar tooan lege tekenreeks evalueert, evalueert de functie IsEmpty Hallo tooTrue.

**Syntaxis:**  
`bool IsEmpty(var Expression)`

- - -
### <a name="isguid"></a>IsGuid
**Beschrijving:**  
Als het Hallo-tekenreeks kan worden geconverteerd tooa GUID, geëvalueerd Hallo IsGuid functie tootrue.

**Syntaxis:**  
`bool IsGuid(str GUID)`

**Opmerkingen:**  
Een GUID is gedefinieerd als een tekenreeks die een van deze patronen te volgen: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx of {xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}

Toodetermine gebruikt als CGuid() uitgevoerd worden kan.

**Voorbeeld:**  
`IIF(IsGuid([strAttribute]),CGuid([strAttribute]),NULL)`  
Als Hallo StrAttribute heeft een GUID-indeling, een binaire voorstelling retourneren, anders een Null geretourneerd.

- - -
### <a name="isnull"></a>IsNull
**Beschrijving:**  
Als Hallo expressie tooNull resulteert, klikt u vervolgens de functie IsNull Hallo true ' geretourneerd.

**Syntaxis:**  
`bool IsNull(var Expression)`

**Opmerkingen:**  
Voor een kenmerk wordt een null-waarde uitgedrukt door Hallo afwezigheid van Hallo-kenmerk.

**Voorbeeld:**  
`IsNull([displayName])`  
Retourneert True als het Hallo-kenmerk is niet aanwezig in Hallo CS of MV.

- - -
### <a name="isnullorempty"></a>IsNullOrEmpty
**Beschrijving:**  
Als het Hallo-expressie is null of een lege tekenreeks, zijn Hallo IsNullOrEmpty functie retourneert true.

**Syntaxis:**  
`bool IsNullOrEmpty(var Expression)`

**Opmerkingen:**  
Voor een kenmerk, zou dit tooTrue evalueren of het Hallo-kenmerk ontbreekt of is aanwezig, maar is een lege tekenreeks.  
Hallo inverse van deze functie heet IsPresent.

**Voorbeeld:**  
`IsNullOrEmpty([displayName])`  
Retourneert True als het Hallo-kenmerk is niet aanwezig of is een lege tekenreeks in Hallo CS of MV.

- - -
### <a name="isnumeric"></a>IsNumeric
**Beschrijving:**  
Hallo IsNumeric functie retourneert een Booleaanse waarde die aangeeft of een expressie kan worden geëvalueerd als een type.

**Syntaxis:**  
`bool IsNumeric(var Expression)`

**Opmerkingen:**  
Toodetermine gebruikt als CNum() geslaagde tooparse Hallo expressie kan worden.

- - -
### <a name="isstring"></a>IsString
**Beschrijving:**  
Als het Hallo-expressie kan worden geëvalueerd tooa tekenreekstype, vervolgens Hallo IsString functie tooTrue evalueert.

**Syntaxis:**  
`bool IsString(var expression)`

**Opmerkingen:**  
Toodetermine gebruikt als CStr() geslaagde tooparse Hallo expressie kan worden.

- - -
### <a name="ispresent"></a>IsPresent
**Beschrijving:**  
Als Hallo expressie tooa tekenreeks die niet Null is en is niet leeg resulteert, Hallo vervolgens IsPresent functie ' true ' geretourneerd.

**Syntaxis:**  
`bool IsPresent(var expression)`

**Opmerkingen:**  
Hallo inverse van deze functie heet IsNullOrEmpty.

**Voorbeeld:**  
`Switch(IsPresent([directManager]),[directManager], IsPresent([skiplevelManager]),[skiplevelManager], IsPresent([director]),[director])`

- - -
### <a name="item"></a>Item
**Beschrijving:**  
Hallo functie Item retourneert één item van een tekenreeks/kenmerk met meerdere waarden.

**Syntaxis:**  
`var Item(mvstr attribute, num index)`

* kenmerk: kenmerk met meerdere waarden
* index: item van de index tooan in Hallo meerwaardige tekenreeks.

**Opmerkingen:**  
Hallo functie Item is nuttig in combinatie met de Hallo bevat de functie sinds de laatste functie Hallo retourneert Hallo index tooan item in een kenmerk met meerdere waarden Hallo.

Genereert een fout als de index valt buiten het bereik.

**Voorbeeld:**  
`Mid(Item([proxyAddress],Contains([proxyAddress], "SMTP:")),6)`  
Retourneert Hallo primaire e-mailadres.

- - -
### <a name="itemornull"></a>ItemOrNull
**Beschrijving:**  
Hallo ItemOrNull functie retourneert één item van een tekenreeks/kenmerk met meerdere waarden.

**Syntaxis:**  
`var ItemOrNull(mvstr attribute, num index)`

* kenmerk: kenmerk met meerdere waarden
* index: item van de index tooan in Hallo meerwaardige tekenreeks.

**Opmerkingen:**  
Hallo ItemOrNull-functie is handig samen met de Hallo bevat de functie sinds de laatste functie Hallo retourneert Hallo index tooan item in een kenmerk met meerdere waarden Hallo.

Als de index valt buiten het bereik, retourneert een Null-waarde.

- - -
### <a name="join"></a>Koppelen
**Beschrijving:**  
Hallo Join-functie een tekenreeks met meerdere waarden en retourneert een tekenreeks met één waarde met opgegeven scheidingsteken ingevoegd tussen de verschillende items.

**Syntaxis:**  
`str Join(mvstr attribute)`  
`str Join(mvstr attribute, str Delimiter)`

* kenmerk: kenmerk met meerdere waarden die toobe die lid zijn van tekenreeksen.
* scheidingsteken: een tekenreeks, gebruikte tooseparate Hallo subtekenreeksen in Hallo tekenreeks geretourneerd. Als u dit weglaat, Hallo spatie ("") wordt gebruikt. Als scheidingsteken een tekenreeks met lengte nul is ("") of niets, alle items in de lijst Hallo worden samengevoegd met zonder scheidingstekens.

**Opmerkingen**  
Er is een pariteit tussen Hallo Join en Split-functies. Hallo Join-functie wordt een matrix met tekenreeksen en koppelt deze met een scheidingsteken tekenreeks, tooreturn één tekenreeks. Hallo gesplitste functie een tekenreeks en afscheiding op Hallo scheidingsteken, tooreturn een matrix met tekenreeksen. Een belangrijk verschil is echter dat Join tekenreeksen met een willekeurige tekenreeks scheidingsteken kunt samenvoegen, gesplitste kunt alleen tekenreeksen met behulp van een enkel teken scheidingsteken scheiden.

**Voorbeeld:**  
`Join([proxyAddresses],",")`  
Kan retourneren: 'SMTP:john.doe@contoso.com,smtp:jd@contoso.com'

- - -
### <a name="lcase"></a>LCase
**Beschrijving:**  
Hallo LCase van converteert alle tekens in een tekenreeks toolower geval.

**Syntaxis:**  
`str LCase(str value)`

**Voorbeeld:**  
`LCase("TeSt")`  
Retourneert 'test'.

- - -
### <a name="left"></a>Links
**Beschrijving:**  
Hallo links functie retourneert een opgegeven aantal tekens vanaf de linkerkant Hallo van een tekenreeks.

**Syntaxis:**  
`str Left(str string, num NumChars)`

* tekenreeks: Hallo tekenreeks tooreturn tekens bevatten uit
* NumChars: een getal dat aangeeft Hallo aantal tekens tooreturn vanaf hello (links) van een tekenreeks

**Opmerkingen:**  
Een tekenreeks met Hallo eerste numChars tekens in de tekenreeks:

* Als numChars = 0, lege tekenreeks retourneren.
* Als numChars < 0, invoerreeks retourneren.
* Als de tekenreeks is null, leeg tekenreeks geretourneerd.

Als de tekenreeks bevat minder tekens dan Hallo getal dat is opgegeven in numChars, wordt een tekenreeks identieke toostring (d.w.z., met alle tekens in parameter 1) geretourneerd.

**Voorbeeld:**  
`Left("John Doe", 3)`  
Retourneert 'Joh'.

- - -
### <a name="len"></a>Len
**Beschrijving:**  
Hallo functie Len retourneert het aantal tekens in een tekenreeks.

**Syntaxis:**  
`num Len(str value)`

**Voorbeeld:**  
`Len("John Doe")`  
Retourneert 8

- - -
### <a name="ltrim"></a>LTrim
**Beschrijving:**  
Hallo LTrim functie verwijdert voorloopspaties wit uit een tekenreeks.

**Syntaxis:**  
`str LTrim(str value)`

**Voorbeeld:**  
`LTrim(" Test ")`  
Retourneert 'Test'

- - -
### <a name="mid"></a>Mid
**Beschrijving:**  
Hallo Mid functie retourneert een opgegeven aantal tekens van een opgegeven positie in een tekenreeks.

**Syntaxis:**  
`str Mid(str string, num start, num NumChars)`

* tekenreeks: Hallo tekenreeks tooreturn tekens bevatten uit
* Start: een getal dat aangeeft Hallo beginpositie in tekenreeks tooreturn tekens bevatten uit
* NumChars: een getal dat aangeeft Hallo aantal tooreturn tekens vanaf positie in de tekenreeks

**Opmerkingen:**  
Retour numChars tekens vanaf positie start in de tekenreeks.  
Een tekenreeks met numChars tekens vanaf het begin van de positie in de tekenreeks:

* Als numChars = 0, lege tekenreeks retourneren.
* Als numChars < 0, invoerreeks retourneren.
* Als start > Hallo lengte van tekenreeks, invoerreeks retourneren.
* Als starten < = 0, invoer-tekenreeks geretourneerd.
* Als de tekenreeks is null, leeg tekenreeks geretourneerd.

Als er niet numChar tekens worden resterend in de tekenreeks van positie-begin zoveel tekens mogelijk geretourneerd.

**Voorbeeld:**  
`Mid("John Doe", 3, 5)`  
Retourneert 'hn komen'.

`Mid("John Doe", 6, 999)`  
Retourneert 'De Vries'

- - -
### <a name="now"></a>Nu
**Beschrijving:**  
Hallo nu retourneert functie een datum/tijd Hallo huidige datum en tijd opgeven op basis van tooyour systeemdatum en -tijd.

**Syntaxis:**  
`dt Now()`

- - -
### <a name="numfromdate"></a>NumFromDate
**Beschrijving:**  
Hallo NumFromDate functie retourneert een datum in de datumnotatie van AD.

**Syntaxis:**  
`num NumFromDate(dt value)`

**Voorbeeld:**  
`NumFromDate(CDate("2012-01-01 23:00:00"))`  
Retourneert 129699324000000000

- - -
### <a name="padleft"></a>PadLeft
**Beschrijving:**  
Hallo PadLeft links pad functie een tekenreeks tooa opgegeven met behulp van een opgegeven opvulteken lengte.

**Syntaxis:**  
`str PadLeft(str string, num length, str padCharacter)`

* tekenreeks: Hallo toopad tekenreeks.
* lengte: een geheel getal dat Hallo gewenste lengte van tekenreeks.
* padCharacter: een tekenreeks die bestaat uit een enkel teken toouse als Hallo pad teken

**Opmerkingen:**

* Als het Hallo-lengte van tekenreeks is kleiner dan de lengte, vervolgens is padCharacter herhaaldelijk toegevoegde toohello begin (links) van een tekenreeks totdat er een gelijk toolength lengte.
* padCharacter mag een spatie, maar dit kan een null-waarde niet.
* Als Hallo lengte van tekenreeks gelijk tooor groter dan lengte is, wordt de tekenreeks ongewijzigd geretourneerd.
* Als de tekenreeks een lengte groter dan of gelijk zijn toolength heeft, wordt een identieke toostring tekenreeks geretourneerd.
* Als het Hallo-lengte van tekenreeks is kleiner dan de lengte, gewenst een nieuwe reeks Hallo lengte wordt geretourneerd met tekenreeks die is opgevuld met een padCharacter.
* Als de tekenreeks is null, Hallo een lege tekenreeks geretourneerd.

**Voorbeeld:**  
`PadLeft("User", 10, "0")`  
Retourneert '000000User'.

- - -
### <a name="padright"></a>PadRight
**Beschrijving:**  
Hallo PadRight rechts pad functie een tekenreeks tooa opgegeven met behulp van een opgegeven opvulteken lengte.

**Syntaxis:**  
`str PadRight(str string, num length, str padCharacter)`

* tekenreeks: Hallo toopad tekenreeks.
* lengte: een geheel getal dat Hallo gewenste lengte van tekenreeks.
* padCharacter: een tekenreeks die bestaat uit een enkel teken toouse als Hallo pad teken

**Opmerkingen:**

* Als het Hallo-lengte van tekenreeks is kleiner dan de lengte, wordt padCharacter herhaaldelijk toegevoegde toohello einde (rechts) van de tekenreeks totdat er een gelijk toolength lengte.
* padCharacter mag een spatie, maar dit kan een null-waarde niet.
* Als Hallo lengte van tekenreeks gelijk tooor groter dan lengte is, wordt de tekenreeks ongewijzigd geretourneerd.
* Als de tekenreeks een lengte groter dan of gelijk zijn toolength heeft, wordt een identieke toostring tekenreeks geretourneerd.
* Als het Hallo-lengte van tekenreeks is kleiner dan de lengte, gewenst een nieuwe reeks Hallo lengte wordt geretourneerd met tekenreeks die is opgevuld met een padCharacter.
* Als de tekenreeks is null, Hallo een lege tekenreeks geretourneerd.

**Voorbeeld:**  
`PadRight("User", 10, "0")`  
Retourneert 'User000000'.

- - -
### <a name="pcase"></a>PCase
**Beschrijving:**  
Hallo PCase functie converteert Hallo eerste teken van elk woord door spaties gescheiden in een tekenreeks tooupper-aanvraag en alle overige tekens worden geconverteerd toolower geval.

**Syntaxis:**  
`String PCase(string)`

**Opmerkingen:**

* Deze functie biedt momenteel geen juiste hoofdlettergebruik tooconvert een woord dat is volledig hoofdletters, zoals een acroniem.

**Voorbeeld:**  
`PCase("TEsT")`  
Retourneert 'Test'.

`PCase(LCase("TEST"))`  
Retourneert 'Test'

- - -
### <a name="randomnum"></a>RandomNum
**Beschrijving:**  
Hallo RandomNum functie retourneert een willekeurig getal tussen een opgegeven interval.

**Syntaxis:**  
`num RandomNum(num start, num end)`

* Start: een getal identificerende Hallo ondergrens van Hallo willekeurige waarde toogenerate
* end: een getal identificerende Hallo bovengrens van Hallo willekeurige waarde toogenerate

**Voorbeeld:**  
`Random(100,999)`  
734 kunnen worden geretourneerd.

- - -
### <a name="removeduplicates"></a>RemoveDuplicates
**Beschrijving:**  
Hallo RemoveDuplicates functie een tekenreeks met meerdere waarden en zorg ervoor dat elke waarde uniek is.

**Syntaxis:**  
`mvstr RemoveDuplicates(mvstr attribute)`

**Voorbeeld:**  
`RemoveDuplicates([proxyAddresses])`  
Retourneert een kenmerk opgeschoonde proxyAddress waar alle dubbele waarden zijn verwijderd.

- - -
### <a name="replace"></a>Vervangen
**Beschrijving:**  
Hallo functie vervangen vervangt alle instanties van een tekenreeks-tekenreeks tooanother.

**Syntaxis:**  
`str Replace(str string, str OldValue, str NewValue)`

* tekenreeks: een tekenreeks tooreplace in waarden.
* OldValue: Hallo tekenreeks toosearch voor en tooreplace.
* NewValue: Hallo tooreplace naar tekenreeks.

**Opmerkingen:**  
Hallo functie herkent Hallo speciale monikers te volgen:

* \n – nieuwe regel
* \r – regelterugloop
* \t – tabblad

**Voorbeeld:**  
`Replace([address],"\r\n",", ")`  
CRLF vervangt door een komma en een spatie en kan leiden te "One Microsoft manier, Redmond, WA, VS"

- - -
### <a name="replacechars"></a>ReplaceChars
**Beschrijving:**  
Hallo ReplaceChars functie vervangt alle instanties van de tekens uit de Hallo ReplacePattern tekenreeks.

**Syntaxis:**  
`str ReplaceChars(str string, str ReplacePattern)`

* tekenreeks: een tekenreeks tooreplace tekens in.
* ReplacePattern: een tekenreeks met een woordenlijst met tooreplace tekens.

Hallo-indeling is {bron1}: {target1}, {bron2}: {target2}, {bronN}, {targetN} waarbij bron Hallo teken toofind en doel Hallo tekenreeks tooreplace met is.

**Opmerkingen:**

* Hallo-functie heeft elk exemplaar van de gedefinieerde bronnen en Hallo doelen vervangen.
* Hallo-bron moet precies één teken voor (unicode).
* Hallo-bron kan niet leeg zijn of langer is dan één teken (parseerfout).
* Hallo doel kan meerdere tekens, bijvoorbeeld ö:oe, β:ss hebben.
* Hallo doel mag leeg die aangeeft dat Hallo teken moet worden verwijderd.
* Hallo-bron is hoofdlettergevoelig en moet een exacte overeenkomst.
* Hallo, (door komma's) en: (dubbele punt) zijn gereserveerde tekens en met deze functie kan niet worden vervangen.
* Spaties en andere witte tekens in Hallo ReplacePattern tekenreeks worden genegeerd.

**Voorbeeld:**  
`%ReplaceString% = ’:,Å:A,Ä:A,Ö:O,å:a,ä:a,ö,o`

`ReplaceChars("Räksmörgås",%ReplaceString%)`  
Retourneert Raksmorgas

`ReplaceChars("O’Neil",%ReplaceString%)`  
Retourneert 'ONeil', één maatstreepjes Hallo is gedefinieerde toobe verwijderd.

- - -
### <a name="right"></a>Rechts
**Beschrijving:**  
Hallo juiste functie retourneert een opgegeven aantal tekens van Hallo rechts (end) van een tekenreeks.

**Syntaxis:**  
`str Right(str string, num NumChars)`

* tekenreeks: Hallo tekenreeks tooreturn tekens bevatten uit
* NumChars: een getal dat aangeeft Hallo aantal tekens tooreturn van Hallo einde (rechts) van de tekenreeks

**Opmerkingen:**  
NumChars tekens geretourneerd vanaf de laatste positie Hallo van een tekenreeks.

Een tekenreeks met Hallo laatste numChars tekens in de tekenreeks:

* Als numChars = 0, lege tekenreeks retourneren.
* Als numChars < 0, invoerreeks retourneren.
* Als de tekenreeks is null, leeg tekenreeks geretourneerd.

Als de tekenreeks bevat minder tekens dan het aantal opgegeven in NumChars hello, wordt een identieke toostring tekenreeks geretourneerd.

**Voorbeeld:**  
`Right("John Doe", 3)`  
Retourneert 'De Vries'.

- - -
### <a name="rtrim"></a>RTrim
**Beschrijving:**  
Hallo functie RTrim verwijdert de afsluitende spaties uit een tekenreeks.

**Syntaxis:**  
`str RTrim(str value)`

**Voorbeeld:**  
`RTrim(" Test ")`  
Retourneert 'Test'.

- - -
### <a name="select"></a>Selecteer
**Beschrijving:**  
Proces alle waarden in een met meerdere waarden kenmerk (of uitvoer van een expressie) op basis van functie die is opgegeven.

**Syntaxis:**  
`mvattr Select(variable item, mvattr attribute, func function)`  
`mvattr Select(variable item, exp expression, func function)`

* item: Hiermee geeft u een element in een kenmerk met meerdere waarden Hallo
* kenmerk: Hallo een kenmerk met meerdere waarden
* expressie: een expressie die een verzameling waarden retourneert
* voorwaarde: de functie waarmee een item in het Hallo-kenmerk kan worden verwerkt.

**Voorbeelden:**  
`Select($item,[otherPhone],Replace($item,“-”,“”))`  
Alle Hallo-waarden in Hallo kenmerk met meerdere waarden otherPhone retourneren nadat afbreekstreepjes (-) zijn verwijderd.

- - -
### <a name="split"></a>Splitsen
**Beschrijving:**  
Hallo gesplitste functie een tekenreeks die van elkaar gescheiden door een scheidingsteken en maakt het een tekenreeks met meerdere waarden.

**Syntaxis:**  
`mvstr Split(str value, str delimiter)`  
`mvstr Split(str value, str delimiter, num limit)`

* waarde: string met een scheidingsteken teken tooseparate Hallo.
* scheidingsteken: één teken toobe als scheidingsteken Hallo gebruikt.
* limiet: maximum aantal waarden die kunnen worden geretourneerd.

**Voorbeeld:**  
`Split("SMTP:john.doe@contoso.com,smtp:jd@contoso.com",",")`  
Retourneert een tekenreeks met meerdere waarden met 2 elementen nuttig voor Hallo proxyAddress-kenmerk.

- - -
### <a name="stringfromguid"></a>StringFromGuid
**Beschrijving:**  
Hallo functie StringFromGuid neemt een binaire GUID en converteert deze tooa

**Syntaxis:**  
`str StringFromGuid(bin GUID)`

- - -
### <a name="stringfromsid"></a>StringFromSid
**Beschrijving:**  
Hallo StringFromSid functie converteert een bytematrix die een beveiligings-id tooa tekenreeks bevat.

**Syntaxis:**  
`str StringFromSid(bin ObjectSID)`  

- - -
### <a name="switch"></a>Switch
**Beschrijving:**  
de functie Switch Hallo is gebruikte tooreturn één waarde op basis van de geëvalueerde voorwaarden.

**Syntaxis:**  
`var Switch(exp expr1, var value1[, exp expr2, var value … [, exp expr, var valueN]])`

* expr: gewenste tooevaluate Variant-expressie.
* waarde: waarde toobe geretourneerd als de bijbehorende expressie Hallo waar is.

**Opmerkingen:**  
Hallo Switch functieargument bestaat uit combinaties van expressies en waarden. Hallo-expressies worden van links tooright geëvalueerd en Hallo-waarde die is gekoppeld aan Hallo eerste expressie tooevaluate tooTrue geretourneerd. Als het Hallo-onderdelen zijn niet correct is gekoppeld, wordt een runtime fout optreedt.

Als expr1 True is, retourneert Switch value1. Als expr-1 ingesteld op False is, maar expr 2 True is, retourneert Switch waarde 2, enzovoort.

Levert een switch als:

* Geen van de expressies Hallo is True.
* Hallo eerste ' True '-expressie heeft een overeenkomende waarde die Null is.

Switch evalueert alle expressies, ook al wordt slechts één van beide geretourneerd. Daarom moet u neveneffecten gecontroleerd. Als Hallo evaluatie van een expressie in een deling door nul-fout resulteert, wordt bijvoorbeeld een fout optreedt.

Waarde kan ook worden Hallo FOUTFUNCTIE, die een aangepaste tekenreeks geretourneerd.

**Voorbeeld:**  
`Switch([city] = "London", "English", [city] = "Rome", "Italian", [city] = "Paris", "French", True, Error("Unknown city"))`  
Hallo taal gesproken in sommige steden retourneert, anders wordt een fout geretourneerd.

- - -
### <a name="trim"></a>Trim
**Beschrijving:**  
Hallo Trim functie verwijdert voorloopspaties en afsluitende spaties uit een tekenreeks.

**Syntaxis:**  
`str Trim(str value)`  

**Voorbeeld:**  
`Trim(" Test ")`  
Retourneert 'Test'.

`Trim([proxyAddresses])`  
Verwijdert voorloopspaties en afsluitende spaties voor elke waarde in Hallo proxyAddress-kenmerk.

- - -
### <a name="ucase"></a>UCase
**Beschrijving:**  
Hallo UCase functie converteert alle tekens in een tekenreeks tooupper geval.

**Syntaxis:**  
`str UCase(str string)`

**Voorbeeld:**  
`UCase("TeSt")`  
Retourneert 'TEST'.

- - -
### <a name="where"></a>waar

**Beschrijving:**  
Retourneert een subset van de waarden van een met meerdere waarden kenmerk (of dezelfde uitvoer van een expressie) op basis van specifieke voorwaarde.

**Syntaxis:**  
`mvattr Where(variable item, mvattr attribute, exp condition)`  
`mvattr Where(variable item, exp expression, exp condition)`  
* item: Hiermee geeft u een element in een kenmerk met meerdere waarden Hallo
* kenmerk: Hallo een kenmerk met meerdere waarden
* voorwaarde: een expressie die kan worden geëvalueerd tootrue of ONWAAR
* expressie: een expressie die een verzameling waarden retourneert

**Voorbeeld:**  
`Where($item,[userCertificate],CertNotAfter($item)>Now())`  
Hallo certificaat waarden retourneren in Hallo kenmerk met meerdere waarden userCertificate die niet zijn verlopen.

- - -
### <a name="with"></a>met
**Beschrijving:**  
Hallo met de functie biedt een manier toosimplify een samengestelde expressie met behulp van een variabele toorepresent een subexpressie die één of meerdere keren in Hallo complexe expressie.

**Syntaxis:**
`With(var variable, exp subExpression, exp complexExpression)`  
* variabele: vertegenwoordigt Hallo subexpressie.
* Subexpressie: subexpressie dat wordt vertegenwoordigd door de variabele.
* complexExpression: een complexe expressie.

**Voorbeeld:**  
`With($unExpiredCerts,Where($item,[userCertificate],CertNotAfter($item)>Now()),IIF(Count($unExpiredCerts)>0,$unExpiredCerts,NULL))`  
Is functioneel equivalent met:  
`IIF (Count(Where($item,[userCertificate],CertNotAfter($item)>Now()))>0, Where($item,[userCertificate],CertNotAfter($item)>Now()),NULL)`  
Die alleen niet-verlopen certificaat waarden resulteert in Hallo userCertificate kenmerk.


- - -
### <a name="word"></a>Word
**Beschrijving:**  
Hallo Word functie retourneert een woord dat voorkomt in een tekenreeks, op basis van parameters Hallo scheidingstekens toouse en Hallo word nummer tooreturn beschrijven.

**Syntaxis:**  
`str Word(str string, num WordNumber, str delimiters)`

* tekenreeks: Hallo tekenreeks tooreturn een woord uit.
* WordNumber: een getal dat aangeeft welke word-nummer moet worden geretourneerd.
* scheidingstekens: een tekenreeks voor Hallo delimiter(s) die gebruikt tooidentify woorden worden moet

**Opmerkingen:**  
Elke reeks tekens in tekenreeks gescheiden door Hallo een Hallo tekens scheidingstekens worden aangeduid als woorden:

* Als < 1 nummer, het resultaat een lege tekenreeks.
* Als tekenreeks null is, retourneert lege tekenreeks.

Als de tekenreeks bevat minder dan het aantal woorden of tekenreeks bevat geen woorden geïdentificeerd door scheidingstekens, wordt een lege tekenreeks geretourneerd.

**Voorbeeld:**  
`Word("hello quick brown fox",3," ")`  
Retourneert 'bruine'

`Word("This,string!has&many separators",3,",!&#")`  
Retourneert 'is'

## <a name="additional-resources"></a>Aanvullende resources
* [Inzicht in expressies declaratieve inrichting](active-directory-aadconnectsync-understanding-declarative-provisioning-expressions.md)
* [Azure AD Connect-synchronisatie: Synchronisatie-opties voor aanpassen](active-directory-aadconnectsync-whatis.md)
* [Uw on-premises identiteiten integreren met Azure Active Directory](active-directory-aadconnect.md)

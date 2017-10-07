---
title: aaaAzure Media Services invoer metagegevensschema | Microsoft Docs
description: Hallo onderwerp overzicht een van de invoer metagegevensschema Azure Media Services.
author: Juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: d72848e2-4b65-4c84-94bc-e2a90a6e7f47
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: juliako
ms.openlocfilehash: 9b72c6ff317aa98451ea75548465dc6023b44a55
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="input-metadata"></a>Invoer metagegevens
Een codeertaak is gekoppeld aan een invoer asset (of activa) waarop tooperform sommige taken codering.  Na voltooiing van een taak wordt een uitvoerasset geproduceerd.  Hallo uitvoerasset video, audio, miniatuurweergaven manifest bevat, enz. Hallo uitvoerasset bevat ook een bestand met metagegevens over Hallo invoer asset. Hallo naam van XML-bestand met metagegevens Hallo heeft Hallo volgende indeling: &lt;asset_id&gt;_metadata.xml (bijvoorbeeld 41114ad3-eb5e - 4c 57 8d 92-5354e2b7d4a4_metadata.xml), waarbij &lt;asset_id&gt; Hallo item-id hebt is de waarde van Hallo invoer actief.  

Als u tooexamine Hallo metagegevensbestand wilt, kunt u een **SAS** locator en downloaden Hallo bestand tooyour lokale computer. U kunt een voorbeeld vinden over het toocreate een SAS-locator en downloaden van een bestand [Hallo Media Services .NET SDK Extensions met](media-services-dotnet-get-started.md).  

Dit onderwerp wordt besproken Hallo-elementen en typen van Hallo XML-schema op welke invoer metada hello (&lt;asset_id&gt;_metadata.xml) is gebaseerd.  Zie voor meer informatie over het Hallo-bestand met metagegevens over Hallo uitvoerasset [uitvoer metagegevens](media-services-output-metadata-schema.md).  

> [!NOTE]
> U vindt Hallo [Schema Code](media-services-input-metadata-schema.md#code) een [XML-voorbeeld](media-services-input-metadata-schema.md#xml) aan Hallo einde van dit onderwerp.  
> 
> 

## <a name="AssetFiles"></a>AssetFiles-element (element root)
Bevat een verzameling [AssetFile element](media-services-input-metadata-schema.md#AssetFile)s voor Hallo coderingstaak.  

Een XML-voorbeeld aan Hallo einde van dit onderwerp: [XML-voorbeeld](media-services-input-metadata-schema.md#xml).  

| Naam | Beschrijving |
| --- | --- |
| **AssetFile**<br /><br /> minOccurs = "1" maxOccurs = 'unbounded' |Een één onderliggend element. Zie voor meer informatie [AssetFile element](media-services-input-metadata-schema.md#AssetFile). |

## <a name="AssetFile"></a>AssetFile element
 Kenmerken en elementen die beschrijving van een assetbestand bevat.  

 Een XML-voorbeeld aan Hallo einde van dit onderwerp: [XML-voorbeeld](media-services-input-metadata-schema.md#xml).  

### <a name="attributes"></a>Kenmerken
| Naam | Type | Beschrijving |
| --- | --- | --- |
| **Naam**<br /><br /> Vereist |**xs:String** |Asset-bestandsnaam. |
| **Grootte**<br /><br /> Vereist |**xs:Long** |Grootte van Hallo asset bestandsgrootte in bytes. |
| **Duur**<br /><br /> Vereist |**xs: duration** |Inhoud afspelen back duur. Voorbeeld: Duur = 'PT25M37.757S'. |
| **NumberOfStreams**<br /><br /> Vereist |**xs:int** |Aantal gegevensstromen in Hallo assetbestand. |
| **FormatNames**<br /><br /> Vereist |**xs:String** |Indelingsnamen. |
| **FormatVerboseNames**<br /><br /> Vereist |**xs:String** |Uitgebreide indelingsnamen. |
| **StartTime** |**xs: duration** |Begintijd van inhoud. Voorbeeld: StartTime = 'PT2.669S'. |
| **OverallBitRate** |**xs:int** |Gemiddelde bitrate van Hallo asset-bestand in kbps. |

> [!NOTE]
> Hallo na 4 onderliggende elementen moet worden weergegeven in een reeks.  
> 
> 

### <a name="child-elements"></a>Onderliggende elementen
| Naam | Type | Beschrijving |
| --- | --- | --- |
| **Programma 's**<br /><br /> minOccurs = '0' | |Verzameling van alle [programma's element](media-services-input-metadata-schema.md#Programs) wanneer Hallo assetbestand heeft MPEG-TS-indeling. |
| **VideoTracks**<br /><br /> minOccurs = '0' | |Elk bestand fysiek activum kan nul of meer video houdt interleaved naar een indeling voor de juiste container bevatten. Dit element bevat een verzameling van alle [VideoTracks element](media-services-input-metadata-schema.md#VideoTracks) die deel uitmaken van Hallo assetbestand. |
| **AudioTracks**<br /><br /> minOccurs = '0' | |Elk bestand fysiek activum kan nul of meer audio houdt interleaved naar een indeling voor de juiste container bevatten. Dit element bevat een verzameling van alle [AudioTracks element](media-services-input-metadata-schema.md#AudioTracks) die deel uitmaken van Hallo assetbestand. |
| **Metagegevens**<br /><br /> minOccurs = "0" maxOccurs = 'unbounded' |[MetadataType](media-services-input-metadata-schema.md#MetadataType) |De metagegevens van assetbestand weergegeven als key\value tekenreeksen. Bijvoorbeeld:<br /><br /> **&lt;Metagegevenssleutel = waarde 'taal' = 'eng' /&gt;** |

## <a name="TrackType"></a>TrackType
Een XML-voorbeeld aan Hallo einde van dit onderwerp: [XML-voorbeeld](media-services-input-metadata-schema.md#xml).  

### <a name="attributes"></a>Kenmerken
| Naam | Type | Beschrijving |
| --- | --- | --- |
| **ID**<br /><br /> Vereist |**xs:int** |Op nul gebaseerde index van dit audio- of -nummer.<br /><br /> Dit is niet noodzakelijkerwijs dat Hallo TrackID zoals gebruikt in een MP4-bestand. |
| **Codec** |**xs:String** |Video bijhouden codec tekenreeks. |
| **CodecLongName** |**xs:String** |Audio- of bijhouden codec lange naam. |
| **Tijdsbasis**<br /><br /> Vereist |**xs:String** |Basis. Voorbeeld: Tijdsbasis = ' 1/48000' |
| **NumberOfFrames** |**xs:int** |Aantal frames (aanwezig voor video houdt). |
| **StartTime** |**xs: duration** |Begintijd bijhouden. Voorbeeld: StartTime = "PT2.669S" |
| **Duur** |**xs: duration** |Duur bijhouden. Voorbeeld: Duur = 'PTSampleFormat M37.757S'. |

> [!NOTE]
> Hallo na 2 onderliggende elementen moet worden weergegeven in een reeks.  
> 
> 

### <a name="child-elements"></a>Onderliggende elementen
| Naam | Type | Beschrijving |
| --- | --- | --- |
| **Toestand**<br /><br /> minOccurs = "0" maxOccurs = '1' |[StreamDispositionType](media-services-input-metadata-schema.md#StreamDispositionType) |Bevat presentatie-informatie (bijvoorbeeld, of een bepaalde-nummer is voor een visuele handicap viewers). |
| **Metagegevens**<br /><br /> minOccurs = "0" maxOccurs = 'unbounded' |[MetadataType](media-services-input-metadata-schema.md#MetadataType) |Algemene sleutel/waarde-tekenreeksen die gebruikt toohold tal van informatie worden kunnen. Bijvoorbeeld, sleutel = 'taal' en waarde = 'eng'. |

## <a name="AudioTrackType"></a>AudioTrackType (neemt over van TrackType)
 **AudioTrackType** is globale complex type die eigenschappen van overneemt [TrackType](media-services-input-metadata-schema.md#TrackType).  

 Hallo type vertegenwoordigt een specifieke-nummer in Hallo assetbestand.  

 Een XML-voorbeeld aan Hallo einde van dit onderwerp: [XML-voorbeeld](media-services-input-metadata-schema.md#xml).  

### <a name="attributes"></a>Kenmerken
| Naam | Type | Beschrijving |
| --- | --- | --- |
| **SampleFormat** |**xs:String** |Voorbeeld-indeling. |
| **ChannelLayout** |**xs:String** |Lay-out van kanaal. |
| **Kanalen**<br /><br /> Vereist |**xs:int** |Aantal (0 of meer) audio kanalen. |
| **SamplingRate**<br /><br /> Vereist |**xs:int** |Samplefrequentie van audio in steekproeven per seconde of Hz. |
| **Bitrate** |**xs:int** |Gemiddelde audio bitsnelheid in bits per seconde berekend op basis van Hallo assetbestand. Alleen Hallo elementaire stroom nettolading wordt beschouwd en Hallo verpakking overhead is niet opgenomen in deze telling. |
| **Het BitsPerSample** |**xs:int** |Bits per fragment voor Hallo wFormatTag indeling typt. |

## <a name="VideoTrackType"></a>VideoTrackType (neemt over van TrackType)
**VideoTrackType** is globale complex type die eigenschappen van overneemt [TrackType](media-services-input-metadata-schema.md#TrackType).  

Hallo type vertegenwoordigt een specifieke video bijhouden in Hallo assetbestand.  

Een XML-voorbeeld aan Hallo einde van dit onderwerp: [XML-voorbeeld](media-services-input-metadata-schema.md#xml).  

### <a name="attributes"></a>Kenmerken
| Naam | Type | Beschrijving |
| --- | --- | --- |
| **Code**<br /><br /> Vereist |**xs:String** |Video-codec code code. |
| **Profiel** |**xs:String** |Profiel van de video bijhouden. |
| **Niveau** |**xs:String** |Niveau van de video bijhouden. |
| **PixelFormat** |**xs:String** |Video bijhouden pixelindeling. |
| **Breedte**<br /><br /> Vereist |**xs:int** |Gecodeerde video breedte in pixels. |
| **Hoogte**<br /><br /> Vereist |**xs:int** |Gecodeerde video hoogte in pixels. |
| **DisplayAspectRatioNumerator**<br /><br /> Vereist |**xs:Double** |Beeldscherm hoogte-breedteverhouding teller. |
| **DisplayAspectRatioDenominator**<br /><br /> Vereist |**xs:Double** |Noemer voor de hoogte-breedteverhouding beeld weergegeven. |
| **DisplayAspectRatioDenominator**<br /><br /> Vereist |**xs:Double** |Video voorbeeld hoogte-breedteverhouding teller. |
| **SampleAspectRatioNumerator** |**xs:Double** |Video voorbeeld hoogte-breedteverhouding teller. |
| **SampleAspectRatioNumerator** |**xs:Double** |Noemer voor de hoogte-breedteverhouding video voorbeeld. |
| **Framesnelheid**<br /><br /> Vereist |**xs:decimal** |Framesnelheid van video .3f indeling gemeten. |
| **Bitrate** |**xs:int** |Gemiddelde video bitsnelheid in kilobits per seconde berekend op basis van Hallo assetbestand. Alleen Hallo elementaire stroom nettolading wordt beschouwd en Hallo verpakking overhead is niet opgenomen. |
| **MaxGOPBitrate** |**xs:int** |Gemiddelde bitrate Max GOP voor deze video spoor in kilobits per seconde. |
| **HasBFrames** |**xs:int** |Video bijhouden aantal B-frames. |

## <a name="MetadataType"></a>MetadataType
**MetadataType** is globale complex type die worden beschreven van metagegevens van een assetbestand als sleutel/waarde-tekenreeksen. Bijvoorbeeld, sleutel = 'taal' en waarde = 'eng'.  

Een XML-voorbeeld aan Hallo einde van dit onderwerp: [XML-voorbeeld](media-services-input-metadata-schema.md#xml).  

### <a name="attributes"></a>Kenmerken
| Naam | Type | Beschrijving |
| --- | --- | --- |
| **sleutel**<br /><br /> Vereist |**xs:String** |Hallo-sleutel in het sleutel-waardepaar Hallo. |
| **waarde**<br /><br /> Vereist |**xs:String** |Hallo-waarde in het sleutel-waardepaar Hallo. |

## <a name="ProgramType"></a>ProgramType
**ProgramType** is globale complex type die worden beschreven van een programma.  

### <a name="attributes"></a>Kenmerken
| Naam | Type | Beschrijving |
| --- | --- | --- |
| **ProgramId**<br /><br /> Vereist |**xs:int** |Programma-Id |
| **NumberOfPrograms**<br /><br /> Vereist |**xs:int** |Het aantal programma's. |
| **PmtPid**<br /><br /> Vereist |**xs:int** |Programma kaart tabellen (PMTs) bevatten informatie over programma's.  Zie voor meer informatie [BET](http://en.wikipedia.org/wiki/MPEG_transport_stream#PMT). |
| **PcrPid**<br /><br /> Vereist |**xs:int** |Door de decoder gebruikt. Zie voor meer informatie [PCR](http://en.wikipedia.org/wiki/MPEG_transport_stream#PCR) |
| **StartPTS** |**xs: lang** |Presentatie tijdstempel wordt gestart. |
| **EndPTS** |**xs: lang** |Beëindigen presentatie tijdstempel. |

## <a name="StreamDispositionType"></a>StreamDispositionType
**StreamDispositionType** is globale complex type die Hallo-stroom beschrijft.  

Een XML-voorbeeld aan Hallo einde van dit onderwerp: [XML-voorbeeld](media-services-input-metadata-schema.md#xml).  

### <a name="attributes"></a>Kenmerken
| Naam | Type | Beschrijving |
| --- | --- | --- |
| **Standaard**<br /><br /> Vereist |**xs:int** |Dit kenmerk too1 tooindicate die dit is de standaardpresentatie Hallo ingesteld. |
| **Dub**<br /><br /> Vereist |**xs:int** |Stel dit kenmerk too1 tooindicate deze optie is Hallo nagesynchroniseerd presentatie. |
| **Origineel**<br /><br /> Vereist |**xs:int** |Dit kenmerk too1 tooindicate die dit is de oorspronkelijke presentatie Hallo ingesteld. |
| **Opmerking**<br /><br /> Vereist |**xs:int** |Stel dit kenmerk too1 tooindicate deze bijhouden commentaar bevat. |
| **Tekst**<br /><br /> Vereist |**xs:int** |Stel dit kenmerk too1 tooindicate deze bijhouden tekst bevat. |
| **Karaoke**<br /><br /> Vereist |**xs:int** |Stel dit kenmerk too1 tooindicate dit vertegenwoordigt Hallo karaoke bijhouden (achtergrondmuziek, geen zang). |
| **Gedwongen**<br /><br /> Vereist |**xs:int** |Hallo gedwongen presentatie voor dit kenmerk too1 tooindicate die dit is ingesteld. |
| **HearingImpaired**<br /><br /> Vereist |**xs:int** |Dit kenmerk too1 tooindicate die dit nummer voor Hallo slechthorenden is ingesteld. |
| **VisualImpaired**<br /><br /> Vereist |**xs:int** |Dit kenmerk too1 tooindicate die dit nummer voor Hallo visueel functioneel is ingesteld. |
| **CleanEffects**<br /><br /> Vereist |**xs:int** |Schone gevolgen voor dit kenmerk too1 tooindicate die dit nummer is ingesteld. |
| **AttachedPic**<br /><br /> Vereist |**xs:int** |Afbeeldingen voor dit kenmerk too1 tooindicate die dit nummer is ingesteld. |

## <a name="Programs"></a>Programma's-element
Wrapper-element dat bevat meerdere **programma** elementen.  

### <a name="child-elements"></a>Onderliggende elementen
| Naam | Type | Beschrijving |
| --- | --- | --- |
| **Programma**<br /><br /> minOccurs = "0" maxOccurs = 'unbounded' |[ProgramType](media-services-input-metadata-schema.md#ProgramType) |Bevat informatie over software in het assetbestand Hallo voor assetbestanden MPEG-TS-indeling. |

## <a name="VideoTracks"></a>VideoTracks element
 Wrapper-element dat bevat meerdere **VideoTrack** elementen.  

 Een XML-voorbeeld aan Hallo einde van dit onderwerp: [XML-voorbeeld](media-services-input-metadata-schema.md#xml).  

### <a name="child-elements"></a>Onderliggende elementen
| Naam | Type | Beschrijving |
| --- | --- | --- |
| **VideoTrack**<br /><br /> minOccurs = "0" maxOccurs = 'unbounded' |[VideoTrackType (neemt over van TrackType)](media-services-input-metadata-schema.md#VideoTrackType) |Bevat informatie over video houdt in Hallo assetbestand. |

## <a name="AudioTracks"></a>AudioTracks element
 Wrapper-element dat bevat meerdere **AudioTrack** elementen.  

 Een XML-voorbeeld aan Hallo einde van dit onderwerp: [XML-voorbeeld](media-services-input-metadata-schema.md#xml).  

### <a name="elements"></a>Elementen
| Naam | Type | Beschrijving |
| --- | --- | --- |
| **AudioTrack**<br /><br /> minOccurs = "0" maxOccurs = 'unbounded' |[AudioTrackType (neemt over van TrackType)](media-services-input-metadata-schema.md#AudioTrackType) |Bevat informatie over audio houdt in Hallo assetbestand. |

## <a name="code"></a>Schema-Code
    <?xml version="1.0" encoding="utf-8"?>  
    <xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:msdata="urn:schemas-microsoft-com:xml-msdata" version="1.0"  
               xmlns="http://schemas.microsoft.com/windowsazure/mediaservices/2014/07/mediaencoder/inputmetadata"  
               targetNamespace="http://schemas.microsoft.com/windowsazure/mediaservices/2014/07/mediaencoder/inputmetadata"  
               elementFormDefault="qualified">  

      <xs:complexType name="MetadataType">  
        <xs:attribute name="key"   type="xs:string" use="required"/>  
        <xs:attribute name="value" type="xs:string" use="required"/>  
      </xs:complexType>  

      <xs:complexType name="ProgramType">  
        <xs:attribute name="ProgramId" type="xs:int" use="required">  
          <xs:annotation>  
            <xs:documentation>Program Id</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
        <xs:attribute name="NumberOfPrograms" type="xs:int" use="required">  
          <xs:annotation>  
            <xs:documentation>Number of programs</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
        <xs:attribute name="PmtPid" type="xs:int" use="required">  
          <xs:annotation>  
            <xs:documentation>pmt pid</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
        <xs:attribute name="PcrPid" type="xs:int" use="required">  
          <xs:annotation>  
            <xs:documentation>pcr pid</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
        <xs:attribute name="StartPTS" type="xs:long">  
          <xs:annotation>  
            <xs:documentation>start pts</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
        <xs:attribute name="EndPTS" type="xs:long">  
          <xs:annotation>  
            <xs:documentation>end pts</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
      </xs:complexType>  

      <xs:complexType name="StreamDispositionType">  
        <xs:attribute name="Default"          type="xs:int" use="required" />  
        <xs:attribute name="Dub"              type="xs:int" use="required" />  
        <xs:attribute name="Original"         type="xs:int" use="required" />  
        <xs:attribute name="Comment"          type="xs:int" use="required" />  
        <xs:attribute name="Lyrics"           type="xs:int" use="required" />  
        <xs:attribute name="Karaoke"          type="xs:int" use="required" />  
        <xs:attribute name="Forced"           type="xs:int" use="required" />  
        <xs:attribute name="HearingImpaired"  type="xs:int" use="required" />  
        <xs:attribute name="VisualImpaired"   type="xs:int" use="required" />  
        <xs:attribute name="CleanEffects"     type="xs:int" use="required" />  
        <xs:attribute name="AttachedPic"      type="xs:int" use="required" />  
      </xs:complexType>  

      <xs:complexType name="TrackType" abstract="true">  
        <xs:sequence>  
          <xs:element name="Disposition" type="StreamDispositionType" minOccurs="0" maxOccurs="1"/>  
          <xs:element name="Metadata" type="MetadataType" minOccurs="0" maxOccurs="unbounded"/>  
        </xs:sequence>  
        <xs:attribute name="Id" use="required">  
          <xs:annotation>  
            <xs:documentation>zero-based index of this video track. Note: this is not necessarily hello TrackID as used in an MP4 file</xs:documentation>  
          </xs:annotation>  
          <xs:simpleType>  
            <xs:restriction base="xs:int">  
              <xs:minInclusive value="0"/>  
            </xs:restriction>  
          </xs:simpleType>  
        </xs:attribute>  
        <xs:attribute name="Codec" type="xs:string">  
          <xs:annotation>  
            <xs:documentation>video track codec string</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
        <xs:attribute name="CodecLongName" type="xs:string">  
          <xs:annotation>  
            <xs:documentation>video track codec long name</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
        <xs:attribute name="TimeBase"  type="xs:string" use="required">  
          <xs:annotation>  
            <xs:documentation>Time base. Example: TimeBase="1/48000"</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
        <xs:attribute name="NumberOfFrames">  
          <xs:annotation>  
            <xs:documentation>number of frames</xs:documentation>  
          </xs:annotation>  
          <xs:simpleType>  
            <xs:restriction base="xs:int">  
              <xs:minInclusive value="0"/>  
            </xs:restriction>  
          </xs:simpleType>  
        </xs:attribute>  
        <xs:attribute name="StartTime" type="xs:duration">  
          <xs:annotation>  
            <xs:documentation>Track start time. Example: StartTime="PT2.669S"</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
        <xs:attribute name="Duration" type="xs:duration">  
          <xs:annotation>  
            <xs:documentation>Track duration. Example: Duration="PT25M37.757S"</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
      </xs:complexType>  

      <xs:complexType name="VideoTrackType">  
        <xs:annotation>  
          <xs:documentation>A specific video track in hello parent AssetFile</xs:documentation>  
        </xs:annotation>  
        <xs:complexContent>  
          <xs:extension base="TrackType">  
            <xs:attribute name="FourCC" type="xs:string" use="required">  
              <xs:annotation>  
                <xs:documentation>video codec FourCC code</xs:documentation>  
              </xs:annotation>  
            </xs:attribute>  
            <xs:attribute name="Profile" type="xs:string">  
              <xs:annotation>  
                <xs:documentation>profile</xs:documentation>  
              </xs:annotation>  
            </xs:attribute>  
            <xs:attribute name="Level" type="xs:string">  
              <xs:annotation>  
                <xs:documentation>level</xs:documentation>  
              </xs:annotation>  
            </xs:attribute>  
            <xs:attribute name="PixelFormat" type="xs:string">  
              <xs:annotation>  
                <xs:documentation>Video track's pixel format</xs:documentation>  
              </xs:annotation>  
            </xs:attribute>  
            <xs:attribute name="Width" use="required">  
              <xs:annotation>  
                <xs:documentation>encoded video width in pixels</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:int">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="Height" use="required">  
              <xs:annotation>  
                <xs:documentation>encoded video height in pixels</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:int">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="DisplayAspectRatioNumerator" use="required">  
              <xs:annotation>  
                <xs:documentation>video display aspect ratio numerator</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:double">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="DisplayAspectRatioDenominator" use="required">  
              <xs:annotation>  
                <xs:documentation>video display aspect ratio denominator</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:double">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="SampleAspectRatioNumerator">  
              <xs:annotation>  
                <xs:documentation>video sample aspect ratio numerator</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:double">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="SampleAspectRatioDenominator">  
              <xs:annotation>  
                <xs:documentation>video sample aspect ratio denominator</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:double">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="FrameRate" use="required">  
              <xs:annotation>  
                <xs:documentation>measured video frame rate in .3f format</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:decimal">  
                  <xs:minInclusive value="0"/>  
                  <xs:fractionDigits value="3"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="Bitrate">  
              <xs:annotation>  
                <xs:documentation>average video bit rate in kilobits per second, as calculated from hello AssetFile. Counts only hello elementary stream payload, and does not include hello packaging overhead</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:int">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="MaxGOPBitrate">  
              <xs:annotation>  
                <xs:documentation>Max GOP average bitrate for this video track, in kilobits per second</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:int">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="HasBFrames" type="xs:int">  
              <xs:annotation>  
                <xs:documentation>video track number of B frames</xs:documentation>  
              </xs:annotation>  
            </xs:attribute>  
          </xs:extension>  
        </xs:complexContent>  
      </xs:complexType>  

      <xs:complexType name="AudioTrackType">  
        <xs:annotation>  
          <xs:documentation>a specific audio track in hello parent AssetFile</xs:documentation>  
        </xs:annotation>  
        <xs:complexContent>  
          <xs:extension base="TrackType">  
            <xs:attribute name="SampleFormat"  type="xs:string">  
              <xs:annotation>  
                <xs:documentation>sample format</xs:documentation>  
              </xs:annotation>  
            </xs:attribute>  
            <xs:attribute name="ChannelLayout"  type="xs:string">  
              <xs:annotation>  
                <xs:documentation>channel layout</xs:documentation>  
              </xs:annotation>  
            </xs:attribute>  
            <xs:attribute name="Channels" use="required">  
              <xs:annotation>  
                <xs:documentation>number of audio channels</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:int">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="SamplingRate" use="required">  
              <xs:annotation>  
                <xs:documentation>audio sampling rate in samples/sec or Hz</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:int">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="Bitrate">  
              <xs:annotation>  
                <xs:documentation>average audio bit rate in bits per second, as calculated from hello AssetFile. Counts only hello elementary stream payload, and does not include hello packaging overhead</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:int">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="BitsPerSample">  
              <xs:annotation>  
                <xs:documentation>Bits per sample for hello wFormatTag format type</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:int">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
          </xs:extension>  
        </xs:complexContent>  
      </xs:complexType>  

      <xs:element name="AssetFiles">  
        <xs:annotation>  
          <xs:documentation>Collection of AssetFile entries for hello encoding job</xs:documentation>  
        </xs:annotation>  
        <xs:complexType>  
          <xs:sequence>  
            <xs:element name="AssetFile" minOccurs="1" maxOccurs="unbounded">  
              <xs:annotation>  
                <xs:documentation>asset file</xs:documentation>  
              </xs:annotation>  
              <xs:complexType>  
                <xs:sequence>  
                  <xs:element name="Programs" minOccurs="0">  
                    <xs:annotation>  
                      <xs:documentation>This is hello collection of all programs when file is MPEG-TS</xs:documentation>  
                    </xs:annotation>  
                    <xs:complexType>  
                      <xs:sequence>  
                        <xs:element name="Program" type="ProgramType" minOccurs="0" maxOccurs="unbounded" />  
                      </xs:sequence>  
                    </xs:complexType>  
                  </xs:element>  
                  <xs:element name="VideoTracks" minOccurs="0">  
                    <xs:annotation>  
                      <xs:documentation>Each physical AssetFile can contain in it zero or more video tracks interleaved into an appropriate container format. This is hello collection of all those video tracks</xs:documentation>  
                    </xs:annotation>  
                    <xs:complexType>  
                      <xs:sequence>  
                        <xs:element name="VideoTrack" type="VideoTrackType" minOccurs="0" maxOccurs="unbounded" />  
                      </xs:sequence>  
                    </xs:complexType>  
                  </xs:element>  
                  <xs:element name="AudioTracks" minOccurs="0">  
                    <xs:annotation>  
                      <xs:documentation>each physical AssetFile can contain in it zero or more audio tracks interleaved into an appropriate container format. This is hello collection of all those audio tracks</xs:documentation>  
                    </xs:annotation>  
                    <xs:complexType>  
                      <xs:sequence>  
                        <xs:element name="AudioTrack" type="AudioTrackType" minOccurs="0" maxOccurs="unbounded" />  
                      </xs:sequence>  
                    </xs:complexType>  
                  </xs:element>  
                  <xs:element name="Metadata" type="MetadataType" minOccurs="0" maxOccurs="unbounded" />  
                </xs:sequence>  
                <xs:attribute name="Name" type="xs:string" use="required">  
                  <xs:annotation>  
                    <xs:documentation>hello media asset file name</xs:documentation>  
                  </xs:annotation>  
                </xs:attribute>  
                <xs:attribute name="Size" use="required">  
                  <xs:annotation>  
                    <xs:documentation>size of file in bytes</xs:documentation>  
                  </xs:annotation>  
                  <xs:simpleType>  
                    <xs:restriction base="xs:long">  
                      <xs:minInclusive value="0"/>  
                    </xs:restriction>  
                  </xs:simpleType>  
                </xs:attribute>  
                <xs:attribute name="Duration" type="xs:duration" use="required">  
                  <xs:annotation>  
                    <xs:documentation>content play back duration. Example: Duration="PT25M37.757S"</xs:documentation>  
                  </xs:annotation>  
                </xs:attribute>  
                <xs:attribute name="NumberOfStreams" type="xs:int" use="required">  
                  <xs:annotation>  
                    <xs:documentation>number of streams in asset file</xs:documentation>  
                  </xs:annotation>  
                </xs:attribute>  
                <xs:attribute name="FormatNames" type="xs:string" use="required">  
                  <xs:annotation>  
                    <xs:documentation>format names</xs:documentation>  
                  </xs:annotation>  
                </xs:attribute>  
                <xs:attribute name="FormatVerboseName" type="xs:string" use="required">  
                  <xs:annotation>  
                    <xs:documentation>format verbose names</xs:documentation>  
                  </xs:annotation>  
                </xs:attribute>  
                <xs:attribute name="StartTime" type="xs:duration">  
                  <xs:annotation>  
                    <xs:documentation>content start time. Example: StartTime="PT2.669S"</xs:documentation>  
                  </xs:annotation>  
                </xs:attribute>  
                <xs:attribute name="OverallBitRate">  
                  <xs:annotation>  
                    <xs:documentation>average bitrate of hello asset file in kbps</xs:documentation>  
                  </xs:annotation>  
                  <xs:simpleType>  
                    <xs:restriction base="xs:int">  
                      <xs:minInclusive value="0"/>  
                    </xs:restriction>  
                  </xs:simpleType>  
                </xs:attribute>  
              </xs:complexType>  
            </xs:element>  
          </xs:sequence>  
        </xs:complexType>  
      </xs:element>  
    </xs:schema>  


## <a name="xml"></a>XML-voorbeeld
Hallo Hier volgt een voorbeeld van een metagegevensbestand Hallo-invoer.  

    <?xml version="1.0" encoding="utf-8"?>  
    <AssetFiles xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns="http://schemas.microsoft.com/windowsazure/mediaservices/2014/07/mediaencoder/inputmetadata">  
      <AssetFile Name="bear.mp4" Size="1973733" Duration="PT12.678S" NumberOfStreams="2" FormatNames="mov,mp4,m4a,3gp,3g2,mj2" FormatVerboseName="QuickTime / MOV" StartTime="PT0S" OverallBitRate="1245">  
        <VideoTracks>  
          <VideoTrack Id="1" Codec="h264" CodecLongName="H.264 / AVC / MPEG-4 AVC / MPEG-4 part 10" TimeBase="1/29970" NumberOfFrames="375" StartTime="PT0.034S" Duration="PT12.645S" FourCC="avc1" Profile="High" Level="4.1" PixelFormat="yuv420p" Width="512" Height="384" DisplayAspectRatioNumerator="4" DisplayAspectRatioDenominator="3" SampleAspectRatioNumerator="1" SampleAspectRatioDenominator="1" FrameRate="29.656" Bitrate="1043" HasBFrames="1">  
            <Disposition Default="1" Dub="0" Original="0" Comment="0" Lyrics="0" Karaoke="0" Forced="0" HearingImpaired="0" VisualImpaired="0" CleanEffects="0" AttachedPic="0" />  
            <Metadata key="creation_time" value="2010-03-10 16:11:56" />  
            <Metadata key="language" value="eng" />  
            <Metadata key="handler_name" value="Mainconcept MP4 Video Media Handler" />  
          </VideoTrack>  
        </VideoTracks>  
        <AudioTracks>  
          <AudioTrack Id="0" Codec="aac" CodecLongName="AAC (Advanced Audio Coding)" TimeBase="1/44100" NumberOfFrames="546" StartTime="PT0S" Duration="PT12.678S" SampleFormat="fltp" ChannelLayout="stereo" Channels="2" SamplingRate="44100" Bitrate="156" BitsPerSample="0">  
            <Disposition Default="1" Dub="0" Original="0" Comment="0" Lyrics="0" Karaoke="0" Forced="0" HearingImpaired="0" VisualImpaired="0" CleanEffects="0" AttachedPic="0" />  
            <Metadata key="creation_time" value="2010-03-10 16:11:56" />  
            <Metadata key="language" value="eng" />  
            <Metadata key="handler_name" value="Mainconcept MP4 Sound Media Handler" />  
          </AudioTrack>  
        </AudioTracks>  
        <Metadata key="major_brand" value="mp42" />  
        <Metadata key="minor_version" value="0" />  
        <Metadata key="compatible_brands" value="mp42mp41" />  
        <Metadata key="creation_time" value="2010-03-10 16:11:53" />  
        <Metadata key="comment" value="Courtesy of National Geographic.  Used by Permission." />  
      </AssetFile>  
    </AssetFiles>  

## <a name="next-steps"></a>Volgende stappen
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Feedback geven
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]


---
title: Codering-standaard schema aaaMedia | Microsoft Docs
description: Hallo onderwerp overzicht een van Media Encoder Standard Hallo-schema.
author: Juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: 4c060062-8ef2-41d9-834e-e81e8eafcf2e
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: juliako
ms.openlocfilehash: 82bad27b9546f75557ac691ff148b46990647632
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="media-encoder-standard-schema"></a>Media Encoder Standard schema
In dit onderwerp worden enkele Hallo-elementen en typen van Hallo XML-schema beschreven waarop [Media Encoder Standard voorinstellingen](media-services-mes-presets-overview.md) zijn gebaseerd. Hallo onderwerp geeft een uitleg van de elementen en hun geldige waarden. Hallo volledige schema wordt gepubliceerd op een later tijdstip.  

## <a name="Preset"></a>Voorinstelling (hoofdelement)
Hiermee definieert u een codering voorinstelling.  

### <a name="elements"></a>Elementen
| Naam | Type | Beschrijving |
| --- | --- | --- |
| **Codering** |[Codering](media-services-mes-schema.md#Encoding) |Hoofdelement, geeft aan dat de invoerbronnen Hallo toobe gecodeerd. |
| **Uitvoer** |[Uitvoer](media-services-mes-schema.md#Output) |Verzameling van gewenste uitvoerbestanden. |

### <a name="attributes"></a>Kenmerken
| Naam | Type | Beschrijving |
| --- | --- | --- |
| **Versie**<br/><br/> Vereist |**xs:decimal** |Hallo vooraf ingestelde versie. Hallo volgende beperkingen zijn van toepassing: xs:fractionDigits waarde = "1" en xs:minInclusive value = "1" bijvoorbeeld **versie = "1.0"**. |

## <a name="Encoding"></a>Codering
Bevat een reeks Hallo elementen te volgen.  

### <a name="elements"></a>Elementen
| Naam | Type | Beschrijving |
| --- | --- | --- |
| **H264Video** |[H264Video](media-services-mes-schema.md#H264Video) |Instellingen voor H.264-codering van video. |
| **AACAudio** |[AACAudio](media-services-mes-schema.md#AACAudio) |Instellingen voor AAC audio-codering. |
| **BmpImage** |[BmpImage](media-services-mes-schema.md#BmpImage) |Instellingen voor Bmp-afbeelding. |
| **PngImage** |[PngImage](media-services-mes-schema.md#PngImage) |Instellingen voor PNG-afbeelding. |
| **JpgImage** |[JpgImage](media-services-mes-schema.md#JpgImage) |Instellingen voor Jpg-afbeelding. |

## <a name="H264Video"></a>H264Video
### <a name="elements"></a>Elementen
| Naam | Type | Beschrijving |
| --- | --- | --- |
| **TwoPass**<br/><br/> minOccurs = '0' |**xs:Boolean** |Codering in slechts één keer wordt momenteel ondersteund. |
| **KeyFrameInterval**<br/><br/> minOccurs = '0'<br/><br/> **standaardwaarde = "00: 00:02 '** |**xs:time** |Hiermee wordt bepaald Hallo vaste afstand tussen IDR frames in eenheden van seconden. Ook wel aangeduid tooas Hallo GOP duur. Zie **SceneChangeDetection** (onder) voor het beheren of hello encoder mag afwijken van deze waarde. |
| **SceneChangeDetection**<br/><br/> minOccurs = '0'<br/><br/> standaardwaarde = "false" |**xs:Boolean** |Als set tootrue, encoder pogingen toodetect scene in Hallo video wijzigt en een frame IDR invoegen. |
| **Complexiteit**<br/><br/> minOccurs = '0'<br/><br/> standaardwaarde = 'Evenwichtig' |**xs:String** |Besturingselementen Hallo compromis tussen coderen snelheid en video. Kan een van de volgende waarden Hallo worden: **snelheid**, **Gebalanceerd**, of **kwaliteit**<br/><br/> Standaardwaarde: **met gelijke taakverdeling** |
| **SyncMode**<br/><br/> minOccurs = '0' | |Functie wordt in een toekomstige releases worden blootgesteld. |
| **H264Layers**<br/><br/> minOccurs = '0' |[H264Layers](media-services-mes-schema.md#H264Layers) |Verzameling van uitvoer video lagen. |

### <a name="attributes"></a>Kenmerken
| Naam | Type | Beschrijving |
| --- | --- | --- |
| **Voorwaarde** |**xs:String** | Wanneer het Hallo-invoer is geen video heeft, kunt u tooforce Hallo encoder tooinsert monochroom video bijgehouden. toodo die voorwaarde gebruiken voor de = 'InsertBlackIfNoVideoBottomLayerOnly' (tooinsert een video op alleen Hallo laagste bitrate) of voorwaarde = 'InsertBlackIfNoVideo' (een video op alle uitvoer bitsnelheden tooinsert). Raadpleeg [dit](media-services-advanced-encoding-with-mes.md#no_video) onderwerp voor meer informatie.|

## <a name="H264Layers"></a>H264Layers

Standaard als u een coderingsprogramma invoer toohello met alleen audio en geen video verzendt bevat Hallo uitvoerasset bestanden met alleen audiogegevens. Sommige spelers mogelijk geen toohandle dergelijke uitvoerstromen. U kunt de Hallo H264Video **InsertBlackIfNoVideo** kenmerk tooforce Hallo encoder tooadd de uitvoer van een video bijhouden toohello instellen in dat scenario. Raadpleeg [dit](media-services-advanced-encoding-with-mes.md#no_video) onderwerp voor meer informatie.
              
### <a name="elements"></a>Elementen
| Naam | Type | Beschrijving |
| --- | --- | --- |
| **H264Layer**<br/><br/> minOccurs = "0" maxOccurs = 'unbounded' |[H264Layer](media-services-mes-schema.md#H264Layer) |Een verzameling van lagen van de geselecteerde instelling H264. |

## <a name="H264Layer"></a>H264Layer
> [!NOTE]
> Video ondersteuningslimieten zijn gebaseerd op Hallo waarden in Hallo [niveaus van de geselecteerde instelling H264](https://en.wikipedia.org/wiki/H.264/MPEG-4_AVC#Levels) tabel.  
> 
> 

### <a name="elements"></a>Elementen
| Naam | Type | Beschrijving |
| --- | --- | --- |
| **Profiel**<br/><br/> minOccurs = '0'<br/><br/> standaardwaarde = 'Auto' |**xs:String** |Kan niet van een van de volgende Hallo **xs:string** waarden: **automatisch**, **basislijn**, **Main**, **hoge**. |
| **Niveau**<br/><br/> minOccurs = '0'<br/><br/> standaardwaarde = 'Auto' |**xs:String** | |
| **Bitrate**<br/><br/> minOccurs = '0' |**xs:int** |Hallo bitrate gebruikt voor deze video laag, opgegeven in kbps. |
| **MaxBitrate**<br/><br/> minOccurs = '0' |**xs:int** |Hallo maximale bitsnelheid gebruikt voor deze video laag, opgegeven in kbps. |
| **BufferWindow**<br/><br/> minOccurs = '0'<br/><br/> standaardwaarde = "00: 00:05 ' |**xs:time** |De lengte van Hallo video buffer. |
| **Breedte**<br/><br/> minOccurs = '0' |**xs:int** |De breedte van Hallo uitvoer video frame in pixels.<br/><br/> Houd er rekening mee dat op dit moment moet u zowel de breedte en hoogte. Hallo breedte en hoogte moet toobe even getallen. |
| **Hoogte**<br/><br/> minOccurs = '0' |**xs:int** |De hoogte van Hallo uitvoer video frame in pixels.<br/><br/> Houd er rekening mee dat op dit moment moet u zowel de breedte en hoogte. Hallo breedte en hoogte moet toobe even getallen.|
| **BFrames**<br/><br/> minOccurs = '0' |**xs:int** |Het aantal B frames tussen verwijzing frames. |
| **ReferenceFrames**<br/><br/> minOccurs = '0'<br/><br/> standaardwaarde = "3" |**xs:int** |Aantal frames in een GOP verwijzing. |
| **EntropyMode**<br/><br/> minOccurs = '0'<br/><br/> standaardwaarde = 'Cabac' |**xs:String** |Kan een van de volgende waarden Hallo worden: **Cabac** en **Cavlc**. |
| **Framesnelheid**<br/><br/> minOccurs = '0' |rationele getal |Hiermee wordt bepaald Hallo framesnelheid van video Hallo-uitvoer. De standaardwaarde ' 0/1' toolet Hallo encoder gebruik Hallo hetzelfde frame beoordelen als invoer Hallo video gebruiken. Toegestane waarden zijn verwachte toobe algemene video frame tarieven, zoals hieronder wordt weergegeven. Echter, een geldige rationele is toegestaan. Bijvoorbeeld 1/1 1 fps zou zijn en geldig is.<br/><br/> -12/1 (12 fps)<br/><br/> -15/1 (15 fps)<br/><br/> -24/1 (24 fps)<br/><br/> 24000/1001 (23.976 fps)<br/><br/> -25/1 (25 fps)<br/><br/>  -30/1 (30 fps)<br/><br/> 30000/1001 (29,97 fps) <br/> <br/>**Opmerking** als u een aangepaste voorinstelling voor het coderen van meerdere bitrate maakt, vervolgens alle lagen van Hallo voorinstelling **moet** gebruik Hallo dezelfde waarde van framesnelheid.|
| **AdaptiveBFrame**<br/><br/> minOccurs = '0' |**xs:Boolean** |Kopiëren van Azure media encoder |
| **Segmenten**<br/><br/> minOccurs = '0'<br/><br/> standaardwaarde = '0' |**xs:int** |Hiermee wordt bepaald hoeveel segmenten een frame is onderverdeeld in. Raden het gebruik van standaard. |

## <a name="AACAudio"></a>AACAudio
 Bevat een reeks Hallo volgende elementen en groepen.  

 Zie voor meer informatie over AAC [AAC](https://en.wikipedia.org/wiki/Advanced_Audio_Coding).  

### <a name="elements"></a>Elementen
| Naam | Type | Beschrijving |
| --- | --- | --- |
| **Profiel**<br/><br/> minOccurs = '0'<br/><br/> standaardwaarde = 'AACLC' |**xs:String** |Kan een van de volgende waarden Hallo worden: **AACLC**, **HEAACV1**, of **HEAACV2**. |

### <a name="attributes"></a>Kenmerken
| Naam | Type | Beschrijving |
| --- | --- | --- |
| **Voorwaarde** |**xs:String** |tooforce hello encoder tooproduce een activum met een achtergrond-nummer invoer bevat geen audio Hallo 'InsertSilenceIfNoAudio'-waarde opgeven.<br/><br/> Standaard als u een coderingsprogramma invoer toohello met alleen video en geen audio verzendt bevat vervolgens Hallo uitvoerasset bestanden die alleen video gegevens bevatten. Sommige spelers mogelijk geen toohandle dergelijke uitvoerstromen. In dit scenario kunt u deze instelling tooforce Hallo encoder tooadd een achtergrond-nummer toohello uitvoer. |

### <a name="groups"></a>Groepen
| Naslaginformatie | Beschrijving |
| --- | --- |
| [AudioGroup](media-services-mes-schema.md#AudioGroup)<br/><br/> minOccurs = '0' |Zie de beschrijving van [AudioGroup](media-services-mes-schema.md#AudioGroup) tooknow Hallo geschikt aantal kanalen, samplefrequentie en bitsnelheid die kan worden ingesteld voor elk profiel. |

## <a name="AudioGroup"></a>AudioGroup
Zie voor meer informatie over welke waarden geldig voor elk profiel zijn Hallo "Audio codec gegevens" tabel hieronder.  

### <a name="elements"></a>Elementen
| Naam | Type | Beschrijving |
| --- | --- | --- |
| **Kanalen**<br/><br/> minOccurs = '0' |**xs:int** |Hallo aantal audio kanalen die zijn gecodeerd. Hallo volgen geldige opties: 1, 2, 5, 6, 8.<br/><br/> Standaard: 2. |
| **SamplingRate**<br/><br/> minOccurs = '0' |**xs:int** |Hallo samplefrequentie van audio, opgegeven in Hz. |
| **Bitrate**<br/><br/> minOccurs = '0' |**xs:int** |Hallo bitrate gebruikt wanneer codering Hallo audio, opgegeven in kbps. |

### <a name="audio-codec-details"></a>Audio-codec details
Audio-Codec|Details  
-----------------|---  
**AACLC**|1:<br/><br/> -11025: 8 &lt;= bitrate &lt; 16<br/><br/> -12000: 8 &lt;= bitrate &lt; 16<br/><br/> -16000: 8 &lt;= bitrate &lt;32<br/><br/>-22050: 24 &lt;= bitrate &lt; 32<br/><br/> -24000: 24 &lt;= bitrate &lt; 32<br/><br/> -32000: 32 &lt;bitrate = &lt;= 192<br/><br/> -44100: 56 &lt;= bitrate &lt;288 =<br/><br/> -48000: 56 &lt;= bitrate &lt;288 =<br/><br/> -88200: 128 &lt;= bitrate &lt;288 =<br/><br/> -96000: 128 &lt;= bitrate &lt;288 =<br/><br/> 2:<br/><br/> -11025: 16 &lt;= bitrate &lt; 24<br/><br/> -12000: 16 &lt;= bitrate &lt; 24<br/><br/> -16000: 16 &lt;= bitrate &lt; 40<br/><br/> -22050: 32 &lt;= bitrate &lt; 40<br/><br/> -24000: 32 &lt;= bitrate &lt; 40<br/><br/> -32000: 40 &lt;bitrate = &lt;= 384<br/><br/> -44100: 96 &lt;= bitrate &lt;576 =<br/><br/> -48000: 96 &lt;= bitrate &lt;576 =<br/><br/> -88200: 256 &lt;= bitrate &lt;576 =<br/><br/> -96000: 256 &lt;= bitrate &lt;576 =<br/><br/> 5/6:<br/><br/> -32000: 160 &lt;= bitrate &lt;896 =<br/><br/> -44100: 240 &lt;= bitrate &lt;1024 =<br/><br/> -48000: 240 &lt;= bitrate &lt;1024 =<br/><br/> -88200: 640 &lt;= bitrate &lt;1024 =<br/><br/> -96000: 640 &lt;= bitrate &lt;1024 =<br/><br/> 8:<br/><br/> -32000: 224 &lt;= bitrate &lt;1024 =<br/><br/> -44100: 384 &lt;= bitrate &lt;1024 =<br/><br/> -48000: 384 &lt;= bitrate &lt;1024 =<br/><br/> -88200: 896 &lt;= bitrate &lt;1024 =<br/><br/> -96000: 896 &lt;= bitrate &lt;1024 =  
**HEAACV1**|1:<br/><br/> -22050: bitrate = 8<br/><br/> -24000: 8 &lt;bitrate = &lt;= 10<br/><br/> -32000: 12 &lt;bitrate = &lt;= 64<br/><br/> -44100: 20 &lt;bitrate = &lt;= 64<br/><br/> -48000: 20 &lt;bitrate = &lt;= 64<br/><br/> -88200: bitrate = 64<br/><br/> 2:<br/><br/> -32000: 16 &lt;bitrate = &lt;= 128<br/><br/> -44100: 16 &lt;bitrate = &lt;= 128<br/><br/> -48000: 16 &lt;bitrate = &lt;= 128<br/><br/> -88200: 96 &lt;bitrate = &lt;= 128<br/><br/> -96000: 96 &lt;bitrate = &lt;= 128<br/><br/> 5/6:<br/><br/> -32000: 64 &lt;= bitrate &lt;320 =<br/><br/> -44100: 64 &lt;= bitrate &lt;320 =<br/><br/> -48000: 64 &lt;= bitrate &lt;320 =<br/><br/> -88200: 256 &lt;= bitrate &lt;320 =<br/><br/> -96000: 256 &lt;= bitrate &lt;320 =<br/><br/> 8:<br/><br/> -32000: 96 &lt;bitrate = &lt;= 448<br/><br/> -44100: 96 &lt;bitrate = &lt;= 448<br/><br/> -48000: 96 &lt;bitrate = &lt;= 448<br/><br/> -88200: 384 &lt;bitrate = &lt;= 448<br/><br/> -96000: 384 &lt;bitrate = &lt;= 448  
**HEAACV2**|2:<br/><br/> -22050: 8 &lt;bitrate = &lt;= 10<br/><br/> -24000: 8 &lt;bitrate = &lt;= 10<br/><br/> -32000: 12 &lt;bitrate = &lt;= 64<br/><br/> -44100: 20 &lt;bitrate = &lt;= 64<br/><br/> -48000: 20 &lt;bitrate = &lt;= 64<br/><br/> -88200: 64 &lt;bitrate = &lt;= 64  
  

## <a name="Clip"></a>Clip
### <a name="attributes"></a>Kenmerken
| Naam | Type | Beschrijving |
| --- | --- | --- |
| **StartTime** |**xs: duration** |Hiermee geeft u de begintijd Hallo van een presentatie. Hallo-waarde van StartTime moet toomatch Hallo absolute tijdstempels van Hallo invoervideo. Bijvoorbeeld, als hello eerste frame van Hallo invoervideo een tijdstempel van 12:00:10.000 heeft, wordt StartTime moet ten minste 12:00:10.000 of hoger. |
| **Duur** |**xs: duration** |Hiermee geeft u Hallo duur van de presentatie (bijvoorbeeld de vormgeving van een overlay in Hallo video). |

## <a name="Output"></a>Uitvoer
### <a name="attributes"></a>Kenmerken
| Naam | Type | Beschrijving |
| --- | --- | --- |
| **Bestandsnaam** |**xs:String** |Hallo-naam van het uitvoerbestand Hallo.<br/><br/> U kunt macro's beschreven in Hallo tabel toobuild Hallo uitvoernamen-bestand te volgen. Bijvoorbeeld:<br/><br/> **'Uitvoer': [{"FileName": "{Basename}*{resolutie}*MP4 {Bitrate} ', 'Indeling': {'Type': 'MP4Format'}}] ** |

### <a name="macros"></a>Macro 's
| Macro | Beschrijving |
| --- | --- |
| **{Basename}** |Als u VoD-codering, is Hallo {Basename} Hallo eerste 32 tekens van Hallo AssetFile.Name eigenschap van het primaire bestand Hallo Hallo invoer actief in.<br/><br/> Als invoer asset Hallo een live-archief is, is klikt u vervolgens hello {Basename} afgeleid van Hallo trackName kenmerken in het manifest voor Hallo-server. Als u een subclip taak Hallo TopBitrate, zoals in indient: ' < VideoStream\>TopBitrate < / VideoStream\>', en het uitvoerbestand Hallo bevat video en klik vervolgens Hallo {Basename} is de eerste 32 tekens van Hallo trackName Hallo Hallo video laag met de hoogste bitrate Hallo.<br/><br/> Als u in plaats daarvan het indienen van een subclip taak met alle invoer bitsnelheden hello, zoals ' < VideoStream\>* < / VideoStream\>', en Hallo uitvoerbestand bevat video en klik vervolgens {Basename} is Hallo eerst 32 tekens van Hallo trackName van Hallo bijbehorende video laag. |
| **{Codec}** |Toegewezen te 'Standaardinstelling H264' voor video en 'AAC' voor audio. |
| **{Bitrate}** |Hallo doel video bitrate als Hallo uitvoerbestand video en audio bevat of audio bitrate doel als Hallo uitvoerbestand alleen audio bevat. Hallo-waarde die wordt gebruikt is Hallo bitrate in kbps. |
| **{Kanaal}** |Aantal audio-kanalen als Hallo-bestand audio bevat. |
| **{Breedte}** |Breedte van Hallo video, in pixels in Hallo uitvoerbestand als Hallo-bestand video bevat. |
| **{Hoogte}** |Hoogte van Hallo video, in pixels in Hallo uitvoerbestand als Hallo-bestand video bevat. |
| **{De extensie}** |Neemt over van de eigenschap 'Type' voor het uitvoerbestand Hallo Hallo. naam van het uitvoerbestand Hallo heeft een extensie die een van: 'mp4', 'ts', 'jpg', 'png' of 'bmp'. |
| **{Index}** |Verplicht voor de miniatuur. Alleen te aanwezig zijn eenmaal. |

## <a name="Video"></a>Video (complex type neemt over van Codec)
### <a name="attributes"></a>Kenmerken
| Naam | Type | Beschrijving |
| --- | --- | --- |
| **Beginnen** |**xs:String** | |
| **Stap** |**xs:String** | |
| **Bereik** |**xs:String** | |
| **PreserveResolutionAfterRotation** |**xs:Boolean** |Zie voor gedetailleerde uitleg Hallo volgende sectie: [PreserveResolutionAfterRotation](media-services-mes-schema.md#PreserveResolutionAfterRotation) |

### <a name="PreserveResolutionAfterRotation"></a>PreserveResolutionAfterRotation
Het verdient aanbeveling toouse hello PreserveResolutionAfterRotation vlag in combinatie met de omzetting van waarden die zijn uitgedrukt in percentages (Width = "100%", hoogte = "100%").  

Standaard coderen Hallo resolutie-instellingen (Width en Height) in Hallo Media Encoder Standard (MES) standaardinstellingen zijn gericht op video's met 0 graden. Bijvoorbeeld, als uw invoervideo 1280 x 720 met nul graden is, vervolgens Hallo standaard standaardinstellingen ervoor zorgen dat Hallo uitvoer Hallo dezelfde resolutie. Zie de volgende afbeelding.  

![MESRoation1](./media/media-services-shemas/media-services-mes-roation1.png) 

Echter, dit betekent dat als Hallo invoer video is opgenomen met niet-nul draaihoek (bv. een smartphone of tablet ondergebracht verticaal), en vervolgens MES standaard van toepassing hello resolutie instellingen (Width en Height) toohello video invoer en vervolgens compenseren voor Hallo rotatie coderen. Zie bijvoorbeeld Hallo in de volgende afbeelding. Hello voorinstelling gebruikt Width = "100%", hoogte = "100%", die MES wordt opgevat als het vereisen van Hallo uitvoer toobe 1280 pixels breed en 720 pixels hoog. Na het Hallo-video draaien, wordt deze vervolgens kleiner Hallo afbeelding toofit in dit venster toopillar vak gebieden op Hallo voorloopspaties linker- en.  

![MESRoation2](./media/media-services-shemas/media-services-mes-roation2.png) 

Als Hallo bovenstaande niet Hallo gewenst gedrag is, dan kunt u het gebruik van Hallo PreserveResolutionAfterRotation vlag en in te stellen te 'true' (de standaardwaarde is "false"). Dus als uw vooraf ingestelde breedte heeft = "100%", hoogte = "100%" en PreserveResolutionAfterRotation instellen te 'true', waarmee een invoervideo die 1280 pixels breed en 720 pixels hoog met 90 graden met nul graden maar 720 pixels breed en 1280 uitvoer wordt geproduceerd pixels hoog. Zie de volgende Hallo-afbeelding.  

![MESRoation3](./media/media-services-shemas/media-services-mes-roation3.png) 

## <a name="FormatGroup"></a>FormatGroup (groeps)
### <a name="elements"></a>Elementen
| Naam | Type | Beschrijving |
| --- | --- | --- |
| **BmpFormat** |**BmpFormat** | |
| **PngFormat** |**PngFormat** | |
| **JpgFormat** |**JpgFormat** | |

## <a name="BmpLayer"></a>BmpLayer
### <a name="element"></a>Element
| Naam | Type | Beschrijving |
| --- | --- | --- |
| **Breedte**<br/><br/> minOccurs = '0' |**xs:int** | |
| **Hoogte**<br/><br/> minOccurs = '0' |**xs:int** | |

### <a name="attributes"></a>Kenmerken
| Naam | Type | Beschrijving |
| --- | --- | --- |
| **Voorwaarde** |**xs:String** | |

## <a name="PngLayer"></a>PngLayer
### <a name="element"></a>Element
| Naam | Type | Beschrijving |
| --- | --- | --- |
| **Breedte**<br/><br/> minOccurs = '0' |**xs:int** | |
| **Hoogte**<br/><br/> minOccurs = '0' |**xs:int** | |

### <a name="attributes"></a>Kenmerken
| Naam | Type | Beschrijving |
| --- | --- | --- |
| **Voorwaarde** |**xs:String** | |

## <a name="JpgLayer"></a>JpgLayer
### <a name="element"></a>Element
| Naam | Type | Beschrijving |
| --- | --- | --- |
| **Breedte**<br/><br/> minOccurs = '0' |**xs:int** | |
| **Hoogte**<br/><br/> minOccurs = '0' |**xs:int** | |
| **Kwaliteit**<br/><br/> minOccurs = '0' |**xs:int** |Geldige waarden: 1(worst)-100(best) |

### <a name="attributes"></a>Kenmerken
| Naam | Type | Beschrijving |
| --- | --- | --- |
| **Voorwaarde** |**xs:String** | |

## <a name="PngLayers"></a>PngLayers
### <a name="elements"></a>Elementen
| Naam | Type | Beschrijving |
| --- | --- | --- |
| **PngLayer**<br/><br/> minOccurs = "0" maxOccurs = 'unbounded' |[PngLayer](media-services-mes-schema.md#PngLayer) | |

## <a name="BmpLayers"></a>BmpLayers
### <a name="elements"></a>Elementen
| Naam | Type | Beschrijving |
| --- | --- | --- |
| **BmpLayer**<br/><br/> minOccurs = "0" maxOccurs = 'unbounded' |[BmpLayer](media-services-mes-schema.md#BmpLayer) | |

## <a name="JpgLayers"></a>JpgLayers
### <a name="elements"></a>Elementen
| Naam | Type | Beschrijving |
| --- | --- | --- |
| **JpgLayer**<br/><br/> minOccurs = "0" maxOccurs = 'unbounded' |[JpgLayer](media-services-mes-schema.md#JpgLayer) | |

## <a name="BmpImage"></a>BmpImage (complex type overneemt van de Video)
### <a name="elements"></a>Elementen
| Naam | Type | Beschrijving |
| --- | --- | --- |
| **PngLayers**<br/><br/> minOccurs = '0' |[PngLayers](media-services-mes-schema.md#PngLayers) |PNG-lagen |

## <a name="JpgImage"></a>JpgImage (complex type overneemt van de Video)
### <a name="elements"></a>Elementen
| Naam | Type | Beschrijving |
| --- | --- | --- |
| **PngLayers**<br/><br/> minOccurs = '0' |[PngLayers](media-services-mes-schema.md#PngLayers) |PNG-lagen |

## <a name="PngImage"></a>PngImage (complex type overneemt van de Video)
### <a name="elements"></a>Elementen
| Naam | Type | Beschrijving |
| --- | --- | --- |
| **PngLayers**<br/><br/> minOccurs = '0' |[PngLayers](media-services-mes-schema.md#PngLayers) |PNG-lagen |

## <a name="examples"></a>Voorbeelden
Zie voorbeelden van XML-standaardinstellingen die zijn gebouwd op basis van dit schema, Zie [taak standaardinstellingen voor MES (Media Encoder Standard)](media-services-mes-presets-overview.md).

## <a name="next-steps"></a>Volgende stappen
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Feedback geven
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]


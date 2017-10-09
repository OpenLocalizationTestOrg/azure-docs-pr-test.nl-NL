---
title: aaaMultiple invoer bestanden en eigenschappen van onderdeel met Premium-Encoder - Azure | Microsoft Docs
description: In dit onderwerp wordt uitgelegd hoe toouse setRuntimeProperties toouse invoer van meerdere bestanden en aangepaste gegevens toohello Media Encoder Premium media werkstroomverwerking doorgeven.
services: media-services
documentationcenter: 
author: xpouyat
manager: cfowler
editor: 
ms.assetid: 7fb35bdd-9891-4401-a65b-ef3cc8190e8a
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: xpouyat;anilmur;juliako
ms.openlocfilehash: e14d10fbf9669e0b88e5ba1c519f1ba5e0bafdd4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="using-multiple-input-files-and-component-properties-with-premium-encoder"></a>Gebruik van meerdere invoerbestanden en eigenschappen van onderdeel met Premium-codering
## <a name="overview"></a>Overzicht
Er zijn scenario's waarin u eigenschappen toocustomize moet Clip lijst XML-inhoud opgeven of meerdere invoerbestanden verzenden wanneer u een taak met Hallo indienen **Media Encoder Premium werkstroom** Mediaprocessor. Een aantal voorbeelden:

* Tekst keer op video en het instellen van tekstwaarde hello (bijvoorbeeld hello vandaag) tijdens runtime voor elke invoervideo.
* Aanpassing van Hallo Clip lijst XML (toospecify een of meer, met of bronbestanden zonder bijsnijden, enz.).
* Een installatiekopie van het logo keer op Hallo invoervideo terwijl Hallo video is gecodeerd.
* Meerdere audio taalcode.

Hallo toolet **Media Encoder Premium werkstroom** weten dat u enkele eigenschappen in de werkstroom Hallo wijzigt wanneer u meerdere invoerbestanden verzenden of Hallo taak maakt, hebt u toouse een configuratietekenreeks met  **setRuntimeProperties** en/of **transcodeSource**. Dit onderwerp wordt uitgelegd hoe toouse ze.

## <a name="configuration-string-syntax"></a>De syntaxis van configuratie
Hallo configuratie tekenreeks tooset in Hallo codering taak maakt gebruik van een XML-document ziet:

```xml
<?xml version="1.0" encoding="utf-8"?>
<transcodeRequest>
  <transcodeSource>
  </transcodeSource>
  <setRuntimeProperties>
    <property propertyPath="Media File Input/filename" value="VideoFileName.mp4" />
  </setRuntimeProperties>
</transcodeRequest>
```

Hallo volgt Hallo C#-code die Hallo XML-configuratie van een bestand wordt gelezen, werk deze bij met Hallo rechts video filename en geeft deze toohello taak in een taak:

```c#
string premiumConfiguration = ReadAllText(@"D:\home\site\wwwroot\Presets\SetRuntime.xml").Replace("VideoFileName", myVideoFileName);

// Declare a new job.
IJob job = _context.Jobs.Create("Premium Workflow encoding job");

// Get a media processor reference, and pass tooit hello name of hello 
// processor toouse for hello specific task.
IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Premium Workflow");

// Create a task with hello encoding details, using a string preset.
ITask task = job.Tasks.AddNew("Premium Workflow encoding task",
                              processor,
                              premiumConfiguration,
                              TaskOptions.None);

// Specify hello input assets
task.InputAssets.Add(workflow); // workflow asset
task.InputAssets.Add(video); // video asset with multiple files

// Add an output asset toocontain hello results of hello job. 
// This output is specified as AssetCreationOptions.None, which 
// means hello output asset is not encrypted. 
task.OutputAssets.AddNew("Output asset", AssetCreationOptions.None);
```

## <a name="customizing-component-properties"></a>Eigenschappen van onderdeel aanpassen
### <a name="property-with-a-simple-value"></a>Eigenschap met een eenvoudige waarde
In sommige gevallen is het nuttig toocustomize eigenschap van een onderdeel samen met de Hallo-bestand voor werkstroom die wordt uitgevoerd door de werkstroom voor Media Encoder Premium toobe.

Stel dat u een werkstroom die tekst overlays op opgezet uw video's en tekst hello (bijvoorbeeld Hallo vandaag) moet toobe set tijdens runtime. U kunt dit doen door te sturen Hallo tekst toobe ingesteld als Hallo nieuwe waarde voor de teksteigenschap Hallo van Hallo overlay onderdeel van Hallo taak codering. Kunt u dit mechanisme toochange andere eigenschappen van een onderdeel in de werkstroom hello (zoals Hallo positie of de kleur van de overlay hello, Hallo bitrate van Hallo AVC-codering, enzovoort).

**setRuntimeProperties** gebruikte toooverride is een eigenschap in Hallo onderdelen van Hallo-werkstroom.

Voorbeeld:

```xml
<?xml version="1.0" encoding="utf-8"?>
  <transcodeRequest>
    <setRuntimeProperties>
      <property propertyPath="Media File Input/filename" value="MyInputVideo.mp4" />
      <property propertyPath="/primarySourceFile" value="MyInputVideo.mp4" />
      <property propertyPath="Optional Text Overlay/Text tooImage Converter/text" value="Today is Friday hello 13th of May, 2016"/>
  </setRuntimeProperties>
</transcodeRequest>
```

### <a name="property-with-an-xml-value"></a>Eigenschap met een XML-waarde
een eigenschap die een XML-waarde verwacht tooset inkapselen met behulp van `<![CDATA[ and ]]>`.

Voorbeeld:

```xml
<?xml version="1.0" encoding="utf-8"?>
  <transcodeRequest>
    <setRuntimeProperties>
      <property propertyPath="/primarySourceFile" value="start.mxf" />
      <property propertyPath="/inactiveTimeout" value="65" />
      <property propertyPath="clipListXml" value="xxx">
      <extendedValue><![CDATA[<clipList>
        <clip>
          <videoSource>
            <mediaFile>
              <file>start.mxf</file>
            </mediaFile>
          </videoSource>
          <audioSource>
            <mediaFile>
              <file>start.mxf</file>
            </mediaFile>
          </audioSource>
        </clip>
        <primaryClipIndex>0</primaryClipIndex>
        </clipList>]]>
      </extendedValue>
      </property>
      <property propertyPath="Media File Input Logo/filename" value="logo.png" />
    </setRuntimeProperties>
  </transcodeRequest>
```

> [!NOTE]
> Zorg ervoor dat geen tooput een regeleinde retourneren vlak na `<![CDATA[`.

### <a name="propertypath-value"></a>propertyPath-waarde
In de voorgaande voorbeelden hello, Hallo propertyPath is ' / Media File invoer/bestandsnaam ' of ' / inactiveTimeout ' of 'clipListXml'.
Dit kan in het algemeen is Hallo-naam van het Hallo-onderdeel en vervolgens Hallo-naam van Hallo-eigenschap. Hello pad kan hebben meer of minder niveaus, zoals ' / primarySourceFile ' (omdat het Hallo-eigenschap is in de hoofdmap Hallo van Hallo werkstroom) of ' / Video-Overlay verwerking/afbeelding/dekking ' (omdat Hallo Overlay bevindt zich in een groep).    

toocheck hello pad en de eigenschap name, gebruik Hallo actieknop die direct naast elke eigenschap. U kunt op deze actieknop en selecteer **bewerken**. Hier ziet u Hallo werkelijke naam van de eigenschap Hallo en onmiddellijk erboven, Hallo naamruimte.

![Actie/bewerken](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture6_actionedit.png)

![Eigenschap](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture7_viewproperty.png)

## <a name="multiple-input-files"></a>Meerdere invoerbestanden
Elke taak dient u toohello **Media Encoder Premium werkstroom** vereist twee elementen:

* Hallo eerst een is een *werkstroom Asset* die een werkstroombestand bevat. U kunt Werkstroombestanden ontwerpen met behulp van Hallo [Workflow Designer](media-services-workflow-designer.md).
* Hallo tweede is een *Media Asset* die Hallo media-bestanden die u wilt dat tooencode bevat.

Wanneer u meerdere media-bestanden toohello verzendt **Media Encoder Premium werkstroom** encoder Hallo volgen beperkingen toepassen:

* Alle Hallo media bestanden moeten zich in dezelfde Hallo *Media Asset*. Gebruik van meerdere elementen van de Media wordt niet ondersteund.
* Moet u het primaire bestand Hallo instellen in deze Asset Media (in het ideale geval dit Hallo is video hoofdbestand die Hallo encoder tooprocess gevraagd).
* Het benodigde toopass configuratiegegevens met Hallo is **setRuntimeProperties** en/of **transcodeSource** element toohello processor.
  * **setRuntimeProperties** is gebruikte toooverride Hallo filename eigenschap of een andere eigenschap Hallo-onderdelen van Hallo-werkstroom.
  * **transcodeSource** gebruikte toospecify Hallo Clip lijst XML-inhoud is.

De verbindingen in Hallo werkstroom:

* Als u een of meer onderdelen van Media bestandsinvoer gebruiken en toouse plannen **setRuntimeProperties** toospecify Hallo bestandsnaam en klik vervolgens Hallo primaire bestand onderdeel pincode toothem niet verbinden. Zorg ervoor dat er geen verbinding tussen de primaire bestandsobject Hallo en Hallo Media bestand Input(s).
* Als u liever toouse Clip lijst XML en een mediabron onderdeel, kunt klikt u vervolgens u beide samen.

![Er is geen verbinding van de primaire bronbestand tooMedia bestandsinvoer](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture0_nopin.png)

*Er is geen verbinding van Hallo primaire bestand tooMedia bestandsinvoer onderdelen als u setRuntimeProperties tooset Hallo filename eigenschap gebruikt.*

![Verbinding van XML-Clip lijst tooClip lijst bron](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture1_pincliplist.png)

*U kunt verbinding maken met XML-Clip lijst tooMedia bron en transcodeSource gebruiken.*

### <a name="clip-list-xml-customization"></a>Lijst met XML-aanpassing bijsnijden
U kunt Hallo Clip lijst XML in Hallo werkstroom tijdens runtime opgeven met behulp van **transcodeSource** in Hallo configuratie string XML. Dit is vereist Hallo Clip lijst XML pincode toobe verbonden toohello mediabron in Hallo-werkstroom.

```xml
<?xml version="1.0" encoding="utf-16"?>
  <transcodeRequest>
    <transcodeSource>
      <clipList>
        <clip>
          <videoSource>
            <mediaFile>
              <file>video-part1.mp4</file>
            </mediaFile>
          </videoSource>
          <audioSource>
            <mediaFile>
              <file>video-part1.mp4</file>
            </mediaFile>
          </audioSource>
        </clip>
        <primaryClipIndex>0</primaryClipIndex>
      </clipList>
    </transcodeSource>
    <setRuntimeProperties>
      <property propertyPath="Media File Input Logo/filename" value="logo.png" />
    </setRuntimeProperties>
  </transcodeRequest>
```

Als u wilt dat toospecify /primarySourceFile toouse deze eigenschap tooname Hallo uitvoer bestanden met behulp van 'Expressies', wordt aangeraden Hallo Clip lijst XML wordt doorgegeven als een eigenschap *nadat* hello /primarySourceFile eigenschap, tooavoid Hallo met worden Clip lijst overschreven door Hallo /primarySourceFile instelling.

```xml
<?xml version="1.0" encoding="utf-8"?>
  <transcodeRequest>
    <setRuntimeProperties>
      <property propertyPath="/primarySourceFile" value="c:\temp\start.mxf" />
      <property propertyPath="/inactiveTimeout" value="65" />
      <property propertyPath="clipListXml" value="xxx">
      <extendedValue><![CDATA[<clipList>
        <clip>
          <videoSource>
            <mediaFile>
              <file>c:\temp\start.mxf</file>
            </mediaFile>
          </videoSource>
          <audioSource>
            <mediaFile>
              <file>c:\temp\start.mxf</file>
            </mediaFile>
          </audioSource>
        </clip>
        <primaryClipIndex>0</primaryClipIndex>
        </clipList>]]>
      </extendedValue>
      </property>
      <property propertyPath="Media File Input Logo/filename" value="logo.png" />
    </setRuntimeProperties>
  </transcodeRequest>
```

Met extra nauwkeurige frame opmaak:

```xml
<?xml version="1.0" encoding="utf-8"?>
  <transcodeRequest>
    <setRuntimeProperties>
      <property propertyPath="/primarySourceFile" value="start.mxf" />
      <property propertyPath="/inactiveTimeout" value="65" />
      <property propertyPath="clipListXml" value="xxx">
      <extendedValue><![CDATA[<clipList>
        <clip>
          <videoSource>
            <trim>
              <inPoint fps="25">00:00:05:24</inPoint>
              <outPoint fps="25">00:00:10:24</outPoint>
            </trim>
            <mediaFile>
              <file>start.mxf</file>
            </mediaFile>
          </videoSource>
          <audioSource>
            <trim>
              <inPoint fps="25">00:00:05:24</inPoint>
              <outPoint fps="25">00:00:10:24</outPoint>
            </trim>
            <mediaFile>
              <file>start.mxf</file>
            </mediaFile>
          </audioSource>
        </clip>
        <primaryClipIndex>0</primaryClipIndex>
        </clipList>]]>
      </extendedValue>
      </property>
      <property propertyPath="Media File Input Logo/filename" value="logo.png" />
    </setRuntimeProperties>
  </transcodeRequest>
```

## <a name="example-1--overlay-an-image-on-top-of-hello-video"></a>Voorbeeld 1: Een afbeelding die boven op Hallo video Overlay

### <a name="presentation"></a>Presentatie
U kunt een voorbeeld waarin u toooverlay wilt een installatiekopie van het logo op Hallo invoervideo terwijl Hallo video is gecodeerd. In dit voorbeeld Hallo invoervideo heet 'Microsoft_HoloLens_Possibilities_816p24.mp4' en Hallo logo heet 'logo.png'. U moet uitvoeren Hallo stappen te volgen:

* Maak een werkstroom activa met Hallo werkstroombestand (Zie het volgende voorbeeld Hallo).
* Maken van een activum Media, waarin twee bestanden: MyInputVideo.mp4 zoals Hallo primaire bestands- en MyLogo.png.
* Een taak toohello Media Encoder Premium werkstroom media-processor met bovenstaande Hallo invoer activa verzenden en geef Hallo configuratietekenreeks te volgen.

Configuratie:

```xml
<?xml version="1.0" encoding="utf-16"?>
  <transcodeRequest>
    <setRuntimeProperties>
      <property propertyPath="Media File Input/filename" value="Microsoft_HoloLens_Possibilities_816p24.mp4" />
      <property propertyPath="/primarySourceFile" value="Microsoft_HoloLens_Possibilities_816p24.mp4" />
      <property propertyPath="Media File Input Logo/filename" value="logo.png" />
    </setRuntimeProperties>
  </transcodeRequest>
```

Hallo bovenstaande voorbeeld Hallo-naam van de videobestand Hallo toohello Media bestandsinvoer onderdeel en Hallo primarySourceFile eigenschap verzonden. Hallo-naam van Hallo logobestand verzonden tooanother Media bestanden invoeren die is verbonden toohello grafische overlay onderdeel.

> [!NOTE]
> Hallo video bestandsnaam toohello primarySourceFile eigenschap verzonden. Hallo reden hiervoor is toouse deze eigenschap in de werkstroom voor het bouwen van Hallo juiste naam van het uitvoerbestand met behulp van expressies, bijvoorbeeld Hallo.

### <a name="step-by-step-workflow-creation"></a>Stapsgewijze werkstroom is gemaakt
Hier vindt u Hallo stappen toocreate een werkstroom die twee bestanden als invoer neemt: een video- en een installatiekopie. Deze wordt installatiekopie Hallo boven op Hallo video overlay.

Open **Workflow Designer** en selecteer **bestand** > **nieuwe werkruimte** > **transcoderen blauwdruk**.

de nieuwe werkstroom Hallo ziet u drie elementen:

* Primaire bronbestand
* Clip XML-lijst
* Uitvoerasset bestand  

![Nieuwe codering werkstroom](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture9_empty.png)

*Nieuwe codering werkstroom*

Begin met het toevoegen van een Media bestand invoer onderdeel in volgorde tooaccept Hallo invoer mediabestand. tooadd een onderdeel toohello werkstroom, zoekt in het zoekvak Hallo-opslagplaats en sleep Hallo gewenst vermelding op Hallo designer deelvenster.

Voeg vervolgens Hallo videobestand toobe gebruikt voor het ontwerpen van uw werkstroom. toodo dus klikt u op Hallo achtergrond deelvenster in de werkstroomontwerper en te bekijken voor Hallo primaire bronbestand-eigenschap op Hallo eigenschap rechter deelvenster. Klik op Hallo mappictogram en selecteer de juiste videobestand Hallo.

![Primaire bestandsbron](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture10_primaryfile.png)

*Primaire bestandsbron*

Geef vervolgens Hallo videobestand in Hallo Media bestandsinvoer-component.   

![Mediabestand invoerbron](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture11_mediafileinput.png)

*Mediabestand invoerbron*

Zodra dit is gebeurd, wordt de Hallo Media bestandsinvoer onderdeel Hallo bestand controleren en de vullen van de bijbehorende pincodes tooreflect Hallo uitvoerbestand dat wordt gecontroleerd.

de volgende stap Hallo is een 'Video gegevens Type Updater' toospecify Hallo kleur ruimte tooRec.709 tooadd. Toevoegen van een 'Video Format Converter' dat is ingesteld tooData lay-out/indelingstype = configureerbare platte. Dit Hallo videostream tooa indeling die kan worden uitgevoerd als een bron van Hallo overlay onderdeel geconverteerd.

![video gegevens Type Updater en Format Converter](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture12_formatconverter.png)

*Video-Data Type Updater en Format Converter*

![Indelingstype configureerbare platte =](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture12_formatconverter2.png)

*Indelingstype is configureerbaar platte*

Vervolgens een Video-Overlay-component toevoegen en verbinding maken met de Hallo (niet-gecomprimeerde) video pincode toohello (niet-gecomprimeerde) video pincode van Hallo media bestandsinvoer.

Toevoegen van een andere Media bestand-invoer (tooload Hallo logo-bestand), klik op dit onderdeel en wijzig de naam ervan te 'Media bestand invoer Logo' en selecteer een installatiekopie (bijvoorbeeld een PNG-bestand) in de eigenschap Hallo-bestand. Verbinding maken met Hallo niet-gecomprimeerde installatiekopie pincode toohello niet-gecomprimeerde installatiekopie pincode van Hallo overlay.

![Bron voor overlay onderdeel en de installatiekopie van bestand](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture13_overlay.png)

*Bron voor overlay onderdeel en de installatiekopie van bestand*

Als u wilt dat toomodify Hallo positie van Hallo logo op Hallo video (u kunt bijvoorbeeld tooposition op 10 procent op Hallo boven linkerbovenhoek van Hallo video) Schakel Hallo 'Handmatige invoer' selectievakje. U kunt dit doen omdat u een Media bestandsinvoer tooprovide Hallo logo bestand toohello overlay-component.

![Positie van de overlay](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture14_overlay_position.png)

*Positie van de overlay*

tooencode Hallo videostream tooH.264, Hallo AVC Video Encoder en AAC encoder onderdelen toohello ontwerpoppervlak toevoegen. Verbinding maken met Hallo pincodes.
Hallo AAC encoder instellen en selecteer Audio-indeling conversie/definitie: 2.0 (L, R).

![Audio en Video coderingsprogramma 's](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture15_encoders.png)

*Audio en Video coderingsprogramma 's*

Voeg nu Hallo **ISO Mpeg-4 Multiplexer** en **uitvoer in een bestand** onderdelen en sluit Hallo pincodes, zoals wordt weergegeven.

![Multiplexer MP4- en uitvoer in een bestand](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture16_mp4output.png)

*Multiplexer MP4- en uitvoer in een bestand*

U moet tooset Hallo naam op voor het Hallo-uitvoerbestand. Klik op Hallo **uitvoer in een bestand** onderdeel en bewerken Hallo-expressie voor het Hallo-bestand:

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_withoverlay.mp4

![Bestandsnaam voor uitvoer](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture17_filenameoutput.png)

*Bestandsnaam voor uitvoer*

U kunt Hallo werkstroom uitvoeren lokaal toocheck dat deze correct wordt uitgevoerd.

Nadat deze is voltooid, kunt u deze uitvoeren in Azure Media Services.

Een actief in Azure Media Services aan twee bestanden erin eerst voorbereiden: Hallo videobestand en het Hallo-logo. U kunt dit doen met behulp van Hallo .NET of REST-API. U kunt dit ook doen met behulp van hello Azure-portal of [Azure Media Services Explorer](https://github.com/Azure/Azure-Media-Services-Explorer) (AMSE).

Deze zelfstudie leert u hoe toomanage activa met AMSE. Er zijn twee manieren tooadd bestanden tooan asset:

* Maken van een lokale map, het Hallo twee bestanden kopiëren, en het slepen en neerzetten van Hallo map toohello **Asset** tabblad.
* Hallo videobestand als een asset uploaden, Hallo asset informatie weergegeven, gaat u tabblad toohello-bestanden en uploaden van een extra bestand (logo).

> [!NOTE]
> Zorg ervoor dat tooset een primair bestand Hallo actief (Hallo belangrijkste video-bestand) in.

![Assetbestanden in AMSE](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture18_assetinamse.png)

*Assetbestanden in AMSE*

Selecteer Hallo asset en kies tooencode met Premium-codering. Hallo werkstroom uploaden en selecteer deze.

Klik op Hallo knop toopass-gegevensprocessor toohello en Hallo volgende XML-tooset Hallo runtime eigenschappen toevoegen:

![Premium-codering in AMSE](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture19_amsepremium.png)

*Premium-codering in AMSE*

Plak Hallo XML-gegevens te volgen. In dat geval moet u toospecify Hallo-naam van de videobestand Hallo in voor zowel hello Media bestandsinvoer- en primarySourceFile. Hallo naam opgeven van Hallo bestandsnaam op voor het Hallo-logo te.

```xml
<?xml version="1.0" encoding="utf-16"?>
  <transcodeRequest>
    <setRuntimeProperties>
      <property propertyPath="Media File Input/filename" value="Microsoft_HoloLens_Possibilities_816p24.mp4" />
      <property propertyPath="/primarySourceFile" value="Microsoft_HoloLens_Possibilities_816p24.mp4" />
      <property propertyPath="Media File Input Logo/filename" value="logo.png" />
    </setRuntimeProperties>
  </transcodeRequest>
```

![setRuntimeProperties](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture20_amsexmldata.png)

*setRuntimeProperties*

Als u Hallo .NET SDK toocreate en Hallo-taak uitvoert, deze XML-gegevens toobe doorgegeven als de configuratietekenreeks Hallo heeft.

```c#
public ITask AddNew(string taskName, IMediaProcessor mediaProcessor, string configuration, TaskOptions options);
```

Nadat het Hallo-taak is voltooid, uitvoer Hallo MP4-bestand in Hallo asset weergegeven Hallo overlay!

![Overlay op Hallo video](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture21_resultoverlay.png)

*Overlay op Hallo video*

U kunt de voorbeeldwerkstroom Hallo van downloaden [GitHub](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows/).

## <a name="example-2--multiple-audio-language-encoding"></a>Voorbeeld 2: Meerdere audio taalcode

Een voorbeeld van meerdere audio taal codering workfkow is beschikbaar in [GitHub](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows/MultilanguageAudioEncoding).

Deze map bevat een voorbeeldwerkstroom die gebruikt tooencode een MXF bestand tooa multi MP4-bestanden activa met meerdere audio houdt worden kan.

Deze werkstroom wordt ervan uitgegaan dat Hallo MXF-bestand bevat een nummer; Hallo audio nummers moeten worden doorgegeven als afzonderlijke audio-bestanden (WAV of MP4...).

tooencode, volg dan deze stappen:

* Een Media Services-activum maken met de Hallo MXF bestands- en Hallo Audio-bestanden (0 too18 audio-bestanden).
* Zorg ervoor dat Hallo MXF-bestand is ingesteld als een primair bestand.
* Maak een taak en een taak met Hallo Premium werkstroom Encoder-processor. Hallo-werkstroom opgegeven (MultiMP4-1080p-19audio-v1.workflow) gebruiken.
* Hallo setruntime.xml data toohello taak doorgeven (als u Azure Media Services Explorer, gebruik Hallo 'geeft de XML-gegevens toohello werkstroom' knop).
  * Werk Hallo XML-gegevens toospecify Hallo juiste bestand namen en talen codes.
  * Hallo werkstroom heeft audio onderdelen met de naam Audio 1 tooAudio 18.
  * RFC5646 wordt ondersteund voor Hallo taallabel.

```xml
<?xml version="1.0" encoding="utf-16"?>
<transcodeRequest>
  <setRuntimeProperties>
    <property propertyPath="Media File Input Video/filename" value="MainVideo.mxf" />
    <property propertyPath="Language/language_code" value="en" />
    <property propertyPath="/primarySourceFile" value="MainVideo.mxf" />
    <property propertyPath="Audio 1/Media File Input/filename" value="french-audio.wav" />
    <property propertyPath="Audio 1/Language/language_code" value="fr" />
    <property propertyPath="Audio 2/Media File Input/filename" value="german-audio.wav" />
    <property propertyPath="Audio 2/Language/language_code" value="de" />
    <property propertyPath="Audio 3/Media File Input/filename" value="japanese-audio.wav" />
    <property propertyPath="Audio 3/Language/language_code" value="ja" />
  </setRuntimeProperties>
</transcodeRequest>
```

* Hallo gecodeerde asset multi taal audio-nummers en worden deze nummers moeten worden geselecteerd in Azure Media Player.

## <a name="see-also"></a>Zie ook
* [Inleiding tot Premium codering in Azure Media Services](http://azure.microsoft.com/blog/2015/03/05/introducing-premium-encoding-in-azure-media-services)
* [Hoe toouse Premium codering in Azure Media Services](http://azure.microsoft.com/blog/2015/03/06/how-to-use-premium-encoding-in-azure-media-services)
* [Codering van inhoud op aanvraag met Azure Media Services](media-services-encode-asset.md#media-encoder-premium-workflow)
* [Werkstroom voor Media Encoder Premium indelingen en codecs](media-services-premium-workflow-encoder-formats.md)
* [Werkstroom voorbeeldbestanden](https://github.com/AzureMediaServicesSamples/Encoding-Presets/tree/master/VoD/MediaEncoderPremiumWorkfows)
* [Azure Media Services Explorer-hulpprogramma](http://aka.ms/amse)

## <a name="media-services-learning-paths"></a>Media Services-leertrajecten
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Feedback geven
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

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
# <a name="using-multiple-input-files-and-component-properties-with-premium-encoder"></a><span data-ttu-id="74ae3-103">Gebruik van meerdere invoerbestanden en eigenschappen van onderdeel met Premium-codering</span><span class="sxs-lookup"><span data-stu-id="74ae3-103">Using multiple input files and component properties with Premium Encoder</span></span>
## <a name="overview"></a><span data-ttu-id="74ae3-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="74ae3-104">Overview</span></span>
<span data-ttu-id="74ae3-105">Er zijn scenario's waarin u eigenschappen toocustomize moet Clip lijst XML-inhoud opgeven of meerdere invoerbestanden verzenden wanneer u een taak met Hallo indienen **Media Encoder Premium werkstroom** Mediaprocessor.</span><span class="sxs-lookup"><span data-stu-id="74ae3-105">There are scenarios in which you might need toocustomize component properties, specify Clip List XML content, or send multiple input files when you submit a task with hello **Media Encoder Premium Workflow** media processor.</span></span> <span data-ttu-id="74ae3-106">Een aantal voorbeelden:</span><span class="sxs-lookup"><span data-stu-id="74ae3-106">Some examples are:</span></span>

* <span data-ttu-id="74ae3-107">Tekst keer op video en het instellen van tekstwaarde hello (bijvoorbeeld hello vandaag) tijdens runtime voor elke invoervideo.</span><span class="sxs-lookup"><span data-stu-id="74ae3-107">Overlaying text on video and setting hello text value (for example, hello current date) at runtime for each input video.</span></span>
* <span data-ttu-id="74ae3-108">Aanpassing van Hallo Clip lijst XML (toospecify een of meer, met of bronbestanden zonder bijsnijden, enz.).</span><span class="sxs-lookup"><span data-stu-id="74ae3-108">Customizing hello Clip List XML (toospecify one or several source files, with or without trimming, etc.).</span></span>
* <span data-ttu-id="74ae3-109">Een installatiekopie van het logo keer op Hallo invoervideo terwijl Hallo video is gecodeerd.</span><span class="sxs-lookup"><span data-stu-id="74ae3-109">Overlaying a logo image on hello input video while hello video is encoded.</span></span>
* <span data-ttu-id="74ae3-110">Meerdere audio taalcode.</span><span class="sxs-lookup"><span data-stu-id="74ae3-110">Multiple audio language encoding.</span></span>

<span data-ttu-id="74ae3-111">Hallo toolet **Media Encoder Premium werkstroom** weten dat u enkele eigenschappen in de werkstroom Hallo wijzigt wanneer u meerdere invoerbestanden verzenden of Hallo taak maakt, hebt u toouse een configuratietekenreeks met  **setRuntimeProperties** en/of **transcodeSource**.</span><span class="sxs-lookup"><span data-stu-id="74ae3-111">toolet hello **Media Encoder Premium Workflow** know that you are changing some properties in hello workflow when you create hello task or send multiple input files, you have toouse a configuration string that contains **setRuntimeProperties** and/or **transcodeSource**.</span></span> <span data-ttu-id="74ae3-112">Dit onderwerp wordt uitgelegd hoe toouse ze.</span><span class="sxs-lookup"><span data-stu-id="74ae3-112">This topic explains how toouse them.</span></span>

## <a name="configuration-string-syntax"></a><span data-ttu-id="74ae3-113">De syntaxis van configuratie</span><span class="sxs-lookup"><span data-stu-id="74ae3-113">Configuration string syntax</span></span>
<span data-ttu-id="74ae3-114">Hallo configuratie tekenreeks tooset in Hallo codering taak maakt gebruik van een XML-document ziet:</span><span class="sxs-lookup"><span data-stu-id="74ae3-114">hello configuration string tooset in hello encoding task uses an XML document that looks like this:</span></span>

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

<span data-ttu-id="74ae3-115">Hallo volgt Hallo C#-code die Hallo XML-configuratie van een bestand wordt gelezen, werk deze bij met Hallo rechts video filename en geeft deze toohello taak in een taak:</span><span class="sxs-lookup"><span data-stu-id="74ae3-115">hello following is hello C# code that reads hello XML configuration from a file, update it with hello right video filename and passes it toohello task in a job:</span></span>

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

## <a name="customizing-component-properties"></a><span data-ttu-id="74ae3-116">Eigenschappen van onderdeel aanpassen</span><span class="sxs-lookup"><span data-stu-id="74ae3-116">Customizing component properties</span></span>
### <a name="property-with-a-simple-value"></a><span data-ttu-id="74ae3-117">Eigenschap met een eenvoudige waarde</span><span class="sxs-lookup"><span data-stu-id="74ae3-117">Property with a simple value</span></span>
<span data-ttu-id="74ae3-118">In sommige gevallen is het nuttig toocustomize eigenschap van een onderdeel samen met de Hallo-bestand voor werkstroom die wordt uitgevoerd door de werkstroom voor Media Encoder Premium toobe.</span><span class="sxs-lookup"><span data-stu-id="74ae3-118">In some cases, it is useful toocustomize a component property together with hello workflow file that is going toobe executed by Media Encoder Premium Workflow.</span></span>

<span data-ttu-id="74ae3-119">Stel dat u een werkstroom die tekst overlays op opgezet uw video's en tekst hello (bijvoorbeeld Hallo vandaag) moet toobe set tijdens runtime.</span><span class="sxs-lookup"><span data-stu-id="74ae3-119">Suppose you designed a workflow that overlays text on your videos, and hello text (for example, hello current date) is supposed toobe set at runtime.</span></span> <span data-ttu-id="74ae3-120">U kunt dit doen door te sturen Hallo tekst toobe ingesteld als Hallo nieuwe waarde voor de teksteigenschap Hallo van Hallo overlay onderdeel van Hallo taak codering.</span><span class="sxs-lookup"><span data-stu-id="74ae3-120">You can do this by sending hello text toobe set as hello new value for hello text property of hello overlay component from hello encoding task.</span></span> <span data-ttu-id="74ae3-121">Kunt u dit mechanisme toochange andere eigenschappen van een onderdeel in de werkstroom hello (zoals Hallo positie of de kleur van de overlay hello, Hallo bitrate van Hallo AVC-codering, enzovoort).</span><span class="sxs-lookup"><span data-stu-id="74ae3-121">You can use this mechanism toochange other properties of a component in hello workflow (such as hello position or color of hello overlay, hello bitrate of hello AVC encoder, etc.).</span></span>

<span data-ttu-id="74ae3-122">**setRuntimeProperties** gebruikte toooverride is een eigenschap in Hallo onderdelen van Hallo-werkstroom.</span><span class="sxs-lookup"><span data-stu-id="74ae3-122">**setRuntimeProperties** is used toooverride a property in hello components of hello workflow.</span></span>

<span data-ttu-id="74ae3-123">Voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="74ae3-123">Example:</span></span>

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

### <a name="property-with-an-xml-value"></a><span data-ttu-id="74ae3-124">Eigenschap met een XML-waarde</span><span class="sxs-lookup"><span data-stu-id="74ae3-124">Property with an XML value</span></span>
<span data-ttu-id="74ae3-125">een eigenschap die een XML-waarde verwacht tooset inkapselen met behulp van `<![CDATA[ and ]]>`.</span><span class="sxs-lookup"><span data-stu-id="74ae3-125">tooset a property that expects an XML value, encapsulate by using `<![CDATA[ and ]]>`.</span></span>

<span data-ttu-id="74ae3-126">Voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="74ae3-126">Example:</span></span>

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
> <span data-ttu-id="74ae3-127">Zorg ervoor dat geen tooput een regeleinde retourneren vlak na `<![CDATA[`.</span><span class="sxs-lookup"><span data-stu-id="74ae3-127">Make sure not tooput a carriage return just after `<![CDATA[`.</span></span>

### <a name="propertypath-value"></a><span data-ttu-id="74ae3-128">propertyPath-waarde</span><span class="sxs-lookup"><span data-stu-id="74ae3-128">propertyPath value</span></span>
<span data-ttu-id="74ae3-129">In de voorgaande voorbeelden hello, Hallo propertyPath is ' / Media File invoer/bestandsnaam ' of ' / inactiveTimeout ' of 'clipListXml'.</span><span class="sxs-lookup"><span data-stu-id="74ae3-129">In hello previous examples, hello propertyPath was "/Media File Input/filename" or "/inactiveTimeout" or "clipListXml".</span></span>
<span data-ttu-id="74ae3-130">Dit kan in het algemeen is Hallo-naam van het Hallo-onderdeel en vervolgens Hallo-naam van Hallo-eigenschap.</span><span class="sxs-lookup"><span data-stu-id="74ae3-130">This is, in general, hello name of hello component, then hello name of hello property.</span></span> <span data-ttu-id="74ae3-131">Hello pad kan hebben meer of minder niveaus, zoals ' / primarySourceFile ' (omdat het Hallo-eigenschap is in de hoofdmap Hallo van Hallo werkstroom) of ' / Video-Overlay verwerking/afbeelding/dekking ' (omdat Hallo Overlay bevindt zich in een groep).</span><span class="sxs-lookup"><span data-stu-id="74ae3-131">hello path can have more or fewer levels, like "/primarySourceFile" (because hello property is at hello root of hello workflow) or "/Video Processing/Graphic Overlay/Opacity" (because hello Overlay is in a group).</span></span>    

<span data-ttu-id="74ae3-132">toocheck hello pad en de eigenschap name, gebruik Hallo actieknop die direct naast elke eigenschap.</span><span class="sxs-lookup"><span data-stu-id="74ae3-132">toocheck hello path and property name, use hello action button that is immediately beside each property.</span></span> <span data-ttu-id="74ae3-133">U kunt op deze actieknop en selecteer **bewerken**.</span><span class="sxs-lookup"><span data-stu-id="74ae3-133">You can click this action button and select **Edit**.</span></span> <span data-ttu-id="74ae3-134">Hier ziet u Hallo werkelijke naam van de eigenschap Hallo en onmiddellijk erboven, Hallo naamruimte.</span><span class="sxs-lookup"><span data-stu-id="74ae3-134">This will show you hello actual name of hello property, and immediately above it, hello namespace.</span></span>

![Actie/bewerken](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture6_actionedit.png)

![Eigenschap](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture7_viewproperty.png)

## <a name="multiple-input-files"></a><span data-ttu-id="74ae3-137">Meerdere invoerbestanden</span><span class="sxs-lookup"><span data-stu-id="74ae3-137">Multiple input files</span></span>
<span data-ttu-id="74ae3-138">Elke taak dient u toohello **Media Encoder Premium werkstroom** vereist twee elementen:</span><span class="sxs-lookup"><span data-stu-id="74ae3-138">Each task that you submit toohello **Media Encoder Premium Workflow** requires two assets:</span></span>

* <span data-ttu-id="74ae3-139">Hallo eerst een is een *werkstroom Asset* die een werkstroombestand bevat.</span><span class="sxs-lookup"><span data-stu-id="74ae3-139">hello first one is a *Workflow Asset* that contains a workflow file.</span></span> <span data-ttu-id="74ae3-140">U kunt Werkstroombestanden ontwerpen met behulp van Hallo [Workflow Designer](media-services-workflow-designer.md).</span><span class="sxs-lookup"><span data-stu-id="74ae3-140">You can design workflow files by using hello [Workflow Designer](media-services-workflow-designer.md).</span></span>
* <span data-ttu-id="74ae3-141">Hallo tweede is een *Media Asset* die Hallo media-bestanden die u wilt dat tooencode bevat.</span><span class="sxs-lookup"><span data-stu-id="74ae3-141">hello second one is a *Media Asset* that contains hello media file(s) that you want tooencode.</span></span>

<span data-ttu-id="74ae3-142">Wanneer u meerdere media-bestanden toohello verzendt **Media Encoder Premium werkstroom** encoder Hallo volgen beperkingen toepassen:</span><span class="sxs-lookup"><span data-stu-id="74ae3-142">When you're sending multiple media files toohello **Media Encoder Premium Workflow** encoder, hello following constraints apply:</span></span>

* <span data-ttu-id="74ae3-143">Alle Hallo media bestanden moeten zich in dezelfde Hallo *Media Asset*.</span><span class="sxs-lookup"><span data-stu-id="74ae3-143">All hello media files must be in hello same *Media Asset*.</span></span> <span data-ttu-id="74ae3-144">Gebruik van meerdere elementen van de Media wordt niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="74ae3-144">Using multiple Media Assets is not supported.</span></span>
* <span data-ttu-id="74ae3-145">Moet u het primaire bestand Hallo instellen in deze Asset Media (in het ideale geval dit Hallo is video hoofdbestand die Hallo encoder tooprocess gevraagd).</span><span class="sxs-lookup"><span data-stu-id="74ae3-145">You must set hello primary file in this Media Asset (ideally, this is hello main video file that hello encoder is asked tooprocess).</span></span>
* <span data-ttu-id="74ae3-146">Het benodigde toopass configuratiegegevens met Hallo is **setRuntimeProperties** en/of **transcodeSource** element toohello processor.</span><span class="sxs-lookup"><span data-stu-id="74ae3-146">It is necessary toopass configuration data that includes hello **setRuntimeProperties** and/or **transcodeSource** element toohello processor.</span></span>
  * <span data-ttu-id="74ae3-147">**setRuntimeProperties** is gebruikte toooverride Hallo filename eigenschap of een andere eigenschap Hallo-onderdelen van Hallo-werkstroom.</span><span class="sxs-lookup"><span data-stu-id="74ae3-147">**setRuntimeProperties** is used toooverride hello filename property or another property in hello components of hello workflow.</span></span>
  * <span data-ttu-id="74ae3-148">**transcodeSource** gebruikte toospecify Hallo Clip lijst XML-inhoud is.</span><span class="sxs-lookup"><span data-stu-id="74ae3-148">**transcodeSource** is used toospecify hello Clip List XML content.</span></span>

<span data-ttu-id="74ae3-149">De verbindingen in Hallo werkstroom:</span><span class="sxs-lookup"><span data-stu-id="74ae3-149">Connections in hello workflow:</span></span>

* <span data-ttu-id="74ae3-150">Als u een of meer onderdelen van Media bestandsinvoer gebruiken en toouse plannen **setRuntimeProperties** toospecify Hallo bestandsnaam en klik vervolgens Hallo primaire bestand onderdeel pincode toothem niet verbinden.</span><span class="sxs-lookup"><span data-stu-id="74ae3-150">If you use one or several Media File Input components and plan toouse **setRuntimeProperties** toospecify hello file name, then do not connect hello primary file component pin toothem.</span></span> <span data-ttu-id="74ae3-151">Zorg ervoor dat er geen verbinding tussen de primaire bestandsobject Hallo en Hallo Media bestand Input(s).</span><span class="sxs-lookup"><span data-stu-id="74ae3-151">Make sure that there is no connection between hello primary file object and hello Media File Input(s).</span></span>
* <span data-ttu-id="74ae3-152">Als u liever toouse Clip lijst XML en een mediabron onderdeel, kunt klikt u vervolgens u beide samen.</span><span class="sxs-lookup"><span data-stu-id="74ae3-152">If you prefer toouse Clip List XML and one Media Source component, then you can connect both together.</span></span>

![Er is geen verbinding van de primaire bronbestand tooMedia bestandsinvoer](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture0_nopin.png)

<span data-ttu-id="74ae3-154">*Er is geen verbinding van Hallo primaire bestand tooMedia bestandsinvoer onderdelen als u setRuntimeProperties tooset Hallo filename eigenschap gebruikt.*</span><span class="sxs-lookup"><span data-stu-id="74ae3-154">*There is no connection from hello primary file tooMedia File Input component(s) if you use setRuntimeProperties tooset hello filename property.*</span></span>

![Verbinding van XML-Clip lijst tooClip lijst bron](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture1_pincliplist.png)

<span data-ttu-id="74ae3-156">*U kunt verbinding maken met XML-Clip lijst tooMedia bron en transcodeSource gebruiken.*</span><span class="sxs-lookup"><span data-stu-id="74ae3-156">*You can connect Clip List XML tooMedia Source and use transcodeSource.*</span></span>

### <a name="clip-list-xml-customization"></a><span data-ttu-id="74ae3-157">Lijst met XML-aanpassing bijsnijden</span><span class="sxs-lookup"><span data-stu-id="74ae3-157">Clip List XML customization</span></span>
<span data-ttu-id="74ae3-158">U kunt Hallo Clip lijst XML in Hallo werkstroom tijdens runtime opgeven met behulp van **transcodeSource** in Hallo configuratie string XML.</span><span class="sxs-lookup"><span data-stu-id="74ae3-158">You can specify hello Clip List XML in hello workflow at runtime by using **transcodeSource** in hello configuration string XML.</span></span> <span data-ttu-id="74ae3-159">Dit is vereist Hallo Clip lijst XML pincode toobe verbonden toohello mediabron in Hallo-werkstroom.</span><span class="sxs-lookup"><span data-stu-id="74ae3-159">This requires hello Clip List XML pin toobe connected toohello Media Source component in hello workflow.</span></span>

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

<span data-ttu-id="74ae3-160">Als u wilt dat toospecify /primarySourceFile toouse deze eigenschap tooname Hallo uitvoer bestanden met behulp van 'Expressies', wordt aangeraden Hallo Clip lijst XML wordt doorgegeven als een eigenschap *nadat* hello /primarySourceFile eigenschap, tooavoid Hallo met worden Clip lijst overschreven door Hallo /primarySourceFile instelling.</span><span class="sxs-lookup"><span data-stu-id="74ae3-160">If you want toospecify /primarySourceFile toouse this property tooname hello output files by using 'Expressions', then we recommend passing hello Clip List XML as a property *after* hello /primarySourceFile property, tooavoid having hello Clip List be overridden by hello /primarySourceFile setting.</span></span>

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

<span data-ttu-id="74ae3-161">Met extra nauwkeurige frame opmaak:</span><span class="sxs-lookup"><span data-stu-id="74ae3-161">With additional frame-accurate trimming:</span></span>

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

## <a name="example-1--overlay-an-image-on-top-of-hello-video"></a><span data-ttu-id="74ae3-162">Voorbeeld 1: Een afbeelding die boven op Hallo video Overlay</span><span class="sxs-lookup"><span data-stu-id="74ae3-162">Example 1 : Overlay an image on top of hello video</span></span>

### <a name="presentation"></a><span data-ttu-id="74ae3-163">Presentatie</span><span class="sxs-lookup"><span data-stu-id="74ae3-163">Presentation</span></span>
<span data-ttu-id="74ae3-164">U kunt een voorbeeld waarin u toooverlay wilt een installatiekopie van het logo op Hallo invoervideo terwijl Hallo video is gecodeerd.</span><span class="sxs-lookup"><span data-stu-id="74ae3-164">Consider an example in which you want toooverlay a logo image on hello input video while hello video is encoded.</span></span> <span data-ttu-id="74ae3-165">In dit voorbeeld Hallo invoervideo heet 'Microsoft_HoloLens_Possibilities_816p24.mp4' en Hallo logo heet 'logo.png'.</span><span class="sxs-lookup"><span data-stu-id="74ae3-165">In this example, hello input video is named "Microsoft_HoloLens_Possibilities_816p24.mp4" and hello logo is named "logo.png".</span></span> <span data-ttu-id="74ae3-166">U moet uitvoeren Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="74ae3-166">You should perform hello following steps:</span></span>

* <span data-ttu-id="74ae3-167">Maak een werkstroom activa met Hallo werkstroombestand (Zie het volgende voorbeeld Hallo).</span><span class="sxs-lookup"><span data-stu-id="74ae3-167">Create a Workflow Asset with hello workflow file (see hello following example).</span></span>
* <span data-ttu-id="74ae3-168">Maken van een activum Media, waarin twee bestanden: MyInputVideo.mp4 zoals Hallo primaire bestands- en MyLogo.png.</span><span class="sxs-lookup"><span data-stu-id="74ae3-168">Create a Media Asset, which contains two files: MyInputVideo.mp4 as hello primary file and MyLogo.png.</span></span>
* <span data-ttu-id="74ae3-169">Een taak toohello Media Encoder Premium werkstroom media-processor met bovenstaande Hallo invoer activa verzenden en geef Hallo configuratietekenreeks te volgen.</span><span class="sxs-lookup"><span data-stu-id="74ae3-169">Send a task toohello Media Encoder Premium Workflow media processor with hello above input assets and specify hello following configuration string.</span></span>

<span data-ttu-id="74ae3-170">Configuratie:</span><span class="sxs-lookup"><span data-stu-id="74ae3-170">Configuration:</span></span>

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

<span data-ttu-id="74ae3-171">Hallo bovenstaande voorbeeld Hallo-naam van de videobestand Hallo toohello Media bestandsinvoer onderdeel en Hallo primarySourceFile eigenschap verzonden.</span><span class="sxs-lookup"><span data-stu-id="74ae3-171">In hello example above, hello name of hello video file is sent toohello Media File Input component and hello primarySourceFile property.</span></span> <span data-ttu-id="74ae3-172">Hallo-naam van Hallo logobestand verzonden tooanother Media bestanden invoeren die is verbonden toohello grafische overlay onderdeel.</span><span class="sxs-lookup"><span data-stu-id="74ae3-172">hello name of hello logo file is sent tooanother Media File Input that is connected toohello graphic overlay component.</span></span>

> [!NOTE]
> <span data-ttu-id="74ae3-173">Hallo video bestandsnaam toohello primarySourceFile eigenschap verzonden.</span><span class="sxs-lookup"><span data-stu-id="74ae3-173">hello video file name is sent toohello primarySourceFile property.</span></span> <span data-ttu-id="74ae3-174">Hallo reden hiervoor is toouse deze eigenschap in de werkstroom voor het bouwen van Hallo juiste naam van het uitvoerbestand met behulp van expressies, bijvoorbeeld Hallo.</span><span class="sxs-lookup"><span data-stu-id="74ae3-174">hello reason for this is toouse this property in hello workflow for building hello correct output file name using Expressions, for example.</span></span>

### <a name="step-by-step-workflow-creation"></a><span data-ttu-id="74ae3-175">Stapsgewijze werkstroom is gemaakt</span><span class="sxs-lookup"><span data-stu-id="74ae3-175">Step-by-step workflow creation</span></span>
<span data-ttu-id="74ae3-176">Hier vindt u Hallo stappen toocreate een werkstroom die twee bestanden als invoer neemt: een video- en een installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="74ae3-176">Here are hello steps toocreate a workflow that takes two files as input: a video and an image.</span></span> <span data-ttu-id="74ae3-177">Deze wordt installatiekopie Hallo boven op Hallo video overlay.</span><span class="sxs-lookup"><span data-stu-id="74ae3-177">It will overlay hello image on top of hello video.</span></span>

<span data-ttu-id="74ae3-178">Open **Workflow Designer** en selecteer **bestand** > **nieuwe werkruimte** > **transcoderen blauwdruk**.</span><span class="sxs-lookup"><span data-stu-id="74ae3-178">Open **Workflow Designer** and select **File** > **New Workspace** > **Transcode Blueprint**.</span></span>

<span data-ttu-id="74ae3-179">de nieuwe werkstroom Hallo ziet u drie elementen:</span><span class="sxs-lookup"><span data-stu-id="74ae3-179">hello new workflow shows three elements:</span></span>

* <span data-ttu-id="74ae3-180">Primaire bronbestand</span><span class="sxs-lookup"><span data-stu-id="74ae3-180">Primary Source File</span></span>
* <span data-ttu-id="74ae3-181">Clip XML-lijst</span><span class="sxs-lookup"><span data-stu-id="74ae3-181">Clip List XML</span></span>
* <span data-ttu-id="74ae3-182">Uitvoerasset bestand</span><span class="sxs-lookup"><span data-stu-id="74ae3-182">Output File/Asset</span></span>  

![Nieuwe codering werkstroom](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture9_empty.png)

<span data-ttu-id="74ae3-184">*Nieuwe codering werkstroom*</span><span class="sxs-lookup"><span data-stu-id="74ae3-184">*New Encoding Workflow*</span></span>

<span data-ttu-id="74ae3-185">Begin met het toevoegen van een Media bestand invoer onderdeel in volgorde tooaccept Hallo invoer mediabestand.</span><span class="sxs-lookup"><span data-stu-id="74ae3-185">In order tooaccept hello input media file, start with adding a Media File Input component.</span></span> <span data-ttu-id="74ae3-186">tooadd een onderdeel toohello werkstroom, zoekt in het zoekvak Hallo-opslagplaats en sleep Hallo gewenst vermelding op Hallo designer deelvenster.</span><span class="sxs-lookup"><span data-stu-id="74ae3-186">tooadd a component toohello workflow, look for it in hello Repository search box and drag hello desired entry onto hello designer pane.</span></span>

<span data-ttu-id="74ae3-187">Voeg vervolgens Hallo videobestand toobe gebruikt voor het ontwerpen van uw werkstroom.</span><span class="sxs-lookup"><span data-stu-id="74ae3-187">Next, add hello video file toobe used for designing your workflow.</span></span> <span data-ttu-id="74ae3-188">toodo dus klikt u op Hallo achtergrond deelvenster in de werkstroomontwerper en te bekijken voor Hallo primaire bronbestand-eigenschap op Hallo eigenschap rechter deelvenster.</span><span class="sxs-lookup"><span data-stu-id="74ae3-188">toodo so, click hello background pane in Workflow Designer and look for hello Primary Source File property on hello right-hand property pane.</span></span> <span data-ttu-id="74ae3-189">Klik op Hallo mappictogram en selecteer de juiste videobestand Hallo.</span><span class="sxs-lookup"><span data-stu-id="74ae3-189">Click hello folder icon and select hello appropriate video file.</span></span>

![Primaire bestandsbron](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture10_primaryfile.png)

<span data-ttu-id="74ae3-191">*Primaire bestandsbron*</span><span class="sxs-lookup"><span data-stu-id="74ae3-191">*Primary File Source*</span></span>

<span data-ttu-id="74ae3-192">Geef vervolgens Hallo videobestand in Hallo Media bestandsinvoer-component.</span><span class="sxs-lookup"><span data-stu-id="74ae3-192">Next, specify hello video file in hello Media File Input component.</span></span>   

![Mediabestand invoerbron](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture11_mediafileinput.png)

<span data-ttu-id="74ae3-194">*Mediabestand invoerbron*</span><span class="sxs-lookup"><span data-stu-id="74ae3-194">*Media File Input Source*</span></span>

<span data-ttu-id="74ae3-195">Zodra dit is gebeurd, wordt de Hallo Media bestandsinvoer onderdeel Hallo bestand controleren en de vullen van de bijbehorende pincodes tooreflect Hallo uitvoerbestand dat wordt gecontroleerd.</span><span class="sxs-lookup"><span data-stu-id="74ae3-195">As soon as this is done, hello Media File Input component will inspect hello file and populate its output pins tooreflect hello file that it inspected.</span></span>

<span data-ttu-id="74ae3-196">de volgende stap Hallo is een 'Video gegevens Type Updater' toospecify Hallo kleur ruimte tooRec.709 tooadd.</span><span class="sxs-lookup"><span data-stu-id="74ae3-196">hello next step is tooadd a "Video Data Type Updater" toospecify hello color space tooRec.709.</span></span> <span data-ttu-id="74ae3-197">Toevoegen van een 'Video Format Converter' dat is ingesteld tooData lay-out/indelingstype = configureerbare platte.</span><span class="sxs-lookup"><span data-stu-id="74ae3-197">Add a "Video Format Converter" that is set tooData Layout/Layout type = Configurable Planar.</span></span> <span data-ttu-id="74ae3-198">Dit Hallo videostream tooa indeling die kan worden uitgevoerd als een bron van Hallo overlay onderdeel geconverteerd.</span><span class="sxs-lookup"><span data-stu-id="74ae3-198">This will convert hello video stream tooa format that can be taken as a source of hello overlay component.</span></span>

![video gegevens Type Updater en Format Converter](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture12_formatconverter.png)

<span data-ttu-id="74ae3-200">*Video-Data Type Updater en Format Converter*</span><span class="sxs-lookup"><span data-stu-id="74ae3-200">*Video Data Type Updater and Format Converter*</span></span>

![Indelingstype configureerbare platte =](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture12_formatconverter2.png)

<span data-ttu-id="74ae3-202">*Indelingstype is configureerbaar platte*</span><span class="sxs-lookup"><span data-stu-id="74ae3-202">*Layout type is Configurable Planar*</span></span>

<span data-ttu-id="74ae3-203">Vervolgens een Video-Overlay-component toevoegen en verbinding maken met de Hallo (niet-gecomprimeerde) video pincode toohello (niet-gecomprimeerde) video pincode van Hallo media bestandsinvoer.</span><span class="sxs-lookup"><span data-stu-id="74ae3-203">Next, add a Video Overlay component and connect hello (uncompressed) video pin toohello (uncompressed) video pin of hello media file input.</span></span>

<span data-ttu-id="74ae3-204">Toevoegen van een andere Media bestand-invoer (tooload Hallo logo-bestand), klik op dit onderdeel en wijzig de naam ervan te 'Media bestand invoer Logo' en selecteer een installatiekopie (bijvoorbeeld een PNG-bestand) in de eigenschap Hallo-bestand.</span><span class="sxs-lookup"><span data-stu-id="74ae3-204">Add another Media File Input (tooload hello logo file), click on this component and rename it too"Media File Input Logo", and select an image (a .png file for example) in hello file property.</span></span> <span data-ttu-id="74ae3-205">Verbinding maken met Hallo niet-gecomprimeerde installatiekopie pincode toohello niet-gecomprimeerde installatiekopie pincode van Hallo overlay.</span><span class="sxs-lookup"><span data-stu-id="74ae3-205">Connect hello Uncompressed image pin toohello Uncompressed image pin of hello overlay.</span></span>

![Bron voor overlay onderdeel en de installatiekopie van bestand](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture13_overlay.png)

<span data-ttu-id="74ae3-207">*Bron voor overlay onderdeel en de installatiekopie van bestand*</span><span class="sxs-lookup"><span data-stu-id="74ae3-207">*Overlay component and image file source*</span></span>

<span data-ttu-id="74ae3-208">Als u wilt dat toomodify Hallo positie van Hallo logo op Hallo video (u kunt bijvoorbeeld tooposition op 10 procent op Hallo boven linkerbovenhoek van Hallo video) Schakel Hallo 'Handmatige invoer' selectievakje.</span><span class="sxs-lookup"><span data-stu-id="74ae3-208">If you want toomodify hello position of hello logo on hello video (for example, you might want tooposition it at 10 percent off of hello top left corner of hello video), clear hello "Manual Input" check box.</span></span> <span data-ttu-id="74ae3-209">U kunt dit doen omdat u een Media bestandsinvoer tooprovide Hallo logo bestand toohello overlay-component.</span><span class="sxs-lookup"><span data-stu-id="74ae3-209">You can do this because you are using a Media File Input tooprovide hello logo file toohello overlay component.</span></span>

![Positie van de overlay](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture14_overlay_position.png)

<span data-ttu-id="74ae3-211">*Positie van de overlay*</span><span class="sxs-lookup"><span data-stu-id="74ae3-211">*Overlay position*</span></span>

<span data-ttu-id="74ae3-212">tooencode Hallo videostream tooH.264, Hallo AVC Video Encoder en AAC encoder onderdelen toohello ontwerpoppervlak toevoegen.</span><span class="sxs-lookup"><span data-stu-id="74ae3-212">tooencode hello video stream tooH.264, add hello AVC Video Encoder and AAC encoder components toohello designer surface.</span></span> <span data-ttu-id="74ae3-213">Verbinding maken met Hallo pincodes.</span><span class="sxs-lookup"><span data-stu-id="74ae3-213">Connect hello pins.</span></span>
<span data-ttu-id="74ae3-214">Hallo AAC encoder instellen en selecteer Audio-indeling conversie/definitie: 2.0 (L, R).</span><span class="sxs-lookup"><span data-stu-id="74ae3-214">Set up hello AAC encoder and select Audio Format Conversion/Preset : 2.0 (L, R).</span></span>

![Audio en Video coderingsprogramma 's](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture15_encoders.png)

<span data-ttu-id="74ae3-216">*Audio en Video coderingsprogramma 's*</span><span class="sxs-lookup"><span data-stu-id="74ae3-216">*Audio and Video Encoders*</span></span>

<span data-ttu-id="74ae3-217">Voeg nu Hallo **ISO Mpeg-4 Multiplexer** en **uitvoer in een bestand** onderdelen en sluit Hallo pincodes, zoals wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="74ae3-217">Now add hello **ISO Mpeg-4 Multiplexer** and **File Output** components and connect hello pins as shown.</span></span>

![Multiplexer MP4- en uitvoer in een bestand](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture16_mp4output.png)

<span data-ttu-id="74ae3-219">*Multiplexer MP4- en uitvoer in een bestand*</span><span class="sxs-lookup"><span data-stu-id="74ae3-219">*MP4 multiplexer and file output*</span></span>

<span data-ttu-id="74ae3-220">U moet tooset Hallo naam op voor het Hallo-uitvoerbestand.</span><span class="sxs-lookup"><span data-stu-id="74ae3-220">You need tooset hello name for hello output file.</span></span> <span data-ttu-id="74ae3-221">Klik op Hallo **uitvoer in een bestand** onderdeel en bewerken Hallo-expressie voor het Hallo-bestand:</span><span class="sxs-lookup"><span data-stu-id="74ae3-221">Click hello **File Output** component and edit hello expression for hello file:</span></span>

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_withoverlay.mp4

![Bestandsnaam voor uitvoer](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture17_filenameoutput.png)

<span data-ttu-id="74ae3-223">*Bestandsnaam voor uitvoer*</span><span class="sxs-lookup"><span data-stu-id="74ae3-223">*File output name*</span></span>

<span data-ttu-id="74ae3-224">U kunt Hallo werkstroom uitvoeren lokaal toocheck dat deze correct wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="74ae3-224">You can run hello workflow locally toocheck that it is running correctly.</span></span>

<span data-ttu-id="74ae3-225">Nadat deze is voltooid, kunt u deze uitvoeren in Azure Media Services.</span><span class="sxs-lookup"><span data-stu-id="74ae3-225">After it finishes, you can run it in Azure Media Services.</span></span>

<span data-ttu-id="74ae3-226">Een actief in Azure Media Services aan twee bestanden erin eerst voorbereiden: Hallo videobestand en het Hallo-logo.</span><span class="sxs-lookup"><span data-stu-id="74ae3-226">First, prepare an asset in Azure Media Services with two files in it: hello video file and hello logo.</span></span> <span data-ttu-id="74ae3-227">U kunt dit doen met behulp van Hallo .NET of REST-API.</span><span class="sxs-lookup"><span data-stu-id="74ae3-227">You can do this by using hello .NET or REST API.</span></span> <span data-ttu-id="74ae3-228">U kunt dit ook doen met behulp van hello Azure-portal of [Azure Media Services Explorer](https://github.com/Azure/Azure-Media-Services-Explorer) (AMSE).</span><span class="sxs-lookup"><span data-stu-id="74ae3-228">You can also do this by using hello Azure portal or [Azure Media Services Explorer](https://github.com/Azure/Azure-Media-Services-Explorer) (AMSE).</span></span>

<span data-ttu-id="74ae3-229">Deze zelfstudie leert u hoe toomanage activa met AMSE.</span><span class="sxs-lookup"><span data-stu-id="74ae3-229">This tutorial shows you how toomanage assets with AMSE.</span></span> <span data-ttu-id="74ae3-230">Er zijn twee manieren tooadd bestanden tooan asset:</span><span class="sxs-lookup"><span data-stu-id="74ae3-230">There are two ways tooadd files tooan asset:</span></span>

* <span data-ttu-id="74ae3-231">Maken van een lokale map, het Hallo twee bestanden kopiëren, en het slepen en neerzetten van Hallo map toohello **Asset** tabblad.</span><span class="sxs-lookup"><span data-stu-id="74ae3-231">Create a local folder, copy hello two files in it, and drag and drop hello folder toohello **Asset** tab.</span></span>
* <span data-ttu-id="74ae3-232">Hallo videobestand als een asset uploaden, Hallo asset informatie weergegeven, gaat u tabblad toohello-bestanden en uploaden van een extra bestand (logo).</span><span class="sxs-lookup"><span data-stu-id="74ae3-232">Upload hello video file as an asset, display hello asset information, go toohello files tab, and upload an additional file (logo).</span></span>

> [!NOTE]
> <span data-ttu-id="74ae3-233">Zorg ervoor dat tooset een primair bestand Hallo actief (Hallo belangrijkste video-bestand) in.</span><span class="sxs-lookup"><span data-stu-id="74ae3-233">Make sure tooset a primary file in hello asset (hello main video file).</span></span>

![Assetbestanden in AMSE](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture18_assetinamse.png)

<span data-ttu-id="74ae3-235">*Assetbestanden in AMSE*</span><span class="sxs-lookup"><span data-stu-id="74ae3-235">*Asset files in AMSE*</span></span>

<span data-ttu-id="74ae3-236">Selecteer Hallo asset en kies tooencode met Premium-codering.</span><span class="sxs-lookup"><span data-stu-id="74ae3-236">Select hello asset and choose tooencode it with Premium Encoder.</span></span> <span data-ttu-id="74ae3-237">Hallo werkstroom uploaden en selecteer deze.</span><span class="sxs-lookup"><span data-stu-id="74ae3-237">Upload hello workflow and select it.</span></span>

<span data-ttu-id="74ae3-238">Klik op Hallo knop toopass-gegevensprocessor toohello en Hallo volgende XML-tooset Hallo runtime eigenschappen toevoegen:</span><span class="sxs-lookup"><span data-stu-id="74ae3-238">Click hello button toopass data toohello processor, and add hello following XML tooset hello runtime properties:</span></span>

![Premium-codering in AMSE](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture19_amsepremium.png)

<span data-ttu-id="74ae3-240">*Premium-codering in AMSE*</span><span class="sxs-lookup"><span data-stu-id="74ae3-240">*Premium Encoder in AMSE*</span></span>

<span data-ttu-id="74ae3-241">Plak Hallo XML-gegevens te volgen.</span><span class="sxs-lookup"><span data-stu-id="74ae3-241">Then, paste hello following XML data.</span></span> <span data-ttu-id="74ae3-242">In dat geval moet u toospecify Hallo-naam van de videobestand Hallo in voor zowel hello Media bestandsinvoer- en primarySourceFile.</span><span class="sxs-lookup"><span data-stu-id="74ae3-242">You need toospecify hello name of hello video file for both hello Media File Input and primarySourceFile.</span></span> <span data-ttu-id="74ae3-243">Hallo naam opgeven van Hallo bestandsnaam op voor het Hallo-logo te.</span><span class="sxs-lookup"><span data-stu-id="74ae3-243">Specify hello name of hello file name for hello logo too.</span></span>

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

<span data-ttu-id="74ae3-245">*setRuntimeProperties*</span><span class="sxs-lookup"><span data-stu-id="74ae3-245">*setRuntimeProperties*</span></span>

<span data-ttu-id="74ae3-246">Als u Hallo .NET SDK toocreate en Hallo-taak uitvoert, deze XML-gegevens toobe doorgegeven als de configuratietekenreeks Hallo heeft.</span><span class="sxs-lookup"><span data-stu-id="74ae3-246">If you use hello .NET SDK toocreate and run hello task, this XML data has toobe passed as hello configuration string.</span></span>

```c#
public ITask AddNew(string taskName, IMediaProcessor mediaProcessor, string configuration, TaskOptions options);
```

<span data-ttu-id="74ae3-247">Nadat het Hallo-taak is voltooid, uitvoer Hallo MP4-bestand in Hallo asset weergegeven Hallo overlay!</span><span class="sxs-lookup"><span data-stu-id="74ae3-247">After hello job is complete, hello MP4 file in hello output asset displays hello overlay!</span></span>

![Overlay op Hallo video](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture21_resultoverlay.png)

<span data-ttu-id="74ae3-249">*Overlay op Hallo video*</span><span class="sxs-lookup"><span data-stu-id="74ae3-249">*Overlay on hello video*</span></span>

<span data-ttu-id="74ae3-250">U kunt de voorbeeldwerkstroom Hallo van downloaden [GitHub](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows/).</span><span class="sxs-lookup"><span data-stu-id="74ae3-250">You can download hello sample workflow from [GitHub](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows/).</span></span>

## <a name="example-2--multiple-audio-language-encoding"></a><span data-ttu-id="74ae3-251">Voorbeeld 2: Meerdere audio taalcode</span><span class="sxs-lookup"><span data-stu-id="74ae3-251">Example 2 : Multiple audio language encoding</span></span>

<span data-ttu-id="74ae3-252">Een voorbeeld van meerdere audio taal codering workfkow is beschikbaar in [GitHub](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows/MultilanguageAudioEncoding).</span><span class="sxs-lookup"><span data-stu-id="74ae3-252">An example of multiple audio language encoding workfkow is available in [GitHub](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows/MultilanguageAudioEncoding).</span></span>

<span data-ttu-id="74ae3-253">Deze map bevat een voorbeeldwerkstroom die gebruikt tooencode een MXF bestand tooa multi MP4-bestanden activa met meerdere audio houdt worden kan.</span><span class="sxs-lookup"><span data-stu-id="74ae3-253">This folder contains a sample workflow which can be used tooencode a MXF file tooa multi MP4 files asset with multiple audio tracks.</span></span>

<span data-ttu-id="74ae3-254">Deze werkstroom wordt ervan uitgegaan dat Hallo MXF-bestand bevat een nummer; Hallo audio nummers moeten worden doorgegeven als afzonderlijke audio-bestanden (WAV of MP4...).</span><span class="sxs-lookup"><span data-stu-id="74ae3-254">This workflow assumes that hello MXF file contains one audio track ; hello additional audio tracks should be passed as seperate audio files (WAV or MP4...).</span></span>

<span data-ttu-id="74ae3-255">tooencode, volg dan deze stappen:</span><span class="sxs-lookup"><span data-stu-id="74ae3-255">tooencode, please follow these steps:</span></span>

* <span data-ttu-id="74ae3-256">Een Media Services-activum maken met de Hallo MXF bestands- en Hallo Audio-bestanden (0 too18 audio-bestanden).</span><span class="sxs-lookup"><span data-stu-id="74ae3-256">Create a Media Services asset with hello MXF file and hello Audio files (0 too18 audio files).</span></span>
* <span data-ttu-id="74ae3-257">Zorg ervoor dat Hallo MXF-bestand is ingesteld als een primair bestand.</span><span class="sxs-lookup"><span data-stu-id="74ae3-257">Make sure that hello MXF file is set as a primary file.</span></span>
* <span data-ttu-id="74ae3-258">Maak een taak en een taak met Hallo Premium werkstroom Encoder-processor.</span><span class="sxs-lookup"><span data-stu-id="74ae3-258">Create a job and a task using hello Premium Workflow Encoder processor.</span></span> <span data-ttu-id="74ae3-259">Hallo-werkstroom opgegeven (MultiMP4-1080p-19audio-v1.workflow) gebruiken.</span><span class="sxs-lookup"><span data-stu-id="74ae3-259">Use hello workflow provided (MultiMP4-1080p-19audio-v1.workflow).</span></span>
* <span data-ttu-id="74ae3-260">Hallo setruntime.xml data toohello taak doorgeven (als u Azure Media Services Explorer, gebruik Hallo 'geeft de XML-gegevens toohello werkstroom' knop).</span><span class="sxs-lookup"><span data-stu-id="74ae3-260">Pass hello setruntime.xml data toohello task (if you use Azure Media Services Explorer, use hello “pass xml data toohello workflow” button).</span></span>
  * <span data-ttu-id="74ae3-261">Werk Hallo XML-gegevens toospecify Hallo juiste bestand namen en talen codes.</span><span class="sxs-lookup"><span data-stu-id="74ae3-261">Please update hello XML data toospecify hello correct file names and languages tags.</span></span>
  * <span data-ttu-id="74ae3-262">Hallo werkstroom heeft audio onderdelen met de naam Audio 1 tooAudio 18.</span><span class="sxs-lookup"><span data-stu-id="74ae3-262">hello workflow has audio components named Audio 1 tooAudio 18.</span></span>
  * <span data-ttu-id="74ae3-263">RFC5646 wordt ondersteund voor Hallo taallabel.</span><span class="sxs-lookup"><span data-stu-id="74ae3-263">RFC5646 is supported for hello language tag.</span></span>

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

* <span data-ttu-id="74ae3-264">Hallo gecodeerde asset multi taal audio-nummers en worden deze nummers moeten worden geselecteerd in Azure Media Player.</span><span class="sxs-lookup"><span data-stu-id="74ae3-264">hello encoded asset will contain multi language audio tracks and these tracks should be selectable in Azure Media Player.</span></span>

## <a name="see-also"></a><span data-ttu-id="74ae3-265">Zie ook</span><span class="sxs-lookup"><span data-stu-id="74ae3-265">See also</span></span>
* [<span data-ttu-id="74ae3-266">Inleiding tot Premium codering in Azure Media Services</span><span class="sxs-lookup"><span data-stu-id="74ae3-266">Introducing Premium Encoding in Azure Media Services</span></span>](http://azure.microsoft.com/blog/2015/03/05/introducing-premium-encoding-in-azure-media-services)
* [<span data-ttu-id="74ae3-267">Hoe toouse Premium codering in Azure Media Services</span><span class="sxs-lookup"><span data-stu-id="74ae3-267">How toouse Premium Encoding in Azure Media Services</span></span>](http://azure.microsoft.com/blog/2015/03/06/how-to-use-premium-encoding-in-azure-media-services)
* [<span data-ttu-id="74ae3-268">Codering van inhoud op aanvraag met Azure Media Services</span><span class="sxs-lookup"><span data-stu-id="74ae3-268">Encoding on-demand content with Azure Media Services</span></span>](media-services-encode-asset.md#media-encoder-premium-workflow)
* [<span data-ttu-id="74ae3-269">Werkstroom voor Media Encoder Premium indelingen en codecs</span><span class="sxs-lookup"><span data-stu-id="74ae3-269">Media Encoder Premium Workflow formats and codecs</span></span>](media-services-premium-workflow-encoder-formats.md)
* [<span data-ttu-id="74ae3-270">Werkstroom voorbeeldbestanden</span><span class="sxs-lookup"><span data-stu-id="74ae3-270">Sample workflow files</span></span>](https://github.com/AzureMediaServicesSamples/Encoding-Presets/tree/master/VoD/MediaEncoderPremiumWorkfows)
* [<span data-ttu-id="74ae3-271">Azure Media Services Explorer-hulpprogramma</span><span class="sxs-lookup"><span data-stu-id="74ae3-271">Azure Media Services Explorer tool</span></span>](http://aka.ms/amse)

## <a name="media-services-learning-paths"></a><span data-ttu-id="74ae3-272">Media Services-leertrajecten</span><span class="sxs-lookup"><span data-stu-id="74ae3-272">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="74ae3-273">Feedback geven</span><span class="sxs-lookup"><span data-stu-id="74ae3-273">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

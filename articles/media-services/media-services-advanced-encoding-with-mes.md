---
title: aaaPerform geavanceerde codering door aan te passen MES standaardinstellingen | Microsoft Docs
description: Dit onderwerp leest hoe tooperform geavanceerde codering met Media Encoder Standard standaardinstellingen van de taak aanpassen.
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 2a4ade25-e600-4bce-a66e-e29cf4a38369
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/01/2017
ms.author: juliako
ms.openlocfilehash: 9caa68fafacaf51f91f0554c5bafe491928d8c77
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="perform-advanced-encoding-by-customizing-mes-presets"></a>Uitvoeren van geavanceerde codering door aan te passen MES standaardinstellingen 

## <a name="overview"></a>Overzicht

Dit onderwerp leest hoe Media Encoder Standard toocustomize voorinstellingen. Hallo [codering met Media Encoder Standard met behulp van aangepaste standaardinstellingen](media-services-custom-mes-presets-with-dotnet.md) onderwerp wordt beschreven hoe toouse .NET toocreate een codering van de taak en een taak die met deze taak wordt uitgevoerd. Wanneer u een vooraf ingestelde levering Hallo aangepaste standaardinstellingen toohello codering taak aanpassen. 

>[!NOTE]
>Als een XML-definitie, moet u ervoor dat toopreserve Hallo volgorde van elementen, zoals wordt weergegeven in de XML-voorbeelden hieronder (bijvoorbeeld KeyFrameInterval moet worden voorafgegaan door een SceneChangeDetection).
>

In dit onderwerp worden de Hallo aangepaste standaardinstellingen die Hallo na codering taken uitvoeren gedemonstreerd.

## <a name="support-for-relative-sizes"></a>Ondersteuning voor relatieve grootten

Bij het genereren van miniaturen, hoeft u niet tooalways Geef uitvoer breedte en hoogte in pixels. U kunt opgeven in percentages in Hallo bereik [% 1,..., 100%].

### <a name="json-preset"></a>JSON-definitie
    "Width": "100%",
    "Height": "100%"

### <a name="xml-preset"></a>XML-definitie
    <Width>100%</Width>
    <Height>100%</Height>

## <a id="thumbnails"></a>Genereren van miniaturen

Deze sectie wordt beschreven hoe toocustomize een voorinstelling die miniaturen genereert. Hallo bevat voorinstelling zoals hieronder gedefinieerd, informatie over hoe u wilt dat tooencode uw bestand evenals informatie nodig toogenerate miniatuurweergaven. U kunt een van de Hallo MES standaardinstellingen beschreven nemen [dit](media-services-mes-presets-overview.md) sectie en code die wordt gegenereerd miniaturen toe te voegen.  

> [!NOTE]
> Hallo **SceneChangeDetection** -instelling in de volgende vooraf ingestelde Hallo kan alleen worden ingesteld tootrue als u tooa single-bitrate video coderen wilt. Als u tooa multi-bitrate coderen wilt video en stel **SceneChangeDetection** tootrue, Hallo codering wordt een fout geretourneerd.  
>
>

Zie voor meer informatie over schema [dit](media-services-mes-schema.md) onderwerp.

Zorg ervoor dat tooreview hello [overwegingen](#considerations) sectie.

### <a id="json"></a>JSON-definitie
    {
      "Version": 1.0,
      "Codecs": [
        {
          "KeyFrameInterval": "00:00:02",
          "SceneChangeDetection": "true",
          "H264Layers": [
            {
              "Profile": "Auto",
              "Level": "auto",
              "Bitrate": 4500,
              "MaxBitrate": 4500,
              "BufferWindow": "00:00:05",
              "Width": 1280,
              "Height": 720,
              "ReferenceFrames": 3,
              "EntropyMode": "Cabac",
              "AdaptiveBFrame": true,
              "Type": "H264Layer",
              "FrameRate": "0/1"

            }
          ],
          "Type": "H264Video"
        },
        {
          "JpgLayers": [
            {
              "Quality": 90,
              "Type": "JpgLayer",
              "Width": 640,
              "Height": 360
            }
          ],
          "Start": "{Best}",
          "Type": "JpgImage"
        },
        {
          "PngLayers": [
            {
              "Type": "PngLayer",
              "Width": 640,
              "Height": 360,
            }
          ],
          "Start": "00:00:01",
          "Step": "00:00:10",
          "Range": "00:00:58",
          "Type": "PngImage"
        },
        {
          "BmpLayers": [
            {
              "Type": "BmpLayer",
              "Width": 640,
              "Height": 360
            }
          ],
          "Start": "10%",
          "Step": "10%",
          "Range": "90%",
          "Type": "BmpImage"
        },
        {
          "Channels": 2,
          "SamplingRate": 48000,
          "Bitrate": 128,
          "Type": "AACAudio"
        }
      ],
      "Outputs": [
        {
          "FileName": "{Basename}_{Index}{Extension}",
          "Format": {
            "Type": "JpgFormat"
          }
        },
        {
          "FileName": "{Basename}_{Index}{Extension}",
          "Format": {
            "Type": "PngFormat"
          }
        },
        {
          "FileName": "{Basename}_{Index}{Extension}",
          "Format": {
            "Type": "BmpFormat"
          }
        },
        {
          "FileName": "{Basename}_{Width}x{Height}_{VideoBitrate}.mp4",
          "Format": {
            "Type": "MP4Format"
          }
        }
      ]
    }


### <a id="xml"></a>XML-definitie
    <?xml version="1.0" encoding="utf-16"?>
    <Preset xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Version="1.0" xmlns="http://www.windowsazure.com/media/encoding/Preset/2014/03">
      <Encoding>
        <H264Video>
          <KeyFrameInterval>00:00:02</KeyFrameInterval>
          <SceneChangeDetection>true</SceneChangeDetection>
          <H264Layers>
            <H264Layer>
              <Bitrate>4500</Bitrate>
              <Width>1280</Width>
              <Height>720</Height>
              <FrameRate>0/1</FrameRate>
              <Profile>Auto</Profile>
              <Level>auto</Level>
              <BFrames>3</BFrames>
              <ReferenceFrames>3</ReferenceFrames>
              <Slices>0</Slices>
              <AdaptiveBFrame>true</AdaptiveBFrame>
              <EntropyMode>Cabac</EntropyMode>
              <BufferWindow>00:00:05</BufferWindow>
              <MaxBitrate>4500</MaxBitrate>
            </H264Layer>
          </H264Layers>
        </H264Video>
        <AACAudio>
          <Profile>AACLC</Profile>
          <Channels>2</Channels>
          <SamplingRate>48000</SamplingRate>
          <Bitrate>128</Bitrate>
        </AACAudio>
        <JpgImage Start="{Best}">
          <JpgLayers>
            <JpgLayer>
              <Width>640</Width>
              <Height>360</Height>
              <Quality>90</Quality>
            </JpgLayer>
          </JpgLayers>
        </JpgImage>
        <BmpImage Start="10%" Step="10%" Range="90%">
          <BmpLayers>
            <BmpLayer>
              <Width>640</Width>
              <Height>360</Height>
            </BmpLayer>
          </BmpLayers>
        </BmpImage>
        <PngImage Start="00:00:01" Step="00:00:10" Range="00:00:58">
          <PngLayers>
            <PngLayer>
              <Width>640</Width>
              <Height>360</Height>
            </PngLayer>
          </PngLayers>
        </PngImage>
      </Encoding>
      <Outputs>
        <Output FileName="{Basename}_{Width}x{Height}_{VideoBitrate}.mp4">
          <MP4Format />
        </Output>
        <Output FileName="{Basename}_{Index}{Extension}">
          <JpgFormat />
        </Output>
        <Output FileName="{Basename}_{Index}{Extension}">
          <BmpFormat />
        </Output>
        <Output FileName="{Basename}_{Index}{Extension}">
          <PngFormat />
        </Output>
      </Outputs>
    </Preset>

### <a name="considerations"></a>Overwegingen

Hallo overwegingen volgende van toepassing:

* Hallo gebruik van expliciete tijdstempels voor stap/beginbereik wordt ervan uitgegaan dat Hallo-invoerbron is minimaal 1 minuut.
* Png-jpg/BmpImage elementen moeten worden gestart, stap en bereik tekenreekskenmerken: deze kunnen worden geïnterpreteerd als:

  * Aantal frame als ze niet-negatieve gehele getallen zijn, bijvoorbeeld 'Start': '120'
  * Duur van de relatieve toosource uitgedrukt in % voorafgegaan, bijvoorbeeld 'Start': '15% ', of
  * Tijdstempel als uitgedrukt als: mm: ss... indeling, bijvoorbeeld 'Start': ' 00: 01:00 '

    U kunt combineren en notaties als u moet overeenkomen.

    Daarnaast ondersteunt Start ook een speciale Macro: {Best}, die probeert toodetermine Hallo eerste 'interessante' frame van Hallo inhoud Opmerking: (stap en bereik worden genegeerd tijdens het starten is ingesteld, te {Best})
  * Standaardwaarden: Starten: {Best}
* De indeling van uitvoer moet expliciet worden opgegeven voor elke afbeeldingsindeling toobe: Png-Jpg/BmpFormat. Als aanwezig is, vergelijkt MES JpgVideo tooJpgFormat enzovoort. OutputFormat introduceert een nieuwe installatiekopie codec specifieke Macro: {Index}, moeten toobe aanwezig (eenmaal en slechts één keer) voor de installatiekopie-uitvoerindelingen.

## <a id="trim_video"></a>Een video (paginaknipsel) knippen
Deze sectie vertelt over het wijzigen van Hallo encoder tooclip voorinstellingen of trim Hallo invoervideo waar Hallo-invoer een zogenaamde tussentijds of op aanvraag-bestand is. Hello coderingsprogramma kan ook worden gebruikt tooclip of een asset, die is vastgelegd of van een live stream gearchiveerd trim – Hallo details voor deze zijn beschikbaar in [deze blog](https://azure.microsoft.com/blog/sub-clipping-and-live-archive-extraction-with-media-encoder-standard/).

tootrim uw video's, u een van de Hallo MES standaardinstellingen gedocumenteerd kunt nemen [dit](media-services-mes-presets-overview.md) sectie en Hallo wijzigen **bronnen** element (zoals hieronder wordt weergegeven). Hallo-waarde van StartTime moet toomatch Hallo absolute tijdstempels van Hallo invoervideo. Bijvoorbeeld, als hello eerste frame van Hallo invoervideo een tijdstempel van 12:00:10.000 heeft, wordt StartTime moet ten minste 12:00:10.000 en hoger. In Hallo onderstaand voorbeeld gaan we ervan uit dat Hallo invoervideo een eerste tijdstempel van nul heeft. **Bronnen** aan Hallo begin van de vooraf ingestelde Hallo moeten worden geplaatst.

### <a id="json"></a>JSON-definitie
    {
      "Version": 1.0,
      "Sources": [
        {
          "StartTime": "00:00:04",
          "Duration": "00:00:16"
        }
      ],
      "Codecs": [
        {
          "KeyFrameInterval": "00:00:02",
          "StretchMode": "AutoSize",
          "H264Layers": [
            {
              "Profile": "Auto",
              "Level": "auto",
              "Bitrate": 3400,
              "MaxBitrate": 3400,
              "BufferWindow": "00:00:05",
              "Width": 1280,
              "Height": 720,
              "BFrames": 3,
              "ReferenceFrames": 3,
              "AdaptiveBFrame": true,
              "Type": "H264Layer",
              "FrameRate": "0/1"
            },
            {
              "Profile": "Auto",
              "Level": "auto",
              "Bitrate": 2250,
              "MaxBitrate": 2250,
              "BufferWindow": "00:00:05",
              "Width": 960,
              "Height": 540,
              "BFrames": 3,
              "ReferenceFrames": 3,
              "AdaptiveBFrame": true,
              "Type": "H264Layer",
              "FrameRate": "0/1"
            },
            {
              "Profile": "Auto",
              "Level": "auto",
              "Bitrate": 1500,
              "MaxBitrate": 1500,
              "BufferWindow": "00:00:05",
              "Width": 960,
              "Height": 540,
              "BFrames": 3,
              "ReferenceFrames": 3,
              "AdaptiveBFrame": true,
              "Type": "H264Layer",
              "FrameRate": "0/1"
            },
            {
              "Profile": "Auto",
              "Level": "auto",
              "Bitrate": 1000,
              "MaxBitrate": 1000,
              "BufferWindow": "00:00:05",
              "Width": 640,
              "Height": 360,
              "BFrames": 3,
              "ReferenceFrames": 3,
              "AdaptiveBFrame": true,
              "Type": "H264Layer",
              "FrameRate": "0/1"
            },
            {
              "Profile": "Auto",
              "Level": "auto",
              "Bitrate": 650,
              "MaxBitrate": 650,
              "BufferWindow": "00:00:05",
              "Width": 640,
              "Height": 360,
              "BFrames": 3,
              "ReferenceFrames": 3,
              "AdaptiveBFrame": true,
              "Type": "H264Layer",
              "FrameRate": "0/1"
            },
            {
              "Profile": "Auto",
              "Level": "auto",
              "Bitrate": 400,
              "MaxBitrate": 400,
              "BufferWindow": "00:00:05",
              "Width": 320,
              "Height": 180,
              "BFrames": 3,
              "ReferenceFrames": 3,
              "AdaptiveBFrame": true,
              "Type": "H264Layer",
              "FrameRate": "0/1"
            }
          ],
          "Type": "H264Video"
        },
        {
          "Profile": "AACLC",
          "Channels": 2,
          "SamplingRate": 48000,
          "Bitrate": 128,
          "Type": "AACAudio"
        }
      ],
      "Outputs": [
        {
          "FileName": "{Basename}_{Width}x{Height}_{VideoBitrate}.mp4",
          "Format": {
            "Type": "MP4Format"
          }
        }
      ]
    }

### <a name="xml-preset"></a>XML-definitie
tootrim uw video's, u een van de Hallo MES standaardinstellingen gedocumenteerd kunt nemen [hier](media-services-mes-presets-overview.md) en Hallo wijzigen **bronnen** element (zoals hieronder wordt weergegeven).

    <?xml version="1.0" encoding="utf-16"?>
    <Preset xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Version="1.0" xmlns="http://www.windowsazure.com/media/encoding/Preset/2014/03">
      <Sources>
        <Source StartTime="PT4S" Duration="PT14S"/>
      </Sources>
      <Encoding>
        <H264Video>
          <KeyFrameInterval>00:00:02</KeyFrameInterval>
          <H264Layers>
            <H264Layer>
              <Bitrate>3400</Bitrate>
              <Width>1280</Width>
              <Height>720</Height>
              <FrameRate>0/1</FrameRate>
              <Profile>Auto</Profile>
              <Level>auto</Level>
              <BFrames>3</BFrames>
              <ReferenceFrames>3</ReferenceFrames>
              <Slices>0</Slices>
              <AdaptiveBFrame>true</AdaptiveBFrame>
              <EntropyMode>Cabac</EntropyMode>
              <BufferWindow>00:00:05</BufferWindow>
              <MaxBitrate>3400</MaxBitrate>
            </H264Layer>
            <H264Layer>
              <Bitrate>2250</Bitrate>
              <Width>960</Width>
              <Height>540</Height>
              <FrameRate>0/1</FrameRate>
              <Profile>Auto</Profile>
              <Level>auto</Level>
              <BFrames>3</BFrames>
              <ReferenceFrames>3</ReferenceFrames>
              <Slices>0</Slices>
              <AdaptiveBFrame>true</AdaptiveBFrame>
              <EntropyMode>Cabac</EntropyMode>
              <BufferWindow>00:00:05</BufferWindow>
              <MaxBitrate>2250</MaxBitrate>
            </H264Layer>
            <H264Layer>
              <Bitrate>1500</Bitrate>
              <Width>960</Width>
              <Height>540</Height>
              <FrameRate>0/1</FrameRate>
              <Profile>Auto</Profile>
              <Level>auto</Level>
              <BFrames>3</BFrames>
              <ReferenceFrames>3</ReferenceFrames>
              <Slices>0</Slices>
              <AdaptiveBFrame>true</AdaptiveBFrame>
              <EntropyMode>Cabac</EntropyMode>
              <BufferWindow>00:00:05</BufferWindow>
              <MaxBitrate>1500</MaxBitrate>
            </H264Layer>
            <H264Layer>
              <Bitrate>1000</Bitrate>
              <Width>640</Width>
              <Height>360</Height>
              <FrameRate>0/1</FrameRate>
              <Profile>Auto</Profile>
              <Level>auto</Level>
              <BFrames>3</BFrames>
              <ReferenceFrames>3</ReferenceFrames>
              <Slices>0</Slices>
              <AdaptiveBFrame>true</AdaptiveBFrame>
              <EntropyMode>Cabac</EntropyMode>
              <BufferWindow>00:00:05</BufferWindow>
              <MaxBitrate>1000</MaxBitrate>
            </H264Layer>
            <H264Layer>
              <Bitrate>650</Bitrate>
              <Width>640</Width>
              <Height>360</Height>
              <FrameRate>0/1</FrameRate>
              <Profile>Auto</Profile>
              <Level>auto</Level>
              <BFrames>3</BFrames>
              <ReferenceFrames>3</ReferenceFrames>
              <Slices>0</Slices>
              <AdaptiveBFrame>true</AdaptiveBFrame>
              <EntropyMode>Cabac</EntropyMode>
              <BufferWindow>00:00:05</BufferWindow>
              <MaxBitrate>650</MaxBitrate>
            </H264Layer>
            <H264Layer>
              <Bitrate>400</Bitrate>
              <Width>320</Width>
              <Height>180</Height>
              <FrameRate>0/1</FrameRate>
              <Profile>Auto</Profile>
              <Level>auto</Level>
              <BFrames>3</BFrames>
              <ReferenceFrames>3</ReferenceFrames>
              <Slices>0</Slices>
              <AdaptiveBFrame>true</AdaptiveBFrame>
              <EntropyMode>Cabac</EntropyMode>
              <BufferWindow>00:00:05</BufferWindow>
              <MaxBitrate>400</MaxBitrate>
            </H264Layer>
          </H264Layers>
        </H264Video>
        <AACAudio>
          <Profile>AACLC</Profile>
          <Channels>2</Channels>
          <SamplingRate>48000</SamplingRate>
          <Bitrate>128</Bitrate>
        </AACAudio>
      </Encoding>
      <Outputs>
        <Output FileName="{Basename}_{Width}x{Height}_{VideoBitrate}.mp4">
          <MP4Format />
        </Output>
      </Outputs>
    </Preset>

## <a id="overlay"></a>Maken van een overlay

Hallo Media Encoder Standard kunt u een installatiekopie op een bestaande video toooverlay. Op dit moment Hallo volgende indelingen worden ondersteund: png, jpg, gif, en bmp. Hallo is voorinstelling zoals hieronder gedefinieerd, een eenvoudige voorbeeld van een video-overlay.

Bovendien toodefining een vooraf ingestelde bestand, hebt u ook toolet Media Services weten welk bestand Hallo actief in is Hallo overlay installatiekopie en waarop het bestand is Hallo bronvideo waarop u wilt dat toooverlay Hallo afbeelding. Hallo videobestand heeft toobe hello **primaire** bestand.

Als u .NET gebruikt, voegt u twee functies toohello .NET-voorbeeld gedefinieerd in de volgende Hallo [dit](media-services-custom-mes-presets-with-dotnet.md#encoding_with_dotnet) onderwerp. Hallo **UploadMediaFilesFromFolder** functie uploadt bestanden vanuit een map (bijvoorbeeld BigBuckBunny.mp4 en Image001.png) en sets Hallo mp4-bestand toobe Hallo primaire bestand Hallo actief in. Hallo **EncodeWithOverlay** functie maakt gebruik van Hallo aangepaste vooraf ingestelde bestand dat is doorgegeven tooit (bijvoorbeeld Hallo die volgt voorinstelling) toocreate Hallo codering taak.


    static public IAsset UploadMediaFilesFromFolder(string folderPath)
    {
        IAsset asset = _context.Assets.CreateFromFolder(folderPath, AssetCreationOptions.None);
    
        foreach (var af in asset.AssetFiles)
        {
            // hello following code assumes 
            // you have an input folder with one MP4 and one overlay image file.
            if (af.Name.Contains(".mp4"))
                af.IsPrimary = true;
            else
                af.IsPrimary = false;
    
            af.Update();
        }
    
        return asset;
    }

    static public IAsset EncodeWithOverlay(IAsset assetSource, string customPresetFileName)
    {
        // Declare a new job.
        IJob job = _context.Jobs.Create("Media Encoder Standard Job");
        // Get a media processor reference, and pass tooit hello name of hello 
        // processor toouse for hello specific task.
        IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Standard");

        // Load hello XML (or JSON) from hello local file.
        string configuration = File.ReadAllText(customPresetFileName);

        // Create a task
        ITask task = job.Tasks.AddNew("Media Encoder Standard encoding task",
            processor,
            configuration,
            TaskOptions.None);

        // Specify hello input assets toobe encoded.
        // This asset contains a source file and an overlay file.
        task.InputAssets.Add(assetSource);

        // Add an output asset toocontain hello results of hello job. 
        task.OutputAssets.AddNew("Output asset",
            AssetCreationOptions.None);

        job.StateChanged += new EventHandler<JobStateChangedEventArgs>(JobStateChanged);
        job.Submit();
        job.GetExecutionProgressTask(CancellationToken.None).Wait();

        return job.OutputMediaAssets[0];
    }


> [!NOTE]
> Huidige beperkingen:
>
> Hallo overlay dekkingsinstelling wordt niet ondersteund.
>
> Uw video bronbestand en Hallo overlay installatiekopiebestand hebben toobe in dezelfde asset Hallo en Hallo videobestand behoeften toobe instellen als primaire Hallo-bestand in deze activa.
>
>

### <a name="json-preset"></a>JSON-definitie
    {
      "Version": 1.0,
      "Sources": [
        {
          "Streams": [],
          "Filters": {
            "VideoOverlay": {
              "Position": {
                "X": 100,
                "Y": 100,
                "Width": 100,
                "Height": 50
              },
              "AudioGainLevel": 0.0,
              "MediaParams": [
                {
                  "OverlayLoopCount": 1
                },
                {
                  "IsOverlay": true,
                  "OverlayLoopCount": 1,
                  "InputLoop": true
                }
              ],
              "Source": "Image001.png",
              "Clip": {
                "Duration": "00:00:05"
              },
              "FadeInDuration": {
                "Duration": "00:00:01"
              },
              "FadeOutDuration": {
                "StartTime": "00:00:03",
                "Duration": "00:00:04"
              }
            }
          },
          "Pad": true
        }
      ],
      "Codecs": [
        {
          "KeyFrameInterval": "00:00:02",
          "H264Layers": [
            {
              "Profile": "Auto",
              "Level": "auto",
              "Bitrate": 1045,
              "MaxBitrate": 1045,
              "BufferWindow": "00:00:05",
              "ReferenceFrames": 3,
              "EntropyMode": "Cavlc",
              "AdaptiveBFrame": true,
              "Type": "H264Layer",
              "Width": "640",
              "Height": "360",
              "FrameRate": "0/1"
            }
          ],
          "Type": "H264Video"
        },
        {
          "Type": "CopyAudio"
        }
      ],
      "Outputs": [
        {
          "FileName": "{Basename}{Extension}",
          "Format": {
            "Type": "MP4Format"
          }
        }
      ]
    }


### <a name="xml-preset"></a>XML-definitie
    <?xml version="1.0" encoding="utf-16"?>
    <Preset xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Version="1.0" xmlns="http://www.windowsazure.com/media/encoding/Preset/2014/03">
      <Sources>
        <Source>
          <Streams />
          <Filters>
            <VideoOverlay>
              <Source>Image001.png</Source>
              <Clip Duration="PT5S" />
              <FadeInDuration Duration="PT1S" />
              <FadeOutDuration StartTime="PT3S" Duration="PT4S" />
              <Position X="100" Y="100" Width="100" Height="50" />
              <Opacity>0</Opacity>
              <AudioGainLevel>0</AudioGainLevel>
              <MediaParams>
                <MediaParam>
                  <IsOverlay>false</IsOverlay>
                  <OverlayLoopCount>1</OverlayLoopCount>
                  <InputLoop>false</InputLoop>
                </MediaParam>
                <MediaParam>
                  <IsOverlay>true</IsOverlay>
                  <OverlayLoopCount>1</OverlayLoopCount>
                  <InputLoop>true</InputLoop>
                </MediaParam>
              </MediaParams>
            </VideoOverlay>
          </Filters>
          <Pad>true</Pad>
        </Source>
      </Sources>
      <Encoding>
        <H264Video>
          <KeyFrameInterval>00:00:02</KeyFrameInterval>
          <H264Layers>
            <H264Layer>
              <Bitrate>1045</Bitrate>
              <Width>640</Width>
              <Height>360</Height>
              <FrameRate>0/1</FrameRate>
              <Profile>Auto</Profile>
              <Level>auto</Level>
              <BFrames>0</BFrames>
              <ReferenceFrames>3</ReferenceFrames>
              <Slices>0</Slices>
              <AdaptiveBFrame>true</AdaptiveBFrame>
              <EntropyMode>Cavlc</EntropyMode>
              <BufferWindow>00:00:05</BufferWindow>
              <MaxBitrate>1045</MaxBitrate>
            </H264Layer>
          </H264Layers>
        </H264Video>
        <CopyAudio />
      </Encoding>
      <Outputs>
        <Output FileName="{Basename}{Extension}">
          <MP4Format />
        </Output>
      </Outputs>
    </Preset>


## <a id="silent_audio"></a>Invoegen van een achtergrond-nummer als invoer geen audio heeft
Standaard als u een coderingsprogramma invoer toohello met alleen video en geen audio verzendt bevat vervolgens Hallo uitvoerasset bestanden die alleen video gegevens bevatten. Sommige spelers mogelijk geen toohandle dergelijke uitvoerstromen. In dit scenario kunt u deze instelling tooforce Hallo encoder tooadd een achtergrond-nummer toohello uitvoer.

tooforce hello encoder tooproduce een activum met een achtergrond-nummer invoer bevat geen audio Hallo 'InsertSilenceIfNoAudio'-waarde opgeven.

U kunt een van de Hallo MES standaardinstellingen gedocumenteerd in nemen [dit](media-services-mes-presets-overview.md) uit en breng Hallo wijziging:

### <a name="json-preset"></a>JSON-definitie
    {
      "Channels": 2,
      "SamplingRate": 44100,
      "Bitrate": 96,
      "Type": "AACAudio",
      "Condition": "InsertSilenceIfNoAudio"
    }

### <a name="xml-preset"></a>XML-definitie
    <AACAudio Condition="InsertSilenceIfNoAudio">
      <Channels>2</Channels>
      <SamplingRate>44100</SamplingRate>
      <Bitrate>96</Bitrate>
    </AACAudio>

## <a id="deinterlacing"></a>Automatische de-interlacing uitschakelen
Klanten hoeft niet toodo iets als ze zoals Hallo inhoud toobe automatisch ongedaan interlaced interliniëren. Wanneer Hallo automatisch de-interlacing is ingeschakeld (standaard) Hallo die mes Hallo automatische detectie van geïnterlinieerde frames en gemarkeerd als geïnterlinieerde frames alleen ongedaan interlaces.

U kunt uitschakelen Hallo automatisch de-interlacing. Deze optie wordt niet aanbevolen.

### <a name="json-preset"></a>JSON-definitie
    "Sources": [
    {
     "Filters": {
        "Deinterlace": {
          "Mode": "Off"
        }
      },
    }
    ]

### <a name="xml-preset"></a>XML-definitie
    <Sources>
    <Source>
      <Filters>
        <Deinterlace>
          <Mode>Off</Mode>
        </Deinterlace>
      </Filters>
    </Source>
    </Sources>


## <a id="audio_only"></a>Alleen audio standaardinstellingen
Deze sectie wordt gedemonstreerd twee alleen audio MES standaardinstellingen: AAC Audio- en AAC goede kwaliteit Audio.

### <a name="aac-audio"></a>AAC Audio
    {
      "Version": 1.0,
      "Codecs": [
        {
          "Profile": "AACLC",
          "Channels": 2,
          "SamplingRate": 48000,
          "Bitrate": 128,
          "Type": "AACAudio"
        }
      ],
      "Outputs": [
        {
          "FileName": "{Basename}_AAC_{AudioBitrate}.mp4",
          "Format": {
            "Type": "MP4Format"
          }
        }
      ]
    }

### <a name="aac-good-quality-audio"></a>AAC goede kwaliteit Audio
    {
      "Version": 1.0,
      "Codecs": [
        {
          "Profile": "AACLC",
          "Channels": 2,
          "SamplingRate": 48000,
          "Bitrate": 192,
          "Type": "AACAudio"
        }
      ],
      "Outputs": [
        {
          "FileName": "{Basename}_AAC_{AudioBitrate}.mp4",
          "Format": {
            "Type": "MP4Format"
          }
        }
      ]
    }

## <a id="concatenate"></a>Samenvoegen van twee of meer video bestanden

Hallo volgende voorbeeld ziet u het genereren van een vooraf ingestelde tooconcatenate twee of meer videobestanden. meest voorkomende scenario Hallo is dat u tooadd een kop of een aanhangwagen toohello belangrijkste video wilt. Hallo bedoeld wordt gebruikt wanneer Hallo videobestanden samen wordt bewerkt eigenschappen (beeldschermresolutie, framesnelheid, count-nummer, enzovoort delen). U moet behandelen niet toomix video's van verschillende framesnelheid of met een verschillend aantal audio houdt.

>[!NOTE]
>Hallo huidige ontwerp van Hallo samenvoeging functie verwacht dat Hallo invoer videoclips zijn consistent in termen van resolutie framesnelheid enzovoort. 

### <a name="requirements-and-considerations"></a>Vereisten en overwegingen

* Invoer video's mag alleen één-nummer hebben.
* Invoer video's, moeten alle Hallo hebben dezelfde framesnelheid.
* U moet uw video's uploaden naar afzonderlijke activa en Hallo video's instellen als primaire bestand Hallo in elke asset.
* U moet tooknow Hallo duur van uw video's.
* Hallo vooraf ingestelde in de volgende voorbeelden wordt ervan uitgegaan dat alle Hallo invoer video's starten met een tijdstempel van nul. U moet toomodify Hallo StartTime waarden als Hallo video's verschillende begin timestamp hebben, zoals gewoonlijk Hallo geval met live archieven.
* Hallo kunt JSON-definitie u expliciete verwijzingen toohello item-id hebt waarden van invoerbestand activa Hallo.
* Hallo voorbeeldcode wordt ervan uitgegaan dat Hallo die JSON voorinstelling tooa lokaal bestand, zoals 'C:\supportFiles\preset.json' is opgeslagen. Ook wordt ervan uitgegaan dat twee activa zijn gemaakt door het uploaden van twee videobestanden, en dat u weet Hallo resulterende waarden van item-id hebt.
* Hallo codefragment en JSON voorinstelling toont een voorbeeld van twee video bestanden worden samengevoegd. U kunt ook toomore dan twee video's door:

  1. Taak aanroepen. InputAssets.Add() herhaaldelijk tooadd meer video's, in volgorde.
  2. Toohello 'bronnen'-element in Hallo JSON, waardoor het bijbehorende bewerkt door meer vermeldingen toe te voegen in Hallo dezelfde volgorde.

### <a name="net-code"></a>.NET-code

    IAsset asset1 = _context.Assets.Where(asset => asset.Id == "nb:cid:UUID:606db602-efd7-4436-97b4-c0b867ba195b").FirstOrDefault();
    IAsset asset2 = _context.Assets.Where(asset => asset.Id == "nb:cid:UUID:a7e2b90f-0565-4a94-87fe-0a9fa07b9c7e").FirstOrDefault();

    // Declare a new job.
    IJob job = _context.Jobs.Create("Media Encoder Standard Job for Concatenating Videos");
    // Get a media processor reference, and pass tooit hello name of the
    // processor toouse for hello specific task.
    IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Standard");

    // Load hello XML (or JSON) from hello local file.
    string configuration = File.ReadAllText(@"c:\supportFiles\preset.json");

    // Create a task
    ITask task = job.Tasks.AddNew("Media Encoder Standard encoding task",
        processor,
        configuration,
        TaskOptions.None);

    // Specify hello input videos toobe concatenated (in order).
    task.InputAssets.Add(asset1);
    task.InputAssets.Add(asset2);
    // Add an output asset toocontain hello results of hello job.
    // This output is specified as AssetCreationOptions.None, which
    // means hello output asset is not encrypted.
    task.OutputAssets.AddNew("Output asset",
        AssetCreationOptions.None);

    job.StateChanged += new EventHandler<JobStateChangedEventArgs>(JobStateChanged);
    job.Submit();
    job.GetExecutionProgressTask(CancellationToken.None).Wait();

### <a name="json-preset"></a>JSON-definitie

Uw aangepaste voorinstelling met id's van Hallo activa dat u wilt dat tooconcatenate en met Hallo tijdstip segment voor elke video bijwerken.

    {
      "Version": 1.0,
      "Sources": [
        {
          "AssetID": "606db602-efd7-4436-97b4-c0b867ba195b",
          "StartTime": "00:00:01",
          "Duration": "00:00:15"
        },
        {
          "AssetID": "a7e2b90f-0565-4a94-87fe-0a9fa07b9c7e",
          "StartTime": "00:00:02",
          "Duration": "00:00:05"
        }
      ],
      "Codecs": [
        {
          "KeyFrameInterval": "00:00:02",
          "SceneChangeDetection": true,
          "H264Layers": [
            {
              "Level": "auto",
              "Bitrate": 1800,
              "MaxBitrate": 1800,
              "BufferWindow": "00:00:05",
              "BFrames": 3,
              "ReferenceFrames": 3,
              "AdaptiveBFrame": true,
              "Type": "H264Layer",
              "Width": "640",
              "Height": "360",
              "FrameRate": "0/1"
            }
          ],
          "Type": "H264Video"
        },
        {
          "Channels": 2,
          "SamplingRate": 48000,
          "Bitrate": 128,
          "Type": "AACAudio"
        }
      ],
      "Outputs": [
        {
          "FileName": "{Basename}_{Width}x{Height}_{VideoBitrate}.mp4",
          "Format": {
            "Type": "MP4Format"
          }
        }
      ]
    }

## <a id="crop"></a>Bijsnijden video's met Media Encoder Standard
Zie Hallo [video's met Media Encoder Standard bijsnijden](media-services-crop-video.md) onderwerp.

## <a id="no_video"></a>Invoegen van een video bijhouden als invoer geen video heeft

Standaard als u een coderingsprogramma invoer toohello met alleen audio en geen video verzendt bevat vervolgens Hallo uitvoerasset bestanden die alleen audiogegevens bevatten. Sommige spelers, met inbegrip van Azure Media Player (Zie [dit](https://feedback.azure.com/forums/169396-azure-media-services/suggestions/8082468-audio-only-scenarios)) mogelijk niet kunnen toohandle dergelijke stromen. U kunt deze instelling tooforce Hallo encoder tooadd een monochroom video bijhouden toohello uitvoer gebruiken in dit scenario.

> [!NOTE]
> Hallo encoder tooinsert dwingen een uitvoer video bijhouden toeneemt Hallo grootte van Hallo Asset uitvoer en waardoor Hallo kosten in rekening gebracht voor Hallo taak codering. U moet uitvoeren van tests tooverify die deze resulterende verhoging heeft alleen een matige impact op uw maandelijkse kosten.
>

### <a name="inserting-video-at-only-hello-lowest-bitrate"></a>Video op alleen Hallo laagste bitrate invoegen

Stel dat u gebruikt een meerdere bitrate encoding preset zoals [' standaardinstelling H264 Multiple Bitrate 720p '](media-services-mes-preset-h264-multiple-bitrate-720p.md) tooencode uw hele invoer catalogus voor streaming, die een combinatie van video en audio alleen-lezen bestanden bevat. In dit scenario wanneer Hallo invoer geen video heeft kunt u tooforce Hallo encoder tooinsert een video monochroom bijhouden op net Hallo laagste bitrate, als tegengestelde tooinserting video op elke bitrate uitvoer. tooachieve, moet u toouse hello **InsertBlackIfNoVideoBottomLayerOnly** vlag.

U kunt een van de Hallo MES standaardinstellingen gedocumenteerd in nemen [dit](media-services-mes-presets-overview.md) uit en breng Hallo wijziging:

#### <a name="json-preset"></a>JSON-definitie
    {
          "KeyFrameInterval": "00:00:02",
          "StretchMode": "AutoSize",
          "Condition": "InsertBlackIfNoVideoBottomLayerOnly",
          "H264Layers": [
          …
          ]
    }

#### <a name="xml-preset"></a>XML-definitie

Wanneer u XML, gebruikt u voorwaarde = 'InsertBlackIfNoVideoBottomLayerOnly' als een kenmerk toohello **H264Video** -element en de voorwaarde 'InsertSilenceIfNoAudio' te als een kenmerk =**AACAudio**.

```
. . .
<Encoding>
  <H264Video Condition="InsertBlackIfNoVideoBottomLayerOnly">
    <KeyFrameInterval>00:00:02</KeyFrameInterval>
    <SceneChangeDetection>true</SceneChangeDetection>
    <StretchMode>AutoSize</StretchMode>
    <H264Layers>
      <H264Layer>
        . . .
      </H264Layer>
    </H264Layers>
    <Chapters />
  </H264Video>
  <AACAudio Condition="InsertSilenceIfNoAudio">
    <Profile>AACLC</Profile>
    <Channels>2</Channels>
    <SamplingRate>48000</SamplingRate>
    <Bitrate>128</Bitrate>
  </AACAudio>
</Encoding>
. . .
```

### <a name="inserting-video-at-all-output-bitrates"></a>Video helemaal invoegen uitvoer bitsnelheden
Stel dat u gebruikt een meerdere bitrate encoding preset zoals [' standaardinstelling H264 Multiple Bitrate 720p](media-services-mes-preset-H264-Multiple-Bitrate-720p.md) tooencode uw hele invoer catalogus voor streaming, die een combinatie van video en audio alleen-lezen bestanden bevat. In dit scenario wanneer Hallo invoer geen video heeft kunt u tooforce Hallo encoder tooinsert monochroom video op alle Hallo uitvoer bitsnelheden bijhouden. Dit zorgt ervoor dat de uitvoer activa zijn alle homogene met toonumber ten opzichte van houdt video en audio houdt. tooachieve, moet u toospecify Hallo 'InsertBlackIfNoVideo' vlag.

U kunt een van de Hallo MES standaardinstellingen gedocumenteerd in nemen [dit](media-services-mes-presets-overview.md) uit en breng Hallo wijziging:

#### <a name="json-preset"></a>JSON-definitie
    {
          "KeyFrameInterval": "00:00:02",
          "StretchMode": "AutoSize",
          "Condition": "InsertBlackIfNoVideo",
          "H264Layers": [
          …
          ]
    }

#### <a name="xml-preset"></a>XML-definitie

Wanneer u XML, gebruikt u voorwaarde = 'InsertBlackIfNoVideo' als een kenmerk toohello **H264Video** -element en de voorwaarde 'InsertSilenceIfNoAudio' te als een kenmerk =**AACAudio**.

```
. . .
<Encoding>
  <H264Video Condition="InsertBlackIfNoVideo">
    <KeyFrameInterval>00:00:02</KeyFrameInterval>
    <SceneChangeDetection>true</SceneChangeDetection>
    <StretchMode>AutoSize</StretchMode>
    <H264Layers>
      <H264Layer>
        . . .
      </H264Layer>
    </H264Layers>
    <Chapters />
  </H264Video>
  <AACAudio Condition="InsertSilenceIfNoAudio">
    <Profile>AACLC</Profile>
    <Channels>2</Channels>
    <SamplingRate>48000</SamplingRate>
    <Bitrate>128</Bitrate>
  </AACAudio>
</Encoding>
. . .  
```

## <a id="rotate_video"></a>Een video draaien
Hallo [Media Encoder Standard](media-services-dotnet-encode-with-media-encoder-standard.md) draaihoek door hoeken van 0/90/180/270 ondersteunt. Hallo standaardgedrag is 'Auto', waarbij toodetect Hallo rotatie metagegevens in de binnenkomende videobestand Hallo probeert en compenseren voor het. Neem de volgende Hallo **bronnen** element tooone van Hallo standaardinstellingen die zijn gedefinieerd in [dit](media-services-mes-presets-overview.md) sectie:

### <a name="json-preset"></a>JSON-definitie
    "Sources": [
    {
      "Streams": [],
      "Filters": {
        "Rotation": "90"
      }
    }
    ],
    "Codecs": [

    ...
### <a name="xml-preset"></a>XML-definitie
    <Sources>
           <Source>
          <Streams />
          <Filters>
            <Rotation>90</Rotation>
          </Filters>
        </Source>
    </Sources>

Zie ook [dit](media-services-mes-schema.md#PreserveResolutionAfterRotation) onderwerp voor meer informatie over hoe Hallo encoder worden geïnterpreteerd Hallo breedte en hoogte-instellingen in Hallo definitie wanneer rotatie compensatie wordt geactiveerd.

U kunt Hallo waarde '0' tooindicate toohello encoder tooignore rotatie van de metagegevens, indien aanwezig, in Hallo invoervideo.

## <a name="media-services-learning-paths"></a>Media Services-leertrajecten
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Feedback geven
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a>Zie ook
[Media Services-codering overzicht](media-services-encode-asset.md)

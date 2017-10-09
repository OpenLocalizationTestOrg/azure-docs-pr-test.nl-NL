---
title: aaaSmooth Streaming Windows Store-App-zelfstudie | Microsoft Docs
description: Meer informatie over hoe toouse Azure Media Services toocreate een C# Windows Store-toepassing met een XML-MediaElement tooplayback Smooth Stream inhoud beheren.
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 0fa5d8c5-3d5f-4886-ae55-fb6de4f5256d
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/11/2017
ms.author: juliako
ms.openlocfilehash: b02aa2c7f68fe22a23ea846d72fdd23bfba2b19c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toobuild-a-smooth-streaming-windows-store-application"></a>Hoe tooBuild een Smooth Streaming Windows Store-toepassing

Hallo Smooth Streaming Client SDK voor Windows 8 kan ontwikkelaars toobuild Windows Store-toepassingen die op aanvraag en live-Smooth Streaming inhoud kunnen spelen. Bovendien biedt toohello basic afspelen van Smooth Streaming-inhoud, Hallo SDK ook uitgebreide functies zoals Microsoft PlayReady protection, kwaliteit niveau beperking, DVR, audiostroom overschakelen, luisteren naar statusupdates (zoals kwaliteit niveau wijzigingen Live ) en foutgebeurtenissen, enzovoort. Zie voor meer informatie van functies ondersteund Hallo Hallo [release-opmerkingen](http://www.iis.net/learn/media/smooth-streaming/smooth-streaming-client-sdk-for-windows-8-release-notes). Zie voor meer informatie [Player Framework voor Windows 8](http://playerframework.codeplex.com/). 

Deze zelfstudie bevat vier uitkomsten:

1. Een eenvoudige Smooth Streaming Store-toepassing maken
2. Toevoegen van een schuifbalk tooControl Hallo Media uitgevoerd
3. Selecteer Streams Smooth Streaming
4. Selecteer nummers Smooth Streaming

## <a name="prerequisites"></a>Vereisten
* Windows 8, 32-bits of 64-bits. U kunt krijgen [Windows 8 Enterprise Evaluation](http://msdn.microsoft.com/evalcenter/jj554510.aspx) van MSDN.
* Visual Studio 2012 of Visual Studio Express 2012 (of een latere versie). U krijgt Hallo evaluatieversie van [hier](http://www.microsoft.com/visualstudio/11/downloads).
* [Microsoft Smooth Streaming Client SDK voor Windows 8](http://visualstudiogallery.msdn.microsoft.com/04423d13-3b3e-4741-a01c-1ae29e84fea6?SRC=Homehttp://visualstudiogallery.msdn.microsoft.com/04423d13-3b3e-4741-a01c-1ae29e84fea6?SRC=Home).

oplossing voor elke les Hallo voltooid kan worden gedownload van MSDN Developer-codevoorbeelden (Codegalerie): 

* [Les 1](http://code.msdn.microsoft.com/Smooth-Streaming-Client-0bb1471f) : een eenvoudige Windows 8-Smooth Streaming MediaPlayer 
* [Les 2](http://code.msdn.microsoft.com/A-simple-Windows-8-Smooth-ee98f63a) : een eenvoudige Windows 8-Smooth Streaming MediaPlayer met een schuifregelaar beheren 
* [Les 3](http://code.msdn.microsoft.com/A-Windows-8-Smooth-883c3b44) - een Windows 8-Smooth Streaming MediaPlayer met Stream-selectie  
* [4 les](http://code.msdn.microsoft.com/A-Windows-8-Smooth-aa9e4907) - een Windows 8-Smooth Streaming MediaPlayer bij selectie bijhouden.

## <a name="lesson-1-create-a-basic-smooth-streaming-store-application"></a>Les 1: Een eenvoudige Smooth Streaming Store-toepassing maken

In deze les maakt u een Windows Store-toepassing met een MediaElement besturingselement tooplay Smooth Stream inhoud.  de actieve toepassing Hello ziet eruit als:

![Voorbeeld van Smooth Streaming Windows Store-toepassing][PlayerApplication]

Zie voor meer informatie over het ontwikkelen van Windows Store-toepassing [ontwikkelen geweldige Apps voor Windows 8](http://msdn.microsoft.com/windows/apps/br229512.aspx). Deze les bevat Hallo procedures te volgen:

1. Een Windows Store-project maken
2. Hallo-gebruikersinterface (XAML) ontwerpen
3. Hallo onderliggende-codebestand wijzigen
4. Compileren en Hallo toepassing testen

**toocreate Windows Store-project**

1. Visual Studio 2012 of hoger wordt uitgevoerd.
2. Van Hallo **bestand** menu, klikt u op **nieuw**, en klik vervolgens op **Project**.
3. In het dialoogvenster Nieuw Project Hallo waarden type of selecteer Hallo volgende:

| Naam | Waarde |
| --- | --- |
| Sjabloongroep |Geïnstalleerd/sjablonen/Visual C# / van Windows Store |
| Template |Lege App (XAML) |
| Naam |SSPlayer |
| Locatie |C:\SSTutorials |
| Naam van de oplossing |SSPlayer |
| Map voor oplossing maken |(geselecteerd) |

1. Klik op **OK**.

**tooadd een verwijzing toohello Smooth Streaming Client SDK**

1. In Solution Explorer met de rechtermuisknop op **SSPlayer**, en klik vervolgens op **verwijzing toevoegen**.
2. Typ of selecteer Hallo volgende waarden:

| Naam | Waarde |
| --- | --- |
| Referentie-groep |Windows-uitbreidingen |
| Naslaginformatie |Selecteer Microsoft Smooth Streaming Client SDK voor Windows 8 en Microsoft Visual C++ Runtime-pakket |

1. Klik op **OK**. 

Na het toevoegen van Hallo verwijzingen u Hallo gericht platform (x64 of x86) moet selecteren, toe te voegen verwijzingen werkt niet voor platformconfiguratie Any CPU.  Klik in solution explorer ziet u gele waarschuwing is ingeschakeld voor deze referenties toegevoegd.

**toodesign hello player-gebruikersinterface**

1. Klik in Solution Explorer, dubbelklik op **MainPage.xaml** tooopen in Hallo ontwerp weergeven.
2. Zoek Hallo  **&lt;raster&gt;**  en  **&lt;/Grid&gt;**  labels Hallo XAML-bestand en plakken Hallo volgende code tussen de twee Hallo tags:

         <Grid.RowDefinitions>

            <RowDefinition Height="20"/>    <!-- spacer -->
            <RowDefinition Height="50"/>    <!-- media controls -->
            <RowDefinition Height="100*"/>  <!-- media element -->
            <RowDefinition Height="80*"/>   <!-- media stream and track selection -->
            <RowDefinition Height="50"/>    <!-- status bar -->
         </Grid.RowDefinitions>

         <StackPanel Name="spMediaControl" Grid.Row="1" Orientation="Horizontal">
            <TextBlock x:Name="tbSource" Text="Source :  " FontSize="16" FontWeight="Bold" VerticalAlignment="Center" />
            <TextBox x:Name="txtMediaSource" Text="http://ecn.channel9.msdn.com/o9/content/smf/smoothcontent/elephantsdream/Elephants_Dream_1024-h264-st-aac.ism/manifest" FontSize="10" Width="700" Margin="0,4,0,10" />
            <Button x:Name="btnSetSource" Content="Set Source" Width="111" Height="43" Click="btnSetSource_Click"/>
            <Button x:Name="btnPlay" Content="Play" Width="111" Height="43" Click="btnPlay_Click"/>
            <Button x:Name="btnPause" Content="Pause"  Width="111" Height="43" Click="btnPause_Click"/>
            <Button x:Name="btnStop" Content="Stop"  Width="111" Height="43" Click="btnStop_Click"/>
            <CheckBox x:Name="chkAutoPlay" Content="Auto Play" Height="55" Width="Auto" IsChecked="{Binding AutoPlay, ElementName=mediaElement, Mode=TwoWay}"/>
            <CheckBox x:Name="chkMute" Content="Mute" Height="55" Width="67" IsChecked="{Binding IsMuted, ElementName=mediaElement, Mode=TwoWay}"/>
         </StackPanel>

         <StackPanel Name="spMediaElement" Grid.Row="2" Height="435" Width="1072"
                    HorizontalAlignment="Center" VerticalAlignment="Center">
            <MediaElement x:Name="mediaElement" Height="356" Width="924" MinHeight="225"
                          HorizontalAlignment="Center" VerticalAlignment="Center" 
                          AudioCategory="BackgroundCapableMedia" />
            <StackPanel Orientation="Horizontal">
                <Slider x:Name="sliderProgress" Width="924" Height="44"
                        HorizontalAlignment="Center" VerticalAlignment="Center"
                        PointerPressed="sliderProgress_PointerPressed"/>
                <Slider x:Name="sliderVolume" 
                        HorizontalAlignment="Right" VerticalAlignment="Center" Orientation="Vertical" 
                        Height="79" Width="148" Minimum="0" Maximum="1" StepFrequency="0.1" 
                        Value="{Binding Volume, ElementName=mediaElement, Mode=TwoWay}" 
                        ToolTipService.ToolTip="{Binding Value, RelativeSource={RelativeSource Mode=Self}}"/>
            </StackPanel>
         </StackPanel>

         <StackPanel Name="spStatus" Grid.Row="4" Orientation="Horizontal">
            <TextBlock x:Name="tbStatus" Text="Status :  " 
               FontSize="16" FontWeight="Bold" VerticalAlignment="Center" HorizontalAlignment="Center" />
            <TextBox x:Name="txtStatus" FontSize="10" Width="700" VerticalAlignment="Center"/>
         </StackPanel>
   
   Hallo MediaElement besturingselement is gebruikte tooplayback media. Hallo schuifregelaars met de naam sliderProgress wordt Hallo volgende les toocontrol Hallo media uitgevoerd gebruikt.
3. Druk op **CTRL + S** toosave Hallo-bestand.

Hallo MediaElement beheer biedt geen ondersteuning voor Smooth Streaming inhoud out-of-box. ondersteuning van tooenable Hallo-Smooth Streaming, moet u Hallo Smooth Streaming bytestream handler door bestandsnaamextensie en een MIME-type registreren.  tooregister, gebruikt u Hallo MediaExtensionManager.RegisterByteStremHandler hello Windows.Media naamruimte.

In dit XAML-bestand zijn sommige gebeurtenis-handlers gekoppeld aan Hallo besturingselementen.  U moet deze gebeurtenis-handlers definiëren.

**toomodify hello onderliggende-codebestand**

1. In Solution Explorer met de rechtermuisknop op **MainPage.xaml**, en klik vervolgens op **weergavecode**.
2. Bovenaan Hallo Hallo-bestand, voegt u de volgende Hallo toe met de instructie:
   
        using Windows.Media;
3. Aan begin Hallo Hallo **MainPage** klasse, Hallo gegevenslid volgende toevoegen:
   
         private MediaExtensionManager extensions = new MediaExtensionManager();
4. Achter Hallo Hallo **MainPage** constructor Hallo volgende twee regels toevoegen:
   
        extensions.RegisterByteStreamHandler("Microsoft.Media.AdaptiveStreaming.SmoothByteStreamHandler", ".ism", "text/xml");
        extensions.RegisterByteStreamHandler("Microsoft.Media.AdaptiveStreaming.SmoothByteStreamHandler", ".ism", "application/vnd.ms-sstr+xml");
5. Achter Hallo Hallo **MainPage** klasse, plak Hallo code te volgen:
   
         # region UI Button Click Events
         private void btnPlay_Click(object sender, RoutedEventArgs e)
         {

         mediaElement.Play();
         txtStatus.Text = "MediaElement is playing ...";
         }
         private void btnPause_Click(object sender, RoutedEventArgs e)
         {

         mediaElement.Pause();
         txtStatus.Text = "MediaElement is paused";
         }
         private void btnSetSource_Click(object sender, RoutedEventArgs e)
         {

         sliderProgress.Value = 0;
         mediaElement.Source = new Uri(txtMediaSource.Text);

         if (chkAutoPlay.IsChecked == true)
         {
             txtStatus.Text = "MediaElement is playing ...";
         }
         else
         {
             txtStatus.Text = "Click hello Play button tooplay hello media source.";
         }
         }
         private void btnStop_Click(object sender, RoutedEventArgs e)
         {

         mediaElement.Stop();
         txtStatus.Text = "MediaElement is stopped";
         }
         private void sliderProgress_PointerPressed(object sender, PointerRoutedEventArgs e)
         {

         txtStatus.Text = "Seek tooposition " + sliderProgress.Value;
         mediaElement.Position = new TimeSpan(0, 0, (int)(sliderProgress.Value));
         }
         # endregion

Hallo sliderProgress_PointerPressed gebeurtenis-handler wordt hier gedefinieerd.  Er zijn meer works toodo tooget Hiermee aan de slag, die worden behandeld in de volgende les Hallo van deze zelfstudie.
6. Druk op **CTRL + S** toosave Hallo-bestand.

Hallo moet klaar Hallo onderliggende-codebestand uitzien:

![CodeView in Visual Studio of Smooth Streaming Windows Store-toepassing][CodeViewPic]

**toocompile en test Hallo-toepassing**

1. Van Hallo **bouwen** menu, klikt u op **Configuration Manager**.
2. Wijziging **actieve oplossing platform** toomatch uw ontwikkelplatform.
3. Druk op **F6** toocompile Hallo project. 
4. Druk op **F5** toorun Hallo-toepassing.
5. Bovenaan Hallo Hallo toepassing, kunt u Hallo standaard-URL voor Smooth Streaming of voer een andere. 
6. Klik op **bron instellen**. Omdat **automatisch afspelen** is standaard hello wordt afgespeeld automatisch ingeschakeld.  U kunt beheren met Hallo Hallo-media **afspelen**, **onderbreken** en **stoppen** knoppen.  U kunt Hallo Mediavolume met verticale schuifbalk Hallo beheren.  Hallo echter horizontale schuifbalk voor het beheren van Hallo media uitgevoerd is volledig nog niet geïmplementeerd. 

U kunt lesson1 hebt voltooid.  In deze les gebruikt u een MediaElement besturingselement tooplayback Smooth Streaming-inhoud.  In de volgende les hello, moet u een schuifregelaar toocontrol Hallo voortgang Hallo Smooth Streaming inhoud toevoegen.

## <a name="lesson-2-add-a-slider-bar-toocontrol-hello-media-progress"></a>Les 2: Een schuifbalk tooControl Hallo Media uitgevoerd toevoegen

In les 1, kunt u een Windows Store-servicetoepassing gemaakt met een MediaElement XAML besturingselement tooplayback Smooth Streaming media-inhoud.  Sommige functies basic media zoals starten, stoppen en onderbreken wordt geleverd.  In deze les, moet u een schuifregelaar balk besturingselement toohello toepassing toevoegen.

In deze zelfstudie gebruiken we een timer tooupdate Hallo positie van de schuifregelaar op basis van de huidige positie Hallo Hallo MediaElement besturingselement.  Hallo schuifregelaar start- en eindtijd ook nodig toobe bijgewerkt in geval van een live-inhoud.  Dit kan beter worden verwerkt in Hallo adaptieve bron update gebeurtenis.

Mediabronnen zijn objecten die mediagegevens genereren.  Hallo voor de bronoplossing een URL of byte-stroom accepteert en maakt Hallo juiste mediumbron voor die inhoud.  Hallo voor de bronoplossing is standaard manier Hallo toepassingen toocreate mediabronnen Hallo. 

Deze les bevat Hallo procedures te volgen:

1. Hallo Smooth Streaming-handler registreren 
2. Hallo adaptieve bron manager niveau gebeurtenis-handlers toevoegen
3. Hallo adaptieve bron niveau gebeurtenis-handlers toevoegen
4. Gebeurtenis-handlers MediaElement toevoegen
5. Schuifregelaar gerelateerde code toevoegen
6. Compileren en Hallo toepassing testen

**tooregister hello Smooth Streaming bytestream handler en pass Hallo propertyset**

1. In Solution Explorer met de rechtermuisknop op **MainPage.xaml**, en klik vervolgens op **weergavecode**.
2. Aan het begin van de Hallo van Hallo-bestand, voegt u de volgende Hallo toe met de instructie:

        using Microsoft.Media.AdaptiveStreaming;
3. Toevoegen aan het begin van de Hallo Hallo MainPage klasse, Hallo gegevensleden te volgen:

         private Windows.Foundation.Collections.PropertySet propertySet = new Windows.Foundation.Collections.PropertySet();             
         private IAdaptiveSourceManager adaptiveSourceManager;
4. Hallo binnen **MainPage** constructor toevoegen na code na Hallo Hallo **dit. Initialiseren van Components();**  regel en Hallo registratie coderegels in de vorige les Hallo geschreven:

        // Gets hello default instance of AdaptiveSourceManager which manages Smooth 
        //Streaming media sources.
        adaptiveSourceManager = AdaptiveSourceManager.GetDefault();
        // Sets property key value tooAdaptiveSourceManager default instance.
        // {A5CE1DE8-1D00-427B-ACEF-FB9A3C93DE2D}" must be hardcoded.
        propertySet["{A5CE1DE8-1D00-427B-ACEF-FB9A3C93DE2D}"] = adaptiveSourceManager;
5. Hallo binnen **MainPage** -constructor aan, wijzig Hallo twee RegisterByteStreamHandler methoden tooadd Hallo beschreven parameters:

         // Registers Smooth Streaming byte-stream handler for ".ism" extension and, 
         // "text/xml" and "application/vnd.ms-ss" mime-types and pass hello propertyset. 
         // http://*.ism/manifest URI resources will be resolved by Byte-stream handler.
         extensions.RegisterByteStreamHandler(

            "Microsoft.Media.AdaptiveStreaming.SmoothByteStreamHandler", 
            ".ism", 
            "text/xml", 
            propertySet );
         extensions.RegisterByteStreamHandler(

            "Microsoft.Media.AdaptiveStreaming.SmoothByteStreamHandler", 
            ".ism", 
            "application/vnd.ms-sstr+xml", 
         propertySet);
6. Druk op **CTRL + S** toosave Hallo-bestand.

**tooadd hello adaptieve bron manager niveau gebeurtenis-handler**

1. In Solution Explorer met de rechtermuisknop op **MainPage.xaml**, en klik vervolgens op **weergavecode**.
2. Hallo binnen **MainPage** klasse, Hallo gegevenslid volgende toevoegen:
   
     persoonlijke AdaptiveSource adaptiveSource = null;
3. Achter Hallo Hallo **MainPage** klasse, Hallo volgende gebeurtenis-handler toevoegen:
   
         # region Adaptive Source Manager Level Events
         private void mediaElement_AdaptiveSourceOpened(AdaptiveSource sender, AdaptiveSourceOpenedEventArgs args)
         {

            adaptiveSource = args.AdaptiveSource;
         }

         # endregion Adaptive Source Manager Level Events
4. Achter Hallo Hallo **MainPage** constructor toevoegen Hallo regel toosubscribe toohello adaptieve bron open gebeurtenis te volgen:
   
         adaptiveSourceManager.AdaptiveSourceOpenedEvent += 
           new AdaptiveSourceOpenedEventHandler(mediaElement_AdaptiveSourceOpened);
5. Druk op **CTRL + S** toosave Hallo-bestand.

**tooadd adaptieve bron niveau gebeurtenis-handlers**

1. In Solution Explorer met de rechtermuisknop op **MainPage.xaml**, en klik vervolgens op **weergavecode**.
2. Hallo binnen **MainPage** klasse, Hallo gegevenslid volgende toevoegen:
   
     persoonlijke AdaptiveSourceStatusUpdatedEventArgs adaptiveSourceStatusUpdate;   persoonlijke Manifest manifestObject;
3. Achter Hallo Hallo **MainPage** klasse, Hallo volgende gebeurtenis-handlers toevoegen:

         # region Adaptive Source Level Events
         private void mediaElement_ManifestReady(AdaptiveSource sender, ManifestReadyEventArgs args)
         {

            adaptiveSource = args.AdaptiveSource;
            manifestObject = args.AdaptiveSource.Manifest;
         }

         private void mediaElement_AdaptiveSourceStatusUpdated(AdaptiveSource sender, AdaptiveSourceStatusUpdatedEventArgs args)
         {

            adaptiveSourceStatusUpdate = args;
         }

         private void mediaElement_AdaptiveSourceFailed(AdaptiveSource sender, AdaptiveSourceFailedEventArgs args)
         {

            txtStatus.Text = "Error: " + args.HttpResponse;
         }

         # endregion Adaptive Source Level Events
4. Achter Hallo Hallo **mediaElement AdaptiveSourceOpened** methode toevoegen Hallo code toosubscribe toohello gebeurtenissen te volgen:
   
         adaptiveSource.ManifestReadyEvent +=

                    mediaElement_ManifestReady;
         adaptiveSource.AdaptiveSourceStatusUpdatedEvent += 

            mediaElement_AdaptiveSourceStatusUpdated;
         adaptiveSource.AdaptiveSourceFailedEvent += 

            mediaElement_AdaptiveSourceFailed;
5. Druk op **CTRL + S** toosave Hallo-bestand.

Hallo dezelfde gebeurtenissen voor adaptieve bron Manager niveau, die kan worden gebruikt voor het verwerken van functionaliteit tooall media standaardelementen in Hallo-app beschikbaar zijn. Elke AdaptiveSource omvat zijn eigen gebeurtenissen en worden alle gebeurtenissen voor AdaptiveSource trapsgewijs onder AdaptiveSourceManager.

**gebeurtenis-handlers voor tooadd Media-Element**

1. In Solution Explorer met de rechtermuisknop op **MainPage.xaml**, en klik vervolgens op **weergavecode**.
2. Achter Hallo Hallo **MainPage** klasse, Hallo volgende gebeurtenis-handlers toevoegen:

         # region Media Element Event Handlers
         private void MediaOpened(object sender, RoutedEventArgs e)
         {

            txtStatus.Text = "MediaElement opened";
         }

         private void MediaFailed(object sender, ExceptionRoutedEventArgs e)
         {

            txtStatus.Text= "MediaElement failed: " + e.ErrorMessage;
         }

         private void MediaEnded(object sender, RoutedEventArgs e)
         {

            txtStatus.Text ="MediaElement ended.";
         }

         # endregion Media Element Event Handlers
3. Achter Hallo Hallo **MainPage** constructor toevoegen Hallo code toosubscript toohello gebeurtenissen te volgen:

         mediaElement.MediaOpened += MediaOpened;
         mediaElement.MediaEnded += MediaEnded;
         mediaElement.MediaFailed += MediaFailed;
4. Druk op **CTRL + S** toosave Hallo-bestand.

**de schuifregelaar tooadd gerelateerde streepjescode**

1. In Solution Explorer met de rechtermuisknop op **MainPage.xaml**, en klik vervolgens op **weergavecode**.
2. Aan het begin van de Hallo van Hallo-bestand, voegt u de volgende Hallo toe met de instructie:
      
        using Windows.UI.Core;
3. Hallo binnen **MainPage** klasse, Hallo volgende gegevensleden toe te voegen:
   
         public static CoreDispatcher _dispatcher;
         private DispatcherTimer sliderPositionUpdateDispatcher;
4. Achter Hallo Hallo **MainPage** constructor Hallo na code toevoegen:
   
         _dispatcher = Window.Current.Dispatcher;
         PointerEventHandler pointerpressedhandler = new PointerEventHandler(sliderProgress_PointerPressed);
         sliderProgress.AddHandler(Control.PointerPressedEvent, pointerpressedhandler, true);    
5. Achter Hallo Hallo **MainPage** klasse, Hallo volgende code toe te voegen:

         # region sliderMediaPlayer
         private double SliderFrequency(TimeSpan timevalue)
         {

            long absvalue = 0;
            double stepfrequency = -1;

            if (manifestObject != null)
            {
                absvalue = manifestObject.Duration - (long)manifestObject.StartTime;
            }
            else
            {
                absvalue = mediaElement.NaturalDuration.TimeSpan.Ticks;
            }

            TimeSpan totalDVRDuration = new TimeSpan(absvalue);

            if (totalDVRDuration.TotalMinutes >= 10 && totalDVRDuration.TotalMinutes < 30)
            {
               stepfrequency = 10;
            }
            else if (totalDVRDuration.TotalMinutes >= 30 
                     && totalDVRDuration.TotalMinutes < 60)
            {
                stepfrequency = 30;
            }
            else if (totalDVRDuration.TotalHours >= 1)
            {
                stepfrequency = 60;
            }

            return stepfrequency;
         }

         void updateSliderPositionoNTicks(object sender, object e)
         {

            sliderProgress.Value = mediaElement.Position.TotalSeconds;
         }

         public void setupTimer()
         {

            sliderPositionUpdateDispatcher = new DispatcherTimer();
            sliderPositionUpdateDispatcher.Interval = new TimeSpan(0, 0, 0, 0, 300);
            startTimer();
         }

         public void startTimer()
         {

            sliderPositionUpdateDispatcher.Tick += updateSliderPositionoNTicks;
            sliderPositionUpdateDispatcher.Start();
         }

         // Slider start and end time must be updated in case of live content
         public async void setSliderStartTime(long startTime)
         {

            await _dispatcher.RunAsync(CoreDispatcherPriority.Normal, () =>
            {
                TimeSpan timespan = new TimeSpan(adaptiveSourceStatusUpdate.StartTime);
                double absvalue = (int)Math.Round(timespan.TotalSeconds, MidpointRounding.AwayFromZero);
                sliderProgress.Minimum = absvalue;
            });
         }

         // Slider start and end time must be updated in case of live content
         public async void setSliderEndTime(long startTime)
         {

            await _dispatcher.RunAsync(CoreDispatcherPriority.Normal, () =>
            {
                TimeSpan timespan = new TimeSpan(adaptiveSourceStatusUpdate.EndTime);
                double absvalue = (int)Math.Round(timespan.TotalSeconds, MidpointRounding.AwayFromZero);
                sliderProgress.Maximum = absvalue;
            });
         }

         # endregion sliderMediaPlayer
      
>[!NOTE]
>CoreDispatcher is gebruikte toomake wijzigingen toohello UI-thread van niet-UI-Thread. In geval van een knelpunt op dispatcher-thread kunt developer toouse dispatcher geleverd door UI-element dat hij wil tooupdate.  Bijvoorbeeld:
   
         await sliderProgress.Dispatcher.RunAsync(CoreDispatcherPriority.Normal, () => { TimeSpan 

         timespan = new TimeSpan(adaptiveSourceStatusUpdate.EndTime); 
         double absvalue  = (int)Math.Round(timespan.TotalSeconds, MidpointRounding.AwayFromZero); 

         sliderProgress.Maximum = absvalue; }); 
6. Achter Hallo Hallo **mediaElement_AdaptiveSourceStatusUpdated** methode Hallo na code toevoegen:

         setSliderStartTime(args.StartTime);
         setSliderEndTime(args.EndTime);
7. Achter Hallo Hallo **MediaOpened** methode Hallo na code toevoegen:

         sliderProgress.StepFrequency = SliderFrequency(mediaElement.NaturalDuration.TimeSpan);
         sliderProgress.Width = mediaElement.Width;
         setupTimer();
8. Druk op **CTRL + S** toosave Hallo-bestand.

**toocompile en test Hallo-toepassing**

1. Druk op **F6** toocompile Hallo project. 
2. Druk op **F5** toorun Hallo-toepassing.
3. Bovenaan Hallo Hallo toepassing, kunt u Hallo standaard-URL voor Smooth Streaming of voer een andere. 
4. Klik op **bron instellen**. 
5. Test Hallo schuifregelaar.

U kunt les 2 hebt voltooid.  In deze les moet u een schuifregelaar tooapplication toegevoegd. 

## <a name="lesson-3-select-smooth-streaming-streams"></a>Les 3: Selecteer Streams Smooth Streaming
Smooth Streaming is geschikt toostream inhoud met meerdere taal audio nummers die kunnen geselecteerd door Hallo viewers worden.  In deze les schakelt u viewers tooselect stromen. Deze les bevat Hallo procedures te volgen:

1. Hallo XAML-bestand wijzigen
2. Hallo-codebestand behand wijzigen
3. Compileren en Hallo toepassing testen

**toomodify hello XAML-bestand**

1. In Solution Explorer met de rechtermuisknop op **MainPage.xaml**, en klik vervolgens op **ontwerper**.
2. Zoek &lt;Grid.RowDefinitions&gt;, en wijzig Hallo RowDefinitions zodat ze eruitzien:
   
         <Grid.RowDefinitions>            
            <RowDefinition Height="20"/>
            <RowDefinition Height="50"/>
            <RowDefinition Height="100"/>
            <RowDefinition Height="80"/>
            <RowDefinition Height="50"/>
         </Grid.RowDefinitions>
3. Hallo binnen &lt;raster&gt;&lt;/Grid&gt; tags toevoegen Hallo volgende code toodefine een keuzelijst, zodat gebruikers kunnen Hallo van de beschikbare stromen overzicht en streams selecteren:

         <Grid Name="gridStreamAndBitrateSelection" Grid.Row="3">
            <Grid.RowDefinitions>
                <RowDefinition Height="300"/>
            </Grid.RowDefinitions>
            <Grid.ColumnDefinitions>
                <ColumnDefinition Width="250*"/>
                <ColumnDefinition Width="250*"/>
            </Grid.ColumnDefinitions>
            <StackPanel Name="spStreamSelection" Grid.Row="1" Grid.Column="0">
                <StackPanel Orientation="Horizontal">
                    <TextBlock Name="tbAvailableStreams" Text="Available Streams:" FontSize="16" VerticalAlignment="Center"></TextBlock>
                    <Button Name="btnChangeStreams" Content="Submit" Click="btnChangeStream_Click"/>
                </StackPanel>
                <ListBox x:Name="lbAvailableStreams" Height="200" Width="200" Background="Transparent" HorizontalAlignment="Left" 
                    ScrollViewer.VerticalScrollMode="Enabled" ScrollViewer.VerticalScrollBarVisibility="Visible">
                    <ListBox.ItemTemplate>
                        <DataTemplate>
                            <CheckBox Content="{Binding Name}" IsChecked="{Binding isChecked, Mode=TwoWay}" />
                        </DataTemplate>
                    </ListBox.ItemTemplate>
                </ListBox>
            </StackPanel>
         </Grid>
4. Druk op **CTRL + S** toosave Hallo wijzigingen.

**toomodify hello onderliggende-codebestand**

1. In Solution Explorer met de rechtermuisknop op **MainPage.xaml**, en klik vervolgens op **weergavecode**.
2. Voeg een nieuwe klasse in Hallo SSPlayer naamruimte:
   
        #region class Stream
   
        public class Stream
        {
            private IManifestStream stream;
            public bool isCheckedValue;
            public string name;
   
            public string Name
            {
                get { return name; }
                set { name = value; }
            }
   
            public IManifestStream ManifestStream
            {
                get { return stream; }
                set { stream = value; }
            }
   
            public bool isChecked
            {
                get { return isCheckedValue; }
                set
                {
                    // mMke hello video stream always checked.
                    if (stream.Type == MediaStreamType.Video)
                    {
                        isCheckedValue = true;
                    }
                    else
                    {
                        isCheckedValue = value;
                    }
                }
            }
   
            public Stream(IManifestStream streamIn)
            {
                stream = streamIn;
                name = stream.Name;
            }
        }
        #endregion class Stream
3. Toevoegen aan het begin van de Hallo Hallo MainPage klasse, Hallo variabele definities te volgen:
   
         private List<Stream> availableStreams;
         private List<Stream> availableAudioStreams;
         private List<Stream> availableTextStreams;
         private List<Stream> availableVideoStreams;
4. Toevoegen in Hallo MainPage klasse, Hallo regio te volgen:
   
        #region stream selection
        ///<summary>
        ///Functionality tooselect streams from IManifestStream available streams
        /// </summary>
   
        // This function is called from hello mediaElement_ManifestReady event handler 
        // tooretrieve hello streams and populate them toohello local data members.
        public void getStreams(Manifest manifestObject)
        {
            availableStreams = new List<Stream>();
            availableVideoStreams = new List<Stream>();
            availableAudioStreams = new List<Stream>();
            availableTextStreams = new List<Stream>();
   
            try
            {
                for (int i = 0; i<manifestObject.AvailableStreams.Count; i++)
                {
                    Stream newStream = new Stream(manifestObject.AvailableStreams[i]);
                    newStream.isChecked = false;
   
                    //populate hello stream lists based on hello types
                    availableStreams.Add(newStream);
   
                    switch (newStream.ManifestStream.Type)
                    {
                        case MediaStreamType.Video:
                            availableVideoStreams.Add(newStream);
                            break;
                        case MediaStreamType.Audio:
                            availableAudioStreams.Add(newStream);
                            break;
                        case MediaStreamType.Text:
                            availableTextStreams.Add(newStream);
                            break;
                    }
   
                    // Select hello default selected streams from hello manifest.
                    for (int j = 0; j<manifestObject.SelectedStreams.Count; j++)
                    {
                        string selectedStreamName = manifestObject.SelectedStreams[j].Name;
                        if (selectedStreamName.Equals(newStream.Name))
                        {
                            newStream.isChecked = true;
                            break;
                        }
                    }
                }
            }
            catch (Exception e)
            {
                txtStatus.Text = "Error: " + e.Message;
            }
        }
   
        // This function set hello list box ItemSource
        private async void refreshAvailableStreamsListBoxItemSource()
        {
            try
            {
                //update hello stream check box list on hello UI
                await _dispatcher.RunAsync(CoreDispatcherPriority.Normal, ()
                    => { lbAvailableStreams.ItemsSource = availableStreams; });
            }
            catch (Exception e)
            {
                txtStatus.Text = "Error: " + e.Message;
            }
        }
   
        // This function creates a selected streams list
        private void createSelectedStreamsList(List<IManifestStream> selectedStreams)
        {
            bool isOneVideoSelected = false;
            bool isOneAudioSelected = false;
   
            // Only one video stream can be selected
            for (int j = 0; j<availableVideoStreams.Count; j++)
            {
                if (availableVideoStreams[j].isChecked && (!isOneVideoSelected))
                {
                    selectedStreams.Add(availableVideoStreams[j].ManifestStream);
                    isOneVideoSelected = true;
                }
            }
   
            // Select hello frist video stream from hello list if no video stream is selected
            if (!isOneVideoSelected)
            {
                availableVideoStreams[0].isChecked = true;
                selectedStreams.Add(availableVideoStreams[0].ManifestStream);
            }
   
            // Only one audio stream can be selected
            for (int j = 0; j<availableAudioStreams.Count; j++)
            {
                if (availableAudioStreams[j].isChecked && (!isOneAudioSelected))
                {
                    selectedStreams.Add(availableAudioStreams[j].ManifestStream);
                    isOneAudioSelected = true;
                    txtStatus.Text = "hello audio stream is changed too" + availableAudioStreams[j].ManifestStream.Name;
                }
            }
   
            // Select hello frist audio stream from hello list if no audio steam is selected.
            if (!isOneAudioSelected)
            {
                availableAudioStreams[0].isChecked = true;
                selectedStreams.Add(availableAudioStreams[0].ManifestStream);
            }
   
            // Multiple text streams are supported.
            for (int j = 0; j < availableTextStreams.Count; j++)
            {
                if (availableTextStreams[j].isChecked)
                {
                    selectedStreams.Add(availableTextStreams[j].ManifestStream);
                }
            }
        }
   
        // Change streams on a smooth streaming presentation with multiple video streams.
        private async void changeStreams(List<IManifestStream> selectStreams)
        {
            try
            {
                IReadOnlyList<IStreamChangedResult> returnArgs =
                    await manifestObject.SelectStreamsAsync(selectStreams);
            }
            catch (Exception e)
            {
                txtStatus.Text = "Error: " + e.Message;
            }
        }
        #endregion stream selection
5. Hallo mediaElement_ManifestReady methode vinden, na de code aan einde van de functie Hallo HALLO hallo toevoegen:
   
        getStreams(manifestObject);
        refreshAvailableStreamsListBoxItemSource();
   
    Dus wanneer MediaElement manifest klaar is, Hallo code wordt een lijst met beschikbare streams Hallo en vult Hallo UI-keuzelijst met Hallo lijst.
6. Zoek in de klasse MainPage Hallo, Hallo UI knoppen klikt u op gebeurtenissen regio en voeg vervolgens Hallo functiedefinitie te volgen:
   
        private void btnChangeStream_Click(object sender, RoutedEventArgs e)
        {
            List<IManifestStream> selectedStreams = new List<IManifestStream>();
   
            // Create a list of hello selected streams
            createSelectedStreamsList(selectedStreams);
   
            // Change streams on hello presentation
            changeStreams(selectedStreams);
        }

**toocompile en test Hallo-toepassing**

1. Druk op **F6** toocompile Hallo project. 
2. Druk op **F5** toorun Hallo-toepassing.
3. Bovenaan Hallo Hallo toepassing, kunt u Hallo standaard-URL voor Smooth Streaming of voer een andere. 
4. Klik op **bron instellen**. 
5. Hallo standaardtaal is audio_eng. Probeer tooswitch tussen audio_eng en audio_es. Telkens wanneer, selecteert u een nieuwe stream, klikt u op de knop verzenden Hallo.

U kunt les 3 hebt voltooid.  In deze les voegt u Hallo functionaliteit toochoose stromen.

## <a name="lesson-4-select-smooth-streaming-tracks"></a>Les 4: Selecteer nummers Smooth Streaming
Een presentatie Smooth Streaming kan meerdere videobestanden gecodeerd met verschillende kwaliteitsniveaus (bitsnelheden) en oplossingen bevatten. In deze les schakelt u gebruikers tooselect houdt. Deze les bevat Hallo procedures te volgen:

1. Hallo XAML-bestand wijzigen
2. Hallo-codebestand behand wijzigen
3. Compileren en Hallo toepassing testen

**toomodify hello XAML-bestand**

1. In Solution Explorer met de rechtermuisknop op **MainPage.xaml**, en klik vervolgens op **ontwerper**.
2. Zoek Hallo &lt;raster&gt; tag met de naam van de Hallo **gridStreamAndBitrateSelection**, Hallo volgende code achter Hallo Hallo-tag toevoegen:
   
         <StackPanel Name="spBitRateSelection" Grid.Row="1" Grid.Column="1">
         <StackPanel Orientation="Horizontal">
             <TextBlock Name="tbBitRate" Text="Available Bitrates:" FontSize="16" VerticalAlignment="Center"/>
             <Button Name="btnChangeTracks" Content="Submit" Click="btnChangeTrack_Click" />
         </StackPanel>
         <ListBox x:Name="lbAvailableVideoTracks" Height="200" Width="200" Background="Transparent" HorizontalAlignment="Left" 
                  ScrollViewer.VerticalScrollMode="Enabled" ScrollViewer.VerticalScrollBarVisibility="Visible">
             <ListBox.ItemTemplate>
                 <DataTemplate>
                     <CheckBox Content="{Binding Bitrate}" IsChecked="{Binding isChecked, Mode=TwoWay}"/>
                 </DataTemplate>
             </ListBox.ItemTemplate>
         </ListBox>
         </StackPanel>
3. Druk op **CTRL + S** toosave hij wordt gewijzigd

**toomodify hello onderliggende-codebestand**

1. In Solution Explorer met de rechtermuisknop op **MainPage.xaml**, en klik vervolgens op **weergavecode**.
2. Voeg een nieuwe klasse in Hallo SSPlayer naamruimte:
   
        #region class Track
        public class Track
        {
            private IManifestTrack trackInfo;
            public string _bitrate;
            public bool isCheckedValue;
   
            public IManifestTrack TrackInfo
            {
                get { return trackInfo; }
                set { trackInfo = value; }
            }
   
            public string Bitrate
            {
                get { return _bitrate; }
                set { _bitrate = value; }
            }
   
            public bool isChecked
            {
                get { return isCheckedValue; }
                set
                {
                    isCheckedValue = value;
                }
            }
   
            public Track(IManifestTrack trackInfoIn)
            {
                trackInfo = trackInfoIn;
                _bitrate = trackInfoIn.Bitrate.ToString();
            }
            //public Track() { }
        }
        #endregion class Track
3. Toevoegen aan het begin van de Hallo Hallo MainPage klasse, Hallo variabele definities te volgen:
   
        private List<Track> availableTracks;
4. Toevoegen in Hallo MainPage klasse, Hallo regio te volgen:
   
        #region track selection
        /// <summary>
        /// Functionality tooselect video streams
        /// </summary>
   
        /// This Function gets hello tracks for hello selected video stream
        public void getTracks(Manifest manifestObject)
        {
            availableTracks = new List<Track>();
   
            IManifestStream videoStream = getVideoStream();
            IReadOnlyList<IManifestTrack> availableTracksLocal = videoStream.AvailableTracks;
            IReadOnlyList<IManifestTrack> selectedTracksLocal = videoStream.SelectedTracks;
   
            try
            {
                for (int i = 0; i < availableTracksLocal.Count; i++)
                {
                    Track thisTrack = new Track(availableTracksLocal[i]);
                    thisTrack.isChecked = true;
   
                    for (int j = 0; j < selectedTracksLocal.Count; j++)
                    {
                        string selectedTrackName = selectedTracksLocal[j].Bitrate.ToString();
                        if (selectedTrackName.Equals(thisTrack.Bitrate))
                        {
                            thisTrack.isChecked = true;
                            break;
                        }
                    }
                    availableTracks.Add(thisTrack);
                }
            }
            catch (Exception e)
            {
                txtStatus.Text = e.Message;
            }
        }
   
        // This function gets hello video stream that is playing
        private IManifestStream getVideoStream()
        {
            IManifestStream videoStream = null;
            for (int i = 0; i < manifestObject.SelectedStreams.Count; i++)
            {
                if (manifestObject.SelectedStreams[i].Type == MediaStreamType.Video)
                {
                    videoStream = manifestObject.SelectedStreams[i];
                    break;
                }
            }
            return videoStream;
        }
   
        // This function set hello UI list box control ItemSource
        private async void refreshAvailableTracksListBoxItemSource()
        {
            try
            {
                // Update hello track check box list on hello UI 
                await _dispatcher.RunAsync(CoreDispatcherPriority.Normal, ()
                    => { lbAvailableVideoTracks.ItemsSource = availableTracks; });
            }
            catch (Exception e)
            {
                txtStatus.Text = "Error: " + e.Message;
            }        
        }
   
        // This function creates a list of hello selected tracks.
        private void createSelectedTracksList(List<IManifestTrack> selectedTracks)
        {
            // Create a list of selected tracks
            for (int j = 0; j < availableTracks.Count; j++)
            {
                if (availableTracks[j].isCheckedValue == true)
                {
                    selectedTracks.Add(availableTracks[j].TrackInfo);
                }
            }
        }
   
        // This function selects hello tracks based on user selection 
        private void changeTracks(List<IManifestTrack> selectedTracks)
        {
            IManifestStream videoStream = getVideoStream();
            try
            {
                videoStream.SelectTracks(selectedTracks);
            }
            catch (Exception ex)
            {
                txtStatus.Text = ex.Message;
            }
        }
        #endregion track selection
5. Hallo mediaElement_ManifestReady methode vinden, na de code aan einde van de functie Hallo HALLO hallo toevoegen:
   
         getTracks(manifestObject);
         refreshAvailableTracksListBoxItemSource();
6. Zoek in de klasse MainPage Hallo, Hallo UI knoppen klikt u op gebeurtenissen regio en voeg vervolgens Hallo functiedefinitie te volgen:
   
         private void btnChangeStream_Click(object sender, RoutedEventArgs e)
         {
            List<IManifestStream> selectedStreams = new List<IManifestStream>();

            // Create a list of hello selected streams
            createSelectedStreamsList(selectedStreams);

            // Change streams on hello presentation
            changeStreams(selectedStreams);
         }

**toocompile en test Hallo-toepassing**

1. Druk op **F6** toocompile Hallo project. 
2. Druk op **F5** toorun Hallo-toepassing.
3. Bovenaan Hallo Hallo toepassing, kunt u Hallo standaard-URL voor Smooth Streaming of voer een andere. 
4. Klik op **bron instellen**. 
5. Alle Hallo houdt van Hallo videostream zijn standaard geselecteerd. tooexperiment Hallo bit tarief wordt gewijzigd, kunt u selecteren Hallo laagste bitsnelheid die beschikbaar is en selecteer vervolgens Hallo hoogste bitsnelheid die beschikbaar is. U moet op verzenden klikt na elke wijziging.  U kunt Hallo videokwaliteit wijzigingen kan zien.

U kunt les 4 hebt voltooid.  In deze les voegt u Hallo functionaliteit toochoose houdt.

## <a name="media-services-learning-paths"></a>Media Services-leertrajecten
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Feedback geven
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="other-resources"></a>Andere bronnen:
* [Hoe toobuild Smooth Streaming Windows 8 JavaScript-toepassing met geavanceerde functies](http://blogs.iis.net/cenkd/archive/2012/08/10/how-to-build-a-smooth-streaming-windows-8-javascript-application-with-advanced-features.aspx)
* [Smooth Streaming technisch overzicht](http://www.iis.net/learn/media/on-demand-smooth-streaming/smooth-streaming-technical-overview)

[PlayerApplication]: ./media/media-services-build-smooth-streaming-apps/SSClientWin8-1.png
[CodeViewPic]: ./media/media-services-build-smooth-streaming-apps/SSClientWin8-2.png


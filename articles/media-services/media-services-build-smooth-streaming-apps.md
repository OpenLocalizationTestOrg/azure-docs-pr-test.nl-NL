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
# <a name="how-toobuild-a-smooth-streaming-windows-store-application"></a><span data-ttu-id="dac98-103">Hoe tooBuild een Smooth Streaming Windows Store-toepassing</span><span class="sxs-lookup"><span data-stu-id="dac98-103">How tooBuild a Smooth Streaming Windows Store Application</span></span>

<span data-ttu-id="dac98-104">Hallo Smooth Streaming Client SDK voor Windows 8 kan ontwikkelaars toobuild Windows Store-toepassingen die op aanvraag en live-Smooth Streaming inhoud kunnen spelen.</span><span class="sxs-lookup"><span data-stu-id="dac98-104">hello Smooth Streaming Client SDK for Windows 8 enables developers toobuild Windows Store applications that can play on-demand and live Smooth Streaming content.</span></span> <span data-ttu-id="dac98-105">Bovendien biedt toohello basic afspelen van Smooth Streaming-inhoud, Hallo SDK ook uitgebreide functies zoals Microsoft PlayReady protection, kwaliteit niveau beperking, DVR, audiostroom overschakelen, luisteren naar statusupdates (zoals kwaliteit niveau wijzigingen Live ) en foutgebeurtenissen, enzovoort.</span><span class="sxs-lookup"><span data-stu-id="dac98-105">In addition toohello basic playback of Smooth Streaming content, hello SDK also provides rich features like Microsoft PlayReady protection, quality level restriction, Live DVR, audio stream switching, listening for status updates (such as quality level changes) and error events, and so on.</span></span> <span data-ttu-id="dac98-106">Zie voor meer informatie van functies ondersteund Hallo Hallo [release-opmerkingen](http://www.iis.net/learn/media/smooth-streaming/smooth-streaming-client-sdk-for-windows-8-release-notes).</span><span class="sxs-lookup"><span data-stu-id="dac98-106">For more information of hello supported features, see hello [release notes](http://www.iis.net/learn/media/smooth-streaming/smooth-streaming-client-sdk-for-windows-8-release-notes).</span></span> <span data-ttu-id="dac98-107">Zie voor meer informatie [Player Framework voor Windows 8](http://playerframework.codeplex.com/).</span><span class="sxs-lookup"><span data-stu-id="dac98-107">For more information, see [Player Framework for Windows 8](http://playerframework.codeplex.com/).</span></span> 

<span data-ttu-id="dac98-108">Deze zelfstudie bevat vier uitkomsten:</span><span class="sxs-lookup"><span data-stu-id="dac98-108">This tutorial contains four lessons:</span></span>

1. <span data-ttu-id="dac98-109">Een eenvoudige Smooth Streaming Store-toepassing maken</span><span class="sxs-lookup"><span data-stu-id="dac98-109">Create a Basic Smooth Streaming Store Application</span></span>
2. <span data-ttu-id="dac98-110">Toevoegen van een schuifbalk tooControl Hallo Media uitgevoerd</span><span class="sxs-lookup"><span data-stu-id="dac98-110">Add a Slider Bar tooControl hello Media Progress</span></span>
3. <span data-ttu-id="dac98-111">Selecteer Streams Smooth Streaming</span><span class="sxs-lookup"><span data-stu-id="dac98-111">Select Smooth Streaming Streams</span></span>
4. <span data-ttu-id="dac98-112">Selecteer nummers Smooth Streaming</span><span class="sxs-lookup"><span data-stu-id="dac98-112">Select Smooth Streaming Tracks</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dac98-113">Vereisten</span><span class="sxs-lookup"><span data-stu-id="dac98-113">Prerequisites</span></span>
* <span data-ttu-id="dac98-114">Windows 8, 32-bits of 64-bits.</span><span class="sxs-lookup"><span data-stu-id="dac98-114">Windows 8 32-bit or 64-bit.</span></span> <span data-ttu-id="dac98-115">U kunt krijgen [Windows 8 Enterprise Evaluation](http://msdn.microsoft.com/evalcenter/jj554510.aspx) van MSDN.</span><span class="sxs-lookup"><span data-stu-id="dac98-115">You can get [Windows 8 Enterprise Evaluation](http://msdn.microsoft.com/evalcenter/jj554510.aspx) from MSDN.</span></span>
* <span data-ttu-id="dac98-116">Visual Studio 2012 of Visual Studio Express 2012 (of een latere versie).</span><span class="sxs-lookup"><span data-stu-id="dac98-116">Visual Studio 2012 or Visual Studio Express 2012 (or a later version).</span></span> <span data-ttu-id="dac98-117">U krijgt Hallo evaluatieversie van [hier](http://www.microsoft.com/visualstudio/11/downloads).</span><span class="sxs-lookup"><span data-stu-id="dac98-117">You can get hello trial version from [here](http://www.microsoft.com/visualstudio/11/downloads).</span></span>
* <span data-ttu-id="dac98-118">[Microsoft Smooth Streaming Client SDK voor Windows 8](http://visualstudiogallery.msdn.microsoft.com/04423d13-3b3e-4741-a01c-1ae29e84fea6?SRC=Homehttp://visualstudiogallery.msdn.microsoft.com/04423d13-3b3e-4741-a01c-1ae29e84fea6?SRC=Home).</span><span class="sxs-lookup"><span data-stu-id="dac98-118">[Microsoft Smooth Streaming Client SDK for Windows 8](http://visualstudiogallery.msdn.microsoft.com/04423d13-3b3e-4741-a01c-1ae29e84fea6?SRC=Homehttp://visualstudiogallery.msdn.microsoft.com/04423d13-3b3e-4741-a01c-1ae29e84fea6?SRC=Home).</span></span>

<span data-ttu-id="dac98-119">oplossing voor elke les Hallo voltooid kan worden gedownload van MSDN Developer-codevoorbeelden (Codegalerie):</span><span class="sxs-lookup"><span data-stu-id="dac98-119">hello completed solution for each lesson can be downloaded from MSDN Developer Code Samples (Code Gallery):</span></span> 

* <span data-ttu-id="dac98-120">[Les 1](http://code.msdn.microsoft.com/Smooth-Streaming-Client-0bb1471f) : een eenvoudige Windows 8-Smooth Streaming MediaPlayer</span><span class="sxs-lookup"><span data-stu-id="dac98-120">[Lesson 1](http://code.msdn.microsoft.com/Smooth-Streaming-Client-0bb1471f) - A Simple Windows 8 Smooth Streaming Media Player,</span></span> 
* <span data-ttu-id="dac98-121">[Les 2](http://code.msdn.microsoft.com/A-simple-Windows-8-Smooth-ee98f63a) : een eenvoudige Windows 8-Smooth Streaming MediaPlayer met een schuifregelaar beheren</span><span class="sxs-lookup"><span data-stu-id="dac98-121">[Lesson 2](http://code.msdn.microsoft.com/A-simple-Windows-8-Smooth-ee98f63a) - A Simple Windows 8 Smooth Streaming Media Player with a Slider Bar Control,</span></span> 
* <span data-ttu-id="dac98-122">[Les 3](http://code.msdn.microsoft.com/A-Windows-8-Smooth-883c3b44) - een Windows 8-Smooth Streaming MediaPlayer met Stream-selectie</span><span class="sxs-lookup"><span data-stu-id="dac98-122">[Lesson 3](http://code.msdn.microsoft.com/A-Windows-8-Smooth-883c3b44) - A Windows 8 Smooth Streaming Media Player with Stream Selection,</span></span>  
* <span data-ttu-id="dac98-123">[4 les](http://code.msdn.microsoft.com/A-Windows-8-Smooth-aa9e4907) - een Windows 8-Smooth Streaming MediaPlayer bij selectie bijhouden.</span><span class="sxs-lookup"><span data-stu-id="dac98-123">[Lesson 4](http://code.msdn.microsoft.com/A-Windows-8-Smooth-aa9e4907)  - A Windows 8 Smooth Streaming Media Player with Track Selection.</span></span>

## <a name="lesson-1-create-a-basic-smooth-streaming-store-application"></a><span data-ttu-id="dac98-124">Les 1: Een eenvoudige Smooth Streaming Store-toepassing maken</span><span class="sxs-lookup"><span data-stu-id="dac98-124">Lesson 1: Create a Basic Smooth Streaming Store Application</span></span>

<span data-ttu-id="dac98-125">In deze les maakt u een Windows Store-toepassing met een MediaElement besturingselement tooplay Smooth Stream inhoud.</span><span class="sxs-lookup"><span data-stu-id="dac98-125">In this lesson, you will create a Windows Store application with a MediaElement control tooplay Smooth Stream content.</span></span>  <span data-ttu-id="dac98-126">de actieve toepassing Hello ziet eruit als:</span><span class="sxs-lookup"><span data-stu-id="dac98-126">hello running application looks like:</span></span>

![Voorbeeld van Smooth Streaming Windows Store-toepassing][PlayerApplication]

<span data-ttu-id="dac98-128">Zie voor meer informatie over het ontwikkelen van Windows Store-toepassing [ontwikkelen geweldige Apps voor Windows 8](http://msdn.microsoft.com/windows/apps/br229512.aspx).</span><span class="sxs-lookup"><span data-stu-id="dac98-128">For more information on developing Windows Store application, see [Develop Great Apps for Windows 8](http://msdn.microsoft.com/windows/apps/br229512.aspx).</span></span> <span data-ttu-id="dac98-129">Deze les bevat Hallo procedures te volgen:</span><span class="sxs-lookup"><span data-stu-id="dac98-129">This lesson contains hello following procedures:</span></span>

1. <span data-ttu-id="dac98-130">Een Windows Store-project maken</span><span class="sxs-lookup"><span data-stu-id="dac98-130">Create a Windows Store project</span></span>
2. <span data-ttu-id="dac98-131">Hallo-gebruikersinterface (XAML) ontwerpen</span><span class="sxs-lookup"><span data-stu-id="dac98-131">Design hello user interface (XAML)</span></span>
3. <span data-ttu-id="dac98-132">Hallo onderliggende-codebestand wijzigen</span><span class="sxs-lookup"><span data-stu-id="dac98-132">Modify hello code behind file</span></span>
4. <span data-ttu-id="dac98-133">Compileren en Hallo toepassing testen</span><span class="sxs-lookup"><span data-stu-id="dac98-133">Compile and test hello application</span></span>

<span data-ttu-id="dac98-134">**toocreate Windows Store-project**</span><span class="sxs-lookup"><span data-stu-id="dac98-134">**toocreate a Windows Store project**</span></span>

1. <span data-ttu-id="dac98-135">Visual Studio 2012 of hoger wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="dac98-135">Run Visual Studio 2012 or later.</span></span>
2. <span data-ttu-id="dac98-136">Van Hallo **bestand** menu, klikt u op **nieuw**, en klik vervolgens op **Project**.</span><span class="sxs-lookup"><span data-stu-id="dac98-136">From hello **FILE** menu, click **New**, and then click **Project**.</span></span>
3. <span data-ttu-id="dac98-137">In het dialoogvenster Nieuw Project Hallo waarden type of selecteer Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="dac98-137">From hello New Project dialog, type or select  hello following values:</span></span>

| <span data-ttu-id="dac98-138">Naam</span><span class="sxs-lookup"><span data-stu-id="dac98-138">Name</span></span> | <span data-ttu-id="dac98-139">Waarde</span><span class="sxs-lookup"><span data-stu-id="dac98-139">Value</span></span> |
| --- | --- |
| <span data-ttu-id="dac98-140">Sjabloongroep</span><span class="sxs-lookup"><span data-stu-id="dac98-140">Template group</span></span> |<span data-ttu-id="dac98-141">Geïnstalleerd/sjablonen/Visual C# / van Windows Store</span><span class="sxs-lookup"><span data-stu-id="dac98-141">Installed/Templates/Visual C#/Windows Store</span></span> |
| <span data-ttu-id="dac98-142">Template</span><span class="sxs-lookup"><span data-stu-id="dac98-142">Template</span></span> |<span data-ttu-id="dac98-143">Lege App (XAML)</span><span class="sxs-lookup"><span data-stu-id="dac98-143">Blank App (XAML)</span></span> |
| <span data-ttu-id="dac98-144">Naam</span><span class="sxs-lookup"><span data-stu-id="dac98-144">Name</span></span> |<span data-ttu-id="dac98-145">SSPlayer</span><span class="sxs-lookup"><span data-stu-id="dac98-145">SSPlayer</span></span> |
| <span data-ttu-id="dac98-146">Locatie</span><span class="sxs-lookup"><span data-stu-id="dac98-146">Location</span></span> |<span data-ttu-id="dac98-147">C:\SSTutorials</span><span class="sxs-lookup"><span data-stu-id="dac98-147">C:\SSTutorials</span></span> |
| <span data-ttu-id="dac98-148">Naam van de oplossing</span><span class="sxs-lookup"><span data-stu-id="dac98-148">Solution Name</span></span> |<span data-ttu-id="dac98-149">SSPlayer</span><span class="sxs-lookup"><span data-stu-id="dac98-149">SSPlayer</span></span> |
| <span data-ttu-id="dac98-150">Map voor oplossing maken</span><span class="sxs-lookup"><span data-stu-id="dac98-150">Create directory for solution</span></span> |<span data-ttu-id="dac98-151">(geselecteerd)</span><span class="sxs-lookup"><span data-stu-id="dac98-151">(selected)</span></span> |

1. <span data-ttu-id="dac98-152">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="dac98-152">Click **OK**.</span></span>

<span data-ttu-id="dac98-153">**tooadd een verwijzing toohello Smooth Streaming Client SDK**</span><span class="sxs-lookup"><span data-stu-id="dac98-153">**tooadd a reference toohello Smooth Streaming Client SDK**</span></span>

1. <span data-ttu-id="dac98-154">In Solution Explorer met de rechtermuisknop op **SSPlayer**, en klik vervolgens op **verwijzing toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="dac98-154">From Solution Explorer, right-click **SSPlayer**, and then click **Add Reference**.</span></span>
2. <span data-ttu-id="dac98-155">Typ of selecteer Hallo volgende waarden:</span><span class="sxs-lookup"><span data-stu-id="dac98-155">Type or select hello following values:</span></span>

| <span data-ttu-id="dac98-156">Naam</span><span class="sxs-lookup"><span data-stu-id="dac98-156">Name</span></span> | <span data-ttu-id="dac98-157">Waarde</span><span class="sxs-lookup"><span data-stu-id="dac98-157">Value</span></span> |
| --- | --- |
| <span data-ttu-id="dac98-158">Referentie-groep</span><span class="sxs-lookup"><span data-stu-id="dac98-158">Reference group</span></span> |<span data-ttu-id="dac98-159">Windows-uitbreidingen</span><span class="sxs-lookup"><span data-stu-id="dac98-159">Windows/Extensions</span></span> |
| <span data-ttu-id="dac98-160">Naslaginformatie</span><span class="sxs-lookup"><span data-stu-id="dac98-160">Reference</span></span> |<span data-ttu-id="dac98-161">Selecteer Microsoft Smooth Streaming Client SDK voor Windows 8 en Microsoft Visual C++ Runtime-pakket</span><span class="sxs-lookup"><span data-stu-id="dac98-161">Select Microsoft Smooth Streaming Client SDK for Windows 8 and Microsoft Visual C++ Runtime Package</span></span> |

1. <span data-ttu-id="dac98-162">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="dac98-162">Click **OK**.</span></span> 

<span data-ttu-id="dac98-163">Na het toevoegen van Hallo verwijzingen u Hallo gericht platform (x64 of x86) moet selecteren, toe te voegen verwijzingen werkt niet voor platformconfiguratie Any CPU.</span><span class="sxs-lookup"><span data-stu-id="dac98-163">After adding hello references, you must select hello targeted platform (x64 or x86), adding references will not work for Any CPU platform configuration.</span></span>  <span data-ttu-id="dac98-164">Klik in solution explorer ziet u gele waarschuwing is ingeschakeld voor deze referenties toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="dac98-164">In solution explorer, you will see yellow warning mark for these added references.</span></span>

<span data-ttu-id="dac98-165">**toodesign hello player-gebruikersinterface**</span><span class="sxs-lookup"><span data-stu-id="dac98-165">**toodesign hello player user interface**</span></span>

1. <span data-ttu-id="dac98-166">Klik in Solution Explorer, dubbelklik op **MainPage.xaml** tooopen in Hallo ontwerp weergeven.</span><span class="sxs-lookup"><span data-stu-id="dac98-166">From Solution Explorer, double click **MainPage.xaml** tooopen it in hello design view.</span></span>
2. <span data-ttu-id="dac98-167">Zoek Hallo  **&lt;raster&gt;**  en  **&lt;/Grid&gt;**  labels Hallo XAML-bestand en plakken Hallo volgende code tussen de twee Hallo tags:</span><span class="sxs-lookup"><span data-stu-id="dac98-167">Locate hello **&lt;Grid&gt;** and **&lt;/Grid&gt;**  tags hello XAML file, and paste hello following code between hello two tags:</span></span>

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
   
   <span data-ttu-id="dac98-168">Hallo MediaElement besturingselement is gebruikte tooplayback media.</span><span class="sxs-lookup"><span data-stu-id="dac98-168">hello MediaElement control is used tooplayback media.</span></span> <span data-ttu-id="dac98-169">Hallo schuifregelaars met de naam sliderProgress wordt Hallo volgende les toocontrol Hallo media uitgevoerd gebruikt.</span><span class="sxs-lookup"><span data-stu-id="dac98-169">hello slider control named sliderProgress will be used in hello next lesson toocontrol hello media progress.</span></span>
3. <span data-ttu-id="dac98-170">Druk op **CTRL + S** toosave Hallo-bestand.</span><span class="sxs-lookup"><span data-stu-id="dac98-170">Press **CTRL+S** toosave hello file.</span></span>

<span data-ttu-id="dac98-171">Hallo MediaElement beheer biedt geen ondersteuning voor Smooth Streaming inhoud out-of-box.</span><span class="sxs-lookup"><span data-stu-id="dac98-171">hello MediaElement control does not support Smooth Streaming content out-of-box.</span></span> <span data-ttu-id="dac98-172">ondersteuning van tooenable Hallo-Smooth Streaming, moet u Hallo Smooth Streaming bytestream handler door bestandsnaamextensie en een MIME-type registreren.</span><span class="sxs-lookup"><span data-stu-id="dac98-172">tooenable hello Smooth Streaming support, you must register hello Smooth Streaming byte-stream handler by file name extension and MIME type.</span></span>  <span data-ttu-id="dac98-173">tooregister, gebruikt u Hallo MediaExtensionManager.RegisterByteStremHandler hello Windows.Media naamruimte.</span><span class="sxs-lookup"><span data-stu-id="dac98-173">tooregister, you use hello MediaExtensionManager.RegisterByteStremHandler method of hello Windows.Media namespace.</span></span>

<span data-ttu-id="dac98-174">In dit XAML-bestand zijn sommige gebeurtenis-handlers gekoppeld aan Hallo besturingselementen.</span><span class="sxs-lookup"><span data-stu-id="dac98-174">In this XAML file, some event handlers are associated with hello controls.</span></span>  <span data-ttu-id="dac98-175">U moet deze gebeurtenis-handlers definiëren.</span><span class="sxs-lookup"><span data-stu-id="dac98-175">You must define those event handlers.</span></span>

<span data-ttu-id="dac98-176">**toomodify hello onderliggende-codebestand**</span><span class="sxs-lookup"><span data-stu-id="dac98-176">**toomodify hello code behind file**</span></span>

1. <span data-ttu-id="dac98-177">In Solution Explorer met de rechtermuisknop op **MainPage.xaml**, en klik vervolgens op **weergavecode**.</span><span class="sxs-lookup"><span data-stu-id="dac98-177">From Solution Explorer, right-click **MainPage.xaml**, and then click **View Code**.</span></span>
2. <span data-ttu-id="dac98-178">Bovenaan Hallo Hallo-bestand, voegt u de volgende Hallo toe met de instructie:</span><span class="sxs-lookup"><span data-stu-id="dac98-178">At hello top of hello file, add hello following using statement:</span></span>
   
        using Windows.Media;
3. <span data-ttu-id="dac98-179">Aan begin Hallo Hallo **MainPage** klasse, Hallo gegevenslid volgende toevoegen:</span><span class="sxs-lookup"><span data-stu-id="dac98-179">At hello beginning of hello **MainPage** class, add hello following data member:</span></span>
   
         private MediaExtensionManager extensions = new MediaExtensionManager();
4. <span data-ttu-id="dac98-180">Achter Hallo Hallo **MainPage** constructor Hallo volgende twee regels toevoegen:</span><span class="sxs-lookup"><span data-stu-id="dac98-180">At hello end of hello **MainPage** constructor, add hello following two lines:</span></span>
   
        extensions.RegisterByteStreamHandler("Microsoft.Media.AdaptiveStreaming.SmoothByteStreamHandler", ".ism", "text/xml");
        extensions.RegisterByteStreamHandler("Microsoft.Media.AdaptiveStreaming.SmoothByteStreamHandler", ".ism", "application/vnd.ms-sstr+xml");
5. <span data-ttu-id="dac98-181">Achter Hallo Hallo **MainPage** klasse, plak Hallo code te volgen:</span><span class="sxs-lookup"><span data-stu-id="dac98-181">At hello end of hello **MainPage** class, paste hello following code:</span></span>
   
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

<span data-ttu-id="dac98-182">Hallo sliderProgress_PointerPressed gebeurtenis-handler wordt hier gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="dac98-182">hello sliderProgress_PointerPressed event handler is defined here.</span></span>  <span data-ttu-id="dac98-183">Er zijn meer works toodo tooget Hiermee aan de slag, die worden behandeld in de volgende les Hallo van deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="dac98-183">There are more works toodo tooget it working, which will be covered in hello next lesson of this tutorial.</span></span>
6. <span data-ttu-id="dac98-184">Druk op **CTRL + S** toosave Hallo-bestand.</span><span class="sxs-lookup"><span data-stu-id="dac98-184">Press **CTRL+S** toosave hello file.</span></span>

<span data-ttu-id="dac98-185">Hallo moet klaar Hallo onderliggende-codebestand uitzien:</span><span class="sxs-lookup"><span data-stu-id="dac98-185">hello finished hello code behind file shall look like this:</span></span>

![CodeView in Visual Studio of Smooth Streaming Windows Store-toepassing][CodeViewPic]

<span data-ttu-id="dac98-187">**toocompile en test Hallo-toepassing**</span><span class="sxs-lookup"><span data-stu-id="dac98-187">**toocompile and test hello application**</span></span>

1. <span data-ttu-id="dac98-188">Van Hallo **bouwen** menu, klikt u op **Configuration Manager**.</span><span class="sxs-lookup"><span data-stu-id="dac98-188">From hello **BUILD** menu, click **Configuration Manager**.</span></span>
2. <span data-ttu-id="dac98-189">Wijziging **actieve oplossing platform** toomatch uw ontwikkelplatform.</span><span class="sxs-lookup"><span data-stu-id="dac98-189">Change **Active solution platform** toomatch your development platform.</span></span>
3. <span data-ttu-id="dac98-190">Druk op **F6** toocompile Hallo project.</span><span class="sxs-lookup"><span data-stu-id="dac98-190">Press **F6** toocompile hello project.</span></span> 
4. <span data-ttu-id="dac98-191">Druk op **F5** toorun Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="dac98-191">Press **F5** toorun hello application.</span></span>
5. <span data-ttu-id="dac98-192">Bovenaan Hallo Hallo toepassing, kunt u Hallo standaard-URL voor Smooth Streaming of voer een andere.</span><span class="sxs-lookup"><span data-stu-id="dac98-192">At hello top of hello application, you can either use hello default Smooth Streaming URL or enter a different one.</span></span> 
6. <span data-ttu-id="dac98-193">Klik op **bron instellen**.</span><span class="sxs-lookup"><span data-stu-id="dac98-193">Click **Set Source**.</span></span> <span data-ttu-id="dac98-194">Omdat **automatisch afspelen** is standaard hello wordt afgespeeld automatisch ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="dac98-194">Because **Auto Play** is enabled by default, hello media shall play automatically.</span></span>  <span data-ttu-id="dac98-195">U kunt beheren met Hallo Hallo-media **afspelen**, **onderbreken** en **stoppen** knoppen.</span><span class="sxs-lookup"><span data-stu-id="dac98-195">You can control hello media using hello **Play**, **Pause** and **Stop** buttons.</span></span>  <span data-ttu-id="dac98-196">U kunt Hallo Mediavolume met verticale schuifbalk Hallo beheren.</span><span class="sxs-lookup"><span data-stu-id="dac98-196">You can control hello media volume using hello vertical slider.</span></span>  <span data-ttu-id="dac98-197">Hallo echter horizontale schuifbalk voor het beheren van Hallo media uitgevoerd is volledig nog niet geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="dac98-197">However hello horizontal slider for controlling hello media progress is not fully implemented yet.</span></span> 

<span data-ttu-id="dac98-198">U kunt lesson1 hebt voltooid.</span><span class="sxs-lookup"><span data-stu-id="dac98-198">You have completed lesson1.</span></span>  <span data-ttu-id="dac98-199">In deze les gebruikt u een MediaElement besturingselement tooplayback Smooth Streaming-inhoud.</span><span class="sxs-lookup"><span data-stu-id="dac98-199">In this lesson, you use a MediaElement control tooplayback Smooth Streaming content.</span></span>  <span data-ttu-id="dac98-200">In de volgende les hello, moet u een schuifregelaar toocontrol Hallo voortgang Hallo Smooth Streaming inhoud toevoegen.</span><span class="sxs-lookup"><span data-stu-id="dac98-200">In hello next lesson, you will add a slider toocontrol hello progress of hello Smooth Streaming content.</span></span>

## <a name="lesson-2-add-a-slider-bar-toocontrol-hello-media-progress"></a><span data-ttu-id="dac98-201">Les 2: Een schuifbalk tooControl Hallo Media uitgevoerd toevoegen</span><span class="sxs-lookup"><span data-stu-id="dac98-201">Lesson 2: Add a Slider Bar tooControl hello Media Progress</span></span>

<span data-ttu-id="dac98-202">In les 1, kunt u een Windows Store-servicetoepassing gemaakt met een MediaElement XAML besturingselement tooplayback Smooth Streaming media-inhoud.</span><span class="sxs-lookup"><span data-stu-id="dac98-202">In lesson 1, you created a Windows Store application with a MediaElement XAML control tooplayback Smooth Streaming media content.</span></span>  <span data-ttu-id="dac98-203">Sommige functies basic media zoals starten, stoppen en onderbreken wordt geleverd.</span><span class="sxs-lookup"><span data-stu-id="dac98-203">It comes some basic media functions like start, stop and pause.</span></span>  <span data-ttu-id="dac98-204">In deze les, moet u een schuifregelaar balk besturingselement toohello toepassing toevoegen.</span><span class="sxs-lookup"><span data-stu-id="dac98-204">In this lesson, you will add a slider bar control toohello application.</span></span>

<span data-ttu-id="dac98-205">In deze zelfstudie gebruiken we een timer tooupdate Hallo positie van de schuifregelaar op basis van de huidige positie Hallo Hallo MediaElement besturingselement.</span><span class="sxs-lookup"><span data-stu-id="dac98-205">In this tutorial, we will use a timer tooupdate hello slider position based on hello current position of hello MediaElement control.</span></span>  <span data-ttu-id="dac98-206">Hallo schuifregelaar start- en eindtijd ook nodig toobe bijgewerkt in geval van een live-inhoud.</span><span class="sxs-lookup"><span data-stu-id="dac98-206">hello slider start and end time also need toobe updated in case of live content.</span></span>  <span data-ttu-id="dac98-207">Dit kan beter worden verwerkt in Hallo adaptieve bron update gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="dac98-207">This can be better handled in hello adaptive source update event.</span></span>

<span data-ttu-id="dac98-208">Mediabronnen zijn objecten die mediagegevens genereren.</span><span class="sxs-lookup"><span data-stu-id="dac98-208">Media sources are objects that generate media data.</span></span>  <span data-ttu-id="dac98-209">Hallo voor de bronoplossing een URL of byte-stroom accepteert en maakt Hallo juiste mediumbron voor die inhoud.</span><span class="sxs-lookup"><span data-stu-id="dac98-209">hello source resolver takes a URL or byte stream and creates hello appropriate media source for that content.</span></span>  <span data-ttu-id="dac98-210">Hallo voor de bronoplossing is standaard manier Hallo toepassingen toocreate mediabronnen Hallo.</span><span class="sxs-lookup"><span data-stu-id="dac98-210">hello source resolver is hello standard way for hello applications toocreate media sources.</span></span> 

<span data-ttu-id="dac98-211">Deze les bevat Hallo procedures te volgen:</span><span class="sxs-lookup"><span data-stu-id="dac98-211">This lesson contains hello following procedures:</span></span>

1. <span data-ttu-id="dac98-212">Hallo Smooth Streaming-handler registreren</span><span class="sxs-lookup"><span data-stu-id="dac98-212">Register hello Smooth Streaming handler</span></span> 
2. <span data-ttu-id="dac98-213">Hallo adaptieve bron manager niveau gebeurtenis-handlers toevoegen</span><span class="sxs-lookup"><span data-stu-id="dac98-213">Add hello adaptive source manager level event handlers</span></span>
3. <span data-ttu-id="dac98-214">Hallo adaptieve bron niveau gebeurtenis-handlers toevoegen</span><span class="sxs-lookup"><span data-stu-id="dac98-214">Add hello adaptive source level event handlers</span></span>
4. <span data-ttu-id="dac98-215">Gebeurtenis-handlers MediaElement toevoegen</span><span class="sxs-lookup"><span data-stu-id="dac98-215">Add MediaElement event handlers</span></span>
5. <span data-ttu-id="dac98-216">Schuifregelaar gerelateerde code toevoegen</span><span class="sxs-lookup"><span data-stu-id="dac98-216">Add slider bar related code</span></span>
6. <span data-ttu-id="dac98-217">Compileren en Hallo toepassing testen</span><span class="sxs-lookup"><span data-stu-id="dac98-217">Compile and test hello application</span></span>

<span data-ttu-id="dac98-218">**tooregister hello Smooth Streaming bytestream handler en pass Hallo propertyset**</span><span class="sxs-lookup"><span data-stu-id="dac98-218">**tooregister hello Smooth Streaming byte-stream handler and pass hello propertyset**</span></span>

1. <span data-ttu-id="dac98-219">In Solution Explorer met de rechtermuisknop op **MainPage.xaml**, en klik vervolgens op **weergavecode**.</span><span class="sxs-lookup"><span data-stu-id="dac98-219">From Solution Explorer, right click **MainPage.xaml**, and then click **View Code**.</span></span>
2. <span data-ttu-id="dac98-220">Aan het begin van de Hallo van Hallo-bestand, voegt u de volgende Hallo toe met de instructie:</span><span class="sxs-lookup"><span data-stu-id="dac98-220">At hello beginning of hello file, add hello following using statement:</span></span>

        using Microsoft.Media.AdaptiveStreaming;
3. <span data-ttu-id="dac98-221">Toevoegen aan het begin van de Hallo Hallo MainPage klasse, Hallo gegevensleden te volgen:</span><span class="sxs-lookup"><span data-stu-id="dac98-221">At hello beginning of hello MainPage class, add hello following data members:</span></span>

         private Windows.Foundation.Collections.PropertySet propertySet = new Windows.Foundation.Collections.PropertySet();             
         private IAdaptiveSourceManager adaptiveSourceManager;
4. <span data-ttu-id="dac98-222">Hallo binnen **MainPage** constructor toevoegen na code na Hallo Hallo **dit. Initialiseren van Components();**  regel en Hallo registratie coderegels in de vorige les Hallo geschreven:</span><span class="sxs-lookup"><span data-stu-id="dac98-222">Inside hello **MainPage** constructor, add hello following code after hello **this.Initialize Components();** line and hello registration code lines written in hello previous lesson:</span></span>

        // Gets hello default instance of AdaptiveSourceManager which manages Smooth 
        //Streaming media sources.
        adaptiveSourceManager = AdaptiveSourceManager.GetDefault();
        // Sets property key value tooAdaptiveSourceManager default instance.
        // {A5CE1DE8-1D00-427B-ACEF-FB9A3C93DE2D}" must be hardcoded.
        propertySet["{A5CE1DE8-1D00-427B-ACEF-FB9A3C93DE2D}"] = adaptiveSourceManager;
5. <span data-ttu-id="dac98-223">Hallo binnen **MainPage** -constructor aan, wijzig Hallo twee RegisterByteStreamHandler methoden tooadd Hallo beschreven parameters:</span><span class="sxs-lookup"><span data-stu-id="dac98-223">Inside hello **MainPage** constructor, modify hello two RegisterByteStreamHandler methods tooadd hello forth parameters:</span></span>

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
6. <span data-ttu-id="dac98-224">Druk op **CTRL + S** toosave Hallo-bestand.</span><span class="sxs-lookup"><span data-stu-id="dac98-224">Press **CTRL+S** toosave hello file.</span></span>

<span data-ttu-id="dac98-225">**tooadd hello adaptieve bron manager niveau gebeurtenis-handler**</span><span class="sxs-lookup"><span data-stu-id="dac98-225">**tooadd hello adaptive source manager level event handler**</span></span>

1. <span data-ttu-id="dac98-226">In Solution Explorer met de rechtermuisknop op **MainPage.xaml**, en klik vervolgens op **weergavecode**.</span><span class="sxs-lookup"><span data-stu-id="dac98-226">From Solution Explorer, right click **MainPage.xaml**, and then click **View Code**.</span></span>
2. <span data-ttu-id="dac98-227">Hallo binnen **MainPage** klasse, Hallo gegevenslid volgende toevoegen:</span><span class="sxs-lookup"><span data-stu-id="dac98-227">Inside hello **MainPage** class, add hello following data member:</span></span>
   
     <span data-ttu-id="dac98-228">persoonlijke AdaptiveSource adaptiveSource = null;</span><span class="sxs-lookup"><span data-stu-id="dac98-228">private AdaptiveSource adaptiveSource = null;</span></span>
3. <span data-ttu-id="dac98-229">Achter Hallo Hallo **MainPage** klasse, Hallo volgende gebeurtenis-handler toevoegen:</span><span class="sxs-lookup"><span data-stu-id="dac98-229">At hello end of hello **MainPage** class, add hello following event handler:</span></span>
   
         # region Adaptive Source Manager Level Events
         private void mediaElement_AdaptiveSourceOpened(AdaptiveSource sender, AdaptiveSourceOpenedEventArgs args)
         {

            adaptiveSource = args.AdaptiveSource;
         }

         # endregion Adaptive Source Manager Level Events
4. <span data-ttu-id="dac98-230">Achter Hallo Hallo **MainPage** constructor toevoegen Hallo regel toosubscribe toohello adaptieve bron open gebeurtenis te volgen:</span><span class="sxs-lookup"><span data-stu-id="dac98-230">At hello end of hello **MainPage** constructor, add hello following line toosubscribe toohello adaptive source open event:</span></span>
   
         adaptiveSourceManager.AdaptiveSourceOpenedEvent += 
           new AdaptiveSourceOpenedEventHandler(mediaElement_AdaptiveSourceOpened);
5. <span data-ttu-id="dac98-231">Druk op **CTRL + S** toosave Hallo-bestand.</span><span class="sxs-lookup"><span data-stu-id="dac98-231">Press **CTRL+S** toosave hello file.</span></span>

<span data-ttu-id="dac98-232">**tooadd adaptieve bron niveau gebeurtenis-handlers**</span><span class="sxs-lookup"><span data-stu-id="dac98-232">**tooadd adaptive source level event handlers**</span></span>

1. <span data-ttu-id="dac98-233">In Solution Explorer met de rechtermuisknop op **MainPage.xaml**, en klik vervolgens op **weergavecode**.</span><span class="sxs-lookup"><span data-stu-id="dac98-233">From Solution Explorer, right click **MainPage.xaml**, and then click **View Code**.</span></span>
2. <span data-ttu-id="dac98-234">Hallo binnen **MainPage** klasse, Hallo gegevenslid volgende toevoegen:</span><span class="sxs-lookup"><span data-stu-id="dac98-234">Inside hello **MainPage** class, add hello following data member:</span></span>
   
     <span data-ttu-id="dac98-235">persoonlijke AdaptiveSourceStatusUpdatedEventArgs adaptiveSourceStatusUpdate;   persoonlijke Manifest manifestObject;</span><span class="sxs-lookup"><span data-stu-id="dac98-235">private AdaptiveSourceStatusUpdatedEventArgs adaptiveSourceStatusUpdate;   private Manifest manifestObject;</span></span>
3. <span data-ttu-id="dac98-236">Achter Hallo Hallo **MainPage** klasse, Hallo volgende gebeurtenis-handlers toevoegen:</span><span class="sxs-lookup"><span data-stu-id="dac98-236">At hello end of hello **MainPage** class, add hello following event handlers:</span></span>

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
4. <span data-ttu-id="dac98-237">Achter Hallo Hallo **mediaElement AdaptiveSourceOpened** methode toevoegen Hallo code toosubscribe toohello gebeurtenissen te volgen:</span><span class="sxs-lookup"><span data-stu-id="dac98-237">At hello end of hello **mediaElement AdaptiveSourceOpened** method, add hello following code toosubscribe toohello events:</span></span>
   
         adaptiveSource.ManifestReadyEvent +=

                    mediaElement_ManifestReady;
         adaptiveSource.AdaptiveSourceStatusUpdatedEvent += 

            mediaElement_AdaptiveSourceStatusUpdated;
         adaptiveSource.AdaptiveSourceFailedEvent += 

            mediaElement_AdaptiveSourceFailed;
5. <span data-ttu-id="dac98-238">Druk op **CTRL + S** toosave Hallo-bestand.</span><span class="sxs-lookup"><span data-stu-id="dac98-238">Press **CTRL+S** toosave hello file.</span></span>

<span data-ttu-id="dac98-239">Hallo dezelfde gebeurtenissen voor adaptieve bron Manager niveau, die kan worden gebruikt voor het verwerken van functionaliteit tooall media standaardelementen in Hallo-app beschikbaar zijn.</span><span class="sxs-lookup"><span data-stu-id="dac98-239">hello same events are available on Adaptive Source manger level as well, which can be used for handling functionality common tooall media elements in hello app.</span></span> <span data-ttu-id="dac98-240">Elke AdaptiveSource omvat zijn eigen gebeurtenissen en worden alle gebeurtenissen voor AdaptiveSource trapsgewijs onder AdaptiveSourceManager.</span><span class="sxs-lookup"><span data-stu-id="dac98-240">Each AdaptiveSource includes its own events and all AdaptiveSource events will be cascaded under AdaptiveSourceManager.</span></span>

<span data-ttu-id="dac98-241">**gebeurtenis-handlers voor tooadd Media-Element**</span><span class="sxs-lookup"><span data-stu-id="dac98-241">**tooadd Media Element event handlers**</span></span>

1. <span data-ttu-id="dac98-242">In Solution Explorer met de rechtermuisknop op **MainPage.xaml**, en klik vervolgens op **weergavecode**.</span><span class="sxs-lookup"><span data-stu-id="dac98-242">From Solution Explorer, right click **MainPage.xaml**, and then click **View Code**.</span></span>
2. <span data-ttu-id="dac98-243">Achter Hallo Hallo **MainPage** klasse, Hallo volgende gebeurtenis-handlers toevoegen:</span><span class="sxs-lookup"><span data-stu-id="dac98-243">At hello end of hello **MainPage** class, add hello following event handlers:</span></span>

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
3. <span data-ttu-id="dac98-244">Achter Hallo Hallo **MainPage** constructor toevoegen Hallo code toosubscript toohello gebeurtenissen te volgen:</span><span class="sxs-lookup"><span data-stu-id="dac98-244">At hello end of hello **MainPage** constructor, add hello following code toosubscript toohello events:</span></span>

         mediaElement.MediaOpened += MediaOpened;
         mediaElement.MediaEnded += MediaEnded;
         mediaElement.MediaFailed += MediaFailed;
4. <span data-ttu-id="dac98-245">Druk op **CTRL + S** toosave Hallo-bestand.</span><span class="sxs-lookup"><span data-stu-id="dac98-245">Press **CTRL+S** toosave hello file.</span></span>

<span data-ttu-id="dac98-246">**de schuifregelaar tooadd gerelateerde streepjescode**</span><span class="sxs-lookup"><span data-stu-id="dac98-246">**tooadd slider bar related code**</span></span>

1. <span data-ttu-id="dac98-247">In Solution Explorer met de rechtermuisknop op **MainPage.xaml**, en klik vervolgens op **weergavecode**.</span><span class="sxs-lookup"><span data-stu-id="dac98-247">From Solution Explorer, right click **MainPage.xaml**, and then click **View Code**.</span></span>
2. <span data-ttu-id="dac98-248">Aan het begin van de Hallo van Hallo-bestand, voegt u de volgende Hallo toe met de instructie:</span><span class="sxs-lookup"><span data-stu-id="dac98-248">At hello beginning of hello file, add hello following using statement:</span></span>
      
        using Windows.UI.Core;
3. <span data-ttu-id="dac98-249">Hallo binnen **MainPage** klasse, Hallo volgende gegevensleden toe te voegen:</span><span class="sxs-lookup"><span data-stu-id="dac98-249">Inside hello **MainPage** class, add hello following data members:</span></span>
   
         public static CoreDispatcher _dispatcher;
         private DispatcherTimer sliderPositionUpdateDispatcher;
4. <span data-ttu-id="dac98-250">Achter Hallo Hallo **MainPage** constructor Hallo na code toevoegen:</span><span class="sxs-lookup"><span data-stu-id="dac98-250">At hello end of hello **MainPage** constructor, add hello following code:</span></span>
   
         _dispatcher = Window.Current.Dispatcher;
         PointerEventHandler pointerpressedhandler = new PointerEventHandler(sliderProgress_PointerPressed);
         sliderProgress.AddHandler(Control.PointerPressedEvent, pointerpressedhandler, true);    
5. <span data-ttu-id="dac98-251">Achter Hallo Hallo **MainPage** klasse, Hallo volgende code toe te voegen:</span><span class="sxs-lookup"><span data-stu-id="dac98-251">At hello end of hello **MainPage** class, add hello following code:</span></span>

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
><span data-ttu-id="dac98-252">CoreDispatcher is gebruikte toomake wijzigingen toohello UI-thread van niet-UI-Thread.</span><span class="sxs-lookup"><span data-stu-id="dac98-252">CoreDispatcher is used toomake changes toohello UI thread from non UI Thread.</span></span> <span data-ttu-id="dac98-253">In geval van een knelpunt op dispatcher-thread kunt developer toouse dispatcher geleverd door UI-element dat hij wil tooupdate.</span><span class="sxs-lookup"><span data-stu-id="dac98-253">In case of bottleneck on dispatcher thread, developer can choose toouse dispatcher provided by UI-element he/she intends tooupdate.</span></span>  <span data-ttu-id="dac98-254">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="dac98-254">For example:</span></span>
   
         await sliderProgress.Dispatcher.RunAsync(CoreDispatcherPriority.Normal, () => { TimeSpan 

         timespan = new TimeSpan(adaptiveSourceStatusUpdate.EndTime); 
         double absvalue  = (int)Math.Round(timespan.TotalSeconds, MidpointRounding.AwayFromZero); 

         sliderProgress.Maximum = absvalue; }); 
6. <span data-ttu-id="dac98-255">Achter Hallo Hallo **mediaElement_AdaptiveSourceStatusUpdated** methode Hallo na code toevoegen:</span><span class="sxs-lookup"><span data-stu-id="dac98-255">At hello end of hello **mediaElement_AdaptiveSourceStatusUpdated** method, add hello following code:</span></span>

         setSliderStartTime(args.StartTime);
         setSliderEndTime(args.EndTime);
7. <span data-ttu-id="dac98-256">Achter Hallo Hallo **MediaOpened** methode Hallo na code toevoegen:</span><span class="sxs-lookup"><span data-stu-id="dac98-256">At hello end of hello **MediaOpened** method, add hello following code:</span></span>

         sliderProgress.StepFrequency = SliderFrequency(mediaElement.NaturalDuration.TimeSpan);
         sliderProgress.Width = mediaElement.Width;
         setupTimer();
8. <span data-ttu-id="dac98-257">Druk op **CTRL + S** toosave Hallo-bestand.</span><span class="sxs-lookup"><span data-stu-id="dac98-257">Press **CTRL+S** toosave hello file.</span></span>

<span data-ttu-id="dac98-258">**toocompile en test Hallo-toepassing**</span><span class="sxs-lookup"><span data-stu-id="dac98-258">**toocompile and test hello application**</span></span>

1. <span data-ttu-id="dac98-259">Druk op **F6** toocompile Hallo project.</span><span class="sxs-lookup"><span data-stu-id="dac98-259">Press **F6** toocompile hello project.</span></span> 
2. <span data-ttu-id="dac98-260">Druk op **F5** toorun Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="dac98-260">Press **F5** toorun hello application.</span></span>
3. <span data-ttu-id="dac98-261">Bovenaan Hallo Hallo toepassing, kunt u Hallo standaard-URL voor Smooth Streaming of voer een andere.</span><span class="sxs-lookup"><span data-stu-id="dac98-261">At hello top of hello application, you can either use hello default Smooth Streaming URL or enter a different one.</span></span> 
4. <span data-ttu-id="dac98-262">Klik op **bron instellen**.</span><span class="sxs-lookup"><span data-stu-id="dac98-262">Click **Set Source**.</span></span> 
5. <span data-ttu-id="dac98-263">Test Hallo schuifregelaar.</span><span class="sxs-lookup"><span data-stu-id="dac98-263">Test hello slider bar.</span></span>

<span data-ttu-id="dac98-264">U kunt les 2 hebt voltooid.</span><span class="sxs-lookup"><span data-stu-id="dac98-264">You have completed lesson 2.</span></span>  <span data-ttu-id="dac98-265">In deze les moet u een schuifregelaar tooapplication toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="dac98-265">In this lesson you added a slider tooapplication.</span></span> 

## <a name="lesson-3-select-smooth-streaming-streams"></a><span data-ttu-id="dac98-266">Les 3: Selecteer Streams Smooth Streaming</span><span class="sxs-lookup"><span data-stu-id="dac98-266">Lesson 3: Select Smooth Streaming Streams</span></span>
<span data-ttu-id="dac98-267">Smooth Streaming is geschikt toostream inhoud met meerdere taal audio nummers die kunnen geselecteerd door Hallo viewers worden.</span><span class="sxs-lookup"><span data-stu-id="dac98-267">Smooth Streaming is capable toostream content with multiple language audio tracks that are selectable by hello viewers.</span></span>  <span data-ttu-id="dac98-268">In deze les schakelt u viewers tooselect stromen.</span><span class="sxs-lookup"><span data-stu-id="dac98-268">In this lesson, you will enable viewers tooselect streams.</span></span> <span data-ttu-id="dac98-269">Deze les bevat Hallo procedures te volgen:</span><span class="sxs-lookup"><span data-stu-id="dac98-269">This lesson contains hello following procedures:</span></span>

1. <span data-ttu-id="dac98-270">Hallo XAML-bestand wijzigen</span><span class="sxs-lookup"><span data-stu-id="dac98-270">Modify hello XAML file</span></span>
2. <span data-ttu-id="dac98-271">Hallo-codebestand behand wijzigen</span><span class="sxs-lookup"><span data-stu-id="dac98-271">Modify hello code behand file</span></span>
3. <span data-ttu-id="dac98-272">Compileren en Hallo toepassing testen</span><span class="sxs-lookup"><span data-stu-id="dac98-272">Compile and test hello application</span></span>

<span data-ttu-id="dac98-273">**toomodify hello XAML-bestand**</span><span class="sxs-lookup"><span data-stu-id="dac98-273">**toomodify hello XAML file**</span></span>

1. <span data-ttu-id="dac98-274">In Solution Explorer met de rechtermuisknop op **MainPage.xaml**, en klik vervolgens op **ontwerper**.</span><span class="sxs-lookup"><span data-stu-id="dac98-274">From Solution Explorer, right-click **MainPage.xaml**, and then click **View Designer**.</span></span>
2. <span data-ttu-id="dac98-275">Zoek &lt;Grid.RowDefinitions&gt;, en wijzig Hallo RowDefinitions zodat ze eruitzien:</span><span class="sxs-lookup"><span data-stu-id="dac98-275">Locate &lt;Grid.RowDefinitions&gt;, and modify hello RowDefinitions so they looks like:</span></span>
   
         <Grid.RowDefinitions>            
            <RowDefinition Height="20"/>
            <RowDefinition Height="50"/>
            <RowDefinition Height="100"/>
            <RowDefinition Height="80"/>
            <RowDefinition Height="50"/>
         </Grid.RowDefinitions>
3. <span data-ttu-id="dac98-276">Hallo binnen &lt;raster&gt;&lt;/Grid&gt; tags toevoegen Hallo volgende code toodefine een keuzelijst, zodat gebruikers kunnen Hallo van de beschikbare stromen overzicht en streams selecteren:</span><span class="sxs-lookup"><span data-stu-id="dac98-276">Inside hello &lt;Grid&gt;&lt;/Grid&gt; tags, add hello following code toodefine a listbox control, so users can see hello list of available streams, and select streams:</span></span>

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
4. <span data-ttu-id="dac98-277">Druk op **CTRL + S** toosave Hallo wijzigingen.</span><span class="sxs-lookup"><span data-stu-id="dac98-277">Press **CTRL+S** toosave hello changes.</span></span>

<span data-ttu-id="dac98-278">**toomodify hello onderliggende-codebestand**</span><span class="sxs-lookup"><span data-stu-id="dac98-278">**toomodify hello code behind file**</span></span>

1. <span data-ttu-id="dac98-279">In Solution Explorer met de rechtermuisknop op **MainPage.xaml**, en klik vervolgens op **weergavecode**.</span><span class="sxs-lookup"><span data-stu-id="dac98-279">From Solution Explorer, right-click **MainPage.xaml**, and then click **View Code**.</span></span>
2. <span data-ttu-id="dac98-280">Voeg een nieuwe klasse in Hallo SSPlayer naamruimte:</span><span class="sxs-lookup"><span data-stu-id="dac98-280">Inside hello SSPlayer namespace, add a new class:</span></span>
   
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
3. <span data-ttu-id="dac98-281">Toevoegen aan het begin van de Hallo Hallo MainPage klasse, Hallo variabele definities te volgen:</span><span class="sxs-lookup"><span data-stu-id="dac98-281">At hello beginning of hello MainPage class, add hello following variable definitions:</span></span>
   
         private List<Stream> availableStreams;
         private List<Stream> availableAudioStreams;
         private List<Stream> availableTextStreams;
         private List<Stream> availableVideoStreams;
4. <span data-ttu-id="dac98-282">Toevoegen in Hallo MainPage klasse, Hallo regio te volgen:</span><span class="sxs-lookup"><span data-stu-id="dac98-282">Inside hello MainPage class, add hello following region:</span></span>
   
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
5. <span data-ttu-id="dac98-283">Hallo mediaElement_ManifestReady methode vinden, na de code aan einde van de functie Hallo HALLO hallo toevoegen:</span><span class="sxs-lookup"><span data-stu-id="dac98-283">Locate hello mediaElement_ManifestReady method, append hello following code at hello end of hello function:</span></span>
   
        getStreams(manifestObject);
        refreshAvailableStreamsListBoxItemSource();
   
    <span data-ttu-id="dac98-284">Dus wanneer MediaElement manifest klaar is, Hallo code wordt een lijst met beschikbare streams Hallo en vult Hallo UI-keuzelijst met Hallo lijst.</span><span class="sxs-lookup"><span data-stu-id="dac98-284">So when MediaElement manifest is ready, hello code gets a list of hello available streams, and populates hello UI list box with hello list.</span></span>
6. <span data-ttu-id="dac98-285">Zoek in de klasse MainPage Hallo, Hallo UI knoppen klikt u op gebeurtenissen regio en voeg vervolgens Hallo functiedefinitie te volgen:</span><span class="sxs-lookup"><span data-stu-id="dac98-285">Inside hello MainPage class, locate hello UI buttons click events region, and then add hello following function definition:</span></span>
   
        private void btnChangeStream_Click(object sender, RoutedEventArgs e)
        {
            List<IManifestStream> selectedStreams = new List<IManifestStream>();
   
            // Create a list of hello selected streams
            createSelectedStreamsList(selectedStreams);
   
            // Change streams on hello presentation
            changeStreams(selectedStreams);
        }

<span data-ttu-id="dac98-286">**toocompile en test Hallo-toepassing**</span><span class="sxs-lookup"><span data-stu-id="dac98-286">**toocompile and test hello application**</span></span>

1. <span data-ttu-id="dac98-287">Druk op **F6** toocompile Hallo project.</span><span class="sxs-lookup"><span data-stu-id="dac98-287">Press **F6** toocompile hello project.</span></span> 
2. <span data-ttu-id="dac98-288">Druk op **F5** toorun Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="dac98-288">Press **F5** toorun hello application.</span></span>
3. <span data-ttu-id="dac98-289">Bovenaan Hallo Hallo toepassing, kunt u Hallo standaard-URL voor Smooth Streaming of voer een andere.</span><span class="sxs-lookup"><span data-stu-id="dac98-289">At hello top of hello application, you can either use hello default Smooth Streaming URL or enter a different one.</span></span> 
4. <span data-ttu-id="dac98-290">Klik op **bron instellen**.</span><span class="sxs-lookup"><span data-stu-id="dac98-290">Click **Set Source**.</span></span> 
5. <span data-ttu-id="dac98-291">Hallo standaardtaal is audio_eng.</span><span class="sxs-lookup"><span data-stu-id="dac98-291">hello default language is audio_eng.</span></span> <span data-ttu-id="dac98-292">Probeer tooswitch tussen audio_eng en audio_es.</span><span class="sxs-lookup"><span data-stu-id="dac98-292">Try tooswitch between audio_eng and audio_es.</span></span> <span data-ttu-id="dac98-293">Telkens wanneer, selecteert u een nieuwe stream, klikt u op de knop verzenden Hallo.</span><span class="sxs-lookup"><span data-stu-id="dac98-293">Everytime, you select a new stream, you must click hello Submit button.</span></span>

<span data-ttu-id="dac98-294">U kunt les 3 hebt voltooid.</span><span class="sxs-lookup"><span data-stu-id="dac98-294">You have completed lesson 3.</span></span>  <span data-ttu-id="dac98-295">In deze les voegt u Hallo functionaliteit toochoose stromen.</span><span class="sxs-lookup"><span data-stu-id="dac98-295">In this lesson, you add hello functionality toochoose streams.</span></span>

## <a name="lesson-4-select-smooth-streaming-tracks"></a><span data-ttu-id="dac98-296">Les 4: Selecteer nummers Smooth Streaming</span><span class="sxs-lookup"><span data-stu-id="dac98-296">Lesson 4: Select Smooth Streaming Tracks</span></span>
<span data-ttu-id="dac98-297">Een presentatie Smooth Streaming kan meerdere videobestanden gecodeerd met verschillende kwaliteitsniveaus (bitsnelheden) en oplossingen bevatten.</span><span class="sxs-lookup"><span data-stu-id="dac98-297">A Smooth Streaming presentation can contain multiple video files encoded with different quality levels (bit rates) and resolutions.</span></span> <span data-ttu-id="dac98-298">In deze les schakelt u gebruikers tooselect houdt.</span><span class="sxs-lookup"><span data-stu-id="dac98-298">In this lesson, you will enable users tooselect tracks.</span></span> <span data-ttu-id="dac98-299">Deze les bevat Hallo procedures te volgen:</span><span class="sxs-lookup"><span data-stu-id="dac98-299">This lesson contains hello following procedures:</span></span>

1. <span data-ttu-id="dac98-300">Hallo XAML-bestand wijzigen</span><span class="sxs-lookup"><span data-stu-id="dac98-300">Modify hello XAML file</span></span>
2. <span data-ttu-id="dac98-301">Hallo-codebestand behand wijzigen</span><span class="sxs-lookup"><span data-stu-id="dac98-301">Modify hello code behand file</span></span>
3. <span data-ttu-id="dac98-302">Compileren en Hallo toepassing testen</span><span class="sxs-lookup"><span data-stu-id="dac98-302">Compile and test hello application</span></span>

<span data-ttu-id="dac98-303">**toomodify hello XAML-bestand**</span><span class="sxs-lookup"><span data-stu-id="dac98-303">**toomodify hello XAML file**</span></span>

1. <span data-ttu-id="dac98-304">In Solution Explorer met de rechtermuisknop op **MainPage.xaml**, en klik vervolgens op **ontwerper**.</span><span class="sxs-lookup"><span data-stu-id="dac98-304">From Solution Explorer, right-click **MainPage.xaml**, and then click **View Designer**.</span></span>
2. <span data-ttu-id="dac98-305">Zoek Hallo &lt;raster&gt; tag met de naam van de Hallo **gridStreamAndBitrateSelection**, Hallo volgende code achter Hallo Hallo-tag toevoegen:</span><span class="sxs-lookup"><span data-stu-id="dac98-305">Locate hello &lt;Grid&gt; tag with hello name **gridStreamAndBitrateSelection**, append hello following code at hello end of hello tag:</span></span>
   
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
3. <span data-ttu-id="dac98-306">Druk op **CTRL + S** toosave hij wordt gewijzigd</span><span class="sxs-lookup"><span data-stu-id="dac98-306">Press **CTRL+S** toosave he changes</span></span>

<span data-ttu-id="dac98-307">**toomodify hello onderliggende-codebestand**</span><span class="sxs-lookup"><span data-stu-id="dac98-307">**toomodify hello code behind file**</span></span>

1. <span data-ttu-id="dac98-308">In Solution Explorer met de rechtermuisknop op **MainPage.xaml**, en klik vervolgens op **weergavecode**.</span><span class="sxs-lookup"><span data-stu-id="dac98-308">From Solution Explorer, right-click **MainPage.xaml**, and then click **View Code**.</span></span>
2. <span data-ttu-id="dac98-309">Voeg een nieuwe klasse in Hallo SSPlayer naamruimte:</span><span class="sxs-lookup"><span data-stu-id="dac98-309">Inside hello SSPlayer namespace, add a new class:</span></span>
   
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
3. <span data-ttu-id="dac98-310">Toevoegen aan het begin van de Hallo Hallo MainPage klasse, Hallo variabele definities te volgen:</span><span class="sxs-lookup"><span data-stu-id="dac98-310">At hello beginning of hello MainPage class, add hello following variable definitions:</span></span>
   
        private List<Track> availableTracks;
4. <span data-ttu-id="dac98-311">Toevoegen in Hallo MainPage klasse, Hallo regio te volgen:</span><span class="sxs-lookup"><span data-stu-id="dac98-311">Inside hello MainPage class, add hello following region:</span></span>
   
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
5. <span data-ttu-id="dac98-312">Hallo mediaElement_ManifestReady methode vinden, na de code aan einde van de functie Hallo HALLO hallo toevoegen:</span><span class="sxs-lookup"><span data-stu-id="dac98-312">Locate hello mediaElement_ManifestReady method, append hello following code at hello end of hello function:</span></span>
   
         getTracks(manifestObject);
         refreshAvailableTracksListBoxItemSource();
6. <span data-ttu-id="dac98-313">Zoek in de klasse MainPage Hallo, Hallo UI knoppen klikt u op gebeurtenissen regio en voeg vervolgens Hallo functiedefinitie te volgen:</span><span class="sxs-lookup"><span data-stu-id="dac98-313">Inside hello MainPage class, locate hello UI buttons click events region, and then add hello following function definition:</span></span>
   
         private void btnChangeStream_Click(object sender, RoutedEventArgs e)
         {
            List<IManifestStream> selectedStreams = new List<IManifestStream>();

            // Create a list of hello selected streams
            createSelectedStreamsList(selectedStreams);

            // Change streams on hello presentation
            changeStreams(selectedStreams);
         }

<span data-ttu-id="dac98-314">**toocompile en test Hallo-toepassing**</span><span class="sxs-lookup"><span data-stu-id="dac98-314">**toocompile and test hello application**</span></span>

1. <span data-ttu-id="dac98-315">Druk op **F6** toocompile Hallo project.</span><span class="sxs-lookup"><span data-stu-id="dac98-315">Press **F6** toocompile hello project.</span></span> 
2. <span data-ttu-id="dac98-316">Druk op **F5** toorun Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="dac98-316">Press **F5** toorun hello application.</span></span>
3. <span data-ttu-id="dac98-317">Bovenaan Hallo Hallo toepassing, kunt u Hallo standaard-URL voor Smooth Streaming of voer een andere.</span><span class="sxs-lookup"><span data-stu-id="dac98-317">At hello top of hello application, you can either use hello default Smooth Streaming URL or enter a different one.</span></span> 
4. <span data-ttu-id="dac98-318">Klik op **bron instellen**.</span><span class="sxs-lookup"><span data-stu-id="dac98-318">Click **Set Source**.</span></span> 
5. <span data-ttu-id="dac98-319">Alle Hallo houdt van Hallo videostream zijn standaard geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="dac98-319">By default, all of hello tracks of hello video stream are selected.</span></span> <span data-ttu-id="dac98-320">tooexperiment Hallo bit tarief wordt gewijzigd, kunt u selecteren Hallo laagste bitsnelheid die beschikbaar is en selecteer vervolgens Hallo hoogste bitsnelheid die beschikbaar is.</span><span class="sxs-lookup"><span data-stu-id="dac98-320">tooexperiment hello bit rate changes, you can select hello lowest bit rate available, and then select hello highest bit rate available.</span></span> <span data-ttu-id="dac98-321">U moet op verzenden klikt na elke wijziging.</span><span class="sxs-lookup"><span data-stu-id="dac98-321">You must click Submit after each change.</span></span>  <span data-ttu-id="dac98-322">U kunt Hallo videokwaliteit wijzigingen kan zien.</span><span class="sxs-lookup"><span data-stu-id="dac98-322">You can see hello video quality changes.</span></span>

<span data-ttu-id="dac98-323">U kunt les 4 hebt voltooid.</span><span class="sxs-lookup"><span data-stu-id="dac98-323">You have completed lesson 4.</span></span>  <span data-ttu-id="dac98-324">In deze les voegt u Hallo functionaliteit toochoose houdt.</span><span class="sxs-lookup"><span data-stu-id="dac98-324">In this lesson, you add hello functionality toochoose tracks.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="dac98-325">Media Services-leertrajecten</span><span class="sxs-lookup"><span data-stu-id="dac98-325">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="dac98-326">Feedback geven</span><span class="sxs-lookup"><span data-stu-id="dac98-326">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="other-resources"></a><span data-ttu-id="dac98-327">Andere bronnen:</span><span class="sxs-lookup"><span data-stu-id="dac98-327">Other Resources:</span></span>
* [<span data-ttu-id="dac98-328">Hoe toobuild Smooth Streaming Windows 8 JavaScript-toepassing met geavanceerde functies</span><span class="sxs-lookup"><span data-stu-id="dac98-328">How toobuild a Smooth Streaming Windows 8 JavaScript application with advanced features</span></span>](http://blogs.iis.net/cenkd/archive/2012/08/10/how-to-build-a-smooth-streaming-windows-8-javascript-application-with-advanced-features.aspx)
* [<span data-ttu-id="dac98-329">Smooth Streaming technisch overzicht</span><span class="sxs-lookup"><span data-stu-id="dac98-329">Smooth Streaming Technical Overview</span></span>](http://www.iis.net/learn/media/on-demand-smooth-streaming/smooth-streaming-technical-overview)

[PlayerApplication]: ./media/media-services-build-smooth-streaming-apps/SSClientWin8-1.png
[CodeViewPic]: ./media/media-services-build-smooth-streaming-apps/SSClientWin8-2.png


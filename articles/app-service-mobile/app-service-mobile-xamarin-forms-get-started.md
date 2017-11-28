---
title: aaaGet slag met Mobile Apps met behulp van Xamarin.Forms
description: Volg deze zelfstudie toostart met Mobile Apps voor Xamarin.Forms-ontwikkeling
services: app-service\mobile
documentationcenter: xamarin
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 5e692220-cc89-4548-96c8-35259722acf5
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: af6b1c1ce4cf91c397552aa3d8ee40728129238c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-xamarinforms-app"></a><span data-ttu-id="22a40-103">Een Xamarin.Forms-app maken</span><span class="sxs-lookup"><span data-stu-id="22a40-103">Create a Xamarin.Forms app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started](../../includes/app-service-mobile-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="22a40-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="22a40-104">Overview</span></span>
<span data-ttu-id="22a40-105">Deze zelfstudie leert u hoe tooadd een back-endservice cloud-gebaseerde tooa mobiele Xamarin.Forms-app met behulp van de functie Mobile Apps van Azure App Service als de back-end Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="22a40-105">This tutorial shows you how tooadd a cloud-based back-end service tooa Xamarin.Forms mobile app by using hello Mobile Apps feature of Azure App Service as hello back end.</span></span> <span data-ttu-id="22a40-106">U maakt zowel een nieuwe back-end voor Mobile Apps als een eenvoudige Xamarin.Forms-app voor takenlijsten die app-gegevens opslaat in Azure.</span><span class="sxs-lookup"><span data-stu-id="22a40-106">You create both a new Mobile Apps back end and a simple to-do list Xamarin.Forms app that stores app data in Azure.</span></span>

<span data-ttu-id="22a40-107">Het voltooien van deze zelfstudie is een vereiste voor alle andere zelfstudies over Mobile Apps voor Xamarin.Forms.</span><span class="sxs-lookup"><span data-stu-id="22a40-107">Completing this tutorial is a prerequisite for all other Mobile Apps tutorials for Xamarin.Forms.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="22a40-108">Vereisten</span><span class="sxs-lookup"><span data-stu-id="22a40-108">Prerequisites</span></span>
<span data-ttu-id="22a40-109">toocomplete in deze zelfstudie, moet u hello te volgen:</span><span class="sxs-lookup"><span data-stu-id="22a40-109">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="22a40-110">Een actief Azure-account.</span><span class="sxs-lookup"><span data-stu-id="22a40-110">An active Azure account.</span></span> <span data-ttu-id="22a40-111">Als u geen account hebt, kunt u zich aanmeldt voor een proefversie van Azure en krijg too10 gratis mobiele apps die u ook na de proefperiode kunt blijven gebruiken.</span><span class="sxs-lookup"><span data-stu-id="22a40-111">If you don't have an account, you can sign up for an Azure trial and get up too10 free mobile apps that you can keep using even after your trial ends.</span></span> <span data-ttu-id="22a40-112">Zie [Maak vandaag nog uw gratis Azure-account](https://azure.microsoft.com/pricing/free-trial/) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="22a40-112">For more information, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

* <span data-ttu-id="22a40-113">Visual Studio met Xamarin.</span><span class="sxs-lookup"><span data-stu-id="22a40-113">Visual Studio with Xamarin.</span></span> <span data-ttu-id="22a40-114">Zie voor informatie Hallo [ingesteld omhoog en installeer Visual Studio en Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) pagina.</span><span class="sxs-lookup"><span data-stu-id="22a40-114">For information, see hello [Set up and install Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) page.</span></span>

* <span data-ttu-id="22a40-115">Een Mac met Xcode v7.0 of hoger en waarop Xamarin Studio Community is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="22a40-115">A Mac with Xcode v7.0 or later and Xamarin Studio Community installed.</span></span> <span data-ttu-id="22a40-116">Zie [Setup and install](https://msdn.microsoft.com/library/mt613162.aspx) (Configureren en installeren) en [Setup, install, and verifications for Mac users](https://msdn.microsoft.com/library/mt488770.aspx) (Instructies voor installatie, configuratie en verificatie voor Mac-gebruikers) (MSDN) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="22a40-116">For information, see [Set up and install Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) and [Set up, install, and verify for Mac users](https://msdn.microsoft.com/library/mt488770.aspx) (MSDN).</span></span>

## <a name="create-a-new-mobile-apps-back-end"></a><span data-ttu-id="22a40-117">Een nieuwe back-end voor Mobile Apps maken</span><span class="sxs-lookup"><span data-stu-id="22a40-117">Create a new Mobile Apps back end</span></span>

<span data-ttu-id="22a40-118">weer een nieuwe Mobile Apps beëindigen, toocreate Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="22a40-118">toocreate a new Mobile Apps back end, do hello following:</span></span>

[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service](../../includes/app-service-mobile-dotnet-backend-create-new-service.md)]

<span data-ttu-id="22a40-119">U hebt nu een back-end voor Mobile Apps ingesteld die uw mobiele clienttoepassingen kunnen gebruiken.</span><span class="sxs-lookup"><span data-stu-id="22a40-119">You have now set up a Mobile Apps back end that your mobile client applications can use.</span></span> <span data-ttu-id="22a40-120">Vervolgens maakt u een serverproject downloaden voor een eenvoudige taak lijst back-end en publiceer deze tooAzure.</span><span class="sxs-lookup"><span data-stu-id="22a40-120">Next, you download a server project for a simple to-do list back end and then publish it tooAzure.</span></span>

## <a name="configure-hello-server-project"></a><span data-ttu-id="22a40-121">Hallo serverproject configureren</span><span class="sxs-lookup"><span data-stu-id="22a40-121">Configure hello server project</span></span>

<span data-ttu-id="22a40-122">tooconfigure hello server project toouse Hallo Node.js- of .NET back-end, Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="22a40-122">tooconfigure hello server project toouse either hello Node.js or .NET back end, do hello following:</span></span>

[!INCLUDE [app-service-mobile-configure-new-backend](../../includes/app-service-mobile-configure-new-backend.md)]

## <a name="download-and-run-hello-xamarinforms-solution"></a><span data-ttu-id="22a40-123">Hallo Xamarin.Forms-oplossing downloaden en uitvoeren</span><span class="sxs-lookup"><span data-stu-id="22a40-123">Download and run hello Xamarin.Forms solution</span></span>

<span data-ttu-id="22a40-124">U kunt Hallo-oplossing op twee manieren downloaden.</span><span class="sxs-lookup"><span data-stu-id="22a40-124">You can download hello solution in either of two ways.</span></span> <span data-ttu-id="22a40-125">Download deze tooa Mac en openen in Xamarin Studio of download deze tooa Windows-computer en openen in Visual Studio met behulp van Mac in een netwerk voor het bouwen van Hallo iOS-app.</span><span class="sxs-lookup"><span data-stu-id="22a40-125">Download it tooa Mac and open it in Xamarin Studio, or download it tooa Windows computer and open it in Visual Studio by using a networked Mac for building hello iOS app.</span></span> <span data-ttu-id="22a40-126">Zie [Setup and install](https://msdn.microsoft.com/library/mt613162.aspx) (Configureren en installeren) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="22a40-126">For more information, see [Set up and install Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx).</span></span>

<span data-ttu-id="22a40-127">Op een Mac of Windows-computer, Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="22a40-127">On a Mac or Windows computer, do hello following:</span></span>

1. <span data-ttu-id="22a40-128">Ga toohello [Azure-portal].</span><span class="sxs-lookup"><span data-stu-id="22a40-128">Go toohello [Azure portal].</span></span>

2. <span data-ttu-id="22a40-129">Op Hallo **instellingen** blade voor uw mobiele app onder **Mobile**, selecteer **aan de slag** > **Xamarin.Forms**.</span><span class="sxs-lookup"><span data-stu-id="22a40-129">On hello **Settings** blade for your mobile app, under **Mobile**, select **Get Started** > **Xamarin.Forms**.</span></span> <span data-ttu-id="22a40-130">Selecteer **Een nieuwe app maken** onder **stap 3** en selecteer vervolgens **Downloaden**.</span><span class="sxs-lookup"><span data-stu-id="22a40-130">Under **step 3**, select  **Create a new app**, and then select **Download**.</span></span>

   <span data-ttu-id="22a40-131">Deze actie een project gedownload dat een clienttoepassing bevat die is verbonden tooyour mobiele app.</span><span class="sxs-lookup"><span data-stu-id="22a40-131">This action downloads a project that contains a client application that's connected tooyour mobile app.</span></span> <span data-ttu-id="22a40-132">Hallo project gecomprimeerde bestand tooyour lokale computer opslaan en maak een notitie van de opslaglocatie.</span><span class="sxs-lookup"><span data-stu-id="22a40-132">Save hello compressed project file tooyour local computer, and make a note of where you save it.</span></span>

3. <span data-ttu-id="22a40-133">Pak Hallo-project dat u hebt gedownload en open het in Xamarin Studio (Mac) of Visual Studio (Windows).</span><span class="sxs-lookup"><span data-stu-id="22a40-133">Extract hello project that you downloaded, and then open it in Xamarin Studio (Mac) or Visual Studio (Windows).</span></span>

   ![Uitgepakt project in Xamarin Studio][9]

   ![Uitgepakt project in Visual Studio][8]

## <a name="optional-run-hello-ios-project"></a><span data-ttu-id="22a40-136">(Optioneel) Hallo iOS-project uitvoeren</span><span class="sxs-lookup"><span data-stu-id="22a40-136">(Optional) Run hello iOS project</span></span>
<span data-ttu-id="22a40-137">In deze sectie kunt uitvoeren u Hallo Xamarin iOS-project voor iOS-apparaten.</span><span class="sxs-lookup"><span data-stu-id="22a40-137">In this section, you run hello Xamarin iOS project for iOS devices.</span></span> <span data-ttu-id="22a40-138">Als u niet met iOS-apparaten werkt, kunt u deze sectie overslaan.</span><span class="sxs-lookup"><span data-stu-id="22a40-138">You can skip this section if you are not working with iOS devices.</span></span>

#### <a name="in-xamarin-studio"></a><span data-ttu-id="22a40-139">In Xamarin Studio</span><span class="sxs-lookup"><span data-stu-id="22a40-139">In Xamarin Studio</span></span>
1. <span data-ttu-id="22a40-140">Met de rechtermuisknop op Hallo iOS-project en selecteer vervolgens **instellen als opstartproject**.</span><span class="sxs-lookup"><span data-stu-id="22a40-140">Right-click hello iOS project, and then select **Set As Startup Project**.</span></span>

2. <span data-ttu-id="22a40-141">Op Hallo **uitvoeren** selecteert u **foutopsporing starten** toobuild Hallo project en Hallo-app in Hallo iPhone-emulator te starten.</span><span class="sxs-lookup"><span data-stu-id="22a40-141">On hello **Run** menu, select **Start Debugging** toobuild hello project and start hello app in hello iPhone emulator.</span></span>

#### <a name="in-visual-studio"></a><span data-ttu-id="22a40-142">In Visual Studio</span><span class="sxs-lookup"><span data-stu-id="22a40-142">In Visual Studio</span></span>
1. <span data-ttu-id="22a40-143">Met de rechtermuisknop op Hallo iOS-project en selecteer vervolgens **instellen als opstartproject**.</span><span class="sxs-lookup"><span data-stu-id="22a40-143">Right-click hello iOS project, and then select **Set as StartUp Project**.</span></span>

2. <span data-ttu-id="22a40-144">Op Hallo **bouwen** selecteert u **Configuration Manager**.</span><span class="sxs-lookup"><span data-stu-id="22a40-144">On hello **Build** menu, select **Configuration Manager**.</span></span>

3. <span data-ttu-id="22a40-145">In Hallo **Configuration Manager** dialoogvenster, selecteer Hallo **bouwen** en **implementeren** selectievakjes volgende toohello iOS-project.</span><span class="sxs-lookup"><span data-stu-id="22a40-145">In hello **Configuration Manager** dialog box, select hello **Build** and **Deploy** check boxes next toohello iOS project.</span></span>

4. <span data-ttu-id="22a40-146">toobuild project Hallo en Hallo-app te starten in Hallo iPhone-emulator, selecteer Hallo **F5** sleutel.</span><span class="sxs-lookup"><span data-stu-id="22a40-146">toobuild hello project and start hello app in hello iPhone emulator, select hello **F5** key.</span></span>

   > [!NOTE]
   > <span data-ttu-id="22a40-147">Als u problemen ondervindt Hallo-project te bouwen, uitvoeren Hallo NuGet package manager en update toohello meest recente versie van Hallo Xamarin-ondersteuningspakketten.</span><span class="sxs-lookup"><span data-stu-id="22a40-147">If you have problems building hello project, run hello NuGet package manager and update toohello latest version of hello Xamarin support packages.</span></span> <span data-ttu-id="22a40-148">QuickStart-projecten mogelijk traag tooupdate toohello meest recente versies.</span><span class="sxs-lookup"><span data-stu-id="22a40-148">Quickstart projects might be slow tooupdate toohello latest versions.</span></span>    
   >
   >

5. <span data-ttu-id="22a40-149">Typ in het Hallo-app zinvolle tekst, zoals *xamarin leren kennen*, en vervolgens selecteert Hallo plusteken (**+**).</span><span class="sxs-lookup"><span data-stu-id="22a40-149">In hello app, type meaningful text, such as *Learn Xamarin*, and then select hello plus sign (**+**).</span></span>

    ![][10]

    <span data-ttu-id="22a40-150">Met deze actie verzendt een post-aanvraag toohello die mobiele Apps van nieuwe back-end die wordt gehost in Azure.</span><span class="sxs-lookup"><span data-stu-id="22a40-150">This action sends a post request toohello new Mobile Apps back end that's hosted in Azure.</span></span> <span data-ttu-id="22a40-151">De gegevens van Hallo-aanvraag is opgenomen in de takentabel Hallo.</span><span class="sxs-lookup"><span data-stu-id="22a40-151">Data from hello request is inserted into hello TodoItem table.</span></span> <span data-ttu-id="22a40-152">Items die zijn opgeslagen in de tabel Hallo worden geretourneerd door Hallo Mobile Apps terug beëindigen en Hallo gegevens worden weergegeven in de lijst Hallo.</span><span class="sxs-lookup"><span data-stu-id="22a40-152">Items that are stored in hello table are returned by hello Mobile Apps back end, and hello data is displayed in hello list.</span></span>

    > [!NOTE]
    > <span data-ttu-id="22a40-153">Hier vindt u Hallo-code die toegang heeft tot uw back-end van Mobile Apps in Hallo TodoItemManager.cs C#-bestand van Hallo portable class library-project van uw oplossing.</span><span class="sxs-lookup"><span data-stu-id="22a40-153">You'll find hello code that accesses your Mobile Apps back end in hello TodoItemManager.cs C# file of hello portable class library project of your solution.</span></span>
    >
    >

## <a name="optional-run-hello-android-project"></a><span data-ttu-id="22a40-154">(Optioneel) Hallo Android-project uitvoeren</span><span class="sxs-lookup"><span data-stu-id="22a40-154">(Optional) Run hello Android project</span></span>
<span data-ttu-id="22a40-155">In deze sectie kunt u Hallo Xamarin droid-project voor Android uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="22a40-155">In this section, you run hello Xamarin droid project for Android.</span></span> <span data-ttu-id="22a40-156">Als u niet met Android-apparaten werkt, kunt u deze sectie overslaan.</span><span class="sxs-lookup"><span data-stu-id="22a40-156">You can skip this section if you are not working with Android devices.</span></span>

#### <a name="in-xamarin-studio"></a><span data-ttu-id="22a40-157">In Xamarin Studio</span><span class="sxs-lookup"><span data-stu-id="22a40-157">In Xamarin Studio</span></span>

1. <span data-ttu-id="22a40-158">Met de rechtermuisknop op Hallo Android-project en selecteer vervolgens **instellen als opstartproject**.</span><span class="sxs-lookup"><span data-stu-id="22a40-158">Right-click hello Android project, and then select **Set As Startup Project**.</span></span>

2. <span data-ttu-id="22a40-159">toobuild project Hallo en Hallo-app te starten in een Android-emulator op Hallo **uitvoeren** selecteert u **foutopsporing starten**.</span><span class="sxs-lookup"><span data-stu-id="22a40-159">toobuild hello project and start hello app in an Android emulator, on hello **Run** menu, select **Start Debugging**.</span></span>

#### <a name="in-visual-studio"></a><span data-ttu-id="22a40-160">In Visual Studio</span><span class="sxs-lookup"><span data-stu-id="22a40-160">In Visual Studio</span></span>

1. <span data-ttu-id="22a40-161">Met de rechtermuisknop op het Hallo-project voor Android (Droid) en selecteer vervolgens **instellen als opstartproject**.</span><span class="sxs-lookup"><span data-stu-id="22a40-161">Right-click hello Android (Droid) project, and then select **Set as StartUp Project**.</span></span>

2. <span data-ttu-id="22a40-162">Op Hallo **bouwen** selecteert u **Configuration Manager**.</span><span class="sxs-lookup"><span data-stu-id="22a40-162">On hello **Build** menu, select **Configuration Manager**.</span></span>

3. <span data-ttu-id="22a40-163">In Hallo **Configuration Manager** dialoogvenster, selecteer Hallo **bouwen** en **implementeren** selectievakjes volgende toohello Android-project.</span><span class="sxs-lookup"><span data-stu-id="22a40-163">In hello **Configuration Manager** dialog box, select hello **Build** and **Deploy** check boxes next toohello Android project.</span></span>

4. <span data-ttu-id="22a40-164">toobuild project Hallo en Hallo-app te starten in een Android-emulator, selecteer Hallo **F5** sleutel.</span><span class="sxs-lookup"><span data-stu-id="22a40-164">toobuild hello project and start hello app in an Android emulator, select hello **F5** key.</span></span>

   > [!NOTE]
   > <span data-ttu-id="22a40-165">Als u problemen ondervindt Hallo-project te bouwen, uitvoeren Hallo NuGet package manager en update toohello meest recente versie van Hallo Xamarin-ondersteuningspakketten.</span><span class="sxs-lookup"><span data-stu-id="22a40-165">If you have problems building hello project, run hello NuGet package manager and update toohello latest version of hello Xamarin support packages.</span></span> <span data-ttu-id="22a40-166">QuickStart-projecten mogelijk traag tooupdate toohello meest recente versies.</span><span class="sxs-lookup"><span data-stu-id="22a40-166">Quickstart projects might be slow tooupdate toohello latest versions.</span></span>    
   >
   >

5. <span data-ttu-id="22a40-167">Typ in het Hallo-app zinvolle tekst, zoals *xamarin leren kennen*, en vervolgens selecteert Hallo plusteken (**+**).</span><span class="sxs-lookup"><span data-stu-id="22a40-167">In hello app, type meaningful text, such as *Learn Xamarin*, and then select hello plus sign (**+**).</span></span>

    ![][11]
    
    <span data-ttu-id="22a40-168">Met deze actie verzendt een post-aanvraag toohello die mobiele Apps van nieuwe back-end die wordt gehost in Azure.</span><span class="sxs-lookup"><span data-stu-id="22a40-168">This action sends a post request toohello new Mobile Apps back end that's hosted in Azure.</span></span> <span data-ttu-id="22a40-169">De gegevens van Hallo-aanvraag is opgenomen in de takentabel Hallo.</span><span class="sxs-lookup"><span data-stu-id="22a40-169">Data from hello request is inserted into hello TodoItem table.</span></span> <span data-ttu-id="22a40-170">Items die zijn opgeslagen in de tabel Hallo worden geretourneerd door Hallo Mobile Apps terug beëindigen en Hallo gegevens worden weergegeven in de lijst Hallo.</span><span class="sxs-lookup"><span data-stu-id="22a40-170">Items that are stored in hello table are returned by hello Mobile Apps back end, and hello data is displayed in hello list.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="22a40-171">Hier vindt u Hallo-code die toegang heeft tot uw back-end van Mobile Apps in Hallo TodoItemManager.cs C#-bestand van Hallo portable class library-project van uw oplossing.</span><span class="sxs-lookup"><span data-stu-id="22a40-171">You'll find hello code that accesses your Mobile Apps back end in hello TodoItemManager.cs C# file of hello portable class library project of your solution.</span></span>
    >
    >

## <a name="optional-run-hello-windows-project"></a><span data-ttu-id="22a40-172">(Optioneel) Hallo Windows-project uitvoeren</span><span class="sxs-lookup"><span data-stu-id="22a40-172">(Optional) Run hello Windows project</span></span>

<span data-ttu-id="22a40-173">In deze sectie kunt uitvoeren u Hallo project Xamarin WinApp voor Windows-apparaten.</span><span class="sxs-lookup"><span data-stu-id="22a40-173">In this section, you run hello Xamarin WinApp project for Windows devices.</span></span> <span data-ttu-id="22a40-174">Als u niet met Windows-apparaten werkt, kunt u deze sectie overslaan.</span><span class="sxs-lookup"><span data-stu-id="22a40-174">You can skip this section if you are not working with Windows devices.</span></span>

#### <a name="in-visual-studio"></a><span data-ttu-id="22a40-175">In Visual Studio</span><span class="sxs-lookup"><span data-stu-id="22a40-175">In Visual Studio</span></span>

1. <span data-ttu-id="22a40-176">Met de rechtermuisknop op een van de Windows-projecten Hallo en selecteer vervolgens **instellen als opstartproject**.</span><span class="sxs-lookup"><span data-stu-id="22a40-176">Right-click any of hello Windows projects, and then select **Set as StartUp Project**.</span></span>

2. <span data-ttu-id="22a40-177">Op Hallo **bouwen** selecteert u **Configuration Manager**.</span><span class="sxs-lookup"><span data-stu-id="22a40-177">On hello **Build** menu, select **Configuration Manager**.</span></span>

3. <span data-ttu-id="22a40-178">In Hallo **Configuration Manager** dialoogvenster, selecteer Hallo **bouwen** en **implementeren** selectievakjes volgende toohello Windows-project dat u hebt gekozen.</span><span class="sxs-lookup"><span data-stu-id="22a40-178">In hello **Configuration Manager** dialog box, select hello **Build** and **Deploy** check boxes next toohello Windows project that you chose.</span></span>

4. <span data-ttu-id="22a40-179">toobuild project Hallo en Hallo-app te starten in een Windows-emulator, selecteer Hallo **F5** sleutel.</span><span class="sxs-lookup"><span data-stu-id="22a40-179">toobuild hello project and start hello app in a Windows emulator, select hello **F5** key.</span></span>

   > [!NOTE]
   > <span data-ttu-id="22a40-180">Als u problemen ondervindt Hallo-project te bouwen, uitvoeren Hallo NuGet package manager en update toohello meest recente versie van Hallo Xamarin-ondersteuningspakketten.</span><span class="sxs-lookup"><span data-stu-id="22a40-180">If you have problems building hello project, run hello NuGet package manager and update toohello latest version of hello Xamarin support packages.</span></span> <span data-ttu-id="22a40-181">QuickStart-projecten mogelijk traag tooupdate toohello meest recente versies.</span><span class="sxs-lookup"><span data-stu-id="22a40-181">Quickstart projects might be slow tooupdate toohello latest versions.</span></span>    
   >
   >

5. <span data-ttu-id="22a40-182">Typ in het Hallo-app zinvolle tekst, zoals *xamarin leren kennen*, en vervolgens selecteert Hallo plusteken (**+**).</span><span class="sxs-lookup"><span data-stu-id="22a40-182">In hello app, type meaningful text, such as *Learn Xamarin*, and then select hello plus sign (**+**).</span></span>

    <span data-ttu-id="22a40-183">Met deze actie verzendt een post-aanvraag toohello die mobiele Apps van nieuwe back-end die wordt gehost in Azure.</span><span class="sxs-lookup"><span data-stu-id="22a40-183">This action sends a post request toohello new Mobile Apps back end that's hosted in Azure.</span></span> <span data-ttu-id="22a40-184">De gegevens van Hallo-aanvraag is opgenomen in de takentabel Hallo.</span><span class="sxs-lookup"><span data-stu-id="22a40-184">Data from hello request is inserted into hello TodoItem table.</span></span> <span data-ttu-id="22a40-185">Items die zijn opgeslagen in de tabel Hallo worden geretourneerd door Hallo Mobile Apps terug beëindigen en Hallo gegevens worden weergegeven in de lijst Hallo.</span><span class="sxs-lookup"><span data-stu-id="22a40-185">Items that are stored in hello table are returned by hello Mobile Apps back end, and hello data is displayed in hello list.</span></span>
    
    ![][12]
    
    > [!NOTE]
    > <span data-ttu-id="22a40-186">Hier vindt u Hallo-code die toegang heeft tot uw back-end van Mobile Apps in Hallo TodoItemManager.cs C#-bestand van Hallo portable class library-project van uw oplossing.</span><span class="sxs-lookup"><span data-stu-id="22a40-186">You'll find hello code that accesses your Mobile Apps back end in hello TodoItemManager.cs C# file of hello portable class library project of your solution.</span></span>
    >
    >

## <a name="next-steps"></a><span data-ttu-id="22a40-187">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="22a40-187">Next steps</span></span>

* [<span data-ttu-id="22a40-188">Verificatie tooyour app toevoegen</span><span class="sxs-lookup"><span data-stu-id="22a40-188">Add authentication tooyour app</span></span>](app-service-mobile-xamarin-forms-get-started-users.md)  
  <span data-ttu-id="22a40-189">Meer informatie over hoe tooauthenticate gebruikers van uw app met een id-provider.</span><span class="sxs-lookup"><span data-stu-id="22a40-189">Learn how tooauthenticate users of your app with an identity provider.</span></span>

* [<span data-ttu-id="22a40-190">Push notifications tooyour app toevoegen</span><span class="sxs-lookup"><span data-stu-id="22a40-190">Add push notifications tooyour app</span></span>](app-service-mobile-xamarin-forms-get-started-push.md)  
  <span data-ttu-id="22a40-191">Informatie over hoe tooadd pushmeldingen tooyour app ondersteunen en uw Mobile Apps back-end toouse Azure Notification Hubs toosend Hallo push-meldingen configureren.</span><span class="sxs-lookup"><span data-stu-id="22a40-191">Learn how tooadd push notifications support tooyour app and configure your Mobile Apps back end toouse Azure Notification Hubs toosend hello push notifications.</span></span>

* [<span data-ttu-id="22a40-192">Offlinesynchronisatie voor uw app inschakelen</span><span class="sxs-lookup"><span data-stu-id="22a40-192">Enable offline sync for your app</span></span>](app-service-mobile-xamarin-forms-get-started-offline-data.md)  
  <span data-ttu-id="22a40-193">Meer informatie over hoe tooadd offlineondersteuning voor uw app met behulp van een mobiele Apps van back-end.</span><span class="sxs-lookup"><span data-stu-id="22a40-193">Learn how tooadd offline support for your app by using a Mobile Apps back end.</span></span> <span data-ttu-id="22a40-194">Offline synchroniseren zorgt ervoor dat u gegevens van een mobiele app kunt weergeven, toevoegen of wijzigen, zelfs als er geen netwerkverbinding is.</span><span class="sxs-lookup"><span data-stu-id="22a40-194">With offline sync, you can view, add, or modify your mobile app's data, even when there is no network connection.</span></span>

* [<span data-ttu-id="22a40-195">Hallo beheerde client gebruiken voor mobiele Apps</span><span class="sxs-lookup"><span data-stu-id="22a40-195">Use hello managed client for Mobile Apps</span></span>](app-service-mobile-dotnet-how-to-use-client-library.md)  
  <span data-ttu-id="22a40-196">Meer informatie over hoe toowork Hello beheerd client SDK in uw Xamarin-app.</span><span class="sxs-lookup"><span data-stu-id="22a40-196">Learn how toowork with hello managed client SDK in your Xamarin app.</span></span>

<!-- Anchors. -->
[Get started with Mobile Apps back ends]:#getting-started
[Create a new Mobile Apps back end]:#create-new-service
[Next steps]:#next-steps


<!-- Images. -->
[6]: ./media/app-service-mobile-xamarin-forms-get-started/xamarin-forms-quickstart.png
[8]: ./media/app-service-mobile-xamarin-forms-get-started/xamarin-forms-quickstart-vs.png
[9]: ./media/app-service-mobile-xamarin-forms-get-started/xamarin-forms-quickstart-xs.png
[10]: ./media/app-service-mobile-xamarin-forms-get-started/mobile-quickstart-startup-ios.png
[11]: ./media/app-service-mobile-xamarin-forms-get-started/mobile-quickstart-startup-android.png
[12]: ./media/app-service-mobile-xamarin-forms-get-started/mobile-quickstart-startup-windows.png


<!-- URLs. -->
[Visual Studio Professional 2013]: https://go.microsoft.com/fwLink/p/?LinkID=257546
[Mobile app SDK]: http://go.microsoft.com/fwlink/?LinkId=257545
[Azure-portal]: https://portal.azure.com/

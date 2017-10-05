---
title: Aan de slag met Mobile Apps met behulp van Xamarin.Forms
description: Volg deze zelfstudie om aan de slag te gaan met Mobile Apps voor Xamarin.Forms-ontwikkeling
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
ms.openlocfilehash: ee12caaad4095cff6dae3282f747ae804f93db81
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-xamarinforms-app"></a><span data-ttu-id="1a533-103">Een Xamarin.Forms-app maken</span><span class="sxs-lookup"><span data-stu-id="1a533-103">Create a Xamarin.Forms app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started](../../includes/app-service-mobile-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="1a533-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="1a533-104">Overview</span></span>
<span data-ttu-id="1a533-105">Deze zelfstudie laat zien hoe u een cloudgebaseerde back-endservice toevoegt aan een mobiele Xamarin.Forms-app door de functie Mobile Apps van Azure App Service als de back-end te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="1a533-105">This tutorial shows you how to add a cloud-based back-end service to a Xamarin.Forms mobile app by using the Mobile Apps feature of Azure App Service as the back end.</span></span> <span data-ttu-id="1a533-106">U maakt zowel een nieuwe back-end voor Mobile Apps als een eenvoudige Xamarin.Forms-app voor takenlijsten die app-gegevens opslaat in Azure.</span><span class="sxs-lookup"><span data-stu-id="1a533-106">You create both a new Mobile Apps back end and a simple to-do list Xamarin.Forms app that stores app data in Azure.</span></span>

<span data-ttu-id="1a533-107">Het voltooien van deze zelfstudie is een vereiste voor alle andere zelfstudies over Mobile Apps voor Xamarin.Forms.</span><span class="sxs-lookup"><span data-stu-id="1a533-107">Completing this tutorial is a prerequisite for all other Mobile Apps tutorials for Xamarin.Forms.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1a533-108">Vereisten</span><span class="sxs-lookup"><span data-stu-id="1a533-108">Prerequisites</span></span>
<span data-ttu-id="1a533-109">Voor het voltooien van deze zelfstudie hebt u het volgende nodig:</span><span class="sxs-lookup"><span data-stu-id="1a533-109">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="1a533-110">Een actief Azure-account.</span><span class="sxs-lookup"><span data-stu-id="1a533-110">An active Azure account.</span></span> <span data-ttu-id="1a533-111">Als u geen account hebt, kunt u zich aanmelden voor een proefversie van Azure en maximaal tien gratis mobiele apps krijgen die u ook na de proefperiode kunt blijven gebruiken.</span><span class="sxs-lookup"><span data-stu-id="1a533-111">If you don't have an account, you can sign up for an Azure trial and get up to 10 free mobile apps that you can keep using even after your trial ends.</span></span> <span data-ttu-id="1a533-112">Zie [Maak vandaag nog uw gratis Azure-account](https://azure.microsoft.com/pricing/free-trial/) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="1a533-112">For more information, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

* <span data-ttu-id="1a533-113">Visual Studio met Xamarin.</span><span class="sxs-lookup"><span data-stu-id="1a533-113">Visual Studio with Xamarin.</span></span> <span data-ttu-id="1a533-114">Zie [Setup and install](https://msdn.microsoft.com/library/mt613162.aspx) (Configureren en installeren) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="1a533-114">For information, see the [Set up and install Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) page.</span></span>

* <span data-ttu-id="1a533-115">Een Mac met Xcode v7.0 of hoger en waarop Xamarin Studio Community is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="1a533-115">A Mac with Xcode v7.0 or later and Xamarin Studio Community installed.</span></span> <span data-ttu-id="1a533-116">Zie [Setup and install](https://msdn.microsoft.com/library/mt613162.aspx) (Configureren en installeren) en [Setup, install, and verifications for Mac users](https://msdn.microsoft.com/library/mt488770.aspx) (Instructies voor installatie, configuratie en verificatie voor Mac-gebruikers) (MSDN) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="1a533-116">For information, see [Set up and install Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) and [Set up, install, and verify for Mac users](https://msdn.microsoft.com/library/mt488770.aspx) (MSDN).</span></span>

## <a name="create-a-new-mobile-apps-back-end"></a><span data-ttu-id="1a533-117">Een nieuwe back-end voor Mobile Apps maken</span><span class="sxs-lookup"><span data-stu-id="1a533-117">Create a new Mobile Apps back end</span></span>

<span data-ttu-id="1a533-118">Doe het volgende om een nieuwe back-end voor Mobile Apps te maken:</span><span class="sxs-lookup"><span data-stu-id="1a533-118">To create a new Mobile Apps back end, do the following:</span></span>

[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service](../../includes/app-service-mobile-dotnet-backend-create-new-service.md)]

<span data-ttu-id="1a533-119">U hebt nu een back-end voor Mobile Apps ingesteld die uw mobiele clienttoepassingen kunnen gebruiken.</span><span class="sxs-lookup"><span data-stu-id="1a533-119">You have now set up a Mobile Apps back end that your mobile client applications can use.</span></span> <span data-ttu-id="1a533-120">Nu gaat u een serverproject downloaden voor een eenvoudige back-end voor takenlijsten en deze vervolgens publiceren naar Azure.</span><span class="sxs-lookup"><span data-stu-id="1a533-120">Next, you download a server project for a simple to-do list back end and then publish it to Azure.</span></span>

## <a name="configure-the-server-project"></a><span data-ttu-id="1a533-121">Het serverproject configureren</span><span class="sxs-lookup"><span data-stu-id="1a533-121">Configure the server project</span></span>

<span data-ttu-id="1a533-122">Doe het volgende om het serverproject te configureren voor het gebruik van de Node.js- of .NET-back-end:</span><span class="sxs-lookup"><span data-stu-id="1a533-122">To configure the server project to use either the Node.js or .NET back end, do the following:</span></span>

[!INCLUDE [app-service-mobile-configure-new-backend](../../includes/app-service-mobile-configure-new-backend.md)]

## <a name="download-and-run-the-xamarinforms-solution"></a><span data-ttu-id="1a533-123">De Xamarin.Forms-oplossing downloaden en uitvoeren</span><span class="sxs-lookup"><span data-stu-id="1a533-123">Download and run the Xamarin.Forms solution</span></span>

<span data-ttu-id="1a533-124">U kunt de oplossing op twee manieren downloaden.</span><span class="sxs-lookup"><span data-stu-id="1a533-124">You can download the solution in either of two ways.</span></span> <span data-ttu-id="1a533-125">Download de oplossing naar een Mac en open deze in Xamarin Studio of download naar een Windows-computer en open de oplossing in Visual Studio en gebruik een Mac in het netwerk om de iOS-app te bouwen.</span><span class="sxs-lookup"><span data-stu-id="1a533-125">Download it to a Mac and open it in Xamarin Studio, or download it to a Windows computer and open it in Visual Studio by using a networked Mac for building the iOS app.</span></span> <span data-ttu-id="1a533-126">Zie [Setup and install](https://msdn.microsoft.com/library/mt613162.aspx) (Configureren en installeren) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="1a533-126">For more information, see [Set up and install Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx).</span></span>

<span data-ttu-id="1a533-127">Ga als volgt te werk op een Mac of Windows-computer:</span><span class="sxs-lookup"><span data-stu-id="1a533-127">On a Mac or Windows computer, do the following:</span></span>

1. <span data-ttu-id="1a533-128">Ga naar de [Azure Portal].</span><span class="sxs-lookup"><span data-stu-id="1a533-128">Go to the [Azure portal].</span></span>

2. <span data-ttu-id="1a533-129">Ga op de blade **Instellingen** voor uw mobiele app naar **Mobiel** en selecteer **Aan de slag** > **Xamarin.Forms**.</span><span class="sxs-lookup"><span data-stu-id="1a533-129">On the **Settings** blade for your mobile app, under **Mobile**, select **Get Started** > **Xamarin.Forms**.</span></span> <span data-ttu-id="1a533-130">Selecteer **Een nieuwe app maken** onder **stap 3** en selecteer vervolgens **Downloaden**.</span><span class="sxs-lookup"><span data-stu-id="1a533-130">Under **step 3**, select  **Create a new app**, and then select **Download**.</span></span>

   <span data-ttu-id="1a533-131">Er wordt nu een project gedownload dat een clienttoepassing bevat die is verbonden met uw mobiele app.</span><span class="sxs-lookup"><span data-stu-id="1a533-131">This action downloads a project that contains a client application that's connected to your mobile app.</span></span> <span data-ttu-id="1a533-132">Sla het gecomprimeerde projectbestand op uw lokale computer op en noteer de opslaglocatie.</span><span class="sxs-lookup"><span data-stu-id="1a533-132">Save the compressed project file to your local computer, and make a note of where you save it.</span></span>

3. <span data-ttu-id="1a533-133">Pak het project uit dat u hebt gedownload en open het in Xamarin Studio (Mac) of Visual Studio (Windows).</span><span class="sxs-lookup"><span data-stu-id="1a533-133">Extract the project that you downloaded, and then open it in Xamarin Studio (Mac) or Visual Studio (Windows).</span></span>

   ![Uitgepakt project in Xamarin Studio][9]

   ![Uitgepakt project in Visual Studio][8]

## <a name="optional-run-the-ios-project"></a><span data-ttu-id="1a533-136">(Optioneel) Het iOS-project uitvoeren</span><span class="sxs-lookup"><span data-stu-id="1a533-136">(Optional) Run the iOS project</span></span>
<span data-ttu-id="1a533-137">In deze sectie gaat u het Xamarin iOS-project uitvoeren voor iOS-apparaten.</span><span class="sxs-lookup"><span data-stu-id="1a533-137">In this section, you run the Xamarin iOS project for iOS devices.</span></span> <span data-ttu-id="1a533-138">Als u niet met iOS-apparaten werkt, kunt u deze sectie overslaan.</span><span class="sxs-lookup"><span data-stu-id="1a533-138">You can skip this section if you are not working with iOS devices.</span></span>

#### <a name="in-xamarin-studio"></a><span data-ttu-id="1a533-139">In Xamarin Studio</span><span class="sxs-lookup"><span data-stu-id="1a533-139">In Xamarin Studio</span></span>
1. <span data-ttu-id="1a533-140">Klik met de rechtermuisknop op het iOS-project en selecteer vervolgens **Set As Startup Project**.</span><span class="sxs-lookup"><span data-stu-id="1a533-140">Right-click the iOS project, and then select **Set As Startup Project**.</span></span>

2. <span data-ttu-id="1a533-141">Selecteer **Start Debugging** in het menu **Run** om het project te bouwen en de app te starten in de iPhone-emulator.</span><span class="sxs-lookup"><span data-stu-id="1a533-141">On the **Run** menu, select **Start Debugging** to build the project and start the app in the iPhone emulator.</span></span>

#### <a name="in-visual-studio"></a><span data-ttu-id="1a533-142">In Visual Studio</span><span class="sxs-lookup"><span data-stu-id="1a533-142">In Visual Studio</span></span>
1. <span data-ttu-id="1a533-143">Klik met de rechtermuisknop op het iOS-project en selecteer vervolgens **Set as StartUp Project**.</span><span class="sxs-lookup"><span data-stu-id="1a533-143">Right-click the iOS project, and then select **Set as StartUp Project**.</span></span>

2. <span data-ttu-id="1a533-144">Selecteer **Configuration Manager** in het menu **Bouwen**.</span><span class="sxs-lookup"><span data-stu-id="1a533-144">On the **Build** menu, select **Configuration Manager**.</span></span>

3. <span data-ttu-id="1a533-145">Schakel in het dialoogvenster **Configuration Manager** de selectievakjes **Bouwen** en **Implementeren** in voor het iOS-project.</span><span class="sxs-lookup"><span data-stu-id="1a533-145">In the **Configuration Manager** dialog box, select the **Build** and **Deploy** check boxes next to the iOS project.</span></span>

4. <span data-ttu-id="1a533-146">Selecteer de toets **F5** om het project te bouwen en de app te starten in de iPhone-emulator.</span><span class="sxs-lookup"><span data-stu-id="1a533-146">To build the project and start the app in the iPhone emulator, select the **F5** key.</span></span>

   > [!NOTE]
   > <span data-ttu-id="1a533-147">Als u er problemen zijn met het bouwen van het project, voert u NuGet Package Manager uit om bij te werken naar de nieuwste versie van de Xamarin-ondersteuningspakketten.</span><span class="sxs-lookup"><span data-stu-id="1a533-147">If you have problems building the project, run the NuGet package manager and update to the latest version of the Xamarin support packages.</span></span> <span data-ttu-id="1a533-148">Het is mogelijk dat het even duurt voordat Quick Start-projecten zijn bijgewerkt naar de nieuwste versie.</span><span class="sxs-lookup"><span data-stu-id="1a533-148">Quickstart projects might be slow to update to the latest versions.</span></span>    
   >
   >

5. <span data-ttu-id="1a533-149">Typ zinvolle tekst in de app, zoals *Xamarin leren kennen*, en selecteer vervolgens het plusteken (**+**).</span><span class="sxs-lookup"><span data-stu-id="1a533-149">In the app, type meaningful text, such as *Learn Xamarin*, and then select the plus sign (**+**).</span></span>

    ![][10]

    <span data-ttu-id="1a533-150">Hierdoor wordt er een POST-aanvraag verzonden naar de nieuwe back-end voor Mobile Apps die wordt gehost in Azure.</span><span class="sxs-lookup"><span data-stu-id="1a533-150">This action sends a post request to the new Mobile Apps back end that's hosted in Azure.</span></span> <span data-ttu-id="1a533-151">Gegevens van de aanvraag worden opgenomen in de takentabel.</span><span class="sxs-lookup"><span data-stu-id="1a533-151">Data from the request is inserted into the TodoItem table.</span></span> <span data-ttu-id="1a533-152">Items die zijn opgeslagen in de tabel, worden geretourneerd door de back-end voor Mobile Apps en de gegevens worden weergegeven in de lijst.</span><span class="sxs-lookup"><span data-stu-id="1a533-152">Items that are stored in the table are returned by the Mobile Apps back end, and the data is displayed in the list.</span></span>

    > [!NOTE]
    > <span data-ttu-id="1a533-153">U vindt de code die toegang geeft tot de back-end voor Mobile Apps in het bestand TodoItemManager.cs C# van het 'portable class library'-project van uw oplossing.</span><span class="sxs-lookup"><span data-stu-id="1a533-153">You'll find the code that accesses your Mobile Apps back end in the TodoItemManager.cs C# file of the portable class library project of your solution.</span></span>
    >
    >

## <a name="optional-run-the-android-project"></a><span data-ttu-id="1a533-154">(Optioneel) Het Android-project uitvoeren</span><span class="sxs-lookup"><span data-stu-id="1a533-154">(Optional) Run the Android project</span></span>
<span data-ttu-id="1a533-155">In deze sectie gaat u het Xamarin Droid-project voor Android uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="1a533-155">In this section, you run the Xamarin droid project for Android.</span></span> <span data-ttu-id="1a533-156">Als u niet met Android-apparaten werkt, kunt u deze sectie overslaan.</span><span class="sxs-lookup"><span data-stu-id="1a533-156">You can skip this section if you are not working with Android devices.</span></span>

#### <a name="in-xamarin-studio"></a><span data-ttu-id="1a533-157">In Xamarin Studio</span><span class="sxs-lookup"><span data-stu-id="1a533-157">In Xamarin Studio</span></span>

1. <span data-ttu-id="1a533-158">Klik met de rechtermuisknop op het Android-project en selecteer vervolgens **Set As Startup Project**.</span><span class="sxs-lookup"><span data-stu-id="1a533-158">Right-click the Android project, and then select **Set As Startup Project**.</span></span>

2. <span data-ttu-id="1a533-159">Selecteer **Start Debugging** in het menu **Run** om het project te bouwen en de app te starten in een Android-emulator.</span><span class="sxs-lookup"><span data-stu-id="1a533-159">To build the project and start the app in an Android emulator, on the **Run** menu, select **Start Debugging**.</span></span>

#### <a name="in-visual-studio"></a><span data-ttu-id="1a533-160">In Visual Studio</span><span class="sxs-lookup"><span data-stu-id="1a533-160">In Visual Studio</span></span>

1. <span data-ttu-id="1a533-161">Klik met de rechtermuisknop op het Android-project (Droid) en selecteer vervolgens **Instellen als opstartproject**.</span><span class="sxs-lookup"><span data-stu-id="1a533-161">Right-click the Android (Droid) project, and then select **Set as StartUp Project**.</span></span>

2. <span data-ttu-id="1a533-162">Selecteer **Configuration Manager** in het menu **Bouwen**.</span><span class="sxs-lookup"><span data-stu-id="1a533-162">On the **Build** menu, select **Configuration Manager**.</span></span>

3. <span data-ttu-id="1a533-163">Schakel in het dialoogvenster **Configuration Manager** de selectievakjes **Bouwen** en **Implementeren** in voor het Android-project.</span><span class="sxs-lookup"><span data-stu-id="1a533-163">In the **Configuration Manager** dialog box, select the **Build** and **Deploy** check boxes next to the Android project.</span></span>

4. <span data-ttu-id="1a533-164">Selecteer de toets **F5** om het project te bouwen en de apps te starten in een Android-emulator.</span><span class="sxs-lookup"><span data-stu-id="1a533-164">To build the project and start the app in an Android emulator, select the **F5** key.</span></span>

   > [!NOTE]
   > <span data-ttu-id="1a533-165">Als u er problemen zijn met het bouwen van het project, voert u NuGet Package Manager uit om bij te werken naar de nieuwste versie van de Xamarin-ondersteuningspakketten.</span><span class="sxs-lookup"><span data-stu-id="1a533-165">If you have problems building the project, run the NuGet package manager and update to the latest version of the Xamarin support packages.</span></span> <span data-ttu-id="1a533-166">Het is mogelijk dat het even duurt voordat Quick Start-projecten zijn bijgewerkt naar de nieuwste versie.</span><span class="sxs-lookup"><span data-stu-id="1a533-166">Quickstart projects might be slow to update to the latest versions.</span></span>    
   >
   >

5. <span data-ttu-id="1a533-167">Typ zinvolle tekst in de app, zoals *Xamarin leren kennen*, en selecteer vervolgens het plusteken (**+**).</span><span class="sxs-lookup"><span data-stu-id="1a533-167">In the app, type meaningful text, such as *Learn Xamarin*, and then select the plus sign (**+**).</span></span>

    ![][11]
    
    <span data-ttu-id="1a533-168">Hierdoor wordt er een POST-aanvraag verzonden naar de nieuwe back-end voor Mobile Apps die wordt gehost in Azure.</span><span class="sxs-lookup"><span data-stu-id="1a533-168">This action sends a post request to the new Mobile Apps back end that's hosted in Azure.</span></span> <span data-ttu-id="1a533-169">Gegevens van de aanvraag worden opgenomen in de takentabel.</span><span class="sxs-lookup"><span data-stu-id="1a533-169">Data from the request is inserted into the TodoItem table.</span></span> <span data-ttu-id="1a533-170">Items die zijn opgeslagen in de tabel, worden geretourneerd door de back-end voor Mobile Apps en de gegevens worden weergegeven in de lijst.</span><span class="sxs-lookup"><span data-stu-id="1a533-170">Items that are stored in the table are returned by the Mobile Apps back end, and the data is displayed in the list.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="1a533-171">U vindt de code die toegang geeft tot de back-end voor Mobile Apps in het bestand TodoItemManager.cs C# van het 'portable class library'-project van uw oplossing.</span><span class="sxs-lookup"><span data-stu-id="1a533-171">You'll find the code that accesses your Mobile Apps back end in the TodoItemManager.cs C# file of the portable class library project of your solution.</span></span>
    >
    >

## <a name="optional-run-the-windows-project"></a><span data-ttu-id="1a533-172">(Optioneel) Het Windows-project uitvoeren</span><span class="sxs-lookup"><span data-stu-id="1a533-172">(Optional) Run the Windows project</span></span>

<span data-ttu-id="1a533-173">In deze sectie gaat u het project Xamarin WinApp uitvoeren voor Windows-apparaten.</span><span class="sxs-lookup"><span data-stu-id="1a533-173">In this section, you run the Xamarin WinApp project for Windows devices.</span></span> <span data-ttu-id="1a533-174">Als u niet met Windows-apparaten werkt, kunt u deze sectie overslaan.</span><span class="sxs-lookup"><span data-stu-id="1a533-174">You can skip this section if you are not working with Windows devices.</span></span>

#### <a name="in-visual-studio"></a><span data-ttu-id="1a533-175">In Visual Studio</span><span class="sxs-lookup"><span data-stu-id="1a533-175">In Visual Studio</span></span>

1. <span data-ttu-id="1a533-176">Klik met de rechtermuisknop op een van de Windows-projecten en selecteer vervolgens **Instellen als opstartproject**.</span><span class="sxs-lookup"><span data-stu-id="1a533-176">Right-click any of the Windows projects, and then select **Set as StartUp Project**.</span></span>

2. <span data-ttu-id="1a533-177">Selecteer **Configuration Manager** in het menu **Bouwen**.</span><span class="sxs-lookup"><span data-stu-id="1a533-177">On the **Build** menu, select **Configuration Manager**.</span></span>

3. <span data-ttu-id="1a533-178">Schakel in het dialoogvenster **Configuration Manager** de selectievakjes **Bouwen** en **Implementeren** in van het Windows-project dat u hebt gekozen.</span><span class="sxs-lookup"><span data-stu-id="1a533-178">In the **Configuration Manager** dialog box, select the **Build** and **Deploy** check boxes next to the Windows project that you chose.</span></span>

4. <span data-ttu-id="1a533-179">Selecteer de toets **F5** om het project te bouwen en de apps te starten in een Windows-emulator.</span><span class="sxs-lookup"><span data-stu-id="1a533-179">To build the project and start the app in a Windows emulator, select the **F5** key.</span></span>

   > [!NOTE]
   > <span data-ttu-id="1a533-180">Als u er problemen zijn met het bouwen van het project, voert u NuGet Package Manager uit om bij te werken naar de nieuwste versie van de Xamarin-ondersteuningspakketten.</span><span class="sxs-lookup"><span data-stu-id="1a533-180">If you have problems building the project, run the NuGet package manager and update to the latest version of the Xamarin support packages.</span></span> <span data-ttu-id="1a533-181">Het is mogelijk dat het even duurt voordat Quick Start-projecten zijn bijgewerkt naar de nieuwste versie.</span><span class="sxs-lookup"><span data-stu-id="1a533-181">Quickstart projects might be slow to update to the latest versions.</span></span>    
   >
   >

5. <span data-ttu-id="1a533-182">Typ zinvolle tekst in de app, zoals *Xamarin leren kennen*, en selecteer vervolgens het plusteken (**+**).</span><span class="sxs-lookup"><span data-stu-id="1a533-182">In the app, type meaningful text, such as *Learn Xamarin*, and then select the plus sign (**+**).</span></span>

    <span data-ttu-id="1a533-183">Hierdoor wordt er een POST-aanvraag verzonden naar de nieuwe back-end voor Mobile Apps die wordt gehost in Azure.</span><span class="sxs-lookup"><span data-stu-id="1a533-183">This action sends a post request to the new Mobile Apps back end that's hosted in Azure.</span></span> <span data-ttu-id="1a533-184">Gegevens van de aanvraag worden opgenomen in de takentabel.</span><span class="sxs-lookup"><span data-stu-id="1a533-184">Data from the request is inserted into the TodoItem table.</span></span> <span data-ttu-id="1a533-185">Items die zijn opgeslagen in de tabel, worden geretourneerd door de back-end voor Mobile Apps en de gegevens worden weergegeven in de lijst.</span><span class="sxs-lookup"><span data-stu-id="1a533-185">Items that are stored in the table are returned by the Mobile Apps back end, and the data is displayed in the list.</span></span>
    
    ![][12]
    
    > [!NOTE]
    > <span data-ttu-id="1a533-186">U vindt de code die toegang geeft tot de back-end voor Mobile Apps in het bestand TodoItemManager.cs C# van het 'portable class library'-project van uw oplossing.</span><span class="sxs-lookup"><span data-stu-id="1a533-186">You'll find the code that accesses your Mobile Apps back end in the TodoItemManager.cs C# file of the portable class library project of your solution.</span></span>
    >
    >

## <a name="next-steps"></a><span data-ttu-id="1a533-187">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="1a533-187">Next steps</span></span>

* [<span data-ttu-id="1a533-188">Verificatie toevoegen aan uw app</span><span class="sxs-lookup"><span data-stu-id="1a533-188">Add authentication to your app</span></span>](app-service-mobile-xamarin-forms-get-started-users.md)  
  <span data-ttu-id="1a533-189">Ontdek hoe u gebruikers van uw app verifieert met een id-provider.</span><span class="sxs-lookup"><span data-stu-id="1a533-189">Learn how to authenticate users of your app with an identity provider.</span></span>

* [<span data-ttu-id="1a533-190">Pushmeldingen toevoegen aan uw app</span><span class="sxs-lookup"><span data-stu-id="1a533-190">Add push notifications to your app</span></span>](app-service-mobile-xamarin-forms-get-started-push.md)  
  <span data-ttu-id="1a533-191">Lees hoe u ondersteuning voor pushmeldingen toevoegt aan uw app en de backend voor Mobile Apps configureert voor het gebruik van Azure Notification Hubs voor het verzenden van pushmeldingen.</span><span class="sxs-lookup"><span data-stu-id="1a533-191">Learn how to add push notifications support to your app and configure your Mobile Apps back end to use Azure Notification Hubs to send the push notifications.</span></span>

* [<span data-ttu-id="1a533-192">Offlinesynchronisatie voor uw app inschakelen</span><span class="sxs-lookup"><span data-stu-id="1a533-192">Enable offline sync for your app</span></span>](app-service-mobile-xamarin-forms-get-started-offline-data.md)  
  <span data-ttu-id="1a533-193">Ontdek hoe u offlineondersteuning voor uw app toevoegt met behulp van een back-end voor Mobile Apps.</span><span class="sxs-lookup"><span data-stu-id="1a533-193">Learn how to add offline support for your app by using a Mobile Apps back end.</span></span> <span data-ttu-id="1a533-194">Offline synchroniseren zorgt ervoor dat u gegevens van een mobiele app kunt weergeven, toevoegen of wijzigen, zelfs als er geen netwerkverbinding is.</span><span class="sxs-lookup"><span data-stu-id="1a533-194">With offline sync, you can view, add, or modify your mobile app's data, even when there is no network connection.</span></span>

* [<span data-ttu-id="1a533-195">De beheerde client gebruiken voor Azure Mobile Apps</span><span class="sxs-lookup"><span data-stu-id="1a533-195">Use the managed client for Mobile Apps</span></span>](app-service-mobile-dotnet-how-to-use-client-library.md)  
  <span data-ttu-id="1a533-196">Informatie over het werken met SDK voor beheerde clients in uw Xamarin-app.</span><span class="sxs-lookup"><span data-stu-id="1a533-196">Learn how to work with the managed client SDK in your Xamarin app.</span></span>

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
[Azure Portal]: https://portal.azure.com/

---
title: Azure AD v2 Windows Desktop ophalen gestart - instellingen | Microsoft Docs
description: Hoe Windows Desktop .NET (XAML) toepassingen een API waarvoor toegangstokens door Azure Active Directory-v2-eindpunt kunnen aanroepen
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.assetid: 820acdb7-d316-4c3b-8de9-79df48ba3b06
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andret
ms.custom: aaddev
ms.openlocfilehash: 4065727aef04d7969d438c6ef79127bb44568be1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
## <a name="set-up-your-project"></a><span data-ttu-id="e0730-103">Instellen van uw project</span><span class="sxs-lookup"><span data-stu-id="e0730-103">Set up your project</span></span>

<span data-ttu-id="e0730-104">Deze sectie bevat stapsgewijze instructies voor het maken van een nieuw project te laten zien hoe u een Windows Desktop .NET-toepassing (XAML) worden geïntegreerd met *aanmelden met Microsoft* zodat Web-API's waarvoor een token op te vragen.</span><span class="sxs-lookup"><span data-stu-id="e0730-104">This section provides step-by-step instructions for how to create a new project to demonstrate how to integrate a Windows Desktop .NET application (XAML) with *Sign-In with Microsoft* so it can query Web APIs that requires a token.</span></span>

<span data-ttu-id="e0730-105">De toepassing gemaakt door deze handleiding beschrijft een knop om een grafiek en resultaten weergeven op het scherm een knop Afmelden.</span><span class="sxs-lookup"><span data-stu-id="e0730-105">The application created by this guide exposes a button to graph and show results on screen and a sign-out button.</span></span>

> <span data-ttu-id="e0730-106">Voorkeur voor het downloaden van dit voorbeeld Visual Studio-project in plaats daarvan?</span><span class="sxs-lookup"><span data-stu-id="e0730-106">Prefer to download this sample's Visual Studio project instead?</span></span> <span data-ttu-id="e0730-107">[Downloaden van een project](https://github.com/Azure-Samples/active-directory-dotnet-desktop-msgraph-v2/archive/master.zip) en doorgaan met de [configuratiestap](#create-an-application-express) voor het configureren van het codevoorbeeld voordat wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="e0730-107">[Download a project](https://github.com/Azure-Samples/active-directory-dotnet-desktop-msgraph-v2/archive/master.zip) and skip to the [Configuration step](#create-an-application-express) to configure the code sample before executing.</span></span>


### <a name="create-your-application"></a><span data-ttu-id="e0730-108">Uw toepassing maken</span><span class="sxs-lookup"><span data-stu-id="e0730-108">Create your application</span></span>
1. <span data-ttu-id="e0730-109">In Visual Studio:`File` > `New` > `Project`</span><span class="sxs-lookup"><span data-stu-id="e0730-109">In Visual Studio: `File` > `New` > `Project`</span></span><br/>
2. <span data-ttu-id="e0730-110">Onder *sjablonen*, selecteer`Visual C#`</span><span class="sxs-lookup"><span data-stu-id="e0730-110">Under *Templates*, select `Visual C#`</span></span>
3. <span data-ttu-id="e0730-111">Selecteer `WPF App` (of *WPF-toepassing* afhankelijk van de versie van uw Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="e0730-111">Select `WPF App` (or *WPF Application* depending on the version of your Visual Studio)</span></span>

## <a name="add-the-microsoft-authentication-library-msal-to-your-project"></a><span data-ttu-id="e0730-112">De Microsoft Authentication Library (MSAL) toevoegen aan uw project</span><span class="sxs-lookup"><span data-stu-id="e0730-112">Add the Microsoft Authentication Library (MSAL) to your project</span></span>
1. <span data-ttu-id="e0730-113">In Visual Studio:`Tools` > `Nuget Package Manager` > `Package Manager Console`</span><span class="sxs-lookup"><span data-stu-id="e0730-113">In Visual Studio: `Tools` > `Nuget Package Manager` > `Package Manager Console`</span></span>
2. <span data-ttu-id="e0730-114">Kopiëren en plakken in het venster Package Manager-Console het volgende:</span><span class="sxs-lookup"><span data-stu-id="e0730-114">Copy/paste the following in the Package Manager Console window:</span></span>

```powershell
Install-Package Microsoft.Identity.Client -Pre
```

> <span data-ttu-id="e0730-115">Het bovenstaande pakket installeert de Microsoft Authentication Library (MSAL).</span><span class="sxs-lookup"><span data-stu-id="e0730-115">The package above installs the Microsoft Authentication Library (MSAL).</span></span> <span data-ttu-id="e0730-116">MSAL verwerkt aanschaf, opslaan in cache en gebruiker toskens gebruikt voor toegang tot API's die zijn beveiligd door Azure Active Directory-v2 te vernieuwen.</span><span class="sxs-lookup"><span data-stu-id="e0730-116">MSAL handles acquiring, caching and refreshing user toskens used to access APIs protected by Azure Active Directory v2.</span></span>

## <a name="add-the-code-to-initialize-msal"></a><span data-ttu-id="e0730-117">Voeg de code voor het initialiseren van MSAL</span><span class="sxs-lookup"><span data-stu-id="e0730-117">Add the code to initialize MSAL</span></span>
<span data-ttu-id="e0730-118">Deze stap helpt u bij het maken van een klasse voor het afhandelen van interactie met MSAL bibliotheek, zoals de verwerking van tokens.</span><span class="sxs-lookup"><span data-stu-id="e0730-118">This step will help you create a class to handle interaction with MSAL Library, such as handling of tokens.</span></span>

1. <span data-ttu-id="e0730-119">Open de `App.xaml.cs` -bestand en voeg de referentie voor MSAL bibliotheek toe aan de klasse:</span><span class="sxs-lookup"><span data-stu-id="e0730-119">Open the `App.xaml.cs` file and add the reference for MSAL library to the class:</span></span>

```csharp
using Microsoft.Identity.Client;
```
<!-- Workaround for Docs conversion bug -->
<ol start="2">
<li>
<span data-ttu-id="e0730-120">De klasse App bijwerken met het volgende:</span><span class="sxs-lookup"><span data-stu-id="e0730-120">Update the App class to the following:</span></span>
</li>
</ol>

```csharp
public partial class App : Application
{
    //Below is the clientId of your app registration. 
    //You have to replace the below with the Application Id for your app registration
    private static string ClientId = "your_client_id_here";

    public static PublicClientApplication PublicClientApp = new PublicClientApplication(ClientId);

}
```

## <a name="create-your-applications-ui"></a><span data-ttu-id="e0730-121">De gebruikersinterface van uw toepassing maken</span><span class="sxs-lookup"><span data-stu-id="e0730-121">Create your application’s UI</span></span>
<span data-ttu-id="e0730-122">De onderstaande sectie wordt beschreven hoe een toepassing een beveiligde back-endserver zoals Microsoft Graph kan een query.</span><span class="sxs-lookup"><span data-stu-id="e0730-122">The section below shows how an application can query a protected backend server like Microsoft Graph.</span></span> <span data-ttu-id="e0730-123">Een bestand MainWindow.xaml moet automatisch worden gemaakt als onderdeel van uw project-sjabloon.</span><span class="sxs-lookup"><span data-stu-id="e0730-123">A MainWindow.xaml file should automatically be created as a part of your project template.</span></span> <span data-ttu-id="e0730-124">Dit bestand voor dit bestand openen en volg de onderstaande instructies:</span><span class="sxs-lookup"><span data-stu-id="e0730-124">Open this file this file and then follow the instructions below:</span></span>

<span data-ttu-id="e0730-125">Vervangen van uw toepassing `<Grid>` worden met het volgende:</span><span class="sxs-lookup"><span data-stu-id="e0730-125">Replace your application’s `<Grid>` with be the following:</span></span>

```xml
<Grid>
    <StackPanel Background="Azure">
        <StackPanel Orientation="Horizontal" HorizontalAlignment="Right">
            <Button x:Name="CallGraphButton" Content="Call Microsoft Graph API" HorizontalAlignment="Right" Padding="5" Click="CallGraphButton_Click" Margin="5" FontFamily="Segoe Ui"/>
            <Button x:Name="SignOutButton" Content="Sign-Out" HorizontalAlignment="Right" Padding="5" Click="SignOutButton_Click" Margin="5" Visibility="Collapsed" FontFamily="Segoe Ui"/>
        </StackPanel>
        <Label Content="API Call Results" Margin="0,0,0,-5" FontFamily="Segoe Ui" />
        <TextBox x:Name="ResultText" TextWrapping="Wrap" MinHeight="120" Margin="5" FontFamily="Segoe Ui"/>
        <Label Content="Token Info" Margin="0,0,0,-5" FontFamily="Segoe Ui" />
        <TextBox x:Name="TokenInfoText" TextWrapping="Wrap" MinHeight="70" Margin="5" FontFamily="Segoe Ui"/>
    </StackPanel>
</Grid>
```

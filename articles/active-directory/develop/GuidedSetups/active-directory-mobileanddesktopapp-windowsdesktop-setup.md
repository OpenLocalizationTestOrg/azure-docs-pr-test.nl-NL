---
title: aaaAzure AD v2 Windows Desktop aan de slag - instellingen | Microsoft Docs
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
ms.openlocfilehash: 097ea99bef01e15edaa5ff914ff4e18392b77c5a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
## <a name="set-up-your-project"></a><span data-ttu-id="47e20-103">Instellen van uw project</span><span class="sxs-lookup"><span data-stu-id="47e20-103">Set up your project</span></span>

<span data-ttu-id="47e20-104">Deze sectie bevat stapsgewijze instructies voor het toocreate een nieuw project toodemonstrate hoe toointegrate een Windows-bureaublad .NET-toepassing (XAML) met *aanmelden met Microsoft* zodat deze Web-API's die een token vereist een query.</span><span class="sxs-lookup"><span data-stu-id="47e20-104">This section provides step-by-step instructions for how toocreate a new project toodemonstrate how toointegrate a Windows Desktop .NET application (XAML) with *Sign-In with Microsoft* so it can query Web APIs that requires a token.</span></span>

<span data-ttu-id="47e20-105">Hallo-toepassing die zijn gemaakt door deze handleiding beschrijft een knop toograph en weergeven van de resultaten op het scherm een knop Afmelden.</span><span class="sxs-lookup"><span data-stu-id="47e20-105">hello application created by this guide exposes a button toograph and show results on screen and a sign-out button.</span></span>

> <span data-ttu-id="47e20-106">Voorkeur toodownload dit voorbeeld Visual Studio-project in plaats daarvan?</span><span class="sxs-lookup"><span data-stu-id="47e20-106">Prefer toodownload this sample's Visual Studio project instead?</span></span> <span data-ttu-id="47e20-107">[Downloaden van een project](https://github.com/Azure-Samples/active-directory-dotnet-desktop-msgraph-v2/archive/master.zip) - en skip-toohello [configuratiestap](#create-an-application-express) tooconfigure Hallo codevoorbeeld voordat wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="47e20-107">[Download a project](https://github.com/Azure-Samples/active-directory-dotnet-desktop-msgraph-v2/archive/master.zip) and skip toohello [Configuration step](#create-an-application-express) tooconfigure hello code sample before executing.</span></span>


### <a name="create-your-application"></a><span data-ttu-id="47e20-108">Uw toepassing maken</span><span class="sxs-lookup"><span data-stu-id="47e20-108">Create your application</span></span>
1. <span data-ttu-id="47e20-109">In Visual Studio:`File` > `New` > `Project`</span><span class="sxs-lookup"><span data-stu-id="47e20-109">In Visual Studio: `File` > `New` > `Project`</span></span><br/>
2. <span data-ttu-id="47e20-110">Onder *sjablonen*, selecteer`Visual C#`</span><span class="sxs-lookup"><span data-stu-id="47e20-110">Under *Templates*, select `Visual C#`</span></span>
3. <span data-ttu-id="47e20-111">Selecteer `WPF App` (of *WPF-toepassing* afhankelijk van het Hallo-versie van uw Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="47e20-111">Select `WPF App` (or *WPF Application* depending on hello version of your Visual Studio)</span></span>

## <a name="add-hello-microsoft-authentication-library-msal-tooyour-project"></a><span data-ttu-id="47e20-112">Hallo Microsoft Authentication Library (MSAL) tooyour project toevoegen</span><span class="sxs-lookup"><span data-stu-id="47e20-112">Add hello Microsoft Authentication Library (MSAL) tooyour project</span></span>
1. <span data-ttu-id="47e20-113">In Visual Studio:`Tools` > `Nuget Package Manager` > `Package Manager Console`</span><span class="sxs-lookup"><span data-stu-id="47e20-113">In Visual Studio: `Tools` > `Nuget Package Manager` > `Package Manager Console`</span></span>
2. <span data-ttu-id="47e20-114">De volgende hello, kopiëren en plakken in Hallo venster Package Manager Console:</span><span class="sxs-lookup"><span data-stu-id="47e20-114">Copy/paste hello following in hello Package Manager Console window:</span></span>

```powershell
Install-Package Microsoft.Identity.Client -Pre
```

> <span data-ttu-id="47e20-115">Hallo pakket bovenstaande installeert Hallo Microsoft Authentication Library (MSAL).</span><span class="sxs-lookup"><span data-stu-id="47e20-115">hello package above installs hello Microsoft Authentication Library (MSAL).</span></span> <span data-ttu-id="47e20-116">MSAL verwerkt aanschaf, opslaan in cache en vernieuwen van de gebruiker gebruikt toskens tooaccess beveiligd door Azure Active Directory-v2 API's.</span><span class="sxs-lookup"><span data-stu-id="47e20-116">MSAL handles acquiring, caching and refreshing user toskens used tooaccess APIs protected by Azure Active Directory v2.</span></span>

## <a name="add-hello-code-tooinitialize-msal"></a><span data-ttu-id="47e20-117">Hallo code tooinitialize MSAL toevoegen</span><span class="sxs-lookup"><span data-stu-id="47e20-117">Add hello code tooinitialize MSAL</span></span>
<span data-ttu-id="47e20-118">Deze stap helpt u bij het maken van een klasse toohandle interactie met MSAL-bibliotheek, zoals de verwerking van tokens.</span><span class="sxs-lookup"><span data-stu-id="47e20-118">This step will help you create a class toohandle interaction with MSAL Library, such as handling of tokens.</span></span>

1. <span data-ttu-id="47e20-119">Open Hallo `App.xaml.cs` bestand en het Hallo-verwijzing voor MSAL bibliotheek toohello klasse toevoegen:</span><span class="sxs-lookup"><span data-stu-id="47e20-119">Open hello `App.xaml.cs` file and add hello reference for MSAL library toohello class:</span></span>

```csharp
using Microsoft.Identity.Client;
```
<!-- Workaround for Docs conversion bug -->
<ol start="2">
<li>
<span data-ttu-id="47e20-120">Hallo App klasse toohello volgende update:</span><span class="sxs-lookup"><span data-stu-id="47e20-120">Update hello App class toohello following:</span></span>
</li>
</ol>

```csharp
public partial class App : Application
{
    //Below is hello clientId of your app registration. 
    //You have tooreplace hello below with hello Application Id for your app registration
    private static string ClientId = "your_client_id_here";

    public static PublicClientApplication PublicClientApp = new PublicClientApplication(ClientId);

}
```

## <a name="create-your-applications-ui"></a><span data-ttu-id="47e20-121">De gebruikersinterface van uw toepassing maken</span><span class="sxs-lookup"><span data-stu-id="47e20-121">Create your application’s UI</span></span>
<span data-ttu-id="47e20-122">Hallo hieronder ziet u hoe een toepassing een beveiligde back-endserver zoals Microsoft Graph kan een query.</span><span class="sxs-lookup"><span data-stu-id="47e20-122">hello section below shows how an application can query a protected backend server like Microsoft Graph.</span></span> <span data-ttu-id="47e20-123">Een bestand MainWindow.xaml moet automatisch worden gemaakt als onderdeel van uw project-sjabloon.</span><span class="sxs-lookup"><span data-stu-id="47e20-123">A MainWindow.xaml file should automatically be created as a part of your project template.</span></span> <span data-ttu-id="47e20-124">Dit bestand voor dit bestand openen en volg de onderstaande instructies voor Hallo:</span><span class="sxs-lookup"><span data-stu-id="47e20-124">Open this file this file and then follow hello instructions below:</span></span>

<span data-ttu-id="47e20-125">Vervangen van uw toepassing `<Grid>` worden met de volgende Hallo:</span><span class="sxs-lookup"><span data-stu-id="47e20-125">Replace your application’s `<Grid>` with be hello following:</span></span>

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

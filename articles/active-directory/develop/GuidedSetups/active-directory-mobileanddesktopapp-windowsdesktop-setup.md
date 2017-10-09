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
## <a name="set-up-your-project"></a>Instellen van uw project

Deze sectie bevat stapsgewijze instructies voor het toocreate een nieuw project toodemonstrate hoe toointegrate een Windows-bureaublad .NET-toepassing (XAML) met *aanmelden met Microsoft* zodat deze Web-API's die een token vereist een query.

Hallo-toepassing die zijn gemaakt door deze handleiding beschrijft een knop toograph en weergeven van de resultaten op het scherm een knop Afmelden.

> Voorkeur toodownload dit voorbeeld Visual Studio-project in plaats daarvan? [Downloaden van een project](https://github.com/Azure-Samples/active-directory-dotnet-desktop-msgraph-v2/archive/master.zip) - en skip-toohello [configuratiestap](#create-an-application-express) tooconfigure Hallo codevoorbeeld voordat wordt uitgevoerd.


### <a name="create-your-application"></a>Uw toepassing maken
1. In Visual Studio:`File` > `New` > `Project`<br/>
2. Onder *sjablonen*, selecteer`Visual C#`
3. Selecteer `WPF App` (of *WPF-toepassing* afhankelijk van het Hallo-versie van uw Visual Studio)

## <a name="add-hello-microsoft-authentication-library-msal-tooyour-project"></a>Hallo Microsoft Authentication Library (MSAL) tooyour project toevoegen
1. In Visual Studio:`Tools` > `Nuget Package Manager` > `Package Manager Console`
2. De volgende hello, kopiëren en plakken in Hallo venster Package Manager Console:

```powershell
Install-Package Microsoft.Identity.Client -Pre
```

> Hallo pakket bovenstaande installeert Hallo Microsoft Authentication Library (MSAL). MSAL verwerkt aanschaf, opslaan in cache en vernieuwen van de gebruiker gebruikt toskens tooaccess beveiligd door Azure Active Directory-v2 API's.

## <a name="add-hello-code-tooinitialize-msal"></a>Hallo code tooinitialize MSAL toevoegen
Deze stap helpt u bij het maken van een klasse toohandle interactie met MSAL-bibliotheek, zoals de verwerking van tokens.

1. Open Hallo `App.xaml.cs` bestand en het Hallo-verwijzing voor MSAL bibliotheek toohello klasse toevoegen:

```csharp
using Microsoft.Identity.Client;
```
<!-- Workaround for Docs conversion bug -->
<ol start="2">
<li>
Hallo App klasse toohello volgende update:
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

## <a name="create-your-applications-ui"></a>De gebruikersinterface van uw toepassing maken
Hallo hieronder ziet u hoe een toepassing een beveiligde back-endserver zoals Microsoft Graph kan een query. Een bestand MainWindow.xaml moet automatisch worden gemaakt als onderdeel van uw project-sjabloon. Dit bestand voor dit bestand openen en volg de onderstaande instructies voor Hallo:

Vervangen van uw toepassing `<Grid>` worden met de volgende Hallo:

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

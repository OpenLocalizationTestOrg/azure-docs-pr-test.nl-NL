---
title: aaaAzure AD v2 Windows Desktop aan de slag - Config | Microsoft Docs
description: Hoe een toepassing .NET Windows-bureaublad (XAML) ophalen van een toegangstoken en een API die wordt beveiligd door Azure Active Directory-v2-eindpunt niet aanroepen. | Microsoft Azure | Microsoft Azure
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
ms.openlocfilehash: 39c257e3e0cb09491f6fe005877601bd46824d12
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
## <a name="create-an-application-express"></a>Maken van een toepassing (snelle)
Nu u uw toepassing in Hallo tooregister moet *Portal voor registratie van Microsoft-toepassing*:
1. Registreren van uw toepassing via Hallo [Portal voor registratie van Microsoft-toepassing](https://apps.dev.microsoft.com/portal/register-app?appType=mobileAndDesktopApp&appTech=windowsDesktop&step=configure)
2.  Voer een naam voor uw toepassing en uw e-mailadres
3.  Zorg ervoor dat de optie Hallo voor begeleide Setup is ingeschakeld
4.  Ga als volgt Hallo instructies tooobtain Hallo toepassings-ID en plak deze in uw code

### <a name="add-your-application-registration-information-tooyour-solution-advanced"></a>Toevoegen van uw toepassing registratie informatie tooyour oplossing (Geavanceerd)
Nu u uw toepassing in Hallo tooregister moet *Portal voor registratie van Microsoft-toepassing*:
1. Ga toohello [Portal voor registratie van Microsoft-toepassing](https://apps.dev.microsoft.com/portal/register-app) tooregister een toepassing
2. Voer een naam voor uw toepassing en uw e-mailadres 
3. Zorg ervoor dat de optie Hallo voor begeleide Setup is uitgeschakeld
4. Klik op `Add Platform`, selecteer daarna `Native Application` en klik op Opslaan
5. Hallo GUID kopiëren in toepassings-ID, gaat u terug tooVisual Studio open `App.xaml.cs` en vervang `your_client_id_here` Hello toepassings-ID die u zojuist hebt geregistreerd:

```csharp
private static string ClientId = "your_application_id_here";
```

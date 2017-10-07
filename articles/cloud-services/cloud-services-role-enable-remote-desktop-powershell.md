---
title: aaaEnable verbinding met extern bureaublad voor een rol in Azure Cloud Services met behulp van PowerShell
description: Hoe tooconfigure uw azure cloud servicetoepassing met behulp van PowerShell tooallow extern bureaublad-verbindingen
services: cloud-services
documentationcenter: 
author: thraka
manager: timlt
editor: 
ms.assetid: bf2f70a4-20dc-4302-a91a-38cd7a2baa62
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: adegeo
ms.openlocfilehash: 3f46b014f29f1c0be0e1b485d2f0152424162bb2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="enable-remote-desktop-connection-for-a-role-in-azure-cloud-services-using-powershell"></a>Verbinding met extern bureaublad inschakelen voor een rol in Azure Cloud Services met behulp van PowerShell
> [!div class="op_single_selector"]
> * [Azure Portal](cloud-services-role-enable-remote-desktop-new-portal.md)
> * [Klassieke Azure Portal](cloud-services-role-enable-remote-desktop.md)
> * [PowerShell](cloud-services-role-enable-remote-desktop-powershell.md)
> * [Visual Studio](../vs-azure-tools-remote-desktop-roles.md)
>
>

Extern bureaublad kunt u tooaccess Hallo bureaublad van een functie die wordt uitgevoerd in Azure. U kunt een tootroubleshoot extern bureaublad-verbinding gebruiken en analyseren van problemen met uw toepassing, terwijl deze wordt uitgevoerd.

Dit artikel wordt beschreven hoe tooenable extern bureaublad op uw Cloud Service-rollen met behulp van PowerShell. Zie [hoe tooinstall en configureren van Azure PowerShell](/powershell/azure/overview) voor Hallo vereisten die nodig zijn voor dit artikel. PowerShell maakt gebruik van extern bureaublad-extensie Hallo zodat u extern bureaublad inschakelen kunt nadat de toepassing hello wordt geïmplementeerd.

## <a name="configure-remote-desktop-from-powershell"></a>Extern bureaublad vanuit PowerShell configureren
Hallo [Set AzureServiceRemoteDesktopExtension](/powershell/module/azure/set-azureserviceremotedesktopextension?view=azuresmps-3.7.0) cmdlet kunt u tooenable extern bureaublad op de opgegeven rollen of alle rollen van uw cloud service-implementatie. Hallo-cmdlet kunt u hello gebruikersnaam en wachtwoord opgeven voor Hallo externe bureaubladgebruiker via Hallo *referentie* parameter een PSCredential-object accepteert.

Als u PowerShell interactief gebruikt, kunt u eenvoudig hello PSCredential-object instellen door de aanroepende Hallo [Get-referenties](https://technet.microsoft.com/library/hh849815.aspx) cmdlet.

```
$remoteusercredentials = Get-Credential
```

Deze opdracht wordt een dialoogvenster zodat u tooenter Hallo gebruikersnaam en wachtwoord voor de externe gebruiker Hallo op een veilige manier weergegeven.

Aangezien PowerShell in automation scenario's helpt, kunt u ook instellen Hallo **PSCredential** object op een manier die geen tussenkomst van de gebruiker vereist. U moet eerst tooset van een beveiligd wachtwoord. U begint met een wachtwoord als tekst zonder opmaak converteren tooa beveiligde tekenreeks opgeven met behulp van [ConvertTo-SecureString](https://technet.microsoft.com/library/hh849818.aspx). Vervolgens dient u tooconvert deze beveiligde tekenreeks in een versleutelde standaardtekenreeks met [ConverterenVan SecureString](https://technet.microsoft.com/library/hh849814.aspx). Nu kunt u deze versleutelde standaardtekenreeks tooa-bestand met opslaan [Set inhoud](https://technet.microsoft.com/library/ee176959.aspx).

U kunt ook een bestand beveiligd wachtwoord maken, zodat er geen tootype in Hallo wachtwoord elke keer. Er is ook een bestand beveiligd wachtwoord beter dan een tekstbestand. Gebruik Hallo PowerShell toocreate een bestand beveiligd wachtwoord te volgen:

```
ConvertTo-SecureString -String "Password123" -AsPlainText -Force | ConvertFrom-SecureString | Set-Content "password.txt"
```

> [!IMPORTANT]
> Bij het Hallo-wachtwoord instellen, zorg ervoor dat u voldoet aan de Hallo [complexiteitsvereisten](https://technet.microsoft.com/library/cc786468.aspx).
>
>

Hallo referentieobject toocreate uit Hallo beveiligd wachtwoordbestand, die u moet Hallo bestandsinhoud lezen en te zetten back tooa beveiligen met behulp van tekenreeks [ConvertTo-SecureString](https://technet.microsoft.com/library/hh849818.aspx).

Hallo [Set AzureServiceRemoteDesktopExtension](/powershell/module/azure/set-azureserviceremotedesktopextension?view=azuresmps-3.7.0) cmdlet accepteert ook een *verlopen* parameter waarmee een **DateTime** op welke gebruiker Hallo account verloopt. Bijvoorbeeld, kunt u instellen Hallo account tooexpire een paar dagen van Hallo huidige datum en tijd.

Dit PowerShell-voorbeeld ziet u hoe tooset extern bureaublad-extensie Hallo op een cloudservice:

```
$servicename = "cloudservice"
$username = "RemoteDesktopUser"
$securepassword = Get-Content -Path "password.txt" | ConvertTo-SecureString
$expiry = $(Get-Date).AddDays(1)
$credential = New-Object System.Management.Automation.PSCredential $username,$securepassword
Set-AzureServiceRemoteDesktopExtension -ServiceName $servicename -Credential $credential -Expiration $expiry
```
U kunt eventueel ook Hallo implementatiesleuf en functies die u op de extern bureaublad tooenable wilt opgeven. Als deze parameters niet zijn opgegeven, Hallo cmdlet kunt Extern bureaublad op alle rollen in Hallo **productie** implementatiesleuf.

Hallo extern bureaublad-extensie is gekoppeld aan een implementatie. Als u een nieuwe implementatie voor Hallo service maakt, hebt u tooenable extern bureaublad op implementatie. Als u wilt dat altijd toohave extern bureaublad is ingeschakeld, moet vervolgens u PowerShell-scripts Hallo integreren in uw werkstroom voor de implementatie.

## <a name="remote-desktop-into-a-role-instance"></a>Extern bureaublad in een rolinstantie
Hallo [Get-AzureRemoteDesktopFile](/powershell/module/azure/get-azureremotedesktopfile?view=azuresmps-3.7.0) cmdlet gebruikte tooremote bureaublad in een specifieke rolexemplaar van de cloudservice is. U kunt Hallo *LocalPath* parameter toodownload Hallo RDP-bestand lokaal. Of u kunt Hallo *starten* parameter toodirectly starten Hallo verbinding met extern bureaublad dialoogvenster tooaccess Hallo rolinstantie cloud-service.

```
Get-AzureRemoteDesktopFile -ServiceName $servicename -Name "WorkerRole1_IN_0" -Launch
```


## <a name="check-if-remote-desktop-extension-is-enabled-on-a-service"></a>Controleer of de extern bureaublad-extensie is ingeschakeld voor een service
Hallo [Get-AzureServiceRemoteDesktopExtension](/powershell/module/azure/get-azureremotedesktopfile?view=azuresmps-3.7.0) cmdlet geeft weer die extern bureaublad is ingeschakeld of uitgeschakeld op een service-implementatie. Hallo cmdlet retourneert Hallo gebruikersnaam voor de externe bureaubladgebruiker hello en Hallo-functies die Hallo extern bureaublad-extensie is ingeschakeld voor. Dit gebeurt op Hallo implementatiesleuf en toouse hello faseringssleuven in plaats daarvan kunt u standaard.

```
Get-AzureServiceRemoteDesktopExtension -ServiceName $servicename
```

## <a name="remove-remote-desktop-extension-from-a-service"></a>Extern bureaublad-uitbreiding te verwijderen van een service
Als u al Hallo extern bureaublad-extensie op een implementatie hebt ingeschakeld en moet tooupdate Hallo instellingen voor extern bureaublad, eerst Hallo uitbreiding te verwijderen. En deze opnieuw inschakelen met de nieuwe instellingen Hallo. Als u wilt dat tooset verlopen bijvoorbeeld een nieuw wachtwoord voor het externe gebruikersaccount Hallo of Hallo-account. Dit is vereist op de bestaande implementaties die Hallo extern bureaublad-extensie ingeschakeld hebben. Voor nieuwe implementaties, kunt u Hallo extensie gewoon rechtstreeks toepassen.

tooremove Hallo extern bureaublad-extensie uit Hallo-implementatie, kunt u Hallo [verwijderen AzureServiceRemoteDesktopExtension](/powershell/module/azure/remove-azureserviceremotedesktopextension?view=azuresmps-3.7.0) cmdlet. U kunt eventueel ook Hallo implementatiesleuf en rol van waaruit u tooremove Hallo extern bureaublad-extensie wilt opgeven.

```
Remove-AzureServiceRemoteDesktopExtension -ServiceName $servicename -UninstallConfiguration
```

> [!NOTE]
> configuratie van toocompletely verwijderen Hallo uitbreiding, moet u Hallo aanroepen *verwijderen* cmdlet Hello **UninstallConfiguration** parameter.
>
> Hallo **UninstallConfiguration** parameter Hiermee verwijdert u de configuratie voor elke uitbreiding die toegepaste toohello service. De configuratie voor elke uitbreiding is gekoppeld aan het Hallo-serviceconfiguratie. Aanroepen Hallo *verwijderen* cmdlet zonder **UninstallConfiguration** instelt, scheidt u Hallo <mark>implementatie</mark> van configuratie van Hallo-uitbreiding, dus effectief verwijderen Hallo-extensie. Configuratie van de uitbreiding Hallo blijft echter gekoppeld aan Hallo-service.
>
>

## <a name="additional-resources"></a>Aanvullende bronnen

[Hoe tooConfigure Cloudservices](cloud-services-how-to-configure.md)
[extern bureaublad-services FAQ - Cloud](cloud-services-faq.md)

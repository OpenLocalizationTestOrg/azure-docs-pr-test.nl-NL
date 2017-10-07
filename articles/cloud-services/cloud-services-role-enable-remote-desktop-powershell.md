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
# <a name="enable-remote-desktop-connection-for-a-role-in-azure-cloud-services-using-powershell"></a><span data-ttu-id="ba33a-103">Verbinding met extern bureaublad inschakelen voor een rol in Azure Cloud Services met behulp van PowerShell</span><span class="sxs-lookup"><span data-stu-id="ba33a-103">Enable Remote Desktop Connection for a Role in Azure Cloud Services using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ba33a-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="ba33a-104">Azure portal</span></span>](cloud-services-role-enable-remote-desktop-new-portal.md)
> * [<span data-ttu-id="ba33a-105">Klassieke Azure Portal</span><span class="sxs-lookup"><span data-stu-id="ba33a-105">Azure classic portal</span></span>](cloud-services-role-enable-remote-desktop.md)
> * [<span data-ttu-id="ba33a-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="ba33a-106">PowerShell</span></span>](cloud-services-role-enable-remote-desktop-powershell.md)
> * [<span data-ttu-id="ba33a-107">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="ba33a-107">Visual Studio</span></span>](../vs-azure-tools-remote-desktop-roles.md)
>
>

<span data-ttu-id="ba33a-108">Extern bureaublad kunt u tooaccess Hallo bureaublad van een functie die wordt uitgevoerd in Azure.</span><span class="sxs-lookup"><span data-stu-id="ba33a-108">Remote Desktop enables you tooaccess hello desktop of a role running in Azure.</span></span> <span data-ttu-id="ba33a-109">U kunt een tootroubleshoot extern bureaublad-verbinding gebruiken en analyseren van problemen met uw toepassing, terwijl deze wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="ba33a-109">You can use a Remote Desktop connection tootroubleshoot and diagnose problems with your application while it is running.</span></span>

<span data-ttu-id="ba33a-110">Dit artikel wordt beschreven hoe tooenable extern bureaublad op uw Cloud Service-rollen met behulp van PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ba33a-110">This article describes how tooenable remote desktop on your Cloud Service Roles using PowerShell.</span></span> <span data-ttu-id="ba33a-111">Zie [hoe tooinstall en configureren van Azure PowerShell](/powershell/azure/overview) voor Hallo vereisten die nodig zijn voor dit artikel.</span><span class="sxs-lookup"><span data-stu-id="ba33a-111">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for hello prerequisites needed for this article.</span></span> <span data-ttu-id="ba33a-112">PowerShell maakt gebruik van extern bureaublad-extensie Hallo zodat u extern bureaublad inschakelen kunt nadat de toepassing hello wordt geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="ba33a-112">PowerShell utilizes hello Remote Desktop Extension so you can enable Remote Desktop after hello application is deployed.</span></span>

## <a name="configure-remote-desktop-from-powershell"></a><span data-ttu-id="ba33a-113">Extern bureaublad vanuit PowerShell configureren</span><span class="sxs-lookup"><span data-stu-id="ba33a-113">Configure Remote Desktop from PowerShell</span></span>
<span data-ttu-id="ba33a-114">Hallo [Set AzureServiceRemoteDesktopExtension](/powershell/module/azure/set-azureserviceremotedesktopextension?view=azuresmps-3.7.0) cmdlet kunt u tooenable extern bureaublad op de opgegeven rollen of alle rollen van uw cloud service-implementatie.</span><span class="sxs-lookup"><span data-stu-id="ba33a-114">hello [Set-AzureServiceRemoteDesktopExtension](/powershell/module/azure/set-azureserviceremotedesktopextension?view=azuresmps-3.7.0) cmdlet allows you tooenable Remote Desktop on specified roles or all roles of your cloud service deployment.</span></span> <span data-ttu-id="ba33a-115">Hallo-cmdlet kunt u hello gebruikersnaam en wachtwoord opgeven voor Hallo externe bureaubladgebruiker via Hallo *referentie* parameter een PSCredential-object accepteert.</span><span class="sxs-lookup"><span data-stu-id="ba33a-115">hello cmdlet lets you specify hello Username and Password for hello remote desktop user through hello *Credential* parameter that accepts a PSCredential object.</span></span>

<span data-ttu-id="ba33a-116">Als u PowerShell interactief gebruikt, kunt u eenvoudig hello PSCredential-object instellen door de aanroepende Hallo [Get-referenties](https://technet.microsoft.com/library/hh849815.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="ba33a-116">If you are using PowerShell interactively, you can easily set hello PSCredential object by calling hello [Get-Credentials](https://technet.microsoft.com/library/hh849815.aspx) cmdlet.</span></span>

```
$remoteusercredentials = Get-Credential
```

<span data-ttu-id="ba33a-117">Deze opdracht wordt een dialoogvenster zodat u tooenter Hallo gebruikersnaam en wachtwoord voor de externe gebruiker Hallo op een veilige manier weergegeven.</span><span class="sxs-lookup"><span data-stu-id="ba33a-117">This command displays a dialog box allowing you tooenter hello username and password for hello remote user in a secure manner.</span></span>

<span data-ttu-id="ba33a-118">Aangezien PowerShell in automation scenario's helpt, kunt u ook instellen Hallo **PSCredential** object op een manier die geen tussenkomst van de gebruiker vereist.</span><span class="sxs-lookup"><span data-stu-id="ba33a-118">Since PowerShell helps in automation scenarios, you can also set up hello **PSCredential** object in a way that doesn't require user interaction.</span></span> <span data-ttu-id="ba33a-119">U moet eerst tooset van een beveiligd wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="ba33a-119">First, you need tooset up a secure password.</span></span> <span data-ttu-id="ba33a-120">U begint met een wachtwoord als tekst zonder opmaak converteren tooa beveiligde tekenreeks opgeven met behulp van [ConvertTo-SecureString](https://technet.microsoft.com/library/hh849818.aspx).</span><span class="sxs-lookup"><span data-stu-id="ba33a-120">You begin with specifying a plain text password convert it tooa secure string using [ConvertTo-SecureString](https://technet.microsoft.com/library/hh849818.aspx).</span></span> <span data-ttu-id="ba33a-121">Vervolgens dient u tooconvert deze beveiligde tekenreeks in een versleutelde standaardtekenreeks met [ConverterenVan SecureString](https://technet.microsoft.com/library/hh849814.aspx).</span><span class="sxs-lookup"><span data-stu-id="ba33a-121">Next you need tooconvert this secure string into an encrypted standard string using [ConvertFrom-SecureString](https://technet.microsoft.com/library/hh849814.aspx).</span></span> <span data-ttu-id="ba33a-122">Nu kunt u deze versleutelde standaardtekenreeks tooa-bestand met opslaan [Set inhoud](https://technet.microsoft.com/library/ee176959.aspx).</span><span class="sxs-lookup"><span data-stu-id="ba33a-122">Now you can save this encrypted standard string tooa file using [Set-Content](https://technet.microsoft.com/library/ee176959.aspx).</span></span>

<span data-ttu-id="ba33a-123">U kunt ook een bestand beveiligd wachtwoord maken, zodat er geen tootype in Hallo wachtwoord elke keer.</span><span class="sxs-lookup"><span data-stu-id="ba33a-123">You can also create a secure password file so that you don't have tootype in hello password every time.</span></span> <span data-ttu-id="ba33a-124">Er is ook een bestand beveiligd wachtwoord beter dan een tekstbestand.</span><span class="sxs-lookup"><span data-stu-id="ba33a-124">Also, a secure password file is better than a plain text file.</span></span> <span data-ttu-id="ba33a-125">Gebruik Hallo PowerShell toocreate een bestand beveiligd wachtwoord te volgen:</span><span class="sxs-lookup"><span data-stu-id="ba33a-125">Use hello following PowerShell toocreate a secure password file:</span></span>

```
ConvertTo-SecureString -String "Password123" -AsPlainText -Force | ConvertFrom-SecureString | Set-Content "password.txt"
```

> [!IMPORTANT]
> <span data-ttu-id="ba33a-126">Bij het Hallo-wachtwoord instellen, zorg ervoor dat u voldoet aan de Hallo [complexiteitsvereisten](https://technet.microsoft.com/library/cc786468.aspx).</span><span class="sxs-lookup"><span data-stu-id="ba33a-126">When setting hello password, make sure that you meet hello [complexity requirements](https://technet.microsoft.com/library/cc786468.aspx).</span></span>
>
>

<span data-ttu-id="ba33a-127">Hallo referentieobject toocreate uit Hallo beveiligd wachtwoordbestand, die u moet Hallo bestandsinhoud lezen en te zetten back tooa beveiligen met behulp van tekenreeks [ConvertTo-SecureString](https://technet.microsoft.com/library/hh849818.aspx).</span><span class="sxs-lookup"><span data-stu-id="ba33a-127">toocreate hello credential object from hello secure password file, you must read hello file contents and convert them back tooa secure string using [ConvertTo-SecureString](https://technet.microsoft.com/library/hh849818.aspx).</span></span>

<span data-ttu-id="ba33a-128">Hallo [Set AzureServiceRemoteDesktopExtension](/powershell/module/azure/set-azureserviceremotedesktopextension?view=azuresmps-3.7.0) cmdlet accepteert ook een *verlopen* parameter waarmee een **DateTime** op welke gebruiker Hallo account verloopt.</span><span class="sxs-lookup"><span data-stu-id="ba33a-128">hello [Set-AzureServiceRemoteDesktopExtension](/powershell/module/azure/set-azureserviceremotedesktopextension?view=azuresmps-3.7.0) cmdlet also accepts an *Expiration* parameter, which specifies a **DateTime** at which hello user account expires.</span></span> <span data-ttu-id="ba33a-129">Bijvoorbeeld, kunt u instellen Hallo account tooexpire een paar dagen van Hallo huidige datum en tijd.</span><span class="sxs-lookup"><span data-stu-id="ba33a-129">For example, you could set hello account tooexpire a few days from hello current date and time.</span></span>

<span data-ttu-id="ba33a-130">Dit PowerShell-voorbeeld ziet u hoe tooset extern bureaublad-extensie Hallo op een cloudservice:</span><span class="sxs-lookup"><span data-stu-id="ba33a-130">This PowerShell example shows you how tooset hello Remote Desktop Extension on a cloud service:</span></span>

```
$servicename = "cloudservice"
$username = "RemoteDesktopUser"
$securepassword = Get-Content -Path "password.txt" | ConvertTo-SecureString
$expiry = $(Get-Date).AddDays(1)
$credential = New-Object System.Management.Automation.PSCredential $username,$securepassword
Set-AzureServiceRemoteDesktopExtension -ServiceName $servicename -Credential $credential -Expiration $expiry
```
<span data-ttu-id="ba33a-131">U kunt eventueel ook Hallo implementatiesleuf en functies die u op de extern bureaublad tooenable wilt opgeven.</span><span class="sxs-lookup"><span data-stu-id="ba33a-131">You can also optionally specify hello deployment slot and roles that you want tooenable remote desktop on.</span></span> <span data-ttu-id="ba33a-132">Als deze parameters niet zijn opgegeven, Hallo cmdlet kunt Extern bureaublad op alle rollen in Hallo **productie** implementatiesleuf.</span><span class="sxs-lookup"><span data-stu-id="ba33a-132">If these parameters are not specified, hello cmdlet enables remote desktop on all roles in hello **Production** deployment slot.</span></span>

<span data-ttu-id="ba33a-133">Hallo extern bureaublad-extensie is gekoppeld aan een implementatie.</span><span class="sxs-lookup"><span data-stu-id="ba33a-133">hello Remote Desktop extension is associated with a deployment.</span></span> <span data-ttu-id="ba33a-134">Als u een nieuwe implementatie voor Hallo service maakt, hebt u tooenable extern bureaublad op implementatie.</span><span class="sxs-lookup"><span data-stu-id="ba33a-134">If you create a new deployment for hello service, you have tooenable remote desktop on that deployment.</span></span> <span data-ttu-id="ba33a-135">Als u wilt dat altijd toohave extern bureaublad is ingeschakeld, moet vervolgens u PowerShell-scripts Hallo integreren in uw werkstroom voor de implementatie.</span><span class="sxs-lookup"><span data-stu-id="ba33a-135">If you always want toohave remote desktop enabled, then you should consider integrating hello PowerShell scripts into your deployment workflow.</span></span>

## <a name="remote-desktop-into-a-role-instance"></a><span data-ttu-id="ba33a-136">Extern bureaublad in een rolinstantie</span><span class="sxs-lookup"><span data-stu-id="ba33a-136">Remote Desktop into a role instance</span></span>
<span data-ttu-id="ba33a-137">Hallo [Get-AzureRemoteDesktopFile](/powershell/module/azure/get-azureremotedesktopfile?view=azuresmps-3.7.0) cmdlet gebruikte tooremote bureaublad in een specifieke rolexemplaar van de cloudservice is.</span><span class="sxs-lookup"><span data-stu-id="ba33a-137">hello [Get-AzureRemoteDesktopFile](/powershell/module/azure/get-azureremotedesktopfile?view=azuresmps-3.7.0) cmdlet is used tooremote desktop into a specific role instance of your cloud service.</span></span> <span data-ttu-id="ba33a-138">U kunt Hallo *LocalPath* parameter toodownload Hallo RDP-bestand lokaal.</span><span class="sxs-lookup"><span data-stu-id="ba33a-138">You can use hello *LocalPath* parameter toodownload hello RDP file locally.</span></span> <span data-ttu-id="ba33a-139">Of u kunt Hallo *starten* parameter toodirectly starten Hallo verbinding met extern bureaublad dialoogvenster tooaccess Hallo rolinstantie cloud-service.</span><span class="sxs-lookup"><span data-stu-id="ba33a-139">Or you can use hello *Launch* parameter toodirectly launch hello Remote Desktop Connection dialog tooaccess hello cloud service role instance.</span></span>

```
Get-AzureRemoteDesktopFile -ServiceName $servicename -Name "WorkerRole1_IN_0" -Launch
```


## <a name="check-if-remote-desktop-extension-is-enabled-on-a-service"></a><span data-ttu-id="ba33a-140">Controleer of de extern bureaublad-extensie is ingeschakeld voor een service</span><span class="sxs-lookup"><span data-stu-id="ba33a-140">Check if Remote Desktop extension is enabled on a service</span></span>
<span data-ttu-id="ba33a-141">Hallo [Get-AzureServiceRemoteDesktopExtension](/powershell/module/azure/get-azureremotedesktopfile?view=azuresmps-3.7.0) cmdlet geeft weer die extern bureaublad is ingeschakeld of uitgeschakeld op een service-implementatie.</span><span class="sxs-lookup"><span data-stu-id="ba33a-141">hello [Get-AzureServiceRemoteDesktopExtension](/powershell/module/azure/get-azureremotedesktopfile?view=azuresmps-3.7.0) cmdlet displays that remote desktop is enabled or disabled on a service deployment.</span></span> <span data-ttu-id="ba33a-142">Hallo cmdlet retourneert Hallo gebruikersnaam voor de externe bureaubladgebruiker hello en Hallo-functies die Hallo extern bureaublad-extensie is ingeschakeld voor.</span><span class="sxs-lookup"><span data-stu-id="ba33a-142">hello cmdlet returns hello username for hello remote desktop user and hello roles that hello remote desktop extension is enabled for.</span></span> <span data-ttu-id="ba33a-143">Dit gebeurt op Hallo implementatiesleuf en toouse hello faseringssleuven in plaats daarvan kunt u standaard.</span><span class="sxs-lookup"><span data-stu-id="ba33a-143">By default, this happens on hello deployment slot and you can choose toouse hello staging slot instead.</span></span>

```
Get-AzureServiceRemoteDesktopExtension -ServiceName $servicename
```

## <a name="remove-remote-desktop-extension-from-a-service"></a><span data-ttu-id="ba33a-144">Extern bureaublad-uitbreiding te verwijderen van een service</span><span class="sxs-lookup"><span data-stu-id="ba33a-144">Remove Remote Desktop extension from a service</span></span>
<span data-ttu-id="ba33a-145">Als u al Hallo extern bureaublad-extensie op een implementatie hebt ingeschakeld en moet tooupdate Hallo instellingen voor extern bureaublad, eerst Hallo uitbreiding te verwijderen.</span><span class="sxs-lookup"><span data-stu-id="ba33a-145">If you have already enabled hello remote desktop extension on a deployment, and need tooupdate hello remote desktop settings, first remove hello extension.</span></span> <span data-ttu-id="ba33a-146">En deze opnieuw inschakelen met de nieuwe instellingen Hallo.</span><span class="sxs-lookup"><span data-stu-id="ba33a-146">And enable it again with hello new settings.</span></span> <span data-ttu-id="ba33a-147">Als u wilt dat tooset verlopen bijvoorbeeld een nieuw wachtwoord voor het externe gebruikersaccount Hallo of Hallo-account.</span><span class="sxs-lookup"><span data-stu-id="ba33a-147">For example, if you want tooset a new password for hello remote user account, or hello account expired.</span></span> <span data-ttu-id="ba33a-148">Dit is vereist op de bestaande implementaties die Hallo extern bureaublad-extensie ingeschakeld hebben.</span><span class="sxs-lookup"><span data-stu-id="ba33a-148">Doing this is required on existing deployments that have hello remote desktop extension enabled.</span></span> <span data-ttu-id="ba33a-149">Voor nieuwe implementaties, kunt u Hallo extensie gewoon rechtstreeks toepassen.</span><span class="sxs-lookup"><span data-stu-id="ba33a-149">For new deployments, you can simply apply hello extension directly.</span></span>

<span data-ttu-id="ba33a-150">tooremove Hallo extern bureaublad-extensie uit Hallo-implementatie, kunt u Hallo [verwijderen AzureServiceRemoteDesktopExtension](/powershell/module/azure/remove-azureserviceremotedesktopextension?view=azuresmps-3.7.0) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="ba33a-150">tooremove hello remote desktop extension from hello deployment, you can use hello [Remove-AzureServiceRemoteDesktopExtension](/powershell/module/azure/remove-azureserviceremotedesktopextension?view=azuresmps-3.7.0) cmdlet.</span></span> <span data-ttu-id="ba33a-151">U kunt eventueel ook Hallo implementatiesleuf en rol van waaruit u tooremove Hallo extern bureaublad-extensie wilt opgeven.</span><span class="sxs-lookup"><span data-stu-id="ba33a-151">You can also optionally specify hello deployment slot and role from which you want tooremove hello remote desktop extension.</span></span>

```
Remove-AzureServiceRemoteDesktopExtension -ServiceName $servicename -UninstallConfiguration
```

> [!NOTE]
> <span data-ttu-id="ba33a-152">configuratie van toocompletely verwijderen Hallo uitbreiding, moet u Hallo aanroepen *verwijderen* cmdlet Hello **UninstallConfiguration** parameter.</span><span class="sxs-lookup"><span data-stu-id="ba33a-152">toocompletely remove hello extension configuration, you should call hello *remove* cmdlet with hello **UninstallConfiguration** parameter.</span></span>
>
> <span data-ttu-id="ba33a-153">Hallo **UninstallConfiguration** parameter Hiermee verwijdert u de configuratie voor elke uitbreiding die toegepaste toohello service.</span><span class="sxs-lookup"><span data-stu-id="ba33a-153">hello **UninstallConfiguration** parameter uninstalls any extension configuration that is applied toohello service.</span></span> <span data-ttu-id="ba33a-154">De configuratie voor elke uitbreiding is gekoppeld aan het Hallo-serviceconfiguratie.</span><span class="sxs-lookup"><span data-stu-id="ba33a-154">Every extension configuration is associated with hello service configuration.</span></span> <span data-ttu-id="ba33a-155">Aanroepen Hallo *verwijderen* cmdlet zonder **UninstallConfiguration** instelt, scheidt u Hallo <mark>implementatie</mark> van configuratie van Hallo-uitbreiding, dus effectief verwijderen Hallo-extensie.</span><span class="sxs-lookup"><span data-stu-id="ba33a-155">Calling hello *remove* cmdlet without **UninstallConfiguration** disassociates hello <mark>deployment</mark> from hello extension configuration, thus effectively removing hello extension.</span></span> <span data-ttu-id="ba33a-156">Configuratie van de uitbreiding Hallo blijft echter gekoppeld aan Hallo-service.</span><span class="sxs-lookup"><span data-stu-id="ba33a-156">However, hello extension configuration remains associated with hello service.</span></span>
>
>

## <a name="additional-resources"></a><span data-ttu-id="ba33a-157">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="ba33a-157">Additional resources</span></span>

<span data-ttu-id="ba33a-158">[Hoe tooConfigure Cloudservices](cloud-services-how-to-configure.md)
[extern bureaublad-services FAQ - Cloud](cloud-services-faq.md)</span><span class="sxs-lookup"><span data-stu-id="ba33a-158">[How tooConfigure Cloud Services](cloud-services-how-to-configure.md)
[Cloud services FAQ - Remote Desktop](cloud-services-faq.md)</span></span>

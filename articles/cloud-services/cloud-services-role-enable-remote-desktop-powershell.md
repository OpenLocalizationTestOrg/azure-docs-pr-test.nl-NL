---
title: Verbinding met extern bureaublad inschakelen voor een rol in Azure Cloud Services met behulp van PowerShell
description: Het configureren van uw azure-cloud-servicetoepassing extern bureaublad-verbindingen toestaan met behulp van PowerShell
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
ms.openlocfilehash: 171f27c92ee9de14301ebb664e9ba3bcd98c394d
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="enable-remote-desktop-connection-for-a-role-in-azure-cloud-services-using-powershell"></a><span data-ttu-id="675b8-103">Verbinding met extern bureaublad inschakelen voor een rol in Azure Cloud Services met behulp van PowerShell</span><span class="sxs-lookup"><span data-stu-id="675b8-103">Enable Remote Desktop Connection for a Role in Azure Cloud Services using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="675b8-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="675b8-104">Azure portal</span></span>](cloud-services-role-enable-remote-desktop-new-portal.md)
> * [<span data-ttu-id="675b8-105">Klassieke Azure Portal</span><span class="sxs-lookup"><span data-stu-id="675b8-105">Azure classic portal</span></span>](cloud-services-role-enable-remote-desktop.md)
> * [<span data-ttu-id="675b8-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="675b8-106">PowerShell</span></span>](cloud-services-role-enable-remote-desktop-powershell.md)
> * [<span data-ttu-id="675b8-107">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="675b8-107">Visual Studio</span></span>](../vs-azure-tools-remote-desktop-roles.md)
>
>

<span data-ttu-id="675b8-108">Extern bureaublad kunt u toegang tot het bureaublad van een rol in Azure wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="675b8-108">Remote Desktop enables you to access the desktop of a role running in Azure.</span></span> <span data-ttu-id="675b8-109">U kunt een verbinding met extern bureaublad gebruiken oplossen en analyseren van problemen met uw toepassing, terwijl deze wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="675b8-109">You can use a Remote Desktop connection to troubleshoot and diagnose problems with your application while it is running.</span></span>

<span data-ttu-id="675b8-110">In dit artikel wordt beschreven hoe extern bureaublad inschakelen op rollen van uw Cloudservice met behulp van PowerShell.</span><span class="sxs-lookup"><span data-stu-id="675b8-110">This article describes how to enable remote desktop on your Cloud Service Roles using PowerShell.</span></span> <span data-ttu-id="675b8-111">Zie [installeren en configureren van Azure PowerShell](/powershell/azure/overview) voor de vereisten die nodig zijn voor dit artikel.</span><span class="sxs-lookup"><span data-stu-id="675b8-111">See [How to install and configure Azure PowerShell](/powershell/azure/overview) for the prerequisites needed for this article.</span></span> <span data-ttu-id="675b8-112">PowerShell maakt gebruik van de extern bureaublad-extensie zodat u extern bureaublad inschakelen kunt nadat de toepassing wordt geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="675b8-112">PowerShell utilizes the Remote Desktop Extension so you can enable Remote Desktop after the application is deployed.</span></span>

## <a name="configure-remote-desktop-from-powershell"></a><span data-ttu-id="675b8-113">Extern bureaublad vanuit PowerShell configureren</span><span class="sxs-lookup"><span data-stu-id="675b8-113">Configure Remote Desktop from PowerShell</span></span>
<span data-ttu-id="675b8-114">De [Set AzureServiceRemoteDesktopExtension](/powershell/module/azure/set-azureserviceremotedesktopextension?view=azuresmps-3.7.0) cmdlet kunt u extern bureaublad inschakelen op de opgegeven rollen of alle rollen van uw cloud service-implementatie.</span><span class="sxs-lookup"><span data-stu-id="675b8-114">The [Set-AzureServiceRemoteDesktopExtension](/powershell/module/azure/set-azureserviceremotedesktopextension?view=azuresmps-3.7.0) cmdlet allows you to enable Remote Desktop on specified roles or all roles of your cloud service deployment.</span></span> <span data-ttu-id="675b8-115">De cmdlet kunt u de gebruikersnaam en wachtwoord opgeven voor de extern bureaublad-gebruiker via de *referentie* parameter een PSCredential-object accepteert.</span><span class="sxs-lookup"><span data-stu-id="675b8-115">The cmdlet lets you specify the Username and Password for the remote desktop user through the *Credential* parameter that accepts a PSCredential object.</span></span>

<span data-ttu-id="675b8-116">Als u PowerShell interactief gebruikt, kunt u eenvoudig de PSCredential-object instellen door het aanroepen van de [Get-referenties](https://technet.microsoft.com/library/hh849815.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="675b8-116">If you are using PowerShell interactively, you can easily set the PSCredential object by calling the [Get-Credentials](https://technet.microsoft.com/library/hh849815.aspx) cmdlet.</span></span>

```
$remoteusercredentials = Get-Credential
```

<span data-ttu-id="675b8-117">Deze opdracht wordt een dialoogvenster waarin u de gebruikersnaam en wachtwoord invoeren voor de externe gebruiker op een veilige manier weergegeven.</span><span class="sxs-lookup"><span data-stu-id="675b8-117">This command displays a dialog box allowing you to enter the username and password for the remote user in a secure manner.</span></span>

<span data-ttu-id="675b8-118">Aangezien PowerShell in automation scenario's helpt, kunt u ook instellen de **PSCredential** object op een manier die geen tussenkomst van de gebruiker vereist.</span><span class="sxs-lookup"><span data-stu-id="675b8-118">Since PowerShell helps in automation scenarios, you can also set up the **PSCredential** object in a way that doesn't require user interaction.</span></span> <span data-ttu-id="675b8-119">Eerst moet u een beveiligd wachtwoord instellen.</span><span class="sxs-lookup"><span data-stu-id="675b8-119">First, you need to set up a secure password.</span></span> <span data-ttu-id="675b8-120">U begint met het opgeven van een wachtwoord als tekst zonder opmaak converteren naar een veilige tekenreeks met [ConvertTo-SecureString](https://technet.microsoft.com/library/hh849818.aspx).</span><span class="sxs-lookup"><span data-stu-id="675b8-120">You begin with specifying a plain text password convert it to a secure string using [ConvertTo-SecureString](https://technet.microsoft.com/library/hh849818.aspx).</span></span> <span data-ttu-id="675b8-121">Vervolgens moet u deze veilige tekenreeks converteren naar een versleutelde standaardtekenreeks met behulp [ConverterenVan SecureString](https://technet.microsoft.com/library/hh849814.aspx).</span><span class="sxs-lookup"><span data-stu-id="675b8-121">Next you need to convert this secure string into an encrypted standard string using [ConvertFrom-SecureString](https://technet.microsoft.com/library/hh849814.aspx).</span></span> <span data-ttu-id="675b8-122">Nu kunt u deze versleutelde standaardtekenreeks opslaan in een bestand met [Set inhoud](https://technet.microsoft.com/library/ee176959.aspx).</span><span class="sxs-lookup"><span data-stu-id="675b8-122">Now you can save this encrypted standard string to a file using [Set-Content](https://technet.microsoft.com/library/ee176959.aspx).</span></span>

<span data-ttu-id="675b8-123">U kunt ook een bestand beveiligd wachtwoord maken zodat u niet hoeft te typen in het wachtwoord elke keer.</span><span class="sxs-lookup"><span data-stu-id="675b8-123">You can also create a secure password file so that you don't have to type in the password every time.</span></span> <span data-ttu-id="675b8-124">Er is ook een bestand beveiligd wachtwoord beter dan een tekstbestand.</span><span class="sxs-lookup"><span data-stu-id="675b8-124">Also, a secure password file is better than a plain text file.</span></span> <span data-ttu-id="675b8-125">De volgende PowerShell gebruiken om een bestand beveiligd wachtwoord te maken:</span><span class="sxs-lookup"><span data-stu-id="675b8-125">Use the following PowerShell to create a secure password file:</span></span>

```
ConvertTo-SecureString -String "Password123" -AsPlainText -Force | ConvertFrom-SecureString | Set-Content "password.txt"
```

> [!IMPORTANT]
> <span data-ttu-id="675b8-126">Wanneer u het wachtwoord, zorg ervoor dat u voldoet aan de [complexiteitsvereisten](https://technet.microsoft.com/library/cc786468.aspx).</span><span class="sxs-lookup"><span data-stu-id="675b8-126">When setting the password, make sure that you meet the [complexity requirements](https://technet.microsoft.com/library/cc786468.aspx).</span></span>
>
>

<span data-ttu-id="675b8-127">Voor het maken van het referentieobject uit het bestand beveiligd wachtwoord, moet u de bestandsinhoud lezen en terug te converteren naar een veilige tekenreeks met [ConvertTo-SecureString](https://technet.microsoft.com/library/hh849818.aspx).</span><span class="sxs-lookup"><span data-stu-id="675b8-127">To create the credential object from the secure password file, you must read the file contents and convert them back to a secure string using [ConvertTo-SecureString](https://technet.microsoft.com/library/hh849818.aspx).</span></span>

<span data-ttu-id="675b8-128">De [Set AzureServiceRemoteDesktopExtension](/powershell/module/azure/set-azureserviceremotedesktopextension?view=azuresmps-3.7.0) cmdlet accepteert ook een *verlopen* parameter waarmee een **DateTime** op dat het gebruikersaccount is verlopen.</span><span class="sxs-lookup"><span data-stu-id="675b8-128">The [Set-AzureServiceRemoteDesktopExtension](/powershell/module/azure/set-azureserviceremotedesktopextension?view=azuresmps-3.7.0) cmdlet also accepts an *Expiration* parameter, which specifies a **DateTime** at which the user account expires.</span></span> <span data-ttu-id="675b8-129">U kunt bijvoorbeeld instellen dat de account verloopt een paar dagen van de huidige datum en tijd.</span><span class="sxs-lookup"><span data-stu-id="675b8-129">For example, you could set the account to expire a few days from the current date and time.</span></span>

<span data-ttu-id="675b8-130">Deze PowerShell-voorbeeld laat zien hoe u de extern bureaublad-extensie instellen op een cloudservice:</span><span class="sxs-lookup"><span data-stu-id="675b8-130">This PowerShell example shows you how to set the Remote Desktop Extension on a cloud service:</span></span>

```
$servicename = "cloudservice"
$username = "RemoteDesktopUser"
$securepassword = Get-Content -Path "password.txt" | ConvertTo-SecureString
$expiry = $(Get-Date).AddDays(1)
$credential = New-Object System.Management.Automation.PSCredential $username,$securepassword
Set-AzureServiceRemoteDesktopExtension -ServiceName $servicename -Credential $credential -Expiration $expiry
```
<span data-ttu-id="675b8-131">U kunt eventueel ook de implementatiesleuf en functies die u inschakelen van extern bureaublad wilt op opgeven.</span><span class="sxs-lookup"><span data-stu-id="675b8-131">You can also optionally specify the deployment slot and roles that you want to enable remote desktop on.</span></span> <span data-ttu-id="675b8-132">Als deze parameters niet zijn opgegeven, de cmdlet wordt ingeschakeld voor extern bureaublad op alle rollen in de **productie** implementatiesleuf.</span><span class="sxs-lookup"><span data-stu-id="675b8-132">If these parameters are not specified, the cmdlet enables remote desktop on all roles in the **Production** deployment slot.</span></span>

<span data-ttu-id="675b8-133">De extern bureaublad-extensie is gekoppeld aan een implementatie.</span><span class="sxs-lookup"><span data-stu-id="675b8-133">The Remote Desktop extension is associated with a deployment.</span></span> <span data-ttu-id="675b8-134">Als u een nieuwe implementatie voor de service maakt, hebt u de extern bureaublad inschakelen op implementatie.</span><span class="sxs-lookup"><span data-stu-id="675b8-134">If you create a new deployment for the service, you have to enable remote desktop on that deployment.</span></span> <span data-ttu-id="675b8-135">Als u altijd hebben van extern bureaublad is ingeschakeld wilt, moet vervolgens u de PowerShell-scripts integreren in uw werkstroom voor de implementatie.</span><span class="sxs-lookup"><span data-stu-id="675b8-135">If you always want to have remote desktop enabled, then you should consider integrating the PowerShell scripts into your deployment workflow.</span></span>

## <a name="remote-desktop-into-a-role-instance"></a><span data-ttu-id="675b8-136">Extern bureaublad in een rolinstantie</span><span class="sxs-lookup"><span data-stu-id="675b8-136">Remote Desktop into a role instance</span></span>
<span data-ttu-id="675b8-137">De [Get-AzureRemoteDesktopFile](/powershell/module/azure/get-azureremotedesktopfile?view=azuresmps-3.7.0) cmdlet wordt gebruikt voor extern bureaublad in een specifieke rolexemplaar van de cloudservice.</span><span class="sxs-lookup"><span data-stu-id="675b8-137">The [Get-AzureRemoteDesktopFile](/powershell/module/azure/get-azureremotedesktopfile?view=azuresmps-3.7.0) cmdlet is used to remote desktop into a specific role instance of your cloud service.</span></span> <span data-ttu-id="675b8-138">U kunt de *LocalPath* parameter voor het downloaden van de RDP-bestand lokaal.</span><span class="sxs-lookup"><span data-stu-id="675b8-138">You can use the *LocalPath* parameter to download the RDP file locally.</span></span> <span data-ttu-id="675b8-139">Of u kunt de *starten* -parameter voor het dialoogvenster verbinding met extern bureaublad voor toegang tot de cloud service-rolinstantie rechtstreeks te starten.</span><span class="sxs-lookup"><span data-stu-id="675b8-139">Or you can use the *Launch* parameter to directly launch the Remote Desktop Connection dialog to access the cloud service role instance.</span></span>

```
Get-AzureRemoteDesktopFile -ServiceName $servicename -Name "WorkerRole1_IN_0" -Launch
```


## <a name="check-if-remote-desktop-extension-is-enabled-on-a-service"></a><span data-ttu-id="675b8-140">Controleer of de extern bureaublad-extensie is ingeschakeld voor een service</span><span class="sxs-lookup"><span data-stu-id="675b8-140">Check if Remote Desktop extension is enabled on a service</span></span>
<span data-ttu-id="675b8-141">De [Get-AzureServiceRemoteDesktopExtension](/powershell/module/azure/get-azureremotedesktopfile?view=azuresmps-3.7.0) cmdlet geeft weer die extern bureaublad is ingeschakeld of uitgeschakeld op een service-implementatie.</span><span class="sxs-lookup"><span data-stu-id="675b8-141">The [Get-AzureServiceRemoteDesktopExtension](/powershell/module/azure/get-azureremotedesktopfile?view=azuresmps-3.7.0) cmdlet displays that remote desktop is enabled or disabled on a service deployment.</span></span> <span data-ttu-id="675b8-142">De cmdlet retourneert de gebruikersnaam voor de extern bureaublad-gebruiker en de functies die de extern bureaublad-extensie is ingeschakeld voor.</span><span class="sxs-lookup"><span data-stu-id="675b8-142">The cmdlet returns the username for the remote desktop user and the roles that the remote desktop extension is enabled for.</span></span> <span data-ttu-id="675b8-143">Dit gebeurt op de implementatiesleuf standaard en u kunt in plaats daarvan de faseringssleuf gebruiken.</span><span class="sxs-lookup"><span data-stu-id="675b8-143">By default, this happens on the deployment slot and you can choose to use the staging slot instead.</span></span>

```
Get-AzureServiceRemoteDesktopExtension -ServiceName $servicename
```

## <a name="remove-remote-desktop-extension-from-a-service"></a><span data-ttu-id="675b8-144">Extern bureaublad-uitbreiding te verwijderen van een service</span><span class="sxs-lookup"><span data-stu-id="675b8-144">Remove Remote Desktop extension from a service</span></span>
<span data-ttu-id="675b8-145">Als u de extern bureaublad-extensie op een implementatie al hebt ingeschakeld en moet de instellingen voor extern bureaublad bijwerken, moet u eerst de uitbreiding verwijderen.</span><span class="sxs-lookup"><span data-stu-id="675b8-145">If you have already enabled the remote desktop extension on a deployment, and need to update the remote desktop settings, first remove the extension.</span></span> <span data-ttu-id="675b8-146">En deze opnieuw inschakelen met de nieuwe instellingen.</span><span class="sxs-lookup"><span data-stu-id="675b8-146">And enable it again with the new settings.</span></span> <span data-ttu-id="675b8-147">Bijvoorbeeld als u wilt een nieuw wachtwoord instellen voor het externe gebruikersaccount of het account is verlopen.</span><span class="sxs-lookup"><span data-stu-id="675b8-147">For example, if you want to set a new password for the remote user account, or the account expired.</span></span> <span data-ttu-id="675b8-148">Dit is vereist op de bestaande implementaties waarvoor de extern bureaublad-extensie is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="675b8-148">Doing this is required on existing deployments that have the remote desktop extension enabled.</span></span> <span data-ttu-id="675b8-149">Voor nieuwe implementaties, kunt u de extensie gewoon rechtstreeks toepassen.</span><span class="sxs-lookup"><span data-stu-id="675b8-149">For new deployments, you can simply apply the extension directly.</span></span>

<span data-ttu-id="675b8-150">Als u wilt de extern bureaublad-uitbreiding verwijderen uit de implementatie, kunt u de [verwijderen AzureServiceRemoteDesktopExtension](/powershell/module/azure/remove-azureserviceremotedesktopextension?view=azuresmps-3.7.0) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="675b8-150">To remove the remote desktop extension from the deployment, you can use the [Remove-AzureServiceRemoteDesktopExtension](/powershell/module/azure/remove-azureserviceremotedesktopextension?view=azuresmps-3.7.0) cmdlet.</span></span> <span data-ttu-id="675b8-151">U kunt eventueel ook de implementatiesleuf en de rol van waaruit u wilt verwijderen van de extern bureaublad-extensie opgeven.</span><span class="sxs-lookup"><span data-stu-id="675b8-151">You can also optionally specify the deployment slot and role from which you want to remove the remote desktop extension.</span></span>

```
Remove-AzureServiceRemoteDesktopExtension -ServiceName $servicename -UninstallConfiguration
```

> [!NOTE]
> <span data-ttu-id="675b8-152">Om volledig te verwijderen configuratie voor de uitbreiding, moet u aanroepen de *verwijderen* cmdlet uit met de **UninstallConfiguration** parameter.</span><span class="sxs-lookup"><span data-stu-id="675b8-152">To completely remove the extension configuration, you should call the *remove* cmdlet with the **UninstallConfiguration** parameter.</span></span>
>
> <span data-ttu-id="675b8-153">De **UninstallConfiguration** parameter Hiermee verwijdert u een extensie-configuratie die wordt toegepast op de service.</span><span class="sxs-lookup"><span data-stu-id="675b8-153">The **UninstallConfiguration** parameter uninstalls any extension configuration that is applied to the service.</span></span> <span data-ttu-id="675b8-154">De configuratie voor elke uitbreiding is gekoppeld aan de configuratie van de service.</span><span class="sxs-lookup"><span data-stu-id="675b8-154">Every extension configuration is associated with the service configuration.</span></span> <span data-ttu-id="675b8-155">Het aanroepen van de *verwijderen* cmdlet zonder **UninstallConfiguration** instelt, scheidt u de <mark>implementatie</mark> van de configuratie voor de uitbreiding, dus effectief verwijderen van de extensie.</span><span class="sxs-lookup"><span data-stu-id="675b8-155">Calling the *remove* cmdlet without **UninstallConfiguration** disassociates the <mark>deployment</mark> from the extension configuration, thus effectively removing the extension.</span></span> <span data-ttu-id="675b8-156">Configuratie voor de uitbreiding blijft echter gekoppeld aan de service.</span><span class="sxs-lookup"><span data-stu-id="675b8-156">However, the extension configuration remains associated with the service.</span></span>
>
>

## <a name="additional-resources"></a><span data-ttu-id="675b8-157">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="675b8-157">Additional resources</span></span>

<span data-ttu-id="675b8-158">[Cloud-Services configureren hoe](cloud-services-how-to-configure.md)
[extern bureaublad-services FAQ - Cloud](cloud-services-faq.md)</span><span class="sxs-lookup"><span data-stu-id="675b8-158">[How to Configure Cloud Services](cloud-services-how-to-configure.md)
[Cloud services FAQ - Remote Desktop](cloud-services-faq.md)</span></span>

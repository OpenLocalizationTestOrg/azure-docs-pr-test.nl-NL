---
title: Meld u aan bij Azure met CLI | Microsoft Docs
description: Verbinding maken met uw Azure-abonnement met de Azure-opdrachtregelinterface (Azure CLI) voor Mac, Linux en Windows
editor: tysonn
manager: timlt
documentationcenter: 
author: squillace
services: virtual-machines-linux,virtual-network,storage,azure-resource-manager
tags: azure-resource-manager,azure-service-management
ms.assetid: ed856527-d75e-4e16-93fb-253dafad209d
ms.service: multiple
ms.workload: multiple
ms.tgt_pltfrm: vm-multiple
ms.devlang: na
ms.topic: article
ms.date: 10/04/2016
ms.author: rasquill
"\"/": 
ms.openlocfilehash: 31efab60690b54faf7992251fcd01e307c4464f2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="log-in-to-azure-from-the-azure-cli"></a><span data-ttu-id="bfbb9-103">Meld u aan bij Azure met Azure CLI</span><span class="sxs-lookup"><span data-stu-id="bfbb9-103">Log in to Azure from the Azure CLI</span></span>
<span data-ttu-id="bfbb9-104">De Azure CLI is een set van open-source, platformoverschrijdende opdrachten voor het werken met Azure-resources.</span><span class="sxs-lookup"><span data-stu-id="bfbb9-104">The Azure CLI is a set of open-source, cross-platform commands for working with Azure resources.</span></span> <span data-ttu-id="bfbb9-105">Dit artikel worden de verschillende manieren waarop u de referenties van uw Azure-account voor de Azure CLI verbinding met uw Azure-abonnement op te geven:</span><span class="sxs-lookup"><span data-stu-id="bfbb9-105">This article describes the different ways to provide your Azure account credentials to connect the Azure CLI to your Azure subscription:</span></span>

* <span data-ttu-id="bfbb9-106">Voer de `azure login` CLI-opdracht om te verifiëren via Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="bfbb9-106">Run the `azure login` CLI command to authenticate through Azure Active Directory.</span></span> <span data-ttu-id="bfbb9-107">Deze methode biedt u toegang tot de CLI-opdrachten in beide [opdracht modi](#cli-command-modes).</span><span class="sxs-lookup"><span data-stu-id="bfbb9-107">This method gives you access to CLI commands in both [command modes](#cli-command-modes).</span></span> <span data-ttu-id="bfbb9-108">Wanneer u de opdracht zonder extra opties uitvoert `azure login` vraagt u om door te gaan interactief aanmelden via een webportal.</span><span class="sxs-lookup"><span data-stu-id="bfbb9-108">When you run the command without additional options, `azure login` prompts you to continue logging in interactively through a web portal.</span></span> <span data-ttu-id="bfbb9-109">Voor extra `azure login` opdracht Opties, raadpleegt u de scenario's in dit artikel of type `azure login --help`.</span><span class="sxs-lookup"><span data-stu-id="bfbb9-109">For additional `azure login` command options, see the scenarios in this article, or type `azure login --help`.</span></span>
* <span data-ttu-id="bfbb9-110">Als u alleen wilt gebruiken van Azure Service Management modus CLI-opdrachten (niet aanbevolen voor de meeste nieuwe implementaties), kunt u downloaden en installeren van een bestand met instellingen publiceren op uw computer.</span><span class="sxs-lookup"><span data-stu-id="bfbb9-110">If you only need to use Azure Service Management mode CLI commands (not recommended for most new deployments), you can download and install a publish settings file on your computer.</span></span>

<span data-ttu-id="bfbb9-111">Als u nog niet de CLI hebt geïnstalleerd, raadpleegt u [Azure CLI installeren](cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="bfbb9-111">If you haven't already installed the CLI, see [Install the Azure CLI](cli-install-nodejs.md).</span></span> <span data-ttu-id="bfbb9-112">Als u geen Azure-abonnement hebt, kunt u binnen een paar minuten een [gratis account](http://azure.microsoft.com/free/) maken.</span><span class="sxs-lookup"><span data-stu-id="bfbb9-112">If you don't have an Azure subscription, you can create a [free account](http://azure.microsoft.com/free/) in just a couple of minutes.</span></span>

<span data-ttu-id="bfbb9-113">Zie voor achtergrondinformatie over andere account-id's en Azure-abonnementen [hoe Azure-abonnementen worden gekoppeld aan Azure Active Directory](active-directory/active-directory-how-subscriptions-associated-directory.md).</span><span class="sxs-lookup"><span data-stu-id="bfbb9-113">For background about different account identities and Azure subscriptions, see [How Azure subscriptions are associated with Azure Active Directory](active-directory/active-directory-how-subscriptions-associated-directory.md).</span></span>

## <a name="scenario-1-azure-login-with-interactive-login"></a><span data-ttu-id="bfbb9-114">Scenario 1: azure-aanmelding met interactieve aanmelding</span><span class="sxs-lookup"><span data-stu-id="bfbb9-114">Scenario 1: azure login with interactive login</span></span>
<span data-ttu-id="bfbb9-115">Met bepaalde accounts, moet u om uit te voeren met de CLI `azure login` en ga vervolgens door de aanmelding met een webbrowser via een webportal, een proces genaamd *interactieve aanmelding*.</span><span class="sxs-lookup"><span data-stu-id="bfbb9-115">With certain accounts, the CLI requires you to run `azure login` and then continue the login process with a web browser through a web portal, a process called *interactive login*.</span></span> <span data-ttu-id="bfbb9-116">Een veelvoorkomende reden is wanneer u een account voor werk of school hebt (ook wel een *organisatieaccount*) die is ingesteld om meervoudige verificatie te vereisen.</span><span class="sxs-lookup"><span data-stu-id="bfbb9-116">A common reason is when you have a work or school account (also called an *organizational account*) that is set up to require multifactor authentication.</span></span> <span data-ttu-id="bfbb9-117">Ook interactieve aanmelding met je Microsoft-account gebruiken als u wilt gebruiken van opdrachten in de modus Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="bfbb9-117">Also use interactive login with your Microsoft account, when you want to use Resource Manager mode commands.</span></span>

<span data-ttu-id="bfbb9-118">Interactieve aanmelding is eenvoudig: type `azure login` --zonder opties--zoals weergegeven in het volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="bfbb9-118">Interactive login is easy: type `azure login` -- without any options -- as shown in the following example:</span></span>

```
azure login
```                                                                                             

<span data-ttu-id="bfbb9-119">De uitvoer ziet er ongeveer als volgt:</span><span class="sxs-lookup"><span data-stu-id="bfbb9-119">The output appears something like the following:</span></span>

```         
info:    Executing command login
info:    To sign in, use a web browser to open the page http://aka.ms/devicelogin. Enter the code XXXXXXXXX to authenticate.
```
<span data-ttu-id="bfbb9-120">Kopieer de code die u in de opdrachtuitvoer aangeboden en open een browser naar http://aka.ms/devicelogin of andere pagina als u opgeeft.</span><span class="sxs-lookup"><span data-stu-id="bfbb9-120">Copy the code offered to you in the command output, and open a browser to http://aka.ms/devicelogin, or other page if specified.</span></span> <span data-ttu-id="bfbb9-121">(U kunt een browser op dezelfde computer of op een andere computer of apparaat kunt openen.) Voer de code en wordt u gevraagd de gebruikersnaam en wachtwoord invoeren voor de identiteit die u wilt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="bfbb9-121">(You can open a browser on the same computer, or on a different computer or device.) Enter the code, and then you are prompted to enter the username and password for the identity you want to use.</span></span> <span data-ttu-id="bfbb9-122">Wanneer dit proces is voltooid, geeft de opdrachtshell van de aanmelding is voltooid.</span><span class="sxs-lookup"><span data-stu-id="bfbb9-122">When that process completes, the command shell completes the login.</span></span> <span data-ttu-id="bfbb9-123">Dit kan als volgt uitzien:</span><span class="sxs-lookup"><span data-stu-id="bfbb9-123">It might look something like:</span></span>

    info:    Added subscription Visual Studio Ultimate with MSDN
    info:    Added subscription Azure Free Trial
    info:    Setting subscription "Visual Studio Ultimate with MSDN" as default
    +
    info:    login command OK

> [!NOTE]
> <span data-ttu-id="bfbb9-124">Met interactieve aanmelding, worden verificatie en autorisatie uitgevoerd met Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="bfbb9-124">With interactive login, authentication and authorization are performed using Azure Active Directory.</span></span> <span data-ttu-id="bfbb9-125">Als u de identiteit van een Microsoft-account gebruikt, heeft uw Azure Active Directory-standaarddomein toegang tot het aanmeldingsproces.</span><span class="sxs-lookup"><span data-stu-id="bfbb9-125">If you use a Microsoft account identity, the login process accesses your Azure Active Directory default domain.</span></span> <span data-ttu-id="bfbb9-126">(Als u zich aangemeld voor een gratis Azure-account, Azure Active Directory automatisch gemaakt een standaarddomein voor uw account.)</span><span class="sxs-lookup"><span data-stu-id="bfbb9-126">(If you signed up for a free Azure account, Azure Active Directory automatically created a default domain for your account.)</span></span>
>
>

## <a name="scenario-2-azure-login-with-a-username-and-password"></a><span data-ttu-id="bfbb9-127">Scenario 2: azure-aanmelding met een gebruikersnaam en wachtwoord</span><span class="sxs-lookup"><span data-stu-id="bfbb9-127">Scenario 2: azure login with a username and password</span></span>
<span data-ttu-id="bfbb9-128">Gebruik de `azure login` opdracht met de gebruikersnaam (`-u`) parameter om te verifiëren wanneer u wilt gebruiken een werk- of schoolaccount die multifactor-verificatie niet vereist.</span><span class="sxs-lookup"><span data-stu-id="bfbb9-128">Use the `azure login` command with the username (`-u`) parameter to authenticate when you want to use a work or school account that doesn't require multifactor authentication.</span></span> <span data-ttu-id="bfbb9-129">U wordt gevraagd op de opdrachtregel voor het wachtwoord (of u kunt desgewenst het wachtwoord doorgeven als een extra parameter van de `azure login` opdracht).</span><span class="sxs-lookup"><span data-stu-id="bfbb9-129">You are prompted at the command line for the password (or you can optionally pass the password as an additional parameter of the `azure login` command).</span></span> <span data-ttu-id="bfbb9-130">Het volgende voorbeeld wordt de gebruikersnaam van een organisatieaccount doorgegeven:</span><span class="sxs-lookup"><span data-stu-id="bfbb9-130">The following example passes the username of an organizational account:</span></span>

    azure login -u myUserName@contoso.onmicrosoft.com

<span data-ttu-id="bfbb9-131">U wordt gevraagd uw wachtwoord in te voeren:</span><span class="sxs-lookup"><span data-stu-id="bfbb9-131">You are then prompted to enter your password:</span></span>

    info:    Executing command login
    Password: *********

<span data-ttu-id="bfbb9-132">De aanmelding wordt voltooid.</span><span class="sxs-lookup"><span data-stu-id="bfbb9-132">The login process then completes.</span></span>

    info:    Added subscription Visual Studio Ultimate with MSDN
    +
    info:    login command OK

<span data-ttu-id="bfbb9-133">Als dit de eerste keer aangemeld met deze referenties, wordt u gevraagd om te controleren die u wilt geen verificatietoken in de cache.</span><span class="sxs-lookup"><span data-stu-id="bfbb9-133">If this is your first time logging in with these credentials, you are asked to verify that you wish to cache an authentication token.</span></span> <span data-ttu-id="bfbb9-134">Deze vraag vindt ook plaats als u eerder hebt gebruikt de `azure logout` opdracht (Zie verderop in het artikel).</span><span class="sxs-lookup"><span data-stu-id="bfbb9-134">This prompt also occurs if you previously used the `azure logout` command (described later in the article).</span></span> <span data-ttu-id="bfbb9-135">Uitvoeren als u wilt deze prompt voor automatiseringsscenario's omzeilen, `azure login` met de `-q` parameter.</span><span class="sxs-lookup"><span data-stu-id="bfbb9-135">To bypass this prompt for automation scenarios, run `azure login` with the `-q` parameter.</span></span>

## <a name="scenario-3-azure-login-with-a-service-principal"></a><span data-ttu-id="bfbb9-136">Scenario 3: azure-aanmelding met een service-principal</span><span class="sxs-lookup"><span data-stu-id="bfbb9-136">Scenario 3: azure login with a service principal</span></span>
<span data-ttu-id="bfbb9-137">Als u een service-principal voor een Active Directory-toepassing maken en de service-principal machtigingen op uw abonnement heeft, kunt u de `azure login` opdracht voor het verifiëren van de service-principal.</span><span class="sxs-lookup"><span data-stu-id="bfbb9-137">If you create a service principal for an Active Directory application, and the service principal has permissions on your subscription, you can use the `azure login` command to authenticate the service principal.</span></span> <span data-ttu-id="bfbb9-138">Afhankelijk van uw scenario kunt u de referenties van de service-principal opgeven als expliciete parameters van de `azure login` opdracht.</span><span class="sxs-lookup"><span data-stu-id="bfbb9-138">Depending on your scenario, you could provide the credentials of the service principal as explicit parameters of the `azure login` command.</span></span> <span data-ttu-id="bfbb9-139">De volgende opdracht geeft bijvoorbeeld de service principal name en de Active Directory-tenant-ID:</span><span class="sxs-lookup"><span data-stu-id="bfbb9-139">For example, the following command passes the service principal name and Active Directory tenant ID:</span></span>

    azure login -u https://www.contoso.org/example --service-principal --tenant myTenantID

<span data-ttu-id="bfbb9-140">U wordt gevraagd het wachtwoord op te geven.</span><span class="sxs-lookup"><span data-stu-id="bfbb9-140">You are then prompted to provide the password.</span></span> <span data-ttu-id="bfbb9-141">U kunt ook de referenties van de via een script of toepassing code voor CLI of een certificaat voor verificatie van de service-principal niet-interactief voor automatiseringsscenario's gebruiken.</span><span class="sxs-lookup"><span data-stu-id="bfbb9-141">You can also provide the credentials through a CLI script or application code, or use a certificate to authenticate the service principal non-interactively for automation scenarios.</span></span> <span data-ttu-id="bfbb9-142">Zie voor meer informatie en voorbeelden [verifiëren van een service-principal met Azure Resource Manager](resource-group-authenticate-service-principal-cli.md).</span><span class="sxs-lookup"><span data-stu-id="bfbb9-142">For details and examples, see [Authenticating a service principal with Azure Resource Manager](resource-group-authenticate-service-principal-cli.md).</span></span>

## <a name="scenario-4-use-a-publish-settings-file"></a><span data-ttu-id="bfbb9-143">Scenario 4: Gebruik een bestand met publicatie-instellingen</span><span class="sxs-lookup"><span data-stu-id="bfbb9-143">Scenario 4: Use a publish settings file</span></span>
<span data-ttu-id="bfbb9-144">Als u alleen hoeft de Azure Service Management modus CLI-opdrachten (bijvoorbeeld voor het implementeren van virtuele Azure-machines in het klassieke implementatiemodel) gebruiken, kunt u verbinding maken met behulp van een bestand met publicatie-instellingen.</span><span class="sxs-lookup"><span data-stu-id="bfbb9-144">If you only need to use the Azure Service Management mode CLI commands (for example, to deploy Azure VMs in the classic deployment model), you can connect using a publish settings file.</span></span> <span data-ttu-id="bfbb9-145">Deze methode wordt een certificaat geïnstalleerd op uw lokale computer waarmee u beheertaken voor uitvoeren als het abonnement en het certificaat geldig zijn.</span><span class="sxs-lookup"><span data-stu-id="bfbb9-145">This method installs a certificate on your local computer that allows you to perform management tasks for as long as the subscription and the certificate are valid.</span></span>

* <span data-ttu-id="bfbb9-146">**Voor het downloaden van het bestand publiceren instellingen** voor uw account, zorg ervoor dat de CLI in Service Management-modus door te typen `azure config mode asm`.</span><span class="sxs-lookup"><span data-stu-id="bfbb9-146">**To download the publish settings file** for your account, ensure that the CLI is in Service Management mode by typing `azure config mode asm`.</span></span> <span data-ttu-id="bfbb9-147">Voer de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="bfbb9-147">Then run the following command:</span></span>

        azure account download

<span data-ttu-id="bfbb9-148">Hiermee opent u de standaardbrowser en vraagt u zich aanmeldt bij de [klassieke Azure-portal](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="bfbb9-148">This opens your default browser and prompts you to sign in to the [Azure classic portal](https://manage.windowsazure.com).</span></span> <span data-ttu-id="bfbb9-149">Nadat u zich aanmeldt, een `.publishsettings` bestand downloads.</span><span class="sxs-lookup"><span data-stu-id="bfbb9-149">After you sign in, a `.publishsettings` file downloads.</span></span> <span data-ttu-id="bfbb9-150">Noteer waar dit bestand wordt opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="bfbb9-150">Make note of where this file is saved.</span></span>

> [!NOTE]
> <span data-ttu-id="bfbb9-151">Als uw account gekoppeld aan meerdere Azure Active Directory-tenants is, kunt u worden gevraagd om te selecteren welke Active Directory die u wilt een publish settings-bestand voor downloaden.</span><span class="sxs-lookup"><span data-stu-id="bfbb9-151">If your account is associated with multiple Azure Active Directory tenants, you may be prompted to select which Active Directory you wish to download a publish settings file for.</span></span>
>
>

<span data-ttu-id="bfbb9-152">Wanneer met behulp van de downloadpagina of via de klassieke Azure portal, wordt de geselecteerde Active Directory de standaardwaarde aan die door de klassieke portal en download de pagina.</span><span class="sxs-lookup"><span data-stu-id="bfbb9-152">Once selected using the download page, or by visiting the Azure classic portal, the selected Active Directory becomes the default used by the classic portal and download page.</span></span> <span data-ttu-id="bfbb9-153">Zodra een standaard actief is, ziet u de tekst '**Klik hier om terug te keren naar de selectiepagina**' aan de bovenkant van de downloadpagina.</span><span class="sxs-lookup"><span data-stu-id="bfbb9-153">Once a default has been established, you see the text '**click here to return to the selection page**' at the top of the download page.</span></span> <span data-ttu-id="bfbb9-154">Gebruik de onderstaande koppeling om terug te keren naar de selectiepagina.</span><span class="sxs-lookup"><span data-stu-id="bfbb9-154">Use the provided link to return to the selection page.</span></span>

* <span data-ttu-id="bfbb9-155">**Het bestand publiceren-instellingen te importeren**, voer de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="bfbb9-155">**To import the publish settings file**, run the following command:</span></span>

        azure account import <path to your .publishsettings file>

> [!IMPORTANT]
> <span data-ttu-id="bfbb9-156">Na het importeren van de publicatie-instellingen, verwijdert u de `.publishsettings` bestand.</span><span class="sxs-lookup"><span data-stu-id="bfbb9-156">After importing your publish settings, you should delete the `.publishsettings` file.</span></span> <span data-ttu-id="bfbb9-157">Het is niet langer vereist voor de Azure CLI en vormt een beveiligingsrisico, omdat omdat deze kan worden gebruikt voor toegang tot uw abonnement.</span><span class="sxs-lookup"><span data-stu-id="bfbb9-157">It is no longer required by the Azure CLI and presents a security risk as it could be used to gain access to your subscription.</span></span>
>
>

## <a name="cli-command-modes"></a><span data-ttu-id="bfbb9-158">CLI-opdrachtmodi</span><span class="sxs-lookup"><span data-stu-id="bfbb9-158">CLI command modes</span></span>
<span data-ttu-id="bfbb9-159">De Azure CLI biedt twee opdrachtmodi voor het werken met Azure-resources met andere opdrachtsets:</span><span class="sxs-lookup"><span data-stu-id="bfbb9-159">The Azure CLI provides two command modes for working with Azure resources, with different command sets:</span></span>

* <span data-ttu-id="bfbb9-160">**Resource Manager-modus** : voor het werken met Azure-resources in het Resource Manager-implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="bfbb9-160">**Resource Manager mode** - for working with Azure resources in the Resource Manager deployment model.</span></span> <span data-ttu-id="bfbb9-161">Uitvoeren als u wilt instellen in deze modus, `azure config mode arm`.</span><span class="sxs-lookup"><span data-stu-id="bfbb9-161">To set this mode, run `azure config mode arm`.</span></span>
* <span data-ttu-id="bfbb9-162">**Service Management-modus** : voor het werken met Azure-resources in het klassieke implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="bfbb9-162">**Service Management mode** - for working with Azure resources in the classic deployment model.</span></span> <span data-ttu-id="bfbb9-163">Uitvoeren als u wilt instellen in deze modus, `azure config mode asm`.</span><span class="sxs-lookup"><span data-stu-id="bfbb9-163">To set this mode, run `azure config mode asm`.</span></span>

<span data-ttu-id="bfbb9-164">Toen geïnstalleerd, is de huidige release van de CLI in de modus Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="bfbb9-164">When first installed, the current release of the CLI is in Resource Manager mode.</span></span>

> [!NOTE]
> <span data-ttu-id="bfbb9-165">De modus Resource Manager en Service Management-modus elkaar wederzijds uit.</span><span class="sxs-lookup"><span data-stu-id="bfbb9-165">The Resource Manager mode and Service Management mode are mutually exclusive.</span></span> <span data-ttu-id="bfbb9-166">Dat wil zeggen, kunnen niet resources die zijn gemaakt in de modus voor één worden beheerd vanaf de andere modus.</span><span class="sxs-lookup"><span data-stu-id="bfbb9-166">That is, resources created in one mode cannot be managed from the other mode.</span></span>
>
>

## <a name="multiple-subscriptions"></a><span data-ttu-id="bfbb9-167">Meerdere abonnementen</span><span class="sxs-lookup"><span data-stu-id="bfbb9-167">Multiple subscriptions</span></span>
<span data-ttu-id="bfbb9-168">Als u meerdere Azure-abonnementen hebt, verleent verbinding maken met Azure toegang tot alle abonnementen die zijn gekoppeld aan uw referenties.</span><span class="sxs-lookup"><span data-stu-id="bfbb9-168">If you have multiple Azure subscriptions, connecting to Azure grants access to all subscriptions associated with your credentials.</span></span> <span data-ttu-id="bfbb9-169">Een abonnement is geselecteerd als de standaard en gebruikt door de Azure CLI bij het uitvoeren van bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="bfbb9-169">One subscription is selected as the default, and used by the Azure CLI when performing operations.</span></span> <span data-ttu-id="bfbb9-170">U kunt de abonnementen kunt weergeven, met inbegrip van de huidige standaardabonnement, met behulp van de `azure account list` opdracht.</span><span class="sxs-lookup"><span data-stu-id="bfbb9-170">You can view the subscriptions, including the current default subscription, using the `azure account list` command.</span></span> <span data-ttu-id="bfbb9-171">Met deze opdracht retourneert informatie ziet er als volgt:</span><span class="sxs-lookup"><span data-stu-id="bfbb9-171">This command returns information similar to the following:</span></span>

    info:    Executing command account list
    data:    Name              Id                                    Current
    data:    ----------------  ------------------------------------  -------
    data:    Azure-sub-1       ####################################  true
    data:    Azure-sub-2       ####################################  false

<span data-ttu-id="bfbb9-172">In de bovenstaande lijst de **huidige** kolom wordt aangegeven dat het huidige standaardabonnement als Azure-sub-1.</span><span class="sxs-lookup"><span data-stu-id="bfbb9-172">In the preceding list, the **Current** column indicates the current default subscription as Azure-sub-1.</span></span> <span data-ttu-id="bfbb9-173">U kunt het standaardabonnement wijzigen met de `azure account set` opdracht en geeft u het abonnement dat u wilt gebruiken als de standaardwaarde.</span><span class="sxs-lookup"><span data-stu-id="bfbb9-173">To change the default subscription, use the `azure account set` command, and specify the subscription that you wish to be the default.</span></span> <span data-ttu-id="bfbb9-174">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="bfbb9-174">For example:</span></span>

    azure account set Azure-sub-2

<span data-ttu-id="bfbb9-175">Hiermee wijzigt u het standaardabonnement op Azure-sub-2.</span><span class="sxs-lookup"><span data-stu-id="bfbb9-175">This changes the default subscription to Azure-sub-2.</span></span>

> [!NOTE]
> <span data-ttu-id="bfbb9-176">Het wijzigen van het standaardabonnement wordt direct van kracht en is een algemene wijziging; nieuwe Azure CLI-opdrachten gebruiken de nieuwe standaardabonnement of u ze vanaf de opdrachtregel hetzelfde exemplaar of een ander exemplaar uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="bfbb9-176">Changing the default subscription takes effect immediately, and is a global change; new Azure CLI commands, whether you run them from the same command-line instance or a different instance, use the new default subscription.</span></span>
>
>

<span data-ttu-id="bfbb9-177">Als u wilt een niet-standaard-abonnement met de Azure CLI gebruiken, maar niet wilt dat de huidige standaardwaarde te wijzigen, kunt u de `--subscription` optie voor de opdracht en geef de naam van het abonnement dat u wilt gebruiken voor de bewerking.</span><span class="sxs-lookup"><span data-stu-id="bfbb9-177">If you wish to use a non-default subscription with the Azure CLI, but don't want to change the current default, you can use the `--subscription` option for the command and provide the name of the subscription you wish to use for the operation.</span></span>

<span data-ttu-id="bfbb9-178">Wanneer u met uw Azure-abonnement verbonden bent, kunt u beginnen met de Azure CLI-opdrachten om te werken met Azure-resources.</span><span class="sxs-lookup"><span data-stu-id="bfbb9-178">Once you are connected to your Azure subscription, you can start using the Azure CLI commands to work with Azure resources.</span></span>

## <a name="storage-of-cli-settings"></a><span data-ttu-id="bfbb9-179">Opslag van CLI-instellingen</span><span class="sxs-lookup"><span data-stu-id="bfbb9-179">Storage of CLI settings</span></span>
<span data-ttu-id="bfbb9-180">Of u zich aan met de `azure login` opdracht of het importeren van publicatie-instellingen, uw CLI-profiel en de logboeken worden opgeslagen in een `.azure` directory zich in uw `user` directory.</span><span class="sxs-lookup"><span data-stu-id="bfbb9-180">Whether you log in with the `azure login` command or import publish settings, your CLI profile and logs are stored in a `.azure` directory located in your `user` directory.</span></span> <span data-ttu-id="bfbb9-181">Uw `user` map wordt beveiligd door het besturingssysteem.</span><span class="sxs-lookup"><span data-stu-id="bfbb9-181">Your `user` directory is protected by your operating system.</span></span> <span data-ttu-id="bfbb9-182">We raden u echter aan dat u extra stappen ondernemen voor het versleutelen van uw `user` directory.</span><span class="sxs-lookup"><span data-stu-id="bfbb9-182">However, we recommend that you take additional steps to encrypt your `user` directory.</span></span> <span data-ttu-id="bfbb9-183">U kunt dit op de volgende manieren doen:</span><span class="sxs-lookup"><span data-stu-id="bfbb9-183">You can do so in the following ways:</span></span>

* <span data-ttu-id="bfbb9-184">Van Windows, de mapeigenschappen van de wijzigen of gebruik van BitLocker.</span><span class="sxs-lookup"><span data-stu-id="bfbb9-184">On Windows, modify the directory properties or use BitLocker.</span></span>
* <span data-ttu-id="bfbb9-185">Schakel op de Mac, FileVault voor de map.</span><span class="sxs-lookup"><span data-stu-id="bfbb9-185">On Mac, turn on FileVault for the directory.</span></span>
* <span data-ttu-id="bfbb9-186">In Ubuntu gebruikt u de functie om de basismap te versleutelen.</span><span class="sxs-lookup"><span data-stu-id="bfbb9-186">On Ubuntu, use the Encrypted Home directory feature.</span></span> <span data-ttu-id="bfbb9-187">Andere Linux-distributies bieden vergelijkbare functies.</span><span class="sxs-lookup"><span data-stu-id="bfbb9-187">Other Linux distributions offer similar features.</span></span>

## <a name="logging-out"></a><span data-ttu-id="bfbb9-188">Afmelden</span><span class="sxs-lookup"><span data-stu-id="bfbb9-188">Logging out</span></span>
<span data-ttu-id="bfbb9-189">Meld u af met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="bfbb9-189">To log out, use the following command:</span></span>

    azure logout -u <username>

<span data-ttu-id="bfbb9-190">Als de abonnementen die zijn gekoppeld aan het account alleen met Active Directory, verwijderingen afmelden met informatie over het abonnement uit het lokale profiel worden geverifieerd.</span><span class="sxs-lookup"><span data-stu-id="bfbb9-190">If the subscriptions associated with the account are only authenticated with Active Directory, logging out deletes the subscription information from the local profile.</span></span> <span data-ttu-id="bfbb9-191">Echter, als een bestand met publicatie-instellingen ook voor de abonnementen is geïmporteerd, afmelden alleen verwijderingen Active Directory gegevens uit het lokale profiel gerelateerde.</span><span class="sxs-lookup"><span data-stu-id="bfbb9-191">However, if a publish settings file was also imported for the subscriptions, logging out only deletes Active Directory related information from the local profile.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bfbb9-192">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="bfbb9-192">Next steps</span></span>
* <span data-ttu-id="bfbb9-193">Zie voor het gebruik van Azure CLI-opdrachten [Azure CLI-opdrachten in de modus Resource Manager](virtual-machines/azure-cli-arm-commands.md) en [Azure CLI-opdrachten in de modus van de Service Management](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="bfbb9-193">To use Azure CLI commands, see [Azure CLI commands in Resource Manager mode](virtual-machines/azure-cli-arm-commands.md) and [Azure CLI commands in Service Management mode](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span></span>
* <span data-ttu-id="bfbb9-194">Als u meer informatie over de Azure CLI, broncode downloaden, problemen melden, of bijdragen aan het project, gaat u naar de [GitHub-opslagplaats voor de Azure CLI](https://github.com/azure/azure-xplat-cli).</span><span class="sxs-lookup"><span data-stu-id="bfbb9-194">To learn more about the Azure CLI, download source code, report problems, or contribute to the project, visit the [GitHub repository for the Azure CLI](https://github.com/azure/azure-xplat-cli).</span></span>
* <span data-ttu-id="bfbb9-195">Als u met de Azure CLI of Azure problemen, gaat u naar de [Azure-Forums](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurescripting).</span><span class="sxs-lookup"><span data-stu-id="bfbb9-195">If you encounter problems using the Azure CLI, or Azure, visit the [Azure Forums](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurescripting).</span></span>

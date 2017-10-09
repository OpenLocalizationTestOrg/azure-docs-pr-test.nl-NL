---
title: aaaLog in tooAzure van Hallo CLI | Microsoft Docs
description: Azure-abonnement tooyour vanaf hello Azure-opdrachtregelinterface (Azure CLI) verbinding te maken voor Mac, Linux en Windows
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
ms.openlocfilehash: 42682c00c8dea78b2c624e640379716d1d4d7a2d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="log-in-tooazure-from-hello-azure-cli"></a><span data-ttu-id="ab1f5-103">Meld u bij tooAzure van hello Azure CLI</span><span class="sxs-lookup"><span data-stu-id="ab1f5-103">Log in tooAzure from hello Azure CLI</span></span>
<span data-ttu-id="ab1f5-104">Hello Azure CLI is een set van open-source, platformoverschrijdende opdrachten voor het werken met Azure-resources.</span><span class="sxs-lookup"><span data-stu-id="ab1f5-104">hello Azure CLI is a set of open-source, cross-platform commands for working with Azure resources.</span></span> <span data-ttu-id="ab1f5-105">Dit artikel wordt beschreven Hallo verschillende manieren tooprovide Azure-account referenties tooconnect hello Azure CLI tooyour Azure-abonnement:</span><span class="sxs-lookup"><span data-stu-id="ab1f5-105">This article describes hello different ways tooprovide your Azure account credentials tooconnect hello Azure CLI tooyour Azure subscription:</span></span>

* <span data-ttu-id="ab1f5-106">Voer Hallo `azure login` CLI opdracht tooauthenticate via Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="ab1f5-106">Run hello `azure login` CLI command tooauthenticate through Azure Active Directory.</span></span> <span data-ttu-id="ab1f5-107">Deze methode biedt u toegang tot de opdrachten tooCLI in beide [opdracht modi](#cli-command-modes).</span><span class="sxs-lookup"><span data-stu-id="ab1f5-107">This method gives you access tooCLI commands in both [command modes](#cli-command-modes).</span></span> <span data-ttu-id="ab1f5-108">Wanneer u de opdracht Hallo zonder extra opties uitvoert `azure login` vraagt u toocontinue interactief aanmelden via een webportal.</span><span class="sxs-lookup"><span data-stu-id="ab1f5-108">When you run hello command without additional options, `azure login` prompts you toocontinue logging in interactively through a web portal.</span></span> <span data-ttu-id="ab1f5-109">Voor extra `azure login` opdracht Opties, Zie Hallo scenario's in dit artikel of type `azure login --help`.</span><span class="sxs-lookup"><span data-stu-id="ab1f5-109">For additional `azure login` command options, see hello scenarios in this article, or type `azure login --help`.</span></span>
* <span data-ttu-id="ab1f5-110">Als u moet alleen toouse Azure Service Management modus CLI-opdrachten (niet aanbevolen voor de meeste nieuwe implementaties), kunt u downloaden en installeren van een bestand met instellingen publiceren op uw computer.</span><span class="sxs-lookup"><span data-stu-id="ab1f5-110">If you only need toouse Azure Service Management mode CLI commands (not recommended for most new deployments), you can download and install a publish settings file on your computer.</span></span>

<span data-ttu-id="ab1f5-111">Als u nog niet Hallo CLI hebt geïnstalleerd, raadpleegt u [installeren hello Azure CLI](cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="ab1f5-111">If you haven't already installed hello CLI, see [Install hello Azure CLI](cli-install-nodejs.md).</span></span> <span data-ttu-id="ab1f5-112">Als u geen Azure-abonnement hebt, kunt u binnen een paar minuten een [gratis account](http://azure.microsoft.com/free/) maken.</span><span class="sxs-lookup"><span data-stu-id="ab1f5-112">If you don't have an Azure subscription, you can create a [free account](http://azure.microsoft.com/free/) in just a couple of minutes.</span></span>

<span data-ttu-id="ab1f5-113">Zie voor achtergrondinformatie over andere account-id's en Azure-abonnementen [hoe Azure-abonnementen worden gekoppeld aan Azure Active Directory](active-directory/active-directory-how-subscriptions-associated-directory.md).</span><span class="sxs-lookup"><span data-stu-id="ab1f5-113">For background about different account identities and Azure subscriptions, see [How Azure subscriptions are associated with Azure Active Directory](active-directory/active-directory-how-subscriptions-associated-directory.md).</span></span>

## <a name="scenario-1-azure-login-with-interactive-login"></a><span data-ttu-id="ab1f5-114">Scenario 1: azure-aanmelding met interactieve aanmelding</span><span class="sxs-lookup"><span data-stu-id="ab1f5-114">Scenario 1: azure login with interactive login</span></span>
<span data-ttu-id="ab1f5-115">Met bepaalde accounts Hallo CLI, moet u toorun `azure login` en ga vervolgens door Hallo aanmelding met een webbrowser via een webportal, een proces genaamd *interactieve aanmelding*.</span><span class="sxs-lookup"><span data-stu-id="ab1f5-115">With certain accounts, hello CLI requires you toorun `azure login` and then continue hello login process with a web browser through a web portal, a process called *interactive login*.</span></span> <span data-ttu-id="ab1f5-116">Een veelvoorkomende reden is wanneer u een account voor werk of school hebt (ook wel een *organisatieaccount*) die toorequire multifactor-verificatie is ingesteld.</span><span class="sxs-lookup"><span data-stu-id="ab1f5-116">A common reason is when you have a work or school account (also called an *organizational account*) that is set up toorequire multifactor authentication.</span></span> <span data-ttu-id="ab1f5-117">Ook interactieve aanmelding met je Microsoft-account gebruiken als u wilt dat de opdrachten in de modus Resource Manager toouse.</span><span class="sxs-lookup"><span data-stu-id="ab1f5-117">Also use interactive login with your Microsoft account, when you want toouse Resource Manager mode commands.</span></span>

<span data-ttu-id="ab1f5-118">Interactieve aanmelding is eenvoudig: type `azure login` --zonder opties--zoals weergegeven in Hallo voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="ab1f5-118">Interactive login is easy: type `azure login` -- without any options -- as shown in hello following example:</span></span>

```
azure login
```                                                                                             

<span data-ttu-id="ab1f5-119">Hallo-uitvoer wordt weergegeven dat lijkt op Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="ab1f5-119">hello output appears something like hello following:</span></span>

```         
info:    Executing command login
info:    toosign in, use a web browser tooopen hello page http://aka.ms/devicelogin. Enter hello code XXXXXXXXX tooauthenticate.
```
<span data-ttu-id="ab1f5-120">Hallo-code die worden aangeboden tooyou in de opdrachtuitvoer Hallo kopiëren en open een browser toohttp://aka.ms/devicelogin of een andere pagina als opgegeven.</span><span class="sxs-lookup"><span data-stu-id="ab1f5-120">Copy hello code offered tooyou in hello command output, and open a browser toohttp://aka.ms/devicelogin, or other page if specified.</span></span> <span data-ttu-id="ab1f5-121">(U kunt een browser op Hallo openen dezelfde computer of op een andere computer of apparaat.) Hallo-code invoeren, en vervolgens u na vragen aan gebruiker tooenter Hallo gebruikersnaam en wachtwoord voor de identiteit van de Hallo gewenste toouse.</span><span class="sxs-lookup"><span data-stu-id="ab1f5-121">(You can open a browser on hello same computer, or on a different computer or device.) Enter hello code, and then you are prompted tooenter hello username and password for hello identity you want toouse.</span></span> <span data-ttu-id="ab1f5-122">Wanneer dit proces is voltooid, geeft opdrachtshell Hallo Hallo aanmelding is voltooid.</span><span class="sxs-lookup"><span data-stu-id="ab1f5-122">When that process completes, hello command shell completes hello login.</span></span> <span data-ttu-id="ab1f5-123">Dit kan als volgt uitzien:</span><span class="sxs-lookup"><span data-stu-id="ab1f5-123">It might look something like:</span></span>

    info:    Added subscription Visual Studio Ultimate with MSDN
    info:    Added subscription Azure Free Trial
    info:    Setting subscription "Visual Studio Ultimate with MSDN" as default
    +
    info:    login command OK

> [!NOTE]
> <span data-ttu-id="ab1f5-124">Met interactieve aanmelding, worden verificatie en autorisatie uitgevoerd met Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="ab1f5-124">With interactive login, authentication and authorization are performed using Azure Active Directory.</span></span> <span data-ttu-id="ab1f5-125">Als u de identiteit van een Microsoft-account gebruikt, heeft uw Azure Active Directory-standaarddomein toegang tot Hallo-aanmelding.</span><span class="sxs-lookup"><span data-stu-id="ab1f5-125">If you use a Microsoft account identity, hello login process accesses your Azure Active Directory default domain.</span></span> <span data-ttu-id="ab1f5-126">(Als u zich aangemeld voor een gratis Azure-account, Azure Active Directory automatisch gemaakt een standaarddomein voor uw account.)</span><span class="sxs-lookup"><span data-stu-id="ab1f5-126">(If you signed up for a free Azure account, Azure Active Directory automatically created a default domain for your account.)</span></span>
>
>

## <a name="scenario-2-azure-login-with-a-username-and-password"></a><span data-ttu-id="ab1f5-127">Scenario 2: azure-aanmelding met een gebruikersnaam en wachtwoord</span><span class="sxs-lookup"><span data-stu-id="ab1f5-127">Scenario 2: azure login with a username and password</span></span>
<span data-ttu-id="ab1f5-128">Gebruik Hallo `azure login` opdracht met Hallo gebruikersnaam (`-u`) parameter tooauthenticate wanneer u wilt dat toouse een werk- of schoolaccount die geen multifactor-verificatie vereist.</span><span class="sxs-lookup"><span data-stu-id="ab1f5-128">Use hello `azure login` command with hello username (`-u`) parameter tooauthenticate when you want toouse a work or school account that doesn't require multifactor authentication.</span></span> <span data-ttu-id="ab1f5-129">U wordt gevraagd op de opdrachtregel Hallo Hallo wachtwoord (of u kunt eventueel Hallo wachtwoord doorgeven als een extra parameter Hallo `azure login` opdracht).</span><span class="sxs-lookup"><span data-stu-id="ab1f5-129">You are prompted at hello command line for hello password (or you can optionally pass hello password as an additional parameter of hello `azure login` command).</span></span> <span data-ttu-id="ab1f5-130">Hallo volgende voorbeeld wordt doorgegeven Hallo gebruikersnaam van een organisatie-account:</span><span class="sxs-lookup"><span data-stu-id="ab1f5-130">hello following example passes hello username of an organizational account:</span></span>

    azure login -u myUserName@contoso.onmicrosoft.com

<span data-ttu-id="ab1f5-131">U bent vervolgens tooenter gevraagd uw wachtwoord:</span><span class="sxs-lookup"><span data-stu-id="ab1f5-131">You are then prompted tooenter your password:</span></span>

    info:    Executing command login
    Password: *********

<span data-ttu-id="ab1f5-132">Hallo-aanmelding wordt voltooid.</span><span class="sxs-lookup"><span data-stu-id="ab1f5-132">hello login process then completes.</span></span>

    info:    Added subscription Visual Studio Ultimate with MSDN
    +
    info:    login command OK

<span data-ttu-id="ab1f5-133">Als dit de eerste keer aangemeld met deze referenties is, wordt u gevraagd tooverify dat u toocache geen verificatietoken wenst.</span><span class="sxs-lookup"><span data-stu-id="ab1f5-133">If this is your first time logging in with these credentials, you are asked tooverify that you wish toocache an authentication token.</span></span> <span data-ttu-id="ab1f5-134">Deze vraag vindt ook plaats als u eerder hebt gebruikt Hallo `azure logout` opdracht (beschreven in artikel hello later).</span><span class="sxs-lookup"><span data-stu-id="ab1f5-134">This prompt also occurs if you previously used hello `azure logout` command (described later in hello article).</span></span> <span data-ttu-id="ab1f5-135">toobypass deze prompt voor automatiseringsscenario's uitgevoerd `azure login` Hello `-q` parameter.</span><span class="sxs-lookup"><span data-stu-id="ab1f5-135">toobypass this prompt for automation scenarios, run `azure login` with hello `-q` parameter.</span></span>

## <a name="scenario-3-azure-login-with-a-service-principal"></a><span data-ttu-id="ab1f5-136">Scenario 3: azure-aanmelding met een service-principal</span><span class="sxs-lookup"><span data-stu-id="ab1f5-136">Scenario 3: azure login with a service principal</span></span>
<span data-ttu-id="ab1f5-137">Als u een service-principal voor een Active Directory-toepassing maakt en service-principal Hallo machtigingen op uw abonnement heeft, kunt u Hallo `azure login` opdracht tooauthenticate Hallo service-principal.</span><span class="sxs-lookup"><span data-stu-id="ab1f5-137">If you create a service principal for an Active Directory application, and hello service principal has permissions on your subscription, you can use hello `azure login` command tooauthenticate hello service principal.</span></span> <span data-ttu-id="ab1f5-138">Afhankelijk van uw scenario kan u referenties van de service-principal Hallo Hallo opgeven als expliciete parameters Hallo `azure login` opdracht.</span><span class="sxs-lookup"><span data-stu-id="ab1f5-138">Depending on your scenario, you could provide hello credentials of hello service principal as explicit parameters of hello `azure login` command.</span></span> <span data-ttu-id="ab1f5-139">Bijvoorbeeld: hello volgende opdracht wordt doorgegeven Hallo service principal name en Active Directory-tenant-ID:</span><span class="sxs-lookup"><span data-stu-id="ab1f5-139">For example, hello following command passes hello service principal name and Active Directory tenant ID:</span></span>

    azure login -u https://www.contoso.org/example --service-principal --tenant myTenantID

<span data-ttu-id="ab1f5-140">U bent na vragen aan gebruiker tooprovide Hallo wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="ab1f5-140">You are then prompted tooprovide hello password.</span></span> <span data-ttu-id="ab1f5-141">U kunt ook Hallo referenties via een CLI script of toepassing code, of gebruik een certificaat tooauthenticate Hallo service-principal niet-interactief voor automatiseringsscenario's.</span><span class="sxs-lookup"><span data-stu-id="ab1f5-141">You can also provide hello credentials through a CLI script or application code, or use a certificate tooauthenticate hello service principal non-interactively for automation scenarios.</span></span> <span data-ttu-id="ab1f5-142">Zie voor meer informatie en voorbeelden [verifiëren van een service-principal met Azure Resource Manager](resource-group-authenticate-service-principal-cli.md).</span><span class="sxs-lookup"><span data-stu-id="ab1f5-142">For details and examples, see [Authenticating a service principal with Azure Resource Manager](resource-group-authenticate-service-principal-cli.md).</span></span>

## <a name="scenario-4-use-a-publish-settings-file"></a><span data-ttu-id="ab1f5-143">Scenario 4: Gebruik een bestand met publicatie-instellingen</span><span class="sxs-lookup"><span data-stu-id="ab1f5-143">Scenario 4: Use a publish settings file</span></span>
<span data-ttu-id="ab1f5-144">Als u moet alleen toouse hello Azure Service Management modus CLI-opdrachten (bijvoorbeeld toodeploy Azure VM's in het klassieke implementatiemodel Hallo), kunt u verbinding maken met behulp van een bestand met publicatie-instellingen.</span><span class="sxs-lookup"><span data-stu-id="ab1f5-144">If you only need toouse hello Azure Service Management mode CLI commands (for example, toodeploy Azure VMs in hello classic deployment model), you can connect using a publish settings file.</span></span> <span data-ttu-id="ab1f5-145">Deze methode wordt een certificaat geïnstalleerd op uw lokale computer waarmee u beheertaken tooperform voor zolang Hallo-abonnement en het Hallo-certificaat geldig zijn.</span><span class="sxs-lookup"><span data-stu-id="ab1f5-145">This method installs a certificate on your local computer that allows you tooperform management tasks for as long as hello subscription and hello certificate are valid.</span></span>

* <span data-ttu-id="ab1f5-146">**Hallo toodownload bestand publicatie-instellingen** Zorg ervoor dat Hallo CLI in Service Management-modus door in te voeren is voor uw account `azure config mode asm`.</span><span class="sxs-lookup"><span data-stu-id="ab1f5-146">**toodownload hello publish settings file** for your account, ensure that hello CLI is in Service Management mode by typing `azure config mode asm`.</span></span> <span data-ttu-id="ab1f5-147">Voer vervolgens de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="ab1f5-147">Then run hello following command:</span></span>

        azure account download

<span data-ttu-id="ab1f5-148">Hiermee opent u de standaardbrowser en vraagt u toosign in toohello [klassieke Azure-portal](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="ab1f5-148">This opens your default browser and prompts you toosign in toohello [Azure classic portal](https://manage.windowsazure.com).</span></span> <span data-ttu-id="ab1f5-149">Nadat u zich aanmeldt, een `.publishsettings` bestand downloads.</span><span class="sxs-lookup"><span data-stu-id="ab1f5-149">After you sign in, a `.publishsettings` file downloads.</span></span> <span data-ttu-id="ab1f5-150">Noteer waar dit bestand wordt opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="ab1f5-150">Make note of where this file is saved.</span></span>

> [!NOTE]
> <span data-ttu-id="ab1f5-151">Als uw account gekoppeld aan meerdere tenants van Azure Active Directory is, hebt u mogelijk na vragen aan gebruiker tooselect die Active Directory die u wenst toodownload publicatie-instellingen voor het bestand.</span><span class="sxs-lookup"><span data-stu-id="ab1f5-151">If your account is associated with multiple Azure Active Directory tenants, you may be prompted tooselect which Active Directory you wish toodownload a publish settings file for.</span></span>
>
>

<span data-ttu-id="ab1f5-152">Wanneer met behulp van de downloadpagina Hallo of via de klassieke Azure-portal Hallo wordt Hallo geselecteerde Active Directory Hallo standaardwaarde gebruikt door de klassieke portal Hallo en downloadpagina.</span><span class="sxs-lookup"><span data-stu-id="ab1f5-152">Once selected using hello download page, or by visiting hello Azure classic portal, hello selected Active Directory becomes hello default used by hello classic portal and download page.</span></span> <span data-ttu-id="ab1f5-153">Nadat een standaard is ingesteld, ziet u de tekst hello '**Klik hier tooreturn toohello selectiepagina**' hello boven aan het Hallo-downloadpagina.</span><span class="sxs-lookup"><span data-stu-id="ab1f5-153">Once a default has been established, you see hello text '**click here tooreturn toohello selection page**' at hello top of hello download page.</span></span> <span data-ttu-id="ab1f5-154">Hallo opgegeven koppeling tooreturn toohello selectiepagina gebruiken.</span><span class="sxs-lookup"><span data-stu-id="ab1f5-154">Use hello provided link tooreturn toohello selection page.</span></span>

* <span data-ttu-id="ab1f5-155">**Hallo tooimport bestand publicatie-instellingen**, voert hello volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="ab1f5-155">**tooimport hello publish settings file**, run hello following command:</span></span>

        azure account import <path tooyour .publishsettings file>

> [!IMPORTANT]
> <span data-ttu-id="ab1f5-156">Na het importeren van de publicatie-instellingen, verwijdert u Hallo `.publishsettings` bestand.</span><span class="sxs-lookup"><span data-stu-id="ab1f5-156">After importing your publish settings, you should delete hello `.publishsettings` file.</span></span> <span data-ttu-id="ab1f5-157">Het is niet langer vereist voor hello Azure CLI en vormt een beveiligingsrisico, omdat als het gebruikte toogain toegang tooyour abonnement mogelijk.</span><span class="sxs-lookup"><span data-stu-id="ab1f5-157">It is no longer required by hello Azure CLI and presents a security risk as it could be used toogain access tooyour subscription.</span></span>
>
>

## <a name="cli-command-modes"></a><span data-ttu-id="ab1f5-158">CLI-opdrachtmodi</span><span class="sxs-lookup"><span data-stu-id="ab1f5-158">CLI command modes</span></span>
<span data-ttu-id="ab1f5-159">Hello Azure CLI biedt twee opdrachtmodi voor het werken met Azure-resources met andere opdrachtsets:</span><span class="sxs-lookup"><span data-stu-id="ab1f5-159">hello Azure CLI provides two command modes for working with Azure resources, with different command sets:</span></span>

* <span data-ttu-id="ab1f5-160">**Resource Manager-modus** : voor het werken met Azure-resources in Hallo Resource Manager-implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="ab1f5-160">**Resource Manager mode** - for working with Azure resources in hello Resource Manager deployment model.</span></span> <span data-ttu-id="ab1f5-161">tooset deze modus wordt uitgevoerd `azure config mode arm`.</span><span class="sxs-lookup"><span data-stu-id="ab1f5-161">tooset this mode, run `azure config mode arm`.</span></span>
* <span data-ttu-id="ab1f5-162">**Service Management-modus** : voor het werken met Azure-resources in het klassieke implementatiemodel Hallo.</span><span class="sxs-lookup"><span data-stu-id="ab1f5-162">**Service Management mode** - for working with Azure resources in hello classic deployment model.</span></span> <span data-ttu-id="ab1f5-163">tooset deze modus wordt uitgevoerd `azure config mode asm`.</span><span class="sxs-lookup"><span data-stu-id="ab1f5-163">tooset this mode, run `azure config mode asm`.</span></span>

<span data-ttu-id="ab1f5-164">Toen geïnstalleerd, Hallo huidige release van Hallo die CLI bevindt zich in de modus Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="ab1f5-164">When first installed, hello current release of hello CLI is in Resource Manager mode.</span></span>

> [!NOTE]
> <span data-ttu-id="ab1f5-165">Hallo Resource Manager en Service Management-modus elkaar wederzijds uit.</span><span class="sxs-lookup"><span data-stu-id="ab1f5-165">hello Resource Manager mode and Service Management mode are mutually exclusive.</span></span> <span data-ttu-id="ab1f5-166">Dat wil zeggen, resources die zijn gemaakt in de modus voor één kunnen niet worden beheerd vanaf Hallo andere modus.</span><span class="sxs-lookup"><span data-stu-id="ab1f5-166">That is, resources created in one mode cannot be managed from hello other mode.</span></span>
>
>

## <a name="multiple-subscriptions"></a><span data-ttu-id="ab1f5-167">Meerdere abonnementen</span><span class="sxs-lookup"><span data-stu-id="ab1f5-167">Multiple subscriptions</span></span>
<span data-ttu-id="ab1f5-168">Als u meerdere Azure-abonnementen hebt, verleent toegang tooall abonnementen die zijn gekoppeld aan uw referenties als u tooAzure verbinding te maken.</span><span class="sxs-lookup"><span data-stu-id="ab1f5-168">If you have multiple Azure subscriptions, connecting tooAzure grants access tooall subscriptions associated with your credentials.</span></span> <span data-ttu-id="ab1f5-169">Een abonnement is Hallo standaard geselecteerd en gebruikt door hello Azure CLI bij het uitvoeren van bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="ab1f5-169">One subscription is selected as hello default, and used by hello Azure CLI when performing operations.</span></span> <span data-ttu-id="ab1f5-170">Vindt u Hallo abonnementen, met inbegrip van de huidige standaardabonnement hello, met behulp van Hallo `azure account list` opdracht.</span><span class="sxs-lookup"><span data-stu-id="ab1f5-170">You can view hello subscriptions, including hello current default subscription, using hello `azure account list` command.</span></span> <span data-ttu-id="ab1f5-171">Met deze opdracht retourneert informatie vergelijkbare toohello volgende:</span><span class="sxs-lookup"><span data-stu-id="ab1f5-171">This command returns information similar toohello following:</span></span>

    info:    Executing command account list
    data:    Name              Id                                    Current
    data:    ----------------  ------------------------------------  -------
    data:    Azure-sub-1       ####################################  true
    data:    Azure-sub-2       ####################################  false

<span data-ttu-id="ab1f5-172">Hallo in Hallo voorafgaand aan de lijst, **huidige** kolom wordt aangegeven Hallo huidige standaardabonnement als Azure-sub-1.</span><span class="sxs-lookup"><span data-stu-id="ab1f5-172">In hello preceding list, hello **Current** column indicates hello current default subscription as Azure-sub-1.</span></span> <span data-ttu-id="ab1f5-173">toochange hello standaardabonnement, gebruik Hallo `azure account set` opdracht in en geef Hallo-abonnement dat u wenst dat toobe Hallo standaard.</span><span class="sxs-lookup"><span data-stu-id="ab1f5-173">toochange hello default subscription, use hello `azure account set` command, and specify hello subscription that you wish toobe hello default.</span></span> <span data-ttu-id="ab1f5-174">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="ab1f5-174">For example:</span></span>

    azure account set Azure-sub-2

<span data-ttu-id="ab1f5-175">Hiermee wijzigt u Hallo standaard abonnement tooAzure-sub-2.</span><span class="sxs-lookup"><span data-stu-id="ab1f5-175">This changes hello default subscription tooAzure-sub-2.</span></span>

> [!NOTE]
> <span data-ttu-id="ab1f5-176">Hallo standaardabonnement wijzigen wordt direct van kracht en is een algemene wijziging; nieuwe Azure CLI-opdrachten, of u deze uit uitvoeren Hallo dezelfde opdrachtregelprogramma exemplaar of een ander exemplaar, nieuwe standaardabonnement hello gebruiken.</span><span class="sxs-lookup"><span data-stu-id="ab1f5-176">Changing hello default subscription takes effect immediately, and is a global change; new Azure CLI commands, whether you run them from hello same command-line instance or a different instance, use hello new default subscription.</span></span>
>
>

<span data-ttu-id="ab1f5-177">Als u toouse een niet-standaard-abonnement met hello Azure CLI wilt, maar niet dat toochange Hallo huidige standaard wilt, kunt u Hallo `--subscription` optie voor de opdracht Hallo en geef Hallo Hallo-abonnement dat u wenst dat toouse voor Hallo-bewerking.</span><span class="sxs-lookup"><span data-stu-id="ab1f5-177">If you wish toouse a non-default subscription with hello Azure CLI, but don't want toochange hello current default, you can use hello `--subscription` option for hello command and provide hello name of hello subscription you wish toouse for hello operation.</span></span>

<span data-ttu-id="ab1f5-178">Wanneer u verbonden tooyour Azure-abonnement bent, kunt u beginnen met behulp van hello Azure CLI-opdrachten toowork met Azure-resources.</span><span class="sxs-lookup"><span data-stu-id="ab1f5-178">Once you are connected tooyour Azure subscription, you can start using hello Azure CLI commands toowork with Azure resources.</span></span>

## <a name="storage-of-cli-settings"></a><span data-ttu-id="ab1f5-179">Opslag van CLI-instellingen</span><span class="sxs-lookup"><span data-stu-id="ab1f5-179">Storage of CLI settings</span></span>
<span data-ttu-id="ab1f5-180">Hiermee wordt aangegeven of u aanmelden met Hallo `azure login` opdracht of het importeren van publicatie-instellingen, uw CLI-profiel en de logboeken worden opgeslagen in een `.azure` directory zich in uw `user` directory.</span><span class="sxs-lookup"><span data-stu-id="ab1f5-180">Whether you log in with hello `azure login` command or import publish settings, your CLI profile and logs are stored in a `.azure` directory located in your `user` directory.</span></span> <span data-ttu-id="ab1f5-181">Uw `user` map wordt beveiligd door het besturingssysteem.</span><span class="sxs-lookup"><span data-stu-id="ab1f5-181">Your `user` directory is protected by your operating system.</span></span> <span data-ttu-id="ab1f5-182">We raden u echter aan dat u rekening houden met extra stappen tooencrypt uw `user` directory.</span><span class="sxs-lookup"><span data-stu-id="ab1f5-182">However, we recommend that you take additional steps tooencrypt your `user` directory.</span></span> <span data-ttu-id="ab1f5-183">U kunt dit doen in de volgende manieren Hallo:</span><span class="sxs-lookup"><span data-stu-id="ab1f5-183">You can do so in hello following ways:</span></span>

* <span data-ttu-id="ab1f5-184">Hallo directory eigenschappen wijzigen van Windows, of gebruik van BitLocker.</span><span class="sxs-lookup"><span data-stu-id="ab1f5-184">On Windows, modify hello directory properties or use BitLocker.</span></span>
* <span data-ttu-id="ab1f5-185">Schakel op de Mac, FileVault voor Hallo-directory.</span><span class="sxs-lookup"><span data-stu-id="ab1f5-185">On Mac, turn on FileVault for hello directory.</span></span>
* <span data-ttu-id="ab1f5-186">Op Ubuntu, Hallo versleutelde Home directory functie te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="ab1f5-186">On Ubuntu, use hello Encrypted Home directory feature.</span></span> <span data-ttu-id="ab1f5-187">Andere Linux-distributies bieden vergelijkbare functies.</span><span class="sxs-lookup"><span data-stu-id="ab1f5-187">Other Linux distributions offer similar features.</span></span>

## <a name="logging-out"></a><span data-ttu-id="ab1f5-188">Afmelden</span><span class="sxs-lookup"><span data-stu-id="ab1f5-188">Logging out</span></span>
<span data-ttu-id="ab1f5-189">toolog uit gebruik Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="ab1f5-189">toolog out, use hello following command:</span></span>

    azure logout -u <username>

<span data-ttu-id="ab1f5-190">Als Hallo abonnementen die zijn gekoppeld aan worden Hallo account alleen met Active Directory, logboekregistratie verwijderingen Hallo abonnement informatie uit het lokale profiel Hallo geverifieerde.</span><span class="sxs-lookup"><span data-stu-id="ab1f5-190">If hello subscriptions associated with hello account are only authenticated with Active Directory, logging out deletes hello subscription information from hello local profile.</span></span> <span data-ttu-id="ab1f5-191">Echter, als een bestand met publicatie-instellingen ook voor Hallo abonnementen is geïmporteerd, afmelden alleen verwijderingen Active Directory gegevens uit het lokale profiel Hallo gerelateerde.</span><span class="sxs-lookup"><span data-stu-id="ab1f5-191">However, if a publish settings file was also imported for hello subscriptions, logging out only deletes Active Directory related information from hello local profile.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ab1f5-192">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="ab1f5-192">Next steps</span></span>
* <span data-ttu-id="ab1f5-193">toouse Azure CLI-opdrachten, Zie [Azure CLI-opdrachten in de modus Resource Manager](virtual-machines/azure-cli-arm-commands.md) en [Azure CLI-opdrachten in de modus van de Service Management](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="ab1f5-193">toouse Azure CLI commands, see [Azure CLI commands in Resource Manager mode](virtual-machines/azure-cli-arm-commands.md) and [Azure CLI commands in Service Management mode](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span></span>
* <span data-ttu-id="ab1f5-194">toolearn meer informatie over hello Azure CLI broncode downloaden, problemen, rapport of bijdragen toohello project, gaat u naar Hallo [GitHub-opslagplaats voor hello Azure CLI](https://github.com/azure/azure-xplat-cli).</span><span class="sxs-lookup"><span data-stu-id="ab1f5-194">toolearn more about hello Azure CLI, download source code, report problems, or contribute toohello project, visit hello [GitHub repository for hello Azure CLI](https://github.com/azure/azure-xplat-cli).</span></span>
* <span data-ttu-id="ab1f5-195">Als u met hello Azure CLI of Azure problemen, gaat u naar Hallo [Azure-Forums](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurescripting).</span><span class="sxs-lookup"><span data-stu-id="ab1f5-195">If you encounter problems using hello Azure CLI, or Azure, visit hello [Azure Forums](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurescripting).</span></span>

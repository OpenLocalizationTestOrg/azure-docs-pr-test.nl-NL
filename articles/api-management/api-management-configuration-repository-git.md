---
title: aaaConfigure uw API Management-service met Git - Azure | Microsoft Docs
description: Meer informatie over hoe toosave en configureren van de configuratie van uw API Management-service met Git.
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: mattfarm
ms.assetid: 364cd53e-88fb-4301-a093-f132fa1f88f5
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: ef7d4c18f2ea3f5c9b86403349a83aef240f979b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosave-and-configure-your-api-management-service-configuration-using-git"></a><span data-ttu-id="43876-103">Hoe toosave en configureren van de configuratie van uw API Management-service met Git</span><span class="sxs-lookup"><span data-stu-id="43876-103">How toosave and configure your API Management service configuration using Git</span></span>
> 
> 

<span data-ttu-id="43876-104">Elk exemplaar van API Management-service houdt een configuratiedatabase die informatie over het Hallo-configuratie en metagegevens voor Hallo service-exemplaar bevat.</span><span class="sxs-lookup"><span data-stu-id="43876-104">Each API Management service instance maintains a configuration database that contains information about hello configuration and metadata for hello service instance.</span></span> <span data-ttu-id="43876-105">Wijzigingen kunnen toohello service-exemplaar worden gemaakt door een instelling in de publicatieportal hello te wijzigen, gebruikt een PowerShell-cmdlet of REST API-aanroep.</span><span class="sxs-lookup"><span data-stu-id="43876-105">Changes can be made toohello service instance by changing a setting in hello publisher portal, using a PowerShell cmdlet, or making a REST API call.</span></span> <span data-ttu-id="43876-106">Bovendien toothese methoden, kunt u ook beheren de serviceconfiguratie-exemplaar met behulp van Git, service management-scenario's zoals inschakelen:</span><span class="sxs-lookup"><span data-stu-id="43876-106">In addition toothese methods, you can also manage your service instance configuration using Git, enabling service management scenarios such as:</span></span>

* <span data-ttu-id="43876-107">Configuratie versioning - downloaden en opslaan van verschillende versies van de serviceconfiguratie</span><span class="sxs-lookup"><span data-stu-id="43876-107">Configuration versioning - download and store different versions of your service configuration</span></span>
* <span data-ttu-id="43876-108">Bulksgewijs configuratiewijzigingen - toomultiple delen van de serviceconfiguratie wijzigingen aanbrengen in uw lokale opslagplaats en Hallo wijzigingen back toohello server integreren met een enkele bewerking</span><span class="sxs-lookup"><span data-stu-id="43876-108">Bulk configuration changes - make changes toomultiple parts of your service configuration in your local repository and integrate hello changes back toohello server with a single operation</span></span>
* <span data-ttu-id="43876-109">Vertrouwde Git toolchain en workflow - Hallo Git tooling en werkstromen die u al bekend met bent gebruiken</span><span class="sxs-lookup"><span data-stu-id="43876-109">Familiar Git toolchain and workflow - use hello Git tooling and workflows that you are already familiar with</span></span>

<span data-ttu-id="43876-110">Hallo volgende diagram geeft een overzicht van Hallo verschillende manieren tooconfigure uw API Management-service-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="43876-110">hello following diagram shows an overview of hello different ways tooconfigure your API Management service instance.</span></span>

![GIT configureren][api-management-git-configure]

<span data-ttu-id="43876-112">Wanneer u wijzigingen tooyour-service met behulp van de publicatieportal hello, PowerShell-cmdlets of Hallo REST-API aanbrengt, beheert u uw service-configuratiedatabase Hallo `https://{name}.management.azure-api.net` eindpunt, zoals wordt weergegeven aan de rechterkant Hallo van Hallo-diagram.</span><span class="sxs-lookup"><span data-stu-id="43876-112">When you make changes tooyour service using hello publisher portal, PowerShell cmdlets, or hello REST API, you are managing your service configuration database using hello `https://{name}.management.azure-api.net` endpoint, as shown on hello right side of hello diagram.</span></span> <span data-ttu-id="43876-113">Hallo links van Hallo diagram ziet u hoe u de configuratie van uw service met Git kunt beheren en Git-opslagplaats voor uw service zich bevindt op `https://{name}.scm.azure-api.net`.</span><span class="sxs-lookup"><span data-stu-id="43876-113">hello left side of hello diagram illustrates how you can manage your service configuration using Git and Git repository for your service located at `https://{name}.scm.azure-api.net`.</span></span>

<span data-ttu-id="43876-114">Hallo stappen geven een overzicht van het beheer van uw API Management-service-exemplaar met Git.</span><span class="sxs-lookup"><span data-stu-id="43876-114">hello following steps provide an overview of managing your API Management service instance using Git.</span></span>

1. <span data-ttu-id="43876-115">Toegang tot de configuratie van Git in uw service</span><span class="sxs-lookup"><span data-stu-id="43876-115">Access Git configuration in your service</span></span>
2. <span data-ttu-id="43876-116">Opslaan van uw service configuration database tooyour Git-opslagplaats</span><span class="sxs-lookup"><span data-stu-id="43876-116">Save your service configuration database tooyour Git repository</span></span>
3. <span data-ttu-id="43876-117">Hallo Git-opslagplaats tooyour lokale machine worden gekloond</span><span class="sxs-lookup"><span data-stu-id="43876-117">Clone hello Git repo tooyour local machine</span></span>
4. <span data-ttu-id="43876-118">Ophalen van de meest recente opslagplaats Hallo omlaag tooyour lokale computer en doorvoeren en push wijzigingen back tooyour opslagplaats</span><span class="sxs-lookup"><span data-stu-id="43876-118">Pull hello latest repo down tooyour local machine, and commit and push changes back tooyour repo</span></span>
5. <span data-ttu-id="43876-119">Hallo wijzigingen uit de opslagplaats naar uw database van de configuration-service implementeren</span><span class="sxs-lookup"><span data-stu-id="43876-119">Deploy hello changes from your repo into your service configuration database</span></span>

<span data-ttu-id="43876-120">Dit artikel wordt beschreven hoe tooenable en gebruik Git toomanage de serviceconfiguratie bevat naslaginformatie voor Hallo bestanden en mappen in Hallo Git-opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="43876-120">This article describes how tooenable and use Git toomanage your service configuration and provides a reference for hello files and folders in hello Git repository.</span></span>

## <a name="access-git-configuration-in-your-service"></a><span data-ttu-id="43876-121">Toegang tot de configuratie van Git in uw service</span><span class="sxs-lookup"><span data-stu-id="43876-121">Access Git configuration in your service</span></span>
<span data-ttu-id="43876-122">U kunt snel Hallo status van de Git-configuratie door bekijkt hello Git-pictogram in de Hallo rechterbovenhoek van de publicatieportal Hallo weergeven.</span><span class="sxs-lookup"><span data-stu-id="43876-122">You can quickly view hello status of your Git configuration by viewing hello Git icon in hello upper-right corner of hello publisher portal.</span></span> <span data-ttu-id="43876-123">In dit voorbeeld status het Hallo-bericht geeft aan dat er niet-opgeslagen wijzigingen toohello opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="43876-123">In this example, hello status message indicates that there are unsaved changes toohello repository.</span></span> <span data-ttu-id="43876-124">Dit komt doordat de configuratiedatabase van Hallo API Management-service is nog niet zijn opgeslagen toohello opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="43876-124">This is because hello API Management service configuration database has not yet been saved toohello repository.</span></span>

![GIT-status][api-management-git-icon-enable]

<span data-ttu-id="43876-126">tooview en de Git-configuratie-instellingen configureren, u kunt Hallo Git pictogram klikt u op of klik op Hallo **beveiliging** menu en navigeer toohello **configuratie opslagplaats** tabblad.</span><span class="sxs-lookup"><span data-stu-id="43876-126">tooview and configure your Git configuration settings, you can either click hello Git icon, or click hello **Security** menu and navigate toohello **Configuration repository** tab.</span></span>

![GIT inschakelen][api-management-enable-git]

> [!IMPORTANT]
> <span data-ttu-id="43876-128">Geen geheimen die niet zijn gedefinieerd zoals eigenschappen worden opgeslagen in de opslagplaats hello en in de geschiedenis totdat u blijft uitschakelen en opnieuw inschakelen Git.</span><span class="sxs-lookup"><span data-stu-id="43876-128">Any secrets that are not defined as properties will be stored in hello repository and will remain in its history until you disable and re-enable Git access.</span></span> <span data-ttu-id="43876-129">Eigenschappen van een veilige plaats toomanage bieden constante string-waarden, inclusief geheimen, voor alle configuratie-API en beleidsregels, dus u geen toostore hebt ze rechtstreeks in uw beleidsverklaringen.</span><span class="sxs-lookup"><span data-stu-id="43876-129">Properties provide a secure place toomanage constant string values, including secrets, across all API configuration and policies, so you don't have toostore them directly in your policy statements.</span></span> <span data-ttu-id="43876-130">Zie voor meer informatie [hoe toouse eigenschappen in Azure API Management-beleidsregels](api-management-howto-properties.md).</span><span class="sxs-lookup"><span data-stu-id="43876-130">For more information, see [How toouse properties in Azure API Management policies](api-management-howto-properties.md).</span></span>
> 
> 

<span data-ttu-id="43876-131">Zie voor meer informatie over het inschakelen of uitschakelen via Hallo REST-API toegang tot een Git [in- of uitschakelen via Hallo REST-API toegang tot een Git](https://msdn.microsoft.com/library/dn781420.aspx#EnableGit).</span><span class="sxs-lookup"><span data-stu-id="43876-131">For information on enabling or disabling Git access using hello REST API, see [Enable or disable Git access using hello REST API](https://msdn.microsoft.com/library/dn781420.aspx#EnableGit).</span></span>

## <a name="toosave-hello-service-configuration-toohello-git-repository"></a><span data-ttu-id="43876-132">toosave hello service configuration toohello Git-opslagplaats</span><span class="sxs-lookup"><span data-stu-id="43876-132">toosave hello service configuration toohello Git repository</span></span>
<span data-ttu-id="43876-133">eerste stap van de Hallo voorafgaand aan het kopiëren van de opslagplaats Hallo is toosave Hallo huidige status van Hallo service configuration toohello opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="43876-133">hello first step before cloning hello repository is toosave hello current state of hello service configuration toohello repository.</span></span> <span data-ttu-id="43876-134">Klik op **opslaan configuratie toorepository**.</span><span class="sxs-lookup"><span data-stu-id="43876-134">Click **Save configuration toorepository**.</span></span>

![Configuratie op te slaan][api-management-save-configuration]

<span data-ttu-id="43876-136">Breng de gewenste wijzigingen op Hallo bevestigingsscherm en klik op **Ok** toosave.</span><span class="sxs-lookup"><span data-stu-id="43876-136">Make any desired changes on hello confirmation screen and click **Ok** toosave.</span></span>

![Configuratie op te slaan][api-management-save-configuration-confirm]

<span data-ttu-id="43876-138">Na enkele ogenblikken Hallo-configuratie is opgeslagen en Hallo configuratiestatus van Hallo opslagplaats wordt weergegeven, inclusief Hallo datum en tijd van laatste configuratiewijziging Hallo en Hallo laatste synchronisatie tussen Hallo-serviceconfiguratie en Hallo opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="43876-138">After a few moments hello configuration is saved, and hello configuration status of hello repository is displayed, including hello date and time of hello last configuration change and hello last synchronization between hello service configuration and hello repository.</span></span>

![Configuratiestatus][api-management-configuration-status]

<span data-ttu-id="43876-140">Zodra Hallo-configuratie is opgeslagen toohello opslagplaats, kunnen worden gekloond.</span><span class="sxs-lookup"><span data-stu-id="43876-140">Once hello configuration is saved toohello repository, it can be cloned.</span></span>

<span data-ttu-id="43876-141">Zie voor informatie over het uitvoeren van deze bewerking met Hallo REST-API, [doorvoeren configuratie momentopname over met Hallo REST-API](https://msdn.microsoft.com/library/dn781420.aspx#CommitSnapshot).</span><span class="sxs-lookup"><span data-stu-id="43876-141">For information on performing this operation using hello REST API, see [Commit configuration snapshot using hello REST API](https://msdn.microsoft.com/library/dn781420.aspx#CommitSnapshot).</span></span>

## <a name="tooclone-hello-repository-tooyour-local-machine"></a><span data-ttu-id="43876-142">tooclone hello opslagplaats tooyour lokale computer</span><span class="sxs-lookup"><span data-stu-id="43876-142">tooclone hello repository tooyour local machine</span></span>
<span data-ttu-id="43876-143">tooclone een opslagplaats, moet u Hallo URL tooyour opslagplaats, een gebruikersnaam en een wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="43876-143">tooclone a repository, you need hello URL tooyour repository, a user name, and a password.</span></span> <span data-ttu-id="43876-144">Hallo gebruikersnaam en -URL worden weergegeven aan de bovenkant Hallo Hallo **configuratie opslagplaats** tabblad.</span><span class="sxs-lookup"><span data-stu-id="43876-144">hello user name and URL are displayed near hello top of hello **Configuration repository** tab.</span></span>

![GIT kloon][api-management-configuration-git-clone]

<span data-ttu-id="43876-146">Hallo-wachtwoord wordt gegenereerd aan de onderkant Hallo Hallo **configuratie opslagplaats** tabblad.</span><span class="sxs-lookup"><span data-stu-id="43876-146">hello password is generated at hello bottom of hello **Configuration repository** tab.</span></span>

![Wachtwoord genereren][api-management-generate-password]

<span data-ttu-id="43876-148">toogenerate een wachtwoord, eerst voor zorgen dat Hallo **verstrijken** toohello gewenst datum en tijd instellen en klik vervolgens op **Token genereren**.</span><span class="sxs-lookup"><span data-stu-id="43876-148">toogenerate a password, first ensure that hello **Expiry** is set toohello desired expiration date and time, and then click **Generate Token**.</span></span>

![Wachtwoord][api-management-password]

> [!IMPORTANT]
> <span data-ttu-id="43876-150">Noteer dit wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="43876-150">Make a note of this password.</span></span> <span data-ttu-id="43876-151">Als u deze pagina Hallo-wachtwoord niet opnieuw weergegeven.</span><span class="sxs-lookup"><span data-stu-id="43876-151">Once you leave this page hello password will not be displayed again.</span></span>
> 
> 

<span data-ttu-id="43876-152">Hallo volgen voorbeelden gebruik Git Bash Hallo hulpprogramma van [Git voor Windows](http://www.git-scm.com/downloads) , maar u kunt een Git-hulpmiddel dat u bekend met bent.</span><span class="sxs-lookup"><span data-stu-id="43876-152">hello following examples use hello Git Bash tool from [Git for Windows](http://www.git-scm.com/downloads) but you can use any Git tool that you are familiar with.</span></span>

<span data-ttu-id="43876-153">Open uw Git-hulpprogramma in de gewenste map Hallo en Hallo opdracht tooclone Hallo git-opslagplaats tooyour lokale computer te volgen, geleverd door de publicatieportal Hallo Hallo-opdracht uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="43876-153">Open your Git tool in hello desired folder and run hello following command tooclone hello git repository tooyour local machine, using hello command provided by hello publisher portal.</span></span>

```
git clone https://bugbashdev4.scm.azure-api.net/
```

<span data-ttu-id="43876-154">Geef Hallo-gebruikersnaam en wachtwoord wanneer u wordt gevraagd.</span><span class="sxs-lookup"><span data-stu-id="43876-154">Provide hello user name and password when prompted.</span></span>

<span data-ttu-id="43876-155">Als u eventuele fouten ontvangt, probeert u het wijzigen van uw `git clone` opdracht tooinclude Hallo-gebruikersnaam en wachtwoord, zoals wordt weergegeven in Hallo voorbeeld te volgen.</span><span class="sxs-lookup"><span data-stu-id="43876-155">If you receive any errors, try modifying your `git clone` command tooinclude hello user name and password, as shown in hello following example.</span></span>

```
git clone https://username:password@bugbashdev4.scm.azure-api.net/
```

<span data-ttu-id="43876-156">Als dit een fout biedt, probeert u URL-codering Hallo wachtwoord gedeelte van Hallo-opdracht.</span><span class="sxs-lookup"><span data-stu-id="43876-156">If this provides an error, try URL encoding hello password portion of hello command.</span></span> <span data-ttu-id="43876-157">Een snelle manier toodo dit tooopen Visual Studio, en geef Hallo de volgende opdracht in Hallo **venster direct**.</span><span class="sxs-lookup"><span data-stu-id="43876-157">One quick way toodo this is tooopen Visual Studio, and issue hello following command in hello **Immediate Window**.</span></span> <span data-ttu-id="43876-158">Hallo tooopen **venster direct**, opent u een oplossing of project in Visual Studio (of maak een nieuwe lege console-toepassing), en kies **Windows**, **Immediate** uit Hallo **Debug** menu.</span><span class="sxs-lookup"><span data-stu-id="43876-158">tooopen hello **Immediate Window**, open any solution or project in Visual Studio (or create a new empty console application), and choose **Windows**, **Immediate** from hello **Debug** menu.</span></span>

```
?System.NetWebUtility.UrlEncode("password from publisher portal")
```

<span data-ttu-id="43876-159">Hallo gecodeerd wachtwoord samen met uw naam en opslagplaats locatie tooconstruct Hallo git opdracht user gebruiken.</span><span class="sxs-lookup"><span data-stu-id="43876-159">Use hello encoded password along with your user name and repository location tooconstruct hello git command.</span></span>

```
git clone https://username:url encoded password@bugbashdev4.scm.azure-api.net/
```

<span data-ttu-id="43876-160">Zodra het Hallo-opslagplaats is gekloond kunt u deze kunt bekijken en bewerken in het lokale bestandssysteem.</span><span class="sxs-lookup"><span data-stu-id="43876-160">Once hello repository is cloned you can view and work with it in your local file system.</span></span> <span data-ttu-id="43876-161">Zie voor meer informatie [structuur verwijzing van lokale Git-opslagplaats, bestanden en mappen](#file-and-folder-structure-reference-of-local-git-repository).</span><span class="sxs-lookup"><span data-stu-id="43876-161">For more information, see [File and folder structure reference of local Git repository](#file-and-folder-structure-reference-of-local-git-repository).</span></span>

## <a name="tooupdate-your-local-repository-with-hello-most-current-service-instance-configuration"></a><span data-ttu-id="43876-162">tooupdate uw lokale opslagplaats met de meest recente configuratie van service-exemplaar Hallo</span><span class="sxs-lookup"><span data-stu-id="43876-162">tooupdate your local repository with hello most current service instance configuration</span></span>
<span data-ttu-id="43876-163">Als u wijzigingen tooyour API Management service-exemplaar in de publicatieportal Hallo of met behulp van Hallo REST-API maakt, moet u deze wijzigingen toohello opslagplaats opslaan voordat u uw lokale opslagplaats met de meest recente wijzigingen Hallo bijwerken kunt.</span><span class="sxs-lookup"><span data-stu-id="43876-163">If you make changes tooyour API Management service instance in hello publisher portal or using hello REST API, you must save these changes toohello repository before you can update your local repository with hello latest changes.</span></span> <span data-ttu-id="43876-164">toodo, klikt u op **opslaan configuratie toorepository** op Hallo **configuratie opslagplaats** tabblad in de publicatieportal hello en vervolgens uitgeeft Hallo volgende opdracht in uw lokale opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="43876-164">toodo this, click **Save configuration toorepository** on hello **Configuration repository** tab in hello publisher portal, and then issue hello following command in your local repository.</span></span>

```
git pull
```

<span data-ttu-id="43876-165">Voordat u `git pull` Zorg ervoor dat u in de map Hallo voor uw lokale opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="43876-165">Before running `git pull` ensure that you are in hello folder for your local repository.</span></span> <span data-ttu-id="43876-166">Als u hebt zojuist Hallo `git clone` opdracht, en vervolgens u Hallo directory tooyour opslagplaats wijzigen moet door het uitvoeren van een opdracht zoals Hallo volgende.</span><span class="sxs-lookup"><span data-stu-id="43876-166">If you have just completed hello `git clone` command, then you must change hello directory tooyour repo by running a command like hello following.</span></span>

```
cd bugbashdev4.scm.azure-api.net/
```

## <a name="toopush-changes-from-your-local-repo-toohello-server-repo"></a><span data-ttu-id="43876-167">toopush wijzigingen uit uw lokale opslagplaats toohello server opslagplaats</span><span class="sxs-lookup"><span data-stu-id="43876-167">toopush changes from your local repo toohello server repo</span></span>
<span data-ttu-id="43876-168">toopush van uw opslagplaats lokale opslagplaats toohello server verandert, moet u uw wijzigingen en push ze toohello server-opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="43876-168">toopush changes from your local repository toohello server repository, you must commit your changes and then push them toohello server repository.</span></span> <span data-ttu-id="43876-169">toocommit uw wijzigingen open uw Git-opdrachthulpprogramma switch toohello directory van uw lokale opslagplaats en probleem Hallo opdrachten te volgen.</span><span class="sxs-lookup"><span data-stu-id="43876-169">toocommit your changes, open your Git command tool, switch toohello directory of your local repository, and issue hello following commands.</span></span>

```
git add --all
git commit -m "Description of your changes"
```

<span data-ttu-id="43876-170">alle Hallo toohello server is, voert doorvoeren toopush Hallo na de opdracht.</span><span class="sxs-lookup"><span data-stu-id="43876-170">toopush all of hello commits toohello server, run hello following command.</span></span>

```
git push
```

## <a name="toodeploy-any-service-configuration-changes-toohello-api-management-service-instance"></a><span data-ttu-id="43876-171">toodeploy eventuele configuratie wijzigingen toohello API Management service-instantie</span><span class="sxs-lookup"><span data-stu-id="43876-171">toodeploy any service configuration changes toohello API Management service instance</span></span>
<span data-ttu-id="43876-172">Wanneer uw lokale wijzigingen doorgevoerd en pushed toohello server-opslagplaats zijn, kunt u ze tooyour API Management service-exemplaar implementeert.</span><span class="sxs-lookup"><span data-stu-id="43876-172">Once your local changes are committed and pushed toohello server repository, you can deploy them tooyour API Management service instance.</span></span>

![Implementeren][api-management-configuration-deploy]

<span data-ttu-id="43876-174">Zie voor informatie over het uitvoeren van deze bewerking met Hallo REST-API, [Git implementeren wijzigingen tooconfiguration-database met de Hallo REST-API](https://docs.microsoft.com/en-us/rest/api/apimanagement/tenantconfiguration).</span><span class="sxs-lookup"><span data-stu-id="43876-174">For information on performing this operation using hello REST API, see [Deploy Git changes tooconfiguration database using hello REST API](https://docs.microsoft.com/en-us/rest/api/apimanagement/tenantconfiguration).</span></span>

## <a name="file-and-folder-structure-reference-of-local-git-repository"></a><span data-ttu-id="43876-175">Verwijzing in de bestanden en mappen de structuur van de lokale Git-opslagplaats</span><span class="sxs-lookup"><span data-stu-id="43876-175">File and folder structure reference of local Git repository</span></span>
<span data-ttu-id="43876-176">Hallo bevatten bestanden en mappen in de lokale git-opslagplaats Hallo Hallo configuratie-informatie over Hallo service-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="43876-176">hello files and folders in hello local git repository contain hello configuration information about hello service instance.</span></span>

| <span data-ttu-id="43876-177">Item</span><span class="sxs-lookup"><span data-stu-id="43876-177">Item</span></span> | <span data-ttu-id="43876-178">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="43876-178">Description</span></span> |
| --- | --- |
| <span data-ttu-id="43876-179">Hoofdmap voor de api-management</span><span class="sxs-lookup"><span data-stu-id="43876-179">root api-management folder</span></span> |<span data-ttu-id="43876-180">Op het hoogste niveau van de configuratie voor service-exemplaar Hallo bevat</span><span class="sxs-lookup"><span data-stu-id="43876-180">Contains top-level configuration for hello service instance</span></span> |
| <span data-ttu-id="43876-181">map van de API 's</span><span class="sxs-lookup"><span data-stu-id="43876-181">apis folder</span></span> |<span data-ttu-id="43876-182">Hallo-configuratie voor Hallo API's bevat in Hallo service-exemplaar</span><span class="sxs-lookup"><span data-stu-id="43876-182">Contains hello configuration for hello apis in hello service instance</span></span> |
| <span data-ttu-id="43876-183">map groepen</span><span class="sxs-lookup"><span data-stu-id="43876-183">groups folder</span></span> |<span data-ttu-id="43876-184">Hallo-configuratie voor Hallo groepen bevat in Hallo service-exemplaar</span><span class="sxs-lookup"><span data-stu-id="43876-184">Contains hello configuration for hello groups in hello service instance</span></span> |
| <span data-ttu-id="43876-185">map beleid</span><span class="sxs-lookup"><span data-stu-id="43876-185">policies folder</span></span> |<span data-ttu-id="43876-186">Bevat Hallo-beleidsregels in Hallo service-exemplaar</span><span class="sxs-lookup"><span data-stu-id="43876-186">Contains hello policies in hello service instance</span></span> |
| <span data-ttu-id="43876-187">portalStyles map</span><span class="sxs-lookup"><span data-stu-id="43876-187">portalStyles folder</span></span> |<span data-ttu-id="43876-188">Hallo-configuratie voor Hallo developer portal aanpassingen bevat in Hallo service-exemplaar</span><span class="sxs-lookup"><span data-stu-id="43876-188">Contains hello configuration for hello developer portal customizations in hello service instance</span></span> |
| <span data-ttu-id="43876-189">map Products</span><span class="sxs-lookup"><span data-stu-id="43876-189">products folder</span></span> |<span data-ttu-id="43876-190">Hallo-configuratie voor Hallo producten bevat in Hallo service-exemplaar</span><span class="sxs-lookup"><span data-stu-id="43876-190">Contains hello configuration for hello products in hello service instance</span></span> |
| <span data-ttu-id="43876-191">sjablonenmap</span><span class="sxs-lookup"><span data-stu-id="43876-191">templates folder</span></span> |<span data-ttu-id="43876-192">Bevat de Hallo-configuratie voor e-mailsjablonen Hallo in Hallo service-exemplaar</span><span class="sxs-lookup"><span data-stu-id="43876-192">Contains hello configuration for hello email templates in hello service instance</span></span> |

<span data-ttu-id="43876-193">Elke map kan een of meer bestanden bevatten en in sommige gevallen een of meer mappen, bijvoorbeeld een map voor elke API, product of groep.</span><span class="sxs-lookup"><span data-stu-id="43876-193">Each folder can contain one or more files, and in some cases one or more folders, for example a folder for each API, product, or group.</span></span> <span data-ttu-id="43876-194">Hallo-bestanden in elke map zijn specifiek voor Hallo entiteitstype beschreven door Hallo mapnaam.</span><span class="sxs-lookup"><span data-stu-id="43876-194">hello files within each folder are specific for hello entity type described by hello folder name.</span></span>

| <span data-ttu-id="43876-195">Bestandstype</span><span class="sxs-lookup"><span data-stu-id="43876-195">File type</span></span> | <span data-ttu-id="43876-196">Doel</span><span class="sxs-lookup"><span data-stu-id="43876-196">Purpose</span></span> |
| --- | --- |
| <span data-ttu-id="43876-197">JSON</span><span class="sxs-lookup"><span data-stu-id="43876-197">json</span></span> |<span data-ttu-id="43876-198">Configuratie-informatie over Hallo respectieve entiteit</span><span class="sxs-lookup"><span data-stu-id="43876-198">Configuration information about hello respective entity</span></span> |
| <span data-ttu-id="43876-199">HTML</span><span class="sxs-lookup"><span data-stu-id="43876-199">html</span></span> |<span data-ttu-id="43876-200">Beschrijvingen over Hallo entiteit, vaak worden weergegeven in het Hallo-portal voor ontwikkelaars</span><span class="sxs-lookup"><span data-stu-id="43876-200">Descriptions about hello entity, often displayed in hello developer portal</span></span> |
| <span data-ttu-id="43876-201">xml</span><span class="sxs-lookup"><span data-stu-id="43876-201">xml</span></span> |<span data-ttu-id="43876-202">Beleidsinstructies</span><span class="sxs-lookup"><span data-stu-id="43876-202">Policy statements</span></span> |
| <span data-ttu-id="43876-203">CSS</span><span class="sxs-lookup"><span data-stu-id="43876-203">css</span></span> |<span data-ttu-id="43876-204">Opmaakmodellen voor developer portal aanpassen</span><span class="sxs-lookup"><span data-stu-id="43876-204">Style sheets for developer portal customization</span></span> |

<span data-ttu-id="43876-205">Deze bestanden kunnen worden gemaakt, verwijderd, bewerkt en beheerd op het lokale bestandssysteem en Hallo wijzigingen geïmplementeerd back toohello uw API Management-service-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="43876-205">These files can be created, deleted, edited, and managed on your local file system, and hello changes deployed back toohello your API Management service instance.</span></span>

> [!NOTE]
> <span data-ttu-id="43876-206">Hallo volgende entiteiten zijn niet opgenomen in de Git-opslagplaats Hallo en kunnen niet worden geconfigureerd met Git.</span><span class="sxs-lookup"><span data-stu-id="43876-206">hello following entities are not contained in hello Git repository and cannot be configured using Git.</span></span>
> 
> * <span data-ttu-id="43876-207">Gebruikers</span><span class="sxs-lookup"><span data-stu-id="43876-207">Users</span></span>
> * <span data-ttu-id="43876-208">Abonnementen</span><span class="sxs-lookup"><span data-stu-id="43876-208">Subscriptions</span></span>
> * <span data-ttu-id="43876-209">Eigenschappen</span><span class="sxs-lookup"><span data-stu-id="43876-209">Properties</span></span>
> * <span data-ttu-id="43876-210">Developer portal entiteiten dan stijlen</span><span class="sxs-lookup"><span data-stu-id="43876-210">Developer portal entities other than styles</span></span>
> 
> 

### <a name="root-api-management-folder"></a><span data-ttu-id="43876-211">Hoofdmap voor de api-management</span><span class="sxs-lookup"><span data-stu-id="43876-211">Root api-management folder</span></span>
<span data-ttu-id="43876-212">Hallo-hoofdmap `api-management` map bevat een `configuration.json` -bestand dat op het hoogste niveau van de informatie over service-exemplaar in de volgende indeling Hallo Hallo bevat.</span><span class="sxs-lookup"><span data-stu-id="43876-212">hello root `api-management` folder contains a `configuration.json` file that contains top-level information about hello service instance in hello following format.</span></span>

```json
{
  "settings": {
    "RegistrationEnabled": "True",
    "UserRegistrationTerms": null,
    "UserRegistrationTermsEnabled": "False",
    "UserRegistrationTermsConsentRequired": "False",
    "DelegationEnabled": "False",
    "DelegationUrl": "",
    "DelegatedSubscriptionEnabled": "False",
    "DelegationValidationKey": ""
  },
  "$ref-policy": "api-management/policies/global.xml"
}
```

<span data-ttu-id="43876-213">instellingen van de eerste vier Hallo (`RegistrationEnabled`, `UserRegistrationTerms`, `UserRegistrationTermsEnabled`, en `UserRegistrationTermsConsentRequired`) toewijzen toohello volgende instellingen op Hallo **identiteiten** tabblad in Hallo **beveiliging** sectie.</span><span class="sxs-lookup"><span data-stu-id="43876-213">hello first four settings (`RegistrationEnabled`, `UserRegistrationTerms`, `UserRegistrationTermsEnabled`, and `UserRegistrationTermsConsentRequired`) map toohello following settings on hello **Identities** tab in hello **Security** section.</span></span>

| <span data-ttu-id="43876-214">Identiteit</span><span class="sxs-lookup"><span data-stu-id="43876-214">Identity setting</span></span> | <span data-ttu-id="43876-215">Te worden toegewezen</span><span class="sxs-lookup"><span data-stu-id="43876-215">Maps too</span></span>|
| --- | --- |
| <span data-ttu-id="43876-216">RegistrationEnabled</span><span class="sxs-lookup"><span data-stu-id="43876-216">RegistrationEnabled</span></span> |<span data-ttu-id="43876-217">**Omleidingspagina anonieme gebruikers toosign in** selectievakje</span><span class="sxs-lookup"><span data-stu-id="43876-217">**Redirect anonymous users toosign-in page** checkbox</span></span> |
| <span data-ttu-id="43876-218">UserRegistrationTerms</span><span class="sxs-lookup"><span data-stu-id="43876-218">UserRegistrationTerms</span></span> |<span data-ttu-id="43876-219">**Gebruiksvoorwaarden op aanmelding gebruiker** tekstvak</span><span class="sxs-lookup"><span data-stu-id="43876-219">**Terms of use on user signup** textbox</span></span> |
| <span data-ttu-id="43876-220">UserRegistrationTermsEnabled</span><span class="sxs-lookup"><span data-stu-id="43876-220">UserRegistrationTermsEnabled</span></span> |<span data-ttu-id="43876-221">**Gebruiksvoorwaarden weergeven op de aanmeldingspagina** selectievakje</span><span class="sxs-lookup"><span data-stu-id="43876-221">**Show terms of use on signup page** checkbox</span></span> |
| <span data-ttu-id="43876-222">UserRegistrationTermsConsentRequired</span><span class="sxs-lookup"><span data-stu-id="43876-222">UserRegistrationTermsConsentRequired</span></span> |<span data-ttu-id="43876-223">**Toestemming vereist** selectievakje</span><span class="sxs-lookup"><span data-stu-id="43876-223">**Require consent** checkbox</span></span> |

![Instellingen van identiteit][api-management-identity-settings]

<span data-ttu-id="43876-225">instellingen van de volgende vier Hallo (`DelegationEnabled`, `DelegationUrl`, `DelegatedSubscriptionEnabled`, en `DelegationValidationKey`) toewijzen toohello volgende instellingen op Hallo **delegering** tabblad in Hallo **beveiliging** sectie.</span><span class="sxs-lookup"><span data-stu-id="43876-225">hello next four settings (`DelegationEnabled`, `DelegationUrl`, `DelegatedSubscriptionEnabled`, and `DelegationValidationKey`) map toohello following settings on hello **Delegation** tab in hello **Security** section.</span></span>

| <span data-ttu-id="43876-226">Delegatie-instelling</span><span class="sxs-lookup"><span data-stu-id="43876-226">Delegation setting</span></span> | <span data-ttu-id="43876-227">Te worden toegewezen</span><span class="sxs-lookup"><span data-stu-id="43876-227">Maps too</span></span>|
| --- | --- |
| <span data-ttu-id="43876-228">DelegationEnabled</span><span class="sxs-lookup"><span data-stu-id="43876-228">DelegationEnabled</span></span> |<span data-ttu-id="43876-229">**Gemachtigde aanmelden & registratie** selectievakje</span><span class="sxs-lookup"><span data-stu-id="43876-229">**Delegate sign-in & sign-up** checkbox</span></span> |
| <span data-ttu-id="43876-230">DelegationUrl</span><span class="sxs-lookup"><span data-stu-id="43876-230">DelegationUrl</span></span> |<span data-ttu-id="43876-231">**De eindpunt-URL voor overdracht** tekstvak</span><span class="sxs-lookup"><span data-stu-id="43876-231">**Delegation endpoint URL** textbox</span></span> |
| <span data-ttu-id="43876-232">DelegatedSubscriptionEnabled</span><span class="sxs-lookup"><span data-stu-id="43876-232">DelegatedSubscriptionEnabled</span></span> |<span data-ttu-id="43876-233">**Product abonnement delegeren** selectievakje</span><span class="sxs-lookup"><span data-stu-id="43876-233">**Delegate product subscription** checkbox</span></span> |
| <span data-ttu-id="43876-234">DelegationValidationKey</span><span class="sxs-lookup"><span data-stu-id="43876-234">DelegationValidationKey</span></span> |<span data-ttu-id="43876-235">**Validatiesleutel delegeren** tekstvak</span><span class="sxs-lookup"><span data-stu-id="43876-235">**Delegate Validation Key** textbox</span></span> |

![Delegatie-instellingen][api-management-delegation-settings]

<span data-ttu-id="43876-237">laatste instelling Hallo `$ref-policy`, toohello algemene instructies beleidsbestand voor Hallo service-exemplaar wordt toegewezen.</span><span class="sxs-lookup"><span data-stu-id="43876-237">hello final setting, `$ref-policy`, maps toohello global policy statements file for hello service instance.</span></span>

### <a name="apis-folder"></a><span data-ttu-id="43876-238">map van de API 's</span><span class="sxs-lookup"><span data-stu-id="43876-238">apis folder</span></span>
<span data-ttu-id="43876-239">Hallo `apis` een map bevat voor elke API in Hallo service-exemplaar waarin de volgende items Hallo.</span><span class="sxs-lookup"><span data-stu-id="43876-239">hello `apis` folder contains a folder for each API in hello service instance which contains hello following items.</span></span>

* <span data-ttu-id="43876-240">`apis\<api name>\configuration.json`-Dit is Hallo-configuratie voor Hallo API en bevat informatie over Hallo back-end voor service-URL en Hallo-bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="43876-240">`apis\<api name>\configuration.json` - this is hello configuration for hello API and contains information about hello backend service URL and hello operations.</span></span> <span data-ttu-id="43876-241">Dit Hallo is dezelfde informatie die wordt geretourneerd als u toocall [ophalen van een specifieke API](https://msdn.microsoft.com/library/azure/dn781423.aspx#GetAPI) met `export=true` in `application/json` indeling.</span><span class="sxs-lookup"><span data-stu-id="43876-241">This is hello same information that would be returned if you were toocall [Get a specific API](https://msdn.microsoft.com/library/azure/dn781423.aspx#GetAPI) with `export=true` in `application/json` format.</span></span>
* <span data-ttu-id="43876-242">`apis\<api name>\api.description.html`-Dit Hallo beschrijving van Hallo API is en overeenkomt met toohello `description` eigenschap Hallo [API entiteit](https://msdn.microsoft.com/library/azure/dn781423.aspx#EntityProperties).</span><span class="sxs-lookup"><span data-stu-id="43876-242">`apis\<api name>\api.description.html` - this is hello description of hello API and corresponds toohello `description` property of hello [API entity](https://msdn.microsoft.com/library/azure/dn781423.aspx#EntityProperties).</span></span>
* <span data-ttu-id="43876-243">`apis\<api name>\operations\`-Deze map bevat `<operation name>.description.html` bestanden die zijn toegewezen toohello bewerkingen in Hallo API.</span><span class="sxs-lookup"><span data-stu-id="43876-243">`apis\<api name>\operations\` - this folder contains `<operation name>.description.html` files that map toohello operations in hello API.</span></span> <span data-ttu-id="43876-244">Elk bestand bevat Hallo beschrijving van één bewerking in Hallo API waarmee toohello toegewezen `description` eigenschap Hallo [bewerking entiteit](https://msdn.microsoft.com/library/azure/dn781423.aspx#OperationProperties) in Hallo REST-API.</span><span class="sxs-lookup"><span data-stu-id="43876-244">Each file contains hello description of a single operation in hello API which maps toohello `description` property of hello [operation entity](https://msdn.microsoft.com/library/azure/dn781423.aspx#OperationProperties) in hello REST API.</span></span>

### <a name="groups-folder"></a><span data-ttu-id="43876-245">map groepen</span><span class="sxs-lookup"><span data-stu-id="43876-245">groups folder</span></span>
<span data-ttu-id="43876-246">Hallo `groups` een map voor elke groep die is gedefinieerd in Hallo service-exemplaar bevat.</span><span class="sxs-lookup"><span data-stu-id="43876-246">hello `groups` folder contains a folder for each group defined in hello service instance.</span></span>

* <span data-ttu-id="43876-247">`groups\<group name>\configuration.json`-Dit is de configuratie Hallo voor Hallo-groep.</span><span class="sxs-lookup"><span data-stu-id="43876-247">`groups\<group name>\configuration.json` - this is hello configuration for hello group.</span></span> <span data-ttu-id="43876-248">Dit Hallo is dezelfde informatie die wordt geretourneerd als u toocall hello [ophalen van een specifieke groep](https://msdn.microsoft.com/library/azure/dn776329.aspx#GetGroup) bewerking.</span><span class="sxs-lookup"><span data-stu-id="43876-248">This is hello same information that would be returned if you were toocall hello [Get a specific group](https://msdn.microsoft.com/library/azure/dn776329.aspx#GetGroup) operation.</span></span>
* <span data-ttu-id="43876-249">`groups\<group name>\description.html`-Dit Hallo beschrijving van Hallo-groep is en overeenkomt met toohello `description` eigenschap Hallo [groep entiteit](https://msdn.microsoft.com/library/azure/dn776329.aspx#EntityProperties).</span><span class="sxs-lookup"><span data-stu-id="43876-249">`groups\<group name>\description.html` - this is hello description of hello group and corresponds toohello `description` property of hello [group entity](https://msdn.microsoft.com/library/azure/dn776329.aspx#EntityProperties).</span></span>

### <a name="policies-folder"></a><span data-ttu-id="43876-250">map beleid</span><span class="sxs-lookup"><span data-stu-id="43876-250">policies folder</span></span>
<span data-ttu-id="43876-251">Hallo `policies` map Hallo beleidsverklaringen voor uw service-exemplaar bevat.</span><span class="sxs-lookup"><span data-stu-id="43876-251">hello `policies` folder contains hello policy statements for your service instance.</span></span>

* <span data-ttu-id="43876-252">`policies\global.xml`-beleid is gedefinieerd op globaal bereik voor uw service-exemplaar bevat.</span><span class="sxs-lookup"><span data-stu-id="43876-252">`policies\global.xml` - contains policies defined at global scope for your service instance.</span></span>
* <span data-ttu-id="43876-253">`policies\apis\<api name>\`-Als er beleid is gedefinieerd op API-scope, zijn opgenomen in deze map.</span><span class="sxs-lookup"><span data-stu-id="43876-253">`policies\apis\<api name>\` - if you have any policies defined at API scope, they are contained in this folder.</span></span>
* <span data-ttu-id="43876-254">`policies\apis\<api name>\<operation name>\`map - als er beleid is gedefinieerd op bewerkingsbereik, zijn opgenomen in deze map in `<operation name>.xml` bestanden die zijn toegewezen toohello beleidsverklaringen voor elke bewerking.</span><span class="sxs-lookup"><span data-stu-id="43876-254">`policies\apis\<api name>\<operation name>\` folder - if you have any policies defined at operation scope, they are contained in this folder in `<operation name>.xml` files that map toohello policy statements for each operation.</span></span>
* <span data-ttu-id="43876-255">`policies\products\`-Als er beleid is gedefinieerd op de product-scope, zijn opgenomen in deze map bevat `<product name>.xml` bestanden die zijn toegewezen toohello beleidsverklaringen voor elk product.</span><span class="sxs-lookup"><span data-stu-id="43876-255">`policies\products\` - if you have any policies defined at product scope, they are contained in this folder, which contains `<product name>.xml` files that map toohello policy statements for each product.</span></span>

### <a name="portalstyles-folder"></a><span data-ttu-id="43876-256">portalStyles map</span><span class="sxs-lookup"><span data-stu-id="43876-256">portalStyles folder</span></span>
<span data-ttu-id="43876-257">Hallo `portalStyles` map bevat configuratie- en opmaakmodellen developer portal aanpassingen voor Hallo service-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="43876-257">hello `portalStyles` folder contains configuration and style sheets for developer portal customizations for hello service instance.</span></span>

* <span data-ttu-id="43876-258">`portalStyles\configuration.json`-Hallo namen bevat van StyleSheets Hallo gebruikt door het Hallo-portal voor ontwikkelaars</span><span class="sxs-lookup"><span data-stu-id="43876-258">`portalStyles\configuration.json` - contains hello names of hello style sheets used by hello developer portal</span></span>
* <span data-ttu-id="43876-259">`portalStyles\<style name>.css`-elke `<style name>.css` bestand bevat stijlen voor Hallo developer-portal (`Preview.css` en `Production.css` standaard).</span><span class="sxs-lookup"><span data-stu-id="43876-259">`portalStyles\<style name>.css` - each `<style name>.css` file contains styles for hello developer portal (`Preview.css` and `Production.css` by default).</span></span>

### <a name="products-folder"></a><span data-ttu-id="43876-260">map Products</span><span class="sxs-lookup"><span data-stu-id="43876-260">products folder</span></span>
<span data-ttu-id="43876-261">Hallo `products` een map voor elk product dat is gedefinieerd in Hallo service-exemplaar bevat.</span><span class="sxs-lookup"><span data-stu-id="43876-261">hello `products` folder contains a folder for each product defined in hello service instance.</span></span>

* <span data-ttu-id="43876-262">`products\<product name>\configuration.json`-Dit is Hallo-configuratie voor het Hallo-product.</span><span class="sxs-lookup"><span data-stu-id="43876-262">`products\<product name>\configuration.json` - this is hello configuration for hello product.</span></span> <span data-ttu-id="43876-263">Dit Hallo is dezelfde informatie die wordt geretourneerd als u toocall hello [ophalen van een specifiek product](https://msdn.microsoft.com/library/azure/dn776336.aspx#GetProduct) bewerking.</span><span class="sxs-lookup"><span data-stu-id="43876-263">This is hello same information that would be returned if you were toocall hello [Get a specific product](https://msdn.microsoft.com/library/azure/dn776336.aspx#GetProduct) operation.</span></span>
* <span data-ttu-id="43876-264">`products\<product name>\product.description.html`-Dit Hallo beschrijving van Hallo product is en overeenkomt met toohello `description` eigenschap Hallo [product entiteit](https://msdn.microsoft.com/library/azure/dn776336.aspx#Product) in Hallo REST-API.</span><span class="sxs-lookup"><span data-stu-id="43876-264">`products\<product name>\product.description.html` - this is hello description of hello product and corresponds toohello `description` property of hello [product entity](https://msdn.microsoft.com/library/azure/dn776336.aspx#Product) in hello REST API.</span></span>

### <a name="templates"></a><span data-ttu-id="43876-265">sjablonen</span><span class="sxs-lookup"><span data-stu-id="43876-265">templates</span></span>
<span data-ttu-id="43876-266">Hallo `templates` map bevat de configuratie voor Hallo [e-mailsjablonen](api-management-howto-configure-notifications.md) van Hallo service-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="43876-266">hello `templates` folder contains configuration for hello [email templates](api-management-howto-configure-notifications.md) of hello service instance.</span></span>

* <span data-ttu-id="43876-267">`<template name>\configuration.json`-Dit is de configuratie Hallo voor Hallo e-mailsjabloon.</span><span class="sxs-lookup"><span data-stu-id="43876-267">`<template name>\configuration.json` - this is hello configuration for hello email template.</span></span>
* <span data-ttu-id="43876-268">`<template name>\body.html`-Dit is de hoofdtekst Hallo van Hallo e-mailsjabloon.</span><span class="sxs-lookup"><span data-stu-id="43876-268">`<template name>\body.html` - this is hello body of hello email template.</span></span>

## <a name="next-steps"></a><span data-ttu-id="43876-269">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="43876-269">Next steps</span></span>
<span data-ttu-id="43876-270">Voor informatie over andere manieren toomanage uw service-exemplaar, Zie:</span><span class="sxs-lookup"><span data-stu-id="43876-270">For information on other ways toomanage your service instance, see:</span></span>

* <span data-ttu-id="43876-271">Uw service-exemplaar met behulp van PowerShell-cmdlets volgen Hallo beheren</span><span class="sxs-lookup"><span data-stu-id="43876-271">Manage your service instance using hello following PowerShell cmdlets</span></span>
  * [<span data-ttu-id="43876-272">Naslaginformatie over PowerShell-cmdlets voor service-implementatie</span><span class="sxs-lookup"><span data-stu-id="43876-272">Service deployment PowerShell cmdlet reference</span></span>](https://msdn.microsoft.com/library/azure/mt619282.aspx)
  * [<span data-ttu-id="43876-273">Service management PowerShell-cmdlet-verwijzing</span><span class="sxs-lookup"><span data-stu-id="43876-273">Service management PowerShell cmdlet reference</span></span>](https://msdn.microsoft.com/library/azure/mt613507.aspx)
* <span data-ttu-id="43876-274">Uw service-exemplaar in de publicatieportal Hallo beheren</span><span class="sxs-lookup"><span data-stu-id="43876-274">Manage your service instance in hello publisher portal</span></span>
  * [<span data-ttu-id="43876-275">Uw eerste API beheren</span><span class="sxs-lookup"><span data-stu-id="43876-275">Manage your first API</span></span>](api-management-get-started.md)
* <span data-ttu-id="43876-276">Beheren van uw service-exemplaar met behulp van Hallo REST-API</span><span class="sxs-lookup"><span data-stu-id="43876-276">Manage your service instance using hello REST API</span></span>
  * [<span data-ttu-id="43876-277">Naslaginformatie over API Management REST API</span><span class="sxs-lookup"><span data-stu-id="43876-277">API Management REST API reference</span></span>](https://msdn.microsoft.com/library/azure/dn776326.aspx)

## <a name="watch-a-video-overview"></a><span data-ttu-id="43876-278">Bekijk een video-overzicht</span><span class="sxs-lookup"><span data-stu-id="43876-278">Watch a video overview</span></span>
> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Configuration-over-Git/player]
> 
> 

[api-management-enable-git]: ./media/api-management-configuration-repository-git/api-management-enable-git.png
[api-management-git-enabled]: ./media/api-management-configuration-repository-git/api-management-git-enabled.png
[api-management-save-configuration]: ./media/api-management-configuration-repository-git/api-management-save-configuration.png
[api-management-save-configuration-confirm]: ./media/api-management-configuration-repository-git/api-management-save-configuration-confirm.png
[api-management-configuration-status]: ./media/api-management-configuration-repository-git/api-management-configuration-status.png
[api-management-configuration-git-clone]: ./media/api-management-configuration-repository-git/api-management-configuration-git-clone.png
[api-management-generate-password]: ./media/api-management-configuration-repository-git/api-management-generate-password.png
[api-management-password]: ./media/api-management-configuration-repository-git/api-management-password.png
[api-management-git-configure]: ./media/api-management-configuration-repository-git/api-management-git-configure.png
[api-management-configuration-deploy]: ./media/api-management-configuration-repository-git/api-management-configuration-deploy.png
[api-management-identity-settings]: ./media/api-management-configuration-repository-git/api-management-identity-settings.png
[api-management-delegation-settings]: ./media/api-management-configuration-repository-git/api-management-delegation-settings.png
[api-management-git-icon-enable]: ./media/api-management-configuration-repository-git/api-management-git-icon-enable.png





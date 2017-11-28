---
title: Configureer uw API Management-service met Git - Azure | Microsoft Docs
description: Informatie over het opslaan en het configureren van de configuratie van uw API Management-service met Git.
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
ms.openlocfilehash: f5d6bb7ccbf15424e9940ccda2fac668a2af5a57
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-save-and-configure-your-api-management-service-configuration-using-git"></a><span data-ttu-id="07d98-103">Het opslaan en het configureren van de configuratie van uw API Management-service met Git</span><span class="sxs-lookup"><span data-stu-id="07d98-103">How to save and configure your API Management service configuration using Git</span></span>
> 
> 

<span data-ttu-id="07d98-104">Elk exemplaar van API Management-service houdt een configuratiedatabase die informatie over de configuratie en metagegevens voor het service-exemplaar bevat.</span><span class="sxs-lookup"><span data-stu-id="07d98-104">Each API Management service instance maintains a configuration database that contains information about the configuration and metadata for the service instance.</span></span> <span data-ttu-id="07d98-105">Door een instelling in de publicatieportal te wijzigen, gebruikt een PowerShell-cmdlet of REST API-aanroep, kunnen u wijzigingen aangebracht in het service-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="07d98-105">Changes can be made to the service instance by changing a setting in the publisher portal, using a PowerShell cmdlet, or making a REST API call.</span></span> <span data-ttu-id="07d98-106">Naast deze methoden kunt u ook de serviceconfiguratie-exemplaar met behulp van Git, zoals het inschakelen van scenario's voor het beheer van service beheren:</span><span class="sxs-lookup"><span data-stu-id="07d98-106">In addition to these methods, you can also manage your service instance configuration using Git, enabling service management scenarios such as:</span></span>

* <span data-ttu-id="07d98-107">Configuratie versioning - downloaden en opslaan van verschillende versies van de serviceconfiguratie</span><span class="sxs-lookup"><span data-stu-id="07d98-107">Configuration versioning - download and store different versions of your service configuration</span></span>
* <span data-ttu-id="07d98-108">Bulksgewijs configuratiewijzigingen - wijzigingen aanbrengen in meerdere delen van uw serviceconfiguratie in uw lokale opslagplaats en de wijzigingen naar de server integreren met een enkele bewerking</span><span class="sxs-lookup"><span data-stu-id="07d98-108">Bulk configuration changes - make changes to multiple parts of your service configuration in your local repository and integrate the changes back to the server with a single operation</span></span>
* <span data-ttu-id="07d98-109">Werkstroom- en bekend Git toolchain de Git tooling en werkstromen die u al bekend met bent gebruiken</span><span class="sxs-lookup"><span data-stu-id="07d98-109">Familiar Git toolchain and workflow - use the Git tooling and workflows that you are already familiar with</span></span>

<span data-ttu-id="07d98-110">Het volgende diagram toont een overzicht van de verschillende manieren voor het configureren van uw API Management-service-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="07d98-110">The following diagram shows an overview of the different ways to configure your API Management service instance.</span></span>

![GIT configureren][api-management-git-configure]

<span data-ttu-id="07d98-112">Wanneer u wijzigingen aan uw service met behulp van de publicatieportal, PowerShell-cmdlets of de REST-API aanbrengt, u beheert uw service configuration database met de `https://{name}.management.azure-api.net` eindpunt, zoals wordt weergegeven aan de rechterkant van het diagram.</span><span class="sxs-lookup"><span data-stu-id="07d98-112">When you make changes to your service using the publisher portal, PowerShell cmdlets, or the REST API, you are managing your service configuration database using the `https://{name}.management.azure-api.net` endpoint, as shown on the right side of the diagram.</span></span> <span data-ttu-id="07d98-113">Aan de linkerkant van het diagram ziet u hoe u de configuratie van uw service met Git kunt beheren en Git-opslagplaats voor uw service zich bevindt op `https://{name}.scm.azure-api.net`.</span><span class="sxs-lookup"><span data-stu-id="07d98-113">The left side of the diagram illustrates how you can manage your service configuration using Git and Git repository for your service located at `https://{name}.scm.azure-api.net`.</span></span>

<span data-ttu-id="07d98-114">De volgende stappen geven een overzicht van het beheer van uw API Management-service-exemplaar met Git.</span><span class="sxs-lookup"><span data-stu-id="07d98-114">The following steps provide an overview of managing your API Management service instance using Git.</span></span>

1. <span data-ttu-id="07d98-115">Toegang tot de configuratie van Git in uw service</span><span class="sxs-lookup"><span data-stu-id="07d98-115">Access Git configuration in your service</span></span>
2. <span data-ttu-id="07d98-116">Sla de configuratiedatabase voor uw service op de Git-opslagplaats</span><span class="sxs-lookup"><span data-stu-id="07d98-116">Save your service configuration database to your Git repository</span></span>
3. <span data-ttu-id="07d98-117">Kloon de Git-opslagplaats op uw lokale computer</span><span class="sxs-lookup"><span data-stu-id="07d98-117">Clone the Git repo to your local machine</span></span>
4. <span data-ttu-id="07d98-118">Trek de meest recente opslagplaats naar beneden op uw lokale computer en wijzigingen doorvoeren en push terug naar uw opslagplaats</span><span class="sxs-lookup"><span data-stu-id="07d98-118">Pull the latest repo down to your local machine, and commit and push changes back to your repo</span></span>
5. <span data-ttu-id="07d98-119">De wijzigingen van uw opslagplaats implementeren in uw service-configuratiedatabase</span><span class="sxs-lookup"><span data-stu-id="07d98-119">Deploy the changes from your repo into your service configuration database</span></span>

<span data-ttu-id="07d98-120">Dit artikel wordt beschreven hoe u inschakelen en Git gebruiken voor het beheren van de serviceconfiguratie en bevat een verwijzing voor de bestanden en mappen in de Git-opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="07d98-120">This article describes how to enable and use Git to manage your service configuration and provides a reference for the files and folders in the Git repository.</span></span>

## <a name="access-git-configuration-in-your-service"></a><span data-ttu-id="07d98-121">Toegang tot de configuratie van Git in uw service</span><span class="sxs-lookup"><span data-stu-id="07d98-121">Access Git configuration in your service</span></span>
<span data-ttu-id="07d98-122">U kunt snel de status van de Git-configuratie weergeven door het bekijken van de Git-pictogram in de rechterbovenhoek van de publicatieportal.</span><span class="sxs-lookup"><span data-stu-id="07d98-122">You can quickly view the status of your Git configuration by viewing the Git icon in the upper-right corner of the publisher portal.</span></span> <span data-ttu-id="07d98-123">In dit voorbeeld geeft het statusbericht aan dat er niet-opgeslagen wijzigingen aan de opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="07d98-123">In this example, the status message indicates that there are unsaved changes to the repository.</span></span> <span data-ttu-id="07d98-124">Dit komt doordat de configuratiedatabase van API Management-service is nog niet zijn opgeslagen in de opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="07d98-124">This is because the API Management service configuration database has not yet been saved to the repository.</span></span>

![GIT-status][api-management-git-icon-enable]

<span data-ttu-id="07d98-126">Als u wilt weergeven en configureren van uw configuratie-instellingen voor Git, u kunt Klik op het pictogram Git, of klikt u op de **beveiliging** menu en navigeer naar de **configuratie opslagplaats** tabblad.</span><span class="sxs-lookup"><span data-stu-id="07d98-126">To view and configure your Git configuration settings, you can either click the Git icon, or click the **Security** menu and navigate to the **Configuration repository** tab.</span></span>

![GIT inschakelen][api-management-enable-git]

> [!IMPORTANT]
> <span data-ttu-id="07d98-128">Geen geheimen die niet zijn gedefinieerd zoals eigenschappen worden opgeslagen in de opslagplaats en in de geschiedenis totdat u blijven uitschakelen en opnieuw inschakelen Git.</span><span class="sxs-lookup"><span data-stu-id="07d98-128">Any secrets that are not defined as properties will be stored in the repository and will remain in its history until you disable and re-enable Git access.</span></span> <span data-ttu-id="07d98-129">Eigenschappen van bieden een veilige plaats voor het beheren van de constante string-waarden, inclusief geheimen, voor alle configuratie-API en beleidsregels, zodat u niet hoeft op te slaan ze rechtstreeks in uw beleidsverklaringen.</span><span class="sxs-lookup"><span data-stu-id="07d98-129">Properties provide a secure place to manage constant string values, including secrets, across all API configuration and policies, so you don't have to store them directly in your policy statements.</span></span> <span data-ttu-id="07d98-130">Zie voor meer informatie [het gebruik van eigenschappen in Azure API Management-beleidsregels](api-management-howto-properties.md).</span><span class="sxs-lookup"><span data-stu-id="07d98-130">For more information, see [How to use properties in Azure API Management policies](api-management-howto-properties.md).</span></span>
> 
> 

<span data-ttu-id="07d98-131">Zie voor meer informatie over het inschakelen of uitschakelen via de REST-API toegang tot een Git [in- of uitschakelen via de REST-API toegang tot een Git](https://msdn.microsoft.com/library/dn781420.aspx#EnableGit).</span><span class="sxs-lookup"><span data-stu-id="07d98-131">For information on enabling or disabling Git access using the REST API, see [Enable or disable Git access using the REST API](https://msdn.microsoft.com/library/dn781420.aspx#EnableGit).</span></span>

## <a name="to-save-the-service-configuration-to-the-git-repository"></a><span data-ttu-id="07d98-132">Configuratie van de service om op te slaan de Git-opslagplaats</span><span class="sxs-lookup"><span data-stu-id="07d98-132">To save the service configuration to the Git repository</span></span>
<span data-ttu-id="07d98-133">De eerste stap voordat u de opslagplaats klonen is de huidige status van de serviceconfiguratie opslaan in de opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="07d98-133">The first step before cloning the repository is to save the current state of the service configuration to the repository.</span></span> <span data-ttu-id="07d98-134">Klik op **configuratie opslaan naar opslagplaats**.</span><span class="sxs-lookup"><span data-stu-id="07d98-134">Click **Save configuration to repository**.</span></span>

![Configuratie op te slaan][api-management-save-configuration]

<span data-ttu-id="07d98-136">Breng de gewenste wijzigingen in het bevestigingsvenster en klik op **Ok** om op te slaan.</span><span class="sxs-lookup"><span data-stu-id="07d98-136">Make any desired changes on the confirmation screen and click **Ok** to save.</span></span>

![Configuratie op te slaan][api-management-save-configuration-confirm]

<span data-ttu-id="07d98-138">Na enkele ogenblikken de configuratie wordt opgeslagen en de status van de configuratie van de opslagplaats wordt weergegeven, inclusief de datum en tijd van de laatste wijziging in de configuratie en de laatste synchronisatie tussen de configuration-service en de opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="07d98-138">After a few moments the configuration is saved, and the configuration status of the repository is displayed, including the date and time of the last configuration change and the last synchronization between the service configuration and the repository.</span></span>

![Configuratiestatus][api-management-configuration-status]

<span data-ttu-id="07d98-140">Zodra de configuratie is opgeslagen in de opslagplaats, kunnen worden gekloond.</span><span class="sxs-lookup"><span data-stu-id="07d98-140">Once the configuration is saved to the repository, it can be cloned.</span></span>

<span data-ttu-id="07d98-141">Zie voor informatie over het uitvoeren van deze bewerking met de REST API, [doorvoeren configuratie momentopname over met de REST-API](https://msdn.microsoft.com/library/dn781420.aspx#CommitSnapshot).</span><span class="sxs-lookup"><span data-stu-id="07d98-141">For information on performing this operation using the REST API, see [Commit configuration snapshot using the REST API](https://msdn.microsoft.com/library/dn781420.aspx#CommitSnapshot).</span></span>

## <a name="to-clone-the-repository-to-your-local-machine"></a><span data-ttu-id="07d98-142">Voor het klonen van de opslagplaats op uw lokale computer</span><span class="sxs-lookup"><span data-stu-id="07d98-142">To clone the repository to your local machine</span></span>
<span data-ttu-id="07d98-143">Als u wilt een opslagplaats klonen, moet u de URL van uw opslagplaats, een gebruikersnaam en een wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="07d98-143">To clone a repository, you need the URL to your repository, a user name, and a password.</span></span> <span data-ttu-id="07d98-144">De gebruikersnaam en een URL worden weergegeven aan de bovenkant van de **configuratie opslagplaats** tabblad.</span><span class="sxs-lookup"><span data-stu-id="07d98-144">The user name and URL are displayed near the top of the **Configuration repository** tab.</span></span>

![GIT kloon][api-management-configuration-git-clone]

<span data-ttu-id="07d98-146">Het wachtwoord is gegenereerd aan de onderkant van de **configuratie opslagplaats** tabblad.</span><span class="sxs-lookup"><span data-stu-id="07d98-146">The password is generated at the bottom of the **Configuration repository** tab.</span></span>

![Wachtwoord genereren][api-management-generate-password]

<span data-ttu-id="07d98-148">Als een wachtwoord worden gegenereerd, eerst voor zorgen dat de **verstrijken** is ingesteld op de gewenste vervaldatum en -tijd en klik vervolgens op **Token genereren**.</span><span class="sxs-lookup"><span data-stu-id="07d98-148">To generate a password, first ensure that the **Expiry** is set to the desired expiration date and time, and then click **Generate Token**.</span></span>

![Wachtwoord][api-management-password]

> [!IMPORTANT]
> <span data-ttu-id="07d98-150">Noteer dit wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="07d98-150">Make a note of this password.</span></span> <span data-ttu-id="07d98-151">Zodra u deze pagina verlaat het wachtwoord niet opnieuw weergegeven.</span><span class="sxs-lookup"><span data-stu-id="07d98-151">Once you leave this page the password will not be displayed again.</span></span>
> 
> 

<span data-ttu-id="07d98-152">De volgende voorbeelden gebruikt het hulpprogramma Git Bash van [Git voor Windows](http://www.git-scm.com/downloads) , maar u kunt een Git-hulpmiddel dat u bekend met bent.</span><span class="sxs-lookup"><span data-stu-id="07d98-152">The following examples use the Git Bash tool from [Git for Windows](http://www.git-scm.com/downloads) but you can use any Git tool that you are familiar with.</span></span>

<span data-ttu-id="07d98-153">Open uw Git-hulpprogramma in de gewenste map en voer de volgende opdracht voor het klonen van de git-opslagplaats op uw lokale computer, met de opdracht die is geleverd door de publicatieportal.</span><span class="sxs-lookup"><span data-stu-id="07d98-153">Open your Git tool in the desired folder and run the following command to clone the git repository to your local machine, using the command provided by the publisher portal.</span></span>

```
git clone https://bugbashdev4.scm.azure-api.net/
```

<span data-ttu-id="07d98-154">Geef de gebruikersnaam en wachtwoord wanneer u wordt gevraagd.</span><span class="sxs-lookup"><span data-stu-id="07d98-154">Provide the user name and password when prompted.</span></span>

<span data-ttu-id="07d98-155">Als u eventuele fouten ontvangt, probeert u het wijzigen van uw `git clone` opdracht om op te nemen van de gebruikersnaam en wachtwoord, zoals wordt weergegeven in het volgende voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="07d98-155">If you receive any errors, try modifying your `git clone` command to include the user name and password, as shown in the following example.</span></span>

```
git clone https://username:password@bugbashdev4.scm.azure-api.net/
```

<span data-ttu-id="07d98-156">Als dit een fout biedt, kunt u URL-codering van het gedeelte van het wachtwoord van de opdracht.</span><span class="sxs-lookup"><span data-stu-id="07d98-156">If this provides an error, try URL encoding the password portion of the command.</span></span> <span data-ttu-id="07d98-157">Een snelle manier om dit te doen is Visual Studio openen, en voert u de volgende opdracht in de **venster direct**.</span><span class="sxs-lookup"><span data-stu-id="07d98-157">One quick way to do this is to open Visual Studio, and issue the following command in the **Immediate Window**.</span></span> <span data-ttu-id="07d98-158">Openen van de **venster direct**, opent u een oplossing of project in Visual Studio (of maak een nieuwe lege console-toepassing), en kies **Windows**, **direct** van de **fouten opsporen in** menu.</span><span class="sxs-lookup"><span data-stu-id="07d98-158">To open the **Immediate Window**, open any solution or project in Visual Studio (or create a new empty console application), and choose **Windows**, **Immediate** from the **Debug** menu.</span></span>

```
?System.NetWebUtility.UrlEncode("password from publisher portal")
```

<span data-ttu-id="07d98-159">Gebruik het gecodeerde wachtwoord samen met de naam en opslagplaats locatie om samen te stellen de git-opdracht.</span><span class="sxs-lookup"><span data-stu-id="07d98-159">Use the encoded password along with your user name and repository location to construct the git command.</span></span>

```
git clone https://username:url encoded password@bugbashdev4.scm.azure-api.net/
```

<span data-ttu-id="07d98-160">Zodra de opslagplaats wordt gekloond kunt u deze kunt bekijken en bewerken in het lokale bestandssysteem.</span><span class="sxs-lookup"><span data-stu-id="07d98-160">Once the repository is cloned you can view and work with it in your local file system.</span></span> <span data-ttu-id="07d98-161">Zie voor meer informatie [structuur verwijzing van lokale Git-opslagplaats, bestanden en mappen](#file-and-folder-structure-reference-of-local-git-repository).</span><span class="sxs-lookup"><span data-stu-id="07d98-161">For more information, see [File and folder structure reference of local Git repository](#file-and-folder-structure-reference-of-local-git-repository).</span></span>

## <a name="to-update-your-local-repository-with-the-most-current-service-instance-configuration"></a><span data-ttu-id="07d98-162">Bijwerken van uw lokale opslagplaats met de meest recente configuratie van de service-exemplaar</span><span class="sxs-lookup"><span data-stu-id="07d98-162">To update your local repository with the most current service instance configuration</span></span>
<span data-ttu-id="07d98-163">Als u wijzigingen in uw API Management-service-exemplaar in de publicatieportal aanbrengen of met de REST API, moet u deze wijzigingen opslaan in de opslagplaats voordat u uw lokale opslagplaats met de meest recente wijzigingen bijwerken kunt.</span><span class="sxs-lookup"><span data-stu-id="07d98-163">If you make changes to your API Management service instance in the publisher portal or using the REST API, you must save these changes to the repository before you can update your local repository with the latest changes.</span></span> <span data-ttu-id="07d98-164">Om dit te doen, klikt u op **configuratie opslaan naar opslagplaats** op de **configuratie opslagplaats** tabblad in de publicatieportal en voert u de volgende opdracht in uw lokale opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="07d98-164">To do this, click **Save configuration to repository** on the **Configuration repository** tab in the publisher portal, and then issue the following command in your local repository.</span></span>

```
git pull
```

<span data-ttu-id="07d98-165">Voordat u `git pull` Zorg ervoor dat u in de map voor uw lokale opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="07d98-165">Before running `git pull` ensure that you are in the folder for your local repository.</span></span> <span data-ttu-id="07d98-166">Als u hebt zojuist de `git clone` opdracht, en vervolgens moet u de map op uw opslagplaats door een opdracht als volgt uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="07d98-166">If you have just completed the `git clone` command, then you must change the directory to your repo by running a command like the following.</span></span>

```
cd bugbashdev4.scm.azure-api.net/
```

## <a name="to-push-changes-from-your-local-repo-to-the-server-repo"></a><span data-ttu-id="07d98-167">Naar wijzigingen uit uw lokale opslagplaats naar de server-opslagplaats forceren</span><span class="sxs-lookup"><span data-stu-id="07d98-167">To push changes from your local repo to the server repo</span></span>
<span data-ttu-id="07d98-168">Voor het wijzigingen van uw lokale opslagplaats pushen naar de opslagplaats van de server, moet u uw wijzigingen en vervolgens toepassen op de server-opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="07d98-168">To push changes from your local repository to the server repository, you must commit your changes and then push them to the server repository.</span></span> <span data-ttu-id="07d98-169">Open uw opdracht Git hulpprogramma, overschakelen naar de map van uw lokale opslagplaats en uitgeven van de volgende opdrachten om uw wijzigingen.</span><span class="sxs-lookup"><span data-stu-id="07d98-169">To commit your changes, open your Git command tool, switch to the directory of your local repository, and issue the following commands.</span></span>

```
git add --all
git commit -m "Description of your changes"
```

<span data-ttu-id="07d98-170">Voor het pushen alle van de doorvoeracties naar de server, moet u de volgende opdracht uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="07d98-170">To push all of the commits to the server, run the following command.</span></span>

```
git push
```

## <a name="to-deploy-any-service-configuration-changes-to-the-api-management-service-instance"></a><span data-ttu-id="07d98-171">Eventuele wijzigingen in de serviceconfiguratie implementeren op service-exemplaar van API Management</span><span class="sxs-lookup"><span data-stu-id="07d98-171">To deploy any service configuration changes to the API Management service instance</span></span>
<span data-ttu-id="07d98-172">Als uw lokale wijzigingen zijn doorgevoerd en naar de opslagplaats server gepusht, kunt u ze kunt implementeren in uw API Management-service-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="07d98-172">Once your local changes are committed and pushed to the server repository, you can deploy them to your API Management service instance.</span></span>

![Implementeren][api-management-configuration-deploy]

<span data-ttu-id="07d98-174">Zie voor informatie over het uitvoeren van deze bewerking met de REST API, [Git implementeren wijzigingen in de REST-API-configuratiedatabase](https://docs.microsoft.com/en-us/rest/api/apimanagement/tenantconfiguration).</span><span class="sxs-lookup"><span data-stu-id="07d98-174">For information on performing this operation using the REST API, see [Deploy Git changes to configuration database using the REST API](https://docs.microsoft.com/en-us/rest/api/apimanagement/tenantconfiguration).</span></span>

## <a name="file-and-folder-structure-reference-of-local-git-repository"></a><span data-ttu-id="07d98-175">Verwijzing in de bestanden en mappen de structuur van de lokale Git-opslagplaats</span><span class="sxs-lookup"><span data-stu-id="07d98-175">File and folder structure reference of local Git repository</span></span>
<span data-ttu-id="07d98-176">De bestanden en mappen in de lokale git-opslagplaats bevatten de configuratie-informatie over het service-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="07d98-176">The files and folders in the local git repository contain the configuration information about the service instance.</span></span>

| <span data-ttu-id="07d98-177">Item</span><span class="sxs-lookup"><span data-stu-id="07d98-177">Item</span></span> | <span data-ttu-id="07d98-178">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="07d98-178">Description</span></span> |
| --- | --- |
| <span data-ttu-id="07d98-179">Hoofdmap voor de api-management</span><span class="sxs-lookup"><span data-stu-id="07d98-179">root api-management folder</span></span> |<span data-ttu-id="07d98-180">Op het hoogste niveau van de configuratie voor de service-exemplaar bevat</span><span class="sxs-lookup"><span data-stu-id="07d98-180">Contains top-level configuration for the service instance</span></span> |
| <span data-ttu-id="07d98-181">map van de API 's</span><span class="sxs-lookup"><span data-stu-id="07d98-181">apis folder</span></span> |<span data-ttu-id="07d98-182">Bevat de configuratie voor de API's in het service-exemplaar</span><span class="sxs-lookup"><span data-stu-id="07d98-182">Contains the configuration for the apis in the service instance</span></span> |
| <span data-ttu-id="07d98-183">map groepen</span><span class="sxs-lookup"><span data-stu-id="07d98-183">groups folder</span></span> |<span data-ttu-id="07d98-184">Bevat de configuratie voor de groepen in het service-exemplaar</span><span class="sxs-lookup"><span data-stu-id="07d98-184">Contains the configuration for the groups in the service instance</span></span> |
| <span data-ttu-id="07d98-185">map beleid</span><span class="sxs-lookup"><span data-stu-id="07d98-185">policies folder</span></span> |<span data-ttu-id="07d98-186">Bevat de beleidsregels in het service-exemplaar</span><span class="sxs-lookup"><span data-stu-id="07d98-186">Contains the policies in the service instance</span></span> |
| <span data-ttu-id="07d98-187">portalStyles map</span><span class="sxs-lookup"><span data-stu-id="07d98-187">portalStyles folder</span></span> |<span data-ttu-id="07d98-188">Bevat de configuratie voor de developer portal aanpassingen in het service-exemplaar</span><span class="sxs-lookup"><span data-stu-id="07d98-188">Contains the configuration for the developer portal customizations in the service instance</span></span> |
| <span data-ttu-id="07d98-189">map Products</span><span class="sxs-lookup"><span data-stu-id="07d98-189">products folder</span></span> |<span data-ttu-id="07d98-190">Bevat de configuratie voor de producten in het service-exemplaar</span><span class="sxs-lookup"><span data-stu-id="07d98-190">Contains the configuration for the products in the service instance</span></span> |
| <span data-ttu-id="07d98-191">sjablonenmap</span><span class="sxs-lookup"><span data-stu-id="07d98-191">templates folder</span></span> |<span data-ttu-id="07d98-192">Bevat de configuratie voor de e-mailsjablonen in het service-exemplaar</span><span class="sxs-lookup"><span data-stu-id="07d98-192">Contains the configuration for the email templates in the service instance</span></span> |

<span data-ttu-id="07d98-193">Elke map kan een of meer bestanden bevatten en in sommige gevallen een of meer mappen, bijvoorbeeld een map voor elke API, product of groep.</span><span class="sxs-lookup"><span data-stu-id="07d98-193">Each folder can contain one or more files, and in some cases one or more folders, for example a folder for each API, product, or group.</span></span> <span data-ttu-id="07d98-194">De bestanden in elke map zijn specifieke voor het entiteitstype beschreven door de naam van de map.</span><span class="sxs-lookup"><span data-stu-id="07d98-194">The files within each folder are specific for the entity type described by the folder name.</span></span>

| <span data-ttu-id="07d98-195">Bestandstype</span><span class="sxs-lookup"><span data-stu-id="07d98-195">File type</span></span> | <span data-ttu-id="07d98-196">Doel</span><span class="sxs-lookup"><span data-stu-id="07d98-196">Purpose</span></span> |
| --- | --- |
| <span data-ttu-id="07d98-197">JSON</span><span class="sxs-lookup"><span data-stu-id="07d98-197">json</span></span> |<span data-ttu-id="07d98-198">Configuratie-informatie over de respectieve entiteit</span><span class="sxs-lookup"><span data-stu-id="07d98-198">Configuration information about the respective entity</span></span> |
| <span data-ttu-id="07d98-199">HTML</span><span class="sxs-lookup"><span data-stu-id="07d98-199">html</span></span> |<span data-ttu-id="07d98-200">Beschrijvingen van de entiteit, vaak worden weergegeven in de portal voor ontwikkelaars</span><span class="sxs-lookup"><span data-stu-id="07d98-200">Descriptions about the entity, often displayed in the developer portal</span></span> |
| <span data-ttu-id="07d98-201">xml</span><span class="sxs-lookup"><span data-stu-id="07d98-201">xml</span></span> |<span data-ttu-id="07d98-202">Beleidsinstructies</span><span class="sxs-lookup"><span data-stu-id="07d98-202">Policy statements</span></span> |
| <span data-ttu-id="07d98-203">CSS</span><span class="sxs-lookup"><span data-stu-id="07d98-203">css</span></span> |<span data-ttu-id="07d98-204">Opmaakmodellen voor developer portal aanpassen</span><span class="sxs-lookup"><span data-stu-id="07d98-204">Style sheets for developer portal customization</span></span> |

<span data-ttu-id="07d98-205">Deze bestanden kunnen worden gemaakt, verwijderd, bewerkt en beheerd op het lokale bestandssysteem en de wijzigingen die zijn geïmplementeerd weer met de uw API Management-service-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="07d98-205">These files can be created, deleted, edited, and managed on your local file system, and the changes deployed back to the your API Management service instance.</span></span>

> [!NOTE]
> <span data-ttu-id="07d98-206">De volgende entiteiten worden niet opgenomen in de Git-opslagplaats en kunnen niet worden geconfigureerd met Git.</span><span class="sxs-lookup"><span data-stu-id="07d98-206">The following entities are not contained in the Git repository and cannot be configured using Git.</span></span>
> 
> * <span data-ttu-id="07d98-207">Gebruikers</span><span class="sxs-lookup"><span data-stu-id="07d98-207">Users</span></span>
> * <span data-ttu-id="07d98-208">Abonnementen</span><span class="sxs-lookup"><span data-stu-id="07d98-208">Subscriptions</span></span>
> * <span data-ttu-id="07d98-209">Eigenschappen</span><span class="sxs-lookup"><span data-stu-id="07d98-209">Properties</span></span>
> * <span data-ttu-id="07d98-210">Developer portal entiteiten dan stijlen</span><span class="sxs-lookup"><span data-stu-id="07d98-210">Developer portal entities other than styles</span></span>
> 
> 

### <a name="root-api-management-folder"></a><span data-ttu-id="07d98-211">Hoofdmap voor de api-management</span><span class="sxs-lookup"><span data-stu-id="07d98-211">Root api-management folder</span></span>
<span data-ttu-id="07d98-212">De hoofdmap `api-management` map bevat een `configuration.json` bestand dat op het hoogste niveau informatie over de service-exemplaar in de volgende indeling bevat.</span><span class="sxs-lookup"><span data-stu-id="07d98-212">The root `api-management` folder contains a `configuration.json` file that contains top-level information about the service instance in the following format.</span></span>

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

<span data-ttu-id="07d98-213">De eerste vier instellingen (`RegistrationEnabled`, `UserRegistrationTerms`, `UserRegistrationTermsEnabled`, en `UserRegistrationTermsConsentRequired`) toewijzen aan de volgende instellingen op de **identiteiten** tabblad de **beveiliging** sectie.</span><span class="sxs-lookup"><span data-stu-id="07d98-213">The first four settings (`RegistrationEnabled`, `UserRegistrationTerms`, `UserRegistrationTermsEnabled`, and `UserRegistrationTermsConsentRequired`) map to the following settings on the **Identities** tab in the **Security** section.</span></span>

| <span data-ttu-id="07d98-214">Identiteit</span><span class="sxs-lookup"><span data-stu-id="07d98-214">Identity setting</span></span> | <span data-ttu-id="07d98-215">Toegewezen aan</span><span class="sxs-lookup"><span data-stu-id="07d98-215">Maps to</span></span> |
| --- | --- |
| <span data-ttu-id="07d98-216">RegistrationEnabled</span><span class="sxs-lookup"><span data-stu-id="07d98-216">RegistrationEnabled</span></span> |<span data-ttu-id="07d98-217">**Anonieme gebruikers omleiden naar de aanmeldingspagina** selectievakje</span><span class="sxs-lookup"><span data-stu-id="07d98-217">**Redirect anonymous users to sign-in page** checkbox</span></span> |
| <span data-ttu-id="07d98-218">UserRegistrationTerms</span><span class="sxs-lookup"><span data-stu-id="07d98-218">UserRegistrationTerms</span></span> |<span data-ttu-id="07d98-219">**Gebruiksvoorwaarden op aanmelding gebruiker** tekstvak</span><span class="sxs-lookup"><span data-stu-id="07d98-219">**Terms of use on user signup** textbox</span></span> |
| <span data-ttu-id="07d98-220">UserRegistrationTermsEnabled</span><span class="sxs-lookup"><span data-stu-id="07d98-220">UserRegistrationTermsEnabled</span></span> |<span data-ttu-id="07d98-221">**Gebruiksvoorwaarden weergeven op de aanmeldingspagina** selectievakje</span><span class="sxs-lookup"><span data-stu-id="07d98-221">**Show terms of use on signup page** checkbox</span></span> |
| <span data-ttu-id="07d98-222">UserRegistrationTermsConsentRequired</span><span class="sxs-lookup"><span data-stu-id="07d98-222">UserRegistrationTermsConsentRequired</span></span> |<span data-ttu-id="07d98-223">**Toestemming vereist** selectievakje</span><span class="sxs-lookup"><span data-stu-id="07d98-223">**Require consent** checkbox</span></span> |

![Instellingen van identiteit][api-management-identity-settings]

<span data-ttu-id="07d98-225">De volgende vier instellingen (`DelegationEnabled`, `DelegationUrl`, `DelegatedSubscriptionEnabled`, en `DelegationValidationKey`) toewijzen aan de volgende instellingen op de **delegering** tabblad de **beveiliging** sectie.</span><span class="sxs-lookup"><span data-stu-id="07d98-225">The next four settings (`DelegationEnabled`, `DelegationUrl`, `DelegatedSubscriptionEnabled`, and `DelegationValidationKey`) map to the following settings on the **Delegation** tab in the **Security** section.</span></span>

| <span data-ttu-id="07d98-226">Delegatie-instelling</span><span class="sxs-lookup"><span data-stu-id="07d98-226">Delegation setting</span></span> | <span data-ttu-id="07d98-227">Toegewezen aan</span><span class="sxs-lookup"><span data-stu-id="07d98-227">Maps to</span></span> |
| --- | --- |
| <span data-ttu-id="07d98-228">DelegationEnabled</span><span class="sxs-lookup"><span data-stu-id="07d98-228">DelegationEnabled</span></span> |<span data-ttu-id="07d98-229">**Gemachtigde aanmelden & registratie** selectievakje</span><span class="sxs-lookup"><span data-stu-id="07d98-229">**Delegate sign-in & sign-up** checkbox</span></span> |
| <span data-ttu-id="07d98-230">DelegationUrl</span><span class="sxs-lookup"><span data-stu-id="07d98-230">DelegationUrl</span></span> |<span data-ttu-id="07d98-231">**De eindpunt-URL voor overdracht** tekstvak</span><span class="sxs-lookup"><span data-stu-id="07d98-231">**Delegation endpoint URL** textbox</span></span> |
| <span data-ttu-id="07d98-232">DelegatedSubscriptionEnabled</span><span class="sxs-lookup"><span data-stu-id="07d98-232">DelegatedSubscriptionEnabled</span></span> |<span data-ttu-id="07d98-233">**Product abonnement delegeren** selectievakje</span><span class="sxs-lookup"><span data-stu-id="07d98-233">**Delegate product subscription** checkbox</span></span> |
| <span data-ttu-id="07d98-234">DelegationValidationKey</span><span class="sxs-lookup"><span data-stu-id="07d98-234">DelegationValidationKey</span></span> |<span data-ttu-id="07d98-235">**Validatiesleutel delegeren** tekstvak</span><span class="sxs-lookup"><span data-stu-id="07d98-235">**Delegate Validation Key** textbox</span></span> |

![Delegatie-instellingen][api-management-delegation-settings]

<span data-ttu-id="07d98-237">De laatste instelling `$ref-policy`, toegewezen aan het bestand globaal beleid instructies voor het service-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="07d98-237">The final setting, `$ref-policy`, maps to the global policy statements file for the service instance.</span></span>

### <a name="apis-folder"></a><span data-ttu-id="07d98-238">map van de API 's</span><span class="sxs-lookup"><span data-stu-id="07d98-238">apis folder</span></span>
<span data-ttu-id="07d98-239">De `apis` een map voor elke API in het service-exemplaar waarin de volgende items bevat.</span><span class="sxs-lookup"><span data-stu-id="07d98-239">The `apis` folder contains a folder for each API in the service instance which contains the following items.</span></span>

* <span data-ttu-id="07d98-240">`apis\<api name>\configuration.json`-Dit is de configuratie voor de API en bevat informatie over de URL van de back-service en de bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="07d98-240">`apis\<api name>\configuration.json` - this is the configuration for the API and contains information about the backend service URL and the operations.</span></span> <span data-ttu-id="07d98-241">Dit is dezelfde informatie die wordt geretourneerd als u aan te roepen [ophalen van een specifieke API](https://msdn.microsoft.com/library/azure/dn781423.aspx#GetAPI) met `export=true` in `application/json` indeling.</span><span class="sxs-lookup"><span data-stu-id="07d98-241">This is the same information that would be returned if you were to call [Get a specific API](https://msdn.microsoft.com/library/azure/dn781423.aspx#GetAPI) with `export=true` in `application/json` format.</span></span>
* <span data-ttu-id="07d98-242">`apis\<api name>\api.description.html`-Dit is de beschrijving van de API en komt overeen met de `description` eigenschap van de [API entiteit](https://msdn.microsoft.com/library/azure/dn781423.aspx#EntityProperties).</span><span class="sxs-lookup"><span data-stu-id="07d98-242">`apis\<api name>\api.description.html` - this is the description of the API and corresponds to the `description` property of the [API entity](https://msdn.microsoft.com/library/azure/dn781423.aspx#EntityProperties).</span></span>
* <span data-ttu-id="07d98-243">`apis\<api name>\operations\`-Deze map bevat `<operation name>.description.html` bestanden die zijn toegewezen aan de bewerkingen in de API.</span><span class="sxs-lookup"><span data-stu-id="07d98-243">`apis\<api name>\operations\` - this folder contains `<operation name>.description.html` files that map to the operations in the API.</span></span> <span data-ttu-id="07d98-244">Elk bestand bevat de beschrijving van één bewerking in de API die wordt toegewezen aan de `description` eigenschap van de [bewerking entiteit](https://msdn.microsoft.com/library/azure/dn781423.aspx#OperationProperties) in de REST-API.</span><span class="sxs-lookup"><span data-stu-id="07d98-244">Each file contains the description of a single operation in the API which maps to the `description` property of the [operation entity](https://msdn.microsoft.com/library/azure/dn781423.aspx#OperationProperties) in the REST API.</span></span>

### <a name="groups-folder"></a><span data-ttu-id="07d98-245">map groepen</span><span class="sxs-lookup"><span data-stu-id="07d98-245">groups folder</span></span>
<span data-ttu-id="07d98-246">De `groups` een map voor elke groep die is gedefinieerd in het service-exemplaar bevat.</span><span class="sxs-lookup"><span data-stu-id="07d98-246">The `groups` folder contains a folder for each group defined in the service instance.</span></span>

* <span data-ttu-id="07d98-247">`groups\<group name>\configuration.json`-Dit is de configuratie voor de groep.</span><span class="sxs-lookup"><span data-stu-id="07d98-247">`groups\<group name>\configuration.json` - this is the configuration for the group.</span></span> <span data-ttu-id="07d98-248">Dit is dezelfde informatie die wordt geretourneerd als u aan te roepen de [ophalen van een specifieke groep](https://msdn.microsoft.com/library/azure/dn776329.aspx#GetGroup) bewerking.</span><span class="sxs-lookup"><span data-stu-id="07d98-248">This is the same information that would be returned if you were to call the [Get a specific group](https://msdn.microsoft.com/library/azure/dn776329.aspx#GetGroup) operation.</span></span>
* <span data-ttu-id="07d98-249">`groups\<group name>\description.html`-Dit is de beschrijving van de groep en komt overeen met de `description` eigenschap van de [groep entiteit](https://msdn.microsoft.com/library/azure/dn776329.aspx#EntityProperties).</span><span class="sxs-lookup"><span data-stu-id="07d98-249">`groups\<group name>\description.html` - this is the description of the group and corresponds to the `description` property of the [group entity](https://msdn.microsoft.com/library/azure/dn776329.aspx#EntityProperties).</span></span>

### <a name="policies-folder"></a><span data-ttu-id="07d98-250">map beleid</span><span class="sxs-lookup"><span data-stu-id="07d98-250">policies folder</span></span>
<span data-ttu-id="07d98-251">De `policies` map bevat de instructies van het beleid voor uw service-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="07d98-251">The `policies` folder contains the policy statements for your service instance.</span></span>

* <span data-ttu-id="07d98-252">`policies\global.xml`-beleid is gedefinieerd op globaal bereik voor uw service-exemplaar bevat.</span><span class="sxs-lookup"><span data-stu-id="07d98-252">`policies\global.xml` - contains policies defined at global scope for your service instance.</span></span>
* <span data-ttu-id="07d98-253">`policies\apis\<api name>\`-Als er beleid is gedefinieerd op API-scope, zijn opgenomen in deze map.</span><span class="sxs-lookup"><span data-stu-id="07d98-253">`policies\apis\<api name>\` - if you have any policies defined at API scope, they are contained in this folder.</span></span>
* <span data-ttu-id="07d98-254">`policies\apis\<api name>\<operation name>\`map - als er beleid is gedefinieerd op bewerkingsbereik, zijn opgenomen in deze map in `<operation name>.xml` bestanden die zijn toegewezen aan de beleidsverklaringen voor elke bewerking.</span><span class="sxs-lookup"><span data-stu-id="07d98-254">`policies\apis\<api name>\<operation name>\` folder - if you have any policies defined at operation scope, they are contained in this folder in `<operation name>.xml` files that map to the policy statements for each operation.</span></span>
* <span data-ttu-id="07d98-255">`policies\products\`-Als er beleid is gedefinieerd op de product-scope, zijn opgenomen in deze map bevat `<product name>.xml` bestanden die zijn toegewezen aan de instructies van het beleid voor elk product.</span><span class="sxs-lookup"><span data-stu-id="07d98-255">`policies\products\` - if you have any policies defined at product scope, they are contained in this folder, which contains `<product name>.xml` files that map to the policy statements for each product.</span></span>

### <a name="portalstyles-folder"></a><span data-ttu-id="07d98-256">portalStyles map</span><span class="sxs-lookup"><span data-stu-id="07d98-256">portalStyles folder</span></span>
<span data-ttu-id="07d98-257">De `portalStyles` map bevat configuratie- en opmaakmodellen developer portal aanpassingen voor service-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="07d98-257">The `portalStyles` folder contains configuration and style sheets for developer portal customizations for the service instance.</span></span>

* <span data-ttu-id="07d98-258">`portalStyles\configuration.json`-de namen bevat van de opmaakmodellen die wordt gebruikt door de portal voor ontwikkelaars</span><span class="sxs-lookup"><span data-stu-id="07d98-258">`portalStyles\configuration.json` - contains the names of the style sheets used by the developer portal</span></span>
* <span data-ttu-id="07d98-259">`portalStyles\<style name>.css`-elke `<style name>.css` bestand bevat stijlen voor de portal voor ontwikkelaars (`Preview.css` en `Production.css` standaard).</span><span class="sxs-lookup"><span data-stu-id="07d98-259">`portalStyles\<style name>.css` - each `<style name>.css` file contains styles for the developer portal (`Preview.css` and `Production.css` by default).</span></span>

### <a name="products-folder"></a><span data-ttu-id="07d98-260">map Products</span><span class="sxs-lookup"><span data-stu-id="07d98-260">products folder</span></span>
<span data-ttu-id="07d98-261">De `products` een map voor elk product dat is gedefinieerd in het service-exemplaar bevat.</span><span class="sxs-lookup"><span data-stu-id="07d98-261">The `products` folder contains a folder for each product defined in the service instance.</span></span>

* <span data-ttu-id="07d98-262">`products\<product name>\configuration.json`-Dit is de configuratie voor het product.</span><span class="sxs-lookup"><span data-stu-id="07d98-262">`products\<product name>\configuration.json` - this is the configuration for the product.</span></span> <span data-ttu-id="07d98-263">Dit is dezelfde informatie die wordt geretourneerd als u aan te roepen de [ophalen van een specifiek product](https://msdn.microsoft.com/library/azure/dn776336.aspx#GetProduct) bewerking.</span><span class="sxs-lookup"><span data-stu-id="07d98-263">This is the same information that would be returned if you were to call the [Get a specific product](https://msdn.microsoft.com/library/azure/dn776336.aspx#GetProduct) operation.</span></span>
* <span data-ttu-id="07d98-264">`products\<product name>\product.description.html`-Dit is de beschrijving van het product en komt overeen met de `description` eigenschap van de [product entiteit](https://msdn.microsoft.com/library/azure/dn776336.aspx#Product) in de REST-API.</span><span class="sxs-lookup"><span data-stu-id="07d98-264">`products\<product name>\product.description.html` - this is the description of the product and corresponds to the `description` property of the [product entity](https://msdn.microsoft.com/library/azure/dn776336.aspx#Product) in the REST API.</span></span>

### <a name="templates"></a><span data-ttu-id="07d98-265">sjablonen</span><span class="sxs-lookup"><span data-stu-id="07d98-265">templates</span></span>
<span data-ttu-id="07d98-266">De `templates` map bevat de configuratie voor de [e-mailsjablonen](api-management-howto-configure-notifications.md) van het service-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="07d98-266">The `templates` folder contains configuration for the [email templates](api-management-howto-configure-notifications.md) of the service instance.</span></span>

* <span data-ttu-id="07d98-267">`<template name>\configuration.json`-Dit is de configuratie voor de e-mailsjabloon.</span><span class="sxs-lookup"><span data-stu-id="07d98-267">`<template name>\configuration.json` - this is the configuration for the email template.</span></span>
* <span data-ttu-id="07d98-268">`<template name>\body.html`-Dit is de hoofdtekst van het e-mailsjabloon.</span><span class="sxs-lookup"><span data-stu-id="07d98-268">`<template name>\body.html` - this is the body of the email template.</span></span>

## <a name="next-steps"></a><span data-ttu-id="07d98-269">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="07d98-269">Next steps</span></span>
<span data-ttu-id="07d98-270">Zie voor informatie over andere manieren voor het beheren van uw service-exemplaar:</span><span class="sxs-lookup"><span data-stu-id="07d98-270">For information on other ways to manage your service instance, see:</span></span>

* <span data-ttu-id="07d98-271">Beheren van uw service-exemplaar met de volgende PowerShell-cmdlets</span><span class="sxs-lookup"><span data-stu-id="07d98-271">Manage your service instance using the following PowerShell cmdlets</span></span>
  * [<span data-ttu-id="07d98-272">Naslaginformatie over PowerShell-cmdlets voor service-implementatie</span><span class="sxs-lookup"><span data-stu-id="07d98-272">Service deployment PowerShell cmdlet reference</span></span>](https://msdn.microsoft.com/library/azure/mt619282.aspx)
  * [<span data-ttu-id="07d98-273">Service management PowerShell-cmdlet-verwijzing</span><span class="sxs-lookup"><span data-stu-id="07d98-273">Service management PowerShell cmdlet reference</span></span>](https://msdn.microsoft.com/library/azure/mt613507.aspx)
* <span data-ttu-id="07d98-274">Beheren van uw service-exemplaar in de publicatieportal</span><span class="sxs-lookup"><span data-stu-id="07d98-274">Manage your service instance in the publisher portal</span></span>
  * [<span data-ttu-id="07d98-275">Uw eerste API beheren</span><span class="sxs-lookup"><span data-stu-id="07d98-275">Manage your first API</span></span>](api-management-get-started.md)
* <span data-ttu-id="07d98-276">Beheren van uw service-exemplaar met de REST API</span><span class="sxs-lookup"><span data-stu-id="07d98-276">Manage your service instance using the REST API</span></span>
  * [<span data-ttu-id="07d98-277">Naslaginformatie over API Management REST API</span><span class="sxs-lookup"><span data-stu-id="07d98-277">API Management REST API reference</span></span>](https://msdn.microsoft.com/library/azure/dn776326.aspx)

## <a name="watch-a-video-overview"></a><span data-ttu-id="07d98-278">Bekijk een video-overzicht</span><span class="sxs-lookup"><span data-stu-id="07d98-278">Watch a video overview</span></span>
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





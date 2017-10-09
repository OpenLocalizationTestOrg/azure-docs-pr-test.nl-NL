---
title: gebruik van aaaImplement disaster recovery back-up en herstel in Azure API Management | Microsoft Docs
description: Meer informatie over hoe toouse back-up en noodherstel tooperform in Azure API Management te herstellen.
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 6f10be3c-f796-4a6c-bacd-7931b6aa82af
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: 058bfb579e3a3f51fb1dac8ea37eb4fdbc83a4ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooimplement-disaster-recovery-using-service-backup-and-restore-in-azure-api-management"></a><span data-ttu-id="ca3f9-103">Hoe gebruik van tooimplement disaster recovery service back-up en herstellen in Azure API Management</span><span class="sxs-lookup"><span data-stu-id="ca3f9-103">How tooimplement disaster recovery using service backup and restore in Azure API Management</span></span>
<span data-ttu-id="ca3f9-104">Door toopublish kiezen en beheren van uw API's via Azure API Management u van veel fout tolerantie en infrastructuur mogelijkheden die hebt u anders toodesign profiteert, implementeren en beheren.</span><span class="sxs-lookup"><span data-stu-id="ca3f9-104">By choosing toopublish and manage your APIs via Azure API Management you are taking advantage of many fault tolerance and infrastructure capabilities that you would otherwise have toodesign, implement, and manage.</span></span> <span data-ttu-id="ca3f9-105">Hello Azure-platform vermindert een groot deel van mogelijke fouten in een fractie van Hallo kosten.</span><span class="sxs-lookup"><span data-stu-id="ca3f9-105">hello Azure platform mitigates a large fraction of potential failures at a fraction of hello cost.</span></span>

<span data-ttu-id="ca3f9-106">toorecover van beschikbaarheidsproblemen bij het Hallo-regio waar uw API Management-service is gehost u moet op elk gewenst moment op gereed tooreconstitute uw service in een andere regio zijn.</span><span class="sxs-lookup"><span data-stu-id="ca3f9-106">toorecover from availability problems affecting hello region where your API Management service is hosted you should be ready tooreconstitute your service in a different region at any time.</span></span> <span data-ttu-id="ca3f9-107">Afhankelijk van uw doelstellingen van de beschikbaarheid en de beoogde hersteltijd mogelijk u wilt dat tooreserve een Backup-service in een of meer regio's en probeer het toomaintain hun configuratie en -inhoud gesynchroniseerd met de Hallo actieve service.</span><span class="sxs-lookup"><span data-stu-id="ca3f9-107">Depending on your availability goals and recovery time objective  you might want tooreserve a backup service in one or more regions and try toomaintain their configuration and content in sync with hello active service.</span></span> <span data-ttu-id="ca3f9-108">Hallo service back-up en herstelfunctie nodig bouwsteen Hallo biedt voor het implementeren van uw strategie voor noodherstel.</span><span class="sxs-lookup"><span data-stu-id="ca3f9-108">hello service backup and restore feature provides hello necessary building block for implementing your disaster recovery strategy.</span></span>

<span data-ttu-id="ca3f9-109">Deze handleiding wordt getoond hoe tooauthenticate Azure Resource Manager-aanvragen en hoe toobackup en herstellen van uw API Management-service-exemplaren.</span><span class="sxs-lookup"><span data-stu-id="ca3f9-109">This guide shows how tooauthenticate Azure Resource Manager requests, and how toobackup and restore your API Management service instances.</span></span>

> [!NOTE]
> <span data-ttu-id="ca3f9-110">Hallo-proces voor een back-up en herstellen van een API Management-service-exemplaar voor herstel na noodgevallen kan ook worden gebruikt voor het repliceren van exemplaren van API Management-service voor scenario's zoals fasering.</span><span class="sxs-lookup"><span data-stu-id="ca3f9-110">hello process for backing up and restoring an API Management service instance for disaster recovery can also be used for replicating API Management service instances for scenarios such as staging.</span></span>
>
> <span data-ttu-id="ca3f9-111">Houd er rekening mee dat elke back-up na 30 dagen verloopt.</span><span class="sxs-lookup"><span data-stu-id="ca3f9-111">Note that each backup expires after 30 days.</span></span> <span data-ttu-id="ca3f9-112">Als u een back-up toorestore probeert nadat de vervalperiode van Hallo 30 dagen is verlopen, Hallo herstellen mislukt met een `Cannot restore: backup expired` bericht.</span><span class="sxs-lookup"><span data-stu-id="ca3f9-112">If you attempt toorestore a backup after hello 30 day expiration period has expired, hello restore will fail with a `Cannot restore: backup expired` message.</span></span>
>
>

## <a name="authenticating-azure-resource-manager-requests"></a><span data-ttu-id="ca3f9-113">Verificatie van Azure Resource Manager-aanvragen</span><span class="sxs-lookup"><span data-stu-id="ca3f9-113">Authenticating Azure Resource Manager requests</span></span>
> [!IMPORTANT]
> <span data-ttu-id="ca3f9-114">Hallo REST-API voor back-up en herstel gebruikt Azure Resource Manager en heeft een ander verificatiemechanisme dan Hallo REST-API's voor het beheren van uw API Management-entiteiten.</span><span class="sxs-lookup"><span data-stu-id="ca3f9-114">hello REST API for backup and restore uses Azure Resource Manager and has a different authentication mechanism than hello REST APIs for managing your API Management entities.</span></span> <span data-ttu-id="ca3f9-115">Hallo stappen in deze sectie wordt beschreven hoe tooauthenticate Azure Resource Manager-aanvragen.</span><span class="sxs-lookup"><span data-stu-id="ca3f9-115">hello steps in this section describe how tooauthenticate Azure Resource Manager requests.</span></span> <span data-ttu-id="ca3f9-116">Zie voor meer informatie [verificatie van Azure Resource Manager-aanvragen](http://msdn.microsoft.com/library/azure/dn790557.aspx).</span><span class="sxs-lookup"><span data-stu-id="ca3f9-116">For more information, see [Authenticating Azure Resource Manager requests](http://msdn.microsoft.com/library/azure/dn790557.aspx).</span></span>
>
>

<span data-ttu-id="ca3f9-117">Alle Hallo-taken die u doen op resources met behulp van hello Azure Resource Manager moeten worden geverifieerd met Azure Active Directory met Hallo stappen te volgen.</span><span class="sxs-lookup"><span data-stu-id="ca3f9-117">All of hello tasks that you do on resources using hello Azure Resource Manager must be authenticated with Azure Active Directory using hello following steps.</span></span>

* <span data-ttu-id="ca3f9-118">Toevoegen van een toepassing toohello Azure Active Directory-tenant.</span><span class="sxs-lookup"><span data-stu-id="ca3f9-118">Add an application toohello Azure Active Directory tenant.</span></span>
* <span data-ttu-id="ca3f9-119">Stel de machtigingen voor Hallo-toepassing die u hebt toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="ca3f9-119">Set permissions for hello application that you added.</span></span>
* <span data-ttu-id="ca3f9-120">Hallo-token ophalen voor het verifiëren van aanvragen tooAzure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="ca3f9-120">Get hello token for authenticating requests tooAzure Resource Manager.</span></span>

<span data-ttu-id="ca3f9-121">de eerste stap Hallo is toocreate een Azure Active Directory-toepassing.</span><span class="sxs-lookup"><span data-stu-id="ca3f9-121">hello first step is toocreate an Azure Active Directory application.</span></span> <span data-ttu-id="ca3f9-122">Meld u aan bij Hallo [klassieke Azure-Portal](http://manage.windowsazure.com/) met Hallo-abonnement met uw API Management-service-instantie en navigeer toohello **toepassingen** tabblad voor uw standaard Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="ca3f9-122">Log into hello [Azure Classic Portal](http://manage.windowsazure.com/) using hello subscription that contains your API Management service instance and navigate toohello **Applications** tab for your default Azure Active Directory.</span></span>

> [!NOTE]
> <span data-ttu-id="ca3f9-123">Als de standaarddirectory voor hello Azure Active Directory is niet zichtbaar tooyour account, vereist contact op met Hallo beheerder hello Azure-abonnement toogrant Hallo tooyour account met machtigingen.</span><span class="sxs-lookup"><span data-stu-id="ca3f9-123">If hello Azure Active Directory default directory is not visible tooyour account, contact hello administrator of hello Azure subscription toogrant hello required permissions tooyour account.</span></span>

![Azure Active Directory-toepassing maken][api-management-add-aad-application]

<span data-ttu-id="ca3f9-125">Klik op **toevoegen**, **mijn organisatie ontwikkelt toepassing toevoegen**, en kies **Native client-toepassing**.</span><span class="sxs-lookup"><span data-stu-id="ca3f9-125">Click **Add**, **Add an application my organization is developing**, and choose **Native client application**.</span></span> <span data-ttu-id="ca3f9-126">Voer een beschrijvende naam en klik op volgende pijl Hallo.</span><span class="sxs-lookup"><span data-stu-id="ca3f9-126">Enter a descriptive name, and click hello next arrow.</span></span> <span data-ttu-id="ca3f9-127">Geef een tijdelijke aanduiding-URL, zoals `http://resources` voor Hallo **omleidings-URI**, zoals dit een verplicht veld is, maar Hallo-waarde is niet later gebruikt.</span><span class="sxs-lookup"><span data-stu-id="ca3f9-127">Enter a placeholder URL such as `http://resources` for hello **Redirect URI**, as it is a required field, but hello value is not used later.</span></span> <span data-ttu-id="ca3f9-128">Klik op Hallo selectievakje toosave Hallo toepassing.</span><span class="sxs-lookup"><span data-stu-id="ca3f9-128">Click hello check box toosave hello application.</span></span>

<span data-ttu-id="ca3f9-129">Nadat de toepassing hello wordt opgeslagen, klikt u op **configureren**, schuif omlaag toohello **machtigingen tooother toepassingen** sectie en op **toepassing toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="ca3f9-129">Once hello application is saved, click **Configure**, scroll down toohello **permissions tooother applications** section, and click **Add application**.</span></span>

![Machtigingen toevoegen][api-management-aad-permissions-add]

<span data-ttu-id="ca3f9-131">Selecteer **Windows** **Azure Service Management API** en klik op Hallo selectievakje tooadd Hallo toepassing.</span><span class="sxs-lookup"><span data-stu-id="ca3f9-131">Select **Windows** **Azure Service Management API** and click hello checkbox tooadd hello application.</span></span>

![Machtigingen toevoegen][api-management-aad-permissions]

<span data-ttu-id="ca3f9-133">Klik op **gedelegeerde machtigingen** naast Hallo toegevoegde **Windows** **Azure Service Management API** toepassing hello selectievakje voor **Access Azure Service Management (preview)**, en klik op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="ca3f9-133">Click **Delegated Permissions** beside hello newly added **Windows** **Azure Service Management API** application, check hello box for **Access Azure Service Management (preview)**, and click **Save**.</span></span>

![Machtigingen toevoegen][api-management-aad-delegated-permissions]

<span data-ttu-id="ca3f9-135">Eerdere tooinvoking Hallo API's die genereren Hallo back-up en herstel hem, is het nodig tooget een token.</span><span class="sxs-lookup"><span data-stu-id="ca3f9-135">Prior tooinvoking hello APIs that generate hello backup and restore it, it is necessary tooget a token.</span></span> <span data-ttu-id="ca3f9-136">Hallo volgende voorbeeld wordt Hallo [Microsoft.IdentityModel.Clients.ActiveDirectory](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory) nuget-pakket tooretrieve Hallo-token.</span><span class="sxs-lookup"><span data-stu-id="ca3f9-136">hello following example uses hello [Microsoft.IdentityModel.Clients.ActiveDirectory](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory) nuget package tooretrieve hello token.</span></span>

```c#
using Microsoft.IdentityModel.Clients.ActiveDirectory;
using System;

namespace GetTokenResourceManagerRequests
{
    class Program
    {
        static void Main(string[] args)
        {
            var authenticationContext = new AuthenticationContext("https://login.microsoftonline.com/{tenant id}");
            var result = authenticationContext.AcquireToken("https://management.azure.com/", {application id}, new Uri({redirect uri});

            if (result == null) {
                throw new InvalidOperationException("Failed tooobtain hello JWT token");
            }

            Console.WriteLine(result.AccessToken);

            Console.ReadLine();
        }
    }
}
```

<span data-ttu-id="ca3f9-137">Vervang `{tentand id}`, `{application id}`, en `{redirect uri}` met Hallo instructies te volgen.</span><span class="sxs-lookup"><span data-stu-id="ca3f9-137">Replace `{tentand id}`, `{application id}`, and `{redirect uri}` using hello following instructions.</span></span>

<span data-ttu-id="ca3f9-138">Vervang `{tenant id}` met tenant-id Hallo Hallo Azure Active Directory-toepassing die u zojuist hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="ca3f9-138">Replace `{tenant id}` with hello tenant id of hello Azure Active Directory application you just created.</span></span> <span data-ttu-id="ca3f9-139">U kunt toegang krijgen tot Hallo-id door te klikken op **eindpunten weergeven**.</span><span class="sxs-lookup"><span data-stu-id="ca3f9-139">You can access hello id by clicking **View endpoints**.</span></span>

![Eindpunten][api-management-aad-default-directory]

![Eindpunten][api-management-endpoint]

<span data-ttu-id="ca3f9-142">Vervang `{application id}` en `{redirect uri}` met Hallo **Client-Id** en de URL van Hallo Hallo **omleidings-URI's** gedeelte van uw Azure Active Directory-toepassing **configureren**  tabblad.</span><span class="sxs-lookup"><span data-stu-id="ca3f9-142">Replace `{application id}` and `{redirect uri}` using hello **Client Id** and  hello URL from hello **Redirect Uris** section from your Azure Active Directory application's **Configure** tab.</span></span>

![Resources][api-management-aad-resources]

<span data-ttu-id="ca3f9-144">Wanneer het Hallo-waarden zijn opgegeven, weer Hallo codevoorbeeld een token vergelijkbare toohello voorbeeld te volgen.</span><span class="sxs-lookup"><span data-stu-id="ca3f9-144">Once hello values are specified, hello code example should return a token similar toohello following example.</span></span>

![Token][api-management-arm-token]

<span data-ttu-id="ca3f9-146">Stel voordat aanroepen Hallo back-up en herstelbewerkingen die zijn beschreven in de volgende secties Hallo, Hallo autorisatie aanvraag-header voor de REST-aanroep.</span><span class="sxs-lookup"><span data-stu-id="ca3f9-146">Before calling hello backup and restore operations described in hello following sections, set hello authorization request header for your REST call.</span></span>

```c#
request.Headers.Add(HttpRequestHeader.Authorization, "Bearer " + token);
```

## <span data-ttu-id="ca3f9-147"><a name="step1"></a>Back-up van een API Management-service</span><span class="sxs-lookup"><span data-stu-id="ca3f9-147"><a name="step1"> </a>Back up an API Management service</span></span>
<span data-ttu-id="ca3f9-148">tooback van een API Management-service probleem Hallo HTTP-aanvraag te volgen:</span><span class="sxs-lookup"><span data-stu-id="ca3f9-148">tooback up an API Management service issue hello following HTTP request:</span></span>

`POST https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/backup?api-version={api-version}`

<span data-ttu-id="ca3f9-149">Waarbij:</span><span class="sxs-lookup"><span data-stu-id="ca3f9-149">where:</span></span>

* <span data-ttu-id="ca3f9-150">`subscriptionId`-id van het Hallo-abonnement met API Management-service Hallo u toobackup probeert</span><span class="sxs-lookup"><span data-stu-id="ca3f9-150">`subscriptionId` - id of hello subscription containing hello API Management service you are attempting toobackup</span></span>
* <span data-ttu-id="ca3f9-151">`resourceGroupName`-een tekenreeks in de vorm van 'Api - standaard-{service regio}' hello waar `service-region` identificeert hello Azure-regio waar Hallo API Management-service die u probeert toobackup wordt gehost, bijvoorbeeld`North-Central-US`</span><span class="sxs-lookup"><span data-stu-id="ca3f9-151">`resourceGroupName` - a string in hello form of 'Api-Default-{service-region}' where `service-region` identifies hello Azure region where hello API Management service you are trying toobackup is hosted, e.g. `North-Central-US`</span></span>
* <span data-ttu-id="ca3f9-152">`serviceName`-naam Hallo Hallo van een back-up van opgegeven Hallo gelijktijdig met het maken maken van API Management-service</span><span class="sxs-lookup"><span data-stu-id="ca3f9-152">`serviceName` - hello name of hello API Management service you are making a backup of specified at hello time of its creation</span></span>
* <span data-ttu-id="ca3f9-153">`api-version`-vervangen`2014-02-14`</span><span class="sxs-lookup"><span data-stu-id="ca3f9-153">`api-version` - replace  with `2014-02-14`</span></span>

<span data-ttu-id="ca3f9-154">Geef in de hoofdtekst van de Hallo van Hallo aanvraag, Hallo doel-Azure-opslag-accountnaam, toegangssleutel, de naam van de blob-container en back-upnaam:</span><span class="sxs-lookup"><span data-stu-id="ca3f9-154">In hello body of hello request, specify hello target Azure storage account name, access key, blob container name, and backup name:</span></span>

```
'{  
    storageAccount : {storage account name for hello backup},  
    accessKey : {access key for hello account},  
    containerName : {backup container name},  
    backupName : {backup blob name}  
}'
```

<span data-ttu-id="ca3f9-155">Hallo-waarde van Hallo `Content-Type` aanvraagheader te`application/json`.</span><span class="sxs-lookup"><span data-stu-id="ca3f9-155">Set hello value of hello `Content-Type` request header too`application/json`.</span></span>

<span data-ttu-id="ca3f9-156">Back-up is een langdurige bewerking die toocomplete van meerdere minuten kan duren.</span><span class="sxs-lookup"><span data-stu-id="ca3f9-156">Backup is a long running operation that may take multiple minutes toocomplete.</span></span>  <span data-ttu-id="ca3f9-157">Als Hallo-aanvraag voltooid is en Hallo back-upproces is gestart. u ontvangt een `202 Accepted` statuscode van antwoord met een `Location` header.</span><span class="sxs-lookup"><span data-stu-id="ca3f9-157">If hello request was successful and hello backup process was initiated you’ll receive a `202 Accepted` response status code with a `Location` header.</span></span>  <span data-ttu-id="ca3f9-158">Controleer 'GET-aanvragen toohello URL in Hallo `Location` header toofind Hallo status van Hallo-bewerking.</span><span class="sxs-lookup"><span data-stu-id="ca3f9-158">Make 'GET' requests toohello URL in hello `Location` header toofind out hello status of hello operation.</span></span> <span data-ttu-id="ca3f9-159">U blijft tooreceive '202 geaccepteerd' statuscode terwijl Hallo back-up uitgevoerd wordt.</span><span class="sxs-lookup"><span data-stu-id="ca3f9-159">While hello backup is in progress you will continue tooreceive a '202 Accepted' status code.</span></span> <span data-ttu-id="ca3f9-160">Reactiecode `200 OK` geven aan welke Hallo back-upbewerking is voltooid.</span><span class="sxs-lookup"><span data-stu-id="ca3f9-160">A Response code of `200 OK` will indicate successful completion of hello backup operation.</span></span>

<span data-ttu-id="ca3f9-161">Houd er rekening mee Hallo volgen beperkingen bij het maken van een back-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="ca3f9-161">Please note hello following constraints when making a backup request.</span></span>

* <span data-ttu-id="ca3f9-162">**Container** opgegeven in de aanvraagtekst Hallo **moet bestaan**.</span><span class="sxs-lookup"><span data-stu-id="ca3f9-162">**Container** specified in hello request body **must exist**.</span></span>
* <span data-ttu-id="ca3f9-163">Terwijl back-up uitgevoerd u wordt **moet niet proberen deze service management bewerkingen** zoals SKU upgrade of een downgrade, wijziging van de domeinnaam, enzovoort.</span><span class="sxs-lookup"><span data-stu-id="ca3f9-163">While backup is in progress you **should not attempt any service management operations** such as SKU upgrade or downgrade, domain name change, etc.</span></span>
* <span data-ttu-id="ca3f9-164">Herstellen van een **back-up kan worden gegarandeerd alleen voor 30 dagen** sinds het moment Hallo van het maken ervan.</span><span class="sxs-lookup"><span data-stu-id="ca3f9-164">Restore of a **backup is guaranteed only for 30 days** since hello moment of its creation.</span></span>
* <span data-ttu-id="ca3f9-165">**Gebruiksgegevens** gebruikt voor het analytics-Rapporten maken **wordt niet meegeleverd** in Hallo back-up.</span><span class="sxs-lookup"><span data-stu-id="ca3f9-165">**Usage data** used for creating analytics reports **is not included** in hello backup.</span></span> <span data-ttu-id="ca3f9-166">Gebruik [REST-API van Azure API Management] [ Azure API Management REST API] tooperiodically ophalen analytics-Rapporten voor veilig te bewaren.</span><span class="sxs-lookup"><span data-stu-id="ca3f9-166">Use [Azure API Management REST API][Azure API Management REST API] tooperiodically retrieve analytics reports for safekeeping.</span></span>
* <span data-ttu-id="ca3f9-167">Hallo frequentie waarmee u de service back-ups uitvoeren heeft invloed op uw beoogd herstelpunt.</span><span class="sxs-lookup"><span data-stu-id="ca3f9-167">hello frequency with which you perform service backups will affect your recovery point objective.</span></span> <span data-ttu-id="ca3f9-168">toominimize deze geadviseerd de uitvoering van regelmatige back-ups als back-ups op aanvraag uitvoeren nadat u belangrijke wijzigingen tooyour API Management-service.</span><span class="sxs-lookup"><span data-stu-id="ca3f9-168">toominimize it we advise implementing regular backups as well as performing on-demand backups after making important changes tooyour API Management service.</span></span>
* <span data-ttu-id="ca3f9-169">**Wijzigingen** en-klare toohello van serviceconfiguratie (bijvoorbeeld API's, beleid, developer portal vormgeving) tijdens het back-upbewerking wordt uitgevoerd **worden mogelijk niet opgenomen in Hallo back-up en daarom gaan verloren**.</span><span class="sxs-lookup"><span data-stu-id="ca3f9-169">**Changes** made toohello service configuration (e.g. APIs, policies, developer portal appearance) while backup operation is in process **might not be included in hello backup and therefore will be lost**.</span></span>

## <span data-ttu-id="ca3f9-170"><a name="step2"></a>Herstellen van een API Management-service</span><span class="sxs-lookup"><span data-stu-id="ca3f9-170"><a name="step2"> </a>Restore an API Management service</span></span>
<span data-ttu-id="ca3f9-171">toorestore een API Management-service van een eerder gemaakte back-up maken Hallo HTTP-aanvraag te volgen:</span><span class="sxs-lookup"><span data-stu-id="ca3f9-171">toorestore an API Management service from a previously created backup make hello following HTTP request:</span></span>

`POST https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/restore?api-version={api-version}`

<span data-ttu-id="ca3f9-172">Waarbij:</span><span class="sxs-lookup"><span data-stu-id="ca3f9-172">where:</span></span>

* <span data-ttu-id="ca3f9-173">`subscriptionId`-id van het Hallo-abonnement met Hallo herstelt u een back-up in API Management-service</span><span class="sxs-lookup"><span data-stu-id="ca3f9-173">`subscriptionId` - id of hello subscription containing hello API Management service you are restoring a backup into</span></span>
* <span data-ttu-id="ca3f9-174">`resourceGroupName`-een tekenreeks in de vorm van 'Api - standaard-{service regio}' hello waar `service-region` identificeert hello Azure-regio waar Hallo herstelt u een back-up in API Management-service wordt gehost, bijvoorbeeld`North-Central-US`</span><span class="sxs-lookup"><span data-stu-id="ca3f9-174">`resourceGroupName` - a string in hello form of 'Api-Default-{service-region}' where `service-region` identifies hello Azure region where hello API Management service you are restoring a backup into is hosted, e.g. `North-Central-US`</span></span>
* <span data-ttu-id="ca3f9-175">`serviceName`-naam Hallo Hallo API Management-service wordt hersteld in bij Hallo van het maken ervan worden opgegeven</span><span class="sxs-lookup"><span data-stu-id="ca3f9-175">`serviceName` - hello name of hello API Management service being restored into specified at hello time of its creation</span></span>
* <span data-ttu-id="ca3f9-176">`api-version`-vervangen`2014-02-14`</span><span class="sxs-lookup"><span data-stu-id="ca3f9-176">`api-version` - replace  with `2014-02-14`</span></span>

<span data-ttu-id="ca3f9-177">Geef in de hoofdtekst van de Hallo van Hallo aanvraag, Hallo back-upbestand locatie, dat wil zeggen accountnaam van de Azure-opslag, toegangssleutel, de naam van de blob-container en back-upnaam:</span><span class="sxs-lookup"><span data-stu-id="ca3f9-177">In hello body of hello request, specify hello backup file location, i.e. Azure storage account name, access key, blob container name, and backup name:</span></span>

```
'{  
    storageAccount : {storage account name for hello backup},  
    accessKey : {access key for hello account},  
    containerName : {backup container name},  
    backupName : {backup blob name}  
}'
```

<span data-ttu-id="ca3f9-178">Hallo-waarde van Hallo `Content-Type` aanvraagheader te`application/json`.</span><span class="sxs-lookup"><span data-stu-id="ca3f9-178">Set hello value of hello `Content-Type` request header too`application/json`.</span></span>

<span data-ttu-id="ca3f9-179">Terugzetten is een langdurige bewerking die voordat too30 of meer minuten toocomplete duren kan.</span><span class="sxs-lookup"><span data-stu-id="ca3f9-179">Restore is a long running operation that may take up too30 or more minutes toocomplete.</span></span>  <span data-ttu-id="ca3f9-180">Als Hallo-aanvraag voltooid is en herstelproces Hallo is gestart. u ontvangt een `202 Accepted` statuscode van antwoord met een `Location` header.</span><span class="sxs-lookup"><span data-stu-id="ca3f9-180">If hello request was successful and hello restore process was initiated you’ll receive a `202 Accepted` response status code with a `Location` header.</span></span>  <span data-ttu-id="ca3f9-181">Controleer 'GET-aanvragen toohello URL in Hallo `Location` header toofind Hallo status van Hallo-bewerking.</span><span class="sxs-lookup"><span data-stu-id="ca3f9-181">Make 'GET' requests toohello URL in hello `Location` header toofind out hello status of hello operation.</span></span> <span data-ttu-id="ca3f9-182">U blijft tooreceive '202 geaccepteerde' statuscode terwijl Hallo terugzetten uitgevoerd wordt.</span><span class="sxs-lookup"><span data-stu-id="ca3f9-182">While hello restore is in progress you will continue tooreceive '202 Accepted' status code.</span></span> <span data-ttu-id="ca3f9-183">Reactiecode `200 OK` geven aan welke Hallo restore-bewerking is voltooid.</span><span class="sxs-lookup"><span data-stu-id="ca3f9-183">A response code of `200 OK` will indicate successful completion of hello restore operation.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ca3f9-184">**Hallo SKU** van Hallo-service wordt hersteld in **moet overeenkomen met** Hallo SKU Hallo een back-up service wordt hersteld.</span><span class="sxs-lookup"><span data-stu-id="ca3f9-184">**hello SKU** of hello service being restored into **must match** hello SKU of hello backed up service being restored.</span></span>
>
> <span data-ttu-id="ca3f9-185">**Wijzigingen** en-klare toohello van serviceconfiguratie (bijvoorbeeld API's, beleid, developer portal vormgeving) tijdens een herstelbewerking wordt uitgevoerd **kunnen worden overschreven**.</span><span class="sxs-lookup"><span data-stu-id="ca3f9-185">**Changes** made toohello service configuration (e.g. APIs, policies, developer portal appearance) while restore operation is in progress **could be overwritten**.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="ca3f9-186">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="ca3f9-186">Next steps</span></span>
<span data-ttu-id="ca3f9-187">Uitchecken Hallo-blogs van Microsoft voor twee verschillende scenario's van de back-up-/ herstelproces hello te volgen.</span><span class="sxs-lookup"><span data-stu-id="ca3f9-187">Check out hello following Microsoft blogs for two different walkthroughs of hello backup/restore process.</span></span>

* [<span data-ttu-id="ca3f9-188">Azure API Management Accounts repliceren</span><span class="sxs-lookup"><span data-stu-id="ca3f9-188">Replicate Azure API Management Accounts</span></span>](https://www.returngis.net/en/2015/06/replicate-azure-api-management-accounts/)
  * <span data-ttu-id="ca3f9-189">Bedankt dat u tooGisela voor haar bijdrage toothis artikel.</span><span class="sxs-lookup"><span data-stu-id="ca3f9-189">Thank you tooGisela for her contribution toothis article.</span></span>
* [<span data-ttu-id="ca3f9-190">Azure API Management: Een back-Up en herstellen van de configuratie</span><span class="sxs-lookup"><span data-stu-id="ca3f9-190">Azure API Management: Backing Up and Restoring Configuration</span></span>](http://blogs.msdn.com/b/stuartleeks/archive/2015/04/29/azure-api-management-backing-up-and-restoring-configuration.aspx)
  * <span data-ttu-id="ca3f9-191">Hallo benadering gedetailleerde door Stuart komt niet overeen met de officiële richtlijnen hello, maar het is heel interessant.</span><span class="sxs-lookup"><span data-stu-id="ca3f9-191">hello approach detailed by Stuart does not match hello official guidance but it is very interesting.</span></span>

[Backup an API Management service]: #step1
[Restore an API Management service]: #step2


[Azure API Management REST API]: http://msdn.microsoft.com/library/azure/dn781421.aspx

[api-management-add-aad-application]: ./media/api-management-howto-disaster-recovery-backup-restore/api-management-add-aad-application.png

[api-management-aad-permissions]: ./media/api-management-howto-disaster-recovery-backup-restore/api-management-aad-permissions.png
[api-management-aad-permissions-add]: ./media/api-management-howto-disaster-recovery-backup-restore/api-management-aad-permissions-add.png
[api-management-aad-delegated-permissions]: ./media/api-management-howto-disaster-recovery-backup-restore/api-management-aad-delegated-permissions.png
[api-management-aad-default-directory]: ./media/api-management-howto-disaster-recovery-backup-restore/api-management-aad-default-directory.png
[api-management-aad-resources]: ./media/api-management-howto-disaster-recovery-backup-restore/api-management-aad-resources.png
[api-management-arm-token]: ./media/api-management-howto-disaster-recovery-backup-restore/api-management-arm-token.png
[api-management-endpoint]: ./media/api-management-howto-disaster-recovery-backup-restore/api-management-endpoint.png

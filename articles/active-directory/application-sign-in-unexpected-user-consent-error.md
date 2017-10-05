---
title: Onverwachte fout bij het uitvoeren van toestemming voor een toepassing | Microsoft Docs
description: Fouten die tijdens het proces optreden kunnen van een toepassing en wat u kunt doen over ze ermee akkoord dat wordt beschreven
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: fd500fdd4c8642bad96dcf71eebcf1fad461a35f
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="unexpected-error-when-performing-consent-to-an-application"></a><span data-ttu-id="48dcb-103">Onverwachte fout bij het uitvoeren van toestemming voor een toepassing</span><span class="sxs-lookup"><span data-stu-id="48dcb-103">Unexpected error when performing consent to an application</span></span>

<span data-ttu-id="48dcb-104">Dit artikel bevat fouten die kunnen optreden tijdens het proces om een toepassing met.</span><span class="sxs-lookup"><span data-stu-id="48dcb-104">This article discusses errors that can occur during the process of consenting to an application.</span></span> <span data-ttu-id="48dcb-105">Als u problemen met onverwachte toestemming wordt gevraagd dat niet eventuele foutberichten bevatten, Zie [verificatie scenario's voor Azure AD](https://docs.microsoft.com/azure/active-directory/develop/active-directory-authentication-scenarios).</span><span class="sxs-lookup"><span data-stu-id="48dcb-105">If you are Troubleshoot unexpected consent prompts that do not contain any error messages, see [Authentication Scenarios for Azure AD](https://docs.microsoft.com/azure/active-directory/develop/active-directory-authentication-scenarios).</span></span>

<span data-ttu-id="48dcb-106">Veel toepassingen die zijn geïntegreerd met Azure Active Directory vereisen machtigingen voor toegang tot andere bronnen om te werken.</span><span class="sxs-lookup"><span data-stu-id="48dcb-106">Many applications that integrate with Azure Active Directory require permissions to access other resources in order to function.</span></span> <span data-ttu-id="48dcb-107">Wanneer deze resources ook worden geïntegreerd met Azure Active Directory, toegang tot deze is vaak aangevraagd met het gemeenschappelijke kader voor toestemming.</span><span class="sxs-lookup"><span data-stu-id="48dcb-107">When these resources are also integrated with Azure Active Directory, permissions to access them is often requested using the common consent framework.</span></span> 

<span data-ttu-id="48dcb-108">Dit resulteert in een instemmingsprompt wordt weergegeven, die treedt meestal op de eerste keer dat een toepassing wordt gebruikt, maar kan ook optreden op een later gebruik van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="48dcb-108">This results in a consent prompt being displayed, which generally occurs the first time an application is used but can also occur on a subsequent use of the application.</span></span>

<span data-ttu-id="48dcb-109">Bepaalde voorwaarden worden voldaan voor een gebruiker toe te staan de machtigingen die vereist zijn voor een toepassing.</span><span class="sxs-lookup"><span data-stu-id="48dcb-109">Certain conditions must be true for a user to consent to the permissions an application requires.</span></span> <span data-ttu-id="48dcb-110">Als u deze voorwaarden niet wordt voldaan, kunnen er diverse fouten optreden.</span><span class="sxs-lookup"><span data-stu-id="48dcb-110">If these conditions are not met, various errors can occur.</span></span> <span data-ttu-id="48dcb-111">Deze omvatten:</span><span class="sxs-lookup"><span data-stu-id="48dcb-111">These include:</span></span>

## <a name="requesting-not-authorized-permissions-error"></a><span data-ttu-id="48dcb-112">Niet-geautoriseerde Machtigingsfout aanvragen</span><span class="sxs-lookup"><span data-stu-id="48dcb-112">Requesting not authorized permissions error</span></span>
* <span data-ttu-id="48dcb-113">**AADSTS90093:** &lt;clientAppDisplayName&gt; vraagt een of meer machtigingen die u bent niet gemachtigd om u te verlenen.</span><span class="sxs-lookup"><span data-stu-id="48dcb-113">**AADSTS90093:** &lt;clientAppDisplayName&gt; is requesting one or more permissions that you are not authorized to grant.</span></span> <span data-ttu-id="48dcb-114">Neem contact op met een beheerder, die u kunt deze toepassing namens jou toestemming.</span><span class="sxs-lookup"><span data-stu-id="48dcb-114">Contact an administrator, who can consent to this application on your behalf.</span></span>

<span data-ttu-id="48dcb-115">Deze fout treedt op wanneer een gebruiker die geen beheerder van een bedrijf wil gebruik van een toepassing die de machtigingen die alleen een beheerder kan verlenen aanvraagt.</span><span class="sxs-lookup"><span data-stu-id="48dcb-115">This error occurs when a user who is not a company administrator attempts to use an application that is requesting permissions that only an administrator can grant.</span></span> <span data-ttu-id="48dcb-116">Deze fout kan worden opgelost door een beheerder toegang verlenen tot de toepassing namens hun organisatie.</span><span class="sxs-lookup"><span data-stu-id="48dcb-116">This error can be resolved by an administrator granting access to the application on behalf of their organization.</span></span>

## <a name="policy-prevents-granting-permissions-error"></a><span data-ttu-id="48dcb-117">Beleid voorkomt dat machtigingen verlenen fout</span><span class="sxs-lookup"><span data-stu-id="48dcb-117">Policy prevents granting permissions error</span></span>
* <span data-ttu-id="48dcb-118">**AADSTS90093:** beheerder van &lt;tenantDisplayName&gt; heeft een beleid dat u niet verlenen ingesteld &lt;naam van de app&gt; de machtigingen die het aanvraagt.</span><span class="sxs-lookup"><span data-stu-id="48dcb-118">**AADSTS90093:** An administrator of &lt;tenantDisplayName&gt; has set a policy that prevents you from granting &lt;name of app&gt; the permissions it is requesting.</span></span> <span data-ttu-id="48dcb-119">Neem contact op met de beheerder van &lt;tenantDisplayName&gt;, wie machtigingen kunt verlenen voor deze app namens jou.</span><span class="sxs-lookup"><span data-stu-id="48dcb-119">Contact an administrator of &lt;tenantDisplayName&gt;, who can grant permissions to this app on your behalf.</span></span>

<span data-ttu-id="48dcb-120">Deze fout treedt op wanneer de beheerder de mogelijkheid voor gebruikers om toestemming aan toepassingen, uitgeschakeld en vervolgens een gebruiker die geen beheerder probeert te gebruiken van een toepassing die toestemming nodig.</span><span class="sxs-lookup"><span data-stu-id="48dcb-120">This error occurs when a company administrator turns off the ability for users to consent to applications, then a non-administrator user attempts to use an application that requires consent.</span></span> <span data-ttu-id="48dcb-121">Deze fout kan worden opgelost door een beheerder toegang verlenen tot de toepassing namens hun organisatie.</span><span class="sxs-lookup"><span data-stu-id="48dcb-121">This error can be resolved by an administrator granting access to the application on behalf of their organization.</span></span>

## <a name="intermittent-problem-error"></a><span data-ttu-id="48dcb-122">Onregelmatige probleem fout</span><span class="sxs-lookup"><span data-stu-id="48dcb-122">Intermittent problem error</span></span>
* <span data-ttu-id="48dcb-123">**AADSTS90090:** het lijkt erop dat we een onregelmatig probleem opname van de machtigingen die u hebt geprobeerd te verlenen aan aangetroffen &lt;clientAppDisplayName&gt;.</span><span class="sxs-lookup"><span data-stu-id="48dcb-123">**AADSTS90090:** It looks like we encountered an intermittent problem recording the permissions you attempted to grant to &lt;clientAppDisplayName&gt;.</span></span> <span data-ttu-id="48dcb-124">Probeer het later opnieuw.</span><span class="sxs-lookup"><span data-stu-id="48dcb-124">try again later.</span></span>

<span data-ttu-id="48dcb-125">Deze fout geeft aan dat er een probleem onregelmatige service aan de clientzijde is opgetreden.</span><span class="sxs-lookup"><span data-stu-id="48dcb-125">This error indicates that an intermittent service side issue has occurred.</span></span> <span data-ttu-id="48dcb-126">Deze kan worden opgelost door probeert toe te staan de toepassing opnieuw.</span><span class="sxs-lookup"><span data-stu-id="48dcb-126">It can be resolved by attempting to consent to the application again.</span></span>

## <a name="resource-not-available-error"></a><span data-ttu-id="48dcb-127">Resource niet beschikbaar-fout</span><span class="sxs-lookup"><span data-stu-id="48dcb-127">Resource not available error</span></span>
* <span data-ttu-id="48dcb-128">**AADSTS65005:** de app &lt;clientAppDisplayName&gt; aangevraagd machtigingen voor toegang tot een resource &lt;resourceAppDisplayName&gt; die is niet beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="48dcb-128">**AADSTS65005:** The app &lt;clientAppDisplayName&gt; requested permissions to access a resource &lt;resourceAppDisplayName&gt; that is not available.</span></span> 

<span data-ttu-id="48dcb-129">Neem contact op met de ontwikkelaar van toepassingen.</span><span class="sxs-lookup"><span data-stu-id="48dcb-129">Contact the application developer.</span></span>

##  <a name="resource-not-available-in-tenant-error"></a><span data-ttu-id="48dcb-130">De resource is niet beschikbaar in de tenant-fout</span><span class="sxs-lookup"><span data-stu-id="48dcb-130">Resource not available in tenant error</span></span>
* <span data-ttu-id="48dcb-131">**AADSTS65005:** &lt;clientAppDisplayName&gt; toegang tot een bron aanvraagt &lt;resourceAppDisplayName&gt; die is niet beschikbaar in uw organisatie &lt; tenantDisplayName&gt;.</span><span class="sxs-lookup"><span data-stu-id="48dcb-131">**AADSTS65005:** &lt;clientAppDisplayName&gt; is requesting access to a resource &lt;resourceAppDisplayName&gt; that is not available in your organization &lt;tenantDisplayName&gt;.</span></span> 

<span data-ttu-id="48dcb-132">Zorg ervoor dat deze resource beschikbaar is of neem contact op met de beheerder van &lt;tenantDisplayName&gt;.</span><span class="sxs-lookup"><span data-stu-id="48dcb-132">Ensure that this resource is available or contact an administrator of &lt;tenantDisplayName&gt;.</span></span>

## <a name="permissions-mismatch-error"></a><span data-ttu-id="48dcb-133">Fout met niet overeenkomende machtigingen</span><span class="sxs-lookup"><span data-stu-id="48dcb-133">Permissions mismatch error</span></span>
* <span data-ttu-id="48dcb-134">**AADSTS65005:** de app aangevraagd toestemming voor toegang tot resources &lt;resourceAppDisplayName&gt;.</span><span class="sxs-lookup"><span data-stu-id="48dcb-134">**AADSTS65005:** The app requested consent to access resource &lt;resourceAppDisplayName&gt;.</span></span> <span data-ttu-id="48dcb-135">Deze aanvraag is mislukt omdat deze komt niet overeen met hoe de app is vooraf geconfigureerd tijdens de registratie van de app.</span><span class="sxs-lookup"><span data-stu-id="48dcb-135">This request failed because it does not match how the app was pre-configured during app registration.</span></span> <span data-ttu-id="48dcb-136">Neem contact op met de app vendor.* *</span><span class="sxs-lookup"><span data-stu-id="48dcb-136">Contact the app vendor.**</span></span>

<span data-ttu-id="48dcb-137">Deze fouten die alle optreden wanneer de toepassing die een gebruiker probeert toe te staan machtigingen vraagt voor toegang tot een resource-toepassing die niet is gevonden in de map van de organisatie (tenant).</span><span class="sxs-lookup"><span data-stu-id="48dcb-137">These errors all occur when the application a user is trying to consent to is requesting permissions to access a resource application that cannot be found in the organization’s directory (tenant).</span></span> <span data-ttu-id="48dcb-138">Dit kan verschillende redenen optreden:</span><span class="sxs-lookup"><span data-stu-id="48dcb-138">This can occur for several reasons:</span></span>

-   <span data-ttu-id="48dcb-139">De ontwikkelaar van de client-toepassing heeft de toepassing niet goed geconfigureerd, waardoor toegang vragen tot een ongeldige resource.</span><span class="sxs-lookup"><span data-stu-id="48dcb-139">The client application developer has configured their application incorrectly, causing it to request access to an invalid resource.</span></span> <span data-ttu-id="48dcb-140">De ontwikkelaar moet in dit geval wordt de configuratie van de clienttoepassing lost dit probleem bijwerken.</span><span class="sxs-lookup"><span data-stu-id="48dcb-140">In this case, the application developer must update the configuration of the client application to resolve this issue.</span></span>

-   <span data-ttu-id="48dcb-141">Een Service-Principal voor de doeltoepassing resource bestaat niet in de organisatie, of in het verleden bestond maar is verwijderd.</span><span class="sxs-lookup"><span data-stu-id="48dcb-141">A Service Principal representing the target resource application does not exist in the organization, or existed in the past but has been removed.</span></span> <span data-ttu-id="48dcb-142">U lost dit probleem, moet een Service-Principal voor de resource-toepassing in de organisatie worden ingericht zodat de clienttoepassing machtigingen kan aanvragen.</span><span class="sxs-lookup"><span data-stu-id="48dcb-142">To resolve this issue, a Service Principal for the resource application must be provisioned in the organization so the client application can request permissions to it.</span></span> <span data-ttu-id="48dcb-143">Dit kan gebeuren in een aantal manieren, afhankelijk van het type toepassing, met inbegrip van:</span><span class="sxs-lookup"><span data-stu-id="48dcb-143">This can happen in an number of ways, depending on the type of application, including:</span></span>

    -   <span data-ttu-id="48dcb-144">Ophalen van een abonnement voor de resource-toepassing (Microsoft gepubliceerde toepassingen)</span><span class="sxs-lookup"><span data-stu-id="48dcb-144">Acquiring a subscription for the resource application (Microsoft published applications)</span></span>

    -   <span data-ttu-id="48dcb-145">Ermee akkoord dat de resource-toepassing</span><span class="sxs-lookup"><span data-stu-id="48dcb-145">Consenting to the resource application</span></span>

    -   <span data-ttu-id="48dcb-146">Machtigingen van de toepassing via Azure Portal</span><span class="sxs-lookup"><span data-stu-id="48dcb-146">Granting the application permissions via the Azure Portal</span></span>

    -   <span data-ttu-id="48dcb-147">Het toevoegen van de toepassing van de Azure AD-Toepassingsgalerie</span><span class="sxs-lookup"><span data-stu-id="48dcb-147">Adding the application from the Azure AD Application Gallery</span></span>

## <a name="next-steps"></a><span data-ttu-id="48dcb-148">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="48dcb-148">Next steps</span></span> 

[<span data-ttu-id="48dcb-149">Apps, machtigingen en toestemming in Azure Active Directory (v1-eindpunt)</span><span class="sxs-lookup"><span data-stu-id="48dcb-149">Apps, permissions, and consent in Azure Active Directory (v1 endpoint)</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-apps-permissions-consent)<br>

[<span data-ttu-id="48dcb-150">Scopes, machtigingen en toestemming in Azure Active Directory (v2.0-eindpunt)</span><span class="sxs-lookup"><span data-stu-id="48dcb-150">Scopes, permissions, and consent in the Azure Active Directory (v2.0 endpoint)</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes)



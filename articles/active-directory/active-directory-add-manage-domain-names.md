---
title: Aangepaste domeinnamen in uw Azure Active Directory beheren | Microsoft Docs
description: Beheerconcepten en uitleg over het beheren van een aangepast domein in Azure Active Directory
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: cf3523bd-9ee0-439e-963d-ccea038867b9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: curtand
ms.custom: oldportal;it-pro;
robots: NOINDEX
ms.openlocfilehash: 5ae19bb370064de96cf466ca09b13d02563d65a4
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="managing-custom-domain-names-in-your-azure-active-directory"></a><span data-ttu-id="73d52-103">Aangepaste domeinnamen in uw Azure Active Directory beheren</span><span class="sxs-lookup"><span data-stu-id="73d52-103">Managing custom domain names in your Azure Active Directory</span></span>
<span data-ttu-id="73d52-104">Een domeinnaam zijn een belangrijk id voor veel directoryresources als onderdeel van:</span><span class="sxs-lookup"><span data-stu-id="73d52-104">A domain name can be an important identifier for many directory resources, as part of:</span></span>

* <span data-ttu-id="73d52-105">Een gebruikersnaam of e-mailadres voor een gebruiker</span><span class="sxs-lookup"><span data-stu-id="73d52-105">A user name or email address for a user</span></span>
* <span data-ttu-id="73d52-106">Het adres voor een groep</span><span class="sxs-lookup"><span data-stu-id="73d52-106">The address for a group</span></span>
* <span data-ttu-id="73d52-107">De app-ID-URI voor een toepassing</span><span class="sxs-lookup"><span data-stu-id="73d52-107">The app ID URI for an application</span></span>

<span data-ttu-id="73d52-108">Een resource in Azure Active Directory (Azure AD), kan een domeinnaam die al is gecontroleerd en eigendom zijn van de map waarin de resource bevatten.</span><span class="sxs-lookup"><span data-stu-id="73d52-108">A resource in Azure Active Directory (Azure AD) can include a domain name that is already verified to be owned by the directory that contains the resource.</span></span> <span data-ttu-id="73d52-109">Alleen een globale beheerder kunt domein-beheertaken uitvoeren in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="73d52-109">Only a global administrator can perform domain management tasks in Azure AD.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="73d52-110">Microsoft raadt u aan Azure AD te beheren met het [Azure AD-beheercentrum](https://aad.portal.azure.com) in Azure Portal in plaats van de klassieke Azure portal waarnaar in dit artikel wordt verwezen.</span><span class="sxs-lookup"><span data-stu-id="73d52-110">Microsoft recommends that you manage Azure AD using the [Azure AD admin center](https://aad.portal.azure.com) in the Azure portal instead of using the Azure classic portal referenced in this article.</span></span> <span data-ttu-id="73d52-111">Voor informatie over het beheren van uw domeinnamen in de Azure AD-beheercentrum, Zie [aangepaste domeinnamen in uw Azure Active Directory beheren](active-directory-domains-manage-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="73d52-111">For how to manage your domain names in the Azure AD admin center, see [Managing custom domain names in your Azure Active Directory](active-directory-domains-manage-azure-portal.md).</span></span>

## <a name="set-the-primary-domain-name-for-your-azure-ad-directory"></a><span data-ttu-id="73d52-112">De naam van het primaire domein voor uw Azure AD-directory instellen</span><span class="sxs-lookup"><span data-stu-id="73d52-112">Set the primary domain name for your Azure AD directory</span></span>
<span data-ttu-id="73d52-113">Wanneer de map wordt gemaakt, wordt de initiële domeinnaam, zoals 'contoso.onmicrosoft.com', is ook de primaire domeinnaam voor uw directory.</span><span class="sxs-lookup"><span data-stu-id="73d52-113">When your directory is created, the initial domain name, such as ‘contoso.onmicrosoft.com,’ is also the primary domain name for your directory.</span></span> <span data-ttu-id="73d52-114">Het primaire domein is de standaard-domeinnaam voor een nieuwe gebruiker bij het maken van een nieuwe gebruiker in de [klassieke Azure-portal](https://manage.windowsazure.com/), of andere portals zoals Office 365-beheerportal.</span><span class="sxs-lookup"><span data-stu-id="73d52-114">The primary domain is the default domain name for a new user when you create a new user in the [Azure classic portal](https://manage.windowsazure.com/), or other portals such as the Office 365 admin portal.</span></span> <span data-ttu-id="73d52-115">Dit stroomlijnt het proces voor de beheerder nieuwe gebruikers maken in de portal.</span><span class="sxs-lookup"><span data-stu-id="73d52-115">This streamlines the process for an administrator to create new users in the portal.</span></span>

<span data-ttu-id="73d52-116">De naam van de primaire domeincontroller voor uw directory wijzigen:</span><span class="sxs-lookup"><span data-stu-id="73d52-116">To change the primary domain name for your directory:</span></span>

1. <span data-ttu-id="73d52-117">Meld u aan bij de [klassieke Azure Portal](https://manage.windowsazure.com/) met een gebruikersaccount met de rechten voor globale beheerder van uw Azure AD-directory.</span><span class="sxs-lookup"><span data-stu-id="73d52-117">Sign in to the [Azure classic portal](https://manage.windowsazure.com/) with a user account that is a global administrator of your Azure AD directory.</span></span>
2. <span data-ttu-id="73d52-118">Selecteer **Active Directory** op de linkernavigatiebalk.</span><span class="sxs-lookup"><span data-stu-id="73d52-118">Select **Active Directory** on the left navigation bar.</span></span>
3. <span data-ttu-id="73d52-119">Open uw directory.</span><span class="sxs-lookup"><span data-stu-id="73d52-119">Open your directory.</span></span>
4. <span data-ttu-id="73d52-120">Selecteer de **domeinen** tabblad.</span><span class="sxs-lookup"><span data-stu-id="73d52-120">Select the **Domains** tab.</span></span>
5. <span data-ttu-id="73d52-121">Selecteer de **primaire wijziging** knop op de opdrachtbalk.</span><span class="sxs-lookup"><span data-stu-id="73d52-121">Select the **Change primary** button on the command bar.</span></span>
6. <span data-ttu-id="73d52-122">Selecteer het domein dat u wilt worden van het nieuwe primaire domein voor uw directory.</span><span class="sxs-lookup"><span data-stu-id="73d52-122">Select the domain that you want to be the new primary domain for your directory.</span></span>

<span data-ttu-id="73d52-123">U kunt de primaire domeinnaam voor uw directory om te worden geverifieerd aangepaste domeinen die niet federatief wijzigen.</span><span class="sxs-lookup"><span data-stu-id="73d52-123">You can change the primary domain name for your directory to be any verified custom domain that is not federated.</span></span> <span data-ttu-id="73d52-124">Het wijzigen van het primaire domein voor uw directory heeft geen invloed op de gebruikersnamen voor alle bestaande gebruikers.</span><span class="sxs-lookup"><span data-stu-id="73d52-124">Changing the primary domain for your directory will not change the user names for any existing users.</span></span>

## <a name="add-custom-domain-names-to-your-azure-ad"></a><span data-ttu-id="73d52-125">Aangepaste domeinnamen toevoegen aan uw Azure AD</span><span class="sxs-lookup"><span data-stu-id="73d52-125">Add custom domain names to your Azure AD</span></span>
<span data-ttu-id="73d52-126">U kunt maximaal 900 aangepaste domeinnamen toevoegen aan elke Azure AD-directory.</span><span class="sxs-lookup"><span data-stu-id="73d52-126">You can add up to 900 custom domain names to each Azure AD directory.</span></span> <span data-ttu-id="73d52-127">Het proces voor het [een aanvullende aangepaste domeinnaam toevoegen](active-directory-add-domain.md) is hetzelfde voor de eerste aangepaste domeinnaam.</span><span class="sxs-lookup"><span data-stu-id="73d52-127">The process to [add an additional custom domain name](active-directory-add-domain.md) is the same for the first custom domain name.</span></span>

## <a name="add-subdomains-of-a-custom-domain"></a><span data-ttu-id="73d52-128">Toevoegen van subdomeinen van een aangepast domein</span><span class="sxs-lookup"><span data-stu-id="73d52-128">Add subdomains of a custom domain</span></span>
<span data-ttu-id="73d52-129">Als u wilt een derde niveau domeinnaam zoals 'europe.contoso.com' toevoegen aan uw directory, moet u eerst toevoegen en controleren van het domein van de tweede niveau, zoals contoso.com.</span><span class="sxs-lookup"><span data-stu-id="73d52-129">If you want to add a third-level domain name such as ‘europe.contoso.com’ to your directory, you should first add and verify the second-level domain, such as contoso.com.</span></span> <span data-ttu-id="73d52-130">Het subdomein wordt automatisch geverifieerd door Azure AD.</span><span class="sxs-lookup"><span data-stu-id="73d52-130">The subdomain will be automatically verified by Azure AD.</span></span> <span data-ttu-id="73d52-131">Overzicht van het subdomein dat u zojuist hebt toegevoegd is geverifieerd, vernieuw de pagina in de browser met een lijst met de domeinen in uw directory.</span><span class="sxs-lookup"><span data-stu-id="73d52-131">To see that the subdomain that you just added has been verified, refresh the page in the browser that lists the domains in your directory.</span></span>

## <a name="what-to-do-if-you-change-the-dns-registrar-for-your-custom-domain-name"></a><span data-ttu-id="73d52-132">Wat te doen als u de DNS-registratieservice voor uw aangepaste domeinnaam wijzigen</span><span class="sxs-lookup"><span data-stu-id="73d52-132">What to do if you change the DNS registrar for your custom domain name</span></span>
<span data-ttu-id="73d52-133">Als u de DNS-registratieservice voor uw aangepaste domeinnaam wijzigt, kunt u uw aangepaste domeinnaam gebruiken met Azure AD zelf zonder onderbreking en zonder aanvullende configuratietaken blijven.</span><span class="sxs-lookup"><span data-stu-id="73d52-133">If you change the DNS registrar for your custom domain name, you can continue to use your custom domain name with Azure AD itself without interruption and without additional configuration tasks.</span></span> <span data-ttu-id="73d52-134">Als u uw aangepaste domeinnaam met Office 365, Intune of andere services die afhankelijk van aangepaste domeinnamen in Azure AD gebruiken zijn, Raadpleeg de documentatie voor deze services.</span><span class="sxs-lookup"><span data-stu-id="73d52-134">If you use your custom domain name with Office 365, Intune, or other services that rely on custom domain names in Azure AD, refer to the documentation for those services.</span></span>

## <a name="delete-a-custom-domain-name"></a><span data-ttu-id="73d52-135">Verwijderen van een aangepaste domeinnaam</span><span class="sxs-lookup"><span data-stu-id="73d52-135">Delete a custom domain name</span></span>
<span data-ttu-id="73d52-136">Als uw organisatie die domeinnaam niet langer gebruikt, of als u wilt gebruiken die domeinnaam met een andere Azure AD, kunt u een aangepaste domeinnaam van uw Azure AD verwijderen.</span><span class="sxs-lookup"><span data-stu-id="73d52-136">You can delete a custom domain name from your Azure AD if your organization no longer uses that domain name, or if you need to use that domain name with another Azure AD.</span></span>

<span data-ttu-id="73d52-137">Als u wilt verwijderen van een aangepaste domeinnaam, moet u eerst controleren of geen resources in uw directory zijn afhankelijk van de domeinnaam.</span><span class="sxs-lookup"><span data-stu-id="73d52-137">To delete a custom domain name, you must first ensure that no resources in your directory rely on the domain name.</span></span> <span data-ttu-id="73d52-138">U kunt een domeinnaam niet verwijderen uit de map als:</span><span class="sxs-lookup"><span data-stu-id="73d52-138">You can't delete a domain name from your directory if:</span></span>

* <span data-ttu-id="73d52-139">Elke gebruiker heeft een gebruikersnaam, het e-mailadres of de proxy-adres dat de domeinnaam omvatten.</span><span class="sxs-lookup"><span data-stu-id="73d52-139">Any user has a user name, email address, or proxy address that include the domain name.</span></span>
* <span data-ttu-id="73d52-140">Een groep heeft een e-mailadres of de proxy-adres dat de domeinnaam bevat.</span><span class="sxs-lookup"><span data-stu-id="73d52-140">Any group has an email address or proxy address that includes the domain name.</span></span>
* <span data-ttu-id="73d52-141">Elke toepassing in uw Azure AD heeft een app ID URI die de domeinnaam bevat.</span><span class="sxs-lookup"><span data-stu-id="73d52-141">Any application in your Azure AD has an app ID URI that includes the domain name.</span></span>

<span data-ttu-id="73d52-142">U moet wijzigen of verwijderen van een dergelijke resource in uw Azure AD-directory voordat u de aangepaste domeinnaam kunt verwijderen.</span><span class="sxs-lookup"><span data-stu-id="73d52-142">You must change or delete any such resource in your Azure AD directory before you can delete the custom domain name.</span></span>

## <a name="use-powershell-or-graph-api-to-manage-domain-names"></a><span data-ttu-id="73d52-143">Gebruik PowerShell of Graph API voor het beheren van domeinnamen</span><span class="sxs-lookup"><span data-stu-id="73d52-143">Use PowerShell or Graph API to manage domain names</span></span>
<span data-ttu-id="73d52-144">De meeste beheertaken voor domeinnamen in Azure Active Directory kunnen ook worden uitgevoerd met behulp van Microsoft PowerShell of programmatisch met behulp van Azure AD Graph API.</span><span class="sxs-lookup"><span data-stu-id="73d52-144">Most management tasks for domain names in Azure Active Directory can also be completed using Microsoft PowerShell, or programmatically using Azure AD Graph API.</span></span>

* [<span data-ttu-id="73d52-145">Met behulp van PowerShell voor het beheren van domeinnamen in Azure AD</span><span class="sxs-lookup"><span data-stu-id="73d52-145">Using PowerShell to manage domain names in Azure AD</span></span>](https://msdn.microsoft.com/library/azure/e1ef403f-3347-4409-8f46-d72dafa116e0#BKMK_ManageDomains)
* [<span data-ttu-id="73d52-146">Domeinnamen in Azure AD beheren met behulp van Graph API</span><span class="sxs-lookup"><span data-stu-id="73d52-146">Using Graph API to manage domain names in Azure AD</span></span>](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/domains-operations)

## <a name="next-steps"></a><span data-ttu-id="73d52-147">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="73d52-147">Next steps</span></span>
* [<span data-ttu-id="73d52-148">Meer informatie over domeinnamen in Azure AD</span><span class="sxs-lookup"><span data-stu-id="73d52-148">Learn about domain names in Azure AD</span></span>](active-directory-add-domain-concepts.md)
* [<span data-ttu-id="73d52-149">Aangepaste domeinnamen beheren</span><span class="sxs-lookup"><span data-stu-id="73d52-149">Manage custom domain names</span></span>](active-directory-add-manage-domain-names.md)


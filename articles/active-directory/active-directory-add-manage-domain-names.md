---
title: aaaManaging aangepaste domeinnamen in uw Azure Active Directory | Microsoft Docs
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
ms.openlocfilehash: 4b6d06fecf3be0621be51c38a1330eafdc1b4d35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="managing-custom-domain-names-in-your-azure-active-directory"></a><span data-ttu-id="2d782-103">Aangepaste domeinnamen in uw Azure Active Directory beheren</span><span class="sxs-lookup"><span data-stu-id="2d782-103">Managing custom domain names in your Azure Active Directory</span></span>
<span data-ttu-id="2d782-104">Een domeinnaam zijn een belangrijk id voor veel directoryresources als onderdeel van:</span><span class="sxs-lookup"><span data-stu-id="2d782-104">A domain name can be an important identifier for many directory resources, as part of:</span></span>

* <span data-ttu-id="2d782-105">Een gebruikersnaam of e-mailadres voor een gebruiker</span><span class="sxs-lookup"><span data-stu-id="2d782-105">A user name or email address for a user</span></span>
* <span data-ttu-id="2d782-106">Hallo-adres voor een groep</span><span class="sxs-lookup"><span data-stu-id="2d782-106">hello address for a group</span></span>
* <span data-ttu-id="2d782-107">Hallo app ID URI voor een toepassing</span><span class="sxs-lookup"><span data-stu-id="2d782-107">hello app ID URI for an application</span></span>

<span data-ttu-id="2d782-108">Een resource in Azure Active Directory (Azure AD), kan een domeinnaam die al is geverifieerd toobe eigendom van Hallo directory die Hallo-bron bevat bevatten.</span><span class="sxs-lookup"><span data-stu-id="2d782-108">A resource in Azure Active Directory (Azure AD) can include a domain name that is already verified toobe owned by hello directory that contains hello resource.</span></span> <span data-ttu-id="2d782-109">Alleen een globale beheerder kunt domein-beheertaken uitvoeren in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2d782-109">Only a global administrator can perform domain management tasks in Azure AD.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2d782-110">Microsoft raadt aan dat u Azure AD beheren met Hallo [Azure AD-beheercentrum](https://aad.portal.azure.com) in Hallo hello Azure-portal in plaats van de klassieke Azure-portal waarnaar wordt verwezen in dit artikel.</span><span class="sxs-lookup"><span data-stu-id="2d782-110">Microsoft recommends that you manage Azure AD using hello [Azure AD admin center](https://aad.portal.azure.com) in hello Azure portal instead of using hello Azure classic portal referenced in this article.</span></span> <span data-ttu-id="2d782-111">Zie voor hoe toomanage uw in hello Azure AD-beheercentrum domeinnamen, [aangepaste domeinnamen in uw Azure Active Directory beheren](active-directory-domains-manage-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="2d782-111">For how toomanage your domain names in hello Azure AD admin center, see [Managing custom domain names in your Azure Active Directory](active-directory-domains-manage-azure-portal.md).</span></span>

## <a name="set-hello-primary-domain-name-for-your-azure-ad-directory"></a><span data-ttu-id="2d782-112">Set Hallo primaire domeinnaam voor uw Azure AD-directory</span><span class="sxs-lookup"><span data-stu-id="2d782-112">Set hello primary domain name for your Azure AD directory</span></span>
<span data-ttu-id="2d782-113">Wanneer de map wordt gemaakt, wordt Hallo initiële domeinnaam, zoals 'contoso.onmicrosoft.com', is ook Hallo primaire domeinnaam voor uw directory.</span><span class="sxs-lookup"><span data-stu-id="2d782-113">When your directory is created, hello initial domain name, such as ‘contoso.onmicrosoft.com,’ is also hello primary domain name for your directory.</span></span> <span data-ttu-id="2d782-114">Primair domein Hallo Hallo standaarddomeinnaam voor een nieuwe gebruiker is wanneer u een nieuwe gebruiker in Hallo maakt [klassieke Azure-portal](https://manage.windowsazure.com/), of andere portals zoals Hallo Office 365-beheerportal.</span><span class="sxs-lookup"><span data-stu-id="2d782-114">hello primary domain is hello default domain name for a new user when you create a new user in hello [Azure classic portal](https://manage.windowsazure.com/), or other portals such as hello Office 365 admin portal.</span></span> <span data-ttu-id="2d782-115">Dit stroomlijnt proces voor een toocreate beheerder nieuwe gebruikers in de portal Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="2d782-115">This streamlines hello process for an administrator toocreate new users in hello portal.</span></span>

<span data-ttu-id="2d782-116">toochange Hallo de naam van het primaire domein voor uw directory:</span><span class="sxs-lookup"><span data-stu-id="2d782-116">toochange hello primary domain name for your directory:</span></span>

1. <span data-ttu-id="2d782-117">Meld u aan toohello [klassieke Azure-portal](https://manage.windowsazure.com/) met een gebruikersaccount dat een globale beheerder van uw Azure AD-directory.</span><span class="sxs-lookup"><span data-stu-id="2d782-117">Sign in toohello [Azure classic portal](https://manage.windowsazure.com/) with a user account that is a global administrator of your Azure AD directory.</span></span>
2. <span data-ttu-id="2d782-118">Selecteer **Active Directory** op de linkernavigatiebalk Hallo.</span><span class="sxs-lookup"><span data-stu-id="2d782-118">Select **Active Directory** on hello left navigation bar.</span></span>
3. <span data-ttu-id="2d782-119">Open uw directory.</span><span class="sxs-lookup"><span data-stu-id="2d782-119">Open your directory.</span></span>
4. <span data-ttu-id="2d782-120">Selecteer Hallo **domeinen** tabblad.</span><span class="sxs-lookup"><span data-stu-id="2d782-120">Select hello **Domains** tab.</span></span>
5. <span data-ttu-id="2d782-121">Selecteer Hallo **primaire wijziging** knop op de opdrachtbalk Hallo.</span><span class="sxs-lookup"><span data-stu-id="2d782-121">Select hello **Change primary** button on hello command bar.</span></span>
6. <span data-ttu-id="2d782-122">Selecteer Hallo-domein dat u toobe Hallo nieuwe primaire domein voor uw directory wilt.</span><span class="sxs-lookup"><span data-stu-id="2d782-122">Select hello domain that you want toobe hello new primary domain for your directory.</span></span>

<span data-ttu-id="2d782-123">U kunt primaire domeinnaam voor uw directory toobe Hallo geverifieerde aangepaste domeinen die niet is gefedereerd wijzigen.</span><span class="sxs-lookup"><span data-stu-id="2d782-123">You can change hello primary domain name for your directory toobe any verified custom domain that is not federated.</span></span> <span data-ttu-id="2d782-124">Veranderende Hallo primair domein voor uw directory heeft geen invloed op Hallo gebruikersnamen voor alle bestaande gebruikers.</span><span class="sxs-lookup"><span data-stu-id="2d782-124">Changing hello primary domain for your directory will not change hello user names for any existing users.</span></span>

## <a name="add-custom-domain-names-tooyour-azure-ad"></a><span data-ttu-id="2d782-125">Toevoegen van aangepast domein namen tooyour Azure AD</span><span class="sxs-lookup"><span data-stu-id="2d782-125">Add custom domain names tooyour Azure AD</span></span>
<span data-ttu-id="2d782-126">U kunt toevoegen, too900 aangepast domein namen tooeach Azure AD-directory.</span><span class="sxs-lookup"><span data-stu-id="2d782-126">You can add up too900 custom domain names tooeach Azure AD directory.</span></span> <span data-ttu-id="2d782-127">Hallo proces te[een aanvullende aangepaste domeinnaam toevoegen](active-directory-add-domain.md) is dezelfde hello voor Hallo eerst de aangepaste domeinnaam.</span><span class="sxs-lookup"><span data-stu-id="2d782-127">hello process too[add an additional custom domain name](active-directory-add-domain.md) is hello same for hello first custom domain name.</span></span>

## <a name="add-subdomains-of-a-custom-domain"></a><span data-ttu-id="2d782-128">Toevoegen van subdomeinen van een aangepast domein</span><span class="sxs-lookup"><span data-stu-id="2d782-128">Add subdomains of a custom domain</span></span>
<span data-ttu-id="2d782-129">Als u een domeinnaam van derde niveau zoals 'europe.contoso.com' tooyour directory tooadd wilt, moet u eerst toevoegen en controleren van Hallo tweede niveau domein, zoals contoso.com. Hallo subdomein wordt automatisch geverifieerd door Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2d782-129">If you want tooadd a third-level domain name such as ‘europe.contoso.com’ tooyour directory, you should first add and verify hello second-level domain, such as contoso.com. hello subdomain will be automatically verified by Azure AD.</span></span> <span data-ttu-id="2d782-130">toosee die subdomein dat u zojuist hebt toegevoegd Hallo is geverifieerd, vernieuwen Hallo pagina in Hallo browser met een lijst met Hallo domeinen in uw directory.</span><span class="sxs-lookup"><span data-stu-id="2d782-130">toosee that hello subdomain that you just added has been verified, refresh hello page in hello browser that lists hello domains in your directory.</span></span>

## <a name="what-toodo-if-you-change-hello-dns-registrar-for-your-custom-domain-name"></a><span data-ttu-id="2d782-131">Welke toodo als u Hallo DNS-registratieservice voor uw aangepaste domeinnaam wijzigen</span><span class="sxs-lookup"><span data-stu-id="2d782-131">What toodo if you change hello DNS registrar for your custom domain name</span></span>
<span data-ttu-id="2d782-132">Als u Hallo DNS-registratieservice voor uw aangepaste domeinnaam wijzigt, kunt u uw aangepaste domeinnaam met Azure AD zelf zonder onderbreking en zonder aanvullende configuratietaken toouse blijven.</span><span class="sxs-lookup"><span data-stu-id="2d782-132">If you change hello DNS registrar for your custom domain name, you can continue toouse your custom domain name with Azure AD itself without interruption and without additional configuration tasks.</span></span> <span data-ttu-id="2d782-133">Als u uw aangepaste domeinnaam met Office 365, Intune of andere services die afhankelijk van aangepaste domeinnamen in Azure AD gebruiken zijn, Raadpleeg de documentatie toohello voor deze services.</span><span class="sxs-lookup"><span data-stu-id="2d782-133">If you use your custom domain name with Office 365, Intune, or other services that rely on custom domain names in Azure AD, refer toohello documentation for those services.</span></span>

## <a name="delete-a-custom-domain-name"></a><span data-ttu-id="2d782-134">Verwijderen van een aangepaste domeinnaam</span><span class="sxs-lookup"><span data-stu-id="2d782-134">Delete a custom domain name</span></span>
<span data-ttu-id="2d782-135">Als uw organisatie die domeinnaam niet langer gebruikt, of als u moet toouse die domeinnaam met een andere Azure AD, kunt u een aangepaste domeinnaam van uw Azure AD verwijderen.</span><span class="sxs-lookup"><span data-stu-id="2d782-135">You can delete a custom domain name from your Azure AD if your organization no longer uses that domain name, or if you need toouse that domain name with another Azure AD.</span></span>

<span data-ttu-id="2d782-136">een aangepaste domeinnaam toodelete, u moet eerst voor zorgen dat geen resources in uw directory zijn afhankelijk van de domeinnaam Hallo.</span><span class="sxs-lookup"><span data-stu-id="2d782-136">toodelete a custom domain name, you must first ensure that no resources in your directory rely on hello domain name.</span></span> <span data-ttu-id="2d782-137">U kunt een domeinnaam niet verwijderen uit de map als:</span><span class="sxs-lookup"><span data-stu-id="2d782-137">You can't delete a domain name from your directory if:</span></span>

* <span data-ttu-id="2d782-138">Elke gebruiker heeft een gebruikersnaam, het e-mailadres of de proxy-adres dat Hallo domeinnaam omvatten.</span><span class="sxs-lookup"><span data-stu-id="2d782-138">Any user has a user name, email address, or proxy address that include hello domain name.</span></span>
* <span data-ttu-id="2d782-139">Een groep heeft een e-mailadres of de proxy-adres dat Hallo domeinnaam bevat.</span><span class="sxs-lookup"><span data-stu-id="2d782-139">Any group has an email address or proxy address that includes hello domain name.</span></span>
* <span data-ttu-id="2d782-140">Elke toepassing in uw Azure AD heeft een app ID URI die Hallo domeinnaam bevat.</span><span class="sxs-lookup"><span data-stu-id="2d782-140">Any application in your Azure AD has an app ID URI that includes hello domain name.</span></span>

<span data-ttu-id="2d782-141">U moet wijzigen of verwijderen van een dergelijke resource in uw Azure AD-directory voordat u de aangepaste domeinnaam Hallo kunt verwijderen.</span><span class="sxs-lookup"><span data-stu-id="2d782-141">You must change or delete any such resource in your Azure AD directory before you can delete hello custom domain name.</span></span>

## <a name="use-powershell-or-graph-api-toomanage-domain-names"></a><span data-ttu-id="2d782-142">PowerShell of Graph API toomanage domeinnamen gebruiken</span><span class="sxs-lookup"><span data-stu-id="2d782-142">Use PowerShell or Graph API toomanage domain names</span></span>
<span data-ttu-id="2d782-143">De meeste beheertaken voor domeinnamen in Azure Active Directory kunnen ook worden uitgevoerd met behulp van Microsoft PowerShell of programmatisch met behulp van Azure AD Graph API.</span><span class="sxs-lookup"><span data-stu-id="2d782-143">Most management tasks for domain names in Azure Active Directory can also be completed using Microsoft PowerShell, or programmatically using Azure AD Graph API.</span></span>

* [<span data-ttu-id="2d782-144">Met behulp van PowerShell toomanage domeinnamen in Azure AD</span><span class="sxs-lookup"><span data-stu-id="2d782-144">Using PowerShell toomanage domain names in Azure AD</span></span>](https://msdn.microsoft.com/library/azure/e1ef403f-3347-4409-8f46-d72dafa116e0#BKMK_ManageDomains)
* [<span data-ttu-id="2d782-145">Met behulp van Graph API toomanage domeinnamen in Azure AD</span><span class="sxs-lookup"><span data-stu-id="2d782-145">Using Graph API toomanage domain names in Azure AD</span></span>](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/domains-operations)

## <a name="next-steps"></a><span data-ttu-id="2d782-146">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="2d782-146">Next steps</span></span>
* [<span data-ttu-id="2d782-147">Meer informatie over domeinnamen in Azure AD</span><span class="sxs-lookup"><span data-stu-id="2d782-147">Learn about domain names in Azure AD</span></span>](active-directory-add-domain-concepts.md)
* [<span data-ttu-id="2d782-148">Aangepaste domeinnamen beheren</span><span class="sxs-lookup"><span data-stu-id="2d782-148">Manage custom domain names</span></span>](active-directory-add-manage-domain-names.md)


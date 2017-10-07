---
title: aaaHow tooconfigure automatische registratie van Windows-domein-apparaten met Azure Active Directory | Microsoft Docs
description: Instellen van uw domein Windows-apparaten tooregister automatisch en zonder tussenkomst met Azure Active Directory.
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 54e1b01b-03ee-4c46-bcf0-e01affc0419d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: 1d736eba734418231f12e23a8fc1a93405f129c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-active-directory-device-registration"></a><span data-ttu-id="e7208-103">Aan de slag met Azure Active Directory-apparaatregistratie</span><span class="sxs-lookup"><span data-stu-id="e7208-103">Get started with Azure Active Directory device registration</span></span>

<span data-ttu-id="e7208-104">Azure Active Directory-apparaatregistratie vormt de basis Hallo voor scenario's voor voorwaardelijke toegang op basis van apparaten.</span><span class="sxs-lookup"><span data-stu-id="e7208-104">Azure Active Directory device registration is hello foundation for device-based conditional access scenarios.</span></span> <span data-ttu-id="e7208-105">Wanneer een apparaat is geregistreerd, biedt Azure Active Directory-apparaatregistratie Hallo-apparaat met een identiteit die gebruikt tooauthenticate Hallo apparaat is wanneer Hallo gebruiker zich aanmeldt.</span><span class="sxs-lookup"><span data-stu-id="e7208-105">When a device is registered, Azure Active Directory device registration provides hello device with an identity which is used tooauthenticate hello device when hello user signs in.</span></span> <span data-ttu-id="e7208-106">vervolgens Hallo geverifieerde apparaat en Hallo kenmerken van Hallo-apparaat, kunnen de gebruikte tooenforce beleidsregels voor voorwaardelijke toegang voor toepassingen die worden gehost in Hallo cloud en on-premises worden.</span><span class="sxs-lookup"><span data-stu-id="e7208-106">hello authenticated device, and hello attributes of hello device, can then be used tooenforce conditional access policies for applications that are hosted in hello cloud and on-premises.</span></span>

<span data-ttu-id="e7208-107">In combinatie met een MDM-oplossing voor mobiele apparaten, zoals Microsoft Intune, worden Hallo apparaatkenmerken in Azure Active Directory bijgewerkt met aanvullende informatie over het Hallo-apparaat.</span><span class="sxs-lookup"><span data-stu-id="e7208-107">When combined with a mobile device management(MDM) solution such as Microsoft Intune, hello device attributes in Azure Active Directory are updated with additional information about hello device.</span></span> <span data-ttu-id="e7208-108">Hiermee kunt u regels voor voorwaardelijke toegang toocreate die toegang van apparaten toomeet afdwingen uw standaarden voor beveiliging en naleving.</span><span class="sxs-lookup"><span data-stu-id="e7208-108">This allows you toocreate conditional access rules that enforce access from devices toomeet your standards for security and compliance.</span></span> <span data-ttu-id="e7208-109">Zie voor meer informatie over de inschrijving van apparaten in Microsoft Intune, apparaten inschrijven voor beheer in Intune.</span><span class="sxs-lookup"><span data-stu-id="e7208-109">For more information on enrolling devices in Microsoft Intune, see Enroll devices for management in Intune.</span></span>
<span data-ttu-id="e7208-110">Mogelijke scenario's met Azure Active Directory apparaat registratie Azure Active Directory-apparaatregistratie biedt ondersteuning voor iOS, Android en Windows apparaten.</span><span class="sxs-lookup"><span data-stu-id="e7208-110">Scenarios enabled by Azure Active Directory Device Registration Azure Active Directory Device Registration includes support for iOS, Android, and Windows devices.</span></span> <span data-ttu-id="e7208-111">afzonderlijke scenario's voor een Hallo die gebruikmaken van Azure AD-apparaatregistratie gelden mogelijk meer specifieke vereisten en platformondersteuning.</span><span class="sxs-lookup"><span data-stu-id="e7208-111">hello individual scenarios that utilize Azure AD Device Registration may have more specific requirements and platform support.</span></span> 

<span data-ttu-id="e7208-112">Het gaat om de volgende scenario's:</span><span class="sxs-lookup"><span data-stu-id="e7208-112">These scenarios are as follows:</span></span>

- <span data-ttu-id="e7208-113">**Voorwaardelijke toegang voor Office 365-toepassingen met Microsoft Intune:** IT-beheerders kunnen voorwaardelijke toegang apparaat beleid toosecure bedrijfsbronnen, inrichten terwijl op Hallo dezelfde toestaan informatiemedewerkers op compatibele apparaten tijdstip tooaccess Hallo-services.</span><span class="sxs-lookup"><span data-stu-id="e7208-113">**Conditional access for Office 365 applications with Microsoft Intune:** IT admins can provision conditional access device policies toosecure corporate resources, while at hello same time allowing information workers on compliant devices tooaccess hello services.</span></span> <span data-ttu-id="e7208-114">Zie Conditional Access Device Policies for Office 365 services (Engelstalig) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="e7208-114">For more information, see Conditional Access Device Policies for Office 365 services.</span></span>

- <span data-ttu-id="e7208-115">**Voorwaardelijke toegang tooapplications die worden gehost op de lokale:** kunt u geregistreerde apparaten met toegangsbeleid voor toepassingen die zijn geconfigureerd toouse AD FS met Windows Server 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="e7208-115">**Conditional access tooapplications that are hosted on-premises:** You can use registered devices with access policies for applications that are configured toouse AD FS with Windows Server 2012 R2.</span></span> <span data-ttu-id="e7208-116">Zie [Setting up On-premises Conditional Access using Azure Active Directory Device Registration](active-directory-device-registration-on-premises-setup.md) (Engelstalig) voor meer informatie over het instellen van on-premises voorwaardelijke toegang.</span><span class="sxs-lookup"><span data-stu-id="e7208-116">For more information about setting up conditional access for on-premises, see [Setting up On-premises Conditional Access using Azure Active Directory device registration](active-directory-device-registration-on-premises-setup.md).</span></span>

## <a name="setting-up-azure-active-directory-device-registration"></a><span data-ttu-id="e7208-117">Azure Active Directory-apparaatregistratie configureren</span><span class="sxs-lookup"><span data-stu-id="e7208-117">Setting up Azure Active Directory Device Registration</span></span>

<span data-ttu-id="e7208-118">apparaatregistratie toosetup, hebt u meerdere opties:</span><span class="sxs-lookup"><span data-stu-id="e7208-118">toosetup device registration, you have multiple options:</span></span>

- <span data-ttu-id="e7208-119">Apparaten kunnen registreren wanneer samengevoegde tooAzure AD-domein.</span><span class="sxs-lookup"><span data-stu-id="e7208-119">Devices can register when joined tooAzure AD domain.</span></span> <span data-ttu-id="e7208-120">Voor meer informatie over dit onderwerp kunt u meer informatie over Azure AD Join en Hallo instellingen die vereist zijn voor gebruikers toojoin Azure AD-domein.</span><span class="sxs-lookup"><span data-stu-id="e7208-120">For more on this topic, you can Learn more about Azure AD Join and hello settings required for users toojoin Azure AD domain.</span></span>

- <span data-ttu-id="e7208-121">Apparaten kunnen worden geregistreerd wanneer gebruikers werk voegen of school tooWindows accounts op een persoonlijk apparaat, of wanneer u mobiele apparaten verbinding maken met bronnen op het werk tooa registratie vereisen.</span><span class="sxs-lookup"><span data-stu-id="e7208-121">Devices can be registered when users add work or school accounts tooWindows on a personal device or when mobile devices connect tooa work resources requiring registration.</span></span> <span data-ttu-id="e7208-122">tooensure, moet u Azure AD-apparaatregistratie in Azure Portal Hallo inschakelen.</span><span class="sxs-lookup"><span data-stu-id="e7208-122">tooensure this, you must enable Azure AD Device Registration in hello Azure Portal.</span></span> 

- <span data-ttu-id="e7208-123">Apparaten kunnen worden geregistreerd met behulp van automatische apparaatregistratie voor traditionele domein-machines.</span><span class="sxs-lookup"><span data-stu-id="e7208-123">Devices can be registered using automatic device registration for traditional domain-joined machines.</span></span> <span data-ttu-id="e7208-124">tooensure, moet u eerst Setup Azure AD Connect voordat u met automatische apparaatregistratie doorgaat.</span><span class="sxs-lookup"><span data-stu-id="e7208-124">tooensure this, you must first Setup Azure AD Connect before you continue with automatic device registration.</span></span>

<span data-ttu-id="e7208-125">Zie voor instructies nieuwste [hoe tooconfigure automatische registratie van Windows-domein apparaten met Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md).</span><span class="sxs-lookup"><span data-stu-id="e7208-125">For latest instructions, see [How tooconfigure automatic registration of Windows domain-joined devices with Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md).</span></span>  
<span data-ttu-id="e7208-126">U kunt ook bekijken en inschakelen of uitschakelen van de geregistreerde apparaten met Hallo Beheerdersportal in Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="e7208-126">You can also review and enable or disable registered devices using hello Administrator Portal in Azure Active Directory.</span></span>

## <a name="enable-hello-azure-active-directory-device-registration-service"></a><span data-ttu-id="e7208-127">Hello Azure Active Directory device registration-service inschakelen</span><span class="sxs-lookup"><span data-stu-id="e7208-127">Enable hello Azure Active Directory device registration service</span></span>

<span data-ttu-id="e7208-128">**tooenable hello Azure Active Directory device registration-service:**</span><span class="sxs-lookup"><span data-stu-id="e7208-128">**tooenable hello Azure Active Directory device registration service:**</span></span>

1.  <span data-ttu-id="e7208-129">Meld u toohello Microsoft Azure-portal als administrator.</span><span class="sxs-lookup"><span data-stu-id="e7208-129">Sign in toohello Microsoft Azure portal as administrator.</span></span>

2.  <span data-ttu-id="e7208-130">Selecteer in het linkerdeelvenster Hallo **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e7208-130">On hello left pane, select **Active Directory**.</span></span>

3.  <span data-ttu-id="e7208-131">Tabblad Hallo-map, selecteer uw directory.</span><span class="sxs-lookup"><span data-stu-id="e7208-131">On hello Directory tab, select your directory.</span></span>

4.  <span data-ttu-id="e7208-132">Klik op **Configureren**</span><span class="sxs-lookup"><span data-stu-id="e7208-132">Click **Configure**.</span></span>

5.  <span data-ttu-id="e7208-133">Schuif te**apparaten**.</span><span class="sxs-lookup"><span data-stu-id="e7208-133">Scroll too**Devices**.</span></span>

6.  <span data-ttu-id="e7208-134">Alles selecteren voor gebruikers kan hun apparaten REGISTREREN met AZURE AD.</span><span class="sxs-lookup"><span data-stu-id="e7208-134">Select ALL for USERS MAY REGISTER THEIR DEVICES WITH AZURE AD.</span></span>

7.  <span data-ttu-id="e7208-135">Selecteer Hallo maximum aantal apparaten dat u wilt dat tooauthorize per gebruiker.</span><span class="sxs-lookup"><span data-stu-id="e7208-135">Select hello maximum number of devices you want tooauthorize per user.</span></span>

<span data-ttu-id="e7208-136">Hallo registratie bij Microsoft Intune of Mobile Device Management voor Office 365 is apparaatregistratie vereist.</span><span class="sxs-lookup"><span data-stu-id="e7208-136">hello enrollment with Microsoft Intune or Mobile Device Management for Office 365 requires device registration.</span></span> <span data-ttu-id="e7208-137">Als u een van deze services hebt geconfigureerd **alle** is geselecteerd en **** is uitgeschakeld.</span><span class="sxs-lookup"><span data-stu-id="e7208-137">If you have configured either of these services, **ALL** is selected and **NONE** is disabled.</span></span> <span data-ttu-id="e7208-138">Zorg ervoor dat ze juist zijn geconfigureerd en Hallo geschikte licenties hebt.</span><span class="sxs-lookup"><span data-stu-id="e7208-138">Please ensure that they are configured correctly and have hello appropriate licensing.</span></span>

<span data-ttu-id="e7208-139">Verificatie met twee factoren is standaard niet ingeschakeld voor Hallo-service.</span><span class="sxs-lookup"><span data-stu-id="e7208-139">By default, two-factor authentication is not enabled for hello service.</span></span> <span data-ttu-id="e7208-140">Deze vorm van verificatie wordt echter wel aanbevolen bij het registreren van een apparaat.</span><span class="sxs-lookup"><span data-stu-id="e7208-140">However, two-factor authentication is recommended when registering a device.</span></span>

- <span data-ttu-id="e7208-141">Voordat u verificatie met twee factoren voor deze service, moet u een provider voor verificatie met twee factoren configureren in Azure Active Directory en uw gebruikersaccounts configureren voor meervoudige verificatie, Zie multi-factor Authentication toevoegen tooAzure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e7208-141">Before requiring two-factor authentication for this service, you must configure a two-factor authentication provider in Azure Active Directory and configure your user accounts for Multi-Factor Authentication, see Adding Multi-Factor Authentication tooAzure Active Directory</span></span>

- <span data-ttu-id="e7208-142">Als u gebruikmaakt van AD FS met Windows Server 2012 R2, moet u een module verificatie met twee factoren configureren in AD FS, Zie multi-factor Authentication gebruiken met Active Directory Federation Services.</span><span class="sxs-lookup"><span data-stu-id="e7208-142">If you are using AD FS with Windows Server 2012 R2, you must configure a two-factor authentication module in AD FS, see Using Multi-Factor Authentication with Active Directory Federation Services.</span></span>

## <a name="view-and-manage-device-objects-in-azure-active-directory"></a><span data-ttu-id="e7208-143">Apparaatobjecten bekijken en beheren in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e7208-143">View and manage device objects in Azure Active Directory</span></span>

<span data-ttu-id="e7208-144">Vanuit de Hallo beheerder van de Azure portal kunt u weergeven, blokkeren en blokkering van apparaten.</span><span class="sxs-lookup"><span data-stu-id="e7208-144">From hello Azure Administrator portal, you can view, block, and unblock devices.</span></span> <span data-ttu-id="e7208-145">Een apparaat dat is geblokkeerd hoeft niet langer toegang tooapplications die geconfigureerd tooallow alleen geregistreerde apparaten zijn.</span><span class="sxs-lookup"><span data-stu-id="e7208-145">A device that is blocked will no longer have access tooapplications that are configured tooallow only registered devices.</span></span>

<span data-ttu-id="e7208-146">**tooview en apparaatobjecten in Azure Active Directory beheren:**</span><span class="sxs-lookup"><span data-stu-id="e7208-146">**tooview and manage device objects in Azure Active Directory:**</span></span>
 
1.  <span data-ttu-id="e7208-147">Meld u aan toohello Microsoft Azure-portal als beheerder.</span><span class="sxs-lookup"><span data-stu-id="e7208-147">Log on toohello Microsoft Azure portal as administrator.</span></span>

2.  <span data-ttu-id="e7208-148">Selecteer in het linkerdeelvenster Hallo **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e7208-148">On hello left pane, select **Active Directory**.</span></span>

3.  <span data-ttu-id="e7208-149">Selecteer uw directory.</span><span class="sxs-lookup"><span data-stu-id="e7208-149">Select your directory.</span></span>

4.  <span data-ttu-id="e7208-150">Selecteer **gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="e7208-150">Select **Users**.</span></span> 

5.  <span data-ttu-id="e7208-151">Klik op Hallo gebruiker waarvoor u wilt dat toosee Hallo apparaten.</span><span class="sxs-lookup"><span data-stu-id="e7208-151">Click hello user for which you want toosee hello devices.</span></span>

6.  <span data-ttu-id="e7208-152">Selecteer **apparaten**.</span><span class="sxs-lookup"><span data-stu-id="e7208-152">Select **Devices**.</span></span>

7.  <span data-ttu-id="e7208-153">Selecteer **apparaten geregistreerd**.</span><span class="sxs-lookup"><span data-stu-id="e7208-153">Select **Registered Devices**.</span></span>

<span data-ttu-id="e7208-154">U kunt nu controleren, blokkeren of deblokkeren van gebruiker Hallo geregistreerde apparaten.</span><span class="sxs-lookup"><span data-stu-id="e7208-154">Now, you can review, block, or unblock hello user's registered devices.</span></span>
<span data-ttu-id="e7208-155">Windows 10-apparaten die zich on-premises domein en automatisch worden geregistreerd, worden niet weergegeven onder het tabblad Hallo-gebruikers. Gebruik Hallo Get MsolDevice PowerShell-opdracht toofind alle apparaten in uw onderneming.</span><span class="sxs-lookup"><span data-stu-id="e7208-155">Windows 10 devices that are on-premises domain-joined and automatically registered do not appear under hello Users tab. Please use hello Get-MsolDevice PowerShell command toofind all your enterprise devices.</span></span> 


## <a name="next-steps"></a><span data-ttu-id="e7208-156">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="e7208-156">Next steps</span></span>

<span data-ttu-id="e7208-157">toosetup automatische apparaatregistratie, Zie [hoe tooconfigure automatische registratie van Windows-domein apparaten met Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md).</span><span class="sxs-lookup"><span data-stu-id="e7208-157">toosetup automated device registration, see [How tooconfigure automatic registration of Windows domain-joined devices with Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md).</span></span>



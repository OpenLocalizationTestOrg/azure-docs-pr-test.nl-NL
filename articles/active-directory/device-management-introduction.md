---
title: aaaIntroduction toodevice management in Azure Active Directory | Microsoft Docs
description: Meer informatie over hoe Apparaatbeheer kan u helpen tooget controle over het Hallo-apparaten die toegang hebben tot bronnen in uw omgeving.
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
ms.date: 08/24/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: e2fc0a3e8d00dc69cf01db9074e34427e396cfcf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toodevice-management-in-azure-active-directory"></a><span data-ttu-id="6aba2-103">Inleiding toodevice management in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6aba2-103">Introduction toodevice management in Azure Active Directory</span></span>

<span data-ttu-id="6aba2-104">Azure Active Directory (Azure AD) kunnen in een wereld mobiel eerste, cloud eerste toodevices voor eenmalige aanmelding, apps en services vanaf elke locatie.</span><span class="sxs-lookup"><span data-stu-id="6aba2-104">In a mobile-first, cloud-first world, Azure Active Directory (Azure AD) enables single sign-on toodevices, apps, and services from anywhere.</span></span> <span data-ttu-id="6aba2-105">IT-professionals worden met Hallo komst van apparaten - Bring Your Own Device (BYOD), inclusief momenteel geconfronteerd met twee tegengestelde doelstellingen:</span><span class="sxs-lookup"><span data-stu-id="6aba2-105">With hello proliferation of devices - including Bring Your Own Device (BYOD), IT professionals are faced with two opposing goals:</span></span>

- <span data-ttu-id="6aba2-106">Hallo eindgebruikers toobe productief zorgen overal en wanneer</span><span class="sxs-lookup"><span data-stu-id="6aba2-106">Empower hello end users toobe productive wherever and whenever</span></span>
- <span data-ttu-id="6aba2-107">Beveiligen van zakelijke activa Hallo op elk gewenst moment</span><span class="sxs-lookup"><span data-stu-id="6aba2-107">Protect hello corporate assets at any time</span></span>

<span data-ttu-id="6aba2-108">Via apparaten wel uw gebruikers toegang tooyour zakelijke activa.</span><span class="sxs-lookup"><span data-stu-id="6aba2-108">Through devices, your users are getting access tooyour corporate assets.</span></span> <span data-ttu-id="6aba2-109">tooprotect uw zakelijke activa als IT-beheerder wilt u toohave controle over deze apparaten.</span><span class="sxs-lookup"><span data-stu-id="6aba2-109">tooprotect your corporate assets, as an IT administrator, you want toohave control over these devices.</span></span> <span data-ttu-id="6aba2-110">Hiermee kunt u ervoor dat uw gebruikers toegang hebben tot de bronnen vanaf apparaten die voldoen aan uw standaarden voor beveiliging en naleving toomake.</span><span class="sxs-lookup"><span data-stu-id="6aba2-110">This enables you toomake sure that your users are accessing your resources from devices that meet your standards for security and compliance.</span></span> 

<span data-ttu-id="6aba2-111">Apparaatbeheer is ook Hallo fundering voor [voorwaardelijke toegang op basis van apparaten](active-directory-conditional-access-policy-connected-applications.md).</span><span class="sxs-lookup"><span data-stu-id="6aba2-111">Device management is also hello foundation for [device-based conditional access](active-directory-conditional-access-policy-connected-applications.md).</span></span> <span data-ttu-id="6aba2-112">Met voorwaardelijke toegang op basis van apparaten, kunt u ervoor zorgen dat toegang tooresources in uw omgeving alleen mogelijk met is vertrouwde apparaten.</span><span class="sxs-lookup"><span data-stu-id="6aba2-112">With device-based conditional access, you can ensure that access tooresources in your environment is only possible with trusted devices.</span></span>   

<span data-ttu-id="6aba2-113">In dit onderwerp wordt uitgelegd hoe beheer van apparaten in Azure Active Directory werkt.</span><span class="sxs-lookup"><span data-stu-id="6aba2-113">This topic explains how device management in Azure Active Directory works.</span></span>

## <a name="getting-devices-under-hello-control-of-azure-ad"></a><span data-ttu-id="6aba2-114">Apparaten onder beheer van Azure AD Hallo laten</span><span class="sxs-lookup"><span data-stu-id="6aba2-114">Getting devices under hello control of Azure AD</span></span>

<span data-ttu-id="6aba2-115">een apparaat onder het beheer van Azure AD Hallo tooget, hebt u twee opties:</span><span class="sxs-lookup"><span data-stu-id="6aba2-115">tooget a device under hello control of Azure AD, you have two options:</span></span>

- <span data-ttu-id="6aba2-116">Registreren</span><span class="sxs-lookup"><span data-stu-id="6aba2-116">Registering</span></span> 
- <span data-ttu-id="6aba2-117">Samenvoegen</span><span class="sxs-lookup"><span data-stu-id="6aba2-117">Joining</span></span>

<span data-ttu-id="6aba2-118">**Registreren van** een apparaat tooAzure AD kunt u toomanage een apparaat-id.</span><span class="sxs-lookup"><span data-stu-id="6aba2-118">**Registering** a device tooAzure AD enables you toomanage a device’s identity.</span></span> <span data-ttu-id="6aba2-119">Wanneer een apparaat is geregistreerd, biedt Azure AD-apparaatregistratie Hallo-apparaat met een identiteit die is gebruikt tooauthenticate Hallo apparaat wanneer een gebruiker zich aanmeldt tooAzure AD.</span><span class="sxs-lookup"><span data-stu-id="6aba2-119">When a device is registered, Azure AD device registration provides hello device with an identity that is used tooauthenticate hello device when a user signs-in tooAzure AD.</span></span> <span data-ttu-id="6aba2-120">U kunt Hallo identiteit tooenable gebruiken of een apparaat uitschakelen.</span><span class="sxs-lookup"><span data-stu-id="6aba2-120">You can use hello identity tooenable or disable a device.</span></span>

<span data-ttu-id="6aba2-121">In combinatie met een MDM-oplossing voor mobiele apparaten, zoals Microsoft Intune, worden Hallo apparaatkenmerken in Azure AD bijgewerkt met aanvullende informatie over het Hallo-apparaat.</span><span class="sxs-lookup"><span data-stu-id="6aba2-121">When combined with a mobile device management(MDM) solution such as Microsoft Intune, hello device attributes in Azure AD are updated with additional information about hello device.</span></span> <span data-ttu-id="6aba2-122">Hiermee kunt u regels voor voorwaardelijke toegang toocreate die toegang van apparaten toomeet afdwingen uw standaarden voor beveiliging en naleving.</span><span class="sxs-lookup"><span data-stu-id="6aba2-122">This allows you toocreate conditional access rules that enforce access from devices toomeet your standards for security and compliance.</span></span> <span data-ttu-id="6aba2-123">Zie voor meer informatie over de inschrijving van apparaten in Microsoft Intune, apparaten inschrijven voor beheer in Intune.</span><span class="sxs-lookup"><span data-stu-id="6aba2-123">For more information on enrolling devices in Microsoft Intune, see Enroll devices for management in Intune .</span></span>

<span data-ttu-id="6aba2-124">**Lid worden van** een apparaat is een uitbreiding tooregistering een apparaat.</span><span class="sxs-lookup"><span data-stu-id="6aba2-124">**Joining** a device is an extension tooregistering a device.</span></span> <span data-ttu-id="6aba2-125">Dit betekent het geeft u alle Hallo voordelen van het registreren van een apparaat en in toevoeging toothis, ook invloed op Hallo van lokale status van een apparaat.</span><span class="sxs-lookup"><span data-stu-id="6aba2-125">This means, it provides you with all hello benefits of registering a device and in addition toothis, it also changes hello local state of a device.</span></span> <span data-ttu-id="6aba2-126">Hallo lokale status wijzigen, kunt uw gebruikers toosign in tooa apparaat met een organisatie werk- of schoolaccount in plaats van een persoonlijk account.</span><span class="sxs-lookup"><span data-stu-id="6aba2-126">Changing hello local state enables your users toosign-in tooa device using an organizational work or school account instead of a personal account.</span></span>

## <a name="azure-ad-registered-devices"></a><span data-ttu-id="6aba2-127">Azure AD ingeschreven apparaten</span><span class="sxs-lookup"><span data-stu-id="6aba2-127">Azure AD registered devices</span></span>   

<span data-ttu-id="6aba2-128">Hallo doel van Azure AD ingeschreven apparaten is tooprovide u met ondersteuning voor Hallo **Bring Your Own Device (BYOD)** scenario.</span><span class="sxs-lookup"><span data-stu-id="6aba2-128">hello goal of Azure AD registered devices is tooprovide you with support for hello **Bring Your Own Device (BYOD)** scenario.</span></span> <span data-ttu-id="6aba2-129">In dit scenario wordt een gebruiker toegang krijgen tot bronnen van van uw organisatie Azure Active Directory die worden beheerd met behulp van een persoonlijk apparaat.</span><span class="sxs-lookup"><span data-stu-id="6aba2-129">In this scenario, a user can access your organization’s Azure Active Directory controlled resources using a personal device.</span></span>  

![Azure AD ingeschreven apparaten](./media/device-management-introduction/03.png)

<span data-ttu-id="6aba2-131">Hallo-toegang is gebaseerd op een account voor werk of school die is ingevoerd op Hallo-apparaat.</span><span class="sxs-lookup"><span data-stu-id="6aba2-131">hello access is based on a work or school account that has been entered on hello device.</span></span>  
<span data-ttu-id="6aba2-132">Windows 10 kan bijvoorbeeld gebruikers tooadd een werk of school-account tooa pc, tablet of telefoon.</span><span class="sxs-lookup"><span data-stu-id="6aba2-132">For example, Windows 10 enables users tooadd a work or school account tooa personal computer, tablet, or phone.</span></span>  
<span data-ttu-id="6aba2-133">Wanneer een gebruiker een werk- of schoolaccount, Hallo-apparaat is toegevoegd, is geregistreerd in Azure AD en eventueel ingeschreven in Hallo mobiele apparaten (MDM) beheersysteem dat uw organisatie is geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="6aba2-133">When a user has added a work or school account, hello device is registered with Azure AD and optionally enrolled in hello mobile device management (MDM) system that your organization has configured.</span></span> <span data-ttu-id="6aba2-134">Gebruikers van uw organisatie kunnen toevoegen van een werk of school account tooa persoonlijk apparaat gemakkelijk:</span><span class="sxs-lookup"><span data-stu-id="6aba2-134">Your organization’s users can add a work or school account tooa personal device conveniently:</span></span>

- <span data-ttu-id="6aba2-135">Bij het openen van een werktoepassing voor Hallo eerst</span><span class="sxs-lookup"><span data-stu-id="6aba2-135">When accessing a work application for hello first time</span></span>
- <span data-ttu-id="6aba2-136">Handmatig via Hallo **instellingen** menu in geval van Windows 10 Hallo</span><span class="sxs-lookup"><span data-stu-id="6aba2-136">Manually via hello **Settings** menu in hello case of Windows 10</span></span> 

<span data-ttu-id="6aba2-137">U kunt Azure AD geregistreerde apparaten configureren voor Windows 10-, iOS-, Android- en Mac OS.</span><span class="sxs-lookup"><span data-stu-id="6aba2-137">You can configure Azure AD registered devices for Windows 10, iOS, Android and macOS.</span></span>

## <a name="azure-ad-joined-devices"></a><span data-ttu-id="6aba2-138">Azure AD die lid zijn van apparaten</span><span class="sxs-lookup"><span data-stu-id="6aba2-138">Azure AD joined devices</span></span>

<span data-ttu-id="6aba2-139">Hallo-doel van Azure AD die lid zijn van apparaten is toosimplify:</span><span class="sxs-lookup"><span data-stu-id="6aba2-139">hello goal of Azure AD joined devices is toosimplify:</span></span>

- <span data-ttu-id="6aba2-140">Windows-implementaties van apparaten die eigendom zijn van werkitems</span><span class="sxs-lookup"><span data-stu-id="6aba2-140">Windows deployments of work-owned devices</span></span> 
- <span data-ttu-id="6aba2-141">Toegang tooorganizational apps en resources van een Windows-apparaat</span><span class="sxs-lookup"><span data-stu-id="6aba2-141">Access tooorganizational apps and resources from any Windows device</span></span>

![Azure AD ingeschreven apparaten](./media/device-management-introduction/02.png)


<span data-ttu-id="6aba2-143">Deze doelstellingen worden bereikt door het verstrekken van uw gebruikers met een selfservice-ervaring voor het ophalen van apparaten die eigendom zijn van werk onder het Hallo-beheer van Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6aba2-143">These goals are accomplished by providing your users with a self-service experience for getting work-owned devices under hello control of Azure AD.</span></span>  
<span data-ttu-id="6aba2-144">**Azure AD Join** is bedoeld voor organisaties die cloud eerste / alleen in de cloud.</span><span class="sxs-lookup"><span data-stu-id="6aba2-144">**Azure AD Join** is intended for organizations that are cloud-first / cloud-only.</span></span> <span data-ttu-id="6aba2-145">Dit zijn meestal kleine en middelgrote bedrijven die geen een on-premises Windows Server Active Directory-infrastructuur.</span><span class="sxs-lookup"><span data-stu-id="6aba2-145">These are typically small- and medium-sized businesses that do not have an on-premises Windows Server Active Directory infrastructure.</span></span> 

<span data-ttu-id="6aba2-146">Implementatie van Azure AD die lid zijn van apparaten biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="6aba2-146">Implementing Azure AD joined devices provides you with hello following benefits:</span></span>

- <span data-ttu-id="6aba2-147">**Eenmalige aanmelding (SSO)** tooyour Azure beheerd SaaS-apps en services.</span><span class="sxs-lookup"><span data-stu-id="6aba2-147">**Single-Sign-On (SSO)** tooyour Azure managed SaaS apps and services.</span></span> <span data-ttu-id="6aba2-148">Uw gebruikers zien geen extra authenticatie prompts bij het openen van bronnen op het werk.</span><span class="sxs-lookup"><span data-stu-id="6aba2-148">Your users don’t see additional authentication prompts when accessing work resources.</span></span> <span data-ttu-id="6aba2-149">Hallo SSO-functionaliteit is zelfs wanneer ze niet verbonden toohello domeinnetwerk die beschikbaar zijn.</span><span class="sxs-lookup"><span data-stu-id="6aba2-149">hello SSO functionality is even when they are not connected toohello domain network available.</span></span>

- <span data-ttu-id="6aba2-150">**Enterprise compatibele roaming** van gebruikersinstellingen op gekoppelde apparaten.</span><span class="sxs-lookup"><span data-stu-id="6aba2-150">**Enterprise compliant roaming** of user settings across joined devices.</span></span> <span data-ttu-id="6aba2-151">Gebruikers hoeven niet tooconnect een Microsoft-account (bijvoorbeeld Hotmail) toosee-instellingen op apparaten.</span><span class="sxs-lookup"><span data-stu-id="6aba2-151">Users don’t need tooconnect a Microsoft account (for example, Hotmail) toosee settings across devices.</span></span>

- <span data-ttu-id="6aba2-152">**Toegang tot tooWindows Store voor bedrijven** met behulp van AD-account.</span><span class="sxs-lookup"><span data-stu-id="6aba2-152">**Access tooWindows Store for Business** using AD account.</span></span> <span data-ttu-id="6aba2-153">Uw gebruikers kunnen kiezen uit een inventarisatie van toepassingen die vooraf zijn geselecteerd door Hallo-organisatie.</span><span class="sxs-lookup"><span data-stu-id="6aba2-153">Your users can choose from an inventory of applications pre-selected by hello organization.</span></span>

- <span data-ttu-id="6aba2-154">**Windows Hello** ondersteuning voor beveiligde en gemakkelijke toegang tot toowork bronnen.</span><span class="sxs-lookup"><span data-stu-id="6aba2-154">**Windows Hello** support for secure and convenient access toowork resources.</span></span>

- <span data-ttu-id="6aba2-155">**Beperking van toegang** tooapps van alleen de apparaten die voldoen aan nalevingsbeleid.</span><span class="sxs-lookup"><span data-stu-id="6aba2-155">**Restriction of access** tooapps from only devices that meet compliance policy.</span></span>

<span data-ttu-id="6aba2-156">Terwijl Azure AD join is voornamelijk bedoeld voor organisaties waarvoor geen een on-premises Windows Server Active Directory-infrastructuur, kunt u gewoon ook worden gebruikt in scenario's waarbij:</span><span class="sxs-lookup"><span data-stu-id="6aba2-156">While Azure AD join is primarily intended for organizations that do not have an on-premises Windows Server Active Directory infrastructure, you can certainly also use it in scenarios where:</span></span>

- <span data-ttu-id="6aba2-157">U kunt een domein lokale bijvoorbeeld niet gebruiken als u mobiele apparaten zoals tablets en telefoons onder controle tooget moet.</span><span class="sxs-lookup"><span data-stu-id="6aba2-157">You can’t use an on-premises domain join, for example, if you need tooget mobile devices such as tablets and phones under control.</span></span>

- <span data-ttu-id="6aba2-158">Uw gebruikers moeten voornamelijk tooaccess Office 365 of andere SaaS-apps die is geïntegreerd met Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6aba2-158">Your users primarily need tooaccess Office 365 or other SaaS apps integrated with Azure AD.</span></span>

- <span data-ttu-id="6aba2-159">U wilt dat een groep gebruikers toomanage in Azure AD in plaats van in Active Directory.</span><span class="sxs-lookup"><span data-stu-id="6aba2-159">You want toomanage a group of users in Azure AD instead of in Active Directory.</span></span> <span data-ttu-id="6aba2-160">Dit kan van toepassing, bijvoorbeeld tooseasonal werknemers, contractanten of studenten.</span><span class="sxs-lookup"><span data-stu-id="6aba2-160">This can apply, for example, tooseasonal workers, contractors, or students.</span></span>

- <span data-ttu-id="6aba2-161">Wilt u gekoppelde mogelijkheden tooworkers tooprovide in externe filialen met beperkte on-premises infrastructuur.</span><span class="sxs-lookup"><span data-stu-id="6aba2-161">You want tooprovide joining capabilities tooworkers in remote branch offices with limited on-premises infrastructure.</span></span>

<span data-ttu-id="6aba2-162">U kunt Azure AD die lid zijn van apparaten voor Windows 10-apparaten kunt configureren.</span><span class="sxs-lookup"><span data-stu-id="6aba2-162">You can configure Azure AD joined devices for Windows 10 devices.</span></span>


## <a name="hybrid-azure-ad-joined-devices"></a><span data-ttu-id="6aba2-163">Hybride Azure AD die lid zijn van apparaten</span><span class="sxs-lookup"><span data-stu-id="6aba2-163">Hybrid Azure AD joined devices</span></span>

<span data-ttu-id="6aba2-164">Voor meer dan een tien jaar hebben veel organisaties Hallo domain join tootheir lokale Active Directory tooenable gebruikt:</span><span class="sxs-lookup"><span data-stu-id="6aba2-164">For more than a decade, many organizations have used hello domain join tootheir on-premises Active Directory tooenable:</span></span>

- <span data-ttu-id="6aba2-165">IT-afdelingen toomanage werk-apparaten die eigendom zijn van een centrale locatie.</span><span class="sxs-lookup"><span data-stu-id="6aba2-165">IT departments toomanage work-owned devices from a central location.</span></span>

- <span data-ttu-id="6aba2-166">Gebruikers toosign in tootheir apparaten met hun Active Directory werk- of schoolaccounts.</span><span class="sxs-lookup"><span data-stu-id="6aba2-166">Users toosign in tootheir devices with their Active Directory work or school accounts.</span></span> 

<span data-ttu-id="6aba2-167">Normaal gesproken organisaties met een lokale footprint afhankelijk zijn van installatiekopieën van de methoden tooprovision apparaten en kunnen ze vaak gebruiken **System Center Configuration Manager (SCCM)** of **Groepsbeleid (GP)** toomanage ze.</span><span class="sxs-lookup"><span data-stu-id="6aba2-167">Typically, organizations with an on-premises footprint rely on imaging methods tooprovision devices, and they often use **System Center Configuration Manager (SCCM)** or **group policy (GP)** toomanage them.</span></span>

<span data-ttu-id="6aba2-168">Als uw omgeving een on-premises AD-footprint en ook voordeel van het Hallo-mogelijkheden van Azure Active Directory, kunt u hybride Azure AD die lid zijn van apparaten implementeren.</span><span class="sxs-lookup"><span data-stu-id="6aba2-168">If your environment has an on-premises AD footprint and you also want benefit from hello capabilities provided by Azure Active Directory, you can implement hybrid Azure AD joined devices.</span></span> <span data-ttu-id="6aba2-169">Dit zijn apparaten die beide zijn, gekoppelde tooyour lokale Active Directory en uw Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="6aba2-169">These are devices that are both, joined tooyour on-premises Active Directory and your Azure Active Directory.</span></span>

![Azure AD ingeschreven apparaten](./media/device-management-introduction/01.png)


<span data-ttu-id="6aba2-171">Gebruik Azure AD hybride die lid zijn van apparaten als:</span><span class="sxs-lookup"><span data-stu-id="6aba2-171">You should use Azure AD hybrid joined devices if:</span></span>

- <span data-ttu-id="6aba2-172">U hebt Win32-apps geïmplementeerde toothese apparaten die gebruikmaken van NTLM / Kerberos.</span><span class="sxs-lookup"><span data-stu-id="6aba2-172">You have Win32 apps deployed toothese devices that use NTLM / Kerberos.</span></span>

- <span data-ttu-id="6aba2-173">Gewenste GP of SCCM / DCM toomanage apparaten.</span><span class="sxs-lookup"><span data-stu-id="6aba2-173">You require GP or SCCM / DCM toomanage devices.</span></span>

- <span data-ttu-id="6aba2-174">U wilt dat toocontinue toouse imaging oplossingen tooconfigure apparaten voor uw werknemers.</span><span class="sxs-lookup"><span data-stu-id="6aba2-174">You want toocontinue toouse imaging solutions tooconfigure devices for your employees.</span></span>

<span data-ttu-id="6aba2-175">U kunt configureren hybride Azure AD die lid zijn van apparaten voor Windows 10 en downlevel-apparaten, zoals Windows 8 en Windows 7.</span><span class="sxs-lookup"><span data-stu-id="6aba2-175">You can configure Hybrid Azure AD joined devices for Windows 10 and down-level devices such as Windows 8 and Windows 7.</span></span>

## <a name="summary"></a><span data-ttu-id="6aba2-176">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="6aba2-176">Summary</span></span>

<span data-ttu-id="6aba2-177">Met Apparaatbeheer in Azure AD, kunt u het volgende doen:</span><span class="sxs-lookup"><span data-stu-id="6aba2-177">With device management in Azure AD, you can:</span></span> 

- <span data-ttu-id="6aba2-178">Hallo vereenvoudigen van apparaten meebrengen onder het Hallo-beheer van Azure AD</span><span class="sxs-lookup"><span data-stu-id="6aba2-178">Simplify hello process of bringing devices under hello control of Azure AD</span></span>

- <span data-ttu-id="6aba2-179">Uw gebruikers voorzien van een eenvoudig toouse toegang tooyour organisatie cloud-gebaseerde bronnen</span><span class="sxs-lookup"><span data-stu-id="6aba2-179">Provide your users with an easy toouse access tooyour organization’s cloud-based resources</span></span>

<span data-ttu-id="6aba2-180">Als een regel van een miniatuur, moet u het volgende gebruiken:</span><span class="sxs-lookup"><span data-stu-id="6aba2-180">As a rule of a thumb, you should use:</span></span>

- <span data-ttu-id="6aba2-181">Azure AD geregistreerde apparaten voor persoonlijke apparaten</span><span class="sxs-lookup"><span data-stu-id="6aba2-181">Azure AD registered devices for personal devices</span></span>

- <span data-ttu-id="6aba2-182">Azure AD die lid zijn van apparaten voor apparaten die niet lid tooan on-premises AD dat</span><span class="sxs-lookup"><span data-stu-id="6aba2-182">Azure AD joined devices for devices that are not joined tooan on-premises AD</span></span> 

- <span data-ttu-id="6aba2-183">Hybride Azure AD die lid zijn van apparaten voor apparaten die zijn gekoppeld tooan on-premises AD dat</span><span class="sxs-lookup"><span data-stu-id="6aba2-183">Hybrid Azure AD joined devices for devices that are joined tooan on-premises AD</span></span>     




## <a name="next-steps"></a><span data-ttu-id="6aba2-184">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="6aba2-184">Next steps</span></span>

- <span data-ttu-id="6aba2-185">een overzicht van hoe toomanage apparaat in Azure portal, Zie Hallo tooget [apparaten beheert met hello Azure-portal](device-management-azure-portal.md)</span><span class="sxs-lookup"><span data-stu-id="6aba2-185">tooget an overview of how toomanage device in hello Azure portal, see [managing devices using hello Azure portal](device-management-azure-portal.md)</span></span>

- <span data-ttu-id="6aba2-186">toolearn meer informatie over voorwaardelijke toegang op basis van apparaten, Zie [Azure Active Directory-beleid voor voorwaardelijke toegang op basis van apparaten configureren](active-directory-conditional-access-policy-connected-applications.md).</span><span class="sxs-lookup"><span data-stu-id="6aba2-186">toolearn more about device-based conditional access, see [configure Azure Active Directory device-based conditional access policies](active-directory-conditional-access-policy-connected-applications.md).</span></span>

- <span data-ttu-id="6aba2-187">toosetup hybride Azure AD die lid zijn van apparaten, Zie [hoe tooconfigure hybride Azure Active Directory apparaten samengevoegd](device-management-hybrid-azuread-joined-devices-setup.md).</span><span class="sxs-lookup"><span data-stu-id="6aba2-187">toosetup hybrid Azure AD joined devices, see [how tooconfigure hybrid Azure Active Directory joined devices](device-management-hybrid-azuread-joined-devices-setup.md).</span></span>



---
title: aaaManaging apparaten met behulp van Azure portal - Hallo preview | Microsoft Docs
description: Meer informatie over hoe toouse hello Azure portal toomanage apparaten.
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
ms.openlocfilehash: a39d14e4ce8bb79f0223a9de40d5f1259a869927
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="managing-devices-using-hello-azure-portal---preview"></a><span data-ttu-id="2ca22-103">Apparaten beheert met Azure-portal Hallo - voorbeeld</span><span class="sxs-lookup"><span data-stu-id="2ca22-103">Managing devices using hello Azure portal - preview</span></span>

>[!NOTE]
><span data-ttu-id="2ca22-104">Deze mogelijkheid is momenteel in de openbare preview.</span><span class="sxs-lookup"><span data-stu-id="2ca22-104">This capability currently is in public preview.</span></span> <span data-ttu-id="2ca22-105">Toorevert worden voorbereid op of verwijder eventuele wijzigingen.</span><span class="sxs-lookup"><span data-stu-id="2ca22-105">Be prepared toorevert or remove any changes.</span></span> <span data-ttu-id="2ca22-106">Hallo-functie is beschikbaar in een abonnement voor Azure Active Directory (Azure AD) tijdens de openbare preview.</span><span class="sxs-lookup"><span data-stu-id="2ca22-106">hello feature is available in any Azure Active Directory (Azure AD) subscription during public preview.</span></span> <span data-ttu-id="2ca22-107">Wanneer het Hallo-functie in het algemeen beschikbaar wordt, mogelijk bepaalde aspecten van de functie Hallo echter een Azure Active Directory premium-abonnement nodig.</span><span class="sxs-lookup"><span data-stu-id="2ca22-107">However, when hello feature becomes generally available, some aspects of hello feature might require an Azure Active Directory premium subscription.</span></span>


<span data-ttu-id="2ca22-108">Met Apparaatbeheer in Azure Active Directory (Azure AD), kunt u ervoor zorgen dat uw gebruikers toegang hebben tot de bronnen vanaf apparaten die voldoen aan uw standaarden voor beveiliging en naleving.</span><span class="sxs-lookup"><span data-stu-id="2ca22-108">With device management in Azure Active Directory (Azure AD), you can ensure that your users are accessing your resources from devices that meet your standards for security and compliance.</span></span> 

<span data-ttu-id="2ca22-109">Dit onderwerp:</span><span class="sxs-lookup"><span data-stu-id="2ca22-109">This topic:</span></span>

- <span data-ttu-id="2ca22-110">Wordt ervan uitgegaan dat u bekend met Hallo bent [inleiding toodevice management in Azure Active Directory](device-management-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="2ca22-110">Assumes that you are familiar with hello [introduction toodevice management in Azure Active Directory](device-management-introduction.md)</span></span>

- <span data-ttu-id="2ca22-111">Biedt u informatie over het beheren van uw apparaten met behulp van Azure-portal Hallo</span><span class="sxs-lookup"><span data-stu-id="2ca22-111">Provides you with information about managing your devices using hello Azure portal</span></span>


<span data-ttu-id="2ca22-112">toomanage apparaten in hello Azure-portal, moet u tooclick **apparaten** in Hallo **beheren** sectie Hallo Hallo **Azure Active Directory** blade.</span><span class="sxs-lookup"><span data-stu-id="2ca22-112">toomanage devices in hello Azure portal, you need tooclick **Devices** in hello **Manage** section of hello hello **Azure Active Directory** blade.</span></span>

![Een apparaat met Intune beheren](./media/device-management-azure-portal/11.png)




## <a name="configure-device-settings"></a><span data-ttu-id="2ca22-114">Apparaatinstellingen configureren</span><span class="sxs-lookup"><span data-stu-id="2ca22-114">Configure device settings</span></span>

<span data-ttu-id="2ca22-115">uw apparaten met behulp van hello Azure-portal, moeten toobe toomanage ingeschreven of die lid zijn van tooAzure AD.</span><span class="sxs-lookup"><span data-stu-id="2ca22-115">toomanage your devices using hello Azure portal, they need toobe either registered or joined tooAzure AD.</span></span> <span data-ttu-id="2ca22-116">Als beheerder, kunt u aanpassen Hallo proces van registreren en door apparaten te koppelen door het Hallo-apparaatinstellingen configureren.</span><span class="sxs-lookup"><span data-stu-id="2ca22-116">As an administrator, you can fine-tune hello process of registering and joining devices by configuring hello device settings.</span></span>

![Een apparaat met Intune beheren](./media/device-management-azure-portal/22.png)


<span data-ttu-id="2ca22-118">blade Hallo apparaat-instellingen kunt u tooconfigure:</span><span class="sxs-lookup"><span data-stu-id="2ca22-118">hello device settings blade enables you tooconfigure:</span></span>

- <span data-ttu-id="2ca22-119">**Gebruikers kunnen apparaten tooAzure AD join** - deze instellingen kunt u tooselect Hallo gebruikers die deel kunnen nemen aan apparaten tooAzure AD.</span><span class="sxs-lookup"><span data-stu-id="2ca22-119">**Users may join devices tooAzure AD** - This settings enables you tooselect hello users who can join devices tooAzure AD.</span></span> <span data-ttu-id="2ca22-120">Hallo standaardwaarde is **alle**.</span><span class="sxs-lookup"><span data-stu-id="2ca22-120">hello default is **All**.</span></span>

- <span data-ttu-id="2ca22-121">**Aanvullende lokale beheerders op Azure AD die lid zijn van de apparaten** -kunt u Hallo-gebruikers die lokale beheerdersrechten op een apparaat krijgen.</span><span class="sxs-lookup"><span data-stu-id="2ca22-121">**Additional local administrators on Azure AD joined devices** - You can select hello users that are granted local administrator rights on a device.</span></span> <span data-ttu-id="2ca22-122">Gebruikers die zijn toegevoegd, worden toegevoegd toohello *Apparaatbeheerders* rol in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2ca22-122">Users added here are added toohello *Device Administrators* role in Azure AD.</span></span> <span data-ttu-id="2ca22-123">Globale beheerders in Azure AD en eigenaren van de apparaten zijn lokale beheerdersrechten standaard toegekend.</span><span class="sxs-lookup"><span data-stu-id="2ca22-123">Global administrators in Azure AD and device owners are granted local administrator rights by default.</span></span> <span data-ttu-id="2ca22-124">Deze optie is een premium edition-functie beschikbaar via producten zoals Azure AD Premium of Enterprise Mobility Suite (EMS) Hallo.</span><span class="sxs-lookup"><span data-stu-id="2ca22-124">This option is a premium edition capability available through products such as Azure AD Premium or hello Enterprise Mobility Suite (EMS).</span></span> 

- <span data-ttu-id="2ca22-125">**Gebruikers kunnen hun apparaten registreren met Azure AD** -moet u deze instelling tooallow apparaten toobe geregistreerd in Azure AD tooconfigure.</span><span class="sxs-lookup"><span data-stu-id="2ca22-125">**Users may register their devices with Azure AD** - You need tooconfigure this setting tooallow devices toobe registered with Azure AD.</span></span> <span data-ttu-id="2ca22-126">Als u selecteert **geen**, apparaten zijn niet toegestaan tooregister wanneer ze niet Azure AD zijn toegevoegd of hybride die lid zijn van Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2ca22-126">If you select **None**, devices are not allowed tooregister when they are not Azure AD joined or hybrid Azure AD joined.</span></span> <span data-ttu-id="2ca22-127">Registratie bij Microsoft Intune of Mobile Device Management (MDM) voor Office 365 moet worden geregistreerd.</span><span class="sxs-lookup"><span data-stu-id="2ca22-127">Enrollment with Microsoft Intune or Mobile Device Management (MDM) for Office 365 requires registration.</span></span> <span data-ttu-id="2ca22-128">Als u een van deze services hebt geconfigureerd **alle** is geselecteerd en **** is niet beschikbaar...</span><span class="sxs-lookup"><span data-stu-id="2ca22-128">If you have configured either of these services, **ALL** is selected and **NONE** is not available..</span></span>

- <span data-ttu-id="2ca22-129">**Multi-factor Auth toojoin apparaten vereisen** -kunt u kiezen of gebruikers zijn vereiste tooprovide een verificatie met tweede factor toojoin hun apparaat tooAzure AD.</span><span class="sxs-lookup"><span data-stu-id="2ca22-129">**Require Multi-Factor Auth toojoin devices** - You can choose whether users are required tooprovide a second authentication factor toojoin their device tooAzure AD.</span></span> <span data-ttu-id="2ca22-130">Hallo standaardwaarde is **Nee**.</span><span class="sxs-lookup"><span data-stu-id="2ca22-130">hello default is **No**.</span></span> <span data-ttu-id="2ca22-131">Het is raadzaam om meervoudige verificatie vereisen wanneer een apparaat wordt geregistreerd.</span><span class="sxs-lookup"><span data-stu-id="2ca22-131">We recommend requiring multi-factor authentication when registering a device.</span></span> <span data-ttu-id="2ca22-132">Voordat u multi-factor authentication voor deze service inschakelt, moet u ervoor zorgen dat multi-factor authentication-server is geconfigureerd voor het Hallo-gebruikers die hun apparaten registreren.</span><span class="sxs-lookup"><span data-stu-id="2ca22-132">Before you enable multi-factor authentication for this service, you must ensure that multi-factor authentication is configured for hello users that register their devices.</span></span> <span data-ttu-id="2ca22-133">Zie voor meer informatie over andere Azure multi-factor authentication-services [aan de slag met Azure multi-factor authentication](../multi-factor-authentication/multi-factor-authentication-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="2ca22-133">For more information on different Azure multi-factor authentication services, see [getting started with Azure multi-factor authentication](../multi-factor-authentication/multi-factor-authentication-get-started.md).</span></span> 

- <span data-ttu-id="2ca22-134">**Maximum aantal apparaten** -deze instelling kunt u tooselect Hallo maximum aantal apparaten dat een gebruiker in Azure AD hebben kan.</span><span class="sxs-lookup"><span data-stu-id="2ca22-134">**Maximum number of devices** - This setting enables you tooselect hello maximum number of devices that a user can have in Azure AD.</span></span> <span data-ttu-id="2ca22-135">Als een gebruiker dit quotum bereikt, zijn ze niet kunnen tooadd extra apparaten totdat een of meer van de bestaande apparaten Hallo worden verwijderd.</span><span class="sxs-lookup"><span data-stu-id="2ca22-135">If a user reaches this quota, they are not be able tooadd additional devices until one or more of hello existing devices are removed.</span></span> <span data-ttu-id="2ca22-136">Hallo apparaat aanhalingsteken worden geteld voor alle apparaten die Azure AD zijn toegevoegd of Azure AD vandaag geregistreerd.</span><span class="sxs-lookup"><span data-stu-id="2ca22-136">hello device quote is counted for all devices that are either Azure AD joined or Azure AD registered today.</span></span> <span data-ttu-id="2ca22-137">de standaardwaarde Hallo is **20**.</span><span class="sxs-lookup"><span data-stu-id="2ca22-137">hello default value is **20**.</span></span>

- <span data-ttu-id="2ca22-138">**Gebruikers kunnen instellingen en app-gegevens synchroniseren via apparaten** -, deze instelling is standaard ingesteld te****.</span><span class="sxs-lookup"><span data-stu-id="2ca22-138">**Users may sync settings and app data across devices** - By default, this setting is set too**NONE**.</span></span> <span data-ttu-id="2ca22-139">Specifieke gebruikers of groepen of alle selecteren die u kan de instellingen en toosync van app-gegevens van de gebruiker Hallo over hun Windows 10-apparaten.</span><span class="sxs-lookup"><span data-stu-id="2ca22-139">Selecting specific users or groups or ALL allows hello user’s settings and app data toosync across their Windows 10 devices.</span></span> <span data-ttu-id="2ca22-140">Meer informatie over de werking van synchronisatie in Windows 10.</span><span class="sxs-lookup"><span data-stu-id="2ca22-140">Learn more on how sync works in Windows 10.</span></span>
<span data-ttu-id="2ca22-141">Deze optie is een premium-functie beschikbaar via producten zoals Azure AD Premium of Enterprise Mobility Suite (EMS) Hallo.</span><span class="sxs-lookup"><span data-stu-id="2ca22-141">This option is a premium capability available through products such as Azure AD Premium or hello Enterprise Mobility Suite (EMS).</span></span>
 
    ![Een apparaat met Intune beheren](./media/device-management-azure-portal/21.png)




## <a name="locate-devices"></a><span data-ttu-id="2ca22-143">Apparaten zoeken</span><span class="sxs-lookup"><span data-stu-id="2ca22-143">Locate devices</span></span>

<span data-ttu-id="2ca22-144">Als een beheerder hebt in hello Azure-portal u twee opties toolocate geregistreerd en die lid zijn van apparaten:</span><span class="sxs-lookup"><span data-stu-id="2ca22-144">As an administrator, in hello Azure portal, you have two options toolocate registered and joined devices:</span></span>

- <span data-ttu-id="2ca22-145">**Alle apparaten** in Hallo **beheren** sectie Hallo **apparaten** blade</span><span class="sxs-lookup"><span data-stu-id="2ca22-145">**All devices** in hello **Manage** section of hello **Devices** blade</span></span>  

    ![Alle apparaten](./media/device-management-azure-portal/41.png)


- <span data-ttu-id="2ca22-147">**Apparaten** in Hallo **beheren** gedeelte van een **gebruiker** blade</span><span class="sxs-lookup"><span data-stu-id="2ca22-147">**Devices** in hello **Manage** section of a **User** blade</span></span>
 
    ![Alle apparaten](./media/device-management-azure-portal/43.png)



<span data-ttu-id="2ca22-149">Met beide opties, kun je tooa weergeven die:</span><span class="sxs-lookup"><span data-stu-id="2ca22-149">With both options, you can get tooa view that:</span></span>


- <span data-ttu-id="2ca22-150">Hiermee kunt u toosearch voor apparaten met de weergavenaam Hallo als filter.</span><span class="sxs-lookup"><span data-stu-id="2ca22-150">Enables you toosearch for devices using hello display name as filter.</span></span>

- <span data-ttu-id="2ca22-151">Biedt u gedetailleerd overzicht van geregistreerde en gekoppelde apparaten</span><span class="sxs-lookup"><span data-stu-id="2ca22-151">Provides you with detailed overview of registered and joined devices</span></span>

- <span data-ttu-id="2ca22-152">Hiermee kunt u tooperform algemene taken</span><span class="sxs-lookup"><span data-stu-id="2ca22-152">Enables you tooperform common device management tasks</span></span>
   

![Alle apparaten](./media/device-management-azure-portal/51.png)


## <a name="device-management-tasks"></a><span data-ttu-id="2ca22-154">Taken voor het beheer van apparaten</span><span class="sxs-lookup"><span data-stu-id="2ca22-154">Device management tasks</span></span>

<span data-ttu-id="2ca22-155">Als beheerder, kunt u beheren Hallo ingeschreven of die lid zijn van apparaten.</span><span class="sxs-lookup"><span data-stu-id="2ca22-155">As an administrator, you can manage hello registered or joined devices.</span></span> <span data-ttu-id="2ca22-156">Deze sectie vindt u informatie over algemene taken.</span><span class="sxs-lookup"><span data-stu-id="2ca22-156">This section provides you with information about common device management tasks.</span></span>


<span data-ttu-id="2ca22-157">**Een apparaat met Intune beheren** -als u een Intune-beheerder bent, kunt u beheren met apparaten die zijn gemarkeerd als **Microsoft Intune**.</span><span class="sxs-lookup"><span data-stu-id="2ca22-157">**Manage an Intune device** - If you are an Intune administrator, you can manage devices marked as **Microsoft Intune**.</span></span> <span data-ttu-id="2ca22-158">Een beheerder kan aanvullende apparaat zien</span><span class="sxs-lookup"><span data-stu-id="2ca22-158">An administrator can see additional device</span></span> 

![Een apparaat met Intune beheren](./media/device-management-azure-portal/31.png)


<span data-ttu-id="2ca22-160">**Inschakelen / uitschakelen van een Azure AD-apparaat**</span><span class="sxs-lookup"><span data-stu-id="2ca22-160">**Enable / disable an Azure AD device**</span></span>

<span data-ttu-id="2ca22-161">tooenable of een apparaat uitschakelen, moet u een globale beheerder toobe in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2ca22-161">tooenable or disable a device, you need toobe a global administrator in Azure  AD.</span></span> <span data-ttu-id="2ca22-162">Als u een apparaat wordt voorkomen dat een apparaat toegang tot uw Azure AD-resources.</span><span class="sxs-lookup"><span data-stu-id="2ca22-162">Disabling a device prevents a device from accessing your Azure AD resources.</span></span>  <span data-ttu-id="2ca22-163">toodisable Hallo-apparaat, kunt u klikken op *...*</span><span class="sxs-lookup"><span data-stu-id="2ca22-163">toodisable hello device, you can either click *…*</span></span> <span data-ttu-id="2ca22-164">Klik op Hallo-apparaat voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="2ca22-164">click hello device for additional details.</span></span>

 
![Een apparaat met Intune beheren](./media/device-management-azure-portal/33.png)

<span data-ttu-id="2ca22-166">Als u een apparaat wijzigt Hallo-status in Hallo **ingeschakeld** kolom te**Nee**.</span><span class="sxs-lookup"><span data-stu-id="2ca22-166">Disabling a device changes hello state in hello **ENABLED** column too**No**.</span></span>

![Een apparaat uitschakelen](./media/device-management-azure-portal/32.png)


<span data-ttu-id="2ca22-168">**Een Azure AD-apparaat verwijderen** -toodelete een apparaat, moet u een globale beheerder toobe in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2ca22-168">**Delete an Azure AD device** - toodelete a device, you need toobe a global administrator in Azure AD.</span></span>  
<span data-ttu-id="2ca22-169">Een apparaat verwijderen:</span><span class="sxs-lookup"><span data-stu-id="2ca22-169">Deleting a device:</span></span>
 
- <span data-ttu-id="2ca22-170">Voorkomen dat een apparaat toegang tot uw Azure AD-resources</span><span class="sxs-lookup"><span data-stu-id="2ca22-170">Prevents a device from accessing your Azure AD resources</span></span> 

- <span data-ttu-id="2ca22-171">Hiermee verwijdert u alle gegevens die aangesloten toohello van het apparaat, bijvoorbeeld zijn, BitLocker-sleutels voor Windows-apparaten</span><span class="sxs-lookup"><span data-stu-id="2ca22-171">Removes all details that are attached toohello device, for example, BitLocker keys for Windows devices</span></span>  

- <span data-ttu-id="2ca22-172">Hiermee geeft u een niet-herstelbare activiteit en wordt niet aanbevolen, tenzij deze vereist is</span><span class="sxs-lookup"><span data-stu-id="2ca22-172">Represents a non-recoverable activity and is not recommended unless it is required</span></span>

<span data-ttu-id="2ca22-173">Als een apparaat wordt beheerd door een andere instantie voor beheer van (bijvoorbeeld Microsoft Intune), zorg dat het Hallo-apparaat is gewist / buiten gebruik gesteld voordat u Hallo-apparaat verwijdert in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2ca22-173">If a device is managed by another management authority (e.g. Microsoft Intune), please make sure that hello device has been wiped / retired before deleting hello device in Azure AD.</span></span>

<span data-ttu-id="2ca22-174">U kunt ook selecteren '...'</span><span class="sxs-lookup"><span data-stu-id="2ca22-174">You can either select “…”</span></span> <span data-ttu-id="2ca22-175">toodelete hello apparaat of klik op het Hallo-apparaat voor aanvullende informatie</span><span class="sxs-lookup"><span data-stu-id="2ca22-175">toodelete hello device or click on hello device for additional details</span></span>
 
![Een apparaat verwijderen](./media/device-management-azure-portal/34.png)


<span data-ttu-id="2ca22-177">**Weergeven of kopiëren van apparaat-ID** -kunt u een apparaat-ID tooverify Hallo apparaat-ID details op Hallo-apparaat of met behulp van PowerShell tijdens het oplossen van problemen.</span><span class="sxs-lookup"><span data-stu-id="2ca22-177">**View or copy device ID** - You can use a device ID tooverify hello device ID details on hello device or using PowerShell during troubleshooting.</span></span> <span data-ttu-id="2ca22-178">tooaccess Hallo kopie optie, klikt u op Hallo-apparaat.</span><span class="sxs-lookup"><span data-stu-id="2ca22-178">tooaccess hello copy option, click hello device.</span></span>

![Een apparaat-ID weergeven](./media/device-management-azure-portal/35.png)
  

<span data-ttu-id="2ca22-180">**Weergeven of kopiëren van BitLocker-sleutels** -als u beheerder bent, u bekijken kunt en kopiëren Hallo BitLocker-sleutels toohelp gebruikers toorecover hun versleutelde station.</span><span class="sxs-lookup"><span data-stu-id="2ca22-180">**View or copy BitLocker keys** - If you are an administrator, you can view and copy hello BitLocker keys toohelp users toorecover their encrypted drive.</span></span> <span data-ttu-id="2ca22-181">Deze sleutels zijn alleen beschikbaar voor Windows-apparaten die zijn versleuteld en hun sleutels hebt opgeslagen in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2ca22-181">These keys are only available for Windows devices that are encrypted and have their keys stored in Azure AD.</span></span> <span data-ttu-id="2ca22-182">Bij het openen van de details van Hallo-apparaat, kunt u deze sleutels kopiëren.</span><span class="sxs-lookup"><span data-stu-id="2ca22-182">You can copy these keys when accessing details of hello device.</span></span>
 
![BitLocker-sleutels weergeven](./media/device-management-azure-portal/36.png)



## <a name="audit-logs"></a><span data-ttu-id="2ca22-184">Controlelogboeken</span><span class="sxs-lookup"><span data-stu-id="2ca22-184">Audit logs</span></span>


<span data-ttu-id="2ca22-185">Hallo apparaat activiteiten zijn beschikbaar via Hallo activiteitenlogboeken.</span><span class="sxs-lookup"><span data-stu-id="2ca22-185">hello device activities are available through hello activity logs.</span></span> <span data-ttu-id="2ca22-186">Dit omvat activiteiten die zijn geactiveerd door Hallo device registration-service of door Hallo gebruiker:</span><span class="sxs-lookup"><span data-stu-id="2ca22-186">This includes activities triggered by hello device registration service or by hello user:</span></span>

- <span data-ttu-id="2ca22-187">Maken van het apparaat en het toevoegen van eigenaars/gebruikers op Hallo-apparaat</span><span class="sxs-lookup"><span data-stu-id="2ca22-187">Device creation and adding owners/users on hello device</span></span>

- <span data-ttu-id="2ca22-188">Wijzigingen toodevice instellingen</span><span class="sxs-lookup"><span data-stu-id="2ca22-188">Changes toodevice settings</span></span>

- <span data-ttu-id="2ca22-189">Apparaatbewerkingen zoals het verwijderen of bijwerken van een apparaat</span><span class="sxs-lookup"><span data-stu-id="2ca22-189">Device operations such as deleting or updating a device</span></span>
 
<span data-ttu-id="2ca22-190">De vermelding punt toohello controle van gegevens is **controlelogboeken** in Hallo **activiteit** sectie Hallo **apparaten* blade.</span><span class="sxs-lookup"><span data-stu-id="2ca22-190">Your entry point toohello auditing data is **Audit logs** in hello **Activity** section of hello **Devices* blade.</span></span>

![Controlelogboeken](./media/device-management-azure-portal/61.png)


<span data-ttu-id="2ca22-192">Een controlelogboek heeft een standaardlijstweergave die het volgende laat zien:</span><span class="sxs-lookup"><span data-stu-id="2ca22-192">An audit log has a default list view that shows:</span></span>

- <span data-ttu-id="2ca22-193">Hallo-datum en tijd van Hallo-instantie</span><span class="sxs-lookup"><span data-stu-id="2ca22-193">hello date and time of hello occurrence</span></span>

- <span data-ttu-id="2ca22-194">Hallo doelen</span><span class="sxs-lookup"><span data-stu-id="2ca22-194">hello targets</span></span>

- <span data-ttu-id="2ca22-195">Hallo initiator / actor (die) van een activiteit</span><span class="sxs-lookup"><span data-stu-id="2ca22-195">hello initiator / actor (who) of an activity</span></span>

- <span data-ttu-id="2ca22-196">Hallo-activiteit (wat)</span><span class="sxs-lookup"><span data-stu-id="2ca22-196">hello activity (what)</span></span>

![Controlelogboeken](./media/device-management-azure-portal/63.png)

<span data-ttu-id="2ca22-198">U kunt de lijstweergave Hallo aanpassen door te klikken op **kolommen** op Hallo-werkbalk.</span><span class="sxs-lookup"><span data-stu-id="2ca22-198">You can customize hello list view by clicking **Columns** in hello toolbar.</span></span>
 
![Controlelogboeken](./media/device-management-azure-portal/64.png)


<span data-ttu-id="2ca22-200">toonarrow omlaag Hallo tooa gegevensniveau dat geldt voor u, kunt u Hallo audit gegevens filteren met behulp van de volgende velden Hallo gerapporteerd:</span><span class="sxs-lookup"><span data-stu-id="2ca22-200">toonarrow down hello reported data tooa level that works for you, you can filter hello audit data using hello following fields:</span></span>

- <span data-ttu-id="2ca22-201">Catergory</span><span class="sxs-lookup"><span data-stu-id="2ca22-201">Catergory</span></span>
- <span data-ttu-id="2ca22-202">Resourcetype van activiteit</span><span class="sxs-lookup"><span data-stu-id="2ca22-202">Activity resource type</span></span>
- <span data-ttu-id="2ca22-203">Activiteit</span><span class="sxs-lookup"><span data-stu-id="2ca22-203">Activity</span></span>
- <span data-ttu-id="2ca22-204">Datumbereik</span><span class="sxs-lookup"><span data-stu-id="2ca22-204">Date range</span></span>
- <span data-ttu-id="2ca22-205">doel</span><span class="sxs-lookup"><span data-stu-id="2ca22-205">Target</span></span>
- <span data-ttu-id="2ca22-206">Gestart door (Actor)</span><span class="sxs-lookup"><span data-stu-id="2ca22-206">Initiated By (Actor)</span></span>

<span data-ttu-id="2ca22-207">Bovendien toohello filters, u kunt zoeken naar specifieke vermeldingen.</span><span class="sxs-lookup"><span data-stu-id="2ca22-207">In addition toohello filters, you can search for specific entries.</span></span>

![Controlelogboeken](./media/device-management-azure-portal/65.png)

## <a name="next-steps"></a><span data-ttu-id="2ca22-209">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="2ca22-209">Next steps</span></span>

* [<span data-ttu-id="2ca22-210">Inleiding toodevice management in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2ca22-210">Introduction toodevice management in Azure Active Directory</span></span>](device-management-introduction.md)




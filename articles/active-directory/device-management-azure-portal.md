---
title: Het beheren van apparaten met behulp van de Azure portal - preview | Microsoft Docs
description: Informatie over het gebruik van de Azure-portal om apparaten te beheren.
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
ms.openlocfilehash: 4b46e1627a229b0649d9ccd2550cd28fda9849f8
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="managing-devices-using-the-azure-portal---preview"></a><span data-ttu-id="440c7-103">Het beheren van apparaten met behulp van de Azure portal - preview</span><span class="sxs-lookup"><span data-stu-id="440c7-103">Managing devices using the Azure portal - preview</span></span>

>[!NOTE]
><span data-ttu-id="440c7-104">Deze mogelijkheid is momenteel in de openbare preview.</span><span class="sxs-lookup"><span data-stu-id="440c7-104">This capability currently is in public preview.</span></span> <span data-ttu-id="440c7-105">Wees voorbereid om te herstellen of verwijderen van eventuele wijzigingen.</span><span class="sxs-lookup"><span data-stu-id="440c7-105">Be prepared to revert or remove any changes.</span></span> <span data-ttu-id="440c7-106">De functie is beschikbaar in een abonnement voor Azure Active Directory (Azure AD) tijdens de openbare preview.</span><span class="sxs-lookup"><span data-stu-id="440c7-106">The feature is available in any Azure Active Directory (Azure AD) subscription during public preview.</span></span> <span data-ttu-id="440c7-107">Wanneer de functie algemeen beschikbaar wordt, kunnen sommige aspecten van de functie echter een Azure Active Directory premium-abonnement nodig.</span><span class="sxs-lookup"><span data-stu-id="440c7-107">However, when the feature becomes generally available, some aspects of the feature might require an Azure Active Directory premium subscription.</span></span>


<span data-ttu-id="440c7-108">Met Apparaatbeheer in Azure Active Directory (Azure AD), kunt u ervoor zorgen dat uw gebruikers toegang hebben tot de bronnen vanaf apparaten die voldoen aan uw standaarden voor beveiliging en naleving.</span><span class="sxs-lookup"><span data-stu-id="440c7-108">With device management in Azure Active Directory (Azure AD), you can ensure that your users are accessing your resources from devices that meet your standards for security and compliance.</span></span> 

<span data-ttu-id="440c7-109">Dit onderwerp:</span><span class="sxs-lookup"><span data-stu-id="440c7-109">This topic:</span></span>

- <span data-ttu-id="440c7-110">Wordt ervan uitgegaan dat u bekend met bent de [Inleiding tot beheer van apparaten in Azure Active Directory](device-management-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="440c7-110">Assumes that you are familiar with the [introduction to device management in Azure Active Directory](device-management-introduction.md)</span></span>

- <span data-ttu-id="440c7-111">Biedt u informatie over het beheren van uw apparaten met de Azure portal</span><span class="sxs-lookup"><span data-stu-id="440c7-111">Provides you with information about managing your devices using the Azure portal</span></span>


<span data-ttu-id="440c7-112">Om apparaten te beheren in de Azure portal, moet u op **apparaten** in de **beheren** sectie van de de **Azure Active Directory** blade.</span><span class="sxs-lookup"><span data-stu-id="440c7-112">To manage devices in the Azure portal, you need to click **Devices** in the **Manage** section of the the **Azure Active Directory** blade.</span></span>

![Een apparaat met Intune beheren](./media/device-management-azure-portal/11.png)




## <a name="configure-device-settings"></a><span data-ttu-id="440c7-114">Apparaatinstellingen configureren</span><span class="sxs-lookup"><span data-stu-id="440c7-114">Configure device settings</span></span>

<span data-ttu-id="440c7-115">Voor het beheren van uw apparaten met de Azure portal, moeten deze worden geregistreerd of toegevoegd aan Azure AD.</span><span class="sxs-lookup"><span data-stu-id="440c7-115">To manage your devices using the Azure portal, they need to be either registered or joined to Azure AD.</span></span> <span data-ttu-id="440c7-116">Als beheerder, kunt u het proces van registreren en door apparaten te koppelen door het configureren van de instellingen aanpassen.</span><span class="sxs-lookup"><span data-stu-id="440c7-116">As an administrator, you can fine-tune the process of registering and joining devices by configuring the device settings.</span></span>

![Een apparaat met Intune beheren](./media/device-management-azure-portal/22.png)


<span data-ttu-id="440c7-118">De apparaat-instellingenblade kunt u configureren:</span><span class="sxs-lookup"><span data-stu-id="440c7-118">The device settings blade enables you to configure:</span></span>

- <span data-ttu-id="440c7-119">**Gebruikers kunnen apparaten te koppelen aan Azure AD** - deze instellingen kunt u selecteren welke gebruikers apparaten met Azure AD verbinden kunnen.</span><span class="sxs-lookup"><span data-stu-id="440c7-119">**Users may join devices to Azure AD** - This settings enables you to select the users who can join devices to Azure AD.</span></span> <span data-ttu-id="440c7-120">De standaardwaarde is **alle**.</span><span class="sxs-lookup"><span data-stu-id="440c7-120">The default is **All**.</span></span>

- <span data-ttu-id="440c7-121">**Aanvullende lokale beheerders op Azure AD die lid zijn van de apparaten** -kunt u de gebruikers die lokale beheerdersrechten op een apparaat worden verleend.</span><span class="sxs-lookup"><span data-stu-id="440c7-121">**Additional local administrators on Azure AD joined devices** - You can select the users that are granted local administrator rights on a device.</span></span> <span data-ttu-id="440c7-122">Gebruikers die zijn toegevoegd, worden toegevoegd aan de *Apparaatbeheerders* rol in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="440c7-122">Users added here are added to the *Device Administrators* role in Azure AD.</span></span> <span data-ttu-id="440c7-123">Globale beheerders in Azure AD en eigenaren van de apparaten zijn lokale beheerdersrechten standaard toegekend.</span><span class="sxs-lookup"><span data-stu-id="440c7-123">Global administrators in Azure AD and device owners are granted local administrator rights by default.</span></span> <span data-ttu-id="440c7-124">Deze optie is een premium edition-functie beschikbaar via producten zoals Azure AD Premium of Enterprise Mobility Suite (EMS).</span><span class="sxs-lookup"><span data-stu-id="440c7-124">This option is a premium edition capability available through products such as Azure AD Premium or the Enterprise Mobility Suite (EMS).</span></span> 

- <span data-ttu-id="440c7-125">**Gebruikers kunnen hun apparaten registreren met Azure AD** -moet u deze instelling om apparaten worden geregistreerd bij Azure AD te laten configureren.</span><span class="sxs-lookup"><span data-stu-id="440c7-125">**Users may register their devices with Azure AD** - You need to configure this setting to allow devices to be registered with Azure AD.</span></span> <span data-ttu-id="440c7-126">Als u selecteert **geen**, apparaten zijn niet toegestaan om te registreren wanneer ze niet Azure AD zijn toegevoegd of hybride die lid zijn van Azure AD.</span><span class="sxs-lookup"><span data-stu-id="440c7-126">If you select **None**, devices are not allowed to register when they are not Azure AD joined or hybrid Azure AD joined.</span></span> <span data-ttu-id="440c7-127">Registratie bij Microsoft Intune of Mobile Device Management (MDM) voor Office 365 moet worden geregistreerd.</span><span class="sxs-lookup"><span data-stu-id="440c7-127">Enrollment with Microsoft Intune or Mobile Device Management (MDM) for Office 365 requires registration.</span></span> <span data-ttu-id="440c7-128">Als u een van deze services hebt geconfigureerd **alle** is geselecteerd en **** is niet beschikbaar...</span><span class="sxs-lookup"><span data-stu-id="440c7-128">If you have configured either of these services, **ALL** is selected and **NONE** is not available..</span></span>

- <span data-ttu-id="440c7-129">**Multi-factor Authentication om toe te voegen apparaten vereisen** -kunt u kiezen of gebruikers zijn vereist voor een tweede verificatiefactor om hun apparaat toevoegen aan Azure AD.</span><span class="sxs-lookup"><span data-stu-id="440c7-129">**Require Multi-Factor Auth to join devices** - You can choose whether users are required to provide a second authentication factor to join their device to Azure AD.</span></span> <span data-ttu-id="440c7-130">De standaardwaarde is **Nee**.</span><span class="sxs-lookup"><span data-stu-id="440c7-130">The default is **No**.</span></span> <span data-ttu-id="440c7-131">Het is raadzaam om meervoudige verificatie vereisen wanneer een apparaat wordt geregistreerd.</span><span class="sxs-lookup"><span data-stu-id="440c7-131">We recommend requiring multi-factor authentication when registering a device.</span></span> <span data-ttu-id="440c7-132">Voordat u multi-factor authentication voor deze service inschakelt, moet u ervoor zorgen dat multi-factor authentication-server is geconfigureerd voor de gebruikers die hun apparaten registreren.</span><span class="sxs-lookup"><span data-stu-id="440c7-132">Before you enable multi-factor authentication for this service, you must ensure that multi-factor authentication is configured for the users that register their devices.</span></span> <span data-ttu-id="440c7-133">Zie voor meer informatie over andere Azure multi-factor authentication-services [aan de slag met Azure multi-factor authentication](../multi-factor-authentication/multi-factor-authentication-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="440c7-133">For more information on different Azure multi-factor authentication services, see [getting started with Azure multi-factor authentication](../multi-factor-authentication/multi-factor-authentication-get-started.md).</span></span> 

- <span data-ttu-id="440c7-134">**Maximum aantal apparaten** -deze instelling schakelt u het maximum aantal apparaten dat een gebruiker in Azure AD hebben kan selecteren.</span><span class="sxs-lookup"><span data-stu-id="440c7-134">**Maximum number of devices** - This setting enables you to select the maximum number of devices that a user can have in Azure AD.</span></span> <span data-ttu-id="440c7-135">Als een gebruiker dit quotum bereikt, dat niet meer mogelijk extra apparaten toevoegen totdat een of meer van de bestaande apparaten zijn verwijderd.</span><span class="sxs-lookup"><span data-stu-id="440c7-135">If a user reaches this quota, they are not be able to add additional devices until one or more of the existing devices are removed.</span></span> <span data-ttu-id="440c7-136">De aanhalingstekens van het apparaat wordt beschouwd voor alle apparaten die Azure AD zijn toegevoegd of Azure AD vandaag geregistreerd.</span><span class="sxs-lookup"><span data-stu-id="440c7-136">The device quote is counted for all devices that are either Azure AD joined or Azure AD registered today.</span></span> <span data-ttu-id="440c7-137">De standaardwaarde is **20**.</span><span class="sxs-lookup"><span data-stu-id="440c7-137">The default value is **20**.</span></span>

- <span data-ttu-id="440c7-138">**Gebruikers kunnen instellingen en app-gegevens synchroniseren via apparaten** -deze instelling is standaard ingesteld op ****.</span><span class="sxs-lookup"><span data-stu-id="440c7-138">**Users may sync settings and app data across devices** - By default, this setting is set to **NONE**.</span></span> <span data-ttu-id="440c7-139">Specifieke gebruikers of groepen of alle selecteren die u kunt de gebruiker instellingen en app-gegevens kunnen synchroniseren via hun Windows 10-apparaten.</span><span class="sxs-lookup"><span data-stu-id="440c7-139">Selecting specific users or groups or ALL allows the user’s settings and app data to sync across their Windows 10 devices.</span></span> <span data-ttu-id="440c7-140">Meer informatie over de werking van synchronisatie in Windows 10.</span><span class="sxs-lookup"><span data-stu-id="440c7-140">Learn more on how sync works in Windows 10.</span></span>
<span data-ttu-id="440c7-141">Deze optie is een premium-functie beschikbaar via producten zoals Azure AD Premium of Enterprise Mobility Suite (EMS).</span><span class="sxs-lookup"><span data-stu-id="440c7-141">This option is a premium capability available through products such as Azure AD Premium or the Enterprise Mobility Suite (EMS).</span></span>
 
    ![Een apparaat met Intune beheren](./media/device-management-azure-portal/21.png)




## <a name="locate-devices"></a><span data-ttu-id="440c7-143">Apparaten zoeken</span><span class="sxs-lookup"><span data-stu-id="440c7-143">Locate devices</span></span>

<span data-ttu-id="440c7-144">Als een beheerder hebt in de Azure portal u twee opties geregistreerd en gekoppelde apparaten vinden:</span><span class="sxs-lookup"><span data-stu-id="440c7-144">As an administrator, in the Azure portal, you have two options to locate registered and joined devices:</span></span>

- <span data-ttu-id="440c7-145">**Alle apparaten** in de **beheren** sectie van de **apparaten** blade</span><span class="sxs-lookup"><span data-stu-id="440c7-145">**All devices** in the **Manage** section of the **Devices** blade</span></span>  

    ![Alle apparaten](./media/device-management-azure-portal/41.png)


- <span data-ttu-id="440c7-147">**Apparaten** in de **beheren** gedeelte van een **gebruiker** blade</span><span class="sxs-lookup"><span data-stu-id="440c7-147">**Devices** in the **Manage** section of a **User** blade</span></span>
 
    ![Alle apparaten](./media/device-management-azure-portal/43.png)



<span data-ttu-id="440c7-149">Met beide opties, kun je op een weergave die:</span><span class="sxs-lookup"><span data-stu-id="440c7-149">With both options, you can get to a view that:</span></span>


- <span data-ttu-id="440c7-150">Hiermee kunt u zoeken naar apparaten met behulp van de weergavenaam op die als filter.</span><span class="sxs-lookup"><span data-stu-id="440c7-150">Enables you to search for devices using the display name as filter.</span></span>

- <span data-ttu-id="440c7-151">Biedt u gedetailleerd overzicht van geregistreerde en gekoppelde apparaten</span><span class="sxs-lookup"><span data-stu-id="440c7-151">Provides you with detailed overview of registered and joined devices</span></span>

- <span data-ttu-id="440c7-152">Hiermee kunt u algemene taken uitvoeren</span><span class="sxs-lookup"><span data-stu-id="440c7-152">Enables you to perform common device management tasks</span></span>
   

![Alle apparaten](./media/device-management-azure-portal/51.png)


## <a name="device-management-tasks"></a><span data-ttu-id="440c7-154">Taken voor het beheer van apparaten</span><span class="sxs-lookup"><span data-stu-id="440c7-154">Device management tasks</span></span>

<span data-ttu-id="440c7-155">Als beheerder, kunt u de geregistreerde of gekoppelde apparaten beheren.</span><span class="sxs-lookup"><span data-stu-id="440c7-155">As an administrator, you can manage the registered or joined devices.</span></span> <span data-ttu-id="440c7-156">Deze sectie vindt u informatie over algemene taken.</span><span class="sxs-lookup"><span data-stu-id="440c7-156">This section provides you with information about common device management tasks.</span></span>


<span data-ttu-id="440c7-157">**Een apparaat met Intune beheren** -als u een Intune-beheerder bent, kunt u beheren met apparaten die zijn gemarkeerd als **Microsoft Intune**.</span><span class="sxs-lookup"><span data-stu-id="440c7-157">**Manage an Intune device** - If you are an Intune administrator, you can manage devices marked as **Microsoft Intune**.</span></span> <span data-ttu-id="440c7-158">Een beheerder kan aanvullende apparaat zien</span><span class="sxs-lookup"><span data-stu-id="440c7-158">An administrator can see additional device</span></span> 

![Een apparaat met Intune beheren](./media/device-management-azure-portal/31.png)


<span data-ttu-id="440c7-160">**Inschakelen / uitschakelen van een Azure AD-apparaat**</span><span class="sxs-lookup"><span data-stu-id="440c7-160">**Enable / disable an Azure AD device**</span></span>

<span data-ttu-id="440c7-161">Als u wilt in- of uitschakelen van een apparaat, moet u een globale beheerder in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="440c7-161">To enable or disable a device, you need to be a global administrator in Azure  AD.</span></span> <span data-ttu-id="440c7-162">Als u een apparaat wordt voorkomen dat een apparaat toegang tot uw Azure AD-resources.</span><span class="sxs-lookup"><span data-stu-id="440c7-162">Disabling a device prevents a device from accessing your Azure AD resources.</span></span>  <span data-ttu-id="440c7-163">U kunt u het apparaat uitschakelen door op *...*</span><span class="sxs-lookup"><span data-stu-id="440c7-163">To disable the device, you can either click *…*</span></span> <span data-ttu-id="440c7-164">Klik op het apparaat voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="440c7-164">click the device for additional details.</span></span>

 
![Een apparaat met Intune beheren](./media/device-management-azure-portal/33.png)

<span data-ttu-id="440c7-166">Als u een apparaat wijzigt de status in de **ingeschakeld** kolom **Nee**.</span><span class="sxs-lookup"><span data-stu-id="440c7-166">Disabling a device changes the state in the **ENABLED** column to **No**.</span></span>

![Een apparaat uitschakelen](./media/device-management-azure-portal/32.png)


<span data-ttu-id="440c7-168">**Een Azure AD-apparaat verwijderen** : verwijderen van een apparaat, moet u een globale beheerder in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="440c7-168">**Delete an Azure AD device** - To delete a device, you need to be a global administrator in Azure AD.</span></span>  
<span data-ttu-id="440c7-169">Een apparaat verwijderen:</span><span class="sxs-lookup"><span data-stu-id="440c7-169">Deleting a device:</span></span>
 
- <span data-ttu-id="440c7-170">Voorkomen dat een apparaat toegang tot uw Azure AD-resources</span><span class="sxs-lookup"><span data-stu-id="440c7-170">Prevents a device from accessing your Azure AD resources</span></span> 

- <span data-ttu-id="440c7-171">Hiermee verwijdert u alle gegevens die zijn gekoppeld aan het apparaat, bijvoorbeeld, BitLocker-sleutels voor Windows-apparaten</span><span class="sxs-lookup"><span data-stu-id="440c7-171">Removes all details that are attached to the device, for example, BitLocker keys for Windows devices</span></span>  

- <span data-ttu-id="440c7-172">Hiermee geeft u een niet-herstelbare activiteit en wordt niet aanbevolen, tenzij deze vereist is</span><span class="sxs-lookup"><span data-stu-id="440c7-172">Represents a non-recoverable activity and is not recommended unless it is required</span></span>

<span data-ttu-id="440c7-173">Als een apparaat wordt beheerd door een andere instantie voor beheer van (bijvoorbeeld Microsoft Intune), Controleer of het apparaat gewist / buiten gebruik gesteld voordat het apparaat wordt verwijderd in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="440c7-173">If a device is managed by another management authority (e.g. Microsoft Intune), please make sure that the device has been wiped / retired before deleting the device in Azure AD.</span></span>

<span data-ttu-id="440c7-174">U kunt ook selecteren '...'</span><span class="sxs-lookup"><span data-stu-id="440c7-174">You can either select “…”</span></span> <span data-ttu-id="440c7-175">het apparaat verwijderen of klik op het apparaat voor meer informatie</span><span class="sxs-lookup"><span data-stu-id="440c7-175">to delete the device or click on the device for additional details</span></span>
 
![Een apparaat verwijderen](./media/device-management-azure-portal/34.png)


<span data-ttu-id="440c7-177">**Weergeven of kopiëren van apparaat-ID** -kunt u een apparaat-ID om te controleren of de details van de apparaat-ID op het apparaat of met behulp van PowerShell tijdens het oplossen van problemen.</span><span class="sxs-lookup"><span data-stu-id="440c7-177">**View or copy device ID** - You can use a device ID to verify the device ID details on the device or using PowerShell during troubleshooting.</span></span> <span data-ttu-id="440c7-178">Voor toegang tot de optie kopiëren, klikt u op het apparaat.</span><span class="sxs-lookup"><span data-stu-id="440c7-178">To access the copy option, click the device.</span></span>

![Een apparaat-ID weergeven](./media/device-management-azure-portal/35.png)
  

<span data-ttu-id="440c7-180">**Weergeven of kopiëren van BitLocker-sleutels** -als u een beheerder bent, kunt u bekijken en kopiëren van de BitLocker-sleutels, zodat gebruikers kunnen hun versleutelde station te herstellen.</span><span class="sxs-lookup"><span data-stu-id="440c7-180">**View or copy BitLocker keys** - If you are an administrator, you can view and copy the BitLocker keys to help users to recover their encrypted drive.</span></span> <span data-ttu-id="440c7-181">Deze sleutels zijn alleen beschikbaar voor Windows-apparaten die zijn versleuteld en hun sleutels hebt opgeslagen in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="440c7-181">These keys are only available for Windows devices that are encrypted and have their keys stored in Azure AD.</span></span> <span data-ttu-id="440c7-182">Bij het openen van de details van het apparaat, kunt u deze sleutels kopiëren.</span><span class="sxs-lookup"><span data-stu-id="440c7-182">You can copy these keys when accessing details of the device.</span></span>
 
![BitLocker-sleutels weergeven](./media/device-management-azure-portal/36.png)



## <a name="audit-logs"></a><span data-ttu-id="440c7-184">Controlelogboeken</span><span class="sxs-lookup"><span data-stu-id="440c7-184">Audit logs</span></span>


<span data-ttu-id="440c7-185">De apparaat-activiteiten zijn beschikbaar via de activiteitenlogboeken van de.</span><span class="sxs-lookup"><span data-stu-id="440c7-185">The device activities are available through the activity logs.</span></span> <span data-ttu-id="440c7-186">Dit omvat activiteiten die zijn geactiveerd door de device registratieservice of door de gebruiker:</span><span class="sxs-lookup"><span data-stu-id="440c7-186">This includes activities triggered by the device registration service or by the user:</span></span>

- <span data-ttu-id="440c7-187">Maken van het apparaat en het toevoegen van eigenaars/gebruikers op het apparaat</span><span class="sxs-lookup"><span data-stu-id="440c7-187">Device creation and adding owners/users on the device</span></span>

- <span data-ttu-id="440c7-188">Apparaatinstellingen</span><span class="sxs-lookup"><span data-stu-id="440c7-188">Changes to device settings</span></span>

- <span data-ttu-id="440c7-189">Apparaatbewerkingen zoals het verwijderen of bijwerken van een apparaat</span><span class="sxs-lookup"><span data-stu-id="440c7-189">Device operations such as deleting or updating a device</span></span>
 
<span data-ttu-id="440c7-190">Uw toegangspunt voor de controle gegevens is **controlelogboeken** in de **activiteit** sectie van de **apparaten* blade.</span><span class="sxs-lookup"><span data-stu-id="440c7-190">Your entry point to the auditing data is **Audit logs** in the **Activity** section of the **Devices* blade.</span></span>

![Controlelogboeken](./media/device-management-azure-portal/61.png)


<span data-ttu-id="440c7-192">Een controlelogboek heeft een standaardlijstweergave die het volgende laat zien:</span><span class="sxs-lookup"><span data-stu-id="440c7-192">An audit log has a default list view that shows:</span></span>

- <span data-ttu-id="440c7-193">de datum en tijd van de gebeurtenis</span><span class="sxs-lookup"><span data-stu-id="440c7-193">the date and time of the occurrence</span></span>

- <span data-ttu-id="440c7-194">de doelen</span><span class="sxs-lookup"><span data-stu-id="440c7-194">the targets</span></span>

- <span data-ttu-id="440c7-195">de initiator / actor (die) van een activiteit</span><span class="sxs-lookup"><span data-stu-id="440c7-195">the initiator / actor (who) of an activity</span></span>

- <span data-ttu-id="440c7-196">de activiteit (wat)</span><span class="sxs-lookup"><span data-stu-id="440c7-196">the activity (what)</span></span>

![Controlelogboeken](./media/device-management-azure-portal/63.png)

<span data-ttu-id="440c7-198">U kunt de lijstweergave aanpassen door te klikken op **Kolommen** op de werkbalk.</span><span class="sxs-lookup"><span data-stu-id="440c7-198">You can customize the list view by clicking **Columns** in the toolbar.</span></span>
 
![Controlelogboeken](./media/device-management-azure-portal/64.png)


<span data-ttu-id="440c7-200">Als u de gerapporteerde gegevens wilt beperken tot een niveau dat geschikt is voor u, kunt u de controlegegevens filteren met de volgende velden:</span><span class="sxs-lookup"><span data-stu-id="440c7-200">To narrow down the reported data to a level that works for you, you can filter the audit data using the following fields:</span></span>

- <span data-ttu-id="440c7-201">Catergory</span><span class="sxs-lookup"><span data-stu-id="440c7-201">Catergory</span></span>
- <span data-ttu-id="440c7-202">Resourcetype van activiteit</span><span class="sxs-lookup"><span data-stu-id="440c7-202">Activity resource type</span></span>
- <span data-ttu-id="440c7-203">Activiteit</span><span class="sxs-lookup"><span data-stu-id="440c7-203">Activity</span></span>
- <span data-ttu-id="440c7-204">Datumbereik</span><span class="sxs-lookup"><span data-stu-id="440c7-204">Date range</span></span>
- <span data-ttu-id="440c7-205">doel</span><span class="sxs-lookup"><span data-stu-id="440c7-205">Target</span></span>
- <span data-ttu-id="440c7-206">Gestart door (Actor)</span><span class="sxs-lookup"><span data-stu-id="440c7-206">Initiated By (Actor)</span></span>

<span data-ttu-id="440c7-207">Naast de filters, kunt u zoeken naar specifieke vermeldingen.</span><span class="sxs-lookup"><span data-stu-id="440c7-207">In addition to the filters, you can search for specific entries.</span></span>

![Controlelogboeken](./media/device-management-azure-portal/65.png)

## <a name="next-steps"></a><span data-ttu-id="440c7-209">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="440c7-209">Next steps</span></span>

* [<span data-ttu-id="440c7-210">Inleiding tot beheer van apparaten in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="440c7-210">Introduction to device management in Azure Active Directory</span></span>](device-management-introduction.md)




---
title: aaaActive Directory Federation Services management en aanpassingen met Azure AD Connect | Microsoft Docs
description: AD FS-beheer met Azure AD Connect en aanpassen van AD FS-aanmeldingspagina gebruikerservaring met Azure AD Connect en PowerShell.
keywords: AD FS, ADFS, AD FS-beheer zijn AAD Connect, Connect, aanmelden, AD FS aanpassing, trust, O365, Federatie, relying party herstellen
services: active-directory
documentationcenter: 
author: anandyadavmsft
manager: femila
editor: 
ms.assetid: 2593b6c6-dc3f-46ef-8e02-a8e2dc4e9fb9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 361a2bfd6d7a6993dbe773d6ea039ad1afc6346a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-and-customize-active-directory-federation-services-by-using-azure-ad-connect"></a><span data-ttu-id="0fe3d-104">Beheren en aanpassen van Active Directory Federation Services met behulp van Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="0fe3d-104">Manage and customize Active Directory Federation Services by using Azure AD Connect</span></span>
<span data-ttu-id="0fe3d-105">Dit artikel wordt beschreven hoe toomanage en aanpassen van Active Directory Federation Services (AD FS) met behulp van Azure Active Directory (Azure AD) verbinding maken.</span><span class="sxs-lookup"><span data-stu-id="0fe3d-105">This article describes how toomanage and customize Active Directory Federation Services (AD FS) by using Azure Active Directory (Azure AD) Connect.</span></span> <span data-ttu-id="0fe3d-106">Dit omvat ook andere taken van de AD FS dat u toodo mogelijk nodig heeft voor een volledige configuratie van een AD FS-farm.</span><span class="sxs-lookup"><span data-stu-id="0fe3d-106">It also includes other common AD FS tasks that you might need toodo for a complete configuration of an AD FS farm.</span></span>

| <span data-ttu-id="0fe3d-107">Onderwerp</span><span class="sxs-lookup"><span data-stu-id="0fe3d-107">Topic</span></span> | <span data-ttu-id="0fe3d-108">Er wordt aangegeven</span><span class="sxs-lookup"><span data-stu-id="0fe3d-108">What it covers</span></span> |
|:--- |:--- |
| <span data-ttu-id="0fe3d-109">**Beheren van AD FS**</span><span class="sxs-lookup"><span data-stu-id="0fe3d-109">**Manage AD FS**</span></span> | |
| [<span data-ttu-id="0fe3d-110">Hallo-vertrouwensrelatie repareren</span><span class="sxs-lookup"><span data-stu-id="0fe3d-110">Repair hello trust</span></span>](#repairthetrust) |<span data-ttu-id="0fe3d-111">Hoe toorepair Hallo federatieve vertrouwensrelatie met Office 365.</span><span class="sxs-lookup"><span data-stu-id="0fe3d-111">How toorepair hello federation trust with Office 365.</span></span> |
| [<span data-ttu-id="0fe3d-112">Gefedereerd met Azure AD met behulp van alternatieve aanmeldings-ID</span><span class="sxs-lookup"><span data-stu-id="0fe3d-112">Federate with Azure AD using alternate login ID </span></span>](#alternateid) | <span data-ttu-id="0fe3d-113">Federatie met behulp van alternatieve aanmeldings-ID configureren</span><span class="sxs-lookup"><span data-stu-id="0fe3d-113">Configure federation using alternate login ID</span></span>  |
| [<span data-ttu-id="0fe3d-114">Een AD FS-server toevoegen</span><span class="sxs-lookup"><span data-stu-id="0fe3d-114">Add an AD FS server</span></span>](#addadfsserver) |<span data-ttu-id="0fe3d-115">Hoe tooexpand een AD FS-farm met een extra AD FS-server.</span><span class="sxs-lookup"><span data-stu-id="0fe3d-115">How tooexpand an AD FS farm with an additional AD FS server.</span></span> |
| [<span data-ttu-id="0fe3d-116">Een AD FS Web Application Proxy-server toevoegen</span><span class="sxs-lookup"><span data-stu-id="0fe3d-116">Add an AD FS Web Application Proxy server</span></span>](#addwapserver) |<span data-ttu-id="0fe3d-117">Hoe tooexpand een AD FS-farm met een extra Webtoepassingsproxy (WAP)-server.</span><span class="sxs-lookup"><span data-stu-id="0fe3d-117">How tooexpand an AD FS farm with an additional Web Application Proxy (WAP) server.</span></span> |
| [<span data-ttu-id="0fe3d-118">Een federatieve domein toevoegen</span><span class="sxs-lookup"><span data-stu-id="0fe3d-118">Add a federated domain</span></span>](#addfeddomain) |<span data-ttu-id="0fe3d-119">Hoe tooadd een federatief domein.</span><span class="sxs-lookup"><span data-stu-id="0fe3d-119">How tooadd a federated domain.</span></span> |
| [<span data-ttu-id="0fe3d-120">Hallo SSL-certificaat bijwerken</span><span class="sxs-lookup"><span data-stu-id="0fe3d-120">Update hello SSL certificate</span></span>](active-directory-aadconnectfed-ssl-update.md)| <span data-ttu-id="0fe3d-121">Hoe tooupdate Hallo SSL-certificaat voor een AD FS-farm.</span><span class="sxs-lookup"><span data-stu-id="0fe3d-121">How tooupdate hello SSL certificate for an AD FS farm.</span></span> |
| <span data-ttu-id="0fe3d-122">**Aanpassen van AD FS**</span><span class="sxs-lookup"><span data-stu-id="0fe3d-122">**Customize AD FS**</span></span> | |
| [<span data-ttu-id="0fe3d-123">Een aangepast bedrijfslogo of afbeelding toevoegen</span><span class="sxs-lookup"><span data-stu-id="0fe3d-123">Add a custom company logo or illustration</span></span>](#customlogo) |<span data-ttu-id="0fe3d-124">Hoe toocustomize een AD FS-aanmeldingspagina pagina met een bedrijfslogo en afbeelding.</span><span class="sxs-lookup"><span data-stu-id="0fe3d-124">How toocustomize an AD FS sign-in page with a company logo and illustration.</span></span> |
| [<span data-ttu-id="0fe3d-125">Een beschrijving van de aanmeldingspagina toevoegen</span><span class="sxs-lookup"><span data-stu-id="0fe3d-125">Add a sign-in description</span></span>](#addsignindescription) |<span data-ttu-id="0fe3d-126">Hoe pagina tooadd een aanmeldingspagina beschrijving.</span><span class="sxs-lookup"><span data-stu-id="0fe3d-126">How tooadd a sign-in page description.</span></span> |
| [<span data-ttu-id="0fe3d-127">Wijzigen van de claimregels van AD FS</span><span class="sxs-lookup"><span data-stu-id="0fe3d-127">Modify AD FS claim rules</span></span>](#modclaims) |<span data-ttu-id="0fe3d-128">Hoe toomodify AD FS-claims voor verschillende scenario's met Federatie.</span><span class="sxs-lookup"><span data-stu-id="0fe3d-128">How toomodify AD FS claims for various federation scenarios.</span></span> |

## <a name="manage-ad-fs"></a><span data-ttu-id="0fe3d-129">Beheren van AD FS</span><span class="sxs-lookup"><span data-stu-id="0fe3d-129">Manage AD FS</span></span>
<span data-ttu-id="0fe3d-130">U kunt verschillende AD FS-gerelateerde taken in Azure AD Connect met minimale tussenkomst uitvoeren met behulp van hello Azure AD Connect-wizard.</span><span class="sxs-lookup"><span data-stu-id="0fe3d-130">You can perform various AD FS-related tasks in Azure AD Connect with minimal user intervention by using hello Azure AD Connect wizard.</span></span> <span data-ttu-id="0fe3d-131">Wanneer u klaar bent met het Azure AD Connect door actieve Hallo wizard installeert, kunt u Hallo wizard uitvoeren opnieuw tooperform aanvullende taken.</span><span class="sxs-lookup"><span data-stu-id="0fe3d-131">After you've finished installing Azure AD Connect by running hello wizard, you can run hello wizard again tooperform additional tasks.</span></span>

## <span data-ttu-id="0fe3d-132">Hallo-vertrouwensrelatie repareren<a name=repairthetrust></a></span><span class="sxs-lookup"><span data-stu-id="0fe3d-132">Repair hello trust <a name=repairthetrust></a></span></span>
<span data-ttu-id="0fe3d-133">U kunt Azure AD Connect toocheck Hallo huidige status van Hallo AD FS en Azure AD-vertrouwensrelatie gebruiken en nemen de nodige acties toorepair Hallo vertrouwen.</span><span class="sxs-lookup"><span data-stu-id="0fe3d-133">You can use Azure AD Connect toocheck hello current health of hello AD FS and Azure AD trust and take appropriate actions toorepair hello trust.</span></span> <span data-ttu-id="0fe3d-134">Volg deze stappen toorepair uw Azure AD en AD FS vertrouwen.</span><span class="sxs-lookup"><span data-stu-id="0fe3d-134">Follow these steps toorepair your Azure AD and AD FS trust.</span></span>

1. <span data-ttu-id="0fe3d-135">Selecteer **reparatie AAD en ADFS-vertrouwen** uit Hallo lijst met aanvullende taken.</span><span class="sxs-lookup"><span data-stu-id="0fe3d-135">Select **Repair AAD and ADFS Trust** from hello list of additional tasks.</span></span>
   <span data-ttu-id="0fe3d-136">![Herstellen van AAD- en AD FS vertrouwen](media/active-directory-aadconnect-federation-management/RepairADTrust1.PNG)</span><span class="sxs-lookup"><span data-stu-id="0fe3d-136">![Repair AAD and ADFS Trust](media/active-directory-aadconnect-federation-management/RepairADTrust1.PNG)</span></span>

2. <span data-ttu-id="0fe3d-137">Op Hallo **verbinding tooAzure AD** pagina, Geef uw referenties voor de globale beheerder voor Azure AD en klikt u op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="0fe3d-137">On hello **Connect tooAzure AD** page, provide your global administrator credentials for Azure AD, and click **Next**.</span></span>
   <span data-ttu-id="0fe3d-138">![Verbinding maken met tooAzure AD](media/active-directory-aadconnect-federation-management/RepairADTrust2.PNG)</span><span class="sxs-lookup"><span data-stu-id="0fe3d-138">![Connect tooAzure AD](media/active-directory-aadconnect-federation-management/RepairADTrust2.PNG)</span></span>

3. <span data-ttu-id="0fe3d-139">Op Hallo **RAS-referenties** pagina, voert u Hallo-referenties in voor de domeinbeheerder Hallo.</span><span class="sxs-lookup"><span data-stu-id="0fe3d-139">On hello **Remote access credentials** page, enter hello credentials for hello domain administrator.</span></span>

   ![Referenties voor externe toegang](media/active-directory-aadconnect-federation-management/RepairADTrust3.PNG)

    <span data-ttu-id="0fe3d-141">Nadat u op **volgende**, Azure AD Connect health certificaat controleert en ziet u eventuele problemen.</span><span class="sxs-lookup"><span data-stu-id="0fe3d-141">After you click **Next**, Azure AD Connect checks for certificate health and shows any issues.</span></span>

    ![Status van certificaten](media/active-directory-aadconnect-federation-management/RepairADTrust4.PNG)

    <span data-ttu-id="0fe3d-143">Hallo **gereed tooconfigure** pagina toont Hallo lijst van acties die worden uitgevoerd toorepair Hallo vertrouwen.</span><span class="sxs-lookup"><span data-stu-id="0fe3d-143">hello **Ready tooconfigure** page shows hello list of actions that will be performed toorepair hello trust.</span></span>

    ![Gereed tooconfigure](media/active-directory-aadconnect-federation-management/RepairADTrust5.PNG)

4. <span data-ttu-id="0fe3d-145">Klik op **installeren** toorepair Hallo vertrouwen.</span><span class="sxs-lookup"><span data-stu-id="0fe3d-145">Click **Install** toorepair hello trust.</span></span>

> [!NOTE]
> <span data-ttu-id="0fe3d-146">Azure AD Connect kan alleen herstellen of act op certificaten die zelf-ondertekend zijn.</span><span class="sxs-lookup"><span data-stu-id="0fe3d-146">Azure AD Connect can only repair or act on certificates that are self-signed.</span></span> <span data-ttu-id="0fe3d-147">Azure AD Connect-certificaten van derden niet worden hersteld.</span><span class="sxs-lookup"><span data-stu-id="0fe3d-147">Azure AD Connect can't repair third-party certificates.</span></span>

## <span data-ttu-id="0fe3d-148">Gefedereerd met Azure AD dat gebruikmaakt van AlternateID<a name=alternateid></a></span><span class="sxs-lookup"><span data-stu-id="0fe3d-148">Federate with Azure AD using AlternateID <a name=alternateid></a></span></span>
<span data-ttu-id="0fe3d-149">Het verdient aanbeveling dat Hallo on-premises User Principal Name(UPN) en Hallo cloud principalnaam van gebruiker worden gehouden Hallo dezelfde.</span><span class="sxs-lookup"><span data-stu-id="0fe3d-149">It is recommended that hello on-premises User Principal Name(UPN) and hello cloud User Principal Name are kept hello same.</span></span> <span data-ttu-id="0fe3d-150">Als Hallo lokale UPN gebruikmaakt van een niet-routeerbare domein (bijvoorbeeld)</span><span class="sxs-lookup"><span data-stu-id="0fe3d-150">If hello on-premises UPN uses a non-routable domain (ex.</span></span> <span data-ttu-id="0fe3d-151">Contoso.local) of kan niet worden gewijzigd vanwege toolocal toepassingsafhankelijkheden, wordt aangeraden instellen van de alternatieve aanmeldings-ID.</span><span class="sxs-lookup"><span data-stu-id="0fe3d-151">Contoso.local) or cannot be changed due toolocal application dependencies, we recommend setting up alternate login ID.</span></span> <span data-ttu-id="0fe3d-152">Alternatieve aanmeldings-ID kunt u een aanmelden waar gebruikers zich kunnen aanmelden met een kenmerk dan de UPN, zoals mail tooconfigure.</span><span class="sxs-lookup"><span data-stu-id="0fe3d-152">Alternate login ID allows you tooconfigure a sign-in experience where users can sign in with an attribute other than their UPN, such as mail.</span></span> <span data-ttu-id="0fe3d-153">Hallo de keuze voor principalnaam van gebruiker in Azure AD Connect standaardwaarden toohello userPrincipalName kenmerk in Active Directory.</span><span class="sxs-lookup"><span data-stu-id="0fe3d-153">hello choice for User Principal Name in Azure AD Connect defaults toohello userPrincipalName attribute in Active Directory.</span></span> <span data-ttu-id="0fe3d-154">Als u een ander kenmerk voor de principalnaam van gebruiker kiezen en zijn Federatie met AD FS, vervolgens Azure AD Connect AD FS wilt configureren voor alternatieve aanmeldings-ID.</span><span class="sxs-lookup"><span data-stu-id="0fe3d-154">If you choose any other attribute for User Principal Name and are federating using AD FS, then Azure AD Connect will configure AD FS for alternate login ID.</span></span> <span data-ttu-id="0fe3d-155">Een voorbeeld van het kiezen van een ander kenmerk voor User Principal Name wordt hieronder weergegeven:</span><span class="sxs-lookup"><span data-stu-id="0fe3d-155">An example of choosing a different attribute for User Principal Name is shown below:</span></span>

![Selectie van alternatieve ID-kenmerk](media/active-directory-aadconnect-federation-management/attributeselection.png)

<span data-ttu-id="0fe3d-157">Alternatieve aanmeldings-ID configureren voor AD FS bestaat uit twee belangrijke stappen:</span><span class="sxs-lookup"><span data-stu-id="0fe3d-157">Configuring alternate login ID for AD FS consists of two main steps:</span></span>
1. <span data-ttu-id="0fe3d-158">**De juiste set Hallo van uitgifte claims configureren**: claimregels Hallo uitgifte van de relying party hello Azure AD vertrouwen gewijzigde toouse Hallo geselecteerd UserPrincipalName kenmerk zijn zoals alternatieve ID van gebruiker Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="0fe3d-158">**Configure hello right set of issuance claims**: hello issuance claim rules in hello Azure AD relying party trust are modified toouse hello selected UserPrincipalName attribute as hello alternate ID of hello user.</span></span>
2. <span data-ttu-id="0fe3d-159">**Schakel alternatieve aanmeldings-ID in Hallo AD FS-configuratie**: Hallo AD FS-configuratie is bijgewerkt, zodat AD FS kunt opzoeken van de gebruikers in de juiste forests Hallo Hallo alternatieve-id.</span><span class="sxs-lookup"><span data-stu-id="0fe3d-159">**Enable alternate login ID in hello AD FS configuration**: hello AD FS configuration is updated so that AD FS can look up users in hello appropriate forests using hello alternate ID.</span></span> <span data-ttu-id="0fe3d-160">Deze configuratie wordt ondersteund voor AD FS in Windows Server 2012 R2 (met KB2919355) of hoger.</span><span class="sxs-lookup"><span data-stu-id="0fe3d-160">This configuration is supported for AD FS on Windows Server 2012 R2 (with KB2919355) or later.</span></span> <span data-ttu-id="0fe3d-161">Als Hallo AD FS-servers 2012 R2 zijn, vereist Azure AD Connect-controles voor Hallo aanwezigheid van Hallo KB.</span><span class="sxs-lookup"><span data-stu-id="0fe3d-161">If hello AD FS servers are 2012 R2, Azure AD Connect checks for hello presence of hello required KB.</span></span> <span data-ttu-id="0fe3d-162">Als hello KB niet wordt gedetecteerd, wordt een waarschuwing weergegeven nadat de configuratie is voltooid, zoals hieronder wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="0fe3d-162">If hello KB is not detected, a warning will be displayed after configuration completes, as shown below:</span></span>

    ![Waarschuwing voor KB op 2012R2 ontbreekt](media/active-directory-aadconnect-federation-management/kbwarning.png)

    <span data-ttu-id="0fe3d-164">toorectify hello configuratie in geval van een ontbrekende KB installeren Hallo vereist [KB2919355](http://go.microsoft.com/fwlink/?LinkID=396590) en herstel daarna de vertrouwensrelatie met behulp van Hallo [AAD herstellen en AD FS-vertrouwensrelatie](#repairthetrust).</span><span class="sxs-lookup"><span data-stu-id="0fe3d-164">toorectify hello configuration in case of missing KB, install hello required [KB2919355](http://go.microsoft.com/fwlink/?LinkID=396590) and then repair hello trust using [Repair AAD and AD FS Trust](#repairthetrust).</span></span>

> [!NOTE]
> <span data-ttu-id="0fe3d-165">Voor meer informatie over alternateID en stappen toomanually configureren, lezen [Configuring Alternate Login ID](https://technet.microsoft.com/windows-server-docs/identity/ad-fs/operations/configuring-alternate-login-id)</span><span class="sxs-lookup"><span data-stu-id="0fe3d-165">For more information on alternateID and steps toomanually configure, read [Configuring Alternate Login ID](https://technet.microsoft.com/windows-server-docs/identity/ad-fs/operations/configuring-alternate-login-id)</span></span>

## <span data-ttu-id="0fe3d-166">Een AD FS-server toevoegen<a name=addadfsserver></a></span><span class="sxs-lookup"><span data-stu-id="0fe3d-166">Add an AD FS server <a name=addadfsserver></a></span></span>

> [!NOTE]
> <span data-ttu-id="0fe3d-167">tooadd een AD FS-server, Azure AD Connect vereist Hallo PFX-certificaat.</span><span class="sxs-lookup"><span data-stu-id="0fe3d-167">tooadd an AD FS server, Azure AD Connect requires hello PFX certificate.</span></span> <span data-ttu-id="0fe3d-168">Daarom kunt u deze bewerking uitvoeren als u Hallo AD FS-farm met behulp van Azure AD Connect geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="0fe3d-168">Therefore, you can perform this operation only if you configured hello AD FS farm by using Azure AD Connect.</span></span>

1. <span data-ttu-id="0fe3d-169">Selecteer **een extra federatieserver implementeren**, en klik op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="0fe3d-169">Select **Deploy an additional Federation Server**, and click **Next**.</span></span>

   ![Extra federatieserver](media/active-directory-aadconnect-federation-management/AddNewADFSServer1.PNG)

2. <span data-ttu-id="0fe3d-171">Op Hallo **verbinding tooAzure AD** pagina, Geef uw referenties hoofdbeheerder voor Azure AD en klikt u op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="0fe3d-171">On hello **Connect tooAzure AD** page, enter your global administrator credentials for Azure AD, and click **Next**.</span></span>

   ![Verbinding maken met tooAzure AD](media/active-directory-aadconnect-federation-management/AddNewADFSServer2.PNG)

3. <span data-ttu-id="0fe3d-173">Geef beheerdersreferenties Hallo-domein.</span><span class="sxs-lookup"><span data-stu-id="0fe3d-173">Provide hello domain administrator credentials.</span></span>

   ![Referenties voor de domeinbeheerder](media/active-directory-aadconnect-federation-management/AddNewADFSServer3.PNG)

4. <span data-ttu-id="0fe3d-175">Azure AD Connect vraagt om wachtwoord op Hallo van Hallo PFX-bestand dat u hebt opgegeven tijdens het configureren van uw nieuwe AD FS-farm met Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="0fe3d-175">Azure AD Connect asks for hello password of hello PFX file that you provided while configuring your new AD FS farm with Azure AD Connect.</span></span> <span data-ttu-id="0fe3d-176">Klik op **wachtwoord invoeren** tooprovide Hallo wachtwoord voor Hallo PFX-bestand.</span><span class="sxs-lookup"><span data-stu-id="0fe3d-176">Click **Enter Password** tooprovide hello password for hello PFX file.</span></span>

   ![Certificaatwachtwoord](media/active-directory-aadconnect-federation-management/AddNewADFSServer4.PNG)

    ![SSL-certificaat opgeven](media/active-directory-aadconnect-federation-management/AddNewADFSServer5.PNG)

5. <span data-ttu-id="0fe3d-179">Op Hallo **AD FS-Servers** pagina, voert u Hallo-servernaam of IP-adres toobe toegevoegd toohello AD FS-farm.</span><span class="sxs-lookup"><span data-stu-id="0fe3d-179">On hello **AD FS Servers** page, enter hello server name or IP address toobe added toohello AD FS farm.</span></span>

   ![AD FS-servers](media/active-directory-aadconnect-federation-management/AddNewADFSServer6.PNG)

6. <span data-ttu-id="0fe3d-181">Klik op **volgende**, en Ga via de uiteindelijke Hallo **configureren** pagina.</span><span class="sxs-lookup"><span data-stu-id="0fe3d-181">Click **Next**, and go through hello final **Configure** page.</span></span> <span data-ttu-id="0fe3d-182">Nadat Azure AD Connect is voltooid met het toevoegen van Hallo servers toohello AD FS-farm, krijgt u Hallo optie tooverify Hallo connectiviteit.</span><span class="sxs-lookup"><span data-stu-id="0fe3d-182">After Azure AD Connect has finished adding hello servers toohello AD FS farm, you will be given hello option tooverify hello connectivity.</span></span>

   ![Gereed tooconfigure](media/active-directory-aadconnect-federation-management/AddNewADFSServer7.PNG)

    ![Installatie voltooid](media/active-directory-aadconnect-federation-management/AddNewADFSServer8.PNG)

## <span data-ttu-id="0fe3d-185">Een AD FS WAP-server toevoegen<a name=addwapserver></a></span><span class="sxs-lookup"><span data-stu-id="0fe3d-185">Add an AD FS WAP server <a name=addwapserver></a></span></span>

> [!NOTE]
> <span data-ttu-id="0fe3d-186">tooadd een WAP-server, in de Azure AD Connect is Hallo PFX-certificaat vereist.</span><span class="sxs-lookup"><span data-stu-id="0fe3d-186">tooadd a WAP server, Azure AD Connect requires hello PFX certificate.</span></span> <span data-ttu-id="0fe3d-187">Daarom kunt u deze bewerking alleen uitvoeren als u Hallo AD FS-farm met behulp van Azure AD Connect geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="0fe3d-187">Therefore, you can only perform this operation if you configured hello AD FS farm by using Azure AD Connect.</span></span>

1. <span data-ttu-id="0fe3d-188">Selecteer **Web Application Proxy implementeren** uit Hallo lijst met beschikbare taken.</span><span class="sxs-lookup"><span data-stu-id="0fe3d-188">Select **Deploy Web Application Proxy** from hello list of available tasks.</span></span>

   ![Webtoepassingsproxy implementeren](media/active-directory-aadconnect-federation-management/WapServer1.PNG)

2. <span data-ttu-id="0fe3d-190">Geef referenties op Hallo Azure globale beheerder.</span><span class="sxs-lookup"><span data-stu-id="0fe3d-190">Provide hello Azure global administrator credentials.</span></span>

   ![Verbinding maken met tooAzure AD](media/active-directory-aadconnect-federation-management/wapserver2.PNG)

3. <span data-ttu-id="0fe3d-192">Op Hallo **Geef SSL-certificaat** pagina, Hallo wachtwoord opgeven voor Hallo PFX-bestand dat u hebt opgegeven toen u Hallo AD FS-farm met Azure AD Connect geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="0fe3d-192">On hello **Specify SSL certificate** page, provide hello password for hello PFX file that you provided when you configured hello AD FS farm with Azure AD Connect.</span></span>
   <span data-ttu-id="0fe3d-193">![Certificaatwachtwoord](media/active-directory-aadconnect-federation-management/WapServer3.PNG)</span><span class="sxs-lookup"><span data-stu-id="0fe3d-193">![Certificate password](media/active-directory-aadconnect-federation-management/WapServer3.PNG)</span></span>

    ![SSL-certificaat opgeven](media/active-directory-aadconnect-federation-management/WapServer4.PNG)

4. <span data-ttu-id="0fe3d-195">Hallo server toobe toegevoegd als een WAP-server toevoegen.</span><span class="sxs-lookup"><span data-stu-id="0fe3d-195">Add hello server toobe added as a WAP server.</span></span> <span data-ttu-id="0fe3d-196">Omdat Hallo WAP-server mogelijk niet lid toohello domein, Hallo wordt gevraagd voor beheerdersreferenties toohello server die wordt toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="0fe3d-196">Because hello WAP server might not be joined toohello domain, hello wizard asks for administrative credentials toohello server being added.</span></span>

   ![Referenties van de beheerserver](media/active-directory-aadconnect-federation-management/WapServer5.PNG)

5. <span data-ttu-id="0fe3d-198">Op Hallo **vertrouwensrelatie proxyreferenties** pagina, Geef beheerdersreferenties tooconfigure Hallo proxyserveradres vertrouwen en toegang Hallo primaire server in Hallo AD FS-farm.</span><span class="sxs-lookup"><span data-stu-id="0fe3d-198">On hello **Proxy trust credentials** page, provide administrative credentials tooconfigure hello proxy trust and access hello primary server in hello AD FS farm.</span></span>

   ![Vertrouwensrelatie proxyreferenties](media/active-directory-aadconnect-federation-management/WapServer6.PNG)

6. <span data-ttu-id="0fe3d-200">Op Hallo **gereed tooconfigure** pagina Hallo wizard geeft Hallo-lijst van acties die worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="0fe3d-200">On hello **Ready tooconfigure** page, hello wizard shows hello list of actions that will be performed.</span></span>

   ![Gereed tooconfigure](media/active-directory-aadconnect-federation-management/WapServer7.PNG)

7. <span data-ttu-id="0fe3d-202">Klik op **installeren** toofinish Hallo configuratie.</span><span class="sxs-lookup"><span data-stu-id="0fe3d-202">Click **Install** toofinish hello configuration.</span></span> <span data-ttu-id="0fe3d-203">Nadat het Hallo-configuratie is voltooid, Hallo Hallo wizard geeft u de optie tooverify Hallo connectiviteit toohello servers.</span><span class="sxs-lookup"><span data-stu-id="0fe3d-203">After hello configuration is complete, hello wizard gives you hello option tooverify hello connectivity toohello servers.</span></span> <span data-ttu-id="0fe3d-204">Klik op **controleren** toocheck connectiviteit.</span><span class="sxs-lookup"><span data-stu-id="0fe3d-204">Click **Verify** toocheck connectivity.</span></span>

   ![Installatie voltooid](media/active-directory-aadconnect-federation-management/WapServer8.PNG)

## <span data-ttu-id="0fe3d-206">Een federatieve domein toevoegen<a name=addfeddomain></a></span><span class="sxs-lookup"><span data-stu-id="0fe3d-206">Add a federated domain <a name=addfeddomain></a></span></span>

<span data-ttu-id="0fe3d-207">Het is gemakkelijk tooadd een domein toobe gefedereerd met Azure AD met behulp van Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="0fe3d-207">It's easy tooadd a domain toobe federated with Azure AD by using Azure AD Connect.</span></span> <span data-ttu-id="0fe3d-208">Azure AD Connect Hallo domein voor Federatie toegevoegd en Hallo claim regels toocorrectly Hallo verlener weer wanneer u meerdere domeinen die zijn gefedereerd met Azure AD hebt gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="0fe3d-208">Azure AD Connect adds hello domain for federation and modifies hello claim rules toocorrectly reflect hello issuer when you have multiple domains federated with Azure AD.</span></span>

1. <span data-ttu-id="0fe3d-209">tooadd een federatieve domein, selecteer Hallo taak **toevoegen van een extra Azure AD-domein**.</span><span class="sxs-lookup"><span data-stu-id="0fe3d-209">tooadd a federated domain, select hello task **Add an additional Azure AD domain**.</span></span>

   ![Extra Azure AD-domein](media/active-directory-aadconnect-federation-management/AdditionalDomain1.PNG)

2. <span data-ttu-id="0fe3d-211">Klik op volgende pagina van wizard Hallo Hallo referenties Hallo hoofdbeheerder voor Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0fe3d-211">On hello next page of hello wizard, provide hello global administrator credentials for Azure AD.</span></span>

   ![Verbinding maken met tooAzure AD](media/active-directory-aadconnect-federation-management/AdditionalDomain2.PNG)

3. <span data-ttu-id="0fe3d-213">Op Hallo **RAS-referenties** pagina, Hallo domein-beheerdersreferenties opgeven.</span><span class="sxs-lookup"><span data-stu-id="0fe3d-213">On hello **Remote access credentials** page, provide hello domain administrator credentials.</span></span>

   ![Referenties voor externe toegang](media/active-directory-aadconnect-federation-management/additionaldomain3.PNG)

4. <span data-ttu-id="0fe3d-215">Op de volgende pagina Hallo overzicht Hallo wizard van Azure AD-domeinen die u kunt uw on-premises directory met federeren.</span><span class="sxs-lookup"><span data-stu-id="0fe3d-215">On hello next page, hello wizard provides a list of Azure AD domains that you can federate your on-premises directory with.</span></span> <span data-ttu-id="0fe3d-216">Hallo domein uit Hallo lijst kiezen.</span><span class="sxs-lookup"><span data-stu-id="0fe3d-216">Choose hello domain from hello list.</span></span>

   ![Azure AD-domein](media/active-directory-aadconnect-federation-management/AdditionalDomain4.PNG)

    <span data-ttu-id="0fe3d-218">Nadat u ervoor Hallo domein kiest, wordt Hallo wizard biedt u met de juiste informatie over verdere acties die wizard Hallo nemen en Hallo gevolgen van het Hallo-configuratie.</span><span class="sxs-lookup"><span data-stu-id="0fe3d-218">After you choose hello domain, hello wizard provides you with appropriate information about further actions that hello wizard will take and hello impact of hello configuration.</span></span> <span data-ttu-id="0fe3d-219">In sommige gevallen, als u een domein dat nog niet is geverifieerd in Azure AD Hallo wizard biedt u informatie toohelp selecteert verifiëren u Hallo domein.</span><span class="sxs-lookup"><span data-stu-id="0fe3d-219">In some cases, if you select a domain that isn't yet verified in Azure AD, hello wizard provides you with information toohelp you verify hello domain.</span></span> <span data-ttu-id="0fe3d-220">Zie [toevoegen van uw aangepaste domein naam tooAzure Active Directory](../active-directory-add-domain.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="0fe3d-220">See [Add your custom domain name tooAzure Active Directory](../active-directory-add-domain.md) for more details.</span></span>

5. <span data-ttu-id="0fe3d-221">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="0fe3d-221">Click **Next**.</span></span> <span data-ttu-id="0fe3d-222">Hallo **gereed tooconfigure** pagina bevat Hallo-lijst van acties die door Azure AD Connect worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="0fe3d-222">hello **Ready tooconfigure** page shows hello list of actions that Azure AD Connect will perform.</span></span> <span data-ttu-id="0fe3d-223">Klik op **installeren** toofinish Hallo configuratie.</span><span class="sxs-lookup"><span data-stu-id="0fe3d-223">Click **Install** toofinish hello configuration.</span></span>

   ![Gereed tooconfigure](media/active-directory-aadconnect-federation-management/AdditionalDomain5.PNG)

> [!NOTE]
> <span data-ttu-id="0fe3d-225">Gebruikers van Hallo toegevoegd federatieve domein moet worden gesynchroniseerd voordat ze kunnen toologin tooAzure AD.</span><span class="sxs-lookup"><span data-stu-id="0fe3d-225">Users from hello added federated domain must be synchronized before they will be able toologin tooAzure AD.</span></span>

## <a name="ad-fs-customization"></a><span data-ttu-id="0fe3d-226">AD FS-aanpassing</span><span class="sxs-lookup"><span data-stu-id="0fe3d-226">AD FS customization</span></span>
<span data-ttu-id="0fe3d-227">Hallo volgende secties bevatten informatie over een aantal algemene taken Hallo tooperform hebt wanneer u uw AD FS-aanmeldingspagina aanpassen.</span><span class="sxs-lookup"><span data-stu-id="0fe3d-227">hello following sections provide details about some of hello common tasks that you might have tooperform when you customize your AD FS sign-in page.</span></span>

## <span data-ttu-id="0fe3d-228">Een aangepast bedrijfslogo of afbeelding toevoegen<a name=customlogo></a></span><span class="sxs-lookup"><span data-stu-id="0fe3d-228">Add a custom company logo or illustration <a name=customlogo></a></span></span>
<span data-ttu-id="0fe3d-229">toochange hello logo van Hallo-bedrijf dat wordt weergegeven op Hallo **aanmelden** pagina, gebruikt u Hallo na de Windows PowerShell-cmdlet en syntaxis.</span><span class="sxs-lookup"><span data-stu-id="0fe3d-229">toochange hello logo of hello company that's displayed on hello **Sign-in** page, use hello following Windows PowerShell cmdlet and syntax.</span></span>

> [!NOTE]
> <span data-ttu-id="0fe3d-230">Hallo aanbevolen dimensies voor Hallo logo 260 x 35 96 dpi-waarde met een bestandsgrootte van niet meer dan 10 KB zijn.</span><span class="sxs-lookup"><span data-stu-id="0fe3d-230">hello recommended dimensions for hello logo are 260 x 35 @ 96 dpi with a file size no greater than 10 KB.</span></span>

    Set-AdfsWebTheme -TargetName default -Logo @{path="c:\Contoso\logo.PNG"}

> [!NOTE]
> <span data-ttu-id="0fe3d-231">Hallo *TargetName* parameter is vereist.</span><span class="sxs-lookup"><span data-stu-id="0fe3d-231">hello *TargetName* parameter is required.</span></span> <span data-ttu-id="0fe3d-232">Hallo standaardthema dat wordt geleverd met AD FS heet standaard.</span><span class="sxs-lookup"><span data-stu-id="0fe3d-232">hello default theme that's released with AD FS is named Default.</span></span>

## <span data-ttu-id="0fe3d-233">Een beschrijving van de aanmeldingspagina toevoegen<a name=addsignindescription></a></span><span class="sxs-lookup"><span data-stu-id="0fe3d-233">Add a sign-in description <a name=addsignindescription></a></span></span>
<span data-ttu-id="0fe3d-234">een aanmeldingspagina beschrijving toohello tooadd **aanmeldingspagina**, Hallo na de Windows PowerShell-cmdlet en syntaxis gebruiken.</span><span class="sxs-lookup"><span data-stu-id="0fe3d-234">tooadd a sign-in page description toohello **Sign-in page**, use hello following Windows PowerShell cmdlet and syntax.</span></span>

    Set-AdfsGlobalWebContent -SignInPageDescriptionText "<p>Sign-in tooContoso requires device registration. Click <A href='http://fs1.contoso.com/deviceregistration/'>here</A> for more information.</p>"

## <span data-ttu-id="0fe3d-235">Wijzigen van de claimregels van AD FS<a name=modclaims></a></span><span class="sxs-lookup"><span data-stu-id="0fe3d-235">Modify AD FS claim rules <a name=modclaims></a></span></span>
<span data-ttu-id="0fe3d-236">AD FS ondersteunt een taal die u kunt gebruiken voor uitgebreide claim toocreate aangepaste claimregels.</span><span class="sxs-lookup"><span data-stu-id="0fe3d-236">AD FS supports a rich claim language that you can use toocreate custom claim rules.</span></span> <span data-ttu-id="0fe3d-237">Zie voor meer informatie [rol van de Claimregeltaal Hallo Hallo](https://technet.microsoft.com/library/dd807118.aspx).</span><span class="sxs-lookup"><span data-stu-id="0fe3d-237">For more information, see [hello Role of hello Claim Rule Language](https://technet.microsoft.com/library/dd807118.aspx).</span></span>

<span data-ttu-id="0fe3d-238">Hallo volgende secties wordt beschreven hoe u aangepaste regels voor enkele scenario's die betrekking tooAzure AD en AD FS-federatie hebben kan schrijven.</span><span class="sxs-lookup"><span data-stu-id="0fe3d-238">hello following sections describe how you can write custom rules for some scenarios that relate tooAzure AD and AD FS federation.</span></span>

### <a name="immutable-id-conditional-on-a-value-being-present-in-hello-attribute"></a><span data-ttu-id="0fe3d-239">Niet-wijzigbaar voorwaardelijke op een waarde in het Hallo-kenmerk-ID</span><span class="sxs-lookup"><span data-stu-id="0fe3d-239">Immutable ID conditional on a value being present in hello attribute</span></span>
<span data-ttu-id="0fe3d-240">Azure AD Connect kunt u een kenmerk toobe gebruikt als een bronanker wanneer objecten zijn gesynchroniseerd tooAzure AD opgeven.</span><span class="sxs-lookup"><span data-stu-id="0fe3d-240">Azure AD Connect lets you specify an attribute toobe used as a source anchor when objects are synced tooAzure AD.</span></span> <span data-ttu-id="0fe3d-241">Als de waarde in het aangepaste kenmerk Hallo Hallo niet leeg is, kunt u een niet-wijzigbaar ID claim tooissue.</span><span class="sxs-lookup"><span data-stu-id="0fe3d-241">If hello value in hello custom attribute is not empty, you might want tooissue an immutable ID claim.</span></span>

<span data-ttu-id="0fe3d-242">Bijvoorbeeld, kunt u selecteren **ms-ds-consistencyguid** als Hallo-kenmerk voor het bronanker hello en probleem **onveranderbare id genoemd** als **ms-ds-consistencyguid** in case Hallo het kenmerk heeft de waarde tegen.</span><span class="sxs-lookup"><span data-stu-id="0fe3d-242">For example, you might select **ms-ds-consistencyguid** as hello attribute for hello source anchor and issue **ImmutableID** as **ms-ds-consistencyguid** in case hello attribute has a value against it.</span></span> <span data-ttu-id="0fe3d-243">Als er geen waarde tegen Hallo kenmerk is, geven **objectGuid** zoals Hallo onveranderbare ID.</span><span class="sxs-lookup"><span data-stu-id="0fe3d-243">If there's no value against hello attribute, issue **objectGuid** as hello immutable ID.</span></span> <span data-ttu-id="0fe3d-244">U kunt Hallo set aangepaste claimregels kunt opstellen, zoals beschreven in de volgende sectie Hallo.</span><span class="sxs-lookup"><span data-stu-id="0fe3d-244">You can construct hello set of custom claim rules as described in hello following section.</span></span>

<span data-ttu-id="0fe3d-245">**Regel 1: Querykenmerken**</span><span class="sxs-lookup"><span data-stu-id="0fe3d-245">**Rule 1: Query attributes**</span></span>

    c:[Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname"]
    => add(store = "Active Directory", types = ("http://contoso.com/ws/2016/02/identity/claims/objectguid", "http://contoso.com/ws/2016/02/identity/claims/msdsconsistencyguid"), query = "; objectGuid,ms-ds-consistencyguid;{0}", param = c.Value);

<span data-ttu-id="0fe3d-246">In deze regel, waaruit u gegevens ophaalt Hallo waarden van **ms-ds-consistencyguid** en **objectGuid** voor Hallo gebruiker uit Active Directory.</span><span class="sxs-lookup"><span data-stu-id="0fe3d-246">In this rule, you're querying hello values of **ms-ds-consistencyguid** and **objectGuid** for hello user from Active Directory.</span></span> <span data-ttu-id="0fe3d-247">Hallo store naam tooan betreffende winkelnaam wijzigen in uw AD FS-implementatie.</span><span class="sxs-lookup"><span data-stu-id="0fe3d-247">Change hello store name tooan appropriate store name in your AD FS deployment.</span></span> <span data-ttu-id="0fe3d-248">Hallo claims type tooa juiste claims type voor uw federatieserver ook wijzigen zoals is gedefinieerd voor **objectGuid** en **ms-ds-consistencyguid**.</span><span class="sxs-lookup"><span data-stu-id="0fe3d-248">Also change hello claims type tooa proper claims type for your federation, as defined for **objectGuid** and **ms-ds-consistencyguid**.</span></span>

<span data-ttu-id="0fe3d-249">Ook met behulp van **toevoegen** en niet **probleem**, u te voorkomen dat een uitgaande probleem voor Hallo entiteit toe te voegen en Hallo waarden kunt gebruiken als tussenliggende waarden.</span><span class="sxs-lookup"><span data-stu-id="0fe3d-249">Also, by using **add** and not **issue**, you avoid adding an outgoing issue for hello entity, and can use hello values as intermediate values.</span></span> <span data-ttu-id="0fe3d-250">Verleent u Hallo claim in een latere regel nadat u hebt vastgesteld welke waarde toouse zoals Hallo onveranderbare ID.</span><span class="sxs-lookup"><span data-stu-id="0fe3d-250">You will issue hello claim in a later rule after you establish which value toouse as hello immutable ID.</span></span>

<span data-ttu-id="0fe3d-251">**Regel 2: Controleer of de ds-ms-consistencyguid voor Hallo-gebruiker bestaat**</span><span class="sxs-lookup"><span data-stu-id="0fe3d-251">**Rule 2: Check if ms-ds-consistencyguid exists for hello user**</span></span>

    NOT EXISTS([Type == "http://contoso.com/ws/2016/02/identity/claims/msdsconsistencyguid"])
    => add(Type = "urn:anandmsft:tmp/idflag", Value = "useguid");

<span data-ttu-id="0fe3d-252">Deze regel definieert een tijdelijke vlag aangeroepen **idflag** ingestelde te**useguid** als er geen **ms-ds-consistencyguid** ingevuld voor Hallo-gebruiker.</span><span class="sxs-lookup"><span data-stu-id="0fe3d-252">This rule defines a temporary flag called **idflag** that is set too**useguid** if there's no **ms-ds-consistencyguid** populated for hello user.</span></span> <span data-ttu-id="0fe3d-253">Hallo logica achter is Hallo-feit dat AD FS leeg claims niet toegestaan.</span><span class="sxs-lookup"><span data-stu-id="0fe3d-253">hello logic behind this is hello fact that AD FS doesn't allow empty claims.</span></span> <span data-ttu-id="0fe3d-254">Dus als u claims http://contoso.com/ws/2016/02/identity/claims/objectguid en http://contoso.com/ws/2016/02/identity/claims/msdsconsistencyguid in regel 1 toevoegt, u uiteindelijk met eindigen een **msdsconsistencyguid** alleen als claim Hallo-waarde wordt voor de gebruiker hello gevuld.</span><span class="sxs-lookup"><span data-stu-id="0fe3d-254">So when you add claims http://contoso.com/ws/2016/02/identity/claims/objectguid and http://contoso.com/ws/2016/02/identity/claims/msdsconsistencyguid in Rule 1, you end up with an **msdsconsistencyguid** claim only if hello value is populated for hello user.</span></span> <span data-ttu-id="0fe3d-255">Als deze niet is ingevuld, wordt AD FS ziet dat het een lege waarde hebben en onmiddellijk verwijderd.</span><span class="sxs-lookup"><span data-stu-id="0fe3d-255">If it isn't populated, AD FS sees that it will have an empty value and drops it immediately.</span></span> <span data-ttu-id="0fe3d-256">Alle objecten hebben **objectGuid**, zodat deze claim wordt altijd er nadat regel 1 wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="0fe3d-256">All objects will have **objectGuid**, so that claim will always be there after Rule 1 is executed.</span></span>

<span data-ttu-id="0fe3d-257">**Regel 3: Ms-ds-consistencyguid verlenen als niet-wijzigbaar ID indien aanwezig**</span><span class="sxs-lookup"><span data-stu-id="0fe3d-257">**Rule 3: Issue ms-ds-consistencyguid as immutable ID if it's present**</span></span>

    c:[Type == "http://contoso.com/ws/2016/02/identity/claims/msdsconsistencyguid"]
    => issue(Type = "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier", Value = c.Value);

<span data-ttu-id="0fe3d-258">Dit is een impliciete **Exist** controleren.</span><span class="sxs-lookup"><span data-stu-id="0fe3d-258">This is an implicit **Exist** check.</span></span> <span data-ttu-id="0fe3d-259">Als het Hallo-waarde voor Hallo claim bestaat, geven vervolgens dat als niet-wijzigbaar Hallo-id.</span><span class="sxs-lookup"><span data-stu-id="0fe3d-259">If hello value for hello claim exists, then issue that as hello immutable ID.</span></span> <span data-ttu-id="0fe3d-260">Hallo maakt gebruik van het vorige voorbeeld Hallo **nameidentifier** claim.</span><span class="sxs-lookup"><span data-stu-id="0fe3d-260">hello previous example uses hello **nameidentifier** claim.</span></span> <span data-ttu-id="0fe3d-261">Hebt u toochange deze toohello juiste claimtype voor Hallo onveranderbare ID in uw omgeving.</span><span class="sxs-lookup"><span data-stu-id="0fe3d-261">You'll have toochange this toohello appropriate claim type for hello immutable ID in your environment.</span></span>

<span data-ttu-id="0fe3d-262">**Regel 4: ObjectGuid verlenen als niet-wijzigbaar-ID als ms-ds-consistencyGuid niet aanwezig is**</span><span class="sxs-lookup"><span data-stu-id="0fe3d-262">**Rule 4: Issue objectGuid as immutable ID if ms-ds-consistencyGuid is not present**</span></span>

    c1:[Type == "urn:anandmsft:tmp/idflag", Value =~ "useguid"]
    && c2:[Type == "http://contoso.com/ws/2016/02/identity/claims/objectguid"]
    => issue(Type = "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier", Value = c2.Value);

<span data-ttu-id="0fe3d-263">In deze regel, bent u gewoon Hallo tijdelijke vlag controleren **idflag**.</span><span class="sxs-lookup"><span data-stu-id="0fe3d-263">In this rule, you're simply checking hello temporary flag **idflag**.</span></span> <span data-ttu-id="0fe3d-264">U bepalen of tooissue Hallo claim is gebaseerd op de waarde ervan.</span><span class="sxs-lookup"><span data-stu-id="0fe3d-264">You decide whether tooissue hello claim based on its value.</span></span>

> [!NOTE]
> <span data-ttu-id="0fe3d-265">Hallo-volgorde van deze regels is belangrijk.</span><span class="sxs-lookup"><span data-stu-id="0fe3d-265">hello sequence of these rules is important.</span></span>

### <a name="sso-with-a-subdomain-upn"></a><span data-ttu-id="0fe3d-266">Eenmalige aanmelding met een subdomein UPN</span><span class="sxs-lookup"><span data-stu-id="0fe3d-266">SSO with a subdomain UPN</span></span>
<span data-ttu-id="0fe3d-267">U kunt meer dan één domein toobe gefedereerd met behulp van Azure AD Connect, zoals beschreven in toevoegen [toevoegen van een nieuwe federatieve domein](active-directory-aadconnect-federation-management.md#addfeddomain).</span><span class="sxs-lookup"><span data-stu-id="0fe3d-267">You can add more than one domain toobe federated by using Azure AD Connect, as described in [Add a new federated domain](active-directory-aadconnect-federation-management.md#addfeddomain).</span></span> <span data-ttu-id="0fe3d-268">U moet Hallo UPN (User Principal Name) Gebruikersclaim zodanig aanpassen dat hello uitgever-ID komt toohello hoofddomein en niet Hallo subdomein overeen omdat Hallo federatieve hoofddomein ook Hallo onderliggende vallen.</span><span class="sxs-lookup"><span data-stu-id="0fe3d-268">You must modify hello user principal name (UPN) claim so that hello issuer ID corresponds toohello root domain and not hello subdomain, because hello federated root domain also covers hello child.</span></span>

<span data-ttu-id="0fe3d-269">Standaard Hallo claimregelsjablonen voor uitgevers-ID is ingesteld als:</span><span class="sxs-lookup"><span data-stu-id="0fe3d-269">By default, hello claim rule for issuer ID is set as:</span></span>

    c:[Type
    == “http://schemas.xmlsoap.org/claims/UPN“]

    => issue(Type = “http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid“, Value = regexreplace(c.Value, “.+@(?<domain>.+)“, “http://${domain}/adfs/services/trust/“));

![Standaard uitgever-ID claim](media/active-directory-aadconnect-federation-management/issuer_id_default.png)

<span data-ttu-id="0fe3d-271">Standaardregel Hallo gewoon duurt Hallo UPN-achtervoegsel en wordt gebruikt in Hallo uitgever-ID claim.</span><span class="sxs-lookup"><span data-stu-id="0fe3d-271">hello default rule simply takes hello UPN suffix and uses it in hello issuer ID claim.</span></span> <span data-ttu-id="0fe3d-272">Bijvoorbeeld: John is een gebruiker in sub.contoso.com en contoso.com is gefedereerd met Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0fe3d-272">For example, John is a user in sub.contoso.com, and contoso.com is federated with Azure AD.</span></span> <span data-ttu-id="0fe3d-273">John voert john@sub.contoso.com zoals Hallo gebruikersnaam tijdens het aanmelden tooAzure AD.</span><span class="sxs-lookup"><span data-stu-id="0fe3d-273">John enters john@sub.contoso.com as hello username while signing in tooAzure AD.</span></span> <span data-ttu-id="0fe3d-274">Hallo standaard uitgever-ID claimregel in AD FS verwerkt op Hallo volgende wijze:</span><span class="sxs-lookup"><span data-stu-id="0fe3d-274">hello default issuer ID claim rule in AD FS handles it in hello following manner:</span></span>

    c:[Type
    == “http://schemas.xmlsoap.org/claims/UPN“]

    => issue(Type = “http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid“, Value = regexreplace(john@sub.contoso.com, “.+@(?<domain>.+)“, “http://${domain}/adfs/services/trust/“));

<span data-ttu-id="0fe3d-275">**Claimwaarde:** http://sub.contoso.com/adfs/services/trust/</span><span class="sxs-lookup"><span data-stu-id="0fe3d-275">**Claim value:**  http://sub.contoso.com/adfs/services/trust/</span></span>

<span data-ttu-id="0fe3d-276">toohave alleen Hallo hoofddomein in Hallo verlener claimwaarde, wijzig Hallo claim regel toomatch Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="0fe3d-276">toohave only hello root domain in hello issuer claim value, change hello claim rule toomatch hello following:</span></span>

    c:[Type == “http://schemas.xmlsoap.org/claims/UPN“]

    => issue(Type = “http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid“, Value = regexreplace(c.Value, “^((.*)([.|@]))?(?<domain>[^.]*[.].*)$”, “http://${domain}/adfs/services/trust/“));

## <a name="next-steps"></a><span data-ttu-id="0fe3d-277">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="0fe3d-277">Next steps</span></span>
<span data-ttu-id="0fe3d-278">Meer informatie over [opties aanmelden gebruiker](active-directory-aadconnect-user-signin.md).</span><span class="sxs-lookup"><span data-stu-id="0fe3d-278">Learn more about [user sign-in options](active-directory-aadconnect-user-signin.md).</span></span>

---
title: Active Directory Federation Services-beheer en aanpassingen met Azure AD Connect | Microsoft Docs
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
ms.openlocfilehash: 14f03542a6553c5bb697192828368ffe6b96441c
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="manage-and-customize-active-directory-federation-services-by-using-azure-ad-connect"></a><span data-ttu-id="32d4c-104">Beheren en aanpassen van Active Directory Federation Services met behulp van Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="32d4c-104">Manage and customize Active Directory Federation Services by using Azure AD Connect</span></span>
<span data-ttu-id="32d4c-105">Dit artikel wordt beschreven hoe u kunt beheren en aanpassen van Active Directory Federation Services (AD FS) met behulp van Azure Active Directory (Azure AD) verbinding maken.</span><span class="sxs-lookup"><span data-stu-id="32d4c-105">This article describes how to manage and customize Active Directory Federation Services (AD FS) by using Azure Active Directory (Azure AD) Connect.</span></span> <span data-ttu-id="32d4c-106">Dit omvat ook andere algemene AD FS-taken die u moet doen voor een volledige configuratie van een AD FS-farm.</span><span class="sxs-lookup"><span data-stu-id="32d4c-106">It also includes other common AD FS tasks that you might need to do for a complete configuration of an AD FS farm.</span></span>

| <span data-ttu-id="32d4c-107">Onderwerp</span><span class="sxs-lookup"><span data-stu-id="32d4c-107">Topic</span></span> | <span data-ttu-id="32d4c-108">Er wordt aangegeven</span><span class="sxs-lookup"><span data-stu-id="32d4c-108">What it covers</span></span> |
|:--- |:--- |
| <span data-ttu-id="32d4c-109">**Beheren van AD FS**</span><span class="sxs-lookup"><span data-stu-id="32d4c-109">**Manage AD FS**</span></span> | |
| [<span data-ttu-id="32d4c-110">Herstellen van de vertrouwensrelatie</span><span class="sxs-lookup"><span data-stu-id="32d4c-110">Repair the trust</span></span>](#repairthetrust) |<span data-ttu-id="32d4c-111">Klik hier voor meer informatie over het herstellen van de federatieve vertrouwensrelatie met Office 365.</span><span class="sxs-lookup"><span data-stu-id="32d4c-111">How to repair the federation trust with Office 365.</span></span> |
| [<span data-ttu-id="32d4c-112">Gefedereerd met Azure AD met behulp van alternatieve aanmeldings-ID</span><span class="sxs-lookup"><span data-stu-id="32d4c-112">Federate with Azure AD using alternate login ID </span></span>](#alternateid) | <span data-ttu-id="32d4c-113">Federatie met behulp van alternatieve aanmeldings-ID configureren</span><span class="sxs-lookup"><span data-stu-id="32d4c-113">Configure federation using alternate login ID</span></span>  |
| [<span data-ttu-id="32d4c-114">Een AD FS-server toevoegen</span><span class="sxs-lookup"><span data-stu-id="32d4c-114">Add an AD FS server</span></span>](#addadfsserver) |<span data-ttu-id="32d4c-115">Het uitbreiden van een AD FS-farm met een extra AD FS-server.</span><span class="sxs-lookup"><span data-stu-id="32d4c-115">How to expand an AD FS farm with an additional AD FS server.</span></span> |
| [<span data-ttu-id="32d4c-116">Een AD FS Web Application Proxy-server toevoegen</span><span class="sxs-lookup"><span data-stu-id="32d4c-116">Add an AD FS Web Application Proxy server</span></span>](#addwapserver) |<span data-ttu-id="32d4c-117">Het uitbreiden van een AD FS-farm met een extra Webtoepassingsproxy (WAP)-server.</span><span class="sxs-lookup"><span data-stu-id="32d4c-117">How to expand an AD FS farm with an additional Web Application Proxy (WAP) server.</span></span> |
| [<span data-ttu-id="32d4c-118">Een federatieve domein toevoegen</span><span class="sxs-lookup"><span data-stu-id="32d4c-118">Add a federated domain</span></span>](#addfeddomain) |<span data-ttu-id="32d4c-119">Het toevoegen van een federatieve domein.</span><span class="sxs-lookup"><span data-stu-id="32d4c-119">How to add a federated domain.</span></span> |
| [<span data-ttu-id="32d4c-120">Het SSL-certificaat bijwerken</span><span class="sxs-lookup"><span data-stu-id="32d4c-120">Update the SSL certificate</span></span>](active-directory-aadconnectfed-ssl-update.md)| <span data-ttu-id="32d4c-121">Het bijwerken van het SSL-certificaat voor AD FS-farm.</span><span class="sxs-lookup"><span data-stu-id="32d4c-121">How to update the SSL certificate for an AD FS farm.</span></span> |
| <span data-ttu-id="32d4c-122">**Aanpassen van AD FS**</span><span class="sxs-lookup"><span data-stu-id="32d4c-122">**Customize AD FS**</span></span> | |
| [<span data-ttu-id="32d4c-123">Een aangepast bedrijfslogo of afbeelding toevoegen</span><span class="sxs-lookup"><span data-stu-id="32d4c-123">Add a custom company logo or illustration</span></span>](#customlogo) |<span data-ttu-id="32d4c-124">Het aanpassen van een AD FS-aanmeldingspagina met een bedrijfslogo en afbeelding.</span><span class="sxs-lookup"><span data-stu-id="32d4c-124">How to customize an AD FS sign-in page with a company logo and illustration.</span></span> |
| [<span data-ttu-id="32d4c-125">Een beschrijving van de aanmeldingspagina toevoegen</span><span class="sxs-lookup"><span data-stu-id="32d4c-125">Add a sign-in description</span></span>](#addsignindescription) |<span data-ttu-id="32d4c-126">Het toevoegen van een beschrijving van de aanmeldingspagina.</span><span class="sxs-lookup"><span data-stu-id="32d4c-126">How to add a sign-in page description.</span></span> |
| [<span data-ttu-id="32d4c-127">Wijzigen van de claimregels van AD FS</span><span class="sxs-lookup"><span data-stu-id="32d4c-127">Modify AD FS claim rules</span></span>](#modclaims) |<span data-ttu-id="32d4c-128">Het wijzigen van de AD FS-claims voor verschillende scenario's met Federatie.</span><span class="sxs-lookup"><span data-stu-id="32d4c-128">How to modify AD FS claims for various federation scenarios.</span></span> |

## <a name="manage-ad-fs"></a><span data-ttu-id="32d4c-129">Beheren van AD FS</span><span class="sxs-lookup"><span data-stu-id="32d4c-129">Manage AD FS</span></span>
<span data-ttu-id="32d4c-130">U kunt verschillende AD FS-gerelateerde taken in Azure AD Connect met minimale tussenkomst uitvoeren met behulp van de Azure AD Connect-wizard.</span><span class="sxs-lookup"><span data-stu-id="32d4c-130">You can perform various AD FS-related tasks in Azure AD Connect with minimal user intervention by using the Azure AD Connect wizard.</span></span> <span data-ttu-id="32d4c-131">Nadat u klaar bent met het Azure AD Connect installeert door de wizard uitvoert, kunt u de wizard opnieuw uitvoeren van extra taken uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="32d4c-131">After you've finished installing Azure AD Connect by running the wizard, you can run the wizard again to perform additional tasks.</span></span>

## <span data-ttu-id="32d4c-132">Herstellen van de vertrouwensrelatie<a name=repairthetrust></a></span><span class="sxs-lookup"><span data-stu-id="32d4c-132">Repair the trust <a name=repairthetrust></a></span></span>
<span data-ttu-id="32d4c-133">U kunt Azure AD Connect gebruiken om te controleren van de huidige status van de AD FS en Azure AD vertrouwt en de benodigde stappen ondernemen om te herstellen van de vertrouwensrelatie.</span><span class="sxs-lookup"><span data-stu-id="32d4c-133">You can use Azure AD Connect to check the current health of the AD FS and Azure AD trust and take appropriate actions to repair the trust.</span></span> <span data-ttu-id="32d4c-134">Volg deze stappen voor het herstellen van uw Azure AD en AD FS vertrouwen.</span><span class="sxs-lookup"><span data-stu-id="32d4c-134">Follow these steps to repair your Azure AD and AD FS trust.</span></span>

1. <span data-ttu-id="32d4c-135">Selecteer **reparatie AAD en ADFS-vertrouwen** uit de lijst met aanvullende taken.</span><span class="sxs-lookup"><span data-stu-id="32d4c-135">Select **Repair AAD and ADFS Trust** from the list of additional tasks.</span></span>
   <span data-ttu-id="32d4c-136">![Herstellen van AAD- en AD FS vertrouwen](media/active-directory-aadconnect-federation-management/RepairADTrust1.PNG)</span><span class="sxs-lookup"><span data-stu-id="32d4c-136">![Repair AAD and ADFS Trust](media/active-directory-aadconnect-federation-management/RepairADTrust1.PNG)</span></span>

2. <span data-ttu-id="32d4c-137">Op de **verbinding maken met Azure AD** pagina, Geef uw referenties voor de globale beheerder voor Azure AD en klikt u op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="32d4c-137">On the **Connect to Azure AD** page, provide your global administrator credentials for Azure AD, and click **Next**.</span></span>
   <span data-ttu-id="32d4c-138">![Verbinding maken met Azure AD](media/active-directory-aadconnect-federation-management/RepairADTrust2.PNG)</span><span class="sxs-lookup"><span data-stu-id="32d4c-138">![Connect to Azure AD](media/active-directory-aadconnect-federation-management/RepairADTrust2.PNG)</span></span>

3. <span data-ttu-id="32d4c-139">Op de **RAS-referenties** pagina, voert u de referenties voor de domeinbeheerder.</span><span class="sxs-lookup"><span data-stu-id="32d4c-139">On the **Remote access credentials** page, enter the credentials for the domain administrator.</span></span>

   ![Referenties voor externe toegang](media/active-directory-aadconnect-federation-management/RepairADTrust3.PNG)

    <span data-ttu-id="32d4c-141">Nadat u op **volgende**, Azure AD Connect health certificaat controleert en ziet u eventuele problemen.</span><span class="sxs-lookup"><span data-stu-id="32d4c-141">After you click **Next**, Azure AD Connect checks for certificate health and shows any issues.</span></span>

    ![Status van certificaten](media/active-directory-aadconnect-federation-management/RepairADTrust4.PNG)

    <span data-ttu-id="32d4c-143">De **klaar om te configureren** pagina bevat de lijst met acties die worden uitgevoerd om te herstellen van de vertrouwensrelatie.</span><span class="sxs-lookup"><span data-stu-id="32d4c-143">The **Ready to configure** page shows the list of actions that will be performed to repair the trust.</span></span>

    ![Klaar om te configureren](media/active-directory-aadconnect-federation-management/RepairADTrust5.PNG)

4. <span data-ttu-id="32d4c-145">Klik op **installeren** te herstellen van de vertrouwensrelatie.</span><span class="sxs-lookup"><span data-stu-id="32d4c-145">Click **Install** to repair the trust.</span></span>

> [!NOTE]
> <span data-ttu-id="32d4c-146">Azure AD Connect kan alleen herstellen of act op certificaten die zelf-ondertekend zijn.</span><span class="sxs-lookup"><span data-stu-id="32d4c-146">Azure AD Connect can only repair or act on certificates that are self-signed.</span></span> <span data-ttu-id="32d4c-147">Azure AD Connect-certificaten van derden niet worden hersteld.</span><span class="sxs-lookup"><span data-stu-id="32d4c-147">Azure AD Connect can't repair third-party certificates.</span></span>

## <span data-ttu-id="32d4c-148">Gefedereerd met Azure AD dat gebruikmaakt van AlternateID<a name=alternateid></a></span><span class="sxs-lookup"><span data-stu-id="32d4c-148">Federate with Azure AD using AlternateID <a name=alternateid></a></span></span>
<span data-ttu-id="32d4c-149">Het wordt aanbevolen dat de lokale gebruiker Principal Name(UPN) en de cloud principalnaam van gebruiker hetzelfde blijven.</span><span class="sxs-lookup"><span data-stu-id="32d4c-149">It is recommended that the on-premises User Principal Name(UPN) and the cloud User Principal Name are kept the same.</span></span> <span data-ttu-id="32d4c-150">Als de UPN van de lokale gebruikmaakt van een niet-routeerbare domein (ex.</span><span class="sxs-lookup"><span data-stu-id="32d4c-150">If the on-premises UPN uses a non-routable domain (ex.</span></span> <span data-ttu-id="32d4c-151">Contoso.local) of kan niet worden gewijzigd vanwege lokale toepassingsafhankelijkheden, wordt aangeraden instellen van de alternatieve aanmeldings-ID.</span><span class="sxs-lookup"><span data-stu-id="32d4c-151">Contoso.local) or cannot be changed due to local application dependencies, we recommend setting up alternate login ID.</span></span> <span data-ttu-id="32d4c-152">Alternatieve aanmeldings-ID kunt u een aanmeldingservaring configureren waarbij gebruikers zich kunnen aanmelden met een kenmerk dan de UPN, zoals e-mail.</span><span class="sxs-lookup"><span data-stu-id="32d4c-152">Alternate login ID allows you to configure a sign-in experience where users can sign in with an attribute other than their UPN, such as mail.</span></span> <span data-ttu-id="32d4c-153">De keuze voor principalnaam van gebruiker in Azure AD Connect wordt standaard ingesteld op het kenmerk userPrincipalName in Active Directory.</span><span class="sxs-lookup"><span data-stu-id="32d4c-153">The choice for User Principal Name in Azure AD Connect defaults to the userPrincipalName attribute in Active Directory.</span></span> <span data-ttu-id="32d4c-154">Als u een ander kenmerk voor de principalnaam van gebruiker kiezen en zijn Federatie met AD FS, vervolgens Azure AD Connect AD FS wilt configureren voor alternatieve aanmeldings-ID.</span><span class="sxs-lookup"><span data-stu-id="32d4c-154">If you choose any other attribute for User Principal Name and are federating using AD FS, then Azure AD Connect will configure AD FS for alternate login ID.</span></span> <span data-ttu-id="32d4c-155">Een voorbeeld van het kiezen van een ander kenmerk voor User Principal Name wordt hieronder weergegeven:</span><span class="sxs-lookup"><span data-stu-id="32d4c-155">An example of choosing a different attribute for User Principal Name is shown below:</span></span>

![Selectie van alternatieve ID-kenmerk](media/active-directory-aadconnect-federation-management/attributeselection.png)

<span data-ttu-id="32d4c-157">Alternatieve aanmeldings-ID configureren voor AD FS bestaat uit twee belangrijke stappen:</span><span class="sxs-lookup"><span data-stu-id="32d4c-157">Configuring alternate login ID for AD FS consists of two main steps:</span></span>
1. <span data-ttu-id="32d4c-158">**Configureer de juiste set met uitgifteregels claims**: claimregels voor de uitgifte van de Azure AD relying party trust voor het gebruik van het geselecteerde kenmerk UserPrincipalName als alternatieve-ID van de gebruiker worden gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="32d4c-158">**Configure the right set of issuance claims**: The issuance claim rules in the Azure AD relying party trust are modified to use the selected UserPrincipalName attribute as the alternate ID of the user.</span></span>
2. <span data-ttu-id="32d4c-159">**Schakel alternatieve aanmeldings-ID in de AD FS-configuratie**: de AD FS-configuratie is bijgewerkt, zodat AD FS kunt opzoeken van de gebruikers in de juiste forests met behulp van de alternatieve-ID.</span><span class="sxs-lookup"><span data-stu-id="32d4c-159">**Enable alternate login ID in the AD FS configuration**: The AD FS configuration is updated so that AD FS can look up users in the appropriate forests using the alternate ID.</span></span> <span data-ttu-id="32d4c-160">Deze configuratie wordt ondersteund voor AD FS in Windows Server 2012 R2 (met KB2919355) of hoger.</span><span class="sxs-lookup"><span data-stu-id="32d4c-160">This configuration is supported for AD FS on Windows Server 2012 R2 (with KB2919355) or later.</span></span> <span data-ttu-id="32d4c-161">Als de AD FS-servers 2012 R2 zijn, controleert de Azure AD Connect op de aanwezigheid van de vereiste KB.</span><span class="sxs-lookup"><span data-stu-id="32d4c-161">If the AD FS servers are 2012 R2, Azure AD Connect checks for the presence of the required KB.</span></span> <span data-ttu-id="32d4c-162">Als de KB niet wordt gedetecteerd, wordt een waarschuwing weergegeven nadat de configuratie is voltooid, zoals hieronder wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="32d4c-162">If the KB is not detected, a warning will be displayed after configuration completes, as shown below:</span></span>

    ![Waarschuwing voor KB op 2012R2 ontbreekt](media/active-directory-aadconnect-federation-management/kbwarning.png)

    <span data-ttu-id="32d4c-164">Installeer de vereiste op te lossen de configuratie in geval van een ontbrekende KB, [KB2919355](http://go.microsoft.com/fwlink/?LinkID=396590) en herstel daarna de vertrouwensrelatie met behulp van [AAD herstellen en AD FS-vertrouwensrelatie](#repairthetrust).</span><span class="sxs-lookup"><span data-stu-id="32d4c-164">To rectify the configuration in case of missing KB, install the required [KB2919355](http://go.microsoft.com/fwlink/?LinkID=396590) and then repair the trust using [Repair AAD and AD FS Trust](#repairthetrust).</span></span>

> [!NOTE]
> <span data-ttu-id="32d4c-165">Lees voor meer informatie over alternateID en stappen voor het handmatig configureren [Configuring Alternate Login ID](https://technet.microsoft.com/windows-server-docs/identity/ad-fs/operations/configuring-alternate-login-id)</span><span class="sxs-lookup"><span data-stu-id="32d4c-165">For more information on alternateID and steps to manually configure, read [Configuring Alternate Login ID](https://technet.microsoft.com/windows-server-docs/identity/ad-fs/operations/configuring-alternate-login-id)</span></span>

## <span data-ttu-id="32d4c-166">Een AD FS-server toevoegen<a name=addadfsserver></a></span><span class="sxs-lookup"><span data-stu-id="32d4c-166">Add an AD FS server <a name=addadfsserver></a></span></span>

> [!NOTE]
> <span data-ttu-id="32d4c-167">Azure AD Connect vereist voor het toevoegen van een AD FS-server, het PFX-certificaat.</span><span class="sxs-lookup"><span data-stu-id="32d4c-167">To add an AD FS server, Azure AD Connect requires the PFX certificate.</span></span> <span data-ttu-id="32d4c-168">Daarom kunt u deze bewerking uitvoeren als u de AD FS-farm met behulp van Azure AD Connect geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="32d4c-168">Therefore, you can perform this operation only if you configured the AD FS farm by using Azure AD Connect.</span></span>

1. <span data-ttu-id="32d4c-169">Selecteer **een extra federatieserver implementeren**, en klik op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="32d4c-169">Select **Deploy an additional Federation Server**, and click **Next**.</span></span>

   ![Extra federatieserver](media/active-directory-aadconnect-federation-management/AddNewADFSServer1.PNG)

2. <span data-ttu-id="32d4c-171">Op de **verbinding maken met Azure AD** pagina, Geef uw referenties hoofdbeheerder voor Azure AD en klikt u op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="32d4c-171">On the **Connect to Azure AD** page, enter your global administrator credentials for Azure AD, and click **Next**.</span></span>

   ![Verbinding maken met Azure AD](media/active-directory-aadconnect-federation-management/AddNewADFSServer2.PNG)

3. <span data-ttu-id="32d4c-173">Geef het domein beheerdersreferenties.</span><span class="sxs-lookup"><span data-stu-id="32d4c-173">Provide the domain administrator credentials.</span></span>

   ![Referenties voor de domeinbeheerder](media/active-directory-aadconnect-federation-management/AddNewADFSServer3.PNG)

4. <span data-ttu-id="32d4c-175">Azure AD Connect wordt u gevraagd om het wachtwoord van het PFX-bestand dat u hebt opgegeven tijdens het configureren van uw nieuwe AD FS-farm met Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="32d4c-175">Azure AD Connect asks for the password of the PFX file that you provided while configuring your new AD FS farm with Azure AD Connect.</span></span> <span data-ttu-id="32d4c-176">Klik op **wachtwoord invoeren** het wachtwoord opgeven voor het PFX-bestand.</span><span class="sxs-lookup"><span data-stu-id="32d4c-176">Click **Enter Password** to provide the password for the PFX file.</span></span>

   ![Certificaatwachtwoord](media/active-directory-aadconnect-federation-management/AddNewADFSServer4.PNG)

    ![SSL-certificaat opgeven](media/active-directory-aadconnect-federation-management/AddNewADFSServer5.PNG)

5. <span data-ttu-id="32d4c-179">Op de **AD FS-Servers** pagina, voert u de servernaam of IP-adres moet worden toegevoegd aan de AD FS-farm.</span><span class="sxs-lookup"><span data-stu-id="32d4c-179">On the **AD FS Servers** page, enter the server name or IP address to be added to the AD FS farm.</span></span>

   ![AD FS-servers](media/active-directory-aadconnect-federation-management/AddNewADFSServer6.PNG)

6. <span data-ttu-id="32d4c-181">Klik op **volgende**, en Ga via de laatste **configureren** pagina.</span><span class="sxs-lookup"><span data-stu-id="32d4c-181">Click **Next**, and go through the final **Configure** page.</span></span> <span data-ttu-id="32d4c-182">Nadat Azure AD Connect is voltooid op de servers toe te voegen aan de AD FS-farm, krijgt u de optie om te controleren of de connectiviteit.</span><span class="sxs-lookup"><span data-stu-id="32d4c-182">After Azure AD Connect has finished adding the servers to the AD FS farm, you will be given the option to verify the connectivity.</span></span>

   ![Klaar om te configureren](media/active-directory-aadconnect-federation-management/AddNewADFSServer7.PNG)

    ![Installatie voltooid](media/active-directory-aadconnect-federation-management/AddNewADFSServer8.PNG)

## <span data-ttu-id="32d4c-185">Een AD FS WAP-server toevoegen<a name=addwapserver></a></span><span class="sxs-lookup"><span data-stu-id="32d4c-185">Add an AD FS WAP server <a name=addwapserver></a></span></span>

> [!NOTE]
> <span data-ttu-id="32d4c-186">Als u wilt een WAP-server toevoegt, wordt in Azure AD Connect het PFX-certificaat vereist.</span><span class="sxs-lookup"><span data-stu-id="32d4c-186">To add a WAP server, Azure AD Connect requires the PFX certificate.</span></span> <span data-ttu-id="32d4c-187">Daarom kunt u deze bewerking alleen uitvoeren als u de AD FS-farm met behulp van Azure AD Connect geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="32d4c-187">Therefore, you can only perform this operation if you configured the AD FS farm by using Azure AD Connect.</span></span>

1. <span data-ttu-id="32d4c-188">Selecteer **Web Application Proxy implementeren** uit de lijst met beschikbare taken.</span><span class="sxs-lookup"><span data-stu-id="32d4c-188">Select **Deploy Web Application Proxy** from the list of available tasks.</span></span>

   ![Webtoepassingsproxy implementeren](media/active-directory-aadconnect-federation-management/WapServer1.PNG)

2. <span data-ttu-id="32d4c-190">Geef de referenties van de globale beheerder van Azure.</span><span class="sxs-lookup"><span data-stu-id="32d4c-190">Provide the Azure global administrator credentials.</span></span>

   ![Verbinding maken met Azure AD](media/active-directory-aadconnect-federation-management/wapserver2.PNG)

3. <span data-ttu-id="32d4c-192">Op de **Geef SSL-certificaat** pagina, geeft u het wachtwoord voor het PFX-bestand dat u hebt opgegeven toen u de AD FS-farm met Azure AD Connect geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="32d4c-192">On the **Specify SSL certificate** page, provide the password for the PFX file that you provided when you configured the AD FS farm with Azure AD Connect.</span></span>
   <span data-ttu-id="32d4c-193">![Certificaatwachtwoord](media/active-directory-aadconnect-federation-management/WapServer3.PNG)</span><span class="sxs-lookup"><span data-stu-id="32d4c-193">![Certificate password](media/active-directory-aadconnect-federation-management/WapServer3.PNG)</span></span>

    ![SSL-certificaat opgeven](media/active-directory-aadconnect-federation-management/WapServer4.PNG)

4. <span data-ttu-id="32d4c-195">De server moet worden toegevoegd als een WAP-server toevoegen.</span><span class="sxs-lookup"><span data-stu-id="32d4c-195">Add the server to be added as a WAP server.</span></span> <span data-ttu-id="32d4c-196">Omdat de WAP-server kan niet worden toegevoegd aan het domein, vraagt de wizard om beheerdersreferenties op de server die wordt toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="32d4c-196">Because the WAP server might not be joined to the domain, the wizard asks for administrative credentials to the server being added.</span></span>

   ![Referenties van de beheerserver](media/active-directory-aadconnect-federation-management/WapServer5.PNG)

5. <span data-ttu-id="32d4c-198">Op de **vertrouwensrelatie proxyreferenties** beheerdersreferenties voor het configureren van de proxy vertrouwen en toegang tot de primaire server in de AD FS-farm.</span><span class="sxs-lookup"><span data-stu-id="32d4c-198">On the **Proxy trust credentials** page, provide administrative credentials to configure the proxy trust and access the primary server in the AD FS farm.</span></span>

   ![Vertrouwensrelatie proxyreferenties](media/active-directory-aadconnect-federation-management/WapServer6.PNG)

6. <span data-ttu-id="32d4c-200">Op de **klaar om te configureren** pagina de wizard geeft de lijst met acties die worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="32d4c-200">On the **Ready to configure** page, the wizard shows the list of actions that will be performed.</span></span>

   ![Klaar om te configureren](media/active-directory-aadconnect-federation-management/WapServer7.PNG)

7. <span data-ttu-id="32d4c-202">Klik op **installeren** om de configuratie te voltooien.</span><span class="sxs-lookup"><span data-stu-id="32d4c-202">Click **Install** to finish the configuration.</span></span> <span data-ttu-id="32d4c-203">Nadat de configuratie voltooid is, kunt u de wizard de optie om te controleren of de verbinding met de servers.</span><span class="sxs-lookup"><span data-stu-id="32d4c-203">After the configuration is complete, the wizard gives you the option to verify the connectivity to the servers.</span></span> <span data-ttu-id="32d4c-204">Klik op **controleren** connectiviteit controleren.</span><span class="sxs-lookup"><span data-stu-id="32d4c-204">Click **Verify** to check connectivity.</span></span>

   ![Installatie voltooid](media/active-directory-aadconnect-federation-management/WapServer8.PNG)

## <span data-ttu-id="32d4c-206">Een federatieve domein toevoegen<a name=addfeddomain></a></span><span class="sxs-lookup"><span data-stu-id="32d4c-206">Add a federated domain <a name=addfeddomain></a></span></span>

<span data-ttu-id="32d4c-207">Het is gemakkelijk om toe te voegen van een domein dat gefedereerd met Azure AD met behulp van Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="32d4c-207">It's easy to add a domain to be federated with Azure AD by using Azure AD Connect.</span></span> <span data-ttu-id="32d4c-208">Azure AD Connect wordt het domein voor Federatie en wijzigt de claimregels naar aanleiding van de verlener correct wanneer er meerdere domeinen die zijn gefedereerd met Azure AD.</span><span class="sxs-lookup"><span data-stu-id="32d4c-208">Azure AD Connect adds the domain for federation and modifies the claim rules to correctly reflect the issuer when you have multiple domains federated with Azure AD.</span></span>

1. <span data-ttu-id="32d4c-209">Als u wilt een federatieve domein toevoegt, selecteert u de taak **toevoegen van een extra Azure AD-domein**.</span><span class="sxs-lookup"><span data-stu-id="32d4c-209">To add a federated domain, select the task **Add an additional Azure AD domain**.</span></span>

   ![Extra Azure AD-domein](media/active-directory-aadconnect-federation-management/AdditionalDomain1.PNG)

2. <span data-ttu-id="32d4c-211">Geef de referenties van de hoofdbeheerder voor Azure AD op de volgende pagina van de wizard.</span><span class="sxs-lookup"><span data-stu-id="32d4c-211">On the next page of the wizard, provide the global administrator credentials for Azure AD.</span></span>

   ![Verbinding maken met Azure AD](media/active-directory-aadconnect-federation-management/AdditionalDomain2.PNG)

3. <span data-ttu-id="32d4c-213">Op de **RAS-referenties** pagina, beheerdersreferenties voor het domein opgeven.</span><span class="sxs-lookup"><span data-stu-id="32d4c-213">On the **Remote access credentials** page, provide the domain administrator credentials.</span></span>

   ![Referenties voor externe toegang](media/active-directory-aadconnect-federation-management/additionaldomain3.PNG)

4. <span data-ttu-id="32d4c-215">Op de volgende pagina biedt de wizard een lijst met Azure AD-domeinen die u kunt uw on-premises directory met federeren.</span><span class="sxs-lookup"><span data-stu-id="32d4c-215">On the next page, the wizard provides a list of Azure AD domains that you can federate your on-premises directory with.</span></span> <span data-ttu-id="32d4c-216">Kies het domein in de lijst.</span><span class="sxs-lookup"><span data-stu-id="32d4c-216">Choose the domain from the list.</span></span>

   ![Azure AD-domein](media/active-directory-aadconnect-federation-management/AdditionalDomain4.PNG)

    <span data-ttu-id="32d4c-218">Nadat u ervoor het domein kiest, de wizard kunt u met de juiste informatie over verdere acties die de wizard wordt uitgevoerd en de impact van de configuratie.</span><span class="sxs-lookup"><span data-stu-id="32d4c-218">After you choose the domain, the wizard provides you with appropriate information about further actions that the wizard will take and the impact of the configuration.</span></span> <span data-ttu-id="32d4c-219">In sommige gevallen, als u een domein dat nog niet is geverifieerd in Azure AD, selecteert biedt de wizard u informatie over het controleren van het domein.</span><span class="sxs-lookup"><span data-stu-id="32d4c-219">In some cases, if you select a domain that isn't yet verified in Azure AD, the wizard provides you with information to help you verify the domain.</span></span> <span data-ttu-id="32d4c-220">Zie [uw aangepaste domeinnaam toevoegen aan Azure Active Directory](../active-directory-add-domain.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="32d4c-220">See [Add your custom domain name to Azure Active Directory](../active-directory-add-domain.md) for more details.</span></span>

5. <span data-ttu-id="32d4c-221">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="32d4c-221">Click **Next**.</span></span> <span data-ttu-id="32d4c-222">De **klaar om te configureren** pagina bevat de lijst met acties die door Azure AD Connect worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="32d4c-222">The **Ready to configure** page shows the list of actions that Azure AD Connect will perform.</span></span> <span data-ttu-id="32d4c-223">Klik op **installeren** om de configuratie te voltooien.</span><span class="sxs-lookup"><span data-stu-id="32d4c-223">Click **Install** to finish the configuration.</span></span>

   ![Klaar om te configureren](media/active-directory-aadconnect-federation-management/AdditionalDomain5.PNG)

> [!NOTE]
> <span data-ttu-id="32d4c-225">Gebruikers van de toegevoegde federatieve domein moeten worden gesynchroniseerd voordat ze zich aanmelden bij Azure AD.</span><span class="sxs-lookup"><span data-stu-id="32d4c-225">Users from the added federated domain must be synchronized before they will be able to login to Azure AD.</span></span>

## <a name="ad-fs-customization"></a><span data-ttu-id="32d4c-226">AD FS-aanpassing</span><span class="sxs-lookup"><span data-stu-id="32d4c-226">AD FS customization</span></span>
<span data-ttu-id="32d4c-227">De volgende secties geven informatie over een aantal algemene taken die u wellicht moet worden uitgevoerd wanneer u uw AD FS-aanmeldingspagina aanpassen.</span><span class="sxs-lookup"><span data-stu-id="32d4c-227">The following sections provide details about some of the common tasks that you might have to perform when you customize your AD FS sign-in page.</span></span>

## <span data-ttu-id="32d4c-228">Een aangepast bedrijfslogo of afbeelding toevoegen<a name=customlogo></a></span><span class="sxs-lookup"><span data-stu-id="32d4c-228">Add a custom company logo or illustration <a name=customlogo></a></span></span>
<span data-ttu-id="32d4c-229">Wijzigen van het logo van het bedrijf dat wordt weergegeven op de **aanmelden** pagina, gebruikt u de volgende Windows PowerShell-cmdlet en syntaxis.</span><span class="sxs-lookup"><span data-stu-id="32d4c-229">To change the logo of the company that's displayed on the **Sign-in** page, use the following Windows PowerShell cmdlet and syntax.</span></span>

> [!NOTE]
> <span data-ttu-id="32d4c-230">De aanbevolen dimensies voor het logo wordt 260 x 35 96 dpi-waarde met een bestandsgrootte van niet meer dan 10 KB.</span><span class="sxs-lookup"><span data-stu-id="32d4c-230">The recommended dimensions for the logo are 260 x 35 @ 96 dpi with a file size no greater than 10 KB.</span></span>

    Set-AdfsWebTheme -TargetName default -Logo @{path="c:\Contoso\logo.PNG"}

> [!NOTE]
> <span data-ttu-id="32d4c-231">De *TargetName* parameter is vereist.</span><span class="sxs-lookup"><span data-stu-id="32d4c-231">The *TargetName* parameter is required.</span></span> <span data-ttu-id="32d4c-232">De naam van het standaardthema dat wordt geleverd met AD FS is standaard.</span><span class="sxs-lookup"><span data-stu-id="32d4c-232">The default theme that's released with AD FS is named Default.</span></span>

## <span data-ttu-id="32d4c-233">Een beschrijving van de aanmeldingspagina toevoegen<a name=addsignindescription></a></span><span class="sxs-lookup"><span data-stu-id="32d4c-233">Add a sign-in description <a name=addsignindescription></a></span></span>
<span data-ttu-id="32d4c-234">Toevoegen van een beschrijving van de aanmeldingspagina in de **aanmeldingspagina**, gebruik de volgende Windows PowerShell-cmdlet en syntaxis.</span><span class="sxs-lookup"><span data-stu-id="32d4c-234">To add a sign-in page description to the **Sign-in page**, use the following Windows PowerShell cmdlet and syntax.</span></span>

    Set-AdfsGlobalWebContent -SignInPageDescriptionText "<p>Sign-in to Contoso requires device registration. Click <A href='http://fs1.contoso.com/deviceregistration/'>here</A> for more information.</p>"

## <span data-ttu-id="32d4c-235">Wijzigen van de claimregels van AD FS<a name=modclaims></a></span><span class="sxs-lookup"><span data-stu-id="32d4c-235">Modify AD FS claim rules <a name=modclaims></a></span></span>
<span data-ttu-id="32d4c-236">AD FS biedt ondersteuning voor een uitgebreide claim taal die u kunt aangepaste claimregels maken.</span><span class="sxs-lookup"><span data-stu-id="32d4c-236">AD FS supports a rich claim language that you can use to create custom claim rules.</span></span> <span data-ttu-id="32d4c-237">Zie voor meer informatie [de rol van de Claimregeltaal](https://technet.microsoft.com/library/dd807118.aspx).</span><span class="sxs-lookup"><span data-stu-id="32d4c-237">For more information, see [The Role of the Claim Rule Language](https://technet.microsoft.com/library/dd807118.aspx).</span></span>

<span data-ttu-id="32d4c-238">De volgende secties wordt beschreven hoe u aangepaste regels voor sommige scenario's met betrekking tot Azure AD kan schrijven en AD FS-federatie.</span><span class="sxs-lookup"><span data-stu-id="32d4c-238">The following sections describe how you can write custom rules for some scenarios that relate to Azure AD and AD FS federation.</span></span>

### <a name="immutable-id-conditional-on-a-value-being-present-in-the-attribute"></a><span data-ttu-id="32d4c-239">Niet-wijzigbaar voorwaardelijke op een waarde in het kenmerk-ID</span><span class="sxs-lookup"><span data-stu-id="32d4c-239">Immutable ID conditional on a value being present in the attribute</span></span>
<span data-ttu-id="32d4c-240">Azure AD Connect kunt u opgeven van een kenmerk moet worden gebruikt als een bronanker wanneer objecten worden gesynchroniseerd met Azure AD.</span><span class="sxs-lookup"><span data-stu-id="32d4c-240">Azure AD Connect lets you specify an attribute to be used as a source anchor when objects are synced to Azure AD.</span></span> <span data-ttu-id="32d4c-241">Als de waarde in het aangepaste kenmerk niet leeg is, is het raadzaam een onveranderbare ID-claim uitgeven.</span><span class="sxs-lookup"><span data-stu-id="32d4c-241">If the value in the custom attribute is not empty, you might want to issue an immutable ID claim.</span></span>

<span data-ttu-id="32d4c-242">Bijvoorbeeld, kunt u selecteren **ms-ds-consistencyguid** als het kenmerk voor het bronanker en probleem **onveranderbare id genoemd** als **ms-ds-consistencyguid** in geval van het kenmerk heeft een waarde op basis van deze.</span><span class="sxs-lookup"><span data-stu-id="32d4c-242">For example, you might select **ms-ds-consistencyguid** as the attribute for the source anchor and issue **ImmutableID** as **ms-ds-consistencyguid** in case the attribute has a value against it.</span></span> <span data-ttu-id="32d4c-243">Als er geen waarde op basis van het kenmerk is, geven **objectGuid** als de niet-wijzigbaar-ID.</span><span class="sxs-lookup"><span data-stu-id="32d4c-243">If there's no value against the attribute, issue **objectGuid** as the immutable ID.</span></span> <span data-ttu-id="32d4c-244">U kunt de reeks aangepaste claimregels zoals beschreven in de volgende sectie opstellen.</span><span class="sxs-lookup"><span data-stu-id="32d4c-244">You can construct the set of custom claim rules as described in the following section.</span></span>

<span data-ttu-id="32d4c-245">**Regel 1: Querykenmerken**</span><span class="sxs-lookup"><span data-stu-id="32d4c-245">**Rule 1: Query attributes**</span></span>

    c:[Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname"]
    => add(store = "Active Directory", types = ("http://contoso.com/ws/2016/02/identity/claims/objectguid", "http://contoso.com/ws/2016/02/identity/claims/msdsconsistencyguid"), query = "; objectGuid,ms-ds-consistencyguid;{0}", param = c.Value);

<span data-ttu-id="32d4c-246">In deze regel, waaruit u de waarden van gegevens ophaalt **ms-ds-consistencyguid** en **objectGuid** voor de gebruiker uit Active Directory.</span><span class="sxs-lookup"><span data-stu-id="32d4c-246">In this rule, you're querying the values of **ms-ds-consistencyguid** and **objectGuid** for the user from Active Directory.</span></span> <span data-ttu-id="32d4c-247">Wijzig de naam van de store naar de naam van een juiste store in uw AD FS-implementatie.</span><span class="sxs-lookup"><span data-stu-id="32d4c-247">Change the store name to an appropriate store name in your AD FS deployment.</span></span> <span data-ttu-id="32d4c-248">Ook wijzigen, typt u de claims naar het juiste type voor uw federatieserver claims zoals is gedefinieerd voor **objectGuid** en **ms-ds-consistencyguid**.</span><span class="sxs-lookup"><span data-stu-id="32d4c-248">Also change the claims type to a proper claims type for your federation, as defined for **objectGuid** and **ms-ds-consistencyguid**.</span></span>

<span data-ttu-id="32d4c-249">Ook met behulp van **toevoegen** en niet **probleem**, u te voorkomen dat een uitgaande probleem voor de entiteit toe te voegen en de waarden als tussenliggende waarden kunt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="32d4c-249">Also, by using **add** and not **issue**, you avoid adding an outgoing issue for the entity, and can use the values as intermediate values.</span></span> <span data-ttu-id="32d4c-250">Geeft u de claim uit in een latere regel nadat u hebt vastgesteld welke waarde om te gebruiken als de niet-wijzigbaar-ID.</span><span class="sxs-lookup"><span data-stu-id="32d4c-250">You will issue the claim in a later rule after you establish which value to use as the immutable ID.</span></span>

<span data-ttu-id="32d4c-251">**Regel 2: Controleer of de ds-ms-consistencyguid voor de gebruiker bestaat**</span><span class="sxs-lookup"><span data-stu-id="32d4c-251">**Rule 2: Check if ms-ds-consistencyguid exists for the user**</span></span>

    NOT EXISTS([Type == "http://contoso.com/ws/2016/02/identity/claims/msdsconsistencyguid"])
    => add(Type = "urn:anandmsft:tmp/idflag", Value = "useguid");

<span data-ttu-id="32d4c-252">Deze regel definieert een tijdelijke vlag aangeroepen **idflag** die is ingesteld op **useguid** als er geen **ms-ds-consistencyguid** ingevuld voor de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="32d4c-252">This rule defines a temporary flag called **idflag** that is set to **useguid** if there's no **ms-ds-consistencyguid** populated for the user.</span></span> <span data-ttu-id="32d4c-253">De logica achter dit is het feit dat AD FS leeg claims niet toegestaan.</span><span class="sxs-lookup"><span data-stu-id="32d4c-253">The logic behind this is the fact that AD FS doesn't allow empty claims.</span></span> <span data-ttu-id="32d4c-254">Dus als u claims http://contoso.com/ws/2016/02/identity/claims/objectguid en http://contoso.com/ws/2016/02/identity/claims/msdsconsistencyguid in regel 1 toevoegt, u uiteindelijk met eindigen een **msdsconsistencyguid** claim alleen als de waarde wordt voor de gebruiker gevuld.</span><span class="sxs-lookup"><span data-stu-id="32d4c-254">So when you add claims http://contoso.com/ws/2016/02/identity/claims/objectguid and http://contoso.com/ws/2016/02/identity/claims/msdsconsistencyguid in Rule 1, you end up with an **msdsconsistencyguid** claim only if the value is populated for the user.</span></span> <span data-ttu-id="32d4c-255">Als deze niet is ingevuld, wordt AD FS ziet dat het een lege waarde hebben en onmiddellijk verwijderd.</span><span class="sxs-lookup"><span data-stu-id="32d4c-255">If it isn't populated, AD FS sees that it will have an empty value and drops it immediately.</span></span> <span data-ttu-id="32d4c-256">Alle objecten hebben **objectGuid**, zodat deze claim wordt altijd er nadat regel 1 wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="32d4c-256">All objects will have **objectGuid**, so that claim will always be there after Rule 1 is executed.</span></span>

<span data-ttu-id="32d4c-257">**Regel 3: Ms-ds-consistencyguid verlenen als niet-wijzigbaar ID indien aanwezig**</span><span class="sxs-lookup"><span data-stu-id="32d4c-257">**Rule 3: Issue ms-ds-consistencyguid as immutable ID if it's present**</span></span>

    c:[Type == "http://contoso.com/ws/2016/02/identity/claims/msdsconsistencyguid"]
    => issue(Type = "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier", Value = c.Value);

<span data-ttu-id="32d4c-258">Dit is een impliciete **Exist** controleren.</span><span class="sxs-lookup"><span data-stu-id="32d4c-258">This is an implicit **Exist** check.</span></span> <span data-ttu-id="32d4c-259">Als de waarde voor de claim bestaat, klikt u vervolgens uitgeeft die als de niet-wijzigbaar-ID.</span><span class="sxs-lookup"><span data-stu-id="32d4c-259">If the value for the claim exists, then issue that as the immutable ID.</span></span> <span data-ttu-id="32d4c-260">In het vorige voorbeeld wordt de **nameidentifier** claim.</span><span class="sxs-lookup"><span data-stu-id="32d4c-260">The previous example uses the **nameidentifier** claim.</span></span> <span data-ttu-id="32d4c-261">U hebt dit wijzigen in het juiste claimtype voor de ID van de niet-wijzigbaar in uw omgeving.</span><span class="sxs-lookup"><span data-stu-id="32d4c-261">You'll have to change this to the appropriate claim type for the immutable ID in your environment.</span></span>

<span data-ttu-id="32d4c-262">**Regel 4: ObjectGuid verlenen als niet-wijzigbaar-ID als ms-ds-consistencyGuid niet aanwezig is**</span><span class="sxs-lookup"><span data-stu-id="32d4c-262">**Rule 4: Issue objectGuid as immutable ID if ms-ds-consistencyGuid is not present**</span></span>

    c1:[Type == "urn:anandmsft:tmp/idflag", Value =~ "useguid"]
    && c2:[Type == "http://contoso.com/ws/2016/02/identity/claims/objectguid"]
    => issue(Type = "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier", Value = c2.Value);

<span data-ttu-id="32d4c-263">In deze regel, bent u gewoon de tijdelijke vlag controleren **idflag**.</span><span class="sxs-lookup"><span data-stu-id="32d4c-263">In this rule, you're simply checking the temporary flag **idflag**.</span></span> <span data-ttu-id="32d4c-264">U beslissen of u de claim uitgeven op basis van de waarde.</span><span class="sxs-lookup"><span data-stu-id="32d4c-264">You decide whether to issue the claim based on its value.</span></span>

> [!NOTE]
> <span data-ttu-id="32d4c-265">De volgorde van deze regels is belangrijk.</span><span class="sxs-lookup"><span data-stu-id="32d4c-265">The sequence of these rules is important.</span></span>

### <a name="sso-with-a-subdomain-upn"></a><span data-ttu-id="32d4c-266">Eenmalige aanmelding met een subdomein UPN</span><span class="sxs-lookup"><span data-stu-id="32d4c-266">SSO with a subdomain UPN</span></span>
<span data-ttu-id="32d4c-267">U kunt meer dan één domein dat gefedereerd met behulp van Azure AD Connect, zoals beschreven in toevoegen [toevoegen van een nieuwe federatieve domein](active-directory-aadconnect-federation-management.md#addfeddomain).</span><span class="sxs-lookup"><span data-stu-id="32d4c-267">You can add more than one domain to be federated by using Azure AD Connect, as described in [Add a new federated domain](active-directory-aadconnect-federation-management.md#addfeddomain).</span></span> <span data-ttu-id="32d4c-268">U moet de UPN (User Principal Name) Gebruikersclaim wijzigen zodat de uitgevers-ID komt met het hoofddomein en niet het subdomein overeen, omdat het federatieve hoofddomein ook de onderliggende vallen.</span><span class="sxs-lookup"><span data-stu-id="32d4c-268">You must modify the user principal name (UPN) claim so that the issuer ID corresponds to the root domain and not the subdomain, because the federated root domain also covers the child.</span></span>

<span data-ttu-id="32d4c-269">De claimregel voor uitgevers-ID is standaard ingesteld als:</span><span class="sxs-lookup"><span data-stu-id="32d4c-269">By default, the claim rule for issuer ID is set as:</span></span>

    c:[Type
    == “http://schemas.xmlsoap.org/claims/UPN“]

    => issue(Type = “http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid“, Value = regexreplace(c.Value, “.+@(?<domain>.+)“, “http://${domain}/adfs/services/trust/“));

![Standaard uitgever-ID claim](media/active-directory-aadconnect-federation-management/issuer_id_default.png)

<span data-ttu-id="32d4c-271">De standaardregel gewoon duurt het UPN-achtervoegsel en wordt gebruikt in de claim uitgever-ID.</span><span class="sxs-lookup"><span data-stu-id="32d4c-271">The default rule simply takes the UPN suffix and uses it in the issuer ID claim.</span></span> <span data-ttu-id="32d4c-272">Bijvoorbeeld: John is een gebruiker in sub.contoso.com en contoso.com is gefedereerd met Azure AD.</span><span class="sxs-lookup"><span data-stu-id="32d4c-272">For example, John is a user in sub.contoso.com, and contoso.com is federated with Azure AD.</span></span> <span data-ttu-id="32d4c-273">John voert john@sub.contoso.com als de gebruikersnaam tijdens het aanmelden bij Azure AD.</span><span class="sxs-lookup"><span data-stu-id="32d4c-273">John enters john@sub.contoso.com as the username while signing in to Azure AD.</span></span> <span data-ttu-id="32d4c-274">De claimregel standaard uitgever-ID in AD FS afhandelt op de volgende manier:</span><span class="sxs-lookup"><span data-stu-id="32d4c-274">The default issuer ID claim rule in AD FS handles it in the following manner:</span></span>

    c:[Type
    == “http://schemas.xmlsoap.org/claims/UPN“]

    => issue(Type = “http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid“, Value = regexreplace(john@sub.contoso.com, “.+@(?<domain>.+)“, “http://${domain}/adfs/services/trust/“));

<span data-ttu-id="32d4c-275">**Claimwaarde:** http://sub.contoso.com/adfs/services/trust/</span><span class="sxs-lookup"><span data-stu-id="32d4c-275">**Claim value:**  http://sub.contoso.com/adfs/services/trust/</span></span>

<span data-ttu-id="32d4c-276">Als u alleen het hoofddomein in de claimwaarde van de certificaatverlener wilt weergeven, wijzigen de claimregel zodat deze overeenkomt met het volgende:</span><span class="sxs-lookup"><span data-stu-id="32d4c-276">To have only the root domain in the issuer claim value, change the claim rule to match the following:</span></span>

    c:[Type == “http://schemas.xmlsoap.org/claims/UPN“]

    => issue(Type = “http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid“, Value = regexreplace(c.Value, “^((.*)([.|@]))?(?<domain>[^.]*[.].*)$”, “http://${domain}/adfs/services/trust/“));

## <a name="next-steps"></a><span data-ttu-id="32d4c-277">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="32d4c-277">Next steps</span></span>
<span data-ttu-id="32d4c-278">Meer informatie over [opties aanmelden gebruiker](active-directory-aadconnect-user-signin.md).</span><span class="sxs-lookup"><span data-stu-id="32d4c-278">Learn more about [user sign-in options](active-directory-aadconnect-user-signin.md).</span></span>

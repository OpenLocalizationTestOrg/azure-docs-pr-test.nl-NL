---
title: Het configureren van automatische registratie van Windows-domein-apparaten met Azure Active Directory | Microsoft Docs
description: Instellen van uw Windows-domein apparaten automatisch en zonder tussenkomst registreren bij Azure Active Directory.
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
ms.date: 06/16/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: dccd7df6a5f85df4179c7ea7cfc476cfb57f48c0
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-configure-automatic-registration-of-windows-domain-joined-devices-with-azure-active-directory"></a><span data-ttu-id="a2200-103">Automatische registratie van Windows-domein-apparaten met Azure Active Directory configureren</span><span class="sxs-lookup"><span data-stu-id="a2200-103">How to configure automatic registration of Windows domain-joined devices with Azure Active Directory</span></span>

<span data-ttu-id="a2200-104">Gebruik [voorwaardelijke toegang voor Azure Active Directory op basis van apparaten](active-directory-conditional-access-azure-portal.md), uw computers moeten worden geregistreerd bij Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a2200-104">To use [Azure Active Directory device-based conditional access](active-directory-conditional-access-azure-portal.md), your computers must be registered with Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="a2200-105">U kunt een lijst met geregistreerde apparaten krijgen in uw organisatie met behulp van de [Get-MsolDevice](https://docs.microsoft.com/powershell/msonline/v1/get-msoldevice) cmdlet in de [Azure Active Directory PowerShell-module](/powershell/azure/install-msonlinev1?view=azureadps-2.0).</span><span class="sxs-lookup"><span data-stu-id="a2200-105">You can get a list of registered devices in your organization by using the [Get-MsolDevice](https://docs.microsoft.com/powershell/msonline/v1/get-msoldevice) cmdlet in the [Azure Active Directory PowerShell module](/powershell/azure/install-msonlinev1?view=azureadps-2.0).</span></span> 

<span data-ttu-id="a2200-106">Dit artikel bevat de stappen voor het configureren van de automatische registratie van Windows-domein-apparaten met Azure AD in uw organisatie.</span><span class="sxs-lookup"><span data-stu-id="a2200-106">This article provides you with the steps for configuring the automatic registration of Windows domain-joined devices with Azure AD in your organization.</span></span>


<span data-ttu-id="a2200-107">Voor meer informatie over:</span><span class="sxs-lookup"><span data-stu-id="a2200-107">For more information about:</span></span>

- <span data-ttu-id="a2200-108">Voorwaardelijke toegang, Zie [voorwaardelijke toegang voor Azure Active Directory op basis van apparaten](active-directory-conditional-access-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="a2200-108">Conditional access, see [Azure Active Directory device-based conditional access](active-directory-conditional-access-azure-portal.md).</span></span> 
- <span data-ttu-id="a2200-109">Windows 10-apparaten in de werkplek en de uitgebreide ervaring als geregistreerd in Azure AD, Zie [Windows 10 voor ondernemingen: apparaten gebruiken voor het werk](active-directory-azureadjoin-windows10-devices-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a2200-109">Windows 10 devices in the workplace and the enhanced experiences when registered with Azure AD, see [Windows 10 for the enterprise: Use devices for work](active-directory-azureadjoin-windows10-devices-overview.md).</span></span>
- <span data-ttu-id="a2200-110">Windows 10 Enterprise E3 in CSP, Zie de [Windows 10 Enterprise E3 in het overzicht van de CSP](https://docs.microsoft.com/en-us/windows/deployment/windows-10-enterprise-e3-overview).</span><span class="sxs-lookup"><span data-stu-id="a2200-110">Windows 10 Enterprise E3 in CSP, see the [Windows 10 Enterprise E3 in CSP Overview](https://docs.microsoft.com/en-us/windows/deployment/windows-10-enterprise-e3-overview).</span></span>


## <a name="before-you-begin"></a><span data-ttu-id="a2200-111">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="a2200-111">Before you begin</span></span>

<span data-ttu-id="a2200-112">Voordat u begint met het configureren van de automatische registratie van Windows-domein-apparaten in uw omgeving, moet u dat vertrouwd raken met de ondersteunde scenario's en de beperkingen.</span><span class="sxs-lookup"><span data-stu-id="a2200-112">Before you start configuring the automatic registration of Windows domain-joined devices in your environment, you should familiarize yourself with the supported scenarios and the constraints.</span></span>  

<span data-ttu-id="a2200-113">In dit onderwerp gebruikt ter verbetering van de leesbaarheid van de beschrijvingen van de volgende voorwaarden:</span><span class="sxs-lookup"><span data-stu-id="a2200-113">To improve the readability of the descriptions, this topic uses the following term:</span></span> 

- <span data-ttu-id="a2200-114">**Huidige Windows-apparaten** -deze term verwijst naar domein apparaten met Windows 10 of Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="a2200-114">**Windows current devices** - This term refers to domain-joined devices running Windows 10 or Windows Server 2016.</span></span>
- <span data-ttu-id="a2200-115">**Apparaten met Windows downlevel-** -deze term verwijst naar alle **ondersteund** domein Windows-apparaten die geen actieve Windows 10 of Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="a2200-115">**Windows down-level devices** - This term refers to all **supported** domain-joined Windows devices that are neither running Windows 10 nor Windows Server 2016.</span></span>  


### <a name="windows-current-devices"></a><span data-ttu-id="a2200-116">Huidige Windows-apparaten</span><span class="sxs-lookup"><span data-stu-id="a2200-116">Windows current devices</span></span>

- <span data-ttu-id="a2200-117">Voor apparaten waarop het besturingssysteem van de Windows-bureaublad wordt uitgevoerd, wordt u aangeraden speciale Update (versie 1607) voor Windows 10 of hoger.</span><span class="sxs-lookup"><span data-stu-id="a2200-117">For devices running the Windows desktop operating system, we recommend using Windows 10 Anniversary Update (version 1607) or later.</span></span> 
- <span data-ttu-id="a2200-118">De registratie van de huidige Windows-apparaten **is** in niet-gefedereerde omgevingen zoals wachtwoord-hash-synchronisatie configuraties ondersteund.</span><span class="sxs-lookup"><span data-stu-id="a2200-118">The registration of Windows current devices **is** supported in non-federated environments such as password hash sync configurations.</span></span>  


### <a name="windows-down-level-devices"></a><span data-ttu-id="a2200-119">Eerdere Windows-apparaten</span><span class="sxs-lookup"><span data-stu-id="a2200-119">Windows down-level devices</span></span>

- <span data-ttu-id="a2200-120">De volgende Windows downlevel-apparaten worden ondersteund:</span><span class="sxs-lookup"><span data-stu-id="a2200-120">The following Windows down-level devices are supported:</span></span>
    - <span data-ttu-id="a2200-121">Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="a2200-121">Windows 8.1</span></span>
    - <span data-ttu-id="a2200-122">Windows 7</span><span class="sxs-lookup"><span data-stu-id="a2200-122">Windows 7</span></span>
    - <span data-ttu-id="a2200-123">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="a2200-123">Windows Server 2012 R2</span></span>
    - <span data-ttu-id="a2200-124">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="a2200-124">Windows Server 2012</span></span>
    - <span data-ttu-id="a2200-125">Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="a2200-125">Windows Server 2008 R2</span></span>
- <span data-ttu-id="a2200-126">De registratie van apparaten met Windows downlevel- **is** in niet-gefedereerde omgevingen via naadloze eenmalige aanmelding ondersteund [Azure Active Directory naadloze eenmalige aanmelding](https://aka.ms/hybrid/sso).</span><span class="sxs-lookup"><span data-stu-id="a2200-126">The registration of Windows down-level devices **is** supported in non-federated environments through Seamless Single Sign On [Azure Active Directory Seamless Single Sign-On](https://aka.ms/hybrid/sso).</span></span>
- <span data-ttu-id="a2200-127">De registratie van apparaten met Windows downlevel- **is niet** ondersteund voor apparaten met behulp van zwervende profielen.</span><span class="sxs-lookup"><span data-stu-id="a2200-127">The registration of Windows down-level devices **is not** supported for devices using roaming profiles.</span></span> <span data-ttu-id="a2200-128">Als u gebruik van zwervende profielen of instellingen, gebruikt u Windows 10.</span><span class="sxs-lookup"><span data-stu-id="a2200-128">If you are relying on roaming of profiles or settings, use Windows 10.</span></span>



## <a name="prerequisites"></a><span data-ttu-id="a2200-129">Vereisten</span><span class="sxs-lookup"><span data-stu-id="a2200-129">Prerequisites</span></span>

<span data-ttu-id="a2200-130">Voordat u begint met het inschakelen van de automatische registratie van apparaten in uw organisatie lid van een domein, moet u ervoor zorgen dat u altijd een actuele versie van Azure AD connect.</span><span class="sxs-lookup"><span data-stu-id="a2200-130">Before you start enabling the auto-registration of domain-joined devices in your organization, you need to make sure that you are running an up-to-date version of Azure AD connect.</span></span>

<span data-ttu-id="a2200-131">Azure AD Connect:</span><span class="sxs-lookup"><span data-stu-id="a2200-131">Azure AD Connect:</span></span>

- <span data-ttu-id="a2200-132">Houdt de koppeling tussen de computeraccount in uw on-premises Active Directory (AD) en het apparaatobject in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a2200-132">Keeps the association between the computer account in your on-premises Active Directory (AD) and the device object in Azure AD.</span></span> 
- <span data-ttu-id="a2200-133">Andere apparaat gerelateerde functies, zoals Windows Hello voor bedrijven.</span><span class="sxs-lookup"><span data-stu-id="a2200-133">Enables other device related features like Windows Hello for Business.</span></span>



## <a name="configuration-steps"></a><span data-ttu-id="a2200-134">Configuratiestappen</span><span class="sxs-lookup"><span data-stu-id="a2200-134">Configuration steps</span></span>

<span data-ttu-id="a2200-135">Dit onderwerp bevat de vereiste stappen voor alle standaardconfiguratie-scenario's.</span><span class="sxs-lookup"><span data-stu-id="a2200-135">This topic includes the required steps for all typical configuration scenarios.</span></span>  
<span data-ttu-id="a2200-136">Gebruik de volgende tabel om een overzicht van de stappen die nodig voor uw scenario zijn:</span><span class="sxs-lookup"><span data-stu-id="a2200-136">Use the following table to get an overview of the steps that are required for your scenario:</span></span>  



| <span data-ttu-id="a2200-137">Stappen</span><span class="sxs-lookup"><span data-stu-id="a2200-137">Steps</span></span>                                      | <span data-ttu-id="a2200-138">Windows huidige en het wachtwoord-hash-synchronisatie</span><span class="sxs-lookup"><span data-stu-id="a2200-138">Windows current and password hash sync</span></span> | <span data-ttu-id="a2200-139">De huidige Windows- en Federatie</span><span class="sxs-lookup"><span data-stu-id="a2200-139">Windows current and federation</span></span> | <span data-ttu-id="a2200-140">Windows downlevel-</span><span class="sxs-lookup"><span data-stu-id="a2200-140">Windows down-level</span></span> |
| :--                                        | :-:                                    | :-:                            | :-:                |
| <span data-ttu-id="a2200-141">Stap 1: Een serviceverbindingspunt configureren</span><span class="sxs-lookup"><span data-stu-id="a2200-141">Step 1: Configure service connection point</span></span> | ![Selecteren][1]                            | ![Selecteren][1]                    | ![Selecteren][1]        |
| <span data-ttu-id="a2200-145">Stap 2: De uitgifte van claims instellen</span><span class="sxs-lookup"><span data-stu-id="a2200-145">Step 2: Setup issuance of claims</span></span>           |                                        | ![Selecteren][1]                    | ![Selecteren][1]        |
| <span data-ttu-id="a2200-148">Stap 3: Windows 10-apparaten inschakelen</span><span class="sxs-lookup"><span data-stu-id="a2200-148">Step 3: Enable non-Windows 10 devices</span></span>      |                                        |                                | ![Selecteren][1]        |
| <span data-ttu-id="a2200-150">Stap 4: Implementatie van het besturingselement en implementatie</span><span class="sxs-lookup"><span data-stu-id="a2200-150">Step 4: Control deployment and rollout</span></span>     | ![Selecteren][1]                            | ![Selecteren][1]                    | ![Selecteren][1]        |
| <span data-ttu-id="a2200-154">Stap 5: Controleren of de geregistreerde apparaten</span><span class="sxs-lookup"><span data-stu-id="a2200-154">Step 5: Verify registered devices</span></span>          | ![Selecteren][1]                            | ![Selecteren][1]                    | ![Selecteren][1]        |



## <a name="step-1-configure-service-connection-point"></a><span data-ttu-id="a2200-158">Stap 1: Een serviceverbindingspunt configureren</span><span class="sxs-lookup"><span data-stu-id="a2200-158">Step 1: Configure service connection point</span></span>

<span data-ttu-id="a2200-159">Het service connection point (SCP)-object wordt gebruikt door uw apparaten tijdens de registratie voor het detecteren van informatie over het Azure AD-tenant.</span><span class="sxs-lookup"><span data-stu-id="a2200-159">The service connection point (SCP) object is used by your devices during the registration to discover Azure AD tenant information.</span></span> <span data-ttu-id="a2200-160">Het SCP-object voor de automatische registratie van apparaten die lid zijn van een domein moet in uw lokale Active Directory (AD) bestaan in de configuratie van de naamgeving van de partitie van de context van de forest van de computer.</span><span class="sxs-lookup"><span data-stu-id="a2200-160">In your on-premises Active Directory (AD), the SCP object for the auto-registration of domain-joined devices must exist in the configuration naming context partition of the computer's forest.</span></span> <span data-ttu-id="a2200-161">Er is slechts één configuratienaamgevingscontext per forest.</span><span class="sxs-lookup"><span data-stu-id="a2200-161">There is only one configuration naming context per forest.</span></span> <span data-ttu-id="a2200-162">In een configuratie met meerdere forests met Active Directory moet het service connection point in alle forests met computers domein bestaan.</span><span class="sxs-lookup"><span data-stu-id="a2200-162">In a multi-forest Active Directory configuration, the service connection point must exist in all forests containing domain-joined computers.</span></span>

<span data-ttu-id="a2200-163">U kunt de [ **Get-ADRootDSE** ](https://technet.microsoft.com/library/ee617246.aspx) cmdlet voor het ophalen van de configuratienaamgevingscontext van het forest.</span><span class="sxs-lookup"><span data-stu-id="a2200-163">You can use the [**Get-ADRootDSE**](https://technet.microsoft.com/library/ee617246.aspx) cmdlet to retrieve the configuration naming context of your forest.</span></span>  

<span data-ttu-id="a2200-164">Voor een forest met de naam van de Active Directory-domein *fabrikam.com*, is de configuratienaamgevingscontext:</span><span class="sxs-lookup"><span data-stu-id="a2200-164">For a forest with the Active Directory domain name *fabrikam.com*, the configuration naming context is:</span></span>

`CN=Configuration,DC=fabrikam,DC=com`

<span data-ttu-id="a2200-165">Het SCP-object voor de automatische registratie van apparaten die lid zijn van een domein bevindt in uw forest zich op:</span><span class="sxs-lookup"><span data-stu-id="a2200-165">In your forest, the SCP object for the auto-registration of domain-joined devices is located at:</span></span>  

`CN=62a0ff2e-97b9-4513-943f-0d221bd30080,CN=Device Registration Configuration,CN=Services,[Your Configuration Naming Context]`

<span data-ttu-id="a2200-166">Afhankelijk van hoe u Azure AD Connect hebt geïmplementeerd, het SCP-object mogelijk al zijn geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="a2200-166">Depending on how you have deployed Azure AD Connect, the SCP object may have already been configured.</span></span>
<span data-ttu-id="a2200-167">U kunt controleren of het object bestaat en ophalen van de detectie van waarden met behulp van de volgende Windows PowerShell-script:</span><span class="sxs-lookup"><span data-stu-id="a2200-167">You can verify the existence of the object and retrieve the discovery values using the following Windows PowerShell script:</span></span> 

    $scp = New-Object System.DirectoryServices.DirectoryEntry;

    $scp.Path = "LDAP://CN=62a0ff2e-97b9-4513-943f-0d221bd30080,CN=Device Registration Configuration,CN=Services,CN=Configuration,DC=fabrikam,DC=com";

    $scp.Keywords;

<span data-ttu-id="a2200-168">De **$scp. Trefwoorden** uitvoer toont de Azure AD-tenant-informatie, bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="a2200-168">The **$scp.Keywords** output shows the Azure AD tenant information, for example:</span></span>

    azureADName:microsoft.com
    azureADId:72f988bf-86f1-41af-91ab-2d7cd011db47

<span data-ttu-id="a2200-169">Als het serviceverbindingspunt niet bestaat, kunt u dit maken door het uitvoeren van de `Initialize-ADSyncDomainJoinedComputerSync` cmdlet uit op uw Azure AD Connect-server.</span><span class="sxs-lookup"><span data-stu-id="a2200-169">If the service connection point does not exist, you can create it by running the `Initialize-ADSyncDomainJoinedComputerSync` cmdlet on your Azure AD Connect server.</span></span> <span data-ttu-id="a2200-170">Enterprise admin credential is vereist voor deze cmdlet uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="a2200-170">Enterprise admin credential is required to run this cmdlet.</span></span>  
<span data-ttu-id="a2200-171">De cmdlet:</span><span class="sxs-lookup"><span data-stu-id="a2200-171">The cmdlet:</span></span>

- <span data-ttu-id="a2200-172">Maakt het serviceverbindingspunt wordt gehost in Azure AD Connect is verbonden met Active Directory-forest.</span><span class="sxs-lookup"><span data-stu-id="a2200-172">Creates the service connection point in the Active Directory forest Azure AD Connect is connected to.</span></span> 
- <span data-ttu-id="a2200-173">Moet u opgeven de `AdConnectorAccount` parameter.</span><span class="sxs-lookup"><span data-stu-id="a2200-173">Requires you to specify the `AdConnectorAccount` parameter.</span></span> <span data-ttu-id="a2200-174">Dit is het account dat is geconfigureerd als Active Directory connector-account in Azure AD connect.</span><span class="sxs-lookup"><span data-stu-id="a2200-174">This is the account that is configured as Active Directory connector account in Azure AD connect.</span></span> 


<span data-ttu-id="a2200-175">Het volgende script toont een voorbeeld voor het gebruik van de cmdlet.</span><span class="sxs-lookup"><span data-stu-id="a2200-175">The following script shows an example for using the cmdlet.</span></span> <span data-ttu-id="a2200-176">In dit script `$aadAdminCred = Get-Credential` , moet u een gebruikersnaam typt.</span><span class="sxs-lookup"><span data-stu-id="a2200-176">In this script, `$aadAdminCred = Get-Credential` requires you to type a user name.</span></span> <span data-ttu-id="a2200-177">U moet de gebruikersnaam van de in de indeling van de principal-naam (User Principal Name) gebruiker opgeven (`user@example.com`).</span><span class="sxs-lookup"><span data-stu-id="a2200-177">You need to provide the user name in the user principal name (UPN) format (`user@example.com`).</span></span> 


    Import-Module -Name "C:\Program Files\Microsoft Azure Active Directory Connect\AdPrep\AdSyncPrep.psm1";

    $aadAdminCred = Get-Credential;

    Initialize-ADSyncDomainJoinedComputerSync –AdConnectorAccount [connector account name] -AzureADCredentials $aadAdminCred;

<span data-ttu-id="a2200-178">De `Initialize-ADSyncDomainJoinedComputerSync` cmdlet:</span><span class="sxs-lookup"><span data-stu-id="a2200-178">The `Initialize-ADSyncDomainJoinedComputerSync` cmdlet:</span></span>

- <span data-ttu-id="a2200-179">Maakt gebruik van de Active Directory PowerShell-module is afhankelijk van de Active Directory Web Services uitgevoerd op een domeincontroller.</span><span class="sxs-lookup"><span data-stu-id="a2200-179">Uses the Active Directory PowerShell module, which relies on Active Directory Web Services running on a domain controller.</span></span> <span data-ttu-id="a2200-180">Active Directory Web Services wordt ondersteund op domeincontrollers met Windows Server 2008 R2 en hoger.</span><span class="sxs-lookup"><span data-stu-id="a2200-180">Active Directory Web Services is supported on domain controllers running Windows Server 2008 R2 and later.</span></span>
- <span data-ttu-id="a2200-181">Wordt alleen ondersteund door de **MSOnline PowerShell moduleversie 1.1.166.0**.</span><span class="sxs-lookup"><span data-stu-id="a2200-181">Is only supported by the **MSOnline PowerShell module version 1.1.166.0**.</span></span> <span data-ttu-id="a2200-182">Deze module downloaden, gebruiken deze [koppeling](http://connect.microsoft.com/site1164/Downloads/DownloadDetails.aspx?DownloadID=59185).</span><span class="sxs-lookup"><span data-stu-id="a2200-182">To download this module, use this [link](http://connect.microsoft.com/site1164/Downloads/DownloadDetails.aspx?DownloadID=59185).</span></span>   

<span data-ttu-id="a2200-183">Gebruik het onderstaande script voor het maken van het service connection point voor domeincontrollers met Windows Server 2008 of eerdere versies.</span><span class="sxs-lookup"><span data-stu-id="a2200-183">For domain controllers running Windows Server 2008 or earlier versions, use the script below to create the service connection point.</span></span>

<span data-ttu-id="a2200-184">In een configuratie met meerdere forests, moet u het volgende script voor het maken van het service connection point in elk forest waar computers bestaan:</span><span class="sxs-lookup"><span data-stu-id="a2200-184">In a multi-forest configuration, you should use the following script to create the service connection point in each forest where computers exist:</span></span>
 
    $verifiedDomain = "contoso.com"    # Replace this with any of your verified domain names in Azure AD
    $tenantID = "72f988bf-86f1-41af-91ab-2d7cd011db47"    # Replace this with you tenant ID
    $configNC = "CN=Configuration,DC=corp,DC=contoso,DC=com"    # Replace this with your AD configuration naming context

    $de = New-Object System.DirectoryServices.DirectoryEntry
    $de.Path = "LDAP://CN=Services," + $configNC

    $deDRC = $de.Children.Add("CN=Device Registration Configuration", "container")
    $deDRC.CommitChanges()

    $deSCP = $deDRC.Children.Add("CN=62a0ff2e-97b9-4513-943f-0d221bd30080", "serviceConnectionPoint")
    $deSCP.Properties["keywords"].Add("azureADName:" + $verifiedDomain)
    $deSCP.Properties["keywords"].Add("azureADId:" + $tenantID)

    $deSCP.CommitChanges()


## <a name="step-2-setup-issuance-of-claims"></a><span data-ttu-id="a2200-185">Stap 2: De uitgifte van claims instellen</span><span class="sxs-lookup"><span data-stu-id="a2200-185">Step 2: Setup issuance of claims</span></span>

<span data-ttu-id="a2200-186">In een federatieve Azure AD-configuratie apparaten zijn afhankelijk van de Active Directory Federation Services (AD FS) of een 3e party on-premises federation-service om te verifiëren met Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a2200-186">In a federated Azure AD configuration, devices rely on Active Directory Federation Services (AD FS) or a 3rd party on-premises federation service to authenticate to Azure AD.</span></span> <span data-ttu-id="a2200-187">Apparaten verifiëren als u een toegangstoken registreren op basis van de Azure Active Directory Device Registration Service (DRS Azure).</span><span class="sxs-lookup"><span data-stu-id="a2200-187">Devices authenticate to get an access token to register against the Azure Active Directory Device Registration Service (Azure DRS).</span></span>

<span data-ttu-id="a2200-188">Windows huidige apparaten met behulp van geïntegreerde Windows-verificatie naar een actieve WS-Trust-eindpunt (1.3 of 2005 versies verifiëren) gehost door de lokale federation-service.</span><span class="sxs-lookup"><span data-stu-id="a2200-188">Windows current devices authenticate using Integrated Windows Authentication to an active WS-Trust endpoint (either 1.3 or 2005 versions) hosted by the on-premises federation service.</span></span>

> [!NOTE]
> <span data-ttu-id="a2200-189">Wanneer u AD FS, ofwel **adfs/services/trust/13/windowstransport** of **adfs/services/trust/2005/windowstransport** moet zijn ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="a2200-189">When using AD FS, either **adfs/services/trust/13/windowstransport** or **adfs/services/trust/2005/windowstransport** must be enabled.</span></span> <span data-ttu-id="a2200-190">Als u de webproxy verificatie gebruikt, zorg er ook voor dat dit eindpunt is gepubliceerd via de proxy.</span><span class="sxs-lookup"><span data-stu-id="a2200-190">If you are using the Web Authentication Proxy, also ensure that this endpoint is published through the proxy.</span></span> <span data-ttu-id="a2200-191">U kunt zien welke eindpunten worden ingeschakeld via de AD FS-beheerconsole onder **Service > eindpunten**.</span><span class="sxs-lookup"><span data-stu-id="a2200-191">You can see what end-points are enabled through the AD FS management console under **Service > Endpoints**.</span></span>
>
><span data-ttu-id="a2200-192">Als u geen AD FS als de lokale federation-service, volg de instructies van uw leverancier om ervoor te zorgen dat ze WS-Trust 1.3 of 2005 eindpunten en deze zijn gepubliceerd via het Metadata Exchange-bestand (MEX) ondersteunen.</span><span class="sxs-lookup"><span data-stu-id="a2200-192">If you don’t have AD FS as your on-premises federation service, follow the instructions of your vendor to make sure they support WS-Trust 1.3 or 2005 end-points and that these are published through the Metadata Exchange file (MEX).</span></span>

<span data-ttu-id="a2200-193">De volgende claims moeten bestaan in het token dat is ontvangen door Azure DRS voor apparaatregistratie te voltooien.</span><span class="sxs-lookup"><span data-stu-id="a2200-193">The following claims must exist in the token received by Azure DRS for device registration to complete.</span></span> <span data-ttu-id="a2200-194">Azure DRS maakt een apparaatobject in Azure AD met enkele van deze informatie die vervolgens door Azure AD Connect gebruikt wordt het zojuist gemaakte apparaatobject koppelen aan de computer account on-premises.</span><span class="sxs-lookup"><span data-stu-id="a2200-194">Azure DRS will create a device object in Azure AD with some of this information which is then used by Azure AD Connect to associate the newly created device object with the computer account on-premises.</span></span>

* `http://schemas.microsoft.com/ws/2012/01/accounttype`
* `http://schemas.microsoft.com/identity/claims/onpremobjectguid`
* `http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid`

<span data-ttu-id="a2200-195">Als u meer dan een geverifieerde domeinnaam hebt, moet u bieden de volgende claim voor computers:</span><span class="sxs-lookup"><span data-stu-id="a2200-195">If you have more than one verified domain name, you need to provide the following claim for computers:</span></span>

* `http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid`

<span data-ttu-id="a2200-196">Als u al een claim onveranderbare id genoemd (bijv, alternatieve aanmeldings-ID) moet u een overeenkomende claim voor computers:</span><span class="sxs-lookup"><span data-stu-id="a2200-196">If you are already issuing an ImmutableID claim (e.g., alternate login ID) you need to provide one corresponding claim for computers:</span></span>

* `http://schemas.microsoft.com/LiveID/Federation/2008/05/ImmutableID`

<span data-ttu-id="a2200-197">In de volgende secties vindt vinden u informatie over:</span><span class="sxs-lookup"><span data-stu-id="a2200-197">In the following sections, you find information about:</span></span>
 
- <span data-ttu-id="a2200-198">De waarden elke claim moet hebben.</span><span class="sxs-lookup"><span data-stu-id="a2200-198">The values each claim should have</span></span>
- <span data-ttu-id="a2200-199">Hoe een definitie eruit als in AD FS</span><span class="sxs-lookup"><span data-stu-id="a2200-199">How a definition would look like in AD FS</span></span>

<span data-ttu-id="a2200-200">De definitie helpt u om te controleren of de waarden aanwezig zijn of als u nodig hebt om ze te maken.</span><span class="sxs-lookup"><span data-stu-id="a2200-200">The definition helps you to verify whether the values are present or if you need to create them.</span></span>

> [!NOTE]
> <span data-ttu-id="a2200-201">Als u AD FS niet voor de lokale federation-server gebruikt, volgt u de leverancier van uw instructies voor het maken van de juiste configuratie om deze claims te verlenen.</span><span class="sxs-lookup"><span data-stu-id="a2200-201">If you don’t use AD FS for your on-premises federation server, follow your vendor's instructions to create the appropriate configuration to issue these claims.</span></span>

### <a name="issue-account-type-claim"></a><span data-ttu-id="a2200-202">Probleem account type claim</span><span class="sxs-lookup"><span data-stu-id="a2200-202">Issue account type claim</span></span>

<span data-ttu-id="a2200-203">**`http://schemas.microsoft.com/ws/2012/01/accounttype`**-Deze claim moet een waarde van bevatten **DJ**, die het apparaat als een domein gekoppelde computer identificeert.</span><span class="sxs-lookup"><span data-stu-id="a2200-203">**`http://schemas.microsoft.com/ws/2012/01/accounttype`** - This claim must contain a value of **DJ**, which identifies the device as a domain-joined computer.</span></span> <span data-ttu-id="a2200-204">U kunt een regel voor het transformeren van uitgifte die uitziet toevoegen in AD FS:</span><span class="sxs-lookup"><span data-stu-id="a2200-204">In AD FS, you can add an issuance transform rule that looks like this:</span></span>

    @RuleName = "Issue account type for domain-joined computers"
    c:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(
        Type = "http://schemas.microsoft.com/ws/2012/01/accounttype", 
        Value = "DJ"
    );

### <a name="issue-objectguid-of-the-computer-account-on-premises"></a><span data-ttu-id="a2200-205">Probleem objectGUID van de computer account on-premises</span><span class="sxs-lookup"><span data-stu-id="a2200-205">Issue objectGUID of the computer account on-premises</span></span>

<span data-ttu-id="a2200-206">**`http://schemas.microsoft.com/identity/claims/onpremobjectguid`**-Deze claim moet bevatten de **objectGUID** waarde van de lokale computeraccount.</span><span class="sxs-lookup"><span data-stu-id="a2200-206">**`http://schemas.microsoft.com/identity/claims/onpremobjectguid`** - This claim must contain the **objectGUID** value of the on-premises computer account.</span></span> <span data-ttu-id="a2200-207">U kunt een regel voor het transformeren van uitgifte die uitziet toevoegen in AD FS:</span><span class="sxs-lookup"><span data-stu-id="a2200-207">In AD FS, you can add an issuance transform rule that looks like this:</span></span>

    @RuleName = "Issue object GUID for domain-joined computers"
    c1:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    && 
    c2:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(
        store = "Active Directory", 
        types = ("http://schemas.microsoft.com/identity/claims/onpremobjectguid"), 
        query = ";objectguid;{0}", 
        param = c2.Value
    );
 
### <a name="issue-objectsid-of-the-computer-account-on-premises"></a><span data-ttu-id="a2200-208">Probleem objectSID van de computer account on-premises</span><span class="sxs-lookup"><span data-stu-id="a2200-208">Issue objectSID of the computer account on-premises</span></span>

<span data-ttu-id="a2200-209">**`http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid`**-Deze claim moet bevatten de de **objectSid** waarde van de lokale computeraccount.</span><span class="sxs-lookup"><span data-stu-id="a2200-209">**`http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid`** - This claim must contain the the **objectSid** value of the on-premises computer account.</span></span> <span data-ttu-id="a2200-210">U kunt een regel voor het transformeren van uitgifte die uitziet toevoegen in AD FS:</span><span class="sxs-lookup"><span data-stu-id="a2200-210">In AD FS, you can add an issuance transform rule that looks like this:</span></span>

    @RuleName = "Issue objectSID for domain-joined computers"
    c1:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    && 
    c2:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(claim = c2);

### <a name="issue-issuerid-for-computer-when-multiple-verified-domain-names-in-azure-ad"></a><span data-ttu-id="a2200-211">IssuerID voor computer uitgeven wanneer meerdere domeinnamen in Azure AD geverifieerd</span><span class="sxs-lookup"><span data-stu-id="a2200-211">Issue issuerID for computer when multiple verified domain names in Azure AD</span></span>

<span data-ttu-id="a2200-212">**`http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid`**-Deze claim moet de id URI (Uniform Resource) van een van de geverifieerde domeinnamen die verbinding met de lokale federation-service (AD FS of 3e partij maken) bevatten voor het uitgeven van het token.</span><span class="sxs-lookup"><span data-stu-id="a2200-212">**`http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid`** - This claim must contain the Uniform Resource Identifier (URI) of any of the verified domain names that connect with the on-premises federation service (AD FS or 3rd party) issuing the token.</span></span> <span data-ttu-id="a2200-213">U kunt in AD FS uitgifte transformatieregels die lijken op die hieronder in die specifieke volgorde na de bovenstaande waarden toevoegen.</span><span class="sxs-lookup"><span data-stu-id="a2200-213">In AD FS, you can add issuance transform rules that look like the ones below in that specific order after the ones above.</span></span> <span data-ttu-id="a2200-214">Houd er rekening mee dat één regel expliciet uitgeven van de regel voor gebruikers nodig is.</span><span class="sxs-lookup"><span data-stu-id="a2200-214">Please note that one rule to explicitly issue the rule for users is necessary.</span></span> <span data-ttu-id="a2200-215">Een eerste regel gebruiker versus computerverificatie identificeren in de onderstaande regels is toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="a2200-215">In the rules below, a first rule identifying user vs. computer authentication is added.</span></span>

    @RuleName = "Issue account type with the value User when its not a computer"
    NOT EXISTS(
    [
        Type == "http://schemas.microsoft.com/ws/2012/01/accounttype", 
        Value == "DJ"
    ]
    )
    => add(
        Type = "http://schemas.microsoft.com/ws/2012/01/accounttype", 
        Value = "User"
    );
    
    @RuleName = "Capture UPN when AccountType is User and issue the IssuerID"
    c1:[
        Type == "http://schemas.xmlsoap.org/claims/UPN"
    ]
    && 
    c2:[
        Type == "http://schemas.microsoft.com/ws/2012/01/accounttype", 
        Value == "User"
    ]
    => issue(
        Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", 
        Value = regexreplace(
        c1.Value, 
        ".+@(?<domain>.+)", 
        "http://${domain}/adfs/services/trust/"
        )
    );
    
    @RuleName = "Issue issuerID for domain-joined computers"
    c:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(
        Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", 
        Value = "http://<verified-domain-name>/adfs/services/trust/"
    );


<span data-ttu-id="a2200-216">In de bovenstaande claim</span><span class="sxs-lookup"><span data-stu-id="a2200-216">In the claim above,</span></span>

- <span data-ttu-id="a2200-217">`$<domain>`de URL van de service AD FS</span><span class="sxs-lookup"><span data-stu-id="a2200-217">`$<domain>` is the AD FS service URL</span></span>
- <span data-ttu-id="a2200-218">`<verified-domain-name>`is een tijdelijke aanduiding die u wilt vervangen door een van uw geverifieerde domeinnamen in Azure AD</span><span class="sxs-lookup"><span data-stu-id="a2200-218">`<verified-domain-name>` is a placeholder you need to replace with one of your verified domain names in Azure AD</span></span>



<span data-ttu-id="a2200-219">Zie voor meer informatie over geverifieerde domeinnamen [een aangepaste domeinnaam toevoegen aan Azure Active Directory](active-directory-add-domain.md).</span><span class="sxs-lookup"><span data-stu-id="a2200-219">For more details about verified domain names, see [Add a custom domain name to Azure Active Directory](active-directory-add-domain.md).</span></span>  
<span data-ttu-id="a2200-220">Als u een lijst van uw bedrijf geverifieerde domeinen, kunt u de [Get-MsolDomain](/powershell/module/msonline/get-msoldomain?view=azureadps-1.0) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="a2200-220">To get a list of your verified company domains, you can use the [Get-MsolDomain](/powershell/module/msonline/get-msoldomain?view=azureadps-1.0) cmdlet.</span></span> 

![Get-MsolDomain](./media/active-directory-conditional-access-automatic-device-registration-setup/01.png)

### <a name="issue-immutableid-for-computer-when-one-for-users-exist-eg-alternate-login-id-is-set"></a><span data-ttu-id="a2200-222">Onveranderbare id genoemd uitgeven voor computer, als een voor gebruikers bestaat (bijvoorbeeld alternatieve aanmeldings-ID is ingesteld)</span><span class="sxs-lookup"><span data-stu-id="a2200-222">Issue ImmutableID for computer when one for users exist (e.g. alternate login ID is set)</span></span>

<span data-ttu-id="a2200-223">**`http://schemas.microsoft.com/LiveID/Federation/2008/05/ImmutableID`**-Deze claim moet een geldige waarde voor computers bevatten.</span><span class="sxs-lookup"><span data-stu-id="a2200-223">**`http://schemas.microsoft.com/LiveID/Federation/2008/05/ImmutableID`** - This claim must contain a valid value for computers.</span></span> <span data-ttu-id="a2200-224">In AD FS, kunt u een regel voor het transformeren van uitgifte als volgt:</span><span class="sxs-lookup"><span data-stu-id="a2200-224">In AD FS, you can create an issuance transform rule as follows:</span></span>

    @RuleName = "Issue ImmutableID for computers"
    c1:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ] 
    && 
    c2:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(
        store = "Active Directory", 
        types = ("http://schemas.microsoft.com/LiveID/Federation/2008/05/ImmutableID"), 
        query = ";objectguid;{0}", 
        param = c2.Value
    );

### <a name="helper-script-to-create-the-ad-fs-issuance-transform-rules"></a><span data-ttu-id="a2200-225">Help-script voor het maken van de AD FS-uitgifte transformatieregels</span><span class="sxs-lookup"><span data-stu-id="a2200-225">Helper script to create the AD FS issuance transform rules</span></span>

<span data-ttu-id="a2200-226">Het volgende script helpt u bij het maken van de uitgifte transformeren regels die hierboven worden beschreven.</span><span class="sxs-lookup"><span data-stu-id="a2200-226">The following script helps you with the creation of the issuance transform rules described above.</span></span>

    $multipleVerifiedDomainNames = $false
    $immutableIDAlreadyIssuedforUsers = $false
    $oneOfVerifiedDomainNames = 'example.com'   # Replace example.com with one of your verified domains
    
    $rule1 = '@RuleName = "Issue account type for domain-joined computers"
    c:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(
        Type = "http://schemas.microsoft.com/ws/2012/01/accounttype", 
        Value = "DJ"
    );'

    $rule2 = '@RuleName = "Issue object GUID for domain-joined computers"
    c1:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    && 
    c2:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(
        store = "Active Directory", 
        types = ("http://schemas.microsoft.com/identity/claims/onpremobjectguid"), 
        query = ";objectguid;{0}", 
        param = c2.Value
    );'

    $rule3 = '@RuleName = "Issue objectSID for domain-joined computers"
    c1:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    && 
    c2:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(claim = c2);'

    $rule4 = ''
    if ($multipleVerifiedDomainNames -eq $true) {
    $rule4 = '@RuleName = "Issue account type with the value User when it is not a computer"
    NOT EXISTS(
    [
        Type == "http://schemas.microsoft.com/ws/2012/01/accounttype", 
        Value == "DJ"
    ]
    )
    => add(
        Type = "http://schemas.microsoft.com/ws/2012/01/accounttype", 
        Value = "User"
    );
    
    @RuleName = "Capture UPN when AccountType is User and issue the IssuerID"
    c1:[
        Type == "http://schemas.xmlsoap.org/claims/UPN"
    ]
    && 
    c2:[
        Type == "http://schemas.microsoft.com/ws/2012/01/accounttype", 
        Value == "User"
    ]
    => issue(
        Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", 
        Value = regexreplace(
        c1.Value, 
        ".+@(?<domain>.+)", 
        "http://${domain}/adfs/services/trust/"
        )
    );
    
    @RuleName = "Issue issuerID for domain-joined computers"
    c:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(
        Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", 
        Value = "http://' + $oneOfVerifiedDomainNames + '/adfs/services/trust/"
    );'
    }

    $rule5 = ''
    if ($immutableIDAlreadyIssuedforUsers -eq $true) {
    $rule5 = '@RuleName = "Issue ImmutableID for computers"
    c1:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ] 
    && 
    c2:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(
        store = "Active Directory", 
        types = ("http://schemas.microsoft.com/LiveID/Federation/2008/05/ImmutableID"), 
        query = ";objectguid;{0}", 
        param = c2.Value
    );'
    }

    $existingRules = (Get-ADFSRelyingPartyTrust -Identifier urn:federation:MicrosoftOnline).IssuanceTransformRules 

    $updatedRules = $existingRules + $rule1 + $rule2 + $rule3 + $rule4 + $rule5

    $crSet = New-ADFSClaimRuleSet -ClaimRule $updatedRules 

    Set-AdfsRelyingPartyTrust -TargetIdentifier urn:federation:MicrosoftOnline -IssuanceTransformRules $crSet.ClaimRulesString 

### <a name="remarks"></a><span data-ttu-id="a2200-227">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="a2200-227">Remarks</span></span> 

- <span data-ttu-id="a2200-228">Dit script worden de regels toegevoegd aan de bestaande regels.</span><span class="sxs-lookup"><span data-stu-id="a2200-228">This script appends the rules to the existing rules.</span></span> <span data-ttu-id="a2200-229">Het script niet twee keer uitgevoerd omdat de set regels tweemaal zou worden toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="a2200-229">Do not run the script twice because the set of rules would be added twice.</span></span> <span data-ttu-id="a2200-230">Zorg ervoor dat er geen overeenkomende regels bestaan voor deze claims (onder de bijbehorende voorwaarden) voordat u het script opnieuw uitvoert.</span><span class="sxs-lookup"><span data-stu-id="a2200-230">Make sure that no corresponding rules exist for these claims (under the corresponding conditions) before running the script again.</span></span>

- <span data-ttu-id="a2200-231">Als u meerdere geverifieerde domeinnamen (zoals weergegeven in de Azure AD-portal of via de cmdlet Get-MsolDomains) hebt, stel de waarde van **$multipleVerifiedDomainNames** in het script naar **$true**.</span><span class="sxs-lookup"><span data-stu-id="a2200-231">If you have multiple verified domain names (as shown in the Azure AD portal or via the Get-MsolDomains cmdlet), set the value of **$multipleVerifiedDomainNames** in the script to **$true**.</span></span> <span data-ttu-id="a2200-232">Controleer ook of u een bestaande issuerid claim die mogelijk zijn gemaakt met Azure AD Connect of via andere middelen.</span><span class="sxs-lookup"><span data-stu-id="a2200-232">Also make sure that you remove any existing issuerid claim that might have been created by Azure AD Connect or via other means.</span></span> <span data-ttu-id="a2200-233">Hier volgt een voorbeeld voor deze regel:</span><span class="sxs-lookup"><span data-stu-id="a2200-233">Here is an example for this rule:</span></span>


        c:[Type == "http://schemas.xmlsoap.org/claims/UPN"]
        => issue(Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", Value = regexreplace(c.Value, ".+@(?<domain>.+)",  "http://${domain}/adfs/services/trust/")); 

- <span data-ttu-id="a2200-234">Als u al uitgegeven een **onveranderbare id genoemd** claim voor gebruikersaccounts, stelt u de waarde van **$immutableIDAlreadyIssuedforUsers** in het script naar **$true**.</span><span class="sxs-lookup"><span data-stu-id="a2200-234">If you have already issued an **ImmutableID** claim  for user accounts, set the value of **$immutableIDAlreadyIssuedforUsers** in the script to **$true**.</span></span>

## <a name="step-3-enable-windows-down-level-devices"></a><span data-ttu-id="a2200-235">Stap 3: Eerdere Windows-apparaten inschakelen</span><span class="sxs-lookup"><span data-stu-id="a2200-235">Step 3: Enable Windows down-level devices</span></span>

<span data-ttu-id="a2200-236">Als sommige van uw apparaten domein Windows downlevel-apparaten, moet u naar:</span><span class="sxs-lookup"><span data-stu-id="a2200-236">If some of your domain-joined devices Windows down-level devices, you need to:</span></span>

- <span data-ttu-id="a2200-237">Stel een beleid in Azure AD, zodat gebruikers kunnen apparaten registreren.</span><span class="sxs-lookup"><span data-stu-id="a2200-237">Set a policy in Azure AD to enable users to register devices.</span></span>
 
- <span data-ttu-id="a2200-238">Configureren van de lokale federation-service voor het verlenen van claims voor de ondersteuning van **geïntegreerde Windows-verificatie (IWA)** voor apparaatregistratie.</span><span class="sxs-lookup"><span data-stu-id="a2200-238">Configure your on-premises federation service to issue claims to support **Integrated Windows Authentication (IWA)** for device registration.</span></span>
 
- <span data-ttu-id="a2200-239">Het verificatie-eindpunt van de Azure AD-apparaat toevoegen aan het lokale Intranet-zones certificaatmeldingen voorkomen wanneer het apparaat te verifiëren.</span><span class="sxs-lookup"><span data-stu-id="a2200-239">Add the Azure AD device authentication end-point to the local Intranet zones to avoid certificate prompts when authenticating the device.</span></span>

### <a name="set-policy-in-azure-ad-to-enable-users-to-register-devices"></a><span data-ttu-id="a2200-240">Beleid instellen in Azure AD, zodat gebruikers kunnen apparaten registreren</span><span class="sxs-lookup"><span data-stu-id="a2200-240">Set policy in Azure AD to enable users to register devices</span></span>

<span data-ttu-id="a2200-241">Voor het registreren van eerdere Windows-apparaten, moet u ervoor zorgen dat de instelling waarmee gebruikers apparaten registreren in Azure AD is ingesteld.</span><span class="sxs-lookup"><span data-stu-id="a2200-241">To register Windows down-level devices, you need to make sure that the setting to allow users to register devices in Azure AD is set.</span></span> <span data-ttu-id="a2200-242">U kunt deze instelling onder vinden in de Azure-portal:</span><span class="sxs-lookup"><span data-stu-id="a2200-242">In the Azure portal, you can find this setting under:</span></span>

`Azure Active Directory > Users and groups > Device settings`
    
<span data-ttu-id="a2200-243">Het volgende beleid moet worden ingesteld op **alle**: **gebruikers hun apparaten kunnen registreren met Azure AD**</span><span class="sxs-lookup"><span data-stu-id="a2200-243">The following policy must be set to **All**: **Users may register their devices with Azure AD**</span></span>

![Apparaten registreren](./media/active-directory-conditional-access-automatic-device-registration-setup/23.png)


### <a name="configure-on-premises-federation-service"></a><span data-ttu-id="a2200-245">Configureren van de lokale federation-service</span><span class="sxs-lookup"><span data-stu-id="a2200-245">Configure on-premises federation service</span></span> 

<span data-ttu-id="a2200-246">De lokale federation-service moet ondersteuning voor het uitgeven de **authenticationmehod** en **wiaormultiauthn** claims tijdens het ontvangen van een verificatieaanvraag naar de Azure AD relying party die een parameter resouce_params met een gecodeerde waarde, zoals hieronder wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="a2200-246">Your on-premises federation service must support issuing the **authenticationmehod** and **wiaormultiauthn** claims when receiving an authentication request to the Azure AD relying party holding a resouce_params parameter with an encoded value as shown below:</span></span>

    eyJQcm9wZXJ0aWVzIjpbeyJLZXkiOiJhY3IiLCJWYWx1ZSI6IndpYW9ybXVsdGlhdXRobiJ9XX0

    which decoded is {"Properties":[{"Key":"acr","Value":"wiaormultiauthn"}]}

<span data-ttu-id="a2200-247">Wanneer een dergelijke aanvraag afkomstig is, wordt de gebruiker met behulp van geïntegreerde Windows-verificatie moet worden geverifieerd door de lokale federation-service en dit lukt, moet deze de volgende twee claims uitgeven:</span><span class="sxs-lookup"><span data-stu-id="a2200-247">When such a request comes, the on-premises federation service must authenticate the user using Integrated Windows Authentication and upon success, it must issue the following two claims:</span></span>

    http://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/windows
    http://schemas.microsoft.com/claims/wiaormultiauthn

<span data-ttu-id="a2200-248">In AD FS, moet u een regel voor het transformeren van uitgifte die geeft via de verificatiemethode toevoegen.</span><span class="sxs-lookup"><span data-stu-id="a2200-248">In AD FS, you must add an issuance transform rule that passes-through the authentication method.</span></span>  

<span data-ttu-id="a2200-249">**Deze regel toevoegen:**</span><span class="sxs-lookup"><span data-stu-id="a2200-249">**To add this rule:**</span></span>

1. <span data-ttu-id="a2200-250">Ga in de AD FS-beheerconsole naar `AD FS > Trust Relationships > Relying Party Trusts`.</span><span class="sxs-lookup"><span data-stu-id="a2200-250">In the AD FS management console, go to `AD FS > Trust Relationships > Relying Party Trusts`.</span></span>
2. <span data-ttu-id="a2200-251">Met de rechtermuisknop op het Identiteitsplatform van Microsoft Office 365 relying party trust object en selecteer vervolgens **Claimregels bewerken**.</span><span class="sxs-lookup"><span data-stu-id="a2200-251">Right-click the Microsoft Office 365 Identity Platform relying party trust object, and then select **Edit Claim Rules**.</span></span>
3. <span data-ttu-id="a2200-252">Op de **uitgifte Transformatieregels** tabblad **regel toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="a2200-252">On the **Issuance Transform Rules** tab, select **Add Rule**.</span></span>
4. <span data-ttu-id="a2200-253">In de **claimregel** lijst met sjablonen, selecteer **Claims verzenden met een aangepaste regel**.</span><span class="sxs-lookup"><span data-stu-id="a2200-253">In the **Claim rule** template list, select **Send Claims Using a Custom Rule**.</span></span>
5. <span data-ttu-id="a2200-254">Selecteer **volgende**.</span><span class="sxs-lookup"><span data-stu-id="a2200-254">Select **Next**.</span></span>
6. <span data-ttu-id="a2200-255">In de **naam Claimregel** in het vak **Auth methode Claimregel**.</span><span class="sxs-lookup"><span data-stu-id="a2200-255">In the **Claim rule name** box, type **Auth Method Claim Rule**.</span></span>
7. <span data-ttu-id="a2200-256">In de **claimregel** typt u de volgende regel:</span><span class="sxs-lookup"><span data-stu-id="a2200-256">In the **Claim rule** box, type the following rule:</span></span>

    `c:[Type == "http://schemas.microsoft.com/claims/authnmethodsreferences"] => issue(claim = c);`

8. <span data-ttu-id="a2200-257">Typ op de federatieserver de PowerShell-opdracht hieronder na het vervangen  **\<RPObjectName\>**  met de relying party objectnaam voor uw Azure AD relying party trust-object.</span><span class="sxs-lookup"><span data-stu-id="a2200-257">On your federation server, type the PowerShell command below after replacing **\<RPObjectName\>** with the relying party object name for your Azure AD relying party trust object.</span></span> <span data-ttu-id="a2200-258">Dit object meestal heet **Identiteitsplatform van Microsoft Office 365**.</span><span class="sxs-lookup"><span data-stu-id="a2200-258">This object usually is named **Microsoft Office 365 Identity Platform**.</span></span>
   
    `Set-AdfsRelyingPartyTrust -TargetName <RPObjectName> -AllowedAuthenticationClassReferences wiaormultiauthn`

### <a name="add-the-azure-ad-device-authentication-end-point-to-the-local-intranet-zones"></a><span data-ttu-id="a2200-259">Het verificatie-eindpunt van de Azure AD-apparaat toevoegen aan de zones Lokaal Intranet</span><span class="sxs-lookup"><span data-stu-id="a2200-259">Add the Azure AD device authentication end-point to the Local Intranet zones</span></span>

<span data-ttu-id="a2200-260">Om te voorkomen dat certificaat wordt gevraagd wanneer gebruikers in het register apparaten verifiëren met Azure AD kunt u een beleid pushen naar uw apparaten domein de volgende URL toevoegen aan de zone Lokaal Intranet in Internet Explorer:</span><span class="sxs-lookup"><span data-stu-id="a2200-260">To avoid certificate prompts when users in register devices authenticate to Azure AD you can push a policy to your domain-joined devices to add the following URL to the Local Intranet zone in Internet Explorer:</span></span>

`https://device.login.microsoftonline.com`

## <a name="step-4-control-deployment-and-rollout"></a><span data-ttu-id="a2200-261">Stap 4: Implementatie van het besturingselement en implementatie</span><span class="sxs-lookup"><span data-stu-id="a2200-261">Step 4: Control deployment and rollout</span></span>

<span data-ttu-id="a2200-262">Wanneer u de vereiste stappen hebt voltooid, worden apparaten die lid zijn van een domein gereed voor het automatisch wordt geregistreerd bij Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a2200-262">When you have completed the required steps, domain-joined devices are ready to automatically register with Azure AD.</span></span> <span data-ttu-id="a2200-263">Alle domein op apparaten met Windows 10 Verjaardag Update en Windows Server 2016 automatisch registreren met Azure AD op het apparaat opnieuw wordt gestart of gebruikersaanmelding.</span><span class="sxs-lookup"><span data-stu-id="a2200-263">All domain-joined devices running Windows 10 Anniversary Update and Windows Server 2016 automatically register with Azure AD at device restart or user sign-in.</span></span> <span data-ttu-id="a2200-264">Nieuwe apparaten registreren met Azure AD wanneer het apparaat opnieuw wordt gestart nadat de domein-join-bewerking is voltooid.</span><span class="sxs-lookup"><span data-stu-id="a2200-264">New devices register with Azure AD when the device restarts after the domain join operation is completed.</span></span>

<span data-ttu-id="a2200-265">Apparaten die eerder in de werkplek is gekoppeld aan de overgang naar Azure AD (bijvoorbeeld voor Intune) '*lid van een domein, geregistreerd bij AAD*"; maar het duurt enige tijd voor dit proces te voltooien op alle apparaten als gevolg van de normale stroom van de domein- en gebruikersactiviteit.</span><span class="sxs-lookup"><span data-stu-id="a2200-265">Devices that were previously workplace-joined to Azure AD (for example for Intune) transition to “*Domain Joined, AAD Registered*”; however it takes some time for this process to complete across all devices due to the normal flow of domain and user activity.</span></span>

### <a name="remarks"></a><span data-ttu-id="a2200-266">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="a2200-266">Remarks</span></span>

- <span data-ttu-id="a2200-267">U kunt een Group Policy object gebruiken voor het beheren van de implementatie van automatische inschrijving van Windows 10 en Windows Server 2016 domein computers.</span><span class="sxs-lookup"><span data-stu-id="a2200-267">You can use a Group Policy object to control the rollout of automatic registration of Windows 10 and Windows Server 2016 domain-joined computers.</span></span>

- <span data-ttu-id="a2200-268">Windows 10 November 2015 automatisch bijwerken registers met Azure AD **alleen** als het groepsbeleidsobject van de implementatie is ingesteld.</span><span class="sxs-lookup"><span data-stu-id="a2200-268">Windows 10 November 2015 Update automatically registers with Azure AD **only** if the rollout Group Policy object is set.</span></span>

- <span data-ttu-id="a2200-269">De automatische registratie van Windows-computers voor downlevel-implementatie, u kunt implementeren een [Windows Installer-pakket](#windows-installer-packages-for-non-windows-10-computers) op computers die u selecteert.</span><span class="sxs-lookup"><span data-stu-id="a2200-269">To rollout the automatic registration of Windows down-level computers, you can deploy a [Windows Installer package](#windows-installer-packages-for-non-windows-10-computers) to computers that you select.</span></span>

- <span data-ttu-id="a2200-270">Als u het groepsbeleidsobject naar domein Windows 8.1-apparaten pushen, worden registratie geprobeerd; maar het wordt aangeraden dat u de [Windows Installer-pakket](#windows-installer-packages-for-non-windows-10-computers) al uw Windows downlevel-apparaten te registreren.</span><span class="sxs-lookup"><span data-stu-id="a2200-270">If you push the Group Policy object to Windows 8.1 domain-joined devices, registration will be attempted; however it is recommended that you use the [Windows Installer package](#windows-installer-packages-for-non-windows-10-computers) to register all your Windows down-level devices.</span></span> 

### <a name="create-a-group-policy-object"></a><span data-ttu-id="a2200-271">Een groepsbeleidsobject maken</span><span class="sxs-lookup"><span data-stu-id="a2200-271">Create a Group Policy object</span></span> 

<span data-ttu-id="a2200-272">Voor het beheren van de implementatie van automatische inschrijving van huidige Windows-computers, implementeert u de **Domeincomputers registreren als apparaten** groepsbeleidsobject voor de apparaten die u wilt registreren.</span><span class="sxs-lookup"><span data-stu-id="a2200-272">To control the rollout of automatic registration of Windows current computers, you should deploy the **Register domain-joined computers as devices** Group Policy object to the devices you want to register.</span></span> <span data-ttu-id="a2200-273">U kunt bijvoorbeeld het beleid implementeren naar een organisatie-eenheid of aan een beveiligingsgroep.</span><span class="sxs-lookup"><span data-stu-id="a2200-273">For example, you can deploy the policy to an organizational unit or to a security group.</span></span>

<span data-ttu-id="a2200-274">**Het beleid instellen:**</span><span class="sxs-lookup"><span data-stu-id="a2200-274">**To set the policy:**</span></span>

1. <span data-ttu-id="a2200-275">Open **Serverbeheer**, en ga vervolgens naar `Tools > Group Policy Management`.</span><span class="sxs-lookup"><span data-stu-id="a2200-275">Open **Server Manager**, and then go to `Tools > Group Policy Management`.</span></span>
2. <span data-ttu-id="a2200-276">Ga naar het knooppunt dat overeenkomt met het domein waar u wilt activeren, automatische registratie van de huidige Windows-computers.</span><span class="sxs-lookup"><span data-stu-id="a2200-276">Go to the domain node that corresponds to the domain where you want to activate auto-registration of Windows current computers.</span></span>
3. <span data-ttu-id="a2200-277">Met de rechtermuisknop op **Group Policy Objects**, en selecteer vervolgens **nieuw**.</span><span class="sxs-lookup"><span data-stu-id="a2200-277">Right-click **Group Policy Objects**, and then select **New**.</span></span>
4. <span data-ttu-id="a2200-278">Typ een naam voor uw groepsbeleidsobject.</span><span class="sxs-lookup"><span data-stu-id="a2200-278">Type a name for your Group Policy object.</span></span> <span data-ttu-id="a2200-279">Bijvoorbeeld: *automatische registratie bij Azure AD*.</span><span class="sxs-lookup"><span data-stu-id="a2200-279">For example, *Automatic Registration to Azure AD*.</span></span> <span data-ttu-id="a2200-280">Selecteer **OK**.</span><span class="sxs-lookup"><span data-stu-id="a2200-280">Select **OK**.</span></span>
5. <span data-ttu-id="a2200-281">Met de rechtermuisknop op uw nieuwe groepsbeleidsobject en selecteer vervolgens **bewerken**.</span><span class="sxs-lookup"><span data-stu-id="a2200-281">Right-click your new Group Policy object, and then select **Edit**.</span></span>
6. <span data-ttu-id="a2200-282">Ga naar **Computerconfiguratie** > **beleid** > **Beheersjablonen** > **Windows-onderdelen** > **apparaatregistratie**.</span><span class="sxs-lookup"><span data-stu-id="a2200-282">Go to **Computer Configuration** > **Policies** > **Administrative Templates** > **Windows Components** > **Device Registration**.</span></span> <span data-ttu-id="a2200-283">Met de rechtermuisknop op **Domeincomputers registreren als apparaten**, en selecteer vervolgens **bewerken**.</span><span class="sxs-lookup"><span data-stu-id="a2200-283">Right-click **Register domain-joined computers as devices**, and then select **Edit**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="a2200-284">Deze groepsbeleidssjabloon gewijzigd van eerdere versies van de console Groepsbeleidsbeheer.</span><span class="sxs-lookup"><span data-stu-id="a2200-284">This Group Policy template has been renamed from earlier versions of the Group Policy Management console.</span></span> <span data-ttu-id="a2200-285">Als u van een eerdere versie van de console gebruikmaakt, gaat u naar `Computer Configuration > Policies > Administrative Templates > Windows Components > Workplace Join > Automatically workplace join client computers`.</span><span class="sxs-lookup"><span data-stu-id="a2200-285">If you are using an earlier version of the console, go to `Computer Configuration > Policies > Administrative Templates > Windows Components > Workplace Join > Automatically workplace join client computers`.</span></span> 

7. <span data-ttu-id="a2200-286">Selecteer **ingeschakeld**, en selecteer vervolgens **toepassen**.</span><span class="sxs-lookup"><span data-stu-id="a2200-286">Select **Enabled**, and then select **Apply**.</span></span>
8. <span data-ttu-id="a2200-287">Selecteer **OK**.</span><span class="sxs-lookup"><span data-stu-id="a2200-287">Select **OK**.</span></span>
9. <span data-ttu-id="a2200-288">Het groepsbeleidsobject koppelen naar een locatie van uw keuze.</span><span class="sxs-lookup"><span data-stu-id="a2200-288">Link the Group Policy object to a location of your choice.</span></span> <span data-ttu-id="a2200-289">Bijvoorbeeld, kunt u deze koppelen aan een specifieke organisatie-eenheid.</span><span class="sxs-lookup"><span data-stu-id="a2200-289">For example, you can link it to a specific organizational unit.</span></span> <span data-ttu-id="a2200-290">U kan ook deze koppelen aan een specifieke beveiligingsgroep met computers die automatisch wordt geregistreerd bij Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a2200-290">You also could link it to a specific security group of computers that automatically register with Azure AD.</span></span> <span data-ttu-id="a2200-291">U dit beleid instellen voor alle Windows 10 en Windows Server 2016 Domeincomputers in uw organisatie, het groepsbeleidsobject aan het domein te koppelen.</span><span class="sxs-lookup"><span data-stu-id="a2200-291">To set this policy for all domain-joined Windows 10 and Windows Server 2016 computers in your organization, link the Group Policy object to the domain.</span></span>

### <a name="windows-installer-packages-for-non-windows-10-computers"></a><span data-ttu-id="a2200-292">Windows Installer-pakketten voor Windows 10-computers</span><span class="sxs-lookup"><span data-stu-id="a2200-292">Windows Installer packages for non-Windows 10 computers</span></span>

<span data-ttu-id="a2200-293">Als u wilt registreren domein Windows downlevel-computers in een federatieve omgeving, kunt u downloaden en installeren van deze Windows Installer-pakket (.msi) van Downloadcentrum op de [Microsoft Workplace Join voor Windows 10-computers](https://www.microsoft.com/en-us/download/details.aspx?id=53554) pagina.</span><span class="sxs-lookup"><span data-stu-id="a2200-293">To register domain-joined Windows down-level computers in a federated environment, you can download and install these Windows Installer package (.msi) from Download Center at the [Microsoft Workplace Join for non-Windows 10 computers](https://www.microsoft.com/en-us/download/details.aspx?id=53554) page.</span></span>

<span data-ttu-id="a2200-294">U kunt het pakket implementeren met behulp van een software-distributiesysteem zoals System Center Configuration Manager.</span><span class="sxs-lookup"><span data-stu-id="a2200-294">You can deploy the package by using a software distribution system like System Center Configuration Manager.</span></span> <span data-ttu-id="a2200-295">Het pakket ondersteunt de standard stille installatie-opties, waarbij de *stille* parameter.</span><span class="sxs-lookup"><span data-stu-id="a2200-295">The package supports the standard silent install options with the *quiet* parameter.</span></span> <span data-ttu-id="a2200-296">System Center Configuration Manager Current Branch biedt extra voordelen van eerdere versies, zoals de mogelijkheid om bij te houden van voltooide registraties.</span><span class="sxs-lookup"><span data-stu-id="a2200-296">System Center Configuration Manager Current Branch offers additional benefits from earlier versions, like the ability to track completed registrations.</span></span> <span data-ttu-id="a2200-297">Zie voor meer informatie [System Center Configuration Manager](https://www.microsoft.com/cloud-platform/system-center-configuration-manager).</span><span class="sxs-lookup"><span data-stu-id="a2200-297">For more information, see [System Center Configuration Manager](https://www.microsoft.com/cloud-platform/system-center-configuration-manager).</span></span>

<span data-ttu-id="a2200-298">Het installatieprogramma maakt een geplande taak op het systeem dat wordt uitgevoerd in de context van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="a2200-298">The installer creates a scheduled task on the system that runs in the user’s context.</span></span> <span data-ttu-id="a2200-299">De taak wordt geactiveerd wanneer de gebruiker zich aanmeldt bij Windows.</span><span class="sxs-lookup"><span data-stu-id="a2200-299">The task is triggered when the user signs in to Windows.</span></span> <span data-ttu-id="a2200-300">De taak wordt het apparaat achtergrond geregistreerd bij Azure AD met referenties van de gebruiker na verificatie met behulp van geïntegreerde Windows-verificatie.</span><span class="sxs-lookup"><span data-stu-id="a2200-300">The task silently registers the device with Azure AD with the user credentials after authenticating using Integrated Windows Authentication.</span></span> <span data-ttu-id="a2200-301">De geplande taak, het apparaat, Ga naar **Microsoft** > **Workplace Join**, en gaat u naar de bibliotheek voor Taakplanner.</span><span class="sxs-lookup"><span data-stu-id="a2200-301">To see the scheduled task, in the device, go to **Microsoft** > **Workplace Join**, and then go to the Task Scheduler library.</span></span>

## <a name="step-5-verify-registered-devices"></a><span data-ttu-id="a2200-302">Stap 5: Controleren of de geregistreerde apparaten</span><span class="sxs-lookup"><span data-stu-id="a2200-302">Step 5: Verify registered devices</span></span>

<span data-ttu-id="a2200-303">U kunt geslaagde geregistreerde apparaten in uw organisatie controleren met behulp van de [Get-MsolDevice](https://docs.microsoft.com/powershell/msonline/v1/get-msoldevice) cmdlet in de [Azure Active Directory PowerShell-module](/powershell/azure/install-msonlinev1?view=azureadps-2.0).</span><span class="sxs-lookup"><span data-stu-id="a2200-303">You can check successful registered devices in your organization by using the [Get-MsolDevice](https://docs.microsoft.com/powershell/msonline/v1/get-msoldevice) cmdlet in the [Azure Active Directory PowerShell module](/powershell/azure/install-msonlinev1?view=azureadps-2.0).</span></span>

<span data-ttu-id="a2200-304">De uitvoer van deze cmdlet toont de apparaten die zijn geregistreerd bij Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a2200-304">The output of this cmdlet shows devices registered in Azure AD.</span></span> <span data-ttu-id="a2200-305">Als u alle apparaten, gebruikt de **-alle** parameter, en ze filteren met behulp van de **deviceTrustType** eigenschap.</span><span class="sxs-lookup"><span data-stu-id="a2200-305">To get all devices, use the **-All** parameter, and then filter them using the **deviceTrustType** property.</span></span> <span data-ttu-id="a2200-306">Verbonden met het domein apparaten hebben een waarde van **domein**.</span><span class="sxs-lookup"><span data-stu-id="a2200-306">Domain joined devices have a value of **Domain Joined**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a2200-307">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a2200-307">Next steps</span></span>

* [<span data-ttu-id="a2200-308">Automatische apparaatregistratie Veelgestelde vragen</span><span class="sxs-lookup"><span data-stu-id="a2200-308">Automatic device registration FAQ</span></span>](active-directory-device-registration-faq.md)
* [<span data-ttu-id="a2200-309">Het oplossen van automatische registratie van domein computers toegevoegd aan Azure AD. – Windows 10 en Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="a2200-309">Troubleshooting auto-registration of domain joined computers to Azure AD – Windows 10 and Windows Server 2016</span></span>](active-directory-device-registration-troubleshoot-windows.md)
* [<span data-ttu-id="a2200-310">Het oplossen van automatische registratie van domein computers toegevoegd aan Azure AD. – Windows 10</span><span class="sxs-lookup"><span data-stu-id="a2200-310">Troubleshooting auto-registration of domain joined computers to Azure AD – non-Windows 10</span></span>](active-directory-device-registration-troubleshoot-windows-legacy.md)
* [<span data-ttu-id="a2200-311">Voorwaardelijke toegang van Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a2200-311">Azure Active Directory conditional access</span></span>](active-directory-conditional-access-azure-portal.md)



<!--Image references-->
[1]: ./media/active-directory-conditional-access-automatic-device-registration-setup/12.png
